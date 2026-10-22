# Airframe for Claude

Airframe grounds Claude's answers about software companies, products, and
markets in Airframe's live catalog of 7,300+ software products and network of
30,000+ practitioners, instead of training data that goes stale on pricing,
funding, and competitor sets within months.

Ask Claude things like:

- "Tell me about Decagon and who it competes with."
- "What does Zendesk cost, and how does that compare with Intercom?"
- "Map the customer-service AI agent market for a board slide."
- "Find practitioners who have deployed Gong at enterprise scale."
- "Write a sales email positioning us against our top competitor."

## What's in this plugin

- **The Airframe connector**, a remote MCP server at
  `https://mcp.airframe.ai/mcp`. It exposes seven read-only tools:

  | Tool | What it does |
  |---|---|
  | `search_products` | Search the catalog by keyword, category, or department |
  | `get_product_details` | Full profiles of 1–5 products: vendor, funding, features, integrations, pricing, compliance, reviews, alternatives |
  | `find_experts` | Find anonymized practitioner profiles by expertise or product experience |
  | `ask_airframe` | Ask a free-form question answered from the catalog, with sources |
  | `get_my_usage` | Show your team's usage and quotas |
  | `list_market_reports` | List the market reports your team is entitled to |
  | `read_market_report_section` | Read one section of an entitled market report |

  None of the tools create, change, or delete anything.

- **The `company-research` skill**, which tells Claude when to use Airframe
  (any answer that states facts about a specific software company), how to
  chain the tools, and a consistent format for vendor briefs and battlecards.

## Getting started

1. Install the plugin from the Claude directory. In Claude Code you can
   also run `/plugin install airframe --marketplace airframeai/claude-plugin`.
2. When Claude first calls an Airframe tool, sign in with your Airframe
   account (OAuth). Don't have one? Sign up at
   [airframe.ai](https://www.airframe.ai).
3. Ask a question about any software company or market.

Setup for 18 clients, the tools reference, and troubleshooting: [airframe.ai/docs](https://www.airframe.ai/docs).

## Data and privacy

The plugin installs no code on your machine and runs no local commands or
hooks. When Claude calls an Airframe tool, it sends that tool's arguments (for
example a product name, search keywords, or the question passed to
`ask_airframe`) to `mcp.airframe.ai` over HTTPS, authenticated as your Airframe
account. Airframe records each call against your team's usage quota. Airframe
doesn't read your Claude conversation history, memory, or files.

See the [Airframe Privacy Policy](https://www.airframe.ai/compliance/privacy-policy)
and [Terms of Service](https://www.airframe.ai/compliance/terms-of-service).

## Support

Email [support@airframe.ai](mailto:support@airframe.ai).
