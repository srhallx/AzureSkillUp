# 1 - Static Page Web Site

## Summary
Create a static page web site hosted in Azure App Service
### Prerequisites:
1. Update your Azure Functions Core Tools through command line [link](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local)



### Tasks
1. Create a directory and a static HTML page (ex: index.html)
2. Using Azure CLI, preview (dry run) the deployment using 'az webapp up' command syntax with appropriate parameters
3. Using Azure CLI, deploy page to a new app service using 'az webapp up' command and test website
4. Update the Auth for the web app to require AD authentication using Azure Portal
5. Test using private mode in browser to ensure it properly requires and uses credentials

### Challenge
If you had to consult documentation or use `--help`, delete function and repeat.

### Spoilers
2. `az webapp up --name day1website --location CentralUS --dryrun`
3. `az webapp up --name day1website --location CentralUS`
4. Go to Authentication/Authorization section of App Service
Turn on App Service Authentication
Select 'Login with Azure Active Directory' in Action dropdown
Select 'Azure Active Directory' as authentication provider
Select 'Express' and click OK
Save settings
