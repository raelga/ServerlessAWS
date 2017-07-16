# ServerlessSomething

Something serverless using API Gateway, Cognito, S3 and DynamoDB. Front maybe with Vue.js.

## First steps

### Set up AWS Users and Permissions

#### Create a Group with permission on the AWS Serverless Services:

On this step, you will create a group with the necessary permissions to manage the AWS Serverless services. You can call this group something like `serverless-adm` as the members of this group will full control over the resources needed in our serverless service.

Go to the AWS Web console and create a new group: [AWS > IAM > Groups > New](https://console.aws.amazon.com/iam/home#/groups$new?step=details)

After the name configuration, you will need to add the following policies for the services that we will use in the future. If your service doesn't need a particular service from the list down below, you can safely ignore it.

Policies for the Group `serverless-adm`:

- AmazonDynamoDBFullAccess
- AmazonS3FullAccess
- AWSLambdaFullAccess
- AmazonCognitoPowerUser
- AmazonAPIGatewayAdministrator

Confirm and we're done!

#### Create a User for the AWS CLI

Now we will create the user that we will use in our computer to deploy and manage the services using the CLI.

Choose the name for the user, I like to have a particular user for each computer / AWS CLI installation. Your choice.

Go to the AWS Web console and create a new user: [AWS > IAM > Users > New](https://console.aws.amazon.com/iam/home#/users$new?step=details)

For the access type, I will only enable `Programmatic access` as this user will be used only via de AWS CLI. Again, this a personal preference, I like to have only one human IAM User for me to manage the AWS resources via the web console and a set of users for the programmatic access. If you want to be able to use the AWS Web Console with this user, enable the `AWS Management Console access` access type too.

Add the user to the group that we created before, `serverless-adm` in this example, and will inherit all the group permissions defined before.

And in the last step, safe-keep the AWS Access Key ID and the Secret Access Key as you will need them to configure your AWS CLI.


### Set up the AWS CLI

#### Install the AWS CLI

Follow the installation guide to install the AWS CLI on your machine.

http://docs.aws.amazon.com/cli/latest/userguide/installing.html

### Configure the AWS CLI access and default settings

```bash
aws configure
```

This command will ask you some configuration needed to be able to access the AWS API:

```bash
AWS Access Key ID [None]: AKIAI44QH8DHBEXAMPLE
AWS Secret Access Key [None]:  je7MtGbClwBF/2Zp9Utk/h3yCo8nvbEXAMPLEKEY
Default region name [None]: eu-west-1
Default output format [None]: json
```

The AWS Access Key and Secret, are the ones generated for the user that we created in the previous step. You can revoke and generate new keys any time, check [Managing Access Keys for IAM Users documentation](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html#Using_CreateAccessKey) for more information.

The region is usually the region closest to you, but you can configure anyone. *Before deploying anything*, be aware that some services are available only in specific regions. For more information about the services of each region, check the [AWS Regions and Endpoints documentation](http://docs.aws.amazon.com/general/latest/gr/rande.html).

The output setting just configures how the AWS CLI will print the execution results.

For more information about the initial AWS CLI configuration, please check [Configuring the AWS CLI documentation](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html).