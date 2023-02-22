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

**http://localhost:9091/realms/{nombre-realm}/.well-known/openid-conﬁguration**

### Introducción a Keycloak

**¿Qué es Keycloak?** Keycloak es una herramienta de gestión de identidad y acceso de código abierto que se centra en aplicaciones modernas, como SPA (single page application), aplicaciones móviles o API REST. Se utiliza en producción para escenarios que van desde pequeños sitios web con solo un puñado de usuarios hasta grandes empresas con millones de usuarios.

#### Características de Keycloak

<img src="./img/caracteristicas-de-keycloack.png" alt="700" width="700"/>

* Permite integrar páginas de inicio de sesión totalmente personalizables en nuestras aplicaciones. Así como varios flujos, por ejemplo, la recuperación de contraseñas. Todo esto sin necesidad de agregar código.
* Al delegar el proceso de autenticación a Keyclock, nuestras aplicaciones no necesitan preocuparse por los mecanismos de autenticación o sobre cómo almacenar las contraseñas de manera segura.
* Permite a los usuarios acceder a múltiples aplicaciones autenticándose una única vez gracias al mecanismo de autenticación conocido como single sign-on (inicio de sesión único). También permite gestionar las sesiones: tanto los usuarios finales como los administradores tienen visibilidad completa de dónde están autenticados y pueden finalizar la sesión de forma remota cuando sea necesario.
* Keycloak viene con su propia base de datos de usuarios, lo que hace que sea fácil de comenzar a utilizar.
* Permite configurar la conexión con otra base de datos, ya sea una existente o una nueva.
* Es una solución ligera y fácil de instalar. Es altamente escalable y proporciona alta disponibilidad.

### Instalación y ejecución de Keycloak

Keycloak proporciona varias opciones de instalación. Algunas de ellas son:

* Ejecutándolo como un contenedor de Docker.
* Instalándolo y ejecutándolo localmente utilizando Java.
* Ejecutándolo con Kubernetes.

Nosotros vamos a utilizar Docker para ejecutarlo, ya que consideramos que es la opción más simple.

Ejecutando Keycloak con Docker

    docker run -p 8080:8080 -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:18.0.0 start-dev

(agregar sudo en ubuntu)

El comando de arriba nos permite ejecutar keycloak en un contenedor, en donde además indicamos que queremos exponer el puerto 8080, y configuramos las credenciales para el usuario administrador.

Listo, ahora podemos acceder a http://localhost:8080 para verificar su ejecución.

### Consola de administración

La consola de administración de Keycloak nos proporciona una interfaz para administradores y desarrolladores que quieran configurar y administrar Keycloak. Para acceder a la consola nos dirigimos a http://localhost:8080/admin/ y nos autenticamos. Una vez autenticados, podemos ver la configuración.

<img src="./img/consola-keycloak.png" alt="700" width="700"/>

### Creando y configurando un realm

Un realm (o reino) es un concepto que en Keycloak refiere a un objeto que administra un conjunto de usuarios junto con sus credenciales, roles y grupos. Un usuario en Keycloak pertenece a un solo reino.
Lo primero que tenemos que hacer es crear un reino para nuestra aplicación, los reinos nos permiten utilizar el servidor de Keycloak para múltiples aplicaciones, esto nos permite por ejemplo que cada aplicación tenga la configuración y su base de datos independiente del resto.

### ¿Cómo creamos un reino?
1. Apoyando el mouse sobre “Master” aparece el botón “Add realm”.

<img src="./img/creando-un-reino/1.png" alt="700" width="700"/>

2. Luego indicamos un nombre y clickeamos en “**Create**”.

<img src="./img/creando-un-reino/2.png" alt="700" width="700"/>

### Exportar/Importar configuraciones en Keycloak

Al trabajar de forma local con Keycloak puede ocurrir que necesitemos guardar la configuración de nuestro reino para poder utilizarla en otra computadora o, también, en el caso de que nuestra configuración se pierda y debamos realizarla desde cero. Keycloak nos permite importar y exportar nuestras configuraciones en archivos JSON.

Para exportar vamos al submenú “Export” en el menú a la izquierda de la consola de administración. Para crear el archivo de conﬁguración solamente tenemos que hacer clic en el botón “Export”.
Opcionalmente, podemos añadir a este archivo la conﬁguración de clientes, roles y grupos que hayamos creado (esto puede aumentar signiﬁcativamente el tamaño del archivo dependiendo de la cantidad que hayamos conﬁgurado).

<img src="./img/exportar-importar-config/1.png" alt="700" width="700"/>

Para importar tenemos dos opciones. Si tenemos que crear el reino nuevamente, podemos simplemente utilizar el archivo al hacerlo. Cuando vimos cómo crear un reino, haciendo clic en el botón “Add realm”, pudimos observar que existe la opción “Import”.
Luego, haciendo clic en “Select ﬁle” podemos buscar el archivo JSON que queremos utilizar y luego hacer clic en “Create”. El nuevo reino se creará con el mismo nombre y conﬁguración que tenga el archivo.

<img src="./img/exportar-importar-config/2.png" alt="700" width="700"/>

La otra opción es para el caso en que hayamos creado el reino, pero necesitamos importar su conﬁguración. Para esto, vamos al submenú “Import” en el menú a la izquierda de la consola de administración. Aquí tendremos que hacer clic en el botón “Select ﬁle”.

<img src="./img/exportar-importar-config/3.png" alt="700" width="700"/>

