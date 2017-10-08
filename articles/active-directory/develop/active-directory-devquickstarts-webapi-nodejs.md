---
title: "aaaAzure AD Node.js Introducción | Documentos de Microsoft"
description: "¿Cómo toobuild una API de REST de Node.js web que se integra con Azure AD para la autenticación."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a>Introducción a las API web para Node.js
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

*Passport* es middleware de autenticación para Node.js. Flexible y modular, Passport puede quitarse de forma discreta en tooany basada en Express o Restify la aplicación web. Un conjunto completo de estrategias da soporte a la autenticación con nombre de usuario y contraseña, Facebook, Twitter, etc. Hemos desarrollado una estrategia para Microsoft Azure Active Directory (Azure AD). Se instale este módulo y, a continuación, agregue Hola Microsoft Azure Active Directory `passport-azure-ad` complemento.

toodo, necesita:

1. Registrar una aplicación con Azure AD.
2. Configurar la aplicación toouse Passport `passport-azure-ad` complemento.
3. Configurar un cliente aplicación toocall hello tooDo lista API web.

código de Hello para este tutorial se mantiene [en GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).

> [!NOTE]
> Este artículo no tratan cómo tooimplement sesión, inicio de sesión, o generar perfiles de administración con Azure AD B2C. Se centra en las API de web que realiza la llamada después de hello usuario ya está autenticado.  Es recomendable que comience con [cómo toointegrate con documentos de Azure Active Directory](active-directory-how-to-integrate.md) toolearn sobre conceptos básicos de Hola de Azure Active Directory.
>
>

Por lo que lanzamos todo código fuente de hello en este ejemplo en GitHub bajo una licencia MIT, sentirse tooclone libre (o incluso mejor, bifurcar) y proporcionar comentarios y solicitudes de extracción.

## <a name="about-nodejs-modules"></a>Acerca de los módulos Node.js
En este tutorial se usan módulos Node.js. Los módulos son paquetes JavaScript que pueden cargarse y que proporcionan una funcionalidad específica para su aplicación. Normalmente se instale módulos mediante hello Node.js una herramienta de línea de comandos de NPM en directorio de instalación de NPM Hola. Sin embargo, algunos módulos, como el módulo HTTP de hello, se incluyen en el paquete de Node.js del núcleo de Hola.

Módulos instalados se guardan en hello **node_modules** directorio raíz de Hola de su directorio de instalación de Node.js. Cada módulo en hello **node_modules** directory mantiene su propio **node_modules** directorio que contiene los módulos que depende. Además, cada módulo requerido tiene un directorio **node_modules**. Esta estructura de directorios recursiva representa la cadena de dependencia de Hola.

Esta estructura de la cadena de dependencias da como resultado una mayor superficie de la aplicación. Pero también garantiza que se cumplen todas las dependencias y esa versión de Hola de módulos de Hola que se usa en el desarrollo también se utiliza en producción. Esto facilita comportamientos de la aplicación de producción de hello más predecible y evita los problemas de control de versiones que podrían afectar a los usuarios.

## <a name="step-1-register-an-azure-ad-tenant"></a>Paso 1: Registro de un inquilino de Azure AD
toouse este ejemplo, necesita un inquilino de Azure Active Directory. Si no está seguro de qué un inquilino o tooget uno, vea [cómo inquilino tooget un Azure AD](active-directory-howto-tenant.md).

## <a name="step-2-create-an-application"></a>Paso 2: Creación de una aplicación
A continuación, creará una aplicación en el directorio que ofrece Azure AD información que necesita toosecurely comunicarse con la aplicación.  Aplicación de cliente de hello y API web se representan mediante una sola **Id. de aplicación** en este caso, porque están formadas por una aplicación lógica.  toocreate una aplicación, siga [estas instrucciones](active-directory-how-applications-are-added.md). Si va a crear una aplicación de línea de negocio [es posible que estas instrucciones adicionales le resulten útiles](../active-directory-applications-guiding-developers-for-lob-applications.md).

toocreate una aplicación:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

2. En el menú superior de hello, seleccione su cuenta. A continuación, en hello **Directory** lista, seleccione la aplicación de inquilino de Active Directory de Hola donde desea tooregister.

3. En el menú de Hola Hola izquierda, seleccione **más servicios**y, a continuación, seleccione **Azure Active Directory**.

4. Seleccione **Registros de aplicaciones** y luego seleccione **Agregar**.

