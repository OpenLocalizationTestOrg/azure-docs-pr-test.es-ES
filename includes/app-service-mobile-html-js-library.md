## <span data-ttu-id="1fbe9-101"><a name="create-client"></a>Creación de conexiones de cliente</span><span class="sxs-lookup"><span data-stu-id="1fbe9-101"><a name="create-client"></a>Create a client connection</span></span>
<span data-ttu-id="1fbe9-102">Cree una conexión de cliente mediante la generación de un objeto `WindowsAzure.MobileServiceClient` .</span><span class="sxs-lookup"><span data-stu-id="1fbe9-102">Create a client connection by creating a `WindowsAzure.MobileServiceClient` object.</span></span>  <span data-ttu-id="1fbe9-103">Reemplace `appUrl` con la aplicación móvil de tooyour de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-103">Replace `appUrl` with the URL tooyour Mobile App.</span></span>

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <span data-ttu-id="1fbe9-104"><a name="table-reference"></a>Trabajo con tablas</span><span class="sxs-lookup"><span data-stu-id="1fbe9-104"><a name="table-reference"></a>Work with tables</span></span>
<span data-ttu-id="1fbe9-105">tooaccess o actualizar los datos, cree una tabla de referencia toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-105">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="1fbe9-106">Reemplace `tableName` con nombre hello de la tabla</span><span class="sxs-lookup"><span data-stu-id="1fbe9-106">Replace `tableName` with hello name of your table</span></span>

```
var table = client.getTable(tableName);
```

<span data-ttu-id="1fbe9-107">Una vez que disponga de una referencia de tabla, podrá realizar más operaciones con su tabla:</span><span class="sxs-lookup"><span data-stu-id="1fbe9-107">Once you have a table reference, you can work further with your table:</span></span>

