# Team Lifepoint "Ready to Serve": project handoff

Paste this whole file into a new chat to carry on where we left off. It records what's been decided, what's built, and what's still open.

Last updated: 17 November 2026.

---

## 1. What this is

Lifepoint Church (Rothwell and Caboolture West, Qld; part of Queensland Baptists) is deciding whether to replace **Safe Ministry Check**, which costs $0.49 per volunteer per month (about $2,000 a year for about 350 volunteers), with its **own branded app**.

The app takes every volunteer through onboarding and child-safe checks, then issues a **Team Lifepoint** clearance certificate.

**Owner:** Dan Sweetman, Senior Pastor. Dan prefers short answers in chat, anything longer as markdown (not .docx), and wants to be asked before any long piece of work starts.

**Status:** Still deciding whether to go ahead. A clickable mockup exists for the pastors and team to review. The full design document is **on hold** until Dan says go.

---

## 2. Where things are

| What | Where |
|---|---|
| Clickable mockup (published) | https://claude.ai/artifact/HMkBEwXjWLN15aar6gLfwu (shared: anyone with the link) |
| Code repository | GitHub `deetsweet/stafftraining`, branch `claude/volunteer-vetting-system-design-fpepu6` |
| Mockup source | `mockup/index.html`: one self-contained HTML file with logos, fonts and photos embedded |
| Logos (SVG) | `brand/logos/`: badge, primary and secondary, in white and black |
| Script font | `brand/fonts/PortraitScript-Alts-Bold.otf` (check the web licence before the real build) |
| Dan's headshot | `brand/photos/dan-sweetman-headshot.jpg` |
| Brand guide | *Lifepoint Brand Guide 2026-10* (PDF, Dan has it) |
| Team handbook | *Team Lifepoint Handbook (draft)* (PDF, Dan has it). The source for induction content |

### Signature
- **No signature on the certificate.** Dan removed it and doesn't want his signature anywhere. The certificate shows his name and title under a plain line.
- **Never add a signature image to the app or the repository.**
- To update the **same** mockup link, publish `mockup/index.html` with `url: https://claude.ai/artifact/HMkBEwXjWLN15aar6gLfwu`. Otherwise a separate page is created.

---

## 3. Decisions made

### Scope and policy
- **Every volunteer** on Team Lifepoint goes through the process, not just children's ministry.
- **Everyone needs a Blue Card**, Queensland's Working With Children Check, because *"young people are involved everywhere in our church."*
- They are called **Team Lifepoint** members, and finishing earns a **"Lifepoint Team Member"** certificate.

### Build approach
- A **full custom branded app**, not a Google Forms setup.
- It works as a website that behaves like an app on phones, with no app store.
- Rough running cost: about $50–80 AUD a month for hosting, database and email.
- Built and maintained with Claude.

### Volunteer journey (six steps)
1. **Your details**: filled in from ChurchSuite; the volunteer confirms.
2. **Welcome to Team Lifepoint**: about 10 minutes of swipeable cards drawn from the handbook.
   - Mission, plus a welcome video from Dan
   - Our story
   - The three values, with "On a team" tips
   - How we do things here (8 culture points)
   - Your commitments, and our commitment to you
   - Ends with an **"I'm in"** tap, and links to the full handbook.
   - **Do not use "We make the path by walking."** Dan removed it: "we take our mission seriously."
3. **Safe Spaces training**: 5 short videos and a quiz. The quiz must be passed, and wrong answers prompt a retry.
4. **Code of conduct**: read, then sign with a finger. Uses the handbook's "What every team member must do" rules. Versioned (v2026.1), with re-signing when it changes.
5. **Two referees**: at least 2 years known, not family. They're emailed automatically and chased if they don't reply.
6. **Blue Card**: card number and expiry, plus "I've linked Lifepoint in the portal", with help for people without a card.

Finishing shows a **"You're cleared to serve"** screen, then the **certificate**.

### Referee form
- Modelled on how Safe Ministry Check's form works, with **our own wording**.
- Tap-to-answer statement cards, each with a **green** (no issue) and a **red** (possible issue) button.

| Section | Statement | Green | Red |
|---|---|---|---|
| About you | "My name is [referee]." | That's me | That's not me |
| | "I've known [volunteer] for at least two years." | Yes | No, less than that |
| | How do you know them? | dropdown, no colour | |
| About [volunteer] | "…never been accused of harming or mistreating anyone." | That's right | There may be an issue |
| | "I would trust [them] to care for children and vulnerable people." | I agree | I have doubts |
| | "There's nothing… Lifepoint should know before [they] start volunteering." | Nothing to raise | I have a concern |

