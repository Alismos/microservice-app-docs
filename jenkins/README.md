# Jenkins

## Requirements

* Install jenkins in [debian/ubuntu](https://www.jenkins.io/doc/book/installing/linux/#debianubuntu)

* Create EC2 machine in aws 

## Configure Jenkins

When launching jenkins we can create our admin credentials or use the default admin credentials. 

## Pipeline Diagram

![image](assets/images/Pipeline.drawio.png)


### Configure webhooks

Add webhook in github repository. settings >> Webhooks

![image](assets/images/github_webhooks.png)

Add repository url in jenkins 

![image](assets/images/jenkins_github_url.png)

Activate hook trigger

![image](assets/images/jenkins_trigger.png)

## Pipeline Skeleton

First of all we create our pipeline skeleton with the three stages: 
* Build 
* Test
* Deploy


## Build 

### Configure github credentials
Create key in ec2 with the jenkins profile 

![image](assets/images/jenkins_git_key.png)

Add key in Github. Project repository >> Settings >> Deploy keys >> Add deploy key 

![image](assets/images/github_key.png)

 Add credential to jenkins.

![image](assets/images/jenkins_github.png)

 Add Github URL to jenkins pipeline. 

![image](assets/images/add_jenkins_url.png)

 Use credentials in pipeline

![image](assets/images/pipeline_script_github_credentials.png)

### Configure pipeline script

Create repo in github with jenkinsfiles and add the github credentials

![image](assets/images/pipeline%20script.png)

### Build image

![image](assets/images/build%20ansible%20image.png)

## Deploy

If the pipeline pass the tests, do you want to proceed for production deployment?

![image](assets/images/ansible_ask.png)

### Log with dockerhub credentials

Create dockerhub credentials

![image](assets/images/dockerhub_credentials.png)

Login dockerhub and push docker image

![image](assets/images/jenkins_push_docker.png)

### Prepare Ansible 

 * [Add shh key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) to clone Ansible repository 

 * [Add GPG key](https://docs.github.com/es/authentication/managing-commit-signature-verification/generating-a-new-gpg-key) to validate signature in commits to the repositories

![image](assets/images/pipeline_skeleton.png)

### Configure Ansible 

Install [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) and libraries dependencies with [python](https://www.scaler.com/topics/python/install-python-on-linux/) in the ec2 machine


$ pip install boto3 botocore

Configure ansible.cfg 

![image](assets/images/ansible_cfg.png)

If there isn´t ansible.cfg 

$ sudo mkdir -p /etc/ansible/

$ tocuh /etc/ansible/ansible.cfg

Create ANSIBLE_CONFIG as env variable to specify the ansible.cfg path

[image](assets/images/ansible_cfg.png)
### Create aws credentials in aws 

Install [CloudBees AWS Credentials Plugin](https://plugins.jenkins.io/aws-credentials) in jenkins

![image](assets/images/jenkins_plugin_aws.png)

Create credentials in jenkins

![iamge](assets/images/jenkins_aws_credentials.png)

## Run pipeline

![image](assets/images/Run_pipeline.png)

## Create Slave to run pipelines

### Configure the slave

![image](assets/images/slave_configuration.png)

Connect the slave throught ssh. 

![image](assets/images/ssh.png)

Add ip of the host and ssh key manually

![image](assets/images/ip_and_credentials.png)

Save and check salve connection

![image](assets/images/slave_connection.png)

### Create Terraform

Terraform [repo](https://github.com/Alismos/terraform-jenkins-slave)

### Create Ansible

Ansible [repo](https://github.com/Alismos/terraform-jenkins-slave)

### Run pipeline with slave

![image](assets/images/pipeline_with_slave.png)

![image](assets/images/pipeline_frontend.png)