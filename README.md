# Calling the Power BI REST API with vscode

* [Official Power BI REST API Docs](https://docs.microsoft.com/rest/api/power-bi/)
* [vscode REST Client Extension](https://marketplace.visualstudio.com/items?itemName=humao.rest-client), [0.24.6 version](https://github.com/Huachao/vscode-restclient/issues/698)

## Authentication Methods

### 1. Workspace - Delegated

* Interactive login via browser using [Device Code Flow](https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-device-code)
* Create AAD application
  * Allow "Public client flows"
  * Configure Power BI Service permissions (delegated)

```
Authorization: Bearer {{$aadV2Token scopes:https://analysis.windows.net/powerbi/api/.default clientId:00000000-0000-0000-0000-000000000000}}
```

Use the `new` keyword to force fetching a new access token:

```
Authorization: Bearer {{$aadV2Token new scopes:https://analysis.windows.net/powerbi/api/.default clientId:00000000-0000-0000-0000-000000000000}}
```

### 2. Workspace - Service Principal

* Automated login using service principal credentials
* Service principal needs to be authorized using Power BI Admin Portal: **"Allow service principals to use Power BI APIs"**
* Service principal needs to be granted workspace-level permissions
* Configure service principal credentials
  * `aadV2TenantId`, `aadV2ClientId`, `aadV2ClientSecret`
  * `"aadV2AppUri": "https://analysis.windows.net/powerbi/api"`

```
Authorization: Bearer {{$aadV2Token appOnly}}
```

### 3. Admin - Delegated

* Use any of the API endpoints starting with [/admin](https://docs.microsoft.com/rest/api/power-bi/admin)
* Interactive login via browser using [Device Code Flow](https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-device-code)
* AAD application needs to have `Tenant.ReadWrite.All` (or `Tenant.Read.All`) permission configured and have admin consent granted

```
Authorization: Bearer {{$aadV2Token scopes:https://analysis.windows.net/powerbi/api/.default clientId:00000000-0000-0000-0000-000000000000}}
```

### 4. Admin - Service Principal (read-only)

* Use any of the ***Read-Only*** API endpoints starting with [/admin](https://docs.microsoft.com/rest/api/power-bi/admin)
* Service principal needs to be authorized using Power BI Admin Portal: **"Allow service principals to use read-only Power BI APIs"**

```
Authorization: Bearer {{$aadV2Token appOnly}}
```

## Contact

![Twitter Follow](https://img.shields.io/twitter/follow/mthierba)
