---
title: Copia de datos con Oracle como origen o destino mediante Data Factory | Microsoft Docs
description: Aprenda a copiar datos con una base de datos de Oracle local como origen o destino mediante Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: bb6af719fe6f1a30c5933ce4342a4c0c072f3ff4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="26083-103">Copia de datos con una instancia local Oracle como origen o destino mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="26083-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="26083-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para mover datos con una base de datos de Oracle local como origen o destino.</span><span class="sxs-lookup"><span data-stu-id="26083-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="26083-105">Se basa en la información general ofrecida en el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="26083-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="26083-106">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="26083-106">Supported scenarios</span></span>
<span data-ttu-id="26083-107">Puede copiar datos **de una base de datos de Oracle** a los siguientes almacenes de datos:</span><span class="sxs-lookup"><span data-stu-id="26083-107">You can copy data **from an Oracle database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="26083-108">Puede copiar datos de los siguientes almacenes de datos **a una base de datos de Oracle**:</span><span class="sxs-lookup"><span data-stu-id="26083-108">You can copy data from the following data stores **to an Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="26083-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="26083-109">Prerequisites</span></span>
<span data-ttu-id="26083-110">Data Factory admite la conexión a orígenes de Oracle locales mediante la puerta de enlace de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="26083-110">Data Factory supports connecting to on-premises Oracle sources using the Data Management Gateway.</span></span> <span data-ttu-id="26083-111">Consulte el artículo [Data Management Gateway](data-factory-data-management-gateway.md) para más información acerca de la puerta de enlace de administración de datos y el artículo [Movimiento de datos entre orígenes locales y la nube con la puerta de enlace de administración de datos](data-factory-move-data-between-onprem-and-cloud.md) para obtener instrucciones detalladas sobre cómo configurar la puerta de enlace de una canalización de datos para mover los datos.</span><span class="sxs-lookup"><span data-stu-id="26083-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article to learn about Data Management Gateway and [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="26083-112">La puerta de enlace es necesaria incluso si Oracle está hospedado en una máquina virtual de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="26083-112">Gateway is required even if the Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="26083-113">Puede instalar la puerta de enlace en la misma máquina virtual de IaaS como almacén de datos o en una máquina virtual diferente, siempre y cuando la puerta de enlace se pueda conectar a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="26083-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="26083-114">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="26083-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="26083-115">Versiones compatibles e instalación</span><span class="sxs-lookup"><span data-stu-id="26083-115">Supported versions and installation</span></span>
<span data-ttu-id="26083-116">Este conector de Oracle admite dos versiones de controladores:</span><span class="sxs-lookup"><span data-stu-id="26083-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="26083-117">**Controlador de Microsoft para Oracle (recomendado)**: a partir de Data Management Gateway versión 2.7, un controlador de Microsoft para Oracle se instala automáticamente junto con la puerta de enlace, por lo que no será necesario realizar ningún control adicional en el controlador para establecer la conectividad con Oracle y podrá también experimentar un mejor rendimiento de copia mediante este controlador.</span><span class="sxs-lookup"><span data-stu-id="26083-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with the gateway, so you don't need to additionally handle the driver in order to establish connectivity to Oracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="26083-118">Se admiten las siguientes versiones de bases de datos de Oracle:</span><span class="sxs-lookup"><span data-stu-id="26083-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="26083-119">Oracle 12c R1 (12.1)</span><span class="sxs-lookup"><span data-stu-id="26083-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="26083-120">Oracle 11g R1, R2 (11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="26083-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="26083-121">Oracle 10g R1, R2 (10.1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="26083-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="26083-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="26083-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="26083-123">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="26083-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26083-124">Actualmente, el controlador de Microsoft para Oracle solo permite copiar datos de Oracle, pero no escribir en Oracle.</span><span class="sxs-lookup"><span data-stu-id="26083-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing to Oracle.</span></span> <span data-ttu-id="26083-125">Y tenga en cuenta que la funcionalidad de conexión de prueba de la pestaña Diagnósticos de Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="26083-125">And note the test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="26083-126">Como alternativa, puede usar al Asistente para copiar para validar la conectividad.</span><span class="sxs-lookup"><span data-stu-id="26083-126">Alternatively, you can use the copy wizard to validate the connectivity.</span></span>
>

