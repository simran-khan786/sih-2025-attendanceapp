# Smart Curriculum Attendance App - Product Requirements Document

**Problem Statement ID:** 25011  
**Department:** Department of Higher Education, Government of Punjab  
**Timeline:** 12 Days  
**Platform:** Web Application  
**Category:** Smart Education

---

## Project Information

### Project Title
Smart Curriculum Attendance App

### Short Description
A web-based attendance management system that uses face recognition technology to automate student attendance marking. Teachers trigger attendance capture from their registered devices, and results are displayed in real-time on classroom screens.

### Long Description

**Problem Statement:**  
Educational institutions in Punjab rely heavily on manual attendance systems that consume valuable instructional time and are prone to errors. Teachers spend 5-10 minutes per class on attendance marking, reducing effective teaching hours and creating opportunities for proxy attendance.

**Proposed Solution:**  
The Smart Curriculum Attendance App leverages face recognition technology to automate the entire attendance process. Teachers initiate attendance capture from their registered devices, and the system automatically identifies and marks students present using AI-powered facial recognition. The entire process takes less than 60 seconds.

**Key Differentiators:**
- Simultaneous capture of entire class
- Teacher-controlled device authentication
- Real-time transparency via classroom displays
- Privacy-first: face processing happens in browser
- No additional hardware required

**Expected Impact:**
- Save 30-45 minutes of instructional time per day per teacher
- Improve attendance accuracy to 98%+
- Eliminate proxy attendance
- Provide instant access to attendance analytics
- Generate comprehensive reports for administration

---

## Learning Objectives

### Primary Learning Outcomes
- Implement face recognition using TensorFlow.js and face-api.js
- Build secure device authentication systems
- Create real-time data synchronization using WebSockets
- Design accessible web interfaces (WCAG 2.1 AA)
- Implement secure camera access and image processing

### Secondary Learning Outcomes
- Build RESTful APIs with proper error handling
- Implement data visualization for analytics
- Apply modern state management patterns
- Deploy full-stack applications to cloud

---

## Technology Stack

### Frontend
- Build Tool: Vite 6.x
- Framework: React 19 with TypeScript 5
- Routing: React Router v7
- State Management: Zustand 5.x
- Styling: TailwindCSS v4 + DaisyUI v5.5
- Icons: Lucide React
- Face Recognition: face-api.js + TensorFlow.js
- Real-time: Socket.io-client
- Charts: Recharts

### Backend
- Runtime: Node.js v22 LTS
- Language: TypeScript 5
- Framework: Express.js v5
- Database: MongoDB with Mongoose v9
- Authentication: JWT + bcrypt
- Real-time: Socket.io
- File Storage: AWS S3 or Cloudinary
- Validation: Zod

---

## MVP Scope - 12 Day Timeline

### Phase 1: Core Authentication and Setup (Days 1-3)
**Priority: P0 (Must Have)**

**Features:**
1. User Authentication System
    - Login/logout for Students, Teachers, Administrators
    - Role-based access control (RBAC)
    - Password reset via email
    - JWT session management
    - Secure password storage with bcrypt

2. Device Registration for Teachers
    - Teachers register devices for attendance capture
    - Browser fingerprinting + manual admin approval
    - Device statuses: Pending, Approved, Rejected, Revoked
    - View all registered devices
    - Admin approval workflow

3. Basic Dashboard Setup
    - Student Dashboard: view attendance, upcoming classes
    - Teacher Dashboard: mark attendance, class schedules, devices
    - Admin Dashboard: system overview, approvals, analytics
    - Responsive navigation with role-based menus
    - User profile with logout

4. Database Schema Design
    - Users: id, name, email, password_hash, role, profile_photo
    - Devices: id, teacher_id, fingerprint, name, status
    - Classes: id, name, course_code, teacher_id, schedule
    - Students: id, user_id, roll_number, department, face_embeddings
    - Attendance: id, class_id, date, time, records, marked_by

---

### Phase 2: Face Recognition Core (Days 4-7)
**Priority: P0 (Must Have)**

