# Load Test in a CICD Environment

## ## Technology and Tool Used

- Visual Studio Code
- Jenkins
- Postman
- Jmeter

## Prerequisites

- You must have installed Postman to your system
- jmeter
- Visual Studio Code
- Jenkins
- java

## API Documents

          https://documenter.getpostman.com/view/16548351/2s9Y5SWRC4

## Load Test in a CICD Environment

The pace of development, adding new features, and taking business time precedence over everything can lead to rapid changes being pushed to production without the quality assurance it deserves. This puts end-users at risk of experiencing poor performance that could have been avoided with proper testing. This is why Continuous Integration and Continuous Development (CICD) comes into play to cope with introducing new bugs or at least breaking the things that worked before.

![image](https://github.com/Mamun104/CICD_environment_for_load_test/assets/78067017/8790cdfc-52b4-4464-8048-12d0a368dd7c)

Contrary to the past when the load testing of a system was pushed to the end of a project, it is nowadays much more widely acknowledged that performance testing should start in the early stages of development. An effective solution to ensure that an application meets acceptance criteria is to build load testing into the CI or CD. However, some people might suggest that performance or reliability is a non-functional requirement that would be often left behind. In that case, if your application cannot scale well enough under peak conditions such as Black Friday, your business application is not functional anymore, and consequently, lose your customers.

## How to integrate automated load testing processes into CICD?

When it comes to integrating automated load tests into the build pipeline there are some points that should be considered.   


- Provide the dynamic and realistic test data that your load test scripts are going to use and make them available in the build pipeline. The test data can be in the form of JSON, TSV, or CSV files.

- Make sure test scripts are already executed.

- Identify which tests should be run and when. Focus on most “at-risk” parts of the application.

- Set up a monitoring tool to measure test server metrics.

- Evaluate how frequently tests need to be executed.

- Assure your load testing tool supports CICD.

In this project, we will integrate a Gatling maven project within the Jenkins pipeline. 

### Step-1:

#### Create a JenkinsFile

Create a JenkinsFile within your project to instruct how to run Gatling by Jenkins. 


    pipeline {
    agent any
    stages {
        stage("Build Maven") {
            steps {
                sh 'mvn -B clean package'
            }
        }
        stage("Run Gatling") {
            steps {
                sh 'mvn gatling:test'
            }
            post {
                always {
                    gatlingArchive()
                }
            }
        }
    }
}


Here, there are two stages: Build Maven and Run Gatling. 

### Step-2:

#### Create a pipeline

Create your own pipeline using JenkinsFile.
Let’s go to the Jenkins home page, select New Item, chose Pipeline, and set a meaningful name. Now you can create a new pipeline through the Pipeline section and select the source of the script. Then you can define to have the script from the supply chain management (SCM). Set the repository URL, credentials, and Branch, and finally indicate the path of your JenkinsFiles. 

![image](https://github.com/Mamun104/CICD_environment_for_load_test/assets/78067017/136028bd-1b4f-493a-b419-61d381038420)


### Step-3:

#### Gatling Jenkins Plugin

Install Gatling Jenkins Plugin to have a detailed report on each pipeline run and check the incoming and outgoing jobs. Navigate to settings and select Manage Jenkins.

![image](https://github.com/Mamun104/CICD_environment_for_load_test/assets/78067017/78b48a84-127b-42c7-8bcc-bb76c4f32469)


### Step-4:

#### Run the Pipeline

Go to the Jenkins home, select the pipeline that you’ve just created then click Build Now. A chart should be displayed at the end of the execution.

![image](https://github.com/Mamun104/CICD_environment_for_load_test/assets/78067017/5ca40110-e5a8-4304-9788-e4c753ac7088)


Now by integrating your load test script into a pipeline like Jenkins you can easily verify that changes in the code don’t cause a significant drop in performance after release. This in turn helps to improve the confidence and reliability of your application.







