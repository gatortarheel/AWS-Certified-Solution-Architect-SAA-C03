# AWS-Certified-Solution-Architect-SAA-C03
[AWS Certified Solutions Architect Study Guide with 900 Practice Test Questions: Associate (SAA-C03) Exam 4th Edition](https://www.amazon.com/Certified-Solutions-Architect-Practice-Questions-dp-1119982626/dp/1119982626/ref=dp_ob_title_bk)
> Release date: 10/4/2022


`Notes are from Third Edition`

---

### Chapter 1
#### Cloud Computing and Virtualization

![image](https://user-images.githubusercontent.com/11463852/185354155-9948885a-11a5-481c-93dc-894043d6e72e.png)

Virtualization's flexibility makes it easy to provision whatever is needed quickly and efficiently.

##### Scalability
> Add and remove virtual machines as demand fluctuates.

##### Elasticity
> Only run the required resources.

##### Cost management
> Keep costs down.
- Transition IT spending from capital expenditure to operation expenditure.
- Total Cost of Operation calculator is provided by AWS to assist with estimating expenses.

### AWS Service Categories

| Category | Function |
| ----------- | ----------- |
| Compute | Traditional role of local physical servers |
| Networking | Application connections, access control, enhanced remote connections |
| Storage | Store stuff |
| Databases | Store data - relational, NoSQL, caching |
| Application Management | Monitoring, auditing, configuring AWS account information |
| Security and Identity | Authentication, authorization, data encryption, third party integrations

---

### Core AWS Services
| Category | Service | Function |
| ----------- | ----------- |---------- |
| Compute | Elastic Compute Cloud | Virtual machines deployed *nearly instantly* |
|  | Lambda | Handles workloads less than 15 minutes, and all resources when not running are shut down |
|  | Auto Scaling | EC2 instances can be defined as image templates and launched as needed |
| | Elastic Load Balancing | Network traffic can be directed as needed |
| | Elastic Beanstalk | Does the compute and networking for you |
| Networking | VPC Virtual Private Cloud | *Highly* configurable networking environments designed to host your EC2 and RDS instances.  Allows control of all network traffic.
| | Direct Connect | AWS enhanced direct tunnel from AWS to your local data center |
| | Route 53 | Manages domain registration, routing protocols, health checks
| | CloudFront | AWS' Content Delivery Network - CDN - stores cached versions of content closer to customers |
| Storage | Simple Storage Service S3 | Store stuff here |
| | S3 Glacier | Large data archives stored cheaply but requires hours for data retrieval |
| | Elastic Block Store EBS | Virtual storage drives for EC2 instances |
| | Storage Gateway | Hybrid system that exposes cloud storage as local on-premise appliance - good for migration, data backup, disaster recovery |
| Database | RDS | Stable, reliable, secure database instance
| | DyanamoDB | Fast, flexible, highly scalable and managed NoSQL database workloads |
| Application Management | CloudWatch | Monitor process performance, resource utilization, can trigger messages or automated responses |
| | CloudFormation | Templates for AWS deployments |
| | CloudTrail | Collects records for all API events - helpful for troubleshooting and auditing |
| | Config | Maintains compliance.  Define a desired configuration state, and Config evaluates any future states against that ideal.  Notifications occur when a configuration change goes outside the ideal baseline.
| Security and Identity | IAM | Users, groups, roles, policies |
| | KMS | Creation and use of encryption keys to secure data |
| | Directory Service | Integrates with Cognito and Microsoft AD Domains |
| Application Integration | SNS | Automates the publishing of alert topics to other services - SQS, trigger Lambda function, SMS, email |
| | Simple Workflow SWF | Performs a series of tasks |
| | SQS | Event driven messaging queue- reliably delivered |
| | API Gateway | Create, manage, secure reliable APIs for AWS based applications |
----
## AWS Regional Services
[Edge Services](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)

![image](https://user-images.githubusercontent.com/11463852/185369123-860ff1f8-ac71-4e05-b6ff-4e44e432e76c.png)

---
### AWS Reliablity and Compliance
- ISO 9000
- FedRAMP
- NIST
- GDPR
- Staples!
[AWS Compliance](https://aws.amazon.com/compliance/programs/)



