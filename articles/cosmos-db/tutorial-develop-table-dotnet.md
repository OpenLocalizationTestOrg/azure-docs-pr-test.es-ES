---
title: 'Azure Cosmos DB: Desarrollar con hello API de tabla en .NET | Documentos de Microsoft'
description: "Obtenga información acerca de cómo toodevelop con API de tabla de Azure Cosmos DB con .NET"
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
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a><span data-ttu-id="17455-103">Azure Cosmos DB: Desarrollar con hello API de tabla en .NET</span><span class="sxs-lookup"><span data-stu-id="17455-103">Azure Cosmos DB: Develop with hello Table API in .NET</span></span>

<span data-ttu-id="17455-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="17455-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="17455-105">Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="17455-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span>

<span data-ttu-id="17455-106">Este tutorial trata Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="17455-106">This tutorial covers hello following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="17455-107">Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="17455-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="17455-108">Habilitar la funcionalidad en el archivo app.config de hello</span><span class="sxs-lookup"><span data-stu-id="17455-108">Enable functionality in hello app.config file</span></span> 
> * <span data-ttu-id="17455-109">Crear una tabla mediante hello [API tabla](table-introduction.md) (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="17455-109">Create a table using hello [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="17455-110">Agregar una tabla de tooa de entidad</span><span class="sxs-lookup"><span data-stu-id="17455-110">Add an entity tooa table</span></span> 
> * <span data-ttu-id="17455-111">Inserción de un lote de entidades</span><span class="sxs-lookup"><span data-stu-id="17455-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="17455-112">una sola entidad</span><span class="sxs-lookup"><span data-stu-id="17455-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="17455-113">Consulta de entidades con índices secundarios automáticos</span><span class="sxs-lookup"><span data-stu-id="17455-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="17455-114">una entidad</span><span class="sxs-lookup"><span data-stu-id="17455-114">Replace an entity</span></span> 
> * <span data-ttu-id="17455-115">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="17455-115">Delete an entity</span></span> 
> * <span data-ttu-id="17455-116">Eliminación de una tabla</span><span class="sxs-lookup"><span data-stu-id="17455-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="17455-117">Tablas en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="17455-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="17455-118">Base de datos de Azure Cosmos proporciona hello [API tabla](table-introduction.md) (vista previa) para las aplicaciones que necesitan un almacén de clave y valor con un diseño sin esquema.</span><span class="sxs-lookup"><span data-stu-id="17455-118">Azure Cosmos DB provides hello [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="17455-119">[El almacenamiento de tabla](../storage/common/storage-introduction.md) SDK y las API de REST pueden ser toowork utilizado con la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="17455-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used toowork with Azure Cosmos DB.</span></span> <span data-ttu-id="17455-120">Puede usar tablas de base de datos de Azure Cosmos toocreate con requisitos de alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="17455-120">You can use Azure Cosmos DB toocreate tables with high throughput requirements.</span></span> <span data-ttu-id="17455-121">Azure Cosmos DB admite tablas optimizadas para el rendimiento (llamadas informalmente "tablas premium"), actualmente en versión preliminar pública.</span><span class="sxs-lookup"><span data-stu-id="17455-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="17455-122">Puede continuar toouse almacenamiento de tabla de Azure para las tablas con almacenamiento alta y requisitos de rendimiento inferior.</span><span class="sxs-lookup"><span data-stu-id="17455-122">You can continue toouse Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="17455-123">Azure DB Cosmos incorporará la compatibilidad con tablas con optimización para el almacenamiento en una futura actualización y se actualiza la tabla de Azure nuevas y existentes serán las cuentas de almacenamiento sin problemas tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="17455-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded tooAzure Cosmos DB.</span></span>

<span data-ttu-id="17455-124">Si actualmente usa almacenamiento de tabla de Azure, obtendrá Hola siguientes ventajas con hello "premium" vista previa:</span><span class="sxs-lookup"><span data-stu-id="17455-124">If you currently use Azure Table storage, you gain hello following benefits with hello "premium table" preview:</span></span>

- <span data-ttu-id="17455-125">[Distribución global](distribute-data-globally.md) llave en mano con hospedaje múltiple y [conmutaciones por error manuales y automáticas](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="17455-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="17455-126">Compatibilidad con el indexado automático independiente del esquema con respecto a todas las propiedades ("índices secundarios") y consultas rápidas</span><span class="sxs-lookup"><span data-stu-id="17455-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="17455-127">Compatibilidad con el [escalado independiente de proceso y almacenamiento](partition-data.md), en cualquier número de regiones</span><span class="sxs-lookup"><span data-stu-id="17455-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="17455-128">Compatibilidad con [rendimiento dedicado por tabla](request-units.md) que se puede escalar de las centenas toomillions de solicitudes por segundo</span><span class="sxs-lookup"><span data-stu-id="17455-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds toomillions of requests per second</span></span>
- <span data-ttu-id="17455-129">Compatibilidad con [cinco niveles de coherencia optimizarse](consistency-levels.md) tootrade disponibilidad, latencia y coherencia según sus necesidades de aplicación</span><span class="sxs-lookup"><span data-stu-id="17455-129">Support for [five tunable consistency levels](consistency-levels.md) tootrade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="17455-130">disponibilidad del 99,99% dentro de una única región y capacidad tooadd más regiones para una mayor disponibilidad y [líderes en la industria completa SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db/) en disponibilidad general</span><span class="sxs-lookup"><span data-stu-id="17455-130">99.99% availability within a single region, and ability tooadd more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="17455-131">Trabajar con almacenamiento de Azure existente .NET SDK de Hola y no haya ninguna aplicación de tooyour de cambios de código</span><span class="sxs-lookup"><span data-stu-id="17455-131">Work with hello existing Azure storage .NET SDK, and no code changes tooyour application</span></span>

<span data-ttu-id="17455-132">Durante la vista previa de hello, admite la base de datos de Azure Cosmos Hola mediante Hola .NET SDK de API de tabla.</span><span class="sxs-lookup"><span data-stu-id="17455-132">During hello preview, Azure Cosmos DB supports hello Table API using hello .NET SDK.</span></span> <span data-ttu-id="17455-133">Puede descargar hello [SDK de vista previa del almacenamiento de Azure](https://aka.ms/premiumtablenuget) de NuGet, que tiene Hola mismas clases y las firmas de método como hello [SDK de almacenamiento de Azure](https://www.nuget.org/packages/WindowsAzure.Storage), pero también puede conectarse tooAzure Cosmos DB cuentas con hello API de la tabla.</span><span class="sxs-lookup"><span data-stu-id="17455-133">You can download hello [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has hello same classes and method signatures as hello [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect tooAzure Cosmos DB accounts using hello Table API.</span></span>

<span data-ttu-id="17455-134">toolearn más información acerca de tareas complejas de almacenamiento de tabla de Azure, vea:</span><span class="sxs-lookup"><span data-stu-id="17455-134">toolearn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="17455-135">Introducción tooAzure DB Cosmos: API de tabla</span><span class="sxs-lookup"><span data-stu-id="17455-135">Introduction tooAzure Cosmos DB: Table API</span></span>](table-introduction.md)
* <span data-ttu-id="17455-136">Hola documentación de referencia de servicio de tabla para obtener información detallada acerca de las API disponibles [biblioteca de cliente de almacenamiento para la referencia de .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="17455-136">hello Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="17455-137">Acerca de este tutorial</span><span class="sxs-lookup"><span data-stu-id="17455-137">About this tutorial</span></span>
<span data-ttu-id="17455-138">Este tutorial está usando para los desarrolladores que están familiarizados con hello almacenamiento de tabla de Azure SDK y desearía disponibles las características toouse Hola premium de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="17455-138">This tutorial is for developers who are familiar with hello Azure Table storage SDK, and would like toouse hello premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="17455-139">Se basa en [Introducción al almacenamiento de tabla de Azure mediante .NET](table-storage-how-to-use-dotnet.md) y muestra cómo tootake aprovechar capacidades adicionales como los índices secundarios, rendimiento aprovisionado y la conexión.</span><span class="sxs-lookup"><span data-stu-id="17455-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how tootake advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="17455-140">Trataremos cómo toouse Hola toocreate portal Azure una cuenta de base de datos de Azure Cosmos y, a continuación, generar e implementar una aplicación de la tabla.</span><span class="sxs-lookup"><span data-stu-id="17455-140">We cover how toouse hello Azure portal toocreate an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="17455-141">También analizaremos ejemplos de .NET para crear y eliminar una tabla, además de insertar, actualizar, eliminar y consultar datos de tabla.</span><span class="sxs-lookup"><span data-stu-id="17455-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="17455-142">Si aún no tiene Visual Studio de 2017 instalado, puede descargar y usar hello **libre** [2017 Community Edition de Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="17455-142">If you don't already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="17455-143">Asegúrese de que habilitar **desarrollo Azure** durante la instalación de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="17455-143">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="17455-144">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="17455-144">Create a database account</span></span>

<span data-ttu-id="17455-145">Empecemos creando una cuenta de base de datos de Azure Cosmos Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="17455-145">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="17455-146">¿Ya tiene una cuenta de Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="17455-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="17455-147">Si es así, pasar demasiado[configure su solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="17455-147">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="17455-148">¿Ya tenía una cuenta de Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="17455-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="17455-149">En caso afirmativo, la cuenta es ahora una cuenta de base de datos de Azure Cosmos y puede saltarse lecciones demasiado[configure su solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="17455-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="17455-150">Si usas hello Azure Cosmos DB emulador, siga los pasos de hello en [emulador de base de datos de Azure Cosmos](local-emulator.md) toosetup Hola emulador y pase demasiado[configurar la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="17455-150">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a><span data-ttu-id="17455-151">Clonar aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="17455-151">Clone hello sample application</span></span>

<span data-ttu-id="17455-152">Ahora vamos a clonar una aplicación de la tabla de github, establezca la cadena de conexión de Hola y ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="17455-152">Now let's clone a Table app from github, set hello connection string, and run it.</span></span>

1. <span data-ttu-id="17455-153">Abra una ventana de terminal de git, como git bash, y `cd` tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="17455-153">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="17455-154">Ejecute hello después de repositorio de ejemplo de comando tooclone Hola.</span><span class="sxs-lookup"><span data-stu-id="17455-154">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="17455-155">A continuación, abra el archivo de solución de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17455-155">Then open hello solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="17455-156">Actualizar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="17455-156">Update your connection string</span></span>

<span data-ttu-id="17455-157">Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="17455-157">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="17455-158">Hola [portal de Azure](http://portal.azure.com/), en la base de datos de Azure Cosmos account, Hola barra de navegación izquierda, haga clic en **claves**y, a continuación, haga clic en **claves de lectura y escritura**.</span><span class="sxs-lookup"><span data-stu-id="17455-158">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="17455-159">Deberá usar botones de copia de hello en hello derecha de la cadena de conexión de hello pantalla toocopy Hola en el archivo app.config de hello en el paso siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="17455-159">You'll use hello copy buttons on hello right side of hello screen toocopy hello connection string into hello app.config file in hello next step.</span></span>

2. <span data-ttu-id="17455-160">En Visual Studio, abra el archivo app.config de hello.</span><span class="sxs-lookup"><span data-stu-id="17455-160">In Visual Studio, open hello app.config file.</span></span> 

3. <span data-ttu-id="17455-161">Copie el valor URI de portal hello (mediante el botón Copiar de Hola) y hacerla Hola valor de clave de cuenta de hello en el archivo app.config. Utilice el nombre de cuenta de hello creado anteriormente para el nombre de cuenta en el archivo app.config.</span><span class="sxs-lookup"><span data-stu-id="17455-161">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello account-key in app.config. Use hello account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="17455-162">toouse esta aplicación con almacenamiento de tabla de Azure estándar, se necesita la cadena de conexión de Hola de toochange en `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="17455-162">toouse this app with standard Azure Table Storage, you need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="17455-163">Utilice el nombre de cuenta de hello como nombre de la cuenta de la tabla y la clave como clave principal de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="17455-163">Use hello account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a><span data-ttu-id="17455-164">Compilar e implementar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="17455-164">Build and deploy hello app</span></span>
1. <span data-ttu-id="17455-165">En Visual Studio, haga doble clic en el proyecto de hello en **el Explorador de soluciones** y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="17455-165">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="17455-166">Hola NuGet **examinar** , escriba ***WindowsAzure.Storage PremiumTable***.</span><span class="sxs-lookup"><span data-stu-id="17455-166">In hello NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="17455-167">Active **Incluir versiones preliminares**.</span><span class="sxs-lookup"><span data-stu-id="17455-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="17455-168">Desde los resultados de hello, instalar hello **WindowsAzure.Storage PremiumTable** y elija la versión preliminar de hello `0.0.1-preview`.</span><span class="sxs-lookup"><span data-stu-id="17455-168">From hello results, install hello **WindowsAzure.Storage-PremiumTable** and choose hello preview build `0.0.1-preview`.</span></span> <span data-ttu-id="17455-169">Esta acción instala el paquete de almacenamiento de tabla de Azure de Hola y todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="17455-169">This action installs hello Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="17455-170">Haga clic en CTRL + F5 aplicación hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="17455-170">Click CTRL + F5 toorun hello application.</span></span> 

<span data-ttu-id="17455-171">Ahora puede volver atrás tooData explorador y vea la consulta, modificar y trabajar con estos datos de tabla.</span><span class="sxs-lookup"><span data-stu-id="17455-171">You can now go back tooData Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="17455-172">toouse esta aplicación con un emulador de base de datos de Cosmos de Azure, que necesita toochange cadena de conexión de hello en `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="17455-172">toouse this app with an Azure Cosmos DB Emulator, you just need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="17455-173">Usar hello por debajo del valor para el emulador.</span><span class="sxs-lookup"><span data-stu-id="17455-173">Use hello below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="17455-174">Funcionalidades de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="17455-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="17455-175">Base de datos de Azure Cosmos admite una serie de funcionalidades que no están disponibles en hello API de almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="17455-175">Azure Cosmos DB supports a number of capabilities that are not available in hello Azure Table storage API.</span></span> <span data-ttu-id="17455-176">Hello nueva funcionalidad puede habilitarse a través siguiente hello `appSettings` valores de configuración.</span><span class="sxs-lookup"><span data-stu-id="17455-176">hello new functionality can be enabled via hello following `appSettings` configuration values.</span></span> <span data-ttu-id="17455-177">No se ha introducido cualquier nueva firmas o sobrecargas toohello vista previa del SDK de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="17455-177">We did not introduce any new signatures or overloads toohello preview Azure Storage SDK.</span></span> <span data-ttu-id="17455-178">Esto le permite tooconnect tooboth standard y premium tablas y trabajar con otros servicios de almacenamiento de Azure como Blobs y colas.</span><span class="sxs-lookup"><span data-stu-id="17455-178">This allows you tooconnect tooboth standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="17455-179">Clave</span><span class="sxs-lookup"><span data-stu-id="17455-179">Key</span></span> | <span data-ttu-id="17455-180">Descripción</span><span class="sxs-lookup"><span data-stu-id="17455-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="17455-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="17455-181">TableConnectionMode</span></span>  | <span data-ttu-id="17455-182">Azure Cosmos DB admite dos modos de conectividad.</span><span class="sxs-lookup"><span data-stu-id="17455-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="17455-183">En `Gateway` modo, las solicitudes se realizan siempre toohello base de datos de Azure Cosmos puerta de enlace, que lo reenvía toohello particiones de datos correspondiente.</span><span class="sxs-lookup"><span data-stu-id="17455-183">In `Gateway` mode, requests are always made toohello Azure Cosmos DB gateway, which forwards it toohello corresponding data partitions.</span></span> <span data-ttu-id="17455-184">En `Direct` modo de conectividad, cliente hello captura asignación Hola de toopartitions de tablas y las solicitudes se realizan directamente en particiones de datos.</span><span class="sxs-lookup"><span data-stu-id="17455-184">In `Direct` connectivity mode, hello client fetches hello mapping of tables toopartitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="17455-185">Se recomienda `Direct`, Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="17455-185">We recommend `Direct`, hello default.</span></span>  |
| <span data-ttu-id="17455-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="17455-186">TableConnectionProtocol</span></span> | <span data-ttu-id="17455-187">Azure Cosmos DB admite dos protocolos de conexión: `Https` y `Tcp`.</span><span class="sxs-lookup"><span data-stu-id="17455-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="17455-188">`Tcp`es el valor predeterminado de Hola y recomienda porque es más ligera.</span><span class="sxs-lookup"><span data-stu-id="17455-188">`Tcp` is hello default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="17455-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="17455-189">TablePreferredLocations</span></span> | <span data-ttu-id="17455-190">Lista separada por comas de las ubicaciones preferidas (hospedaje múltiple) para las lecturas.</span><span class="sxs-lookup"><span data-stu-id="17455-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="17455-191">Cada cuenta de Azure Cosmos DB se puede asociar con entre 1 y 30 regiones más.</span><span class="sxs-lookup"><span data-stu-id="17455-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="17455-192">Cada instancia del cliente puede especificar un subconjunto de estas regiones en orden de hello preferido para las lecturas de latencia baja.</span><span class="sxs-lookup"><span data-stu-id="17455-192">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="17455-193">regiones de Hello deben denominarse mediante sus [nombres para mostrar](https://msdn.microsoft.com/library/azure/gg441293.aspx), por ejemplo, `West US`.</span><span class="sxs-lookup"><span data-stu-id="17455-193">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="17455-194">Consulte también las [API de hospedaje múltiple](tutorial-global-distribution-table.md).</span><span class="sxs-lookup"><span data-stu-id="17455-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="17455-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="17455-195">TableConsistencyLevel</span></span> | <span data-ttu-id="17455-196">Puede compensar entre la latencia, la coherencia y la disponibilidad si elige entre cinco niveles de coherencia bien definidos: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix` y `Eventual`.</span><span class="sxs-lookup"><span data-stu-id="17455-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="17455-197">El valor predeterminado es `Session`.</span><span class="sxs-lookup"><span data-stu-id="17455-197">Default is `Session`.</span></span> <span data-ttu-id="17455-198">elección de Hola de nivel de coherencia realiza una diferencia significativa del rendimiento en configuraciones de varias regiones.</span><span class="sxs-lookup"><span data-stu-id="17455-198">hello choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="17455-199">Consulte [Niveles de coherencia](consistency-levels.md) para obtener detalles.</span><span class="sxs-lookup"><span data-stu-id="17455-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="17455-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="17455-200">TableThroughput</span></span> | <span data-ttu-id="17455-201">Rendimiento reservados para la tabla de hello expresado en unidades de solicitud (RU) por segundo.</span><span class="sxs-lookup"><span data-stu-id="17455-201">Reserved throughput for hello table expressed in request units (RU) per second.</span></span> <span data-ttu-id="17455-202">Las tablas únicas puede admitir cientos de millones de RU/s.</span><span class="sxs-lookup"><span data-stu-id="17455-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="17455-203">Consulte [Unidades de solicitud](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="17455-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="17455-204">El valor predeterminado es `400`</span><span class="sxs-lookup"><span data-stu-id="17455-204">Default is `400`</span></span> |
| <span data-ttu-id="17455-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="17455-205">TableIndexingPolicy</span></span> | <span data-ttu-id="17455-206">Indexado secundario coherente y automático de todas las columnas dentro de las tablas</span><span class="sxs-lookup"><span data-stu-id="17455-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="17455-207">Toohello que cumplan con la indización de especificación de la directiva de cadena JSON.</span><span class="sxs-lookup"><span data-stu-id="17455-207">JSON string conforming toohello indexing policy specification.</span></span> <span data-ttu-id="17455-208">Vea [directiva de indización](indexing-policies.md) toosee cómo puede cambiar columnas específicas de indización directiva tooinclude/exclude.</span><span class="sxs-lookup"><span data-stu-id="17455-208">See [Indexing Policy](indexing-policies.md) toosee how you can change indexing policy tooinclude/exclude specific columns.</span></span> | <span data-ttu-id="17455-209">Indexado automático de todas las propiedades (hash para cadenas e intervalo para números)</span><span class="sxs-lookup"><span data-stu-id="17455-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="17455-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="17455-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="17455-211">Configurar Hola número máximo de elementos devueltos por la consulta de tabla en un viaje de ida y.</span><span class="sxs-lookup"><span data-stu-id="17455-211">Configure hello maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="17455-212">Valor predeterminado es `-1`, que permite que base de datos de Azure Cosmos determinar dinámicamente el valor de hello en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="17455-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |
| <span data-ttu-id="17455-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="17455-213">TableQueryEnableScan</span></span> | <span data-ttu-id="17455-214">Si consulta hello no puede utilizar el índice de Hola para cualquier filtro, a continuación, ejecutarlo todos modos a través de un examen.</span><span class="sxs-lookup"><span data-stu-id="17455-214">If hello query cannot use hello index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="17455-215">El valor predeterminado es `false`.</span><span class="sxs-lookup"><span data-stu-id="17455-215">Default is `false`.</span></span>|
| <span data-ttu-id="17455-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="17455-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="17455-217">grado de Hola de paralelismo para la ejecución de una consulta entre particiones.</span><span class="sxs-lookup"><span data-stu-id="17455-217">hello degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="17455-218">`0`es en serie con ninguna captura previa, `1` es en serie con captura previa y los valores altos aumento de velocidad de Hola de paralelismo.</span><span class="sxs-lookup"><span data-stu-id="17455-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase hello rate of parallelism.</span></span> <span data-ttu-id="17455-219">Valor predeterminado es `-1`, que permite que base de datos de Azure Cosmos determinar dinámicamente el valor de hello en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="17455-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |

<span data-ttu-id="17455-220">toochange Hola valor, abra hello `app.config` archivo desde el Explorador de soluciones en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17455-220">toochange hello default value, open hello `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="17455-221">Agregar contenido de Hola de hello `<appSettings>` elemento se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="17455-221">Add hello contents of hello `<appSettings>` element shown below.</span></span> <span data-ttu-id="17455-222">Reemplace `account-name` con el nombre de saludo de la cuenta de almacenamiento y `account-key` con su clave de acceso de cuenta.</span><span class="sxs-lookup"><span data-stu-id="17455-222">Replace `account-name` with hello name of your storage account, and `account-key` with your account access key.</span></span> 

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

<span data-ttu-id="17455-223">Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="17455-223">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="17455-224">Abra hello `Program.cs` archivo y descubre que estas líneas de código crean Hola recursos de la tabla.</span><span class="sxs-lookup"><span data-stu-id="17455-224">Open hello `Program.cs` file and you find that these lines of code create hello Table resources.</span></span> 

## <a name="create-hello-table-client"></a><span data-ttu-id="17455-225">Crear el cliente de la tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="17455-225">Create hello table client</span></span>
<span data-ttu-id="17455-226">Inicializar un `CloudTableClient` cuenta de tabla de tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="17455-226">You initialize a `CloudTableClient` tooconnect toohello table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="17455-227">Este cliente se inicializa con hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, y `TablePreferredLocations` si se especifica en configuración de la aplicación hello de los valores de configuración.</span><span class="sxs-lookup"><span data-stu-id="17455-227">This client is initialized using hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in hello app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="17455-228">Creación de una tabla</span><span class="sxs-lookup"><span data-stu-id="17455-228">Create a table</span></span>
<span data-ttu-id="17455-229">Luego, se crea una tabla con `CloudTable`.</span><span class="sxs-lookup"><span data-stu-id="17455-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="17455-230">Tablas de base de datos de Azure Cosmos pueden escalar de forma independiente en cuanto a almacenamiento y rendimiento, y el servicio Hola particiones administra automáticamente.</span><span class="sxs-lookup"><span data-stu-id="17455-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by hello service.</span></span> <span data-ttu-id="17455-231">Azure Cosmos DB admite tanto tablas ilimitadas como de tamaño fijo.</span><span class="sxs-lookup"><span data-stu-id="17455-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="17455-232">Consulte [Creación de particiones en Azure Cosmos DB](partition-data.md) para obtener detalles.</span><span class="sxs-lookup"><span data-stu-id="17455-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="17455-233">Existe una diferencia importante en la manera de crear las tablas.</span><span class="sxs-lookup"><span data-stu-id="17455-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="17455-234">Azure Cosmos DB reserva rendimiento, a diferencia del modelo basado en consumo de Azure Storage para las transacciones.</span><span class="sxs-lookup"><span data-stu-id="17455-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="17455-235">modelo de reserva de Hello tiene dos ventajas clave:</span><span class="sxs-lookup"><span data-stu-id="17455-235">hello reservation model has two key benefits:</span></span>

* <span data-ttu-id="17455-236">El rendimiento es dedicado/reservado, por lo que nunca se verá limitado si la velocidad de solicitudes se encuentra en el rendimiento aprovisionado o está por debajo de este</span><span class="sxs-lookup"><span data-stu-id="17455-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="17455-237">modelo de reserva de Hello es más [rentable para cargas de trabajo de uso intensivo de rendimiento](key-value-store-cost.md)</span><span class="sxs-lookup"><span data-stu-id="17455-237">hello reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="17455-238">Puede configurar el rendimiento de hello predeterminado mediante la configuración de Hola para `TableThroughput` en cuanto a RU (unidades de solicitud) por segundo.</span><span class="sxs-lookup"><span data-stu-id="17455-238">You can configure hello default throughput by configuring hello setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="17455-239">Una lectura de una entidad de 1 KB se normaliza como 1 RU y otras operaciones son tooa normalizado fijo valor RU según su consumo de CPU, memoria y e/s por segundo.</span><span class="sxs-lookup"><span data-stu-id="17455-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized tooa fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="17455-240">Más información sobre [Unidades de solicitud en Azure Cosmos DB](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="17455-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="17455-241">Aunque SDK de almacenamiento de tabla no admite actualmente la modificación de rendimiento, puede cambiar el rendimiento de hello al instante en cualquier momento mediante el portal de Azure de Hola o CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="17455-241">While Table storage SDK does not currently support modifying throughput, you can change hello throughput instantaneously at any time using hello Azure portal or Azure CLI.</span></span>

<span data-ttu-id="17455-242">A continuación, se recorra lectura simple hello y operaciones de escritura (CRUD) mediante almacenamiento de tabla de Azure Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="17455-242">Next, we walk through hello simple read and write (CRUD) operations using hello Azure Table storage SDK.</span></span> <span data-ttu-id="17455-243">En este tutorial se muestran las consultas rápidas y las latencias bajas predecibles de milisegundos de un solo dígito que proporciona Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="17455-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="17455-244">Agregar una tabla de tooa de entidad</span><span class="sxs-lookup"><span data-stu-id="17455-244">Add an entity tooa table</span></span>
<span data-ttu-id="17455-245">Las entidades de almacenamiento de tabla de Azure se extienden desde hello `TableEntity` clase y debe tener `PartitionKey` y `RowKey` propiedades.</span><span class="sxs-lookup"><span data-stu-id="17455-245">Entities in Azure Table storage extend from hello `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="17455-246">La siguiente es una definición de ejemplo de una entidad de cliente.</span><span class="sxs-lookup"><span data-stu-id="17455-246">Here's a sample definition for a customer entity.</span></span>

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

<span data-ttu-id="17455-247">Hola siguiente fragmento de código muestra cómo tooinsert una entidad con Hola almacenamiento de Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="17455-247">hello following snippet shows how tooinsert an entity with hello Azure storage SDK.</span></span> <span data-ttu-id="17455-248">Base de datos de Azure Cosmos está diseñado para garantiza una latencia baja a cualquier escala, a través de Hola a todos.</span><span class="sxs-lookup"><span data-stu-id="17455-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across hello world.</span></span>

<span data-ttu-id="17455-249">Completar escrituras < 15 ms en p99 y ~ 6 ms en p50 para aplicaciones que se ejecutan Hola misma región que la cuenta de base de datos de Azure Cosmos Hola.</span><span class="sxs-lookup"><span data-stu-id="17455-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in hello same region as hello Azure Cosmos DB account.</span></span> <span data-ttu-id="17455-250">Y esta duración cuentas para hechos de Hola que escribe se confirmen cliente toohello espera una vez que se replican de forma sincrónica, confirma de forma duradera, y se indiza todo el contenido.</span><span class="sxs-lookup"><span data-stu-id="17455-250">And this duration accounts for hello fact that writes are acknowledged back toohello client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="17455-251">Hola API de tabla de base de datos de Azure Cosmos está en vista previa.</span><span class="sxs-lookup"><span data-stu-id="17455-251">hello Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="17455-252">En disponibilidad general, garantías de latencia de hello p99 respaldados por el SLA al igual que otras API de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="17455-252">At general availability, hello p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="17455-253">Inserción de un lote de entidades</span><span class="sxs-lookup"><span data-stu-id="17455-253">Insert a batch of entities</span></span>
<span data-ttu-id="17455-254">Azure tabla almacenamiento es compatible con una API de operación por lotes, que le permite combinar las actualizaciones, eliminaciones e inserciones en Hola misma operación por lotes.</span><span class="sxs-lookup"><span data-stu-id="17455-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in hello same single batch operation.</span></span> <span data-ttu-id="17455-255">Base de datos de Azure Cosmos no tiene algunas de las limitaciones de hello en API de lote de hello como almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="17455-255">Azure Cosmos DB does not have some of hello limitations on hello batch API as Azure Table storage.</span></span> <span data-ttu-id="17455-256">Por ejemplo, puede realizar varias lecturas dentro de un lote, puede realizar varias toohello escrituras misma entidad dentro de un lote, y no hay ningún límite en 100 operaciones por lote.</span><span class="sxs-lookup"><span data-stu-id="17455-256">For example, you can perform multiple reads within a batch, you can perform multiple writes toohello same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="17455-257">una sola entidad</span><span class="sxs-lookup"><span data-stu-id="17455-257">Retrieve a single entity</span></span>
<span data-ttu-id="17455-258">Recupera (obtiene) en la base de datos de Cosmos a Azure completo < 10 ms en p99 y ~ 1 ms en p50 en Hola la misma región de Azure.</span><span class="sxs-lookup"><span data-stu-id="17455-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in hello same Azure region.</span></span> <span data-ttu-id="17455-259">Puede agregar tantos cuenta tooyour de regiones para lecturas de latencia baja e implementar aplicaciones tooread de su región local ("host múltiple") estableciendo `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="17455-259">You can add as many regions tooyour account for low latency reads, and deploy applications tooread from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="17455-260">Puede recuperar una sola entidad con el siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="17455-260">You can retrieve a single entity using hello following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="17455-261">Obtenga información sobre las API de hospedaje múltiple en [Desarrollo con varias regiones](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="17455-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="17455-262">Consulta de entidades con índices secundarios automáticos</span><span class="sxs-lookup"><span data-stu-id="17455-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="17455-263">Las tablas se pueden consultar mediante hello `TableQuery` clase.</span><span class="sxs-lookup"><span data-stu-id="17455-263">Tables can be queried using hello `TableQuery` class.</span></span> <span data-ttu-id="17455-264">Azure Cosmos DB tiene un motor de base de datos optimizado para escritura que indexa automáticamente todas las columnas dentro de la tabla.</span><span class="sxs-lookup"><span data-stu-id="17455-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="17455-265">La indización de base de datos de Azure Cosmos es tooschema independiente.</span><span class="sxs-lookup"><span data-stu-id="17455-265">Indexing in Azure Cosmos DB is agnostic tooschema.</span></span> <span data-ttu-id="17455-266">Por lo tanto, incluso si el esquema es diferente entre las filas, o si el esquema de hello evoluciona con el tiempo, se indizan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="17455-266">Therefore, even if your schema is different between rows, or if hello schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="17455-267">Puesto que la base de datos de Azure Cosmos admite índices secundarios automática, las consultas con respecto a cualquier propiedad pueden usar el índice de Hola y servidas eficazmente.</span><span class="sxs-lookup"><span data-stu-id="17455-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use hello index and be served efficiently.</span></span>

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

<span data-ttu-id="17455-268">En la vista previa, base de datos de Azure Cosmos admite Hola igual funcionalidad como almacenamiento de tabla de Azure para hello API de tabla de consulta.</span><span class="sxs-lookup"><span data-stu-id="17455-268">In preview, Azure Cosmos DB supports hello same query functionality as Azure Table storage for hello Table API.</span></span> <span data-ttu-id="17455-269">Azure Cosmos DB también admite ordenación, agregados, consulta geoespacial, jerarquía y una amplia variedad de funciones integradas.</span><span class="sxs-lookup"><span data-stu-id="17455-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="17455-270">se proporciona funcionalidad adicional de Hello en hello API de tabla en una actualización de servicio futura.</span><span class="sxs-lookup"><span data-stu-id="17455-270">hello additional functionality will be provided in hello Table API in a future service update.</span></span> <span data-ttu-id="17455-271">En [Consulta de Azure Cosmos DB](documentdb-sql-query.md) puede encontrar información general sobre esas funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="17455-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="17455-272">una entidad</span><span class="sxs-lookup"><span data-stu-id="17455-272">Replace an entity</span></span>
<span data-ttu-id="17455-273">tooupdate una entidad, recuperar del servicio de tabla de hello, modificar el objeto de entidad de hello y, a continuación, guardar los cambios de hello hacer copia de servicio de la tabla de toohello.</span><span class="sxs-lookup"><span data-stu-id="17455-273">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="17455-274">Hello código siguiente cambia número de teléfono de un cliente existente.</span><span class="sxs-lookup"><span data-stu-id="17455-274">hello following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="17455-275">Del mismo modo, puede realizar las operaciones `InsertOrMerge` o `Merge`.</span><span class="sxs-lookup"><span data-stu-id="17455-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="17455-276">Eliminación de una entidad</span><span class="sxs-lookup"><span data-stu-id="17455-276">Delete an entity</span></span>
<span data-ttu-id="17455-277">Puede eliminar fácilmente una entidad después de que se han recuperado mediante el uso de hello mismo patrón que se muestra para la actualización de una entidad.</span><span class="sxs-lookup"><span data-stu-id="17455-277">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="17455-278">Hola siguiente código recupera y elimina una entidad customer.</span><span class="sxs-lookup"><span data-stu-id="17455-278">hello following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="17455-279">Eliminación de una tabla</span><span class="sxs-lookup"><span data-stu-id="17455-279">Delete a table</span></span>
<span data-ttu-id="17455-280">Por último, Hola ejemplo de código siguiente elimina una tabla de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="17455-280">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="17455-281">Puede eliminar una tabla y volver a crearla de inmediato con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="17455-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="17455-282">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="17455-282">Clean up resources</span></span> 

<span data-ttu-id="17455-283">Si no va toocontinue toouse esta aplicación, utilice Hola después toodelete pasos todos los recursos creados por este tutorial Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="17455-283">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>   

1. <span data-ttu-id="17455-284">En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="17455-284">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span>  
2. <span data-ttu-id="17455-285">En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="17455-285">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="17455-286">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="17455-286">Next steps</span></span>

<span data-ttu-id="17455-287">En este tutorial, hemos aprendido cómo tooget a usar base de datos de Azure Cosmos con hello API de tabla y ha hecho siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="17455-287">In this tutorial, we covered how tooget started using Azure Cosmos DB with hello Table API, and you've done hello following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="17455-288">Se creó una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="17455-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="17455-289">Funcionalidad activada en el archivo app.config de hello</span><span class="sxs-lookup"><span data-stu-id="17455-289">Enabled functionality in hello app.config file</span></span> 
> * <span data-ttu-id="17455-290">Se creó una tabla</span><span class="sxs-lookup"><span data-stu-id="17455-290">Created a table</span></span> 
> * <span data-ttu-id="17455-291">Se ha agregado una tabla de tooa de entidad</span><span class="sxs-lookup"><span data-stu-id="17455-291">Added an entity tooa table</span></span> 
> * <span data-ttu-id="17455-292">Se insertó un lote de entidades</span><span class="sxs-lookup"><span data-stu-id="17455-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="17455-293">Se recuperó una sola entidad</span><span class="sxs-lookup"><span data-stu-id="17455-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="17455-294">Se consultaron las entidades con índices secundarios automáticos</span><span class="sxs-lookup"><span data-stu-id="17455-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="17455-295">Se reemplazó una entidad</span><span class="sxs-lookup"><span data-stu-id="17455-295">Replaced an entity</span></span> 
> * <span data-ttu-id="17455-296">Se eliminó una entidad</span><span class="sxs-lookup"><span data-stu-id="17455-296">Deleted an entity</span></span> 
> * <span data-ttu-id="17455-297">Se eliminó una tabla</span><span class="sxs-lookup"><span data-stu-id="17455-297">Deleted a table</span></span>  

<span data-ttu-id="17455-298">Ahora puede continuar el tutorial siguiente toohello y más información sobre cómo consultar los datos de la tabla.</span><span class="sxs-lookup"><span data-stu-id="17455-298">You can now proceed toohello next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="17455-299">Consultar con hello API de tabla</span><span class="sxs-lookup"><span data-stu-id="17455-299">Query with hello Table API</span></span>](tutorial-query-table.md)