Buscamos el archivo JSON de conﬁguración que queremos añadir y lo seleccionamos. Allí podremos:
* Ver el detalle del archivo haciendo clic en “View Details”.
* Limpiar la selección del archivo haciendo clic en “Clear import”.
* Podremos elegir si queremos importar los clientes, roles de cliente o roles de usuario que contenga el archivo. Entre paréntesis, podemos ver el detalle de la cantidad que posee el archivo de cada uno.
* Por último, la opción “If a resource exists”, nos permite seleccionar qué acción debe tomar Keycloak en el caso de que se esté por importar un recurso que ya exista en nuestro entorno. Tenemos tres opciones: “Fail” lanzará un error detallando que el recurso ya existe, “Skip” ignorará los conﬂictos que existan y “Overwrite” sobreescribirá cualquier recurso que ya exista con el que estemos importando.

<img src="./img/exportar-importar-config/4.png" alt="700" width="700"/>

Una vez seleccionadas las opciones que queremos, hacemos clic en el botón “Import” y podremos ver un detalle de los cambios que fueron realizados.

<img src="./img/exportar-importar-config/5.png" alt="700" width="700"/>

Utilizar un administrador de acceso e identidades (IAM) permite que los desarrolladores se enfoquen en las reglas de negocio, al delegar los aspectos de seguridad de la autenticación y autorización. A su vez, una herramienta como Keycloak nos brinda la seguridad de que estamos utilizando una solución probada en producción a gran escala y nos evita el riesgo de implementar una solución propia que podría eventualmente fallar.

### Ejercitemos lo aprendido

<img src="./img/Ejercitemos-lo-aprendido.png" alt="700" width="700"/>

http://localhost:8080/realms/dh/protocol/openid-connect/auth?client_id=oidc-postman&response_type=code&redirect_uri=http://localhost:8082/&scope=openid

    docker-compose up

URL: http://localhost:8080/ | https://askcodes.net/coding/how-to-pass-arguments-to-entrypoint-in-docker-compose-yml

## Estándares de Autenticación y Autorización
### Introducción a estándares
<img src="./img/Introduccion-a-estandares.png" alt="700" width="700"/>

***Seguridad***: Los protocolos de autenticación estandarizados han sido examinados públicamente por expertos y son de confianza. Debido a esto, muchas organizaciones confiarán en determinadas soluciones solo si se utilizan protocolos estandarizados como **OAuth, OIDC o SAML**. Cuando utilizamos un protocolo estandarizado, tenemos la tranquilidad de saber que nuestro sistema de autenticación sigue los pasos de los expertos de la industria y las mejores prácticas.

***Aprendizaje transferible***: ¿Qué pasaría si cada vez que construimos el sistema de autenticación de un nuevo sistema, tenemos que crearlo desde cero? Tendríamos que aprender los detalles esenciales de la autenticación una y otra vez. Esto conduciría a un escenario en el que no podríamos aprovechar el conocimiento ganado con tanto esfuerzo entre proyectos y empleadores. Si, en cambio, utilizamos un protocolo ubicuo (como OAuth) puede haber diferencias sutiles, pero **comprenderemos la arquitectura de autenticación general**. Si sabemos cómo funcionan los protocolos estandarizados y qué casos de uso resuelven, **podemos llevar ese conocimiento a otros proyectos y empresas**. Lo mismo se aplica al enseñar e incorporar nuevos desarrolladores al equipo. Si utilizamos un protocolo de autenticación estandarizado, es probable que los nuevos miembros del equipo ya los conozcan. Por lo que será mucho más fácil hacer que estos nuevos miembros del equipo se pongan en marcha y contribuyan a estas áreas relevantes del sistema.

***Soporte de librerías***: La mayoría de los lenguajes de programación modernos tienen bibliotecas de códigos que se integran con los protocolos de autenticación estándar, lo que **acelera nuestro trabajo de desarrollo**. Mediante el uso de un protocolo de autenticación estandarizado, nuestros clientes y consumidores de API pueden reutilizar bibliotecas de códigos comunes para el lenguaje de programación elegido.

***Interoperabilidad entre sistemas***. El uso de un protocolo de autenticación como OAuth hace que nuestro sistema sea más interoperable con otros, es decir, **se comunique de manera más sencilla con otros sistemas**. Si trabajamos con una organización empresarial más grande, nuestro sistema necesitará integrarse con otros sistemas todo el tiempo. El uso de una forma estandarizada ahorra tiempo, sobrecarga mental y costos generales. Lo mismo se aplica a los sistemas externos. Si hemos creado una API compatible con OAuth, por ejemplo, nuestros clientes comprenderán cómo integrar sus soluciones y sistemas con los nuestros mucho más rápido y con muchos menos dolores de cabeza.

***Manejo de casos límite***: Los estándares han sido utilizados por muchas organizaciones y sistemas de muchas maneras diferentes. A menudo, los casos límite se manejan o se descartan explícitamente. Al aprovechar un estándar, **obtendremos los beneficios de todo ese conocimiento y experiencia**.

### OAuth 2.0

Cuando necesitamos darle acceso a la información de nuestra cuenta de Google (o a cualquier servicio) a un sitio web o aplicación, OAuth puede ayudarnos a garantizar ese acceso de forma segura. OAuth es, probablemente, el protocolo de autenticación más popular de la industria. ¿De autenticación? Bueno, de hecho, no es un protocolo de autenticación en sí mismo, como estamos a punto de ver.
Específicamente, OAuth permite que una aplicación obtenga de forma segura un token de acceso (un poco más adelante vamos a adentrarnos en el mundo de los tokens), que puede ser usado para realizar solicitudes adicionales a API de terceros o servicios web.
Podríamos decir, básicamente, que OAuth es un estándar que define la coreografía entre clientes y servicios para garantizar la forma en que se obtiene un token para acceder a los diferentes recursos de la aplicación o sitio web.
Por supuesto, en esta coreografía hay actores que tendrán diferentes roles y jugarán papeles muy importantes en el transcurso del proceso o flujo de solicitudes y recuperación de la información.

