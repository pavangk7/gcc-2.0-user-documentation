# Understand GCC billing report

GCC billing report shows the cost incurred by all the cloud accounts linked to your GCC tenant account.

The report displays the following information.

| **Billing report attributes** | **Description** |
| :--- | :--- |
| **Report ID** | Unique id of the GCC billing report generated every month. |
| **Date Generated** | Date the report is generated in YYYY-MM-DD format. |
| **Service Month** | Month for which this billing report is generated. |
| **Tenant Billing Account** | Your tenant billing account name. |
| **Tenant Billing Account ID** | Unique ID for this tenant billing account. |
| **Attention To** | Public officer to whom this report is assigned.<br>While creating the tenant account, the Tenant Manager assigns a public officer to be notified for billing matters. The name of that public officer is displayed here.|
| **Conversion Rate** | Conversion rate as provided by MAS to convert the cost from USD to SGD for the **Service Month**. |
| **CSP Account** | Cloud account ID |
| **CSP Account Alias** | Alias name provided by your agency for this cloud account. |
| **Service Charges** | Service charge of the CSP as displayed on the Bill Details. |
| **EDP Discount (to return to GovTech GCC)** | EDP is the enterprise discount program offered by your CSP. This discount is entrusted to GovTech as this is a part of the SMF you pay to GovTech GCC service. |
| **Support** | Support cost as charged by the cloud service provider. |
| **Marketplace** | Cost as charged by cloud service provider. |
| **SMF (3%)** | This is the Service Management Fee charged by GCC.<br>It is 3% of your total service charge in SGD + EDP Discount that is entrusted to GovTech. |

<kbd>![billing-report-details](images/billing-report-details-new.png)</kbd>

Authorised agency users can [view GCC billing report](#view-your-agency-billing-report). If there is a discrepancy in cloud service utilisation charges, they need to contact their CSP to resolve it.

>**Important**:
> When the discrepancy is resolved, the agency must inform the GCC team via [ITSM](https://itsm.sgnet.gov.sg/sp3) by raising a support request. For more information on how to raise an SR in ITSM, refer to [GCC 2.0 Support](https://docs.developer.tech.gov.sg/docs/gcc-version-2-user-documentation/#/support/raise-an-incident-request).

If a billing report gets updated, its version number gets incremented and is available on the CMP for the authorised users to review.

### Guidelines for CSP cost analysis tool

[Authorised users](#prerequisites) can analyse your cloud service cost using the cost analysis tools provided by your CSP.

In this document, as an example, we explain how to analyse your cloud service usage costs using the [billing and cost explorer tools provided by AWS](#to-use-cost-explorer) and identify any mismatch between our billing report and the actual usage.


> **Note**:
> Refer to [View your agency billing report](#view-your-agency-billing-report).

#### How to use AWS cost explorer

1. [Log in to the Cloud Management Portal](log-in-to-cmp). The **Dashboard** displays the available tenant accounts.
2. Locate the required tenant account and click **Manage**.
<kbd>![choose-tenant-from-dashboard](images/view-billing-report-choose-tenant-account.png)</kbd>
3. Click **Launch console**.

<kbd>![launch-console](images/launch-console.png)</kbd>

> **Note**:
> Alternatively, you can access the AWS console from your AWS cloud account.

4. Go to **AWS Account** to view the available cloud accounts.
5. Choose the required cloud account.

<kbd>![csp-sso](images/csp-sso.png)</kbd>

6. Click **Management console**.

<kbd>![management-console](images/aws-management-console.png)</kbd>

7. In the search box on the navigation bar, enter **Billing**.

<kbd>![billing-service](images/go-to-billing-service.png)</kbd>

8. Choose **Billing** from the list of search results.

<kbd>![billing-service](images/choose-billing-services.png)</kbd>


By default, the console shows the **AWS Billing Dashboard** page. To understand what is displayed on this page, visit [AWS documentation on Billing Dashboard](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/view-billing-dashboard.html).

9. In the navigation pane, choose **Bills**. By default, the current month's bill detail is displayed.

<kbd>![billing-dashboard](images/view-bills.png)</kbd>

10. Select the required month in **Date**. The **Summary** section displays the details for that month.

<kbd>![bill-summary](images/bill-summary.png)</kbd>

10. To view and understand your cost usage pattern based on required filter criteria, click **Cost Explorer** from the navigation pane.

<kbd>![cost-explorer](images/cost-explorer.png)</kbd>

11. Click **Launch Cost Explorer**.

<kbd>![launch-cost-explorer](images/launch-cost-explorer.png)</kbd>

12. On the **AWS Cost Management** page, click **view in Cost Explorer**.

<kbd>![cost-explorer-filters](images/cost-explorer-filters.png)</kbd>

13. Select the required date range and indicate if you want an hourly, daily, or monthly cost breakdown in a graph (line, bar, or stack) for the selected **Group by** filter criterion.

<kbd>![date-range](images/date-range.png)</kbd>

14. Scroll down below to view the same information in a table format.

> **Note**:
>- There are other filters by which you can customise as needed and view the related cost for the selected date range.
>- For more information, visit [AWS documentation on Cost Explorer](https://docs.aws.amazon.com/cost-management/latest/userguide/ce-what-is.html)
