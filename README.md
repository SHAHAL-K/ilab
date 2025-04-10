Invoice Overview
Use
You use this function to generate a list of invoices, for example, to check which documents were posted in the background or which
were not posted and therefore have to be processed manually.
Features
Selection Criteria
You can use numerous selection criteria to narrow down the list of invoices selected, including:
Document number
Document type
Reference
Document header text
Fiscal year
Processor
Invoicing Party
Posting and document date
Invoice Status
You can select posted invoices, and can display invoices in the invoice overview that
were created using BAPIs
were created via evaluated receipt settlement (ERS)
were created using invoicing plan settlement
cancel another document
have been parked
You can also select and process parked and held invoices that have the following statuses:
Held
Parked
Parked as Complete
List of Invoice Documents
The list of invoice documents contains various information, including:
If the invoice was posted
4/10/25, 6:26 AM
2
When it was last verified
If the invoice contains items with unclarified errors or vendor errors
If the invoice is scheduled for background verification
If there is an error log for the invoices
The origin of the invoice document
The document type
Document date
Posting date
The document header text
You can go from the list to the individual documents that have not been verified or have been verified as containing errors and
process them manually. You can process the documents in the same way as in the application Enter Invoice by double-clicking the
document number.
Activities
1. Choose 
Logistics Invoice Verification   Further Processing    Invoice Overview
 .
2. Enter selection criteria as required.
3. Choose 
 Display.
The system displays the list of invoice documents.
See also:
Invoice Status
Processing Invoices Following Background Verification
Aggregation
Deleting Invoice Documents
Changing Invoice Documents
Invoice Verification Online
 Note
You can only process held documents created using transaction Enter Invoice for Verification in the Background , using the
Invoice Overview . These documents are not displayed in the Worklist under the node Held Documents in the transactions
Enter Invoice or Park Invoice .
Documents that contain errors and that were transmitted via EDI can also only be displayed using the Invoice Overview
transaction.
4/10/25, 6:26 AM
3
Invoice Status
Definition
Information about the processing status of an invoice.
The following table explains the meaning of all the existing statuses:
Status
Meaning
Held (Held Parked, Held Entered)
The current status of the document was saved. Only minimal
checks were performed, for example, to check if the company code
exists. No updates to Financial Accounting were performed. You
can use the status to differentiate between invoices that have been
held and parked or held and entered . This applies dependent on
whether you have held the invoices from the transaction Hold
Invoice or Enter Invoice .
Parked
The invoice document is missing some information that is required
for posting. The balance might not be zero.
The preliminary checks and updates were performed, such as the
informative purchase order history, data for advance tax returns,
and logs of document changes.
Parked Released
If a completely parked document cannot be posted at the time of
release in the workflow, the document receives the status parked
released . Afterwards, you can process the document as you would
any other completely parked document, both online as well as in
the workflow.
Parked as Complete
No more changes should be made to the invoice document.
The balance is zero. The invoice document is flagged for posting
but has not yet been posted.
Planned for background verification
The invoice is to be verified in the background.
The invoice was saved online using the application Enter Invoice
for invoice Verification in the Background or an older invoice
document from an earlier release was converted.
Verified as incorrect
During invoice verification in the background, the system has noted
differences that are too large.
During invoice verification in the background, a system error
occurred, for example, some system settings are missing. No
updates are made into Financial Accounting.
The invoice was held online using the application Enter Invoice for
Invoice Verification in the Background (no verification)
Correct (posted, not completed)
The invoice was successfully posted using Invoice Verification in
the background.
You can use this status to differentiate between invoices posted
online and those posted in the background (see status Posted ).
Posted
The invoice was posted online.
4/10/25, 6:26 AM
4
Status
Meaning
The invoice was verified in the background as being correct and the
status was manually changed later on.
Deleted
If you have parked an invoice or have scheduled it for background
processsing, or if the invoice was verified in the background and
contains errors, then you can flag the document with the status
Deleted . This also applies to documents containing errors via EDI.
During deletion, the invoice document header is always retained,
but you can no longer access the document.
In Customizing for Logistics Invoice Verification , you can configure the system so that invoices successfully posted in the
background are given the status Posted immediately. To do this, choose 
Invoice Verification in the Background   Define
Automatic Status Change
 .
Processing Invoices Following Background Verification
Use
If invoices contain errors or were held or saved in the application Enter Invoice for Invoice Verification in the Background , you
must process them manually so that the system can post them.
Prerequisites
You use the Invoice overview to generate a list of invoices verified as containing errors and of those not verified.
Features
From the list of invoice documents, you can go directly back to the selection screen by choosing 
 New selection , to choose
