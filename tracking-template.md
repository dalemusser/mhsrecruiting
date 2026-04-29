# Tracking Template

Schema and workflow for the per-contact tracking system that holds every recruiting lead. The tracker itself is not a markdown file — it should live in **Airtable** (recommended) or a shared spreadsheet — but this file documents the fields and process so the system is reproducible and reviewable.

Without tracking, two things happen: (1) Spring 2027 candidates who declined Fall 2026 are lost, and (2) channel ROI cannot be measured, which prevents budget reallocation.

---

## Recommended Platform: Airtable

### Why Airtable
- Strong filtering and views (per-state, per-channel, per-status segments without exporting)
- Linked records (one teacher → multiple touchpoints)
- Automations (auto-email on status change, weekly summary reports)
- Form-as-input (the public application form can write directly into the tracker)
- Easy to share and grant scoped access to team members

### Alternatives (if Airtable isn't available)
- **Google Sheets** — workable for a single operator; weaker on automation and views
- **HubSpot CRM (free tier)** — overkill for our scale but works; designed for sales pipelines, which is the right shape
- **Notion databases** — usable; less mature than Airtable for this kind of work

---

## Schema (Fields)

### Core identity
- **`teacher_id`** — auto-generated unique ID
- **`first_name`** *(text)*
- **`last_name`** *(text)*
- **`email`** *(email)*
- **`phone`** *(text, optional)*
- **`linkedin_url`** *(url, optional)*

### School and role
- **`school_name`** *(text)*
- **`district`** *(text)*
- **`state`** *(single-select; all 50 states + DC + PR)*
- **`grade_taught`** *(multi-select: 5, 6, 7, 8)*
- **`subject`** *(text — should include "earth science" indicator)*
- **`years_teaching`** *(number, optional)*
- **`role`** *(single-select: classroom teacher / department chair / instructional coach / other)*

### Tech and deployment fit
- **`device_platform`** *(single-select: iPads / Chromebooks / both / other)*
- **`class_size`** *(number, estimated)*
- **`number_of_periods`** *(number, optional)*
- **`planned_unit_timing`** *(single-select: early / mid / late semester; Fall vs. Spring)*

### Recruiting funnel
- **`status`** *(single-select; see status values below)*
- **`channel`** *(single-select; see channel values below)*
- **`referral_source`** *(linked record to another teacher in the table, or text — for pilot teacher referrals or named-person referrals)*
- **`first_contact_date`** *(date)*
- **`last_contact_date`** *(date)*
- **`next_followup_date`** *(date, optional)*
- **`cohort_target`** *(single-select: Fall 2026 / Spring 2027 / either / declined)*
- **`application_submitted_date`** *(date, optional)*
- **`acceptance_date`** *(date, optional)*

### Notes and artifacts
- **`notes`** *(long text)*
- **`artifacts`** *(attachments — testimonials, photos, video clips, signed consent forms)*
- **`consent_status`** *(single-select: not asked / pending / consented for use / declined)*

### Tracking and metrics support
- **`first_response_received`** *(date, optional — measures responsiveness)*
- **`utm_source`** *(text — populated from URL params on application form)*
- **`utm_medium`** *(text)*
- **`utm_campaign`** *(text)*

---

## Status Values

The single most important field. Drives all reporting.

| Status | Meaning | Next action |
|---|---|---|
| `lead` | Discovered / referred but not yet contacted | Send initial outreach |
| `contacted` | Initial outreach sent; no response yet | Followup in 5 days if no response |
| `responded` | Replied; in conversation | Schedule call or guide to application |
| `applied` | Submitted application form | Review and decide |
| `interview_scheduled` | Optional screening call scheduled | Conduct interview |
| `accepted_fall26` | Accepted into Fall 2026 cohort | Onboarding workflow |
| `accepted_spring27` | Accepted into Spring 2027 cohort | Onboarding workflow |
| `waitlist_fall26` | Strong fit, but Fall cohort full | Hold for Spring 2027 / contingency |
| `declined_us` | Teacher declined to participate | Mark for outreach in following year |
| `declined_by_us` | We declined (poor fit, etc.) | Note reason in `notes` |
| `withdrew` | Accepted then withdrew | Note reason; consider Spring 2027 |
| `referrer_only` | Pilot teacher acting as referrer (not a candidate themselves) | Engage per [pilot-teacher-engagement.md](pilot-teacher-engagement.md) |

