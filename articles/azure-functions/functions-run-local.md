---
title: "aaaDevelop y ejecución de Azure funciona localmente | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocode y prueba de Azure funciona en el equipo local antes de ejecutar en las funciones de Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
ms.assetid: 242736be-ec66-4114-924b-31795fd18884
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 07/12/2017
ms.author: glenga
ms.openlocfilehash: 342ed4d6df41a2d2df9067948e19e347bb52c844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="82b88-103">Codificación y comprobación de las funciones de Azure en un entorno local</span><span class="sxs-lookup"><span data-stu-id="82b88-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="82b88-104">Mientras hello [portal de Azure] proporciona un completo conjunto de herramientas para el desarrollo y prueba de las funciones de Azure, muchos desarrolladores prefieren una experiencia de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="82b88-104">While hello [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="82b88-105">Las funciones de Azure hace fácil toouse favoritos toodevelop de herramientas de desarrollo local de editor de código y probar las funciones en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="82b88-105">Azure Functions makes it easy toouse your favorite code editor and local development tools toodevelop and test your functions on your local computer.</span></span> <span data-ttu-id="82b88-106">Las funciones pueden desencadenarse a partir de eventos de Azure, y puede depurar sus funciones en C# y JavaScript en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="82b88-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="82b88-107">Si es un desarrollador de C# de Visual Studio, Azure Functions también [permite la integración con Visual Studio 2017](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="82b88-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-hello-azure-functions-core-tools"></a><span data-ttu-id="82b88-108">Instalar las herramientas de hello Azure funciones principales</span><span class="sxs-lookup"><span data-stu-id="82b88-108">Install hello Azure Functions Core Tools</span></span>

<span data-ttu-id="82b88-109">Herramientas de Azure funciones principales es una versión local de en tiempo de ejecución de funciones de Azure de Hola que se pueden ejecutar en el equipo local de Windows.</span><span class="sxs-lookup"><span data-stu-id="82b88-109">Azure Functions Core Tools is a local version of hello Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="82b88-110">No se trata de un emulador o simulador.</span><span class="sxs-lookup"><span data-stu-id="82b88-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="82b88-111">Ha Hola mismo en tiempo de ejecución que proporciona funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="82b88-111">It's hello same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="82b88-112">Hola [herramientas básicas de las funciones de Azure] se proporciona como un paquete de npm.</span><span class="sxs-lookup"><span data-stu-id="82b88-112">hello [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="82b88-113">Primero debe [instalar NodeJS](https://docs.npmjs.com/getting-started/installing-node), que incluye npm.</span><span class="sxs-lookup"><span data-stu-id="82b88-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="82b88-114">En este momento, el paquete de herramientas de Azure funciones principales de hello solo puede instalarse en equipos con Windows.</span><span class="sxs-lookup"><span data-stu-id="82b88-114">At this time, hello Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="82b88-115">Esta restricción es debido a limitación temporal de tooa en host de las funciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="82b88-115">This restriction is due tooa temporary limitation in hello Functions host.</span></span>

<span data-ttu-id="82b88-116">[herramientas básicas de las funciones de Azure] agrega Hola siguiendo los alias de comandos:</span><span class="sxs-lookup"><span data-stu-id="82b88-116">[Azure Functions Core Tools] adds hello following command aliases:</span></span>
* <span data-ttu-id="82b88-117">**func**</span><span class="sxs-lookup"><span data-stu-id="82b88-117">**func**</span></span>
* <span data-ttu-id="82b88-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="82b88-118">**azfun**</span></span>
* <span data-ttu-id="82b88-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="82b88-119">**azurefunctions**</span></span>

<span data-ttu-id="82b88-120">Todos estos alias pueden utilizarse en lugar de `func` se muestra en los ejemplos de hello en este tema.</span><span class="sxs-lookup"><span data-stu-id="82b88-120">All of these alias can be used instead of `func` shown in hello examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="82b88-121">Creación de un proyecto local de Functions</span><span class="sxs-lookup"><span data-stu-id="82b88-121">Create a local Functions project</span></span>

