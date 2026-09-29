# Copilot Ticket Intake Template

**Artifact:** Slide 52, "Copilot Ticket Intake Template - Standardize evidence collection"
**Course:** Microsoft Copilot Operations for the US Government Publishing Office (GPO), GCC tenant
**Version:** 1.0, September 29, 2026
**Owner:** Copilot Operations Team (Tier 2). Review quarterly; next review January 2027.
**Companion artifacts:** Copilot Triage Decision Tree, Tier 1 Quick Reference, Escalation Matrix, GCC Feature Reference, Known Issues Playbook.

All names, identifiers and values in the worked example are fictional. Click paths and technical facts are aligned to Microsoft Learn as of September 2026; verify in the GPO tenant before configuring a ticketing system.

---

## Part 1: What makes an intake template effective

An intake template succeeds when a Tier 2 analyst can pick up any ticket cold and start investigating without calling the user back. It fails when it is a free-text box with a category dropdown. The template below is built on nine design characteristics, each of which fixes a specific failure seen in Copilot support queues.

| Characteristic | What it fixes |
|---|---|
| **The five facts are mandatory fields, not prose.** Who, Where, What, When, What changed each have their own structured field with validation. | "Copilot is broken, please fix ASAP" tickets that consume a full callback before any work begins. |
| **Observation is separated from interpretation.** The user's words are captured verbatim in one field; the analyst's classification lives in a different section. | Tickets whose title already contains the wrong diagnosis ("Excel Copilot outage") and steer every downstream reader. |
| **Mode and client are first-class fields.** Work mode versus Web mode, browser versus desktop, assigned laptop versus shared workstation. | Most Layer 2 and Layer 3 questions are answered by "which app, which mode, which device". Without these, web grounding and channel eligibility tickets cannot be triaged. |
| **Evidence is collected at intake, with results recorded.** License view, File > Account, browser test, direct-open test, Service health check, each with a result and a time stamp. | Escalations that arrive as a symptom with no evidence, forcing Tier 2 to repeat Tier 1's work. |
| **An expected-behavior screen runs before classification.** GCC policy, feature availability, reporting latency, provisioning window, agent scope. | Roughly seven in eight Copilot tickets are not failures. Screening for the known non-failures first keeps them out of the incident count. |
| **Classification mirrors slide 36's six outputs.** Affected experience, layer, evidence and first check, administrative surface, user action, escalation and destination. | Tier 1 and Tier 2 speaking different languages about the same ticket. |
| **Picklists wherever a value repeats.** Apps, modes, clients, devices, symptom families, layers, root causes, destinations. | Free-text categories that cannot be counted, so the monthly ticket analysis (slide 41) is guesswork. |
| **Initial classification and confirmed root cause are different fields.** The first is Tier 1's best guess at intake; the second is set at closure. | Ticket analysis that measures what analysts thought at minute five instead of what was true. |
| **Every closed ticket answers "was this a Copilot failure?"** One field, yes or no, with a reason. | The debrief question from the triage exercise becomes a metric instead of an anecdote. |

Two constraints shape the length: intake should take a trained Tier 1 analyst six to eight minutes on the phone, and the template must never require a change to any setting. It collects and reads; it does not fix.

---

## Part 2: The template (blank)

Fields marked **(M)** are mandatory before the ticket can be saved in the Copilot category. Fields marked **(C)** are conditionally mandatory; the condition is stated. Everything else is recommended.

### Section 0: Ticket header

| Field | Value |
|---|---|
| Ticket ID | (system generated) |
| Opened (date, time, time zone) **(M)** | |
| Channel (portal, phone, walk-up, chat, email) **(M)** | |
| Requester name and UPN **(M)** | |
| Department **(M)** | |
| Building or site, and whether on VPN or agency network at time of issue | |
| Preferred contact and availability | |
| Requester's stated urgency and business reason | |
| Agency-assessed priority (set by analyst after Section 7) **(M)** | |
| Copilot license wave, if known (see background facts) | |

### Section 1: Who - scope

| Field | Value |
|---|---|
| Scope **(M)** | [ ] One user [ ] Several users, same team [ ] Several users, several departments [ ] Whole agency |
| Number of users affected (estimate) **(M)** | |
| Affected users' UPNs (with their consent) or team name | |
| Did the requester ask nearby colleagues whether they see the same thing? Result | |
| Parent ticket ID if this is one of several identical reports | |

**Stop rule.** If three or more users report the same symptom within about fifteen minutes, or a whole team reports at once, link this ticket to a parent, record the time of the first report, and run the Service health check in Section 6 before any other step (Decision Tree, Branch S).

