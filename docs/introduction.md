# Introduction

The Concurrency-Safe Online Ticketing System allows users to browse events, reserve tickets, make payments, and receive electronic tickets online.

The system is specifically designed to prevent booking collisions and duplicate payments when multiple users attempt to purchase the same remaining ticket simultaneously.

The design incorporates:
- reservation handling
- transaction management
- row-level database locking
- payment authorization

to ensure safe and consistent ticket sales.