**Features:**
1. Student Face Registration
    - Upload 3-5 clear photos from different angles
    - Client-side face detection validates quality
    - Generate face embeddings using face-api.js
    - Store embeddings in database
    - Update photos if recognition accuracy is low

2. Face Recognition Engine
    - Integrate face-api.js with TensorFlow.js
    - Load pre-trained models (SSD MobileNet v1)
    - Face detection, landmarks, and recognition
    - Confidence threshold: 0.6 (60%)
    - Handle multiple faces in single frame

3. Attendance Capture Workflow
    - Teacher selects class and initiates capture
    - Verify device is approved
    - Camera interface with live preview
    - Single click captures and processes all faces
    - Progress indicator shows status
    - Display results with matched students

4. Attendance Marking Logic
    - Compare detected embeddings with registered students
    - Mark Present if confidence exceeds threshold
    - Mark Absent if not detected or low confidence
    - Allow manual override by teacher
    - Store timestamp, device info, confidence scores
    - Generate session ID for each capture event

---

### Phase 3: Real-time Display and Reports (Days 8-10)
**Priority: P0 (Must Have)**

**Features:**
1. Classroom Display Mode
    - Large screen view for projectors/displays
    - Real-time attendance status showing:
        - Student photos in grid layout
        - Green border for Present
        - Red border for Absent
        - Names and roll numbers
    - Auto-refresh on updates
    - Full-screen mode support
    - QR code to join display session

2. WebSocket Real-time Sync
    - WebSocket connection between teacher device and display
    - Emit attendance updates as faces recognized
    - Display updates instantly without refresh
    - Handle connection drops with reconnection
    - Room-based channels per class session

3. Attendance History and Records
    - Students view personal attendance:
        - Daily calendar view
        - Percentage per subject
        - Monthly trends
    - Teachers view class attendance:
        - Select class and date range
        - View trends over time
        - Identify low attendance students
    - Sortable and filterable tables

4. Basic Reporting System
    - Generate reports by:
        - Date range (daily, weekly, monthly)
        - Class/subject
        - Individual student
        - Department-wide
    - Export to CSV format
    - Visual charts (line, bar charts)
    - Automated weekly email reports

---

### Phase 4: Polish and Testing (Days 11-12)
**Priority: P1 (Should Have)**

**Features:**
1. Admin Management
    - User management: add, edit, disable users
    - Class schedule management
    - Device approval workflow
    - System settings
    - View system logs and audit trail

2. Error Handling
    - Handle poor lighting conditions
    - Handle similar facial features
    - Handle unregistered students
    - Network error handling with retry
    - Camera permission denial handling

3. Performance Optimization
    - Lazy loading of TensorFlow.js models
    - Image compression before upload
    - Database query optimization with indexes
    - API response caching
    - WebSocket connection pooling

4. Testing and Bug Fixes
    - Unit tests for business logic
    - Integration tests for API endpoints
    - End-to-end testing of attendance workflow
    - Cross-browser testing
    - Mobile responsiveness testing
    - Fix critical bugs

---

## Target Users and Personas

### Primary Persona: Teacher (Faculty Member)

**Demographics:**
- Age: 28-55 years
- Location: Punjab, India
- Occupation: College/University Teacher
- Tech Savviness: Medium
- Device: Laptop or tablet with camera

**Goals and Motivations:**
- Save time on manual attendance marking
- Focus on teaching and student interaction
- Maintain accurate attendance records effortlessly
- Reduce disputes about attendance accuracy
- Access attendance data for performance reviews

**Pain Points:**
- Wastes 5-10 minutes every class on manual attendance
- Students attempt proxy attendance
- Difficult to track attendance patterns
- Paper records prone to loss
- Manual data entry is tedious

**User Needs:**
- Quick attendance marking (under 1 minute)
- Simple interface without technical complexity
- Ability to manually correct errors
- View attendance history
- Generate reports for administration

---

### Primary Persona: Student

**Demographics:**
- Age: 18-24 years
- Location: Punjab, India
- Occupation: College/University Student
- Tech Savviness: High
- Device: Smartphone or laptop

**Goals and Motivations:**
- Track own attendance easily
- Know attendance percentage per subject
- Avoid missing minimum requirements
- Ensure accurate marking
- Meet exam eligibility criteria

