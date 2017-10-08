---
title: "solicitud de aaaAdvanced limitación con administración de API de Azure"
description: "Obtenga información acerca de cómo toocreate y aplicar una cuota flexible y las directivas de administración de API de Azure de limitación de velocidad."
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: ac87f83118a37bd587fddf044e5c2d6fc2af9031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a>Limitación avanzada de solicitudes con Administración de API de Azure
Ser capaz de toothrottle las solicitudes entrantes es una función clave de administración de API de Azure. Ya sea mediante la tasa de hello control de solicitudes u Hola total de solicitudes/datos transferidos, administración de API permite API proveedores tooprotect sus API de abuso y crear el valor de distintos niveles de producto de API.

## <a name="product-based-throttling"></a>Limitación por producto
toodate, las capacidades de limitación de velocidad de hello ha sido limitado toobeing ámbito tooa determinado producto suscripción (básicamente una clave), se definen en hello portal para desarrolladores de administración de API. Esto es útil para los límites de tooapply de proveedor de API de hello en los programadores de Hola que se suscribieron toouse su API, sin embargo, no ayuda, por ejemplo, en el límite de usuarios finales individuales de hello API. Es posible que el único usuario de tooconsume de aplicación del desarrollador de Hola Hola cuota todo y, a continuación, impedir que otros clientes de desarrollador de hello toouse capaz de aplicación de hello. Además, varios clientes que podrían generar un gran volumen de solicitudes pueden limitar a los usuarios de acceso toooccasional.

## <a name="custom-key-based-throttling"></a>Limitación por clave personalizada
Hola nueva [límite de velocidad por clave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) y [cuota por clave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) las directivas proporcionan un control de tootraffic solución significativamente más flexible. Estas nuevas directivas le permiten toodefine expresiones tooidentify hello las claves que serán usado tootrack uso del tráfico. Hola funcionamiento Esto se ilustra lo más sencillo con un ejemplo. 

## <a name="ip-address-throttling"></a>Limitación por dirección IP
las siguientes directivas Hello restringen un único cliente IP dirección tooonly 10 llama a cada minuto, con un total de 1.000.000 llamadas y 10.000 kilobytes de ancho de banda al mes. 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

Si todos los clientes en Internet de hello usan una dirección IP única, podría tratarse de una manera eficaz para limitar el uso por el usuario. Sin embargo, es bastante probable que varios usuarios compartir una única dirección IP pública debido toothem Hola acceso a Internet a través de un dispositivo NAT. A pesar de ello, para las API que permiten Hola de acceso no autenticado `IpAddress` podría ser mejor opción de Hola.

## <a name="user-identity-throttling"></a>Limitación por identidad de usuario
Si se autentica un usuario final, puede generarse una clave de limitación basada en información que identifica de forma única a ese usuario.

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

En este ejemplo se extraer el encabezado de autorización de hello, conviértala demasiado`JWT` objeto y usar asunto Hola del usuario de hello tooidentify token hello y usarla como clave de limitación de la tasa de Hola. Si la identidad de usuario de Hola se almacena en hello `JWT` como uno de hello otra notificaciones, a continuación, que el valor se podría usar en su lugar.

## <a name="combined-policies"></a>Directivas de combinación
Aunque Hola limitación nuevas directivas proporciona un control más que Hola existente de las directivas de limitación, sigue siendo valor combinar ambas capacidades. Limitación por clave de suscripción de producto ([limitar la tasa de llamadas por suscripción](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) y [establecer la cuota de uso por suscripción](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) es una excelente manera de tooenable monetización de una API con cargo basándose en los niveles de uso. Hello un control más preciso de ser capaz de toothrottle por el usuario es complementario e impide que uno del comportamiento del usuario degradar experiencia Hola de otro. 

## <a name="client-driven-throttling"></a>Limitación controlada por cliente
Cuando Hola limitación clave se define mediante una [expresión de directiva](https://msdn.microsoft.com/library/azure/dn910913.aspx), es proveedor Hola API que está decidiendo si la limitación de hello está en el ámbito. Sin embargo, un desarrollador puede toocontrol cómo valoran limitar sus propios clientes. Esto podría habilitarse por el proveedor de la API de hello introduciendo cliente aplicación toocommunicate Hola clave toohello de un encabezado personalizado tooallow Hola desarrollador API.

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

Esto permite toochoose de aplicación de cliente del desarrollador de hello cómo desean limitación clave de la tasa de toocreate Hola. Con un poco de ingenio un programador del cliente podría crear sus propios niveles de velocidad asignando conjuntos de claves toousers y rotación de uso de claves de Hola.

## <a name="summary"></a>Resumen
Administración de API de Azure proporciona velocidad y quote limitación tooboth protección y agregar servicio de API de tooyour de valor. Hola limitación nuevas directivas con reglas de ámbito personalizadas permite que más precisa control sobre esos tooenable directivas las aplicaciones incluso mejores toobuild de los clientes. ejemplos de Hello en este artículo muestran uso de Hola de estas nuevas directivas de claves con direcciones IP del cliente, identidad de usuario y valores de cliente generado de limitación de la tasa de fabricación. Sin embargo, hay muchas otras partes de mensaje de Hola que podría utilizarse como agente de usuario, fragmentos de ruta de acceso de dirección URL, tamaño del mensaje.

## <a name="next-steps"></a>Pasos siguientes
Envíenos sus comentarios en el subproceso de Disqus Hola de este tema. Sería excelente toohear sobre otros posibles valores de clave que han sido una elección lógica en los escenarios.

## <a name="watch-a-video-overview-of-these-policies"></a>Ver un vídeo de información general de estas directivas
Para obtener más información sobre hello [límite de velocidad por clave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) y [cuota por clave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) las directivas que se describen en este artículo, consulte Hola después de vídeo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

