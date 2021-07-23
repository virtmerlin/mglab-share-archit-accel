## 11-cicd-tvapp-ecs

#### GIVEN:
  - An AWS Cloud9 desktop from 00-setup-cloud9
  - An application to deploy (TV Character Hello App (java))

#### WHEN:
  - I create a stack from my cloudformation template

#### THEN:
  - I will get an ECS Cluster
  - I will get an ECR Repo
  - I will get IAM roles for CodePipeline & CodeBuild
  - I will get an AWS CodeCommit repo with my java tv app src in it
  - I will get an AWS CodePipeline pipeline with 3 stages (Source, Build, Deploy)
  - I will get an AWS CodePipeline stage 1 that triggers off of a commit to my AWS CodeCommit repo
  - I will get an AWS CodePipeline stage 2 that uses an AWS CodeBuild action provider to build and push my OCI image to ECR
  - I will get an AWS CodePipeline stage 3 that uses an ECS action provider to rolling update my app to ECS / Fargate

#### SO THAT:
  - I can CICD my java tv app

##### [Return to Main Readme](https://github.com/virtmerlin/mglab-share-archit-accel#demos)

---------------------------------------------------------------
---------------------------------------------------------------
### REQUIRES
- 00-setup-cloud9

---------------------------------------------------------------
---------------------------------------------------------------
### DEMO

##### 0: Reset C9 Instance env variables
- Reset your region & aws account variables in case you launched a new terminal session
```
cd ~/environment/mglab-share-archit-accel/demos/11-cicd-tvapp-ecs/
export C9_REGION=$(curl --silent http://169.254.169.254/latest/dynamic/instance-identity/document |  grep region | awk -F '"' '{print$4}')
export C9_AWS_ACCT=$(curl -s http://169.254.169.254/latest/dynamic/instance-identity/document | grep accountId | awk -F '"' '{print$4}')
clear
echo "C9_REGION=$C9_REGION"
echo "C9_AWS_ACCT=$C9_AWS_ACCT"
```

#### 1: Deploy CodeCommit, ECR, & Code Pipeline/Build projects via Cloud Formation templates.

- Deploy CloudFormation to create pipeline environment:
```
aws cloudformation deploy --region $C9_REGION --template-file ./artifacts/11-cicd-tvapp-ecs-codepipeline-build.cfn \
    --capabilities CAPABILITY_IAM \
    --stack-name archit-accel-demos-11-cicd-tvapp-ecs \
    --tags CLASS=ARCHIT_ACCEL
```

#### 2: Push the src of the Java tvApp to CodeCommit & trigger Code Pipeline.
- Setup the git credential helper to authN to CodeCommit:
```
git config --global credential.helper '!aws codecommit credential-helper $@'
git config --global credential.UseHttpPath true
```
- Get the CodeCommit Repository CloneURL:
```
export CCREPOURL=$(aws cloudformation --region $C9_REGION \
    describe-stacks \
    --stack-name archit-accel-demos-11-cicd-tvapp-ecs \
    --query "Stacks[].Outputs[?OutputKey=='CCRepository'].[OutputValue]" \
    --output text)
echo $CCREPOURL
```
- Clone the empty repo into your cloud9 Desktop:
```
git clone $CCREPOURL
```
- Copy the sample app src code into the repo:
```
cd archit-accel-demos-11-cicd-tvapp-ecs*
wget -c https://mglab-aws-samples.s3.amazonaws.com/classes/archit-accel/11/src/archit-hello-monolith-src.tgz -O - | tar -xz
```
- Commit & 'Init' Push to the CodeCommit repo with the sample python application/Dockerfile:
```
git add -A
git commit -am "init"
git branch -M main
git push origin main
```
-  Open CodePipeline in the Console [link](https://console.aws.amazon.com/codesuite/codepipeline/pipelines), confirm the pipeline runs successfully.

#### 3: Verify the Java tvApp is running and LoadBalancer service is running.  Then 'devops' some changes.
- Get the Load balancer URL and test it in a Browser:
```
export ECSSVCURL=$(aws cloudformation --region $C9_REGION \
    describe-stacks \
    --stack-name archit-accel-demos-11-cicd-tvapp-ecs \
    --query "Stacks[].Outputs[?OutputKey=='ServiceUrl'].[OutputValue]" \
    --output text)
echo $ECSSVCURL
```
- Now lets change the Background from blue to green ... edit the thyme template & push the changes to CodeCommit:
```
sed -i "s/aliceblue/green/g" ./src/main/resources/static/styles/hello/main.css
git commit -am "green Background"
git push origin main
```
-  Open CodePipeline in the Console [link](https://console.aws.amazon.com/codesuite/codepipeline/pipelines), confirm the pipeline runs successfully, then test for new background color (make sure your browser isn't caching if u don't see the change).

---------------------------------------------------------------
---------------------------------------------------------------
### DEPENDENTS

---------------------------------------------------------------
---------------------------------------------------------------
### CLEANUP
- Do not cleanup if you plan to run any dependent demos
```
aws cloudformation delete-stack --region $C9_REGION  --stack-name archit-accel-demos-11-cicd-tvapp-ecs
```
