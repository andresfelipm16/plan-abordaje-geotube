# Plan de abordaje – Técnico Integral de Geotube®

App web para seguir el plan de abordaje (25 actividades, 5 semanas) con dos sesiones:

- **Técnico**: responde la evaluación de opción múltiple de cada actividad y ve sus notas.
- **Evaluador**: hace seguimiento, ve los resultados del técnico, califica, firma y registra brechas.

Se publica gratis con **GitHub Pages**. Los datos se guardan en **Firebase (Firestore)**, así todos ven lo mismo en tiempo real.
Para entrar, cada persona crea su cuenta con su correo y una contraseña, y verifica el correo una sola vez.

## Archivos

| Archivo | Para qué |
|---|---|
| `index.html` | La app completa |
| `firebase-config.js` | Datos de conexión a tu proyecto de Firebase (lo llenas tú) |
| `firestore.rules` | Quién puede leer y escribir |
| `.nojekyll` | Para que GitHub Pages sirva los archivos tal cual |

## Puesta en marcha (una sola vez, unos 20 minutos)

### 1. Crear el proyecto en Firebase (gratis, plan Spark)
1. Entra a <https://console.firebase.google.com> con una cuenta de Google y crea un proyecto (por ejemplo `plan-abordaje-geotube`). Puedes desactivar Google Analytics.
2. **Authentication → Comenzar → Método de acceso → Correo electrónico/contraseña**: actívalo (la opción de vínculo sin contraseña déjala apagada).
3. **Firestore Database → Crear base de datos**: modo producción, ubicación `southamerica-east1` (São Paulo) o la más cercana.
4. **Firestore → Reglas**: borra lo que hay, pega el contenido de `firestore.rules` y publica.
5. **Configuración del proyecto (engranaje) → Tus apps → Web (`</>`)**: registra la app y copia el objeto `firebaseConfig` en el archivo `firebase-config.js`.

### 2. Publicar en GitHub Pages
1. Crea un repositorio en GitHub (puede ser privado si tu cuenta lo permite con Pages; si no, público: las respuestas **no** quedan en el repo, quedan en Firebase).
2. Sube los 4 archivos a la raíz del repositorio.
3. **Settings → Pages → Build and deployment → Deploy from a branch → `main` / `(root)`** y guarda.
4. En un minuto queda en `https://TU-USUARIO.github.io/NOMBRE-DEL-REPO/`.

### 3. Autorizar el dominio en Firebase
**Authentication → Configuración → Dominios autorizados → Agregar dominio** y escribe `TU-USUARIO.github.io`.
Sin este paso la app no puede iniciar sesión desde GitHub Pages.

### 4. Quién puede entrar
- Cualquier correo **@geosoluciones.com** entra directo.
- Para alguien con otro correo (por ejemplo el técnico con Gmail): en **Firestore → Iniciar colección** crea la colección `acceso`, documento `usuarios`, campo `correos` de tipo **array** y agrega cada correo en minúscula.

## Uso
1. Abre el enlace. La primera vez escribe tu correo y una contraseña y toca **Crear mi cuenta**.
2. Abre el correo de verificación, toca el enlace y vuelve a la app: **Ya verifiqué mi correo**. Las siguientes veces solo **Entrar**.
3. Elige **Soy el técnico** o **Soy evaluador**. Se cambia con **Cambiar sesión**.
4. En el celular: menú del navegador → **Agregar a pantalla de inicio** para tenerla como app.

## Notas
- La fecha de inicio del plan está en **19 de noviembre de 2026**. Se cambia en *Ajustes* (sesión evaluador) y todo el cronograma se recorre en días hábiles sin festivos.
- La elección de sesión no tiene clave: cualquier persona autorizada puede entrar como evaluador. Las respuestas correctas están dentro de `index.html`.
- La carga de fotos no está activa en esta versión (Firebase Storage exige el plan de pago Blaze).
- Cualquiera puede crear una cuenta, pero solo entran a los datos los correos @geosoluciones.com verificados o los que agregues en `acceso/usuarios`.
- El plan gratuito de Firebase sobra para este uso (50.000 lecturas y 20.000 escrituras al día).
