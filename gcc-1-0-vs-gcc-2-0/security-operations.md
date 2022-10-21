# Security operations

This section summarises the key differences in security operations between GCC 1.0 and GCC 2.0.

- [Security monitoring and logs](#security-monitoring-and-logs)
- [Account security baseline](#account-security-baseline)

## Security monitoring and logs

| GCC 1.0 | GCC 2.0 |
| :-------------: |:-------------:|
|Agency can use CASB **(until April 2022)**, Compliance Monitoring (Patch and Compartment), Security Hub and Guard Duty to monitor their security posture.|Agency can use CSP native products (AWS Security Hub, Azure Defender, GCP Security Command Centre - Premium) to monitor their security posture.<br><br>**No CASB and Compliance Monitoring (Patch and Compartment). Additional PaC monitoring (e.g. IM8 compliance) to be provided by CSG CloudSCAPE. No setup work required for agency to install Cloudscape**.|
|Agency Security Hub and GuardDuty will be managed by GCC centrally.|Agency Security Hub and GuardDuty will be managed by GCC centrally. **No change**.|
|Agency must send CSP audit logs, device & system logs, and application logs to GCC1 Central Log Repository.|Agency must send CSP audit logs, device & system logs, and application logs to **GCC2 Central Log Repository**.|
|Agency can access GCC1 Central Log Repository via CSP portal using role switching.|**Agency can access GCC2 Central Log Repository**.|
|Agency can create and manage their own AWS Config rules.|Agency can create and manage their own AWS Config rules.  **No change**.|


## Account security baseline

| GCC 1.0 | GCC 2.0 |
| :-------------: |:-------------:|
|Agency account default setting for new EBS creation is unencrypted, unless explicitly changed.| Agency account default setting for new EBS creation is **encrypted with default AWS key**, unless explicitly changed. **No change to existing EBS**.|
|Agency account default setting for new S3 creation is allow public settings, unless explicitly changed.|Agency account default setting for new S3 creation is **disallow public settings**, unless explicitly changed. **No change to existing S3**.|
|Agency can allow non-GCC org to assume a GCC account role.|Non-GCC org assuming a GCC account role will be **be alerted via PaC Monitoring into Security Hub**.|
|Agency can create IAM users or roles by themselves via CSP, but must have GCC Permission boundary attached.|Agencies can create programmatic IAM Users or custom IAM roles by themselves via CSP without any GCC Permission Boundary.|
|Agency can login to AWS using the root account.|**Agency cannot login to AWS using the root account as the 'root' email ID (because the account's mailbox is not directly accessible by agency).   Any AWS config that require root access will not be available eg. configuring MFA to delete S3 bucket.  Note that 'root' is different from Cloud admin which is still available to agencies.**<br><br>For functionalities that require root access, visit https://docs.aws.amazon.com/general/latest/gr/root-vs-iam.html#aws_tasks-that-require-root |
|Agency must submit SR to CMP to modify Trust Relationships for IAM roles.|Agency can modify Trust Relationships for custom IAM Roles via CSP by themselves.|
|Agency can attach full admin rights to new IAM users, groups or roles.|Agencies **cannot** attach **AdministratorAccess**, **AWSOrganizationsFullAccess** and **IAMFullAccess** policies to any IAM resources. Agencies are recommended to apply or grant least-privilege permissions to perform a task.|
