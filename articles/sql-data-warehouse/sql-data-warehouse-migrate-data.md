---
title: "Migración de los datos a SQL Data Warehouse | Microsoft Docs"
description: Sugerencias para migrar los datos a Almacenamiento de datos SQL de Azure a fin de desarrollar soluciones.
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
ms.openlocfilehash: dbdf1696cd169aa7e5e23f116027a1170347f4ea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="9e014-103">Migración de los datos</span><span class="sxs-lookup"><span data-stu-id="9e014-103">Migrate Your Data</span></span>
<span data-ttu-id="9e014-104">Se pueden mover datos de distintos orígenes a Almacenamiento de datos SQL con diversas herramientas.</span><span class="sxs-lookup"><span data-stu-id="9e014-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="9e014-105">Puede usarse Copia de ADF, SSIS y bcp para lograr este objetivo.</span><span class="sxs-lookup"><span data-stu-id="9e014-105">ADF Copy, SSIS, and bcp can all be used to achieve this goal.</span></span> <span data-ttu-id="9e014-106">Sin embargo, a medida que la cantidad de datos aumente debería pensar en descomponer en pasos el proceso de migración de datos.</span><span class="sxs-lookup"><span data-stu-id="9e014-106">However, as the amount of data increases you should think about breaking down the data migration process into steps.</span></span> <span data-ttu-id="9e014-107">Esto le ofrece la posibilidad de optimizar cada paso en cuanto a rendimiento y resistencia para garantizar una migración de datos sin problemas.</span><span class="sxs-lookup"><span data-stu-id="9e014-107">This affords you the opportunity to optimize each step both for performance and for resilience to ensure a smooth data migration.</span></span>

<span data-ttu-id="9e014-108">En este artículo se describen en primer lugar los escenarios sencillos de migración de Copia de ADF, SSIS y bcp.</span><span class="sxs-lookup"><span data-stu-id="9e014-108">This article first discusses the simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="9e014-109">Luego ahonda algo más en cómo se puede optimizar la migración.</span><span class="sxs-lookup"><span data-stu-id="9e014-109">It then look a little deeper into how the migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="9e014-110">Copia de Factoría de datos de Azure (ADF)</span><span class="sxs-lookup"><span data-stu-id="9e014-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="9e014-111">[Copia de ADF][ADF Copy] forma parte de [Azure Data Factory][Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="9e014-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="9e014-112">Puede usar Copia de ADF para exportar los datos a archivos planos que se encuentran en el almacenamiento local, a archivos planos remotos que se mantienen en el almacenamiento de blobs de Azure o directamente a Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="9e014-112">You can use ADF Copy to export your data to flat files residing on local storage, to remote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="9e014-113">Si los datos comienzan en archivos planos, tendrá que transferirlos primero a Azure Storage Blob antes de iniciar su carga en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="9e014-113">If your data starts in flat files, then you will first need to transfer it to Azure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="9e014-114">Una vez que se transfieren los datos a Azure Blob Storage puede volver a usar [Copia de ADF][ADF Copy] para insertar los datos en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="9e014-114">Once the data is transferred into Azure blob storage you can choose to use [ADF Copy][ADF Copy] again to push the data into SQL Data Warehouse.</span></span>

