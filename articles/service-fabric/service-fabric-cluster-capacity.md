---
title: "Hola aaaPlanning capacidad de clúster de Service Fabric | Documentos de Microsoft"
description: "Consideraciones de planeación de capacidad del clúster de Service Fabric Tipos de nodos, durabilidad y niveles de confiabilidad"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 4c584f4a-cb1f-400c-b61f-1f797f11c982
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: chackdan
ms.openlocfilehash: 83272ce7fefe698eef755cf66493c2874cc3b120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-capacity-planning-considerations"></a>Consideraciones de planeación de capacidad del clúster de Service Fabric
En cualquier implementación de producción, la planeación de capacidad es un paso importante. Estos son algunos de los elementos de hello tiene tooconsider como parte de ese proceso.

* número de Hello del nodo de tipos de su necesidades de clúster toostart out con
* propiedades de Hola de cada tipo de nodo (tamaño, principal, con conexión a, número de máquinas virtuales, etcetera internet).
* características de confiabilidad y durabilidad de Hola de clúster de Hola

Repasemos brevemente cada uno de estos elementos.

## <a name="hello-number-of-node-types-your-cluster-needs-toostart-out-with"></a>número de Hello del nodo de tipos de su necesidades de clúster toostart out con
En primer lugar, necesita toofigure qué clúster Hola que está creando va toobe permiten y qué tipos de aplicaciones va toodeploy en este clúster. Si no está claro en la finalidad de Hola de clúster de hello, es más probable que no aún está listo capacidad de hello tooenter proceso de planeación.

Establecer número de Hola de tipos de nodos con que del clúster debe toostart out.  Cada tipo de nodo es asignada tooa conjunto de escala de máquinas virtuales. Cada tipo de nodo se puede escalar o reducir verticalmente de forma independiente. Cada uno tiene diferentes conjuntos de puertos abiertos y puede tener distintas métricas de capacidad. Por lo tanto decisión Hola de número de Hola de tipos de nodos básicamente desciende toohello siguientes consideraciones:

* ¿La aplicación tiene varios servicios, y cualquiera de ellos necesita toobe pública o con conexión a internet? Las aplicaciones típicas contienen un servicio de front-end de la puerta de enlace que recibe la entrada de un cliente y uno o más servicios back-end que se comunican con los servicios front-end de Hola. Por lo que en este caso, acaba teniendo al menos dos tipos de nodo.
* ¿Tienen los servicios (que componen la aplicación) distintos requisitos de infraestructura, como, por ejemplo, una RAM mayor o un número más alto de ciclos de CPU? Supongamos, por ejemplo, esa aplicación Hola que desea toodeploy contiene un servicio front-end y un servicio back-end. Hello front-end servicio se puede ejecutar en máquinas virtuales más pequeñas (tamaños de máquina virtual como D2) que tienen abiertos toohello puertos de internet.  servicio de back-end de Hello, sin embargo, se toorun intensiva y las necesidades de cálculo en máquinas virtuales más grandes (con tamaños de máquina virtual como D4, D6, D15) que no son internet cara.
  
  En este ejemplo, aunque puede decidir tooput Hola a todos los servicios en un tipo de nodo, se recomienda colocarlas en un clúster con dos tipos de nodos.  Esto permite que cada propiedades distintos toohave del tipo de nodo como conectividad a internet o tamaño de máquina virtual. número de Hola de máquinas virtuales se puede escalar independientemente, así como.  
* Puesto que no se puede predecir el futuro de hello, vaya a hechos de que sabrá y decida en número de Hola de tipos de nodos que las aplicaciones necesitan toostart con. Siempre puede agregar o quitar tipos de nodos más adelante. Un clúster de Service Fabric debe tener como mínimo un tipo de nodo.

