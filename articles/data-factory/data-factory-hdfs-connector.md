---
title: Traslado de los datos de HDFS local | Microsoft Docs
description: "Obtenga información acerca de cómo mover datos desde HDFS local mediante Factoría de datos de Azure"
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
ms.openlocfilehash: 9a8f3156a62a1a7aa49377349e8a85454efeda50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a><span data-ttu-id="0cff5-103">Movimiento de datos desde HDFS local mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0cff5-103">Move data from on-premises HDFS using Azure Data Factory</span></span>
<span data-ttu-id="0cff5-104">En este artículo se explica el uso de la actividad de copia en Azure Data Factory para mover datos de HDFS local.</span><span class="sxs-lookup"><span data-stu-id="0cff5-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises HDFS.</span></span> <span data-ttu-id="0cff5-105">Se basa en la información general que ofrece el artículo [Movimiento de datos con la actividad de copia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="0cff5-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="0cff5-106">Puede copiar datos de HDFS en cualquier almacén de datos de receptor admitido.</span><span class="sxs-lookup"><span data-stu-id="0cff5-106">You can copy data from HDFS to any supported sink data store.</span></span> <span data-ttu-id="0cff5-107">Para ver una lista de almacenes de datos admitidos como receptores por la actividad de copia, consulte la tabla de [almacenes de datos compatibles](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="0cff5-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="0cff5-108">En la actualidad, Factoría de datos solo admite el movimiento de datos desde HDFS local a otros almacenes de datos, pero no el movimiento inverso.</span><span class="sxs-lookup"><span data-stu-id="0cff5-108">Data factory currently supports only moving data from an on-premises HDFS to other data stores, but not for moving data from other data stores to an on-premises HDFS.</span></span>

> [!NOTE]
> <span data-ttu-id="0cff5-109">La actividad de copia no elimina el archivo de origen una vez copiado correctamente en el destino.</span><span class="sxs-lookup"><span data-stu-id="0cff5-109">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="0cff5-110">Si necesita eliminar el archivo de origen tras una copia correcta, cree una actividad personalizada para tal fin y úsela en la canalización.</span><span class="sxs-lookup"><span data-stu-id="0cff5-110">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="0cff5-111">Habilitación de la conectividad</span><span class="sxs-lookup"><span data-stu-id="0cff5-111">Enabling connectivity</span></span>
<span data-ttu-id="0cff5-112">El servicio Factoría de datos admite la conexión a HDFS local mediante Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="0cff5-112">Data Factory service supports connecting to on-premises HDFS using the Data Management Gateway.</span></span> <span data-ttu-id="0cff5-113">Consulte el artículo sobre cómo [mover datos entre ubicaciones locales y la nube](data-factory-move-data-between-onprem-and-cloud.md) para obtener información acerca de Data Management Gateway, así como instrucciones paso a paso sobre cómo configurar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="0cff5-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="0cff5-114">Use la puerta de enlace para conectar con HDFS, aunque esté hospedado en una máquina virtual de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="0cff5-114">Use the gateway to connect to HDFS even if it is hosted in an Azure IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="0cff5-115">Asegúrese de que Data Management Gateway puede obtener acceso a **TODOS** los [servidor de nodo de nombres]:[puerto de nodo de nombres] y [servidores de nodos de datos]:[puerto de nodo de datos] del clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0cff5-115">Make sure the Data Management Gateway can access to **ALL** the [name node server]:[name node port] and [data node servers]:[data node port] of the Hadoop cluster.</span></span> <span data-ttu-id="0cff5-116">El [puerto de nodo de nombres] predeterminado es 50070 y el [puerto de nodo de datos] es 50075.</span><span class="sxs-lookup"><span data-stu-id="0cff5-116">Default [name node port] is 50070, and default [data node port] is 50075.</span></span>

<span data-ttu-id="0cff5-117">Aunque puede instalar la puerta de enlace en el mismo equipo local o en la máquina virtual de Azure como HDFS, se recomienda que instale la puerta de enlace en un equipo independiente o una máquina virtual de IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="0cff5-117">While you can install gateway on the same on-premises machine or the Azure VM as the HDFS, we recommend that you install the gateway on a separate machine/Azure IaaS VM.</span></span> <span data-ttu-id="0cff5-118">Al tener la puerta de enlace en un equipo independiente, se reduce la contención de recursos y se mejora el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="0cff5-118">Having gateway on a separate machine reduces resource contention and improves performance.</span></span> <span data-ttu-id="0cff5-119">Al instalar la puerta de enlace en una máquina independiente, la máquina debería poder acceder a la máquina con HDFS.</span><span class="sxs-lookup"><span data-stu-id="0cff5-119">When you install the gateway on a separate machine, the machine should be able to access the machine with the HDFS.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0cff5-120">Introducción</span><span class="sxs-lookup"><span data-stu-id="0cff5-120">Getting started</span></span>
<span data-ttu-id="0cff5-121">Puede crear una canalización con actividad de copia que mueva los datos desde un origen de HDFS mediante el uso de diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="0cff5-121">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span></span>

<span data-ttu-id="0cff5-122">La manera más fácil de crear una canalización es usar el **Asistente para copia**.</span><span class="sxs-lookup"><span data-stu-id="0cff5-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="0cff5-123">Consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md) para ver un tutorial rápido sobre la creación de una canalización mediante el Asistente para copiar datos.</span><span class="sxs-lookup"><span data-stu-id="0cff5-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="0cff5-124">También puede usar las herramientas siguientes para crear una canalización: **Azure Portal**, **Visual Studio**, **Azure PowerShell**, **plantilla de Azure Resource Manager**, **API de .NET** y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="0cff5-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="0cff5-125">Consulte el [tutorial de actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obtener instrucciones paso a paso sobre cómo crear una canalización con una actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="0cff5-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="0cff5-126">Tanto si usa las herramientas como las API, realice los pasos siguientes para crear una canalización que mueva datos de un almacén de datos de origen a un almacén de datos receptor:</span><span class="sxs-lookup"><span data-stu-id="0cff5-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="0cff5-127">Cree **servicios vinculados** para vincular almacenes de datos de entrada y salida a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="0cff5-127">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="0cff5-128">Cree **conjuntos de datos** con el fin de representar los datos de entrada y salida para la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="0cff5-128">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="0cff5-129">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="0cff5-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="0cff5-130">Cuando se usa el Asistente, se crean automáticamente definiciones de JSON para estas entidades de Data Factory (servicios vinculados, conjuntos de datos y la canalización).</span><span class="sxs-lookup"><span data-stu-id="0cff5-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="0cff5-131">Al usar herramientas o API (excepto la API de .NET), se definen estas entidades de Data Factory con el formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0cff5-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="0cff5-132">Para obtener un ejemplo con definiciones de JSON para entidades de Data Factory que se utilizan para copiar los datos de un almacén de datos de HDFS, consulte la sección [Ejemplo de JSON: Copiar datos de HDFS local a un blob de Azure](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="0cff5-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS to Azure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span></span>

<span data-ttu-id="0cff5-133">En las secciones siguientes se proporcionan detalles sobre las propiedades JSON que se usan para definir entidades de Data Factory específicas de HDFS:</span><span class="sxs-lookup"><span data-stu-id="0cff5-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to HDFS:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="0cff5-134">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="0cff5-134">Linked service properties</span></span>
<span data-ttu-id="0cff5-135">Un servicio vinculado vincula un almacén de datos a una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="0cff5-135">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="0cff5-136">Se crea un servicio vinculado de tipo **Hdfs** para vincular HDFS local a la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="0cff5-136">You create a linked service of type **Hdfs** to link an on-premises HDFS to your data factory.</span></span> <span data-ttu-id="0cff5-137">En la tabla siguiente se proporciona la descripción de los elementos JSON específicos del servicio vinculado de HDFS.</span><span class="sxs-lookup"><span data-stu-id="0cff5-137">The following table provides description for JSON elements specific to HDFS linked service.</span></span>

| <span data-ttu-id="0cff5-138">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0cff5-138">Property</span></span> | <span data-ttu-id="0cff5-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="0cff5-139">Description</span></span> | <span data-ttu-id="0cff5-140">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0cff5-140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0cff5-141">type</span><span class="sxs-lookup"><span data-stu-id="0cff5-141">type</span></span> |<span data-ttu-id="0cff5-142">La propiedad type debe establecerse en: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="0cff5-142">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="0cff5-143">Sí</span><span class="sxs-lookup"><span data-stu-id="0cff5-143">Yes</span></span> |
| <span data-ttu-id="0cff5-144">URL</span><span class="sxs-lookup"><span data-stu-id="0cff5-144">Url</span></span> |<span data-ttu-id="0cff5-145">Dirección URL a HDFS</span><span class="sxs-lookup"><span data-stu-id="0cff5-145">URL to the HDFS</span></span> |<span data-ttu-id="0cff5-146">Sí</span><span class="sxs-lookup"><span data-stu-id="0cff5-146">Yes</span></span> |
| <span data-ttu-id="0cff5-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0cff5-147">authenticationType</span></span> |<span data-ttu-id="0cff5-148">Anónima o Windows.</span><span class="sxs-lookup"><span data-stu-id="0cff5-148">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="0cff5-149">Para usar la **autenticación Kerberos** para el conector HDFS, consulte [esta sección](#use-kerberos-authentication-for-hdfs-connector) a fin de configurar el entorno local en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="0cff5-149">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="0cff5-150">Sí</span><span class="sxs-lookup"><span data-stu-id="0cff5-150">Yes</span></span> |
| <span data-ttu-id="0cff5-151">userName</span><span class="sxs-lookup"><span data-stu-id="0cff5-151">userName</span></span> |<span data-ttu-id="0cff5-152">Nombre de usuario para la autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="0cff5-152">Username for Windows authentication.</span></span> |<span data-ttu-id="0cff5-153">Sí (para la autenticación de Windows)</span><span class="sxs-lookup"><span data-stu-id="0cff5-153">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="0cff5-154">contraseña</span><span class="sxs-lookup"><span data-stu-id="0cff5-154">password</span></span> |<span data-ttu-id="0cff5-155">Contraseña para la autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="0cff5-155">Password for Windows authentication.</span></span> |<span data-ttu-id="0cff5-156">Sí (para la autenticación de Windows)</span><span class="sxs-lookup"><span data-stu-id="0cff5-156">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="0cff5-157">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0cff5-157">gatewayName</span></span> |<span data-ttu-id="0cff5-158">Nombre de la puerta de enlace que el servicio Factoría de datos debe usar para conectarse a HDFS.</span><span class="sxs-lookup"><span data-stu-id="0cff5-158">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="0cff5-159">Sí</span><span class="sxs-lookup"><span data-stu-id="0cff5-159">Yes</span></span> |
| <span data-ttu-id="0cff5-160">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="0cff5-160">encryptedCredential</span></span> |<span data-ttu-id="0cff5-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) de la credencial de acceso.</span><span class="sxs-lookup"><span data-stu-id="0cff5-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of the access credential.</span></span> |<span data-ttu-id="0cff5-162">No</span><span class="sxs-lookup"><span data-stu-id="0cff5-162">No</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="0cff5-163">Uso de autenticación anónima</span><span class="sxs-lookup"><span data-stu-id="0cff5-163">Using Anonymous authentication</span></span>

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

### <a name="using-windows-authentication"></a><span data-ttu-id="0cff5-164">Uso de autenticación de Windows</span><span class="sxs-lookup"><span data-stu-id="0cff5-164">Using Windows authentication</span></span>

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
## <a name="dataset-properties"></a><span data-ttu-id="0cff5-165">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="0cff5-165">Dataset properties</span></span>
<span data-ttu-id="0cff5-166">Para una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, vea el artículo [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="0cff5-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="0cff5-167">Las secciones como structure, availability y policy del código JSON del conjunto de datos son similares para todos los tipos de conjunto de datos (SQL Azure, blob de Azure, tabla de Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="0cff5-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="0cff5-168">La sección **typeProperties** es diferente en cada tipo de conjunto de datos y proporciona información acerca de la ubicación de los datos en el almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="0cff5-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="0cff5-169">La sección typeProperties del conjunto de datos del tipo **FileShare** (que incluye el conjunto de datos de HDFS) tiene las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="0cff5-169">The typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has the following properties</span></span>

| <span data-ttu-id="0cff5-170">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0cff5-170">Property</span></span> | <span data-ttu-id="0cff5-171">Descripción</span><span class="sxs-lookup"><span data-stu-id="0cff5-171">Description</span></span> | <span data-ttu-id="0cff5-172">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0cff5-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0cff5-173">folderPath</span><span class="sxs-lookup"><span data-stu-id="0cff5-173">folderPath</span></span> |<span data-ttu-id="0cff5-174">Ruta de acceso a la carpeta.</span><span class="sxs-lookup"><span data-stu-id="0cff5-174">Path to the folder.</span></span> <span data-ttu-id="0cff5-175">Ejemplo: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="0cff5-175">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="0cff5-176">Use el carácter de escape "\" para los caracteres especiales de la cadena.</span><span class="sxs-lookup"><span data-stu-id="0cff5-176">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="0cff5-177">Por ejemplo: para folder\subfolder, especifique la carpeta\\\\subcarpeta y para d:\samplefolder, especifique d:\\\\samplefolder.</span><span class="sxs-lookup"><span data-stu-id="0cff5-177">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="0cff5-178">Puede combinar esta propiedad con **partitionBy** para que las rutas de acceso de carpeta se basen en las fechas y horas de inicio y finalización del segmento.</span><span class="sxs-lookup"><span data-stu-id="0cff5-178">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="0cff5-179">Sí</span><span class="sxs-lookup"><span data-stu-id="0cff5-179">Yes</span></span> |
| <span data-ttu-id="0cff5-180">fileName</span><span class="sxs-lookup"><span data-stu-id="0cff5-180">fileName</span></span> |<span data-ttu-id="0cff5-181">Especifique el nombre del archivo en **folderPath** si quiere que la tabla haga referencia a un archivo específico de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="0cff5-181">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="0cff5-182">Si no especifica ningún valor para esta propiedad, la tabla apunta a todos los archivos de la carpeta.</span><span class="sxs-lookup"><span data-stu-id="0cff5-182">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="0cff5-183">Si no se especifica fileName para un conjunto de datos de salida, el nombre del archivo generado estaría en el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="0cff5-183">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="0cff5-184">Data<Guid>.txt (por ejemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="0cff5-184">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="0cff5-185">No</span><span class="sxs-lookup"><span data-stu-id="0cff5-185">No</span></span> |
| <span data-ttu-id="0cff5-186">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="0cff5-186">partitionedBy</span></span> |<span data-ttu-id="0cff5-187">partitionedBy se puede usar para especificar un valor de folderPath dinámico, un nombre de archivo para datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="0cff5-187">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="0cff5-188">Por ejemplo, folderPath se parametriza para cada hora de datos.</span><span class="sxs-lookup"><span data-stu-id="0cff5-188">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="0cff5-189">No</span><span class="sxs-lookup"><span data-stu-id="0cff5-189">No</span></span> |
| <span data-ttu-id="0cff5-190">formato</span><span class="sxs-lookup"><span data-stu-id="0cff5-190">format</span></span> | <span data-ttu-id="0cff5-191">Se admiten los siguientes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** y **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="0cff5-191">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="0cff5-192">Establezca la propiedad **type** de formato en uno de los siguientes valores.</span><span class="sxs-lookup"><span data-stu-id="0cff5-192">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="0cff5-193">Para más información, consulte las secciones [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) y [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="0cff5-193">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="0cff5-194">Si desea **copiar los archivos tal cual** entre los almacenes basados en archivos (copia binaria), omita la sección de formato en las definiciones de los conjuntos de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="0cff5-194">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="0cff5-195">No</span><span class="sxs-lookup"><span data-stu-id="0cff5-195">No</span></span> |
| <span data-ttu-id="0cff5-196">compresión</span><span class="sxs-lookup"><span data-stu-id="0cff5-196">compression</span></span> | <span data-ttu-id="0cff5-197">Especifique el tipo y el nivel de compresión de los datos.</span><span class="sxs-lookup"><span data-stu-id="0cff5-197">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="0cff5-198">Los tipos admitidos son **GZip**, **Deflate**, **BZip2** y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="0cff5-198">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="0cff5-199">Los niveles admitidos son **Optimal** y **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="0cff5-199">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="0cff5-200">Para más información, consulte el artículo sobre [formatos de compresión de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="0cff5-200">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="0cff5-201">No</span><span class="sxs-lookup"><span data-stu-id="0cff5-201">No</span></span> |

> [!NOTE]
> <span data-ttu-id="0cff5-202">filename y fileFilter no pueden usarse simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="0cff5-202">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="0cff5-203">Uso de la propiedad partitionedBy</span><span class="sxs-lookup"><span data-stu-id="0cff5-203">Using partionedBy property</span></span>
<span data-ttu-id="0cff5-204">Como ya se ha indicado en la sección anterior, se puede especificar un valor dinámico de folderPath y filename para datos de series temporales con la propiedad **partitionedBy**, [funciones de Data Factory y las variables del sistema](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="0cff5-204">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="0cff5-205">Para aprender más sobre los conjuntos de datos de series temporales [Creación de conjuntos de datos](data-factory-create-datasets.md), [Programación y ejecución](data-factory-scheduling-and-execution.md) y [Creación de canalizaciones](data-factory-create-pipelines.md) para conocer más detalles sobre los conjuntos de datos de series temporales, la programación y los segmentos.</span><span class="sxs-lookup"><span data-stu-id="0cff5-205">To learn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="0cff5-206">Muestra 1:</span><span class="sxs-lookup"><span data-stu-id="0cff5-206">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="0cff5-207">En este ejemplo, {Slice} se reemplaza por el valor de la variable del sistema SliceStart de Data Factory en el formato (YYYYMMDDHH) especificado.</span><span class="sxs-lookup"><span data-stu-id="0cff5-207">In this example {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="0cff5-208">SliceStart hace referencia a la hora de inicio del segmento.</span><span class="sxs-lookup"><span data-stu-id="0cff5-208">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="0cff5-209">folderPath es diferente para cada segmento.</span><span class="sxs-lookup"><span data-stu-id="0cff5-209">The folderPath is different for each slice.</span></span> <span data-ttu-id="0cff5-210">Por ejemplo: wikidatagateway/wikisampledataout/2014100103 o wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="0cff5-210">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="0cff5-211">Ejemplo 2:</span><span class="sxs-lookup"><span data-stu-id="0cff5-211">Sample 2:</span></span>

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
<span data-ttu-id="0cff5-212">En este ejemplo, year, month, day y time de SliceStart se extraen en variables independientes que se usan en las propiedades folderPath y fileName.</span><span class="sxs-lookup"><span data-stu-id="0cff5-212">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="0cff5-213">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="0cff5-213">Copy activity properties</span></span>
<span data-ttu-id="0cff5-214">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte el artículo [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="0cff5-214">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="0cff5-215">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="0cff5-215">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="0cff5-216">Por otra parte, las propiedades disponibles en la sección typeProperties de la actividad varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="0cff5-216">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="0cff5-217">Para la actividad de copia, varían en función de los tipos de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="0cff5-217">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="0cff5-218">En caso de actividad de copia, si el origen es del tipo **FileSystemSource** , estarán disponibles las propiedades siguientes en la sección typeProperties:</span><span class="sxs-lookup"><span data-stu-id="0cff5-218">For Copy Activity, when source is of type **FileSystemSource** the following properties are available in typeProperties section:</span></span>

<span data-ttu-id="0cff5-219">**FileSystemSource** admite las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="0cff5-219">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="0cff5-220">Propiedad</span><span class="sxs-lookup"><span data-stu-id="0cff5-220">Property</span></span> | <span data-ttu-id="0cff5-221">Descripción</span><span class="sxs-lookup"><span data-stu-id="0cff5-221">Description</span></span> | <span data-ttu-id="0cff5-222">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="0cff5-222">Allowed values</span></span> | <span data-ttu-id="0cff5-223">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0cff5-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0cff5-224">recursive</span><span class="sxs-lookup"><span data-stu-id="0cff5-224">recursive</span></span> |<span data-ttu-id="0cff5-225">Indica si los datos se leen de forma recursiva de las subcarpetas o solo de la carpeta especificada.</span><span class="sxs-lookup"><span data-stu-id="0cff5-225">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="0cff5-226">True, False (predeterminada)</span><span class="sxs-lookup"><span data-stu-id="0cff5-226">True, False (default)</span></span> |<span data-ttu-id="0cff5-227">No</span><span class="sxs-lookup"><span data-stu-id="0cff5-227">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="0cff5-228">Formatos de archivo y de compresión admitidos</span><span class="sxs-lookup"><span data-stu-id="0cff5-228">Supported file and compression formats</span></span>
<span data-ttu-id="0cff5-229">Consulte los detalles en [Formatos de compresión y de archivos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="0cff5-229">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-on-premises-hdfs-to-azure-blob"></a><span data-ttu-id="0cff5-230">Ejemplo de JSON: Copiar datos de HDFS local a un blob de Azure</span><span class="sxs-lookup"><span data-stu-id="0cff5-230">JSON example: Copy data from on-premises HDFS to Azure Blob</span></span>
<span data-ttu-id="0cff5-231">En este ejemplo, se muestra cómo copiar datos de un sistema HDFS local al Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="0cff5-231">This sample shows how to copy data from an on-premises HDFS to Azure Blob Storage.</span></span> <span data-ttu-id="0cff5-232">Sin embargo, se pueden copiar datos **directamente** a cualquiera de los receptores indicados [aquí](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante la actividad de copia en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="0cff5-232">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="0cff5-233">El ejemplo proporciona definiciones de JSON para las siguientes entidades de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0cff5-233">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="0cff5-234">Puede utilizar estas definiciones para crear una canalización para copiar datos desde HDFS a Azure Blob Storage mediante [Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0cff5-234">You can use these definitions to create a pipeline to copy data from HDFS to Azure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

1. <span data-ttu-id="0cff5-235">Un servicio vinculado del tipo [OnPremisesHdfs](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0cff5-235">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span></span>
2. <span data-ttu-id="0cff5-236">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="0cff5-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="0cff5-237">Un [conjunto de datos](data-factory-create-datasets.md) de entrada de tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0cff5-237">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
4. <span data-ttu-id="0cff5-238">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0cff5-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="0cff5-239">Una [canalización](data-factory-create-pipelines.md) con la actividad de copia que usa [FileSystemSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0cff5-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="0cff5-240">El ejemplo copia los datos de un HDFS local a un blob de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="0cff5-240">The sample copies data from an on-premises HDFS to an Azure blob every hour.</span></span> <span data-ttu-id="0cff5-241">Las propiedades JSON usadas en estos ejemplos se describen en las secciones que aparecen después de los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="0cff5-241">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="0cff5-242">En primer lugar, configure la puerta de enlace de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="0cff5-242">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="0cff5-243">Las instrucciones se encuentran en el artículo sobre cómo [mover datos entre ubicaciones locales y en la nube](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="0cff5-243">The instructions in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="0cff5-244">**Servicio vinculado de HDFS:** En este ejemplo se usa la autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="0cff5-244">**HDFS linked service:** This example uses the Windows authentication.</span></span> <span data-ttu-id="0cff5-245">Consulte la sección [Propiedades del servicio vinculado de HDFS](#linked-service-properties) para conocer los diferentes tipos de autenticación que se pueden usar.</span><span class="sxs-lookup"><span data-stu-id="0cff5-245">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="0cff5-246">**Servicio vinculado de Almacenamiento de Azure:**</span><span class="sxs-lookup"><span data-stu-id="0cff5-246">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="0cff5-247">**Conjunto de datos de entrada de HDFS:** Este conjunto de datos hace referencia a la carpeta DataTransfer/UnitTest/ de HDFS.</span><span class="sxs-lookup"><span data-stu-id="0cff5-247">**HDFS input dataset:** This dataset refers to the HDFS folder DataTransfer/UnitTest/.</span></span> <span data-ttu-id="0cff5-248">La canalización copia todos los archivos de su carpeta en el destino.</span><span class="sxs-lookup"><span data-stu-id="0cff5-248">The pipeline copies all the files in this folder to the destination.</span></span>

<span data-ttu-id="0cff5-249">Si se establece "external": "true", se informa al servicio Data Factory que el conjunto de datos es externo a Data Factory y que no lo genera ninguna actividad de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="0cff5-249">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="0cff5-250">**Conjunto de datos de salida de blob de Azure:**</span><span class="sxs-lookup"><span data-stu-id="0cff5-250">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="0cff5-251">Los datos se escriben en un nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="0cff5-251">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="0cff5-252">La ruta de acceso de la carpeta para el blob se evalúa dinámicamente según la hora de inicio del segmento que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="0cff5-252">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="0cff5-253">La ruta de acceso de la carpeta usa las partes year, month, day y hours de la hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="0cff5-253">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="0cff5-254">**Actividad de copia en una canalización con el origen del sistema de archivos y el receptor de blob:**</span><span class="sxs-lookup"><span data-stu-id="0cff5-254">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="0cff5-255">La canalización contiene una actividad de copia que está configurada para usar estos conjuntos de datos de entrada y de salida y está programada para ejecutarse cada hora.</span><span class="sxs-lookup"><span data-stu-id="0cff5-255">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="0cff5-256">En la definición de JSON de canalización, el tipo **source** se establece en **FileSystemSource** y el tipo **sink** se establece en **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="0cff5-256">In the pipeline JSON definition, the **source** type is set to **FileSystemSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="0cff5-257">La consulta SQL especificada para la propiedad **query** selecciona los datos de la última hora que se van a copiar.</span><span class="sxs-lookup"><span data-stu-id="0cff5-257">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="0cff5-258">Uso de autenticación Kerberos para el conector HDFS</span><span class="sxs-lookup"><span data-stu-id="0cff5-258">Use Kerberos authentication for HDFS connector</span></span>
<span data-ttu-id="0cff5-259">Existen dos opciones para configurar el entorno local para usar la autenticación Kerberos en el conector HDFS.</span><span class="sxs-lookup"><span data-stu-id="0cff5-259">There are two options to set up the on-premises environment so as to use Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="0cff5-260">Puede elegir la que mejor se adapte en su caso.</span><span class="sxs-lookup"><span data-stu-id="0cff5-260">You can choose the one better fits your case.</span></span>
* <span data-ttu-id="0cff5-261">Opción 1: [Unirse a la máquina de puerta de enlace en el dominio Kerberos](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="0cff5-261">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="0cff5-262">Opción 2: [Habilitar la confianza mutua entre el dominio de Windows y el dominio Kerberos](#kerberos-mutual-trust)</span><span class="sxs-lookup"><span data-stu-id="0cff5-262">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <span data-ttu-id="0cff5-263"><a name="kerberos-join-realm"></a>Opción 1: Unirse a la máquina de puerta de enlace en el dominio Kerberos</span><span class="sxs-lookup"><span data-stu-id="0cff5-263"><a name="kerberos-join-realm"></a>Option 1: Join gateway machine in Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="0cff5-264">Requisito:</span><span class="sxs-lookup"><span data-stu-id="0cff5-264">Requirement:</span></span>

* <span data-ttu-id="0cff5-265">La máquina de puerta de enlace debe unirse al dominio Kerberos y no puede unirse a ningún dominio de Windows.</span><span class="sxs-lookup"><span data-stu-id="0cff5-265">The gateway machine needs to join the Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-to-configure"></a><span data-ttu-id="0cff5-266">Configuración:</span><span class="sxs-lookup"><span data-stu-id="0cff5-266">How to configure:</span></span>

<span data-ttu-id="0cff5-267">**En la máquina de puerta de enlace:**</span><span class="sxs-lookup"><span data-stu-id="0cff5-267">**On gateway machine:**</span></span>

1.  <span data-ttu-id="0cff5-268">Ejecute la utilidad **Ksetup** para configurar el dominio y el servidor KDC de Kerberos.</span><span class="sxs-lookup"><span data-stu-id="0cff5-268">Run the **Ksetup** utility to configure the Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="0cff5-269">La máquina debe configurarse como miembro de un grupo de trabajo dado que un dominio Kerberos es diferente de un dominio de Windows.</span><span class="sxs-lookup"><span data-stu-id="0cff5-269">The machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="0cff5-270">Para ello, establezca el dominio Kerberos y agregue un servidor KDC de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="0cff5-270">This can be achieved by setting the Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="0cff5-271">Sustituya *REALM.COM* por su dominio respectivo, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0cff5-271">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="0cff5-272">**Reinicie** la máquina después de ejecutar estos 2 comandos.</span><span class="sxs-lookup"><span data-stu-id="0cff5-272">**Restart** the machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="0cff5-273">Compruebe la configuración con el comando **Ksetup**.</span><span class="sxs-lookup"><span data-stu-id="0cff5-273">Verify the configuration with **Ksetup** command.</span></span> <span data-ttu-id="0cff5-274">La salida debe ser como la siguiente:</span><span class="sxs-lookup"><span data-stu-id="0cff5-274">The output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="0cff5-275">**En Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="0cff5-275">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="0cff5-276">Configure el conector HDFS mediante la **autenticación de Windows** junto con el nombre y la contraseña de la entidad de seguridad de Kerberos para conectarse al origen de datos de HDFS.</span><span class="sxs-lookup"><span data-stu-id="0cff5-276">Configure the HDFS connector using **Windows authentication** together with your Kerberos principal name and password to connect to the HDFS data source.</span></span> <span data-ttu-id="0cff5-277">Compruebe la sección [HDFS Linked Service properties](#linked-service-properties) (Propiedades de servicio vinculado de HDFS) en los detalles de configuración.</span><span class="sxs-lookup"><span data-stu-id="0cff5-277">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <span data-ttu-id="0cff5-278"><a name="kerberos-mutual-trust"></a>Opción 2: Habilitar la confianza mutua entre el dominio de Windows y el dominio Kerberos</span><span class="sxs-lookup"><span data-stu-id="0cff5-278"><a name="kerberos-mutual-trust"></a>Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="0cff5-279">Requisito:</span><span class="sxs-lookup"><span data-stu-id="0cff5-279">Requirement:</span></span>
*   <span data-ttu-id="0cff5-280">La máquina de puerta de enlace debe unirse a un dominio de Windows.</span><span class="sxs-lookup"><span data-stu-id="0cff5-280">The gateway machine must join a Windows domain.</span></span>
*   <span data-ttu-id="0cff5-281">Necesita permiso para actualizar la configuración del controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="0cff5-281">You need permission to update the domain controller's settings.</span></span>

#### <a name="how-to-configure"></a><span data-ttu-id="0cff5-282">Configuración:</span><span class="sxs-lookup"><span data-stu-id="0cff5-282">How to configure:</span></span>

> [!NOTE]
> <span data-ttu-id="0cff5-283">Sustituya REALM.COM y AD.COM en el siguiente tutorial por su propio dominio y controlador de dominio, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0cff5-283">Replace REALM.COM and AD.COM in the following tutorial with your own respective realm and domain controller as needed.</span></span>

<span data-ttu-id="0cff5-284">**En el servidor KDC:**</span><span class="sxs-lookup"><span data-stu-id="0cff5-284">**On KDC server:**</span></span>

1.  <span data-ttu-id="0cff5-285">Edite la configuración de KDC en el archivo **krb5.conf** para permitir que KDC confíe en el dominio de Windows que hace referencia a la siguiente plantilla de configuración.</span><span class="sxs-lookup"><span data-stu-id="0cff5-285">Edit the KDC configuration in **krb5.conf** file to let KDC trust Windows Domain referring to the following configuration template.</span></span> <span data-ttu-id="0cff5-286">De forma predeterminada, la configuración está ubicada en **/etc/krb5.conf**.</span><span class="sxs-lookup"><span data-stu-id="0cff5-286">By default, the configuration is located at **/etc/krb5.conf**.</span></span>

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

  <span data-ttu-id="0cff5-287">**Reinicie** el servicio KDC después de la configuración.</span><span class="sxs-lookup"><span data-stu-id="0cff5-287">**Restart** the KDC service after configuration.</span></span>

2.  <span data-ttu-id="0cff5-288">Prepare una entidad de seguridad llamada **krbtgt/REALM.COM@AD.COM** en el servidor KDC con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0cff5-288">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with the following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="0cff5-289">En el archivo de configuración de servicio de HDFS **hadoop.security.auth_to_local**, agregue `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span><span class="sxs-lookup"><span data-stu-id="0cff5-289">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="0cff5-290">**En el controlador de dominio:**</span><span class="sxs-lookup"><span data-stu-id="0cff5-290">**On domain controller:**</span></span>

1.  <span data-ttu-id="0cff5-291">Ejecute los siguientes comandos **Ksetup** para agregar una entrada de dominio:</span><span class="sxs-lookup"><span data-stu-id="0cff5-291">Run the following **Ksetup** commands to add a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="0cff5-292">Establezca la confianza entre el dominio de Windows y el dominio Kerberos.</span><span class="sxs-lookup"><span data-stu-id="0cff5-292">Establish trust from Windows Domain to Kerberos Realm.</span></span> <span data-ttu-id="0cff5-293">[contraseña] es la contraseña de la entidad de seguridad  **krbtgt/REALM.COM@AD.COM**.</span><span class="sxs-lookup"><span data-stu-id="0cff5-293">[password] is the password for the principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="0cff5-294">Seleccione el algoritmo de cifrado usado en Kerberos.</span><span class="sxs-lookup"><span data-stu-id="0cff5-294">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="0cff5-295">Vaya a Administrador de servidores > Administración de directivas de grupo > Dominio > Objetos de directiva de grupo > Default or Active Domain Policy (Directiva de dominio predeterminada o activa) y haga clic en Editar.</span><span class="sxs-lookup"><span data-stu-id="0cff5-295">Go to Server Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="0cff5-296">En la ventana emergente **Editor de administración de directivas de grupo**, vaya a Configuración de equipo > Directivas > Configuración de Windows > Configuración de seguridad > Directivas locales > Opciones de seguridad, y configure **Seguridad de red: configurar tipos de cifrado permitidos para Kerberos**.</span><span class="sxs-lookup"><span data-stu-id="0cff5-296">In the **Group Policy Management Editor** popup window, go to Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="0cff5-297">Seleccione el algoritmo de cifrado que quiere usar al conectarse a KDC.</span><span class="sxs-lookup"><span data-stu-id="0cff5-297">Select the encryption algorithm you want to use when connect to KDC.</span></span> <span data-ttu-id="0cff5-298">Normalmente, puede seleccionar todas las opciones.</span><span class="sxs-lookup"><span data-stu-id="0cff5-298">Commonly, you can simply select all the options.</span></span>

        ![Configuración de tipos de cifrado para Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="0cff5-300">Use el comando **Ksetup** para especificar el algoritmo de cifrado que se usará en el dominio específico.</span><span class="sxs-lookup"><span data-stu-id="0cff5-300">Use **Ksetup** command to specify the encryption algorithm to be used on the specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="0cff5-301">Cree la asignación entre la cuenta de dominio y la entidad de seguridad de Kerberos, a fin de usar la entidad de seguridad de Kerberos en el dominio de Windows.</span><span class="sxs-lookup"><span data-stu-id="0cff5-301">Create the mapping between the domain account and Kerberos principal, in order to use Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="0cff5-302">Inicie las herramientas administrativas > **Usuarios y equipos de Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0cff5-302">Start the Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="0cff5-303">Configure características avanzadas; para ello, haga clic en **Ver** > **Características avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="0cff5-303">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="0cff5-304">Busque la cuenta a la que quiere crear asignaciones y haga clic con el botón derecho para ver **Asignaciones de nombres** > haga clic en la pestaña **Nombres de Kerberos**.</span><span class="sxs-lookup"><span data-stu-id="0cff5-304">Locate the account to which you want to create mappings, and right-click to view **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="0cff5-305">Agregue una entidad de seguridad desde el dominio.</span><span class="sxs-lookup"><span data-stu-id="0cff5-305">Add a principal from the realm.</span></span>

        ![Asignación de la identidad de seguridad](media/data-factory-hdfs-connector/map-security-identity.png)

<span data-ttu-id="0cff5-307">**En la máquina de puerta de enlace:**</span><span class="sxs-lookup"><span data-stu-id="0cff5-307">**On gateway machine:**</span></span>

* <span data-ttu-id="0cff5-308">Ejecute los siguientes comandos **Ksetup** para agregar una entrada de dominio.</span><span class="sxs-lookup"><span data-stu-id="0cff5-308">Run the following **Ksetup** commands to add a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="0cff5-309">**En Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="0cff5-309">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="0cff5-310">Configure el conector de HDFS mediante la **autenticación de Windows** en combinación con la cuenta de dominio o la entidad de seguridad de Kerberos para conectarse al origen de datos de HDFS.</span><span class="sxs-lookup"><span data-stu-id="0cff5-310">Configure the HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal to connect to the HDFS data source.</span></span> <span data-ttu-id="0cff5-311">Compruebe la sección [HDFS Linked Service properties](#linked-service-properties) (Propiedades de servicio vinculado de HDFS) en los detalles de configuración.</span><span class="sxs-lookup"><span data-stu-id="0cff5-311">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

> [!NOTE]
> <span data-ttu-id="0cff5-312">Para asignar columnas del conjunto de datos de origen a columnas del conjunto de datos del receptor, consulte [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Asignación de columnas de conjunto de datos en Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="0cff5-312">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="performance-and-tuning"></a><span data-ttu-id="0cff5-313">Rendimiento y optimización</span><span class="sxs-lookup"><span data-stu-id="0cff5-313">Performance and Tuning</span></span>
<span data-ttu-id="0cff5-314">Consulte [Guía de optimización y rendimiento de la actividad de copia](data-factory-copy-activity-performance.md) para más información sobre los factores clave que afectan al rendimiento del movimiento de datos (actividad de copia) en Azure Data Factory y las diversas formas de optimizarlo.</span><span class="sxs-lookup"><span data-stu-id="0cff5-314">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
