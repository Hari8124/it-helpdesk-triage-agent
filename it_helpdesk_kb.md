# IT Helpdesk Knowledge Base (v1 synthetic set)

8 articles, 2 per category for Hardware / Software / Access & Permissions / Network.
"Other" intentionally has no article — see design note at the bottom.

---

### KB-001 — Laptop won't power on or charge
**Category:** Hardware
**Keywords:** laptop dead, won't turn on, not charging, battery not charging, power button, no lights when plugged in

**Steps:**
1. Confirm the charger is fully seated at both ends; try a different outlet.
2. Look for any light on the charging brick or the laptop's charging port when plugged in.
3. Hold the power button for 15 seconds to force a hard reset, then try powering on.
4. If possible, try a colleague's charger of the same model to isolate charger vs. laptop.
5. Check for visible damage to the cable or port.

**Escalate if:** physical damage, liquid exposure, a burning smell, or a swollen battery. Treat as a safety issue — don't troubleshoot further, escalate immediately.

---

### KB-002 — External monitor not detected
**Category:** Hardware
**Keywords:** monitor not detected, external display not working, second screen, HDMI, USB-C, docking station

**Steps:**
1. Confirm the cable is fully seated at both the laptop/dock and monitor.
2. Try a different port or cable if available (HDMI vs. DisplayPort vs. USB-C).
3. Force a display refresh (Windows: Win+P; Mac: System Settings → Displays → Detect Displays).
4. Restart the laptop with the monitor already connected.
5. If using a dock, connect the monitor directly to the laptop to isolate the dock as the cause.

**Escalate if:** the issue persists across multiple ports/cables/docks — likely a hardware fault needing a loaner or replacement.

---

### KB-003 — Application crashing or won't open
**Category:** Software
**Keywords:** app crashes, program won't open, software freezing, not responding, crashes on launch

**Steps:**
1. Fully close and reopen the application.
2. Restart the computer.
3. Check Software Center for a pending update to the application.
4. Confirm at least 2GB of free disk space (low space causes instability).
5. If it's a one-off document, try opening a different file to isolate a corrupt file vs. a broken install.

**Escalate if:** the crash caused data loss, the app is business-critical (e.g. finance/ERP) and work is blocked, or the issue persists after the update/restart steps.

---

### KB-004 — Software installation or license request
**Category:** Software
**Keywords:** need to install, request software, license request, can't install, admin rights to install, software center

**Steps:**
1. Check Software Center / the app catalog first — many tools are available as self-service installs.
2. If it needs a paid license, submit the software request form with business justification; manager approval may be required by policy.
3. Standard requests are typically fulfilled within 1–2 business days once approved.

**Escalate if:** the software isn't on the approved list (needs security/compliance review) or is high-risk (admin tooling, browser extensions with broad permissions).

---

### KB-005 — Password reset or account lockout
**Category:** Access & Permissions
**Keywords:** forgot password, locked out, account locked, can't log in, password expired, MFA

**Steps:**
1. Use the self-service password reset portal (requires enrolled MFA or security questions).
2. Lockouts from repeated failed attempts typically self-clear after 30 minutes, or can be cleared via the same portal.

**Escalate if:** the employee can't complete identity verification (e.g. lost MFA device, no backup method), or there's any hint the lockout is from a suspicious/unauthorized attempt — that's security-sensitive and always goes to a human, regardless of urgency.

---

### KB-006 — Requesting access to a shared drive or system
**Category:** Access & Permissions
**Keywords:** need access to, permission denied, access request, can't open shared drive, request folder access, system access

**Steps:**
1. Standard access requests (shared drives, distribution lists, line-of-business apps) go through the Access Request form, routed to the resource owner for approval.
2. Typical turnaround is 2–3 business days pending approval; note urgency and business reason for time-sensitive requests.

**Escalate if:** the request is for elevated or admin-level access (production systems, financial systems, HR/payroll data, local admin rights). These always need human review — never auto-approved by a canned response, no matter how urgent it's framed.

---

### KB-007 — VPN connection issues
**Category:** Network
**Keywords:** VPN won't connect, VPN disconnecting, can't connect to VPN, VPN timeout, remote access

**Steps:**
1. Confirm general internet access works without the VPN first.
2. Fully quit and relaunch the VPN client (not just disconnect/reconnect).
3. Restart the computer.
4. Confirm the VPN client is up to date via Software Center.
5. On public/hotel/coffee-shop Wi-Fi, some networks block VPN ports — try a mobile hotspot to isolate.

**Escalate if:** urgent access to business-critical systems is blocked and steps don't resolve it quickly, or several people report it at once (possible infrastructure issue — needs the network team's attention immediately, not a one-off reply).

---

### KB-008 — Wi-Fi or office network connectivity
**Category:** Network
**Keywords:** wifi not working, can't connect to network, internet not working in office, wifi keeps dropping, ethernet not working

**Steps:**
1. Toggle Wi-Fi off/on or reconnect to the network.
2. Forget the network and reconnect with credentials.
3. Restart the laptop.
4. On ethernet, check the cable is fully seated and try a different port/cable.
5. Ask whether nearby colleagues are also affected.

**Escalate if:** multiple employees in the same location report it simultaneously — likely an infrastructure outage, which needs immediate network-team escalation rather than individual canned replies.

---

## Design note: why "Other" has no article

Other is a deliberate pressure-release valve for the classifier, not a dumping ground with its own canned playbook. If a ticket is odd enough not to fit the four operational categories, it almost by definition isn't something a KB article was pre-written for — so the routing rule is: **category = Other implies escalate**. That's a testable claim step 3's error analysis can try to break.
