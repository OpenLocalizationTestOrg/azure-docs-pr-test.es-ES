---
title: "copia de aaaRepeatable de factoría de datos de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooavoid duplicados aunque un segmento que copia los datos se ejecute más de una vez."
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
ms.openlocfilehash: 79a3fde2b700bf0a0e167479d6a86c5bee1bf7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="75cd6-103">Copia repetible en Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="75cd6-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="75cd6-104">Lectura repetible de orígenes relacionales</span><span class="sxs-lookup"><span data-stu-id="75cd6-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="75cd6-105">Al copiar datos de almacenes de datos relacionales, tenga repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="75cd6-105">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="75cd6-106">En Azure Data Factory, puede volver a ejecutar un segmento manualmente.</span><span class="sxs-lookup"><span data-stu-id="75cd6-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="75cd6-107">También puede configurar la directiva de reintentos para un conjunto de datos con el fin de que un segmento se vuelva a ejecutar cuando se produce un error.</span><span class="sxs-lookup"><span data-stu-id="75cd6-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="75cd6-108">Cuando se vuelve a ejecutar un segmento de cualquier manera, debe toomake seguro de que Hola los mismos datos no se lee importa cómo se ejecuta muchas veces un segmento.</span><span class="sxs-lookup"><span data-stu-id="75cd6-108">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="75cd6-109">Hello en los ejemplos siguientes son para SQL Azure pero tooany aplicables almacén de datos que admite conjuntos de datos rectangular.</span><span class="sxs-lookup"><span data-stu-id="75cd6-109">hello following samples are for Azure SQL but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="75cd6-110">Es posible que tenga hello tooadjust **tipo** de hello y origen **consulta** propiedad (por ejemplo: consulta en lugar de sqlReaderQuery) para los datos de hello almacenar.</span><span class="sxs-lookup"><span data-stu-id="75cd6-110">You may have tooadjust hello **type** of source and hello **query** property (for example: query instead of sqlReaderQuery) for hello data store.</span></span>   

