# CLAUDE.md — Contexte de passation LifeMicroNut

> **Ce fichier est lu automatiquement par Claude Code au démarrage.** Il contient l'historique des décisions, les conventions et les chantiers en cours du projet LifeMicroNut.

---

## 🏥 Le projet en 2 phrases

**LifeMicroNut** est un site de bilans micronutritionnels en ligne conçu par une pharmacienne micronutritionniste (Dr Lapothicaire = Assiya Aiche). Site statique HTML/CSS/JS déployé sur Cloudflare Pages, domaine : **lifemicronut.com**.

---

## 👥 Les humains

| Personne | Rôle |
|---|---|
| **Youness** | Co-fondateur, opérationnel/business/produit. C'est lui qui pilote ce projet. |
| **Assiya** | Co-fondatrice, Dr en Pharmacie, pharmacovigilance ANSM, micronutrition fonctionnelle. C'est elle la caution scientifique. |

---

## 📁 Structure du dépôt

Tous les fichiers du site sont dans `lifemicronut/` :

### Quiz / bilans actifs (5 fichiers)
- `microbiote-mental.html` — Bilan microbiote & santé mentale
- `hormones.html` — Bilan hormones féminines (SPM, périménopause, SOPK)
- `peau-psoriasis-eczema.html` — Bilan peau (psoriasis, eczéma)
- `LifeMicroNut-Bilan-Microbiote-SanteMentale.html` — Doublon archive du microbiote-mental (à garder pour historique)

### Pages site (8 fichiers)
- `index.html` — Accueil, 3 cards quiz
- `about.html` — À propos (Dr Lapothicaire + Youness)
- `comprendre.html` — Pédagogie micronutrition
- `blog.html` + dossier `blog/` (6 articles)
- `faq.html`
- `contact.html`
- `mentions-legales.html`
- `boutique.html` — E-commerce compléments (panier localStorage)
- `pro.html` — Offre B2B pour pros (naturopathes, pharmaciens)

### Fichiers config Cloudflare
- `_headers`, `_redirects`, `robots.txt`, `sitemap.xml`, `favicon.svg`, `wa.js`, `tips.js`

---

## 🔑 Décisions importantes prises (chronologique)

### Gate d'accès aux quiz
- Tous les quiz commencent par un gate "Demandez votre code d'accès au Dr Lapothicaire"
- Formulaire : prénom + nom + email → envoie une notification à `Lifemicronut@gmail.com` via Web3Forms (access_key = `57726177-ef80-4817-bcf9-e1a59d4d0131`)
- Section repliable "J'ai déjà mon code" avec input — code actuel = `1234` (changeable dans chaque fichier : `var VALID = '1234'`)
- Une fois validé, accès stocké dans `sessionStorage` → pas de re-demande sur les autres quiz

### Quiz supprimés
- **NeuroLab** (7 quiz : Big Five, DISC, Manager toxique, Ennéagramme, PNL, Psychopathe, PN) → supprimés à la demande du user
- **TDAH** + protocole 3 mois → supprimés à la demande du user

### Web3Forms (notifications email)
- Tous les formulaires (gate access, boutique checkout, contact, newsletter) envoient à `Lifemicronut@gmail.com`
- Access key web3forms : `57726177-ef80-4817-bcf9-e1a59d4d0131`
- ⚠️ Ne JAMAIS écrire `contact.smartbnb@gmail.com` — c'est l'email de Youness mais le système envoie à `Lifemicronut@gmail.com`

### Charte visuelle
- Couleur principale : **vert #12936A** (vert nature)
- Couleur sombre : `#16211C`
- Fond doux : `#F1F7F3`
- Accent or : `#C19A1C`
- Polices : **Inter** (sans-serif, body) + **Fraunces** (serif italique, accents)
- Style : moderne, médical, premium, pas marketing agressif

### Ton éditorial
- **Tutoiement-vouvoiement mixte** selon les pages (vouvoiement majoritaire, tutoiement quand on parle "à toi")
- **Pas de promesses thérapeutiques** : on n'emploie jamais les verbes "soigner", "traiter", "guérir", "diagnostiquer"
- On parle de "comprendre", "explorer", "soutenir le terrain", "orientation"
- Toujours un **disclaimer médical** : "ne remplace pas un avis médical"

