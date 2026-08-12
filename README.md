# HUBTECH INDUSTRIE — Site web officiel

Site vitrine B2B complet, **fonctionnel et prêt à publier**. Aucun build, aucune dépendance à installer : ouvrez `index.html`.

---

## 1. Contenu du dossier

```
hubtech-industrie/
├── index.html          Site complet (HTML + CSS + JS intégrés)
├── robots.txt          Indexation moteurs de recherche
├── sitemap.xml         Plan du site (à mettre à jour avec le domaine réel)
└── assets/img/         Vos photos — voir assets/img/A_LIRE.txt
    └── realisations/   Photos de chantier de la galerie
```

## 2. Mise en ligne

**Hébergement classique (cPanel, OVH, LWS…)** : envoyez le contenu du dossier dans `public_html/` par FTP. C'est tout.

**Netlify / Vercel / Cloudflare Pages** : glissez-déposez le dossier, ou reliez un dépôt Git. Aucun paramètre de build à renseigner.

Après la mise en ligne, remplacez `https://www.hubtech-industrie.com/` par le domaine réel dans `index.html` (balises canonical + Open Graph + Schema.org) et dans `sitemap.xml`.

## 3. Images

Le site s'affiche correctement **même sans photos** : un visuel technique de repli prend le relais. Déposez vos fichiers dans `assets/img/` en respectant les noms indiqués dans `assets/img/A_LIRE.txt` — ils apparaissent automatiquement.

## 4. Personnalisation rapide

| À modifier | Où |
|---|---|
| Couleurs de marque | Bloc `:root` en haut du `<style>` (`--blue`, `--yellow`, `--navy`) |
| Chiffres clés animés | Attribut `data-count` des éléments `.count` |
| Numéro WhatsApp | Constante `WA_NUMBER` dans le script + tous les liens `wa.me/237651735628` |
| Adresse e-mail | Rechercher `Prestations@hubtech_industrie.com` |
| Réseaux sociaux | `href="#"` du bloc `.socials` dans le footer |
| Services du formulaire | `<select id="f-service">` |

## 5. Formulaire de devis

Le formulaire valide les champs obligatoires puis **compose la demande et ouvre WhatsApp** avec un message pré-rempli et une référence unique au format `HTI-AAAAMMJJ-XXXX`. Aucun serveur n'est nécessaire.

Pour recevoir aussi les demandes par e-mail, deux options simples :

- **Formspree / Web3Forms** : ajouter `action="https://formspree.io/f/VOTRE_ID" method="POST"` sur la balise `<form>` et retirer le `e.preventDefault()`.
- **PHP** : créer `envoi.php` avec un `mail()` et pointer le `fetch()` dessus.

La pièce jointe n'est pas transmise par WhatsApp — le message sous le bouton l'indique clairement à l'utilisateur.

## 6. Migration vers Next.js (optionnel)

L'architecture a été pensée pour être découpée sans réécriture :

```
app/
├── layout.tsx          <head> + métadonnées + JSON-LD
├── page.tsx            Assemblage des sections
└── globals.css         Le bloc <style> tel quel (variables CSS conservées)
components/
├── Header.tsx  Hero.tsx  Stats.tsx  ServiceGrid.tsx
├── ServiceSplit.tsx     ← composant réutilisable (7 sections l'utilisent)
├── Pillars.tsx  Sectors.tsx  Gallery.tsx  Process.tsx
└── QuoteForm.tsx  Footer.tsx  WhatsAppFab.tsx
```

`ServiceSplit` prend en props : `eyebrow, title, lead, items[], image, badge, cta, reversed, theme`. Les animations `.rv` se remplacent par Framer Motion (`whileInView`), les compteurs par un `useEffect` avec `IntersectionObserver`.

## 7. Qualité intégrée

- Responsive de 320 px aux très grands écrans, sans débordement horizontal
- Navigation clavier avec focus visible, libellés ARIA, lien d'évitement
- `prefers-reduced-motion` respecté (animations neutralisées)
- Images en `loading="lazy"`, hero en `fetchpriority="high"`
- Zéro requête bloquante hors polices Google, aucun framework chargé
- SEO : title, meta description, Open Graph, favicon, sitemap, robots, JSON-LD `ProfessionalService`, hiérarchie H1/H2/H3, `alt` sur toutes les images

---

Réalisé par **Luciole-Services** — devis@luciole-serves.com · +237 699 958 089
