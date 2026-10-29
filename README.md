# TLDix plugin for Claude

Track domain, hosting, SSL and licence renewals for all your clients from Claude.

This plugin adds:

- **TLDix connector** (`https://tldix.com/mcp`): domain lookups, bulk expiry checks and SSL checks without an account; your TLDix renewal list, adding and removing items with a free TLDix account (OAuth sign-in on tldix.com).
- **`renewal-report` skill**: everything that renews in a chosen window, grouped by urgency, with alert gaps flagged and optional client reminder drafts.
- **`domain-health-check` skill**: audit up to 25 domains for expiry, registrar lock and SSL problems.

## Install

In Claude Code:

```
/plugin marketplace add KominikeDigital/tldix-plugin
/plugin install tldix@tldix
```

Then run `/mcp` and sign in to TLDix when you want account tools.

In Claude (web and desktop) you can add the TLDix connector from the directory, or as a custom connector with the URL `https://tldix.com/mcp`.

## Links

- Documentation: https://tldix.com/claude
- Privacy policy: https://tldix.com/privacy-policy
- Support: hello@tldix.com

## License

MIT
