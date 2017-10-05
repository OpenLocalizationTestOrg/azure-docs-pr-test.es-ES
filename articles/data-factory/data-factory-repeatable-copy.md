---
title: Copia repetible en Azure Data Factory| Microsoft Docs
description: "Aprenda a evitar duplicados aunque un segmento que copia datos se ejecute más de una vez."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 5b88a235915bf35fec701eee4a5f80beb4a67632
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="3ea90-103">Copia repetible en Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3ea90-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="3ea90-104">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="3ea90-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="3ea90-105">Cuando se copian datos desde almacenes de datos relacionales, hay que tener presente la repetibilidad para evitar resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="3ea90-105">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="3ea90-106">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="3ea90-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="3ea90-107">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="3ea90-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="3ea90-108">Cuando se vuelve a ejecutar un segmento, debe asegurarse de que los mismos datos se leen sin importar cuántas veces se ejecuta un segmento.</span><span class="sxs-lookup"><span data-stu-id="3ea90-108">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="3ea90-109">Los ejemplos siguientes son para SQL Azure, pero son aplicables a cualquier almacén de datos que admita conjuntos de datos rectangulares.</span><span class="sxs-lookup"><span data-stu-id="3ea90-109">The following samples are for Azure SQL but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="3ea90-110">Puede que deba ajustar el **tipo** de origen y la propiedad de la **consulta** (por ejemplo, consulta en lugar de sqlReaderQuery) del almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="3ea90-110">You may have to adjust the **type** of source and the **query** property (for example: query instead of sqlReaderQuery) for the data store.</span></span>   

<span data-ttu-id="3ea90-111">Normalmente, al leer desde almacenes relacionales, lo que quiere es leer únicamente los datos correspondientes a ese segmento.</span><span class="sxs-lookup"><span data-stu-id="3ea90-111">Usually, when reading from relational stores, you want to read only the data corresponding to that slice.</span></span> <span data-ttu-id="3ea90-112">Una manera de hacerlo sería usar las variables WindowStart y WindowEnd disponibles en Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3ea90-112">A way to do so would be by using the WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="3ea90-113">Lea sobre las variables y funciones de Azure Data Factory aquí en el artículo [Azure Data Factory: funciones y variables del sistema](data-factory-functions-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="3ea90-113">Read about the variables and functions in Azure Data Factory here in the [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="3ea90-114">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3ea90-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="3ea90-115">Esta consulta lee los datos que se encuentran en el intervalo de duración del segmento (WindowStart-> WindowEnd) de la tabla MyTable.</span><span class="sxs-lookup"><span data-stu-id="3ea90-115">This query reads data that falls in the slice duration range (WindowStart -> WindowEnd) from the table MyTable.</span></span> <span data-ttu-id="3ea90-116">Una segunda ejecución de este segmento también garantizará que se leen los mismos datos.</span><span class="sxs-lookup"><span data-stu-id="3ea90-116">Rerun of this slice would also always ensure that the same data is read.</span></span> 

<span data-ttu-id="3ea90-117">En otros casos, puede que desee leer toda la tabla y puede definir el valor de sqlReaderQuery de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="3ea90-117">In other cases, you may wish to read the entire table and may define the sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-to-sqlsink"></a><span data-ttu-id="3ea90-118">Escritura repetible en SqlSink</span><span class="sxs-lookup"><span data-stu-id="3ea90-118">Repeatable write to SqlSink</span></span>
<span data-ttu-id="3ea90-119">Cuando se copian datos en **Azure SQL o SQL Server desde** otros orígenes de datos, es necesario tener en mente la repetibilidad para evitar resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="3ea90-119">When copying data to **Azure SQL/SQL Server** from other data stores, you need to keep repeatability in mind to avoid unintended outcomes.</span></span> 

