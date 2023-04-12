## What is Vault?
HashiCorp Vault is an identity-based secrets and encryption management system.A secret is anything that you want to tightly control access to, such as API encryption keys, passwords, and certificates. Vault provides encryption services that are gated by authentication and authorization methods. Using Vault’s UI, CLI, or HTTP API, access to secrets and other sensitive data can be securely stored and managed, tightly controlled (restricted), and auditable.

A modern system requires access to a multitude of secrets, including database credentials, API keys for external services, credentials for service-oriented architecture communication, etc. It can be difficult to understand who is accessing which secrets, especially since this can be platform-specific. Adding on key rolling, secure storage, and detailed audit logs is almost impossible without a custom solution. This is where Vault steps in.

Vault validates and authorizes clients (users, machines, apps) before providing them access to secrets or stored sensitive data.

![Image](Security/Hashicorp-vault/image/Vault-01.png)
![Design Flow1](image/Vault-01.png)
