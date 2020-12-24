# aws-nuke-temp
A CloudFormation way to deploy and schedule aws-nuke (https://github.com/rebuy-de/aws-nuke) in your account

#Current features
- A CloudFormation template to deploy this in any account, with no configuration required
- A CodeBuild project is created that allows you to run aws-nuke in dry run mode with one click (dry run = it doesn't delete anything)
- A seprate CodeBuild project is created that runs aws-nuke with --no-dry-run flag (it actually deletes resources, so be careful)
- The --no-dry-run project can be scheduled to run periodically

#Steps to use
- Create CloudFormation stack with template cfn-nuke-account.yaml and your desired values for parameters
- Name resources you want to delete starting with "temp-" (case sensitive) or with the prefix you configured in parameters
- Manually run CodeBuild project NukeAccount-NukeThisAccount-DryRun and check what would be deleted
- (Optional) Manually run CodeBuild project NukeAccount-NukeThisAccount-NoDryRun-CAREFUL whenever you want to delete resources
- (Optional) Update CFN stack parameters so that NoDryRun CodeBuild project runs periodically

#Requirements
- An AWS account with an alias that doesn't contain the string "prod" (constraint from aws-nuke)
- The CloudFormation Stack must be created in us-east-1

#Note
- Only resources with name starting with a configurable name prefix (default is "temp-") will be deleted

#Upcoming features (someday)
- More readable logs
- Improving how the resources that will be deleted are reported. Probably parse the aws-nuke output and create a list of resources that would be deleted
- Notifying about which resources will be deleted (initially just sending the Build logs somewhere) and allowing an admin to trigger the no-dry-run build from somewhere nice (e.g. through a lambda that can be invoked from maybe Api Gateway?)

Originally this project was meant to provide a way to centralize resource deletion in some/all accounts in an Organization. If you're interested in making this org-wide, get in touch.