<span data-ttu-id="9e014-115">PolyBase ofrece también una opción de alto rendimiento para cargar los datos.</span><span class="sxs-lookup"><span data-stu-id="9e014-115">PolyBase also provides a high-performance option for loading the data.</span></span> <span data-ttu-id="9e014-116">Sin embargo, eso significa tener que usar dos herramientas en lugar de una.</span><span class="sxs-lookup"><span data-stu-id="9e014-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="9e014-117">Si necesita el mejor rendimiento, use PolyBase.</span><span class="sxs-lookup"><span data-stu-id="9e014-117">If you need the best performance then use PolyBase.</span></span> <span data-ttu-id="9e014-118">Si lo que quiere es una experiencia de una sola herramienta (y los datos no son grandes), ADF es la respuesta.</span><span class="sxs-lookup"><span data-stu-id="9e014-118">If you want a single tool experience (and the data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="9e014-119">Vaya al siguiente artículo para ver algunos excelentes [ejemplos de ADF][ADF samples].</span><span class="sxs-lookup"><span data-stu-id="9e014-119">Head over to the following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="9e014-120">Servicios de integración</span><span class="sxs-lookup"><span data-stu-id="9e014-120">Integration Services</span></span>
<span data-ttu-id="9e014-121">Integration Services (SSIS) es una herramienta eficaz y flexible de extracción, transformación y carga de datos (ETL) que admite varias opciones de carga de datos, flujos de trabajo complejos y transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="9e014-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="9e014-122">Use SSIS para transferir simplemente datos a Azure o como parte de una migración más amplia.</span><span class="sxs-lookup"><span data-stu-id="9e014-122">Use SSIS to simply transfer data to Azure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="9e014-123">SSIS puede exportar a UTF-8 sin la marca BOM en el archivo.</span><span class="sxs-lookup"><span data-stu-id="9e014-123">SSIS can export to UTF-8 without the byte order mark in the file.</span></span> <span data-ttu-id="9e014-124">Para configurar este comportamiento, debe usar primero el componente de columna derivada para convertir los datos de caracteres del flujo de datos para usar la página de códigos 65001 UTF-8.</span><span class="sxs-lookup"><span data-stu-id="9e014-124">To configure this you must first use the derived column component to convert the character data in the data flow to use the 65001 UTF-8 code page.</span></span> <span data-ttu-id="9e014-125">Una vez convertidas las columnas, escriba los datos en el adaptador de destino de archivo plano asegurándose de que 65001 también se ha seleccionado como la página de códigos para el archivo.</span><span class="sxs-lookup"><span data-stu-id="9e014-125">Once the columns have been converted, write the data to the flat file destination adapter ensuring that 65001 has also been selected as the code page for the file.</span></span>
> 
> 

<span data-ttu-id="9e014-126">SSIS se conecta a Almacenamiento de datos SQL del mismo modo que se conectaría a una implementación de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9e014-126">SSIS connects to SQL Data Warehouse just as it would connect to a SQL Server deployment.</span></span> <span data-ttu-id="9e014-127">Sin embargo, las conexiones tendrán que usar un administrador de conexiones de ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="9e014-127">However, your connections will need to be using an ADO.NET connection manager.</span></span> <span data-ttu-id="9e014-128">También debe ocuparse de configurar el ajuste "Usar la inserción masiva cuando esté disponible" para maximizar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="9e014-128">You should also take care to configure the "Use bulk insert when available" setting to maximize throughput.</span></span> <span data-ttu-id="9e014-129">Consulte el artículo [Adaptador de destino de ADO.NET][ADO.NET destination adapter] para obtener más información sobre esta propiedad.</span><span class="sxs-lookup"><span data-stu-id="9e014-129">Please refer to the [ADO.NET destination adapter][ADO.NET destination adapter] article to learn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="9e014-130">No se admite la conexión a Almacenamiento de datos SQL de Azure mediante OLEDB.</span><span class="sxs-lookup"><span data-stu-id="9e014-130">Connecting to Azure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="9e014-131">Además, siempre existe la posibilidad de que se produzcan errores en un paquete por problemas de red o de limitación.</span><span class="sxs-lookup"><span data-stu-id="9e014-131">In addition, there is always the possibility that a package might fail due to throttling or network issues.</span></span> <span data-ttu-id="9e014-132">Diseñe los paquetes de manera que se puedan reanudar en el punto de error, sin tener que rehacer el trabajo que se completó antes del error.</span><span class="sxs-lookup"><span data-stu-id="9e014-132">Design packages so they can be resumed at the point of failure, without redoing work that completed before the failure.</span></span>

