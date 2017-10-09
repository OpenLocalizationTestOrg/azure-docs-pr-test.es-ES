---
title: "Introducción a la API de REST operaciones aaaMedia Services | Documentos de Microsoft"
description: "Información general de la API de REST de Servicios multimedia"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a5f1c5e7-ec52-4e26-9a44-d9ea699f68d9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b54f4d9123486d6cae832c9817688b0f3da5b401
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-operations-rest-api-overview"></a>Información general sobre la API de REST de operaciones de Media Services
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

Hola **REST de operaciones de servicios multimedia** API se usa para crear trabajos, activos, las directivas de acceso y otras operaciones en objetos en una cuenta de servicios multimedia. Para obtener más información, consulte la [referencia de la API de REST de Media Services Operations](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).

Servicios multimedia de Microsoft Azure es un servicio que acepta solicitudes HTTP basadas en OData y puede responder en JSON detallado o atom+pub. Debido a que los servicios multimedia cumple las directrices de diseño de tooAzure, hay un conjunto de encabezados HTTP obligatorios que cada cliente debe utilizar al conectarse tooMedia servicios, así como un conjunto de encabezados opcionales que puede utilizarse. Hello las secciones siguientes describen los encabezados de Hola y verbos HTTP a los que puede usar al crear solicitudes y recibir respuestas de servicios multimedia.

Este tema proporciona información general sobre cómo toouse REST v2 con servicios multimedia.

## <a name="considerations"></a>Consideraciones

Hola siguientes consideraciones se aplica al usar REST.

