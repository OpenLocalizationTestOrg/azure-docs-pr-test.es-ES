---
title: aaaManaging simultaneidad en el almacenamiento de Azure de Microsoft
description: "¿Cómo toomanage simultaneidad para Hola servicios Blob, cola, tabla y archivo"
services: storage
documentationcenter: 
author: jasontang501
manager: tadb
editor: tysonn
ms.assetid: cc6429c4-23ee-46e3-b22d-50dd68bd4680
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: jasontang501
ms.openlocfilehash: 5b8efbe0a9ebc881ded8f3abef5f138e0385f7c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-concurrency-in-microsoft-azure-storage"></a>Administración de la simultaneidad en Almacenamiento de Microsoft Azure
## <a name="overview"></a>Información general
Las aplicaciones modernas basadas en Internet, normalmente tienen varios usuarios que ven y actualizan datos simultáneamente. Para ello, toothink a los desarrolladores de aplicaciones con cuidado sobre cómo tooprovide una predicción experimentar los usuarios finales de tootheir, especialmente para escenarios donde pueden actualizar varios usuarios Hola mismo datos. Hay tres estrategias principales de simultaneidad de datos que normalmente tienen en cuenta los desarrolladores:  

1. Simultaneidad optimista: última una aplicación para realizar una actualización como parte de su actualización comprobará si los datos de hello ha cambiado desde la aplicación hello lee esos datos. Por ejemplo, si dos usuarios ver una página wiki realizan un toohello actualización misma página, a continuación, debe asegurarse de que esa segunda actualización hello no sobrescribe la primera actualización hello: plataforma de wiki de Hola y de ambos usuarios comprenden si su actualización fue correcta o no. Esta estrategia se usa con más frecuencia en aplicaciones web.
2. Simultaneidad pesimista: una aplicación busca tooperform una actualización tomará un bloqueo en un objeto para evitar que otros usuarios actualicen datos Hola hasta que se libere el bloqueo de Hola. Por ejemplo, en un escenario de replicación de datos maestro/esclavo donde llevará a cabo actualizaciones solo master Hola master Hola normalmente contendrá un bloqueo exclusivo para un período de tiempo en hello datos tooensure ningún otro usuario puede actualizarlo.
3. Último escritor gana: un método que le permita cualquier tooproceed de las operaciones de actualización sin comprobar si cualquier otra aplicación ha Hola datos actualizados desde la aplicación hello primero lectura datos Hola. Esta estrategia (o la falta de una estrategia formal) suele utilizarse donde los datos se dividen de forma que no hay ninguna posibilidad de que varios usuarios tendrán acceso Hola mismos datos. También puede resultar útil donde se procesen transmisiones de datos de corta duración.  

Este artículo proporciona información general sobre la plataforma de almacenamiento de Azure Hola simplifica el desarrollo proporcionando soporte de primera clase para las tres de estas estrategias de simultaneidad.  

## <a name="azure-storage--simplifies-cloud-development"></a>Almacenamiento de Azure: simplificación del desarrollo en la nube
Hola servicio almacenamiento de Azure es compatible con todas las tres estrategias, aunque es distintivo en su capacidad tooprovide totalmente compatible con la simultaneidad optimista y pesimista porque se trataba de tooembrace diseñado un modelo de coherencia fuerte que garantiza que, cuando Hola confirmaciones de servicio de almacenamiento datos insertar o actualizar operación toothat más todos los accesos a datos verá Hola actualización más reciente. Plataformas de almacenamiento que utilizan un modelo de coherencia definitiva tienen un retraso entre cuando un usuario realiza una operación de escritura y cuando Hola actualiza datos pueden verse por otros usuarios, por tanto, lo que complica el desarrollo de aplicaciones de cliente en incoherencias de tooprevent de orden de que afectan a los usuarios finales.  

