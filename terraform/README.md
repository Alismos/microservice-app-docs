# Microservice infraestructure in AWS

## To be architecture 

![image](assets/images/terraform%20architecture.drawio.png)
## Configuración de Terraform

### Previous requirements 
* [Terraform Cli](https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/aws-get-started)
* [AWS Cli](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
* AWS account and [credentials](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html) 

To use IAM credentials to authenticate the Terraform AWS provider, the AWS_ACCESS_KEY_ID environment variable must be set.

**$ export AWS_ACCESS_KEY_ID=<aws_key_id>**

Secret key.

**$ export AWS_SECRET_ACCESS_KEY=<aws_secret>**

main.tf file with the terraform settings and deploy ec2 instances.

![image](assets/images/terraform_block.png)

The terraform {} block contains the Terraform configuration, including any necessary providers that Terraform will use to provide the infrastructure.

## Desplegar instancias ec2 

The resource block is used to define the components of your infrastructure. In this case we will define the ec2 instances.

![image](assets/images/frontend_instance.png)

Once our architecture is defined.

**$terraform init**

Once our architecture is defined.

**$terraform fmt**

To format our code.

**$terraform apply**

To deploy our architecture

![image](assets/images/ec2_instances_in_AWS.png)

## Configuration variables

The directory **variables.tf** contains all the variables for configuring our resources. 

![image](assets/images/terraform_variables.gif)


## Security groups

To configure our security group we are to create the rules allowing ssh to our machine, the slave we are going to configure in jenkins and the port our api is going to expose.

![image](assets/images/sg_terraform.png)

EC2 intance in aws

![image](assets/images/terraform_sg_aws.png)

## Load balancer

We are going to define our target group in the vpc the load balancer is going to target. 

![image](assets/images/target_load_balancer.png)

After creating our target groupd we must attach the required EC2 Instances with the target group.

![image](assets/images/attach_load_balancer.png)

Creation of the Application Load Balancer.

![image](assets/images/application_load_balancer.png)

Attach the listener rule for the ALBs created

![image](assets/images/listener_load_balancer.png)

Load balancer in aws

![image](assets/images/terraform_lb.png)

## Optional
### Providing

To provide our machines we must determine the applications that it needs, the files to deploy our application and the hosts where the null resource is going to be connected. 

![image](assets/images/terraform_providing.png)

## Demo

![image](assets/images/demo.gif)



