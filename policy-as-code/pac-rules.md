# PaC rules

The following section provides the list of PaC rules for AWS and its respective description.

## Custom batch 1&2 PaC rules

| Rule name | Severity level | Frequency | Description |
| --- | --- | --- | --- |
| **GT1.1 Ensure CloudWatch event for snapshot creation failures is created** | MEDIUM | Scanned every 24 hours | Checks for the existence of a CloudWatch event that monitors EBS volume snapshot failures. </br>GT1.1 also checks for the EventBridge rule that includes "createSnapshot" and the "failed" result patterns.</br></br>This check will be flagged as non-compliant if:</br>- "createSnapshot" and the "failed" result patterns are not present.|
| **GT1.2 Ensure GuardDuty alert rule check is enabled** | HIGH | Scanned every 24 hours | Checks through all existing EventBridgerule to ensure that monitor GuardDuty alerts are available. Ensure the rule pattern contains "aws.guardduty" as the source attribute.</br></br>This check will be flagged as non-compliant if:</br>- None of the EventBridge rule contains this pattern. |
| **GT1.3 Ensure subscription to central GCCI Logs** | HIGH | Scanned every 24 hours | Checks all VPCs in tenant account to ensure at least one VPC Flow Log is created. The VPC Flow Log shall have a subscription filter configured to pipe logs to the tenant's Kinesis Firehose ARN.</br></br>This check will be flagged as non-compliant if:</br>- VPCs do not have VPC Flow Log created</br>- VPC Flow Log does not have subscription filterVPC Flow Log's subscription filter is not configured to tenant's Kinesis Firehose ARN.|
| **GT1.4 Ensure CloudWatch alarms compliance are set in place** | MEDIUM | Scanned every 24 hours | Checks all the running EC2 instances under tenant account and ensure the instances have configured the following CloudWatch alarms:</br>- CPU utilization</br>- Memory utilization</br>- Disk utilization</br></br>This check will be flagged as non-compliant if the following alarms are not configured:</br>- CPU utilization</br>- Memory utilization</br>- Disk Utilization |
| **GT1.5 Ensure SSM patch baselines have compliance levels configured** | HIGH | Scanned every 24 hours | Checks patch baselines present in AWS systems manager owned by the account. Has a compliance level mapped to each of the severity levels. </br></br>This check is flagged as non-compliant:</br>- if a severity level in the patch baseline has "Unspecified" compliance level.|
| **GT1.6 Ensure following minimal tags to resources are available** | LOW | Scanned every 24 hours | Checks through all VPC tag key and value within the account.</br></br>This rule check will be flagged as non-compliant if the VPC does not contain:</br> - All three mandatory tag keys and values - If the key and value have incorrect syntax (spelling/capitalisation).</br>**Key:** type</br>- **Value:** Intranet</br>- **Value:** Internet</br>- **Value:** Mixed</br>**Key:** gcc:team</br>- **Value:** gcci</br>- **Value:** Agency</br>**Key:** gcc:origin</br>- **Value:** v1</br>- **Value:** v2 |
| **GT1.7 Ensure intranet VPC with tag type:_intranet_ does not have IGW attachments** | HIGH | Scanned during configuration changes | Checks through GEN VPCs (type: intranet) in tenant account to ensure it does not have Internet Gateways (IGW) attachments. </br></br>This check is non-compliant:</br>- if there is a recorded configuration change that indicates GEN VPC has an IGW attached to a compartment with VPC tag value "type=intranet".</br> |
| **GT1.8 Ensure Intranet VPC with tag type:_intranet_ contains GEN CIDR ranges.** | LOW | Scanned every 24 hours | Checks GEN VPCs for their route table configurations.</br> </br>Intranet VPCs with tag value 'type:intranet' will be non-compliant:</br>- If the intranet VPC is not configured with GEN CIDR of either 10.x or 100.x |
| **GT 2.1 detects for existing VPC peering connections with any external organization** | HIGH | Scanned when event matches | Checks through all VPCs in tenant account. This check will be flagged as non-compliant:</br>- if either the VPC peering connection requester or accepter does not come from GCC organization. |
| **GT 2.2 Detects for existing TGW attachments with any external organization** | HIGH | Scanned when event matches | Checks through all Transit GateWay (TGW) attachments in tenant account.</br></br>This check will be flagged as non-compliant:</br>- if either the TGW attachment requester or accepter does not come from GCC Organization. |
| **GT2.3 Detects IAM roles that trust external accounts that are from an external organization** | MEDIUM | Scanned when event matches | Checks through all trusted entities in IAM roles does not come from an external organization.</br></br>This check will flag if IAM role's trusted entity contains an account that's from an external organization. |
| **GT2.4 Detects IAM roles which have an inline policy that contains the IAM action 'iam:\*'** | HIGH | Scanned when event matches | Checks through all IAM inline policies to ensure it does not contain "iam:\*" action. </br></br>This check will flag if Inline policies contains the IAM action "iam:\*", which allows all actions under the IAM service. |

