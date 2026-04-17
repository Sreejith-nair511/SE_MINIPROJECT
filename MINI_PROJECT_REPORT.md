# Engineering Career OS — Mini Project Report

---

## 1. Mini Project Title & Problem Statement

**Title:** Engineering Career OS — A Unified Career Development Platform for Engineering Students

### Problem Definition

Engineering students in India face a fragmented career preparation landscape. They must juggle multiple disconnected platforms — YouTube for learning, LinkedIn for networking, Unstop/Hack2Skill for hackathons, Canva for resumes, and various AI tools for guidance. There is no single, cohesive platform that brings all these career-building tools together in one place.

### Real-World Relevance

With over 1.5 million engineering graduates entering the Indian job market annually, the competition is intense. Most students lack structured guidance on what to learn, how to present themselves, and where to compete. This platform directly addresses that gap by providing a one-stop career OS tailored for Indian engineering students.

---

## 2. Abstract

### Problem

Engineering students lack a unified platform that combines structured learning, career tools, hackathon discovery, and AI-powered guidance. The fragmented ecosystem wastes time and creates inconsistent learning outcomes.

### Proposed Solution

Engineering Career OS is a full-stack web application that integrates:
- Curated engineering courses (sourced from YouTube playlists via API)
- An AI-powered career assistant (powered by Groq LLM)
- An ATS-optimized resume builder with live preview
- A hackathon discovery hub with embedded Unstop and Hack2Skill feeds
- Personalized learning roadmaps for different engineering specializations
- A progress-tracking dashboard with enrollment management

### Technology Used

Next.js 16, TypeScript, Tailwind CSS, Supabase (PostgreSQL), Clerk (Auth), Groq AI SDK, shadcn/ui, Radix UI

### Application / Impact

Students can go from zero to job-ready using a single platform — learning, building their resume, competing in hackathons, and getting AI guidance — all without switching tools.

---

## 3. Objectives

1. **Build a centralized learning hub** — Aggregate 300+ engineering courses with filtering by category, level, and search, backed by a real Supabase database.
2. **Enable AI-assisted career guidance** — Integrate a Groq-powered AI assistant that answers career, coding, and learning questions in real time.
3. **Simplify hackathon discovery** — Embed live Unstop and Hack2Skill feeds alongside curated hackathon cards so students never miss an opportunity.
4. **Provide a professional resume builder** — Allow students to create, preview, and export ATS-optimized resumes directly within the platform.

---

## 4. Stakeholders / Users / Investors

| Role | Who | How They Benefit |
|---|---|---|
| Primary Users | Engineering students (B.Tech / B.E.) | Access to courses, resume builder, hackathons, AI assistant |
| Secondary Users | Recent graduates / job seekers | Career roadmaps, mock interview prep, skill tracking |
| Instructors / Content Creators | YouTube educators, course creators | Exposure through platform course listings |
| Recruiters / Companies | HR teams, startups | Access to a pool of skilled, verified candidates |
| Platform Investors | EdTech VCs, angel investors | Scalable SaaS model targeting India's 8M+ engineering students |
| Hackathon Platforms | Unstop, Hack2Skill | Increased traffic and registrations via embedded feeds |

---

## 5. Team Members & Roles

| Name | Role | Responsibilities |
|---|---|---|
| Sreejith Nair | Team Lead & Full Stack Developer | Architecture, Next.js pages, Supabase integration, deployment |
| Member 2 | Frontend Developer | UI components, Tailwind styling, responsive design |
| Member 3 | Backend Developer | API routes, Supabase schema, Clerk auth integration |
| Member 4 | QA Tester | Test case design, manual testing, bug reporting |
| Member 5 | UI/UX Designer | Wireframes, design system, component library |
| Member 6 | Scrum Master | Sprint planning, Jira board management, stand-ups |

---

## 6. System Overview / Proposed Solution

The system follows a **client-server architecture** built on Next.js App Router with server-side rendering for performance and SEO.

**High-Level Flow:**

