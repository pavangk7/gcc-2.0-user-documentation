# AWS GCC 2.0 central logging system

- GCC 2.0 offers a Central Log Repo, allowing agencies to centrally store their security-related logs such as Custom Logs and VPC Flow Logs for archival purposes and comply with the 12 months retention policy.
- The GCC team centrally manages platform logs such as CloudTrail, Config, GuardDuty, Security Hub to store the Central Log Repos.
- Logs are piped to a single Central Log Account, but different S3 buckets based on the log types.

> **Note**:
> Central Log Account refers to the AWS Account and Central Log Repo refers to the storage in that Account.

<kbd>![central-log-architecture-diagram-aws](/gcc-central-logging-system/images/central-log-aws-architecture-diagram-numbered.png)</kbd>



<figcaption align = "center"><b>High-level architecture for AWS GCC 2.0 central logging</b></figcaption>



| Service| Description| Responsibility of |
| --- | ------------- |:-------------|:----: |
| 1 | **CloudTrail logs** | Managed by organisational CloudTrail and piped to central Log S3 bucket.| GovTech |
| 2 | **AWS Config** | Configured to direct export logs to central Log S3 bucket. | GovTech |
| 3 | **GuardDuty** | Managed by a central GuardDuty and configured to export log to central Log S3 bucket.| GovTech |
| 4 | **Security Hub** | Managed by a central Security Hub and configured to direct export log to central Log S3 bucket.| GovTech |
| 5 | **VPC Flow Logs and Custom Logs** | Logs such as workload and application logs are stored in CloudWatch Log group and are piped to Kinesis Firehose using the **Subscription Filter**. | Agency |
| 6 | **Kinesis Data Firehose**| GCC Team provisions this for the tenant accounts. | Agency |
| 7  | **Kinesis Firehose** | Exports the logs to central Log S3 bucket.| Agency |

## Enable subscription filter to pipe custom logs to central log S3 buckets

1.	[Log in to the Cloud Management Portal](log-in-to-cmp). The **Dashboard** displays the available tenant accounts.
2.	Locate the required tenant account and click **Manage**.
3.	Click **Launch console**.
4.	Go to your **AWS Account** and choose the required cloud account.
5.	Click **Management console**.
6.	Open **CloudWatch** console by searching for or selecting **CloudWatch**.
7.	From the navigation pane, choose **Log groups**.
8.	In the list of log groups, choose the name of the log group that you want to pipe to Central Log S3 Buckets.
9.	Go to **Subscription filters** tab and select **Create** > **Create Kinesis Firehose subscription filter**.
<kbd>![create-kfh-subscription-filter-1](/gcc-central-logging-system/images/create-kinesis-firehose-subscription-filter.png)</kbd>
10.	Go to **Choose destination** and do the following:

  a)	Select **Current account** as the **Destination account**.

  b)	Select **clm-central-logging-firehose** as the **Kinesis Firehose delivery stream**.

<kbd>![create-kfh-subscription-filter-2](/gcc-central-logging-system/images/create-kinesis-firehose-subscription-filter-2.png)</kbd>
11.	Go to **Grant permission** and select **central-logging-cloudwatch-firehose-role** as the existing role.
<kbd>![grant-permission](/gcc-central-logging-system/images/grant-permission.png)
12. Enter a **Subscription filter name**.

> **Note**:
> Do not modify other configurations on this page.  

13.	Click **Start streaming**.

## Access central logs piped to central S3 bucket

**Prerequisites**

-  Only users with **Cloud Security Auditor** or equivalent role can access the logs stored in the central S3 bucket. Log in to CMP, ensure your cloud account has a user with this role.

> **Note**:
> Agency can assign the **Cloud Security Auditor** role to the cloud account through CMP. For more information, refer to [Add cloud users](manage-csp-account-users).

**To access central logs piped to central S3 bucket**

1.	[Log in to the Cloud Management Portal](log-in-to-cmp). The **Dashboard** displays the available tenant accounts.
2.	Locate the required tenant account and click **Manage**.
3.	Click **Launch console**.
4.	Go to your **AWS Account** and choose the required cloud account on which you have the **agency_security_operations** role.

> **Note**:
> If you are a **Cloud Security Auditor**, you will be able to access the cloud console using **agency_security_operations** role.

5.	Click **Management console**.
![choose-aws-account](/gcc-central-logging-system/images/choose-aws-account.png)</kbd>
6.	Open **Amazon Kinesis** console by searching for or selecting **Kinesis**.
7.	From the navigation pane, choose **Delivery Streams**.
8.	Select **clm-central-logging-firehose**.
<kbd>![select-clm-central-logging](/gcc-central-logging-system/images/select-clm-central-logging.png)</kbd>
9. On **clm-central-logging-firehose**, choose the **Configuration** tab.
<kbd>![delivery-stream-details](/gcc-central-logging-system/images/delivery-stream-details.png)</kbd>
10.	Under the **Destination settings**, choose the specified S3 bucket link.
<kbd>![destination-settings](/gcc-central-logging-system/images/destination-settings.png)</kbd>
11.	Open o-csdezrhp47/ and search for the required AWS Account ID from the list to access the Logs.
<kbd>![objects](/gcc-central-logging-system/images/objects.png)</kbd>
