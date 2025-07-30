# DeviceCodeGenerator
Quick steps to generate Microsoft device codes for testing purposes.

## Generate a device code
1. Open a command prompt (e.g. Powershell)
2. Run below command:

```
curl -s -X POST `
  -H "Content-Type: application/x-www-form-urlencoded" `
  -d "client_id=93d53678-613d-4013-afc1-62e9e444a0a5&resource=https://graph.microsoft.com/" `
  "https://login.microsoftonline.com/common/oauth2/devicecode?api-version=1.0" | ConvertFrom-Json | ConvertTo-Json -Depth 10
```

3. This results in the generation of a device code by using the Office on the web client ID.
4. After the user authenticates using the device code it gives you an access token scoped for the Microsoft Graph API.
5. Example authentication endpoint: https://microsoft.com/devicelogin

