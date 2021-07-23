### 12-cache-inventory-app
##### GIVEN:
  - An AWS Cloud9 desktop from 00-setup-cloud9
  - An a sample PHP Inventory App using Memcached
  - The Mysql DB from the 04-rds-mysql-access Demo

##### WHEN:

  - I create a CFN stack with V1.1 Inventory App

##### THEN:
  - I will be get the Inventory App
  - I will also get an ASG + a Memcached Cluster

##### SO THAT:
  - I can see the impact & complexity of Caches in front of a RDBMS

##### NOTE: _This demo will provide CLI steps, but may have been demonstrated via the UI during a class delivery_

##### [Return to Main Readme](https://github.com/virtmerlin/mglab-share-archit-accel#demos)

---------------------------------------------------------------
---------------------------------------------------------------
#### REQUIRES
- 00-setup-cloud9
- 04-rds-mysql-access

---------------------------------------------------------------
---------------------------------------------------------------
#### DEMO

##### 0: Reset C9 Instance env variables
- Reset your region & aws account variables in case you launched a new terminal session
```
cd ~/environment/mglab-share-archit-accel/demos/12-cache-inventory-app/
export C9_REGION=$(curl --silent http://169.254.169.254/latest/dynamic/instance-identity/document |  grep region | awk -F '"' '{print$4}')
export C9_AWS_ACCT=$(curl -s http://169.254.169.254/latest/dynamic/instance-identity/document | grep accountId | awk -F '"' '{print$4}')
clear
echo "C9_REGION=$C9_REGION"
echo "C9_AWS_ACCT=$C9_AWS_ACCT"
```

##### 1: Create CloudFormation 'Stack' that will all reqd resources for V1.1 Inventory App with Memcached support.
- Create 'Stack'
```
aws cloudformation deploy --region $C9_REGION --template-file ./artifacts/inventory-memcached.yaml \
    --stack-name archit-accel-demos-12-cache-inventory-app --tags CLASS=ARCHIT-ACCEL --capabilities CAPABILITY_NAMED_IAM
```

##### 1: Test the faulty cache mechanism behaviour with the application.  What happens when you delete an Item and immediately refresh inventory?
- Get the url from the Stack to test it in a web browser:
```
aws cloudformation --region $C9_REGION \
    describe-stacks \
    --stack-name archit-accel-demos-12-cache-inventory-app \
    --query "Stacks[].Outputs[?OutputKey=='AppInstancePublicDNS'].[OutputValue]" \
    --output text
```
- Initially the inventory page will present an error message stating that the table is not present. Goto the 'settings' link & click save to populate test data, do not change any of the settings.
- Test inventory update & delete scenarios and look at _./artifacts/inventory-app-memcache/show-data.php_ to see the logic flaw in this read ahead cache scenario
  - [Code Link](https://github.com/virtmerlin/mglab-share-archit/blob/main/demos/10-cache-inventory-app/artifacts/inventory-app-memcache/show-data.php#L48-#L71)

---------------------------------------------------------------
---------------------------------------------------------------
#### CLEANUP
Only run these scripts if you are done cleaning &/or running all dependent demos.
```
aws cloudformation --region $C9_REGION delete-stack --stack-name archit-accel-demos-12-cache-inventory-app
```
