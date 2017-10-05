---
title: "Introducción al SDK de red CDN de Azure para Node.js | Microsoft Docs"
description: Aprenda a escribir aplicaciones Node.js para administrar la red CDN de Azure.
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
ms.openlocfilehash: 46ae8cd9775432d126cbde856c1fb06ea319297e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="e3db0-103">Introducción al desarrollo de la red de entrega de contenido (CDN) de Azure</span><span class="sxs-lookup"><span data-stu-id="e3db0-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3db0-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="e3db0-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="e3db0-105">.NET</span><span class="sxs-lookup"><span data-stu-id="e3db0-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="e3db0-106">Puede usar el [SDK de red CDN de Azure para Node.js](https://www.npmjs.com/package/azure-arm-cdn) para automatizar la creación y la administración de puntos de conexión y perfiles de red CDN.</span><span class="sxs-lookup"><span data-stu-id="e3db0-106">You can use the [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="e3db0-107">Este tutorial explica paso a paso la creación de una aplicación de consola Node.js sencilla que muestra algunas de las operaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="e3db0-107">This tutorial walks through the creation of a simple Node.js console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="e3db0-108">No se pretende describir todos los aspectos del SDK de red CDN de Azure para Node.js en detalle.</span><span class="sxs-lookup"><span data-stu-id="e3db0-108">This tutorial is not intended to describe all aspects of the Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="e3db0-109">Para completar este tutorial, debe tener ya instalado y configurado [Node.js](http://www.nodejs.org) **4.x.x** o superior.</span><span class="sxs-lookup"><span data-stu-id="e3db0-109">To complete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="e3db0-110">Puede usar cualquier editor de texto que desee para crear la aplicación de Node.js.</span><span class="sxs-lookup"><span data-stu-id="e3db0-110">You can use any text editor you want to create your Node.js application.</span></span>  <span data-ttu-id="e3db0-111">Para escribir este tutorial, se ha usado [Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="e3db0-111">To write this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="e3db0-112">El [proyecto completado en este tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) está disponible para descargarse en MSDN.</span><span class="sxs-lookup"><span data-stu-id="e3db0-112">The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="e3db0-113">Creación del proyecto e incorporación de dependencias NPM</span><span class="sxs-lookup"><span data-stu-id="e3db0-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="e3db0-114">Ahora que hemos creado un grupo de recursos para los perfiles de CDN y concedido permiso a la aplicación de Azure AD para administrar perfiles y puntos de conexión de CDN dentro de ese grupo, podemos comenzar a crear la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e3db0-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="e3db0-115">Cree una carpeta para almacenar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e3db0-115">Create a folder to store your application.</span></span>  <span data-ttu-id="e3db0-116">Desde una consola con las herramientas de Node.js en su ruta de acceso actual, establezca su ubicación actual en esta nueva carpeta e inicialice el proyecto ejecutando:</span><span class="sxs-lookup"><span data-stu-id="e3db0-116">From a console with the Node.js tools in your current path, set your current location to this new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="e3db0-117">A continuación, se le ofrecerán una serie de preguntas para inicializar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="e3db0-117">You will then be presented a series of questions to initialize your project.</span></span>  <span data-ttu-id="e3db0-118">Para **punto de entrada**, este tutorial usa *app.js*.</span><span class="sxs-lookup"><span data-stu-id="e3db0-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="e3db0-119">Puede ver las demás opciones en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="e3db0-119">You can see my other choices in the following example.</span></span>

