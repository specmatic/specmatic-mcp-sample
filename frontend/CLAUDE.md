# Frontend Instructions

This is the frontend implementation for the Specmatic MCP Sample project.

## Overview
Build a web interface that consumes the Products API defined in `../products_api.yaml`.

## Features to Implement

### Product Listing
- Display products with filtering by type (book, food, gadget, other)
- Show product details: name, type, inventory count
- Handle loading states and empty results

### Product Creation
- Form to create new products
- Input fields: name, type (dropdown), inventory (number input)
- Validation according to API spec:
  - Name is required
  - Type must be one of: book, food, gadget, other
  - Inventory must be between 1-9999
- Handle success and error responses

### API Integration
- Base URL: As per first URL in `../products_api.yaml`
- GET /products?type={type} for filtering
- POST /products for creating new products
- Handle 200, 201, and 400 responses appropriately
- Display error messages from API responses

## UI/UX Guidelines
- Responsive design
- Clear error messaging
- Loading indicators during API calls
- Form validation feedback
- Clean, intuitive interface

## Development Notes
- Build Frontend by using Specmatic MCP Mock by passing it `../products_api.yaml`. Do not start the backend in `../backend` for this purpose.
- Setup up node env such that in Dev mode the Frontend talks to Specmatic MCP Mock server and prod / regular mode it is wired to talk to the real application. This will help avoid conflict of where the real backend is running and the mock backend is running.
- Always use the dev mode while in active development and thereby build the Frontend agains the mock backend only
- Use React
- Implement proper error handling
- Add loading states for better UX
- Consider using a HTTP client library for API calls
- Run Frontend on port 4000 only

## Frontend Testing (MANDATORY)

**IMPORTANT**: Frontend implementation is NOT complete without proper UI testing using Playwright MCP tools. Both isolation and integration testing phases are required.

### Phase 1: Isolation Testing (Against Specmatic Mock)
**Required after frontend implementation:**

1. **Start Test Environment**
   - Start Specmatic MCP Mock server on port 9001
   - Start frontend in dev mode (port 4000)
   - Ensure frontend uses mock server (http://localhost:9001)

2. **Playwright MCP Browser Testing** (Use these MCP tools):
   - `mcp__playwright__browser_navigate` - Navigate to http://localhost:4000
   - `mcp__playwright__browser_snapshot` - Verify UI loads correctly
   - `mcp__playwright__browser_fill_form` - Test product creation form
   - `mcp__playwright__browser_click` - Test type filtering buttons/dropdown
   - `mcp__playwright__browser_take_screenshot` - Document UI state
   
3. **Test Coverage Requirements**:
   - ✅ Product listing displays correctly
   - ✅ Type filtering works (book, food, gadget, other)
   - ✅ Product creation form validation
   - ✅ Error handling with invalid inputs
   - ✅ Loading states during API calls
   - ✅ Responsive design verification

### Phase 2: Integration Testing (Against Real Backend)
**Required after isolation testing passes:**

1. **Switch to Integration Environment**
   - Stop Specmatic Mock server
   - Start real backend on port 3000
   - Configure frontend for production mode (http://localhost:3000)

2. **End-to-End Playwright MCP Testing**:
   - `mcp__playwright__browser_navigate` - Open application
   - Complete user workflows (create → list → filter)
   - Verify data persistence across page refreshes
   - Test real API error scenarios

3. **Integration Success Criteria**:
   - ✅ Full product creation to listing workflow
   - ✅ Data persists between frontend sessions
   - ✅ Real backend error handling works
   - ✅ No mock server dependencies in production mode

### Testing Success Definition
**Frontend is only considered complete when:**
- All Playwright MCP browser tests pass in isolation mode
- All integration tests pass against real backend
- Screenshots/snapshots document working UI
- Both dev and prod configurations tested

**Note**: Simply starting servers without browser automation testing is insufficient. Playwright MCP tools must be used to verify actual UI functionality.