### 03-ec2-userdata
##### GIVEN:
  - An AWS Cloud9 desktop from 00-setup-cloud9
  - An application to deploy TV Character Hello app (java)

##### WHEN:

  - I create an IAM role to attach to an IAM instance via CloudFormation
  - I create an EC2 Instance with a public IP via CloudFormation
  - I add UserData Profile to the instance via CloudFormation

##### THEN:
  - I will be able to access my TV Character Hello app

##### SO THAT:
  - I can learn how to use run once bootstrapping on EC2

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
- Reset your region & AWS account variables in case you launched a new terminal session
```
cd ~/environment/mglab-share-archit-accel/demos/03-ec2-userdata/
export C9_REGION=$(curl --silent http://169.254.169.254/latest/dynamic/instance-identity/document |  grep region | awk -F '"' '{print$4}')
export C9_AWS_ACCT=$(curl -s http://169.254.169.254/latest/dynamic/instance-identity/document | grep accountId | awk -F '"' '{print$4}')
clear
echo "C9_REGION=$C9_REGION"
echo "C9_AWS_ACCT=$C9_AWS_ACCT"
```

##### 1: Create CloudFormation 'Stack' that will create an IAM Role for the EC2 Instance, an Instance, and a security group to allow inbound traffic.
- Create 'Stack'
```
aws cloudformation deploy --region $C9_REGION --template-file ./artifacts/ec2-userdata-demo-cfn.yaml \
    --stack-name archit-accel-demos-03-ec2-userdata --tags CLASS=ARCHIT-ACCEL --capabilities CAPABILITY_NAMED_IAM
```
- In the EC2 console: review the New Instance UserData
  - [AWS EC2 Console](https://console.aws.amazon.com/ec2/v2/home) ... (you may need to select your region)

##### 2: Test the TV Character 'Hello' App
- Get the url from the Stack
```
aws cloudformation --region $C9_REGION \
    describe-stacks \
    --stack-name archit-accel-demos-03-ec2-userdata \
    --query "Stacks[].Outputs[?OutputKey=='URL'].[OutputValue]" \
    --output text
```
- Get a 'Unique' hello from the webapp by clicking on thew link in the Cloud9 IDE

---------------------------------------------------------------
---------------------------------------------------------------
#### CLEANUP
Only run these scripts if you are done cleaning &/or running all dependent demos.
```
aws cloudformation delete-stack --region $C9_REGION  --stack-name archit-accel-demos-03-ec2-userdata
```
