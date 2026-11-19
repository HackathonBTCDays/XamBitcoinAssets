# 06 · Captures, schémas et clips

> Inventaire de tous les médias de présentation de XamBitcoin : ce que montre chaque image, son texte alternatif, la section Devpost qui l'utilise et l'ordre conseillé des 15 images de la galerie. Toutes les captures ont été prises **sur le site en ligne** (`https://xambitcoin.com`) le **2026-11-19**, avec des comptes de test à adresse e-mail fictive (`@example.org`), par un script de pilotage de navigateur (Playwright, fenêtre de 1200 par 800 points, soit le rapport 3:2 que Devpost conseille). Les schémas sont les blocs Mermaid de ce dossier, exportés en PNG.

---

## 1. Ce qui est réel, et ce qui reste à faire

| Parcours | État | Preuve |
|---|---|---|
| Pages publiques du site en ligne | **Réel** | Captures 01, 02, 04, 05 |
| Inscription depuis le portail vers l'API réelle | **Réel** (réponse 201, redirection vers le tableau de bord) | Essai du 2026-11-19 |
| Mission 1 (quiz) et mission 2 (wallet) | **Réel** | Captures 09b, 10 |
| Mission 3 : **21 sats réels** sur mainnet | **Réel** : solde 21 sats, transaction « Récompense Learn, +21 sats, Réglé » | Captures 31, 32, 33 |
| Création d'une campagne Naatal sur le site en ligne | **Réel** : page publique, QR LNURL-pay, adresse Lightning, **ligne de frais avant le paiement** | Captures 15, 17 |
| **Don réel** (100 sats, commission affichée, paiement par un wallet) | **À faire avec le propriétaire** (niveau 3) | Pas encore de capture |
| **Paiement sortant réel** de la mission 5 (facture de 10 sats) | **À faire avec le propriétaire** (niveau 3) | Pas encore de capture |

Tant que le niveau 3 n'est pas fait, l'histoire Devpost ne dit **pas** qu'une contribution réelle a été payée ni que la commission est arrivée au Treasury.

## 2. Captures (`media/`)

| Fichier | Ce que l'image montre | Texte alternatif | Section Devpost |
|---|---|---|---|
| `01-accueil.png` | Accueil : « Apprends Bitcoin en le faisant. », boutons, badges « bientôt » | Page d'accueil de XamBitcoin | What it does |
| `02-accueil-modele.png` | Les 6 missions et l'exemple de commission (don de 10 000 sats : 9 900 au porteur, 100 de frais) | Les six missions et le modèle de commission | What it does |
| `04-apercu-tutoriel.png` | Aperçu du tutoriel **sans argent**, bandeau « Données de démonstration » | Aperçu du tutoriel, sans argent | What it does |
| `05-naatal-demo.png` | Campagne de démonstration étiquetée, ligne de frais visible | Aperçu d'une campagne Naatal (démonstration) | Galerie |
| `08b-tableau-de-bord-neuf.png` | Tableau de bord d'un compte neuf (pas de wallet) | Tableau de bord d'un nouveau compte | Galerie |
| `09b-missions-progression.png` | Liste des missions : M1 et M2 terminées | Liste des missions, deux terminées | Challenges (honnêteté) |
| `10-mission1-quiz.png` | Quiz de la mission 1, réponses choisies | Quiz « C'est quoi un sat ? » | Galerie |
| `13-tableau-de-bord-wallet.png` | Wallet actif à 0 sat, progression 2 sur 6 | Wallet actif, solde 0 | Galerie |
| `14-finance.png` | Page Finance : solde, plafond, aucune transaction | Portefeuille sans transaction | Galerie |
| `15-campagne-formulaire.png` | Formulaire de création d'une campagne Naatal | Création d'une campagne | Galerie |
| `17-campagne-frais-avant-paiement.png` | Page publique de la campagne : **« Tu paies 1 000 sats, dont 10 sats de frais de service XamBitcoin (1 %, min 1, max 500). 990 sats vont au porteur de campagne. »**, QR permanent, adresse Lightning | La campagne affiche les frais avant le don | What it does |
| `21-mobile-campagne.png` | La même page sur téléphone (390 points) | Page de campagne sur téléphone | Galerie |
| `31-mission3-apres.png` | Mission 3 terminée avec les chiffres réels : 21 sats, statut Payé | Mission 3 : 21 sats reçus | What it does |
| `32-tableau-de-bord-21-sats.png` | Solde du wallet : 21 sats, progression 3 sur 6 | Solde de 21 sats après la récompense | Galerie |
| `33-finance-transaction.png` | Transaction « Récompense Learn, +21 sats, Réglé » | Historique avec la récompense réglée | What it does |

