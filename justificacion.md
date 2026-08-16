---
layout: default
title: Justificación tecnológica
nav_order: 3
---

# 🛠️ Justificación tecnológica

En esta sección documentamos las decisiones técnicas tomadas para la construcción del microservicio de autenticación, asegurando que cada herramienta elegida aporte valor real al desarrollo y mantenimiento del producto.

## Lenguajes y frameworks

Para este microservicio, crítico para la seguridad de la plataforma, la selección de nuestra pila tecnológica se basó en la robustez y los estándares de la industria:

* **Python:** Elegido por su legibilidad, extensa librería estándar y gran soporte para integraciones criptográficas y de seguridad.
* **FastAPI:** Seleccionado por su altísimo rendimiento y su validación estricta de datos (mediante Pydantic). Su autogeneración de documentación interactiva (Swagger/OpenAPI) facilita enormemente la integración con los clientes web y móviles.
* **Firebase Authentication:** Implementado para delegar la gestión del ciclo de vida de las contraseñas, recuperación de cuentas y emisión de tokens seguros. Esto nos exime de almacenar contraseñas en texto plano y eleva el nivel de seguridad de la plataforma.
* **SQLAlchemy:** Utilizado para gestionar el almacenamiento relacional de los perfiles de usuario y la jerarquía de roles de manera eficiente y escalable.
* **Pytest:** Nuestro framework de pruebas para garantizar que las validaciones de tokens y la asignación de permisos no presenten fisuras de seguridad antes de cualquier despliegue.
* **Docker y Docker Compose:** La contenerización es indispensable en nuestra arquitectura. Nos permite aislar el microservicio y garantizar la paridad exacta entre entornos (desarrollo, *staging* y producción).

## Integración y despliegue continuo (CI/CD)

La implementación de pipelines de CI/CD es fundamental en el microservicio para garantizar entregas ágiles y seguras. Nos permite automatizar la ejecución de pruebas y el despliegue a los distintos entornos, reduciendo el error humano y acelerando el *time-to-market*.

## Pruebas unitarias y Code Coverage

Para asegurar la robustez y estabilidad del código, mantenemos un estándar estricto de calidad:

* Se ha implementado una gran cantidad de pruebas unitarias cubriendo los flujos de autenticación, validación de roles y casos borde de denegación de servicio.
* Mantenemos un **estricto nivel de Code Coverage** (cobertura de código) fijado en un mínimo del **90%**, el cual es validado automáticamente en cada Pull Request mediante nuestro pipeline.

## Documentación integral

Utilizamos **JustTheDocs** para mantener esta documentación viva, versionada junto con el código y fácilmente accesible para cualquier miembro del equipo. Esto centraliza el conocimiento y reduce los cuellos de botella en la comunicación.
