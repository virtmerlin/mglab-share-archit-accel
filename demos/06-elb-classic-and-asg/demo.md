### 06-elb-classic-and-asg
##### GIVEN:
  - An AWS Cloud9 desktop from 01-setup-cloud9
  - An application to deploy (TV Character Hello App (java))

##### WHEN:

  - I create an IAM role to attach to each instance
  - I create multiple Security Groups
  - I create an ELB with a Public DNS name & URL
  - I create an EC2 LaunchConfig to define my instances
  - I create an EC2 Autoscaling Group using the LaunchConfig

##### THEN:
  - I will be able to access my TV Character Hello App via a LB
  - My LB will be in a public subnet
  - My EC2 Instances will be in a private subnet

##### SO THAT:
  - I can generate load with jmeter/blazemeter
  - I can see my ASG scale in and out based on load
  - I can attach Route 53 names & Signed SSL Certs to my ELB

##### NOTE: _This demo will provide CLI steps, but may have been demonstrated via the UI during a class delivery_

##### [Return to Main Readme](https://github.com/virtmerlin/mglab-share-archit-accel#demos)

---------------------------------------------------------------
---------------------------------------------------------------
#### REQUIRES
- 00-setup-cloud9

---------------------------------------------------------------
---------------------------------------------------------------
#### DEMO

##### 0: Reset C9 Instance env variables
- Reset your region & aws account variables in case you launched a new terminal session
```
cd ~/environment/mglab-share-archit-accel/demos/06-elb-classic-and-asg/
export C9_REGION=$(curl --silent http://169.254.169.254/latest/dynamic/instance-identity/document |  grep region | awk -F '"' '{print$4}')
export C9_AWS_ACCT=$(curl -s http://169.254.169.254/latest/dynamic/instance-identity/document | grep accountId | awk -F '"' '{print$4}')
clear
echo "C9_REGION=$C9_REGION"
echo "C9_AWS_ACCT=$C9_AWS_ACCT"
```
##### 1: Create CloudFormation 'Stack' that will create an IAM Role for each EC2 Instance, an ASG to launch instances, and a security group to allow inbound traffic.
- Create 'Stack'
```
aws cloudformation deploy --region $C9_REGION --template-file ./artifacts/elb-classic-asg-cfn-cw-agent.yaml \
    --stack-name archit-accel-demos-06-elb-classic-and-asg --tags CLASS=ARCHIT --capabilities CAPABILITY_NAMED_IAM
```

##### 2: Test the TV Character 'Hello' App
- Get Load Balancer URL url from the Stack
```
aws cloudformation --region $C9_REGION \
    describe-stacks \
    --stack-name archit-accel-demos-06-elb-classic-and-asg \
    --query "Stacks[].Outputs[?OutputKey=='URL'].[OutputValue]" \
    --output text
```
- Get a hello from the webapp

##### 3: Setup R53 & ACM Certificates
- Optional Challenge:
  - [DOC-LINK: ACM](https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-public.html)
  - [DOC-LINK: R53](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-creating.html)
  - Create an ACM Certificate with appropriate SAN via Console
  - Create Route53 CNAME entry using from your SAN to the Load Balancer URL

##### 4: Run scaling tests
- Optional Challenge:
  - Use a service (like Jmeter/Blazemeter) to generate load and see ASG the autoscale

---------------------------------------------------------------
---------------------------------------------------------------
#### CLEANUP
Only run these scripts if you are done cleaning &/or running all dependent demos.
```
aws cloudformation delete-stack --region $C9_REGION  --stack-name archit-accel-demos-06-elb-classic-and-asg
```
