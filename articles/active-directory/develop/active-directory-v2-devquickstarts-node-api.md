---
title: aaaSecure una API web de v2.0 de Azure Active Directory mediante el uso de Node.js | Documentos de Microsoft
description: "Obtenga información acerca de cómo toobuild una Node.js web API que acepta los tokens de una cuenta Microsoft personal y de cuentas profesionales o educativas."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 0b572fc1-2aaf-4cb6-82de-63010fb1941d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 219e324cca11e107186b7e5f995589b9260af8a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-api-by-using-nodejs"></a>Protección de una API web mediante Node.js
> [!NOTE]
> No todas las características y escenarios de Azure Active Directory funcionan con el punto de conexión de hello v2.0. toodetermine si debe utilizar Hola v2.0 extremo u Hola v1.0, conozca [v2.0 limitaciones](active-directory-v2-limitations.md).
> 
> 

Cuando se usa el punto de conexión de hello Azure Active Directory (Azure AD) v2.0, puede usar [OAuth 2.0](active-directory-v2-protocols.md) tooprotect los tokens de acceso a la API web. Con los tokens de OAuth 2.0, los usuarios que tienen una cuenta Microsoft personal, y cuentas profesionales o educativas, pueden acceder de forma segura a su API web.

*Passport* es middleware de autenticación para Node.js. Passport, flexible y modular, se puede usar discretamente en cualquier aplicación web de Restify o basada en Express. En esta herramienta, un conjunto completo de estrategias admite la autenticación mediante nombre de usuario y contraseña, Facebook, Twitter y mucho más. Hemos desarrollado una estrategia para Azure AD. En este artículo, le mostramos cómo tooinstall Hola módulo y, a continuación, agregue hello Azure AD `passport-azure-ad` complemento.

## <a name="download"></a>Descargar
código de Hello para este tutorial se mantiene [en GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs). tutorial de hello toofollow, puede [descargar el esqueleto de la aplicación hello como un archivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip), o un clon Hola esqueleto:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

También puede obtener la aplicación hello completado final Hola de este tutorial.

## <a name="1-register-an-app"></a>1: Registro de una aplicación
Crear una nueva aplicación en [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), o seguir [estos pasos detallan](active-directory-v2-app-registration.md) tooregister una aplicación. Asegúrese de lo siguiente:

* Hola copia **Id. de aplicación** asignado tooyour aplicación. Lo necesitará para este tutorial.
* Agregar hello **Mobile** plataforma para la aplicación.
* Hola copia **URI de redireccionamiento** desde el portal de Hola. Debe usar el valor de identificador URI predeterminado de Hola de `urn:ietf:wg:oauth:2.0:oob`.

