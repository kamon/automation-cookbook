
# Building infrastructure on Amazon AWS using Terraform

## Installation

For details, see https://www.terraform.io/intro/getting-started/install.html.

## Launch an AWS EC2 instance

As a prerequisite, read the following documentation to better understand your AWS services and account details:

* http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/default-vpc.html
* https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html

With Terraform, you do things in 3 steps:

* 1. Write the configuration needed.
* 2. Run the *execution plan*.
* 3. *Apply the configuration*.

### Write the configuration needed to launch the instance

In this scenario, we will use an "t2.micro" EC2 instance.

If needed, get the following info via the AWS management console or AWSCLI:

* The region that was currently defined for my account: us-west-2,
* The name of an available AMI for Linux to use (Ubuntu): ami-7172b611.
  
Then add an example.tf file, using these details:

```
provider "aws" {
  access_key = "ACCESS_KEY_HERE"
  secret_key = "SECRET_KEY_HERE"
  region     = "us-west-2" 
}

resource "aws_instance" "example" {
  ami           = "ami-7172b611"
  instance_type = "t2.micro"
}
```

A provider, in this case *AWS*, is responsible for creating and managing resources. See https://www.terraform.io/docs/providers/ for more information.

The resource block defines a resource that exists within the infrastructure. It can be:
* A physical component such as an EC2 instance,
* An Heroku application,
* ...

### Run the Terraform execution plan

In the same directory as the *example.tf* file, we will use the "terraform plan" command.

```
$ terraform plan

...

+ aws_instance.example
    ami:                      "" => "ami-7172b611"
    availability_zone:        "" => "<computed>"
    ebs_block_device.#:       "" => "<computed>"
    ephemeral_block_device.#: "" => "<computed>"
    instance_state:           "" => "<computed>"
    instance_type:            "" => "t2.micro"
    key_name:                 "" => "<computed>"
    placement_group:          "" => "<computed>"
    private_dns:              "" => "<computed>"
    private_ip:               "" => "<computed>"
    public_dns:               "" => "<computed>"
    public_ip:                "" => "<computed>"
    root_block_device.#:      "" => "<computed>"
    security_groups.#:        "" => "<computed>"
    source_dest_check:        "" => "true"
    subnet_id:                "" => "<computed>"
    tenancy:                  "" => "<computed>"
    vpc_security_group_ids.#: "" => "<computed>"

```

This command shows the changes Terraform will apply to your infrastructure given the current state of your 
infrastructure as well as the current contents of your configuration.


### Apply the configuration

```
$ terraform apply

aws_instance.example: Creating...
  ami:                      "" => "ami-7172b611"
  availability_zone:        "" => "<computed>"
  ebs_block_device.#:       "" => "<computed>"
  ephemeral_block_device.#: "" => "<computed>"
  instance_state:           "" => "<computed>"
  instance_type:            "" => "t2.micro"
  key_name:                 "" => "<computed>"
  placement_group:          "" => "<computed>"
  private_dns:              "" => "<computed>"
  private_ip:               "" => "<computed>"
  public_dns:               "" => "<computed>"
  public_ip:                "" => "<computed>"
  root_block_device.#:      "" => "<computed>"
  security_groups.#:        "" => "<computed>"
  source_dest_check:        "" => "true"
  subnet_id:                "" => "<computed>"
  tenancy:                  "" => "<computed>"
  vpc_security_group_ids.#: "" => "<computed>"
aws_instance.example: Still creating... (10s elapsed)
aws_instance.example: Still creating... (20s elapsed)
aws_instance.example: Creation complete

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

The state of your infrastructure has been saved to the path
below. This state is required to modify and destroy your
infrastructure, so keep it safe. To inspect the complete state
use the `terraform show` command.

State path: terraform.tfstate
```

Done!

Terraform also put some state into the terraform.tfstate file by default. 
This state file maps various resource metadata to actual resource IDs so that Terraform knows what it is managing. 
It must be saved and distributed to anyone who might run Terraform. Put it into version control!

You can inspect the state using "terraform show":

```
aws_instance.example:
  id = i-34c0799b
  ami = ami-7172b611
  availability_zone = us-west-2b
  disable_api_termination = false
  ebs_block_device.# = 0
  ebs_optimized = false
  ephemeral_block_device.# = 0
  iam_instance_profile = 
  instance_state = running
  instance_type = t2.micro
  key_name = 
  monitoring = false
  private_dns = ip-172-31-27-30.us-west-2.compute.internal
  private_ip = 172.31.27.30
  public_dns = ec2-52-39-168-113.us-west-2.compute.amazonaws.com
  public_ip = 52.39.168.113
  root_block_device.# = 1
  root_block_device.0.delete_on_termination = true
  root_block_device.0.iops = 100
  root_block_device.0.volume_size = 8
  root_block_device.0.volume_type = gp2
  security_groups.# = 0
  source_dest_check = true
  subnet_id = subnet-7fe27b1b
  tags.# = 0
  tenancy = default
  vpc_security_group_ids.# = 1
  vpc_security_group_ids.824438014 = sg-a23988c4
```

