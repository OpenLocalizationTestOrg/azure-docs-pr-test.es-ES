---
title: "los puntos de conexión aaaManage en Azure Traffic Manager | Documentos de Microsoft"
description: "Este artículo le ayudará a agregar, quitar, habilitar y deshabilitar extremos del Administrador de tráfico de Azure."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: ade2bbc2-35a7-43c5-8001-4698f7254526
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kumud
ms.openlocfilehash: fc65874ae2eaeb6fca5d8c4f33403c258307bdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-disable-enable-or-delete-endpoints"></a>Incorporación, deshabilitación, habilitación o eliminación de puntos de conexión

característica de las aplicaciones Web de Hello en el servicio de aplicación de Azure ya proporciona la funcionalidad de enrutamiento de tráfico de round robin para sitios Web en un centro de datos, independientemente del modo del sitio Web de Hola y de conmutación por error. Azure Traffic Manager permite toospecify conmutación por error y el enrutamiento del tráfico de round robin para los servicios de nube y sitios Web en distintos centros de datos. Hola primer paso es necesario tooprovide que la funcionalidad es tooadd Hola en la nube sitio Web o servicio de punto de conexión tooTraffic Manager.

También puede deshabilitar los extremos individuales que forman parte de un perfil del Administrador de tráfico. Deshabilitar un punto de conexión, este sigue formando parte del perfil de hello, pero el perfil de hello actúa como si Hola extremo no estuviera incluido en ella. Esta acción es útil para quitar temporalmente un punto de conexión que se encuentre en modo de mantenimiento o que se vaya a implementar. Una vez que Hola extremo activo y ejecutándose, se puede habilitar.

> [!NOTE]
> Deshabilitar un punto de conexión no tiene nada toodo con su estado de implementación en Azure. Un extremo en buen estado permanece arriba y puede tooreceive tráfico incluso cuando está deshabilitado en el Administrador de tráfico. Además, al deshabilitar un extremo de un perfil, no se afecta al estado en otro perfil.

## <a name="tooadd-a-cloud-service-or-an-app-service-endpoint-tooa-traffic-manager-profile"></a>tooadd un servicio de nube o un punto de conexión de servicio aplicación tooa perfil de Traffic Manager

