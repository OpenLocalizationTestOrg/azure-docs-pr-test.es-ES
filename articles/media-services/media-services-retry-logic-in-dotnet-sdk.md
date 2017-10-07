---
title: "lógica de aaaRetry en hello SDK de servicios multimedia para .NET | Documentos de Microsoft"
description: "tema de Hola encontrará un resumen de la lógica de reintento en hello SDK de servicios multimedia para. NET."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 527b61a6-c862-4bd8-bcbc-b9aea1ffdee3
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako
ms.openlocfilehash: 18d0a9d68e55a48bc769fb6ae5711ddba78ed8e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="retry-logic-in-hello-media-services-sdk-for-net"></a>Vuelva a intentar la lógica de hello SDK de servicios multimedia para .NET
Cuando se trabaja con servicios de Microsoft Azure, pueden producirse errores transitorios. Si se produce un error transitorio, en la mayoría de los casos, después de unos cuantos reintentos hello operación se realiza correctamente. Hola SDK de servicios multimedia para .NET implementa Hola Reintentar lógica toohandle errores transitorios asociados a las excepciones y errores provocados por las solicitudes web, ejecutar consultas, guardar los cambios y operaciones de almacenamiento.  De forma predeterminada, Hola SDK de servicios multimedia para .NET ejecuta cuatro reintentos antes de volver a iniciar la aplicación de hello excepción tooyour. código de Hello de la aplicación debe controlar correctamente esta excepción.  

 Hola te mostramos una breve guía sobre las directivas de solicitud de servicio Web, almacenamiento, consulta y SaveChanges:  

* Hola directiva de almacenamiento se utiliza para las operaciones de almacenamiento de blob (carga o descarga de archivos de recursos).  
* Hola directiva de solicitud de servicio Web se utiliza para las solicitudes web genérico (por ejemplo, para obtener token de autenticación y resolución de punto de conexión de clúster de los usuarios de hello).  
* Hola directiva de consulta se utiliza para consultar entidades de REST (por ejemplo, mediaContext.Assets.Where(...)).  
* Hola SaveChanges directiva se usa para hacer todo lo que cambia los datos de servicio de hello (por ejemplo, crear una entidad actualizar una entidad, una llamada a una función de servicio para una operación).  
  
  Este tema enumeran los tipos de excepción y lógica de reintento de códigos de error que se administran con hello SDK de servicios multimedia para. NET.  

## <a name="exception-types"></a>Tipos de excepciones
Hello siguiente tabla describe las excepciones que hello SDK de servicios multimedia para .NET controla o no controla para algunas operaciones que pueden causar errores transitorios.  

| Excepción | Solicitud web | Almacenamiento | Consultar | SaveChanges |
| --- | --- | --- | --- | --- |
| WebException<br/>Para obtener más información, vea hello [códigos de estado de WebException](media-services-retry-logic-in-dotnet-sdk.md#WebExceptionStatus) sección. |Sí |Sí |Sí |Sí |
| DataServiceClientException<br/> Para obtener más información, consulte [Códigos de estado de error HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |No |Sí |Sí |Sí |
| DataServiceQueryException<br/> Para obtener más información, consulte [Códigos de estado de error HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |No |Sí |Sí |yes |
| DataServiceRequestException<br/> Para obtener más información, consulte [Códigos de estado de error HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |No |Sí |Sí |Sí |
| DataServiceTransportException |No |No |Sí |Sí |
| TimeoutException |Sí |Sí |Sí |No |
| SocketException |Sí |Sí |Sí |yes |
| StorageException |No |Sí |No |No |
| IOException |No |Sí |No |No |

### <a name="WebExceptionStatus"></a> Códigos de estado WebException
Hello siguiente tabla muestra qué error de WebException se implementa la lógica de reintento de Hola de códigos. Hola [WebExceptionStatus](http://msdn.microsoft.com/library/system.net.webexceptionstatus.aspx) enumeración define los códigos de estado de Hola.  

| Estado | Solicitud web | Almacenamiento | Consultar | SaveChanges |
| --- | --- | --- | --- | --- |
| ConnectFailure |Sí |Sí |Sí |Sí |
| NameResolutionFailure |yes |Sí |Sí |Sí |
| ProxyNameResolutionFailure |Sí |Sí |Sí |yes |
| SendFailure |Sí |Sí |Sí |yes |
| PipelineFailure |yes |Sí |Sí |No |
| ConnectionClosed |yes |Sí |Sí |No |
| KeepAliveFailure |yes |Sí |Sí |No |
| UnknownError |Sí |Sí |Sí |No |
| ReceiveFailure |Sí |Sí |Sí |No |
| RequestCanceled |Sí |Sí |Sí |No |
| Tiempo de espera |Sí |Sí |Sí |No |
| ProtocolError <br/>reintento de Hello en ProtocolError se controla mediante el control de código de estado HTTP de Hola. Para obtener más información, consulte [Códigos de estado de error HTTP](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |yes |Sí |Sí |Sí |

### <a name="HTTPStatusCode"></a> Códigos de estado de error HTTP
Cuando las operaciones de consulta y SaveChanges producen DataServiceClientException, DataServiceQueryException o DataServiceQueryException, Hola código de estado de error HTTP se devuelve en hello propiedad StatusCode.  Hello tabla siguiente muestran para los códigos de error se implementa la lógica de reintento de Hola.  

| Estado | Solicitud web | Almacenamiento | Consultar | SaveChanges |
| --- | --- | --- | --- | --- |
| 401 |No |Sí |No |No |
| 403 |No |Sí<br/>Administración de reintentos con esperas más prolongadas. |No |No |
| 408 |yes |Sí |Sí |Sí |
| 429 |Sí |Sí |Sí |yes |
| 500 |Sí |Sí |Sí |No |
| 502 |yes |Sí |Sí |No |
| 503 |Sí |Sí |Sí |Sí |
| 504 |Sí |Sí |Sí |No |

Si desea tootake un vistazo a la implementación real de Hola de hello SDK de servicios multimedia para la lógica de reintento. NET, vea [azure sdk de media services](https://github.com/Azure/azure-sdk-for-media-services/tree/dev/src/net/Client/TransientFaultHandling).

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

