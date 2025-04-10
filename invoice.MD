
1
Parking Invoice Documents
1. To park a document, choose 
Logistics Invoice Verification   Document Entry   Park Invoice
.
2. The Park Invoice screen appears.
3. Enter the invoice data. It does not matter if:
Your entries are complete or incomplete
The balance of the document is zero or not
The system does not carry out any checks, as you can correct or add more information to a parked document later on.
4. Choose 
 to park the document.
Result
The system issues a message containing the document number created.
See also:
Processing Invoice Documents
Processing Invoice Documents
Calling Invoice Documents from the Worklist
Your worklist shows the invoice documents where you were the last person to change them. You can select the following
documents from the worklist by double-clicking them:
Held documents
Parked documents
Documents complete for posting
You can process them in the following ways:
Function
Description
Change
You want to change a parked document.
If you call a document from the worklist by double-clicking it, you
can change the document.
Save your changes by choosing:
 Note
In addition to entering the application Park Invoice directly, you can switch from the application Enter Invoice to document
parking. To do this, choose 
Edit   Switch to document parking
. When you do this, the data entered so far is retained. The
Park Invoice screen appears.
If you want to use a workflow to control the invoice verification process flow, see Parking: Complete Invoices for Posting (MM-
IV-LIV) for more information.

2
 Save parked document or
choose 
 Save as complete
Delete
You no longer want to use a parked document.
If you call a document from the worklist by double-clicking it, the
system displays the document in Change mode.
You can delete the document.
Choose 
Invoice document   Delete
 .
Post
You want to post a parked document.
If you call a document from the worklist by double-clicking it and it
is not subject to release, you can post the document directly.
Choose 
 Post .
Displaying Change Documents
For documents that you call from the worklist, you can display any change documents that exist. Choose 
Goto    Display Change
Documents
 . The system displays the following information:
Document number
Date
Time
Changed By
Entering Invoice Documents Directly
If you know the number of the invoice document that you want to process, you can enter this number directly and process the
corresponding document.
1. Choose 
 Other invoice document .
2. Enter the invoice document number and acknowledge your entry.
Update Allocations for Goods-Receipt-Based Invoice Verification
If you have already entered or changed quantities or amounts for invoice items, you can no longer change the allocation. Changed
values arise, for example, from different values in incoming invoices, and should be taken account of during verification.
Invoice receipt before goods receipt
If goods-receipt-based invoice verification has been defined for the transaction and no goods receipt has been posted yet, the
system does not proposed any items to be settled. If you park a document that is allocated to a purchase order item subject to
goods-receipt-based invoice verification and no goods receipt has been posted for this item yet, you can enter the allocation, even
without the proposed items.
When you subsequently call up the parked document from the worklist and a goods receipt has been posted in the meantime, the
system can find this goods receipt and proposed the corresponding items for settlement on the item list.
Choose 
 Update allocation to do this.
 Example
Updating the document item for subsequent goods receipts
4/10/25, 9:18 AM
3
Reversing Goods Receipts
You have already parked an invoice document for a document item. Later, the goods receipt for this invoice document is reversed.
In order to remove the document from your worklist, you can delete the parked document. To do this, choose 
Invoice document 
 Delete
 .
Update Allocations for Purchase-Order-Based Invoice Verification
For purchase-order-based invoice verification, the quantities and values for parked documents are no longer changed using the
function Update allocation . The accounts payable clerk can verify the invoice using the purchase order history. If the invoice
quantity is larger than the quantity of goods received, and you still try to post the document, the invoice is blocked for payment.
Controlling Invoice Document Processing Using Workflow
If you want to use a workflow to control the invoice verification process flow, see Parking: Release of Invoices Completed for
Posting (MM-IV-LIV) for more information.
Prepayment
Use
 Example
