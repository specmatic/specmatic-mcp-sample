# Reset Sample Project

Reset the project to its initial state, keeping only the directory structure and essential configuration files.

## Command

```bash
# Remove all files from backend directory except CLAUDE.md
find backend -type f ! -name "CLAUDE.md" -delete

# Remove all files from frontend directory except CLAUDE.md
find frontend -type f ! -name "CLAUDE.md" -delete

# Remove all files from mcp-server directory except CLAUDE.md
find mcp-server -type f ! -name "CLAUDE.md" -delete

# Remove any generated files from root directory but keep essential files
find . -maxdepth 1 -type f ! -name "products_api.yaml" ! -name "CLAUDE.md" ! -name "README.md" ! -name ".gitignore" -delete

echo "Project reset complete. Directory structure preserved with only CLAUDE.md files and essential root files."
```

This command will:
- Keep the directory structure: `backend/`, `frontend/`, `mcp-server/`
- Preserve all `CLAUDE.md` files in each directory
- Keep essential root files: `products_api.yaml`, `CLAUDE.md`, `README.md`, `.gitignore`
- Remove all generated/implementation files from each component directory
- Remove any temporary files from the root directory