## <a name="hello-properties-of-each-node-type"></a>propiedades de Hola de cada tipo de nodo
Hola **tipo de nodo** puede verse como tooroles equivalente en servicios en la nube. Tipos de nodos definen tamaños de máquinas virtuales de hello, Hola número de máquinas virtuales y sus propiedades. Cada tipo de nodo que se define en un clúster de Service Fabric está configurado como un conjunto de escalado de máquinas virtuales independiente. Conjunto de escalas de máquina virtual es un recurso de proceso de Azure puede usar toodeploy y administrar una colección de máquinas virtuales como un conjunto. Al definirse como diferentes conjuntos de escalado de máquinas virtuales, cada tipo de nodo se puede escalar o reducir verticalmente de forma independiente, tener diferentes conjuntos de puertos abiertos y puede tener distintas métricas de capacidad.

Lectura [este documento](service-fabric-cluster-nodetypes.md) para obtener más detalles de la relación de hello Nodetypes toovirtual escala del conjunto de máquinas, cómo tooRDP en una de las instancias de hello, abrir nuevos puertos etcetera.

El clúster puede tener más de un tipo de nodo pero el tipo de nodo principal de hello (Hola la primera de ellas que define en el portal de hello) debe tener al menos cinco máquinas virtuales para clústeres que se usan para las cargas de trabajo de producción (o al menos tres máquinas virtuales para clústeres de prueba). Si va a crear utilizando una plantilla de administrador de recursos de clúster de hello, a continuación, busque **es principal** atributo en la definición de tipo de nodo de Hola. tipo de nodo principal de Hello es tipo de nodo de Hola donde se colocan los servicios del sistema de Service Fabric.  

### <a name="primary-node-type"></a>Tipo de nodo principal
Para un clúster con varios tipos de nodo, deberá toochoose uno de ellos toobe principal. A continuación se indican las características de Hola de un tipo de nodo principal:

* Hola **tamaño mínimo de máquinas virtuales** tipo de nodo principal de Hola se determina mediante hello **el nivel de durabilidad** elija. valor predeterminado de Hello para el nivel de durabilidad hello es Bronce. Desplácese hacia abajo para obtener más información sobre qué nivel de durabilidad de hello es y valores de hello puede tardar.  
* Hola **mínimo número de máquinas virtuales** tipo de nodo principal de Hola se determina mediante hello **nivel de confiabilidad** elija. valor predeterminado de Hello para el nivel de confiabilidad de hello es plata. Desplácese hacia abajo para obtener más información sobre qué nivel de confiabilidad de hello es y valores de hello puede tardar. 


* servicios del sistema de Service Fabric Hello (por ejemplo, servicio de administrador de clústeres de Hola o el servicio de almacenamiento de la imagen) se colocan en el tipo de nodo principal de Hola y la confiabilidad de hello así y durabilidad de clúster de hello viene determinada por el nivel de valor y la durabilidad de la capa del confiabilidad Hola valor que se selecciona para el tipo de nodo principal de Hola.

![Captura de pantalla de un clúster que tiene dos tipos de nodos ][SystemServices]

### <a name="non-primary-node-type"></a>Tipo de nodo no principal
Para un clúster con varios tipos de nodo, hay un tipo de nodo principal y resto Hola son no principal. A continuación se indican las características de Hola de un tipo de nodo no principales:

* tamaño mínimo de Hola de máquinas virtuales para este tipo de nodo se determina según el nivel de durabilidad de Hola que elija. valor predeterminado de Hello para el nivel de durabilidad hello es Bronce. Desplácese hacia abajo para obtener más información sobre qué nivel de durabilidad de hello es y valores de hello puede tardar.  
* número mínimo de Hola de máquinas virtuales para este tipo de nodo puede ser uno. Sin embargo, debe elegir este número según el número de Hola de réplicas de hello aplicaciones o servicios que desearía toorun en este tipo de nodo. número de Hola de máquinas virtuales en un tipo de nodo puede aumentarse después de implementar el clúster de Hola.

## <a name="hello-durability-characteristics-of-hello-cluster"></a>características de durabilidad de Hola de clúster de Hola
el nivel de durabilidad Hello es tooindicate usado toohello Hola privilegios del sistema que tienen las máquinas virtuales con la infraestructura subyacente de Azure Hola. En el tipo de nodo principal de hello, este permiso permite a Service Fabric toopause cualquier solicitud de infraestructura de nivel de máquina virtual (por ejemplo, un reinicio de la VM, crear una nueva imagen de VM o migración de máquinas virtuales) que afectar a los requisitos de quórum de Hola para los servicios de sistema de Hola y los servicios con estado. En tipos de nodo no es el principal de hello, este permiso permite a Service Fabric toopause las solicitudes de nivel de infraestructura VM como reinicio de la VM, crear una nueva imagen de máquina virtual, etc., migración de máquinas virtuales que afectan a los requisitos de quórum de Hola para los servicios con estado que se ejecutan en él.

