# HairCare AI — primera versión

Proyecto inicial para una aplicación web adaptable y Android (Capacitor).

## Qué incluye
- Interfaz adaptable a móvil y escritorio.
- Selector de perfiles familiares de demostración.
- Selección de fotografía desde galería/cámara del navegador.
- API Node para enviar la foto a Gemini y devolver orientación cosmética.
- Base preparada para Supabase Auth.
- Configuración inicial de Capacitor para Android.

**Importante:** esta entrega es una base funcional de interfaz y API, no una app familiar lista para producción. Los perfiles de la pantalla sin Supabase son de demostración; todavía no guardan cuentas ni historiales en la nube. No subas fotos sensibles hasta activar autenticación, permisos, almacenamiento privado y políticas de acceso. El análisis por imagen es orientativo, no médico.

## 1. Requisitos
- Node.js 20 o superior.
- Una cuenta de Supabase para registro e inicio de sesión.
- Una clave de Gemini API para activar análisis real. Consulta los límites y precios vigentes antes de usarla.

## 2. Preparar la aplicación web
En la carpeta raíz:
```bash
npm install
cp .env.example .env
npm run dev
```
Abre la URL que Vite muestre. Sin configurar Supabase, se abre una vista de demostración. El análisis real requiere que el servidor esté iniciado y tenga una clave válida.

## 3. Activar análisis con IA
En Google AI Studio crea una clave de Gemini. Copia la clave únicamente en `GEMINI_API_KEY` del archivo `.env` del servidor. Nunca la pongas en una variable `VITE_` ni la publiques en GitHub.
```bash
cd server
npm install
```
Configura `GEMINI_API_KEY` y `PORT=3001` en el entorno del servidor y ejecuta:
```bash
npm start
```
En el `.env` de la raíz configura `VITE_API_URL` con la dirección de tu API. Para una web publicada, debe ser la URL HTTPS de tu servidor desplegado, no `localhost`.

## 4. Cuentas privadas con Supabase
1. Crea un proyecto en https://supabase.com.
2. Copia Project URL y anon/public key al `.env` como `VITE_SUPABASE_URL` y `VITE_SUPABASE_ANON_KEY`.
3. Configura confirmación de correo y políticas RLS antes de guardar información personal.
4. La pantalla de acceso usa Supabase Auth cuando estas variables están configuradas.

La gestión real de miembros familiares, permisos de administrador, historial persistente y almacenamiento privado aún debe implementarse antes de producción. No basta con ocultar botones: los permisos deben verificarse en el servidor/base de datos.

## 5. Crear proyecto Android
Desde la raíz, después de instalar dependencias:
```bash
npm run build
npx cap add android
npx cap sync android
```
Abre `android/` en Android Studio para compilar APK. También puedes configurar GitHub Actions una vez que el proyecto web esté probado.

## 6. Privacidad y seguridad
- No guardes claves secretas en GitHub.
- No hagas públicos los archivos de fotos.
- Usa permisos de acceso por usuario y políticas RLS.
- Ofrece borrar cuenta, fotos e historial.
- Pide consentimiento antes de subir fotos.
- No uses el análisis como diagnóstico ni sustituto de un dermatólogo.

## Estructura
- `src/`: aplicación web.
- `server/`: API para análisis con Gemini.
- `capacitor.config.json`: configuración Android.
- `.env.example`: variables de entorno de ejemplo.
