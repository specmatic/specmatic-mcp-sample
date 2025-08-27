# Specmatic MCP Sample Project

This is a sample project demonstrating contract testing using Specmatic MCP (Model Context Protocol) with a full-stack application.

## Project Structure

- `products_api.yaml` - OpenAPI specification defining the Products API contract
- `backend/` - Node.js/Express API implementation
- `frontend/` - React frontend application

## Overview

The project implements a simple Products API with the following capabilities:
- GET /products - Retrieve products filtered by type (book, food, gadget, other)
- POST /products - Create new products

## Development Guidelines

- Name variables and method descriptively, avoid short forms
- Create appropriate .gitignore file

## Development Workflow

Build components in this specific order:

### 1. Backend Development (First Priority)
```bash
cd backend
# Follow instructions in backend/CLAUDE.md
# Use Specmatic MCP for contract testing, not manual curl testing
# IMPORTANT: Resiliency tests MUST pass
# When there are contract or resiliency tests failed, analyse the test failures in JUnit report file provided in Specmatic MCP response and make necessary fixes in the code
```

### 2. Frontend Development (Second Priority)
```bash
cd frontend
# Follow instructions in frontend/CLAUDE.md

# This phase includes BOTH implementation AND isolation testing:
# 1. Shutdown backend if running to avoid port conflicts
# 2. Start Specmatic MCP Mock on port 9001 (based on products_api.yaml)
# 3. Configure frontend to use http://localhost:9001 for API calls
# 4. Develop against consistent mock responses
# 5. Run Playwright MCP browser testing against mock server
# 6. Complete all isolation testing requirements (MANDATORY)

# CLEANUP: Always shutdown Specmatic MCP Mock after development and testing
```

### 3. Final Integration Testing (Third Priority)
```bash
# Integration testing between Frontend and Backend:
# 1. Ensure all mock servers are shutdown
# 2. Start real backend on port 3000
# 3. Configure frontend for production mode (http://localhost:3000)
# 4. Run Playwright MCP UI automation testing only (no contract/resiliency tests needed)
# 5. Verify end-to-end workflows and data persistence
```

## Contract Testing with Specmatic MCP

This project uses Specmatic MCP for:
- **Contract Testing**: Verify backend implementation against `products_api.yaml`
- **Mock Server**: Provide mock backend for frontend development
- **Resiliency Testing**: Test error scenarios and edge cases in backend (MANDATORY)

### Key Benefits
- Both backend and frontend can be developed independently
- Automatic contract validation across components
- No manual API testing needed
- Consistent behavior across environments

## Mock Server Management

### Port Allocation Strategy
- **Backend**: http://localhost:3000 (as defined in products_api.yaml)
- **Frontend Dev Mock**: http://localhost:9001 (for frontend development)

### Starting Mock Servers
```bash
# For Frontend development
cd frontend
# Start Specmatic MCP Mock on port 9001
# Use Specmatic MCP manage_mock_server tool or equivalent
```

### Stopping Mock Servers
```bash
# Always cleanup after development to free ports
# Stop Frontend mock server on port 9001
# Use Specmatic MCP manage_mock_server stop commands
```

### Best Practices
1. **Always shutdown backend** before starting mock servers to avoid port conflicts
2. **Use dedicated port** for frontend mock server (9001)
3. **Cleanup mock servers** after development sessions

## Getting Started

1. Start with the OpenAPI spec in `products_api.yaml`
2. **Build Backend first** - implement according to contract, ensure resiliency tests pass
3. **Build Frontend second** - use Specmatic MCP Mock (port 9001) for development and isolation testing
   - Start mock server before development
   - Complete implementation and Playwright MCP testing
   - Shutdown mock server after development and testing
4. **Final Integration** - Run UI automation testing with real backend (no additional contract tests needed)

### Mock Server Lifecycle in Development Workflow
```bash
# Frontend Development Cycle (includes isolation testing)
cd frontend
# 1. Start Specmatic MCP Mock on port 9001
# 2. Develop frontend features against mock
# 3. Run Playwright MCP browser testing against mock
# 4. Complete all isolation testing requirements
# 5. Shutdown mock server when done

# Final Integration Testing (UI automation only)
# 1. Ensure all mock servers are shutdown
# 2. Start real backend on port 3000  
# 3. Run Playwright MCP UI automation against real backend
# 4. Verify end-to-end workflows
```

## Testing Strategy

### Phase 1: Backend Testing
- **Backend Contract Tests**: Verify implementation matches products_api.yaml  
- **Backend Resiliency Tests**: Verify error handling and edge cases (MANDATORY)

### Phase 2: Frontend Development with Isolation Testing
- **Frontend Implementation**: Build UI components against Specmatic MCP Mock (port 9001)
- **Isolation Testing**: Complete Playwright MCP browser testing against mock server
- **Requirements**: All UI functionality verified in isolation

### Phase 3: Final Integration Testing  
- **UI Automation Only**: Playwright MCP testing against real backend (port 3000)
- **End-to-End Workflows**: Verify complete user journeys and data persistence
- **No Additional Contract Tests**: Backend contract compliance already verified in Phase 1

## Documentation

- Add README.md with clear instructions to start and run each application
- Update .gitignore as needed

Each component has detailed instructions in its respective CLAUDE.md file.
- **Build Order**: Backend → Frontend (with Isolation Testing) → Final Integration
- **Phase 2**: Frontend development includes Playwright MCP isolation testing against mock server
- **Phase 3**: Integration testing uses UI automation only (no additional contract tests)
- **Port Strategy**: Backend (3000), Frontend Mock (9001)