5. Siga Hola indicaciones toocreate una **aplicación Web o WebAPI**.

      * Hola **nombre** de hello aplicación describe los usuarios de tooend de aplicación.

      * Hola **dirección URL de inicio de sesión** es Hola dirección URL base de la aplicación.  Hola predeterminado es la dirección URL del código de ejemplo de Hola `https://localhost:8080`.

6. Después de registrarse, Azure AD asigna a su aplicación un identificador de aplicación individual. Se necesita este valor en las secciones siguientes de hello, por lo tanto cópiela desde la página de aplicación Hola.

7. De hello **configuración** -> **propiedades** página de la aplicación, actualice Hola App ID URI. Hola **App ID URI** es un identificador único para la aplicación. convención de Hello es toouse `https://<tenant-domain>/<app-name>`, por ejemplo: `https://contoso.onmicrosoft.com/my-first-aad-app`.

8. Crear un **clave** para la aplicación de hello **configuración** página y, a continuación, cópielo en otro. La necesitará en breve.

## <a name="step-3-download-nodejs-for-your-platform"></a>Paso 3: Descarga de Node.js para la plataforma
toosuccessfully utilizar este ejemplo, debe tener una instalación activa de Node.js.

Instale Node.js desde [http://nodejs.org](http://nodejs.org).

## <a name="step-4-install-mongodb-on-your-platform"></a>Paso 4: Instalación de MongoDB en la plataforma
toosuccessfully utilizar este ejemplo, debe tener una instalación activa de MongoDB. Utilice MongoDB toomake Hola API de REST persistente en instancias del servidor.

Instale MongoDB desde [http://mongodb.org](http://www.mongodb.org).

> [!NOTE]
> Este tutorial se supone que utiliza Hola instalación y servidor de puntos de conexión predeterminados para MongoDB, que en tiempo de Hola de redactar este artículo es mongodb://localhost.
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a>Paso 5: Instalar los módulos de Restify hello en la API web
Estamos usando Restify toobuild nuestra API de REST. Restify es un marco de trabajo de la aplicación de Node.js mínimo y flexible que se deriva de Express. Tiene un sólido conjunto de características para crear API de REST sobre Connect.

### <a name="install-restify"></a>Instalar Restify
1. Desde la línea de comandos de hello, cambiar directorios toohello **organización** directory. Si hello **organización** directorio no existe, créelo.

        `cd azuread - or- mkdir azuread; cd azuread`

2. Escriba el siguiente comando de hello:

    `npm install restify`

    Este comando instala Restify.

#### <a name="did-you-get-an-error"></a>¿Ha recibido un error?
Si se usa NPM en algunos sistemas operativos, se puede que recibir el siguiente mensaje **Error: EPERM, chmod "/usr/local/bin/.."** y una sugerencia que intentas ejecución cuenta de hello como administrador. Si esto ocurre, use hello sudo comando toorun NPM con un nivel de privilegios superior.

#### <a name="did-you-get-an-error-regarding-dtrace"></a>¿Ha recibido un error relacionado con DTRACE?
Al instalar Restify puede que vea un error similar al siguiente:

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
Restify proporciona un mecanismo eficaz para rastrear llamadas a REST mediante DTrace. Sin embargo, muchos sistemas operativos no tienen DTrace. Puede omitir estos errores con seguridad.

salida de Hello de este comando debe ser similar toohello después de salida:

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


## <a name="step-6-install-passportjs-in-your-web-api"></a>Paso 6: Instalación de Passport.js en su API web
[Passport](http://passportjs.org/) es middleware de autenticación para Node.js. Flexible y modular, Passport puede quitarse de forma discreta en tooany basada en Express o Restify la aplicación web. Un conjunto completo de estrategias da soporte a la autenticación con nombre de usuario y contraseña, Facebook, Twitter, etc.

Hemos desarrollado una estrategia para Azure Active Directory. Se instala este módulo y, a continuación, agrega la estrategia de Azure Active Directory Hola complemento.

1. Desde la línea de comandos de hello, cambiar directorios toohello **organización** directory.

2. tooinstall passport.js, escriba el siguiente comando de hello:

    `npm install passport`

    salida de Hello de comando hello debería ser similar siguiente toohello:

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a>Paso 7: Agregar AD de Azure de Passport tooyour web API
A continuación, agregamos estrategia de OAuth de hello mediante el uso de `passport-azure-ad`, un conjunto de estrategias que se conectan tooPassport de Azure Active Directory. En este ejemplo de API de REST, esta estrategia se usa para los tokens de portador.

> [!NOTE]
> Aunque OAuth2 proporciona un marco en el que se puede emitir cualquier tipo de token conocido, habitualmente solo se usan determinados tipos de token. Tokens de portador son tokens de hello suelen usada para proteger los puntos de conexión. Son tipo hello emitido más comúnmente del token de OAuth2. Muchas implementaciones, se supone que los tokens de portador son Hola único tipo de tokens emitidos.
>
>

Desde la línea de comandos de hello, cambiar directorios toohello **organización** directory.

Escriba lo siguiente Hola comando hello tooinstall Passport.js `passport-azure-ad module`:

`npm install passport-azure-ad`

resultado de Hello de comando de Hola debería ser similar toohello después de salida:


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



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a>Paso 8: Agregar MongoDB módulos tooyour web API
MongoDB se usa como almacén de datos. Por esta razón, es necesario tooinstall Hola usadas de complemento llamados modelos de toomanage Mongoose y esquemas. También es necesario el controlador de base de datos de hello tooinstall para MongoDB (conocida también como MongoDB).

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a>Paso 9: Instalación de módulos adicionales
A continuación se instale Hola restantes módulos necesarios.

1. Desde la línea de comandos de hello, cambiar directorios toohello **organización** carpeta si no está ya no existe.

    `cd azuread`

2. Escriba Hola después comandos tooinstall estos módulos en su **node_modules** directorio:

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a>Paso 10: Creación de server.js con sus dependencias
archivo de Hello server.js proporciona la mayor parte de la funcionalidad de hello para el servidor de la API web. Agregamos la mayor parte de nuestro archivo de código toothis. Para fines de producción, se recomienda refactorizar funcionalidad hello en archivos más pequeños, como rutas independientes y controladores. En esta demostración, se usa server.js para esta funcionalidad.

1. Desde la línea de comandos de hello, cambiar directorios toohello **organización** carpeta si no está ya no existe.

    `cd azuread`

2. Crear un `server.js` un archivo en el editor que prefiera y después agregue Hola siguiente información:

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. Guarde el archivo hello. Volverás tooit en breve.

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a>Paso 11: Crear un toostore del archivo de configuración de la configuración de Azure AD
Este archivo de código pasa los parámetros de configuración de Hola de su tooPassport.js de portal de Azure Active Directory. Estos valores de configuración se crean cuando se agrega hello web API toohello el portal en la primera parte del tutorial Hola de Hola. Se explica qué tooput en valores de hello de estos parámetros después de copiar el código de hello.

1. Desde la línea de comandos de hello, cambiar directorios toohello **organización** carpeta si no está ya no existe.

    `cd azuread`

2. Crear un `config.js` un archivo en el editor que prefiera y después agregue Hola siguiente información:

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. Guarde el archivo hello.

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a>Paso 12: Agregar el archivo de configuración de valores tooyour server.js
Necesitamos tooread estos valores desde el archivo .config de Hola que creaste en nuestra aplicación. toodo, agregamos archivo .config de hello como un recurso necesario en nuestra aplicación. A continuación, se establecer variables de Hola de toomatch de variables globales de hello en documento config.js de Hola.

1. Desde la línea de comandos de hello, cambiar directorios toohello **organización** carpeta si no está ya no existe.

    `cd azuread`

2. Abra su `server.js` un archivo en el editor que prefiera y después agregue Hola siguiente información:

    ```Javascript
    var config = require('./config');
    ```
3. A continuación, agregue una nueva sección demasiado`server.js` con hello siguiente código:

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. Guarde el archivo hello.

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>Paso 13: Agregar Hola MongoDB modelo e información de esquema mediante Mongoose
Ahora toda esta preparación va toostart buenos resultados tal y como se combinan estos tres archivos en un servicio de API de REST.

En este tutorial, usamos MongoDB toostore nuestro tareas tal como se describe en el paso 4.

Hola `config.js` que hemos creado en el paso 11, llamamos a nuestra base de datos de archivo `tasklist`, porque ese era colocamos final Hola de nuestro **mogoose_auth_local** dirección URL de conexión. No es necesario toocreate esta base de datos con antelación en MongoDB. En su lugar, MongoDB esto para que podamos en hello primero crea ejecución de nuestra aplicación de servidor (suponiendo que aún no existe esa base de datos de hello).

Ahora que hemos dicho servidor hello a qué base de datos de MongoDB nos gustaría toouse, es necesario toowrite algunos modelos de código adicional toocreate Hola y el esquema para las tareas del servidor.

### <a name="discussion-of-hello-model"></a>Descripción del modelo de Hola
Nuestro modelo de esquema es muy sencillo. Expándalo si fuera necesario.

NOMBRE: nombre de Hola de hello quien se asigna la tarea de toohello. Un valor de **cadena**.

TAREA: hello propia tarea. Un valor de **cadena**.

Fecha: Hola esa tarea hello es debida. Un valor **DATETIME**.

COMPLETADO: Si tiene la tarea hello ha completado o no. Un valor **booleano**.

### <a name="creating-hello-schema-in-hello-code"></a>Crear el esquema de hello en el código de hello
1. Desde la línea de comandos de hello, cambiar directorios toohello **organización** carpeta si no está ya no existe.

    `cd azuread`

2. Abra su `server.js` un archivo en el editor que prefiera y después agregue Hola siguiendo la información que aparece debajo de la entrada de configuración de hello:

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
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
Como puede imaginar desde el código de hello, crearemos nuestro esquema primero. A continuación, se crea un objeto de modelo que utilizamos toostore nuestros datos a lo largo de hello código cuando se definen nuestro **rutas**.

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a>Paso 14: Adición de rutas para el servidor de API de REST de la tarea
Ahora que tenemos un toowork de modelo de base de datos con, vamos a agregar rutas de hello estamos uso continuo para el servidor de API de REST.

### <a name="about-routes-in-restify"></a>Información acerca de las rutas en Restify
Rutas de trabajo en Restify Hola igual manera que en hello Express en la pila. Definir las rutas mediante el uso de URI que se espera toocall de las aplicaciones de cliente de Hola Hola. Normalmente, las rutas se definen en un archivo independiente. Para nuestros propósitos, colocamos nuestra rutas de archivo de hello server.js. Se recomienda factorizarlas en su propio archivo para que se puedan usar en producción.

Este es un patrón típico de una ruta de Restify:

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


Este es el patrón de hello en su nivel más básico. Restify (y Express) proporcionan una funcionalidad mucho más profunda, como definir los tipos de aplicación y proporcionar un enrutamiento complejo en distintos puntos de conexión. Estas rutas van a ser simples.

### <a name="add-default-routes-tooour-server"></a>Agregar servidor de forma predeterminada las rutas tooour
Ahora agregar hello básico CRUD de las rutas de crear, recuperar, actualizar y eliminar.

1. Desde la línea de comandos de hello, cambiar directorios toohello **organización** carpeta si no está ya no existe:

    `cd azuread`

2. Abra hello `server.js` un archivo en el editor que prefiera y después agregue Hola siguiendo la información que aparece debajo de hello base de datos las entradas anteriores que haya realizado:

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
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

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
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

### <a name="add-error-handling-in-our-apis"></a>Incorporación del control de errores a nuestras API
```

///--- Errors for communicating something interesting back toohello client.

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


## <a name="step-15-create-your-server"></a>Paso 15: Creación de un servidor
Hemos definido la base de datos y las rutas están en su lugar. Hola última cosa toodo es agregar instancia del servidor hello que administra las llamadas.

Restify (y Express) puede hacer una gran cantidad de personalización de un servidor de la API de REST, pero nuevo vamos toouse hello más básico el programa de instalación para nuestros propósitos.

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a>Paso 16: Agregar servidor de toohello de rutas de hello (sin autenticación por ahora)
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
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
// Register a default '/' handler.
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

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a>Paso 17: Ejecutar servidor hello (antes de agregar compatibilidad con OAuth)
Pruebe el servidor antes de agregar la autenticación.

Hola tootest de manera más fácil el servidor está utilizando curl en una línea de comandos. Antes de hacerlo, necesitamos una utilidad que nos permite tooparse salida como JSON.

1. Instalar Hola después de la herramienta JSON (Hola todos los ejemplos siguientes usa esta herramienta):

    `$npm install -g jsontool`

    Esto instala herramienta JSON de hello globalmente. Ahora que nos hemos realizado, vamos a reproducir con servidor hello:

2. En primer lugar, asegúrese de que se ejecuta la instancia de MongoDB:

    `$sudo mongod`

3. A continuación, cambie el directorio de toohello e iniciar volver una:

    `$ cd azuread``$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
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

4. A continuación, podemos agregar una tarea de este modo:

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

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
    Además, podemos mostrar tareas de Brandon así:

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

Si todo esto funciona, se dispone de un servidor de la API de REST de listo tooadd OAuth toohello.

Tiene un servidor de API de REST con MongoDB

## <a name="step-18-add-authentication-tooour-rest-api-server"></a>Paso 18: Agregar servidor de la API de REST de autenticación tooour
Ahora que tenemos una API de REST en ejecución, podemos empezar a darle una utilidad con Azure AD.

Desde la línea de comandos de hello, cambiar directorios toohello **organización** carpeta si no está ya no existe.

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Usar hello OIDCBearerStrategy que se incluye con azure de passport de ad
Hasta ahora hemos creado un servidor típico de TODO de REST sin ningún tipo de autorización. Finalmente, empezamos a prepararlo.

1. En primer lugar, necesitamos tooindicate que deseamos toouse Passport. Incluya esto justo después de la otra configuración del servidor:

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > No se puede suplantar al escribir las API, es recomendable que vincule siempre Hola datos toosomething único del token de Hola que Hola de usuario. Cuando este servidor almacena elementos de lista de tareas, almacena en función de hello Id. de objeto de usuario de hello en el token de hello (llamado a través de token.oid), que colocamos cuando nos en el campo de "propietario" Hola. Esto garantiza que ese usuario es el único que puede acceder a sus tareas pendientes. No hay ningún riesgo en hello API de "propietario", por lo que un usuario externo puede solicitar Hola TODOs de los demás incluso si se autentican en.                    

2. Siguiente vamos a usar la estrategia de portador de Hola que viene con `passport-azure-ad`. Examine el código de hello por ahora y explicaremos rest hello en breve. Colóquelo después de lo que pegó anteriormente:

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
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


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

Passport usa un patrón similar para todas sus estrategias (Twitter, Facebook, etc.) al que se ajustan todos los escritores de estrategias. Examinando la estrategia de hello, verá que pasamos una función que tiene un token y un hecho como parámetros de Hola. estrategia de Hello incluye volver toous después de que realice su trabajo. Cuando lo hace, almacenamos usuario hello y token de hello complementario por lo que no necesitamos tooask para este nuevo.

> [!IMPORTANT]
> código de Hello anterior toma cualquier usuario que se produce a tooauthenticate tooour server. Esto se conoce como registro automático. En los servidores de producción, se recomienda no permitir que acceda nadie que no haya pasado por el proceso de registro que decida. Se trata normalmente de patrón de Hola que se ven en las aplicaciones de consumidor, que le permiten tooregister con Facebook, pero a continuación, pida toofill información adicional. Si esto no era un programa de línea de comandos, se pudo extrajeron correo electrónico Hola de objeto de símbolo (token) de Hola que se devuelve y, a continuación, más frecuentes Hola usuario toofill información adicional. Dado que se trata de un servidor de prueba, se debe hacer es agregar base de datos de toohello en memoria.
>
>

### <a name="protect-some-endpoints"></a>Protección de puntos de conexión
Proteger los puntos de conexión mediante la especificación de hello `passport.authenticate()` llamada con protocolo de Hola que desea toouse.

toomake nuestro código de servidor hacer algo más interesante, Editar ruta Hola.

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a>Paso 19: ejecutar de nuevo su aplicación de servidor y asegurarse de que le rechaza
Vamos a usar `curl` nuevo toosee si ahora tenemos OAuth2 protección contra nuestro puntos de conexión. Esta prueba se realiza antes de ejecutar cualquiera de nuestros SDK de cliente en este punto de conexión. Hello encabezados que se devuelven deben ser suficiente tootell nos si vamos hacia abajo de la ruta de acceso correcta de Hola.

1. En primer lugar, asegúrese de que se ejecuta la instancia de MongoDB:

    `$sudo mongod`

2. A continuación, cambie el directorio de toohello e iniciar volver una.

      `$ cd azuread``$ node server.js`

3. Pruebe una operación POST básica.

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

401 es respuesta Hola que está buscando aquí. Esta respuesta indica que capa de Passport Hola está tratando de tooredirect toohello autorizado extremo, que es exactamente lo que desea.

## <a name="next-steps"></a>Pasos siguientes
Ha avanzado todo lo posible con este servidor sin usar un cliente compatible con OAuth2. Deberá toogo a través de un tutorial adicional.

Ahora que ha aprendido cómo tooimplement una API de REST mediante el uso de Restify y OAuth2. También tiene más que suficiente tookeep código desarrollando su servicio y aprender cómo toobuild en este ejemplo.

Si está interesado en pasos de hello en su viaje AAL, presentamos algunos clientes AAL compatibles se recomienda que seguir trabajando con.

Clonar la máquina del desarrollador de tooyour y configurar como se describe en el tutorial Hola.

[ADAL para iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[ADAL para Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
