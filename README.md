# Agenda CONDELPI — CRM Vehículos y Viviendas

Página de acceso para Agenda CONDELPI. La página de GitHub Pages abre la aplicación de Google Apps Script en una pestaña nueva porque los navegadores pueden bloquear la aplicación cuando se intenta mostrar dentro de un `iframe`.

## Archivos

- `index.html`: página de acceso responsive con enlace a la aplicación.
- `manifest.json`: metadatos de la aplicación instalable.
- `logo.png`: icono opcional que debe agregarse a la raíz del repositorio para que estén disponibles los iconos del manifiesto.
- `.github/workflows/deploy-pages.yml`: flujo que publica el contenido de la rama `main` en GitHub Pages.

## Aplicación

La URL configurada se encuentra en `index.html`. Si cambia la implementación de Apps Script, actualiza el enlace allí.

## Publicación

GitHub Pages está configurado para utilizar **GitHub Actions**. El flujo se ejecuta al actualizar la rama `main` y también admite ejecución manual desde **Actions → Deploy Agenda CONDELPI to GitHub Pages → Run workflow**.

Comprueba que la ejecución termine correctamente antes de compartir la página publicada.

## Seguridad

No incrustes la aplicación de Apps Script en un `iframe` si el servicio bloquea la incrustación. Abrirla como página principal en una pestaña separada evita ese bloqueo del navegador sin tener que permitir que otros sitios incrusten la aplicación.

No añadas contraseñas, claves API ni secretos al código público del repositorio.
