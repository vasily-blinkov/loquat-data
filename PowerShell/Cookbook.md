# PowerShell Cookbook

_This page consists of typical tasks executing in PowerShell_

## Read a string securely and decrypt in

Useful in scripts to obtain a secure token etc from a user and pass it further without showing and storing it in history.

```pwsh
[System.Runtime.InteropServices.Marshal]::PtrToStringAuto([System.Runtime.InteropServices.Marshal]::SecureStringToBSTR((Read-Host -Prompt "GitHub Personal Access Token" -AsSecureString)))
```
