## <span data-ttu-id="ee70e-101"><a name="create-client"></a>Creación de conexiones de cliente</span><span class="sxs-lookup"><span data-stu-id="ee70e-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="ee70e-102">Cree una conexión de cliente mediante la generación de un objeto `WindowsAzure.MobileServiceClient` .</span><span class="sxs-lookup"><span data-stu-id="ee70e-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="ee70e-103">Sustituya `appUrl` por la dirección URL de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="ee70e-103">Replace `appUrl` with the URL to your Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="ee70e-104"><a name="table-reference"></a>Trabajo con tablas</span><span class="sxs-lookup"><span data-stu-id="ee70e-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="ee70e-105">Para acceder a los datos o actualizarlos, cree una referencia a la tabla de back-end.</span><span class="sxs-lookup"><span data-stu-id="ee70e-105">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="ee70e-106">Reemplace `tableName` por el nombre de la tabla.</span><span class="sxs-lookup"><span data-stu-id="ee70e-106">Replace `tableName` with the name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="ee70e-107">Una vez que disponga de una referencia de tabla, podrá realizar más operaciones con su tabla:</span><span class="sxs-lookup"><span data-stu-id="ee70e-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="ee70e-108">Consulta de tablas</span><span class="sxs-lookup"><span data-stu-id="ee70e-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="ee70e-109">Filtrado de datos</span><span class="sxs-lookup"><span data-stu-id="ee70e-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="ee70e-110">Paginación mediante datos</span><span class="sxs-lookup"><span data-stu-id="ee70e-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="ee70e-111">Ordenación de datos</span><span class="sxs-lookup"><span data-stu-id="ee70e-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="ee70e-112">Inserción de datos</span><span class="sxs-lookup"><span data-stu-id="ee70e-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="ee70e-113">Modificación de datos</span><span class="sxs-lookup"><span data-stu-id="ee70e-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="ee70e-114">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="ee70e-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="ee70e-115"><a name="querying"></a>Consulta de una referencia de tabla</span><span class="sxs-lookup"><span data-stu-id="ee70e-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="ee70e-116">Una vez que tiene una referencia de tabla, puede utilizarla para consultar datos en el servidor.</span><span class="sxs-lookup"><span data-stu-id="ee70e-116">Once you have a table reference, you can use it to query for data on the server.</span></span>  <span data-ttu-id="ee70e-117">Las consultas se realizan en un lenguaje "similar a LINQ".</span><span class="sxs-lookup"><span data-stu-id="ee70e-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="ee70e-118">Para devolver todos los datos de la tabla, utilice el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="ee70e-118">To return all data from the table, use the following code:</span></span>

```
/**
 * Process the results that are received by a call to table.read()
 *
 * @param {Object} results the results as a pseudo-array
 * @param {int} results.length the length of the results array
 * @param {Object} results[] the individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - the properties are the columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

<span data-ttu-id="ee70e-119">Se llama a la función success con los resultados.</span><span class="sxs-lookup"><span data-stu-id="ee70e-119">The success function is called with the results.</span></span>  <span data-ttu-id="ee70e-120">No use `for (var i in results)` en la función success, dado que se efectuaría una iteración en la información incluida en los resultados al utilizar otras funciones de consulta (como `.includeTotalCount()`).</span><span class="sxs-lookup"><span data-stu-id="ee70e-120">Do not use `for (var i in results)` in the success function as that will iterate over information that is included in the results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="ee70e-121">Para más información sobre la sintaxis de Query, consulte la [documentación del objeto Query].</span><span class="sxs-lookup"><span data-stu-id="ee70e-121">For more information on the Query syntax, see the [Query object documentation].</span></span>

#### <span data-ttu-id="ee70e-122"><a name="table-filter"></a>Filtrado de datos en el servidor</span><span class="sxs-lookup"><span data-stu-id="ee70e-122"><a name="table-filter"></a>Filtering data on the server</span></span>
<span data-ttu-id="ee70e-123">Puede usar una cláusula `where` en la referencia de tabla:</span><span class="sxs-lookup"><span data-stu-id="ee70e-123">You can use a `where` clause on the table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="ee70e-124">También puede utilizar una función que filtre el objeto.</span><span class="sxs-lookup"><span data-stu-id="ee70e-124">You can also use a function that filters the object.</span></span>  <span data-ttu-id="ee70e-125">En este caso, la variable `this` se asigna al objeto actual que se está filtrando.</span><span class="sxs-lookup"><span data-stu-id="ee70e-125">In this case, the `this` variable is assigned to the current object being filtered.</span></span>  <span data-ttu-id="ee70e-126">El siguiente código es funcionalmente equivalente al ejemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="ee70e-126">The following code is functionally equivalent to the prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="ee70e-127"><a name="table-paging"></a>Paginación mediante datos</span><span class="sxs-lookup"><span data-stu-id="ee70e-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="ee70e-128">Utilice los métodos `take()` y `skip()`.</span><span class="sxs-lookup"><span data-stu-id="ee70e-128">Utilize the `take()` and `skip()` methods.</span></span>  <span data-ttu-id="ee70e-129">Por ejemplo, si desea dividir la tabla en registros de 100 filas:</span><span class="sxs-lookup"><span data-stu-id="ee70e-129">For example, if you wish to split the table into 100-row records:</span></span>

```
var totalCount = 0, pages = 0;