```
User visits platform
       ↓
Clerk Authentication (Sign In / Sign Up)
       ↓
Dashboard — shows enrolled courses, progress, streaks
       ↓
┌──────────────────────────────────────────┐
│  Courses  │  AI Assistant  │  Hackathons │
│  Roadmaps │  Resume Builder│  Settings   │
└──────────────────────────────────────────┘
       ↓
Supabase DB — stores courses, enrollments, progress
       ↓
Groq AI API — powers the AI assistant chat
       ↓
YouTube API — populates course catalog
```

Users authenticate via Clerk, land on their dashboard, and can navigate to any module. All course data is stored in Supabase and fetched server-side. The AI assistant streams responses from Groq. The hackathons page embeds live feeds from Unstop and Hack2Skill.

---

## 7. System Architecture Diagram

```
┌─────────────────────────────────────────────────────────┐
│                     CLIENT LAYER                        │
│  Next.js 16 App Router (React 19, TypeScript)           │
│  Tailwind CSS + shadcn/ui + Radix UI Components         │
└────────────────────────┬────────────────────────────────┘
                         │ HTTP / Server Actions
┌────────────────────────▼────────────────────────────────┐
│                   SERVER LAYER                          │
│  Next.js API Routes (/api/chat, /api/populate-courses)  │
│  Clerk Middleware (Auth guard on protected routes)      │
│  Server Components (SSR for courses, dashboard)         │
└──────┬──────────────────┬───────────────────────────────┘
       │                  │
┌──────▼──────┐    ┌──────▼──────────────────────────────┐
│  SUPABASE   │    │         EXTERNAL APIS               │
│  PostgreSQL │    │  Groq AI (LLM chat completions)     │
│  - courses  │    │  YouTube Data API v3 (playlists)    │
│  - enrollments   │  Clerk (JWT auth, user management)  │
│  - progress │    │  Unstop / Hack2Skill (iframe embed) │
└─────────────┘    └─────────────────────────────────────┘
```

**Layers explained:**
- **Client Layer** — React components rendered in the browser. Uses React hooks for local state, server components for data-heavy pages.
- **Server Layer** — Next.js handles SSR, API routes, and middleware. Clerk middleware protects `/dashboard`, `/courses`, `/resume-builder`, etc.
- **Data Layer** — Supabase (PostgreSQL) stores all persistent data. Accessed via `@supabase/ssr` for server-side and `@supabase/supabase-js` for client-side.
- **External APIs** — Groq for AI, YouTube for course population, Clerk for identity.

---

## 8. Technology Stack

| Layer | Technology | Version / Notes |
|---|---|---|
| **Frontend** | Next.js | 16.1.6 (App Router, Turbopack) |
| **Frontend** | React | 19.2.3 |
| **Frontend** | TypeScript | 5.7.3 |
| **Frontend** | Tailwind CSS | 3.4.17 |
| **Frontend** | shadcn/ui + Radix UI | Component library |
| **Frontend** | Lucide React | 0.544.0 (icons) |
| **Backend** | Next.js API Routes | Server-side logic |
| **Backend** | Groq SDK | 0.37.0 (AI chat) |
| **Database** | Supabase (PostgreSQL) | 2.95.3 |
| **Auth** | Clerk | 6.37.4 |
| **Forms** | React Hook Form + Zod | Validation |
| **Charts** | Recharts | 2.15.0 |
| **Package Manager** | pnpm | 10.x |
| **IDE** | VS Code / Kiro IDE | — |
| **Version Control** | Git + GitHub | — |
| **Task Tracking** | Jira | Agile sprint management |

---

## 9. Requirements

### Functional Requirements

| ID | Feature | Description |
|---|---|---|
| FR-01 | User Authentication | Sign up, sign in, sign out via Clerk (email + OAuth) |
| FR-02 | Course Catalog | Browse, search, filter courses by category and level |
| FR-03 | Course Enrollment | Enroll in courses, track progress per course |
| FR-04 | AI Assistant | Chat interface with Groq-powered LLM for career guidance |
| FR-05 | Resume Builder | Create resume with sections (experience, education, skills), live preview, export |
| FR-06 | Hackathon Discovery | View curated hackathon cards + embedded Unstop/Hack2Skill feeds |
| FR-07 | Learning Roadmaps | View structured roadmaps for different engineering paths |
| FR-08 | Dashboard | Personalized view of enrolled courses, progress, and activity |
| FR-09 | Course Population | Admin API to sync YouTube playlists into the course database |
| FR-10 | Pagination & Filtering | Server-side pagination on course listings |