Updating the document items for reversed goods receipts
4/10/25, 9:18 AM
4
You use prepayment for vendors with whom you have built up good business relations over a longer period of time. This approach
benefits both parties:
The vendor receives prompt payment after issuing an invoice.
As the ship-to party, you can make optimum use of payment targets, as the system pays the invoice independently of the
corresponding goods receipt and the invoice check.
You should only use prepayment if you have built up a business relationship good enough to ensure that you are paid back any
unauthorized prepayments.
The standard functions in logistics invoice verification are not affected by prepayment, as the only difference is that payment is
performed at an earlier date. The system continues to perform standard functions (with restrictions) such as checks and FI
postings (after goods receipt). For more information, see Constraints below.
For each company code, you can define in the vendor master whether prepayment is required, is possible, or is not permitted.
Prepayment has the following characteristics:
A vendor item is created and an invoice is paid, independently of the corresponding goods receipt and the invoice check.
Payment of an expense invoice is triggered when the invoice is entered.
The posting date of the invoice document is used as the posting date for the prepayment document.
You can use the SET_POSTING_DATE method in BAdI WRF_PREPAY_INVOICE to change the posting date, for example,
to the current system date, or the posting date of the invoice document.
Relevant invoice amounts for prepayment of the invoice are transferred to Financial Accounting (SAP FI).
The prepaid invoice is checked at a later date.
The inclusion of a clearing account for prepayment. The system clears this after invoice verification and the corresponding
FI posting have been carried out.
Restrictions
If you use prepayment with logistics invoice verification, the system can only determine approximate solutions for the
following closing settlements:
Month-end closing
Year-end closing
Closing at profit center or segment level
The system does not take invoice items into account for prepayment, only the invoice header and taxes.
A breakdown by individual item is required for a specific statement, however. You can get round this constraint by
manually reclassifying or clearing individual invoice items in the prepayment clearing account in consultation with
your external auditor.
 Note
An invoice reduction is still possible as the result of a check.
 Note
Note the following technical constraints:
4/10/25, 9:18 AM
5
You must check customer-specific substitutions or validations in Financial Accounting or Controlling and adjust them if
necessary.
There are no invoice items available for prepayment. The system does not derive a business area for vendor line items if
business area balances are active. The business area must be entered manually.
If you use the new general ledger, the following constraint applies for the account assignment of the prepayment clearing
items: Since no items are known for an entered invoice at the time of prepayment, only an approximate solution is possible.
There are two account assignment options for profit centers:
The system posts prepayment clearing account postings to a dummy profit center. You define the dummy profit
center in Customizing.
The system distributes the amount to be posted to the prepayment clearing account to all profit centers, weighted
according to the purchase order item amount. The system determines profit centers from the purchase order items
assigned to the invoice.
The system cannot avoid discrepancies or incorrect distribution of the values to profit centers (for example, if
different profit centers are determined during invoice verification to those determined in prepayment). They cannot
be corrected.
The system cannot distribute follow-up costs (such as exchange rate differences, cash discounts, and so on) to the
original CO objects by adjusting the profit and loss statement. The system does not support this function in the
context of prepayment.
You cannot use prepayment in the following circumstances:
For credit notes or subsequent credits (only for invoices)
In connection with the American tax jurisdiction code
In connection with import sales/purchase tax or acquisition tax
For one-time vendors
For invoices in which the cash discount base amount is not the same as the tax base amount
Depending on your Customizing settings, you can change the invoice amount, the taxes, the reference (because of the FI
assignment), and the invoicing party for a prepaid invoice. In this way, you can change important header data even after the
invoice has been saved and the prepayment document has been posted. In this case, the system creates a credit memo in
the background with the old invoice values (the equivalent of canceling the original document) and also creates a
prepayment document with the new invoice values.
Invoice verification is not performed when prepayment is made. The system does not identify variances in the invoice
compared with the purchase order or the goods receipt. When prepayment is used, the system does not set an automatic
payment block in line with the tolerance limits that you set in Customizing.
The system updates the fields on the Payment tab page when a non-prepaid invoice is posted, for example, the payment
conditions are read or a payment block is set. The updated data is only transferred to the invoice document for a prepaid
invoice if the relevant field is allowed to be changed according to the Customizing settings.
If you subsequently change an invoice document manually in distributed systems (if data has been entered incorrectly, for
example), the system cancels the prepayment document and creates a new one.
 Note
