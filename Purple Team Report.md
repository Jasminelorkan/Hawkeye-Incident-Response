# Hawkeye Purple Team

## **Executive Summary**

A simulated phishing and credential harvesting attack was conducted against workstation
BEIJING-5CD1-PC (10.4.10.132) using HawkEye Keylogger - Reborn v9. The Red Team successfully
delivered the payload, harvested credentials from four accounts, and exfiltrated data via
SMTP every 10 minutes — all without triggering any alerts during the operation.

Post-incident analysis by the Blue Team confirmed the full attack chain through PCAP
forensics. However the attack was not detected in real time, indicating significant gaps in
the organization's monitoring and endpoint protection capabilities.

This report bridges both perspectives to identify detection gaps and recommend
improvements to prevent similar attacks.

## **Attack Overview**

Target:     BEIJING-5CD1-PC (10.4.10.132)
User:       roman.mcguire
Malware:    HawkEye Keylogger - Reborn v9
Payload:    tkraw_Protected99.exe
Source:     [proforma-invoices.com](http://proforma-invoices.com/) (217.182.138.150)

Attack Summary:
The Red Team delivered HawkEye Reborn v9 to the target workstation via HTTP. The
malware executed silently, harvested credentials from Chrome and MS Outlook, then exfiltrated stolen data via SMTP every 10 minutes to an attacker controlled email address.

Full attack chain completed without detection. Total credentials compromised: 4 Total accounts accessed: Bank of America, AOL, MS Outlook.

![wrieshark1.jpeg](wrieshark1.jpeg)

## **Detection Gaps**

1. No HTTP download filtering
Malicious .exe downloaded from unknown external domain without any alert or block
2. No Endpoint Detection (EDR)
HawkEye executed and ran silently . No behavioral detection triggered
3. No outbound SMTP monitoring
Workstation sending emails is abnormal. No alert was generated
4. No email content inspection
Base64 encoded credentials transmitted via SMTP without detection
5. No repeated pattern alerting
Same data exfiltrated every 10 minutes. No anomaly detection in place

## **Recommendations**

1. Implement Web Proxy with URL Filtering
Block downloads of executable files (.exe) from unknown external domains via HTTP. Alert on any unsigned executable download.
2. Deploy Endpoint Detection & Response (EDR)
Tools like Microsoft Defender for Endpoint or CrowdStrike to detect malicious process behavior and keylogger activity in real time.
3. Monitor Outbound SMTP Traffic
Alert when any workstation attempts direct SMTP connections to external servers.
Only the mail server should send outbound SMTP traffic.
4. Implement Email Content Inspection
Deploy email security gateway to scan outbound emails for encoded credentials, suspicious attachments, and data patterns.
5. Anomaly Detection for Repeated Patterns
Configure SIEM alerts for repeated outbound connections to the same external IP at regular intervals — indicating automated exfiltration behavior.

## **MITRE ATT&CK Coverage**

TECHNIQUE                  DETECTED?              COVERAGE GAP
─────────────────────────────────────────────────
T1566 - Phishing                   No                     No email filtering
in place

T1059 - Scripting                  No                    No script execution
Interpreter                                                       monitoring

T1555 - Credentials             No                    No EDR to detect
from Password Stores                                  credential access

T1056 - Input Capture        No                    No behavioral
(Keylogging)                                                  detection deployed

T1048 - Exfiltration              No                    No outbound SMTP
Over Alt Protocol                                         monitoring

T1071 - Application             No                    No network traffic
Layer Protocol                                               anomaly detection

## **Conclusion**

This Purple Team exercise revealed critical detection gaps across all six MITRE ATT&CK techniques employed during the operation. The attack achieved a 100% success rate with zero real time detections.

The most significant risk is the ongoing credential exfiltration every 10 minutes
via SMTP — compromising banking, personal, and corporate accounts belonging to
roman.mcguire without triggering a single alert.

The most urgent fixes are EDR deployment for endpoint behavioral detection and
outbound SMTP monitoring to catch credential exfiltration in real time.
Without these controls, similar attacks will continue to operate undetected.