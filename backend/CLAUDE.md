# Backend Instructions

This is the backend implementation for the Specmatic MCP Sample project.

## API Specification
The backend should implement the Order API defined in `../products_api.yaml`:

- Default server URL as per first server URL in `../products_api.yaml`

## Tech Stack

- Use NodeJS and Express
- Storage should be in memory data structures, no database required
- Use nvm use stable to use latest version of node

## Development Guidelines
- Implement all endpoints according to the OpenAPI specification
- Return proper HTTP status codes as per the OpenAPI specification
- Handle validation errors with appropriate error responses
- Follow RESTful conventions
- Structure the code such that routes, models, etc. are in separate folders and files
- Do not use curl to verify endpoints, use Specmatic MCP contract test instead to get feedback

## Testing
- Test against the OpenAPI specification using Specmatic MCP. Both contract test and resiliency test should pass

## Cleanup
- Shutdown backend server after all tests have passed