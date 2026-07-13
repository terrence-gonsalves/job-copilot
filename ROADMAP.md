# Job Copilot Roadmap

## Product Vision

Job Copilot is a Canadian-first AI job-search assistant that helps users find relevant Canadian jobs, understand fit, tailor applications, and manage the job-search process.

The product should avoid becoming a low-quality auto-apply tool. The long-term value is in helping users make better application decisions and submit stronger, more targeted applications.

---

# V1 — MVP Application Copilot

## Goal

Let a Canadian user upload a resume, paste a job posting, receive a job-fit analysis, generate application materials, and track the application.

## Core Outcome

A user should be able to answer:

> “Is this job worth applying to, and how should I position myself for it?”

## Features

### Account and Profile

* User authentication
* Basic job-search profile
* Target job titles
* Preferred locations
* Remote/hybrid/onsite preference
* Province and city preferences
* Salary expectations
* Work authorization status
* Language preferences

### Resume Upload and Parsing

* Upload resume as PDF or DOCX
* Parse resume into structured profile data
* Extract skills, roles, experience, education, certifications, and industries
* Allow user to review parsed data
* Store original resume and parsed version

### Job Posting Input

* Paste job description manually
* Paste job posting URL if supported
* Extract employer, title, location, salary if available, and requirements
* Save job posting to application tracker

### AI Job Fit Score

* Compare resume/profile against job posting
* Generate match score
* Identify strong matches
* Identify gaps
* Identify unclear or missing details
* Explain fit in plain language

### Resume Tailoring Suggestions

* Suggest summary improvements
* Suggest keyword alignment
* Suggest bullet refinements
* Flag missing experience honestly
* Do not invent skills or experience

### Cover Letter Draft

* Generate a tailored cover letter
* Use user’s real background
* Keep tone professional, direct, and human
* Allow user to edit before use

### Application Tracker

* Save jobs
* Track statuses:

  * Saved
  * Ready to apply
  * Applied
  * Follow-up due
  * Interviewing
  * Rejected
  * Offer
* Store application date
* Store resume version used
* Store notes

### Follow-up Reminders

* Set follow-up date
* Email reminder or dashboard reminder
* Default follow-up after 5–7 business days

### Privacy and Data Controls

* User can delete resume
* User can delete account
* User can delete application history
* AI outputs should be auditable
* Sensitive user data should be minimized

## V1 Exclusions

Do not build in V1:

* Full auto-apply
* Browser extension
* Large-scale scraping
* Employer marketplace
* Recruiter network
* Mobile app
* Advanced salary intelligence
* NOC mapping
* Full ATS autofill

---

# V2 — Canadian Job Discovery

## Goal

Help users discover relevant Canadian roles automatically instead of relying only on pasted job postings.

## Core Outcome

A user should be able to receive a useful list of Canadian job matches based on their profile.

## Features

### Saved Searches

* Save target job titles
* Save locations
* Save remote preference
* Save salary expectations
* Save employment type

### Canadian Location Filters

* Postal code support
* City and province support
* Province/territory filters
* Commute radius
* Remote Canada
* Hybrid within selected radius

### Job Source Research

Investigate and prioritize:

* Job Bank
* Company career pages
* Public-sector job boards
* Provincial job boards
* Municipal job boards
* University and hospital job boards
* Remote Canada job boards
* Employer-direct listings

### Job Matching Feed

* Daily or weekly recommended jobs
* Match score
* Freshness indicator
* Location fit
* Skill fit
* Experience fit
* Application effort estimate

### Duplicate Detection

* Detect same job across sources
* Prefer employer-direct listing where possible

### Notifications

* Email job match digest
* Dashboard job alerts
* Saved search updates

---

# V3 — Application Assistant

## Goal

Reduce repetitive application work while keeping the user in control.

## Core Outcome

A user should be able to prepare and submit applications faster without sacrificing quality or accuracy.

## Features

### Application Checklist

* Resume selected
* Cover letter drafted
* Screening questions reviewed
* Salary expectations prepared
* Follow-up reminder set

### Screening Question Assistant

* Help answer common application questions
* Use only facts from the user profile
* Mark uncertain answers for user review
* Never submit answers automatically without approval

### Recruiter Outreach

* Draft recruiter emails
* Draft LinkedIn connection messages
* Draft follow-up messages
* Draft thank-you notes after interviews

### Interview Prep

* Generate likely interview questions from job description
* Generate company research prompts
* Generate STAR story suggestions
* Identify skills to review before interview

### Resume Version Manager

* Store tailored resume versions
* Link each version to a job application
* Track which resume was used where

### ATS Autofill Research

* Investigate feasibility for common ATS platforms
* Consider browser extension
* Avoid violating platform terms
* Keep user approval required

---

# V4 — Job Market Intelligence

## Goal

Help Canadian users understand the job market, salary expectations, career paths, and skill gaps.

## Core Outcome

A user should be able to make better career decisions, not just apply to individual jobs.

## Features

### Salary Insights

* Salary by province
* Salary by city
* Salary by role
* Public/private sector salary comparison
* Confidence level for estimated ranges

### Skill Gap Analysis

* Compare user profile against target roles
* Identify recurring missing skills
* Prioritize skills by market frequency
* Suggest learning paths

### NOC Mapping

* Map roles to likely NOC codes
* Help users understand related job families
* Support newcomer and immigration-adjacent use cases carefully

### Career Path Suggestions

* Suggest adjacent roles
* Identify realistic next-step jobs
* Identify overqualified or underqualified roles
* Explain tradeoffs

### Canadian Market Trends

* Province-level demand
* Remote Canada trends
* Bilingual role trends
* Public-sector opportunity trends

---

# Long-Term Direction

Potential future directions:

* Chrome extension
* Employer-direct integrations
* Referral tracking
* Recruiter CRM
* Mobile companion app
* Newcomer-focused version
* Public-sector application assistant
* Bilingual English/French application workflows
* Resume quality score
* Scam job detection
* Interview pipeline dashboard
