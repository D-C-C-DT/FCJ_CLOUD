---
title : "Create VPC"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.1.1 </b> "
---


#### Creating a VPC with Subnets and Associated Resources
1. Go to [VPC service management console](https://console.aws.amazon.com/vpc/home)
   + Click **Your VPC**.
   + Click **Create VPC**.

![VPC](/images/vpc/001-createvpc.png)

2. For **Resources to create**, select **VPC and more** to create a complete VPC environment.

![VPC](/images/vpc/002-createvpc.png)


3. **Name tag auto-generation**:
Allows AWS to automatically assign consistent names to VPC resources.

4. IPv4 CIDR block:
Enter the internal IP address range for your VPC (e.g., 10.0.0.0/16).

5. **IPv6 CIDR block** (optional):
Enable IPv6 if needed, using an address range provided by Amazon.

6. **Tenancy**:

   **Default:** EC2 instances use the default setting – cost-effective.

   **Dedicated:** EC2 instances run on dedicated hardware – used for compliance or special licensing needs.

      💡 Recommendation: Use Default unless you have specific requirements to save costs.

7. **Availability Zones (AZs)**:
Select at least 2 AZs to ensure high availability.

![VPC](/images/vpc/003-createvpc.png)
![VPC](/images/vpc/004-createvpc.png)

9. **Number of subnets:**

      Select the number of public and private subnets.

      Use private subnets for RDS to enhance security.

10. **Security 🔒:**

      Do not place RDS in public subnets.

      Create a NAT Gateway if private subnets need internet access.

11. **NAT Gateway (optional):**

      Create one NAT Gateway per Availability Zone (AZ) to avoid cross-AZ dependencies.

12. **Egress-only Internet Gateway (IPv6 – optional):**

      Used for outbound IPv6 traffic from private subnets.

13. **S3 Gateway Endpoint (optional):**

      Allows internal access to Amazon S3 without going through the public internet.

14. **DNS options**:

      DNS resolution and DNS hostnames are enabled by default – it’s recommended to keep them that way.

15. **Tagging:**

      You can add key–value tag pairs for easier resource management.

19. **Preview architecture:**

      Review the VPC architecture in the Preview section before creation.

20. **Create VPC:**

      Click **“Create VPC”** to provision all the configured resources.

![VPC](/images/vpc/005-createvpc.png)

#### Configuring Public IP Address Assignment for Subnets

To modify the public IP address assignment behavior for a subnet:

1. Open the Amazon VPC console at **https://console.aws.amazon.com/vpc/.**
2. In the navigation pane, choose **Subnets**.
3. Select your subnet and choose **Actions**, then **Edit subnet settings**.

![VPC](/images/vpc/006-createvpc.png)

4. Configure the **Auto-assign public IPv4 address** setting:

      **Checked:** EC2 instances in the subnet will automatically receive a public IPv4 address.

      **Unchecked:** EC2 instances will not receive a public IPv4 address unless explicitly specified during launch.

🔒 **Security Note**: For subnets that host RDS instances, do not enable this setting to avoid accidental public IP assignment.

5. Click **“Save”** to apply the configuration.

![VPC](/images/vpc/007-createvpc.png)

{{% notice warning %}}
⚠️ **Warning**: Default subnets have auto-assign public IPv4 addresses enabled by default. Always verify this setting when using default subnets for database deployments.
{{% /notice %}}