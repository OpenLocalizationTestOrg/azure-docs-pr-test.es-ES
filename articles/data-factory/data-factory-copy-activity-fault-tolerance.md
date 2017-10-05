---
title: "Incorporación de tolerancia a errores en la actividad de copia de Azure Data Factory a través de la omisión de filas incompatibles | Microsoft Docs"
description: "Obtenga información sobre cómo agregar tolerancia a errores en la actividad de copia de Azure Data Factory a través de la omisión de filas incompatibles durante la copia"
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
ms.openlocfilehash: e2a108752259d5da3b401666c6bdbaad13b7ea90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="d5648-103">Incorporación de tolerancia a errores en la actividad de copia a través de la omisión de filas incompatibles</span><span class="sxs-lookup"><span data-stu-id="d5648-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="d5648-104">La [actividad de copia](data-factory-data-movement-activities.md) de Azure Data Factory ofrece dos maneras para tratar con filas incompatibles cuando se copian datos entre almacenes de datos de origen y de receptor:</span><span class="sxs-lookup"><span data-stu-id="d5648-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways to handle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="d5648-105">Puede anular y omitir la actividad de copia cuando se encuentren datos incompatibles (comportamiento predeterminado).</span><span class="sxs-lookup"><span data-stu-id="d5648-105">You can abort and fail the copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="d5648-106">Se puede continuar copiando todos los datos a través de la incorporación de tolerancia a errores y la omisión de filas de datos incompatibles.</span><span class="sxs-lookup"><span data-stu-id="d5648-106">You can continue to copy all of the data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="d5648-107">Además, puede registrar las filas incompatibles en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="d5648-107">In addition, you can log the incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="d5648-108">Luego puede examinar el registro para obtener información sobre la causa del error, corregir los datos en el origen de datos y reintentar la actividad de copia.</span><span class="sxs-lookup"><span data-stu-id="d5648-108">You can then examine the log to learn the cause for the failure, fix the data on the data source, and retry the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="d5648-109">Escenarios admitidos</span><span class="sxs-lookup"><span data-stu-id="d5648-109">Supported scenarios</span></span>
<span data-ttu-id="d5648-110">La actividad de copia admite tres escenarios para detectar, omitir y registrar datos incompatibles:</span><span class="sxs-lookup"><span data-stu-id="d5648-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="d5648-111">**Incompatibilidad entre el tipo de datos de origen y el tipo nativo de receptor**</span><span class="sxs-lookup"><span data-stu-id="d5648-111">**Incompatibility between the source data type and the sink native type**</span></span>

    <span data-ttu-id="d5648-112">Por ejemplo: copie los datos desde un archivo CSV en Blob Storage a una base de datos SQL con una definición de esquema que contiene tres columnas de tipo **INT**.</span><span class="sxs-lookup"><span data-stu-id="d5648-112">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="d5648-113">Las filas del archivo CSV que contienen datos numéricos, como `123,456,789`, se copian correctamente en el almacén de receptor.</span><span class="sxs-lookup"><span data-stu-id="d5648-113">The CSV file rows that contain numeric data, such as `123,456,789` are copied successfully to the sink store.</span></span> <span data-ttu-id="d5648-114">Sin embargo, las filas que contienen valores no numéricos, como `123,456,abc`, se detectan como incompatibles y se omiten.</span><span class="sxs-lookup"><span data-stu-id="d5648-114">However, the rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="d5648-115">**Error de coincidencia en el número de columnas entre el origen y el receptor**</span><span class="sxs-lookup"><span data-stu-id="d5648-115">**Mismatch in the number of columns between the source and the sink**</span></span>

    <span data-ttu-id="d5648-116">Por ejemplo: copie los datos desde un archivo CSV en Blob Storage a una base de datos SQL con una definición de esquema que contiene seis columnas.</span><span class="sxs-lookup"><span data-stu-id="d5648-116">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="d5648-117">Las filas del archivo CSV que contiene seis columnas se copian correctamente en el almacén de receptor.</span><span class="sxs-lookup"><span data-stu-id="d5648-117">The CSV file rows that contain six columns are copied successfully to the sink store.</span></span> <span data-ttu-id="d5648-118">Las filas del archivo CSV que contienen más o menos de seis columnas se detectan como incompatibles y se omiten.</span><span class="sxs-lookup"><span data-stu-id="d5648-118">The CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="d5648-119">**Infracción de clave principal al escribir en una base de datos relacional**</span><span class="sxs-lookup"><span data-stu-id="d5648-119">**Primary key violation when writing to a relational database**</span></span>

    <span data-ttu-id="d5648-120">Por ejemplo: copie datos desde un servidor SQL a una base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="d5648-120">For example: Copy data from a SQL server to a SQL database.</span></span> <span data-ttu-id="d5648-121">Se define una clave principal en la base de datos SQL de receptor, pero no se define en el servidor SQL de origen.</span><span class="sxs-lookup"><span data-stu-id="d5648-121">A primary key is defined in the sink SQL database, but no such primary key is defined in the source SQL server.</span></span> <span data-ttu-id="d5648-122">Las filas duplicadas que existen en el origen no se pueden copiar en el receptor.</span><span class="sxs-lookup"><span data-stu-id="d5648-122">The duplicated rows that exist in the source cannot be copied to the sink.</span></span> <span data-ttu-id="d5648-123">La actividad de copia solo copia la primera fila de los datos de origen en el receptor.</span><span class="sxs-lookup"><span data-stu-id="d5648-123">Copy Activity copies only the first row of the source data into the sink.</span></span> <span data-ttu-id="d5648-124">Las filas de origen subsiguientes que contienen el valor de clave principal duplicado se detectan como incompatibles y se omiten.</span><span class="sxs-lookup"><span data-stu-id="d5648-124">The subsequent source rows that contain the duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="d5648-125">Configuración</span><span class="sxs-lookup"><span data-stu-id="d5648-125">Configuration</span></span>
