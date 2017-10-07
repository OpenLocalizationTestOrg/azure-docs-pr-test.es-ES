---
title: almacenamiento de blobs de Node.js del aaaHow toouse | Documentos de Microsoft
description: Almacenar datos no estructurados en la nube de hello con almacenamiento de blobs de Azure (almacenamiento de objetos).
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 572e7fc9f7b19ff01720a7cadd495c809ed49fb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a>¿Cómo toouse almacenamiento de blobs de Node.js
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a>Información general
Este artículo muestra cómo tooperform escenarios comunes con almacenamiento de blobs. ejemplos de Hola se escriben a través de la API Node.js Hola. escenarios de Hello descritos incluyen cómo tooupload, enumerar, descargar y eliminar los blobs.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a>Creación de una aplicación Node.js
Para obtener instrucciones sobre cómo toocreate una aplicación Node.js, vea [creación de una aplicación web de Node.js en el servicio de aplicación de Azure], [compilar e implementar un tooan de aplicación servicio de nube de Azure de Node.js](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) --con Windows PowerShell, o [de compilación y implementar un tooAzure de aplicación web de Node.js mediante Web Matrix](https://www.microsoft.com/web/webmatrix/).

## <a name="configure-your-application-tooaccess-storage"></a>Configurar el almacenamiento de tooaccess de aplicación
toouse almacenamiento de Azure, necesitará Hola SDK de almacenamiento de Azure para Node.js, que incluye un conjunto de bibliotecas de conveniencia que se comunican con servicios REST de almacenamiento de Hola.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Usar el Administrador de paquetes de nodo (NPM) tooobtain Hola paquete
1. Use una interfaz de línea de comandos como **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Unix), toonavigate toohello carpeta en la que creó el ejemplo aplicación.
2. Tipo de **npm instalar almacenamiento de azure** en la ventana de comandos de Hola. Salida de comando de hello es toohello similar el ejemplo de código siguiente.

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
3. También puede ejecutar manualmente hello **ls** tooverify de comando que un **nodo\_módulos** se creó la carpeta. Dentro de esa carpeta, busque hello **almacenamiento de azure** paquete, que contiene las bibliotecas de Hola que necesita almacenamiento tooaccess.

### <a name="import-hello-package"></a>Importar paquete de Hola
Con el Bloc de notas u otro editor de texto, agregar Hola después de la parte superior de toohello de Hola **server.js** archivo de aplicación hello donde piensa toouse almacenamiento:

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a>Configuración de una conexión de almacenamiento de Azure
Hello Azure módulo leerá las variables de entorno de hello `AZURE_STORAGE_ACCOUNT` y `AZURE_STORAGE_ACCESS_KEY`, o `AZURE_STORAGE_CONNECTION_STRING`, para obtener información necesaria tooconnect tooyour cuenta de almacenamiento Azure. Si no se establecen estas variables de entorno, debe especificar la información de la cuenta de hello al llamar a **createBlobService**.

