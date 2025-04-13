# Invoice Processing Workflow
## Internal Documentation

### Purpose
This document outlines the complete workflow for processing vendor invoices, including validation steps, system integrations, and exception handling procedures.

### 1. Invoice Retrieval
**Action:** Retrieve the invoice based on ID  
**System:** VIM (Vendor Invoice Management)  
**Input:** Invoice ID  
**Output:** Invoice details  
**Exception Handling:**
- If invoice ID is invalid: Log error and notify invoice processing team
- If system unavailable: Retry connection 3 times with 30-second intervals before escalating to IT support
- If invoice data is corrupted: Flag for manual review

### 2. PO ID Verification
**Action:** Check if invoice has PO ID  
**Decision Point:** Yes/No  
**Exception Handling:**
- If PO field exists but is empty: Treat as "No PO ID"
- If PO field contains non-standard format: Attempt to normalize before proceeding

### 3a. PO ID Present - PO Retrieval
**Action:** Retrieve PO from VIM using PO ID  
**System:** VIM  
**Input:** PO ID from invoice  
**Output:** PO details  
**Exception Handling:**
- If PO retrieval fails due to system error: Retry 3 times before escalating
- If connection timeout: Log incident and retry during off-peak hours

### 3b. PO ID Missing - Vendor Communication
**Action:** Communicate to the vendor about missing PO ID  
**System:** Vendor Communication Portal  
**Input:** Invoice ID, Vendor ID  
**Output:** Communication record  
**Exception Handling:**
- If communication system fails: Create email notification via backup system
- If vendor contact information is missing: Escalate to Vendor Management team

### 4. Open PO Search
**Action:** Retrieve all open POs from VIM for the Vendor ID  
**System:** VIM  
**Input:** Vendor ID (extracted from invoice)  
**Output:** List of open POs  
**Exception Handling:**
- If Vendor ID cannot be extracted from invoice: Flag for manual review
- If no open POs exist: Document in vendor record and proceed to vendor communication
- If too many open POs returned (>100): Apply additional filters based on date and amount

### 5. PO Matching
**Action:** Find a PO having a match with the invoice  
**Logic:** Match based on amount, items, dates, and other relevant fields  
**Decision Point:** PO Found/Not Found  
**Exception Handling:**
- If partial matches found: Select best match based on predefined scoring system
- If system cannot complete matching operation: Flag for manual review

### 6. PO Validation
**Action:** Check if PO exists  
**Decision Point:** Yes/No  
**Exception Handling:**
- If PO status is ambiguous (neither clearly active nor clearly inactive): Flag for review by Procurement team

### 7. Goods Receipt (GR) Retrieval
**Action:** Retrieve GR based on invoice  
**System:** ERP System  
**Input:** Invoice ID, PO ID  
**Output:** GR details  
**Exception Handling:**
- If multiple GRs exist for the PO: Consolidate GR data before matching
- If GR not found but should exist: Notify receiving department
- If GR system unavailable: Schedule automated retry and notify stakeholders

### 8. Three-Way Matching
**Action:** Match details across invoice, PO & GR  
**Logic:** Compare line items, quantities, prices, taxes, and totals  
**Decision Point:** Match/Mismatch  
**Exception Handling:**
- If matching cannot be completed due to missing data: Document specific missing elements and request from appropriate party
- If minor discrepancies exist (within tolerance): Document and proceed with approval
- If currency conversion issues exist: Apply current exchange rates and recalculate

### 9a. Successful Match - Invoice Approval
**Action:** Approve invoice  
**System:** Accounts Payable system  
**Input:** Invoice ID, approval code  
**Output:** Approved invoice record  
**Exception Handling:**
- If approval system unavailable: Queue approval for batch processing
- If approval triggers audit flags: Document reason and escalate to AP Manager for review
- If duplicate payment warning appears: Halt process and initiate duplicate check

### 9b. Failed Match - Vendor Communication
**Action:** Communicate to the vendor about mismatch  
**System:** Vendor Communication Portal  
**Input:** Invoice ID, PO ID, mismatch details  
**Output:** Communication record  
**Exception Handling:**
- If communication fails: Create backup email notification
- If recurring issue with specific vendor: Flag vendor account for review
- If mismatch is suspected system error: Initiate internal review before vendor communication

### 10. Invalid PO Communication
**Action:** Communicate to the vendor about invalid PO  
**System:** Vendor Communication Portal  
**Input:** Invoice ID, invalid PO ID, vendor ID  
**Output:** Communication record  
**Exception Handling:**
- If communication system unavailable: Use alternate contact methods (email/phone)
- If vendor disputes PO validity: Escalate to Procurement for review
- If vendor has history of invalid PO submissions: Flag for vendor performance review

## Performance Monitoring & Compliance

### Key Performance Indicators
- Average processing time per invoice
- Exception rate by category
- Vendor response time to communications
- First-pass match rate

### Compliance Requirements
- All communications with vendors must be logged in the system
- Approvals must include digital signature of approving agent
- Exceptions requiring manual intervention must be documented with resolution notes
- All invoices on hold for >5 business days require management notification

### System Access & Security
- All actions in this workflow require appropriate system permissions
- Activity logs are maintained for audit purposes
- Sensitive vendor and financial data must be handled according to data protection policies

## Document Control
- Version: 1.2
- Last Updated: April 13, 2025
- Next Review: October 13, 2025
- Document Owner: Accounts Payable Department