### Section 2: Where - surface, client, device, account

| Field | Value |
|---|---|
| Application **(M)** | [ ] Microsoft Copilot app [ ] Teams [ ] Outlook [ ] Word [ ] Excel [ ] PowerPoint [ ] OneNote [ ] SharePoint [ ] Copilot Studio or Agent Builder [ ] Admin center report [ ] Other: |
| Mode **(C: mandatory for Copilot app, Teams and Outlook chat tickets)** | [ ] Work (organizational grounding) [ ] Web [ ] Not applicable or unknown |
| Client **(M)** | [ ] Desktop app [ ] Browser (which browser) [ ] Mobile app [ ] Teams desktop [ ] Web app (Word for the web and similar) |
| Device **(M for desktop tickets)** | [ ] Assigned laptop or desktop [ ] Shared workstation [ ] Mobile [ ] Personal device [ ] Other. Device name if known: |
| Signed-in account as observed in File > Account or profile menu **(C: mandatory for desktop Office tickets)** | |
| How the user opens Copilot (ribbon button, Teams left rail, Copilot app URL, taskbar pin, Outlook toolbar, other) | |
| Network location at time of issue (office, VPN, home, mobile network) | |
| For agent tickets: agent name exactly as shown, and whether any other agents are visible **(C)** | |
| For report tickets: report name, tab, time window, and when it was viewed **(C)** | |

### Section 3: What - expected versus observed

| Field | Value |
|---|---|
| Requester's description in their own words (verbatim, unedited) **(M)** | |
| What the requester expected to happen **(M)** | |
| What actually happened **(M)** | |
| Exact prompt used, if the ticket is about an answer, a document, or an agent **(C)** | |
| Exact error text, if any, copied not paraphrased **(C: mandatory when an error appeared)** | |
| Citation or document Copilot returned, if the ticket is about content **(C)** | |
| Feature the requester was trying to use | [ ] Chat or Q and A [ ] Summarize [ ] Draft or rewrite [ ] Inline document editing [ ] Data analysis in Excel [ ] Meeting recap [ ] Email draft or summary [ ] Agent [ ] Web-grounded answer [ ] Scheduled prompt [ ] Image generation [ ] Other: |
| Screenshot or photo attached **(M: yes or no, with reason if no)** | |
| Does the requester compare to a colleague, a video, a demo, or a personal (consumer) Copilot? Note which | |

### Section 4: When - timeline

| Field | Value |
|---|---|
| When did it last work? (date and time, or "never") **(M)** | |
| When did it first fail or first appear wrong? (date and time) **(M)** | |
| Frequency | [ ] Every time [ ] Intermittent [ ] Once [ ] Only in one location or on one device |
| Reproducible on demand while on the call? **(M)** | [ ] Yes [ ] No [ ] Not attempted (reason) |
| Time zone used for all times in this ticket **(M)** | |

### Section 5: What changed - differential

Tick everything the requester or the analyst knows changed between last-worked and first-failed. Record the date where known.

| Change | Yes | Date or detail |
|---|---|---|
| Copilot license assigned, removed or moved between groups | [ ] | |
| Requester's department, role, or group memberships changed | [ ] | |
| New device, reimaged device, or moved to a shared workstation | [ ] | |
| Office or Windows update installed | [ ] | |
| Content moved, renamed, deleted, restored, re-versioned, or re-shared | [ ] | |
| Site permissions changed or a site placed under Restricted Content Discovery | [ ] | |
| Agent created, shared, published, blocked, or owner left the agency | [ ] | |
| Network, proxy, VPN or allow-list change | [ ] | |
| Tenant policy change (web grounding, agent access, Copilot settings) | [ ] | |
| Microsoft change announced in Message center (record MC identifier) | [ ] | |
| Nothing known to have changed | [ ] | |

### Section 6: Evidence collected at intake

Tier 1 collects and reads. No setting is changed. Record the result and the time of every check performed. Skip checks that do not apply and say why.

