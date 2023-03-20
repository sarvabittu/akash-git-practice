# Terraform Interview Questions:

### Q. What is Terraform?
Answer:Terraform is a tool for creating, updating, and versioning infrastructure securely and efficiently. Terraform is capable of managing both current and popular service providers, as well as custom in-house solutions. Configuration files notify Terraform which components are required to run a single application or an entire datacenter.

Terraform helps you Manage All of Your Infrastructure as Infrastructure as Code and promote Self-Service Infrastructure allows you to construct infrastructure as needed :

- Terraform code is written in the HCL programming language.
- Stop constructing things by hand.
- Put everything into a Terraform setup that can be repeated.
- All of the build steps are now written in code.
- It's a lot easier if you ever have to rebuild something!

### Q. What are the key features of Terraform?
Answer:Below are the key features of Terraform:
- Infrastructure as Code: A high-level configuration syntax is used to define infrastructure.
- Execution Plans: Terraform generates an execution plan during the "planning" phase.
- Resource Graph
- Change Automation 

### Q. What are most useful terraform commands?
Answer: 
![Terraform Workflow](https://k21academy.com/wp-content/uploads/2022/08/Terraform_Workflow-2048x983.jpg)
```
terraform init    # Initialize the current directory
terraform plan    # Dry run to see what Terraform will do
terraform apply   # Apply the Terraform code and build stuff
terraform destroy # Destroy what was built by Terraform
terraform refresh # Refresh the state file
terraform output  # View Terraform outputs
terraform graph   # Create a DOT-formatted graph
```

### Q.What is Terraform Cloud? ANd its different versions available?
Answer:Terraform Cloud is a hosted application that includes remote state management, API-driven runs, policy management, and other capabilities. Many users prefer a SaaS solution that is hosted in the cloud since they do not want to manage the infrastructure required to run it.

- __Terraform Enterprise___ is the same tool, but it runs in your own data centre or cloud environment. Some users want more control over the Terraform Cloud application, or they want to execute it behind corporate firewalls in restricted networks.
- ___Terraform Cloud for Business___ uses the same hosted environment as Terraform Cloud, but with additional features for larger teams. Single sign-on, audit logging, and the ability to Terraform on-premise resources from the cloud are just a few of the features available.

### Q. How does Terraform work?
Answer: Terraform creates an implementation plan, defines what it will do to achieve the desired state, and then executes it to build the infrastructure described. Terraform is capable of determining what changed and generating incremental execution plans that are practical as the configuration changes.

### Q. How to check the installed version of Terraform?
Answer: We can use terraform -version of the command to identify the version which we are running.

### Q. What are the ways to lock Terraform module versions?
Answer: You can use the terraform module registry as a source and specify the attribute’version’ in the module in a terraform configuration file. If you are using the GitHub repository as a source, you must use ‘? ref’ to specify the branch, version, and query string.

### Q. What are the key features of Terraform?
Answer: Following are the key features of Terraform:

Infrastructure as Code: Terraform’s high-level configuration language is used to define your infrastructure in human-readable declarative configuration files.
You may now create an editable, shareable, and reusable blueprint.
Terraform generates an execution plan that specifies what it will do and asks for your approval before making any infrastructure alterations. You can assess the modifications before Terraform creates, updates, or destroys infrastructure.
Terraform creates a resource graph while simultaneously developing or altering non-dependent resources. Terraform can now build resources as quickly as possible while also giving you more information about your infrastructure.
Terraform’s the automation of change allows you to apply complex changesets to your infrastructure with little to no human interaction. Terraform recognises.

### Q. What are the use cases of Terraform?
Answer: Following are the use cases of Terraform:
- Setting Up a Heroku App:
Heroku is a popular platform as a service for hosting web applications (PaaS). Developers first create an app, then add add-ons such as a database or an email service. One of the best features is the ability to scale the number of dynos or workers as needed. Most non-trivial applications, on the other hand, quickly necessitate a large number of add-ons and external services.
Terraform can be used to codify the configuration of a Heroku application, ensuring that all necessary add-ons are present, but it can also go beyond, such as configuring DNSimple to set a CNAME or Cloudflare as the app’s CDN. Best of all, Terraform can accomplish all of this in under 30 seconds without the use of a web interface.
- Clusters of Self-Service: 
A centralised operations team overseeing a large and expanding infrastructure becomes extremely difficult at a certain organisational level. Implementing “self-service” infrastructure, which allows product teams to manage their own infrastructure using tooling provided by the central operations team, becomes more appealing.
Terraform configuration can be used to keep track of how a service is built and scaled. You can then share these settings with the rest of your company, allowing client teams to manage their services using Terraform.
- Quick Creation of Environments: 
It is common to have both a production and a staging or quality assurance environment. These environments are miniature versions of their production counterparts, and they are used to test new programmes before they are released to the public. Maintaining an up-to-date staging environment becomes increasingly difficult as the production environment grows larger and more involved.
Terraform can be used to codify and share the production environment with staging, QA, and development. These parameters can be quickly used to create new testing environments that can be easily discarded. Terraform, which allows parallel environments to be created and destroyed on the fly, can help to alleviate the difficulty of maintaining them.
- Schedulers of Resources:
Static application assignment to computers becomes increasingly difficult in large-scale infrastructures. Among the schedulers that can help with this challenge are Borg, Mesos, YARN, and Kubernetes. These can be used to schedule Docker containers, Hadoop, Spark, and a variety of other software applications dynamically.
Terraform isn’t just for Amazon Web Services and other physical service providers. Terraform can request resources from resource schedulers because they can be viewed as providers. Terraform can now work in layers, such as deploying the physical infrastructure that powers the schedulers and provisioning into the scheduled grid.
- Demonstrations of software:
In today’s world, software is becoming increasingly networked and distributed. Although virtualized demo environments can be created with tools such as Vagrant, displaying software on real infrastructure that closely replicates production environments remains difficult.
A Terraform configuration can be used by software authors to design, provision, and bootstrap a demo on cloud providers such as AWS. End users can simply demo the application on their own infrastructure, and configuration options such as cluster size can be changed to evaluate tools at any scale.

### Q. How to create a SSH in Terraform when using AWS?
Answer: SSH private keys for Terraform can be created using tls_private_key
```
variable "terraform_key" {}

resource "tls_private_key" "example" {
  algorithm = "RSA"
  rsa_bits  = 4096
}

resource "aws_key_pair" "generated_key" {
  terraform_key   = var.terraform_key
  public_key = tls_private_key.example.public_key_openssh
}

data "aws_ami" "ubuntu" {
  most_recent = true

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-focal-20.04-amd64-server-*"]
  }

  filter {
    name   = "virtualization-type"
    values = ["hvm"]
  }

  owners = ["0977"] # Canonical
}

resource "aws_instance" "web" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = "t2.micro"
  terraform_key      = aws_key_pair.generated_key.terraform_key

  tags {
    Name = "Terraform Example"
  }
}
```

### Q. How to upgrade terraform to a specific version ?
Answer: After installation using brew install tfenv for installing terraform we can select the specific version -
```
$ tfenv list-remote
0.13.0
0.13.0-rc1
0.13.0-beta2
0.13.0-beta1
0.13.0
0.11.15
...

$ tfenv install 0.11.15
[INFO] Installing Terraform v0.11.15
[INFO] Downloading release tarball from https://releases.hashicorp.com/terraform/0.11.15/terraform_0.11.14_darwin_amd64.zip
...
[INFO] Installation of terraform v0.11.15 successful
[INFO] Switching to v0.11.14
[INFO] Switching completed
```

### Q. How to set up a lambda function triggered by a scheduled event source when using Terraform?
Answer: This can be achieved using aws_cloudwatch_event_target as follows -
```
resource "aws_lambda_function" "check_javainuse" {
    filename = "check_javainuse.zip"
    function_name = "checkFoo"
    role = "arn:aws:iam::424242:role/something"
    handler = "index.handler"
}

resource "aws_cloudwatch_event_rule" "check_every_ten_minutes" {
    name = "every-ten-minutes"
    description = "Fires every ten minutes"
    schedule_expression = "rate(10 minutes)"
}

resource "aws_cloudwatch_event_target" "check_javainuse_every_ten_minutes" {
    rule = ""
    target_id = "check_javainuse"
    arn = ""
}

resource "aws_lambda_permission" "allow_cloudwatch_to_call_check_foo" {
    statement_id = "AllowExecutionFromCloudWatch"
    action = "lambda:InvokeFunction"
    function_name = ""
    principal = "events.amazonaws.com"
    source_arn = ""
```

### Q. How to make use of AND/OR operators in Terraform?
Answer: Terraform has no defined binary types. How ever we can make use of Simple math for [interpolations (https://developer.hashicorp.com/terraform/language/v1.1.x/configuration-0-11/interpolation#math).
```
count = signum( + )
```

### Q. How to attach AWS managed policies to a role for Terraform?
Answer: This can be achieved using Data Source: [aws_iam_policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy.html)
```
data "aws_iam_policy" "ReadWriteAccess" {
  arn = "arn:aws:iam::aws:policy/ReadWriteAccess"
}
```
### Q. How to index all attributes when using DynamoDB with Terraform ?
Answer: This can be achieved using the [AttributeDefinition](https://docs.aws.amazon.com/amazondynamodb/latest/APIReference/API_AttributeDefinition.html)
```
resource "aws_dynamodb_table" "test-javainuse" {
  name           = "javainuse-table-name"
  read_capacity  = 5
  write_capacity = 5
  hash_key       = "javainuse-attribute"

  attribute {
    name = "javainuse-attribute"
    type = "S"
  }
}
```

### Q.How does Terraform help in discovering plugins?
Answer: Terraform interprets configuration files in the operational directory with the authority “Terraform init.” Then, Terraform determines the necessary plugins and searches for installed plugins in various locations. Terraform may also download additional plugins at times. Then it decides which plugin versions to use and creates a security device file to ensure that Terraform uses the same plugin versions.

### Q. What is module in terraform?
Answer: A module is a container for several resources that are used in conjunction with one another. Modules can be used to construct lightweight abstractions, allowing you to define the infrastructure in terms of architecture instead of physical objects.

- A Terraform module is a set of Terraform configuration files contained within a single directory. Or a basic configuration with a single directory having one or more .tf file is a module. When Terraform commands are run directly from such a directory, it is referred to as the root module.

In this way, each Terraform configuration is a module. You may have a basic collection of Terraform configuration files like:
```
.
|--- LICENSE
|--- README.md
|--- main.tf
|--- variables.tf
|--- output.tf
```

### Q. What is Private Module Registry?
Answer: Terraform Cloud provides a Private Module Registry, which allows you to store, version, and distribute modules to your organisations and teams.

### Q. What is main.tf in terraform?
Answer: main.tf contains the primary configuration for your module. You can also build additional configuration files and arrange them in some helpful way for your project. Variable definitions for your module will be stored in variables.tf.

### Q. How do you call a main.tf module?
Answer: When you run terraform plan or terraform apply, the.tf files in your working directory combine to form the root module. This module will call other modules and bind them by transferring output values from one to input values from another.


### Q. What language does terraform use?
Answer: Terraform configuration syntax is known as HashiCorp Configuration Language (HCL). It is designed to be both human-readable and editable, as well as machine-friendly. Terraform can also read JSON configurations for machine-friendliness.

### Q. How does terraform integrate with github and public cloud?
Answer:The majority of businesses are migrating to the public cloud. Managing infrastructure in a secure and controlled manner is a critical step for businesses.

Check out this [Terraform + GCP + Git Complete Example](https://www.techgeeknext.com/cloud/terraform-gcp-github-example) to learn how to use terraform to provision infrastructure on Cloud while keeping the infrastructure code in a github repository.

### Q. What is Terraform State?
Answer: Terraform keeps track of the resources it has created in a state file. This crucial file contains all of the information Terraform requires to change, update, and delete infrastructure.

The state file is saved in your local workspace by default. We can use Terraform Cloud to store the state file as a Remote State on the cloud.

### Q. What are the disadvantages of maintaining the Terraform state file on the local machine?
Answer: 
- State file sometimes contains secrets or sensitive data may be exposed
- We are unable to collaborate with the team because the file is on someone's laptop.
- On a local machine, there is a possibility of losing or deleting the state file.
- There is no centralised record keeping to track historical developments.

### Q. What exactly is Sentinel?
Answer: Sentinel is the policy enforcement language used by HashiCorp. Sentinel policies are validated when the Terraform plan is executed. Sentinel will detect incorrect settings before they reach production, not later.

![Sentinel Policy](https://www.techgeeknext.com/img/terraform/terraform-sentinel-policy.png)

We can choose the scope of Sentinel policies that will be enforced at the Organization or Workspace level.
```
# Restricting region in GCP
google_region_valid = rule {
  all region_values as rv {
    rv == "us-west-1"
  }
}
```

### Q. What exactly do you mean when you say Policy-as-Code?
Answer: 
- Treat policies as applications
- Store in version control
- Proactive vs. reactive
- Automate enforcement and review
- Automate logic testing

### Q. Can you provide few examples where we can use for Sentinel policies?
Answer: Sentinel is a powerful tool that can be used to implement a variety of policies. Here are a few examples:
***Security Standards***
- Forbid or allow only certain resources, providers or data sources
- Restrict roles the cloud provider can assume
- Restrict roles the cloud provider can assume

***Audit Tracking***
- Review an audit trail for Terraform Cloud operations
- Enforce explicit ownership in resources

***Resource Restriction***
- Limit the size of VMs and clusters for cost
- Enforce mandatory tagging on resources built with Terraform
- Restrict modules to your organizations Private Module Registry

### Q. What are the various levels of sentinel enforcement?
Answer: Sentinel is a powerful tool that can be used to implement a variety of policies. Here are a few examples:
***Advisory :***
- Logged but allowed to pass
- When a user triggers a plan that violates the policy, an advisory is issued to the user.

***Soft-Mandatory :***
- Teams based permissions for overrides
- Overrides logged for audit if the policy fails
- Prevents non-compliant infrastructure from being deployed by regular users. Only administrators have the ability to overrule.

***Hard-Mandatory :***
- Default enforcement level
- The policy must pass
- Only way to override is to explicitly remove the policy
- Prevents non-compliant infrastructure from being deployed by all users and apps.

### Q. Why write tests for Sentinel policies?
Answer:
- Policies and infrastructure are prone to change for refactoring.
- Writing tests assures that your policy will continue to work as intended even if things change.
- Writing testing instils trust in the policymaking process.

### Q. How to Store Sensitive Data in Terraform?
Answer: In order to communicate with your cloud provider's API, Terraform requires credentials. Although config files and environment variables are a preferable alternative, the credentials are still saved in plaintext on your desktop.

*Every day, GitHub is exposed to thousands of API and cryptographic keys! Protecting sensitive variables such as Cloud API Keys, Passwords, SSH private keys, SSL certificates, and other sensitive text or data is critical. So these API keys should never be stored in terraform code directly.*

Sensitive Variable is Secure Place for API Credentials : Terraform Cloud can securely store and encrypt your passwords. This encrypted storage can be used to store passwords, TLS certificates, SSH keys, and anything else that shouldn't be stored in plain text.

### Q. How can terraform plan aid in the development process?
A. Validates your expectations against the execution plan without permanently modifying state
B. Initializes your working directory containing your Terraform configuration files
C. Formats your Terraform configuration files
D. Reconciles Terraformג€™s state against deployed resources and permanently modifies state using the current status of deployed resources
Answer: A (Readmore from [here](https://github.com/hashicorp/terraform/issues/19235)


### Q. Imagine you have a Terraform module that deploys an application to a single server instance. How would you modify the module to deploy the application to multiple server instances?
Answer: You can modify the Terraform module to deploy the application to multiple server instances by using a loop in the resource definition. For example, you could use a count parameter to specify the number of server instances to deploy and then use the count.index variable to reference each instance in the resource definition.

### Q. You are working on a Terraform project that needs to provision an S3 bucket, and a user with read and write access to the bucket. What resources would you use to accomplish this, and how would you configure them?
Answer: To provision an S3 bucket and a user with read and write access to the bucket, you can use the aws_s3_bucket and aws_iam_user resources in Terraform. You can then use the aws_iam_user_policy_attachment resource to attach a policy to the user that grants them read and write access to the bucket. Here is an example of how you could configure these resources:

```
resource "aws_s3_bucket" "my_bucket" {
  bucket = "my-bucket"
}

resource "aws_iam_user" "my_user" {
  name = "my-user"
}

resource "aws_iam_user_policy_attachment" "my_policy_attachment" {
  user       = aws_iam_user.my_user.name
  policy_arn = "arn:aws:iam::aws:policy/AmazonS3FullAccess"
}
```

### Q. How do you manage sensitive data in Terraform, such as API keys or passwords?
Answer: Terraform provides several ways to manage sensitive data, including using environment variables, using the Vault provider, and using the SSM parameter store. One common way to manage sensitive data is to use environment variables, which can be referenced in the Terraform code using the "${var.VARIABLE_NAME}" syntax. The actual values of the variables can be stored securely in a separate file or managed by a separate tool.

### Q. Suppose you are working on a project that requires provisioning a new VPC with a public and private subnet. How would you write the Terraform code to accomplish this task?
Answer: To provision a new VPC with a public and private subnet, you can use the aws_vpc, aws_subnet, and aws_internet_gateway resources in Terraform. Here is an example of how you could configure these resources:

```
resource "aws_vpc" "my_vpc" {
  cidr_block = "10.0.0.0/16"
}

resource "aws_subnet" "public_subnet" {
  vpc_id     = aws_vpc.my_vpc.id
  cidr_block = "10.0.1.0/24"
}

resource "aws_subnet" "private_subnet" {
  vpc_id     = aws_vpc.my_vpc.id
  cidr_block = "10.0.2.0/24"
}

resource "aws_internet_gateway" "my_gateway" {
  vpc_id = aws_vpc.my_vpc.id
}

resource "aws_route_table" "public_route_table" {
  vpc_id = aws_vpc.my_vpc.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.my_gateway.id
  }
}

resource "aws_route_table_association" "public_association" {
  subnet_id      = aws_subnet.public_subnet.id
  route_table_id = aws_route_table.public_route_table.id
}
```
