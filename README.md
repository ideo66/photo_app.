# photo_app.
git init
git add .
git commit -m # Galerie Photo Complète 📸

Application web complète de gestion et d’hébergement de photos avec **Next.js + Tailwind CSS + Supabase**.

---

## 🚀 Fonctionnalités
- Authentification via Supabase (email OTP / inscription).
- Upload de photos (stockées dans Supabase Storage).
- Métadonnées enregistrées dans Postgres (table `images`).
- Galerie responsive avec affichage en grille.
- Aperçu en lightbox (agrandissement d’image au clic).
- Déconnexion sécurisée.

---

## 📂 Structure du projet
```
galerie-photo-complete/
├─ package.json
├─ tailwind.config.js
├─ postcss.config.js
├─ .env.local
├─ /pages
│  ├─ _app.js
│  ├─ index.js
├─ /components
│  ├─ Auth.jsx
│  ├─ UploadForm.jsx
│  ├─ Gallery.jsx
│  ├─ PhotoCard.jsx
├─ /lib
│  └─ supabaseClient.js
├─ /styles
│  └─ globals.css
```

---

## ⚙️ Installation locale

1. **Cloner le dépôt :**
   ```bash
   git clone https://github.com/<TON-UTILISATEUR>/galerie-photo-complete.git
   cd galerie-photo-complete
   ```

2. **Installer les dépendances :**
   ```bash
   npm install
   ```

3. **Configurer les variables d’environnement :**
   Crée un fichier `.env.local` à la racine :
   ```env
   NEXT_PUBLIC_SUPABASE_URL=https://your-project-ref.supabase.co
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
   SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
   NEXT_PUBLIC_SUPABASE_BUCKET=photos
   ```

4. **Lancer le projet :**
   ```bash
   npm run dev
   ```
   Le site sera disponible sur [http://localhost:3000](http://localhost:3000).

---

## 🗄️ Base de données Supabase

Créer la table `images` dans **Supabase SQL Editor** :
```sql
create table public.images (
  id uuid default gen_random_uuid() primary key,
  user_id uuid references auth.users(id) on delete set null,
  filename text not null,
  path text not null,
  metadata jsonb,
  created_at timestamptz default now()
);

create index on public.images (created_at desc);
```

Créer un **bucket public** dans Supabase Storage : `photos`.

---

## 🌍 Déploiement

### 🔹 Vercel
1. Connecte ton dépôt GitHub à [Vercel](https://vercel.com/).
2. Ajoute les variables d’environnement dans le dashboard (Settings → Environment Variables).
3. Déploie → ton site est en ligne 🎉

### 🔹 Netlify (alternative)
1. Lier le dépôt GitHub à Netlify.
2. Ajouter les variables `.env.local` dans le dashboard.
3. Déploiement automatique après chaque `git push`.

---

## 🔐 Sécurité & bonnes pratiques
- Ne jamais exposer `SUPABASE_SERVICE_ROLE_KEY` côté client.
- Limiter la taille d’upload (par ex. 10 Mo max).
- Ajouter une vérification côté client (type MIME).
- Option : utiliser des **signed URLs** si bucket non public.

---

## ✨ Améliorations possibles
- Catégories / tags de photos.
- Albums privés avec partage par lien.
- Génération automatique de miniatures.
- Pagination infinie avec lazy-loading.
- Quotas de stockage par utilisateur.

---

## 👨‍💻 Commandes utiles

```bash
# Lancer le projet en dev
npm run dev

# Build de production
npm run build

# Lancer le build optimisé
npm start
```

---

## 📜 Licence
Projet open-source — à personnaliser librement.

git branch -M main
git remote add origin https://github.com/ton-utilisateur/photo_app.git
git push -u origin main
