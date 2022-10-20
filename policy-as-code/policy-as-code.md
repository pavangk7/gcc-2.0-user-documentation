
# Policy AS Code
 ## PAC with AWS Security Hub

Revision History


| Date | Revision | Author | Description |
| :--- | :--- | :--- | :--- |
| **2/8/2022** | 1.0.0 | Hazel Wong</br> Chua Kai Ming | - Initial Draft |
| **10/8/2022** | 1.1.0 | Hazel Wong | - Updated remediation steps, included step-by-step guide for compliance to Batch 1 & 2 PaC rules (GT1.4 + GT1.5 not completed)</br> - Updated PaC Overview background, provided more details of Security Hub available controls, pricing </br> - Included new Section 6: References with AWS Documentation URLs </br> - Section 1.2 – Included new column containing resources used by PaC setup </br> - Incomplete: Included new Section 3.2. for alert notifications to Slack/Email/ITSM |


# Contents

[Revision History 2](#_Toc113987053)

[1.GCC 2.0 Policy as Code Overview 5](#_Toc113987054)

[1.1.Target Audience 5](#_Toc113987055)

[1.2.Prerequisites (Things to take note) 5](#_Toc113987056)

[1.3.Background 5](#_Toc113987057)

[1.4.What does GCC 2.0 PaC covers 5](#_Toc113987058)

[1.5.AWS Resources Utilized for custom PaC Rules 6](#_Toc113987059)

[1.6.Costing 7](#_Toc113987070)

[2.PaC Rules 9](#_Toc113987071)

[2.1.Custom Batch 1 & 2 PaC Rules 9](#_Toc113987072)

[2.2.Batch 1 & 2 PaC Rules Remediation Steps 10](#_Toc113987073)

[3.Compliance Management on Aws Security Hub 29](#_Toc113987074)

[3.1.Suppressing Alerts 29](#_Toc113987075)

[3.2.Setup Security Hub alerts to Email/Slack/ServiceNow ITSM 32](#_Toc113987076)

[4.Frequently Asked Questions (FAQ) 33](#_Toc113987077)

[5.Technical Support 34](#_Toc113987078)

[6.References 35](#_Toc113987079)

# 1.GCC 2.0 Policy as Code - Overview

## 1.1.Audience

This playbook is intended for the following agency users:

- Agency Chief Information Security Officer (ACISO)
- Agency Security Incident Response Officer (ASIRO) and
- Account administrators.

## 1.2. Key things to take note

- Agency can't modify the clm-pac rules deployed to their agency account.
- Agency can't modify resources used by clm-pac which has a tag key gcc:team and value as gcci.
- In addition to clm-pac rules, agency can define and add additional PaC rules to their account .
- Agency can additionally add up to 391 more custom config rules within their accounts
- In addition to resources used by clm-pac, agencies can also add additional tags.

## 1.3.Background

Policy as Code (PaC) custom rule is introduced as part of GCC2.0's enhancement to provide additional security coverage for organisation-specific security requirements. PaC acts a detection service that alerts agency administrators/CISO/SIRO of non-compliant resources and does not perform intrusive actions such as modifying, adding, or deleting any resources.

GCC2.0 adopts a _light-touch_ approach in compliance monitoring to improve security posture while ensuring that the security measures are not overly restrictive.

AWS Security Hub is a Cloud Security Posture Management (CSPM) that checks AWS services and resources against security best practices and aggregates compliance alerts onto the Security Hub Findings dashboard.

Security Hub with AWS config and EventBridge are used in GCC 2.0 as the main PaC toolchain to detect non-compliant settings or resources in the tenant environment.

## 1.4.What does GCC 2.0 PaC cover

The following security standards are available on GCC 2.0:

| **#** | **Standards** | **Is it enabled by default?** | **Can it be disabled?** | **Industry Benchmark/Custom** | **Can it be modified?** |
| --- | --- | --- | --- | --- | --- |
| 1 | CIS AWS Foundations Benchmark | Yes | No | Industry Benchmark | No |
| 2 | AWS Foundational Security Best Practices | Yes | Yes (Depending on agency's requirement) | Industry Benchmark | No |
| 3 | Payment Card Industry Data Security Standard (PCI DSS) | No.
 Note: Agency may enable it if required) | Yes (Depending on agency's requirement)
 | Industry Benchmark | No |
| 4 | GovTech PaC rules | Yes | No | Custom | No |

Security Hub findings retention period:

- Findings are **retained for 90 days** and will be automatically removed from the dashboard after 90 days.
- Findings can be exported to S3 buckets for long-term storage:
  - To be configured by the agencies.
  - To export security hub findings to S3 buckets, setup security hub custom action and EventBridge rule. When the agency administrators export the findings to S3 buckets, they need to invoke the custom action manually on the security hub dashboard.
  - For detailed instructions, refer to the additional resources.

**Additional resources:**

- [Overview of Security Hub](https://aws.amazon.com/security-hub/)
- [Security Hub Features](https://aws.amazon.com/security-hub/features)
- [Security Hub Cost](https://aws.amazon.com/security-hub/pricing/)
- Integration of [Security](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-settingup.html) Hub
- [Security Hub standards and control](/C:/Users/gt-senks/AppData/Local/Microsoft/Windows/INetCache/Content.Outlook/D5DEQ5RN/5.%09https:/docs.aws.amazon.com/securityhub/latest/userguide/securityhub-standards.html)
- [Overview of EventBridge](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html)
- [EventBridge Cost](https://aws.amazon.com/eventbridge/pricing/)

## 1.5.AWS resources utilised for custom PaC rules

|
 |
 |
 |
| --- | --- | --- |
|
## AWS services
 |
## AWS resources utilised
 |
## Description
 |
|
## **Lambda**
 | **PaC Functions** :
- clm-pac-rules-**[PaC-Name]**
 **Update PaC severity level** :
- clm-modify-sechub-severity-label-lambda
 | Contains the **custom logic** to determine the compliance of agency resources status with AWS config as evaluation results or AWS Security Hub as Findings. In addition, Lambda also modifies the severity level for custom PaC rules.
 |
|
## **Config**
 | **Custom Config Rules:**
- clm-pac-**[PaC-Name]**
 | Custom Config leverages on Lambda logic evaluation to determine compliance status. Automatically imports AWS Config evaluation results to Security Hub as Findings.


 |
|
## **EventBridge Rule**
 | **Custom EventBridge Rules** :
- clm-event-**[Rule-Name]**
- clm-modify-sechub-severity-label-cw-rule
 |

Lambda evaluates the resources to determine compliance status in case of events, such as the creation of new resources or configuration changes that match the patterns predefined in the EventBridge Rule.
 |
|
## **Security Hub**
 |

**N/A** |

Displays non-compliant resources or configuration changes in the Findings Dashboard. From this dashboard, agency administrators can perform the necessary remediation to ensure all resources remain compliant. |
|
## **SNS (Optional & Agency responsibility)**
 |
## **Topic:**

- clm-pac-sechubfindings-email
 |
##

Sends PaC alert notifications to recipients through email, Slack and third-party products. Refer to section 3.2.
 |

## 1.6.Costing

Note: Prices are in US dollars.

Lambda:

| **No. of Occurrences** | **Cost Calculation** | **Total Cost** |
| --- | --- | --- |
| **5 million requests** | 1 million x 1 region x $0.00 per request (free tier: first 1 million requests)4 million x 1 region x $0.20 per 1 million requests | First 1 million requests: $0.00Next 4 million requests: $0.80 |
| **200,000 compute time (per GB-second)** | 200,000 x 1 region x $0.00 per event (free tier: first 400,000 events) | $0.00 |
|
 | Total Lambda cost per month (USD) | $0.80 |

Config Rules:

| **No. of Occurrences** | **Cost Calculation** | **Total Cost** |
| --- | --- | --- |
| **500 rule evaluations** | 500 x 1 region x $0.001 per evaluation (first 100,000 rule evaluations) | $0.50 |
| **350 configuration item change** | 350 x 1 region x $0.003 per configuration item recorded | $1.05 |
|
 | Total Config cost per month (USD) | $1.55 |

EventBridge:

| **No. of Occurrences** | **Cost Calculation** | **Total Cost** |
| --- | --- | --- |
| **10 custom events** | 10 x 1 region x $0.00 per check($0 for \< 1 million events, AWS will only start charging if it exceeds 1 million events) | $0.00 |
|
 | Total EventBridge cost per month (USD) | Free of charge |

Security Hub:

| **No. of Occurrences** | **Cost Calculation** | **Total Cost** |
| --- | --- | --- |
| **2500 security checks** | 2500 x 1 region x $0.0010 per check (first 100,000 checks tier) | $2.50 |
| **150,000 finding ingestions** | 10000 x 1 region x $0.00 per event (first 10,000 events - free tier)140000 x 1 region x $0.00003 per event (more than 10000 events) | First 10,000 events: $0.00Next 140,000 events: $4.20 |
|
 | Total Security Hub cost per month (USD) | $6.70 |

Simple Notification Service (SNS)\*:

| **No. of Occurrences** | **Cost Calculation** | **Total Cost** |
| --- | --- | --- |
| **60 email notifications** | 60 x 1 region x $0.00 per notification (free tier: first 1,000 notifications) | $0.00 |
|
 | Total SNS cost per month (USD) | $0.00 |

\*(Optional: Agency responsibility)

Note:

- For more information, refer to the links provided in Section 6: References
- Estimated total PaC recurring cost is **approximately**** 10.00 USD per month.**

# 2.PaC Rules

The following section provides the list of PaC rules for AWS and its respective description.

## 2.1.Custom bBatch 1 & 2 PaC rRules

|
 |
 |
 |
 |
| --- | --- | --- | --- |
| Rule Name | Severity Level | Frequency | Description |
| **GT1.1 Ensure CloudWatch event for snapshot creation failures is created** | MEDIUM | Scanned every 24 hours | Checks for the existence of a CloudWatch event that monitors EBS volume snapshot failures.
 GT1.1 also checks for the EventBridge rule that includes "createSnapshot" and the "failed" result patterns.

This check will be flagged as non-compliant if:
- If "createSnapshot" and the "failed" result patterns are not present.


 |
| **GT1.2 Ensure GuardDuty Alert Rule Check is enabled** | HIGH | Scanned every 24 hours | Checks through all existing EventBridgerule to ensure that monitor GuardDuty alerts are available.
 Ensure the rule pattern contains "aws.guardduty" as the source attribute.


This check will be flagged as non-compliant if:
 - None of the EventBridge rule contains this pattern. |
| **GT1.3 Ensure Subscription to Central GCCI Logs** | HIGH | Scanned every 24 hours | Checks all VPCs in tenant account to ensure at least one VPC Flow Log is created. The VPC Flow Log shall have a subscription filter configured to pipe logs to the tenant's Kinesis Firehose ARN.This check will be flagged as non-compliant if:
- VPCs do not have VPC Flow Log created
- VPC Flow Log does not have subscription filterVPC Flow Log's subscription filter is not configured to tenant's Kinesis Firehose ARN
 |
| **GT1.4 Ensure CloudWatch alarms compliance are set in place** | MEDIUM | Scanned every 24 hours | Checks all the running EC2 instances under tenant account and ensure the instances have configured the following CloudWatch alarms:

This check will be flagged as non-compliant if the following alarms are not configured:
- CPU Utilization
- Memory Utilization
- Disk Utilization
 |
| **GT1.5 Ensure SSM Patch Baselines Have Compliance Levels Configured** | HIGH | Scanned every 24 hours | Checks patch baselines present in AWS Systems Manager owned by the account. Has a compliance level mapped to each of the severity levels.

This check is flagged as non-compliant:
- if a severity level in the patch baseline has "Unspecified" compliance level.
 |
| **GT1.6 Ensure following minimal tags to resources are available** | LOW | Scanned every 24 hours | Checks through all VPC tag key and value within the account.

This rule check will be flagged as non-compliant if the VPC does not contain:

 - All three mandatory tag keys and values - If the key and value have incorrect syntax (spelling/capitalisation).

**Key:** type
- **Value:** Intranet
- **Value:** Internet
- **Value:** Mixed
**Key:** gcc:team
- **Value:** gcci
- **Value:** Agency
**Key:** gcc:origin
- **Value:** v1
- **Value:** v2
 |
| **GT1.7 Ensure Intranet VPC with tag 'type:intranet does not have IGW attachments** | HIGH | Scanned during configuration changes | Checks through GEN VPCs (type: intranet) in tenant account to ensure it does not have Internet Gateways (IGW) attachments.
 This check is non-compliant:


- if there is a recorded configuration change that indicates GEN VPC has an IGW attached to a compartment with VPC tag value "type=intranet".
 |
| **GT1.8 Ensure Intranet VPC with tag 'type:intranet' contains GEN CIDR ranges.** | LOW | Scanned every 24 hours | Checks GEN VPCs for their route table configurations.

Intranet VPCs with tag value 'type:intranet' will be non-compliant:- If the intranet VPC is not configured with GEN CIDR of either 10.x or 100.x |
| **GT 2.1 Detects for existing VPC Peering connections with any external organization** | HIGH | Scanned when event matches | Checks through all VPCs in tenant account. This check will be flagged as non-compliant:
- if either the VPC peering connection requester or accepter does not come from GCC Organization.
 |
| **GT 2.2 Detects for existing TGW attachments with any external organization** | HIGH | Scanned when event matches | Checks through all Transit Gateway (TGW) attachments in tenant account.

This check will be flagged as non-compliant:- if either the TGW attachment requester or accepter does not come from GCC Organization. |
| **GT2.3 Detects IAM roles that trust external accounts that are from an external organization** | MEDIUM | Scanned when event matches | Checks through all trusted entities in IAM roles does not come from an external organization. This check will flag if IAM role's trusted entity contains an account that's from an external organization. |
| **GT2.4 Detects IAM roles which have an inline policy that contains the IAM action 'iam:\*'** | HIGH | Scanned when event matches | Checks through all IAM inline policies to ensure it does not contain "iam:\*" action. This check will flag if Inline policies contains the IAM action "iam:\*", which allows all actions under the IAM service. |

## 2.2.Batch 1 & 2 PaC Rules Remediation Steps

If there are any non-compliant PaC findings within the agency account's Security Hub, administrators may refer to the following remediation steps applicable to the PaC rules in section 2.2. For certain PaC rules, examples between a compliant and non-compliant resource are provided (for example, GT1.6 to GT2.4), which allows administrators/users to easily differentiate the resources' compliance status.

Note: PaC **does not** automatically remediate non-compliant resources.

**GT1.1 Ensure Cloudwatch event for snapshot creation failures is created**

To ensure agency account is compliant with GT1.1, create an **EventBridge** rule that detects and alerts administrators of EBS snapshot creation failure.

1. Go to **EventBridge** and \> sSelect **Create rule**

![](RackMultipart20221019-1-6mthxk_html_f0ce197de5f14339.png)

1. Under **Define rule detail** , \> enter _clm-pac-GT1\_1-ebs-snapshot-failure_ **as Name.** : _clm-pac-GT1\_1-ebs-snapshot-failure._
2. \> select **Rule type** : _Rule with an event pattern as_ **Rule type** :

![](RackMultipart20221019-1-6mthxk_html_db502414a8b59a53.png)

1. Under **Build event pattern** \> Select **Event source** : _AWS events or EventBridge partner events_

![](RackMultipart20221019-1-6mthxk_html_80958de78d02c3e1.png)

1. Leave **Sample events** blank

![](RackMultipart20221019-1-6mthxk_html_6bfeb4ed3fe70fe6.png)

1. Under **Event pattern** :
  1. Select **Event source** : _AWS services_
  2. Select **AWS service** : _EC2_
  3. Select **Event type** : _EBS Snapshot Notification_
  4. Select **Specific event(s)** \> **createSnapshot**
  5. Select **Specific result(s)** \> **failed**
  6. Select **Any source**
  7. Select **Any snapshot ID**

Before proceeding further, ensure that the **Event pattern** matches the example provided in the following image.

 ![Shape5](RackMultipart20221019-1-6mthxk_html_8510435db794eaaa.gif)

![](RackMultipart20221019-1-6mthxk_html_c75a192b13ab027c.png)

![](RackMultipart20221019-1-6mthxk_html_6f5e84bec7c43ca2.png)

1. Under **Target 1** :
  1. Select **Target**  **types** : _AWS service_
  2. **Select a target** : _Lambda function_
  3. Select **Function** : _clm-pac-rules-GT1\_1-cloudwatch-for-snapshot-creation-failures_

![](RackMultipart20221019-1-6mthxk_html_cabb9d067b2ebdca.png)

1. Click **Next** \> Skip **Configure tags** \> Click **Next** \> **Create rule**

![](RackMultipart20221019-1-6mthxk_html_f2cedfe480c2ebaf.png)

**GT1.2 Ensure GuardDuty Alert Rule Check is enabled**

To ensure aAgency account is compliant tocompliant with GT1.2, create an EventBridge Rule that checks if GuardDuty alert rule check is enabled in ththe e aAgency account.

1. Go to **EventBridge** \> Select **Create rule**

![](RackMultipart20221019-1-6mthxk_html_f0ce197de5f14339.png)

1. Under **Define rule detail** \> enter **Name** : clm-pac-GT1\_2-guardduty-alert-check \> select **Rule type** : _Rule with an event pattern_

![](RackMultipart20221019-1-6mthxk_html_561a3e57b7a8f808.png)

1. Under **Build event pattern** \> Select **Event source** : _AWS events or EventBridge partner events_

![](RackMultipart20221019-1-6mthxk_html_df3df94b6264edc0.png)

1. Leave **Sample events** blank

![](RackMultipart20221019-1-6mthxk_html_6bfeb4ed3fe70fe6.png)

1. Under **Event pattern** :
  1. Select **Event source** : _AWS services_
  2. Select **AWS service** : _GuardDuty_
  3. Select **Event type** : _GuardDuty Finding_

Before proceeding further, ensure that the **Event pattern** matches the example provided in the following image.

![](RackMultipart20221019-1-6mthxk_html_31af4815ca57df47.png)

![](RackMultipart20221019-1-6mthxk_html_3d5f3738a74b0f8a.png)

1. Under **Target 1** :
  1. Select **Target types** : _AWS service_
  2. **Select a target** : _Lambda function_
  3. Select **Function** : _clm-pac-rules-GT1\_2-enable-GuardDuty-alert-RuleCheck_

![](RackMultipart20221019-1-6mthxk_html_b6df024be39ac8f9.png)

1. Click **Next** \> Skip **Configure tags** \> Click **Next** \> **Create rule**

![](RackMultipart20221019-1-6mthxk_html_f2cedfe480c2ebaf.png)

1.

**GT1.3 Ensure Subscription to Central GCCI Logs**

To ensure aAgency account is compliant tocompliant with GT1.3, create a Kinesis Data Firehose and Subscription Filter in all Cloudwatch Log Groups named 'vpc-flow-log', which streams all logs from aAgency accounts to Central GCCI.

1. Go to **Kinesis Data Firehose** \> Select **Create Delivery stream**

![](RackMultipart20221019-1-6mthxk_html_b5669982696e066.png)

1. Under **Choose source and destination:**

1. Select **Source** : _Direct PUT_
2. Select **Destination** : _Amazon S3_

![](RackMultipart20221019-1-6mthxk_html_d4b0008a90fab758.png)

![](RackMultipart20221019-1-6mthxk_html_98fd3c09652cffce.png)

1. Under **Delivery stream name** \> Enter _clm-central-logging-firehose_

![](RackMultipart20221019-1-6mthxk_html_d58bbf94ea94546a.png)

1. Under **Transform and convert records** :

1. Select **Data transformation** : _Enabled_

![](RackMultipart20221019-1-6mthxk_html_f0be4fe2c8508f08.png)

1. Under **AWS**** Lambda function **\> Click** Browse**

![](RackMultipart20221019-1-6mthxk_html_7ea8f9ef0c54e4cb.png)

1. Search **AWS Lambda functions** : _clm-central-logging-firehose-lambda_ \> Choose this function

![](RackMultipart20221019-1-6mthxk_html_d1bfe1385c3d842e.png)

1. Select **Buffer size** : _3_ MB
2. Select **Buffer interval** : _60_ seconds
3. Select **Record format conversion** : _Disabled_

![](RackMultipart20221019-1-6mthxk_html_f0be4fe2c8508f08.png)

![](RackMultipart20221019-1-6mthxk_html_12c5a7c2be87dee3.png)

1. Under **Destination settings** :

1. Input **S3 bucket** : _s3://clm-all-central-__876385073014_
2. Select **Dynamic partitioning** : _Enabled_

![](RackMultipart20221019-1-6mthxk_html_fa3b9f90cb4c361d.png)

![](RackMultipart20221019-1-6mthxk_html_783640a2774340a4.png)

1. Select **Multi record deaggregation** : _Enabled_
2. Select **Multi record deaggregation type** : _JSON_
3. Select **New line delimiter** : _Disabled_
4. Select **Inline parsing for JSON** : _Disabled_

![](RackMultipart20221019-1-6mthxk_html_67d90c52a13b02fc.png)

1.

![](RackMultipart20221019-1-6mthxk_html_a7fa7c25e808609.png)

1. Input at **S3 bucket prefix** : _AWSLogs/o-csdezrhp47/ __AGENCY\_ACCOUNT\_ID__ /lg/!{partitionKeyFromLambda:logGroup}/ls/!{partitionKeyFromLambda:logStream}/ts/!{timestamp:yyyy/MM/dd/HH}/_

(Note: Replace AGENCY\_ACCOUNT\_ID with the agency account's own ID)

1. Input at **S3 bucket error output prefix** : _AWSLogs/o-csdezrhp47/ __AGENCY\_ACCOUNT\_ID__ /error/!{firehose:error-output-type}/!{timestamp:yyyy/MM/dd/HH}/_

(Note: Replace AGENCY\_ACCOUNT\_ID with the agency account's own ID)

1. Select **Retry duration** : _300_ seconds

![](RackMultipart20221019-1-6mthxk_html_6dfe1c0613f0f62e.png)

1. Under **Backup settings** \> Select **Source record backup in Amazon S3** : _Disabled_ ![](RackMultipart20221019-1-6mthxk_html_44f9f9324d4b4a3a.png)

![](RackMultipart20221019-1-6mthxk_html_1e092f5f5c17ed27.png)

1. Under **Advanced settings** :

  1. Select **Amazon CloudWatch error logging** : _Enabled_
  2. Select **Permissions** : _Choose existing IAM_ _role_
  3. Select **Existing IAM role** : _clm-central-logging-firehose-__role_
  4. Input **Tags** :

    - **Key** : _gcc:__team_
    - **Value** : _gcci_

![](RackMultipart20221019-1-6mthxk_html_3dcaa1078a029ef1.png)

1. Click **Create delivery stream**

![](RackMultipart20221019-1-6mthxk_html_8152f8ca1e363a27.png)

After successful creation of the Kinesis Data Firehose Delivery Stream:

1. Go to **CloudWatch** \> navigate to **Log groups**
2. **Search** at search bar: _vpc-flow-__log_
3. Select the **vpc-flow-log** group

![](RackMultipart20221019-1-6mthxk_html_dfe7287ebfed7b21.png)

1. Click on **Actions** :

1. Click on **Subscription filters**
2. Select **Create Kinesis Firehose subscription filter**

Note: Only enable subscription filter for all _vpc-flow-__log_ groups, do not enable for other log groups

![](RackMultipart20221019-1-6mthxk_html_336a2a3ef269e25c.png)

![](RackMultipart20221019-1-6mthxk_html_682298ffb3787e4d.png)

1. Under **Create**  **Kinesis Firehose**  **subscription filter** :

1. Select **Destination account** : _Current account_
2. Select **Kinesis Firehose**  **delivery stream** : _clm-central-logging-__firehose_

![](RackMultipart20221019-1-6mthxk_html_5a80cde6b2d8be8c.png)

1. Under **Grant permission** :

1. **Select**  **an existing**  **role** : _clm-central-logging-firehose-__role_

![](RackMultipart20221019-1-6mthxk_html_5a80cde6b2d8be8c.png)

![](RackMultipart20221019-1-6mthxk_html_3437eb30d8a6b085.png)

1. Under **Configure log format and filters** :

1. Select **Log format** : _Other_
2. Leave **Subscription filter pattern** _blank_
3. Input **Subscription filter name** : _VPC flow logs to central_ _logging_

![](RackMultipart20221019-1-6mthxk_html_c5de0fae174d5785.png)

1. Under **Test pattern** :

1. **Select log data to test** : _Custom log_ _data_
2. Ignore **Log event messages**

![](RackMultipart20221019-1-6mthxk_html_e0fec8e0f9bb0c64.png)

![](RackMultipart20221019-1-6mthxk_html_19744bac551df411.png)

1. Select **Start streaming**

To ensure that the subscription filter has been setup successfully to the Kinesis Firehose, under the vpc-flow-log group, navigate to **Subscription filters** tab, ensure filter _VPC flow logs to central_ _logging_ is reflected.

![](RackMultipart20221019-1-6mthxk_html_284ff07331209e89.png)

![](RackMultipart20221019-1-6mthxk_html_11ea1ca87833a83d.png)

If the subscription filter is not shown within the log group, the subscription filter setup has failed. Please follow the above steps again to ensure proper configuration.

![](RackMultipart20221019-1-6mthxk_html_46e35ec89227ee27.png)

![](RackMultipart20221019-1-6mthxk_html_c02cf2cb3d4e0023.png)

**GT1.4 Ensure Cloudwatch alarms compliance are set in place**

-Remediation steps not available at the moment-

**GT1.5 Ensure SSM Patch Baselines Have Compliance Levels Configured**

-Remediation steps not available at the moment-

**GT1.6 Ensure following minimal tags to resources are available**

To ensure VPC aAgency account remains compliant tocompliant with GT1.6, all VPC Resources shall contain these tags:

| **Tag Key\*** | **Tag Value** |
| --- | --- |
| Type |
- Intranet
- Internet
- Mixed
 |
| --- | --- |
| gcc:team |
- gcci
- Agency
 |
| gcc:origin |
- v1
- v2
 |

\*All VPC resources shall contain these 3 tag keys with any of the values defined in the above table.

**Example of Compliant VPC:**

All required tag keys with the correct values are present within the VPC

![](RackMultipart20221019-1-6mthxk_html_a8759fdc84af1128.png)

![](RackMultipart20221019-1-6mthxk_html_77c8c9ec9c319ebf.png)

**1**** st **** Example of Non-Compliant non-compliant VPC:**

This VPC resource is not compliant as it does not contain any/all of the required tags.

![](RackMultipart20221019-1-6mthxk_html_9598f10b2be5fdb9.png)

![](RackMultipart20221019-1-6mthxk_html_c63ddc87c0e7a495.png)

**2**** nd **** Example of Non-Compliant non-compliant VPC:**

This VPC resource is not compliant as the gcc:team tag is not present within the resource.

![](RackMultipart20221019-1-6mthxk_html_e8cee627b955a725.png)

![](RackMultipart20221019-1-6mthxk_html_86a2a2d9aa8d08de.png)

**3**** rd **** Example of Non-Compliant non-compliant VPC:**

This VPC resource is not compliant due to syntax errors and wrong values specified within the resource.

![](RackMultipart20221019-1-6mthxk_html_be48a37a83cb1eff.png)

![](RackMultipart20221019-1-6mthxk_html_d775ab6fd7340f27.png)

**GT1.7 Ensure Intranet VPC with tag key "type" and tag value "Intranet", excludes IGW**

To ensure aAgency account is compliant tocompliant with GT1.7, all VPC with Tag 'type:Intranet' shall not be attached to Internet Gateways.

Example of Compliant VPC Internet Gateway Attachment:
 ![](RackMultipart20221019-1-6mthxk_html_53e132fb15d21330.png)

![](RackMultipart20221019-1-6mthxk_html_81e2b238c4f301a6.png)

VPC with tag 'type:Internet' is allowed to have Internet Gateway Attachments:

![](RackMultipart20221019-1-6mthxk_html_896bb8606e490723.png)

![](RackMultipart20221019-1-6mthxk_html_fb529bb3be689fa1.png)

Example of Non-Compliant non-compliant VPC Internet Gateway Attachment:

![Shape6](RackMultipart20221019-1-6mthxk_html_20f473d41a064279.gif) ![](RackMultipart20221019-1-6mthxk_html_481b234b758b91af.png)

![](RackMultipart20221019-1-6mthxk_html_8f48260db0eb27ed.png)

VPC with tag '_type:Intranet'_ is not allowed to have Internet Gateway Attachments:

![](RackMultipart20221019-1-6mthxk_html_2ba5e7e28b1ccb3.png)

![](RackMultipart20221019-1-6mthxk_html_c49b18cfe1b51c80.png)

**GT1.8 Ensure Intranet VPC is tag "type=Intranet" with gen routable CIDR**

To ensure aAgency account is compliant tocompliant with GT1.8, VPCs with tag '_type:Intranet'_ are only permitted to use GEN routable 10.x.x.x (/27, /26, /25) IPv4 CIDR.

VPCs with tag '_type:Intranet'_ that uses Non-GEN routable 100.x (/24, /25, /26, /27) IPv4 CIDR will be flagged as non-compliant.

Example of Compliant VPC tagged as _type:__Intranet_ with GEN routable CIDR:

![](RackMultipart20221019-1-6mthxk_html_b3246ee7d77b1c83.png)

![](RackMultipart20221019-1-6mthxk_html_1528baba544f00db.png)

Example of Non-Compliant non-compliant VPC tagged as '_type:Intranet'_ with Non-GEN routable CIDR:

![](RackMultipart20221019-1-6mthxk_html_f5866f5e8664aaa8.png)

![](RackMultipart20221019-1-6mthxk_html_2bb0933714849884.png)

**GT2.1 Detects for existing VPC Peering Connections with any external organization**

To ensure aAgency account is compliant tocompliant with GT2.1, all VPC peering connection shall be only established within the aAgency account.

Establishing VPC peering connection to other Account IDs will be flagged as non-compliant.

Example of Compliant and Non-Compliant non-compliant VPC peering connection:

![](RackMultipart20221019-1-6mthxk_html_8dcf71da17dc5596.png)

![](RackMultipart20221019-1-6mthxk_html_a98fee949e6a4ac2.png)

In an event where GT2.1 is non-compliant, check through the flagged VPC peering connection and ensure it is peering to another VPC from My account:

![](RackMultipart20221019-1-6mthxk_html_6f0bb92c85eede34.png)

![](RackMultipart20221019-1-6mthxk_html_f243ccc64294b103.png)

**GT2.2 Detects for existing TGW attachments with any external organization**

To ensure aAgency account is compliant tocompliant with GT2.2, VPC transit gateway attachment shall establish peering connection within the aAgency account.

Transit gateway attachment via peering connection to other Account IDs will be deemed as non-compliant.

Example of Compliant VPC transit gateway attachment via peering connection:

![](RackMultipart20221019-1-6mthxk_html_b100bd489b050faa.png)

![](RackMultipart20221019-1-6mthxk_html_59a734233484cc9.png)

Example of Non-Compliant non-compliant VPC transit gateway attachment via peering connection:

![](RackMultipart20221019-1-6mthxk_html_45f215444831760e.png)

![](RackMultipart20221019-1-6mthxk_html_76d08e7001201335.png)

In an event where GT2.2 is non-compliant, check through the flagged transit gateway attachment and ensure the peering connection attachment is set to "My account":

![](RackMultipart20221019-1-6mthxk_html_d7e229e68492af97.png)

![](RackMultipart20221019-1-6mthxk_html_4eacc4b15fd8860c.png)

**GT2.3 Detects IAM roles that trust external accounts that are from an external organization**

To ensure Agency accountTo ensure agency account is compliant tocompliant with GT2.3, all IAM role shall not contain "sts:ExternalId" conditions and external Account IDs within the trust relationship.

Example of a Compliant IAM Role quoting its own aAgency Account ID under 'principal' within trust relationship:

![](RackMultipart20221019-1-6mthxk_html_55df906d0ba9782a.png)

![](RackMultipart20221019-1-6mthxk_html_1869dca0d187d0ff.png)

Example of a Non-Compliant non-compliant IAM Role using external account ID and "ExternalId" conditions within trust relationship:

![](RackMultipart20221019-1-6mthxk_html_67634768e6b0834e.png)

![](RackMultipart20221019-1-6mthxk_html_bae88d158ab2f6e2.png)

**GT2.4 Detects IAM roles which have an inline policy that contains the IAM action 'iam:\*'**

To ensure Agency accountTo ensure agency account is compliant tocompliant with GT2.4, all IAM roles in aAgency account shall not contain any actions allowing all (\*) IAM actions.

Note: IAM roles are allowed to perform multiple IAM actions but are not allowed to perform all IAM actions as part of principles of least privilege security best practices

Example of a Compliant IAM Role using specific IAM action:

![](RackMultipart20221019-1-6mthxk_html_43dbdebdc09da82d.png)

![](RackMultipart20221019-1-6mthxk_html_a9fd7a19b26a239b.png)

Example of a Non-Compliant non-compliant IAM Role using all IAM actions:

![](RackMultipart20221019-1-6mthxk_html_81a9422ba3b29be5.png)

![](RackMultipart20221019-1-6mthxk_html_a5fc9fa713dba0b5.png)

# 3.Compliance Management on Aws Security Hub

If the non-compliant PaC Security Hub findings has been resolved, administrators canhave the option to remove the resolved finding from the dashboard via using alert suppression. Alternatively, if the PaC findings are not applicable to the aAgency account, administrators may also supress those findings that are not required.

## 3.1.Suppressing Alerts

In an event where the aAgency deems certain Security Hub findings as not applicable (_for example,e.g. IAM.6 Hardware MFA shall be enabled for the root user_ - as aAgency accounts does not utilisze hardware MFA), the findings can be supressed via using AWS Security Hub Findings Dashboard on Management Console or through AWS CLI.

3.1.1. To sSuppress PaC findings via using AWS Console:

 ![Shape7](RackMultipart20221019-1-6mthxk_html_e0f68a6081b1859f.gif)
1. Log in to AWS Tenant Account.
2. Go to AWS Security Hub \> Findings . ![Shape8](RackMultipart20221019-1-6mthxk_html_1f6d2919513d9470.gif) ![Shape9](RackMultipart20221019-1-6mthxk_html_1f6d2919513d9470.gif)- \> Select findings (to be suppressed) and \>
- CClick on ' **Workflow status'** \> Select ' **Supressed'**

![](RackMultipart20221019-1-6mthxk_html_f3f1629aef21c97.png)

You have now successfully suppressed the PaC Findings has now been suppressed successfully.

3.1.2. To sSuppress PaC findings via using AWS CLI:

1. On awsapps SSO page \> Select 'Command line or programmatic access' \> Copy and paste AWS Access Key ID, Secret Access Key and Session Token into ~/.aws/credentials file in account administrator's local terminal

![Shape10](RackMultipart20221019-1-6mthxk_html_fa177ece3a9e5bab.gif)

**AWS\_CLI\_PROFILE**

 ![](RackMultipart20221019-1-6mthxk_html_733077051010ac4e.png)

![](RackMultipart20221019-1-6mthxk_html_1e4f65f480be240d.png)

1. Using AWS CLI, provide the target Finding Title to retrieve finding's Id and ProductArn:

| aws securityhub get-findings --filters '{"Title":[{"Value": "_ **FINDING\_TITLE** _","Comparison":"EQUALS"}]}' --profile **AWS\_CLI\_PROFILE** --region ap-southeast-1 |
| --- |

CLI Results Syntax: Copy _ **FINDING\_ID** _ & _ **FINDING\_PRODUCT\_ARN** _ from results \> To be used in Step 3:

![Shape15](RackMultipart20221019-1-6mthxk_html_df08ce17ee18263.gif) ![Shape12](RackMultipart20221019-1-6mthxk_html_1fe1b01e0aae9301.gif) ![Shape14](RackMultipart20221019-1-6mthxk_html_a774aaa6755eea23.gif) ![Shape16](RackMultipart20221019-1-6mthxk_html_586f356401ccd189.gif) ![Shape11](RackMultipart20221019-1-6mthxk_html_597b3604cb0ea31b.gif) ![Shape13](RackMultipart20221019-1-6mthxk_html_5ee56d03b1b677d5.gif)

_ **FINDING\_ID** _

_ **FINDING\_PRODUCT\_ARN** _

 ![](RackMultipart20221019-1-6mthxk_html_23a0500e81da046.png)

![](RackMultipart20221019-1-6mthxk_html_8e926ed53472777e.png)

1. Paste the _ **FINDING\_ID** _ & _ **FINDING\_PRODUCT\_ARN** _ obtained from Step 2 into the following command to suppress PaC findings:

| aws securityhub batch-update-findings --finding-identifiers Id="_ **FINDING\_ID** _",ProductArn="_ **FINDING\_PRODUCT\_ARN** _" --workflow Status="SUPPRESSED" --profile **AWS\_CLI\_PROFILE** --region ap-southeast-1 |
| --- |

![Shape17](RackMultipart20221019-1-6mthxk_html_22e130c39f2dab9a.gif) ![](RackMultipart20221019-1-6mthxk_html_e665e9e6c48fd733.png)

![](RackMultipart20221019-1-6mthxk_html_c056d85c0de63686.png)

Finding is suppressed successfully if the _Id_ and _ProductArn_ is reflected under "ProcessedFindings" in CLI result.

## 3.2.Setup Security Hub alerts to Email/Slack/ServiceNow ITSM

Asides from viewing PaC related alerts on Security Hub, if a resource is non-compliant, PaC detects it and notifies the agency administrators through the preferred channel.

Agency administrators can also receive notifications either via through one or more of the following channels:

- Email: Notifications will be sent through a setup comprising of Simple Notification Service (SNS), EventBridge rule and a Lambda function from agency account to email inbox.

, Slack: Notifications will be sent through SNS and Chatbot from agency account to Slack Channel.

and/or

- ITSM: Notifications will be sent via a CloudFormation Stack Security Hub-ITSM Connector from agency account to ServiceNow instance.
- .

Notifications will be sent to the preferred platforms whenever PaC detects any resources that are non-compliant.

- Email

Notifications will be sent via a setup comprising of Simple Notification Service (SNS), EventBridge rule and a Lambda function from Agency account to email inbox.

- Slack

Notifications will be sent via SNS and Chatbot from Agency account to Slack Channel.

- ServiceNow ITSM

Notifications will be sent via a CloudFormation Stack Security Hub-ITSM Connector from Agency account to ServiceNow instance.

Please refer to Section 6: References for more information.

# 4.Frequently Asked Questions (FAQ)

1. Why is there a SNS topic residing in the us-east-1 region? (Iinstead of ap-southeast-1?)

1. The SNS topic , (clm-pac-forward-iam-events-topics,) was intentionally hosted on the us-east-1 to send event logs of events that took place within that region. Some AWS services such as (e.g. IAM) operates on global endpoint, which is hosted in the us-east-1. The SNS topic is connected to a Lambda function (clm-pac-iam-event-sns-to-EventBridge) that processes and logs all events that have taken place within AWS services hosted on global endpoint regions.

1. Can agencies disassociate their accounts from the security hub?

1. No, agency accounts remain associated to with the security hub.

1. Can administrators disable any of the services used by PaC such as (Security Hub and , Config etc.) used by PaC?

1. Security hub, config and EventBridge must be enabled on agency accounts for PaC to work normallycorrectly.

1. Can administrators manage multiple agency more than one account of their agency s on a centralised security hub dashboard?

1. No, agency administratorsaccounts do not have permission to add accounts into the security hub. This feature is managed by GCCI administrators.

1. Are the services used by PaC such as (e.g. Security Hub and b, Config) used by PaC automatically enabled on agency account?

1. Yes, security hub and config are automatically enabled in new agency accounts.

# 5.Technical Support

If you need help or have additional For assistance/queries regarding AWS Custom PaC rules, please contact:

- GCC Support: [GCC\_Support@tech.gov.sg](mailto:GCC_Support@tech.gov.sg)
- CODEX Enquires: [Ask\_CODEX@tech.gov.sg](mailto:Ask_CODEX@tech.gov.sg)

# 6.References

For more information, please refer to the URLs below:

| **AWS Documentation** | **URL** |
| --- | --- |
| AWS Security Hub
1. Overview
2. Features
3. Cost
4. Integration of Security Hub
5. Security standards and controls
 |
1. [https://aws.amazon.com/security-hub/](https://aws.amazon.com/security-hub/)
2. [https://aws.amazon.com/security-hub/features](https://aws.amazon.com/security-hub/features)
3. [https://aws.amazon.com/security-hub/pricing/](https://aws.amazon.com/security-hub/pricing/)
4. [https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-settingup.html](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-settingup.html)
5. [https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-standards.html](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-standards.html)
 |
| AWS EventBridge
1. Overview
2. Cost
 |
1. [https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html)
2. [https://aws.amazon.com/eventbridge/pricing/](https://aws.amazon.com/eventbridge/pricing/)
 |
| AWS Config
1. Overview
2. Custom Config Lambda Rules
3. Cost
 |
1. [https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config.html](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config.html)
2. [https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config\_develop-rules\_lambda-functions.html](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config_develop-rules_lambda-functions.html)
3. [https://aws.amazon.com/config/pricing/](https://aws.amazon.com/config/pricing/)
 |
| Alert Notification System
1. Email
2. Slack
3. ServiceNow ITSM

 |
1. [https://aws.amazon.com/premiumsupport/knowledge-center/sns-email-notifications-eventbridge/](https://aws.amazon.com/premiumsupport/knowledge-center/sns-email-notifications-eventbridge/)
2. [https://aws.amazon.com/blogs/security/enabling-aws-security-hub-integration-with-aws-chatbot/](https://aws.amazon.com/blogs/security/enabling-aws-security-hub-integration-with-aws-chatbot/)
3. [https://aws.amazon.com/blogs/security/how-to-set-up-two-way-integration-between-aws-security-hub-and-servicenow/](https://aws.amazon.com/blogs/security/how-to-set-up-two-way-integration-between-aws-security-hub-and-servicenow/)
 |
| Export Security Hub Findings to S3 Bucket for Long-Term Storage |
1. [https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-cwe-custom-actions.html](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-cwe-custom-actions.html)
 |

![](RackMultipart20221019-1-6mthxk_html_dfcc82c5dc75645f.png)