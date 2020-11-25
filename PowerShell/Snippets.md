# PowerShell Snippets

_This is a collection of less or more complete PowerShell snippets I had to use._

## `Ping-Uri`

### Description

This is a function for test if a host or a web page exists.
Performs a web request to a specified URI and returns `$true` if it succeed and `$false` if not.
Doesn't raise exceptions if a page of an existing host wasn't found and also even if a host itself if absent.

### Code

```pwsh
function ping-uri {
    param(
        [parameter(mandatory=$true)]
        [string]$URI
    )

    $Status=200

    try {
        $Status=(invoke-webrequest $URI -SkipHttpErrorCheck).StatusCode
    }
    catch {
        $Status=404
    }

    return $Status -EQ 200
}
```

### Usage

#### Page

```pwsh
    if (ping-uri "https://github.com/vasily-blinkov/loquat-data") {
        write-error "Repository exists"
    }
    else {
        write-error "Repository doesn't exist"
    }
```

#### Host

```pwsh
    if (ping-uri "minimumminimorum.azurewebsites.net") {
        write-error "Host exists"
    }
    else {
        write-error "Host doesn't exist"
    }
```
