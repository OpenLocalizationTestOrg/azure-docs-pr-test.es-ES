---
title: aaaMigrate el almacenamiento de datos de datos tooSQL | Documentos de Microsoft
description: Sugerencias para migrar el almacenamiento de datos SQL de datos tooAzure para desarrollar soluciones.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="330b1-103">Migración de los datos</span><span class="sxs-lookup"><span data-stu-id="330b1-103">Migrate Your Data</span></span>
<span data-ttu-id="330b1-104">Se pueden mover datos de distintos orígenes a Almacenamiento de datos SQL con diversas herramientas.</span><span class="sxs-lookup"><span data-stu-id="330b1-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="330b1-105">Copia de ADF y SSIS, bcp pueden ser utilizado tooachieve este objetivo.</span><span class="sxs-lookup"><span data-stu-id="330b1-105">ADF Copy, SSIS, and bcp can all be used tooachieve this goal.</span></span> <span data-ttu-id="330b1-106">Sin embargo, a medida que aumenta la cantidad de Hola de datos debería pensar en dividir el proceso de migración de datos de hello en pasos.</span><span class="sxs-lookup"><span data-stu-id="330b1-106">However, as hello amount of data increases you should think about breaking down hello data migration process into steps.</span></span> <span data-ttu-id="330b1-107">Esta opción proporciona Hola oportunidad toooptimize cada paso para obtener un rendimiento y de resistencia tooensure una migración de datos sin problemas.</span><span class="sxs-lookup"><span data-stu-id="330b1-107">This affords you hello opportunity toooptimize each step both for performance and for resilience tooensure a smooth data migration.</span></span>

<span data-ttu-id="330b1-108">En primer lugar, este artículo describe escenarios de migración simple de Hola de copia de ADF, SSIS y bcp.</span><span class="sxs-lookup"><span data-stu-id="330b1-108">This article first discusses hello simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="330b1-109">A continuación, busque un poco más en cómo se puede optimizar la migración de Hola.</span><span class="sxs-lookup"><span data-stu-id="330b1-109">It then look a little deeper into how hello migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="330b1-110">Copia de Factoría de datos de Azure (ADF)</span><span class="sxs-lookup"><span data-stu-id="330b1-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="330b1-111">[Copia de ADF][ADF Copy] forma parte de [Azure Data Factory][Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="330b1-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="330b1-112">Puede usar tooexport ADF copia los archivos de tooflat de datos que reside en el almacenamiento local, archivos sin formato tooremote mantienen en el almacenamiento de blobs de Azure o directamente en el almacén de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="330b1-112">You can use ADF Copy tooexport your data tooflat files residing on local storage, tooremote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="330b1-113">Si los datos se inicia en archivos planos, primero deberá tootransfer se tooAzure blob de almacenamiento antes de iniciar una carga en el almacén de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="330b1-113">If your data starts in flat files, then you will first need tootransfer it tooAzure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="330b1-114">Una vez que se transfieren datos de hello en el almacenamiento de blobs de Azure puede elegir toouse [ADF copia] [ ADF Copy] nuevo toopush datos hello en almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="330b1-114">Once hello data is transferred into Azure blob storage you can choose toouse [ADF Copy][ADF Copy] again toopush hello data into SQL Data Warehouse.</span></span>

