**Guidance for Accelerating Analytics on AWS**

This Guidance enables developers and admins to deploy a customizable AWS Analytics stack through CloudFormation. ISV and Enterprise customers want replicable architectures and support for advanced identity and access requirements. CloudFormation enables these personas to get started quickly by following best practices around fine-grained identity and access management control. The target services to onboard as part of this experience include S3, Lake Formation, Glue, Athena and QuickSight.
The Guidance flow enables customers to deploy an end-to-end AWS Analytics POC through a guided onboarding experience with minimal configuration overhead. The target use case for this experience is a POC in a sandbox environment where complex permissions and configurations are not required to validate core business requirements.

**Getting Started**

To gain insights from data, you have to create a S3 bucket and upload data as flat file(s). Then, the CloudFormation template Easyanalytics.yml can be leveraged to create a stack that provisions all necessary services including IAM Role, LakeFormation, Glue, Athena and QuickSight. The stack output is a QuickSight Analysis that can be used to visualize the data in the S3 bucket.

**Input**

All input parameters are required.

- Stack name - Stack name can include letters (A-Z and a-z), numbers (0-9), and dashes (-)
- DataSetLocation - Enter S3 URI for your dataset. E.g. s3://bucket/prefix/data/
- QuickSightUser - User name of QuickSight user from default namespace (as displayed in - QuickSight admin panel). For new a QuickSight subscription, ensure this User name is not same as any IAM username and does not contain ‘/’. Dashboard created by this template with be shared with this user
- QuickSighAccountName - Account name for a new QuickSight subscription. The account name cannot be changed later. This value is ignored if you have an existing QuickSight account
- QuickSighNotificationEmail - Notification email for a new QuickSight account. This value is ignored if you have an existing QuickSight account
- Suffix - If you need to create multiple instances of embedding sample on the same AWS account, add a short NUMERIC suffix here

**Follow the steps below to create the CloudFormation stack**

1. Download/Save the Easyanalytics.yml file
Navigate to AWS Console
1. Search for CloudFormation in the "Services" search bar
2. Once in the CloudFormation console, click on the "Create Stack" button (use the "With new resources option")
3. In the "Create Stack" wizard, chose "Template is ready", then select "Upload a template file"
4. Upload the provided yaml file, click Next
5. In the Specify stack details screen, provide the required inputs
6. In the Configure Stack options screen, leave the configurations as-is. Click Next
7. In the Review screen, scroll down to the bottom of the page to the Capabilities section and acknowledge the notice that the stack is going to create required IAM Roles by checking the check box. 
8. Click Create stack

**Output**

The stack creation can take up to 15 minutes. Once the stack creation is complete, you can check the Outputs section of the stack for the following:

- If you had an existing QuickSight subscription in your AWS Account, the output section will have a link to an empty QuickSight Analysis, accessible by the QuickSight username you provided
* If you do not have an existing QuickSight subscription, the stack creates a new QuickSight subscription, a user with the username provided and outputs an empty QuickSight Analysis as well as an invitation URL to setup login credentials for the user

You can now start visualizing your data in Amazon QuickSight!

**Resources**

The CloudFormation template provisiones the following resources which can be optionally deleted to avoid additional billing.

- S3 Bucket: *easyanalytics-codebucket-<AWS_Account_ID>-< Suffix>*
- Lambda Functions: *EasyAnalyticsCodeDownload< Suffix>* and *EasyAnalyticsCustomResource< Suffix>*  