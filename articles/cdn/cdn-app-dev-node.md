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
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="c2632-103">Introducción al desarrollo de la red de entrega de contenido (CDN) de Azure</span><span class="sxs-lookup"><span data-stu-id="c2632-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c2632-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="c2632-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="c2632-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c2632-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="c2632-106">Puede usar hello [CDN de Azure SDK para Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate creación y administración de perfiles de red CDN y puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="c2632-106">You can use hello [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="c2632-107">Este tutorial le guía por la creación de hello de una aplicación de consola Node.js simple que muestra algunas de las operaciones disponibles de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2632-107">This tutorial walks through hello creation of a simple Node.js console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="c2632-108">Este tutorial es todos los aspectos de SDK de Azure CDN Hola toodescribe no está diseñado para Node.js en detalle.</span><span class="sxs-lookup"><span data-stu-id="c2632-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="c2632-109">toocomplete este tutorial, debe tener ya [Node.js](http://www.nodejs.org) **4.x.x** o superior instalado y configurado.</span><span class="sxs-lookup"><span data-stu-id="c2632-109">toocomplete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="c2632-110">Puede usar cualquier editor de texto que desea toocreate la aplicación de Node.js.</span><span class="sxs-lookup"><span data-stu-id="c2632-110">You can use any text editor you want toocreate your Node.js application.</span></span>  <span data-ttu-id="c2632-111">toowrite este tutorial, he usado [código de Visual Studio](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="c2632-111">toowrite this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="c2632-112">Hola [proyecto completado de este tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) está disponible para su descarga en MSDN.</span><span class="sxs-lookup"><span data-stu-id="c2632-112">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="c2632-113">Creación del proyecto e incorporación de dependencias NPM</span><span class="sxs-lookup"><span data-stu-id="c2632-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="c2632-114">Ahora que hemos creado un grupo de recursos para los perfiles de la red CDN y dada nuestra perfiles de red CDN de Azure AD aplicación permiso toomanage y los puntos de conexión dentro de ese grupo, podemos comenzar a crear nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="c2632-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="c2632-115">Crear una carpeta toostore su aplicación.</span><span class="sxs-lookup"><span data-stu-id="c2632-115">Create a folder toostore your application.</span></span>  <span data-ttu-id="c2632-116">Desde una consola con herramientas de Node.js de hello en la ruta de acceso actual, establecer la ubicación toothis nueva carpeta actual e inicializar el proyecto mediante la ejecución:</span><span class="sxs-lookup"><span data-stu-id="c2632-116">From a console with hello Node.js tools in your current path, set your current location toothis new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="c2632-117">A continuación, podrá presentan una serie de preguntas tooinitialize el proyecto.</span><span class="sxs-lookup"><span data-stu-id="c2632-117">You will then be presented a series of questions tooinitialize your project.</span></span>  <span data-ttu-id="c2632-118">Para **punto de entrada**, este tutorial usa *app.js*.</span><span class="sxs-lookup"><span data-stu-id="c2632-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="c2632-119">Puede ver mi otras opciones en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2632-119">You can see my other choices in hello following example.</span></span>

