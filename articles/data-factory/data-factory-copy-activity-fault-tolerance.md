---
title: "aaaAdd tolerancia a errores en la actividad de copia de factoría de datos de Azure omitiendo filas incompatibles | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooadd tolerancia a errores en la actividad de copia de factoría de datos de Azure omitiendo filas incompatibles durante la copia"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="9c35f-103">Incorporación de tolerancia a errores en la actividad de copia a través de la omisión de filas incompatibles</span><span class="sxs-lookup"><span data-stu-id="9c35f-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="9c35f-104">Factoría de datos de Azure [actividad de copia](data-factory-data-movement-activities.md) ofrece filas de dos maneras toohandle incompatible cuando se copian datos entre almacenes de datos de origen y el receptor:</span><span class="sxs-lookup"><span data-stu-id="9c35f-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways toohandle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="9c35f-105">Puede anular y producirá un error de copia de hello actividad una vez datos incompatibles detectó (comportamiento predeterminado).</span><span class="sxs-lookup"><span data-stu-id="9c35f-105">You can abort and fail hello copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="9c35f-106">Puede seguir toocopy todos los datos de hello agregando tolerancia a errores y omitir filas de datos incompatibles.</span><span class="sxs-lookup"><span data-stu-id="9c35f-106">You can continue toocopy all of hello data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="9c35f-107">Además, puede registrar filas incompatible hello en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="9c35f-107">In addition, you can log hello incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="9c35f-108">A continuación, puede examinar Hola registro toolearn Hola causa el error de hello, corregir datos hello en el origen de datos de hello y vuelva a intentar la actividad de copia de hello.</span><span class="sxs-lookup"><span data-stu-id="9c35f-108">You can then examine hello log toolearn hello cause for hello failure, fix hello data on hello data source, and retry hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="9c35f-109">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="9c35f-109">Supported scenarios</span></span>
<span data-ttu-id="9c35f-110">La actividad de copia admite tres escenarios para detectar, omitir y registrar datos incompatibles:</span><span class="sxs-lookup"><span data-stu-id="9c35f-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="9c35f-111">**Incompatibilidad entre el tipo de datos de origen de Hola y el tipo nativo de hello receptor**</span><span class="sxs-lookup"><span data-stu-id="9c35f-111">**Incompatibility between hello source data type and hello sink native type**</span></span>

    <span data-ttu-id="9c35f-112">Por ejemplo: copiar datos desde un archivo CSV en almacenamiento de Blob tooa SQL de base de datos con una definición de esquema que contiene tres **INT** columnas de tipo.</span><span class="sxs-lookup"><span data-stu-id="9c35f-112">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="9c35f-113">Hola filas de los archivos CSV que contienen datos numéricos, como `123,456,789` se copian correctamente toohello almacén de receptor.</span><span class="sxs-lookup"><span data-stu-id="9c35f-113">hello CSV file rows that contain numeric data, such as `123,456,789` are copied successfully toohello sink store.</span></span> <span data-ttu-id="9c35f-114">Sin embargo, Hola filas que contienen valores no numéricos, como `123,456,abc` se detectan como incompatibles y se omiten.</span><span class="sxs-lookup"><span data-stu-id="9c35f-114">However, hello rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="9c35f-115">**El número de columnas entre el origen de Hola y el receptor de Hola Hola no coinciden**</span><span class="sxs-lookup"><span data-stu-id="9c35f-115">**Mismatch in hello number of columns between hello source and hello sink**</span></span>

    <span data-ttu-id="9c35f-116">Por ejemplo: copiar datos desde un archivo CSV en almacenamiento de Blob tooa SQL de base de datos con una definición de esquema que contiene seis columnas.</span><span class="sxs-lookup"><span data-stu-id="9c35f-116">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="9c35f-117">Hello archivo CSV que contiene seis columnas es copió correctamente toohello almacén de receptor.</span><span class="sxs-lookup"><span data-stu-id="9c35f-117">hello CSV file rows that contain six columns are copied successfully toohello sink store.</span></span> <span data-ttu-id="9c35f-118">Hola CSV filas de los archivos que contengan más o menos de seis columnas se detectan como incompatible y se omiten.</span><span class="sxs-lookup"><span data-stu-id="9c35f-118">hello CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="9c35f-119">**Infracción de clave principal al escribir la base de datos relacional tooa**</span><span class="sxs-lookup"><span data-stu-id="9c35f-119">**Primary key violation when writing tooa relational database**</span></span>

    <span data-ttu-id="9c35f-120">Por ejemplo: copiar los datos de una base de datos SQL de SQL server tooa.</span><span class="sxs-lookup"><span data-stu-id="9c35f-120">For example: Copy data from a SQL server tooa SQL database.</span></span> <span data-ttu-id="9c35f-121">Una clave principal se define en la base de datos SQL de receptor de hello, pero dicha clave principal no se define en SQL server de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c35f-121">A primary key is defined in hello sink SQL database, but no such primary key is defined in hello source SQL server.</span></span> <span data-ttu-id="9c35f-122">filas Hola duplicado que existen en el origen de hello no pueden ser copiado toohello receptor.</span><span class="sxs-lookup"><span data-stu-id="9c35f-122">hello duplicated rows that exist in hello source cannot be copied toohello sink.</span></span> <span data-ttu-id="9c35f-123">Actividad de copia copia solo Hola primera fila de datos de origen de hello en receptor Hola.</span><span class="sxs-lookup"><span data-stu-id="9c35f-123">Copy Activity copies only hello first row of hello source data into hello sink.</span></span> <span data-ttu-id="9c35f-124">Hello fuente posterior las filas que contienen el valor de clave principal de hello duplicado se detectan como incompatible y se omiten.</span><span class="sxs-lookup"><span data-stu-id="9c35f-124">hello subsequent source rows that contain hello duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="9c35f-125">Configuración</span><span class="sxs-lookup"><span data-stu-id="9c35f-125">Configuration</span></span>
