# Windows vs Linux Security Event Mapping

| Үйл явдал | Windows Event ID / Sysmon | Linux Log Source |
|---|---|---|
| **Failed Login** | Event ID **4625** | `/var/log/auth.log` (`Failed password`) |
| **Successful Login** | Event ID **4624** | `/var/log/auth.log` (`Accepted password`) |
| **User Created** | Event ID **4720** | `/var/log/auth.log` (`new user`) |
| **Privilege Escalation**| Event ID **4672** | `/var/log/auth.log` (`sudo: COMMAND`) |
