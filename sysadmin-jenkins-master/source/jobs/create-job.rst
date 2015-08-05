.. _create-job:

###############
Setting up jobs
###############

============
Introduction
============

A job is a particular way of compiling, testing, packaging, deploying or otherwise doing something
with your project. Build jobs come in a variety of forms; you may want to compile and unit test your
application, report on code quality metrics related to the source code, generate documentation, bundle
up an application for a release, deploy it to production, run an automated smoke test, or do any number
of other similar tasks.

======================
Setting up the project
======================

Go to Jenkins top page, select "New Job", then choose "Build a free-style software project". This job type consists of the following elements:

- optional SCM, such as CVS or Subversion where your source code resides.
- optional triggers to control when Jenkins will perform builds.
- some sort of build script that performs the build (ant, maven, shell script, batch file, etc.) where the real work happens
- optional steps to collect information out of the build, such as archiving the artifacts and/or recording javadoc and test results.
- optional steps to notify other people/systems with the build result, such as sending e-mails, IMs, updating issue tracker, etc.

.. warning::
   Jenkins Set Environment Variable Jenkins sets some environment variables that are available to shell scripts, Windows batch files, Ant and Maven^1^ files that are executed by Jenkins. A list of environment variables and how they are used are shown below.

======================================
Builds for Non-Source Control Projects
======================================

There is sometimes a need to build a project simply for demonstration purposes or access to a SVN/CVS repository is unavailable. By choosing to configure the project  as "None

==================== =====================================================================================================================================================================================================================================
Environment Variable Description 
==================== =====================================================================================================================================================================================================================================
BUILD_NUMBER         The current build number, such as "153"
BUILD_ID             The current build id, such as "2005-08-22_23-59-59" (YYYY-MM-DD_hh-mm-ss, defunct since version 1.597)
BUILD_URL            The URL where the results of this build can be found (e.g. http://buildserver/jenkins/job/MyJobName/666/)
NODE_NAME            The name of the node the current build is running on. Equals 'master' for master node.
JOB_NAME             Name of the project of this build. This is the name you gave your job when you first set it up. It's the third column of the Jenkins Dashboard main page.
BUILD_TAG            String of jenkins-${JOB_NAME}-${BUILD_NUMBER}. Convenient to put into a resource file, a jar file, etc for easier identification.
JENKINS_URL          Set to the URL of the Jenkins master that's running the build. This value is used by Jenkins CLI for example
EXECUTOR_NUMBER      The unique number that identifies the current executor (among executors of the same machine) that's carrying out this build. This is the number you see in the "build executor status", except that the number starts from 0, not 1. 
JAVA_HOME            If your job is configured to use a specific JDK, this variable is set to the JAVA_HOME of the specified JDK. When this variable is set, PATH is also updated to have $JAVA_HOME/bin.
WORKSPACE            The absolute path of the workspace.
SVN_REVISION         For Subversion-based projects, this variable contains the revision number of the module. If you have more than one module specified, this won't be set.
CVS_BRANCH           For CVS-based projects, this variable contains the branch of the module. If CVS is configured to check out the trunk, this environment variable will not be set.
GIT_COMMIT           For Git-based projects, this variable contains the Git hash of the commit checked out for the build (like ce9a3c1404e8c91be604088670e93434c4253f03) ﻿(all the GIT_* variables require git plugin)|
GIT_URL              For Git-based projects, this variable contains the Git url (like git@github.com:user/repo.git or [https://github.com/user/repo.git)]
GIT_BRANCH           For Git-based projects, this variable contains the Git branch that was checked out for the build (normally origin/master)
==================== =====================================================================================================================================================================================================================================

===========================================
Promoted Build Plugin Environment Variables
===========================================

If you are using the Promoted Build Plugin, you will have access to the following environment variables. This allows you to access information about your Jenkins build since certain environment variables stated above (such as BUILD_TAG now refer to the Promoted Build Plugin's job.

==================== ============ ==============================================================================================================================================
Environment Variable Replaces     Description
==================== ============ ==============================================================================================================================================
PROMOTED_URL         BUILD_URL    The URL of the original Jenkins job that is involved with the promotion. BUILD_URL now refers to the Promotion's URL
PROMOTED_JOB_NAME    JOB_NAME     The name of the original Jenkins job that is involved with the promotion. JOB_NAME now refers to the Promotion's job's name
PROMOTED_NUMBER	     BUILD_NUMBER The Build Number of the job being promoted. BUILD_NUMBER now refer's the the Promotion Number
PROMOTED_ID	         BUILD_ID     The Build ID (ex. "2005-08-22_23-59-59" (YYYY-MM-DD_hh-mm-ss) ) of the original Jenkins job. BUILD_ID now refer's to the Promotion's build ID.
==================== ============ ==============================================================================================================================================

========================================
Shell Scripts and Windows Batch Commands
========================================

If you're using a shell script to do your build, you can either put these environment variables directly into your shell scripts, or call them as parameters in your shell script. Below is an example how this can be done:

.. image:: img/shell_script.jpg

If you are executing a Windows Batch Command, the variables should be referenced using the %VARIABLE_NAME% pattern. For example:

.. image:: img/WindowsBatchCmdHudsonExample.GIF