- **Any red answer** opens a comment box and a "Kept private" panel asking for a phone number.
- The referee must tick "true to the best of my knowledge" before submitting.
- The **volunteer never sees** the answers. If there's a concern, the volunteer only sees "Both replied · the office will be in touch."
- Referee links are unique, expire after 14 days, and stop working once used.

### Certificate
- **A4 landscape PDF.**
- Charcoal left panel with the white primary logo, a large Sage badge, the certificate number and the date issued.
- Linen right panel:
  - "this is to certify that" (script)
  - the volunteer's **name**
  - "…officially cleared to join **TEAM LIFEPOINT**"
  - "as a Lifepoint Team Member · [team]"
  - four ticks: training, code of conduct, referees, Blue Card
  - "Dan Sweetman, Senior Pastor, Lifepoint Church" under a plain line, with no signature
- **"Valid until"** is the earlier of the training refresher (1 year) and the Blue Card expiry.
- It's emailed to the volunteer and saved on their record.

### Blue Card checking
- **Queensland has no official API** for this, and Blue Card Services has said it has no plans to publish one.
- Safe Ministry Check "auto-validates" by filling in the government's public **"Check if a blue card is valid"** web form (name, card number, expiry). Their own post says it broke when the government's site changed.
- **Dan's view:** build the same auto-check, and fix it with Claude when it breaks. Ground rules:
  - **Fail safe.** On any error, mark the card "needs manual check" and email an admin. It must never show "valid" by mistake.
  - **Daily self-test** on a known card.
  - **Ask Blue Card Services first** whether automated use of the form is allowed.
  - **Keep linking every volunteer in the Organisation Portal.** That's a legal requirement, and it's how the government notifies you of suspended or cancelled cards.
- **Not yet checked:** whether the government form has a "not a robot" test. The session's network blocked the site.
- **Fallback:** a 30-second manual check. The admin screen shows the details with copy buttons, plus a "Verified" button that records who checked and when.

### ChurchSuite
- ChurchSuite **has an API** (with an API key). Exact tag and custom-field endpoints are still to be confirmed.
- **How it starts:** a team leader adds the person to a fixed tag such as **"Team Lifepoint – Onboarding"** in ChurchSuite. The app picks them up and sends an invite by text and email, with their details already filled in.
- **When they're cleared:** the app moves them to **"Team Lifepoint – Cleared"** and sets custom fields ("Cleared until", "Blue Card expiry"). The tag comes off automatically if anything lapses.
- **ChurchSuite** holds who people are. **The app** holds the sensitive records: referee reports, disclosures, signatures and Blue Card checks.
- **Fallback:** a weekly CSV export and import.
- **Existing ~350 volunteers:**
  - Import their history from a Safe Ministry Check export (do this **before** cancelling).
  - Mark currently cleared people as cleared.
  - Send each person into the app when their next renewal is due.
  - Do a one-off catch-up of the induction and the Blue Card requirement for everyone over a couple of months.
  - Run Safe Ministry Check in parallel for one intake before switching.

### Sign-in and roles
- **Volunteers:** no passwords. The invite link logs them in; after that, a one-time code by email or text. They stay signed in on their phone for about 30 days.
- **Referees:** no login, just their single-use link.
- **Staff:** sign in with their Lifepoint Google Workspace account, with two-step verification. Switching off someone's Google account removes their access.

| Role | Can see | Can't see |
|---|---|---|
| Volunteer | Only their own steps and certificate | Anyone else, and their referees' answers |
| Team leader | Their own team's status | Referee reports, concern details, Blue Card numbers |
| Office admin | Everyone's progress. Can verify Blue Cards, send invites and reminders | Referee reports and concern details |
| Safe Spaces Coordinator | Everything, including referee reports. Records outcomes | |
| Senior Pastor | Everything, plus managing roles | |

- **Every view** of a sensitive record is logged.
- **Admins are logged out** automatically after a period of inactivity.
- **Records can't be deleted.** Changes keep their history, and records are kept for 45 years.

### Names (match the handbook)
- **"Safe Spaces training"**, not "Safe Volunteers".
- **"Safe Spaces Coordinator"**, not "child safety officer".

