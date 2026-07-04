# AI-SOC-assistant
An AI Agent I built with n8n that can look up domains and IP addresses using VirusTotal and then generate a SOC report on them.

**Overview**

This workflow allows a user to submit an IP address or domain via chat. The AI agent will:

1. Extract indicators of compromise (IP or domain)
2. Query VirusTotal for threat intelligence
3. Analyse the response data
4. Generate a ~200-word SOC-style security report

It is designed as a lightweight security enrichment and reporting assistant for learning, automation, or SOC lab environments.

**Features**
1. Chat-based Trigger
2. AI Agent powered by OpenAI
3. VirusTotal enrichment for IP addresses and Domains
4. Automated SOC-style report generation

**Architecture**

1. Chat Trigger
2. AI Agent (Langchain)
3. VirusTotal IP Tool
4. VirusTotal Domain Tool
5. LLM (OpenAI)

**Example Output**

```
Summary: br-icloud.com.br is flagged by multiple engines as malicious and likely part of phishing/malicious infrastructure impersonating Apple iCloud. VirusTotal reputation is -2 with 14 engines classifying it as malicious and 2 as suspicious (last analysis stats: malicious 14, suspicious 2, undetected 32, harmless 43). Community votes: 6 malicious / 4 harmless.

Technical details:

Resolved A: 103.224.182.242
Nameservers: ns11.abovedomains.com, ns12.abovedomains.com
SPF TXT: "v=spf1 ip6:fdcf:abda:4154::/48 -all"
TLS: Let's Encrypt (R13), certificate subject CN: 859t.me; SANs include br-icloud.com.br and many unrelated domains (suggests shared/wildcard cert used by mass-hosting/abuse)
WHOIS: domain registered under br-icloud.com.br with mixed historical changes; expires 2027
Detections of note: BitDefender, Kaspersky, Fortinet, Sophos, Webroot, Certego and others tag it as phishing/malicious. Some engines report “malware” classification.

Assessment & impact: High risk — domain is consistent with credential-phishing campaigns targeting iCloud users and/or hosting malicious payloads. Shared certificate and numerous SAN entries suggest use of shared hosting or automated provisioning for abusive domains.

Recommended actions:

Block domain and IP (103.224.182.242) at perimeter and email gateways.
Add to internal denylists and SIEM IOC feeds.
Hunt for related traffic and credential-submission events; escalate suspected compromises.
Preserve samples (HTTP landing pages, headers) and submit to takedown/registrar where applicable.
Monitor for certificate/hosts changes and update detection rules.
```

**Setup Instructions**
1. Import JSON into n8n
2. Configure credentials - you will need an OpenAI API key (or other LLM) and a VirusTotal API key
3. Activate Workflow - enable workflow and use chat trigger to send IPs and domains.

