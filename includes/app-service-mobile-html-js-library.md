## <a name="create-client"></a>Creación de conexiones de cliente
Cree una conexión de cliente mediante la generación de un objeto `WindowsAzure.MobileServiceClient` .  Reemplace `appUrl` con la aplicación móvil de tooyour de dirección URL.

```
var client = WindowsAzure.MobileServiceClient(appUrl);
```

## <a name="table-reference"></a>Trabajo con tablas
tooaccess o actualizar los datos, cree una tabla de referencia toohello back-end. Reemplace `tableName` con nombre hello de la tabla

```
var table = client.getTable(tableName);
```

Una vez que disponga de una referencia de tabla, podrá realizar más operaciones con su tabla:

* [Consulta de tablas](#querying)
  * [Filtrado de datos](#table-filter)
  * [Paginación mediante datos](#table-paging)
  * [Ordenación de datos](#sorting-data)
* [Inserción de datos](#inserting)
* [Modificación de datos](#modifying)
* [Eliminación de datos](#deleting)

### <a name="querying"></a>Consulta de una referencia de tabla
Una vez que tenga una referencia de tabla, puede usarlo tooquery para los datos en el servidor de Hola.  Las consultas se realizan en un lenguaje "similar a LINQ".
código de todos los datos de tabla de hello, Hola de uso después de tooreturn:

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

se llama la función de éxito de Hello con resultados de Hola.  No utilice `for (var i in results)` de éxito de hello funciona de la manera que creará una iteración sobre la información que se incluye en los resultados de hello cuando otras funciones de consulta (como `.includeTotalCount()`) se usan.

Para obtener más información sobre la sintaxis de consulta de Hola, vea Hola [consultar la documentación del objeto].

#### <a name="table-filter"></a>Filtrar datos en el servidor de Hola
Puede usar un `where` cláusula en referencia a la tabla hello:

```
table
    .where({ userId: user.userId, complete: false })
    .read()
    .then(success, failure);
```

También puede usar una función que filtra los objetos de Hola.  En este caso, Hola `this` variable se asigna toothe objeto actual que se está filtrando.  Hola siguiente código es funcionalmente equivalente toohello anterior ejemplo:

```
function filterByUserId(currentUserId) {
    return this.userId === currentUserId && this.complete === false;
}

table
    .where(filterByUserId, user.userId)
    .read()
    .then(success, failure);
```

#### <a name="table-paging"></a>Paginación mediante datos
Utilizar hello `take()` y `skip()` métodos.  Por ejemplo, si desea toosplit tabla de hello en registros de 100 filas:

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

Hola `.includeTotalCount()` método es tooadd usa un objeto de resultados totalCount toohello de campo.  El campo totalCount se rellena con el número total de Hola de registros que se devolverían si no se usa ninguna paginación.

A continuación, puede usar variable de páginas de Hola y algunos tooprovide de botones de la interfaz de usuario una lista de páginas; usar `loadPage()` para cargar nuevos registros de Hola para cada página.  Implementar el almacenamiento en caché toorecords de acceso toospeed que ya se han cargado.

#### <a name="sorting-data"></a>Devolución de los datos ordenados
Hola de uso `.orderBy()` o `.orderByDescending()` métodos de consulta:

```
table
    .orderBy('name')
    .read()
    .then(success, failure);
```

Para obtener más información sobre el objeto de consulta de hello, vea Hola [consultar la documentación del objeto].

### <a name="inserting"></a>Inserción de datos
Crear un objeto de JavaScript con fecha apropiada de Hola y llame al método `table.insert()` asincrónica:

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

Al insertar correctamente, se devuelve el elemento de hello inserta con campos adicionales de Hola que son necesarios para las operaciones de sincronización.  Actualice su propia caché con esta información para actualizaciones posteriores.

Hola Node.js servidor SDK de Azure Mobile Apps es compatible con el esquema dinámico para fines de desarrollo.  Esquema dinámico permite tabla toohello de tooadd columnas especificándolas en una operación insert o update.  Se recomienda desactivar esquema dinámico antes de mover el tooproduction de aplicación.

### <a name="modifying"></a>Modificación de datos
Toohello similar `.insert()` método, debe crear un objeto de actualización y, a continuación, llamar a `.update()`.  Hello update del objeto debe contener identificador hello de hello toobe registro actualizado: Id. de Hola se obtiene al leer el registro de Hola o al llamar a `.insert()`.

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

### <a name="deleting"></a>Eliminación de datos
toodelete un registro, llamada hello `.del()` método.  Pase el identificador hello en una referencia de objeto:

```
table
    .del({ id: '7163bc7a-70b2-4dde-98e9-8818969611bd' })
    .done(function () {
        // Record is now deleted - update your cache
    }, failure);
```
