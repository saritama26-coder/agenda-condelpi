# Agenda CONDELPI — CRM Vehículos y Viviendas

Contenedor PWA de Agenda CONDELPI servido por GitHub Pages. La interfaz de negocio se entrega desde Google Apps Script dentro de un `iframe`, siguiendo el patrón del proyecto PROFORMA GASV.

## Enlaces de acceso

- **Aplicación publicada en GitHub Pages:** https://saritama26-coder.github.io/agenda-condelpi/
- **Implementación actual de Google Apps Script:** https://script.google.com/macros/s/AKfycbzZC9zWRiVMUijCYsvo10Nly5zPrZDJHS14fS2IKfS2z5HIYhHJSXHZvnwR-yhVUOT-5w/exec


## Archivos principales

- `index.html`: carga la URL `/exec` de Agenda CONDELPI a pantalla completa dentro de un `iframe`.
- `manifest.json`: metadatos de la aplicación instalable.
- `logo.png`: icono referenciado por el HTML y el manifiesto; agrega el archivo en la raíz si deseas que aparezca el icono de CONDELPI.
- `.github/workflows/deploy-pages.yml`: publica automáticamente el sitio cuando hay cambios en `main`.

## Cambio obligatorio dentro de Google Apps Script

**El `iframe` de GitHub Pages no funcionará hasta que el proyecto de Google Apps Script permita la incrustación.** En el editor del proyecto correcto de CONDELPI, localiza la función existente `doGet()`. En la cadena que devuelve `HtmlOutput`, añade esta llamada al objeto `HtmlOutput` después de `.evaluate()` y antes del punto y coma final:

```javascript
.setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL)
```

Por ejemplo, si la función ya utiliza una plantilla HTML llamada `Index`, el retorno tendría esta forma:

```javascript
return HtmlService.createTemplateFromFile('Index')
  .evaluate()
  .setTitle('Agenda CONDELPI')
  .addMetaTag('viewport', 'width=device-width, initial-scale=1, viewport-fit=cover')
  .setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL);
```

No pegues una segunda función `doGet()` al final del archivo: modifica la existente y conserva cualquier lógica propia de CONDELPI que ya contenga. Usa el nombre real del archivo HTML si no se llama `Index`.

Después, guarda el proyecto y abre **Implementar → Gestionar implementaciones → Editar** (icono de lápiz), selecciona **Nueva versión** y pulsa **Implementar**. Comprueba que la URL `/exec` permanece igual. La configuración `ALLOWALL` permite que otros sitios incrusten la aplicación; úsala solo si es adecuado para la información manejada por CONDELPI y revisa sus controles de acceso frente a *clickjacking*.

## Publicar en GitHub Pages

GitHub Pages utiliza **GitHub Actions**. Tras guardar cambios, revisa la ejecución del flujo **Deploy Agenda CONDELPI to GitHub Pages** y confirma que termine correctamente.

- Repositorio: https://github.com/saritama26-coder/agenda-condelpi
- Sitio: https://saritama26-coder.github.io/agenda-condelpi/

## Nota de seguridad

GitHub Pages publica el código HTML al público. No guardes secretos, credenciales ni datos de clientes en este repositorio. La autorización a datos del CRM debe permanecer en Apps Script/los servicios de backend.
