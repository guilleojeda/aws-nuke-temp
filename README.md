# aws-nuke-organization
A CloudFormation way to deploy and schedule aws-nuke in your organization

#Current features
- A CloudFormation template to deploy this in any account, with no configuration required (except for aws-nuke-config)
- An aws-nuke-config.yaml file with preset configurations to prevent aws-nuke from deleting this stack and its resources and any AWS SSO resources.
- A CodeBuild project is created that allows you to run aws-nuke in dry run mode with one click (dry run = it doesn't delete anything)

#Requirements
- An AWS account with an alias that doesn't contain the string "prod"
- The CloudFormation Stack must be created in us-east-1
- An S3 bucket with the name "nukeaccount-${AWS::AccountId}" in us-east-1
- The bucket must contain the aws-nuke-config.yaml file

#Upcoming features
- A CloudWatch Events event that triggers the CodeBuild project build (this is currently being tested)
- The cfn stack should create the S3 bucket and put there the aws-nuke-config.yaml file
- A way to run aws-nuke --no-dry-run with one click (possibly another CodeBuild project?)
- Notifying about which resources will be deleted (initially just sending the Build logs) and allowing an admin to trigger the no-dry-run build from somewhere nice (e.g. through a lambda that can be invoked from ????)
- Improving how the resources that will be deleted are reported. Probably parse the aws-nuke output and create a list of resources that would be deleted
- A StackSet that deploys the cfn Stack in some/all accounts in an Organization (yeah, it's in the title but it's this far into the upcoming features list. sorry)
- Centralizing the report of resources that would be deleted
- Centralizing triggering aws-nuke --no-dry-run for one/some/all accounts
- A way to provide a base aws-nuke-config (like the one preventing it from deleting itself and SSO) and allow each account to extend it with its own resources
- At this point I might as well create a static website that triggers Lambdas, I guess
