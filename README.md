# Géoportail

Site cartographique pour publier vos données géographiques (couches vectorielles, rasters, images, projets) et les mettre à jour depuis une page d'administration.

## 1. Préparer Supabase

1. Créez un projet sur https://supabase.com.
2. Ouvrez **SQL Editor**, collez le contenu de `supabase/schema.sql` puis cliquez sur **Run**.
3. Créez votre compte administrateur : **Authentication > Users > Add user**, avec votre e-mail et un mot de passe.
4. Désactivez les inscriptions publiques : **Authentication > Providers > Email**, puis désactivez **Allow new users to sign up**.
5. Récupérez l'URL et la clé anon dans **Project Settings > API**.

## 2. Lancer le site sur votre ordinateur

1. Installez Node.js (version 20 ou plus) depuis https://nodejs.org.
2. Copiez `.env.example` en `.env.local` et remplacez les deux valeurs par celles de Supabase.
3. Dans un terminal, placé dans le dossier du projet :

```bash
npm install
npm run dev
```

4. Ouvrez l'adresse affichée (en général http://localhost:5173).

## 3. Ajouter vos données

Cliquez sur **Administration** en bas de la barre latérale, connectez-vous, puis :

- **Couche vectorielle** : fichier `.geojson` ou `.json` (FeatureCollection). Pour mettre à jour une couche existante, choisissez-la dans la liste « Mettre à jour une couche existante ».
- **Image** : photo (JPG ou PNG) avec sa latitude et sa longitude en degrés décimaux (WGS84).
- **Raster** : image PNG ou JPG, avec son emprise (nord, sud, est, ouest) en degrés décimaux.

Pour un GeoTIFF, exportez-le d'abord en PNG ou JPG avec QGIS (Exporter > Enregistrer la carte sous l'image) en notant son emprise.

Les coordonnées doivent être en WGS84 (EPSG:4326). Dans QGIS, reprojetez la couche avant l'export.

## 4. Mettre le site en ligne (Vercel)

1. Mettez le projet sur GitHub (sans le fichier `.env.local`, déjà exclu par `.gitignore`).
2. Sur https://vercel.com, cliquez sur **Add New > Project** et choisissez votre dépôt.
3. Dans **Environment Variables**, ajoutez `VITE_SUPABASE_URL` et `VITE_SUPABASE_ANON_KEY`.
4. Cliquez sur **Deploy**. Chaque modification poussée sur GitHub se met en ligne automatiquement.
