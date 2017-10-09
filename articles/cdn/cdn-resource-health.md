---
title: estado de hello aaaMonitor de recursos de red CDN de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomonitor Hola mantenimiento de los recursos de red CDN de Azure mediante el mantenimiento de recursos de Azure."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a>Supervisar el estado de Hola de recursos de red CDN de Azure
  
El estado de los recursos de la red CDN de Azure es un subconjunto de [Estado de los recursos de Azure](../resource-health/resource-health-overview.md).  Puede utilizar Mantenimiento de hello toomonitor Azure recursos de mantenimiento de recursos de red CDN y problemas de tootroubleshoot las instrucciones de recepción.

>[!IMPORTANT] 
>Mantenimiento de recursos de red CDN de Azure actualmente solo las cuentas para el estado de Hola de entrega de CDN global y funciones de API.  El estado de los recursos de la red CDN de Azure no comprueba los puntos de conexión individuales de la red CDN.
>
>señales de Hello esa fuente mantenimiento de recursos de red CDN de Azure pueden ser up too15 minutos.

## <a name="how-toofind-azure-cdn-resource-health"></a>¿Cómo toofind mantenimiento de recursos de red CDN de Azure

1. Hola [portal de Azure](https://portal.azure.com), examinar el perfil de CDN tooyour.

2. Haga clic en hello **configuración** botón.

    ![Botón Configuración](./media/cdn-resource-health/cdn-profile-settings.png)

3. En *Soporte y solución de problemas*, haga clic en **Estado de los recursos**.

    ![Estado de los recursos de la red CDN](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
>También puede encontrar recursos de red CDN enumerados en hello *estado de los recursos* el icono Servicios hello *ayuda y soporte técnico* hoja.  ¿Puede obtener demasiado rápidamente*ayuda y soporte técnico* haciendo clic en hello en un círculo **?** en hello esquina superior derecha del portal de Hola.
>
> ![Ayuda y soporte técnico](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a>Mensajes específicos de la red CDN de Azure

Mantenimiento de recursos de red CDN de Estados tooAzure relacionado se encuentra por debajo.

|Message | Acción recomendada |
|---|---|
|Es posible que haya detenido, quitado o configurado de forma incorrecta uno o más de los puntos de conexión de la red CDN. | Es posible que haya detenido, quitado o configurado de forma incorrecta uno o más de los puntos de conexión de la red CDN.|
|Lo sentimos, el servicio de administración de red CDN Hola no está disponible actualmente | Vuelva aquí para las actualizaciones de estado; comprobar Si el problema persiste después de hello espera el tiempo de resolución, póngase en contacto con el soporte técnico.|
|Es posible que los puntos de conexión de la red CDN se vean afectados por problemas continuos con algunos de nuestros proveedores de redes CDN. | Vuelva aquí para las actualizaciones de estado; comprobar Usar toolearn de herramienta de solución de problemas de hello cómo tootest su origen y el punto de conexión de red CDN; Si el problema persiste después de hello espera el tiempo de resolución, póngase en contacto con el soporte técnico. |
|Los cambios de configuración en los puntos de conexión de la red CDN están experimentando retrasos en la propagación. | Vuelva aquí para las actualizaciones de estado; comprobar Si los cambios de configuración no se ha propagado completamente en el tiempo de espera de hello, póngase en contacto con el soporte técnico.|
|Lo sentimos, que estamos sufriendo problemas el cargar portal complementario de Hola | Vuelva aquí para las actualizaciones de estado; comprobar Si el problema persiste después de hello espera el tiempo de resolución, póngase en contacto con el soporte técnico.|
Tenemos problemas con algunos de nuestros proveedores de red CDN. | Vuelva aquí para las actualizaciones de estado; comprobar Si el problema persiste después de hello espera el tiempo de resolución, póngase en contacto con el soporte técnico. |

## <a name="next-steps"></a>Pasos siguientes

- [Información general sobre el estado de los recursos de Azure](../resource-health/resource-health-overview.md)
- [Solución de problemas de la compresión en la red CDN](./cdn-troubleshoot-compression.md)
- [Solución de problemas de errores 404](./cdn-troubleshoot-endpoint.md)