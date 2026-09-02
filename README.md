



# He Is Risen — Website

A Next.js site for the He Is Risen project: home, the paintings, the
artist, vision/about, get involved (donate + advisory board), and contact.

## Run it locally

You'll need [Node.js](https://nodejs.org) 18+ installed.

```bash
npm install
npm run dev
```

Then open http://localhost:3000.

## Deploy on Vercel (no local setup required)

1. Create a free GitHub account if you don't have one, and create a new
   empty repository (e.g. `he-is-risen-site`).
2. Upload this whole folder's contents to that repository (GitHub's web
   UI lets you drag-and-drop files if you don't want to use git directly).
3. Go to [vercel.com](https://vercel.com) → sign up (free) → **Add New
   Project** → import the repository you just created.
4. Leave the default settings — Vercel auto-detects Next.js. Click
   **Deploy**.
5. In a few minutes you'll get a live URL (like `he-is-risen.vercel.app`).
   You can attach your real domain (e.g. `heisrisen.org`) under
   **Project Settings → Domains**.

Every time you push a change to the repository, Vercel redeploys
automatically.

## Replacing placeholder content

- **Paintings**: edit `lib/paintings.ts` with real titles, years,
  dimensions, and descriptions.
- **Painting images**: each painting currently shows a textured
  placeholder (see `components/PaintingPlaque.tsx`). Once you have
  photography, add the images to `/public/paintings/` and swap the
  placeholder `<div>` for a Next.js `<Image>` component.
- **Artist bio / photo**: edit `app/artist/page.tsx`.
- **Board of Directors**: edit `app/about/page.tsx`.
- **Colors/fonts**: `tailwind.config.js` and `app/layout.tsx`.

## Connecting real donations

The donate section on `/get-involved` currently shows a placeholder box.
The two fastest ways to make it live:

**Option A — Donorbox (simplest, no code)**
1. Create a free account at [donorbox.org](https://donorbox.org) and set
   up a campaign for the project.
2. Donorbox gives you an embed `<iframe>` snippet.
3. In `app/get-involved/page.tsx`, replace the placeholder `<div>` in the
   "DONATION EMBED SLOT" comment with that snippet.

**Option B — Stripe Payment Links**
1. Create a free [Stripe](https://stripe.com) account and set up a
   Payment Link for donations (supports one-time and recurring giving).
2. Replace the placeholder with a link/button pointing to that Payment
   Link URL, or embed Stripe's checkout button code.

Either option takes about 10–15 minutes to set up and requires no
further code changes beyond pasting in the snippet.

## Connecting the forms (advisory board / contact / newsletter)

All three forms on the site currently POST to `/app/api/inquiry/route.ts`,
which validates the submission and logs it — it does not yet send an
email or save to a list. To make it functional:

1. Create a free account at [resend.com](https://resend.com) (recommended
   — simplest email API) and get an API key.
2. In Vercel, go to **Project Settings → Environment Variables** and add
   `RESEND_API_KEY`.
3. In `app/api/inquiry/route.ts`, uncomment the `fetch(...)` block and
   set the `to` address to the board's real inbox.

Alternatively, a no-code option is to swap the `endpoint` prop on each
`<InquiryForm>` to a [Formspree](https://formspree.io) form URL — their
free tier requires no backend code at all.
