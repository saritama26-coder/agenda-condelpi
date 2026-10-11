# Agenda CONDELPI — CRM Vehículos y Viviendas

Repositorio web para el contenedor PWA de Agenda CONDELPI. La interfaz se carga desde una aplicación de Google Apps Script mediante un `iframe`.

## Archivos

- `index.html`: página contenedora para escritorio y móvil.
- `manifest.json`: metadatos de la aplicación instalable.
- `logo.png`: archivo de imagen que debes agregar; se referencia como icono y acceso directo móvil.

## Configuración antes de publicar

- La URL `/exec` de Google Apps Script ya está configurada en `index.html`.
- Agrega `logo.png` en la raíz del repositorio. El manifiesto lo referencia en tamaños de 192×192 y 512×512.
- Prueba la URL de Apps Script directamente y luego comprueba la página contenedora en móvil y escritorio.

**Importante:** no publiques una URL de Apps Script sin verificar que corresponda a esta aplicación. La dirección estará visible en el código del cliente. No incluyas contraseñas, claves API ni otros secretos en `index.html`.

## Publicar con GitHub Pages

1. Sube estos archivos a la rama `main` en la raíz del repositorio.
2. En GitHub, entra en **Settings → Pages**.
3. En **Build and deployment**, selecciona **Deploy from a branch**, elige `main` y la carpeta `/(root)`, y guarda.
4. Espera a que GitHub Pages indique que el sitio está publicado y prueba la URL resultante.

Si el CRM contiene datos personales o información de clientes, mantén el código y los datos protegidos y revisa la visibilidad del repositorio y los permisos de acceso antes de publicarlo.
