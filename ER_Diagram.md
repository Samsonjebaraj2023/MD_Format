# ER Flow Diagram

## Payment Flow Diagram

- **USERS** initiate payments
- **PAYMENTS** are recorded and if status = `COMPLETED` then it linked to **STUDENTPAYMENTS**
- **PAYMENTS** generate corresponding **INVOICES**

(**Note** : If Payment is not completed (Started or Failed) then it will stores in payments table)

The Below diagram shows the key relationships in the purchase process:

1. A Student can make multiple payments
2. Each payment can create a student payment record
3. Each payment can generate an invoice

![Payment Diagarm](payment.png)
-----------------------------------------------------------

## Session/Slot Flow Diagram

- **SESSIONS** can have multiple **SLOTS**
- **SESSIONS** manage multiple **SLOTENROLLED **entries
- **SESSIONS** link to multiple SESSIONINSTRUCTOR records
- **SLOTS** can have multiple **SLOTENROLLED **entries

Detailed Relationship Flow:

1. A single SESSION can have multiple SLOTS
2. Each SLOT can be enrolled by multiple students through SLOTENROLLED
3. Each SESSION can be linked to multiple instructors via SESSIONINSTRUCTOR
4. The ***SESSION ID*** serves as the primary linking identifier across these tables

![Session flow Diagarm](Session.png)
-----------------------------------------------------

## Course Purchase Flow Diagram

Course Purchase Flow Explanation:
- **USERS** purchase courses, which creates **COURSESENROLLED** records
- Each **COURSESENROLLED** entry:
  1. Generates **NOTIFICATIONS** to Super Admin panel 
  2. Triggers entries in **MAILQUEUE**
  3. Creates a **TIMELINE** record for student activity

### Relationship Flow:


- When a Student purchases a course:
   - A record is created in COURSESENROLLED
   - Automatically generates a notification
   - Adds an entry to the mail queue for sending confirmation email
   - Creates a timeline entry for student activity

![Coursesflow Diagarm](Courses.png)
--------------------------------------------------------
## Product Purchase Flow Diagram

- A single USER can purchase multiple PRODUCTS (one-to-many relationship)
- Each PRODUCT_ENROLLED entry can generate multiple NOTIFICATIONS
- Each PRODUCT_ENROLLED entry can create multiple TIMELINE entries

### Relationship Flow:

- When a Student purchases a Product:
   - A record is created in PRODUCT_ENROLLED
   - Automatically generates a notification
   - Creates a timeline entry for student activity

![Product Diagarm](Product.png)