## Batch 1 & 2 PaC rules remediation steps

If there are any non-compliant PaC findings within the agency account's Security Hub, administrators may refer to the following remediation steps applicable to the PaC rules in section 2.2. For certain PaC rules, examples between a compliant and non-compliant resource are provided (for example, GT1.6 to GT2.4), which allows administrators/users to easily differentiate the resources' compliance status.

> **Note:** PaC **does not** automatically remediate non-compliant resources.

### GT1.1 Ensure CloudWatch event for snapshot creation failures is created

To ensure agency account is compliant with GT1.1, create an **EventBridge** rule that detects and alerts administrators of EBS snapshot creation failure.

1. In **EventBridge**, select **Create rule.**

<kbd><img src="policy-as-code/images/rules.png" alt="drawing" width="100%"/></kbd>

2. In **Define rule detail** , enter _clm-pac-GT1\_1-ebs-snapshot-failure_ as **Name**.

3. Select _Rule with an event pattern as_ **Rule type**.

<kbd><img src="policy-as-code/images/define-rule-detail.png" alt="drawing" width="100%"/></kbd>

4. In **Build event pattern**, select _AWS events or EventBridge partner events_ as **Event source**.

<kbd><img src="policy-as-code/images/build-event-pattern.png" alt="drawing" width="100%"/></kbd>

5. Leave **Sample events** blank.

<kbd><img src="policy-as-code/images/sample-event.png" alt="drawing" width="100%"/></kbd>

6. In **Event pattern**:

  a. Select  _AWS services_ as **Event source**.

  b. Select _EC2_ as **AWS service**.

  c. Select _EBS Snapshot Notification_ as **Event type**.

  d. In **Specific event(s)**, select **createSnapshot**

  e. Select **failed** as **Specific result(s)**.

  f. Select **Any source**.

  g. Select **Any snapshot ID**.

Before proceeding further, ensure that the **Event pattern** matches the example provided in the following image.

<kbd><img src="policy-as-code/images/event-pattern-selection.png" alt="drawing" width="100%"/></kbd>

7. In **Target 1**:

  a. Select _AWS service_ as **target types**.

  b. Select _Lambda function_ in **Select a target**.

  c. Select _clm-pac-rules-GT1\_1-cloudwatch-for-snapshot-creation-failures_ as **Function**.

<kbd><img src="policy-as-code/images/select-target.png" alt="drawing" width="100%"/></kbd>

8. Click **Next** and skip **Configure tags**. Cick **Next** and select **Create rule**.

<kbd><img src="policy-as-code/images/configure-tags.png" alt="drawing" width="100%"/></kbd>

### GT1.2 Ensure GuardDuty alert rule check is enabled

To ensure agency account is compliant with GT1.2, create an EventBridge rule that checks if GuardDuty alert rule check is enabled in the agency account.

1. In **EventBridge**, select **Create rule**.

  <kbd><img src="policy-as-code/images/create-rule.png" alt="drawing" width="100%"/></kbd>

2. In **Define rule detail,** enter _clm-pac-GT1\_2-guardduty-alert-check_ as **Name** and select _Rule with an event pattern_ as **Rule type**.

  <kbd><img src="policy-as-code/images/define-rule-detail-2.png" alt="drawing" width="100%"/></kbd>

3. In **Build event pattern**, select _AWS events or EventBridge partner events_ as  **Event source**.

  <kbd><img src="policy-as-code/images/build-event-pattern-2.png" alt="drawing" width="100%"/></kbd>

4. Leave **Sample events** blank

  <kbd><img src="policy-as-code/images/sample-event-2.png" alt="drawing" width="100%"/></kbd>

5. In **Event pattern**:

  a. Select  _AWS services_ as **Event source**.

  b. Select _GuardDuty_ as **AWS service**.

  c. Select _GuardDuty Finding_ as **Event type**.

  Before proceeding further, ensure that the **Event pattern** matches the example provided in the following image.

  <kbd><img src="policy-as-code/images/event-pattern.png" alt="drawing" width="100%"/></kbd>

