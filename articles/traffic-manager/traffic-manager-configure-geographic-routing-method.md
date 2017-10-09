---
title: "con Azure Traffic Manager de método de enrutamiento de tráfico aaaConfigure geográfica | Documentos de Microsoft"
description: "Este artículo explica cómo tooconfigure Hola método de enrutamiento de tráfico geográfica con Azure Traffic Manager"
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
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 4142389211ae54e7feea6564641e01e4477491e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-geographic-traffic-routing-method-using-traffic-manager"></a>Configurar método de enrutamiento de tráfico geográfica de Hola por Traffic Manager

Hola método de enrutamiento de tráfico geográfica permite el tráfico de toodirect puntos de conexión de toospecific según Hola ubicación geográfica donde se originan las solicitudes de Hola. Este tutorial muestra cómo generar perfiles de toocreate un administrador de tráfico con este método de enrutamiento y configurar el Hola extremos tooreceive tráfico desde ubicaciones geográficas específicas.

## <a name="create-a-traffic-manager-profile"></a>Creación de un perfil del Administrador de tráfico

1. Desde un explorador, inicie sesión en toohello [portal de Azure](http://portal.azure.com). Si aún no tiene cuenta, puede registrarse para obtener [una evaluación gratuita durante un mes](https://azure.microsoft.com/free/).
2. En el menú del concentrador hello, haga clic en **New** > **red** > **ver todas**y, a continuación, haga clic en **perfil de Traffic Manager**hello tooopen **crear Traffic Manager perfil** hoja.
3. En hello **crear Traffic Manager perfil** hoja:
    1. Proporcione un nombre para el perfil. Este nombre debe toobe único dentro de la zona de trafficmanager.net hello y dará como resultado en nombre DNS de hello <profilename>, trafficmanager.net lo que puede tooaccess usa el perfil de Traffic Manager.
    2. Seleccione hello **geográfico** método de enrutamiento.
    3. Seleccione la suscripción de Hola que desea toocreate este perfil bajo.
    4. Usar un grupo de recursos existente o crear un nuevo tooplace de grupo de recursos de este perfil en. Si elige toocreate un nuevo grupo de recursos, utilice hello **ubicación del grupo de recursos** ubicación de lista desplegable toospecify Hola Hola del grupo de recursos. Esta configuración hace referencia toohello ubicación del grupo de recursos de hello y no tiene ningún efecto en el perfil de Traffic Manager que se va a implementar todo el mundo Hola.
    5. Una vez que haga clic en **Crear**, se creará el perfil de Traffic Manager y se implementará globalmente.

![Crear un perfil de Traffic Manager](./media/traffic-manager-geographic-routing-method/create-traffic-manager-profile.png)

## <a name="add-endpoints"></a>Incorporación de puntos de conexión

1. Busque el nombre del perfil de Traffic Manager de Hola que acaba de crear en la barra de búsqueda del portal de Hola y haga clic en el resultado de hello cuando se muestre.
2. Navegue demasiado**configuración** -> **extremos** en la hoja de hello Traffic Manager.
3. Haga clic en **agregar** tooshow hello **Agregar extremo** hoja.
3. Hola **extremos** hoja, haga clic en **agregar** y Hola **Agregar extremo** hoja que se muestra, complete los siguientes:
4. Seleccione **tipo** según el tipo de saludo de punto de conexión que se va a agregar. En el caso de los perfiles de enrutamiento geográfico que se usan en producción, se recomienda usar tipos de punto de conexión anidado que contengan un perfil secundario con más de un punto de conexión. Para más detalles, consulte [Preguntas más frecuentes sobre los métodos de enrutamiento de tráfico geográfico](traffic-manager-FAQs.md).
5. Proporcionar un **nombre** por los que desea toorecognize este punto de conexión.
6. Algunos de los campos en esta hoja dependen del tipo hello de punto de conexión que se va a agregar:
    1. Si va a agregar un extremo de Azure, seleccione hello **tipo de recurso de destino** hello y **destino** basadas en el recurso de hello desee tráfico de toodirect
    2. Si va a agregar un **externo** punto de conexión, proporcionar hello **nombre de dominio completo (FQDN)** para el punto de conexión.
    3. Si va a agregar un **Nested extremo**, seleccione hello **recurso de destino** correspondiente perfil de toohello secundario que desee toouse y especifique hello **extremos secundarios de mínimo recuento**.
7. Hola sección mapas geográficos, use Hola desplegable regiones de hello tooadd desde donde desea que el punto de conexión de tráfico toobe envía toothis. Debe agregar al menos una región y puede tener asignadas varias regiones.
8. Repita este paso para todos los extremos que desee tooadd en este perfil

![Incorporación de un punto de conexión de Traffic Manager](./media/traffic-manager-geographic-routing-method/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Usar perfil de Traffic Manager Hola
1.  En la barra de búsqueda del portal de hello, busque hello **perfil de Traffic Manager** nombre que creó en la sección anterior de Hola y haga clic en el perfil del Administrador de tráfico de Hola Hola da ese hello muestra.
2. Hola **perfil de Traffic Manager** hoja, haga clic en **Introducción**.
3. Hola **perfil de Traffic Manager** hoja muestra el nombre DNS de Hola de su perfil de Traffic Manager recién creado. Esto se puede utilizar cualquier extremo derecho de los clientes (por ejemplo, desplazándose tooit mediante un explorador web) tooget enrutado toohello determinado por el tipo de enrutamiento de Hola.  En caso de hello de enrutamiento geográfico, Traffic Manager busca en la dirección IP de origen de Hola de solicitud entrante de Hola y determina la región de Hola desde el que se origina. Si dicha región es el punto de conexión de tooan asignado, el tráfico es enrutado toothere. Si esta región no está asignada tooan punto de conexión, Traffic Manager devuelve una respuesta de consulta NODATA.

## <a name="next-steps"></a>Pasos siguientes

- Obtenga más información sobre el [método de enrutamiento del tráfico geográfico](traffic-manager-routing-methods.md#geographic).
- Obtenga información acerca de cómo demasiado[Probar configuración de Traffic Manager](traffic-manager-testing-settings.md).
