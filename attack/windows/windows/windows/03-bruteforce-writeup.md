# Windows Brute Force Detection Write-Up

## 1. PowerShell Detection Script
```powershell
Get-WinEvent -FilterHashtable @{
    LogName = 'Security'
    ID = 4625
} | Select-Object TimeCreated, Message
