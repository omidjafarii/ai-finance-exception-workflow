# Finance Exception Routing Workflow in n8n

## Overview

This project demonstrates a finance exception routing workflow built in n8n.

The workflow takes raw sample finance records, validates them using JavaScript logic, calculates review status and priority, then routes each record into the correct Google Sheets log based on business rules.

The goal is to show how n8n can be used for process automation, conditional routing, audit logging, and human-in-the-loop finance review workflows.

## Business Problem

Finance teams often need to separate clean records from records that require human review.

A simple spreadsheet can identify issues, but it does not automatically route records into different operational queues.

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


##Input Data
The workflow starts from raw finance records.

The sample input includes fields such as:

- invoice ID
- supplier name
- invoice date
- due date
- total amount
- VAT amount
- expected VAT amount
- payment status
- payment date
- account code

The input data does not manually include priority, review status, exception category, or action notes. These are calculated inside the workflow.
Sample data is available in:
```text
v2-routing-automation/sample-data/sample-finance-records.csv

##Validation Logic

The validation step checks each record and calculates:
- review status
- priority
- exception category
- detected issues
- suggested action
- review note

##Example checks include:
- missing account code
- due date before invoice date
- VAT mismatch
- paid invoice with missing payment date
- possible duplicate invoice records

##Routing Logic
The workflow uses two decision gates.
##Gate1:Review Needed?
Clean records are sent to the cleared records log.
Records with detected issues continue to the urgency check.
##Gate 2: Urgent Review?
High-priority records are sent to the urgent escalation log.
Non-urgent records are sent to the standard review queue.

##Output
The workflow writes routed results into a Google Sheet named:
```text
Finance Exception Workflow Log

It uses three tabs:
```text
Cleared Records
Standard Review Queue
Urgent Escalations

##Cleared Records
Used for records that passed validation and do not need manual review.

##Standard Review Queue
Used for records that require finance review within a normal review cycle.

##Urgent Escalations
Used for high-priority records that should be reviewed as soon as possible before further processing.

##Screenshots
##Workflow Canvas

The workflow validates raw finance records, routes them through two decision gates, and sends each category to a different Google Sheets output.

##Cleared Records Log
Clean records are logged separately because they do not require human review.

##Standard Review Queue
Non-urgent exceptions are routed into a normal finance review queue.

##Urgent Escalations Log
High-priority exceptions are routed into an urgent escalation log for same-day review.

##Repository Structure
```text
finance-exception-monitoring-workflow/
├── README.md
├── v1-simple-report/
│   ├── workflow/
│   ├── sample-data/
│   ├── screenshots/
│   └── reports/
│
└── v2-routing-automation/
    ├── workflow/
    │   └── n8n-finance-exception-routing-v2.json
    │
    ├── sample-data/
    │   └── sample-finance-records.csv
    │
    ├── screenshots/
    │   ├── workflow-canvas-v2.png
    │   ├── cleared-records-log.png
    │   ├── standard-review-queue.png
    │   └── urgent-escalations-log.png
    │
    ├── reports/
    └── docs/

##Why n8n Was Used
This workflow uses n8n because the value is not only in detecting issues.

The value is in orchestrating a process:
- scheduled execution
- JavaScript-based validation
- conditional gates
- separate process branches
- Google Sheets integration
- audit-style logging
- human review routing

##What This Project Demonstrates

This project demonstrates:
- building a workflow in n8n
- writing JavaScript validation logic inside workflow nodes
- routing records based on calculated business rules
- separating clean, standard, and urgent cases
- connecting n8n to Google Sheets
- creating audit-style operational logs
- designing human-in-the-loop review processes

##Current Limitations
This is a portfolio workflow, not a production finance system.

- sample data is generated inside the workflow
- duplicate alert prevention is not implemented yet
- urgent email alerts are planned but not included in the current version
- no live ERP or accounting system is connected
- no approval workflow is included yet

##Future Improvements
Planned improvements:
- connect the workflow to a real CSV upload, database, or ERP-style data source
- add duplicate prevention before logging repeated urgent cases
- add email or Slack alerts for urgent exceptions
- add approval tracking for reviewed items
- connect to a SQL-backed business dataset
- add error handling and execution failure notifications

##Project Evolution
This repository includes two versions.

##V1: Simple Report
The first version validates sample finance records and creates a basic exception report.

##V2: Routing Automation
The second version improves the workflow by adding:
- decision gates
- separate process branches
- Google Sheets logging
- clearer human review routing
- standard and urgent review separation

##Project Purpose
This project was built to demonstrate practical process automation skills using n8n.
It shows how raw business records can be validated, classified, routed, and logged into operational queues using automation logic.