- <span data-ttu-id="26083-127">**Proveedor de datos de Oracle para. NET:** también es posible usar el proveedor de datos de Oracle para copiar datos desde Oracle o en Oracle.</span><span class="sxs-lookup"><span data-stu-id="26083-127">**Oracle Data Provider for .NET:** you can also choose to use Oracle Data Provider to copy data from/to Oracle.</span></span> <span data-ttu-id="26083-128">Este componente se incluye en [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/) (Componentes de acceso a datos Oracle para Windows).</span><span class="sxs-lookup"><span data-stu-id="26083-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="26083-129">Instale la versión adecuada (32/64 bits) en la máquina en la que está instalada la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="26083-129">Install the appropriate version (32/64 bit) on the machine where the gateway is installed.</span></span> <span data-ttu-id="26083-130">[Proveedor de datos de Oracle para NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) puede tener acceso a bases de datos Oracle 10g Release 2 o posterior.</span><span class="sxs-lookup"><span data-stu-id="26083-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access to Oracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="26083-131">Si elige XCopy Installation (Instalación de XCopy), siga los pasos del archivo readme.htm.</span><span class="sxs-lookup"><span data-stu-id="26083-131">If you choose “XCopy Installation”, follow steps in the readme.htm.</span></span> <span data-ttu-id="26083-132">Se recomienda elegir el programa de instalación con la interfaz de usuario (no puede ser una de XCopy).</span><span class="sxs-lookup"><span data-stu-id="26083-132">We recommend you choose the installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="26083-133">Después de instalar el proveedor, **reinicie** el servicio de host de la puerta de enlace de administración de datos en la máquina con el applet Servicios o el Administrador de configuración de la puerta de enlace de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="26083-133">After installing the provider, **restart** the Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="26083-134">Si utiliza el asistente para copia para crear la canalización de copia, el tipo de controlador se determinará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="26083-134">If you use copy wizard to author the copy pipeline, the driver type will be auto-determined.</span></span> <span data-ttu-id="26083-135">El controlador de Microsoft se usará de forma predeterminada, a menos que la versión de la puerta de enlace sea inferior a 2.7 o elija Oracle como receptor.</span><span class="sxs-lookup"><span data-stu-id="26083-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="26083-136">Introducción</span><span class="sxs-lookup"><span data-stu-id="26083-136">Getting started</span></span>
<span data-ttu-id="26083-137">Puede crear una canalización con una actividad de copia que mueva datos desde una base de datos de Oracle local o hacia ella mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="26083-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="26083-138">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="26083-138">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="26083-139">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="26083-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="26083-140">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="26083-140">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="26083-141">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="26083-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="26083-142">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="26083-142">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="26083-143">Crear una **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="26083-143">Create a **data factory**.</span></span> <span data-ttu-id="26083-144">Una factoría de datos puede contener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="26083-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="26083-145">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="26083-145">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="26083-146">Por ejemplo, si copia datos de una base de datos de Oracle a Azure Blob Storage, crea dos servicios vinculados para vincular la base de datos de Oracle y la cuenta de Azure Storage a su factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="26083-146">For example, if you are copying data from an Oralce database to an Azure blob storage, you create two linked services to link your Oracle database and Azure storage account to your data factory.</span></span> <span data-ttu-id="26083-147">Para conocer las propiedades de los servicios vinculados que son específicas de Oracle, consulte la sección [Propiedades del servicio vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="26083-147">For linked service properties that are specific to Oracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="26083-148">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="26083-148">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="26083-149">En el ejemplo mencionado en el último paso, cree un conjunto de datos para especificar la tabla de la base de datos de Oracle que contiene los datos de entrada.</span><span class="sxs-lookup"><span data-stu-id="26083-149">In the example mentioned in the last step, you create a dataset to specify the table in your Oracle database that contains the input data.</span></span> <span data-ttu-id="26083-150">Cree también otro conjunto de datos para especificar el contenedor de blobs y la carpeta que contiene los datos copiados de la base de datos de Oracle.</span><span class="sxs-lookup"><span data-stu-id="26083-150">And, you create another dataset to specify the blob container and the folder that holds the data copied from the Oracle database.</span></span> <span data-ttu-id="26083-151">Para conocer las propiedades del conjunto de datos que son específicas de Oracle, consulte la sección [Propiedades del conjunto de datos](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="26083-151">For dataset properties that are specific to Oracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="26083-152">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="26083-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="26083-153">En el ejemplo mencionado anteriormente, se usa OracleSource como origen y BlobSink como receptor para la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="26083-153">In the example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="26083-154">De igual forma, si realiza la copia de Azure Blob Storage a Oracle Database, usa BlobSource y OracleSink en la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="26083-154">Similarly, if you are copying from Azure Blob Storage to Oracle Database, you use BlobSource and OracleSink in the copy activity.</span></span> <span data-ttu-id="26083-155">Para conocer las propiedades de la actividad de copia que son específicas de la base de datos de Oracle, consulte la sección [Propiedades de la actividad de copia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="26083-155">For copy activity properties that are specific to Oracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="26083-156">Para obtener más información sobre cómo usar un almacén de datos como origen o receptor, haga clic en el vínculo de la sección anterior para el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="26083-156">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="26083-157">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="26083-157">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="26083-158">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="26083-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="26083-159">Para ver ejemplos con definiciones de JSON de entidades de Data Factory que se usan para copiar datos a una base de datos de Oracle local o desde ella, consulte la sección [Ejemplos de JSON](#json-examples-for-copying-data-to-and-from-oracle-database) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="26083-159">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="26083-160">Las secciones siguientes proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory:</span><span class="sxs-lookup"><span data-stu-id="26083-160">The following sections provide details about JSON properties that are used to define Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="26083-161">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="26083-161">Linked service properties</span></span>
<span data-ttu-id="26083-162">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos al servicio vinculado de Oracle.</span><span class="sxs-lookup"><span data-stu-id="26083-162">The following table provides description for JSON elements specific to Oracle linked service.</span></span>

| <span data-ttu-id="26083-163">Propiedad</span><span class="sxs-lookup"><span data-stu-id="26083-163">Property</span></span> | <span data-ttu-id="26083-164">Descripción</span><span class="sxs-lookup"><span data-stu-id="26083-164">Description</span></span> | <span data-ttu-id="26083-165">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="26083-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="26083-166">type</span><span class="sxs-lookup"><span data-stu-id="26083-166">type</span></span> |<span data-ttu-id="26083-167">La propiedad type debe establecerse en: **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="26083-167">The type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="26083-168">Sí</span><span class="sxs-lookup"><span data-stu-id="26083-168">Yes</span></span> |
| <span data-ttu-id="26083-169">driverType</span><span class="sxs-lookup"><span data-stu-id="26083-169">driverType</span></span> | <span data-ttu-id="26083-170">Especifique qué controlador usar para copiar datos en bases de datos de Oracle o desde ellas.</span><span class="sxs-lookup"><span data-stu-id="26083-170">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="26083-171">Los valores permitidos son **Microsoft** u **ODP** (valor predeterminado).</span><span class="sxs-lookup"><span data-stu-id="26083-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="26083-172">Consulte la sección [Versiones compatibles e instalación](#supported-versions-and-installation) para obtener información detallada sobre los controladores.</span><span class="sxs-lookup"><span data-stu-id="26083-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="26083-173">No</span><span class="sxs-lookup"><span data-stu-id="26083-173">No</span></span> |
| <span data-ttu-id="26083-174">connectionString</span><span class="sxs-lookup"><span data-stu-id="26083-174">connectionString</span></span> | <span data-ttu-id="26083-175">Especifique la información necesaria para conectarse a la instancia de Base de datos de Oracle para la propiedad connectionString.</span><span class="sxs-lookup"><span data-stu-id="26083-175">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="26083-176">Sí</span><span class="sxs-lookup"><span data-stu-id="26083-176">Yes</span></span> |
| <span data-ttu-id="26083-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="26083-177">gatewayName</span></span> | <span data-ttu-id="26083-178">Nombre de la puerta de enlace que se usa para conectarse al servidor de Oracle local</span><span class="sxs-lookup"><span data-stu-id="26083-178">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="26083-179">Sí</span><span class="sxs-lookup"><span data-stu-id="26083-179">Yes</span></span> |

<span data-ttu-id="26083-180">**Ejemplo: Uso del controlador de Microsoft**</span><span class="sxs-lookup"><span data-stu-id="26083-180">**Example: using Microsoft driver:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="26083-181">**Ejemplo: uso del controlador de ODP**</span><span class="sxs-lookup"><span data-stu-id="26083-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="26083-182">Consulte [este sitio](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) para conocer los formatos permitidos.</span><span class="sxs-lookup"><span data-stu-id="26083-182">Refer to [this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for the allowed formats.</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="26083-183">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="26083-183">Dataset properties</span></span>
<span data-ttu-id="26083-184">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="26083-184">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="26083-185">Las secciones como structure, availability y policy de un conjunto de datos JSON son similares en todos los tipos de conjunto de datos (Oracle, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="26083-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="26083-186">La sección typeProperties es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="26083-186">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="26083-187">La sección typeProperties del conjunto de datos de tipo OracleTable tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="26083-187">The typeProperties section for the dataset of type OracleTable has the following properties:</span></span>

| <span data-ttu-id="26083-188">Propiedad</span><span class="sxs-lookup"><span data-stu-id="26083-188">Property</span></span> | <span data-ttu-id="26083-189">Descripción</span><span class="sxs-lookup"><span data-stu-id="26083-189">Description</span></span> | <span data-ttu-id="26083-190">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="26083-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="26083-191">tableName</span><span class="sxs-lookup"><span data-stu-id="26083-191">tableName</span></span> |<span data-ttu-id="26083-192">Nombre de la tabla en la instancia de Base de datos de Oracle a la que hace referencia el servicio vinculado.</span><span class="sxs-lookup"><span data-stu-id="26083-192">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="26083-193">No (si se especifica **oracleReaderQuery** de **OracleSource**)</span><span class="sxs-lookup"><span data-stu-id="26083-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="26083-194">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="26083-194">Copy activity properties</span></span>
<span data-ttu-id="26083-195">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="26083-195">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="26083-196">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="26083-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="26083-197">La actividad de copia toma solo una entrada y genera una única salida.</span><span class="sxs-lookup"><span data-stu-id="26083-197">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="26083-198">Por otra parte, las propiedades disponibles en la sección typeProperties de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="26083-198">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="26083-199">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="26083-199">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="26083-200">OracleSource</span><span class="sxs-lookup"><span data-stu-id="26083-200">OracleSource</span></span>
<span data-ttu-id="26083-201">En la actividad de copia, si el origen es de tipo **OracleSource**, están disponibles las propiedades siguientes en la sección **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="26083-201">In Copy activity, when the source is of type **OracleSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="26083-202">Propiedad</span><span class="sxs-lookup"><span data-stu-id="26083-202">Property</span></span> | <span data-ttu-id="26083-203">Descripción</span><span class="sxs-lookup"><span data-stu-id="26083-203">Description</span></span> | <span data-ttu-id="26083-204">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="26083-204">Allowed values</span></span> | <span data-ttu-id="26083-205">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="26083-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="26083-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="26083-206">oracleReaderQuery</span></span> |<span data-ttu-id="26083-207">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="26083-207">Use the custom query to read data.</span></span> |<span data-ttu-id="26083-208">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="26083-208">SQL query string.</span></span> <span data-ttu-id="26083-209">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="26083-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="26083-210">Si no se especifica, la instrucción SQL que se ejecuta es select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="26083-210">If not specified, the SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="26083-211">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="26083-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="26083-212">OracleSink</span><span class="sxs-lookup"><span data-stu-id="26083-212">OracleSink</span></span>
<span data-ttu-id="26083-213">**OracleSink** admite las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="26083-213">**OracleSink** supports the following properties:</span></span>

| <span data-ttu-id="26083-214">Propiedad</span><span class="sxs-lookup"><span data-stu-id="26083-214">Property</span></span> | <span data-ttu-id="26083-215">Descripción</span><span class="sxs-lookup"><span data-stu-id="26083-215">Description</span></span> | <span data-ttu-id="26083-216">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="26083-216">Allowed values</span></span> | <span data-ttu-id="26083-217">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="26083-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="26083-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="26083-218">writeBatchTimeout</span></span> |<span data-ttu-id="26083-219">Tiempo de espera para que la operación de inserción por lotes se complete antes de que se agote el tiempo de espera.</span><span class="sxs-lookup"><span data-stu-id="26083-219">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="26083-220">timespan</span><span class="sxs-lookup"><span data-stu-id="26083-220">timespan</span></span><br/><br/> <span data-ttu-id="26083-221">Ejemplo: 00:30:00 (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="26083-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="26083-222">No</span><span class="sxs-lookup"><span data-stu-id="26083-222">No</span></span> |
| <span data-ttu-id="26083-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="26083-223">writeBatchSize</span></span> |<span data-ttu-id="26083-224">Inserta datos en la tabla SQL cuando el tamaño del búfer alcanza el valor writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="26083-224">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="26083-225">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="26083-225">Integer (number of rows)</span></span> |<span data-ttu-id="26083-226">No (valor predeterminado: 100)</span><span class="sxs-lookup"><span data-stu-id="26083-226">No (default: 100)</span></span> |
| <span data-ttu-id="26083-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="26083-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="26083-228">Especifique una consulta para que se ejecute la actividad de copia de tal forma que se limpien los datos de un segmento específico.</span><span class="sxs-lookup"><span data-stu-id="26083-228">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="26083-229">Una instrucción de consulta.</span><span class="sxs-lookup"><span data-stu-id="26083-229">A query statement.</span></span> |<span data-ttu-id="26083-230">No</span><span class="sxs-lookup"><span data-stu-id="26083-230">No</span></span> |
| <span data-ttu-id="26083-231">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="26083-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="26083-232">Especifique el nombre de columna para que la rellene la actividad de copia con un identificador de segmentos generado automáticamente, que se usará para limpiar los datos de un segmento específico cuando se vuelva a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="26083-232">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="26083-233">Nombre de columna de una columna con el tipo de datos binarios (32).</span><span class="sxs-lookup"><span data-stu-id="26083-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="26083-234">No</span><span class="sxs-lookup"><span data-stu-id="26083-234">No</span></span> |

## <a name="json-examples-for-copying-data-to-and-from-oracle-database"></a><span data-ttu-id="26083-235">Ejemplos de JSON para copiar datos a la base de datos de Oracle y desde esta</span><span class="sxs-lookup"><span data-stu-id="26083-235">JSON examples for copying data to and from Oracle database</span></span>
<span data-ttu-id="26083-236">En el siguiente ejemplo, se proporcionan definiciones JSON de ejemplo que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="26083-236">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="26083-237">Se muestra cómo copiar datos desde una base de datos de Oracle a Azure Blob Storage y viceversa.</span><span class="sxs-lookup"><span data-stu-id="26083-237">They show how to copy data from/to an Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="26083-238">Sin embargo, los datos se pueden copiar en cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="26083-238">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-to-azure-blob"></a><span data-ttu-id="26083-239">Ejemplo: Copia de datos de Oracle a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="26083-239">Example: Copy data from Oracle to Azure Blob</span></span>

<span data-ttu-id="26083-240">El ejemplo consta de las siguientes entidades de factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="26083-240">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="26083-241">Un servicio vinculado de tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="26083-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="26083-242">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="26083-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="26083-243">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="26083-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="26083-244">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="26083-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="26083-245">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) como origen y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) como receptor.</span><span class="sxs-lookup"><span data-stu-id="26083-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="26083-246">En el ejemplo de copian datos de una tabla de una base de datos de Oracle local en un blob cada hora.</span><span class="sxs-lookup"><span data-stu-id="26083-246">The sample copies data from a table in an on-premises Oracle database to a blob hourly.</span></span> <span data-ttu-id="26083-247">Para más información sobre las distintas propiedades usadas en el ejemplo, consulte la documentación de las secciones que vienen a continuación de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="26083-247">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="26083-248">**Servicio vinculado de Oracle:**</span><span class="sxs-lookup"><span data-stu-id="26083-248">**Oracle linked service:**</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="26083-249">**Servicio vinculado Azure Blob Storage:**</span><span class="sxs-lookup"><span data-stu-id="26083-249">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="26083-250">**Conjunto de datos de entrada de Oracle:**</span><span class="sxs-lookup"><span data-stu-id="26083-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="26083-251">El ejemplo supone que ha creado una tabla "MyTable" en Oracle que contiene una columna denominada "timestampcolumn" para los datos de serie temporales.</span><span class="sxs-lookup"><span data-stu-id="26083-251">The sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="26083-252">Si se establece "external": "true", se informa al servicio Data Factory que el conjunto de datos es externo a la factoría de datos y que no lo genera ninguna actividad de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="26083-252">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {     
            "externalData": {        
                "retryInterval": "00:01:00",    
                "retryTimeout": "00:10:00",       
                "maximumRetry": 3       
            }     
        }
    }
}
```

<span data-ttu-id="26083-253">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="26083-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="26083-254">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="26083-254">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="26083-255">La ruta de acceso de la carpeta y el nombre de archivo para el blob se evalúan dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="26083-255">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="26083-256">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="26083-256">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ],
            "format": {
                "type": "TextFormat",
                "columnDelimiter": "\t",
                "rowDelimiter": "\n"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="26083-257">**Canalización con actividad de copia:**</span><span class="sxs-lookup"><span data-stu-id="26083-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="26083-258">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="26083-258">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="26083-259">En la definición de JSON de canalización, el tipo **source** se establece en **OracleSource** y el tipo **sink**, en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="26083-259">In the pipeline JSON definition, the **source** type is set to **OracleSource** and **sink** type is set to **BlobSink**.</span></span>  <span data-ttu-id="26083-260">La consulta SQL especificada para la propiedad **oracleReaderQuery** selecciona los datos de la última hora que se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="26083-260">The SQL query specified with **oracleReaderQuery** property selects the data in the past hour to copy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "OldestFirst",
                    "retry": 0,
                    "timeout": "01:00:00"
                }
            }
        ]
    }
}
```

## <a name="example-copy-data-from-azure-blob-to-oracle"></a><span data-ttu-id="26083-261">Ejemplo: Copia de datos de un blob de Azure a Oracle</span><span class="sxs-lookup"><span data-stu-id="26083-261">Example: Copy data from Azure Blob to Oracle</span></span>
<span data-ttu-id="26083-262">En este ejemplo se muestra cómo se copian datos de Azure Blob Storage a una base de datos Oracle local.</span><span class="sxs-lookup"><span data-stu-id="26083-262">This sample shows how to copy data from an Azure Blob Storage to an on-premises Oracle database.</span></span> <span data-ttu-id="26083-263">Sin embargo, se pueden copiar datos **directamente** desde cualquiera de los orígenes indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia de Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="26083-263">However, data can be copied **directly** from any of the sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="26083-264">El ejemplo consta de las siguientes entidades de factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="26083-264">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="26083-265">Un servicio vinculado de tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="26083-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="26083-266">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="26083-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="26083-267">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="26083-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="26083-268">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="26083-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="26083-269">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) como origen y [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) como receptor.</span><span class="sxs-lookup"><span data-stu-id="26083-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="26083-270">El ejemplo copia datos de un blob a una tabla de una base de datos de Oracle local cada hora.</span><span class="sxs-lookup"><span data-stu-id="26083-270">The sample copies data from a blob to a table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="26083-271">Para más información sobre las distintas propiedades usadas en el ejemplo, consulte la documentación de las secciones que vienen a continuación de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="26083-271">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="26083-272">**Servicio vinculado de Oracle:**</span><span class="sxs-lookup"><span data-stu-id="26083-272">**Oracle linked service:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="26083-273">**Servicio vinculado Azure Blob Storage:**</span><span class="sxs-lookup"><span data-stu-id="26083-273">**Azure Blob storage linked service:**</span></span>
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="26083-274">**Conjunto de datos de entrada de blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="26083-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="26083-275">Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="26083-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="26083-276">La ruta de acceso de la carpeta y el nombre de archivo para el blob se evalúan dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="26083-276">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="26083-277">La ruta de acceso de la carpeta usa la parte year, month y day de la hora de inicio y el nombre de archivo, la parte hour.</span><span class="sxs-lookup"><span data-stu-id="26083-277">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="26083-278">El valor "external": "true" informa al servicio Data Factory que esta tabla es externa a la factoría de datos y no la produce una actividad de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="26083-278">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                }
            ],
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="26083-279">**Conjunto de datos de salida de Oracle:**</span><span class="sxs-lookup"><span data-stu-id="26083-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="26083-280">En el ejemplo se supone que ha creado una tabla "MyTable" en Oracle.</span><span class="sxs-lookup"><span data-stu-id="26083-280">The sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="26083-281">Cree la tabla en Oracle con el mismo número de columnas que espera que contenga el archivo CSV de Blob.</span><span class="sxs-lookup"><span data-stu-id="26083-281">Create the table in Oracle with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="26083-282">Se agregan nuevas filas a la tabla cada hora.</span><span class="sxs-lookup"><span data-stu-id="26083-282">New rows are added to the table every hour.</span></span>

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

