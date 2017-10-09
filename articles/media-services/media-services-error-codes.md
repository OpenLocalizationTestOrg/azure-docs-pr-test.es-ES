---
title: "códigos de error de servicios multimedia de aaaAzure | Documentos de Microsoft"
description: "tema de Hello ofrezca una visión general de los códigos de error de servicios multimedia de Azure."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d3a62a64-7608-4b17-8667-479b26ba0d6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: de1ffd6dee8901a3051eb5032536c3669482d6b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-error-codes"></a>Códigos de error de Azure Media Services
Cuando se usa servicios de multimedia de Microsoft Azure, puede recibir códigos de error HTTP del servicio de hello según problemas como los tokens de autenticación a expirar tooactions que no se admiten en los servicios multimedia. Hello siguiente es una lista de **códigos de error HTTP** que puede devolver los servicios multimedia y Hola posibles causas de ellos.  

## <a name="400-bad-request"></a>400 - Solicitud incorrecta
solicitud de Hello contiene información no válida y se rechaza due tooone de hello siguientes motivos:

* Se especifica una versión de API no compatible. Para la versión más reciente de hello, consulte [el programa de instalación para el desarrollo de API de REST de servicios multimedia](media-services-rest-how-to-use.md).
* no se especifica la versión de Hola API de servicios multimedia. Para obtener información sobre cómo toospecify Hola versión de API, consulte [Media Services operaciones REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).
  
  > [!NOTE]
  > Si usas tooMedia de hello .NET o el SDK de Java tooconnect Services, versión de API de Hola se especificará automáticamente cada vez que intente y realizar alguna acción en servicios multimedia.
  > 
  > 
