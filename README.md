# DeviceCodeGenerator
Quick steps to generate Microsoft device codes for testing purposes.

#### Why ? 
You can test the Microsoft device code flow manually without the need of installing any powershell modules.

## 1. Generate a device code

1. Open a Powershell prompt
2. Run below command:

```
$device = curl -s -X POST `
  -H "Content-Type: application/x-www-form-urlencoded" `
  -d "client_id=04b07795-8ddb-461a-bbee-02f9e1bf7b46&scope=https://graph.microsoft.com/.default" `
  "https://login.microsoftonline.com/common/oauth2/v2.0/devicecode" | ConvertFrom-Json

$device | ConvertTo-Json -Depth 10
```

3. This results in the generation of a device code by using the client ID of Azure CLI.
4. After the user authenticates using the device code it gives you an access token scoped for the Microsoft Graph API.
5. Example authentication endpoint: https://microsoft.com/devicelogin

## 2. Fetch Access token

1. After the user authenticated via the device code flow, run below command:

```
curl -s -X POST `
  -H "Content-Type: application/x-www-form-urlencoded" `
  -d "grant_type=urn:ietf:params:oauth:grant-type:device_code&client_id=04b07795-8ddb-461a-bbee-02f9e1bf7b46&device_code=$($device.device_code)" `
  "https://login.microsoftonline.com/common/oauth2/v2.0/token" | ConvertFrom-Json | ConvertTo-Json -Depth 10
```

2. Keep in mind to use the same prompt so earlier `$device` variable can be used.
3. Done, the Access token can be used for additional testing purposes.

## Credits
Early work by https://github.com/rvrsh3ll Author of TokenTactics.