1. Desde un explorador, inicie sesión en toohello [portal de Azure](http://portal.azure.com).
2. En la barra de búsqueda del portal de hello, busque hello **perfil de Traffic Manager** nombre que desee toomodify y, a continuación, haga clic en el perfil de Traffic Manager de Hola Hola resultados que muestra de Hola.
3. Hola **perfil de Traffic Manager** hoja en hello **configuración** sección, haga clic en **extremos**.
4. Hola **extremos** hoja que se muestra, haga clic en **agregar**.
5. Hola **Agregar extremo** hoja, completa, como sigue:
    1. En **Tipo**, haga clic en **Punto de conexión de Azure**.
    2. Proporcionar un **nombre** por los que desea toorecognize este punto de conexión.
    3. Para **tipo de recurso de destino**, de Hola lista desplegable, elija tipo de recurso apropiado Hola.
    4. Para **recurso de destino**, de Hola lista desplegable, elija el recurso de destino adecuado de hello tooshow recursos de anuncio de Hola en Hola misma suscripción Hola **hoja de recursos**. Hola **recursos** hoja que se muestra, servicio de Hola de selección que desee tooadd como Hola el primer punto de conexión.
    5. En **Prioridad**, seleccione **1**. Esto se produce en todo el tráfico encaminado toothis extremo si es correcto.
    6. No active la opción **Agregar como deshabilitado**.
    7. Haga clic en **Aceptar**
6.  Repita los pasos 4 y 5 tooadd hello Azure punto de conexión siguiente. Asegúrese de que tooadd con su **prioridad** valor establecido en **2**.
7.  Cuando se completa la adición de Hola de ambos extremos, se muestran en hello **perfil de Traffic Manager** hoja junto con su estado de supervisión como **Online**.

> [!NOTE]
> Después de agregar o quitar un punto de conexión de un perfil mediante hello *conmutación por error* método de enrutamiento de tráfico, la lista de prioridad de conmutación por error de hello no se puede pedir como desee. Puede ajustar el orden de Hola de hello lista de prioridad de conmutación por error en la página de configuración de Hola. Para obtener más información, consulte [Método de enrutamiento del tráfico de conmutación por error](traffic-manager-configure-failover-routing-method.md).

## <a name="toodisable-an-endpoint"></a>toodisable un punto de conexión

1. Desde un explorador, inicie sesión en toohello [portal de Azure](http://portal.azure.com).
2. En la barra de búsqueda del portal de hello, busque hello **perfil de Traffic Manager** nombre que desee toomodify y, a continuación, haga clic en el perfil de Traffic Manager de hello en los resultados de Hola que se muestran.
3. Hola **perfil de Traffic Manager** hoja en hello **configuración** sección, haga clic en **extremos**. 
4. Haga clic en el punto de conexión de Hola que desea toodisable y, a continuación, en hello **extremo** hoja que se muestra, haga clic en **editar**.
5. Hola **extremo** hoja, también cambian el estado de punto de conexión de hello**deshabilitado**y, a continuación, haga clic en **guardar**.
6. Los clientes siguen el punto de conexión de toosend tráfico toohello durante Hola del período de vida (TTL). Puede cambiar Hola TTL en página de configuración de Hola de hello perfil de Traffic Manager.

## <a name="tooenable-an-endpoint"></a>tooenable un punto de conexión

1. Desde un explorador, inicie sesión en toohello [portal de Azure](http://portal.azure.com).
2. En la barra de búsqueda del portal de hello, busque hello **perfil de Traffic Manager** nombre que desee toomodify y, a continuación, haga clic en el perfil de Traffic Manager de hello en los resultados de Hola que se muestran.
3. Hola **perfil de Traffic Manager** hoja en hello **configuración** sección, haga clic en **extremos**. 
4. Haga clic en el punto de conexión de Hola que desea toodisable y, a continuación, en hello **extremo** hoja que se muestra, haga clic en **editar**.
5. Hola **extremo** hoja, también cambian el estado de punto de conexión de hello**habilitado**y, a continuación, haga clic en **guardar**.
6. Los clientes siguen el punto de conexión de toosend tráfico toohello durante Hola del período de vida (TTL). Puede cambiar Hola TTL en página de configuración de Hola de hello perfil de Traffic Manager.

## <a name="toodelete-an-endpoint"></a>toodelete un punto de conexión

1. Desde un explorador, inicie sesión en toohello [portal de Azure](http://portal.azure.com).
2. En la barra de búsqueda del portal de hello, busque hello **perfil de Traffic Manager** nombre que desee toomodify y, a continuación, haga clic en el perfil de Traffic Manager de hello en los resultados de Hola que se muestran.
3. Hola **perfil de Traffic Manager** hoja en hello **configuración** sección, haga clic en **extremos**. 
4. Haga clic en el punto de conexión de Hola que desea toodisable y, a continuación, en hello **extremo** hoja que se muestra, haga clic en **editar**.
5. Hola **extremo** hoja, también cambian el estado de punto de conexión de hello**habilitado**y, a continuación, haga clic en **guardar**.


## <a name="next-steps"></a>Pasos siguientes

* [Administración de perfiles de Traffic Manager](traffic-manager-manage-profiles.md)
* [Configurar métodos de enrutamiento](traffic-manager-configure-routing-method.md)
* [Solución de problemas de estado degradado del Administrador de tráfico](traffic-manager-troubleshooting-degraded.md)
* [Consideraciones de rendimiento sobre el Administrador de tráfico](traffic-manager-performance-considerations.md)
* [Operaciones del Administrador de tráfico (referencia de la API de REST)](http://go.microsoft.com/fwlink/p/?LinkID=313584)