## <a name="2-install-nodejs"></a>2: Instalación de Node.js
ejemplo de Hola a toouse para este tutorial, debe [instalar Node.js](http://nodejs.org).

## <a name="3-install-mongodb"></a>3: Instalación de MongoDB
toosuccessfully utilizar este ejemplo, debe [instalar MongoDB](http://www.mongodb.org). En este ejemplo, utilizará MongoDB toomake la API de REST persistente en instancias del servidor.

> [!NOTE]
> En este artículo, supondremos que usan Hola instalación y servidor de puntos de conexión predeterminados para MongoDB: mongodb://localhost.
> 
> 

## <a name="4-install-hello-restify-modules-in-your-web-api"></a>4: instalar hello restify módulos en la API web
Utilizamos Resitfy toobuild nuestra API de REST. Restify es un marco de trabajo de la aplicación de Node.js mínimo y flexible que se deriva de Express. Restify tiene un conjunto robusto de características que puede usar toobuild encima de conectar las API de REST.

### <a name="install-restify"></a>Instalación de Restify
1.  En un símbolo del sistema, cambie el directorio de hello demasiado**organización**:

    `cd azuread`

    Si hello **organización** directorio no existe, créelo:

    `mkdir azuread`

2.  Instale Restify:

    `npm install restify`

    resultado de Hello de este comando debe tener este aspecto:

    ```
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
    └── bunyan@0.22.0(mv@0.0.5)
    ```

#### <a name="did-you-get-an-error"></a>¿Ha recibido un error?
En algunos sistemas operativos, cuando se usa hello `npm` comando, verá este mensaje: `Error: EPERM, chmod '/usr/local/bin/..'`. error de Hello va seguido de una solicitud que intentas ejecución cuenta de hello como administrador. Si esto ocurre, use el comando de hello `sudo` toorun `npm` en un nivel de privilegios superior.

#### <a name="did-you-get-an-error-related-toodtrace"></a>¿Obtuvo un error relacionado con tooDTrace?
Al instalar Restify, podría aparecer este mensaje:

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: two
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

Restify tiene un tootrace un mecanismo eficaz llamadas REST mediante el uso de DTrace. Sin embargo, DTrace no está disponible en muchos sistemas operativos. Puede omitir estos errores.


## <a name="5-install-passportjs-in-your-web-api"></a>Paso 5: Instalación de Passport.js en su API web
1.  En hello símbolo del sistema, cambie el directorio de hello demasiado**organización**.

2.  Instale Passport.js:

    `npm install passport`

    Hola resultado del comando de hello debería tener este aspecto:

    ```
     passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3
    ```

## <a name="6-add-passport-azure-ad-tooyour-web-api"></a>6: agregar ad de azure de passport tooyour web API
A continuación, agregue la estrategia de OAuth de hello, mediante el uso de la organización de passport. `passport-azuread` es un conjunto de estrategias que conectan Azure AD a Passport. En este ejemplo de API de REST, esta estrategia se usa para los tokens de portador.

> [!NOTE]
> Aunque OAuth 2.0 proporciona un marco en el que se puede emitir cualquier tipo de token conocido, habitualmente se usan determinados tipos de token. Tokens de portador son puntos de conexión de tooprotect utilizadas. Tokens de portador son tipo de hello emitido más comúnmente de token de OAuth 2.0. Muchas implementaciones de OAuth 2.0, se supone que los tokens de portador son Hola único tipo de token emitido.
> 
> 

1.  En un símbolo del sistema, cambie el directorio de hello demasiado**organización**.

    `cd azuread`

2.  Instalar hello Passport.js `passport-azure-ad` módulo:

    `npm install passport-azure-ad`

    Hola resultado del comando de hello debería tener este aspecto:

    ```
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
    ```

## <a name="7-add-mongodb-modules-tooyour-web-api"></a>7: agregar MongoDB módulos tooyour web API
En este ejemplo, utilizamos MongoDB como el almacén de datos. 

1.  Instalar Mongoose, ampliamente utilizado complemento, toomanage modelos y esquemas: 

    `npm install mongoose`

2.  Instalar el controlador de la base de datos de Hola para MongoDB, que también se denomina MongoDB:

    `npm install mongodb`

## <a name="8-install-additional-modules"></a>8: Instalar módulos adicionales
Instalar Hola restantes módulos necesarios.

1.  En un símbolo del sistema, cambie el directorio de hello demasiado**organización**:

    `cd azuread`

2.  Escriba Hola siga los comandos. comandos de Hello instalan Hola después de módulos en el directorio node_modules:

    *   `npm install crypto`
    *   `npm install assert-plus`
    *   `npm install posix-getopt`
    *   `npm install util`
    *   `npm install path`
    *   `npm install connect`
    *   `npm install xml-crypto`
    *   `npm install xml2js`
    *   `npm install xmldom`
    *   `npm install async`
    *   `npm install request`
    *   `npm install underscore`
    *   `npm install grunt-contrib-jshint@0.1.1`
    *   `npm install grunt-contrib-nodeunit@0.1.2`
    *   `npm install grunt-contrib-watch@0.2.0`
    *   `npm install grunt@0.4.1`
    *   `npm install xtend@2.0.3`
    *   `npm install bunyan`
    *   `npm update`

## <a name="9-create-a-serverjs-file-for-your-dependencies"></a>9: Creación de un archivo server.js con sus dependencias
Un archivo de Server.js contiene la mayoría de Hola de funcionalidad de hello para el servidor de la API web. Agregue la mayor parte de su archivo de código toothis. Para fines de producción, puede refactorizar funcionalidad hello en archivos más pequeños, como para los controladores y rutas separadas que cubre. En este artículo, utilizamos Server.js para este fin.

1.  En un símbolo del sistema, cambie el directorio de hello demasiado**organización**:

    `cd azuread`

2.  Con el editor que prefiera, cree un archivo Server.js. Agregue Hola información toohello archivo siguiente:

    ```Javascript
    'use strict';
    /**
    * Module dependencies.
    */
    var util = require('util');
    var assert = require('assert-plus');
    var mongoose = require('mongoose/');
    var bunyan = require('bunyan');
    var restify = require('restify');
    var config = require('./config');
    var passport = require('passport');
    var OIDCBearerStrategy = require('passport-azure-ad').OIDCStrategy;
    ```

3.  Guarde el archivo hello. Se devolverá tooit en breve.

## <a name="10-create-a-config-file-toostore-your-azure-ad-settings"></a>10: crear un toostore del archivo de configuración de la configuración de Azure AD
Este archivo de código pasa los parámetros de configuración de Hola de su tooPassport.js de portal de Azure AD. Estos valores de configuración se crean cuando se agrega hello web API toohello el portal al principio de Hola de artículo de Hola. Después de copiar el código de hello, explicaremos qué tooput en valores de hello de estos parámetros.

1.  En un símbolo del sistema, cambie el directorio de hello demasiado**organización**:

    `cd azuread`

2.  En un editor, cree un archivo Config.js. Agregue Hola siguiente información:

    ```Javascript
    // Don't commit this file tooyour public repos. This config is for first-run.
    exports.creds = {
    mongoose_auth_local: 'mongodb://localhost/tasklist', // Your Mongo auth URI goes here.
    issuer: 'https://sts.windows.net/**<your application id>**/',
    audience: '<your redirect URI>',
    identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For Microsoft, you should never need toochange this.
    };

    ```



### <a name="required-values"></a>Valores obligatorios

*   **IdentityMetadata**: aquí es donde `passport-azure-ad` busca los datos de configuración para el proveedor de identidades (IDP) de Hola y Hola claves toovalidate Hola Tokens de Web JSON (Jwt). Si utilizas Azure AD, probablemente no desee toochange esto.

*   **audiencia**: el URI de redirección desde el portal de Hola.

> [!NOTE]
> Distribuimos sus claves con frecuencia. Asegúrese de que siempre de extracción de dirección URL de "openid_keys" Hola, y esa aplicación hello puede tener acceso a Internet de Hola.
> 
> 

## <a name="11-add-hello-configuration-tooyour-serverjs-file"></a>11: agregar tooyour Server.js archivo de configuración de Hola
La aplicación necesita valores de hello tooread del archivo de configuración de Hola que acaba de crear. Agregue el archivo .config de hello como un recurso necesario en la aplicación. Establecer hello toothose de variables globales que se encuentran en Config.js.

1.  En hello símbolo del sistema, cambie el directorio de hello demasiado**organización**:

    `cd azuread`

2.  En un editor, abra Server.js. Agregue Hola siguiente información:

    ```Javascript
    var config = require('./config');
    ```

3.  Agregue un nuevo tooServer.js de sección:

    ```Javascript
    // Pass these options in toohello ODICBearerStrategy.
    var options = {
    // hello URL of hello metadata document for your app. Put hello keys for token validation from hello URL found in hello jwks_uri tag in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    issuer: config.creds.issuer,
    audience: config.creds.audience
    };
    // Array toohold signed-in users and hello current signed-in user (owner).
    var users = [];
    var owner = null;
    // Your logger
    var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
    });
    ```

## <a name="12-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>12: agregar Hola MongoDB modelo e información de esquema mediante Mongoose
Después, conecte estos tres archivos en un servicio de API de REST.

En este artículo, utilizamos MongoDB toostore nuestro tareas. Se explican en el *paso 4*.

En el archivo de hello Config.js que creó en el paso 11, se llama a la base de datos *tasklist*. Eso estaba coloca al final de saludo de la dirección URL de conexión de mongoose_auth_local. No es necesario toocreate esta base de datos con antelación en MongoDB. Hola crear base de datos en hello primero ejecución de la aplicación de servidor (suponiendo que la base de datos de hello aún no existe).

Ha dijo a servidor hello qué toouse de base de datos de MongoDB. A continuación, debe toowrite algunos modelos de código adicional toocreate Hola y el esquema para las tareas de su servidor.

### <a name="hello-model"></a>modelo de Hola
modelo de esquema de Hello es muy básica. Puede expandirlo si lo necesita. 

modelo de esquema de Hello tiene estos valores:

*   **NAME**. tarea de Hello persona toohello asignado. Se trata de un valor de **cadena**.
*   **TASK**. nombre de Hola de tarea hello. Se trata de un valor de **cadena**.
*   **DATE**. fecha de Hello vence esa tarea hello. Se trata de un **datetime** valor.
*   **COMPLETED**. Si se completa la tarea hello. Se trata de un elemento **booleano**.

### <a name="create-hello-schema-in-hello-code"></a>Crear esquemas de hello en el código de hello
1.  En un símbolo del sistema, cambie el directorio de hello demasiado**organización**:

    `cd azuread`

2.  En el editor, abra Server.js. Por debajo de la entrada de configuración de hello, agregue Hola siguiente información:

    ```Javascript
    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');
    ```

Este código conecta toohello MongoDB server. También devuelve un objeto de esquema.

#### <a name="using-hello-schema-create-your-model-in-hello-code"></a>Usa el esquema de hello, crear el modelo en el código de hello
Debajo de hello anterior de código, agregue Hola siguiente código:

```Javascript
// Create a basic schema toostore your tasks and users.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use hello schema tooregister a model.
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```

Como puede imaginar desde el código de hello, primero debe crear el esquema. Después, un objeto de modelo. Usar toostore de objeto de modelo de hello los datos a lo largo de Hola de código cuando se define la **rutas**.

## <a name="13-add-your-routes-for-your-task-rest-api-server"></a>13: Incorporación de las rutas para el servidor de API de REST de su tarea
Ahora que tiene un toowork de modelo de base de datos con, agregar rutas de Hola que va a utilizar para el servidor de la API de REST.

### <a name="about-routes-in-restify"></a>Información de las rutas en Restify
Rutas de restify trabajo exactamente hello igual que lo hacen cuando se usa Hola pila de Express. Definir las rutas mediante el uso de URI que se espera toocall de las aplicaciones de cliente de Hola Hola. Normalmente, las rutas se definen en un archivo independiente. En este tutorial, colocamos nuestra rutas en Server.js. Se recomienda diseñarlas en su propio archivo para que se puedan usar en producción.

Un patrón típico de una ruta Restify es:

```Javascript
function createObject(req, res, next) {
// Do work on object.
_object.name = req.params.object; // Passed value is in req.params under object.
///...
return next(); // Keep hello server going.
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


Este es el patrón de hello en el nivel más básico de Hola. Restify (y Express) proporcionan una funcionalidad mucho más profunda, como tipos de aplicaciones de toodefine de capacidad de Hola y el enrutamiento complejo en distintos puntos de conexión.

#### <a name="add-default-routes-tooyour-server"></a>Agregar servidor de forma predeterminada las rutas tooyour
Agregar rutas de hello básicas CRUD: **crear**, **recuperar**, **actualizar**, y **eliminar**.

1.  En un símbolo del sistema, cambie el directorio de hello demasiado**organización**:

    `cd azuread`

2.  En un editor, abra Server.js. A continuación Hola entradas de base de datos realizadas anteriormente, agregue Hola siguiente información:

    ```Javascript
    /**
    *
    * APIs for your REST task server
    */
    // Create a task.
    function createTask(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow you toouse MongoDB Server as your response tooany origin.
    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");
    // Create a new task model, fill it, and save it tooMongoDB.
    var _task = new Task();
    if (!req.params.task) {
    req.log.warn({
    params: p
    }, 'createTodo: missing task');
    next(new MissingTaskError());
    return;
    }
    _task.owner = owner;
    _task.task = req.params.task;
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
    // Delete a task by name.
    function removeTask(req, res, next) {
    Task.remove({
    task: req.params.task,
    owner: owner
    }, function(err) {
    if (err) {
    req.log.warn(err,
    'removeTask: unable toodelete %s',
    req.params.task);
    next(err);
    } else {
    log.info('Deleted task:', req.params.task);
    res.send(204);
    next();
    }
    });
    }
    // Delete all tasks.
    function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
    }
    // Get a specific task based on name.
    function getTask(req, res, next) {
    log.info('getTask was called for: ', owner);
    Task.find({
    owner: owner
    }, function(err, data) {
    if (err) {
    req.log.warn(err, 'get: unable tooread %s', owner);
    next(err);
    return;
    }
    res.json(data);
    });
    return next();
    }
    /// Returns hello list of TODOs that were loaded.
    function listTasks(req, res, next) {
    // Resitify currently has a bug that doesn't allow you tooset default headers.
    // These headers comply with CORS, and allow us toouse MongoDB Server as our response tooany origin.
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
    log.warn(err, "There are no tasks in hello database. Add one!");
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

### <a name="add-error-handling-for-hello-routes"></a>Agregar control de errores para las rutas de Hola
Agregue algunos control de errores de forma que pueda comunicarse a toohello atrás cliente acerca de cómo detectó un problema en Hola.

Agregue Hola siguiendo el siguiente código de hello, que ya ha escrito código:

```Javascript
///--- Errors for communicating something more information back toohello client.
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


## <a name="14-create-your-server"></a>14: Creación del servidor
Hola toodo de lo último es tooadd la instancia del servidor. instancia del servidor Hello controla sus llamadas.

Restify (y Express) tiene una personalización más avanzada que puede usar con un servidor de API de REST. En este tutorial, se usa el programa de instalación más sencilla de Hola.

```Javascript
/**
* Your server
*/
var server = restify.createServer({
name: "Microsoft Azure Active Directory TODO Server",
version: "2.0.1"
});
// Ensure that you don't drop data on uploads.
server.pre(restify.pre.pause());
// Clean up imprecise paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());
// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());
// Set a per-request Bunyan logger (with requestid filled in).
server.use(restify.requestLogger());
// Allow 5 requests/second by IP address, and burst too10.
server.use(restify.throttle({
burst: 10,
rate: 5,
ip: true,
}));
// Use common commands, such as:
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
mapParams: true
}));
```
## <a name="15-add-hello-routes-without-authentication-for-now"></a>15: agregar rutas de hello (sin autenticación, por ahora)
```Javascript
/// Use CRUD tooadd hello real handlers.
/**
/*
/* Each of these handlers is protected by your Open ID Connect Bearer strategy. Invoke 'oidc-bearer'
/* in hello pasport.authenticate() method. Because REST is stateless, set 'session: false'. You 
/* don't need toomaintain session state. You can experiment with removing API protection.
/* toodo this, remove hello passport.authenticate() method:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-run-hello-server"></a>16: ejecutar servidor hello
Es una buena idea tootest el servidor antes de agregar la autenticación.

Hola tootest de manera más fácil su servidor consiste en usar curl en un símbolo del sistema. toodo, necesita una utilidad simple que pueden usar tooparse salida como JSON. 

1.  Instale la herramienta JSON de Hola que utilizamos en hello en los ejemplos siguientes:

    `$npm install -g jsontool`

    Esto instala herramienta JSON de hello globalmente.

2.  Asegúrese de que la instancia de MongoDB se esté ejecutando:

    `$sudo mongod`

3.  Cambie el directorio de hello demasiado**organización**, y, a continuación, ejecute curl:

    `$ cd azuread`
    `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 2.0OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4.  tooadd una tarea:

    `$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

    respuesta de Hello debe ser:

    ```Shell
    HTTP/1.1 201 Created
    Connection: close
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Headers: X-Requested-With
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 5
    Date: Tue, 04 Feb 2014 01:02:26 GMT
    Hello
    ```

5.  Lista de tareas de Brandon:

    `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

Si todos estos comandos se ejecutan sin errores, es el servidor de la API de REST de listo tooadd OAuth toohello.

*Ahora tiene un servidor de API de REST con MongoDB.*

## <a name="17-add-authentication-tooyour-rest-api-server"></a>17: Agregar servidor de la API de REST de autenticación tooyour
Ahora que tiene una API de REST de ejecución, se configura toouse con Azure AD.

En un símbolo del sistema, cambie el directorio de hello demasiado**organización**:

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-thats-included-with-passport-azure-ad"></a>Use hello oidcbearerstrategy que se incluye con azure de passport de ad
Hasta ahora hemos creado un servidor típico de TODO de REST sin ningún tipo de autorización. Ahora, agregue la autenticación.

En primer lugar, indique que desea que toouse Passport. Incluya esto justo después de la configuración del servidor anterior:

```Javascript
// Start using Passport.js.

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> Al escribir las API, es un Hola de vínculo de tooalways buena idea toosomething de datos único del token de Hola que Hola usuario no se puede suplantar la identidad. Cuando este servidor almacena elementos de lista de tareas, almacena en función del Id. de suscripción de usuario de Hola de símbolo (token) de hello (llamado a través de token.sub). Coloque token.sub hello en el campo de "propietario" Hola. Esto garantiza que sólo ese usuario puede tener acceso a TODOs del usuario de Hola. Nadie más puede tener acceso a TODOs Hola que se especificaron. No hay ningún riesgo en hello API para el "propietario". Un usuario externo puede solicitar las tareas pendientes de otros usuarios, incluso si estos se autentican.
> 
> 

A continuación, use la estrategia de portador de conectarse de identificador abierto de Hola que viene con `passport-azure-ad`. Colóquela después de lo que pegó anteriormente:

```Javascript
/**
/*
/* Calling hello OIDCBearerStrategy and managing users.
/*
/* Because of hello Passport pattern, you need toomanage users and info tokens
/* with a FindorCreate() method. hello method must be provided by hello implementor.
/* In hello following code, you autoregister any user and implement a FindById().
/* It's a good idea toodo something more advanced.
**/
var findById = function(id, fn) {
for (var i = 0, len = users.length; i < len; i++) {
var user = users[i];
if (user.sub === id) {
log.info('Found user: ', user);
return fn(null, user);
}
}
return fn(null, null);
};
var oidcStrategy = new OIDCBearerStrategy(options,
function(token, done) {
log.info('verifying hello user');
log.info(token, 'was hello token retrieved');
findById(token.sub, function(err, user) {
if (err) {
return done(err);
}
if (!user) {
// "Auto-registration"
log.info('User was added automatically, because they were new. Their sub is: ', token.sub);
users.push(token);
owner = token.sub;
return done(null, token);
}
owner = token.sub;
return done(null, user, token);
});
}
);
passport.use(oidcStrategy);
```

Passport usa un patrón similar para todas sus estrategias (Twitter, Facebook, etc.). Todos los escritores de estrategia cumplen toohello patrón. Pasar la estrategia de hello un `function()` que usa un token y `done` como parámetros. estrategia de Hola se devuelve cuando hace todo su trabajo. Almacenar usuario hello y token de hello complementario por lo que no necesita tooask para ella de nuevo.

> [!IMPORTANT]
> Hello código anterior toma cualquier usuario que puede autenticar el servidor de tooyour. Esto se conoce como registro automático. En un servidor de producción, desearía toolet cualquiera sin tener primero que les vaya a través de un proceso de registro que elija. Se trata normalmente de patrón de Hola que se ven en las aplicaciones de consumidor. aplicación Hello podrían tooregister con Facebook, pero, a continuación, le pide que tooenter obtener información adicional. Si no usa un programa de línea de comandos para este tutorial, podría extraer correo electrónico de Hola de objeto de símbolo (token) de Hola que se devuelve. A continuación, podría solicitar información adicional de hello usuario tooenter. Dado que se trata de un servidor de prueba, agregar usuario Hola directamente toohello en la memoria de base de datos.
> 
> 

### <a name="protect-endpoints"></a>Protección de los puntos de conexión
Proteger los puntos de conexión mediante la especificación de hello **passport.authenticate()** llamada con protocolo de Hola que desea toouse.

Puede editar la ruta en el código del servidor para ver una opción más avanzada:

```Javascript
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="18-run-your-server-application-again"></a>18: Reejecución de la aplicación de servidor
Use nuevo curl toosee si tiene protección de OAuth 2.0 en los extremos. Haga esto antes de ejecutar cualquiera de nuestros SDK de cliente en este punto de conexión. encabezados de Hello devueltos deben indicar si la autenticación está funcionando correctamente.

