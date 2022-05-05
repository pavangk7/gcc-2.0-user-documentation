# Create Tenant Account

Agencies onboarding GCC 2.0 can consolidate and centrally manage all their cloud accounts using the CMP. To do this, agencies need to create tenant account on GCC 2.0.

Public officers who has onboarded to GCC 2.0 requests for a tenant account to be created for their agency on GCC 2.0 and submits this request for the approval of their Chief Information Officer(CIO) or CIO delegate. CIO of the agency gets notified on their organisation email address who then reviews the request and processes it as needed or can delegate this approval process to

**To submit tenant account creation request:**

1. [Log in to the Cloud Management Portal](log-in-to-cmp)

2. In the **Dashboard**, click **Create New Tenant**.

<kbd>![create-tenant-from-dashboard](images/create-tenant-from-dashboard.png)</kbd>

3. Accept the Terms of Use (TOU), Acceptable Use Policy (AUP) and click **Next**.

<kbd>![accept-tou-aup](images/accept-tou-aup.png)</kbd>

4. Specify the required agency details and click **Next**.

<kbd>![create-tenant-acc-agency-details](images/create-tenant-acc-agency-details.png)</kbd>

| <div style="width:290px">Field Name</div>  | Description |
| :------------------------------------------ |:-------------|
| **Tenant Name**      | Human readable alias name for this tenancy     |
| **Parent Agency**     | Name of your agency     |
| **Agency Address** | Official mailing address of your Agency. This is automatically populated based on the specified **Parent Agency** |
| **Agency CIO Email** | Organisation email address of your agency's CIO or the CIO delegate who is authorised to approve the GCC 2.0 tenant request |

6. To assign **Tenant Admin**, go to **Tenant Admin Details** section and choose one the following steps:

      - To assign the role to you, click **Assign To Me**.
      - To assign the role to another user, enter that public officer's TechPass ID in **Email** and full name in **Name**.

<kbd>![create-tenant-assign-roles](images/create-tenant-assign-roles.png)</kbd>

| <div style="width:290px">Field Name</div>  | Description |
| :------------------------------------------ |:-------------|
| **Tenant Manager Details**                  | This section displays the organisation email address, full name and handphone number(if available) of the **Tenant Manager**. By default, the agency officer requesting this tenant account is assigned as the **Tenant Manager**. |
| &nbsp;&nbsp;&nbsp;&nbsp;**Email**                                |   By default, displays the organisation email address of the requestor. You can assign this role to another user by entering the email address of the required public officer provided you first assign the **Tenant Admin** role for yourself. **Tenant Manager**.                                                    |
| &nbsp;&nbsp;&nbsp;&nbsp;**Name**                                    |   Full name of the **Tenant Manager**.                                                       |
| &nbsp;&nbsp;&nbsp;&nbsp;**Mobile Number**   | Contact number of the **Tenant Manager**.                                                    |
| &nbsp;&nbsp;&nbsp;&nbsp;**Assign To Me**                            |   Click this to assign the **Tenant Manager** role to yourself. |
| **Tenant Admin Details**                    |   Displays the organisation email address, full name and handphone number(if available) of the **Tenant Admin**. |
| &nbsp;&nbsp;&nbsp;&nbsp;**Email**                                   |   By default, this field is blank.  Organisation email address of the **Tenant Admin**. |
| &nbsp;&nbsp;&nbsp;&nbsp;**Name**                                    |   Full name of the **Tenant Admin**. |
| &nbsp;&nbsp;&nbsp;&nbsp;**Assign To Me**                            |   Click this to assign the **Tenant Admin** role to another public officer in your agency. |  
| 




> **Notes**
>- Initially, it is mandatory for the requestor to be assigned with at least one of these roles.
>- To assign another member as Tenant Manager, click **Assign to Me** in Tenant Admin Details so that you become the **Tenant Admin** first. Now go to **Tenant Manager Details** section, enter the required public officer's TechPass ID in **Email** and full name in **Name**.
>- You can add additional tenant users after the Tenant Account gets approved.

7. Click **Next**.

<kbd>![create-tenant-assign-roles-next](images/create-tenant-assign-roles-next.png)</kbd>

8. Specify the required details and click **Next**.

| Field Name  | Description |
| ------------- |:-------------:|
| **Billing Account Name**      | Human readable alias name for this billing account. This is to make it easy for the agencies to identify a billing account.    |
| **Agency Department** | Department billed for this tenant account. |
| **Agency Business Unit** | Business Unit billed for this tenant account.|
| **Attention To** | Full name of the public officer who receives the invoice for this tenant account. |
| **Contact Number** | Phone number of the public officer who receives the invoice. |
| **Email Address** | Organisation email address of the public officer who receives the invoice. |
| **Payment Mode (for agencies)** | This is applicable for agencies other than GovTech.<br><ul><li>GIRO to auto debit the billing amount from your agency's designated bank account on the invoice due date.</li><li>PUBBS (Payment Under Block Billing System) to auto debit the billing amount from the account activated on the PUBBS Portal. The billing amount is deducted in two instalments with the first and second instalment dates falling on 15th and 24th of every month, respectively.</li><li>Interbank Transfer to make the payment only after your agency initiates the payment</li> |
| **Cost Centre (for GovTech only)** | Code used by the Finance for internal GovTech inter-department charging/journal entry. |


?> To view the complete list of agency departments and business units, refer to [Vendors@Gov website](https://www.vendors.gov.sg/UsefulReferences/MinStatuaryBoards.aspx)

<kbd>![create-tenant-billing-details](images/create-tenant-billing-details.png)</kbd>

?> **Agency Billing Address** is the official mailing address of your agency and is displayed automatically based on the agency information provided.

9. Verify if the information displayed in this page is correct and click **Submit**.

<kbd>![create-tenant-summary](images/create-tenant-summary.png)</kbd>

The agency's CIO or the CIO delegate receives an email notification for this request.
