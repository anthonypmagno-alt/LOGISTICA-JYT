# Migrar Control Logístico a otro GitHub

Este paquete contiene la versión actual de la aplicación. Puede subirse a un repositorio nuevo sin crear otra base de datos: seguirá utilizando el mismo proyecto Supabase y la misma carpeta de evidencias en Google Drive.

## Archivos que debes subir

Conserva esta estructura:

```text
index.html
app.js
styles.css
config.js
README.md
apps-script/Code.gs
supabase/schema.sql
supabase/functions/crear-usuario/index.ts
```

También puedes subir `.gitignore` y este archivo de instrucciones.

## Configuración que se conserva

En `config.js` ya está configurada la misma instancia de Supabase:

- URL: `https://qtgcpmpbtfhvoasncmkg.supabase.co`
- Clave: `SUPABASE_PUBLISHABLE_KEY`
- Zona horaria: `America/Lima`

No reemplaces la URL ni la clave publicable si deseas trabajar con los mismos usuarios y registros. Nunca agregues una clave `sb_secret_...` o `service_role` a GitHub.

`config.js` ya contiene la URL `/exec` de Apps Script. Si en el futuro vuelves a publicar la función, reemplaza únicamente ese valor por la nueva URL que termina en `/exec`.

## Pasos en el repositorio nuevo

1. Crea el repositorio nuevo en GitHub.
2. Sube todos los archivos conservando las carpetas `apps-script/` y `supabase/`.
3. En **Settings → Pages**, selecciona **Deploy from a branch**, rama `main` y carpeta `/root`.
4. Espera a que GitHub Pages publique la web.
5. Copia la nueva URL de GitHub Pages.

## Ajuste obligatorio en Supabase

Como la URL de GitHub Pages cambiará, agrega la nueva dirección en:

**Supabase → Authentication → URL Configuration → Redirect URLs**

Agrega la URL exacta de la nueva página y, si corresponde, actualiza también **Site URL**. Esto permite que el inicio de sesión funcione desde el nuevo repositorio.

## Base de datos y funciones

Si la misma Supabase ya tiene aplicada la versión actual, no debes crear otra base ni importar datos. Si todavía no aplicaste la última versión, ejecuta `supabase/schema.sql` en el SQL Editor; incluye la auditoría que permite agregar costales con código o sin código.

La función `supabase/functions/crear-usuario/index.ts` pertenece a Supabase, no a GitHub Pages. Si ya está desplegada en el proyecto actual, no es necesario volver a crearla.

## Prueba final

1. Abre la nueva URL usando HTTPS.
2. Ingresa con el mismo usuario Administrador.
3. Revisa que aparezcan los registros existentes.
4. Prueba la carga de una evidencia y la opción **Agregar costal** en una auditoría.
