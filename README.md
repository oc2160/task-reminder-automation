# Task Reminder Automation - Salesforce Project

## Overview
An automated task reminder system built on a custom Project_Task__c object in Salesforce.
Proactively notifies assigned users before due dates and automatically marks overdue tasks.

## Features
- 3-day advance email reminder before task due date
- 1-day advance email reminder before task due date
- Instant overdue detection and status update on save
- Overdue notification email with red-highlighted HTML template
- Business logic guards - no duplicate emails for already-overdue or completed tasks

## Tech Stack
- Custom Object: Project_Task__c with 7 custom fields, including a Formula field
- Record-Triggered Flow: Project_Task_Reminder_Flow
  - Immediate Path: Decision logic, Update Records, Email Alert
  - Scheduled Path 1: 3 days before Due_Date__c
  - Scheduled Path 2: 1 day before Due_Date__c
- Email Alerts: Task_Due_Reminder_Alert, Task_Overdue_Notification_Alert
- Email Templates: Custom HTML and plain text templates with merge fields

## Object Schema - Project_Task__c

| Field | Type | Purpose |
|---|---|---|
| Task Name | Text | Record identifier |
| Assigned To | Lookup (User) | Owner responsible for the task |
| Due Date | Date | Deadline for the task |
| Status | Picklist | Not Started / In Progress / Completed / Overdue |
| Priority | Picklist | High / Medium / Low |
| Reminder Sent | Checkbox | Tracking flag |
| Description | Long Text Area | Task details |
| Days Until Due | Formula (Number) | Due_Date__c - TODAY() |

## Flow Logic

Start (Record-Triggered: Created or Updated, Status not equal Completed)
- Run Immediately
  - Decision: Check If Task Is Overdue
    (Due Date < Today AND Status not Overdue AND Status not Completed)
    - True: Update Status to Overdue, Send Overdue Email
    - False: End
- Scheduled Path: 3 Days Before Due Date - Send 3-Day Reminder Email
- Scheduled Path: 1 Day Before Due Date - Send 1-Day Reminder Email

## What I Learned
- Building Record-Triggered Flows with multiple Scheduled Paths
- Designing Decision-element business logic with multi-condition guards to prevent duplicate automation runs
- Configuring Email Alerts and HTML/text email templates with merge fields
- Testing automation logic using manual record creation and field-state verification in a Developer Org

## Author
Omkar Choudhari | MCA (Data Science) | Salesforce PD1 Certified
[github.com/oc2160](https://github.com/oc2160)
