### 02-s3-setup-simple-webapp
##### GIVEN:
  - An AWS Cloud9 desktop from 00-setup-cloud9

##### WHEN:

  - I create a Bucket
  - Apply an IAM Bucket Policy to it
  - Add some html objects to it
  - Enable Static Web Hosting on it

##### THEN:
  - I will be able to access my car website

##### SO THAT:
  - I can learn how to build a static webapp on AWS

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
cd ~/environment/mglab-share-archit-accel/demos/02-s3-setup-simple-webapp/
export C9_REGION=$(curl --silent http://169.254.169.254/latest/dynamic/instance-identity/document |  grep region | awk -F '"' '{print$4}')
export C9_AWS_ACCT=$(curl -s http://169.254.169.254/latest/dynamic/instance-identity/document | grep accountId | awk -F '"' '{print$4}')
clear
echo "C9_REGION=$C9_REGION"
echo "C9_AWS_ACCT=$C9_AWS_ACCT"
```

##### 1: Create Bucket
- Generate a random name for the bucket you will create.  S3 buckets are 'global' and therefore must have a unique name across all of AWS (Public DNS Path requirement).
```
BUCKET_NAME=s3-simple-webapp-$(cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 16 | head -n 1 | tr '[:upper:]' '[:lower:]')
echo $BUCKET_NAME
```
- Now lets create the bucket.
```
aws s3 mb s3://$BUCKET_NAME --region $C9_REGION
aws s3api put-bucket-tagging --bucket $BUCKET_NAME --tagging 'TagSet=[{Key=CLASS,Value=ARCHIT-ACCEL},{Key=DEMO,Value=02-s3-multi-part-upload}]'
```
- Now lets list it to confirm it was created ... it should be empty.
```
aws s3 ls | grep $BUCKET_NAME
```

##### 2: Create a Bucket Policy to allow public access to the website
- Review the bucket policy.
```
cat artifacts/bucket-policy.json
```

- Lets edit it so it includes the same of the bucket you just created instead of the variable marker.
```
sed  -i "s/<BUCKET_NAME>/$BUCKET_NAME/g" ./artifacts/bucket-policy.json
```

- Review it one more time to ensure the variable marker has changed.
```
cat artifacts/bucket-policy.json
```

- Add the policy you just edited and verify it.
```
aws s3api put-bucket-policy --bucket $BUCKET_NAME --policy file://./artifacts/bucket-policy.json
aws s3api get-bucket-policy --bucket $BUCKET_NAME
```

##### 3: Add static html content to the bucket
- Copy a demo car website to the cloud9 Desktop
```
mkdir mywebsite && cd mywebsite && wget -c https://mglab-aws-samples.s3.amazonaws.com/classes/archit/02/archit-s3-car-site-v1.tgz -O - | tar -xz && cd ..
aws s3 sync ./mywebsite s3://$BUCKET_NAME
aws s3 ls s3://$BUCKET_NAME
```

##### 4: Enable static website hosting on the bucket and see if our website is up :)
- Turn on website hosting ... grab your url and enjoy :)
```
aws s3api put-bucket-website --bucket $BUCKET_NAME --website-configuration '{"IndexDocument": {"Suffix": "index.html"}}'
echo "http://$BUCKET_NAME.s3-website-$C9_REGION.amazonaws.com"
```

---------------------------------------------------------------
---------------------------------------------------------------
#### CLEANUP
Only run these scripts if you are done cleaning &/or running all dependent demos.

_You will need to delete versioned objects via the Console if you ran the mpu & video upload demo ... until lazy Merlin adds a delete script for versioned objects in the bucket here._

```
aws s3 rb s3://$BUCKET_NAME --force
```
