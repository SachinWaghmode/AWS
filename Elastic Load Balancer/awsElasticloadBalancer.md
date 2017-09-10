#Key Steps Are:

Create or Select a Launch Configuration
Create an Auto Scaling Group
Using a Load Balancer With an Auto Scaling Group

PART 1 - CREATE LAUNCH CONFIG AND AUTOSCALE GROUP

# Tutorial: Set Up a Scaled and Load-Balanced Application

    DOC:  http://docs.aws.amazon.com/autoscaling/latest/userguide/as-register-lbs-with-asg.html
    
## Create or Select a Launch Configuration

    Select My AMI:                     aws-php-ami
    Instance Type:                     T2-Micro (Free Tier)
    Launch Configuration Name:  aws-php-autoscale
    Enable Monitoring:                Enable CloudWatch detailed monitoring
    Select Public IP:                    Assign a public IP address to every instance.
    Security Group:                     cmpe281-dmz (SG)
    Select Key Pair:                     cmpe281-us-west-1
    Select VPC:                           cmpe281 (VPC) & Public Subnet
    

## Create an Auto Scaling Group

    Create Auto Scale Group:        aws-php-autoscale
    Group Size (Starts with):        1
    Network:                               cmpe281 (VPC) | Public Subnet
    
    Use scaling policies to adjust the capacity of this group

    Scale between:                    1 - 3 instances
    Increase when:                    AVG CPU >= 40% (for at lease 1 minute)
    Decrease when:                   AVG CPU <= 15% (for at lease 1 minute)
    
PART 2 - CREATE CLASSIC LOAD BALANCER

    
# Tutorial: Set Up a Scaled and Load-Balanced Application

    DOC:  http://docs.aws.amazon.com/autoscaling/latest/userguide/as-register-lbs-with-asg.html
    
## Create or Select a Launch Configuration

    Select My AMI:                     aws-php-ami
    Instance Type:                     T2-Micro (Free Tier)
    Launch Configuration Name:        aws-php-autoscale
    Enable Monitoring:                Enable CloudWatch detailed monitoring
    Select Public IP:                Assign a public IP address to every instance.
    Security Group:                     cmpe281-dmz (SG)
    Select Key Pair:                    cmpe281-us-west-1
    Select VPC:                        cmpe281 (VPC) & Public Subnet
    

## Create an Auto Scaling Group

    Create Auto Scale Group:        aws-php-autoscale
    Group Size (Starts with):        1
    Network:                            cmpe281 (VPC) | Public Subnet
    
    Use scaling policies to adjust the capacity of this group

    Scale between:                    1 - 3 instances
    Increase when:                    AVG CPU >= 40% (for at lease 1 minute)
    Decrease when:                    AVG CPU <= 15% (for at lease 1 minute)


## Using a Load Balancer With an Auto Scaling Group    
    DOC: http://docs.aws.amazon.com/autoscaling/latest/userguide/autoscaling-load-balancer.html
    
    
## Create ELB (Classic Load Balancer)

        Name:         aws-php-elb-classic 
        VPC:         cmpe281 (select public subnet)
        SG:            cmpe281-dmz
        Port:         80
        Health Check: Default path, Unhealthy Checks: 2, Healthy Checks: 4
        Add Instances: Select running instance (from aws-php-autoscale)        
        Edit Auto Scale Group:    aws-php-autoscale
        Select ELB: aws-php-elb-classic
    
    
## Expanding Your Scaled and Load-Balanced Application to an Additional Availability Zone

    DOC:  http://docs.aws.amazon.com/autoscaling/latest/userguide/as-add-availability-zone.html#as-add-az-console
    
    Select Auto Scale Group:        aws-php-autoscale
    Select Edit / Details / AZs:    Select two Public Subnets (in us-west-1a and us-west-1b)
    Set the Desired and Min to:    two instances    
   