Además tooselecting una simultaneidad correcta estrategia los desarrolladores deben también tener en cuenta cómo una plataforma de almacenamiento aísla los cambios, especialmente los toohello cambios mismo objeto a través de las transacciones. Hola servicio almacenamiento de Azure usa tooallow de aislamiento de instantánea leer operaciones toohappen simultáneamente con las operaciones de escritura en una única partición. A diferencia de otros niveles de aislamiento, el aislamiento de instantánea garantiza que todas las lecturas verán una instantánea coherente de los datos de hello incluso mientras se producen actualizaciones – básicamente devolviendo valores último confirmada de hello mientras se procesa una transacción de actualización.  

## <a name="managing-concurrency-in-blob-storage"></a>Administrar la simultaneidad en almacenamiento de blobs
Puede optar por toouse tanto modelos de simultaneidad optimista o pesimista toomanage acceso tooblobs y contenedores en Hola servicio blob. Si no especifica explícitamente una estrategia de última escribe wins es el valor predeterminado de Hola.  

### <a name="optimistic-concurrency-for-blobs-and-containers"></a>Simultaneidad optimista para blobs y contenedores
Hola servicio de almacenamiento asigna un objeto de tooevery identificador almacenado. Este identificador se actualiza cada vez que se realiza una operación de actualización en un objeto. identificador de Hola se devuelve a toohello cliente como parte de una respuesta HTTP GET con encabezado de ETag (etiqueta de entidad) de Hola que se define en el protocolo de hello HTTP. Un usuario para realizar una actualización de este tipo de objeto puede enviar en Hola ETag original junto con un tooensure encabezado condicional que una actualización sólo aparecerá si se cumple una determinada condición: en este caso condición hello es un encabezado "If-Match", que requiere Hola almacenamiento Servicio tooensure Hola valo Hola ETag especificado en la solicitud de actualización de hello es Hola mismos que almacenan en hello servicio de almacenamiento.  

esquema de Hola de este proceso es el siguiente:  

1. Recuperar un blob del servicio de almacenamiento de hello, respuesta de hello incluye un valor de encabezado de ETag de HTTP que identifica la versión actual de hello del objeto de hello en el servicio de almacenamiento de Hola.
2. Cuando se actualiza el blob de hello, incluir el valor de ETag de Hola que recibió en el paso 1 en hello **If-Match** condicional encabezado de solicitud de hello enviar toohello servicio.
3. servicio de Hello compara el valor de ETag de hello en solicitud de hello con valor de ETag actual de Hola de blob de Hola.
4. Si valor de ETag actual de Hola de blob de hello es una versión diferente de Hola ETag en hello **If-Match** encabezado condicional en solicitud de hello, servicio de hello devuelve un cliente de toohello 412 error. Esto indica que otro proceso ha actualizado el blob de Hola desde cliente Hola recuperó de cliente de toohello.
5. Si Hola actual ETag es el valor del blob de Hola Hola misma versión que Hola ETag en hello **If-Match** realiza condicional encabezado de solicitud de hello, servicio de Hola Hola solicitó la operación y las actualizaciones de Hola el valor ETag actual de blob de Hola tooshow que ha creado una nueva versión.  

Hello siguiente fragmento de C# (mediante la biblioteca de cliente de almacenamiento 4.2.0 Hola) muestra un ejemplo sencillo de cómo tooconstruct una **AccessCondition If-Match** según Hola valor ETag que se obtiene acceso desde propiedades Hola de un blob que estaba previamente recuperados o insertado. A continuación, utiliza hello **AccessCondition** objeto cuando se actualiza el blob de hello: Hola **AccessCondition** objeto agrega hello **If-Match** solicitud toohello de encabezado. Si otro proceso ha actualizado el blob de hello, servicio de blob de hello devuelve un mensaje de estado 412 de HTTP (error de condición previa). Puede descargar aquí completo ejemplo hello: [administración de simultaneidad con el almacenamiento de Azure](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).  

