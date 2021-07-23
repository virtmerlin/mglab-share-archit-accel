### 14-decouple-sqs-sns-eventbridge

##### GIVEN:
  - An AWS Cloud9 desktop from 00-setup-cloud9
  - A Cloudformation template

##### WHEN:

  - I create a stack from the Cloudformation template

##### THEN:
  - I will get a SQS Queue
  - I will get a SNS Topic
        + I will add an _email_ Subscription to my email inbox via the Console
        + I will add a _SQS_ Subscription to my SQS Queue via the Console
  - I will get an EVENTBRIDGE rule to publish a message to the SNS topic whenever an ec2 instance state changes

##### SO THAT:

  - I can shutdown an ec2 instance
  - I will get a notification in my email box from my SNS Topic
  - I will get a message in my SQS Queue from my SNS Topic that I could have an Application polling to take action upon

  - I can see the basic functions of decoupled/event driven architectures
    - SQS Queues messages are _poll_ ed by consumers
    - SNS Topics published messages are _push_ ed to subscribers

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
cd ~/environment/mglab-share-archit-accel/demos/14-decouple-sqs-sns-eventbridge/
export C9_REGION=$(curl --silent http://169.254.169.254/latest/dynamic/instance-identity/document |  grep region | awk -F '"' '{print$4}')
export C9_AWS_ACCT=$(curl -s http://169.254.169.254/latest/dynamic/instance-identity/document | grep accountId | awk -F '"' '{print$4}')
clear
echo "C9_REGION=$C9_REGION"
echo "C9_AWS_ACCT=$C9_AWS_ACCT"
```

##### 1: Create a SQS Standard Queue & SNS Topic & EventBridgeRule
- Create 'Stack' that will create the SQS standard Queue + the SNS Topic:
```
aws cloudformation deploy --region $C9_REGION --template-file ./artifacts/decoupled-sqs-sns.yaml \
    --stack-name archit-accel-demos-14-decouple-sqs-sns-eventbridge --tags CLASS=ARCHIT-ACCEL --capabilities CAPABILITY_NAMED_IAM
```

##### 2: Create an email subscription on the SNS Topic
- Use the [AWS SNS Console](https://console.aws.amazon.com/sns) [verify your region] to create an email subscription to the archit-accel-demos-14-decouple-sqs-sns-eventbridge-SNS Topic.  *!!!You will need to look in your inbox to confirm!!!*
  - Protocol: Email
  - Endpoint: [YOUR EMAIL ADDR]

##### 3: Create a SQS subscription on the SNS Topic
- Use the [AWS SNS Console](https://console.aws.amazon.com/sns) [verify your region] to create asqs subscription to the archit-accel-demos-14-decouple-sqs-sns-eventbridge-SNS Topic.
  - Protocol: Amazon SQS
  - Endpoint: archit-accel-demos-14-decouple-sqs-sns-eventbridge-SQS

##### 4: Review the EventBridge rule to trigger a SNS publish off of instance termination & start it.
- Use the [AWS Eventbridge Console](https://console.aws.amazon.com/events) [verify your region] to review the rule: archit-accel-demos-14-decouple-sqs-sns-eventbridge-RULE
- Terminate a test ec2 instance and check for notifications:
  - Check your email
  - Check the SQS Queue [AWS SQS Console](https://console.aws.amazon.com/sqs) [verify your region]

---------------------------------------------------------------
---------------------------------------------------------------
#### CLEANUP
Only run these scripts if you are done cleaning &/or running all dependent demos.
```
aws cloudformation --region $C9_REGION delete-stack --stack-name archit-accel-demos-14-decouple-sqs-sns-eventbridge
```
