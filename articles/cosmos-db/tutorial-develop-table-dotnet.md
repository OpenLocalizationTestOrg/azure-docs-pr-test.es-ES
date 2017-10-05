---
title: 'Azure Cosmos DB: desarrollo con Table API en .NET | Microsoft Docs'
description: "Obtenga información sobre cómo desarrollar con Table API de Azure Cosmos DB en .NET"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 52cb5f2569b6c3a5301752b1e8bfb6cea13ff7f6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cosmos-db-develop-with-the-table-api-in-net"></a><span data-ttu-id="b55f0-103">Azure Cosmos DB: desarrollo con Table API en .NET</span><span class="sxs-lookup"><span data-stu-id="b55f0-103">Azure Cosmos DB: Develop with the Table API in .NET</span></span>

<span data-ttu-id="b55f0-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b55f0-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="b55f0-105">Puede crear rápidamente bases de datos de documentos, clave-valor y grafos y realizar consultas en ellas. Todas las bases de datos se beneficiarán de las funcionalidades de distribución global y escala horizontal en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b55f0-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

<span data-ttu-id="b55f0-106">En este tutorial se describen las tareas siguientes:</span><span class="sxs-lookup"><span data-stu-id="b55f0-106">This tutorial covers the following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="b55f0-107">Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b55f0-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="b55f0-108">Habilitación de la funcionalidad en el archivo app.config</span><span class="sxs-lookup"><span data-stu-id="b55f0-108">Enable functionality in the app.config file</span></span> 
> * <span data-ttu-id="b55f0-109">Creación de una tabla con [Table API](table-introduction.md) (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="b55f0-109">Create a table using the [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="b55f0-110">Adición de una entidad a una tabla</span><span class="sxs-lookup"><span data-stu-id="b55f0-110">Add an entity to a table</span></span> 
> * <span data-ttu-id="b55f0-111">Inserción de un lote de entidades</span><span class="sxs-lookup"><span data-stu-id="b55f0-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="b55f0-112">una sola entidad</span><span class="sxs-lookup"><span data-stu-id="b55f0-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="b55f0-113">Consulta de entidades con índices secundarios automáticos</span><span class="sxs-lookup"><span data-stu-id="b55f0-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="b55f0-114">una entidad</span><span class="sxs-lookup"><span data-stu-id="b55f0-114">Replace an entity</span></span> 
> * <span data-ttu-id="b55f0-115">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="b55f0-115">Delete an entity</span></span> 
> * <span data-ttu-id="b55f0-116">Eliminación de una tabla</span><span class="sxs-lookup"><span data-stu-id="b55f0-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="b55f0-117">Tablas en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b55f0-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="b55f0-118">Azure Cosmos DB proporciona [Table API](table-introduction.md) (versión preliminar) para las aplicaciones que necesitan un almacén de pares clave-valor con un diseño sin esquema.</span><span class="sxs-lookup"><span data-stu-id="b55f0-118">Azure Cosmos DB provides the [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="b55f0-119">Las API de REST y los SDK de [Azure Table Storage](../storage/common/storage-introduction.md) se pueden usar para trabajar con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b55f0-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used to work with Azure Cosmos DB.</span></span> <span data-ttu-id="b55f0-120">Puede usar Azure Cosmos DB para crear tablas con requisitos de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="b55f0-120">You can use Azure Cosmos DB to create tables with high throughput requirements.</span></span> <span data-ttu-id="b55f0-121">Azure Cosmos DB admite tablas optimizadas para el rendimiento (llamadas informalmente "tablas premium"), actualmente en versión preliminar pública.</span><span class="sxs-lookup"><span data-stu-id="b55f0-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="b55f0-122">Puede seguir usando Azure Table Storage para las tablas con requisitos de alto almacenamiento y menor rendimiento.</span><span class="sxs-lookup"><span data-stu-id="b55f0-122">You can continue to use Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="b55f0-123">Azure Cosmos DB incorporará compatibilidad con tablas optimizadas para almacenamiento en una futura actualización; además, las cuentas existentes y nuevas de Azure Table Storage se actualizarán sin problemas a Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b55f0-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded to Azure Cosmos DB.</span></span>

<span data-ttu-id="b55f0-124">Si actualmente usa Azure Table Storage, obtendrá las siguientes ventajas con la versión preliminar de las "tablas premium":</span><span class="sxs-lookup"><span data-stu-id="b55f0-124">If you currently use Azure Table storage, you gain the following benefits with the "premium table" preview:</span></span>

- <span data-ttu-id="b55f0-125">[Distribución global](distribute-data-globally.md) llave en mano con hospedaje múltiple y [conmutaciones por error manuales y automáticas](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="b55f0-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="b55f0-126">Compatibilidad con el indexado automático independiente del esquema con respecto a todas las propiedades ("índices secundarios") y consultas rápidas</span><span class="sxs-lookup"><span data-stu-id="b55f0-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="b55f0-127">Compatibilidad con el [escalado independiente de proceso y almacenamiento](partition-data.md), en cualquier número de regiones</span><span class="sxs-lookup"><span data-stu-id="b55f0-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="b55f0-128">Compatibilidad con [rendimiento dedicado por tabla](request-units.md) que se puede escalar de cientos a millones de solicitudes por segundo</span><span class="sxs-lookup"><span data-stu-id="b55f0-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds to millions of requests per second</span></span>
- <span data-ttu-id="b55f0-129">Compatibilidad con [cinco niveles de coherencia bien definidos](consistency-levels.md) para compensar la disponibilidad, la latencia y la coherencia en función de lo que necesita la aplicación</span><span class="sxs-lookup"><span data-stu-id="b55f0-129">Support for [five tunable consistency levels](consistency-levels.md) to trade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="b55f0-130">Disponibilidad del 99,99 % dentro de una única región y la capacidad de agregar más regiones para tener una mayor disponibilidad, además de [Acuerdos de Nivel de Servicio completos líderes en el sector](https://azure.microsoft.com/support/legal/sla/cosmos-db/) sobre la disponibilidad general</span><span class="sxs-lookup"><span data-stu-id="b55f0-130">99.99% availability within a single region, and ability to add more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="b55f0-131">Trabajo con el SDK de .NET para Azure Storage, sin cambios de código en la aplicación</span><span class="sxs-lookup"><span data-stu-id="b55f0-131">Work with the existing Azure storage .NET SDK, and no code changes to your application</span></span>

<span data-ttu-id="b55f0-132">Durante la versión preliminar, Azure Cosmos DB admite Table API con el SDK de .NET.</span><span class="sxs-lookup"><span data-stu-id="b55f0-132">During the preview, Azure Cosmos DB supports the Table API using the .NET SDK.</span></span> <span data-ttu-id="b55f0-133">Puede descargar el [SDK de versión preliminar de Azure Storage](https://aka.ms/premiumtablenuget) en NuGet, que tiene las mismas firmas de método y clases que el [SDK de Azure Storage](https://www.nuget.org/packages/WindowsAzure.Storage), pero que también se puede conectar a cuentas de Azure Cosmos DB mediante Table API.</span><span class="sxs-lookup"><span data-stu-id="b55f0-133">You can download the [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has the same classes and method signatures as the [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect to Azure Cosmos DB accounts using the Table API.</span></span>

<span data-ttu-id="b55f0-134">Para más información sobre las tareas complejas de Azure Table Storage, consulte:</span><span class="sxs-lookup"><span data-stu-id="b55f0-134">To learn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="b55f0-135">Introducción a Table API de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b55f0-135">Introduction to Azure Cosmos DB: Table API</span></span>](table-introduction.md)
* <span data-ttu-id="b55f0-136">Consulte la documentación de referencia de Table service para detalles completo sobre las API disponibles en [Referencia de la biblioteca de clientes de almacenamiento para .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="b55f0-136">The Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="b55f0-137">Acerca de este tutorial</span><span class="sxs-lookup"><span data-stu-id="b55f0-137">About this tutorial</span></span>
<span data-ttu-id="b55f0-138">Este tutorial está dirigido a desarrolladores que conocen el SDK de Azure Table Storage y que quieran usar las características premium disponibles con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b55f0-138">This tutorial is for developers who are familiar with the Azure Table storage SDK, and would like to use the premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="b55f0-139">Se basa en [Introducción a Azure Table Storage mediante .NET](table-storage-how-to-use-dotnet.md) y muestra cómo aprovechar funcionalidades adicionales, como índices secundarios, rendimiento aprovisionado y hospedaje múltiple.</span><span class="sxs-lookup"><span data-stu-id="b55f0-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how to take advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="b55f0-140">Se explica cómo usar Azure Portal para crear una cuenta de Azure Cosmos DB y, luego, compilar e implementar una aplicación de Table.</span><span class="sxs-lookup"><span data-stu-id="b55f0-140">We cover how to use the Azure portal to create an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="b55f0-141">También analizaremos ejemplos de .NET para crear y eliminar una tabla, además de insertar, actualizar, eliminar y consultar datos de tabla.</span><span class="sxs-lookup"><span data-stu-id="b55f0-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="b55f0-142">Si todavía no tiene instalado Visual Studio 2017, puede descargar y usar la versión **gratis** de [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b55f0-142">If you don't already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="b55f0-143">Asegúrese de que habilita **Desarrollo de Azure** durante la instalación de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b55f0-143">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="b55f0-144">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="b55f0-144">Create a database account</span></span>

<span data-ttu-id="b55f0-145">Para comenzar, creemos una cuenta de Azure Cosmos DB en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b55f0-145">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="b55f0-146">¿Ya tiene una cuenta de Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="b55f0-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="b55f0-147">Si es así, vaya a [Configuración de la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="b55f0-147">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="b55f0-148">¿Ya tenía una cuenta de Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="b55f0-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="b55f0-149">Si es así, ahora es una cuenta de Azure Cosmos DB, por lo que puede ir directamente a [Configuración de la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="b55f0-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="b55f0-150">Si usa el Emulador de Azure Cosmos DB, siga los pasos que se indican en [Emulador de Azure Cosmos DB](local-emulator.md) para configurar el emulador y vaya directamente a [Configuración de la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="b55f0-150">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting to any location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-the-sample-application"></a><span data-ttu-id="b55f0-151">Clonación de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b55f0-151">Clone the sample application</span></span>

<span data-ttu-id="b55f0-152">Ahora vamos a clonar una aplicación de Table desde GitHub, establecer la cadena de conexión y ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="b55f0-152">Now let's clone a Table app from github, set the connection string, and run it.</span></span>

1. <span data-ttu-id="b55f0-153">Abra una ventana de terminal de Git, como Git Bash, y `cd` en un directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b55f0-153">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="b55f0-154">Ejecute el comando siguiente para clonar el repositorio de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b55f0-154">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="b55f0-155">Después, abra el archivo de solución en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b55f0-155">Then open the solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="b55f0-156">Actualización de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="b55f0-156">Update your connection string</span></span>

<span data-ttu-id="b55f0-157">Ahora vuelva a Azure Portal para obtener la información de la cadena de conexión y cópiela en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b55f0-157">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="b55f0-158">En [Azure Portal](http://portal.azure.com/), en la cuenta de Azure Cosmos DB, en el panel de navegación izquierdo, haga clic en **Claves** y en **Claves de lectura y escritura**.</span><span class="sxs-lookup"><span data-stu-id="b55f0-158">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="b55f0-159">Deberá usar los botones de copia que se encuentran al lado derecho de la pantalla para copiar la cadena de conexión en el archivo app.config en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="b55f0-159">You'll use the copy buttons on the right side of the screen to copy the connection string into the app.config file in the next step.</span></span>

2. <span data-ttu-id="b55f0-160">En Visual Studio, abra el archivo app.config.</span><span class="sxs-lookup"><span data-stu-id="b55f0-160">In Visual Studio, open the app.config file.</span></span> 

3. <span data-ttu-id="b55f0-161">Copie el valor del URI del portal (con el botón de copia) y conviértalo en el valor de la clave de la cuenta en app.config. Use el nombre de la cuenta que se creó anteriormente en nombre de cuenta de app.config.</span><span class="sxs-lookup"><span data-stu-id="b55f0-161">Copy your URI value from the portal (using the copy button) and make it the value of the account-key in app.config. Use the account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="b55f0-162">Para usar esta aplicación con Azure Table Storage estándar, debe cambiar la cadena de conexión en `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="b55f0-162">To use this app with standard Azure Table Storage, you need to change the connection string in `app.config file`.</span></span> <span data-ttu-id="b55f0-163">Use el nombre de contraseña como el nombre de la cuenta de tabla y la clave como la clave principal de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b55f0-163">Use the account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-the-app"></a><span data-ttu-id="b55f0-164">Compilación e implementación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="b55f0-164">Build and deploy the app</span></span>
1. <span data-ttu-id="b55f0-165">En Visual Studio, haga clic con el botón derecho en el proyecto en el **Explorador de soluciones** y, después, haga clic en **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b55f0-165">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="b55f0-166">En el cuadro **Examinar** de NuGet, escriba ***WindowsAzure.Storage-PremiumTable***.</span><span class="sxs-lookup"><span data-stu-id="b55f0-166">In the NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="b55f0-167">Active **Incluir versiones preliminares**.</span><span class="sxs-lookup"><span data-stu-id="b55f0-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="b55f0-168">Desde los resultados, instale **WindowsAzure.Storage-PremiumTable** y elija la versión preliminar `0.0.1-preview`.</span><span class="sxs-lookup"><span data-stu-id="b55f0-168">From the results, install the **WindowsAzure.Storage-PremiumTable** and choose the preview build `0.0.1-preview`.</span></span> <span data-ttu-id="b55f0-169">Con esta acción se instala el paquete de Azure Table Storage y todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="b55f0-169">This action installs the Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="b55f0-170">Haga clic en CTRL + F5 para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b55f0-170">Click CTRL + F5 to run the application.</span></span> 

<span data-ttu-id="b55f0-171">Ahora puede volver al Explorador de datos y ver, consultar, modificar y trabajar con estos datos de tabla.</span><span class="sxs-lookup"><span data-stu-id="b55f0-171">You can now go back to Data Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="b55f0-172">Para usar esta aplicación con un emulador de Azure Cosmos DB, solo debe cambiar la cadena de conexión en `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="b55f0-172">To use this app with an Azure Cosmos DB Emulator, you just need to change the connection string in `app.config file`.</span></span> <span data-ttu-id="b55f0-173">Use el valor siguiente para el emulador.</span><span class="sxs-lookup"><span data-stu-id="b55f0-173">Use the below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="b55f0-174">Funcionalidades de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b55f0-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="b55f0-175">Azure Cosmos DB admite una serie de funcionalidades que no están disponibles en la API de Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="b55f0-175">Azure Cosmos DB supports a number of capabilities that are not available in the Azure Table storage API.</span></span> <span data-ttu-id="b55f0-176">La funcionalidad nueva se puede habilitar a través de los siguientes valores de configuración de `appSettings`.</span><span class="sxs-lookup"><span data-stu-id="b55f0-176">The new functionality can be enabled via the following `appSettings` configuration values.</span></span> <span data-ttu-id="b55f0-177">No incluimos ninguna firma o sobrecarga nueva en el SDK de Azure Storage para la versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="b55f0-177">We did not introduce any new signatures or overloads to the preview Azure Storage SDK.</span></span> <span data-ttu-id="b55f0-178">Esto le permite conectarse con tablas estándar y premium, además de trabajar con otros servicios de Azure Storage, como Blobs y Queues.</span><span class="sxs-lookup"><span data-stu-id="b55f0-178">This allows you to connect to both standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="b55f0-179">Clave</span><span class="sxs-lookup"><span data-stu-id="b55f0-179">Key</span></span> | <span data-ttu-id="b55f0-180">Descripción</span><span class="sxs-lookup"><span data-stu-id="b55f0-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b55f0-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="b55f0-181">TableConnectionMode</span></span>  | <span data-ttu-id="b55f0-182">Azure Cosmos DB admite dos modos de conectividad.</span><span class="sxs-lookup"><span data-stu-id="b55f0-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="b55f0-183">En el modo `Gateway`, las solicitudes siempre se hacen a la puerta de enlace de Azure Cosmos DB, que las reenvía a las particiones de datos correspondientes.</span><span class="sxs-lookup"><span data-stu-id="b55f0-183">In `Gateway` mode, requests are always made to the Azure Cosmos DB gateway, which forwards it to the corresponding data partitions.</span></span> <span data-ttu-id="b55f0-184">En el modo de conectividad `Direct`, el cliente recupera la asignación de tablas a particiones y las solicitudes se hacen directamente en las particiones de datos.</span><span class="sxs-lookup"><span data-stu-id="b55f0-184">In `Direct` connectivity mode, the client fetches the mapping of tables to partitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="b55f0-185">Se recomienda el valor predeterminado, `Direct`.</span><span class="sxs-lookup"><span data-stu-id="b55f0-185">We recommend `Direct`, the default.</span></span>  |
| <span data-ttu-id="b55f0-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="b55f0-186">TableConnectionProtocol</span></span> | <span data-ttu-id="b55f0-187">Azure Cosmos DB admite dos protocolos de conexión: `Https` y `Tcp`.</span><span class="sxs-lookup"><span data-stu-id="b55f0-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="b55f0-188">El valor predeterminado es`Tcp` que es, además, el valor recomendado porque es más ligero.</span><span class="sxs-lookup"><span data-stu-id="b55f0-188">`Tcp` is the default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="b55f0-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="b55f0-189">TablePreferredLocations</span></span> | <span data-ttu-id="b55f0-190">Lista separada por comas de las ubicaciones preferidas (hospedaje múltiple) para las lecturas.</span><span class="sxs-lookup"><span data-stu-id="b55f0-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="b55f0-191">Cada cuenta de Azure Cosmos DB se puede asociar con entre 1 y 30 regiones más.</span><span class="sxs-lookup"><span data-stu-id="b55f0-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="b55f0-192">Cada instancia de cliente puede especificar un subconjunto de estas regiones en el orden de preferencia para las lecturas de latencia baja.</span><span class="sxs-lookup"><span data-stu-id="b55f0-192">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="b55f0-193">Estas regiones se deben denominar según sus [nombres para mostrar](https://msdn.microsoft.com/library/azure/gg441293.aspx), por ejemplo, `West US`.</span><span class="sxs-lookup"><span data-stu-id="b55f0-193">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="b55f0-194">Consulte también las [API de hospedaje múltiple](tutorial-global-distribution-table.md).</span><span class="sxs-lookup"><span data-stu-id="b55f0-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="b55f0-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="b55f0-195">TableConsistencyLevel</span></span> | <span data-ttu-id="b55f0-196">Puede compensar entre la latencia, la coherencia y la disponibilidad si elige entre cinco niveles de coherencia bien definidos: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix` y `Eventual`.</span><span class="sxs-lookup"><span data-stu-id="b55f0-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="b55f0-197">El valor predeterminado es `Session`.</span><span class="sxs-lookup"><span data-stu-id="b55f0-197">Default is `Session`.</span></span> <span data-ttu-id="b55f0-198">La elección del nivel de coherencia marca una diferencia importante en el rendimiento en las configuraciones con varias regiones.</span><span class="sxs-lookup"><span data-stu-id="b55f0-198">The choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="b55f0-199">Consulte [Niveles de coherencia](consistency-levels.md) para obtener detalles.</span><span class="sxs-lookup"><span data-stu-id="b55f0-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="b55f0-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="b55f0-200">TableThroughput</span></span> | <span data-ttu-id="b55f0-201">Rendimiento reservado para la tabla expresado en unidades de solicitud (RU) por segundo.</span><span class="sxs-lookup"><span data-stu-id="b55f0-201">Reserved throughput for the table expressed in request units (RU) per second.</span></span> <span data-ttu-id="b55f0-202">Las tablas únicas puede admitir cientos de millones de RU/s.</span><span class="sxs-lookup"><span data-stu-id="b55f0-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="b55f0-203">Consulte [Unidades de solicitud](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="b55f0-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="b55f0-204">El valor predeterminado es `400`</span><span class="sxs-lookup"><span data-stu-id="b55f0-204">Default is `400`</span></span> |
| <span data-ttu-id="b55f0-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="b55f0-205">TableIndexingPolicy</span></span> | <span data-ttu-id="b55f0-206">Indexado secundario coherente y automático de todas las columnas dentro de las tablas</span><span class="sxs-lookup"><span data-stu-id="b55f0-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="b55f0-207">Cadena JSON en conformidad con la especificación de la directiva de indexación.</span><span class="sxs-lookup"><span data-stu-id="b55f0-207">JSON string conforming to the indexing policy specification.</span></span> <span data-ttu-id="b55f0-208">Consulte [Directiva de indexación](indexing-policies.md) para ver cómo puede cambiar la directiva de indexación para incluir o excluir columnas específicas.</span><span class="sxs-lookup"><span data-stu-id="b55f0-208">See [Indexing Policy](indexing-policies.md) to see how you can change indexing policy to include/exclude specific columns.</span></span> | <span data-ttu-id="b55f0-209">Indexado automático de todas las propiedades (hash para cadenas e intervalo para números)</span><span class="sxs-lookup"><span data-stu-id="b55f0-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="b55f0-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="b55f0-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="b55f0-211">Configure el número máximo de elementos devueltos por consulta de tabla en un solo recorrido de ida y vuelta.</span><span class="sxs-lookup"><span data-stu-id="b55f0-211">Configure the maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="b55f0-212">El valor predeterminado es `-1`, que permite que Azure Cosmos DB determine el valor en runtime de manera dinámica.</span><span class="sxs-lookup"><span data-stu-id="b55f0-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |
| <span data-ttu-id="b55f0-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="b55f0-213">TableQueryEnableScan</span></span> | <span data-ttu-id="b55f0-214">Si la consulta no puede usar el índice para algún filtro, ejecútela de todas maneras a través de un examen.</span><span class="sxs-lookup"><span data-stu-id="b55f0-214">If the query cannot use the index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="b55f0-215">El valor predeterminado es `false`.</span><span class="sxs-lookup"><span data-stu-id="b55f0-215">Default is `false`.</span></span>|
| <span data-ttu-id="b55f0-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="b55f0-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="b55f0-217">El grado de paralelismo para la ejecución de una consulta entre particiones.</span><span class="sxs-lookup"><span data-stu-id="b55f0-217">The degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="b55f0-218">`0` es un valor en serie sin captura previa, `1` es un valor en serie con captura previa y los valores más altos aumentan el índice de paralelismo.</span><span class="sxs-lookup"><span data-stu-id="b55f0-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase the rate of parallelism.</span></span> <span data-ttu-id="b55f0-219">El valor predeterminado es `-1`, que permite que Azure Cosmos DB determine el valor en runtime de manera dinámica.</span><span class="sxs-lookup"><span data-stu-id="b55f0-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |

<span data-ttu-id="b55f0-220">Para cambiar el valor predeterminado, abra el archivo `app.config` del Explorador de soluciones en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b55f0-220">To change the default value, open the `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="b55f0-221">Agregue el contenido del elemento `<appSettings>` , que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="b55f0-221">Add the contents of the `<appSettings>` element shown below.</span></span> <span data-ttu-id="b55f0-222">Reemplace `account-name` por el nombre de su cuenta de almacenamiento, y `account-key` por la clave de acceso de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="b55f0-222">Replace `account-name` with the name of your storage account, and `account-key` with your account access key.</span></span> 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

<span data-ttu-id="b55f0-223">Vamos a revisar rápidamente lo que sucede en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b55f0-223">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="b55f0-224">Abra el archivo `Program.cs` y observe que estas líneas de código crean los recursos de Table.</span><span class="sxs-lookup"><span data-stu-id="b55f0-224">Open the `Program.cs` file and you find that these lines of code create the Table resources.</span></span> 

## <a name="create-the-table-client"></a><span data-ttu-id="b55f0-225">Creación del cliente de Table</span><span class="sxs-lookup"><span data-stu-id="b55f0-225">Create the table client</span></span>
<span data-ttu-id="b55f0-226">Inicializa un elemento `CloudTableClient` para conectarse a la cuenta de Table.</span><span class="sxs-lookup"><span data-stu-id="b55f0-226">You initialize a `CloudTableClient` to connect to the table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="b55f0-227">El cliente se inicializa a través de los valores de configuración `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel` y `TablePreferredLocations` si se especifican en la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b55f0-227">This client is initialized using the `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in the app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="b55f0-228">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="b55f0-228">Create a table</span></span>
<span data-ttu-id="b55f0-229">Luego, se crea una tabla con `CloudTable`.</span><span class="sxs-lookup"><span data-stu-id="b55f0-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="b55f0-230">Las tablas en Azure Cosmos DB pueden escalar de manera independiente en términos de almacenamiento y rendimiento, y el servicio controla automáticamente la creación de particiones.</span><span class="sxs-lookup"><span data-stu-id="b55f0-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by the service.</span></span> <span data-ttu-id="b55f0-231">Azure Cosmos DB admite tanto tablas ilimitadas como de tamaño fijo.</span><span class="sxs-lookup"><span data-stu-id="b55f0-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="b55f0-232">Consulte [Creación de particiones en Azure Cosmos DB](partition-data.md) para obtener detalles.</span><span class="sxs-lookup"><span data-stu-id="b55f0-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="b55f0-233">Existe una diferencia importante en la manera de crear las tablas.</span><span class="sxs-lookup"><span data-stu-id="b55f0-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="b55f0-234">Azure Cosmos DB reserva rendimiento, a diferencia del modelo basado en consumo de Azure Storage para las transacciones.</span><span class="sxs-lookup"><span data-stu-id="b55f0-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="b55f0-235">El modelo de reserva tiene dos ventajas principales:</span><span class="sxs-lookup"><span data-stu-id="b55f0-235">The reservation model has two key benefits:</span></span>

* <span data-ttu-id="b55f0-236">El rendimiento es dedicado/reservado, por lo que nunca se verá limitado si la velocidad de solicitudes se encuentra en el rendimiento aprovisionado o está por debajo de este</span><span class="sxs-lookup"><span data-stu-id="b55f0-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="b55f0-237">El modelo de reserva es más [rentable para las cargas de trabajo de alto uso de rendimiento](key-value-store-cost.md)</span><span class="sxs-lookup"><span data-stu-id="b55f0-237">The reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="b55f0-238">Puede configurar el rendimiento predeterminado si configura los ajustes para `TableThroughput` en términos de RU (unidades de solicitud) por segundo.</span><span class="sxs-lookup"><span data-stu-id="b55f0-238">You can configure the default throughput by configuring the setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="b55f0-239">Una lectura de una entidad de 1 KB se normaliza como 1 RU y otras operaciones se normalizan como un valor de RU fijo basado en el consumo de CPU, memoria e IOPS.</span><span class="sxs-lookup"><span data-stu-id="b55f0-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized to a fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="b55f0-240">Más información sobre [Unidades de solicitud en Azure Cosmos DB](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="b55f0-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b55f0-241">Si bien el SDK de Table Storage no admite actualmente la modificación del rendimiento, este se puede cambiar inmediatamente en cualquier momento con Azure Portal o la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="b55f0-241">While Table storage SDK does not currently support modifying throughput, you can change the throughput instantaneously at any time using the Azure portal or Azure CLI.</span></span>

<span data-ttu-id="b55f0-242">A continuación, analizaremos las operaciones simples de lectura y escritura (CRUD) mediante el SDK de Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="b55f0-242">Next, we walk through the simple read and write (CRUD) operations using the Azure Table storage SDK.</span></span> <span data-ttu-id="b55f0-243">En este tutorial se muestran las consultas rápidas y las latencias bajas predecibles de milisegundos de un solo dígito que proporciona Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b55f0-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="b55f0-244">Adición de una entidad a una tabla</span><span class="sxs-lookup"><span data-stu-id="b55f0-244">Add an entity to a table</span></span>
<span data-ttu-id="b55f0-245">Las entidades de Azure Table Storage se extienden desde la clase `TableEntity` y deben tener las propiedades `PartitionKey` y `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="b55f0-245">Entities in Azure Table storage extend from the `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="b55f0-246">La siguiente es una definición de ejemplo de una entidad de cliente.</span><span class="sxs-lookup"><span data-stu-id="b55f0-246">Here's a sample definition for a customer entity.</span></span>

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

<span data-ttu-id="b55f0-247">El fragmento de código siguiente muestra cómo insertar una entidad con el SDK de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b55f0-247">The following snippet shows how to insert an entity with the Azure storage SDK.</span></span> <span data-ttu-id="b55f0-248">Azure Cosmos DB está diseñado para garantizar una latencia baja a cualquier escala, en todo el mundo.</span><span class="sxs-lookup"><span data-stu-id="b55f0-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across the world.</span></span>

<span data-ttu-id="b55f0-249">Las escrituras completan <15 ms en p99 y ~6 ms en p50 en el caso de las aplicaciones que se ejecutan en la misma región que la cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b55f0-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in the same region as the Azure Cosmos DB account.</span></span> <span data-ttu-id="b55f0-250">Además, esta duración explica el hecho de que las escrituras se reconocen en el cliente solo una vez que se replican de forma sincrónica, se confirman de forma duradera y se indexa todo el contenido.</span><span class="sxs-lookup"><span data-stu-id="b55f0-250">And this duration accounts for the fact that writes are acknowledged back to the client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="b55f0-251">Table API para Azure Cosmos DB está en su versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="b55f0-251">The Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="b55f0-252">Cuando esté disponible a nivel general, las garantías de la latencia de p99 están respaldadas por los Acuerdos de Nivel de Servicio del mismo modo que las otras API de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b55f0-252">At general availability, the p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute the insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="b55f0-253">Inserción de un lote de entidades</span><span class="sxs-lookup"><span data-stu-id="b55f0-253">Insert a batch of entities</span></span>
<span data-ttu-id="b55f0-254">Azure Table Storage admite una API de operación por lotes que le permite combinar actualizaciones, eliminaciones e inserciones en la misma operación por lotes.</span><span class="sxs-lookup"><span data-stu-id="b55f0-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in the same single batch operation.</span></span> <span data-ttu-id="b55f0-255">Azure Cosmos DB no tiene en la API de lote algunas de las limitaciones que tiene Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="b55f0-255">Azure Cosmos DB does not have some of the limitations on the batch API as Azure Table storage.</span></span> <span data-ttu-id="b55f0-256">Por ejemplo, puede realizar varias lecturas dentro de un lote, realizar varias escrituras en la misma entidad dentro de un lote y no existe el límite de 100 operaciones por lote.</span><span class="sxs-lookup"><span data-stu-id="b55f0-256">For example, you can perform multiple reads within a batch, you can perform multiple writes to the same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

```csharp
// Create the batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it to the table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it to the table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities to the batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute the batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="b55f0-257">una sola entidad</span><span class="sxs-lookup"><span data-stu-id="b55f0-257">Retrieve a single entity</span></span>
<span data-ttu-id="b55f0-258">Las recuperaciones (operaciones GET) en Azure Cosmos DB completan <10 ms en p99 y ~1 ms en p50 en la misma región de Azure.</span><span class="sxs-lookup"><span data-stu-id="b55f0-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in the same Azure region.</span></span> <span data-ttu-id="b55f0-259">Puede agregar todas las regiones necesarias en la cuenta para las lecturas de latencia baja e implementar aplicaciones para leer desde la región local ("con hospedaje múltiple") si establece `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="b55f0-259">You can add as many regions to your account for low latency reads, and deploy applications to read from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="b55f0-260">Puede recuperar una sola entidad mediante el siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="b55f0-260">You can retrieve a single entity using the following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="b55f0-261">Obtenga información sobre las API de hospedaje múltiple en [Desarrollo con varias regiones](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="b55f0-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="b55f0-262">Consulta de entidades con índices secundarios automáticos</span><span class="sxs-lookup"><span data-stu-id="b55f0-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="b55f0-263">Puede usar la clase `TableQuery` para consultar las tablas.</span><span class="sxs-lookup"><span data-stu-id="b55f0-263">Tables can be queried using the `TableQuery` class.</span></span> <span data-ttu-id="b55f0-264">Azure Cosmos DB tiene un motor de base de datos optimizado para escritura que indexa automáticamente todas las columnas dentro de la tabla.</span><span class="sxs-lookup"><span data-stu-id="b55f0-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="b55f0-265">El indexado en Azure Cosmos DB es independiente del esquema.</span><span class="sxs-lookup"><span data-stu-id="b55f0-265">Indexing in Azure Cosmos DB is agnostic to schema.</span></span> <span data-ttu-id="b55f0-266">Por lo tanto, incluso si el esquema es distinto entre las filas o si el esquema evoluciona en el tiempo, se indexará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b55f0-266">Therefore, even if your schema is different between rows, or if the schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="b55f0-267">Como Azure Cosmos DB admite los índices secundarios automáticos, las consultas en cualquier propiedad pueden usar el índice y se atenderán de forma eficaz.</span><span class="sxs-lookup"><span data-stu-id="b55f0-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use the index and be served efficiently.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

<span data-ttu-id="b55f0-268">En la versión preliminar, Azure Cosmos DB admite la misma funcionalidad de consulta que Azure Table Storage para Table API.</span><span class="sxs-lookup"><span data-stu-id="b55f0-268">In preview, Azure Cosmos DB supports the same query functionality as Azure Table storage for the Table API.</span></span> <span data-ttu-id="b55f0-269">Azure Cosmos DB también admite ordenación, agregados, consulta geoespacial, jerarquía y una amplia variedad de funciones integradas.</span><span class="sxs-lookup"><span data-stu-id="b55f0-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="b55f0-270">Una futura actualización de servicio de Table API ofrecerá funcionalidades adicionales.</span><span class="sxs-lookup"><span data-stu-id="b55f0-270">The additional functionality will be provided in the Table API in a future service update.</span></span> <span data-ttu-id="b55f0-271">En [Consulta de Azure Cosmos DB](documentdb-sql-query.md) puede encontrar información general sobre esas funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="b55f0-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="b55f0-272">una entidad</span><span class="sxs-lookup"><span data-stu-id="b55f0-272">Replace an entity</span></span>
<span data-ttu-id="b55f0-273">Para actualizar una entidad, recupérela del servicio Tabla, modifique su objeto y, a continuación, guarde los cambios de nuevo en el servicio Tabla.</span><span class="sxs-lookup"><span data-stu-id="b55f0-273">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="b55f0-274">El código siguiente cambia el número de teléfono de un cliente.</span><span class="sxs-lookup"><span data-stu-id="b55f0-274">The following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="b55f0-275">Del mismo modo, puede realizar las operaciones `InsertOrMerge` o `Merge`.</span><span class="sxs-lookup"><span data-stu-id="b55f0-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="b55f0-276">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="b55f0-276">Delete an entity</span></span>
<span data-ttu-id="b55f0-277">Puede eliminar fácilmente una entidad una vez recuperada utilizando el mismo patrón mostrado para actualizar una entidad.</span><span class="sxs-lookup"><span data-stu-id="b55f0-277">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span></span> <span data-ttu-id="b55f0-278">El código siguiente recupera y elimina una entidad de cliente.</span><span class="sxs-lookup"><span data-stu-id="b55f0-278">The following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="b55f0-279">Eliminación de una tabla</span><span class="sxs-lookup"><span data-stu-id="b55f0-279">Delete a table</span></span>
<span data-ttu-id="b55f0-280">Finalmente, el ejemplo de código siguiente elimina una tabla de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b55f0-280">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="b55f0-281">Puede eliminar una tabla y volver a crearla de inmediato con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b55f0-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="b55f0-282">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="b55f0-282">Clean up resources</span></span> 

<span data-ttu-id="b55f0-283">Si no va a seguir usando esta aplicación, use los pasos siguientes para borrar todos los recursos que se crearon en este tutorial en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b55f0-283">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span>   

1. <span data-ttu-id="b55f0-284">En el menú de la izquierda de Azure Portal, haga clic en **Grupos de recursos** y en el nombre del recurso que creó.</span><span class="sxs-lookup"><span data-stu-id="b55f0-284">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span>  
2. <span data-ttu-id="b55f0-285">En la página del grupo de recursos, haga clic en **Eliminar**, escriba en el cuadro de texto el nombre del recurso que quiere eliminar y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="b55f0-285">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b55f0-286">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b55f0-286">Next steps</span></span>

<span data-ttu-id="b55f0-287">En este tutorial, describimos cómo empezar a usar Azure Cosmos DB con Table API y se realizó lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b55f0-287">In this tutorial, we covered how to get started using Azure Cosmos DB with the Table API, and you've done the following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="b55f0-288">Se creó una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b55f0-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="b55f0-289">Se habilitaron funcionalidades en el archivo app.config</span><span class="sxs-lookup"><span data-stu-id="b55f0-289">Enabled functionality in the app.config file</span></span> 
> * <span data-ttu-id="b55f0-290">Se creó una tabla</span><span class="sxs-lookup"><span data-stu-id="b55f0-290">Created a table</span></span> 
> * <span data-ttu-id="b55f0-291">Se agregó una entidad a una tabla</span><span class="sxs-lookup"><span data-stu-id="b55f0-291">Added an entity to a table</span></span> 
> * <span data-ttu-id="b55f0-292">Se insertó un lote de entidades</span><span class="sxs-lookup"><span data-stu-id="b55f0-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="b55f0-293">Se recuperó una sola entidad</span><span class="sxs-lookup"><span data-stu-id="b55f0-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="b55f0-294">Se consultaron las entidades con índices secundarios automáticos</span><span class="sxs-lookup"><span data-stu-id="b55f0-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="b55f0-295">Se reemplazó una entidad</span><span class="sxs-lookup"><span data-stu-id="b55f0-295">Replaced an entity</span></span> 
> * <span data-ttu-id="b55f0-296">Se eliminó una entidad</span><span class="sxs-lookup"><span data-stu-id="b55f0-296">Deleted an entity</span></span> 
> * <span data-ttu-id="b55f0-297">Se eliminó una tabla</span><span class="sxs-lookup"><span data-stu-id="b55f0-297">Deleted a table</span></span>  

<span data-ttu-id="b55f0-298">Ahora puede pasar al siguiente tutorial y obtener más información sobre cómo consultar los datos de tabla.</span><span class="sxs-lookup"><span data-stu-id="b55f0-298">You can now proceed to the next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="b55f0-299">Consulta con Table API</span><span class="sxs-lookup"><span data-stu-id="b55f0-299">Query with the Table API</span></span>](tutorial-query-table.md)
