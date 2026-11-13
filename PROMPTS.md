# AI Assistance and Development Log

## About This Record

This project was built through a Chinese-language conversation with
ChatGPT, including step-by-step instruction and AI-generated code.

This document is a curated development log, not a complete verbatim
transcript. Quoted user prompts are original messages. English
translations and process summaries are labeled separately.

## 1. Learning and Project Selection

Original user prompt:
“可是我不会 你可以一步一步教我吗”

English translation:
“I don't know how to do this. Can you teach me step by step?”

Process summary:
The AI initially suggested a logistics exception assistant.
The applicant asked how the project related to the logistics role
and whether customs-clearance tracking would be a better topic.

Original user prompt:
“那是不是还是做清关状态方面的比较好”

English translation:
“Would it be better to focus on customs-clearance status?”

Decision:
Build a hardware shipment clearance follow-up assistant.
The first version analyzes user-provided updates rather than
connecting to live customs systems.

## 2. Implementation Assistance

Process summary:
The AI supplied code and instructions for these files:

- wrangler.jsonc
- package.json
- src/index.js
- public/index.html

The applicant created the files in GitHub, connected the repository
to Cloudflare, deployed the application, and ran interactive tests.

The AI selected the initial implementation:
- Workers AI for model responses
- A Worker for request handling and case routing
- Durable Objects for conversation persistence
- Static assets for the browser interface
- Browser localStorage for the current case and display history

The applicant followed guided implementation steps.
The code was AI-generated rather than independently written
from scratch by the applicant.

## 3. Business Rules

Process summary:
The AI proposed rules distinguishing documents received,
entry submitted, release confirmation, missing documents,
and conflicting evidence.

These rules were checked through the manual tests below.
They are not a substitute for independent customs verification.

## 4. Manual Test Prompts

The following prompts were supplied by the AI and submitted by
the applicant to the deployed application.

### Documents Received

Shipment DEMO-001 contains network equipment destined for Canada.
The broker wrote: "We have received your documents and are processing
the entry." Has the entry been submitted? What should I follow up on?

Observed result:
The app did not treat processing as confirmed submission.

### Submission Confirmed

Update for DEMO-001: The broker has now confirmed:
“The entry has been submitted. We are awaiting customs release.”
What is the status now? Please reply in Chinese, with the email
draft in English.

Observed result:
The English email reflected submission and pending release,
but the Chinese explanation was incomplete.

### English Diagnostic

For DEMO-001, repeat your assessment entirely in English.
Clearly state whether submission is confirmed and whether
release is confirmed.
Do not draft an email this time.

Observed result:
The English response distinguished confirmed submission
from unconfirmed release.

### Negated Release

New broker update for DEMO-001:
“The shipment is NOT released. Please provide a revised commercial invoice.”

Summarize the current status and next action in English.
Do not draft an email.

Observed result:
The app recognized “NOT released” and the invoice request.

### Conflicting Sources

For DEMO-001, the warehouse says the shipment is released.
The broker says it is NOT released and requests a revised
commercial invoice.
Neither message has a timestamp or release reference.

Can I mark it as released?
Explain the conflicting information in English. Do not draft an email.

Observed result:
The app identified the conflict and required human review.

### Chinese Response

请只用简体中文回答，不要写邮件。

虚构订单 DEMO-002，目的地加拿大。
清关行说：“已收到资料，正在处理。”
这能证明已经提交申报或已经放行吗？请用三句话解释。

Observed result:
The app produced a complete Chinese response and did not
infer submission or release.

### Refresh and Continue

清关行刚刚补充确认：“申报已提交，正在等待放行。”
请结合这票货之前的信息，用中文说明状态发生了什么变化，
不需要写邮件。

Observed result:
After refreshing, the prior conversation remained visible.
The response described the change from unconfirmed submission
to confirmed submission, with release still unconfirmed.

## 5. Issues Identified During Review

- One Chinese response was incomplete; the cause remains unresolved.
- Some responses inferred that documents were complete or insufficient
  beyond what the supplied message explicitly established.
- Some wording did not sufficiently distinguish a broker's report
  from independently verified current customs status.

These issues were identified during testing.
The initial code has not yet been revised to resolve them.

## 6. Attribution

The applicant selected the clearance-follow-up direction,
performed the guided setup and deployment, and submitted
test outputs for review.

ChatGPT proposed the architecture, generated the initial code,
supplied test prompts, and helped interpret test results.

This log will be updated as development continues.