<span data-ttu-id="330b1-115">PolyBase también proporciona una opción de alto rendimiento para cargar los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="330b1-115">PolyBase also provides a high-performance option for loading hello data.</span></span> <span data-ttu-id="330b1-116">Sin embargo, eso significa tener que usar dos herramientas en lugar de una.</span><span class="sxs-lookup"><span data-stu-id="330b1-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="330b1-117">Si necesita obtener el mejor rendimiento de hello, a continuación, usar PolyBase.</span><span class="sxs-lookup"><span data-stu-id="330b1-117">If you need hello best performance then use PolyBase.</span></span> <span data-ttu-id="330b1-118">Si desea una experiencia única herramienta (y datos de hello no son masivos) ADF es la respuesta.</span><span class="sxs-lookup"><span data-stu-id="330b1-118">If you want a single tool experience (and hello data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="330b1-119">Principal sobre toohello artículo para algunos great siguiente [ejemplos ADF][ADF samples].</span><span class="sxs-lookup"><span data-stu-id="330b1-119">Head over toohello following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="330b1-120">Servicios de integración</span><span class="sxs-lookup"><span data-stu-id="330b1-120">Integration Services</span></span>
<span data-ttu-id="330b1-121">Integration Services (SSIS) es una herramienta eficaz y flexible de extracción, transformación y carga de datos (ETL) que admite varias opciones de carga de datos, flujos de trabajo complejos y transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="330b1-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="330b1-122">Usar SSIS toosimply transferencia datos tooAzure o como parte de una migración más amplia.</span><span class="sxs-lookup"><span data-stu-id="330b1-122">Use SSIS toosimply transfer data tooAzure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="330b1-123">SSIS puede exportar tooUTF-8 sin marca de orden de bytes de hello en el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="330b1-123">SSIS can export tooUTF-8 without hello byte order mark in hello file.</span></span> <span data-ttu-id="330b1-124">tooconfigure esto primero debe usar Hola derivar datos de caracteres de columna componente tooconvert hello en Hola página de códigos de datos flujo toouse Hola 65001 UTF-8.</span><span class="sxs-lookup"><span data-stu-id="330b1-124">tooconfigure this you must first use hello derived column component tooconvert hello character data in hello data flow toouse hello 65001 UTF-8 code page.</span></span> <span data-ttu-id="330b1-125">Una vez que se han convertido columnas hello, Hola datos toohello archivos planos destino adaptador asegurar que la escritura que 65001 también se ha seleccionado como página de códigos de hello para el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="330b1-125">Once hello columns have been converted, write hello data toohello flat file destination adapter ensuring that 65001 has also been selected as hello code page for hello file.</span></span>
> 
> 

<span data-ttu-id="330b1-126">SSIS conecta tooSQL almacenamiento de datos tal y como conectaría tooa implementación de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="330b1-126">SSIS connects tooSQL Data Warehouse just as it would connect tooa SQL Server deployment.</span></span> <span data-ttu-id="330b1-127">Sin embargo, las conexiones tendrá toobe mediante un administrador de conexiones de ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="330b1-127">However, your connections will need toobe using an ADO.NET connection manager.</span></span> <span data-ttu-id="330b1-128">También debe tener cuidado para hello tooconfigure "Use inserción masiva cuando esté disponible" rendimiento de toomaximize de configuración.</span><span class="sxs-lookup"><span data-stu-id="330b1-128">You should also take care tooconfigure hello "Use bulk insert when available" setting toomaximize throughput.</span></span> <span data-ttu-id="330b1-129">Consulte toohello [adaptador de destino de ADO.NET] [ ADO.NET destination adapter] más información acerca de esta propiedad de artículo toolearn</span><span class="sxs-lookup"><span data-stu-id="330b1-129">Please refer toohello [ADO.NET destination adapter][ADO.NET destination adapter] article toolearn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="330b1-130">No se admite la conexión tooAzure almacenamiento de datos SQL mediante OLE DB.</span><span class="sxs-lookup"><span data-stu-id="330b1-130">Connecting tooAzure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="330b1-131">Además, siempre hay posibilidad de Hola que un paquete puede producir un error debido a problemas de red o toothrottling.</span><span class="sxs-lookup"><span data-stu-id="330b1-131">In addition, there is always hello possibility that a package might fail due toothrottling or network issues.</span></span> <span data-ttu-id="330b1-132">Paquetes de diseño, por lo que se puedan reanudar en punto de Hola de error, sin rehacer de trabajo que se complete antes de error de Hola.</span><span class="sxs-lookup"><span data-stu-id="330b1-132">Design packages so they can be resumed at hello point of failure, without redoing work that completed before hello failure.</span></span>