### Liens
- **Tous les liens internes sont absolus** (commencent par `/`) — ex: `/microbiote-mental.html`
- Pas de `index.html` à la fin, juste `/`
- Pour Cloudflare Pages : le déploiement est en flat structure (pas de dossier wrapper)

---

## 🎯 Chantiers en cours / TODO

### Court terme
1. **3 nouveaux bilans à créer** (déjà évoqués, scientifiquement écrits, 1h chacun) :
   - Surpoids / Métabolisme (insulinorésistance, cortisol, thyroïde, microbiote)
   - Polymédication (carences induites par médicaments : statines→CoQ10, metformine→B12, IPP→Mg, etc.)
   - Fatigue chronique (mitochondries, thyroïde, surrénales, fer/B12, microbiote, sommeil)
2. **Newsletter** : aujourd'hui rien n'est connecté. Plan : Brevo (300/jour gratuit, RGPD FR) — Youness validera quand prêt.
3. **Stripe Payment Links** pour la boutique : placeholders à activer

### Moyen terme
- CRM Klaviyo (annoncé mais pas urgent)
- Optimisation SEO
- Relocalisation fiscale (côté business, hors code)

### Long terme
- Application iOS/Android ?
- Plateforme de RDV intégrée

---

## ⚙ Conventions techniques

### Stack
- **Static HTML/CSS/JS** uniquement (pas de framework, pas de build)
- CSS inline dans `<style>` de chaque page (autonomes)
- Web3Forms pour les formulaires serverless
- localStorage pour le panier boutique
- html2canvas + jsPDF (CDN) pour génération PDF des rapports quiz

### Déploiement
- Cloudflare Pages
- Direct Upload (pas de GitHub Actions auto-sync)
- Le ZIP du dossier `lifemicronut/` est uploadé manuellement par Youness

### Git
- Branche de travail principale : `claude/eloquent-edison-KXY7o` (sur l'ancien repo Smartbnb)
- Push automatique à chaque commit
- Une PR sera créée pour merger sur `main` quand un chantier est validé

---

## 🚨 Pièges connus à éviter

1. **Ne pas hardcoder `index.html`** dans les liens — utiliser `/`
2. **Ne pas modifier la structure de fichiers** sans valider avec Youness (Cloudflare Pages réagit mal)
3. **Toujours respecter la défensive line** : aucun verbe thérapeutique
4. **Email destinataire = `Lifemicronut@gmail.com`** (pas smartbnb)
5. **Code d'accès = `1234`** (pas `lafrançaise2026` qui était l'ancien)
6. **Pas d'expiration sur le gate** — l'ancien expirait dimanche 7 juin 18h, c'est retiré
7. **Cloudflare → flat structure** : zipper depuis l'intérieur de `lifemicronut/`, pas en enrobant le dossier

---

## 💼 Modèle business (contexte)

- **Bilans gratuits** = lead magnet, génèrent des emails
- **Boutique** = revenue principal (compléments sélectionnés par Assiya)
- **Pro** = abonnement B2B (€50/3mois ou €100/an pour naturopathes/pharmaciens — placeholder, à activer)
- **Pas de consultation payante** pour l'instant (Assiya est encore en activité officinale)

---

## 📞 Comment me parler (Claude) en démarrant la session

Si tu reprends ce projet, fais simple :

1. Lis ce fichier en entier
2. `ls lifemicronut/*.html` pour voir ce qui existe
3. Réponds à Youness avec un récap court : "J'ai lu le CLAUDE.md. État actuel : X quiz, Y pages. Chantier en cours : Z. Tu veux qu'on commence par quoi ?"

**Évite** :
- Les longues introductions
- Les options trop nombreuses (max 3)
- Le sur-zèle ("je vais créer un test unitaire pour…")
- Le sous-zèle ("dis-moi exactement ligne par ligne")

Youness est rapide, direct, pragmatique. Tu peux être pareil.

---

*Dernière mise à jour : 8 juin 2026 — Claude (session passation)*
