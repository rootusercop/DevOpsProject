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

 1. Goto `Configure` option in Jenkins project.
 2. In Build Triggers, select the following options:

>-  Build when a change is pushed to github
>- Poll SCM

3. In the Schedule, type `*/5 * * * *` which indicates that the git repository will be polled for every 5 minutes.<br>
If a change is identified in the repository then the project will be build in Jenkins

![Build Trigger Configuration](https://github.com/nkatre/DevOpsProject/blob/master/Images/buildTrigger.png "Build Trigger Configuration")