### Non-Functional Requirements

**Performance**
- Page load time under 2 seconds for server-rendered pages
- Turbopack dev server for fast HMR (< 500ms)
- Supabase queries optimized with indexes on `category`, `level`, `created_at`

**Security**
- All protected routes guarded by Clerk middleware
- Supabase Row Level Security (RLS) enabled
- Environment variables never exposed to client (service role key server-only)
- `NEXT_PUBLIC_` prefix only for safe-to-expose keys

**Usability**
- Fully responsive — mobile, tablet, desktop
- Dark-first design with consistent color system
- Accessible components via Radix UI primitives
- Clear empty states and loading indicators

---

## 10. Use Case Modeling

### Use Cases (Text)

**UC-01: Student Enrolls in a Course**
- Actor: Authenticated Student
- Precondition: Student is signed in
- Flow: Student browses courses → applies filters → clicks course → views details → clicks "Enroll" → enrollment saved to Supabase → course appears in dashboard
- Postcondition: Course visible in "My Courses" with 0% progress

**UC-02: Student Uses AI Assistant**
- Actor: Authenticated Student
- Precondition: Student is signed in, Groq API key configured
- Flow: Student navigates to AI Assistant → types a career/coding question → message sent to `/api/chat` → Groq streams response → response rendered with markdown formatting
- Postcondition: Conversation history maintained in session

**UC-03: Student Discovers a Hackathon**
- Actor: Any User (authenticated or not)
- Precondition: None
- Flow: User navigates to Hackathons → views curated cards with prize/date/tags → switches to Unstop tab → embedded iframe loads live Unstop hackathon listings → clicks "Register" → redirected to platform
- Postcondition: User registers on external platform

### Use Case Diagram

```
                    ┌─────────────────────────────────┐
                    │        Engineering Career OS     │
                    │                                  │
  ┌──────────┐      │  ┌─────────────────────────┐    │
  │          │─────▶│  │   Browse Courses         │    │
  │          │      │  └─────────────────────────┘    │
  │          │─────▶│  ┌─────────────────────────┐    │
  │ Student  │      │  │   Enroll in Course       │    │
  │  (Auth)  │─────▶│  └─────────────────────────┘    │
  │          │      │  ┌─────────────────────────┐    │
  │          │─────▶│  │   Use AI Assistant       │    │
  │          │      │  └─────────────────────────┘    │
  │          │─────▶│  ┌─────────────────────────┐    │
  └──────────┘      │  │   Build Resume           │    │
                    │  └─────────────────────────┘    │
  ┌──────────┐      │  ┌─────────────────────────┐    │
  │  Guest   │─────▶│  │   View Hackathons        │    │
  │  User    │      │  └─────────────────────────┘    │
  └──────────┘      │  ┌─────────────────────────┐    │
                    │  │   View Roadmaps          │    │
  ┌──────────┐      │  └─────────────────────────┘    │
  │  Admin   │─────▶│  ┌─────────────────────────┐    │
  └──────────┘      │  │   Populate Courses (API) │    │
                    │  └─────────────────────────┘    │
                    └─────────────────────────────────┘
```

---

## 11. System Design

### Class Diagram (Core Entities)

