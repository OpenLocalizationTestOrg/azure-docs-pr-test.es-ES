---
title: almacenamiento de tablas de Azure de Node.js del aaaHow toouse | Documentos de Microsoft
description: "Almacenar datos estructurados de la nube de hello mediante el almacenamiento de tabla de Azure, un almacén de datos NoSQL."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 990a71337b806d759d0277a7691712346db7b355
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a>¿Cómo toouse almacenamiento de tablas de Azure de Node.js
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Información general
Este tema muestra cómo service tooperform escenarios comunes con hello tabla de Azure en una aplicación Node.js.

ejemplos de código de Hello en este tema se suponen que ya tiene una aplicación Node.js. Para obtener información acerca de cómo toocreate una aplicación Node.js en Azure, vea cualquiera de estos temas:

* [Creación de una aplicación web de Node.js en el Servicio de aplicaciones de Azure](../app-service-web/app-service-web-get-started-nodejs.md)
* [Compilar e implementar un tooAzure de aplicación web de Node.js mediante WebMatrix](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* [Compilar e implementar un tooan de aplicación Node.js servicio de nube de Azure](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (uso de Windows PowerShell)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a>Configurar el almacenamiento de Azure tooaccess de aplicación
toouse almacenamiento de Azure, necesitará Hola SDK de almacenamiento de Azure para Node.js, que incluye un conjunto de bibliotecas de conveniencia que se comunican con servicios REST de almacenamiento de Hola.

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a>Usar el Administrador de paquetes de nodo (NPM) tooinstall Hola paquete
1. Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Unix) y desplazarse por las carpetas de toohello en la que creó la aplicación.
2. Tipo de **npm instalar almacenamiento de azure** en la ventana de comandos de Hola. Salida de comando de hello es similar toohello siguiente ejemplo.

       azure-storage@0.5.0 node_modules\azure-storage
       +-- extend@1.2.1
       +-- xmlbuilder@0.4.3
       +-- mime@1.2.11
       +-- node-uuid@1.4.3
       +-- validator@3.22.2
       +-- underscore@1.4.4
       +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
       +-- xml2js@0.2.7 (sax@0.5.2)
       +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. También puede ejecutar manualmente hello **ls** tooverify de comando que un **nodo\_módulos** se creó la carpeta. Dentro de esa carpeta, encontrará hello **almacenamiento de azure** paquete, que contiene las bibliotecas de Hola que necesita almacenamiento tooaccess.

### <a name="import-hello-package"></a>Importar paquete de Hola
Agregar Hola después de la parte superior de toohello de código de hello **server.js** archivo en la aplicación:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Configuración de una conexión de almacenamiento de Azure
módulo de Hello azure leerá variables de entorno de hello AZURE\_almacenamiento\_cuenta y AZURE\_almacenamiento\_acceso\_clave o AZURE\_almacenamiento\_conexión \_Cadena para la información necesaria tooconnect tooyour cuenta de almacenamiento de Azure. Si no se establecen estas variables de entorno, debe especificar la información de la cuenta de hello al llamar a **TableService**.

Para obtener un ejemplo de establecer las variables de entorno de hello en hello [portal de Azure](https://portal.azure.com) para un sitio Web de Azure, consulte [aplicación web de Node.js con Hola servicio tabla de Azure](../app-service-web/storage-nodejs-use-table-storage-web-site.md).

## <a name="create-a-table"></a>Creación de una tabla
Hello código siguiente se crea un **TableService** objeto y lo usa toocreate una nueva tabla. Agregue Hola siguiente cerca de la parte superior de Hola de **server.js**.

```nodejs
var tableSvc = azure.createTableService();
```

Hola llamada demasiado**createTableIfNotExists** creará una nueva tabla con el nombre especificado de hello si aún no existe. Hello en el ejemplo siguiente se crea una nueva tabla denominada "mytable" Si aún no existe:

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

Hola `result.created` será `true` si se crea una nueva tabla, y `false` si Hola tabla ya existe. Hola `response` contendrá información sobre la solicitud de saludo.

### <a name="filters"></a>Filtros
Las operaciones de filtrado opcionales pueden ser aplicada toooperations realizada con **TableService**. Las operaciones de filtrado pueden incluir registros, reintentos automáticos, etc. Los filtros son objetos que implementan un método con firma de hello:

```nodejs
function handle (requestOptions, next)
```

Después de realizar su procesamiento previo en Opciones de solicitud de hello, método hello necesita toocall "siguiente", pasando una devolución de llamada con hello siguiente firma:

```nodejs
function (returnObject, finalCallback, next)
```

En esta devolución de llamada y, después de procesar hello returnObject (respuesta Hola Hola solicitud enviada toohello al servidor), la devolución de llamada de hello necesita tooeither invocar a continuación si existe toocontinue otros filtros de procesamiento o simplemente invocar finalCallback en caso contrario hello tooend invocación de servicio.

Dos filtros que implementan la lógica de reintento se incluyen con hello Azure SDK para Node.js, **ExponentialRetryPolicyFilter** y **LinearRetryPolicyFilter**. Hola siguiente crea un **TableService** objeto que usa hello **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a>Agregar una tabla de tooa de entidad
tooadd una entidad, primero cree un objeto que define las propiedades de entidad. Todas las entidades deben contener una **PartitionKey** y **RowKey**, que son identificadores únicos de entidad de Hola.

* **PartitionKey** -determina la partición de Hola Hola entidad se almacena en
* **RowKey** : de forma única identifica la entidad de hello en partición de Hola

Tanto **PartitionKey** como **RowKey** tiene que ser valores de cadena. Para obtener más información, consulte [Hola de entender el modelo de datos del servicio de tabla](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Hola aquí te mostramos un ejemplo de definición de una entidad. Tenga en cuenta que **dueDate** se define como un tipo de **Edm.DateTime**. Especificar tipo de hello es opcional y tipos se pueden inferir si no se especifica.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> Hay también un campo **Timestamp** para cada registro; Azure lo establece cuando se inserta o actualiza una entidad.
>
>

También puede usar hello **entityGenerator** toocreate entidades. Hello en el ejemplo siguiente se crea Hola misma entidad tarea utilizando hello **entityGenerator**.

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

tooadd una tabla de tooyour de entidad, pasar toohello de objeto de entidad de hello **insertEntity** método.

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

Si es correcta, la operación de hello `result` contendrá hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) de hello registro insertado y `response` contendrá información sobre la operación de Hola.

Respuesta de ejemplo:

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> De forma predeterminada, **insertEntity** no devuelve entidades Hola insertado como parte del programa Hola `response` información. Si la intención de realizar otras operaciones en esta entidad, o desea obtener información de hello toocache, puede ser útil toohave devuelve como parte del programa Hola a `result`. Para ello, puede habilitar **echoContent** de la manera siguiente:
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a>Actualización de una entidad
Hay varios métodos a disponible tooupdate una entidad existente:

* **replaceEntity** : actualiza una entidad que ya existe reemplazándola.
* **mergeEntity** -actualiza una entidad existente mediante la combinación de nuevos valores de propiedad de entidad existente Hola
* **insertOrReplaceEntity** : actualiza una entidad existente reemplazándola. Si no hay entidades, se insertará una nueva.
* **insertOrMergeEntity** -actualiza una entidad existente mediante la combinación de nuevos valores de propiedad Hola existente. Si no hay entidades, se insertará una nueva.

Hello en el ejemplo siguiente se muestra cómo actualizar una entidad utilizando **replaceEntity**:

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> De forma predeterminada, actualizar una entidad no comprueba toosee si anteriormente se han modificado los datos de Hola que se está actualizados en otro proceso. toosupport actualizaciones simultáneas:
>
> 1. Obtener Hola ETag del objeto de Hola que se está actualizando. Esto se devuelve como parte del programa Hola a `response` para todas las operaciones relacionadas con la entidad y se pueden recuperar mediante `response['.metadata'].etag`.
> 2. Al realizar una operación de actualización en una entidad, agregue información de ETag Hola recuperado previamente toohello nueva entidad. Por ejemplo:
>
>       entity2['.metadata'].etag = currentEtag;
> 3. Realizar la operación de actualización de Hola. Si se ha modificado la entidad de hello puesto que recuperar el valor de ETag de hello, como otra instancia de la aplicación, un `error` se devolverán que indica que no se cumple la condición de actualización de hello especificado en la solicitud de saludo.
>
>

Con **replaceEntity** y **mergeEntity**, si no existe la entidad Hola que se está actualizando, se producirá un error en la operación de actualización de Hola. Por lo tanto, si desea toostore una entidad, independientemente de si ya existe, utilice **insertOrReplaceEntity** o **insertOrMergeEntity**.

Hola `result` para actualización correcta operaciones contendrá hello **Etag** de hello Actualizar entidad.

## <a name="work-with-groups-of-entities"></a>Trabajo con grupos de entidades
A veces tiene sentido toosubmit varias operaciones juntos en un lote tooensure atómica de procesamiento por servidor hello. tooaccomplish que usar hello **TableBatch** clase toocreate un lote y, a continuación, usar hello **executeBatch** método **TableService** operaciones por lotes tooperform Hola.

 Hola de ejemplo siguiente se muestra cómo enviar dos entidades en un lote:

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

Realizó correctamente las operaciones por lotes, `result` contendrá información de cada operación de lote de Hola.

### <a name="work-with-batched-operations"></a>Trabajar con operaciones por lotes
Agregar operaciones por lotes tooa pueden ser inspeccionado por ver hello `operations` propiedad. También puede usar Hola siguiendo métodos toowork con operaciones:

* **clear** : borra todas las operaciones de un lote
* **getOperations** -Obtiene una operación del lote de Hola
* **hasOperations** -devuelve true si el lote de hello contiene operaciones
* **removeOperations** : quita una operación.
* **tamaño** -devuelve Hola número de operaciones en lote Hola

## <a name="retrieve-an-entity-by-key"></a>Recuperación de una entidad por clave
tooreturn una entidad específica en función de hello **PartitionKey** y **RowKey**, usar hello **retrieveEntity** método.

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

Una vez completada, esta operación `result` contendrá entidad Hola.

## <a name="query-a-set-of-entities"></a>Consulta de un conjunto de entidades
tooquery una tabla, utilice hello **TableQuery** toobuild una expresión de consulta mediante Hola después de las cláusulas de objeto:

* **Seleccione** -Hola campos toobe procedentes de la consulta de Hola
* **donde** : hello donde cláusula

  * **and**: es una condición where `and`
  * **or**: es una condición where `or`
* **parte superior** -Hola número de elementos toofetch

Hello en el ejemplo siguiente se genera una consulta que devolverá Hola superiores cinco elementos con un PartitionKey de 'hometasks'.

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

Dado que **select** no se usa, se devolverán todos los campos. consulta de Hola de tooperform en una tabla, utilice **queryEntities**. Hello en el ejemplo siguiente se usa este tooreturn consultar entidades de "mytable".

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

Si se realiza correctamente, `result.entries` contendrá una matriz de entidades que coinciden con la consulta de Hola. Si la consulta de hello era tooreturn no se puede todas las entidades, `result.continuationToken` será no son*null* y puede utilizarse como Hola tercer parámetro del **queryEntities** tooretrieve más resultados. Para la consulta inicial de hello, use *null* para el tercer parámetro de Hola.

### <a name="query-a-subset-of-entity-properties"></a>Consulta de un subconjunto de propiedades de las entidades
Una tabla de tooa de consulta puede recuperar solo unos cuantos campos de una entidad.
Esto reduce el ancho de banda y puede mejorar el rendimiento de las consultas, en especial en el caso de entidades de gran tamaño. Hola de uso **seleccione** devuelven los nombres de Hola de cláusula y pase de hello campos toobe. Por ejemplo, hello siguiente consulta devolverá solo hello **descripción** y **dueDate** campos.

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a>Eliminación de una entidad
Puede eliminar una entidad usando sus claves de partición y fila. En este ejemplo, Hola **Tarea1** objeto contiene Hola **RowKey** y **PartitionKey** valores de hello entidad toobe eliminado. A continuación, se pasa el objeto de hello toohello **deleteEntity** método.

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> Considere el uso de valores de eTag al eliminar elementos, tooensure que Hola de elemento no se haya modificado por otro proceso. Consulte [Actualización de una entidad](#update-an-entity) para obtener información sobre el uso de etiquetas ETag.
>
>

## <a name="delete-a-table"></a>Eliminación de una tabla
Hola siguiente código elimina una tabla de una cuenta de almacenamiento.

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

Si no está seguro de si existe la tabla de hello, use **deleteTableIfExists**.

## <a name="use-continuation-tokens"></a>Usar tokens de continuación
Cuando consulte tablas para grandes cantidades de resultados, busque tokens de continuación. Puede haber grandes cantidades de datos disponibles para la consulta que no es posible que consiga si no genere toorecognize cuando hay un token de continuación.

resultados de Hello objeto devuelto durante consultar conjuntos de entidades un `continuationToken` propiedad cuando está presente un token de este tipo. A continuación, puede usar al realizar una toomove de toocontinue de consulta en las entidades de partición y la tabla de Hola.

Al realizar una consulta, puede proporcionarse un parámetro de continuationToken entre la instancia de objeto de consulta de Hola y función de devolución de llamada de hello:

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

Si examina hello `continuationToken` objeto, encontrará propiedades como `nextPartitionKey`, `nextRowKey` y `targetLocation`, lo que puede ser usado tooiterate a través de todos los resultados de Hola.

También hay un ejemplo de continuación en el repositorio de hello Node.js de almacenamiento de Azure en GitHub. Busque `examples/samples/continuationsample.js`.

## <a name="work-with-shared-access-signatures"></a>Trabajo con firmas de acceso compartido
Firmas de acceso compartido (SAS) son un tootables de acceso granular de tooprovide de forma segura sin tener que proporcionar el nombre de la cuenta de almacenamiento o claves. SAS son a menudo utilizados tooprovide limitado acceder a tooyour los datos, como permitir que una aplicación móvil tooquery registros.

Una aplicación de confianza, como un servicio basado en la nube genera una SAS con hello **generatesharedaccesssignature tal** de hello **TableService**y proporciona tooan aplicación de confianza o de confianza parcial Por ejemplo, una aplicación móvil. Hola SAS se genera mediante una directiva, que describe el inicio de Hola y fechas de finalización durante qué Hola SAS es válido, así como Hola titular SAS toohello concedidos nivel de acceso.

Hello en el ejemplo siguiente se genera una nueva directiva de acceso compartido que le permitirá hello tooquery ("r") de la tabla de hello SAS titular y expira 100 minutos tarde Hola se crea.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

Recuerde que debe ser información de host de hello siempre también, tal y como se requiere cuando titular SAS de hello intentos de tabla de hello tooaccess.

Hola aplicación cliente, a continuación, utiliza Hola SAS con **TableServiceWithSAS** tooperform operaciones contra la tabla Hola. Hola siguiente ejemplo conecta la tabla toohello y realiza una consulta.

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

Dado que hello SAS se genera con acceso de consulta solo si se realiza un intento tooinsert, actualizar o eliminar entidades, se devolvería un error.

### <a name="access-control-lists"></a>Listas de control de acceso
También puede usar una directiva de acceso de Hola de tooset de lista de Control de acceso (ACL) para una SAS. Esto es útil si desea tooallow varias tablas de hello tooaccess de los clientes, pero proporcionar las directivas de acceso diferente para cada cliente.

Una ACL se implementa mediante el uso de un conjunto de directivas de acceso, con un Id. asociado a cada directiva. Hola siguiente ejemplo define dos directivas, uno para "user1" y otro para el usuario '2':

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Hola siguiendo el ejemplo se obtiene Hola ACL actual para hello **hometasks** de tabla y, a continuación, agrega nuevas directivas de hello mediante **setTableAcl**. Este enfoque permite lo siguiente:

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Una vez se ha establecido la ACL de hello, puede crear una SAS basada en Id. de Hola para una directiva. Hola de ejemplo siguiente crea una nueva SAS para el usuario '2':

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea Hola recursos siguientes.

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente disponible, de Microsoft que le permite toowork visualmente con datos del almacenamiento de Azure en Windows, Mac OS y Linux.
* [SDK de almacenamiento de Azure para Node.js](https://github.com/Azure/azure-storage-node) en GitHub
* [Centro para desarrolladores de Node.js](/develop/nodejs/)
* [Crear e implementar un tooan de aplicación Node.js sitio Web de Azure](../app-service-web/app-service-web-get-started-nodejs.md)