### Accounts
- **Claude:** don't share one login. Use a **Claude Team plan**, with a seat for each pastor under the church account.
- **Everything else should be church-owned, not personal:**
  - a GitHub organisation (move the repository out of Dan's personal account)
  - hosting
  - the email-sending service
  - the web address, e.g. safe.lifepoint.org.au
- Use a shared church email, with at least two admins on each account.

---

## 4. Brand rules (from the brand guide, plus Dan's corrections)

- **Colours:**

| Name | Hex | Role |
|---|---|---|
| Charcoal | #333333 | primary |
| Linen | #FFFBF0 | primary |
| Deep Blue | #3D6270 | supporting |
| Sage | #71806D | supporting |
| Stone | #E8E4E4 | supporting |
| Mist | #BFCFD7 | tint |
| Moss | #B1B89F | tint |

- **Balance:** Linen 45 · Charcoal 35 · Deep Blue 12 · Sage 8. Start with Linen, and use Charcoal for impact.
- **Blue is for headings and labels only.** Never use it for body text. Body text is white, Linen, grey or black. On Charcoal, use Linen at about 74% opacity rather than Mist.
- **Type:**
  - Futura Medium for headings. The mockup uses **Jost** as the free web stand-in until a Futura web licence is sorted.
  - **Lato** for body text.
  - **Portrait Script Alts Bold** for three or four lower-case words as an eyebrow line.
- **Design elements:**
  - Pill buttons with an arrow (→).
  - An oversized badge cropped off the edge at 5–10% opacity.
  - Event-card style: a photo on top, details on a Charcoal or Linen panel.
  - Corner radius around 22–28px.
- **Photos:** real Lifepoint photos only, no stock images. **Avoid identifiable children's faces in this app.**
- **Writing:** Australian spelling, warm and plain.

---

## 5. Mockup: what's in it

There are three tabs: **Volunteer**, **Referee** and **Admin**. Nothing is saved.

**Volunteer tab**
- Welcome screen with a photo, Dan's message and headshot, and a "Sign in" option.
- The home checklist and progress ring.
- All six steps.
- The "cleared" screen, with confetti and a photo, and the certificate viewer.

Dan's welcome message:
> "Thank you for joining our mission to see thousands of lives transformed by Jesus. These steps are how we make Lifepoint a safe place for everyone who walks through the door."

**Referee tab**
- The invitation email.
- The green/red statement form.
- A thank-you screen.

**Admin tab**
- Staff Google sign-in, then a two-step code.
- A dashed **"View as"** switcher: Senior Pastor, Safe Spaces Coordinator, Office admin, Team leader.
- Tiles: cleared, in progress, expiring, needs attention.
- Search and team filter, and the volunteer table.
- A slide-out record for each volunteer with:
  - checklist
  - referee reports (by role)
  - a logged-view notice
  - Blue Card verify button
  - reminders
- "Manage roles", visible to the Senior Pastor only.

**Sample people:**
- Sarah Mitchell (Welcome team): the live demo person, whose row updates as you use the other tabs.
- Hannah Cole: a referee concern.
- Tom Brennan: one referee still waiting.
- Ben Tran: Blue Card expired.
- Priya Nair and Leah Wright: expiring soon.

---

## 6. Open questions and to-dos

1. **Decide whether to go ahead.** Gather the team's feedback on the mockup.
2. **Ask Safe Ministry Check** exactly how their Queensland auto-validation works and how often it re-checks.
3. **Email Blue Card Services** to ask whether automated use of the public validation form is allowed.
4. **Check the government validation page** for a "not a robot" test.
5. **Get a ChurchSuite API key,** then confirm the tag and custom-field endpoints.
6. **Team leaders and concerns:** should they see "Needs attention", or just "In progress" so nothing is hinted at?
7. **Office admins:** confirm they should see Blue Card numbers but not referee reports.
8. **Font licences:** check web use for Futura and Portrait Script.
9. **Handbook fixes:**
   - Page 4: remove "We make the path by walking."
   - Page 13: make the Blue Card required for everyone, and change "first three" to "first four".
   - Page 15: replace the placeholder "Jase what info do we want here".
10. **Accounts:** set up a Claude Team plan and a GitHub organisation, and move the repository into it.
11. **Optional mockup additions offered:**
    - a team leader's ChurchSuite view and the invite text, to show the full start-to-finish journey
    - a QR code on the certificate so anyone can check it's genuine
12. **When Dan says go:** write the full design document in markdown, covering:
    - the workflow
    - every form and email
    - the data and who can see it
    - the ChurchSuite link
    - a phased build plan with costs

    Phases: (1) core flow, (2) automation and reminders, (3) ChurchSuite sync, then a pilot.
