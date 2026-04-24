# Data Processing Automation Workflow (n8n)

## Overview
This project demonstrates a cloud-based data automation workflow built using **n8n Cloud**.  
The workflow accepts a spreadsheet file upload, processes the data automatically, and generates summary metrics.

The goal of this project is to show **automation thinking**, **data processing logic**, and the ability to work within real-world cloud constraints.

---

## Problem
Manually calculating summaries from spreadsheets (such as total sales or averages) is time-consuming and error-prone when done repeatedly.

---

## Solution
I built an automation workflow that:
1. Accepts a spreadsheet file upload via a webhook
2. Extracts structured data from the uploaded file
3. Processes the data using custom logic
4. Outputs key summary metrics in a clean format

Each file upload automatically triggers the full workflow.

---

## Workflow Steps
1. **Webhook**
   - Receives a spreadsheet file upload (CSV or Excel)
   - Triggers the workflow execution

2. **Extract from File**
   - Reads and converts the uploaded file into structured JSON data

3. **Function Node**
   - Calculates:
     - Total number of records
     - Total sales amount
     - Average sales value

4. **Output / Set Node**
   - Formats results for clear and readable output

---

## Metrics Generated
- Records processed
- Total sales amount
- Average sales amount

---

## Tools Used
- **n8n Cloud**
- **JavaScript** (Function node logic)
- **CSV / Excel spreadsheets**

---

## What I Learned
- Designing cloud-native automation workflows
- Handling file uploads using webhooks
- Working with binary data in n8n
- Translating data analysis logic into automated systems
- Debugging real workflow execution issues

---

## Notes
This project is part of a **learning-focused portfolio**, emphasizing practical skills, documentation, and continuous improvement rather than claiming advanced expertise.

