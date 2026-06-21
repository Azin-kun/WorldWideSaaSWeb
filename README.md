# WorldWideSaaS — Public Website (Homeslice)

The public, data-driven website for the **Business OS** platform. It renders live
from the Supabase project the POS app writes to, so the owner edits everything
from the mobile app (**Website** screen) and it appears here — no code changes.

## What it shows
- **Theme** — palette + fonts come from `website_theme` and are applied to CSS
  variables at load (`--esp`, `--brn`, `--gld`, `--crm`, `--ff`, `--fs`, …).
- **Content** — hero, story/about, hours, contact come from `website_sections`
  (title / body / image / structured `content`). Sensible defaults show if a
  section hasn't been filled in yet.
- **Menu** — pulled live from `catalog_items` + `categories` + options
  (variant items show a "from" price).
- **Reservations** — the form calls the `create_public_booking` RPC, which lands
  in the POS app's **Incoming** feed (the cashier's 🔔) as a new reservation.
- **Chat assistant** — a temporary placeholder widget (quick actions work; free
  chat is wired to be added later).

Everything reads with the **publishable (anon) key** only — no secrets here.

## Configuration
Edit the `CONFIG` block near the top of the `<script>` in `index.html`:

```js
const SUPABASE_URL = 'https://gfekclkhdrqyncmvnjsn.supabase.co';
const SUPABASE_ANON_KEY = 'sb_publishable_…';   // publishable/anon — public-safe
```

These are public by design (anon key, protected by Row-Level Security). The
`service_role` key must **never** appear here.

## Hosting (GitHub Pages)
This is a single static `index.html` — no build step.
1. Push to `main`.
2. Repo **Settings → Pages → Source: Deploy from a branch → `main` / root**.
3. The `.nojekyll` file makes Pages serve files as-is.

## Connecting to the editor
The data this site reads is produced by the POS app:
- **Website screen → Theme tab** → `website_theme`
- **Website screen → Content tab** → `website_sections`
- **Manage products** → `catalog_items` (the menu)

Reservations created here flow back into the app's **Incoming** screen.