## Launch an AWS EC2 instance - Using variables

* Let's start with the configuration.

Modify the configuration file to use variables:

```
provider "aws" {
    access_key = "${var.access_key}"
    secret_key = "${var.secret_key}"
    region     = "${var.region}" 
}

resource "aws_instance" "example" {
  ami           = "ami-7172b611"
  instance_type = "t2.micro"
}
```

Create a new file called *variables.tf* to set the variables:

```
variable "region" {
    type = "string"

    default = "us-west-2"
}

variable "access_key" {
    type = "string"

    default = "foo"
}

variable "secret_key" {
    type = "string"

    default = "bar"
}

```

* Run the execution plan as usual.

* Finally, apply:

```
$ terraform apply
aws_instance.example: Creating...
  ami:                      "" => "ami-7172b611"
  availability_zone:        "" => "<computed>"
  ebs_block_device.#:       "" => "<computed>"
  ephemeral_block_device.#: "" => "<computed>"
  instance_state:           "" => "<computed>"
  instance_type:            "" => "t2.micro"
  key_name:                 "" => "<computed>"
  placement_group:          "" => "<computed>"
  private_dns:              "" => "<computed>"
  private_ip:               "" => "<computed>"
  public_dns:               "" => "<computed>"
  public_ip:                "" => "<computed>"
  root_block_device.#:      "" => "<computed>"
  security_groups.#:        "" => "<computed>"
  source_dest_check:        "" => "true"
  subnet_id:                "" => "<computed>"
  tenancy:                  "" => "<computed>"
  vpc_security_group_ids.#: "" => "<computed>"
aws_instance.example: Still creating... (10s elapsed)
aws_instance.example: Still creating... (20s elapsed)
aws_instance.example: Creation complete

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
...
```

## Changing infrastructure

TODO...


## Destroying infrastructure

Destroying your infrastructure is a rare event in production environments. But if you're using Terraform 
to spin up multiple environments such as development, test, QA environments, then destroying is a useful action.

Before destroying our infrastructure, we can use the plan command to see what resources Terraform will destroy.

```
$ terraform plan -destroy

aws_instance.example: Refreshing state...

The Terraform execution plan has been generated and is shown below.
Resources are shown in alphabetical order for quick scanning. Green resources
will be created (or destroyed and then created if an existing resource
exists), yellow resources are being changed in-place, and red resources
will be destroyed.

Note: You didn't specify an "-out" parameter to save this plan, so when
"apply" is called, Terraform can't guarantee this is what will execute.

- aws_instance.example
```

To destroy the infrastructure:

```
$ terraform destroy
```

## Launch an AWS EC2 instance with an Elastic IP

See https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html

Change the example.tf file to:

```
provider "aws" {
  access_key = "ACCESS_KEY_HERE"
  secret_key = "SECRET_KEY_HERE"
  region     = "us-west-2"
}

resource "aws_instance" "example" {
  ami           = "ami-7172b611"
  instance_type = "t2.micro"
}

resource "aws_eip" "ip" {
    instance = "${aws_instance.example.id}"
}
```

Then, plan:

```
$ terraform plan

+ aws_eip.ip
    allocation_id:     "" => "<computed>"
    association_id:    "" => "<computed>"
    domain:            "" => "<computed>"
    instance:          "" => "${aws_instance.example.id}"
    network_interface: "" => "<computed>"
    private_ip:        "" => "<computed>"
    public_ip:         "" => "<computed>"

+ aws_instance.example
    ami:                      "" => "ami-7172b611"
    availability_zone:        "" => "<computed>"
    ebs_block_device.#:       "" => "<computed>"
    ephemeral_block_device.#: "" => "<computed>"
    instance_state:           "" => "<computed>"
    instance_type:            "" => "t2.micro"
    key_name:                 "" => "<computed>"
    placement_group:          "" => "<computed>"
    private_dns:              "" => "<computed>"
    private_ip:               "" => "<computed>"
    public_dns:               "" => "<computed>"
    public_ip:                "" => "<computed>"
    root_block_device.#:      "" => "<computed>"
    security_groups.#:        "" => "<computed>"
    source_dest_check:        "" => "true"
    subnet_id:                "" => "<computed>"
    tenancy:                  "" => "<computed>"
    vpc_security_group_ids.#: "" => "<computed>"


Plan: 2 to add, 0 to change, 0 to destroy.
```

Apply the new configuration:

```
$ terraform apply
...
```

From the documentation, about dependencies:
```
Most dependencies in Terraform are implicit: Terraform is able to infer dependencies based on usage of attributes 
of other resources.
```


