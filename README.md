# discovery-server-grupo03

Registro y descubrimiento de microservicios mediante **Spring Cloud Netflix Eureka**.

Este proyecto funciona como un **Discovery Server**, es decir, un servidor central donde los microservicios se registran para que otros servicios puedan encontrarlos sin depender de direcciones IP o puertos fijos.

## Tecnologías utilizadas

- Java 25
- Spring Boot 4.1.1
- Spring Cloud 2025.1.3
- Spring Cloud Netflix Eureka Server
- Maven

## Estructura principal

```text
src/main/java/pe/edu/cibertec/discoveryservergrupo03
└── DiscoveryServerGrupo03Application.java

src/main/resources
└── application.properties
```

La clase principal `DiscoveryServerGrupo03Application` utiliza la anotación `@EnableEurekaServer`, que habilita la aplicación como servidor Eureka.

## Configuración

El archivo `src/main/resources/application.properties` contiene la configuración principal:

```properties
spring.application.name=discovery-server-grupo03
server.port=8761
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
```

### Detalle de propiedades

- `spring.application.name`: nombre de la aplicación dentro del ecosistema Spring.
- `server.port`: puerto donde se ejecuta el servidor Eureka. Por defecto es `8761`.
- `eureka.client.register-with-eureka=false`: evita que el servidor Eureka se registre a sí mismo como cliente.
- `eureka.client.fetch-registry=false`: evita que el servidor intente obtener el registro de otro servidor Eureka.

## Requisitos previos

- JDK 25 instalado.
- Maven instalado o utilizar el Maven Wrapper incluido en el proyecto.

## Ejecución del proyecto

Desde la raíz del proyecto, ejecutar:

### En Windows

```bash
mvnw.cmd spring-boot:run
```

### En Linux/macOS

```bash
./mvnw spring-boot:run
```

También se puede compilar y ejecutar el archivo `.jar`:

```bash
mvnw.cmd clean package
java -jar target/discovery-server-grupo03-0.0.1-SNAPSHOT.jar
```

## Acceso al panel de Eureka

Una vez iniciado el proyecto, abrir en el navegador:

```text
http://localhost:8761
```

Desde este panel se pueden visualizar los microservicios registrados en Eureka.

## Registro de microservicios clientes

Los microservicios que quieran registrarse en este servidor deben incluir Eureka Client y configurar la URL del servidor Eureka, por ejemplo:

```properties
spring.application.name=nombre-del-servicio
eureka.client.service-url.defaultZone=http://localhost:8761/eureka/
```

## Pruebas

Para ejecutar las pruebas del proyecto:

```bash
mvnw.cmd test
```

## Rol dentro de una arquitectura de microservicios

Este servicio debe iniciarse antes que los demás microservicios, ya que actúa como punto central de descubrimiento. Los servicios clientes se registran aquí y pueden ser localizados dinámicamente por otros componentes del sistema.
