# CarCare Product Requirements Document

## Project Title
CarCare

## Brief Description
A phone-first web app that helps personal drivers and small rental fleet owners track vehicle maintenance, log service history with receipts, get mileage- and time-based reminders, review expenses, and compare local shops before contacting a provider.

## Target Users

### Personal Drivers
- Example: A college student in Chico with a limited budget
- Needs: Track maintenance for one or a few vehicles, budget for repairs, find affordable shops

### Small Rental Fleet Owners
- Manages multiple vehicles (e.g., 5-20 cars)
- Needs: Track maintenance across fleet, compare upkeep costs, schedule service around rentals

### Rental Employees
- Enters odometer readings when vehicles are returned
- Needs: Quick data entry interface, accurate mileage updates for service planning

## Technical Architecture

### Front-End
- React PWA (Progressive Web App)
- Build tool: Vite
- Mobile-first responsive design

### Back-End
- Express API (Node.js)
- RESTful API endpoints

### Database
- Supabase (PostgreSQL)
- Hosted database with authentication

## Exclusions (Out of Scope)

The following features are explicitly **not** included in CarCare:

- Live vehicle location tracking
- Previous-owner service history
- Booking and payment processing
- Rental reservation management
- In-app messaging system
- Parts commerce/sales
- Review moderation system

## Future Considerations
These features may be considered for future iterations but are not part of the initial MVP.