<span data-ttu-id="9c35f-126">Hello en el ejemplo siguiente se proporciona un tooconfigure de definición de JSON omitir Hola filas incompatible en la actividad de copia:</span><span class="sxs-lookup"><span data-stu-id="9c35f-126">hello following example provides a JSON definition tooconfigure skipping hello incompatible rows in Copy Activity:</span></span>

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| <span data-ttu-id="9c35f-127">Propiedad</span><span class="sxs-lookup"><span data-stu-id="9c35f-127">Property</span></span> | <span data-ttu-id="9c35f-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="9c35f-128">Description</span></span> | <span data-ttu-id="9c35f-129">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="9c35f-129">Allowed values</span></span> | <span data-ttu-id="9c35f-130">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="9c35f-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9c35f-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="9c35f-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="9c35f-132">Habilite si lo desea la omisión de filas incompatibles durante la copia.</span><span class="sxs-lookup"><span data-stu-id="9c35f-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="9c35f-133">True</span><span class="sxs-lookup"><span data-stu-id="9c35f-133">True</span></span><br/><span data-ttu-id="9c35f-134">False (valor predeterminado)</span><span class="sxs-lookup"><span data-stu-id="9c35f-134">False (default)</span></span> | <span data-ttu-id="9c35f-135">No</span><span class="sxs-lookup"><span data-stu-id="9c35f-135">No</span></span> |
| <span data-ttu-id="9c35f-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="9c35f-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="9c35f-137">Un grupo de propiedades que se pueden especifica cuando desee filas incompatibles de toolog Hola.</span><span class="sxs-lookup"><span data-stu-id="9c35f-137">A group of properties that can be specified when you want toolog hello incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="9c35f-138">No</span><span class="sxs-lookup"><span data-stu-id="9c35f-138">No</span></span> |
| <span data-ttu-id="9c35f-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="9c35f-139">**linkedServiceName**</span></span> | <span data-ttu-id="9c35f-140">Hola vinculado servicio de registro de hello toostore de almacenamiento de Azure que contiene filas de hello omitido.</span><span class="sxs-lookup"><span data-stu-id="9c35f-140">hello linked service of Azure Storage toostore hello log that contains hello skipped rows.</span></span> | <span data-ttu-id="9c35f-141">nombre de Hola de un [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) o [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) servicio, que hace referencia la instancia de almacenamiento de toohello que desea que el archivo de registro de hello toouse toostore vinculado.</span><span class="sxs-lookup"><span data-stu-id="9c35f-141">hello name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers toohello storage instance that you want toouse toostore hello log file.</span></span> | <span data-ttu-id="9c35f-142">No</span><span class="sxs-lookup"><span data-stu-id="9c35f-142">No</span></span> |
| <span data-ttu-id="9c35f-143">**path**</span><span class="sxs-lookup"><span data-stu-id="9c35f-143">**path**</span></span> | <span data-ttu-id="9c35f-144">ruta de acceso de Hola Hola del archivo de registro que contiene Hola omite filas.</span><span class="sxs-lookup"><span data-stu-id="9c35f-144">hello path of hello log file that contains hello skipped rows.</span></span> | <span data-ttu-id="9c35f-145">Especifique la ruta de almacenamiento de blobs de Hola que desea toouse toolog Hola incompatibles de los datos.</span><span class="sxs-lookup"><span data-stu-id="9c35f-145">Specify hello Blob storage path that you want toouse toolog hello incompatible data.</span></span> <span data-ttu-id="9c35f-146">Si no se proporciona una ruta de acceso, el servicio de Hola crea un contenedor para usted.</span><span class="sxs-lookup"><span data-stu-id="9c35f-146">If you do not provide a path, hello service creates a container for you.</span></span> | <span data-ttu-id="9c35f-147">No</span><span class="sxs-lookup"><span data-stu-id="9c35f-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="9c35f-148">Supervisión</span><span class="sxs-lookup"><span data-stu-id="9c35f-148">Monitoring</span></span>
<span data-ttu-id="9c35f-149">Una vez finalizada la ejecución de actividad de copia de hello, puede ver Hola número de filas omitidas en la sección supervisión de hello:</span><span class="sxs-lookup"><span data-stu-id="9c35f-149">After hello copy activity run completes, you can see hello number of skipped rows in hello monitoring section:</span></span>

![Supervisión de filas incompatibles omitidas](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="9c35f-151">Si configura filas incompatibles de toolog hello, puede encontrar el archivo de registro de hello en esta ruta de acceso: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` en archivo de registro de hello, puede ver las filas de hello omitidos y Hola a causa de incompatibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c35f-151">If you configure toolog hello incompatible rows, you can find hello log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In hello log file, you can see hello rows that were skipped and hello root cause of hello incompatibility.</span></span>

<span data-ttu-id="9c35f-152">Los datos originales de Hola y de error correspondiente Hola se registran en el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="9c35f-152">Both hello original data and hello corresponding error are logged in hello file.</span></span> <span data-ttu-id="9c35f-153">Un ejemplo de contenido del archivo de registro de hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="9c35f-153">An example of hello log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="9c35f-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9c35f-154">Next steps</span></span>
<span data-ttu-id="9c35f-155">toolearn más información acerca de la actividad de copia de factoría de datos de Azure, consulte [mover datos mediante la actividad de copia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="9c35f-155">toolearn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>
