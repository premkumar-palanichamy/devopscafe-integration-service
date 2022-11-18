**TASK 1 :** 

List down and explain in a paragraph the various tools which are helpful to set up a CI/CD environment and provide your preference of toolset for a CI/CD environment that you will be setting up , along with the Pros and Cons. Provide a high-level diagram showing the various components involved.

1.	Source code repository : Git, BitBucket, Gitlab
2.	CICD Tool : Jenkins, AWS Codepipeline, Gitlab CICD
3.	Quality Analysis tool : Sonarqube
4.	Testing tool : Junit
5.	Deployment tool : AWS ECS, docker cluster on EC2
6.	Monitoring tool : Splunk, Nagios, Datadog 

### MY PREFERRED TOOLS :

***Source code repository : Git***

Pros:

`Good distributed model as each developer gets a local repository with a full history of commits which makes git fast compared to other VCs.

Branching capabilities and merging are easy (as they are cheap), good data integrity.

They are free and open-source we can easily download the source code and performs changes to it. They can handle larger projects efficiently.

The push/pull operations are faster with a simple They save time and developers can fetch and create pull requests without switching.

Data redundancy and replications. Add ons can be written in many languages.

They have good and faster network performance and superior disk utilization and they think about its data like a sequence of snapshots.

The object model is very simple and minimizes push/pull data transfers.`

Cons:

`GIT requires technical excellence and it is slower on windows. They have tedious command lines to input and don’t track renames.

They have poor GUI and usability. And also, they take a lot of resources which slows down the performance.

GIT doesn’t support checking out sub-trees. For each project, the central service would need to be set up for multiple package repositories.

It lacks window support and doesn’t track empty folders.
GIT needs multiple branches to support parallel developments used by the developers.

There is no built-in access control and doesn’t support binary files.

They do not provide access control mechanisms in case of security.`


***CICD Tool : Jenkins***

Pros:

`
Open Source and Free

Plug-ins and Integration

Hosting Option

Community Support

Integration with other CI/CD platforms

Keep your team in sync

Easy to debug

Less time to deliver the project

Flexible in creating the jobs

Source Code Management (SCM)

It makes the process of converting in GUI from CLI very easy.

It provides accurate data support to project management.

It supports many languages, like Java, Python, etc.`

Cons:

`Jenkins management is a tough nut to crack.

It runs on a server and requires server administrator abilities to keep track of all of its actions.

When compared to contemporary UI trends, it lacks user-friendliness in some areas.

Jenkins installation and configuration is a time-consuming operation.

When the settings are changed, the continuous integration pipeline breaks. The integration comes to a halt, and the developer must intervene.`




***Quality Analysis tool : Sonarqube***

Pros : 

`Enforces coding standards

It allows for cleaner code. 

Allows checking for methods with too many conditions(Systematic Complexity.)

Ensures every method is commented.

Can pick and choose what rules are active using SonarQube`

Cons :

`Take a longer time to complete coding.

Some rules may not fit your coding style. (These rules can be excluded.)

The increased quality, due to sonar, can sometimes explain from a business perspective.`

***Testing tool : Junit***

Pros :

`It helps you write better code.

It helps you catch bugs earlier.

It helps you detect regression bugs.

It makes your code easy to refactor.

It makes you more efficient at writing code.`

Cons :

`It takes time to write test cases.

It’s difficult to write tests for legacy code.

Tests require a lot of time for maintenance.

It can be challenging to test GUI code.

Unit testing can’t catch all errors.`

***Deployment tool : AWS ECS***

Pros :

`Serverless by default with AWS Fargate
Amazon ECS Anywhere : With ECS Anywhere, you can use the same familiar Amazon ECS console and operator tools to manage your on-premises container workloads for a consistent experience across your container-based applications.

Security and isolation by design
Autonomous control plane operations
Amazon ECS supports Docker and enables you to run and manage Docker containers.

Amazon ECS can be used with any third-party hosted Docker image repository or accessible private Docker registry, such as Docker Hub and Amazon Elastic Container Registry (ECR).

Amazon ECS provides you with a set of simple API actions to allow you to integrate and extend the service. 

Amazon ECS allows you to easily update your containers to new versions.

Blue/green deployments with AWS CodeDeploy help you minimize downtime during application updates.

The Amazon ECS will automatically recover unhealthy containers to ensure that you have the desired number of containers supporting your application.

Capacity Providers allow you to define flexible rules for how containerized workloads run on different types of compute capacity, and manage the scaling of the capacity.

Amazon Elastic File System (Amazon EFS) is a simple, scalable, fully managed elastic file system, enabling you to build modern applications, and persist and share data and state, from your Amazon ECS and AWS Fargate deployments.

Amazon ECS is integrated with Elastic Load Balancing, allowing you to distribute traffic across your containers using Application Load Balancers or Network Load Balancers.

Container security. EC2 instances reside in the Amazon VPC and a user can specify which instances are exposed to the internet. EC2 instances and ECS tasks also adhere to IAM roles, while security groups and network access control lists limit access to instances.`

Cons :

`You can’t alter the instance type or size when hibernation is enabled.

When you hibernate an instance, the data which is stored in the instance is lost.

You can’t hibernate any instance for more than 150 GB of RAM.`






***Monitoring tool : Nagios***

Pros :

`Nagios is open source software. It’s free to use and edit.

It has an open configuration which is easy to add a custom scripts to extend the services available.
There’re many devices which the Nagios system can monitor. The requirement is an SNMP protocol on that device.

Alert, notification or comment the status of the system. It has varieties of alert tools.

It has many plugins and add-ons which are free to download and develop.`

Cons :

`Many features are not available on a free version of Nagios. Features such as wizards or interactive dashboard are available on Nagios XI, which is very expensive.

There’re many configuration files which are very hard to configure.

Nagios core has a confusing interface.

Nagios can’t monitor network throughput (bandwidth uses or available).

Nagios can’t manage the network, just monitor the network.`

 



