#### Configure the service project

- Open the `TodoList-WebApi\appsettings.json` file

- Find the app key `Domain` and replace the existing value with your Azure AD tenant name.

- Find the app key `TenantId` and replace the existing value with your Azure AD tenant ID.

- Find the app key `ClientId` and replace the existing value with the application ID (clientId) of the `TodoList-webapi-daemon-v2` application copied from the Azure portal.

  ```yaml
  "AzureAd": {
  	# Could be hosted Active directory for based on enterprises
    "Instance": "https://login.microsoftonline.com/",
    
    # Client id from app registration 
    "ClientId": "[Enter the Client Id of the service (Application ID obtained from the Azure portal), e.g. ba74781c2-53c2-442a-97c2-3d60re42f403]",
    
    # Azure AD tenant name.
    "Domain": "[Enter the domain of your tenant, e.g. contoso.onmicrosoft.com]",
    
    "TenantId": "[Enter 'common', or 'organizations' or the Tenant Id (Obtained from the Azure portal. Select 'Endpoints' from the 'App registrations' blade and use the GUID in any of the URLs), e.g. da41245a5-11b3-996c-00a8-4d99re19f292]"
  },
  
  
  ```

  