# Linux SSH Brute Force Write-Up

## 1. Лог шүүх (Grep & Awk)
```bash
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -nr
