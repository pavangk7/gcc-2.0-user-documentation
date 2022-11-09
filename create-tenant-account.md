# Create tenant account

**What is a tenant account?**

In GCC 2.0, agencies can consolidate and centrally manage their cloud accounts using the GCC 2.0 CMP. To do this, agency has to create a GCC 2.0 tenant account on CMP.

**Who can create a tenant account?**

Public officer.

Topics:

- [Request for a tenant account](#request-for-a-tenant-account)
- [Approve or reject a tenant account](#approve-or-reject-a-tenant-account-creation-request)
- [View tenant accounts](#view-tenant-accounts)

## Request for a tenant account

> **Note**:
> By default, the public officer who requests for the tenant account is the Tenant Manager and has to complete the following steps.

**To request for a tenant account**

1. In the CMP **Dashboard**, click **Create New Tenant**.

<kbd>![create-tenant-from-dashboard](images/create-tenant-from-dashboard.png)</kbd>

2. Accept the Terms of Use (TOU), Acceptable Use Policy (AUP) and click **Next**.

<kbd>![accept-tou-aup](images/accept-tou-aup.png)</kbd>

3. Specify the required **Agency Details** and click **Next**.

| <div style="width:270px">Field Name</div>  | Description |
| :------------------------------------------ |:-------------|
| **Tenant Name**      | Enter a human-readable alias name for this tenancy.     |
| **Parent Agency**     | Select your agency name from the drop-down list.     |
| **Agency Address** | Official mailing address of your Agency. This is automatically displayed based on the selected **Parent Agency**. |
| **Agency CIO Email** | Enter the organisation email address of your CIO or the designated CIO delegate of your agency. <br><br> When you submit the request, this user receives an email for processing the request. |

<kbd>![create-tenant-acc-agency-details](images/create-tenant-acc-agency-details.png)</kbd>

4. Specify **Tenant User Details** and click **Next**.
> **Note:**
> You can assign only one tenant role to a user.

| <div style="width:270px">Field Name</div>  | Description |
| :------------------------------------------ |:-------------|
| **Tenant Manager Details**                  | By default, the public officer requesting this tenant account is assigned as the Tenant Manager. Hence, this section displays the details of the requestor.  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Email**                                |   By default, this field displays the email address registered with TechPass for the requestor.<br><br> Note:  Requestors can assign this role to another user, provided they first assign the Tenant Admin role to themselves. To assign the Tenant Manager role to another user, enter the email address registered with TechPass for the required public officer.                                                   |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Name**                                    |   Displays the full name of the Tenant Manager.                                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Mobile Number**   | Displays the handphone number of the Tenant Manager if available.                                                    |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Assign To Me**                            |   This option is enabled only if the Tenant Manager role is currently assigned to another user. Click this to assign the Tenant Manager role to yourself. |
| **Tenant Admin Details**                    |   This section allows requestor to assign a Tenant Admin for this account. |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Email**                                   |   By default, this field is blank.  To assign this role to a user in your agency, enter the email address registered with TechPass for the required public officer. |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Name**                                    |   Displays the full name of the assigned Tenant Admin. |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Assign To Me**                            |   As a requestor, you can assign the **Tenant Admin** role to yourself by clicking this option. |

<kbd>![create-tenant-assign-roles](images/create-tenant-assign-roles.png)</kbd>

> **Note:**
> You can add other public officers to this account when the tenant account creation request is approved. For more information, refer to [manage additional tenant users](managing-additional-tenant-account-users).

5. Click **Next**.

<kbd>![create-tenant-assign-roles-next](images/create-tenant-assign-roles-next.png)</kbd>

6. Specify the required **Billing Details** and click **Next**.

| <div style="width:270px">Field Name</div>   | Description |
| :------------- |:-------------|
| **Billing Account Name**      | Enter a human-readable alias name for this billing account. This is to make it easy for the agencies to identify their billing account.    |
| **Agency Department** | Select the department to be billed for this tenant account. |
| **Business Unit** | Select the business unit to be billed for this tenant account.|
| **Agency Billing Address** | This is the official mailing address of your agency and is displayed automatically based on the Agency Details provided earlier. |
| **Attention to** | Enter the full name of the public officer who receives the invoice for this tenant account. |
| **Contact Number** | Enter the phone number of the public officer who receives the invoice. |
| **Email Address** | Enter the email address registered with TechPass for the public officer who receives the invoice. |
| **Cost Center**  | This is applicable only for GovTech tenant accounts. Enter the cost center code for your agency. This code is used by the Finance for internal GovTech inter-department charging/journal entry.|
| **Payment Mode (for agencies)** | This is applicable for agencies other than GovTech. Choose one of the following payment modes. <ul><li>GIRO - Choose this to auto debit the billing amount from your agency's designated bank account on the invoice due date.</li><li>PUBBS (Payment Under Block Billing System) - Choose this to auto debit the billing amount from the account activated on the PUBBS Portal. The billing amount is deducted in two instalments with the first and second instalment dates falling on 15th and 24th of every month.</li><li>Interbank Transfer - Choose this to make the payment only after your agency initiates the payment.</li> |

<kbd>![create-tenant-billing-details](images/create-tenant-billing-details.png)</kbd>


> **Note:**
> To view the complete list of agency departments and business units, refer to the [Vendors@Gov website](https://www.vendors.gov.sg/UsefulReferences/MinStatuaryBoards.aspx).

7. Make sure the information displayed on this page is correct and click **Submit**. CIO or the CIO delegate for your agency receives an email notification to process this request.

> **Note:** To edit the details you specified, click the **Back** button on this page.

<kbd>![create-tenant-summary](images/create-tenant-summary.png)</kbd>

> **Note:** After your request to create tenant account is approved, you can [view the tenant account](#view-tenant-account) on CMP.

## Approve or reject a tenant account
When a Tenant Manager submits a request to create a tenant account, the Chief Information Officer(CIO) or the designated CIO delegate of the agency receives an email to process this request via email.

**To approve or reject a tenant account**

1. Open the email that notified you about the new tenant account creation request.
2. Review the submitted request details enclosed in this email.
3. Reply to this email and in the first line of your reply, enter one of the supported response words.

| <div style="width:270px">Approval words</div>  | <div style="width:270px">Rejection words </div>|
| :------------- |:-------------|
| APPROVE | REJECT |
| APPROVED | REJECTED |
| YES | NO |

4. Optionally, in the second line, add your comments.
5. Click **Send**.

If the request is approved, the tenant account is created and listed on the CMP Dashboard. The Tenant Manager who requested this account is notified via email.

## View tenant accounts
Tenant Manager and Tenant Admin can view and manage the tenant account. They can [Manage additional tenant account users](manage-additional-tenant-account-users) for this account.

**To view tenant accounts**
- [Log in to the Cloud Management Portal](log-in-to-cmp). The **Dashboard** displays the available tenant accounts.

<kbd>![view-tenant-account-from-dashboard](images/view-tenant-account-users-01.png)</kbd>
