# Agenda CONDELPI — CRM Vehículos y Viviendas

## Acceso

- **Aplicación / instalador móvil:** https://saritama26-coder.github.io/agenda-condelpi/
- **Repositorio público del contenedor:** https://github.com/saritama26-coder/agenda-condelpi
- **Aplicación Google Apps Script:** https://script.google.com/macros/s/AKfycbwqDvHpvf4tdI-0MdH_WstIvjCi_nRoNBgm5jUPXyByo6lAtbE_mQI15Az1IuTuaAYq1w/exec

GitHub Pages sirve una página de lanzamiento e instalación; abre Apps Script en una pestaña separada. No se incrusta el CRM en un `iframe`, para no depender de habilitar la incrustación desde cualquier dominio.

## Archivos del contenedor

- `index.html`: página de acceso adaptable a móvil y escritorio.
- `manifest.json`: metadatos de la aplicación instalable.
- `logo.png`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png`: logotipo oficial del usuario en tamaños adecuados para los iconos.
- `sw.js`: caché local del instalador y sus recursos estáticos. **No almacena el CRM ni datos de clientes.**

## Instalar en el teléfono

**iPhone/iPad:** abre el enlace en Safari, pulsa **Compartir** y luego **Añadir a pantalla de inicio**.

**Android:** abre el enlace en Chrome y selecciona **Instalar aplicación** o **Añadir a pantalla principal**.

El icono solo abre la página de acceso; desde ella se pulsa **Abrir Agenda CONDELPI**. El CRM necesita internet. Si el icono viejo persiste, elimina el acceso directo anterior y vuelve a añadirlo.

## Actualizar el backend de Apps Script

La interfaz y la lógica del CRM están en un paquete separado, porque este repositorio público no debe contener los datos ni el código interno del backend.

1. Primero duplica la hoja de cálculo de producción y guarda una copia del proyecto actual.
2. Abre **Extensiones → Apps Script** desde la hoja que usa el CRM.
3. En el proyecto vinculado, actualiza los archivos existentes con los archivos del paquete privado `Apps_Script/Codigo.gs`, `Apps_Script/Mensajeria.gs` y `Apps_Script/Formulario.html`. Conserva los nombres exactos. No agregues `Index.html`: la función `doGet()` sirve `Formulario.html`.
4. Guarda y ejecuta desde la hoja **CRM Ventas → 1. Configurar sistema (primer uso)**. Autoriza los permisos de Sheets y Drive cuando Google los solicite. Esta acción configura el CRM y trata de instalar el respaldo semanal y los recordatorios.
5. Ejecuta **CRM Ventas → Configurar clave de acceso (teléfono)** y define una clave fuerte de al menos 8 caracteres.
6. Ejecuta **CRM Ventas → Crear respaldo ahora** y confirma que aparezca un archivo en la carpeta de Google Drive `Agenda_CONDELPI_Respaldos`.
7. Prueba registrar y editar un contacto, validar CI/RUC, agendar/reprogramar/cancelar una cita, exportar Excel y revisar el historial de correo. Las campañas de correo automáticas son opcionales: actívalas solo cuando hayas verificado el consentimiento y las plantillas.
8. En **Implementar → Gestionar implementaciones**, edita la implementación de aplicación web y selecciona **Nueva versión → Implementar**. La URL `/exec` debería permanecer estable en la implementación editada, pero compruébala antes de usarla.
9. Verifica que el proyecto desplegado sea el de la hoja de producción correcta. No publiques `Codigo.gs` ni datos de clientes en el repositorio público.

El código de Apps Script no se puede desplegar directamente desde esta conexión; debe guardarse y autorizarse desde la cuenta dueña del proyecto.

## Mejoras realizadas en el paquete fuente

- Acceso al servidor antes de mostrar las funciones protegidas; la clave no se almacena en `localStorage`.
- Hash de clave con sal guardado en propiedades del proyecto y migración del hash anterior tras un acceso válido.
- Validaciones de identificación ecuatoriana CI/RUC, correo, teléfono, fechas, listas, campos y longitudes en servidor.
- Evita que textos iniciados por `=`, `+`, `-` o `@` se conviertan en fórmulas al escribir texto en Sheets.
- Bloqueos de concurrencia para registros, citas y marcado de envíos de WhatsApp; prevención de conflictos de horario.
- Registro de alta/revocación del consentimiento de comunicaciones y filtros de consentimiento, canal, frecuencia y límite de mensajes.
- Envío de correo limitado por cuota disponible y por contactos por ejecución, con registro de resultados.
- Cola WhatsApp manual; el CRM solo abre `wa.me` y no afirma enviar por su cuenta.
- Copia semanal de la hoja de datos en Google Drive con retención de hasta 30 copias, más copia manual.
- Interfaz más adaptable, logotipo oficial visible y mensajes de error más claros.
- `doGet()` ya no solicita `ALLOWALL`; por eso el lanzador no usa iframe.

## Limitaciones que requieren verificación en la cuenta

El paquete fue revisado estáticamente y los archivos JavaScript pasan la comprobación sintáctica de Node después de sustituir los marcadores de plantilla de Apps Script. No equivale a una ejecución dentro de Google Apps Script. Hace falta autorizar Sheets, Drive, MailApp y Calendar según el uso, así como realizar pruebas de usuario en la hoja duplicada. Los respaldos copian la hoja de cálculo, no el código del proyecto; mantén una copia de los archivos fuente por separado.

El recordatorio de citas puede enviar correos; la campaña diaria de seguimiento solo debe activarse tras validar la base legal/consentimiento, las plantillas y el horario. Google ejecuta los disparadores en franjas aproximadas, no necesariamente en el minuto exacto.

## Corrección de citas que no aparecían (11/10/2026)

- Causa identificada en el registro de ejecuciones: en las versiones 12 y 13 de la aplicación web, `listarCitas` fallaba con `ReferenceError: leerConfig_ is not defined`, porque el proyecto tenía una versión reducida de `Mensajeria.gs` sin esa función.
- Solución: se instalaron en el proyecto vinculado los archivos completos del paquete (`Codigo.gs`, `Mensajeria.gs`, `Formulario.html`). En la implementación de prueba (`/dev`) la agenda muestra todas las citas registradas.
- `listarCitas()` acepta fechas nativas, seriales y de texto (`dd/mm/aaaa`, `aaaa-mm-dd`); la vista inicial es **Todas las citas**.
- Nuevo menú **CRM Ventas → Revisar citas que no aparecen**: muestra el libro y la pestaña que lee el script y los problemas de fecha, hora, ID o estado por fila.
- Pendiente: publicar una **Nueva versión** de la implementación web para que la URL `/exec` use el código corregido.
- Disparadores antiguos `recordatoriosCitas` y `tareaDiaria`, creados por otra cuenta, deben eliminarse desde esa cuenta: sus funciones ya no existen en el código.

## Publicación

El flujo **Deploy Agenda CONDELPI to GitHub Pages** publica los cambios de la rama `main`. Revisa Actions tras cada actualización.