![Salida de NPM init](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="c2632-121">El proyecto se inicializa ahora con un archivo *packages.json* .</span><span class="sxs-lookup"><span data-stu-id="c2632-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="c2632-122">Nuestro proyecto va toouse algunas bibliotecas de Azure contenidos en paquetes de NPM.</span><span class="sxs-lookup"><span data-stu-id="c2632-122">Our project is going toouse some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="c2632-123">Vamos a usar en tiempo de ejecución del cliente de Azure para Node.js (ms-rest-azure) de Hola y Hola biblioteca de cliente de red CDN de Azure para Node.js (cd de arm de azure).</span><span class="sxs-lookup"><span data-stu-id="c2632-123">We'll use hello Azure Client Runtime for Node.js (ms-rest-azure) and hello Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="c2632-124">Vamos a agregar esos proyectos toohello como dependencias.</span><span class="sxs-lookup"><span data-stu-id="c2632-124">Let's add those toohello project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="c2632-125">Después de hello terminados paquetes de instalación, hello *package.json* archivo debería ser similar toothis ejemplo (versión pueden variar):</span><span class="sxs-lookup"><span data-stu-id="c2632-125">After hello packages are done installing, hello *package.json* file should look similar toothis example (version numbers may differ):</span></span>

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

<span data-ttu-id="c2632-126">Por último, con su editor de texto, cree un archivo de texto en blanco y guárdela en la raíz de saludo de la carpeta del proyecto como *app.js*.</span><span class="sxs-lookup"><span data-stu-id="c2632-126">Finally, using your text editor, create a blank text file and save it in hello root of our project folder as *app.js*.</span></span>  <span data-ttu-id="c2632-127">Ahora estamos listo toobegin escribir código.</span><span class="sxs-lookup"><span data-stu-id="c2632-127">We're now ready toobegin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="c2632-128">"Requieres", constantes, autenticación y estructura</span><span class="sxs-lookup"><span data-stu-id="c2632-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="c2632-129">Con *app.js* abierto en el editor, vamos a estructura básica de Hola de nuestro programa escrito.</span><span class="sxs-lookup"><span data-stu-id="c2632-129">With *app.js* open in our editor, let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="c2632-130">Agregue Hola "requiere" para los paquetes de NPM princip Hola con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="c2632-130">Add hello "requires" for our NPM packages at hello top with hello following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="c2632-131">Necesitamos toodefine algunas constantes que nuestros métodos va a usar.</span><span class="sxs-lookup"><span data-stu-id="c2632-131">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="c2632-132">Agregue Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="c2632-132">Add hello following.</span></span>  <span data-ttu-id="c2632-133">Ser seguro tooreplace marcadores de posición de hello, incluidos hello  **&lt;corchetes angulares&gt;**, con sus propios valores según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c2632-133">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="c2632-134">A continuación, se deberá crear una instancia de cliente de administración de red CDN Hola y asígnele nuestras credenciales.</span><span class="sxs-lookup"><span data-stu-id="c2632-134">Next, we'll instantiate hello CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="c2632-135">Si utiliza la autenticación de usuario individual, estas dos líneas tendrán un aspecto algo distinto.</span><span class="sxs-lookup"><span data-stu-id="c2632-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="c2632-136">Sólo puede utilizar este ejemplo de código si se elige el toohave autenticación de usuario individuales en lugar de una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="c2632-136">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="c2632-137">Ser tooguard cuidado las credenciales de usuario individual y mantener en secreto.</span><span class="sxs-lookup"><span data-stu-id="c2632-137">Be careful tooguard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="c2632-138">Estar seguro tooreplace compuesta por elementos hello en  **&lt;corchetes angulares&gt;**  con hello corregir la información.</span><span class="sxs-lookup"><span data-stu-id="c2632-138">Be sure tooreplace hello items in **&lt;angle brackets&gt;** with hello correct information.</span></span>  <span data-ttu-id="c2632-139">Para `<redirect URI>`, usar redirección Hola URI que especificó al registrar la aplicación hello en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2632-139">For `<redirect URI>`, use hello redirect URI you entered when you registered hello application in Azure AD.</span></span>
4. <span data-ttu-id="c2632-140">Nuestra aplicación de consola Node.js va tootake algunos parámetros de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="c2632-140">Our Node.js console application is going tootake some command-line parameters.</span></span>  <span data-ttu-id="c2632-141">Vamos a dar por válido que por lo menos un parámetro se pasó.</span><span class="sxs-lookup"><span data-stu-id="c2632-141">Let's validate that at least one parameter was passed.</span></span>
   
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
5. <span data-ttu-id="c2632-142">Eso nos lleva toohello parte principal de nuestro programa, donde se separarlos tooother funciones que se basan en los parámetros que se pasaron.</span><span class="sxs-lookup"><span data-stu-id="c2632-142">That brings us toohello main part of our program, where we branch off tooother functions based on what parameters were passed.</span></span>
   
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
6. <span data-ttu-id="c2632-143">En varios lugares en nuestro programa, necesitaremos toomake seguro número correcto de Hola de parámetros se pasaron y mostrar ayuda si no tienen un aspecto correctos.</span><span class="sxs-lookup"><span data-stu-id="c2632-143">At several places in our program, we'll need toomake sure hello right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="c2632-144">Vamos a crear funciones toodo que.</span><span class="sxs-lookup"><span data-stu-id="c2632-144">Let's create functions toodo that.</span></span>
   
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
7. <span data-ttu-id="c2632-145">Por último, funciones de hello que usaremos en cliente de administración de red CDN Hola son asincrónicas, por lo que necesitan un método toocall cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="c2632-145">Finally, hello functions we'll be using on hello CDN management client are asynchronous, so they need a method toocall back when they're done.</span></span>  <span data-ttu-id="c2632-146">Vamos a hacer que puede mostrar el resultado de hello de cliente de administración de red CDN Hola (si existe) y salir del programa Hola correctamente.</span><span class="sxs-lookup"><span data-stu-id="c2632-146">Let's make one that can display hello output from hello CDN management client (if any) and exit hello program gracefully.</span></span>
   
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

<span data-ttu-id="c2632-147">Ahora que se escribe la estructura básica de Hola de nuestro programa, se deben crear funciones de hello llamadas basándose en nuestro parámetros.</span><span class="sxs-lookup"><span data-stu-id="c2632-147">Now that hello basic structure of our program is written, we should create hello functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="c2632-148">Lista de perfiles y puntos de conexión de CDN</span><span class="sxs-lookup"><span data-stu-id="c2632-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="c2632-149">Comencemos con toolist código nuestros perfiles existentes y los puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="c2632-149">Let's start with code toolist our existing profiles and endpoints.</span></span>  <span data-ttu-id="c2632-150">Mis comentarios de código proporcionan sintaxis de hello esperada para saber dónde va cada parámetro.</span><span class="sxs-lookup"><span data-stu-id="c2632-150">My code comments provide hello expected syntax so we know where each parameter goes.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="c2632-151">Creación de perfiles y puntos de conexión de CDN</span><span class="sxs-lookup"><span data-stu-id="c2632-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="c2632-152">A continuación, se escribirá los puntos de conexión y perfiles de hello funciones toocreate.</span><span class="sxs-lookup"><span data-stu-id="c2632-152">Next, we'll write hello functions toocreate profiles and endpoints.</span></span>

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

## <a name="purge-an-endpoint"></a><span data-ttu-id="c2632-153">Purga de un punto de conexión</span><span class="sxs-lookup"><span data-stu-id="c2632-153">Purge an endpoint</span></span>
<span data-ttu-id="c2632-154">Suponiendo que ha creado el extremo de hello, una tarea habitual que tengamos que queremos tooperform en nuestro programa purga de contenido en el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="c2632-154">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="c2632-155">Eliminación de perfiles y puntos de conexión de CDN</span><span class="sxs-lookup"><span data-stu-id="c2632-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="c2632-156">función last Hola que incluiremos elimina los puntos de conexión y perfiles.</span><span class="sxs-lookup"><span data-stu-id="c2632-156">hello last function we will include deletes endpoints and profiles.</span></span>

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

## <a name="running-hello-program"></a><span data-ttu-id="c2632-157">Programa hello en ejecución</span><span class="sxs-lookup"><span data-stu-id="c2632-157">Running hello program</span></span>
<span data-ttu-id="c2632-158">Ahora podemos ejecutar nuestro programa Node.js con el depurador de favoritos o en la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2632-158">We can now execute our Node.js program using our favorite debugger or at hello console.</span></span>

> [!TIP]
> <span data-ttu-id="c2632-159">Si está utilizando el código de Visual Studio como el depurador, necesitará tooset seguridad su toopass de entorno en los parámetros de línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2632-159">If you're using Visual Studio Code as your debugger, you'll need tooset up your environment toopass in hello command-line parameters.</span></span>  <span data-ttu-id="c2632-160">Código de Visual Studio hace esto de hello **lanuch.json** archivo.</span><span class="sxs-lookup"><span data-stu-id="c2632-160">Visual Studio Code does this in hello **lanuch.json** file.</span></span>  <span data-ttu-id="c2632-161">Busque una propiedad denominada **args** y agregar una matriz de valores de cadena para los parámetros, por lo que parece similar toothis: `"args": ["list", "profiles"]`.</span><span class="sxs-lookup"><span data-stu-id="c2632-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar toothis:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="c2632-162">Vamos a empezar con una lista de nuestros perfiles.</span><span class="sxs-lookup"><span data-stu-id="c2632-162">Let's start by listing our profiles.</span></span>

![Listado de perfiles](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="c2632-164">Recuperamos una matriz vacía.</span><span class="sxs-lookup"><span data-stu-id="c2632-164">We got back an empty array.</span></span>  <span data-ttu-id="c2632-165">Esto es normal ya que no tenemos ningún perfil en nuestro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c2632-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="c2632-166">Vamos a crear un perfil.</span><span class="sxs-lookup"><span data-stu-id="c2632-166">Let's create a profile now.</span></span>

![Creación de perfil](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="c2632-168">Ahora, vamos a agregar un punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="c2632-168">Now, let's add an endpoint.</span></span>

![Crear extremo](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="c2632-170">Por último, vamos a eliminar el perfil.</span><span class="sxs-lookup"><span data-stu-id="c2632-170">Finally, let's delete our profile.</span></span>

![Eliminación de perfil](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="c2632-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c2632-172">Next Steps</span></span>
<span data-ttu-id="c2632-173">proyecto de toosee Hola completado de este tutorial, [Descargar ejemplo hello](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span><span class="sxs-lookup"><span data-stu-id="c2632-173">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="c2632-174">referencia de hello toosee para hello CDN de Azure SDK para Node.js, Hola vista [referencia](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span><span class="sxs-lookup"><span data-stu-id="c2632-174">toosee hello reference for hello Azure CDN SDK for Node.js, view hello [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="c2632-175">documentación adicional toofind en hello Azure SDK para Node.js, Hola vista [completo referencia](http://azure.github.io/azure-sdk-for-node/).</span><span class="sxs-lookup"><span data-stu-id="c2632-175">toofind additional documentation on hello Azure SDK for Node.js, view hello [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="c2632-176">Administre sus recursos de red CDN con [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c2632-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

