# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repository Is

This is an **Appian application deployment package** (v26.3.107.0) — a configuration export from the Appian low-code BPM platform. It is **not** traditional source code. All files are XML-based declarative configuration metadata intended to be imported into an Appian server instance.

**System:** U.S. Department of Labor — Job Corps National Office (UMS UAT environment)

## Package Structure

- `META-INF/MANIFEST.MF` — Package version and creation timestamp
- `META-INF/export.log` — Export operation log listing all included items
- `adminSetting/` — 37 system administration configuration files (security, authentication, integrations, branding, email, data retention, etc.)
- `content/` — Binary branding assets (logo PNG, favicon ICO)
- `dataSource/` — JDBC connection configs for two Azure-hosted SQL Server databases
- `embeddedSailTheme/` — UI theme configuration (accent color, designer defaults)

## Deployment

There is no build system. This package is deployed by importing it through Appian's deployment/transport mechanism on the target Appian server.

- **Import:** Use Appian's "Compare & Deploy" or the Admin Console package import
- **Export:** Generate a new export via Appian's deployment interface; this repo should reflect the exported package state

## Tech Stack

- **Platform:** Appian v26.3.107.0
- **Database:** SQL Server (Azure-hosted at `20.122.91.182:1433`, database `sqlumsappiandev`)
- **Integrations:** Microsoft Azure OpenAI, HTTP/REST API logging, Outlook add-in
- **Auth:** Appian-native + MFA, 20-minute session timeout, password policy (min 7 chars, 1 numeric, 1 alphabetic, 4-password history)
- **Environment:** UAT (banner: `*** UMS UAT ***`)

## Key Configuration Files

| File | Purpose |
|---|---|
| `adminSetting/SYSTEM_BRANDING` | Login page branding, site name, banner message |
| `adminSetting/SYSTEM_AUTHENTICATION` | MFA, session timeout, password policies |
| `dataSource/jdbc_Azure*` | Database connection strings |
| `embeddedSailTheme/DEFAULT_DESIGNER_THEME` | UI accent color and theme |
| `adminSetting/SYSTEM_LOGGING_*` | HTTP, AI, and API request/response logging settings |

## Editing Guidelines

- All configuration files are XML; edit with care to preserve valid XML structure
- Appian uses its own serialization namespace (`urn:com.appian.types`)
- Sensitive values (passwords, connection strings) in `dataSource/` files should be managed via Appian's secure credential store rather than hardcoded in XML where possible
- Binary `content/` files must be replaced as a whole (re-export from Appian)