Este privilegio se expresa en hello siguientes valores:

* Oro - infraestructura Hola trabajos se pueden pausar una duración de dos horas por UD. La durabilidad de Gold solo puede habilitarse en las SKU de la máquina virtual del nodo completo, como D15_V2, G5, etc.
* Plata - hello trabajos de infraestructura se puede pausar una duración de 10 minutos por UD y está disponibles en todas las máquinas virtuales estándares de núcleo y versiones posteriores.
* Bronze: sin privilegios. Éste es el predeterminado de Hola. Utilice solo este nivel de durabilidad en los tipos de nodos que ejecutan _exclusivamente_ cargas de trabajo sin estado. 

> [!WARNING]
> Los tipos de nodos que se ejecutan con la durabilidad Bronze no obtienen _privilegios_. Es decir, los trabajos de infraestructura que afectan a las cargas de trabajo sin estado no se detendrán ni retrasarán. Es posible que estos trabajos todavía pueden afectar a las cargas de trabajo, de forma que generen tiempos de inactividad u otros problemas. Se recomienda la durabilidad Silver para cualquier tipo de carga de trabajo de producción. 
> 

Obtener el nivel de durabilidad de toochoose para cada uno de los tipos de nodos. Puede elegir un toohave del tipo de nodo de un nivel de durabilidad de oro o plata y Hola otro tener bronce Hola mismo clúster. **Debe mantener un recuento mínimo de 5 nodos para cualquier tipo de nodo que tiene una duración de oro o plata**. 

**Ventajas del uso de los niveles de durabilidad Silver o Gold**
 
1. Reduce el número de Hola de pasos necesarios en una operación de escala (es decir, desactivación de nodo y Remove-ServiceFabricNodeState se denomina automáticamente)
2. Reduce el riesgo de Hola de pérdida de datos de vencimiento iniciadas por el cliente de tooa en operación de cambio de VM SKU de in situ o las operaciones de infraestructura de Azure.
     
**Desventajas del uso de los niveles de durabilidad Silver o Gold**
 
1. Tooyour implementaciones conjunto de escala de máquinas virtuales y otros recursos de Azure relacionados) se pueden retrasar, pueden agotar el tiempo o se pueden bloquear completamente con problemas en el clúster o en el nivel de la infraestructura de Hola. 
2. Aumenta Hola número de [eventos de ciclo de vida de réplica](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle ) (por ejemplo, principales intercambios) debido desactivaciones de nodo tooautomated durante las operaciones de infraestructura de Azure.

### <a name="recommendations-on-when-toouse-silver-or-gold-durability-levels"></a>Recomendaciones sobre cuándo los niveles de durabilidad de plata u oro de toouse

Use plata u oro durabilidad para ese stateful host los tipos de nodo todos los servicios esperados en tooscale (reducir el número de instancias VM) con frecuencia, y prefiere que las operaciones de implementación se retrasa en favor de simplificación de estas operaciones de escala. escenarios de escalado horizontal de Hello (agregar instancias de máquinas virtuales) no se reproducen en la elección del nivel de durabilidad de hello, en escala solo realiza.

### <a name="operational-recommendations-for-hello-node-type-that-you-have-set-toosilver-or-gold-durability-level"></a>Recomendaciones operativas para el nodo de hello escriba que haya establecido la durabilidad toosilver u oro nivel.

