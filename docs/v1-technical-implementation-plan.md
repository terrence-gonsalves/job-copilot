# V1 Technical Implementation Plan — Job Copilot

## Purpose

This document defines the technical implementation plan for V1 of Job Copilot.

V1 should deliver a focused Canadian-first application copilot that allows a user to:

1. Create an account.
2. Set up a job-search profile.
3. Upload a resume.
4. Parse the resume into structured data.
5. Paste a job posting.
6. Generate a job-fit analysis.
7. Generate resume tailoring suggestions.
8. Generate a cover letter draft.
9. Track the application.
10. Set follow-up reminders.
11. Delete personal job-search data.

---

# 1. Recommended Tech Stack

## Frontend

* Next.js
* TypeScript
* Tailwind CSS
* React components
* Server actions or API routes depending on final architecture preference

## Backend

* Supabase Auth
* Supabase Postgres
* Supabase Storage
* Supabase Row Level Security
* Supabase client/server helpers

## AI Layer

Use either:

* OpenAI
* Anthropic Claude

The AI provider should be abstracted behind an internal service layer so the app is not tightly coupled to one provider.

## Email

* Resend

Used later for:

* Follow-up reminders
* Account emails
* Usage notifications
* Optional job match digests in future versions

## Hosting

* Vercel

## Payments

Billing is not required for the first functional MVP, but the data model should allow usage limits later.

Potential future provider:

* Stripe

---

# 2. V1 Product Boundary

## Included in V1

* Auth
* User profile
* Canadian location preferences
* Resume upload
* Resume text extraction
* Resume parsing
* Job posting paste/import
* Job fit score
* Resume tailoring suggestions
* Cover letter draft
* Application tracker
* Follow-up reminders
* Privacy/delete controls

## Excluded from V1

* Full auto-apply
* Browser extension
* Job scraping at scale
* Employer marketplace
* Recruiter marketplace
* Full ATS autofill
* Salary intelligence
* NOC mapping
* Bilingual application generation
* Public-sector-specific workflows
* Mobile app

---

# 3. Application Architecture

## High-Level Flow

```text
User
  ↓
Next.js Frontend
  ↓
Supabase Auth
  ↓
Supabase Database / Storage
  ↓
AI Service Layer
  ↓
Structured AI Outputs
  ↓
Application Tracker
```

## Core Architecture Principle

Keep AI calls isolated in dedicated server-side services.

Do not call AI providers directly from frontend components.

---

# 4. Suggested Folder Structure

```text
job-copilot/
├── app/
│   ├── auth/
│   │   ├── login/
│   │   └── callback/
│   ├── dashboard/
│   │   ├── page.tsx
│   │   ├── profile/
│   │   ├── resumes/
│   │   ├── jobs/
│   │   ├── applications/
│   │   └── settings/
│   ├── api/
│   │   ├── resumes/
│   │   ├── jobs/
│   │   ├── ai/
│   │   └── reminders/
│   ├── layout.tsx
│   └── page.tsx
│
├── components/
│   ├── auth/
│   ├── dashboard/
│   ├── forms/
│   ├── resumes/
│   ├── jobs/
│   ├── applications/
│   ├── ai/
│   └── ui/
│
├── lib/
│   ├── supabase/
│   │   ├── client.ts
│   │   ├── server.ts
│   │   └── middleware.ts
│   ├── ai/
│   │   ├── client.ts
│   │   ├── prompts.ts
│   │   ├── resume-parser.ts
│   │   ├── job-fit.ts
│   │   └── cover-letter.ts
│   ├── parsers/
│   │   ├── pdf.ts
│   │   └── docx.ts
│   ├── validators/
│   │   ├── profile.ts
│   │   ├── resume.ts
│   │   ├── job.ts
│   │   └── application.ts
│   └── utils/
│
├── types/
│   ├── database.ts
│   ├── resume.ts
│   ├── job.ts
│   ├── application.ts
│   └── ai.ts
│
├── supabase/
│   ├── migrations/
│   └── seed.sql
│
├── docs/
│   ├── planning-pack.md
│   ├── v1-technical-implementation-plan.md
│   └── prompts/
│
├── .env.example
├── README.md
└── ROADMAP.md
```

---

# 5. Environment Variables

Create:

```text
.env.example
```

Suggested values:

```env
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=

AI_PROVIDER=
OPENAI_API_KEY=
ANTHROPIC_API_KEY=

RESEND_API_KEY=
RESEND_FROM_EMAIL=

NEXT_PUBLIC_APP_URL=
```

## Notes

* `SUPABASE_SERVICE_ROLE_KEY` must only be used server-side.
* AI provider keys must only be used server-side.
* Frontend should only use safe public variables.

---

# 6. Database Schema

## 6.1 profiles

