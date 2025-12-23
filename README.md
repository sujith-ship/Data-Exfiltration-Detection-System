# Data Exfiltration Detection System

A real-time network traffic monitoring and **data exfiltration detection system** implemented using **C, Libpcap, and MySQL**. The system captures live packets, extracts metadata, and detects suspicious activity through **signature-based IP and domain matching** using Traffic Light Protocol (TLP) classification.

---

## Features

* Real-time packet capture using Libpcap
* TCP/UDP packet filtering on sensitive ports
* Source/Destination IP and hostname extraction
* Secure traffic logging in MySQL
* Signature-based detection using TLP (GREEN, AMBER, RED)
* Automated MySQL event-driven comparison
* Scalable and modular architecture

---

## Tech Stack

* **Language:** C
* **Packet Capture:** Libpcap
* **Database:** MySQL
* **Networking:** TCP/IP, DNS resolution
* **OS:** Linux

---

## System Workflow

1. Capture live network packets
2. Extract packet headers and metadata
3. Store traffic data in MySQL (`TRAFFIC1`)
4. Compare destination IPs/domains with TLP tables
5. Classify traffic as GREEN, AMBER, or RED
6. Generate results for monitoring and analysis

---

## Database Structure

**Database:** `TRAFFIC_NETWORK`

**Main Table:** `TRAFFIC1`
Stores captured traffic data with a composite primary key:

```
(DATE, SRC_IP, DST_IP, DST_HOST, PROTOCOL, SRC_PORT_ID, DST_PORT_ID)
```

**Threat Intelligence Tables:**

* `TLP_GREEN`
* `TLP_AMBER`
* `TLP_RED`

---

## Setup Instructions

### 1. Install Dependencies

```bash
sudo apt update
sudo apt install libpcap-dev mysql-server libmysqlclient-dev gcc
```

---

### 2. Database Setup

```sql
CREATE DATABASE TRAFFIC_NETWORK;
USE TRAFFIC_NETWORK;
```

Create `TRAFFIC1` and TLP tables as per schema and enable events:

```sql
SET GLOBAL event_scheduler = ON;
```

---

### 3. Compile the Program

```bash
gcc traffic_capture.c -o traffic_capture -lpcap -lmysqlclient
```

---

### 4. Configure Network Interface

Update the interface name in the source code:

```c
char *interface = "enp1s0";
```

---

### 5. Run the Application

```bash
sudo ./traffic_capture
```

> Root privileges are required for packet capture.

---

## Detection Method

* Signature-based matching of destination IPs and domains
* Automated MySQL events for continuous comparison
* TLP-based threat categorization

---

## Use Cases

* Data Exfiltration Detection
* Network Forensics
* SOC Monitoring
* Academic and Research Projects

---

## Conclusion

This project provides an efficient and reliable approach to detecting data exfiltration by combining low-level packet capture with database-driven threat intelligence and automated analysis.

---

## Author

**Tedlapu Sagar**
Cyber Security | Network Monitoring | Digital Forensics