<img src="./img/oauth-clase-intro.jpg" alt="700" width="700"/>

#### Funcionamiento de OAuth 2.0

<img src="./img/diagrama-clase-intro.png" alt="700" width="700"/>

En esencia, en el flujo de protocolo OAuth, el cliente (la aplicación) solicita al servidor de autorización (el servicio) el acceso a un recurso en nombre del propietario (el usuario). El servidor de autorización emite un acceso limitado al recurso en forma de token de acceso. Tras recibir el token de acceso, el cliente puede acceder al recurso en el servidor de recursos (aquí aparece Keycloak, gestionando el proceso), incluyendo el token de acceso en la solicitud.

Ya tenemos, entonces, una comprensión un tanto básica de cómo funciona tras bambalinas el estándar de OAuth… ¿Pero no necesitamos introducirnos más a fondo hasta desenterrar todo el complicado proceso y código que esto conlleva? Bueno, no necesariamente. Lo que siempre vamos a priorizar es usar una biblioteca que oculte su complejidad y nos ayude a aplicarlo de la manera correcta… y, por supuesto, nos ahorre trabajo.

Pero después de repasar el funcionamiento, habrás notado algo raro… OAuth se dedica a conceder acceso a los recursos (para continuar usando la terminología correcta: “autorizar”), pero no hace nada respecto a la “autenticación” de los usuarios. Para cubrir este aspecto aparece OpenID Connect (OIDC), una extensión de OAuth 2.0. Veámoslo a continuación.

### OpenID Connect (OIDC)

Decíamos que OpenID Connect es una extensión de OAuth, es decir, una capa simple de identidad (es también un protocolo estándar como OAuth) que se coloca por encima y hace que la tarea de verificar la identidad de un usuario (autenticarlo) sea más sencilla. Además, obtiene información básica del perfil desde el proveedor de identidad y permite que aplicaciones de terceros puedan verificar dicha identidad del usuario final.

Digamos que, una de las características más importantes (y parte de su propósito) es proponer un solo login para múltiples sitios o aplicaciones cada vez que vayamos a loguearnos en un sitio web que use OIDC, seremos redirigidos a un sitio de OpenID donde nos loguearemos y, posteriormente, seremos llevados de vuelta al sitio web principal.

Por ejemplo, si ingresamos a un sitio y decidimos hacer login usando una cuenta de Google, entonces habremos usado OIDC. Una vez que somos autenticados exitosamente y autorizamos al sitio web o aplicación a la que estabamos tratando de ingresar para que pueda acceder a nuestra información, Google envía información al sitio web/aplicación sobre el usuario y sobre la autenticación realizada.

Esta información vuelve bajo la forma de un JWT (recibiremos un token de acceso -access token- y, probablemente, un token de identificación -ID token). Ya conocemos algo de JWT, pero vamos a ver qué papel juega exactamente en este proceso de autenticación/autorización.

Como habremos notado por el ejemplo, OIDC también sigue un flujo, y este es muy similar al de OAuth, excepto que los actores involucrados en el proceso son menos y tiene diferentes nombres:

<img src="./img/open-id-connect.png" alt="700" width="700"/>

Entonces, OIDC es de gran ayuda para cuando queremos permitir a los usuarios que se logueen en una aplicación por medio de otro servicio (los más comunes son Google, Facebook o Twitter). Históricamente, esto se hacía a través de OAuth, agregando algunas customizaciones extras. Pero OIDC nos provee de un estándar sólido para hacerlo de una manera segura y confiable.

Y ahora, repetimos una pregunta… ¿Necesitamos introducirnos a fondo hasta desenterrar todo el complicado proceso y código que OIDC conlleva? Por supuesto que no.

### Json Web Token (JWT)

Los JSON web tokens (JWT) son una forma estandarizada, compacta y autocontenida de transmitir de manera segura información entre partes. Sabemos que la J refiere a JSON y es que esa información se transmite como objetos de tipo JSON. Los JWT pueden ser verificados y confiados, ya que son firmados digitalmente (junto con la posibilidad de ser encriptados) y contienen toda la información requerida sobre una entidad, evitando tener que hacer consultas a una base de datos más de una vez. Además, quien recibe ese JWT tampoco necesita llamar a un servidor para validarlo. Pero vale la pena recalcar que, como dijimos que son un estándar, esto significa que todos los JWT son tokens, pero no todos los token son JWT.

***Beneficios de JWT***

<img src="./img/Beneficios-de-JWT/1.png" alt="700" width="700"/>
<img src="./img/Beneficios-de-JWT/2.png" alt="700" width="700"/>
<img src="./img/Beneficios-de-JWT/3.png" alt="700" width="700"/>
<img src="./img/Beneficios-de-JWT/4.png" alt="700" width="700"/>
<img src="./img/Beneficios-de-JWT/5.png" alt="700" width="700"/>
<img src="./img/Beneficios-de-JWT/6.png" alt="700" width="700"/>
<img src="./img/Beneficios-de-JWT/7.png" alt="700" width="700"/>
<img src="./img/Beneficios-de-JWT/8.png" alt="700" width="700"/>

Entonces, es muy importante que, antes de usar un JWT, este sea validado de forma apropiada usando su firma. Podemos notar que un token validado con éxito asegura que la información no fue manipulada, pero no significa que no haya sido vista; por ello es muy importante nunca transmitir información sensible vía JWT y utilizar mecanismos para que no sea interceptado (por ejemplo, enviarlos por medio de HTTPS).

### OIDC Discovery

**Configuración de Keycloak**

Compartimos la configuración de Keycloak que vamos a utilizar para esta clase:

    Nombre del reino (realm): digital-house
    Client ID: oidc-postman
    Root URL: http://localhost:8080