1.  Asegúrese de que la instancia de MongoDB se esté ejecutando:

    `$sudo mongod`

2.  Cambiar toohello **organización** directorio y, a continuación, use curl:

    `$ cd azuread`

    `$ node server.js`

3.  Pruebe una operación POST básica:

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

Una respuesta 401 indica dicho nivel de Passport Hola está tratando de tooredirect toohello extremo authorize, que es exactamente lo que desea.

*Ahora tiene un servicio de API de REST que usa OAuth 2.0.*

Ha avanzado todo lo posible con este servidor sin usar un cliente compatible con OAuth 2.0. Para ello, deberá tooreview un tutorial adicional.

## <a name="next-steps"></a>Pasos siguientes
Como referencia, ejemplo de Hola finalizado (sin los valores de configuración) se proporciona como [un archivo .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip). También puede clonarlo desde GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

Ahora, puede mover en toomore temas avanzados. Es recomendable tootry [proteger una aplicación web de Node.js con el punto de conexión de hello v2.0](active-directory-v2-devquickstarts-node-web.md).

Estos son algunos recursos adicionales:

* [Guía del desarrollador de Azure AD v2.0](active-directory-appmodel-v2-overview.md)
* [Etiqueta "azure-active-directory" de Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>Obtención de actualizaciones de seguridad para nuestros productos
Recomendamos que toosign una toobe una notificación cuando se produzcan incidentes de seguridad. En hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) página, subscribe tooSecurity avisos de alertas.