| Check | Performed | Result | Time |
|---|---|---|---|
| License assigned? Users > Active users > user > Licenses and apps. Base plan present (Microsoft 365 G5, G3, F1; Office 365 G5, G3, G1, F3)? Date of assignment if recent **(C: mandatory for Branch A tickets)** | [ ] | | |
| Service plans: expand Apps under the license; any Copilot plan unchecked? If AI Administrator support is available, Copilot Service Plan Diagnostic result (Support > Help and support > "copilot missing") | [ ] | | |
| File > Account: product, version, build, update channel, signed-in account. Build above 20131.20000 (Version 2606 or later) or Current Channel? **(C: mandatory for desktop Office tickets)** | [ ] | | |
| Sign-out, sign-in and full app restart performed? Result | [ ] | | |
| Second client test: same action in a browser (Copilot app or Word for the web). Result | [ ] | | |
| Second network test, if feasible: off VPN or another building. Result | [ ] | | |
| Direct-open test: can the user open the document in the browser from SharePoint or OneDrive? **(C: mandatory for find-my-file and wrong-version tickets)** | [ ] | | |
| Organization-wide search test: does the SharePoint start page find the document by title? | [ ] | | |
| Citation opened: which document, which site, which version did Copilot actually use? | [ ] | | |
| Health > Service health checked: any incident or advisory for Microsoft Copilot or the Microsoft 365 suite? Record ID, status, start time **(M for scope of three or more users; recommended for all)** | [ ] | | |
| Web grounding context: which mode was the user in, and does the tenant's recorded policy (Option 3) allow web there? Is the Web content toggle visible? **(C: mandatory for no-web-results tickets)** | [ ] | | |
| Agent Registry (with AI Reader): agent status, availability scope, owner, platform **(C: for agent tickets, if Tier 1 holds read access; otherwise mark for Tier 2)** | [ ] | | |
| Report check: window viewed, latency edge (last 48 hours), active definition, correct report for licensed or unlicensed users **(C: for report tickets)** | [ ] | | |
| Screenshots and attachments stored on the ticket | [ ] | | |

### Section 7: Expected-behavior screen

Before classifying, test the symptom against the known non-failures. If any box is ticked, the ticket is likely expected behavior; explain it to the user and record that you did.

| Known non-failure | Applies | Explained to requester |
|---|---|---|
| License assigned within the last 4 hours (provisioning window) | [ ] | [ ] |
| Web grounding requested in Work mode while the tenant runs Option 3 (off in Work mode, on in Web mode and Copilot Chat); toggle hidden by design | [ ] | [ ] |
| Feature not yet available in GCC: inline editing (Edit with Copilot) in Word, Excel, PowerPoint or OneNote; Word, Excel or PowerPoint Agents; Scheduled Prompts; Copilot app on Mac desktop; Copilot Chat in the Edge sidebar; Excel structured data analysis at commercial parity | [ ] | [ ] |
| Report discrepancy falls within the 48-hour reporting latency (72 hours for the readiness report), or the activity does not meet the active definition (opening the pane does not count) | [ ] | [ ] |
| Desktop build below 20131.20000 (Semi-Annual 2508) on a device scheduled for Version 2606; Copilot in desktop Office not yet eligible | [ ] | [ ] |
| Agent not shared with or assigned to this user (scope, not fault) | [ ] | [ ] |
| Document not accessible to the user directly (permissions), or on a site under Restricted Content Discovery (discoverability by design) | [ ] | [ ] |
| Different wording from a previous run of a similar prompt (expected nondeterminism) | [ ] | [ ] |
| Requester compared to consumer Copilot or a commercial tenant demo | [ ] | [ ] |
| Policy message shown (data loss prevention or sensitivity label acting as designed) | [ ] | [ ] |

### Section 8: Classification (the six outputs from slide 36)

| Output | Value |
|---|---|
| 1. Affected user(s) and affected experience (one sentence) **(M)** | |
| 2. Likely troubleshooting layer, primary **(M)** | [ ] 1 Identity and Entitlement [ ] 2 Administrative Policy [ ] 3 Client and Application [ ] 4 Data and Permissions [ ] 5 Service [ ] 6 Request and Expectation |
| 2a. Secondary layer, if the ticket straddles two | |
| 2b. Decision Tree branch followed and node reached **(M)** | Branch: [ ] S [ ] A [ ] B [ ] C [ ] D [ ] E [ ] F [ ] G. Node reached: |
| 3. Evidence required and first check performed, with result **(M)** | |
| 4. Administrative surface to investigate **(M)** | [ ] Users > Active users (license) [ ] Service Plan Diagnostic [ ] Copilot > Settings [ ] Cloud Policy (web search) [ ] Agents > All agents > Registry [ ] Health > Service health [ ] Reports > Usage [ ] SharePoint admin center [ ] Microsoft 365 Apps admin center [ ] Purview [ ] None required |
| 5. User action recommended, in plain language **(M)** | |
| 6. Escalation required? **(M)** | [ ] No, resolved at Tier 1 [ ] No, expected behavior explained [ ] Yes [ ] Pending evidence (state what) |
| 6a. Escalation destination **(C: mandatory if Yes)** | [ ] Tier 2 Copilot Operations [ ] Tier 3 Identity [ ] Tier 3 Endpoint [ ] Tier 3 SharePoint [ ] Tier 3 Networking [ ] Tier 3 Purview or Compliance [ ] Tier 3 Power Platform or agent developer [ ] Agent owner (sharing request) [ ] Content owner [ ] Policy request to CIO office [ ] Microsoft Support (Tier 2 opens) |
| 6b. Ready-to-escalate checklist **(C: all must be true before escalating)** | [ ] Five facts complete [ ] Evidence section results recorded with times [ ] Expected-behavior screen completed [ ] Branch and node recorded [ ] Attachments stored [ ] User informed of hand-off and next update time |

