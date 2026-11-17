# Business Manager App
### Attendance, Fee Tracking and Appointment Booking for Small Businesses

> **Working name:** Business Manager App (change it later)
> **Status:** Planning phase
> **Document purpose:** Make the goal clear before building anything. This file explains WHAT we are building, WHY, for WHOM, and WITH WHICH TOOLS. It contains no code on purpose.

---

## Table of Contents

1. [Vision and Goal](#1-vision-and-goal)
2. [The Problem We Are Solving](#2-the-problem-we-are-solving)
3. [Who Will Use It](#3-who-will-use-it)
4. [What We Will Build (Scope)](#4-what-we-will-build-scope)
5. [Features in Detail](#5-features-in-detail)
6. [Key User Flows (Step by Step)](#6-key-user-flows-step-by-step)
7. [Payment Approach (Manual UPI)](#7-payment-approach-manual-upi)
8. [Notifications and Email](#8-notifications-and-email)
9. [Tech Stack and Why](#9-tech-stack-and-why)
10. [System Architecture](#10-system-architecture)
11. [Data Overview (What We Store)](#11-data-overview-what-we-store)
12. [Security and Data Separation](#12-security-and-data-separation)
13. [Free Tools Plan and Limits](#13-free-tools-plan-and-limits)
14. [Project Folder Plan](#14-project-folder-plan)
15. [Step-by-Step Build Roadmap](#15-step-by-step-build-roadmap)
16. [Business Model and Pricing Idea](#16-business-model-and-pricing-idea)
17. [Risks and How to Handle Them](#17-risks-and-how-to-handle-them)
18. [Success Metrics](#18-success-metrics)
19. [Future Features](#19-future-features)
20. [Final Checklist Before Coding](#20-final-checklist-before-coding)

---

## 1. Vision and Goal

### One-line vision
A simple, low-cost web app that helps small local businesses manage their **people, schedule and money** in one place.

### Main goal
Build a **multi-business (multi-tenant) application** that starts with **tuition centers** (attendance and fee tracking) and then adds **clinics, salons and gyms** (appointment booking), all inside **one application** and **one codebase**.

### Personal goals for this project
- Build a real product that can earn monthly income.
- Build everything using **free tools** at the start.
- Write our **own backend** (not only rely on a backend-as-a-service) so we learn and keep control.
- Keep the first version **small** and get **real paying users** before adding more.

### What "done" looks like for version 1 (MVP)
A tuition center owner can:
1. Sign up and create their center.
2. Add students and batches.
3. Mark daily attendance in under one minute.
4. Track which student has paid or not paid fees.
5. Send fee reminders and absent alerts to parents by email.
6. Record fee payments with manual UPI verification.

---

## 2. The Problem We Are Solving

Small businesses in India still run on paper registers, Excel sheets and WhatsApp messages. This causes real daily pain.

| Business | Current pain |
|---|---|
| **Tuition centers** | Attendance on paper. Owner forgets who paid. Chasing parents for fees is awkward and slow. |
| **Clinics** | Patients call to book. Double bookings. Many no-shows. |
| **Salons** | Bookings through calls and chats. Empty slots. No customer history. |
| **Gyms** | Membership expiry is forgotten. Fees are tracked by memory. |

### What these businesses lose
- **Time** (daily paperwork and calls)
- **Money** (unpaid fees, missed appointments)
- **Trust** (mistakes and confusion)

### What our app fixes
- Attendance and bookings become digital and fast.
- Fee status is always visible: who paid, who is pending.
- Automatic reminders reduce no-shows and late fees.
- Owners see simple reports instead of guessing.

> **Core idea:** People do not pay for apps. They pay to solve a problem that costs them time or money. Our product is **"never chase fees or lose a booking again."**

---

## 3. Who Will Use It

### User roles

| Role | Who they are | What they do in the app |
|---|---|---|
| **Platform Admin (you)** | The app creator | Approves subscription payments, manages all businesses, sees platform stats |
| **Business Owner** | Tuition center owner, clinic owner, salon owner | Full control of their own business data |
| **Staff / Teacher** | Employee of the business | Marks attendance, manages bookings (limited access) |
| **Customer / Parent / Student** | End user | Books an appointment, uploads fee payment proof, receives reminders |

### First target customer (start here)
**Small tuition centers** (20 to 150 students) in your own city.

**Why start here:**
- Easy to reach in person.
- Fee tracking is a clear, daily pain.
- The feature set is small and simple.
- Owners decide quickly (no big company approval).

---

## 4. What We Will Build (Scope)

### Two modules, one application

| Module | For | Priority |
|---|---|---|
| **Module A: Attendance and Fees** | Tuition centers (and gyms for fees) | **Build first** |
| **Module B: Appointment Booking** | Clinics, salons, gyms | **Build second** |

### Shared core (built once, used by both)
- Owner login and business profile
- People database (students or customers)
- Calendar and schedule
- Payments and receipts
- Reminders by email (SMS/WhatsApp later)
- Reports dashboard

### What is IN version 1 (MVP)
- Business signup and login
- Student, batch and fee setup
- Attendance marking
- Fee tracking and pending list
- Manual UPI payment proof upload and approval
- Email reminders and email alerts
- Basic reports
- Admin approval page for the platform owner

### What is NOT in version 1 (on purpose)
- Native mobile apps (we start with a mobile-friendly website)
- Online payment gateway (Razorpay and similar)
- WhatsApp Business API
- Multiple branches per business
- Advanced analytics
- Parent mobile login (maybe later)

> **Rule:** If a feature does not help us get the first 5 paying customers, it waits.

---

## 5. Features in Detail

### 5.1 Core Features (shared by both modules)

#### A. Authentication and Accounts
- Sign up with email and password (phone OTP later).
- Login and logout.
- Password reset by email.
- Each owner belongs to exactly one business.
- Roles: owner, staff.

#### B. Business Profile
- Business name, type (tuition center, clinic, salon, gym), address, phone.
- Business logo (optional).
- UPI ID and QR code for receiving payments from customers.
- Working days and working hours.
- Holiday list.

#### C. People Management (students or customers)
- Add, edit, delete and search people.
- Store name, phone, email, parent name, notes.
- Import many people at once from a spreadsheet (nice to have).
- Active and inactive status.

#### D. Dashboard
- Today's summary (absent students, appointments, pending payments).
- Money summary (collected this month, pending this month).
- Quick action buttons (Mark attendance, Add booking, Add payment).

#### E. Reports
- Monthly fee collection.
- Pending fee list.
- Attendance percentage per student.
- Download reports as PDF or spreadsheet (later).

#### F. Receipts
- Automatic fee receipt after a payment is approved.
- Receipt includes business name, student name, amount, date, month, receipt number.
- Receipt can be downloaded or emailed.

---

### 5.2 Module A: Attendance and Fees (Tuition Centers)

#### Batches / Classes
- Create batches (example: "Class 10 Maths, 5 PM").
- Set days and timings.
- Assign a teacher.
- Add students to one or more batches.
- Set the monthly fee per batch or per student.

#### Attendance
- Select a batch and date.
- Mark each student **Present** or **Absent** with one tap.
- "Mark all present" button for speed.
- Edit attendance for a past date (with limits).
- Attendance history per student.
- Monthly attendance report.

**Expectation:** Marking attendance for a full batch should take **under 30 seconds**.

#### Fee Management
- Set fee amount and due date per student.
- Fee status: **Paid, Pending, Overdue, Partially Paid**.
- Record a payment (manually by owner, or uploaded by parent).
- Discounts and late fees (simple version).
- Pending fee list sorted by due date.
- Payment history per student.

#### Reminders (Module A)
- **Fee pending reminder** to parent (before due date and after).
- **Absent alert** to parent ("Your child was absent today").
- **Fee received confirmation** with receipt.
- Owner can also press a "Send reminder now" button.

---

### 5.3 Module B: Appointment Booking (Clinic, Salon, Gym)

#### Services Setup
- Add services with name, duration and price (example: Haircut, 30 minutes, 300 rupees).
- Add staff or doctors and what services each one provides.

#### Booking Page for Customers
- A **shareable link** the owner puts on WhatsApp and Instagram.
- Customer picks a service, date and time slot.
- Customer enters name and phone number and confirms.
- No customer login needed (keeps it simple).
- Customer gets a confirmation email (if email given).

#### Calendar and Slots
- Time slots are created from working hours and service duration.
- **Double booking is prevented.**
- Block holidays, breaks and special days.
- Owner can add, cancel or reschedule bookings.

#### Customer Records
- Visit history per customer.
- Notes (example: allergies, preferences).
- No-show tracking.

#### Reminders (Module B)
- Booking confirmation.
- Reminder before the appointment (example: one day before).
- Cancellation or reschedule notice.

#### Memberships (Gym use)
- Plans such as monthly, quarterly and yearly.
- Start date, expiry date and renewal reminders.
- Uses the same fee system as Module A.

---

### 5.4 Platform Admin Features (for you)

- Dashboard of all businesses on the platform.
- **Pending subscription payments** list (screenshot, UTR, amount).
- Approve or reject payments with a reason.
- Duplicate UTR check.
- Activate, suspend or extend a business's subscription.
- Simple platform stats (number of businesses, active, expired).
- Audit log of every approval.

---

## 6. Key User Flows (Step by Step)

### Flow 1: New tuition center onboarding
1. Owner opens the website and signs up.
2. Owner enters business name, type and phone.
3. Owner sets UPI ID and uploads the QR code.
4. Owner creates the first batch.
5. Owner adds students (one by one or in bulk).
6. Owner sets fees.
7. Owner starts marking attendance.

### Flow 2: Daily attendance
1. Teacher opens the app on the phone.
2. Teacher selects today's batch.
3. All students are listed. Teacher marks Present or Absent.
4. Teacher taps Save.
5. Absent students' parents receive an email alert (if enabled).

### Flow 3: Monthly fee collection
1. System creates fee records for the month.
2. Parent receives a reminder with the amount and UPI details.
3. Parent pays through any UPI app.
4. Parent uploads a screenshot and enters the UTR (transaction ID).
5. Payment status becomes **Pending verification**.
6. Owner is notified by email.
7. Owner checks their own bank or UPI app.
8. Owner taps **Approve** or **Reject**.
9. On approval, status becomes **Paid** and a receipt is created.
10. Parent receives a confirmation email.

### Flow 4: Customer books an appointment
1. Customer opens the business's booking link.
2. Customer chooses a service and a free time slot.
3. Customer enters name and phone, then confirms.
4. Booking appears on the owner's calendar.
5. Customer gets a confirmation and later a reminder.

### Flow 5: Business pays for our app (subscription)
1. Business owner sees their plan and due date.
2. Owner pays our UPI ID.
3. Owner uploads a screenshot and enters the UTR.
4. We receive an email notification.
5. We check our own phone or bank app.
6. We approve in the admin page.
7. The business's subscription is extended.

---

## 7. Payment Approach (Manual UPI)

We start **without** a payment gateway, to keep it free and simple.

### Two separate payment cases (never mix them)

| Case | Who pays whom | Where the money goes |
|---|---|---|
| **A. Fee payment** | Parent pays the tuition center | Directly to the **center's own UPI** |
| **B. Subscription** | Business pays our app | To **our UPI** |

> We should **not** collect other people's fee money into our account. It avoids legal, tax and trust problems.

### The manual verification process
1. App shows the receiver's UPI ID or QR code with the amount and a reference.
2. Payer pays in any UPI app.
3. Payer enters the **UTR number** and uploads a **screenshot**.
4. Status = **Pending**.
5. The receiver is notified by email.
6. The receiver verifies in their **own bank or UPI app**.
7. The receiver approves or rejects (with a reason).
8. A receipt is created on approval.

### Safety rules
- **Never auto-approve** because a screenshot was uploaded.
- **Block duplicate UTR numbers.**
- Always verify the credit in the real bank app, not only the screenshot.
- Keep an **audit trail** (who approved, when).
- Store screenshots in **private storage**.
- Aim to verify within 24 hours and tell users this.

### Why manual first
- 100 percent free.
- No gateway paperwork.
- Great for the first 5 to 10 customers.
- We learn real payment behavior before automating.

### Future upgrade
When checking payments takes too much time, move to a payment gateway (Razorpay or Cashfree) with **automatic confirmation**. The data design should allow this later without rebuilding.

---

## 8. Notifications and Email

### Why email first
- It is **free** (permanent free plans exist).
- No telecom registration needed to start.
- Good enough for the MVP.

### Chosen provider
**Brevo** (free plan). It allows around 300 emails per day and includes SMS and WhatsApp options for later. Free emails may carry the provider's footer.

**Backup option:** Resend (cleaner emails, needs your own domain, lower daily limit).

> Free limits change. Always check the provider's pricing page before relying on numbers.

### Emails the system will send

| Email | Sent to | Purpose |
|---|---|---|
| New payment uploaded | **Platform admin (you)** | So you can check and approve |
| Payment approved or rejected | Customer or parent | Confirmation |
| Fee pending reminder | Parent | Reduce late fees |
| Absent today alert | Parent | Keep parents informed |
| Booking confirmation and reminder | Customer | Reduce no-shows |
| Welcome and password reset | Owner | Account basics |

### Rules for emails
- Respect daily limits (use a queue if needed).
- Add an opt-out option for reminder emails.
- Verify the sender email.
- Later use our own domain with proper email authentication so mails do not go to spam.

### Later: SMS and WhatsApp
- **SMS in India needs DLT registration** and approved message templates. Start this process early because it takes days.
- **WhatsApp Business API** needs approval and has per-message charges.
- Parents often prefer WhatsApp, so add it once there are paying users.
- Until then, an optional "Open WhatsApp with a ready message" button is a free trick.

---

## 9. Tech Stack and Why

### Summary table

| Part | Technology | Why we chose it |
|---|---|---|
| **Frontend** | Next.js (React + TypeScript) | One popular framework, mobile-friendly, many tutorials |
| **Styling** | Tailwind CSS and a component library | Fast, clean mobile screens |
| **Backend** | Node.js + TypeScript + Express | Same language as frontend, simple to learn |
| **ORM** | Prisma | Easy database access without messy queries |
| **Validation** | Zod | Checks incoming data is correct and safe |
| **Database** | PostgreSQL on Supabase | Linked data, good reports, free to start |
| **Login** | Supabase Auth (backend verifies the token) | Safer than writing login ourselves |
| **File storage** | Supabase Storage (private) | Payment screenshots and receipts |
| **Email** | Brevo (free plan) | Free, includes SMS later |
| **Scheduled jobs** | node-cron inside backend | Daily reminders |
| **Containers** | Docker | Same setup on laptop and server |
| **Frontend hosting** | Vercel (free plan) | Easy deploy from GitHub |
| **Backend hosting** | Render or Railway (free or low-cost plan) | Runs our Node server |
| **Code storage** | GitHub | Version control |

### Why PostgreSQL (and not MongoDB)
Our data is **connected**: business, students, batches, attendance, fees. PostgreSQL:
- Keeps links strict (no payment for a student who does not exist).
- Makes reports easy ("who has not paid this month").
- Handles money records reliably.

### Why our own backend (not only Supabase APIs)
- Full control of business rules.
- Better learning and portfolio value.
- Easier to add payments, jobs and custom logic.
- Supabase is used mainly as the **database, login and file storage**.

### Why a mobile-friendly website first
- No app store approval.
- Updates reach everyone instantly.
- One codebase.
- Owners just open a link.

### Docker: where it helps
- Run the database and backend the same way on any computer.
- Use **volumes** so local database data is not lost when containers are removed.
- Use **Docker Compose** with a YAML file to start everything with one command.
- Deploy the backend the same way it runs locally.

---

## 10. System Architecture

### Simple picture (in words)

1. The **user's phone browser** opens the **Next.js frontend** (hosted on Vercel).
2. The frontend sends requests to our **Node.js backend** (hosted on Render or Railway).
3. The backend reads and writes data in **Supabase PostgreSQL**.
4. The backend stores screenshots and receipts in **Supabase Storage**.
5. The backend sends emails through **Brevo**.
6. A **scheduled job** inside the backend sends reminders every day.

### Backend layers (clean structure)
- **Routes:** list of available endpoints.
- **Controllers:** handle each request.
- **Services:** business logic (fees, attendance, emails).
- **Middleware:** login check, role check, business separation check, error handling.
- **Jobs:** scheduled tasks like reminders.
- **Config:** environment settings.

### Why this structure
So adding Module B (booking) later does not break Module A.

### API areas (what the backend offers, described simply)
- Authentication and profile
- Business settings
- People (students and customers)
- Batches and attendance
- Fees and payments
- Payment proof upload and approval
- Services, slots and bookings
- Reports
- Platform admin tools

---

## 11. Data Overview (What We Store)

No technical code here. This is the plain-language list of what the database holds.

| Data | What it contains |
|---|---|
| **Businesses** | Name, type, address, phone, UPI details, subscription status |
| **Users** | Login details, role (owner, staff), which business they belong to |
| **People** | Students or customers: name, phone, email, parent contact |
| **Batches** | Class name, days, timing, teacher, fee |
| **Batch members** | Which student is in which batch |
| **Attendance** | Student, batch, date, present or absent |
| **Fee records** | Student, month, amount due, due date, status |
| **Payments** | Amount, method, UTR, screenshot, status, approved by, approved at |
| **Receipts** | Receipt number, linked payment, date |
| **Services** | Name, duration, price (Module B) |
| **Staff** | Name, services offered, working hours (Module B) |
| **Bookings** | Customer, service, staff, date, time, status (Module B) |
| **Subscriptions** | Plan, start date, end date, status for each business |
| **Notifications log** | What email was sent, to whom, when, success or failure |
| **Audit log** | Who did what and when (approvals, deletions) |

### The most important rule
**Every table that belongs to a business carries that business's ID.** This keeps one business's data separate from another's.

### Payment record design note
Each payment stores its **method** (manual UPI now, gateway later) and **status** (pending, approved, rejected). This makes future gateway support easy.

---

## 12. Security and Data Separation

### Must-have rules from day one
1. **Business separation:** every query is filtered by the logged-in user's business. The business ID comes from the login token, **never** from what the user sends.
2. **Role checks:** staff cannot do owner-only actions.
3. **Database rules (Row Level Security):** keep as a second safety layer.
4. **Secrets safe:** database URL, email key and other keys live in environment files, never in code or GitHub.
5. **Private files:** payment screenshots are not public. Access only by the right owner or admin.
6. **Input validation:** check all incoming data.
7. **Rate limiting:** prevent abuse of login and upload endpoints.
8. **HTTPS only** in production.
9. **Passwords:** handled by the login provider, never stored by us in plain text.
10. **Audit logs:** record approvals and sensitive actions.

### Privacy
- We store phone numbers, names and payment proofs of other people. Treat this data carefully.
- Show a simple privacy policy and terms.
- Allow data deletion on request.
- Do not share data with third parties except the email provider.

### Backups
- Free database plans may not include backups.
- Export important data regularly while on the free plan.
- Upgrade to a paid plan when real customer data is stored.

---

## 13. Free Tools Plan and Limits

Everything below can start at zero cost. **Limits change often, so verify before depending on them.**

| Need | Free choice | Things to watch |
|---|---|---|
| Database | Supabase free plan | About 500 MB storage; projects pause after about a week of no activity; no backups reported on free |
| Frontend hosting | Vercel free plan | Fine for an MVP |
| Backend hosting | Render or Railway free tier | Free servers may **sleep** when idle, which can delay or miss scheduled reminders |
| Email | Brevo free plan | Around 300 emails per day; provider footer on free emails |
| File storage | Supabase Storage free allowance | About 1 GB; compress screenshots |
| Code | GitHub free | Keep repository private |
| Domain | Skip at first | Costs a small yearly fee when added |

### When to start paying (in this order)
1. **Database** (to avoid pausing and to get backups) once real customers use it.
2. **Backend hosting** (so it never sleeps and reminders run reliably).
3. **Domain and email authentication** (so emails look professional).
4. **SMS or WhatsApp** when parents ask for it.
5. **Payment gateway** when manual checking takes too much time.

### Simple cost logic
If a paid database plan costs around 25 dollars per month, **5 customers paying 500 rupees per month** already come close to covering it. Check current exchange rates and prices.

---

## 14. Project Folder Plan

### Two separate projects

**frontend/** (the website)
- pages and screens
- reusable components
- API connection helpers
- styles and assets

**backend/** (the server)
- routes
- controllers
- services (business logic, email, payments)
- middleware (login, roles, business check, errors)
- jobs (reminders)
- config (environment and database)
- database schema folder
- Docker files
- environment example file (never the real one)

### Root of the repository
- this README file
- docs folder (notes, diagrams, decisions)
- Docker Compose file to run everything locally
- ignore file so secrets are never uploaded

---

## 15. Step-by-Step Build Roadmap

### Phase 0: Preparation (Week 0)
- [ ] Finish this README and agree on the goal.
- [ ] Talk to 5 tuition center owners. Ask what hurts and if they would pay.
- [ ] Create GitHub account and private repository.
- [ ] Create Supabase and Brevo free accounts.
- [ ] Sketch main screens on paper.
- [ ] Decide the app name.

### Phase 1: Foundation (Weeks 1 to 2)
- [ ] Set up the frontend and backend projects.
- [ ] Set up Docker for local development.
- [ ] Design and create database tables.
- [ ] Set up login and business signup.
- [ ] Build the business separation middleware.
- [ ] Turn on database security rules.

### Phase 2: Module A core (Weeks 3 to 5)
- [ ] Student management.
- [ ] Batch management.
- [ ] Attendance marking screen.
- [ ] Fee setup and fee status.
- [ ] Pending fee list.
- [ ] Basic dashboard.

### Phase 3: Payments and notifications (Weeks 6 to 7)
- [ ] Payment proof upload (UTR plus screenshot).
- [ ] Admin approval page.
- [ ] Duplicate UTR check.
- [ ] Email to admin when a payment is uploaded.
- [ ] Email to parent on approval or rejection.
- [ ] Receipt creation.

### Phase 4: Reminders (Week 8)
- [ ] Scheduled fee reminders.
- [ ] Absent alerts.
- [ ] Opt-out option.
- [ ] Test reminders on a sleeping free server and fix timing issues.

### Phase 5: Real-world testing (Weeks 9 to 10)
- [ ] Deploy to the internet.
- [ ] Give it free to 1 or 2 tuition centers.
- [ ] Watch how they use it. Fix confusing parts.
- [ ] Collect written feedback.

### Phase 6: First paying customers (Weeks 11 to 12)
- [ ] Add subscription tracking.
- [ ] Add the "business pays us" flow.
- [ ] Ask for payment from the first 5 centers.
- [ ] Upgrade the database plan when real data is stored.

### Phase 7: Module B (Month 4)
- [ ] Services and staff setup.
- [ ] Public booking page.
- [ ] Slot logic and double booking prevention.
- [ ] Booking reminders.
- [ ] Test with 1 salon and 1 clinic.

### Phase 8: Growth (Month 5 onward)
- [ ] Reports and PDF export.
- [ ] SMS and WhatsApp.
- [ ] Payment gateway.
- [ ] Parent login.
- [ ] Marketing and referrals.

---

## 16. Business Model and Pricing Idea

### How we earn
**Monthly subscription per business.**

### Starting price idea (to test, not final)

| Plan | Price per month | Includes |
|---|---|---|
| **Starter** | 299 to 499 rupees | Up to 50 students, attendance, fees, email reminders |
| **Standard** | 599 to 999 rupees | Up to 200 students, reports, receipts |
| **Booking add-on** | Extra | Appointment booking module |

### Pricing principles
- Offer a **free trial** (example: 14 or 30 days).
- Keep it simple: no hidden costs.
- Include a limit on reminders so message costs stay controlled later.
- Ask early customers what they would really pay before fixing prices.

### How to find customers
- Visit local tuition centers in person with a working demo.
- Show the pending fee list. That is the feature that sells.
- Use word of mouth between owners.
- Share demo videos on Instagram and YouTube.
- Offer a discount for the first 10 customers in exchange for feedback.

---

## 17. Risks and How to Handle Them

| Risk | Why it matters | How we handle it |
|---|---|---|
| Nobody wants to pay | Product may not fit | Talk to owners first, test with real users before building more |
| Building too much | Slow, never launches | Strict MVP scope, one module first |
| Data leak between businesses | Loses trust, legal risk | Business ID on everything, role checks, database security rules |
| Fake payment screenshots | Money loss | Never auto-approve, verify in real bank app, block duplicate UTR |
| Free server sleeps | Reminders missed | Test early, move to paid hosting when real customers join |
| Free database pauses or has no backup | Data loss or downtime | Regular data export, upgrade early |
| Emails go to spam | Reminders not seen | Verified sender, own domain later, short plain emails |
| SMS rules (DLT) delay | Cannot send SMS | Start with email, begin registration early |
| Handling other people's money | Legal and tax issues | Fee money goes straight to the center's UPI, not through us |
| Burnout working alone | Project stops | Small weekly goals, ship small |
| Free limits change | Plans break | Recheck pricing pages before decisions |

---

## 18. Success Metrics

### MVP is successful when
- [ ] 1 tuition center uses it **daily** for a full month.
- [ ] Attendance marking takes **under 30 seconds** per batch.
- [ ] At least **5 centers** agree to pay.
- [ ] Owners say fee tracking saves them time.
- [ ] No data leak between businesses in testing.

### Numbers to watch
- Number of businesses signed up
- Number of businesses active weekly
- Students and bookings managed
- Fees tracked per month
- Reminder emails delivered
- Payments verified per week and time taken to verify
- Monthly recurring income
- How many customers cancel

---

## 19. Future Features

**Near future**
- WhatsApp reminders through the official API
- SMS reminders after DLT registration
- Payment gateway with automatic confirmation
- PDF and spreadsheet report downloads
- Parent login to see attendance and fee status
- Progressive web app (install on phone home screen, push notifications)

**Later**
- Test marks and progress reports
- Homework sharing
- Multiple branches per business
- Multiple staff and doctors with separate calendars
- Online booking with advance payment
- Reviews and ratings
- Mobile apps for Android and iOS
- AI helper (example: summaries, smart reminders)
- Support for more business types (yoga, music, coaching)
- Multiple languages (Telugu, Hindi, English)

---

## 20. Final Checklist Before Coding

Answer these clearly. If any answer is "not sure", fix it first.

- [ ] **Who is my first customer?** (Tuition centers in my city.)
- [ ] **What is their biggest pain?** (Chasing fees and paper attendance.)
- [ ] **What is the smallest version I can sell?** (Attendance, fees, email reminders, manual UPI approval.)
- [ ] **Which tools am I using?** (Next.js, Node + Express, PostgreSQL on Supabase, Brevo, Docker.)
- [ ] **How will payments work at first?** (Manual UPI with UTR and screenshot, approved by hand.)
- [ ] **Where will I find my first 5 customers?** (Visiting local centers with a demo.)
- [ ] **What will I charge?** (Test 299 to 999 rupees per month.)
- [ ] **What will I NOT build yet?** (Gateway, WhatsApp API, native apps, branches.)
- [ ] **How will I protect customer data?** (Business ID rules, private files, secrets in environment files.)
- [ ] **What is my weekly target?** (Finish one small phase at a time.)

---

## Guiding Principles (Read When Confused)

1. **Solve one problem well** before solving many.
2. **Talk to real customers** before and during building.
3. **Keep the first version small.**
4. **Security and data separation are not optional.**
5. **Free tools first, pay only when real customers depend on it.**
6. **Never auto-approve money.**
7. **Ship, learn, improve.**

---

*This document is a living plan. Update it as you learn from real users. Prices, free limits and platform rules change often, so always confirm on each provider's official website before depending on them. This is a planning document, not legal or financial advice.*
