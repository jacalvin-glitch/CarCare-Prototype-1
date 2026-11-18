# CarCare Development Tasks

## User Story Breakdown

### US01 · F01 Vehicle Profiles
**User Story:** As a driver, I want to add a vehicle with its make, model, VIN, and current mileage so that I can keep its records separate.

**Feature:** Vehicle Profiles

**Development Tasks:**

#### Task 1.1: Vehicle Profile Data Model
- Design database schema for vehicles table (make, model, VIN, current_mileage, user_id, created_at, updated_at)
- Create Supabase migration
- Add RLS policies for user-specific access

**Acceptance Criteria:**
- Vehicles table exists in Supabase with all required fields
- RLS policy ensures users can only access their own vehicles
- Migration can be applied and rolled back successfully

#### Task 1.2: API Endpoints for Vehicle CRUD
- Create Express endpoints: GET /api/vehicles, POST /api/vehicles, PUT /api/vehicles/:id, DELETE /api/vehicles/:id
- Implement input validation for VIN format and required fields
- Add error handling for duplicate VINs per user

**Acceptance Criteria:**
- All CRUD endpoints return appropriate HTTP status codes
- VIN validation rejects invalid formats
- Users cannot create vehicles with duplicate VINs
- API includes proper error messages

#### Task 1.3: Vehicle Profile Form UI
- Create React form component for adding/editing vehicles
- Implement form validation (required fields, VIN format)
- Add vehicle list view with ability to add, edit, delete vehicles
- Style for mobile-first responsive design

**Acceptance Criteria:**
- Form validates required fields before submission
- Users can successfully add, edit, and delete vehicles
- Vehicle list displays all user's vehicles
- UI is responsive on mobile devices

---

### US02 · F02 Mileage Tracking
**User Story:** As a rental employee, I want to enter a vehicle's odometer reading when it is returned so that the owner has current mileage for service planning.

**Feature:** Mileage Tracking

**Development Tasks:**

#### Task 2.1: Mileage Update API
- Create PUT /api/vehicles/:id/mileage endpoint
- Validate mileage is greater than previous reading
- Log mileage updates with timestamp and employee ID

**Acceptance Criteria:**
- Endpoint accepts vehicle ID and new mileage
- Rejects mileage less than or equal to current reading
- Mileage history is tracked with timestamps

#### Task 2.2: Mileage Entry UI
- Create simplified mileage entry form for rental employees
- Add vehicle selector (by VIN or license plate)
- Display current mileage for reference
- Quick-submit button for common scenarios

**Acceptance Criteria:**
- Form allows selecting vehicle and entering new mileage
- Shows current mileage before update
- Prevents entry of invalid mileage values
- Optimized for quick, repeated use

---

### US03 · F03 Maintenance Reminders
**User Story:** As a daily driver, I want to receive a phone reminder when service approaches its mileage or time limit so that I can plan maintenance before I miss it.

**Feature:** Maintenance Reminders

**Development Tasks:**

#### Task 3.1: Reminder Configuration Data Model
- Create service_reminders table (vehicle_id, service_type, mileage_threshold, date_threshold, last_mileage, last_date, reminder_sent)
- Create reminder_settings table (user preferences for notification timing)

**Acceptance Criteria:**
- Tables support both mileage-based and time-based reminders
- Reminder settings allow customization of advance notice
- Proper foreign key relationships to vehicles

#### Task 3.2: Reminder Calculation Logic
- Implement background job to check vehicles against thresholds
- Calculate when to send reminders based on user preferences
- Support multiple reminder types (oil change, tire rotation, etc.)

**Acceptance Criteria:**
- Job runs daily to check all vehicles
- Correctly identifies vehicles approaching service thresholds
- Sends reminders at configured advance intervals

#### Task 3.3: Push Notification Integration
- Integrate with web push notifications for PWA
- Request notification permissions from users
- Send reminder notifications with vehicle and service details