<span data-ttu-id="9e014-133">Para obtener más información, consulte la [documentación de SSIS][SSIS documentation].</span><span class="sxs-lookup"><span data-stu-id="9e014-133">For more information consult the [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="9e014-134">bcp</span><span class="sxs-lookup"><span data-stu-id="9e014-134">bcp</span></span>
<span data-ttu-id="9e014-135">bcp es una utilidad de línea de comandos que se ha diseñado para la importación y exportación de datos de archivos planos.</span><span class="sxs-lookup"><span data-stu-id="9e014-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="9e014-136">Puede producirse alguna transformación durante la exportación de datos.</span><span class="sxs-lookup"><span data-stu-id="9e014-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="9e014-137">Si desea realizar transformaciones simples, use una consulta para seleccionar y transformar los datos.</span><span class="sxs-lookup"><span data-stu-id="9e014-137">To perform simple transformations use a query to select and transform the data.</span></span> <span data-ttu-id="9e014-138">Una vez exportados, los archivos planos pueden cargarse directamente en el destino de la base de datos de Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="9e014-138">Once exported, the flat files can then be loaded directly into the target the SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="9e014-139">A menudo resulta una buena idea encapsular las transformaciones usadas durante la exportación de datos en una vista en el sistema de origen.</span><span class="sxs-lookup"><span data-stu-id="9e014-139">It is often a good idea to encapsulate the transformations used during data export in a view on the source system.</span></span> <span data-ttu-id="9e014-140">Con ello se garantiza que la lógica se conserva y el proceso se puede repetir.</span><span class="sxs-lookup"><span data-stu-id="9e014-140">This ensures that the logic is retained and the process is repeatable.</span></span>
> 
> 

<span data-ttu-id="9e014-141">Las ventajas de bcp son:</span><span class="sxs-lookup"><span data-stu-id="9e014-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="9e014-142">Simplicidad.</span><span class="sxs-lookup"><span data-stu-id="9e014-142">Simplicity.</span></span> <span data-ttu-id="9e014-143">Los comandos de bcp son fáciles de generar y ejecutar</span><span class="sxs-lookup"><span data-stu-id="9e014-143">bcp commands are simple to build and execute</span></span>
* <span data-ttu-id="9e014-144">Proceso de carga reiniciable.</span><span class="sxs-lookup"><span data-stu-id="9e014-144">Re-startable load process.</span></span> <span data-ttu-id="9e014-145">Una vez exportada, la carga se puede ejecutar un número ilimitado de veces</span><span class="sxs-lookup"><span data-stu-id="9e014-145">Once exported the load can be executed any number of times</span></span>

<span data-ttu-id="9e014-146">Las limitaciones de bcp son:</span><span class="sxs-lookup"><span data-stu-id="9e014-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="9e014-147">bcp solo funciona con archivos planos tabulados.</span><span class="sxs-lookup"><span data-stu-id="9e014-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="9e014-148">No funciona con archivos, como xml o JSON.</span><span class="sxs-lookup"><span data-stu-id="9e014-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="9e014-149">Las capacidades de transformación de datos se limitan solo a la fase de exportación y son en esencia sencillas.</span><span class="sxs-lookup"><span data-stu-id="9e014-149">Data transformation capabilities are limited to the export stage only and are simple in nature</span></span>
* <span data-ttu-id="9e014-150">bcp no está adaptado para que sea sólido al cargar datos a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="9e014-150">bcp has not been adapted to be robust when loading data over the internet.</span></span> <span data-ttu-id="9e014-151">Cualquier inestabilidad en la red puede provocar un error de carga.</span><span class="sxs-lookup"><span data-stu-id="9e014-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="9e014-152">bcp se basa en el esquema existente en la base de datos de destino antes de la carga.</span><span class="sxs-lookup"><span data-stu-id="9e014-152">bcp relies on the schema being present in the target database prior to the load</span></span>

<span data-ttu-id="9e014-153">Para obtener más información, vea [Uso de bcp para cargar datos en Almacenamiento de datos SQL][Use bcp to load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="9e014-153">For more information, see [Use bcp to load data into SQL Data Warehouse][Use bcp to load data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="9e014-154">Optimización de migración de datos</span><span class="sxs-lookup"><span data-stu-id="9e014-154">Optimizing data migration</span></span>
<span data-ttu-id="9e014-155">Un proceso de migración de datos SQLDW puede dividirse eficazmente en tres pasos independientes:</span><span class="sxs-lookup"><span data-stu-id="9e014-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="9e014-156">Exportación de datos de origen</span><span class="sxs-lookup"><span data-stu-id="9e014-156">Export of source data</span></span>
2. <span data-ttu-id="9e014-157">Transferencia de datos en Azure</span><span class="sxs-lookup"><span data-stu-id="9e014-157">Transfer of data to Azure</span></span>
3. <span data-ttu-id="9e014-158">Carga en la base de datos de destino SQLDW</span><span class="sxs-lookup"><span data-stu-id="9e014-158">Load into the target SQLDW database</span></span>

<span data-ttu-id="9e014-159">Cada paso puede optimizarse individualmente para crear un proceso de migración eficaz, reiniciable y resistente que maximiza el rendimiento en cada paso.</span><span class="sxs-lookup"><span data-stu-id="9e014-159">Each step can be individually optimized to create a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="9e014-160">Optimización de carga de datos</span><span class="sxs-lookup"><span data-stu-id="9e014-160">Optimizing data load</span></span>
<span data-ttu-id="9e014-161">Si miramos esto en orden inverso por un momento, la forma más rápida de cargar datos resulta ser a través de PolyBase.</span><span class="sxs-lookup"><span data-stu-id="9e014-161">Looking at these in reverse order for a moment; the fastest way to load data is via PolyBase.</span></span> <span data-ttu-id="9e014-162">La optimización de un proceso de carga de PolyBase impone requisitos previos en los pasos anteriores, por lo que conviene comprender esto por adelantado.</span><span class="sxs-lookup"><span data-stu-id="9e014-162">Optimizing for a PolyBase load process places prerequisites on the preceding steps so it's best to understand this upfront.</span></span> <span data-ttu-id="9e014-163">Son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="9e014-163">They are:</span></span>

1. <span data-ttu-id="9e014-164">Codificación de archivos de datos</span><span class="sxs-lookup"><span data-stu-id="9e014-164">Encoding of data files</span></span>
2. <span data-ttu-id="9e014-165">Formato de archivos de datos</span><span class="sxs-lookup"><span data-stu-id="9e014-165">Format of data files</span></span>
3. <span data-ttu-id="9e014-166">Ubicación de archivos de datos</span><span class="sxs-lookup"><span data-stu-id="9e014-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="9e014-167">Codificación</span><span class="sxs-lookup"><span data-stu-id="9e014-167">Encoding</span></span>
<span data-ttu-id="9e014-168">PolyBase requiere que los archivos de datos estén codificados en UTF-8 o UTF-16FE.</span><span class="sxs-lookup"><span data-stu-id="9e014-168">PolyBase requires data files to be UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="9e014-169">Formato de archivos de datos</span><span class="sxs-lookup"><span data-stu-id="9e014-169">Format of data files</span></span>
<span data-ttu-id="9e014-170">PolyBase exige un terminador de fila fijo de \n o una línea nueva.</span><span class="sxs-lookup"><span data-stu-id="9e014-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="9e014-171">Los archivos de datos deben seguir este estándar.</span><span class="sxs-lookup"><span data-stu-id="9e014-171">Your data files must conform to this standard.</span></span> <span data-ttu-id="9e014-172">No hay ninguna restricción sobre terminadores de columna o de cadena.</span><span class="sxs-lookup"><span data-stu-id="9e014-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="9e014-173">Debe definir todas las columnas del archivo como parte de la tabla externa de PolyBase.</span><span class="sxs-lookup"><span data-stu-id="9e014-173">You will have to define every column in the file as part of your external table in PolyBase.</span></span> <span data-ttu-id="9e014-174">Asegúrese de que todas las columnas exportadas son necesarias y los tipos se ajustan a los estándares necesarios.</span><span class="sxs-lookup"><span data-stu-id="9e014-174">Make sure that all exported columns are required and that the types conform to the required standards.</span></span>

<span data-ttu-id="9e014-175">Vuelva a consultar el artículo [migración del esquema] para obtener información detallada sobre los tipos de datos admitidos.</span><span class="sxs-lookup"><span data-stu-id="9e014-175">Please refer back to the [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="9e014-176">Ubicación de archivos de datos</span><span class="sxs-lookup"><span data-stu-id="9e014-176">Location of data files</span></span>
<span data-ttu-id="9e014-177">Almacenamiento de datos SQL usa PolyBase para cargar exclusivamente datos del Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e014-177">SQL Data Warehouse uses PolyBase to load data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="9e014-178">Por consiguiente, los datos deben transferirse primero al almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="9e014-178">Consequently, the data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="9e014-179">Optimización de transferencia de datos</span><span class="sxs-lookup"><span data-stu-id="9e014-179">Optimizing data transfer</span></span>
<span data-ttu-id="9e014-180">Una de las partes más lentas de la migración de datos es la transferencia de los datos en Azure.</span><span class="sxs-lookup"><span data-stu-id="9e014-180">One of the slowest parts of data migration is the transfer of the data to Azure.</span></span> <span data-ttu-id="9e014-181">No solo el ancho de banda de red puede ser un problema, sino que la confiabilidad de la red también puede dificultar seriamente el progreso.</span><span class="sxs-lookup"><span data-stu-id="9e014-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="9e014-182">De forma predeterminada, la migración de datos a Azure se realiza a través de Internet, por lo que es bastante probable que se produzcan errores de transferencia.</span><span class="sxs-lookup"><span data-stu-id="9e014-182">By default migrating data to Azure is over the internet so the chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="9e014-183">Sin embargo, puede que estos errores requieran que los datos se vuelvan a enviar en su totalidad o en parte.</span><span class="sxs-lookup"><span data-stu-id="9e014-183">However, these errors may require data to be re-sent either in whole or in part.</span></span>

<span data-ttu-id="9e014-184">Afortunadamente se cuenta con varias opciones para mejorar la velocidad y la resistencia de este proceso:</span><span class="sxs-lookup"><span data-stu-id="9e014-184">Fortunately you have several options to improve the speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="9e014-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="9e014-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="9e014-186">Es aconsejable considerar el uso de [ExpressRoute][ExpressRoute] para acelerar la transferencia.</span><span class="sxs-lookup"><span data-stu-id="9e014-186">You may want to consider using [ExpressRoute][ExpressRoute] to speed up the transfer.</span></span> <span data-ttu-id="9e014-187">[ExpressRoute][ExpressRoute] le proporcionará una conexión privada establecida en Azure para que la conexión no vaya por la red pública de Internet.</span><span class="sxs-lookup"><span data-stu-id="9e014-187">[ExpressRoute][ExpressRoute] provides you with an established private connection to Azure so the connection does not go over the public internet.</span></span> <span data-ttu-id="9e014-188">No se trata en ningún caso de un paso obligatorio.</span><span class="sxs-lookup"><span data-stu-id="9e014-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="9e014-189">Sin embargo, mejorará el rendimiento al insertar datos en Azure desde una instalación local o de ubicación compartida.</span><span class="sxs-lookup"><span data-stu-id="9e014-189">However, it will improve throughput when pushing data to Azure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="9e014-190">Las ventajas de usar [ExpressRoute][ExpressRoute] son:</span><span class="sxs-lookup"><span data-stu-id="9e014-190">The benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="9e014-191">Mayor confiabilidad</span><span class="sxs-lookup"><span data-stu-id="9e014-191">Increased reliability</span></span>
2. <span data-ttu-id="9e014-192">Mayor velocidad de red</span><span class="sxs-lookup"><span data-stu-id="9e014-192">Faster network speed</span></span>
3. <span data-ttu-id="9e014-193">Menor latencia de red</span><span class="sxs-lookup"><span data-stu-id="9e014-193">Lower network latency</span></span>
4. <span data-ttu-id="9e014-194">Mayor seguridad de red</span><span class="sxs-lookup"><span data-stu-id="9e014-194">higher network security</span></span>

<span data-ttu-id="9e014-195">[ExpressRoute][ExpressRoute] resulta útil en una serie de escenarios; no solo la migración.</span><span class="sxs-lookup"><span data-stu-id="9e014-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just the migration.</span></span>

<span data-ttu-id="9e014-196">¿Le interesa?</span><span class="sxs-lookup"><span data-stu-id="9e014-196">Interested?</span></span> <span data-ttu-id="9e014-197">Para obtener más información y precios, visite la [documentación de ExpressRoute][ExpressRoute documentation].</span><span class="sxs-lookup"><span data-stu-id="9e014-197">For more information and pricing please visit the [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="9e014-198">Servicio Importación/Exportación de Azure</span><span class="sxs-lookup"><span data-stu-id="9e014-198">Azure Import and Export Service</span></span>
<span data-ttu-id="9e014-199">El Servicio Importación/Exportación de Azure es un proceso de transferencia de datos diseñado para transferencias de datos de gran tamaño (GB++) a masivas (TB++) en Azure.</span><span class="sxs-lookup"><span data-stu-id="9e014-199">The Azure Import and Export Service is a data transfer process designed for large (GB++) to massive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="9e014-200">Implica escribir los datos en los discos y enviarlos a un centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e014-200">It involves writing your data to disks and shipping them to an Azure data center.</span></span> <span data-ttu-id="9e014-201">El contenido del disco se cargará después automáticamente en Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="9e014-201">The disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="9e014-202">A continuación, se ofrece una vista general del proceso de importación y exportación:</span><span class="sxs-lookup"><span data-stu-id="9e014-202">A high-level view of the import export process is as follows:</span></span>

1. <span data-ttu-id="9e014-203">Configurar un contenedor de Almacenamiento de blobs de Azure para recibir los datos</span><span class="sxs-lookup"><span data-stu-id="9e014-203">Configure an Azure Blob Storage container to receive the data</span></span>
2. <span data-ttu-id="9e014-204">Exportar los datos al almacenamiento local</span><span class="sxs-lookup"><span data-stu-id="9e014-204">Export your data to local storage</span></span>
3. <span data-ttu-id="9e014-205">Copiar los datos en unidades de disco duro de 3,5 pulgadas SATA II/III con la [herramienta Importación/Exportación de Azure]</span><span class="sxs-lookup"><span data-stu-id="9e014-205">Copy the data to 3.5 inch SATA II/III hard disk drives using the [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="9e014-206">Crear un trabajo de importación mediante el Servicio Importación/Exportación de Azure proporcionando los archivos del diario generados por la [herramienta Importación/Exportación de Azure]</span><span class="sxs-lookup"><span data-stu-id="9e014-206">Create an Import Job using the Azure Import and Export Service providing the journal files produced by the [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="9e014-207">Enviar los discos al centro de datos de Azure asignado</span><span class="sxs-lookup"><span data-stu-id="9e014-207">Ship the disks your nominated Azure data center</span></span>
6. <span data-ttu-id="9e014-208">Los datos se transfieren a su contenedor de almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="9e014-208">Your data is transferred to your Azure Blob Storage container</span></span>
7. <span data-ttu-id="9e014-209">Cargar los datos en SQLDW mediante PolyBase</span><span class="sxs-lookup"><span data-stu-id="9e014-209">Load the data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="9e014-210">Utilidad [AZCopy][AZCopy]</span><span class="sxs-lookup"><span data-stu-id="9e014-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="9e014-211">La utilidad [AZCopy][AZCopy] es una excelente herramienta para organizar los datos transferidos a blobs de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9e014-211">The [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="9e014-212">Está diseñado para transferencias de datos de pequeño tamaño (MB++) a muy grandes (GB++).</span><span class="sxs-lookup"><span data-stu-id="9e014-212">It is designed for small (MB++) to very large (GB++) data transfers.</span></span> <span data-ttu-id="9e014-213">[AZCopy] también se ha diseñado para proporcionar buen rendimiento resistente al transferir datos a Azure, por lo que es una excelente opción para el paso de transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="9e014-213">[AZCopy] has also been designed to provide good resilient throughput when transferring data to Azure and so is a great choice for the data transfer step.</span></span> <span data-ttu-id="9e014-214">Una vez transferidos, puede cargar los datos con PolyBase en Almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="9e014-214">Once transferred you can load the data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="9e014-215">También puede incorporar AZCopy a los paquetes SSIS con una tarea "Ejecutar proceso".</span><span class="sxs-lookup"><span data-stu-id="9e014-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="9e014-216">Para usar AZCopy, debe primero descargarlo e instalarlo.</span><span class="sxs-lookup"><span data-stu-id="9e014-216">To use AZCopy you will first need to download and install it.</span></span> <span data-ttu-id="9e014-217">Hay una [versión de producción][production version] y una [versión preliminar][preview version] disponibles.</span><span class="sxs-lookup"><span data-stu-id="9e014-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="9e014-218">Para cargar un archivo desde su sistema de archivos, necesitará un comando como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="9e014-218">To upload a file from your file system you will need a command like the one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="9e014-219">Un resumen del proceso general podría ser:</span><span class="sxs-lookup"><span data-stu-id="9e014-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="9e014-220">Configurar un contenedor de blobs de almacenamiento de Azure para recibir los datos</span><span class="sxs-lookup"><span data-stu-id="9e014-220">Configure an Azure storage blob container to receive the data</span></span>
2. <span data-ttu-id="9e014-221">Exportar los datos al almacenamiento local</span><span class="sxs-lookup"><span data-stu-id="9e014-221">Export your data to local storage</span></span>
3. <span data-ttu-id="9e014-222">AZCopy copia los datos en el contenedor de almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="9e014-222">AZCopy your data in the Azure Blob Storage container</span></span>
4. <span data-ttu-id="9e014-223">Cargar los datos con PolyBase en Almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="9e014-223">Load the data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="9e014-224">Documentación completa disponible: [AZCopy][AZCopy].</span><span class="sxs-lookup"><span data-stu-id="9e014-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="9e014-225">Optimización de exportación de datos</span><span class="sxs-lookup"><span data-stu-id="9e014-225">Optimizing data export</span></span>
<span data-ttu-id="9e014-226">Además de asegurarse de que la exportación se ajusta a los requisitos de PolyBase, también puede tratar de optimizar la exportación de datos para mejorar aún más el proceso.</span><span class="sxs-lookup"><span data-stu-id="9e014-226">In addition to ensuring that the export conforms to the requirements laid out by PolyBase you can also seek to optimize the export of the data to improve the process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="9e014-227">Compresión de datos</span><span class="sxs-lookup"><span data-stu-id="9e014-227">Data compression</span></span>
<span data-ttu-id="9e014-228">PolyBase puede leer datos comprimidos con gzip.</span><span class="sxs-lookup"><span data-stu-id="9e014-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="9e014-229">Si puede comprimir los datos en archivos gzip, minimizará la cantidad de datos que se transmite por la red.</span><span class="sxs-lookup"><span data-stu-id="9e014-229">If you are able to compress your data to gzip files then you will minimize the amount of data being pushed over the network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="9e014-230">Varios archivos</span><span class="sxs-lookup"><span data-stu-id="9e014-230">Multiple files</span></span>
<span data-ttu-id="9e014-231">La división de tablas grandes en varios archivos no solo ayuda a mejorar la velocidad de exportación, sino que también contribuye a la posibilidad de reiniciar la transferencia y a la facilidad de uso general de los datos una vez se encuentren en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e014-231">Breaking up large tables into several files not only helps to improve export speed, it also helps with transfer re-startability, and the overall manageability of the data once in the Azure blob storage.</span></span> <span data-ttu-id="9e014-232">Una de las muchas características útiles de PolyBase es que leerá todos los archivos contenidos en una carpeta y los tratará como una sola tabla.</span><span class="sxs-lookup"><span data-stu-id="9e014-232">One of the many nice features of PolyBase is that it will read all the files inside a folder and treat it as one table.</span></span> <span data-ttu-id="9e014-233">Por lo tanto, conviene aislar los archivos de cada tabla en su propia carpeta.</span><span class="sxs-lookup"><span data-stu-id="9e014-233">It is therefore a good idea to isolate the files for each table into its own folder.</span></span>

<span data-ttu-id="9e014-234">PolyBase también admite una característica conocida como "cruce de carpetas recursivo".</span><span class="sxs-lookup"><span data-stu-id="9e014-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="9e014-235">Puede usar esta característica para mejorar aún más la organización de los datos exportados a fin de mejorar la administración de datos.</span><span class="sxs-lookup"><span data-stu-id="9e014-235">You can use this feature to further enhance the organization of your exported data to improve your data management.</span></span>

<span data-ttu-id="9e014-236">Para obtener más información sobre la carga de datos con PolyBase, vea [Uso de PolyBase para cargar datos en Almacenamiento de datos SQL][Use PolyBase to load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="9e014-236">To learn more about loading data with PolyBase, see [Use PolyBase to load data into SQL Data Warehouse][Use PolyBase to load data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e014-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9e014-237">Next steps</span></span>
<span data-ttu-id="9e014-238">Para obtener más información sobre la migración, vea [Migración de la solución a Almacenamiento de datos SQL][Migrate your solution to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="9e014-238">For more about migration, see [Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse].</span></span>
<span data-ttu-id="9e014-239">Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].</span><span class="sxs-lookup"><span data-stu-id="9e014-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution to SQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp to load data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase to load data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
