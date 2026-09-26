# Project 2 — Lead / Sponsorship Intake Automation

## Overview

This n8n workflow automates the intake and initial processing of lead or sponsorship inquiries.

A company submits an inquiry through an n8n form. The workflow evaluates the submitted budget, routes the inquiry based on a **1,000,000 budget threshold**, sends an appropriate email response, and records the inquiry and decision in Google Sheets.

This project demonstrates how n8n can connect forms, conditional logic, email, and spreadsheets into a complete business automation workflow.

---

## Workflow Architecture

```text
Form Submission
       ↓
Budget Evaluation
       ↓
     Switch
    ↙      ↘
Decline    Approval
   ↓          ↓
 Gmail       Gmail
   ↓          ↓
 Google     Google
 Sheets     Sheets
```

---

## Workflow Components

### 1. Form Trigger

The workflow starts when a user submits the **Sponsor Inquiry** form.

The form collects:

* Company Name
* Contact Name
* Email
* Website
* Budget
* Notes

The form submission also provides metadata such as the submission timestamp.

---

### 2. Budget Evaluation

The submitted budget is evaluated using an n8n **Switch** node.

The workflow uses:

* **Budget < 1,000,000** → Decline branch
* **Budget ≥ 1,000,000** → Approval / Follow-Up branch

For example:

| Submitted Budget | Route    |
| ---------------: | -------- |
|           50,000 | Decline  |
|          500,000 | Decline  |
|        1,000,000 | Approval |
|        2,000,000 | Approval |

---

### 3. Decline Email

In the decline branch, n8n sends an email to the submitted email address.

The email uses the submitted **Company Name** in the subject and **Contact Name** in the message.

The node is documented as **Send Decline Message**.

> Note: The original exported workflow currently contains the node name `Send Deline Message`. This README uses the corrected spelling **Send Decline Message**. If the workflow itself is published, the n8n node should also be renamed to match.

After sending the email, the workflow records the inquiry in Google Sheets with:

```text
Decision = Declined
```

---

### 4. Approval / Follow-Up Email

If the submitted budget is **1,000,000 or higher**, the workflow sends a follow-up email to the submitted email address.

The email uses the submitted **Company Name** in the subject and **Contact Name** in the message.

After the email is sent, the inquiry is recorded in Google Sheets with:

```text
Decision = Follow Up Sent
```

---

### 5. Google Sheets Record

Both branches append the inquiry to Google Sheets.

The following information is stored:

* Company Name
* Contact Name
* Email
* Website
* Budget
* Notes
* Submitted At
* Decision

This creates a simple centralized record of all submitted inquiries.

---

## Technologies Used

* **n8n** — Workflow automation
* **n8n Form Trigger** — Inquiry collection
* **Switch Node** — Conditional budget routing
* **Gmail** — Automated email responses
* **Google Sheets** — Lead/inquiry tracking

---

## Project Structure

```text
project-2-lead-intake/
├── project-2-lead-intake.json
└── README.md
```

---

## Setup

### 1. Start n8n

Run your local n8n installation:

```bash
n8n
```

Open the n8n editor:

```text
http://localhost:5678
```

### 2. Import the Workflow

1. Open n8n.
2. Import `project-2-lead-intake.json`.
3. Review the workflow nodes and connections.
4. Configure your own Gmail credentials.
5. Configure your own Google Sheets credentials.
6. Select your own Google Sheets document.

### 3. Review the Budget Threshold

The current workflow uses:

```text
1,000,000
```

as the routing threshold.

Modify the Switch node if a different threshold is required.

### 4. Activate the Workflow

After configuring the required credentials and reviewing the workflow, activate it.

---

## Testing

Submit the form using test information.

### Test a Decline Route

Use a budget below:

```text
1,000,000
```

The workflow should:

1. Receive the form submission.
2. Route it to the decline branch.
3. Send the decline email.
4. Append the inquiry to Google Sheets.
5. Store `Declined` as the decision.

### Test an Approval / Follow-Up Route

Use a budget of:

```text
1,000,000
```

or higher.

The workflow should:

1. Receive the form submission.
2. Route it to the approval branch.
3. Send the follow-up email.
4. Append the inquiry to Google Sheets.
5. Store `Follow Up Sent` as the decision.

---

## Security and Public Repository Notes

The exported n8n workflow may contain environment-specific configuration and test information.

Before committing the workflow to a public repository:

* Remove or sanitize `pinData` from the exported JSON.
* Do not publish personal test email addresses.
* Do not publish API keys, access tokens, passwords, or other secrets.
* Do not expose private Google Sheets document IDs unnecessarily.
* Do not expose private OAuth credential information unnecessarily.
* Replace personal Google resources with the user's own resources when importing the workflow.
* Keep credentials configured inside n8n rather than hardcoding them into the workflow.

The repository should also use a `.gitignore` that excludes environment files and credential-related files such as `.env` and credential files.

**Important:** `.gitignore` only prevents separately stored files from being committed. It does **not** remove sensitive information already embedded inside an exported `.json` workflow. The workflow JSON itself must therefore be reviewed and sanitized before publishing.

---

## Key Takeaways

This project demonstrates several practical n8n concepts:

* Form-based workflow triggers
* Receiving and using submitted form data
* Conditional routing with Switch
* Dynamic values in Gmail messages
* Automated business-rule decisions
* Writing workflow results to Google Sheets
* Connecting multiple external services
* Building an end-to-end business automation without writing a traditional backend

The core pattern is:

```text
Collect Data
     ↓
Apply Business Logic
     ↓
Take Action
     ↓
Record Result
```