```
┌─────────────────────┐       ┌─────────────────────┐
│        User         │       │       Course         │
├─────────────────────┤       ├─────────────────────┤
│ id: string (Clerk)  │       │ id: uuid             │
│ email: string       │       │ title: string        │
│ name: string        │       │ description: string  │
└────────┬────────────┘       │ instructor: string   │
         │                    │ category: string     │
         │ 1                  │ level: string        │
         │                    │ thumbnail_url: string│
         ▼ N                  │ youtube_playlist_id  │
┌─────────────────────┐       │ price: number        │
│    Enrollment       │       │ created_at: timestamp│
├─────────────────────┤       └──────────┬──────────┘
│ id: uuid            │                  │
│ user_id: string     │◀─────────────────┘ 1
│ course_id: uuid     │       N
│ enrolled_at: ts     │
└────────┬────────────┘
         │
         ▼
┌─────────────────────┐
│      Progress       │
├─────────────────────┤
│ id: uuid            │
│ user_id: string     │
│ course_id: uuid     │
│ completed: boolean  │
│ updated_at: ts      │
└─────────────────────┘
```

### Sequence Diagram — Course Enrollment

```
Student        Browser         Next.js Server      Supabase
   │               │                  │                │
   │─── Click ────▶│                  │                │
   │   "Enroll"    │                  │                │
   │               │── POST /enroll ─▶│                │
   │               │                  │── INSERT ─────▶│
   │               │                  │   enrollments  │
   │               │                  │◀── success ────│
   │               │◀── 200 OK ───────│                │
   │◀── Update UI ─│                  │                │
   │  (enrolled=true)                 │                │
```

---

## 12. Agile Methodology

### Primary: Scrum

The project followed a 2-week sprint cycle with the following structure:

**Sprint 1 — Foundation**
- Project setup (Next.js, Tailwind, Clerk, Supabase)
- Authentication flow (sign-in, sign-up, middleware)
- Database schema design and migrations

**Sprint 2 — Core Features**
- Course catalog with Supabase integration
- Course enrollment and progress tracking
- Dashboard with enrolled courses view

**Sprint 3 — Advanced Features**
- AI Assistant with Groq streaming
- Resume Builder (sections, live preview, export)
- Hackathons page with Unstop/Hack2Skill embeds

**Sprint 4 — Polish & Deployment**
- Roadmaps page
- Bug fixes (ThemeProvider SSR, TypeScript errors)
- Performance optimization, production build

### Task Tracking (Jira)

| Epic | Story | Status |
|---|---|---|
| Auth | Implement Clerk sign-in/sign-up | Done |
| Courses | Build course catalog with filters | Done |
| Courses | Enroll + progress tracking | Done |
| AI | Groq chat API integration | Done |
| Resume | Resume builder with live preview | Done |
| Hackathons | Curated cards + iframe embeds | Done |
| Roadmaps | Engineering path roadmaps | Done |
| DevOps | GitHub CI, Vercel deployment | Done |

**Optional secondary methodology:** Kanban was used informally for bug tracking — a simple To Do / In Progress / Done board for hotfixes between sprints.

---

## 13. Implementation / Screenshots

### Key Features

**1. Dashboard**
- Personalized welcome card with user name
- Enrolled courses with progress bars
- Quick navigation to all modules

**2. Course Catalog (`/courses`)**
- Server-side rendered grid of 300+ courses
- Sidebar filters: category, level, search
- Pagination (12 per page)
- Each card shows instructor, level, thumbnail, enroll status

**3. AI Assistant (`/ai-assistant`)**
- Chat interface with message history
- Markdown rendering for code blocks and lists
- Powered by Groq (llama3-8b-8192 model)
- Streaming responses for real-time feel

**4. Resume Builder (`/resume-builder`)**
- Form sections: Personal Info, Experience, Education, Skills
- Live split-pane preview
- ATS-friendly formatting

**5. Hackathons (`/hackathons`)**
- Tab 1: Curated cards — SIH, HackWithInfy, Flipkart Grid, Google Solution Challenge, Microsoft Imagine Cup, Hack2Skill AI Challenge
- Tab 2: Embedded Unstop live feed (iframe)
- Tab 3: Embedded Hack2Skill live feed (iframe)
- Platform filter pills, prize/date/location/tags per card

---

## 14. Testing Approach

### Types of Testing Used

- **Unit Testing** — Individual component logic (form validation, filter functions)
- **Integration Testing** — API routes tested with real Supabase and Groq connections
- **System Testing** — End-to-end user flows (sign up → enroll → track progress)
- **Manual UI Testing** — Cross-browser and responsive layout verification

