# Athens Job/Internship Opportunity Tracker

##  Overview

This repository represents the culminating project for CSCI 4300 – Web Programming at UGA.  
Our team collaboratively designed, developed, and deployed this full-stack web application using React + Next.js, Node.js and MongoDB. Our application is a Athens/UGA Job, Internship or Opportunity Tracker. Users can search for jobs or paste a resume that will be parsed by a LLM (OpenAI Open-Source model hosted by Groq) that return ATS keywords relevant to the resume. Users can then click the keywords to query an API (Jsearch API from RapidAPI) with those keywords to find jobs relevant to their resume. Users can CREATE (add jobs returned by the API to the tracker), READ (read information about the jobs on the tracker), UPDATE (update job application information in the tracker), and DELETE (delete jobs from the tracker). 

---

## Our Team - Internship_Tracker

| Member Name      | GitHub Username      | Role          |
|------------------|----------------------|---------------|
| Gaurish Vasireddy|      GaurishHaveFun        | Project Manager & Team Lead  |
| Allen Chiu       |           allchiu           | Communication Leader   |
| Shishir Lohar    |          winterblacksmith            | Member |

---
## Screenshots

<img width="1706" height="944" alt="Screenshot 2026-01-29 at 4 00 05 PM" src="https://github.com/user-attachments/assets/4c5252bf-207b-4e9b-b1da-85948563cdbc" />
<img width="1710" height="946" alt="Screenshot 2026-01-29 at 4 00 15 PM" src="https://github.com/user-attachments/assets/6769e625-abb6-4768-b392-8234f5b07049" />
<img width="1680" height="943" alt="Screenshot 2026-01-29 at 4 09 49 PM" src="https://github.com/user-attachments/assets/6a0e9bb0-45f8-4b2d-8617-d162118a4a28" />
<img width="1704" height="943" alt="Screenshot 2026-01-29 at 4 10 30 PM" src="https://github.com/user-attachments/assets/8815e3d3-a053-4aa4-b844-a80e2063ce4b" />

## Project Features 

- Authentication & Authorization** (login/sign-up, protected routes)  
- Middleware or Route Protection** for authenticated users  
- CRUD operations** using a database and API endpoints
- Responsive UI** & dynamic navigation bar  
- Users can SEARCH and TRACK for jobs using the application (search feature and dashboard/tracker feature)
- Features use of "openai/gpt-oss-20b" to scan through a parsed resume for ATS keywords pertaining to the user's resume for personalized and custom job queries.
 
---

## Repository Structure 

```
│── {athens-uga-opportunity-tracker}
│   └── src
|       └── auth.ts (nextAuth options configuration)
|       └── proxy.ts (middleware)
│       └── app - App Router pages & API routes
│            └──   components → Card.tsx, Footer.tsx, HeroSection.tsx, Nav.tsx, OpportunityCard.tsx, OpportunityList.tsx, ResumeModal.tsx
│            └──   models → Mongoose schemas / MongoDB models (User.ts and itemSchema.ts)
|            └──   dashboard → page.tsx
|            └──   job/[id] → page.tsx
|            └──   lib → groq.tsx (OpenAI GPT prompting), mongodb.ts, seed.ts
|            └──   login → page.tsx
|            └──   nonauth → page.tsx
|            └──   signup → page.tsx
|            └──   splash → page.tsx
|            └──   stats → page.tsx
|            └──   JobsContext.tsx (Process and holds Job endpoints for use throughout the project)
|            └──   layout.tsx
|            └──   not-found.tsx
|            └──   page.tsx
|            └──   providers.tsx (session provider)
│── design - mockups.md 
│── images - mockup images, etc.
│── .env (environment)
│── .env.local (environment for local)
└── status - WEEKLY_STATUS.md

```

---

## Tech Stack

| Layer             | Technology                                   |
|-------------------|----------------------------------------------|
| Frontend          | React + Next.js (App Router)                 |
| Backend           | Next.js API Routes / Node.js                 |
| Database          | MongoDB + Mongoose                           |
| Styling           | Tailwind CSS                                 |
| Authentication    | NextAuth.js                                  |

---

## Run the development server

```
npm run dev
```

The project should now be running at:
    http://localhost:3000

## API Endpoints 

| Method      | Endpoint             | Description            |
| ----------- | -------------------- | ---------------------- |
| GET         | /api/jobs            | Fetch all jobs for a particular user        |
| POST        | /api/jobs            | Create a new job      |
| GET         | /api/jobs/[id]       | Get job by ID         |
| PUT         | /api/jobs/[id]       | Update job by ID      |
| DELETE      | /api/jobs/[id]       | Delete job by ID      |
| POST        | /api/parse-resume    | Parses resume into JSON format and POSTS to Groq (openai/gpt-oss-20b) for ATS keyword processing             |
| POST        | /api/search-jobs     | Query JSearch API for jobs and POST data returned to the nonauth page for users (used in search bar and paste resume to search jobs)                |
| POST & GET  | /api/auth/[...nextauth]     | Add and fetch authOptions for NextAuth when needed |
| POST  | /api/auth/create-admin     | Creates/adds the admin user  |
| POST  | /api/auth/signup           | Creates/adds the a new user  |

