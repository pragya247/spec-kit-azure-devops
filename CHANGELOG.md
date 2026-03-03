# Changelog

All notable changes to the Azure DevOps Integration extension will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-03-03

### Added

- Initial release of Azure DevOps Integration extension
- User Story sync from spec.md to Azure DevOps User Story work items
- Task sync from tasks.md to Azure DevOps Task work items
- OAuth authentication via Azure CLI (no PAT tokens required)
- Interactive configuration with persistence to `~/.speckit/ado-config.json`
- Work item mapping tracker in `.speckit/azure-devops-mapping.json`
- Automatic priority mapping (P1-P4 to Azure DevOps priorities)
- Task-to-User Story automatic linking via `[US#]` references
- Hook integration with `/speckit.tasks` command
- Support for both bash and PowerShell scripts
- Interactive selection of which items to sync
- Real-time progress feedback during sync
- Summary table with work item IDs and URLs

### Documentation

- Comprehensive README with usage examples
- Configuration reference
- Troubleshooting guide
- Field mapping documentation

### Scripts

- Bash script: `scripts/bash/create-ado-workitems.sh`
- PowerShell script: `scripts/powershell/create-ado-workitems.ps1`

[1.0.0]: https://github.com/github/spec-kit-azure-devops/releases/tag/v1.0.0
