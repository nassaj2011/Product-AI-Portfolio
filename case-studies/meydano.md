# Meydano — Sports Booking & Venue Operations Platform

## Overview

Meydano is a production web platform for sports-venue booking and venue operations. The platform supports multiple operational roles, reservation workflows, payments, wallet/refund logic, discounting, and pilot-based rollout.

## Problem

Sports facilities often manage availability, bookings, payments, cancellations, and operator coordination through fragmented manual processes. This creates several risks:

- inconsistent court or venue availability,
- duplicate or conflicting reservations,
- weak visibility for venue operators,
- payment and booking-state mismatches,
- difficult refund handling,
- operational errors around edge cases such as midnight schedules.

The objective was to turn these flows into a reliable digital booking and operations system suitable for real users and gradual rollout.

## My Role

I worked across product, business, and delivery layers rather than in a single narrow function. My responsibilities included:

- defining and refining product requirements,
- translating venue operations into product workflows,
- coordinating development and release priorities,
- reviewing booking, payment, wallet, cancellation, and refund behavior,
- designing pilot-launch gates and operational monitoring,
- validating production behavior with real transactions and regression tests,
- controlling scope and avoiding unnecessary changes during pilot periods.

## Solution

The platform was designed around role-based operations for administrators, venue managers, coaches, and players, with additional operational roles planned as the product evolves.

Core product capabilities include:

- venue and court scheduling,
- booking lifecycle management,
- payment verification,
- wallet and refund flows,
- SMS-based authentication and notifications,
- discount/coupon mechanisms,
- operational controls for venue managers,
- health and readiness monitoring,
- pilot monitoring with explicit stop/go criteria.

## Technology

The production stack includes:

- **Next.js** with the App Router,
- **PostgreSQL**,
- **Drizzle ORM**,
- **Tailwind CSS**,
- Jalali-calendar support,
- SMS OTP integration,
- online-payment integration,
- cloud deployment and health-check endpoints.

## Key Challenges

### 1. Booking consistency

A booking system must distinguish between historical bookings and currently blocking reservations. Cancellation, expiration, completion, and other lifecycle states must release availability correctly without creating duplicate active bookings.

### 2. Payment-to-booking integrity

A successful payment must correspond to the correct reservation state. The operational design therefore treated payment success without a confirmed reservation as a critical stop condition.

### 3. Midnight scheduling

Venue schedules crossing `23:00 → 00:00` required explicit handling and regression testing to avoid invalid availability behavior.

### 4. Pilot discipline

Instead of continuously changing production, the rollout was deliberately frozen around a known-good baseline. The pilot uses a limited cohort and predefined monitoring checkpoints, with expansion only after stability criteria are met.

## Validation & Results

Key outcomes achieved during stabilization and pilot preparation include:

- production deployment on a known-good baseline,
- booking/payment/refund flow validated with a real production transaction,
- full refund successfully returned to the user wallet after intentional cancellation,
- midnight scheduling regression fixed and validated,
- health and readiness endpoints confirmed operational,
- hundreds of automated tests passing across relevant booking and operational areas,
- a formal pilot plan established with monitoring checkpoints and stop conditions.

The product has moved from feature development into controlled real-user pilot operations.

## Product & Management Lessons

- A production pilot should be treated as an operational experiment, not as an excuse for continuous deployment.
- Payment and booking state must be monitored as a single business transaction.
- Explicit stop conditions reduce the risk of rationalizing serious pilot failures.
- Architecture and performance optimization should follow real operational evidence rather than precede it.
- Small controlled cohorts produce more useful feedback than broad launches when a product is still stabilizing.

## Confidentiality Note

This case study is intentionally sanitized. No credentials, private user data, proprietary source code, production secrets, or confidential organizational information are included.