Note that frequent changes to header data can produce a large number of FI documents, resulting in an unmanageable
number of items in Accounts Payable Accounting. Discuss this with your external auditor in advance.
4/10/25, 9:18 AM
6
You cannot use prepayment with material ledgers. We recommend that you customize the system so prepayment is not
allowed for company codes to which plants with active material ledger are assigned.
Exchange rate differences arise if the exchange rate in the logistics invoice document changes between prepayment and
invoice posting.When it posts the invoice, the system does not post exchange rate differences for prepayment. If exchange
rate differences arise, the system posts them when it clears the open items on the prepayment clearing account.
There can be differences due to exchange rate rounding in local or foreign currency for postings at document level.The
system usually assigns the rounding differences to the vendor line item in logistics invoice verification. Due to prepayment,
the vendor line item has already been posted in a separate document. Any differences in the local currency or document
currency remain on the prepayment clearing account and must be written off using FI methods (such as clearing open
items).
Prerequisites
Prepayment requires invoices that you enter using logistics invoice entry.
In a background process
Using BAPI BAPI_INCOMINGVOICE_SAVE or BAPI_INCOMINGINVOICE_PARK
Using EDI
By parking (preliminary entry of) incoming invoices
The prepayment clearing account must be created in the local currency as a balance sheet account that, like the goods
receipt/invoice receipt clearing account, only allows automatic postings and is stored in account determination.
The system must group and assign the open items during the clearing process. You must make sure that a suitable sort key
is stored in the account master. You can customize the system so that the reference key is transferred to the Assignment of
Prepayment Allocation Item field. When the system clears open items, it groups and assigns them on the prepayment
clearing account, according to the relevant MM invoice.
MM invoice documents can only be prepaid if you have made company-code-specific Customizing settings for the main
company code. You make settings to control prepayment in Customizing for logistics invoice verification by choosing 
Incoming Invoice   Prepayment   Configure Control of Prepayment at Company Code Level
.
To allow the system to post taxes during prepayment, you must enter the taxes in the header for each tax rate when you
enter an invoice manually.
EDI invoices must contain the tax for each tax rate at IDoc header level.
You must customize fields that you want to change subsequently in prepaid invoices, for example, the Invoice Amount, Tax,
Reference (FI assignment), or the Invoicing Party. You do this in Customizing for logistics invoice verification by choosing
Incoming Invoice   Prepayment   Configure Field Control for Prepayment
.
For invoice reduction, you must have activated Tax Reduction in Complaint Document. The system posts the taxes in the
FI invoice reduction document and not in the FI invoice document.
 Note
The system only performs prepayment if your settings allow it for both the company code and the vendor.
 Note
If, for example, the IDoc contains invoice items for the tax rates 16% and 7%, the IDoc must contain a segment with the
tax rate 16% and a segment with the tax rate 7%.
4/10/25, 9:18 AM
7
Process
The standard procedure for invoice verification with prepayment of an expense invoice involves the following steps:
1. Entering invoices and posting the prepayment document.
2. Paying the invoice in SAP Financial Accounting (SAP FI).
3. Posting prepaid logistics invoices.
The order in which invoice verification procedure takes place can vary: Payment of the invoice can take place in FI or after
prepaid logistics invoices have been posted.
Changes to a prepaid invoice document
If the payment run has not yet been performed and a document cancellation is possible, the system cancels the prepayment
document. Otherwise, the system creates a credit memo for the amount in the prepayment document.
If the Customizing settings for prepayment allow field changes in invoice documents, you can change a specific field in an entered,
prepaid invoice document. This Customizing setting means that the field in the invoice is ready for input. If this field can also be
changed in the FI prepayment document, the system changes the existing prepayment document when it saves it. Otherwise, the
system cancels the prepayment document and creates it again.
If the Customizing settings for prepayment do not allow fields to be changed, you must delete the logistics invoice and create it
again. If you delete a prepaid invoice, the system also cancels the prepaid FI invoice.
Result
Depending on the Customizing settings, the system performs prepayment automatically by creating an additional posting
document. The system creates open items on the vendor account as part of logistics invoice verification, and posts the payables
with taxes before checking the corresponding invoices. The system stores the prepaid invoice with the relevant status, for example,
Scheduled for Background Check or Parked in logistics invoice verification. You can further process the invoice in logistics invoice
verification, however, only limited changes can be made to the header fields.
Entering Invoices
Use
Before the system is able to begin prepayment, you must have entered the logistics invoices in the system. There are three ways of
entering invoices:
You can enter them manually for the background check.
You can park them, in which case they are known as parked invoices .
They can be entered automatically (using Electronic Data Exchange (EDI) or BAPIs).
After you have saved a logistics invoice, the system simultaneously creates a logistics invoice document (MM document) based on
your Customizing settings and a prepayment document (FI invoice).
 Note
