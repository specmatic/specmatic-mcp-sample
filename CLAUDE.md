# Specmatic MCP Sample Project

This is a sample project demonstrating contract testing using Specmatic MCP (Model Context Protocol) with a full-stack application.

## Project Structure

- `products_api.yaml` - OpenAPI specification defining the Products API contract
- `BackEnd/` - Node.js/Express API implementation
- `FrontEnd/` - React frontend application
- `MCPServer/` - MCP Server with Products API tools

## Overview

The project implements a simple Products API with the following capabilities:
- GET /products - Retrieve products filtered by type (book, food, gadget, other)
- POST /products - Create new products

## Development Workflow

Build components in this specific order:

### 1. Backend Development (First Priority)
```bash
cd BackEnd
# Follow instructions in BackEnd/CLAUDE.md
# Use Specmatic MCP for contract testing, not manual curl testing
# IMPORTANT: Resiliency tests MUST pass
```

### 2. Frontend Development (Second Priority)
```bash
cd FrontEnd
# Follow instructions in FrontEnd/CLAUDE.md
# Use Specmatic MCP Mock for backend simulation during development
# Shutdown backend before starting to avoid port conflicts
```

### 3. MCP Server Development (Third Priority)
```bash
cd MCPServer
# Follow instructions in MCPServer/CLAUDE.md
# Implements get_products and create_product MCP tools
# Use Specmatic MCP Mock for development
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

## Getting Started

1. Start with the OpenAPI spec in `products_api.yaml`
2. **Build Backend first** - implement according to contract, ensure resiliency tests pass
3. **Build Frontend second** - use Specmatic MCP Mock for development
4. **Build MCP Server third** - implement get_products and create_product tools
5. Run integration tests across all components

## Testing Strategy

- Backend: Specmatic MCP contract and resiliency tests (resiliency tests MUST pass)
- Frontend: Test against Specmatic MCP Mock
- MCP Server: Test against Specmatic MCP Mock
- Integration: Full contract compliance verification across all components

## Documentation

- Add README.md with clear instructions to start and run each application
- Update .gitignore as needed

Each component has detailed instructions in its respective CLAUDE.md file.
- **Build Order**: Backend → Frontend → MCP Server
- Shutdown backend before starting frontend/MCP server development to avoid port collision with Specmatic MCP Mock