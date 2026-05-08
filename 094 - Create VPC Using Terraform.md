```sql
# create main.tf
resource "aws_vpc" "datacenter_vpc" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "datacenter-vpc"
  }
}
```
```sql
terraform init
terraform apply -auto-approve
```