<span data-ttu-id="d5648-126">En el ejemplo siguiente se proporciona una definición JSON para configurar la omisión de las filas incompatibles en la actividad de copia:</span><span class="sxs-lookup"><span data-stu-id="d5648-126">The following example provides a JSON definition to configure skipping the incompatible rows in Copy Activity:</span></span>

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

| <span data-ttu-id="d5648-127">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d5648-127">Property</span></span> | <span data-ttu-id="d5648-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="d5648-128">Description</span></span> | <span data-ttu-id="d5648-129">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="d5648-129">Allowed values</span></span> | <span data-ttu-id="d5648-130">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d5648-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d5648-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="d5648-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="d5648-132">Habilite si lo desea la omisión de filas incompatibles durante la copia.</span><span class="sxs-lookup"><span data-stu-id="d5648-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="d5648-133">True</span><span class="sxs-lookup"><span data-stu-id="d5648-133">True</span></span><br/><span data-ttu-id="d5648-134">False (valor predeterminado)</span><span class="sxs-lookup"><span data-stu-id="d5648-134">False (default)</span></span> | <span data-ttu-id="d5648-135">No</span><span class="sxs-lookup"><span data-stu-id="d5648-135">No</span></span> |
| <span data-ttu-id="d5648-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="d5648-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="d5648-137">Un grupo de propiedades que puede especificarse cuando quiere registrar las filas incompatibles.</span><span class="sxs-lookup"><span data-stu-id="d5648-137">A group of properties that can be specified when you want to log the incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="d5648-138">No</span><span class="sxs-lookup"><span data-stu-id="d5648-138">No</span></span> |
| <span data-ttu-id="d5648-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="d5648-139">**linkedServiceName**</span></span> | <span data-ttu-id="d5648-140">El servicio vinculado de Azure Storage para almacenar el registro que contiene las filas que se omiten.</span><span class="sxs-lookup"><span data-stu-id="d5648-140">The linked service of Azure Storage to store the log that contains the skipped rows.</span></span> | <span data-ttu-id="d5648-141">El nombre de un servicio vinculado de [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) o [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service), que hace referencia a la instancia de almacenamiento que desea usar para almacenar el archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="d5648-141">The name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers to the storage instance that you want to use to store the log file.</span></span> | <span data-ttu-id="d5648-142">No</span><span class="sxs-lookup"><span data-stu-id="d5648-142">No</span></span> |
| <span data-ttu-id="d5648-143">**path**</span><span class="sxs-lookup"><span data-stu-id="d5648-143">**path**</span></span> | <span data-ttu-id="d5648-144">La ruta de acceso del archivo de registro que contiene las filas que se omiten.</span><span class="sxs-lookup"><span data-stu-id="d5648-144">The path of the log file that contains the skipped rows.</span></span> | <span data-ttu-id="d5648-145">Especifique la ruta de acceso de Blob Storage que desee usar para registrar los datos incompatibles.</span><span class="sxs-lookup"><span data-stu-id="d5648-145">Specify the Blob storage path that you want to use to log the incompatible data.</span></span> <span data-ttu-id="d5648-146">Si no se proporciona una ruta de acceso, el servicio creará un contenedor para usted.</span><span class="sxs-lookup"><span data-stu-id="d5648-146">If you do not provide a path, the service creates a container for you.</span></span> | <span data-ttu-id="d5648-147">No</span><span class="sxs-lookup"><span data-stu-id="d5648-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="d5648-148">Supervisión</span><span class="sxs-lookup"><span data-stu-id="d5648-148">Monitoring</span></span>
<span data-ttu-id="d5648-149">Una vez que se completa la ejecución de la actividad de copia, puede ver el número de filas omitidas en la sección de supervisión:</span><span class="sxs-lookup"><span data-stu-id="d5648-149">After the copy activity run completes, you can see the number of skipped rows in the monitoring section:</span></span>

![Supervisión de filas incompatibles omitidas](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="d5648-151">Si configura el registro de las filas incompatibles, puede encontrar el archivo de registro en esta ruta de acceso: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` En el archivo de registro, puede ver las filas que se omitieron y la causa principal de la incompatibilidad.</span><span class="sxs-lookup"><span data-stu-id="d5648-151">If you configure to log the incompatible rows, you can find the log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In the log file, you can see the rows that were skipped and the root cause of the incompatibility.</span></span>

<span data-ttu-id="d5648-152">Los datos originales y el error correspondiente se registran en el archivo.</span><span class="sxs-lookup"><span data-stu-id="d5648-152">Both the original data and the corresponding error are logged in the file.</span></span> <span data-ttu-id="d5648-153">A continuación se muestra un ejemplo del contenido del archivo de registro:</span><span class="sxs-lookup"><span data-stu-id="d5648-153">An example of the log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' to type 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. The duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="d5648-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d5648-154">Next steps</span></span>
<span data-ttu-id="d5648-155">Para más información sobre la actividad de copia de Azure Data Factory, consulte [Movimiento de datos con la actividad de copia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="d5648-155">To learn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>