Invoice payment is a standard function in SAP FI. When an invoice is due, the system processes the open vendor item in
SAP FI and expands it.
4/10/25, 9:18 AM
8
Integration
Prepayment can be performed for parked logistics invoices and invoices that are entered using EDI, or logistics invoice entry for
the background process.
Prepayment is not required for evaluated receipt settlement (ERS) or consignment settlement, since the invoices are created
automatically by the system in these cases and transferred directly to Financial Accounting (FI).
Prerequisites
To enable the system to take account of invoices from a vendor when performing prepayment, you must have made settings in
company-code-specific Customizing and for the Prepayment Relevance field in the vendor master.
Features
When a logistics invoice entry is made, the system transfers payment-relevant data to Financial Accounting. The system creates
the relevant prepayment document in SAP FI as an FI invoice.
In Financial Accounting, the system posts the payment-relevant data to a clearing account for the prepayment and creates an
open vendor item.
Activities
You carry out the following steps when you enter invoices in the system:
1. Specify taxes
2. Set Change Prepayment Status indicator
3. Calculate cash discount
 Note
One of the steps required to enter an invoice is entering (manually) the taxes that the system has to post.
For invoices with several tax rates, you must have entered tax amounts for each rate. If there are several tax rates, the
system makes a posting for each one to the Clearing Account for Prepayment .
You can only use the Calculate Taxes function with prepayment if the invoice contains one tax indicator only.
 Note
If you set the attribute for the company code and the vendor to Prepayment Requested or Prepayment Possible in
Customizing, the user can change the prepayment status manually and therefore determine whether or not the system
should prepay an invoice.
It is possible to override the prepayment status using the PREPAYMENT_RELEVANCE_CHANGE method in the
WRF_PREPAY_INVOICE BAdI.
 Caution
If the cash discount base amount is different from the tax base amount, you must enter the cash discount base amount
manually for each tax rate. This is not possible in SAP FI, however. The system therefore posts the wrong cash discount
base amount. Note that there is a Cash Discount Base Amount field in SAP FI, but it cannot be used by invoice
verification.If you want to enter one or more cash discount base amounts, you must make customer-specific
modifications in SAP FI. Alternatively, you can arrange with your vendor to split the invoice into two separate invoices:
4/10/25, 9:18 AM
9
4. Perform FI assignment
We recommend that you always enter the external vendor invoice number in the Reference field in the logistics invoice. Based on
the Reference field and if the Customizing settings are appropriate, the system performs automatic FI clearing of the prepayment
document and the payment.
1. Post prepayment document
If the prepayment document cannot be posted despite a request, the system generates a customizable message when it
saves the data. This message contains a reference to the message log.
The logistics invoice document can still be saved even if creating the prepayment document has been unsuccessful.
Posting Prepaid Logistics Invoices
Use
To complete the invoicing procedure, the system must post the prepaid logistics invoice.
A prepaid invoice is not paid again after it is posted. The system prevents a multiple payment by not creating any further vendor or
tax postings when it posts the invoice. Instead, the system clears the internal clearing account for prepayment.
Activities
You check the invoice in the same way as for Invoice Verification in the Background or for parked invoices.
After the system posts logistics invoices that have been checked and found to be correct it:
Creates FI documents
Creates an offsetting entry on the internal clearing account for prepayment
Updates the goods receipt/invoice receipt account.
In contrast to logistics invoice verification without prepayment, the system does not make a vendor posting or an input tax
posting.
One invoice with cash-discount-relevant items
One invoice with non cash-discount-relevant items
 Recommendation
 Note
4/10/25, 9:18 AM
10
You make Customizing settings to determine if you can change tax fields once the system has created the prepayment document.
If you have allowed subsequent changes to tax fields, the system cancels the relevant prepayment document and posts it again. If
you have not allowed subsequent changes to the tax fields and the system has already created the prepayment document, you can
no longer correct tax fields.
Entering Invoices for Invoice Verification in the Background
Post
1. Choose 
Logistics Invoice Verification   Document Entry    Enter Invoice for Invoice Verification in Background.
2. Enter the header data as required and match up the invoice.
3. Choose 
 Post .
