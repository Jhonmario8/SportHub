# 🏟️ SportHub

**SportHub** es una plataforma basada en arquitectura de microservicios para la administración de canchas deportivas y reservas.

El proyecto está compuesto por varios microservicios independientes que trabajan de forma colaborativa para ofrecer autenticación, gestión de reservas y envío de notificaciones.

Cada microservicio puede desarrollarse, desplegarse y escalarse de forma independiente.

---

# 📖 Tabla de Contenidos

- Descripción
- Arquitectura del Sistema
- Microservicios
- Tecnologías
- Requisitos Previos
- Estructura del Proyecto
- Clonar el Proyecto
- Inicializar los Submódulos
- Ejecución
- Comunicación entre Microservicios
- Flujo General
- Futuras Mejoras
- Autor

---

# 📝 Descripción

SportHub fue desarrollado siguiendo una arquitectura de microservicios con el objetivo de separar responsabilidades y facilitar la escalabilidad del sistema.

Actualmente el proyecto permite:

- Registro y autenticación de usuarios.
- Administración de canchas deportivas.
- Gestión de reservas.
- Envío de notificaciones por correo electrónico.

Cada funcionalidad se encuentra implementada en un microservicio independiente.

---

# 🏗 Arquitectura del Sistema

```text
                        +----------------+
                        |     Cliente    |
                        +--------+-------+
                                 |
                                 |
                 +---------------+---------------+
                 |                               |
                 v                               v
      +---------------------+        +------------------------+
      | SP-auth-service     |        | SP-reservation-service |
      |                     |<------>|                        |
      | Autenticación JWT   |        | Canchas y Reservas     |
      +----------+----------+        +-----------+------------+
                                                 |
                                                 |
                                                 v
                                   +---------------------------+
                                   | SP-notification-service   |
                                   |                           |
                                   | Envío de Correos          |
                                   +---------------------------+
```

---

# 📦 Microservicios

## 🔐 SP-auth-service

Responsable de:

- Registro de administradores.
- Registro de clientes.
- Inicio de sesión.
- Generación de JWT.
- Autenticación de usuarios.

Repositorio:

```
SP-auth-service
```

---

## 🏟 SP-reservation-service

Responsable de:

- Administración de canchas.
- Creación de reservas.
- Actualización del estado de reservas.
- Cancelación de reservas.
- Consulta de reservas.
- Consulta de canchas.

Repositorio:

```
SP-reservation-service
```

---

## 📧 SP-notification-service

Responsable de:

- Envío de correos electrónicos.
- Centralización de notificaciones.
- Integración SMTP con Gmail.

Repositorio:

```
SP-notification-service
```

---

# 🚀 Tecnologías

Todo el ecosistema fue desarrollado utilizando:

- Java 17
- Spring Boot
- Spring Security
- Spring Data JPA
- JWT
- OpenFeign
- MapStruct
- Lombok
- MySQL
- Gradle
- Git Submodules

---

# 📋 Requisitos Previos

Antes de ejecutar el proyecto es necesario tener instalado:

- Java JDK 17
- Gradle
- MySQL
- Git

Además será necesario configurar las variables de entorno correspondientes en cada microservicio.

---

# 📂 Estructura del Proyecto

```text
SportHub
│
├── SP-auth-service
│
├── SP-reservation-service
│
└── SP-notification-service
```

Cada directorio corresponde a un repositorio Git independiente administrado mediante **Git Submodules**.

---

# ⬇ Clonar el Proyecto

Clonar el repositorio principal:

```bash
git clone https://github.com/Jhonmario8/SportHub.git

cd SportHub
```

---

# 🔄 Inicializar los Submódulos

Después de clonar el proyecto es necesario descargar el contenido de los submódulos.

```bash
git submodule update --init --recursive
```

Si se agregan nuevos submódulos posteriormente:

```bash
git submodule update --remote
```

---

# ▶ Ejecución

Cada microservicio debe ejecutarse de forma independiente.

Orden recomendado:

### 1.

```
SP-auth-service
```

Puerto:

```
8080
```

---

### 2.

```
SP-reservation-service
```

Puerto:

```
8081
```

---

### 3.

```
SP-notification-service
```

Puerto:

```
8082
```

---

# 🔗 Comunicación entre Microservicios

Los microservicios colaboran entre sí para cumplir el flujo completo de una reserva.

- **SP-auth-service** autentica usuarios y genera JWT.

- **SP-reservation-service** valida el usuario autenticado y administra las reservas.

- **SP-notification-service** envía correos electrónicos cuando otro microservicio solicita una notificación.

La comunicación entre servicios se realiza mediante HTTP utilizando **OpenFeign** cuando es necesario.

---

# 🔄 Flujo General

```text
Usuario
    │
    ▼
SP-auth-service
    │
    │ JWT
    ▼
SP-reservation-service
    │
    │ Solicitud de notificación
    ▼
SP-notification-service
    │
    ▼
Correo enviado al usuario
```

---

# 📈 Futuras Mejoras

Algunas funcionalidades que pueden incorporarse en futuras versiones:

- Microservicio de trazabilidad.
- Docker Compose.
- API Gateway.
- Config Server.
- Service Discovery.
- Circuit Breaker.
- Observabilidad.
- OpenAPI / Swagger.
- CI/CD.
- Despliegue en la nube.

---

# 🤝 Contribución

1. Crear una rama.

```bash
git checkout -b feature/nueva-funcionalidad
```

2. Realizar los cambios.

3. Crear el commit.

```bash
git commit -m "feat: nueva funcionalidad"
```

4. Subir la rama.

```bash
git push origin feature/nueva-funcionalidad
```

5. Abrir un Pull Request.

---

# 👨‍💻 Autor

**Jhon Mario**

GitHub:

https://github.com/Jhonmario8

Proyecto:

https://github.com/Jhonmario8/SportHub