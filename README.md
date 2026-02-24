# HR Consultant MCP Server

MCP server with rich Fluent UI React widgets for managing HR consultants, projects, and assignments.

## Author

| Name | GitHub |
|---|---|
| Rabia Williams | [@rabwill](https://github.com/rabwill) |

## Prerequisites

| Requirement | Version |
|---|---|
| Node.js | ≥ 18 |
| npm | ≥ 9 |

Azurite is included as a dev dependency — no separate install needed.

## Quick Start

```bash
npm run install:all        # Install all dependencies
npm run start:azurite      # Start local Azure Table Storage (port 10002) (keep this running in a terminal)
npm run seed               # Seed consultants, projects, assignments (in a new terminal)
npm run build:widgets      # Build widget HTML into assets/
npm run start:server       # Start MCP server on http://localhost:3001
```


## Testing with AI Clients

### Claude

1. Start a tunnel to expose your local server:
   ```bash
   npx localtunnel --port 3001
   # or
   ngrok http 3001
   ```
2. Copy the tunnel URL (e.g., `https://xyz.loca.lt`)
3. Go to [Claude](https://claude.ai) and open a conversation
4. Click the **Connectors** icon in the chat input area
5. Click **Manage Connectors**
5. Click **Add custom connector**
6. Enter a name (e.g., "Trey HR") and your tunnel URL with `/mcp` as the Remote MCP server URL:
   ```
   https://xyz.loca.lt/mcp
   ```
7. Click **Add** to connect
8. The MCP tools will now be available in your conversation

### ChatGPT

1. Start a tunnel to expose your local server:
   ```bash
   npx localtunnel --port 3001
   # or
   ngrok http 3001
   ```
2. Copy the tunnel URL (e.g., `https://xyz.loca.lt`)
3. Go to [ChatGPT](https://chat.openai.com) 
4. Click the **Setting** from your profile 
5. Click **Apps** > **Create app**
6. Enter a name (e.g., "Trey HR") and your tunnel URL with `/mcp` as the Remote MCP server URL:
   ```
   https://xyz.loca.lt/mcp
   ```
7. Authentication is `No Auth`, select it
8. Click **Create** 
9. The MCP tools will now be available in your conversation

### Testing Prompts

Once connected, try these prompts:
- "Show me the HR dashboard"
- "Search for consultants with Azure skills"
- "Show profile for consultant 1"

## MCP Tools

### Widget Tools

| Tool | Widget | Description |
|---|---|---|
| `show-hr-dashboard` | Dashboard | KPIs, consultant cards, project list. Optional filters: `consultantName`, `projectName`, `skill`, `role`, `billable`. |
| `show-consultant-profile` | Profile | Detailed profile card with contact info, skills, certifications, roles, and assignments. Requires `consultantId`. |
| `show-project-details` | Dashboard | Project detail with assigned consultants and forecasted hours. Requires `projectId`. |
| `search-consultants` | Bulk Editor | Search consultants by `skill` or `name`, results shown in the bulk editor for viewing and editing. |
| `show-bulk-editor` | Bulk Editor | View and edit consultant records. Optional filters: `skill`, `name`. |

### Data Tools

| Tool | Description |
|---|---|
| `update-consultant` | Update a single consultant's name, email, phone, skills, or roles. |
| `bulk-update-consultants` | Batch-update multiple consultant records at once. |
| `assign-consultant-to-project` | Assign a consultant to a project with a role, optional rate. |
| `bulk-assign-consultants` | Assign multiple consultants to a project at once. |
| `remove-assignment` | Remove a consultant's assignment from a project. |

## Sample Prompts

| Prompt | What it does |
|---|---|
| *Show me the HR dashboard* | Opens the dashboard widget with all data |
| *Show dashboard filtered by Azure skill* | Dashboard filtered to Azure-skilled consultants |
| *Show profile for consultant 1* | Opens a consultant profile card |
| *Show project details for project 1* | Opens project detail with team |
| *Search consultants with Azure skills* | Finds matching consultants in the bulk editor |
| *Open the bulk editor* | Opens the editor with all consultants |
| *Open bulk editor for consultants named Avery* | Editor filtered to matching consultants |
| *Assign consultant 3 to project 1 as Architect at $150/hr* | Creates an assignment |
| *Remove consultant 2 from project 1* | Removes an assignment |
| *Update consultant 1 — add skill "Kubernetes"* | Updates a single field |

## Development

```bash
npm run dev:server         # Server with hot-reload (tsx --watch)
npm run build:widgets      # Rebuild widgets after changes
npm run inspector          # Launch MCP Inspector for testing
```
