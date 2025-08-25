# MCP Server Instructions

This is an MCP (Model Context Protocol) server implementation for the Specmatic MCP Sample project.

## Overview
Build an MCP server that provides tools wrapping the Products API capabilities defined in `../products_api.yaml`.

## Features to Implement

### Products API MCP Tools
- **get_products**: Retrieve products with optional type filtering (book, food, gadget, other)
- **create_product**: Create new products with validation
- **list_product_types**: Get available product types from the schema

### Product Management Tools  
- **filter_products_by_type**: Filter products by specific type
- **validate_product**: Validate product data against schema constraints
- **get_product_schema**: Return product schema information for clients

## API Integration
- Base URL: As per first URL in `../products_api.yaml`
- GET /products?type={type} for filtering
- POST /products for creating new products
- Handle 200, 201, and 400 responses appropriately
- Return structured error messages from API responses

## Development Notes
- Build MCP Server by using Specmatic MCP Mock by passing it `../products_api.yaml`. Do not start the backend in `../backend` for this purpose.
- Setup node env such that in Dev mode the MCP Server talks to Specmatic MCP Mock server and prod / regular mode it is wired to talk to the real application. This will help avoid conflict of where the real Backend is running and the mock backend is running.
- Always use the dev mode while in active development and thereby build the MCP Server against the mock backend only
- Use Node.js/TypeScript for MCP server implementation
- Implement proper error handling for all MCP tool calls
- Add validation for all inputs according to OpenAPI spec
- Consider using HTTP client library for API calls

## MCP Tool Implementation Guidelines
- All tools should return structured JSON responses
- Include proper error handling with meaningful messages
- Validate inputs against OpenAPI schema constraints
- Handle network failures gracefully
- Provide clear success/failure status in responses

## Documentation

Add README that has
- Details on how to run this MCP server with
  - Specmatic MCP mock
  - Real backend
- Instructions to add this MCP to Claude Code using addJSON