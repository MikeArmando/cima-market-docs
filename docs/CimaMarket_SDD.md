# Software Design Description (SDD)

## Cima Market — Plataforma de Compra-Venta para Estudiantes UABC

| Campo                   | Detalle                             |
| ----------------------- | ----------------------------------- |
| **Nombre del Producto** | Cima Market                         |
| **Versión**             | 1.0.0                               |
| **Fecha**               | 20 de Julio de 2026                 |
| **Estado**              | Aprobado                            |
| **Autor**               | Mike Armando Montano Valencia       |
| **Clasificación**       | Interno — Uso Académico/Estudiantil |

---

## Tabla de Contenidos

- [Software Design Description (SDD)](#software-design-description-sdd)
  - [Cima Market — Plataforma de Compra-Venta para Estudiantes UABC](#cima-market--plataforma-de-compra-venta-para-estudiantes-uabc)
  - [Tabla de Contenidos](#tabla-de-contenidos)
  - [1. Introducción](#1-introducción)
    - [1.1 Propósito del Documento](#11-propósito-del-documento)
    - [1.2 Alcance](#12-alcance)
    - [1.3 Relación con el SRS](#13-relación-con-el-srs)
    - [1.4 Organización del Documento](#14-organización-del-documento)
    - [1.5 Referencias](#15-referencias)
    - [1.6 Definiciones, Acrónimos y Abreviaturas](#16-definiciones-acrónimos-y-abreviaturas)
  - [2. Visión General del Diseño](#2-visión-general-del-diseño)
    - [2.1 Contexto del Sistema](#21-contexto-del-sistema)
    - [2.2 Stakeholders y sus Preocupaciones de Diseño](#22-stakeholders-y-sus-preocupaciones-de-diseño)
    - [2.3 Vistas de Diseño Seleccionadas](#23-vistas-de-diseño-seleccionadas)
    - [2.4 Restricciones de Diseño](#24-restricciones-de-diseño)
  - [3. Vistas de Diseño](#3-vistas-de-diseño)
    - [3.1 Vista de Contexto — Componentes Externos e Integraciones](#31-vista-de-contexto--componentes-externos-e-integraciones)
      - [3.1.1 Límites del Sistema](#311-límites-del-sistema)
      - [3.1.2 Integraciones con Servicios Externos](#312-integraciones-con-servicios-externos)
      - [3.1.3 Datos Sensibles y sus Fronteras](#313-datos-sensibles-y-sus-fronteras)
    - [3.2 Vista Lógica — Arquitectura de la Aplicación](#32-vista-lógica--arquitectura-de-la-aplicación)
      - [3.2.1 Arquitectura General](#321-arquitectura-general)
      - [3.2.2 Estructura del Cliente](#322-estructura-del-cliente)
      - [3.2.3 Estructura del Servidor](#323-estructura-del-servidor)
      - [3.2.4 Cadena de Middleware por Tipo de Endpoint](#324-cadena-de-middleware-por-tipo-de-endpoint)
      - [3.2.5 Comunicación Cliente-Servidor](#325-comunicación-cliente-servidor)
      - [3.2.6 Validación de Variables de Entorno](#326-validación-de-variables-de-entorno)
      - [3.2.7 Estrategia de Testing](#327-estrategia-de-testing)
    - [3.3 Vista de Seguridad](#33-vista-de-seguridad)
      - [3.3.1 Modelo de Autenticación y Gestión de Sesiones](#331-modelo-de-autenticación-y-gestión-de-sesiones)
      - [3.3.2 Modelo de Autorización](#332-modelo-de-autorización)
      - [3.3.3 Protección contra Amenazas Comunes](#333-protección-contra-amenazas-comunes)
      - [3.3.4 Rate Limiting](#334-rate-limiting)
      - [3.3.5 Seguridad en el Manejo de Imágenes](#335-seguridad-en-el-manejo-de-imágenes)
      - [3.3.6 Protección de Datos Personales (LFPDPPP)](#336-protección-de-datos-personales-lfpdppp)
  - [4. Diseño de la Interfaz de API](#4-diseño-de-la-interfaz-de-api)
    - [4.1 Autenticación y Sesiones (`/api/auth`)](#41-autenticación-y-sesiones-apiauth)
    - [4.2 Usuarios y Perfiles (`/api/users`)](#42-usuarios-y-perfiles-apiusers)
    - [4.3 Publicaciones (`/api/products`)](#43-publicaciones-apiproducts)
    - [4.4 Categorías (`/api/categories`)](#44-categorías-apicategories)
    - [4.5 Campus (`/api/campuses`)](#45-campus-apicampuses)
    - [4.6 Contacto WhatsApp (`/api/contact`)](#46-contacto-whatsapp-apicontact)
    - [4.7 Reseñas (`/api/reviews`)](#47-reseñas-apireviews)
    - [4.8 Favoritos (`/api/saved`)](#48-favoritos-apisaved)
    - [4.9 Reportes (`/api/reports`)](#49-reportes-apireports)
    - [4.10 Notificaciones (`/api/notifications`)](#410-notificaciones-apinotifications)
    - [4.11 Geolocalización en Tiempo Real (`/api/geo`)](#411-geolocalización-en-tiempo-real-apigeo)
    - [4.12 Mapa e Infraestructura del Campus (`/api/map`)](#412-mapa-e-infraestructura-del-campus-apimap)
    - [4.13 Administración (`/api/admin`)](#413-administración-apiadmin)
  - [5. Diseño de Datos](#5-diseño-de-datos)
    - [5.1 Estrategia de Persistencia](#51-estrategia-de-persistencia)
    - [5.2 Entidades y Esquema](#52-entidades-y-esquema)
      - [`campuses`](#campuses)
      - [`categories`](#categories)
      - [`campus_buildings`](#campus_buildings)
      - [`users`](#users)
      - [`user_moderation_actions`](#user_moderation_actions)
      - [`refresh_tokens`](#refresh_tokens)
      - [`seller_live_locations`](#seller_live_locations)
      - [`products`](#products)
      - [`product_images`](#product_images)
      - [`contact_events`](#contact_events)
      - [`saved_products`](#saved_products)
      - [`reviews`](#reviews)
      - [`reports`](#reports)
      - [`notifications`](#notifications)
    - [5.3 Índices y Consideraciones de Rendimiento](#53-índices-y-consideraciones-de-rendimiento)
    - [5.4 Estrategia de Limpieza de Datos (Cron Jobs)](#54-estrategia-de-limpieza-de-datos-cron-jobs)
  - [6. Decisiones de Diseño Significativas](#6-decisiones-de-diseño-significativas)
    - [DD-01 — Hono sobre Express como framework del servidor](#dd-01--hono-sobre-express-como-framework-del-servidor)
    - [DD-02 — Un único entry point serverless en lugar de una función por ruta](#dd-02--un-único-entry-point-serverless-en-lugar-de-una-función-por-ruta)
    - [DD-03 — Google OAuth con restricción de dominio institucional como mecanismo de autenticación](#dd-03--google-oauth-con-restricción-de-dominio-institucional-como-mecanismo-de-autenticación)
    - [DD-04 — Soft delete en publicaciones mediante `deleted_at`](#dd-04--soft-delete-en-publicaciones-mediante-deleted_at)
    - [DD-05 — Anonimización en lugar de borrado físico de cuentas de usuario](#dd-05--anonimización-en-lugar-de-borrado-físico-de-cuentas-de-usuario)
    - [DD-06 — Access token en memoria del cliente](#dd-06--access-token-en-memoria-del-cliente)
    - [DD-07 — Número de WhatsApp gestionado exclusivamente server-side](#dd-07--número-de-whatsapp-gestionado-exclusivamente-server-side)
    - [DD-08 — Cloudinary como servicio de imágenes con el servidor como intermediario obligatorio](#dd-08--cloudinary-como-servicio-de-imágenes-con-el-servidor-como-intermediario-obligatorio)
    - [DD-09 — Vitest y Playwright como stack de testing](#dd-09--vitest-y-playwright-como-stack-de-testing)
    - [DD-10 — Tabla de historial dedicada para acciones de moderación sobre usuarios](#dd-10--tabla-de-historial-dedicada-para-acciones-de-moderación-sobre-usuarios)
  - [Apéndices](#apéndices)
    - [A. Variables de Entorno](#a-variables-de-entorno)

---

## 1. Introducción

### 1.1 Propósito del Documento

Este documento describe el diseño técnico de **Cima Market**, detallando las decisiones de arquitectura, la estructura de componentes, los contratos de interfaz, el modelo de datos y los flujos de operación que guiarán su implementación. Su audiencia principal es el equipo de desarrollo responsable de construir el sistema.

Este SDD complementa el SRS de Cima Market y no reemplaza ni repite los requisitos funcionales — los referencia mediante identificadores (`RF-AUTH-02`, `RF-PUB-06`, etc.) para mantener trazabilidad sin duplicar contenido.

### 1.2 Alcance

El diseño descrito en este documento cubre el sistema completo de Cima Market en su versión MVP, incluyendo:

- La Single Page Application (SPA) desplegada como PWA en Vercel.
- El servidor REST API construido sobre Vercel Serverless Functions con Hono.
- La base de datos PostgreSQL serverless (Neon) con extensión PostGIS.
- La integración con servicios externos: Cloudinary, Google OAuth y la API de geolocalización del navegador.

El diseño de la interfaz de usuario final (paleta de colores, tipografía, componentes visuales específicos) queda fuera del alcance de este documento.

### 1.3 Relación con el SRS

Este SDD define la arquitectura y las soluciones técnicas diseñadas para satisfacer los objetivos detallados en la Especificación de Requisitos de Software (SRS) de Cima Market. Cuando un diseño satisface un requisito específico, se indica mediante referencia explícita al identificador del requisito (`→ RF-XXX-NN`, `→ §6.2 SRS`).

Los cambios en el SRS que afecten el alcance funcional o los requisitos no funcionales deben evaluarse contra este SDD y, si es necesario, generar una nueva versión del mismo.

### 1.4 Organización del Documento

El documento está organizado en seis secciones principales:

- **§1 Introducción** — propósito, alcance y relación con el SRS.
- **§2 Visión General del Diseño** — contexto, preocupaciones de los stakeholders y restricciones que condicionan las decisiones técnicas.
- **§3 Vistas de Diseño** — arquitectura del sistema organizada por tres perspectivas: contexto externo e integraciones (§3.1), arquitectura lógica interna (§3.2), y modelo de seguridad (§3.3).
- **§4 Diseño de la Interfaz de API** — contratos de todos los endpoints REST: método, ruta, nivel de acceso, propósito y notas de implementación.
- **§5 Diseño de Datos** — esquema de base de datos, entidades, índices y estrategia de limpieza periódica.
- **§6 Decisiones de Diseño Significativas** — registro de decisiones arquitectónicas no obvias con contexto, alternativas y justificación.
- **Apéndices** — material de soporte: variables de entorno requeridas.

### 1.5 Referencias

| Documento                                         | Versión | Relación                                        |
| ------------------------------------------------- | ------- | ----------------------------------------------- |
| SRS — Cima Market                                 | 1.0.0   | Fuente de requisitos que este SDD implementa    |
| IEEE Std 1016-2009 — Software Design Descriptions | 2009    | Estándar que gobierna la estructura de este SDD |

### 1.6 Definiciones, Acrónimos y Abreviaturas

Los términos de negocio (Vendedor, Comprador, Publicación, etc.) están definidos en el Glosario del SRS y no se repiten aquí. Este glosario cubre únicamente términos técnicos específicos del diseño.

| Término         | Definición                                                                                                                                                                                                 |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **SDD**         | Software Design Description — este documento.                                                                                                                                                              |
| **SRS**         | Software Requirements Specification — documento de requisitos de Cima Market.                                                                                                                              |
| **SPA**         | Single Page Application — aplicación web que carga una sola página HTML y gestiona la navegación en el cliente mediante JavaScript.                                                                        |
| **PWA**         | Progressive Web Application — SPA con capacidades extendidas: instalable, con soporte offline parcial y acceso a APIs nativas del dispositivo.                                                             |
| **REST**        | Representational State Transfer — estilo arquitectónico para APIs web sobre HTTP.                                                                                                                          |
| **JWT**         | JSON Web Token — estándar para transmitir información de identidad de forma compacta y verificable entre cliente y servidor.                                                                               |
| **ORM**         | Object-Relational Mapper — capa de abstracción entre el código de aplicación y la base de datos relacional.                                                                                                |
| **Serverless**  | Modelo de despliegue donde el proveedor gestiona la infraestructura; el código se ejecuta en funciones efímeras invocadas por petición.                                                                    |
| **PostGIS**     | Extensión de PostgreSQL que agrega soporte nativo para datos y operaciones geoespaciales.                                                                                                                  |
| **UPSERT**      | Operación de base de datos que inserta un registro si no existe, o actualiza el existente si ya está presente.                                                                                             |
| **Soft delete** | Técnica de eliminación lógica que marca el registro como inactivo o eliminado en el sistema sin remover la información físicamente de la base de datos, permitiendo su recuperación o auditoría posterior. |
| **Middleware**  | Función que intercepta una petición HTTP antes de llegar al handler final, aplicando lógica transversal como autenticación o validación.                                                                   |
| **GIST**        | Generalized Search Tree — tipo de índice de PostgreSQL optimizado para tipos de datos complejos como geometrías espaciales.                                                                                |
| **GIN**         | Generalized Inverted Index — tipo de índice de PostgreSQL optimizado para búsquedas full-text y datos JSONB.                                                                                               |
| **Cron Job**    | Tarea programada que se ejecuta automáticamente en intervalos definidos.                                                                                                                                   |
| **ADR**         | Architecture Decision Record — registro de una decisión de diseño significativa, con su contexto, alternativas y justificación.                                                                            |
| **E.164**       | Estándar internacional de formato de números telefónicos (ej. `+526641234567`).                                                                                                                            |
| **httpOnly**    | Atributo de cookie que la hace inaccesible desde JavaScript del cliente, previniendo ataques XSS.                                                                                                          |
| **SameSite**    | Atributo de cookie que controla si el navegador la adjunta en peticiones cross-site, mitigando CSRF.                                                                                                       |
| **SRID**        | Spatial Reference System Identifier — código que identifica un sistema de coordenadas geográficas. El valor 4326 corresponde a WGS 84 (GPS estándar).                                                      |

---

## 2. Visión General del Diseño

### 2.1 Contexto del Sistema

Cima Market opera como una aplicación web cliente-servidor de dos capas. El cliente es una SPA/PWA que se comunica exclusivamente con el servidor mediante REST API sobre HTTPS. El servidor actúa como único punto de acceso a la base de datos y a todos los servicios externos; el cliente nunca interactúa directamente con ningún servicio de terceros.

Los servicios externos con los que el sistema se integra son:

| Servicio                          | Rol en el sistema                                                        | Dirección del flujo          |
| --------------------------------- | ------------------------------------------------------------------------ | ---------------------------- |
| **Cloudinary**                    | Almacenamiento, optimización y moderación automática de imágenes         | Servidor → Cloudinary        |
| **Google OAuth 2.0**              | Verificación de identidad institucional restringida a `@uabc.edu.mx`     | Servidor ↔ Google            |
| **Neon**                          | Base de datos PostgreSQL serverless con PostGIS                          | Servidor → Neon              |
| **Vercel**                        | Hosting del cliente (SPA estática) y del servidor (Serverless Functions) | Infraestructura              |
| **WhatsApp**                      | Canal de contacto entre comprador y vendedor mediante URL scheme `wa.me` | Cliente → WhatsApp (externo) |
| **Geolocalización del navegador** | API nativa para obtener coordenadas del usuario en tiempo real           | Cliente → API nativa del SO  |

El servidor es el único componente que accede directamente a servicios externos y a datos sensibles como credenciales de Cloudinary y números de WhatsApp de los vendedores.

### 2.2 Stakeholders y sus Preocupaciones de Diseño

| Stakeholder                  | Preocupación principal de diseño                                                                                                                  |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Equipo de desarrollo**     | Claridad de contratos de API, estructura de base de datos, flujos de autenticación y moderación.                                                  |
| **Estudiantes (usuarios)**   | Rendimiento percibido, privacidad de datos (especialmente número de WhatsApp y ubicación en tiempo real), y experiencia fluida en móvil.          |
| **Administrador**            | Capacidad de moderar contenido, gestionar reportes y ejecutar acciones sobre cuentas vía API.                                                     |
| **Plataforma (Vercel/Neon)** | Compatibilidad con el modelo serverless: funciones efímeras sin estado persistente entre invocaciones, y consultas eficientes a la base de datos. |

### 2.3 Vistas de Diseño Seleccionadas

Este SDD organiza el diseño en las siguientes vistas y componentes, cada uno respondiendo a las preocupaciones de los stakeholders identificados arriba:

| Componente               | Sección | Preocupación que aborda                                                                                                   |
| ------------------------ | ------- | ------------------------------------------------------------------------------------------------------------------------- |
| **Vista de Contexto**    | §3.1    | Límites del sistema, integraciones externas y fronteras de datos sensibles.                                               |
| **Vista Lógica**         | §3.2    | Estructura interna del cliente y del servidor, capas, middleware y comunicación.                                          |
| **Vista de Seguridad**   | §3.3    | Modelo de autenticación y autorización, protección de datos sensibles, mitigación de amenazas y cumplimiento con LFPDPPP. |
| **Interfaz de API**      | §4      | Contratos de API REST: endpoints, métodos, acceso y notas de implementación.                                              |
| **Diseño de Datos**      | §5      | Esquema de base de datos, entidades, índices y estrategia de persistencia.                                                |
| **Decisiones de Diseño** | §6      | Registro de decisiones arquitectónicas no obvias: contexto, alternativas evaluadas y justificación de la opción elegida.  |

### 2.4 Restricciones de Diseño

Las siguientes restricciones son impuestas por el entorno de ejecución, las dependencias externas o los requisitos del SRS, y condicionan directamente las decisiones de diseño:

| Restricción                                 | Origen               | Impacto en el diseño                                                                                                                            |
| ------------------------------------------- | -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| Ejecución serverless sin estado persistente | Vercel               | El servidor no puede mantener conexiones WebSocket persistentes ni estado en memoria entre invocaciones. Cada función es efímera.               |
| Pool de conexiones de base de datos         | Neon serverless      | Las conexiones a PostgreSQL deben gestionarse con un pool adaptado al modelo serverless.                                                        |
| Sin acceso directo del cliente a Cloudinary | Seguridad (SRS §6.2) | El servidor actúa como intermediario obligatorio en todas las subidas de imágenes.                                                              |
| Enlace de contacto construido server-side   | Arquitectura (DD-07) | El servidor construye la URL de WhatsApp internamente. El cliente recibe un string listo para abrir, sin lógica de construcción en el frontend. |
| Geolocalización solo desde el navegador     | API nativa           | La ubicación del usuario se obtiene exclusivamente mediante la Geolocation API del navegador; no hay geolocalización por IP.                    |
| Datos personales bajo LFPDPPP               | Legal (SRS §8.2)     | El diseño de la base de datos debe soportar anonimización en lugar de borrado físico para preservar integridad referencial.                     |

## 3. Vistas de Diseño

### 3.1 Vista de Contexto — Componentes Externos e Integraciones

Esta vista describe los límites del sistema y cómo Cima Market se relaciona con cada servicio externo. Su propósito es dejar claro qué responsabilidades pertenecen al sistema y cuáles se delegan a terceros.

---

#### 3.1.1 Límites del Sistema

El sistema Cima Market se compone de dos artefactos desplegables propios:

- **Cliente** — SPA/PWA servida como archivos estáticos desde Vercel CDN.
- **Servidor** — conjunto de Vercel Serverless Functions agrupadas bajo un único entry point (`api/index.ts`) con routing interno gestionado por Hono.

Todo lo que esté fuera de estos dos artefactos es un servicio externo. El cliente se comunica únicamente con el servidor propio. El servidor es el único componente que se comunica con servicios externos.

---

#### 3.1.2 Integraciones con Servicios Externos

**Neon (PostgreSQL serverless)**

El servidor es el único consumidor de la base de datos. Ningún cliente externo tiene credenciales de acceso directo. La conexión usa el driver de Neon con soporte para entornos serverless, que gestiona el pooling de conexiones internamente para evitar el agotamiento de conexiones típico de funciones efímeras.

Responsabilidades delegadas a Neon: persistencia de todos los datos estructurados, ejecución de consultas geoespaciales mediante PostGIS, y disponibilidad del servicio bajo el SLA del proveedor.

**Cloudinary**

El servidor actúa como intermediario obligatorio en todas las operaciones sobre imágenes. El cliente nunca interactúa con Cloudinary directamente. El flujo es siempre: cliente → servidor → Cloudinary.

Responsabilidades delegadas a Cloudinary: almacenamiento físico de archivos, conversión automática de HEIC a formatos web, aplicación de transformaciones de imagen (recorte, redimensionado, conversión a WebP), y moderación automática de contenido mediante su add-on nativo.

Responsabilidades retenidas en el servidor: decisión de cuándo invocar la subida, construcción de las URLs de transformación antes de retornarlas al cliente, y ejecución del rollback de archivos cuando una publicación falla (→ RF-PUB-06).

**Convención de transformaciones de imagen**

Las URLs de transformación se construyen server-side antes de devolverse al cliente. Ninguna transformación se almacena como segunda URL en la base de datos — todas se derivan a partir del `cloudinary_public_id` cuando el contexto lo requiere, excepto el thumbnail, que sí se persiste como la URL principal en `product_images.url`.

| Contexto                                                    | Transformación Cloudinary           | Notas                                                                                                                                  |
| ----------------------------------------------------------- | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Thumbnail en tarjetas del catálogo (P-01, P-14, P-09, P-03) | `c_fill,ar_1:1,w_400,f_webp,q_auto` | Imagen cuadrada recortada desde el centro. Garantiza grid uniforme. Se persiste en `product_images.url`.                               |
| Galería de detalle de publicación (P-02)                    | `c_limit,w_1200,f_webp,q_auto`      | Proporción original, limitada a 1200 px de ancho. Se deriva server-side en `GET /api/products/:id` a partir de `cloudinary_public_id`. |
| Avatar de usuario                                           | `c_fill,ar_1:1,w_200,f_webp,q_auto` | Imagen cuadrada recortada desde el centro. Se retorna en la respuesta de `POST /api/users/avatar`.                                     |

Esta tabla es la fuente única de verdad para todas las transformaciones de Cloudinary del sistema. Los endpoints en §4 la referencian sin repetir los parámetros de transformación.

**Google Identity (OAuth 2.0)**

El servidor invoca la API de Google OAuth exclusivamente para verificar la identidad institucional del usuario durante el flujo de autenticación (→ RF-AUTH-03). El parámetro `hd=uabc.edu.mx` garantiza que solo cuentas del dominio institucional pueden autenticarse. Google gestiona internamente la verificación de identidad y la protección contra fuerza bruta.

**Vercel (plataforma de hosting)**

Vercel gestiona el despliegue del cliente como archivos estáticos en su CDN global, el despliegue del servidor como Serverless Functions bajo el runtime de Node.js, y la ejecución de Cron Jobs para tareas de limpieza periódica.

**WhatsApp (URL scheme `wa.me`)**

La integración con WhatsApp es unidireccional y pasiva: el servidor construye una URL del formato `https://wa.me/{número}?text={mensaje}` y la retorna al cliente, que la abre en una nueva pestaña del navegador. No existe integración con la API de WhatsApp Business. → §3.3.3 para el modelo de protección del número.

**Geolocation API del navegador**

La ubicación del usuario se obtiene exclusivamente mediante `navigator.geolocation.getCurrentPosition()` o `watchPosition()` del navegador. El cliente la envía al servidor como parámetros `lat` y `lng` en las peticiones que la requieren. El servidor no determina la ubicación del usuario por otros medios (no hay geolocalización por IP).

---

#### 3.1.3 Datos Sensibles y sus Fronteras

| Dato sensible                   | Dónde se origina       | Dónde se almacena                                      | Quién puede accederlo                                                                                       |
| ------------------------------- | ---------------------- | ------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------- |
| Número de WhatsApp del vendedor | Onboarding / P-11      | `users.whatsapp_number`                                | Solo el servidor como dato independiente; el cliente solo recibe la URL de contacto construida server-side. |
| Refresh Token                   | Servidor               | `refresh_tokens.token_hash` (hash) + cookie `httpOnly` | Solo el servidor al renovar sesión                                                                          |
| Coordenadas del vendedor        | Navegador del vendedor | `seller_live_locations.location`                       | Solo usuarios autenticados mediante `GET /api/map/sellers`                                                  |
| Correo institucional            | Flujo de autenticación | `users.email`                                          | Solo el propio usuario (campo de solo lectura en UI)                                                        |

---

### 3.2 Vista Lógica — Arquitectura de la Aplicación

Esta vista describe la estructura interna de los dos artefactos del sistema (cliente y servidor), cómo se organizan sus responsabilidades y cómo se comunican entre sí.

---

#### 3.2.1 Arquitectura General

Cima Market sigue una arquitectura cliente-servidor de dos capas con separación estricta de responsabilidades:

- El **cliente** contiene exclusivamente lógica de presentación, gestión de estado de UI, y orquestación de peticiones al servidor. No contiene lógica de negocio ni accede directamente a ningún servicio externo.
- El **servidor** contiene toda la lógica de negocio, autorización, y acceso a servicios externos. Es el único componente que conoce las credenciales de Google OAuth, Cloudinary, y la cadena de conexión a la base de datos.

Esta separación es una decisión de seguridad tanto como de arquitectura: garantiza que ningún dato sensible (números de teléfono, tokens, hashes) pueda ser extraído inspeccionando el bundle del cliente.

---

#### 3.2.2 Estructura del Cliente

El cliente es una SPA construida con React 18 + TypeScript compilada por Vite. Se despliega como archivos estáticos en la CDN de Vercel.

**Capas internas del cliente:**

| Capa                        | Responsabilidad                                                                                                                                                                                              |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Routing**                 | Gestión de rutas del lado del cliente (React Router o equivalente). Implementa los route guards de RF-AUTH-02 y RF-AUTH-04.                                                                                  |
| **Páginas (Pages)**         | Componentes de nivel de ruta. Cada página corresponde a una entrada de §7.3 SRS.                                                                                                                             |
| **Componentes**             | Unidades de UI reutilizables sin lógica de negocio propia.                                                                                                                                                   |
| **Capa de API (API layer)** | Funciones que encapsulan las peticiones HTTP al servidor. Gestiona el adjunto del access token y el reintento silencioso al recibir 401.                                                                     |
| **Gestión de estado**       | Estado global de sesión (usuario autenticado, access token en memoria), campus activo, y notificaciones no leídas.                                                                                           |
| **Service Workers**         | Registrado para capacidades PWA (caché de assets estáticos). No gestiona sincronización de datos en background.                                                                                              |
| **Estilos (Tailwind CSS)**  | Sistema de diseño basado en clases utilitarias. Compilado en tiempo de build por Vite; el bundle de producción incluye únicamente las clases referenciadas en el código. No se usa CSS-in-JS ni módulos CSS. |

**Reglas de la capa de cliente:**

1. El access token (JWT de corta duración → §3.3.1) se almacena únicamente en memoria — nunca en `localStorage` ni `sessionStorage`. Al recargar la página, se recupera ejecutando `POST /api/auth/refresh` antes de renderizar cualquier vista autenticada.
2. El refresh token no es accesible desde JavaScript del cliente — vive exclusivamente en la cookie `httpOnly; Secure; SameSite=Strict`.
3. Los route guards del cliente son la primera línea de protección de UI, pero no son la única — el servidor aplica sus propias validaciones de autorización en cada endpoint.

---

#### 3.2.3 Estructura del Servidor

El servidor es un conjunto de Vercel Serverless Functions con Hono como framework web interno. Toda la API vive en un único entry point (`api/index.ts`) desplegado como una sola función serverless; Hono gestiona el routing interno.

**Capas internas del servidor:**

| Capa                                | Responsabilidad                                                                                                                                                                                                                |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Entry point**                     | `api/index.ts` — registra el middleware global y monta los routers de cada grupo de endpoints.                                                                                                                                 |
| **Middleware de autenticación**     | `requireAuth` — verifica y decodifica el JWT del header `Authorization: Bearer`. Retorna `401` si falta o es inválido.                                                                                                         |
| **Middleware de onboarding**        | `requireOnboarding` — verifica `onboarding_completed = true` en el payload del JWT. Retorna `403` si no se cumple. Se aplica a todos los endpoints autenticados excepto `POST /api/auth/onboarding` y `POST /api/auth/logout`. |
| **Middleware de rol vendedor**      | `requireSeller` — verifica el rol vendedor del usuario. → §3.3.2 para el mecanismo de verificación.                                                                                                                            |
| **Middleware de propietario**       | `requireProductOwner` — verifica que `seller_id` del producto coincida con el `id` del usuario en el JWT. No requiere `is_seller` activo.                                                                                      |
| **Middleware de rol administrador** | `requireAdmin` — verifica que `role = admin` en el payload del JWT. Se aplica a nivel de router sobre todo el grupo `/api/admin`.                                                                                              |
| **Routers**                         | Un router por grupo de endpoints (`/api/auth`, `/api/products`, `/api/users`, etc.). Cada router registra sus propios middlewares específicos.                                                                                 |
| **Handlers**                        | Funciones que implementan la lógica de negocio de cada endpoint: validan el body, interactúan con la base de datos y los servicios externos, y construyen la respuesta.                                                        |
| **Capa de acceso a datos**          | Queries de Drizzle ORM sobre la conexión a Neon. Los handlers nunca construyen SQL crudo — usan el query builder tipado de Drizzle.                                                                                            |
| **Clientes de servicios externos**  | Instancias de los SDKs de Cloudinary y el cliente HTTP para Google OAuth, inicializadas con variables de entorno al arrancar la función.                                                                                       |
| **Configuración de límites**        | `api/config/limits.ts` — constante `PLAN_LIMITS` con los límites por plan de usuario (`max_total_products`, `max_images`).                                                                                                     |

---

#### 3.2.4 Cadena de Middleware por Tipo de Endpoint

La cadena de middleware que se aplica a cada petición depende del tipo de endpoint:

| Tipo de endpoint                      | Middleware aplicado (en orden)                                                      |
| ------------------------------------- | ----------------------------------------------------------------------------------- |
| Público                               | Global                                                                              |
| Autenticado                           | Global → `requireAuth` → `requireOnboarding`                                        |
| Autenticado (sin requerir onboarding) | Global → `requireAuth` (solo `POST /api/auth/onboarding` y `POST /api/auth/logout`) |
| Vendedor autenticado                  | Global → `requireAuth` → `requireOnboarding` → `requireSeller`                      |
| Propietario de publicación            | Global → `requireAuth` → `requireOnboarding` → `requireProductOwner`                |
| Administrador                         | Global → `requireAuth` → `requireOnboarding` → `requireAdmin`                       |

---

#### 3.2.5 Comunicación Cliente-Servidor

Toda comunicación entre cliente y servidor ocurre mediante REST API sobre HTTPS. Los contratos detallados de cada endpoint (método, ruta, acceso, propósito) se encuentran en el Diseño de la Interfaz de API (§4).

**Convenciones aplicadas en todos los endpoints:**

| Convención                      | Detalle                                                                                                                                                                                                      |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Formato de petición             | `Content-Type: application/json` obligatorio en todos los endpoints de escritura (POST, PATCH, DELETE con body).                                                                                             |
| Formato de respuesta            | JSON estructurado en todos los casos, incluyendo errores.                                                                                                                                                    |
| Formato de errores              | `{ "error": "código_snake_case", "message": "descripción legible" }` con el código HTTP apropiado.                                                                                                           |
| Autenticación                   | Header `Authorization: Bearer {access_token}` en todos los endpoints autenticados.                                                                                                                           |
| Renovación silenciosa de token  | Al recibir `401 Unauthorized`, el cliente ejecuta `POST /api/auth/refresh` automáticamente y reintenta la petición original una sola vez. Si el refresh también falla, cierra la sesión y redirige al login. |
| Prevención de caché en contacto | `POST /api/contact/:productId` usa POST en lugar de GET para prevenir que el navegador o proxies intermedios cacheen la respuesta con el enlace de WhatsApp.                                                 |

---

#### 3.2.6 Validación de Variables de Entorno

Al iniciar la función serverless, el servidor valida que todas las variables de entorno críticas estén presentes antes de procesar cualquier petición. Si alguna falta, la función lanza un error en tiempo de inicialización en lugar de fallar silenciosamente en tiempo de ejecución.

Las variables de entorno requeridas se documentan en el archivo `.env.example` del repositorio. Su gestión en producción ocurre mediante el panel de configuración de Vercel.

#### 3.2.7 Estrategia de Testing

El diseño contempla dos niveles de pruebas automatizadas. En el MVP, únicamente las pruebas unitarias (Vitest) se ejecutan en cada Pull Request mediante GitHub Actions como condición de merge a `main`. Las pruebas end-to-end (Playwright) están fuera del alcance del MVP — ver "Alcance en el MVP" más abajo.

| Nivel          | Herramienta | Alcance                                                                                                                                                            | Cobertura mínima requerida                                                                                                                |
| -------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| **Unitario**   | Vitest      | Lógica de negocio del backend: validaciones, flujos de autenticación, reglas de límites de plan, construcción de enlaces de WhatsApp, y lógica de moderación.      | 70% sobre lógica de negocio del backend (→ §6.5 SRS)                                                                                      |
| **End-to-end** | Playwright  | Flujos críticos del usuario sobre el sistema completo desplegado: autenticación, creación de publicación, contacto con vendedor, y flujo de eliminación de cuenta. | Fuera del alcance del MVP (→ "Alcance en el MVP" abajo). Alcance y criterios de cobertura se definirán en la versión donde se implemente. |

**Alcance en el MVP:**
- Vitest cubre exclusivamente la lógica de negocio del backend.
- Las pruebas unitarias de frontend (componentes React) quedan fuera del alcance del MVP.
- Playwright queda fuera del alcance del MVP; se incluye en el stack como intención de diseño para versiones posteriores.

### 3.3 Vista de Seguridad

Esta vista consolida el modelo de seguridad completo del sistema. Su propósito es documentar en un único lugar las decisiones de protección que de otro modo quedarían dispersas entre las vistas de contexto, lógica e interfaz de API. Todo mecanismo descrito aquí tiene su implementación correspondiente referenciada en §4 o §5.

---

#### 3.3.1 Modelo de Autenticación y Gestión de Sesiones

Cima Market delega la verificación de identidad a Google OAuth 2.0, restringida al dominio institucional `@uabc.edu.mx`. Una vez verificada la identidad, el sistema emite y gestiona sus propias credenciales de sesión mediante un esquema de tokens de doble capa (access + refresh), descrito a continuación.


**Flujo de emisión de credenciales:**

1. El cliente redirige al usuario a Google OAuth con `hd=uabc.edu.mx`. Google verifica que el usuario tenga una cuenta activa del dominio institucional.
2. Google redirige al callback del servidor con un código de autorización. El servidor intercambia el código por el perfil del usuario (email verificado) mediante la API de Google.
3. El servidor verifica que el dominio del email sea exactamente `uabc.edu.mx` como segunda línea de validación, independientemente del parámetro `hd`.
4. Si la verificación es exitosa, el servidor emite las credenciales propias del sistema: access token y refresh token.

**Payload del Access Token (JWT):**

```json
{
  "sub": "uuid-del-usuario",
  "display_name": "Nombre Apellido",
  "avatar_url": "https://res.cloudinary.com/...",
  "campus_id": "uuid-del-campus",
  "default_building_id": "uuid-del-edificio-o-null",
  "is_seller": false,
  "plan": "free",
  "onboarding_completed": true,
  "role": "user",
  "iat": 1234567890,
  "exp": 1234567890
}
```

El payload incluye los campos de perfil necesarios para que el cliente opere sin peticiones adicionales tras el login.

**Implicación de caché:** los campos del JWT reflejan el estado del perfil en el momento de emisión. Cambios posteriores (por ejemplo, activar el rol vendedor o cambiar el campus) no se reflejan hasta que el token se renueva (DD-06). Para operaciones que dependen del estado más reciente (como verificar el límite de publicaciones activas), el servidor consulta la base de datos directamente sin confiar en el payload del JWT. `default_building_id` sigue el mismo comportamiento de caché que el resto de campos de perfil del payload — no requiere revalidación contra base de datos, ya que no participa en decisiones de autorización.

**Renovación silenciosa:** al recibir `401 Unauthorized`, el cliente ejecuta `POST /api/auth/refresh` automáticamente usando el refresh token de la cookie. Si el refresh falla, la sesión se cierra y el usuario es redirigido al login. El access token no se rota en cada uso — se emite uno nuevo al expirar o al recibir 401.

| Propiedad                      | Access Token                                      | Refresh Token                                                                  |
| ------------------------------ | ------------------------------------------------- | ------------------------------------------------------------------------------ |
| Vigencia                       | 15 minutos                                        | 30 días                                                                        |
| Almacenamiento en cliente      | Memoria del proceso JS                            | No se almacena                                                                 |
| Accesible desde JS del cliente | Sí                                                | No                                                                             |
| Protección XSS                 | Limitada — expira según vigencia (fila anterior)  | Total                                                                          |
| Protección CSRF                | Total                                             | Altamente inmune                                                               |
| Almacenamiento en servidor     | No se almacena (verificación stateless vía firma) | Hash almacenado en `refresh_tokens` (§5.2), necesario para permitir revocación |
| Revocación                     | Por expiración natural                            | Por logout explícito, suspensión/ban o expiración                              |

**Soporte de múltiples dispositivos:** cada dispositivo tiene su propio registro en `refresh_tokens`. El logout desde un dispositivo revoca únicamente el token de ese dispositivo. Los demás permanecen activos.

---

#### 3.3.2 Modelo de Autorización

La autorización se aplica en capas sucesivas. Ninguna capa sustituye a las demás — todas deben pasar para que una petición sea procesada.

**Capa 1 — Verificación de identidad (`requireAuth`):** Verifica que el header `Authorization: Bearer {token}` contenga un JWT válido, no expirado, y firmado con `JWT_SECRET`. Si falla → `401 Unauthorized`. No verifica permisos, solo identidad.

**Capa 2 — Verificación de onboarding (`requireOnboarding`):** Verifica que `onboarding_completed = true` en el payload del JWT. Previene que un usuario que abandonó el flujo de registro a mitad pueda acceder a endpoints autenticados. Si falla → `403 Forbidden: { "error": "onboarding_required" }`.

**Capa 3 — Verificación de rol vendedor (`requireSeller`):** Verifica que `is_seller = true` consultando el registro del usuario en base de datos en el momento de la petición. No se confía en el valor de `is_seller` del payload del JWT, ya que este puede quedar desactualizado hasta 15 minutos tras una desactivación del rol (→ §3.3.1). Se aplica exclusivamente a los endpoints que requieren ser vendedor para proceder (ej. creación de publicaciones). Si falla → `403 Forbidden: { "error": "seller_role_required" }`.

**Capa 4 — Verificación de propiedad de recurso (`requireProductOwner`):** Verifica que `products.seller_id` del recurso solicitado coincida con el `id` del usuario en el JWT. Se aplica a operaciones de modificación y eliminación de publicaciones e imágenes. No requiere `is_seller` activo — un usuario puede gestionar su contenido aunque haya desactivado el rol vendedor. Si falla → `403 Forbidden: { "error": "not_product_owner" }`.

**Capa 5 — Verificación de rol administrador (inline en handlers):** Verifica que `role = admin` en el payload del JWT. Se aplica mediante middleware en cada endpoint perteneciente al grupo admin. Si falla → `403 Forbidden`.

**Principio de mínimo privilegio:** cada endpoint declara explícitamente el nivel de acceso mínimo requerido. Ningún endpoint asume permisos por defecto. La cadena de middleware garantiza que cada capa se evalúa en orden antes de llegar al handler.

**Doble validación cliente-servidor:** los route guards del cliente son la primera línea de protección de UI, pero no son el único mecanismo. El servidor aplica sus propias validaciones de autorización en cada endpoint, independientemente de lo que el cliente haya verificado. Un atacante que ignore el cliente y llame directamente a la API recibe exactamente la misma respuesta de error que el cliente mostraría.

---

#### 3.3.3 Protección contra Amenazas Comunes

**Cross-Site Request Forgery (CSRF)**

El sistema no implementa tokens CSRF clásicos. La mitigación se logra mediante dos mecanismos complementarios:

- **`SameSite=Strict` en la cookie del refresh token:** el navegador no adjunta la cookie en peticiones originadas desde otro dominio, por lo que un sitio malicioso no puede invocar `POST /api/auth/refresh` con credenciales del usuario.  Adicionalmente, `POST /api/auth/refresh` es el único endpoint que depende de la cookie del refresh token. Incluso en el caso hipotético de un CSRF exitoso contra este endpoint, el impacto es nulo: el access token resultante se devuelve en el cuerpo de la respuesta JSON, que la política Same-Origin del navegador impide que el sitio atacante lea.
- **`Content-Type: application/json` obligatorio en todos los endpoints de escritura:** los formularios HTML externos no pueden enviar JSON de forma nativa. Un atacante que intente un CSRF clásico desde un formulario HTML no podrá satisfacer este requisito. El servidor rechaza cualquier petición de escritura sin este header.
- **Access token en header `Authorization`:** los endpoints autenticados requieren el access token en el header, que un formulario externo no puede adjuntar.

**Cross-Site Scripting (XSS)**

El riesgo de XSS se mitiga en dos niveles:

- **Access token en memoria:** si un script malicioso se inyecta en la aplicación, el access token expira a corta duración (§3.3.1) y no puede ser extraído de ningún almacenamiento persistente.
- **Refresh token en cookie `httpOnly`:** inaccesible desde JavaScript por definición del estándar de cookies. Un script XSS no puede leer ni exfiltrar el refresh token.

El riesgo residual es que un script XSS activo durante la sesión podría hacer peticiones autenticadas en nombre del usuario usando el access token en memoria. Este riesgo se acepta como limitación del modelo de SPA con autenticación en cliente, y se mitiga mediante la corta duración del access token (§3.3.1) y la validación de inputs en servidor.

**Inyección SQL**

Todas las queries se construyen mediante Drizzle ORM con parámetros tipados. No se usa SQL crudo en ningún handler. El ORM serializa y escapa automáticamente todos los valores antes de enviarlos a la base de datos, eliminando la posibilidad de inyección SQL por concatenación de strings.

**Enumeración de recursos**

Todos los identificadores de recursos son UUIDs v4 generados aleatoriamente, no IDs secuenciales. Un atacante no puede inferir la existencia de recursos por incremento de IDs. Adicionalmente, los endpoints de recursos inexistentes o eliminados retornan `404 Not Found` sin exponer si el recurso existió alguna vez.

**Fuerza bruta en autenticación**

Delegada a Google OAuth. El sistema no implementa lógica propia de bloqueo por intentos fallidos de autenticación — Google gestiona internamente la protección contra fuerza bruta sobre sus endpoints de login.

**Extracción masiva de datos de contacto**

El endpoint de contacto aplica controles acumulativos de autenticación, límite de frecuencia y registro de eventos. → §3.3.4 para los valores exactos de rate limiting, → `contact_events` (§5.2) para el registro de eventos.

**Scraping del catálogo**

Los endpoints públicos del catálogo (`GET /api/products`, `GET /api/products/:id`) están sujetos a rate limiting de 100 peticiones por IP por minuto. Las imágenes se sirven desde Cloudinary con transformaciones fijas; un atacante que descargue las URLs de thumbnail no obtiene acceso a los originales sin `cloudinary_public_id` y las credenciales del servidor.

---

#### 3.3.4 Rate Limiting

El rate limiting se aplica por capa de endpoint, no de forma global uniforme.

| Capa de endpoint                                               | Límite                | Criterio      |
| -------------------------------------------------------------- | --------------------- | ------------- |
| Endpoints públicos generales                                   | 100 peticiones/minuto | Por IP        |
| Endpoint de contacto WhatsApp (`POST /api/contact/:productId`) | 20 contactos/hora     | Por `user_id` |

El rate limiting por `user_id` en el endpoint de contacto es más restrictivo y específico que el rate limiting por IP, porque su propósito no es proteger contra DDoS sino prevenir la extracción automatizada de números de WhatsApp por parte de usuarios autenticados.

---

#### 3.3.5 Seguridad en el Manejo de Imágenes

**Moderación automática:** todas las imágenes pasan por el sistema de moderación automática de Cloudinary antes de que la publicación sea creada. Una imagen rechazada cancela la publicación completa y elimina todos los archivos del lote del almacenamiento. No quedan archivos huérfanos en Cloudinary.

**Intermediario obligatorio:** el cliente nunca sube imágenes directamente a Cloudinary. Las credenciales del API de Cloudinary (`CLOUDINARY_API_KEY`, `CLOUDINARY_API_SECRET`) solo existen en el servidor.

**Carga diferida:** las imágenes no se procesan hasta que el usuario confirma explícitamente la publicación. Un usuario que abandone el formulario antes de confirmar no genera ningún archivo almacenado en Cloudinary.

**Rollback garantizado:** si cualquier paso posterior a la subida de imágenes falla (creación de la publicación en base de datos, validación de campos, error del servidor), el servidor ejecuta `cloudinary.uploader.destroy` sobre cada imagen del lote antes de retornar el error. → DD-08.

---

#### 3.3.6 Protección de Datos Personales (LFPDPPP)

El sistema opera bajo la **Ley Federal de Protección de Datos Personales en Posesión de los Particulares (LFPDPPP)** de México. Las decisiones de diseño que afectan el cumplimiento legal se documentan aquí como referencia técnica.

**Datos personales recopilados y su base legal:**

| Dato                        | Momento de recolección                                                                                   | Base legal                                                                                                                | Propósito                                                                                    | Retención                                                                                                                 |
| --------------------------- | -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| Correo institucional        | Inicio del flujo de autenticación (RF-AUTH-03)                                                           | Consentimiento explícito — aceptación de Términos de Uso y Aviso de Privacidad (RF-AUTH-03, P-05)                         | Identificación única del usuario y verificación de pertenencia institucional                 | Anonimizado al eliminar cuenta (RF-AUTH-09); no se borra físicamente para preservar integridad referencial                |
| Nombre de display           | Onboarding (RF-AUTH-04)                                                                                  | Consentimiento explícito — aceptación de Términos de Uso y Aviso de Privacidad                                            | Identificación pública del usuario en el UI de la aplicación                                 | Reemplazado por `"Usuario eliminado"` al eliminar cuenta (RF-AUTH-09)                                                     |
| Foto de perfil              | Configuración de perfil en configuraciones (RF-AUTH-07)                                                  | Consentimiento explícito — acción voluntaria del usuario                                                                  | Identificación visual en el UI de la aplicación                                              | Eliminada físicamente de Cloudinary cuando solicitada (RF-AUTH-09)                                                        |
| Campus principal            | Onboarding (RF-AUTH-04)                                                                                  | Consentimiento explícito — aceptación de Términos de Uso y Aviso de Privacidad                                            | Determinar el contexto geográfico por defecto del catálogo y el mapa                         | Eliminado junto con el registro anonimizado al eliminar cuenta (RF-AUTH-09)                                               |
| Número de WhatsApp          | Onboarding si el usuario elige vender (RF-AUTH-04), o activación posterior del rol vendedor (RF-AUTH-06) | Consentimiento explícito — acción voluntaria del usuario al activar el rol vendedor                                       | Generación del enlace de contacto server-side (RF-WA-01)                                     | Eliminado al eliminar cuenta (RF-AUTH-09)                                                                                 |
| Ubicación habitual de venta | Configuración de perfil (RF-AUTH-07) o formulario de publicación (RF-PUB-01)                             | Consentimiento explícito — acción voluntaria del usuario                                                                  | Filtrado por cercanía en el catálogo (RF-CAT-03) y pre-llenado del formulario de publicación | Eliminado junto con el registro anonimizado al eliminar cuenta (RF-AUTH-09)                                               |
| Coordenadas en tiempo real  | Activación voluntaria del modo "Estoy vendiendo ahora" (RF-GEO-02)                                       | Consentimiento explícito opt-in — el usuario activa el modo manualmente e información clara se muestra antes de activarlo | Mostrar la ubicación del vendedor en el mapa a compradores autenticados (RF-MAP-01)          | Eliminadas automáticamente 90 segundos tras el último ping, o al desactivar el modo, o al eliminar la cuenta (RF-AUTH-09) |

**Derechos del titular y mecanismos de ejercicio:**

El sistema implementa los derechos ARCO (Acceso, Rectificación, Cancelación y Oposición) de la LFPDPPP mediante los siguientes mecanismos:

| Derecho           | Mecanismo                                                                                                                                                                                                 |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Acceso**        | El usuario puede consultar todos sus datos desde P-11 (`/configuracion`) y su historial de moderación desde P-16 (`/configuracion/moderacion`).                                                           |
| **Rectificación** | El usuario puede modificar los datos de su perfil de manera autónoma bajo las condiciones y campos permitidos en el requisito (RF-AUTH-07).                                                               |
| **Cancelación**   | El usuario puede solicitar la eliminación permanente de su cuenta y datos desde P-11, ejecutando el flujo completo de RF-AUTH-09.                                                                         |
| **Oposición**     | El usuario puede desactivar el modo de ubicación en tiempo real en cualquier momento desde P-03 (RF-GEO-02). El número de WhatsApp puede eliminarse desactivando el rol vendedor desde P-11 (RF-AUTH-06). |

**Principios de diseño aplicados para el cumplimiento:**

- **Minimización de datos:** el sistema solicita únicamente los datos estrictamente necesarios para cada funcionalidad. El número de WhatsApp solo se recopila para usuarios que activan el rol vendedor; las coordenadas en tiempo real solo se procesan durante el modo "Estoy vendiendo ahora".
- **Privacidad por diseño:** las coordenadas del vendedor solo son accesibles para usuarios autenticados (RF-GEO-02, §3.1.3).
- **Consentimiento revocable:** toda recolección de datos sensibles (geolocalización en tiempo real, número de WhatsApp) es opt-in y puede revertirse en cualquier momento desde la interfaz sin necesidad de contactar al equipo de soporte.
- **Anonimización sobre borrado físico:** al ejercer el derecho de Cancelación, los datos de identidad se anonimizan en lugar de borrarse físicamente para preservar la integridad referencial del historial de moderación (DD-05), sin exponer datos personales del usuario eliminado.

## 4. Diseño de la Interfaz de API

Esta sección define los contratos de todos los endpoints REST del sistema. Para cada grupo de endpoints se documenta: método HTTP, ruta, nivel de acceso requerido, propósito y notas de implementación relevantes.

Las convenciones globales que aplican a todos los endpoints — formato de petición y respuesta, manejo de errores, autenticación mediante header `Authorization: Bearer`, y renovación silenciosa de tokens — están definidas en §3.2.5 y no se repiten aquí. El nivel de acceso se indica por fila: **Pública** (sin token), **Autenticada** (JWT obligatorio vía `requireAuth` + `requireOnboarding`) o **Admin** (`role = admin` verificado inline en el handler). Los middlewares adicionales de rol se indican en las notas de cada grupo.

El sistema expone 13 grupos de endpoints organizados por dominio funcional:

| Grupo | Prefijo              | Descripción                          |
| ----- | -------------------- | ------------------------------------ |
| §4.1  | `/api/auth`          | Autenticación, sesiones y onboarding |
| §4.2  | `/api/users`         | Perfiles de usuario                  |
| §4.3  | `/api/products`      | Publicaciones                        |
| §4.4  | `/api/categories`    | Catálogo de categorías               |
| §4.5  | `/api/campuses`      | Catálogo de campus                   |
| §4.6  | `/api/contact`       | Contacto WhatsApp                    |
| §4.7  | `/api/reviews`       | Reseñas y calificaciones             |
| §4.8  | `/api/saved`         | Favoritos                            |
| §4.9  | `/api/reports`       | Reportes de usuarios                 |
| §4.10 | `/api/notifications` | Notificaciones in-app                |
| §4.11 | `/api/geo`           | Geolocalización en tiempo real       |
| §4.12 | `/api/map`           | Mapa e infraestructura del campus    |
| §4.13 | `/api/admin`         | Administración y moderación          |

---

### 4.1 Autenticación y Sesiones (`/api/auth`)

| Método | Ruta                        | Acceso                              | Propósito                                                                                                                                                                                         |
| ------ | --------------------------- | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GET    | `/api/auth/google`          | Pública                             | Redirige al flujo de Google OAuth con `hd=uabc.edu.mx`. Genera y almacena un state parameter para prevenir CSRF en el callback.                                                                   |
| GET    | `/api/auth/google/callback` | Pública                             | Recibe el código de Google, lo intercambia por el email verificado, valida el dominio, crea la cuenta si es nueva, emite access token y refresh token. Redirige al onboarding o según RF-AUTH-02. |
| POST   | `/api/auth/onboarding`      | Autenticada (sin requireOnboarding) | Persiste los datos recopilados durante el onboarding (→ RF-AUTH-04) y marca la cuenta como lista para operar. Endpoint autenticado exento del middleware `requireOnboarding`.                     |
| POST   | `/api/auth/refresh`         | Pública                             | Lee el refresh token de la cookie `httpOnly`, verifica su hash contra `refresh_tokens`, y emite un nuevo access token. No rota el refresh token en el MVP.                                        |
| POST   | `/api/auth/logout`          | Autenticada (sin requireOnboarding) | Establece `revoked_at = NOW()` en el registro del refresh token activo del dispositivo actual. Instruye al cliente a eliminar la cookie.                                                          |

**Notas de implementación:**

- El `state` parameter en `/api/auth/google` es un valor aleatorio almacenado en sesión temporal. El callback verifica que el `state` recibido de Google coincida con el generado, previniendo ataques CSRF sobre el flujo OAuth.
- El servidor verifica que `email.endsWith('@uabc.edu.mx')` sobre el email retornado por Google como segunda línea de validación, independiente del parámetro `hd`. Si no coincide → `403 Forbidden: { "error": "domain_not_allowed" }`.
- El callback persiste `terms_accepted_at = NOW()` y `terms_version` (constante de configuración del servidor con la versión vigente) al crear la cuenta, como registro del consentimiento declarado en RF-AUTH-03.

---

### 4.2 Usuarios y Perfiles (`/api/users`)

| Método | Ruta                | Acceso      | Propósito                                                                                                                                                                                                                                                                                                              |
| ------ | ------------------- | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GET    | `/api/users/:id`    | Pública     | Devuelve el perfil público del usuario, incluyendo el campo derivado `selling_now: boolean` calculado a partir del estado activo en `seller_live_locations`.                                                                                                                                                           |
| PATCH  | `/api/users/:id`    | Autenticada | Actualiza los campos editables del perfil propio (RF-AUTH-07). Solo el propietario puede modificar su perfil. Si `campus_id` cambia en la misma petición, `default_building_id` se resetea a NULL.                                                                                                                     |
| DELETE | `/api/users/:id`    | Autenticada | Ejecuta el flujo de anonimización y eliminación → RF-AUTH-09. Requiere `{ "confirm": "DELETE_ACCOUNT" }` en el body como confirmación explícita. Ejecuta el mismo flujo de anonimización que `DELETE /api/admin/users/:id`, pero sin el campo `reason` — la autoeliminación no requiere justificación ante un tercero. |
| POST   | `/api/users/avatar` | Autenticada | Sube la foto de perfil a Cloudinary como intermediario. Si ya existía un avatar, destruye el asset anterior (`cloudinary.uploader.destroy`) antes de confirmar el nuevo. Retorna `200 OK` con la URL transformada.                                                                                                     |

**Notas de implementación:**

- `selling_now` en `GET /api/users/:id` se calcula con `EXISTS (SELECT 1 FROM seller_live_locations WHERE seller_id = :id AND expires_at > NOW())`. No se almacena como campo en `users`. → RF-GEO-02.
- La validación de integridad campus-edificio en `PATCH /api/users/:id`: si `default_building_id` no es NULL, el servidor verifica que `campus_buildings.campus_id = users.campus_id`. Si no coinciden → `422 Unprocessable Entity: { "error": "building_campus_mismatch" }`.

---

### 4.3 Publicaciones (`/api/products`)

| Método | Ruta                                | Acceso                              | Propósito                                                                                                                                                                                                                                                                                                                                                                              |
| ------ | ----------------------------------- | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GET    | `/api/products`                     | Pública                             | Catálogo paginado con soporte de filtros (`campus`, `category`, `min_price`, `max_price`, `min_rating`, `lat`/`lng`), ordenamiento y búsqueda full-text (`q`) (→ RF-CAT-02, RF-CAT-03, RF-CAT-04). `min_rating` filtra sobre `users.average_rating` del vendedor. Si `seller_id` está presente, `status` no se restringe a `active`. Devuelve solo registros con `deleted_at IS NULL`. |
| POST   | `/api/products`                     | Autenticada + `requireSeller`       | Verifica el límite del plan antes de insertar. Requiere `is_seller = true`. → RF-PUB-01, RF-PUB-04.                                                                                                                                                                                                                                                                                    |
| GET    | `/api/products/:id`                 | Pública                             | `200 OK` si `deleted_at IS NULL` (cualquier `status`). `404 Not Found` si `deleted_at IS NOT NULL`.                                                                                                                                                                                                                                                                                    |
| PATCH  | `/api/products/:id`                 | Autenticada + `requireProductOwner` | Actualiza campos o `status`. No requiere `is_seller` activo. → RF-PUB-02, RF-PUB-03.                                                                                                                                                                                                                                                                                                   |
| DELETE | `/api/products/:id`                 | Autenticada + `requireProductOwner` | Soft delete: establece `deleted_at = NOW()`. → RF-PUB-02.                                                                                                                                                                                                                                                                                                                              |
| POST   | `/api/products/images`              | Autenticada + `requireSeller`       | Sube lote de imágenes a Cloudinary como intermediario. Aplica moderación automática. Si alguna imagen es rechazada → `422` con rollback inmediato de todas las del lote. → RF-PUB-06.                                                                                                                                                                                                  |
| DELETE | `/api/products/:id/images/:imageId` | Autenticada + `requireProductOwner` | Elimina imagen en Cloudinary (`cloudinary.uploader.destroy`) y su registro en `product_images`.                                                                                                                                                                                                                                                                                        |

**Notas de implementación:**

- **`requireSeller`:** → §3.3.2, Capa 3.
- **`requireProductOwner`:** verifica que `products.seller_id = jwt.user_id`. Si falla → `403 Forbidden: { "error": "not_product_owner" }`. No requiere `is_seller` activo — permite gestionar publicaciones aunque el rol vendedor esté desactivado.
- **Verificación de límite (`POST /api/products`):** antes de insertar, el servidor verifica que el vendedor no haya alcanzado el máximo de publicaciones activas y pausadas permitidas por su plan (→ RF-PUB-04). Si el límite se alcanzó → `403 Forbidden`.
- **Rollback de imágenes:** si `POST /api/products` falla después de que las imágenes fueron aprobadas por Cloudinary, el servidor ejecuta `cloudinary.uploader.destroy` para cada imagen del lote antes de retornar el error.
- **Validación campus-edificio:** en `POST /api/products` y `PATCH /api/products/:id`, si `building_id` no es NULL, se verifica que `campus_buildings.campus_id = products.campus_id`. Si no coinciden → `422: { "error": "building_campus_mismatch" }`.
- **Búsqueda full-text (`q`):** implementada con índice GIN sobre `to_tsvector('spanish', title || ' ' || description)`. → RF-CAT-02.
- **URLs de imágenes:** → §3.1.2 para la tabla completa de transformaciones y su lógica de derivación.
- **Regla de imagen mínima (`DELETE /api/products/:id/images/:imageId`):** antes de eliminar, el servidor verifica `COUNT(*) FROM product_images WHERE product_id = :id`. Si el resultado es 1, la petición se rechaza con `422 Unprocessable Entity: { "error": "last_image_required" }`.
- **Relación entre `POST /api/products/images` y la persistencia de `product_images`:** este endpoint no inserta filas en `product_images` — `product_images.product_id` es `NOT NULL` y el producto aún no existe en este punto del flujo (→ RF-PUB-06). El endpoint únicamente sube el lote a Cloudinary, aplica moderación, y retorna un arreglo de referencias temporales (`cloudinary_public_id`, `url`, `position`) por cada imagen aprobada. El cliente incluye ese arreglo en el body de `POST /api/products`, que inserta el producto y sus filas en `product_images` en una única transacción. Si `POST /api/products` falla después de recibir las referencias, el servidor ejecuta el rollback descrito en §3.3.5 sobre cada imagen del arreglo antes de retornar el error.

---

### 4.4 Categorías (`/api/categories`)

| Método | Ruta              | Acceso  | Propósito                                                                 |
| ------ | ----------------- | ------- | ------------------------------------------------------------------------- |
| GET    | `/api/categories` | Pública | Devuelve categorías con `is_active = true`, ordenadas por `position ASC`. |

El CRUD de categorías se gestiona desde `/api/admin/categories` (→ §4.13).

---

### 4.5 Campus (`/api/campuses`)

| Método | Ruta            | Acceso  | Propósito                                                                                                         |
| ------ | --------------- | ------- | ----------------------------------------------------------------------------------------------------------------- |
| GET    | `/api/campuses` | Pública | Devuelve campus con `is_active = true`, incluyendo `center_lat`, `center_lng` y `zoom_level` para el mapa (P-04). |

El CRUD de campus se gestiona desde `/api/admin/campuses` (→ §4.13).

---

### 4.6 Contacto WhatsApp (`/api/contact`)

| Método | Ruta                           | Acceso      | Propósito                                                                                                                                                                                                                                                                                                                |
| ------ | ------------------------------ | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| POST   | `/api/contact/:productId`      | Autenticada | Verifica sesión, aplica rate limiting, registra evento de contacto en `contact_events`, construye la URL `https://wa.me/{número}?text={mensaje}` server-side, y la retorna en `{ "url": "..." }`. El número no aparece en ningún endpoint de listado ni de detalle de producto.                                          |
| POST   | `/api/contact-free/:productId` | Autenticada | Verifica sesión, aplica el mismo rate limiting que el contacto automático, registra el evento en `contact_events` (mismo efecto sobre elegibilidad de reseñas que RF-WA-01), y retorna `{ "url": "https://wa.me/{número}" }` **sin** parámetro `text`. El usuario escribe su mensaje libremente en WhatsApp. → RF-WA-02. |

**Notas de implementación:**

- Se usa `POST` en lugar de `GET` para prevenir caché del navegador o proxies intermedios sobre una respuesta que contiene un enlace con el número de WhatsApp.
- Rate limiting por `user_id`. → §3.3.4 para el valor exacto.
- Ambos endpoints son idempotentes ante contacto duplicado: usan `INSERT INTO contact_events ... ON CONFLICT (buyer_id, seller_id, product_id) DO NOTHING`. El enlace se retorna igualmente en ambos casos. → RF-WA-01.
- El mensaje pre-generado de `POST /api/contact/:productId` sigue la plantilla definida en RF-WA-01.

---

### 4.7 Reseñas (`/api/reviews`)

| Método | Ruta                         | Acceso      | Propósito                                                                                                                                                                                                                                                                               |
| ------ | ---------------------------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GET    | `/api/reviews?seller_id=:id` | Pública     | Devuelve reseñas paginadas de un vendedor, con calificación promedio y distribución de estrellas.                                                                                                                                                                                       |
| POST   | `/api/reviews`               | Autenticada | Crea reseña. Verifica elegibilidad: `EXISTS (SELECT 1 FROM contact_events WHERE buyer_id = :reviewer_id AND seller_id = :seller_id)`. Si no existe contacto previo → `403 Forbidden: { "error": "no_prior_contact" }`. → RF-REV-01.                                                     |
| POST   | `/api/reviews/:id/reply`     | Autenticada | Agrega respuesta del vendedor. Si `seller_reply IS NOT NULL` → `409 Conflict: { "error": "already_replied" }`. Solo el vendedor receptor puede responder (verificado contra `reviews.seller_id`). → RF-REV-02.                                                                          |
| DELETE | `/api/reviews/:id`           | Autenticada | Elimina físicamente la reseña (no soft delete). Solo el autor (`reviews.reviewer_id = jwt.user_id`) puede eliminar su propia reseña. Si no coincide → `403 Forbidden: { "error": "not_review_owner" }`. La calificación promedio del vendedor se recalcula inmediatamente. → RF-REV-01. |

**Notas de implementación:**

- La restricción `UNIQUE (reviewer_id, seller_id)` en la tabla `reviews` garantiza a nivel de base de datos que un usuario no puede tener más de una reseña por vendedor. → §5.2.
- La eliminación de reseñas es física (`DELETE FROM reviews WHERE id = :id`), no soft delete, para que la calificación promedio refleje inmediatamente el estado real.
- Reportes huérfanos: al eliminar una reseña (por el autor o por un administrador), el servidor ejecuta `UPDATE reports SET status = 'dismissed', resolved_at = NOW() WHERE target_type = 'review' AND target_id = :reviewId AND status = 'pending'` en la misma operación. Esto evita que reportes pendientes queden referenciando una reseña que ya no existe. `reviewed_by` permanece NULL en estos casos, ya que el cierre es automático y no corresponde a la decisión de un administrador específico.

---

### 4.8 Favoritos (`/api/saved`)

| Método | Ruta                    | Acceso      | Propósito                                                                                                                                                                                                 |
| ------ | ----------------------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GET    | `/api/saved`            | Autenticada | Devuelve productos guardados del usuario autenticado, ordenados por `saved_products.created_at DESC`. Incluye productos con `deleted_at IS NOT NULL` para mostrar estado "Ya no disponible". → RF-FAV-03. |
| POST   | `/api/saved/:productId` | Autenticada | Guarda producto en favoritos. Idempotente: usa `INSERT ... ON CONFLICT (user_id, product_id) DO NOTHING`. No falla si ya estaba guardado. → RF-FAV-01.                                                    |
| DELETE | `/api/saved/:productId` | Autenticada | Elimina producto de favoritos. → RF-FAV-02.                                                                                                                                                               |

---

### 4.9 Reportes (`/api/reports`)

| Método | Ruta           | Acceso      | Propósito                                                                                                                                                                |
| ------ | -------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| POST   | `/api/reports` | Autenticada | Crea reporte sobre publicación, usuario o reseña. Valida combinaciones válidas de `target_type` y `reason` en la capa de API antes de persistir. → RF-MOD-01, RF-MOD-02. |

**Combinaciones válidas de `target_type` y `reason`:**

| `target_type` | `reason` válidos                                                         |
| ------------- | ------------------------------------------------------------------------ |
| `product`     | `inappropriate_content`, `prohibited_item`, `spam_or_duplicate`, `other` |
| `user`        | `misconduct`, `harassment`, `fraud`, `other`                             |
| `review`      | `inappropriate_content`, `other`                                         |

---

### 4.10 Notificaciones (`/api/notifications`)

| Método | Ruta                            | Acceso      | Propósito                                                                                                                                                             |
| ------ | ------------------------------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GET    | `/api/notifications`            | Autenticada | Devuelve notificaciones del usuario en orden cronológico descendente, con filtro de recencia  sobre `created_at` para el feed de P-10.                                |
| GET    | `/api/notifications/moderation` | Autenticada | Devuelve todos los registros de tipo `content_removed` del usuario sin filtro de recencia, ordenados por `created_at DESC`. Alimenta el historial permanente de P-16. |
| PATCH  | `/api/notifications/read-all`   | Autenticada | Establece `read_at = NOW()` en todas las notificaciones con `read_at IS NULL` del usuario autenticado. El cliente lo invoca automáticamente al entrar a P-10.         |

**Notas de implementación:**

- El endpoint `GET /api/notifications` aplica `WHERE created_at > NOW() - INTERVAL '30 days'` para el feed de P-10. Los registros de tipo `content_removed` (con `expires_at = NULL`) permanecen en la base de datos sin límite de tiempo, pero no aparecen en este feed pasados 30 días — sí aparecen en `GET /api/notifications/moderation`.
- El mecanismo UPSERT de notificaciones de proximidad (`seller_nearby`) requiere un índice único parcial sobre `(user_id, payload->>'seller_id')` filtrado a `type = 'seller_nearby'`. Sin este índice el `ON CONFLICT` no tiene restricción sobre la cual operar. → §5.3.
- UPSERT de notificaciones de proximidad: la operación usa `INSERT INTO notifications (...) VALUES (...) ON CONFLICT (user_id, (payload->>'seller_id')) WHERE type = 'seller_nearby' DO UPDATE SET created_at = NOW(), expires_at = NOW() + INTERVAL '30 days', read_at = NULL, payload = EXCLUDED.payload`. Es crítico que el `UPDATE` resetee `read_at = NULL` además de `created_at`: si la fila existente ya había sido leída (`read_at` no nulo) y el conflicto solo actualizara `created_at`, la notificación "revivida" a los 30 minutos seguiría marcada como leída y el badge de no leídas en P-10 nunca se incrementaría para ese evento, violando el comportamiento esperado en RF-GEO-04 (columna "Registro en P-10 → ✓" tras 30 min)
- Por la misma razón, `expires_at` debe reescribirse en cada `UPDATE`: de lo contrario conserva el valor calculado en el INSERT original, y el Cron Job de limpieza (→ §5.4) puede eliminar físicamente la notificación antes de que se cumplan 30 días desde su reactivación más reciente, incumpliendo la retención definida en RF-NOT-01.

---

### 4.11 Geolocalización en Tiempo Real (`/api/geo`)

| Método | Ruta              | Acceso                        | Propósito                                                                                                                                                                                                                                                                   |
| ------ | ----------------- | ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| POST   | `/api/geo/live`   | Autenticada + `requireSeller` | UPSERT en `seller_live_locations` con `campus_id` (el campus donde el vendedor activa el modo), las coordenadas actuales del vendedor y `expires_at = NOW() + INTERVAL '90 seconds'`. Se invoca cada 60 segundos desde el cliente mientras el modo esté activo (RF-GEO-02). |
| DELETE | `/api/geo/live`   | Autenticada + `requireSeller` | Elimina el registro del vendedor en `seller_live_locations`. Desactiva el modo "Estoy vendiendo ahora". → RF-GEO-02.                                                                                                                                                        |
| GET    | `/api/geo/nearby` | Autenticada                   | Recibe `lat` y `lng` del comprador. Identifica vendedores en favoritos del usuario con modo activo (`expires_at > NOW()`) dentro de 200 metros usando `ST_DWithin`. Aplica control de frecuencia de 30 min para registro en `notifications`. → RF-GEO-03, RF-GEO-04.        |

**Notas de implementación:**

- Validación del `featured_product_id` en `POST /api/geo/live`: si no es NULL, el producto debe cumplir simultáneamente `seller_id = jwt.user_id`, `status = 'active'`, `deleted_at IS NULL`, y `campus_id` igual al campus donde se activa el modo. Si alguna condición falla → `422: { "error": "invalid_featured_product" }`.
- La consulta de proximidad usa `ST_DWithin(seller_live_locations.location, ST_SetSRID(ST_MakePoint(:lng, :lat), 4326), 200)` donde el último parámetro es la distancia en metros sobre la proyección geográfica. Requiere el índice GIST sobre `seller_live_locations.location`. → §5.3.

---

### 4.12 Mapa e Infraestructura del Campus (`/api/map`)

| Método | Ruta                                                                      | Acceso      | Propósito                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ------ | ------------------------------------------------------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| GET    | `/api/map/buildings?campus_id=:id`                                        | Pública     | Devuelve edificios y áreas con `is_active = true` para el campus especificado. Usado para renderizar marcadores en P-04 y alimentar el selector de ubicación en P-07. → RF-MAP-02                                                                                                                                                                                                                                                                                                                                                                                                                |
| GET    | `/api/map/sellers?campus_id=:id&category_id=:id&highlight_product_id=:id` | Autenticada | Devuelve vendedores con `expires_at > NOW()` en `seller_live_locations` para el campus especificado, opcionalmente filtrados a quienes tengan al menos una publicación activa en `category_id`. Para cada vendedor incluye: datos del producto destacado (o el más reciente como fallback), lista de hasta 4 productos activos adicionales en ese campus ordenados por `created_at DESC`, y mini tarjeta del vendedor (nombre y calificación promedio). `highlight_product_id` es opcional y prioriza un producto específico como primer elemento de la lista secundaria (RF-GEO-02, RF-MAP-01). |

**Notas de implementación:**

- `GET /api/map/sellers` es autenticado porque la ubicación en tiempo real de los
  vendedores solo es visible para usuarios autenticados de la UABC. → RF-GEO-02, §3.1.3.
- El producto destacado de fallback se obtiene con: `SELECT * FROM products WHERE seller_id = :id AND campus_id = :campus_id AND status = 'active' AND deleted_at IS NULL ORDER BY created_at DESC LIMIT 1`.
- Los productos activos adicionales excluyen el producto destacado y se obtienen con la misma condición limitada a 4 resultados: `SELECT * FROM products WHERE seller_id = :id AND campus_id = :campus_id AND id != :featured_product_id AND status = 'active' AND deleted_at IS NULL ORDER BY created_at DESC LIMIT 4`.
- Si el vendedor no tiene ninguna publicación activa en ese campus en el momento de la consulta (el producto destacado fue pausado o eliminado y no hay fallback), el marcador se incluye en la respuesta sin datos de producto. El cliente renderiza el marcador sin imagen y sin precio.
- `category_id` es opcional. Cuando se especifica, el vendedor solo se incluye en la respuesta si tiene al menos una publicación activa en esa categoría dentro del campus consultado — independientemente de si su producto destacado (`featured_product_id`) pertenece a otra categoría.
- **Deep link desde P-02:** La navegación "Ver en el mapa" (→ RF-MAP-01, P-02) se implementa como convención de query params en la ruta del cliente, análoga a la ya usada para el campus activo (→ RF-CAT-03): `/mapa?campus={campus_slug}&seller={seller_id}&product={product_id}`, usando el mismo slug de campus que RF-CAT-03 (`sauzal` / `valle-dorado`). El cliente resuelve `campus_slug` a `campus_id` (UUID) contra el catálogo de campus ya cargado (`GET /api/campuses`), y reenvía `product_id` como `highlight_product_id` en su llamada a `GET /api/map/sellers?campus_id={campus_id}&highlight_product_id={product_id}`, garantizando que el producto de origen aparezca primero en la lista secundaria del popup. Si el vendedor referenciado no aparece en la respuesta (el modo ya no está activo), el cliente ignora todos los parámetros del deep link y aplica el centrado por defecto en el campus.
- **Parámetro `highlight_product_id` (deep link desde P-02):** Cuando se proporciona, el servidor verifica que el producto pertenezca al vendedor consultado, esté `status = 'active'` y `deleted_at IS NULL` en el campus solicitado. Si el producto coincide con `featured_product_id` (ya es el destacado del vendedor), el parámetro no tiene efecto adicional — el producto ya es visible de forma prominente y no se duplica en la lista secundaria. En cualquier otro caso, si cumple las condiciones anteriores, se coloca como primer elemento de la lista de hasta 4 productos adicionales; el resto se completa con los productos activos restantes ordenados por `created_at DESC` (excluyendo el destacado y el producto priorizado), sin exceder 4 elementos en total. Si el producto no cumple las condiciones (p. ej. fue pausado entre la navegación y la carga del mapa) o el parámetro no se envía, la lista se genera con el ordenamiento por defecto sin priorización.

---

### 4.13 Administración (`/api/admin`)

Todos los endpoints de este grupo requieren `role = admin`, verificado mediante el middleware de administrador.

**Reportes:**

| Método | Ruta                 | Propósito                                                                                   |
| ------ | -------------------- | ------------------------------------------------------------------------------------------- |
| GET    | `/api/admin/reports` | Lista de reportes con filtro por `status` y `target_type`, ordenados por `created_at DESC`. |

**Usuarios:**

| Método | Ruta                                      | Propósito                                                                                                                                                                                                                                     |
| ------ | ----------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GET    | `/api/admin/users`                        | Lista de usuarios con búsqueda por correo o nombre.                                                                                                                                                                                           |
| DELETE | `/api/admin/users/:id`                    | Ejecuta el flujo de eliminación y anonimización de RF-AUTH-09. Requiere `{ "confirm": "DELETE_ACCOUNT", "reason": "..." }` en el body. `reason` (VARCHAR) es obligatorio cuando la eliminación es iniciada por un administrador. → RF-MOD-04. |
| GET    | `/api/admin/users/:id/moderation-history` | Devuelve el historial completo de acciones de moderación sobre la cuenta: tipo de acción, motivo, fecha y administrador responsable, ordenado por `created_at DESC`. → RF-MOD-04, `user_moderation_actions` (§5.2).                           |
| PATCH  | `/api/admin/users/:id`                    | Suspender (requiere `reason` VARCHAR en el body) o reactivar cuenta (`is_active`), o cambiar `role`. Cada suspensión o reactivación se registra como un nuevo evento en el historial de moderación de la cuenta (→ RF-MOD-04).                |

**Notas de implementación (Usuarios):**

- `PATCH /api/admin/users/:id` (suspensión) y `DELETE /api/admin/users/:id` (eliminación): el `reason` recibido, junto con el tipo de acción y `jwt.user_id` del administrador, se inserta como nuevo registro en `user_moderation_actions`. El estado actual de la cuenta (`is_active`, `deleted_at`) se actualiza en la misma operación. → RF-MOD-04, §5.2 `user_moderation_actions`.
- `GET /api/admin/users/:id/moderation-history` devuelve el historial completo de acciones sobre una cuenta específica, ordenado por `created_at DESC`. → RF-MOD-04.

**Publicaciones:**

| Método | Ruta                      | Propósito                                                                                                                                                                                                                        |
| ------ | ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GET    | `/api/admin/products`     | Lista de publicaciones con filtros por `status` y `category_id`.                                                                                                                                                                 |
| PATCH  | `/api/admin/products/:id` | Pausar (`status = 'paused'`) o eliminar (`deleted_at = NOW()`) por moderación. Requiere `reason` (VARCHAR) en el body. Genera una notificación al vendedor (`type = content_removed`, `content_type = 'product'`) con el motivo. |

**Reseñas:**

| Método | Ruta                     | Propósito                                                                                                                                                                                                                                                                                                                                           |
| ------ | ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GET    | `/api/admin/reviews`     | Lista reseñas con filtro por `seller_id` y opcionalmente por número mínimo de reportes (`min_reports`). Incluye el conteo de reportes pendientes por reseña para priorizar la revisión.                                                                                                                                                             |
| DELETE | `/api/admin/reviews/:id` | Elimina físicamente una reseña por moderación. La calificación promedio del vendedor se recalcula inmediatamente. → RF-REV-04. Cierra automáticamente los reportes pendientes que referencien esta reseña (→ §4.7). Genera una notificación al autor de la reseña (type = content_removed, content_type = 'review') con el motivo de la eliminación |

**Categorías:**

| Método | Ruta                        | Propósito                               |
| ------ | --------------------------- | --------------------------------------- |
| GET    | `/api/admin/categories`     | Lista completa (activas e inactivas).   |
| POST   | `/api/admin/categories`     | Crea nueva categoría.                   |
| PATCH  | `/api/admin/categories/:id` | Edita `name`, `position` o `is_active`. |

**Campus:**

| Método | Ruta                      | Propósito                                                 |
| ------ | ------------------------- | --------------------------------------------------------- |
| GET    | `/api/admin/campuses`     | Lista todos los campus incluyendo inactivos.              |
| POST   | `/api/admin/campuses`     | Crea un nuevo campus con sus datos geográficos.           |
| PATCH  | `/api/admin/campuses/:id` | Edita cualquier campo del campus, incluyendo `is_active`. |

**Edificios:**

| Método | Ruta                       | Propósito                                                                             |
| ------ | -------------------------- | ------------------------------------------------------------------------------------- |
| GET    | `/api/admin/buildings`     | Lista edificios de todos los campus, incluyendo inactivos. Filtrable por `campus_id`. |
| POST   | `/api/admin/buildings`     | Crea un nuevo edificio con su campus y coordenadas.                                   |
| PATCH  | `/api/admin/buildings/:id` | Edita `name`, `location` o `is_active`.                                               |

**Anuncios:**

| Método | Ruta                           | Propósito                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ------ | ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GET    | `/api/admin/announcements`     | Lista los anuncios enviados: agrupa `notifications` por `announcement_id` (`GROUP BY announcement_id`, tomando `title`/`message` de `payload` de cualquier fila del grupo y `MIN(created_at)` como fecha de envío), ordenados por `created_at DESC`. El conteo de destinatarios activos se deriva con `COUNT(*) FROM notifications WHERE announcement_id = :id`. Ambos decaen con el tiempo conforme la retención de `notifications` (§5.2) elimina filas — comportamiento intencional. |
| POST   | `/api/admin/announcements`     | Crea anuncio general y lo distribuye como notificación a todos los usuarios activos de la plataforma. Retorna el `announcement_id` del lote y el número de destinatarios. → RF-NOT-03.                                                                                                                                                                                                                                                                                                  |
| DELETE | `/api/admin/announcements/:id` | Retracta anuncio. Elimina físicamente todos los registros en `notifications` con `announcement_id = :id`.                                                                                                                                                                                                                                                                                                                                                                               |

**Métricas:**

| Método | Ruta                 | Propósito                                                                       |
| ------ | -------------------- | ------------------------------------------------------------------------------- |
| GET    | `/api/admin/metrics` | Usuarios registrados, publicaciones activas por categoría, reportes pendientes. |

---

## 5. Diseño de Datos

### 5.1 Estrategia de Persistencia

PostgreSQL serverless (Neon) con extensión PostGIS es el único sistema de persistencia del sistema. No se usa ningún otro mecanismo de almacenamiento de datos estructurados (sin Redis, sin almacenamiento en memoria entre invocaciones, sin archivos locales).

Las imágenes se almacenan en Cloudinary; la base de datos únicamente guarda la URL de transformación de thumbnail y el `cloudinary_public_id` necesario para operaciones de eliminación y derivación de otras URLs.

**Decisiones transversales del esquema:**

| Decisión                                 | Aplicación                                                                                                                                                                                                              |
| ---------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| UUIDs como claves primarias              | La mayoría de tablas usa un campo `id UUID` como PK para evitar enumeración secuencial de recursos vía API.                                                                                                             |
| `TIMESTAMPTZ` para fechas                | Todos los campos de fecha usan zona horaria (`TIMESTAMPTZ`) para evitar ambigüedades en un sistema potencialmente accedido desde distintas zonas.                                                                       |
| Soft delete via `deleted_at`             | En `products` (DD-04) y en `users` (DD-05), donde marca el momento de anonimización y es independiente de `is_active` (usado para suspensión reversible). El resto de eliminaciones son físicas o desactivación lógica. |
| Anonimización en lugar de borrado físico | Solo en `users`. Preserva integridad referencial de tablas que no se eliminan. → §6 (Decisión DD-05).                                                                                                                   |
| ORM tipado (Drizzle)                     | Todas las queries estándar se construyen mediante el query builder tipado de Drizzle ORM                                                                                                                                |

---

### 5.2 Entidades y Esquema

Los campos cuya descripción está vacía son autoexplicativos dado su nombre y tipo. La columna de descripción se reserva para comportamiento no obvio, decisiones de diseño, restricciones de negocio, y casos edge que el nombre del campo y sus restricciones no comunican por sí solos.

#### `campuses`
Catálogo de campus universitarios. Datos estáticos insertados mediante `seed.ts`. Fuente de verdad para coordenadas y zoom del mapa (P-04).

| Campo        | Tipo          | Restricciones          | Descripción                                                      |
| ------------ | ------------- | ---------------------- | ---------------------------------------------------------------- |
| `id`         | UUID          | PK                     |                                                                  |
| `name`       | VARCHAR(100)  | UNIQUE NOT NULL        |                                                                  |
| `slug`       | VARCHAR(50)   | UNIQUE NOT NULL        | Identificador URL-friendly                                       |
| `center_lat` | NUMERIC(10,7) | NOT NULL               | Latitud del centro geográfico para centrar el mapa               |
| `center_lng` | NUMERIC(10,7) | NOT NULL               | Longitud del centro geográfico para centrar el mapa              |
| `zoom_level` | SMALLINT      | NOT NULL DEFAULT 16    | Nivel de zoom inicial del mapa al seleccionar este campus (P-04) |
| `is_active`  | BOOLEAN       | NOT NULL DEFAULT true  | Permite desactivar sin eliminar                                  |
| `created_at` | TIMESTAMPTZ   | NOT NULL DEFAULT NOW() |                                                                  |
| `updated_at` | TIMESTAMPTZ   | NOT NULL DEFAULT NOW() |                                                                  |

---

#### `categories`
Catálogo administrable de categorías de productos. Gestionable por el administrador sin cambios en el código (→ RF-PUB-05, SDD §4.13).

| Campo        | Tipo        | Restricciones          | Descripción                                                                                                                             |
| ------------ | ----------- | ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `id`         | UUID        | PK                     |                                                                                                                                         |
| `name`       | VARCHAR(50) | UNIQUE NOT NULL        | Nombre de la categoría                                                                                                                  |
| `is_active`  | BOOLEAN     | NOT NULL DEFAULT true  | Permite desactivar sin eliminar ni afectar productos existentes                                                                         |
| `position`   | SMALLINT    | NOT NULL UNIQUE        | Orden en el carrusel. UNIQUE garantiza orden determinístico. Valores en múltiplos de 10 para inserciones intermedias sin reorganización |
| `created_at` | TIMESTAMPTZ | NOT NULL DEFAULT NOW() |                                                                                                                                         |
| `updated_at` | TIMESTAMPTZ | NOT NULL DEFAULT NOW() |                                                                                                                                         |

---

#### `campus_buildings`
Catálogo de edificios y áreas de cada campus. Fuente de verdad para ubicaciones habituales de venta y marcadores del mapa.

| Campo        | Tipo                  | Restricciones                             | Descripción                                                                                                                                                            |
| ------------ | --------------------- | ----------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`         | UUID                  | PK                                        |                                                                                                                                                                        |
| `campus_id`  | UUID                  | FK → campuses ON DELETE RESTRICT NOT NULL | Garantiza que edificios de un campus no aparezcan en otro. Borrado físico de campus bloqueado mientras exista al menos un edificio (activo o inactivo) referenciándolo |
| `name`       | VARCHAR(100)          | NOT NULL                                  |                                                                                                                                                                        |
| `location`   | GEOMETRY(POINT, 4326) | NOT NULL                                  | Coordenadas geográficas (PostGIS, WGS 84)                                                                                                                              |
| `is_active`  | BOOLEAN               | NOT NULL DEFAULT true                     | Permite desactivar sin eliminar completamente                                                                                                                          |
| `created_at` | TIMESTAMPTZ           | NOT NULL DEFAULT NOW()                    |                                                                                                                                                                        |
| `updated_at` | TIMESTAMPTZ           | NOT NULL DEFAULT NOW()                    |                                                                                                                                                                        |

---

#### `users`
Registro central de cuentas verificadas. Entidad raíz del sistema.

| Campo                         | Tipo                  | Restricciones                                 | Descripción                                                                                                                                                                                                                                                                                                                                                                       |
| ----------------------------- | --------------------- | --------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                          | UUID                  | PK                                            |                                                                                                                                                                                                                                                                                                                                                                                   |
| `email`                       | VARCHAR(255)          | UNIQUE NOT NULL                               | Correo institucional. Inmutable tras el registro. Se anonimiza en RF-AUTH-09                                                                                                                                                                                                                                                                                                      |
| `display_name`                | VARCHAR(50)           | NULL                                          | NULL hasta completar onboarding                                                                                                                                                                                                                                                                                                                                                   |
| `avatar_url`                  | VARCHAR(500)          | NULL                                          | URL de transformación de avatar en Cloudinary                                                                                                                                                                                                                                                                                                                                     |
| `avatar_cloudinary_public_id` | VARCHAR(300)          | NULL                                          | Requerido para destruir el asset anterior al actualizar o al eliminar cuenta                                                                                                                                                                                                                                                                                                      |
| `campus_id`                   | UUID                  | FK → campuses ON DELETE RESTRICT NULL         | NULL hasta completar onboarding. El borrado físico de un campus queda bloqueado mientras exista al menos un usuario asignado a él.                                                                                                                                                                                                                                                |
| `default_building_id`         | UUID                  | FK → campus_buildings ON DELETE SET NULL NULL | Ubicación habitual del vendedor. Se resetea a NULL si `campus_id` cambia, o si el edificio es eliminado físicamente                                                                                                                                                                                                                                                               |
| `whatsapp_number`             | VARCHAR(20)           | NULL                                          | Formato E.164. NULL hasta activar rol vendedor                                                                                                                                                                                                                                                                                                                                    |
| `plan`                        | VARCHAR(20)           | NOT NULL DEFAULT 'free'                       | Determina los límites. → RF-PUB-04, §3.2.3 (`PLAN_LIMITS`)                                                                                                                                                                                                                                                                                                                        |
| `is_seller`                   | BOOLEAN               | NOT NULL DEFAULT false                        |                                                                                                                                                                                                                                                                                                                                                                                   |
| `role`                        | ENUM(`user`, `admin`) | NOT NULL DEFAULT 'user'                       |                                                                                                                                                                                                                                                                                                                                                                                   |
| `is_active`                   | BOOLEAN               | NOT NULL DEFAULT true                         | `false` indica cuenta suspendida por un administrador (reversible) o eliminada (permanente, junto con `deleted_at IS NOT NULL`). El historial de motivos y fechas de cada suspensión/reactivación se registra en `user_moderation_actions` (→ RF-MOD-04).                                                                                                                         |
| `onboarding_completed`        | BOOLEAN               | NOT NULL DEFAULT false                        | → §3.2.5                                                                                                                                                                                                                                                                                                                                                                          |
| `average_rating`              | NUMERIC(2,1)          | NOT NULL DEFAULT 0                            | Promedio denormalizado de `reviews.rating` para este vendedor. Se recalcula transaccionalmente en cada INSERT/DELETE de reviews (→ RF-CAT-03, RF-REV-01). Evita agregar sobre `reviews` en cada consulta del catálogo.                                                                                                                                                            |
| `review_count`                | SMALLINT              | NOT NULL DEFAULT 0                            | Número de reseñas recibidas. Se incrementa/decrementa junto con `average_rating`. Determina si se muestra "Sin reseñas aún" en P-02/P-03.                                                                                                                                                                                                                                         |
| `created_at`                  | TIMESTAMPTZ           | NOT NULL DEFAULT NOW()                        |                                                                                                                                                                                                                                                                                                                                                                                   |
| `updated_at`                  | TIMESTAMPTZ           | NOT NULL DEFAULT NOW()                        |                                                                                                                                                                                                                                                                                                                                                                                   |
| `deleted_at`                  | TIMESTAMPTZ           | NULL                                          | Marca el momento de anonimización (RF-AUTH-09), sea autoiniciada o ejecutada por un administrador. Distingue una cuenta eliminada (`deleted_at IS NOT NULL`) de una simplemente suspendida (`is_active = false`, `deleted_at IS NULL`). El motivo, si la eliminación fue iniciada por un administrador, se registra en `user_moderation_actions` (→ RF-MOD-04), no en esta tabla. |
| `terms_accepted_at`           | TIMESTAMPTZ           | NULL                                          | Momento de aceptación de Términos de Uso y Aviso de Privacidad (RF-AUTH-03). NULL solo transitoriamente antes de completar el registro.                                                                                                                                                                                                                                           |
| `terms_version`               | VARCHAR(20)           | NULL                                          | Identificador de la versión de Términos/Aviso de Privacidad vigente al momento de la aceptación (ej. `2025-07`). Permite responder qué texto aceptó el usuario si el documento cambia después.                                                                                                                                                                                    |

---

#### `user_moderation_actions`
Historial inmutable de acciones de moderación ejecutadas por un administrador sobre una cuenta de usuario. Permite auditar suspensiones, reactivaciones y eliminaciones a lo largo del tiempo, incluyendo casos de reincidencia. → RF-MOD-04.

| Campo          | Tipo                                    | Restricciones                          | Descripción                                                                                                                                               |
| -------------- | --------------------------------------- | -------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`           | UUID                                    | PK                                     |                                                                                                                                                           |
| `user_id`      | UUID                                    | FK → users ON DELETE RESTRICT NOT NULL | Cuenta afectada. El borrado físico de `users` está bloqueado por diseño (→ DD-05); este historial se preserva sin importar el estado actual de la cuenta. |
| `action`       | ENUM(`suspend`, `reactivate`, `delete`) | NOT NULL                               | Tipo de acción ejecutada.                                                                                                                                 |
| `reason`       | VARCHAR(500)                            | NOT NULL                               | Motivo proporcionado por el administrador en el momento de la acción (→ RF-MOD-03).                                                                       |
| `performed_by` | UUID                                    | FK → users ON DELETE RESTRICT NOT NULL | Administrador que ejecutó la acción.                                                                                                                      |
| `created_at`   | TIMESTAMPTZ                             | NOT NULL DEFAULT NOW()                 |                                                                                                                                                           |

---


#### `refresh_tokens`
Tokens de sesión de larga duración. Permiten renovación silenciosa del access token y soporte de múltiples dispositivos.

| Campo        | Tipo         | Restricciones                          | Descripción                                                                                                                                                                                                                |
| ------------ | ------------ | -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`         | UUID         | PK                                     |                                                                                                                                                                                                                            |
| `user_id`    | UUID         | FK → users ON DELETE RESTRICT NOT NULL | El borrado físico de `users` está bloqueado por diseño (→ DD-05); la única vía de baja es la anonimización. El flujo de RF-AUTH-09 elimina explícitamente las sesiones activas del usuario antes de anonimizar su registro |
| `token_hash` | VARCHAR(100) | NOT NULL                               | Hash del refresh token. Nunca en texto plano                                                                                                                                                                               |
| `expires_at` | TIMESTAMPTZ  | NOT NULL                               | → §3.3.1                                                                                                                                                                                                                   |
| `revoked_at` | TIMESTAMPTZ  | NULL                                   | Establecido por logout explícito. NULL si sesión activa                                                                                                                                                                    |
| `user_agent` | VARCHAR(500) | NULL                                   | Para identificar sesiones activas por dispositivo                                                                                                                                                                          |
| `created_at` | TIMESTAMPTZ  | NOT NULL DEFAULT NOW()                 |                                                                                                                                                                                                                            |

**Estrategia de limpieza:** Cron Job diario elimina registros con `expires_at < NOW() OR revoked_at IS NOT NULL`.

---

#### `seller_live_locations`
Ubicación en tiempo real de vendedores con el modo "Estoy vendiendo ahora" activo. Un registro por vendedor, actualizado por UPSERT cada 60 segundos.

**Nota sobre retención:** `seller_live_locations` no requiere un Cron Job de limpieza. La clave primaria es `seller_id`, por lo que el UPSERT garantiza como máximo una fila por vendedor — la tabla no crece de forma ilimitada con el tiempo, a diferencia de `refresh_tokens` o `notifications`. El único efecto de no limpiar filas expiradas es que la última coordenada de un vendedor inactivo permanece almacenada indefinidamente, aunque sea funcionalmente invisible (`WHERE expires_at > NOW()` la excluye de toda consulta). Se acepta este riesgo de retención como menor dado el volumen acotado (una fila por vendedor) y se documenta explícitamente en cumplimiento del principio de minimización de datos de la LFPDPPP.

| Campo                 | Tipo                  | Restricciones                             | Descripción                                                                                                                                                                                                                                                                              |
| --------------------- | --------------------- | ----------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `seller_id`           | UUID                  | PK, FK → users ON DELETE RESTRICT         | PK garantiza un único registro por vendedor. El borrado físico de `users` está bloqueado por diseño (→ DD-05); el flujo de RF-AUTH-09 elimina explícitamente este registro antes de anonimizar la cuenta                                                                                 |
| `campus_id`           | UUID                  | FK → campuses ON DELETE RESTRICT NOT NULL | Campus donde el vendedor activó el modo. Borrado físico de campus bloqueado mientras exista cualquier registro en esta tabla que lo referencie, incluidos los ya expirados (→ nota de retención de `seller_live_locations`). Necesario para filtrar por campus en `GET /api/map/sellers` |
| `location`            | GEOMETRY(POINT, 4326) | NOT NULL                                  | Coordenadas actuales (PostGIS, WGS 84)                                                                                                                                                                                                                                                   |
| `featured_product_id` | UUID                  | FK → products ON DELETE SET NULL NULL     | NULL si el vendedor no seleccionó ninguna al activar el modo. → RF-GEO-02 para el comportamiento de fallback                                                                                                                                                                             |
| `expires_at`          | TIMESTAMPTZ           | NOT NULL                                  | Si `expires_at < NOW()` el vendedor se considera inactivo. → RF-GEO-02 para el intervalo                                                                                                                                                                                                 |
| `updated_at`          | TIMESTAMPTZ           | NOT NULL                                  | Timestamp del último ping                                                                                                                                                                                                                                                                |

---

#### `products`
Publicaciones creadas por vendedores. Entidad central del marketplace.

| Campo         | Tipo                     | Restricciones                                 | Descripción                                                                                                                                                                                                          |
| ------------- | ------------------------ | --------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`          | UUID                     | PK                                            |                                                                                                                                                                                                                      |
| `seller_id`   | UUID                     | FK → users ON DELETE RESTRICT NOT NULL        | El flujo de RF-AUTH-09 anonimiza al usuario antes de llegar aquí; el borrado físico directo queda bloqueado para preservar el historial de publicaciones                                                             |
| `campus_id`   | UUID                     | FK → campuses ON DELETE RESTRICT NOT NULL     | Pre-poblado con el campus principal del vendedor al crear la publicación, editable. → RF-PUB-01                                                                                                                      |
| `title`       | VARCHAR(100)             | NOT NULL                                      |                                                                                                                                                                                                                      |
| `description` | VARCHAR(600)             | NOT NULL                                      |                                                                                                                                                                                                                      |
| `price`       | NUMERIC(10,2)            | NOT NULL CHECK (price > 0)                    | En MXN                                                                                                                                                                                                               |
| `category_id` | UUID                     | FK → categories ON DELETE RESTRICT NOT NULL   | Borrado físico de categoría bloqueado mientras exista al menos una publicación (activa, pausada o eliminada vía soft delete) que la referencie. Las categorías se desactivan con `is_active = false`, no se eliminan |
| `status`      | ENUM(`active`, `paused`) | NOT NULL DEFAULT 'active'                     | La eliminación se gestiona con `deleted_at`, no con este campo                                                                                                                                                       |
| `building_id` | UUID                     | FK → campus_buildings ON DELETE SET NULL NULL | NULL si el vendedor no especificó ubicación. Si el edificio se elimina físicamente, la ubicación habitual del producto se pierde sin afectar la publicación                                                          |
| `schedule`    | JSONB                    | NULL                                          | Esquema: `{ "days": string[], "start": string, "end": string }`. NULL si no especifica horarios                                                                                                                      |
| `created_at`  | TIMESTAMPTZ              | NOT NULL DEFAULT NOW()                        |                                                                                                                                                                                                                      |
| `updated_at`  | TIMESTAMPTZ              | NOT NULL DEFAULT NOW()                        |                                                                                                                                                                                                                      |
| `deleted_at`  | TIMESTAMPTZ              | NULL                                          | Soft delete. → §5.1, DD-04                                                                                                                                                                                           |

---

#### `product_images`
Imágenes asociadas a publicaciones. Separada de `products` para soportar múltiples imágenes por publicación y permitir reordenamiento independiente sin modificar la entidad principal.

| Campo                  | Tipo          | Restricciones                            | Descripción                                                                                                                                                                                                                                                                       |
| ---------------------- | ------------- | ---------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                   | UUID          | PK                                       |                                                                                                                                                                                                                                                                                   |
| `product_id`           | UUID          | FK → products ON DELETE CASCADE NOT NULL | Las imágenes no tienen existencia independiente del producto. Si el producto se borra físicamente, sus imágenes se eliminan en cascada. En la práctica products usa soft delete (→ DD-04), por lo que esta cascada solo aplica a operaciones administrativas directas sobre la DB |
| `url`                  | VARCHAR(1000) | NOT NULL                                 | URL de transformación de thumbnail almacenada en el momento de la carga. La URL de galería se deriva server-side a partir de `cloudinary_public_id`. → §4.3                                                                                                                       |
| `cloudinary_public_id` | VARCHAR(300)  | NOT NULL                                 | Requerido para eliminar el asset del servicio de almacenamiento y para derivar URLs de otras transformaciones. → §4.3.                                                                                                                                                            |
| `position`             | SMALLINT      | NOT NULL                                 | Orden de visualización. `0` = imagen principal en catálogo                                                                                                                                                                                                                        |
| `created_at`           | TIMESTAMPTZ   | NOT NULL DEFAULT NOW()                   |                                                                                                                                                                                                                                                                                   |

**Restricción:** `UNIQUE (product_id, position)` — garantiza que la imagen principal (position = 0) sea siempre unívoca por publicación.

---

#### `contact_events`
Registro de cada contacto iniciado por un comprador vía WhatsApp. Prerequisito para la elegibilidad de reseñas (→ RF-REV-01) y fuente de métricas de interés por producto en el panel del vendedor.

| Campo        | Tipo        | Restricciones                             | Descripción                                                                                                                                                                                            |
| ------------ | ----------- | ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `id`         | UUID        | PK                                        |                                                                                                                                                                                                        |
| `buyer_id`   | UUID        | FK → users ON DELETE RESTRICT NOT NULL    | El borrado físico de `users` está bloqueado por diseño (→ DD-05); el flujo de RF-AUTH-09 anonimiza en lugar de eliminar, por lo que este evento siempre referencia una fila válida (anonimizada o no). |
| `seller_id`  | UUID        | FK → users ON DELETE RESTRICT NOT NULL    | Misma razón que `buyer_id`.                                                                                                                                                                            |
| `product_id` | UUID        | FK → products ON DELETE RESTRICT NOT NULL | Borrado físico bloqueado por diseño — products usa soft delete (→ DD-04)                                                                                                                               |
| `created_at` | TIMESTAMPTZ | NOT NULL DEFAULT NOW()                    |                                                                                                                                                                                                        |

**Restricción:** `UNIQUE (buyer_id, seller_id, product_id)` — contactos duplicados sobre el mismo producto usan `ON CONFLICT DO NOTHING`. La elegibilidad de reseña se verifica con `EXISTS (SELECT 1 FROM contact_events WHERE buyer_id = X AND seller_id = Y)`, sin restricción por producto.

---

#### `saved_products`
Lista de favoritos de cada usuario. Los registros se conservan aunque el producto sea pausado o eliminado, para preservar el historial del comprador (→ RF-FAV-03).

| Campo        | Tipo        | Restricciones                             | Descripción                                                                                                                                                                                                 |
| ------------ | ----------- | ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `user_id`    | UUID        | FK → users ON DELETE RESTRICT NOT NULL    | El borrado físico de `users` está bloqueado por diseño (→ DD-05). El flujo de RF-AUTH-09 elimina explícitamente los favoritos del usuario antes de anonimizar su registro                                   |
| `product_id` | UUID        | FK → products ON DELETE RESTRICT NOT NULL | Borrado físico bloqueado por diseño — products usa soft delete (→ DD-04). Los favoritos que apuntan a productos con `deleted_at IS NOT NULL` se conservan para mostrar el estado "Ya no disponible" en P-09 |
| `created_at` | TIMESTAMPTZ | NOT NULL DEFAULT NOW()                    |                                                                                                                                                                                                             |

**Restricción:** `PRIMARY KEY (user_id, product_id)` — clave compuesta garantiza unicidad sin campo `id` separado. Esta tabla nunca es referenciada como FK desde otras tablas.

---

#### `reviews`
Reseñas de compradores sobre vendedores. Una reseña evalúa al vendedor, no a un producto específico.

| Campo             | Tipo         | Restricciones                          | Descripción                                                                                                                                                                                                                                                               |
| ----------------- | ------------ | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`              | UUID         | PK                                     |                                                                                                                                                                                                                                                                           |
| `reviewer_id`     | UUID         | FK → users ON DELETE RESTRICT NOT NULL | El borrado físico de `users` está bloqueado por diseño (DD-05). El vínculo con el autor se preserva incluso tras la anonimización — el texto de la reseña se reemplaza por `"[Reseña eliminada]"` en el flujo de RF-AUTH-09, pero el vínculo no se anula (SRS RF-AUTH-09) |
| `seller_id`       | UUID         | FK → users ON DELETE RESTRICT NOT NULL | El borrado físico de `users` está bloqueado por diseño (DD-05). Como el vendedor solo se anonimiza y nunca se elimina físicamente, sus reseñas recibidas se preservan intactas (SRS RF-AUTH-09)                                                                           |
| `rating`          | SMALLINT     | CHECK(1-5) NOT NULL                    |                                                                                                                                                                                                                                                                           |
| `comment`         | VARCHAR(500) | NULL                                   |                                                                                                                                                                                                                                                                           |
| `seller_reply`    | VARCHAR(500) | NULL                                   | NULL si el vendedor no ha respondido. → RF-REV-02.                                                                                                                                                                                                                        |
| `seller_reply_at` | TIMESTAMPTZ  | NULL                                   | Campo independiente de `updated_at` para evitar ambigüedad de timestamps en la UI                                                                                                                                                                                         |
| `created_at`      | TIMESTAMPTZ  | NOT NULL DEFAULT NOW()                 |                                                                                                                                                                                                                                                                           |
| `updated_at`      | TIMESTAMPTZ  | NOT NULL DEFAULT NOW()                 |                                                                                                                                                                                                                                                                           |

**Restricción:** `UNIQUE (reviewer_id, seller_id)` — garantiza que un usuario no puede tener más de una reseña por vendedor.

---

#### `reports`
Reportes enviados por usuarios sobre publicaciones, usuarios o reseñas.

| Campo         | Tipo                                                                                                                | Restricciones                          | Descripción                                                                                                                                                                                                                       |
| ------------- | ------------------------------------------------------------------------------------------------------------------- | -------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`          | UUID                                                                                                                | PK                                     |                                                                                                                                                                                                                                   |
| `reporter_id` | UUID                                                                                                                | FK → users ON DELETE RESTRICT NOT NULL | El borrado físico de `users` está bloqueado por diseño (→ DD-05). El vínculo con el reportante se preserva tras la anonimización, permitiendo trazar patrones de reportes abusivos incluso si la cuenta reportante fue eliminada. |
| `target_type` | ENUM(`product`, `user`, `review`)                                                                                   | NOT NULL                               |                                                                                                                                                                                                                                   |
| `target_id`   | UUID                                                                                                                | NOT NULL                               | No es FK tipada porque referencia tablas distintas según `target_type`                                                                                                                                                            |
| `reason`      | ENUM(`inappropriate_content`, `prohibited_item`, `spam_or_duplicate`, `misconduct`, `harassment`, `fraud`, `other`) | NOT NULL                               |                                                                                                                                                                                                                                   |
| `details`     | VARCHAR(1000)                                                                                                       | NULL                                   | Descripción adicional opcional                                                                                                                                                                                                    |
| `status`      | ENUM(`pending`, `reviewed`, `resolved`, `dismissed`)                                                                | NOT NULL DEFAULT 'pending'             |                                                                                                                                                                                                                                   |
| `reviewed_by` | UUID                                                                                                                | FK → users ON DELETE RESTRICT NULL     | El borrado físico de `users` está bloqueado por diseño (→ DD-05). El vínculo con el administrador que resolvió el reporte se preserva como registro de auditoría interna.                                                         |
| `resolved_at` | TIMESTAMPTZ                                                                                                         | NULL                                   |                                                                                                                                                                                                                                   |
| `created_at`  | TIMESTAMPTZ                                                                                                         | NOT NULL DEFAULT NOW()                 |                                                                                                                                                                                                                                   |

---

#### `notifications`
Notificaciones persistentes generadas por el sistema. El campo `payload` contiene los datos necesarios para renderizar cada tipo sin queries adicionales.

| Campo             | Tipo                                                                               | Restricciones                          | Descripción                                                                                                                    |
| ----------------- | ---------------------------------------------------------------------------------- | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| `id`              | UUID                                                                               | PK                                     |                                                                                                                                |
| `user_id`         | UUID                                                                               | FK → users ON DELETE RESTRICT NOT NULL | RF-AUTH-09 elimina las notificaciones del usuario explícitamente antes de anonimizar su registro. → DD-05                      |
| `type`            | ENUM(`review_received`, `content_removed`, `seller_nearby`, `system_announcement`) | NOT NULL                               |                                                                                                                                |
| `payload`         | JSONB                                                                              | NOT NULL                               | Datos contextuales por tipo (ver tabla de esquemas abajo)                                                                      |
| `announcement_id` | UUID                                                                               | NULL                                   | Identificador de lote para anuncios generales. Permite retractar todos los registros de un envío con una sola operación DELETE |
| `read_at`         | TIMESTAMPTZ                                                                        | NULL                                   | NULL si no leída                                                                                                               |
| `expires_at`      | TIMESTAMPTZ                                                                        | NULL                                   | NULL para `content_removed` (permanente). 30 días desde `created_at` para el resto. → RF-NOT-01                                |
| `created_at`      | TIMESTAMPTZ                                                                        | NOT NULL DEFAULT NOW()                 |                                                                                                                                |

**Esquema de `payload` por tipo:**

| `type`                | Claves del objeto JSON                                                                                                            |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `review_received`     | `{ "reviewer_name": string, "rating": number }`                                                                                   |
| `content_removed`     | `{ "content_type": "product" / "review", "title": string, "reason": string }`                                                     |
| `seller_nearby`       | `{ "seller_id": string, "seller_name": string, "product_title": string, "product_image_url": string, "distance_meters": number }` |
| `system_announcement` | `{ "title": string, "message": string }`                                                                                          |

**Estrategia de limpieza:** Cron Job diario elimina registros con `expires_at IS NOT NULL AND expires_at < NOW()`. Los registros con `expires_at = NULL` (`content_removed`) son permanentes y nunca se eliminan automáticamente. Como consecuencia, el conteo de destinatarios en `GET /api/admin/announcements` (§4.13) decae con el tiempo hasta llegar a 0 — comportamiento intencional.

---

### 5.3 Índices y Consideraciones de Rendimiento

Los índices listados a continuación son requeridos para el funcionamiento correcto del sistema o para cumplir con los requisitos de rendimiento del SRS (→ §6.1 SRS).

**Índices de consultas geoespaciales — PostGIS:**

| Tabla                   | Índice       | Tipo | Motivo                                                                                                           |
| ----------------------- | ------------ | ---- | ---------------------------------------------------------------------------------------------------------------- |
| `campus_buildings`      | `(location)` | GIST | Consultas de distancia contra `products.building_id` para el ordenamiento por cercanía del catálogo (RF-CAT-04). |
| `seller_live_locations` | `(location)` | GIST | Consultas de proximidad con `ST_DWithin` en `GET /api/geo/nearby`                                                |

**Índices de búsqueda full-text:**

| Tabla      | Índice                                                    | Tipo | Motivo                                                            |
| ---------- | --------------------------------------------------------- | ---- | ----------------------------------------------------------------- |
| `products` | `to_tsvector('spanish', title \|\| ' ' \|\| description)` | GIN  | Búsquedas con el parámetro `q` en `GET /api/products` (RF-CAT-02) |

Este índice se implementa como índice de expresión sobre la columna computada, sin necesidad de agregar una columna `tsvector` a la tabla.

**Índices de lectura frecuente:**

| Tabla                     | Índice                                                          | Tipo           | Motivo                                                                                                                     |
| ------------------------- | --------------------------------------------------------------- | -------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `products`                | `(seller_id)`                                                   | B-tree         | Publicaciones por vendedor en P-03                                                                                         |
| `products`                | `(campus_id, status, created_at DESC) WHERE deleted_at IS NULL` | B-tree parcial | Query principal del catálogo (RF-CAT-01)                                                                                   |
| `products`                | `(building_id)`                                                 | B-tree         | JOIN con `campus_buildings` en el ordenamiento por cercanía (RF-CAT-04)                                                    |
| `products`                | `(category_id)`                                                 | B-tree         | Filtro por categoría en `GET /api/products` y en el panel de administración                                                |
| `products`                | `(status)`                                                      | B-tree         | Filtro por estado en `GET /api/products` y en `GET /api/admin/products`                                                    |
| `products`                | `(created_at DESC)`                                             | B-tree         | Ordenamiento por defecto del catálogo (más reciente) cuando no aplica el índice compuesto                                  |
| `reviews`                 | `(seller_id, created_at DESC)`                                  | B-tree         | Query principal de P-03 y P-15 (`GET /api/reviews?seller_id=:id`)                                                          |
| `refresh_tokens`          | `(token_hash)`                                                  | B-tree         | Renovación silenciosa en cada carga de aplicación (`POST /api/auth/refresh`)                                               |
| `refresh_tokens`          | `(user_id)`                                                     | B-tree         | Revocación en logout y eliminación explícita de sesiones al ejecutar RF-AUTH-09                                            |
| `contact_events`          | `(seller_id, product_id)`                                       | B-tree         | Métricas de interés por producto en panel del vendedor (P-03)                                                              |
| `reports`                 | `(target_type, target_id)`                                      | B-tree         | Conteo de reportes por reseña para el umbral de 3+ reportes (RF-REV-04) y filtro `min_reports` en `GET /api/admin/reviews` |
| `users`                   | `(average_rating)`                                              | B-tree         | Filtro `min_rating` en `GET /api/products` (RF-CAT-03)                                                                     |
| `campus_buildings`        | `(campus_id) WHERE is_active = true`                            | B-tree parcial | `GET /api/map/buildings` (renderizado de marcadores por campus)                                                            |
| `user_moderation_actions` | `(user_id, created_at DESC)`                                    | B-tree         | Consulta del historial completo de una cuenta en `GET /api/admin/users/:id/moderation-history` (RF-MOD-04)                 |

**Índices requeridos por el mecanismo de notificaciones de proximidad:**

Estos tres índices son estructuralmente necesarios para el funcionamiento de RF-GEO-04, no solo para rendimiento.

| Tabla           | Índice                                                          | Tipo           | Motivo                                                                                                                          |
| --------------- | --------------------------------------------------------------- | -------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `notifications` | `(user_id, payload->>'seller_id') WHERE type = 'seller_nearby'` | Único parcial  | Habilita el UPSERT de notificaciones de proximidad. Sin este índice el `ON CONFLICT` no tiene restricción sobre la cual operar. |
| `notifications` | `(user_id, created_at DESC) WHERE type = 'seller_nearby'`       | B-tree parcial | Verificación del intervalo de 30 min en cada ciclo de polling                                                                   |
| `notifications` | `(user_id, created_at DESC)`                                    | B-tree         | Query principal de `GET /api/notifications` para renderizar P-10                                                                |
| `notifications` | `(announcement_id) WHERE announcement_id IS NOT NULL`           | B-tree parcial | Localiza y elimina todos los registros de un anuncio en `DELETE /api/admin/announcements/:id`                                   |

Todos estos índices deben crearse en la migración inicial de la base de datos.

---

### 5.4 Estrategia de Limpieza de Datos (Cron Jobs)

El sistema implementa dos Cron Jobs ejecutados mediante Vercel Cron, programados en `vercel.json`. Cada uno invoca un endpoint interno protegido del servidor.

| Job                          | Frecuencia | Operación                                                                       |
| ---------------------------- | ---------- | ------------------------------------------------------------------------------- |
| Limpieza de `refresh_tokens` | Diaria     | `DELETE FROM refresh_tokens WHERE expires_at < NOW() OR revoked_at IS NOT NULL` |
| Limpieza de `notifications`  | Diaria     | `DELETE FROM notifications WHERE expires_at IS NOT NULL AND expires_at < NOW()` |

---

## 6. Decisiones de Diseño Significativas

Esta sección registra las decisiones técnicas no obvias tomadas durante el diseño, incluyendo el contexto que las motivó, las alternativas evaluadas y la justificación de la opción elegida. Su propósito es prevenir que decisiones correctas sean revertidas en el futuro por falta de contexto.

---

### DD-01 — Hono sobre Express como framework del servidor

**Contexto:** El servidor se despliega como Vercel Serverless Functions bajo el runtime de Node.js. Se necesita un framework web que gestione routing, middleware y tipado.

**Alternativas evaluadas:**

| Alternativa                                | Razón de descarte                                                                                                                                                                                                |
| ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Express.js                                 | Diseñado para servidores persistentes con manejo de conexiones de larga duración. Su modelo de middleware no está optimizado para funciones efímeras y su ecosistema de tipos es retrocompatible pero no nativo. |
| Fastify                                    | Excelente rendimiento pero orientado a servidores persistentes. Mayor overhead de configuración para entornos serverless.                                                                                        |
| Sin framework (handlers nativos de Vercel) | Viable pero requiere implementar routing, parsing de body, y manejo de errores desde cero, sin beneficio justificable.                                                                                           |

**Decisión:** Hono. Framework TypeScript-first diseñado explícitamente para entornos serverless y edge. Provee routing, middleware tipado y un bundle mínimo (~15 KB) sin el overhead de frameworks diseñados para servidores persistentes. Compatible nativamente con el runtime de Node.js de Vercel.

---

### DD-02 — Un único entry point serverless en lugar de una función por ruta

**Contexto:** Vercel permite desplegar cada archivo en `api/` como una función serverless independiente, o redirigir todo el tráfico a un único entry point con routing interno.

**Alternativas evaluadas:**

| Alternativa                                                    | Razón de descarte                                                                                                                                                                                                                            |
| -------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Una función por ruta (`api/users.ts`, `api/products.ts`, etc.) | Aumenta el cold start total del sistema (cada función se inicializa de forma independiente). El middleware global (autenticación, logging) debe replicarse en cada función o extraerse a un módulo compartido sin garantías de consistencia. |

**Decisión:** Un único entry point (`api/index.ts`) con routing interno gestionado por Hono. Reduce la superficie de cold starts, centraliza el middleware global, y simplifica la gestión de errores. La configuración en `vercel.json` redirige todo el tráfico `/api/*` a este entry point.

---

### DD-03 — Google OAuth con restricción de dominio institucional como mecanismo de autenticación

**Contexto:** Los usuarios se identifican mediante su correo institucional `@uabc.edu.mx`. Se necesita un mecanismo de autenticación que valide la pertenencia a la institución sin requerir infraestructura propia de verificación de identidad.

**Alternativas evaluadas:**

| Alternativa                           | Razón de descarte                                                                                                                                                                                                                                                                                                                                                                                                             |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Correo + contraseña                   | Añade fricción de registro y recuperación de contraseña. No verifica pertenencia institucional — cualquiera podría registrarse con cualquier correo.                                                                                                                                                                                                                                                                          |
| OTP por correo (Resend)               | Requiere infraestructura propia de envío de correo (Resend), tabla `otp_tokens` con lógica de bloqueo por fuerza bruta, y rate limiting de autenticación. En móvil con PWA, el usuario debe alternar entre la app y el cliente de correo para copiar el código. La UABC usa Google Workspace, por lo que Google ya actúa como verificador de identidad institucional — duplicar esa verificación con OTP no agrega seguridad. |
| OAuth institucional propio de la UABC | Requeriría que la UABC desarrolle y mantenga su propio proveedor OAuth. No disponible.                                                                                                                                                                                                                                                                                                                                        |
| Magic link por correo                 | Funcionalmente equivalente al OTP en implementación y comparte las mismas desventajas en móvil: tocar el enlace en el correo interrumpe el flujo de la PWA en iOS al abrir una pestaña externa.                                                                                                                                                                                                                               |

**Decisión:** Google OAuth 2.0 con el parámetro `hd=uabc.edu.mx`, que restringe el login exclusivamente a cuentas del dominio institucional. Google verifica la pertenencia a la institución como parte del flujo de autenticación estándar, sin infraestructura adicional.

**Ventajas sobre OTP:**
- Elimina Resend como dependencia de criticidad alta.
- El rate limiting y la protección contra fuerza bruta los gestiona Google internamente.
- Experiencia de usuario en móvil superior: un tap en el selector de cuenta de Google en lugar de alternar entre apps para copiar un código.
- Gratuito sin límite de usuarios (Google Cloud, nivel gratuito permanente).

**Lo que no cambia:** el esquema de sesiones de doble token (access + refresh), el flujo de onboarding, y toda la lógica de negocio posterior a la autenticación permanecen idénticos. Google OAuth reemplaza únicamente el mecanismo de verificación de identidad inicial — el resto del sistema no se ve afectado.

**Variables de entorno requeridas:** `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`. 

---

### DD-04 — Soft delete en publicaciones mediante `deleted_at`

**Contexto:** Cuando un vendedor o un administrador elimina una publicación, el sistema necesita decidir si borra el registro físicamente o lo marca como eliminado.

**Alternativas evaluadas:**

| Alternativa               | Razón de descarte                                                                                                                                                                        |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Borrado físico inmediato  | Rompe la integridad referencial de `contact_events` y `saved_products`, que referencian `product_id`. Requeriría CASCADE que eliminaría historial de contacto relevante para moderación. |
| Tabla de archivo separada | Mayor complejidad de queries; requiere mover el registro a otra tabla en lugar de actualizar un campo.                                                                                   |

**Decisión:** Soft delete mediante `deleted_at TIMESTAMPTZ NULL`. Las queries públicas filtran siempre con `WHERE deleted_at IS NULL`. Los registros eliminados permanecen accesibles para moderación y se mantiene la integridad referencial. Esto también permite que `saved_products` conserve referencias a productos eliminados para mostrar el estado "Ya no disponible".

---

### DD-05 — Anonimización en lugar de borrado físico de cuentas de usuario

**Contexto:** El SRS requiere cumplir con el derecho de cancelación de la LFPDPPP (RF-AUTH-09). Al eliminar una cuenta, el sistema debe decidir cómo tratar el registro de `users`.

**Alternativas evaluadas:**

| Alternativa                        | Razón de descarte                                                                                                                                                                    |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Borrado físico del registro        | Rompe la integridad referencial de `contact_events` y `reports`, que referencian `users` y deben conservarse para el historial de moderación.                                        |
| Borrado físico con SET NULL en FKs | Haría anónimos los registros de moderación pero perdería la capacidad de rastrear patrones (ej: una cuenta que fue baneada múltiples veces con el mismo correo no sería detectable). |

**Decisión:** Anonimización del registro de `users`: el email se reemplaza por un valor aleatorio no recuperable, el nombre por "Usuario eliminado", la foto se elimina físicamente de Cloudinary, y el número de WhatsApp se elimina. El registro en sí permanece con `is_active = false`. Esto preserva la integridad referencial de las tablas de moderación sin exponer datos personales del usuario eliminado.

**Nota de implementación — consistencia entre FKs y el flujo de eliminación:** dado que el registro de `users` nunca se borra físicamente, todas las FKs hacia `users` en tablas dependientes usan `ON DELETE RESTRICT` como red de seguridad: cualquier intento accidental de ejecutar un `DELETE FROM users` (script, migración, consola SQL) falla de forma explícita en lugar de propagar un borrado o anulación silenciosa. La limpieza real de datos asociados a una cuenta (`refresh_tokens`, `notifications`, `saved_products`, `product_images`) al ejecutar RF-AUTH-09 se realiza mediante sentencias `DELETE` explícitas en el propio flujo de aplicación, no mediante `ON DELETE CASCADE`. Las publicaciones del usuario (`products`) no se eliminan físicamente en este flujo — reciben soft delete (`deleted_at = NOW()`), consistente con DD-04. Las `reviews` recibidas por un vendedor **no** se eliminan en este flujo, y el vínculo del autor (`reviewer_id`) tampoco se anula — se preserva, ya que el usuario solo queda anonimizado, no eliminado.

---

### DD-06 — Access token en memoria del cliente

**Contexto:** El access token (JWT de corta duración §3.3.1) necesita estar disponible para adjuntarse en cada petición autenticada. Se necesita decidir dónde almacenarlo en el cliente.

**Alternativas evaluadas:**

| Alternativa        | Razón de descarte                                                                                                                       |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| `localStorage`     | Accesible desde JavaScript. Vulnerable a ataques XSS: cualquier script inyectado puede leer el token y suplir la identidad del usuario. |
| `sessionStorage`   | Misma vulnerabilidad XSS que `localStorage`. Adicionalmente, se pierde al cerrar la pestaña, degradando la experiencia de usuario.      |
| Cookie no-httpOnly | Accesible desde JavaScript. Misma vulnerabilidad XSS. Sin ventaja sobre `localStorage`.                                                 |

**Decisión:** El access token se almacena en memoria del cliente (variable de módulo en el estado global de la aplicación). Al recargar la página, se recupera automáticamente ejecutando `POST /api/auth/refresh` antes de renderizar cualquier vista autenticada (silent refresh). El refresh token, de mayor duración, se almacena en una cookie `httpOnly; Secure; SameSite=Strict`, inaccesible desde JavaScript.

---

### DD-07 — Número de WhatsApp gestionado exclusivamente server-side

**Contexto:** Los compradores necesitan contactar a los vendedores vía WhatsApp. Se necesita decidir cómo se construye el enlace de contacto y qué información se expone al cliente.

**Alternativas evaluadas:**

| Alternativa                                             | Razón de descarte                                                                                                                                |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Número incluido en el payload de detalle de producto    | Expone el número en endpoints públicos sin autenticación, facilitando la extracción masiva sin ningún control.                                   |
| Número incluido en los payloads de listado del catálogo | Endpoints públicos que devuelven múltiples registros en una sola petición, permitiendo extraer todos los números del sistema con pocas llamadas. |

**Decisión:** El servidor construye la URL completa de WhatsApp internamente y la retorna únicamente a través del endpoint de contacto, que requiere autenticación verificada y aplica rate limiting por usuario. El número nunca aparece en endpoints públicos ni en payloads de listado. La URL resultante contiene el número embebido pero no como campo estructurado y parseable independientemente — su único uso funcional es ser abierta directamente.

---

### DD-08 — Cloudinary como servicio de imágenes con el servidor como intermediario obligatorio

**Contexto:** Los vendedores necesitan subir imágenes de sus productos. Se necesita decidir dónde almacenarlas y cómo gestionar la carga.

**Alternativas evaluadas:**

| Alternativa                                   | Razón de descarte                                                                                                                                                                                                                                                |
| --------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Almacenamiento propio (Vercel Blob, S3, etc.) | Requiere implementar manualmente optimización de imágenes, conversión de formatos, moderación de contenido y gestión de almacenamiento. Cloudinary resuelve todo esto como servicio, reduciendo significativamente la complejidad de implementación para el MVP. |
| Carga directa del cliente a Cloudinary        | Expone las credenciales de Cloudinary en el bundle del cliente. Cualquier usuario podría subir archivos ilimitados a la cuenta del sistema sin autenticación ni rate limiting.                                                                                   |

**Decisión:** Cloudinary como servicio de imágenes, con el servidor actuando como intermediario obligatorio en todas las cargas. El servidor controla autenticación, moderación, rollback y rate limiting. Las credenciales de Cloudinary nunca abandonan el servidor.

---

### DD-09 — Vitest y Playwright como stack de testing

**Contexto:** El sistema requiere una cobertura mínima del 70% sobre la lógica de
negocio del backend (→ §6.5 SRS). Se necesitan herramientas de pruebas unitarias y
end-to-end compatibles con el stack tecnológico del proyecto (Vite + TypeScript +
Node.js).

**Alternativas evaluadas:**

| Alternativa | Tipo       | Razón de descarte                                                                                                                                                                                                                          |
| ----------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Jest        | Unitario   | Diseñado para CommonJS. Requiere configuración adicional de transformadores (`ts-jest`, `babel-jest`) para funcionar con proyectos Vite + ESModules, generando inconsistencias con la resolución de rutas que Vite maneja automáticamente. |
| Mocha       | Unitario   | Framework de bajo nivel que requiere configurar assertions, mocks y cobertura por separado. Mayor overhead de setup sin beneficio justificable sobre Vitest para este proyecto.                                                            |
| Cypress     | End-to-end | Soporte nativo limitado a Chromium. Safari requiere versión experimental, lo cual es relevante para una PWA que debe funcionar en iOS Safari. Tiene limitaciones históricas con múltiples pestañas y navegación compleja.                  |

**Decisión:** Vitest para pruebas unitarias del backend y Playwright para pruebas end-to-end.

Vitest comparte la configuración de Vite del proyecto sin transformadores adicionales, lo que garantiza que el entorno de pruebas sea consistente con el entorno de ejecución real. Su API es compatible con Jest, por lo que la documentación y recursos de la comunidad de Jest son aplicables sin cambios.

Playwright corre en Chromium, Firefox y Safari con el mismo código de prueba, lo cual es relevante para verificar el comportamiento en iOS Safari. Maneja de forma nativa flujos asíncronos complejos como los que involucran el callback de OAuth, navegación entre rutas protegidas, e interacción con el mapa.

---

### DD-10 — Tabla de historial dedicada para acciones de moderación sobre usuarios

**Contexto:** RF-MOD-04 requiere conservar el historial completo de suspensiones, reactivaciones y eliminaciones sobre una cuenta, incluyendo motivo, fecha y administrador responsable — no solo el evento más reciente, ya que una cuenta puede suspenderse y reactivarse más de una vez.

**Alternativas evaluadas:**

| Alternativa                                                 | Razón de descarte                                                                                                                                                                                                                     |
| ----------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Columnas `suspension_reason` / `deletion_reason` en `users` | Una columna simple solo retiene el motivo más reciente. Una cuenta suspendida, reactivada, y suspendida de nuevo perdería silenciosamente el motivo de la primera suspensión, incumpliendo el historial que exige RF-MOD-04.          |
| Notificación `content_removed` dirigida al usuario afectado | RF-NOT-01 enumera explícitamente los eventos que generan notificación in-app; la moderación sobre la propia cuenta no está en esa lista. Además, una notificación no es consultable como historial estructurado por un administrador. |

**Decisión:** Tabla `user_moderation_actions` (→ §5.2), de solo inserción (append-only), con una fila por cada acción de moderación ejecutada sobre una cuenta. `users` conserva únicamente el estado actual (`is_active`, `deleted_at`) para checks rápidos en el hot path de autenticación y listados; la tabla de historial resuelve exclusivamente la pregunta de auditoría ("qué pasó, cuándo, por qué, quién lo hizo"), consultada solo desde el panel de administración.

**Relación con DD-05:** dado que `users` nunca se borra físicamente (→ DD-05), `user_moderation_actions.user_id` usa `ON DELETE RESTRICT` como el resto de FKs hacia `users`, preservando el historial de moderación incluso después de que la cuenta referenciada sea anonimizada.

---

## Apéndices

### A. Variables de Entorno

Las siguientes variables de entorno son requeridas para el funcionamiento del servidor. Se gestionan mediante Vercel Environment Variables en producción y staging, y mediante un archivo `.env` local en desarrollo. El archivo `.env.example` en el repositorio lista todas las variables sin valores.

| Variable                   | Servicio     | Propósito                                                                                                                               |
| -------------------------- | ------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| `DATABASE_URL`             | Neon         | Cadena de conexión a PostgreSQL serverless. Incluye el pooler de conexiones de Neon.                                                    |
| `JWT_SECRET`               | Propio       | Secreto para firmar y verificar los access tokens (JWT). Mínimo 256 bits de entropía.                                                   |
| `JWT_EXPIRES_IN`           | Propio       | Duración del access token. Valor esperado: `15m`.                                                                                       |
| `REFRESH_TOKEN_SECRET`     | Propio       | Secreto para generar y hashear los refresh tokens.                                                                                      |
| `REFRESH_TOKEN_EXPIRES_IN` | Propio       | Duración del refresh token. Valor esperado: `30d`.                                                                                      |
| `CLOUDINARY_CLOUD_NAME`    | Cloudinary   | Identificador de la cuenta de Cloudinary.                                                                                               |
| `CLOUDINARY_API_KEY`       | Cloudinary   | Clave pública de la API de Cloudinary.                                                                                                  |
| `CLOUDINARY_API_SECRET`    | Cloudinary   | Clave secreta de la API de Cloudinary. Nunca expuesta al cliente.                                                                       |
| `GOOGLE_CLIENT_ID`         | Google Cloud | Client ID de la aplicación OAuth registrada en Google Cloud Console en Google Cloud Console.                                            |
| `GOOGLE_CLIENT_SECRET`     | Google Cloud | Client Secret de la aplicación OAuth. Nunca expuesto al cliente.                                                                        |
| `CRON_SECRET`              | Propio       | Token de autorización para los endpoints internos invocados por los Cron Jobs de Vercel. Previene invocaciones externas no autorizadas. |