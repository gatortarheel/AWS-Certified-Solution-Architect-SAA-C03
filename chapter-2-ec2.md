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

# EC2 Storage Volumes


