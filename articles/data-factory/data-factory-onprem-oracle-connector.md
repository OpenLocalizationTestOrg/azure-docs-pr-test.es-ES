---
title: "aaaCopy datos de Oracle se realiza mediante la factoría de datos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocopy datos de base de datos de Oracle que sea de manera local mediante Data Factory de Azure."
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
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="8653a-103">Copia de datos con una instancia local Oracle como origen o destino mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8653a-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="8653a-104">Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde una base de datos de Oracle local.</span><span class="sxs-lookup"><span data-stu-id="8653a-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="8653a-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="8653a-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="8653a-106">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="8653a-106">Supported scenarios</span></span>
<span data-ttu-id="8653a-107">Puede copiar datos **desde una base de datos de Oracle** toohello siguientes almacenes de datos:</span><span class="sxs-lookup"><span data-stu-id="8653a-107">You can copy data **from an Oracle database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="8653a-108">Puede copiar los datos de hello siguientes almacenes de datos **tooan base de datos de Oracle**:</span><span class="sxs-lookup"><span data-stu-id="8653a-108">You can copy data from hello following data stores **tooan Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="8653a-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8653a-109">Prerequisites</span></span>
<span data-ttu-id="8653a-110">Factoría de datos admite conexión orígenes de Oracle de tooon locales mediante Hola Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="8653a-110">Data Factory supports connecting tooon-premises Oracle sources using hello Data Management Gateway.</span></span> <span data-ttu-id="8653a-111">Vea [Data Management Gateway](data-factory-data-management-gateway.md) toolearn artículo acerca de Data Management Gateway y [mover datos desde local toocloud](data-factory-move-data-between-onprem-and-cloud.md) artículo para obtener instrucciones paso a paso sobre cómo configurar la puerta de enlace de hello una canalización de datos datos de toomove.</span><span class="sxs-lookup"><span data-stu-id="8653a-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article toolearn about Data Management Gateway and [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="8653a-112">Puerta de enlace es necesaria incluso aunque hello Oracle hospedado en una VM de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="8653a-112">Gateway is required even if hello Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="8653a-113">Puede instalar la puerta de enlace de hello en Hola mismo IaaS VM como datos de hello almacenar o en una máquina virtual diferente siempre que la puerta de enlace de Hola pueden conectar toohello base de datos.</span><span class="sxs-lookup"><span data-stu-id="8653a-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="8653a-114">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8653a-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="8653a-115">Versiones compatibles e instalación</span><span class="sxs-lookup"><span data-stu-id="8653a-115">Supported versions and installation</span></span>
<span data-ttu-id="8653a-116">Este conector de Oracle admite dos versiones de controladores:</span><span class="sxs-lookup"><span data-stu-id="8653a-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="8653a-117">**Controlador de Microsoft para Oracle (recomendado)**: a partir de Data Management Gateway versión 2.7, un controlador de Microsoft para Oracle se instala automáticamente junto con la puerta de enlace de hello, por lo que no necesita tooadditionally identificador hello controlador en orden tooestablish conectividad tooOracle y, también puede experimentar un mejor rendimiento de copia con este controlador.</span><span class="sxs-lookup"><span data-stu-id="8653a-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with hello gateway, so you don't need tooadditionally handle hello driver in order tooestablish connectivity tooOracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="8653a-118">Se admiten las siguientes versiones de bases de datos de Oracle:</span><span class="sxs-lookup"><span data-stu-id="8653a-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="8653a-119">Oracle 12c R1 (12.1)</span><span class="sxs-lookup"><span data-stu-id="8653a-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="8653a-120">Oracle 11g R1, R2 (11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="8653a-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="8653a-121">Oracle 10g R1, R2 (10.1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="8653a-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="8653a-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="8653a-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="8653a-123">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="8653a-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8653a-124">Controlador de Microsoft para Oracle sólo admite actualmente copiaría datos de Oracle, pero no escribir tooOracle.</span><span class="sxs-lookup"><span data-stu-id="8653a-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing tooOracle.</span></span> <span data-ttu-id="8653a-125">Y capacidad de conexión de prueba de nota hello en la pestaña de diagnóstico de puerta de enlace de administración de datos no es compatible con este controlador.</span><span class="sxs-lookup"><span data-stu-id="8653a-125">And note hello test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="8653a-126">Como alternativa, puede usar la conectividad de Hola de hello copia Asistente toovalidate.</span><span class="sxs-lookup"><span data-stu-id="8653a-126">Alternatively, you can use hello copy wizard toovalidate hello connectivity.</span></span>
>

