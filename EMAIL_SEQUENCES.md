# DataLabSync Email Sequences

## Overview

Email sequences are segmented based on user responses to the onboarding quiz, specifically the **engagement preference** question.

---

## Sequence 1: Demo Seekers
**Trigger:** User selected "I'd love to see an early demo"

### Email 1: Immediate Confirmation (Send: Immediately)

**Subject:** You're on the list — let's find a time to talk

**Body:**
```
Hi [First Name],

Thanks for signing up for DataLabSync early access — and for letting us know you'd like to see a demo.

We're still in early development, but we're scheduling discovery conversations with people like you to make sure we're building the right thing.

Would you be open to a 20-minute call in the next week or two? No pitch — just a conversation about your workflows and what would actually help.

Reply to this email with a few times that work, or grab a slot here: [Calendly Link]

Looking forward to it,

Gloire
Founder, DataLabSync
```

### Email 2: Follow-up (Send: Day 3 if no reply)

**Subject:** Still interested in that demo?

**Body:**
```
Hi [First Name],

Just following up on my earlier note. I know inboxes get busy.

If you're still interested in seeing what we're building, I'd love to set up a quick call. If now's not the right time, no worries — I'll keep you posted as we make progress.

Best,
Gloire
```

### Email 3: Value Add (Send: Day 7)

**Subject:** What we're learning from FAS teams

**Body:**
```
Hi [First Name],

Wanted to share something we've been hearing a lot in our conversations with FAS professionals:

The #1 frustration isn't the fieldwork itself — it's the documentation overhead that comes after.

We're building DataLabSync specifically to solve that: guided workflows that capture data as you work, so documentation generates automatically.

If that resonates, I'd still love to chat. Reply anytime.

Gloire
```

---

## Sequence 2: Passive Interest
**Trigger:** User selected "Send me updates, I'll explore when ready" or "I'm just curious for now"

### Email 1: Immediate Confirmation (Send: Immediately)

**Subject:** You're on the DataLabSync waitlist

**Body:**
```
Hi [First Name],

Thanks for joining the DataLabSync early access list.

We'll keep you updated as we hit milestones — no spam, no sales pressure. Just honest updates about what we're building.

In the meantime, if you ever want to share feedback or just say hi, reply to this email. I read everything.

Gloire
Founder, DataLabSync
```

### Email 2: Progress Update (Send: Day 14)

**Subject:** Quick update on DataLabSync

**Body:**
```
Hi [First Name],

Quick update from the DataLabSync team:

We've been heads-down talking to FAS professionals and building the first version of our guided validation workflows. Early feedback has been really encouraging.

A few things we're working on:
- Step-by-step PAR documentation flows
- Automatic validation record generation
- Manager visibility dashboards

We'll share more when there's something to show. Thanks for your patience.

Gloire
```

### Email 3: Beta Invitation (Send: When beta opens)

**Subject:** DataLabSync beta is open — you're invited

**Body:**
```
Hi [First Name],

It's happening — DataLabSync beta is now open to early access members.

As someone who signed up early, you're first in line. Here's what you can expect:

✓ Guided validation workflows (PAR, correlation, AMR)
✓ Automatic documentation generation
✓ Real-time progress tracking

If you'd like to participate, just reply to this email and we'll get you set up.

No pressure if the timing isn't right — we'll keep you posted either way.

Gloire
```

---

## Sequence 3: Pilot Candidates
**Trigger:** User selected "I'd consider a pilot if timing is right" or "I'd want to involve my team or manager"

### Email 1: Immediate Confirmation (Send: Immediately)

**Subject:** Thanks for your interest in piloting DataLabSync

**Body:**
```
Hi [First Name],

Thanks for signing up for DataLabSync early access — and for indicating interest in a potential pilot.

We're building DataLabSync specifically for diagnostics FAS teams, and pilots with real teams are how we'll know if we're getting it right.

When we're ready to run pilots (likely in the next few months), you'll be first to hear about it. In the meantime, if you have questions or want to share more about your team's needs, just reply.

Gloire
Founder, DataLabSync
```

### Email 2: Needs Assessment (Send: Day 5)

**Subject:** Quick question about your team

**Body:**
```
Hi [First Name],

As we prepare for pilot programs, I'm trying to understand what teams would benefit most from DataLabSync.

Would you mind sharing:
- Roughly how many FAS team members do you have?
- What's your biggest documentation or workflow challenge?

No formal survey — just reply with whatever comes to mind. It helps us prioritize.

Thanks,
Gloire
```

### Email 3: Pilot Preview (Send: Day 21)

**Subject:** What a DataLabSync pilot would look like

**Body:**
```
Hi [First Name],

We're getting closer to opening pilot programs, so I wanted to share what participation would involve:

**Pilot Overview:**
- 4-week guided pilot with your team
- Direct access to our team for feedback and support
- Free during pilot period
- No commitment to continue afterward

**What we'd need from you:**
- 2-3 FAS team members willing to try the workflows
- 30-minute kickoff call
- Weekly 15-minute check-ins

If this sounds interesting, reply and let me know. We're prioritizing teams that match well.

Gloire
```

---

## Sequence 4: High-Value Prospects
**Trigger:** User indicated $300+ monthly willingness AND 10+ hours/week admin time

### Email 1: Immediate Confirmation (Send: Immediately)

**Subject:** Thanks for your detailed feedback

**Body:**
```
Hi [First Name],

Thanks for taking the time to complete our discovery quiz. Your responses were really helpful.

It sounds like documentation overhead is a significant challenge for your team. That's exactly the problem we're solving — and your input helps us make sure we get it right.

I'd love to learn more about your specific workflows. Would you be open to a brief call? No pitch — just research.

Reply with a few times that work, or grab a slot here: [Calendly Link]

Gloire
Founder, DataLabSync
```

### Email 2: Case Study Share (Send: Day 4)

**Subject:** How one FAS team saved 8 hours/week

**Body:**
```
Hi [First Name],

Wanted to share a quick story from one of our early conversations:

A 6-person FAS team we spoke with was spending roughly 12 hours/week on documentation and compliance prep. Their biggest pain? Recreating the same validation documents for every installation.

With a workflow-driven approach, they estimated they could cut that to 4 hours/week — without sacrificing compliance quality.

That's the gap we're building DataLabSync to close.

If your team faces similar challenges, I'd love to hear more. Just reply.

Gloire
```

---

## Email Footer (All Sequences)

```
—
DataLabSync | Field Execution Platform for Diagnostics
datalabsync.com

You're receiving this because you signed up for early access.
Reply to unsubscribe — we'll remove you immediately, no hard feelings.
```

---

## Segmentation Logic

| Quiz Response | Email Sequence |
|--------------|----------------|
| Demo interest | Sequence 1: Demo Seekers |
| Updates only / Just curious | Sequence 2: Passive Interest |
| Pilot interest / Involve team | Sequence 3: Pilot Candidates |
| $300+/mo + 10+ hrs/week admin | Sequence 4: High-Value Prospects |

---

## Formspree Integration Notes

All quiz responses are sent to Formspree with the following fields:
- `role`
- `roleOther`
- `currentTools`
- `biggestFrustration`
- `timeSpentOnAdmin`
- `engagementPreference`
- `pricingWillingness`
- `openFeedback`
- `skippedQuestions`
- `completedAt`

Use Formspree's integrations or Zapier to route responses to your email marketing platform (ConvertKit, Mailchimp, etc.) for automated sequence triggers.
