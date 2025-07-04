# Project Overview

This web application recreates key Google Classroom features for Biology pre-service teachers in collaborative settings (TPS, TAS and PTS) across North-East Nigeria. Teachers and students sign in with Google OAuth, then engage in:

- Class creation with embedded YouTube lectures, images and unique join codes  
- Time-bound pretests that students must complete before entering the main classroom  
- Real-time pairing of online students into small groups (2–3) with shared notes, chat and AI assistance  
- AI-powered group chat via OpenAI ChatGPT or Google Flash Gemini using a RAG pipeline (Context7 MCP ensures up-to-date SDKs)  
- Video/audio sessions powered by Daily.co (with Twilio fallback) and in-call text chat  
- Posttests that students take immediately before logging out, capturing final scores  
- Analytics dashboards for teachers showing per-student scores, time spent, join/leave timestamps, retention and engagement metrics, with gender breakdowns  

Development follows an AI-driven loop:  
Gemini CLI reads Markdown “memory bank” files → generates precise prompts for Google AI Studio → ingests, validates and documents generated code. Render.com hosts the app; Prisma + PostgreSQL and TablePlus manage data; Next.js + React, NextAuth.js and Socket.io form the core stack; Jest, React Testing Library and Cypress ensure quality.

## Objectives

1. Determine the impact of an AI-assisted platform on Biology pre-service teachers’ academic achievement in TPS, TAS and PTS collaborative settings.  
2. Examine the platform’s effect on pre-service teachers’ knowledge retention across TPS, TAS and PTS modalities.  
3. Measure engagement levels when using the AI platform in each collaborative setting.  
4. Analyze how gender influences the AI platform’s effect on academic achievement in collaborative settings.  
5. Compare knowledge retention outcomes between male and female pre-service teachers using the AI platform.  
6. Assess engagement differences by gender when interacting with the AI platform in collaborative learning scenarios. 

## Standards & Guidelines

- Research each integration’s **official API documentation** and proven implementation patterns before coding.  
- Always use the **latest stable**, non-deprecated libraries and frameworks.  
- Analyze the **existing codebase patterns and conventions**; adhere to established module and naming styles.  
- Confirm file paths and module names exist before referencing them in code or tests.  


## Technology Stack Evaluation

| Layer               | Node.js + EJS         | Next.js + React         | Vue.js + Nuxt          |
|---------------------|-----------------------|-------------------------|------------------------|
| SSR & SEO           | Basic                 | Advanced                | Advanced               |
| AI/Data Fetching    | Manual REST           | React Hooks + SWR       | Vue Composition + Axios|
| File-based Routing  | No                    | Yes                     | Yes                    |
| Developer Ecosystem | Mature                | Very Active             | Growing                |
| Scalability         | Medium                | High                    | Medium                 |

**Chosen:** Next.js + React for superior routing, SEO, rich ecosystem, and optimized AI data fetching.


## Core Services & Tools
Hosting & CI/CD: Render.com
Database: PostgreSQL (managed), TablePlus for local management
ORM: Prisma
Auth: Google OAuth via NextAuth.js
Real-time: Socket.io (Pairing & Chat)
Video/Audio Calls: Daily.co SDK (free tier), Twilio Video (paid fallback)
AI/Q&A: OpenAI ChatGPT & Google Flash Gemini via RAG pattern, Context7 MCP server for up-to-date SDKs
Testing: Jest, React Testing Library, Cypress

## Directory Structure:
/project-root
 /AITaskDocs
  /memory-bank
    ProjectOverview.md
  /tasks
    Task01_Setup.md
    Task02_Auth.md
    Task03_ClassManagement.md
    Task04_QuizEngine.md
    Task05_PairingCollab.md
    Task06_AIIntegration.md
    Task07_VideoChat.md
    Task08_AnalyticsDashboard.md
  /generated-code
  /prompts

## Roles & Responsibilities
UI/UX Engineer: Wireframes, component libraries, responsive design
Backend Engineer: API routes, database schemas, business logic
AI/RAG Engineer: RAG pipelines, vector DB (Pinecone), Context7 integration
QA Engineer: Test plans, automations, performance benchmarking

## Resources
- [Gemini Code Documentation](https://ai.google.dev/gemini-api/docs)
- [Context Engineering Best Practices](https://www.philschmid.de/context-engineering)

## Development Flow
Gemini CLI reads ProjectOverview.md → loads /tasks/Task01_Setup.md.
AI prompt is generated and fed to Google AI Studio.
Generated code lands in project directory.
Gemini CLI validates code, updates task file (session_start, last_stop, % complete).
Proceed to next task.

