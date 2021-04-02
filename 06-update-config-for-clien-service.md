Fixing client auth : 

- https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/tree/master/1-Call-MSGraph#variation-daemon-application-using-client-credentials-with-certificates

- https://github.com/Azure-Samples/active-directory-dotnetcore-daemon-v2/issues/107

- Error : 

  ```yaml
  A configuration issue is preventing authentication - check the error message from the server for details. You can modify the configuration in the application registration portal. See https://aka.ms/msal-net-invalid-client for details.  Original exception: AADSTS7000215: Invalid client secret is provided.
  Trace ID: 8c64e4ae-adf3-48a3-bfd8-7fe7bc472f00
  Correlation ID: 51df69dc-4a52-40be-bdec-77a562ccb8e1
  Timestamp: 2021-04-02 10:55:14Z
  
  ```

  

1. Open the `Daemon-Console\appsettings.json` file
1. If you are connecting to a national cloud, change the instance to the correct Azure AD endpoint. [See this reference for a list of Azure AD endpoints.](https://docs.microsoft.com/graph/deployments#app-registration-and-token-service-root-endpoints)
1. Find the app key `Tenant` and replace the existing value with your Azure AD tenant name.
1. Find the app key `ClientId` and replace the existing value with the application ID (clientId) of the `daemon-console-v2` application copied from the Azure portal.
1. Find the app key `ClientSecret` and replace the existing value with the key you saved during the creation of the `daemon-console-v2` app, in the Azure portal.
1. Find the app key `TodoListBaseAddress` and set to `https://localhost:44372`
1. Find the app key `TodoListScope` and replace the existing value with the **App ID URI** of your web API, followed by "/.default".
   - If your tenant did not go through domain verification this would be `api://<web api client id>/.default`
   - If your tenant went through [domain verification](https://docs.microsoft.com/azure/active-directory/develop/howto-configure-publisher-domain) this can be `https://domain/.default`, for instance the scope would be `https://<tenant name>.onmicrosoft.com/<web api client id>/.default` where the `<tenant name>` is the Azure AD tenant name (not the tenant Id) and the `<web api client id>` is the application id (clientId) of the web API created above.
   
```yaml
	"Instance": "https://login.microsoftonline.com/{0}",
	"Tenant": "345cb91a-f138-4ce4-90e0-c3902a912866",
	"ClientId": "a4d814ba-6d10-4b3e-97cc-95ec47d62f3f",
	"ClientSecret": "-l-_aDNvimP96QM2pSN.MWvW6ts-RP9jGi",
	"CertificateName": "[Or instead of client secret: Enter here the name of a certificate (from the user cert store) as registered with your application]",
	"TodoListBaseAddress": "https://localhost:44372",
	"TodoListScope": "api://91af0621-857a-4cda-bf0e-76e9ad9ecb88/.default"
```



```yaml
{
	"Instance": "https://login.microsoftonline.com/{0}",
	"Tenant": "[Enter here the tenantID or domain name for your Azure AD tenant]",
	"ClientId": "[Enter here the ClientId for your application]",
	"ClientSecret": "[Enter here a client secret for your application]",
	"CertificateName": "[Or instead of client secret: Enter here the name of a certificate (from the user cert store) as registered with your application]",
	"TodoListBaseAddress": "https://localhost:44372",
	"TodoListScope": "api://[Enter_client_ID_Of_TodoListService-v2_from_Azure_Portal,_e.g._2ec40e65-ba09-4853-bcde-bcb60029e596]/.default"
}

```

