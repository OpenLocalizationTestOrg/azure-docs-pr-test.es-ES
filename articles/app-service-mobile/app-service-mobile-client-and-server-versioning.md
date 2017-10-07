---
title: "versiones SDK aaaClient y el servidor de aplicaciones móviles y servicios móviles | Documentos de Microsoft"
description: "Lista de SDK de cliente y compatibilidad con versiones de SDK de servidor para Servicios móviles y Aplicaciones móviles de Azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a>Control de versiones de cliente y servidor en Aplicaciones móviles y Servicios móviles
versión más reciente de Hello de servicios móviles de Azure es hello **aplicaciones móviles** característica del servicio de aplicaciones de Azure.

Hola cliente de aplicaciones móviles y SDK de servidor originalmente se basa en los de servicios móviles, pero son *no* compatibles entre sí.
Es decir, debe usar el SDK de cliente de *Mobile Apps* con un SDK de servidor de *Mobile Apps* y algo parecido sucede con *Mobile Services*. Este contrato se establece a través de un valor de encabezado especial utilizado por hello cliente y servidor de SDK, `ZUMO-API-VERSION`.

Nota: cada vez que este documento hace referencia tooa *servicios móviles* back-end, no es necesario toobe hospedada en servicios móviles. Ahora es posible toomigrate un toorun de servicio móvil en el servicio de aplicaciones sin realizar ningún cambio en el código, pero todavía sería utilizar el servicio de hello *servicios móviles* versiones del SDK.

toolearn Obtenga más información sobre migración tooApp servicio sin realizar ningún cambio de código, vea el artículo de hello [migrar un servicio de aplicaciones de servicio móvil tooAzure].

## <a name="header-specification"></a>Especificación del encabezado
clave de Hello `ZUMO-API-VERSION` se pueden especificar en el encabezado HTTP de Hola o de cadena de consulta de Hola. valor de Hello es una cadena de versión en forma de hello **x.y.z**.

Por ejemplo:

GET https://service.azurewebsites.net/tables/TodoItem

HEADERS: ZUMO-API-VERSION: 2.0.0

POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0

## <a name="opting-out-of-version-checking"></a>Anulación de la comprobación de la versión
Puede optar por comprobación estableciendo el valor de la versión **true** para la configuración de la aplicación hello **MS_SkipVersionCheck**. Especifique en el archivo web.config o en la sección de configuración de la aplicación de portal de Azure Hola Hola.

> [!NOTE]
> Hay una serie de cambios de comportamiento entre servicios móviles y aplicaciones móviles, especialmente en las áreas de Hola de sincronización sin conexión, la autenticación y las notificaciones de inserción. Solo debe rechazar comprobación después de tooensure prueba completa que estos cambios de comportamiento no interrumpe la funcionalidad de la aplicación de la versión.
>
>

## <a name="summary-of-compatibility-for-all-versions"></a>Resumen de compatibilidad para todas las versiones
gráfico de Hello siguiente muestra la compatibilidad de hello entre todos los tipos de cliente y servidor. Un back-end se clasifica como cualquier Mobile **servicios** o Mobile **aplicaciones** basado en servidor hello SDK que utiliza.

|  | **Servicios móviles** | **Aplicaciones móviles** |
| --- | --- | --- |
| [Clientes de Servicios móviles] |Aceptar |Error\* |
| [Clientes de Aplicaciones móviles] |Error\* |Aceptar |

\*Para controlarlo, especifique **MS_SkipVersionCheck**.

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <a name="1.0.0"></a>Cliente y servidor de Servicios móviles
SDK de cliente de Hello en tabla Hola siguiente son compatibles con **servicios móviles**.

Nota: Hola SDK de cliente de servicios móviles *no* enviar un valor de encabezado `ZUMO-API-VERSION`. Si el servicio de hello recibe este encabezado o el valor de cadena de consulta, se devolverá un error, a menos que explícitamente optó por tal y como se ha descrito anteriormente.

### <a name="MobileServicesClients"></a> SDK de cliente de *Servicios* móviles
| Plataforma de cliente | Versión | Valor de encabezado de versión |
| --- | --- | --- |
| Cliente administrado (Windows, Xamarin) |[1.3.2](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |N/D |
| iOS |[2.2.2](http://aka.ms/gc6fex) |N/D |
| Android |[2.0.3](https://go.microsoft.com/fwLink/?LinkID=280126) |N/D |
| HTML |[1.2.7](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |N/D |

### <a name="mobile-services-server-sdks"></a>SDK de servidor de *Servicios* móviles
| Plataforma de servidor | Versión | Encabezado de versión aceptado |
| --- | --- | --- |
| .NET |[WindowsAzure.MobileServices.Backend.* Versión 1.0.x](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |** Ningún encabezado de versión ** |
| Node.js |(próximamente) |**Ningún encabezado de versión** |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a>Comportamiento de back-ends de Servicios móviles
| ZUMO-API-VERSION | Valor de MS_SkipVersionCheck | Response |
| --- | --- | --- |
| Sin especificar |Cualquiera |200 - CORRECTO |
| Cualquier valor |True |200 - CORRECTO |
| Cualquier valor |False/Sin especificar |400 - Solicitud incorrecta |

## <a name="2.0.0"></a>Cliente y servidor de Aplicaciones móviles de Azure
### <a name="MobileAppsClients"></a> SDK de cliente de *Aplicaciones* móviles
Comprobación de la versión se incorpora a partir de hello después de las versiones de SDK de cliente de Hola para **aplicaciones móviles de Azure**:

| Plataforma de cliente | Versión | Valor de encabezado de versión |
| --- | --- | --- |
| Cliente administrado (Windows, Xamarin) |[2.0.0](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |2.0.0 |
| iOS |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=529823) |2.0.0 |
| Android |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |3.0.0 |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a>SDK de servidor de *Aplicaciones* móviles
La comprobación de versión se incluye en las siguientes versiones del SDK de servidor:

| Plataforma de servidor | SDK | Encabezado de versión aceptado |
| --- | --- | --- |
| .NET |[Microsoft.Azure.Mobile.Server](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |2.0.0 |
| Node.js |[azure-mobile-apps)](https://www.npmjs.com/package/azure-mobile-apps) |2.0.0 |

### <a name="behavior-of-mobile-apps-backends"></a>Comportamiento de back-ends de Aplicaciones móviles
| ZUMO-API-VERSION | Valor de MS_SkipVersionCheck | Response |
| --- | --- | --- |
| x.y.z o Null |True |200 - CORRECTO |
| Null |False/Sin especificar |400 - Solicitud incorrecta |
| 1.x.y |False/Sin especificar |400 - Solicitud incorrecta |
| 2.0.0-2.x.y |False/Sin especificar |200 - CORRECTO |
| 3.0.0-3.x.y |False/Sin especificar |400 - Solicitud incorrecta |

## <a name="next-steps"></a>Pasos siguientes
* [migrar un servicio de aplicaciones de servicio móvil tooAzure]

[Clientes de Servicios móviles]: #MobileServicesClients
[Clientes de Aplicaciones móviles]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[migrar un servicio de aplicaciones de servicio móvil tooAzure]: app-service-mobile-migrating-from-mobile-services.md
