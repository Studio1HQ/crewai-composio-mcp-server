<div align="center">

<img src="https://raw.githubusercontent.com/Studio1HQ/Studio1HQ/main/assets/banners/crewai-composio-mcp-server.webp" alt="GitHub Analysis MCP Server with Composio: An MCP server that runs CrewAI agents through Composio and Nebius" width="100%" />

<br />
<br />

# GitHub Analysis MCP Server with Composio

### An MCP server that runs CrewAI agents through Composio and Nebius

A FastMCP server that exposes CrewAI workflows as MCP tools. Agents use Composio to read GitHub issues and PRs, build a Notion database and schedule bug review meetings in Google Calendar, with Nebius as the LLM.

<br />

[![Built by Studio1](https://img.shields.io/badge/Built_by_Studio1-f97316?style=for-the-badge&logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAxNjAgMTYwIiBmaWxsPSJub25lIj48cGF0aCBmaWxsLXJ1bGU9ImV2ZW5vZGQiIGNsaXAtcnVsZT0iZXZlbm9kZCIgZD0iTTAgMzVDMCAxNi42ODA3IDE0LjA3NDQgMS42NDg0NCAzMiAwLjEyNjk1M1YxNDFINTEuMDUyM0M1Mi40MzA4IDEzNy4zNDQgNTQuNzQ0NiAxMzMuNjg5IDU3Ljk5MzggMTMwLjAzM0M2MS4xNDQ2IDEyNi41MDggNjQuNjg5MiAxMjMuNDQgNjguNjI3NyAxMjAuODI5QzcyLjU2NjIgMTE4LjM0OSA3Ni4zNTY5IDExNi43ODIgODAgMTE2LjEyOVY4Ni43NTQ0Qzc1LjQ3MDggODcuOTI5MiA3MS4zODQ2IDg5LjY5MTkgNjcuNzQxNSA5Mi4wNDE1QzY0IDk0LjUyMjUgNjAuNzUwOCA5Ny40NiA1Ny45OTM4IDEwMC44NTRDNTYuNTM0NSAxMDIuNzIgNTUuMjU0NSAxMDQuNjU5IDU0LjE1MzkgMTA2LjY3MVYwSDEyNUMxNDQuMzMgMCAxNjAgMTUuNjY5OSAxNjAgMzVWMTI1QzE2MCAxNDQuMzMgMTQ0LjMzIDE2MCAxMjUgMTYwSDEyNFYxOEgxMDQuOTQ4QzEwMy41NjkgMjEuNjgxNiAxMDEuMjU1IDI1LjM2MjggOTguMDA2MiAyOS4wNDQ0Qzk0Ljg1NTQgMzIuNTk0MiA5MS4zMTA4IDM1LjY4NDEgODcuMzcyMyAzOC4zMTRDODMuNDMzOCA0MC44MTIgNzkuNjQzMSA0Mi4zODk2IDc2IDQzLjA0NzRWNzIuNjMwNEM4MC41MjkyIDcxLjQ0NzMgODQuNjE1NCA2OS42NzI0IDg4LjI1ODUgNjcuMzA1N0M5MiA2NC44MDc2IDk1LjI0OTIgNjEuODQ5MSA5OC4wMDYyIDU4LjQzMDdDOTkuNDY1NSA1Ni41NTEzIDEwMC43NDUgNTQuNTk4NiAxMDEuODQ2IDUyLjU3MjNWMTYwSDM1QzE1LjY3IDE2MCAwIDE0NC4zMyAwIDEyNVYzNVoiIGZpbGw9IiNmZmZmZmYiLz48L3N2Zz4K)](https://studio1hq.com)
[![Built with Composio](https://img.shields.io/badge/Built_with_Composio-141414?style=for-the-badge)](https://composio.dev)

[Composio docs](https://docs.composio.dev) &nbsp;·&nbsp; [Composio](https://composio.dev) &nbsp;·&nbsp; [Nebius](https://nebius.com) &nbsp;·&nbsp; [More examples](https://github.com/Studio1HQ) &nbsp;·&nbsp; [studio1hq.com](https://studio1hq.com)

</div>

<br />

## Overview

This repo is an MCP server that exposes multi-agent workflows as tools. It uses [CrewAI](https://www.crewai.com) agents, [Composio](https://composio.dev) for tool access to GitHub, Notion and Google Calendar, and a [Nebius](https://nebius.com) model as the LLM. The server is built with FastMCP and serves over SSE so it can handle workflows that take two to five minutes.

A full run analyzes a GitHub repository's issues and pull requests, creates a Notion database from the results, and schedules bug review meetings in Google Calendar for bug-labelled items. Composio supplies the authenticated GitHub, Notion and Google Calendar actions the agents call.

## Features

- **MCP tools over SSE**: FastMCP serves at `http://localhost:8080/sse`.
- **Full analysis**: `analyze_github_repository` runs GitHub analysis, Notion database creation and bug meeting scheduling in one call.
- **Step-by-step tools**: `fetch_github_data`, `create_notion_database` and `schedule_bug_meetings` run each stage on its own.
- **Status check**: `get_workflow_status` reports the server configuration.
- **Composio tools**: GitHub, Notion and Google Calendar actions are loaded through `composio_crewai`.
- **Nebius LLM**: agents use an OpenAI-compatible Nebius client.

## Tech stack

| Layer | Tool |
| --- | --- |
| Agents | [CrewAI](https://www.crewai.com) |
| Tools | [Composio](https://docs.composio.dev) with the CrewAI integration |
| LLM | [Nebius](https://docs.tokenfactory.nebius.com), OpenAI-compatible API |
| Protocol | [Model Context Protocol](https://modelcontextprotocol.io), FastMCP with SSE transport |
| Language | Python |

## Getting started

### Prerequisites

- Python 3.10 or later
- A Composio API key from [composio.dev](https://composio.dev), with GitHub, Notion and Google Calendar connected for the `default` entity
- A Nebius API key and a model name

### Installation

```bash
git clone https://github.com/Studio1HQ/crewai-composio-mcp-server.git
cd crewai-composio-mcp-server
pip install -r requirements.txt
```

### Environment variables

Create a `.env` file:

| Variable | Description |
| --- | --- |
| `COMPOSIO_API_KEY` | Composio API key. |
| `NEBIUS_API_KEY` | Nebius API key. |
| `NEBIUS_MODEL` | Nebius model ID used by the agents. No default. |
| `NEBIUS_BASE_URL` | Optional. Default `https://api.studio.nebius.ai/v1/`. |
| `DEFAULT_ATTENDEE_EMAIL` | Optional. Default recipient for meeting invitations. Set your own. |
| `TARGET_REPOSITORY` | Optional. Repository to analyze by default. Default `vercel/next-learn`. |

### Run

```bash
python mcp_server_wrapper.py
```

The server starts on `http://localhost:8080/sse`. Connect any MCP client to that URL. The repo includes test scripts such as `test_mcp_server.py` and `test_composio_setup.py` that check the server and the Composio connections before you connect a client.

## How it works

```text
mcp_server_wrapper.py   FastMCP server and tool definitions
agents/                 github_agent, notion_agent, calendar_agent (CrewAI)
tasks/                  CrewAI tasks per agent
workflow/               github, notion, calendar and full_orchestrator workflows
tools/composio_setup.py Composio toolsets for GitHub, Notion, Google Calendar
llm/nebius_client.py    Nebius OpenAI-compatible client
config/settings.py      environment settings
```

The full workflow runs in order: the GitHub agent collects issues and pull requests and analyzes them, the Notion agent creates a database and inserts the data, and the Calendar agent schedules review meetings for items labelled `bug`. Meetings default to 30 minutes.

| MCP tool | Description |
| --- | --- |
| `analyze_github_repository` | Full analysis with Notion database and bug meetings. |
| `fetch_github_data` | GitHub issues and pull requests only. |
| `create_notion_database` | Create a Notion database from provided GitHub data. |
| `schedule_bug_meetings` | Schedule meetings for bug-labelled items. |
| `get_workflow_status` | Server and configuration status. |

## Resources

- [Composio docs](https://docs.composio.dev) and [site](https://composio.dev): tool integrations for agents.
- [Nebius Token Factory docs](https://docs.tokenfactory.nebius.com): OpenAI-compatible inference.
- [CrewAI](https://www.crewai.com): multi-agent framework.
- [Model Context Protocol](https://modelcontextprotocol.io): the protocol this server implements.

<br />

---

<div align="center">

<a href="https://studio1hq.com">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Studio1HQ/website/main/brand/studio1-logo-on-dark.svg" />
    <img src="https://raw.githubusercontent.com/Studio1HQ/website/main/brand/studio1-logo-on-light.svg" alt="Studio1" width="160" />
  </picture>
</a>

Built by **[Studio1](https://studio1hq.com)**, the technical content and DevRel partner for devtool teams. Made with [Composio](https://composio.dev).<br />
Browse more open-source examples at [github.com/Studio1HQ](https://github.com/Studio1HQ).

[![Website](https://img.shields.io/badge/studio1hq.com-0b0807?style=for-the-badge&logo=googlechrome&logoColor=white)](https://studio1hq.com)
[![Book a call](https://img.shields.io/badge/Book_a_strategy_call-f97316?style=for-the-badge&logo=googlecalendar&logoColor=white)](https://cal.com/studio1/collab)
[![X](https://img.shields.io/badge/%40Studio1HQ-141414?style=for-the-badge&logo=x&logoColor=white)](https://x.com/Studio1HQ)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0a66c2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/company/studio1hq/)

<sub><a href="https://studio1hq.com">studio1hq.com</a> · Technical content, docs, video and DevRel for devtools</sub>

</div>
