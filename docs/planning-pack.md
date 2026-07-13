# Job Copilot Planning Pack

This file contains the initial product requirements, MVP scope, Kanban setup, and V1 issue backlog.

---

# Product Requirements

## Product Name

Job Copilot

## Product Summary

Job Copilot is a Canadian-first AI job-search copilot that helps users analyze job fit, tailor applications, and manage the job-search process.

## Product Principle

Job Copilot should help users apply better, not simply apply more.

## Primary User

The initial user is a Canadian job seeker who wants help identifying strong-fit jobs, tailoring applications, and staying organized.

## Initial Target Segment

Canadian tech and digital professionals, including:

* Web developers
* WordPress developers
* Salesforce admins/developers
* Digital specialists
* Accessibility specialists
* Product-adjacent technical workers
* Mid-career professionals

## Core User Problems

Users struggle with:

* Finding Canadian-relevant roles
* Understanding whether they are a good fit
* Tailoring resumes without exaggerating
* Writing cover letters efficiently
* Tracking applications
* Following up consistently
* Avoiding generic AI-generated application material

## Core Product Jobs

The product should help users:

1. Understand job fit.
2. Tailor application materials.
3. Track the application process.
4. Follow up at the right time.
5. Avoid wasting time on poor-fit roles.

## Non-Goals for V1

V1 should not include:

* Full auto-apply
* Large-scale scraping
* Employer-facing tools
* Recruiter marketplace
* Browser extension
* Mobile app
* Complex job-source integrations

---

# MVP Scope

## MVP Goal

Build the smallest useful version of Job Copilot that helps a Canadian user move from resume + job posting to application-ready materials and a tracked application.

## MVP User Flow

1. User signs up.
2. User creates job-search profile.
3. User uploads resume.
4. System parses resume.
5. User pastes job posting.
6. System analyzes fit.
7. System suggests resume tailoring.
8. System drafts cover letter.
9. User saves job to tracker.
10. User sets or receives follow-up reminder.

## MVP Features

### Authentication

* User signup
* User login
* User logout
* Protected dashboard

### User Profile

Fields:

* Name
* Target roles
* Preferred cities
* Preferred provinces
* Remote/hybrid/onsite preference
* Salary expectation
* Employment type
* Work authorization
* Languages

### Resume Upload

Requirements:

* Accept PDF
* Accept DOCX if feasible
* Store uploaded file securely
* Extract text
* Parse structured fields
* Allow user review

### Resume Parser

Extract:

* Skills
* Work history
* Job titles
* Years of experience
* Education
* Certifications
* Tools/platforms
* Industries
* Seniority signals

### Job Posting Input

Requirements:

* Paste job description
* Optional URL field
* Extract title, company, location, requirements, salary if listed
* Store job posting

### Job Fit Analysis

Output:

* Match score
* Strong matches
* Possible gaps
* Missing keywords
* Experience fit
* Location fit
* Application recommendation

### Resume Tailoring

Output:

* Suggested summary
* Suggested bullet refinements
* Keyword alignment
* Items the user must verify
* Warnings where experience is not found

### Cover Letter

Output:

* Draft cover letter
* Grounded in resume/profile
* No invented claims
* Editable by user

### Application Tracker

Statuses:

* Saved
* Ready to apply
* Applied
* Follow-up due
* Interviewing
* Rejected
* Offer

### Follow-up Reminder

Requirements:

* Default reminder date
* User-editable date
* Dashboard reminder
* Email reminder if email system is enabled

### Privacy Controls

Requirements:

* Delete resume
* Delete application
* Delete account
* Clear AI-generated outputs
* Basic consent record

---

# Kanban Setup

## Recommended GitHub Project Columns

Use these columns:

| Column      | Purpose                                  |
| ----------- | ---------------------------------------- |
| Backlog     | Ideas and future work                    |
| Ready       | Defined and ready to build               |
| In Progress | Currently being worked on                |
| Blocked     | Waiting on decision, data, or dependency |
| Review / QA | Built and awaiting test/review           |
| Done        | Completed                                |

## Recommended Milestones

Create these GitHub milestones:

| Milestone                    | Purpose                                                    |
| ---------------------------- | ---------------------------------------------------------- |
| V1 — MVP Application Copilot | Resume upload, job paste, AI fit score, tailoring, tracker |
| V2 — Canadian Job Discovery  | Saved searches and Canadian job discovery                  |
| V3 — Application Assistant   | ATS helper, screening support, outreach, interview prep    |
| V4 — Market Intelligence     | Salary, skills, NOC, and career insights                   |
| Post-MVP / Future            | Ideas not yet scheduled                                    |

