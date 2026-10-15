<img width="1774" height="887" alt="subysync 로고" src="https://github.com/user-attachments/assets/ee3093f9-d849-47f2-8aca-4aa1c109c425" />

# 🎬 SubSync


**YouTube를 보면서 자막, 단어 학습, AI Tutor까지 한 번에**

YouTube 영·한 이중자막과 AI Video Tutor를 결합한 Chrome Extension 기반 영어 학습 서비스

> 프로젝트: 엔코아 멀티 에이전트 AI 오케스트레이션 2기 · Team 4

[🌟주요 기능](#-주요-기능) · [🧩 Frontend Repo](https://github.com/931njhthe-star/subsync-frontend) · [⚙️ Backend Repo](https://github.com/931njhthe-star/subsync-backend) · [📊 Dashboard Repo](https://github.com/931njhthe-star/subsync-dashboard)

### 📘 Subsync | Project Contributions

> 프로젝트에서 직접 담당한 작업과 구현 과정, 기술적 문제 해결 경험을 정리한 문서입니다.

[![Notion](https://img.shields.io/badge/Notion-View_My_Contributions-000000?style=for-the-badge&logo=notion&logoColor=white)](https://app.notion.com/p/1-Subsync-3fabea03dbce80c8a1bbe24690ee9e8d?source=copy_link)

📌 **[상세 프로젝트 기여 내역 및 개발 기록 보기 →](https://app.notion.com/p/1-Subsync-3fabea03dbce80c8a1bbe24690ee9e8d?source=copy_link)**

---

## 🚩 목차

1. [프로젝트 소개](#-프로젝트-소개)
2. [기획 배경](#-기획-배경)
3. [주요 기능](#-주요-기능)
4. [팀원](#-팀원)
5. [AI Video Tutor](#-ai-tutor)
6. [서비스 이용 흐름](#-서비스-이용-흐름)
7. [대시보드](#-대시보드)
8. [기술 스택](#-기술-스택)
9. [시스템 아키텍처](#-시스템-아키텍처)
10. [프로젝트 구성](#-프로젝트-구성)
11. [배포 확인](#️-배포-확인)
12. [관련 문서](#-관련-문서)
---

## ✨ 프로젝트 소개

<p align="center">
  <img src="https://raw.githubusercontent.com/teach97/subsync-assets/main/1.gif" alt="SubSync 영상 학습 탭 이중자막·Script 시연" width="740" />
</p>

**SubSync**는 YouTube 영상을 시청하면서 영어를 학습할 수 있도록 만든 Chrome Extension 기반 영어 학습 서비스입니다.

사용자는 영·한 이중자막과 전체 Script를 확인하며 영상을 시청하고, 모르는 영어 단어를 마우스로 바로 조회하거나 저장할 수 있습니다. 또한 영상의 자막과 현재 재생 시점을 AI가 문맥으로 활용해 사용자가 영상 내용에 대해 질문하고 학습할 수 있는 **Video Tutor**를 제공합니다.

> **한 줄 소개**
> YouTube 영상 시청의 흐름을 끊지 않고 자막 → 단어 → AI 대화까지 연결하는 영어 학습 서비스

SubSync는 크게 세 개의 시스템으로 구성됩니다.

| 시스템 | 역할 |
|---|---|
| **Chrome Extension** | 이중자막, Script, 단어 학습, Video Tutor, 로그인, 학습 설정을 제공하는 사용자 화면 |
| **FastAPI Backend** | 인증, 단어 조회/저장, Tutor AI 호출, 학습 데이터 저장, 로그 수집, LLM 사용량 관리를 담당하는 REST API |
| **Streamlit Dashboard** | 사용자·AI·API 사용량과 운영 상태를 분석하는 내부 운영 화면 |

---

## 👥 팀원

| 이름 | 담당 영역 | GitHub |
|---|---|---|
| 노지훈 | PM | [열기 ↗](https://github.com/931njhthe-star) |
| 김훈 | Frontend | [열기 ↗](https://github.com/teach97) |
| 전소예 | Dashboard | [열기 ↗](https://github.com/soyedev) |
| 박서윤 | Backend | [열기 ↗](https://github.com/seoyun-park) |
| 최경락 | AI | [열기 ↗](https://github.com/Kyeongrak-Choi) |

---

## 🧭 기획 배경

YouTube는 영어 학습에 활용할 수 있는 방대한 영상 콘텐츠를 제공하지만, 실제 학습 과정에서는 여러 서비스 사이를 이동해야 하는 문제가 있습니다.

```
YouTube 시청 → 모르는 단어 발견 → 영상 일시정지 → 사전 검색
     → 다시 YouTube → 영상 내용 질문 → 별도의 AI 서비스 이용
```

이 과정이 반복되면 영상 시청과 학습의 흐름이 끊어집니다. SubSync는 이를 하나의 흐름으로 연결하는 것을 목표로 합니다.

```
YouTube → 영·한 이중자막 → 단어 Hover/Click → 단어 저장 → Video Tutor → 학습 기록
```

**목표**
- YouTube 시청과 영어 학습의 자연스러운 결합
- 영상에서 바로 모르는 단어 확인 및 개인 단어장 저장
- 영상 문맥 기반 AI 질의응답
- 학습 행동 데이터 기록 및 분석

---

## 🌟 주요 기능

<p align="center">
  <img src="https://raw.githubusercontent.com/teach97/subsync-assets/main/2.gif" alt="SubSync 인터랙티브 UI와 Script 시연" width="740" />
</p>

### 인터랙티브 UI

영상 시청 흐름을 끊지 않도록 퀵바, 영상 자막, 메인 패널을 자유롭게 배치하고 조작할 수 있습니다.

- **자유로운 드래그 이동**
  - 퀵바, 영상 위 자막, 메인 패널을 원하는 위치로 드래그할 수 있습니다.
  - 학습 환경과 영상 화면 구성에 맞춰 각 UI를 편리하게 배치할 수 있습니다.

- **더블클릭으로 원위치 복귀**
  - 퀵바·자막·메인 패널을 더블클릭하면 기본 위치로 부드럽게 돌아갑니다.
  - 화면을 정리하거나 처음 배치로 되돌리고 싶을 때 빠르게 복구할 수 있습니다.

- **퀵바 위치를 따라 펼쳐지는 패널**
  - 퀵바를 펼치면 메인 패널이 현재 퀵바 위치를 기준으로 이동한 뒤 자연스럽게 펼쳐집니다.
  - 사용자가 배치한 위치를 유지하면서 필요한 학습 화면을 바로 확인할 수 있습니다.

- **메인 패널 리사이징**
  - 메인 패널의 여덟 방향 핸들을 이용해 가로·세로 크기를 자유롭게 조절할 수 있습니다.
  - 패널 크기에 맞춰 Script와 AI Tutor 영역도 함께 확장되어 화면을 효율적으로 사용할 수 있습니다.

<hr />

<p align="center">
  <img src="https://raw.githubusercontent.com/teach97/subsync-assets/main/3.gif" alt="SubSync 영상 학습 UI" width="740" />
</p>

### 영상 학습 탭

영상 시청에 필요한 자막과 학습 도구를 한 화면에서 제공합니다. 재생 위치에 맞춘 자막 강조, Script 탐색, 단어 조회 기능을 사용할 수 있습니다.


- **영·한 이중자막**
  - YouTube 영상의 영어 자막과 한국어 자막을 함께 표시합니다.
  - 현재 재생 위치에 해당하는 문장을 자동으로 강조합니다.
  - 영상 위 자막과 학습 패널의 자막을 함께 확인할 수 있습니다.

- **Script**
  - 영상 전체 자막을 Script 형태로 확인합니다.
  - 자막 내용을 검색할 수 있습니다.
  - 타임스탬프를 클릭하면 해당 시점으로 이동합니다.
  - 현재 재생 중인 문장을 자동으로 강조합니다.

- **Mouse Hover 단어 조회**
  - 자막, Script, AI Tutor 답변에 포함된 영어 단어에 마우스를 올리면 간단한 뜻을 표시합니다.
  - 학습 흐름을 끊지 않고 단어 의미를 빠르게 확인할 수 있습니다.

- **단어 상세 조회**
  - 단어의 발음기호와 품사를 확인합니다.
  - 기본 정의와 현재 문맥에서의 의미를 제공합니다.
  - 관련 표현과 추가 학습 정보를 확인할 수 있습니다.


<hr />

<br />

<p align="center">
  <img src="https://raw.githubusercontent.com/teach97/subsync-assets/main/6.gif" alt="SubSync 저장소 탭 단어·시청 기록 시연" width="740" />
</p>

### 저장소 탭

학습 중 발견한 단어를 저장하고, 저장한 단어와 학습 이력을 관리합니다.

- **단어 저장**:
  - 자막·Script·단어 상세 화면에서 단어를 저장하고 목록에서 확인합니다.

- **중복 저장 관리**
  - 동일한 단어의 중복 저장을 방지하고 재학습 기록을 관리합니다.

- **저장 단어 관리**
  - 저장 단어를 조회·삭제하고 변경 사항을 즉시 반영합니다.

- **시청 기록 확인**
  - 시청 기록을 계정 기반으로 관리합니다.
  - 기록 영상을 클릭하면 해당 영상 링크가 열립니다.

<hr />

<br />

<p align="center">
  <img src="https://raw.githubusercontent.com/teach97/subsync-assets/main/5.gif" alt="SubSync 5번 기능 시연" width="740" />
</p>

### Google 로그인

Supabase Auth 기반 Google OAuth 로그인을 통해 학습 기록을 계정에 연결합니다.

- **Google OAuth 로그인**
  - Google 계정으로 간편하게 로그인합니다.
  - 별도의 SubSync 전용 비밀번호를 생성할 필요가 없습니다.

- **Supabase Auth 연동**
  - Supabase Auth를 통해 로그인 세션을 관리합니다.
  - 로그인 상태에 따라 학습 기록을 안전하게 연결합니다.

- **학습 기록 동기화**
  - 저장한 단어와 시청 기록을 계정에 연결합니다.
  - 다른 환경에서도 동일한 학습 기록을 확인할 수 있습니다.

<hr />

<p align="center">
  <img src="https://raw.githubusercontent.com/teach97/subsync-assets/main/4.gif" alt="SubSync AI Tutor 탭 질문·답변 시연" width="740" />
</p>

### AI Tutor 탭

현재 시청 중인 영상과 자막 문맥을 활용하여 영어 학습을 돕는 대화형 AI Tutor를 제공합니다.


- **영상 문맥 기반 질의응답**
  - 현재 영상의 자막과 문맥을 바탕으로 질문에 답변합니다.
  - 영상 속 표현, 문장, 내용에 대해 질문할 수 있습니다.

- **대화형 후속 질문**
  - 이전 질문과 답변을 바탕으로 추가 질문을 이어갈 수 있습니다.
  - 단어와 문장의 의미를 단계적으로 확인할 수 있습니다.

- **선제 질문**
  - 설정에 따라 AI Tutor가 현재 영상과 관련된 학습 질문을 제안합니다.
  - 영상 시청 중 자연스럽게 복습을 진행할 수 있습니다.

- **답변 피드백**
  - AI Tutor 답변에 대한 피드백을 남길 수 있습니다.
  - 피드백을 통해 답변 품질을 평가할 수 있습니다.
  
<hr />

<p align="center">
  <img src="https://raw.githubusercontent.com/teach97/subsync-assets/main/7.gif" alt="SubSync 7번 기능 시연" width="740" />
</p>

### 설정 탭

학습 방식과 화면 환경에 맞춰 SubSync의 동작과 UI를 개인화합니다.


- **테마 설정**
  - 다크 테마, 화이트 테마, 글라스 테마를 선택할 수 있습니다.
  - 글라스 테마는 실시간 반응형 글래스 효과를 지원합니다

- **폰트 설정**
  - 기본 시스템 폰트와 지원되는 사용자 지정 폰트를 선택할 수 있습니다.

- **자막 설정**
  - 영·한 이중자막 표시 여부를 설정합니다.
  - 자막 표시 방식과 학습 화면 구성을 조정할 수 있습니다.

- **단어 조회 설정**
  - Mouse Hover 단어 조회 기능의 사용 여부를 설정합니다.
  - 자막과 Script에서 단어를 조회하는 방식을 개인화할 수 있습니다.

- **AI Tutor 설정**
  - 선제 질문 사용 여부를 설정합니다.
  - 영상 학습 중 AI Tutor의 동작 방식을 조정할 수 있습니다.

---

## 🤖 AI Tutor

SubSync의 핵심 AI 학습 기능입니다. 일반적인 챗봇이 아니라 **현재 보고 있는 YouTube 영상의 문맥을 활용하는 Tutor**를 목표로 합니다.

```
사용자 질문 + Video ID + 현재 재생 시점 + 영상 Script/Subtitle Context + 사용자 학습 정보
                              ↓
                          AI Tutor
                              ↓
                     영상 문맥 기반 답변
```

예를 들어 "여기서 speaker가 왜 이 표현을 사용한 거야?"라고 질문하면, 현재 영상의 자막과 재생 위치를 바탕으로 답변합니다.

**주요 기능**
- Gemini 기반 질의응답 (영상 자막·재생 시점 문맥 활용)
- Tutor 대화 이력 저장 및 응답 피드백 기록
- Tutor 답변 속 영어 단어도 Mouse Interaction으로 조회 가능
- 선제 질문(Proactive Question) — 영상 흐름에 맞춰 AI가 먼저 질문
- **LLM Provider Fallback** — Gemini ↔ Groq ↔ stub 순서로 장애·사용량 제한에 대응
- 자막 속 문장이 Tutor의 시스템 규칙을 바꾸지 못하도록 시스템 지시와 사용자 질문/자막을 구조적으로 분리하여 방어

---

## 🔄 서비스 이용 흐름

1. Chrome Extension 설치
2. YouTube 영상 접속 및 SubSync 활성화
3. 영·한 이중자막으로 영상 시청
4. 모르는 단어 Hover → Click → 저장
5. Video Tutor에게 영상 내용 질문
6. 학습 기록 서버 저장
7. Dashboard에서 데이터 분석

---

## 📊 대시보드
<img width="1114" height="851" alt="스크린샷 2026-09-10 223444" src="https://github.com/user-attachments/assets/3939fc96-7a75-4f9e-8408-dad6181dd649" />

SubSync는 Streamlit 기반 대시보드에서 서비스 운영 현황과 AI·API 사용량을 분석합니다. FastAPI Dashboard API로 데이터를 조회하고 화면별 기간·필터를 적용할 수 있습니다.

- 대시보드 홈: 기간별 사용자·AI 호출 수, 일별 AI 사용량, 최근 활동, 제공자별 호출 비중을 확인합니다.
- AI 사용량: 모델·사용자별 요청·토큰, 평균·P95 응답시간, 오류율, 제공자·일별 추이와 상세 내역을 확인합니다.
- API 호출: 엔드포인트·사용자별 요청·성공률·응답시간·오류와 최근 상태 코드를 확인하며, 429 발생 시 Rate Limit 안내를 표시합니다.
- 공통 기능: 화면별 조회 기간·필터, 데이터 연결 상태, API 상태와 마지막 스냅샷을 확인합니다.

[📊 Dashboard 바로가기](https://subsync-dashboard-5xicocfzxxf2lngqm4mj7s.streamlit.app)

---

## 🛠 기술 스택

**Frontend**
| 기술 | 용도 |
|---|---|
| Chrome Extension (Manifest V3) | YouTube 학습 UI |
| JavaScript / HTML / CSS | Extension 로직 및 UI |
| Chrome APIs | Extension 기능 및 인증 연동 |

**Backend**
| 기술 | 용도 |
|---|---|
| Python 3.11+ / FastAPI | REST API |
| Uvicorn | ASGI Server |
| Pydantic | API Schema |
| uv | 패키지 관리 |
| Pytest | 테스트 |

**AI**
| 기술 | 용도 |
|---|---|
| Google Gemini | Video Tutor |
| Groq | LLM Fallback |
| Prompt Engineering / Context Builder | 영상 기반 Tutor 응답 및 자막 문맥 구성 |

**Database / Auth**
| 기술 | 용도 |
|---|---|
| Supabase (PostgreSQL, Auth) | 데이터 저장 및 사용자 인증 |
| Google OAuth / JWT | 로그인 및 API 인증 |

**Cache / Dashboard / Deployment**
| 기술 | 용도 |
|---|---|
| Redis | 세션 및 단어 조회 캐시 |
| Streamlit + Pandas | 운영·분석 Dashboard |
| Render | Backend 배포 |
| Chrome Web Store | Extension 배포 |

---

## 🏗 시스템 아키텍처

```
┌───────────────────────────────────────────┐
│               User Browser                 │
│                YouTube Page                 │
│              Chrome Extension               │
│  ┌──────────────┬─────────┬──────────────┐ │
│  │Dual Subtitle │ Script  │ Video Tutor  │ │
│  └──────────────┴─────────┴──────────────┘ │
└──────────────────────┬──────────────────────┘
                        │ HTTPS REST API
                        ▼
┌───────────────────────────────────────────┐
│              FastAPI Backend               │
│   Auth / Dictionary / Words / Tutor / Logs  │
└───────┬──────────────┬──────────────┬───────┘
        ▼              ▼              ▼
  ┌──────────┐   ┌──────────┐  ┌──────────────┐
  │ Supabase │   │  Redis   │  │ Gemini/Groq  │
  │ Postgres │   │  Cache   │  │     LLM      │
  └────┬─────┘   └──────────┘  └──────────────┘
       ▼
┌────────────────────┐
│ Streamlit Dashboard │
│ User/AI/API Analytics │
└────────────────────┘
```

---


## 📦 프로젝트 구성

SubSync는 기능별로 3개의 Repository로 분리되어 있습니다.

```
SubSync
├── subsync-frontend   → Chrome Extension
├── subsync-backend    → FastAPI REST API
└── subsync-dashboard  → Streamlit Analytics Dashboard
```

| Repository | 설명 | 링크 |
|---|---|---|
| **subsync-frontend** | Chrome Manifest V3 기반 무빌드 확장 프로그램 | [바로가기](https://github.com/931njhthe-star/subsync-frontend) |
| **subsync-backend** | FastAPI 기반 REST API 서버 | [바로가기](https://github.com/931njhthe-star/subsync-backend) |
| **subsync-dashboard** | Streamlit 기반 운영·분석 대시보드 | [바로가기](https://github.com/931njhthe-star/subsync-dashboard) |

---

## ☁️ 배포 확인

Backend는 Render에 배포되어 있습니다.

```
GET https://subsync-backend-4bmh.onrender.com/health
GET https://subsync-backend-4bmh.onrender.com/api/v1/dictionary/hover?word=honest
```

> `/health`는 프로세스 상태만 확인하므로, 외부 사전·번역·LLM Provider의 정상 여부까지 보장하지는 않습니다.

Dashboard는 Streamlit Cloud, Frontend는 Chrome Web Store에 배포되어 있습니다.


- [Dashboard (Streamlit)](https://subsync-dashboard-5xicocfzxxf2lngqm4mj7s.streamlit.app)
- [Frontend (Chrome Extension)](https://chromewebstore.google.com/detail/subsync/akckibdjhdhehbfjellpgododmcpfphc?authuser=0&hl=ko)


> Render 서버가 15분동안 사용이 없을시 서버가 잠드므로, 데이터 안나올시 몇분뒤 새로고침 하시면 됩니다.


---


## 📚 관련 문서

- [Project Dashboard](https://yleeylee.notion.site/Subsync-2102b0d658a68394bc070175f52809d0)
---
