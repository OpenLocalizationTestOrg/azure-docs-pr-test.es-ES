---
title: "Azure AD B2C: Protección de una API web mediante Node.js | Microsoft Docs"
description: "Cómo toobuild una Node.js web API que acepta los tokens de un inquilino B2C"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a>Azure AD B2C: Protección de una API web mediante Node.js
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

Con Azure Active Directory (Azure AD) B2C, puede proteger una API web mediante el uso de tokens de acceso de OAuth 2.0. Estos tokens permiten que las aplicaciones cliente que usan API de Azure AD B2C tooauthenticate toohello. Este artículo muestra cómo toocreate una API "lista de tareas pendientes" permite a los usuarios tooadd y lista de tareas. Hola web API se protege mediante Azure AD B2C y solo permite a los usuarios autenticados toomanage su lista de tareas pendientes.

> [!NOTE]
> En este ejemplo se escribió toobe conectado tooby utilizando nuestro [aplicación de ejemplo de iOS B2C](active-directory-b2c-devquickstarts-ios.md). Hola tutorial actual en primer lugar y, a continuación, seguir el ejemplo.
>
>

**Passport** es middleware de autenticación para Node.js. Passport es flexible y modular, y se puede instalar discretamente en cualquier aplicación web basada en Express o Restify. Un conjunto completo de estrategias admite la autenticación mediante un nombre de usuario y contraseña, Facebook, Twitter, etc. Hemos desarrollado una estrategia para Azure Active Directory (Azure AD). Instalar este módulo y, a continuación, agregar hello Azure AD `passport-azure-ad` complemento.

toodo en este ejemplo, necesita:

1. Registrar una aplicación con Azure AD.
2. Configurar la aplicación toouse Passport `azure-ad-passport` complemento.
3. Configurar un cliente aplicación toocall Hola "lista de tareas pendientes" API web.

## <a name="get-an-azure-ad-b2c-directory"></a>Obtener un directorio de Azure AD B2C
Para poder usar Azure AD B2C, debe crear un directorio o inquilino.  Un directorio es un contenedor de todos los usuarios, aplicaciones, grupos, etc.  Antes de continuar, si no tiene un directorio B2C, [créelo](active-directory-b2c-get-started.md) .

## <a name="create-an-application"></a>Creación de una aplicación
A continuación, debe toocreate una aplicación en el directorio B2C que ofrece cierta información que necesita toosecurely de Azure AD comunicarse con la aplicación. En este caso, aplicación de cliente de hello y API web se representan mediante una sola **Id. de aplicación**, porque están formadas por una aplicación lógica. toocreate una aplicación, siga [estas instrucciones](active-directory-b2c-app-registration.md). Asegúrese de:

* Incluir un **web de aplicación web o api** en aplicación hello
* Escribir `http://localhost/TodoListService` como **Dirección URL de respuesta**. Es dirección URL predeterminada de Hola para este ejemplo de código.
* Crear un **secreto de aplicación** para la aplicación y copiarlo. Estos datos se necesitarán más adelante. Tenga en cuenta que este valor debe toobe [XML escape](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) antes de utilizarla.
* Hola copia **Id. de aplicación** decir tooyour asignado aplicación. Estos datos se necesitarán más adelante.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Crear sus directivas
En Azure AD B2C, cada experiencia del usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md). Esta aplicación contiene dos experiencias de identidad: registrarse e iniciar sesión. Deberá toocreate una directiva de cada tipo, tal y como se describe en el [artículo de referencia de directiva](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).  Cuando cree las tres directivas, asegúrese de:

* Elija hello **nombre para mostrar** y otros atributos de inicio de sesión en la directiva de inicio de sesión.
* Elija hello **nombre para mostrar** y **Id. de objeto** notificaciones de la aplicación en cada directiva.  Puede elegir también otras notificaciones.
* Copia hacia abajo hello **nombre** de cada directiva después de haberlo creado. Deberían tener el prefijo de hello `b2c_1_`.  Los nombres de directiva se necesitarán más adelante.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Una vez haya creado las tres directivas, está listo toobuild la aplicación.

