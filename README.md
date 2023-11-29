# Jenkins Pipeline for Flask Application

# Table of Contents

1. [Overview](#overview)

2. [Prerequisites](#prerequisites)

    a. [Instance creation](#instance-creation)
   
    b. [Plugins Installation](#plugins-installation)

    c. [Configuring Email Notifications](#configuring-email-notifications)

4. [Pipeline Stages](#pipeline-stages)

    a. [Screenshots](#screenshots)

    b. [Jenkinsfile Configuration](#jenkinsfile-configuration)
5. [Poll SCM](#poll-scm)
6. [Email Notifications](#email-notifications)
7. [Overall Workflow](#overall-workflow)


## Overview

This Jenkins pipeline automates the build, test, and deployment of a Flask application. It fetches the application code from a GitHub repository, installs dependencies, runs unit tests, and deploys to a staging environment.

### Prerequisites

#### Instance creation

We need to create an Instance and install Jenkins.

![image](https://github.com/patilajayv/jenkins/blob/main/1.png)

![image](https://github.com/patilajayv/jenkins/blob/main/2.png)

#### Plugins Installation

To support this pipeline, install the following plugins:

- ![image](https://github.com/patilajayv/jenkins/blob/main/Untitled.png)


#### Configuring Email Notifications

Configure email notifications by navigating to `Manage Jenkins` > `System` > `E-mail Notification` (scroll to the bottom) and set up as shown below:

![image](https://github.com/patilajayv/jenkins/blob/main/6.png)
Scroll to the bottom of the page and find App passwords as shown in the screenshot


Copy and paste the code in the password section.
![image](https://github.com/patilajayv/jenkins/blob/main/5.png)
![image](https://github.com/patilajayv/jenkins/blob/main/7.png)



### Pipeline Stages

The pipeline includes these stages:

1. **Checkout:** Retrieves the application code from the GitHub repository.
2. **Build:** Installs application dependencies using `pip`.
3. **Test:** Runs unit tests for the application with `pytest`.
4. **Deploy:** Deploys the application to a staging environment if tests pass.

#### Screenshots

1. ![image](https://github.com/patilajayv/jenkins/blob/main/8.png)
2. ![image](https://github.com/patilajayv/jenkins/blob/main/9.png)
3. ![image](https://github.com/patilajayv/jenkins/blob/main/10.png)
4. We need to click on `settings` in the GitHub repository, check for `Webhooks`, and give the instance `public IP address:8080/github-webhook/` as shown below.
5. ![image](https://github.com/patilajayv/jenkins/blob/main/11.png)
6. To generate Git syntax for Jenkinsfile, click on `Pipeline Syntax`.
7. ![image](https://github.com/sayanalokesh/Jenkins/assets/105637305/59354843-7216-43b2-85c4-cb63fe848d18)

### Jenkinsfile Configuration

The Jenkinsfile defines pipeline stages and steps:

- `agent any`: Allows the pipeline to run on any available Jenkins agent.
- `git`: Fetches application code from GitHub repository using `git-cred` credentials.
- `pip install`: Installs dependencies from `requirements.txt`.
- `pytest`: Runs unit tests using the `pytest` framework.
- `gunicorn`: Installs and starts the Gunicorn WSGI server to run the Flask application.

[Jenkinsfile Link](https://github.com/patilajayv/jenkins/blob/main/Jenkinsfile)

#### Poll SCM

Poll SCM checks for new commits in Git and automatically triggers the build process to deploy code to the EC2 server.

![image](https://github.com/patilajayv/jenkins/blob/main/succeess.png)

### Email Notifications

The pipeline sends email notifications to `patilajayv2201@gmail.com` upon successful or failed builds, with customized subject lines and body content.

![image](https://github.com/patilajayv/jenkins/blob/main/mail.png)


### Overall Workflow

1. Checkout code from GitHub repository.
2. Install dependencies using pip.
3. Run unit tests with pytest.
4. Deploy application to staging using Gunicorn.
5. Send email notification indicating build status.
