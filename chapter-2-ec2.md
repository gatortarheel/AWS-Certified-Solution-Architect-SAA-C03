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
|General purpose | A1, T3, T2, M6g, M5, M5a, M5n, M4 | t2.micrso is a good choice for experimenting; T2s are burstable, you can accumulate CPU credits when your instance is underutilized, and then apply those credits during high demand time in the form of CPU performance|
|Compute optimized|C5, C5n, C4 |
|Memory optimized|R5, R5a, R5n, X1e, X1, High Memory, z1d |
|Accelerated computing|P3, P2, Inf1, G4, G3, F1|
|Storage optimized|I3, I3en, D2|

