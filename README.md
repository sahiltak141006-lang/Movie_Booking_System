# Movie Ticket Booking System (Low-Level Design)

A clean, modular C++ implementation of an in-memory movie ticket booking system focusing on core object-oriented principles, low coupling, and clear separation of concerns.

---

## Key Design Principles & Trade-offs

* **Seat vs. ShowSeat Decoupling**: A physical `Seat` only tracks static layout data (identifier and tier)[cite: 1, 3]. Availability (`AVAILABLE` / `BOOKED`) belongs strictly to runtime show scheduling via `ShowSeat`[cite: 1, 7]. This allows multiple shows to reuse the same physical screen without state conflicts[cite: 1, 4, 6].
* **Separation of Concerns (SRP)**: Core entities like `Booking` manage state transitions (`CONFIRMED`, `CANCELLED`) without coupling to console I/O or price math[cite: 1, 9]. Output formatting is handled by `TicketPrinter`, while tier sums live in `PriceCalculator`[cite: 1, 12, 13].
* **Pluggable Payment Gateway (OCP / DIP)**: `BookingService` interacts with a high-level `Payment` interface[cite: 1, 10, 14]. New payment methods (e.g., NetBanking) can be added by implementing the base contract without altering existing booking orchestration.
* **Transaction Rollback**: If a payment fails or an invalid seat is encountered, the service rolls back locked seat states to keep show availability consistent[cite: 1, 14].

---

## Project Structure

```text
├── 01_Movie.cpp            # Movie entity (title, language, duration)
├── 02_Seat.cpp             # Physical seat entity and tier definitions
├── 03_Screen.cpp           # Screen room configuration
├── 04_Cinema.cpp           # Cinema venue holding screens
├── 05_Show.cpp             # Show scheduling entity
├── 06_ShowSeat.cpp         # Slot-specific seat status wrapper
├── 07_Customer.cpp         # Customer profile representation
├── 08_Booking.cpp          # Booking record and status lifecycle
├── 09_Payment.cpp          # Abstract base payment interface
├── 10_PaymentTypes.cpp     # UPI, Card, and Cash implementations
├── 11_PriceCalculator.cpp  # Stateless pricing utility
├── 12_TicketPrinter.cpp    # Terminal receipt formatter
├── 13_BookingService.cpp   # Orchestrator (locks, payments, state)
└── main.cpp                # Interactive CLI menu driver