### Section 9: Communication log

| Date and time | To whom | What was said (summary) | Next update promised |
|---|---|---|---|
| | | | |

Standing phrases that carry authority rather than apology: "This is working as designed under agency policy; here is the alternative." "Microsoft is reporting [ID]; here is the impact statement and the next update time." "Your license was assigned at [time]; the client picks it up after a sign-out and sign-in; I will check back at [time]."

### Section 10: Resolution and closure (completed by the closing tier)

| Field | Value |
|---|---|
| Closed by (tier and analyst) **(M)** | |
| Confirmed root cause **(M)** | [ ] License not assigned [ ] License provisioning window [ ] Service plan disabled [ ] Wrong or multiple accounts [ ] Client build below eligibility [ ] Client not Microsoft 365 Apps for enterprise or device-based licensing [ ] Office privacy setting or add-in [ ] Network or allow-list [ ] Web grounding policy (expected) [ ] Feature not in GCC (expected) [ ] Agent scope or sharing [ ] Agent lifecycle state (blocked, ownerless, pending, deleted) [ ] Agent dependency (connector, license, environment) [ ] Permissions [ ] Indexing delay [ ] Restricted Content Discovery or Restricted SharePoint Search [ ] Superseded or duplicate content [ ] Prompt grounding [ ] Expected nondeterminism [ ] Reporting latency or definition [ ] Data loss prevention or label policy (expected) [ ] Confirmed Microsoft incident (record ID) [ ] Other (describe) |
| Was this a Copilot failure? **(M)** | [ ] Yes [ ] No. One-line reason: |
| Resolution action taken and by whom **(M)** | |
| Linked identifiers (Service health ID, Message center MC ID, parent ticket) | |
| Knowledge article used | |
| Knowledge article needed or updated (title, owner) | |
| Time to resolution (opened to closed) **(M)** | |
| Repeat incident? (same requester or same root cause within 30 days) **(M)** | [ ] Yes [ ] No |
| Follow-up scheduled (for provisioning and device-update tickets) | |

### Section 11: Telemetry tags (populated from the fields above; used for the monthly analysis on slide 41)

| Tag | Source field |
|---|---|
| Category | Section 8, primary layer, plus "How-to or prompting" when Section 10 root cause is prompt grounding or expected nondeterminism |
| Application | Section 2, Application |
| Department | Section 0 |
| Root cause | Section 10 |
| Expected behavior (yes or no) | Section 7, any box ticked and confirmed at closure |
| Copilot failure (yes or no) | Section 10 |
| Escalated (yes or no) and destination | Section 8 |
| Time to resolution | Section 10 |
| Repeat incident | Section 10 |

---

## Part 3: Field guidance - why each field exists and how to collect it fast

