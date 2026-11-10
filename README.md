# shopify-storefront

Theme source of truth for the Shopify storefront.

## How it works

- `main` on GitHub is connected to the Shopify theme (Shopify → Themes → ⋯ → Connect from GitHub).
- Push to `main` → Shopify syncs the connected theme (near-instant, editable only via git while connected).
- `origin` (Forgejo) is the private mirror/backup. `github` is the Shopify sync remote.

## Rules

- Theme files live at repo root: `layout/`, `sections/`, `snippets/`, `templates/`, `assets/`, `config/`, `locales/`.
- Do not edit the theme in Shopify admin while connected — git wins on every push.
- Keep `config/settings_data.json` edits intentional: it stores live customizer values.

## Game pages (metafield-driven)

Every product template gets two content sections (`sections/game-content.liquid`,
`sections/game-devlog.liquid`). They read per-game copy from **product metafields**,
so each game's text is edited in Shopify admin (Products → … → metafields), one field
per page section. Sections (and the whole page parts) render nothing while their
metafield is empty — non-game products are unaffected.

One-time setup in Shopify admin → Settings → Custom data → Products → Add definition:

| Name | Key | Type |
|---|---|---|
| Game description | `custom.game_description` | Rich text |
| Micro manual | `custom.game_manual` | Rich text |
| Game history & references | `custom.game_history` | Rich text |
| Devlog tag | `custom.blog_tag` | Single line text |

Devlog posts: `game-devlog` shows the newest posts from the **devlog** blog whose tags
match the product's `custom.blog_tag` (case-insensitive), falling back to the product
handle when the metafield is empty. So for each game: tag its devlog posts with the
handle (e.g. `koro`, `fungus-foray-dx`) and optionally set the metafield explicitly.

Section headings are editable in the theme editor (Customize → product page),
but the copy itself lives in the metafields, not the theme.

KORO paste-ready content: `docs/koro-metafields.html` (open in a browser, copy each
dashed block into the matching metafield).
