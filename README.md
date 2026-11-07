# Enterprise AI Pilot

**A governed AI assistant for internal company knowledge.** Employees ask questions in plain
language and get answers drawn only from the documents they are allowed to see, with the
source shown for every answer and every request recorded in a tamper-evident audit log.

Most internal AI pilots stall at the same point: the demo works, then the security, legal and
data-protection teams ask who can see what, what gets logged, and what happens when the model
is wrong. Enterprise AI Pilot is built around those questions from day one.

> This repository contains product documentation only. The software itself is proprietary and
> not published here.

## What it does

- **Answers from your own documents.** Policies, handbooks, runbooks, reports. Every answer
  names the documents it came from, so people can check it.
- **Respects access rights.** Someone in engineering and someone in HR can ask the same
  question and get different answers, because each person only ever sees the documents their
  role permits. Restricted content is filtered out before the AI model sees anything.
- **Says "I don't know" instead of guessing.** If nothing the user may see answers the
  question, the assistant declines rather than inventing an answer.
- **Hides personal data in answers.** Email addresses, phone numbers, bank account numbers and
  national identity codes are masked before an answer is shown, and are kept out of the logs.
- **Resists manipulation.** Questions and documents are screened for prompt-injection attempts,
  such as text that tries to override the assistant's instructions.
- **Checks its own citations.** References to documents the model was not given are removed,
  and answers without a traceable source are flagged.
- **Keeps a tamper-evident audit trail.** Every request is recorded, and administrators can
  verify that no record has been altered or removed.

## Choose where the AI runs

| Option | Good fit for |
|---|---|
| **Cloud AI model** | Best answer quality, quick start |
| **Local model on your own server** | Documents and questions never leave your network |
| **Offline mode** | Demos and testing without any AI service |

The model can be chosen per question, and if a model is unavailable the assistant falls back
to a simpler answer instead of failing.

## How a question is handled

```mermaid
flowchart LR
    Q[Question] --> A[Identity and<br/>rate limit]
    A --> I[Manipulation<br/>check]
    I --> R[Search only<br/>permitted documents]
    R --> M([AI model])
    M --> C[Citation<br/>check]
    C --> P[Personal data<br/>masking]
    P --> L[Audit log]
```

The AI model is one step in the middle. Every step around it is fixed, tested logic that
decides what the model may see and what the user may receive.

## Quality you can measure

Every release runs through automated tests and an evaluation suite with hard pass/fail gates:
correct answers with the right source, zero leaks across roles, refusal of questions the
documents cannot answer, blocked manipulation attempts, and an intact audit trail. A release
that fails any gate does not ship.

## Who it is for

Organisations that want to put AI on top of internal knowledge without losing control of
access rights, personal data or accountability. Typical first use cases are HR and policy
questions, IT and engineering runbooks, and internal finance or operations reporting.

## Pilots and access

We run focused pilots on a customer's own documents and access model, in the cloud or on
premises. To discuss a pilot or see a live demo, contact the author through the GitHub
profile.

© 2026 Onur Kapucu. All rights reserved.
