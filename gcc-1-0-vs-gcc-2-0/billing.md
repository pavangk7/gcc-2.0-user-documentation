# Billing

This section summarises the key differences on the billing feature between GCC 1.0 and GCC 2.0:

- [Account structure](#account-structure)
- [Cloud spend](#cloud-spend)


## Account structure

| GCC 1.0 | GCC 2.0 |
| :-------------: |:-------------:|
| Agency can have multiple tenant accounts, which can have multiple CMP accounts, which can have multiple CSP accounts.|Agency can have multiple tenant accounts, and each account can have multiple CSP account. However, each tenant account can only have 1 billing account.|

## Cloud spend

| GCC 1.0 | GCC 2.0 |
| :-------------: |:-------------:|
| Agency procure GCC services under GCCS Bulk Tender – GVT(T)-18015.|There is no bulk tender for GCC 2.0, the act of tenant creation is covered with the acceptance of TOU and AUP. Please refer to this link. |
|Agency Saving Plans and Reserved Instances cannot be shared across accounts.|Agency Saving Plans and Reserved Instances cannot be shared across accounts. **No Change**.|
|Monthly subscription for AWS Shield Advance Plan is covered by GCC.|Monthly subscription for AWS Shield Advance Plan is covered by GCC. **No Change**.|
|All AWS accounts are enrolled to AWS Enterprise Support Pooled Plan, with dedicated TAM available for USD$10,000 per month.|All AWS accounts are enrolled to AWS Enterprise Support Pooled Plan, with dedicated TAM available for USD$10,000 per month. **No Change**.|
|Agency can access CSP spending details from CMP, Nimbus Stream, and CSP Cost Management Tool.|Agency can access billing report from CMP to view summary spending. [View billing report](https://docs.developer.tech.gov.sg/docs/gcc-version-2-user-documentation/billing-report-docs/view-your-agency-billing-report).<br><br>No Nimbus Stream in GCC 2.0, agency is given access to native tools where spending details can be accessed from respective CSP's cost management tool.|
|GCC invoice include detail service usage and cost, grouped by “Project-Code” and “Environment”.|GCC invoice include only summary cost. **Agency to use CSP Cost Management Tool to further extract usage and cost by “Project-Code” and “Environment”**. <br><br>**(GovTech sites on CasCOM can continue to use cost optimisation tool)**.|
|Agency can set budget amount in CMP, and spending alerts will be triggered based on different threshold from CMP.|**Agency should leverage on CSP Tool to manage budget and alerts**.|
