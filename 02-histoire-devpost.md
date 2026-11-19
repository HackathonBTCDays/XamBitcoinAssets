# 02 · Histoire Devpost (texte anglais à coller)

> Ce fichier contient **tout ce qu'il faut coller dans Devpost** : accroche, histoire en Markdown (les 7 titres de Devpost), étiquettes « Built with », liens « Try it out ». Le texte à coller est en anglais, le reste du fichier en français. Chaque chiffre vient du dépôt (`docs/TESTING.md` mesuré le 2026-11-19, `docs/DATABASE_MODEL.md`, `docs/BUSINESS_RULES.md`, `docs/DEPLOYMENT.md`, `docs/LESSONS_LEARNED.md`, `XamBitcoin_Proposition_Concrete.md`) ou des essais réels du 2026-11-19 décrits dans [`06-captures-et-medias.md`](06-captures-et-medias.md). Fiche de ce qui est réel ou non : [`05-reel-simule-vision-et-jury.md`](05-reel-simule-vision-et-jury.md). Sources Mermaid de tous les schémas : [`07-schemas-mermaid.md`](07-schemas-mermaid.md).

---

## 1. Champs courts

| Champ Devpost | Valeur |
|---|---|
| Project name | `XamBitcoin` |
| Elevator pitch (200 caractères maximum) | `Learn Bitcoin by using it: six 3-minute missions with real Lightning micro-sats, then launch a real fundraising campaign. Live on mainnet with LNbits and phoenixd.` (163 caractères) |
| Built with (25 maximum) | `typescript`, `nestjs`, `typeorm`, `postgresql`, `react`, `vite`, `tailwindcss`, `lnbits`, `phoenixd`, `lightning-network`, `bitcoin`, `lnurl`, `docker`, `caddy`, `cloudflare-pages`, `github-actions`, `jest`, `vitest` (18 sur 25) |
| Try it out | `https://xambitcoin.com` (portail en ligne) et `https://github.com/HackathonBTCDays/XamBitcoin` (dépôt, **à rendre public avant l'envoi**) |
| Vidéo | lien YouTube ou Vimeo (à produire : voir [`03-script-video.md`](03-script-video.md)) |
| Vignette et galerie | images de [`06-captures-et-medias.md`](06-captures-et-medias.md), 15 au plus, 5 Mo au plus chacune |

---

## 2. Histoire à coller (Markdown, anglais)

Les images sont des liens vers le dépôt public. Elles ne s'affichent qu'**après la fusion de la branche dans `main` et le passage du dépôt en public**. Tant que ce n'est pas fait, téléversez les mêmes fichiers (dossier `docs/pitch/media/`) avec l'éditeur de Devpost (glisser-déposer). Les schémas sont des **images PNG** : **Devpost n'affiche pas Mermaid** (essayé par le propriétaire, un bloc `mermaid` ne s'affiche pas en dessin). Devpost accepte les titres, le gras, l'italique, les citations, les listes, les tableaux, les blocs de code, les images et les cases à cocher : c'est tout ce que ce texte utilise. Les sources Mermaid restent dans [`07-schemas-mermaid.md`](07-schemas-mermaid.md) pour GitHub.

````markdown
# XamBitcoin - Learn Bitcoin by using it

