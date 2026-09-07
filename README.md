# Movie Ticket Booking System (Low-Level Design)

A modular, console-based movie ticket booking system implemented in C++ demonstrating object-oriented principles, design patterns, and clean separation of concerns.

---

## Key Design Highlights

* **Decoupled Seat Availability (`Seat` vs. `ShowSeat`)**: Physical seats belong to the screen layout (`Seat`), while show-specific availability states (`AVAILABLE` / `BOOKED`) are managed independently via `ShowSeat`[cite: 1, 3, 4, 7].
* **Clean Domain Boundaries (SRP)**: Domain entities like `Booking` do not format receipts or calculate costs[cite: 1, 9]. Ticket generation is handled by `TicketPrinter`, and tier sums are handled by `PriceCalculator`[cite: 1, 12, 13].
* **Extensible Payments (OCP / DIP)**: `BookingService` depends on an abstract `Payment` interface, allowing easy integration of new methods (UPI, Card, Cash) without altering core booking orchestration[cite: 1, 10, 11, 14].

---

## Architecture & Diagrams

### Class Diagram
![Class Diagram](docs/class_diagram.png)

### Sequence Flow
![Sequence Diagram](docs/sequence_diagram.png)

---

## Project Structure

```text
├── 01_Movie.cpp            # Movie entity (title, language, duration)
├── 02_Seat.cpp             # Physical seat entity and tier definitions
├── 03_Screen.cpp           # Physical screen configuration
├── 04_Cinema.cpp           # Cinema venue holding screens
├── 05_Show.cpp             # Show scheduling entity
├── 06_ShowSeat.cpp         # Slot-specific seat status wrapper
├── 07_Customer.cpp         # Customer profile representation
├── 08_Booking.cpp          # Booking record and status lifecycle
├── 09_Payment.cpp          # Base payment interface
├── 10_PaymentTypes.cpp     # UPI, Card, and Cash implementations
├── 11_PriceCalculator.cpp  # Pricing logic utility
├── 12_TicketPrinter.cpp    # Console receipt formatter
├── 13_BookingService.cpp   # Core booking controller
└── main.cpp                # Interactive CLI driver loop
