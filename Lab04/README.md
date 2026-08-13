<img width="2325" height="1283" alt="screenshot 1 - application registration overview" src="https://github.com/user-attachments/assets/d98332a2-3705-47a6-b763-785b16152611" />
# Lab 04 – Application Registration and Role-Based Access

## Objective

The objective of this lab was to explore how Microsoft Entra ID represents and manages applications and how users can be granted application access through role-based assignments.

The lab demonstrates the relationship between an App Registration, its corresponding Enterprise Application (service principal), application roles, and user access assignments.

## Scenario

A custom internal application, `Lab04-IAM-App`, requires controlled access within the organization.

A read-only application role was created so that users who need access to the application can be assigned a defined role rather than receiving unnecessary administrative privileges.

For this scenario, Jarvis Miller, an executive assistant, requires read-only access to the application to support business responsibilities.

## Steps Performed

1. Registered `Lab04-IAM-App` in Microsoft Entra ID as a single-tenant application.
2. Reviewed the application registration and its unique application and object identifiers.
3. Created a custom application role named `Lab Reader` for users requiring read-only access.
4. Located the corresponding Enterprise Application created by Entra ID and reviewed its service principal information.
5. Assigned Jarvis Miller to the Enterprise Application using the `Lab Reader` role.
6. Reviewed the application's Users and Groups assignments to confirm that the role assignment was successfully created.
7. Opened Jarvis Miller's user identity and independently verified that `Lab04-IAM-App` appeared under the user's assigned applications with the `Lab Reader` role.

## Verification

The access assignment was verified from both sides of the identity relationship.

From the Enterprise Application, Jarvis Miller appeared as a directly assigned user with the `Lab Reader` role.

From the user's identity, `Lab04-IAM-App` appeared as an assigned application with the `Lab Reader` role.

This confirmed that the application role assignment had been successfully recorded in Microsoft Entra ID.

## Key Takeaways

This lab helped demonstrate the distinction between an App Registration and an Enterprise Application.

The App Registration represents the application's identity and configuration definition. Microsoft Entra ID also creates a service principal for the application within the tenant, which administrators manage through Enterprise Applications.

Application roles provide a way to define authorization levels for an application. Users or groups can then be assigned those roles through the Enterprise Application.

The lab also reinforced the principle of least privilege by assigning a user a specific read-only application role rather than broader administrative access.

Finally, verifying the assignment from both the application and user perspectives demonstrated the importance of validating access changes rather than assuming that a configuration change was successfully applied.

## Screenshots

### 1. Application Registration Overview

![Application Registration Overview](screenshot%201%20-%20application%20registration%20overview.png)

### 2. Application Role Configuration

![Application Role Configuration](screenshot%202%20-%20application%20role%20configuration.png)

### 3. Enterprise Application Service Principal

![Enterprise Application Service Principal](screenshot%203%20-%20enterprise%20application%20service%20principal.png)

### 4. User Application Role Assignment

![User Application Role Assignment](screenshot%204%20-%20user%20application%20role%20assignment.png)

### 5. User Application Access Verification

![User Application Access Verification](screenshot%205%20-%20user%20application%20access%20verification.png)
