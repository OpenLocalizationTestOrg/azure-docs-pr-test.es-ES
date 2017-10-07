---
title: "método de enrutamiento con Azure Traffic Manager de tráfico de rendimiento de aaaConfigure | Documentos de Microsoft"
description: "Este artículo explica cómo tooconfigure Traffic Manager tooroute tráfico toohello extremo con latencia más baja"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: d0ccd4c9de411844c6f36068859265244f4aa52b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-performance-traffic-routing-method"></a>Configurar el método de enrutamiento de tráfico de rendimiento de Hola

Hola método de enrutamiento de tráfico de rendimiento permite el punto de conexión de toodirect tráfico toohello con una latencia más baja desde la red del cliente de Hola Hola. Por lo general, Hola centro de datos con latencia más baja de hello es hello más cercano en distancia geográfica. Este método de enrutamiento de tráfico no cuenta los cambios en tiempo real en la carga o configuración de red.

##  <a name="tooconfigure-performance-routing-method"></a>método de enrutamiento de rendimiento tooconfigure

1. Desde un explorador, inicie sesión en toohello [portal de Azure](http://portal.azure.com). Si aún no tiene cuenta, puede registrarse para obtener [una evaluación gratuita durante un mes](https://azure.microsoft.com/free/). 
2. En la barra de búsqueda del portal de hello, busque hello **perfiles de Traffic Manager** y, a continuación, haga clic en nombre de perfil de Hola que desea que el método de enrutamiento de hello tooconfigure para.
3. Hola **perfil de Traffic Manager** hoja, compruebe que ambos Hola servicios en la nube y sitios Web que desea tooinclude en la configuración está presentes.
4. Hola **configuración** sección, haga clic en **configuración**y en hello **configuración** hoja, completa, como sigue:
    1. En la **configuración del método de enrutamiento de tráfico**, seleccione **Rendimiento** en **Método de enrutamiento**.
    2. Conjunto hello **configuración del monitor de punto de conexión** idénticos para todas las cada punto de conexión dentro de este perfil como se indica a continuación:
        1. Seleccione Hola adecuado **protocolo**y especifique hello **puerto** número. 
        2. En el tipo de **ruta de acceso**, escriba una barra diagonal */*. los puntos de conexión de toomonitor, debe especificar una ruta de acceso y nombre de archivo. Una barra diagonal "/" es una entrada válida para la ruta de acceso relativa de Hola e implica que el archivo hello esté en el directorio raíz de hello (valor predeterminado).
        3. En la parte superior de Hola de página de hello, haga clic en **guardar**.
5.  Probar cambios de hello en la configuración como se indica a continuación:
    1.  En la barra de búsqueda del portal de hello, busque el nombre del perfil de Traffic Manager de Hola y haga clic en perfil de Traffic Manager de hello en los resultados de Hola que hello muestra.
    2.  Hola **Traffic Manager** hoja de perfil, haga clic en **Introducción**.
    3.  Hola **perfil de Traffic Manager** hoja muestra el nombre DNS de Hola de su perfil de Traffic Manager recién creado. Esto se puede utilizar cualquier extremo derecho de los clientes (por ejemplo, desplazándose tooit mediante un explorador web) tooget enrutado toohello determinado por el tipo de enrutamiento de Hola. En este caso, todas las solicitudes son toohello enrutado extremo con una latencia más baja desde la red del cliente de Hola Hola.
6. Una vez que el perfil de Traffic Manager está en funcionamiento, edite registro DNS de hello en su toopoint de servidor DNS autoritativo su nombre de dominio de empresa dominio nombre toohello Traffic Manager.

![Configuración del método de enrutamiento del tráfico de rendimiento con Traffic Manager][1]

## <a name="next-steps"></a>Pasos siguientes

- Obtenga información sobre el [método de enrutamiento del tráfico ponderado](traffic-manager-configure-weighted-routing-method.md).
- Sepa cómo funciona el [método de enrutamiento por prioridad](traffic-manager-configure-priority-routing-method.md).
- Información sobre el [método de enrutamiento geográfico](traffic-manager-configure-geographic-routing-method.md).
- Obtenga información acerca de cómo demasiado[Probar configuración de Traffic Manager](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png