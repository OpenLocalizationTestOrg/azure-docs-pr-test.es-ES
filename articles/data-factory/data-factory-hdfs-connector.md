---
title: datos de aaaMove de HDFS local | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomove datos desde local HDFS mediante Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a><span data-ttu-id="2aa28-103">Movimiento de datos desde HDFS local mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2aa28-103">Move data from on-premises HDFS using Azure Data Factory</span></span>
<span data-ttu-id="2aa28-104">Este artículo explica cómo toouse Hola actividad de copia de datos de toomove Data Factory de Azure desde un HDFS local.</span><span class="sxs-lookup"><span data-stu-id="2aa28-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises HDFS.</span></span> <span data-ttu-id="2aa28-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="2aa28-106">Puede copiar datos de almacén de datos de receptor HDFS tooany compatible.</span><span class="sxs-lookup"><span data-stu-id="2aa28-106">You can copy data from HDFS tooany supported sink data store.</span></span> <span data-ttu-id="2aa28-107">Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla.</span><span class="sxs-lookup"><span data-stu-id="2aa28-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="2aa28-108">Factoría de datos admite actualmente solo mover datos desde un almacenes de datos de tooother HDFS local, pero no para mover los datos de otros datos tooan almacenes locales HDFS.</span><span class="sxs-lookup"><span data-stu-id="2aa28-108">Data factory currently supports only moving data from an on-premises HDFS tooother data stores, but not for moving data from other data stores tooan on-premises HDFS.</span></span>

> [!NOTE]
> <span data-ttu-id="2aa28-109">Actividad de copia no elimina archivos de origen de Hola cuando este destino toohello copió correctamente.</span><span class="sxs-lookup"><span data-stu-id="2aa28-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="2aa28-110">Si necesita toodelete archivo de código fuente de hello después de una copia correcta, cree un archivo de actividad personalizada toodelete hello y usar actividad hello en la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="2aa28-111">Habilitación de la conectividad</span><span class="sxs-lookup"><span data-stu-id="2aa28-111">Enabling connectivity</span></span>
<span data-ttu-id="2aa28-112">Servicio de factoría de datos admite la conexión HDFS local tooon con hello Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="2aa28-112">Data Factory service supports connecting tooon-premises HDFS using hello Data Management Gateway.</span></span> <span data-ttu-id="2aa28-113">Vea [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) toolearn artículo acerca de la puerta de enlace de datos de administración y las instrucciones paso a paso sobre cómo configurar la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="2aa28-114">Utilice Hola puerta de enlace tooconnect tooHDFS incluso si está hospedado en una máquina virtual de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="2aa28-114">Use hello gateway tooconnect tooHDFS even if it is hosted in an Azure IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="2aa28-115">Asegúrese de Hola que puede tener acceso Data Management Gateway demasiado**todos los** Hola [servidor de nombres de nodo]: [nombre de puerto de nodo] y [servidores de nodos de datos]: [puerto de nodo de datos] de clúster de Hadoop de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-115">Make sure hello Data Management Gateway can access too**ALL** hello [name node server]:[name node port] and [data node servers]:[data node port] of hello Hadoop cluster.</span></span> <span data-ttu-id="2aa28-116">El [puerto de nodo de nombres] predeterminado es 50070 y el [puerto de nodo de datos] es 50075.</span><span class="sxs-lookup"><span data-stu-id="2aa28-116">Default [name node port] is 50070, and default [data node port] is 50075.</span></span>

<span data-ttu-id="2aa28-117">Durante la instalación de puerta de enlace en hello mismo locales máquina o hello Azure VM Hola HDFS, se recomienda que instale la puerta de enlace de hello en un equipo independiente/Azure VM de IaaS.</span><span class="sxs-lookup"><span data-stu-id="2aa28-117">While you can install gateway on hello same on-premises machine or hello Azure VM as hello HDFS, we recommend that you install hello gateway on a separate machine/Azure IaaS VM.</span></span> <span data-ttu-id="2aa28-118">Al tener la puerta de enlace en un equipo independiente, se reduce la contención de recursos y se mejora el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="2aa28-118">Having gateway on a separate machine reduces resource contention and improves performance.</span></span> <span data-ttu-id="2aa28-119">Cuando se instala la puerta de enlace de hello en un equipo independiente, máquina Hola debe ser capaz de tooaccess máquina de hello con hello HDFS.</span><span class="sxs-lookup"><span data-stu-id="2aa28-119">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello HDFS.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2aa28-120">Introducción</span><span class="sxs-lookup"><span data-stu-id="2aa28-120">Getting started</span></span>
<span data-ttu-id="2aa28-121">Puede crear una canalización con actividad de copia que mueva los datos desde un origen de HDFS mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="2aa28-121">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span></span>

