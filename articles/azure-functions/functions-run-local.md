---
title: "Desarrollo y ejecución de funciones de Azure de forma local | Microsoft Docs"
description: "Aprenda a codificar y probar funciones de Azure en la máquina local antes de ejecutarlas en Azure Functions."
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
ms.openlocfilehash: bbe03973dbd7c70463caa6d1a45efae2ec722c05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="a4f08-103">Codificación y comprobación de las funciones de Azure en un entorno local</span><span class="sxs-lookup"><span data-stu-id="a4f08-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="a4f08-104">A pesar de que [Azure Portal] proporciona un conjunto completo de herramientas para desarrollar y probar Azure Functions, muchos desarrolladores prefieren desarrollar productos localmente.</span><span class="sxs-lookup"><span data-stu-id="a4f08-104">While the [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="a4f08-105">Azure Functions facilita el uso de su editor de código favorito y de las herramientas de desarrollo locales para desarrollar y probar sus funciones en un equipo local.</span><span class="sxs-lookup"><span data-stu-id="a4f08-105">Azure Functions makes it easy to use your favorite code editor and local development tools to develop and test your functions on your local computer.</span></span> <span data-ttu-id="a4f08-106">Las funciones pueden desencadenarse a partir de eventos de Azure, y puede depurar sus funciones en C# y JavaScript en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="a4f08-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="a4f08-107">Si es un desarrollador de C# de Visual Studio, Azure Functions también [permite la integración con Visual Studio 2017](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="a4f08-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-the-azure-functions-core-tools"></a><span data-ttu-id="a4f08-108">Instalación de Azure Functions Core Tools</span><span class="sxs-lookup"><span data-stu-id="a4f08-108">Install the Azure Functions Core Tools</span></span>

<span data-ttu-id="a4f08-109">Azure Functions Core Tools es una versión local del entorno de ejecución de Azure Functions que puede ejecutar en el equipo Windows local.</span><span class="sxs-lookup"><span data-stu-id="a4f08-109">Azure Functions Core Tools is a local version of the Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="a4f08-110">No se trata de un emulador o simulador.</span><span class="sxs-lookup"><span data-stu-id="a4f08-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="a4f08-111">Se trata del mismo entorno de ejecución que se usa en Functions en Azure.</span><span class="sxs-lookup"><span data-stu-id="a4f08-111">It's the same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="a4f08-112">[Azure Functions Core Tools] se proporciona como un paquete npm.</span><span class="sxs-lookup"><span data-stu-id="a4f08-112">The [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="a4f08-113">Primero debe [instalar NodeJS](https://docs.npmjs.com/getting-started/installing-node), que incluye npm.</span><span class="sxs-lookup"><span data-stu-id="a4f08-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="a4f08-114">En este momento el paquete Azure Functions Core Tools solo se puede instalar en equipos Windows.</span><span class="sxs-lookup"><span data-stu-id="a4f08-114">At this time, the Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="a4f08-115">Esta restricción se debe a una limitación temporal del host de Functions.</span><span class="sxs-lookup"><span data-stu-id="a4f08-115">This restriction is due to a temporary limitation in the Functions host.</span></span>

<span data-ttu-id="a4f08-116">[Azure Functions Core Tools] agrega los siguientes alias de comando:</span><span class="sxs-lookup"><span data-stu-id="a4f08-116">[Azure Functions Core Tools] adds the following command aliases:</span></span>
* <span data-ttu-id="a4f08-117">**func**</span><span class="sxs-lookup"><span data-stu-id="a4f08-117">**func**</span></span>
* <span data-ttu-id="a4f08-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="a4f08-118">**azfun**</span></span>
* <span data-ttu-id="a4f08-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="a4f08-119">**azurefunctions**</span></span>

<span data-ttu-id="a4f08-120">Es posible utilizar cualquier de estos alias en lugar del alias `func` de este tema.</span><span class="sxs-lookup"><span data-stu-id="a4f08-120">All of these alias can be used instead of `func` shown in the examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="a4f08-121">Creación de un proyecto local de Functions</span><span class="sxs-lookup"><span data-stu-id="a4f08-121">Create a local Functions project</span></span>

