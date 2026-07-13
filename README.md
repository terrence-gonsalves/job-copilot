This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.
=======
# Job Copilot

A Canadian-first AI job-search copilot designed to help job seekers find relevant Canadian roles, tailor application materials, and manage the job-search process with more structure and less repetitive work.

## Product Direction

Job Copilot is not intended to be a mass auto-apply tool.

The product should prioritize:

* Application quality
* User control
* Canadian job-market relevance
* Transparent AI recommendations
* Resume-grounded outputs
* Privacy-conscious handling of user data

The core product idea:

> Help Canadians apply to the right jobs better, not simply apply to more jobs faster.

## Problem

Many AI job-search tools are built primarily around the U.S. job market. Canadian users can run into issues such as:

* ZIP code-only location fields
* No Canadian postal code support
* U.S.-only job listings
* Poor filtering for remote Canada roles
* Weak understanding of Canadian provinces, public-sector hiring, bilingual roles, and work authorization
* Generic resume and cover letter outputs that do not reflect Canadian hiring norms

## Target Users

Initial users:

* Canadian job seekers
* Canadian tech and digital professionals
* Career changers
* Mid-career professionals
* Applicants who want better organization and less repetitive application work

Future users may include:

* Newcomers to Canada
* Public-sector applicants
* Bilingual job seekers
* Remote-first Canadian workers

## Initial MVP

The first version focuses on a manual but high-value workflow:

1. User creates an account.
2. User uploads a resume.
3. The system parses the resume into structured profile data.
4. User pastes a Canadian job posting or job URL.
5. The system generates a job-fit analysis.
6. The system suggests resume improvements.
7. The system drafts application material.
8. User tracks the application and follow-up status.

## Core Differentiators

* Canadian postal code and province support
* Canadian work authorization awareness
* Remote Canada and province-specific job filtering
* Public-sector and bilingual job-market awareness
* Resume-grounded AI outputs
* Human approval before any application action
* Application tracking built around quality, not volume

## Planned Roadmap

See `ROADMAP.md`.

## Planning Docs

See `docs/planning-pack.md`.

## Initial Build Philosophy

Start narrow.

The first version should not try to become Indeed, LinkedIn, Job Bank, Sonara, and Jobright at the same time.

The MVP should prove that the tool can help a Canadian job seeker:

* Understand whether a job is worth applying to
* Tailor their resume honestly
* Draft useful application material
* Track the application properly
* Follow up at the right time

Automated job discovery, ATS autofill, and market intelligence can come later.
