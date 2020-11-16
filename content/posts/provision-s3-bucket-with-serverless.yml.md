---
title: "Provision S3 Bucket with serverless.yml"
date: 2020-11-15T19:45:09Z
draft: false
---
# Provision S3 Bucket with serverless.yml

I am working on a backup story this weekend for my side project. Now the mobile app has around 250 users and we have a need to back up the users. Sometimes, user details are updated by mistake and we want to track down the old details.

So, our solution \(me and my friend. it's two developer project\), is get all the users from User Pool and save it as json blog on to S3 bucket. serverless.yml supports resource creation with minimum Cloud Formation syntax.

### resources

You can define any AWS resources in a property titled `resources`. What goes in this property is raw CloudFormation template syntax, in YAML. The following is my resource definition for S3 bucket where the function will upload the backup data to.

```yaml
resources:
  Resources:
    usersBackupBucket:
      Type: AWS::S3::Bucket
      Properties:
        BucketName: xxx-xxxxx-users-backup
        AccessControl: Private
        CorsConfiguration:
          CorsRules:
            - AllowedMethods:
                - GET
                - PUT
                - POST
                - HEAD
              AllowedOrigins:
                - "*"
              AllowedHeaders:
                - "*"
```