```csharp
// Retrieve hello ETag from hello newly created blob
// Etag is already populated as UploadText should cause a PUT Blob call
// toostorage blob service which returns hello etag in response.
string orignalETag = blockBlob.Properties.ETag;

// This code simulates an update by a third party.
string helloText = "Blob updated by a third party.";

// No etag, provided so orignal blob is overwritten (thus generating a new etag)
blockBlob.UploadText(helloText);
Console.WriteLine("Blob updated. Updated ETag = {0}",
blockBlob.Properties.ETag);

// Now try tooupdate hello blob using hello orignal ETag provided when hello blob was created
try
{
    Console.WriteLine("Trying tooupdate blob using orignal etag toogenerate if-match access condition");
    blockBlob.UploadText(helloText,accessCondition:
    AccessCondition.GenerateIfMatchCondition(orignalETag));
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
    {
        Console.WriteLine("Precondition failure as expected. Blob's orignal etag no longer matches");
        // TODO: client can decide on how it wants toohandle hello 3rd party updated content.
    }
    else
        throw;
}  
```

Hola servicio de almacenamiento también incluye compatibilidad para encabezados condicionales adicionales como **If-Modified-Since**, **If-Unmodified-Since** y **If-None-Match** como combinaciones de los mismos. Para obtener más información, consulte [Especificación de encabezados condicionales para las operaciones de Blob Service](http://msdn.microsoft.com/library/azure/dd179371.aspx) en MSDN.  

Hello tabla siguiente resumen las operaciones de contenedor de Hola que aceptan como encabezados condicionales **If-Match** en solicitud de Hola y que devuelven un valor de ETag en la respuesta de Hola.  

| Operación | Devuelve el valor ETag del contenedor | Acepta encabezados condicionales |
|:--- |:--- |:--- |
| Create Container |Sí |No |
| Get Container Properties |Sí |No |
| Get Container Metadata |Sí |No |
| Set Container Metadata |Sí |Sí |
| Get Container ACL |Sí |No |
| Set Container ACL |Sí |Sí (*) |
| Delete Container |No |Sí |
| Lease Container |Sí |Sí |
| List Blobs |No |No |

permisos de hello (*) definidos por SetContainerACL se almacenan en caché y las actualizaciones toothese permisos tarden 30 segundos toopropagate durante el periodo del que las actualizaciones no están garantiza toobe coherente.  

Hello tabla siguiente resumen las operaciones de blob de Hola que aceptan como encabezados condicionales **If-Match** en solicitud de Hola y que devuelven un valor de ETag en la respuesta de Hola.

| Operación | Devuelve el valor ETag | Acepta encabezados condicionales |
|:--- |:--- |:--- |
| Put Blob |Sí |Sí |
| Get Blob |Sí |Sí |
| Get Blob Properties |Sí |Sí |
| Set Blob Properties |Sí |Sí |
| Get Blob Metadata |Sí |Sí |
| Set Blob Metadata |Sí |Sí |
| Lease Blob (*) |Sí |Sí |
| Instantánea de blob |Sí |Sí |
| Copia de blobs |Sí |Sí (para blob de origen y destino) |
| Abort Copy Blob |No |No |
| Delete Blob |No |Sí |
| Put Block |No |No |
| Put Block List |Sí |Sí |
| Get Block List |Sí |No |
| Put Page |Sí |Sí |
| Get Page Ranges |Sí |Sí |

(*) Blob de concesión no cambia Hola ETag en un blob.  

### <a name="pessimistic-concurrency-for-blobs"></a>Simultaneidad pesimista para blobs
toolock un blob para uso exclusivo, puede adquirir un [concesión](http://msdn.microsoft.com/library/azure/ee691972.aspx) en él. Al adquirir una concesión, se especifica durante cuánto tiempo necesita Hola concesión: puede ser de entre 15 segundos de too60 o infinito, que los importes tooan un bloqueo exclusivo. Puede renovar una tooextend de concesión finito y puede liberar cualquier concesión cuando haya terminado con él. servicio de blob de Hello libera automáticamente concesiones finitos cuando expiran.  

Concesiones de habilitar la sincronización diferentes estrategias toobe admitido, incluidos exclusivo de escritura / comparten lectura, exclusivo de escritura / exclusivo de lectura y compartido de escritura / lectura exclusivo. Cuando existe una concesión de servicio de almacenamiento de Hola exige exclusivo de escritura (put, defina y las operaciones de eliminación) sin embargo garantizar la exclusividad de las operaciones de lectura requiere Hola developer tooensure que todas las aplicaciones cliente usar un identificador de concesión y que solo un cliente a la vez tiene un identificador de concesión válido. Las operaciones de lectura que no incluyen un identificador de concesión, dan lugar a lecturas compartidas.  

Hello fragmento de C# siguiente muestra un ejemplo de adquirir una concesión exclusiva durante 30 segundos en un blob, actualizar el contenido de Hola de blob de hello y, a continuación, liberar la concesión de Hola. Si ya hay una concesión válido en el blob de hello cuando intente tooacquire una nueva concesión, el servicio de blob de hello devuelve un resultado de estado de "HTTP (409) conflicto". Hello siguiente fragmento de código utiliza un **AccessCondition** tooencapsulate Hola concesión información del objeto al realizar un blob de hello tooupdate de solicitud de servicio de almacenamiento de Hola.  Puede descargar aquí completo ejemplo hello: [administración de simultaneidad con el almacenamiento de Azure](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

```csharp
// Acquire lease for 15 seconds
string lease = blockBlob.AcquireLease(TimeSpan.FromSeconds(15), null);
Console.WriteLine("Blob lease acquired. Lease = {0}", lease);

// Update blob using lease. This operation will succeed
const string helloText = "Blob updated";
var accessCondition = AccessCondition.GenerateLeaseCondition(lease);
blockBlob.UploadText(helloText, accessCondition: accessCondition);
Console.WriteLine("Blob updated using an exclusive lease");

//Simulate third party update tooblob without lease
try
{
    // Below operation will fail as no valid lease provided
    Console.WriteLine("Trying tooupdate blob without valid lease");
    blockBlob.UploadText("Update without lease, will fail");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
        Console.WriteLine("Precondition failure as expected. Blob's lease does not match");
    else
        throw;
}  
```

Si trata de una operación de escritura en un blob en concesión sin pasar un identificador de concesión de hello, se produce un error en la solicitud de Hola con un error 412. Tenga en cuenta que si hello concesión expira antes de llamar a hello **UploadText** método pero seguir pasando identificador de concesión de hello, Hola solicitud también produce un error con un **412** error. Para obtener más información acerca de cómo administrar los tiempos de expiración de concesión y los identificadores de concesión, vea hello [Lease Blob](http://msdn.microsoft.com/library/azure/ee691972.aspx) documentación de REST.  

Hello siguientes operaciones de blob pueden usar simultaneidad pesimista de concesiones toomanage:  

* Put Blob
* Get Blob
* Get Blob Properties
* Set Blob Properties
* Get Blob Metadata
* Set Blob Metadata
* Delete Blob
* Put Block
* Put Block List
* Get Block List
* Put Page
* Get Page Ranges
* Snapshot Blob (identificador de concesión opcional si existe una concesión)
* Identificador de concesión de Blob de copia; necesarios si existe una concesión de blob de destino de Hola
* Abort Copy Blob - identificador de concesión necesario si existe una concesión infinita en blob de destino de Hola
* Lease Blob  

### <a name="pessimistic-concurrency-for-containers"></a>Simultaneidad pesimista para contenedores
Concesiones en contenedores habilitar Hola admite la misma toobe de estrategias de sincronización como en blobs (exclusivo de escritura / compartido lectura, exclusivo de escritura / exclusivo de lectura y compartido de escritura / lectura exclusivo) sin embargo a diferencia de los blobs de servicio de almacenamiento de hello solo exige exclusividad en las operaciones de eliminación. toodelete un contenedor con una concesión activa, un cliente debe incluir el identificador de concesión activa de hello en solicitud de eliminación de Hola. Todas las demás operaciones de contenedor correctamente en un contenedor de concesión sin necesidad de incluir el identificador de concesión de hello en cuyo caso se comparten las operaciones. Si la exclusividad de la actualización (poner o establecer) o las operaciones de lectura son obligatorias, entonces los desarrolladores deben garantizar que todos los clientes usan un identificador de concesión y que solamente un cliente tiene un identificador de concesión válido en cada momento.  

Hello siguientes operaciones de contenedor pueden usar simultaneidad pesimista de concesiones toomanage:  

* Delete Container
* Get Container Properties
* Get Container Metadata
* Set Container Metadata
* Get Container ACL
* Set Container ACL
* Lease Container  

Para más información, consulte:  

* [Especificar encabezados condicionales para las operaciones del servicio BLOB](http://msdn.microsoft.com/library/azure/dd179371.aspx)
* [Lease Container](http://msdn.microsoft.com/library/azure/jj159103.aspx)
* [Concesiones de blob ](http://msdn.microsoft.com/library/azure/ee691972.aspx)

## <a name="managing-concurrency-in-hello-table-service"></a>Administrar la simultaneidad en hello servicio tabla
servicio de la tabla de Hello usa optimista de simultaneidad se comprueba como comportamiento predeterminado de hello cuando se trabaja con entidades, a diferencia del servicio de blob de hello en el que debe elegir explícitamente tooperform comprobaciones de simultaneidad optimista. Hola otra diferencia entre los servicios de tabla y blob de hello es que sólo se puede administrar comportamiento de simultaneidad de Hola de entidades, mientras que con el servicio de blobs de hello puede administrar la simultaneidad de Hola de contenedores y blobs.  

simultaneidad optimista toouse y toocheck si otro proceso modifica una entidad porque se recuperan del servicio de almacenamiento de tabla de Hola, puede usar el valor de ETag Hola que recibirá cuando el servicio de la tabla de hello devuelve una entidad. esquema de Hola de este proceso es el siguiente:  

1. Recuperar una entidad de servicio de almacenamiento de tabla de hello, respuesta de hello incluye un valor de ETag que identifica el identificador del actual Hola asociada a esa entidad en el servicio de almacenamiento de Hola.
2. Cuando se actualiza la entidad de hello, incluir el valor de ETag de Hola que recibió en el paso 1 en hello obligatorio **If-Match** encabezado de solicitud de hello enviar toohello servicio.
3. servicio de Hello compara el valor de ETag de hello en solicitud de hello con valor de ETag actual de Hola de entidad de Hola.
4. Si valor de ETag actual de Hola de entidad de hello es diferente al Hola ETag en hello obligatorio **If-Match** encabezado de solicitud de hello, servicio de hello devuelve un cliente de toohello 412 error. Esto indica que otro proceso ha actualizado entidad Hola desde cliente hello había recuperado de cliente de toohello.
5. Si es Hola Hola el valor ETag actual de entidad de hello igual Hola ETag en hello obligatorio **If-Match** encabezado de solicitud de Hola o hello **If-Match** encabezado contiene el carácter comodín de hello (*), servicio de Hola lleva a cabo Hola solicitó la operación y las actualizaciones de Hola el valor ETag actual de hello tooshow de entidad que se ha actualizado.  

Tenga en cuenta que, a diferencia del servicio de blob de hello, servicio de la tabla de hello requiere Hola cliente tooinclude una **If-Match** encabezado en las solicitudes de actualización. Sin embargo, es posible tooforce un incondicional actualizar (último escritor gana estrategia) y omitir las comprobaciones de simultaneidad si el cliente de hello establece hello **If-Match** carácter de comodín toohello encabezado (*) en la solicitud de saludo.  

Hola siguiente fragmento de código C# muestra una entidad cliente que ya se creó anteriormente o se recupera con su dirección de correo electrónico que se actualiza. Insertar Hello inicial o recuperar operación almacena el valor de ETag de hello en el objeto de cliente de Hola y como ejemplo de Hola utiliza hello misma instancia del objeto cuando se ejecuta Hola operación de reemplazo, envía automáticamente Hola ETag valor toohello back-servicio de tabla, Habilitar Hola servicio toocheck las infracciones de simultaneidad. Si otro proceso ha actualizado la entidad de hello en el almacenamiento de tabla, servicio de hello devuelve un mensaje de estado 412 de HTTP (error de condición previa).  Puede descargar aquí completo ejemplo hello: [administración de simultaneidad con el almacenamiento de Azure](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

```csharp
try
{
    customer.Email = "updatedEmail@contoso.org";
    TableOperation replaceCustomer = TableOperation.Replace(customer);
    customerTable.Execute(replaceCustomer);
    Console.WriteLine("Replace operation succeeded.");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == 412)
        Console.WriteLine("Optimistic concurrency violation – entity has changed since it was retrieved.");
    else
        throw;
}  
```

tooexplicitly deshabilitar la comprobación de simultaneidad de hello, debe establecer hello **ETag** propiedad de hello **empleado** objeto demasiado "*" antes de ejecutar la operación de reemplazo Hola.  

```csharp
customer.ETag = "*";  
```

Hello tabla siguiente resume cómo las operaciones de entidad de tabla de hello utilizan valores ETag:

| Operación | Devuelve el valor ETag | Requiere encabezado de solicitud If-Match |
|:--- |:--- |:--- |
| Query Entities |Sí |No |
| Insert Entity |Sí |No |
| Update Entity |Sí |Sí |
| Merge Entity |Sí |Sí |
| Delete Entity |No |Sí |
| Insert or Replace Entity |Sí |No |
| Insert or Merge Entity |Sí |No |

Tenga en cuenta que hello **insertar o reemplazar entidades** y **insertar o combinar entidades** Microsoft operations ¿ *no* porque no envían un toohello del valor de ETag, se realiza ninguna comprobación de simultaneidad servicio de la tabla.  

En general, los desarrolladores que usan tablas deben basarse en simultaneidad optimista cuando desarrollan aplicaciones escalables. Si se necesita el bloqueo pesimista, los desarrolladores de un enfoque pueden realizar cuando el acceso a tablas es tooassign un blob designado para cada tabla e inténtelo tootake una concesión en hello blob antes de operar en la tabla de Hola. Este método requiere Hola aplicación tooensure todo acceso a datos rutas de acceso obtener toooperating anteriores de concesión de hello en la tabla de Hola. También debe tener en cuenta que tiempo de concesión mínimo de hello es 15 segundos, que requiere una consideración cuidadosa de escalabilidad.  

Para más información, consulte:  

* [Operaciones en entidades](http://msdn.microsoft.com/library/azure/dd179375.aspx)  

## <a name="managing-concurrency-in-hello-queue-service"></a>Administrar la simultaneidad en hello servicio cola
Un escenario en que simultaneidad es un problema en el servicio de puesta en cola de hello es donde varios clientes recupere mensajes de una cola. Cuando se recupera un mensaje de cola de hello, respuesta de hello incluye mensajes de bienvenida y un valor de confirmación de recepción, que es el mensaje de bienvenida de toodelete necesarios. mensaje de bienvenida no se elimina automáticamente de cola de hello, pero después de que se ha recuperado, no es visible tooother clientes para intervalo de tiempo de hello especificado por el parámetro de hello visibilitytimeout. cliente de Hola que recupera mensajes de bienvenida es mensajes de bienvenida del toodelete esperado después de haberla procesado y antes de hello hora especificada por hello elemento TimeNextVisible de hello respuesta, que se calcula en función de valor de Hola de hello visibilitytimeout parámetro. valor de Hola de visibilitytimeout se agrega tiempo toohello en qué Hola mensaje es recupera toodetermine valor hello TimeNextVisible.  

servicio de cola de Hello no dispone de compatibilidad para la simultaneidad optimista o pesimista y para este deben asegurarse clientes motivo procesar mensajes recuperados de una cola de mensajes se procesan de manera idempotente. Una estrategia El último que escribe gana se usa para actualizar operaciones como SetQueueServiceProperties, SetQueueMetaData, SetQueueACL y UpdateMessage.  

Para más información, consulte:  

* [API de REST del servicio Cola](http://msdn.microsoft.com/library/azure/dd179363.aspx)
* [Get Messages](http://msdn.microsoft.com/library/azure/dd179474.aspx)  

## <a name="managing-concurrency-in-hello-file-service"></a>Administrar la simultaneidad en hello servicio de archivos
puede tener acceso al servicio de archivo de Hello mediante dos extremos de otro protocolo: SMB y REST. Hola servicio REST no dispone de compatibilidad de bloqueo optimista o el bloqueo pesimista y todas las actualizaciones seguirá una estrategia de wins último escritor. Los clientes SMB que montan recursos compartidos de archivos pueden aprovechar archivo bloqueo mecanismos toomanage acceso tooshared archivos del sistema, incluyendo Hola capacidad tooperform el bloqueo pesimista. Cuando un cliente SMB abre un archivo, especifica acceso de archivo de Hola y el recurso compartido de modo. Establecer una opción de acceso de archivo de "Escritura" o "Lectura/escritura" junto con un modo de uso compartido de archivo de "None" dará como resultado en el archivo hello está bloqueado por un cliente SMB hasta que se cierre el archivo hello. Si se intenta la operación REST en un archivo donde un cliente SMB tiene bloqueado el archivo de Hola Hola servicio REST devolverá el código de estado 409 (conflicto) con código de error SharingViolation.  

Cuando un cliente SMB abre un archivo para eliminarlo, marca archivo hello como pendiente de eliminación hasta que todos los otros clientes SMB se cierran los identificadores abiertos en ese archivo. Mientras un archivo se marca como eliminación pendiente, cualquier operación REST en ese archivo devolverá el código de estado 409 (Conflicto) con el código de error SMBDeletePending. No se devuelve el código de estado 404 (no encontrado) ya que es posible que Hola Hola de tooremove de cliente SMB archivo Hola de eliminación marca tooclosing previa está pendiente. En otras palabras, solo se espera que el código de estado 404 (no encontrado) cuando se ha quitado el archivo hello. Tenga en cuenta que mientras un archivo está en un SMB estado pendiente de eliminación, no se incluirá en hello que enumerar archivos de resultados. Además, tenga en cuenta que las operaciones de REST eliminar archivo y directorio eliminar de REST de Hola se confirman de forma automática y no dan lugar a un estado de eliminación pendiente.  

Para más información, consulte:  

* [Administración de bloqueos de archivo](http://msdn.microsoft.com/library/azure/dn194265.aspx)  

## <a name="summary-and-next-steps"></a>Resumen y pasos siguientes
Hello ha sido el servicio de almacenamiento de Microsoft Azure diseñado necesidades de hello toomeet de aplicaciones en línea más complejas de hello sin obligar a los desarrolladores toocompromise o nueva consideración de diseño clave suposiciones como simultaneidad y coherencia de datos que se vuelven a tootake Para conceder.  

Para hello completar la aplicación de ejemplo que se hace referencia en este blog:  

* [Administración de simultaneidad con Almacenamiento de Azure: aplicación de ejemplo](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114)  

Para obtener más información acerca de Almacenamiento de Azure, consulte:  

* [Página principal de Almacenamiento de Microsoft Azure](https://azure.microsoft.com/services/storage/)
* [Introducción tooAzure almacenamiento](storage-introduction.md)
* Introducción al almacenamiento para [Blob](../blobs/storage-dotnet-how-to-use-blobs.md), [Table](../../cosmos-db/table-storage-how-to-use-dotnet.md), [Queues](../storage-dotnet-how-to-use-queues.md) y [Files](../storage-dotnet-how-to-use-files.md)
* Arquitectura de almacenamiento. [Azure Storage: un servicio de almacenamiento en nube altamente disponible con coherencia fuerte](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

