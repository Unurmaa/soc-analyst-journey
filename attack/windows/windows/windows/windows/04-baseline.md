# Windows Baseline & Anomaly Rules

## 1. Baseline Хүснэгт
- **Logon Type:** Type 2 (Interactive), Type 3 (Network SMB) (Ажлын цагаар)
- **Process Execution:** `explorer.exe` -> `chrome.exe`, `cmd.exe`
- **PowerShell:** Зөвхөн админ хэрэглэгчийн шаардлагатай үед ашиглагдах

## 2. 5 Anomaly Rules (Гажилт илрүүлэх дүрмүүд)
1. Ажлын бус цагаар (22:00 - 06:00) RDP (Logon Type 10) амжилттай үүсэх.
2. Word/Excel файлуудаас `cmd.exe` эсвэл `powershell.exe` задарч ажиллах.
3. 1 минутад нэг хэрэглэгч дээр 5-аас дээш удаа 4625 (Failed Logon) гарах.
4. Security Log цэвэрлэгдэх (Event ID 1102).
5. Локал Administrators группэд шинэ хэрэглэгч шууд нэмэгдэх.