6. In **Target 1**:

  a. Select _AWS service_ as **Target types**.

  b. Select _Lambda function_ in **Select a target**.

  c. Select _clm-pac-rules-GT1\_2-enable-GuardDuty-alert-RuleCheck_ as **Function**.

    <kbd><img src="policy-as-code/images/select-target-2.png" alt="drawing" width="100%"/></kbd>

7. Click **Next** and skip **Configure tags**. Click **Next** and select **Create rule**.

  <kbd><img src="policy-as-code/images/config-tags-optional.png" alt="drawing" width="100%"/></kbd>

### GT1.3 Ensure subscription to central GCCI logs

To ensure agency account is compliant with GT1.3, create a Kinesis data firehose and subscription filter in all CloudWatch log groups named _vpc-flow-log_, which streams all logs from agency accounts to Central GCCI.

1. Go to **Kinesis data firehose** and select **Create delivery stream**.

  <kbd><img src="policy-as-code/images/amazon-kinsesis.png" alt="drawing" width="100%"/></kbd>

2. In **Choose source and destination**:

    a. Select _Direct PUT_ as **Source**.

    b. Select _Amazon S3_ as **Destination**.

    <kbd><img src="policy-as-code/images/create-delivery-stream.png" alt="drawing" width="100%"/></kbd>


3. In **Delivery stream name**, enter _clm-central-logging-firehose_.

  <kbd><img src="policy-as-code/images/create-delivery-system-2.png" alt="drawing" width="100%"/></kbd>

4. In **Transform and convert records:**

    a. Select _Enabled_ as **Data transformation**.

    <kbd><img src="policy-as-code/images/transform-convert-goods.png" alt="drawing" width="100%"/></kbd></img>

    b. In **AWS Lambda function**, click **Browse**.

    <kbd><img src="policy-as-code/images/aws-lambda.png" alt="drawing" width="100%"/></kbd></img>

    c. In **AWS Lambda functions**, enter _clm-central-logging-firehose-lambda_ on the search bar and choose the function.

     <kbd><img src="policy-as-code/images/search-lambda.png" alt="drawing" width="100%"/></kbd></img>
     
    d. Enter _3_.mb as **Buffer size**.

    e. Enter _60_ seconds as **Buffer interval**.

    f. Select _Disabled_ as **Record format conversion**.

    <kbd><img src="policy-as-code/images/lambda-setting.png" alt="drawing" width="100%"/></kbd></img>

5. In **Destination settings:**

    a. Enter _s3://clm-all-central-__876385073014_ as **S3 bucket**.

    b. Enable **Dynamic partitioning**.

    <kbd><img src="policy-as-code/images/destination-setting.png" alt="drawing" width="100%"/></kbd></img>

    c. Select _Enabled_ as  **Multi record deaggregation**.

    d. Select _JSON_ as **Multi record deaggregation type**.

    e. Select _Disabled_ as **New line delimiter**.

    f. Select _Disabled_ as **Inline parsing for JSON**.

    <kbd><img src="policy-as-code/images/multi-record.png" alt="drawing" width="100%"/></kbd></img>
    
    g. Enter _AWSLogs/o-csdezrhp47/ _AGENCY\_ACCOUNT\_ID/lg/!{partitionKeyFromLambda:logGroup}/ls/!{partitionKeyFromLambda:logStream}/ts/!{timestamp:yyyy/MM/dd/HH}/_ as **S3 bucket prefix**.
    
    >**Note:** Replace AGENCY\_ACCOUNT\_ID with the agency account's own ID)
    
    h. Enter _AWSLogs/o-csdezrhp47/AGENCY\_ACCOUNT\_ID/error/!{firehose:error-output-type}/!{timestamp:yyyy/MM/dd/HH}/_ as **S3 bucket error output prefix**.
    
    >**Note:** Replace AGENCY\_ACCOUNT\_ID with the agency account's own ID)
    
    i. Select _300_ seconds as **Retry duration**.

    <kbd><img src="policy-as-code/images/s3-prefix.png" alt="drawing" width="100%"/></kbd></img>

6. In **Backup settings**, select _Disabled_ as **Source record backup in Amazon S3**.

  <kbd><img src="policy-as-code/images/backup-settings.png" alt="drawing" width="100%"/></kbd></img>

7. In **Advanced settings:**

  a. Select _Enabled_ as **Amazon CloudWatch error logging**.

  b. Select _Choose existing IAM_ _role_ as **Permissions**.

  c. Select _clm-central-logging-firehose-role_ as **Existing IAM role**.

  d. Enter the following text **Tags:**

    - **Key** : _gcc:team_
    - **Value** : _gcci_

  <kbd><img src="policy-as-code/images/advance-settings.png" alt="drawing" width="100%"/></kbd></img>