different invoice documents.
If you have already corrected invoice documents that contain errors and go back to the list to continue processing, you can update
the list of invoice documents by choosing 
 Refresh .
If the following symbols are active on the invoice document rows, you can call up the corresponding function by choosing the
symbol.
Symbol and Function
Description
 Display items
You can display header data, vendor data, and item data for the
invoice document (in the same way as in the application Enter
Invoice ), for example, unplanned delivery costs and the PO
structure.
 Change items
You can change the items (in the same way as in the application
Enter Invoice ), for example, the quantity, the amount, or the tax
code of incorrect invoices.
 Change Allocation Criteria
You can change the allocation criteria for invoices containing errors
(in the same way as in the application Enter Invoice ), for example,
4/10/25, 6:26 AM
5
This is custom documentation. For more information, please visit SAP Help Portal.
you can change an incorrect order number or add an additional
allocation.
 Display error log
The messages collected notify you of the causes of the errors that
occurred and how to proceed.
 Quantity comparison: goods receipt - delivery note
Differences can occur between the quantity of the actual goods
receipt and the goods receipt noted by the vendor on the delivery
note. You can filter invoice items containing such differences out of
the invoices selected.
 Unclarified errors
You can filter the display of the invoices selected by unclarified
errors. The system only includes invoice items containing
unclarified errors in the item list.
 Display follow-on documents
You can display follow-on documents, for example, accounting
documents.
 Checked
You can set invoice documents that were successfully posted in the
background to status Completed .
 Schedule for background verification
You can schedule the invoice document for verification in the
background. The invoice documents are then verified using report
RMBABG00.
See also:
Automatic Amount Correction
Automatic Amount Correction
Use
When quantity changes occur, you can perform automatic correction of an item amount using the user parameter
IVAMOUNTADJUST. You can use the automatic amount correction in the following transactions, for example, if you often enter
partial invoices:
Enter Invoice (MIRO)
Park Invoice (MIR7)
Invoice Overview (MIR6)
Features
If you enter the value X for the parameter, automatic amount correction takes place. This means that if you change the quantity of
an invoice item and then choose Enter , the system automatically calculates the new item amount. If you have already entered the
quantity and item amount manually, and you change the quantity afterwards, the system does not calculate the amount again.
 Note
If an invoice was verified in the background as incorrect, you can set the invoice to Invoice Verification in background again to
have the system verify it again. You would do this, for example, if you had not yet entered the delivery to which the invoice
refers.
4/10/25, 6:26 AM
6
If you do not enter a value for the parameter, you must enter the values for quantities and amounts manually.
Activities
1. Choose 
User profile     Own data
 .
2. Choose the Parameters tab page and enter IVAMOUNTADJUST in the Parameter column.
3. If you want the system to perform automatic amount correction, enter X in the Value column.
4. Save your entries.
Aggregation
Use
You can aggregate several invoice items of an invoice. That means that the invoice items are grouped together for display as a
single line, depending on the aggregation criterion used. This allows you to considerably reduce the work involved in checking the
invoice or searching for variances.
You have received vendor invoices containing several invoice items and totals lines for each purchase order, delivery note, material,
or plant.
Prerequisites
Function
Setting in Customizing for Logistics Invoice Verification
Define appropriate variants for aggregation.
Incoming Invoice     Aggregation     Maintain Variants for
Aggregation List
Maintain additional aggregation criteria for each aggregation
variant.
Incoming Invoice     Aggregation     Preset Aggregation Criteria
Integration
You can call the aggregation function from the list of invoice documents on the Invoice Overview and using the display variant on
the item list in the applications Invoice Overview and Enter Invoice .
Features
You can only use the following criteria to aggregate invoices containing errors:
Aggregation: Delivery Note
Aggregation: Purchase Order
Aggregation: Material
Aggregation: Plant
After choosing the aggregation, you go to further processing of the invoice document on a screen analog to that used in the
application Enter Invoice . Here you can expand the aggregated lines according to your requirements. You can maintain your
personal criteria in Customizing for Logistics Invoice Verification:
7
In the case of variances in the totals lines specified in the vendor invoices, you can branch to the item list of the aggregated lines
and change the quantities and amounts, if necessary. After you have changed the invoice items and hidden the item list, the
system updates the values according to the items changed.
Activities
1. Choose 
Logistics Invoice Verification   Further Processing    Invoice Overview
 .
2. Enter selections as required.
3. Choose 
 Display.
4. The system displays the list of invoice documents selected.
5. Aggregate the invoice document required by choosing the aggregation criterion on the row containing the document to be
verified.
6. A screen analog to that in the application Enter Invoice appears displaying the aggregated lines.
7. Compare the amounts with the totals lines specified on the vendor invoices.
8. If you find variances and want to enter other quantities or values, choose 
 Items .
