# Security and Privacy

This repository is a sanitized portfolio case study.

Do not publish files from a real agent runtime without reviewing them first.

## Never Commit

- credentials
- tokens
- `.env` files
- messaging configuration
- MCP server secrets
- browser profiles
- raw traces
- memory indexes
- private diaries
- user profile records
- local automation commands
- screenshots from private sessions

## Recommended Review

Before publishing a derivative repository, run a secret and path scan for:

- API keys
- bearer tokens
- chat IDs
- local absolute paths
- private IPs
- webhook URLs
- personal names or addresses
- raw conversation logs

## Scope

The prompt patterns here can reduce behavioral leakage, but they are not a security sandbox.
Runtime systems still need proper authentication, authorization, tool allowlists, output filtering, and audit logging.

