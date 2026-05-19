# Software Requirements Specification (SRS)

## Preface

This document provides the Software Requirements Specification (SRS) for the **Bus Ticket Booking System**. It defines the system’s functionalities, performance criteria, security requirements, and overall system architecture necessary for development and deployment in the Bangladeshi transportation sector.

---

## Version History

* **Version 1.0** – Initial draft including core booking logic and persistent storage.
* **Version 1.1** – Integrated PyQt6 GUI specifications, real-time update requirements, and system models.

---

## 1. Introduction

### Purpose

The Bus Ticket Booking System is a desktop-based application designed to modernize the manual ticketing process in Bangladesh. It provides a centralized platform for passengers to search for routes and book seats while allowing administrators to manage bus schedules and passenger records efficiently.

### Document Conventions

This document follows the IEEE SRS standard:

* **Must** – Mandatory requirement.
* **Should** – Recommended feature.
* **May** – Optional enhancement.

### Intended Audience

* **Developers**: For implementing the PyQt6 interface and JSON logic.
* **Stakeholders**: To understand the project scope and preloaded schedule capabilities.
* **QA Teams**: To validate search accuracy and real-time refresh rates.

### Scope

The system provides:

* Real-time bus availability viewing.
* Advanced route-based searching.
* Seat management and automated ticket ID generation.
* Persistent data storage via JSON.
* Professional ticket receipt generation.

---

## 2. Overall Description

### Product Perspective

The Bus Ticket Booking System is a standalone desktop application. It operates locally on the user's machine but mimics a networked environment through an automated 5-second data refresh mechanism.

### Product Functions

* **Bus Management**: View name, origin, destination, time, and seat count.
* **Search Engine**: Filter buses by origin and destination (case-insensitive).
* **Booking System**: Allocate seats and calculate total price.
* **Receipt System**: Generate visual confirmation for successful bookings.
* **Persistence**: Automatically save/load data from `data_store.json`.

### User Classes and Characteristics

* **Admin**: Responsible for setting up schedules and managing the persistent data store.
* **Passenger/User**: Interacts with the GUI to find and book tickets.

### Operating Environment

* **Platform**: Windows, macOS, or Linux.
* **Runtime**: Python 3.7+ with PyQt6.
* **Storage**: Local JSON file system.

### Design and Implementation Constraints

* **Library**: Must use PyQt6 for the GUI.
* **Persistence**: Must use a single-file JSON database for lightweight portability.
* **Architecture**: Must follow a modular structure (`bus.py`, `ticket.py`, etc.).

---

## 3. System Requirements Specification

### Functional Requirements

* **Bus View & Refresh**
* The system must display all 24+ preloaded bus companies.
* The table must refresh every 5 seconds to show updated seat counts.


* **Search Functionality**
* The system must allow searching by "Origin" and "Destination".
* Search results must update instantly upon clicking the search button.


* **Ticket Booking**
* The system must allow selecting a bus from a dropdown menu.
* The system must validate that the requested seat count is available.
* Upon successful booking, the system must decrement the `available_seats` attribute.


* **Receipt Generation**
* The system must display a professional dialog showing Ticket ID, Passenger Name, and total BDT paid.



### Non-Functional Requirements

* **Performance**
* UI components must remain responsive during the 5-second refresh interval.
* JSON read/write operations must complete in under 200ms.


* **Security**
* The system must prevent booking if the seat count exceeds availability.
* Input validation must prevent empty passenger names or contact numbers.


* **Usability**
* The interface must follow Material Design principles (Dark theme, purple accents).
* Receipts should include shadow effects for visual depth.


* **Reliability**
* The system must automatically create `data_store.json` if it is missing on startup.
* The system must handle UTF-8 encoding for proper rendering of Bangladeshi location names.



---

## 4. System Models

> **SYSTEM CONTEXT DIAGRAM**
> *Shows the interaction between the Passenger, Admin, JSON Data Store, and the PyQt6 Application.*

> **USE CASE DIAGRAM**
> *Illustrates the actions performed by Passengers (Search/Book) and Admins (Manage Schedule).*

![System Context Diagram](images/context_diagram.png)
---

## 5. System Evolution

### Assumptions

* Future versions will include a SQL-based database for enterprise-level scaling.
* Integration of SMS Gateway for automated receipt delivery.

### Expected Changes

* Migration from JSON to an Online API for multi-user synchronization.
* Implementation of an interactive seat-map (graphical seat selection).

---

## 6. Appendices

### Hardware Requirements

* **RAM**: Minimum 50MB.
* **Display**: 800x600 resolution or higher.

### Database Requirements

* A flat-file `data_store.json` following the `{"buses": [], "tickets": [], "next_ticket_id": X}` schema.
