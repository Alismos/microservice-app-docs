# Jenkins

## Requirements

* Install jenkins in [debian/ubuntu](https://www.jenkins.io/doc/book/installing/linux/#debianubuntu)

* Create EC2 machine in aws 

## Configure Jenkins

When launching jenkins we can create our admin credentials or use the default admin credentials. 

## Pipeline Diagram

![image](assets/images/Pipeline.drawio.png)

## Pipeline Skeleton

First of all we create our pipeline skeleton with the three stages: 
* Build 
* Test
* Deploy

### Prepare Ansible 

 * [Add shh key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) to clone Ansible repository 

 * [Add GPG key](https://docs.github.com/es/authentication/managing-commit-signature-verification/generating-a-new-gpg-key) to validate signature in commits to the repositories
![image](assets/images/pipeline_skeleton.png)

## Deploy 

### Configure github credentials
Create key in ec2 with the jenkins profile 

![image](assets/images/jenkins_git_key.png)

Add key in Github. Project repository >> Settings >> Deploy keys >> Add deploy key 

![image](assets/images/github_key.png)

 Add credential to jenkins.

![image](assets/images/jenkins_github.png)

 Add Github URL to jenkins pipeline. 

![image](assets/images/pipeline_github.png)

 Use credentials in pipeline

![image](assets/images/pipeline_script_github_credentials.png)

### Configure Ansible 

Install [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) and libraries dependencies with [python](https://www.scaler.com/topics/python/install-python-on-linux/) in the ec2 machine


$ pip install boto3 botocore

Configure ansible.cfg 

![image](assets/images/ansible_cfg.png)

If there isn´t ansible.cfg 

$ sudo mkdir -p /etc/ansible/
$ tocuh /etc/ansible/ansible.cfg

### Create aws credentials in aws 

Install [CloudBees AWS Credentials Plugin](https://plugins.jenkins.io/aws-credentials) in jenkins

![image](assets/images/jenkins_plugin_aws.png)

Create credentials in jenkins

![iamge](assets/images/jenkins_aws_credentials.png)
