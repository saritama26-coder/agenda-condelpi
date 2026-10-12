# Agenda CONDELPI — CRM Vehículos y Viviendas

Contenedor web instalable para acceder a Agenda CONDELPI, cuya interfaz de negocio se sirve desde Google Apps Script.

## Enlaces

- **Aplicación / acceso móvil:** https://saritama26-coder.github.io/agenda-condelpi/
- **Repositorio:** https://github.com/saritama26-coder/agenda-condelpi
- **Google Apps Script:** https://script.google.com/macros/s/AKfycbzZC9zWRiVMUijCYsvo10Nly5zPrZDJHS14fS2IKfS2z5HIYhHJSXHZvnwR-yhVUOT-5w/exec

## Cambios del contenedor

- Página de acceso móvil con el logotipo de CONDELPI y botón de apertura directa del CRM.
- Iconos PNG para manifest/PWA y para añadir el acceso a la pantalla de inicio.
- Diseño adaptable, áreas seguras para pantallas con muesca y objetivos táctiles grandes.
- Botón de instalación en navegadores compatibles y guía para la instalación manual en iPhone/iPad.
- Service worker que guarda la página de acceso y sus recursos estáticos para disponibilidad básica sin conexión. El CRM requiere conexión a internet y no se usa ni se almacena información del CRM en la caché del contenedor.
- En escritorio se conserva la vista integrada con un enlace alternativo para abrir Apps Script fuera del marco.

## Instalar en la pantalla del teléfono

**iPhone/iPad:** abre el enlace de la aplicación en Safari, toca **Compartir** y después **Añadir a pantalla de inicio**.

**Android:** abre el enlace en Chrome, abre el menú de tres puntos (⋮) y selecciona **Instalar aplicación** o **Añadir a pantalla principal**. Cuando el navegador muestre el botón de instalación en la página, también puedes usarlo.

## Limitaciones y tareas del backend

Este repositorio incluye el contenedor web, el manifiesto, iconos y recursos estáticos; no incluye el código interno completo del CRM. Por tanto, no modifica ni certifica los permisos, formularios, tablas, almacenamiento, copias de seguridad, validaciones de datos ni las operaciones comerciales de Google Apps Script. Para auditar y corregir esas funciones hace falta el código fuente del proyecto de Apps Script.

La vista de escritorio usa un `iframe`. Si Google Apps Script bloquea la incrustación, debe probarse la apertura directa y revisar la configuración de `doGet()` del proyecto correcto antes de decidir si se permite incrustar el contenido. No actives `ALLOWALL` sin revisar los controles de acceso y el riesgo de *clickjacking*.

## Seguridad

GitHub Pages publica los archivos de este repositorio. No guardes contraseñas, tokens, credenciales ni datos personales de clientes aquí. Los permisos de acceso deben aplicarse en el backend de Google Apps Script, no en el contenedor público.

## Publicación

Los cambios en la rama `main` activan el flujo **Deploy Agenda CONDELPI to GitHub Pages**. Comprueba en la pestaña Actions que la ejecución más reciente termine con estado `success`.
