# Claude / Anthropic Rules for Clash

Complete **Clash (Mihomo) rule set** for Claude / Anthropic services — merged and deduplicated from multiple authoritative sources, with official ASN / IP prefix coverage from BGP.

## Files

| File | Description |
|---|---|
| [`rules/anthropic.yaml`](rules/anthropic.yaml) | **Core rules** — first-party Anthropic domains + official ASN/IP prefixes. Recommended for most users. |
| [`rules/anthropic-full.yaml`](rules/anthropic-full.yaml) | **Full rules** — core + third-party dependencies (fonts, CDN, telemetry, support widgets). Some entries are shared services — read the warning inside. |

## What's covered

### Domains (19 core)

```
anthropic.com          anthropic.com.cn       antspace.dev
clau.de                claude.ai              claude.app
claude.com             claude.new             claude.site
claudemcpclient.com    claudemcpcontent.com   claudepages.dev
claudestudio.com       claudeusercontent.com  claude.dev
modelcontextprotocol.com / .io / .net / .org
```

### Network (Anthropic, PBC — official registration)

| Type | Value |
|---|---|
| ASN | `AS399358` (also registered: AS60808, AS4167, AS401551) |
| IPv4 | `160.79.104.0/21` (includes /22, /23, /24 sub-prefixes) |
| IPv6 | `2607:6bc0::/32` |

## Usage

### As a rule-provider (recommended)

```yaml
rule-providers:
  anthropic:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/<owner>/<repo>/main/rules/anthropic.yaml"
    path: ./ruleset/anthropic.yaml
    interval: 86400

rules:
  - RULE-SET,anthropic,<YOUR-PROXY-GROUP>
```

### As inline rules

Copy the `payload:` entries directly into your `rules:` section (remove the `payload:` line, keep the `- ` items).

## Notes

- **Cloudflare CDN**: `claude.ai` and `anthropic.com` resolve to Cloudflare IPs, so **domain rules are the primary coverage** — IP rules are a backup for direct-IP connections.
- **IPv6**: If your config uses a global IPv6 block rule (e.g. `IP-CIDR6,2000::/3,REJECT`), Anthropic's IPv6 range will be caught by it first. Either accept IPv4-only for Claude, or place the Anthropic IPv6 rule before the global block.
- **GeoIP database**: `IP-ASN` rules require a GeoIP database (Mihomo ships with one).
- **Privacy**: route this rule set to a clean residential-IP proxy group if you care about account risk control.

## Sources

- [MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat) — geosite/anthropic
- [v2fly/domain-list-community](https://github.com/v2fly/domain-list-community) — data/anthropic
- [VPSDance/ai-proxy-rules](https://github.com/VPSDance/ai-proxy-rules) — rules/clash/anthropic.yaml
- [tanitany/claude-quantumultx-rules](https://github.com/tanitany/claude-quantumultx-rules) — Anthropic-Full.list
- [BGP.he.net](https://bgp.he.net/) — ASN & prefix lookup (Anthropic, PBC)

## License

MIT