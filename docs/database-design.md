# Database Design

## Users Table

| Field | Type |
|---|---|
| user_id | INT |
| name | VARCHAR |
| email | VARCHAR |
| password | VARCHAR |

---

## Events Table

| Field | Type |
|---|---|
| event_id | INT |
| title | VARCHAR |
| venue | VARCHAR |
| date | DATETIME |
| total_tickets | INT |
| available_tickets | INT |

---

## Reservations Table

| Field | Type |
|---|---|
| reservation_id | INT |
| user_id | INT |
| event_id | INT |
| status | VARCHAR |
| expiry_time | DATETIME |

---

## Payments Table

| Field | Type |
|---|---|
| payment_id | INT |
| reservation_id | INT |
| amount | DECIMAL |
| payment_status | VARCHAR |

---

## Tickets Table

| Field | Type |
|---|---|
| ticket_id | INT |
| reservation_id | INT |
| qr_code | TEXT |
| status | VARCHAR |