### Sample Test Cases

| Test ID | Test Case | Input | Expected Output | Status |
|---|---|---|---|---|
| TC-01 | User can sign up | Valid email + password | Redirected to `/dashboard` | Pass |
| TC-02 | Course filter by level | Level = "Beginner" | Only beginner courses shown | Pass |
| TC-03 | AI assistant responds | "What is system design?" | Streamed markdown response | Pass |
| TC-04 | Enroll in course | Click "Enroll" on course | Enrollment saved, button changes to "Enrolled" | Pass |
| TC-05 | Supabase URL missing | No `.env.local` | Error: `supabaseUrl is required` | Expected |
| TC-06 | Hackathon iframe loads | Click "Unstop" tab | Unstop website embedded in iframe | Pass |
| TC-07 | Resume builder preview | Fill in name + experience | Live preview updates in real time | Pass |
| TC-08 | Pagination works | Navigate to page 2 | Next 12 courses loaded | Pass |

---

## 15. Tools Used

| Tool | Purpose |
|---|---|
| **GitHub** | Version control, code hosting at `github.com/Sreejith-nair511/SE_MINIPROJECT` |
| **Jira** | Sprint planning, task tracking, backlog management |
| **VS Code / Kiro IDE** | Primary development environment |
| **Supabase Dashboard** | Database management, RLS policies, SQL editor |
| **Clerk Dashboard** | User management, API key configuration |
| **Vercel** | Production deployment and preview deployments |
| **Postman** | API route testing (`/api/chat`, `/api/populate-courses`) |
| **Figma** | UI wireframes and design system |
| **pnpm** | Fast, disk-efficient package management |

---

## 16. Challenges Faced

**1. Supabase SSR vs Client-Side Auth**
Clerk and Supabase both manage sessions differently. Getting server components to correctly read the authenticated user's ID and pass it to Supabase queries required careful use of `@supabase/ssr` and Clerk's `auth()` helper — they couldn't be mixed naively.

**2. ThemeProvider SSR Crash**
The `ThemeProvider` component caused a production build crash because it used `useContext` in a way that wasn't safe during server-side rendering. Fixed by ensuring the context always has a default value and wrapping with a client boundary.

**3. YouTube API Quota**
The `/api/populate-courses` route hits YouTube's Data API v3, which has a strict daily quota of 10,000 units. Bulk playlist fetching exhausted the quota quickly. Solved by adding upsert logic so re-runs don't re-fetch already-stored courses.

**4. iframe Embedding Restrictions**
Both Unstop and Hack2Skill set `X-Frame-Options` headers that block embedding on some browsers. Handled gracefully with a fallback "Open in new tab" button and a user-facing notice explaining the limitation.

**5. TypeScript Strict Mode**
With `strict: true` in tsconfig, many `any` types from Supabase responses caused compile errors. Required explicit typing of all database response shapes and careful use of type assertions.

**6. Environment Variable Management**
The project uses `.env.local` (not committed) for secrets. New team members frequently hit the `supabaseUrl is required` error because they only had `.env.example`. Documented the setup process clearly in README.

---

## 17. Conclusion

Engineering Career OS successfully delivers a unified career development platform for engineering students. The project achieved all four core objectives:

- A fully functional course catalog backed by a real Supabase database with search, filtering, and pagination
- A working AI assistant powered by Groq that provides real-time career and coding guidance
- A hackathon discovery hub with curated listings and live embedded feeds from Unstop and Hack2Skill
- A professional resume builder with live preview and ATS-optimized output

Beyond the features, the project demonstrated practical application of modern full-stack engineering practices — server-side rendering with Next.js App Router, secure authentication with Clerk, real-time AI streaming, and agile development with Scrum sprints tracked in Jira.

The platform is deployed and production-ready, with a clean codebase on GitHub and a scalable architecture that can support thousands of concurrent users. Future enhancements could include peer-to-peer mentorship, coding challenge integration, and a mobile app.

---

*Report prepared for Software Engineering Mini Project | April 2026*