**Learn Bitcoin. Use it. Build with it.** Live at [xambitcoin.com](https://xambitcoin.com), running on Bitcoin mainnet.

---

## Inspiration

Bitcoin and Lightning are easy to describe and hard to *feel*. **What is a sat? What does an invoice really contain? Why does a payment sometimes cost a few extra sats? Who actually holds the keys of the wallet in my phone?** Even people who follow Bitcoin closely stay unsure about some of these mechanisms, and most tutorials make it worse in two ways:

1. **They explain first and let you try later**, so the explanation lands on nothing.
2. **They send you to a test network**, where nothing is at stake and nothing is real, so you never learn what a real fee or a real expiry feels like.

We lived this ourselves: some mechanisms stayed blurry until we saw a real payment go through with real figures. That is the idea behind XamBitcoin:

> **You do a real operation first. Then the app explains what just happened, using the real figures of your own payment.**

The second inspiration is what comes *after* learning. In Dakar and across Africa, communities already pool money: a student association equipping a computer lab, a neighbourhood fund, a small shop selling on credit, a savings circle. Lightning is the natural rail for these small, frequent, borderline-free payments. So **the last learning mission is the first real action of the product: launching a fundraising campaign**, and the same base can later carry more modules.

We built it for the **Dakar Bitcoin Hack**.

---

## What it does

XamBitcoin is **one common Bitcoin and Lightning base** (wallet, payment engine, double-entry ledger, receipts, treasury) with **three layers** on top:

![Learn, Use, Build and the common base](https://raw.githubusercontent.com/HackathonBTCDays/XamBitcoin/main/docs/pitch/media/40-learn-use-build.png)

### Learn: six missions of three minutes

Every mission follows the same loop: **context, real action, verification by the backend, real result, written explanation.**

![The mission loop](https://raw.githubusercontent.com/HackathonBTCDays/XamBitcoin/main/docs/pitch/media/41-mission-loop.png)

| # | Mission | What the learner does | What is explained afterwards | Status on the live site |
|---|---|---|---|---|
| 1 | **What is a sat?** | A 3-question quiz, graded by the server | 1 BTC = 100,000,000 sats; Lightning = fast, cheap payments on top of Bitcoin | **Real** |
| 2 | **Your wallet** | Activates the starter wallet, sees a 0 balance | It is a *starter* wallet: we hold the keys; keep savings in a wallet where you hold your seed; **we never ask for a seed** | **Real** |
| 3 | **Receive your first sats** | Asks for the reward: an invoice of 21 sats is created in the learner's wallet and paid | What an invoice contains: amount, description, **expiry** | **Real, 21 sats on mainnet** |
| 4 | **The QR that works many times** | Creates a LNURL-pay link and has it paid twice | One invoice = one payment; LNURL-pay creates a **new invoice at every scan**, ideal for donations | Built and tested, **not tried on the live site yet** |
| 5 | **Pay your first invoice** | Pays a 10-sat invoice from an **external wallet** | Amount sent vs total debited; routing fees are paid by the sender | Built and tested, **not tried on the live site yet** |
| 6 | **Launch your Naatal campaign** | Creates a campaign: public page, permanent QR | How the app learns a donation arrived; the fee line is shown **before** the donation | The campaign page is **real**; the mission itself is not offered on the live site yet |

Missions 4 and 5 can be skipped; skipping the reception mission forces the outgoing one to be skipped too. Explanations are **texts written in advance** (no AI runs on the server); only the figures come from the real payment, and the screen says so ("Written in advance, not generated by an AI").

![Mission 3 done, with the real figures of the payment](https://raw.githubusercontent.com/HackathonBTCDays/XamBitcoin/main/docs/pitch/media/31-mission3-apres.png)

### Use: a starter wallet and Naatal

**The starter wallet** is custodial and capped (100,000 sats): XamBitcoin is **not a bank**, the app never asks for a seed phrase or a private key, and withdrawal to a wallet you control is free of commission (only real network fees).

![Balance of 21 sats after the real reward](https://raw.githubusercontent.com/HackathonBTCDays/XamBitcoin/main/docs/pitch/media/32-tableau-de-bord-21-sats.png)

![The transaction list: Learn reward, +21 sats, settled](https://raw.githubusercontent.com/HackathonBTCDays/XamBitcoin/main/docs/pitch/media/33-finance-transaction.png)

**Naatal** (the only module of the MVP) turns what was learned into something useful: a **fundraising campaign** with a title, a goal in sats, a public link, a **permanent LNURL-pay QR**, a **Lightning address** and a progress bar. Any Lightning wallet can pay: no app to install for the donor.

![Creating a campaign](https://raw.githubusercontent.com/HackathonBTCDays/XamBitcoin/main/docs/pitch/media/15-campagne-formulaire.png)

**The service fee is shown before the donation**, never after:

> *"You pay 1,000 sats, of which 10 sats of XamBitcoin service fee (1 %, min 1, max 500). 990 sats go to the campaign owner."*

![A live Naatal campaign page: the fee is shown before paying](https://raw.githubusercontent.com/HackathonBTCDays/XamBitcoin/main/docs/pitch/media/17-campagne-frais-avant-paiement.png)

### How the platform earns (and what it never charges)

| Flow | Commission |
|---|---|
| Personal reception into a wallet | **None** |
| Withdrawal or sending | **None**, only real network fees |
| Donation to a Naatal campaign | Configurable rule: **percentage + minimum + maximum** (starting value 1 %, min 1 sat, max 500 sats: a teaching value, still to be tuned with real testers) |

The commission goes to the **Treasury**, which holds **only earned revenue, never user funds**.

![Example: a 10,000-sat donation, 100 sats to the Treasury](https://raw.githubusercontent.com/HackathonBTCDays/XamBitcoin/main/docs/pitch/media/42-commission-treasury.png)

### Build (later)

API keys, "payment received" webhooks, and LNURL-pay, withdraw and auth tools for developers. Today only a preview page exists: **nothing of Build is built yet.**

### Honest by design

Demo pages are labelled **"Demonstration data"** and never mix with real payments. The "demonstration" preview of the tutorial sends no payment at all.

![The tutorial preview: no money, clearly labelled](https://raw.githubusercontent.com/HackathonBTCDays/XamBitcoin/main/docs/pitch/media/04-apercu-tutoriel.png)

---

## How we built it

### Stack at a glance

| Layer | Choice | Why |
|---|---|---|
| Payment engine | **LNbits 1.6.2** on top of a **phoenixd 0.9.3** node, **mainnet** | One wallet per user, LNURL-pay, webhooks; phoenixd is a light node we can operate alone |
| Backend | **NestJS**, **TypeORM**, **PostgreSQL** | Modules by domain, migrations written as TypeScript classes, validation on every input |
| Portal | **Vite**, **React**, **Tailwind** | Static build, fed by one shared package |
| Shared contract | `packages/shared` | Mission sheets, texts and design tokens in one place: the portal never re-defines a rule |
| Production | **Docker Compose**, **Caddy**, a small server, **Cloudflare Pages** | One public door, automatic HTTPS |
| Quality | **Jest**, **Vitest**, GitHub Actions | Tests on every pull request |

### 1. The payment engine: LNbits and phoenixd

- **One LNbits wallet per user**, one for each **campaign**, one for the **Treasury** and one for the **learning budget** that pays the 21-sat rewards.
- **LNURL-pay**: a static QR code that creates a new invoice at every scan. The campaign link is built on the public domain, and the **Lightning address** (`<campaign-link>@api.xambitcoin.com`) is served by the API.
- **phoenixd** is a Lightning node for mainnet, run as an official container **with no public port**: only LNbits can talk to it.

### 2. The backend: the only component that touches the money

The NestJS API is the only component that talks to LNbits and holds the admin keys. Main routes (all validated, JWT-protected unless public):

```text
POST /api/auth/register            create an account (e-mail + password, sessions with refresh tokens)
POST /api/missions/m1/quiz         the quiz is graded on the server
POST /api/missions/m2/wallet       activate the starter wallet
POST /api/missions/m3/reward       pay the 21-sat reward from the learning budget
POST /api/campaigns                create a Naatal campaign (title, goal, link)
GET  /api/fees/preview             compute the service fee BEFORE the donation
POST /api/campaigns/:slug/donations  create the donation invoice
POST /api/webhooks/lnbits          "payment received" (authenticated, then re-read from LNbits)
GET  /lnurlp/:slug/callback        LNURL-pay: a new invoice at every scan
GET  /api/wallets/me/transactions  the personal history (paged)
GET  /api/healthz                  health check (database included)
```

### 3. Money rules that are enforced, not just documented

- **Whole sats only.** No float, no fractional BTC. The commission (percent, minimum, maximum) is computed on integers with an explicit rounding rule.
- **Double-entry ledger.** Every movement is a debit and a credit of the same amount, in **one database transaction**. A ledger that does not balance is a blocking bug.
- **Treasury is not user money.** It holds earned revenue only; every movement goes through the ledger.
- **Idempotent webhooks, re-read from the source.** The webhook URL is signed; the backend then **re-reads the payment status from LNbits** before crediting. Replaying the same webhook never credits twice (the key is the payment hash). A **periodic sweep** re-reads pending payments to catch a lost webhook.
- **Status is never invented.** An incoming or outgoing payment stays *pending* until LNbits says *paid*; a failed or expired payment is recorded as such.

![How an incoming payment is credited](https://raw.githubusercontent.com/HackathonBTCDays/XamBitcoin/main/docs/pitch/media/44-incoming-payment.png)

![The life of a payment](https://raw.githubusercontent.com/HackathonBTCDays/XamBitcoin/main/docs/pitch/media/47-payment-states.png)

### 4. Security by design

- **No seed phrase, no private key** is ever asked or stored from a user.
- **Admin keys only on the server.** They never reach the portal, the logs or an API response.
- **Two database roles.** A *migration* role owns the tables; the API runs with an *execution* role that cannot change the schema and can only **insert and read** the administrators' audit trail.
- **One public door.** Caddy is the only service that publishes ports; LNbits and phoenixd are never exposed; the LNbits admin UI is reachable only through an SSH tunnel.
- **Rate limits and trusted proxy.** Connection and sign-up are rate-limited by client address, with the number of trusted proxies set exactly.
- **An administrators' audit trail** records sensitive actions.
- **A capped starter wallet** and a **free withdrawal** keep the custodial risk small and the exit open.

### 5. Production and delivery

![Production architecture](https://raw.githubusercontent.com/HackathonBTCDays/XamBitcoin/main/docs/pitch/media/43-production-architecture.png)

- **Docker Compose** on a small server; **Caddy** gives automatic HTTPS; the portal is on **Cloudflare Pages**.
- A **deploy script** takes a **backup before every migration**, refuses to deploy a commit that is not on the main branch, refuses a roll-back from the CI key, and fails loudly if the proxy loses its address or the internal DNS.
- A **GitHub Actions** workflow runs the whole test suite on every pull request; the deploy workflow is **manual by default**.
- **Reference data** (the fee rule and the mission sheets) is seeded by a command that is safe in production.

### 6. Tests

**1,378** unit and contract tests (42 suites), **260 end-to-end tests on a real PostgreSQL**, **139** portal tests. They include replayed webhooks, balanced-ledger checks, and repository contracts that run against both an in-memory double and PostgreSQL.

### The end-to-end path, step by step

```text
1. Sign up          -> POST /api/auth/register              (account + session)
2. Mission 1        -> POST /api/missions/m1/quiz           (graded on the server)
3. Mission 2        -> POST /api/missions/m2/wallet         (LNbits wallet created)
4. Mission 3        -> POST /api/missions/m3/reward         (invoice of 21 sats created in the learner's wallet,
                                                             paid from the learning budget, ledger entry posted once)
5. Campaign         -> POST /api/campaigns                  (campaign wallet + permanent LNURL-pay link)
6. Donation         -> GET  /api/fees/preview               (fee shown BEFORE paying)
                       POST /api/campaigns/:slug/donations  (invoice) -> payer's wallet pays
7. Credit           -> webhook (signed) -> re-read from LNbits -> ledger: campaign + Treasury
```

---

## Challenges we ran into

### 1. The first Lightning channel is expensive

**Challenge:** a Lightning node needs inbound liquidity before anyone can pay it. For 2,000,000 sats of capacity, phoenixd quoted **21,000 sats of service fee plus about 400 sats of mining fee**. A first deposit of 30,000 sats left only about **7,600 sats** once the channel was open.
**Solution:** we always ask for the **quote before funding**, we turned off automatic channel opening, and we now recommend a first deposit of 50,000 to 100,000 sats.
**Learning:** on Lightning, liquidity has a price, and a "small test deposit" can be eaten by fees.

### 2. LNbits refuses to call back a private address

**Challenge:** LNbits will not send a webhook to a name that resolves to a private address. An internal network shortcut we had added to be helpful made the webhooks fail.
**Solution:** the webhooks go through the **public** address; we removed the shortcut, documented why, and kept the periodic sweep as a safety net.
**Learning:** a security default you do not understand can break a "helpful" shortcut.

### 3. A slow Lightning backend

**Challenge:** creating an invoice sometimes took **more than 10 seconds**, so the reward request failed with "slow connection".
**Solution:** the logs showed the failures happened **before** any payment: the reward quota was released and nothing was paid twice. We made the timeout configurable, and the screen now explains what happened instead of a generic error. A rarer case (a payment sent but the answer lost) is documented as a known risk.
**Learning:** read the logs before believing the first theory. We had suspected a triple payment; the logs disproved it.

### 4. A payment that is paid but still "pending"

**Challenge:** an outgoing payment can be reported *pending* by LNbits for a while even though it goes through. The mission stayed blocked.
**Solution:** a **"Verify my payment"** step re-reads the status from LNbits and completes the mission **only when LNbits reads it as settled**, never on *failed* or *pending*.
**Learning:** do not guess the outcome of a payment; re-read it from the source.

### 5. A test that failed by pure chance

**Challenge:** a continuous-integration run failed on a test that had passed many times.
**Solution:** the test searched the answer for the text "777", the amount of another user, but the short payment identifier is a **random hash prefix** and happened to contain "777". We compare the **amount field** instead.
**Learning:** a test must assert what the code guarantees for every case, never a lucky one.

### 6. Production surprises on day one

Three incidents on the first deployment, each documented in the repository:
- **A truncated secret.** A wallet password copied with the mouse lost most of its characters and was **stored in LNbits' own database**; fixing the environment did nothing.
- **A fixed Docker address taken by another container**, so the proxy could not start.
- **Docker's internal DNS failing** after partial restarts, so the whole site answered 502 while the deploy script said "done".
**Solution:** write down the cause of each, never copy secrets by hand, never partially restart, and make the **deploy script fail loudly** in the last case.
**Learning:** the incident that costs you a day is usually in the plumbing, not in the code.

### 7. Custody and trust

**Challenge:** a custodial wallet makes people nervous, and rightly so.
**Solution:** a **capped balance**, a **free withdrawal**, **no seed ever asked**, a Treasury kept apart from user balances, admin keys only on the server, and a **ledger** where every sat is traceable.
**Learning:** security and honesty are part of the product, not a page at the end.

### 8. Time

**Challenge:** from late October to the submission on 20 November, with studies and work in parallel, a product that touches real money.
**Solution:** strict priorities: **foundation, then Learn, then one module (Naatal)**; everything else on a roadmap; a feature that we could not prove stayed out of the claims.
**Learning:** it is better to ship a smaller product that is true than a larger one that is not.

---

## Accomplishments that we're proud of

- **A live product with real sats on mainnet**, not a mock-up: account, wallet, a **21-sat reward** and a Naatal campaign page, all on the live site.
- **The fee is visible before you pay**, and the commission rule (percent, minimum, maximum) is configurable.
- **A money core we can defend**: double-entry ledger, idempotent webhooks re-read from LNbits, a sweep for lost webhooks, a Treasury kept apart from user balances.
- **Security by default**: no seed ever asked, capped wallet, admin keys only on the server, one public door, two database roles, an audit trail.
- **1,378 + 260 + 139 automated tests**, including replayed webhooks and balanced-ledger checks.
- **A real deployment**, not a tunnel: HTTPS, backup before every migration, a guarded deploy script, a CI that runs on every pull request.
- **A product that tells the truth**: the demo is labelled, the explanations are said to be written in advance, and the repository lists what is **not** done.
- **Documentation that records what went wrong**, with cause, fix and the rule to remember.

---

## What we learned

### About Lightning and LNbits
- Inbound liquidity is a cost, and the quote must come before the deposit.
- An invoice contains an **amount, a description and an expiry**; the sender pays the routing fees, not the receiver.
- **LNURL-pay** gives one QR code that creates a new invoice at every scan: ideal for donations.
- Webhooks are not signed by default: we sign the URL, then **re-read the payment** before crediting.
- A **timeout on our side does not stop LNbits**: an invoice may exist even though our call failed. It leaves harmless unpaid invoices, but it must never release money.

### About money software
- Whole sats and a **balanced double-entry ledger** make bugs visible.
- **Idempotency** (one entry per payment hash) is what makes retries and replays safe.
- The **Treasury must never include user funds**; separation is a rule, not a hope.
- A status is a fact read from the source, never a guess.

### About operating a real node
- A restart does **not** reload environment variables; a recreated container does.
- A setting saved in an admin interface can live in the **application's own database**, not in the environment you just fixed.
- A fixed network address must sit **outside** the automatic address range.
- Never copy a secret by hand; use the clipboard or a hidden prompt.
- A deploy script should **fail loudly** rather than report "done" in front of a broken site.

### About testing
- A test asserts what the code guarantees for **every** order of events, not one lucky order.
- A test double and the real database must pass the **same contract**.
- **Counts without dates are lies**: we measure and date every number.

### About product and honesty
- People trust a product that says what is a demonstration and what is real.
- Written-in-advance explanations with real figures beat a generated explanation that may be wrong.
- Plain, human error messages ("the payment service is slow, nothing was debited, try again") beat technical ones.

---

## What's next for XamBitcoin

XamBitcoin is **one base on which several modules can sit**: each new module only adds its **specific part**, because the wallet, payments, ledger, Treasury, receipts and notifications already exist.

![The modules on the common base](https://raw.githubusercontent.com/HackathonBTCDays/XamBitcoin/main/docs/pitch/media/45-modules-on-the-base.png)

*This is a proposed roadmap, not a promise: durations are estimates, and the rates mentioned are illustrative values still to be set.*

![The roadmap in three horizons](https://raw.githubusercontent.com/HackathonBTCDays/XamBitcoin/main/docs/pitch/media/46-roadmap.png)

### Short term (1 to 3 months): prove it, then make it usable

**1. Close the proof of the Naatal loop on mainnet**
- A real donation with the fee shown before, the payment credited, and the **commission landing in the Treasury**, filmed and documented.
- The same for the outgoing payment of mission 5 and the reusable link of mission 4, on the live site.

**2. Test with 3 to 5 real people**
- Time each mission (above 3 minutes, we simplify), watch where they stop, fix the texts.
- Tune the **starting commission rate** (1 %, min 1, max 500) with their feedback.

**3. Finish the wallet in the portal**
- Receive, send and **withdraw** from the portal (the API routes exist; the portal says "not available yet").
- Balance cap and free withdrawal explained at each step.

**4. Harden what is already running**
- **Encrypted backups sent off the server** and a tested restore.
- Close the administrator routes to the Internet once the demo is done, and keep the audit trail.
- Fix the server's outgoing DNS and IPv6, and add the portal's security headers.
- Move the runtime to a supported Node version.

**5. The mobile app**
- An **Expo** app on the same shared package and the same API, **Android first** (an APK), iOS and the stores later. It does not exist yet.

**6. First extra module: Jefandikoo**
- See below. It is the closest to what Naatal already does.

### Medium term (3 to 6 months): open the platform

**7. Build: a public API for developers**
- An **API key per user**, documentation, a sandbox on a test network, **"payment received" webhooks**.
- Examples: a donation page, a payment button, LNURL-auth login.
- Free up to a quota, paid beyond it (more calls, a custom Lightning-address domain).

**8. Dekkandoo**
- See below. It holds the group's money between two cycles: it needs the security work above first.

**9. Wolof and local reach**
- **Plain French first, Wolof next** for the mission texts.
- A way to connect **your own wallet** (NWC) without commission on reception.
- Investigate local payment channels (mobile money, local exchanges): **to be verified, nothing is promised**.

**10. Schools and bootcamps**
- A **class space** to follow students' progress on Learn.
- **Sponsored missions**: a Bitcoin project pays for a mission on its own tool and funds the rewards.

### Long term (6 to 12+ months): a super-app and an ecosystem

**11. Fayma**
- See below. It holds money until a deliverable is validated: the most sensitive module.

**12. An extensions catalogue**
- Modules written by outside developers, with a possible **revenue share**.

**13. Regional growth**
- Adapt to other French-speaking markets in West Africa, with local partners, once the first pilots have proven the model.

**14. Pro features**
- Multi-shop accounting exports and SMS reminders for merchants, and a paid tier for heavy API users.

### The three planned modules

Each module reuses the same bricks (wallet and payments, ledger and Treasury, receipts and history, notifications) and adds **only its specific part**.

| Module | What it is | Specific part | Commission (illustrative, to be set) |
|---|---|---|---|
| **Naatal** | Fundraising campaigns (**built**) | Campaign, goal, supporting documents | 1 % with a minimum and a maximum |
| **Jefandikoo** | Sales on credit for small merchants | Customers, debts, reminders | about 0.5 % or a small fixed amount on a customer's Lightning payment |
| **Dekkandoo** | Savings circles and shared funds | Group, cycles, turn order | a small fixed amount per cycle, on the payout to the beneficiary |
| **Fayma** | Freelance missions with milestones | Missions, milestones, deliverables | about 1 % on a milestone payment |

![How the three planned modules work](https://raw.githubusercontent.com/HackathonBTCDays/XamBitcoin/main/docs/pitch/media/48-module-flows.png)

**A rule for all modules:** the platform earns **when a module renders a service**, never when you simply receive money and never when you withdraw. Withdrawal stays free of commission, with only the real network fees.

**A point of vigilance:** a savings circle keeps the group's money between two cycles, and a freelance escrow keeps money until validation. These two are the most sensitive in security and responsibility, so they come **after** the hardening work above.

### Impact we aim for

**Quantitative goals (proposed, to be measured):**
- Learners who finish the six missions and **make a first real payment**.
- Real campaigns created and funded in sats.
- Time per mission under **3 minutes**.

**Qualitative goals:**
- Make Lightning something people have *done*, not just *heard of*.
- Give communities a simple, **transparent** way to pool money, with the fee visible before the payment.
- Offer developers a base they can build on.

### Ultimate vision

*A place where learning Bitcoin is the first step of using it, where a student association can fund its lab in a few taps, where every fee is visible before it is paid, and where the same simple base carries the tools that communities need.*

---

## Team

**Salif Diallo**: project author and developer. GitHub: [@MrSalifDiallo](https://github.com/MrSalifDiallo)

## Links

- **Live site:** [xambitcoin.com](https://xambitcoin.com)
- **Code:** [github.com/HackathonBTCDays/XamBitcoin](https://github.com/HackathonBTCDays/XamBitcoin)
- **Built for:** Dakar Bitcoin Hack
````

---

## 3. Ce que le texte ne dit volontairement pas

| On n'écrit pas | Pourquoi |
|---|---|
| « Application mobile », « APK disponible » | N'existe pas (`D-007` : pas d'APK pour la soumission). Le texte la met en « 1 à 3 mois » comme travail à faire |
| « Mission 6 jouable » | La création d'une campagne passe par une page à part. La table l'indique |
| « Explique ce paiement par IA » | Textes écrits d'avance, aucune IA côté serveur : le texte le dit |
| « Commission de 1 % retenue » | C'est une valeur d'enseignement (Q-01 ouverte) : le texte le dit |
| « Retrait dans le portail » | Existe côté API, pas dans le portail : listé dans « 1 à 3 mois » |
| « Une vraie contribution a été payée et la commission est arrivée au Treasury » | Pas encore prouvé : listé dans « 1 à 3 mois » comme première étape |
| Wave, Orange Money, échanges locaux | À vérifier, rien n'est promis (`ROADMAP_NEXT_STEPS.md`) : le texte écrit « to be verified, nothing is promised » |
| Des dates précises | Les durées (1 à 3, 3 à 6, 6 à 12 mois) sont des estimations ; les taux des modules sont des valeurs illustratives (Proposition, § 3) |
| Le nom de l'hébergeur, une adresse IP, un e-mail | Dépôt public |

## 4. À relire avant de coller

- [ ] **La phrase « We lived this ourselves »** (Inspiration) : elle vient de la Proposition (« même en ayant participé à un hackathon Bitcoin, certains mécanismes m'échappaient »). Adaptez-la si elle n'est pas exacte.
- [ ] **La feuille de route** (1 à 3, 3 à 6, 6 à 12 mois) est une proposition tirée de la Proposition (ordre : Jefandikoo, Build, Dekkandoo, Fayma, wallet externe NWC, wolof, catalogue d'extensions). Ajustez les durées si vous voulez.
- [ ] **La section « Team »** ne met que votre nom et votre identifiant GitHub : ajoutez ce que vous voulez rendre public (LinkedIn), mais pas d'e-mail personnel.
- [ ] Les liens d'images fonctionnent (dépôt public et branche fusionnée), sinon téléverser les fichiers à la main.
- [ ] Les chiffres de tests sont ceux de `docs/TESTING.md` à la date d'envoi.
- [ ] Si le don réel du niveau 3 a été fait, remplacer la première puce de « Short term » par le résultat et ajouter la capture.
- [ ] Les noms `Jefandikoo` et `Dekkandoo` sont écrits sans accent pour éviter un problème d'encodage dans Devpost.
