Sources: 

- Code-  https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/tree/master/2-Call-OwnApi
- Doc - https://docs.microsoft.com/en-us/azure/active-directory/develop/scenario-daemon-overview



# Objective

- Setup two services on local machine 
  - **DemoAuthServer**
  - **DemoAuthClientService**
- Configure AAD to implement following workflow to enable authorizatoin and authentication in **DemoAuthServer**

![Topology](./ReadmeFiles/daemon-with-secret.svg)

### Summary

- ***[Tenant](#create-tenant)***

  > We use the default organization for user account

- ***[App registration for server](01-create-app-reg.md)***

  > Define identity of a service/app and get created client-id (aka application-id)
  >
  > **Application (client) ID :** 91af0621-857a-4cda-bf0e-76e9ad9ecb88
  >
  > **Directory (tenant) ID**: 345cb91a-f138-4ce4-90e0-c3902a912866
  >
  > **Object ID** :6fabe4c3-e574-4bc4-9c20-5fdb39bd99ac

- [***Create a role for server to use for Role Based Access Control (RBAC)***](./02-create-server-role.md)

  > Create a role that can be accesses by applicatoin only (we won't use user roles for now).
  >
  > We will assign access control to roles and then assign these roles to individual services.

- ***[App registration for client](03-create-app-reg-client.md)***

  > **Display name**:DemoAuthClientService
  >
  > **Application (client) ID:** a4d814ba-6d10-4b3e-97cc-95ec47d62f3f
  >
  > **Directory (tenant) ID:** 345cb91a-f138-4ce4-90e0-c3902a912866
  >
  > **Object ID:** 9ad88898-3dcb-4f09-88a9-0217d168d93e

- [***Setup Api Permissions in client***](./04-setup-api-permission-in-client.md)

  > This allows client to request for Oauth token with role created earlier.
  >
  > The Azure admin has to explicitly approve this permission. i.e. app can only request a permission if admin allows it.



<span name="create-tenant"></span>

### Tenant

>  **Represents an organization.** Dedicated instance of Azure AD that an organization or app developer **receives at the beginning of a relationship with Microsoft**.
>
>  No need to create one. You already have a default one created when you signup on azure portal.





<span name=app-reg></span>

