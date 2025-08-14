# Specmatic MCP Sample Project

This is a sample project demonstrating contract testing using Specmatic MCP (Model Context Protocol) with a full-stack application.

## Project Structure

- `products_api.yaml` - OpenAPI specification defining the Products API contract
- `BackEnd/` - Node.js/Express API implementation
- `FrontEnd/` - React frontend application

## Overview

The project implements a simple Products API with the following capabilities:
- GET /products - Retrieve products filtered by type (book, food, gadget, other)
- POST /products - Create new products

## Development Workflow

### 1. Backend Development
```bash
cd BackEnd
# Follow instructions in BackEnd/CLAUDE.md
# Use Specmatic MCP for contract testing, not manual curl testing
```

### 2. Frontend Development
```bash
cd FrontEnd
# Follow instructions in FrontEnd/CLAUDE.md
# Use Specmatic MCP Mock for backend simulation during development
```

## Contract Testing with Specmatic MCP

This project uses Specmatic MCP for:
- **Contract Testing**: Verify backend implementation against `products_api.yaml`
- **Mock Server**: Provide mock backend for frontend development
- **Resiliency Testing**: Test error scenarios and edge cases in backend

### Key Benefits
- Frontend and backend can be developed independently
- Automatic contract validation
- No manual API testing needed
- Consistent behavior across environments

## Getting Started

1. Start with the OpenAPI spec in `products_api.yaml`
2. Use Specmatic MCP Mock for frontend development
3. Implement backend according to contract
4. Run Specmatic MCP contract tests to verify compliance

## Testing Strategy

- Backend: Specmatic MCP contract and resiliency tests
- Frontend: Test against Specmatic MCP Mock
- Integration: Full contract compliance verification

## Documentation

- Add README.md with clear instructions to start and run each application
- Update .gitignore as needed

Each component has detailed instructions in its respective CLAUDE.md file.