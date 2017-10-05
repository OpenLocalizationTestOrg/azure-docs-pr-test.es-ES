---
title: "Movimiento de datos desde orígenes de datos ODBC | Microsoft Docs"
description: "Obtenga información sobre cómo mover datos desde almacenes de datos ODBC mediante Factoría de datos de Azure."
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
ms.openlocfilehash: 269d9802ca4a6a16dbf9021929fe21104cb431f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="19b08-103">Movimiento de datos desde almacenes de datos ODBC mediante Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="19b08-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="19b08-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para mover datos desde un almacén de datos ODBC local.</span><span class="sxs-lookup"><span data-stu-id="19b08-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises ODBC data store.</span></span> <span data-ttu-id="19b08-105">Se basa en la información general ofrecida en el artículo [Actividades de movimiento de datos](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="19b08-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="19b08-106">Puede copiar datos de un almacén de datos ODBC a cualquier almacén de datos receptor admitido.</span><span class="sxs-lookup"><span data-stu-id="19b08-106">You can copy data from an ODBC data store to any supported sink data store.</span></span> <span data-ttu-id="19b08-107">Consulte la tabla de [almacenes de datos compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para ver una lista de almacenes de datos que la actividad de copia admite como receptores.</span><span class="sxs-lookup"><span data-stu-id="19b08-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="19b08-108">Data Factory solo admite actualmente el movimiento de datos de un almacén de datos ODBC a otros almacenes de datos, pero no viceversa.</span><span class="sxs-lookup"><span data-stu-id="19b08-108">Data factory currently supports only moving data from an ODBC data store to other data stores, but not for moving data from other data stores to an ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="19b08-109">Habilitación de la conectividad</span><span class="sxs-lookup"><span data-stu-id="19b08-109">Enabling connectivity</span></span>
<span data-ttu-id="19b08-110">El servicio Factoría de datos admite la conexión a orígenes ODBC locales mediante Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="19b08-110">Data Factory service supports connecting to on-premises ODBC sources using the Data Management Gateway.</span></span> <span data-ttu-id="19b08-111">Consulte el artículo sobre cómo [mover datos entre ubicaciones locales y la nube](data-factory-move-data-between-onprem-and-cloud.md) para obtener información acerca de Data Management Gateway, así como instrucciones paso a paso sobre cómo configurar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="19b08-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="19b08-112">Use la puerta de enlace para conectar con un almacén de datos ODBC, incluso si está hospedado en una máquina virtual de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="19b08-112">Use the gateway to connect to an ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="19b08-113">Puede instalar la puerta de enlace en el mismo equipo local o en la máquina virtual de Azure como almacén de datos ODBC.</span><span class="sxs-lookup"><span data-stu-id="19b08-113">You can install the gateway on the same on-premises machine or the Azure VM as the ODBC data store.</span></span> <span data-ttu-id="19b08-114">Sin embargo, se recomienda que instale la puerta de enlace en un equipo o máquina virtual IaaS de Azure independiente para evitar la contención de recursos y mejorar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="19b08-114">However, we recommend that you install the gateway on a separate machine/Azure IaaS VM to avoid resource contention and for better performance.</span></span> <span data-ttu-id="19b08-115">Al instalar la puerta de enlace en una máquina independiente, la máquina debería poder acceder a la máquina con el almacén de datos ODBC.</span><span class="sxs-lookup"><span data-stu-id="19b08-115">When you install the gateway on a separate machine, the machine should be able to access the machine with the ODBC data store.</span></span>

<span data-ttu-id="19b08-116">Aparte de Data Management Gateway, también debe instalar el controlador ODBC para el almacén de datos en la máquina de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="19b08-116">Apart from the Data Management Gateway, you also need to install the ODBC driver for the data store on the gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="19b08-117">Consulte [Solución de problemas de la puerta de enlace](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para obtener sugerencias para solucionar problemas de conexión o puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="19b08-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="19b08-118">Introducción</span><span class="sxs-lookup"><span data-stu-id="19b08-118">Getting started</span></span>
<span data-ttu-id="19b08-119">Puede crear una canalización con una actividad de copia que mueva datos desde un almacén de datos ODBC mediante diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="19b08-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="19b08-120">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="19b08-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="19b08-121">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="19b08-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="19b08-122">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="19b08-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="19b08-123">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="19b08-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="19b08-124">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="19b08-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="19b08-125">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="19b08-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="19b08-126">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="19b08-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="19b08-127">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="19b08-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="19b08-128">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="19b08-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="19b08-129">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="19b08-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="19b08-130">Si desea obtener un ejemplo con definiciones de JSON para entidades de Data Factory que se utilizan con el fin de copiar los datos desde un almacén de datos ODBC, consulte la sección [Ejemplo de JSON: Copia de datos de un almacén de datos ODBC a un blob de Azure](#json-example-copy-data-from-odbc-data-store-to-azure-blob) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="19b08-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an ODBC data store, see [JSON example: Copy data from ODBC data store to Azure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="19b08-131">Las secciones siguientes proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de un almacén de datos ODBC:</span><span class="sxs-lookup"><span data-stu-id="19b08-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to ODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="19b08-132">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="19b08-132">Linked service properties</span></span>
<span data-ttu-id="19b08-133">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio vinculado de ODBC.</span><span class="sxs-lookup"><span data-stu-id="19b08-133">The following table provides description for JSON elements specific to ODBC linked service.</span></span>

| <span data-ttu-id="19b08-134">Propiedad</span><span class="sxs-lookup"><span data-stu-id="19b08-134">Property</span></span> | <span data-ttu-id="19b08-135">Descripción</span><span class="sxs-lookup"><span data-stu-id="19b08-135">Description</span></span> | <span data-ttu-id="19b08-136">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19b08-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19b08-137">type</span><span class="sxs-lookup"><span data-stu-id="19b08-137">type</span></span> |<span data-ttu-id="19b08-138">La propiedad type tiene que establecerse en: **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="19b08-138">The type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="19b08-139">Sí</span><span class="sxs-lookup"><span data-stu-id="19b08-139">Yes</span></span> |
| <span data-ttu-id="19b08-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="19b08-140">connectionString</span></span> |<span data-ttu-id="19b08-141">La parte de la credencial de no acceso de la cadena de conexión, así como una credencial cifrada opcional.</span><span class="sxs-lookup"><span data-stu-id="19b08-141">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="19b08-142">Vea ejemplos en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="19b08-142">See examples in the following sections.</span></span> |<span data-ttu-id="19b08-143">Sí</span><span class="sxs-lookup"><span data-stu-id="19b08-143">Yes</span></span> |
| <span data-ttu-id="19b08-144">credential</span><span class="sxs-lookup"><span data-stu-id="19b08-144">credential</span></span> |<span data-ttu-id="19b08-145">La parte de la credencial de acceso de la cadena de conexión especificada en formato de valor de propiedad específico del controlador.</span><span class="sxs-lookup"><span data-stu-id="19b08-145">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="19b08-146">Ejemplo: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span><span class="sxs-lookup"><span data-stu-id="19b08-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="19b08-147">No</span><span class="sxs-lookup"><span data-stu-id="19b08-147">No</span></span> |
| <span data-ttu-id="19b08-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="19b08-148">authenticationType</span></span> |<span data-ttu-id="19b08-149">Tipo de autenticación que se usa para conectarse al almacén de datos ODBC.</span><span class="sxs-lookup"><span data-stu-id="19b08-149">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="19b08-150">Los valores posibles son: Anonymous y Basic.</span><span class="sxs-lookup"><span data-stu-id="19b08-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="19b08-151">Sí</span><span class="sxs-lookup"><span data-stu-id="19b08-151">Yes</span></span> |
| <span data-ttu-id="19b08-152">nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="19b08-152">username</span></span> |<span data-ttu-id="19b08-153">Especifique el nombre de usuario si usa la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="19b08-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="19b08-154">No</span><span class="sxs-lookup"><span data-stu-id="19b08-154">No</span></span> |
| <span data-ttu-id="19b08-155">contraseña</span><span class="sxs-lookup"><span data-stu-id="19b08-155">password</span></span> |<span data-ttu-id="19b08-156">Especifique la contraseña de la cuenta de usuario especificada para el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="19b08-156">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="19b08-157">No</span><span class="sxs-lookup"><span data-stu-id="19b08-157">No</span></span> |
| <span data-ttu-id="19b08-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="19b08-158">gatewayName</span></span> |<span data-ttu-id="19b08-159">Nombre de la puerta de enlace que el servicio Factoría de datos debe usar para conectarse al almacén de datos ODBC.</span><span class="sxs-lookup"><span data-stu-id="19b08-159">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="19b08-160">Sí</span><span class="sxs-lookup"><span data-stu-id="19b08-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="19b08-161">Uso de la autenticación básica</span><span class="sxs-lookup"><span data-stu-id="19b08-161">Using Basic authentication</span></span>

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
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="19b08-162">Uso de la autenticación básica con credenciales cifradas</span><span class="sxs-lookup"><span data-stu-id="19b08-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="19b08-163">Las credenciales se pueden cifrar mediante el cmdlet [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (versión 1.0 de Azure PowerShell) o [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (versión 0.9 o una versión anterior de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="19b08-163">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="19b08-164">Uso de autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="19b08-164">Using Anonymous authentication</span></span>

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


## <a name="dataset-properties"></a><span data-ttu-id="19b08-165">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="19b08-165">Dataset properties</span></span>
<span data-ttu-id="19b08-166">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="19b08-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="19b08-167">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="19b08-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="19b08-168">La sección **typeProperties** es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="19b08-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="19b08-169">La sección typeProperties del conjunto de datos del tipo **RelationalTable** (que incluye el conjunto de datos ODBC) tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="19b08-169">The typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has the following properties</span></span>

| <span data-ttu-id="19b08-170">Propiedad</span><span class="sxs-lookup"><span data-stu-id="19b08-170">Property</span></span> | <span data-ttu-id="19b08-171">Descripción</span><span class="sxs-lookup"><span data-stu-id="19b08-171">Description</span></span> | <span data-ttu-id="19b08-172">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19b08-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="19b08-173">tableName</span><span class="sxs-lookup"><span data-stu-id="19b08-173">tableName</span></span> |<span data-ttu-id="19b08-174">Nombre de la tabla en el almacén de datos ODBC.</span><span class="sxs-lookup"><span data-stu-id="19b08-174">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="19b08-175">Sí</span><span class="sxs-lookup"><span data-stu-id="19b08-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="19b08-176">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="19b08-176">Copy activity properties</span></span>
<span data-ttu-id="19b08-177">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="19b08-177">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="19b08-178">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="19b08-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="19b08-179">Por otra parte, las propiedades disponibles en la sección **typeProperties** de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="19b08-179">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="19b08-180">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="19b08-180">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="19b08-181">En la actividad de copia, si el origen es del tipo **RelationalSource** (que incluye ODBC), las propiedades siguientes están disponibles en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="19b08-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="19b08-182">Propiedad</span><span class="sxs-lookup"><span data-stu-id="19b08-182">Property</span></span> | <span data-ttu-id="19b08-183">Descripción</span><span class="sxs-lookup"><span data-stu-id="19b08-183">Description</span></span> | <span data-ttu-id="19b08-184">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="19b08-184">Allowed values</span></span> | <span data-ttu-id="19b08-185">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="19b08-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="19b08-186">query</span><span class="sxs-lookup"><span data-stu-id="19b08-186">query</span></span> |<span data-ttu-id="19b08-187">Utilice la consulta personalizada para leer los datos.</span><span class="sxs-lookup"><span data-stu-id="19b08-187">Use the custom query to read data.</span></span> |<span data-ttu-id="19b08-188">Cadena de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="19b08-188">SQL query string.</span></span> <span data-ttu-id="19b08-189">Por ejemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="19b08-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="19b08-190">Sí</span><span class="sxs-lookup"><span data-stu-id="19b08-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-to-azure-blob"></a><span data-ttu-id="19b08-191">Ejemplo de JSON: Copia de datos de un almacén de datos ODBC a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="19b08-191">JSON example: Copy data from ODBC data store to Azure Blob</span></span>
<span data-ttu-id="19b08-192">Este ejemplo proporciona definiciones de JSON que puede usar para crear una canalización mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="19b08-192">This example provides JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="19b08-193">En ellos, se muestra cómo copiar datos de un origen ODBC a Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="19b08-193">It shows how to copy data from an ODBC source to an Azure Blob Storage.</span></span> <span data-ttu-id="19b08-194">Sin embargo, los datos se pueden copiar en cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="19b08-194">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="19b08-195">El ejemplo consta de las siguientes entidades de factoría de datos:</span><span class="sxs-lookup"><span data-stu-id="19b08-195">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="19b08-196">Un servicio vinculado del tipo [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="19b08-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="19b08-197">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="19b08-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="19b08-198">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="19b08-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="19b08-199">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="19b08-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="19b08-200">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [RelationalSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="19b08-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="19b08-201">El ejemplo copia los datos del resultado de una consulta en un almacén de datos ODBC en un blob cada hora.</span><span class="sxs-lookup"><span data-stu-id="19b08-201">The sample copies data from a query result in an ODBC data store to a blob every hour.</span></span> <span data-ttu-id="19b08-202">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="19b08-202">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="19b08-203">En primer lugar, configure la puerta de enlace de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="19b08-203">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="19b08-204">Las instrucciones se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="19b08-204">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="19b08-205">**Servicio vinculado de ODBC** En este ejemplo se usa la autenticación básica.</span><span class="sxs-lookup"><span data-stu-id="19b08-205">**ODBC linked service** This example uses the Basic authentication.</span></span> <span data-ttu-id="19b08-206">Consulte la sección [Propiedades del servicio vinculado de ODBC](#linked-service-properties) para conocer los diferentes tipos de autenticación que se pueden usar.</span><span class="sxs-lookup"><span data-stu-id="19b08-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="19b08-207">**Servicio vinculado de Almacenamiento de Azure**</span><span class="sxs-lookup"><span data-stu-id="19b08-207">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="19b08-208">**Conjunto de datos de entrada de ODBC**</span><span class="sxs-lookup"><span data-stu-id="19b08-208">**ODBC input dataset**</span></span>

<span data-ttu-id="19b08-209">El ejemplo asume que ha creado una tabla, "MyTable", en una base de datos ODBC y que contiene una columna denominada "timestampcolumn" para los datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="19b08-209">The sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="19b08-210">Si se establece "external": "true", se informa al servicio Data Factory que el conjunto de datos es externo a Data Factory y que no lo genera ninguna actividad de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="19b08-210">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="19b08-211">**Conjunto de datos de salida de blob de Azure**</span><span class="sxs-lookup"><span data-stu-id="19b08-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="19b08-212">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="19b08-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="19b08-213">La ruta de acceso de la carpeta para el blob se evalúa dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="19b08-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="19b08-214">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="19b08-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


<span data-ttu-id="19b08-215">**Actividad de copia en una canalización con origen ODBC (RelationalSource) y receptor blob (BlobSink)**</span><span class="sxs-lookup"><span data-stu-id="19b08-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="19b08-216">La canalización contiene una actividad de copia que está configurada para usar estos conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="19b08-216">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="19b08-217">En la definición de la canalización JSON, el tipo **source** se establece en **RelationalSource** y el tipo **sink** se establece en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="19b08-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="19b08-218">La consulta SQL especificada para la propiedad **query** selecciona los datos de la última hora que se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="19b08-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="19b08-219">Asignación de tipos para ODBC</span><span class="sxs-lookup"><span data-stu-id="19b08-219">Type mapping for ODBC</span></span>
<span data-ttu-id="19b08-220">Como se mencionó en el artículo sobre [actividades del movimiento de datos](data-factory-data-movement-activities.md) , la actividad de copia realiza conversiones automáticas de los tipos de origen a los tipos de receptor con el siguiente enfoque de dos pasos:</span><span class="sxs-lookup"><span data-stu-id="19b08-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="19b08-221">Conversión de tipos de origen nativos al tipo .NET</span><span class="sxs-lookup"><span data-stu-id="19b08-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="19b08-222">Conversión de tipo .NET al tipo del receptor nativo</span><span class="sxs-lookup"><span data-stu-id="19b08-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="19b08-223">Al mover datos desde almacenes de datos ODBC, los tipos de datos ODBC se asignan a tipos de .NET, tal y como se mencionó en el tema [Asignar tipos de datos ODBC](https://msdn.microsoft.com/library/cc668763.aspx) .</span><span class="sxs-lookup"><span data-stu-id="19b08-223">When moving data from ODBC data stores, ODBC data types are mapped to .NET types as mentioned in the [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="19b08-224">Asignación de columnas de origen a columnas de receptor</span><span class="sxs-lookup"><span data-stu-id="19b08-224">Map source to sink columns</span></span>
<span data-ttu-id="19b08-225">Para obtener más información sobre la asignación de columnas del conjunto de datos de origen a las del conjunto de datos receptor, consulte [Asignación de columnas de conjunto de datos de Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="19b08-225">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="19b08-226">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="19b08-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="19b08-227">Cuando se copian datos desde almacenes de datos relacionales, hay que tener presente la repetibilidad para evitar resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="19b08-227">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="19b08-228">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="19b08-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="19b08-229">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="19b08-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="19b08-230">Cuando se vuelve a ejecutar un segmento, debe asegurarse de que los mismos datos se lean sin importar el número de ejecuciones.</span><span class="sxs-lookup"><span data-stu-id="19b08-230">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="19b08-231">Consulte [Lectura repetible de orígenes relacionales](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="19b08-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="19b08-232">Almacén GE Historian</span><span class="sxs-lookup"><span data-stu-id="19b08-232">GE Historian store</span></span>
<span data-ttu-id="19b08-233">Cree un servicio vinculado ODBC para vincular un almacén de datos [GE Proficy Historian (ahora GE Historian)](http://www.geautomation.com/products/proficy-historian) a Data Factory de Azure, tal y como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="19b08-233">You create an ODBC linked service to link a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store to an Azure data factory as shown in the following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of the GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="19b08-234">Debe instalar Data Management Gateway en un equipo local y registrar la puerta de enlace con el portal.</span><span class="sxs-lookup"><span data-stu-id="19b08-234">Install Data Management Gateway on an on-premises machine and register the gateway with the portal.</span></span> <span data-ttu-id="19b08-235">La puerta de enlace instalada en su equipo local utiliza el controlador ODBC para que GE Historian se conecte al almacén de datos GE Historian.</span><span class="sxs-lookup"><span data-stu-id="19b08-235">The gateway installed on your on-premises computer uses the ODBC driver for GE Historian to connect to the GE Historian data store.</span></span> <span data-ttu-id="19b08-236">Por lo tanto, instale el controlador si no está instalado aún en el equipo de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="19b08-236">Therefore, install the driver if it is not already installed on the gateway machine.</span></span> <span data-ttu-id="19b08-237">Consulte la sección [Habilitación de la conectividad](#enabling-connectivity) para más información.</span><span class="sxs-lookup"><span data-stu-id="19b08-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="19b08-238">Antes de usar el almacén GE Historian en una solución de Data Factory, compruebe si la puerta de enlace puede conectarse al almacén de datos mediante instrucciones en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="19b08-238">Before you use the GE Historian store in a Data Factory solution, verify whether the gateway can connect to the data store using instructions in the next section.</span></span>

<span data-ttu-id="19b08-239">Lea el artículo desde el principio para obtener información general detallada de uso de almacenes de datos ODBC como almacenes de datos de origen en una operación de copia.</span><span class="sxs-lookup"><span data-stu-id="19b08-239">Read the article from the beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="19b08-240">Solución de problemas de conectividad</span><span class="sxs-lookup"><span data-stu-id="19b08-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="19b08-241">Use la pestaña **Diagnósticos** del **Administrador de configuración de Data Management Gateway**para solucionar problemas de conexión.</span><span class="sxs-lookup"><span data-stu-id="19b08-241">To troubleshoot connection issues, use the **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="19b08-242">Inicie el **Administrador de configuración de Data Management Gateway**.</span><span class="sxs-lookup"><span data-stu-id="19b08-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="19b08-243">Puede ejecutar C:\Archivos de programa\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe directamente, o bien buscar **Gateway** para encontrar un vínculo a la aplicación **Microsoft Data Management Gateway**, tal y como se muestra en la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="19b08-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** to find a link to **Microsoft Data Management Gateway** application as shown in the following image.</span></span>

    ![Buscar puerta de enlace](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="19b08-245">Cambie a la pestaña **Diagnósticos** .</span><span class="sxs-lookup"><span data-stu-id="19b08-245">Switch to the **Diagnostics** tab.</span></span>

    ![Diagnóstico de puerta de enlace](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="19b08-247">Seleccione el **tipo** de almacén de datos (el servicio vinculado).</span><span class="sxs-lookup"><span data-stu-id="19b08-247">Select the **type** of data store (linked service).</span></span>
4. <span data-ttu-id="19b08-248">Especifique la **autenticación** y escriba las **credenciales**, o bien escriba la **cadena de conexión** que se usa para conectarse al almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="19b08-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used to connect to the data store.</span></span>
5. <span data-ttu-id="19b08-249">Haga clic en **Probar conexión** para probar la conexión con el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="19b08-249">Click **Test connection** to test the connection to the data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="19b08-250">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="19b08-250">Performance and Tuning</span></span>
<span data-ttu-id="19b08-251">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="19b08-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
