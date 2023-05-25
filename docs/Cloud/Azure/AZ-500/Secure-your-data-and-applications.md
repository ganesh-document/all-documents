# **AZ-500: Microsoft Certified: Azure Security Engineer Associate**

## **Secure your data and applications**
Application running within Azure access your confidential data need to be locked down. Learn to secure your applications, storage, databases, and key vaults.

This learning path helps prepare you for [Exam AZ-500: Microsoft Azure Security Technologies](https://learn.microsoft.com/en-gb/certifications/exams/az-500/).

1. **Deploy and secure Azure Key Vault**
      - Introduction
      - Explore Azure Key Vault
      - Configure Key Vault access
      - Review a secure Key Vault example
      - Deploy and manage Key Vault certificates
      - Create Key Vault keys
      - Manage customer managed keys
      - Enable Key Vault secrets
      - Configure key rotation
      - Manage Key Vault safety and recovery features
      - Perform Try-This exercises
      - Explore the Azure Hardware Security Module
      - Knowledge check
      - Summary
2. **Configure application security features**
      - Introduction
      - Review the Microsoft identity platform
      - Explore Azure AD application scenarios
      - Register an application with App Registration
      - Configure Microsoft Graph permissions
      - Enable managed identities
      - Azure App Services
      - App Service Environment
      - Azure App Service plan
      - App Service Environment networking
      - Availability Zone Support for App Service Environments
      - App Service Environment Certificates
      - Perform Try-This exercises
      - Knowledge check
      - Summary
3. **Implement storage security**
      - Introduction
      - Define data sovereignty
      - Configure Azure storage access
      - Deploy shared access signatures
      - Manage Azure AD storage authentication
      - Implement storage service encryption
      - Configure blob data retention policies
      - Configure Azure files authentication
      - Enable the secure transfer required​ property
      - Perform Try-This exercises
      - Knowledge check
      - Summary
4. **Configure and manage SQL database security**
      - Introduction
      - Enable SQL database authentication
      - Configure SQL database firewalls
      - Enable and monitor database auditing
      - Implement data discovery and classification
      - Microsoft Defender for SQL
      - Vulnerability assessment for SQL Server
      - SQL Advanced Threat Protection
      - Explore detection of a suspicious event
      - SQL vulnerability assessment express and classic configurations
      - Configure dynamic data masking
      - Implement transparent data encryption
      - Deploy always encrypted​ features
      - Deploy an always encrypted implementation
      - Perform Try-This exercises
      - Knowledge check
      - Summary


# **Explore Azure Key Vault**

Protecting your keys is essential to protecting your identity and data in the cloud.

Azure Key Vault helps safeguard cryptographic keys and secrets that cloud applications and services use. Key Vault streamlines the key management process and enables you to maintain control of keys that access and encrypt your data. Developers can create keys for development and testing in minutes, and then migrate them to production keys. Security administrators can grant (and revoke) permission to keys, as needed.

You can use Key Vault to create multiple secure containers, called vaults. Vaults help reduce the chances of accidental loss of security information by centralizing application secrets storage. Key vaults also control and log the access to anything stored in them.

Azure Key Vault can manage requesting and renewing TLS certificates. It provides features for a robust solution for certificate lifecycle management.

Azure Key Vault helps address the following issues:

   - Secrets management. You can use Azure Key Vault to securely store and tightly control access to tokens, passwords, certificates, API keys, and other secrets.
   - Key management. You use Azure Key Vault as a key management solution, making it easier to create and control the encryption keys used to encrypt your data.
   - Certificate management. Azure Key Vault is also a service that lets you easily provision, manage, and deploy public and private SSL/TLS certificates for use with Azure and your internal connected resources.
   - Store secrets backed by hardware security modules (HSMs). The secrets and keys can be protected either by software, or FIPS 140-2 Level 2 validates HSMs.

Azure Key Vault is designed to support application keys and secrets. Key Vault is not intended as storage for user passwords.

The following table lists security best practices for using Key Vault.

| Best practice                                                              	| Solution                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         	|
|----------------------------------------------------------------------------	|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| Grant access to users, groups, and applications at a specific scope.       	| Use RBAC’s predefined roles. For example, to grant access to a user to manage key vaults, you would assign the predefined role Key Vault Contributor to this user at a specific scope. The scope in this case would be a subscription, a resource group, or just a specific key vault. If the predefined roles don’t fit your needs, you can define your own roles.                                                                                                                                                                                                                                                                                                                                              	|
| Control what users have access to.                                         	| Access to a key vault is controlled through two separate interfaces: management plane, and data plane. The management plane and data plane access controls work independently. Use RBAC to control what users have access to. For example, if you want to grant an application access to use keys in a key vault, you only need to grant data plane access permissions by using key vault access policies, and no management plane access is needed for this application. Conversely, if you want a user to be able to read vault properties and tags but not have any access to keys, secrets, or certificates, you can grant this user read access by using RBAC, and no access to the data plane is required. 	|
| Store certificates in your key vault.                                      	| Azure Resource Manager can securely deploy certificates stored in Azure Key Vault to Azure VMs when the VMs are deployed. By setting appropriate access policies for the key vault, you also control who gets access to your certificate. Another benefit is that you manage all your certificates in one place in Azure Key Vault.                                                                                                                                                                                                                                                                                                                                                                              	|
| Ensure that you can recover a deletion of key vaults or key vault objects. 	| Deletion of key vaults or key vault objects can be either inadvertent or malicious. Enable the soft delete and purge protection features of Key Vault, particularly for keys that are used to encrypt data at rest. Deletion of these keys is equivalent to data loss, so you can recover deleted vaults and vault objects if needed. Practice Key Vault recovery operations on a regular basis.                                                                                                                                                                                                                                                                                                                 	|

**Azure Key Vault is offered in two service tiers—standard and premium**

The main difference between Standard and Premium is that Premium supports HSM-protected keys.

```
Important

If a user has contributor permissions (RBAC) to a key vault management plane, they can grant themselves access to the data plane by setting a key vault access policy. We recommend that you tightly control who has contributor access to your key vaults, to ensure that only authorized persons can access and manage your key vaults, keys, secrets, and certificates.
```