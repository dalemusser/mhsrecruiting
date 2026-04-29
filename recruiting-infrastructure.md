# Recruiting Infrastructure

Inventory of the infrastructure required to recruit, screen, onboard, and track 50+ teachers per cohort. Distinguishes **what already exists** from **what needs to be built**.

The recruiting campaign cannot launch Wave 1 outreach until the items in "Critical gaps" are in place, because every outreach message will direct teachers to a place to learn more, apply, or sign up. If those endpoints don't exist, leads disappear.

---

## Existing Infrastructure (Confirmed)

### Landing page on mhs.missouri.edu
- **Status:** Live
- **Used for:** general project information
- **Recruiting needs:** A dedicated recruiting section or sub-page is recommended. It should include:
  - Cohort timing (Fall 2026, Spring 2027)
  - Teacher value proposition (see [value-proposition.md](value-proposition.md))
  - Eligibility criteria (middle-school earth-science teacher, U.S., iPads or Chromebooks)
  - Pilot teacher testimonials (once captured — see [pilot-teacher-engagement.md](pilot-teacher-engagement.md))
  - Demo video
  - Apply button → application form
  - FAQ
  - IRB / consent language reference

### IRB-Approved Consent + Recruitment Language
- **Status:** Approved
- **Used for:** any recruitment communication and teacher consent
- **Recruiting needs:** Confirm scope — is the existing IRB-approved language usable for nationwide cold outreach, or only Missouri pilots? If scoped to Missouri, an IRB amendment may be needed before broad outreach.

---

## Critical Gaps (Build These First)

### Online Teacher Application + Screening Form
- **Status:** Not built (highest-priority gap)
- **Target live date:** 2026-05-15
- **Why critical:** every outreach message points here. No form, no campaign.
- **Platform options (in order of preference):**
  - **Qualtrics** — preferred. IRB-friendly, Mizzou likely already has a license, supports complex branching, exports to research tools.
  - **Google Forms** — fastest to deploy. Adequate for screening but weaker on branching and IRB integration.
  - **Custom on mhs.missouri.edu** — most polished but slowest to build; only feasible if developer time is available.
- **Required fields:**
  - Name (first, last)
  - Email
  - Phone (optional)
  - School name
  - District
  - State
  - Grade(s) taught
  - Subject(s) taught (filter for "earth science" relevance)
  - Years teaching
  - Device platform: iPads / Chromebooks / both / other (free text)
  - Estimated class size
  - Number of class periods per day
  - Planned timing for MHS unit (early / mid / late semester; Fall vs. Spring)
  - Prior research participation (yes/no/details)
  - Referral source (pilot teacher / website / Facebook / NESTA / other — populated from URL params if possible)
  - Anything else we should know (free text)
  - IRB consent acknowledgment
- **Backend:** acceptance/decline workflow, data export, automated confirmation email.

### Per-Contact Tracking System
- **Status:** Not built
- **Target live date:** 2026-05-08
- **Why critical:** without tracking, we lose Spring 2027 candidates and can't measure channel ROI.
- **Recommended:** Airtable. Strong filtering, views, automations, and team collaboration. Mizzou or IB likely has accounts.
- **Alternatives:** Google Sheets (acceptable for a single operator); HubSpot CRM free tier (overkill but works).
- **Schema:** documented in [tracking-template.md](tracking-template.md).

### One-Page Recruitment Flyer
- **Status:** Not built
- **Target ready date:** 2026-05-15
- **Format:** PDF, 1 page, designed for print + screen.
- **Use cases:** Newsletter mentions, partner co-marketing, conference handouts, email attachments to district contacts.
- **Content:**
  - MHS one-line description
  - Cohort dates and target audience
  - Value proposition (stipend, free curriculum, PD credit if confirmed)
  - Compatible devices (iPads + Chromebooks)
  - Apply URL + QR code
  - Funder + institutional credit (DoE, Mizzou, PI Jim Laffey)

### Demo Video
- **Status:** Not built
- **Target ready date:** 2026-05-30
- **Format:** 60–90 second video for landing page; 30-second cut for social media.
- **Content:** show actual gameplay, classroom footage (FERPA-cleared), one pilot teacher quote.
- **Critical dependency:** pilot teacher consent and footage availability (see [pilot-teacher-engagement.md](pilot-teacher-engagement.md)).

### Webinar / Virtual Info-Session Series
- **Status:** Not built
- **Target schedule:**
  - Webinar #1: late May 2026
  - Webinar #2: late June 2026
  - Webinar #3: late July 2026
  - Optional Webinar #4: mid-August 2026 (final push)
  - Spring 2027 series: Sep–Nov 2026
- **Format:** 30–45 minutes. Agenda: project overview (10 min), pilot teacher voice (10 min), what participating looks like (10 min), Q&A (10–15 min).
- **Platform:** Zoom (Mizzou license) recommended; record every session for replay on landing page.
- **Promotion:** every wave-2 outreach message should include the next webinar date.

### Email Sequence Templates
- **Status:** Partial (initial cold outreach exists in [outreach-templates.md](outreach-templates.md))
- **What's missing:**
  - Lead nurture follow-up (5-day, 12-day) for non-responders
  - Application confirmation email (auto-sent on submit)
  - Application reminder email (for prospects who started but didn't submit)
  - Acceptance email
  - Waitlist email
  - Decline email
  - Cohort kickoff email (1 week before training)
- **Owner:** to assign

### Recruiting Sub-Page on mhs.missouri.edu
- **Status:** May or may not exist as a distinct page; needs confirmation
- **Target live date:** 2026-05-15
- **Content:** see "Existing Infrastructure → Landing page" above

---

## Optional / Phase 2 Infrastructure

Worth considering if the campaign has bandwidth, but not blocking Fall 2026 cohort.

- **Newsletter for accepted teachers** — monthly, before and during the cohort, to maintain engagement.
- **Slack or Discord community** for cohort teachers — peer support during deployment.
- **Public dashboard / counter** showing "X teachers from Y states have joined the Fall 2026 cohort" — social proof on the landing page.
- **Application URL with channel-specific UTM parameters** — allows tracking which channel each application came through, even when teachers self-select "referral source."

---

## Owner / Due-By Tracking

| Item | Owner | Target date | Status |
|---|---|---|---|
| Online application form | _MHS team_ | 2026-05-15 | Not started |
| Tracking system | _MHS team_ | 2026-05-08 | Not started |
| One-page flyer | _MHS team / design_ | 2026-05-15 | Not started |
| Demo video | _MHS team / video_ | 2026-05-30 | Not started |
| Recruiting sub-page on mhs.missouri.edu | _MHS team / web_ | 2026-05-15 | Not started |
| Webinar #1 scheduled | _MHS team_ | 2026-05-25 | Not started |
| Email sequence drafts | _MHS team_ | 2026-05-15 | Not started |
| IRB amendment (if needed) | _MHS team / IRB_ | 2026-05-08 | Not started |

This table is the single coordination point for infrastructure. Update weekly.

---

## Risks

- **Application form delay.** Most likely failure mode. If form is not ready by 2026-05-15, push Wave 1 outreach by one week rather than running outreach without a place for applicants to land.
- **Demo video delay.** Less critical than the form; landing page can launch with text + photos and add video later. But fundraising-quality video is a meaningful conversion lift, so the 2026-05-30 target should be defended.
- **IRB scope ambiguity.** If the IRB-approved recruitment language is Missouri-only, broad national outreach may need amendment first. This should be confirmed with the IRB office in week 1.
- **Mizzou IT bottlenecks.** Custom landing page work and Qualtrics setup may queue behind other Mizzou IT priorities. Plan around this.
