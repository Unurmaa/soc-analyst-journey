# Windows Event Logs Cheat Sheet (Ярилцлагад бэлэн)

| Event ID | Эх сурвалж | Утга / Тодорхойлолт | MITRE ATT&CK | Жишээ Query (PowerShell) |
|---|---|---|---|---|
| **4624** | Security | Амжилттай нэвтэрсэн (Successful Logon) | T1078 | `Get-WinEvent -FilterHashtable @{LogName='Security';ID=4624}` |
| **4625** | Security | Амжилтгүй нэвтрэх туршилт (Failed Logon) | T1110 | `Get-WinEvent -FilterHashtable @{LogName='Security';ID=4625}` |
| **4688** | Security | Шинэ процесс үүссэн (Process Creation - Command Line) | T1059 | `Get-WinEvent -FilterHashtable @{LogName='Security';ID=4688}` |
| **1 (Sysmon)** | Sysmon | Процесс эхэлсэн (Process Create with Hash) | T1059 | `EventID: 1 AND image: "*cmd.exe"` |
| **3 (Sysmon)** | Sysmon | Сүлжээний холболт үүссэн (Network Connection) | T1071 | `EventID: 3 AND DestinationPort: 4444` |
| **1102** | Security | Windows Security Log-ийг устгасан/цэвэрлэсэн | T1070.001 | `Get-WinEvent -FilterHashtable @{LogName='Security';ID=1102}` |
| **7045** | System | Системд шинэ Service суулгасан | T1543.003 | `Get-WinEvent -FilterHashtable @{LogName='System';ID=7045}` |
