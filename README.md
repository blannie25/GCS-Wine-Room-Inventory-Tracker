# GCS-Wine-Room-Inventory-Tracker
keeping track of the wines in the GCS Wine Room
We can build a surprisingly powerful QR-based item tracking system using just Microsoft Forms, Microsoft Lists, and Microsoft Power Automate—no scanners needed. The key idea: use phones to scan QR codes → open a form → log activity → update a master list automatically.
Here’s a clean, real-world setup you can implement quickly:
⸻
🧩 SYSTEM OVERVIEW
Flow:
1. Generate QR codes for each item (or case/pallet)
2. User scans QR with phone camera
3. QR opens a pre-filled Microsoft Form
4. User selects action (Received, Picked, Moved, etc.)
5. Submission logs to Microsoft List
6. Power Automate updates item status + history
⸻
⚙️ STEP 1: CREATE YOUR MASTER TRACKING LIST
In Microsoft Lists, create a list like:
List Name: Inventory Tracker
Columns:
• Item ID (Single line text)
• Description
• Location
• Status (Choice: In Stock, Picked, Shipped, Hold, etc.)
• Last Updated (Date/Time)
• Last Action By
• Notes
👉 This is your single source of truth
⸻
📱 STEP 2: BUILD THE FORM (SCAN ENTRY POINT)
In Microsoft Forms, create a form like:
Form Name: Inventory Scan Log
Fields:
• Item ID (important)
• Action (Received / Move / Pick / Ship / Adjust)
• Location
• Notes
• Optional: Photo upload (for proof)
🔑 KEY TRICK:
Use pre-filled URLs so the QR code already contains the Item ID
Example:
https://forms.office.com/...&ItemID=VB031124
So when scanned:
👉 User doesn’t type anything → just selects action and submits
⸻
🔳 STEP 3: GENERATE QR CODES (NO SCANNER NEEDED)
For each item:
• Use Excel or an online QR generator
• Encode the pre-filled Form URL
You can even bulk generate via Excel:
• Column A: Item ID
• Column B: Form URL + Item ID
• Use QR generator add-in or export
Print labels → stick on:
• Cases
• Pallets
• Shelves
• Bins
👉 Any smartphone camera can scan → no hardware cost
⸻
⚡ STEP 4: AUTOMATE WITH POWER AUTOMATE
In Power Automate, create a flow:
Trigger:
• “When a new response is submitted” (Microsoft Forms)
Actions:
1. Get response details
2. Find item in Microsoft Lists (match Item ID)
3. Update item:
• Status = based on Action
• Location = submitted value
• Last Updated = now
• Last Action By = responder
4. (Optional) Append to History Log list
⸻
🧾 BONUS: CREATE A HISTORY LOG (HIGHLY RECOMMENDED)
Create a second List:
List Name: Inventory History
Columns:
• Item ID
• Action
• Location
• Timestamp
• User
• Notes
👉 Every scan = permanent audit trail
⸻
🧠 HOW THIS REPLACES SCANNERS
Instead of:
❌ Dedicated barcode scanners
❌ Expensive WMS
You use:
✅ Phone camera (native QR scan)
✅ Form auto-fill
✅ Cloud logging
⸻
🚀 ADVANCED FEATURES (WORTH ADDING)
1. Location QR Codes
• Put QR codes on shelves/bins
• Scan item → then scan location
2. Conditional logic in Forms
• If “Move” → require Location
• If “Damage” → require photo
3. Notifications
• Auto-email or Teams alert when:
• Item shipped
• Item moved to wrong location
• Low inventory
4. Dashboard
• Use Power BI connected to Microsoft Lists
• Live inventory + movement tracking
⸻
🧱 SIMPLE EXAMPLE FLOW
1. Warehouse worker scans case QR
2. Form opens: Item ID already filled
3. Selects: “Picked”
4. Submits
5. Power Automate:
• Updates status → “Picked”
• Logs timestamp
• Saves user
Done in ~5 seconds per scan
⸻
⚠️ COMMON PITFALLS (AVOID THESE)
• ❌ Not using pre-filled forms → slows everything down
• ❌ No unique Item IDs → breaks automation
• ❌ Overcomplicating status logic early
• ❌ Not logging history (you’ll regret it later)
⸻
🏁 WHAT YOU END UP WITH
• Real-time inventory tracking
• Full audit trail
• Zero hardware cost
• Scalable system using tools you already have
⸻
