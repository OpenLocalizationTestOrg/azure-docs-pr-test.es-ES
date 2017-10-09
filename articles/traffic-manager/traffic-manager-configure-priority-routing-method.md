---
title: "con Azure Traffic Manager de método de enrutamiento de tráfico de prioridad aaaConfigure | Documentos de Microsoft"
description: "Este artículo explica cómo prioridad de hello tooconfigure tráfico método de enrutamiento en el Administrador de tráfico"
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
ms.openlocfilehash: dd3e3bb2a727e5ea087cee35962c8e6f7c357282
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-priority-traffic-routing-method-in-traffic-manager"></a>Configuración del método de enrutamiento de tráfico por prioridad en Traffic Manager

Con independencia del modo del sitio Web de hello, sitios Web de Azure ya proporcionan funcionalidad de conmutación por error para sitios Web en un centro de datos (también conocido como región). Traffic Manager proporciona conmutación por error para sitios web en distintos centros de datos.

Un patrón común de conmutación por error de servicio es servicio principal de toosend tráfico tooa y proporcionar un conjunto de servicios de copia de seguridad idénticos para conmutación por error. Hello pasos siguientes explica cómo tooconfigure esto priorizan conmutación por error con los servicios de nube de Azure y sitios Web:

## <a name="tooconfigure-hello-priority-traffic-routing-method"></a>método de enrutamiento de tráfico de tooconfigure Hola prioridad

1. Desde un explorador, inicie sesión en toohello [portal de Azure](http://portal.azure.com). Si aún no tiene cuenta, puede registrarse para obtener [una evaluación gratuita durante un mes](https://azure.microsoft.com/free/). 
2. En la barra de búsqueda del portal de hello, busque hello **perfiles de Traffic Manager** y, a continuación, haga clic en nombre de perfil de Hola que desea que el método de enrutamiento de hello tooconfigure para.
3. Hola **perfil de Traffic Manager** hoja, compruebe que ambos Hola servicios en la nube y sitios Web que desea tooinclude en la configuración está presentes.
4. Hola **configuración** sección, haga clic en **configuración**y en hello **configuración** hoja, completa, como sigue:
    1. Para **configuración del método de enrutamiento de tráfico**, compruebe que es el método de enrutamiento de tráfico de hello **prioridad**. Si no es así, haga clic en **prioridad** de lista desplegable de Hola.
    2. Conjunto hello **configuración del monitor de punto de conexión** idénticos para todas las cada punto de conexión dentro de este perfil como se indica a continuación:
        1. Seleccione Hola adecuado **protocolo**y especifique hello **puerto** número. 
        2. En el tipo de **ruta de acceso**, escriba una barra diagonal */*. los puntos de conexión de toomonitor, debe especificar una ruta de acceso y nombre de archivo. Una barra diagonal "/" es una entrada válida para la ruta de acceso relativa de Hola e implica que el archivo hello esté en el directorio raíz de hello (valor predeterminado).
        3. En la parte superior de Hola de página de hello, haga clic en **guardar**.
5. Hola **configuración** sección, haga clic en **extremos**.
6. Hola **extremos** hoja, orden de prioridad de Hola de revisión de los extremos. Cuando selecciona hello **prioridad** método de enrutamiento de tráfico, Hola orden de los puntos de conexión de hello seleccionado es importante. Compruebe el orden de prioridad de Hola de puntos de conexión.  extremo principal de Hola se encuentra en la parte superior. Compruebe en el orden de Hola se muestra. todas las solicitudes se toohello enrutado primer punto de conexión y ser incorrecto si el Administrador de tráfico lo detecta, tráfico de hello conmuta por error automáticamente toohello siguiente punto de conexión. 
7. toochange Hola orden de prioridad de punto de conexión, haga clic en el extremo de hello y en hello **extremo** hoja que se muestra, haga clic en **editar** y cambiar hello **prioridad** valor según sea necesario . 
8. Haga clic en **guardar** toosave cambiar la configuración de punto de conexión de Hola.
9. Después de completar los cambios de configuración, haga clic en **guardar** final Hola de página Hola.
10. Probar cambios de hello en la configuración como se indica a continuación:
    1.  En la barra de búsqueda del portal de hello, busque el nombre del perfil de Traffic Manager de Hola y haga clic en perfil de Traffic Manager de hello en los resultados de Hola que hello muestra.
    2.  Hola **Traffic Manager** hoja de perfil, haga clic en **Introducción**.
    3.  Hola **perfil de Traffic Manager** hoja muestra el nombre DNS de Hola de su perfil de Traffic Manager recién creado. Esto se puede utilizar cualquier extremo derecho de los clientes (por ejemplo, desplazándose tooit mediante un explorador web) tooget enrutado toohello determinado por el tipo de enrutamiento de Hola. En este caso son el primer punto de conexión toohello enrutado y ser incorrecto si el Administrador de tráfico lo detecta todas las solicitudes, tráfico de hello conmuta por error automáticamente toohello siguiente punto de conexión.
11. Una vez que el perfil de Traffic Manager está en funcionamiento, edite registro DNS de hello en su toopoint de servidor DNS autoritativo su nombre de dominio de empresa dominio nombre toohello Traffic Manager.

![Configuración del método de enrutamiento de tráfico por prioridad con Traffic Manager][1]

## <a name="next-steps"></a>Pasos siguientes


- Información sobre el [método de enrutamiento de tráfico ponderado](traffic-manager-configure-weighted-routing-method.md).
- Información sobre el [método de enrutamiento de rendimiento](traffic-manager-configure-performance-routing-method.md).
- Información sobre el [método de enrutamiento geográfico](traffic-manager-configure-geographic-routing-method.md).
- Obtenga información acerca de cómo demasiado[Probar configuración de Traffic Manager](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-priority-routing-method/traffic-manager-priority-routing-method.png