* Cuando se consultan las entidades, hay un límite de 1000 entidades devueltas al mismo tiempo porque pública v2 REST limita los resultados de too1000 de resultados de consulta. Necesita toouse **omitir** y **tomar** (. NET) / **arriba** (REST) como se describe en [en este ejemplo .NET](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) y [esta API de REST en el ejemplo se](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities). 
* Cuando usa JSON y especifica toouse hello **__metadata** palabra clave en la solicitud de hello (por ejemplo, un objeto vinculado tooreferences), debe establecer hello **Accept** encabezado demasiado[formato JSON detallado ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) (vea el siguiente ejemplo de Hola). OData no entiende hello **__metadata** propiedad Hola solicitar, a menos que establezca tooverbose.  
  
        POST https://media.windows.net/API/Jobs HTTP/1.1
        Content-Type: application/json;odata=verbose
        Accept: application/json;odata=verbose
        DataServiceVersion: 3.0
        MaxDataServiceVersion: 3.0
        x-ms-version: 2.11
        Authorization: Bearer <token> 
        Host: media.windows.net
  
        {
            "Name" : "NewTestJob", 
            "InputMediaAssets" : 
                [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aba5356eb-30ff-4dc6-9e5a-41e4223540e7')"}}]
        . . . 

## <a name="standard-http-request-headers-supported-by-media-services"></a>Encabezados de solicitud HTTP estándar compatibles con los Servicios multimedia
Para cada llamada efectuada a servicios multimedia, hay un conjunto de encabezados necesarios que debe incluir en la solicitud y también un conjunto de encabezados opcionales puede que desee tooinclude. Hola después Hola de listas de tabla necesarios encabezados:

| Encabezado | Tipo | Valor |
| --- | --- | --- |
| Autorización |Portador |Portador es Hola solo acepta el mecanismo de autorización. valor de Hello también debe incluir el token de acceso de hello proporcionada por ACS. |
| x-ms-version |Decimal |2.11 |
| DataServiceVersion |Decimal |3.0 |
| MaxDataServiceVersion |Decimal |3.0 |

> [!NOTE]
> Dado que los servicios multimedia utiliza OData tooexpose su repositorio de metadatos de recursos subyacente a través de la API de REST, hello DataServiceVersion y MaxDataServiceVersion encabezados debe incluirse en cualquier solicitud; Sin embargo, si no lo están, a continuación, actualmente los servicios multimedia supone hello DataServiceVersion valor en uso es 3.0.
> 
> 

Hola te mostramos un conjunto de encabezados opcionales:

| Encabezado | Tipo | Valor |
| --- | --- | --- |
| Date |Fecha RFC 1123 |Marca de tiempo de solicitud de Hola |
| Accept |Tipo de contenido |Hola solicita el tipo de contenido de respuesta de hello como siguiente hello:<p> -application/json;odata=verbose<p> - application/atom+xml<p> Las respuestas pueden tener un tipo de contenido diferentes, como una captura de blob, donde una respuesta correcta contendrá flujo de blobs de hello como carga de Hola. |
| Accept-Encoding |Gzip, deflate |Codificación GZIP y DEFLATE, según corresponda. En el caso de recursos grandes, Servicios multimedia puede ignorar el encabezado y devolver datos sin comprimir. |
| Accept-Language |"en", "es", etc. |Especifica el idioma de hello preferido de respuesta de Hola. |
| Accept-Charset |Tipo de juego de caracteres como "UTF-8" |El valor predeterminado es UTF-8. |
| X-HTTP-Method |Método HTTP |Permite a los clientes o firewalls que no admiten métodos HTTP como PUT o DELETE toouse estos métodos, túnel a través de una llamada GET. |
| Content-Type |Tipo de contenido |Se solicita el tipo de contenido del cuerpo de la solicitud de hello en PUT o POST. |
| client-request-id |String |Un valor definido por el llamador que identifica Hola dada la solicitud. Si se especifica, este valor se incluirá en el mensaje de respuesta de hello como una solicitud de manera toomap Hola. <p><p>**Importante**<p>Los valores deben estar limitados a 2096b (2k). |

## <a name="standard-http-response-headers-supported-by-media-services"></a>Encabezados de respuesta HTTP estándar compatibles con los Servicios multimedia
Hola aquí te mostramos un conjunto de encabezados que pueden devolverse tooyou según el recurso de Hola que estaba solicitando y Hola acción que pretendía tooperform.

| Encabezado | Tipo | Valor |
| --- | --- | --- |
| request-id |String |Un identificador único para la operación actual de hello, servicio generado. |
| client-request-id |String |Un identificador especificado por el llamador de hello en la solicitud original de hello, si está presente. |
| Date |Fecha RFC 1123 |fecha de Hola se procesó la solicitud Hola. |
| Content-Type |Varía |tipo de contenido de Hola Hola del cuerpo de respuesta. |
| Content-Encoding |Varía |Gzip o deflate, según corresponda. |

## <a name="standard-http-verbs-supported-by-media-services"></a>Verbos HTTP estándar compatibles con los Servicios multimedia
Hola te mostramos una lista completa de los verbos HTTP que pueden utilizarse al efectuar solicitudes HTTP:

| Verbo | Description |
| --- | --- |
| GET |Devuelve Hola valor actual de un objeto. |
| POST |Crea un objeto basado en los datos de hello proporcionados o envía un comando. |
| PUT |Reemplaza un objeto o crea un objeto con nombre (si procede). |
| DELETE |Elimina un objeto. |
| MERGE |Actualiza un objeto existente con los cambios de propiedad con nombre. |
| HEAD |Devuelve los metadatos de un objeto para una respuesta GET. |

## <a name="discover-media-services-model"></a>Detección del modelo de Media Services
se pueden usar entidades de servicios multimedia toomake más reconocibles, operación Hola $metadata. Le permite tooretrieve todos los tipos de entidad válidos, propiedades de la entidad, asociaciones, funciones, acciones y así sucesivamente. Hello en el ejemplo siguiente se muestra cómo tooconstruct Hola URI: https://media.windows.net/API/$ metadatos.

Debe anexar "? api-version=2.x" toohello final de hello URI si quiere tooview Hola metadatos en un explorador, o si no incluyó el encabezado x-ms-version de hello en la solicitud.

## <a name="connect-toomedia-services"></a>Conectar servicios de tooMedia

Para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md). Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia. Debe realizar las llamadas subsiguientes toohello nuevo URI.

## <a name="next-steps"></a>Pasos siguientes

tooaccess APIs AMS con REST, consulte [tooaccess de autenticación de uso de Azure AD Hola API de servicios multimedia de Azure con REST](media-services-rest-connect-with-aad.md).

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