* [<span data-ttu-id="1fbe9-108">Consulta de tablas</span><span class="sxs-lookup"><span data-stu-id="1fbe9-108">Query a Table</span></span>](#querying)
  * [<span data-ttu-id="1fbe9-109">Filtrado de datos</span><span class="sxs-lookup"><span data-stu-id="1fbe9-109">Filtering Data</span></span>](#table-filter)
  * [<span data-ttu-id="1fbe9-110">Paginación mediante datos</span><span class="sxs-lookup"><span data-stu-id="1fbe9-110">Paging through Data</span></span>](#table-paging)
  * [<span data-ttu-id="1fbe9-111">Ordenación de datos</span><span class="sxs-lookup"><span data-stu-id="1fbe9-111">Sorting Data</span></span>](#sorting-data)
* [<span data-ttu-id="1fbe9-112">Inserción de datos</span><span class="sxs-lookup"><span data-stu-id="1fbe9-112">Inserting Data</span></span>](#inserting)
* [<span data-ttu-id="1fbe9-113">Modificación de datos</span><span class="sxs-lookup"><span data-stu-id="1fbe9-113">Modifying Data</span></span>](#modifying)
* [<span data-ttu-id="1fbe9-114">Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="1fbe9-114">Deleting Data</span></span>](#deleting)

### <span data-ttu-id="1fbe9-115"><a name="querying"></a>Consulta de una referencia de tabla</span><span class="sxs-lookup"><span data-stu-id="1fbe9-115"><a name="querying"></a>How to: Query a table reference</span></span>
<span data-ttu-id="1fbe9-116">Una vez que tenga una referencia de tabla, puede usarlo tooquery para los datos en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-116">Once you have a table reference, you can use it tooquery for data on hello server.</span></span>  <span data-ttu-id="1fbe9-117">Las consultas se realizan en un lenguaje "similar a LINQ".</span><span class="sxs-lookup"><span data-stu-id="1fbe9-117">Queries are made in a "LINQ-like" language.</span></span>
<span data-ttu-id="1fbe9-118">código de todos los datos de tabla de hello, Hola de uso después de tooreturn:</span><span class="sxs-lookup"><span data-stu-id="1fbe9-118">tooreturn all data from hello table, use hello following code:</span></span>

```
/**
 * Process hello results that are received by a call tootable.read()
 *
 * @param {Object} results hello results as a pseudo-array
 * @param {int} results.length hello length of hello results array
 * @param {Object} results[] hello individual results
 */
function success(results) {
   var numItemsRead = results.length;

   for (var i = 0 ; i < results.length ; i++) {
       var row = results[i];
       // Each row is an object - hello properties are hello columns
   }
}

function failure(error) {
    throw new Error('Error loading data: ', error);
}

table
    .read()
    .then(success, failure);
```

<span data-ttu-id="1fbe9-119">se llama la función de éxito de Hello con resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-119">hello success function is called with hello results.</span></span>  <span data-ttu-id="1fbe9-120">No utilice `for (var i in results)` de éxito de hello funciona de la manera que creará una iteración sobre la información que se incluye en los resultados de hello cuando otras funciones de consulta (como `.includeTotalCount()`) se usan.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-120">Do not use `for (var i in results)` in hello success function as that will iterate over information that is included in hello results when other query functions (such as `.includeTotalCount()`) are used.</span></span>

<span data-ttu-id="1fbe9-121">Para obtener más información sobre la sintaxis de consulta de Hola, vea Hola [consultar la documentación del objeto].</span><span class="sxs-lookup"><span data-stu-id="1fbe9-121">For more information on hello Query syntax, see hello [Query object documentation].</span></span>

#### <span data-ttu-id="1fbe9-122"><a name="table-filter"></a>Filtrar datos en el servidor de Hola</span><span class="sxs-lookup"><span data-stu-id="1fbe9-122"><a name="table-filter"></a>Filtering data on hello server</span></span>
<span data-ttu-id="1fbe9-123">Puede usar un `where` cláusula en referencia a la tabla hello:</span><span class="sxs-lookup"><span data-stu-id="1fbe9-123">You can use a `where` clause on hello table reference:</span></span>

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

<span data-ttu-id="1fbe9-124">También puede usar una función que filtra los objetos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-124">You can also use a function that filters hello object.</span></span>  <span data-ttu-id="1fbe9-125">En este caso, Hola `this` variable se asigna toothe objeto actual que se está filtrando.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-125">In this case, hello `this` variable is assigned toothe current object being filtered.</span></span>  <span data-ttu-id="1fbe9-126">Hola siguiente código es funcionalmente equivalente toohello anterior ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1fbe9-126">hello following code is functionally equivalent toohello prior example:</span></span>

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <span data-ttu-id="1fbe9-127"><a name="table-paging"></a>Paginación mediante datos</span><span class="sxs-lookup"><span data-stu-id="1fbe9-127"><a name="table-paging"></a>Paging through data</span></span>
<span data-ttu-id="1fbe9-128">Utilizar hello `take()` y `skip()` métodos.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-128">Utilize hello `take()` and `skip()` methods.</span></span>  <span data-ttu-id="1fbe9-129">Por ejemplo, si desea toosplit tabla de hello en registros de 100 filas:</span><span class="sxs-lookup"><span data-stu-id="1fbe9-129">For example, if you wish toosplit hello table into 100-row records:</span></span>

```
var totalCount = 0, pages = 0;

// Step 1 - get hello total number of records
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

<span data-ttu-id="1fbe9-130">Hola `.includeTotalCount()` método es tooadd usa un objeto de resultados totalCount toohello de campo.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-130">hello `.includeTotalCount()` method is used tooadd a totalCount field toohello results object.</span></span>  <span data-ttu-id="1fbe9-131">El campo totalCount se rellena con el número total de Hola de registros que se devolverían si no se usa ninguna paginación.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-131">The totalCount field is filled with hello total number of records that would be returned if no paging is used.</span></span>

<span data-ttu-id="1fbe9-132">A continuación, puede usar variable de páginas de Hola y algunos tooprovide de botones de la interfaz de usuario una lista de páginas; usar `loadPage()` para cargar nuevos registros de Hola para cada página.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-132">You can then use hello pages variable and some UI buttons tooprovide a page list; use `loadPage()` to load hello new records for each page.</span></span>  <span data-ttu-id="1fbe9-133">Implementar el almacenamiento en caché toorecords de acceso toospeed que ya se han cargado.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-133">Implement caching toospeed access toorecords that have already been loaded.</span></span>

#### <span data-ttu-id="1fbe9-134"><a name="sorting-data"></a>Devolución de los datos ordenados</span><span class="sxs-lookup"><span data-stu-id="1fbe9-134"><a name="sorting-data"></a>How to: Return sorted data</span></span>
<span data-ttu-id="1fbe9-135">Hola de uso `.orderBy()` o `.orderByDescending()` métodos de consulta:</span><span class="sxs-lookup"><span data-stu-id="1fbe9-135">Use hello `.orderBy()` or `.orderByDescending()` query methods:</span></span>

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

<span data-ttu-id="1fbe9-136">Para obtener más información sobre el objeto de consulta de hello, vea Hola [consultar la documentación del objeto].</span><span class="sxs-lookup"><span data-stu-id="1fbe9-136">For more information on hello Query object, see hello [Query object documentation].</span></span>

### <span data-ttu-id="1fbe9-137"><a name="inserting"></a>Inserción de datos</span><span class="sxs-lookup"><span data-stu-id="1fbe9-137"><a name="inserting"></a>How to: Insert data</span></span>
<span data-ttu-id="1fbe9-138">Crear un objeto de JavaScript con fecha apropiada de Hola y llame al método `table.insert()` asincrónica:</span><span class="sxs-lookup"><span data-stu-id="1fbe9-138">Create a JavaScript object with hello appropriate date and call `table.insert()` asynchronously:</span></span>

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

<span data-ttu-id="1fbe9-139">Al insertar correctamente, se devuelve el elemento de hello inserta con campos adicionales de Hola que son necesarios para las operaciones de sincronización.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-139">On successful insertion, hello inserted item is returned with hello additional fields that are required for sync operations.</span></span>  <span data-ttu-id="1fbe9-140">Actualice su propia caché con esta información para actualizaciones posteriores.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-140">Update your own cache with this information for later updates.</span></span>

<span data-ttu-id="1fbe9-141">Hola Node.js servidor SDK de Azure Mobile Apps es compatible con el esquema dinámico para fines de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-141">hello Azure Mobile Apps Node.js Server SDK supports dynamic schema for development purposes.</span></span>  <span data-ttu-id="1fbe9-142">Esquema dinámico permite tabla toohello de tooadd columnas especificándolas en una operación insert o update.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-142">Dynamic Schema allows you tooadd columns toohello table by specifying them in an insert or update operation.</span></span>  <span data-ttu-id="1fbe9-143">Se recomienda desactivar esquema dinámico antes de mover el tooproduction de aplicación.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-143">We recommend that you turn off dynamic schema before moving your application tooproduction.</span></span>

### <span data-ttu-id="1fbe9-144"><a name="modifying"></a>Modificación de datos</span><span class="sxs-lookup"><span data-stu-id="1fbe9-144"><a name="modifying"></a>How to: Modify data</span></span>
<span data-ttu-id="1fbe9-145">Toohello similar `.insert()` método, debe crear un objeto de actualización y, a continuación, llamar a `.update()`.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-145">Similar toohello `.insert()` method, you should create an Update object and then call `.update()`.</span></span>  <span data-ttu-id="1fbe9-146">Hello update del objeto debe contener identificador hello de hello toobe registro actualizado: Id. de Hola se obtiene al leer el registro de Hola o al llamar a `.insert()`.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-146">hello update object must contain hello ID of hello record toobe updated - hello ID is obtained when reading hello record or when calling `.insert()`.</span></span>

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

### <span data-ttu-id="1fbe9-147"><a name="deleting"></a>Eliminación de datos</span><span class="sxs-lookup"><span data-stu-id="1fbe9-147"><a name="deleting"></a>How to: Delete data</span></span>
<span data-ttu-id="1fbe9-148">toodelete un registro, llamada hello `.del()` método.</span><span class="sxs-lookup"><span data-stu-id="1fbe9-148">toodelete a record, call hello `.del()` method.</span></span>  <span data-ttu-id="1fbe9-149">Pase el identificador hello en una referencia de objeto:</span><span class="sxs-lookup"><span data-stu-id="1fbe9-149">Pass hello ID in an object reference:</span></span>

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
