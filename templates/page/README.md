# Orbit Page Extension Template

Pages in Orbit represent full dashboard workspaces arranged into a 1 to 4-column responsive grid.

## How to Create and Distribute a Page Extension

1. **Define Layout**: Define the columns and widget IDs in `page.toml` (refer to `page.toml` in this directory).
2. **Registry Entry**: Add a page entry to `registry.json` with `"type": "page"`:
   ```json
   {
       "id": "page_my_workspace",
       "name": "My Workspace",
       "description": "Custom multi-column dashboard layout.",
       "version": "0.1.0",
       "api_version": "0.10.0",
       "author": "your_name",
       "type": "page",
       "components": ["coin"],
       "layout": [
           ["system", "cpu"],
           ["clock", "coin"],
           ["network", "weather"]
       ]
   }
   ```
3. **Installation**: Orbit users install page extensions via `orbit install page_my_workspace`.
