# 3CX Integration with Salesforce with Person Accounts

This is customized version of the template "SalesforceV2" from 3CX v18.0 with the support of Person Account entities in Salesforce.

From here: [3cx manual Salesforce CRM Integration - Server Side](https://www.3cx.com/docs/salesforce-crm-integration)  
`- Salesforce accounts with Person Accounts enabled are not supported`

### Disclaimer: it was tested ONLY for journaling of outgoing calls.
---
## Install

Use "salesforce_template_w_person_accounts.xml" for production.  
Use "salesforce_template_w_person_accounts_sandbox.xml" for sandbox testing.

How to setup - [read here](https://www.3cx.com/docs/salesforce-crm-integration) 


## Extra information for development/testing
### Salesforce links
* a. https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_prereq.htm
* b. https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&type=5
* c. https://www.postman.com/salesforce-developers/workspace/salesforce-developers/collection/12721794-67cb9baa-e0da-4986-957e-88d8734647e2?action=share&creator=665632

## How to setup OAuth authentication in Postman.
The configuration is described for the Salesforce Sandbox. If you connect to live version - adjust URLs accordingly.
1. On the top level of imported collection (Salesforce APIs) set next Variables (tab 4):

* 1. url: https://test.salesforce.com  (or https://login.salesforce.com for live environment).   
NOTE - it MUST be "test" or "login". Do not use personalized URLs, like https://mycompany.my.salesforce.com or https://mycompany--sandboxname.lightning.force.com
* 2. version: 53.0
* 3. username: username@myemail.com.sandboxname (or username@myemail.com for live environment)
* 4. password  (NOTE: the pass for OAuth API=pass_for_web+security_token). I.e. if you have web pass "Pass1234" and security token: "hjgj6554jhksdkjf", then API pass should be: "Pass1234hjgj6554jhksdkjf"
* 5. clientId: from link "b"  (from "Salesforce links" above)
* 6. clientSecret: from link "b"

2. On the top level of imported collection (Salesforce APIs) set next Authorization params (tab 1):
```
Type: OAuth2.0
Token Name: anyname
Grant Type: Password Credentials
Access Token URL: {{url}}/services/oauth2/token
Client ID: {{clientId}}
Client Secret: {{clientSecret}}
Username: {{username}}
Password: {{password}}
Scope: "" (leave empty)
Client Authentication: Send client credentials in body
```

Press "Get New Access Token".  
If everything is ok you should get a window with the token info. Press "Use Token". Copy "instance_url" and update the "_endpoint" Variable (tab 4) to it. This endpoint will be used for all requests.
