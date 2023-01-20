# datastore-deployment repo overview

The datastore-deployment repo manages deployment-specific artifacts for installations using the [datastore-support](https://github.com/craigmcchesney/datastore-support) repo.  Please see the readme for that repo for additional details.

The intention for this repo is to use a branch for each deployed system, and I'd suggest starting with a tarball installation for a recent deployment when creating a new one.  Once the directory structure and contents are better understood, maybe I'll switch to using a template for new deployments but for now that would be overkill as the only contents are config files for setting up the environment.

## directories

### bin

The idea for the bin directory is to create symbolic links to system tools that might not always be installed in the same location so that the scripts in datastore-deployment can access them from a common location.  For example, the directory includes a link to "mvn", which in the case of one deployment is installed in "/opt/apache-maven-3.8.7/bin/mvn".

### custom

The custom directory contains items whose purpose is to customize the datastore-support environment.  The subdirectories are described in more detail below.

#### cron

* Contains the crontab file for the user whose home directory is used for datastore-support and datastore-deployment.  
* The datastore-support repo includes crontab templates for both production/demo/test and development systems.

#### env

* Contains config files to customize the datastore-support environment, defining environment variables that are utilized by the scripts in that repo.  
* The gitignore file excludes the password config file so that it's not stored on github, so it might be better to start with a full tarball copy of an existing deployment than cloning a git repo to create a new branch of datastoreo-deployment.  
* Currently this directory includes two files, datastore-env-passwd and datastore-env-vars.  The former defines environment variables for the influxdb token and mongodb password that are needed to start up those services and the Java application that uses them.  The latter defines other environment variables to support those same services and applications.