8. Click **Create delivery stream**.

After successful creation of the Kinesis data firehose delivery stream:
  1. Click **CloudWatch** and go to **Log groups**.

  2. Enter _vpc-flow-log_ in the **search bar**.
  
  3. Select **vpc-flow-log** as **group**.

    <kbd><img src="policy-as-code/images/log-groups.png" alt="drawing" width="100%"/></kbd></img>

  4. In **Actions:**

    a. Click **Subscription filters**.

    b. Select **Create Kinesis Firehose subscription filter**.

  >**Note:** Only enable subscription filter for all *vpc-flow-log* groups, do not enable for other log groups.

    <kbd><img src="policy-as-code/images/kinesis-filter.png" alt="drawing" width="100%"/></kbd></img>

  5. In **Create Kinesis firehose subscription filter:**

    a. Select _Current account_ as **Destination account**.

    b. Select _clm-central-logging-firehose_ as **Kinesis Firehose delivery stream**.

  <kbd><img src="policy-as-code/images/create-sub-filter.png" alt="drawing" width="100%"/></kbd></img>

  6. In **Grant permission:**
  
  Enter _clm-central-logging-firehose-role_ as **Select an existing role**.

  <kbd><img src="policy-as-code/images/grant-permission.png" alt="drawing" width="100%"/></kbd></img>

  7. In **Configure log format and filters:**

    a. Select _Other_ as **Log format**.

    b. Set **Subscription filter pattern** as empty.

    c. Enter _VPC flow logs to central logging_ as **Subscription filter name**.

    <kbd><img src="policy-as-code/images/log-format-filter.png" alt="drawing" width="100%"/></kbd></img>

  8. In **Test pattern:**

    a. Select _Custom log data_ as **log data to test**.

    b. Ignore **Log event messages**.

    <kbd><img src="policy-as-code/images/test-pattern.png" alt="drawing" width="100%"/></kbd></img>


  9. Select **Start streaming**.

  To ensure that the subscription filter has been setup successfully to the Kinesis Firehose, under the vpc-flow-log group, navigate to **Subscription filters** tab, ensure filter _VPC flow logs to central logging_ is reflected.

  <kbd><img src="policy-as-code/images/vpc-log.png" alt="drawing" width="100%"/></kbd></img>

  If the subscription filter is not shown within the log group, the subscription filter setup has failed. Please follow the above steps again to ensure proper configuration.

  <kbd><img src="policy-as-code/images/vpc-no-filter.png" alt="drawing" width="100%"/></kbd></img>

### GT1.4 Ensure CloudWatch alarms compliance are set in place

Remediation steps not available at the moment.

### GT1.5 Ensure SSM patch baselines have compliance levels configured

Remediation steps not available at the moment.

### GT1.6 Ensure following minimal tags to resources are available

To ensure VPC agency account remains compliant with GT1.6, all VPC Resources shall contain these tags:

| **Tag Key** | **Tag Value** |
| --- | --- |
| Type | - Intranet </br>- Internet</br>- Mixed |
| gcc:team | - gcci</br>- Agency |
| gcc:origin | - v1 </br>- v2 |

> **Note:** All VPC resources shall contain these 3 tag keys with any of the values defined in the above table.

**Example of compliant VPC:**

All required tag keys with the correct values are present within the VPC.

<kbd><img src="policy-as-code/images/tags-vpc.png" alt="drawing" width="100%"/></kbd></img>

**First example of non-compliant VPC:**

This VPC resource is not compliant as it does not contain any/all of the required tags.

<kbd><img src="policy-as-code/images/vpc-non-compliant-1.png" alt="drawing" width="100%"/></kbd></img>

**Second example of non-compliant VPC:**

This VPC resource is not compliant as the _gcc:team_ tag is not present within the resource.

<kbd><img src="policy-as-code/images/vpc-non-compliant-2.png" alt="drawing" width="100%"/></kbd></img>

**Third example of non-compliant VPC:**

This VPC resource is not compliant due to syntax errors and wrong values specified within the resource.

<kbd><img src="policy-as-code/images/vpc-non-compliant-3.png" alt="drawing" width="100%"/></kbd></img>

### GT1.7 Ensure intranet VPC with tag key _type_ and tag value _Intranet_, excludes IGW

To ensure agency account is compliant with GT1.7, all VPC with Tag type:_Intranet_ shall not be attached to internet gateways.

**Example of compliant VPC internet gateway attachment:**

