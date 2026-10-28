# WannaCry Ransomware Analysis & Kill Chain Write-Up

## 1. Overview (Ерөнхий ойлголт)
WannaCry нь 2017 оны 5 сард дэлхий даяар сая сая компьютерыг гэмтээсэн, EternalBlue (CVE-2017-0144) эмзэг байдлыг ашиглан SMBv1 протоколоор дамжин хүний оролцоогүйгээр сүлжээгээр өөрөө тархдаг (Worm-like) ransomware төрлийн хортой програм юм.

---

## 2. Cyber Kill Chain Задаргаа
WannaCry халдлагын үе шатыг Kill Chain загвараар дараах байдлаар задалж харж болно:

1. **Reconnaissance (Тагнуул хийх):**
   * Халдагч нь интернет эсвэл дотоод сүлжээн дэх 445 (SMB) порт нээлттэй, EternalBlue эмзэг байдалтай host-уудыг сканнердаж илрүүлдэг.
2. **Weaponisation (Зэвсэгжүүлэх):**
   * NSA-аас задарсан EternalBlue exploit-ийг DoublePulsar backdoor болон ransomware payload-тай хослуулан халдлагын багц болгож бэлтгэдэг.
3. **Delivery (Хүргэх):**
   * Шинээр холбогдсон сүлжээ рүү SMBv1 эмзэг байдлаар дамжуулан хортой пакетуудыг илгээх замаар анхны халдлагыг хүргэдэг.
4. **Exploitation (Ашиглах):**
   * Windows-ийн `srv.sys` драйверын санах ойн бафер халих (Buffer Overflow) эмзэг байдлыг ашиглан системд SYSTEM эрхтэйгээр код амжилттай ажиллуулдаг.
5. **Installation (Суулгах):**
   * DoublePulsar ашиглан хортой файлуудыг дискэнд суулгаж, `tasksche.exe` форк үүсгэн `mssecsvc2.0` нэртэй Windows Service хэлбэрээр байршиж тогтвортой байдлыг (Persistence) хангадаг.
6. **Command & Control (C2):**
   * Hardcoded хийсэн Kill-switch домэйн рүү (жишээ нь `www.iuqerfsodp9ifjaposdfjhgosurijfaewrwergwea.com`) HTTP хүсэлт явуулж шалгадаг. Хэрэв домэйн хариу өгвөл шифрлэлт зогсоно, хариу өгөхгүй бол шифрлэлт эхэлнэ.
7. **Actions on Objectives (Үндсэн зорилгоо биелүүлэх):**
   * Компьютер дэх `.docx`, `.pdf`, `.jpg`, `.zip` зэрэг өгөгдлийг AES-128 болон RSA-2048 алгоритмаар шифрлэж, `.WNCRY` болгон хувиргаад дэлгэц дээр ransom note (мөнгө нэхсэн зурвас) гаргаж ирдэг.

---

## 3. MITRE ATT&CK Mapping (Техникүүдийн зураглал)

| ATT&CK Tactic | Technique ID | Technique Name | WannaCry-ийн гүйцэтгэх үйлдэл |
|---|---|---|---|
| **Initial Access** | T1190 | Exploit Public-Facing Application | EternalBlue (CVE-2017-0144) ашиглан SMB-р нэвтрэх |
| **Execution** | T1059.003 | Windows Command Shell | Команд мөрөөр дамжуулан үйлдэл хийх |
| **Persistence** | T1543.003 | Windows Service | `mssecsvc2.0` нэртэй сервис үүсгэж үлдэх |
| **Defense Evasion** | T1070.004 | File Deletion / Volume Shadow Copy | `vssadmin delete shadows /all` ашиглан backup сэргээх боломжийг устгах |
| **Lateral Movement** | T1210 | Exploitation of Remote Services | Сүлжээн дэх бусад компьютерүүд рүү автоматаар цацагдах |
| **Impact** | T1486 | Data Encrypted for Impact | Бүх чухал файлуудыг шифрлэж түгжих |

---

## 4. Дүгнэлт
WannaCry нь хуучирсан SMBv1 протоколыг ашигладаг, систем дэх patch (шинэчлэлт)-ийг хийгээгүй байх үед хэр аюултай болохыг харуулсан сонгодог жишээ юм. Үүнээс хамгаалахын тулд хуучирсан протоколуудыг хаах, байнгын patch update хийх, болон EDR/SIEM систем ашиглан abnormal SMB traffic-ийг эрт илрүүлэх нь чухал болохыг энэхүү шинжилгээ харуулж байна.
