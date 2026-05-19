# Class Diagram Explanation

## Overview

The Class Diagram represents the structure of the Concurrency-Safe Online Ticketing System.

It shows:
- system entities
- class attributes
- class methods
- relationships between classes
- ticket reservation and payment flow

The diagram is designed to support secure ticket booking while preventing double booking and payment collisions.

---

## Main Classes

### User

The User class represents customers using the platform.

Functions:
- register account
- login
- logout

Attributes:
- userID
- name
- email
- password

---

### Admin

The Admin class inherits from the User class.

The administrator manages:
- events
- reservations
- ticket inventory

Functions:
- add events
- update events
- delete events
- manage reservations

---

### Event

The Event class stores event information and ticket inventory.

Functions:
- check ticket availability
- reduce available tickets after reservation
- restore tickets after failed payments or expired reservations

Important attributes:
- totalTickets
- availableTickets

These attributes are critical for preventing overselling.

---

### Reservation

The Reservation class is the core concurrency-control component of the system.

Its purpose is to temporarily hold tickets before payment is completed.

Functions:
- reserve tickets
- confirm reservations
- expire unpaid reservations
- cancel reservations

Reservation statuses:
- RESERVED
- CONFIRMED
- EXPIRED
- CANCELLED

This design prevents multiple users from purchasing the same final ticket simultaneously.

---

### Booking

The Booking class stores finalized booking information after successful payment authorization.

Functions:
- create booking
- cancel booking

---

### Payment

The Payment class handles payment processing.

Functions:
- authorize payment
- capture payment
- cancel payment
- refund payment

Payment authorization occurs before final ticket confirmation to avoid charging unsuccessful users.

---

### Ticket

The Ticket class represents the electronic ticket issued to the customer.

Functions:
- generate QR ticket
- validate ticket during entry

---

## Relationships Between Classes

### Admin Inherits User

The Admin class extends the User class because administrators are also system users.

---

### Event → Reservation

Each reservation belongs to an event.

This relationship allows the system to track reserved ticket inventory.

---

### Reservation → Booking

A booking is created after a reservation is successfully confirmed.

---

### Booking → Payment

Each booking is associated with a payment transaction.

---

### Payment → Ticket

A ticket is generated only after successful payment confirmation.

---

## Concurrency Handling

The system is designed to prevent ticket collisions when multiple users attempt to purchase the same remaining ticket.

The Reservation class plays the most important role in this process.

The system uses:
- reservation handling
- database transactions
- row-level locking
- payment authorization flow

to ensure:
- only one reservation succeeds
- only one payment is captured
- ticket inventory remains consistent

This approach improves transaction safety and prevents double booking.