**Pain Points:**
- Unaware of attendance until late in semester
- Manual systems are slow and disruptive
- Disputes about being marked present
- No easy way to check history
- Proxy attendance causes issues

**User Needs:**
- View real-time attendance status
- Check percentage anytime
- Receive low attendance alerts
- Simple face registration
- Transparent attendance records

---

### Secondary Persona: Administrator

**Demographics:**
- Age: 35-60 years
- Location: Punjab, India
- Occupation: College Admin, HOD, Principal
- Tech Savviness: Medium to High
- Device: Desktop or laptop

**Goals and Motivations:**
- Maintain accurate institutional records
- Monitor attendance trends
- Generate compliance reports
- Identify at-risk students
- Ensure system security

**Pain Points:**
- Difficulty consolidating data
- Manual report generation is time-consuming
- No real-time visibility
- Hard to identify low-attendance students
- Managing teacher access

**User Needs:**
- Comprehensive analytics dashboard
- Approve device registration requests
- Generate reports by period/department
- Export data for government reporting
- Manage user accounts
- View system logs

---

## Branding and Visual Identity

### Brand Identity

**Brand Name:** SmartAttend  
**Tagline:** Intelligent Attendance, Effortless Management

**Brand Personality:**
- Tone: Professional yet approachable, modern, efficient
- Voice: Clear, helpful, educational, trustworthy
- Mood: Clean, organized, technology-forward, accessible

**Brand Values:**
- Efficiency: Saving time for education
- Accuracy: Precision with AI technology
- Transparency: Clear attendance records
- Accessibility: Simple for everyone
- Privacy: Protecting student data

---

### Color System (OKLCH)

**Primary Brand Color - Trust Blue**
```
--color-primary: oklch(55% 0.20 250)
--color-primary-content: oklch(98% 0.01 250)
```
- Usage: Primary CTAs, navigation, attendance Present indicators
- Meaning: Trust, professionalism, education, technology
- Contrast: 7.2:1 (AAA)

**Secondary Brand Color - Academic Purple**
```
--color-secondary: oklch(60% 0.18 290)
--color-secondary-content: oklch(98% 0.01 290)
```
- Usage: Secondary actions, admin features, charts
- Meaning: Wisdom, academic excellence, innovation
- Contrast: 5.8:1 (AA)

**Accent Color - Success Green**
```
--color-accent: oklch(65% 0.18 145)
--color-accent-content: oklch(20% 0.05 145)
```
- Usage: Success states, Present status, confirmations
- Meaning: Success, achievement, presence, completion
- Contrast: 5.2:1 (AA)

**Neutral Colors - Modern Gray**
```
--color-neutral: oklch(35% 0.02 250)
--color-neutral-content: oklch(95% 0.01 250)
```
- Usage: Text, borders, subtle UI elements, disabled states

**Base Colors (Backgrounds)**
```
--color-base-100: oklch(98% 0.01 250)  /* Main background */
--color-base-200: oklch(94% 0.02 250)  /* Cards */
--color-base-300: oklch(88% 0.03 250)  /* Borders */
--color-base-content: oklch(25% 0.015 250)  /* Text */
```

**Semantic Colors**
```
--color-info: oklch(65% 0.18 240)      /* Info messages */
--color-success: oklch(65% 0.18 145)   /* Success, Present */
--color-warning: oklch(75% 0.15 85)    /* Low attendance warnings */
--color-error: oklch(60% 0.22 25)      /* Errors, Absent status */
```

---

### Typography

**Primary Font (Headings) - Poppins**
- Weights: 500 (Medium), 600 (Semi-Bold), 700 (Bold)
- Usage: Titles, headings, navigation, buttons
- Modern, friendly, geometric, readable

**Secondary Font (Body) - Inter**
- Weights: 400 (Regular), 500 (Medium), 600 (Semi-Bold), 700 (Bold)
- Usage: Body text, labels, table data, descriptions
- Excellent screen readability, neutral, professional

