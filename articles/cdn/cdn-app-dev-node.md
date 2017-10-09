---
title: "aaaGet partió Hola CDN de Azure SDK para Node.js | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toowrite Node.js aplicaciones toomanage CDN de Azure."
services: cdn
documentationcenter: nodejs
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c4bb6a61-de3d-4f0c-9dca-202554c43dfa
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6c805e5fb8e0b471e8b248cb2f4b29efd6c85940
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a>Introducción al desarrollo de la red de entrega de contenido (CDN) de Azure
> [!div class="op_single_selector"]
> * [Node.js](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

Puede usar hello [CDN de Azure SDK para Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate creación y administración de perfiles de red CDN y puntos de conexión.  Este tutorial le guía por la creación de hello de una aplicación de consola Node.js simple que muestra algunas de las operaciones disponibles de Hola.  Este tutorial es todos los aspectos de SDK de Azure CDN Hola toodescribe no está diseñado para Node.js en detalle.

toocomplete este tutorial, debe tener ya [Node.js](http://www.nodejs.org) **4.x.x** o superior instalado y configurado.  Puede usar cualquier editor de texto que desea toocreate la aplicación de Node.js.  toowrite este tutorial, he usado [código de Visual Studio](https://code.visualstudio.com).  

> [!TIP]
> Hola [proyecto completado de este tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) está disponible para su descarga en MSDN.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a>Creación del proyecto e incorporación de dependencias NPM
Ahora que hemos creado un grupo de recursos para los perfiles de la red CDN y dada nuestra perfiles de red CDN de Azure AD aplicación permiso toomanage y los puntos de conexión dentro de ese grupo, podemos comenzar a crear nuestra aplicación.

Crear una carpeta toostore su aplicación.  Desde una consola con herramientas de Node.js de hello en la ruta de acceso actual, establecer la ubicación toothis nueva carpeta actual e inicializar el proyecto mediante la ejecución:

    npm init

A continuación, podrá presentan una serie de preguntas tooinitialize el proyecto.  Para **punto de entrada**, este tutorial usa *app.js*.  Puede ver mi otras opciones en el siguiente ejemplo de Hola.

![Salida de NPM init](./media/cdn-app-dev-node/cdn-npm-init.png)

El proyecto se inicializa ahora con un archivo *packages.json* .  Nuestro proyecto va toouse algunas bibliotecas de Azure contenidos en paquetes de NPM.  Vamos a usar en tiempo de ejecución del cliente de Azure para Node.js (ms-rest-azure) de Hola y Hola biblioteca de cliente de red CDN de Azure para Node.js (cd de arm de azure).  Vamos a agregar esos proyectos toohello como dependencias.

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

Después de hello terminados paquetes de instalación, hello *package.json* archivo debería ser similar toothis ejemplo (versión pueden variar):

``` json
{
  "name": "cdn_node",
  "version": "1.0.0",
  "description": "Azure CDN Node.js tutorial project",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Cam Soper",
  "license": "MIT",
  "dependencies": {
    "azure-arm-cdn": "^0.2.1",
    "ms-rest-azure": "^1.14.4"
  }
}
```

Por último, con su editor de texto, cree un archivo de texto en blanco y guárdela en la raíz de saludo de la carpeta del proyecto como *app.js*.  Ahora estamos listo toobegin escribir código.

## <a name="requires-constants-authentication-and-structure"></a>"Requieres", constantes, autenticación y estructura
Con *app.js* abierto en el editor, vamos a estructura básica de Hola de nuestro programa escrito.

1. Agregue Hola "requiere" para los paquetes de NPM princip Hola con siguiente hello:
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. Necesitamos toodefine algunas constantes que nuestros métodos va a usar.  Agregue Hola siguiente.  Ser seguro tooreplace marcadores de posición de hello, incluidos hello  **&lt;corchetes angulares&gt;**, con sus propios valores según sea necesario.
   
    ``` javascript
    //Tenant app constants
    const clientId = "<YOUR CLIENT ID>";
    const clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    const tenantId = "<YOUR TENANT ID>";
   
    //Application constants
    const subscriptionId = "<YOUR SUBSCRIPTION ID>";
    const resourceGroupName = "CdnConsoleTutorial";
    const resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. A continuación, se deberá crear una instancia de cliente de administración de red CDN Hola y asígnele nuestras credenciales.
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    Si utiliza la autenticación de usuario individual, estas dos líneas tendrán un aspecto algo distinto.
   
   > [!IMPORTANT]
   > Sólo puede utilizar este ejemplo de código si se elige el toohave autenticación de usuario individuales en lugar de una entidad de servicio.  Ser tooguard cuidado las credenciales de usuario individual y mantener en secreto.
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    Estar seguro tooreplace compuesta por elementos hello en  **&lt;corchetes angulares&gt;**  con hello corregir la información.  Para `<redirect URI>`, usar redirección Hola URI que especificó al registrar la aplicación hello en Azure AD.
4. Nuestra aplicación de consola Node.js va tootake algunos parámetros de línea de comandos.  Vamos a dar por válido que por lo menos un parámetro se pasó.
   
   ```javascript
   //Collect command-line parameters
   var parms = process.argv.slice(2);
   
   //Do we have parameters?
   if(parms == null || parms.length == 0)
   {
       console.log("Not enough parameters!");
       console.log("Valid commands are list, delete, create, and purge.");
       process.exit(1);
   }
   ```
5. Eso nos lleva toohello parte principal de nuestro programa, donde se separarlos tooother funciones que se basan en los parámetros que se pasaron.
   
    ```javascript
    switch(parms[0].toLowerCase())
    {
        case "list":
            cdnList();
            break;
   
        case "create":
            cdnCreate();
            break;
   
        case "delete":
            cdnDelete();
            break;
   
        case "purge":
            cdnPurge();
            break;
   
        default:
            console.log("Valid commands are list, delete, create, and purge.");
            process.exit(1);
    }
    ```
6. En varios lugares en nuestro programa, necesitaremos toomake seguro número correcto de Hola de parámetros se pasaron y mostrar ayuda si no tienen un aspecto correctos.  Vamos a crear funciones toodo que.
   
   ```javascript
   function requireParms(parmCount) {
       if(parms.length < parmCount) {
           usageHelp(parms[0].toLowerCase());
           process.exit(1);
       }
   }
   
   function usageHelp(cmd) {
       console.log("Usage for " + cmd + ":");
       switch(cmd)
       {
           case "list":
               console.log("list profiles");
               console.log("list endpoints <profile name>");
               break;
   
           case "create":
               console.log("create profile <profile name>");
               console.log("create endpoint <profile name> <endpoint name> <origin hostname>");
               break;
   
           case "delete":
               console.log("delete profile <profile name>");
               console.log("delete endpoint <profile name> <endpoint name>");
               break;
   
           case "purge":
               console.log("purge <profile name> <endpoint name> <path>");
               break;
   
           default:
               console.log("Invalid command.");
       }
   }
   ```
7. Por último, funciones de hello que usaremos en cliente de administración de red CDN Hola son asincrónicas, por lo que necesitan un método toocall cuando haya terminado.  Vamos a hacer que puede mostrar el resultado de hello de cliente de administración de red CDN Hola (si existe) y salir del programa Hola correctamente.
   
    ```javascript
    function callback(err, result, request, response) {
        if (err) {
            console.log(err);
            process.exit(1);
        } else {
            console.log((result == null) ? "Done!" : result);
            process.exit(0);
        }
    }
    ```

Ahora que se escribe la estructura básica de Hola de nuestro programa, se deben crear funciones de hello llamadas basándose en nuestro parámetros.

## <a name="list-cdn-profiles-and-endpoints"></a>Lista de perfiles y puntos de conexión de CDN
Comencemos con toolist código nuestros perfiles existentes y los puntos de conexión.  Mis comentarios de código proporcionan sintaxis de hello esperada para saber dónde va cada parámetro.

```javascript
// list profiles
// list endpoints <profile name>
function cdnList(){
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profiles":
            console.log("Listing profiles...");
            cdnClient.profiles.listByResourceGroup(resourceGroupName, callback);
            break;

        case "endpoints":
            requireParms(3);
            console.log("Listing endpoints...");
            cdnClient.endpoints.listByProfile(parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a>Creación de perfiles y puntos de conexión de CDN
A continuación, se escribirá los puntos de conexión y perfiles de hello funciones toocreate.

```javascript
function cdnCreate() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profile":
            cdnCreateProfile();
            break;

        case "endpoint":
            cdnCreateEndpoint();
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}

// create profile <profile name>
function cdnCreateProfile() {
    requireParms(3);
    console.log("Creating profile...");
    var standardCreateParameters = {
        location: resourceLocation,
        sku: {
            name: 'Standard_Verizon'
        }
    };

    cdnClient.profiles.create(parms[2], standardCreateParameters, resourceGroupName, callback);
}

// create endpoint <profile name> <endpoint name> <origin hostname>        
function cdnCreateEndpoint() {
    requireParms(5);
    console.log("Creating endpoint...");
    var endpointProperties = {
        location: resourceLocation,
        origins: [{
            name: parms[4],
            hostName: parms[4]
        }]
    };

    cdnClient.endpoints.create(parms[3], endpointProperties, parms[2], resourceGroupName, callback);
}
```

## <a name="purge-an-endpoint"></a>Purga de un punto de conexión
Suponiendo que ha creado el extremo de hello, una tarea habitual que tengamos que queremos tooperform en nuestro programa purga de contenido en el punto de conexión.

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a>Eliminación de perfiles y puntos de conexión de CDN
función last Hola que incluiremos elimina los puntos de conexión y perfiles.

```javascript
function cdnDelete() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        // delete profile <profile name>
        case "profile":
            requireParms(3);
            console.log("Deleting profile...");
            cdnClient.profiles.deleteIfExists(parms[2], resourceGroupName, callback);
            break;

        // delete endpoint <profile name> <endpoint name>
        case "endpoint":
            requireParms(4);
            console.log("Deleting endpoint...");
            cdnClient.endpoints.deleteIfExists(parms[3], parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="running-hello-program"></a>Programa hello en ejecución
Ahora podemos ejecutar nuestro programa Node.js con el depurador de favoritos o en la consola de Hola.

> [!TIP]
> Si está utilizando el código de Visual Studio como el depurador, necesitará tooset seguridad su toopass de entorno en los parámetros de línea de comandos de Hola.  Código de Visual Studio hace esto de hello **lanuch.json** archivo.  Busque una propiedad denominada **args** y agregar una matriz de valores de cadena para los parámetros, por lo que parece similar toothis: `"args": ["list", "profiles"]`.
> 
> 

Vamos a empezar con una lista de nuestros perfiles.

![Listado de perfiles](./media/cdn-app-dev-node/cdn-list-profiles.png)

Recuperamos una matriz vacía.  Esto es normal ya que no tenemos ningún perfil en nuestro grupo de recursos.  Vamos a crear un perfil.

![Creación de perfil](./media/cdn-app-dev-node/cdn-create-profile.png)

Ahora, vamos a agregar un punto de conexión.

![Crear extremo](./media/cdn-app-dev-node/cdn-create-endpoint.png)

Por último, vamos a eliminar el perfil.

![Eliminación de perfil](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a>Pasos siguientes
proyecto de toosee Hola completado de este tutorial, [Descargar ejemplo hello](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).

referencia de hello toosee para hello CDN de Azure SDK para Node.js, Hola vista [referencia](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).

documentación adicional toofind en hello Azure SDK para Node.js, Hola vista [completo referencia](http://azure.github.io/azure-sdk-for-node/).

Administre sus recursos de red CDN con [PowerShell](cdn-manage-powershell.md).

