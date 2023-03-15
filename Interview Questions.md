# Terraform Interview Questions:

### 1. Imagine you have a Terraform module that deploys an application to a single server instance. How would you modify the module to deploy the application to multiple server instances?
Answer: You can modify the Terraform module to deploy the application to multiple server instances by using a loop in the resource definition. For example, you could use a count parameter to specify the number of server instances to deploy and then use the count.index variable to reference each instance in the resource definition.

### 2. You are working on a Terraform project that needs to provision an S3 bucket, and a user with read and write access to the bucket. What resources would you use to accomplish this, and how would you configure them?
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

### 3. How do you manage sensitive data in Terraform, such as API keys or passwords?
Answer: Terraform provides several ways to manage sensitive data, including using environment variables, using the Vault provider, and using the SSM parameter store. One common way to manage sensitive data is to use environment variables, which can be referenced in the Terraform code using the "${var.VARIABLE_NAME}" syntax. The actual values of the variables can be stored securely in a separate file or managed by a separate tool.

### 4. Suppose you are working on a project that requires provisioning a new VPC with a public and private subnet. How would you write the Terraform code to accomplish this task?
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