Stores user job-search profile data.

```sql
create table profiles (
  id uuid primary key references auth.users(id) on delete cascade,
  full_name text,
  target_roles text[],
  preferred_cities text[],
  preferred_provinces text[],
  postal_code text,
  work_arrangement text check (work_arrangement in ('remote', 'hybrid', 'onsite', 'flexible')),
  employment_types text[],
  salary_min integer,
  salary_target integer,
  work_authorization text,
  languages text[],
  created_at timestamptz default now(),
  updated_at timestamptz default now()
);
```

## 6.2 resumes

Stores uploaded resume records.

```sql
create table resumes (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  file_name text not null,
  file_path text not null,
  file_type text not null,
  file_size integer,
  extracted_text text,
  is_primary boolean default false,
  created_at timestamptz default now(),
  updated_at timestamptz default now()
);
```

## 6.3 parsed_resumes

Stores structured resume output.

```sql
create table parsed_resumes (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  resume_id uuid not null references resumes(id) on delete cascade,
  parsed_data jsonb not null,
  reviewed_by_user boolean default false,
  created_at timestamptz default now(),
  updated_at timestamptz default now()
);
```

## 6.4 jobs

Stores pasted job postings.

```sql
create table jobs (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  title text,
  company text,
  location text,
  province text,
  source_url text,
  employment_type text,
  work_arrangement text,
  salary_min integer,
  salary_max integer,
  raw_description text not null,
  extracted_data jsonb,
  created_at timestamptz default now(),
  updated_at timestamptz default now()
);
```

## 6.5 job_fit_results

Stores AI fit analysis.

```sql
create table job_fit_results (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  job_id uuid not null references jobs(id) on delete cascade,
  resume_id uuid references resumes(id) on delete set null,
  match_score integer check (match_score >= 0 and match_score <= 100),
  strengths jsonb,
  gaps jsonb,
  missing_keywords jsonb,
  recommendation text,
  full_analysis jsonb,
  created_at timestamptz default now()
);
```

## 6.6 cover_letters

Stores generated cover letter drafts.

```sql
create table cover_letters (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  job_id uuid not null references jobs(id) on delete cascade,
  resume_id uuid references resumes(id) on delete set null,
  content text not null,
  tone text default 'professional',
  created_at timestamptz default now(),
  updated_at timestamptz default now()
);
```

## 6.7 applications

Tracks saved applications.

```sql
create table applications (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  job_id uuid not null references jobs(id) on delete cascade,
  resume_id uuid references resumes(id) on delete set null,
  cover_letter_id uuid references cover_letters(id) on delete set null,
  status text not null default 'saved' check (
    status in (
      'saved',
      'ready_to_apply',
      'applied',
      'follow_up_due',
      'interviewing',
      'rejected',
      'offer'
    )
  ),
  applied_at timestamptz,
  notes text,
  created_at timestamptz default now(),
  updated_at timestamptz default now()
);
```

## 6.8 follow_ups

Stores follow-up reminders.

```sql
create table follow_ups (
  id uuid primary key default gen_random_uuid(),
  user_id uuid not null references auth.users(id) on delete cascade,
  application_id uuid not null references applications(id) on delete cascade,
  reminder_date date not null,
  reminder_sent boolean default false,
  reminder_channel text default 'dashboard',
  created_at timestamptz default now(),
  updated_at timestamptz default now()
);
```

## 6.9 ai_logs

Stores AI request metadata for audit/debugging.

```sql
create table ai_logs (
  id uuid primary key default gen_random_uuid(),
  user_id uuid references auth.users(id) on delete set null,
  feature text not null,
  provider text,
  model text,
  input_summary text,
  output_summary text,
  status text default 'success',
  error_message text,
  created_at timestamptz default now()
);
```

---

# 7. Supabase Storage

## Bucket

Create a private bucket:

```text
resumes
```

## Path Convention

```text
user_id/resume_id/original-file-name.pdf
```

Example:

```text
a1b2c3/resume-uuid/terrence-resume.pdf
```

## Storage Rules

* Users can upload only to their own folder.
* Users can read only their own files.
* Users can delete only their own files.
* Resume files should not be public.

---

# 8. Row Level Security

Enable RLS on all user-owned tables.

Tables requiring RLS:

* profiles
* resumes
* parsed_resumes
* jobs
* job_fit_results
* cover_letters
* applications
* follow_ups
* ai_logs

## Basic Policy Pattern

Each user can only access rows where:

```sql
user_id = auth.uid()
```

For `profiles`, use:

```sql
id = auth.uid()
```

---

# 9. Core Routes

## Public Routes

```text
/
```

Landing page.

```text
/auth/login
```

Login page.

```text
/auth/callback
```

Supabase auth callback.

## Protected Routes

```text
/dashboard
```

