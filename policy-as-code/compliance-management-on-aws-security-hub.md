# Compliance management on AWS Security hub

If the non-compliant PaC Security Hub findings has been resolved, administrators can remove the resolved finding from the dashboard using alert suppression. Alternatively, if the PaC findings are not applicable to the agency account, administrators may also supress those findings that are not required.

## Suppressing alerts

In an event where the agency deems certain Security Hub findings as not applicable (_for example, IAM.6 Hardware MFA shall be enabled for the root user_ - as agency accounts does not utilisze hardware MFA), the findings can be supressed using AWS Security Hub Findings Dashboard on Management Console or through AWS CLI.

### To suppress PaC findings using AWS Console:

  a. Log in to **AWS Tenant Account**.

  b. Click **AWS Security Hub** and select **Findings**.

  c. Select findings to be suppressed.

  d. Click **Workflow status** and select **Supressed**.

  <kbd><img src="policy-as-code/images/supressed.png" alt="drawing" width="100%"/></kbd>

You have now successfully suppressed the PaC Findings.

### To suppress PaC findings via using AWS CLI:

  a. Go to **awsapps SSO** and select **Command line or programmatic access**. Copy and paste **AWS access key ID**, **Secret access key** and **Session token** into _~/.aws/credentials_ file in account administrator's local terminal.

  <kbd><img src="policy-as-code/images/credentials-new.png" alt="drawing" width="100%"/></kbd>

  b. Using **AWS CLI**, provide the target Finding Title to retrieve **finding's ID** and **ProductArn**:

      aws securityhub get-findings --filters '{"Title":[{"Value": "FINDING_TITLE","Comparison":"EQUALS"}]}' --profile AWS_CLI_PROFILE --region ap-southeast-1 

  c. Go to **CLI Results Syntax** and copy _**FINDING\_ID**_ & _**FINDING\_PRODUCT\_ARN**_ from results to be used in the next step.

  <kbd><img src="policy-as-code/images/cli-results.png" alt="drawing" width="100%"/></kbd>


  d. Paste _**FINDING\_ID**_ & _**FINDING\_PRODUCT\_ARN**_ obtained from the previous step into the following command to suppress PaC findings:

    aws securityhub batch-update-findings --finding-identifiers Id="FINDING_ID",ProductArn="_FINDING_PRODUCT_ARN" --workflow Status="SUPPRESSED" --profile AWS_CLI_PROFILE --region ap-southeast-1 

  <kbd><img src="policy-as-code/images/success-supressed.png" alt="drawing" width="100%"/></kbd>


  Finding is suppressed successfully if the _Id_ and _ProductArn_ is reflected on **ProcessedFindings** in **CLI result**.

## Setup Security hub alerts to email/Slack/ServiceNow ITSM

Aside from viewing PaC related alerts on Security Hub, if a resource is non-compliant, PaC detects it and notifies the agency administrators through the preferred channel.

Agency administrators can receive notifications through one or more of the following channels:

- Email: Notifications will be sent through a setup comprising of Simple Notification Service (SNS), EventBridge rule and a Lambda function from agency account to email inbox.

- Slack: Notifications will be sent through SNS and Chatbot from agency account to Slack channel.

- ITSM: Notifications will be sent via a CloudFormation Stack Security Hub-ITSM Connector from agency account to ServiceNow instance.

Refer to [References](/policy-as-code/references.md) for more information.