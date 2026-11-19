# BallooonVan website

Official website for Karida's BallooonVan (face painting, balloon twisting,
party decoration) — Vancouver & beyond. Static site, $0 hosting on Cloudflare
Pages, content editable by Karida via Sveltia CMS, code editable by Muse via Git.

## What's in here

- `index.html` — the whole public site (single page: services, showcase,
  Instagram carousel, pricing, booking form, contact). Content loads from
  `content/*.json` with built-in fallbacks, so the page works even if a JSON
  file is missing.
- `assets/gallery/` — photos (compressed, max 1200px). Photos showing
  children's faces are fine when the owner asked the child (or parent) and
  got consent before taking the photo (policy changed 2026-11-19, see
  Content rules). If anyone later asks for a photo to be removed, take it
  down.
- `content/settings.json` — phone, email, prices, service area (editable in CMS).
- `content/gallery.json` — gallery photos, captions, categories (editable in
  CMS, but the Gallery section was removed 2026-11-19 — this file is dormant
  and not displayed; the Instagram carousel in `content/instagram.json` is
  the only photo display).
- `content/instagram.json` — Instagram carousel photos, captions and post
  links (editable in CMS under **Instagram Carousel** — drag the photos to
  reorder them; the site shows them in that order).
- `assets/whatsapp-icon.png` — WhatsApp mark used in the Contact
  section (official logo, grey outer ring removed 2026-11-19).
- `admin/` — Sveltia CMS admin page + config (`/admin` on the live site).

## How Karida edits the site (no code)

1. Open `https://ballooonvan.com/admin` (or the `.pages.dev` URL before the
   domain is attached) and sign in with GitHub. Sveltia accepts a fine-grained
   personal access token (PAT) for sign-in — no OAuth App needed.
2. Edit **Site Settings** (phone, prices, wording), **Instagram Carousel**
   (drag photos to reorder, or add/remove photos) or **Photo Gallery**
   (dormant — the Gallery section was removed, so edits here do nothing
   visible) and save. Saving commits to GitHub; Cloudflare Pages rebuilds
   automatically (about a minute).
3. Photos uploaded through the CMS land in `assets/gallery/`.

## How Muse edits the site (code + content)

Muse pushes to the same repo with a fine-grained PAT (repo Contents: read &
write, scoped to this repo only) stored in the Secure Vault. Design, layout,
new sections and fixes go through git; content files stay CMS-compatible
(keep the JSON keys and structure unchanged unless the page JS is updated too).

## Setup checklist (first publish)

1. **GitHub repo**: create public repo `ballooonvan-website` under
   `karidazhang-beep`. Push this directory's contents to `main`.
2. **Muse push access**: Karida creates a fine-grained PAT (GitHub Settings →
   Developer settings → Personal access tokens → Fine-grained tokens, scope:
   this repo only, Contents read & write) and enters it via Muse's Secure
   Vault. Commit emails use GitHub's private noreply address.
3. **Cloudflare Pages**: free account → Workers & Pages → Create → Pages →
   Connect to Git → repo `ballooonvan-website`, branch `main`, build command
   empty, output directory `/`. Free plan: unlimited bandwidth/requests.
4. **Domain**: buy `ballooonvan.com` ($11.81/yr) and/or `ballooonvan.ca`
   ($8.63 first year promo) on Porkbun (both available, checked 2026-11-17).
   In Cloudflare Pages → Custom domains, attach it; update the `url` in the
   JSON-LD block in `index.html` if the final domain differs.
5. **Booking form**: the form currently opens the visitor's email app
   (mailto to `ballooonvan@yahoo.com`). To switch to direct submissions, create
   a free Tally form (tally.so) and replace the form's submit handler — see
   "Tally" note below. Do this after launch if preferred.
6. **Google Business Profile**: create the free GBP listing pointing at the
   live site (see the discoverability goal notes). Helps parents find the
   business on Google Maps / "face painting near me" searches.

## Local preview

```sh
cd ballooonvan-site
python3 -m http.server 8000
# open http://localhost:8000
```

Note: `/admin` (Sveltia) needs the live GitHub-backed deployment to sign in;
locally it loads but cannot authenticate.

## Tally form (later step)

Tally's free plan: unlimited forms and submissions. Create a form with the
same fields as the booking form (name, contact, date, time, address, services,
hours, kids, message), set email notifications to `ballooonvan@yahoo.com`, and
either link the site's Book button to the Tally URL or embed the form. Keep
the mailto form as fallback until Tally is verified live.

## Content rules (owner's decisions, 2026-11-17)

- Phone 778-881-4661 is public, marked "Text preferred".
- Pricing IS shown: $120/hr face painting and balloon twisting; travel fee by
  distance (no zone prices decided — never invent them).
- Party Decoration stays in outward copy (owner outsources it) — custom quote.
- Face painting + balloon twisting can be booked together; combined-booking
  price is UNCONFIRMED — the site says "Book both together!" with no invented
  total. Update if the owner confirms a combo rate.
- Service area: Metro Vancouver & beyond — other places welcome.
- Children's faces ARE allowed in photos (policy changed 2026-11-19): the
  owner asks each child (or parent) and gets consent before taking the photo.
  If a parent or child later asks for a photo to be removed, take it down.
  Two carousel photos (2026-10-19 princess collection, 2025-06-02 Alice party)
  and the face-painting showcase collage still carry the old BALLOOON STUDIO
  watermark — published as-is, same as the 2026-11-18 collage exception.
- Brand spelling: **Ballooonvan** (three o's) / BallooonVan.
