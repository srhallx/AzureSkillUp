# 1 - Blob Storage Trigger
## Summary
Use functions with a blob storage trigger to process *.txt files
### Prerequisites:
1. Update your Azure Functions Core Tools through command line [link](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local)
2. Install/Update [Azure Storage Explorer](https://azure.microsoft.com/en-us/features/storage-explorer/)


### Tasks
1. Create a Resource Group for the challenges (ex: AzureChallenges)
2. Using CLI, create storage account. Retrieve connection string and create blob container 'challengefiles'.
3. Using CLI, create server-less function app that *only* retrieves *.txt files from the storage blob
4. Print file name, size and first 20 characters to information log output
5. Run locally, submitting files in this repo directory through Storage Explorer

### Challenge
If you had to consult documentation or use `--help`, delete function and repeat.

### Spoilers
1. `az group create --name AzureChallenges --location CentralUS`
2. `az storage account create --resource-group AzureChallenges --name challengestore`  
`az storage account show-connection-string --name challengestore`  
`az storage container create --connection-string "CONNECTIONSTRING" --name challengefiles`  
3. `...Run([BlobTrigger("challengefiles/{name}.txt",...`
4. Use `log.LogInformation()`
5. `func host start`