<span data-ttu-id="2aa28-122">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="2aa28-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="2aa28-123">Vea [Tutorial: crear una canalización mediante el Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial sobre cómo crear una canalización mediante el Asistente para datos de copia de hello rápido.</span><span class="sxs-lookup"><span data-stu-id="2aa28-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="2aa28-124">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="2aa28-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2aa28-125">Vea [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="2aa28-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="2aa28-126">Si usa herramientas de Hola o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="2aa28-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="2aa28-127">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="2aa28-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="2aa28-128">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="2aa28-129">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="2aa28-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="2aa28-130">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="2aa28-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="2aa28-131">Al usar herramientas y API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="2aa28-132">Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos HDFS, consulte [ejemplo de JSON: copiar los datos de tooAzure HDFS local Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="2aa28-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS tooAzure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span></span>

<span data-ttu-id="2aa28-133">Hola las secciones siguientes proporciona detalles acerca de las propiedades JSON que son entidades de factoría de datos usado toodefine tooHDFS específico:</span><span class="sxs-lookup"><span data-stu-id="2aa28-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooHDFS:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2aa28-134">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="2aa28-134">Linked service properties</span></span>
<span data-ttu-id="2aa28-135">Un servicio vinculado vincula una factoría de datos de tooa de almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="2aa28-135">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="2aa28-136">Crear un servicio vinculado de tipo **Hdfs** toolink una factoría de datos de tooyour HDFS local.</span><span class="sxs-lookup"><span data-stu-id="2aa28-136">You create a linked service of type **Hdfs** toolink an on-premises HDFS tooyour data factory.</span></span> <span data-ttu-id="2aa28-137">Hello en la tabla siguiente proporciona la descripción del servicio JSON elementos específicos tooHDFS vinculado.</span><span class="sxs-lookup"><span data-stu-id="2aa28-137">hello following table provides description for JSON elements specific tooHDFS linked service.</span></span>

| <span data-ttu-id="2aa28-138">Propiedad</span><span class="sxs-lookup"><span data-stu-id="2aa28-138">Property</span></span> | <span data-ttu-id="2aa28-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="2aa28-139">Description</span></span> | <span data-ttu-id="2aa28-140">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2aa28-140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2aa28-141">type</span><span class="sxs-lookup"><span data-stu-id="2aa28-141">type</span></span> |<span data-ttu-id="2aa28-142">propiedad de tipo Hello debe establecerse en: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="2aa28-142">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="2aa28-143">Sí</span><span class="sxs-lookup"><span data-stu-id="2aa28-143">Yes</span></span> |
| <span data-ttu-id="2aa28-144">URL</span><span class="sxs-lookup"><span data-stu-id="2aa28-144">Url</span></span> |<span data-ttu-id="2aa28-145">Dirección URL toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="2aa28-145">URL toohello HDFS</span></span> |<span data-ttu-id="2aa28-146">Sí</span><span class="sxs-lookup"><span data-stu-id="2aa28-146">Yes</span></span> |
| <span data-ttu-id="2aa28-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="2aa28-147">authenticationType</span></span> |<span data-ttu-id="2aa28-148">Anónima o Windows.</span><span class="sxs-lookup"><span data-stu-id="2aa28-148">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="2aa28-149">toouse **la autenticación Kerberos** para conector HDFS, consulte demasiado[en esta sección](#use-kerberos-authentication-for-hdfs-connector) tooset del entorno local en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="2aa28-149">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="2aa28-150">Sí</span><span class="sxs-lookup"><span data-stu-id="2aa28-150">Yes</span></span> |
| <span data-ttu-id="2aa28-151">userName</span><span class="sxs-lookup"><span data-stu-id="2aa28-151">userName</span></span> |<span data-ttu-id="2aa28-152">Nombre de usuario para la autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="2aa28-152">Username for Windows authentication.</span></span> |<span data-ttu-id="2aa28-153">Sí (para la autenticación de Windows)</span><span class="sxs-lookup"><span data-stu-id="2aa28-153">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="2aa28-154">contraseña</span><span class="sxs-lookup"><span data-stu-id="2aa28-154">password</span></span> |<span data-ttu-id="2aa28-155">Contraseña para la autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="2aa28-155">Password for Windows authentication.</span></span> |<span data-ttu-id="2aa28-156">Sí (para la autenticación de Windows)</span><span class="sxs-lookup"><span data-stu-id="2aa28-156">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="2aa28-157">gatewayName</span><span class="sxs-lookup"><span data-stu-id="2aa28-157">gatewayName</span></span> |<span data-ttu-id="2aa28-158">Nombre de puerta de enlace de Hola Hola servicio Data Factory debe usar tooconnect toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="2aa28-158">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="2aa28-159">Sí</span><span class="sxs-lookup"><span data-stu-id="2aa28-159">Yes</span></span> |
| <span data-ttu-id="2aa28-160">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="2aa28-160">encryptedCredential</span></span> |<span data-ttu-id="2aa28-161">[Nueva AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) salida de credenciales de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="2aa28-162">No</span><span class="sxs-lookup"><span data-stu-id="2aa28-162">No</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="2aa28-163">Uso de autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="2aa28-163">Using Anonymous authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a><span data-ttu-id="2aa28-164">Uso de autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="2aa28-164">Using Windows authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a><span data-ttu-id="2aa28-165">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="2aa28-165">Dataset properties</span></span>
<span data-ttu-id="2aa28-166">Para obtener una lista completa de secciones y propiedades disponibles para definir conjuntos de datos, vea hello [crear conjuntos de datos](data-factory-create-datasets.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="2aa28-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2aa28-167">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="2aa28-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2aa28-168">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="2aa28-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="2aa28-169">sección typeProperties Hello para el conjunto de datos de tipo **FileShare** (que incluye el conjunto de datos HDFS) tiene Hola propiedades siguientes</span><span class="sxs-lookup"><span data-stu-id="2aa28-169">hello typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has hello following properties</span></span>

| <span data-ttu-id="2aa28-170">Propiedad</span><span class="sxs-lookup"><span data-stu-id="2aa28-170">Property</span></span> | <span data-ttu-id="2aa28-171">Descripción</span><span class="sxs-lookup"><span data-stu-id="2aa28-171">Description</span></span> | <span data-ttu-id="2aa28-172">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2aa28-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2aa28-173">folderPath</span><span class="sxs-lookup"><span data-stu-id="2aa28-173">folderPath</span></span> |<span data-ttu-id="2aa28-174">Carpeta de toohello de ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="2aa28-174">Path toohello folder.</span></span> <span data-ttu-id="2aa28-175">Ejemplo: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="2aa28-175">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="2aa28-176">Utilice el carácter de escape ' \ ' para los caracteres especiales en la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-176">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="2aa28-177">Por ejemplo: para folder\subfolder, especifique la carpeta\\\\subcarpeta y para d:\samplefolder, especifique d:\\\\samplefolder.</span><span class="sxs-lookup"><span data-stu-id="2aa28-177">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="2aa28-178">Puede combinar esta propiedad con **partitionBy** toohave de rutas de acceso de carpeta según fechas y horas de inicio y fin.</span><span class="sxs-lookup"><span data-stu-id="2aa28-178">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="2aa28-179">Sí</span><span class="sxs-lookup"><span data-stu-id="2aa28-179">Yes</span></span> |
| <span data-ttu-id="2aa28-180">fileName</span><span class="sxs-lookup"><span data-stu-id="2aa28-180">fileName</span></span> |<span data-ttu-id="2aa28-181">Especifique el nombre de hello del archivo hello en hello **folderPath** si desea Hola tabla toorefer tooa archivo específico en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-181">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="2aa28-182">Si no especifica ningún valor para esta propiedad, tabla de hello señala tooall archivos en la carpeta de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-182">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="2aa28-183">Cuando no se especifica el nombre de archivo para un conjunto de datos de salida, nombre de hello del archivo hello genera sería Hola siguiendo este formato:</span><span class="sxs-lookup"><span data-stu-id="2aa28-183">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="2aa28-184">Data<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="2aa28-184">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="2aa28-185">No</span><span class="sxs-lookup"><span data-stu-id="2aa28-185">No</span></span> |
| <span data-ttu-id="2aa28-186">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="2aa28-186">partitionedBy</span></span> |<span data-ttu-id="2aa28-187">partitionedBy puede ser usado toospecify un folderPath dinámico, nombre de archivo de datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="2aa28-187">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="2aa28-188">Por ejemplo, folderPath se parametriza para cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="2aa28-188">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="2aa28-189">No</span><span class="sxs-lookup"><span data-stu-id="2aa28-189">No</span></span> |
| <span data-ttu-id="2aa28-190">formato</span><span class="sxs-lookup"><span data-stu-id="2aa28-190">format</span></span> | <span data-ttu-id="2aa28-191">se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="2aa28-191">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="2aa28-192">Conjunto hello **tipo** propiedad en formato tooone de estos valores.</span><span class="sxs-lookup"><span data-stu-id="2aa28-192">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="2aa28-193">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="2aa28-193">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="2aa28-194">Si desea demasiado**copiar archivos como-es** entre los almacenes basados en archivos (copia binaria), omita la sección de formato de hello en ambas definiciones de conjunto de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="2aa28-194">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="2aa28-195">No</span><span class="sxs-lookup"><span data-stu-id="2aa28-195">No</span></span> |
| <span data-ttu-id="2aa28-196">compresión</span><span class="sxs-lookup"><span data-stu-id="2aa28-196">compression</span></span> | <span data-ttu-id="2aa28-197">Especificar tipo de Hola y el nivel de compresión para datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-197">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="2aa28-198">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="2aa28-198">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="2aa28-199">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="2aa28-199">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="2aa28-200">Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="2aa28-200">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="2aa28-201">No</span><span class="sxs-lookup"><span data-stu-id="2aa28-201">No</span></span> |

> [!NOTE]
> <span data-ttu-id="2aa28-202">filename y fileFilter no pueden usarse simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="2aa28-202">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="2aa28-203">Uso de la propiedad partitionedBy</span><span class="sxs-lookup"><span data-stu-id="2aa28-203">Using partionedBy property</span></span>
<span data-ttu-id="2aa28-204">Como se mencionó en la sección anterior de hello, puede especificar un folderPath dinámica y el nombre de archivo de datos de serie temporal con hello **partitionedBy** propiedad, [funciones de factoría de datos y las variables del sistema hello](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="2aa28-204">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="2aa28-205">toolearn más información acerca de los conjuntos de datos de series de tiempo, la programación y sectores, consulte [crear conjuntos de datos](data-factory-create-datasets.md), [ejecución y programación](data-factory-scheduling-and-execution.md), y [crear canalizaciones](data-factory-create-pipelines.md) artículos.</span><span class="sxs-lookup"><span data-stu-id="2aa28-205">toolearn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="2aa28-206">Muestra 1:</span><span class="sxs-lookup"><span data-stu-id="2aa28-206">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="2aa28-207">En este ejemplo {Slice} se reemplaza con el valor de Hola de variable del sistema SliceStart factoría de datos en formato de hello (AAAAMMDDHH) especificado.</span><span class="sxs-lookup"><span data-stu-id="2aa28-207">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="2aa28-208">Hola SliceStart refiere a tiempo toostart de segmento de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-208">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="2aa28-209">Hola folderPath es diferente para cada segmento.</span><span class="sxs-lookup"><span data-stu-id="2aa28-209">hello folderPath is different for each slice.</span></span> <span data-ttu-id="2aa28-210">Por ejemplo: wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="2aa28-210">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="2aa28-211">Ejemplo 2:</span><span class="sxs-lookup"><span data-stu-id="2aa28-211">Sample 2:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="2aa28-212">En este ejemplo, year, month, day y time de SliceStart se extraen en variables independientes que se usan en las propiedades folderPath y fileName.</span><span class="sxs-lookup"><span data-stu-id="2aa28-212">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="2aa28-213">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="2aa28-213">Copy activity properties</span></span>
<span data-ttu-id="2aa28-214">Para obtener una lista completa de secciones y propiedades disponibles para la definición de actividades, vea hello [crear canalizaciones](data-factory-create-pipelines.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="2aa28-214">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2aa28-215">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="2aa28-215">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="2aa28-216">Mientras que las propiedades disponibles en la sección de typeProperties de Hola de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="2aa28-216">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="2aa28-217">Para la actividad de copia, varían en función de los tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="2aa28-217">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="2aa28-218">Para la actividad de copia, cuando el origen es de tipo **FileSystemSource** Hola propiedades siguientes está disponible en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="2aa28-218">For Copy Activity, when source is of type **FileSystemSource** hello following properties are available in typeProperties section:</span></span>

<span data-ttu-id="2aa28-219">**FileSystemSource** admite Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="2aa28-219">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="2aa28-220">Propiedad</span><span class="sxs-lookup"><span data-stu-id="2aa28-220">Property</span></span> | <span data-ttu-id="2aa28-221">Descripción</span><span class="sxs-lookup"><span data-stu-id="2aa28-221">Description</span></span> | <span data-ttu-id="2aa28-222">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="2aa28-222">Allowed values</span></span> | <span data-ttu-id="2aa28-223">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2aa28-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2aa28-224">recursive</span><span class="sxs-lookup"><span data-stu-id="2aa28-224">recursive</span></span> |<span data-ttu-id="2aa28-225">Indica si hello es leer los datos de forma recursiva de subcarpetas de Hola o solo de carpeta especificada de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-225">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="2aa28-226">True, False (predeterminada)</span><span class="sxs-lookup"><span data-stu-id="2aa28-226">True, False (default)</span></span> |<span data-ttu-id="2aa28-227">No</span><span class="sxs-lookup"><span data-stu-id="2aa28-227">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="2aa28-228">Formatos de archivo y de compresión admitidos</span><span class="sxs-lookup"><span data-stu-id="2aa28-228">Supported file and compression formats</span></span>
<span data-ttu-id="2aa28-229">Consulte los detalles en [Formatos de compresión y de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="2aa28-229">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a><span data-ttu-id="2aa28-230">Ejemplo de JSON: copiar los datos de tooAzure HDFS local Blob</span><span class="sxs-lookup"><span data-stu-id="2aa28-230">JSON example: Copy data from on-premises HDFS tooAzure Blob</span></span>
<span data-ttu-id="2aa28-231">Este ejemplo se muestra cómo toocopy datos desde un tooAzure HDFS local almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="2aa28-231">This sample shows how toocopy data from an on-premises HDFS tooAzure Blob Storage.</span></span> <span data-ttu-id="2aa28-232">Sin embargo, se pueden copiar datos **directamente** tooany de receptores de hello indicadas [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) utilizando Hola actividad de copia de factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2aa28-232">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="2aa28-233">ejemplo de Hola proporciona definiciones de JSON para hello siguiendo las entidades de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="2aa28-233">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="2aa28-234">Puede usar estos toocreate definiciones una toocopy de datos de canalización de HDFS tooAzure almacenamiento de blobs mediante [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2aa28-234">You can use these definitions toocreate a pipeline toocopy data from HDFS tooAzure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

1. <span data-ttu-id="2aa28-235">Un servicio vinculado del tipo [OnPremisesHdfs](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2aa28-235">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span></span>
2. <span data-ttu-id="2aa28-236">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="2aa28-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="2aa28-237">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2aa28-237">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
4. <span data-ttu-id="2aa28-238">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2aa28-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="2aa28-239">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [FileSystemSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2aa28-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="2aa28-240">ejemplo de Hola copia datos de un tooan HDFS local blobs de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="2aa28-240">hello sample copies data from an on-premises HDFS tooan Azure blob every hour.</span></span> <span data-ttu-id="2aa28-241">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="2aa28-241">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="2aa28-242">Como primer paso, configurar la puerta de enlace de administración de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-242">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="2aa28-243">Hola instrucciones de hello [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="2aa28-243">hello instructions in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="2aa28-244">**Servicio vinculado de HDFS:** en este ejemplo usa Hola autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="2aa28-244">**HDFS linked service:** This example uses hello Windows authentication.</span></span> <span data-ttu-id="2aa28-245">Consulte la sección [Propiedades del servicio vinculado de HDFS](#linked-service-properties) para conocer los diferentes tipos de autenticación que se pueden usar.</span><span class="sxs-lookup"><span data-stu-id="2aa28-245">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="2aa28-246">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="2aa28-246">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="2aa28-247">**Conjunto de datos de entrada de HDFS:** este conjunto de datos hace referencia a carpeta HDFS toohello DataTransfer/UnitTest /.</span><span class="sxs-lookup"><span data-stu-id="2aa28-247">**HDFS input dataset:** This dataset refers toohello HDFS folder DataTransfer/UnitTest/.</span></span> <span data-ttu-id="2aa28-248">canalización de Hello copia todos los archivos de hello en este destino de carpeta toohello.</span><span class="sxs-lookup"><span data-stu-id="2aa28-248">hello pipeline copies all hello files in this folder toohello destination.</span></span>

<span data-ttu-id="2aa28-249">Establecer "externo": "true" informa a servicio de factoría de datos de hello ese conjunto de datos de hello es factoría de datos de toohello externo y no se crea una actividad de factoría de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-249">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

<span data-ttu-id="2aa28-250">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="2aa28-250">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="2aa28-251">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="2aa28-251">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="2aa28-252">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="2aa28-252">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="2aa28-253">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de tiempo de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-253">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="2aa28-254">**Actividad de copia en una canalización con origen del sistema de archivos y receptor blob:**</span><span class="sxs-lookup"><span data-stu-id="2aa28-254">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="2aa28-255">canalización de Hello contiene una actividad de copia que esté configurado toouse estos conjuntos de datos de entrada y salidas o toorun programada cada hora.</span><span class="sxs-lookup"><span data-stu-id="2aa28-255">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="2aa28-256">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**FileSystemSource** y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2aa28-256">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="2aa28-257">consulta SQL Hola especificada para hello **consulta** propiedad selecciona datos Hola Hola más allá de hora toocopy.</span><span class="sxs-lookup"><span data-stu-id="2aa28-257">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="2aa28-258">Uso de autenticación Kerberos para el conector HDFS</span><span class="sxs-lookup"><span data-stu-id="2aa28-258">Use Kerberos authentication for HDFS connector</span></span>
<span data-ttu-id="2aa28-259">Hay dos tooset de opciones de entorno local de hello así como toouse la autenticación Kerberos en el conector de HDFS.</span><span class="sxs-lookup"><span data-stu-id="2aa28-259">There are two options tooset up hello on-premises environment so as toouse Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="2aa28-260">Puede elegir Hola uno se adapta mejor a su caso.</span><span class="sxs-lookup"><span data-stu-id="2aa28-260">You can choose hello one better fits your case.</span></span>
* <span data-ttu-id="2aa28-261">Opción 1: [Unirse a la máquina de puerta de enlace en el dominio Kerberos](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="2aa28-261">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="2aa28-262">Opción 2: [Habilitar la confianza mutua entre el dominio de Windows y el dominio Kerberos](#kerberos-mutual-trust)</span><span class="sxs-lookup"><span data-stu-id="2aa28-262">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <span data-ttu-id="2aa28-263"><a name="kerberos-join-realm"></a>Opción 1: Unirse a la máquina de puerta de enlace en el dominio Kerberos</span><span class="sxs-lookup"><span data-stu-id="2aa28-263"><a name="kerberos-join-realm"></a>Option 1: Join gateway machine in Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="2aa28-264">Requisito:</span><span class="sxs-lookup"><span data-stu-id="2aa28-264">Requirement:</span></span>

* <span data-ttu-id="2aa28-265">máquina de puerta de enlace de Hello necesita dominio Kerberos de toojoin hello y no puede unir a ningún dominio de Windows.</span><span class="sxs-lookup"><span data-stu-id="2aa28-265">hello gateway machine needs toojoin hello Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="2aa28-266">¿Cómo tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="2aa28-266">How tooconfigure:</span></span>

<span data-ttu-id="2aa28-267">**En la máquina de puerta de enlace:**</span><span class="sxs-lookup"><span data-stu-id="2aa28-267">**On gateway machine:**</span></span>

1.  <span data-ttu-id="2aa28-268">Ejecute hello **Ksetup** utilidad tooconfigure Hola servidor KDC de Kerberos o el dominio Kerberos.</span><span class="sxs-lookup"><span data-stu-id="2aa28-268">Run hello **Ksetup** utility tooconfigure hello Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="2aa28-269">máquina de Hello debe configurarse como un miembro de un grupo de trabajo desde un dominio Kerberos que es diferente de un dominio de Windows.</span><span class="sxs-lookup"><span data-stu-id="2aa28-269">hello machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="2aa28-270">Esto puede lograrse estableciendo el dominio Kerberos de Hola y agregar un servidor KDC como sigue.</span><span class="sxs-lookup"><span data-stu-id="2aa28-270">This can be achieved by setting hello Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="2aa28-271">Sustituya *REALM.COM* por su dominio respectivo, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2aa28-271">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="2aa28-272">**Reinicie** máquina Hola después de ejecutar estos 2 comandos.</span><span class="sxs-lookup"><span data-stu-id="2aa28-272">**Restart** hello machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="2aa28-273">Comprobar la configuración de hello con **Ksetup** comando.</span><span class="sxs-lookup"><span data-stu-id="2aa28-273">Verify hello configuration with **Ksetup** command.</span></span> <span data-ttu-id="2aa28-274">salida de Hello será similar:</span><span class="sxs-lookup"><span data-stu-id="2aa28-274">hello output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="2aa28-275">**En Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="2aa28-275">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="2aa28-276">Configure el conector HDFS de hello mediante **autenticación de Windows** junto con Kerberos principal nombre y la contraseña tooconnect toohello HDFS origen de datos.</span><span class="sxs-lookup"><span data-stu-id="2aa28-276">Configure hello HDFS connector using **Windows authentication** together with your Kerberos principal name and password tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="2aa28-277">Compruebe la sección [HDFS Linked Service properties](#linked-service-properties) (Propiedades de servicio vinculado de HDFS) en los detalles de configuración.</span><span class="sxs-lookup"><span data-stu-id="2aa28-277">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <span data-ttu-id="2aa28-278"><a name="kerberos-mutual-trust"></a>Opción 2: Habilitar la confianza mutua entre el dominio de Windows y el dominio Kerberos</span><span class="sxs-lookup"><span data-stu-id="2aa28-278"><a name="kerberos-mutual-trust"></a>Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="2aa28-279">Requisito:</span><span class="sxs-lookup"><span data-stu-id="2aa28-279">Requirement:</span></span>
*   <span data-ttu-id="2aa28-280">máquina de puerta de enlace de Hello debe unirse a un dominio de Windows.</span><span class="sxs-lookup"><span data-stu-id="2aa28-280">hello gateway machine must join a Windows domain.</span></span>
*   <span data-ttu-id="2aa28-281">Necesita una configuración del controlador de dominio de permiso tooupdate Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-281">You need permission tooupdate hello domain controller's settings.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="2aa28-282">¿Cómo tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="2aa28-282">How tooconfigure:</span></span>

> [!NOTE]
> <span data-ttu-id="2aa28-283">Reemplazar dominio.com y AD.COM en hello sigue el tutorial con su propio controlador de dominio Kerberos y el dominio respectivo según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2aa28-283">Replace REALM.COM and AD.COM in hello following tutorial with your own respective realm and domain controller as needed.</span></span>

<span data-ttu-id="2aa28-284">**En el servidor KDC:**</span><span class="sxs-lookup"><span data-stu-id="2aa28-284">**On KDC server:**</span></span>

1.  <span data-ttu-id="2aa28-285">Editar configuración de KDC de hello en **krb5.conf** toolet archivo KDC confiar en que hace referencia toohello después de la plantilla de configuración de dominio de Windows.</span><span class="sxs-lookup"><span data-stu-id="2aa28-285">Edit hello KDC configuration in **krb5.conf** file toolet KDC trust Windows Domain referring toohello following configuration template.</span></span> <span data-ttu-id="2aa28-286">De forma predeterminada, se encuentra en configuración de hello **/etc/krb5.conf**.</span><span class="sxs-lookup"><span data-stu-id="2aa28-286">By default, hello configuration is located at **/etc/krb5.conf**.</span></span>

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  <span data-ttu-id="2aa28-287">**Reinicie** Hola servicio KDC después de la configuración.</span><span class="sxs-lookup"><span data-stu-id="2aa28-287">**Restart** hello KDC service after configuration.</span></span>

2.  <span data-ttu-id="2aa28-288">Preparar una entidad de seguridad denominado  **krbtgt/REALM.COM@AD.COM**  en el servidor KDC con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2aa28-288">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with hello following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="2aa28-289">En el archivo de configuración de servicio de HDFS **hadoop.security.auth_to_local**, agregue `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span><span class="sxs-lookup"><span data-stu-id="2aa28-289">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="2aa28-290">**En el controlador de dominio:**</span><span class="sxs-lookup"><span data-stu-id="2aa28-290">**On domain controller:**</span></span>

1.  <span data-ttu-id="2aa28-291">Ejecute hello siguiente **Ksetup** comandos tooadd una entrada de dominio:</span><span class="sxs-lookup"><span data-stu-id="2aa28-291">Run hello following **Ksetup** commands tooadd a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="2aa28-292">Establecer la confianza de dominio Kerberos del dominio de Windows tooKerberos.</span><span class="sxs-lookup"><span data-stu-id="2aa28-292">Establish trust from Windows Domain tooKerberos Realm.</span></span> <span data-ttu-id="2aa28-293">[contraseña] es la contraseña de Hola de entidad de seguridad de hello  **krbtgt/REALM.COM@AD.COM** .</span><span class="sxs-lookup"><span data-stu-id="2aa28-293">[password] is hello password for hello principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="2aa28-294">Seleccione el algoritmo de cifrado usado en Kerberos.</span><span class="sxs-lookup"><span data-stu-id="2aa28-294">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="2aa28-295">Vaya tooServer Manager > Administración de directivas de grupo > dominio > objetos de directiva de grupo > predeterminado o la directiva de dominio de Active y la edición.</span><span class="sxs-lookup"><span data-stu-id="2aa28-295">Go tooServer Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="2aa28-296">Hola **Editor de administración de directivas de grupo** ventana emergente, vaya tooComputer configuración > directivas > configuración de Windows > configuración de seguridad > directivas locales > Opciones de seguridad y configurar **red seguridad: configurar los tipos de cifrado permitidos para que Kerberos**.</span><span class="sxs-lookup"><span data-stu-id="2aa28-296">In hello **Group Policy Management Editor** popup window, go tooComputer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="2aa28-297">Algoritmo de cifrado de hello seleccione desea toouse cuando conecta tooKDC.</span><span class="sxs-lookup"><span data-stu-id="2aa28-297">Select hello encryption algorithm you want toouse when connect tooKDC.</span></span> <span data-ttu-id="2aa28-298">Normalmente, puede seleccionar simplemente todas las opciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-298">Commonly, you can simply select all hello options.</span></span>

        ![Configuración de tipos de cifrado para Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="2aa28-300">Use **Ksetup** toobe comando toospecify Hola cifrado algoritmo usado en hello territorio específico.</span><span class="sxs-lookup"><span data-stu-id="2aa28-300">Use **Ksetup** command toospecify hello encryption algorithm toobe used on hello specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="2aa28-301">Crear asignación de hello entre Hola cuenta y de dominio Kerberos principal, en orden toouse principal de Kerberos en el dominio de Windows.</span><span class="sxs-lookup"><span data-stu-id="2aa28-301">Create hello mapping between hello domain account and Kerberos principal, in order toouse Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="2aa28-302">Iniciar herramientas administrativas de hello > **equipos y usuarios de Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2aa28-302">Start hello Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="2aa28-303">Configure características avanzadas; para ello, haga clic en **Ver** > **Características avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="2aa28-303">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="2aa28-304">Busque Hola cuenta toowhich desee toocreate asignaciones y haga clic en tooview **las asignaciones de nombres** > haga clic en **nombres Kerberos** ficha.</span><span class="sxs-lookup"><span data-stu-id="2aa28-304">Locate hello account toowhich you want toocreate mappings, and right-click tooview **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="2aa28-305">Agregar una entidad de seguridad de dominio Kerberos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2aa28-305">Add a principal from hello realm.</span></span>

        ![Asignación de la identidad de seguridad](media/data-factory-hdfs-connector/map-security-identity.png)

<span data-ttu-id="2aa28-307">**En la máquina de puerta de enlace:**</span><span class="sxs-lookup"><span data-stu-id="2aa28-307">**On gateway machine:**</span></span>

* <span data-ttu-id="2aa28-308">Ejecute hello siguiente **Ksetup** comandos tooadd una entrada de dominio Kerberos.</span><span class="sxs-lookup"><span data-stu-id="2aa28-308">Run hello following **Ksetup** commands tooadd a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="2aa28-309">**En Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="2aa28-309">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="2aa28-310">Configure el conector HDFS de hello mediante **autenticación de Windows** junto con su cuenta de dominio o el origen de datos de entidad de seguridad de Kerberos tooconnect toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="2aa28-310">Configure hello HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="2aa28-311">Compruebe la sección [HDFS Linked Service properties](#linked-service-properties) (Propiedades de servicio vinculado de HDFS) en los detalles de configuración.</span><span class="sxs-lookup"><span data-stu-id="2aa28-311">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

> [!NOTE]
> <span data-ttu-id="2aa28-312">columnas de toomap de toocolumns de conjunto de datos de origen del conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2aa28-312">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="performance-and-tuning"></a><span data-ttu-id="2aa28-313">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="2aa28-313">Performance and Tuning</span></span>
<span data-ttu-id="2aa28-314">Vea [guía para la optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos de Azure y toooptimize de diversas maneras.</span><span class="sxs-lookup"><span data-stu-id="2aa28-314">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
