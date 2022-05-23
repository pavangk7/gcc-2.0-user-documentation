<!--
# Create cloud compartment
**Prerequisites:** [CSP account](create-csp-account) with [cloud users](manage-csp-account-users).



- [View CSP account users](#view-csp-account-users)
- [Submit request to add cloud users](#submit-request-to-add-cloud-users)
- [Retract add cloud user request](#retract-add-cloud-user-request)
- [Approve or reject add cloud user request](#approve-or-reject-add-cloud-user-request)

If a request is approved, the new users are added to the CSP account and their status changes from **Pending** to **Enabled**.
>- After the cloud users are added to the CSP account, it may take up to one hour to assign all the access rights to a newly created CSP user account. So as a cloud user, if you are facing difficulties to launch your console or portal of your cloud service provider, try again after sometime.

-   Once you have been added as a Cloud Admin to an AWS account, the
    \'Launch console\' option will now appear to you in the Tenant
    Account dashboard

> ![Graphical user interface, text, application Description
> automatically
> generated](media/image27.png){width="6.120138888888889in"
> height="2.548611111111111in"}

-   Click on \'Launch console\'. This will launch the AWS SSO console in
    a new browser window

-   Click on the \'AWS account\' to display a list of all AWS accounts
    you have console access to

> ![Graphical user interface, application Description automatically
> generated](media/image28.png){width="5.669872047244095in"
> height="2.9722222222222223in"}

-   Click on \'Management console\' to launch the AWS Management Console
    in a new browser window

> ![Graphical user interface, application Description automatically
> generated](media/image29.png){width="4.704214785651794in"
> height="4.536111111111111in"}

Verify that your Cloud Admin is able to access and view the AWS Security
Hub dashboard

-   Make sure you have switched to the Asia Pacific (Singapore) region

> ![Graphical user interface, application Description automatically
> generated](media/image30.png){width="5.944715660542432in"
> height="2.8819444444444446in"}

-   Search for the \'Security Hub\' AWS service, and click on
    \'Dashboard\'

> ![A screenshot of a computer Description automatically generated with
> medium confidence](media/image31.png){width="5.008845144356956in"
> height="1.8888888888888888in"}

-   Verify that you are able to view your compliance findings on the AWS
    Security Hub dashboard

> ![Graphical user interface, application Description automatically
> generated](media/image32.png){width="5.333333333333333in"
> height="3.2291666666666665in"}

3.  ## Creating your first AWS compartment (WIP)

    1.  ##### [Submitting your Create Compartment request (WIP)]{.underline}

Any compartments that your system requires to have a connection back to
the Government Enterprise Network (GEN) or Common Services (CS) will
have to be created via CMP.

To submit a Create Compartment request:

-   Log in to CMP to access the Tenant Dashboard either as

    i.  Tenant Admin, or

    ii. Tenant Manager (only if there is more than one Tenant Manager in
        your team)

-   Click on 'Manage' of your Tenant Account

-   Click on 'CSP' to access your list of CSP accounts, and then
    'Manage' on the AWS account you want the compartment to be created

![Graphical user interface, text, application Description automatically
generated](media/image15.png){width="5.956614173228346in"
height="2.2775021872265966in"}

-   Click on the 'Compartments' tab

-   Click on 'Create New'

> ![Graphical user interface, text, application Description
> automatically generated](media/image33.png){width="6.4125in"
> height="2.6944444444444446in"}

-   Enter the Compartment details

![Graphical user interface, application Description automatically
generated](media/image34.png){width="6.386111111111111in"
height="3.6597222222222223in"}

+---------------+------------------------------------------------------+
| **Input       | **Description**                                      |
| Field**       |                                                      |
+===============+======================================================+
| Compartment   | Human-readable name to be assigned to your           |
| Name          | compartment                                          |
+---------------+------------------------------------------------------+
| Compartment   | There are 2 types of compartments                    |
| Type          |                                                      |
|               | -   INTRANET compartment -- For workloads that       |
|               |     require connectivity back to the Government      |
|               |     Enterprise Network (GEN). Intranet compartments  |
|               |     will also be connected to Common Services (CS)   |
|               |     automatically                                    |
|               |                                                      |
|               | -   INTERNET compartment -- For workloads that don't |
|               |     require connectivity back to GEN, but require    |
|               |     connection to Common Services (CS)               |
+---------------+------------------------------------------------------+
| CIDR Range    | Size of CIDR range the compartment should be         |
|               | provisioned with                                     |
|               |                                                      |
|               | Only 2 standard ranges are available - /26 and /25.  |
|               | For larger CIDR ranges, you will need to submit a    |
|               | service request for case by case review              |
+---------------+------------------------------------------------------+

-   Click on 'Next'

-   Select the Tenant Manager(s) that you want to seek approval from.
    Enter any accompanying remarks you'd like to add to the request.

![Graphical user interface, application Description automatically
generated](media/image35.png){width="6.196527777777778in"
height="4.180555555555555in"}

Note that

i.  You may request approval from more than one Tenant Manager, if
    available

ii. Your request will be processed if any of the indicated
    approvers responds to the request

iii. If you are requesting as a Tenant Manager but you are the only
     Tenant Manager for your account, there will no other available
     Tenant Manager to seek approval from and you will not be able to
     proceed

-   Click on 'Next'

-   Review a summary of details to be created for the compartment

![Graphical user interface, application, website Description
automatically generated](media/image36.png){width="6.284722222222222in"
height="5.111111111111111in"}

-   Click on 'Submit' to send your request to your approvers.

-   Your requested compartment will now be in 'Pending' status

> ![Graphical user interface, application Description automatically
> generated](media/image37.png){width="6.7067366579177605in"
> height="3.2222222222222223in"}

After submission, you may view and track the status of your request via
the Approval Dashboard

-   Click on the Notifications icon, and then the 'Approvals' section

-   Filter via 'Pending' and 'Sent' to see all outstanding requests

![Graphical user interface, application Description automatically
generated](media/image38.png){width="5.923611111111111in"
height="3.657642169728784in"}

-   Locate the request you are interested in, and click on 'Go To' to
    view the details of your request

![Graphical user interface, application Description automatically
generated](media/image39.png){width="6.0993055555555555in"
height="4.201388888888889in"}

-   If your request has not been approved or rejected by your Tenant
    Manager yet, you may cancel your request by clicking on 'Retract'

    1.  ##### [Approving the Create Compartment request (WIP)]{.underline}

After submission of the Create Compartment request, your Tenant Manager
will receive an email notification about the request \[WIP -- TBC
later\]

Sample of Create Compartment approval request email:

> \[WIP -- TBC later\]

To approve the request as Tenant Manager:

-   Login to CMP

-   Click on the Notifications icon, and then the 'Approvals' section

-   Filter via 'Pending' and 'Received' to see all outstanding requests
    that you need to approve

![Graphical user interface, application Description automatically
generated](media/image40.png){width="5.95505905511811in"
height="4.541666666666667in"}

-   Locate the request you want to respond to, and click on 'Go To' to
    view the details of the request

> ![Graphical user interface, application Description automatically
> generated](media/image41.png){width="6.152083333333334in"
> height="4.638888888888889in"}

-   Enter any accompanying remarks you'd like to add to the approval
    response

-   Click on 'Accept' or 'Reject'

    1.  ##### [Verifying your created Compartment (WIP)]{.underline}

After the Create Compartment request has been approved by your Tenant
Manager, the requestor Tenant Admin will receive an email notification
about the approval \[WIP -- TBC later\]

Sample email notification of approved Create Compartment request:

\[WIP -- TBC later\]

Verify that your Compartment has been created

\[WIP -- TBC later\]-->
