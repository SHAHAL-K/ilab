## Introduction

This guide outlines the standard procedures for invoice verification in the SAP system. Invoice verification is a crucial process that ensures all invoices are properly matched with their corresponding purchase orders and goods receipts, following the three-way matching principle. Proper verification helps maintain financial accuracy, prevent duplicate payments, and ensure compliance with company policies.

## Key Process Steps

### Does Invoice Have PO ID?

**Overview**: This decision point determines the subsequent processing path for the invoice by checking whether a valid Purchase Order (PO) ID is present.

**Process**:
1. Examine the invoice document for a PO reference number
2. Check common locations for PO ID:
   - Header section (labeled as "Purchase Order," "PO Number," "Our Order Reference")
   - Near vendor information
   - Line item details
   - Reference fields in the footer
3. For electronic invoices, check the designated PO ID field in the data structure
4. Document findings to determine next steps

**Decision Outcomes**:
- If PO ID is present: Proceed to "Retrieve PO from VIM using PO ID"
- If PO ID is missing: Proceed to "Retrieve vendor ID based on invoice" and then search for potential matching POs

**Special Considerations**:
- Certain categories may not require POs (utilities, rent, subscriptions under $1,000/year)
- Check vendor master data for "PO Required" indicator
- Capital expenditures (>$5,000) always require POs per company policy
- Consult "Non-PO Allowlist" for exceptions

### Retrieve PO ID from Invoice

**Overview**: This step involves locating and extracting the Purchase Order (PO) ID from the invoice document to enable subsequent validation.

**Process**:
1. Open the document in the VIM (Vendor Invoice Management) system
2. For electronic invoices, extract PO ID from the structured data
3. For scanned/paper invoices, check header, line items, and footer sections
4. Verify OCR-extracted PO ID against the image for accuracy
5. Standard SAP PO format is a 10-digit number, but formats may vary by vendor
6. Record the PO ID for use in subsequent validation steps

**Common PO ID Formats**:
- 10-digit numeric: 4500012345 (most common)
- With leading zeros: 0000004500012345
- With company code prefix: 1000-4500012345
- Special order types: Framework agreements (43xxxxxxxx), Service agreements (74xxxxxxxx)
- Legacy formats: Region-specific (US45-012345), Pre-migration format (OLDxxxxxxxx)

**Handling Special Cases**:
- Multiple PO references: Process as consolidated invoice or split the invoice
- Contract numbers instead of PO: Use transaction ME33K to verify and process accordingly
- Purchase requisition numbers: Check if converted to PO using transaction ME5A
- Missing PO: Search using alternative references (delivery note, requesting department)

### Retrieve PO from VIM using PO ID

**Overview**: This step involves accessing the Purchase Order details from the VIM system using the PO ID to validate the invoice against authorized procurement data.

**Process**:
1. Access PO data through transaction ME23N (Display Purchase Order)
2. Review PO header information:
   - Vendor details (should match invoice vendor)
   - PO creation date (should precede invoice date)
   - Payment and delivery terms
   - Currency information
3. Examine PO line items:
   - Material/service descriptions
   - Quantities ordered
   - Unit prices
   - Expected delivery dates
4. Check document flow for previous invoices or goods receipts
5. Verify PO status (open, partially delivered, blocked, etc.)

**Common Issues**:
- Blocked PO: Identify block reason and contact appropriate department for resolution
- Insufficient remaining quantity/value: Calculate shortage and request PO adjustment
- Price discrepancies: Compare invoice prices with PO prices and address differences
- Currency differences: Verify exchange rates and conversion calculations

### Retrieve Vendor ID Based on Invoice

**Overview**: This step identifies the vendor ID from the invoice document, which is critical when the PO ID is missing or for validating the correct vendor.

**Process**:
1. Open invoice document using transaction MIR4 (Display Invoice Document)
2. Navigate to header data section for vendor information
3. Locate vendor ID field (format: "Vendor: XXXXXXXX (Vendor Name)")
4. If not visible in header, check "Additional data" tab or use XK03
5. For electronic invoices, verify against metadata in EDI/XML file
6. Validate vendor ID is active and properly set up
7. Record vendor ID for subsequent processing

**Handling Special Cases**:
- Missing vendor ID: Check attachments, search by name (XK03), or tax ID (XKN1)
- Vendor not in system: Verify format, search alternatives, or initiate vendor onboarding
- Multiple potential vendor IDs: Compare tax ID, banking details, and address
- Subsidiary/branch of existing vendor: Check hierarchy (XK14) and determine if separate vendor ID needed

### Retrieve GR Based on Invoice

**Overview**: This step involves accessing the Goods Receipt document associated with the invoice to verify that goods/services were received before payment.

**Process**:
1. With invoice and PO information, open transaction MIGO (Display Goods Receipt)
2. Enter PO number and select document type "Goods Receipt"
3. Review GR list for matching line items and quantities
4. Verify GR date (should precede invoice date)
5. For partial deliveries, multiple GR documents may need consolidation
6. Record GR document number(s) for three-way matching

**Alternative Methods**:
- Use T-code MB03 to display material documents by PO number
- Use T-code ME23N, select PO, then use "GR/IR" button

**Common Issues**:
- No GR document found: Verify PO, contact receiving department, check service entry sheets
- GR quantity less than invoiced: Verify all GRs, process partial payment or request correction
- GR date after invoice date: Verify actual delivery date, address pre-invoicing issues
- Unit of measure differences: Check conversion factors (MEKA), calculate and verify
- Multiple GR documents: Use MB90 for comprehensive overview, sum quantities for comparison

## Common Issues and Solutions

### PO Issues
- **Format discrepancies**: Transform per standard rules (add zeros, remove prefixes)
- **PO blocked**: Identify block reason and follow appropriate resolution path
- **Insufficient quantity/value**: Calculate shortage and request adjustment
- **Price differences**: Compare and document discrepancies, request correction

### Vendor Issues
- **Vendor not in system**: Initiate onboarding or use one-time vendor code
- **Multiple vendor IDs**: Use tax ID, banking details for verification
- **Inactive vendor**: Check blocking indicators and validity dates

### GR Issues
- **Missing GR**: Verify delivery, check service entry sheets
- **Quantity mismatch**: Process partial payment or request correction
- **Date issues**: Verify actual delivery vs. posting date
- **UOM differences**: Apply standard conversion factors