* Se ha especificado una propiedad no definida. nombre de la propiedad de Hello es en el mensaje de error de saludo. Se pueden especificar solo las propiedades miembro de una entidad determinada. Consulte [Referencia de la API de REST de Azure Media Services](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) para obtener una lista de entidades y sus propiedades.
* Se ha especificado un valor de propiedad no válido. nombre de la propiedad de Hello es en el mensaje de error de saludo. Vea el vínculo anterior de Hola para tipos de propiedad válidos y sus valores.
* Falta un valor de propiedad y es obligatorio.
* Parte de la dirección URL de hello especificada contiene un valor incorrecto.
* Fue un intento realizado tooupdate una propiedad WriteOnce.
* Fue un intento realizado toocreate un trabajo que tiene un recurso de entrada con un AssetFile principal que no se especificó o no se pudo determinar.
* Fue un intento realizado tooupdate un localizador SAS. Solo se pueden crear o eliminar localizadores SAS. Los localizadores en streaming pueden actualizarse. Para obtener más información, consulte [Localizadores](https://docs.microsoft.com/rest/api/media/operations/locator).
* Se ha enviado una operación no compatible o una consulta.

## <a name="401-unauthorized"></a>401 No autorizado
no se pudo autenticar la solicitud de Hello (antes de que pueda autorizarse) tooone vencimiento de hello siguientes motivos:

* Falta el encabezado de autenticación.
* Valor del encabezado de autenticación incorrecto.
  * Hola token ha expirado. 
  * símbolo (token) de Hello contiene una firma no válida.

## <a name="403-forbidden"></a>403 Prohibido
no se permite debido Hola solicitud tooone de hello siguientes motivos:

* Hola cuenta de servicios multimedia no se encuentra o se ha eliminado.
* se deshabilita la cuenta de servicios multimedia de Hola y tipo de solicitud de hello no es HTTP GET. Las operaciones de servicio devolverán también la respuesta 403.
* Hello token de autenticación no contiene información de credenciales del usuario de hello: AccountName o Id. de suscripción. Puede encontrar esta información en hello extensión de interfaz de usuario de servicios multimedia para su cuenta de servicios multimedia en hello Portal de administración de Azure.
* no se pueden tener acceso a recursos de Hola.
  
  * Fue un intento realizado toouse un MediaProcessor que no está disponible para su cuenta de servicios multimedia.
  * Se ha intentado tooupdate JobTemplate definida por servicios multimedia.
  * Fue un intento realizado toooverwrite localizador alguna otra cuenta de servicios multimedia del.
  * Fue un intento realizado toooverwrite ContentKey algunos otros servicios multimedia de la cuenta.
* no se pudo crear el recurso de Hello debido tooa cuota de servicio que se ha alcanzado para la cuenta de servicios multimedia de Hola. Para obtener más información acerca de las cuotas de servicio de hello, consulte [cuotas y limitaciones](media-services-quotas-and-limitations.md).

## <a name="404-not-found"></a>404 No encontrado
no se permite la solicitud de Hello en un recurso tooone vencimiento de hello siguientes motivos:

* Fue un intento realizado tooupdate una entidad que no existe.
* Fue un intento realizado toodelete una entidad que no existe.
* Fue un intento realizado toocreate una entidad que se vincula la entidad tooan que no existe.
* Fue un intento realizado tooGET una entidad que no existe.
* Fue un intento realizado toospecify una cuenta de almacenamiento que no está asociada a la cuenta de servicios multimedia de Hola.  

## <a name="409-conflict"></a>409 Conflicto
no se permite debido Hola solicitud tooone de hello siguientes motivos:

* AssetFile más de una con nombre especificado de hello en hello activo.
* Se produjo un intento toocreate un segundo principal AssetFile dentro de hello activo.
* Se produjo un intento toocreate una ContentKey con hello especificado identificador ya en uso.
* Se produjo un intento toocreate un localizador con hello especificado identificador ya en uso.
* Más de un IngestManifestFile con nombre especificado de hello en hello IngestManifest.
* Fue un intento realizado toolink un segundo toohello de ContentKey de cifrado de almacenamiento activo cifrados de almacenamiento.
* Se produjo un intento toolink Hola mismo ContentKey toohello activo.
* Se ha intentado toocreate un tooan de localizador activo cuyo contenedor de almacenamiento falta o ya no está asociada a Hola activo.
* Fue un intento realizado toocreate un tooan de localizador activo que ya tiene 5 localizadores en uso. (Almacenamiento de azure impone límite de Hola de cinco directivas de acceso compartido en un contenedor de almacenamiento).
* Vincular cuenta de almacenamiento de un tooan Asset IngestManifestAsset no es Hola igual que la cuenta de almacenamiento de hello usa primario hello IngestManifest.  

## <a name="500-internal-server-error"></a>Error de servidor interno 500
Durante el procesamiento de saludo de solicitud de hello, servicios multimedia encuentra algún error que impide el procesamiento de hello impide continuar. Esto puede deberse tooone de hello siguientes motivos:

* Crear un activo o trabajo produce un error porque no está disponible temporalmente información de cuota de servicio de la cuenta de servicios multimedia de Hola.
* Creación de un contenedor de almacenamiento de blobs activos o IngestManifest produce un error porque la información de cuenta de almacenamiento de la cuenta de hello no está disponible temporalmente.
* Otro error inesperado.

## <a name="503-service-unavailable"></a>Servicio no disponible 503
servidor de Hello es tooreceive actualmente, no solicitudes. Este error puede deberse a servicio de toohello un exceso de solicitudes. Servicios multimedia de mecanismo de limitación restringe el uso de recursos de Hola para aplicaciones que realizan el servicio de toohello solicitudes excesivas.

> [!NOTE]
> Comprobación de hello error mensajes y errores código cadena tooget obtener más información sobre el motivo de Hola que se obtuvo Hola error 503. Este error no siempre implica limitación.
> 
> 

Los estados posibles son:

* "El servidor está ocupado. Las ejecuciones anteriores de este tipo de solicitud tardaron más de {0} segundos".
* "El servidor está ocupado. Se pueden limitar más de {0} solicitudes por segundo".
* "El servidor está ocupado. Se pueden limitar más de {0} solicitudes en {1} segundos".

toohandle este error, se recomienda utilizar lógica de reintento de retroceso exponencial. Eso significa usar progresivamente esperas más largas entre reintentos para respuestas de error consecutivas.  Para más información, consulte [Bloque de aplicación de control de errores transitorios](https://msdn.microsoft.com/library/hh680905.aspx).

> [!NOTE]
> Si utilizas [SDK de servicios multimedia de Azure para .net](https://github.com/Azure/azure-sdk-for-media-services/tree/master), se ha implementado lógica de reintento de hello para el error 503 Hola Hola SDK.  
> 
> 

## <a name="see-also"></a>Otras referencias
[Códigos de error de administración de Media Services](http://msdn.microsoft.com/library/windowsazure/dn167016.aspx)

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

