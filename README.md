# 🍔 Food Delivery

**Food Delivery** es una plataforma de comida a domicilio que permite a los usuarios descubrir restaurantes, consultar sus menús, realizar pedidos y seguir el estado de sus entregas.

El proyecto se desarrollará utilizando **Java, Spring Boot y una arquitectura de microservicios**, con el objetivo de construir una aplicación escalable, mantenible y preparada para incorporar nuevas funcionalidades.

Además, servirá como proyecto de portfolio para poner en práctica tecnologías y patrones utilizados habitualmente en el desarrollo backend.

## 🎯 Objetivos del proyecto

- Desarrollar una API REST con Java y Spring Boot.
- Aplicar una arquitectura basada en microservicios.
- Implementar autenticación y autorización mediante JWT.
- Gestionar usuarios, restaurantes, productos, pedidos y pagos.
- Implementar comunicación síncrona mediante REST y asíncrona mediante Apache Kafka.
- Utilizar PostgreSQL para la persistencia de datos.
- Contenerizar los servicios mediante Docker.
- Implementar pruebas automatizadas.
- Automatizar procesos de integración continua mediante GitHub Actions.
- Desarrollar una interfaz web para interactuar con la plataforma.

## ✨ Funcionalidades principales

### 👤 Usuarios y autenticación
- Registro e inicio de sesión.
- Autenticación mediante JWT.
- Gestión de perfiles.
- Administración de direcciones de entrega.
- Control de acceso basado en roles.

### 🍕 Restaurantes y menús
- Listado y búsqueda de restaurantes.
- Consulta de información y horarios.
- Gestión de menús y categorías.
- Consulta de productos, precios y disponibilidad.
- Gestión de restaurantes y sus productos por usuarios autorizados.

### 🛒 Pedidos
- Selección de productos.
- Gestión del carrito.
- Cálculo del importe del pedido.
- Confirmación de pedidos.
- Consulta del historial.
- Seguimiento del estado del pedido.

### 💳 Pagos
- Simulación inicial de pagos.
- Registro del resultado de las operaciones.
- Gestión de pagos aprobados y rechazados.
- Posible integración futura con una pasarela de pagos real.

### 🛵 Entregas
- Gestión de repartidores.
- Asignación de pedidos.
- Actualización del estado de las entregas.
- Consulta del progreso del reparto.

### 🔔 Notificaciones
- Confirmación de pedidos.
- Notificaciones sobre cambios de estado.
- Avisos de pedidos preparados y entregados.
- Envío de emails y posibles notificaciones adicionales.

## 🏗️ Arquitectura

El backend estará organizado como un **monorepo**, alojando los distintos microservicios en un único repositorio, pero manteniendo cada servicio como una aplicación independiente.

```text
food-delivery/
├── backend/
│   ├── api-gateway/
│   ├── auth-service/
│   ├── user-service/
│   ├── restaurant-service/
│   ├── order-service/
│   ├── payment-service/
│   ├── delivery-service/
│   └── notification-service/
├── frontend/
├── infrastructure/
│   └── docker-compose.yml
├── docs/
└── README.md
```

### Microservicios

| Microservicio | Responsabilidad |
|---|---|
| `api-gateway` | Punto de entrada para las peticiones del frontend. |
| `auth-service` | Registro, autenticación y emisión de tokens. |
| `user-service` | Perfiles y direcciones de los usuarios. |
| `restaurant-service` | Restaurantes, menús, categorías y productos. |
| `order-service` | Carritos, pedidos y estados. |
| `payment-service` | Procesamiento y registro de pagos. |
| `delivery-service` | Repartidores y gestión de entregas. |
| `notification-service` | Notificaciones y comunicaciones. |

Cada microservicio será responsable de su lógica de negocio y de sus propios datos. La comunicación entre servicios se realizará mediante APIs REST y eventos asíncronos cuando corresponda.

## 🛠️ Tecnologías

### Backend
- **Java 21**
- **Spring Boot**
- Spring Web
- Spring Data JPA
- Spring Security
- Spring Validation
- Spring Cloud Gateway
- Spring Kafka

### Datos y mensajería
- **PostgreSQL**
- **Apache Kafka**
- Redis, para funcionalidades de caché cuando sea necesario.