## Recommended Labels

### Product Labels

* `product`
* `mvp`
* `enhancement`
* `research`
* `risk`

### Feature Area Labels

* `auth`
* `resume`
* `jobs`
* `ai`
* `applications`
* `canada`
* `privacy`
* `billing`
* `notifications`
* `frontend`
* `backend`

### Priority Labels

* `priority: high`
* `priority: medium`
* `priority: low`

---

# V1 Issue Backlog

Create these as GitHub issues.

---

## Issue 1: Define product requirements for Canadian Job Copilot

Labels:

* `product`
* `mvp`
* `priority: high`

Milestone:

* `V1 — MVP Application Copilot`

Body:

```md
## Goal

Define the first-version product requirements for Job Copilot.

## User Story

As a Canadian job seeker, I want a focused AI job-search tool that understands Canadian job-market needs so that I can apply to better-fit roles with more confidence.

## Requirements

- [ ] Define the target user for V1
- [ ] Define the core MVP workflow
- [ ] Define what is excluded from V1
- [ ] Define Canadian-specific requirements
- [ ] Define AI safety and accuracy principles

## Acceptance Criteria

- [ ] Product scope is documented
- [ ] MVP workflow is clear
- [ ] V1 exclusions are listed
- [ ] Canadian-first differentiators are documented
```

---

## Issue 2: Create initial database schema

Labels:

* `backend`
* `mvp`
* `priority: high`

Milestone:

* `V1 — MVP Application Copilot`

Body:

```md
## Goal

Create the initial database schema for the MVP.

## User Story

As a user, I want my profile, resumes, jobs, and applications stored securely so that I can manage my job search in one place.

## Requirements

- [ ] Create users/profile table
- [ ] Create resumes table
- [ ] Create parsed_resume_data table or JSON field
- [ ] Create jobs table
- [ ] Create job_fit_results table
- [ ] Create applications table
- [ ] Create cover_letters table
- [ ] Create follow_ups table
- [ ] Create AI audit/log table if needed

## Acceptance Criteria

- [ ] Schema supports the full V1 workflow
- [ ] User-owned records are scoped by user ID
- [ ] Deletion paths are considered
- [ ] Sensitive data fields are identified
```

---

## Issue 3: Build authentication and user profile setup

Labels:

* `auth`
* `frontend`
* `backend`
* `mvp`

Milestone:

* `V1 — MVP Application Copilot`

Body:

```md
## Goal

Allow users to create an account and set up a basic job-search profile.

## User Story

As a user, I want to create an account and enter my job-search preferences so that the app can tailor recommendations to me.

## Requirements

- [ ] Implement signup
- [ ] Implement login
- [ ] Implement logout
- [ ] Protect dashboard routes
- [ ] Create profile setup screen
- [ ] Save target roles
- [ ] Save location preferences
- [ ] Save remote/hybrid/onsite preference
- [ ] Save work authorization status
- [ ] Save language preferences

## Acceptance Criteria

- [ ] User can create an account
- [ ] User can complete profile setup
- [ ] Profile data persists
- [ ] Dashboard uses authenticated user data
```

---

## Issue 4: Add Canadian location preferences

Labels:

* `canada`
* `product`
* `frontend`
* `backend`
* `mvp`

Milestone:

* `V1 — MVP Application Copilot`

Body:

```md
## Goal

Support Canadian-specific location preferences.

## User Story

As a Canadian job seeker, I want to search by Canadian cities, provinces, postal codes, and remote Canada preferences so that job matching reflects my actual location needs.

## Requirements

- [ ] Add city field
- [ ] Add province field
- [ ] Add postal code field
- [ ] Add remote Canada preference
- [ ] Add hybrid distance preference
- [ ] Validate Canadian postal code format
- [ ] Avoid ZIP-code-only assumptions

## Acceptance Criteria

- [ ] Canadian postal codes are accepted
- [ ] Province selection is supported
- [ ] Remote Canada preference is supported
- [ ] Location preferences are saved to the user profile
```

---

## Issue 5: Build resume upload flow

Labels:

* `resume`
* `frontend`
* `backend`
* `mvp`
* `priority: high`

Milestone:

* `V1 — MVP Application Copilot`

