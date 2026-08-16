---
layout: default
title: Endpoints
nav_order: 2
---

# 🔌 Endpoints

En esta sección se listan los endpoints disponibles en el microservicio de autenticación.

Al actuar como orquestador de identidad, esta API expone rutas para el login, registro y control de permisos, así como accesos delegados a otros módulos del club.

## Autenticación y usuarios

<details>
  <summary style="font-size: 1.1em; cursor: pointer; padding: 10px; background-color: #f8f9fa; border-radius: 4px; border-left: 4px solid #007bff; margin-bottom: 5px;">
    <strong style="color: #007bff;">GET</strong> <code>/api/v1/auth/health</code> - Health Check
  </summary>
  <div style="padding: 15px; border: 1px solid #f8f9fa; border-top: none; margin-bottom: 20px;">
    <p><strong>ID de la Operación:</strong> <code>health_check_api_v1_auth_health_get</code></p>
    <p>Endpoint para verificar que el microservicio está funcionando correctamente.</p>
    <h3>Respuestas</h3>
    <p><strong>Código:</strong> <code>200 OK</code></p>
    <div class="language-json highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="p">{}</span>
</code></pre></div></div>
  </div>
</details>

<details>
  <summary style="font-size: 1.1em; cursor: pointer; padding: 10px; background-color: #f8f9fa; border-radius: 4px; border-left: 4px solid #28a745; margin-bottom: 5px;">
    <strong style="color: #28a745;">POST</strong> <code>/api/v1/auth/registrar</code> - Registrar Usuario
  </summary>
  <div style="padding: 15px; border: 1px solid #f8f9fa; border-top: none; margin-bottom: 20px;">
    <p><strong>ID de la Operación:</strong> <code>registrar_usuario_api_v1_auth_registrar_post</code></p>
    <p>Registra un nuevo usuario administrativo. Ejecuta una Saga: crea el usuario en Firebase Auth, lee permisos de la DB, setea custom claims, impacta en <code>ms-club</code> y realiza rollback en caso de falla.</p>
    <h3>Parámetros</h3>
    <ul>
      <li><strong>Header:</strong> <code>x-internal-secret</code> (Requerido)</li>
    </ul>
    <h3>Cuerpo de la Petición (Request Body)</h3>
    <div class="language-json highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="p">{</span><span class="w">
  </span><span class="nl">"email"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="p">,</span><span class="w">
  </span><span class="nl">"password"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="p">,</span><span class="w">
  </span><span class="nl">"nombre"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="p">,</span><span class="w">
  </span><span class="nl">"apellido"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="p">,</span><span class="w">
  </span><span class="nl">"fecha_nacimiento"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="p">,</span><span class="w">
  </span><span class="nl">"tipo_doc"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="p">,</span><span class="w">
  </span><span class="nl">"nro_documento"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="p">,</span><span class="w">
  </span><span class="nl">"rol"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="w">
</span><span class="p">}</span>
</code></pre></div></div>
    <h3>Respuestas</h3>
    <p><strong>Código:</strong> <code>201 Created</code></p>
  </div>
</details>

<details>
  <summary style="font-size: 1.1em; cursor: pointer; padding: 10px; background-color: #f8f9fa; border-radius: 4px; border-left: 4px solid #28a745; margin-bottom: 5px;">
    <strong style="color: #28a745;">POST</strong> <code>/api/v1/auth/login</code> - Login
  </summary>
  <div style="padding: 15px; border: 1px solid #f8f9fa; border-top: none; margin-bottom: 20px;">
    <p><strong>ID de la Operación:</strong> <code>login_api_v1_auth_login_post</code></p>
    <p>Login de usuario administrativo. Verifica el ID token de Firebase, busca al usuario, obtiene permisos y devuelve la información unificada.</p>
    <h3>Parámetros</h3>
    <ul>
      <li><strong>Header:</strong> <code>x-internal-secret</code> (Requerido)</li>
    </ul>
    <h3>Cuerpo de la Petición</h3>
    <div class="language-json highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="p">{</span><span class="w"> </span><span class="nl">"id_token"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="w"> </span><span class="p">}</span>
</code></pre></div></div>
    <h3>Respuestas</h3>
    <p><strong>Código:</strong> <code>200 OK</code></p>
    <div class="language-json highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="p">{</span><span class="w">
  </span><span class="nl">"usuario_id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="p">,</span><span class="w">
  </span><span class="nl">"nombre"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="p">,</span><span class="w">
  </span><span class="nl">"apellido"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="p">,</span><span class="w">
  </span><span class="nl">"email"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="p">,</span><span class="w">
  </span><span class="nl">"rol"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="p">,</span><span class="w">
  </span><span class="nl">"permisos"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="s2">"string"</span><span class="p">]</span><span class="w">
</span><span class="p">}</span>
</code></pre></div></div>
  </div>
