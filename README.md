# AWS.IAM
This repository provides a focused overview of AWS Identity and Access Management (IAM), including key concepts such as users, groups, roles, policies, and permission management. Ideal for developers and cloud engineers looking to understand and apply IAM securely and effectively.

# AWS IAM (Identity and Access Management) 

A simple and practical guide to understand how IAM works in AWS, using a real-world analogy.
</br>

![Visual Guide](https://github.com/user-attachments/assets/7e150078-0372-4ffc-9189-899602771ad0)

---

## IAM as a Company

### 1. **User** = Employee
- A person with a badge (**login/password** or **access key**).
- Can work alone, but it’s better to add them to a **Group**.
- Can receive permissions directly, but that gets messy.

### 2. **Group** = Department
- A collection of users (e.g., "Developers").
- Policies are attached to the group, and all users inherit those permissions.
- **Recommended best practice**.

### 3. **Role** = Temporary Role or Visitor Badge
- Not tied to any specific person.
- It is **assumed temporarily** by a user, service, or external identity.
- Used by **EC2, Lambda**, etc., to interact with AWS securely. (Services)
- Policies define what the Role can do.

### 4. **Policy** = Access Manual (in JSON)
- A document that defines **permissions** (e.g., "can read/write to S3").
- Types of policies:
  - **AWS Managed**: Prebuilt by AWS
  - **Customer Managed**: Created by you (recommended)
  - **Inline**: Attached directly to a user/group/role (avoid unless really needed)

---

## Who Can Have What?

| Entity    | Can Have Policy? | Recommended?           | Best Practice                                     |
|-----------|------------------|------------------------|---------------------------------------------------|
| **User**  |  Yes           |  Avoid              | Use **Groups** instead of attaching directly      |
| **Group** |  Yes           |  Yes                | Attach reusable policies to the group             |
| **Role**  |  Yes           |  Yes                | Attach policies, then allow EC2/Lambda to assume  |
| **Service**|  No           |  No                 | Services must **assume a Role with permissions**  |

---

## Example 1: Developer Fernanda Needs EC2 and S3

 Correct:
- Create User **Fernanda**
- Create Group **Developers**
- Create Policy that allows EC2 and S3
- Attach Policy to Group
- Add Fernanda to the Group

 Wrong:
- Attach Policy directly to Fernanda

---

## Example 2: EC2 Accessing S3

 Correct:
- Create a **Role** with a Policy for S3 access
- Allow EC2 to assume the Role
- EC2 now inherits those permissions automatically

 Wrong:
- Create an IAM User and paste the access key into the EC2 machine

---

##  Policy Types

| Type                  | Use Case                                 | Reusable? | Recommended?     |
|-----------------------|-------------------------------------------|-----------|------------------|
| AWS Managed           | Prebuilt, quick start                     | Yes    |  Yes           |
| Customer Managed      | Custom, reusable                          |  Yes    |  **Best Choice**|
| Inline Policy         | One-off, specific use only                |  No     |  Only if needed |

---

##  Final Summary

- **Users**: People with permanent credentials. Avoid direct policies.
- **Groups**: Used to manage permissions for multiple users.  Recommended.
- **Roles**: Used by AWS services or external users. Always have policies.
- **Policies**: JSON documents that define permissions.

---

## References
https://www.youtube.com/watch?v=hAk-7ImN6iM
