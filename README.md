# Azure DevOps Integration Extension

Sync user stories and tasks from Spec Kit to Azure DevOps work items using OAuth authentication (no PAT tokens required).

## Features

- OAuth Authentication: Uses Azure CLI with OAuth flow - no Personal Access Tokens needed
- User Story Sync: Create Azure DevOps User Story work items from spec.md
- Task Sync: Create Azure DevOps Task work items from tasks.md, automatically linked to parent User Stories
- Interactive Selection: Choose which user stories or tasks to sync
- Configuration Persistence: Saves organization, project, and area path for reuse
- Work Item Mapping: Tracks synced items to prevent duplicates
- Priority Mapping: Automatically maps spec-kit priorities (P1-P4) to Azure DevOps priorities
- Auto-Hook: Optional automatic sync after task generation

## Installation

```bash
# Install from catalog
$env:SPECKIT_CATALOG_URL="https://raw.githubusercontent.com/github/spec-kit/main/extensions/catalog.community.json"
specify extension add azure-devops

# Or install Directly by URL
specify extension add azure-devops --from https://github.com/pragya247/spec-kit-azure-devops/archive/refs/tags/v1.0.0.zip
```

## Prerequisites

- **Azure CLI**: Required for Azure DevOps API access
  - Windows: https://aka.ms/installazurecliwindows
  - macOS: `brew install azure-cli`
  - Linux: See https://docs.microsoft.com/cli/azure/install-azure-cli
- **Azure DevOps Access**: Contributor or higher permissions on the target project
- **Spec Kit**: Version 0.1.0 or higher

## Configuration

### Option 1: Interactive Configuration (Recommended)

The extension will prompt you for configuration the first time you use it:

1. **Organization**: Your Azure DevOps organization name (e.g., "MSFTDEVICES" from `https://dev.azure.com/MSFTDEVICES`)
2. **Project**: Your Azure DevOps project name (e.g., "Devices")
3. **Area Path**: Work item area path (e.g., "Devices\\SW\\ASPX\\CE\\Portals and Services")

Configuration is saved to `~/.speckit/ado-config.json` and reused for future syncs.

### Option 2: Manual Configuration

Create `~/.speckit/ado-config.json`:

```json
{
  "Organization": "your-org-name",
  "Project": "your-project-name",
  "AreaPath": "your-area-path",
  "LastUpdated": "2026-03-03 10:30:00"
}
```

### Option 3: Environment Variables

Override configuration with environment variables:

```bash
export AZURE_DEVOPS_ORG="your-org-name"
export AZURE_DEVOPS_PROJECT="your-project-name"
export AZURE_DEVOPS_AREA_PATH="your-area-path"
```

## Usage

### Sync User Stories

```bash
# In your AI agent (Claude, Copilot, etc.)
> /speckit.azure-devops.sync

# Or use the shorter alias
> /speckit.adosync
```

The command will:

1. Ask for Azure DevOps configuration (if not already saved)
2. Parse user stories from `spec.md`
3. Display found stories and ask which ones to sync
4. Create Azure DevOps User Story work items
5. Display results with work item IDs and URLs

### Sync Tasks

```bash
# Sync tasks from tasks.md
> /speckit.adosync -FromTasks
```

The command will:

1. Parse tasks from `tasks.md`
2. Display found tasks grouped by User Story
3. Ask which tasks to sync (can select by User Story or task number)
4. Create Azure DevOps Task work items linked to parent User Stories
5. Display results

### Automatic Hook After Task Generation

After running `/speckit.tasks`, you'll be prompted:

```text
## Extension Hooks

**Optional Hook**: azure-devops
Command: `/speckit.azure-devops.sync`
Description: Automatically create Azure DevOps work items after task generation

Sync tasks to Azure DevOps? (yes/no)
```

## Configuration Reference

### Saved Configuration (`~/.speckit/ado-config.json`)

| Setting       | Type   | Required | Description                                               |
| ------------- | ------ | -------- | --------------------------------------------------------- |
| Organization  | string | Yes      | Azure DevOps organization name                            |
| Project       | string | Yes      | Azure DevOps project name                                 |
| AreaPath      | string | Yes      | Work item area path (e.g., "Project\\Team\\Component")      |
| LastUpdated   | string | No       | Timestamp of last configuration update (auto-maintained)  |

## Examples

### Example 1: First-Time Setup and Sync

```bash
# Step 1: Create specification
> /speckit.spec Create photo album management feature

# Step 2: Generate tasks
> /speckit.tasks

# Step 3: Sync to Azure DevOps (will prompt for configuration)
> /speckit.adosync
```

## Troubleshooting

### Issue: Azure CLI not found

**Solution**: Install Azure CLI:

- Windows: https://aka.ms/installazurecliwindows
- macOS: `brew install azure-cli`
- Linux: Follow guide at https://docs.microsoft.com/cli/azure/install-azure-cli

### Issue: Azure DevOps extension not installed

**Solution**: The extension will auto-install it when needed:

```bash
az extension add --name azure-devops
```

### Issue: Authentication failed

**Solution**: Authenticate with Azure CLI:

```bash
az login --use-device-code
```

### Issue: Permission denied when creating work items

**Solution**: Ensure you have Contributor or higher permissions on the Azure DevOps project.

### Issue: Command not available in AI agent

**Solutions**:

1. Check extension is installed: `specify extension list`
2. Restart your AI agent
3. Reinstall extension: `specify extension remove azure-devops && specify extension add azure-devops`

## License

MIT License - see [LICENSE](LICENSE) file

## Support

- **Issues**: https://github.com/github/spec-kit-azure-devops/issues
- **Spec Kit Docs**: https://github.com/github/spec-kit

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for version history.

---

*Extension Version: 1.0.0*  
*Spec Kit: >=0.1.0*  
*Azure CLI: >=2.0.0*
