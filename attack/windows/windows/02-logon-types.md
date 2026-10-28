# Windows Logon Types Guide

| Logon Type | Нэр / Тайлбар | Хэзээ хэвийн (Normal)? | Хэзээ сэжигтэй (Suspicious)? |
|---|---|---|---|
| **2** | Interactive | Физик эсвэл ВМ консол дээр нэвтрэх | Ажлын бус цагаар энгийн хэрэглэгч серверт хандах |
| **3** | Network | Сүлжээний Share, SMB, IIS веб сервер | Нэг машинаас олон удаа 4625 (Brute force) үүсэх |
| **10** | RemoteInteractive | RDP (Remote Desktop)-оор зайнаас нэвтрэх | Гадаад IP-ээс эсвэл зөвшөөрөлгүй цагаар RDP хийх |
