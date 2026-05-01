# DISH PLANET

<p align="center">
  <img src="src/main/resources/static/img/logo.jpg" alt="DISH PLANET logo" width="180">
</p>

<p align="center">
  <strong>Aplicacion web para la gestion de un restaurante: carta digital, pedidos, reservas, inventario, panel de administracion e informes.</strong>
</p>

<p align="center">
  <img alt="Java" src="https://img.shields.io/badge/Java-17-red?style=for-the-badge&logo=openjdk">
  <img alt="Spring Boot" src="https://img.shields.io/badge/Spring%20Boot-3.2.5-6DB33F?style=for-the-badge&logo=springboot&logoColor=white">
  <img alt="Thymeleaf" src="https://img.shields.io/badge/Thymeleaf-Templates-005F0F?style=for-the-badge&logo=thymeleaf">
  <img alt="MySQL" src="https://img.shields.io/badge/MySQL-Database-4479A1?style=for-the-badge&logo=mysql&logoColor=white">
  <img alt="Docker" src="https://img.shields.io/badge/Docker-Ready-2496ED?style=for-the-badge&logo=docker&logoColor=white">
</p>

---

## Vista general

**DISH PLANET** es una aplicacion web desarrollada con **Spring Boot** para digitalizar la operativa de un restaurante. El proyecto permite navegar por una carta organizada por categorias, crear pedidos, gestionar reservas, controlar inventario en tiempo real y administrar platos, menus e informes desde un panel privado.

La aplicacion se despliega como archivo **WAR** en **Tomcat** y utiliza **MySQL** como base de datos principal. Incluye scripts de inicializacion con platos, menus, inventario base y un usuario administrador.

---

## Funcionalidades principales

### Carta digital

- Visualizacion de platos separados por **entrantes**, **principales**, **postres** y **bebidas**.
- Seccion de **menus completos** con entrante, principal, postre, bebida y precio.
- Imagen, descripcion, precio e ingredientes asociados a cada plato.
- Ranking de menus mas pedidos en la pagina de inicio.

### Pedidos

- Agregar platos y menus al pedido.
- Calculo automatico de **subtotal**, **IVA del 10%** y **descuento del 15%** para pedidos grandes.
- Historial temporal de pedido mediante cookies.
- Finalizacion del pedido y almacenamiento en la tabla de detalle.
- Envio de recibo por correo electronico.

### Reservas

- Registro de reservas con fecha y hora.
- Validacion de disponibilidad: maximo de reservas por franja horaria.
- Consulta, busqueda y cancelacion de reservas desde el panel de administracion.

### Inventario

- Listado y busqueda de productos por nombre o categoria.
- Actualizacion manual de cantidades.
- Descuento de ingredientes al realizar pedidos.
- Reposicion automatica cuando el stock baja del umbral definido.
- Notificaciones de inventario mediante **WebSocket/STOMP**.
- Alerta por email cuando se repone stock.

### Panel de administracion

- Alta de nuevos platos con subida de imagen JPG/PNG.
- Alta de nuevos menus.
- Eliminacion de platos, menus e items de inventario.
- Generacion de informe PDF de pedidos.
- Acceso reservado al usuario administrador.

### Autenticacion

- Login y logout con **Spring Security**.
- Registro de usuarios con contrasena cifrada mediante BCrypt.
- Recuperacion de contrasena mediante codigo de verificacion por email.

---

## Stack tecnologico

| Area | Tecnologias |
| --- | --- |
| Backend | Java 17, Spring Boot 3.2.5, Spring MVC |
| Seguridad | Spring Security, BCrypt |
| Persistencia | Spring Data JPA, Hibernate, MySQL |
| Frontend | Thymeleaf, HTML, CSS, JavaScript, Bootstrap, jQuery |
| Tiempo real | Spring WebSocket, STOMP, SockJS |
| Email | Spring Mail, Jakarta Mail |
| PDF | iText |
| Contenedores | Docker, Docker Compose, Tomcat |
| Testing | JUnit, Mockito, Spring Boot Test |

---

## Arquitectura del proyecto

