<img src=".github/cabecera.svg" width="100%" alt="CentinelaWP — seguridad para WordPress: antivirus, cortafuegos, doble factor y copias de seguridad">

<div align="center">

![WordPress](https://img.shields.io/badge/WordPress-5.8+-07070C?style=for-the-badge&logo=wordpress&logoColor=00E5FF&labelColor=07070C)
![PHP](https://img.shields.io/badge/PHP-7.4--8.2-07070C?style=for-the-badge&logo=php&logoColor=B026FF&labelColor=07070C)
![Tests](https://img.shields.io/badge/PHPUnit_·_PHPCS_·_PHPStan-07070C?style=for-the-badge&logo=github&logoColor=00E5FF&labelColor=07070C)
![Estado](https://img.shields.io/badge/Desarrollo_activo-07070C?style=for-the-badge&logoColor=B026FF&labelColor=07070C)

</div>

Suite de seguridad todo en uno para WordPress, pensada para que cualquiera —tenga o no conocimientos técnicos— pueda proteger su sitio sin sentirse perdido. Se instala con **todo desactivado por defecto** y un asistente de bienvenida explica, paso a paso, qué hace cada protección antes de activarla.

> [!WARNING]
> Proyecto personal y educativo. **No ha sido auditado profesionalmente.** Revisa el código antes de usarlo en producción.

<img src=".github/separador.svg" width="100%" alt="">

## Cómo funciona

Cada petición atraviesa varias capas antes de tocar WordPress. Si falla en cualquiera de ellas, se queda fuera y queda registrada.

<img src=".github/flujo.svg" width="100%" alt="Recorrido de una petición: pasa el cortafuegos, el login endurecido y el doble factor antes de llegar a WordPress">

<img src=".github/separador.svg" width="100%" alt="">

## Qué hace

<table>
<tr>
<td width="50%" valign="top">

**Puntuación de seguridad 0–100**

Calculada según las protecciones activas, con recomendaciones clicables que llevan directas al ajuste.

</td>
<td width="50%" valign="top">

**Modo pánico**

Un botón que endurece el sitio al instante: bloqueo de login al primer fallo, cortafuegos agresivo y modo solo lectura.

</td>
</tr>
<tr>
<td width="50%" valign="top">

**Antivirus con seis modos**

Desde una revisión de `/uploads/` hasta un análisis completo del núcleo. Analiza cualquier archivo de texto, no solo PHP.

</td>
<td width="50%" valign="top">

**Integridad por hash**

Línea base del núcleo, plugins y tema. Diff línea a línea de qué cambió en `wp-config.php` y restauración con un clic.

</td>
</tr>
</table>

<img src=".github/separador.svg" width="100%" alt="">

## Todo lo que incluye

<details>
<summary><b>Dashboard</b> · puntuación, modo pánico y actividad</summary>

<br>

- Puntuación de seguridad de 0 a 100 según las protecciones activas, con recomendaciones clicables
- **Modo pánico**: endurece el sitio al instante ante la sospecha de un ataque en curso
- Ranking de las IP con más bloqueos, con su país de origen
- Gráfica de actividad bloqueada de los últimos 30 días
- Deshacer el último cambio de configuración con un clic

</details>

<details>
<summary><b>Protección</b> · endurecimiento general</summary>

<br>

- Ocultar la versión de WordPress: meta generator, `readme.html`, `license.txt` y el `?ver=` de scripts y estilos
- Desactivar el editor de archivos del escritorio y XML-RPC
- Bloquear la enumeración de usuarios (`?author=`) y ocultarlos en la API REST
- Cabeceras de seguridad HTTP: `X-Frame-Options`, `X-Content-Type-Options` y demás
- Bloqueo de ejecución de PHP en `/uploads/`
- Forzar HTTPS, proteger `debug.log` y bloquear el listado de directorios

</details>

<details>
<summary><b>Login</b> · contra fuerza bruta y automatismos</summary>

<br>

- Límite de intentos con bloqueo temporal por IP
- Mensajes de error genéricos: no revela si falló el usuario o la contraseña
- **URL de login personalizada**: `wp-login.php` y `/wp-admin/` devuelven un 404 real —no una redirección— a quien no tenga sesión
- Honeypot invisible y captcha visible por pregunta matemática, sin depender de servicios externos
- Protección de "¿olvidaste tu contraseña?" y de las contraseñas de aplicación de la REST API

</details>

<details>
<summary><b>Cortafuegos</b> · filtrado por origen</summary>

<br>

- Lista negra y lista blanca de IP
- Bloqueo de nodos de salida Tor, desde la lista pública oficial
- Reputación de IP mediante AbuseIPDB, opcional y con tu propia clave gratuita

</details>

<details>
<summary><b>Autenticación</b> · doble factor y control de sesiones</summary>

<br>

- 2FA por email o TOTP, compatible con Google Authenticator
- El método por email **exige verificarlo con un código de prueba antes de activarlo**, para que nunca puedas quedarte fuera por un correo que no llega
- Política de contraseñas fuertes: longitud, mayúscula, número y símbolo
- Gestión de sesiones activas por usuario, con cierre forzado
- Alerta de administradores nuevos o inesperados, y de accesos correctos desde un país nuevo
- Vigilancia de capacidades peligrosas en roles que no son administrador, rastro típico de una puerta trasera

</details>

<details>
<summary><b>Horario de acceso</b> · la puerta, no el sitio</summary>

<br>

Restringe el panel de administración y el login a un horario concreto por día de la semana. La web pública sigue funcionando siempre con normalidad: esto no cierra el sitio, solo la puerta de entrada para modificarlo.

</details>

<details>
<summary><b>Antivirus</b> · escáner de malware</summary>

<br>

- **Seis modos de escaneo**: Simple (`/uploads/`), Normal (plugins, temas y uploads), Completo (añade el núcleo), Plugins, Temas y Archivos recientes (solo lo modificado en 48 horas)
- Analiza cualquier archivo de texto, no solo `.php`: también `.js`, `.html`, `.htaccess`, `.json`
- Heurística de patrones —webshells conocidos, `eval` con `base64`, ejecución de comandos— con filtrado para evitar falsos positivos en archivos legítimos del núcleo
- Barra de progreso en tiempo real, cuarentena manual o automática, y copia de seguridad antes de poner nada en cuarentena
- Escaneo automático al subir archivos y bloqueo de dobles extensiones (`foto.jpg.php`)
- Firmas actualizables desde una URL propia, sin reinstalar el plugin

</details>

<details>
<summary><b>Analizador de plugins</b> · vulnerabilidades conocidas</summary>

<br>

- Compara la versión instalada contra WordPress.org
- Vulnerabilidades reales y documentadas (CVE) mediante la API de WPScan, opcional y con token gratuito
- Aviso al activarse un plugin nuevo

</details>

<details>
<summary><b>Integridad de archivos</b> · qué ha cambiado y cuándo</summary>

<br>

- Línea base por hash del núcleo de WordPress, los plugins activos y el tema activo
- Vigilancia inmediata de `wp-config.php` y `.htaccess`
- Diff línea a línea de qué cambió, con botón de restaurar en un clic

</details>

<details>
<summary><b>Mantenimiento</b> · sin dejarte fuera</summary>

<br>

- Modo mantenimiento con enlace de vista previa para tu equipo
- Modo solo lectura: bloquea formularios sin cerrar la lectura del sitio, diseñado para no poder bloquear nunca el propio login
- Interruptor de emergencia para cortar todos los correos del plugin si tu servidor de correo falla

</details>

<details>
<summary><b>Notificaciones</b> · email, Telegram y Discord</summary>

<br>

- Avisos por email, Telegram y Discord
- Resumen semanal automático
- Envío desacoplado en segundo plano vía WP-Cron: un fallo de correo nunca puede reventar la acción que lo disparó

</details>

<details>
<summary><b>Actividad y registro</b> · trazabilidad</summary>

<br>

- Registro de quién ha iniciado sesión, editado contenido o activado plugins
- Exportación automática a archivo, diaria, semanal o mensual, con descarga desde el panel
- Registro completo de eventos de seguridad con severidad y filtros

</details>

<details>
<summary><b>Herramientas</b> · lo que no cabía en otro sitio</summary>

<br>

- Comprobación de permisos de archivos críticos, con aviso de que no es fiable en Windows
- **URLs señuelo**: quien visite una ruta falsa se banea automáticamente
- Generador de `security.txt` según la RFC 9116
- Exportar e importar toda la configuración en `.json`
- Informe de seguridad descargable en HTML, imprimible como PDF
- Copia de seguridad en `.zip` antes de que WordPress actualice un plugin o un tema

</details>

<details>
<summary><b>Spam en base de datos</b> · SEO inyectado</summary>

<br>

- Detecta spam SEO inyectado —enlaces ocultos, palabras clave— en entradas, comentarios y widgets
- Compara los enlaces salientes de tu contenido contra URLhaus de abuse.ch, sin necesitar clave de API

</details>

<img src=".github/separador.svg" width="100%" alt="">

## Pensado para no perderse

La mayoría de plugins de seguridad se instalan con todo activado y el primer día te dejan fuera de tu propio sitio. Aquí es al revés:

- **Asistente de bienvenida de 7 pasos** la primera vez, relanzable cuando quieras desde el Dashboard
- Feedback instantáneo en cada botón, y mensajes que dicen exactamente qué has cambiado en vez de un "guardado" a secas
- Panel organizado en categorías —Dashboard, Protección, Escaneo y detección, Gestión, Registros— en lugar de una lista interminable de pestañas

<img src=".github/separador.svg" width="100%" alt="">

## Instalación

1. Descarga el `.zip` del plugin
2. En WordPress: **Plugins → Añadir nuevo → Subir plugin**
3. Actívalo y sigue el asistente de bienvenida

**Requisitos:** WordPress 5.8 o superior · PHP 7.4 o superior · extensión `ZipArchive` para la copia previa a actualizaciones (opcional)

<img src=".github/separador.svg" width="100%" alt="">

## Desarrollo y calidad

```bash
composer install
bash bin/install-wp-tests.sh wordpress_test root '' localhost latest

composer test       # PHPUnit
composer lint       # PHPCS, estándares de WordPress
composer analyse    # PHPStan
```

**Tests** — en `tests/`, con PHPUnit y `WP_UnitTestCase`, incluyendo pruebas de regresión de fallos reales encontrados durante el desarrollo: que guardar una pestaña no resetee las demás, que la cadena de hashes del registro detecte manipulación, y otras.

**Integración continua** — `.github/workflows/ci.yml` ejecuta tests, PHPCS y PHPStan en cada push y cada pull request, sobre PHP 7.4 a 8.2.

**Seguridad de segunda capa** — interruptor de emergencia `WPSS_DISABLE`, cifrado en reposo de los secretos, registro con cadena de hashes, firmas HMAC de las reglas del escáner y límite de intentos con tabla propia en vez de transients, para no depender del backend de caché.

**Documentación** — [`THREAT_MODEL.md`](THREAT_MODEL.md) explica qué protege este plugin y, más importante, qué no. [`SECURITY.md`](SECURITY.md) describe cómo reportar una vulnerabilidad de forma responsable. [`CHANGELOG.md`](CHANGELOG.md) sigue versionado semántico, con las correcciones de seguridad marcadas explícitamente.

<img src=".github/separador.svg" width="100%" alt="">

## Lo que todavía no está resuelto

Esta ronda de mejoras añadió seguridad de segunda capa y andamiaje de calidad. Lo siguiente queda pendiente a propósito, por riesgo o por alcance, y se documenta en vez de fingir que está hecho:

- **Inyección de dependencias completa.** Varias clases aceptan `$settings` inyectado en el constructor, pero caen a una llamada estática si no se les pasa. No es DI pura.
- **Separación de lógica y presentación.** El HTML de las pestañas del panel vive en `class-wpss-admin.php`, no en plantillas aparte.
- **Cobertura de tests exhaustiva.** Hay pruebas de las piezas más críticas, no de las treinta y pico clases al completo.

<img src=".github/separador.svg" width="100%" alt="">

## Licencia

Ver [`LICENSE.txt`](LICENSE.txt). Uso gratuito, sin reventa ni redistribución o modificación por terceros. Las sugerencias de mejora son bienvenidas por la pestaña Issues.

---

Hecho por [Maitini](https://github.com/Maitini) · [LinkedIn](https://www.linkedin.com/in/maitini1812/)
