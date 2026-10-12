# Agenda CONDELPI — CRM Vehículos y Viviendas

Contenedor web instalable para acceder a Agenda CONDELPI, cuya interfaz de negocio se sirve desde Google Apps Script.

## Enlaces

- **Aplicación / acceso móvil:** https://saritama26-coder.github.io/agenda-condelpi/
- **Repositorio:** https://github.com/saritama26-coder/agenda-condelpi
- **Google Apps Script:** https://script.google.com/macros/s/AKfycbzZC9zWRiVMUijCYsvo10Nly5zPrZDJHS14fS2IKfS2z5HIYhHJSXHZvnwR-yhVUOT-5w/exec

## Logo oficial y acceso móvil

Los archivos `logo.png`, `icon-192.png`, `icon-512.png` y `apple-touch-icon.png` usan ahora el logotipo que proporcionó el usuario. Los iconos PWA se presentan sobre fondo blanco para mejorar su legibilidad en la pantalla de inicio; el dibujo, los colores y la proporción del logotipo se conservan.

- Página de acceso móvil con el logotipo oficial y botón para abrir el CRM directamente.
- Botón de instalación en navegadores compatibles y guía para instalación manual en iPhone/iPad y Android.
- Diseño adaptable, zonas seguras para teléfonos con muesca y objetivos táctiles grandes.
- El service worker se actualizó a `agenda-condelpi-shell-v2` para invalidar la caché anterior y volver a descargar los nuevos iconos.
- En escritorio se conserva la vista integrada con una alternativa para abrir Apps Script fuera del marco.

## Instalar en la pantalla del teléfono

**iPhone/iPad:** abre la página en Safari, toca **Compartir** y luego **Añadir a pantalla de inicio**.

**Android:** abre la página en Chrome y selecciona **Instalar aplicación** o **Añadir a pantalla principal** en el menú del navegador.

El CRM requiere conexión a internet.

## Limitaciones y tareas del backend

Este repositorio contiene el contenedor, el manifiesto, los iconos y los recursos estáticos; no contiene el código interno completo del CRM. Por eso no modifica ni certifica los permisos, formularios, tablas, almacenamiento, copias de seguridad, validaciones de datos ni las operaciones comerciales de Google Apps Script. Para auditarlos se requiere el código fuente del proyecto de Apps Script.

La vista de escritorio usa un `iframe`. Si Apps Script bloquea la incrustación, debe revisarse la configuración de `doGet()` del proyecto correcto antes de decidir si se permite incrustar el contenido. No actives `ALLOWALL` sin revisar los controles de acceso y el riesgo de *clickjacking*.

## Seguridad

GitHub Pages publica los archivos del repositorio. No guardes contraseñas, tokens, credenciales ni datos personales de clientes aquí. Los permisos de acceso deben aplicarse en el backend de Google Apps Script, no en el contenedor público.

## Publicación

Los cambios en `main` activan el flujo **Deploy Agenda CONDELPI to GitHub Pages**. Comprueba en la pestaña Actions que la ejecución más reciente termine con estado `success`.