<span data-ttu-id="3ea90-120">Cuando se copien datos en Azure SQL o SQL Server Database, la actividad de copia anexa datos a la tabla del receptor de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3ea90-120">When copying data to Azure SQL/SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="3ea90-121">Supongamos que va a copiar datos de un archivo CSV (valores separados por comas) que contiene dos registros en la siguiente tabla en una instancia de Azure SQL o SQL Server Database.</span><span class="sxs-lookup"><span data-stu-id="3ea90-121">Say, you are copying data from a CSV (comma-separated values) file containing two records to the following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="3ea90-122">Cuando se ejecuta un segmento, se copian los dos registros en la tabla SQL.</span><span class="sxs-lookup"><span data-stu-id="3ea90-122">When a slice runs, the two records are copied to the SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="3ea90-123">Supongamos que encontró errores en el archivo de origen y actualizó la cantidad de Down Tube de 2 a 4.</span><span class="sxs-lookup"><span data-stu-id="3ea90-123">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4.</span></span> <span data-ttu-id="3ea90-124">Si vuelve a ejecutar el segmento de datos durante ese período, encontrará dos nuevos registros anexados a Azure SQL o SQL Server Database.</span><span class="sxs-lookup"><span data-stu-id="3ea90-124">If you rerun the data slice for that period manually, you’ll find two new records appended to Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="3ea90-125">En este ejemplo se asume que ninguna de las columnas de la tabla tiene la restricción de clave principal.</span><span class="sxs-lookup"><span data-stu-id="3ea90-125">This example assumes that none of the columns in the table has the primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="3ea90-126">Para evitar este comportamiento, debe especificar una semántica UPSERT mediante uno de los dos mecanismos siguientes:</span><span class="sxs-lookup"><span data-stu-id="3ea90-126">To avoid this behavior, you need to specify UPSERT semantics by using one of the following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="3ea90-127">Mecanismo 1: Uso de sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="3ea90-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="3ea90-128">Puede usar la propiedad **sqlWriterCleanupScript** para limpiar los datos de la tabla del receptor antes de insertar los datos cuando se ejecuta un segmento.</span><span class="sxs-lookup"><span data-stu-id="3ea90-128">You can use the **sqlWriterCleanupScript** property to clean up data from the sink table before inserting the data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="3ea90-129">Cuando se ejecuta un segmento, el script de limpieza se ejecuta primero para eliminar los datos que corresponden al segmento de la tabla de SQL.</span><span class="sxs-lookup"><span data-stu-id="3ea90-129">When a slice runs, the cleanup script is run first to delete data that corresponds to the slice from the SQL table.</span></span> <span data-ttu-id="3ea90-130">La actividad de copia inserta entonces datos en la tabla de SQL.</span><span class="sxs-lookup"><span data-stu-id="3ea90-130">The copy activity then inserts data into the SQL Table.</span></span> <span data-ttu-id="3ea90-131">Si se vuelve a ejecutar el segmento, la cantidad se actualiza según de la forma deseada.</span><span class="sxs-lookup"><span data-stu-id="3ea90-131">If the slice is rerun, the quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="3ea90-132">Supongamos que se quita el registro Flat Washer desde el archivo csv original.</span><span class="sxs-lookup"><span data-stu-id="3ea90-132">Suppose the Flat Washer record is removed from the original csv.</span></span> <span data-ttu-id="3ea90-133">Después, si vuelve a ejecutar el segmento, se producirá el siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="3ea90-133">Then rerunning the slice would produce the following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="3ea90-134">La actividad de copia ejecutó el script de limpieza para eliminar los datos correspondientes para ese segmento.</span><span class="sxs-lookup"><span data-stu-id="3ea90-134">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span></span> <span data-ttu-id="3ea90-135">Luego leyó la entrada del archivo csv (que entonces solo contenía un registro) y la insertó en la tabla.</span><span class="sxs-lookup"><span data-stu-id="3ea90-135">Then it read the input from the csv (which then contained only one record) and inserted it into the Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="3ea90-136">Mecanismo 2: Uso de sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="3ea90-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3ea90-137">sliceIdentifierColumnName no se admite en este momento para Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3ea90-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="3ea90-138">El segundo mecanismo para lograr la repetibilidad es tener una columna dedicada (sliceIdentifierColumnName) en la tabla de destino.</span><span class="sxs-lookup"><span data-stu-id="3ea90-138">The second mechanism to achieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in the target Table.</span></span> <span data-ttu-id="3ea90-139">Esta columna debe usarla Factoría de datos de Azure para asegurarse de que el origen y el destino estén sincronizados.</span><span class="sxs-lookup"><span data-stu-id="3ea90-139">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="3ea90-140">Este enfoque funciona cuando hay flexibilidad para cambiar o definir el esquema de la tabla SQL de destino.</span><span class="sxs-lookup"><span data-stu-id="3ea90-140">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span></span> 

<span data-ttu-id="3ea90-141">Azure Data Factory usa esta columna con fines de repetibilidad y, en el proceso, Azure Data Factory no realiza ningún cambio de esquema en la tabla.</span><span class="sxs-lookup"><span data-stu-id="3ea90-141">This column is used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory does not make any schema changes to the Table.</span></span> <span data-ttu-id="3ea90-142">Forma de usar este enfoque:</span><span class="sxs-lookup"><span data-stu-id="3ea90-142">Way to use this approach:</span></span>

1. <span data-ttu-id="3ea90-143">Defina una columna de tipo **binario (32)** en la tabla DE SQL de destino.</span><span class="sxs-lookup"><span data-stu-id="3ea90-143">Define a column of type **binary (32)** in the destination SQL Table.</span></span> <span data-ttu-id="3ea90-144">No debería haber ninguna restricción en esta columna.</span><span class="sxs-lookup"><span data-stu-id="3ea90-144">There should be no constraints on this column.</span></span> <span data-ttu-id="3ea90-145">En este ejemplo, llamaremos a esta columna AdfSliceIdentifier.</span><span class="sxs-lookup"><span data-stu-id="3ea90-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="3ea90-146">Tabla de origen:</span><span class="sxs-lookup"><span data-stu-id="3ea90-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="3ea90-147">Tabla de destino:</span><span class="sxs-lookup"><span data-stu-id="3ea90-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="3ea90-148">Úselo en la actividad de copia de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="3ea90-148">Use it in the copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="3ea90-149">Azure Data Factory rellena esta columna según sus necesidades para asegurarse de que el origen y el destino permanecen sincronizados.</span><span class="sxs-lookup"><span data-stu-id="3ea90-149">Azure Data Factory populates this column as per its need to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="3ea90-150">Los valores de esta columna no deben usarse fuera de este contexto.</span><span class="sxs-lookup"><span data-stu-id="3ea90-150">The values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="3ea90-151">Similar al mecanismo de 1, la actividad de copia limpia automáticamente los datos del segmento especificado de la tabla de SQL de destino.</span><span class="sxs-lookup"><span data-stu-id="3ea90-151">Similar to mechanism 1, Copy Activity automatically cleans up the data for the given slice from the destination SQL Table.</span></span> <span data-ttu-id="3ea90-152">Luego, inserta datos del origen en la tabla de destino.</span><span class="sxs-lookup"><span data-stu-id="3ea90-152">It then inserts data from source in to the destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3ea90-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3ea90-153">Next steps</span></span>
<span data-ttu-id="3ea90-154">Revise los siguientes artículos de conectores para ver ejemplos completos de JSON:</span><span class="sxs-lookup"><span data-stu-id="3ea90-154">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="3ea90-155">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="3ea90-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="3ea90-156">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3ea90-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="3ea90-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="3ea90-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)