| Field | Why it matters | How to collect in under a minute | Common mistake |
|---|---|---|---|
| Scope | Decides whether Service health runs first. One user with three symptoms is three tickets; twenty users with one symptom is one investigation. | "Is anyone sitting near you seeing this too?" Check the queue for identical subjects in the last hour. | Recording the requester as the scope when the requester is reporting for a team. |
| Application and Mode | Web grounding, agent visibility and most Layer 2 questions turn on mode; channel eligibility and most Layer 3 questions turn on application and client. | "Which app were you in? Was the little toggle set to Work or Web?" | Writing "Copilot" as the application. |
| Client and Device | Separates the desktop build question from everything else. Shared workstations at GPO are on a different update schedule than assigned laptops. | "Are you on your own laptop or a floor workstation? What is the computer name on the sticker?" | Not asking, then discovering at Tier 2 that the device is a Semi-Annual 2508 kiosk. |
| Signed-in account | Personal accounts, second agency accounts and stale sign-ins are a top Layer 3 cause; multiple account access to Copilot is always disabled in GCC. | "In Word, click File, then Account, and read me the email under User Information." | Assuming the account is correct because the user says so. |
| Verbatim description | Preserves the user's actual words for the analyst who never spoke to them. Also the raw material for Tier 0 FAQ wording. | Type what they say. Do not clean it up. | Rewriting the complaint into a diagnosis. |
| Expected versus observed | The gap between the two is the ticket. Expectation tickets reveal themselves here. | "What did you think would happen? What happened instead?" | Capturing only the observed half. |
| Exact prompt | Answer-quality, find-my-file and agent tickets are unreproducible without it. | "Can you paste the exact words you typed?" Or ask them to screenshot the conversation. | Accepting "I asked it to summarize the policy." |
| Exact error text | Distinguishes policy messages (expected) from technical errors; matches Service health impact statements. | "Read me the message word for word, or send a screenshot." | Paraphrasing "something about an error." |
| Citation | The document Copilot actually used. Tells the wrong-version story in one click. | "Click the number next to the answer. What document opens, and which site is it on?" | Never opening it. |
| Last worked and first failed | Correlates with license changes, Service health onset, Message center changes, device updates. | "When did this last work for you? When did you first notice?" | Accepting "recently." |
| What changed | Points at the layer before any check. Users often know: "I got a new laptop Friday," "my manager added me to the group yesterday." | Read the checklist aloud; tick what they recognize. | Skipping it because the user says "nothing changed." Ask anyway; then check the license assignment date and the change log. |
| File > Account build | One dialog separates "licensed this morning" from "device below the eligibility threshold." Builds above 20131.20000 indicate Version 2606 or later. | "File, Account, About Word. Read me the version and build." Screenshot preferred. | Recording the channel label from Intune instead of the build from the device. |
| Second client and second network | Cheapest isolation tests available. Browser working and desktop failing is Layer 3; both failing on two networks with no policy message points to entitlement, policy, data or service. | "Open office.com in Edge and try the same thing. Now try off VPN if you can." | Reinstalling Office before running either test. |
| Direct-open test | If the user cannot open the file without Copilot, Copilot is right. Ends most find-my-file tickets. | "Open SharePoint in your browser and open the document directly. Does it open?" | Treating a permissions denial as a Copilot failure. |
| Service health check with time | Turns a guess into evidence; matches onset to first report. | Health > Service health; note ID, status, start time, and the clock time you looked. | Checking once, not recording when, then quoting it hours later. |
| Expected-behavior screen | Seven in eight tickets are not failures. Screening first keeps the incident count honest and gets the user a real answer faster. | Walk the ten rows; tick what applies; explain it on the same call. | Skipping the screen and escalating expected behavior to Microsoft. |
| Branch and node | Tells Tier 2 exactly where Tier 1 stopped and why. | Record the letter and the node text, for example "Branch A, node: desktop eligible? answer No." | Escalating with a symptom and no path. |
| Confirmed root cause and "was this a Copilot failure?" | The two fields that make the monthly analysis true. | Set at closure by whoever closes. Reason in one line. | Leaving the initial guess as the root cause. |

---

## Part 4: Recommended picklists for the ticketing system

Configure these as controlled values so the monthly analysis can count them. Add values through Tier 2 change control only.

**Application:** Microsoft Copilot app; Teams; Outlook; Word; Excel; PowerPoint; OneNote; SharePoint; Copilot Studio; Agent Builder; Admin center report; Other.

**Mode:** Work; Web; Not applicable; Unknown.

**Client:** Desktop app; Browser, Edge; Browser, other; Mobile app; Teams desktop; Web app.

**Device:** Assigned laptop or desktop; Shared workstation; Mobile; Personal device; Other.

**Symptom family (Decision Tree branch):** S Multi-user sudden; A Copilot missing or not appearing; B Cannot find a file or wrong version; C No web results; D Agent missing or cannot use; E Wrong, weak or inconsistent answer; F Usage report looks wrong; G Error message or feature fails.

**Layer:** 1 Identity and Entitlement; 2 Administrative Policy; 3 Client and Application; 4 Data and Permissions; 5 Service; 6 Request and Expectation.

**Escalation destination:** Tier 2 Copilot Operations; Tier 3 Identity; Tier 3 Endpoint; Tier 3 SharePoint; Tier 3 Networking; Tier 3 Purview or Compliance; Tier 3 Power Platform or agent developer; Agent owner; Content owner; Policy request to CIO office; Microsoft Support.