<span data-ttu-id="330b1-133">Para obtener más información, consulte hello [documentación SSIS][SSIS documentation].</span><span class="sxs-lookup"><span data-stu-id="330b1-133">For more information consult hello [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="330b1-134">bcp</span><span class="sxs-lookup"><span data-stu-id="330b1-134">bcp</span></span>
<span data-ttu-id="330b1-135">bcp es una utilidad de línea de comandos que se ha diseñado para la importación y exportación de datos de archivos planos.</span><span class="sxs-lookup"><span data-stu-id="330b1-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="330b1-136">Puede producirse alguna transformación durante la exportación de datos.</span><span class="sxs-lookup"><span data-stu-id="330b1-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="330b1-137">transformaciones simples tooperform utilizar una consulta tooselect y transforman datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="330b1-137">tooperform simple transformations use a query tooselect and transform hello data.</span></span> <span data-ttu-id="330b1-138">Una vez exportado, a continuación, se pueden cargar archivos planos Hola directamente en la base de datos de almacenamiento de datos SQL de hello destino Hola.</span><span class="sxs-lookup"><span data-stu-id="330b1-138">Once exported, hello flat files can then be loaded directly into hello target hello SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="330b1-139">A menudo resulta una Hola de tooencapsulate conveniente exportación las transformaciones que se usa durante los datos en una vista de sistema de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="330b1-139">It is often a good idea tooencapsulate hello transformations used during data export in a view on hello source system.</span></span> <span data-ttu-id="330b1-140">Esto garantiza que se conserva la lógica de Hola y Hola proceso es repetible.</span><span class="sxs-lookup"><span data-stu-id="330b1-140">This ensures that hello logic is retained and hello process is repeatable.</span></span>
> 
> 

<span data-ttu-id="330b1-141">Las ventajas de bcp son:</span><span class="sxs-lookup"><span data-stu-id="330b1-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="330b1-142">Simplicidad.</span><span class="sxs-lookup"><span data-stu-id="330b1-142">Simplicity.</span></span> <span data-ttu-id="330b1-143">se toobuild simple y ejecutarán comandos de bcp</span><span class="sxs-lookup"><span data-stu-id="330b1-143">bcp commands are simple toobuild and execute</span></span>
* <span data-ttu-id="330b1-144">Proceso de carga reiniciable.</span><span class="sxs-lookup"><span data-stu-id="330b1-144">Re-startable load process.</span></span> <span data-ttu-id="330b1-145">Carga una vez exportado Hola pueden ejecutar un número ilimitado de veces</span><span class="sxs-lookup"><span data-stu-id="330b1-145">Once exported hello load can be executed any number of times</span></span>

<span data-ttu-id="330b1-146">Las limitaciones de bcp son:</span><span class="sxs-lookup"><span data-stu-id="330b1-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="330b1-147">bcp solo funciona con archivos planos tabulados.</span><span class="sxs-lookup"><span data-stu-id="330b1-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="330b1-148">No funciona con archivos, como xml o JSON.</span><span class="sxs-lookup"><span data-stu-id="330b1-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="330b1-149">Capacidades de transformación de datos son de solo copia intermedia de exportación de toohello limitado y son de naturaleza simples</span><span class="sxs-lookup"><span data-stu-id="330b1-149">Data transformation capabilities are limited toohello export stage only and are simple in nature</span></span>
* <span data-ttu-id="330b1-150">bcp no ha sido adaptado toobe sólida cuando Hola de cargar datos en internet.</span><span class="sxs-lookup"><span data-stu-id="330b1-150">bcp has not been adapted toobe robust when loading data over hello internet.</span></span> <span data-ttu-id="330b1-151">Cualquier inestabilidad en la red puede provocar un error de carga.</span><span class="sxs-lookup"><span data-stu-id="330b1-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="330b1-152">bcp se basa en el esquema Hola estén presentes en la carga de toohello anteriores de base de datos de destino de Hola</span><span class="sxs-lookup"><span data-stu-id="330b1-152">bcp relies on hello schema being present in hello target database prior toohello load</span></span>

<span data-ttu-id="330b1-153">Para obtener más información, consulte [usar datos de tooload de bcp en almacenamiento de datos de SQL][Use bcp tooload data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="330b1-153">For more information, see [Use bcp tooload data into SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="330b1-154">Optimización de migración de datos</span><span class="sxs-lookup"><span data-stu-id="330b1-154">Optimizing data migration</span></span>
<span data-ttu-id="330b1-155">Un proceso de migración de datos SQLDW puede dividirse eficazmente en tres pasos independientes:</span><span class="sxs-lookup"><span data-stu-id="330b1-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="330b1-156">Exportación de datos de origen</span><span class="sxs-lookup"><span data-stu-id="330b1-156">Export of source data</span></span>
2. <span data-ttu-id="330b1-157">Transferencia de datos tooAzure</span><span class="sxs-lookup"><span data-stu-id="330b1-157">Transfer of data tooAzure</span></span>
3. <span data-ttu-id="330b1-158">Cargar en la base de datos de hello destino SQLDW</span><span class="sxs-lookup"><span data-stu-id="330b1-158">Load into hello target SQLDW database</span></span>

<span data-ttu-id="330b1-159">Cada paso puede ser individualmente optimizado toocreate un proceso de migración sólido, podrá volver a iniciar y flexible que maximiza el rendimiento en cada paso.</span><span class="sxs-lookup"><span data-stu-id="330b1-159">Each step can be individually optimized toocreate a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="330b1-160">Optimización de carga de datos</span><span class="sxs-lookup"><span data-stu-id="330b1-160">Optimizing data load</span></span>
<span data-ttu-id="330b1-161">Examinando estos en orden inverso durante un momento; datos de tooload de manera más rápidos de saludo están a través de PolyBase.</span><span class="sxs-lookup"><span data-stu-id="330b1-161">Looking at these in reverse order for a moment; hello fastest way tooload data is via PolyBase.</span></span> <span data-ttu-id="330b1-162">Optimizar para un proceso de carga de PolyBase coloca los requisitos previos en hello pasos anteriores por lo que es mejor toounderstand esto por adelantado.</span><span class="sxs-lookup"><span data-stu-id="330b1-162">Optimizing for a PolyBase load process places prerequisites on hello preceding steps so it's best toounderstand this upfront.</span></span> <span data-ttu-id="330b1-163">Son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="330b1-163">They are:</span></span>

1. <span data-ttu-id="330b1-164">Codificación de archivos de datos</span><span class="sxs-lookup"><span data-stu-id="330b1-164">Encoding of data files</span></span>
2. <span data-ttu-id="330b1-165">Formato de archivos de datos</span><span class="sxs-lookup"><span data-stu-id="330b1-165">Format of data files</span></span>
3. <span data-ttu-id="330b1-166">Ubicación de archivos de datos</span><span class="sxs-lookup"><span data-stu-id="330b1-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="330b1-167">Codificación</span><span class="sxs-lookup"><span data-stu-id="330b1-167">Encoding</span></span>
<span data-ttu-id="330b1-168">PolyBase requiere toobe de archivos de datos UTF-8 o UTF-16FE.</span><span class="sxs-lookup"><span data-stu-id="330b1-168">PolyBase requires data files toobe UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="330b1-169">Formato de archivos de datos</span><span class="sxs-lookup"><span data-stu-id="330b1-169">Format of data files</span></span>
<span data-ttu-id="330b1-170">PolyBase exige un terminador de fila fijo de \n o una línea nueva.</span><span class="sxs-lookup"><span data-stu-id="330b1-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="330b1-171">Los archivos de datos deben cumplir toothis estándar.</span><span class="sxs-lookup"><span data-stu-id="330b1-171">Your data files must conform toothis standard.</span></span> <span data-ttu-id="330b1-172">No hay ninguna restricción sobre terminadores de columna o de cadena.</span><span class="sxs-lookup"><span data-stu-id="330b1-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="330b1-173">Tendrá toodefine todas las columnas en el archivo hello como parte de la tabla externa en PolyBase.</span><span class="sxs-lookup"><span data-stu-id="330b1-173">You will have toodefine every column in hello file as part of your external table in PolyBase.</span></span> <span data-ttu-id="330b1-174">Asegúrese de que todas las columnas exportadas son necesarias y que los tipos de Hola ajustan toohello necesario estándares.</span><span class="sxs-lookup"><span data-stu-id="330b1-174">Make sure that all exported columns are required and that hello types conform toohello required standards.</span></span>

<span data-ttu-id="330b1-175">Por favor, consulte toohello [migrar el esquema] artículo para obtener detalles sobre los tipos de datos admitidos.</span><span class="sxs-lookup"><span data-stu-id="330b1-175">Please refer back toohello [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="330b1-176">Ubicación de archivos de datos</span><span class="sxs-lookup"><span data-stu-id="330b1-176">Location of data files</span></span>
<span data-ttu-id="330b1-177">Almacenamiento de datos de SQL utiliza datos de tooload de PolyBase de almacenamiento de blobs de Azure exclusivamente.</span><span class="sxs-lookup"><span data-stu-id="330b1-177">SQL Data Warehouse uses PolyBase tooload data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="330b1-178">Por lo tanto, los datos de hello deben primero transferidos en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="330b1-178">Consequently, hello data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="330b1-179">Optimización de transferencia de datos</span><span class="sxs-lookup"><span data-stu-id="330b1-179">Optimizing data transfer</span></span>
<span data-ttu-id="330b1-180">Uno de los elementos más lentas de Hola de migración de datos es la transferencia de Hola de hello tooAzure de datos.</span><span class="sxs-lookup"><span data-stu-id="330b1-180">One of hello slowest parts of data migration is hello transfer of hello data tooAzure.</span></span> <span data-ttu-id="330b1-181">No solo el ancho de banda de red puede ser un problema, sino que la confiabilidad de la red también puede dificultar seriamente el progreso.</span><span class="sxs-lookup"><span data-stu-id="330b1-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="330b1-182">De forma predeterminada tooAzure migración de datos es sobre Hola internet tan Hola posibilidades de errores de transferencia que se producen es bastante probable.</span><span class="sxs-lookup"><span data-stu-id="330b1-182">By default migrating data tooAzure is over hello internet so hello chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="330b1-183">Sin embargo, estos errores pueden requerir volver a enviar en su totalidad o en parte de toobe de datos.</span><span class="sxs-lookup"><span data-stu-id="330b1-183">However, these errors may require data toobe re-sent either in whole or in part.</span></span>

<span data-ttu-id="330b1-184">Afortunadamente tiene varias velocidad de opciones tooimprove hello y resistencia de este proceso:</span><span class="sxs-lookup"><span data-stu-id="330b1-184">Fortunately you have several options tooimprove hello speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="330b1-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="330b1-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="330b1-186">Puede que desee usar tooconsider [ExpressRoute] [ ExpressRoute] toospeed la transferencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="330b1-186">You may want tooconsider using [ExpressRoute][ExpressRoute] toospeed up hello transfer.</span></span> <span data-ttu-id="330b1-187">[ExpressRoute] [ ExpressRoute] proporciona a una conexión privada establecida tooAzure para conexión de hello no pasa por Hola internet pública.</span><span class="sxs-lookup"><span data-stu-id="330b1-187">[ExpressRoute][ExpressRoute] provides you with an established private connection tooAzure so hello connection does not go over hello public internet.</span></span> <span data-ttu-id="330b1-188">No se trata en ningún caso de un paso obligatorio.</span><span class="sxs-lookup"><span data-stu-id="330b1-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="330b1-189">Sin embargo, mejora el rendimiento al realizar inserciones tooAzure de datos de una implementación local o instalación de colocalización.</span><span class="sxs-lookup"><span data-stu-id="330b1-189">However, it will improve throughput when pushing data tooAzure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="330b1-190">ventajas del uso de Hola [ExpressRoute] [ ExpressRoute] son:</span><span class="sxs-lookup"><span data-stu-id="330b1-190">hello benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="330b1-191">Mayor confiabilidad</span><span class="sxs-lookup"><span data-stu-id="330b1-191">Increased reliability</span></span>
2. <span data-ttu-id="330b1-192">Mayor velocidad de red</span><span class="sxs-lookup"><span data-stu-id="330b1-192">Faster network speed</span></span>
3. <span data-ttu-id="330b1-193">Menor latencia de red</span><span class="sxs-lookup"><span data-stu-id="330b1-193">Lower network latency</span></span>
4. <span data-ttu-id="330b1-194">Mayor seguridad de red</span><span class="sxs-lookup"><span data-stu-id="330b1-194">higher network security</span></span>

<span data-ttu-id="330b1-195">[ExpressRoute] [ ExpressRoute] es beneficioso para varios escenarios; no solo Hola migración.</span><span class="sxs-lookup"><span data-stu-id="330b1-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just hello migration.</span></span>

<span data-ttu-id="330b1-196">¿Le interesa?</span><span class="sxs-lookup"><span data-stu-id="330b1-196">Interested?</span></span> <span data-ttu-id="330b1-197">Para obtener más información y los precios, visite hello [documentación de ExpressRoute][ExpressRoute documentation].</span><span class="sxs-lookup"><span data-stu-id="330b1-197">For more information and pricing please visit hello [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="330b1-198">Servicio Importación/Exportación de Azure</span><span class="sxs-lookup"><span data-stu-id="330b1-198">Azure Import and Export Service</span></span>
<span data-ttu-id="330b1-199">Hello Azure servicio de importación y exportación es un proceso de transferencia de datos diseñado para grandes (GB ++) toomassive (TB ++) las transferencias de datos en Azure.</span><span class="sxs-lookup"><span data-stu-id="330b1-199">hello Azure Import and Export Service is a data transfer process designed for large (GB++) toomassive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="330b1-200">Implica escribir su toodisks de datos y su posterior envío tooan centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="330b1-200">It involves writing your data toodisks and shipping them tooan Azure data center.</span></span> <span data-ttu-id="330b1-201">contenido del disco Hello, a continuación, se cargarán en Blobs de almacenamiento de Azure en su nombre.</span><span class="sxs-lookup"><span data-stu-id="330b1-201">hello disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="330b1-202">Una vista de alto nivel del proceso de exportación de importación de hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="330b1-202">A high-level view of hello import export process is as follows:</span></span>

1. <span data-ttu-id="330b1-203">Configurar un contenedor de almacenamiento de blobs de Azure tooreceive Hola datos</span><span class="sxs-lookup"><span data-stu-id="330b1-203">Configure an Azure Blob Storage container tooreceive hello data</span></span>
2. <span data-ttu-id="330b1-204">Exportar el almacenamiento de datos toolocal</span><span class="sxs-lookup"><span data-stu-id="330b1-204">Export your data toolocal storage</span></span>
3. <span data-ttu-id="330b1-205">Copiar Hola datos too3.5 pulgadas SATA II/III unidades de disco duro con hello [herramienta de importación y exportación de Azure]</span><span class="sxs-lookup"><span data-stu-id="330b1-205">Copy hello data too3.5 inch SATA II/III hard disk drives using hello [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="330b1-206">Crear un trabajo de importación mediante hello importación de Azure y servicio de exportación que proporciona archivos de diario de hello generados por hello [herramienta de importación y exportación de Azure]</span><span class="sxs-lookup"><span data-stu-id="330b1-206">Create an Import Job using hello Azure Import and Export Service providing hello journal files produced by hello [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="330b1-207">Enviar discos de hello su centro de datos de Azure designado</span><span class="sxs-lookup"><span data-stu-id="330b1-207">Ship hello disks your nominated Azure data center</span></span>
6. <span data-ttu-id="330b1-208">Los datos están el contenedor de almacenamiento de blobs de Azure de tooyour transferidos</span><span class="sxs-lookup"><span data-stu-id="330b1-208">Your data is transferred tooyour Azure Blob Storage container</span></span>
7. <span data-ttu-id="330b1-209">Cargar datos de hello en SQLDW con PolyBase</span><span class="sxs-lookup"><span data-stu-id="330b1-209">Load hello data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="330b1-210">Utilidad [AZCopy][AZCopy]</span><span class="sxs-lookup"><span data-stu-id="330b1-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="330b1-211">Hola [AZCopy][AZCopy] utilidad es una herramienta excelente para obtener los datos transferidos a Blobs de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="330b1-211">hello [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="330b1-212">Está diseñada para pequeñas (MB ++) toovery grandes (GB ++) las transferencias de datos.</span><span class="sxs-lookup"><span data-stu-id="330b1-212">It is designed for small (MB++) toovery large (GB++) data transfers.</span></span> <span data-ttu-id="330b1-213">[AZCopy] también ha sido un buen rendimiento resistente de tooprovide diseñada al transferir datos tooAzure de modo que es una excelente opción para el paso de transferencia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="330b1-213">[AZCopy] has also been designed tooprovide good resilient throughput when transferring data tooAzure and so is a great choice for hello data transfer step.</span></span> <span data-ttu-id="330b1-214">Una vez transferidos puede cargar datos de hello con PolyBase en almacenamiento de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="330b1-214">Once transferred you can load hello data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="330b1-215">También puede incorporar AZCopy a los paquetes SSIS con una tarea "Ejecutar proceso".</span><span class="sxs-lookup"><span data-stu-id="330b1-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="330b1-216">toouse AZCopy necesitará toodownload e instalarlo primero.</span><span class="sxs-lookup"><span data-stu-id="330b1-216">toouse AZCopy you will first need toodownload and install it.</span></span> <span data-ttu-id="330b1-217">Hay una [versión de producción][production version] y una [versión preliminar][preview version] disponibles.</span><span class="sxs-lookup"><span data-stu-id="330b1-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="330b1-218">tooupload un archivo desde el sistema de archivos que se necesitará un comando como Hola uno a continuación:</span><span class="sxs-lookup"><span data-stu-id="330b1-218">tooupload a file from your file system you will need a command like hello one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="330b1-219">Un resumen del proceso general podría ser:</span><span class="sxs-lookup"><span data-stu-id="330b1-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="330b1-220">Configurar un contenedor de almacenamiento de Azure blob tooreceive Hola datos</span><span class="sxs-lookup"><span data-stu-id="330b1-220">Configure an Azure storage blob container tooreceive hello data</span></span>
2. <span data-ttu-id="330b1-221">Exportar el almacenamiento de datos toolocal</span><span class="sxs-lookup"><span data-stu-id="330b1-221">Export your data toolocal storage</span></span>
3. <span data-ttu-id="330b1-222">Los datos en el contenedor de almacenamiento de blobs de Azure de hello AZCopy</span><span class="sxs-lookup"><span data-stu-id="330b1-222">AZCopy your data in hello Azure Blob Storage container</span></span>
4. <span data-ttu-id="330b1-223">Cargar datos de hello en almacenamiento de datos de SQL con PolyBase</span><span class="sxs-lookup"><span data-stu-id="330b1-223">Load hello data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="330b1-224">Documentación completa disponible: [AZCopy][AZCopy].</span><span class="sxs-lookup"><span data-stu-id="330b1-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="330b1-225">Optimización de exportación de datos</span><span class="sxs-lookup"><span data-stu-id="330b1-225">Optimizing data export</span></span>
<span data-ttu-id="330b1-226">Además tooensuring que exportación Hola cumple requisitos toohello dispuestos PolyBase puede buscar también exportación de hello toooptimize Hola proceso de datos tooimprove Hola aún más.</span><span class="sxs-lookup"><span data-stu-id="330b1-226">In addition tooensuring that hello export conforms toohello requirements laid out by PolyBase you can also seek toooptimize hello export of hello data tooimprove hello process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="330b1-227">Compresión de datos</span><span class="sxs-lookup"><span data-stu-id="330b1-227">Data compression</span></span>
<span data-ttu-id="330b1-228">PolyBase puede leer datos comprimidos con gzip.</span><span class="sxs-lookup"><span data-stu-id="330b1-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="330b1-229">Si es capaz de toocompress que los archivos de datos toogzip, a continuación, se minimizará la cantidad de Hola de datos que se va a insertar en la red de Hola.</span><span class="sxs-lookup"><span data-stu-id="330b1-229">If you are able toocompress your data toogzip files then you will minimize hello amount of data being pushed over hello network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="330b1-230">Varios archivos</span><span class="sxs-lookup"><span data-stu-id="330b1-230">Multiple files</span></span>
<span data-ttu-id="330b1-231">Dividir las tablas grandes en varios archivos no solo ayuda a tooimprove exportar velocidad, también ayuda a con transferencia re-startability y Hola facilidad de uso general de los datos de hello una vez en el almacenamiento de blobs de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="330b1-231">Breaking up large tables into several files not only helps tooimprove export speed, it also helps with transfer re-startability, and hello overall manageability of hello data once in hello Azure blob storage.</span></span> <span data-ttu-id="330b1-232">Uno de hello muchas características "nice" de PolyBase es que se leen todos los archivos de hello dentro de una carpeta y tratarlo como una tabla.</span><span class="sxs-lookup"><span data-stu-id="330b1-232">One of hello many nice features of PolyBase is that it will read all hello files inside a folder and treat it as one table.</span></span> <span data-ttu-id="330b1-233">Por lo tanto es archivos de hello tooisolate una buena idea para cada tabla en su propia carpeta.</span><span class="sxs-lookup"><span data-stu-id="330b1-233">It is therefore a good idea tooisolate hello files for each table into its own folder.</span></span>

<span data-ttu-id="330b1-234">PolyBase también admite una característica conocida como "cruce de carpetas recursivo".</span><span class="sxs-lookup"><span data-stu-id="330b1-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="330b1-235">Puede utilizar esta característica toofurther mejorar la organización de Hola de los datos exportados tooimprove la administración de datos.</span><span class="sxs-lookup"><span data-stu-id="330b1-235">You can use this feature toofurther enhance hello organization of your exported data tooimprove your data management.</span></span>

<span data-ttu-id="330b1-236">toolearn más información acerca de la carga de datos con PolyBase, consulte [datos de uso PolyBase tooload en almacenamiento de datos de SQL][Use PolyBase tooload data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="330b1-236">toolearn more about loading data with PolyBase, see [Use PolyBase tooload data into SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="330b1-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="330b1-237">Next steps</span></span>
<span data-ttu-id="330b1-238">Para obtener más información acerca de la migración, consulte [migrar el almacenamiento de datos de solución tooSQL][Migrate your solution tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="330b1-238">For more about migration, see [Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse].</span></span>
<span data-ttu-id="330b1-239">Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].</span><span class="sxs-lookup"><span data-stu-id="330b1-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
