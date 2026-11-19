# 07 · Schémas Mermaid (sources)

> Les neuf schémas de la présentation de XamBitcoin, en texte Mermaid : **GitHub les affiche directement**. **Devpost, lui, n'affiche pas Mermaid** (constaté) : pour Devpost, les mêmes schémas existent en **images PNG** dans `media/` (`40-` à `48-`) et c'est ce que l'histoire utilise. Pour modifier un schéma : changer le texte ici, puis régénérer le PNG. Couleurs de la palette du projet : bleu = étape, vert = réel ou réussi, orange = argent, jaune = prévu ou en attente. Chaque schéma ne montre que ce que le code fait, ou ce qui est marqué « planned ».

---

## 1. Learn, Use, Build et le socle commun (`40-learn-use-build.png`)

```mermaid
flowchart TB
  subgraph LEARN["Learn (free)"]
    L1["Guided missions M1 to M6"]
    L2["Explain this payment<br/>(text written in advance)"]
  end
  subgraph USE["Use"]
    W["XamBitcoin starter wallet"]
    N["Naatal: fundraising campaigns (the MVP module)"]
    F["Later: Jefandikoo, Dekkandoo, Fayma"]
  end
  subgraph BUILD["Build (later)"]
    B1["API keys"]
    B2["Webhooks"]
    B3["LNURL-pay, withdraw, auth"]
  end
  subgraph CORE["Common base"]
    C1["Payment engine: LNbits + phoenixd"]
    C2["Ledger: user balances"]
    C3["Treasury: platform revenue"]
    C4["Receipts and history"]
  end
  LEARN --> USE --> BUILD
  USE --> CORE
  BUILD --> CORE
  classDef process fill:#4c6ef5,stroke:#1971c2,color:#fff
  classDef finance fill:#ff922b,stroke:#d9480f,color:#fff
  classDef pending fill:#ffd43b,stroke:#e67700,color:#333
  class C1,C2,C4 process
  class C3 finance
  class F,B1,B2,B3 pending
```

## 2. La boucle d'une mission (`41-mission-loop.png`)

```mermaid
flowchart TB
  A["1. Context<br/>30 s, one notion"] --> B["2. Action<br/>a real operation in the app"]
  B --> C["3. Verification<br/>the backend observes the result"]
  C --> D["4. Result<br/>real amount, fees, status"]
  D --> E["5. Explanation<br/>written in advance, figures from the real payment"]
  E --> G["Badge and next mission"]
  classDef process fill:#4c6ef5,stroke:#1971c2,color:#fff
  classDef ok fill:#51cf66,stroke:#2b8a3e,color:#fff
  class A,B,C,D,E process
  class G ok
```

## 3. Commission et Treasury, exemple de 10 000 sats (`42-commission-treasury.png`)

```mermaid
flowchart TB
  P["Contributor pays 10,000 sats<br/>to a Naatal campaign"] --> R["XamBitcoin backend<br/>payment received webhook"]
  R --> V["Re-reads the payment status<br/>from LNbits"]
  V --> U["Ledger: campaign wallet<br/>+ 9,900 sats"]
  V --> T["Treasury<br/>+ 100 sats (1 %)"]
  U --> O["Owner withdrawal<br/>0 commission, real network fees"]
  classDef process fill:#4c6ef5,stroke:#1971c2,color:#fff
  classDef finance fill:#ff922b,stroke:#d9480f,color:#fff
  classDef ok fill:#51cf66,stroke:#2b8a3e,color:#fff
  class P,R,V process
  class U,O ok
  class T finance
```

## 4. Architecture de production (`43-production-architecture.png`)

```mermaid
flowchart TB
  U["Visitor's browser"] --> CF["Cloudflare Pages<br/>web portal"]
  CF -->|"HTTPS calls"| CD
  PW["Payer's Lightning wallet"] --> CD
  subgraph VPS["One server, one private Docker network"]
    CD["Caddy<br/>the only public door"]
    API["NestJS API<br/>missions, ledger, commission"]
    PG[("PostgreSQL")]
    LN["LNbits 1.6.2<br/>one wallet per user"]
    PH["phoenixd 0.9.3<br/>mainnet, no public port"]
    CD --> API
    CD -->|"only /lnurlp, read-only"| LN
    API --> PG
    API --> LN
    LN -->|"payment received webhook"| API
    LN --> PH
  end
  PH --> NET["Lightning network"]
  classDef process fill:#4c6ef5,stroke:#1971c2,color:#fff
  classDef finance fill:#ff922b,stroke:#d9480f,color:#fff
  classDef ok fill:#51cf66,stroke:#2b8a3e,color:#fff
  class CF,CD,API,LN process
  class PG,PH finance
  class NET ok
```

## 5. Crédit d'un paiement reçu (`44-incoming-payment.png`)

