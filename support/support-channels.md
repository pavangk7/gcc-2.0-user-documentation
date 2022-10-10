# Support

## General queries

| Query Category  | Support Channel |
| ------------- |:-------------|
| For enquiries related to Cloud Adoption Team (CAT) activities      | [Ask_CAT@tech.gov.sg](mailto:Ask_CAT@tech.gov.sg)     |
| For general enquiries related to GCC 2.0 and SG Tech Stack      | [Ask_CODEX@tech.gov.sg](mailto:Ask_CODEX@tech.gov.sg)    |
| Other enquiries      | [Ask GovTech at ITSM Portal](https://itsm.sgnet.gov.sg/sp3?id=askgovtech) from your GSIB device     |

## Service queries

To raise any GCC 2.0 incident or service support requests, agencies need a GCC 2.0 project on ITSM. Refer to [create ITSM project](#create-itsm-project).


| Query category &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 	  | Support channel |
| ------------- |-------------|
| **Create an incident request for the following**:<br><br>- issues with service provisioning or service provisioned via GCC 2.0 CMP<br><br>-  issues in accessing GCC 2.0 CMP<br><br>-   network connectivity issues between GEN and Cloud Service Provider (CSP)<br><br>- issues in centralised logging<br><br>billing issues| <br><br><br><br>Use your GSIB device to create the incident support request from the GC2.0 project on [ITSM](https://itsm.sgnet.gov.sg/sp3). <br><br>For more information, refer to[create an incident support request](https://docs.developer.tech.gov.sg/docs/gcc-version-2-user-documentation/#/supportraisan-incident-request).|
| **Create a service request for the following**:<br><br><br>- Additional or customised CIDR ranges for GCC2.0 compartments<br><br>- DNS service to resolve GCC 2.0 DNS domains from GEN<br><br>- DNS service to resolveWOG DNS from GCC 2.0<br><br>- Create or delete network compartment peering between GCC 2.0 and GCC<br><br>- Delete AWS account<br><br>- Delete GCC managed Intranet(GEN) compartment<br><br>- Delete GCC managed Internet(Non-GEN) compartment<br><br>- Delete migrated type 1,2 or 3 compartments|<br><br><br><br><br><br><br><br><br>Use your GSIB device to create the incident support request from the GCC 2.0 project on [ITSM](https://itsm.sgnet.gov.sg/sp3). <br><br>For more information, refer to [create a service request](https://docs.developer.tech.gov.sg/docs/gcc-version-2-user-documentation/#/support/raise-a-service-request).|
|TechPass issues     | Refer to [TechPass documentation](https://docs.developer.tech.gov.sg/docs/techpauser-guide/) before raising a [support request](https://go.gov.sg/techpass-sr).<br><br>- For account related issues, refer to [Account Management FAQ](https://docs.developer.tech.gov.sg/docs/techpass-usguide/#/support/account)<br><br>- For onboarding and signing in issues, refer to [Problems with Onboarding and Signing In](https://docs.developer.tech.gov.sg/docs/techpass-user-guide/#/supposigninissues).<br><br> If you log a support request with TechPass, we will get back to you within three business days.  |
| SEED issues   | Refer to [SEED FAQs](https://docs.developer.tech.gov.sg/docs/security-suite-fengineering-endpoint-devices/faqs/seed-faqs) before raising a support request. To raise a support request refer to [SEED support channels](https://docs.developer.tech.gov.sg/docs/security-suite-for-engineeriendpoint-devices/#/raise-an-incident-support-request).|


> **Note**: If you have issues with your CSP or their services, create an incident support tickets with your respective CSP.

## Create ITSM project

GCC 2.0 users must have a GCC 2.0 project on ITSM. This is a prerequisite to raise GCC 2.0 incident and service requests.

**Who can create GCC 2.0 project on ITSM?**
- Agency ATFM team
- Agency IT Representative or IT Support team.
- Agency user who has existing GCC 2.0 projects on ITSM can add other users to this project.

<details><summary style="font-size:20px;font-weight:bold">Create ITSM project</summary>

1. Go to [ITSM Portal](https://itsm.sgnet.gov.sg/sp3).

2. Click **Project** >> **New Project**.
3. On the **Create Project Profile** page, specify the required details.

> **Note**:
>- Enter **GCC 2.0 &lt;tenant name&gt;** as the **Project Name**. For example, *GCC 2.0 GovTech*.
>- Select **GCC** as the **Hosting Environment** and **GCC 2.0** as **Support Organisation**.

4. Click **Submit**.

When this project is available on ITSM, GCC 2.0 users in your agency can use it from their GSIB device to log incident and service requests for GCC 2.0. Refer to [GCC 2.0 support](https://docs.developer.tech.gov.sg/docs/overview-of-gcc-version-2/#/support) to know when to use this ITSM project to raise incident and service requests for GCC 2.0.

<hr />
</details>


## Raise an incident support request

<details>
<summary style="font-size:20px;font-weight:bold">To raise an incident support request</summary>

This article guides how to raise an incident support request on ITSM for GCC 2.0.

**Prerequisite**: [ITSM project for GCC 2.0](#create-itsm-project).

1. From your GSIB device, go to [ITSM Portal](https://itsm.sgnet.gov.sg/sp3).
1. Go to **Project** > ***GCC 2.0 &lt;agency name&gt;*** > **Incidents**.

> **Note**
>- If your agency does not have a GCC 2.0 project on ITSM, you will not see the **project** tab. Refer to [Create ITSM project](support/create-itsm-project).

3. In **Active Incidents**, select **Report Incident**.

![raise incident request on ITSM project](../images/raise-incident-request-itsm-project.png)

4. Fill in the incident details and click **Submit**.

<hr />
</details>


## Raise a service support request     

<details>
<summary style="font-size:20px;font-weight:bold">To raise a service request</summary>

This article guides how to raise a service request on ITSM for GCC 2.0.

**Prerequisite**: [ITSM project for GCC 2.0](#create-itsm-project).

1. From your GSIB device, go to [ITSM Portal](https://itsm.sgnet.gov.sg/sp3).
1. Go to **Project** > **Requests**.

![raise service request on ITSM project](../images/itsm-projects-page-for-sr.png)

> **Note**
>- If your agency does not have a GCC 2.0 project on ITSM, you will not see the **project** tab. Refer to [Create ITSM project](support/create-itsm-project).

3. Select **Submit Request** > **GCC** > **GCC 2.0**. List of service requests that are supported currently are listed.

![select service request on ITSM](../images/sr-creation.png)

> **Note**
>- Time required to complete a service request is displayed on the request form.

4. Select the required service request and provide the required details before submitting your service request.


<hr /></details>
