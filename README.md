# DISH PLANET

<p align="center">
  <img src="src/main/resources/static/img/logo.jpg" alt="DISH PLANET logo" width="180">
</p>

<p align="center">
  <strong>Aplicacion web full stack para digitalizar la operativa de un restaurante: carta digital, pedidos, reservas, inventario, panel de administracion, notificaciones e informes.</strong>
</p>

<p align="center">
  <img alt="Java" src="https://img.shields.io/badge/Java-17-red?style=for-the-badge&logo=openjdk">
  <img alt="Spring Boot" src="https://img.shields.io/badge/Spring%20Boot-3.2.5-6DB33F?style=for-the-badge&logo=springboot&logoColor=white">
  <img alt="Thymeleaf" src="https://img.shields.io/badge/Thymeleaf-Templates-005F0F?style=for-the-badge&logo=thymeleaf">
  <img alt="PostgreSQL" src="https://img.shields.io/badge/PostgreSQL-Cloud-4169E1?style=for-the-badge&logo=postgresql&logoColor=white">
  <img alt="Docker" src="https://img.shields.io/badge/Docker-Ready-2496ED?style=for-the-badge&logo=docker&logoColor=white">
  <img alt="Render" src="https://img.shields.io/badge/Render-Deployment-46E3B7?style=for-the-badge&logo=render&logoColor=black">
</p>

---

## Vista general

**DISH PLANET** es una aplicacion web desarrollada con **Spring Boot** orientada a digitalizar la operativa de un restaurante mediante una plataforma moderna e interactiva.

La aplicacion permite navegar por la carta digital, gestionar pedidos, realizar reservas, controlar inventario, administrar platos y menus, recibir notificaciones en tiempo real, generar informes y gestionar usuarios con autenticacion segura.

El proyecto utiliza una arquitectura full stack basada en **Spring Boot**, **Thymeleaf**, **PostgreSQL**, **Docker** y despliegue cloud en **Render**. La aplicacion esta preparada para despliegue cloud permanente utilizando **Render**, **Neon PostgreSQL** y **GitHub**.

---

## Funcionalidades principales

### Carta digital

- Visualizacion de platos separados por categorias:
  - Entrantes
  - Principales
  - Postres
  - Bebidas
- Imagenes dinamicas de platos.
- Ingredientes y descripcion detallada.
- Menus completos con precio total.
- Ranking de platos y menus mas pedidos.

### Pedidos

- Anadir platos y menus al pedido.
- Calculo automatico de subtotal, IVA y descuentos.
- Persistencia temporal mediante cookies.
- Confirmacion y almacenamiento de pedidos.
- Generacion de historial.
- Envio automatico de recibos por email.

### Reservas

- Registro de reservas por fecha y hora.
- Validacion automatica de disponibilidad.
- Gestion y cancelacion de reservas.
- Panel administrativo de control.

### Inventario

- Gestion de stock en tiempo real.
- Busqueda por nombre y categoria.
- Actualizacion de cantidades.
- Descuento automatico de ingredientes.
- Reposicion automatica de productos.
- Notificaciones mediante WebSocket/STOMP.
- Alertas por correo electronico.

### Panel de administracion

- Alta de platos con imagenes.
- Gestion de menus.
- Gestion de inventario.
- Eliminacion de elementos.
- Generacion de informes PDF.
- Acceso restringido para administradores.

### Seguridad y usuarios

- Login y logout con Spring Security.
- Contrasenas cifradas con BCrypt.
- Registro de usuarios.
- Recuperacion de contrasena por email.
- Gestion de roles y autenticacion.

---

## Stack tecnologico

| Area | Tecnologias |
| --- | --- |
| Backend | Java 17, Spring Boot 3.2.5, Spring MVC |
| Seguridad | Spring Security, BCrypt |
| Persistencia | Spring Data JPA, Hibernate, PostgreSQL |
| Frontend | Thymeleaf, HTML, CSS, JavaScript, Bootstrap, jQuery |
| Tiempo real | Spring WebSocket, STOMP, SockJS |
| Email | Spring Mail, Jakarta Mail |
| PDF | iText |
| Cloud | Render, Neon PostgreSQL |
| Contenedores | Docker |
| Testing | JUnit, Mockito, Spring Boot Test |

