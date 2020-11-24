# Azure CLI Examples

_Sample commands with Azure CLI._

## Show help message for specific command

Show help message for a command to create a web app.

```pwsh
az webapp create --help
```

## Web apps

### Create a web app

Create a web app and set Git repository URL to link with manual integration.

  ```pwsh
  az webapp create `
   --name "$WebAppName" `
   --plan "$AppServicePlanName" `
   --resource-group "$ResourceGroupName" `
   --deployment-source-url "GitHubRepositoryURL"
  ```
  
### Manage deployment from Git or Mercurial repositories

See the output of the next command

```pwsh
az webapp deployment source config -h
```

to find out the full documentation.
  
#### Get the Git repository URL from a source control deployment configuration
  
  ```pwsh
  (az webapp deployment source show `
   --name $WebAppName `
   --resource-group $ResourceGroupName `
   --subscription $SubscriptionID `
   --output json `
   --query "{repoUrl: repoUrl}" `
  | ConvertFrom-Json).repoUrl
  ```

#### Update the Git repository URL in a source control deployment configuration

```pwsh
az webapp deployment source config `
 --subscription "$SubscriptionID" `
 --name "$WebAppName" `
 --resource-group "$ResourceGroupName" `
 --repo-url "$GitHubRepositoryURL"
```

#### Synchronize a web app from the repository under manual integration mode

```pwsh
az webapp deployment source sync `
 --name "$WebAppName" `
 --resource-group "$ResourceGroupName"
```

### Test if a web app with the specified name does not exist

```pwsh
(az webapp list --query "[?name=='$WebAppName'].name" | ConvertFrom-Json | measure).Count -EQ 0
```