### Infraestructura y calidad
- **Maven** para la gestión de dependencias.
- **Docker y Docker Compose** para la ejecución de los servicios.
- **JUnit y Mockito** para las pruebas.
- **Springdoc OpenAPI / Swagger** para documentar las APIs.
- **Git y GitHub** para el control de versiones.
- **GitHub Actions** para la integración continua.

### Frontend
- React.
- TypeScript.
- Tailwind CSS.

Las versiones y dependencias definitivas se establecerán durante la configuración inicial del proyecto.

## 🔐 Seguridad

La aplicación incorporará medidas de seguridad como:

- Autenticación mediante JWT.
- Autorización basada en roles y permisos.
- Validación de los datos recibidos.
- Protección de los endpoints privados.
- Gestión centralizada de errores.
- Almacenamiento seguro de contraseñas mediante algoritmos de hash adecuados.
- Configuración de secretos y credenciales mediante variables de entorno.

## 📨 Comunicación entre servicios

La plataforma combinará dos mecanismos de comunicación:

**REST:** para operaciones que necesitan una respuesta inmediata, como consultar información de un restaurante.

**Apache Kafka:** para distribuir eventos de negocio, como la creación de un pedido o la actualización de su estado.

Ejemplo del flujo de un pedido:

```text
Cliente realiza un pedido
          |
          v
     Order Service
          |
          v
      Apache Kafka
          |
     +----+-----+
     |          |
     v          v
Payment      Notification
Service      Service
```

Los procesos de pedidos y pagos deberán contemplar errores, reintentos e idempotencia para evitar operaciones duplicadas y mantener la coherencia de los datos.

## 🗄️ Persistencia de datos

Cada microservicio será propietario de sus datos y no accederá directamente a las tablas internas de otros servicios.

Se utilizará PostgreSQL como sistema de gestión de bases de datos. La separación de datos se diseñará para preservar la autonomía de los microservicios, incluso si inicialmente varios utilizan una misma instancia de PostgreSQL.

Las operaciones que involucren varios servicios se diseñarán teniendo en cuenta que no existe una única transacción de base de datos que abarque todo el sistema.

## 🧪 Testing

Se implementarán pruebas en distintos niveles:

- **Unitarias:** validación de la lógica de negocio.
- **Integración:** comprobación de la interacción con bases de datos y otros componentes.
- **API:** validación de endpoints, respuestas y códigos HTTP.
- **Seguridad:** comprobación de autenticación, autorización y permisos.
- **End-to-end:** verificación de los principales flujos de usuario cuando la aplicación esté integrada.

## 🚀 Plan de desarrollo

El proyecto se desarrollará de forma incremental:

1. Configuración del repositorio y del entorno de desarrollo.
2. Creación del `auth-service`.
3. Implementación del `user-service`.
4. Desarrollo del `restaurant-service`.
5. Implementación del `order-service`.
6. Desarrollo del `payment-service` con pagos simulados.
7. Integración de Apache Kafka.
8. Desarrollo del `delivery-service`.
9. Implementación del `notification-service`.
10. Configuración del API Gateway.
11. Desarrollo e integración del frontend.
12. Pruebas automatizadas, documentación y seguridad.
13. Contenerización y automatización mediante Docker y GitHub Actions.

El orden podrá ajustarse según las dependencias entre funcionalidades y las necesidades de cada fase.

## 📌 Alcance inicial

La primera versión se centrará en las funcionalidades esenciales para completar el flujo de un pedido:

1. Registrar e iniciar sesión.
2. Consultar restaurantes y sus menús.
3. Seleccionar productos y crear un pedido.
4. Simular el pago.
5. Consultar el estado del pedido.
6. Gestionar la entrega y las notificaciones básicas.

Las integraciones con pagos reales, el seguimiento geográfico en tiempo real y otras funcionalidades avanzadas se considerarán ampliaciones futuras.

## 📚 Documentación

La documentación técnica del proyecto podrá incluir:

- Diagramas de arquitectura.
- Diseño de los microservicios.
- Contratos de las APIs REST.
- Modelo de datos.
- Diagramas de secuencia.
- Instrucciones de instalación y ejecución.
- Decisiones de arquitectura.

## 👨‍💻 Estado del proyecto

**En desarrollo.**

El proyecto se construirá progresivamente, priorizando una base funcional y bien estructurada antes de incorporar componentes avanzados de arquitectura distribuida.

---

Desarrollado como proyecto personal de aprendizaje y portfolio de backend con Java y Spring Boot.