// Step 1 - get the total number of records
table.includeTotalCount().take(0).read(function (results) {
    totalCount = results.totalCount;
    pages = Math.floor(totalCount/100) + 1;
    loadPage(0);
}, failure);

function loadPage(pageNum) {
    let skip = pageNum * 100;
    table.skip(skip).take(100).read(function (results) {
        for (var i = 0 ; i < results.length ; i++) {
            var row = results[i];
            // Process each row
        }
    }
}
```

<span data-ttu-id="ee70e-130">El método `.includeTotalCount()` se utiliza para agregar un campo totalCount al objeto de resultados.</span><span class="sxs-lookup"><span data-stu-id="ee70e-130">The `.includeTotalCount()` method is used to add a totalCount field to the results object.</span></span>  <span data-ttu-id="ee70e-131">El campo totalCount se rellena con el número total de registros que se devolverían si no se utilizara ninguna paginación.</span><span class="sxs-lookup"><span data-stu-id="ee70e-131">The totalCount field is filled with the total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="ee70e-132">A continuación, puede usar la variable de páginas y algunos botones de la interfaz de usuario para proporcionar una lista de páginas; utilice `loadPage()` para cargar los nuevos registros de cada página.</span><span class="sxs-lookup"><span data-stu-id="ee70e-132">You can then use the pages variable and some UI buttons to provide a page list; use `loadPage()` to load the new records for each page.</span></span>  <span data-ttu-id="ee70e-133">Implemente el almacenamiento en caché para acelerar el acceso a los registros que ya se han cargado.</span><span class="sxs-lookup"><span data-stu-id="ee70e-133">Implement caching to speed access to records that have already been loaded.</span></span>

#### <span data-ttu-id="ee70e-134"><a name="sorting-data"></a>Devolución de los datos ordenados</span><span class="sxs-lookup"><span data-stu-id="ee70e-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="ee70e-135">Utilice los métodos de consulta `.orderBy()` o `.orderByDescending()`:</span><span class="sxs-lookup"><span data-stu-id="ee70e-135">Use the `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="ee70e-136">Para más información sobre el objeto Query, consulte la [documentación del objeto Query].</span><span class="sxs-lookup"><span data-stu-id="ee70e-136">For more information on the Query object, see the [Query object documentation].</span></span>

### <span data-ttu-id="ee70e-137"><a name="inserting"></a>Inserción de datos</span><span class="sxs-lookup"><span data-stu-id="ee70e-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="ee70e-138">Cree un objeto de JavaScript con la fecha adecuada y llame a `table.insert()` de manera asincrónica:</span><span class="sxs-lookup"><span data-stu-id="ee70e-138">Create a JavaScript object with the appropriate date and call `table.insert()` asynchronously:</span></span>

```javascript
var newItem = {
    name: 'My Name',
    signupDate: new Date()
};

table
    .insert(newItem)
    .done(function (insertedItem) {
        var id = insertedItem.id;
    }, failure);
```

<span data-ttu-id="ee70e-139">Tras la inserción correcta, el elemento insertado se devuelve con los campos adicionales que son necesarios para las operaciones de sincronización.</span><span class="sxs-lookup"><span data-stu-id="ee70e-139">On successful insertion, the inserted item is returned with the additional fields that are required for sync operations.</span></span>  <span data-ttu-id="ee70e-140">Actualice su propia caché con esta información para actualizaciones posteriores.</span><span class="sxs-lookup"><span data-stu-id="ee70e-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="ee70e-141">El SDK del servidor de Node.js para Azure Mobile Apps admite el esquema dinámico con fines de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="ee70e-141">The Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="ee70e-142">El esquema dinámico permite agregar columnas a la tabla al especificarlas en una operación de inserción o actualización.</span><span class="sxs-lookup"><span data-stu-id="ee70e-142">Dynamic Schema allows you to add columns to the table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="ee70e-143">Se recomienda desactivar el esquema dinámico antes de pasar la aplicación a producción.</span><span class="sxs-lookup"><span data-stu-id="ee70e-143">We recommend that you turn off dynamic schema before moving your application to production.</span></span>

### <span data-ttu-id="ee70e-144"><a name="modifying"></a>Modificación de datos</span><span class="sxs-lookup"><span data-stu-id="ee70e-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="ee70e-145">De forma similar al método `.insert()`, debe crear un objeto Update y luego llamar a `.update()`.</span><span class="sxs-lookup"><span data-stu-id="ee70e-145">Similar to the `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="ee70e-146">El objeto Update debe contener el identificador del registro que se va a actualizar, que se obtiene al leer el registro o al llamar a `.insert()`.</span><span class="sxs-lookup"><span data-stu-id="ee70e-146">The update object must contain the ID of the record to be updated - the ID is obtained when reading the record or when calling `.insert()`.</span></span>

```javascript
var updateItem = {
    id: '7163bc7a-70b2-4dde-98e9-8818969611bd',
    name: 'My New Name'
};

table
    .update(updateItem)
    .done(function (updatedItem) {
        // You can now update your cached copy
    }, failure);
```

### <span data-ttu-id="ee70e-147"><a name="deleting"></a>Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="ee70e-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="ee70e-148">Para eliminar un registro, llame al método `.del()`.</span><span class="sxs-lookup"><span data-stu-id="ee70e-148">To delete a record, call the `.del()` method.</span></span>  <span data-ttu-id="ee70e-149">Pase el identificador de una referencia de objeto:</span><span class="sxs-lookup"><span data-stu-id="ee70e-149">Pass the ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
