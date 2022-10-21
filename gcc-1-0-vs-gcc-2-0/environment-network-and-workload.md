# Environment, network and workload

This section summarises the key differences on the following between GCC 1.0 and GCC 2.0:

- [Network compartments](#network-compartments)
- [Network connectivity](#network-connectivity)


## Network compartments

| GCC 1.0 | GCC 2.0 |
| :-------------: |:-------------:|
| No default VPC available in the agency account.| No default VPC available in the agency account. |
| Agency can provision Type 0 compartment via CMP, with up to **/24 CIDR range by default**. |Type 0 compartment in GCC 1.0 can potentially be mapped to Agency-Managed Compartment in GCC 2.0.<br><br>Agency can access and manage the provisioning of the Internet and Intranet workloads/resources, including the network constructs such as CIDR, Agency TGW, IGW, NGW and VPC peering, in the **Agency-Managed Compartment** through the **CSP console**. |
| Agency can provision Type 1 compartment via CMP, with up to /25 for GEN Routable CIDR, and **/24 CIDR range for non-GEN Routable CIDR**.|Type 1 compartment in GCC 1.0 will be replaced by the Internet (Non-GEN) Compartment and Intranet (GEN) Compartment in GCC 2.0 respectively.<br><br>Agency can manage the provisioning of the **Internet (Non-GEN) Compartment with up to /24 CIDR range**, and **Intranet (GEN) Compartment with up to /25 CIDR range** through the **CMP2.0 portal** respectively.<br><br>As for the rest of the network constructs such as Agency TGW, IGW, NGW and VPC peering, Agency can access and manage these network constructs, where applicable for the respective compartments, through the CSP portal. |
| Agency can provision Type 2 compartment via CMP, with up to **/24 CIDR range**.|Type 2 compartment in GCC 1.0 will be replaced by the Internet (Non-GEN) Compartments in GCC 2.0. <br><br>Agency can manage the provisioning of the **Internet (Non-GEN) Compartment with up to /24 CIDR range** through the **CMP2.0 portal**.<br><br>As for the rest of the network constructs such as Agency TGW, IGW, NGW and VPC peering, Agency can access and manage these network constructs where applicable for the Internet (Non-GEN) Compartment, through the CSP portal. |
| Agency can provision Type 3 compartment via CMP, with up to /25 for GEN Routable CIDR.| Type 3 compartment in GCC 1.0 will be replaced by the Intranet (GEN) Compartments in GCC 2.0. <br><br>Agency can manage the provisioning of the **Intranet (GEN) Compartment with up to /25 CIDR range** through the **CMP2.0 portal**.<br><br>As for the rest of the network constructs such as Agency TGW and VPC peering, Agency can access and manage these network constructs where applicable for the Intranet (GEN) Compartment, through the CSP portal.|
| Agency cannot provision any IPv6 compartments.| It is planned in the roadmap to support IPv6 for Agency-Managed Compartments (Non-GEN) and Internet Compartments (Non-GEN).|

## Network connectivity

| GCC 1.0 | GCC 2.0 |
| :-------------: |:-------------:|
|Agency can create and manage their own TGW via CSP, and submit SR to CMP to share TGW, and create/accept TGW attachments, with accounts in **GCC 1.0** and **GCC 2.0**.| Agency can manage the provisioning of the Agency TGW and VPC peering through the CSP portal in GCC 2.0.|
|Agency can submit SR to CMP to peer network compartments in GCC 1.0 and GCC 2.0 only (exceptions can be granted, case-by-case basis).|For the VPC peering between the compartment in GCC 2.0 and GCC 1.0, Agency will need to raise the SR (under Others) in GCC 1.0 CMP to request for the acceptance of the VPC peering.|
|Agency can create their own VPC Endpoints via CSP, but must submit SR to CMP to accept VPC Endpoint connection requests.|Agency can create and accept their own VPC Endpoints **by themselves via CSP**.|
|Agency must open relevant firewalls (e.g. GPC FW, GDC FW, CLZ FW, etc) to access their GCC Intranet workload.|Agency must open relevant firewalls (e.g. GPC FW, GDC FW, CLZ FW, etc) to access their GCC Intranet workload. **No Change**.|
|Agency can setup DirectConnect from Agency DC to GCC Link Landing Zone (Type 0 + Type 2).|Agency can setup DirectConnect from Agency DC to GCC Link Landing Zone **(Internet Compartment + Internet or Non-Gen Routable Compartment)**. **No Change**.|
|Agency can leverage on Common Services (PIM, EDR, Secrets Management, Vulnerability Management, AMHIPS) for Type 1, 2, 3 Compartments via GCC managed TGW.|Agency can subscribe and access to the resources in Common Services via the CS TGW that is attached to the respective Internet (Non-GEN) Compartment and Intranet (GEN) Compartment.<br><br>Agency is not able to subscribe and access to the resources in Common Services from the Agency-Managed Compartment yet. |
