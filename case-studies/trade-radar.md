# Trade Radar IR — Market Intelligence Automation

## Overview

Trade Radar IR is a cloud-operated market-intelligence workflow designed to collect trade-related signals from explicitly authorized messaging sources, normalize them into structured records, filter low-quality data, and surface potentially useful commercial opportunities.

The project combines source authorization, data collection, conservative parsing, provenance preservation, cloud execution, and operational pilot monitoring.

## Problem

Commercial opportunities are often published in fragmented messaging channels and informal networks. Raw messages may contain useful information, but they are difficult to use systematically because:

- message structure is inconsistent,
- product terminology varies,
- intent may be ambiguous,
- quantity, price, and contact details may be incomplete,
- the same opportunity may appear multiple times,
- automated collectors can easily create noisy or misleading outputs.

The objective was to build a pipeline that favors traceability and conservative quality gates over aggressive extraction.

## My Role

My responsibilities included:

- defining product scope and pilot criteria,
- selecting and validating authorized sources,
- designing the collection and filtering workflow,
- reviewing parser behavior against real samples,
- defining structural usability gates,
- coordinating cloud deployment and operational-state persistence,
- establishing privacy and credential-handling rules,
- monitoring the live pilot and deciding when technical changes should be frozen.

## Solution

The workflow separates collection, normalization, classification, storage, and sanitized operator outputs.

Core principles include:

- collect only from explicitly authorized sources,
- keep source evidence and credentials private,
- use read-only collection where possible,
- normalize product terminology conservatively,
- require explicit trade intent and recognized product structure before surfacing an opportunity,
- preserve source-level traceability,
- encrypt operational state used in cloud execution,
- measure source health independently of business-value metrics.

## Technology & Architecture

The project uses a combination of:

- Python-based collection and parsing,
- Telegram Web read-only collection for authorized sources,
- Bale Bot API integration,
- automated tests and linting,
- GitHub Actions for cloud execution,
- encrypted runtime state and checkpoints,
- structured opportunity records linked back to private raw signals.

## Key Challenges

### 1. Authorized source access

One Telegram public-preview route worked differently in cloud runners than in local testing. The project therefore moved away from assuming that a public preview endpoint was reliable and used an authenticated read-only web collector for an explicitly authorized source.

### 2. Credential transfer in cloud automation

A cloud preflight initially failed even though the underlying Bale token was valid locally. The issue was isolated to secret-transfer formatting and corrected without exposing the credential.

### 3. Conservative parser adaptation

Initial real samples showed that product vocabulary was too narrow. Instead of relaxing the entire parser, only evidence-supported product terms were added. Generic and ambiguous terms remained unsupported.

### 4. Metrics clarity

The project distinguished between run-scoped metrics and cumulative/rematerialized snapshot metrics so pilot results would not be misinterpreted.

### 5. Pilot stability

Once the four-source cohort was established, the active 72-hour window was frozen: no parser, source-cohort, or configuration changes unless the system degraded.

## Pilot Evidence

The four-source cloud cohort consists of three authorized Telegram Web sources and one Bale source.

At the start of the current pilot window:

- all **4/4 sources** were healthy,
- no sources failed,
- new live signals were collected,
- multiple structurally usable SELL opportunities were produced,
- contact provenance was retained for usable opportunities,
- encrypted cloud state was saved successfully.

The operator-facing sanitized layer intentionally does not expose raw private message content or credential values.

## Product & Engineering Lessons

- Source health and business value are different metrics and should be monitored separately.
- Parser improvements should be evidence-driven and minimal during a live validation phase.
- A secure automation pipeline must preserve provenance without leaking raw data.
- Cloud execution should have preflight checks before a real measurement window begins.
- Freezing a cohort during a pilot is critical if results are meant to be comparable over time.
- A useful market-intelligence product needs an operator-safe path from structured opportunity back to authorized source evidence.

## Confidentiality Note

This case study is intentionally sanitized. Real source identifiers, message text, credentials, private contacts, encrypted state, and proprietary operational data are not included.