## Database Models 
User.ts
| Field    | Type   | Description     |
| -------- | ------ | --------------- |
| name     | String | Full name       |
| email    | String | Unique email    |
| role     | String | admin/student   |
| password | String | Hashed password |
| timestamps | String | Timestamp of "createdAt" and "updateAt" in mongoDB|

itemSchema.ts
| Field                                | Type     | Description                                      |
| ------------------------------------ | -------- | ------------------------------------------------ |
| userId                               | String   | User identifier (required, indexed)              |
| role                                 | String   | Job role/position (required)                     |
| company                              | String   | Company name (required)                          |
| location                             | String   | Job location (required)                          |
| status                               | String   | Applied/Interview/Offer/Accepted/Rejected        |
| link                                 | String   | Job posting URL                                  |
| notes                                | String   | Additional notes                                 |
| job_id                               | String   | Unique job identifier from JSearch API           |
| employer_name                        | String   | Employer name                                    |
| employer_logo                        | String   | URL to employer logo                             |
| employer_website                     | String   | Employer website URL                             |
| employer_company_type                | String   | Type of company                                  |
| job_publisher                        | String   | Job posting publisher                            |
| job_employment_type                  | String   | Full-time/Part-time/Contract/etc.                |
| job_title                            | String   | Job title                                        |
| job_apply_link                       | String   | Direct application link                          |
| job_apply_is_direct                  | Boolean  | Whether application is direct                    |
| job_apply_quality_score              | Number   | Quality score of application                     |
| job_description                      | String   | Full job description                             |
| job_is_remote                        | Boolean  | Whether job is remote                            |
| job_posted_at_timestamp              | Number   | Unix timestamp of posting                        |
| job_posted_at_datetime_utc           | Date     | UTC date/time of posting                         |
| job_city                             | String   | Job city                                         |
| job_state                            | String   | Job state/province                               |
| job_country                          | String   | Job country                                      |
| job_latitude                         | Number   | Geographic latitude                              |
| job_longitude                        | Number   | Geographic longitude                             |
| job_benefits                         | [String] | Array of job benefits                            |
| job_google_link                      | String   | Google search link for job                       |
| job_offer_expiration_datetime_utc    | Date     | UTC expiration date of offer                     |
| job_offer_expiration_timestamp       | Number   | Unix timestamp of offer expiration               |
| job_required_experience              | Object   | Experience requirements object                   |
| job_required_skills                  | [String] | Array of required skills                         |
| job_required_education               | Object   | Education requirements object                    |
| job_experience_in_place_of_education | Boolean  | Whether experience can replace education         |
| job_min_salary                       | Number   | Minimum salary                                   |
| job_max_salary                       | Number   | Maximum salary                                   |
| job_salary_currency                  | String   | Salary currency (USD/EUR/etc.)                   |
| job_salary_period                    | String   | Salary period (YEAR/MONTH/HOUR)                  |
| job_highlights                       | Object   | Qualifications/Responsibilities/Benefits object  |
| job_job_title                        | String   | Job title (duplicate field)                      |
| job_posting_language                 | String   | Language of job posting                          |
| job_onet_soc                         | String   | O*NET SOC code                                   |
| job_onet_job_zone                    | String   | O*NET job zone                                   |
| job_naics_code                       | String   | NAICS industry code                              |
| job_naics_name                       | String   | NAICS industry name                              |
| createdAt                            | Date     | Document creation timestamp (auto-generated)     |
| updatedAt                            | Date     | Document last update timestamp (auto-generated)  |

## Client Routes 
| Route         | Description       |
| ------------- | ----------------- |
| `/`           | Homepage/spash          |
| `/login`      | User login        |
| `/signup`     | User signup        |
| `/dashboard`  | User dashboard    |
| `/jobs/new`   | Adding new job     |
| `/jobs/[id]` | View job details and editing jobs page |
| `/nonauth` | Page for users to query for jobs and paste their resume  |
| `/stats` | stats page for admin (for testing)  |

## Future Improvements
- I think the project could benefit from better API choices. The JSearch API does not have a search-skill parameter, so we were forced into plugging in the ATS keywords from the LLM into the generic query. Therefore, some of the results weren't the best as the ATS keywords must be in the job title. The API can not query jobs by specifically skill. 

- I think the project could benefit from more CSS/Tailwind. I felt that some of our UI/UX were kind of barebones in terms of customization. Hopefully, in the future, we can maybe add custom tailwind and CSS components to liven up the frontend and UI/UX. 

- Lastly, I think we could improve on the backend of this project. Some of the API's are quite janky in terms of rate limits and request limits. The LLM API had a token API that we had to work around. I think we could've added some test functions that could help monitor those issues, as most of those API services provide documentation on how add those monitoring (rates/request/token) services. In addition, we could've done a better job of using NextAuth and used auth() instead of useSession(). This would've made our session processing across client and server side much easier and more uniform. 