Main dashboard.

```text
/dashboard/profile
```

User job-search profile.

```text
/dashboard/resumes
```

Resume upload and resume management.

```text
/dashboard/jobs/new
```

Paste/import job posting.

```text
/dashboard/jobs/[id]
```

View saved job and fit analysis.

```text
/dashboard/applications
```

Application tracker.

```text
/dashboard/applications/[id]
```

Application detail page.

```text
/dashboard/settings
```

Privacy/delete controls.

---

# 10. Main UI Screens

## 10.1 Landing Page

Purpose:

* Explain what Job Copilot does.
* Emphasize Canadian-first positioning.
* Drive user to sign up.

Sections:

* Hero
* Problem
* How it works
* Canadian-first differentiators
* MVP feature preview
* Call to action

## 10.2 Dashboard

Should show:

* Resume status
* Profile completion
* Saved jobs
* Applications by status
* Follow-ups due
* Recent AI analyses

## 10.3 Profile Setup

Fields:

* Full name
* Target roles
* Cities
* Provinces
* Postal code
* Work arrangement
* Employment types
* Salary expectations
* Work authorization
* Languages

## 10.4 Resume Upload

User can:

* Upload resume
* View uploaded resume
* See parsing status
* Review extracted data
* Mark resume as primary
* Delete resume

## 10.5 Job Posting Input

User can:

* Paste job description
* Add source URL
* Confirm extracted job fields
* Save job posting
* Run fit analysis

## 10.6 Job Fit Results

Display:

* Match score
* Recommendation
* Strengths
* Gaps
* Missing keywords
* Suggested next step
* Button to generate resume suggestions
* Button to generate cover letter
* Button to save to application tracker

## 10.7 Application Tracker

Table or card view showing:

* Job title
* Company
* Status
* Application date
* Follow-up date
* Notes
* Actions

## 10.8 Settings / Privacy

User can:

* Delete resume
* Delete saved jobs
* Delete applications
* Delete account
* Review data handling note

---

# 11. AI Service Layer

## Principle

AI outputs must be grounded in user-provided data.

The AI must not invent:

* Work experience
* Employers
* Job titles
* Education
* Certifications
* Tools
* Metrics
* Achievements
* Languages
* Immigration/work authorization details

## AI Features in V1

### 11.1 Resume Parser

Input:

* Extracted resume text

Output:

```json
{
  "name": "",
  "email": "",
  "phone": "",
  "location": "",
  "summary": "",
  "skills": [],
  "tools": [],
  "work_experience": [],
  "education": [],
  "certifications": [],
  "industries": [],
  "seniority_signals": [],
  "possible_target_roles": []
}
```

### 11.2 Job Posting Parser

Input:

* Raw job posting text

Output:

```json
{
  "title": "",
  "company": "",
  "location": "",
  "province": "",
  "work_arrangement": "",
  "employment_type": "",
  "salary_min": null,
  "salary_max": null,
  "responsibilities": [],
  "requirements": [],
  "preferred_qualifications": [],
  "technologies": [],
  "soft_skills": [],
  "application_notes": []
}
```

### 11.3 Job Fit Analysis

Input:

* Parsed resume
* Parsed job posting
* User profile

Output:

```json
{
  "match_score": 0,
  "recommendation": "",
  "strong_matches": [],
  "possible_gaps": [],
  "missing_keywords": [],
  "experience_fit": "",
  "location_fit": "",
  "risk_flags": [],
  "suggested_next_steps": []
}
```

### 11.4 Resume Tailoring Suggestions

Input:

* Parsed resume
* Job posting
* Fit analysis

Output:

```json
{
  "suggested_summary": "",
  "bullet_suggestions": [],
  "keyword_suggestions": [],
  "items_to_verify": [],
  "do_not_claim": []
}
```

### 11.5 Cover Letter Generator

Input:

* User profile
* Resume data
* Job posting
* Fit analysis

Output:

```json
{
  "cover_letter": "",
  "assumptions": [],
  "items_to_verify": []
}
```

---

# 12. Prompt Guardrails

Every AI prompt should include rules like:

```text
Use only information provided in the user profile, resume, and job posting.

Do not invent experience, employers, education, certifications, metrics, achievements, tools, or work authorization details.

If something is not present in the source material, mark it as missing or requiring user confirmation.

Be specific, practical, and direct.

Return structured JSON only when requested.
```

---

# 13. Validation and Error Handling

## Resume Upload

Handle:

* Unsupported file type
* File too large
* Empty file
* Text extraction failure
* AI parsing failure

## Job Posting Input

Handle:

* Empty job description
* Too-short posting
* Missing company
* Missing salary
* Missing location
* AI extraction failure

## AI Calls

Handle:

