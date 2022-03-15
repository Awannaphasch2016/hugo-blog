+++
title = "Using Terraform to set up ec2 instances for data science projects."
author = ["Anak Wannaphaschaiyong"]
tags = ["ec2", "blog", "terraform"]
draft = false
+++

## Take Away {#take-away}

-   you will learn how to automate ec2 setup using terraform that is
    suited for data science project.


## Tools {#tools}

-   EC2
-   Terraform


## Requirements {#requirements}


### Knowledge Requirements {#knowledge-requirements}

-   understand basic of how to create terraform project
-   understand basic of how to set up ec2 instances


### System Requirements {#system-requirements}

-   WSL/Ubuntu
    -   I have only tested this in WSL

-   install all dependencies of cuda
    -   for list of software requirements, see
        -   <https://www.tensorflow.org/install/gpu#linux_setup>

-   optional
    -   Docker # References

-   Terraform AWS documentation
    -   <https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance#availability_zone>

-   pytorch docker image
    -   <https://github.com/anibali/docker-pytorch> # Content


## Code {#code}


### AWS {#aws}

1.  export the following environment variables including
    -   AWS_ACCESS_KEY_ID
    -   AWS_SECRET_ACCESS_KEY
    -   AWS_DEFAULT_REGION


### Terraform {#terraform}

1.  create terraform project
2.  In the project, create main.tf and copy&amp;paste the following code

<!--listend-->

```text
    resource "aws_instance" "web" {
      ami = "ami-08962a4068733a2b6"
      instance_type = "p3.8xlarge"
      cpu_core_count = 16
      cpu_threads_per_core = 2
      tags = {
        Name = "HelloWorld"
      }

    }
```

1.  now you have ec2 running with
