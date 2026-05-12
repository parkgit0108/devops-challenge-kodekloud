```sql
#main.tf
resource "aws_sns_topic" "nautilus_sns_topic" {
  name = "nautilus-sns-topic"
}

resource "aws_instance" "nautilus_ec2" {
  ami           = "ami-0c02fb55956c7d316"
  instance_type = "t2.micro"

  lifecycle {
    ignore_changes = [vpc_security_group_ids, subnet_id]
  }

  tags = {
    Name = "nautilus-ec2"
  }
}

resource "aws_cloudwatch_metric_alarm" "nautilus_alarm" {
  alarm_name          = "nautilus-alarm"
  comparison_operator = "GreaterThanOrEqualToThreshold"
  evaluation_periods  = 1
  metric_name         = "CPUUtilization"
  namespace           = "AWS/EC2"
  period              = 300
  statistic           = "Average"
  threshold           = 90

  dimensions = {
    InstanceId = aws_instance.nautilus_ec2.id
  }

  alarm_actions     = [aws_sns_topic.nautilus_sns_topic.arn]
  alarm_description = "Alarm when CPU utilization exceeds 90% for 1 consecutive 5-minute period"

  tags = {
    Name = "nautilus-alarm"
  }
}
```
```sql
#outputs.tf
output "KKE_instance_name" {
  description = "Name of the EC2 instance"
  value       = aws_instance.nautilus_ec2.tags["Name"]
}

output "KKE_alarm_name" {
  description = "Name of the CloudWatch alarm"
  value       = aws_cloudwatch_metric_alarm.nautilus_alarm.alarm_name
}
```
```sql
cd /home/bob/terraform
terraform init
terraform apply -auto-approve
terraform plan
```
