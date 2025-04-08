🔹 Scenario 1: Successful Match & Approval
Invoice ID: INV-1001
Vendor ID: VEND-2001
Step-by-Step:

Retrieve Invoice INV-1001

Item: Laptop

Qty: 10

Amount: $15,000

PO ID: PO-3001

Retrieve GR GR-4001 linked to INV-1001

Item: Laptop

Qty: 10

Retrieve PO PO-3001 from VIM

Vendor: VEND-2001

Item: Laptop

Qty: 10

Amount: $15,000

Match Invoice, PO, GR → ✅ Matched

Action: ✅ Invoice Approved

🔹 Scenario 2: Invalid PO
Invoice ID: INV-1002
Vendor ID: VEND-2002
Step-by-Step:

Retrieve Invoice INV-1002

Item: Printer

Qty: 2

Amount: $1,200

PO ID: PO-9999

Retrieve GR GR-4002 linked to INV-1002

Retrieve PO PO-9999 → ❌ PO Not Found in VIM

Action: ❌ Communicate to Vendor - Invalid PO ID

🔹 Scenario 3: Missing PO in Invoice, Match Found
Invoice ID: INV-1003
Vendor ID: VEND-2003
Step-by-Step:

Retrieve Invoice INV-1003

Item: Office Chair

Qty: 5

Amount: $750

PO ID: ❌ Missing

Retrieve GR GR-4003 linked to INV-1003

Retrieve all open POs from VIM for VEND-2003

PO-3002: Office Chair, Qty: 5, Amount: $750

PO-3003: Desk, Qty: 3

PO-3002 matches invoice → ✅ Match with GR

Action: ✅ Invoice Approved

🔹 Scenario 4: Missing PO in Invoice, No Match Found
Invoice ID: INV-1004
Vendor ID: VEND-2004
Step-by-Step:

Retrieve Invoice INV-1004

Item: Monitor

Qty: 4

Amount: $800

PO ID: ❌ Missing

Retrieve GR GR-4004 linked to INV-1004

Retrieve all open POs from VIM for VEND-2004

PO-3004: Keyboard, Qty: 10

PO-3005: Mouse, Qty: 15

❌ No PO matches invoice

Action: ❌ Communicate to Vendor - PO ID Missing or Invalid
