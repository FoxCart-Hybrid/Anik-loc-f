Patrol Tracking System (PWA)

Overview

The Patrol Tracking System is a web-based Progressive Web Application (PWA) designed to support patrol operations through authenticated access, device authorization, and near real-time location tracking.
It provides centralized command visibility without requiring native Android or iOS applications.

The system is suitable for pilot deployment, training environments, and operational prototyping, with scope for further security hardening.

Key Capabilities
	•	Secure user authentication using Supabase Auth
	•	Patrol device authorization through HQ approval and confirmation code
	•	Near real-time GPS-based patrol tracking
	•	Patrol lifecycle management (start, pause, end)
	•	Centralized data storage and audit logging
	•	Installable PWA (runs on mobile, tablet, desktop)
	•	Zero-cost deployment supported (Vercel + Supabase free tiers)

System Architecture
	•	Frontend: Next.js (React) Progressive Web App
	•	Backend Services: Supabase (PostgreSQL, Auth, Edge Functions)
	•	Messaging Layer: MQTT-based pub/sub (configurable)
	•	Hosting: Vercel (Free Tier)
	•	Security: Environment-based secrets, HTTPS, session-based authentication

Authorization Model (Current Implementation)
	1.	HQ Access
	•	Any authenticated Supabase user can access HQ Control
	•	Role-based restrictions are not yet enforced
	2.	Patrol Device Authorization
	•	Patrol device submits authorization request
	•	HQ approves or rejects the request
	•	Approved device confirms using a generated confirmation code
	•	Authorized devices can initiate patrol activities

Note: Multi-level authorization (Platoon/Company/Battalion/HQ) is not yet implemented.

Deployment (Free / No VPS)

Requirements
	•	GitHub account
	•	Supabase (Free Tier)
	•	Vercel (Free Tier)

Environment Variables

Create the following variables in Vercel:

NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
NEXT_PUBLIC_SITE_URL=

Optional:

NEXT_PUBLIC_MQTT_BROKER_URL=
RESEND_API_KEY=
ADMIN_EMAIL=

Deploy Steps (Summary)
	1.	Upload this repository to GitHub
	2.	Create a Supabase project and obtain API keys
	3.	Import the repository into Vercel
	4.	Add environment variables
	5.	Deploy
	6.	Configure Supabase Auth redirect URLs

Database & Functions
	•	Database schema is defined in supabase/migrations
	•	Email authorization handled via Supabase Edge Function:
	•	send-authorization-email

Security Notes
	•	MQTT broker is public by default (not hardened)
	•	Device fingerprinting is non-cryptographic
	•	RLS policies must be tightened for production use

This system should not be considered hardened or classified without further security controls.

Future Enhancements
	•	Role-based authorization (Pl / Coy / Bn / HQ)
	•	Secure private MQTT or Supabase Realtime
	•	Enforced Row-Level Security (RLS)
	•	Map-based command dashboard
	•	Offline-first patrol caching

License

This project is intended for educational, pilot, and controlled operational use.
Further distribution or operational deployment should follow organizational security policy.
