<img width="1774" height="887" alt="SubSync logo" src="https://github.com/user-attachments/assets/ee3093f9-d849-47f2-8aca-4aa1c109c425" />

### 📘 SubSync | My Project Contributions

> A record of my responsibilities, implementations, and technical problem-solving throughout the project.

[![Notion](https://img.shields.io/badge/Notion-View_My_Contributions-000000?style=for-the-badge&logo=notion&logoColor=white)](https://app.notion.com/p/1-Subsync-3fabea03dbce80c8a1bbe24690ee9e8d?source=copy_link) **[Detailed Contributions and Development Notes →](https://app.notion.com/p/1-Subsync-3fabea03dbce80c8a1bbe24690ee9e8d?source=copy_link)**

# 🎬 SubSync

**Learn English while watching YouTube—with dual subtitles, vocabulary tools, and an AI Video Tutor in one place.**

A Chrome Extension-based English learning service combining English–Korean dual subtitles and a context-aware AI Video Tutor.

> Project: Encore Multi-Agent AI Orchestration, Cohort 2 · Team 4

[🌟 Features](#-key-features) · [🧩 Frontend Repo](https://github.com/931njhthe-star/subsync-frontend) · [⚙️ Backend Repo](https://github.com/931njhthe-star/subsync-backend) · [📊 Dashboard Repo](https://github.com/931njhthe-star/subsync-dashboard)

---

## 🚩 Table of Contents

1. [Project Overview](#-project-overview)
2. [Team](#-team)
3. [Motivation](#-motivation)
4. [Key Features](#-key-features)
5. [AI Video Tutor](#-ai-video-tutor)
6. [User Journey](#-user-journey)
7. [Analytics Dashboard](#-analytics-dashboard)
8. [Technology Stack](#-technology-stack)
9. [System Architecture](#-system-architecture)
10. [Repository Structure](#-repository-structure)
11. [Deployment and Verification](#️-deployment-and-verification)
12. [Related Documentation](#-related-documentation)

---

## ✨ Project Overview

<p align="center">
  <img src="https://raw.githubusercontent.com/teach97/subsync-assets/main/1.gif" alt="SubSync dual subtitles and transcript demo" width="740" />
</p>

**SubSync** is a Chrome Extension-based English learning service designed to make learning from YouTube videos more seamless.

Users can watch videos with **English–Korean dual subtitles** and a complete transcript, look up or save unfamiliar English words directly from the page, and ask the **AI Video Tutor** questions informed by the video subtitles and current playback position.

> **In one sentence:** An English learning experience that connects subtitles → vocabulary → AI conversation without interrupting the video.

The service consists of three main components:

| Component | Responsibility |
|---|---|
| **Chrome Extension** | Dual subtitles, transcript, vocabulary learning, Video Tutor, sign-in, and user preferences |
| **FastAPI Backend** | Authentication, word lookup and storage, AI Tutor requests, learning data, logging, and LLM usage management via REST APIs |
| **Streamlit Dashboard** | Internal monitoring and analysis of user activity, AI/API usage, and operational status |

---

## 👥 Team

| Member | Role | GitHub |
|---|---|---|
| Jihun Rho | Project Manager (PM) | [Profile ↗](https://github.com/931njhthe-star) |
| Hoon Kim | Frontend | [Profile ↗](https://github.com/teach97) |
| Soye Jeon | Dashboard | [Profile ↗](https://github.com/soyedev) |
| Seoyun Park | Backend | [Profile ↗](https://github.com/seoyun-park) |
| Gyeongrak Choi | AI | [Profile ↗](https://github.com/Kyeongrak-Choi) |

---

## 🧭 Motivation

YouTube offers an enormous amount of English-language content, but learning from a video often requires switching repeatedly between unrelated services.

```text
Watch YouTube → Encounter an unfamiliar word → Pause → Search a dictionary
              → Return to YouTube → Ask about the video → Open a separate AI tool
```

These interruptions fragment both viewing and learning. SubSync aims to bring the workflow together:

```text
YouTube → English–Korean subtitles → Word hover/click → Save vocabulary
        → Video Tutor → Learning history
```

**Project goals:**
- Combine YouTube viewing with natural, continuous English learning.
- Let learners look up and save vocabulary directly from subtitles.
- Support AI-powered questions and answers grounded in video context.
- Collect and analyze learning interaction data.

---

## 🌟 Key Features

<p align="center">
  <img src="https://raw.githubusercontent.com/teach97/subsync-assets/main/2.gif" alt="SubSync interactive UI and transcript demo" width="740" />
</p>

### Interactive Interface

The quick bar, overlaid subtitles, and main panel can be positioned and adjusted independently to preserve the viewing experience.

- **Drag-and-drop positioning:** Move the quick bar, video subtitles, and main panel to convenient locations.
- **Double-click to reset:** Restore each element to its default position with a smooth transition.
- **Contextual panel expansion:** The main panel opens relative to the current quick-bar location while preserving the user-selected layout.
- **Resizable main panel:** Eight resize handles support horizontal and vertical resizing; the transcript and AI Tutor areas scale with the panel.

<hr />

<p align="center">
  <img src="https://raw.githubusercontent.com/teach97/subsync-assets/main/3.gif" alt="SubSync video learning tab demo" width="740" />
</p>

### Video Learning Tab

Subtitles and learning tools are presented alongside the video, including playback-synchronized highlighting, transcript navigation, and instant word lookup.

- **English–Korean dual subtitles:** Display both subtitle languages, highlight the sentence at the current playback position, and show subtitles in both the video overlay and learning panel.
- **Transcript:** Browse or search the full transcript, jump to timestamps, and automatically highlight the currently playing sentence.
- **Word lookup on hover:** See quick definitions for English words in subtitles, transcripts, and AI Tutor replies without leaving the video.
- **Detailed vocabulary view:** Inspect phonetic transcriptions, parts of speech, general and contextual meanings, related expressions, and supplementary learning information.

<hr />

<p align="center">
  <img src="https://raw.githubusercontent.com/teach97/subsync-assets/main/6.gif" alt="SubSync saved vocabulary and viewing history demo" width="740" />
</p>

### Library Tab

Save vocabulary encountered while learning and manage saved words and watch history.

- **Save words:** Save vocabulary from subtitles, transcripts, or word-detail views.
- **Duplicate management:** Prevent duplicate saved entries while retaining relearning activity.
- **Vocabulary management:** View or delete saved words with immediate updates.
- **Viewing history:** Associate watch history with an account and reopen previously watched videos.

<hr />

<p align="center">
  <img src="https://raw.githubusercontent.com/teach97/subsync-assets/main/5.gif" alt="SubSync Google sign-in demo" width="740" />
</p>

### Google Sign-In

Google OAuth through **Supabase Auth** connects personal learning history to a user account.

- **Google OAuth:** Sign in using a Google account without creating a separate SubSync password.
- **Supabase Auth:** Manage authentication sessions and associate records with the signed-in user.
- **Learning history sync:** Access saved vocabulary and viewing history across environments through the account.

<hr />

<p align="center">
  <img src="https://raw.githubusercontent.com/teach97/subsync-assets/main/4.gif" alt="SubSync AI Tutor Q&A demo" width="740" />
</p>

### AI Tutor Tab

A conversational learning assistant answers questions using the current YouTube video and its subtitle context.

- **Context-aware Q&A:** Ask about expressions, sentences, and video content using the current subtitles and playback context.
- **Follow-up questions:** Continue conversations based on earlier questions and replies.
- **Proactive questions:** Optionally receive learning prompts suggested by the Tutor while watching.
- **Response feedback:** Submit feedback to evaluate AI Tutor responses.

<hr />

<p align="center">
  <img src="https://raw.githubusercontent.com/teach97/subsync-assets/main/7.gif" alt="SubSync settings tab demo" width="740" />
</p>

### Settings Tab

Customize learning behavior and the interface.

- **Themes:** Choose dark, light, or glass themes; the glass theme includes a responsive glass-like effect.
- **Fonts:** Select the system font or supported custom fonts.
- **Subtitles:** Enable or disable English–Korean dual subtitles and adjust display preferences.
- **Word lookup:** Configure hover-based vocabulary lookup in subtitles and transcripts.
- **AI Tutor:** Enable or disable proactive questions and adjust Tutor behavior during viewing.

---

## 🤖 AI Video Tutor

The project's central AI learning feature is designed not as a generic chatbot, but as a **Tutor that uses the context of the YouTube video currently being watched**.

```text
User question + Video ID + Current playback time + Subtitle/transcript context
                           + User learning information
                                   ↓
                               AI Tutor
                                   ↓
                         Context-aware answer
```

For example, a learner asking “Why did the speaker use this expression here?” can receive an answer informed by the subtitle text and playback position.

**Key capabilities:**
- **Gemini-based Q&A** grounded in subtitle and playback context.
- Conversation history and response-feedback storage.
- Interactive word lookup within AI Tutor responses.
- **Proactive questions** tied to video content.
- **LLM provider fallback:** Gemini → Groq → stub to handle failures or usage limits.
- **Prompt-injection protection:** System-level instructions are structurally separated from user questions and subtitle content so that text in the video cannot directly override Tutor rules.

---

## 🔄 User Journey

1. Install the Chrome Extension.
2. Open a YouTube video and activate SubSync.
3. Watch with English–Korean dual subtitles.
4. Hover over, click, and save unfamiliar vocabulary.
5. Ask the Video Tutor about video content.
6. Save learning activity to the backend.
7. Review operational and usage data in the dashboard.

---

## 📊 Analytics Dashboard

<img width="1114" height="851" alt="SubSync analytics dashboard screenshot" src="https://github.com/user-attachments/assets/3939fc96-7a75-4f9e-8408-dad6181dd649" />

The **Streamlit dashboard** analyzes service operation and AI/API usage. It retrieves data from the FastAPI Dashboard API and supports per-screen date ranges and filters.

- **Overview:** Time-based users and AI calls, daily usage, recent activity, and provider shares.
- **AI usage:** Requests and tokens by model/user, average and P95 latency, error rates, provider/day trends, and detailed records.
- **API activity:** Requests, success rates, response times, errors, and recent status codes by endpoint and user, with guidance for HTTP 429 rate limits.
- **Shared controls:** Date ranges, filters, connection status, API state, and latest snapshot information.

[📊 Open Dashboard](https://subsync-dashboard-5xicocfzxxf2lngqm4mj7s.streamlit.app)

---

## 🛠 Technology Stack

**Frontend**

| Technology | Purpose |
|---|---|
| Chrome Extension (Manifest V3) | YouTube learning UI |
| JavaScript / HTML / CSS | Extension logic and interface |
| Chrome APIs | Browser integration and authentication |

**Backend**

| Technology | Purpose |
|---|---|
| Python 3.11+ / FastAPI | REST API |
| Uvicorn | ASGI server |
| Pydantic | Request and response schemas |
| uv | Dependency and package management |
| pytest | Automated testing |

**AI**

| Technology | Purpose |
|---|---|
| Google Gemini | Video Tutor |
| Groq | LLM fallback |
| Prompt engineering / context builder | Video-aware prompts and subtitle context |

**Database / Authentication**

| Technology | Purpose |
|---|---|
| Supabase (PostgreSQL, Auth) | Data storage and user authentication |
| Google OAuth / JWT | Login and API authentication |

**Cache / Dashboard / Deployment**

| Technology | Purpose |
|---|---|
| Redis | Session and vocabulary lookup caching |
| Streamlit + Pandas | Operational analytics dashboard |
| Render | Backend hosting |
| Chrome Web Store | Extension distribution |

---

## 🏗 System Architecture

```text
┌─────────────────────────────────────────────┐
│                 User Browser                │
│                 YouTube Page                │
│               Chrome Extension              │
│  ┌───────────────┬──────────┬─────────────┐ │
│  │Dual Subtitles │Transcript│ Video Tutor │ │
│  └───────────────┴──────────┴─────────────┘ │
└────────────────────────┬────────────────────┘
                         │ HTTPS REST API
                         ▼
┌─────────────────────────────────────────────┐
│               FastAPI Backend               │
│    Auth / Dictionary / Words / Tutor / Logs │
└──────────┬───────────────┬──────────────────┘
           ▼               ▼                  ▼
     ┌──────────┐    ┌──────────┐    ┌──────────────┐
     │ Supabase │    │  Redis   │    │ Gemini/Groq  │
     │ Postgres │    │  Cache   │    │     LLM      │
     └────┬─────┘    └──────────┘    └──────────────┘
          ▼
┌──────────────────────────────┐
│     Streamlit Dashboard      │
│     User / AI / API Metrics  │
└──────────────────────────────┘
```

---

## 📦 Repository Structure

SubSync is split into **three repositories** by responsibility:

```text
SubSync
├── subsync-frontend   → Chrome Extension
├── subsync-backend    → FastAPI REST API
└── subsync-dashboard  → Streamlit Analytics Dashboard
```

| Repository | Description | Link |
|---|---|---|
| **subsync-frontend** | Build-free Chrome Manifest V3 extension | [View](https://github.com/931njhthe-star/subsync-frontend) |
| **subsync-backend** | FastAPI REST API service | [View](https://github.com/931njhthe-star/subsync-backend) |
| **subsync-dashboard** | Streamlit operational and analytics dashboard | [View](https://github.com/931njhthe-star/subsync-dashboard) |

---

## ☁️ Deployment and Verification

The backend is hosted on **Render**. Example endpoints:

```text
GET https://subsync-backend-4bmh.onrender.com/health
GET https://subsync-backend-4bmh.onrender.com/api/v1/dictionary/hover?word=honest
```

> The `/health` endpoint checks process health only; it does not guarantee that third-party dictionary, translation, or LLM providers are operational.

The dashboard is deployed on **Streamlit Cloud**, and the frontend is published to the **Chrome Web Store**:

- [Dashboard (Streamlit)](https://subsync-dashboard-5xicocfzxxf2lngqm4mj7s.streamlit.app)
- [Frontend (Chrome Extension)](https://chromewebstore.google.com/detail/subsync/akckibdjhdhehbfjellpgododmcpfphc?authuser=0&hl=ko)

> Render instances may sleep after approximately 15 minutes of inactivity. If data does not appear immediately, allow the service to wake up and refresh.

---

## 📚 Related Documentation

- [Project Dashboard](https://yleeylee.notion.site/Subsync-2102b0d658a68394bc070175f52809d0)
