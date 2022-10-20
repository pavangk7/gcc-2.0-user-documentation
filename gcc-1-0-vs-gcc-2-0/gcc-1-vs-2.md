# GCC 1.0 vs GCC 2.0

This article summarises the difference between GCC 1.0 and GCC 2.0 in the following aspects:

- [User devices](#user-devices)
- [Connecting and authentication modes](#connecting-and-authentication-modes)
- [User roles](#user-roles)
- Environment, network and workload
  - Network compartments
  - Network connectivity
- Security operations
  - Security monitoring and logs
  - Account security baseline
- Billing and reporting
  - Account structure
  - Cloud spend
  - GCC reports

## User devices

This sections summarises the difference in user devices compatibility between GCC 1.0 and GCC 2.0.

<!--![user-devices](./images/user-devices.png)-->
**GCC 1.0**

|  Non-SE GSIB |   GMD | GoMax |
| :-------------: |:-------------:|:-------------: |
| Yes | No|  Yes |


**GCC 2.0**

|  Non-SE GSIB |   GMD | GoMax |
| :-------------: |:-------------:|:-------------: |
| Yes| Yes | No|

## Connecting and authentication modes

| GCC 1.0 | GCC 2.0 |
| :-------------: |:-------------:|
| - Cloud ID<br>- GlobalProtect VPN      | - TechPass<br>- Cloudflare WARP client     |

## User roles

| GCC 1.0 | GCC 2.0 |
| :-------------: |:-------------:|
| **Agency Manager**<br><br>- Approver for all service requests<br>- Not allowed to perform any other actions in CMP (i.e. Compartment Request).      | **Tenant Manager**<br><br>- Approver for all requests (i.e. Compartment creation, assignment of tenant roles to user).<br>-  Requestor of the Tenant automatically becomes either the TM or TA.<br>- Allowed to perform actions such as compartment creation and user assignment.<br><br> Note: *Highly recommended to register at least two (2) **Tenant Managers** for each Tenant Account*.    |
| **Agency Admin**<br><br>- Main tenant administrator.<br>- Able to perform actions to administer tenant (i.e. request compartments, raise SRs).<br>- Approver of requests from CMP Cloud Admin. | **Tenant Admin**<br><br>- Main tenant administrator.<br>- Requestor of the Tenant automatically becomes either the TM or TA.<br>- Able to perform all actions to administer tenant (i.e. raise compartment requests, assign tenant users). |
| **CMP Cloud Admin**<br><br>- Assign access to CSP console to CSP Cloud Admins.<br>- CSP Cloud Admin<br>- Administrative access into CSP .accounts web console. | **Cloud Admin**<br><br>- Assign CSP console assess to other users.<br>- Administrative access to CSP Account web console. |
