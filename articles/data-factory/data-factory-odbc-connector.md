---
title: aaaMove datos de almacenes de datos ODBC | Documentos de Microsoft
description: "Obtenga información acerca de cómo usar Data Factory de Azure de almacenes de datos de toomove de datos ODBC."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="d5b1a-103">Movimiento de datos desde almacenes de datos ODBC mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="d5b1a-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="d5b1a-104">Este artículo explica cómo almacenar toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde un datos ODBC local.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises ODBC data store.</span></span> <span data-ttu-id="d5b1a-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="d5b1a-106">Puede copiar datos desde un almacén de datos ODBC datos almacén tooany admitida receptor.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-106">You can copy data from an ODBC data store tooany supported sink data store.</span></span> <span data-ttu-id="d5b1a-107">Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="d5b1a-108">Factoría de datos admite actualmente solo mover tooother almacenes de datos del almacén de datos desde un datos ODBC, pero no para mover los datos de otro almacén de datos ODBC tooan de datos almacenes.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-108">Data factory currently supports only moving data from an ODBC data store tooother data stores, but not for moving data from other data stores tooan ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="d5b1a-109">Habilitación de la conectividad</span><span class="sxs-lookup"><span data-stu-id="d5b1a-109">Enabling connectivity</span></span>
<span data-ttu-id="d5b1a-110">Servicio de factoría de datos admite conectar orígenes ODBC de tooon locales mediante Hola Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-110">Data Factory service supports connecting tooon-premises ODBC sources using hello Data Management Gateway.</span></span> <span data-ttu-id="d5b1a-111">Vea [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) toolearn artículo acerca de la puerta de enlace de datos de administración y las instrucciones paso a paso sobre cómo configurar la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="d5b1a-112">Usar almacén de datos ODBC de tooan tooconnect de puerta de enlace de hello incluso si está hospedado en una máquina virtual de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-112">Use hello gateway tooconnect tooan ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="d5b1a-113">Puede instalar la puerta de enlace de Hola en hello local mismo equipo u Hola VM de Azure como almacén de datos ODBC de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-113">You can install hello gateway on hello same on-premises machine or hello Azure VM as hello ODBC data store.</span></span> <span data-ttu-id="d5b1a-114">Sin embargo, recomendamos que instale la puerta de enlace de hello en un equipo independiente/Azure IaaS VM tooavoid contención de recursos y para mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-114">However, we recommend that you install hello gateway on a separate machine/Azure IaaS VM tooavoid resource contention and for better performance.</span></span> <span data-ttu-id="d5b1a-115">Cuando se instala la puerta de enlace de hello en un equipo independiente, máquina Hola debe ser tooaccess capaz de máquina de hello con almacén de datos ODBC Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-115">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello ODBC data store.</span></span>

