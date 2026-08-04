# Profile maintenance

## Monthly (5 minutes)

1. Update **Now** in `README.md` with what you’re actually shipping.
2. Add one line to **Recently shipped** (product nouns + month). Drop oldest if >5.
3. Confirm pins still tell the story (owned Nowah surfaces only).

## Never reintroduce

- Multicolor badge walls
- github-readme-stats / trophies / snakes / visitor counters
- Non-owned mega-star pins (fork cosplay)
- Dual public emails (keep `maslin@nowah.xyz` only)
- Hustle / “world-class” / peacock language

## Sidebar (GitHub → Settings → Public profile)

| Field | Value |
|-------|--------|
| Bio | `Founder of Nowah · AI travel that books · Singapore` |
| Website | `https://nowah.xyz` |
| Company | `@Nowah-xyz` |
| Location | Singapore |
| X | `maslinedwin` |

## Pins (order)

1. `Nowah-xyz/nowah-mcp-server`
2. `Nowah-xyz/nowah-go-sdk`
3. `Nowah-xyz/nowah-java-sdk`

Unpin anything else, especially third-party forks.

## One-time CLI (if `gh` has `user` scope)

```bash
gh auth refresh -h github.com -s user -s read:user -s repo -s read:org -s workflow
gh api user -X PATCH \
  -f bio='Founder of Nowah · AI travel that books · Singapore' \
  -f blog='https://nowah.xyz'
```

Pins still require the GitHub UI: **Customize your pins**.