<span data-ttu-id="75cd6-111">Por lo general, al leer de almacenes relacionales, desea solo datos de hello tooread correspondiente toothat segmento.</span><span class="sxs-lookup"><span data-stu-id="75cd6-111">Usually, when reading from relational stores, you want tooread only hello data corresponding toothat slice.</span></span> <span data-ttu-id="75cd6-112">Un toodo de manera por lo que sería mediante el uso de hello WindowStart y WindowEnd variables del sistema disponibles en Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="75cd6-112">A way toodo so would be by using hello WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="75cd6-113">Leer sobre las variables de Hola y funciones de factoría de datos de Azure aquí en hello [factoría de datos de Azure: funciones y Variables del sistema](data-factory-functions-variables.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="75cd6-113">Read about hello variables and functions in Azure Data Factory here in hello [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="75cd6-114">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="75cd6-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="75cd6-115">Esta consulta lee los datos que se encuentra en el intervalo de duración del segmento hello (WindowStart -> WindowEnd) de la tabla MyTable de Hola.</span><span class="sxs-lookup"><span data-stu-id="75cd6-115">This query reads data that falls in hello slice duration range (WindowStart -> WindowEnd) from hello table MyTable.</span></span> <span data-ttu-id="75cd6-116">Vuelva a ejecutar de este segmento aseguraría también siempre que Hola se leen los mismos datos.</span><span class="sxs-lookup"><span data-stu-id="75cd6-116">Rerun of this slice would also always ensure that hello same data is read.</span></span> 

<span data-ttu-id="75cd6-117">En otros casos, puede que quieran tooread Hola toda la tabla y puede definir hello sqlReaderQuery como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="75cd6-117">In other cases, you may wish tooread hello entire table and may define hello sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a><span data-ttu-id="75cd6-118">Escritura repetible tooSqlSink</span><span class="sxs-lookup"><span data-stu-id="75cd6-118">Repeatable write tooSqlSink</span></span>
<span data-ttu-id="75cd6-119">Cuando se copian datos demasiado**Azure SQL o SQL Server** desde otros almacenes de datos, necesita tookeep repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="75cd6-119">When copying data too**Azure SQL/SQL Server** from other data stores, you need tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="75cd6-120">Cuando se copian datos tooAzure base de datos SQL o SQL Server, actividad de copia de hello anexa la tabla de datos toohello receptor de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="75cd6-120">When copying data tooAzure SQL/SQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="75cd6-121">Supongamos, se copian datos desde un CSV (valores separados por comas) archivo que contiene dos registros toohello en una base de datos de Azure SQL o SQL Server en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="75cd6-121">Say, you are copying data from a CSV (comma-separated values) file containing two records toohello following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="75cd6-122">Cuando se ejecuta un segmento, Hola dos registros son copiados toohello table de SQL.</span><span class="sxs-lookup"><span data-stu-id="75cd6-122">When a slice runs, hello two records are copied toohello SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="75cd6-123">Suponga que encuentra errores en el archivo de código fuente y actualiza la cantidad de Hola de Tube hacia abajo de too4 2.</span><span class="sxs-lookup"><span data-stu-id="75cd6-123">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4.</span></span> <span data-ttu-id="75cd6-124">Si se vuelve a ejecutar el segmento de datos de Hola durante ese período manualmente, encontrará dos nuevos registros anexan tooAzure base de datos SQL o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="75cd6-124">If you rerun hello data slice for that period manually, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="75cd6-125">En este ejemplo se da por supuesto que ninguna de las columnas de hello en la tabla de hello tiene restricción de clave principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="75cd6-125">This example assumes that none of hello columns in hello table has hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="75cd6-126">tooavoid este comportamiento, necesita una semántica UPSERT toospecify mediante uno de hello siguiendo dos mecanismos:</span><span class="sxs-lookup"><span data-stu-id="75cd6-126">tooavoid this behavior, you need toospecify UPSERT semantics by using one of hello following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="75cd6-127">Mecanismo 1: Uso de sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="75cd6-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="75cd6-128">Puede usar hello **sqlWriterCleanupScript** propiedad tooclean los datos de tabla de receptor de hello antes de insertar datos de hello cuando se ejecuta un segmento.</span><span class="sxs-lookup"><span data-stu-id="75cd6-128">You can use hello **sqlWriterCleanupScript** property tooclean up data from hello sink table before inserting hello data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="75cd6-129">Cuando se ejecuta un segmento, script de limpieza de Hola se ejecuta primero los datos toodelete correspondiente segmento toohello de tabla SQL Hola.</span><span class="sxs-lookup"><span data-stu-id="75cd6-129">When a slice runs, hello cleanup script is run first toodelete data that corresponds toohello slice from hello SQL table.</span></span> <span data-ttu-id="75cd6-130">actividad de copia de Hello, a continuación, inserta datos en hello Table de SQL.</span><span class="sxs-lookup"><span data-stu-id="75cd6-130">hello copy activity then inserts data into hello SQL Table.</span></span> <span data-ttu-id="75cd6-131">Si se vuelve a ejecutar el segmento de hello, se actualiza la cantidad de hello según lo deseado.</span><span class="sxs-lookup"><span data-stu-id="75cd6-131">If hello slice is rerun, hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="75cd6-132">Imagine Hola registro arandela sin formato se quita de hello original csv.</span><span class="sxs-lookup"><span data-stu-id="75cd6-132">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="75cd6-133">A continuación, volver a ejecutar el segmento de Hola generaría Hola siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="75cd6-133">Then rerunning hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="75cd6-134">actividad de copia de Hello ejecutó Hola limpieza script toodelete Hola datos correspondientes para dicho sector.</span><span class="sxs-lookup"><span data-stu-id="75cd6-134">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="75cd6-135">A continuación, debe leer Hola entrada desde archivo csv de hello (que, a continuación, se incluye un único registro) y se inserta en hello tabla.</span><span class="sxs-lookup"><span data-stu-id="75cd6-135">Then it read hello input from hello csv (which then contained only one record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="75cd6-136">Mecanismo 2: Uso de sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="75cd6-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="75cd6-137">sliceIdentifierColumnName no se admite en este momento para Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="75cd6-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="75cd6-138">repetibilidad de Hello segundo mecanismo tooachieve es tener una columna dedicada (sliceIdentifierColumnName) en el destino de hello tabla.</span><span class="sxs-lookup"><span data-stu-id="75cd6-138">hello second mechanism tooachieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in hello target Table.</span></span> <span data-ttu-id="75cd6-139">Esta columna se usaría por factoría de datos de Azure tooensure Hola origen y destino permanecen sincronizadas.</span><span class="sxs-lookup"><span data-stu-id="75cd6-139">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="75cd6-140">Este enfoque funciona cuando se produce la flexibilidad de cambiar o definir el esquema de tabla SQL de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="75cd6-140">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="75cd6-141">Esta columna se utiliza por factoría de datos de Azure para fines de capacidad de repetición y, en el proceso de hello Data Factory de Azure no cualquier esquema cambia toohello tabla.</span><span class="sxs-lookup"><span data-stu-id="75cd6-141">This column is used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory does not make any schema changes toohello Table.</span></span> <span data-ttu-id="75cd6-142">Forma toouse este enfoque:</span><span class="sxs-lookup"><span data-stu-id="75cd6-142">Way toouse this approach:</span></span>

1. <span data-ttu-id="75cd6-143">Definir una columna de tipo **binario (32)** en el destino de hello Table de SQL.</span><span class="sxs-lookup"><span data-stu-id="75cd6-143">Define a column of type **binary (32)** in hello destination SQL Table.</span></span> <span data-ttu-id="75cd6-144">No debería haber ninguna restricción en esta columna.</span><span class="sxs-lookup"><span data-stu-id="75cd6-144">There should be no constraints on this column.</span></span> <span data-ttu-id="75cd6-145">En este ejemplo, llamaremos a esta columna AdfSliceIdentifier.</span><span class="sxs-lookup"><span data-stu-id="75cd6-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="75cd6-146">Tabla de origen:</span><span class="sxs-lookup"><span data-stu-id="75cd6-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="75cd6-147">Tabla de destino:</span><span class="sxs-lookup"><span data-stu-id="75cd6-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="75cd6-148">Usarlo en la actividad de copia de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="75cd6-148">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="75cd6-149">Factoría de datos de Azure rellena esta columna según su necesidad tooensure Hola origen y destino están sincronizadas.</span><span class="sxs-lookup"><span data-stu-id="75cd6-149">Azure Data Factory populates this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="75cd6-150">valores de Hello de esta columna no deben utilizarse fuera de este contexto.</span><span class="sxs-lookup"><span data-stu-id="75cd6-150">hello values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="75cd6-151">Toomechanism similar 1, actividad de copia limpia automáticamente los datos de Hola para hello proporcionada segmento desde el destino de hello Table de SQL.</span><span class="sxs-lookup"><span data-stu-id="75cd6-151">Similar toomechanism 1, Copy Activity automatically cleans up hello data for hello given slice from hello destination SQL Table.</span></span> <span data-ttu-id="75cd6-152">A continuación, inserta datos de origen en la tabla de destino de toohello.</span><span class="sxs-lookup"><span data-stu-id="75cd6-152">It then inserts data from source in toohello destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="75cd6-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="75cd6-153">Next steps</span></span>
<span data-ttu-id="75cd6-154">Revisar los siguientes artículos de conector que para JSON ejemplos completos de Hola:</span><span class="sxs-lookup"><span data-stu-id="75cd6-154">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="75cd6-155">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="75cd6-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="75cd6-156">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="75cd6-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="75cd6-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="75cd6-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)