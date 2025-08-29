# Specmatic MCP Sample Project

This project demonstrates how to build a complete full-stack application from an OpenAPI specification using **[Specmatic MCP](https://hub.docker.com/repository/docker/specmatic/specmatic-mcp)** as intelligent guardrails, without requiring Specmatic as a project dependency.

> **Note:** This project uses Claude Code for demo purposes, however you can use any coding agent of your choice and make necessary changes accordingly.

## 🎯 What This Demo Shows

Starting with just an OpenAPI specification (`products_api.yaml`), this project shows how you can:

- Build a complete Node.js/Express backend API using Specmatic MCP Contract and Resiliency Test as guard rails
- Create a React frontend application using Specmatic MCP Mock to isolate and build the Frontend independently
- Ensure frontend and backend stay in sync with the API specification in the process

## 🚀 Quick Start

> **⚡ Just One Prompt - No Contract Drift!**
>
> Complete the quick setup below, then Claude Code with Specmatic MCP will build your entire full-stack application without any drift from the OpenAPI specification.

### ✅ Prerequisites (Required)

**Step 1:** **Install Claude Code** (if not already installed):

Follow installation instructions at [https://docs.anthropic.com/claude/docs/claude-code](https://docs.anthropic.com/claude/docs/claude-code)

**Step 2:** **Add Specmatic MCP Server**:
```bash
cd specmatic-mcp-sample
claude mcp add-json specmatic '{"command":"docker","args":["run","--rm","-i","--network=host","-v","'$(pwd)':/app/reports","specmatic/specmatic-mcp:latest"],"env":{}}'
```
### 🎯 Usage (2 Simple Commands)

**Step 3:** **Open this project in Claude Code**:
```bash
claude
```

**Step 4:** **Ask Claude to build the application**:
```
Please build the complete application according to the OpenAPI specification
```

TIP: use plan mode to review the task list before proceeding

### 🔄 Optional Reset
**Reset the project to try again** (optional - Claude Code command available):
```
/reset-sample-project
```

---

**🎉 That's it! Claude will automatically:**
- ✨ Build complete Node.js/Express backend API
- ✨ Create React frontend application
- ✨ Validate implementations against the OpenAPI contract
- ✨ Provide mock servers for development
- ✨ Run contract and resiliency tests
- ✨ Ensure all components comply with the specification

## Alternative to Claude Code: MCP Server Workflow with VS Code and Copilot Agent

1. **Start Docker Desktop.**  
2. **Open your project** in VS Code as a **workspace** (single-folder or multi-root as needed).  
3. **Open the Command Palette** (`Ctrl+Shift+P` / `Cmd+Shift+P`) and search for **`MCP: Add server`**, then press **Enter**.  
4. **Choose transport protocol** as **`stdio`**.  
5. **Enter the command** to run the MCP server (adjust the project path to your setup):  
   ```bash
   docker run --rm -i --network=host -v /path/to/specmatic-mcp-sample:/app/reports specmatic/specmatic-mcp:latest
   ```
6. **Set the server ID** to `specmatic-mcp`.  
7. **Choose installation scope**: `Global` (available everywhere) or `Workspace` (just this project).  
8. **Verify the server**: open the **MCP servers** panel in VS Code and confirm the server is listed without errors.  
9. Once connected, the MCP server is ready.  
10. **Interact with Copilot Agent**: ask it to run contract tests, resiliency tests, or start a mock server in natural language.  
11. To build the app, keep the README open and prompt Copilot with:  
    ```
    Please build the complete application according to the OpenAPI specification.
    Show me the plan before proceeding with the changes.
    ```
12. Continue collaborating with the agent until the backend passes all tests and the frontend is integrated using the mock server.  

## 📁 Project Structure

```
specmatic-mcp-sample/
├── products_api.yaml      # OpenAPI specification (the single source of truth)
├── backend/              # Node.js/Express API implementation
│   ├── CLAUDE.md        # Backend development instructions
│   └── ...
├── frontend/            # React frontend application
│   ├── CLAUDE.md        # Frontend development instructions
│   └── ...
├── CLAUDE.md           # Main project instructions
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

## 🏗️ Architecture Diagrams

### Production Setup
```
┌─────────────────┐                                  ┌─────────────────┐
│                 │ ────── HTTP Requests ──────────► │                 │
│    Frontend     │                                  │    Backend      │
│   (React App)   │        ┌─────────────────┐       │ (Express API)   │
│                 │        │products_api.yaml│       │                 │
│   Port: 4000    │        │  (OpenAPI Spec) │       │   Port: 3000    │
│                 │        └─────────────────┘       │                 │
|                 |                                  |                 |
│                 │ ◄────── HTTP Responses ───────── │                 │
└─────────────────┘                                  └─────────────────┘
```

### Development Setup - Frontend
```
┌─────────────────┐                     ┌─────────────────┐
│                 │                     │                 │
│    Frontend     │     Mock Requests   │ Specmatic Mock  │
│   (React App)   │ ◄─────────────────► │    Server       │
│                 │                     │                 │
│   Port: 4000    │                     │   Port: 9001    │
└─────────────────┘                     └─────────┬───────┘
                                                  │
                                                  │ Based on
                                                  │
                                                  ▼
                                     ┌─────────────────────┐
                                     │                     │
                                     │   products_api.yaml │
                                     │  (OpenAPI Spec)     │
                                     │                     │
                                     └─────────────────────┘
```

### Development Setup - Backend
```
┌─────────────────┐                       ┌─────────────────┐
│                 │                       │                 │
│ Specmatic MCP   │ ───► Contract   ───►  │    Backend      │
│    Tools        │      Testing          │ (Express API)   │
│                 │                       │                 │
│ (via Docker)    │ ───► Resiliency ───►  │   Port: 3000    │
└─────────┬───────┘      Testing          └─────────────────┘
          │
          │ Validates against
          │
          ▼
┌─────────────────────┐
│                     │
│  products_api.yaml  │
│  (OpenAPI Spec)     │
│                     │
└─────────────────────┘
```

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
- [Use MCP servers in VS Code](https://code.visualstudio.com/docs/copilot/customization/mcp-servers)
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io/)

---

**Ready to see contract-driven development in action? Just ask Claude to build the application!**