**Typography Scale:**
- H1: 36px / 44px - Bold (Poppins)
- H2: 30px / 38px - Semi-Bold (Poppins)
- H3: 24px / 32px - Semi-Bold (Poppins)
- H4: 20px / 28px - Semi-Bold (Poppins)
- Body Regular: 16px / 24px - Regular (Inter)
- Button: 16px / 24px - Semi-Bold (Inter)
- Caption: 12px / 16px - Regular (Inter)

---

## Component Design System

### Component Organization

```
src/components/
├── atoms/              # Basic UI elements
│   ├── Button/
│   ├── Input/
│   ├── Badge/
│   ├── Avatar/
│   └── Icon/
├── molecules/          # Combinations
│   ├── FormField/
│   ├── Card/
│   ├── AttendanceCard/
│   └── SearchBar/
├── organisms/          # Complex sections
│   ├── Navbar/
│   ├── Footer/
│   ├── AttendanceGrid/
│   ├── DataTable/
│   └── ClassroomDisplay/
├── layouts/           # Page layouts
│   ├── MainLayout/
│   ├── DashboardLayout/
│   └── DisplayLayout/
└── pages/             # Route pages
    ├── Login/
    ├── StudentDashboard/
    ├── TeacherDashboard/
    └── AdminDashboard/
```

---

### Key Components

**Atom Components:**
- Button: Primary, secondary, outline, ghost variants
- Input: Text, email, password with validation states
- Badge: Status indicators (Present, Absent, Pending)
- Avatar: Student/teacher photos with fallbacks
- Icon: Lucide React icons with consistent sizing

**Molecule Components:**
- FormField: Label + Input + Error message
- AttendanceCard: Student card with photo, name, status
- SearchBar: Input with search icon and clear button
- DateRangePicker: Calendar-based date selection

**Organism Components:**
- Navbar: Logo, navigation, user menu, notifications
- AttendanceGrid: Grid of student attendance cards
- ClassroomDisplay: Full-screen real-time attendance view
- DataTable: Sortable table with pagination
- CameraCapture: Face recognition camera interface

---

## Page Wireframes

### 1. Login Page
**Route:** /login  
**Layout:** Centered authentication layout

**Sections:**
- Logo and app name
- Email input field
- Password input field
- Remember me checkbox
- Login button (primary)
- Forgot password link
- Background: Gradient with education imagery

---

### 2. Student Dashboard
**Route:** /student/dashboard  
**Layout:** Main layout with sidebar

**Sections:**
- Welcome header with student name
- Attendance summary cards:
    - Overall percentage
    - This week attendance
    - Low attendance subjects (warning)
- Quick stats: Total classes, Present, Absent
- Recent attendance list (last 10 classes)
- Calendar view with color-coded dates
- Navigation: Dashboard, Attendance History, Profile

---

### 3. Teacher Dashboard
**Route:** /teacher/dashboard  
**Layout:** Main layout with sidebar

**Sections:**
- Welcome header with teacher name
- Quick actions:
    - Mark Attendance (large primary button)
    - View Reports
    - Manage Devices
- Today's schedule with class list
- Recent attendance sessions
- Class-wise attendance statistics
- Navigation: Dashboard, Classes, Reports, Devices, Profile

---

### 4. Mark Attendance Page
**Route:** /teacher/mark-attendance  
**Layout:** Full-width layout

**Sections:**
- Class selection dropdown
- Device status indicator (approved/not approved)
- Camera preview area (large)
- Capture button (primary, centered)
- Instructions: Position students in frame
- Progress indicator during processing
- Results grid: detected students with confidence scores
- Manual override controls
- Submit attendance button

---

### 5. Classroom Display
**Route:** /display/:sessionId  
**Layout:** Full-screen, no chrome

**Sections:**
- Header: Class name, date, time
- Real-time attendance grid:
    - Student photos (4-6 columns)
    - Green border: Present
    - Red border/grayed: Absent
    - Names and roll numbers
- Attendance count: X/Y Present
- Auto-refresh indicator
- QR code in corner (to join session)

---

### 6. Admin Dashboard
**Route:** /admin/dashboard  
**Layout:** Admin layout with sidebar

**Sections:**
- Statistics cards:
    - Total students
    - Total teachers
    - Classes today
    - Average attendance