**Confirmed root cause:** the list in Section 10. Keep "Expected" values distinct from failure values so the two can be counted separately.

**Expected-behavior reason:** Provisioning window; Web grounding policy Option 3; Feature not in GCC; Reporting latency or definition; Client build below eligibility pending 2606; Agent scope; Permissions or Restricted Content Discovery; Expected nondeterminism; Consumer or commercial comparison; DLP or label policy.

**Feature requested (for the "not in GCC" analysis):** Inline document editing; Excel structured data analysis; Word, Excel or PowerPoint Agent; Scheduled prompt; Copilot in Edge sidebar; Copilot on Mac desktop; Schedule with Copilot in Outlook; Other.

---

## Part 5: Tier 1 phone script (six to eight minutes)

Read the section numbers as you go so the ticket fills in order.

**Open (Section 0).** "Thanks for calling. I am going to ask a set of questions so that whoever works this next does not have to call you back. Which department are you in, and are you in the office or on VPN right now?"

**Scope (Section 1).** "Is this happening just to you, or have colleagues mentioned the same thing? Roughly how many?" If three or more, say: "I am going to check Microsoft's service status before we go further," and do it.

**Where (Section 2).** "Which app were you in when this happened? Were you on your own laptop or a shared workstation? If you were in the Copilot app or Teams, was the toggle on Work or Web? How do you normally open Copilot?" For desktop Office: "Click File, then Account. Read me the email address under User Information, then click About and read me the version and build."

**What (Section 3).** "In your own words, what happened?" Type it exactly. "What did you expect to happen? If you typed a prompt, can you paste it into the chat with me, or take a screenshot? If there was an error message, read it to me word for word." For content tickets: "Click the citation number by the answer. What document opens and which site is it on?"

**When (Section 4).** "When did this last work? When did you first notice it? Does it happen every time? Can you try it right now while we are on the phone?"

**What changed (Section 5).** "Since it last worked, did anything change: a new license, a new laptop, a different desk, a document that moved, a new group, an Office update you noticed?" Read the checklist.

**Evidence (Section 6).** "Let us try two quick things. Open Edge, go to office.com, sign in with your agency account and try the same action. Now sign fully out of the desktop app and back in." Record results. For content: "Open the document directly from SharePoint. Does it open?" Check Service health and record the time.

**Expected-behavior screen (Section 7).** Walk the rows silently. If one applies, explain it now with the standing phrase, and record that you explained it.

**Classify (Section 8).** Follow the Decision Tree. Record the branch and node. Tell the user the outcome and the next step.

**Close the call (Section 9).** "Here is what I found, here is what to do now, and here is when you will hear from us." Record it.

---

## Part 6: Worked example (completed template)

This example uses Ticket F from the triage exercise. Values are fictional.

### Section 0: Ticket header

| Field | Value |
|---|---|
| Ticket ID | INC-2026-09-4472 |
| Opened | Tuesday, September 29, 2026, 08:55 ET |
| Channel | Walk-up, production floor help desk |
| Requester | Press operator and shift lead, demo.shiftlead@gpo.gov |
| Department | Production Operations |
| Building and network | Production floor, Building C; agency network, not VPN |
| Preferred contact | Desk phone on the floor, before 14:00 shift change |
| Stated urgency | Medium. "I can work around it but it is confusing." |
| Agency-assessed priority | Low. Expected behavior with a dated remediation; workaround available. |
| License wave | Wave 3, July 8, 2026 |

### Section 1: Who

| Field | Value |
|---|---|
| Scope | One user reporting; likely applies to all users of the shared production-floor workstations |
| Number affected | 1 reported; up to about 40 potentially (workstation users) |
| Others asked? | Requester asked two colleagues on the same shift; both said "we just use the browser" |
| Parent ticket | None; not a sudden multi-user event |

### Section 2: Where

| Field | Value |
|---|---|
| Application | Word (Copilot button absent); Copilot app in Edge works |
| Mode | Not applicable for Word; Work mode in the Copilot app works |
| Client | Desktop app (Word); Browser, Edge (Copilot app) |
| Device | Shared workstation, PROD-KIOSK-17 |
| Signed-in account | demo.shiftlead@gpo.gov (confirmed in File > Account) |
| How Copilot is opened | Expected the Word ribbon button; uses Copilot app URL in Edge |
| Network location | Office, agency network |

### Section 3: What

