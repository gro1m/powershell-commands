# Some random commands
```powershell
docker images | Select-String -Pattern "mcr.microsoft.com"
```

# Some random references
- https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_environment_variables?view=powershell-7.1
- https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-powershell-1.0/ee332526(v=msdn.10)
- https://devblogs.microsoft.com/scripting/understanding-the-six-powershell-profiles/ (PowerShell profiles)

# Remove from environment variable
## Version 1
```powershell
PS C:\Miniconda3> $Remove = 'C:\Miniconda3\python.exe'
PS C:\Miniconda3> $env:Path = ($env:Path.Split(';') | Where-Object -FilterScript {$_ -ne $Remove}) -join ';'
```

## Better than Version 1
```powershell
# Get it
$path = [System.Environment]::GetEnvironmentVariable(
    'PATH',
    'User'
)
# Remove unwanted elements
$path = ($path.Split(';') | Where-Object { $_ -ne 'ValueToRemove' }) -join ';'
# Set it
[System.Environment]::SetEnvironmentVariable(
    'PATH',
    $path,
    'User'
)
```
Reference: https://stackoverflow.com/questions/39010405/powershell-how-to-delete-a-path-in-the-path-environment-variable


# PowerShell conda profile.ps1
```powershell
#region conda initialize
# !! Contents within this block are managed by 'conda init' !!
(& "C:\ieu\Miniconda3\Scripts\conda.exe" "shell.powershell" "hook") | Out-String | Invoke-Expression
#endregion
```

# Reference on PowerShell Here String syntax (multiline strings)
https://devblogs.microsoft.com/scripting/maximizing-the-power-of-here-string-in-powershell-for-configuration-data/

# Microsoft Docs Reference
https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/move-item?view=powershell-7.1

# Delete existing files and folders
https://gimpland.org/now/2014/02/powershell-test-if-file-exists-and-delete/
