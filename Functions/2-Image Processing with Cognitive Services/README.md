# 2 - Image Processing with Cognitive Services
## Summary
Process image files through Cognitive Services with Azure Functions and Blob Storage

### Tasks
1. Using CLI, create storage account. Retrieve connection string and create blob container 'challengefiles'.
2. Using CLI, create cognitive services vision service
3. Using CLI, create server-less function app that *only* retrieves *.jpg files from the storage blob
4. Add Cognitive Services Vision SDK to function project [Microsoft.Azure.CognitiveServices.Vision.ComputerVision].
5. Use the Cognitive Services Vision SDK in your function app and send image file to get image metadata
```
public static class ReadBlob
{
   private static HttpClient httpClient = new HttpClient();

   [FunctionName("ReadBlob")]
   public async static void Run([BlobTrigger("day1/{name}.jpg", Connection = "AzureWebJobsStorage")]Stream myBlob, string name, ILogger log)
   {
      var credentials = new ApiKeyServiceClientCredentials("d37f8c6195df44ee8275eec42e5c302a");

      using (var visionClient = new ComputerVisionClient(credentials) { Endpoint = "https://eastus.api.cognitive.microsoft.com/"} ) {
            VisualFeatureTypes[] visualFeatures = new VisualFeatureTypes[] {VisualFeatureTypes.Tags};
            var cts = new CancellationTokenSource();

            var result = await visionClient.AnalyzeImageInStreamAsync(myBlob, visualFeatures, null, "en", cts.Token);

            log.LogInformation($"Name:{name} \n Size: {myBlob.Length} Bytes");
            log.LogInformation($"Image Format: {result.Metadata.Format}, Width: {result.Metadata.Width}, Height: {result.Metadata.Height}");
      };
   }
}
```
6. Run locally, submitting files in this repo directory through Storage Explorer
7. Output JSON return values from service to information log

### Challenge
If you had to consult documentation or use `--help`, delete function and repeat.

### Spoilers
1. `az storage account create --resource-group AzureChallenges --name challengestore`  
`az storage account show-connection-string --name challengestore`  
`az storage container create --connection-string "CONNECTIONSTRING" --name challengefiles`  
2. `az cognitiveservices account create --resource-group AzureChallenges --name ACVisionService --kind ComputerVision --location eastus --sku S1`  
`az cognitiveservices account keys list --name ACVisionService --resource-group AzureChallenges`  
3. `...Run([BlobTrigger("challengefiles/{name}.jpg",...`
4. `dotnet add package Microsoft.Azure.CognitiveServices.Vision.ComputerVision --version 4.0.0`
