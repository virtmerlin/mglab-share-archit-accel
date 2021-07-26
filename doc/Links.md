## Doc Links

#### [Return to Main Readme](https://github.com/virtmerlin/mglab-share-archit-accel#links)

#### (1) Introduction to Cloud:

  - [AWS Global Infra](https://aws.amazon.com/about-aws/global-infrastructure/?p=ngi&loc=1)
  - [Timeline of AWS Services](https://en.wikipedia.org/wiki/Timeline_of_Amazon_Web_Services)
  - [Global Submarine Cable Map](https://www.submarinecablemap.com/)

#### (2) The Simplest Architectures (S3):

  - [Common S3 Bucket Policy Examples](https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-bucket-policies.html)
  - [S3 Accelerator Simulator](https://s3-accelerate-speedtest.s3-accelerate.amazonaws.com/en/accelerate-speed-comparsion.html)
  - [Glacier Step by Step via CLI](https://softwaredevelopmentstuff.com/2017/05/02/downloading-an-aws-glacier-archive-step-by-step/)

#### (3) Adding a Compute Layer (EC2/EBS/EFS):

  - [Marketplace AMIs](https://aws.amazon.com/marketplace)
  - [EC2 Instance Types](https://aws.amazon.com/ec2/instance-types/)
  - [EC2 'EBS Optimized' Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-optimized.html)
  - [EC2 Instance Types w/ Instance Stores](https://aws.amazon.com/ec2/spot/instance-advisor/)
  - [EBS Volume Types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html)
  - [EFS Workshop Repo](https://github.com/aws-samples/amazon-efs-workshop)
  - [FSX Workshop Repo](https://github.com/aws-samples/amazon-fsx-workshop)
  - [Spot Advisor](https://aws.amazon.com/ec2/spot/instance-advisor/)

#### (4) Adding a Database Layer (RDS/Dynamo/Neptune):

  - [RDS Quotas & Constraints](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_Limits.html)
  - [RDS Aurora: Clusters](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.html)
  - [RDS Aurora: Replication](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Replication.html)
  - [RDS Aurora: Global Databases](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-global-database.html)
  - [DynamoDB Workshop](https://amazon-dynamodb-labs.com/)
  - [Neptune Workshop](https://neptune-deep-dive.workshop.aws/en/)

#### (5,6,19) VPC Networking:

  - [Cidr Tool](https://cidr.xyz/)
  - [Direct Connect Locations](https://aws.amazon.com/directconnect/features/#AWS_Direct_Connect_Locations)
  - [VPC Endpoint Workshop](https://www.vpcendpointworkshop.com/)
  - [TGW & Network Firewall Workshop](https://networkfirewall.workshop.aws/intro.html)

#### (7) IAM:

  - [IAM Integrated AWS Resource List](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html)
  - [IAM Policy Simulator](https://policysim.aws.amazon.com/home/index.jsp?#)
  - [IAM Policy Condition Examples](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_condition_operators.html)
  - [IAM Quotas & Constraints](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_iam-quotas.html)

#### (8) Organizations:

  - [AWS Orgs Tutorial](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_tutorials_basic.html)
  - [AWS Control Tower Workshops](https://controltower.aws-management.tools/)
  - [Example Service Control Policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps_examples.html)

#### (9) Elasticity, HA, & Monitoring:

  - [DynamoDB Partitions](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.Partitions.html)
  - [DynamoDB Partitions Deep Dive _3rd party_](https://shinesolutions.com/2016/06/27/a-deep-dive-into-dynamodb-partitions/)
  - [AWS Observability Workshop](https://observability.workshop.aws/en/)
  - [EC2 Autoscaling & Spot Workshop](https://ec2spotworkshops.com/running-amazon-ec2-workloads-at-scale.html)

#### (10) Automation (Infra):

  - [Cloud Formation (CFN) Quickstarts](https://aws.amazon.com/quickstart/?quickstart-all.sort-by=item.additionalFields.sortDate&quickstart-all.sort-order=desc)
  - [CFN Github Examples](https://github.com/awslabs/aws-cloudformation-templates)
  - [CFN Resource & Property Refs](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html)
  - [CFN-HUP](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html)
  - [Ogres r Like Onions ... I mean OpsWorks layer](https://docs.aws.amazon.com/opsworks/latest/userguide/workinglayers.html)
  - [Elastic Beanstalk Workshop](https://aws-elastic-beanstalk-webapp.workshop.aws/en/)
  - [AWS CDK Workshop](https://cdkworkshop.com/)

#### (11) Deploying Methods (CI/CD , Change-Mgmt):

  - [AWS T&C System Operations on AWS ILT](https://www.aws.training/SessionSearch?pageNumber=1&courseId=10020&languageId=1)
  - [AWS T&C DevOps Engineering on AWS ILT](https://www.aws.training/SessionSearch?pageNumber=1&courseId=10018&languageId=1)
  - [SSM Workshop](https://workshop.aws-management.tools/ssm/)
  - AWS Devops Workshops:
    - https://docker.awsworkshop.io/
    - https://ghg.awsworkshop.io/

#### (12) Caching:

  - [Elasticache Tutorials & Videos](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/Tutorials.html)
  - [Common Caching Strategies](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/Strategies.html)

#### (13) Data Security (KMS):

  - [AWS KMS Workshop Repo](https://github.com/aws-samples/aws-kms-workshop)
  - [AWS Security Workshops](https://awssecworkshops.com/)

#### (14) Decoupled Architectures (SQS/SNS/EventBridge):

  - [AWS Async Messaging Workshop](https://github.com/aws-samples/asynchronous-messaging-workshop)
  - [Building Event Driven Architecture Workshop](https://event-driven-architecture.workshop.aws/)

#### (16) MicroServices (EKS/ECS/FARGATE):

  - [Should that be a MicroService?](https://tanzu.vmware.com/content/blog/should-that-be-a-microservice-keep-these-six-factors-in-mind)
  - [Breaking the Monolith](https://martinfowler.com/articles/break-monolith-into-microservices.html)
  - [EKS vs. ECS](https://aws.amazon.com/blogs/containers/amazon-ecs-vs-amazon-eks-making-sense-of-aws-container-services/)
  - [EKS Workshops](https://eksworkshop.com/)
  - [ECS Workshops](https://ecsworkshop.com/)

#### (17) Serverless (Lambda/Step Functions/API Gateway):

  - [Lambda Quotas](https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-limits.html)
  - [Lambda Runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html)
  - [Predictable Lambda Start Times](https://docs.aws.amazon.com/step-functions/latest/dg/connect-supported-services.html)
  - [Step Function Integrated Services](https://docs.aws.amazon.com/step-functions/latest/dg/connect-supported-services.html)
  - [AWS Serverless Workshops](https://aws.amazon.com/serverless-workshops/)
    - https://github.com/aws-samples/aws-serverless-workshop-innovator-island
    - https://github.com/aws-samples/aws-serverless-webapp-workshop

#### (18) Resilience (CloudMap/WAF/FIS):

  - [Appmesh + CloudMap Workshop](https://www.appmeshworkshop.com/introduction/)
  - [AWS WAF Workshop](https://introduction-to-waf.workshop.aws/00-introduction.html)
  - [AWS Fault Injector Service](https://aws.amazon.com/fis/)

#### (20) Understanding Costs:

  - [Setup CUR](https://docs.aws.amazon.com/cur/latest/userguide/cur-create.html)
  - [Query CUR with Athena](https://docs.aws.amazon.com/cur/latest/userguide/use-athena-cf.html)
  - [Video: Compare Savings Plan to Reservations](https://www.youtube.com/watch?v=xjq-1CdvgQ8)
  - [Cost Workshop 101](https://activate-next.workshop.aws/001_intro.html)

#### (21) Migration Strategies:

  - [Migration Hub](https://aws.amazon.com/migration-hub/)
  - [DMS & SCT Workshop](https://dms-immersionday.workshop.aws/en/)
  - [AWS Snow Family](https://aws.amazon.com/snow/)
  - [Application Migration Service (CloudEndure 2) Workshop](https://application-migration-with-aws.workshop.aws/en/server-migration.html)

#### (22) RPO/RTO:

  - [AWS DR Workshop](https://disaster-recovery.workshop.aws/en/)
