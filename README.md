# Hardware Shipment Clearance Follow-up Assistant

An AI-powered demonstration app that helps logistics teams interpret
customs broker updates, identify missing information, and draft
follow-up emails for hardware shipments.

## Live Demo

https://cf-ai-logistics-assistant-lynn.lynnli-office.workers.dev

Use fictional shipment data only.

## Problem

Logistics updates can be ambiguous. “Documents received” does not
necessarily mean an entry has been submitted, and “entry submitted”
does not mean customs release has been confirmed.

This app helps users distinguish those stages and identify what
needs to be verified next.

## Features

- Chat input in English or Chinese
- Evidence-based summaries of supplied broker messages
- Missing-information checklists and suggested next actions
- English follow-up email drafts
- Case-specific conversation history
- A new-case function to separate conversations

## How It Works

1. The user pastes a broker update or asks a question.
2. A Cloudflare Worker validates the request.
3. A case-specific Durable Object loads the conversation history.
4. Workers AI analyzes the update using the conversation and
   clearance-follow-up instructions.
5. The successful exchange is saved and displayed.

The browser stores the current case ID and a local conversation copy.
The Durable Object stores conversation history used for model context.

## Technology

- Cloudflare Workers: request handling and application logic
- Workers AI: Llama 3.3 70B Instruct FP8 Fast
- Durable Objects: persistent case conversation history
- Workers Static Assets: HTML, CSS, and JavaScript chat interface
- Browser localStorage: current case and local display history

## Assignment Components

| Component | Implementation |
| --- | --- |
| LLM | Workers AI |
| Workflow and coordination | Worker request validation, case routing, model call, and persistence |
| User input | Browser-based chat |
| Memory or state | Durable Object history and browser localStorage |

## Manual Testing

The following scenarios were tested interactively:

| Scenario | Observed result |
| --- | --- |
| Documents received and processing | Did not treat this as confirmed submission |
| Entry submitted, awaiting release | Distinguished submission from release |
| “NOT released” with revised invoice requested | Recognized negation and the requested document |
| Warehouse and broker give conflicting updates | Required human review rather than marking released |
| A new Chinese-language case | Produced a complete Chinese explanation |
| Refresh and continue the current case | Previous messages remained visible and the response used prior context |

An earlier Chinese response was incomplete. Later Chinese tests
succeeded, but the cause has not been established.

These are manual observations, not a guarantee of model reliability.

## Limitations

- No live customs-system or email integration
- No independent verification of customs release
- No automatic email sending
- Status assessments are model-generated text, not a validated
  structured shipment-status record
- Country-specific customs requirements still require human review
- No user authentication; this is a demonstration, not a production system
- Each case supports up to 10 successful exchanges
- New case starts a separate conversation but does not delete
  older server records
- No automatic retention expiry or server-record deletion interface
- Browser storage is not a cross-device account system
- Public usage may consume Cloudflare AI and storage quotas

## Run Locally

Requirements: Node.js, npm, and a Cloudflare account.

    npm install
    npx wrangler login
    npm run dev

Workers AI requests require Cloudflare access.

## Deploy

    npm run deploy

The Worker name and resource bindings are defined in wrangler.jsonc.

## AI Assistance

This project was developed with AI-assisted coding and step-by-step
guidance. Project-related prompts, decisions, and corrections are
documented in PROMPTS.md.

## Project Status

Working prototype. Further work includes stronger output validation,
structured status tracking, access controls, and retention management.
