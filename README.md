# Finance Exception Routing Workflow in n8n

## Overview

This project demonstrates a finance exception routing workflow built in n8n.

The workflow takes raw sample finance records, validates them using JavaScript logic, calculates review status and priority, then routes each record into the correct Google Sheets log based on business rules.

The goal is to show how n8n can be used for process automation, conditional routing, audit logging, and human-in-the-loop finance review workflows.

## Business Problem

Finance teams often need to separate clean records from records that require human review.

A simple spreadsheet can show problems, but it does not automatically route records into different operational queues.

This workflow simulates a practical finance control process:

- clean records are logged as cleared
- standard issues are added to a review queue
- urgent issues are added to an escalation log

## Workflow Architecture

```text
Schedule Trigger
↓
Create Sample Finance Data
↓
Validate Finance Exceptions
↓
Gate 1 - Review Needed?
   ├── No
   │   └── Create Cleared Records Log
   │       └── Append Cleared Records to Google Sheets
   │
   └── Yes
       ↓
       Gate 2 - Urgent Review?
          ├── Yes
          │   └── Create Same-Day Escalation Alert
          │       └── Append Urgent Escalations to Google Sheets
          │
          └── No
              └── Create Standard Review Queue
                  └── Append Standard Review Queue to Google Sheets