#### OpenID Connect Discovery

Dentro de las “reglas” de OpenID, podemos destacar OpenID Connect Discovery. Esta indica que el proveedor debe ofrecer un endpoint que nos permita obtener información acerca de su conﬁguración. El proveedor que implementa OpenID Connect, en nuestro caso, es Keycloak

**¿Cómo podemos ver esta información?**

Mediante una petición utilizando el método GET al endpoint:

    URL_HOST_KECLOAK/realms/REALM_NAME/.well-known/openid-conﬁguration

En nuestro caso, tenemos al servidor de Keycloak ejecutándose en el puerto 8085, así que nos quedará:

    http://localhost:8085/realms/digital-house/.well-known/openid-conﬁguration

**¿Qué información obtenemos?**

    {
        "issuer": "http://localhost:8085/realms/digital-house",  --issuer: URL de nuestro reino dentro de Keycloak.
        "authorization_endpoint": "http://localhost:8085/realms/digital-house/protocol/openid-connect/auth", --authorization_ endpoint: endpoint que se utiliza para autenticar al usuario en caso de que no esté logueado.
        "token_endpoint": "http://localhost:8085/realms/digital-house/protocol/openid-connect/token", --token_endpoint: endpoint para obtener el token.
        "introspection_endpoint": "http://localhost:8085/realms/digital-house/protocol/openid-connect/token/introspect",  --Introspection_ endpoint: endpoint para obtener información sobre un token dado.
        "userinfo_endpoint": "http://localhost:8085/realms/digital-house/protocol/openid-connect/userinfo", --userinfo_endpoint: endpoint para obtener información de un usuario.
        "end_session_endpoint": "http://localhost:8085/realms/digital-house/protocol/openid-connect/logout",
        "frontchannel_logout_session_supported": true,
        "frontchannel_logout_supported": true,
        "jwks_uri": "http://localhost:8085/realms/digital-house/protocol/openid-connect/certs",
        "check_session_iframe":
    "http://localhost:8085/realms/digital-house/protocol/openid-connect/login-status-iframe.html",
    ...
    }

**¿Para qué se usa esta información?** Esta información es utilizada por Spring Security (o cualquier otro cliente que se comunique con Keycloak) para implementar los diferentes ﬂujos (autenticación y autorización) que especiﬁca OpenID. Por eso es que en esta clase decidimos explicarlo utilizando solamente Postman. Si utilizamos Spring, no podríamos ver cómo es realmente la conexión entre estos dos componentes.

### Autenticación de un usuario

<img src="./img/autenticacion-de-un-usuario.png" alt="700" width="700"/>

1. La aplicación prepara lo que se llama una solicitud de autenticación y pide al navegador del usuario que sea redirigido a Keycloak.
2. El navegador del usuario redirige al usuario a Keycloak en una “terminal” llamada “terminal de autorización”.
3. Si el usuario no está autentificado previamente, Keycloak lo autentifica.
4. La aplicación recibe un código de autorización de Keycloak en forma de respuesta de autenticación.
5. La aplicación intercambia el código de autorización por un token de identificación y un token de acceso, a través de una solicitud de token a la terminal de token en Keycloak.
6. La aplicación tiene ahora el token de identificación que puede ser utilizado para descubrir la identidad del usuario y puede establecer una sesión autenticada para el usuario.

#### Flujo de autenticación de OpenID Connect

Si nos fijamos en la respuesta de la consulta al siguiente endpoint:

    http://localhost:8085/realms/digital-house/.well-known/openid-configuration

Podemos ver el campo authorization_endpoint. Ahora utilizaremos esa URL para crear el request de autenticación, que luego nos redirigirá a Keycloak para ingresar las credenciales del usuario.

Nos debería quedar de la siguiente manera:

    http://localhost:8085/realms/digital-house/protocol/openid-connect/auth?client_id=oidc-postman&response_type=code&redirect_uri=http://localhost:8080/&scope=openid

En la URL, podemos notar una serie de parámetros:

* client_id: el ID del cliente que creamos en Keycloak.

* response_type: indica que queremos que nos retorne un código (este código luego lo usamos para cambiarlo por un token).

* redirect_uri: en un caso real, esta URL debería ser la de nuestra aplicación front-end, en nuestro caso, es solo a modo de ejemplo.

* scope: los scopes se utilizan para especificar qué tipo de acceso solicitamos cuando realizamos una petición. Sin embargo, en este caso, al pasarle el valor de openid, estamos indicando a Keycloak que estamos realizando un request de OpenID Connect.

Al abrir la URL en el navegador, podemos ver que somos redirigidos a la pantalla de inicio de sesión de Keycloak. Luego de ingresar un usuario y contraseña válidos, Keycloak nos retorna el código que le solicitamos. Este código lo podemos tomar de la URL a la que nos redirige. En nuestro caso es:

    http://localhost:8080/?session_state=7e04cd1c-780c-41d4-bb44-a6b1d0746876&code=1f381d5e-46da-4942-b204-cc64fdbca4fe.7e04cd1c-780c-41d4-bb44-a6b1d0746876.dcddbad9-696a-4b1a-a070-6af5c14a586f

En donde el valor de code es el código que nos interesa tomar, para intercambiar por un token.

##### Obteniendo el token de un usuario autenticado

Si volvemos a  la respuesta de la consulta al endpoint http://localhost:8085/realms/digital-house/.well-known/openid-configuration, podemos ver el campo token_endpoint, que tiene la URL que necesitamos para conseguir el token del usuario autenticado. Desde Postman enviamos el siguiente request:

<img src="./img/flujo-de-autenticacion-de-openid-connect/1.png" alt="700" width="700"/>