**Acceptance Criteria:**
- Users can grant/deny notification permissions
- Notifications include vehicle make/model and service type
- Notifications are sent at appropriate times
- Users can dismiss or snooze reminders

#### Task 3.4: Reminder Settings UI
- Create settings page for reminder preferences
- Allow users to configure advance notice (e.g., 500 miles or 1 month)
- Enable/disable reminders per vehicle or service type

**Acceptance Criteria:**
- Users can customize reminder timing preferences
- Can enable/disable reminders for specific vehicles
- Settings persist across sessions

---

### US04 · F04 Service History
**User Story:** As a vehicle owner, I want to log a completed maintenance or repair job with its date, mileage, and cost so that I can review what was done and when.

**Feature:** Service History

**Development Tasks:**

#### Task 4.1: Service Record Data Model
- Create service_records table (vehicle_id, service_type, date, mileage, cost, description, shop_name, created_at)
- Add indexes for efficient querying by vehicle and date range

**Acceptance Criteria:**
- Table captures all required service information
- Proper foreign key to vehicles table
- Indexes support common query patterns

#### Task 4.2: Service History API
- Create GET /api/vehicles/:id/service-history endpoint
- Support filtering by date range and service type
- Create POST /api/service-records endpoint
- Implement cost aggregation endpoints

**Acceptance Criteria:**
- Can retrieve service history for a vehicle
- Filtering by date range works correctly
- Can create new service records
- Cost calculations are accurate

#### Task 4.3: Service History UI
- Create service history list view per vehicle
- Add form for logging new service records
- Display service records with date, mileage, cost, and description
- Show summary statistics (total spent, last service date)

**Acceptance Criteria:**
- Service history displays in chronological order
- Form allows logging all required information
- Summary statistics update automatically
- UI is mobile-friendly

---

### US05 · F05 Receipt Attachments
**User Story:** As a vehicle owner, I want to attach a receipt photo or digital copy to a service record so that I can retrieve proof of the work from that vehicle's history.

**Feature:** Receipt Attachments

**Development Tasks:**

#### Task 5.1: File Storage Integration
- Integrate Supabase Storage for receipt uploads
- Create storage bucket for receipts
- Configure security policies for user-specific access

**Acceptance Criteria:**
- Storage bucket is created and secured
- Users can only access their own receipts
- File upload/download endpoints work correctly

#### Task 5.2: Receipt Data Model
- Add receipt_attachments table (service_record_id, file_path, uploaded_at)
- Update service_records API to handle file uploads

**Acceptance Criteria:**
- Receipts are linked to service records
- Multiple receipts can be attached to one service record
- File metadata is stored correctly

#### Task 5.3: Receipt Upload UI
- Add file upload component to service record form
- Support camera capture on mobile devices
- Show preview of uploaded images
- Allow viewing/downloading attached receipts

**Acceptance Criteria:**
- Users can upload photos from camera or gallery
- Image preview displays before submission
- Receipts can be viewed from service history
- Upload progress is shown to user

---

### US06 · F06 Expense Review
**User Story:** As a small rental fleet owner, I want to view recorded service expenses by vehicle over a chosen date range so that I can compare upkeep costs across my fleet.

**Feature:** Expense Review

**Development Tasks:**

#### Task 6.1: Expense Aggregation API
- Create GET /api/expenses endpoint with vehicle_id and date_range filters
- Implement cost calculation per vehicle
- Add fleet-wide expense summary endpoint

**Acceptance Criteria:**
- Can query expenses by vehicle and date range
- Cost calculations are accurate
- Fleet summary aggregates all vehicles correctly

#### Task 6.2: Expense Dashboard UI
- Create expense comparison view
- Implement date range picker
- Display bar chart or table comparing costs across vehicles
- Show breakdown by service type

**Acceptance Criteria:**
- Dashboard visualizes cost comparisons clearly
- Date range filter updates data correctly
- Users can identify high-cost vehicles
- Data is exportable (e.g., CSV)

---

