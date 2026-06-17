# aws-s3-cloudfront-deployment
Static site deployed on AWS — private S3 bucket served through CloudFront with OAC. No direct bucket exposure.
# Deploying a Static Site Securely on AWS S3 + CloudFront

Aiming for a solid understanding of AWS, I embarked on something basic —
correctly hosting a static site instead of just making the bucket public. 

## Structure

User → CloudFront (HTTPS) → S3 (private)  
User → S3 direct   → 403 Access Denied

## The Steps I Took

- S3 bucket was blocked from public access.
- OAC was created and connected to CloudFront distribution.
- IAM bucket policy generated was pasted. S3 now verifies the requests only signed by that specific distribution.
- HTTPS redirect was set at the CloudFront layer.
- Cache invalidated after push updates

## Things I discovered

OAC is not a special feature but it's CloudFront signing every request to S3 using AWS credentials which S3 can use to verify the user.
The bucket policy is what ties it all up. If it were not for this S3 would have had no trust in anyone.

## Technology Used
AWS S3 · CloudFront · IAM
**Live:** https://d2bilue0rk2rbp.cloudfront.net/