| Field | Value |
|---|---|
| Verbatim | "When I use the Copilot app in Edge on the floor workstation, Copilot answers my questions about job tickets and even reads our SharePoint files. But when I open Word on the same workstation there is no Copilot button at all. Same login, same computer. My supervisor said everyone in Production got Copilot in July. Do I have half a license?" |
| Expected | Copilot button in the Word ribbon on the workstation |
| Observed | No Copilot button in Word; Copilot app in Edge fully functional with organizational grounding |
| Exact prompt | Not applicable |
| Exact error | None; feature absent, no error |
| Citation | Not applicable |
| Feature requested | Draft or rewrite in Word |
| Screenshot | Yes: photo of About Word dialog attached |
| Comparison | Compared to colleagues in other departments who have the ribbon button |

### Section 4: When

| Field | Value |
|---|---|
| Last worked | Never in desktop Word on the floor workstations |
| First noticed | Around September 22, 2026, after a colleague mentioned the ribbon button |
| Frequency | Every time, on every floor workstation tried (17 and 22) |
| Reproducible now | Yes |
| Time zone | ET |

### Section 5: What changed

| Change | Yes | Detail |
|---|---|---|
| Nothing known to have changed | [x] | Behavior has been constant since the July license assignment |
| Device: shared workstation | [x] | Requester has no assigned laptop; works only from shared workstations |

### Section 6: Evidence

| Check | Performed | Result | Time |
|---|---|---|---|
| License assigned | [x] | Microsoft Copilot assigned via group, July 8, 2026; base plan Microsoft 365 G3 present | 09:02 |
| Service plans | [x] | All Copilot plans checked in Licenses and apps | 09:03 |
| File > Account | [x] | Microsoft 365 Apps for enterprise, Version 2508 (Build 16.0.19127.20268), Semi-Annual Enterprise Channel, last updated August 12, 2026. Build below 20131.20000. Account correct. | 09:05 |
| Sign-out, sign-in, restart | [x] | Performed; no change | 09:08 |
| Second client test | [x] | Copilot app in Edge and Word for the web both show Copilot and work in Work mode | 09:10 |
| Second network test | [ ] | Not applicable; browser test already isolates the client | |
| Direct-open test | [ ] | Not applicable | |
| Service health | [x] | No incidents or advisories for Microsoft Copilot or the Microsoft 365 suite | 09:11 |
| Web grounding context | [ ] | Not applicable | |
| Report check | [x] | Readiness report shows requester with "Uses eligible update channel: No" | 09:13 |
| Attachments | [x] | Photo of About Word dialog stored | 09:13 |

### Section 7: Expected-behavior screen

| Known non-failure | Applies | Explained |
|---|---|---|
| Desktop build below 20131.20000 on a device scheduled for Version 2606 | [x] | [x] Explained at 09:15 |

### Section 8: Classification

| Output | Value |
|---|---|
| 1. Affected experience | One user today, and by extension all shared production-floor workstation users: Copilot in desktop Word on Semi-Annual 2508 devices. Browser Copilot unaffected. |
| 2. Layer | 3 Client and Application |
| 2b. Branch and node | Branch A, node "Desktop eligible? Build above 20131.20000 or Current Channel?" answered No |
| 3. Evidence and first check | File > Account showed Version 2508, Build 16.0.19127.20268, Semi-Annual Enterprise Channel, below the eligibility threshold. Browser test confirmed the license and account are fine. |
| 4. Administrative surface | Microsoft 365 Apps admin center (inventory and Cloud Update schedule for PROD-KIOSK workstations); readiness report confirms channel status |
| 5. User action | Use Word for the web from the workstation until the device receives Version 2606 the week of October 5. The license is complete; the desktop app on this device is not yet eligible and is also out of support since September 8. |
| 6. Escalation | Yes, as a confirmation rather than a repair |
| 6a. Destination | Tier 3 Endpoint: confirm PROD-KIOSK-17 and the workstation group are in the October 5 Cloud Update onboarding set. Separately, log a governance question for the CTO and license administrator on individual licensing for shared-workstation users (Copilot is not supported with device-based licensing; each user must sign in as themselves). |
| 6b. Ready-to-escalate | All boxes checked |

### Section 9: Communication log

| Date and time | To whom | Summary | Next update |
|---|---|---|---|
| Sep 29, 09:15 | Requester | Explained that the license is complete and the workstation's Word build is below the Copilot threshold until the October 5 update; showed Word for the web as the workaround; confirmed colleagues' browser use is the same situation | Oct 6, after the device update window |
| Sep 29, 09:20 | Tier 3 Endpoint queue | Requested confirmation of onboarding set and post-update build check | Oct 5 |

