# Shared Demo Scripts
## Accelerated Architecting on AWS

<img src="doc/images/ec2.png" width="100" height="100" /> <img src="doc/images/s3.jpeg" width="100" height="100" /> <img src="doc/images/vpc.png" width="120" height="100" />

### What is this?

This repository provides an export of various AWS demonstrations an instructor may leverage to deliver an accelerated course about architecting on the AWS cloud.

The demos in this repository are provide as is with **NO WARRANTIES** explicit or implied.  It is the consumers responsibility for costs & management of ANY & ALL provisioned resources in the consumers own AWS account(s) when using these demos.

### Whats in it?

The idea is that a student will create an AWS VPC & Cloud9 instance into their own AWS account, via the AWS Cloudformation templates in this repository.  They will then clone this repository into that Cloud9 instance to run each of the demos that may have been seen in a class delivery.

After cloning this repository within the Cloud9 instance, a student can simply `cd` into the relevant demo directory and follow the instructions in the 'demo.txt' or 'demo.md' file.

Here is the folder structure for each demo:

```
     demos /
           /##-some-demo-description/
                        demo.txt|md
                       /pre-reqs
                       /artifacts
                       /tests
```

- The Idea is that for each demo there will be a _demo folder_.
- The folder will be named `##-some-demo-description`
  - with the `##` being ~ to the module in the course to give you an idea where it fits in a story
  - and the `some-demo-description` being a short description of the actual demo within
- Within each _demo folder_ there will be:
  - _**a demo.txt or demo.md file**_: A simple file that you should be able to follow to repeat/perform a demo.  This is where you will start each demo.
  - _**a pre-reqs folder**_:  (optional) will contain any cfn & scripts that you may need to setup the demo environment for that demo.
  - _**an artifacts folder**_: (optional) will contain any yaml / json/ bins that you may use in running the demo(s).           
  - _**a tests folder**_: (optional) will contain some tests for the automation that will validate a demo is working on a regular schedule and post test results to the README.md.

#### Links

[ARCHIT-ACCEL Agenda]
- [Day1](doc/images/day1.png)
- [Day2](doc/images/day2.png)
- [Day3](doc/images/day3.png)
- [Day4](doc/images/day4.png)
- [Day5](doc/images/day5.png)

[ARCHIT-ACCEL Helpful Links](doc/Links.md)


#### Demos
Demo Name     | Demo Link     | Last Automated Test Timestamp
--- | ---| ---
00-setup-cloud9     | [link](demos/00-setup-cloud9/demo.md)   | Not Yet Automated
02-s3-setup-simple-webapp     | [link](demos/02-s3-setup-simple-webapp/demo.md)   | Not Yet Automated
03-ec2-userdata     | [link](demos/03-ec2-userdata/demo.md)   | Not Yet Automated
04-rds-mysql-access     | [link](demos/04-rds-mysql-access/demo.md)   | Not Yet Automated
06-elb-classic-and-asg     | [link](demos/06-elb-classic-and-asg/demo.md)   | Not Yet Automated
10-cloudformation-and-cfnhup     | [link](demos/10-cloudformation-and-cfnhup/demo.md)   | Not Yet Automated
11-cicd-tvapp-ecs     | [link](demos/11-cicd-tvapp-ecs/demo.md)   | Not Yet Automated
12-cache-inventory-app     | [link](demos/12-cache-inventory-app/demo.md)   | Not Yet Automated
13-data-encryption-primer  | [link](demos/13-data-encryption-primer/demo.md)   | Not Yet Automated
14-decouple-sqs-sns-eventbridge | [link](demos/14-decouple-sqs-sns-eventbridge/demo.md)   | Not Yet Automated
