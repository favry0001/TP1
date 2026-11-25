# CLAUDE.md — Agent IA pour SportBillet MTL

## Contexte du projet
Plateforme de billetterie en ligne pour événements sportifs à Montréal . L'utilisateur achète un billet, reçoit un code QR unique, et le présente à l'entrée. Les organisateurs publient leurs événements et touchent les revenus après commission de la plateforme.

## Stack
- **Front-end** : Next.js 15 , TypeScript, Tailwind CSS, shadcn/ui
- **Back-end** : Route handlers Next.js, Server Actions
- **Base de données** : PostgreSQL hébergé chez Neon
- **ORM** : Prisma
- **Authentification** : NextAuth.js
- **Paiement** : Stripe Checkout + webhooks signés
- **Déploiement** : Vercel

## Commandes courantes
- `npm run dev` — serveur local
- `npm run build` — build prod
- `npx prisma migrate dev --name <nom>` — nouvelle migration
- `npx prisma validate` — valider le schéma
- `npx prisma studio` — explorer la base
- `stripe listen --forward-to localhost:3000/api/webhooks/stripe` — tester webhooks en local

## Règles métier (à respecter dans le code)
- **RM-01** — Tous les montants sont stockés en Int (cents). Jamais de Float ou Decimal.
- **RM-02** — Une commande ne passe à `PAID` qu'à la réception d'un webhook Stripe `checkout.session.completed` validé par signature.
- **RM-03** — Le prix du billet est copié dans `OrderItem.unitPriceCents` au moment de la commande (prix figé).
- **RM-04** — Les taxes (TPS 5 %, TVQ 9,975 %) sont calculées taxe par taxe et arrondies individuellement.
- **RM-05** — Aucun billet n'est émis si l'événement est complet (capacité atteinte).
- **RM-06** — Un remboursement est possible jusqu'à 48 h avant l'événement, 100 % du prix hors frais de service.
- **RM-07** — Chaque billet a un code QR unique (UUID) vérifié à l'entrée.
- **RM-08** — Les webhooks Stripe sont journalisés dans `WebhookEvent` (id = eventId Stripe) pour éviter le double traitement.

## Interdits 
- **Ne jamais commiter `.env`**, clés Stripe, URL Neon, mots de passe.
- **Ne jamais stocker de données de carte bancaire** sur nos serveurs, tout passe par Stripe.
- **Ne jamais désactiver la vérification de signature** des webhooks Stripe.
- **Ne jamais utiliser `git add .`** sans vérifier ce qui est ajouté avec `git status`.
- **Ne jamais mettre de vraies données personnelles** dans les seeds ou les tests .

## Conventions
- **Commits** : `type: description` 
- **Branches** : `main` (prod), `dev` intégration, `feat/<nom>` fonctionnalités
- **Identifiants** : US-01, US-02... user stories ; RM-01... règles métier ; ENF-01...
- **Nommage BD** : camelCase pour colonnes, PascalCase pour tables ; montants suffixés `...Cents`

## Protection des secrets
Voir `.claude/settings.json` : l'agent a interdiction absolue de lire `.env` et `.env.*`.
