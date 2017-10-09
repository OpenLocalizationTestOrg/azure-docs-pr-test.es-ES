## <a name="repeatability-during-copy"></a><span data-ttu-id="3a1b9-101">Repetibilidad durante la copia</span><span class="sxs-lookup"><span data-stu-id="3a1b9-101">Repeatability during Copy</span></span>
<span data-ttu-id="3a1b9-102">Cuando copia tooAzure de datos SQL o SQL Server de otros datos almacena una necesidades tookeep repetibilidad en mente tooavoid resultados imprevistos.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-102">When copying data tooAzure SQL/SQL Server from other data stores one needs tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="3a1b9-103">Al copiar datos tooAzure base de datos SQL o SQL Server, actividad de copia aparecerá por tabla del conjunto de datos toohello receptor de predeterminado ANEXAR Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-103">When copying data tooAzure SQL/SQL Server Database, copy activity will by default APPEND hello data set toohello sink table by default.</span></span> <span data-ttu-id="3a1b9-104">Por ejemplo, al copiar datos de un origen de archivo CSV (datos de valores separados por comas) que contiene dos registros tooAzure base de datos SQL o SQL Server, esto es qué tabla Hola aspecto:</span><span class="sxs-lookup"><span data-stu-id="3a1b9-104">For example, when copying data from a CSV (comma separated values data) file source containing two records tooAzure SQL/SQL Server Database, this is what hello table looks like:</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="3a1b9-105">Suponga que encontró errores en el archivo de código fuente y la cantidad de Hola actualizada de Tube hacia abajo desde too4 2 en el archivo de código fuente de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-105">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4 in hello source file.</span></span> <span data-ttu-id="3a1b9-106">Si vuelve a ejecutar el segmento de datos de Hola durante ese período, encontrará dos nuevos registros anexan tooAzure base de datos SQL o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-106">If you re-run hello data slice for that period, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="3a1b9-107">Hola siguiente se da por supuesto que ninguna de las columnas de hello en la tabla de Hola tiene restricción de clave principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-107">hello below assumes none of hello columns in hello table have hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="3a1b9-108">tooavoid esto, necesitará una semántica UPSERT toospecify mediante el aprovechamiento de uno de Hola por debajo de 2 mecanismos indicadas a continuación.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-108">tooavoid this, you will need toospecify UPSERT semantics by leveraging one of hello below 2 mechanisms stated below.</span></span>

> [!NOTE]
> <span data-ttu-id="3a1b9-109">Un segmento se puede volver a ejecutar automáticamente en Data Factory de Azure según la directiva de reintento de hello especificada.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-109">A slice can be re-run automatically in Azure Data Factory as per hello retry policy specified.</span></span>
> 
> 

### <a name="mechanism-1"></a><span data-ttu-id="3a1b9-110">Mecanismo 1</span><span class="sxs-lookup"><span data-stu-id="3a1b9-110">Mechanism 1</span></span>
<span data-ttu-id="3a1b9-111">Puede aprovechar **sqlWriterCleanupScript** toofirst propiedad realizar la acción de limpieza cuando se ejecuta un segmento.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-111">You can leverage **sqlWriterCleanupScript** property toofirst perform cleanup action when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="3a1b9-112">Hello script de limpieza se ejecutaría primera durante la copia de un sector determinado que podría eliminar datos de Hola de segmento de toothat Hola tabla SQL correspondiente.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-112">hello cleanup script would be executed first during copy for a given slice which would delete hello data from hello SQL Table corresponding toothat slice.</span></span> <span data-ttu-id="3a1b9-113">actividad Hello posteriormente insertará los datos de hello en hello Table de SQL.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-113">hello activity will subsequently insert hello data into hello SQL Table.</span></span> 

<span data-ttu-id="3a1b9-114">Si el segmento de hello es ahora vuelva a ejecutar; a continuación, encontrará Hola cantidad se actualiza como se desea.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-114">If hello slice is now re-run, then you will find hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="3a1b9-115">Imagine Hola registro arandela sin formato se quita de hello original csv.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-115">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="3a1b9-116">A continuación, volver a ejecutar segmento Hola generaría Hola siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="3a1b9-116">Then re-running hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
<span data-ttu-id="3a1b9-117">Nada nuevo tenía toobe realiza.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-117">Nothing new had toobe done.</span></span> <span data-ttu-id="3a1b9-118">actividad de copia de Hello ejecutó Hola limpieza script toodelete Hola datos correspondientes para dicho sector.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-118">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="3a1b9-119">A continuación, debe leer Hola entrada desde archivo csv de hello (que, a continuación, incluidos 1 sólo registro) y se inserta en hello tabla.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-119">Then it read hello input from hello csv (which then contained only 1 record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2"></a><span data-ttu-id="3a1b9-120">Mecanismo 2</span><span class="sxs-lookup"><span data-stu-id="3a1b9-120">Mechanism 2</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3a1b9-121">sliceIdentifierColumnName no se admite en este momento para Almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span></span> 

<span data-ttu-id="3a1b9-122">Capacidad de repetición de otro mecanismo tooachieve es tener una columna dedicada (**sliceIdentifierColumnName**) en hello la tabla de destino.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-122">Another mechanism tooachieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in hello target Table.</span></span> <span data-ttu-id="3a1b9-123">Esta columna se usaría por factoría de datos de Azure tooensure Hola origen y destino permanecen sincronizadas.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-123">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="3a1b9-124">Este enfoque funciona cuando se produce la flexibilidad de cambiar o definir el esquema de tabla SQL de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-124">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="3a1b9-125">Esta columna se usaría por factoría de datos de Azure para fines de capacidad de repetición y en proceso de hello Data Factory de Azure no realizará ningún esquema cambia toohello tabla.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-125">This column would be used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory will not make any schema changes toohello Table.</span></span> <span data-ttu-id="3a1b9-126">Forma toouse este enfoque:</span><span class="sxs-lookup"><span data-stu-id="3a1b9-126">Way toouse this approach:</span></span>

1. <span data-ttu-id="3a1b9-127">Definir una columna de tipo binary (32) en el destino de hello Table de SQL.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-127">Define a column of type binary (32) in hello destination SQL Table.</span></span> <span data-ttu-id="3a1b9-128">No debería haber ninguna restricción en esta columna.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-128">There should be no constraints on this column.</span></span> <span data-ttu-id="3a1b9-129">Llamemos a esta columna 'ColumnForADFuseOnly' para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span></span>
2. <span data-ttu-id="3a1b9-130">Usarlo en la actividad de copia de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="3a1b9-130">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

<span data-ttu-id="3a1b9-131">Factoría de datos de Azure se llenará esta columna según su necesidad tooensure Hola origen y destino están sincronizadas.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-131">Azure Data Factory will populate this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="3a1b9-132">valores de Hello de esta columna no deben usarse fuera de este contexto de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-132">hello values of this column should not be used outside of this context by hello user.</span></span> 

<span data-ttu-id="3a1b9-133">Toomechanism similar 1, se de actividad de copia automáticamente primera limpiar los datos de Hola para hello proporcionadas segmento desde el destino de hello Table de SQL y, a continuación, ejecute actividad de copia de hello normalmente datos de hello tooinsert de toodestination de origen para dicho sector.</span><span class="sxs-lookup"><span data-stu-id="3a1b9-133">Similar toomechanism 1, Copy Activity will automatically first clean up hello data for hello given slice from hello destination SQL Table and then run hello copy activity normally tooinsert hello data from source toodestination for that slice.</span></span> 

