# Republic of Türkiye - Electronic Visa Application System

## Overview

This is a full-stack e-Visa application system for Turkey built with a React frontend and Express backend. The application allows users to submit visa applications, make payments via Stripe, and track their application status. It includes an admin interface for managing applications.

Key features:
- Multi-step visa application form with document uploads
- Stripe payment integration for application fees
- Application status tracking via reference numbers
- Admin dashboard for application management
- Object storage for document uploads via Google Cloud Storage

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight React router)
- **State Management**: TanStack React Query for server state
- **Styling**: Tailwind CSS with shadcn/ui component library (New York style)
- **Forms**: React Hook Form with Zod validation
- **Animations**: Framer Motion for page transitions

The frontend is a single-page application with pages for:
- Home (landing page)
- Apply (multi-step application form)
- Payment (Stripe checkout)
- Payment Success (confirmation)
- Status (application lookup)
- FAQ (frequently asked questions)
- Admin (application management dashboard)

### Backend Architecture
- **Runtime**: Node.js with Express
- **Language**: TypeScript compiled via tsx/esbuild
- **API Style**: RESTful JSON APIs under `/api/*`

The server handles:
- Application CRUD operations
- Stripe payment intent creation and webhook processing
- Object storage signed URL generation for uploads
- Static file serving in production

### Data Storage
- **Database**: PostgreSQL via Drizzle ORM
- **Schema Location**: `shared/schema.ts` (shared between frontend and backend)
- **Migrations**: Drizzle Kit with push command (`npm run db:push`)

Main tables:
- `users`: Admin user accounts
- `applications`: Visa application records with personal details, passport info, and payment status
- `adminSettings`: System configuration

### File Uploads
- **Service**: Google Cloud Storage via Replit's Object Storage integration
- **Pattern**: Server generates signed upload URLs, client uploads directly to GCS
- **Storage**: Private bucket configured via `PRIVATE_OBJECT_DIR` environment variable

### Payment Processing
- **Provider**: Stripe
- **Integration**: `stripe-replit-sync` package for managed webhooks
- **Flow**: Create payment intent → Stripe Elements checkout → Webhook confirmation

## External Dependencies

### Third-Party Services
- **Stripe**: Payment processing for visa application fees ($92.95 per application)
- **Google Cloud Storage**: Document storage (passport scans, supporting documents)
- **PostgreSQL**: Primary database (provisioned via Replit)

### Key NPM Packages
- `drizzle-orm` / `drizzle-kit`: Database ORM and migrations
- `stripe` / `@stripe/react-stripe-js`: Payment integration
- `@google-cloud/storage`: Object storage client
- `@tanstack/react-query`: Async state management
- `zod`: Runtime type validation
- `react-hook-form`: Form handling
- `framer-motion`: Animations
- `date-fns`: Date formatting

### Environment Variables Required
- `DATABASE_URL`: PostgreSQL connection string
- `PRIVATE_OBJECT_DIR`: GCS bucket path for uploads
- Stripe credentials are fetched dynamically via Replit Connectors