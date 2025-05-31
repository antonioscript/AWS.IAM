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

# AWS Console

## Create a User
</br>

![image](https://github.com/user-attachments/assets/0c41e24e-0020-4882-a526-0ec829d14188)

---

### Details of User

**Click on User**

</br>

![image](https://github.com/user-attachments/assets/9a41e7b9-5444-43b4-947c-26f9653976e4)

</br>

> In this case, as the change password flag has been marked, on the first access of the user he will have to change the password

-----

</br>

Notice in the panel on the Permissions tab, that it has a Directly Attached policy. That is, it is not because it is part of a group but yes, because this policy was linked to it atuomaticamente by default when the user was created

And here’s a very important note: 

> 💡 **Highly** | When we talk about attaching permissions to a user, group or role. We’re talking about **policies**! When someone talks about attaching permissions to a group/user we are talking indirectly about **policies**. 


## Create a Group
</br>

![image](https://github.com/user-attachments/assets/2a7e4a5a-1c1b-490c-8bc0-85e653469bbb)

----

![image](https://github.com/user-attachments/assets/335d51dd-bcab-419e-8094-78d9bb611522)

</br>
> In this case you can already put a user in the group creation or attach that user later. No matter
----

### Details of Group

Here we can see details of the group, such as who is part of the group and what permissions (policies)

</br>

![image](https://github.com/user-attachments/assets/91a5c300-8aa2-43d3-b3a4-b62896edbe93)

-----

![image](https://github.com/user-attachments/assets/614f00af-46f8-4ef7-afa0-ef9883c9df42)


### Attach policy to a group

![image](https://github.com/user-attachments/assets/fdc84c62-b4c0-4a0f-849d-78b1bace9f10)


------

![image](https://github.com/user-attachments/assets/4103837c-35d9-4152-8857-c5a09a693229)


-----

![image](https://github.com/user-attachments/assets/850df1d3-9e46-4c38-93f6-d1dd939d9bb5)

----

### Users in the group


## Policies

### Attach policy to a group

![image](https://github.com/user-attachments/assets/9a4deedb-09a4-4579-b389-deaee98aab8a)

> Notice that the user has policies applied to himself directly and others that are inherited through the group

## Roles


## Permissions






# References
https://www.youtube.com/watch?v=hAk-7ImN6iM