Y obtenemos:

<img src="./img/flujo-de-autenticacion-de-openid-connect/2.png" alt="700" width="700"/>

Si obtenemos algún error de tipo invalid_grant, puede ser debido a las siguientes razones:

* Realizamos la petición para obtener el token demasiado lento. El código de autorización solo es válido durante 1 minuto. Tendremos que reintentarlo más rápido.

* Enviamos la misma petición más de una vez. El código de autorización es válido para usar una única vez.

### Análisis de un ID token

En la consulta anterior obtuvimos —en la respuesta— un campo llamado id_token, cuyo valor es un JWT que contiene la información del usuario autenticado. Si copiamos el id_token y lo pegamos en https://jwt.io/ para decodificarlo y ver su información, nos muestra algo como lo siguiente:

    {
      "exp": 1651579706,    -- exp: Fecha de expiración del token.
      "iat": 1651579406,    -- Iat: Fecha de creación del token.
      "auth_time": 1651579398,  -- aut_time: Fecha de la última autenticación del usuario.
      "jti": "20909551-494f-4146-99a7-da06d9d8ae23",    -- jti: ID del token.
      "iss": "http://localhost:8085/realms/digital-house",
      "aud": "oidc-postman",    --aud: ID del cliente.
      "sub": "b222d389-9e51-44ec-96dc-ea3f7a6a27be",    -- sub: ID del usuario. Es recomendado utilizar este ID en las bases de datos en lugar de username o email, ya que estos pueden cambiar.
      "typ": "ID",
      "azp": "oidc-postman",
      "session_state": "a91cf7c1-0fc7-4fb7-a092-00fcb9b207f7",
      "at_hash": "abDTBzH0X4UtqW4dbbHjUQ",
      "acr": "1",
      "sid": "a91cf7c1-0fc7-4fb7-a092-00fcb9b207f7",
      "email_verified": true,
      "name": "Tomas Pereyra",
      "preferred_username": "tomas",
      "given_name": "Tomas",
      "family_name": "Pereyra",
      "email": "pereyratomas18@gmail.com"
    }

Las fechas en los JWT están representadas en segundos desde el 1 de enero de 1970. Si queremos averiguar la fecha de algún campo, podemos utilizar la página www.epochconverter.com.

### Refresh token

Generalmente, el ID token tiene una corta duración. Luego de unos pocos minutos, vence. Para obtener un nuevo token tenemos que enviar el refresh_token al mismo endpoint que enviamos el code autenticamos un usuario.

**Ejemplo de request:**

<img src="./img/example-request.png" alt="700" width="700"/>

Ahora, en lugar de pasar el valor “code” para la key grant_type, le pasamos “refresh_token”. La respuesta nos envía el nuevo id_token y un nuevo refresh_token, ya que solamente lo podemos usar una única vez.

<img src="./img/example-response.png" alt="700" width="700"/>

### Modificación del perfil de usuario

Para agregar atributos a los usuarios, vamos al Panel de administración > Users y hacemos clic en el usuario que queremos modiﬁcar. Luego, ingresamos en la solapa Attributes. En nuestro caso, vamos a agregar un nuevo atributo llamado “nacionalidad”.

<img src="./img/modificacion-del-perfil-de-usuario/1.png" alt="700" width="700"/>

Para agregar este campo al token tenemos que crear un nuevo client scope. Este nos permitirá mapear los atributos del usuario en el token. Para crearlo vamos a Client Scopes en el menú de la izquierda y hacemos clic en Create. En nuestro caso, le vamos a poner de nombre “userScope” y guardamos

<img src="./img/modificacion-del-perfil-de-usuario/2.png" alt="700" width="700"/>

Ahora, dentro del detalle del client scope creado, hacemos clic en Mappers y creamos un nuevo Mapper con las siguientes características:

<img src="./img/modificacion-del-perfil-de-usuario/3.png" alt="700" width="700"/>

Como último paso, tenemos que agregar el client scope creado a nuestro cliente creado al comienzo de la clase. En el menú de la izquierda, hacemos clic en Clients y buscamos el cliente creado, en nuestro caso, oidc-postman. Entramos al detalle y seleccionamos Clients Scopes.

En la sección de scopes opcionales, agregamos el scope creado anteriormente. Como agregamos este scope como opcional, signiﬁca que el cliente deberá solicitarlo explícitamente.

<img src="./img/modificacion-del-perfil-de-usuario/4.png" alt="700" width="700"/>

Para comprobar que este nuevo atributo se esté agregando en el ID token, tenemos que volver a enviar la petición de autenticación, pero —en el campo scope— tenemos que agregar el scope creado. Por lo tanto, en nuestro caso, nos quedaría: scope: openid userScope.

### Agregar roles al ID token

Por defecto, los roles no se agregan al ID token. Si queremos agregarlos para hacer validaciones o simplemente leer la información, podemos hacerlo fácilmente de la siguiente forma:

    1- Debemos hacer clic en Client Scopes en el menú de la izquierda y luego ingresar a Roles

<img src="./img/Agregar%20roles%20al%20ID%20token/1.png" alt="700" width="700"/>

    2- Establecer en ON la opción Include in Token Scope

<img src="./img/Agregar%20roles%20al%20ID%20token/2.png" alt="700" width="700"/>

    3- De esta manera, podremos ver el rol del usuario desde el ID token (por ejemplo, copiando el access token y decodificándolo como ya vimos previamente con la herramienta www.jwt.io)

<img src="./img/Agregar%20roles%20al%20ID%20token/3.png" alt="700" width="700"/>

***Logout***

