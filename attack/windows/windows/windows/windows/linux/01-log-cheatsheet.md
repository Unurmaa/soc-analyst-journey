# Linux Log Cheatsheet & Commands

## Гол лог файлууд
- `/var/log/auth.log` (Debian/Ubuntu) эсвэл `/var/log/secure` (RHEL/CentOS): Баталгаажуулалт, SSH, sudo логууд.
- `/var/log/syslog`: Системийн ерөнхий үйл явдлын логууд.

## Чухал командууд ба жишээ
- SSH амжилтгүй болсон оролдлогуудыг харах:
  `grep "Failed password" /var/log/auth.log`
- Sudo команд ашигласан түүхийг шүүх:
  `grep "sudo:" /var/log/auth.log | grep "COMMAND"`
- Systemd лог харах:
  `journalctl -u ssh -f`