Body:

```md
## Goal

Allow users to upload their resume.

## User Story

As a user, I want to upload my resume so that Job Copilot can analyze my background and help tailor applications.

## Requirements

- [ ] Build resume upload UI
- [ ] Accept PDF files
- [ ] Accept DOCX files if feasible
- [ ] Validate file type
- [ ] Validate file size
- [ ] Store file securely
- [ ] Associate resume with authenticated user
- [ ] Show upload success/error states

## Acceptance Criteria

- [ ] User can upload a resume
- [ ] Invalid files are rejected
- [ ] Uploaded resume is associated with the correct user
- [ ] User receives clear feedback after upload
```

---

## Issue 6: Parse uploaded resume into structured profile data

Labels:

* `resume`
* `ai`
* `backend`
* `mvp`
* `priority: high`

Milestone:

* `V1 — MVP Application Copilot`

Body:

```md
## Goal

Extract structured data from an uploaded resume.

## User Story

As a user, I want the system to understand my resume so that it can compare my experience against job postings.

## Requirements

- [ ] Extract resume text
- [ ] Identify skills
- [ ] Identify work history
- [ ] Identify job titles
- [ ] Identify years of experience
- [ ] Identify education
- [ ] Identify certifications
- [ ] Identify tools and technologies
- [ ] Save parsed resume data
- [ ] Allow user to review parsed data

## Acceptance Criteria

- [ ] Resume text is extracted successfully
- [ ] Structured resume data is saved
- [ ] AI parsing does not invent experience
- [ ] User can review or correct parsed data
```

---

## Issue 7: Add job posting paste/import flow

Labels:

* `jobs`
* `frontend`
* `backend`
* `mvp`
* `priority: high`

Milestone:

* `V1 — MVP Application Copilot`

Body:

```md
## Goal

Allow users to paste a job posting for analysis.

## User Story

As a user, I want to paste a job posting so that Job Copilot can analyze whether I am a good fit.

## Requirements

- [ ] Create job posting input screen
- [ ] Allow manual paste of job description
- [ ] Optional field for source URL
- [ ] Extract job title
- [ ] Extract company name if available
- [ ] Extract location if available
- [ ] Extract salary if available
- [ ] Extract requirements and responsibilities
- [ ] Save job posting

## Acceptance Criteria

- [ ] User can save a pasted job posting
- [ ] Job data is stored correctly
- [ ] Missing optional fields do not block the workflow
- [ ] Saved job can be used for AI fit analysis
```

---

## Issue 8: Generate AI job fit score

Labels:

* `ai`
* `jobs`
* `resume`
* `mvp`
* `priority: high`

Milestone:

* `V1 — MVP Application Copilot`

Body:

```md
## Goal

Compare the user’s resume/profile against a job posting and generate a useful fit analysis.

## User Story

As a user, I want to know whether a job is a strong fit so that I can decide whether to apply.

## Requirements

- [ ] Compare resume data to job requirements
- [ ] Generate match score
- [ ] Identify strong matches
- [ ] Identify possible gaps
- [ ] Identify missing keywords
- [ ] Assess experience fit
- [ ] Assess location fit
- [ ] Provide plain-language recommendation

## Acceptance Criteria

- [ ] Fit score is generated
- [ ] Explanation is clear and specific
- [ ] Gaps are identified honestly
- [ ] AI does not invent user experience
- [ ] User can save analysis
```

---

## Issue 9: Generate resume tailoring suggestions

Labels:

* `ai`
* `resume`
* `applications`
* `mvp`

Milestone:

* `V1 — MVP Application Copilot`

Body:

```md
## Goal

Suggest resume improvements based on a specific job posting.

## User Story

As a user, I want resume tailoring suggestions so that I can better align my application with the role.

## Requirements

- [ ] Suggest updated resume summary
- [ ] Suggest bullet refinements
- [ ] Suggest keyword alignment
- [ ] Flag missing experience
- [ ] Mark suggestions that require user verification
- [ ] Avoid fabricated claims

## Acceptance Criteria

- [ ] Suggestions are based on user resume data
- [ ] Suggestions are tied to the job posting
- [ ] Unverified claims are clearly marked
- [ ] User can copy or save suggestions
```

---

## Issue 10: Generate cover letter draft

Labels:

* `ai`
* `applications`
* `mvp`

Milestone:

* `V1 — MVP Application Copilot`

Body:

