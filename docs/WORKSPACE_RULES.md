# CarCare Workspace Rules

## Naming Conventions

### JavaScript/TypeScript
- **Variables and functions**: `camelCase`
  ```javascript
  const vehicleMileage = 50000;
  function calculateServiceDue() { ... }
  ```

- **Constants**: `UPPER_SNAKE_CASE`
  ```javascript
  const MAX_MILEAGE_THRESHOLD = 5000;
  ```

- **Classes/Components**: `PascalCase`
  ```javascript
  class VehicleProfile { ... }
  function ServiceHistoryForm() { ... }
  ```

- **React Component Files**: `PascalCase`
  ```
  VehicleProfile.jsx
  ServiceHistoryForm.jsx
  ```

### File Names
- **General files**: `kebab-case`
  ```
  vehicle-service-utils.js
  api-client.js
  ```

- **Test files**: Same as source file with `.test.` or `.spec.` suffix
  ```
  vehicle-service-utils.test.js
  ServiceHistoryForm.spec.jsx
  ```

### Database
- **Table names**: `snake_case`
  ```sql
  CREATE TABLE service_records (...);
  ```

- **Column names**: `snake_case`
  ```sql
  vehicle_id, current_mileage, created_at
  ```

### API Endpoints
- **URL paths**: `kebab-case`
  ```
  GET /api/vehicles
  POST /api/service-records
  ```

## Commit Message Guidelines

### Format
Use imperative tense and reference the associated user story ID when applicable.

**Template:**
```
<short description in imperative tense> (US<XX>)

<optional detailed explanation>
```

**Examples:**
```
Add vehicle profile form (US01)

Implemented the vehicle profile form component with validation for make, model, and VIN fields.
```

```
Implement mileage update API endpoint (US02)

Added PUT /api/vehicles/:id/mileage endpoint with validation to ensure new mileage is greater than previous reading.
```

```
Fix reminder notification timing bug (US03)

Corrected the background job to calculate reminder dates based on user preference settings instead of hardcoded values.
```

### Guidelines
- Use imperative mood ("Add" not "Added" or "Adding")
- Keep the subject line under 50 characters
- Reference the user story ID when the commit relates to a specific US
- Capitalize the subject line
- Do not end the subject line with a period
- Use the body to explain what and why, not how
- Reference related issue numbers if applicable

## Pull Request and Review Process

### PR Requirements
1. **Descriptive Title**: Include user story ID and brief description
   ```
   [US01] Implement vehicle profile CRUD operations
   ```

2. **PR Description Template:**
   ```markdown
   ## User Story
   US01 · F01 Vehicle Profiles

   ## Changes
   - [ ] API endpoints for vehicle CRUD
   - [ ] Database migration for vehicles table
   - [ ] React form component for adding/editing vehicles
   - [ ] Unit tests for vehicle service

   ## Testing
   - [ ] Manual testing completed
   - [ ] All unit tests passing
   - [ ] Integration tests passing

   ## Screenshots (if UI changes)
   [Attach screenshots]

   ## Checklist
   - [ ] Code follows workspace rules
   - [ ] Commit messages follow guidelines
   - [ ] No console errors or warnings
   - [ ] Mobile responsive
   ```

3. **Branch Name**: Must follow branching strategy (see below)

### Review Process
1. **Self-Review**: Before requesting review, creator should:
   - Review their own changes
   - Ensure all tests pass
   - Check for console errors
   - Verify mobile responsiveness

2. **Peer Review**: At least one approval required
   - Reviewer checks code quality and adherence to rules
   - Tests must pass on reviewer's machine
   - UI changes should be tested on mobile viewport

3. **Approval Criteria**:
   - Code follows naming conventions
   - Commit messages are properly formatted
   - Tests cover new functionality
   - No breaking changes without documentation
   - Security best practices followed (no exposed secrets)

4. **Merge Requirements**:
   - At least one approval
   - All CI checks passing
   - No merge conflicts
   - PR description completed

## Branching Strategy

### Main Branch
- **Name**: `main`
- **Protection**: Require PR approval and CI checks before merge
- **Usage**: Production-ready code only

### Feature Branches
- **Naming Convention**: `feature/US<XX>-short-description`
  ```
  feature/US01-vehicle-profiles
  feature/US03-maintenance-reminders
  feature/US08-shop-comparison
  ```

- **Creation**: Create from `main` when starting work on a user story
- **Lifecycle**:
  1. Create branch from `main`
  2. Develop feature with small, focused commits
  3. Ensure commit messages reference the user story
  4. Create PR to `main`
  5. Address review feedback
  6. Merge after approval

### Bugfix Branches
- **Naming Convention**: `bugfix/description-of-issue`
  ```
  bugfix/reminder-notification-not-sending
  bugfix/mileage-validation-edge-case
  ```

- **Usage**: For bug fixes that don't align with a specific user story

### Hotfix Branches
- **Naming Convention**: `hotfix/description-of-hotfix`
  ```
  hotfix/critical-security-patch
  hotfix/production-data-corruption
  ```

- **Usage**: For urgent production fixes
- **Process**: Merge to both `main` and release branches if applicable

### Branch Cleanup
- Delete feature branches after successful merge
- Keep bugfix/hotfix branches for 1 week after merge, then delete
- Use `git branch -d <branch-name>` locally after PR merge

## Code Quality Standards

### JavaScript/React
- Use ESLint for linting
- Use Prettier for code formatting
- Avoid console.log in production code
- Add JSDoc comments for complex functions
- Keep functions under 50 lines when possible
- Extract reusable logic into custom hooks

### API
- Validate all inputs
- Return appropriate HTTP status codes
- Include error messages in responses
- Log errors for debugging
- Rate limit public endpoints

### Database
- Use parameterized queries (no SQL injection risk)
- Add indexes for frequently queried columns
- Use transactions for multi-table operations
- Include created_at/updated_at timestamps
- Never commit sensitive data (passwords, API keys)

## Testing Standards

### Unit Tests
- Test all service layer functions
- Test utility functions
- Mock external dependencies
- Aim for 80%+ coverage on critical paths

### Integration Tests
- Test API endpoints
- Test database operations
- Test authentication flows

### E2E Tests
- Test critical user journeys
- Test mobile-specific interactions
- Test file upload flows

### Manual Testing Checklist
- Test on mobile viewport (375px width)
- Test on tablet viewport (768px width)
- Test on desktop viewport
- Test on Chrome, Firefox, Safari
- Test file uploads
- Test form validation
- Test error states
