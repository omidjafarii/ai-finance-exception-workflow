# AI Finance Exception Workflow

## Overview

I built this project as a small finance process automation prototype in n8n.

The workflow takes sample invoice and transaction records, checks them for common finance exceptions, and creates a readable report for review. It separates clean records from items that need attention, so a finance specialist can focus on exceptions instead of manually checking every row.

This is not an accounting approval tool. It is a human-in-the-loop workflow that supports data validation, reconciliation checks, and review preparation.

## Business Problem

Finance teams often need to review invoice and transaction data before posting, payment, reporting, or closing activities.

Common issues include:

* Missing supplier VAT numbers
* Duplicate invoice records
* VAT calculation mismatches
* Total amount mismatches
* Paid invoices without payment dates
* Due dates before invoice dates
* Missing account codes

Checking every row manually is slow, repetitive, and easy to get wrong, especially when the same checks need to be repeated across many records.

## Automation Goal

The goal of this workflow is to separate clean finance records from records that need human review.

The workflow produces:

* Review status: OK, Needs Review, or Exception
* Priority: Low, Medium, or High
* Exception category
* Issue description
* Suggested finance action
* Markdown summary report

## Why This Workflow Matters

In finance operations, not every record needs the same level of attention. Clean records can move forward, while records with missing data, duplicate IDs, VAT mismatches, date issues, or payment-status problems need review.

This workflow shows how a lightweight automation can reduce repetitive checking and prepare clear review notes before posting, payment, reporting, or closing activities.

## Workflow Steps

1. A manual trigger starts the workflow.
2. Sample finance data is created.
3. Invoice and transaction records are validated.
4. Exceptions are classified by category and priority.
5. A summary report is generated.
6. A Markdown report is prepared for export.

## Tools Used

* n8n
* JavaScript Code nodes
* Manual Trigger
* Edit Fields node
* Markdown report output

## Human-in-the-Loop Control

The workflow does not approve payments, post invoices, or make accounting decisions.

It only highlights exceptions and prepares review notes so a finance specialist can decide the correct next action.

This is important because finance automation should support control and review, not remove human responsibility from sensitive decisions.

## Example Checks

The workflow checks for issues such as:

* Missing invoice ID
* Missing supplier VAT number
* Possible duplicate invoice ID
* Due date before invoice date
* VAT mismatch
* Total amount mismatch
* Invoice marked as paid but missing payment date
* Missing account code

## Example Output

The final report groups records into review categories such as:

* OK
* Needs Review
* Exception

Each exception includes:

* Invoice ID
* Supplier name
* Amount
* Review status
* Priority
* Exception category
* Issue description
* Suggested action

## Possible Extensions

This prototype could be extended by adding:

* ERP export input
* Power Automate, Make, or Teams integration
* Real AI-generated explanations using ChatGPT, Claude, or Copilot
* Email or Teams notifications for exception reports
* Historical exception tracking for audit review
* Dashboard reporting for finance operations

## Repository Structure

```text
ai-finance-exception-workflow/
│
├── README.md
├── reports/
│   └── ai-finance-exception-report.md
├── sample-data/
│   └── sample-finance-records.json
├── screenshots/
│   ├── 01-workflow-canvas.png
│   ├── 02-validation-output.png
│   └── 03-report-export-output.png
└── workflow/
    └── n8n-workflow.json
```

## Project Purpose

This project was created as a practical showcase for AI-assisted process automation in finance operations.

It shows how a small workflow can:

* Understand a repetitive finance review process
* Detect data quality and reconciliation risks
* Classify exceptions by priority
* Prepare clear output for non-technical finance users
* Keep human review inside the process