<span data-ttu-id="d5b1a-116">Además de hello Data Management Gateway, también se necesita el controlador ODBC de tooinstall Hola para Hola de almacén de datos en la máquina de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-116">Apart from hello Data Management Gateway, you also need tooinstall hello ODBC driver for hello data store on hello gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="d5b1a-117">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d5b1a-118">Introducción</span><span class="sxs-lookup"><span data-stu-id="d5b1a-118">Getting started</span></span>
<span data-ttu-id="d5b1a-119">Puede crear una canalización con una actividad de copia que mueva datos desde un almacén de datos ODBC mediante diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="d5b1a-120">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="d5b1a-121">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="d5b1a-122">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d5b1a-123">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="d5b1a-124">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="d5b1a-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="d5b1a-125">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="d5b1a-126">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="d5b1a-127">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="d5b1a-128">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="d5b1a-129">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="d5b1a-130">Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos ODBC, vea [ejemplo de JSON: tooAzure Blob del almacén de datos de copia de datos ODBC](#json-example-copy-data-from-odbc-data-store-to-azure-blob) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an ODBC data store, see [JSON example: Copy data from ODBC data store tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="d5b1a-131">Hello las secciones siguientes proporciona detalles acerca de las propiedades JSON que son el almacén de datos de uso toodefine factoría de datos entidades tooODBC específico:</span><span class="sxs-lookup"><span data-stu-id="d5b1a-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d5b1a-132">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="d5b1a-132">Linked service properties</span></span>
<span data-ttu-id="d5b1a-133">Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooODBC vinculado.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-133">hello following table provides description for JSON elements specific tooODBC linked service.</span></span>

| <span data-ttu-id="d5b1a-134">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d5b1a-134">Property</span></span> | <span data-ttu-id="d5b1a-135">Descripción</span><span class="sxs-lookup"><span data-stu-id="d5b1a-135">Description</span></span> | <span data-ttu-id="d5b1a-136">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d5b1a-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5b1a-137">type</span><span class="sxs-lookup"><span data-stu-id="d5b1a-137">type</span></span> |<span data-ttu-id="d5b1a-138">propiedad de tipo Hello debe establecerse en: **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="d5b1a-138">hello type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="d5b1a-139">Sí</span><span class="sxs-lookup"><span data-stu-id="d5b1a-139">Yes</span></span> |
| <span data-ttu-id="d5b1a-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="d5b1a-140">connectionString</span></span> |<span data-ttu-id="d5b1a-141">parte de credencial de acceso no Hola de cadena de conexión de Hola y opcional cifra credenciales.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-141">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="d5b1a-142">Vea los ejemplos de hello las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-142">See examples in hello following sections.</span></span> |<span data-ttu-id="d5b1a-143">Sí</span><span class="sxs-lookup"><span data-stu-id="d5b1a-143">Yes</span></span> |
| <span data-ttu-id="d5b1a-144">credential</span><span class="sxs-lookup"><span data-stu-id="d5b1a-144">credential</span></span> |<span data-ttu-id="d5b1a-145">Hola credencial parte de acceso a cadena de conexión de hello especificada en formato de valores de propiedad específicos del controlador.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-145">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="d5b1a-146">Ejemplo: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="d5b1a-147">No</span><span class="sxs-lookup"><span data-stu-id="d5b1a-147">No</span></span> |
| <span data-ttu-id="d5b1a-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="d5b1a-148">authenticationType</span></span> |<span data-ttu-id="d5b1a-149">Tipo de autenticación que utiliza el almacén de datos ODBC tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-149">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="d5b1a-150">Los valores posibles son: Anonymous y Basic.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="d5b1a-151">Sí</span><span class="sxs-lookup"><span data-stu-id="d5b1a-151">Yes</span></span> |
| <span data-ttu-id="d5b1a-152">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="d5b1a-152">username</span></span> |<span data-ttu-id="d5b1a-153">Especifique el nombre de usuario si usa la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="d5b1a-154">No</span><span class="sxs-lookup"><span data-stu-id="d5b1a-154">No</span></span> |
| <span data-ttu-id="d5b1a-155">Contraseña</span><span class="sxs-lookup"><span data-stu-id="d5b1a-155">password</span></span> |<span data-ttu-id="d5b1a-156">Especifique la contraseña de cuenta de usuario de Hola que especificó para el nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-156">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="d5b1a-157">No</span><span class="sxs-lookup"><span data-stu-id="d5b1a-157">No</span></span> |
| <span data-ttu-id="d5b1a-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d5b1a-158">gatewayName</span></span> |<span data-ttu-id="d5b1a-159">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar el almacén de datos ODBC tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="d5b1a-160">Sí</span><span class="sxs-lookup"><span data-stu-id="d5b1a-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="d5b1a-161">Uso de la autenticación básica</span><span class="sxs-lookup"><span data-stu-id="d5b1a-161">Using Basic authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="d5b1a-162">Uso de la autenticación básica con credenciales cifradas</span><span class="sxs-lookup"><span data-stu-id="d5b1a-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="d5b1a-163">Puede cifrar las credenciales de hello con hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (1.0 versión de PowerShell de Azure) o [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 versión o una anterior de hello Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="d5b1a-163">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="d5b1a-164">Uso de autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="d5b1a-164">Using Anonymous authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a><span data-ttu-id="d5b1a-165">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="d5b1a-165">Dataset properties</span></span>
<span data-ttu-id="d5b1a-166">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d5b1a-167">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="d5b1a-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="d5b1a-168">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="d5b1a-169">sección typeProperties Hello para el conjunto de datos de tipo **RelationalTable** (que incluye el conjunto de datos ODBC) tiene Hola propiedades siguientes</span><span class="sxs-lookup"><span data-stu-id="d5b1a-169">hello typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has hello following properties</span></span>

| <span data-ttu-id="d5b1a-170">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d5b1a-170">Property</span></span> | <span data-ttu-id="d5b1a-171">Descripción</span><span class="sxs-lookup"><span data-stu-id="d5b1a-171">Description</span></span> | <span data-ttu-id="d5b1a-172">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d5b1a-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5b1a-173">tableName</span><span class="sxs-lookup"><span data-stu-id="d5b1a-173">tableName</span></span> |<span data-ttu-id="d5b1a-174">Nombre de tabla de hello en el almacén de datos ODBC Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-174">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="d5b1a-175">Sí</span><span class="sxs-lookup"><span data-stu-id="d5b1a-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="d5b1a-176">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="d5b1a-176">Copy activity properties</span></span>
<span data-ttu-id="d5b1a-177">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-177">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d5b1a-178">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="d5b1a-179">Propiedades disponibles en hello **typeProperties** sección de actividad de hello en hello varían con cada tipo de actividad en otra parte.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-179">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="d5b1a-180">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-180">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="d5b1a-181">En la actividad de copia, cuando el origen es de tipo **RelationalSource** (que incluye ODBC), Hola propiedades siguientes está disponible en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="d5b1a-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="d5b1a-182">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d5b1a-182">Property</span></span> | <span data-ttu-id="d5b1a-183">Descripción</span><span class="sxs-lookup"><span data-stu-id="d5b1a-183">Description</span></span> | <span data-ttu-id="d5b1a-184">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="d5b1a-184">Allowed values</span></span> | <span data-ttu-id="d5b1a-185">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d5b1a-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5b1a-186">query</span><span class="sxs-lookup"><span data-stu-id="d5b1a-186">query</span></span> |<span data-ttu-id="d5b1a-187">Usar datos de tooread de hello consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-187">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d5b1a-188">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-188">SQL query string.</span></span> <span data-ttu-id="d5b1a-189">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="d5b1a-190">Sí</span><span class="sxs-lookup"><span data-stu-id="d5b1a-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a><span data-ttu-id="d5b1a-191">Ejemplo de JSON: tooAzure Blob del almacén de datos de copia de datos ODBC</span><span class="sxs-lookup"><span data-stu-id="d5b1a-191">JSON example: Copy data from ODBC data store tooAzure Blob</span></span>
<span data-ttu-id="d5b1a-192">Este ejemplo proporciona definiciones de JSON que puede usar toocreate una canalización mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d5b1a-192">This example provides JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d5b1a-193">Muestra cómo del origen de datos de toocopy desde un ODBC tooan almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-193">It shows how toocopy data from an ODBC source tooan Azure Blob Storage.</span></span> <span data-ttu-id="d5b1a-194">Sin embargo, los datos pueden ser tooany copiada de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-194">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="d5b1a-195">ejemplo de Hola tiene Hola después de entidades de la factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="d5b1a-195">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="d5b1a-196">Un servicio vinculado del tipo [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d5b1a-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="d5b1a-197">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="d5b1a-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d5b1a-198">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d5b1a-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="d5b1a-199">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d5b1a-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="d5b1a-200">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d5b1a-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d5b1a-201">ejemplo de Hola copia datos de un resultado de consulta en un blob de tooa del almacén de datos ODBC cada hora.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-201">hello sample copies data from a query result in an ODBC data store tooa blob every hour.</span></span> <span data-ttu-id="d5b1a-202">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-202">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="d5b1a-203">Como primer paso, configurar la puerta de enlace de administración de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-203">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="d5b1a-204">instrucciones de Hola se encuentran en hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-204">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="d5b1a-205">**Servicio vinculado de ODBC** en este ejemplo utiliza la autenticación básica de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-205">**ODBC linked service** This example uses hello Basic authentication.</span></span> <span data-ttu-id="d5b1a-206">Consulte la sección [Propiedades del servicio vinculado de ODBC](#linked-service-properties) para conocer los diferentes tipos de autenticación que se pueden usar.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="d5b1a-207">**Servicio vinculado de Almacenamiento de Azure**</span><span class="sxs-lookup"><span data-stu-id="d5b1a-207">**Azure Storage linked service**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
    }
}
```

<span data-ttu-id="d5b1a-208">**Conjunto de datos de entrada de ODBC**</span><span class="sxs-lookup"><span data-stu-id="d5b1a-208">**ODBC input dataset**</span></span>

<span data-ttu-id="d5b1a-209">ejemplo de Hola se da por supuesto que ha creado una tabla "MyTable" en una base de datos ODBC y contiene una columna denominada "timestampcolumn" para los datos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-209">hello sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="d5b1a-210">Establecer "externo": "true" informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-210">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="d5b1a-211">**Conjunto de datos de salida de blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="d5b1a-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="d5b1a-212">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="d5b1a-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d5b1a-213">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="d5b1a-214">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


<span data-ttu-id="d5b1a-215">**Actividad de copia en una canalización con origen ODBC (RelationalSource) y receptor blob (BlobSink)**</span><span class="sxs-lookup"><span data-stu-id="d5b1a-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="d5b1a-216">canalización de Hello contiene una actividad de copia que esté configurado toouse estos conjuntos de datos de entrada y salidas o toorun programada cada hora.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-216">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="d5b1a-217">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**RelationalSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="d5b1a-218">consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos Hola Hola más allá de hora toocopy.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="d5b1a-219">Asignación de tipos para ODBC</span><span class="sxs-lookup"><span data-stu-id="d5b1a-219">Type mapping for ODBC</span></span>
<span data-ttu-id="d5b1a-220">Como se mencionó en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, actividad de copia realiza conversiones de tipos automática de tipos de toosink de tipos de origen con hello enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="d5b1a-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="d5b1a-221">Convertir del tipo de origen nativo tipos too.NET</span><span class="sxs-lookup"><span data-stu-id="d5b1a-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="d5b1a-222">Convertir el tipo de receptor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="d5b1a-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="d5b1a-223">Al mover los datos de almacenes de datos ODBC, tipos de datos ODBC son tipos de too.NET asignado como se mencionó en hello [asignaciones de tipos de datos de ODBC](https://msdn.microsoft.com/library/cc668763.aspx) tema.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-223">When moving data from ODBC data stores, ODBC data types are mapped too.NET types as mentioned in hello [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="d5b1a-224">Asignar columnas de origen toosink</span><span class="sxs-lookup"><span data-stu-id="d5b1a-224">Map source toosink columns</span></span>
<span data-ttu-id="d5b1a-225">toolearn acerca de la asignación de columnas en toocolumns de conjunto de datos de origen en el conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d5b1a-225">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="d5b1a-226">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="d5b1a-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="d5b1a-227">Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-227">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="d5b1a-228">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="d5b1a-229">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="d5b1a-230">Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-230">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="d5b1a-231">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="d5b1a-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="d5b1a-232">Almacén GE Historian</span><span class="sxs-lookup"><span data-stu-id="d5b1a-232">GE Historian store</span></span>
<span data-ttu-id="d5b1a-233">Crear un toolink de servicio ODBC vinculada una [Proficy en GE historia (ahora en historia GE)](http://www.geautomation.com/products/proficy-historian) tooan factoría de datos de Azure del almacén de datos tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="d5b1a-233">You create an ODBC linked service toolink a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store tooan Azure data factory as shown in hello following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="d5b1a-234">Instalar Data Management Gateway en un equipo local y registrar la puerta de enlace de hello con el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-234">Install Data Management Gateway on an on-premises machine and register hello gateway with hello portal.</span></span> <span data-ttu-id="d5b1a-235">puerta de enlace de Hello instalada en el equipo local utiliza el controlador ODBC de Hola para en historia GE tooconnect toohello almacén de datos en historia GE.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-235">hello gateway installed on your on-premises computer uses hello ODBC driver for GE Historian tooconnect toohello GE Historian data store.</span></span> <span data-ttu-id="d5b1a-236">Por lo tanto, instalar a controladores de hello si aún no está instalado en la máquina de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-236">Therefore, install hello driver if it is not already installed on hello gateway machine.</span></span> <span data-ttu-id="d5b1a-237">Consulte la sección [Habilitación de la conectividad](#enabling-connectivity) para más información.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="d5b1a-238">Antes de usar hello en historia GE almacenar en una solución de factoría de datos, compruebe si la puerta de enlace de hello puede conectarse toohello almacén de datos siguiendo las instrucciones en la sección siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-238">Before you use hello GE Historian store in a Data Factory solution, verify whether hello gateway can connect toohello data store using instructions in hello next section.</span></span>

<span data-ttu-id="d5b1a-239">Leer el artículo de Hola desde el principio de Hola para obtener una descripción detallada del uso de datos ODBC se almacena como almacenes de datos de origen en una operación de copia.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-239">Read hello article from hello beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="d5b1a-240">Solución de problemas de conectividad</span><span class="sxs-lookup"><span data-stu-id="d5b1a-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="d5b1a-241">problemas de conexión de tootroubleshoot, usar hello **diagnósticos** ficha de **Administrador de configuración de Data Management Gateway**.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-241">tootroubleshoot connection issues, use hello **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="d5b1a-242">Inicie el **Administrador de configuración de Data Management Gateway**.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="d5b1a-243">Se puede ejecutar para la búsqueda de "C:\Program Files\Microsoft datos administración Gateway\1.0\Shared\ConfigManager.exe" directamente (o) **puerta de enlace** toofind un vínculo demasiado**Microsoft Data Management Gateway** aplicación tal como se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** toofind a link too**Microsoft Data Management Gateway** application as shown in hello following image.</span></span>

    ![Buscar puerta de enlace](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="d5b1a-245">Cambiar toohello **diagnósticos** ficha.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-245">Switch toohello **Diagnostics** tab.</span></span>

    ![Diagnóstico de puerta de enlace](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="d5b1a-247">Seleccione hello **tipo** (servicio vinculado) del almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-247">Select hello **type** of data store (linked service).</span></span>
4. <span data-ttu-id="d5b1a-248">Especifique **autenticación** y escriba **credenciales** (o) Especifique **cadena de conexión** que es el almacén de datos de uso tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used tooconnect toohello data store.</span></span>
5. <span data-ttu-id="d5b1a-249">Haga clic en **Probar conexión** tootest Hola conexión toohello almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-249">Click **Test connection** tootest hello connection toohello data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d5b1a-250">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="d5b1a-250">Performance and Tuning</span></span>
<span data-ttu-id="d5b1a-251">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="d5b1a-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
