# soc-home-lab
Build a centralized log ingestion and analysis pipeline using Splunk Enterprise, forwarding logs from Kali Linux to a Windows-hosted Splunk server.

## 02 Splunk Enterprise — Log Analysis Pipeline

**Objective:** Build a centralized log ingestion and analysis pipeline using Splunk Enterprise, forwarding logs from Kali Linux to a Windows-hosted Splunk server.

**Environment:**
- Splunk Enterprise v10.0.1 (Windows, 64-bit)
- Splunk Universal Forwarder v9.3.2 (Kali Linux)
- Log sources: `/var/log/auth.log`, `/var/log/syslog`

**What I built:**
- Installed Splunk Enterprise on Windows and configured receiving port 9997
- Deployed Universal Forwarder on Kali Linux and configured log monitoring
- Built SPL queries for real-time security monitoring and event correlation
- Developed dashboards for sourcetype analysis and boot/auth log investigation

**SPL Queries Used:**

```spl
# Count events by sourcetype
index=* host="vbox" | stats count by sourcetype

# Top 10 sourcetypes by frequency
index=* host="vbox" | top sourcetype limit=10

# Filter boot/startup events
index=* host="vbox" sourcetype="syslog" "boot"

# Authentication failure analysis
index=* host="vbox" sourcetype="auth" "Failed password" | stats count by src_ip | sort -count

# Suspicious sudo usage
index=* host="vbox" sourcetype="syslog" sudo | timechart count span=5m
```

**Key outcomes:**
- Successfully ingested auth, syslog, and boot logs from heterogeneous environment
- Identified authentication anomalies and privilege escalation patterns in log data
- Built dashboards enabling real-time SOC-style monitoring

**Tools:** Splunk Enterprise 10.0.1, Splunk Universal Forwarder, Kali Linux, Windows