toolearn acerca de cómo funcionan las directivas en Azure AD B2C, comience con hello [.NET web app tutorial de introducción](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="download-hello-code"></a>Descargar código de hello
Hola código para este tutorial [se mantiene en GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS). ejemplo de Hola a toobuild que vaya, también puede [descargar un proyecto como un archivo .zip esqueleto](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip). También puede clonar el esqueleto de hello:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

aplicación Hello completado también es [disponible como un archivo .zip](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) o en hello `complete` rama de hello mismo repositorio.

## <a name="download-nodejs-for-your-platform"></a>Descarga de Node.js para su plataforma
toosuccessfully utilizar este ejemplo, se necesita una instalación activa de Node.js.

Instale Node.js desde [nodejs.org](http://nodejs.org).

## <a name="install-mongodb-for-your-platform"></a>Instalación de MongoDB en la plataforma
toosuccessfully utilizar este ejemplo, se necesita una instalación activa de MongoDB. Utilizamos MongoDB toomake la API de REST persistente en instancias del servidor.

Instale MongoDB desde [mongodb.org](http://www.mongodb.org).

> [!NOTE]
> Este tutorial se supone que utiliza Hola instalación y servidor de puntos de conexión predeterminados para MongoDB, lo cual en tiempo de presentación de redactar este artículo es `mongodb://localhost`.
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a>Instalar los módulos de Restify hello en la API web
Utilizamos Restify toobuild su API de REST. Restify es un marco de aplicación de Node.js mínimo y flexible que deriva de Express. Tiene un sólido conjunto de características para crear API de REST sobre Connect.

### <a name="install-restify"></a>Instalar Restify
Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`. Si hello `azuread` directorio no existe, créelo.

`cd azuread` o `mkdir azuread;`

Escriba el siguiente comando de hello:

`npm install restify`

Este comando instala Restify.

#### <a name="did-you-get-an-error"></a>¿Ha recibido un error?
En algunos sistemas operativos, cuando se usa `npm`, puede recibir el error hello `Error: EPERM, chmod '/usr/local/bin/..'` y una solicitud que ejecutar la cuenta de hello como administrador. Si se produce este problema, use hello `sudo` toorun comando `npm` con un nivel de privilegios superior.

#### <a name="did-you-get-a-dtrace-error"></a>¿Recibió un error de DTrace?
Al instalar Restify, puede ver algo parecido a esto:

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

Restify proporciona un mecanismo eficaz para rastrear llamadas a REST mediante DTrace. Sin embargo, muchos sistemas operativos no tienen DTrace disponible. Puede omitir estos errores con seguridad.

salida de Hello de comando de Hola debe aparecer un texto similar toothis:

    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0 (mv@0.0.5)

## <a name="install-passport-in-your-web-api"></a>Instalación de Passport en la API web
Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está allí.

Instalar mediante el siguiente comando de Hola de Passport:

`npm install passport`

salida de Hello de comando de hello debe ser un texto similar toothis:

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a>Agregar organización passport tooyour web API
A continuación, agregue la estrategia de OAuth de hello mediante el uso de `passport-azuread`, un conjunto de estrategias que se conectan a Azure AD con Passport. Utilice esta estrategia para los tokens de portador en el ejemplo de Hola a API de REST.

> [!NOTE]
> Aunque OAuth2 proporciona un marco de trabajo en el que se puede emitir cualquier tipo de token conocido, solo ciertos tipos de token tienen un uso generalizado. tokens de Hola para proteger los puntos de conexión son tokens de portador. Estos tipos de tokens son Hola emitido más comúnmente en OAuth2. Muchas implementaciones, se supone que los tokens de portador son Hola único tipo de token emitido.
>
>

Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está allí.

Instalar Hola Passport `passport-azure-ad` módulo mediante el siguiente comando de hello:

`npm install passport-azure-ad`

salida de Hello de comando de hello debe ser un texto similar toothis:

``
passport-azure-ad@1.0.0 node_modules/passport-azure-ad
├── xtend@4.0.0
├── xmldom@0.1.19
├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
├── underscore@1.8.3
├── async@1.3.0
├── jsonwebtoken@5.0.2
├── xml-crypto@0.5.27 (xpath.js@1.0.6)
├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
└── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
``

## <a name="add-mongodb-modules-tooyour-web-api"></a>Agregar MongoDB módulos tooyour web API
En este ejemplo se MongoDB como almacén de datos. Para ello, instale Mongoose, un complemento para administrar modelos y esquemas muy utilizados.

* `npm install mongoose`

## <a name="install-additional-modules"></a>Instalar módulos adicionales
A continuación, instale Hola restantes módulos necesarios.

Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está:

`cd azuread`

Instalar los módulos de hello en su `node_modules` directorio:

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a>Creación de un archivo server.js con sus dependencias
Hola `server.js` archivo proporciona mayoría Hola de funcionalidad de hello para el servidor de Web API.

Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está:

`cd azuread`

Cree un archivo `server.js` en un editor. Agregue Hola siguiente información:

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

Guarde el archivo hello. Devolver tooit más tarde.

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a>Crear un toostore de archivo config.js la configuración de Azure AD
Este archivo de código pasa los parámetros de configuración de Hola desde el Portal de Azure AD toohello `Passport.js` archivo. Estos valores de configuración se crean cuando se agrega hello web API toohello el portal en la primera parte del tutorial Hola de Hola. Se explica qué tooput en valores de hello de estos parámetros después de copiar el código de hello.

Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está:

`cd azuread`

Cree un archivo `config.js` en un editor. Agregue Hola siguiente información:

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a>Valores obligatorios
`clientID`: Hola Id. de cliente de la aplicación de API Web.

`IdentityMetadata`: Aquí es donde `passport-azure-ad` busca los datos de configuración para el proveedor de identidades de Hola. También busca los tokens de web JSON de hello claves toovalidate Hola.

`audience`: Hola el identificador uniforme de recursos (URI) del portal de Hola que identifica la aplicación que realiza la llamada.

`tenantName`: su nombre de inquilino (por ejemplo, **contoso.onmicrosoft.com**).

`policyName`: Hola directiva que desea que los tokens de hello toovalidate que entran en el servidor de tooyour. Esta directiva debe ser Hola la misma directiva que usa en la aplicación de cliente de Hola para inicio de sesión.

> [!NOTE]
> Por ahora, utilice Hola mismo directivas en el programa de instalación de cliente y servidor. Si ya ha completado un tutorial y crear estas directivas, no necesita toodo de nuevo. Como completado el tutorial de hello, no es necesario tooset directivas nuevas para los tutoriales de cliente en el sitio de Hola.
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a>Agregar el archivo de configuración tooyour server.js
valores de hello tooread de hello `config.js` de archivos que ha creado, agregue hello `.config` archivo como un recurso necesario en la aplicación y, a continuación, establecer Hola variables globales toothose en hello `config.js` documento.

Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está:

`cd azuread`

Abra hello `server.js` archivo en un editor. Agregue Hola siguiente información:

```Javascript
var config = require('./config');
```
Agregar una nueva sección demasiado`server.js` que incluye el siguiente código de hello:

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

A continuación, vamos a agregar algunos marcadores de posición para los usuarios de Hola que recibimos de nuestras aplicaciones que realiza la llamada.

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

Ahora vamos a crear también nuestro registrador.

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>Agregar información del esquema y el modelo de MongoDB hello mediante Mongoose
Hello preparación anterior se compensa como aportar estos tres archivos juntos en un servicio de API de REST.

Para este tutorial, utilice MongoDB toostore las tareas, como se explicó anteriormente.

Hola `config.js` archivo, se llama a la base de datos **tasklist**. Este nombre también era lo que se incluye al final de Hola de hello `mongoose_auth_local` dirección URL de conexión. No es necesario toocreate esta base de datos con antelación en MongoDB. Crea la base de datos de hello automáticamente en primera ejecución de saludo de la aplicación de servidor.

Una vez que indique al servidor hello qué toouse de base de datos de MongoDB, necesita toowrite algunos modelo de código adicional toocreate hello y esquema para las tareas de servidor.

### <a name="expand-hello-model"></a>Expanda el modelo de Hola
Este modelo de esquema es muy sencillo. Se puede expandir según sea necesario.

`owner`: Que se asignó la tarea de toohello. Este objeto es de tipo **cadena**.  

`Text`: tarea de hello en Sí. Este objeto es de tipo **cadena**.

`date`: fecha de hello vence esa tarea hello. Este objeto es de tipo **datetime**.

`completed`: Si la tarea hello está completa. Este objeto es de tipo **booleano**.

### <a name="create-hello-schema-in-hello-code"></a>Crear esquemas de hello en el código de hello
Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está:

`cd azuread`

Abra hello `server.js` archivo en un editor. Agregue Hola siguiendo la información que aparece debajo de la entrada de configuración de hello:

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
En primer lugar crear esquema hello y, a continuación, se crea un objeto de modelo que use toostore los datos a lo largo de Hola de código cuando se define la **rutas**.

## <a name="add-routes-for-your-rest-api-task-server"></a>Incorporación de rutas para el servidor de la tarea de API de REST
Ahora que tiene un toowork de modelo de base de datos con, agregar rutas de Hola que use para el servidor de la API de REST.

### <a name="about-routes-in-restify"></a>Información acerca de las rutas en Restify
Rutas funcionan en Restify Hola misma forma en que funcionan cuando usen la pila de hello Express. Definir las rutas mediante el uso de URI que se espera toocall de las aplicaciones de cliente de Hola Hola.

Un patrón típico de una ruta Restify es:

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

Restify y Express proporcionan una funcionalidad mucho más profunda, como la definición de tipos de aplicación y la realización de un enrutamiento complejo en distintos puntos de conexión. Para fines de Hola de este tutorial, mantenemos estas rutas simple.

#### <a name="add-default-routes-tooyour-server"></a>Agregar servidor de forma predeterminada las rutas tooyour
Ahora agregue rutas CRUD básicas de Hola de **crear** y **lista** para la API de REST. Otras rutas pueden encontrarse en hello `complete` rama de ejemplo de Hola.

Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está:

`cd azuread`

Abra hello `server.js` archivo en un editor. Por debajo de las entradas de base de datos de hello realizados anteriormente agregar Hola siguiente información:

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
    _task.date = new Date();

    _task.save(function(err) {
        if (err) {
            req.log.warn(err, 'createTask: unable toosave');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err)
            return next(err);

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Add one!");
        }

        if (!owner) {
            log.warn(err, "You did not pass an owner when listing tasks.");
        } else {

            res.json(data);

        }
    });

    return next();
}
```


#### <a name="add-error-handling-for-hello-routes"></a>Agregar control de errores para las rutas de Hola
Agregar un control de errores para que puedan comunicarse los problemas que encontrar a toohello atrás cliente de forma que puede entender.

Agregue Hola siguiente código:

```Javascript
///--- Errors for communicating something interesting back toohello client
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="create-your-server"></a>Creación del servidor
Ahora ha definido la base de datos y colocado las rutas en su sitio. últimos Hola para toodo es la instancia del servidor de Hola de tooadd que administra las llamadas.

Restify y Express proporcionan personalización en profundidad para un servidor de la API de REST, pero el programa de instalación más sencilla de hello aquí utilizamos.

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a>Agregar servidor de hello rutas toohello (sin autenticación)
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a>Agregar servidor de la API de REST de autenticación tooyour
Ahora que tiene un servidor de API de REST en ejecución, puede hacer que sea útil en Azure AD.

Desde la línea de comandos de hello, cambie el directorio demasiado`azuread`, si aún no está:

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Usar hello OIDCBearerStrategy que se incluye con azure de passport de ad
> [!TIP]
> No se puede suplantar al escribir las API, siempre debe vincular Hola datos toosomething único del token de Hola que Hola de usuario. Al servidor de hello almacena elementos de lista de tareas, hace según hello **oid** del usuario de hello en el token de hello (llamado a través de token.oid), que entra en el campo propietario"Hola". Este valor garantiza que el usuario es el único que puede acceder a sus propias tareas pendientes. No hay ningún riesgo en hello API de "propietario", por lo que un usuario externo puede solicitar otros elementos de lista de tareas, incluso si se autentican en.
>
>

A continuación, use la estrategia de portador de Hola que viene con `passport-azure-ad`.

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

Passport utiliza Hola mismo patrón para todas las estrategias de sus. Le pasa un elemento `function()` que tiene los parámetros `token` y `done`. estrategia de Hello vuelve a estar tooyou después de que lo ha hecho todo su trabajo. A continuación, debe almacenar usuario hello y guardar el token de Hola por lo que no es necesario tooask para este nuevo.

> [!IMPORTANT]
> código de Hello anterior toma cualquier usuario que ocurre tooauthenticate tooyour server. Este proceso se conoce como registro automático. En servidores de producción, no permita que en cualquier API de Hola de acceso de los usuarios sin tener primero que les vaya a través de un proceso de registro. Este proceso suele ser patrón Hola que se ven en las aplicaciones de consumidor que permiten tooregister mediante el uso de Facebook, pero a continuación, pida toofill información adicional. Si este programa no era un programa de línea de comandos, se pudo extrajeron correo electrónico Hola de objeto de símbolo (token) de Hola que se devuelve y, a continuación, pide a los usuarios toofill información adicional. Dado que este es un ejemplo, agregamos base de datos de tooan en memoria.
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a>Ejecute el tooverify de aplicación de servidor que TI rechaza
Puede usar `curl` toosee si tiene ahora OAuth2 protección frente a los extremos. Hello encabezados devueltos deben ser suficiente tootell que se encuentra en la ruta de acceso correcta de Hola.

Asegúrese de que la instancia de MongoDB se esté ejecutando:

    $sudo mongodb

Cambiar directorio toohello y el servidor de ejecución hello:

    $ cd azuread
    $ node server.js

En una nueva ventana de terminal, ejecute `curl`

Pruebe una operación POST básica:

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

Un error 401 es respuesta Hola que desee. Indica que está tratando de esa capa de Passport hello tooredirect toohello extremo authorize.

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a>Ahora tiene un servicio de API de REST que usa OAuth2
Ha implementado una API de REST mediante Restify y OAuth. Ahora tienes código suficiente para que pueda continuar toodevelop el servicio y crear en este ejemplo. Ha avanzado todo lo que se puede con este servidor sin usar un cliente compatible con OAuth2. Para ese paso siguiente, utilice un tutorial adicional como nuestro [conectarse tooa web API con iOS con B2C](active-directory-b2c-devquickstarts-ios.md) tutorial.

## <a name="next-steps"></a>Pasos siguientes
Ahora puede mover temas toomore avanzada, como:

[Conectar tooa web API con iOS y B2C](active-directory-b2c-devquickstarts-ios.md)
