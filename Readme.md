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

## Challenges Faced

1. **Policies not showing in initiative scope**
   - Initially, custom policy definitions didn’t appear when trying to add them to the initiative.
   - **Reason:** The policy scope and initiative scope were mismatched.

2. **Incorrect use of tag alias**
   - The wrong alias for tags was used in the `require-projectname-tag` policy.
   - Resolved using: `"field": "[concat('tags[', 'ProjectName', ']')]"`

3. **Unexpected deployment failures**
   - Even compliant resources failed due to small mistakes like missing tags or wrong regions.

4. **Policy evaluation delay**
   - Some enforcement didn't happen instantly after assignment.

5. **Uncertainty with initiative parameters**
   - Unsure whether parameters were needed (they weren’t for this lab).

6. **No enforcement until assignment**
   - Learned that policies must be explicitly assigned to enforce rules.

---

## 🧠 Lessons Learned

- Matching scope between **policy** and **initiative** is critical.
- Azure Policy can enforce compliance **before** resource creation — proactively.
- **Initiatives** simplify grouping and managing multiple policies.
- Custom policy creation requires careful use of **Azure resource aliases**.
- Always **test both compliant and non-compliant scenarios**.
- Clear documentation, naming, and structure help maintain governance.

---

## Conclusion

This lab demonstrated how **Azure Policy** can enforce governance automatically.  
It's a powerful tool for securing cloud environments, ensuring compliance, and enabling DevOps teams to maintain control over growing cloud infrastructure — without manual reviews.




