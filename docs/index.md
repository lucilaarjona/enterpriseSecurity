# Seguridad en Microservicios

## ¿Qué es una Identity and Access Management?

un Identity and Access Management es un sistema que permite a las personas verificadas acceder a los recursos permitidos en el momento que sea solicitado. IAM viene a resolver la necesidad de garantizar el acceso adecuado a los recursos en entornos tecnológicos cada vez más heterogéneos, cumpliendo con rigurosos requisitos.

### ¿Cómo funciona el IAM?

<img src="./img/como funciona el iam.png" alt="700" width="700"/>

#### Autenticación
1. El usuario provee sus credenciales, ya sea por software o hardware.
2. El IAM tiene mecanismos para verificar si las credenciales son válidas o no.
3. Por lo general, los métodos para verificar credenciales consisten en camparar resultados de funciones de hash.
#### Autorización
1. Permite integrar páginas de inicio de sesión totalmente personalizables en nuestras aplicaciones. Así como varios flujos, por ejemplo, la recuperación de contraseñas. Todo esto sin necesidad de agregar código.
2. Suponiendo que el usuario ya está autenticado, lo siguiente es verificar que dicho usuario "puede" acceder al recurso solicitado. Esta verificación se hace de manera centralizada (es decir, "X usuario tiene aceso a Y recurso") o el propio recurso puede validar quién tiene acceso a él.
3. La configuración ideal es que el acceso a los recursos (o acciones sobre los mismos) se agrupen en perfiles y estos se agrupen en roles, y los usuarios tengan asignados determinados roles. En la práctica, se aplican distintas combinaciones de la implementación anterior. Por ejemplo, que los usuarios tengan perfiles y no roles o, en algunos casos, permisos individuales.

### ¿Qué hace el IAM?

Los sistemas IAM, como base, proporcionan:

- Gestión de los usuarios: el sistema puede gestionar un repositorio propio de usuarios para crear, modificar y eliminarlos, o puede integrarse con otros repositorios y sincronizarse con ellos. Los usuarios también pueden representar a entidades no humanas, como software, dispositivos IoT o robótica.
- Roles: IAM permite agrupar usuarios según un rol para luego determinar su nivel de acceso. Por ejemplo, administradores, editores, etc.
- Autenticación: IAM autentica a un usuario al confirmar que es quien dice ser. Generalmente, se utiliza la autenticación multifactor. Esta consiste en proveer más credenciales generadas de manera distinta a fin de fortalecer la autenticación
- Autorización: la gestión de accesos garantiza que a un usuario se le otorga el nivel exacto y el tipo de acceso al que tiene derecho.
- Reportes: podemos generar reportes sobre las acciones realizadas en la plataforma, como la hora de inicio de sesión, los sistemas a los que se accede y el tipo de autenticación.
- Single sign-on (SSO): permite a los usuarios autenticarse utilizando las credenciales “federadas” en un único portal (por ejemplo: Google o Facebook). De esta manera, no es necesario que el usuario se registre nuevamente con un usuario y contraseña.
- Autenticación de múltiples factores (MFA): en una era en la que las contraseñas a menudo son robadas, el requisito de una prueba de identidad adicional es el nuevo estándar. La autenticación a través de huellas dactilares y las contraseñas de un solo uso son ejemplos de métodos de autenticación comunes.

### Clientes de reinos de Keycloak

Son las entidades que pueden solicitar a Keycloak la autenticación de un usuario. Generalmente, son aplicaciones y/o servicios que necesitan autenticar vía single sign-on.
También pueden ser entidades que requieren información del usuario autenticado previamente o un token relacionado con ellos para poder invocar a otros servicios de la solución que también usen KeyCloak.

Para crear un cliente dentro de la opción de “**Clients**” seleccionamos el ícono de “**Create**” y dentro de la opción “**Root URL**” especiﬁcamos la URL root de nuestra aplicación o servicio.

<img src="./img/ClientesKeycloak/1.png" alt="700" width="700"/>

Luego debemos hacer que nuestro cliente sea de acceso conﬁdencial para que cada API o servicio que lo requiera deba tener una clave y una contraseña como **secret** para poder acceder a estos servicios de Keycloak.Con esta opción habilitada tendremos que indicar que la característica “**Authorization Enabled**” esté habilitada.

<img src="./img/ClientesKeycloak/2.png" alt="700" width="700"/>

Luego de seleccionar la opción “**Save**”, en la solapa de “**Credentials**”, podremos visualizar el secret a utilizar para conectarnos como clientes de Keycloak desde nuestro microservicio que desea autenticar a un usuario. En este caso, sería: “**jVgqbVwgkG2f9dWkEWI670uUGj4DTMo9**”.

<img src="./img/ClientesKeycloak/3.png" alt="700" width="700"/>

#### Crear un usuario

Para crear un usuario, debemos ir la opción de “**Manage > Users**” y hacer clic en el botón “**Add user**”.

<img src="./img/ClientesKeycloak/4.png" alt="700" width="700"/>

Completamos los datos de usuario y lo dejamos, en esta instancia, sin grupo

<img src="./img/ClientesKeycloak/5.png" alt="700" width="700"/>

Luego de guardarlo, vamos a ir a la opción de “**Credentials**” para asignarle una contraseña.

<img src="./img/ClientesKeycloak/6.png" alt="700" width="700"/>

Si queremos revisar nuestra conﬁguración en formato JSON, podemos ingresar en la siguiente URL:
**http://localhost:9091/realms/{nombre-realm}/.well-known/openid-conﬁguration**

## Introducción a Keycloak
## Consola de administración
## Creando y configurando un realm
## Exportar/Importar configuraciones en Keycloak




docker run -p 8080:8080 -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:18.0.0 start-dev

http://localhost:8080/realms/dh/protocol/openid-connect/auth?client_id=oidc-postman&response_type=code&redirect_uri=http://localhost:8082/&scope=openid

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

<!-- <img src="./img/Screenshot from 2022-11-08 17-38-27.png" alt="700" width="700"/>

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

-->