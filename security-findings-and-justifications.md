## Introduction

During tenant account creation or migration, GCC2.0 deploys resources into the account as a baseline. Some resources and configurations may attract security findings against the security benchmarks or standards.

This document lists the known findings on such GCCI resources in tenant accounts and provides justifications for the deviation. It also keeps track of any suppression implemented for such findings by GCC2.0.

## AWS

**Notation**

* CIS: CIS AWS Foundations Benchmark v1.20
* SBP: AWS Foundational Security Best Practices v1.0.0
* PCI DSS: Payment Card Industry Data Security Standard v3.2.1


## Tables

| Resource | Resource ID (if applicable) | Deviation from Standard & Control | Justification |
| ------------- |-------------|-------------|-------------|
| root user account      | | **CIS**<br>- CIS.1.14: Ensure hardware MFA is enabled for the "root" account<br>- CIS.1.13: Ensure MFA is enabled for the "root" account<br><br>**SBP**<br>- IAM.6: Hardware MFA should be enabled for the root user<br><br>**PCI DSS**<br>- PCI.IAM.4: Hardware MFA should be enabled for the root user<br>- PCI.IAM.5: Virtual MFA should be enabled for the root user |1. According to IM 8, MFA is needed for all administrative access. However, it did not specify the need for hardware MFA.<br><br>2.	For all root accounts, there a need to enforce MFA.<br><br>3. Agency tenant should refer to this link to reset root account password and configure MFA. |



| Resource | Resource ID (if applicable) | Deviation from Standard & Control | Justification |
| ------------- |-------------|-------------|-------------|
|  **IAM User**<br>terraform_svc    |  arn:aws:iam::379388416279:user/terraform_svc   |**CIS**<br>-	CIS.1.4: Ensure access keys are rotated every 90 days or less<br>-	CIS.1.3: Ensure credentials unused for 90 days or greater are disabled<br><br>**SBP**<br>-	IAM.3: IAM users' access keys should be rotated every 90 days or less<br><br>**PCI DSS**<br>- PCI.IAM.7: Unused IAM user credentials should be removed<br>- PCI.IAM.6: MFA should be enabled for all IAM users |1. This IAM user is reserved for tenants to manage their infrastructure using IaC. Currently it is not in use, and there is no permission attached to it. In future, tenants will be managing the permissions for this IAM user based on their needs.<br><br>2. The IAM key and secret generation is fully handled by automation. The key and secret are only used by terraform workspace and nobody else has access to the key and secret. SCP is also in place to block tenants from adding, deactivating or removing existing key secret pair. <br><br>3. Removal of unused credentials for more than 90 days is no longer valid because there is a chance that a tenant has no change made or trigger a terraform plan and apply in 90 days. |



| Resource | Resource ID (if applicable) | Deviation from Standard & Control | Justification |
| ------------- |-------------|-------------|-------------|
| **Cloudformation Stack**<br><br>awsconfigconforms-OrgConformsPack-CloudSCAPE-Conformance-Pack | arn:aws:cloudformation:ap-southeast-1:*:stack/awsconfigconforms-OrgConformsPack-CloudSCAPE-Conformance-Pack-* | **SBP**<br>CloudFormation.1: CloudFormation stacks should be integrated with Simple Notification Service(SNS) | This cloudformation is a deployment of AWS organization conformance pack managed by cloudscape team.<br> Instead of using SNS, deployment status or errors, are directly reflected on core-security account console under organization conformance pack service. Cloudscape team and GCC2.0 CLM team will handle the failure during deployment. |
| **Cloudformation Stack**<br><br>gcci-vend-gateway-subnet-for-* | arn:aws:cloudformation:ap-southeast-1:*:stack/gcci-vend-gateway-subnet-for-* | **SBP**<br>CloudFormation.1: CloudFormation stacks should be integrated with Simple Notification Service (SNS) | This cloudformation is part of workflow to provision new VPC in agency account. The request originates from agency request on GCC2.0 CMP.<br><br>Instead of using SNS, GCC2.0 Provisioning team and CMP team receive and monitor alert of failure directly from provisioning api responses and handle the provisioning failure accordingly. |
| **Cloudformation Stack** <br><br> gcci-vend-gen-cidr-for-* | arn:aws:cloudformation:ap-southeast-1:*:stack/gcci-vend-gen-cidr-for-* | **SBP**<br>CloudFormation.1: CloudFormation stacks should be integrated with Simple Notification Service (SNS) | This cloudformation is part of workflow to provision new VPC in agency account. The request originates from agency request on GCC2.0 CMP. <br><br>Instead of using SNS, GCC2.0 Provisioning team and CMP team receive and monitor alert of failure directly from provisioning api responses and handle the provisioning failure accordingly. |



