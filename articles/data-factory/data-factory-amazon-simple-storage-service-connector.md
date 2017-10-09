---
title: "datos de aaaMove de Amazon Simple Storage Service mediante el uso de la factoría de datos | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomove datos de Amazon Simple Storage Service (S3) mediante el uso de Data Factory de Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="280d7-103">Movimiento de datos desde Amazon Simple Storage Service mediante Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="280d7-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="280d7-104">Este artículo explica cómo toouse Hola actividad de copia de datos de Data Factory de Azure toomove de Amazon Simple Storage Service (S3).</span><span class="sxs-lookup"><span data-stu-id="280d7-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="280d7-105">Se basa en hello [las actividades de movimiento de datos](data-factory-data-movement-activities.md) artículo, que presenta una descripción general de movimiento de datos con la actividad de copia de Hola.</span><span class="sxs-lookup"><span data-stu-id="280d7-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="280d7-106">Puede copiar datos de almacén de datos de Amazon S3 tooany admitida receptor.</span><span class="sxs-lookup"><span data-stu-id="280d7-106">You can copy data from Amazon S3 tooany supported sink data store.</span></span> <span data-ttu-id="280d7-107">Para obtener una lista de datos admite los almacenes como receptores de actividad de copia de hello, vea hello [admite almacenes de datos](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabla.</span><span class="sxs-lookup"><span data-stu-id="280d7-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="280d7-108">Factoría de datos admite actualmente solo migración de datos de almacenes de datos de Amazon S3 tooother, pero no mover los datos de otros datos almacena tooAmazon S3.</span><span class="sxs-lookup"><span data-stu-id="280d7-108">Data Factory currently supports only moving data from Amazon S3 tooother data stores, but not moving data from other data stores tooAmazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="280d7-109">Permisos necesarios</span><span class="sxs-lookup"><span data-stu-id="280d7-109">Required permissions</span></span>
<span data-ttu-id="280d7-110">toocopy datos de Amazon S3, asegúrese de que se le ha concedido Hola los siguientes permisos:</span><span class="sxs-lookup"><span data-stu-id="280d7-110">toocopy data from Amazon S3, make sure you have been granted hello following permissions:</span></span>

* <span data-ttu-id="280d7-111">`s3:GetObject` y `s3:GetObjectVersion` para operaciones de objeto de Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="280d7-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="280d7-112">`s3:ListBucket` para operaciones de depósito de Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="280d7-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="280d7-113">Si usas Hola Asistente para copia de generador de datos, `s3:ListAllMyBuckets` también es necesario.</span><span class="sxs-lookup"><span data-stu-id="280d7-113">If you are using hello Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="280d7-114">Para obtener más información acerca de la lista completa de Hola de Amazon S3 permisos, consulte [especificación de permisos en una directiva de](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="280d7-114">For details about hello full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="280d7-115">Introducción</span><span class="sxs-lookup"><span data-stu-id="280d7-115">Getting started</span></span>
<span data-ttu-id="280d7-116">Puede crear una canalización con una actividad de copia que mueva los datos desde un origen de Amazon S3 mediante diferentes herramientas o API.</span><span class="sxs-lookup"><span data-stu-id="280d7-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="280d7-117">toocreate de manera más fácil de Hello una canalización es hello de toouse **Asistente para copiar**.</span><span class="sxs-lookup"><span data-stu-id="280d7-117">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="280d7-118">Para ver un tutorial rápido, consulte el [tutorial sobre la creación de una canalización mediante el Asistente para copia](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="280d7-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="280d7-119">También puede usar Hola después herramientas toocreate una canalización: **portal de Azure**, **Visual Studio**, **Azure PowerShell**, **plantilla del Administrador de recursos de Azure** , **API de .NET**, y **API de REST**.</span><span class="sxs-lookup"><span data-stu-id="280d7-119">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="280d7-120">Para obtener instrucciones paso a paso toocreate una canalización con una actividad de copia, consulte hello [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="280d7-120">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="280d7-121">Si usa herramientas o las API, realizar Hola siguiendo los pasos toocreate una canalización que mueve el almacén de datos del receptor de tooa del almacén de datos desde un origen de datos:</span><span class="sxs-lookup"><span data-stu-id="280d7-121">Whether you use tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="280d7-122">Crear **servicios vinculados** factoría de datos de tooyour de almacenes de datos de entrada y salida de toolink.</span><span class="sxs-lookup"><span data-stu-id="280d7-122">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="280d7-123">Crear **conjuntos de datos** toorepresent de entrada y salida la operación de copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="280d7-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="280d7-124">Cree una **canalización** con una actividad de copia que tome como entrada un conjunto de datos y un conjunto de datos como salida.</span><span class="sxs-lookup"><span data-stu-id="280d7-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="280d7-125">Cuando se utiliza el Asistente de hello, las definiciones de JSON para estas entidades de la factoría de datos (servicios vinculados, conjuntos de datos y canalización Hola) se crean automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="280d7-125">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="280d7-126">Al usar herramientas o las API (excepto la API. NET), se definen estas entidades de la factoría de datos con formato JSON de Hola.</span><span class="sxs-lookup"><span data-stu-id="280d7-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="280d7-127">Para obtener un ejemplo con definiciones de JSON para entidades de la factoría de datos que son datos de uso toocopy desde un almacén de datos de Amazon S3, vea hello [ejemplo de JSON: copiar los datos de Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="280d7-127">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon S3 data store, see hello [JSON example: Copy data from Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="280d7-128">Para información sobre los formatos de compresión y de archivo compatibles para una actividad de copia, consulte [Formatos de archivo y de compresión admitidos en Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="280d7-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="280d7-129">Hello las secciones siguientes proporciona detalles acerca de las propiedades JSON que son utilizados toodefine factoría de datos entidades específica tooAmazon S3.</span><span class="sxs-lookup"><span data-stu-id="280d7-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="280d7-130">Propiedades del servicio vinculado</span><span class="sxs-lookup"><span data-stu-id="280d7-130">Linked service properties</span></span>
<span data-ttu-id="280d7-131">Un servicio vinculado vincula una factoría de datos de tooa de almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="280d7-131">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="280d7-132">Crear un servicio vinculado de tipo **AwsAccessKey** toolink tooyour factoría de datos del almacén de los datos de Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="280d7-132">You create a linked service of type **AwsAccessKey** toolink your Amazon S3 data store tooyour data factory.</span></span> <span data-ttu-id="280d7-133">Hello en la tabla siguiente proporciona el servicio de descripción para JSON elementos específico tooAmazon S3 (AwsAccessKey) que se vincula.</span><span class="sxs-lookup"><span data-stu-id="280d7-133">hello following table provides description for JSON elements specific tooAmazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="280d7-134">Propiedad</span><span class="sxs-lookup"><span data-stu-id="280d7-134">Property</span></span> | <span data-ttu-id="280d7-135">Descripción</span><span class="sxs-lookup"><span data-stu-id="280d7-135">Description</span></span> | <span data-ttu-id="280d7-136">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="280d7-136">Allowed values</span></span> | <span data-ttu-id="280d7-137">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="280d7-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="280d7-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="280d7-138">accessKeyID</span></span> |<span data-ttu-id="280d7-139">Id. de clave de acceso de los secretos de Hola.</span><span class="sxs-lookup"><span data-stu-id="280d7-139">ID of hello secret access key.</span></span> |<span data-ttu-id="280d7-140">cadena</span><span class="sxs-lookup"><span data-stu-id="280d7-140">string</span></span> |<span data-ttu-id="280d7-141">Sí</span><span class="sxs-lookup"><span data-stu-id="280d7-141">Yes</span></span> |
| <span data-ttu-id="280d7-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="280d7-142">secretAccessKey</span></span> |<span data-ttu-id="280d7-143">clave de acceso de los secretos de Hello propio.</span><span class="sxs-lookup"><span data-stu-id="280d7-143">hello secret access key itself.</span></span> |<span data-ttu-id="280d7-144">Cadena secreta cifrada</span><span class="sxs-lookup"><span data-stu-id="280d7-144">Encrypted secret string</span></span> |<span data-ttu-id="280d7-145">Sí</span><span class="sxs-lookup"><span data-stu-id="280d7-145">Yes</span></span> |

<span data-ttu-id="280d7-146">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="280d7-146">Here is an example:</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="280d7-147">Propiedades del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="280d7-147">Dataset properties</span></span>
<span data-ttu-id="280d7-148">toospecify toorepresent de un conjunto de datos de entrada de datos en el almacenamiento de blobs de Azure, propiedad de tipo de conjunto Hola del conjunto de datos de hello demasiado**AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="280d7-148">toospecify a dataset toorepresent input data in Azure Blob storage, set hello type property of hello dataset too**AmazonS3**.</span></span> <span data-ttu-id="280d7-149">Conjunto hello **linkedServiceName** servicio vinculado de propiedad del nombre de toohello de conjunto de datos de Hola de hello S3 de Amazon.</span><span class="sxs-lookup"><span data-stu-id="280d7-149">Set hello **linkedServiceName** property of hello dataset toohello name of hello Amazon S3 linked service.</span></span> <span data-ttu-id="280d7-150">Para ver una lista completa de las secciones y propiedades disponibles para definir conjuntos de datos, consulte [Creación de conjuntos de datos](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="280d7-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="280d7-151">Las secciones como structure, availability y policy son similares para todos los tipos de conjunto de datos (como base de datos SQL, blob de Azure y tabla de Azure).</span><span class="sxs-lookup"><span data-stu-id="280d7-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="280d7-152">Hola **typeProperties** sección es diferente para cada tipo de conjunto de datos y se proporciona información acerca de la ubicación de Hola de hello datos Hola almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="280d7-152">hello **typeProperties** section is different for each type of dataset, and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="280d7-153">Hola **typeProperties** sección para un conjunto de datos de tipo **AmazonS3** (que incluye el conjunto de datos de hello Amazon S3) tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="280d7-153">hello **typeProperties** section for a dataset of type **AmazonS3** (which includes hello Amazon S3 dataset) has hello following properties:</span></span>

| <span data-ttu-id="280d7-154">Propiedad</span><span class="sxs-lookup"><span data-stu-id="280d7-154">Property</span></span> | <span data-ttu-id="280d7-155">Descripción</span><span class="sxs-lookup"><span data-stu-id="280d7-155">Description</span></span> | <span data-ttu-id="280d7-156">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="280d7-156">Allowed values</span></span> | <span data-ttu-id="280d7-157">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="280d7-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="280d7-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="280d7-158">bucketName</span></span> |<span data-ttu-id="280d7-159">nombre del depósito de Hello S3.</span><span class="sxs-lookup"><span data-stu-id="280d7-159">hello S3 bucket name.</span></span> |<span data-ttu-id="280d7-160">String</span><span class="sxs-lookup"><span data-stu-id="280d7-160">String</span></span> |<span data-ttu-id="280d7-161">Sí</span><span class="sxs-lookup"><span data-stu-id="280d7-161">Yes</span></span> |
| <span data-ttu-id="280d7-162">key</span><span class="sxs-lookup"><span data-stu-id="280d7-162">key</span></span> |<span data-ttu-id="280d7-163">clave del objeto Hola S3.</span><span class="sxs-lookup"><span data-stu-id="280d7-163">hello S3 object key.</span></span> |<span data-ttu-id="280d7-164">String</span><span class="sxs-lookup"><span data-stu-id="280d7-164">String</span></span> |<span data-ttu-id="280d7-165">No</span><span class="sxs-lookup"><span data-stu-id="280d7-165">No</span></span> |
| <span data-ttu-id="280d7-166">prefix</span><span class="sxs-lookup"><span data-stu-id="280d7-166">prefix</span></span> |<span data-ttu-id="280d7-167">Prefijo para la clave del objeto Hola S3.</span><span class="sxs-lookup"><span data-stu-id="280d7-167">Prefix for hello S3 object key.</span></span> <span data-ttu-id="280d7-168">Se seleccionan objetos cuyas claves comienzan por este prefijo.</span><span class="sxs-lookup"><span data-stu-id="280d7-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="280d7-169">Se aplica solo cuando la clave está vacía.</span><span class="sxs-lookup"><span data-stu-id="280d7-169">Applies only when key is empty.</span></span> |<span data-ttu-id="280d7-170">string</span><span class="sxs-lookup"><span data-stu-id="280d7-170">String</span></span> |<span data-ttu-id="280d7-171">No</span><span class="sxs-lookup"><span data-stu-id="280d7-171">No</span></span> |
| <span data-ttu-id="280d7-172">versión</span><span class="sxs-lookup"><span data-stu-id="280d7-172">version</span></span> |<span data-ttu-id="280d7-173">versión de Hola del objeto de hello S3, si está habilitado el control de versiones de S3.</span><span class="sxs-lookup"><span data-stu-id="280d7-173">hello version of hello S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="280d7-174">String</span><span class="sxs-lookup"><span data-stu-id="280d7-174">String</span></span> |<span data-ttu-id="280d7-175">No</span><span class="sxs-lookup"><span data-stu-id="280d7-175">No</span></span> |
| <span data-ttu-id="280d7-176">formato</span><span class="sxs-lookup"><span data-stu-id="280d7-176">format</span></span> | <span data-ttu-id="280d7-177">se admite los siguientes tipos de formato de Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="280d7-177">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="280d7-178">Conjunto hello **tipo** propiedad en formato tooone de estos valores.</span><span class="sxs-lookup"><span data-stu-id="280d7-178">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="280d7-179">Para obtener más información, vea hello [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [el formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), y [formato Parquet ](data-factory-supported-file-and-compression-formats.md#parquet-format) secciones.</span><span class="sxs-lookup"><span data-stu-id="280d7-179">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="280d7-180">Si desea que los archivos de toocopy como-está entre los almacenes basados en archivos (copia binaria), sección de formato de hello skip en ambas definiciones de conjunto de datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="280d7-180">If you want toocopy files as-is between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="280d7-181">No</span><span class="sxs-lookup"><span data-stu-id="280d7-181">No</span></span> | |
| <span data-ttu-id="280d7-182">compresión</span><span class="sxs-lookup"><span data-stu-id="280d7-182">compression</span></span> | <span data-ttu-id="280d7-183">Especificar tipo de Hola y el nivel de compresión para datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="280d7-183">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="280d7-184">tipos de Hello admitido son: **GZip**, **Deflate**, **BZip2**, y **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="280d7-184">hello supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="280d7-185">Hola admitida niveles son: **óptimo** y **más rápido**.</span><span class="sxs-lookup"><span data-stu-id="280d7-185">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="280d7-186">Para obtener más información, consulte el artículo sobre [formatos de archivo y compresión en Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="280d7-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="280d7-187">No</span><span class="sxs-lookup"><span data-stu-id="280d7-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="280d7-188">**bucketName + tecla** especifica la ubicación de Hola Hola S3 de objeto de, donde depósitos es el contenedor de raíz de Hola para S3 objetos, y la clave es objeto de toohello S3 de ruta de acceso completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="280d7-188">**bucketName + key** specifies hello location of hello S3 object, where bucket is hello root container for S3 objects, and key is hello full path toohello S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="280d7-189">Conjunto de datos de ejemplo con prefijo</span><span class="sxs-lookup"><span data-stu-id="280d7-189">Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a><span data-ttu-id="280d7-190">Conjunto de datos de ejemplo (con versión)</span><span class="sxs-lookup"><span data-stu-id="280d7-190">Sample dataset (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="280d7-191">Rutas de acceso dinámicas para S3</span><span class="sxs-lookup"><span data-stu-id="280d7-191">Dynamic paths for S3</span></span>
<span data-ttu-id="280d7-192">Hello en el ejemplo anterior utiliza valores fijos para hello **clave** y **bucketName** propiedades de conjunto de datos de hello S3 de Amazon.</span><span class="sxs-lookup"><span data-stu-id="280d7-192">hello preceding sample uses fixed values for hello **key** and **bucketName** properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="280d7-193">Puede hacer que Data Factory calcule estas propiedades dinámicamente en tiempo de ejecución mediante variables del sistema como SliceStart.</span><span class="sxs-lookup"><span data-stu-id="280d7-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="280d7-194">Puede hacer Hola igual para hello **prefijo** propiedad de un conjunto de datos de Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="280d7-194">You can do hello same for hello **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="280d7-195">Para ver una lista de funciones y variables admitidas, consulte [Azure Data Factory: funciones y variables del sistema](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="280d7-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="280d7-196">Propiedades de la actividad de copia</span><span class="sxs-lookup"><span data-stu-id="280d7-196">Copy activity properties</span></span>
<span data-ttu-id="280d7-197">Para ver una lista completa de las secciones y propiedades disponibles para definir actividades, consulte [Creación de canalizaciones](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="280d7-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="280d7-198">Las propiedades (como nombre, descripción, tablas de entrada y salida, y directivas) están disponibles para todos los tipos de actividades.</span><span class="sxs-lookup"><span data-stu-id="280d7-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="280d7-199">Propiedades disponibles en hello **typeProperties** sección de actividad hello varían con cada tipo de actividad.</span><span class="sxs-lookup"><span data-stu-id="280d7-199">Properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="280d7-200">Para la actividad de copia de hello, propiedades varían en función de tipos de Hola de orígenes y receptores.</span><span class="sxs-lookup"><span data-stu-id="280d7-200">For hello copy activity, properties vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="280d7-201">Cuando un origen de la actividad de copia de hello es del tipo **FileSystemSource** (que incluye Amazon S3), Hola después de la propiedad está disponible en **typeProperties** sección:</span><span class="sxs-lookup"><span data-stu-id="280d7-201">When a source in hello copy activity is of type **FileSystemSource** (which includes Amazon S3), hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="280d7-202">Propiedad</span><span class="sxs-lookup"><span data-stu-id="280d7-202">Property</span></span> | <span data-ttu-id="280d7-203">Descripción</span><span class="sxs-lookup"><span data-stu-id="280d7-203">Description</span></span> | <span data-ttu-id="280d7-204">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="280d7-204">Allowed values</span></span> | <span data-ttu-id="280d7-205">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="280d7-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="280d7-206">recursive</span><span class="sxs-lookup"><span data-stu-id="280d7-206">recursive</span></span> |<span data-ttu-id="280d7-207">Especifica si toorecursively lista S3 objetos en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="280d7-207">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="280d7-208">true/false</span><span class="sxs-lookup"><span data-stu-id="280d7-208">true/false</span></span> |<span data-ttu-id="280d7-209">No</span><span class="sxs-lookup"><span data-stu-id="280d7-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a><span data-ttu-id="280d7-210">Ejemplo de JSON: copiar los datos de Amazon S3 tooAzure almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="280d7-210">JSON example: Copy data from Amazon S3 tooAzure Blob storage</span></span>
<span data-ttu-id="280d7-211">Este ejemplo se muestra cómo toocopy datos de Amazon S3 tooan almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="280d7-211">This sample shows how toocopy data from Amazon S3 tooan Azure Blob storage.</span></span> <span data-ttu-id="280d7-212">Sin embargo, se pueden copiar datos directamente demasiado[cualquiera de los receptores de Hola que se admiten](data-factory-data-movement-activities.md#supported-data-stores-and-formats) mediante el uso de actividad de copia de hello de factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="280d7-212">However, data can be copied directly too[any of hello sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using hello copy activity in Data Factory.</span></span>

<span data-ttu-id="280d7-213">ejemplo de Hola proporciona definiciones de JSON para hello siguiendo las entidades de la factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="280d7-213">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="280d7-214">Puede usar estos toocreate definiciones una toocopy de datos de canalización desde el almacenamiento de Amazon S3 tooBlob, mediante el uso de hello [portal de Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), o [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="280d7-214">You can use these definitions toocreate a pipeline toocopy data from Amazon S3 tooBlob storage, by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="280d7-215">Un servicio vinculado de tipo [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="280d7-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="280d7-216">Un servicio vinculado de tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="280d7-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="280d7-217">Un [conjunto de datos](data-factory-create-datasets.md) de tipo [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="280d7-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="280d7-218">Un [conjunto de datos](data-factory-create-datasets.md) de salida de tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="280d7-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="280d7-219">Una [canalización](data-factory-create-pipelines.md) con actividad de copia que usa [FileSystemSource](#copy-activity-properties) y [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="280d7-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="280d7-220">ejemplo de Hola copia datos de Amazon S3 tooan blobs de Azure cada hora.</span><span class="sxs-lookup"><span data-stu-id="280d7-220">hello sample copies data from Amazon S3 tooan Azure blob every hour.</span></span> <span data-ttu-id="280d7-221">propiedades JSON de Hello utilizadas en estos ejemplos se describen en los apartados siguientes a los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="280d7-221">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="280d7-222">Servicio vinculado de Amazon S3</span><span class="sxs-lookup"><span data-stu-id="280d7-222">Amazon S3 linked service</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="280d7-223">Servicio vinculado de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="280d7-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="280d7-224">Conjunto de datos de entrada de Amazon S3</span><span class="sxs-lookup"><span data-stu-id="280d7-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="280d7-225">Establecer **"externo": true** informa servicio Data Factory de hello ese conjunto de datos de hello es externo toohello factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="280d7-225">Setting **"external": true** informs hello Data Factory service that hello dataset is external toohello data factory.</span></span> <span data-ttu-id="280d7-226">Establecer esta propiedad tootrue en un conjunto de datos de entrada que no se crea una actividad de canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="280d7-226">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="280d7-227">Conjunto de datos de salida de blob de Azure</span><span class="sxs-lookup"><span data-stu-id="280d7-227">Azure Blob output dataset</span></span>

<span data-ttu-id="280d7-228">Los datos se escriben tooa nuevo blob cada hora (frecuencia: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="280d7-228">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="280d7-229">ruta de acceso de carpeta de Hola para blob Hola se evalúa dinámicamente según el tiempo de inicio de Hola de sector de Hola que se está procesando.</span><span class="sxs-lookup"><span data-stu-id="280d7-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="280d7-230">ruta de acceso de carpeta Hola utiliza elementos de año, mes, día y horas de Hola Hola hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="280d7-230">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="280d7-231">Actividad de copia en una canalización con un origen de Amazon S3 y un receptor de blob</span><span class="sxs-lookup"><span data-stu-id="280d7-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="280d7-232">Hello canalización contiene una actividad de copia que está configurado toouse Hola conjuntos de datos de entrada y salida, y es toorun programada cada hora.</span><span class="sxs-lookup"><span data-stu-id="280d7-232">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="280d7-233">En la definición de JSON de canalización de hello, Hola **origen** tipo está establecido demasiado**FileSystemSource**, y **receptor** tipo está establecido demasiado**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="280d7-233">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="280d7-234">columnas de toomap de un toocolumns de conjunto de datos de origen de un conjunto de datos del receptor, consulte [asignar columnas de conjunto de datos de Data Factory de Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="280d7-234">toomap columns from a source dataset toocolumns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="280d7-235">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="280d7-235">Next steps</span></span>
<span data-ttu-id="280d7-236">Vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="280d7-236">See hello following articles:</span></span>

* <span data-ttu-id="280d7-237">toolearn acerca de la clave de factores que afectan al rendimiento de movimiento de datos (actividad de copia) en la factoría de datos y toooptimize de diversas formas, vea hello [copiar actividad Guía de rendimiento y optimización](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="280d7-237">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="280d7-238">Para obtener instrucciones paso a paso para crear una canalización con una actividad de copia, consulte hello [tutorial de la actividad de copia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="280d7-238">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
