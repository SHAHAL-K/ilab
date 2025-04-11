# Invoice Verification Process Guide

## Table of Contents
1. [Introduction](#introduction)
2. [Invoice Processing Scenarios](#invoice-processing-scenarios)
   - [Scenario 1: Valid PO ID with Matching Items](#scenario-1-valid-po-id-with-matching-items)
   - [Scenario 2: Valid PO ID with Non-Matching Items](#scenario-2-valid-po-id-with-non-matching-items)
   - [Scenario 3: Invalid PO ID](#scenario-3-invalid-po-id)
   - [Scenario 4: Missing PO ID with Matchable Open POs](#scenario-4-missing-po-id-with-matchable-open-pos)
   - [Scenario 5: Missing PO ID with No Matching POs](#scenario-5-missing-po-id-with-no-matching-pos)
3. [Common Issues and Solutions](#common-issues-and-solutions)
   - [PO-Related Issues](#po-related-issues)
   - [Invoice Status Issues](#invoice-status-issues)
   - [Account Posting Issues](#account-posting-issues)
   - [Aggregation Issues](#aggregation-issues)
4. [System Transactions and Codes](#system-transactions-and-codes)
5. [Contact Information](#contact-information)

## Introduction

This document provides guidance for handling various invoice verification scenarios in the SAP system. It covers standard procedures for invoice processing, troubleshooting common issues, and resolving discrepancies.

## Invoice Processing Scenarios

### Scenario 1: Valid PO ID with Matching Items

**Process Steps:**
1. Extract the PO ID from the invoice
2. Retrieve the PO details associated with the PO ID
3. Confirm invoice items match PO details (description, quantity, price, product details)
4. Validate invoice items against the Goods Receipt (GR)
5. If all details align between invoice, PO, and GR:
   - Mark the invoice as fully matched and approve for processing

**Common Issues:**
- **Invalid PO ID**: Verify for typographical errors, contact procurement for correct PO ID or request a new valid PO
- **Non-matching invoice items**: Flag for manual review, contact vendor for correction or initiate partial approval for matching items

### Scenario 2: Valid PO ID with Non-Matching Items

**Process Steps:**
1. Extract the PO ID from the invoice
2. Retrieve the PO details associated with the PO ID
3. Compare invoice items with PO details
4. Validate invoice items against the Goods Receipt (GR)
5. Resolution path:
   - If no match between invoice and PO: Notify vendor and buyer of mismatch
   - If invoice details align with PO details but not with GR: Notify vendor and buyer of mismatch
   - If both PO and GR align with invoice items: Mark invoice as fully matched and approve for processing

**Common Issues:**
- **"Verified as incorrect" status**: Check error log (T-code MIR7) for error codes like IV-007 (Price Deviation) or IV-012 (GR Missing)
- **"Parked Released" status**: Run T-code FB03 to identify errors related to missing tax codes or GL account blocks

### Scenario 3: Invalid PO ID

**Process Steps:**
1. Extract the PO ID from the invoice
2. Attempt to retrieve PO details
3. If PO not found in system:
   - Notify vendor and buyer about invalid PO ID

**Common Issues:**
- **Aggregation totals mismatch**: Use T-code MIR6 to check line-item breakdown and adjust if within tolerance
- **Custom aggregation requirements**: Configure in "Customizing for Logistics Invoice Verification"

### Scenario 4: Missing PO ID with Matchable Open POs

**Process Steps:**
1. Attempt to extract PO ID from invoice
2. Get vendor ID associated with invoice
3. Retrieve list of open POs for that vendor
4. Compare invoice details with open POs
5. Validate invoice items against Goods Receipt
6. If matching PO and GR found:
   - Update invoice with correct PO and approve for processing

**Common Issues:**
- **Wrong G/L account posting**: Reverse with T-code MR8M, check OBYC mapping
- **Missing required accounts**: Park invoice (T-code MIR7) and notify GL team

### Scenario 5: Missing PO ID with No Matching POs

**Process Steps:**
1. Attempt to extract PO ID from invoice
2. Get vendor ID associated with invoice
3. Retrieve list of open POs for that vendor
4. Compare invoice details with open POs
5. If no matching PO found:
   - Notify vendor and buyer about missing PO

**Common Issues:**
- **Missing purchase account postings**: Verify PAM configuration is active for company code
- **Separate accounting documents not being created**: Check settings in Customizing under "Purchase Account Management"

## Common Issues and Solutions

### PO-Related Issues

1. **Invalid PO ID**
   - Verify for typographical errors
   - Contact procurement team for correct PO ID
   - Request a new valid PO if needed
   - Invoice remains on hold until valid PO is provided

2. **Non-matching PO Details**
   - Flag invoice for manual review
   - Contact vendor for corrected invoice
   - Consider partial approval for matching items
   - Escalate mismatched items for resolution

3. **Price Discrepancy Exceeding Tolerance**
   - Update PO price if invoice price is correct
   - Contact vendor for credit memo or new invoice
   - Force posting with appropriate authorization if variance is acceptable
   - Park document until resolution

### Invoice Status Issues

1. **"Verified as incorrect" Status**
   - Check error log (T-code MIR7) for specific error codes
   - For price mismatch: Adjust via T-code MIRO or escalate to Procurement
   - For missing GR: Verify in T-code MIGO and reprocess
   - Resubmit using T-code MRBR for background verification
   - Unresolved issues auto-park in holding bucket INV_HOLD_002 after 3 business days

2. **"Parked Released" Status**
   - Run T-code FB03 to identify errors
   - Update missing tax codes via T-code FTXP
   - Unlock GL account via T-code FS00
   - Retry workflow submission using T-code MRHR

3. **"Deleted" Status**
   - Deletion is irreversible in SAP/4HANA (v2022+)
   - Recreate manually using T-code MIRO with original data
   - Enable soft-delete flag INV_SOFT_DEL in Customizing for future protection

### Account Posting Issues

1. **Wrong G/L Account Posting**
   - Reverse with T-code MR8M
   - Check OBYC mapping for transaction key BSX
   - Run FAGLB03 to validate account assignments

2. **Missing Required Accounts**
   - Park invoice (T-code MIR7)
   - Create ticket for GL team (#MM-FI-001)
   - Verify OBYC → WRX configuration for material type

3. **Purchase Account Postings Missing**
   - Check PAM configuration: SPRO → MM → PAM → Company Code 1000
   - Verify materials have price control "V" (MAP materials)

4. **Separate Accounting Documents Not Created**
   - Verify settings in Customizing under "Purchase Account Management"
   - Check authorization settings and document number ranges

### Aggregation Issues

1. **Totals Mismatch**
   - Use T-code MIR6 → "Items" view to check line-item breakdown
   - Manually override if within ±2% tolerance (per policy FIN-POL-0042)
   - Force post with auth. object M_MSEG_WRG if critical (requires L2 approval)

2. **Custom Aggregation Requirements**
   - Configure in "Customizing for Logistics Invoice Verification"
   - Navigate to "Incoming Invoice → Aggregation → Maintain Variants"
   - Submit CR to IT using template CR_MM_008 for non-standard needs
   - Use user exit EXIT_SAPLV60B_001 for temporary fix

## System Transactions and Codes

- **MIR7**: Check error logs for verification issues
- **MIRO**: Adjust invoice details
- **MIGO**: Verify Goods Receipt
- **MRBR**: Requeue for background verification
- **FB03**: Diagnose parked document errors
- **FTXP**: Update tax codes
- **FS00**: Manage GL account locks
- **MRHR**: Retry workflow submission
- **MR8M**: Reverse incorrect postings
- **MIR6**: Check line-item breakdown for aggregation
- **SPRO**: Access system configuration settings

## Contact Information

For further assistance with invoice verification issues, contact:
- Support email: support@invoice.vpc.com
- Finance team ticket system: #MM-FI-001