| Resource | Resource ID (if applicable) | Deviation from Standard & Control | Justification |
| ------------- |-------------|-------------|-------------|
| **Lambda Function**<br><br>clm-pac-rules-GT* | arn:aws:lambda:ap-southeast-1:*:function:clm-pac-rules-GT* | **PCI DSS**<br>PCI.Lambda.2: Lambda functions should be in a VPC | These lambdas form part of GCC2.0 PaC policies. Custom logic is implemented to inspect tenants’ AWS resources. The lambdas do not require network interface in any VPC, and do not inspect resources at OS level in virtual machines.<br><br>Therefore, the lambdas do not require interaction with any VPC or private subnet. Hence these lambda functions should not be placed in VPC. https://aws.amazon.com/blogs/architecture/best-practices-for-developing-on-aws-lambda/ <br><br>As further confirmed by AWS, lambda not deployed in VPC cannot be triggered by any public resources, and not exposed to public network |
| **Lambda Function**<br><br>clm-central-logging-migration | arn:aws:lambda:ap-southeast-1:*:function:clm-central-logging-migration | **PCI DSS** <br>PCI.Lambda.2: Lambda functions should be in a VPC | Same as above.<br><br>This lambda is used at GCC to GCC2.0 account migration. It re-configures CloudWatch log groups’ subscription filters from GCC1.0 central logging to GCC2.0’s. It does not require network interface in any VPC, and does not update resources at OS level in virtual machines. |
| **Lambda Function** <br> clm-modify-sechub-severity-label-lambda | arn:aws:lambda:ap-southeast-1:*:function:clm-modify-sechub-severity-label-lambda | **PCI DSS**<br>PCI.Lambda.2: Lambda functions should be in a VPC<br> | Same as above.<br><br> This lambda forms part of GCC2.0 PaC implementation. It adjusts finding’s severity level in security hub. It does not require network interface in any VPC, and does not update resources at OS level in virtual machines. |
| **Lambda Function**<br><br>clm-central-logging-firehose-lambda | arn:aws:lambda:ap-southeast-1:*:function:clm-central-logging-firehose-lambda | **PCI DSS**<br>PCI.Lambda.2: Lambda functions should be in a VPC | Same as above.<br><br> This lambda forms part of GCC2.0 central logging implementation. It facilitates the logging partition in firehose before piping CloudWatch log groups to central S3 bucket in GCC2.0 core logging account. It does not require network interface in any VPC, and does not update resources at OS level in virtual machines.|
| **Lambda Function** <br><br>clm-pac-iam-event-sns-to-EventBridge| arn:aws:lambda:ap-southeast-1:*:function:clm-pac-iam-event-sns-to-EventBridge| **PCI DSS**<br>PCI.Lambda.2: Lambda functions should be in a VPC | Same as above.<br><br> This lambda forms part of GCC2.0 PaC implementation. It forwards IAM events that are collected globally to ap-southeast-1 region for further processing. It does not require network interface in any VPC, and does not update resources at OS level in virtual machines. |
| **Lambda Function** <br><br>tlz-ipam-management-retry| arn:aws:lambda:ap-southeast-1:*:function:tlz-ipam-management-retry | **PCI DSS**<br>PCI.Lambda.2: Lambda functions should be in a VPC | Same as above<br><br>This lambda forms part of GCC2.0 VPC provisioning implementation. It sends retry request for CIDR reservation to IPAM (DynamoDB based). It does not require network interface in any VPC, and does not update resources at OS level in virtual machines. |
| **Lambda Function**<br><br>tlz-ipam-management-updatecidr |arn:aws:lambda:ap-southeast-1:*:function:tlz-ipam-management-updatecidr | **PCI DSS** <br>PCI.Lambda.2: Lambda functions should be in a VPC | Same as above<br><br>This lambda forms part of GCC2.0 VPC provisioning implementation. It sends update or delete request for CIDR record to IPAM  (DynamoDB based). It does not require network interface in any VPC, and does not update resources at OS level in virtual machines. |
| **Lambda Function** <br><br>tlz-ipam-management-getcidr| arn:aws:lambda:ap-southeast-1:*:function:tlz-ipam-management-getcidr | **PCI DSS**<br>PCI.Lambda.2: Lambda functions should be in a VPC | Same as above<br><br>This lambda forms part of GCC2.0 VPC provisioning implementation. It sends get request for CIDR record to IPAM (DynamoDB based). It does not require network interface in any VPC, and does not update resources at OS level in virtual machines. |
