# Specmatic MCP Sample Project

This is a sample project demonstrating contract testing using Specmatic MCP (Model Context Protocol) with a full-stack application.

## Project Structure

- `products_api.yaml` - OpenAPI specification defining the Products API contract
- `backend/` - Node.js/Express API implementation
- `frontend/` - React frontend application

## Development Workflow

Build components in this specific order:

### 1. Backend Development (First Priority)
```bash
# Work in the backend/ directory at repo root level
cd backend
# Follow instructions in backend/CLAUDE.md
# Use Specmatic MCP for contract testing, not manual curl testing
# IMPORTANT: Resiliency tests MUST pass
```

### 2. Frontend Development (Second Priority) 
```bash
# Work in the frontend/ directory at repo root level (NOT inside backend/)
cd frontend
# Start Specmatic MCP Mock on port 9001 (based on products_api.yaml)
# Configure frontend dev mode: REACT_APP_API_BASE_URL=http://localhost:9001
# Develop against mock server and run Playwright MCP browser testing
# Complete all isolation testing requirements (MANDATORY)
```

### 3. Final Integration Testing (Third Priority)
```bash
# Stop all mock servers (port 9001)
# Start real backend on port 3000
# RECONFIGURE frontend to production mode: REACT_APP_API_BASE_URL=http://localhost:3000
# Run Playwright MCP UI automation testing only
# Verify end-to-end workflows and data persistence
```

## Frontend Environment Configuration

Setup environment-based API configuration:
- **Dev mode**: `REACT_APP_API_BASE_URL=http://localhost:9001` (mock server)
- **Prod mode**: `REACT_APP_API_BASE_URL=http://localhost:3000` (real backend)

For integration testing, run frontend in prod mode.

## Features to Implement

### Product Listing
- Display products with filtering by type (book, food, gadget, other)
- Show product details: name, type, inventory count

### Product Creation
- Form to create new products
- Input fields: name, type (dropdown), inventory (number input)
- Validation: Name required, type (book/food/gadget/other), inventory (1-9999)

### API Integration
- GET /products?type={type} for filtering
- POST /products for creating new products
- Handle 200, 201, and 400 responses appropriately

## Development Notes
- Use React, run frontend on port 4000 only
- Implement proper error handling and loading states
- Name variables descriptively, avoid short forms