```text
DISHPLANET
├── src
│   ├── main
│   │   ├── java/com/example/dishplanet
│   │   │   ├── config              # Configuracion web, WebSocket y utilidades
│   │   │   ├── controladores       # Controladores MVC
│   │   │   ├── controladoresRest   # Validaciones AJAX
│   │   │   ├── entidades           # Entidades JPA
│   │   │   ├── repositorios        # Repositorios Spring Data
│   │   │   ├── seguridad           # Configuracion de seguridad
│   │   │   └── servicios           # Logica de negocio
│   │   └── resources
│   │       ├── static              # CSS, JS, imagenes y animaciones
│   │       ├── templates           # Vistas Thymeleaf
│   │       └── application.properties
│   └── test                        # Tests unitarios e integracion basica
├── mysql-init                      # Scripts SQL de esquema y datos iniciales
├── Dockerfile                      # Imagen Tomcat para desplegar el WAR
├── docker-compose.yml              # Servicios MySQL + Tomcat
└── pom.xml                         # Configuracion Maven
```

---

## Modelo de datos

La base de datos se inicializa con los scripts de `mysql-init` e incluye las siguientes tablas principales:

- `Usuario`: usuarios registrados y administrador.
- `Plato`: platos de la carta con tipo, precio, imagen e ingredientes.
- `menu`: menus compuestos y contador de veces pedidas.
- `Pedido`: pedidos activos.
- `Detalle_Pedido`: historico de pedidos finalizados.
- `Ingredientes_Usados`: ingredientes consumidos por platos y menus.
- `Reserva`: reservas asociadas a usuarios.
- `Inventario`: stock, categorias, unidades y precio unitario.

---

## Instalacion y ejecucion

### Requisitos

- Java 17
- Maven
- Docker Desktop
- Puertos disponibles:
  - `8081` para la aplicacion
  - `3306` para MySQL

### 1. Clonar el repositorio

```bash
git clone <url-del-repositorio>
cd <nombre-del-repositorio>
```

### 2. Construir el WAR

```bash
mvn clean package -DskipTests
```

Tambien puedes usar el wrapper incluido:

```bash
./mvnw clean package -DskipTests
```

En Windows:

```bash
mvnw.cmd clean package -DskipTests
```

### 3. Levantar los contenedores

```bash
docker compose up --build
```

El `docker-compose.yml` levanta:

- Un contenedor **MySQL** con la base de datos `mydb`.
- Un contenedor **Tomcat** que despliega `DISHPLANET-0.0.1-SNAPSHOT.war` como aplicacion raiz.

### 4. Abrir la aplicacion

```text
http://localhost:8081
```

---

## Rutas principales

| Ruta | Descripcion |
| --- | --- |
| `/` | Pagina de inicio con slider y menus destacados |
| `/plato/entrantes` | Carta de entrantes |
| `/plato/principales` | Carta de platos principales |
| `/plato/postres` | Carta de postres |
| `/plato/bebidas` | Carta de bebidas |
| `/menu/menus` | Menus completos |
| `/pedido/pedidos` | Resumen del pedido |
| `/pedido/verPedidos` | Historial temporal del pedido |
| `/reservas` | Formulario de reserva |
| `/consultar-reservas` | Gestion de reservas para administrador |
| `/inventario` | Inventario para administrador |
| `/panel` | Panel de administracion |
| `/usuario/login` | Inicio de sesion |
| `/usuario/signup` | Registro |

---

## Pruebas

El proyecto incluye tests sobre servicios clave:

- `UserServiceTest`
- `InventarioServiceTest`
- `EmailServiceTest`
- `DishplanetApplicationTests`

Para ejecutarlos:

```bash
mvn test
```

---


## Despliegue con Docker

El despliegue esta preparado para un flujo sencillo:

1. Maven genera el WAR en `target/`.
2. Docker construye una imagen Tomcat.
3. El WAR se copia como `ROOT.war`.
4. MySQL carga automaticamente los scripts SQL de `mysql-init`.
5. La aplicacion queda disponible en `localhost:8081`.

---

## Autor
Miguel Aguilera
Proyecto desarrollado como sistema web de gestion para restaurante, integrando carta digital, pedidos, reservas, inventario y administracion en una unica aplicacion.

