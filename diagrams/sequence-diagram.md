# Sequence Diagram Explanation

## Overview

The Sequence Diagram illustrates how different components of the Online Ticketing System interact during ticket purchasing.

The diagram focuses on:
- ticket reservation flow
- payment authorization
- concurrency control
- collision prevention

The main objective is to ensure that when only one ticket remains, only one customer can successfully complete payment and receive the ticket.

---

## Main Participants

### User A, User B, User C

These users represent customers attempting to purchase tickets simultaneously.

The diagram demonstrates how the system handles concurrent requests safely.

---

### System

The System component processes:
- reservation requests
- ticket availability checks
- payment coordination
- ticket generation

It acts as the main controller of the booking workflow.

---

### Database

The Database stores:
- event information
- ticket inventory
- reservations
- bookings
- payment records

The database is responsible for maintaining consistency during concurrent transactions.

---

### Payment Gateway

The Payment Gateway authorizes customer payments before tickets are confirmed.

Examples:
- Stripe
- M-Pesa

---

### Ticket Service

The Ticket Service generates electronic tickets after successful payment confirmation.

---

## Sequence Flow

### 1. Multiple Users Request Tickets

Several users attempt to purchase tickets at the same time.

Example:
- only one ticket remains
- multiple users submit requests simultaneously

This creates the possibility of ticket collisions.

---

### 2. System Locks Event Inventory

The system sends a request to the database to lock the event row.

Purpose:
- prevent simultaneous ticket modifications
- ensure only one transaction accesses the remaining ticket

This process is called row-level locking.

---

### 3. System Checks Availability

After locking the event record, the system checks:

- available ticket count

If tickets are available:
- reservation process continues

If no tickets remain:
- request is rejected safely

---

### 4. Ticket Reservation

If availability is confirmed:
- available ticket count is reduced
- reservation record is created

At this stage:
- the ticket is temporarily held
- payment is not yet finalized

---

### 5. Payment Authorization

The system sends a payment authorization request to the Payment Gateway.

The gateway verifies:
- payment validity
- transaction approval

Only authorized payments proceed.

---

### 6. Reservation Confirmation

After successful payment authorization:
- reservation status changes to CONFIRMED
- booking becomes finalized

---

### 7. Ticket Generation

The Ticket Service generates:
- electronic ticket
- QR code
- ticket validation data

The ticket is then sent to the successful customer.

---

### 8. Other Users Are Rejected

If the remaining ticket has already been reserved:
- other users receive a sold-out response
- no payment is captured from unsuccessful users

This prevents:
- duplicate payments
- overselling
- ticket collisions

---

## Concurrency Control

Concurrency control is the most important concept in this system design.

The system uses:
- database transactions
- row-level locking
- reservation management
- payment authorization before capture

to ensure:
- only one transaction succeeds
- ticket inventory remains accurate
- customers are not charged incorrectly

This design improves transaction safety and system reliability.

---

## Importance of the Sequence Diagram

The Sequence Diagram helps developers understand:
- interaction order
- request flow
- database synchronization
- reservation lifecycle
- payment coordination

It also demonstrates how the system prevents double booking in real-time environments.