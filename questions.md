This work sample requires you to do the following things.
1. List down and explain in a paragraph the various tools which are helpful to set up a CI/CD
environment and provide your preference of toolset for a CI/CD environment that you will be
setting up , along with the Pros and Cons. Provide a high-level diagram showing the various
components involved.
2. How do you manage security credentials in a CI/CD environment, such that only the relevant
people who need access to the credentials will be able to access it? For Example, you could
take Jenkins as an example environment (or other environments based on your experience).
Provide the approach you will take.
3. Let’s assume we have this repository/module by the name of the integration-service in a
version control system of choice. Assignment is to design a CI/CD Pipeline for the above
module. Below are the requirements mentioned for the CI/CD pipeline (Jenkins is the tools of preference, feel free to chose otherwise)

● Build is triggered when Pull Request/Merge Request (source) is raised

● Build is triggered for the release branch when the feature/hot-fix branch gets merged in it.

● Build is triggered for the master branch when the release branch is merged in it.

● Build is triggered when a commit is made to feature/hotfix branch 

Include the minimal CI/CD pipeline stages as per your understanding, on top of that include
additional stages per branch type, as mentioned below :-

__feature/hotfix__

● Add an additional stage to create and store artefact at location (as per your understanding)

__release__

● Add an additional stage to create and store artefact at location (as per your understanding)

● Add an additional stage to, to deploy the artefact (Standalone Server/Kubernetes)
and send email on status of the deployment to the team DL and developer who made the last commit.

● Add an additional stage to, to trigger smoke and UAT tests and share the results with
the qa team.

__Master__

● Add an additional stage to create and store artefact at location (as per your understanding)

● Add an additional stage to, to deploy the artefact (Standalone Server/Kubernetes)
after approval and email on status of the deployment to engineering DL and developer who made the last commit.

● Add an additional stage to, to trigger post release tests and share the results with the qa team

As a last stage of all pipelines, send email to the team DL,developer who made the last
commit about the build results, branch being built, commit being built.

___Expectations on problem 3:___

1. Design Document of the various stages of CI/CD across different branch types.
2. Jenkinsfile covering all requirements (if Jenkins is the choice, otherwise snippets of
implementation from your preferred choice of CI tool) , even a git repo link will work.

DELIVERABLES

1.	Documentation including Diagram for Problem 1 and 2.
2. Code and Instructions on how to run for Problem 3.