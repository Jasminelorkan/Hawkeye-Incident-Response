# HawkEye Incident Response Investigation

Complete incident response investigation of a HawkEye Keylogger - Reborn v9 infection.Includes Blue Team, Red Team, and Purple Team perspectives with technical analysis and recommendations.

## Reports Included

- **Blue-Team-Report.md** - Incident response and forensic analysis from defender perspective
  
- **Red-Team-Report.md** - Attack simulation and exploitation techniques from attacker perspective
  
- **Purple-Team-Report.md** - Bridging both perspectives with detection gaps and recommendations

## Quick Facts

- **Malware**: HawkEye Keylogger - Reborn v9
- **Victims**: 4 compromised accounts
- **Attack Duration**: 01:03:41 captured
- **Exfiltration**: Every 10 minutes via SMTP
- **Tool Used**: Wireshark PCAP analysis

## Key Findings

- Malware delivered via HTTP from France-based server
- Credentials harvested from browser and email
- Data exfiltrated via SMTP without detection
- Complete attack chain documented with IOCs

## Full Writeup

Read the complete technical walkthrough on Medium:
[How I Investigated HawkEye Using Wireshark](https://medium.com/@jasminelorkan/how-i-investigated-a-hawkeye-keylogger-infection-using-only-wireshark-7963dc094367)

---

*Documentation, screenshots, and analysis 
files included.*
