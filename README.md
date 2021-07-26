# CloudFormation-S3-bucket-webpage
This repository describes the process i went through when i created a CloudFormation template which hosts a webpage in S3.

**Step 1**
I created a new YAML file which contained the following:

```
AWSTemplateFormatVersion: 2010-09-09
Description: This template will create a S3 bucket that will host a webpage
Resources:
  S3WebPageBucket:
    Type: AWS::S3::Bucket
    Properties:
      AccessControl: PublicRead
      BucketName: webapp-endava-andriescosmin
      WebsiteConfiguration:
        IndexDocument: index.html
        ErrorDocument: error.html
Outputs:
    WebsiteURL:
        Value: !GetAtt [Bucket, WebsiteURL]
        Description: URL for website hosted on S3
```
