# Eval set — 24 synthetic tickets

Grouped here by test purpose for readability. The agent sees each ticket independently — no memory of the others, no hint of this grouping. Predictions are my hypothesis going in, not an answer key; the ambiguous ones deliberately don't have a single correct label.

## Clean match → should be canned (8)

| ID | Ticket | Predicted |
|----|--------|-----------|
| T01 | "Hi, my laptop won't turn on today. I left it plugged in overnight but there's no light on the charger or the laptop when I press the power button. Tried a different outlet too, still nothing." | Hardware / canned (KB-001) |
| T02 | "hey the external monitor at my desk stopped showing anything this morning. it was working fine friday. i checked the hdmi cable and its plugged in on both ends" | Hardware / canned (KB-002) |
| T03 | "Excel keeps crashing every time I try to open one specific spreadsheet, it just freezes for a few seconds and then closes. Other spreadsheets open fine. This is the only one that does it." | Software / canned (KB-003) |
| T04 | "Hi team, I need Adobe Acrobat Pro installed on my laptop for a contract review I'm doing next week. Not sure if this needs manager approval or if I can just request it. Thanks!" | Software / canned (KB-004) |
| T05 | "I forgot my password and got locked out after a few tries. I have the authenticator app on my phone if that helps. Need to get back in soon, have a 1pm deadline." | Access & Permissions / canned (KB-005) |
| T06 | "Could someone grant me access to the Marketing Assets shared drive? My manager (Dana) said I'd need it for the Q3 campaign work starting this week." | Access & Permissions / canned (KB-006) |
| T07 | "My VPN client keeps saying 'connection timed out' when I try to connect from home this morning. Internet itself is working fine, I can browse normally, it's just the VPN." | Network / canned (KB-007) |
| T08 | "The wifi on my laptop keeps dropping every 10-15 min today, just at my desk though, my coworker next to me hasn't had any issues. Reconnecting fixes it temporarily." | Network / canned (KB-008) |

## Category obvious, but policy says escalate (6)

| ID | Ticket | Predicted | Why escalate |
|----|--------|-----------|---------------|
| T09 | "This might be nothing but my laptop has started smelling like burning plastic when it's been on for a while, especially near the left hinge. Should I keep using it?" | Hardware / escalate | Safety |
| T10 | "Our finance close tool (NetSuite) just crashed and I lost about an hour of unsaved reconciliation work. This is happening for two other people on my team too, right in the middle of month-end close." | Software / escalate | Business-critical + data loss + multi-user |
| T11 | "Can I get admin/root access to the prod Kubernetes cluster? Need it to debug a deploy issue for the release going out Thursday." | Access & Permissions / escalate | Privileged/production |
| T12 | "I got locked out of my account and when I finally reset my password, I noticed there was a login attempt logged from a location I don't recognize last night. Is that normal?" | Access & Permissions / escalate | Suspicious activity |
| T13 | "Not sure if this is just me but literally the entire 3rd floor has no internet right now, like 20+ people including me. Started about 15 min ago." | Network / escalate | Outage scale |
| T14 | "VPN has been down for 2 hours. I've restarted my laptop twice, fully reinstalled the VPN client, tried a different network. Nothing works. I have a client call in 10 minutes and need VPN to access our files." | Network / escalate | Already tried standard steps + urgent |

## Genuinely ambiguous — two categories both defensible (5)

| ID | Ticket | Plausible categories |
|----|--------|----------------------|
| T15 | "My laptop won't connect to any wifi network at all, not even my phone's hotspot, even though it shows wifi as 'on' in settings. Other devices connect to the same networks fine." | Hardware (device radio) or Network |
| T16 | "I can't log into Salesforce, it just says 'invalid session, please try again' over and over no matter how many times I re-enter my password." | Access & Permissions (session/auth) or Software (app bug) |
| T17 | "My laptop has gotten so slow over the past week or two. Just opening Chrome takes like 5 minutes now. It didn't used to be like this." | Hardware (aging device) or Software (bloat/malware) |
| T18 | "I can open the Finance shared drive fine at the office but when I work from home I get 'access denied.' Nothing's changed about my account as far as I know." | Network (VPN — permissions aren't usually location-gated) or Access & Permissions |
| T19 | "Every time my laptop wakes up from sleep, my second monitor stays black. I have to unplug the HDMI cable and plug it back in to get it to show anything again." | Software (wake/driver bug) or Hardware (cable/port) |

## Other — not really IT (2)

| ID | Ticket | Predicted |
|----|--------|-----------|
| T20 | "Is there someone I should talk to about getting a standing desk converter? My back's been bothering me sitting all day." | Other / escalate |
| T21 | "Do I need to request a parking permit for the new garage on 5th street or is my old badge still going to work there?" | Other / escalate |

## Security triggers + no-KB-match (3)

| ID | Ticket | Predicted | Why |
|----|--------|-----------|-----|
| T22 | "I think I might have clicked a phishing link. I got an email that looked like it was from IT asking me to verify my password on a login page, and I entered it before I second-guessed myself. What do I do?" | Access & Permissions / escalate | Phishing/security |
| T23 | "This is a weird one — when I share my second monitor on Zoom calls, everyone on the call sees a green tint over everything, but only when I share that specific monitor. Sharing my main screen looks totally normal." | Software / escalate | Category obvious, no close KB match (also tests whether "screen"/"monitor" wording falsely pulls KB-002) |
| T24 | "A few keys on my keyboard aren't registering when I type, mainly E, R, and the space bar. It's making it really hard to type anything without a bunch of typos." | Hardware / escalate | Category obvious, no close KB match |

**Design note:** the brief asked for "a few ambiguous" and "one clear escalate." I went further on both — 5 ambiguous cases across different category pairs, and 9 total escalate-policy tests across 6 different triggers (safety, business-critical, privilege, security/suspicious, security/phishing, scale, already-tried, and 2 no-KB-match cases) — because testing only one escalation reason would leave most of the policy logic in the system prompt completely unverified.
