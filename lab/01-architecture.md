# Хичээл 1.1 · Архитектур ба лабораторийн бүтэц

## 1. Виртуал машин (VM) хүснэгт
| Хөрөнгийн нэр (Asset) | Үйлдлийн систем (OS) | Үүрэг (Role) | RAM / CPU |
| :--- | :--- | :--- | :--- |
| **wazuh-srv** | Ubuntu Server 22.04 / 24.04 | Wazuh Manager, Indexer, Dashboard & Lab Server | 4GB RAM / 2 vCPU |
| **WIN-EP01** | Windows Server 2022 | End-point agent (Sysmon, FIM, SCA, Vulnerability source) | 2GB RAM / 2 vCPU |

## 2. IP Төлөвлөгөө (IP Plan)
| Интерфейс / Сүлжээ | IP Хаяг | Тайлбар |
| :--- | :--- | :--- |
| **Host-only Network** | `192.168.56.0/24` | Лабораторийн дотоод изолирсон сүлжээ |
| **wazuh-srv IP** | `192.168.56.10` | Wazuh Manager болон Lab Web Server-ийн IP |
| **WIN-EP01 IP** | `192.168.56.20` | Windows Endpoint агентын IP |

## 3. Урсгалын схем (Flow Diagram)
[WIN-EP01 Agent (Sysmon, FIM, SCA, CVE)] 
        │
        ├─► (TCP 1514 - Encrypted Channel) ─► [Wazuh Manager (wazuh-srv: 192.168.56.10)]
        │                                             │
        └─► (HTTP 8000 - Plaintext / Sniffing) ───────┴─► [Wazuh Indexer & Dashboard]