1. Mantener sus aplicaciones y el clúster funciona correctamente en todo momento y asegúrese de que las aplicaciones responden tooall [eventos de ciclo de vida de réplica de servicio](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle) (como la réplica en la compilación está atascada) de manera oportuna.
2. Adoptar más seguro formas toomake un cambio de VM SKU (escala arriba/abajo): cambiar Hola VM SKU de un conjunto de escala de máquinas virtuales es en sí una operación no segura de modo que deberían evitarse si es posible. Este es proceso Hola puede seguir tooavoid los problemas comunes.
    - **Para el elemento nodetypes no principales:** se recomienda crear conjunto de escala de máquinas virtuales nuevas, modificar Hola servicio colocación tooinclude Hola nuevo nodo de conjunto de escalas de máquina Virtual tipo de restricción y, a continuación, reducir Hola conjunto anterior de escala de máquinas virtuales too0 de recuento de instancia, un nodo a la vez (es decir, toomake seguro de que la eliminación de nodos de hello no afectan confiabilidad Hola de clúster de hello).
    - **Para hello principal nodetype:** nuestra recomendación es que no cambian VM SKU del tipo de nodo principal de Hola. Si Hola razón para SKU nueva hello es capacidad, se recomienda agregar más instancias o si es posible, cree un nuevo clúster. Si no tiene ninguna opción, asegúrese de modificaciones toohello tooreflect de definición de modelo de conjunto de escala de máquina Virtual Hola SKU nuevo. Si el clúster tiene solo un valor de nodetype, asegúrese de que todas las aplicaciones con estado responden tooall [eventos de ciclo de vida de réplica de servicio](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle) (como la réplica en la compilación está atascada) de manera oportuna y que la réplica de servicio volver a generar duración es inferior a cinco minutos (nivel de durabilidad plata). 


> [!WARNING]
> Hola cambiar tamaño de los conjuntos de escalas de máquina virtual no se está ejecutando al menos plata durabilidad SKU de máquina virtual no está recomendado. Modificar el tamaño de la SKU de VM constituye una operación de infraestructura local de destrucción de datos. Sin al menos alguna capacidad toodelay o el monitor de este cambio, es posible que la operación Hola puede provocar dataloss para los servicios con estado o provocar otros problemas de funcionamiento de imprevistas, incluso para las cargas de trabajo sin estado. 
> 
    
3. Mantenga un número mínimo de cinco nodos en todos los conjuntos de escalado de máquinas virtuales en los que MR esté habilitado
4. No elimine instancias de máquina virtual aleatorias, use siempre la característica de reducción vertical del conjunto de escalado de máquinas virtuales. eliminación de Hola de aleatorias instancias de máquina virtual tiene un potencial de crear desequilibrios en la instancia de máquina virtual de Hola se reparten entre UD y FD. Este desequilibrio podría afectar negativamente al equilibrio de carga de hello sistemas capacidad tooproperly entre réplicas de instancias/servicio del servicio de Hola.
6. Si usa el escalado automático, a continuación, establezca las reglas de Hola tal que escala en (eliminación de instancias de máquina virtual) se realiza un único nodo cada vez. No es seguro reducir verticalmente más de una instancia a la vez.
7. Si reduce verticalmente un tipo de nodo principal, no deberá ampliar nunca más que permite que el nivel de confiabilidad de hello hacia abajo.


## <a name="hello-reliability-characteristics-of-hello-cluster"></a>características de confiabilidad de Hola de clúster de Hola
Hello nivel de confiabilidad se utiliza número de hello tooset de réplicas hello de servicios del sistema que desea que toorun en este clúster en el tipo de nodo principal de Hola. Hola mayor número de Hola de réplicas, hello más confiable Hola sistema servicios se encuentran en el clúster.  

nivel de confiabilidad de Hello puede tomar Hola siguientes valores:

* Platino - servicios del sistema de Hola de ejecución con un número de conjunto de réplica de destino de 9
* Oro - servicios del sistema de Hola de ejecución con un número de conjunto de réplica de destino de 7
* Plata - servicios del sistema de Hola de ejecución con un número de conjunto de réplica de destino de 5 
* Bronce, servicios del sistema de Hola de ejecución con un número de conjunto de réplica de destino de 3

> [!NOTE]
> nivel de confiabilidad de Hola que elija determina el número mínimo de Hola de nodos que debe tener el tipo de nodo principal. 
> 
> 


