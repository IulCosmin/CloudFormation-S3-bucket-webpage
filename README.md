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

After that i used the following command in the aws cli in order to check if the stack was created succesfully

```
aws cloudformation list-stacks --stack-status-filter CREATE_COMPLETE
```

**Step 3**
I used the following commands in the aws cli in order to upload the index and error files in the bucket

```
aws s3 cp .\error.html s3://webpage-endava-andriescosmin/
aws s3 cp .\error.html s3://webpage-endava-andriescomin/
```

**Step 4**
In the end, i checked if both pages (index + error) were sucessfully hosted using the following links:
https://webapp-endava-andriescosmin.s3.eu-west-1.amazonaws.com/index.html
https://webapp-endava-andriescosmin.s3.eu-west-1.amazonaws.com/errortesting.html
