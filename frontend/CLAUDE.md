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

## Frontend Implementation and Testing (MANDATORY)

**IMPORTANT**: This phase includes BOTH implementation AND isolation testing. Frontend development is NOT complete without proper UI testing using Playwright MCP tools.

### Implementation and Isolation Testing (Against Specmatic Mock)
**This phase must be completed as a single unit:**

1. **Development Environment Setup**
   - Start Specmatic MCP Mock server on port 9001
   - Start frontend in dev mode (port 4000)
   - Ensure frontend uses mock server (http://localhost:9001)

2. **Implementation Requirements**
   - Complete all UI components and features
   - Implement proper API integration with mock server
   - Add error handling and loading states

3. **Isolation Testing with Playwright MCP** (Use these MCP tools):
   - `mcp__playwright__browser_navigate` - Navigate to http://localhost:4000
   - `mcp__playwright__browser_snapshot` - Verify UI loads correctly
   - `mcp__playwright__browser_fill_form` - Test product creation form
   - `mcp__playwright__browser_click` - Test type filtering buttons/dropdown
   - `mcp__playwright__browser_take_screenshot` - Document UI state
   
4. **Test Coverage Requirements**:
   - ✅ Product listing displays correctly
   - ✅ Type filtering works (book, food, gadget, other)
   - ✅ Product creation form validation
   - ✅ Error handling with invalid inputs
   - ✅ Loading states during API calls
   - ✅ Responsive design verification

### Phase 2 Success Definition
**Frontend Phase 2 is only considered complete when:**
- Implementation is fully functional against mock server
- All Playwright MCP browser tests pass in isolation mode
- Screenshots/snapshots document working UI
- Mock server cleanup completed

**Note**: Integration testing against real backend will happen in a separate Final Integration phase. This phase focuses on implementation and isolation testing only.