<span data-ttu-id="a4f08-122">Cuando se ejecuta localmente, un proyecto de Functions es un directorio que tiene los archivos host.json y local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="a4f08-122">When running locally, a Functions project is a directory that has the files host.json and local.settings.json.</span></span> <span data-ttu-id="a4f08-123">Este directorio es el equivalente a una aplicación de función en Azure.</span><span class="sxs-lookup"><span data-stu-id="a4f08-123">This directory is the equivalent of a function app in Azure.</span></span> <span data-ttu-id="a4f08-124">Para obtener más información sobre la estructura de carpetas de Azure Functions, vea la [Guía para desarrolladores de Azure Functions](functions-reference.md#folder-structure).</span><span class="sxs-lookup"><span data-stu-id="a4f08-124">To learn more about the Azure Functions folder structure, see the [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="a4f08-125">En el símbolo del sistema, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a4f08-125">At a command prompt, run the following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="a4f08-126">La salida tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="a4f08-126">The output looks like the following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="a4f08-127">Para no participar en la creación de un repositorio Git, use la opción `--no-source-control [-n]`.</span><span class="sxs-lookup"><span data-stu-id="a4f08-127">To opt out of creating a Git repository, use the option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="a4f08-128">Archivo de configuración local</span><span class="sxs-lookup"><span data-stu-id="a4f08-128">Local settings file</span></span>

<span data-ttu-id="a4f08-129">El archivo local.settings.json almacena la configuración de la aplicación, las cadenas de conexión y la configuración de Azure Functions Core Tools.</span><span class="sxs-lookup"><span data-stu-id="a4f08-129">The file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="a4f08-130">Tiene la siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="a4f08-130">It has the following structure:</span></span>

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
| <span data-ttu-id="a4f08-131">Configuración</span><span class="sxs-lookup"><span data-stu-id="a4f08-131">Setting</span></span>      | <span data-ttu-id="a4f08-132">Descripción</span><span class="sxs-lookup"><span data-stu-id="a4f08-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="a4f08-133">**IsEncrypted**</span><span class="sxs-lookup"><span data-stu-id="a4f08-133">**IsEncrypted**</span></span> | <span data-ttu-id="a4f08-134">Cuando se establece en **true**, todos los valores se cifran con una clave de máquina local.</span><span class="sxs-lookup"><span data-stu-id="a4f08-134">When set to **true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="a4f08-135">Se usa con los comandos `func settings`.</span><span class="sxs-lookup"><span data-stu-id="a4f08-135">Used with `func settings` commands.</span></span> <span data-ttu-id="a4f08-136">El valor predeterminado es **false**.</span><span class="sxs-lookup"><span data-stu-id="a4f08-136">Default value is **false**.</span></span> |
| <span data-ttu-id="a4f08-137">**Valores**</span><span class="sxs-lookup"><span data-stu-id="a4f08-137">**Values**</span></span> | <span data-ttu-id="a4f08-138">Colección de opciones de configuración de la aplicación que se usa en la ejecución local.</span><span class="sxs-lookup"><span data-stu-id="a4f08-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="a4f08-139">Agregue la configuración de la aplicación a este objeto.</span><span class="sxs-lookup"><span data-stu-id="a4f08-139">Add your application settings to this object.</span></span>  |
| <span data-ttu-id="a4f08-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="a4f08-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="a4f08-141">Establece la cadena de conexión para la cuenta de Azure Storage que el entorno de ejecución de Azure Functions usa internamente.</span><span class="sxs-lookup"><span data-stu-id="a4f08-141">Sets the connection string to the Azure Storage account that is used internally by the Azure Functions runtime.</span></span> <span data-ttu-id="a4f08-142">La cuenta de almacenamiento admite los desencadenadores de su función.</span><span class="sxs-lookup"><span data-stu-id="a4f08-142">The storage account supports your function's triggers.</span></span> <span data-ttu-id="a4f08-143">Esta configuración de conexión de la cuenta de almacenamiento es necesaria para todas las funciones, salvo en el caso de las funciones desencadenadas de HTTP.</span><span class="sxs-lookup"><span data-stu-id="a4f08-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="a4f08-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="a4f08-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="a4f08-145">Establece la cadena de conexión a la cuenta de Azure Storage que se usa para almacenar los registros de funciones.</span><span class="sxs-lookup"><span data-stu-id="a4f08-145">Sets the connection string to the Azure Storage account that is used to store the function logs.</span></span> <span data-ttu-id="a4f08-146">Este valor opcional hace que se pueda acceder a los registros en el portal.</span><span class="sxs-lookup"><span data-stu-id="a4f08-146">This optional value makes the logs accessible in the portal.</span></span>|
| <span data-ttu-id="a4f08-147">**Host**</span><span class="sxs-lookup"><span data-stu-id="a4f08-147">**Host**</span></span> | <span data-ttu-id="a4f08-148">La configuración que se muestra esta sección permite personalizar el proceso de host de Functions cuando se ejecuta localmente.</span><span class="sxs-lookup"><span data-stu-id="a4f08-148">Settings in this section customize the Functions host process when running locally.</span></span> | 
| <span data-ttu-id="a4f08-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="a4f08-149">**LocalHttpPort**</span></span> | <span data-ttu-id="a4f08-150">Establece el puerto predeterminado que se usa cuando al ejecutar el host de Functions local (`func host start` y `func run`).</span><span class="sxs-lookup"><span data-stu-id="a4f08-150">Sets the default port used when running the local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="a4f08-151">La opción de línea de comandos `--port` tiene prioridad sobre este valor.</span><span class="sxs-lookup"><span data-stu-id="a4f08-151">The `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="a4f08-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="a4f08-152">**CORS**</span></span> | <span data-ttu-id="a4f08-153">Define los orígenes permitidos para el [uso compartido de recursos entre orígenes (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span><span class="sxs-lookup"><span data-stu-id="a4f08-153">Defines the origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="a4f08-154">Los orígenes se proporcionan en una lista de valores separados por comas y sin espacios.</span><span class="sxs-lookup"><span data-stu-id="a4f08-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="a4f08-155">Se admite el valor comodín (**\***), lo que permite realizar solicitudes desde cualquier origen.</span><span class="sxs-lookup"><span data-stu-id="a4f08-155">The wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="a4f08-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="a4f08-156">**ConnectionStrings**</span></span> | <span data-ttu-id="a4f08-157">Contiene las cadenas de conexión de la base de datos para las funciones.</span><span class="sxs-lookup"><span data-stu-id="a4f08-157">Contains the database connection strings for your functions.</span></span> <span data-ttu-id="a4f08-158">Las cadenas de conexión de este objeto se agregan al entorno con el tipo de proveedor de **System.Data.SqlClient**.</span><span class="sxs-lookup"><span data-stu-id="a4f08-158">Connection strings in this object are added to the environment with the provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="a4f08-159">La mayoría de los desencadenadores y los enlaces tienen una propiedad **Connection** que se asigna al nombre de una variable de entorno o a una configuración de aplicación.</span><span class="sxs-lookup"><span data-stu-id="a4f08-159">Most triggers and bindings have a **Connection** property that maps to the name of an environment variable or app setting.</span></span> <span data-ttu-id="a4f08-160">Por cada propiedad de conexión debe haber una configuración de aplicación definida en el archivo local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="a4f08-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="a4f08-161">Esta configuración también se puede leer en el código como variables de entorno.</span><span class="sxs-lookup"><span data-stu-id="a4f08-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="a4f08-162">En C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) o [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4f08-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="a4f08-163">En JavaScript, use `process.env`.</span><span class="sxs-lookup"><span data-stu-id="a4f08-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="a4f08-164">Las opciones de configuración especificadas como variable de entorno del sistema tienen prioridad sobre otros valores del archivo local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="a4f08-164">Settings specified as a system environment variable take precedence over values in the local.settings.json file.</span></span> 

<span data-ttu-id="a4f08-165">Las herramientas de Functions solo usan las opciones de configuración de dicho archivo cuando las herramientas se ejecutan localmente.</span><span class="sxs-lookup"><span data-stu-id="a4f08-165">Settings in the local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="a4f08-166">De manera predeterminada, estas opciones de configuración no se migran automáticamente cuando el proyecto se publica en Azure.</span><span class="sxs-lookup"><span data-stu-id="a4f08-166">By default, these settings are not migrated automatically when the project is published to Azure.</span></span> <span data-ttu-id="a4f08-167">Use el conmutador `--publish-local-settings` [al publicarlo](#publish) para asegurarse de que la configuración se agregue a la aplicación de función en Azure.</span><span class="sxs-lookup"><span data-stu-id="a4f08-167">Use the `--publish-local-settings` switch [when you publish](#publish) to make sure these settings are added to the function app in Azure.</span></span>

<span data-ttu-id="a4f08-168">Cuando no se establece ninguna cadena de conexión de almacenamiento válida para **AzureWebJobsStorage**, se muestra el siguiente mensaje de error:</span><span class="sxs-lookup"><span data-stu-id="a4f08-168">When no valid storage connection string is set for **AzureWebJobsStorage**, the following error message is shown:</span></span>  

><span data-ttu-id="a4f08-169">Missing value for AzureWebJobsStorage in local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="a4f08-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="a4f08-170">This is required for all triggers other than HTTP.</span><span class="sxs-lookup"><span data-stu-id="a4f08-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="a4f08-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json. (Falta un valor para AzureWebJobsStorage en local.settings.json. Este valor es necesario para todos los desencadenadores que no sean HTTP. Puede ejecutar "func azure functionary fetch-app-settings " o especificar una cadena de conexión en local.settings.json).</span><span class="sxs-lookup"><span data-stu-id="a4f08-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note to not use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="a4f08-172">Configuración de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="a4f08-172">Configure app settings</span></span>

<span data-ttu-id="a4f08-173">Para establecer un valor para las cadenas de conexión, puede realizar alguna de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="a4f08-173">To set a value for connection strings, you can do one of the following:</span></span>
* <span data-ttu-id="a4f08-174">Indique la cadena de conexión desde el [Explorador de Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="a4f08-174">Enter the connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="a4f08-175">Use uno de los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a4f08-175">Use one of the following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="a4f08-176">Ambos comandos requieren que primero inicie sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="a4f08-176">Both commands require you to first sign-in to Azure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="a4f08-177">Creación de una función</span><span class="sxs-lookup"><span data-stu-id="a4f08-177">Create a function</span></span>

<span data-ttu-id="a4f08-178">Para crear una función, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a4f08-178">To create a function, run the following command:</span></span>

```
func new
``` 
<span data-ttu-id="a4f08-179">`func new` admite los siguientes argumentos opcionales:</span><span class="sxs-lookup"><span data-stu-id="a4f08-179">`func new` supports the following optional arguments:</span></span>

| <span data-ttu-id="a4f08-180">Argumento</span><span class="sxs-lookup"><span data-stu-id="a4f08-180">Argument</span></span>     | <span data-ttu-id="a4f08-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="a4f08-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="a4f08-182">Lenguaje de programación de la plantilla, como C#, F# o JavaScript.</span><span class="sxs-lookup"><span data-stu-id="a4f08-182">The template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="a4f08-183">Nombre de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="a4f08-183">The template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="a4f08-184">Nombre de la función.</span><span class="sxs-lookup"><span data-stu-id="a4f08-184">The function name.</span></span> |

<span data-ttu-id="a4f08-185">Por ejemplo, para crear un desencadenador HTTP de JavaScript, ejecute:</span><span class="sxs-lookup"><span data-stu-id="a4f08-185">For example, to create a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="a4f08-186">Para crear una función desencadenada por la cola, ejecute:</span><span class="sxs-lookup"><span data-stu-id="a4f08-186">To create a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="a4f08-187">Ejecución local de funciones</span><span class="sxs-lookup"><span data-stu-id="a4f08-187">Run functions locally</span></span>

<span data-ttu-id="a4f08-188">Para ejecutar un proyecto de Functions, ejecute el host de Functions.</span><span class="sxs-lookup"><span data-stu-id="a4f08-188">To run a Functions project, run the Functions host.</span></span> <span data-ttu-id="a4f08-189">El host habilita desencadenadores para todas las funciones del proyecto:</span><span class="sxs-lookup"><span data-stu-id="a4f08-189">The host enables triggers for all functions in the project:</span></span>

```
func host start
```

<span data-ttu-id="a4f08-190">`func host start` admite las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="a4f08-190">`func host start` supports the following options:</span></span>

| <span data-ttu-id="a4f08-191">Opción</span><span class="sxs-lookup"><span data-stu-id="a4f08-191">Option</span></span>     | <span data-ttu-id="a4f08-192">Descripción</span><span class="sxs-lookup"><span data-stu-id="a4f08-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="a4f08-193">Puerto local en el que se escucha.</span><span class="sxs-lookup"><span data-stu-id="a4f08-193">The local port to listen on.</span></span> <span data-ttu-id="a4f08-194">Valor predeterminado: 7071.</span><span class="sxs-lookup"><span data-stu-id="a4f08-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="a4f08-195">Las opciones son `VSCode` y `VS`.</span><span class="sxs-lookup"><span data-stu-id="a4f08-195">The options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="a4f08-196">Lista separada por comas de orígenes CORS, sin espacios en blanco.</span><span class="sxs-lookup"><span data-stu-id="a4f08-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="a4f08-197">Puerto del depurador de nodo que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="a4f08-197">The port for the node debugger to use.</span></span> <span data-ttu-id="a4f08-198">Valor predeterminado: un valor de launch.json o 5858.</span><span class="sxs-lookup"><span data-stu-id="a4f08-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="a4f08-199">Nivel de seguimiento de la consola (desactivado, detallado, información, advertencia o error).</span><span class="sxs-lookup"><span data-stu-id="a4f08-199">The console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="a4f08-200">Valor predeterminado: información.</span><span class="sxs-lookup"><span data-stu-id="a4f08-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="a4f08-201">Tiempo de espera en segundos para iniciar el host de Functions.</span><span class="sxs-lookup"><span data-stu-id="a4f08-201">The time out for the Functions host t     o start, in seconds.</span></span> <span data-ttu-id="a4f08-202">Valor predeterminado: 20 segundos.</span><span class="sxs-lookup"><span data-stu-id="a4f08-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="a4f08-203">Se enlaza a https://localhost:{port} en lugar de a http://localhost:{port}.</span><span class="sxs-lookup"><span data-stu-id="a4f08-203">Bind to https://localhost:{port} rather than to http://localhost:{port}.</span></span> <span data-ttu-id="a4f08-204">De forma predeterminada, esta opción crea un certificado de confianza en el equipo.</span><span class="sxs-lookup"><span data-stu-id="a4f08-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="a4f08-205">Se pone en pausa en espera de entrada adicional antes de salir del proceso.</span><span class="sxs-lookup"><span data-stu-id="a4f08-205">Pause for additional input before exiting the process.</span></span> <span data-ttu-id="a4f08-206">Resulta útil cuando se inicia Azure Functions Core Tools desde un entorno de desarrollo integrado (IDE).</span><span class="sxs-lookup"><span data-stu-id="a4f08-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="a4f08-207">Cuando se inicia el host de Functions, devuelve la dirección URL de las funciones desencadenadas por HTTP:</span><span class="sxs-lookup"><span data-stu-id="a4f08-207">When the Functions host starts, it outputs the URL of HTTP-triggered functions:</span></span>

```
Found the following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="a4f08-208">Depuración en VS Code o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a4f08-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="a4f08-209">Para asociar un depurador, pase el argumento `--debug`.</span><span class="sxs-lookup"><span data-stu-id="a4f08-209">To attach a debugger, pass the `--debug` argument.</span></span> <span data-ttu-id="a4f08-210">Para depurar funciones de JavaScript, use Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="a4f08-210">To debug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="a4f08-211">Para funciones de C#, use Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a4f08-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="a4f08-212">Para depurar funciones de C#, use `--debug vs`.</span><span class="sxs-lookup"><span data-stu-id="a4f08-212">To debug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="a4f08-213">También puede usar [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="a4f08-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="a4f08-214">Para iniciar el host y configurar la depuración de JavaScript, ejecute:</span><span class="sxs-lookup"><span data-stu-id="a4f08-214">To launch the host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="a4f08-215">Luego, en la vista de **depuración** de Visual Studio Code, seleccione **Attach to Azure Functions** (Asociar a Azure Functions).</span><span class="sxs-lookup"><span data-stu-id="a4f08-215">Then, in Visual Studio Code, in the **Debug** view, select **Attach to Azure Functions**.</span></span> <span data-ttu-id="a4f08-216">Puede asociar puntos de interrupción, inspeccionar variables y recorrer el código.</span><span class="sxs-lookup"><span data-stu-id="a4f08-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![Depuración de JavaScript con Visual Studio Code](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-to-a-function"></a><span data-ttu-id="a4f08-218">Paso de datos de prueba a una función</span><span class="sxs-lookup"><span data-stu-id="a4f08-218">Passing test data to a function</span></span>

<span data-ttu-id="a4f08-219">También puede invocar una función directamente con `func run <FunctionName>` y proporcionar datos de entrada para la función.</span><span class="sxs-lookup"><span data-stu-id="a4f08-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for the function.</span></span> <span data-ttu-id="a4f08-220">Este comando es similar a la ejecución de una función con la pestaña **Prueba** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a4f08-220">This command is similar to running a function using the **Test** tab in the Azure portal.</span></span> <span data-ttu-id="a4f08-221">Este comando inicia el host de Functions completo.</span><span class="sxs-lookup"><span data-stu-id="a4f08-221">This command launches the entire Functions host.</span></span>

<span data-ttu-id="a4f08-222">`func run` admite las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="a4f08-222">`func run` supports the following options:</span></span>

| <span data-ttu-id="a4f08-223">Opción</span><span class="sxs-lookup"><span data-stu-id="a4f08-223">Option</span></span>     | <span data-ttu-id="a4f08-224">Descripción</span><span class="sxs-lookup"><span data-stu-id="a4f08-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="a4f08-225">Contenido alineado.</span><span class="sxs-lookup"><span data-stu-id="a4f08-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="a4f08-226">Se asocia un depurador al proceso de host antes de ejecutar la función.</span><span class="sxs-lookup"><span data-stu-id="a4f08-226">Attach a debugger to the host process before running the function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="a4f08-227">Tiempo de espera (en segundos) hasta que el host local de Functions está listo.</span><span class="sxs-lookup"><span data-stu-id="a4f08-227">Time to wait (in seconds) until the local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="a4f08-228">Nombre del archivo que se usa como contenido.</span><span class="sxs-lookup"><span data-stu-id="a4f08-228">The file name to use as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="a4f08-229">No pide entrada.</span><span class="sxs-lookup"><span data-stu-id="a4f08-229">Does not prompt for input.</span></span> <span data-ttu-id="a4f08-230">Resulta útil en escenarios de automatización.</span><span class="sxs-lookup"><span data-stu-id="a4f08-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="a4f08-231">Por ejemplo, para llamar a una función desencadenada por HTTP y pasar cuerpo del contenido, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a4f08-231">For example, to call an HTTP-triggered function and pass content body, run the following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="a4f08-232"><a name="publish"></a>Publicación en Azure</span><span class="sxs-lookup"><span data-stu-id="a4f08-232"><a name="publish"></a>Publish to Azure</span></span>

<span data-ttu-id="a4f08-233">Para publicar un proyecto de Functions en una aplicación de función en Azure, use el comando `publish`:</span><span class="sxs-lookup"><span data-stu-id="a4f08-233">To publish a Functions project to a function app in Azure, use the `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="a4f08-234">Puede usar las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="a4f08-234">You can use the following options:</span></span>

| <span data-ttu-id="a4f08-235">Opción</span><span class="sxs-lookup"><span data-stu-id="a4f08-235">Option</span></span>     | <span data-ttu-id="a4f08-236">Descripción</span><span class="sxs-lookup"><span data-stu-id="a4f08-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="a4f08-237">Se publica la configuración de local.settings.json en Azure, se pide que se sobrescriba si la configuración ya existe.</span><span class="sxs-lookup"><span data-stu-id="a4f08-237">Publish settings in local.settings.json to Azure, prompting to overwrite if the setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="a4f08-238">Debe usarse con `-i`.</span><span class="sxs-lookup"><span data-stu-id="a4f08-238">Must be used with `-i`.</span></span> <span data-ttu-id="a4f08-239">Sobrescribe AppSettings en Azure con el valor local si es distinto.</span><span class="sxs-lookup"><span data-stu-id="a4f08-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="a4f08-240">El valor predeterminado es Preguntar.</span><span class="sxs-lookup"><span data-stu-id="a4f08-240">Default is prompt.</span></span>|

<span data-ttu-id="a4f08-241">El comando `publish` carga el contenido del directorio del proyecto de Functions.</span><span class="sxs-lookup"><span data-stu-id="a4f08-241">The `publish` command uploads the contents of the Functions project directory.</span></span> <span data-ttu-id="a4f08-242">Si elimina archivos localmente, el comando `publish` no los eliminará de Azure.</span><span class="sxs-lookup"><span data-stu-id="a4f08-242">If you delete files locally, the `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="a4f08-243">Puede eliminar archivos de Azure con la [herramienta Kudu](functions-how-to-use-azure-function-app-settings.md#kudu) de [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="a4f08-243">You can delete files in Azure by using the [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in the [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4f08-244">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a4f08-244">Next steps</span></span>

<span data-ttu-id="a4f08-245">Azure Functions Core Tools es [código abierto que se hospeda en GitHub](https://github.com/azure/azure-functions-cli).</span><span class="sxs-lookup"><span data-stu-id="a4f08-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="a4f08-246">Para notificar un error o realizar una solicitud de característica, [abra un problema de GitHub](https://github.com/azure/azure-functions-cli/issues).</span><span class="sxs-lookup"><span data-stu-id="a4f08-246">To file a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[Azure Functions Core Tools]: https://www.npmjs.com/package/azure-functions-core-tools
[Azure Portal]: https://portal.azure.com 