9. The Edit Item List screen appears.
10. Make the changes.
11. When you have changed the items, choose Hide item list . The system updates the values in the aggregated rows.
12. Choose 
 Post .
See also:
Invoice Item
Deleting Invoice Documents
Use
You want to delete an invoice document that is posted in the background or that you did not want verified at the time.
Prerequisites
The invoice has not been posted yet.
Procedure
1. Choose 
Logistics Invoice Verification   Further Processing    Invoice Overview
 .
 Example
A delivery note details deliveries to different plants, you can expand the aggregated lines for the delivery note via Plants and
check the aggregation lines displayed for the delivery note and the plant respectively.
8
1. Enter your selection criteria.
The system displays the list of invoice documents.
1. Choose the invoice document to be deleted by choosing the icon 
 Change .
2. The Logistics Invoice Verification screen appears and the system displays the invoice document.
3. Choose 
Invoice document   Delete
 .
Result
The system deletes the invoice document. A message appears indicating that the document was deleted.
Changing Invoice Documents
Use
If you entered an invoice for verification in the background or which you did not want verified at the time, you can change the
invoice.
Procedure
1. Choose 
Logistics Invoice Verification   Further Processing   Invoice Overview
.
2. Enter your selection criteria.
The system displays the list of invoice documents.
3. Choose the invoice document to be processed by choosing the icon 
.
The Logistics Invoice Verification screen appears and the system displays the invoice document.
4. Enter your changes and choose:
Symbol/Menu
Function
Hold
The current invoice document data is saved and you can further
process the invoice document later.
The invoice document is posted.
Schedule for background verification
The invoice is scheduled for background verification
Edit   Accept difference and post
For more information, see Posting Total-Based Differences.
The difference in the invoice document is accepted and posted.
This can save you time and effort searching for variances in mass
data.
Account Determination
Use
4/10/25, 6:26 AM
9
When you post an invoice, the system updates various accounts in Financial Accounting. It determines automatically which
amounts have to be posted to which accounts.
Account assignment is based partly on your entries when you enter an invoice, partly on information stored in the system and
partly on the system settings.
Prerequisites
The system administration must define and configure the accounts in the chart of accounts when implementing the ERP system in
your company.
Features
Your entries provide the following information:
Which vendor account must be posted to?
Which amounts must be posted?
The material master record provides the following information:
Which valuation class does the material belong to?
Which type of price control is required for the material?
Which account must be posted to for the material?
Is the stock available smaller than the quantity invoiced?
Posted documents provide the following information:
What is the purchase order price?
Has a goods receipt been posted for the purchase order?
The system settings provide the following information:
Is the invoice posted as a net or a gross amount?
Which G/L accounts must be posted to?
See also:
Important Accounts for Invoice Verification
Purchase Account Management
Posting Small Differences
Purchase Account Management
Use
Some countries require companies to manage purchase accounts. This account documents the value that externally procured
materials are posted at.
4/10/25, 6:26 AM
10
Prerequisites
Function
Customizing Setting
Define whether purchase account management is active for the
company code.
Materials Management     Valuation and Account Assignment  
  Account Determination     Account Determination Without
Wizard     Purchase Account Management     Activate Purchase
Account in Company Code
Define the value calculation that applies to the purchase account.
Purchase Account Management     Calculation of Value for
Purchase Account
Define whether the system is to create separate accounting
documents for the purchase account postings.
Purchase Account Management     Separate Accounting
Document for Purchase Account Postings
Create the appropriate accounts.
Materials Management    Invoice Verification     Logistics
Invoice Verification     Incoming Invoice Configure Automatic
Postings
Features
Purchase accounts can be updated in the following ways:
At the receipt value
In this case, the exact amount posted at goods receipt to the GR/IR clearing account is posted to the purchase account.
In Invoice Verification, the system only posts to the purchase account if there is a price difference. The system posts this difference
to the stock account or to a price difference account, the sum of these two postings is posted to the purchase account.
For more information, see Postings at Receipt Value .
At the stock value
In this case, the exact amount posted at goods receipt or at invoice receipt is posted to the purchase account.
In Invoice Verification, the system only posts to the stock account – and therefore to the purchase account and to the purchase
offsetting account – if the invoice item meets the following conditions (see Price Variance ):
A price variance has occurred
The material is subject to moving average price control
Stock exists for the material
For more information, see Postings at Stock Value .
Similar to the purchase account, a freight account exists for documenting delivery costs that have been posted for externally
procured materials.
If purchase account management is active, the system automatically carries out the additional postings.
Constraints
For settlements of subcontracting transactions, the system does not post to the purchase account nor to the purchase offsetting
account. For further information, see Subcontracting in Invoice Verification .
