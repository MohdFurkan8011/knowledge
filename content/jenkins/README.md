# Jenkins



- [Jenkins fundamentals](#jenkins-fundamentals)
- [CI/CD pipeline](#ci/cd-pipeline)
- [Jenkins git integration](#jenkins-git-integration)
- [Docker Jenkins pipeline](#docker-jenkins-pipeline)
- [Maven Jenkins integration](#maven-jenkins-integration)
- [Selenium Jenkins integration](#selenium-jenkins-integration)
- [Jenkins groovy](#jenkins-groovy)
- [Webhooks in Jenkins](#webhooks-in-jenkins)
- [Email notification](#email-notification)
- [SonarQube Jenkins](#sonarqube-jenkins)
- [Jenkins X](#jenkins-x)
- [Misc](#misc)





### Jenkins fundamentals

**Jenkins** is an open-source Continuous Integration server written in Java for orchestrating a chain of actions to achieve the Continuous Integration process in an automated fashion. Jenkins supports the complete development life cycle of software from building, testing, documenting the software, deploying, and other stages of the software development life cycle.

Jenkins is a widely used application around the world that has around 300k installations and growing day by day. By using Jenkins, software companies can accelerate their software development process, as Jenkins can automate build and test at a rapid rate.

It is a server-based application and requires a web server like Apache Tomcat. The reason Jenkins software became so popular is that of its monitoring of repeated tasks which arise during the development of a project. For example, if your team is developing a project, Jenkins will continuously test your project builds and show you the errors in early stages of your development.



**What is continuous integration?**

Continuous Integration is a process of integrating code changes from multiple developers in a single project many times. The software is tested immediately after a code commit. With each code commit, code is built and tested. If the test is passed, the build is tested for deployment. If the deployment is successful, the code is pushed to production.

This commit, build, test, and deploy is a continuous process and hence the name continuous integration/deployment.

To use Jenkins, you need to create pipelines which are a series of steps that a Jenkins server will take. Jenkins Continuous Integration Pipeline is a powerful instrument that consists of a set of tools designed to **host**, **monitor**, **compile** and **test** code, or code changes.



**Jenkins plugins**

By default, Jenkins comes with a limited set of features. If you want to integrate your Jenkins installation with version control tools like Git, then you need to install plugins related to Git. In fact, for integration with tools like Maven, Amazon EC2, you need to install respective plugins in your jenkins.



