# State Diagram Explanation

## Overview

The State Diagram illustrates the lifecycle of a ticket reservation within the Online Ticketing System.

It shows how a ticket changes between different states during the booking process.

The diagram focuses on:
- reservation states
- payment confirmation
- reservation expiration
- ticket availability restoration

This diagram is important for understanding how the system manages ticket inventory safely while preventing double booking and payment collisions.

---

## Reservation States

### 1. AVAILABLE

This is the default state of a ticket before any customer attempts to reserve it.

In this state:
- the ticket can be viewed
- the ticket can be reserved
- inventory count includes the ticket as available

This state exists before the booking process begins.

---

### 2. RESERVED

When a customer initiates a reservation:
- the ticket moves from AVAILABLE to RESERVED

In this state:
- the ticket is temporarily locked
- other users cannot purchase it
- payment is still pending

The RESERVED state is critical for concurrency control because it prevents multiple users from purchasing the same ticket simultaneously.

The system may also assign:
- reservation timer
- expiration deadline

to prevent abandoned reservations from blocking inventory permanently.

---

### 3. CONFIRMED

After successful payment authorization:
- reservation status changes to CONFIRMED

In this state:
- payment has been approved
- booking becomes finalized
- electronic ticket is generated

The customer receives:
- ticket confirmation
- e-ticket
- booking details

Once confirmed, the ticket is no longer available to other users.

---

### 4. EXPIRED

If payment is not completed within the allowed reservation period:
- reservation status changes to EXPIRED

Possible causes:
- customer abandons checkout
- payment timeout
- failed transaction
- network interruption

In this state:
- reservation becomes invalid
- ticket is released back into inventory

This prevents tickets from remaining locked indefinitely.

---

## State Transitions

### AVAILABLE → RESERVED

Occurs when:
- customer requests ticket reservation

The system:
- reduces available ticket inventory
- temporarily locks the reservation

---

### RESERVED → CONFIRMED

Occurs when:
- payment authorization succeeds

The system:
- finalizes booking
- generates electronic ticket

---

### RESERVED → EXPIRED

Occurs when:
- payment is not completed before timeout

The system:
- cancels reservation
- restores ticket inventory

---

### EXPIRED → AVAILABLE

Occurs when:
- expired reservation is cleared

The ticket becomes available again for other customers.

---

## Concurrency Handling

The RESERVED state is the most important concurrency-control mechanism in the system.

It ensures:
- only one customer can hold the final ticket
- ticket inventory remains accurate
- payment collisions are prevented

The system combines:
- reservation management
- database transactions
- row-level locking
- payment authorization

to maintain consistency during high traffic booking periods.

---

## Importance of the State Diagram

The State Diagram helps developers understand:
- reservation lifecycle
- ticket state transitions
- payment-related state changes
- inventory restoration process

It also demonstrates how the system safely handles:
- abandoned reservations
- failed payments
- concurrent booking attempts

while maintaining accurate ticket availability.