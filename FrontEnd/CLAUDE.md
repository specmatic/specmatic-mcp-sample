# FrontEnd Instructions

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
- Base URL: As per first UR in `../products_api.yaml`
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
- Build FrontEnd by using Specmatic MCP Mock by passing it `../products_api.yaml`. Do not start the backend in `../BackEnd` for this purpose.
- Use React
- Implement proper error handling
- Add loading states for better UX
- Consider using a HTTP client library for API calls