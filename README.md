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
