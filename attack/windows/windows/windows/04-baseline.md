# Windows System Baseline ба Anomaly дүрэм (E хэсэг)

## 1. Baseline хүснэгт (Жишээ параметрүүд)

| Шалгуур үзүүлэлт (Parameter) | Хэвийн хүлээгдэж буй утга (Expected Baseline) | Тайлбар |
| :--- | :--- | :--- |
| **Үндсэн Service-үүд** | `W3SVC`, `WinRM`, `Spooler`, `Dhcp` | Зөвхөн шаардлагатай систем болон бизнесийн service-үүд ажиллах |
| **Админ эрхтэй хэрэглэгчид** | `Administrator`, `Domain Admins` (Цөөн тооны баталгаатай аккаунт) | Шинээр үүссэн эсвэл зөвшөөрөлгүй admin аккаунт байхгүй байх |
| **Автомат асах програм (Autorun)** | `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run` доторх баталгаатай path-ууд | Хортой программ суухаас сэргийлж автоматаар асах програмуудыг хянах |
| **Сүлжээний портууд** | TCP `135`, `445`, `3389`, `5985` | Зөвхөн нээлттэй байх ёстой стандарт портуудын жагсаалт |
| **PowerShell Execution Policy** | `RemoteSigned` эсвэл `Restricted` | Систем дээр дур мэдэн script ажиллахаас хамгаалах |

---

## 2. Anomaly (Гажилт илрүүлэх) 5 дүрэм

1. **Anomaly Rule 1: Шинэ Local Administrator аккаунт үүсэх**
   * **Event ID:** `4720` (A user account was created) болон дараа нь `4728` / `4732` (Administrators группт хэрэглэгч нэмэгдэх).
   * **Тайлбар:** Зөвшөөрөлгүйгээр нууц хэрэглэгч үүсгэж администратор эрх олгох оролдлогыг илрүүлэх.

2. **Anomaly Rule 2: Scheduled Task (Хуваарьт ажил) шинээр бүртгэгдэх**
   * **Event ID:** `4698` (A scheduled task was created).
   * **Тайлбар:** Халдагчид persistence (системд үлдэх) үүсгэх зорилгоор хортой скрипт эсвэл exe файлыг task-аар дамжуулан ажиллуулахаар тохируулсныг илрүүлэх.

3. **Anomaly Rule 3: PowerShell Script Block Logging (`4104`) дээр сэжигтэй түлхүүр үг илрэх**
   * **Event ID:** `4104` (Script Block Logging).
   * **Тайлбар:** `Invoke-Expression`, `Net.WebClient`, `EncodedCommand`, `Bypass` зэрэг obfuscation (халхавчилсан) болон payload татах команд ажиллах үед илрүүлэх.

4. **Anomaly Rule 4: Windows Firewall идэвхгүй болох эсвэл дүрэм өөрчлөгдөх**
   * **Event ID:** `4971` / `5025` (The Windows Firewall has been disabled).
   * **Тайлбар:** Халдагч сүлжээний холболтоо чөлөөтэй болгохын тулд firewall-ийг унтраах үед шууд alert өгөх.

5. **Anomaly Rule 5: LSASSプロセス (lsass.exe)-д хандах сэжигтэй процесс илрэх**
   * **Sysmon Event ID 10** (ProcessAccess) эсвэл **Event ID 4663** (An attempt was made to access an object).
   * **Тайлбар:** Credential dumping (Mimikatz гэх мэт хэрэгсэл ашиглан санах ойноос нууц үг хулгайлах) хийх зорилгоор `lsass.exe`-ийн руу хандаж буй зөвшөөрөлгүй процессуудыг илрүүлэх.