<span data-ttu-id="82b88-122">Cuando se ejecuta localmente, un proyecto de funciones es un directorio que tiene local.settings.json y Hola archivos host.json.</span><span class="sxs-lookup"><span data-stu-id="82b88-122">When running locally, a Functions project is a directory that has hello files host.json and local.settings.json.</span></span> <span data-ttu-id="82b88-123">Este directorio es Hola equivalente de una aplicación de la función en Azure.</span><span class="sxs-lookup"><span data-stu-id="82b88-123">This directory is hello equivalent of a function app in Azure.</span></span> <span data-ttu-id="82b88-124">toolearn más información acerca de hello estructura de carpetas de las funciones de Azure, vea hello [Guía de desarrolladores de Azure funciones](functions-reference.md#folder-structure).</span><span class="sxs-lookup"><span data-stu-id="82b88-124">toolearn more about hello Azure Functions folder structure, see hello [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="82b88-125">En un símbolo del sistema, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="82b88-125">At a command prompt, run hello following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="82b88-126">salida de Hello es similar a Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="82b88-126">hello output looks like hello following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="82b88-127">tooopt fuera de la creación de un repositorio Git, el uso de la opción hello `--no-source-control [-n]`.</span><span class="sxs-lookup"><span data-stu-id="82b88-127">tooopt out of creating a Git repository, use hello option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="82b88-128">Archivo de configuración local</span><span class="sxs-lookup"><span data-stu-id="82b88-128">Local settings file</span></span>

<span data-ttu-id="82b88-129">Hola archivo local.settings.json almacena la configuración de la aplicación, las cadenas de conexión y configuración de herramientas básicas de las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="82b88-129">hello file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="82b88-130">Tiene Hola siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="82b88-130">It has hello following structure:</span></span>

```json
{
  "IsEncrypted": false,   
  "Values": {
    "AzureWebJobsStorage": "<connection string>", 
    "AzureWebJobsDashboard": "<connection string>", 
  },
  "Host": {
    "LocalHttpPort": 7071, 
    "CORS": "*" 
  },
  "ConnectionStrings": {
    "SQLConnectionString": "Value"
  }
}
```
| <span data-ttu-id="82b88-131">Configuración</span><span class="sxs-lookup"><span data-stu-id="82b88-131">Setting</span></span>      | <span data-ttu-id="82b88-132">Descripción</span><span class="sxs-lookup"><span data-stu-id="82b88-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="82b88-133">**IsEncrypted**</span><span class="sxs-lookup"><span data-stu-id="82b88-133">**IsEncrypted**</span></span> | <span data-ttu-id="82b88-134">Cuando se establece demasiado**true**, todos los valores se cifran mediante una clave del equipo local.</span><span class="sxs-lookup"><span data-stu-id="82b88-134">When set too**true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="82b88-135">Se usa con los comandos `func settings`.</span><span class="sxs-lookup"><span data-stu-id="82b88-135">Used with `func settings` commands.</span></span> <span data-ttu-id="82b88-136">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="82b88-136">Default value is **false**.</span></span> |
| <span data-ttu-id="82b88-137">**Valores**</span><span class="sxs-lookup"><span data-stu-id="82b88-137">**Values**</span></span> | <span data-ttu-id="82b88-138">Colección de opciones de configuración de la aplicación que se usa en la ejecución local.</span><span class="sxs-lookup"><span data-stu-id="82b88-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="82b88-139">Agregue su objeto de toothis de configuración de aplicación.</span><span class="sxs-lookup"><span data-stu-id="82b88-139">Add your application settings toothis object.</span></span>  |
| <span data-ttu-id="82b88-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="82b88-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="82b88-141">Conjuntos de Hola toohello de cadena de conexión cuenta de almacenamiento de Azure que se usa internamente en tiempo de ejecución de funciones de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="82b88-141">Sets hello connection string toohello Azure Storage account that is used internally by hello Azure Functions runtime.</span></span> <span data-ttu-id="82b88-142">cuenta de almacenamiento de Hello es compatible con los desencadenadores de la función.</span><span class="sxs-lookup"><span data-stu-id="82b88-142">hello storage account supports your function's triggers.</span></span> <span data-ttu-id="82b88-143">Esta configuración de conexión de la cuenta de almacenamiento es necesaria para todas las funciones, salvo en el caso de las funciones desencadenadas de HTTP.</span><span class="sxs-lookup"><span data-stu-id="82b88-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="82b88-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="82b88-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="82b88-145">Establece Hola cadena toohello almacenamiento de Azure cuenta de conexión que es usado toostore Hola función registros.</span><span class="sxs-lookup"><span data-stu-id="82b88-145">Sets hello connection string toohello Azure Storage account that is used toostore hello function logs.</span></span> <span data-ttu-id="82b88-146">Este valor opcional hace Hola registros esté accesible en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="82b88-146">This optional value makes hello logs accessible in hello portal.</span></span>|
| <span data-ttu-id="82b88-147">**Host**</span><span class="sxs-lookup"><span data-stu-id="82b88-147">**Host**</span></span> | <span data-ttu-id="82b88-148">Configuración de esta sección Personalizar el proceso de host de las funciones hello cuando se ejecuta localmente.</span><span class="sxs-lookup"><span data-stu-id="82b88-148">Settings in this section customize hello Functions host process when running locally.</span></span> | 
| <span data-ttu-id="82b88-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="82b88-149">**LocalHttpPort**</span></span> | <span data-ttu-id="82b88-150">Conjuntos de Hola puerto predeterminado utilizado cuando se ejecuta el host local de las funciones de hello (`func host start` y `func run`).</span><span class="sxs-lookup"><span data-stu-id="82b88-150">Sets hello default port used when running hello local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="82b88-151">Hola `--port` opción de línea de comandos tiene prioridad sobre este valor.</span><span class="sxs-lookup"><span data-stu-id="82b88-151">hello `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="82b88-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="82b88-152">**CORS**</span></span> | <span data-ttu-id="82b88-153">Define los orígenes de hello permitidos para [recursos entre orígenes (CORS) de uso compartido](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span><span class="sxs-lookup"><span data-stu-id="82b88-153">Defines hello origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="82b88-154">Los orígenes se proporcionan en una lista de valores separados por comas y sin espacios.</span><span class="sxs-lookup"><span data-stu-id="82b88-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="82b88-155">Hola valor de carácter comodín (**\***) es compatible, que permite que las solicitudes desde cualquier origen.</span><span class="sxs-lookup"><span data-stu-id="82b88-155">hello wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="82b88-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="82b88-156">**ConnectionStrings**</span></span> | <span data-ttu-id="82b88-157">Contiene las cadenas de conexión de base de datos de Hola para sus funciones.</span><span class="sxs-lookup"><span data-stu-id="82b88-157">Contains hello database connection strings for your functions.</span></span> <span data-ttu-id="82b88-158">Cadenas de conexión en este objeto se agregan toohello entorno con el tipo de proveedor de Hola de **System.Data.SqlClient**.</span><span class="sxs-lookup"><span data-stu-id="82b88-158">Connection strings in this object are added toohello environment with hello provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="82b88-159">La mayoría de los desencadenadores y los enlaces tienen un **conexión** propiedad que se asigna el nombre de toohello de una configuración de aplicación o la variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="82b88-159">Most triggers and bindings have a **Connection** property that maps toohello name of an environment variable or app setting.</span></span> <span data-ttu-id="82b88-160">Por cada propiedad de conexión debe haber una configuración de aplicación definida en el archivo local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="82b88-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="82b88-161">Esta configuración también se puede leer en el código como variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="82b88-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="82b88-162">En C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) o [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="82b88-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="82b88-163">En JavaScript, use `process.env`.</span><span class="sxs-lookup"><span data-stu-id="82b88-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="82b88-164">Configuración especificada como una variable de entorno del sistema tiene prioridad sobre los valores en el archivo de hello local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="82b88-164">Settings specified as a system environment variable take precedence over values in hello local.settings.json file.</span></span> 

<span data-ttu-id="82b88-165">Configuración de archivo de hello local.settings.json solo se usa con herramientas de funciones cuando se ejecuta localmente.</span><span class="sxs-lookup"><span data-stu-id="82b88-165">Settings in hello local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="82b88-166">De forma predeterminada, esta configuración no se migra automáticamente cuando el proyecto de hello tooAzure publicado.</span><span class="sxs-lookup"><span data-stu-id="82b88-166">By default, these settings are not migrated automatically when hello project is published tooAzure.</span></span> <span data-ttu-id="82b88-167">Hola de uso `--publish-local-settings` cambiar [al publicar](#publish) toomake seguro de estos valores se agregan toohello función aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="82b88-167">Use hello `--publish-local-settings` switch [when you publish](#publish) toomake sure these settings are added toohello function app in Azure.</span></span>

<span data-ttu-id="82b88-168">Cuando no se establece ninguna cadena de conexión de almacenamiento válida para **AzureWebJobsStorage**, se muestra el siguiente mensaje de error de hello:</span><span class="sxs-lookup"><span data-stu-id="82b88-168">When no valid storage connection string is set for **AzureWebJobsStorage**, hello following error message is shown:</span></span>  

><span data-ttu-id="82b88-169">Missing value for AzureWebJobsStorage in local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="82b88-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="82b88-170">This is required for all triggers other than HTTP.</span><span class="sxs-lookup"><span data-stu-id="82b88-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="82b88-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json. (Falta un valor para AzureWebJobsStorage en local.settings.json. Este valor es necesario para todos los desencadenadores que no sean HTTP. Puede ejecutar "func azure functionary fetch-app-settings " o especificar una cadena de conexión en local.settings.json).</span><span class="sxs-lookup"><span data-stu-id="82b88-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="82b88-172">Configuración de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="82b88-172">Configure app settings</span></span>

<span data-ttu-id="82b88-173">tooset un valor para las cadenas de conexión, siga uno de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="82b88-173">tooset a value for connection strings, you can do one of hello following:</span></span>
* <span data-ttu-id="82b88-174">Escriba la cadena de conexión de Hola desde [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="82b88-174">Enter hello connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="82b88-175">Use uno de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="82b88-175">Use one of hello following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="82b88-176">Ambos comandos requieren toofirst inicio de sesión tooAzure.</span><span class="sxs-lookup"><span data-stu-id="82b88-176">Both commands require you toofirst sign-in tooAzure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="82b88-177">Creación de una función</span><span class="sxs-lookup"><span data-stu-id="82b88-177">Create a function</span></span>

<span data-ttu-id="82b88-178">toocreate una función, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="82b88-178">toocreate a function, run hello following command:</span></span>

```
func new
``` 
<span data-ttu-id="82b88-179">`func new`admite Hola argumentos opcionales siguientes:</span><span class="sxs-lookup"><span data-stu-id="82b88-179">`func new` supports hello following optional arguments:</span></span>

| <span data-ttu-id="82b88-180">Argumento</span><span class="sxs-lookup"><span data-stu-id="82b88-180">Argument</span></span>     | <span data-ttu-id="82b88-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="82b88-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="82b88-182">plantilla de Hello programación lenguaje, como C#, F # o JavaScript.</span><span class="sxs-lookup"><span data-stu-id="82b88-182">hello template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="82b88-183">nombre de la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="82b88-183">hello template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="82b88-184">nombre de la función de Hola.</span><span class="sxs-lookup"><span data-stu-id="82b88-184">hello function name.</span></span> |

<span data-ttu-id="82b88-185">Por ejemplo, toocreate un desencadenador de HTTP de JavaScript, ejecute:</span><span class="sxs-lookup"><span data-stu-id="82b88-185">For example, toocreate a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="82b88-186">toocreate una función activa a la cola, ejecute:</span><span class="sxs-lookup"><span data-stu-id="82b88-186">toocreate a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="82b88-187">Ejecución local de funciones</span><span class="sxs-lookup"><span data-stu-id="82b88-187">Run functions locally</span></span>

<span data-ttu-id="82b88-188">toorun un proyecto de funciones, ejecute hello funciones host.</span><span class="sxs-lookup"><span data-stu-id="82b88-188">toorun a Functions project, run hello Functions host.</span></span> <span data-ttu-id="82b88-189">host de Hello permite desencadenadores para todas las funciones de proyecto hello:</span><span class="sxs-lookup"><span data-stu-id="82b88-189">hello host enables triggers for all functions in hello project:</span></span>

```
func host start
```

<span data-ttu-id="82b88-190">`func host start`admite Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="82b88-190">`func host start` supports hello following options:</span></span>

| <span data-ttu-id="82b88-191">Opción</span><span class="sxs-lookup"><span data-stu-id="82b88-191">Option</span></span>     | <span data-ttu-id="82b88-192">Descripción</span><span class="sxs-lookup"><span data-stu-id="82b88-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="82b88-193">Hola toolisten de puerto local en.</span><span class="sxs-lookup"><span data-stu-id="82b88-193">hello local port toolisten on.</span></span> <span data-ttu-id="82b88-194">Valor predeterminado: 7071.</span><span class="sxs-lookup"><span data-stu-id="82b88-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="82b88-195">Opciones de Hello son `VSCode` y `VS`.</span><span class="sxs-lookup"><span data-stu-id="82b88-195">hello options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="82b88-196">Lista separada por comas de orígenes CORS, sin espacios en blanco.</span><span class="sxs-lookup"><span data-stu-id="82b88-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="82b88-197">puerto de Hola para hello nodo depurador toouse.</span><span class="sxs-lookup"><span data-stu-id="82b88-197">hello port for hello node debugger toouse.</span></span> <span data-ttu-id="82b88-198">Valor predeterminado: un valor de launch.json o 5858.</span><span class="sxs-lookup"><span data-stu-id="82b88-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="82b88-199">nivel de seguimiento de la consola de Hello (desactivado, verbose, info, warning o error).</span><span class="sxs-lookup"><span data-stu-id="82b88-199">hello console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="82b88-200">Valor predeterminado: información.</span><span class="sxs-lookup"><span data-stu-id="82b88-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="82b88-201">Hola a tiempo de espera de inicio de hello funciones host t o, en segundos.</span><span class="sxs-lookup"><span data-stu-id="82b88-201">hello time out for hello Functions host t     o start, in seconds.</span></span> <span data-ttu-id="82b88-202">Valor predeterminado: 20 segundos.</span><span class="sxs-lookup"><span data-stu-id="82b88-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="82b88-203">Enlazar toohttps://localhost: {puerto} en lugar de toohttp://localhost: {port}.</span><span class="sxs-lookup"><span data-stu-id="82b88-203">Bind toohttps://localhost:{port} rather than toohttp://localhost:{port}.</span></span> <span data-ttu-id="82b88-204">De forma predeterminada, esta opción crea un certificado de confianza en el equipo.</span><span class="sxs-lookup"><span data-stu-id="82b88-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="82b88-205">Pausa de una entrada adicional antes de salir del proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="82b88-205">Pause for additional input before exiting hello process.</span></span> <span data-ttu-id="82b88-206">Resulta útil cuando se inicia Azure Functions Core Tools desde un entorno de desarrollo integrado (IDE).</span><span class="sxs-lookup"><span data-stu-id="82b88-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="82b88-207">Cuando se inicia el host de las funciones hello, genera funciones de hello desencadenados por dirección URL de HTTP:</span><span class="sxs-lookup"><span data-stu-id="82b88-207">When hello Functions host starts, it outputs hello URL of HTTP-triggered functions:</span></span>

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="82b88-208">Depuración en VS Code o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="82b88-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="82b88-209">tooattach un depurador, pasar hello `--debug` argumento.</span><span class="sxs-lookup"><span data-stu-id="82b88-209">tooattach a debugger, pass hello `--debug` argument.</span></span> <span data-ttu-id="82b88-210">funciones de JavaScript de toodebug, utilice el código de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82b88-210">toodebug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="82b88-211">Para funciones de C#, use Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82b88-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="82b88-212">toodebug C#, utilice `--debug vs`.</span><span class="sxs-lookup"><span data-stu-id="82b88-212">toodebug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="82b88-213">También puede usar [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="82b88-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="82b88-214">host de hello toolaunch y establezca la depuración de JavaScript, ejecute:</span><span class="sxs-lookup"><span data-stu-id="82b88-214">toolaunch hello host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="82b88-215">A continuación, en el código de Visual Studio, en hello **depurar** visualizarla, seleccione **adjuntar funciones tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="82b88-215">Then, in Visual Studio Code, in hello **Debug** view, select **Attach tooAzure Functions**.</span></span> <span data-ttu-id="82b88-216">Puede asociar puntos de interrupción, inspeccionar variables y recorrer el código.</span><span class="sxs-lookup"><span data-stu-id="82b88-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![Depuración de JavaScript con Visual Studio Code](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a><span data-ttu-id="82b88-218">Función de paso de prueba datos tooa</span><span class="sxs-lookup"><span data-stu-id="82b88-218">Passing test data tooa function</span></span>

<span data-ttu-id="82b88-219">También puede invocar una función directamente mediante `func run <FunctionName>` y proporcionar datos de entrada para la función hello.</span><span class="sxs-lookup"><span data-stu-id="82b88-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for hello function.</span></span> <span data-ttu-id="82b88-220">Este comando es similar toorunning una función mediante hello **prueba** ficha Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="82b88-220">This command is similar toorunning a function using hello **Test** tab in hello Azure portal.</span></span> <span data-ttu-id="82b88-221">Este comando inicia el host de las funciones todo Hola.</span><span class="sxs-lookup"><span data-stu-id="82b88-221">This command launches hello entire Functions host.</span></span>

<span data-ttu-id="82b88-222">`func run`admite Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="82b88-222">`func run` supports hello following options:</span></span>

| <span data-ttu-id="82b88-223">Opción</span><span class="sxs-lookup"><span data-stu-id="82b88-223">Option</span></span>     | <span data-ttu-id="82b88-224">Descripción</span><span class="sxs-lookup"><span data-stu-id="82b88-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="82b88-225">Contenido alineado.</span><span class="sxs-lookup"><span data-stu-id="82b88-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="82b88-226">Asociar un proceso de host de depuración toohello antes de ejecutar la función hello.</span><span class="sxs-lookup"><span data-stu-id="82b88-226">Attach a debugger toohello host process before running hello function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="82b88-227">Toowait de tiempo (en segundos) hasta que el host local de las funciones de hello está listo.</span><span class="sxs-lookup"><span data-stu-id="82b88-227">Time toowait (in seconds) until hello local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="82b88-228">Hola toouse de nombre de archivo como contenido.</span><span class="sxs-lookup"><span data-stu-id="82b88-228">hello file name toouse as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="82b88-229">No pide entrada.</span><span class="sxs-lookup"><span data-stu-id="82b88-229">Does not prompt for input.</span></span> <span data-ttu-id="82b88-230">Resulta útil en escenarios de automatización.</span><span class="sxs-lookup"><span data-stu-id="82b88-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="82b88-231">Por ejemplo, toocall una función activa de HTTP y cuerpo de contenido de paso, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="82b88-231">For example, toocall an HTTP-triggered function and pass content body, run hello following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="82b88-232"><a name="publish"></a>Publicar tooAzure</span><span class="sxs-lookup"><span data-stu-id="82b88-232"><a name="publish"></a>Publish tooAzure</span></span>

<span data-ttu-id="82b88-233">una aplicación de función de las funciones proyecto tooa en Azure, use hello toopublish `publish` comando:</span><span class="sxs-lookup"><span data-stu-id="82b88-233">toopublish a Functions project tooa function app in Azure, use hello `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="82b88-234">Puede usar Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="82b88-234">You can use hello following options:</span></span>

| <span data-ttu-id="82b88-235">Opción</span><span class="sxs-lookup"><span data-stu-id="82b88-235">Option</span></span>     | <span data-ttu-id="82b88-236">Descripción</span><span class="sxs-lookup"><span data-stu-id="82b88-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="82b88-237">Configuración de publicación en local.settings.json tooAzure, preguntar toooverwrite si Hola configuración ya existe.</span><span class="sxs-lookup"><span data-stu-id="82b88-237">Publish settings in local.settings.json tooAzure, prompting toooverwrite if hello setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="82b88-238">Debe usarse con `-i`.</span><span class="sxs-lookup"><span data-stu-id="82b88-238">Must be used with `-i`.</span></span> <span data-ttu-id="82b88-239">Sobrescribe AppSettings en Azure con el valor local si es distinto.</span><span class="sxs-lookup"><span data-stu-id="82b88-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="82b88-240">El valor predeterminado es Preguntar.</span><span class="sxs-lookup"><span data-stu-id="82b88-240">Default is prompt.</span></span>|

<span data-ttu-id="82b88-241">Hola `publish` comando carga contenido hello del directorio de proyecto de funciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="82b88-241">hello `publish` command uploads hello contents of hello Functions project directory.</span></span> <span data-ttu-id="82b88-242">Si elimina archivos localmente, Hola `publish` comando no los elimina de Azure.</span><span class="sxs-lookup"><span data-stu-id="82b88-242">If you delete files locally, hello `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="82b88-243">Puede eliminar archivos en Azure mediante hello [herramienta Kudu](functions-how-to-use-azure-function-app-settings.md#kudu) en hello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="82b88-243">You can delete files in Azure by using hello [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in hello [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="82b88-244">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="82b88-244">Next steps</span></span>

<span data-ttu-id="82b88-245">Azure Functions Core Tools es [código abierto que se hospeda en GitHub](https://github.com/azure/azure-functions-cli).</span><span class="sxs-lookup"><span data-stu-id="82b88-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="82b88-246">una solicitud de error o una característica, toofile [abrir un problema de GitHub](https://github.com/azure/azure-functions-cli/issues).</span><span class="sxs-lookup"><span data-stu-id="82b88-246">toofile a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[herramientas básicas de las funciones de Azure]: https://www.npmjs.com/package/azure-functions-core-tools
[portal de Azure]: https://portal.azure.com 
