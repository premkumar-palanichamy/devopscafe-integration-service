**TASK 3 :** 
- Create a Jenkins Pipeline job for merge requests

- Create a new build job of type “Pipeline” in Jenkins with the following parameters:
1.	Enable this checkbox in build triggers: “Build when a change is pushed to GitLab”. If it is not available, install Gitlab Hook Plugin in Jenkins.

2.	Copy the displayed “GitLab CI Service URL” (e.g., “https://my-jenkins/jenkins/project/my_project&#8221;), you will need it later for GitLab configuration.

3.	Check events that should trigger builds on Jenkins. I personally like these three events: “Merge Request”, “Push to source branch” and “Comment”.

***Configure Web Hooks in your GitLab project***

Open your project in GitLab and go to GitLab Web Hooks in project settings.

Add the following web hook:
1.	URL: paste the “GitLab CI Service URL” that you copied from the build job configuration in Jenkins. (e.g., “https://my-jenkins/jenkins/project/my_project&#8221;)

2.	Enable the following triggers: “Merge request events”, “Push events”, “Comments”

When a build job is triggered by a GitLab Web Hook, there are several additional environment variables provided by the Gitlab Hook Plugin, such as gitlabSourceBranch and gitlabTargetBranch. We will use these additional variables to checkout and merge the required branches in Jenkinsfile.

The provided scm object contains only one repository to fetch the Jenkinsfile, therefore we need to configure two different repositories for two reasons:

•	The source and target branches of the merge request are not necessarily the branches that Jenkins used to fetch the Jenkinsfile. Remember, the scm object represents the repository of the Jenkinsfile for the build job.

•	The source branch of the merge request might originate from a different repository than the target branch.

Therefore, the only use of the scm object in this case is to obtain the Jenkins credentials ID for accessing the Git repositories.

##### JENKINSFILE

```
#!groovy
def handleCheckout = {
	if (env.gitlabMergeRequestId) {
                         sh "echo 'Merge request detected. Merging…'"
		def credentialsId = scm.userRemoteConfigs[0].credentialsId
		checkout ([
			$class: 'GitSCM',
			branches: [[name: "${env.gitlabSourceNamespace}/${env.gitlabSourceBranch}"]],
			extensions: [
				[$class: 'PruneStaleBranch'],
				[$class: 'CleanCheckout'],
				[
					$class: 'PreBuildMerge',
					options: [
						fastForwardMode: 'NO_FF',
						mergeRemote: env.gitlabTargetNamespace,
						mergeTarget: env.gitlabTargetBranch
					]
				]
			],
			userRemoteConfigs: [
				[
					credentialsId: credentialsId,
					name: env.gitlabTargetNamespace,
					url: env.gitlabTargetRepoSshURL
				],
				[
					credentialsId: credentialsId,
					name: env.gitlabSourceNamespace,
					url: env.gitlabSourceRepoSshURL
				]
			]
		])
	} else {
		sh "echo 'No merge request detected. Checking out current branch'"
		checkout ([
			$class: 'GitSCM',
			branches: scm.branches,
			extensions: [
					[$class: 'PruneStaleBranch'],
					[$class: 'CleanCheckout']
			],
			userRemoteConfigs: scm.userRemoteConfigs
		])
	}
}
node() {
	stage('setup') {
		sh "env | sort"
		handleCheckout()
		sh "git branch -vv"
	}

stage('Build .JAR') {
            steps {
                // clean 
                dir("Project-app/"){
                    sh "mvn versions:set versions:commit -DnewVersion=${env.sourceVersionTag}-${env.ProjectGitHash}"
                    sh 'mvn clean install'
                    
                }
            }      
        }
stage('Move .JAR'){
            steps {
                sh "ls -la"
                sh 'pwd'
                sh "ls -la '${env.WORKSPACE}/Project-app/target'"
                sh "mv '${env.WORKSPACE}/Project-app/target/exancloud-${env.sourceVersionTag}-${env.ProjectGitHash}.jar' '${env.WORKSPACE}/Project_devops/SampleProject/jenkins/docker/Project-app/'"
                sh "cp '${env.WORKSPACE}/Project_devops/SampleProject/${params.ENV_NAME}/${params.ENV_NAME}_ssh_public_key.txt' '${env.WORKSPACE}/Project_devops/SampleProject/jenkins/docker/Project-app/ssh_public_key.txt'"
                
            }
        }
stage('Terminate existing ECS tasks'){
            when {
                expression {
                    params.DoTerminateExisting == true
                }
            }             
            steps {
		//set the env name to file to get the value from sh block
		sh "echo ${params.ENV_NAME} > env.txt"
				
		sh '''#!/bin/bash -xe
		       env=$(<env.txt)
	                     cluster="${env}-cluster"
		      project="${env}-app"
		      result=\$(aws ecs list-tasks --cluster ${cluster} --service ${project} --output text)
		     tasks=(${result//TASKARNS/ })
		     length=\$(echo ${#tasks[@]})
		     for (( c=0; c<length; c++ )); do echo $c; output=$(aws ecs stop-task --cluster                        ${cluster} --task ${tasks[$c]}); done
				'''
						
			}
		}
	stage('test') {
		sh "echo 'Throw in some tests here'"
	}
}
```