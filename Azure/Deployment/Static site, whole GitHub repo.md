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
подписка и ресурсная группа должны существовать
очистка
для выкладки запустить скрипт github.ps1
скрипты тоже выкладываются, что нехорошо
алгоритм - создать сайт с нуля
алгоритм - выкладка - перечислить основные команды azure cli, которые я использовал
алгоритм - зачистка - перечислить основные команды azure cli, которые я использовал
