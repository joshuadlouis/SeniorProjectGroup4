# AgentB - Architecture Diagram

## Project Overview
AgentB is an AI-powered adaptive learning platform built with React, TypeScript, and Supabase. It provides personalized learning experiences, campus resources, and adaptive study tools tailored to individual learning styles.

---

## High-Level System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                     CLIENT LAYER (Browser)                       │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │         React + TypeScript + Vite                          │  │
│  │  ┌──────────────────────────────────────────────────────┐  │  │
│  │  │            App Router (React Router)                │  │  │
│  │  │  ├─ / (Index - Landing/Dashboard)                  │  │  │
│  │  │  ├─ /auth (Authentication)                         │  │  │
│  │  │  ├─ /calendar (Calendar Management)                │  │  │
│  │  │  └─ /profile (User Profile & Settings)             │  │  │
│  │  └──────────────────────────────────────────────────────┘  │  │
│  │                          ↕                                  │  │
│  │  ┌──────────────────────────────────────────────────────┐  │  │
│  │  │         Component Layer (UI Components)             │  │  │
│  │  │  ┌─ Dashboard (Main Learning Interface)            │  │  │
│  │  │  ├─ Hero (Landing Page)                           │  │  │
│  │  │  ├─ ChatInterface (AI Chat Support)               │  │  │
│  │  │  ├─ LearningStyleQuiz (Adaptive Assessment)       │  │  │
│  │  │  ├─ PlacementQuiz (Knowledge Evaluation)          │  │  │
│  │  │  ├─ MiniQuiz (Quick Assessments)                  │  │  │
│  │  │  ├─ StudyPlan (AI-Generated Study Plans)          │  │  │
│  │  │  ├─ InteractiveExercise (Practice Problems)       │  │  │
│  │  │  ├─ SyllabusUpload (Course Material Upload)       │  │  │
│  │  │  ├─ AssignmentUpload (Assignment Management)      │  │  │
│  │  │  ├─ TestReminders (Exam Notifications)            │  │  │
│  │  │  ├─ PracticeHistory (Learning Analytics)          │  │  │
│  │  │  └─ ui/* (shadcn-ui Component Library)           │  │  │
│  │  └──────────────────────────────────────────────────────┘  │  │
│  │                          ↕                                  │  │
│  │  ┌──────────────────────────────────────────────────────┐  │  │
│  │  │         Custom Hooks & State Management             │  │  │
│  │  │  ├─ useProfile (User Profile Logic)               │  │  │
│  │  │  ├─ useStudyPlan (Study Plan Generation)          │  │  │
│  │  │  ├─ useAgentBChat (AI Chat Integration)           │  │  │
│  │  │  ├─ use-toast (Notification System)               │  │  │
│  │  │  └─ use-mobile (Responsive Design Detection)      │  │  │
│  │  └──────────────────────────────────────────────────────┘  │  │
│  │                          ↕                                  │  │
│  │  ┌──────────────────────────────────────────────────────┐  │  │
│  │  │    Styling & Configuration                          │  │  │
│  │  │  ├─ Tailwind CSS (Utility-First Styling)          │  │  │
│  │  │  ├─ PostCSS (CSS Processing)                      │  │  │
│  │  │  └─ App.css & index.css (Global Styles)           │  │  │
│  │  └──────────────────────────────────────────────────────┘  │  │
│  └────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
                              ↓ HTTP/REST
┌─────────────────────────────────────────────────────────────────┐
│              API LAYER & DATA MANAGEMENT                         │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │    Supabase Integration                                    │  │
│  │  ├─ PostgreSQL Database                                  │  │
│  │  │  ├─ Users Table (Authentication & Profiles)          │  │
│  │  │  ├─ Classes Table (Course Information)               │  │
│  │  │  ├─ Syllabi Table (Course Materials)                 │  │
│  │  │  ├─ Assignments Table (Assignment Tracking)          │  │
│  │  │  ├─ Quiz Results Table (Assessment Scores)           │  │
│  │  │  ├─ Learning Resources Table (Content Library)       │  │
│  │  │  ├─ Study Plans Table (AI-Generated Plans)           │  │
│  │  │  ├─ Calendar Events Table (Exam Schedule)            │  │
│  │  │  └─ Chat History Table (Conversation Logs)           │  │
│  │  │                                                        │  │
│  │  ├─ Authentication (Supabase Auth)                       │  │
│  │  │  ├─ Email/Password Authentication                   │  │
│  │  │  ├─ Session Management                              │  │
│  │  │  └─ Row-Level Security (RLS)                        │  │
│  │  │                                                        │  │
│  │  ├─ Storage (Supabase Storage)                          │  │
│  │  │  ├─ Syllabus File Storage                           │  │
│  │  │  ├─ Assignment Submissions                          │  │
│  │  │  └─ User Generated Content                          │  │
│  │  │                                                        │  │
│  │  └─ Edge Functions (Supabase Functions)                 │  │
│  │     ├─ agent-b-chat (AI Chat Endpoint)                │  │
│  │     └─ Query Processing & AI Integration               │  │
│  │                                                        │  │
│  └────────────────────────────────────────────────────────────┘  │
│                                                                   │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │    React Query (@tanstack/react-query)                    │  │
│  │  ├─ Request Caching & Synchronization                   │  │
│  │  ├─ Background Refetching                               │  │
│  │  └─ Optimistic Updates                                  │  │
│  └────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
                              ↓ HTTP/REST
┌─────────────────────────────────────────────────────────────────┐
│           EXTERNAL SERVICES & AI INTEGRATION                     │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │    AI/ML Services (Lovable Platform)                       │  │
│  │  ├─ Adaptive Learning Algorithm                          │  │
│  │  ├─ AI Chat Generation (Agent B Chat)                   │  │
│  │  ├─ Study Plan Generation                               │  │
│  │  ├─ Quiz Question Generation                            │  │
│  │  └─ Learning Resource Recommendations                   │  │
│  │                                                           │  │
│  └────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Component Architecture

### Page Components
```
┌─ Index.tsx (Landing & Main Dashboard)
│  ├─ Hero Component
│  ├─ Dashboard Component
│  └─ Navigation
│
├─ Auth.tsx (Authentication Page)
│  ├─ Login Form
│  ├─ Register Form
│  └─ Password Reset
│
├─ Profile.tsx (User Profile Management)
│  ├─ Profile Information Form
│  ├─ Class Management
│  ├─ Syllabus Display
│  ├─ Learning Resources
│  └─ User Settings
│
└─ CalendarPage.tsx (Event & Exam Management)
   ├─ Calendar View
   ├─ Event Creation
   └─ Event Details
```

### Feature Components
```
┌─ Dashboard.tsx
│  ├─ User Welcome Section
│  ├─ Quick Actions
│  ├─ Study Progress Overview
│  └─ Recommended Content
│
├─ ChatInterface.tsx
│  ├─ Message Display
│  ├─ Input Field
│  ├─ AI Response Handler
│  └─ Message History
│
├─ LearningStyleQuiz.tsx
│  ├─ Quiz Questions
│  ├─ Answer Tracking
│  ├─ Learning Style Analysis
│  └─ Recommendation Engine
│
├─ PlacementQuiz.tsx
│  ├─ Assessment Questions
│  ├─ Progress Tracking
│  ├─ Score Calculation
│  └─ Weak Area Identification
│
├─ MiniQuiz.tsx
│  ├─ Quick Quiz Interface
│  ├─ Instant Feedback
│  └─ Score Recording
│
├─ StudyPlan.tsx
│  ├─ AI-Generated Plan Display
│  ├─ Learning Objectives
│  ├─ Resource Recommendations
│  └─ Progress Tracking
│
├─ InteractiveExercise.tsx
│  ├─ Problem Display
│  ├─ Solution Submission
│  └─ Feedback Generation
│
├─ SyllabusUpload.tsx
│  ├─ File Upload Interface
│  ├─ Course Information Entry
│  └─ Content Processing
│
├─ AssignmentUpload.tsx
│  ├─ Assignment Management
│  ├─ Submission Tracking
│  └─ Due Date Management
│
├─ TestReminders.tsx
│  ├─ Exam Schedule
│  ├─ Notification System
│  └─ Time Management
│
└─ PracticeHistory.tsx
   ├─ Performance Analytics
   ├─ Progress Charts
   └─ Historical Data
```

---

## Data Flow Architecture

### Authentication Flow
```
User Login/Register
    ↓
[Auth.tsx] Component
    ↓
useProfile Hook → Supabase Auth
    ↓
JWT Token Management
    ↓
Session Storage
    ↓
Protected Routes Accessed
```

### Learning Content Flow
```
User Uploads Syllabus
    ↓
[SyllabusUpload.tsx]
    ↓
Supabase Storage (File)
    ↓
Supabase Database (Metadata)
    ↓
AI Processing (Agent B)
    ↓
Extract Learning Objectives
    ↓
Generate Study Plan
    ↓
[StudyPlan.tsx] Display
```

### Quiz & Assessment Flow
```
User Starts Quiz
    ↓
[PlacementQuiz.tsx] / [MiniQuiz.tsx]
    ↓
Question Fetched from Database
    ↓
User Answers Submitted
    ↓
Answer Processing & Scoring
    ↓
Results Stored in Database
    ↓
[PracticeHistory.tsx] Analytics Updated
    ↓
Learning Style & Weak Areas Identified
    ↓
[StudyPlan.tsx] Recommendations Updated
```

### AI Chat Flow
```
User Message Input
    ↓
[ChatInterface.tsx]
    ↓
Message Stored & Sent to Backend
    ↓
Supabase Edge Function (agent-b-chat)
    ↓
useAgentBChat Hook
    ↓
AI Processing & Response Generation
    ↓
Response Returned to Frontend
    ↓
[ChatInterface.tsx] Display Message
    ↓
Chat History Updated in Database
```

---

## State Management & Custom Hooks

### useProfile Hook
- **Purpose**: Manage user profile data and authentication state
- **State**: User profile, classes, learning style
- **Operations**: Fetch profile, update profile, manage classes

### useStudyPlan Hook
- **Purpose**: Handle study plan generation and retrieval
- **State**: Study plan data, learning objectives, resources
- **Operations**: Generate plan, fetch plan, update progress

### useAgentBChat Hook
- **Purpose**: Integrate with AI chat backend
- **State**: Chat messages, loading state, error handling
- **Operations**: Send message, fetch history, clear chat

### use-toast Hook
- **Purpose**: Display notifications and alerts
- **State**: Toast queue, duration
- **Operations**: Show toast, dismiss toast

### use-mobile Hook
- **Purpose**: Detect mobile viewport and adjust UI
- **State**: Is mobile flag
- **Operations**: Check screen size, listen to resize

---

## Technology Stack

### Frontend
- **Framework**: React 18+ with TypeScript
- **Build Tool**: Vite (Fast module bundler)
- **UI Library**: shadcn-ui (Accessible component library)
- **Styling**: Tailwind CSS (Utility-first CSS)
- **CSS Processing**: PostCSS
- **Routing**: React Router v6
- **State Management**: React Hooks + React Context
- **Data Fetching**: React Query (@tanstack/react-query)
- **Form Handling**: react-hook-form
- **Validation**: @hookform/resolvers (Zod, Yup, etc.)

### Backend & Database
- **Backend-as-a-Service**: Supabase
- **Database**: PostgreSQL
- **Authentication**: Supabase Auth (JWT-based)
- **File Storage**: Supabase Storage
- **Serverless Functions**: Supabase Edge Functions
- **APIs**: RESTful (via @supabase/supabase-js)

### UI Components & Icons
- **Component Library**: shadcn/ui built on Radix UI
- **Radix UI Primitives**: 
  - Alert Dialog, Accordion, Aspect Ratio, Avatar
  - Checkbox, Collapsible, Context Menu, Dialog
  - Dropdown Menu, Hover Card, Label, Menubar
  - Navigation Menu, Popover, Progress, Radio Group
  - Scroll Area, Select, Separator, Slider, Switch
  - Tabs, Toggle, Toggle Group, Tooltip
- **Icons**: Lucide React
- **Input**: input-otp (for OTP fields)
- **Carousel**: embla-carousel-react

### Development Tools
- **Linting**: ESLint with TypeScript support
- **Package Manager**: Bun (Fast JavaScript runtime & package manager)
- **TypeScript**: Full type safety

---

## Database Schema Overview

### Users Table
```
- id (UUID, PK)
- email (String, UK)
- full_name (String)
- university_id (String)
- learning_style (Enum: visual, auditory, kinesthetic, reading)
- created_at (Timestamp)
- updated_at (Timestamp)
```

### Classes Table
```
- id (UUID, PK)
- user_id (UUID, FK)
- class_name (String)
- professor (String)
- semester (String)
- year (Integer)
- created_at (Timestamp)
```

### Syllabi Table
```
- id (UUID, PK)
- user_id (UUID, FK)
- class_name (String)
- file_name (String)
- file_path (String)
- file_size (Integer)
- uploaded_at (Timestamp)
```

### Quiz Results Table
```
- id (UUID, PK)
- user_id (UUID, FK)
- quiz_type (Enum: placement, mini, practice)
- score (Number)
- total_questions (Integer)
- weak_areas (JSON Array)
- created_at (Timestamp)
```

### Study Plans Table
```
- id (UUID, PK)
- user_id (UUID, FK)
- class_id (UUID, FK)
- learning_objectives (JSON Array)
- resources (JSON Array)
- timeline (JSON)
- created_at (Timestamp)
- updated_at (Timestamp)
```

### Calendar Events Table
```
- id (UUID, PK)
- user_id (UUID, FK)
- title (String)
- event_date (Date)
- event_type (Enum: exam, assignment, lecture, other)
- description (Text)
- start_time (Time)
- created_at (Timestamp)
```

### Chat History Table
```
- id (UUID, PK)
- user_id (UUID, FK)
- message (Text)
- response (Text)
- topic (String)
- created_at (Timestamp)
```

### Learning Resources Table
```
- id (UUID, PK)
- user_id (UUID, FK)
- title (String)
- resource_type (Enum: written_explanation, real_world_example, diagram, pre_quiz, video, article)
- content (Text)
- subject (String)
- difficulty_level (Enum: beginner, intermediate, advanced)
- created_at (Timestamp)
```

---

## Key Features & Their Architecture

### 1. Adaptive Learning System
```
Learning Style Quiz → Profile Analysis → 
AI Recommends Learning Resources → Study Plan Generation →
Mini Quizzes for Weak Areas → Dynamic Content Adjustment
```

### 2. AI-Powered Chat Assistant
```
User Query Input → Edge Function Processing → 
AI Model Response → Response Formatting →
Context-Aware Suggestions → Message Persistence
```

### 3. Syllabus-Based Learning
```
Upload Syllabus → Extract Content →
AI Analysis of Key Topics → Learning Objectives Generation →
Resource Recommendations → Study Plan Creation
```

### 4. Assessment & Progress Tracking
```
Placement Quiz → Skill Evaluation →
Mini Quizzes → Weak Area Identification →
Study Plan Adaptation → Practice History Analytics
```

### 5. Calendar & Deadline Management
```
Manual Event Creation / Import →
Deadline Tracking → Reminder Notifications →
Calendar Integration → Study Plan Synchronization
```

---

## Deployment Architecture

```
Development
    ↓
[Git Repository] (GitHub)
    ↓
Lovable Platform CI/CD
    ↓
Build Process (Vite)
    ↓
Production Build Artifacts
    ↓
Supabase Hosting / Custom Domain
    ↓
Live Application
    ↓
Analytics & Monitoring
```

---

## Security Measures

1. **Authentication**: Supabase Auth with JWT tokens
2. **Database Security**: Row-Level Security (RLS) policies
3. **File Security**: Signed URLs for file access
4. **API Security**: Environment variables for sensitive data
5. **Type Safety**: TypeScript prevents runtime errors
6. **Input Validation**: React Hook Form with custom validators
7. **CORS**: Configured through Supabase

---

## Performance Optimizations

1. **Code Splitting**: Vite automatic route-based code splitting
2. **Caching**: React Query with intelligent cache invalidation
3. **Lazy Loading**: Dynamic component imports
4. **Image Optimization**: Proper sizing and formats
5. **CSS Minification**: Tailwind CSS purging
6. **Database Indexing**: Supabase optimized queries
7. **Edge Functions**: Serverless execution for scalability

---

## Future Enhancements

1. **Mobile Native Apps**: React Native implementation
2. **Advanced Analytics**: Detailed learning analytics dashboard
3. **Gamification**: Points, badges, leaderboards
4. **Collaborative Learning**: Peer study groups
5. **Integration with LMS**: Canvas, Blackboard compatibility
6. **Offline Support**: Service Workers & PWA
7. **Advanced AI Features**: Personalized tutoring, code review
8. **Video Integration**: Video lectures & tutorials