### <a name="recommendations-for-hello-reliability-tier"></a>Recomendaciones para el nivel de confiabilidad de Hola.

 Al aumentar o reducir el tamaño Hola del clúster (suma de Hola de instancias de máquina virtual en todos los tipos de nodo), debe actualizar confiabilidad Hola del clúster desde un nivel tooanother. Esto desencadena hello las actualizaciones necesarias toochange Hola sistema servicios réplica conjunto recuento de clústeres. Espere Hola actualización en curso toocomplete antes de realizar cualquier otro clúster toohello de cambios, como agregar nodos.  Puede supervisar el progreso de Hola de actualización de hello en el Explorador de Service Fabric o ejecutando [Get ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

Aquí es recomendación Hola sobre cómo elegir el nivel de confiabilidad de Hola.

| **Tamaño del clúster** | **Nivel de confiabilidad** |
| --- | --- |
| 1 |No se especifica Hola parámetro de nivel de confiabilidad, lo calcula el sistema de Hola |
| 3 |Bronze |
| 5 o 6|Silver |
| 7 u 8 |Gold |
| 9 y superiores |Platinum |




## <a name="primary-node-type---capacity-guidance"></a>Tipo de nodo principal: guía de capacidad

Ésta es una guía de Hola para planear la capacidad del tipo de nodo principal de Hola

1. **Número de VM instancias toorun cualquier carga de trabajo de producción en Azure:** debe especificar un tamaño mínimo de tipo de nodo principal de 5. 
2. **Número de VM instancias toorun cargas de trabajo de pruebas en Azure** puede especificar un tamaño de tipo de nodo principal mínimo de 1 o 3. Hola un clúster de nodo, se ejecuta con una configuración especial y por lo tanto, no se admite la escala fuera de ese clúster. Hello un clúster de nodo, no tiene ningún confiabilidad y por lo que en la plantilla de administrador de recursos, debe tooremove/no especificar esa configuración (no establece el valor de configuración de hello no es suficiente). Si configuras clúster de un nodo de hello configurados a través del portal, a continuación, configuración de Hola se ocupe de. Los clústeres de 1 y 3 nodos no se admiten en la ejecución de cargas de trabajo de producción. 
3. **VM SKU:** tipo de nodo principal es donde se ejecutan servicios de sistema de hello, por lo Hola SKU VM que elija, debe tienen en hello cuenta general pico de carga se planear tooplace en clúster de Hola. Aquí es un tooillustrate analogía quiero decir aquí - opinión del tipo de nodo principal de Hola como los "pulmones", es lo que ofrece cerebro de oxígeno tooyour y, por lo que si cerebro hello no obtener suficiente oxígeno, su cuerpo sufre. 

Puesto que las necesidades de capacidad de Hola de un clúster viene determinado por la carga de trabajo piensa toorun en clúster de Hola, no podemos proporcionar orientación cualitativa para la carga de trabajo específico, sin embargo aquí es Hola orientación amplia toohelp empezar a

Para cargas de trabajo de producción 


- Hola recomienda VM SKU estándar D3 o D3_V2 estándar o un grupo equivalente con un mínimo de 14 GB de SSD local.
- uso de Hello mínimo admitida VM SKU es D1 estándar o D1_V2 estándar o un grupo equivalente con un mínimo de 14 GB de SSD local. 
- Las SKU de máquina virtual de núcleo parcial, como Standard A0, no se admiten en cargas de trabajo de producción.
- La SKU Standard A1 no se admite en cargas de trabajo de producción por motivos de rendimiento.


## <a name="non-primary-node-type---capacity-guidance-for-stateful-workloads"></a>Tipo de nodo no principal: guía de capacidad para cargas de trabajo con estado

Esta guía está dirigida a las cargas de trabajo con estado con Service fabric [colecciones confiables o actores confiables](service-fabric-choose-framework.md) que se está ejecutando en el tipo de nodo principal no Hola.


**Número de instancias de máquina virtual**: para cargas de trabajo de producción con estado, se recomienda ejecutarlas con un número mínimo de réplicas de destino de 5. Esto significa que en estado estable acabará con una réplica (de un conjunto de réplicas) en cada dominio de error y dominio de actualización. concepto de nivel de confiabilidad todo Hello para el tipo de nodo principal de hello es una manera toospecify esta configuración para los servicios del sistema. Hola así mismo consideración aplica a servicios con estado de tooyour.

Por lo tanto para cargas de trabajo de producción, tamaño del tipo hello mínima recomendada no - nodo principal es 5, si ejecuta las cargas de trabajo con estado en ella.


**VM SKU:** trata el tipo de nodo de Hola donde se ejecutan los servicios de aplicación, por lo que Hola VM SKU elija, debe tener en cuenta Hola pico de carga planee tooplace en cada nodo. Hola necesidades de capacidad de hello nodetype, viene determinado por la carga de trabajo que tiene previsto toorun en clúster de hello, por lo que no podemos proporcionar cualitativa orientación para la carga de trabajo específico, sin embargo aquí es Hola orientación amplia toohelp comenzar

Para cargas de trabajo de producción 

- Hola recomienda VM SKU estándar D3 o D3_V2 estándar o un grupo equivalente con un mínimo de 14 GB de SSD local.
- uso de Hello mínimo admitida VM SKU es D1 estándar o D1_V2 estándar o un grupo equivalente con un mínimo de 14 GB de SSD local. 
- Las SKU de máquina virtual de núcleo parcial, como Standard A0, no se admiten en cargas de trabajo de producción.
- En concreto, la SKU Standard A1 no se admite en cargas de producción por motivos de rendimiento.


## <a name="non-primary-node-type---capacity-guidance-for-stateless-workloads"></a>Tipo de nodo no principal: guía de capacidad para cargas de trabajo sin estado

Esta guía de las cargas de trabajo sin estado que se están ejecutando en hello no principal nodetype.

**Número de instancias de máquina virtual:** para las cargas de trabajo de producción que no tienen estados, el tamaño del tipo hello mínimo compatible no nodo principal es 2. Esto le permite toorun dos instancias sin estado de la aplicación y permitir que el servicio toosurvive Hola pérdida de una instancia de la máquina virtual. 

> [!NOTE]
> Si el clúster se ejecuta en una versión de fabric servicio inferior a 5.6, debido tooa defecto en hello en tiempo de ejecución (este problema se corregirá en 5.6), ajuste de escala hacia abajo una que no requiere herramientas de tipo de nodo no principal que 5, da como resultado el estado del clúster activar incorrecto, hasta que se llama a [ Remove-ServiceFabricNodeState cmd](https://docs.microsoft.com/powershell/servicefabric/vlatest/Remove-ServiceFabricNodeState) con el nombre de nodo apropiado Hola. Para más información, lea [Escalado o reducción horizontal de un clúster de Service Fabric ](service-fabric-cluster-scale-up-down.md).
> 
>

**VM SKU:** trata el tipo de nodo de Hola donde se ejecutan los servicios de aplicación, por lo que Hola VM SKU elija, debe tener en cuenta Hola pico de carga planee tooplace en cada nodo. Hola necesidades de capacidad de hello nodetype, viene determinado por la carga de trabajo que tiene previsto toorun en clúster de hello, por lo que no podemos proporcionar cualitativa orientación para la carga de trabajo específico, sin embargo aquí es Hola orientación amplia toohelp comenzar

Para cargas de trabajo de producción 


- Hola recomienda VM SKU estándar D3 o D3_V2 estándar o un grupo equivalente. 
- uso de Hello mínimo admitida VM SKU es D1 estándar o D1_V2 estándar o un grupo equivalente. 
- Las SKU de máquina virtual de núcleo parcial, como Standard A0, no se admiten en cargas de trabajo de producción.
- La SKU Standard A1 no se admite en cargas de trabajo de producción por motivos de rendimiento.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Pasos siguientes
Una vez que termine la planificación de capacidad y configurar un clúster, lea Hola siguiente:

* [Seguridad de los clústeres de Service Fabric](service-fabric-cluster-security.md)
* [Introducción al modelo de mantenimiento de Service Fabric](service-fabric-health-introduction.md)
* [Establece la relación de escala de máquinas de Nodetypes tooVirtual](service-fabric-cluster-nodetypes.md)

<!--Image references-->
[SystemServices]: ./media/service-fabric-cluster-capacity/SystemServices.png
