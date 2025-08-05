# Azure Policy Lab – Cloud Governance

## Course
**CST8919 – DevOps Security and Compliance**  
**Lab Title:** Enforcing Organizational Policies in the Cloud

## Scenario – MapleTech Solutions

MapleTech Solutions as a **Cloud Security Engineer**.  
Developers were deploying resources with:
- Random global regions 
- Missing tags 
- Public IPs exposed to the internet 

Our mission was to bring **cloud governance, security, and compliance** to Azure using **Azure Policy**.

---

## Objectives

-  Create 3 custom Azure Policies
- Group them into a Policy Initiative
- Assign initiative to a Resource Group
- Test enforcement with sample deployments

---

## Policies Implemented

| Policy Name              | Description                                                        | Effect |
|--------------------------|--------------------------------------------------------------------|--------|
| `only-canadacentral`     | Denies resources deployed **outside** `Canada Central`             | Deny   |
| `require-projectname-tag`| Denies resources **without** a `ProjectName` tag                   | Deny   |
| `denypublic-ip`          | Prevents creation of **Public IP addresses**                      | Deny   |

All three were grouped into a single initiative called **`maplesecure-foundation`**.
## Reference Screenshots remaining screen shots in the folder: 
<img width="1401" height="686" alt="image" src="https://github.com/user-attachments/assets/d55892fe-4f91-44f6-97fe-e2be145178ac" />

<img width="1401" height="686" alt="image" src="https://github.com/user-attachments/assets/55e39bce-ed0a-480a-8f9f-9a38f0193b46" />

<img width="1401" height="686" alt="image" src="https://github.com/user-attachments/assets/fcfdd8f3-be28-48bc-975f-b458dd685522" />



---

## Initiative Details

- **Name:** `maplesecure-foundation`  
- **Category:** `Security Compliance`  
- **Definition Location:** Azure for Students subscription  
- **Type:** Custom  
- **Policies Included:** 3 (see above)

---

## Test Cases & Results

| Test Case                                          | Result       | Screenshot |
|---------------------------------------------------|--------------|------------|
| Deploy VM in `East US`                            | ❌ Denied     | ✅ see `/screenshots/test1-eastus-denied.png` |
| Deploy Storage without `ProjectName` tag          | ❌ Denied     | ✅ see `/screenshots/test2-tag-denied.png` |
| Create Public IP address                          | ❌ Denied     | ✅ see `/screenshots/test3-publicip-denied.png` |
| Deploy VM in `Canada Central` with `ProjectName` tag | ✅ Allowed | ✅ see `/screenshots/test4-success-canada-central.png` |

---



