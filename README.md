<p align="center">
<img src="https://imgur.com/2HDDgj5.jpeg" alt="AWS logo"/>
</p>

<h1>Lab -  Implement AWS Config to Monitor Compliance with Security Policies
 </h1>

 This project focuses on setting up AWS Config to monitor the compliance of AWS resources with your organization’s security policies. AWS Config continuously records configuration changes and evaluates them against predefined rules, ensuring that your infrastructure is compliant with best practices and internal standards.

Objective:
- Goal: Implement AWS Config to monitor and enforce compliance with security policies for AWS resources, such as ensuring S3 buckets are encrypted, EC2 instances are properly tagged, and security groups do not allow open ports.
- Skills Covered: AWS Config setup, rule creation, resource compliance monitoring, remediation actions, reporting, and automation.

Step 1: Create or Access an AWS Account
1. If you don’t already have an AWS account, create one at AWS sign-up page.
2. Log into the AWS Management Console using your credentials.

Step 2: Navigate to AWS Config
1. In the AWS Management Console, type AWS Config in the search bar and select it from the dropdown.
2. Once inside the AWS Config dashboard, you’ll be prompted to configure AWS Config for the first time if it hasn’t been set up already.

Step 3: Set Up AWS Config
3.1: Choose Resources to Record
AWS Config allows you to record the configuration changes for specific AWS resources or all resources in your account.

1. In the AWS Config dashboard, click on Set Up AWS Config.
2. Under Resource Types to Record, choose Record all resources supported in this region if you want AWS Config to track all AWS resources.
 - Alternatively, you can select Specific types and choose specific resources to track (e.g., S3, EC2, IAM, Lambda).

3.2: Set Up a Delivery Channel
The delivery channel is where AWS Config stores configuration snapshots and changes.

1. Under Delivery method, AWS Config will automatically create an S3 bucket to store snapshots. The bucket name will be auto-generated, but you can also create a custom S3 bucket.

3.3: Set Up IAM Role for AWS Config
AWS Config needs permissions to track and record configuration changes. AWS will create a role automatically with the necessary permissions.

1. In the IAM Role section, select Create a new role if AWS hasn't created one for you automatically.
2. The role will have a policy allowing AWS Config to perform actions such as reading your resources and writing configuration changes to your S3 bucket.
3. Review the setup and click Next to continue.

Step 4: Define Compliance Rules
AWS Config evaluates your resources against rules, which define the desired configuration state for your resources. AWS offers predefined managed rules, or you can create custom rules using AWS Lambda.

4.1: Select AWS Managed Rules
To monitor compliance with common security best practices, you can choose from the list of AWS Config Managed Rules.

1. In the AWS Config dashboard, click Rules on the left panel.
2. Click Add Rule.
3. Choose from popular AWS Managed Rules, such as:
 - s3-bucket-server-side-encryption-enabled: Ensures all S3 buckets are encrypted.
 - ec2-instance-detailed-monitoring-enabled: Checks if detailed monitoring is enabled for EC2 instances.
 - security-group-no-ingress-check: Ensures security groups do not allow unrestricted inbound access (e.g., open ports).
 - iam-password-policy: Ensures IAM password policies are in line with best practices.
4. Select the desired rules for your environment and click Next.

4.2: Customize Rule Parameters (Optional)
Some rules allow you to customize parameters to fit your organization’s security policies.

1. For example, when using s3-bucket-public-read-prohibited, you can configure which buckets should be exempt from the rule.
2. For the security-group-no-ingress-check rule, you can specify allowed IP ranges or ports if necessary.
3. Once configured, click Save to add the rule to AWS Config.

Step 5: Monitor Resource Compliance
AWS Config will now evaluate your AWS resources against the rules you defined and provide compliance reports.

5.1: View Compliance Dashboard
1. Navigate to the Rules section of AWS Config to view the compliance status.
2. The dashboard will show the compliance status (compliant or non-compliant) for each rule applied to your resources.

5.2: Investigate Non-Compliant Resources
1. Click on any non-compliant rule to view details about which resources are non-compliant.
 - For example, if an S3 bucket is not encrypted, it will be flagged under the s3-bucket-server-side-encryption-enabled rule.
2. AWS Config provides details about when the resource became non-compliant, the exact rule violation, and the resource’s current configuration.

Step 6: Automate Remediation with AWS Systems Manager (Optional)
For non-compliant resources, you can automate remediation actions using AWS Systems Manager Automation or by triggering custom AWS Lambda functions.

6.1: Create an Automation Document (Runbook)
1. Go to the AWS Systems Manager console and select Automation from the left menu.
2. Click Create Automation and choose to create a new automation document.
3. In this document (runbook), specify the steps required to remediate the issue. For example:
 - For non-encrypted S3 buckets, you can automatically apply SSE (Server-Side Encryption).
 - For open security groups, automatically adjust the rules to block unwanted ports.
4. Save the automation document.

6.2: Link Automation to AWS Config Rules
1. In the AWS Config dashboard, select the non-compliant rule.
2. Click Remediation and associate the automation runbook you just created.
3. Set the remediation to trigger automatically whenever a resource becomes non-compliant.
Now, whenever AWS Config detects a non-compliant resource, AWS Systems Manager will automatically run the automation to bring it back into compliance.

Step 7: Reporting and Alerts
7.1: Generate Compliance Reports
AWS Config automatically generates reports showing the compliance status of your AWS resources.

1. In the AWS Config dashboard, navigate to Compliance > Resource Compliance.
2. View a list of all resources and their compliance status.
3. You can export this data in CSV format for internal audits or compliance reviews.

7.2: Set Up Alerts for Non-Compliance
1. Go to AWS CloudWatch and set up an Alarm to trigger when non-compliance is detected.
2. In CloudWatch, create a New Alarm, and under the metric search, type ConfigCompliance.
3. Set a threshold for when the number of non-compliant resources exceeds a specific limit.
4. Connect the alarm to your SNS topic to receive alerts via email or SMS when a compliance issue arises.

Step 8: Clean Up Resources
Once you've completed the project, make sure to clean up your environment to avoid any unnecessary charges.

1. Delete AWS Config Rules:
 - Go to the AWS Config dashboard and delete the rules you created.

2. Delete the S3 Bucket:
 -  If you created a custom S3 bucket for AWS Config, delete it from the S3 Console.

3. Delete Automation Documents:
 - If you created an automation document in AWS Systems Manager, delete it from the Automation section.

Project Outcomes
By completing this project, you will have:

- Set up AWS Config to monitor the configuration of AWS resources.
- Defined compliance rules using AWS Managed Rules to enforce security best practices.
- Monitored resource compliance using the AWS Config dashboard.
- (Optional) Automated remediation using AWS Systems Manager or Lambda.
- Generated compliance reports and set up alerts for non-compliant resources.
This project will help you gain hands-on experience with cloud security monitoring, compliance management, and automated remediation, which are essential skills in the cloud security and IAM domains.
