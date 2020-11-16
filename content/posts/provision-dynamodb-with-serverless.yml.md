---
title: "Provision DynamoDb with serverless.yml"
date: 2020-11-15T19:45:09Z
draft: false
---
# Provision DynamoDb with serverless.yml

Basically, it employs the same syntax as Cloud Formation json but is in yaml.

More details to here: [https://www.serverless.com/dynamodb](https://www.serverless.com/dynamodb)

```yaml
resources:
  Resources:
    companies:
      Type: AWS::DynamoDB::Table
      Properties:
        TableName: companies
        AttributeDefinitions:
          - AttributeName: gasSafeNumber
            AttributeType: S
        KeySchema:
          - AttributeName: gasSafeNumber
            KeyType: HASH
        ProvisionedThroughput:
          ReadCapacityUnits: 3
          WriteCapacityUnits: 3
```



