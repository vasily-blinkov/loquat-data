# Azure CLI Examples

_Sample commands with Azure CLI._

## Show help message for specific command

Show help message for a command to create a web app.

```pwsh
az webapp create --help
```

## Subscriptions

### Test if the subscription specified by its I.D. does not exist

```pwsh
(az account list --query "[?id=='$SubscriptionID'].name" | ConvertFrom-Json | measure).Count -EQ 0
```

## App Service plans

### Test if the specified by its name App Service plan does not exist

```pwsh
(az appservice plan list --query "[?name=='$AppServicePlanName'].id" | ConvertFrom-Json | measure).Count -EQ 0
```

## Resource groups and template deployments

### Test if the resource group specified by name does not exits

```pwsh
(az group list --query "[?name=='$ResourceGroupName']" | ConvertFrom-Json | measure).Count -EQ 0
```

## Web apps

### Create a web app

Create a web app and set Git repository URL to link with manual integration.

```pwsh
az webapp create `
 --name "$WebAppName" `
 --plan "$AppServicePlanName" `
 --resource-group "$ResourceGroupName" `
 --deployment-source-url "$GitHubRepositoryURL"
```

### Delete a web app

```pwsh
az webapp delete `
 --name $WebAppName `
 --resource-group $ResourceGroupName
```

### Test if a web app exists

```pwsh
(az webapp list `
 --query "[?name=='$WebAppName'].name"
| ConvertFrom-Json
| measure).Count -NE 0
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