---

## Channel Values

The channel field determines ROI analysis. Use these standardized values:

- `pilot_referral` — referred by a pilot teacher
- `peer_referral` — referred by a non-pilot teacher in the cohort
- `mizzou_alumni` — Mizzou College of Education / Engineering channel
- `nesta_newsletter`
- `nagt_newsletter`
- `nsta_publication`
- `agi_earth_science_week`
- `state_assoc_<STATE>` — e.g., `state_assoc_CA` for CSTA
- `state_doe_<STATE>` — e.g., `state_doe_TX`
- `teacher_site_<NAME>` — e.g., `teacher_site_sunrise_science`
- `facebook_<GROUP>` — e.g., `facebook_ms_science_teachers`
- `reddit_<SUBREDDIT>` — e.g., `reddit_scienceteachers`
- `twitter_ngsschat`
- `linkedin_direct`
- `cold_email`
- `conference_<NAME>` — e.g., `conference_csta_2026`
- `apple_education`
- `google_education`
- `apple_distinguished_educator`
- `google_innovator`
- `bscs_partnership`
- `nextgen_science_partnership`
- `webinar_signup`
- `landing_page_organic`
- `paid_promotion_<DESCRIPTION>`
- `other`

Channel taxonomy should be locked at campaign launch; adding new values mid-campaign breaks ROI comparison.

---

## Workflow

### Daily (during active recruiting waves)
- Review new applications coming through the form (auto-imported)
- Send 5–10 fresh cold/warm outreach messages
- Reply to any responses within 24 hours
- Update last_contact_date and notes for any touched record

### Weekly (every Monday)
- Run channel ROI report (lead count, application count, conversion rates by channel)
- Review records with `next_followup_date` in the past — chase or close
- Update weekly metrics in [recruiting-strategy.md](recruiting-strategy.md) Channel ROI table
- Identify any waitlist candidates to push to Spring 2027 outreach
- Triage any "declined_us" records — note the reason and check for re-engagement opportunities

### Monthly
- Full pipeline review with MHS team
- Adjust channel priority based on ROI data
- Decide whether to trigger Wave 5 contingency (see [recruiting-strategy.md](recruiting-strategy.md))

---

## Reporting Views

Set up these saved views in Airtable on day one:

1. **All active leads** — `status` is `lead`, `contacted`, or `responded`
2. **Applications pending review** — `status` is `applied`
3. **Fall 2026 cohort** — `status` is `accepted_fall26`
4. **Spring 2027 hold list** — `status` is `waitlist_fall26` OR (`status` is `responded` AND `cohort_target` includes "Spring 2027")
5. **Followups due** — `next_followup_date` is on or before today
6. **Channel ROI** — group by `channel`; count statuses
7. **By state** — group by `state`; count active and accepted
8. **By device platform** — split iPads / Chromebooks / both / other
9. **Pilot referrals network** — filter on `channel = pilot_referral`; group by `referral_source`
10. **Stale records** — `last_contact_date` more than 14 days ago AND status not in (`accepted_*`, `declined_*`, `withdrew`)

These views are the operational backbone of the campaign.

---

## Privacy and IRB Considerations

- The tracker contains personally identifiable information (PII) about teachers. Apply appropriate access controls — only the recruiting team should have edit access; broader project staff can have read-only access if needed.
- Any data fields collected via the application form must be covered by IRB consent.
- Retention: clarify with the IRB how long teacher contact data may be kept after the cohort ends — Spring 2027 recruiting depends on retaining Fall 2026 declines, so retention through 2027 is needed at minimum.
- Don't store classroom photos, video clips, or student-identifying material in the tracker. Those go in a separate consent-managed asset library — link to filenames only.

---

## Setup Checklist (Before Wave 1 Launch)

- [ ] Airtable workspace created with appropriate access controls
- [ ] Schema implemented per the field list above
- [ ] All saved views configured
- [ ] Form-to-tracker integration tested (application form writes a new row)
- [ ] Channel taxonomy reviewed and locked
- [ ] Initial pilot teacher list imported as `referrer_only` records
- [ ] Test record run end-to-end (application → review → acceptance)
- [ ] Team trained on workflow

Target completion: 2026-05-08.
