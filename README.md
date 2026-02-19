# 🏡 Real Estate Voice Agent

**Autonomous Lead Research · Personalized Voice Outreach · Calendar-Validated Booking**

An end-to-end outbound voice system that researches real estate agents, dynamically personalizes conversation context, places outbound calls, validates availability through booking APIs (Cal.com), and confirms appointments via SMS and Google Calendar.

Built using Make.com workflows, VAPI, Twilio, Cal.com webhooks, and enrichment APIs.

---

## 🚀 System Architecture

The system runs on **two coordinated Make.com workflows**, separating enrichment/orchestration from post-call validation and booking logic.

---

## Workflow 1 — Lead Enrichment & Call Orchestration

**Objective:** Prepare a fully personalized outbound call.

### 1. Lead Intake
- Imports PhantomBuster LinkedIn exports via Google Sheets  
- Extracts:
  - Name  
  - Niche  
  - Company  
  - Location  

### 2. Research Enrichment
Uses Perplexity API to gather:
- Agent background  
- Niche positioning  
- Company summary  

Attempts to locate the official company website.

### 3. Conditional Website Scraping
If a website is found:
- Scrapes homepage content  
- Extracts tone, positioning, differentiators  
- Identifies service offerings  
- Checks available social profiles  

### 4. Dynamic Prompt Injection
Updates the VAPI assistant with:
- Agent-specific introduction  
- Niche-aware context  
- Company positioning hooks  
- Objection anticipation logic  

Each call receives a dynamically constructed system prompt.

### 5. Outbound Call Trigger
- Queues outbound call via VAPI API  
- Passes enriched metadata payload  
- Initiates personalized voice interaction  

---

## Workflow 2 — Call Analysis, Availability Validation & Booking Automation

**Objective:** Verify availability before confirming an appointment.

### 1. Call Completion Webhook
- VAPI sends transcript + metadata via GET request  
- Workflow triggered automatically  

### 2. Conversation Parsing
Router analyzes:
- Did the prospect agree to a meeting?  
- What date/time was requested?  
- Does confidence threshold meet booking criteria?  

### 3. Availability Validation (Cal.com / Booking API)

Before confirming any booking:

- Sends webhook/API request to Cal.com (or equivalent scheduler)  
- Checks:
  - Is requested time slot available?  
  - Does it conflict with existing bookings?  

No booking is confirmed without validation.

### 4. Conditional Routing

If time is available:
- Create confirmed booking in Cal.com  
- Send Google Calendar invite  
- Send Twilio confirmation SMS  
- Log success  

If time is unavailable:
- Trigger alternative slot suggestion (optional enhancement)  
- Initiate follow-up logic  

### 5. CRM / Tracking Update
- Update lead status in Sheet or CRM  
- Store transcript  
- Record booking outcome  

---

## 🧠 Key System Capabilities

- Dynamic GPT prompt generation per lead  
- Conditional website + social scraping  
- Context-aware outbound calling  
- Transcript-based appointment detection  
- API-based availability validation before booking  
- Automated SMS confirmation  
- Google Calendar integration  
- Fully orchestrated workflow automation  
- Scalable outbound infrastructure  

---

## 🛠 Tech Stack

- **Make.com** — Workflow orchestration  
- **VAPI** — Voice AI + outbound calling  
- **Perplexity API** — Research enrichment  
- **PhantomBuster** — LinkedIn lead scraping  
- **Cal.com API** — Availability validation  
- **Twilio** — SMS confirmations  
- **Google Calendar API** — Booking sync  
- **Google Sheets** — Lead tracking

---

## 📌 Why This Project Matters

This project demonstrates:

- API orchestration across multiple services  
- Conditional workflow routing  
- Dynamic system prompt engineering  
- Voice infrastructure integration  
- Transcript parsing and decision automation  
- Real-world booking validation logic  

It reflects applied automation engineering and production-style workflow design.