<kbd><img src="policy-as-code/images/internet-gateways.png" alt="drawing" width="100%"/></kbd></img>

VPC with tag type:_Internet_ is allowed to have internet gateway attachments:

<kbd><img src="policy-as-code/images/vpc-internet.png" alt="drawing" width="100%"/></kbd></img>

**Example of non-compliant VPC internet gateway attachment:**

<kbd><img src="policy-as-code/images/vpc-non-compliant-example.png" alt="drawing" width="100%"/></kbd></img>

VPC with tag type:_Intranet_ is not allowed to have internet gateway attachments:

<kbd><img src="policy-as-code/images/vpc-intranet.png" alt="drawing" width="100%"/></kbd></img>

### GT1.8 Ensure intranet VPC is tag type:_Intranet_ with gen routable CIDR

To ensure agency account is compliant with GT1.8, VPCs with tag type:_Intranet_ are only permitted to use GEN routable 10.x.x.x (/27, /26, /25) IPv4 CIDR.

VPCs with tag type:_Intranet_ that uses Non-GEN routable 100.x (/24, /25, /26, /27) IPv4 CIDR will be flagged as non-compliant.

**Example of compliant VPC tagged as type:_Intranet_ with GEN routable CIDR:**

<kbd><img src="policy-as-code/images/compliant-intranet.png" alt="drawing" width="100%"/></kbd></img>

**Example of non-compliant VPC tagged as type:_Intranet_ with Non-GEN routable CIDR:**

<kbd><img src="policy-as-code/images/non-gen.png" alt="drawing" width="100%"/></kbd></img>

### GT2.1 Detects for existing VPC peering connections with any external organization

To ensure agency account is compliant with GT2.1, all VPC peering connection shall be only established within the agency account.

Establishing VPC peering connection to other Account IDs will be flagged as non-compliant.

**Example of compliant and non-compliant VPC peering connection:**

<kbd><img src="policy-as-code/images/non-compliant-peering.png" alt="drawing" width="100%"/></kbd></img>

In an event where GT2.1 is non-compliant, check through the flagged VPC peering connection and ensure it is peering to another VPC from **My account**:

<kbd><img src="policy-as-code/images/create-peering.png" alt="drawing" width="100%"/></kbd></img>

### GT2.2 Detects for existing TGW attachments with any external organization

To ensure agency account is compliant with GT2.2, VPC transit gateway attachment shall establish peering connection within the agency account.

Transit gateway attachment via peering connection to other Account IDs will be deemed as non-compliant.

**Example of compliant VPC transit gateway attachment via peering connection:**

<kbd><img src="policy-as-code/images/compliant-peer.png" alt="drawing" width="100%"/></kbd></img>


**Example of non-compliant VPC transit gateway attachment via peering connection:**

<kbd><img src="policy-as-code/images/non-compliant-peer.png" alt="drawing" width="100%"/></kbd></img>

In an event where GT2.2 is non-compliant, check through the flagged transit gateway attachment and ensure the peering connection attachment is set to **My account**:

<kbd><img src="policy-as-code/images/transit.png" alt="drawing" width="100%"/></kbd></img>

### GT2.3 Detects IAM roles that trust external accounts that are from an external organization

To ensure agency account is compliant with GT2.3, all IAM role shall not contain _sts:ExternalId_ conditions and external Account IDs within the trust relationship.

**Example of a compliant IAM Role quoting its own agency Account ID under _principal_ within trust relationship:**

<kbd><img src="policy-as-code/images/compliant-iam.png" alt="drawing" width="100%"/></kbd></img>

**Example of a non-compliant IAM Role using external account ID and _ExternalId_ conditions within trust relationship:**

<kbd><img src="policy-as-code/images/non-compliant-iam.png" alt="drawing" width="100%"/></kbd></img>


### GT2.4 Detects IAM roles which have an inline policy that contains the IAM action _iam:\*_

To ensure agency account is compliant with GT2.4, all IAM roles in aAgency account shall not contain any actions allowing all (\*) IAM actions.

> **Note:** IAM roles are allowed to perform multiple IAM actions but are not allowed to perform all IAM actions as part of principles of least privilege security best practices

**Example of a compliant IAM Role using specific IAM action:**

<kbd><img src="policy-as-code/images/compliant-iam-role.png" alt="drawing" width="100%"/></kbd></img>

**Example of a non-compliant IAM Role using all IAM actions:**

<kbd><img src="policy-as-code/images/non-compliant-iam-role.png" alt="drawing" width="100%"/></kbd></img>

