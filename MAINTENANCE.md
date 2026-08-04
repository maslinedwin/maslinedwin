# Profile maintenance

## Monthly (5 min)

1. Update **Now** with what you’re actually shipping.
2. Add one **Recently shipped** row (product nouns + period). Keep ≤5.
3. Confirm pins: owned Nowah surfaces only.

## Design system (don’t break)

| Token | Value |
|-------|--------|
| Jade | `#00A86B` / bright `#1FD08A` |
| Dark GH | `#0d1117` |
| Headers | `assets/header-dark.svg` + `header-light.svg` |
| Hero | `assets/nowah-hero.png` |
| Product | phone + web framed PNGs |

**One craft motion max.** No badge walls, stats cards, snakes, trophies, visitor counters.

## Sidebar (manual — needs `user` scope or UI)

| Field | Value |
|-------|--------|
| Bio | `Founder of Nowah · AI travel that books · Singapore` |
| Website | `https://nowah.xyz` |
| Company | `@Nowah-xyz` |

```bash
gh auth refresh -h github.com -s user -s read:user -s repo -s read:org
gh api user -X PATCH \
  -f bio='Founder of Nowah · AI travel that books · Singapore' \
  -f blog='https://nowah.xyz'
```

## Pins (GitHub UI → Customize your pins)

1. `Nowah-xyz/nowah-mcp-server`  
2. `Nowah-xyz/nowah-go-sdk`  
3. `Nowah-xyz/nowah-java-sdk`  

**Unpin** `google-gemini/gemini-cli` and any non-owned star cosplay.

## Regenerating assets

Product frames/hero are built from:

- iOS sim boarding-pass screenshot  
- nowah-web “Where to?” desktop screenshot  

Re-run the framing script when product UI meaningfully changes; keep dual-theme SVG headers brand-aligned.
