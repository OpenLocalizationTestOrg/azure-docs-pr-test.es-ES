---
title: Cifrado del lado de aaaClient con .NET para almacenamiento de Microsoft Azure | Documentos de Microsoft
description: "Hola biblioteca de cliente de almacenamiento de Azure para .NET admite cifrado en el cliente y la integración con el almacén de claves de Azure para lograr la máxima seguridad para las aplicaciones de almacenamiento de Azure."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: becfccca-510a-479e-a798-2044becd9a64
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c09246f43801e17aff96ea453182d11ffbf5e420
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-and-azure-key-vault-for-microsoft-azure-storage"></a>Cifrado del lado de cliente y Almacén de claves de Azure para el Almacenamiento de Microsoft Azure
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>Información general
Hola [biblioteca de cliente de almacenamiento de Azure para el paquete Nuget de .NET](https://www.nuget.org/packages/WindowsAzure.Storage) admite el cifrado de datos dentro de las aplicaciones cliente antes de cargar tooAzure almacenamiento y descifrar los datos mientras se descargaba toohello cliente. biblioteca de Hello también admite la integración con [el almacén de claves de Azure](https://azure.microsoft.com/services/key-vault/) para administración de claves de cuenta de almacenamiento.

Para obtener un tutorial paso a paso que le guíe por el proceso de Hola de cifrado de blobs mediante el cifrado en el cliente y el almacén de claves de Azure, consulte [blobs en almacenamiento de Azure de Microsoft con el almacén de claves de Azure cifrar y descifrar](../blobs/storage-encrypt-decrypt-blobs-key-vault.md).

Para el cifrado del lado cliente con Java, consulte el artículo [Cifrado del lado cliente con Java para el Almacenamiento de Microsoft Azure](storage-client-side-encryption-java.md).

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>Cifrado y descifrado mediante la técnica de sobres de Hola
Hola de los procesos de cifrado y descifrado sigue técnica de sobres de Hola.

### <a name="encryption-via-hello-envelope-technique"></a>Cifrado a través de la técnica de sobres de Hola
Cifrado a través de la técnica de sobres de hello funciona en hello siguiente forma:

1. biblioteca de cliente de almacenamiento de Azure de Hello genera una clave de cifrado de contenido (CEK), que es una clave simétrica de un solo uso.
2. Los datos de usuario se cifran mediante esta CEK.
3. Hello CEK se incluye después (cifrada) con clave de cifrado de claves de Hola (de claves KEK). Hola KEK se identifica mediante un identificador de clave y puede ser un par de claves asimétricas o una clave simétrica y se puede administrar de forma local o almacenado en los almacenes de claves de Azure.
   
    biblioteca de cliente de almacenamiento de Hello propio nunca tiene acceso tooKEK. biblioteca de Hello invoca el algoritmo de encapsulado de clave de hello proporcionada por el almacén de claves. Los usuarios pueden elegir toouse proveedores personalizados para clave ajuste/desencapsulación si lo desea.

4. Hola datos cifrados están, a continuación, cargar el servicio de almacenamiento de Azure toohello. Hola clave ajustada junto con algunos metadatos de cifrado adicional se almacenan como metadatos (en un blob) o se interpolan con datos de hello cifrada (cola de mensajes y entidades de tabla).

### <a name="decryption-via-hello-envelope-technique"></a>Descifrado mediante la técnica de sobres de Hola
Descifrado mediante la técnica de sobres de hello funciona en hello siguiente forma:

1. biblioteca de cliente de Hola se da por supuesto que el usuario Hola administra Hola clave cifrado de claves (KEK) ya sea localmente o en los almacenes de claves de Azure. Hola usuario no necesita clave específica de tooknow Hola que se usó para el cifrado. En su lugar, una resolución de clave que se resuelve tookeys diferentes identificadores de clave se puede configurar y usar.
2. biblioteca de cliente de Hello descarga los datos de hello cifrado junto con cualquier material de cifrado que se almacena en el servicio de Hola.
3. clave de cifrado de contenido ajustada Hello (CEK) es (descifran) con desempaquetarse Hola claves de cifrado de claves (KEK). Aquí una vez más, biblioteca de cliente de hello no tiene acceso tooKEK. Simplemente invoca Hola personalizado o algoritmo desencapsulación del proveedor de almacén de claves.
4. Hola contenido clave de cifrado (CEK) es, a continuación, utiliza datos de usuario de toodecrypt Hola cifrado.

## <a name="encryption-mechanism"></a>Mecanismo de cifrado
usa la biblioteca de cliente de almacenamiento de Hello [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) en los datos de usuario de tooencrypt de orden. En concreto, emplea el modo [Cipher Block Chaining (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) con AES. Cada servicio funciona de forma ligeramente diferente, por lo que describiremos aquí cada uno de ellos.

### <a name="blobs"></a>Blobs
biblioteca de cliente de Hello actualmente admite el cifrado de todo blobs solo. En concreto, se admite el cifrado cuando los usuarios usen hello **UploadFrom*** métodos o hello **OpenWrite** método. En el caso de las descargas, se admiten tanto las descargas de intervalo como las completas.

Durante el cifrado, la biblioteca de cliente de hello generará un Vector de inicialización aleatorio (IV) de 16 bytes, junto con una clave de cifrado aleatoria de contenido (CEK) de 32 bytes y realizar el cifrado de sellado de datos de blob de hello con esta información. Hola ajustó CEK y algunos metadatos de cifrado adicional, a continuación, se almacenan como metadatos junto con el blob cifrado de hello en el servicio de hello del blob.

> [!WARNING]
> Si está modificando o cargar sus propios metadatos del blob de hello, deberá tooensure que estos metadatos se conservan. Si va a cargar nuevos metadatos sin estos metadatos, hello CEK ajustada, IV y otros metadatos se perderán y el contenido de blob Hola nunca pueda recuperarse nuevo.
> 
> 

Descargar un blob cifrado implica recuperando Hola contenido de blob completo hello mediante hello **DownloadTo***/**BlobReadStream** comodidad métodos. Hola CEK ajustada se desempaqueta y se utiliza junto con hello IV (almacenados como metadatos del blob en este caso) tooreturn Hola descifrado datos toohello a los usuarios.

Descargar un intervalo arbitrario (**DownloadRange*** métodos) en hello blob cifrado implica el ajuste del rango de hello proporcionados por los usuarios en orden tooget una pequeña cantidad de datos adicionales que pueden ser utilizado toosuccessfully descifrar Hola intervalo solicitado.

Todos los tipos de blobs (blobs en bloques, blobs de anexión) se pueden cifrar y descifrar usando este esquema.

### <a name="queues"></a>Colas
Puesto que la cola de mensajes puede ser de cualquier formato, biblioteca de cliente de hello define un formato personalizado que incluye Hola Vector de inicialización (IV) y la clave de cifrado de contenido cifrada de hello (CEK) en el texto del mensaje de Hola.

Durante el cifrado, la biblioteca de cliente de hello genera un vector de inicialización aleatorio de 16 bytes junto con una CEK aleatoria de 32 bytes y realiza el cifrado de sellado de texto del mensaje de cola de hello con esta información. Hola ajustó CEK y algunos metadatos de cifrado adicional, a continuación, se agregan toohello la cola cifrado de mensajes. Este mensaje modificado (se muestra a continuación) se almacena en el servicio de Hola.

    <MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>

Durante el descifrado, clave ajustada Hola se extrae del mensaje de la cola de Hola y desempaqueta. Hola IV también está extraído del mensaje de la cola de Hola y utilizar junto con datos del mensaje de Hola desempaqueta toodecrypt clave Hola cola. Tenga en cuenta que metadatos de cifrado de hello están pequeño (en bytes) 500, por lo que mientras cuentan para el límite de 64KB de Hola para un mensaje de la cola, el impacto de hello debería ser fácil de administrar.

### <a name="tables"></a>Tablas
Hola cliente biblioteca admite el cifrado de propiedades de entidad para la inserción de operaciones y reemplazo.

> [!NOTE]
> Las operaciones de combinación no se admiten actualmente. Puesto que un subconjunto de propiedades se puede haber cifrado previamente mediante una clave diferente, simplemente combinar nuevas propiedades de Hola y actualizar metadatos de hello producirá pérdida de datos. Combinar cualquiera requiere servicio adicional de realizar llamadas entidad preexistente de hello tooread del servicio de hello, o mediante una clave nueva por cada propiedad, los cuales no son adecuados por motivos de rendimiento.
> 
> 

El cifrado de datos de tabla funciona de la siguiente forma:  

1. Los usuarios especificar Hola propiedades toobe cifrado.
2. biblioteca de cliente de Hello genera un Vector de inicialización aleatorio (IV) de 16 bytes junto con una clave de cifrado aleatoria de contenido (CEK) de 32 bytes para cada entidad y realiza el cifrado de sellado en toobe de las propiedades individuales de hello cifrada al derivar un nuevo vector de inicialización por propiedad. propiedad Hola cifrada se almacena como datos binarios.
3. Hola ajustó CEK y algunos metadatos de cifrado adicional, a continuación, se almacenan como dos propiedades reservadas adicionales. Hola primera propiedad reservada (_ClientEncryptionMetadata1) es una propiedad de cadena que contiene información de hello sobre IV, la versión y la clave ajustada. Hola segunda propiedad reservada (_ClientEncryptionMetadata2) es una propiedad binaria que contiene información de hello sobre propiedades de Hola que estén cifrados. información de Hello en esta segunda propiedad (_ClientEncryptionMetadata2) está cifrada.
4. Pagar toothese reservadas propiedades adicionales necesarias para el cifrado, los usuarios ahora pueden tener sólo 250 propiedades personalizadas en lugar de 252. tamaño total de Hola de entidad de hello debe ser inferior a 1 MB.

Tenga en cuenta que solo se pueden cifrar las propiedades de cadena. Si hay otros tipos de propiedades toobe cifrado, deben ser toostrings convertido. cadenas de Hello cifrado se almacenan en el servicio de hello como propiedades binarias y se convierten toostrings atrás tras la descodificación.

Para las tablas, además toohello directiva de cifrado, los usuarios deben especificar Hola propiedades toobe cifrado. Para ello, pueden especificar un atributo EncryptProperty (para las entidades POCO que se derivan de TableEntity) o una resolución de cifrado en las opciones de solicitud. Una resolución de cifrado es un delegado que toma una clave de partición, una clave de fila y un nombre de propiedad y devuelve un valor booleano que indica si se debe cifrar dicha propiedad. Durante el cifrado, biblioteca de cliente de hello utilizará esta toodecide información si se debe cifrar una propiedad al escribir el cable toohello. delegado de Hello también proporciona posibilidad de Hola de lógica de alrededor de cómo se cifran las propiedades. (Por ejemplo, si el valor es X, hay que cifrar la propiedad A; en caso contrario, hay que cifrar las propiedades A y B). Tenga en cuenta que TI es tooprovide no es necesario que esta información al leer o consultar entidades.

### <a name="batch-operations"></a>Operaciones por lotes
En operaciones por lotes, hello KEK mismo se usará en todas las filas de hello en esa operación por lotes porque la biblioteca de cliente de hello sólo permite un objeto de opciones (y por lo tanto, una directiva/KEK) por operación por lotes. Sin embargo, la biblioteca de cliente de Hola generará internamente un nuevo vector de inicialización aleatorio y una CEK aleatorio por cada fila en lote Hola. Los usuarios también pueden elegir tooencrypt diferentes propiedades para cada operación de lote de hello mediante la definición de este comportamiento de resolución de cifrado de Hola.

### <a name="queries"></a>Consultas
operaciones de consulta de tooperform, debe especificar un solucionador de clave que es capaz de tooresolve todos Hola claves Hola conjunto de resultados. Si una entidad incluida en el resultado de la consulta de hello no se puede resolver tooa proveedor, biblioteca de cliente de Hola producirá un error. Para cualquier consulta que lleva a cabo proyecciones del lado servidor, la biblioteca de cliente de hello agregará propiedades de metadatos de cifrado especial de hello (_ClientEncryptionMetadata1 y _ClientEncryptionMetadata2) por columnas de toohello seleccionado de forma predeterminada.

## <a name="azure-key-vault"></a>Azure Key Vault
El Almacén de claves de Azure ayuda a proteger claves criptográficas y secretos usados por servicios y aplicaciones en la nube. Mediante el uso del Almacén de claves de Azure, los usuarios pueden cifrar claves y secretos (por ejemplo claves de autenticación, claves de cuenta de almacenamiento, claves de cifrado de datos, archivos .PFX y contraseñas) usando claves que están protegidas por módulos de seguridad de hardware (HSM). Para obtener más información, consulte [¿Qué es el Almacén de claves de Azure?](../../key-vault/key-vault-whatis.md)

biblioteca de cliente de almacenamiento de Hello utiliza la biblioteca de núcleo de almacén de claves de hello en orden tooprovide un marco común a través de Azure para administrar las claves. Los usuarios también obtendrán la ventaja adicional de hello del uso de la biblioteca de extensiones del almacén de claves de Hola. biblioteca de extensiones de Hello proporciona funcionalidad útil alrededor de sencilla y sin problemas Symmetric/RSA local y proveedores de clave en la nube, así como con la agregación y almacenamiento en caché.

### <a name="interface-and-dependencies"></a>Interfaz y dependencias
Hay tres paquetes del Almacén de claves:

* Microsoft.Azure.KeyVault.Core contiene Hola IKey y IKeyResolver. Es un paquete pequeño sin dependencias. biblioteca de cliente de almacenamiento de Hola para .NET define como una dependencia.
* Microsoft.Azure.KeyVault contiene Hola de cliente de REST del almacén de claves.
* Microsoft.Azure.KeyVault.Extensions contiene el código de extensión que incluye implementaciones de algoritmos criptográficos, además de una RSAKey y una SymmetricKey. Depende de los espacios de nombres de KeyVault y los núcleos de Hola y proporciona funcionalidad toodefine un solucionador de agregado (cuando los usuarios desean toouse varios proveedores de claves) y una resolución de clave de almacenamiento en caché. Aunque biblioteca de cliente de almacenamiento de hello no directamente dependen de este paquete, si los usuarios desea toostore de almacén de claves de Azure toouse sus claves o toouse Hola Hola de tooconsume de extensiones de almacén de claves local y proveedores de servicios criptográficos en la nube, necesitará este paquete.

El Almacén de claves está diseñado para claves maestras de gran valor. Por su parte, los valores de limitación por cada Almacén de claves se diseñan teniendo en cuenta este aspecto. Al realizar el cifrado en el cliente con el almacén de claves, modelo preferido de hello es toouse master las claves simétricas almacenadas como secretos en el almacén de claves y almacenado en caché localmente. Los usuarios deben hacer siguiente hello:

1. Crear un secreto sin conexión y cargarlo tooKey almacén.
2. Usar identificador de base del secreto de Hola como un parámetro tooresolve Hola versión actual de secreto de hello para el cifrado y almacenar en caché localmente esta información. Use CachingKeyResolver para almacenar en caché; los usuarios es tooimplement no esperado en lógica de su propio almacenamiento en caché.
3. Utilizar a la resolución de caché hello como una entrada al crear la directiva de cifrado de Hola.

Encontrará más información sobre el uso del almacén de claves en hello [ejemplos de código de cifrado](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples).

## <a name="best-practices"></a>Prácticas recomendadas
Compatibilidad con el cifrado está disponible solo en la biblioteca de cliente de almacenamiento de Hola para. NET. Windows Phone y Windows en tiempo de ejecución no admiten actualmente cifrado.

> [!IMPORTANT]
> Tenga en cuenta estos puntos importantes al usar el cifrado del lado del cliente:
> 
> * Cuando tooan leer o escribir los cifra blob, usar comandos de carga de blob completo y comandos de descarga de blobs de intervalo/todo. Evite escribir tooan blob cifrado mediante operaciones de protocolo como bloque Put, coloque la lista de bloqueados, escribir páginas, borrar páginas o anexión de bloques; en caso contrario, puede dañar blob cifrado de Hola y que no sea legible.
> * Para las tablas, existe una restricción similar. Ser toonot cuidado actualización cifrado propiedades sin actualizar los metadatos de cifrado de Hola.
> * Si establece metadatos en blob cifrado de hello, pueden sobrescribir metadatos relacionados con el cifrado de hello necesarios para el descifrado, puesto que no se suma al establecer metadatos. Esto también se aplica a las instantáneas: evite la especificación de metadatos durante la creación de una instantánea de un blob cifrado. Si se deben establecer los metadatos, que seguro hello toocall **FetchAttributes** tooget primer método Hola metadatos de cifrado actual y evitar operaciones de escritura simultáneas metadatos mientras está habilitada.
> * Habilitar hello **RequireEncryption** propiedad opciones de solicitud de hello predeterminadas para los usuarios que deben trabajar solo con los datos cifrados. Vea a continuación para obtener más información.
> 
> 

## <a name="client-api--interface"></a>Interfaz/API de cliente
Al crear un objeto de EncryptionPolicy, los usuarios pueden proporcionar solo una clave (implementación de IKey), solo una resolución (implementación de IKeyResolver) o ambas. IKey es hello básico tipo de clave que se identifica mediante un identificador de clave y que proporciona la lógica de Hola para ajuste/desencapsulación. IKeyResolver es tooresolve usa una clave durante el proceso de descifrado de Hola. Define un método ResolveKey que devuelve un IKey concreto (identificador de clave). Esto proporciona a los usuarios Hola capacidad toochoose entre varias claves que se administran en varias ubicaciones.

* Para el cifrado, se utiliza siempre la clave de Hola y ausencia de Hola de una clave se producirá un error.
* Para el descifrado:
  * resolución de clave de Hola se invoca si se especifica la clave de hello tooget. Si la resolución de Hola se especifica, pero no tiene una asignación para el identificador de clave de hello, se produce un error.
  * Si no se especifica la resolución, pero se especifica una clave, clave de Hola se usa si su identificador coincide con el identificador de clave de hello necesario. Si no coincide con el identificador de hello, se produce un error.

Hola [ejemplos de cifrado](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) muestran un escenario de extremo a extremo más detallado para blobs, colas y tablas, junto con la integración del almacén de claves.

### <a name="requireencryption-mode"></a>Modo RequireEncryption
Los usuarios pueden habilitar opcionalmente un modo de operación en el que se deben cifrar todas las cargas y descargas. En este modo, se producirá un error de los intentos de tooupload datos sin un cifrado directiva o descarga los datos que no se cifran en el servicio de hello en cliente hello. Hola **RequireEncryption** propiedad de objeto de opciones de solicitud de hello controla este comportamiento. Si la aplicación, se cifrarán todos los objetos almacenados en el almacenamiento de Azure, puede establecer hello **RequireEncryption** propiedad opciones de solicitud de hello predeterminadas para el objeto de cliente de servicio de Hola. Por ejemplo, establecer **CloudBlobClient.DefaultRequestOptions.RequireEncryption** demasiado**true** toorequire cifrado para todas las operaciones de blob se realiza a través de ese objeto de cliente.

### <a name="blob-service-encryption"></a>Cifrado del servicio de blobs
Crear un **BlobEncryptionPolicy** de objeto y establecer en Opciones de solicitud de hello (por API o en un nivel de cliente mediante el uso de **DefaultRequestOptions**). Todo lo demás se controlarán mediante la biblioteca de cliente de hello internamente.

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 BlobEncryptionPolicy policy = new BlobEncryptionPolicy(key, null);

 // Set hello encryption policy on hello request options.
 BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

 // Upload hello encrypted contents toohello blob.
 blob.UploadFromStream(stream, size, null, options, null);

 // Download and decrypt hello encrypted contents from hello blob.
 MemoryStream outputStream = new MemoryStream();
 blob.DownloadToStream(outputStream, null, options, null);
```

### <a name="queue-service-encryption"></a>Cifrado del servicio Cola
Crear un **QueueEncryptionPolicy** de objeto y establecer en Opciones de solicitud de hello (por API o en un nivel de cliente mediante el uso de **DefaultRequestOptions**). Todo lo demás se controlarán mediante la biblioteca de cliente de hello internamente.

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 QueueEncryptionPolicy policy = new QueueEncryptionPolicy(key, null);

 // Add message
 QueueRequestOptions options = new QueueRequestOptions() { EncryptionPolicy = policy };
 queue.AddMessage(message, null, null, options, null);

 // Retrieve message
 CloudQueueMessage retrMessage = queue.GetMessage(null, options, null);
```

### <a name="table-service-encryption"></a>Cifrado del servicio Tabla
Además toocreating una directiva de cifrado y la configuración de opciones de solicitud, se debe especificar un **EncryptionResolver** en **TableRequestOptions**, o establezca el atributo Hola [EncryptProperty] en entidad de Hola.

#### <a name="using-hello-resolver"></a>Utilizar al Solucionador de Hola

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 TableEncryptionPolicy policy = new TableEncryptionPolicy(key, null);

 TableRequestOptions options = new TableRequestOptions()
 {
    EncryptionResolver = (pk, rk, propName) =>
     {
        if (propName == "foo")
         {
            return true;
         }
         return false;
     },
     EncryptionPolicy = policy
 };

 // Insert Entity
 currentTable.Execute(TableOperation.Insert(ent), options, null);

 // Retrieve Entity
 // No need toospecify an encryption resolver for retrieve
 TableRequestOptions retrieveOptions = new TableRequestOptions()
 {
    EncryptionPolicy = policy
 };

 TableOperation operation = TableOperation.Retrieve(ent.PartitionKey, ent.RowKey);
 TableResult result = currentTable.Execute(operation, retrieveOptions, null);
```

#### <a name="using-attributes"></a>Uso de los atributos
Como se mencionó anteriormente, si la entidad de hello implementa TableEntity, a continuación, propiedades de Hola se pueden decorar con atributo Hola [EncryptProperty] en lugar de especificar hello **EncryptionResolver**.

```csharp
[EncryptProperty]
 public string EncryptedProperty1 { get; set; }
```

## <a name="encryption-and-performance"></a>Cifrado y rendimiento
Tenga en cuenta que el cifrado de sus resultados de datos de almacenamiento da lugar a la sobrecarga de rendimiento adicional. Hola contenido deben generarse clave y un IV, se debe cifrar el propio contenido hello y metadatos adicionales deben con formato y cargarse. Esta sobrecarga variará según la cantidad de Hola de datos está cifrados. Se recomienda que los clientes prueben siempre sus aplicaciones para obtener un rendimiento durante el desarrollo.

## <a name="next-steps"></a>Pasos siguientes
* [Tutorial: Cifrado y descifrado de blobs en Almacenamiento de Microsoft Azure con Almacén de claves de Azure](../blobs/storage-encrypt-decrypt-blobs-key-vault.md)
* Descargar hello [biblioteca de cliente de almacenamiento de Azure para el paquete NuGet de .NET](https://www.nuget.org/packages/WindowsAzure.Storage)
* Descargar hello Azure Key Vault NuGet [Core](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core/), [cliente](http://www.nuget.org/packages/Microsoft.Azure.KeyVault/), y [extensiones](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions/) paquetes  
* Visite hello [documentación del almacén de claves de Azure](../../key-vault/key-vault-whatis.md)