- <span data-ttu-id="8653a-127">**Proveedor de datos de Oracle para. NET:** también puede elegir el proveedor de datos de Oracle toocopy datos de toouse de / tooOracle.</span><span class="sxs-lookup"><span data-stu-id="8653a-127">**Oracle Data Provider for .NET:** you can also choose toouse Oracle Data Provider toocopy data from/tooOracle.</span></span> <span data-ttu-id="8653a-128">Este componente se incluye en [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/) (Componentes de acceso a datos Oracle para Windows).</span><span class="sxs-lookup"><span data-stu-id="8653a-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="8653a-129">Instale la versión adecuada de hello (32 o 64 bits) en la máquina de Hola donde se instala la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="8653a-129">Install hello appropriate version (32/64 bit) on hello machine where hello gateway is installed.</span></span> <span data-ttu-id="8653a-130">[Proveedor de datos de Oracle .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) puede tener acceso a tooOracle base de datos 10 g versión 2 o posterior.</span><span class="sxs-lookup"><span data-stu-id="8653a-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access tooOracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="8653a-131">Si elige "Instalación de XCopy", siga los pasos de hello readme.htm.</span><span class="sxs-lookup"><span data-stu-id="8653a-131">If you choose “XCopy Installation”, follow steps in hello readme.htm.</span></span> <span data-ttu-id="8653a-132">Se recomienda que elegir a instalador Hola con interfaz de usuario (no-XCopy uno).</span><span class="sxs-lookup"><span data-stu-id="8653a-132">We recommend you choose hello installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="8653a-133">Después de instalar el proveedor de hello, **reiniciar** Hola servicio de host de Data Management Gateway en su equipo con servicios de applet (u) Administrador de configuración de Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="8653a-133">After installing hello provider, **restart** hello Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="8653a-134">Si utiliza copia Asistente tooauthor Hola copia canalización, tipo de controlador de hello será determina automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8653a-134">If you use copy wizard tooauthor hello copy pipeline, hello driver type will be auto-determined.</span></span> <span data-ttu-id="8653a-135">El controlador de Microsoft se usará de forma predeterminada, a menos que la versión de la puerta de enlace sea inferior a 2.7 o elija Oracle como receptor.</span><span class="sxs-lookup"><span data-stu-id="8653a-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="8653a-136">Introducción</span><span class="sxs-lookup"><span data-stu-id="8653a-136">Getting started</span></span>
<span data-ttu-id="8653a-137">Puede crear una canalización con una actividad de copia que mueva datos desde una base de datos de Oracle local o hacia ella mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="8653a-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="8653a-138">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="8653a-138">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="8653a-139">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="8653a-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="8653a-140">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="8653a-140">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="8653a-141">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="8653a-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="8653a-142">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="8653a-142">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="8653a-143">Crear una **factoría de datos**.</span><span class="sxs-lookup"><span data-stu-id="8653a-143">Create a **data factory**.</span></span> <span data-ttu-id="8653a-144">Una factoría de datos puede contener una o más canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="8653a-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="8653a-145">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="8653a-145">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="8653a-146">Por ejemplo, si va a copiar datos desde un tooan de base de datos de Oralce almacenamiento de blobs de Azure, cree dos toolink servicios vinculados su base de datos de Oracle y la factoría de datos de tooyour de cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8653a-146">For example, if you are copying data from an Oralce database tooan Azure blob storage, you create two linked services toolink your Oracle database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="8653a-147">Para las propiedades de servicio vinculado que son tooOracle específico, consulte [vinculado propiedades del servicio](#linked-service-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="8653a-147">For linked service properties that are specific tooOracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="8653a-148">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8653a-148">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="8653a-149">En el ejemplo de Hola mencionado en el último paso de hello, creará una tabla de hello toospecify de conjunto de datos en la base de datos de Oracle que contiene datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="8653a-149">In hello example mentioned in hello last step, you create a dataset toospecify hello table in your Oracle database that contains hello input data.</span></span> <span data-ttu-id="8653a-150">Crear contenedor de blobs Hola de otro conjunto de datos toospecify y carpeta Hola que contiene datos de hello copiados de Hola de base de datos de Oracle.</span><span class="sxs-lookup"><span data-stu-id="8653a-150">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello Oracle database.</span></span> <span data-ttu-id="8653a-151">Para las propiedades de conjunto de datos que son tooOracle específico, consulte [propiedades de conjunto de datos](#dataset-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="8653a-151">For dataset properties that are specific tooOracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="8653a-152">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="8653a-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="8653a-153">En el ejemplo de Hola que se ha mencionado anteriormente, use OracleSource como un origen y BlobSink como un receptor para la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="8653a-153">In hello example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="8653a-154">De forma similar, si va a copiar desde la base de datos del almacenamiento de blobs de Azure tooOracle, usar BlobSource y OracleSink de actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="8653a-154">Similarly, if you are copying from Azure Blob Storage tooOracle Database, you use BlobSource and OracleSink in hello copy activity.</span></span> <span data-ttu-id="8653a-155">Para copiar propiedades de actividad que son la base de datos tooOracle específica, consulte [copiar propiedades de la actividad](#copy-activity-properties) sección.</span><span class="sxs-lookup"><span data-stu-id="8653a-155">For copy activity properties that are specific tooOracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="8653a-156">Para obtener detalles sobre cómo toouse un almacén de datos como un origen o un receptor, haga clic en el vínculo de hello en la sección anterior de hello para el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="8653a-156">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="8653a-157">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="8653a-157">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="8653a-158">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="8653a-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="8653a-159">Para obtener ejemplos con definiciones de JSON para entidades de la factoría de datos que son utilizados toocopy datos hacia y desde una base de datos de Oracle local, vea [ejemplos JSON](#json-examples-for-copying-data-to-and-from-oracle-database) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="8653a-159">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="8653a-160">Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son entidades de factoría de datos de uso toodefine:</span><span class="sxs-lookup"><span data-stu-id="8653a-160">hello following sections provide details about JSON properties that are used toodefine Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="8653a-161">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="8653a-161">Linked service properties</span></span>
<span data-ttu-id="8653a-162">Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooOracle vinculado.</span><span class="sxs-lookup"><span data-stu-id="8653a-162">hello following table provides description for JSON elements specific tooOracle linked service.</span></span>

| <span data-ttu-id="8653a-163">Propiedad</span><span class="sxs-lookup"><span data-stu-id="8653a-163">Property</span></span> | <span data-ttu-id="8653a-164">Descripción</span><span class="sxs-lookup"><span data-stu-id="8653a-164">Description</span></span> | <span data-ttu-id="8653a-165">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8653a-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8653a-166">type</span><span class="sxs-lookup"><span data-stu-id="8653a-166">type</span></span> |<span data-ttu-id="8653a-167">propiedad de tipo Hello debe establecerse en: **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="8653a-167">hello type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="8653a-168">Sí</span><span class="sxs-lookup"><span data-stu-id="8653a-168">Yes</span></span> |
| <span data-ttu-id="8653a-169">driverType</span><span class="sxs-lookup"><span data-stu-id="8653a-169">driverType</span></span> | <span data-ttu-id="8653a-170">Especificar qué controlador toouse toocopy datos / tooOracle base de datos.</span><span class="sxs-lookup"><span data-stu-id="8653a-170">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="8653a-171">Los valores permitidos son **Microsoft** u **ODP** (valor predeterminado).</span><span class="sxs-lookup"><span data-stu-id="8653a-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="8653a-172">Consulte la sección [Versiones compatibles e instalación](#supported-versions-and-installation) para obtener información detallada sobre los controladores.</span><span class="sxs-lookup"><span data-stu-id="8653a-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="8653a-173">No</span><span class="sxs-lookup"><span data-stu-id="8653a-173">No</span></span> |
| <span data-ttu-id="8653a-174">connectionString</span><span class="sxs-lookup"><span data-stu-id="8653a-174">connectionString</span></span> | <span data-ttu-id="8653a-175">Especifique la información necesaria la instancia de base de datos de Oracle toohello tooconnect para la propiedad connectionString de Hola.</span><span class="sxs-lookup"><span data-stu-id="8653a-175">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="8653a-176">Sí</span><span class="sxs-lookup"><span data-stu-id="8653a-176">Yes</span></span> |
| <span data-ttu-id="8653a-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8653a-177">gatewayName</span></span> | <span data-ttu-id="8653a-178">Nombre de puerta de enlace de Hola que es usado tooconnect toohello servidor Oracle local</span><span class="sxs-lookup"><span data-stu-id="8653a-178">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="8653a-179">Sí</span><span class="sxs-lookup"><span data-stu-id="8653a-179">Yes</span></span> |

<span data-ttu-id="8653a-180">**Ejemplo: Uso del controlador de Microsoft**</span><span class="sxs-lookup"><span data-stu-id="8653a-180">**Example: using Microsoft driver:**</span></span>
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

<span data-ttu-id="8653a-181">**Ejemplo: uso del controlador de ODP**</span><span class="sxs-lookup"><span data-stu-id="8653a-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="8653a-182">Consulte demasiado[este sitio](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) para hello formatos permitido.</span><span class="sxs-lookup"><span data-stu-id="8653a-182">Refer too[this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for hello allowed formats.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="8653a-183">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="8653a-183">Dataset properties</span></span>
<span data-ttu-id="8653a-184">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="8653a-184">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="8653a-185">Las secciones como structure, availability y policy de un conjunto de datos JSON son similares en todos los tipos de conjunto de datos (Oracle, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="8653a-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="8653a-186">sección de typeProperties Hello es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="8653a-186">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="8653a-187">sección de typeProperties Hello para el conjunto de datos de Hola de tipo OracleTable tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="8653a-187">hello typeProperties section for hello dataset of type OracleTable has hello following properties:</span></span>

| <span data-ttu-id="8653a-188">Propiedad</span><span class="sxs-lookup"><span data-stu-id="8653a-188">Property</span></span> | <span data-ttu-id="8653a-189">Descripción</span><span class="sxs-lookup"><span data-stu-id="8653a-189">Description</span></span> | <span data-ttu-id="8653a-190">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8653a-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8653a-191">tableName</span><span class="sxs-lookup"><span data-stu-id="8653a-191">tableName</span></span> |<span data-ttu-id="8653a-192">Nombre de tabla de Hola Hola base de datos de Oracle que Hola servicio vinculado que hace referencia a.</span><span class="sxs-lookup"><span data-stu-id="8653a-192">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="8653a-193">No (si se especifica **oracleReaderQuery** de **OracleSource**)</span><span class="sxs-lookup"><span data-stu-id="8653a-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="8653a-194">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="8653a-194">Copy activity properties</span></span>
<span data-ttu-id="8653a-195">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="8653a-195">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="8653a-196">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="8653a-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="8653a-197">Hola actividad de copia toma solo una entrada y produce un único resultado.</span><span class="sxs-lookup"><span data-stu-id="8653a-197">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="8653a-198">Mientras que las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="8653a-198">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="8653a-199">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="8653a-199">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="8653a-200">OracleSource</span><span class="sxs-lookup"><span data-stu-id="8653a-200">OracleSource</span></span>
<span data-ttu-id="8653a-201">En la actividad de copia, cuando el origen de hello es de tipo **OracleSource** Hola propiedades siguientes está disponible en **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="8653a-201">In Copy activity, when hello source is of type **OracleSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="8653a-202">Propiedad</span><span class="sxs-lookup"><span data-stu-id="8653a-202">Property</span></span> | <span data-ttu-id="8653a-203">Descripción</span><span class="sxs-lookup"><span data-stu-id="8653a-203">Description</span></span> | <span data-ttu-id="8653a-204">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8653a-204">Allowed values</span></span> | <span data-ttu-id="8653a-205">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8653a-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8653a-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="8653a-206">oracleReaderQuery</span></span> |<span data-ttu-id="8653a-207">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="8653a-207">Use hello custom query tooread data.</span></span> |<span data-ttu-id="8653a-208">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="8653a-208">SQL query string.</span></span> <span data-ttu-id="8653a-209">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="8653a-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="8653a-210">Si no se especifica, Hola instrucción SQL que se ejecuta: seleccione * from MyTable</span><span class="sxs-lookup"><span data-stu-id="8653a-210">If not specified, hello SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="8653a-211">No (si se especifica **tableName** de **dataset**)</span><span class="sxs-lookup"><span data-stu-id="8653a-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="8653a-212">OracleSink</span><span class="sxs-lookup"><span data-stu-id="8653a-212">OracleSink</span></span>
<span data-ttu-id="8653a-213">**OracleSink** admite Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="8653a-213">**OracleSink** supports hello following properties:</span></span>

| <span data-ttu-id="8653a-214">Propiedad</span><span class="sxs-lookup"><span data-stu-id="8653a-214">Property</span></span> | <span data-ttu-id="8653a-215">Descripción</span><span class="sxs-lookup"><span data-stu-id="8653a-215">Description</span></span> | <span data-ttu-id="8653a-216">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8653a-216">Allowed values</span></span> | <span data-ttu-id="8653a-217">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8653a-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8653a-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="8653a-218">writeBatchTimeout</span></span> |<span data-ttu-id="8653a-219">Tiempo de espera para toocomplete de operación de inserción de lote de hello antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="8653a-219">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="8653a-220">timespan</span><span class="sxs-lookup"><span data-stu-id="8653a-220">timespan</span></span><br/><br/> <span data-ttu-id="8653a-221">Ejemplo: 00:30:00 (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="8653a-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="8653a-222">No</span><span class="sxs-lookup"><span data-stu-id="8653a-222">No</span></span> |
| <span data-ttu-id="8653a-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="8653a-223">writeBatchSize</span></span> |<span data-ttu-id="8653a-224">Inserta datos en tablas SQL de hello cuando el tamaño de búfer de hello alcance el valor writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="8653a-224">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="8653a-225">Entero (número de filas)</span><span class="sxs-lookup"><span data-stu-id="8653a-225">Integer (number of rows)</span></span> |<span data-ttu-id="8653a-226">No (valor predeterminado: 100)</span><span class="sxs-lookup"><span data-stu-id="8653a-226">No (default: 100)</span></span> |
| <span data-ttu-id="8653a-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="8653a-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="8653a-228">Especificar una consulta para tooexecute de actividad de copia de forma que los datos de un determinado segmento se limpian.</span><span class="sxs-lookup"><span data-stu-id="8653a-228">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="8653a-229">Una instrucción de consulta.</span><span class="sxs-lookup"><span data-stu-id="8653a-229">A query statement.</span></span> |<span data-ttu-id="8653a-230">No</span><span class="sxs-lookup"><span data-stu-id="8653a-230">No</span></span> |
| <span data-ttu-id="8653a-231">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="8653a-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="8653a-232">Especifique el nombre de columna para la actividad de copia toofill con el identificador de segmento generados automáticamente, que es usado tooclean los datos de un determinado segmento cuando vuelva a ejecutar.</span><span class="sxs-lookup"><span data-stu-id="8653a-232">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="8653a-233">Nombre de columna de una columna con el tipo de datos binarios (32).</span><span class="sxs-lookup"><span data-stu-id="8653a-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="8653a-234">No</span><span class="sxs-lookup"><span data-stu-id="8653a-234">No</span></span> |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a><span data-ttu-id="8653a-235">Ejemplos JSON para copiar datos tooand de base de datos de Oracle</span><span class="sxs-lookup"><span data-stu-id="8653a-235">JSON examples for copying data tooand from Oracle database</span></span>
<span data-ttu-id="8653a-236">Hello en el ejemplo siguiente se proporciona definiciones de JSON de ejemplo que puede utilizar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8653a-236">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="8653a-237">Muestran cómo toocopy datos de Oracle tooan la base de datos de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="8653a-237">They show how toocopy data from/tooan Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="8653a-238">Sin embargo, los datos pueden ser tooany copiada de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8653a-238">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a><span data-ttu-id="8653a-239">Ejemplo: Copiar los datos de Oracle tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="8653a-239">Example: Copy data from Oracle tooAzure Blob</span></span>

<span data-ttu-id="8653a-240">ejemplo de Hola tiene Hola después de entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="8653a-240">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="8653a-241">Un servicio vinculado de tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8653a-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="8653a-242">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="8653a-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="8653a-243">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8653a-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="8653a-244">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8653a-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="8653a-245">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) como origen y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) como receptor.</span><span class="sxs-lookup"><span data-stu-id="8653a-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="8653a-246">ejemplo de Hola copia datos de una tabla en un blob de tooa de base de datos de Oracle local cada hora.</span><span class="sxs-lookup"><span data-stu-id="8653a-246">hello sample copies data from a table in an on-premises Oracle database tooa blob hourly.</span></span> <span data-ttu-id="8653a-247">Para obtener más información sobre varias propiedades utilizadas en el ejemplo de Hola, consulte la documentación en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="8653a-247">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="8653a-248">**Servicio vinculado de Oracle:**</span><span class="sxs-lookup"><span data-stu-id="8653a-248">**Oracle linked service:**</span></span>

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

<span data-ttu-id="8653a-249">**Servicio vinculado Azure Blob Storage:**</span><span class="sxs-lookup"><span data-stu-id="8653a-249">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="8653a-250">**Conjunto de datos de entrada de Oracle:**</span><span class="sxs-lookup"><span data-stu-id="8653a-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="8653a-251">ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en Oracle y contiene una columna denominada "timestampcolumn" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="8653a-251">hello sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="8653a-252">Establecer "externo": "true" informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8653a-252">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="8653a-253">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="8653a-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="8653a-254">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="8653a-254">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="8653a-255">Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="8653a-255">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="8653a-256">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8653a-256">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="8653a-257">**Canalización con actividad de copia:**</span><span class="sxs-lookup"><span data-stu-id="8653a-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="8653a-258">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y es toorun programada cada hora.</span><span class="sxs-lookup"><span data-stu-id="8653a-258">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="8653a-259">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**OracleSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="8653a-259">In hello pipeline JSON definition, hello **source** type is set too**OracleSource** and **sink** type is set too**BlobSink**.</span></span>  <span data-ttu-id="8653a-260">consulta SQL Hola especificada con **oracleReaderQuery** propiedad selecciona datos Hola Hola más allá de hora toocopy.</span><span class="sxs-lookup"><span data-stu-id="8653a-260">hello SQL query specified with **oracleReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-toooracle"></a><span data-ttu-id="8653a-261">Ejemplo: Copiar los datos de Blob de Azure tooOracle</span><span class="sxs-lookup"><span data-stu-id="8653a-261">Example: Copy data from Azure Blob tooOracle</span></span>
<span data-ttu-id="8653a-262">Este ejemplo muestra cómo toocopy datos desde un almacenamiento de blobs de Azure tooan locales base de datos de Oracle.</span><span class="sxs-lookup"><span data-stu-id="8653a-262">This sample shows how toocopy data from an Azure Blob Storage tooan on-premises Oracle database.</span></span> <span data-ttu-id="8653a-263">Sin embargo, se pueden copiar datos **directamente** desde cualquiera de los orígenes de hello indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8653a-263">However, data can be copied **directly** from any of hello sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="8653a-264">ejemplo de Hola tiene Hola después de entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="8653a-264">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="8653a-265">Un servicio vinculado de tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8653a-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="8653a-266">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="8653a-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="8653a-267">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8653a-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="8653a-268">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8653a-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="8653a-269">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) como origen y [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) como receptor.</span><span class="sxs-lookup"><span data-stu-id="8653a-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="8653a-270">ejemplo de Hola copia datos de una tabla de tooa de blob en una base de datos de Oracle local cada hora.</span><span class="sxs-lookup"><span data-stu-id="8653a-270">hello sample copies data from a blob tooa table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="8653a-271">Para obtener más información sobre varias propiedades utilizadas en el ejemplo de Hola, consulte la documentación en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="8653a-271">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="8653a-272">**Servicio vinculado de Oracle:**</span><span class="sxs-lookup"><span data-stu-id="8653a-272">**Oracle linked service:**</span></span>
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

<span data-ttu-id="8653a-273">**Servicio vinculado de almacenamiento de blobs de Azure:**</span><span class="sxs-lookup"><span data-stu-id="8653a-273">**Azure Blob storage linked service:**</span></span>
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

<span data-ttu-id="8653a-274">**Conjunto de datos de entrada de blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="8653a-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="8653a-275">Los datos se seleccionan de un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="8653a-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="8653a-276">Hola ruta de acceso y nombre de la carpeta para el blob de Hola se evalúan dinámicamente en función del tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="8653a-276">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="8653a-277">ruta de acceso de carpeta de Hello utiliza year, month y parte del día de la hora de inicio de Hola y el nombre de archivo usa parte de hora de inicio de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="8653a-277">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="8653a-278">"externo": "true" configuración informa a servicio de factoría de datos de Hola que esta tabla es factoría de datos de toohello externos y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8653a-278">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="8653a-279">**Conjunto de datos de salida de Oracle:**</span><span class="sxs-lookup"><span data-stu-id="8653a-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="8653a-280">ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en Oracle.</span><span class="sxs-lookup"><span data-stu-id="8653a-280">hello sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="8653a-281">Crear tabla de hello en Oracle con Hola mismo número de columnas, tal como se esperaba toocontain de archivo CSV de Blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="8653a-281">Create hello table in Oracle with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="8653a-282">Se agregan nuevas filas toohello tabla cada hora.</span><span class="sxs-lookup"><span data-stu-id="8653a-282">New rows are added toohello table every hour.</span></span>

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

<span data-ttu-id="8653a-283">**Canalización con actividad de copia:**</span><span class="sxs-lookup"><span data-stu-id="8653a-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="8653a-284">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida y está programada toorun cada hora.</span><span class="sxs-lookup"><span data-stu-id="8653a-284">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="8653a-285">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**BlobSource** hello y **receptor** tipo está establecido demasiado**OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="8653a-285">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and hello **sink** type is set too**OracleSink**.</span></span>  

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


## <a name="troubleshooting-tips"></a><span data-ttu-id="8653a-286">Sugerencias de solución de problemas</span><span class="sxs-lookup"><span data-stu-id="8653a-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="8653a-287">Problema 1: proveedor de datos .NET Framework</span><span class="sxs-lookup"><span data-stu-id="8653a-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="8653a-288">Ve a continuación hello **mensaje de error**:</span><span class="sxs-lookup"><span data-stu-id="8653a-288">You see hello following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="8653a-289">**Causas posibles:**</span><span class="sxs-lookup"><span data-stu-id="8653a-289">**Possible causes:**</span></span>

1. <span data-ttu-id="8653a-290">no se instaló el proveedor de datos de .NET Framework para Oracle Hola.</span><span class="sxs-lookup"><span data-stu-id="8653a-290">hello .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="8653a-291">Hola proveedor de datos de .NET Framework para Oracle era too.NET instalado Framework 2.0 y no se encuentra en carpetas de hello .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="8653a-291">hello .NET Framework Data Provider for Oracle was installed too.NET Framework 2.0 and is not found in hello .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="8653a-292">**Resolución o solución alternativa:**</span><span class="sxs-lookup"><span data-stu-id="8653a-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="8653a-293">Si no ha instalado Hola proveedor .NET para Oracle, [instalarlo](http://www.oracle.com/technetwork/topics/dotnet/downloads/) e intente de nuevo escenario de Hola.</span><span class="sxs-lookup"><span data-stu-id="8653a-293">If you haven't installed hello .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry hello scenario.</span></span>
2. <span data-ttu-id="8653a-294">Si recibe el mensaje de error de hello incluso después de instalar el proveedor de hello, Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8653a-294">If you get hello error message even after installing hello provider, do hello following steps:</span></span>
   1. <span data-ttu-id="8653a-295">Abrir configuración de máquina de .NET 2.0 desde la carpeta de hello: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span><span class="sxs-lookup"><span data-stu-id="8653a-295">Open machine config of .NET 2.0 from hello folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="8653a-296">Busque **proveedor de datos de Oracle para .NET**, y debe ser capaz de toofind una entrada como se muestra en hello según muestra en **system.data** -> **DbProviderFactories**: "<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Proveedor de datos de oracle para .NET</span><span class="sxs-lookup"><span data-stu-id="8653a-296">Search for **Oracle Data Provider for .NET**, and you should be able toofind an entry as shown in hello following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="8653a-297">”</span><span class="sxs-lookup"><span data-stu-id="8653a-297">”</span></span>
3. <span data-ttu-id="8653a-298">Copie este archivo de entrada toohello machine.config Hola después carpeta v4.0: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config y too4.xxx.x.x de versión de Hola de cambio.</span><span class="sxs-lookup"><span data-stu-id="8653a-298">Copy this entry toohello machine.config file in hello following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change hello version too4.xxx.x.x.</span></span>
4. <span data-ttu-id="8653a-299">Instalar "< ruta de instalación ODP.NET > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll" en la caché de ensamblados global (GAC) de hello ejecutando `gacutil /i [provider path]`. ## sugerencias para solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="8653a-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into hello global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="8653a-300">Problema 2: formato de fecha y hora</span><span class="sxs-lookup"><span data-stu-id="8653a-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="8653a-301">Ve a continuación hello **mensaje de error**:</span><span class="sxs-lookup"><span data-stu-id="8653a-301">You see hello following **error message**:</span></span>

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="8653a-302">**Resolución o solución alternativa:**</span><span class="sxs-lookup"><span data-stu-id="8653a-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="8653a-303">Puede que necesite tooadjust cadena de consulta de hello en la actividad de copia según cómo se configuran las fechas en la base de datos de Oracle, como se muestra en la siguiente Hola ejemplo (mediante la función to_date de hello):</span><span class="sxs-lookup"><span data-stu-id="8653a-303">You may need tooadjust hello query string in your copy activity based on how dates are configured in your Oracle database, as shown in hello following sample (using hello to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="8653a-304">Asignación de tipos para Oracle</span><span class="sxs-lookup"><span data-stu-id="8653a-304">Type mapping for Oracle</span></span>
<span data-ttu-id="8653a-305">Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque del paso 2:</span><span class="sxs-lookup"><span data-stu-id="8653a-305">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="8653a-306">Convertir del tipo de origen nativo tipos too.NET</span><span class="sxs-lookup"><span data-stu-id="8653a-306">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="8653a-307">Convertir el tipo de receptor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="8653a-307">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="8653a-308">Al mover los datos de Oracle, se usa Hola siguiendo las asignaciones del tipo de too.NET del tipo de datos de Oracle y viceversa.</span><span class="sxs-lookup"><span data-stu-id="8653a-308">When moving data from Oracle, hello following mappings are used from Oracle data type too.NET type and vice versa.</span></span>

| <span data-ttu-id="8653a-309">Tipo de datos de Oracle</span><span class="sxs-lookup"><span data-stu-id="8653a-309">Oracle data type</span></span> | <span data-ttu-id="8653a-310">Tipo de datos de .NET Framework</span><span class="sxs-lookup"><span data-stu-id="8653a-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="8653a-311">BFILE</span><span class="sxs-lookup"><span data-stu-id="8653a-311">BFILE</span></span> |<span data-ttu-id="8653a-312">Byte[]</span><span class="sxs-lookup"><span data-stu-id="8653a-312">Byte[]</span></span> |
| <span data-ttu-id="8653a-313">BLOB</span><span class="sxs-lookup"><span data-stu-id="8653a-313">BLOB</span></span> |<span data-ttu-id="8653a-314">Byte[]</span><span class="sxs-lookup"><span data-stu-id="8653a-314">Byte[]</span></span> |
| <span data-ttu-id="8653a-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="8653a-315">CHAR</span></span> |<span data-ttu-id="8653a-316">String</span><span class="sxs-lookup"><span data-stu-id="8653a-316">String</span></span> |
| <span data-ttu-id="8653a-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="8653a-317">CLOB</span></span> |<span data-ttu-id="8653a-318">String</span><span class="sxs-lookup"><span data-stu-id="8653a-318">String</span></span> |
| <span data-ttu-id="8653a-319">DATE</span><span class="sxs-lookup"><span data-stu-id="8653a-319">DATE</span></span> |<span data-ttu-id="8653a-320">DateTime</span><span class="sxs-lookup"><span data-stu-id="8653a-320">DateTime</span></span> |
| <span data-ttu-id="8653a-321">FLOAT</span><span class="sxs-lookup"><span data-stu-id="8653a-321">FLOAT</span></span> |<span data-ttu-id="8653a-322">Decimal, String (si la precisión > 28)</span><span class="sxs-lookup"><span data-stu-id="8653a-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="8653a-323">INTEGER</span><span class="sxs-lookup"><span data-stu-id="8653a-323">INTEGER</span></span> |<span data-ttu-id="8653a-324">Decimal, String (si la precisión > 28)</span><span class="sxs-lookup"><span data-stu-id="8653a-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="8653a-325">INTERVALO año tooMONTH</span><span class="sxs-lookup"><span data-stu-id="8653a-325">INTERVAL YEAR tooMONTH</span></span> |<span data-ttu-id="8653a-326">Int32</span><span class="sxs-lookup"><span data-stu-id="8653a-326">Int32</span></span> |
| <span data-ttu-id="8653a-327">INTERVALO día tooSECOND</span><span class="sxs-lookup"><span data-stu-id="8653a-327">INTERVAL DAY tooSECOND</span></span> |<span data-ttu-id="8653a-328">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="8653a-328">TimeSpan</span></span> |
| <span data-ttu-id="8653a-329">LONG</span><span class="sxs-lookup"><span data-stu-id="8653a-329">LONG</span></span> |<span data-ttu-id="8653a-330">String</span><span class="sxs-lookup"><span data-stu-id="8653a-330">String</span></span> |
| <span data-ttu-id="8653a-331">LONG RAW</span><span class="sxs-lookup"><span data-stu-id="8653a-331">LONG RAW</span></span> |<span data-ttu-id="8653a-332">Byte[]</span><span class="sxs-lookup"><span data-stu-id="8653a-332">Byte[]</span></span> |
| <span data-ttu-id="8653a-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="8653a-333">NCHAR</span></span> |<span data-ttu-id="8653a-334">String</span><span class="sxs-lookup"><span data-stu-id="8653a-334">String</span></span> |
| <span data-ttu-id="8653a-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="8653a-335">NCLOB</span></span> |<span data-ttu-id="8653a-336">String</span><span class="sxs-lookup"><span data-stu-id="8653a-336">String</span></span> |
| <span data-ttu-id="8653a-337">NUMBER</span><span class="sxs-lookup"><span data-stu-id="8653a-337">NUMBER</span></span> |<span data-ttu-id="8653a-338">Decimal, String (si la precisión > 28)</span><span class="sxs-lookup"><span data-stu-id="8653a-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="8653a-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="8653a-339">NVARCHAR2</span></span> |<span data-ttu-id="8653a-340">String</span><span class="sxs-lookup"><span data-stu-id="8653a-340">String</span></span> |
| <span data-ttu-id="8653a-341">RAW</span><span class="sxs-lookup"><span data-stu-id="8653a-341">RAW</span></span> |<span data-ttu-id="8653a-342">Byte[]</span><span class="sxs-lookup"><span data-stu-id="8653a-342">Byte[]</span></span> |
| <span data-ttu-id="8653a-343">ROWID</span><span class="sxs-lookup"><span data-stu-id="8653a-343">ROWID</span></span> |<span data-ttu-id="8653a-344">String</span><span class="sxs-lookup"><span data-stu-id="8653a-344">String</span></span> |
| <span data-ttu-id="8653a-345">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="8653a-345">TIMESTAMP</span></span> |<span data-ttu-id="8653a-346">DateTime</span><span class="sxs-lookup"><span data-stu-id="8653a-346">DateTime</span></span> |
| <span data-ttu-id="8653a-347">TIMESTAMP WITH LOCAL TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="8653a-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="8653a-348">DateTime</span><span class="sxs-lookup"><span data-stu-id="8653a-348">DateTime</span></span> |
| <span data-ttu-id="8653a-349">TIMESTAMP WITH TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="8653a-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="8653a-350">DateTime</span><span class="sxs-lookup"><span data-stu-id="8653a-350">DateTime</span></span> |
| <span data-ttu-id="8653a-351">UNSIGNED INTEGER</span><span class="sxs-lookup"><span data-stu-id="8653a-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="8653a-352">NUMBER</span><span class="sxs-lookup"><span data-stu-id="8653a-352">Number</span></span> |
| <span data-ttu-id="8653a-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="8653a-353">VARCHAR2</span></span> |<span data-ttu-id="8653a-354">String</span><span class="sxs-lookup"><span data-stu-id="8653a-354">String</span></span> |
| <span data-ttu-id="8653a-355">XML</span><span class="sxs-lookup"><span data-stu-id="8653a-355">XML</span></span> |<span data-ttu-id="8653a-356">String</span><span class="sxs-lookup"><span data-stu-id="8653a-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="8653a-357">Tipo de datos **año del intervalo tooMONTH** y **tooSECOND INTERVAL DAY** no se admiten cuando se utiliza el controlador de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8653a-357">Data type **INTERVAL YEAR tooMONTH** and **INTERVAL DAY tooSECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="8653a-358">Asignar columnas de origen toosink</span><span class="sxs-lookup"><span data-stu-id="8653a-358">Map source toosink columns</span></span>
<span data-ttu-id="8653a-359">toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="8653a-359">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="8653a-360">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="8653a-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="8653a-361">Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="8653a-361">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="8653a-362">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="8653a-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="8653a-363">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="8653a-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="8653a-364">Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento.</span><span class="sxs-lookup"><span data-stu-id="8653a-364">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="8653a-365">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="8653a-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="8653a-366">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="8653a-366">Performance and Tuning</span></span>
<span data-ttu-id="8653a-367">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="8653a-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
