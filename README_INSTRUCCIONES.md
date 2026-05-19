# Cómo publicar esta app en GitHub Pages

Tu archivo original era código React, no un HTML normal. Por eso ahora está convertido a proyecto React con Vite.

## 1. Sube estos archivos al repositorio
Sube TODO el contenido de esta carpeta al repositorio:

`III-Congreso-FOL--SIMARED-FP`

No subas la carpeta dentro del repositorio; sube los archivos de dentro.

Deben verse archivos como:

- package.json
- index.html
- vite.config.js
- src/App.jsx
- src/main.jsx
- .github/workflows/deploy.yml

## 2. Configura GitHub Pages
En el repositorio entra en:

Settings → Pages

En “Source”, selecciona:

GitHub Actions

## 3. Crea Firebase
Esta app necesita Firebase para recibir ideas en tiempo real desde móviles.

En Firebase:

1. Crea un proyecto.
2. Añade una app web.
3. Copia la configuración de Firebase.
4. Activa Authentication → Sign-in method → Anonymous.
5. Activa Firestore Database.
6. En reglas de Firestore, para pruebas puedes usar:

```txt
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /artifacts/{appId}/public/data/ideas/{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

## 4. Añade las claves a GitHub Secrets
En GitHub ve a:

Settings → Secrets and variables → Actions → New repository secret

Crea estos secrets, uno por uno:

- VITE_FIREBASE_API_KEY
- VITE_FIREBASE_AUTH_DOMAIN
- VITE_FIREBASE_PROJECT_ID
- VITE_FIREBASE_STORAGE_BUCKET
- VITE_FIREBASE_MESSAGING_SENDER_ID
- VITE_FIREBASE_APP_ID

## 5. Publicación automática
Cuando subas los archivos a la rama `main`, GitHub Actions compilará la app automáticamente.

La web quedará en:

https://yaizatbdocencia-cmd.github.io/III-Congreso-FOL--SIMARED-FP/

## 6. Enlace para participantes
Cuando esté publicada, el QR de la app generará automáticamente el enlace de participante:

https://yaizatbdocencia-cmd.github.io/III-Congreso-FOL--SIMARED-FP/?role=participant
