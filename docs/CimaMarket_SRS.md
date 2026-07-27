# Software Requirements Specification (SRS)

## Cima Market — Plataforma de Compra-Venta para Estudiantes UABC

| Campo                   | Detalle                             |
| ----------------------- | ----------------------------------- |
| **Nombre del Producto** | Cima Market                         |
| **Versión**             | 1.1.0                               |
| **Fecha**               | 20 de Julio de 2026                 |
| **Estado**              | Aprobado                            |
| **Autor**               | Mike Armando Montano Valencia       |
| **Clasificación**       | Interno — Uso Académico/Estudiantil |

---

## Historial de Cambios

| Versión | Fecha               | Sección       | Cambio                                                                                                                                                                |
| ------- | ------------------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.1.0   | 27 de Julio de 2026 | §5 (Módulo 8) | Se agrega RF-MOD-05 (reporte general de la plataforma) para formalizar la acción "Reportar un problema" de P-11, que no tenía requisito ni trazabilidad hacia el SDD. |

---

## Tabla de Contenidos

- [Software Requirements Specification (SRS)](#software-requirements-specification-srs)
  - [Cima Market — Plataforma de Compra-Venta para Estudiantes UABC](#cima-market--plataforma-de-compra-venta-para-estudiantes-uabc)
  - [Historial de Cambios](#historial-de-cambios)
  - [Tabla de Contenidos](#tabla-de-contenidos)
  - [1. Introducción](#1-introducción)
    - [1.1 Propósito del Documento](#11-propósito-del-documento)
    - [1.2 Alcance del Sistema](#12-alcance-del-sistema)
    - [1.3 Contexto y Problemática](#13-contexto-y-problemática)
    - [1.4 Acrónimos y Abreviaturas](#14-acrónimos-y-abreviaturas)
    - [1.5 Referencias](#15-referencias)
  - [2. Descripción General del Sistema](#2-descripción-general-del-sistema)
    - [2.1 Perspectiva del Producto](#21-perspectiva-del-producto)
    - [2.2 Funciones Principales del Producto](#22-funciones-principales-del-producto)
    - [2.3 Características de los Usuarios](#23-características-de-los-usuarios)
    - [2.4 Restricciones Generales](#24-restricciones-generales)
  - [3. Stakeholders y Usuarios](#3-stakeholders-y-usuarios)
  - [4. Suposiciones y Dependencias](#4-suposiciones-y-dependencias)
    - [4.1 Suposiciones](#41-suposiciones)
    - [4.2 Dependencias Externas](#42-dependencias-externas)
  - [5. Requisitos Funcionales](#5-requisitos-funcionales)
    - [Módulo 1: Autenticación y Gestión de Cuentas](#módulo-1-autenticación-y-gestión-de-cuentas)
      - [RF-AUTH-01 — Acceso público sin autenticación](#rf-auth-01--acceso-público-sin-autenticación)
      - [RF-AUTH-02 — Autenticación diferida](#rf-auth-02--autenticación-diferida)
      - [RF-AUTH-03 — Registro e inicio de sesión](#rf-auth-03--registro-e-inicio-de-sesión)
      - [RF-AUTH-04 — Onboarding](#rf-auth-04--onboarding)
      - [RF-AUTH-05 — Sesión persistente y renovación de tokens](#rf-auth-05--sesión-persistente-y-renovación-de-tokens)
      - [RF-AUTH-06 — Activación del rol vendedor](#rf-auth-06--activación-del-rol-vendedor)
      - [RF-AUTH-07 — Gestión de perfil de usuario](#rf-auth-07--gestión-de-perfil-de-usuario)
      - [RF-AUTH-08 — Cierre de sesión y revocación de tokens](#rf-auth-08--cierre-de-sesión-y-revocación-de-tokens)
      - [RF-AUTH-09 — Eliminación de cuenta](#rf-auth-09--eliminación-de-cuenta)
    - [Módulo 2: Gestión de Publicaciones](#módulo-2-gestión-de-publicaciones)
      - [RF-PUB-01 — Crear publicación](#rf-pub-01--crear-publicación)
      - [RF-PUB-02 — Editar y eliminar publicación](#rf-pub-02--editar-y-eliminar-publicación)
      - [RF-PUB-03 — Pausar y reactivar publicación](#rf-pub-03--pausar-y-reactivar-publicación)
      - [RF-PUB-04 — Límite de publicaciones](#rf-pub-04--límite-de-publicaciones)
      - [RF-PUB-05 — Categorías de productos](#rf-pub-05--categorías-de-productos)
      - [RF-PUB-06 — Moderación automática de imágenes](#rf-pub-06--moderación-automática-de-imágenes)
    - [Módulo 3: Catálogo y Búsqueda](#módulo-3-catálogo-y-búsqueda)
      - [RF-CAT-01 — Catálogo principal](#rf-cat-01--catálogo-principal)
      - [RF-CAT-02 — Búsqueda por texto](#rf-cat-02--búsqueda-por-texto)
      - [RF-CAT-03 — Filtros avanzados](#rf-cat-03--filtros-avanzados)
      - [RF-CAT-04 — Ordenamiento](#rf-cat-04--ordenamiento)
    - [Módulo 4: Contacto con Vendedor vía WhatsApp](#módulo-4-contacto-con-vendedor-vía-whatsapp)
      - [RF-WA-01 — Contacto automático con el vendedor](#rf-wa-01--contacto-automático-con-el-vendedor)
      - [RF-WA-02 — Contacto libre con el vendedor](#rf-wa-02--contacto-libre-con-el-vendedor)
      - [RF-WA-03 — Validación del número de WhatsApp del vendedor](#rf-wa-03--validación-del-número-de-whatsapp-del-vendedor)
    - [Módulo 5: Geolocalización y Proximidad](#módulo-5-geolocalización-y-proximidad)
      - [RF-GEO-01 — Ubicación habitual del vendedor](#rf-geo-01--ubicación-habitual-del-vendedor)
      - [RF-GEO-02 — Compartir ubicación en tiempo real](#rf-geo-02--compartir-ubicación-en-tiempo-real)
      - [RF-GEO-03 — Notificación de vendedor cercano](#rf-geo-03--notificación-de-vendedor-cercano)
      - [RF-GEO-04 — Entrega de notificación de proximidad](#rf-geo-04--entrega-de-notificación-de-proximidad)
    - [Módulo 6: Mapa del Campus](#módulo-6-mapa-del-campus)
      - [RF-MAP-01 — Mapa interactivo de la UABC](#rf-map-01--mapa-interactivo-de-la-uabc)
      - [RF-MAP-02 — Catálogo de edificios y áreas del campus](#rf-map-02--catálogo-de-edificios-y-áreas-del-campus)
    - [Módulo 7: Reseñas y Calificaciones](#módulo-7-reseñas-y-calificaciones)
      - [RF-REV-01 — Dejar una reseña](#rf-rev-01--dejar-una-reseña)
      - [RF-REV-02 — Respuesta del vendedor a reseñas](#rf-rev-02--respuesta-del-vendedor-a-reseñas)
      - [RF-REV-03 — Calificación promedio del vendedor](#rf-rev-03--calificación-promedio-del-vendedor)
      - [RF-REV-04 — Reporte de reseña inapropiada](#rf-rev-04--reporte-de-reseña-inapropiada)
    - [Módulo 8: Sistema de Reportes y Moderación](#módulo-8-sistema-de-reportes-y-moderación)
      - [RF-MOD-01 — Reporte de publicación](#rf-mod-01--reporte-de-publicación)
      - [RF-MOD-02 — Reporte de usuario](#rf-mod-02--reporte-de-usuario)
      - [RF-MOD-03 — Herramientas de administración](#rf-mod-03--herramientas-de-administración)
      - [RF-MOD-04 — Historial de acciones de moderación sobre usuarios](#rf-mod-04--historial-de-acciones-de-moderación-sobre-usuarios)
      - [RF-MOD-05 — Reporte general de la plataforma](#rf-mod-05--reporte-general-de-la-plataforma)
    - [Módulo 9: Notificaciones](#módulo-9-notificaciones)
      - [RF-NOT-01 — Notificaciones in-app](#rf-not-01--notificaciones-in-app)
      - [RF-NOT-02 — Notificaciones push web](#rf-not-02--notificaciones-push-web)
      - [RF-NOT-03 — Anuncios generales del sistema](#rf-not-03--anuncios-generales-del-sistema)
    - [Módulo 10: Favoritos](#módulo-10-favoritos)
      - [RF-FAV-01 — Guardar producto en favoritos](#rf-fav-01--guardar-producto-en-favoritos)
      - [RF-FAV-02 — Eliminar producto de favoritos](#rf-fav-02--eliminar-producto-de-favoritos)
      - [RF-FAV-03 — Listar favoritos del usuario](#rf-fav-03--listar-favoritos-del-usuario)
    - [Módulo 11: Campus](#módulo-11-campus)
      - [RF-CAMPUS-01 — Gestión del catálogo de campus](#rf-campus-01--gestión-del-catálogo-de-campus)
      - [RF-CAMPUS-02 — Selector de campus en panel de filtros](#rf-campus-02--selector-de-campus-en-panel-de-filtros)
  - [6. Requisitos No Funcionales](#6-requisitos-no-funcionales)
    - [6.1 Rendimiento](#61-rendimiento)
    - [6.2 Seguridad](#62-seguridad)
    - [6.3 Disponibilidad y Confiabilidad](#63-disponibilidad-y-confiabilidad)
    - [6.4 Usabilidad y Accesibilidad](#64-usabilidad-y-accesibilidad)
    - [6.5 Mantenibilidad](#65-mantenibilidad)
    - [6.6 Escalabilidad](#66-escalabilidad)
  - [7. Especificación de Interfaz de Usuario (UI)](#7-especificación-de-interfaz-de-usuario-ui)
    - [7.1 Principios de Diseño](#71-principios-de-diseño)
    - [7.2 Navegación Global](#72-navegación-global)
      - [Estructura de navegación](#estructura-de-navegación)
      - [Móvil (\< 1024 px)](#móvil--1024-px)
      - [Header superior (móvil)](#header-superior-móvil)
      - [Desktop (≥ 1024 px)](#desktop--1024-px)
    - [7.3 Inventario de Páginas y Rutas](#73-inventario-de-páginas-y-rutas)
    - [7.4 Descripción Detallada de Páginas](#74-descripción-detallada-de-páginas)
      - [P-01 — Catálogo (`/`)](#p-01--catálogo-)
      - [P-02 — Detalle de Publicación (`/producto/:id`)](#p-02--detalle-de-publicación-productoid)
      - [P-03 — Perfil de Usuario (`/perfil/:id`)](#p-03--perfil-de-usuario-perfilid)
      - [P-04 — Mapa del Campus (`/mapa`)](#p-04--mapa-del-campus-mapa)
      - [P-05 — Autenticación (`/auth`)](#p-05--autenticación-auth)
      - [P-06 — Onboarding (`/onboarding`)](#p-06--onboarding-onboarding)
      - [P-07 — Crear Publicación (`/publicar`)](#p-07--crear-publicación-publicar)
      - [P-08 — Editar Publicación (`/publicar/:id/editar`)](#p-08--editar-publicación-publicarideditar)
      - [P-09 — Favoritos (`/favoritos`)](#p-09--favoritos-favoritos)
      - [P-10 — Notificaciones (`/notificaciones`)](#p-10--notificaciones-notificaciones)
      - [P-11 — Configuración de cuenta (`/configuracion`)](#p-11--configuración-de-cuenta-configuracion)
      - [P-12 — Términos de Uso (`/terminos`)](#p-12--términos-de-uso-terminos)
      - [P-13 — Aviso de Privacidad (`/privacidad`)](#p-13--aviso-de-privacidad-privacidad)
      - [P-14 — Búsqueda (`/buscar`)](#p-14--búsqueda-buscar)
      - [P-15 — Reseñas del Vendedor (`/perfil/:id/resenas`)](#p-15--reseñas-del-vendedor-perfilidresenas)
      - [P-16 — Historial de Moderación (`/configuracion/moderacion`)](#p-16--historial-de-moderación-configuracionmoderacion)
    - [7.5 Estados Transversales de la UI](#75-estados-transversales-de-la-ui)
  - [8. Restricciones y Limitaciones](#8-restricciones-y-limitaciones)
    - [8.1 Técnicas](#81-técnicas)
    - [8.2 Legales y de Privacidad](#82-legales-y-de-privacidad)
    - [8.3 De Negocio](#83-de-negocio)
  - [9. Criterios de Aceptación](#9-criterios-de-aceptación)
  - [10. Glosario](#10-glosario)

---

## 1. Introducción

### 1.1 Propósito del Documento

Este documento define los requisitos de software para **Cima Market**, una plataforma web orientada a la comunidad estudiantil de la Universidad Autónoma de Baja California (UABC). El presente SRS sirve como referencia técnica y funcional para el equipo de desarrollo, diseñadores, y cualquier parte interesada en el ciclo de vida del proyecto.

### 1.2 Alcance del Sistema

Cima Market es una plataforma web progresiva (PWA) que permite a los estudiantes de la UABC publicar, promover y adquirir productos dentro del ecosistema universitario. El sistema opera en los dos campus de la institución en Ensenada: **UABC Sauzal** y **UABC Valle Dorado**, cada uno con su propia comunidad de vendedores y compradores. El sistema digitaliza y formaliza el flujo de comercio informal que actualmente ocurre a través de grupos de WhatsApp, ofreciendo una experiencia estructurada, segura y rastreable para vendedores y compradores.

El sistema **no** procesará pagos en línea en su versión inicial. La transacción económica ocurre fuera de la plataforma (en persona o por medios externos). El sistema actúa como un canal de descubrimiento y contacto.

### 1.3 Contexto y Problemática

Existe una comunidad activa de estudiantes-vendedores en la UABC que comercializan productos como snacks caseros, comida preparada, accesorios, artículos electrónicos de segunda mano y merchandise personalizado. Esta actividad se coordina actualmente mediante grupos de WhatsApp con hasta **1,000 participantes**, lo que genera:

- Saturación del canal de comunicación.
- Dificultad para descubrir productos relevantes.
- Falta de historial de reputación de los vendedores.
- Imposibilidad de filtrar por categoría, ubicación o precio.
- Nula trazabilidad de transacciones o acuerdos.

Cima Market resuelve estas fricciones mediante una plataforma centralizada, organizada y verificada institucionalmente.

### 1.4 Acrónimos y Abreviaturas

| Término | Definición                              |
| ------- | --------------------------------------- |
| SRS     | Software Requirements Specification     |
| UABC    | Universidad Autónoma de Baja California |
| PWA     | Progressive Web Application             |
| API     | Application Programming Interface       |
| JWT     | JSON Web Token                          |
| CRUD    | Create, Read, Update, Delete            |
| MVP     | Minimum Viable Product                  |

### 1.5 Referencias

| Documento / Estándar                                                                          | Relación                                                                                                             |
| --------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| IEEE Std 830-1998: Recommended Practice for Software Requirements Specifications              | Estándar que gobierna la estructura de este documento                                                                |
| Ley Federal de Protección de Datos Personales en Posesión de los Particulares (LFPDPPP, 2010) | Marco legal obligatorio que condiciona los requisitos de privacidad (§6.2, §8.2, §7.4 P-13, RF-AUTH-09)              |
| Web Content Accessibility Guidelines (WCAG) 2.1                                               | Estándar de accesibilidad referenciado en §6.4                                                                       |
| SDD — Cima Market v1.0.0                                                                      | Documento de diseño técnico que implementa este SRS. Las referencias cruzadas hacia el SDD usan el prefijo `→ SDD §` |

---

## 2. Descripción General del Sistema

### 2.1 Perspectiva del Producto

Cima Market es un sistema independiente que se integra con servicios externos de forma no intrusiva:

- **WhatsApp**: redireccionamiento a través de URLs profundas para contacto entre usuarios. No se requiere integración de API de WhatsApp Business en el MVP.
- **Cuenta institucional UABC**: autenticación mediante Google OAuth con restricción al dominio `@uabc.edu.mx`. Google verifica la pertenencia institucional del usuario como parte del flujo estándar de OAuth. El sistema verifica adicionalmente el dominio del email recibido como segunda línea de validación. La protección contra fuerza bruta en el proceso de autenticación queda delegada a Google OAuth; el sistema no implementa lógica propia de bloqueo de intentos.
- **Geolocalización del navegador**: API nativa del navegador para funciones de proximidad.

### 2.2 Funciones Principales del Producto

| #    | Función                                                                    |
| ---- | -------------------------------------------------------------------------- |
| F-01 | Registro e inicio de sesión con cuenta institucional UABC                  |
| F-02 | Publicación de productos con fotos, descripción, precio, y categoría       |
| F-03 | Catálogo de productos con búsqueda y filtros avanzados                     |
| F-04 | Contacto con vendedor vía WhatsApp (mensaje automático y personalizado)    |
| F-05 | Geolocalización del vendedor y notificaciones de proximidad                |
| F-06 | Sistema de reseñas y calificaciones                                        |
| F-07 | Mapa interactivo de la universidad con ubicación de edificios y vendedores |
| F-08 | Gestión del perfil de vendedor (tienda)                                    |
| F-09 | Sistema de reportes de publicaciones o usuarios                            |
| F-10 | Herramientas de administración y moderación de contenido                   |

### 2.3 Características de los Usuarios

| Tipo de Usuario          | Descripción                                                                                                                                                                           |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Estudiante Comprador** | Usuario autenticado que navega, busca y contacta vendedores.                                                                                                                          |
| **Estudiante Vendedor**  | Usuario autenticado que publica y gestiona sus productos. Un mismo usuario puede ser ambos.                                                                                           |
| **Administrador**        | Usuario con privilegios elevados para moderar contenido, gestionar reportes y administrar la plataforma. En el MVP, el rol de administrador corresponde al desarrollador del sistema. |
| **Visitante**            | Usuario no autenticado. Puede explorar el catálogo en modo lectura, pero no puede contactar vendedores ni publicar.                                                                   |

### 2.4 Restricciones Generales

El sistema opera exclusivamente dentro del contexto de la comunidad UABC, no procesa pagos, y debe cumplir con la legislación mexicana de protección de datos personales. Las restricciones técnicas, legales y de negocio se detallan en §8.

---

## 3. Stakeholders y Usuarios

| Stakeholder                  | Interés Principal                                            |
| ---------------------------- | ------------------------------------------------------------ |
| Estudiantes vendedores       | Visibilidad de sus productos, contacto fácil con compradores |
| Estudiantes compradores      | Descubrimiento rápido y confiable de productos               |
| Administración universitaria | Formalización del comercio estudiantil, imagen institucional |
| Equipo de desarrollo         | Claridad de requisitos para implementación                   |

---

## 4. Suposiciones y Dependencias

### 4.1 Suposiciones

- Los estudiantes cuentan con un correo institucional activo `@uabc.edu.mx`.
- Los usuarios disponen de un smartphone con WhatsApp instalado para la funcionalidad de contacto.
- Se cuenta con acceso a internet en el campus universitario.

### 4.2 Dependencias Externas

| Dependencia                                   | Proveedor                       | Criticidad |
| --------------------------------------------- | ------------------------------- | ---------- |
| Base de datos PostgreSQL                      | Neon (serverless)               | Alta       |
| Hosting y despliegue                          | Vercel                          | Alta       |
| Almacenamiento de imágenes                    | Cloudinary                      | Alta       |
| Autenticación institucional                   | Google OAuth 2.0 (Google Cloud) | Alta       |
| Geolocalización                               | API nativa del navegador        | Media      |
| Integración WhatsApp                          | URL scheme `wa.me`              | Media      |
| Notificaciones push                           | Web Push API / service workers  | Baja       |
| Limpieza periódica de tokens y notificaciones | Vercel Cron Jobs                | Media      |

---

## 5. Requisitos Funcionales

> **Convención de identificadores:** `RF-[módulo]-[número]`
> Prioridad: **Alta** (MVP) · **Media** · **Baja**

---

### Módulo 1: Autenticación y Gestión de Cuentas

> **Principio de diseño del módulo:** La autenticación debe ser un proceso transparente y de baja fricción. El sistema nunca debe bloquear la exploración; solo solicita identificación en el momento en que una acción específica lo requiere.

---

#### RF-AUTH-01 — Acceso público sin autenticación
**Prioridad:** Alta

El catálogo de productos, los perfiles de vendedores y el detalle de cada publicación serán accesibles públicamente sin necesidad de iniciar sesión. El sistema **no** mostrará una pantalla de login al entrar a la plataforma por primera vez.

Los visitantes no autenticados podrán:
- Navegar el catálogo completo con todos sus filtros y buscador.
- Ver el detalle de cualquier publicación.
- Ver el perfil público de cualquier vendedor, incluyendo sus reseñas.
- Ver el mapa del campus.

Los visitantes **no** podrán:
- Contactar a un vendedor por WhatsApp.
- Dejar reseñas.
- Publicar productos.
- Ver y recibir notificaciones.
- Acceder a funciones de perfil o configuración.

---

#### RF-AUTH-02 — Autenticación diferida
**Prioridad:** Alta

La autenticación se solicita únicamente cuando el usuario intenta realizar una acción que la requiere. El sistema clasifica toda ruta o acción protegida en una de tres categorías, cada una con un comportamiento distinto. Esta sección es la única fuente de verdad sobre el comportamiento de autenticación diferida.

| #   | Categoría                       | Criterio de clasificación                                                                                    | Comportamiento del sistema                                                                                                                                                                                                                                                                         |
| --- | ------------------------------- | ------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Destinos de navegación primaria | Rutas alcanzables directamente desde la navegación principal (navbar, header, etc.)                          | El sistema renderiza la pantalla en un estado alternativo de no-autenticado, sin redirigir al usuario. Al completar el flujo de autenticación, la pantalla se actualiza con su contenido real. → Especificación visual del estado alternativo: §7.5.                                               |
| 2   | Acciones puntuales              | El usuario activa una acción específica sobre contenido que ya está viendo, sin navegar a ninguna ruta nueva | El sistema captura la intención, presenta el flujo de autenticación, y completa la acción automáticamente al finalizar, sin que el usuario necesite repetirla. → Especificación visual: §7.5.                                                                                                      |
| 3   | Cualquier otra ruta autenticada | Toda ruta que requiere sesión activa y no está clasificada en las categorías 1 o 2                           | Si el usuario llega sin sesión activa por cualquier medio (URL manual, historial del navegador, enlace externo), el sistema redirige a la pantalla de autenticación (P-05). Al completar el flujo exitosamente, el usuario es dirigido directamente a la ruta que intentaba acceder originalmente. |

**Categoría 1 — Rutas incluidas:**
- `/favoritos` 
- `/perfil/:id` (propio) 
- `/notificaciones` 
- `/mapa`

**Categoría 2 — Acciones incluidas:**

| Acción del usuario                                    | Resultado al completar la autenticación              |
| ----------------------------------------------------- | ---------------------------------------------------- |
| Iniciar contacto con el vendedor (RF-WA-01, RF-WA-02) | Completa la acción de contacto y redirige a WhatsApp |
| Crear una reseña (RF-REV-01)                          | Abre el formulario de reseña                         |
| Guardar una publicación en favoritos (RF-FAV-01)      | Guarda el producto en favoritos                      |

**Categoría 3 — Ejemplos de rutas incluidas:** `/publicar` (P-07), `/publicar/:id/editar` (P-08), `/configuracion` (P-11), `/configuracion/moderacion` (P-16). Esta lista es ilustrativa, no exhaustiva — el criterio de clasificación (cualquier ruta autenticada no listada en la categoría 1) es la fuente de verdad.

**Regla de redirección post-login (aplica a las tres categorías):** Si el usuario ya tenía una sesión activa (refresh token válido), esta se restaura automáticamente sin mostrar la pantalla de login. Si es un usuario nuevo o el onboarding no está completado, se muestra el onboarding antes de completar la acción original.

---

#### RF-AUTH-03 — Registro e inicio de sesión
**Prioridad:** Alta

El sistema utiliza Google OAuth 2.0 como único mecanismo de autenticación, restringido al dominio institucional `@uabc.edu.mx`. El flujo cubre tanto el registro de nuevos usuarios como el inicio de sesión de usuarios existentes en una única operación.

**Razón de diseño:** La UABC usa Google Workspace para el correo institucional, lo que permite delegar la verificación de identidad a Google sin infraestructura propia de envío de correos ni lógica de códigos de verificación.

**Reglas de negocio:**

1. El sistema acepta únicamente cuentas Google del dominio exacto `uabc.edu.mx`. El parámetro `hd=uabc.edu.mx` en la solicitud OAuth restringe el selector de cuentas de Google al dominio institucional. El servidor verifica adicionalmente el dominio del email recibido como segunda línea de validación.
2. El sistema rechaza cualquier cuenta de dominio distinto a `uabc.edu.mx`, incluso si Google la autentica correctamente.
3. El usuario debe aceptar los Términos de Uso y el Aviso de Privacidad antes de poder iniciar el flujo de autenticación.
4. El sistema no distingue entre usuario nuevo y existente hasta después de completar el flujo de OAuth — Google retorna el email verificado y el sistema determina si ya existe una cuenta asociada.

**Comportamiento post-autenticación:**

Una vez que Google retorna el email verificado, el servidor determina el estado de la cuenta:

- Si el correo **no existía** → crea la cuenta, emite las credenciales de sesión y redirige al onboarding (RF-AUTH-04).
- Si el correo **ya existía** y el **onboarding no fue completado** → emite las credenciales de sesión y redirige al onboarding.
- Si el correo **ya existía** y el **onboarding fue completado** → emite las credenciales de sesión y redirige según RF-AUTH-02.

**Estado inicial de la cuenta al crearse:** el sistema crea la cuenta con el correo institucional verificado por Google. Los campos de nombre, campus y número de WhatsApp quedan pendientes hasta que el usuario completa el onboarding.

---

#### RF-AUTH-04 — Onboarding
**Prioridad:** Alta

El onboarding se presenta **únicamente la primera vez** que un usuario accede al sistema, inmediatamente después de la primera autenticación exitosa. Se presenta en una única pantalla.

**Campos y reglas de validación:**

| Campo              | Obligatorio          | Restricciones                                                                                                                                                                                                                                                                                                                                |
| ------------------ | -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Nombre de display  | Sí                   | Mín. 2 chars, máx. 50 chars. Se mostrará públicamente en el catálogo y perfiles. Si no se configura una foto posteriormente, el sistema genera un avatar automático con las iniciales de este nombre.                                                                                                                                        |
| Campus principal   | Sí                   | "UABC Sauzal" o "UABC Valle Dorado". Determina el campus por defecto en el catálogo, el mapa y el formulario de publicaciones. No restringe al usuario — puede ver y publicar en cualquier campus en cualquier momento.                                                                                                                      |
| Intención de uso   | Sí                   | "Solo quiero comprar / explorar" o "También quiero vender". Si el usuario selecciona la segunda opción, el campo de número de WhatsApp se convierte en obligatorio.                                                                                                                                                                          |
| Número de WhatsApp | Solo si elige vender | Formato E.164. Se valida el formato antes de guardar. El número se almacena una vez validado el formato; no se realiza verificación de posesión del número en el MVP ni se verifica que corresponda a una cuenta de WhatsApp activa. Si el número no tiene formato E.164 válido, el servidor rechaza el guardado con un error de validación. |

El sistema no permite completar el onboarding hasta que todos los campos obligatorios sean válidos.

**Carácter obligatorio:** El onboarding no puede ser omitido ni saltado. La SPA implementa un route guard global que verifica el estado del onboarding al cargar cualquier ruta. Si el onboarding no está completado, el usuario es redirigido a `/onboarding` independientemente de la URL solicitada. Ninguna pantalla de la aplicación, excepto `/onboarding`, es accesible para un usuario que haya iniciado sesión pero no haya completado el onboarding.

**Validación server-side del onboarding:** El servidor valida adicionalmente que el onboarding esté completado antes de procesar cualquier endpoint autenticado, garantizando que el route guard del cliente no sea el único mecanismo de protección. → SDD §3.2.3 (middleware `requireOnboarding`), §3.3.2 (Capa 2).

**Nota:** Los usuarios que elijan "Solo comprar" en el onboarding podrán activar el rol vendedor posteriormente desde su perfil en cualquier momento.

---

#### RF-AUTH-05 — Sesión persistente y renovación de tokens
**Prioridad:** Alta

El sistema implementa un esquema de autenticación basado en tokens de doble capa:

| Token         | Duración   | Propósito                                     |
| ------------- | ---------- | --------------------------------------------- |
| Access Token  | 15 minutos | Autoriza peticiones a la API                  |
| Refresh Token | 30 días    | Renueva el access token de forma transparente |

→ Mecanismo de almacenamiento e implementación: SDD §3.3.1, §4.1.

**Comportamiento:**
- **Renovación silenciosa al cargar la aplicación:** Al iniciar la aplicación, si la sesión activa en el dispositivo es válida, el sistema la restaura de forma transparente antes de renderizar cualquier vista autenticada. El usuario nunca percibe la expiración ni necesita volver a ingresar su correo.
- El access token se renueva automáticamente al expirar durante la sesión activa, sin que el usuario lo perciba.
- La sesión de **30 días** aplica de manera uniforme en todos los dispositivos (móvil y desktop).
- Si el refresh token expira o es revocado, el usuario debe autenticarse nuevamente.
- Un mismo usuario puede tener sesiones activas en múltiples dispositivos simultáneamente.

---

#### RF-AUTH-06 — Activación del rol vendedor
**Prioridad:** Alta

Un usuario podrá activar el rol vendedor en dos momentos: durante el onboarding (RF-AUTH-04), seleccionando la opción 'También quiero vender' e ingresando su número de WhatsApp, o posteriormente desde la sección de configuración de su perfil en cualquier momento. No se realiza verificación de posesión del número (sin SMS ni OTP); el número se guarda tras validar que el formato E.164 sea correcto.

Una vez activado el rol vendedor, el usuario tendrá acceso a:
- Formulario de creación de publicaciones.
- Gestión de sus publicaciones desde su perfil (P-03, modo propietario).
- Modo "Estoy vendiendo ahora" (geolocalización en tiempo real).
- Recepción de reseñas en su perfil.

**Desactivación del rol vendedor:** Si el usuario desactiva el rol vendedor desde su perfil, todas sus publicaciones en estado `active` pasarán automáticamente a estado `paused`. Las publicaciones pausadas no se eliminan y pueden reactivarse si el usuario vuelve a habilitar el rol vendedor.

**Comportamiento del guard de rol vendedor en el cliente:** Si el usuario está autenticado pero no tiene el rol vendedor activo al intentar acceder a `/publicar` (P-07), el sistema redirige a `/configuracion` (P-11).

El servidor aplica controles de autorización distintos según el tipo de operación: la creación de publicaciones requiere que el usuario tenga el rol vendedor activo; la gestión de publicaciones existentes (editar, eliminar) no lo requiere — un usuario puede gestionar su contenido aunque haya desactivado el rol vendedor. → Implementación de los controles de autorización en el servidor: SDD §4.

El rol vendedor no reemplaza al rol comprador; ambos coexisten en la misma cuenta.

---

#### RF-AUTH-07 — Gestión de perfil de usuario
**Prioridad:** Alta

El sistema permitirá al usuario autenticado consultar y editar los datos de su perfil, y mostrará públicamente en modo lectura la reputación e inventario activo del usuario cuando corresponda.

El usuario autenticado podrá editar los siguientes campos de su perfil:

| Campo                              | Modificable | Notas                                                                                                                                |
| ---------------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Nombre de display                  | Sí          | Mismas restricciones que en el onboarding (RF-AUTH-04).                                                                              |
| Foto de perfil                     | Sí          | Reemplaza la anterior. Se gestiona a través de un proceso de carga independiente. → SDD §4.2.                                        |
| Campus principal                   | Sí          | UABC Sauzal o UABC Valle Dorado. Cambia el contexto por defecto del catálogo y el mapa.                                              |
| Ubicación habitual (edificio/área) | Sí          | Solo editable si el rol vendedor está activo. Debe pertenecer al campus principal. Se resetea a vacío si el campus principal cambia. |
| Número de WhatsApp                 | Sí          | Formato E.164. Obligatorio si el rol vendedor está activo.                                                                           |
| Correo institucional               | No          | Campo de solo lectura; es el identificador de la cuenta.                                                                             |
| Rol vendedor activo                | Sí          | Puede desactivarse; las publicaciones existentes se pausan automáticamente.                                                          |

**Comportamiento al cambiar el campus principal:** Si el usuario cambia su campus principal desde P-11, la ubicación habitual configurada se resetea automáticamente en la misma operación, ya que pertenece al campus anterior. El usuario deberá configurar una nueva ubicación habitual para el campus recién seleccionado si lo desea.

Adicionalmente, el perfil público mostrará en modo lectura:

- **Calificación promedio y reseñas recibidas** — visible si el usuario tiene al menos una reseña recibida, **independientemente de si el rol vendedor está activo en este momento**. La reputación construida como vendedor se preserva aunque el usuario pause temporalmente su actividad de venta; desactivar el rol no oculta ni borra el historial de reseñas.

- **Publicaciones activas** — Al desactivar el rol vendedor, las publicaciones pasan automáticamente a `paused` (RF-AUTH-06), por lo que esta sección deja de mostrarse de forma natural, sin necesidad de una regla adicional.

---

#### RF-AUTH-08 — Cierre de sesión y revocación de tokens
**Prioridad:** Alta

El sistema permitirá el cierre de sesión manual desde cualquier pantalla (accesible desde el menú de perfil). Al cerrar sesión:
- El refresh token del dispositivo actual se invalida en el servidor.
- Las credenciales en memoria del cliente se descartan.
- El usuario es redirigido al catálogo público.

El cierre de sesión afecta únicamente al dispositivo/navegador desde el que se ejecuta la acción.

---

#### RF-AUTH-09 — Eliminación de cuenta
**Prioridad:** Alta

En cumplimiento con el derecho de cancelación establecido en el Artículo 16 de la **Ley Federal de Protección de Datos Personales en Posesión de los Particulares (LFPDPPP)**, el usuario autenticado podrá solicitar la eliminación permanente de su cuenta y datos asociados desde la sección "Privacidad y soporte" de P-11 (`/configuracion`).

**Flujo de eliminación:**
1. El usuario solicita la eliminación permanente de su cuenta desde P-11.
2. El sistema presenta las consecuencias de la acción y requiere confirmación explícita mediante un diálogo de confirmación.
3. El sistema ejecuta la eliminación y anonimización según las reglas descritas abajo.
4. El usuario es redirigido al catálogo público como visitante no autenticado.

**Reglas de eliminación y anonimización:**

| Entidad                             | Acción                                                                                                                                                                                                                                                      |
| ----------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `users`                             | Anonimización: email → valor aleatorio no recuperable, nombre → `"Usuario eliminado"`, foto de perfil → eliminada (el archivo se elimina del servicio de almacenamiento antes de anonimizar), número de WhatsApp → eliminado, cuenta marcada como inactiva. |
| `products`                          | Soft delete en todas las publicaciones del usuario.                                                                                                                                                                                                         |
| `product_images`                    | Eliminación física en el servicio de almacenamiento y del registro en base de datos.                                                                                                                                                                        |
| `reviews` (escritas por el usuario) | El vínculo con el usuario anonimizado se preserva para mantener la integridad del historial; el texto de la reseña se reemplaza por `"[Reseña eliminada]"`. La anonimización del usuario es suficiente para desligar la reseña de la identidad original.    |
| `reviews` (recibidas como vendedor) | Se conservan con el rating para no afectar integridad del historial de otros usuarios.                                                                                                                                                                      |
| `saved_products`                    | Eliminación física de todos los registros del usuario.                                                                                                                                                                                                      |
| Tokens de sesión                    | Eliminación física de todos los tokens activos.                                                                                                                                                                                                             |
| `contact_events`                    | Se conservan para integridad del historial de moderación.                                                                                                                                                                                                   |
| `reports` enviados                  | Se conservan para integridad del historial de moderación.                                                                                                                                                                                                   |
| `notifications`                     | Eliminación física de todos los registros del usuario.                                                                                                                                                                                                      |
| Ubicación en tiempo real            | Eliminación física del registro del vendedor si existe, para que no quede activo en el mapa.                                                                                                                                                                |

**Nota:** La anonimización en lugar del borrado físico del registro de usuario preserva la integridad referencial de las tablas que no se eliminan (como el historial de contactos y reportes) sin exponer datos personales del usuario.

**Re-registro posterior:** Una vez completada la eliminación, el correo institucional del usuario queda disponible nuevamente en el sistema. El usuario podrá crear una nueva cuenta con el mismo correo `@uabc.edu.mx` en cualquier momento futuro, pasando por el flujo de autenticación y onboarding como si fuera un usuario nuevo. La nueva cuenta no tendrá ninguna relación ni historial vinculado con la cuenta eliminada.

---

### Módulo 2: Gestión de Publicaciones

#### RF-PUB-01 — Crear publicación
**Prioridad:** Alta

Un usuario con rol vendedor podrá crear una publicación que incluya:

| Campo                  | Obligatorio | Restricciones / Comportamiento                                                                                                                                                                                                                                                |
| ---------------------- | ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Título                 | Sí          | Máx. 100 chars                                                                                                                                                                                                                                                                |
| Descripción            | Sí          | Texto plano, máx. 600 chars                                                                                                                                                                                                                                                   |
| Precio                 | Sí          | Numérico (MXN)                                                                                                                                                                                                                                                                |
| Categoría              | Sí          | Referencia a tabla `categories`                                                                                                                                                                                                                                               |
| Campus                 | Sí          | Referencia a tabla `campuses`. Valor por defecto: campus principal del vendedor.                                                                                                                                                                                              |
| Ubicación habitual     | No          | Referencia a `campus_buildings`. Pre-llenado automáticamente con la ubicación habitual del vendedor si la publicación se crea en el mismo campus que su campus principal; vacío en cualquier otro caso. El vendedor puede aceptar el valor pre-llenado, cambiarlo o vaciarlo. |
| Imágenes               | Sí (mín. 1) | JPG, PNG o HEIC, máx. 5 MB c/u. Límite de cantidad según plan del vendedor (→ RF-PUB-04). Los archivos HEIC son convertidos automáticamente por el servicio de almacenamiento.                                                                                                |
| Días/horarios de venta | No          | Días de la semana y rango horario. → SDD §5.2 (`products`).                                                                                                                                                                                                                   |

**Valor por defecto del campo Campus:** el campus principal registrado en el perfil del vendedor. El vendedor puede cambiarlo.

**Valor por defecto del campo Ubicación habitual:** Determinado por la relación entre el campus de la publicación y el campus principal del vendedor. Si coinciden, el servidor pre-llena el campo con la ubicación habitual del vendedor (que puede estar vacía si el vendedor no la ha configurado). Si el vendedor cambió el campus de la publicación a uno distinto de su campus principal, el campo de ubicación no se pre-llena y queda vacío hasta que el vendedor lo seleccione manualmente. Este comportamiento evita que se le atribuya a una publicación ocasional en otro campus la ubicación habitual configurada para el campus principal.

---

#### RF-PUB-02 — Editar y eliminar publicación
**Prioridad:** Alta

El vendedor podrá editar cualquier campo de su publicación o eliminarla en cualquier momento. Las publicaciones eliminadas se conservan en el sistema para efectos de moderación, pero dejan de ser visibles en el catálogo y para otros usuarios.

---

#### RF-PUB-03 — Pausar y reactivar publicación
**Prioridad:** Alta

El vendedor podrá pausar temporalmente su publicación sin eliminarla. Las publicaciones pausadas no aparecen en el catálogo público pero permanecen en el panel del vendedor.

**Regla de pausa automática por desactivación del rol:** Cuando un usuario desactiva su rol vendedor (RF-AUTH-06) o es suspendido por un administrador, todas sus publicaciones en estado `active` pasan automáticamente a estado `paused`. Esta transición ocurre de forma atómica junto con la desactivación del rol, garantizando que no queden publicaciones activas sin un vendedor activo detrás. Las publicaciones pausadas por esta causa pueden reactivarse si el rol vendedor se vuelve a habilitar.

---

#### RF-PUB-04 — Límite de publicaciones
**Prioridad:** Media

Para proteger los recursos de almacenamiento y evitar el spam, el sistema implementa un límite sobre el catálogo total del vendedor, determinado por su plan.

**Límite establecido (Plan Gratuito):** Máximo 10 publicaciones totales (suma de publicaciones con estado `active` y `paused`). Las publicaciones eliminadas no cuentan hacia este límite.

**Límite de imágenes por publicación (Plan Gratuito):** Máximo 4 imágenes por publicación. Si el vendedor intenta subir más imágenes de las permitidas, el sistema rechaza las imágenes excedentes e indica el máximo permitido.

**Comportamiento del sistema al crear una publicación:**
1. El sistema verifica el total de publicaciones activas y pausadas del vendedor (excluyendo las eliminadas).
2. Si el total alcanza o supera el límite del plan, el sistema rechaza la creación con un mensaje descriptivo indicando que debe eliminar una publicación existente antes de crear una nueva.

→ Implementación del límite y su configuración por plan: SDD §4.3.

**Nota de escalabilidad:** El sistema de límites está preparado para soportar planes adicionales en el futuro, de modo que la incorporación de monetización no requerirá cambios en la lógica de validación existente.

---

#### RF-PUB-05 — Categorías de productos
**Prioridad:** Alta

El sistema gestionará un catálogo fijo de categorías que clasifica las publicaciones y permite a los compradores filtrar el contenido por tipo de producto.

El sistema soportará las siguientes categorías iniciales:

- Comida y Snacks
- Bebidas
- Electrónicos
- Accesorios (llaveros, stickers, pins, etc.)
- Ropa
- Material Académico (libros, apuntes, etc.)
- Otros

Las categorías son administrables por el equipo operador a través de un panel de administración (→ SDD §4.13). Los datos iniciales del catálogo se cargan antes del lanzamiento del MVP.

---

#### RF-PUB-06 — Moderación automática de imágenes
**Prioridad:** Media

Las imágenes subidas son evaluadas automáticamente por el servicio de moderación de contenido antes de completar la publicación.

**Flujo de moderación:**

1. Las imágenes son enviadas para evaluación únicamente cuando el usuario confirma la publicación.
2. Si alguna imagen es rechazada por contenido inapropiado:
   - La publicación completa se cancela.
   - Todos los archivos del lote que hayan sido procesados se eliminan del servicio de almacenamiento.
   - El sistema informa al usuario qué imagen fue rechazada.
   - No queda ningún archivo almacenado.
3. Si todas las imágenes son aprobadas, el sistema procede a crear la publicación.
4. Si la creación de la publicación falla por cualquier causa tras la aprobación de las imágenes, el sistema elimina todos los archivos ya procesados antes de retornar el error. El usuario puede reintentar sin necesidad de volver a seleccionar sus imágenes.

**Principio de diseño:** Las imágenes no se procesan hasta que el usuario confirma su intención de publicar. Esto minimiza la posibilidad de que existan archivos almacenados sin una publicación asociada — cubre el escenario más frecuente: el abandono del formulario antes de confirmar.

→ Implementación del flujo de subida, moderación y rollback: SDD §4.3.

---

### Módulo 3: Catálogo y Búsqueda

#### RF-CAT-01 — Catálogo principal
**Prioridad:** Alta

La página principal mostrará un catálogo paginado de publicaciones activas, ordenadas por defecto por fecha de publicación descendente.

---

#### RF-CAT-02 — Búsqueda por texto
**Prioridad:** Alta

El sistema ofrecerá un campo de búsqueda que filtre publicaciones por coincidencia en título y descripción mediante búsqueda full-text.

---

#### RF-CAT-03 — Filtros avanzados
**Prioridad:** Alta

El sistema permitirá al usuario acotar el catálogo de publicaciones mediante un conjunto de filtros combinables, reflejados en la URL para permitir compartir búsquedas contextualizadas.

El catálogo podrá filtrarse por:
- Campus (primera sección del panel, ver reglas específicas abajo)
- Categoría
- Rango de precio (mínimo / máximo)
- Calificación mínima del vendedor
- Ver todo (remueve los filtros de categoría)

Los filtros son combinables y se reflejan en la URL para permitir compartir búsquedas.

**Reglas específicas del filtro Campus:**
- El comportamiento general del selector de campus (siempre un valor seleccionado, persistencia local entre sesiones, no se resetea con "Limpiar todo") está definido en RF-CAMPUS-02 y aplica sin excepción a este panel de filtros.
- Cambiar el campus desde el panel de filtros actualiza la preferencia local pero **no** actualiza el campus principal del perfil. El campus del perfil solo se modifica desde P-11 (`/configuracion`).

**Jerarquía de precedencia para determinar el campus activo:**

| Prioridad | Fuente                                | Condición                                               |
| --------- | ------------------------------------- | ------------------------------------------------------- |
| 1 (mayor) | Query param en URL (`?campus=sauzal`) | Si está presente en la URL al cargar la pantalla        |
| 2         | Preferencia guardada en el navegador  | Si existe un valor de una sesión previa                 |
| 3         | Campus principal del perfil           | Si el usuario está autenticado y completó el onboarding |
| 4 (menor) | Default hardcodeado: UABC Sauzal      | Si ninguna fuente anterior está disponible              |

---

#### RF-CAT-04 — Ordenamiento
**Prioridad:** Media

El sistema permitirá al usuario cambiar el criterio de ordenamiento del catálogo, incluyendo ordenamiento por proximidad geográfica cuando el usuario otorgue permiso de geolocalización.

El catálogo podrá ordenarse por:
- Más reciente (default)
- Precio: menor a mayor / mayor a menor
- Mejor calificación
- Más cercano (requiere geolocalización activa)

**Mecanismo del filtro de Cercanía:** Al seleccionar 'Más cercano', el sistema solicita permiso de geolocalización inmediatamente. Si el usuario lo niega, el sistema revierte el criterio de ordenamiento a "Más reciente". Compara la posición del comprador contra la ubicación habitual de venta de cada publicación (no contra la ubicación en tiempo real del vendedor). Las publicaciones sin ubicación habitual de venta especificado no participan en este filtro ni en el ordenamiento por cercanía (RF-CAT-04) — no aparecen ni se excluyen explícitamente, simplemente no tienen una distancia calculable.

---

### Módulo 4: Contacto con Vendedor vía WhatsApp

#### RF-WA-01 — Contacto automático con el vendedor
**Prioridad:** Alta

Cada publicación incluirá una acción de contacto automático que, al activarse, ejecutará una solicitud autenticada al servidor. El servidor construirá el enlace de WhatsApp internamente y lo retornará al cliente para abrirlo en una nueva ventana.

**Contrato de datos del mensaje pre-generado:** El servidor construye el mensaje incluyendo obligatoriamente las siguientes variables: nombre del vendedor, título del producto y una pregunta de disponibilidad.

**Mecanismo de contacto:** El sistema valida la sesión del usuario, aplica límites de frecuencia para prevenir uso automatizado, registra el evento de contacto y construye el enlace de WhatsApp en el servidor → SDD §4.6.

**Controles de acceso al endpoint de contacto:**

| Capa | Mecanismo                                   | Propósito                                                            |
| ---- | ------------------------------------------- | -------------------------------------------------------------------- |
| 1    | Autenticación obligatoria                   | Solo cuentas `@uabc.edu.mx` verificadas pueden obtener el enlace     |
| 2    | Límite de frecuencia por usuario (ver §6.2) | Previene extracción masiva automatizada                              |
| 3    | Registro del evento de contacto             | Prerequisito para reseñas. Detecta patrones anómalos para moderación |

---

#### RF-WA-02 — Contacto libre con el vendedor
**Prioridad:** Alta

Junto a la acción de contacto automático, existirá una acción de contacto libre que abrirá directamente WhatsApp con el chat del vendedor y sin texto pre-llenado. El usuario escribe su mensaje libremente en WhatsApp. El servidor registra el evento de contacto antes de retornar el enlace, de modo que las métricas y la elegibilidad de reseña funcionan de forma idéntica a RF-WA-01.

---

#### RF-WA-03 — Validación del número de WhatsApp del vendedor
**Prioridad:** Alta

El sistema validará que el número de WhatsApp del vendedor tenga formato internacional válido (E.164) antes de generar el enlace. La validación ocurre en el momento de captura, antes de persistir el dato:

- **Onboarding (RF-AUTH-04):** el servidor rechaza el guardado con un error de validación inline si el formato no es válido.
- **Activación posterior del rol vendedor (RF-AUTH-06):** misma validación, mismo rechazo inline.
- **Edición desde P-11 (`/configuracion`):** misma validación inline antes de guardar el cambio.

---

### Módulo 5: Geolocalización y Proximidad

#### RF-GEO-01 — Ubicación habitual del vendedor
**Prioridad:** Alta

El vendedor podrá indicar en su publicación su **ubicación habitual de venta** dentro del campus, seleccionando un edificio o área del catálogo predefinido de la UABC (ver RF-MAP-02).

Esta ubicación es un dato editorial de la publicación — equivalente al precio o la categoría — e indica dónde suele vender el vendedor, no dónde está en este momento. Se muestra como texto en el detalle de la publicación (P-02) junto a los horarios. No se representa como marcador en el mapa.

---

#### RF-GEO-02 — Compartir ubicación en tiempo real
**Prioridad:** Media

El vendedor podrá activar voluntariamente el modo **"Estoy vendiendo ahora"**, que compartirá su ubicación en tiempo real (actualizada cada 60 segundos mientras la sesión esté activa en el dispositivo). El vendedor puede desactivar esta función en cualquier momento.

Al activar el modo, el vendedor puede seleccionar una publicación destacada para aparecer como producto principal en su marcador del mapa. Si no selecciona ninguna, el sistema usa su publicación activa más reciente en ese campus como fallback. El resto de sus publicaciones activas en ese campus se muestran automáticamente en la lista secundaria del marcador (→ RF-MAP-01).

**Comportamiento si el producto destacado deja de estar disponible:** Si el producto seleccionado como destacado es pausado o eliminado mientras el modo "Estoy vendiendo ahora" sigue activo, el sistema recalcula el fallback automáticamente: usa la publicación activa más reciente del vendedor en ese campus como nuevo producto destacado. Si el vendedor no tiene ninguna publicación activa en ese campus en ese momento, el marcador permanece visible en el mapa sin producto destacado, junto con un aviso de su ausencia (RF-MAP-01).

**Consideración de privacidad:** La ubicación en tiempo real es opt-in y se informa claramente al usuario antes de activarse. Esta pantalla del mapa es solo visible para usuarios autenticados de la UABC.

**Comportamiento ante inactividad sin desactivación explícita:** Si el dispositivo del vendedor deja de enviar actualizaciones (la app se cierra, pierde conexión, o pasa a segundo plano por más de 90 segundos), el registro de ubicación expira automáticamente. El vendedor deja de aparecer en el mapa y en las notificaciones de proximidad de inmediato.

Al recargar la aplicación, el cliente debe verificar el estado real del modo contra el servidor, en lugar de confiar en un estado guardado localmente, para evitar mostrar el toggle como activo cuando en realidad expiró por inactividad.



---

#### RF-GEO-03 — Notificación de vendedor cercano
**Prioridad:** Media

Cuando un comprador tiene activa la detección de ubicación, el sistema detecta si algún vendedor de su interés se encuentra dentro de un radio de 200 metros de la ubicación actual del comprador. La detección se ejecuta en cada solicitud de proximidad del comprador y sus resultados alimentan el mecanismo de notificación descrito en RF-GEO-04.

**Requisitos previos:**
- El comprador debe haber dado permiso de geolocalización al navegador.
- El vendedor debe tener activo el modo "Estoy vendiendo ahora" (RF-GEO-02).
- El comprador debe tener al menos un producto del vendedor guardado en favoritos. Esta señal indica intención de compra previa explícita.

**Flujo del servidor** — ejecutado en cada solicitud de proximidad:

1. Identificar los vendedores que el comprador tiene en favoritos.
2. De esos, filtrar cuáles tienen el modo "Estoy vendiendo ahora" activo y están dentro del umbral.
3. Responder con la lista completa de vendedores elegibles. El servidor delega en el mecanismo de RF-GEO-04 la decisión de registrar la notificación para cada uno.

---

#### RF-GEO-04 — Entrega de notificación de proximidad
**Prioridad:** Media

Una vez que la solicitud de proximidad identifica vendedores elegibles (RF-GEO-03), el sistema los comunica al usuario mediante dos canales independientes con comportamientos y controles distintos. En el MVP la notificación se enviará exclusivamente como alerta in-app (RF-NOT-01). Las notificaciones push web quedan reservadas para post-MVP (RF-NOT-02).

**Separación de canales:**

| Canal                 | Control                                       | Frecuencia máxima | Propósito                                             |
| --------------------- | --------------------------------------------- | ----------------- | ----------------------------------------------------- |
| Toast / banner in-app | Cliente (estado en memoria)                   | Cada 30 minutos   | Aviso inmediato mientras la app está abierta          |
| Notificación en P-10  | Servidor (registro con control de frecuencia) | Cada 30 minutos   | Registro persistente consultable en cualquier momento |

Ambos canales comparten el mismo intervalo de 30 minutos pero operan de forma independiente. El cliente puede mostrar un toast sin que el servidor actualice P-10, y el servidor puede actualizar P-10 sin que el cliente muestre un toast.

**Flujo del servidor** — ejecutado al responder una solicitud de proximidad:

Para cada vendedor elegible, el servidor verifica si han transcurrido 30 minutos desde el último registro en las notificaciones del comprador para ese vendedor: si es así, registra la notificación; si no, la omite. Este control de frecuencia aplica únicamente al registro de la notificación — no afecta qué vendedores aparecen en la respuesta.

**Flujo del cliente** — ejecutado al recibir cada respuesta:

El cliente mantiene en memoria un registro de cuándo mostró el último toast por cada vendedor. Al recibir la lista, para cada vendedor en ella:

- Si nunca se le mostró un toast, o el último fue hace más de 30 minutos → mostrar toast y registrar el momento actual.
- Si el último toast fue hace menos de 30 minutos → no mostrar nada.

El toast muestra el nombre del vendedor y la distancia aproximada. El usuario puede descartarlo manualmente en cualquier momento, o desaparece automáticamente a los 5 segundos si no hay interacción. Puede aparecer sobre cualquier pantalla mientras la app esté activa.

Este registro vive únicamente en memoria. Persiste mientras la pestaña del navegador siga abierta. Al cerrar la pestaña, cerrar el navegador o recargar la página, el registro se descarta y todos los vendedores pueden volver a generar un toast.


**Comportamiento resultante por escenario:**

| Escenario                                            | Toast | Registro en P-10              |
| ---------------------------------------------------- | ----- | ----------------------------- |
| Vendedor aparece por primera vez en la sesión        | ✓     | ✓ (si no hay registro previo) |
| Vendedor sigue cerca, menos de 30 min después        | ✗     | ✗                             |
| Vendedor sigue cerca, después de 30 min              | ✓     | ✓                             |
| Comprador cambia de tab y regresa (menos de 30 min)  | ✗     | ✗                             |
| Comprador apaga pantalla y regresa (menos de 30 min) | ✗     | ✗                             |
| Comprador cierra/recarga la app (menos de 30 min)    | ✓     | ✗                             |
| Comprador cierra/recarga la app (después de 30 min)  | ✓     | ✓                             |
| Vendedor sale y regresa al radio (menos de 30 min)   | ✗     | ✗                             |
| Vendedor sale y regresa al radio (después de 30 min) | ✓     | ✓                             |

Si el vendedor abandona el radio y regresa, el toast puede aparecer nuevamente solo si han transcurrido 30 minutos desde el último toast mostrado para ese vendedor, independientemente de si la app estuvo abierta o cerrada durante ese tiempo.

---

### Módulo 6: Mapa del Campus

#### RF-MAP-01 — Mapa interactivo de la UABC
**Prioridad:** Media

El sistema incluirá una vista de mapa (implementada con Leaflet.js + OpenStreetMap) que mostrará el campus seleccionado actualmente por el usuario. El mapa se centra automáticamente en las coordenadas del campus activo.

Contenido del mapa:
- Los edificios y áreas principales del campus seleccionado.
- Marcadores de los vendedores con el modo "Estoy vendiendo ahora" activo en ese campus. Cada marcador muestra el producto destacado del vendedor como información principal. Al seleccionar un marcador, el sistema presenta el producto destacado en detalle, la lista de hasta 4 productos activos adicionales del vendedor en ese campus, y una mini tarjeta del vendedor con su nombre y calificación promedio como contexto de confianza.

**Selector de campus:** El usuario puede cambiar entre los campus disponibles desde un control. Al cambiar de campus, el mapa se recentra en las coordenadas del campus seleccionado y recarga los marcadores correspondientes. La opción de mostrar más de un campus a la vez simultáneamente no se implementa — los campus están físicamente distantes.

**Acceso desde el detalle de publicación:** Un comprador que vea el indicador de vendedor activo en P-02 puede navegar directamente a P-04 con el marcador de ese vendedor ya centrado y su popup abierto, sin necesidad de localizarlo manualmente en el mapa.

---

#### RF-MAP-02 — Catálogo de edificios y áreas del campus
**Prioridad:** Media

El sistema contará con un catálogo interno de los edificios y áreas de cada campus de la UABC registrado. Este catálogo servirá como referencia para que vendedores indiquen su ubicación y para que compradores entiendan el mapa.

Cada edificio tiene una referencia obligatoria al campus al que pertenece, garantizando que los edificios de un campus nunca aparezcan en el mapa de otro campus.

Ejemplos por campus:
- **Sauzal:** Biblioteca Central, Cafetería, Explanada, Facultad de Ingeniería, Estacionamiento.
- **Valle Dorado:** Edificios académicos, servicios y áreas comunes propios de ese campus.

Los edificios son administrables por el equipo operador a través de un panel de administración (→ SDD §4.13). Los datos iniciales del catálogo se cargan antes del lanzamiento del MVP.

---

### Módulo 7: Reseñas y Calificaciones

#### RF-REV-01 — Dejar una reseña
**Prioridad:** Alta

Un comprador podrá dejar una reseña sobre un vendedor después de haber iniciado contacto con él (haber presionado el botón de WhatsApp). La reseña incluirá:
- Calificación de 1 a 5 estrellas.
- Comentario de texto opcional (máx. 500 chars).

Las reseñas son públicas y visibles en el perfil del vendedor. Para el MVP no se permitirá editar las reseñas, solo se podrán eliminar.

**Límite:** Un usuario puede dejar máximo una reseña por vendedor.

**Decisión de diseño — Elegibilidad por vendedor, no por producto:** La reseña evalúa al vendedor como persona (confiabilidad, trato, puntualidad) y no a un producto específico. Por esta razón, la elegibilidad se verifica a nivel del par (comprador y vendedor): haber contactado cualquier producto de un vendedor habilita al comprador para dejar una reseña sobre ese vendedor. Esta restricción de unicidad por par comprador-vendedor se aplica a nivel de base de datos (→ SDD §5.2 `reviews`) y en la capa de API (→ SDD §4.7).

**Eliminación de una reseña propia:** En cualquier punto donde una reseña sea visible, el usuario autenticado que sea su autor podrá eliminarla. El sistema requiere confirmación explícita antes de ejecutar la eliminación. Una vez confirmada, la reseña es eliminada permanentemente.

---

#### RF-REV-02 — Respuesta del vendedor a reseñas
**Prioridad:** Media

El vendedor podrá responder públicamente a cada reseña recibida, una sola vez por reseña. La respuesta aparece debajo de la reseña en el perfil.

La respuesta del vendedor es inmutable en el MVP una vez publicada.

---

#### RF-REV-03 — Calificación promedio del vendedor
**Prioridad:** Alta

El perfil de cada vendedor mostrará su calificación promedio (media aritmética), número total de reseñas y distribución de calificaciones (estrellas 1-5).

---

#### RF-REV-04 — Reporte de reseña inapropiada
**Prioridad:** Media

Los usuarios podrán reportar una reseña como inapropiada. Las reseñas con 3 o más reportes entrarán en revisión manual por un administrador.

**Acción del administrador:** Cuando un administrador revisa una reseña reportada y determina que viola las políticas de la plataforma, puede eliminarla mediante el endpoint de moderación correspondiente. La eliminación tiene el mismo efecto que si el autor la hubiera borrado: la reseña desaparece del perfil del vendedor y la calificación promedio se recalcula inmediatamente.

**Notificación al autor**: cuando un administrador elimina una reseña por violar las políticas de la plataforma, el autor de la reseña recibe una notificación in-app con el motivo, bajo el mismo mecanismo y período de retención definidos para publicaciones eliminadas (→ RF-NOT-01)

---

### Módulo 8: Sistema de Reportes y Moderación

#### RF-MOD-01 — Reporte de publicación
**Prioridad:** Alta

El sistema permitirá a cualquier usuario autenticado reportar una publicación que considere inapropiada, proporcionando una razón predefinida y un campo opcional de detalle.

Cualquier usuario autenticado podrá reportar una publicación por las siguientes razones:
- Contenido inapropiado o engañoso
- Producto prohibido
- Spam o publicación duplicada
- Otro (campo de texto libre)

**Confirmación al reportero:** Al enviar el reporte exitosamente, el sistema confirma al usuario que el reporte fue recibido.

---

#### RF-MOD-02 — Reporte de usuario
**Prioridad:** Alta

Cualquier usuario autenticado podrá reportar a otro usuario por las siguientes razones:
- Comportamiento inadecuado
- Acoso
- Fraude
- Otro (campo de texto libre)

---

#### RF-MOD-03 — Herramientas de administración
**Prioridad:** Alta

El sistema contará con un conjunto de herramientas de administración accesibles únicamente para usuarios con rol de administrador, que permitirán moderar contenido, gestionar reportes y administrar la plataforma sin necesidad de acceso directo a la base de datos.

Las capacidades de administración incluyen:
- Consultar y gestionar reportes pendientes: ver detalle, cambiar estado y registrar acción tomada.
- Ejecutar acciones de moderación sobre publicaciones: eliminar contenido y notificar al usuario afectado con el motivo.
- Ejecutar acciones de moderación sobre usuarios: suspender cuentas (reversible) o eliminar y anonimizar la cuenta de forma permanente ejecutando el mismo flujo de RF-AUTH-09 (irreversible), registrando el motivo en ambos casos (→ RF-MOD-04 para el historial de estas acciones). La eliminación se reserva para violaciones graves donde la suspensión es insuficiente (ej. fraude, contenido ilegal, orden de una autoridad).
- Gestionar el catálogo de campus: crear, editar y desactivar campus.
- Publicar y retirar anuncios generales dirigidos a todos los usuarios activos de la plataforma.
- Consultar métricas básicas de uso: usuarios registrados, publicaciones activas por categoría y reportes pendientes.
- Gestionar el catálogo de edificios y áreas de cada campus: crear, editar y desactivar edificios.

Los contratos técnicos de los endpoints que implementan estas capacidades se encuentran en SDD §4.13.

---

#### RF-MOD-04 — Historial de acciones de moderación sobre usuarios
**Prioridad:** Media

El sistema mantendrá un registro histórico de cada acción de moderación ejecutada sobre una cuenta de usuario (suspensión, reactivación, o eliminación), permitiendo al administrador consultar el historial completo de una cuenta en cualquier momento — no solo la acción más reciente.

Cada registro del historial incluirá, como mínimo:
- El tipo de acción ejecutada (suspensión, reactivación, eliminación).
- El motivo proporcionado por el administrador en el momento de la acción (→ RF-MOD-03).
- La fecha y hora en que se ejecutó.
- El administrador que la ejecutó.

**Razón de diseño:** una cuenta puede ser suspendida y reactivada más de una vez a lo largo de su vida en la plataforma. Conservar únicamente el motivo de la acción más reciente impediría detectar patrones de reincidencia o auditar decisiones pasadas de moderación. Este historial es independiente del estado actual de la cuenta (activa, suspendida o eliminada), que el sistema debe poder consultar de forma inmediata sin depender de este registro histórico.

Este historial es de uso exclusivo del panel de administración y no es visible para el usuario afectado ni para otros usuarios de la plataforma.

---

#### RF-MOD-05 — Reporte general de la plataforma
**Prioridad:** Media

Un usuario autenticado podrá enviar un reporte general sobre un problema con la plataforma. A diferencia de los reportes de contenido (RF-MOD-01, RF-MOD-02), no requiere razón predefinida — el campo de detalle es obligatorio y contiene la descripción completa del problema.

---

### Módulo 9: Notificaciones

#### RF-NOT-01 — Notificaciones in-app
**Prioridad:** Alta

El sistema generará notificaciones persistentes dentro de la aplicación para mantener al usuario informado sobre eventos relevantes relacionados con su actividad en la plataforma.

El sistema generará notificaciones in-app para los siguientes eventos:
- Alguien dejó una reseña en el perfil del vendedor.
- Una publicación o una reseña fue eliminada por un administrador, con razón.
- Un producto guardado en favoritos está disponible a menos del umbral de proximidad (→ RF-GEO-03) — el vendedor tiene el modo "Estoy vendiendo ahora" activo.
- El administrador publicó un anuncio general del sistema.

**Retención:** Todas las notificaciones, independientemente de su tipo, permanecen visibles en P-10 durante 30 días desde su generación; al vencer este período, dejan de mostrarse ahí. Las notificaciones de tipo "publicación eliminada por moderación" no se eliminan del sistema al vencer ese período — permanecen consultables de forma permanente en el historial de moderación (P-16). El resto de tipos de notificación se eliminan físicamente del sistema a los 30 días.

---

#### RF-NOT-02 — Notificaciones push web
**Prioridad:** Baja

En versiones posteriores, el sistema podrá enviar notificaciones push al dispositivo del usuario (con permiso previo) para alertas de proximidad (RF-GEO-03) y novedades de vendedores.

---

#### RF-NOT-03 — Anuncios generales del sistema
**Prioridad:** Media

El administrador podrá enviar un anuncio general que se distribuye como notificación a todos los usuarios activos de la plataforma, para comunicar mantenimientos, nuevas funciones u otros avisos relevantes para la comunidad.

**Mecanismo de envío:** El anuncio se crea mediante el endpoint de anuncios (→ SDD §4.13). El servidor genera las notificaciones para todos los usuarios activos en una única operación, evitando un ciclo de inserciones individuales por usuario.

**Identificador de lote:** Cada anuncio se asocia a un identificador de lote común entre todos los registros generados por el mismo envío. Esto permite al administrador retractar un anuncio enviado por error, eliminando todas sus notificaciones asociadas en una sola operación sin afectar otras notificaciones de los usuarios.

**Inmutabilidad del contenido:** Una vez enviado, el texto del anuncio no puede editarse. Si el administrador necesita corregirlo, debe retractar el anuncio original y enviar uno nuevo.

**Nota sobre retención:** El registro del anuncio y su conteo de destinatarios siguen la misma retención de 30 días definida en RF-NOT-01. No se mantiene un historial permanente de anuncios enviados.

---

### Módulo 10: Favoritos

#### RF-FAV-01 — Guardar producto en favoritos
**Prioridad:** Alta

Un usuario autenticado podrá guardar cualquier publicación activa en su lista de favoritos desde cualquier pantalla donde una publicación sea visible.

Si el usuario no está autenticado al presionar el ícono, se aplica el flujo de autenticación diferida definido en RF-AUTH-02. Una vez autenticado, la acción de guardar se completa automáticamente.

**Restricción:** Un usuario no puede guardar el mismo producto más de una vez. Si el usuario vuelve a presionar el ícono de corazón se removerá el producto de favoritos.

---

#### RF-FAV-02 — Eliminar producto de favoritos
**Prioridad:** Alta

El sistema permitirá al usuario eliminar cualquier producto de su lista de favoritos desde cualquier pantalla donde una publicación sea visible y tenga la opcionalidad, sin necesidad de navegar a la pantalla dedicada de favoritos.

---

#### RF-FAV-03 — Listar favoritos del usuario
**Prioridad:** Alta

El usuario autenticado podrá acceder a su lista completa de productos guardados en P-09 (`/favoritos`). La lista se ordena por defecto por fecha de guardado descendente.

Los productos pausados o eliminados se mantienen en la lista con un estado visual diferenciado que indica su no disponibilidad, y la acción de eliminar de favoritos permanece disponible sobre ellos.

Un producto guardado en estado pausado conserva su detalle accesible (P-02).

---

### Módulo 11: Campus

> **Principio de diseño del módulo:** El campus es una dimensión de contexto geográfico, no una categoría de producto. Opera como un selector de primer nivel que filtra todo el contenido de la plataforma — catálogo, mapa y ubicaciones — sin mezclarse con los atributos del producto.

---

#### RF-CAMPUS-01 — Gestión del catálogo de campus
**Prioridad:** Alta

Los campus son administrables por el equipo operador a través de un panel de administración (→ SDD §4.13). Los datos iniciales se cargan antes del lanzamiento del MVP.

| nombre            | slug           |
| ----------------- | -------------- |
| UABC Sauzal       | `sauzal`       |
| UABC Valle Dorado | `valle-dorado` |

Cada campus almacena sus coordenadas de centro y nivel de zoom por defecto para el mapa (→ SDD §5.2 `campuses`), permitiendo que P-04 se centre automáticamente al seleccionarlo.

---

#### RF-CAMPUS-02 — Selector de campus en panel de filtros
**Prioridad:** Alta

El sistema mantendrá siempre un campus activo seleccionado que determina qué publicaciones se muestran.

**Comportamiento:**
- Siempre hay exactamente un campus seleccionado — no existe estado vacío.
- El valor por defecto al entrar a la app es el campus principal del perfil del usuario. Para visitantes no autenticados, el default en los filtros es UABC Sauzal.
- La selección persiste localmente en el navegador entre sesiones.
- Al cambiar de campus el contenido se actualiza sin recargar la página.
- El campus activo se refleja en la URL como query param (`?campus=sauzal`) para permitir compartir búsquedas contextualizadas.
- El campus **no se resetea** al presionar "Limpiar todo" en el panel de filtros (ver RF-CAT-03).

---

## 6. Requisitos No Funcionales

### 6.1 Rendimiento

| Requisito                     | Métrica                                                        |
| ----------------------------- | -------------------------------------------------------------- |
| Tiempo de carga inicial (LCP) | < 2.5 segundos en conexión 4G                                  |
| Tiempo de respuesta de API    | < 500 ms para el 95% de las peticiones                         |
| Carga de imágenes             | Imágenes optimizadas (WebP, lazy loading), < 200 KB por imagen |
| Paginación del catálogo       | Máximo 20 ítems por página, carga con infinite scroll          |

### 6.2 Seguridad

| Requisito              | Detalle                                                                                                                                                                 |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Autenticación          | Esquema de doble token (access + refresh) con almacenamiento diferenciado por nivel de sensibilidad. → SDD §3.3.1 para el modelo completo.                              |
| Protección CSRF        | Mitigada por diseño mediante la combinación de tres mecanismos complementarios sin tokens CSRF clásicos. → SDD §3.3.3 para el modelo completo.                          |
| Rate limiting          | El sistema limita la frecuencia de peticiones por IP en endpoints públicos y por usuario en el endpoint de contacto, para prevenir abuso. Valores exactos → SDD §3.3.4. |
| Sanitización de inputs | Validación y sanitización de todos los inputs en servidor (backend)                                                                                                     |
| HTTPS                  | Todo el tráfico cifrado mediante TLS 1.2+ (provisto por Vercel)                                                                                                         |

### 6.3 Disponibilidad y Confiabilidad

- **SLA objetivo:** 99.5% de disponibilidad mensual (provisto principalmente por Vercel y Neon).
- **Manejo de errores:** Todos los errores de API retornarán respuestas JSON estructuradas con código HTTP apropiado y mensaje descriptivo.
- **Degradación elegante:** Si el servicio de geolocalización o el mapa no están disponibles, el resto de la plataforma debe seguir funcionando correctamente.

### 6.4 Usabilidad y Accesibilidad

- Diseño **mobile-first** y totalmente responsivo con breakpoints.
- Cumplimiento con **WCAG 2.1 nivel AA** para accesibilidad.
- Soporte para navegadores modernos: Chrome 100+, Firefox 100+, Safari 15+, Edge 100+.
- Idioma principal: **Español (México)**. El sistema no requiere soporte multilingüe en el MVP.
- Interfaz intuitiva que no requiere tutorial o capacitación previa.

### 6.5 Mantenibilidad

- Cobertura de pruebas unitarias mínima del **70%** en lógica de negocio del backend.
- Variables de entorno gestionadas mediante archivos `.env` con validación en tiempo de inicio del servidor.
- Commits bajo el estándar **Conventional Commits** (`feat:`, `fix:`, `chore:`, etc.).

### 6.6 Escalabilidad

- La arquitectura serverless de Vercel y Neon permite escalar horizontalmente sin cambios de infraestructura para el rango esperado de usuarios (hasta ~5,000 usuarios activos).
- Las consultas a la base de datos deberán contar con índices apropiados en campos de búsqueda frecuente (`category`, `created_at`, `user_id`, `location`).

---

## 7. Especificación de Interfaz de Usuario (UI)

> Esta sección especifica los requisitos de interfaz de usuario de Cima Market: la estructura de navegación, el inventario de páginas, el comportamiento funcional de cada pantalla y los estados transversales de la aplicación. Incluye decisiones de navegación global (patrones mobile/desktop) que condicionan la arquitectura del frontend. El diseño visual detallado — paleta de colores, tipografía, espaciado y componentes específicos — queda fuera del alcance de este documento y corresponde al Design Spec del proyecto.

---

### 7.1 Principios de Diseño

| Principio                            | Descripción                                                                                                                                                         |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Mobile-first**                     | El diseño se concibe primero para pantallas en dispositivos móviles y se adapta progresivamente a tablets y desktop.                                                |
| **Claridad sobre decoración**        | Cada elemento en pantalla debe tener un propósito funcional claro. Se evitan elementos decorativos que compitan con el contenido.                                   |
| **Acción principal siempre visible** | En las pantallas en donde se tenga una acción primaria se mostrará correspondientemente una acción primaria evidente (CTA). El usuario nunca debe buscar qué hacer. |
| **Feedback inmediato**               | Toda interacción (tap, envío de formulario, carga) debe tener respuesta visual en menos de 100 ms.                                                                  |
| **Acceso progresivo**                | Las funciones avanzadas (vender, ubicación, notificaciones) se presentan cuando el usuario las necesita, no desde el primer acceso.                                 |
| **Consistencia de componentes**      | Botones, tarjetas, inputs y modales siguen un sistema de diseño único en toda la aplicación.                                                                        |

---

### 7.2 Navegación Global

La aplicación utiliza dos patrones de navegación según el breakpoint activo, manteniendo consistencia en los destinos y reglas de acceso entre ambos.

#### Estructura de navegación

| Destino        | Ruta              | Acceso      | Descripción                                                          |
| -------------- | ----------------- | ----------- | -------------------------------------------------------------------- |
| Inicio         | `/`               | Público     | Catálogo principal con campus activo y filtros en estado por defecto |
| Buscar         | `/buscar`         | Público     | Búsqueda dedicada con campo de texto en foco automático              |
| Mapa           | `/mapa`           | Autenticado | Mapa interactivo centrado en el campus activo                        |
| Favoritos      | `/favoritos`      | Autenticado | Lista de productos guardados por el usuario                          |
| Perfil         | `/perfil/:id`     | Autenticado | Perfil propio en modo propietario                                    |
| Notificaciones | `/notificaciones` | Autenticado | Centro de notificaciones con badge de no leídas                      |

Los destinos autenticados aplican el patrón de autenticación diferida definido en RF-AUTH-02.

#### Móvil (< 1024 px)

Bottom navigation bar fija de 5 ítems: Inicio, Buscar, Mapa, Favoritos y Perfil. Permanece visible en todas las pantallas principales y se oculta en flujos de pantalla completa.

El ícono de notificaciones se ubica en el header superior derecho. Muestra un badge numérico cuando hay notificaciones no leídas.

#### Header superior (móvil)

Presente solo en las pantallas necesarias. En pantallas principales muestra el logotipo y el icono de notificación. En pantallas secundarias lo reemplaza un botón de retroceso con el título de la sección actual.

#### Desktop (≥ 1024 px)

Top navigation bar horizontal fija que reemplaza la bottom bar, contiene: logotipo, ítems de navegación principales (Inicio, Mapa, Favoritos, notificaciones, perfil) y barra de búsqueda expandida.

---

### 7.3 Inventario de Páginas y Rutas

| #                                               | Página                  | Ruta                        | Acceso mínimo                  | Descripción                                                                                    |
| ----------------------------------------------- | ----------------------- | --------------------------- | ------------------------------ | ---------------------------------------------------------------------------------------------- |
| P-01                                            | Catálogo                | `/`                         | Público                        | Pantalla principal. Feed de publicaciones activas.                                             |
| P-02                                            | Detalle de Publicación  | `/producto/:id`             | Público                        | Información completa de un producto.                                                           |
| P-03                                            | Perfil de Usuario       | `/perfil/:id`               | Público/Autenticado            | Perfil público o privado dependiendo de si el usuario viendo el perfil es el propietario o no. |
| P-04                                            | Mapa del Campus         | `/mapa`                     | Autenticado                    | Mapa interactivo con vendedores y edificios.                                                   |
| P-05                                            | Autenticación           | `/auth`                     | Público                        | Pantalla de login/registro unificado.                                                          |
| P-06                                            | Onboarding              | `/onboarding`               | Público (solo nuevos usuarios) | Configuración inicial post-registro.                                                           |
| P-07                                            | Crear Publicación       | `/publicar`                 | Vendedor autenticado           | Formulario de nueva publicación.                                                               |
| P-08                                            | Editar Publicación      | `/publicar/:id/editar`      | Autenticado (propietario)      |
| Formulario de edición de publicación existente. |
| P-09                                            | Favoritos               | `/favoritos`                | Autenticado                    | Lista de productos guardados por el usuario.                                                   |
| P-10                                            | Notificaciones          | `/notificaciones`           | Autenticado                    | Lista de notificaciones del usuario.                                                           |
| P-11                                            | Configuración de cuenta | `/configuracion`            | Autenticado                    | Configuración de la cuenta del usuario.                                                        |
| P-12                                            | Términos de Uso         | `/terminos`                 | Público                        | Documento legal de términos de uso.                                                            |
| P-13                                            | Aviso de Privacidad     | `/privacidad`               | Público                        | Documento de aviso de privacidad (LFPDPPP).                                                    |
| P-14                                            | Búsqueda                | `/buscar`                   | Público                        | Pantalla de búsqueda dedicada.                                                                 |
| P-15                                            | Reseñas del Vendedor    | `/perfil/:id/resenas`       | Público                        | Lista completa paginada de reseñas recibidas por un vendedor.                                  |
| P-16                                            | Historial de Moderación | `/configuracion/moderacion` | Autenticado                    | Registro permanente de acciones de moderación tomadas sobre el contenido del usuario.          |

---

### 7.4 Descripción Detallada de Páginas

---

#### P-01 — Catálogo (`/`)

**Propósito:** Punto de entrada principal. Permite a cualquier usuario descubrir productos disponibles en el campus activo.

**Información requerida:** listado de publicaciones activas con imagen principal, título, precio, nombre del vendedor, calificación promedio del vendedor e indicador de si el vendedor está activo en tiempo real en ese momento. El listado se ordena por defecto por fecha de publicación descendente.

**Acciones disponibles:**
- Filtrar el catálogo (RF-CAT-03).
- Ordenar el catálogo (RF-CAT-04).
- Guardar una publicación en favoritos (RF-FAV-01).
- Navegar al detalle de una publicación (P-02).

**Reglas de visibilidad condicional:**
- El selector de campus aparece como la primera sección del panel de filtros, separado visualmente del resto de las opciones.
- El campus seleccionado siempre tiene un valor activo; nunca existe un estado sin campus.
- El campus activo no se resetea al limpiar los demás filtros (RF-CAT-03, RF-CAMPUS-02).
- Si no hay resultados para los filtros aplicados, se muestra un estado vacío con mensaje descriptivo y acción sugerida.
- El ícono de favoritos de cada publicación refleja el estado guardado del usuario autenticado. Si no hay sesión, aplica autenticación diferida al interactuar con él.

---

#### P-02 — Detalle de Publicación (`/producto/:id`)

**Propósito:** Presentar la información completa de una publicación y permitir al comprador contactar al vendedor o gestionar la publicación si es su propietario.

**Información requerida:** imágenes del producto, título, precio, categoría, descripción completa, horarios y días de venta (si el vendedor los especificó), ubicación habitual de venta (si el vendedor la especificó), nombre del vendedor, calificación promedio del vendedor e indicador de si el vendedor está activo en tiempo real en ese momento.

**Acciones disponibles:**
- Iniciar contacto automático con el vendedor mediante mensaje preformateado (RF-WA-01).
- Iniciar contacto libre con el vendedor (RF-WA-02).
- Guardar en favoritos (RF-FAV-01). No disponible para el propietario de la publicación.
- Reportar la publicación (RF-MOD-01) — requiere autenticación. No disponible para el propietario.
- Navegar al perfil del vendedor (P-03).
- Ver la ubicación del vendedor en el mapa — visible únicamente si la publicación está activa y el vendedor tiene el modo "Estoy vendiendo ahora" activo en este momento. Navega a P-04 con el marcador del vendedor centrado, su popup abierto automáticamente, y este producto como primer elemento de la lista de productos adicionales del vendedor.
- **Solo propietario:** editar la publicación (P-08), pausar la publicación y eliminar la publicación (con confirmación).

**Reglas de visibilidad condicional:**

| Estado de la publicación | Comportamiento                                                                                                                                                                |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Activa                   | Renderizado completo. Todas las acciones disponibles según rol.                                                                                                               |
| Pausada (visitante)      | Renderizado completo. Las acciones de contacto se reemplazan por un aviso de no disponibilidad y un enlace al perfil del vendedor. El ícono de favoritos permanece funcional. |
| Pausada (propietario)    | Igual que visitante, pero las opciones de gestión (reactivar, editar, eliminar) siguen disponibles.                                                                           |
| Eliminada                | Se renderiza una pantalla de "producto no encontrado" sin exponer ningún dato del producto ni del vendedor.                                                                   |

**Nota — indicador y acceso al mapa en tiempo real:** El indicador "Vendiendo ahora" y la acción "Ver la ubicación del vendedor en el mapa" solo se muestran cuando la publicación está activa. Esto es consistente con que el marcador del vendedor en el mapa (producto destacado + lista secundaria) solo incluye publicaciones activas (SDD §4.11, §4.12) — mostrar cualquiera de los dos elementos sobre una publicación pausada sería engañoso, ya que esa publicación no aparecería en el mapa. Ninguno de los dos se muestra para publicaciones eliminadas (P-02 no se renderiza en ese caso).

**Razón de diseño — distinción entre pausado y eliminado:** Los productos pausados son temporalmente inactivos por decisión del vendedor; el enlace puede volver a ser válido, por lo que se preserva la página. Los productos eliminados nunca estarán disponibles en esa URL, por lo que se muestra una pantalla de no encontrado.

---

#### P-03 — Perfil de Usuario (`/perfil/:id`)

**Propósito:** Mostrar el perfil completo de cualquier usuario junto con sus publicaciones activas y reseñas recibidas. Renderiza en dos modos según si el usuario autenticado es o no el dueño del perfil.

**Información requerida (ambos modos):**
- Foto de perfil, nombre de display y campus principal.
- Calificación promedio y número de reseñas.
- Número de publicaciones activas.
- Indicador "Vendiendo ahora" — visible únicamente si el vendedor tiene el modo activo en este momento.
- Lista de publicaciones del usuario, organizada en dos pestañas: "Activas" y "Pausadas". Ambas pestañas son visibles para cualquier usuario, incluyendo visitantes no autenticados.
- Lista de las últimas 5 reseñas recibidas, con respuesta del vendedor si existe. Sección oculta si no hay reseñas.

**Reglas de visibilidad condicional (ambos modos):**
- Calificación promedio y número de reseñas — visible si el usuario tiene al menos una reseña recibida, independientemente de si el rol vendedor está activo en este momento.
- Número de publicaciones activas — corresponde al conteo de la pestaña "Activas" únicamente.
- Si la pestaña "Activas" no tiene publicaciones (todas están pausadas, o el usuario aún no ha creado ninguna), la pestaña permanece visible: el número muestra "0" y el contenido muestra un mensaje breve indicando que no hay publicaciones activas en este momento.
- La pestaña "Pausadas" sigue el mismo comportamiento: permanece visible incluso sin resultados, mostrando un mensaje breve equivalente si el usuario no tiene publicaciones pausadas.
- Resumen de calificación y lista de reseñas — sección oculta si el usuario no tiene reseñas recibidas.
- En el menú de cada reseña, "Eliminar reseña" solo aparece si el usuario autenticado es el autor de esa reseña específica — no el dueño del perfil que se está visitando.
- La opción de dejar una reseña al vendedor es visible únicamente si el usuario autenticado ha iniciado contacto previamente con este vendedor y no ha dejado reseña aún.

---

**MODO VISITANTE**

**Acciones disponibles:**
- Compartir el perfil mediante el selector nativo del dispositivo. En navegadores sin soporte, copia el enlace al portapapeles.
- Reportar el perfil (RF-MOD-02).
- Navegar al detalle de cualquier publicación del vendedor (P-02).
- Ver todas las reseñas (P-15).
- Dejar una reseña al vendedor (RF-REV-01).
- En cada reseña, el usuario puede:
  - Reportarla como inapropiada (RF-REV-04).
  - Eliminarla (RF-REV-01) — únicamente si el usuario autenticado es el autor de esa reseña específica.

---

**MODO PROPIETARIO**

Incluye todo lo del modo visitante más los siguientes elementos exclusivos:

**Acciones adicionales:**
- Navegar a la configuración de cuenta (P-11).
- Compartir el perfil (mismo comportamiento que modo visitante).
- Activar o desactivar el modo "Estoy vendiendo ahora" — disponible únicamente si el rol vendedor está activo (→ RF-GEO-02).
- Crear una nueva publicación (P-07).
- Sobre cada publicación propia: pausar, reactivar, ver publicación (P-02), editar publicación (P-08) y eliminar (con confirmación).
- En cada reseña recibida: responder mediante un campo de texto (RF-REV-02) y reportarla como inapropiada (RF-REV-04).

---

#### P-04 — Mapa del Campus (`/mapa`)

**Propósito:** Visualizar geográficamente los vendedores con el modo activo en tiempo real y los edificios del campus seleccionado, con foco en los productos disponibles para compra inmediata.

**Información requerida:**
- Mapa centrado en el campus activo con sus coordenadas y nivel de zoom por defecto.
- Marcadores de los vendedores con el modo "Estoy vendiendo ahora" activo en ese campus. Cada marcador muestra visualmente el producto destacado del vendedor (imagen thumbnail).
- Al seleccionar un marcador, el sistema despliega un popup con:
  1. **Producto destacado** — imagen, título, precio y acción de navegar a su detalle (P-02).
  2. **Lista de hasta 4 productos activos adicionales** del vendedor en ese campus
     — imagen pequeña, título y precio de cada uno. Si tiene más, se ofrece acción para ver todos en su perfil (P-03).
  3. **Mini tarjeta del vendedor** — foto de perfil, nombre y calificación promedio, con acción para navegar a su perfil completo (P-03).
- Edificios y áreas del campus (RF-MAP-02).
- Lista de productos de vendedores activos en ese campus ordenados por distancia al usuario — requiere permiso de geolocalización.

**Acciones disponibles:**
- Cambiar entre campus disponibles. Al cambiar, el mapa se recentra y recarga los marcadores del campus seleccionado.
- Filtrar marcadores/Lista de productos por categoría de producto.
- Centrar el mapa en la ubicación del usuario — requiere permiso de geolocalización. Si el permiso no ha sido otorgado, el sistema lo solicita al interactuar con esta acción.
- Navegar al detalle del producto destacado o de cualquier producto de la lista secundaria (P-02).
- Navegar al perfil del vendedor desde su mini tarjeta en el popup (P-03).

**Reglas de visibilidad condicional:**
- Si el usuario no ha otorgado permiso de geolocalización, la lista de productos se muestra ordenada por fecha de activación del modo descendente, sin indicador de distancia. 
- El control para centrar el mapa en la ubicación del usuario se reemplaza por un aviso que, al tocarlo, solicita el permiso. Al otorgarlo, la lista se reordena por distancia y el mapa se centra en la ubicación del usuario sin recargar la pantalla.
- Solo se muestran en el mapa vendedores cuyo modo "Estoy vendiendo ahora" esté activo en este momento.
- Comportamiento ante producto destacado no disponible: → RF-GEO-02.
- Un usuario no autenticado que acceda a `/mapa` ve el estado de no-autenticado estándar. Al autenticarse, tendrá acceso a la página completa.
- Si el usuario llega a esta pantalla desde la acción "Ver en el mapa" de P-02, el mapa se centra en las coordenadas del vendedor referenciado y su popup se abre automáticamente al cargar, mostrando el producto de origen como primer elemento de la lista de productos adicionales, sin esperar a que el usuario toque el marcador. Si ese producto fue pausado o eliminado entre la navegación y la carga del mapa, la lista se genera con el ordenamiento por defecto sin él. Si el vendedor ya no tiene el modo activo al momento de cargar el mapa (por ejemplo, lo desactivó entre la navegación), el mapa se centra en el campus como comportamiento por defecto y no se muestra ningún popup.

---

#### P-05 — Autenticación (`/auth`)

**Propósito:** Flujo de registro e inicio de sesión mediante Google OAuth con restricción al dominio institucional `@uabc.edu.mx`. Redirige al catálogo si ya hay una sesión activa.

**Acciones disponibles:**
- Iniciar sesión con Google — presenta el selector de cuentas de Google restringido al dominio `@uabc.edu.mx`. El usuario selecciona o confirma su cuenta institucional.
- Aceptar los Términos de Uso y el Aviso de Privacidad — requerido antes de poder iniciar el flujo de autenticación. Los enlaces a P-12 y P-13 están disponibles desde esta pantalla.

**Reglas de visibilidad condicional:**
- Si el usuario intenta autenticarse con una cuenta de dominio distinto a `@uabc.edu.mx`, el sistema muestra un error indicando que solo se permiten cuentas institucionales de la UABC.

---

#### P-06 — Onboarding (`/onboarding`)

**Propósito:** Configuración mínima del perfil en el primer acceso. Solo se presenta una vez, inmediatamente después de la primera autenticación exitosa. No puede omitirse.

**Información requerida:** ninguna preexistente — el usuario ingresa todos los datos.

**Acciones disponibles:**
- Ingresar nombre de display.
- Seleccionar campus principal (obligatorio).
- Seleccionar intención de uso, comprar o vender (obligatorio).
- Si elige vender debe ingresar su número de WhatsApp (obligatorio para esta opción).
- Confirmar y completar el onboarding.

**Reglas de visibilidad condicional:**
- El campo de WhatsApp solo aparece si el usuario selecciona la opción de vender.
- El botón de confirmación permanece deshabilitado hasta que todos los campos requeridos estén completos.

---

#### P-07 — Crear Publicación (`/publicar`)

**Propósito:** Formulario para que el vendedor publique un nuevo producto.

**Campos requeridos:** imágenes, título, categoría, campus, precio, descripción.

**Campos opcionales:** ubicación habitual de venta (pre-llenada con la ubicación habitual del vendedor si el campus de la publicación coincide con su campus principal; vacía si difiere), días y horarios de venta.

**Acciones disponibles:**
- Seleccionar y previsualizar imágenes localmente antes de publicar.
- Completar todos los campos del formulario.
- Publicar — deshabilitado hasta que todos los campos obligatorios sean válidos. Si alguna imagen es rechazada, se indica cuál y el vendedor puede sustituirla y reintentar.
- Cancelar y regresar sin guardar.

**Reglas de visibilidad condicional:**
- Si una imagen es rechazada por el servicio de moderación, se indica visualmente y el botón de publicar vuelve a habilitarse para que el vendedor corrija y reintente.

**Navegación tras publicar exitosamente:** P-02 de la publicación recién creada.

---

#### P-08 — Editar Publicación (`/publicar/:id/editar`)

**Propósito:** Modificar una publicación existente.

**Acceso:** Usuario autenticado y propietario de la publicación.

**Origen de navegación:** menú de gestión en las publicaciones, disponible únicamente para el propietario.

**Información requerida:** todos los campos de la publicación pre-poblados con sus valores actuales, incluyendo las imágenes existentes en su orden actual.

**Acciones disponibles:**
- Editar cualquier campo del formulario.
- Eliminar imágenes existentes — si eliminar una imagen dejaría la publicación sin imágenes, esta acción se deshabilita hasta que el vendedor añada al menos una nueva.
- Añadir imágenes nuevas.
- Reordenar imágenes — la imagen en posición 0 es la principal del catálogo.
- Guardar los cambios — deshabilitado si la publicación no tiene al menos una imagen.
- Eliminar la publicación — requiere confirmación.

**Navegación:**
- Tras guardar exitosamente: P-02 de la publicación editada.
- Tras eliminar: origen desde donde se accedió.
- Retroceso: origen desde donde se accedió.

---

#### P-09 — Favoritos (`/favoritos`)

**Propósito:** Mostrar al usuario autenticado todos los productos que ha guardado.

**Información requerida:** lista de publicaciones guardadas ordenadas por fecha de guardado descendente.

**Acciones disponibles:**
- Navegar al detalle de una publicación (P-02).
- Eliminar una publicación de favoritos (RF-FAV-02).

**Reglas de visibilidad condicional:**
- Las publicaciones pausadas por el vendedor desde que se guardaron permanecen en la lista pero se muestran con un estado visual indicando su estado pausado. La acción de eliminar de favoritos sigue disponible sobre ellas.
- Si la lista está vacía, se muestra un estado vacío con acción para explorar el catálogo (P-01).

---

#### P-10 — Notificaciones (`/notificaciones`)

**Propósito:** Centro de notificaciones del usuario autenticado.

**Información requerida:** lista de notificaciones en orden cronológico descendente. Cada notificación muestra su tipo, la información contextual relevante (nombre del autor, título del producto, distancia, etc.), fecha relativa e indicador visual de no leída.

**Acciones disponibles:**
- Todas las notificaciones no leídas se marcan como leídas automáticamente al entrar a esta pantalla.
- Navegar a la pantalla relevante al tocar una notificación — excepto los anuncios del sistema, que no navegan a ninguna pantalla.

**Reglas de visibilidad condicional:**
- Las notificaciones de contenido eliminado aparecen aquí durante el período de retención definido en RF-NOT-01. El historial permanente está en P-16.
- Si no hay notificaciones, se muestra un estado vacío.

---

#### P-11 — Configuración de cuenta (`/configuracion`)

**Propósito:** Configuración de la cuenta del usuario autenticado.

**Origen de navegación:** menú en P-03, modo propietario.

**Información requerida:** datos actuales del perfil en modo lectura: foto, nombre de display, campus principal, número de WhatsApp (solo si el rol vendedor está activo) y correo institucional (solo lectura, no editable).

**Acciones disponibles:**

*Edición del perfil:*
- Actualizar foto de perfil.
- Actualizar nombre de display.
- Cambiar campus principal.
- Actualizar ubicación habitual.
- Actualizar número de WhatsApp.

*Rol vendedor:*
- Activar el rol vendedor — si no hay número de WhatsApp registrado, el sistema solicita el número antes de confirmar el cambio.
- Desactivar el rol vendedor — requiere confirmación.

*Privacidad y soporte:*
- Navegar al Aviso de Privacidad (P-13).
- Navegar a los Términos de Uso (P-12).
- Navegar al Historial de Moderación (P-16).
- Reportar un problema — abre un formulario de contacto que envía el mensaje al equipo de soporte.
- Eliminar la cuenta — requiere que el usuario confirme.

*Sesión:*
- Cerrar sesión — requiere confirmación.

**Reglas de visibilidad condicional:**
- El correo institucional no es editable.
- El campo de ubicación habitual es visible solo cuando el rol vendedor está activo.

---

#### P-12 — Términos de Uso (`/terminos`)

**Propósito:** Documento legal con las condiciones de uso de la plataforma. Accesible para cualquier visitante sin autenticación.

**Información requerida:** texto completo de los Términos de Uso.

**Acciones disponibles:** ninguna más allá de la lectura del contenido.

**Origen de navegación:** checkbox de aceptación en P-05 · sección de privacidad y soporte en P-11.

---

#### P-13 — Aviso de Privacidad (`/privacidad`)

**Propósito:** Documento de aviso de privacidad en cumplimiento con la LFPDPPP. Accesible para cualquier visitante sin autenticación.

**Información requerida:** texto completo del Aviso de Privacidad, incluyendo responsable del tratamiento de datos, finalidades, datos recopilados, derechos ARCO y mecanismos de ejercicio.

**Acciones disponibles:** ninguna más allá de la lectura del contenido.

**Origen de navegación:** checkbox de aceptación en P-05 · sección de privacidad y soporte en P-11.

---

#### P-14 — Búsqueda (`/buscar`)

**Propósito:** Pantalla dedicada de búsqueda y filtrado del catálogo.

**Información requerida:** resultados de publicaciones activas que coincidan con el texto ingresado en título o descripción (RF-CAT-02), organizados con las mismas opciones de filtrado que P-01.

**Acciones disponibles:**
- Buscar por texto con actualización en tiempo real con breve retardo para evitar peticiones excesivas (RF-CAT-02).
- Filtrar y ordenar (RF-CAT-03, RF-CAT-04).
- Guardar una publicación en favoritos (RF-FAV-01).
- Navegar al detalle de una publicación (P-02).

**Reglas de visibilidad condicional:**
- Si no hay texto ingresado, se muestra el catálogo de publicaciones recientes como punto de partida.
- Si no hay resultados para el término buscado, se muestra un estado vacío indicando la ausencia.

---

#### P-15 — Reseñas del Vendedor (`/perfil/:id/resenas`)

**Propósito:** Lista completa y paginada de todas las reseñas recibidas por un vendedor específico.

**Origen de navegación:** P-03 (sección Reseñas recibidas), cuando hay más de 5 reseñas.

**Información requerida:** calificación promedio del vendedor, distribución de estrellas, número total de reseñas y lista paginada de reseñas. Cada reseña muestra el nombre del autor, calificación, fecha relativa, comentario completo y respuesta del vendedor si existe.

**Acciones disponibles:**
- Dejar una reseña al vendedor — visible únicamente si el usuario autenticado ha iniciado contacto previamente con este vendedor y no ha dejado reseña aún (RF-REV-01).
- En cada reseña, el usuario puede:
  - Reportarla como inapropiada (RF-REV-04).
  - Eliminarla (RF-REV-01) — únicamente si el usuario autenticado es el autor de esa reseña específica.

**Reglas de visibilidad condicional:**
- Si el usuario no tiene reseñas recibidas, se muestra un estado vacío.
- La pantalla es accesible independientemente de si el rol vendedor está activo en este momento — un usuario que desactiva el rol conserva su historial de reseñas visible (RF-AUTH-07).

---

#### P-16 — Historial de Moderación (`/configuracion/moderacion`)

**Propósito:** Registro permanente de todas las acciones de moderación tomadas sobre el contenido del usuario. Permite consultar el historial en cualquier momento, en cumplimiento con el derecho de acceso establecido en la LFPDPPP.

**Origen de navegación:** P-11 (sección Privacidad y soporte).

**Información requerida:** lista de registros de moderación ordenada por fecha descendente. Cada registro muestra el tipo de acción ("Publicación eliminada" o "Reseña eliminada"), el título o contenido resumido del elemento afectado, el motivo comunicado por el equipo de moderación y la fecha.

**Reglas de visibilidad condicional:**
- Si el usuario no tiene registros, se muestra un estado vacío con un mensaje apropiado.

---

### 7.5 Estados Transversales de la UI

| Estado                                      | Descripción                                                                                       | Comportamiento                                                                                                                                                                                                                               |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Carga inicial**                           | Primera carga de la página o de datos.                                                            | Skeleton screens (placeholders del mismo tamaño que el contenido real) en lugar de spinner genérico.                                                                                                                                         |
| **Carga de acción**                         | El usuario presionó un botón o se realizo alguna acción y se espera respuesta.                    | Se muestra un spinner o similar indicando que se está cargando, evitando confusión.                                                                                                                                                          |
| **Error de red**                            | Fallo de conexión al hacer una petición.                                                          | Banner no intrusivo en la parte superior: *"Sin conexión. Verifica tu internet."* con botón "Reintentar".                                                                                                                                    |
| **Error de servidor**                       | La API retorna un error 5xx.                                                                      | Mensaje de error descriptivo inline en el contexto de la acción fallida.                                                                                                                                                                     |
| **Proximidad (toast)**                      | Un vendedor de interés está activo cerca del usuario.                                             | Toast no intrusivo que aparece sobre cualquier pantalla. → RF-GEO-04.                                                                                                                                                                        |
| **Estado vacío**                            | Una lista o catálogo no tiene resultados.                                                         | Ilustración temática + mensaje descriptivo + acción sugerida (ej. "Limpiar filtros" o "Publicar el primero").                                                                                                                                |
| **Sin autenticación — pantalla de destino** | Usuario no autenticado navega directamente a una ruta de navegación primaria que requiere sesión. | Renderiza la pantalla con un estado alternativo (ilustración + mensaje + botón de inicio de sesión). Al completar el flujo de autenticación, la pantalla se actualiza con el contenido real. Ver RF-AUTH-02 para el comportamiento completo. |
| **Sin autenticación — acción puntual**      | Usuario no autenticado intenta ejecutar una acción específica que requiere sesión.                | Captura la intención, presenta el flujo de autenticación y ejecuta la acción automáticamente al completarlo. Ver RF-AUTH-02 para el comportamiento completo.                                                                                 |
| **Sin permisos**                            | Usuario autenticado intenta acceder a una ruta no autorizada para su rol.                         | Redirección al catálogo.                                                                                                                                                                                                                     |
| **Confirmación de reporte**                 | El usuario envió un reporte de publicación, usuario o reseña.                                     | Toast no intrusivo de duración breve confirmando la recepción. No navega ni genera notificación persistente.                                                                                                                                 |

---

## 8. Restricciones y Limitaciones

### 8.1 Técnicas

- El sistema no integrará pagos en línea. Cualquier transacción económica es responsabilidad exclusiva de los usuarios.
- No se implementará un chat interno en la plataforma. El canal de comunicación principal es WhatsApp.
- La geolocalización en tiempo real del vendedor solo funciona mientras el dispositivo del vendedor tenga la sesión activa y el navegador en primer plano (limitación de los service workers en iOS).

### 8.2 Legales y de Privacidad

- La ubicación en tiempo real del vendedor es un dato personal sensible y su recolección requiere consentimiento explícito, informado y revocable en cualquier momento.
- El sistema deberá contar con un **Aviso de Privacidad** visible y accesible, en cumplimiento con la LFPDPPP.
- El enlace de contacto con el vendedor se construye server-side. El acceso al endpoint de contacto requiere autenticación y está sujeto a rate limiting. → SDD §3.3.4.

### 8.3 De Negocio

- La plataforma no cobra comisión por transacción.
- La plataforma es exclusiva para la comunidad UABC y no está orientada al público general.
- El equipo de administración tiene potestad para eliminar contenido que viole las políticas de uso aceptable.

---

## 9. Criterios de Aceptación

Los siguientes criterios deben cumplirse antes del lanzamiento del MVP:

| #     | Criterio                                                                                                                                                                                                                                                                                                                                                                                                              |
| ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| AC-01 | Un visitante no autenticado puede navegar el catálogo, ver el detalle de publicaciones y ver perfiles de vendedores sin que el sistema solicite login.                                                                                                                                                                                                                                                                |
| AC-02 | Al presionar la acción de contacto con el vendedor sin sesión activa, el sistema muestra el flujo de autenticación y, tras completarlo, ejecuta la acción de contacto originalmente solicitada.                                                                                                                                                                                                                       |
| AC-03 | Un nuevo usuario puede completar el registro autenticándose con su cuenta institucional `@uabc.edu.mx` y terminar el onboarding en menos de 1 minuto.                                                                                                                                                                                                                                                                 |
| AC-04 | El sistema solo permite autenticarse con cuentas del dominio `@uabc.edu.mx`. Un intento con una cuenta de otro dominio es rechazado antes de crear o acceder a ninguna cuenta.                                                                                                                                                                                                                                        |
| AC-05 | La sesión persiste según la política de expiración/renovación definida en RF-AUTH-05. El access token se renueva automáticamente sin interrumpir al usuario.                                                                                                                                                                                                                                                          |
| AC-06 | Un usuario que elige "Solo comprar" en el onboarding puede activar el rol vendedor posteriormente desde su perfil, ingresando su número de WhatsApp.                                                                                                                                                                                                                                                                  |
| AC-07 | Un vendedor puede crear una publicación con al menos una imagen, precio y categoría, y esta aparece en el catálogo público.                                                                                                                                                                                                                                                                                           |
| AC-08 | Un comprador puede presionar "Quiero comprar" y se abre WhatsApp en una nueva pestaña/aplicación con el mensaje preformateado correcto.                                                                                                                                                                                                                                                                               |
| AC-09 | La búsqueda por texto retorna resultados relevantes en menos de 1 segundo.                                                                                                                                                                                                                                                                                                                                            |
| AC-10 | Los filtros de categoría y rango de precio funcionan correctamente y son combinables.                                                                                                                                                                                                                                                                                                                                 |
| AC-11 | Un comprador que haya iniciado contacto con un vendedor previamente puede dejar una reseña de 1-5 estrellas con comentario en el perfil de ese vendedor. El botón "Dejar reseña" no se muestra si el comprador no ha iniciado contacto previamente con ese vendedor.                                                                                                                                                  |
| AC-12 | El administrador puede ver, revisar y resolver reportes, suspender usuarios y gestionar publicaciones mediante un cliente REST externo. Todas las operaciones retornan respuestas estructuradas y requieren autenticación con rol de administrador.                                                                                                                                                                   |
| AC-13 | El sistema es completamente funcional en dispositivos móviles (Chrome en Android e iOS Safari).                                                                                                                                                                                                                                                                                                                       |
| AC-14 | El tiempo de carga inicial (LCP) no supera 2.5 segundos en una conexión 4G simulada (Lighthouse).                                                                                                                                                                                                                                                                                                                     |
| AC-15 | El selector de campus filtra correctamente el catálogo, el mapa y los resultados de búsqueda. Al cambiar de campus el contenido se actualiza sin recargar la página y la selección persiste al navegar entre secciones. El onboarding incluye el paso de selección de campus y lo persiste en el perfil del usuario.                                                                                                  |
| AC-16 | Un usuario autenticado puede guardar un producto presionando el ícono de corazón en P-01 o P-02. El ícono cambia inmediatamente a un corazón relleno. Al presionarlo de nuevo, el producto se elimina de favoritos y el ícono regresa a un corazón vacío. Un usuario no autenticado que presione el ícono ve el flujo de autenticación diferida; al completarlo, el producto queda guardado automáticamente.          |
| AC-17 | Los productos guardados en favoritos que posteriormente sean pausados o eliminados por su vendedor aparecen en P-09 con imagen en escala de grises y etiqueta "Ya no disponible", sin desaparecer de la lista. El botón "Eliminar de favoritos" sigue siendo funcional sobre esas tarjetas.                                                                                                                           |
| AC-18 | Cuando un comprador deja una reseña a un vendedor, el vendedor recibe una notificación visible en P-10 con el badge del ícono de campana incrementado. Al entrar a P-10, todas las notificaciones no leídas se marcan como leídas automáticamente y el badge desaparece.                                                                                                                                              |
| AC-19 | El número de WhatsApp del vendedor no aparece en ningún endpoint público del catálogo ni en el detalle de producto. El enlace de contacto solo es accesible para usuarios autenticados y está sujeto a rate limiting.                                                                                                                                                                                                 |
| AC-20 | Si una imagen subida en el formulario de publicación es rechazada por el servicio de moderación de contenido, el sistema cancela la publicación completa sin almacenar ningún archivo. El formulario muestra un mensaje de error indicando qué imagen fue rechazada.                                                                                                                                                  |
| AC-21 | Un usuario que completa el flujo de eliminación de cuenta en P-11 es redirigido al catálogo como visitante no autenticado. Su correo institucional queda disponible para un nuevo registro. Si intenta registrarse con el mismo correo, pasa por el flujo completo de autenticación y onboarding sin acceso a ningún dato de la cuenta eliminada.                                                                     |
| AC-22 | Un vendedor en plan gratuito que intenta crear una publicación habiendo alcanzado el límite de publicaciones totales recibe un mensaje descriptivo que le indica que debe eliminar una publicación existente antes de poder crear una nueva.                                                                                                                                                                          |
| AC-23 | Un usuario autenticado sin el rol vendedor activo que navega directamente a la ruta de creación de publicaciones es redirigido a su configuración de cuenta con un mensaje informativo antes de que la pantalla se renderice. El sistema rechaza en el servidor cualquier intento de crear publicaciones sin el rol vendedor activo. La edición y eliminación de publicaciones existentes no requieren el rol activo. |
| AC-24 | Un comprador que ve el indicador de "vendiendo ahora" en el detalle de una publicación (P-02) puede navegar al mapa (P-04) y ver el marcador de ese vendedor centrado con su popup abierto automáticamente.                                                                                                                                                                                                           |

---

## 10. Glosario

| Término                    | Definición                                                                                                                                                                                                                                               |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Catálogo**               | Vista principal de la aplicación que lista las publicaciones activas de productos.                                                                                                                                                                       |
| **Campus**                 | Sede universitaria física donde opera la plataforma. Cima Market soporta dos campus: UABC Sauzal y UABC Valle Dorado. Se selecciona desde la primera sección del panel de filtros en P-01 y P-14, y desde un control dedicado en el mapa (P-04).         |
| **CSRF**                   | Cross-Site Request Forgery. Ataque en el que un sitio malicioso induce al navegador a realizar peticiones autenticadas a otro dominio sin el conocimiento del usuario. El mecanismo de mitigación implementado en Cima Market se describe en SDD §3.3.3. |
| **Publicación**            | Anuncio creado por un vendedor que contiene información de un producto disponible.                                                                                                                                                                       |
| **Vendedor**               | Estudiante de la UABC que utiliza la plataforma para promover y vender productos.                                                                                                                                                                        |
| **Comprador**              | Estudiante de la UABC que utiliza la plataforma para descubrir y contactar vendedores.                                                                                                                                                                   |
| **Visitante**              | Usuario no autenticado. Puede explorar el catálogo pero no puede contactar vendedores ni publicar.                                                                                                                                                       |
| **Autenticación diferida** | Patrón de UX en el que el sistema no solicita login al entrar a la plataforma, sino únicamente cuando el usuario intenta realizar una acción que lo requiere.                                                                                            |
| **Onboarding**             | Flujo de configuración inicial que se presenta al usuario la primera vez que accede al sistema, tras su registro.                                                                                                                                        |
| **Access Token**           | JWT de corta duración (15 min) que autoriza las peticiones del cliente a la API.                                                                                                                                                                         |
| **Refresh Token**          | Token de larga duración (30 días) almacenado en cookie segura, utilizado para renovar el access token de forma transparente.                                                                                                                             |
| **MVP**                    | Minimum Viable Product — versión inicial del producto con las funcionalidades esenciales.                                                                                                                                                                |
| **PWA**                    | Progressive Web App — aplicación web con capacidades similares a una app nativa (offline, notificaciones, instalable).                                                                                                                                   |
| **E.164**                  | Estándar internacional de formato de números telefónicos (ej. `+526641234567`).                                                                                                                                                                          |