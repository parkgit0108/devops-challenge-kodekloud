variable.tf
```sql
variable "KKE_VPC_CIDR" {
  description = "CIDR block for the VPC"
  type        = string
  default     = "10.0.0.0/16"
}

variable "KKE_SUBNET_CIDR" {
  description = "CIDR block for the subnet"
  type        = string
  default     = "10.0.1.0/24"
}
```
outputs.tf
```sql
output "KKE_vpc_name" {
  description = "Name of the VPC"
  value       = aws_vpc.xfusion_priv_vpc.tags["Name"]
}

output "KKE_subnet_name" {
  description = "Name of the subnet"
  value       = aws_subnet.xfusion_priv_subnet.tags["Name"]
}

output "KKE_ec2_private" {
  description = "Name of the EC2 instance"
  value       = aws_instance.xfusion_priv_ec2.tags["Name"]
}
```
main.tf
```sql
resource "aws_vpc" "xfusion_priv_vpc" {
  cidr_block           = var.KKE_VPC_CIDR
  enable_dns_support   = true
  enable_dns_hostnames = true

  tags = {
    Name = "xfusion-priv-vpc"
  }
}

resource "aws_subnet" "xfusion_priv_subnet" {
  vpc_id                  = aws_vpc.xfusion_priv_vpc.id
  cidr_block              = var.KKE_SUBNET_CIDR
  map_public_ip_on_launch = false

  tags = {
    Name = "xfusion-priv-subnet"
  }
}

resource "aws_security_group" "xfusion_priv_sg" {
  name        = "xfusion-priv-sg"
  description = "Allow traffic only from within the VPC CIDR"
  vpc_id      = aws_vpc.xfusion_priv_vpc.id

  ingress {
    description = "Allow all inbound from VPC CIDR"
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = [var.KKE_VPC_CIDR]
  }

  egress {
    description = "Allow all outbound within VPC CIDR"
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = [var.KKE_VPC_CIDR]
  }

  tags = {
    Name = "xfusion-priv-sg"
  }
}

data "aws_ami" "amazon_linux_2" {
  most_recent = true
  owners      = ["amazon"]

  filter {
    name   = "name"
    values = ["amzn2-ami-hvm-*-x86_64-gp2"]
  }

  filter {
    name   = "virtualization-type"
    values = ["hvm"]
  }
}

resource "aws_instance" "xfusion_priv_ec2" {
  ami                         = data.aws_ami.amazon_linux_2.id
  instance_type               = "t2.micro"
  subnet_id                   = aws_subnet.xfusion_priv_subnet.id
  vpc_security_group_ids      = [aws_security_group.xfusion_priv_sg.id]
  associate_public_ip_address = false

  lifecycle {
    ignore_changes = [vpc_security_group_ids]
  }

  tags = {
    Name = "xfusion-priv-ec2"
  }
}
```
```sql
cd /home/bob/terraform
terraform init
terraform apply -auto-approve
terraform plan
```
