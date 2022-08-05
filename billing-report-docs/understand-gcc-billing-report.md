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

<kbd>![billing-report-details](../images/billing-report-details-new.png)</kbd>

Authorised agency users can [view GCC billing report](#view-your-agency-billing-report). If there is a discrepancy in cloud service utilisation charges, they need to contact their CSP to resolve it.

>**Important**:
> When the discrepancy is resolved, the agency must inform the GCC team via [ITSM](https://itsm.sgnet.gov.sg/sp3) by raising a support request. For more information on how to raise an SR in ITSM, refer to [GCC 2.0 Support](https://docs.developer.tech.gov.sg/docs/gcc-version-2-user-documentation/#/support/raise-an-incident-request).

If a billing report gets updated, its version number gets incremented and is available on the CMP for the authorised users to review.
