# Cahier des charges — SportBillet MTL

**Auteur** : Fabiola Sainvry
**Cours** : 420-951-MA Applications Web transactionnelles
**Session** : Automne 2026, Groupe 25604
**Date** : 23 novembre 2026
**Mode** : Seul (10 user stories, paiement unique)

---

## Table des matières
1. [Contexte, problème, public cible et concurrents](#1-contexte)
2. [Vision, SWOT, personas et 7 P](#2-vision)
3. [Modèle de paiement](#3-modèle-de-paiement)
4. [User stories, critères d'acceptation et cas d'utilisation](#4-user-stories)
5. [Diagrammes de classes et de séquence](#5-diagrammes)
6. [Maquettes](#6-maquettes)
7. [Schéma de base de données](#7-schéma-bd)
8. [Exigences non fonctionnelles](#8-enf)
9. [Planification et rôles](#9-planification)
10. [Technologie choisie](#10-technologie)
11. [Journal IA et configuration de l'agent](#11-journal-ia)
12. [Rédaction et traçabilité](#12-rédaction)

---


## 1. Contexte, problème, public cible et concurrents <a id="1-contexte"></a>

### 1.1 Le problème
À Montréal, les organisateurs d'événements sportifs de niche comme les galas de boxe, cartes de MMA, tournois de jiu-jitsu, karaté, ping-pong, matchs amateurs de football et basketball, qui n'ont pas de plateforme locale dédiée pour vendre leurs billets en ligne. Ils utilisent aujourd'hui :
- **Facebook + virement Interac** : pas de traçabilité, pas de billet officiel, pas de QR code, aucun contrôle à l'entrée.
- **Eventbrite** : frais de 3,7 % + 1,79 $ CAD **par billet** vendu, interface en anglais par défaut, support axé USA.
- **Billetterie manuelle à la porte** : files d'attente, erreurs de monnaie, pas de données post-événement.

**Coût réel** aujourd'hui pour un organisateur de gala de MMA à 300 billets à 45 $ :
- Perte estimée en frais Eventbrite : ~1 200 $ par événement
- Temps de gestion manuelle : ~15 h entre promotion, vente, décompte, remboursements
- Billets fantômes et fraude

### 1.2 Public cible

| Segment | Qui | Besoin |
|---|---|---|
| **Organisateurs** | Promoteurs de boxe/MMA indépendants, gyms de jiu-jitsu, ligues amateures de foot/basket, clubs de ping-pong | Vendre des billets facilement, encaisser rapidement, contrôler l'entrée |
| **Spectateurs** | Fans de sports de combat et sports amateurs à Montréal, 18-45 ans, actifs sur Instagram, facebook, Snapchat et TikTok | Trouver des événements proches, acheter en 2 clics, recevoir un billet mobile |
| **Contrôleurs d'entrée** | Bénévoles ou staff de l'organisateur | Scanner les QR codes sans compte complexe |

### 1.3 Concurrents

| Concurrent | Offre | Prix | Faiblesse pour notre public |
|---|---|---|---|
| **Eventbrite** | Billetterie générale internationale | 3,7 % + 1,79 $ par billet | Pas adapté au Québec, cher pour petits volumes, interface anglophone par défaut |
| **lepointdevente.com** | Billetterie québécoise généraliste | 2 $ fixe par billet + 2 % | Pas spécialisé sport, UX datée, pas de catégorisation par discipline sportive |
| **Showpass** | Billetterie canadienne événementielle | 2,5 % + 1,50 $ par billet | Pas de sport local, surtout concerts et festivals |

### 1.4 Positionnement
**Nyx billets| Apex billets| Centurionsport billets | SportBillet MTL est la billetterie québécoise pensée pour les événements sportifs locaux, avec des frais fixes bas, une interface bilingue et un contrôle d'entrée par QR code intégré.**

---

## 2. Vision, SWOT, personas et 7 P <a id="2-vision"></a>

### 2.1 Cercle d'or (Why / How / What)
- **Why** — Parce que les passionnés de sports de niche à Montréal méritent des événements bien organisés, et que les organisateurs locaux ne devraient pas perdre 10 % de leurs revenus en frais de billetterie étrangers.
- **How** — En offrant une plateforme spécialisée, bilingue, avec paiement unique sans abonnement, frais fixes transparents et outils de contrôle d'entrée simples.
- **What** — Un site web où l'organisateur publie son événement en 5 minutes, et où le spectateur achète son billet en 2 clics avec Apple Pay, Google Pay ou carte de crédit.

### 2.2 Analyse SWOT

| Forces (interne +) | Faiblesses (interne −) |
|---|---|
| Spécialisation sport = marketing ciblé | Nouveau joueur sans notoriété |
| Interface bilingue FR/EN native | Petit catalogue au lancement |
| Frais plus bas que concurrents | Pas encore d'app mobile dédiée |

| Opportunités (externe +) | Menaces (externe −) |
|---|---|
| Croissance des sports de combat à MTL | Eventbrite peut baisser ses frais |
| Multiplication des gyms MMA/BJJ | Fraude aux captures de QR codes |
| Loi 25 favorise acteurs locaux | Changements aux frais Stripe |

### 2.3 Personas

**Persona 1 — Marc, 34 ans, promoteur de MMA**
- Organise 4 galas par an au Centre Pierre-Charbonneau
- **Besoin** : vendre 300-500 billets par événement, suivre qui a payé, émettre des remboursements rapidement
- **Frustration** : perd environ 1 200 $ à Eventbrite par événement et déteste leur support anglophone
- **Capacité de payer** : 500-2 000 $ en frais de plateforme par événement.
- **Volonté** : prêt à essayer une plateforme québécoise si ça lui aide vraiment a économise 

**Persona 2 — Sophie, 26 ans, fan de jiu-jitsu brésilien**
- Assiste à 8-10 tournois et galas par année à Montréal et environs
- **Besoin** : découvrir les événements, acheter rapidement sur mobile, montrer le billet à l'entrée
- **Frustration** : perd des événements faute de les voir annoncés trop tard et  déteste payer 7-10 $ de frais sur un  billet à 40  $$ .
- **Capacité de payer** : 30-80 $ par billet, 1-2 billets par achat
- **Volonté** : forte, tant que le processus est fluide Apple Pay en 1 geste

### 2.4 Les 7 P
- **Produit** — Plateforme web de billetterie spécialisée sport, QR code mobile, bilingue FR/EN
- **Prix** — Billets fixés par l'organisateur ; frais de service de 1,50 $ CAD + 3 % par billet payés par l'acheteur taxes TPS/TVQ en sus, bien plus bas qu'Eventbrite
- **Place** — Site web responsive accessible partout, hébergé au Canada idéalement / Vercel + Neon
- **Promotion** — Partenariats avec gyms de MMA/BJJ de Montréal, Instagram, Facebook, Snapchat et TikTok des organisateurs
- **Personnes** — Équipe réduite au lancement : 1 dev-fondateur, support par courriel
- **Processus** — Publication d'événement en 5 min, achat en 2 clics, scan QR à l'entrée
- **Preuve physique** — Reçu PDF envoyé par courriel, billet avec QR dans un compte sécurisé, confirmation visible à l'écran après paiement

---

## 3. Modèle de paiement <a id="3-modèle-de-paiement"></a>

### 3.1 Type — Paiement unique ( à revoir!)
Mode **seul** → le règlement choisit **paiement unique**, pas d'abonnement.
**Pourquoi** : le spectateur n'achète qu'occasionnellement (quelques événements par an) ; un abonnement n'a pas de sens. L'organisateur, lui, préfère payer uniquement quand il vend. Ce modèle élimine la friction d'inscription et correspond aux habitudes des utilisateurs Eventbrite/Showpass.

### 3.2 Grille tarifaire

Toutes les transactions sont en **dollars canadiens (CAD)**. L'acheteur paie le prix du billet + les frais de service  + TPS (5 %) + TVQ (9,975 %). Les montants sont stockés en **cents** (Int) selon RM-01.

| Type d'événement | Prix billet (CAD) | Frais Service | Exemple TPS | Exemple TVQ | Total acheteur |
|---|---|---|---|---|---|
| Petit tournoi amateur | 15,00 $ | 1,95 $ | 0,85 $ | 1,69 $ | 19,49 $ |
| Match ligue locale | 25,00 $ | 2,25 $ | 1,36 $ | 2,72 $ | 31,33 $ |
| Gala de boxe/MMA | 45,00 $ | 2,85 $ | 2,39 $ | 4,77 $ | 55,01 $ |
| Carte combat premium | 95,00 $ | 4,35 $ | 4,97 $ | 9,92 $ | 114,24 $ |

### 3.3 Exemple de calcul détaillé (en cents, selon RM-04)

**Billet gala de MMA à 45,00 $ CAD** :
Les taxes sont arrondies **individuellement** (pas sur le total) selon la pratique de Revenu Québec.

### 3.4 Tableau des plans (gratuit / payant / premium)

| Plan | Qui | Prix | Ce qui est inclus |
|---|---|---|---|
| **Gratuit** | Tout visiteur | 0 $ | Navigation du catalogue, création de compte, filtres par sport/date/lieu |
| **Payant** (par billet) | Spectateur qui achète | Prix billet + frais | Billet avec QR unique, reçu PDF, historique d'achats, remboursement automatisé si annulation ≥ 48 h |
| **Premium organisateur** | Organisateur vérifié | 0 $ + 1,50 $/3 % par billet vendu | Publication d'événements, statistiques de vente temps réel, scan QR à l'entrée, exports CSV |

### 3.5 Parcours

**a) Achat**
- Utilisateur voit : page événement → clic "Acheter" → sélectionne quantité → Stripe Checkout (Apple Pay/Google Pay/carte) → page de confirmation avec billet et QR
- Système fait : crée `Order` en statut `PENDING`, redirige vers Stripe, attend le webhook `checkout.session.completed`, passe `Order` à `PAID`, génère QR, envoie le reçu par courriel
- Règle : **RM-02** — commande `PAID` **uniquement** après webhook vérifié par signature

**b) Échec de paiement**
- Utilisateur voit : message Stripe "carte refusée", retour à la page panier avec option de réessayer
- Système fait : `Order` reste `PENDING` ; pas de place réservée au-delà de 15 min (expiration automatique)
- Règle : **RM-09** — une commande `PENDING` qui dépasse 15 min repasse à `EXPIRED` et libère les places

**c) Annulation par l'utilisateur** (avant paiement)
- Utilisateur voit : bouton "Annuler" dans le panier → confirmation → retour catalogue
- Système fait : passe `Order` à `CANCELLED`, libère les places réservées
- Règle : **RM-10** — l'utilisateur peut annuler une commande tant qu'elle est `PENDING`

**d) Remboursement** (après paiement)
- Utilisateur voit : bouton "Demander un remboursement" dans son historique, actif seulement si événement > 48 h
- Système fait : appelle Stripe Refund API, crée une entrée `Refund` avec statut, invalide le QR
- Règle : **RM-06** — remboursement possible jusqu'à 48 h avant l'événement, 100 % du prix billet, frais de service non remboursés

**e) Annulation d'événement** (par l'organisateur)
- Utilisateur voit : courriel automatique annonçant l'annulation et le remboursement sous 5 jours ouvrables
- Système fait : passe `Event` à `CANCELLED`, déclenche un remboursement complet (prix + frais) pour toutes les commandes `PAID`
- Règle : **RM-11** — si l'événement est annulé par l'organisateur, remboursement total obligatoire sous 5 jours ouvrables

cat >> docs/cahier-des-charges.md << 'EOF'

### 3.6 Programme de parrainage

Chaque utilisateur reçoit un code de parrainage unique à la création de son compte (format `FAB-A3K7`). Le partage se fait par lien direct (`sportbillet.ca/?ref=FAB-A3K7`) ou par copie du code.

**Fonctionnement — deux rabais à la fois**

| Qui | Rabais | Quand |
|---|---|---|
| **Le  nouveau client qui utilise le code referal** | **10 %** sur sa **commande actuelle** avant taxes et frais de service | Appliqué automatiquement au passage en caisse |
| **Le parrain** propriétaire du code | **15 %** de crédit max 20,00 $ CAD sur sa **prochaine commande** | Crédité au compte dès que le filleul complète son premier paiement |

**Exemple concret — filleul**

**Parcours**
- Le filleul voit : bannière verte "🎁 10 % offerts grâce à `FAB-A3K7`" dans le panier, ligne explicite "Rabais parrainage" dans le récapitulatif
- Le parrain voit : notification par courriel + ligne dans son compte "Crédit 20,00 $ disponible (expire le 22 fév. 2027)"
- Le système fait : vérifie l'unicité du code, vérifie que le filleul n'a jamais acheté, applique le rabais avant calcul des frais et taxes, crée une entrée `Referral` liée aux deux comptes, génère le `CreditLedger` du parrain au moment du webhook payé