```mermaid
flowchart TB
  P["Payer's wallet pays the invoice"] --> LN["LNbits receives the payment"]
  LN -->|"webhook with a signed URL"| W["API checks the signature"]
  W --> R["API re-reads the payment status<br/>from LNbits"]
  S["Periodic sweep of pending payments<br/>(catches a lost webhook)"] --> R
  R -->|"paid"| L["Ledger entry, once per payment hash<br/>(replays never credit twice)"]
  R -->|"not paid"| X["Nothing is credited"]
  classDef process fill:#4c6ef5,stroke:#1971c2,color:#fff
  classDef ok fill:#51cf66,stroke:#2b8a3e,color:#fff
  classDef pending fill:#ffd43b,stroke:#e67700,color:#333
  class P,LN,W,R,S process
  class L ok
  class X pending
```

## 6. Les modules sur le socle commun (`45-modules-on-the-base.png`)

```mermaid
flowchart TB
  subgraph BASE["Common base (built)"]
    B1["Wallet and payments"]
    B2["Ledger and Treasury"]
    B3["Receipts and history"]
    B4["Notifications"]
  end
  subgraph MODS["Modules: each one adds only its specific part"]
    N["Naatal (built)<br/>campaign, goal, supporting documents"]
    J["Jefandikoo (planned)<br/>customers, debts, reminders"]
    D["Dekkandoo (planned)<br/>group, cycles, turn order"]
    F["Fayma (planned)<br/>missions, milestones, deliverables"]
  end
  BASE --> N
  BASE --> J
  BASE --> D
  BASE --> F
  classDef process fill:#4c6ef5,stroke:#1971c2,color:#fff
  classDef ok fill:#51cf66,stroke:#2b8a3e,color:#fff
  classDef pending fill:#ffd43b,stroke:#e67700,color:#333
  class B1,B2,B3,B4 process
  class N ok
  class J,D,F pending
```

Note : « Notifications » est dans la vision de la Proposition (`XamBitcoin_Proposition_Concrete.md`, § 5) ; ce n'est pas une brique que le code expose aujourd'hui.

## 7. La feuille de route en trois horizons (`46-roadmap.png`)

Proposition d'ordre, pas un engagement : les durées sont des estimations.

```mermaid
flowchart TB
  subgraph S["Short term: 1 to 3 months"]
    S1["Prove the Naatal loop on mainnet<br/>commission in the Treasury"]
    S2["Test with 3 to 5 real people<br/>tune the commission"]
    S3["Wallet in the portal<br/>receive, send, withdraw"]
    S4["Harden: encrypted backups,<br/>admin routes, security headers"]
    S5["Expo mobile app<br/>Android first"]
    S6["Jefandikoo"]
    S1 ~~~ S4
    S2 ~~~ S5
    S3 ~~~ S6
  end
  subgraph M["Medium term: 3 to 6 months"]
    M1["Build: API keys,<br/>webhooks, sandbox"]
    M2["Dekkandoo"]
    M3["Wolof, own wallet<br/>through NWC"]
    M4["Schools,<br/>sponsored missions"]
    M1 ~~~ M3
    M2 ~~~ M4
  end
  subgraph L["Long term: 6 to 12+ months"]
    L1["Fayma"]
    L2["Extensions catalogue"]
    L3["Regional growth"]
    L4["Pro features"]
    L1 ~~~ L3
    L2 ~~~ L4
  end
  S --> M --> L
  classDef process fill:#4c6ef5,stroke:#1971c2,color:#fff
  classDef pending fill:#ffd43b,stroke:#e67700,color:#333
  class S1,S2,S3,S4 process
  class S5,S6,M1,M2,M3,M4,L1,L2,L3,L4 pending
```

## 8. La vie d'un paiement (`47-payment-states.png`)

```mermaid
stateDiagram-v2
  [*] --> pending : invoice created, or payment sent
  pending --> paid : LNbits reads it as settled
  pending --> expired : the invoice expires
  pending --> failed : LNbits reports a failure
  paid --> [*] : credited once, ledger balanced
  expired --> [*] : nothing credited
  failed --> [*] : nothing credited
```

## 9. Les trois modules prévus (`48-module-flows.png`)

Tout est **prévu**, rien n'est construit. Les commissions sont des valeurs illustratives de la Proposition (§ 3).

```mermaid
flowchart LR
  subgraph J["Jefandikoo (planned): sales on credit"]
    direction TB
    J1["Customer pays the merchant<br/>over Lightning"] --> J2["Debt is settled<br/>receipt for both sides"]
    J2 --> J3["Small commission<br/>on the customer payment"]
  end
  subgraph D["Dekkandoo (planned): savings circles"]
    direction TB
    D1["Members pay in<br/>each cycle"] --> D2["The pot is held<br/>between cycles"]
    D2 --> D3["Payout to the beneficiary<br/>whose turn it is"]
    D3 --> D4["Small fixed fee per cycle"]
  end
  subgraph F["Fayma (planned): freelance missions"]
    direction TB
    F1["Client funds a milestone"] --> F2["Money held until<br/>the deliverable is validated"]
    F2 --> F3["Release to the freelancer"]
    F3 --> F4["Commission on the milestone"]
  end
  classDef process fill:#4c6ef5,stroke:#1971c2,color:#fff
  classDef finance fill:#ff922b,stroke:#d9480f,color:#fff
  class J1,J2,D1,D2,D3,F1,F2,F3 process
  class J3,D4,F4 finance
```
