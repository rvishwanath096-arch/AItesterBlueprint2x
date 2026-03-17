# Restful Booker API - Comprehensive Test Cases Documentation

**Created Date:** 2026-03-17
**API Base URL:** https://restful-booker.herokuapp.com
**API Version:** Latest
**QA Standard:** Enterprise Level SDET
**Total Test Cases:** 55+

---

## Table of Contents
1. [Overview](#overview)
2. [API Endpoints Summary](#api-endpoints-summary)
3. [Test Case Strategy](#test-case-strategy)
4. [Step-by-Step Processing](#step-by-step-processing)
5. [Test Case Categories](#test-case-categories)
6. [Authentication Details](#authentication-details)
7. [Test Data Management](#test-data-management)

---

## Overview

The Restful Booker API is a CRUD (Create, Read, Update, Delete) web API designed for learning API testing. It includes authentication mechanisms and intentional bugs for testing practice. The API automatically resets every 10 minutes to its default state with 10 pre-loaded booking records.

### Key Characteristics:
- **Authentication Required:** For PUT, PATCH, DELETE operations
- **Response Format:** JSON
- **Auto-reset:** Every 10 minutes
- **Pre-loaded Data:** 10 sample booking records
- **Error Handling:** Multiple HTTP status codes for various scenarios

---

## API Endpoints Summary

| Endpoint | Method | Authentication | Purpose |
|----------|--------|-----------------|---------|
| /auth | POST | None Required | Generate authentication token |
| /ping | GET | None Required | Health check endpoint |
| /booking | GET | None Required | Retrieve all booking IDs |
| /booking/{id} | GET | None Required | Retrieve specific booking details |
| /booking | POST | None Required | Create new booking |
| /booking/{id} | PUT | Token Required | Complete booking update |
| /booking/{id} | PATCH | Token Required | Partial booking update |
| /booking/{id} | DELETE | Token Required | Delete booking |

---

## Test Case Strategy

### Testing Layers

#### 1. **Positive Testing**
- Valid credentials and payloads
- Correct status codes (200, 201, 204)
- Valid response body structure
- Successful operations confirmation

#### 2. **Negative Testing**
- Invalid credentials
- Missing required fields
- Invalid data types
- Non-existent resource IDs
- Unauthorized access attempts

#### 3. **Security Testing**
- Authentication token validation
- Authorization checks
- Missing authentication headers
- Expired or invalid tokens

#### 4. **Boundary Testing**
- Empty strings
- NULL values
- Maximum length strings
- Special characters in inputs
- Numeric edge cases

#### 5. **Data Validation Testing**
- Required field validation
- Data type validation
- Format validation (dates, emails)
- Business logic validation

#### 6. **Performance & Reliability**
- Response time checks
- Concurrent request handling
- Error recovery
- Consistent response format

---

## Step-by-Step Processing

### Phase 1: Pre-Test Setup

```
Step 1: Environment Verification
├─ Confirm API Base URL accessibility
├─ Verify API is responsive (GET /ping)
├─ Document API response time baseline
└─ Note current system date/time

Step 2: Authentication Validation
├─ Test valid credentials
├─ Capture authentication token
├─ Validate token format
├─ Document token expiration details
└─ Save token for subsequent tests
```

### Phase 2: Test Case Execution

```
Step 1: Auth Endpoint Testing
├─ Positive: Valid login
├─ Negative: Invalid credentials
├─ Negative: Missing fields
├─ Negative: Invalid email format
└─ Boundary: Very long password

Step 2: Ping Endpoint Testing
├─ Positive: Health check status
├─ Verify response structure
└─ Validate status code 200

Step 3: Booking GET Operations
├─ Positive: Get all booking IDs
├─ Positive: Get specific booking
├─ Negative: Invalid booking ID
├─ Negative: Non-existent ID
└─ Boundary: Very large ID numbers

Step 4: Booking CREATE Operation
├─ Positive: Create booking with valid data
├─ Negative: Missing required fields
├─ Negative: Invalid data types
├─ Boundary: Special characters in names
└─ Data Validation: Invalid dates

Step 5: Booking UPDATE Operations
├─ PUT: Complete update with token
├─ PUT: Without authentication token
├─ PATCH: Partial update with token
├─ PATCH: Update single field
└─ Authorization: Invalid token

Step 6: Booking DELETE Operation
├─ Positive: Delete with valid token
├─ Negative: Delete without token
├─ Negative: Delete non-existent booking
└─ Verification: Confirm deletion
```

### Phase 3: Validation & Reporting

```
Step 1: Response Validation
├─ HTTP Status Code verification
├─ Response Header validation
├─ Response Body structure check
├─ Data type consistency
└─ Required fields presence

Step 2: Error Handling Validation
├─ Error message format
├─ Error code presence
├─ Error description clarity
└─ Proper HTTP status codes

Step 3: Data Integrity
├─ Verify created data persistence
├─ Validate updated data accuracy
├─ Confirm deleted data removal
└─ Test concurrent operations

Step 4: Test Report Generation
├─ Execution summary
├─ Pass/Fail metrics
├─ Defect logging
├─ Recommendations
└─ Sign-off documentation
```

---

## Test Case Categories

### 1. Authentication (9 Test Cases)
- Valid login credentials
- Invalid username/password
- Missing required fields
- Special characters in credentials
- Boundary conditions for credentials

### 2. Health Check - Ping (3 Test Cases)
- Standard ping check
- Response format validation
- Status code verification

### 3. Get All Bookings (5 Test Cases)
- Standard get all request
- Response format verification
- Count validation
- Header validation
- Performance check

### 4. Get Single Booking (8 Test Cases)
- Valid booking ID
- Invalid booking ID
- Non-existent booking
- Boundary numeric values
- Special characters in ID
- Null ID
- Negative ID values
- Very large ID numbers

### 5. Create Booking (15 Test Cases)
- Valid booking with all fields
- Missing first name
- Missing last name
- Missing check-in date
- Missing check-out date
- Invalid date format
- Check-out before check-in
- Invalid email format
- Null values in required fields
- Special characters in names
- Maximum length string values
- Duplicate booking detection

### 6. Update Booking (10 Test Cases)
- Complete update with valid token
- Update without token
- Update with invalid token
- Update non-existent booking
- Update with partial data
- Update with null values
- Dates before current date
- Invalid date formats
- Very long field values
- Special characters update

### 7. Partial Update (8 Test Cases)
- Single field update
- Multiple field update
- Null value update
- Without authentication
- Invalid token
- Non-existent booking
- Boundary field values
- Invalid data type

### 8. Delete Booking (5 Test Cases)
- Delete with valid token
- Delete without token
- Delete with invalid token
- Delete non-existent booking
- Delete already deleted booking

---

## Authentication Details

### Auth Endpoint: POST /auth

**Request Body:**
```json
{
  "username": "admin",
  "password": "password123"
}
```

**Success Response (200):**
```json
{
  "token": "abc123xyz"
}
```

**Error Response (200 - with error):**
```json
{
  "reason": "Bad credentials"
}
```

### Using Authentication Token

For protected endpoints (PUT, PATCH, DELETE), include token in:
- Cookie header: `Cookie: token=<token_value>`
- OR Authorization header: `Authorization: Bearer <token_value>`

---

## Test Data Management

### Pre-Test Data Setup

1. **Default Booking Records:** API comes with 10 pre-loaded bookings (IDs 1-10)
2. **Authentication Data:**
   - Username: `admin`
   - Password: `password123`
3. **Reset Cycle:** Every 10 minutes

### Booking Creation Test Data Structure

```json
{
  "firstname": "String",
  "lastname": "String",
  "totalprice": "Number",
  "depositpaid": "Boolean",
  "bookingdates": {
    "checkin": "YYYY-MM-DD",
    "checkout": "YYYY-MM-DD"
  },
  "additionalneeds": "String"
}
```

### Required Fields
- firstname
- lastname
- totalprice
- depositpaid
- bookingdates (checkin, checkout)

### Optional Fields
- additionalneeds

---

## Test Execution Framework

### Pre-Test Checklist
- [ ] API Base URL is accessible
- [ ] Network connectivity confirmed
- [ ] Test user credentials verified
- [ ] Test environment isolated
- [ ] Test data cleaned up from previous run
- [ ] Authentication token generation confirmed

### Test Execution Steps for Each Test Case

1. **Identify Test Case ID:** TC_XXX_NNN format
2. **Review Pre-conditions:** Ensure all prerequisites met
3. **Execute Test Steps:** Follow step sequence exactly
4. **Capture Actual Results:** Record actual response
5. **Compare with Expected:** Validate all criteria
6. **Document Status:** Pass/Fail/Blocked
7. **Log Defects:** If actual != expected
8. **Record Execution Details:** Timestamp, QA name, notes

### Test Result Categories

- **PASS:** All expected results met
- **FAIL:** One or more expectations not met
- **BLOCKED:** Cannot execute due to environment/dependency
- **NOT EXECUTED:** Test not run (skip reason documented)

---

## Defect Logging Standards

When an actual result differs from expected:

1. Document the exact mismatch
2. Classify defect severity:
   - **Critical:** API unusable, security risk
   - **High:** Major functionality broken
   - **Medium:** Partial functionality impacted
   - **Low:** Minor issue, workaround available
3. Include reproduction steps
4. Note environment details
5. Attach evidence/screenshots

---

## Enterprise QA Standards Applied

✓ Comprehensive endpoint coverage
✓ Positive and negative scenarios
✓ Security and authentication testing
✓ Boundary and edge case testing
✓ Data validation testing
✓ Error handling verification
✓ Response structure validation
✓ Status code verification
✓ Header validation
✓ Performance baseline testing
✓ Defect traceability
✓ Test report documentation
✓ Reusable test data
✓ Clear pass/fail criteria
✓ Audit trail maintenance

---

## Next Steps After Test Case Creation

1. Load test cases into test management system
2. Assign test cases to QA engineers
3. Define test execution schedule
4. Prepare test environment
5. Execute test cases per priority
6. Log defects in defect tracking system
7. Create test execution report
8. Perform regression testing as needed
9. Sign off on test completion
10. Archive test documentation

---

**Document Version:** 1.0
**Last Updated:** 2026-03-17
**Status:** Ready for Test Execution