### Section 10: Resolution and closure

| Field | Value |
|---|---|
| Closed by | Pending: Tier 1 holds the ticket open with a follow-up date; closure expected October 6 after build verification |
| Confirmed root cause | Client build below eligibility (Semi-Annual 2508, Version 2606 pending) |
| Was this a Copilot failure? | No. The desktop app on this device is below the eligible build; browser Copilot works with the same license and account. |
| Resolution action | Workaround provided (Word for the web); device update scheduled by Endpoint; governance question logged |
| Linked identifiers | Message center MC1274325 (channel unification); readiness report, September 26 |
| Knowledge article used | "Copilot is missing: shared workstations and the update channel" |
| Article needed | Add the workstation group and October 5 date to the article; add a line that Version 2508 is out of support since September 8 |
| Time to resolution | Open; target 7 days |
| Repeat incident | No, but expect similar reports from other workstation users until October 5; link them to this ticket |
| Follow-up | October 6: verify build above 20131.20000 on PROD-KIOSK-17; confirm Copilot button in Word; close |

### Section 11: Telemetry tags

Category: 3 Client and Application. Application: Word. Department: Production Operations. Root cause: Client build below eligibility. Expected behavior: Yes. Copilot failure: No. Escalated: Yes, Tier 3 Endpoint (confirmation). Repeat: No.

---

## Part 7: Implementation notes for the ticketing system

**Mandatory field enforcement.** The Copilot category cannot be saved without Section 0, Section 1 scope and count, Section 2 application and client, Section 3 verbatim, expected and observed, Section 4 last-worked and first-failed with time zone, and Section 8 outputs 1, 2, 3, 4, 5 and 6. Everything marked (C) becomes mandatory when its condition is met; implement as form logic, not as guidance.

**Conditional logic worth building.**
- Application in (Word, Excel, PowerPoint, Outlook, OneNote) and Client = Desktop app: require File > Account fields (account, version, build, channel).
- Scope of three or more users: require the Service health check with time before saving; auto-suggest linking to an existing parent ticket with a matching subject in the last hour.
- Symptom family in (B, E): require exact prompt and citation.
- Symptom family = C: require Mode and the web grounding context check.
- Symptom family = D: require agent name and "other agents visible" answer.
- Symptom family = F: require report name, window and time viewed.
- Escalation = Yes: block until the ready-to-escalate checklist is complete.

**Two-field root cause.** Keep Section 8's primary layer (initial classification) and Section 10's confirmed root cause as separate fields. The monthly review measures the second and uses the gap between them to tune Tier 1 training.

**Time stamps on evidence.** Every row in Section 6 carries a time. Service health in particular is only meaningful with a "checked at" time, because the answer changes.

**Privacy and data handling.** Prompts and responses can contain sensitive content. Store them on the ticket under the agency's data handling rules, restrict the Copilot category's visibility to the support tiers, and do not export prompt text into the monthly analysis. When user names feed the analysis, follow the same anonymization policy the agency applies to the admin center usage reports. Obtain consent before listing other users' UPNs in Section 1. For Microsoft support requests, confirm what may be shared before attaching prompts, responses or diagnostics logs.

**Read, do not change.** No field in this template asks the analyst to change a setting, a license, a policy or a permission. If the ticketing form includes a "resolution action" free-text field at intake, remove it; resolution belongs in Section 10 and to the tier that owns the change.

**Keep it current.** The expected-behavior screen and the "feature requested" picklist reference the GCC feature state as of September 2026 (Edit with Copilot, Scheduled Prompts and Office agents not yet available; Microsoft 365 G7 and Agent 365 purchasable from October 1, 2026 with capabilities phased in). Review both quarterly against the Microsoft Copilot service description feature availability table and the Microsoft 365 Roadmap filtered to GCC, and immediately when the web grounding decision changes. Record changes in the revision log below.

**Definition of complete intake.** The five facts recorded; at least the applicable evidence checks performed with results and times; the expected-behavior screen walked; six classification outputs written; the user told what happens next. A Tier 2 analyst should be able to open the ticket and take the next investigative step without contacting the requester.

---

## Revision log

| Version | Date | Change |
|---|---|---|
| 1.0 | September 29, 2026 | Initial release aligned to the Day 7 Copilot Operations course, the Copilot Triage Decision Tree v1.0 and the six triage outputs on slide 36. |
