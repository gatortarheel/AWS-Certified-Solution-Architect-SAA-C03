# EC2 Instances

## AMI

### Amazon Machine Image

- Quick Start AMIs - popular, up to date, officially supported
- AWS Marketplace AMIs - official production ready images, supported by industry vendors
- Community AMIs - good catalog to search for a custom combination
- Private AMIs - created by you

*A particular AMI will be available in a single region - but frequently images with identical functionality are in all regions.*

## Instance Types

|Family|Types|Notes|
|----------|----------|-------------------|
|General purpose | A1, T3, T2, M6g, M5, M5a, M5n, M4 | t2.micros is a good choice for experimenting; T2s are burstable, you can accumulate CPU credits when your instance is underutilized, and then apply those credits during high demand time in the form of CPU performance

- M5 and M4 instances are recommended for small and mid sized data operations
- T2 require EBS virtual volumens for storage
- some M5 come with their own instance storage drives

|Family|Types|Notes|
|----------|----------|-------------------|
|Compute optimized|C5, C5n, C4 | C - compute optimized you can get 3.5 GHz of processing speed, the c5d.24xlarge
|Memory optimized|R5, R5a, R5n, X1e, X1, High Memory, z1d | for intensive database, analysis, and caching operations.  The X1e, X1, and R4 go up to 3.9 TB of DRAM with low latency SSD attached|
|Accelerated computing|P3, P2, Inf1, G4, G3, F1| Recommended for 3D visualizations and rendering, financial analysis, and computational fluid dynamics|
|Storage optimized|I3, I3en, D2| work well with distributed file systems and heavyweight data processing applications - the H1, I3, and D2 types make up the Storage Optimized family |

## EC2 Instances - 3 things to Always Get Right

### Geographic Region

- Launch EC2 instances close to customers
- If there are compliance needs, launch EC2 instances in required regions
- You must be "in the region" to manage the EC2 instances in that region
- Update region in console or with `aws configure`

### VPCs

- Easy to use AWS network organizers
- Great tools to organize infrastructure
- You could have one VPC for development, one for beta testing, and one for production
- wow, wow, wow...wow.
- Adding a VPC that does NOT use a Network Address Translation (NAT) gateway or VPN access won't cost *anything*

### Tenancy

- Default setting is *shared tenancy* where instance runs as VM on physical server with other instances
- Other instances might be operated by others, but the possibility of insecure interactions between instances is *remote*
- Dedicated Instance means you get your own physical server
- Dedicated Host option allows you to control the assigned physical server to meet licensing or regulatory requirements

## Configure Instance Behavior

>Bootstrapping: You can tell EC2 to execute commands as it boosts via an instance configuration file.

- Using the AWS CLI `--user-data` value, you can script any changes needed.
  - Example: install a web server and populate the root directory

## Placement Groups

|Placement Group|Notes|
|----------|-------------------|
|Cluster|launch each instance into a single availability zone with close proximity to each other.  This provides low latency network interconnectivity for HPC (high performance computing) applications |
|Spread|separate instances physically across hardware racks to reduce risk, similar to VMWare's Distributed Resource Scheduler|
|Partition|instances can exist close to each other in a single partition, but instances within that partition are separated `???`|

## Instance Pricing

### On-Demand

- Most expensive per hour
- Most flexible as you can start and stop instances

### Reserve

- You want to stay on 24/7
- Commitment is 1-3 years
- Usually paid for up front for savings

### Spot

- For workloads that can be interrupted
- You bid and hope you get some compute based on your bid

## Instance Lifecycle

- Terminating an instance destroys all data on the instance.  The exception is when Elastic Block Store is used, which can be set to persist the data.

- A stopped instance with a nonpersisted public IP address will most likely get a different IP address when restarted.  If a predictable IP address is needed, allocate an elastic IP address and associate that with your instance.

- An instance's security group can be changed *while it is running*.

- An instance type can be changed (increase memory or speed, for example) *not while it is running*.  You do need to stop it, then change the type, then restart it.

## Resource Tags

- Establish a consistent naming convention and apply it to tags

> The related security group has the same `key` but uses a different value, allowed them to be searched more easily.

|Key|Value|
|-----|------|
|`production-server`|`server1`|
|`production-server`|`server2`|
|`production-server`|`security-group1`|
|`staging-server`|`server1`|
|`staging-server`|`server2`|
|`staging-server`|`security-gropu1`|
|`test-server`|`server1`|
|`test-server`|`security-group1`|

## Service Limits

- Only 5 VPCs per region
- Only 5,000 SSH Secure Shell key pairs across account.

