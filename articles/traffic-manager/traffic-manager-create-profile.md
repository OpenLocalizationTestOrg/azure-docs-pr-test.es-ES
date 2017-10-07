---
title: aaaCreate un perfil de Traffic Manager de Azure | Documentos de Microsoft
description: "Este artículo se describe cómo toocreate un perfil de Traffic Manager"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: kumud
ms.openlocfilehash: 5cd3d2903552c9a0427da41a73f6f38f6b0afc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-traffic-manager-profile"></a>Crear un perfil de Traffic Manager

Este artículo se describe cómo un perfil con **prioridad** tipo de enrutamiento se puede crear puntos de conexión de tooroute usuarios tootwo aplicaciones Web de Azure. Mediante el uso de hello **prioridad** enrutamiento tipo, todo el tráfico es enrutado toohello primer extremo mientras hello en segundo lugar se mantiene como una copia de seguridad. Como resultado, los usuarios pueden ser enrutado toohello segundo extremo si el primer punto de conexión de hello pasa a ser incorrecto.

En este artículo, dos puntos de conexión de aplicación Web de Azure creados anteriormente son perfil de Traffic Manager asociado toothis recién creado. más información acerca de cómo toolearn toocreate puntos de conexión de aplicación Web de Azure, visite hello [página de documentación de aplicaciones Web de Azure](https://docs.microsoft.com/azure/app-service-web/). Puede agregar cualquier punto de conexión que tiene un nombre DNS y sea accesible por Hola internet pública y que estamos usando los extremos de aplicaciones Web de Azure como ejemplo.

### <a name="create-a-traffic-manager-profile"></a>Crear un perfil de Traffic Manager
1. Desde un explorador, inicie sesión en toohello [portal de Azure](http://portal.azure.com). Si aún no tiene cuenta, puede registrarse para obtener una [evaluación gratuita durante un mes](https://azure.microsoft.com/free/). 
2. En hello **concentrador** menú, haga clic en **New** > **red** > **ver todas**, haga clic en **tráfico Administrador de** hello tooopen de perfil **perfil del Administrador de tráfico crear** hoja, a continuación, haga clic en **crear**.
3. En hello **crear Traffic Manager perfil** hoja, completa, como sigue:
    1. En **Nombre**, proporcione un nombre para el perfil. Este nombre debe toobe único dentro de la zona de trafficmanager.net hello y da lugar a nombre DNS de hello <name>, trafficmanager.net que es tooaccess usa el perfil de Traffic Manager.
    2. En **método de enrutamiento**, seleccione hello **prioridad** método de enrutamiento.
    3. En **suscripción**, seleccione suscripción Hola desees toocreate este perfil en
    4. En **grupo de recursos**, crear un nuevo tooplace de grupo de recursos de este perfil en.
    5. En **ubicación del grupo de recursos**, Seleccionar ubicación de Hola Hola del grupo de recursos. Esta configuración hace referencia toohello ubicación del grupo de recursos de hello y no tiene ningún efecto en el perfil de Traffic Manager que se va a implementar todo el mundo Hola.
    6. Haga clic en **Crear**.
    7. Una vez completada la implementación global Hola de su perfil de Traffic Manager, se muestra en el grupo de recursos correspondiente como uno de los recursos de Hola.

    ![Crear un perfil de Traffic Manager](./media/traffic-manager-create-profile/Create-traffic-manager-profile.png)

## <a name="add-traffic-manager-endpoints"></a>Incorporación de puntos de conexión de Traffic Manager

1. En la barra de búsqueda del portal de hello, busque hello **perfil de Traffic Manager** nombre que creó en hello anterior sección y haga clic en perfil de administrador de tráfico de Hola Hola resultados que muestra de Hola.
2. Hola **perfil de Traffic Manager** hoja en hello **configuración** sección, haga clic en **extremos**.
3. Hola **extremos** hoja que se muestra, haga clic en **agregar**.
4. Hola **Agregar extremo** hoja, completa, como sigue:
    1. En **Tipo**, haga clic en **Punto de conexión de Azure**.
    2. Proporcionar un **nombre** por los que desea toorecognize este punto de conexión.
    3. En **Tipo de recurso de destino**, haga clic en **App Service**.
    4. Para **recurso de destino**, haga clic en **elegir un servicio de aplicaciones** tooshow anuncio de Hola de hello las aplicaciones Web en hello misma suscripción. Hola **recursos** hoja que se muestra, Hola de selección que desee tooadd Hola el primer punto de conexión de servicio de aplicaciones.
    5. En **Prioridad**, seleccione **1**. Esto se produce en todo el tráfico encaminado toothis extremo si es correcto.
    6. No active la opción **Agregar como deshabilitado**.
    7. Haga clic en **Aceptar**
5.  Repita los pasos 3 y 4 para el punto de conexión de hello siguiente aplicaciones Web de Azure. Asegúrese de que tooadd con su **prioridad** valor establecido en **2**.
6.  Cuando se completa la adición de Hola de ambos extremos, se muestran en hello **perfil de Traffic Manager** hoja junto con su estado de supervisión como **Online**.

    ![Incorporación de un punto de conexión de Traffic Manager](./media/traffic-manager-create-profile/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Usar perfil de Traffic Manager Hola
1.  En la barra de búsqueda del portal de hello, busque hello **perfil de Traffic Manager** nombre que creó en la sección anterior de Hola. En los resultados de Hola que se muestran, haga clic en perfil del Administrador de tráfico de Hola.
2. Hola **perfil de Traffic Manager** hoja, haga clic en **Introducción**.
3. Hola **perfil de Traffic Manager** hoja muestra el nombre DNS de Hola de su perfil de Traffic Manager recién creado. Esto se puede utilizar cualquier extremo derecho de los clientes (por ejemplo, desplazándose tooit mediante un explorador web) tooget enrutado toohello determinado por el tipo de enrutamiento de Hola. En este caso, todas las solicitudes son toohello enrutado primer punto de conexión y si Traffic Manager detecta ser incorrecto, tráfico de hello conmuta por error automáticamente toohello siguiente punto de conexión.

## <a name="delete-hello-traffic-manager-profile"></a>Eliminar perfil de Traffic Manager Hola
Cuando ya no es necesario, eliminar el grupo de recursos de Hola y perfil de Traffic Manager de Hola que haya creado. toodo seleccione por lo tanto, el grupo de recursos de Hola de hello **perfil de Traffic Manager** hoja y haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

- Más información sobre los [tipos de enrutamiento](traffic-manager-routing-methods.md).
- Más información sobre los [tipos de punto de conexión](traffic-manager-endpoint-types.md).
- Más información sobre la [supervisión de los puntos de conexión](traffic-manager-monitoring.md).



