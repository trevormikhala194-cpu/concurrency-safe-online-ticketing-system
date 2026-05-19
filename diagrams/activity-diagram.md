# Activity Diagram Explanation

## Overview

The Activity Diagram illustrates the workflow of the Online Ticketing System from the moment a customer accesses the platform to the point where a ticket is successfully issued.

The diagram focuses on:
- user actions
- system processes
- decision points
- payment handling
- reservation management
- concurrency protection

It helps explain how the system processes ticket purchases safely and efficiently.

---

## Workflow Description

### 1. Start

The process begins when a customer accesses the system.

The user may:
- register a new account
- login into an existing account

Authentication ensures that bookings are linked to verified users.

---

### 2. Browse Events

After authentication, the customer can:
- browse available events
- view event details
- search for preferred events

The system displays:
- event title
- venue
- date
- ticket availability
- ticket pricing

---

### 3. Select Event

The customer selects an event and initiates a ticket reservation request.

At this stage, the system prepares to verify ticket inventory.

---

### 4. Request Reservation

The system receives the reservation request and begins concurrency handling procedures.

This stage is important because multiple users may attempt to reserve tickets simultaneously.

---

### 5. Lock Ticket Inventory

The system temporarily locks the event inventory record in the database.

Purpose:
- prevent simultaneous ticket modifications
- maintain inventory consistency
- avoid overselling

This process ensures that only one transaction can modify the remaining ticket count at a time.

---

### 6. Check Ticket Availability

The system checks whether tickets are still available.

Decision Point:
- If tickets are available → reservation continues
- If tickets are sold out → booking process stops

This decision node is critical for preventing ticket collisions.

---

### 7. Reserve Ticket

If tickets are available:
- available ticket count is reduced
- reservation record is created

The reservation temporarily holds the ticket while payment is processed.

Reservation statuses may include:
- RESERVED
- CONFIRMED
- EXPIRED
- CANCELLED

---

### 8. Authorize Payment

The system sends payment details to the Payment Gateway.

The payment gateway verifies:
- transaction validity
- customer payment approval

Payment authorization occurs before final ticket confirmation.

This prevents charging customers for unavailable tickets.

---

### 9. Payment Decision

The system evaluates the payment response.

#### If Payment Succeeds:
- reservation becomes confirmed
- booking is finalized

#### If Payment Fails:
- reservation is cancelled
- ticket inventory is restored

This ensures unused tickets become available again.

---

### 10. Generate Ticket

After successful payment:
- electronic ticket is generated
- QR code is created
- booking confirmation is prepared

The ticket is then delivered to the customer.

---

### 11. Send Confirmation

The customer receives:
- e-ticket
- payment confirmation
- booking details

The booking process is successfully completed.

---

### 12. End

The workflow ends after:
- successful ticket issuance
OR
- reservation cancellation due to sold-out inventory or failed payment

---

## Concurrency Protection

Concurrency protection is one of the most important aspects of this system.

The Activity Diagram demonstrates how the system prevents:
- double booking
- duplicate payments
- ticket inventory conflicts

using:
- reservation handling
- database locking
- transaction management
- controlled payment authorization

This ensures accurate ticket sales even during high traffic conditions.

---

## Importance of the Activity Diagram

The Activity Diagram helps developers understand:
- booking workflow
- system decision points
- reservation lifecycle
- payment flow
- inventory management process

It also provides a clear visual representation of how the system handles concurrent booking requests safely.