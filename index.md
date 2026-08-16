---
layout: default
title: Inicio
nav_order: 1
description: "Documentacion del microservicio de autenticación de SocioUnido"
---

# Microservicio de autenticación

Microservicio encargado de la gestión de identidad, control de acceso, roles y perfiles de usuario de "SocioUnido".

## Utilidad y funcionalidad

El microservicio de autenticación está diseñado para manejar las siguientes responsabilidades clave:

* **Gestión de identidad y seguridad:** Administra el registro, inicio de sesión y validación de credenciales delegando la capa de máxima seguridad a proveedores robustos (Firebase), garantizando la protección de los datos sensibles de los socios.
* **Control de autorización y roles:** Emite y valida tokens JWT, estableciendo qué nivel de acceso y permisos tiene cada usuario dentro de la plataforma (ej. administrador, socio activo, moroso).
* **Orquestación del perfil del socio:** Actúa como nexo para recuperar información del club asociada al usuario logueado (como instalaciones reservadas o disciplinas inscriptas), consolidando su perfil para el frontend.

## ¿Qué vas a encontrar en esta página?

A continuación, se detalla toda la información técnica, arquitectónica y organizativa sobre esta implementación en particular:

* 🔌 **[Endpoints](endpoints.html):** Documentación estática y detallada de la API, ideal para consultar integraciones.
* 🛠️ **[Justificación tecnológica](justificacion.html):** El porqué de los lenguajes y frameworks elegidos, nuestro pipeline de CI/CD, la estrategia de testing y métricas de Code Coverage definidas.
* 🏗️ **[Arquitectura y diagramas](diagramas.html):** Representación visual de la arquitectura del microservicio utilizando el modelo C4.
* 📊 **[Métricas de la implementación](metricas.html):** Estadísticas del desarrollo, cantidad de commits, Pull Requests y distribución del trabajo en el equipo.