El proceso de cerrar una sesión consiste, simplemente, en invalidar todos los tokens de un usuario. Para hacer esto:

    1- La aplicación (es decir, nosotros que estamos probando) enviará una petición al endpoint end_session_endpoint (podemos ver la URL en el JSON de resultado donde se listan todos los endpoints, el endpoint del Discovery)

<img src="./img/Agregar%20roles%20al%20ID%20token/4.png" alt="700" width="700"/>

    2- Además, debemos agregar como query param el id_token del usuario autenticado (el id_token podemos encontrarlo en el resultado del endpoint openid-connect/token)

<img src="./img/Agregar%20roles%20al%20ID%20token/5.png" alt="700" width="700"/>
<img src="./img/Agregar%20roles%20al%20ID%20token/6.png" alt="700" width="700"/>

    3- Keycloak recibirá la petición, avisará a los otros clientes con los que el usuario podría intentar conectarse y luego invalidará la sesión, es decir, no permitirá renovar nunca más el ID token utilizando el refresh token.

### Resumen

#### OAuth 2.0

OAuth 2.0 es un estándar abierto para la autorización de APIs que nos permite compartir información con otras aplicaciones sin tener que compartir los datos del usuario. Actualmente, es utilizado por grandes empresas, como Google, Facebook, Twitter, entre otras.

**¿Qué problema resuelve?**
Pensemos en la siguiente situación: si tenemos un back end que expone una API y un front end que la consume, en principio no tenemos grandes problemas para gestionar los usuarios y sus credenciales, ya que somos dueños del 100% del sistema. Sin embargo, llega un momento en el que queremos agregar una funcionalidad que dependa de un tercero, por ejemplo, que nuestra aplicación escriba y publique contenido en la cuenta de Twitter de los usuarios. Para hacer esto, deberíamos pedirle el nombre de usuario y contraseña... Pensemos, ¿quién nos daría esta información? Nadie.
Con OAuth 2.0, el usuario puede autorizar a nuestra aplicación a publicar contenido en Twitter sin tener que compartir su contraseña.

**¿Cómo lo hace?**
OAuth 2.0 permite al cliente solicitar acceso a recursos con la aprobación del usuario mediante la generación de un token de acceso. De este modo, OAuth 2.0 permite que una aplicación acceda a recursos proporcionados por otra aplicación, sin solicitar el nombre de usuario y la contraseña del usuario.

<img src="./img/como-lo-hace.png" alt="700" width="700"/>

Mediante la generación de un token de acceso —una cadena que denota un ámbito específico, un tiempo de vida y otros atributos de acceso—, OAuth 2.0 permite al cliente solicitar acceso a recursos controlados por el propietario del recurso y alojados por el servidor de recursos, y recibir un conjunto diferente de credenciales del propietario del recurso. Los tokens de acceso son emitidos a los clientes de terceros por un servidor de autorización con la aprobación del propietario del recurso. El cliente utiliza el token de acceso para acceder a los recursos protegidos alojados en el servidor de recur Es un recurso muy presente en nuestro día a día. Posiblemente, ustedes (propietarios del recurso) han accedido a una aplicación (cliente) en la que le han concedido acceso a la información existente en otra aplicación (servidor de recursos), sin que esta nueva aplicación a la que ha accedido recientemente pueda ver toda la información, solo aquella a la que ustedes le han permitido acceder. Se autentifican directamente con un servidor de confianza del servicio (servidor de autorización), que emite las credenciales específicas de la delegación del servicio (token de acceso).

De este modo, OAuth 2.0 permite que una aplicación acceda a recursos proporcionados por otra aplicación sin solicitar el nombre y la contraseña del usuario.

#### OpenID Connect

Como vimos, con OAuth 2.0 realizamos el proceso de autorización que se realiza gracias a la incorporación de OpenID Connect, lo que permite llevar a cabo un inicio de sesión único mediante OAuth. OpenID Connect introduce el concepto de token ID. Este es un token de seguridad que permite al cliente verificar la identidad del usuario. El token ID también obtiene información básica del perfil del usuario.

#### OpenID Connect Discovery

Entonces, OpenID Connect es una simple capa de identidad que se coloca sobre el protocolo OAuth 2.0 y permite a los clientes verificar la identidad del usuario final basándose en la autenticación realizada por un servidor de autorización. Además, permite obtener información de perfil básica sobre el usuario final de una manera interoperable, tipo REST. Esta especificación define un mecanismo para que un tercero de confianza de OpenID Connect descubra el proveedor de OpenID del usuario final y obtenga la información necesaria para interactuar con él, incluyendo sus endpoints de OAuth 2.0. En este punto, entra en juego un servicio de OpenID Connect: Discovery. Este facilita el cambio entre diferentes proveedores de OpenID.

## Estrategias de Autorización Avanzadas
### Introducción
En esta clase vamos a ver un tema que es esencial para la seguridad de cualquier sistema: los mecanismos de control de acceso. Estos se pueden definir como un componente lógico que sirve para capturar una solicitud de acceso (de un usuario/cliente), tomar una decisión y verificar que esa decisión de acceso se cumpla.

Existen diversas estrategias (cada una con sus puntos fuertes y débiles), pero no se puede decir que una sea superadora por sobre otra, sino que son distintos enfoques que —muy a menudo— se usan en forma conjunta para enfrentar escenarios complejos.

Conocer y comprender estos métodos y sus características es un buen punto de partida para aplicarlos en distintos casos de uso de forma eficaz y costo-eficiente.

Las estrategias de control de acceso sobre las cuales estaremos aprendiendo son:

    RBAC (role-based access control)
    ABAC (attribute-based access control)
    Scopes de OAuth 2.0
    GBAC (group-based access control)

### RBAC (role-based access control)

 Tradicionalmente, para garantizar la seguridad, el control de acceso se gestionaba de forma individual mediante listas de control de acceso (ACL o access control list). El problema de este tipo de mecanismo es que tanto el costo de mantenimiento como el número de errores de gestión aumentan a medida que crece el número de usuarios a gestionar.