```md
## Goal

Generate a tailored cover letter draft for a saved job posting.

## User Story

As a user, I want a cover letter draft that reflects my real background so that I can apply faster without sounding generic.

## Requirements

- [ ] Generate cover letter from resume/profile and job posting
- [ ] Keep tone professional and human
- [ ] Avoid exaggeration
- [ ] Allow user editing
- [ ] Save cover letter to application record

## Acceptance Criteria

- [ ] Cover letter is generated
- [ ] Cover letter references the target role
- [ ] Cover letter uses only grounded user information
- [ ] User can edit and save the draft
```

---

## Issue 11: Build application tracker

Labels:

* `applications`
* `frontend`
* `backend`
* `mvp`
* `priority: high`

Milestone:

* `V1 — MVP Application Copilot`

Body:

```md
## Goal

Create an application tracker for saved jobs.

## User Story

As a user, I want to track my applications so that I know what I applied to, when I applied, and what needs follow-up.

## Requirements

- [ ] Create application tracker page
- [ ] Add application statuses
- [ ] Save application date
- [ ] Save notes
- [ ] Link application to job posting
- [ ] Link application to resume version if available
- [ ] Support status updates

## Acceptance Criteria

- [ ] User can save jobs to tracker
- [ ] User can update application status
- [ ] User can view all applications
- [ ] User can add notes
```

---

## Issue 12: Add follow-up reminder system

Labels:

* `notifications`
* `applications`
* `mvp`

Milestone:

* `V1 — MVP Application Copilot`

Body:

```md
## Goal

Help users follow up after applying.

## User Story

As a user, I want follow-up reminders so that I do not lose track of applications after submitting them.

## Requirements

- [ ] Add follow-up date field
- [ ] Set default follow-up window
- [ ] Allow user to edit reminder date
- [ ] Show follow-up reminders in dashboard
- [ ] Support email reminders if email system is enabled

## Acceptance Criteria

- [ ] Follow-up date can be set
- [ ] Reminder appears in dashboard
- [ ] User can change reminder date
- [ ] Reminder is linked to application record
```

---

## Issue 13: Add privacy and data deletion controls

Labels:

* `privacy`
* `backend`
* `mvp`
* `priority: high`

Milestone:

* `V1 — MVP Application Copilot`

Body:

```md
## Goal

Give users control over their personal job-search data.

## User Story

As a user, I want to delete my resume, applications, and account data so that I can control my personal information.

## Requirements

- [ ] Delete resume
- [ ] Delete parsed resume data
- [ ] Delete saved job posting
- [ ] Delete application record
- [ ] Delete cover letter
- [ ] Delete account
- [ ] Document data deletion behavior
- [ ] Avoid unnecessary collection of sensitive data

## Acceptance Criteria

- [ ] User can delete uploaded resume
- [ ] User can delete application records
- [ ] User can request or complete account deletion
- [ ] Deleted data is not used in future AI outputs
```

---

## Issue 14: Define pricing and free-tier limits

Labels:

* `billing`
* `product`
* `priority: medium`

Milestone:

* `V1 — MVP Application Copilot`

Body:

```md
## Goal

Define the initial pricing and free-tier model.

## User Story

As a product owner, I want a simple pricing model so that the MVP can be tested without overcomplicating billing.

## Requirements

- [ ] Define free-tier limits
- [ ] Define paid-tier value
- [ ] Decide whether billing is included in V1
- [ ] Define usage limits for AI job analyses
- [ ] Define usage limits for cover letters
- [ ] Define upgrade triggers

## Acceptance Criteria

- [ ] Pricing model is documented
- [ ] Free-tier usage limit is defined
- [ ] Paid-tier value proposition is defined
- [ ] Billing implementation is either scoped or explicitly deferred
```

---

# Suggested GitHub CLI Commands

If GitHub CLI is installed and authenticated, issues can be created with commands like:

```bash
gh issue create \
  --repo terrence-gonsalves/job-copilot \
  --title "Define product requirements for Canadian Job Copilot" \
  --body-file docs/issues/001-product-requirements.md \
  --label "product,mvp,priority: high"
```

Before using labels in commands, create the labels in GitHub manually or through GitHub CLI.

Example:

```bash
gh label create "mvp" --repo terrence-gonsalves/job-copilot
gh label create "priority: high" --repo terrence-gonsalves/job-copilot
gh label create "product" --repo terrence-gonsalves/job-copilot
```
