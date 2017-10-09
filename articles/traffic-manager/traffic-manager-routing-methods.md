---
title: "los métodos de enrutamiento de tráfico de Traffic Manager - aaaAzure | Documentos de Microsoft"
description: "En este artículo le ayudará a que comprender los métodos de enrutamiento de tráfico distintos de hello utilizados por el Administrador de tráfico"
services: traffic-manager
documentationcenter: 
author: KumudD
manager: timlt
editor: 
ms.assetid: db1efbf6-6762-4c7a-ac99-675d4eeb54d0
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: kumud
ms.openlocfilehash: b3eeca63ab5f2b9cd4a3a6b6a8fd3e40059e32b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-routing-methods"></a>Métodos de enrutamiento del Administrador de tráfico

Azure Traffic Manager admite cuatro enrutamiento del tráfico métodos toodetermine cómo tooroute red tráfico toohello varios extremos de servicio. El Administrador de tráfico aplica Hola enrutamiento del tráfico método tooeach DNS consulta recibe. método de enrutamiento del tráfico de Hello determina qué extremo se devuelve en respuesta DNS de Hola.

En Traffic Manager, hay cuatro métodos de enrutamiento de tráfico disponibles:

* **[Prioridad](#priority):** seleccione **prioridad** cuando desee toouse un extremo de servicio principal para todo el tráfico y proporcionar copias de seguridad en caso de hello principal o los puntos de conexión de copia de seguridad de hello no están disponibles.
* **[Weighted](#weighted):** seleccione **Weighted** cuando desee toodistribute tráfico a través de un conjunto de extremos, ya sea uniformemente o tooweights correspondiente, que se define.
* **[Rendimiento](#performance):** seleccione **rendimiento** cuando tenga extremos en diferentes ubicaciones geográficas y desea que los usuarios finales toouse Hola "más cercano" punto de conexión en términos de latencia de red más baja de Hola.
* **[Geográfico](#geographic):** seleccione **geográfica** para que los usuarios son dirigidos toospecific puntos de conexión (Azure, externas o Nested) según qué ubicación geográfica su consulta DNS se origina en. Esto permite a los escenarios de tooenable de los clientes de Traffic Manager donde es importante conocer la región geográfica de un usuario y enrutarlos en base a eso. Algunos ejemplos incluyen cumplir los mandatos de soberanía de datos, la localización del contenido y de la experiencia del usuario, y la medición del tráfico de otras regiones.

Todos los perfiles de Traffic Manager incluyen supervisión del estado y conmutación por error automática del punto de conexión. Para más información, consulte [Acerca de la supervisión del Administrador de tráfico](traffic-manager-monitoring.md). Con un único perfil de Administrador de tráfico solo se puede usar un método de enrutamiento de tráfico. El método de enrutamiento de tráfico para el perfil se puede cambiar en cualquier momento. Los cambios se aplican en un minuto, sin tiempo de inactividad. Los métodos de enrutamiento de tráfico se pueden combinar mediante perfiles anidados del Administrador de tráfico. El anidamiento permite sofisticadas y flexibles configuraciones de enrutamiento del tráfico que satisfagan las necesidades de Hola de aplicaciones grandes y complejas. Para más información, consulte [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md)(Perfiles anidados de Administrador de tráfico).

## <a name = "priority"></a>Método de enrutamiento de tráfico Prioridad

A menudo una organización desea tooprovide confiabilidad para sus servicios mediante la implementación de uno o más servicios de copia de seguridad en caso de que el servicio principal deja de funcionar. método Hello enrutamiento de tráfico "Prioridad" permite a Azure tooeasily clientes implementan este patrón de conmutación por error.

![Método de enrutamiento de tráfico de "prioridad" de Azure Traffic Manager][1]

Hola perfil de Traffic Manager contiene una lista de prioridades de los extremos de servicio. De forma predeterminada, Traffic Manager envía todo tráfico toohello (prioridad más alta) punto de conexión primario. Si no hay ningún punto de conexión principal de hello, rutas de Traffic Manager Hola toohello segundo extremo de tráfico. Si ambos extremos de hello principales y secundarias no están disponibles, el tráfico de hello dirige toohello en tercer lugar, y así sucesivamente. Disponibilidad de punto de conexión de Hola se basa en el estado de hello configurado (habilitado o deshabilitado) y Hola supervisión continuada del extremo.

### <a name="configuring-endpoints"></a>Configuración de puntos de conexión

Con el Administrador de recursos de Azure, configurar la prioridad de punto de conexión de hello explícitamente con propiedad de 'priority' hello para cada extremo. Esta propiedad es un valor comprendido entre 1 y 1000. Los valores más bajos representan una prioridad más alta. Los puntos de conexión no pueden compartir valores de prioridad. Establecer propiedad de hello es opcional. Cuando se omite, se usa una prioridad predeterminada basada en el orden de punto de conexión de Hola.

##<a name = "weighted"></a>Método de enrutamiento de tráfico Ponderado
método Hello enrutamiento de tráfico 'Weighted' permite el tráfico toodistribute uniformemente o toouse una ponderación predefinido.

![Método de enrutamiento de tráfico "ponderado" de Azure Traffic Manager][2]

En el método de enrutamiento de tráfico ponderado de hello, se pueden asignar un punto de conexión de tooeach de peso en la configuración de perfil de Traffic Manager de Hola. peso de Hello es un entero entre 1 too1000. Este parámetro es opcional. Si se omite, Traffic Manager usará un peso predeterminado de '1'.

Para cada consulta de DNS recibida, Traffic Manager elegirá aleatoriamente un punto de conexión disponible. probabilidad de Hola de elegir un punto de conexión se basa en pesos Hola asignados tooall puntos de conexión disponibles. Usar Hola mismo peso a través de todos los resultados de los puntos de conexión en una distribución de tráfico incluso. Mediante valores ponderados mayores o menores en puntos de conexión concretos hace que esos toobe extremos devuelven mayor o menor frecuencia en las respuestas DNS de Hola.

método Hello ponderada habilita algunos escenarios útiles:

* Actualización gradual de la aplicación: asignar un porcentaje del tráfico tooroute tooa nuevo punto de conexión y aumentar gradualmente el tráfico de hello superar % de tiempo too100.
* TooAzure de migración de aplicaciones: crear un perfil con extremos de Azure y externos. Ajustar el peso de Hola de hello extremos tooprefer Hola nuevos puntos de conexión.
* Irrupción en la nube para obtener capacidad adicional: expanda rápidamente una implementación de local en la nube de hello colocándola detrás de un perfil de Traffic Manager. Cuando necesite capacidad adicional en la nube de hello, puede agregar o habilitar varios puntos de conexión y especificar qué parte del tráfico queda tooeach extremo.

Hola portal de Azure Resource Manager admite la configuración de Hola de enrutamiento del tráfico ponderado.  Puede configurar pesos con versiones de administrador de recursos de Hola de PowerShell de Azure, CLI, hello y las API de REST.

Es importante toounderstand que las respuestas DNS se almacenan en caché los clientes y servidores DNS de hello recursiva que Hola los clientes usan nombres DNS de tooresolve. Este almacenamiento en caché puede tener un impacto en las distribuciones de tráfico ponderadas. Cuando el número de Hola de clientes y servidores DNS recursivas es grande, una distribución del tráfico funciona según lo previsto. Sin embargo, cuando el número de Hola de clientes o servidores DNS recursivas es pequeño, el almacenamiento en caché puede sesgar significativamente una distribución del tráfico Hola.

Entre los casos de uso comunes se incluye:

* Entornos de desarrollo y pruebas
* Comunicaciones de aplicación a aplicación
* Las aplicaciones dirigidas a una base de usuarios estrecha que comparten una infraestructura DNS recursiva común (por ejemplo, los empleados de la empresa que se conectan a través de un proxy)

Estos efectos de almacenamiento en caché de DNS son comunes tooall tráfico basado en DNS enrutamiento sistemas, no solo el Administrador de tráfico de Azure. En algunos casos, borrar explícitamente Hola memoria caché de DNS puede proporcionar una solución alternativa. En otros, puede resultar más adecuado el uso de un método de enrutamiento de tráfico alternativo.

## <a name = "performance"></a>Método de enrutamiento de tráfico Rendimiento

Implementar puntos de conexión en dos o más ubicaciones en todo el mundo de hello puede mejorar la capacidad de respuesta de Hola de muchas aplicaciones por enrutamiento tráfico toohello ubicación tooyou "más cercano". el método de enrutamiento de tráfico 'Rendimiento' Hello proporciona esta capacidad.

![Método de enrutamiento de tráfico de "rendimiento" de Azure Traffic Manager][3]

punto de conexión "más cercano" Hello no es necesariamente más cercano, medido por la distancia geográfica. En su lugar, el método de enrutamiento de tráfico 'Rendimiento' hello determina extremo más cercano de Hola medir la latencia de red. El Administrador de tráfico mantiene un tiempo de ida y vuelta tabla de latencia de Internet tootrack Hola entre los intervalos de direcciones IP y cada centro de datos de Azure.

Traffic Manager busca la dirección IP de origen Hola de solicitud DNS entrante Hola Hola tabla de latencia de Internet. Administrador de tráfico se elige un punto de conexión disponible en hello Azure centro de datos que tiene una latencia más baja de Hola para ese intervalo de direcciones IP y luego devuelve ese punto de conexión en hello respuesta DNS.

Como se explica en [Cómo funciona Traffic Manager](traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager no recibe consultas de DNS directamente desde los clientes. En su lugar, las consultas DNS proceden de hello recursiva DNS de servicio que los clientes de hello son toouse configurado. Por lo tanto, hello IP dirección usada toodetermine hello "más cercano" extremo no es dirección IP del cliente de hello, pero es Hola dirección IP del servicio DNS recursivas Hola. En la práctica, esta dirección IP es un buen proxy para cliente de Hola.


El Administrador de tráfico con regularidad actualizaciones Hola tooaccount de tabla de latencia de Internet para los cambios en Hola Internet global y regiones de Azure nuevo. Sin embargo, rendimiento de la aplicación varía según las variaciones en tiempo real de carga a través de Internet de Hola. El enrutamiento de tráfico de rendimiento no supervisa la carga en un punto de conexión de servicio determinado. Sin embargo, si un punto de conexión no está disponible, Traffic Manager no lo incluye en las respuestas a las consultas de DNS.


Toonote puntos:

* Si el perfil contiene varios puntos de conexión en Hola misma región de Azure, a continuación, el Administrador de tráfico distribuye el tráfico uniformemente entre los extremos disponibles de hello en dicha región. Si prefiere una distribución de tráfico diferente dentro de una región, puede usar los [perfiles anidados de Traffic Manager](traffic-manager-nested-profiles.md).
* Si habilita puntos de conexión de hello más cercano región de Azure son degradado, Traffic Manager mueve los puntos de conexión de toohello de tráfico en la región de Azure más cercana siguiente Hola. Si desea toodefine una secuencia preferido de conmutación por error, use [anidados perfiles de Traffic Manager](traffic-manager-nested-profiles.md).
* Cuando use el método de enrutamiento de tráfico de rendimiento de Hola con extremos externos o extremos anidados, debe toospecify ubicación de Hola de esos puntos de conexión. Elija la implementación de tooyour más cercano de hello región de Azure. Esas ubicaciones son valores de hello admitidos Hola tabla de latencia de Internet.
* algoritmo de Hola que elige el punto de conexión de hello es determinista. Repetir las consultas DNS de hello es del mismo cliente dirigen toohello mismo punto de conexión. Normalmente, los clientes utilizan servidores DNS recursivos diferentes durante su recorrido. cliente de Hello puede ser enrutado tooa otro extremo. Enrutamiento también puede verse afectado por las actualizaciones toohello tabla de latencia de Internet. Por lo tanto, Hola rendimiento método de enrutamiento del tráfico no garantiza que siempre es un cliente enruta toohello mismo punto de conexión.
* Cuando se cambia el Hola tabla de latencia de Internet, puede observar que algunos clientes sean dirigidas tooa otro extremo. Este cambio de enrutamiento es más adecuado en función de los datos de latencia actuales. Estas actualizaciones son la precisión de hello toomaintain esenciales de tráfico de enrutamiento de rendimiento como Hola que Internet evolucione continuamente.

## <a name = "geographic"></a>Método de enrutamiento de tráfico Geográfico

Perfiles de Traffic Manager pueden ser hello toouse configurado geográfico método de enrutamiento para que los usuarios son dirigidos a los puntos de conexión de toospecific (Azure, externo o Nested) en función de qué ubicación geográfica su consulta DNS se origina en. Esto permite a los escenarios de tooenable de los clientes de Traffic Manager donde es importante conocer la región geográfica de un usuario y enrutarlos en base a eso. Algunos ejemplos incluyen cumplir los mandatos de soberanía de datos, la localización del contenido y de la experiencia del usuario, y la medición del tráfico de otras regiones.
Cuando se configura un perfil para el enrutamiento geográfico, cada punto de conexión asociados a que el perfil debe toohave un conjunto de regiones geográficas asignadas tooit. Una región geográfica puede estar en los siguientes niveles de granularidad 
- Mundo: cualquier región
- Agrupación regional: por ejemplo, África, Oriente Medio, Australia/Pacífico, etc. 
- País o región: p. ej., Irlanda, Perú, Hong Kong (RAE), etc. 
- Estado o provincia: p. ej., Estados Unidos-California, Australia-Queensland, etc. (este nivel de granularidad solo se admite en estados o provincias de Australia, Canadá, Reino Unido y Estados Unidos).

Cuando tooan extremo se asigna a una región o un conjunto de regiones, las solicitudes de esas regiones obtiene enrutado extremo toothat única. Administrador de tráfico usa la dirección IP de origen Hola de hello DNS consulta toodetermine Hola región desde la que se consulta un usuario desde: normalmente se trata de dirección IP de Hola de resolución DNS local Hola realizar consultas de hello en nombre de usuario de Hola.  

![Método de enrutamiento del tráfico "geográfico" de Azure Traffic Manager](./media/traffic-manager-routing-methods/geographic.png)

Traffic Manager lee la dirección IP de origen Hola de consulta DNS de Hola y decide qué región geográfica que se originan desde. Después, busca toosee si hay un punto de conexión que tiene este tooit de región geográfica asignado. Esta búsqueda se inicia en el nivel de granularidad más bajo de hello (estado o provincia donde se admite, qué más sitios en el nivel de país/región Hola) y pasa todos los Hola ascendiendo toohello nivel más alto, que es **World**. Hola primera coincidencia utilizando este recorrido se designa como tooreturn de punto de conexión de Hola en respuesta a la consulta Hola. En el caso de coincidencia con un punto de conexión de tipo Anidado, se devolverá un punto de conexión de dicho perfil secundario, en función de su método de enrutamiento. Hola siguientes puntos es aplicables toothis comportamiento:

- Una región geográfica puede ser asignado extremo de tooone sólo en un perfil de Traffic Manager cuando el tipo de enrutamiento de hello es enrutamiento geográfico. Esto garantiza que el enrutamiento de los usuarios es determinista y que los clientes pueden habilitar escenarios que requieran límites geográficos inequívocos.
- Si región del usuario entra asignación geográfica de los extremos diferentes en dos, el Administrador de tráfico selecciona el punto de conexión de hello con granularidad más baja de hello y no considere la posibilidad de enrutar las solicitudes de esa región toohello otro punto de conexión. Ejemplo: considere un perfil del tipo enrutamiento Geográfico con dos puntos de conexión, Punto de conexión 1 y Punto de conexión 2. Se configura Endpoint1 tooreceive tráfico de Irlanda y Endpoint2 se configura tooreceive tráfico de Europa. Si una solicitud se origina desde Irlanda, siempre es tooEndpoint1 enrutado.
- Puesto que una región puede ser el extremo de tooone sólo asignada, Traffic Manager devuelve independientemente de si el punto de conexión de hello es correcto o no.

    >[!IMPORTANT]
    >Se recomienda encarecidamente que los clientes que usan el método de enrutamiento geográfico hello asociarlo con extremos de tipo anidadas de Hola que tenga los perfiles secundarios que contiene al menos dos puntos de conexión dentro de cada.
- Si se encuentra una coincidencia de punto de conexión y ese punto de conexión está en hello **detenido** estado, Traffic Manager devuelve una respuesta NODATA. En este caso, no se realiza ninguna búsquedas más más arriba en la jerarquía de la región geográfica de Hola. Este comportamiento también es aplicable para los tipos anidados del punto de conexión cuando el perfil de secundarios de Hola Hola **detenido** o **deshabilitado** estado.
- Si un punto de conexión muestra un **deshabilitado** estado, no se incluirán en el proceso de coincidencia de región de Hola. Este comportamiento también es aplicable para los tipos anidados del punto de conexión al extremo de hello tiene hello **deshabilitado** estado.
- Si una consulta procede de una región geográfica que no tiene ninguna asignación en dicho perfil, Traffic Manager devolverá una respuesta NODATA. Por lo tanto, se recomienda encarecidamente que los clientes utilicen enrutamiento geográfico con un punto de conexión, lo ideal es que del tipo anidado con al menos dos extremos de perfil de secundarios de hello, con la región de hello **World** asignado tooit. Esto también garantiza que todas las direcciones IP que no se asignen tooa región se administran.

Como se explica en [Cómo funciona Traffic Manager](traffic-manager-how-traffic-manager-works.md), Traffic Manager no recibe consultas de DNS directamente desde los clientes. En su lugar, las consultas DNS proceden de hello recursiva DNS de servicio que los clientes de hello son toouse configurado. Por lo tanto, Hola IP dirección usada toodetermine Hola región no es Hola dirección IP del cliente, pero es dirección IP de hello del servicio DNS recursivas de Hola. En la práctica, esta dirección IP es un buen proxy para cliente de Hola.


## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo las aplicaciones de alta disponibilidad de toodevelop con [supervisión de extremos de Traffic Manager](traffic-manager-monitoring.md)

Obtenga información acerca de cómo demasiado[crear un perfil de Traffic Manager](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-routing-methods/priority.png
[2]: ./media/traffic-manager-routing-methods/weighted.png
[3]: ./media/traffic-manager-routing-methods/performance.png