- Pending device approvals (action list)
- Recent activity feed
- Attendance trends chart (line chart)
- Low attendance alerts
- Quick links: Users, Classes, Reports, Settings
- Navigation: Dashboard, Users, Devices, Classes, Reports, Settings

---

## Responsive Design

**Breakpoints:**
- Mobile: < 768px - Single column, stacked layout
- Tablet: 768px - 1279px - 2-column layouts, collapsible sidebar
- Desktop: >= 1280px - Full multi-column, persistent sidebar

**Mobile Optimizations:**
- Hamburger menu
- Full-width buttons (min 44px height)
- Single column cards
- Simplified tables (vertical layout)
- Bottom navigation bar

**Tablet Optimizations:**
- 2-column grids
- Collapsible sidebar with overlay
- Touch-friendly spacing (8px minimum)
- Larger tap targets

---

## Accessibility Requirements

**WCAG 2.1 AA Compliance:**

**Perceivable:**
- All images have descriptive alt text
- Color contrast >= 4.5:1 for normal text
- Color contrast >= 3:1 for large text
- Color not sole indicator (icons + text)
- Text resizable to 200%

**Operable:**
- All functionality via keyboard
- No keyboard traps
- Visible focus indicators (2px outline)
- Skip navigation link
- Clear page titles
- Logical tab order

**Understandable:**
- Language declared (html lang="en")
- Consistent navigation
- Form labels and instructions
- Error identification with suggestions
- Clear, simple language

**Robust:**
- Valid HTML
- Proper ARIA usage (roles, states, properties)
- Name, role, value for all UI components
- Compatible with assistive technologies

---

## Security Considerations

**Authentication:**
- Secure password hashing with bcrypt (cost factor 12)
- JWT tokens with expiration (24 hours)
- HTTP-only cookies for token storage
- CSRF protection
- Rate limiting on login attempts

**Device Security:**
- Browser fingerprinting (Canvas, WebGL, Audio)
- Device approval workflow
- Ability to revoke device access
- Audit log of device usage

**Data Privacy:**
- Face embeddings stored encrypted
- HTTPS only in production
- No raw face images stored (only embeddings)
- GDPR/data protection compliance
- Student data access controls

**API Security:**
- Input validation with Zod
- SQL/NoSQL injection prevention
- XSS protection
- Rate limiting on endpoints
- CORS configuration

---

## Testing Strategy

**Unit Testing:**
- Test business logic functions
- Test utility functions
- Test API routes
- Target: 70% code coverage

**Integration Testing:**
- Test API endpoints with database
- Test authentication flow
- Test face recognition pipeline
- Test WebSocket connections

**End-to-End Testing:**
- Test complete attendance marking workflow
- Test user registration and login
- Test report generation
- Test across different browsers

**Manual Testing:**
- Test on actual devices (laptops, tablets)
- Test with real classroom conditions
- Test camera in different lighting
- Test with multiple faces
- Usability testing with teachers and students

---

## Deployment

**Frontend Deployment (Vercel):**
- Build command: npm run build
- Output directory: dist
- Environment variables: API_URL, SOCKET_URL
- Custom domain: smartattend.punjab.gov.in

**Backend Deployment (Railway/Render):**
- Node.js v22 runtime
- Environment variables: DATABASE_URL, JWT_SECRET, AWS_KEYS
- Health check endpoint: /api/health
- Auto-scaling based on load

**Database (MongoDB Atlas):**
- M10 cluster (dedicated)
- Automated backups
- Geographic redundancy
- Connection string as environment variable

---

## Success Metrics

**Key Performance Indicators:**
- Attendance marking time: < 60 seconds per class
- Face recognition accuracy: >= 95%
- System uptime: >= 99%
- Teacher adoption rate: >= 80% within 1 month
- Student satisfaction: >= 4/5 rating
- Time saved per teacher: 30+ minutes per day

**Analytics to Track:**
- Daily active users (teachers, students)
- Number of attendance sessions
- Average time per attendance capture
- Face recognition success rate
- Device approval turnaround time
- Report generation frequency

---

End of PRD Document