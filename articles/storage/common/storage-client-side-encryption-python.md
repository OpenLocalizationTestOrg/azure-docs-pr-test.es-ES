---
title: Cifrado del lado de aaaClient con Python para almacenamiento de Microsoft Azure | Documentos de Microsoft
description: "Hola biblioteca de cliente de almacenamiento de Azure para Python es compatible con el cifrado de cliente para lograr la máxima seguridad para las aplicaciones de almacenamiento de Azure."
services: storage
documentationcenter: python
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: f9bf7981-9948-4f83-8931-b15679a09b8a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: 3a52b64f93daf85a55308f8a4bee9c98b2315d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-with-python-for-microsoft-azure-storage"></a>Cifrado del lado cliente con Python para Almacenamiento de Microsoft Azure
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>Información general
Hola [biblioteca de cliente de almacenamiento de Azure para Python](https://pypi.python.org/pypi/azure-storage) admite el cifrado de datos dentro de las aplicaciones cliente antes de cargar tooAzure almacenamiento y descifrar los datos mientras se descargaba toohello cliente.

> [!NOTE]
> biblioteca de Python de almacenamiento de Azure Hola está en vista previa.
> 
> 

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>Cifrado y descifrado mediante la técnica de sobres de Hola
Hola de los procesos de cifrado y descifrado sigue técnica de sobres de Hola.

### <a name="encryption-via-hello-envelope-technique"></a>Cifrado a través de la técnica de sobres de Hola
Cifrado a través de la técnica de sobres de hello funciona en hello siguiente forma:

1. biblioteca de cliente de almacenamiento de Azure de Hello genera una clave de cifrado de contenido (CEK), que es una clave simétrica de un solo uso.
2. Los datos de usuario se cifran mediante esta CEK.
3. Hello CEK se incluye después (cifrada) con clave de cifrado de claves de Hola (de claves KEK). Hola KEK se identifica mediante un identificador de clave y puede tener un par de claves asimétricas o una clave simétrica, que se administra localmente.
   biblioteca de cliente de almacenamiento de Hello propio nunca tiene acceso tooKEK. biblioteca de Hello invoca clave Hola algoritmo proporcionada por hello KEK de ajuste. Los usuarios pueden elegir toouse proveedores personalizados para clave ajuste/desencapsulación si lo desea.
4. Hola datos cifrados están, a continuación, cargar el servicio de almacenamiento de Azure toohello. Hola clave ajustada junto con algunos metadatos de cifrado adicional se almacenan como metadatos (en un blob) o se interpolan con datos de hello cifrada (cola de mensajes y entidades de tabla).

### <a name="decryption-via-hello-envelope-technique"></a>Descifrado mediante la técnica de sobres de Hola
Descifrado mediante la técnica de sobres de hello funciona en hello siguiente forma:

1. biblioteca de cliente de Hola se da por supuesto que el usuario Hola administra localmente Hola clave cifrado de claves (KEK). Hola usuario no necesita clave específica de tooknow Hola que se usó para el cifrado. En su lugar, una resolución de clave, que se resuelve tookeys diferentes identificadores de clave, se puede configurar y usar.
2. biblioteca de cliente de Hello descarga los datos de hello cifrado junto con cualquier material de cifrado que se almacena en el servicio de Hola.
3. clave de cifrado de contenido ajustada Hello (CEK) es (descifran) con desempaquetarse Hola claves de cifrado de claves (KEK). Aquí una vez más, biblioteca de cliente de hello no tiene acceso tooKEK. Simplemente invoca algoritmo desencapsulación del proveedor personalizado de Hola.
4. Hola contenido clave de cifrado (CEK) es, a continuación, utiliza datos de usuario de toodecrypt Hola cifrado.

## <a name="encryption-mechanism"></a>Mecanismo de cifrado
usa la biblioteca de cliente de almacenamiento de Hello [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) en los datos de usuario de tooencrypt de orden. En concreto, emplea el modo [Cipher Block Chaining (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) con AES. Cada servicio funciona de forma ligeramente diferente, por lo que describiremos aquí cada uno de ellos.

### <a name="blobs"></a>Blobs
biblioteca de cliente de Hello actualmente admite el cifrado de todo blobs solo. En concreto, se admite el cifrado cuando los usuarios usen hello **crear*** métodos. En el caso de las descargas, se admiten tanto las descargas de intervalo como las completas, y está disponible la paralelización tanto de la carga como de la descarga.

Durante el cifrado, la biblioteca de cliente de hello generará un Vector de inicialización aleatorio (IV) de 16 bytes, junto con una clave de cifrado aleatoria de contenido (CEK) de 32 bytes y realizar el cifrado de sellado de datos de blob de hello con esta información. Hola ajustó CEK y algunos metadatos de cifrado adicional, a continuación, se almacenan como metadatos junto con el blob cifrado de hello en el servicio de hello del blob.

> [!WARNING]
> Si está modificando o cargar sus propios metadatos del blob de hello, deberá tooensure que estos metadatos se conservan. Si va a cargar nuevos metadatos sin estos metadatos, Hola CEK ajustada, se perderán IV y otros metadatos y contenido de blob de hello nunca pueda recuperarse nuevo.
> 
> 

Descargar un blob cifrado implica recuperando Hola contenido de blob completo hello mediante hello **obtener*** métodos útiles. Hola CEK ajustada se desempaqueta y se utiliza junto con hello IV (almacenados como metadatos del blob en este caso) tooreturn Hola descifrado datos toohello a los usuarios.

Descargar un intervalo arbitrario (**obtener*** pasan métodos con parámetros de rango) en hello blob cifrado implica el ajuste del rango de hello proporcionado por los usuarios en orden tooget una pequeña cantidad de datos adicionales que se pueden usar Hola de descifrar toosuccessfully intervalo solicitado.

Los blobs en bloques y los blobs en páginas solo se pueden cifrar y descifrar usando este esquema. Actualmente, no se admite el cifrado de blobs en anexos.

### <a name="queues"></a>Colas
Puesto que la cola de mensajes puede ser de cualquier formato, biblioteca de cliente de hello define un formato personalizado que incluye Hola Vector de inicialización (IV) y la clave de cifrado de contenido cifrada de hello (CEK) en el texto del mensaje de Hola.

Durante el cifrado, la biblioteca de cliente de hello genera un vector de inicialización aleatorio de 16 bytes junto con una CEK aleatoria de 32 bytes y realiza el cifrado de sellado de texto del mensaje de cola de hello con esta información. Hola ajustó CEK y algunos metadatos de cifrado adicional, a continuación, se agregan toohello la cola cifrado de mensajes. Este mensaje modificado (se muestra a continuación) se almacena en el servicio de Hola.

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

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
3. Hola ajustó CEK y algunos metadatos de cifrado adicional, a continuación, se almacenan como dos propiedades reservadas adicionales. Hola primero la propiedad reservada (\_ClientEncryptionMetadata1) es una propiedad de cadena que contiene información de hello sobre IV, la versión y la clave ajustada. Hola propiedad reservada en segundo lugar (\_ClientEncryptionMetadata2) es una propiedad binaria que contiene información de hello sobre propiedades de Hola que estén cifrados. Hola información en esta segunda propiedad (\_ClientEncryptionMetadata2) está cifrada.
4. Pagar toothese reservadas propiedades adicionales necesarias para el cifrado, los usuarios ahora pueden tener sólo 250 propiedades personalizadas en lugar de 252. tamaño total de Hola de entidad de hello debe ser inferior a 1MB.
   
   Tenga en cuenta que solo se pueden cifrar las propiedades de cadena. Si hay otros tipos de propiedades toobe cifrado, deben ser toostrings convertido. cadenas de Hello cifrado se almacenan en el servicio de hello como propiedades binarias y se convierten toostrings atrás (las cadenas sin formato, no EntityProperties con tipo EdmType.STRING) después de descifrado.
   
   Para las tablas, además toohello directiva de cifrado, los usuarios deben especificar Hola propiedades toobe cifrado. Esto puede realizarse almacenando estas propiedades en objetos TableEntity con tooEdmType.STRING de conjunto de tipo hello y cifrar encryption_resolver_function hello en el objeto de hello tableservice del tootrue o la configuración del conjunto. Una resolución de cifrado es una función que toma una clave de partición, una clave de fila y un nombre de propiedad y devuelve un valor booleano que indica si se debe cifrar dicha propiedad. Durante el cifrado, biblioteca de cliente de hello utilizará esta toodecide información si se debe cifrar una propiedad al escribir el cable toohello. delegado de Hello también proporciona posibilidad de Hola de lógica de alrededor de cómo se cifran las propiedades. (Por ejemplo, si el valor es X, hay que cifrar la propiedad A; en caso contrario, hay que cifrar las propiedades A y B). Tenga en cuenta que TI es tooprovide no es necesario que esta información al leer o consultar entidades.

### <a name="batch-operations"></a>Operaciones por lotes
Una directiva de cifrado aplica a filas de tooall en el lote de Hola. biblioteca de cliente de Hello internamente generará un nuevo vector de inicialización aleatorio y una CEK aleatorio por cada fila en el lote de Hola. Los usuarios también pueden elegir tooencrypt diferentes propiedades para cada operación de lote de hello mediante la definición de este comportamiento de resolución de cifrado de Hola.
Si un lote se crea como un administrador de contexto a través del método de hello tableservice batch(), directiva de cifrado de hello tableservice estarán automáticamente por lotes toohello aplicada. Si un lote se crea explícitamente llamando al constructor de hello, directiva de cifrado de hello debe pasarse como un parámetro e izquierda sin modificar la duración de Hola de lote de Hola.
Tenga en cuenta que las entidades están cifradas tal y como se ha insertado en el lote de hello mediante Directiva de cifrado del lote de hello (entidades no están cifradas en tiempo de Hola de confirmación de lote de hello mediante Directiva de cifrado de hello tableservice).

### <a name="queries"></a>Consultas
operaciones de consulta de tooperform, debe especificar un solucionador de clave que es capaz de tooresolve todos Hola claves Hola conjunto de resultados. Si una entidad incluida en el resultado de la consulta de hello no se puede resolver tooa proveedor, biblioteca de cliente de Hola producirá un error. Para cualquier consulta que lleva a cabo proyecciones del lado servidor, la biblioteca de cliente de hello agregará propiedades de metadatos de cifrado especial de hello (\_ClientEncryptionMetadata1 y \_ClientEncryptionMetadata2) de forma predeterminada toohello seleccionan columnas .

> [!IMPORTANT]
> Tenga en cuenta estos puntos importantes al usar el cifrado del lado del cliente:
> 
> * Cuando tooan leer o escribir los cifra blob, usar comandos de carga de blob completo y comandos de descarga de blobs de intervalo/todo. Evite escribir tooan blob cifrado mediante operaciones de protocolo como bloque Put, coloque la lista de bloqueados, escribir páginas o borrar páginas; en caso contrario, puede dañar blob cifrado de Hola y que no sea legible.
> * Para las tablas, existe una restricción similar. Ser toonot cuidado actualización cifrado propiedades sin actualizar los metadatos de cifrado de Hola.
> * Si establece metadatos en blob cifrado de hello, pueden sobrescribir metadatos relacionados con el cifrado de hello necesarios para el descifrado, puesto que no se suma al establecer metadatos. Esto también se aplica a las instantáneas: evite la especificación de metadatos durante la creación de una instantánea de un blob cifrado. Si se deben establecer los metadatos, que seguro hello toocall **get_blob_metadata** tooget primer método Hola metadatos de cifrado actual y evitar operaciones de escritura simultáneas metadatos mientras está habilitada.
> * Habilitar hello **require_encryption** indicador de objeto de servicio de Hola para los usuarios que deben trabajar solo con los datos cifrados. Vea a continuación para obtener más información.
> 
> 

biblioteca de cliente de almacenamiento de Hola espera Hola proporciona KEK y resolución clave hello tooimplement siguiendo la interfaz. [Almacén de claves de Azure](https://azure.microsoft.com/services/key-vault/) con la administración de KEK de Python está pendiente y se integrará a esta biblioteca cuando se complete.

## <a name="client-api--interface"></a>Interfaz/API de cliente
Después de crear un objeto de servicio de almacenamiento (es decir, blockblobservice), el usuario Hola puede asignar valores toohello campos que constituyen una directiva de cifrado: key_encryption_key, key_resolver_function y require_encryption. Los usuarios pueden proporcionar solo una KEK, solo una resolución o ambos. key_encryption_key es hello básico tipo de clave que se identifica mediante un identificador de clave y que proporciona la lógica de Hola para ajuste/desencapsulación. key_resolver_function es tooresolve usa una clave durante el proceso de descifrado de Hola. Devuelve una KEK válida en función de un identificador de clave. Esto proporciona a los usuarios Hola capacidad toochoose entre varias claves que se administran en varias ubicaciones.

Hola KEK debe implementar siguiente Hola métodos toosuccessfully cifrar datos:

* wrap_key(CEK): Hola ajusta especificado CEK (bytes) mediante un algoritmo de elección del usuario de Hola. Hola devuelve clave encapsulada.
* get_key_wrap_algorithm(): algoritmo de hello devuelve usa claves de toowrap.
* get_kid(): identificador de clave de cadena de Hola y devuelve para esta KEK.
  Hola KEK debe implementar Hola métodos toosuccessfully descifrar datos siguientes:
* unwrap_key (cek, el algoritmo): devuelve Hola desempaqueta formada por hello especificado CEK mediante el algoritmo de cadena especificada de Hola.
* get_kid(): devuelve un id. de clave de cadena de esta KEK.

resolución clave Hola debe implementar al menos un método que, dados un identificador de clave, devuelve Hola KEK implementación Hola interfaz correspondiente anterior. Solo este método es toobe toohello key_resolver_function propiedad en el objeto de servicio de hello asignado.

* Para el cifrado, se utiliza siempre la clave de Hola y ausencia de Hola de una clave se producirá un error.
* Para el descifrado:
  
  * resolución de clave de Hola se invoca si se especifica la clave de hello tooget. Si la resolución de Hola se especifica, pero no tiene una asignación para el identificador de clave de hello, se produce un error.
  * Si no se especifica la resolución, pero se especifica una clave, clave de Hola se usa si su identificador coincide con el identificador de clave de hello necesario. Si no coincide con el identificador de hello, se produce un error.
    
    Hola ejemplos de cifrado en azure.storage.samples <fix URL>muestra un escenario de extremo a extremo más detallado para blobs, colas y tablas.
      Implementaciones de ejemplo de Hola KEK y resolución de clave se proporcionan en los archivos de ejemplo de Hola como KeyWrapper y KeyResolver respectivamente.

### <a name="requireencryption-mode"></a>Modo RequireEncryption
Los usuarios pueden habilitar opcionalmente un modo de operación en el que se deben cifrar todas las cargas y descargas. En este modo, se producirá un error de los intentos de tooupload datos sin un cifrado directiva o descarga los datos que no se cifran en el servicio de hello en cliente hello. Hola **require_encryption** marca en controles de objeto de servicio de hello este comportamiento.

### <a name="blob-service-encryption"></a>Cifrado del servicio de blobs
Establecer campos de directiva de cifrado de hello en objeto de blockblobservice de Hola. Todo lo demás se controlarán mediante la biblioteca de cliente de hello internamente.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_block_blob_service.key_encryption_key = kek
my_block_blob_service.key_resolver_funcion = key_resolver.resolve_key

# Upload hello encrypted contents toohello blob.
my_block_blob_service.create_blob_from_stream(container_name, blob_name, stream)

# Download and decrypt hello encrypted contents from hello blob.
blob = my_block_blob_service.get_blob_to_bytes(container_name, blob_name)
```

### <a name="queue-service-encryption"></a>Cifrado del servicio Cola
Establecer campos de directiva de cifrado de hello en objeto de queueservice de Hola. Todo lo demás se controlarán mediante la biblioteca de cliente de hello internamente.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_queue_service.key_encryption_key = kek
my_queue_service.key_resolver_funcion = key_resolver.resolve_key

# Add message
my_queue_service.put_message(queue_name, content)

# Retrieve message
retrieved_message_list = my_queue_service.get_messages(queue_name)
```

### <a name="table-service-encryption"></a>Cifrado del servicio Tabla
Además toocreating una directiva de cifrado y la configuración de opciones de solicitud, se debe especificar un **encryption_resolver_function** en hello **tableservice**, o hello conjunto cifrar el atributo en Hola EntityProperty.

### <a name="using-hello-resolver"></a>Utilizar al Solucionador de Hola

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Define hello encryption resolver_function.
def my_encryption_resolver(pk, rk, property_name):
        if property_name == 'foo':
                return True
        return False

# Set hello KEK and key resolver on hello service object.
my_table_service.key_encryption_key = kek
my_table_service.key_resolver_funcion = key_resolver.resolve_key
my_table_service.encryption_resolver_function = my_encryption_resolver

# Insert Entity
my_table_service.insert_entity(table_name, entity)

# Retrieve Entity
# Note: No need toospecify an encryption resolver for retrieve, but it is harmless tooleave hello property set.
my_table_service.get_entity(table_name, entity['PartitionKey'], entity['RowKey'])
```

### <a name="using-attributes"></a>Uso de los atributos
Como se mencionó anteriormente, una propiedad puede estar marcada para cifrado mediante el almacenamiento en un objeto EntityProperty y establecer Hola cifrar el campo.

```python
encrypted_property_1 = EntityProperty(EdmType.STRING, value, encrypt=True)
```

## <a name="encryption-and-performance"></a>Cifrado y rendimiento
Tenga en cuenta que el cifrado de sus resultados de datos de almacenamiento da lugar a la sobrecarga de rendimiento adicional. Hola contenido deben generarse clave y un IV, se debe cifrar el propio contenido hello y metadatos adicionales deben con formato y cargarse. Esta sobrecarga variará según la cantidad de Hola de datos está cifrados. Se recomienda que los clientes prueben siempre sus aplicaciones para obtener un rendimiento durante el desarrollo.

## <a name="next-steps"></a>Pasos siguientes
* Descargar hello [biblioteca de cliente de almacenamiento de Azure para Java PyPi paquete](https://pypi.python.org/pypi/azure-storage)
* Descargar hello [biblioteca de cliente de almacenamiento de Azure para el código fuente de Python desde GitHub](https://github.com/Azure/azure-storage-python)
