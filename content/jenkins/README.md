# Jenkins



- [Jenkins fundamentals](#jenkins-fundamentals)
- [Jenkins pipeline](#jenkins-pipeline)
- [Jenkins git integration](#jenkins-git-integration)
- [Jenkins master slave configuration](#jenkins-master-slave-configuration)
- [Docker Jenkins pipeline](#docker-jenkins-pipeline)
- [Maven Jenkins integration](#maven-jenkins-integration)
- [Selenium Jenkins integration](#selenium-jenkins-integration)
- [Jenkins groovy](#jenkins-groovy)
- [Webhooks in Jenkins](#webhooks-in-jenkins)
- [Email notification](#email-notification)
- [SonarQube Jenkins](#sonarqube-jenkins)
- [Jenkins X](#jenkins-x)
- [Misc](#misc).





### Jenkins fundamentals

**Jenkins** is an open-source Continuous Integration server written in Java for orchestrating a chain of actions to achieve the Continuous Integration process in an automated fashion. Jenkins supports the complete development life cycle of software from building, testing, documenting the software, deploying, and other stages of the software development life cycle.

Jenkins is a widely used application around the world that has around 300k installations and growing day by day. By using Jenkins, software companies can accelerate their software development process, as Jenkins can automate build and test at a rapid rate.

It is a server-based application and requires a web server like Apache Tomcat. The reason Jenkins software became so popular is that of its monitoring of repeated tasks which arise during the development of a project. For example, if your team is developing a project, Jenkins will continuously test your project builds and show you the errors in early stages of your development.



**What is continuous integration?**

Continuous Integration is a process of integrating code changes from multiple developers in a single project many times. The software is tested immediately after a code commit. With each code commit, code is built and tested. If the test is passed, the build is tested for deployment. If the deployment is successful, the code is pushed to production.

This commit, build, test, and deploy is a continuous process and hence the name continuous integration/deployment.

To use Jenkins, you need to create pipelines which are a series of steps that a Jenkins server will take. Jenkins Continuous Integration Pipeline is a powerful instrument that consists of a set of tools designed to **host**, **monitor**, **compile** and **test** code, or code changes.



**Jenkins plugins**

By default, Jenkins comes with a limited set of features. If you want to integrate your Jenkins installation with version control tools like Git, then you need to install plugins related to Git. In fact, for integration with tools like Maven, Amazon EC2, you need to install respective plugins in your Jenkins.



### Jenkins pipeline

In Jenkins, a pipeline is a collection of events or jobs which are interlinked with one another in a sequence. It is a combination of plugins that support the integration and implementation of **continuous delivery pipelines** using Jenkins.

In other words, a Jenkins Pipeline is a collection of jobs or events that brings the software from version control into the hands of the end users by using automation tools. It is used to incorporate continuous delivery in our software development workflow.

**Continuous delivery pipelines** - 

In a Jenkins pipeline, every job has some sort of dependency on at least one or more jobs or events. 

![](D:\MohdFurkan\knowledge\content\images\pipeline.png)

The above diagram represents a continuous delivery pipeline in Jenkins. It contains a collection of states such as build, deploy, test and release. These jobs or events are interlinked with each other. Every state has its jobs, which work in a sequence called a continuous delivery pipeline.

A continuous delivery pipeline is an automated expression to show your process for getting software for version control. Thus, every change made in your software goes through a number of complex processes on its manner to being released. It also involves developing the software in a repeatable and reliable manner, and progression of the built software through multiple stages of testing and deployment.



**Jenkins File**

Jenkins Pipeline can be defined by a text file called Jenkins File. You can implement pipeline as code using Jenkins File, and this can be defined by using a DSL (Domain Specific Language). With the help of Jenkins File, you can write the steps required for running a Jenkins Pipeline.

The benefits of using Jenkins File are:

- You can make pipelines automatically for all branches and can execute pull requests with just one Jenkins File.
- You can review your code on the pipeline.
- You can review your Jenkins pipeline.
- This is the singular source for your pipeline and can be customized by multiple users.

Jenkins File can be defined by using either Web UI or with a Jenkins File.

**Pipeline syntax**

Two types of syntax are used for defining your Jenkins File.

- Declarative
- Scripted

**Declarative**

Declarative pipeline syntax offers a simple way to create pipelines. It consists of a predefined hierarchy to create Jenkins pipelines. It provides you the ability to control all aspects of a pipeline execution in a simple, straightforward manner. 

**Scripted**

Scripted Jenkins pipeline syntax runs on the Jenkins master with the help of a lightweight executor. It uses very few resources to convert the pipeline into atomic commands.

Both scripted and declarative syntax are different from each other and are defined totally differently.

**Syntax of Jenkins Files**

```jenkins

pipeline {  
    agent any  
    stages {  
            stage ('Build') {  
                steps {  
                        echo 'Running build phase...'  
                }  
            }  
    }  
}  
```

 

**Jenkins workflow**

![](D:\MohdFurkan\knowledge\content\images\jenkins_workflow.png)



### Jenkins git integration

For git integration we need to add plugin-in, after that we can use GIT for getting source code in a job. Git option will asks you to provide repository, branch, username and password to authentication.



### Jenkins master slave configuration

**Jenkins Architecture**

![](D:\MohdFurkan\knowledge\content\images\jenkins_arch.png)



**Jenkins master slave configuration**

![](D:\MohdFurkan\knowledge\content\images\jenkins_master.png)



The use of this master slave architecture is to manage the distributed builds so in this architecture the master and slave communicate through TCP protocol so if you talk about Jenkins master your main Jenkins server is the master so there are few responsibilities of Jenkins master in this architecture so say for example scheduling build jobs, dispatching builds to the slaves for actual execution, monitoring the slaves possibly taking them online and offline whenever required, recording  and presenting the build results, a master instance of Jenkins can also execute build jobs directly so this was about the Jenkins master, so if you talk about Jenkins slaves, a slave is a java executable that runs on a remote machine so what are the responsibilities of the Jenkins slave. So slave hears requests from the Jenkins master instance. Slaves can run on variety of operating systems, so you can have one slave working on a different operating system say for example Linux, Windows, etc. So the job of slave is to do as they are told to which involves executing build jobs dispatched by the master. You can configure a project to always run on a particular slave machine or a particular type of slave machine or simply let Jenkins pick up the next available slave. 

**Working of master and slave Jenkins**

![](D:\MohdFurkan\knowledge\content\images\jenkins_master_working.png)



**Configuration**

Manage Jenkins > Manage nodes and clouds > New node



### Docker Jenkins pipeline

![](D:\MohdFurkan\knowledge\content\images\docker_jenkins.png)

### 

