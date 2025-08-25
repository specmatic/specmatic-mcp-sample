# Specmatic MCP Sample Project

This is a sample project demonstrating contract testing using Specmatic MCP (Model Context Protocol) with a full-stack application.

## Project Structure

- `products_api.yaml` - OpenAPI specification defining the Products API contract
- `backend/` - Node.js/Express API implementation
- `frontend/` - React frontend application
- `mcp-server/` - MCP Server with Products API tools

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

# DEV MODE (Default for development):
# 1. Shutdown backend if running to avoid port conflicts
# 2. Start Specmatic MCP Mock on port 9001 (based on products_api.yaml)
# 3. Configure frontend to use http://localhost:9001 for API calls
# 4. Develop against consistent mock responses

# PROD MODE (Integration testing):
# 1. Ensure backend is running on http://localhost:3000
# 2. Configure frontend to use http://localhost:3000 for API calls
# 3. Test against real backend implementation

# CLEANUP: Always shutdown Specmatic MCP Mock after development
```

### 3. MCP Server Development (Third Priority)
```bash
cd mcp-server
# Follow instructions in mcp-server/CLAUDE.md
# Implements get_products and create_product MCP tools

# DEV MODE (Default for development):
# 1. Shutdown backend if running to avoid port conflicts
# 2. Start Specmatic MCP Mock on port 9002 (based on products_api.yaml)
# 3. Configure MCP tools to use http://localhost:9002 for API calls
# 4. Develop against consistent mock responses
# 5. Use different port (9002) than Frontend mock (9001) to avoid conflicts

# PROD MODE (Integration testing):
# 1. Ensure backend is running on http://localhost:3000
# 2. Configure MCP tools to use http://localhost:3000 for API calls
# 3. Test against real backend implementation

# CLEANUP: Always shutdown Specmatic MCP Mock after development
```

## Contract Testing with Specmatic MCP

This project uses Specmatic MCP for:
- **Contract Testing**: Verify backend implementation against `products_api.yaml`
- **Mock Server**: Provide mock backend for frontend and MCP server development
- **Resiliency Testing**: Test error scenarios and edge cases in backend (MANDATORY)

### Key Benefits
- All components (backend, frontend, MCP server) can be developed independently
- Automatic contract validation across all components
- No manual API testing needed
- Consistent behavior across environments

## Mock Server Management

### Port Allocation Strategy
- **Backend**: http://localhost:3000 (as defined in products_api.yaml)
- **Frontend Dev Mock**: http://localhost:9001 (for frontend development)
- **MCP Server Dev Mock**: http://localhost:9002 (for MCP server development)

### Starting Mock Servers
```bash
# For Frontend development
cd frontend
# Start Specmatic MCP Mock on port 9001
# Use Specmatic MCP manage_mock_server tool or equivalent

# For MCP Server development
cd mcp-server
# Start Specmatic MCP Mock on port 9002
# Use Specmatic MCP manage_mock_server tool or equivalent
```

### Stopping Mock Servers
```bash
# Always cleanup after development to free ports
# Stop Frontend mock server on port 9001
# Stop MCP Server mock server on port 9002
# Use Specmatic MCP manage_mock_server stop commands
```

### Best Practices
1. **Always shutdown backend** before starting mock servers to avoid port conflicts
2. **Use dedicated ports** for each component's mock server (9001, 9002)
3. **Cleanup mock servers** after development sessions
4. **Never run multiple mock servers simultaneously** unless testing component interactions

## Getting Started

1. Start with the OpenAPI spec in `products_api.yaml`
2. **Build Backend first** - implement according to contract, ensure resiliency tests pass
3. **Build Frontend second** - use Specmatic MCP Mock (port 9001) for development
   - Start mock server before development
   - Shutdown mock server after development
4. **Build MCP Server third** - implement get_products and create_product tools  
   - Use Specmatic MCP Mock (port 9002) for development
   - Shutdown mock server after development
5. Run integration tests across all components

### Mock Server Lifecycle in Development Workflow
```bash
# Frontend Development Cycle
cd frontend
# 1. Start Specmatic MCP Mock on port 9001
# 2. Develop frontend features against mock
# 3. Shutdown mock server when done

# MCP Server Development Cycle  
cd mcp-server
# 1. Start Specmatic MCP Mock on port 9002
# 2. Develop MCP tools against mock
# 3. Shutdown mock server when done

# Integration Testing
# 1. Ensure all mock servers are shutdown
# 2. Start real backend on port 3000  
# 3. Test all components against real backend
```

## Testing Strategy

### Development Testing (Dev Mode)
- **Backend**: Specmatic MCP contract and resiliency tests against implementation (resiliency tests MUST pass)
- **Frontend**: Test against Specmatic MCP Mock (port 9001) for consistent development experience
- **MCP Server**: Test against Specmatic MCP Mock (port 9002) for consistent development experience

### Integration Testing (Prod Mode)
- **Frontend**: Test against real Backend (port 3000) for end-to-end validation
- **MCP Server**: Test against real Backend (port 3000) for end-to-end validation
- **Full Stack**: Complete contract compliance verification across all components

### Test Execution Order
1. **Backend Contract Tests**: Verify implementation matches products_api.yaml
2. **Backend Resiliency Tests**: Verify error handling and edge cases (MANDATORY)
3. **Frontend Dev Tests**: Against mock server for rapid development
4. **MCP Server Dev Tests**: Against mock server for rapid development  
5. **Integration Tests**: All components against real backend

## Documentation

- Add README.md with clear instructions to start and run each application
- Update .gitignore as needed

Each component has detailed instructions in its respective CLAUDE.md file.
- **Build Order**: Backend → Frontend → MCP Server  
- **Dev Mode**: Shutdown backend before starting mock servers to avoid port conflicts
- **Prod Mode**: Shutdown all mock servers before starting backend for integration testing
- **Port Strategy**: Backend (3000), Frontend Mock (9001), MCP Server Mock (9002)