* Provider timeout
* Invalid JSON response
* Rate limit
* Empty response
* Unsafe or low-confidence response

## User Data

Handle:

* Unauthorized access
* Missing profile
* Missing resume
* Missing job posting
* Deleted records

---

# 14. Usage Limits

Billing does not need to be implemented immediately, but usage limits should be considered.

Potential free-tier limits:

* 1 active resume
* 5 job analyses/month
* 5 cover letters/month
* 25 tracked applications

Potential paid tier:

* Multiple resumes
* More job analyses
* More cover letters
* More tracked applications
* Follow-up reminders
* Saved searches in V2

---

# 15. Privacy and Data Handling

## Sensitive Data

The app may store:

* Resume
* Employment history
* Education
* Location
* Salary expectations
* Work authorization
* Application history

## V1 Requirements

* User can delete resume
* User can delete parsed resume data
* User can delete jobs
* User can delete applications
* User can delete account
* AI logs should avoid storing full sensitive content when possible
* Data should be scoped to authenticated user

## AI Logging

Avoid storing full raw prompts if they contain resume text.

Prefer:

* Feature name
* Provider
* Model
* Status
* Input summary
* Output summary
* Error message if relevant

---

# 16. Development Sequence

## Phase 1 — Project Foundation

Issues:

* Create initial Next.js application scaffold
* Set up Supabase project and environment variables
* Create dashboard layout
* Create initial database schema
* Add Row Level Security policies

Acceptance:

* App runs locally
* Supabase connection works
* Protected dashboard route exists
* Initial schema is migrated

---

## Phase 2 — Auth and Profile

Issues:

* Build authentication and user profile setup
* Add Canadian location preferences

Acceptance:

* User can sign up/login/logout
* User can create/update profile
* Canadian postal codes are supported
* Province and remote preference are stored

---

## Phase 3 — Resume Workflow

Issues:

* Build resume upload flow
* Parse uploaded resume into structured profile data
* Add parsed resume review screen

Acceptance:

* User can upload a resume
* Resume is stored securely
* Resume text is extracted
* Parsed data is saved
* User can review parsed data

---

## Phase 4 — Job Workflow

Issues:

* Add job posting paste/import flow
* Parse job posting into structured data
* Save job posting to user account

Acceptance:

* User can paste a job posting
* Job details are extracted
* Job is saved
* User can view saved job

---

## Phase 5 — AI Application Support

Issues:

* Generate AI job fit score
* Generate resume tailoring suggestions
* Generate cover letter draft
* Create AI prompt guardrails for resume-grounded outputs

Acceptance:

* Fit score is generated
* Strengths and gaps are shown
* Resume suggestions are grounded
* Cover letter does not invent experience
* AI outputs are saved

---

## Phase 6 — Application Tracker

Issues:

* Build application tracker
* Add follow-up reminder system
* Add application status workflow

Acceptance:

* User can save application
* User can update status
* User can set follow-up date
* Dashboard shows follow-up reminders

---

## Phase 7 — Privacy and Polish

Issues:

* Add privacy and data deletion controls
* Create settings page
* Add empty states and error states
* Add basic QA checklist

Acceptance:

* User can delete personal data
* App handles missing data gracefully
* Core flow works from signup to tracked application

---

# 17. Initial GitHub Issues to Add

Add these issues if they do not already exist:

1. Create initial Next.js application scaffold
2. Set up Supabase project and environment variables
3. Create dashboard layout
4. Add Row Level Security policies
5. Add parsed resume review screen
6. Parse job posting into structured data
7. Create AI prompt guardrails for resume-grounded outputs
8. Add application status workflow
9. Create settings page
10. Add basic QA checklist

---

# 18. Definition of Done for V1

V1 is done when a user can:

* Sign up
* Complete profile
* Upload resume
* Parse resume
* Paste job posting
* Generate job fit analysis
* Generate resume tailoring suggestions
* Generate cover letter
* Save application
* Track application status
* Set follow-up reminder
* Delete resume/application/account data

V1 should be considered successful if it helps a user make a better decision about whether and how to apply to a job.

---

# 19. V1 Success Metrics

Initial qualitative metrics:

* User understands job fit more clearly
* User saves time tailoring applications
* User trusts the AI output
* User does not feel the app is generating generic material
* User uses tracker to manage applications

Initial quantitative metrics:

* Number of resumes uploaded
* Number of job postings analyzed
* Number of applications saved
* Number of cover letters generated
* Number of follow-ups created
* Percentage of users completing full workflow
* Repeat usage within 7 days

---

# 20. Immediate Next Build Step

Start with:

```text
Create initial Next.js application scaffold
```

Then:

```text
Set up Supabase project and environment variables
```

Then:

```text
Create initial database schema
```

Do not start AI features until auth, profile, resume storage, and job posting storage are working.
