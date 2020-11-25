# How to deploy a static site from a GitHub repository to Azure

_This article will shortly describe a process of automating a process of static site deployment from a GitHub repo to Microsoft Azure App Service._

## Complete example

There is a completed example sourced at the [vasily-blinkov/minimum-minimorum](https://github.com/vasily-blinkov/minimum-minimorum) GitHub repository.
This site was published to App Service and it is available at [minimumminimorum.azurewebsites.net](http://minimumminimorum.azurewebsites.net/).

This is a project of a static HTML5 site. The structure of the project is quite simple:

```
index.html - the only content file representing a static site; in reality you may want to create a whole bunch of content, styles, images and client side scripts
deployment/ - directory for deployment automation scripts
    github.ps1 - deployment automation script to deploy the static site to Azure 
    cleanup.ps1 - script to remove the static site from Azure; it reverts github.ps1 results
    parameters.json - variable parameters such as resource group name, subscription I.D. etc.
    common/ - this directory stores a helper functions for scripts mentioned above
```

You are free to deploy this mini-site, but you need to have

1. an Azure subscription,
1. a resource group and
1. an AppService Plan.

If you haven't got something of listed above, create it.

Then checkout the repository and edit values in the `deployment/parameters.json` file. All the parameters except the `githubRepo` **must** be replaced with **your** values.

After that you are able to deploy the site by running the `deployment/github.ps1` script.

To remove the deployed web app from your resource group run the `deployment/cleanup.ps1` script.

Feel free to examine the scripts in the `deployment/`. If you like a step-by-step explanation of the simplest static web site creation process then read the next section.

### A note

The PowerShell scripts for deployment and cleanup and them auxiliaries are parts of the repository. This leads to publishing them to sites too. They won't be accessible after publish by referencing them by full path.

## Configure publishing of a static web site from a GitHub repository

_This seciton is about how to create and publish a static site to Azure App Service using the Azure CLI tool and a GitHub repository as a deployment source. 
But just remember that commands described below are just milestones. To see the complete deployment/cleanup script, please take a look at source code referenced in the section above._

### Create a GitHub repository

This step is a quite straightforward step for most of new projects. Just

1. create a new GitHub repository,
1. clone it locally and
1. create a static site.

To taste webapp deployment is is enough to create an `index.html` file in the repository root and fill it with a hello-world markup.

```xml
<!DOCTYPE html>
<html>
    <head>
        <title>Minimum minimorum</title>
    </head>
    <body>
        <h1>Hello, world!</h1>
    </body>
</html>
```

### Create a new webapp in AppService

Now, we are ready to create our static site in the cloud.

```bash
az webapp create `
 --name "$WebAppName" `
 --plan "$ServicePlanName" `
 --resource-group "$ResourceGroupName" `
 --deployment-source-url "$GhRepositoryUrl"
```

Remember to define variables (like `$ResourceGroupName`) or replace them with real values befor executing the command above.

The `--deployment-source-url` argument is a Git repository URL to link with manual integration. It will set the `repoUrl` parameter of deployment source configuration for the site.

The created site is available at the next URL: `"http://$($WebAppName.ToLower()).azurewebsites.net"` (PowerShell). Note: the site has been created but its content wasn't synchronized yet.

### Performing manual integration

To perform manual integration to sync the previously created use the next command.

```bash
az webapp deployment source sync --name "$WebAppName" --resource-group "$ResourceGroupName"
```

It will publish the content (only the `index.html` file in the example) of the site to the previously created URL.

### Updating the site

Let's suppose everyting described above passed and the site works. But what should we do to publish updates and new content to our site. I described the process step-by-step below.

1. Update your site (HTML, styles, images etc.).
1. Commit your changes.
1. Push your changes (the site was created by pointing a Git repository as a sync source, therefore Azure AppService will seek for all the data to publish in the repository in the URL passed when creating the site; I'm going to describe how to change the repository URL in the next section).
1. Perform the manual integration (described above).

### How to change a `repoUrl`?

To change a `repoUrl` use the command below.

```bash
az webapp deployment source config --subscription "$SubscriptionID" --name "$WebAppName" --resource-group "$ResourceGroupName" --repo-url "$NewRepoUrl"
```

Take your attention to the `--repo-url` argument. This is the trick.

### Cleaning up

The next command will remove the webapp created and published using the commands described in the previous secitons.

```bash
az webapp delete --name "$WebAppName" --resource-group "$ResourceGroupName"
```

## Final notes

Above I listed a few Azure CLI commands aimed to create a webapp and publish a static web site to it.




