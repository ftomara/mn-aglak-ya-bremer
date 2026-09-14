# CodeRefine Qualification 2 - Carieeer

## [Excalidraw file](carieersystemarch.excalidraw)

## Functional Requirements :

**Candidates:**

- can create profile with skills, experience and other details
- can search & view list of jobs
- can get matched and apply to matching job
- can view missing skills for a specific job
- can view applied job state updates (Applied → Screened → Interview → Offer → Rejected)
- can get notifications of matching jobs and applied jobs updates and other events 

**Employers:**

- can create profile with company information
- can post open positions and create jobs (with all of job's details i.e. salary)
- can search & view candidates 
- can get notifications of matching candidates / applications
- can get candidate job state updates (Applied → Screened → Interview → Offer → Rejected)

## nonFunctional Requirements :
- consistency >> availability : job states and open positions should be consistent for good ux to get current job openings realtime without any delays
- scalability : system should be able to maintain a large number of users 50M DAU
- low latency : get search results <300ms
- security

## Data Model :

```text
Candidate {
    can_id(PK),
    user_name,
    email,
    hashed_password,
    skills[],
    education,
    portfolio_url,
    experience,
    applications[],
}
```

```text
Employer {
    emp_id(PK),
    user_name,
    email,
    hashed_password,
    company_info,
    jobs_ids[],
}
```


```text
Job {
    job_id(PK),
    emp_id(FK),
    status <Open, Closed>,
    title,
    desc,
    salary,
    skills_req[],
    application_ids[](FK),
}
```

```text
Application {
    app_id(PK),
    emp_id(FK),
    can_id(FK),
    status <Applied, Screened, Interview, Offer, Rejected>,
    cand_cv,
}
```

## API Design

**`POST /create_profile/candidate`** → `Candidate`

```text
{
    user_name,
    email,
    hashed_password,
    skills[],
    education,
    portfolio_url,
    experience,
}
```
**`POST /create_profile/employer`** → `Employer`

```text
{
    user_name,
    email,
    hashed_password,
    company_info,
}
```
**`GET /search_jobs/job?skills=[]&payrange=[]&keywords=[]`** → `Job[]`

**`GET /search_candidates/candidate?expertise=[]&experiencelevel={}&keywords=[]`** → `Candidate[]`

**`GET /jobs/job?page={}`** → `Job[]`

**`GET /candidates/candidate?page={}`** → `Candidate[]`

**`GET /match/candidate_id`** → `Job[]`

**`GET /match/job_id`** → `Candidate[]`

**`GET /match/job_id/missingskills?cand_id={}`** → `missing_skills[]`

**`POST /application/apply`** → `Application`

```text
{
    app_id,
    emp_id,
    can_id,
    status <Applied>,
    cand_cv,
}
```
**`GET /application/status/job_id/cand_id`** → `status <Applied, Screened, Interview, Offer, Rejected>`

**`POST /create_job`** → `Job`

```text
{
    emp_id,
    status <Open>,
    title,
    desc,
    salary,
    skills_req[],
}
```

## High level architecture :
<img width="1210" height="648" alt="Screenshot 2026-09-14 at 1 20 17 PM" src="https://github.com/user-attachments/assets/9538e1a2-16bd-436e-aa16-b48b2a8e03a2" />

----
[Deep Dives](deep_dives.md)
---
## Team Members :
### Fatma Omara
### Salma Shaker




