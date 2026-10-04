# FrameGard Bot — Telegram AI Image Workflow & Credit Operations

## Overview

FrameGard Bot is a serverless Telegram-based image workflow that combines AI image providers, user credits, package configuration, admin controls, and webhook-driven interaction in a single operational flow.

The project was designed to test how an AI image service can be delivered through a messaging interface while keeping provider choice, user balances, moderation/operational review, and configuration manageable from an admin layer.

## Problem

A Telegram AI service looks simple at first: receive an image, call an AI model, and return a result. In practice, a usable paid workflow needs to manage several additional concerns:

- webhook-driven state transitions,
- provider availability and model differences,
- user entitlements and credit balances,
- package configuration without redeployment,
- admin visibility and manual fallback workflows,
- input normalization before provider calls,
- separation of automated and manually fulfilled services,
- safe secret management in serverless deployment.

## My Role

I worked on the product and implementation flow across:

- service and pricing-model definition,
- Telegram user journey design,
- AI-provider integration decisions,
- credit/package behavior,
- admin workflow requirements,
- image-input normalization rules,
- production configuration and secret-handling requirements,
- iteration of available styles and provider routing.

## Solution

The bot supports a guided conversational flow inside Telegram.

Core capabilities include:

- `/start`, balance, purchase, admin and cancel flows,
- optional sponsor-channel membership checks,
- a free first-image rule,
- separate balances for automatic API processing and manual/economical processing,
- AI-model and style selection,
- configurable packages and pricing,
- admin-controlled model toggles and operational notices,
- webhook-driven Telegram interaction,
- server-side image normalization before provider submission.

The architecture also supports a hybrid fulfillment model: some packages are handled automatically through an AI provider while lower-cost/manual packages can be routed to an admin workflow for external processing and return through the bot.

## Technology

The project uses:

- **Next.js App Router**,
- Telegram Bot API and webhooks,
- **Upstash Redis** for lightweight state and configuration,
- multiple AI image-provider integrations,
- serverless deployment,
- environment-based credential management.

## Integration Patterns

### 1. Provider abstraction

The model catalog is tied to actual provider support rather than advertising models that are not available through the configured provider. Provider-specific routing is explicit.

### 2. Configurable commercial rules

Package sizes and pricing are stored in the operational configuration layer so they can be adjusted without redeploying the application.

### 3. Input normalization

Images are normalized server-side before provider use, with bounded dimensions, preserved aspect ratio, no forced upscaling, and a controlled temporary encoding policy.

### 4. Hybrid automation

The workflow recognizes that not every service needs to be fully automated. Automated and manual fulfillment can coexist while maintaining separate credit balances and user expectations.

## What This Demonstrates

FrameGard provides practical evidence for work involving:

- Telegram bots and webhook integrations,
- AI API integration,
- serverless workflow implementation,
- Redis-backed application state,
- configurable business rules,
- admin tooling,
- hybrid human-in-the-loop operations,
- lightweight digital-product delivery.

## Current Scope

The project is a focused product implementation rather than a claim of large-scale bot infrastructure. Its value as a case study is the integration of user flow, business rules, provider routing, credits, admin control, and AI processing in one working system.

## Confidentiality Note

This case study is sanitized. Bot tokens, API credentials, payment details, private user images, admin identifiers, and production environment values are not included.