The system creates an invoice document containing the header data. The invoice is saved for invoice verification in the
background.
You can process the invoice further using the Invoice Overview function.
Hold
1. Choose 
Logistics Invoice Verification   Document Entry    Enter Invoice for Invoice Verification in Background.
2. Enter the header data as required and match up the invoice. However, this information does not have to be complete.
3. Choose Hold .
You save the invoice in its current status. The system creates an invoice document containing the header data. The invoice
document is not verified. These invoice documents are not flagged with a traffic light icon on the Invoice Overview .
You can only process the invoice further using the Invoice Overview function.
Invoice Overview
Use
You use this function to generate a list of invoices, for example, to check which documents were posted in the background or which
were not posted and therefore have to be processed manually.
Features
Selection Criteria
You can use numerous selection criteria to narrow down the list of invoices selected, including:
 Note
You can convert invoice documents that were posted or held in releases earlier than Release 4.6C using the function 
Schedule background verification . In the list, select the column for Schedule background verification and choose the symbol
 in the list of invoices. Only those invoices are converted that have already been assigned items.
4/10/25, 9:18 AM
11
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
When it was last verified
If the invoice contains items with unclarified errors or vendor errors
If the invoice is scheduled for background verification
If there is an error log for the invoices
The origin of the invoice document
The document type
Document date
Posting date
The document header text
4/10/25, 9:18 AM
12
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
Invoice Status
Definition
Information about the processing status of an invoice.
The following table explains the meaning of all the existing statuses:
 Note
You can only process held documents created using transaction Enter Invoice for Verification in the Background , using the
Invoice Overview . These documents are not displayed in the Worklist under the node Held Documents in the transactions
Enter Invoice or Park Invoice .
Documents that contain errors and that were transmitted via EDI can also only be displayed using the Invoice Overview
transaction.
4/10/25, 9:18 AM
13
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
The invoice was verified in the background as being correct and the
status was manually changed later on.
Deleted
If you have parked an invoice or have scheduled it for background
processsing, or if the invoice was verified in the background and
contains errors, then you can flag the document with the status
Deleted . This also applies to documents containing errors via EDI.
During deletion, the invoice document header is always retained,
but you can no longer access the document.
4/10/25, 9:18 AM
14
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
4/10/25, 9:18 AM
15
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
If you do not enter a value for the parameter, you must enter the values for quantities and amounts manually.
Activities
1. Choose 
User profile     Own data
 .
2. Choose the Parameters tab page and enter IVAMOUNTADJUST in the Parameter column.
3. If you want the system to perform automatic amount correction, enter X in the Value column.
 Note
If an invoice was verified in the background as incorrect, you can set the invoice to Invoice Verification in background again to
have the system verify it again. You would do this, for example, if you had not yet entered the delivery to which the invoice
refers.
4/10/25, 9:18 AM
16
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
In the case of variances in the totals lines specified in the vendor invoices, you can branch to the item list of the aggregated lines
and change the quantities and amounts, if necessary. After you have changed the invoice items and hidden the item list, the
 Example
A delivery note details deliveries to different plants, you can expand the aggregated lines for the delivery note via Plants and
check the aggregation lines displayed for the delivery note and the plant respectively.
4/10/25, 9:18 AM
17
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
1. Enter your selection criteria.
The system displays the list of invoice documents.
1. Choose the invoice document to be deleted by choosing the icon 
 Change .
2. The Logistics Invoice Verification screen appears and the system displays the invoice document.
3. Choose 
Invoice document   Delete
 .
4/10/25, 9:18 AM
18
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
When you post an invoice, the system updates various accounts in Financial Accounting. It determines automatically which
amounts have to be posted to which accounts.
Account assignment is based partly on your entries when you enter an invoice, partly on information stored in the system and
partly on the system settings.
Prerequisites
The system administration must define and configure the accounts in the chart of accounts when implementing the ERP system in
your company.
4/10/25, 9:18 AM
19
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
4/10/25, 9:18 AM
20
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