![Salida de NPM init](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="e3db0-121">El proyecto se inicializa ahora con un archivo *packages.json* .</span><span class="sxs-lookup"><span data-stu-id="e3db0-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="e3db0-122">Va a usar algunas bibliotecas de Azure contenidas en paquetes NPM.</span><span class="sxs-lookup"><span data-stu-id="e3db0-122">Our project is going to use some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="e3db0-123">Vamos a usar el tiempo de ejecución de cliente de Azure para Node.js (ms-rest-azure) y la biblioteca de cliente de red CDN de Azure para Node.js (azure-arm-cd).</span><span class="sxs-lookup"><span data-stu-id="e3db0-123">We'll use the Azure Client Runtime for Node.js (ms-rest-azure) and the Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="e3db0-124">Vamos a agregar estos elementos al proyecto como dependencias.</span><span class="sxs-lookup"><span data-stu-id="e3db0-124">Let's add those to the project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="e3db0-125">Una vez que los paquetes se han instalado, el archivo *package.json* debe ser similar a este ejemplo (los números de versión pueden variar):</span><span class="sxs-lookup"><span data-stu-id="e3db0-125">After the packages are done installing, the *package.json* file should look similar to this example (version numbers may differ):</span></span>

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

<span data-ttu-id="e3db0-126">Por último, con el editor de texto, cree un archivo de texto en blanco y guárdelo en la raíz de la carpeta del proyecto como *app.js*.</span><span class="sxs-lookup"><span data-stu-id="e3db0-126">Finally, using your text editor, create a blank text file and save it in the root of our project folder as *app.js*.</span></span>  <span data-ttu-id="e3db0-127">Ya está todo preparado para empezar a escribir código.</span><span class="sxs-lookup"><span data-stu-id="e3db0-127">We're now ready to begin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="e3db0-128">"Requieres", constantes, autenticación y estructura</span><span class="sxs-lookup"><span data-stu-id="e3db0-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="e3db0-129">Con *apps.js* abierto en el editor, vamos a escribir la estructura básica del programa.</span><span class="sxs-lookup"><span data-stu-id="e3db0-129">With *app.js* open in our editor, let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="e3db0-130">En la parte superior agregue los "requiere" para los paquetes NPM con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e3db0-130">Add the "requires" for our NPM packages at the top with the following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="e3db0-131">Necesitamos definir algunas constantes que los métodos van a usar.</span><span class="sxs-lookup"><span data-stu-id="e3db0-131">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="e3db0-132">Agregue lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="e3db0-132">Add the following.</span></span>  <span data-ttu-id="e3db0-133">Asegúrese de reemplazar los marcadores de posición (incluidos los **&lt;corchetes angulares&gt;**) con sus propios valores según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e3db0-133">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="e3db0-134">A continuación, crearemos una instancia del cliente de administración de la red CDN y le asignaremos nuestras credenciales.</span><span class="sxs-lookup"><span data-stu-id="e3db0-134">Next, we'll instantiate the CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="e3db0-135">Si utiliza la autenticación de usuario individual, estas dos líneas tendrán un aspecto algo distinto.</span><span class="sxs-lookup"><span data-stu-id="e3db0-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="e3db0-136">Use este ejemplo de código únicamente si opta por la autenticación de usuario individual en lugar de una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="e3db0-136">Only use this code sample if you are choosing to have individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="e3db0-137">Asegúrese de guardar las credenciales de usuario individual y de mantenerlas en secreto.</span><span class="sxs-lookup"><span data-stu-id="e3db0-137">Be careful to guard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="e3db0-138">No olvide reemplazar los elementos en **&lt;corchetes angulares&gt;** por la información correcta.</span><span class="sxs-lookup"><span data-stu-id="e3db0-138">Be sure to replace the items in **&lt;angle brackets&gt;** with the correct information.</span></span>  <span data-ttu-id="e3db0-139">Para `<redirect URI>`, use el URI de redirección que especificó al registrar la aplicación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3db0-139">For `<redirect URI>`, use the redirect URI you entered when you registered the application in Azure AD.</span></span>
4. <span data-ttu-id="e3db0-140">Nuestra aplicación de consola Node.js necesita algunos parámetros de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="e3db0-140">Our Node.js console application is going to take some command-line parameters.</span></span>  <span data-ttu-id="e3db0-141">Vamos a dar por válido que por lo menos un parámetro se pasó.</span><span class="sxs-lookup"><span data-stu-id="e3db0-141">Let's validate that at least one parameter was passed.</span></span>
   
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
5. <span data-ttu-id="e3db0-142">Con esto llegamos a la parte principal del programa, donde vamos a derivar a otras funciones basadas en los parámetros que se pasaron.</span><span class="sxs-lookup"><span data-stu-id="e3db0-142">That brings us to the main part of our program, where we branch off to other functions based on what parameters were passed.</span></span>
   
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
6. <span data-ttu-id="e3db0-143">En varios lugares del programa, es necesario asegurarse de que se ha pasado la cantidad correcta de parámetros, si parece que esto no es así, hay que mostrar ayudas.</span><span class="sxs-lookup"><span data-stu-id="e3db0-143">At several places in our program, we'll need to make sure the right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="e3db0-144">Vamos a crear funciones para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="e3db0-144">Let's create functions to do that.</span></span>
   
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
7. <span data-ttu-id="e3db0-145">Por último, las funciones que vamos a usar en el cliente de administración de la red CDN son asincrónicas, por lo que necesitan un método al que llamar cuando hayan terminado.</span><span class="sxs-lookup"><span data-stu-id="e3db0-145">Finally, the functions we'll be using on the CDN management client are asynchronous, so they need a method to call back when they're done.</span></span>  <span data-ttu-id="e3db0-146">Vamos a hacer uno que pueda mostrar el resultado desde el cliente de administración de la red CDN (si lo hubiera) y salir del programa sin contratiempos.</span><span class="sxs-lookup"><span data-stu-id="e3db0-146">Let's make one that can display the output from the CDN management client (if any) and exit the program gracefully.</span></span>
   
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

<span data-ttu-id="e3db0-147">Ahora que ya hemos escrito la estructura básica del programa, deberíamos crear las funciones a las que se llama en base a los parámetros.</span><span class="sxs-lookup"><span data-stu-id="e3db0-147">Now that the basic structure of our program is written, we should create the functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="e3db0-148">Lista de perfiles y puntos de conexión de CDN</span><span class="sxs-lookup"><span data-stu-id="e3db0-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="e3db0-149">Comencemos con código para enumera los perfiles y puntos de conexión existentes.</span><span class="sxs-lookup"><span data-stu-id="e3db0-149">Let's start with code to list our existing profiles and endpoints.</span></span>  <span data-ttu-id="e3db0-150">Los comentarios de código proporcionan la sintaxis esperada para saber dónde va cada parámetro.</span><span class="sxs-lookup"><span data-stu-id="e3db0-150">My code comments provide the expected syntax so we know where each parameter goes.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="e3db0-151">Creación de perfiles y puntos de conexión de CDN</span><span class="sxs-lookup"><span data-stu-id="e3db0-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="e3db0-152">A continuación, escribiremos las funciones para crear perfiles y puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="e3db0-152">Next, we'll write the functions to create profiles and endpoints.</span></span>

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

## <a name="purge-an-endpoint"></a><span data-ttu-id="e3db0-153">Purga de un punto de conexión</span><span class="sxs-lookup"><span data-stu-id="e3db0-153">Purge an endpoint</span></span>
<span data-ttu-id="e3db0-154">Suponiendo que se haya creado el punto de conexión, una tarea habitual que podríamos llevar a cabo en el programa es purgar el contenido del punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="e3db0-154">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="e3db0-155">Eliminación de perfiles y puntos de conexión de CDN</span><span class="sxs-lookup"><span data-stu-id="e3db0-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="e3db0-156">La última función que incluiremos elimina puntos de conexión y perfiles.</span><span class="sxs-lookup"><span data-stu-id="e3db0-156">The last function we will include deletes endpoints and profiles.</span></span>

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

## <a name="running-the-program"></a><span data-ttu-id="e3db0-157">Ejecución del programa</span><span class="sxs-lookup"><span data-stu-id="e3db0-157">Running the program</span></span>
<span data-ttu-id="e3db0-158">Ahora ya podemos ejecutar nuestro programa de Node.js usando nuestro depurador preferido o en la consola.</span><span class="sxs-lookup"><span data-stu-id="e3db0-158">We can now execute our Node.js program using our favorite debugger or at the console.</span></span>

> [!TIP]
> <span data-ttu-id="e3db0-159">Si usa código de Visual Studio como depurador, tiene que configurar su entorno para pasar los parámetros de línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="e3db0-159">If you're using Visual Studio Code as your debugger, you'll need to set up your environment to pass in the command-line parameters.</span></span>  <span data-ttu-id="e3db0-160">El código de Visual Studio realiza esta operación en el archivo **lanuch.json** .</span><span class="sxs-lookup"><span data-stu-id="e3db0-160">Visual Studio Code does this in the **lanuch.json** file.</span></span>  <span data-ttu-id="e3db0-161">Busque una propiedad denominada **args** y agregue una matriz de valores de cadena para los parámetros, de forma que se parezca a esto: `"args": ["list", "profiles"]`.</span><span class="sxs-lookup"><span data-stu-id="e3db0-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar to this:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="e3db0-162">Vamos a empezar con una lista de nuestros perfiles.</span><span class="sxs-lookup"><span data-stu-id="e3db0-162">Let's start by listing our profiles.</span></span>

![Listado de perfiles](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="e3db0-164">Recuperamos una matriz vacía.</span><span class="sxs-lookup"><span data-stu-id="e3db0-164">We got back an empty array.</span></span>  <span data-ttu-id="e3db0-165">Esto es normal ya que no tenemos ningún perfil en nuestro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e3db0-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="e3db0-166">Vamos a crear un perfil.</span><span class="sxs-lookup"><span data-stu-id="e3db0-166">Let's create a profile now.</span></span>

![Creación de perfil](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="e3db0-168">Ahora, vamos a agregar un punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="e3db0-168">Now, let's add an endpoint.</span></span>

![Crear extremo](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="e3db0-170">Por último, vamos a eliminar el perfil.</span><span class="sxs-lookup"><span data-stu-id="e3db0-170">Finally, let's delete our profile.</span></span>

![Eliminación de perfil](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="e3db0-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e3db0-172">Next Steps</span></span>
<span data-ttu-id="e3db0-173">Para ver el proyecto de este tutorial terminado, [descargue el ejemplo](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span><span class="sxs-lookup"><span data-stu-id="e3db0-173">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="e3db0-174">Para ver la referencia del SDK de red CDN de Azure para Node.js, consulte el documento de [referencia](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span><span class="sxs-lookup"><span data-stu-id="e3db0-174">To see the reference for the Azure CDN SDK for Node.js, view the [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="e3db0-175">Para encontrar más documentación sobre Azure SDK para Node.js, consulte el [material de referencia completo](http://azure.github.io/azure-sdk-for-node/).</span><span class="sxs-lookup"><span data-stu-id="e3db0-175">To find additional documentation on the Azure SDK for Node.js, view the [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="e3db0-176">Administre sus recursos de red CDN con [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e3db0-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