### US07 · F07 Service Cost Estimates
**User Story:** As a budget-conscious driver, I want to look up an estimated price range for a service on my vehicle so that I can budget before contacting a shop.

**Feature:** Service Cost Estimates

**Development Tasks:**

#### Task 7.1: Cost Estimate Data Model
- Create service_estimates table (service_type, vehicle_make, vehicle_model, min_price, max_price, year_range)
- Seed with initial cost data for common services

**Acceptance Criteria:**
- Table structure supports make/model-specific estimates
- Initial seed data covers common services
- Estimates can be updated over time

#### Task 7.2: Cost Estimate API
- Create GET /api/estimates endpoint with service_type, make, model parameters
- Return price range based on vehicle specifics
- Handle cases where exact match isn't available (fallback to make-only or generic)

**Acceptance Criteria:**
- Returns appropriate price range for vehicle
- Falls back gracefully to less specific estimates
- Includes data source or confidence level

#### Task 7.3: Cost Estimate UI
- Add cost lookup feature to service planning section
- Allow users to select service type and vehicle
- Display estimated price range prominently
- Show disclaimer that estimates are averages

**Acceptance Criteria:**
- Users can easily look up estimates
- Price range is clearly displayed
- Disclaimers are visible
- UI integrates with reminder context

---

### US08 · F08 Shop Comparison
**User Story:** As a driver looking for a mechanic, I want to compare shops for a selected service and search area by estimated prices, ratings, and reviews so that I can decide which shops to contact.

**Feature:** Shop Comparison

**Development Tasks:**

#### Task 8.1: Shop Data Model
- Create shops table (name, address, phone, services_offered, average_rating, review_count, price_level, latitude, longitude)
- Create shop_reviews table (shop_id, user_id, rating, comment, date)

**Acceptance Criteria:**
- Shop data includes location and contact info
- Reviews are linked to shops and users
- Price level indicator supports comparison

#### Task 8.2: Shop Search API
- Create GET /api/shops endpoint with location, service_type, and radius parameters
- Implement geographic search (bounding box or radius)
- Sort by rating, price, or distance
- Return aggregated ratings and review counts

**Acceptance Criteria:**
- Search returns shops within specified radius
- Filtering by service type works
- Sorting options function correctly
- Pagination is supported

#### Task 8.3: Shop Comparison UI
- Create shop search form with location input
- Display shop cards with key info (name, rating, price level, distance)
- Implement comparison view for selected shops
- Show individual reviews when requested

**Acceptance Criteria:**
- Search form is intuitive
- Shop cards display essential information
- Users can select multiple shops to compare
- Reviews are readable and helpful

---

### US09 · F09 Fleet Overview
**User Story:** As a small rental fleet owner, I want to review upcoming or due service across my vehicles so that I can schedule maintenance around rentals.

**Feature:** Fleet Overview

**Development Tasks:**

#### Task 9.1: Fleet Status API
- Create GET /api/fleet/status endpoint
- Return all vehicles with service status (due soon, overdue, upcoming)
- Calculate days until service or miles until threshold
- Sort by urgency

**Acceptance Criteria:**
- Endpoint returns all user's vehicles
- Status calculation is accurate
- Sorting by urgency works correctly
- Response includes actionable info (days/miles until due)

#### Task 9.2: Fleet Dashboard UI
- Create fleet overview page
- Display vehicle cards with status indicators (color-coded)
- Show due date/mileage for each vehicle
- Implement filtering by status (all, due soon, overdue)

**Acceptance Criteria:**
- Dashboard provides at-a-glance fleet status
- Status indicators are visually distinct
- Filtering helps prioritize
- Mobile layout supports reviewing multiple vehicles

#### Task 9.3: Fleet Calendar Integration
- Add calendar view of upcoming service
- Display service due dates across timeline
- Allow quick access to vehicle details from calendar

**Acceptance Criteria:**
- Calendar view shows all upcoming service
- Clicking an event shows vehicle details
- View is responsive on mobile