<span data-ttu-id="26083-283">**Canalización con actividad de copia:**</span><span class="sxs-lookup"><span data-stu-id="26083-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="26083-284">La canalización contiene una actividad de copia que está configurada para usar los conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="26083-284">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="26083-285">En la definición de JSON de canalización, el tipo **source** se establece en **BlobSource** y el tipo **sink**, en **OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="26083-285">In the pipeline JSON definition, the **source** type is set to **BlobSource** and the **sink** type is set to **OracleSink**.</span></span>  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "OldestFirst",
                    "retry": 0,
                    "timeout": "01:00:00"
                }
            }
        ]
    }
}
```


## <a name="troubleshooting-tips"></a><span data-ttu-id="26083-286">Sugerencias de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="26083-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="26083-287">Problema 1: proveedor de datos .NET Framework</span><span class="sxs-lookup"><span data-stu-id="26083-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="26083-288">Se muestra el siguiente **mensaje de error**:</span><span class="sxs-lookup"><span data-stu-id="26083-288">You see the following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable to find the requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="26083-289">**Causas posibles:**</span><span class="sxs-lookup"><span data-stu-id="26083-289">**Possible causes:**</span></span>

1. <span data-ttu-id="26083-290">No se instaló el proveedor de datos de .NET Framework para Oracle.</span><span class="sxs-lookup"><span data-stu-id="26083-290">The .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="26083-291">El proveedor de datos de .NET Framework para Oracle se instaló en .NET Framework 2.0 y no se encuentra en las carpetas de .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="26083-291">The .NET Framework Data Provider for Oracle was installed to .NET Framework 2.0 and is not found in the .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="26083-292">**Resolución o solución alternativa:**</span><span class="sxs-lookup"><span data-stu-id="26083-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="26083-293">Si no ha instalado el proveedor de .NET para Oracle, [instálelo](http://www.oracle.com/technetwork/topics/dotnet/downloads/) e intente de nuevo este escenario.</span><span class="sxs-lookup"><span data-stu-id="26083-293">If you haven't installed the .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry the scenario.</span></span>
2. <span data-ttu-id="26083-294">Si recibe el mensaje de error incluso después de instalar el proveedor, lleve a cabo los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="26083-294">If you get the error message even after installing the provider, do the following steps:</span></span>
   1. <span data-ttu-id="26083-295">Abra la configuración de máquina de .NET 2.0 desde la carpeta: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span><span class="sxs-lookup"><span data-stu-id="26083-295">Open machine config of .NET 2.0 from the folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="26083-296">Busque **Proveedor de datos de Oracle para .NET**; debería encontrar una entrada tal y como se muestra en el siguiente ejemplo, en **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Proveedor de datos de Oracle para .NET</span><span class="sxs-lookup"><span data-stu-id="26083-296">Search for **Oracle Data Provider for .NET**, and you should be able to find an entry as shown in the following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="26083-297">”</span><span class="sxs-lookup"><span data-stu-id="26083-297">”</span></span>
3. <span data-ttu-id="26083-298">Copie esta entrada en el archivo machine.config en la siguiente carpeta v4.0: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, y cambie la versión a 4.xxx.x.x.</span><span class="sxs-lookup"><span data-stu-id="26083-298">Copy this entry to the machine.config file in the following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change the version to 4.xxx.x.x.</span></span>
4. <span data-ttu-id="26083-299">Instale “<Ruta de instalación de ODP.NET>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” en la caché global de ensamblados (GAC) ejecutando `gacutil /i [provider path]`.## Sugerencias de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="26083-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into the global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="26083-300">Problema 2: formato de fecha y hora</span><span class="sxs-lookup"><span data-stu-id="26083-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="26083-301">Se muestra el siguiente **mensaje de error**:</span><span class="sxs-lookup"><span data-stu-id="26083-301">You see the following **error message**:</span></span>

    Message=Operation failed in Oracle Database with the following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="26083-302">**Resolución o solución alternativa:**</span><span class="sxs-lookup"><span data-stu-id="26083-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="26083-303">Es posible que deba ajustar la cadena de consulta en la actividad de copia en función de cómo estén configuradas las fechas en la base de datos de Oracle, tal y como se muestra en el ejemplo siguiente (con la función to_date):</span><span class="sxs-lookup"><span data-stu-id="26083-303">You may need to adjust the query string in your copy activity based on how dates are configured in your Oracle database, as shown in the following sample (using the to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="26083-304">Asignación de tipos para Oracle</span><span class="sxs-lookup"><span data-stu-id="26083-304">Type mapping for Oracle</span></span>
<span data-ttu-id="26083-305">Como se mencionó en el artículo sobre [actividades del movimiento de datos](data-factory-data-movement-activities.md), la actividad de copia realiza conversiones automáticas de los tipos de origen a los tipos de receptor con el siguiente enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="26083-305">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="26083-306">Conversión de tipos de origen nativos al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="26083-306">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="26083-307">Conversión de tipo .NET al tipo del receptor nativo</span><span class="sxs-lookup"><span data-stu-id="26083-307">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="26083-308">Al mover datos de Oracle, se usan las siguientes asignaciones del tipo de datos de Oracle al tipo de .NET, y viceversa.</span><span class="sxs-lookup"><span data-stu-id="26083-308">When moving data from Oracle, the following mappings are used from Oracle data type to .NET type and vice versa.</span></span>

| <span data-ttu-id="26083-309">Tipo de datos de Oracle</span><span class="sxs-lookup"><span data-stu-id="26083-309">Oracle data type</span></span> | <span data-ttu-id="26083-310">Tipo de datos de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="26083-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="26083-311">BFILE</span><span class="sxs-lookup"><span data-stu-id="26083-311">BFILE</span></span> |<span data-ttu-id="26083-312">Byte[]</span><span class="sxs-lookup"><span data-stu-id="26083-312">Byte[]</span></span> |
| <span data-ttu-id="26083-313">BLOB</span><span class="sxs-lookup"><span data-stu-id="26083-313">BLOB</span></span> |<span data-ttu-id="26083-314">Byte[]</span><span class="sxs-lookup"><span data-stu-id="26083-314">Byte[]</span></span> |
| <span data-ttu-id="26083-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="26083-315">CHAR</span></span> |<span data-ttu-id="26083-316">String</span><span class="sxs-lookup"><span data-stu-id="26083-316">String</span></span> |
| <span data-ttu-id="26083-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="26083-317">CLOB</span></span> |<span data-ttu-id="26083-318">String</span><span class="sxs-lookup"><span data-stu-id="26083-318">String</span></span> |
| <span data-ttu-id="26083-319">DATE</span><span class="sxs-lookup"><span data-stu-id="26083-319">DATE</span></span> |<span data-ttu-id="26083-320">DateTime</span><span class="sxs-lookup"><span data-stu-id="26083-320">DateTime</span></span> |
| <span data-ttu-id="26083-321">FLOAT</span><span class="sxs-lookup"><span data-stu-id="26083-321">FLOAT</span></span> |<span data-ttu-id="26083-322">Decimal, String (si la precisión > 28)</span><span class="sxs-lookup"><span data-stu-id="26083-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="26083-323">INTEGER</span><span class="sxs-lookup"><span data-stu-id="26083-323">INTEGER</span></span> |<span data-ttu-id="26083-324">Decimal, String (si la precisión > 28)</span><span class="sxs-lookup"><span data-stu-id="26083-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="26083-325">INTERVAL YEAR TO MONTH</span><span class="sxs-lookup"><span data-stu-id="26083-325">INTERVAL YEAR TO MONTH</span></span> |<span data-ttu-id="26083-326">Int32</span><span class="sxs-lookup"><span data-stu-id="26083-326">Int32</span></span> |
| <span data-ttu-id="26083-327">INTERVAL DAY TO SECOND</span><span class="sxs-lookup"><span data-stu-id="26083-327">INTERVAL DAY TO SECOND</span></span> |<span data-ttu-id="26083-328">timespan</span><span class="sxs-lookup"><span data-stu-id="26083-328">TimeSpan</span></span> |
| <span data-ttu-id="26083-329">LONG</span><span class="sxs-lookup"><span data-stu-id="26083-329">LONG</span></span> |<span data-ttu-id="26083-330">String</span><span class="sxs-lookup"><span data-stu-id="26083-330">String</span></span> |
| <span data-ttu-id="26083-331">LONG RAW</span><span class="sxs-lookup"><span data-stu-id="26083-331">LONG RAW</span></span> |<span data-ttu-id="26083-332">Byte[]</span><span class="sxs-lookup"><span data-stu-id="26083-332">Byte[]</span></span> |
| <span data-ttu-id="26083-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="26083-333">NCHAR</span></span> |<span data-ttu-id="26083-334">String</span><span class="sxs-lookup"><span data-stu-id="26083-334">String</span></span> |
| <span data-ttu-id="26083-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="26083-335">NCLOB</span></span> |<span data-ttu-id="26083-336">String</span><span class="sxs-lookup"><span data-stu-id="26083-336">String</span></span> |
| <span data-ttu-id="26083-337">NUMBER</span><span class="sxs-lookup"><span data-stu-id="26083-337">NUMBER</span></span> |<span data-ttu-id="26083-338">Decimal, String (si la precisión > 28)</span><span class="sxs-lookup"><span data-stu-id="26083-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="26083-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="26083-339">NVARCHAR2</span></span> |<span data-ttu-id="26083-340">String</span><span class="sxs-lookup"><span data-stu-id="26083-340">String</span></span> |
| <span data-ttu-id="26083-341">RAW</span><span class="sxs-lookup"><span data-stu-id="26083-341">RAW</span></span> |<span data-ttu-id="26083-342">Byte[]</span><span class="sxs-lookup"><span data-stu-id="26083-342">Byte[]</span></span> |
| <span data-ttu-id="26083-343">ROWID</span><span class="sxs-lookup"><span data-stu-id="26083-343">ROWID</span></span> |<span data-ttu-id="26083-344">String</span><span class="sxs-lookup"><span data-stu-id="26083-344">String</span></span> |
| <span data-ttu-id="26083-345">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="26083-345">TIMESTAMP</span></span> |<span data-ttu-id="26083-346">DateTime</span><span class="sxs-lookup"><span data-stu-id="26083-346">DateTime</span></span> |
| <span data-ttu-id="26083-347">TIMESTAMP WITH LOCAL TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="26083-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="26083-348">DateTime</span><span class="sxs-lookup"><span data-stu-id="26083-348">DateTime</span></span> |
| <span data-ttu-id="26083-349">TIMESTAMP WITH TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="26083-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="26083-350">DateTime</span><span class="sxs-lookup"><span data-stu-id="26083-350">DateTime</span></span> |
| <span data-ttu-id="26083-351">UNSIGNED INTEGER</span><span class="sxs-lookup"><span data-stu-id="26083-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="26083-352">NUMBER</span><span class="sxs-lookup"><span data-stu-id="26083-352">Number</span></span> |
| <span data-ttu-id="26083-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="26083-353">VARCHAR2</span></span> |<span data-ttu-id="26083-354">String</span><span class="sxs-lookup"><span data-stu-id="26083-354">String</span></span> |
| <span data-ttu-id="26083-355">XML</span><span class="sxs-lookup"><span data-stu-id="26083-355">XML</span></span> |<span data-ttu-id="26083-356">String</span><span class="sxs-lookup"><span data-stu-id="26083-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="26083-357">Los tipos de datos **INTERVAL YEAR TO MONTH** e **INTERVAL DAY TO SECOND** no se admiten cuando se utiliza el controlador de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="26083-357">Data type **INTERVAL YEAR TO MONTH** and **INTERVAL DAY TO SECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="26083-358">Asignación de columnas de origen a columnas de receptor</span><span class="sxs-lookup"><span data-stu-id="26083-358">Map source to sink columns</span></span>
<span data-ttu-id="26083-359">Para obtener más información sobre la asignación de columnas del conjunto de datos de origen a las del conjunto de datos receptor, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="26083-359">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="26083-360">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="26083-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="26083-361">Cuando se copian datos desde almacenes de datos relacionales, hay que tener presente la repetibilidad para evitar resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="26083-361">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="26083-362">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="26083-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="26083-363">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="26083-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="26083-364">Cuando se vuelve a ejecutar un segmento, debe asegurarse de que los mismos datos se lean sin importar el número de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="26083-364">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="26083-365">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="26083-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="26083-366">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="26083-366">Performance and Tuning</span></span>
<span data-ttu-id="26083-367">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="26083-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
