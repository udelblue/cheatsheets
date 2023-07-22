
#AWS SAM Cheat Sheet

##CLI instructions

###Install AWS SAM CLI

```console
brew tap aws/tap
brew install aws-sam-cli
```


###Verify installation
```console
sam --version
```



###Upgrading SAM
```console
brew upgrade aws-sam-cli
```



##Build and deploy a Simple Application

###Download a sample application
```console
sam init
```


###Build your application
```console
sam build
```



###Deploy your application
```console
sam deploy --guided
```


###Host your API locally
```console
sam local start-api
```


###Invoke your Lambda function directly.
```console
sam local invoke “HelloWorldFunction” -e events/event.json
```


###Packages a SAM application.
```console
sam package
```

###Publish an AWS SAM application to the AWS Serverless Application Repository.
```console
sam publish
```

###Verifies whether an AWS SAM template file is valid.
```console
sam validate
```


###Provide environment variables to the lambda functions
```console
sam local invoke --env-vars env.json “HelloWorldFunction”
```


##Logging


###Fetch logs by AWS CloudFormation stack
```console
sam logs -n HelloWorldFunction --stack-name mystack
```

###Fetch logs by using the function’s name.
```console
sam logs -n HelloWorldFunction
```

###Filters logs
```console
sam logs -n HelloWorldFunction —- stack-name mystack —- filter “error” 
```

##Generate Sample Event


###Generate sample event for s3 put operation
```console
sam local generate-event s3 delete
```
####The sample event looks like this:
```console
{
  "Records": [
    {
      "eventVersion": "2.0",
      "eventSource": "aws:s3",
      "awsRegion": "us-east-1",
      "eventTime": "1970-01-01T00:00:00.000Z",
      "eventName": "ObjectCreated:Put",
      "userIdentity": {
        "principalId": "EXAMPLE"
      },
      "requestParameters": {
        "sourceIPAddress": "127.0.0.1"
      },
      "responseElements": {
        "x-amz-request-id": "EXAMPLE123456789",
        "x-amz-id-2": "EXAMPLE123/5678abcdefghijklambdaisawesome/mnopqrstuvwxyzABCDEFGH"
      },
      "s3": {
        "s3SchemaVersion": "1.0",
        "configurationId": "testConfigRule",
        "bucket": {
          "name": "example-bucket",
          "ownerIdentity": {
            "principalId": "EXAMPLE"
          },
          "arn": "arn:aws:s3:::example-bucket"
        },
        "object": {
          "key": "test/key",
          "size": 1024,
          "eTag": "0123456789abcdef0123456789abcdef",
          "sequencer": "0A1B2C3D4E5F678901"
        }
      }
    }
  ]
}
```

##AWS SAM CLI Configuration File
The default file name is samconfig.toml
Here is an example configuration file that contains seven parameters for the default environment and the deploy command:
```console
 version=0.1
 [default.deploy.parameters]
 stack_name = "my-app-stack"
 s3_bucket = "my-source-bucket"
 s3_prefix = "my-s3-prefix"
 region = "us-west-2"
 confirm_changeset = true
 capabilities = "CAPABILITY_IAM"
 tags = "project=\"my-application\" stage=\"production\""
```

##Clean Up
```console
aws cloudformation delete-stack --stack-name sam-app --region region
```