</details>

<details>
  <summary style="font-size: 1.1em; cursor: pointer; padding: 10px; background-color: #f8f9fa; border-radius: 4px; border-left: 4px solid #28a745; margin-bottom: 5px;">
    <strong style="color: #28a745;">POST</strong> <code>/api/v1/auth/verificar</code> - Verificar Permiso
  </summary>
  <div style="padding: 15px; border: 1px solid #f8f9fa; border-top: none; margin-bottom: 20px;">
    <p><strong>ID de la Operación:</strong> <code>verificar_permiso_api_v1_auth_verificar_post</code></p>
    <p><strong>Uso INTERNO:</strong> Otros microservicios llaman aquí para verificar si un usuario tiene un permiso específico antes de ejecutar una acción protegida.</p>
    <h3>Parámetros</h3>
    <ul>
      <li><strong>Header:</strong> <code>x-internal-secret</code> (Requerido)</li>
    </ul>
    <h3>Cuerpo de la Petición</h3>
    <div class="language-json highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="p">{</span><span class="w">
  </span><span class="nl">"firebase_uid"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="p">,</span><span class="w">
  </span><span class="nl">"permiso_requerido"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="w">
</span><span class="p">}</span>
</code></pre></div></div>
    <h3>Respuestas</h3>
    <p><strong>Código:</strong> <code>200 OK</code></p>
    <div class="language-json highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="p">{</span><span class="w">
  </span><span class="nl">"autorizado"</span><span class="p">:</span><span class="w"> </span><span class="kc">true</span><span class="p">,</span><span class="w">
  </span><span class="nl">"usuario_id"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="p">,</span><span class="w">
  </span><span class="nl">"rol"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="p">,</span><span class="w">
  </span><span class="nl">"nombre_completo"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="p">,</span><span class="w">
  </span><span class="nl">"detalle"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="w">
</span><span class="p">}</span>
</code></pre></div></div>
  </div>
</details>

<details>
  <summary style="font-size: 1.1em; cursor: pointer; padding: 10px; background-color: #f8f9fa; border-radius: 4px; border-left: 4px solid #fd7e14; margin-bottom: 5px;">
    <strong style="color: #fd7e14;">PATCH</strong> <code>/api/v1/auth/usuarios/{id_usuario}/rol</code> - Actualizar Rol Usuario
  </summary>
  <div style="padding: 15px; border: 1px solid #f8f9fa; border-top: none; margin-bottom: 20px;">
    <p><strong>ID de la Operación:</strong> <code>actualizar_rol_usuario_api_v1_auth_usuarios__id_usuario__rol_patch</code></p>
    <p>Actualiza el rol de un usuario administrativo impactando en la base de datos y en los claims de Firebase.</p>
    <h3>Parámetros</h3>
    <ul>
      <li><strong>Path:</strong> <code>id_usuario</code> (Requerido)</li>
      <li><strong>Header:</strong> <code>x-internal-secret</code> (Requerido)</li>
    </ul>
    <h3>Cuerpo de la Petición</h3>
    <div class="language-json highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="p">{</span><span class="w"> </span><span class="nl">"rol"</span><span class="p">:</span><span class="w"> </span><span class="s2">"string"</span><span class="w"> </span><span class="p">}</span>
</code></pre></div></div>
    <h3>Respuestas</h3>
    <p><strong>Código:</strong> <code>200 OK</code></p>
  </div>
</details>

## Roles y permisos

<details>
  <summary style="font-size: 1.1em; cursor: pointer; padding: 10px; background-color: #f8f9fa; border-radius: 4px; border-left: 4px solid #007bff; margin-bottom: 5px;">
    <strong style="color: #007bff;">GET</strong> <code>/api/v1/permisos</code> - Listar Permisos
  </summary>
  <div style="padding: 15px; border: 1px solid #f8f9fa; border-top: none; margin-bottom: 20px;">
    <p>Lista todos los permisos disponibles en el sistema.</p>
    <p><strong>Header Requerido:</strong> <code>x-internal-secret</code></p>
  </div>
</details>

<details>
  <summary style="font-size: 1.1em; cursor: pointer; padding: 10px; background-color: #f8f9fa; border-radius: 4px; border-left: 4px solid #007bff; margin-bottom: 5px;">
    <strong style="color: #007bff;">GET</strong> <code>/api/v1/roles</code> - Listar Roles
  </summary>
  <div style="padding: 15px; border: 1px solid #f8f9fa; border-top: none; margin-bottom: 20px;">
    <p>Lista todos los roles creados junto con sus permisos asignados.</p>
    <p><strong>Header Requerido:</strong> <code>x-internal-secret</code></p>
  </div>
</details>

