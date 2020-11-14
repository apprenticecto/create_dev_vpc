# Create A Development VPC

In this [repo](https://github.com/apprenticecto/create-aws-ec2-with-terraform) we configured AWS CLI, created an IAM user and created an ec2 to the [default VPC](https://docs.aws.amazon.com/vpc/latest/userguide/default-vpc.html). 

Now we'll make use of Terraform modules to create a development VPC and a management VPN, deployed onto two [availability zones](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/), with private addresses, public addresses and [NAT gatway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) enabled. We'll launch two basic EC2 instances.

This slightly more complex configuration makes use of the following concepts:
 - [Terraform modules](https://registry.terraform.io/search/modules?q=modules), specifically [VPC](https://github.com/terraform-aws-modules/terraform-aws-vpc) and [EC2](https://github.com/terraform-aws-modules/terraform-aws-ec2-instance) ones.
 - [Terraform input variables](https://www.terraform.io/docs/configuration/variables.html)
 - [Separation between dev and prod](https://learn.hashicorp.com/tutorials/terraform/organize-configuration?in=terraform/modules): we'll only see dev here, through directories.
 
## Build your infrastructure

Cd into your dev folder and:
- launch `terraform init`
- launch `terraform fmt`
- launch `terraform apply` and enter 'yes' when prompted.

At the end of the creation you should see your output variables value:
```
Apply complete! Resources: 22 added, 0 changed, 0 destroyed.

Outputs:

ec2_instance_public_ips = [
  "<first instance public ip address is shown here>",
  "<second instance public ip address is shown here",
]
vpc_public_subnets = [
  "<first public subnet value is shown here",
  "<second public subnet value is shown here",
]

```

## INspct Your Infrastructure

Terraform writes configuration data into a file called `terraform.tfstate`, which you have in your local repo. This file contains the IDs and properties of the resources Terraform created so that Terraform can manage or destroy those resources going forward.

To inspect your infrastructure configuration launch `terraform show`.

## Destroy Your infrastructure

Launch `terraform destroy` and enter 'yes' when prompted.


