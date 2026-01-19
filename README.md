# 🩺 Doctor Appointment Booking AI Agent

An automated WhatsApp AI agent built on **n8n** that handles doctor appointments, payments, and patient reminders without human intervention.

## 📋 Prerequisites
In order to execute this workflow, you must connect the following accounts in n8n:
* **Google Sheets:** Required to read/write patient records and appointment logs.
* **Stripe Test Account:** Required to generate payment links and process refunds (Test Mode credentials).
* **WhatsApp Meta Developer Account:** Required to send and receive messages via the WhatsApp Business API.

## 🛠️ Tech Stack

| Component | Technology | Role |
| :--- | :--- | :--- |
| **Orchestrator** | **n8n** | Handles workflow logic, triggers, and API connectivity. |
| **AI Model** | **OpenAI (GPT-4o-mini)** | Powers the conversational agent and user intent recognition. |
| **Database** | **Google Sheets** | Stores patient records, appointment logs, and clinic configuration. |
| **Interface** | **WhatsApp Business API** | Primary user interface for chat, bookings, and notifications. |
| **Payments** | **Stripe API** | Manages payment links, transaction verification, and automatic refunds. |

## 🚀 Key Features

### 🤖 AI Agent Capabilities
* **Conversational Booking:** Natural language processing for booking, rescheduling, and cancelling appointments.
* **Contextual Memory:** Remembers conversation state (patient details, selected dates) for seamless multi-turn chats.
* **Smart Availability:** Automatically cross-references `working_hours` and blocked slots in Google Sheets to prevent double-booking.

### 📅 Workflow Automation
* **Patient Management:** Auto-detects existing patients by mobile number or registers new profiles on the fly.
* **Dynamic Scheduling:** Users can view and modify their own upcoming appointments directly in the chat.
* **Daily Reminders:** Automated trigger runs daily at 8:00 AM to send WhatsApp reminders for that day's appointments.

### 💳 Integrated Payments (Stripe)
* **Auto-Invoicing:** Generates and sends a Stripe payment link immediately when a user selects "Online Payment."
* **Payment Confirmation:** Listens for `payment_intent.succeeded` events to automatically mark appointments as "Confirmed."
* **Automated Refunds:** Triggered automatically if a paid appointment is cancelled by the user.