## EC2 Storage Volumes

- You can install multiple Elastic Block Store volumes to your instance - but each volume can only be attached to one instance.
- AWS SLA guarantees *99.99%* availability
- If an EBS does fail there are backups in place you *probably will not notice*

> IOPS - Input / Output Operations per Second

### EBS-Provisioned IOPS SSD

- For intense workloads
- Provides max IOPS/volume of 64,000
- Max throughput volume of 1,000 MB/s
- Costs $0.125/GB/month in addition to $0.065/provisioned IOPS

### EBS General-Purpose SSD

- Most regular workloads
- Provides max IOPS/volume of 16,000 IOPS/volume
- Cost $0.10/GB/month
- General purpose 8 GB boot drive for Linux - $9.60/year

### Throughput-Optimized HDD

- Reduced cost with acceptable performance
- Good for log processing and big data operations
- IOPS/volume of 500
- Maximum throughput of 500 MB/sec
- $0.045/GB/month

#### Cold HDD

- ok for infrequent access
- IOPS/volume of 250
- $0.25/GB/month

### EBS Volume Features

- All can be copied with a snapshot
- Snapshots can be used to generate other volumes
- Can be encrypted automatically or with AWS KMS keys you provide

## Instance Store Volumes

- Ephemeral
- Instance store volumes are SSDs that are physically attached so they are connected to your instance via a fast NVMe [Non-Volatile Memory Express] interface
- Use of instance store generally include in price of instance
- Work well for deployment models where instances are launched as a part of auto-scaling
- Function as disposable instances to allow for short term roles

### EBS Bottom Line

- EBS the right choice for data that needs to persist past a reboot
- EBS the right choice for working with off-the-shelf AMIs [Amazon Machine Image]

### Instance Store

- Useful for low-latency access to large amounts of data that doesn't need to survive a reboot
- Can work well when requirements do not include fantastic read/write speeds, but you want to enjoy flexibility and cost savings of S3

## Accessing EC2 Instances

- EC2s are identified by a unique IP address

> The three IP address ranges used by private networks

|From|To|
|----|----|
|10.0.0.0|10.255.255.255|
|172.16.0.0|172.31.255.255|
|192.168.0.0|192.168.255.255|

- Out of the box, you can only connect to your instance from `within its subnet` - **The instance will have no direct connection to the Internet**

If your configuration requires multiple network interfaces - to connect to otherwise unreachable resources - you create and attach one or more `virtual elastic network interfaces` to your instance.  Each of these interfaces must be connected to an **existing subnet and security group.**  Additionally, if you want, you can assign a static IP address within the subnet range.

An instance can be assigned a public IP address.  The default public IP address is **ephmeral**.  You can add a permanent elastic IP address for long term deployments.  Elasic IPs are *free* provided they are attached to *running instances.*

`$ curl http://169.254.169.254/latest/meta-data`

- ami-id
- ami-launch-index
- ami-manifest path
- block-device-mapping
- hostname
- instance-action
- instance-id
- instance-type
- local-hostname
- local-ipv4
- mac
- metrics/
- network/
- placement/
- profile
- public-hostname
- public-ipv4
- public-keys/
- reservation-id
- security-groups

> You will use the 169.254.169.254 IP for the command regardless of privae/public IP address.

---

## EC2 Security

### Security Groups

- plays the role of firewall
- default is to deny all incoming traffic and allow outgoing traffic
- group behavior defined with policy rules that allow or block traffic types
- example: a TCP [transmission control protocol] packet sent to SSH port 22 could only allow access to an instance if the source IP address is whitelisted to your company's internal network.
- web site can be open to the world, but backend servers are blocked for everyone but the members of your team

### IAM Roles

- access can be assigned with IAM roles
- when a role is assigned, they will gain access to the resources in the role policies
- you can assign a role to an EC2 instance so that processes running within it can access external rools, like an RDS instance

### NAT Devices

- Network Address Translation
- can provide private instance access *to* the Internet without allowing access to it **from** the Internet.

### Key Pairs

- Windows AMI - use private key file to retrieve password and connect to instance
- Linux AMI - private key allows for SSH session
- save the public key to the EC2 server, save the private key to a local machine
- you **should** delete the AWS copy in the event the public key is lost or exposed

## EC2 Auto Scaling

- dynamically adds more instances
- uses a launch configuration or launch template

### launch configurations

- document that contains launch information
- can be created from scratch
- you can **not** launch an instance from a launch configuration
- it can **not** be modified once created

### launch templates

- versioned
- more versitile than launch configurations
- can be copy/pasted to other instances

##
