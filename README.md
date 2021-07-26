# CloudFormation-S3-bucket-webpage
This repository describes the process i went through when i created a CloudFormation template which hosts a webpage in S3.

**Step 1**
- I created a new YAML file which contained the following:

```
AWSTemplateFormatVersion: 2010-09-09
Description: This template will create a S3 bucket that will host a webpage
Resources:
  Bucket:
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
In the properties section i did the following:
-set the Access Control to public so that the webpage can be accessed by anyone.
-i set an unique name to the bucket because every bucket's name needs to be so

**Step 2**
- I used the following command in the aws cli in order to create the template based on the yaml file:

```
aws cloudformation deploy --template-file template.yaml --stack-name static-website
```