<details>
  <summary style="font-size: 1.1em; cursor: pointer; padding: 10px; background-color: #f8f9fa; border-radius: 4px; border-left: 4px solid #28a745; margin-bottom: 5px;">
    <strong style="color: #28a745;">POST</strong> <code>/api/v1/roles</code> - Crear Rol
  </summary>
  <div style="padding: 15px; border: 1px solid #f8f9fa; border-top: none; margin-bottom: 20px;">
    <p>Crea un nuevo rol en la base de datos.</p>
    <p><strong>Header Requerido:</strong> <code>x-internal-secret</code></p>
    <h3>Cuerpo de la Petición</h3>
    <div class="language-json highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="p">{</span><span class="w">
  </span><span class="nl">"nombre"</span><span class="p">:</span><span class="w"> </span><span class="s2">"TESORERO"</span><span class="p">,</span><span class="w">
  </span><span class="nl">"permisos_ids"</span><span class="p">:</span><span class="w"> </span><span class="p">[</span><span class="mi">1</span><span class="p">,</span><span class="w"> </span><span class="mi">2</span><span class="p">,</span><span class="w"> </span><span class="mi">5</span><span class="p">]</span><span class="w">
</span><span class="p">}</span>
</code></pre></div></div>
  </div>
</details>

<details>
  <summary style="font-size: 1.1em; cursor: pointer; padding: 10px; background-color: #f8f9fa; border-radius: 4px; border-left: 4px solid #fd7e14; margin-bottom: 5px;">
    <strong style="color: #fd7e14;">PATCH</strong> <code>/api/v1/roles/{id_rol}</code> - Actualizar Rol
  </summary>
  <div style="padding: 15px; border: 1px solid #f8f9fa; border-top: none; margin-bottom: 20px;">
    <p>Actualiza los datos o permisos de un rol existente.</p>
    <p><strong>Path Param:</strong> <code>id_rol</code> | <strong>Header:</strong> <code>x-internal-secret</code></p>
  </div>
</details>

<details>
  <summary style="font-size: 1.1em; cursor: pointer; padding: 10px; background-color: #f8f9fa; border-radius: 4px; border-left: 4px solid #dc3545; margin-bottom: 5px;">
    <strong style="color: #dc3545;">DELETE</strong> <code>/api/v1/roles/{id_rol}</code> - Eliminar Rol
  </summary>
  <div style="padding: 15px; border: 1px solid #f8f9fa; border-top: none; margin-bottom: 20px;">
    <p>Elimina un rol de la base de datos.</p>
    <p><strong>Path Param:</strong> <code>id_rol</code> | <strong>Header:</strong> <code>x-internal-secret</code></p>
  </div>
</details>

## Módulos delegados (Instalaciones, reservas y disciplinas)

*(Estos endpoints delegan y orquestan la interacción con los recursos internos del usuario autenticado).*

<details>
  <summary style="font-size: 1.1em; cursor: pointer; padding: 10px; background-color: #f8f9fa; border-radius: 4px; border-left: 4px solid #007bff; margin-bottom: 5px;">
    <strong style="color: #007bff;">GET / POST / PATCH / DELETE</strong> <code>/api/v1/instalaciones</code>
  </summary>
  <div style="padding: 15px; border: 1px solid #f8f9fa; border-top: none; margin-bottom: 20px;">
    <p>Rutas para <strong>Listar, Crear, Obtener, Actualizar y Desactivar</strong> instalaciones.</p>
    <p><strong>Header Requerido:</strong> <code>x-internal-secret</code></p>
  </div>
</details>

<details>
  <summary style="font-size: 1.1em; cursor: pointer; padding: 10px; background-color: #f8f9fa; border-radius: 4px; border-left: 4px solid #28a745; margin-bottom: 5px;">
    <strong style="color: #28a745;">GET / POST / DELETE</strong> <code>/api/v1/reservas</code>
  </summary>
  <div style="padding: 15px; border: 1px solid #f8f9fa; border-top: none; margin-bottom: 20px;">
    <p>Rutas para <strong>Listar, Crear, Obtener y Cancelar</strong> reservas.</p>
    <p><strong>Header Requerido:</strong> <code>x-internal-secret</code></p>
  </div>
</details>

<details>
  <summary style="font-size: 1.1em; cursor: pointer; padding: 10px; background-color: #f8f9fa; border-radius: 4px; border-left: 4px solid #fd7e14; margin-bottom: 5px;">
    <strong style="color: #fd7e14;">GET / POST / DELETE</strong> <code>/api/v1/disciplinas</code>
  </summary>
  <div style="padding: 15px; border: 1px solid #f8f9fa; border-top: none; margin-bottom: 20px;">
    <p>Rutas para <strong>Listar, Crear, Obtener y Borrar</strong> (pausar) disciplinas.</p>
    <p><strong>Header Requerido:</strong> <code>x-internal-secret</code></p>
  </div>
</details>
