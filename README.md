# Specmatic MCP Sample Project

This project demonstrates how to build a complete full-stack application from an OpenAPI specification using **Specmatic MCP** as intelligent guardrails, without requiring Specmatic as a project dependency.

## 🎯 What This Demo Shows

Starting with just an OpenAPI specification (`products_api.yaml`), this project shows how you can:

- Build a complete Node.js/Express backend API
- Create a React frontend application  
- Use contract testing and mock servers for development
- Ensure frontend and backend stay in sync with the contract
- All without adding Specmatic as a dependency to your project

## 🚀 Quick Start

### Prerequisites

1. **Install Claude Code** (if not already installed):
   ```bash
   # Follow installation instructions at https://docs.anthropic.com/claude/docs/claude-code
   ```

2. **Add Specmatic MCP Server**:
   ```bash
   claude mcp add-json specmatic '{"command":"docker","args":["run","--rm","-i","--network=host","specmatic-mcp-server"],"env":{}}'
   ```

### Usage

Once you have Claude Code with Specmatic MCP configured:

1. **Open this project in Claude Code**:
   ```bash
   cd specmatic-mcp-sample
   claude
   ```

2. **Ask Claude to build the application**:
   ```
   Please build the complete application according to the OpenAPI specification
   ```

That's it! Claude will use the Specmatic MCP server to:
- Validate implementations against the OpenAPI contract
- Provide mock servers for frontend development
- Run contract and resiliency tests
- Ensure both frontend and backend comply with the specification

## 📁 Project Structure

```
specmatic-mcp-sample/
├── products_api.yaml      # OpenAPI specification (the single source of truth)
├── BackEnd/              # Node.js/Express API implementation
│   ├── CLAUDE.md        # Backend development instructions
│   └── ...
├── FrontEnd/            # React frontend application  
│   ├── CLAUDE.md        # Frontend development instructions
│   └── ...
└── README.md           # This file
```

## 🎯 Key Benefits Demonstrated

### Contract-First Development
- The OpenAPI specification serves as the single source of truth
- Both frontend and backend are built to conform to this contract
- Changes to the API require updating the specification first

### Independent Development
- Frontend can be developed using Specmatic's mock server
- Backend can be developed and tested against the contract
- No need to coordinate development schedules

### Automatic Validation
- Specmatic MCP automatically validates backend implementations
- Contract tests ensure API compliance
- Resiliency tests verify error handling

### Zero Dependencies
- Specmatic runs as an MCP server through Docker
- No need to add Specmatic dependencies to your project
- Clean project structure with minimal tooling overhead

## 🔧 How It Works

1. **OpenAPI Specification**: Defines the Products API with GET and POST endpoints for managing products

2. **Specmatic MCP Integration**: 
   - Provides contract testing capabilities
   - Offers mock server functionality  
   - Validates implementations against the specification
   - Runs resiliency tests for error scenarios

3. **Claude Code Integration**:
   - Uses Specmatic MCP to guide development
   - Automatically runs appropriate tests
   - Ensures contract compliance throughout development

## 🎨 The Products API

The sample API includes:
- **GET /products**: Retrieve products filtered by type (book, food, gadget, other)
- **POST /products**: Create new products with validation

See `products_api.yaml` for the complete specification with examples and validation rules.

## 🏗️ Development Workflow

1. Start with the OpenAPI specification
2. Use Specmatic MCP mock for frontend development  
3. Implement backend according to the contract
4. Run Specmatic MCP tests to verify compliance
5. Both applications work together seamlessly

## 📚 Learn More

- [Specmatic Documentation](https://specmatic.io/)
- [Claude Code Documentation](https://docs.anthropic.com/claude/docs/claude-code)
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/)

---

**Ready to see contract-driven development in action? Just ask Claude to build the application!**