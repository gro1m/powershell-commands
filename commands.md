# Some random commands
docker images | Select-String -Pattern "mcr.microsoft.com"
https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_environment_variables?view=powershell-7.1
https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-powershell-1.0/ee332526(v=msdn.10)

# Remove from environment variable
## Version 1
```powershell
PS C:\Miniconda3> $Remove = 'C:Miniconda3\python.exe'
PS C:\Miniconda3> $env:Path = ($env:Path.Split(';') | Where-Object -FilterScript {$_ -ne $Remove}) -join ';'
```

## Better than Version 1
# Get it
```powershell
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

https://devblogs.microsoft.com/scripting/understanding-the-six-powershell-profiles/

Better Removing 

PowerShell conda profile.ps1
```powershell
#region conda initialize
# !! Contents within this block are managed by 'conda init' !!
(& "C:\ieu\Miniconda3\Scripts\conda.exe" "shell.powershell" "hook") | Out-String | Invoke-Expression
#endregion
```