# Manage tenant account users
**Prerequisites:** [GCC 2.0 tenant account](create-tenant-account).

Tenant Manager and Tenant Admin can manage the tenant account by doing the following tasks:

- [View tenant account users](#view-tenant-account-users)
- [Submit additional tenant account user request](#submit-additional-tenant-account-user-request)
- [Retract additional tenant account user creation request](#retract-additional-tenant-account-user-request)
- [Approve or reject additional tenant account user request](#approve-or-reject-additional-tenant-account-user-request)


## View tenant account users
Tenant Manager and Tenant Admin of the tenant account can view and manage the tenant account users.

**To view and manage tenant account users**:
1. Log in to the [Cloud Management Portal](log-in-to-cmp). The **Dashboard** displays the available tenant accounts.
2. Locate the required tenant account and click **Manage**.
3. Select **Users** to view the list of users.
4. You may do the following:
   - [Submit additional tenant account user request](#submit-additional-tenant-account-user-request).
   - Delete a user from this tenant by clicking the trash icon in that row.

<kbd>![view-users](images/view-users.png)</kbd>   

> **Note:**
>
> User status can be any of the following:
>- Enabled - Request to add the user to this tenant account is approved.
>- Pending - Request to add the user for this tenant is pending to be processed.

## Submit additional tenant account user request

When a tenant account is created, it will have only two users, and they are the Tenant Manager and Tenant Admin. The Tenant Admin and Tenant Manager can add and manage additional users.

> **Note:** Tenant Managers can submit a request to add additional tenant users provided there are more than one Tenant Manager for the account as the request has to be approved by another Tenant Manager.

**To add additional users to a tenant account**

1. [Log in to the Cloud Management Portal](log-in-to-cmp). The **Dashboard** displays the available tenant accounts.
2. Click **Manage** on the tenant account.
<kbd>![view-tenant-account-from-dashboard](images/view-tenant-account-users-01.png)</kbd>
<!--<kbd>![add-additioal-user-manage-account](images/add-additioal-user-manage-account.png)</kbd>-->
3. Go to **Users** and click **Add New Users**.
<kbd>![add-new-user](images/add-new-user.png)</kbd>
4. In the **Add Users** page, specify the required details and click **Next**.

| <div style="width:270px">Field Name</div>  | Description |
| :------------------------------------------ |:-------------|
| **Role**      | Select a role for the cloud user. Possible roles are: <br> - Tenant Admin<br>- Tenant Manager<br>- Tenant Billing Admin. <br><br>Refer to the [Glossary](glossary) to know more about these roles and their responsibilities.  |
| **Email**     | Type the first few characters of the TechPass ID, and select the required TechPass ID from the matching results. <br><br>- You can add users who have an active TechPass account. <br>- If you can't locate user by entering the email address, verify if the user has an active TechPass account. |
| **Name** | Displays the user name based on the TechPass ID selected as **Email**. |
| **Phone Number** | Displays the phone number of the user if available. |
| **Add another user** |  Click this to add another user. |

  <kbd>![add-users](images/add-users-02.png)</kbd>

5. Select at least one Tenant Manager as the approver and if needed, specify additional information in **Remarks**.
6. Click **Next**.
 <kbd>![select-approvers](images/select-approvers-01.png)</kbd>

7. Review the request **Summary** and to change the **Tenant User Details** or the **Approving Party**, click the **Edit** link.

  <kbd>![review-additional-user-request](images/review-additional-user-request.png)</kbd>
8. Click **Submit**. The status of the users requested to be added will be **Pending** until the request is approved.

>- **Note:** Requestor can [cancel or retract an additional user creation request](#retract-additional-tenant-account-user-request) if it is not yet been processed.


## Retract additional tenant account user request
Requestor may retract a request and CMP allows this if the request is yet to be processed. Some of the possible reason for retracting a request are:
- requested approvers are not available
- requestor wants to assign a different approver
- request is no longer valid.

When you retract a request, you may have to provide a reason for retracting the request and the request status changes from **Pending** to **Cancelled** and will be listed under **Notifications** > **Approvals** > **Cancelled**.

**To retract the additional tenant account user request**
1. [Log in to the Cloud Management Portal](log-in-to-cmp).
1. Go to notifications ![notifications-icon](images/notifications-icon.png) > **Approvals**.
<kbd>![go-to-approvals](images/go-to-approvals.png)</kbd>
1. Select **Pending** and then go to the **Sent** tab to view requests submitted by you and pending approval.
<kbd>![filter-sent-and pending approval](images/filter-sent.png)</kbd>
1. Locate the request you want to retract and click **Go To**.
<kbd>![view-request-details-for-retraction](images/retract-additional-user-request.png)</kbd>
1. Verify the request details and click **Retract**.
<kbd>![retract-request](images/retract-request.png)</kbd>

> **Note:**
> You can retract requests that are not yet processed by the approvers.

## Approve or reject additional tenant account user request
When a request to add tenant account users is submitted, the assigned Tenant Manager(s) receive an email notification to process the request.

> **Note:**
> A request is considered to be processed if one of the assigned Tenant Manager approves or rejects the request.

**To approve or reject the additional tenant account user request**

1. [Log in to the Cloud Management Portal](log-in-to-cmp) as **Tenant Manager**.
1. Go to notifications ![notifications-icon](images/notifications-icon.png) > **Approvals**.
<kbd>![go-to-approvals](images/go-to-approvals.png)</kbd>
1. Select **Pending** and then go to the **Received** tab to view requests that are waiting for your approval.
1. Locate the required request for adding users and click **Go To**.
<kbd>![filter-approvals](images/filter-approvals-additional-user-request.png)</kbd>
1. Review the request details and enter your comments in **Approver Comments**.
1. Select **Accept** or **Reject** as needed.
<kbd>![approve-or-reject](images/approve-or-reject.png)</kbd>

  The requestor receives an email notification about the approval or rejection. If a request is approved, the new users get added to the tenant account and their status changes from **Pending** to **Enabled**.

  <kbd>![user-status-after-approval](images/user-status-after-approval.png)</kbd>

**Next steps:**  
- [Create CSP account](create-csp-account)
- [Manage CSP account](manage-csp-account-users)
