# 1. Policy as Code - Overview

## 1.1. Audience

This playbook is intended for the following agency users:

- Agency Chief Information Security Officer (ACISO)
- Agency Security Incident Response Officer (ASIRO)
- Account administrators.

## 1.2. Key things to take note

- Agency can't modify the _clm-pac_ rules deployed to their agency account.
- Agency can't modify resources used by _clm-pac_ which has a tag key _gcc:team_ and value as _gcci_.
- In addition to _clm-pac_ rules, agency can define and add additional PaC rules to their account .
- Agency can additionally add up to 391 more custom config rules within their accounts.
- In addition to resources used by _clm-pac_, agencies can also add additional tags.

## 1.3. Background

Policy as Code (PaC) custom rule is introduced as part of GCC2.0's enhancement to provide additional security coverage for organisation-specific security requirements. PaC acts a detection service that alerts agency administrators/CISO/SIRO of non-compliant resources and does not perform intrusive actions such as modifying, adding, or deleting any resources.

GCC2.0 adopts a light-touch approach in compliance monitoring to improve security posture while ensuring that the security measures are not overly restrictive.

AWS Security Hub is a Cloud Security Posture Management (CSPM) that checks AWS services and resources against security best practices and aggregates compliance alerts onto the Security Hub Findings dashboard.
Security Hub with AWS config and EventBridge are used in GCC 2.0 as the main PaC toolchain to detect non-compliant settings or resources in the tenant environment.

## 1.4. What does GCC 2.0 PaC cover

The following security standards are available on GCC 2.0:

| **#** | **Standards** | **Is it enabled by default?** | **Can it be disabled?** | **Industry Benchmark/Custom** | **Can it be modified?** |
| --- | --- | --- | --- | --- | --- |
| 1 | CIS AWS Foundations Benchmark | Yes | No | Industry Benchmark | No |
| 2 | AWS Foundational Security Best Practices | Yes | Yes (Depending on agency's requirement) | Industry Benchmark | No |
| 3 | Payment Card Industry Data Security Standard (PCI DSS) | No. </br>Note: Agency may enable it if required) | Yes (Depending on agency's requirement)| Industry Benchmark | No |
| 4 | GovTech PaC rules | Yes | No | Custom | No |


## 1.5. AWS resources utilised for custom PaC rules

| AWS services | AWS resources utilised | Description |
| --- | --- | --- |
| **Lambda** | **PaC Functions** : </br>- clm-pac-rules-**[PaC-Name]**</br></br>**Update PaC severity level** : </br>- clm-modify-sechub-severity-label-lambda | Contains the **custom logic** to determine the compliance of agency resources status with AWS config as evaluation results or AWS Security Hub as Findings. In addition, Lambda also modifies the severity level for custom PaC rules.|
| **Config** | **Custom Config Rules:** </br>- clm-pac-**[PaC-Name]** | Custom Config leverages on Lambda logic evaluation to determine compliance status. Automatically imports AWS Config evaluation results to Security Hub as Findings. | **EventBridge Rule** | **Custom EventBridge Rules** :</br>- clm-event-**[Rule-Name]**</br>- clm-modify-sechub-severity-label-cw-rule | Lambda evaluates the resources to determine compliance status in case of events, such as the creation of new resources or configuration changes that match the patterns predefined in the EventBridge Rule. | **Security Hub** | **N/A** | Displays non-compliant resources or configuration changes in the Findings Dashboard. From this dashboard, agency administrators can perform the necessary remediation to ensure all resources remain compliant. | **SNS (Optional & Agency responsibility)** | **Topic:** </br>- clm-pac-sechubfindings-email | Sends PaC alert notifications to recipients through email, Slack and third-party products. Refer to section 3.2. |

## 1.6. Cost

> **Note:** Prices are in US dollars.

Lambda:

| **No. of Occurrences** | **Cost Calculation** | **Total Cost** |
| --- | --- | --- |
| **5 million requests** | 1 million x 1 region x $0.00 per request</br>(free tier: first 1 million requests)</br>4 million x 1 region x $0.20 per 1 million requests | First 1 million requests: $0.00</br>Next 4 million requests: $0.80 |
| **200,000 compute time</br>(per GB-second)** | 200,000 x 1 region x $0.00 per event (free tier: first 400,000 events) | $0.00 |
|  | Total Lambda cost per month (USD) | $0.80 |


Config Rules:

| **No. of Occurrences** | **Cost Calculation** | **Total Cost** |
| --- | --- | --- |
| **500 rule evaluations** | 500 x 1 region x $0.001 per evaluation (first 100,000 rule evaluations) | $0.50 |
| **350 configuration item change** | 350 x 1 region x $0.003 per configuration item recorded | $1.05 |
|  | Total Config cost per month (USD) | $1.55 |

EventBridge:

| **No. of Occurrences** | **Cost Calculation** | **Total Cost** |
| --- | --- | --- |
| **10 custom events** | 10 x 1 region x $0.00 per check</br>($0 for \< 1 million events, AWS will only start charging if it exceeds 1 million events) | $0.00 |
|  | Total EventBridge cost per month (USD) | Free of charge |

Security Hub:

| **No. of Occurrences** | **Cost Calculation** | **Total Cost** |
| --- | --- | --- |
| **2500 security checks** | 2500 x 1 region x $0.0010 per check</br> (first 100,000 checks tier) | $2.50 |
| **150,000 finding ingestions** | 10000 x 1 region x $0.00 per event</br>(first 10,000 events - free tier)</br>140000 x 1 region x $0.00003 per event (more than 10000 events) | First 10,000 events: $0.00</br>Next 140,000 events: $4.20 |
| | Total Security Hub cost per month (USD) | $6.70 |

Simple Notification Service (SNS)\*:

| **No. of Occurrences** | **Cost Calculation** | **Total Cost** |
| --- | --- | --- |
| **60 email notifications** | 60 x 1 region x $0.00 per notification (free tier: first 1,000 notifications) | $0.00 |
| | Total SNS cost per month (USD) | $0.00 |

*(Optional: Agency responsibility)

> **Note:**
> - For more information, refer to the links provided in Section 6: References
> - Estimated total PaC recurring cost is **approximately 10.00 USD per month**.