---
title: aaaUsing compartido (SAS) de firmas de acceso en el almacenamiento de Azure | Documentos de Microsoft
description: "Obtenga información acerca de toouse compartido acceso firmas (SAS) toodelegate acceso tooAzure recursos de almacenamiento, incluidos los blobs, colas, tablas y archivos."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 46fd99d7-36b3-4283-81e3-f214b29f1152
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/18/2017
ms.author: marsma
ms.openlocfilehash: 5b75a3c25bcfb9f1ceb81f31dc2d42376bd105cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-shared-access-signatures-sas"></a>Uso de firmas de acceso compartido (SAS)

Una firma de acceso compartido (SAS) proporciona un tooobjects de acceso de manera toogrant limitado en su cuenta de almacenamiento tooother clientes, sin exponer su clave de cuenta. En este artículo, se proporcionan información general del modelo SAS de hello, revise las prácticas recomendadas SAS y ver algunos ejemplos.

Para obtener ejemplos de código adicional mediante SAS más allá de los que se presentan aquí, consulte [Introducción al almacenamiento de blobs de Azure en .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) así como otros ejemplos disponibles en hello [ejemplos de código de Azure](https://azure.microsoft.com/documentation/samples/?service=storage) biblioteca. Puede descargar aplicaciones de ejemplo de Hola y ejecutarlos o examinar el código de hello en GitHub.

## <a name="what-is-a-shared-access-signature"></a>¿Qué es una firma de acceso compartido?
Una firma de acceso compartido proporciona acceso delegado tooresources en su cuenta de almacenamiento. Con una SAS, puede conceder a los clientes tener acceso a tooresources en la cuenta de almacenamiento sin compartir las claves de cuenta. Éste es Hola punto clave del uso de firmas de acceso compartido en las aplicaciones--una SAS es un tooshare de forma segura los recursos de almacenamiento sin poner en peligro sus claves de cuenta.

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

Una SAS ofrece un control granular sobre tipo hello de acceso que se conceda tooclients que tienen Hola SAS, incluidos:

* intervalo de Hola durante qué hello es válida, incluidos la hora de expiración de Hola y la hora de inicio de hello SAS.
* permisos de Hello concedidos por hello SAS. Por ejemplo, una SAS para un blob puede conceder y escribir permisos toothat blob, pero no eliminar permisos.
* Una dirección IP opcional o intervalo de direcciones IP desde el que va a aceptar el almacenamiento de Azure Hola SAS. Por ejemplo, puede especificar un intervalo de direcciones IP que pertenezcan tooyour organización.
* Protocolo de Hello en el cual el almacenamiento de Azure aceptará Hola SAS. Puede usar este tooclients de acceso de parámetro opcional toorestrict mediante HTTPS.

## <a name="when-should-you-use-a-shared-access-signature"></a>¿Cuándo debe usar una firma de acceso compartido?
Puede usar una SAS cuando desee tooprovide acceso tooresources en el cliente de tooany de cuenta de almacenamiento que no posee las teclas de acceso de la cuenta de almacenamiento. La cuenta de almacenamiento incluye una clave de acceso principal y secundaria, los cuales conceder acceso administrativo tooyour cuenta y todos los recursos dentro de él. Exposición de cualquiera de estas claves, abre la posibilidad de toohello de cuenta de uso malintencionado o por negligencia. Firmas de acceso compartido proporcionan una alternativa segura que permite a los clientes tooread, escribir y eliminar datos en la cuenta de almacenamiento según los permisos de toohello que le ha concedido explícitamente y sin necesidad de una clave de cuenta.

Un escenario común donde una SAS es útil es un servicio donde los usuarios leerán y escribir su propia cuenta de almacenamiento de datos tooyour. Existen dos patrones de diseño típicos en los escenarios en los que una cuenta de almacenamiento guarda datos de usuario:

1. Los clientes cargan y descargan datos mediante un servicio de proxy front-end que realiza la autenticación. Este servicio de proxy de front-end tiene la ventaja de Hola de permitir que la validación de reglas de negocios, pero con grandes cantidades de datos o transacciones de gran volumen, la creación de un servicio que se pueda escalar a petición toomatch puede resultar costoso o difícil.

  ![Diagrama del escenario: servicio de proxy de front-end](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-fe-proxy-service.png)   

1. Un servicio ligero autentica el cliente de hello según sea necesario y, a continuación, genera una SAS. Una vez que el cliente de hello recibe Hola SAS, puede acceder a recursos de la cuenta de almacenamiento directamente con permisos de hello definidos Hola SAS y para el intervalo de saludo permitido por hello SAS. Hola SAS mitiga la necesidad de hello para el enrutamiento de todos los datos a través del servicio de proxy de front-end de Hola.

  ![Diagrama del escenario: servicio de proveedor de SAS](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-provider-service.png)   

Muchos servicios reales pueden usar una combinación de estos dos enfoques. Por ejemplo, algunos datos se pueden procesar y validar a través de proxy de front-end de hello, mientras que otros datos se guardan o leer directamente mediante SAS.

Además, necesitará toouse un objeto de origen SAS tooauthenticate hello en una operación de copia en ciertos escenarios:

* Al copiar un blob de tooanother de blob que reside en una cuenta de almacenamiento diferente, debe usar un blob de origen SAS tooauthenticate Hola. También puede usar un blob de destino para las hello de la tooauthenticate SAS también.
* Al copiar un archivo de tooanother de archivo que se encuentra en una cuenta de almacenamiento diferente, debe usar un archivo de código fuente SAS tooauthenticate Hola. También puede usar una SAS tooauthenticate Hola de destino también.
* Al copiar un archivo de tooa de blob o un blob de tooa de archivo, debe usar un objeto de origen SAS tooauthenticate hello, incluso si los objetos de origen y destino de hello residen dentro de hello mismo cuenta de almacenamiento.

## <a name="types-of-shared-access-signatures"></a>Tipos de firmas de acceso compartido
Puede crear dos tipos de firmas de acceso compartido:

* **SAS de servicio.** delegados SAS del servicio de Hello tener acceso a recursos tooa en solo uno de los servicios de almacenamiento de hello: Hola servicio Blob, cola, tabla o archivo. Vea [construir una SAS de servicio](https://msdn.microsoft.com/library/dn140255.aspx) y [ejemplos de SAS del servicio](https://msdn.microsoft.com/library/dn140256.aspx) para obtener información detallada sobre cómo generar el token SAS del servicio de Hola.
* **SAS de cuenta.** los delegados SAS de cuenta de Hello tener acceso a tooresources en uno o varios de los servicios de almacenamiento de Hola. Todas las operaciones de hello disponibles a través de un servicio de SAS de también están disponibles a través de una cuenta SA. Además, con la cuenta de hello SAS, puede delegar toooperations de acceso que se aplican tooa dado servicio, como **propiedades de servicio Get/Set** y **obtener estadísticas del servicio**. También puede delegar el acceso tooread, escritura y las operaciones de eliminación en contenedores de blobs, tablas, colas y recursos compartidos de archivos que no se permiten con un servicio de SAS. Vea [construir una SAS de cuenta](https://msdn.microsoft.com/library/mt584140.aspx) para obtener información detallada sobre cómo generar el token de SAS de cuenta de hello.

## <a name="how-a-shared-access-signature-works"></a>Funcionamiento de una firma de acceso compartido
Una firma de acceso compartido es un URI firmado que señala tooone o más recursos de almacenamiento e incluye un símbolo (token) que contiene un conjunto especial de parámetros de consulta. símbolo (token) de Hello indica cómo se pueden tener acceso a recursos de hello cliente Hola. Uno de los parámetros de consulta de hello, Hola firma, está construido a partir de los parámetros de SAS de Hola y firmado con la clave de la cuenta de hello. Hola de tooauthenticate de almacenamiento de Azure SAS usa esta firma.

Este es un ejemplo de un URI de SAS, el URI del recurso de Hola que muestra y el token de SAS de hello:

![Componentes de un identificador URI de SAS](./media/storage-dotnet-shared-access-signature-part-1/sas-storage-uri.png)   

token de SAS Hello es una cadena que se generan en hello *cliente* lado (vea hello [ejemplos SAS](#sas-examples) sección para obtener ejemplos de código). Un token SAS que se genera con la biblioteca de cliente de almacenamiento de hello, por ejemplo, no está registrado por el almacenamiento de Azure de forma alguna. Puede crear un número ilimitado de tokens de SAS en el lado del cliente de Hola.

Cuando un cliente proporciona un almacenamiento de URI de SAS tooAzure como parte de una solicitud, servicio de hello comprueba los parámetros de SAS de Hola y tooverify de firma que es válido para la autenticación de la solicitud de Hola. Si el servicio Hola comprueba que esa firma hello es válida, se autentica solicitud Hola. En caso contrario, se rechazó una solicitud Hola con código de error 403 (prohibido).

## <a name="shared-access-signature-parameters"></a>Parámetros de la firma de acceso compartido
cuenta de Hello SAS y tokens SAS del servicio incluyen algunos parámetros comunes y tener unos parámetros que son diferentes.

### <a name="parameters-common-tooaccount-sas-and-service-sas-tokens"></a>Parámetros comunes tooaccount SAS y tokens SAS del servicio
* **Versión de API** un parámetro opcional que especifica la solicitud de hello almacenamiento servicio versión toouse tooexecute Hola.
* **Versión del servicio** un parámetro obligatorio que especifica la solicitud de hello almacenamiento servicio versión toouse tooauthenticate Hola.
* **Hora de inicio.** Se trata de tiempo de hello en qué Hola SAS se vuelve válida. hora de inicio de Hola de firma de acceso compartido es opcional. Si se omite una hora de inicio, Hola SAS es efectiva de inmediato. Hello hora de inicio se debe expresar en UTC (hora Universal), con un designador de hora UTC especial ("Z"), por ejemplo `1994-11-05T13:15:30Z`.
* **Hora de expiración.** Se trata de hello hora después del cual hello SAS ya no es válida. En las prácticas recomendadas se aconseja especificar una hora de expiración para una SAS o asociarla a una directiva de acceso almacenada. Hola la hora de expiración se debe expresar en UTC (hora Universal), con un designador de hora UTC especial ("Z"), por ejemplo `1994-11-05T13:15:30Z` (ver más abajo).
* **Permisos.** permisos de Hello especificados en hello SAS indican qué operaciones puede realizar cliente hello en un recurso de almacenamiento de hello mediante Hola SAS. Los permisos disponibles son diferentes para SAS de cuenta y SAS de servicio.
* **Dirección Dirección IP.** Un parámetro opcional que especifica una dirección IP o un intervalo de direcciones IP fuera de Azure (consulte la sección de hello [estado de configuración de sesión de enrutamiento](../../expressroute/expressroute-workflows.md#routing-session-configuration-state) de Express Route) desde qué solicitudes de tooaccept.
* **Protocolo.** Un parámetro opcional que especifica el protocolo de hello permitidos para una solicitud. Los valores posibles son HTTP y HTTPS (`https,http`), que es valor predeterminado de Hola o HTTPS solo (`https`). Tenga en cuenta que HTTP solo no es un valor permitido.
* **Firma.** firma de Hola se construye a partir de hello otros parámetros especificado como parte de símbolo (token) y, a continuación, se cifra. Ha utilizado tooauthenticate Hola SAS.

### <a name="parameters-for-a-service-sas-token"></a>Parámetros para un token de SAS de servicio
* **Recurso de almacenamiento.** Los recursos de almacenamiento para los que puede delegar el acceso con una SAS de servicio incluyen:
  * Contenedores y blobs
  * Archivos y recursos compartidos de archivo
  * Colas
  * Las tablas y los intervalos de las entidades de tabla.

### <a name="parameters-for-an-account-sas-token"></a>Parámetros para un token de SAS de cuenta
* **Servicio o servicios.** Una cuenta de SAS puede delegar acceso tooone o varios de los servicios de almacenamiento de Hola. Por ejemplo, puede crear una cuenta SAS que los delegados de tener acceso a servicio de Blob y archivo de toohello. O bien, puede crear una SAS que los delegados de tener acceso a tooall cuatro servicios (Blob, cola, tabla y archivo).
* **Tipos de recursos de almacenamiento.** Aplica una cuenta SA tooone o más clases de recursos de almacenamiento, en lugar de un recurso concreto. Puede crear un acceso de cuenta SAS toodelegate para:
  * API de nivel de servicio, que se llaman en un recurso de cuenta de almacenamiento de Hola. Algunos ejemplos incluyen **Get/Set Service Properties**, **Get Service Stats**, and **List Containers/Queues/Tables/Shares**.
  * Las API de nivel de contenedor, que se denominan con los objetos de contenedor de Hola para cada servicio: blob contenedores, colas, tablas y los recursos compartidos de archivos. Algunos ejemplos incluyen **Create/Delete Container**, **Create/Delete Queue**, **Create/Delete Table**, **Create/Delete Share** y **List Blobs/Files y Directories**.
  * Las API de nivel de objeto, a las que se llaman en blobs, mensajes de colas, entidades de tablas y archivos. Por ejemplo, **Put Blob**, **Query Entity**, **Get Messages** y **Create File**.

## <a name="examples-of-sas-uris"></a>Ejemplos de URI de SAS

### <a name="service-sas-uri-example"></a>Ejemplo de identificador URI de SAS de servicio

Este es un ejemplo de un servicio URI de SAS proporciona leer y escribir permisos tooa blob. tabla de Hello desglosa cada parte de hello URI toounderstand cómo contribuye toohello SAS:

```
https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2015-04-05&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D
```

| Nombre | Parte de SAS | Description |
| --- | --- | --- |
| URI de blobs |`https://myaccount.blob.core.windows.net/sascontainer/sasblob.txt` |dirección de Hola de blob de Hola. Tenga en cuenta que se recomienda fehacientemente el uso de HTTPS. |
| Versión de servicios de almacenamiento |`sv=2015-04-05` |Para servicios de almacenamiento versión 2012-02-12 y versiones posteriores, este parámetro indica Hola versión toouse. |
| Hora de inicio |`st=2015-04-29T22%3A18%3A26Z` |Se especifica en hora UTC. Si desea Hola SAS toobe válida inmediatamente, omita la hora de inicio Hola. |
| Hora de expiración |`se=2015-04-30T02%3A23%3A26Z` |Se especifica en hora UTC. |
| Recurso |`sr=b` |recurso de Hello es un blob. |
| Permisos |`sp=rw` |permisos de Hello concedidos por hello SAS incluyen Read (r) y escritura (w). |
| Intervalo de IP |`sip=168.1.5.60-168.1.5.70` |Hola intervalo de direcciones IP desde el que se aceptarán una solicitud. |
| Protocol |`spr=https` |Solo se permiten solicitudes con HTTPS. |
| Firma |`sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D` |Usa el blob de tooauthenticate acceso toohello. firma de Hello es un HMAC calculado sobre un valor string-to-sign y una clave con el algoritmo SHA256 de hello y, a continuación, codificado con Base64. |

### <a name="account-sas-uri-example"></a>Ejemplo de identificador URI de SAS de cuenta

Este es un ejemplo de una cuenta de SAS que usa Hola mismo parámetros comunes de token de Hola. Como estos parámetros aparecen descritos anteriormente, no los vamos a describir aquí. Hello en los parámetros que son específico tooaccount que SAS se describen en la siguiente tabla se Hola.

```
https://myaccount.blob.core.windows.net/?restype=service&comp=properties&sv=2015-04-05&ss=bf&srt=s&st=2015-04-29T22%3A18%3A26Z&se=2015-04-30T02%3A23%3A26Z&sr=b&sp=rw&sip=168.1.5.60-168.1.5.70&spr=https&sig=F%6GRVAZ5Cdj2Pw4tgU7IlSTkWgn7bUkkAg8P6HESXwmf%4B
```

| Nombre | Parte de SAS | Description |
| --- | --- | --- |
| URI de recurso |`https://myaccount.blob.core.windows.net/?restype=service&comp=properties` |Hola extremo del servicio Blob, con parámetros para obtener propiedades del servicio (cuando se llama con GET) o establecer las propiedades del servicio (cuando se llama con conjunto). |
| Services |`ss=bf` |Hola SAS aplica toohello Blob y servicios de archivos |
| Tipos de recursos |`srt=s` |Hola SAS aplica a las operaciones de nivel de tooservice. |
| Permisos |`sp=rw` |permisos de Hello conceder acceso tooread y las operaciones de escritura. |

Dado que los permisos están restringidos toohello el nivel de servicio, operaciones accesibles con esta SAS son **obtener propiedades del servicio Blob** (lectura) y **Set Blob Service Properties** (escribir). Sin embargo, con un URI de recurso diferente, hello mismo token SAS también pueden usar toodelegate acceso demasiado**obtener estadísticas del servicio Blob** (lectura).

## <a name="controlling-a-sas-with-a-stored-access-policy"></a>Control de una SAS con una directiva de acceso almacenada
Una firma de acceso compartido puede presentar una de estas dos formas:

* **SAS ad hoc:** cuando se crea un SAS ad hoc, la hora de inicio de hello, la hora de expiración y permisos para hello SAS se especifican en Hola URI de SAS (o implícitas, en caso de hello donde se omite la hora de inicio). Este tipo de SAS puede crearse como SAS de cuenta o como SAS de servicio.
* **Asociaciones de seguridad con la directiva de acceso almacenada:** una directiva de acceso almacenada se define en un contenedor de recursos: un contenedor de blob, tabla, poner en cola, o de recurso compartido, de archivos y puede ser restricciones toomanage usado para una o varias firmas de acceso compartido. Al asociar una SAS con una directiva de acceso almacenada, Hola SAS hereda las restricciones de hello: hora de inicio de hello, la hora de expiración y permisos--definidos para la directiva de acceso de hello almacenado.

> [!NOTE]
> Actualmente, una SAS de cuenta debe ser una SAS ad hoc. Las directivas de acceso almacenadas ya no son compatibles para SAS de cuenta.

Hello diferencia entre Hola dos formatos es importante para un escenario clave: revocación. Dado que un URI de SAS es una dirección URL, cualquier persona que obtenga Hola SAS puede utilizar, independientemente de quién lo creó originalmente. Si una SAS se publica públicamente, se puede utilizar cualquier usuario de Hola a todos. Un tooanyone de tooresources acceso SAS concede se que cuente con él hasta que se produce uno de cuatro aspectos:

1. hora de expiración de Hello especificado en hello que SAS se alcanza.
2. hora de expiración de Hello especificado en la directiva de acceso de hello almacenado al que hace referencia Hola que SAS se alcanza (si se hace referencia a una directiva de acceso almacenada y si especifica una hora de expiración). Esto puede ocurrir porque transcurre el intervalo de saludo o porque se ha modificado la directiva de acceso de hello almacenado con una hora de expiración en hello anterior, que es una manera de toorevoke hello SAS.
3. Hola almacenado al que hace referencia Hola que SAS se elimina, que es hello de toorevoke de otra manera SAS de directiva de acceso. Tenga en cuenta que si exactamente, volver a directiva de acceso de hello almacenado con Hola homónimas, todas las SA existentes tokens will nuevo asociarse permisos toohello correspondiente válidos esa directiva de acceso almacenada (suponiendo que la hora de expiración hello en hello SAS no ha pasado). Si tiene previsto toorevoke Hola SAS, ser seguro toouse un nombre diferente si vuelve a crear la directiva de acceso Hola con una hora de expiración en hello futuras.
4. clave de la cuenta de Hello que estaba toocreate usado Hola SAS se vuelve a generar. Volver a generar una clave de cuenta hará que todos los componentes de aplicación mediante esa tooauthenticate toofail clave hasta que se actualizan toouse Hola ya sea otra clave de cuenta válido o la clave de cuenta recién regenerada de Hola.

> [!IMPORTANT]
> Un URI de firma de acceso compartido está asociado a la firma de hello cuenta clave toocreate usado Hola y Hola asociados directiva de acceso almacenada (si existe). Si no se especifica ninguna directiva de acceso almacenada, hello toorevoke de manera sólo firma de acceso compartido es toochange Hola cuenta clave.

## <a name="authenticating-from-a-client-application-with-a-sas"></a>Autenticación desde una aplicación cliente con una SAS
Un cliente que está en posesión de una SAS puede utilizar Hola SAS tooauthenticate una solicitud en una cuenta de almacenamiento para el que no poseen claves de cuenta de hello. Una SAS pueden incluirse en una cadena de conexión, o utilización directa desde el método o constructor adecuado de Hola.

### <a name="using-a-sas-in-a-connection-string"></a>Uso de SAS en una cadena de conexión
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

### <a name="using-a-sas-in-a-constructor-or-method"></a>Uso de una SAS en un constructor o método
Varios constructores de biblioteca de cliente de almacenamiento de Azure y sobrecargas de método ofrecen un parámetro SAS, para que pueda autenticar un servicio de toohello de solicitud con una SAS.

Por ejemplo, aquí un URI de SAS es toocreate usado un blob en bloques tooa referencia. Hola SAS proporciona credenciales solo Hola necesarias para la solicitud de Hola. referencia de blob de bloque de Hello, a continuación, se utiliza para una operación de escritura:

```csharp
string sasUri = "https://storagesample.blob.core.windows.net/sample-container/" +
    "sampleBlob.txt?sv=2015-07-08&sr=b&sig=39Up9JzHkxhUIhFEjEH9594DJxe7w6cIRCg0V6lCGSo%3D" +
    "&se=2016-10-18T21%3A51%3A37Z&sp=rcw";

CloudBlockBlob blob = new CloudBlockBlob(new Uri(sasUri));

// Create operation: Upload a blob with hello specified name toohello container.
// If hello blob does not exist, it will be created. If it does exist, it will be overwritten.
try
{
    MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    msWrite.Position = 0;
    using (msWrite)
    {
        await blob.UploadFromStreamAsync(msWrite);
    }

    Console.WriteLine("Create operation succeeded for SAS {0}", sasUri);
    Console.WriteLine();
}
catch (StorageException e)
{
    if (e.RequestInformation.HttpStatusCode == 403)
    {
        Console.WriteLine("Create operation failed for SAS {0}", sasUri);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    else
    {
        Console.WriteLine(e.Message);
        Console.ReadLine();
        throw;
    }
}

```

## <a name="best-practices-when-using-sas"></a>Procedimientos recomendados al usar SAS
Al usar firmas de acceso compartido en las aplicaciones, necesita toobe en cuenta dos posibles riesgos:

* Si se perdió una SAS, cualquier persona que la consiga puede usarla, lo que puede poner en riesgo su cuenta de almacenamiento.
* Si no proporciona una SAS expira tooa aplicación de cliente o aplicación hello no se puede tooretrieve una nueva SAS de su servicio, puede impedirse funcionalidad de la aplicación hello.

Hello siguientes recomendaciones para el uso de firmas de acceso compartido pueden ayudar a mitigar estos riesgos:

1. **Utilizar siempre HTTPS** toocreate o distribuya una SAS. Si se pasa a través de HTTP e interceptar una SAS, un atacante que realiza un ataque de man-in-the-middle es capaz de tooread hello SAS y, a continuación, use solo según lo previsto de hello podrían tener usuarios, podría poner en peligro los datos confidenciales o permitir de daños en los datos por hello usuario malintencionado.
2. **Haga referencia a las directivas de acceso almacenadas cuando sea posible.** Almacena ofrecen a las directivas de acceso Hola permisos de toorevoke opción sin tener claves de cuenta de almacenamiento de tooregenerate Hola. Establecer caducidad Hola estos temas muy alejadas en hello futura (o infinito) y asegurarse de que se ha actualizado con regularidad toomove más lejos en hello futuras.
3. **Use horas de expiración a corto plazo en una SAS ad-hoc.** De esta manera, incluso si una SAS está en peligro, es válida solo durante un breve período. Esta práctica es especialmente importante si no puede hacer referencia a una directiva de acceso almacenada. Tiempos de expiración a corto plazo también limitan la cantidad de Hola de datos que se pueden escribir tooa blob mediante la limitación de hello tiempo disponible tooupload tooit.
4. **Tener clientes renovar automáticamente Hola SAS si es necesario.** Los clientes deben renovar Hola SAS bien antes de que caduque hello, en el tiempo de tooallow de orden de los reintentos si servicio Hola proporcionar Hola SAS no está disponible. Si su SAS está pensado toobe usado para un número reducido de inmediato, las operaciones de corta duración que espera toobe completada dentro del período de expiración de hello, esto puede ser innecesario como Hola que SAS no esperaba toobe renovado. Sin embargo, si tiene un cliente que habitualmente se está realizando solicitudes a través de SAS, posibilidad de Hola de expiración entra en juego. Hello consideraciones clave es toobalance Hola necesidad para hello SAS toobe corta duración (como se mencionó anteriormente) con hello necesidad tooensure que Hola cliente está solicitando renovación al principio suficiente (interrupción de tooavoid debido a que van a expirar toosuccessful anterior renovación de toohello SAS).
5. **Tenga cuidado con la hora de inicio de la SAS.** Si establece la hora de inicio de Hola para una SAS demasiado**ahora**, luego debido tooclock sesgo (las diferencias en la hora actual según toodifferent máquinas), errores, se pueden observar de vez en cuando para hello primeros minutos. En general, establezca toobe de tiempo de inicio de hello al menos 15 minutos en hello anterior. O, no establezca esta opción en absoluto, lo que hará que sea válido inmediatamente en todos los casos. Hola mismo sucede generalmente tooexpiry tiempo también--Recuerde que se puede observar una too15 minutos del reloj del sesgo en cualquier dirección en cualquier solicitud. Para los clientes que usan un resto versión anterior too2012-02-12, duración máxima de Hola para una SA que no hace referencia a una directiva de acceso almacenada es 1 hora y las directivas que se especifica a largo plazo de se producirá un error.
6. **Ser específico con hello recursos toobe tiene acceso.** Una práctica recomendada de seguridad es un usuario con privilegios mínimos requeridos de hello tooprovide. Si un usuario solo necesita acceso de lectura tooa única entidad, a continuación, concederles acceso de lectura toothat única entidad y no de lectura/escritura/eliminación acceso tooall entidades. Esto también ayuda a reducir los daños de hello si se pone en peligro una SAS porque Hola SAS tiene menor consumo de energía en manos de Hola de que un atacante.
7. **Comprenda que se le hará un cargo en la cuenta por cualquier uso, incluido el realizado con la SAS.** Si proporciona acceso de escritura tooa blob, un usuario puede elegir tooupload un blob de 200GB. Si se le ha dado ellos también acceso de lectura, puede elegir toodownload 10 veces, incurriendo en 2 TB en salida cuesta automáticamente. Una vez más, proporcionar permisos limitados toohelp mitigar posibles acciones de Hola de usuarios malintencionados. Usar esta amenaza de corta duración tooreduce SAS (aunque esté atento a reloj se sesga en hora de finalización de hello).
8. **Valide los datos escritos mediante la SAS.** Cuando una aplicación cliente escribe la cuenta de almacenamiento de datos tooyour, tenga en cuenta que puede haber problemas con dichos datos. Si la aplicación requiere que se valida o autorización antes de que se toouse listo datos, debe realizar esta validación después de que se escriben los datos de Hola y antes de que se usa la aplicación. Esta práctica también protege frente a dañado o malintencionados de los datos que se escriben tooyour cuenta, ya sea por un usuario que se adquirió correctamente Hola SAS o por un usuario aprovecharse de una SAS perdida.
9. **No use siempre la SAS.** A veces los riesgos de hello asociados con una operación determinada en su cuenta de almacenamiento superan a las ventajas de Hola de SAS. Para estas operaciones, crear un servicio de nivel intermedio que escribe la cuenta de almacenamiento tooyour después de realizar negocios de reglas de validación, autenticación y auditoría. Además, a veces resulta más fácil acceso toomanage de otras maneras. Por ejemplo, si desea que toomake todos los blobs en un contenedor de leer públicamente, puede realizar Hola contenedor público, en lugar de proporcionar un cliente de tooevery SAS para el acceso.
10. **Use toomonitor de análisis de almacenamiento de la aplicación.** Puede utilizar el registro y tooobserve métricas cualquier incremento en errores de autenticación debido a una interrupción de tooan en su SAS proveedor servicio o toohello involuntario eliminación de una directiva de acceso almacenada. Vea hello [Blog del equipo de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/08/03/windows-azure-storage-logging-using-logs-to-track-storage-requests.aspx) para obtener información adicional.

## <a name="sas-examples"></a>Ejemplos de SAS
A continuación figuran algunos ejemplos de ambos tipos de firmas de acceso compartido, SAS de cuenta y SAS de servicio.

toorun estos ejemplos de C#, necesita hello tooreference siguientes paquetes de NuGet en el proyecto:

* [Biblioteca de cliente de almacenamiento de Azure para .NET](http://www.nuget.org/packages/WindowsAzure.Storage), versión 6.x o posterior (toouse cuenta SAS).
* [Azure Configuration Manager](http://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager)

Para obtener ejemplos adicionales que muestran cómo toocreate y prueba una SAS, consulte [ejemplos de código de Azure para almacenamiento](https://azure.microsoft.com/documentation/samples/?service=storage).

### <a name="example-create-and-use-an-account-sas"></a>Ejemplo: Crear y utilizar una SAS de cuenta
Hello ejemplo de código siguiente crea una cuenta SA que es válida para hello Blob y servicios de archivos, y proporciona Hola permisos de cliente de lectura, escritura y permisos de lista de las API de nivel de servicio tooaccess. cuenta de Hello SAS restringe hello tooHTTPS de protocolo, por lo que solicitud Hola debe realizarse con HTTPS.

```csharp
static string GetAccountSASToken()
{
    // toocreate hello account SAS, you need toouse your shared key credentials. Modify for your account.
    const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

    // Create a new access policy for hello account.
    SharedAccessAccountPolicy policy = new SharedAccessAccountPolicy()
        {
            Permissions = SharedAccessAccountPermissions.Read | SharedAccessAccountPermissions.Write | SharedAccessAccountPermissions.List,
            Services = SharedAccessAccountServices.Blob | SharedAccessAccountServices.File,
            ResourceTypes = SharedAccessAccountResourceTypes.Service,
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Protocols = SharedAccessProtocol.HttpsOnly
        };

    // Return hello SAS token.
    return storageAccount.GetSharedAccessSignature(policy);
}
```

toouse Hola cuenta SAS tooaccess el API de nivel de servicio para el servicio de Blob de hello, construir un objeto de cliente de Blob utilizando Hola SAS y Hola de punto de conexión de almacenamiento de blobs para su cuenta de almacenamiento.

```csharp
static void UseAccountSAS(string sasToken)
{
    // Create new storage credentials using hello SAS token.
    StorageCredentials accountSAS = new StorageCredentials(sasToken);
    // Use these credentials and hello account name toocreate a Blob service client.
    CloudStorageAccount accountWithSAS = new CloudStorageAccount(accountSAS, "account-name", endpointSuffix: null, useHttps: true);
    CloudBlobClient blobClientWithSAS = accountWithSAS.CreateCloudBlobClient();

    // Now set hello service properties for hello Blob client created with hello SAS.
    blobClientWithSAS.SetServiceProperties(new ServiceProperties()
    {
        HourMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        MinuteMetrics = new MetricsProperties()
        {
            MetricsLevel = MetricsLevel.ServiceAndApi,
            RetentionDays = 7,
            Version = "1.0"
        },
        Logging = new LoggingProperties()
        {
            LoggingOperations = LoggingOperations.All,
            RetentionDays = 14,
            Version = "1.0"
        }
    });

    // hello permissions granted by hello account SAS also permit you tooretrieve service properties.
    ServiceProperties serviceProperties = blobClientWithSAS.GetServiceProperties();
    Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
    Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
    Console.WriteLine(serviceProperties.HourMetrics.Version);
}
```

### <a name="example-create-a-stored-access-policy"></a>Ejemplo: Crear una directiva de acceso almacenada
Hello código siguiente crea una directiva de acceso almacenada en un contenedor. Puede utilizar restricciones de toospecify de directivas de acceso de Hola para un servicio SAS en el contenedor de Hola o sus blobs.

```csharp
private static async Task CreateSharedAccessPolicyAsync(CloudBlobContainer container, string policyName)
{
    // Create a new shared access policy and define its constraints.
    // hello access policy provides create, write, read, list, and delete permissions.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
        // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
        SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.List |
            SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create | SharedAccessBlobPermissions.Delete
    };

    // Get hello container's existing permissions.
    BlobContainerPermissions permissions = await container.GetPermissionsAsync();

    // Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    await container.SetPermissionsAsync(permissions);
}
```

### <a name="example-create-a-service-sas-on-a-container"></a>Ejemplo: Crear una SAS de servicio en un contenedor
Hola siguiente código crea una SAS en un contenedor. Si se proporciona el nombre de Hola de una directiva de acceso almacenada existente, esa directiva está asociada con hello SAS. Si no se proporciona ninguna directiva de acceso almacenada, código de hello crea una SAS de ad hoc en el contenedor de Hola.

```csharp
private static string GetContainerSasUri(CloudBlobContainer container, string storedPolicyName = null)
{
    string sasContainerToken;

    // If no stored policy is specified, create a new access policy and define its constraints.
    if (storedPolicyName == null)
    {
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocPolicy = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List
        };

        // Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
        sasContainerToken = container.GetSharedAccessSignature(adHocPolicy, null);

        Console.WriteLine("SAS for blob container (ad hoc): {0}", sasContainerToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello container. In this case, all of hello constraints for the
        // shared access signature are specified on hello stored access policy, which is provided by name.
        // It is also possible toospecify some constraints on an ad-hoc SAS and others on hello stored access policy.
        sasContainerToken = container.GetSharedAccessSignature(null, storedPolicyName);

        Console.WriteLine("SAS for blob container (stored access policy): {0}", sasContainerToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

### <a name="example-create-a-service-sas-on-a-blob"></a>Ejemplo: Crear una SAS de servicio en un blob
Hola siguiente código crea una SAS en un blob. Si se proporciona el nombre de Hola de una directiva de acceso almacenada existente, esa directiva está asociada con hello SAS. Si no se proporciona ninguna directiva de acceso almacenada, código de hello crea una SAS de ad hoc en blob Hola.

```csharp
private static string GetBlobSasUri(CloudBlobContainer container, string blobName, string policyName = null)
{
    string sasBlobToken;

    // Get a reference tooa blob within hello container.
    // Note that hello blob may not exist yet, but a SAS can still be created for it.
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    if (policyName == null)
    {
        // Create a new access policy and define its constraints.
        // Note that hello SharedAccessBlobPolicy class is used both toodefine hello parameters of an ad-hoc SAS, and
        // tooconstruct a shared access policy that is saved toohello container's shared access policies.
        SharedAccessBlobPolicy adHocSAS = new SharedAccessBlobPolicy()
        {
            // When hello start time for hello SAS is omitted, hello start time is assumed toobe hello time when hello storage service receives hello request.
            // Omitting hello start time for a SAS that is effective immediately helps tooavoid clock skew.
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.Create
        };

        // Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
        sasBlobToken = blob.GetSharedAccessSignature(adHocSAS);

        Console.WriteLine("SAS for blob (ad hoc): {0}", sasBlobToken);
        Console.WriteLine();
    }
    else
    {
        // Generate hello shared access signature on hello blob. In this case, all of hello constraints for the
        // shared access signature are specified on hello container's stored access policy.
        sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

        Console.WriteLine("SAS for blob (stored access policy): {0}", sasBlobToken);
        Console.WriteLine();
    }

    // Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

## <a name="conclusion"></a>Conclusión
Firmas de acceso compartido son útiles para proporcionar permisos limitados tooclients de cuenta de almacenamiento de tooyour que no se debería tener la clave de la cuenta de hello. Por lo tanto, son una parte fundamental del modelo de seguridad de Hola para las aplicaciones que utilizan el almacenamiento de Azure. Si sigue los procedimientos recomendados de hello enumerados aquí, puede usar tooprovide mayor flexibilidad en SAS de acceso tooresources en su cuenta de almacenamiento, sin poner en peligro la seguridad de saludo de la aplicación.

## <a name="next-steps"></a>Pasos siguientes
* [Administrar blobs y acceso de lectura anónimo toocontainers](../blobs/storage-manage-access-to-resources.md)
* [Delegación de acceso con una firma de acceso compartido](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Introducción a las firmas de acceso compartido de tabla y cola](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
