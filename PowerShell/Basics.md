# PowerShell basics

_This article contains usage examples of main PowerShell commands and constructs._

## Commands

### Filesystem

#### Create a new directory

```pwsh
ni -ItemType Directory public
```

#### Move a file from the current directory to a sub-directory

```pwsh
mi .\index.html .\public\
```

### Interactive

#### Read-Host

##### With prompt

```pwsh
Read-Host -Prompt "GitHub Personal Access Token"
```

##### Masked

```pwsh
Read-Host -Prompt "GitHub Personal Access Token" -AsSequreString
```

## Constructs

TODO
