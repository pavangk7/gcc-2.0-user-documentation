# FAQs

<details>
<summary style="font-size:20px;font-weight:bold">Why is there a SNS topic residing in the us-east-1 region instead of ap-southeast-1? </summary>

The SNS topic, clm-pac-forward-iam-events-topics, was intentionally hosted on the us-east-1 to send event logs of that region. Some AWS services such as IAM operates on global endpoint, which is hosted in us-east-1. The SNS topic is connected to a Lambda function (clm-pac-iam-event-sns-to-EventBridge) that processes and logs all events that have taken place within AWS services hosted on global endpoint regions.

</details>
     <hr />

<details>
<summary style="font-size:20px;font-weight:bold">Can agencies disassociate their accounts from Security hub?</summary>

No, agency accounts remain associated with Security hub.

</details>
     <hr />

<details>
<summary style="font-size:20px;font-weight:bold">Can administrators disable services used by PaC such as Security hub and Config?</summary>

No. Security hub, Config and EventBridge must be enabled on agency accounts for PaC to work correctly.

</details>
     <hr />

<details>
<summary style="font-size:20px;font-weight:bold">Can administrators manage more than one account of their agency on a centralised Security hub dashboard? </summary>

No, agency administrators do not have permission to add accounts into Security hub. This feature is managed by GCCI administrators.

</details>
     <hr />

<details>
<summary style="font-size:20px;font-weight:bold">Are the services used by PaC such as Security hub and Config automatically enabled on agency account? </summary>

Yes, Security hub and Config are automatically enabled in new agency accounts.
</details>
     <hr />
