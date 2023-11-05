# auto-scaling-nodejs-test-app

From the following video https://youtu.be/lB3Ip0Yn-Zs?si=PCfQd6bTFDA8PwLq

## AWS setup

### Create Security Group

- EC2 -> Security Groups
- Create security group
- Set name
- Set Description
- Default VPC
- Add inbound rules
- SSH 22 Anywhere
- HTTP 80 Anywhere
- HTTPS 443 Anywhere
- Custom 3000 Anywhere
- Click Create

### Create Launch Template

- EC2 -> Launch Templates
- Create Launch Templates
- Set name
- Check Provide guidance
- Select Amazon Linux 2 AMI
- Select t3a.nano or t2.micro (free tier) instance type
- Select existing key pair or create one
- Select existing security group
- Select Advanced Details
- Update User data with code from user_data_script.sh 
- Click Create Launch Template

### Create Auto Scaling Group

- EC2 -> Auto Scaling Groups
- Click Create Auto Scaling Group
- Set name
- Select launch template
- Select Latest Version
- Click  next
- Select default VPC
- Select top 3 availability zones
- Click  next
- Select attach a new load balancer
- Give it a unique name
- Select internet-facing load balancer scheme
- For default routing select Create a target group
- Click next
- Select desired, min and max capacity
- Select target tracking scaling policy
- Leave it as Average CPU Utilization with target of 50%
- Click next
- Add notification email if required
- Click next
- Click Create Auto Scaling Group

Now the minimum number of EC2 instances should spin up.
From each instance you can grab the IP and load it in your browser with the port number 3000.
You should see the test app.
You can get the load balancer URL and load it in your browser with standard port 80
You should see the test app.

Set permission on key pair
- chmod 400 ~/Documents/aws/aws-key.pem

SSH into instance
- Get instance IP
- ssh -i ~/Documents/aws/aws-key.pem ec2-user@44.193.8.167 
