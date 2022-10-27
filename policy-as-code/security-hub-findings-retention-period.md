# Security Hub findings retention period

- Findings are **retained for 90 days** and will be automatically removed from the dashboard after 90 days.
- Findings can be exported to S3 buckets for long-term storage:
  - To be configured by the agencies.
  - To export security hub findings to S3 buckets, setup security hub custom action and EventBridge rule. When the agency administrators export the findings to S3 buckets, they need to invoke the custom action manually on the security hub dashboard.
  - For detailed instructions, refer to the additional resources.

**Additional resources:**

- [Overview of Security Hub](https://aws.amazon.com/security-hub/)
- [Security Hub Features](https://aws.amazon.com/security-hub/features)
- [Security Hub Cost](https://aws.amazon.com/security-hub/pricing/)
- [Integration of Security Hub](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-settingup.html)
- [Security Hub standards and control](/C:/Users/gt-senks/AppData/Local/Microsoft/Windows/INetCache/Content.Outlook/D5DEQ5RN/5.%09https:/docs.aws.amazon.com/securityhub/latest/userguide/securityhub-standards.html)
- [Overview of EventBridge](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html)
- [EventBridge Cost](https://aws.amazon.com/eventbridge/pricing/)

> **Note:** For more information, refer to the links provided in Section 6: References.