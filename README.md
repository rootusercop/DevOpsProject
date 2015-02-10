DevOps Project
===================
Team :

 1. Nikhil Katre (nkatre@ncsu.edu)
 2. Pengyu Li (pli5@ncsu.edu)
 
Submission: **Milestone#1** <br>
Project Worked On: [WebGoat](https://github.com/nkatre/WebGoat) <br>

Evaluation
-------------

**Milestone#1** is evaluated based on the following
> **Evaluation Parameters:**

> - Triggered Builds - 20% <br>
> The ability to trigger a build in response to a git commit via a git hook.
> - Dependency Management - 20% <br>
> The ability to setup dependencies for the project and restore to a clean state.
> - Build Script Execution - 20%<br>
> The ability to execute a build script (e.g., shell, maven)
> - Multiple Nodes - 20%<br>
> The ability to run a build on multiple nodes (e.g. jenkins slaves, go agents, or a spawned droplet/AWS.).
> - Status - 20%<br>
> The ability to retrieve the status of the build via http.

----------

I. Triggered Builds
-------------------

We have used **Poll SCM** feature of Jenkins to achieve build trigger.<br>
The following steps were followed to achieve build trigger.<br>

 - Goto `Configure` option in Jenkins project.
 - In `Build Triggers`, select the options as shown in the image below

>-  Build when a change is pushed to github
>- Poll SCM

 - In the Schedule, type `*/5 * * * *` which indicates that the git
   repository will be polled for every 5 minutes.<br> If a change is
   identified in the repository then the project will be build in
   Jenkins

![Build Trigger Configuration](https://github.com/nkatre/DevOpsProject/blob/master/Images/buildTrigger.png "Build Trigger Configuration")

 - I create a sample file called **sampleFile** and add this to the project [WebGoat](https://github.com/nkatre/WebGoat)
 - In the next git poll, Jenkins identifies the changes made to the repository and hence builds the project automatically on identifying changes.

**Output of build triggered by changes to Project**
![BuildTriggeredByPoll](https://github.com/nkatre/DevOpsProject/blob/master/Images/pollOutput.png)
![BuildTriggeredByPoll](https://github.com/nkatre/DevOpsProject/blob/master/Images/pollOutput1.png)

----------


II. Dependency Management
-------------

#### <i class="icon-upload"></i> Build dependency and restore to a clean state

 1. We achieve this by configuring maven in Jenkins<br>
 2. In the Project Configuration, we invoke maven and set goal to `clean install`<br>
 3. To demonstrate this, a dependency is added in `pom.xml` file of the
    project<br>
 4. When the project is build then this dependency is also included in
    the project which can be seen in console output in Jenkins.

**Steps for maven configuration**

 5. Goto `Manage Jenkins` > `Configure System`.
 6. In `Maven Configuration`, set the following
![Maven Configuration](https://github.com/nkatre/DevOpsProject/blob/master/Images/mj_mavenConfig.png)
 7. Scroll down to `Maven` option and select to install maven automatically.
 8. In `Maven Project Configuration` select `Default` as `Local Maven Repository` as shown in the figure below
 ![Maven Config](https://github.com/nkatre/DevOpsProject/blob/master/Images/mj_mavenConfig.png)
 9. `Save` this configuration

**Steps for clean install**

 10. Goto Dashboard of Jenkins, select Project and click on `Configure`.
 11. Select `Build` > `Add a Build Step` > `Invoke Top Level Maven Targets`
 12. In this, select `Maven Version` as **maven** and in `Goals` we have to write **clean install** as mentioned in the following image.
 ![Maven Clean Install](https://github.com/nkatre/DevOpsProject/blob/master/Images/mavencleanInstall.png)

**Steps to add a dependency and build the project**

 13. We add a dependency ***commons-fileupload*** in `pom.xml` file of the project as follows
      ![Initial State](https://github.com/nkatre/DevOpsProject/blob/master/Images/dependency1.png)
      ![Added Dependancy](https://github.com/nkatre/DevOpsProject/blob/master/Images/dependency2.png)
 14. Now, go to the `Dashboard` of Jenkins and `Build` the Project

**Output of build after adding `"commons-fileupload"` dependency**
![dependency output](https://github.com/nkatre/DevOpsProject/blob/master/Images/commons-fileupload-dependency.png)
![dependency output](https://github.com/nkatre/DevOpsProject/blob/master/Images/common-fileupload.png)

----------


III. Build Script Execution
--------------------

 1. To demonstrate a build script execution, we have added a shell script
   file named `sampleScript.sh` in the
   [WebGoat](https://github.com/nkatre/WebGoat) project directory.
 2. The contents of `sampleScript.sh` file is an echo command which outputs "**Hello WebGoat**" to the console screen when the project is built

**Steps to demonstrate build script execution**

 1. Goto Dashboard of Jenkins, select Project and click on `Configure`.
 2. Select `Build` > `Add a Build Step` > `Execute Shell`
 3. In the `command`, write "***sh sampleScript.sh***" which will execute the shell script sampleScript.sh
 ![build script](https://github.com/nkatre/DevOpsProject/blob/master/Images/buildScript.png)
 4. Goto [WebGoat](https://github.com/nkatre/WebGoat) project directory and add a file `sampleScript.sh` which echoes "**Hello WebGoat**" to the console screen on execution
 ![sampleScript.sh](https://github.com/nkatre/DevOpsProject/blob/master/Images/Screenshot%20from%202015-02-09%2020:26:04.png)
 5.  Now goto Dashboard of Jenkins and build the project

**Output of build script execution**
![scriptExecution](https://github.com/nkatre/DevOpsProject/blob/master/Images/helloWebGoat.png)