Les captures montrent des comptes de test à e-mail fictif. L'adresse de la campagne de test et son LNURL sont des liens publics de la campagne de démonstration créée pour ces captures.

## 3. Schémas (`media/`, source Mermaid de tous les schémas dans [`07-schemas-mermaid.md`](07-schemas-mermaid.md))

| Fichier | Contenu | Texte alternatif |
|---|---|---|
| `40-learn-use-build.png` | Learn, Use, Build et le socle commun | Les trois couches et le socle commun |
| `41-mission-loop.png` | La boucle d'une mission : contexte, action, vérification, résultat, explication | La boucle d'une mission |
| `42-commission-treasury.png` | Don de 10 000 sats : 9 900 au porteur, 100 au Treasury, retrait sans commission | Répartition d'un don avec commission |
| `43-production-architecture.png` | Navigateur, Cloudflare Pages, Caddy (seule porte publique), API, PostgreSQL, LNbits, phoenixd, réseau Lightning | Architecture de production |
| `44-incoming-payment.png` | Crédit d'un paiement reçu : webhook, relecture du statut, ledger, balayage | Comment un paiement reçu est crédité |
| `45-modules-on-the-base.png` | Le socle commun et les quatre modules (Naatal construit, les trois autres prévus) | Les modules sur le socle commun |
| `46-roadmap.png` | La feuille de route en trois horizons : 1 à 3, 3 à 6, 6 à 12+ mois | Feuille de route |
| `47-payment-states.png` | La vie d'un paiement : en attente, payé, expiré, échoué | États d'un paiement |
| `48-module-flows.png` | Les flux prévus de Jefandikoo, Dekkandoo et Fayma | Flux des trois modules prévus |

Les schémas sont en **orientation verticale** (environ 450 à 1 300 points de large) pour rester lisibles dans la colonne de texte de Devpost. Ils sont acceptés dans la galerie (JPG, PNG ou GIF, 5 Mo au plus).

## 4. Ordre conseillé des 15 images de la galerie Devpost

1. `01-accueil.png` (vignette conseillée, déjà en 3:2)
2. `04-apercu-tutoriel.png`
3. `10-mission1-quiz.png`
4. `09b-missions-progression.png`
5. `31-mission3-apres.png`
6. `32-tableau-de-bord-21-sats.png`
7. `33-finance-transaction.png`
8. `15-campagne-formulaire.png`
9. `17-campagne-frais-avant-paiement.png`
10. `05-naatal-demo.png`
11. `02-accueil-modele.png`
12. `40-learn-use-build.png`
13. `42-commission-treasury.png`
14. `43-production-architecture.png`
15. `44-incoming-payment.png`

## 5. Clips vidéo (`clips/`, **non suivis par Git**, fichiers `.webm` lourds)

| Fichier | Contenu | Durée utile |
|---|---|---|
| `clip-A-pages-publiques.webm` | Tour des pages publiques : accueil, comment ça marche, aperçu, campagne de démonstration, sécurité, inscription | environ 30 s |
| `clip-B-session-connectee.webm` | Connexion, tableau de bord, missions, quiz, wallet, finance, création d'une campagne | environ 1 min |
| `clip-C-missions-1-et-2.webm` | Compte neuf : tableau de bord, mission 1, mission 2 | environ 1 min |
| `clip-D-mission-3-reelle.webm` | Mission 3 : clic sur « Recevoir ma récompense », 21 sats reçus, solde, transaction | environ 30 s |

Ils sont bruts : sans voix, avec des attentes. Monter et couper dans CapCut, DaVinci Resolve ou OBS (voir [`03-script-video.md`](03-script-video.md)).

## 6. Règles pour toute nouvelle capture

- Compte de test à e-mail `@example.org` uniquement ; jamais l'e-mail réel du propriétaire.
- Aucune capture de l'administration de LNbits, du serveur, d'un terminal ni d'un secret.
- Relire chaque image avant de la publier (e-mail, solde, identifiant, jeton).
- Un don réel ou un paiement sortant réel coûte de vrais sats : une seule exécution, montant minuscule.
