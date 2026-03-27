# Incident Response Playbook — Phishing Attack

**Playbook ID:** IRP-001  
**Category:** Phishing  
**Version:** 1.0  
**Analyst:** Michael Eziuzor  
**Date:** March 2026  

---

## 1. Overview

This playbook provides a structured step-by-step response procedure for 
handling phishing incidents within a SOC environment. It covers the full 
incident response lifecycle from detection through to post-incident review.

---

## 2. Scope

This playbook applies to the following phishing scenarios:

- Phishing emails reported by end users
- Phishing emails detected by email gateway
- Credential harvesting sites identified via threat intelligence
- Spear phishing targeting specific individuals or departments

---

## 3. Severity Classification

| Severity | Criteria |
|----------|----------|
| Critical | Executive targeted, credentials confirmed compromised |
| High | Multiple users targeted, malicious attachment executed |
| Medium | Single user targeted, link clicked, no confirmed compromise |
| Low | Email blocked at gateway, no user interaction |

---

## 4. Incident Response Procedure

### Phase 1 — Identification

- [ ] Receive phishing report from end user or SIEM alert
- [ ] Obtain the suspicious email including full headers
- [ ] Record the following details:
  - Sender display name and actual email address
  - Reply-to address
  - Subject line
  - Date and time received
  - List of recipients

---

### Phase 2 — Analysis

- [ ] Inspect email headers for SPF, DKIM, and DMARC results
- [ ] Identify originating IP address from email headers
- [ ] Check originating IP on AbuseIPDB and VirusTotal
- [ ] Extract all URLs from the email body
- [ ] Defang all URLs before analysis: replace http with hxxp
- [ ] Submit URLs to VirusTotal and URLScan.io
- [ ] Check domain registration date via WHOIS
- [ ] Analyse any attachments in a sandbox environment
- [ ] Determine if the user clicked any links
- [ ] Determine if the user submitted any credentials

---

### Phase 3 — Containment

- [ ] Block sender domain at email gateway
- [ ] Block malicious URLs at web proxy and firewall
- [ ] Block originating IP at perimeter firewall
- [ ] If user clicked link — reset user credentials immediately
- [ ] If credentials compromised — disable affected account
- [ ] If attachment executed — isolate affected endpoint immediately
- [ ] Notify IT and management of containment actions taken

---

### Phase 4 — Eradication

- [ ] Remove phishing email from all user mailboxes
- [ ] Confirm no persistence mechanisms installed on affected endpoints
- [ ] Verify no lateral movement occurred from affected accounts
- [ ] Submit malicious domain to Google Safe Browsing and Microsoft 
  SmartScreen for takedown
- [ ] Report phishing domain to registrar for takedown

---

### Phase 5 — Recovery

- [ ] Restore affected user account with new credentials
- [ ] Confirm endpoint integrity before reconnecting to network
- [ ] Monitor affected accounts for 72 hours post-incident
- [ ] Verify email gateway rules are active and updated
- [ ] Confirm user can access systems normally

---

### Phase 6 — Post-Incident Review

- [ ] Document full incident timeline
- [ ] Record all IOCs discovered during investigation
- [ ] Identify how the phishing email bypassed existing controls
- [ ] Update email gateway rules based on findings
- [ ] Conduct targeted phishing awareness training for affected users
- [ ] Submit lessons learned report to SOC lead

---

## 5. Key IOC Documentation Template

| IOC Type | Value | Source | Action Taken |
|----------|-------|--------|--------------|
| Sender Domain | | | Blocked |
| Originating IP | | | Blocked |
| Phishing URL | | | Blocked |
| File Hash | | | Quarantined |

---

## 6. Escalation Criteria

Escalate to Tier 2 / Incident Response team if any of the following apply:

- Confirmed credential compromise
- Malicious attachment executed on endpoint
- Evidence of lateral movement
- Executive or privileged account targeted
- Multiple users affected simultaneously

---

## 7. Tools Used

| Tool | Purpose |
|------|---------|
| VirusTotal | URL and IP reputation analysis |
| AbuseIPDB | IP abuse history lookup |
| URLScan.io | URL behaviour analysis |
| WHOIS | Domain registration lookup |
| Email Header Analyser | SPF, DKIM, DMARC inspection |
| Sandbox | Attachment analysis |

---

## 8. References

- NIST SP 800-61 Computer Security Incident Handling Guide
- MITRE ATT&CK T1566 — Phishing
- Sans Institute Incident Handler's Handbook

---

**Playbook Version:** 1.0  
**Last Updated:** March 2026  
**Analyst:** Michael Eziuzor | github.com/Eziuzor-SEC