El control de acceso basado en roles (de ahora en adelante, RBAC, y también conocido como seguridad basada en roles) es un mecanismo de control de acceso que define los roles y asigna permisos a los usuarios finales para determinar si se le debe dar acceso a un recurso.

El aprovisionamiento u otorgamiento de acceso de usuarios se basa en las necesidades de un grupo dentro de la compañía u organización y en función de responsabilidades y necesidades comunes. Esto significa que los roles se definen en función de características propias de la organización, como la ubicación, el departamento, la antigüedad o las funciones del usuario. Por otro lado, los permisos se asignan según el acceso (lo que el usuario puede ver), las operaciones (lo que el usuario puede hacer) y las sesiones (cuánto tiempo puede hacerlo el usuario).

Vamos a ver 3 reglas fundamentales por las cuales se rige el RBAC:

* Asignación de roles: un usuario solo puede ejercer privilegios si se le ha asignado un rol.
* Autorización basada en roles: dicho rol del usuario debe estar autorizado, lo que garantiza que los usuarios solo puedan asumir roles para los que están autorizados.
* Autorización de privilegios: un usuario puede ejercer ciertos privilegios si, por supuesto, está autorizado para hacerlo.

Por otro lado, el RBAC tiene objetivos, funciones para las cuales está diseñado y orientado.

<img src="./img/funciones-rbac.png" alt="700" width="700"/>

<img src="./img/rbac-mesa-de-trabajo.png" alt="700" width="700"/>


Todas estas características hacen del RBAC muy popular en grandes organizaciones que necesitan otorgar acceso a cientos o miles de empleados. Pero también es cada vez más popular entre las organizaciones más pequeñas, ya que a menudo es más fácil de administrar que las listas de control de acceso.

**¿Y cómo hace Keycloak para poner en juego este mecanismo de seguridad?**

<img src="./img/tipos-de-roles-keycloak.jpg" alt="700" width="700"/>

### ABAC (attribute-based access control)

A diferencia de RBAC, en un sistema de control de acceso basado en atributos (ABAC), cualquier tipo de atributo —como los atributos de usuario y los atributos de recursos— se utilizan para determinar el acceso. Estos atributos se comparan con valores estáticos definidos o incluso con otros atributos, lo que lo convierte en un control de acceso basado en relaciones. Los atributos vienen en pares clave-valor (como "Rol = Supervisor"), que se pueden usar para limitar el acceso a una determinada característica de un sistema. Es decir, que este tipo de control utiliza los atributos que contiene el token e información sobre el contexto de autorización para conceder acceso a los recursos. Es probablemente el mecanismo de control más flexible y soporta de forma natural la autorización de accesos de granularidad fina.

<img src="./img/texto-intro-abac.png" alt="700" width="700"/>

Como ya vimos, la autorización a partir de tokens se basa en realizar una introspección de los mismos y utilizar la información que contienen para así permitir el acceso a los recursos. Esta información se representa como un set de atributos, o claims, y son sus valores los que verificaremos para conceder el acceso.

**Roles dentro de Keycloak**

<img src="./img/roles-dentro-keycloak.png" alt="700" width="700"/>