Para obtener un ejemplo de establecer las variables de entorno de hello en hello [portal de Azure](https://portal.azure.com) para una aplicación web de Azure, consulte [aplicación web de Node.js con Hola servicio tabla de Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).

## <a name="create-a-container"></a>Crear un contenedor
Hola **BlobService** objeto le permite trabajar con contenedores y blobs. Hello código siguiente se crea un **BlobService** objeto. Agregue Hola siguiente cerca de la parte superior de Hola de **server.js**:

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> Se puede tener acceso a un blob de forma anónima mediante el uso de **createBlobServiceAnonymous** y proporcionar la dirección de host de Hola. Por ejemplo, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

toocreate un nuevo contenedor, use **createContainerIfNotExists**. Hello ejemplo de código siguiente crea un nuevo contenedor denominado 'mycontainer':

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

Si se acaba de crear el contenedor de hello, `result.created` es true. Si ya existe un contenedor de hello, `result.created` es false. `response`contiene información acerca de la operación de hello, incluida la información de ETag de hello para el contenedor de Hola.

### <a name="container-security"></a>Seguridad del contenedor
De forma predeterminada, los nuevos contenedores son privados, así que no se puede acceder a ellos de forma anónima. contenedor de hello toomake pública para que se pueda acceder de forma anónima, puede establecer nivel de acceso del contenedor de hello demasiado**blob** o **contenedor**.

* **BLOB** -permite acceso de lectura anónimo tooblob contenido y metadatos dentro de este contenedor, pero no los metadatos de toocontainer como enumerar todos los blobs dentro de un contenedor
* **contenedor** -permite acceso de lectura anónimo tooblob contenido y metadatos, así como metadatos del contenedor

Hello ejemplo de código siguiente muestra el nivel de acceso de configuración Hola demasiado**blob**:

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

Como alternativa, puede modificar el nivel de acceso de Hola de un contenedor mediante el uso de **setContainerAcl** nivel de acceso de toospecify Hola. Hola siguiente de código toocontainer de nivel de acceso de Hola de cambios de ejemplo:

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

resultado hello contiene información acerca de la operación de hello, incluida la corriente de hello **ETag** para el contenedor de Hola.

### <a name="filters"></a>Filtros
Puede aplicar opcional filtrado operaciones toooperations realizadas utilizando **BlobService**. Las operaciones de filtrado pueden incluir registros, reintentos automáticos, etc. Los filtros son objetos que implementan un método con firma de hello:

```nodejs
function handle (requestOptions, next)
```

Después de realizar su procesamiento previo en Opciones de solicitud de hello, método hello necesita toocall "siguiente", pasando una devolución de llamada con hello siguiente firma:

```nodejs
function (returnObject, finalCallback, next)
```

En esta devolución de llamada y, después de procesar hello returnObject (respuesta Hola Hola solicitud enviada toohello al servidor), la devolución de llamada de hello necesita tooeither invocar a continuación si existe toocontinue otros filtros de procesamiento o simplemente invocar el servicio de finalCallback tooend Hola invocación.

Dos filtros que implementan la lógica de reintento se incluyen con hello Azure SDK para Node.js, **ExponentialRetryPolicyFilter** y **LinearRetryPolicyFilter**. Hola siguiente crea un **BlobService** objeto que usa hello **ExponentialRetryPolicyFilter**:

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a>Cargar un blob en un contenedor
Hay tres tipos de blobs: blobs en bloques, blobs en páginas y blobs en anexos. Los blobs en bloques permiten toomore eficazmente cargar datos de gran tamaño. Los blobs en anexos están optimizados para las operaciones de anexión. Los blobs en páginas están optimizados para las operaciones de lectura y escritura. Para más información, consulte [Descripción de los blobs en bloques, en anexos y en páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).

### <a name="block-blobs"></a>Blobs en bloques
tooupload datos tooa blob en bloques, Hola de uso siguientes:

* **createBlockBlobFromLocalFile** : crea un nuevo blob en bloques y carga el contenido de Hola de un archivo
* **createBlockBlobFromStream** : crea un nuevo blob en bloques y carga el contenido de Hola de un flujo
* **createBlockBlobFromText** : crea un nuevo blob en bloques y carga el contenido de Hola de una cadena
* **createWriteStreamToBlockBlob** -proporciona un blob en bloques escritura flujo tooa

Hello ejemplo de código siguiente carga contenido Hola de hello **test.txt** el archivo en **myblob**.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

Hola `result` estos métodos devuelven contiene información sobre el funcionamiento de hello, como hello **ETag** de blob de Hola.

### <a name="append-blobs"></a>Blobs en anexos
tooupload datos tooa nueva anexar blob, utilice Hola siguiente:

* **createAppendBlobFromLocalFile** : crea un nuevo blob en anexos y carga el contenido de Hola de un archivo
* **createAppendBlobFromStream** : crea un nuevo blob en anexos y carga el contenido de Hola de un flujo
* **createAppendBlobFromText** : crea un nuevo blob en anexos y carga el contenido de Hola de una cadena
* **createWriteStreamToNewAppendBlob** : crea un nuevo blob en anexos y, a continuación, proporciona un tooit de toowrite de secuencia

Hello ejemplo de código siguiente carga contenido Hola de hello **test.txt** el archivo en **myappendblob**.

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

tooappend un bloque existente de tooan anexar blob, Hola de uso siguientes:

* **appendFromLocalFile** -anexar Hola contenido de un archivo tooan existente anexar blob
* **appendFromStream** -anexar Hola contenido de una secuencia tooan existente anexar blob
* **appendFromText** -anexar Hola contenido de una cadena tooan existente anexar blob
* **appendBlockFromStream** -anexar Hola contenido de una secuencia tooan existente anexar blob
* **appendBlockFromText** -anexar Hola contenido de una cadena tooan existente anexar blob

> [!NOTE]
> appendFromXXX API realizará algunas llamadas de validación del lado cliente toofail tooavoid rápido innecesario del servidor. appendBlockFromXXX no.
>
>

Hello ejemplo de código siguiente carga contenido Hola de hello **test.txt** el archivo en **myappendblob**.

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a>Blobs en páginas
tooupload datos tooa blob en páginas, Hola de uso siguientes:

* **createPageBlob** : crea un nuevo blob en páginas de una longitud especificada.
* **createPageBlobFromLocalFile** : crea un nuevo blob en páginas y carga el contenido de Hola de un archivo
* **createPageBlobFromStream** : crea un nuevo blob en páginas y carga el contenido de Hola de un flujo
* **createWriteStreamToExistingPageBlob** -proporciona un escritura flujo tooan blob en páginas existente
* **createWriteStreamToNewPageBlob** : crea un nuevo blob en páginas y, a continuación, proporciona un tooit de toowrite de secuencia

Hello ejemplo de código siguiente carga contenido Hola de hello **test.txt** el archivo en **mypageblob**.

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> Los blobs en páginas constan de 'páginas' de 512 bytes. Al cargar datos con un tamaño que no sea múltiplo de 512 recibirá un error.
>
>

## <a name="list-hello-blobs-in-a-container"></a>Lista de blobs de hello en un contenedor
blobs de hello toolist en un contenedor, use hello **listBlobsSegmented** método. Si desea que tooreturn blobs con un prefijo concreto, utilice **listBlobsSegmentedWithPrefix**.

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

Hola `result` contiene un `entries` colección, que es una matriz de objetos que describen cada blob. Si no se puede devolver todos los blobs, Hola `result` también proporciona un `continuationToken`, que se puede utilizar como entradas adicionales de hello segundo parámetro tooretrieve.

## <a name="download-blobs"></a>Descargar blobs
datos de toodownload de un blob, use siguiente hello:

* **getBlobToLocalFile** -escribe Hola blob contenido toofile
* **getBlobToStream** -escribe Hola blob contenido tooa secuencia
* **getBlobToText** -escribe el contenido de blob de hello tooa cadena
* **createReadStream** -proporciona un tooread de flujo de blob de Hola

Hello ejemplo de código siguiente muestra cómo utilizar **getBlobToStream** contenido de hello toodownload de hello **myblob** blob y almacenar toohello **output.txt** un archivo utilizando un secuencia:

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

Hola `result` contiene información sobre el blob de hello, incluidos los **ETag** información.

## <a name="delete-a-blob"></a>Eliminar un blob
Por último, llame un blob, toodelete **deleteBlob**. Hola el siguiente ejemplo de código elimina Hola blob denominado **myblob**.

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a>simultáneo
blob en tooa toosupport acceso simultáneo de varios clientes o varias instancias de proceso, puede usar **ETags** o **concesiones**.

* **ETag** -proporciona un toodetect de manera que Hola blob o contenedor ha sido modificado por otro proceso
* **Concesión** : proporciona una manera tooobtain exclusivo renovable, escritura o eliminar el blob de tooa de acceso para un período de tiempo

### <a name="etag"></a>ETag
Usar ETags si necesita tooallow varios clientes o instancias toowrite toohello bloque Blob o página Blob simultáneamente. Hello ETag permite toodetermine si hello contenedor o blob se ha modificado desde que inicialmente lee o crearla, lo que permite tooavoid sobrescriba los cambios confirmados por otro proceso o cliente.

Puede establecer condiciones de ETag mediante Hola opcional `options.accessConditions` parámetro. Hello ejemplo de código siguiente solo carga hello **test.txt** contiene archivos si blob Hola ya existe y tiene el valor de ETag hello `etagToMatch`.

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

Cuando se usa ETags, patrón general de hello es:

1. Obtener Hola ETag como resultado de hello de crear, la lista o la operación get.
2. Realizar una acción, comprobación de ese valor de ETag hello no se ha modificado.

Si se ha modificado el valor de hello, esto indica que otro cliente o instancia modificado Hola blob o contenedor desde que obtuvo el valor de ETag Hola.

### <a name="lease"></a>Concesión
Puede adquirir una nueva concesión mediante hello **acquireLease** método, especificando el blob de Hola o un contenedor que desee tooobtain una concesión en. Por ejemplo, el siguiente código de hello adquiere una concesión en **myblob**.

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

Las operaciones subsiguientes en **myblob** debe proporcionar hello `options.leaseId` parámetro. concesión de Hello Id. se devuelve como `result.id` de **acquireLease**.

> [!NOTE]
> De forma predeterminada, la duración de la concesión de hello es infinita. Puede especificar una duración no infinita (entre 15 y 60 segundos) proporcionando hello `options.leaseDuration` parámetro.
>
>

usar tooremove una concesión, **releaseLease**. toobreak una concesión, pero impedir que otras personas obtengan una nueva concesión hasta que expire la duración original de hello, use **breakLease**.

## <a name="work-with-shared-access-signatures"></a>Trabajo con firmas de acceso compartido
Firmas de acceso compartido (SAS) son un tooblobs de forma segura tooprovide acceso granular y contenedores sin proporcionar el nombre de la cuenta de almacenamiento o claves. Firmas de acceso compartido con frecuencia son datos de tooyour de acceso de tooprovide uso limitado, como permitir que una aplicación móvil tooaccess blobs.

> [!NOTE]
> Aunque también puede permitir el acceso anónimo tooblobs, firmas de acceso compartido permiten el acceso tooprovide más controlado, como debe generar Hola SAS.
>
>

Una aplicación de confianza, como un servicio basado en la nube genera firmas de acceso compartido con hello **generatesharedaccesssignature tal** de hello **BlobService**y le proporciona tooan no es de confianza o aplicación de confianza parcial, como una aplicación móvil. Acceso compartido firmas se generan mediante una directiva, que describe el inicio de Hola y fechas de finalización durante qué Hola firmas de acceso compartido son válidas, así como Hola tener acceso a nivel titular de firmas de acceso compartido toohello concedidos.

ejemplo de código siguiente Hello genera una nueva directiva de acceso compartido que permite Hola compartido acceso firmas titular tooperform operaciones de lectura en hello **myblob** blob y expira 100 minutos tarde Hola se crea.

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

Tenga en cuenta que la información de host de hello debe estar siempre también, tal y como se requiere cuando el titular de firmas de acceso compartido de Hola intente en el contenedor de hello tooaccess.

Hola, a continuación, la aplicación cliente usa firmas de acceso compartido con **BlobServiceWithSAS** tooperform operaciones con blobs de Hola. Hello siguiente obtiene información sobre **myblob**.

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

Puesto que las firmas de acceso compartido de hello generadas con acceso de solo lectura, si se realiza un intento de blob de hello toomodify, se devolverá un error.

### <a name="access-control-lists"></a>Listas de control de acceso
También puede usar una directiva de acceso (ACL) de la lista tooset Hola de acceso control SAS. Esto es útil si desea tooallow varios clientes tooaccess un contenedor, pero proporcionar las directivas de acceso diferente para cada cliente.

Una ACL se implementa mediante el uso de un conjunto de directivas de acceso, con un Id. asociado a cada directiva. Hola, ejemplo de código siguiente define dos directivas, uno para "user1" y otro para el usuario '2':

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

Hola siguiendo el ejemplo de código obtiene Hola ACL actual para **mycontainer**y, a continuación, agrega nuevas directivas de hello mediante **setBlobAcl**. Este enfoque permite lo siguiente:

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

Una vez Hola que ACL se establece, puede crear en función de Id. de Hola para una directiva de firmas de acceso compartido. Hola, ejemplo de código siguiente crea nuevas firmas de acceso compartido para el usuario '2':

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea Hola recursos siguientes.

* [Referencia de la API del SDK de Azure Storage para Node][Referencia de la API del SDK de Azure Storage para Node]
* [Blog del equipo de Azure Storage] [Blog del equipo de Azure Storage]
* [SDK de Azure Storage para Node.js][Azure Storage SDK for Node] en GitHub
* [Centro para desarrolladores de Node.js](https://azure.microsoft.com/develop/nodejs/)
* [Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

[Aplicación web de Node.js con hello servicio tabla de Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)    
[Compilar e implementar un tooAzure de aplicación web de Node.js mediante Web Matrix]: https://www.microsoft.com/web/webmatrix/  
[Usar Hola REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx [portal de Azure]: https://portal.azure.com [compilar e implementar un tooan de aplicación Node.js servicio de nube de Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Blog del equipo de almacenamiento de Azure]: http:// blogs.msdn.com/b/windowsazurestorage/ [almacenamiento de Azure SDK para la referencia de la API de nodo]: http://dl.windowsazure.com/nodestoragedocs/index.html
