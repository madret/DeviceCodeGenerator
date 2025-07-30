# DeviceCodeGenerator
Quick steps to generate Microsoft device codes for testing purposes.

#### Why ? 
You can test the Microsoft device code flow manually without the need of installing any powershell modules.

## 1. Generate a device code

1. Open a Powershell prompt
2. Run below command:

```
curl -s -X POST `
  -H "Content-Type: application/x-www-form-urlencoded" `
  -d "client_id=04b07795-8ddb-461a-bbee-02f9e1bf7b46&resource=https://graph.microsoft.com/" `
  "https://login.microsoftonline.com/common/oauth2/devicecode?api-version=1.0" | ConvertFrom-Json | ConvertTo-Json -Depth 10
```

3. This results in the generation of a device code by using the Office on the web client ID.
4. After the user authenticates using the device code it gives you an access token scoped for the Microsoft Graph API.
5. Example authentication endpoint: https://microsoft.com/devicelogin

## 2. Fetch Access + Refresh tokens

1. After the user authenticated via the device code flow, run below command:

```
curl -s -X POST `
  -H "Content-Type: application/x-www-form-urlencoded" `
  -d "grant_type=urn:ietf:params:oauth:grant-type:device_code&client_id=04b07795-8ddb-461a-bbee-02f9e1bf7b46&device_code=YOUR_DEVICE_CODE_HERE" `
  "https://login.microsoftonline.com/common/oauth2/token" | ConvertFrom-Json | ConvertTo-Json -Depth 10
```

2. Keep in mind to change "YOUR_DEVICE_CODE_HERE" to the actual device code you've generated earlier.
3. Done

## Credits
Early work by https://github.com/rvrsh3ll Author of TokenTactics.
