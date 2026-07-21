# ⚽ Brandable Penalty Shootout Game

A single-file, self-contained HTML penalty shoot-out game built for events,
trade shows and marketing activations. One player takes a set of penalties,
sees their score, and can have it **emailed to them** together with your
branding, a promo message, a discount code and a call-to-action link.

No build step, no framework, no server required — just open `index.html`.

---

## ✨ Features

- **Playable penalty shootout** — tap a target zone, stop the power bar, beat the keeper.
- **Fully brandable** — add your logo, company name, tagline and a custom colour scheme.
- **Live customisation panel** — click the ⚙️ gear icon in-game to change everything without touching code.
- **Email the score** — results are emailed to the player via [EmailJS](https://www.emailjs.com) (free, no backend).
- **Promotional email content** — include a prize/discount code, marketing copy, and a CTA button/link.
- **Lead capture** — name, email, optional phone and a marketing opt-in checkbox. Leads are stored in the browser and (if configured) emailed to your team.
- **Export tools** — download a JSON config or a fully-branded standalone HTML file to deploy.
- Works great on phones/tablets (kiosk-friendly) and desktop.

---

## 🚀 Quick start

1. Open `index.html` in any browser (or host it — see **Deploy** below).
2. Click the **⚙️ gear icon** (top-right).
3. Set your **branding, colours, promo text and email settings**.
4. Click **Save & apply**. That's it.

To keep your settings permanently (rather than only in the current browser),
use **Download game** in the settings panel — it produces a new
`penalty-shootout-branded.html` with your configuration baked in.

---

## 📧 Setting up email (EmailJS)

The game sends the player's score by email straight from the browser using
EmailJS, so you don't need to run any server.

1. Create a free account at **https://www.emailjs.com**.
2. **Add an Email Service** (Gmail, Outlook, your SMTP, etc.) → note the **Service ID**.
3. **Create an Email Template** → note the **Template ID**.
4. Copy your **Public Key** from *Account → API Keys*.
5. In the game, open **⚙️ → Email** and paste the **Public Key**, **Service ID**
   and **Template ID**. (Optionally add a "notify address" to CC your sales team.)

### Template variables

When you design your EmailJS template, these variables are sent and can be used
with `{{double_braces}}`:

| Variable | Meaning |
|---|---|
| `{{to_name}}` | Player's name |
| `{{to_email}}` / `{{player_email}}` | Player's email (set this as the "To" address in EmailJS) |
| `{{phone}}` | Phone number (if collected) |
| `{{score}}` | Goals scored |
| `{{total}}` | Total penalties |
| `{{percent}}` | Score as a percentage |
| `{{results}}` | Shot-by-shot summary (⚽ / ✗) |
| `{{brand_name}}` | Your company name |
| `{{promo_text}}` | Your promotional headline |
| `{{promo_code}}` | Discount / prize code |
| `{{cta_text}}` / `{{cta_url}}` | Call-to-action button text + link |
| `{{opt_in}}` | Whether they ticked the marketing opt-in (Yes/No) |
| `{{date}}` | When they played |
| `{{notify_email}}` | Your internal notification address |

A ready-to-paste HTML email template is provided in
[`email-template.html`](email-template.html).

> **No EmailJS configured?** The game still works — it saves the lead in the
> browser and offers the player a "mailto" link to email their own score.

---

## 🎨 What you can customise

Open **⚙️** in-game. Tabs:

- **Branding** — company name, logo (upload or URL), tagline.
- **Colours** — primary, secondary, accent/highlight, background, panel surface, text, keeper kit. Live preview.
- **Promo** — prize/promo headline, discount code, CTA button text + link, marketing opt-in wording.
- **Email** — EmailJS keys + optional internal notify address.
- **Game** — number of penalties (3/5/7/10), keeper difficulty (easy/normal/hard), whether to ask for a phone number.

Developers can also edit the `DEFAULT_CONFIG` object near the top of the
`<script>` in `index.html`.

---

## 📊 Retrieving captured leads

Every result (even without EmailJS) is stored in the browser under the
`penaltyLeads` localStorage key. On a kiosk you can retrieve them via the
browser console:

```js
JSON.parse(localStorage.getItem("penaltyLeads"))
```

For a proper CRM/marketing pipeline, the recommended route is to point your
EmailJS template (or the `notify_email` field) at your own inbox / automation
tool so each play is delivered to you in real time.

---

## 🌐 Deploy

Because it's a single file, you can host it anywhere static:

- Drag `index.html` into **Netlify Drop**, **Vercel**, **Cloudflare Pages**, or **GitHub Pages**.
- Or run locally: `python3 -m http.server` and open `http://localhost:8000`.

For an event kiosk, open it full-screen (F11) on a tablet in guided-access /
kiosk mode.

---

## 🕹️ How to play

1. **Tap the part of the goal** you want to aim at (6 zones).
2. A **power bar** starts moving — tap **Shoot!** to stop it. Aim for the
   middle-to-high range: too weak and it won't reach, maxed out and it may
   fly over.
3. Beat the keeper across all penalties, then enter your details to get your
   score emailed to you.

---

## 🔒 Notes

- All logic runs client-side. EmailJS keys are "public" keys designed for
  browser use; restrict allowed domains/rate limits in your EmailJS dashboard.
- Uploaded logos are stored as data URLs in the config, so exported
  branded files are fully portable.
