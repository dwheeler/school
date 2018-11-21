# Professor M's School for Gifted Coders [![Build Status](https://travis-ci.org/sugarcrm/school.svg?branch=windows-build-pack-php)](https://travis-ci.org/sugarcrm/school)

Professor M's School for Gifted Coders is a module loadable package that can be installed in Sugar.  The following 
sections explain more about the scenario and how to install the package and sample data.

## Contents
[About the scenario](#about-the-scenario) 

[Installation instructions](#installation-instructions) 

[Setting up your development environment](#setting-up-your-development-environment) 

[Contribute to this project](#contribute-to-this-project)

[Generating the Professor M module loadable packages locally](#generating-the-professor-m-module-loadable-packages-locally) 

[Continuous integration with Travis CI](#continuous-integration-with-travis-ci) 

[Continuous integration with Jenkins](#continuous-integration-with-jenkins) 

[Automated tests](#automated-tests)

[How to fix your Sugar instance without starting completely over](#how-to-fix-your-sugar-instance-without-starting-completely-over)

## About the scenario
Professor M aka Professor Marum has created an exclusive not-for-profit school for gifted coders.  

Learn more about the implemented [Use Cases](docs/UseCases.md) in the [docs](docs/).

Want a quick summary? Watch the video below.
[![The Professor M Scenario Part 1 - What is it and why should you care?](images/profmvideo1.png)](https://youtu.be/aKBTKcaney4 "The Professor M Scenario Part 1 - What is it and why should you care?")

## Installation instructions

Watch the video below for instructions on how to install the scenario.  Text-based instructions follow.
[![The Professor M Scenario Part 2 - How do you install it?](images/profmvideo2.png)](https://youtu.be/SO-Rav35X5U "The Professor M Scenario Part 2 - How do you install it?")

### Prerequisites
- Sugar 7.9.1.0 (or newer) installed with NO sample data.  See [Getting Started with Sugar Development](https://developer.sugarcrm.com/getting-started) for help.
   * Note:  If you install Sugar using ***config_si.php***, ensure that the `disable_unknown_platforms` property is set to `false` or is not in the file.
   * Note for Windows users:  Make the path to your Sugar instance as short as possible to avoid errors of file paths being too long.
- [Postman](https://www.getpostman.com) installed 

### Install the modules and customizations
We've created a custom package you can install.  The package will create and customize the modules you'll need for the scenario.  The following instructions will walk you throw how to install the package.
1. Download the appropriate zip file from the latest [release](https://github.com/sugarcrm/school/releases). If you are
installing in Sugar Cloud, you will need to select the **production** version of the release.  If you are installing
elsewhere, you can select the **production** release or the **standard** release.  The **standard** release includes 
automated testing files while the **production** release does not.
1. Login to Sugar as an Administrator
1. Navigate to **Administration** > **Module Loader**
1. Upload **sugarcrm-ProfessorM-standard.zip**
1. Click **Install** for the ProfessorM package
1. Review and accept the license agreement
1. Click **Commit**
   * Hint for Windows users:  If you receive a warning with the message "Full extraction path exceed MAXPATHLEN (260)...", try the following:
     1. Download **sugarcrm-ProfessorM-windows.zip** from the latest [release](https://github.com/sugarcrm/school/releases).
     1. Install the zip as a module loadable package using the steps above.
     1. Download **sugarcrm-ProfessorM-windows-manual-install.zip** from the latest [release](https://github.com/sugarcrm/school/releases).
     1. Unzip the file. Note that you'll find **ProfMForWindowsReadme.txt** and a set of directories inside of the zip.
     If no directories are inside the zip, then all file paths in the `package/src` directory have been deemed short 
     enough to be included in a typical Windows installation and you will need to generate the zips yourself locally 
     on your own machine (see [Generating the Professor M module loadable packages locally](#generating-the-professor-m-module-loadable-packages-locally) 
     for instructions on how to do so).
     1. Open **ProfMForWindowsReadme.txt**.
     1. Follow the instructions inside of the readme to manually copy the files from the zip to your Sugar instance.  You
     may need to create directories in your Sugar directory if they do not already exist.
     1. Navigate to **Administration** > **Repair** > **Quick Repair and Rebuild**.
   * If the above installation still fails due to a MAXPATHLEN error, we recommend generating the zips yourself locally 
   on your own machine.  See 
   [Generating the Professor M module loadable packages locally](#generating-the-professor-m-module-loadable-packages-locally) 
   for instructions on how to do so.
   
   
### Customize the modules that are displayed
Sugar will display many modules by default that you will not be using while working on the tutorials.  To make things simpler, we'll hide the modules that won't be used and rearrange the modules that are displayed.
1. Login to Sugar as an Administrator if you have not already done so
1. Go to **Administration** > **Display Modules and Subpanels**
1. Drag the following modules from the **Displayed Modules** box to the **Hidden Modules** box:
   * Calendar
   * Calls
   * Meetings
   * Tasks
   * Notes
   * Emails
   * Targets
   * Target Lists
   * Forecasts
   * Documents
   * Cases
   * Tags
1. Rearrange the items in the **Displayed Modules** box so they are in the following order from top to bottom:
   * Accounts
   * Leads
   * Contacts
   * Professors
   * Opportunities
   * Revenue Line Items
   * Quotes
   * Reports
   * Campaigns
   * Process Email Templates
   * Process Definitions
   * Process Business Rules
   * Processes
1. Click **Save**

### Use the Sugar REST API to create the Professor M sample data
In order to create the Professor M sample data, you'll use Postman to run a collection of Sugar REST API calls.  Each call in the collection has one or more simple tests associated with it to ensure the call was successful.
1. Save a copy of [ProfessorM_PostmanCollection.json](https://raw.githubusercontent.com/sugarcrm/school/master/data/ProfessorM_PostmanCollection.json)
1. In Postman, click **Import**
1. Click **Choose Files** and import **ProfessorM_PostmanCollection.json**
1. Click the gear icon in the upper right corner and select **Manage Enviornments**
1. Click **Add** 
1. Input a name for your environment (for example, **Professor M**)
1. Add the following keys and values:
   * url: the url of your Sugar installation (for example, http://localhost:8888/profm)
   * rest_endpoint:  /rest/v10
   * username:  the username for an admin user in your Sugar installation
   * password:  the password associated with the username above
1. Click **Add**
1. Close the **Manage Environments** dialog
1. Click **Runner**
1. Select the **ProfessorM Sample Data** collection
1. Ensure the environment you just created is selected
1. Click **Run ProfessorM S...**
1. Wait for the collection to finish running. All tests should pass.
   Hint:  If you see many failures, you may have forgotten to install the Professor M module loadable package.  See the 
   instructions in previous section for how to do the install.
   
If you are using an Enterprise or Ultimate edition of Sugar, you can use the features that leverage Advanced Workflow.
Save a copy of [ProfessorM_PostmanCollection_AdvancedWorkflow.json](https://raw.githubusercontent.com/sugarcrm/school/master/data/ProfessorM_PostmanCollection_AdvancedWorkflow.json)
and follow the steps above to import the collection and run it.

## Setting up your development environment
If you want to generate the Professor M module loadable packages yourself or make changes to the code in this repo, you
will need to set up a development environment.  You do NOT need to set up a development environment if you simply want
to install the Professor M scenario as-is in your Sugar instance.

1. Checkout or download a copy of this repo.
1. [Install PHP 7](http://php.net/manual/en/install.php).
1. [Install Composer](https://getcomposer.org/download/). We use Composer to install the PHP dependencies for the project.  
1. Execute the following command from your `school/package` directory in order to install the dependencies:
```
composer install
```

You may also want to set up your development environment so you can execute the unit tests.  See 
[Automated tests](#automated-tests) for more information.

## Contribute to this project
Professor M's School is [open source](https://github.com/sugarcrm/school/blob/master/LICENSE), and we would love for you 
to get involved!  Below are some ways you can contribute to this project:
- Get notifications about this repo by clicking the **Watch** button at the top of this 
[repo](https://github.com/sugarcrm/school).
- Explore the code and use it as a resource as you develop your integrations and customizations.
- Create a [new Issue](https://github.com/sugarcrm/school/issues/new) if you have ideas for improvement, a feature 
request, or a bug report.
- Assign yourself an Issue, update the code, and create a pull request.  See [CONTRIBUTING.MD](docs/CONTRIBUTING.md) for
more details.


### ZenHub
We utilize ZenHub to organize our backlog and track our Issues.  You can view our ZenHub board inside the GitHub web 
interface if you have a [ZenHub browser extension](https://www.zenhub.com/extension) installed.  You can also view our 
ZenHub board at 
[https://app.zenhub.com/workspace/o/sugarcrm/school/boards?repos=109023666](https://app.zenhub.com/workspace/o/sugarcrm/school/boards?repos=109023666). 

When viewing our ZenHub board, you can view our prioritized backlog as well which stories are currently in progress, 
blocked, under review, and closed.  


## Generating the Professor M module loadable packages locally
The Professor M module loadable packages can be found on the [Releases](https://github.com/sugarcrm/school/releases) 
page of this GitHub repo.  You may want to generate the module loadable packages yourself if you are a Windows user with 
a long Sugar directory path or if you want to make changes to the package.

1. [Set up your development environment](#setting-up-your-development-environment) if you have not already done so.
1. In a shell, navigate to the `package` directory inside of your `school` directory.
1. For standard builds, execute ```./pack.php -v versionNameOrNumber```
1. For Windows builds where installing the standard build results in MAXPATHLEN errors, 
execute ```./pack.php -v versionNameOrNumber -w lengthOfWindowsSugarDirectoryPath```


## Continuous integration with Travis CI
This repository is configured to work with [Travis CI](https://docs.travis-ci.com/user/for-beginners/).  Whenever a commit
is pushed to the repository or a Pull Request is made, Travis CI will automatically kick off a build.

### Viewing results in Travis CI

You can view the Travis CI build results at [https://travis-ci.org/sugarcrm/school](https://travis-ci.org/sugarcrm/school).

### Viewing results in GitHub

You can view the latest build status at the top of this README ([![Build Status](https://travis-ci.org/sugarcrm/school.svg?branch=windows-build-pack-php)](https://travis-ci.org/sugarcrm/school)).  
Clicking on the build status will open the detailed results in Travis CI.

You can also view build results in Pull Requests.  Toward the bottom of each Pull Request, you can click "Show all 
checks" to see the Travis CI build results for that Pull Request.  

![Show all checks](images/pr1.png)

You can then click Details to open the build results in Travis CI.

![Details](images/pr2.png)

### About the build

The build has four Environment Variables that have been configured in the project settings in Travis CI:
- SUGARCRM_USERNAME: The username for an account that has access to the 
[SugarCRM Developer Builds Space](https://community.sugarcrm.com/community/developer/developer-builds) and the [Sugar
Store](https://store.sugarcrm.com/download)
- SUGARCRM_PASSWORD: The password associated with the above account
- GITHUB_USERNAME: The username for a GitHub account that has access to https://github.com/sugarcrm/unit-tests
- GITHUB_PASSWORD: The password associated with the above account

![Travis CI Environment Variables](images/travisenvvars.png)

The build is configured in [.travis.yml](.travis.yml). Currently, the build has three stages:
- Test PackageGenerator
- Run Tests
- Build & Post on GitHub

All of the jobs in each stage must pass before the jobs in the following stage will begin.

The Test PackageGenerator stage is run first and has two jobs:
  - Execute the PHPUnit tests associated with the PackageGenerator (see 
  [PHPUnit tests for PackageGenerator](#phpunit-tests-for-packagegenerator) for details).
  - Execute the Jasmine tests associated with the PackageGenerator (see 
  [Jasmine tests for PackageGenerator](#jasmine-tests-for-packagegenerator) for details).
The PackageGenerator is responsible for creating the Professor M Module Loadable Package.  This stage ensures that the
PackageGenerator is functioning as we expect that it would.  This stage does NOT test the Module Loadable Package.  

The next stage to run is the Run Tests stage.  Each job in this stage deploys Sugar, installs the Professor M Module
Loadable Package, runs the setup for the PHPUnit tests that Sugar provides, runs the PHPUnit tests written 
specifically for our Professor M Module Loadable Package, and runs the Postman tests. Each job in this stage is run 
against a different combination of Sugar versions and editions.  See 
[PHPUnit tests for the Professor M Module Loadable Package](#phpunit-tests-for-the-professor-m-module-loadable-package) 
for details.
 
The final stage to run is the Build & Post on GitHub stage.  Note that this stage is only run when the branch is Master. 
This stage executes the pack.php script to generate the Professor M Module Loadable Packages as zips. The 
zips will be automatically posted to GitHub: https://github.com/sugarcrm/school/releases.

If you want the Build & Post on GitHub stage to be kicked off for a branch other than master, you should do **both** of 
the following in [.travis.yml](.travis.yml).
- Remove the "if: branch = master" in the `stages` section
- Add the branch as an option in the deploy section. For example:
```$xslt
    deploy:
      provider: releases
      file: releases/sugarcrm-ProfessorM-latest.zip
      api_key:
          secure: mykey
      skip_cleanup: true
      on:
        branch: mybranchname
```



## Continuous integration with Jenkins
This repository can be configured for continuous integration with [Jenkins](https://jenkins-ci.org/).  Jenkins can be 
configured so that whenever a commit is pushed to the repository or at certain time intervals, Jenkins will 
automatically kick off a build.

### Installing Jenkins

Before beginning, you'll need to set up your own installation of Jenkins.  Check out the 
[Jenkins Installation Guide](https://jenkins.io/doc/book/installing/) for more details.  

To help you get started, we have provided [PrepareJenkinsDockerContainer.sh](scripts/PrepareJenkinsDockerContainer.sh) 
that you can run to start Jenkins inside of a Docker container.  The machine or container where Jenkins is running will 
need to have [Docker Compose](https://docs.docker.com/compose/install/) and [Perl](https://www.perl.org/get.html) 
installed. [PrepareJenkinsDockerContainer.sh](scripts/PrepareJenkinsDockerContainer.sh) will take care of installing 
both for you. If you use [PrepareJenkinsDockerContainer.sh](scripts/PrepareJenkinsDockerContainer.sh), you should be 
able to access Jenkins at [http://localhost:8080](http://localhost:8080).

We recommend installing the Jenkins suggested plugins.  You will also need to install the 
[EnvInject Plugin](https://wiki.jenkins.io/display/JENKINS/EnvInject+Plugin).

### Storing Credentials in Jenkins

The build you will create in Jenkins needs access to credentials and configurations.  We will store these using
Jenkins Credentials.

The instructions below will walk you through how to create the necessary credentials and configurations.  For more 
information on how to store credentials in Jenkins, see 
[Credentials Binding Plugin](https://wiki.jenkins.io/display/JENKINS/Credentials+Binding+Plugin).

1. On the Jenkins dashboard, click **Credentials**.  (If you do not see the Credentials option, you may need to install the
Credentials Binding Plugin.)
1. Create new global credentials for the GitHub account that has access to the 
[SugarCRM Unit Tests repo](https://github.com/sugarcrm/unit-tests).  
   1. Kind: **Username with password**
   1. Scope: **Global** 
   1. Username: your GitHub username
   1. Password: your GitHub password
   1. ID: GITHUB_SUGARCRM_UNIT_TESTS
   1. Description: GitHub account that has access to https://github.com/sugarcrm/unit-tests
1. Create new global credentials for the account that has access to the 
   [SugarCRM Developer Builds Space](https://community.sugarcrm.com/community/developer/developer-builds) and the [Sugar
   Store](https://store.sugarcrm.com/download).  
   1. Kind: **Username with password**
   1. Scope: **Global** 
   1. Username: your SugarCRM username
   1. Password: your SugarCRM password
   1. ID: SUGARCRM_ACCOUNT
   1. Description: SugarCRM Account
1. Create a new global secret for the Sugar license key.
   1. Kind: **Secret text**
   1. Scope: **Global** 
   1. Secret: Your Sugar license key. This secret is used by [InstallSugarAndProfM.sh](scripts/InstallSugarAndProfM.sh). 
   1. ID: SUGAR_LICENSE_KEY
   1. Description: The Sugar license key


### Creating a Jenkins project

Now you're ready to create a new project in Jenkins that will build the school project. 

1. On the Jenkins dashboard, click **New Item**.
1. Name your new item something like **ProfessorM**.  
1. Select **Freestyle project** and click **OK**. The item configuration page will display.
1. In the **Source Code Management** section, select **Git.**
1. Input your Repository URL (for example, `https://github.com/sugarcrm/school`) and select the GitHub credentials you
created in the previous section.
1. Configure the Build Triggers section as you'd like. If you do not want to configure this now, you can skip this step
and manually trigger the builds instead.
1. In the **Build Environment** section, select the **Delete workspace before build starts** option and the **Use secret
text(s) or file(s)** option.
1. In the **Bindings** section, select **Add** > **Username and password (separated)**. Then input the following:
    1. Username Variable: `GITHUB_USERNAME`
    1. Password Variable: `GITHUB_PASSWORD`
    1. Credentials: **Specific credentials**
    1. Select the GITHUB_SUGARCRM_UNIT_TESTS credentials.
1. In the **Bindings** section, select **Add** > **Username and password (separated)**. Then input the following:
    1. Username Variable: `SUGARCRM_USERNAME`
    1. Password Variable: `SUGARCRM_PASSWORD`
    1. Credentials: **Specific credentials**
    1. Select the SUGARCRM_ACCOUNT credentials.
1. In the **Bindings** section, select **Add** > **Secret text**. Then input the following:
    1. Variable: `SUGAR_LICENSE_KEY`
    1. Credentials: **Specific credentials**
    1. Select the SUGAR_LICENSE_KEY secret text.
1. In the **Bindings** section, select the **Inject environment variables to the build process** checkbox. If you do not
see this checkbox, you may need to install the 
[EnvInject Plugin](https://wiki.jenkins.io/display/JENKINS/EnvInject+Plugin). Then...
    1. In the **Properties Content** input box, add a line for the WORKSPACE_PATH variable. This path represents the path
    to the workspace for your Jenkins job on the *host* machine.  For example, if your Jenkins home directory is 
    `/Users/lschaefer/jenkins` and your Jenkins project is named ProfessorM, you would input the following:
    `WORKSPACE_PATH=/Users/lschaefer/jenkins/workspace/ProfessorM`
    1. In the **Properties Content** input box, add a line for the PATH_TO_SUGAR_DOCKER_ON_HOST variable.  This variable
     represents the path to Sugar Docker on the *host* machine. If you want to use the default location, input the 
     following:
     `PATH_TO_SUGAR_DOCKER_ON_HOST=$WORKSPACE_PATH/scripts/workspace/sugardocker`
     If you want to customize where Sugar Docker is stored, you can update this variable to reflect that.
    

1. In the **Build** section, click **Add build step** and select **Execute shell**. 
1. In the **Command** box that appears, input the following: 
    ```
    # The Sugar version you want to test
    SUGAR_VERSION="7.11"
    
    # The Sugar Edition you want to test. Options: Pro, Ent, and Ult
    SUGAR_EDITION="Ent"
    
    # Path to where the Sugar Docker directory should be stored. If you do not have a preference, leave this as is.
    SUGAR_DOCKER_DIRECTORY="workspace/sugardocker"
    
    # This variable is completely optional.  If you want to store the Sugar source zips on your local machine instead
    # of downloading them from the SugarCRM Developer Builds space or Sugar Store, input the path to where the Sugar 
    # source zips are stored. For example: /var/sugardocker/data/app/sugar_source_zips. Note that your Sugar source zips 
    # MUST follow this naming convention: Sugar$sugarEdition-$sugarVersion.zip (for example: SugarEnt-7.11.zip).
    # SUGAR_SOURCE_ZIPS_DIRECTORY=""
     
    cd scripts
     
    bash -ex RunPackUnitTestsAndBuildProfMPackage.sh $SUGAR_WORKSPACE_PATH
     
    bash SetupEnvAndRunTests.sh $SUGARCRM_USERNAME $SUGARCRM_PASSWORD $SUGAR_VERSION $SUGAR_EDITION $GITHUB_USERNAME $GITHUB_PASSWORD $SUGAR_DOCKER_DIRECTORY $SUGAR_SOURCE_ZIPS_DIRECTORY
    ```
    Be sure to update the variables appropriately.
1. In the **Post-build Actions** section, click **Add post-build action** and select **Archive the artifacts**.
1. In the **Files to archive** box that appears, input the following: `package/releases/*.zip`
1. Click **Save**.

### Running a build and viewing the results

Once you have your Jenkins project created, it's time to see if it works!

Navigate to your ProfessorM project in Jenkins. Trigger your build manually by clicking **Build Now**.

View the Build History panel to quickly browse the build results.  If you see a blue dot, you know all of the tests passed!

![Build passed](images/jenkins-buildpassed.png)

Click on a build to view more details.  If the build passed, the Professor M module loadable packages will be stored as 
build artifacts.

![Build artifacts](images/jenkins-buildartifact.png)

To see more details on a build, click **Console Output**.  If any step in the process fails (for example, a Jasmine test
fails), the remaining steps will not be run.  If everything succeeds, you'll be able to find the Jasmine test results
for PackageGenerator, the PHPUnit test results for PackageGenerator, the PHPUnit test results for Sugar, the PHPUnit 
tests for the Professor M Module Loadable Package, and the results of the Professor M module loadable packages being 
generated, copied, and archived. 

Jasmine results for PackageGenerator:

![Jasmine passed](images/jenkins-jasmine.png)

PHPUnit results for PackageGenerator:

![PHPUnit results](images/jenkins-phpunit.png)

PHPUnit results for the Professor M Module Loadable Package:

![PHPUnit results](images/phpunitprofm.png)

Postman test results:

![Postman results](images/jenkinspostmansuccess.png)

Professor M package results:

![ProfM zip](images/jenkins-profm.png)

Tip:  If you see errors in the Console Output about git not being found, you may need to update your Jenkins configuration.
On the Jenkins dashboard, click **Manage Jenkins**. Click **Conifgure System**. In the **Global Properties** section,
enable the **Tool Locations** checkbox. In the Name box, select **(Git) Default**.  In the Home box, input the path
to the Git installation (for example, `/usr/bin/git`).  Click **Save**.

Tip for those running Jenkins in Docker:  If you see errors in the Console Output similar to 'Fatal error: Unable to 
find local grunt', you may need to update your Jenkins job.  The likely cause is that your 
`$SUGAR_WORKSPACE_PATH` is not pointing to the path of the workspace that is storing the school repo's files that are being pulled out of 
GitHub.  You can diagnose if this is the issue by adding `docker exec my-yarn pwd` and `docker exec my-yarn ls` around 
line 18 of [RunPackUnitTestsAndBuildProfMPackage.sh](scripts/RunPackUnitTestsAndBuildProfMPackage.sh) to see what is in 
the `workspace` directory after the `docker run` command has mounted the volume.  If you do not see files from the 
school repo in the `workspace`, you need to update `$SUGAR_WORKSPACE_PATH`. 

### About the build

The build calls two scripts
1. [RunPackUnitTestsAndBuildProfMPackage.sh](scripts/RunPackUnitTestsAndBuildProfMPackage.sh)
1. [SetupEnvAndRunTests.sh](scripts/SetupEnvAndRunTests.sh)

[RunPackUnitTestsAndBuildProfMPackage.sh](scripts/RunPackUnitTestsAndBuildProfMPackage.sh) has three key parts:
1. Run the Jasmine tests that test [PackageGenerator](package/PackageGenerator.php)
1. Run the PHPUnit tests that test [PackageGenerator](package/PackageGenerator.php)
1. Build the Professor M Module Loadable Packages using the [PackageGenerator](package/PackageGenerator.php)

This script relies on Docker images stored on [Docker Hub](https://hub.docker.com/r/sugarcrmdev/school) in order to 
implement the three parts listed above. [The sugarcrmdev/school Docker Hub repository](https://hub.docker.com/r/sugarcrmdev/school) 
stores two images:
- The `yarn` image has all of the dependencies managed by Yarn installed in it.  The shell script uses this image to run 
the Jasmine tests.
- The `composer` image has all of the dependencies managed by Composer installed in it. The shell script uses this image 
to run the PHPUnit tests as well as to generate the Professor M module loadable packages.

This script does NOT test the Module Loadable Package.  

The next step is to run [SetupEnvAndRunTests.sh](scripts/SetupEnvAndRunTests.sh).  This script deploys 
Sugar, installs the Professor M Module Loadable Package, runs the setup for the PHPUnit tests that Sugar provides, 
runs the PHPUnit tests written specifically for our Professor M Module Loadable Package, and runs the Postman tests.

Note:  if any step in the process fails (for example, a Jasmine test fails), the remaining steps will not be run.

## Automated tests

This repository contains various automated tests.  We'll discuss each category of tests below.

### Testing PackageGenerator.php

This repository contains automated PHPUnit and Jasmine tests specifically for testing 
[PackageGenerator](package/PackageGenerator.php).  Since PackageGenerator does not require the Sugar code base in order
to run, these tests can be executed separate from the Sugar code base.

These tests can be executed manually or as part of a continuous integration build.

#### PHPUnit tests for PackageGenerator
[PHPUnit](https://phpunit.de/) is a testing framework for PHP.  The PHPUnit test files are located in 
[/tests/phpunit](tests/phpunit).  The [/tests/phpunit](tests/phpunit) directory can contain 
multiple test files, and each test file can contain multiple tests.

##### Manual execution
To manually execute the tests, you will need to use Composer to install PHPUnit and other PHP dependencies.
If you have not installed Composer before, visit the [Composer Getting Started Guide](https://getcomposer.org/doc/00-intro.md).

Execute the following command from your `school/package` directory in order to install the test dependencies:
```
composer install
```

If you need to update the namespaces, manually update [composer.json](package/composer.json) and then run the following command from
your `school/package` directory:
```
./composer.phar update
```

The PHPUnit tests can be executed by running the following command from your `school/tests/phpunit` directory on macOS:
```
../../package/vendor/bin/phpunit
```
or on Windows:
```
..\..\package\vendor\bin\phpunit
```

##### Automatic execution in Travis CI
The PHPUnit tests are automatically run as part of the Test PackageGenerator stage of the Travis CI build.  Travis CI's 
default build script for PHP is PHPUnit, so we don't have to include anything special in [.travis.yml](.travis.yml) in 
order for the tests to run.  However, we have added `composer install` to [.travis.yml](.travis.yml) in order for the 
dependencies to be installed on the build machine. Travis CI looks in [phpunit.xml](tests/phpunit/phpunit.xml) for the PHPUnit config. 
Our config indicates that the PHPUnit tests are stored in [tests/phpunit](tests/phpunit).  

#### Interpreting the results
To see the results of the tests that are run as part of the Travis CI build, open the build in Travis CI.  If the build 
passed, you know all of the tests passed.

![Green build](images/greenbuild.png)

To see the detailed test results, click the PHP build job to expand it:
![PHP build job](images/phpbuildjob.png)

You can scroll through the job log to see the results of the PHPUnit tests.

![PHPUnit passed](images/phpunitpassed.png)

If the build failed, a variety of things could have caused the failure including a failing PHPUnit test.

![Red build](images/redbuild.png)

If a PHPUnit test fails, you'll see something like the following in the job log.

![PHPUnit failed](images/phpunitfailed.png)


##### Automatic execution in Jenkins

The PHPUnit tests are automatically run as part of the Jenkins build when 
[RunPackUnitTestsAndBuildProfMPackage.sh](scripts/RunPackUnitTestsAndBuildProfMPackage.sh) is executed.

#### Interpreting the results
To see the results of the tests that are run as part of the Jenkins build, open the build in Jenkins.  If the build 
passed, you know all of the tests passed.

![Passing build](images/jenkinsbuildpassed.png)

To see the detailed test results, open the build and click **Console Output**. You can scroll through the job log to see 
the results of the PHPUnit tests.  Note:  you may need to open the Full Log to find the results.

![PHPUnit passed](images/jenkinsphpunitpassed.png)

If the build failed, a variety of things could have caused the failure including a failing PHPUnit test.

![Failing build](images/jenkinsfailingbuild.png)

If a PHPUnit test fails, you'll see something like the following in the job log.

![PHPUnit failed](images/jenkinsphpunitfailed.png)


#### Jasmine tests for PackageGenerator
[Jasmine](https://jasmine.github.io/) is a testing framework for JavaScript.  We have included a very simple Jasmine 
test in this repository as an example.

The tests are located in [/tests/jasmine/specs](tests/jasmine/specs).  Currently, there is one test inside of the 
[DummySpec.js](tests/jasmine/specs/DummySpec.js) test file.  The [/tests/jasmine/specs](tests/jasmine/specs) directory 
can contain multiple test files, and each test file can contain multiple tests.

##### Manual execution
To manually execute the tests, you will need to install a few different things on your machine before you can run the 
tests. 

###### Setup
Install Yarn which is an NPM compatible package manager. See 
[Yarn Installation Guide](https://yarnpkg.com/lang/en/docs/install/) for more details on how to install Yarn.

Next navigate to your `school` directory and then execute the following commands. 

Navigate to the `tests/jasmine` directory.
```
cd tests/jasmine
```

Install the JavaScript dependencies using Yarn. These dependencies include Grunt, Jasmine, and Phantomjs.
```
yarn install
```

Install the Grunt command line interface globally. See 
[Grunt's Getting Started Guide](https://gruntjs.com/getting-started) for more details on installing and using Grunt.
```
yarn global add grunt-cli
```

###### Execution
Inside of your `tests/jasmine` directory, execute the following command to run the Jasmine tests:
```
grunt test-js
```

##### Automatic execution in Travis CI
The Jasmine tests are automatically run as part of the Travis CI build process.  In [.travis.yml](.travis.yml), the Test 
PackageGenerator stage kicks off the "test-js" task.

###### Interpreting the results
To see the results of the tests that are run as part of the Travis CI build, open the build in Travis CI.  If the build 
passed, you know all of the tests passed.

![Green build](images/greenbuild.png)

To see the detailed test results, click the Node.js build job to expand it:
![Node build job](images/nodebuildjob.png)

You can scroll through the job log to see the results of the Jasmine tests.

![Jasmine passed](images/jasminepassed.png)

If the build failed, a variety of things could have caused the failure including a failing Jasmine test.

![Red build](images/redbuild.png)

If a Jasmine test fails, you'll see something like the following in the job log.

![Jasmine failed](images/jasminefailed.png)

##### Automatic execution in Jenkins
The Jasmine tests are automatically run as part of the Jenkins build when 
[RunPackUnitTestsAndBuildProfMPackage.sh](scripts/RunPackUnitTestsAndBuildProfMPackage.sh) is executed.

###### Interpreting the results
To see the results of the tests that are run as part of the Jenkins build, open the build in Jenkins.  If the build 
passed, you know all of the tests passed.

![Passing build](images/jenkinsbuildpassed.png)

To see the detailed test results, open the build and click **Console Output**. You can scroll through the job log to see 
the results of the Jasmine tests.  Note:  you may need to open the Full Log to find the results.

![Jasmine passed](images/jenkinsjasminepassed.png)

If the build failed, a variety of things could have caused the failure including a failing Jasmine test.

![Failing build](images/jenkinsfailingbuild.png)

If a Jasmine test fails, you'll see something like the following in the job log.

![Jasmine failed](images/jenkinsjasminefailed.png)

### Testing Sugar and the Professor M Module Loadable Package

Many customizations in the Professor M Module Loadable Package require a copy of the Sugar code in order to compile
and/or run.  Therefore, we will only test the Professor M Module Loadable Package after it has been installed in Sugar.

In this section, we'll discuss how to run the automated tests for the Professor M Module Loadable Package.  Since the
setup for running the Sugar provided automated tests is so similar, we will discuss how to do that here as well.

Currently, we have PHPUnit tests and Postman tests.

#### PHPUnit tests for the Professor M Module Loadable Package
[PHPUnit](https://phpunit.de/) is a testing framework for PHP.  The PHPUnit test files are located in 
[package/src/custom/tests/unit-php/School](package/src/custom/tests/unit-php/School).  

##### Manual execution

There are two primary ways to manually execute the PHPUnit tests.  We'll explore both below.

###### Manual execution using Docker

The easiest way to run the PHPUnit tests is to run the same scripts that the automated tests run.  

First, you will need to install [Docker](https://docs.docker.com/install/), 
[Docker Compose](https://docs.docker.com/compose/install/#install-compose), and [Perl](https://www.perl.org/get.html).
If the script will be downloading a copy of Sugar from the Sugar Store or the Sugar Developer Builds Community (instead 
of using a copy of Sugar stored on your machine), you will also need a package installed that can execute the `sha1sum` 
command. On a Mac, you can install md5sha1sum by executing `brew install md5sha1sum` in a shell.

Then execute [SetupEnvAndRunTests.sh](scripts/SetupEnvAndRunTests.sh).  Note that the Sugar provided unit 
tests are NOT run as part of [SetupEnvAndRunTests.sh](scripts/SetupEnvAndRunTests.sh).  If you want to add
them, add the following line after the call to `SetupSugarPHPUnitTests.sh`:

```
./RunSugarPHPUnitTests.sh $sugarDirectory || exit 1
```

###### Manual execution in an installed version of Sugar

If you are actively developing the Professor M Module Loadable Package, you will most likely want to run the unit tests
as you are working and making updates to the code.  

In order to manually execute the tests, you will need a running copy of Sugar that has been installed with no sample data.
See [Getting Started with Sugar Development](https://community.sugarcrm.com/community/developer/pages/getting-started) 
for instructions on setting up a development environment.

You will also need to get a copy of the Sugar provided unit tests and put them in your Sugar source code directory. See
the [SugarCRM unit tests GitHub repo](https://github.com/sugarcrm/unit-tests) for more information.  

Prepare to run the Sugar provided PHPUnit tests and the Professor M PHPUnit tests by executing the following commands:
```
$ cd /path/to/sugar_source_dir
$ composer install
$ cd tests/unit-php
$ chmod +x ../../vendor/bin/phpunit
```

Run the Sugar provided unit tests by executing the following command from the `tests/unit-php` directory:

```
$ ../../vendor/bin/phpunit
```

Install the **standard** version of the Professor M Module Loadable Package using 
[Module Loader](https://support.sugarcrm.com/SmartLinks/Administration_Guide/Developer_Tools/Module_Loader/index.html) 
if you have not already done so.  The code for 
Professor M and the associated tests will be installed in to the Sugar source directory.

Run the Professor M PHPUnit tests by executing the following command from the `tests/unit-php` directory:

```
$ ../../vendor/bin/phpunit --testsuite custom
```

##### Automatic execution in Travis CI
The PHPUnit tests that test the Professor M Module Loadable Package are automatically run as part of the Run Tests 
stage of the Travis CI build.  

Each job in this stage is basically the same with the exception of the environment variables.  Each job calls 
[SetupEnvAndRunTests.sh](scripts/SetupEnvAndRunTests.sh), which executes the Professor M PHPUnit tests.

Note that the Sugar provided unit tests are NOT run as part of 
[SetupEnvAndRunTests.sh](scripts/SetupEnvAndRunTests.sh).  If you want to add
them, add the following line after the call to `SetupSugarPHPUnitTests.sh`:

```
./RunSugarPHPUnitTests.sh $sugarDirectory || exit 1
```

#### Interpreting the results
To see the results of the tests that are run as part of the Travis CI build, open the build in Travis CI.  If the build 
passed, you know all of the tests passed.

![Green build](images/greenbuild.png)

To see the detailed test results, click a job in the Run Tests stage:
![PHPUnit job](images/travisphpunitjob.png)

You can scroll through the job log to see the results of the PHPUnit tests.

![PHPUnit passed](images/travisphpunitresults.png)

If the build failed, a variety of things could have caused the failure including a failing PHPUnit test.

![Red build](images/redbuild.png)

If a PHPUnit test fails, you'll see something like the following in the job log.

![PHPUnit failed](images/travisphpunitfail.png)


##### Automatic execution in Jenkins

The PHPUnit tests that test the Professor M Module Loadable Package are automatically run as part of the Jenkins build 
when [SetupEnvAndRunTests.sh](scripts/SetupEnvAndRunTests.sh) is run.
     
Note that the Sugar provided unit tests are NOT run as part of 
[SetupEnvAndRunTests.sh](scripts/SetupEnvAndRunTests.sh).  If you want to add them, add the following line 
after the call to `SetupSugarPHPUnitTests.sh`:
     
     ```
     ./RunSugarPHPUnitTests.sh $sugarDirectory || exit 1
     ```

#### Interpreting the results
To see the results of the tests that are run as part of the Jenkins build, open the build in Jenkins.  If the build 
passed, you know all of the tests passed.

![Passing build](images/jenkinsbuildpassed.png)

To see the detailed test results, open the build and click **Console Output**. You can scroll through the job log to see 
the results of the PHPUnit tests.

![PHPUnit passed](images/jenkinsphpunit.png)

If the build failed, a variety of things could have caused the failure including a failing PHPUnit test.

![Failing build](images/jenkinsfailingbuild.png)

If a PHPUnit test fails, you'll see something like the following in the job log.

![PHPUnit failed](images/jenkinsphpunitfailed2.png)


#### Postman tests for the Professor M Module Loadable Package

[Postman](https://www.getpostman.com/) is an API development environment.  We use Postman Collections to insert our 
sample data into Sugar via the REST API.  Each API call in the collections has one or more associated tests to ensure
the calls were successful.  

The Postman Collections can be run via the Postman application as described 
[above](#use-the-sugar-rest-api-to-create-the-professor-m-sample-data) or the command line using 
[Newman](https://www.getpostman.com/docs/v6/postman/collection_runs/command_line_integration_with_newman).

##### Manual execution using the command line interface

You can execute the tests against any running instance of Sugar. Note that the Postman tests will NOT be installed
as part of the Professor M module loadable package.  The tests will only be available in your `school` repo.

The first step is to configure the Postman Environment for your particular instance of Sugar.  Open 
[ProfessorM_PostmanEnvironment](data/ProfessorM_PostmanEnvironment.json) and update the url, username, password, and 
rest_endpoint to reflect your instance.

Then you can choose to install Newman to execute the tests or use a Docker image to execute the tests.

###### Using Newman

[Install Node.js](https://nodejs.org/en/download/) if you haven't already.

Install Newman by executing the following:

`npm install -g newman`

Navigate to the `school/data` directory in your shell.  Execute the tests by running the following:

`newman run ProfessorM_PostmanCollection.json -e ProfessorM_PostmanEnvironment.json`

You can execute the tests that leverage Advanced Workflow (only available in Enterprise and Ultimate editions of Sugar)
by running the following:

`newman run ProfessorM_PostmanCollection_AdvancedWorkflow.json -e ProfessorM_PostmanEnvironment.json`

###### Using Docker

[Install Docker](https://docs.docker.com/install) if you haven't already.

Pull the Newman Docker container that we will use to run the tests by executing the following:

`docker pull postman/newman_ubuntu1404`

Execute the tests by running the following:

`docker run -v pathToTheDataDirectoryInYourSchoolRepo:/etc/newman -t postman/newman_ubuntu1404 run "ProfessorM_PostmanCollection.json" --environment="ProfessorM_PostmanEnvironment.json"`

Be sure to replace `pathToTheDataDirectoryInYourSchoolRepo` with the path to the `data` directory in your school repo.

You can execute the tests that leverage Advanced Workflow (only available in Enterprise and Ultimate editions of Sugar)
by running the following:

`docker run -v pathToTheDataDirectoryInYourSchoolRepo:/etc/newman -t postman/newman_ubuntu1404 run "ProfessorM_PostmanCollection_AdvancedWorkflow.json" --environment="ProfessorM_PostmanEnvironment.json"`

Hint:  If your instance of Sugar is running inside a Docker container, you may need to add the `--net="host"` option:

`docker run -v pathToTheDataDirectoryInYourSchoolRepo:/etc/newman --net="host" -t postman/newman_ubuntu1404 run "ProfessorM_PostmanCollection.json" --environment="ProfessorM_PostmanEnvironment.json"`

##### Automatic Execution in Travis CI

The Postman tests are automatically run as part of the Run Tests stage of the Travis CI build.

Each job in this stage is basically the same with the exception of the environment variables.  Each job calls 
[SetupEnvAndRunTests.sh](scripts/SetupEnvAndRunTests.sh), which executes the Postman tests.

##### Interpreting the results

To see the results of the tests that are run as part of the Travis CI build, open the build in Travis CI.  If the build 
passed, you know all of the tests passed.

![Green build](images/greenbuild.png)

To see the detailed test results, click a job in the Run Tests stage:

![PHPUnit job](images/travisphpunitjob.png)

You can scroll through the job log to see the results of the Postman tests.

![PHPUnit passed](images/travispostmansuccess.png)

If the build failed, a variety of things could have caused the failure including a failing Postman test.

![Red build](images/redbuild.png)

If a Postman test fails, you'll see something like the following in the job log.

![PHPUnit failed](images/travispostmanfailure.png)

##### Automatic execution in Jenkins

The Postman tests are automatically run as part of the Jenkins build when 
[SetupEnvAndRunTests.sh](scripts/SetupEnvAndRunTests.sh) is run.

#### Interpreting the results
To see the results of the tests that are run as part of the Jenkins build, open the build in Jenkins.  If the build 
passed, you know all of the tests passed.

![Passing build](images/jenkinsbuildpassed.png)

To see the detailed test results, open the build and click **Console Output**. You can scroll through the job log to see 
the results of the Postman tests.

![PHPUnit passed](images/jenkinspostmansuccess.png)

If the build failed, a variety of things could have caused the failure including a failing Postman test.

![Failing build](images/jenkinsfailingbuild.png)

If a Postman test fails, you'll see something like the following in the job log.

![PHPUnit failed](images/jenkinspostmanfailed.png)


## How to fix your Sugar instance without starting completely over

As you customize this instance, you may do something like accidentally write broken code that seems to break your Sugar instance.  Try running **Quick Repair and Rebuild**:
1. Log in as an administrator.
1. Click your profile picture in the upper-right corner and select **Administration**.
1. In the **System** section, click **Repair**.
1. Click **Quick Repair and Rebuild**.

If you become unable to login to your Sugar instance or running **Quick Repair** does not work, try the following:

1. Remove the custom code that is causing problems.
1. Delete the contents of the `cache` directory.
1. Use a program like MySQL Workbench to truncate the `metadata_cache` table.
1. Access your Sugar instance in a browser. If you still receive an error, reload the page.

If the above steps do not fix your problem, you may need to start over.  Delete your Sugar root directory and follow the steps in the Installation Instructions above.