[ABAC (attribute-based access control)](https://www.keycloak.org/docs/latest/server_admin/#_protocol-mappers)

### OAuth 2.0 scopes

Keycloak es, fundamentalmente, un servidor de autorización basado en OAuth 2.0. A OAuth 2.0 ya lo conocemos y lo revisamos a fondo en clases pasadas, pero repasemos un aspecto importante. En OAuth hay dos tipos de aplicaciones: clientes y servidores de recursos. Vimos también que los tokens se generan para que los clientes puedan actuar en nombre de un usuario y están limitados al alcance (scope) al que el usuario otorgue su consentimiento. Por otro lado, los servidores de recursos son los que, basándose en ese token, deciden si un cliente puede acceder a un recurso protegido.

¿Pero qué es el scope? Es el alcance de la autorización y se usa para restringir el acceso a los recursos. Cuando se solicita un access token del servidor de autorizaciones, la aplicación cliente incluirá un scope como parámetro de la petición, especificando una lista de scopes (alcances) o determinados accesos a los recursos del usuario, que el token generado debe tener.

<img src="./img/texto-intro-oauth.jpg" alt="700" width="700"/>

Por defecto, los clientes en Keycloak no están configurados para pedir consentimiento del usuario. Esto sucede porque usualmente se emplea dentro de un ámbito empresarial, donde los clientes se encuentran dentro de los límites de la organización y los recursos a los cuales se puede acceder no requieren del consentimiento del usuario. En su lugar, requieren de un permiso de acceso que se define de acuerdo a roles, atributos específicos de un usuario o incluso grupos de usuarios (como veremos más adelante).

La autorización mediante los scopes de OAuth 2.0 se basa solamente en el consentimiento del usuario. Es una mejor estrategia a la hora de integrar servicios de terceros en nuestra aplicación y, en este caso, el usuario tendrá la decisión a la hora de autorizar a una aplicación de terceros a acceder a sus recursos. Para implementar esta estrategia se deberá poner énfasis en proteger la información de los usuarios. Debemos entender que esta estrategia de autorización se enfoca en proteger a los recursos de otros clientes (aplicaciones o servicios). Esto difiere de las estrategias que vimos anteriormente, como RBAC, en la cual se protege a los recursos de los usuarios.

### GBAC (group-based access control)

Keycloak nos permite administrar grupos (groups) dentro de nuestro reino. Los usuarios pueden formar parte de un group ya sea para representar su función dentro de una unidad de negocio de la organización o para agruparlos de acuerdo a los roles que cumplen dentro del contexto de nuestra aplicación —como podría ser, por ejemplo, un grupo de usuarios administradores—. Aquí entra en juego GBAC, asignando roles a los groups. De esta manera, Keycloak hace mucho más fácil la tarea de administrar roles comunes para múltiples usuarios sin obligarnos a otorgar o revocar roles a cada usuario de forma individual dentro del reino.

Los groups dentro de Keycloak son jerárquicos y, cuando se emiten los tokens, se puede atravesar esta jerarquía observando el path del group. Supongamos un ejemplo: tenemos un group de recursos humanos llamado “human resource”. Como hijo de este group, tenemos un grupo de administradores llamado “manager”. Cuando Keycloak almacena información sobre groups dentro de los tokens, la información debería llegar en el siguiente formato: /human resource/manager. Esta información estará disponible para cada token emitido por el servidor, donde el sujeto (usuario) sea miembro del group.

A diferencia de los roles, la información sobre el group no se incluye de forma automática dentro de los tokens, sino que debemos asociar un protocolo de mapeo al client (o un client scope con el mismo mapeo).

#### Mapear membresías de groups dentro del token

Empecemos creando un cliente con “client id: myclient”. Luego, creamos un usuario en
Keycloak, por ejemplo, un usuario con “username: Carlos”. Una vez tenemos estos datos,
navegamos al client myclient y hacemos clic en la pestaña “Mappers”. En esta pestaña,
crearemos un mapper haciendo clic en el botón “Create”.

En esta página crearemos un mapper con los siguientes atributos:

    ■ Name: groups
    ■ Mapper Type: Group Membership
    ■ Token Claim Name: groups

<img src="./img/mapear-memebresia/1.png" alt="700" width="700"/>

Hacemos clic en el botón “Save” y se creará nuestro mapper para el client myclient.

<img src="./img/mapear-memebresia/2.png" alt="700" width="700"/>

Ahora debemos crear un grupo para este usuario. Para eso hacemos clic en el link “Groups”.

<img src="./img/mapear-memebresia/3.png" alt="700" width="700"/>

Luego, hacemos clic en “New” y crearemos un grupo que se llamará “Project Management
Office”. Escribimos el nombre dentro de “Name” y hacemos clic en “Save”.

<img src="./img/mapear-memebresia/4.png" alt="700" width="700"/>

Ahora debemos añadir a Carlos al grupo, para esto vamos a la página de usuarios y, en el detalle del usuario, vamos a la pestaña “Groups”.

<img src="./img/mapear-memebresia/5.png" alt="700" width="700"/>

Para ingresar al grupo hacemos clic en el nombre del grupo en el recuadro “Available Groups” y luego en “Join”. Ahora, el grupo nos deberá aparecer dentro de “Group Membership”.

<img src="./img/mapear-memebresia/6.png" alt="700" width="700"/>

El usuario Carlos es ahora miembro del grupo Project Management Office. Volvamos a la pantalla del client, dentro de la pestaña “Client Scopes” vamos al apartado “Evaluate”. Una vez allí, donde dice “user”, escribimos el nombre del usuario y lo seleccionamos.

<img src="./img/mapear-memebresia/7.png" alt="700" width="700"/>

Una vez tenemos el usuario, hacemos clic en el botón “Evaluate” y veremos lo siguiente:

<img src="./img/mapear-memebresia/8.png" alt="700" width="700"/>

Hacemos clic en la pestaña “Generated Access Token” para ver que nuestro token posea la información sobre el grupo del usuario.

<img src="./img/mapear-memebresia/9.png" alt="700" width="700"/>

Como se puede observar, se tiene el atributo “groups”:[ “/Project Management Office” ], indicándonos que nuestro token ahora devuelve la información sobre los grupos a los que pertenece un usuario.

### Resumen

En esta clase pudimos hacer un breve recorrido por algunas de las estrategias de control de acceso más importantes y probadas en la industria. Podemos reflexionar, entonces, sobre la importancia de estos mecanismos para reforzar políticas de acceso (autorizar la obtención de recursos sobre la base de reglas que nosotros definamos) y hacer que nuestro sistema tenga una defensa más robusta frente a usuarios no autorizados que intenten realizar acciones indebidas o que pongan en riesgo la seguridad de nuestra aplicación.

Aprovechando la autorización mediante token, las aplicaciones pueden ser capaces de inspeccionar dichos tokens (ya sea localmente o mediante el endpoint de inspección) y usar sus claims para implementar esos diversos mecanismos de control de acceso —como RBAC, GBAC o ABAC—, o utilizar los scopes otorgados por el usuario a través de una aplicación client que actúa en su nombre. También tuvimos la oportunidad de ver que Keycloak puede ser utilizado como un servicio de autenticación centralizado que nos permitirá desacoplar la autorización de las aplicaciones, donde las decisiones de acceso son tomadas por Keycloak basándose en los recursos, políticas y reglas administradas a través del servidor.

Por último, te proponemos un tutorial sobre la configuración de grupos en Keycloak. De esta manera, vas a poder ver la puesta en escena de una de las estrategias vistas en clase que nos permitirá repasar la lógica por detrás de la misma. En el siguiente enlace, podrás descargar el código utilizado en el video.

## Tokens y sesiones

### Introducción
### Introdcción al manejo de sesioness
### Tiempo de vida de una sesión
### Ejercicio práctico con sesiones
### Forzar expiración de una sesión
### Gestión de tokens
### Resumen
### Ejercicio práctico integrador














***

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

<!--

<img src="./img/Screenshot from 2022-11-08 17-38-27.png" alt="700" width="700"/>

https://markdown.es/sintaxis-markdown/

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