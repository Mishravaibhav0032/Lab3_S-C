# Cloud Governance Gone Rogue – Azure Policy Lab

## 📘 Course
CST8919 – DevOps Security and Compliance

## 🎯 Objective
The purpose of this lab is to bring governance, security, and compliance to a cloud-native environment using **Azure Policy**. As a newly hired Cloud Security Engineer at **MapleTech Solutions**, I was tasked with implementing guardrails to:

- Enforce resource deployment only in **Canada Central**
- Ensure every resource has a **ProjectName** tag
- Block the creation of **Public IP Addresses**

## 🧱 Policy Definitions

### 1. Only-CanadaCentral
- **Type**: Custom Policy
- **Effect**: Deny
- **Description**: Blocks resource deployments outside of the `canadacentral` region.
- **Policy Rule Summary**: If a resource is not in `canadacentral`, deny deployment.

### 2. Require-ProjectName-Tag
- **Type**: Custom Policy
- **Effect**: Deny
- **Description**: Requires all resources to include a `ProjectName` tag.
- **Policy Rule Summary**: If tag `ProjectName` does not exist, deny the resource.

### 3. Deny-Public-IP
- **Type**: Custom Policy
- **Effect**: Deny
- **Description**: Prevents creation of any public IP addresses.
- **Policy Rule Summary**: If the resource type is `Microsoft.Network/publicIPAddresses`, deny it.

## 🧩 Policy Initiative: MapleTech Secure Foundation

The above three policies were grouped into a **Policy Initiative** called `MapleTech Secure Foundation`. It was created and then assigned at the **resource group scope** with `Enforcement Mode` set to **Enforce**.

## 🧪 Test Cases and Results

| # | Action | Expected Result | Status |
|---|--------|------------------|--------|
| 1 | Deploy VM in **East US** | ❌ Denied by region policy | ✅ Passed |
| 2 | Deploy Storage Account **without `ProjectName` tag** | ❌ Denied by tag policy | ✅ Passed |
| 3 | Create a **Public IP address** | ❌ Denied by public IP policy | ✅ Passed |
| 4 | Deploy VM in **Canada Central** with `ProjectName` tag | ✅ Allowed | ✅ Passed |

📸 Screenshots are included in the `/screenshots/` folder.

## 📂 Directory Structure

```
/policy-lab/
├── screenshots/
│   ├── vm-eastus-denied.png
│   ├── storage-no-tag-denied.png
│   ├── publicip-denied.png
│   └── vm-canadacentral-tag-success.png
├── policy-definitions/
│   ├── only-canadacentral.json
│   ├── require-projectname-tag.json
│   └── deny-public-ip.json
└── README.md
```

## 🎥 Video Demo
https://drive.google.com/file/d/1SfOFVBPEkGOSNZ-mW7AmEiHVB_8n7592/view?usp=sharing

## 🚧 Challenges Faced

- Azure Policy schema issues due to missing `properties` block during initial definitions
- Mistaken use of `type` instead of `field: "type"` for resource type validation
- Needed to re-create assignments when initiative definitions were updated

## 🎓 Lessons Learned

- All Azure custom policy definitions must include the correct JSON structure, especially the `properties.policyRule`
- Initiatives make policy management scalable and easier to assign in bulk
- Enforcement mode can block non-compliant resources, aiding in compliance and cost control

---

✅ **Lab Completed Successfully**

**Name : -Vaibhav Mishra**

**Student ID :- 041165850**
