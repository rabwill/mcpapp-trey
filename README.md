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

1. Expose your local server using VS Code port forwarding:
   - Open the **Ports** view in VS Code (click the **Ports** tab in the bottom panel, or run **Ports: Focus on Ports View** from the Command Palette)
   - Click **Forward a Port** and enter `3001`
   - Right-click the forwarded port and select **Port Visibility** > **Public**
   - Copy the generated forwarded URL (e.g., `https://<id>-3001.uks1.devtunnels.ms`)
2. Go to [Claude](https://claude.ai) and open a conversation
3. Click the **Connectors** icon in the chat input area
4. Click **Manage Connectors**
5. Click **Add custom connector**
6. Enter a name (e.g., "Trey HR") and your forwarded URL with `/mcp` as the Remote MCP server URL:
   ```
   https://<id>-3001.uks1.devtunnels.ms/mcp
   ```
7. Click **Add** to connect
8. The MCP tools will now be available in your conversation

### ChatGPT

1. Expose your local server using VS Code port forwarding:
   - Open the **Ports** view in VS Code (click the **Ports** tab in the bottom panel, or run **Ports: Focus on Ports View** from the Command Palette)
   - Click **Forward a Port** and enter `3001`
   - Right-click the forwarded port and select **Port Visibility** > **Public**
   - Copy the generated forwarded URL (e.g., `https://<id>-3001.uks1.devtunnels.ms`)
2. Go to [ChatGPT](https://chat.openai.com)
3. Click the **Setting** from your profile
4. Click **Apps** > **Create app**
5. Enter a name (e.g., "Trey HR") and your forwarded URL with `/mcp` as the Remote MCP server URL:
   ```
   https://<id>-3001.uks1.devtunnels.ms/mcp
   ```
6. Authentication is `No Auth`, select it
7. Click **Create**
8. The MCP tools will now be available in your conversation

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
| *Avery Howard is on two projects already — show me her profile, then find another React developer who could take over the Woodgrove Bank financial plugin work* | Agent opens the profile to review Avery's workload, searches for consultants with React skills, and surfaces Sanjay Puranik as a candidate — reasoning across tools a static page can't do |
| *We just signed Southridge Video's platform migration — find everyone with Python or Node.js skills, show me their profiles, and assign the best fit as Architect at $130/hr* | Agent searches by skill, evaluates multiple consultant profiles, picks Robin Zupanc (Python + multi-cloud certs), and creates the assignment — a multi-step workflow in one conversation |
| *Show the dashboard filtered to billable consultants, then open the bulk editor and add the certification "GitHub Copilot" to every consultant who has JavaScript as a skill* | Agent filters the dashboard for insight, pivots to the bulk editor, identifies Avery and Sanjay as JavaScript-skilled, and batch-updates their certifications — chaining read and write operations |
| *Bellows College needs a project lead for their network security review — who's free, and can you assign them and update their skills to include "Network Security"?* | Agent checks current assignments, finds Lois Wyn (Project lead role, no assignments), assigns her to the project, and updates her skill list — orchestrating three tools in one request |

## Development

```bash
npm run dev:server         # Server with hot-reload (tsx --watch)
npm run build:widgets      # Rebuild widgets after changes
npm run inspector          # Launch MCP Inspector for testing
```