---

## Arquitectura del proyecto

```text
DISHPLANET
├── src
│   ├── main
│   │   ├── java/com/example/dishplanet
│   │   │   ├── config
│   │   │   ├── controladores
│   │   │   ├── controladoresRest
│   │   │   ├── entidades
│   │   │   ├── repositorios
│   │   │   ├── seguridad
│   │   │   └── servicios
│   │   └── resources
│   │       ├── static
│   │       │   └── img
│   │       ├── templates
│   │       ├── application.properties
│   │       └── data.sql
│   └── test
├── Dockerfile
├── pom.xml
└── README.md
```

---

## Base de datos

La aplicacion utiliza **PostgreSQL** desplegado en la nube mediante **Neon**.

Las tablas se generan automaticamente mediante **Hibernate/JPA** y los datos iniciales se cargan automaticamente desde:

```text
src/main/resources/data.sql
```

Esto permite:

- Reconstruccion automatica del entorno.
- Despliegues reproducibles.
- Demos persistentes.
- Inicializacion automatica de datos.

---

## Modelo de datos

Principales entidades del sistema:

- `usuario`
- `plato`
- `menu`
- `pedido`
- `detalle_pedido`
- `inventario`
- `ingredientes_usados`
- `reserva`

---

## Imagenes y recursos estaticos

Las imagenes de platos y menus se almacenan en:

```text
src/main/resources/static/img
```

Y son servidas automaticamente por Spring Boot.

Ejemplo:

```text
/img/fideosSalteados.jpg
```

---

## Instalacion y ejecucion local

### Requisitos

- Java 17
- Maven
- Docker Desktop
- PostgreSQL

### 1. Clonar repositorio

```bash
git clone <url-del-repositorio>
cd DISH_PLANET
```

### 2. Configurar variables de entorno

```bash
DB_URL=
DB_USERNAME=
DB_PASSWORD=
MAIL_USERNAME=
MAIL_PASSWORD=
```

### 3. Compilar proyecto

```bash
mvn clean package -DskipTests
```

### 4. Ejecutar aplicacion

```bash
java -jar target/DISHPLANET-0.0.1-SNAPSHOT.jar
```

### 5. Abrir aplicacion

```text
http://localhost:8080
```

---

## Despliegue cloud

La aplicacion esta preparada para despliegue automatico mediante:

- Render
- Docker
- PostgreSQL Neon
- GitHub CI/CD

### Flujo de despliegue

```text
GitHub
↓
Render Build
↓
Docker
↓
Spring Boot
↓
Neon PostgreSQL
↓
Aplicacion online
```

---

## Despliegue Docker

### Construccion

```bash
docker build -t dishplanet .
```

### Ejecucion

```bash
docker run -p 8080:8080 dishplanet
```

---

## Rutas principales

| Ruta | Descripcion |
| --- | --- |
| `/` | Pagina principal |
| `/plato/entrantes` | Carta de entrantes |
| `/plato/principales` | Carta de principales |
| `/plato/postres` | Carta de postres |
| `/plato/bebidas` | Carta de bebidas |
| `/menu/menus` | Menus completos |
| `/pedido/pedidos` | Resumen del pedido |
| `/reservas` | Sistema de reservas |
| `/inventario` | Gestion de inventario |
| `/panel` | Panel administrativo |
| `/usuario/login` | Inicio de sesion |
| `/usuario/signup` | Registro de usuarios |

---

## Testing

El proyecto incluye pruebas unitarias e integracion basica utilizando:

- JUnit
- Mockito
- Spring Boot Test

Ejecutar tests:

```bash
mvn test
```

---

## Caracteristicas tecnicas destacadas

- Arquitectura MVC.
- Persistencia JPA/Hibernate.
- Seguridad Spring Security.
- WebSockets en tiempo real.
- Integracion SMTP.
- Docker deployment.
- PostgreSQL cloud.
- CI/CD automatico.
- Inicializacion automatica de datos.
- Gestion de imagenes estaticas.
- Backend y frontend integrados.

---

## Autor

**Miguel Aguilera**

Proyecto desarrollado como sistema web full stack para la gestion digital de restaurantes, integrando carta interactiva, reservas, pedidos, inventario, administracion y despliegue cloud profesional en una unica plataforma.
