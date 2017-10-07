---
title: "recuperación ante desastres de Service Fabric aaaAzure | Documentos de Microsoft"
description: "Azure Service Fabric ofrece Hola capacidades necesarios toodeal con todos los tipos de desastres. Este artículo describen los tipos de Hola de desastres que se pueden producir y cómo toodeal con ellos."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 04b8348fb63e8a1c76a8f722c4c8255b339908e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-in-azure-service-fabric"></a>Recuperación ante desastres en Service Fabric de Azure
Una parte fundamental de la entrega de alta disponibilidad es garantizar que los servicios sobreviven a cualquier tipo de error. Esto es especialmente importante para los errores imprevistos y que se encuentran fuera de control. En este artículo se describen algunos modos de error comunes que podrían ser desastres si no hubieran modelado y administrado correctamente. También explican tootake mitigaciones y acciones si un desastre produjo de todos modos. el objetivo de Hello es toolimit o eliminar el riesgo de Hola de tiempo de inactividad o pérdida de datos cuando se producen errores, planeados o de lo contrario, se producen.

## <a name="avoiding-disaster"></a>Impedimento de desastres
Objetivo principal de Service Fabric es toohelp modelar su entorno y los servicios de tal manera que los tipos de error comunes no son los casos de desastres. 

En general, hay dos tipos de escenarios de desastre o error:

1. Errores de hardware o software
2. Errores operativos

### <a name="hardware-and-software-faults"></a>Errores de hardware y software
Los errores de hardware y software son imprevisibles. errores de toosurvive de manera más fáciles de Hola se está ejecutando más copias del servicio de hello distribuirse a través de los límites de error de hardware o software. Por ejemplo, si el servicio se ejecuta solamente en un equipo determinado, a continuación, hello error de que un equipo es un auténtico desastre para ese servicio. tooavoid de manera sencilla de Hello este desastre es tooensure que realmente se ejecuta el servicio de hello en varios equipos. Probar también es Error de hello tooensure necesarios de una máquina no interrumpe Hola ejecutando el servicio. Planificación de capacidad garantiza puede crearse una instancia de reemplazo en alguna otra parte y que reducción de capacidad no sobrecarga Hola restantes servicios. Hola mismo patrón funciona independientemente de lo que está tratando de error de hello tooavoid de. Por ejemplo. Si le preocupa error Hola de una red SAN, debe ejecutar en múltiples SANs. Si le preocupa la pérdida de Hola de un conjunto de servidores, debe ejecutar entre varios bastidores. Si le preocupa la pérdida de Hola de centros de datos, el servicio debe ejecutarse en varias regiones de Azure o centros de datos. 

Cuando se ejecuta en este tipo de modo distribuido, todavía está tipos de toosome de asunto de errores simultáneos, pero solo e incluso varios errores de un tipo determinado (por ejemplo: un error de vínculo de red o de máquina virtual solo) administra automáticamente (y por lo que ya no es un "desastre"). Service Fabric proporciona varios mecanismos para expandir el clúster de Hola y controladores que se devuelvan errores nodos y los servicios. Service Fabric también permite ejecutar varias instancias de los servicios en orden tooavoid estos tipos de errores no planeados de activar en los casos de desastres reales.

Puede haber razones ¿por qué no es factible quedarse un toospan lo suficientemente grande como implementación con errores. Por ejemplo, puede tardar más recursos de hardware que no esté dispuesto toopay para toohello relativa posibilidad de error. Cuando se trabaja con aplicaciones distribuidas, es posible que los costos de los saltos de comunicación o de replicación de estados adicionales a distancia geográfica provoquen una latencia inaceptable. Esta línea se traza en función de cada aplicación. Para errores de software concreto, error Hola podría ser en el servicio de Hola que está tratando de tooscale. En este caso más copias no impiden que desastre hello, ya que la condición de error de Hola se correlaciona en todas las instancias de Hola.

### <a name="operational-faults"></a>Errores operativos
Incluso si el servicio se distribuye en el mundo Hola con numerosas redundancias, aún puede experimentar eventos desastrosos. Por ejemplo, si alguien accidentalmente reconfigura el nombre de dns de hello para el servicio de Hola o elimina directamente. A modo de ejemplo, supongamos que tuviera un servicio de Service Fabric con estado y que alguien lo elimina por error. A menos que haya algunos otro mitigación, ese servicio y todo Estado Hola tenía es ya no aparece. Estos tipos de desastres operativos ("vaya") requieren más mitigaciones y pasos para la recuperación que los errores imprevistos normales. 

Hola mejores formas tooavoid estos tipos de errores de funcionamiento son para
1. restringir el entorno de acceso operativa toohello
2. inspeccionar minuciosamente las operaciones peligrosas;
3. imponer automatización, evitar manual o cambios fuera de banda y validar los cambios concretos en el entorno real de hello antes de establecer ellos
4. asegurarse de que las operaciones destructivas "se suavizan". Las operaciones de software suavizadas no surten efecto inmediatamente o se pueden deshacer en un plazo determinado.

Service Fabric proporciona algunos mecanismos de tooprevent operativa, tiene errores, como proporcionar [basada en roles](service-fabric-cluster-security-roles.md) control de acceso para las operaciones del clúster. Sin embargo, la mayoría de estos errores operativos requiere esfuerzos organizativos y otros sistemas. Service Fabric proporciona mecanismos para sobrevivir a errores operativos, concretamente, de copia de seguridad y restauración, para los servicios con estado.

## <a name="managing-failures"></a>Administración de errores
objetivo de Hola de Service Fabric casi siempre es la administración automática de errores. Sin embargo, en orden toohandle algunos tipos de errores, los servicios deben tener código adicional. Otros tipos de errores _no_ deben solucionarse automáticamente, por motivos de seguridad y continuidad empresarial. 

### <a name="handling-single-failures"></a>Abordaje de errores únicos
Una máquina puede fallar por todo tipo de razones. Algunas de las causas provienen del hardware, como los errores en los suministros de alimentación o el hardware de las redes. Otros errores son de software. Se trata de errores de hello actuales del sistema operativo y el propio servicio Hola. Service Fabric detecta automáticamente estos tipos de errores, incluidos los casos que no está aislada de otras máquinas debido a problemas de toonetwork máquina Hola.

Independientemente del tipo hello de servicio, ejecutar una sola instancia resultados en tiempo de inactividad para ese servicio si se produce un error en dicha copia única de código de hello por cualquier motivo. 

En orden toohandle cualquier error único, lo más sencillo de Hola que puede hacer es tooensure que los servicios se ejecutan en más de un nodo de forma predeterminada. Para los servicios sin estado, esto se consigue con un `InstanceCount` mayor que 1. Para los servicios con estado, la recomendación mínimo de hello es siempre un `TargetReplicaSetSize` y `MinReplicaSetSize` de al menos 3. La ejecución de más copias del código de servicio garantiza que este puede abordar cualquier error único automáticamente. 

### <a name="handling-coordinated-failures"></a>Abordaje de errores coordinados
Pueden producir errores coordinadas en un clúster de vencimiento tooeither planeado o errores de infraestructura no planeada y cambios o cambios de software planeado. Service Fabric modela las zonas de infraestructura que experimentan errores coordinados como dominios de error. Las áreas que experimentarán cambios coordinados de software se modelan como dominios de actualización. Para más información acerca de los dominios de error y de actualización, consulte [este documento](service-fabric-cluster-resource-manager-cluster-description.md), que indica la definición y la topología del clúster.

Service Fabric considera los dominios de error y de actualización al planear dónde deben ejecutarse los servicios. De forma predeterminada, Service Fabric intenta tooensure que los servicios se ejecutan en varios dominios de error y de actualización, por lo que si se realizan cambios planeados o no los servicios siguen estando disponibles. 

Por ejemplo, supongamos que un error de una fuente de alimentación provoca un bastidor de toofail máquinas simultáneamente. Con varias copias del servicio de hello pérdida de Hola de muchas máquinas se está ejecutando en un dominio de error error se convierte en otro ejemplo de error único para un servicio determinado. Este es el motivo por el que la administración de dominios de error es crítico tooensuring alta disponibilidad de los servicios. Al ejecutar Service Fabric en Azure, los dominios de error se administran automáticamente. En otros entornos puede que esto no sea así. Si va a compilar sus propios clústeres de forma local, ser toomap seguro y planear el diseño de dominio de error correctamente.

Dominios de actualización son útiles para modelar las áreas que se va software toobe actualizado en hello mismo tiempo. Por este motivo, dominios de actualización también suelen definir límites de Hola donde software ha sido desconectado durante las actualizaciones planeadas. Las actualizaciones de Service Fabric y los servicios siguen Hola mismo modelo. Para obtener más información acerca de la propagación de las actualizaciones y los dominios de actualización, modelo de estado de Service Fabric Hola que ayuda a evitar que los cambios no deseados afectando al clúster de Hola y el servicio, vea estos documentos:

 - [Actualización de aplicaciones](service-fabric-application-upgrade.md)
 - [Tutorial sobre la actualización de aplicaciones](service-fabric-application-upgrade-tutorial.md)
 - [Modelo de estado de Service Fabric](service-fabric-health-introduction.md)

Puede visualizar diseño Hola de su clúster mediante la asignación de clúster de hello proporcionada en [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md):

<center>
![Distribución de nodos entre dominios de error en Service Fabric Explorer][sfx-cluster-map]
</center>

> [!NOTE]
> Áreas de error, las actualizaciones sucesivas, ejecuta varias instancias de su código de servicio y su estado de modelado tooensure de reglas de selección de ubicación los servicios ejecutan entre dominios de error y de actualización y supervisión de estado integrada son simplemente **algunos** de hello características que proporciona Service Fabric en problemas de funcionamiento normal de orden tookeep y errores de activación en los casos de desastres. 
>

### <a name="handling-simultaneous-hardware-or-software-failures"></a>Abordaje de errores simultáneos en el hardware y en el software
Anteriormente hablamos de errores únicos. Como puede ver, son toohandle fácil para los servicios sin estado y con estado manteniendo más copias del código de hello (y el estado) se ejecuta en varios dominios de error y actualización. También se pueden producir varios errores simultáneos y aleatorios. Estas son más probable toolead tooan ante desastres efectivo.


### <a name="random-failures-leading-tooservice-failures"></a>Errores aleatorios iniciales tooservice errores
Supongamos que el servicio de hello tenía un `InstanceCount` de 5 y varios nodos ejecutan las instancias de todos los errores en hello mismo tiempo. Service Fabric responde mediante la creación automática de instancias de reemplazo en otros nodos. Seguirá creando reemplazos hasta que servicio Hola se vuelve tooits deseado recuento de instancias. Como otro ejemplo, supongamos que se ha producido un servicio sin estado con un `InstanceCount`de -1, lo que significa que se ejecuta en todos los nodos clúster Hola válidos. Supongamos que algunas de esas instancias estaban toofail. En este caso, Service Fabric observa que el servicio de hello no está en su estado deseado y trata de instancias de hello toocreate en nodos de Hola donde lo están. 

Para los servicios con estado situación Hola depende de si el servicio de hello tiene un estado persistente o no. También depende de cuántas réplicas del servicio hello y cuántas dieron error. La determinación de si se ha producido un desastre para un servicio con estado y su administración constan de tres etapas:

1. Determinación de si se ha producido pérdida de cuórum o no
 - Una pérdida de quórum es siempre una mayoría de las réplicas de Hola de un servicio con estado están inactivos en hello vez Hola principal.
2. Determinar si la pérdida del quórum hello es permanente o no
 - La mayoría de casos de hello, los errores son transitorios. Los procesos, los nodos y las máquinas virtuales se reinician y las particiones de la red se reparan. Sin embargo, a veces los errores son permanentes. 
    - Para servicios sin estado persistente, un error de un cuórum o varios en las réplicas deriva _inmediatamente_ en una pérdida de cuórum permanente. Cuando Service Fabric detecta la pérdida de quórum en un servicio con estado no persistente, continúa inmediatamente dataloss toostep 3 declarando (potenciales). Continuar toodataloss tiene sentido porque Service Fabric sabe que no hay ningún punto de espera para las réplicas de hello toocome copia, porque incluso si se recuperaron podría estar vacíos.
    - Los servicios con estado persistente, un error de un quórum o más réplicas provoca toostart Service Fabric esperando Hola réplicas volver toocome y quórum de restauración. Esto da como resultado una interrupción del servicio para cualquier _escribe_ toohello afectado partición (o "conjunto de réplicas") del servicio de Hola. Sin embargo, la lectura seguirá siendo posible, con garantía de coherencia reducida. cantidad de tiempo que espera Service Fabric toobe quórum restaurar predeterminada de Hello es infinito, ya que continuar es un evento dataloss (potencial) y contiene otros riesgos. Reemplazar el método predeterminado de hello `QuorumLossWaitDuration` valor es posible, pero no se recomienda. En su lugar en este momento, todos los esfuerzos deben realizarse hello toorestore hacia abajo de réplicas. Esto requiere poner Hola nodos que no estén funcionando copia de seguridad y asegurarse de que puede volver a montar las unidades de Hola donde almacenan el estado persistente local Hola. Si se produce pérdida de quórum de Hola por error de proceso, Service Fabric automáticamente intenta toorecreate procesos de Hola y reinicie réplicas hello en ellos. Si no es posible, Service Fabric informa de los errores de estado. Si estos se pueden resolver, a continuación, las réplicas de hello normalmente consultar de nuevo. A veces, sin embargo, las réplicas de Hola no se podrán volver. Por ejemplo, todas las unidades de hello podrán haya podido o máquinas Hola destruyen físicamente algún modo. En estos casos, lo que ocurre es una evento de pérdida de cuórum permanente. tootell Service Fabric toostop esperando Hola hacia abajo toocome de réplicas, un administrador de clústeres debe determinar qué particiones de los cuales los servicios se ven afectados y llamar a hello `Repair-ServiceFabricPartition -PartitionId` o ` System.Fabric.FabricClient.ClusterManagementClient.RecoverPartitionAsync(Guid partitionId)` API.  Esta API permite especificar el identificador hello de hello partición toomove de QuorumLoss y pasarlo al dataloss posibles.

> [!NOTE]
> Es _nunca_ toouse seguro para esta API no sea de una manera dirigida con particiones específicas. 
>

3. Determinación de si se ha producido realmente pérdida de datos y restauración de copias de seguridad
  - Cuando Service Fabric llama hello `OnDataLossAsync` método siempre es debido _sospecha_ dataloss. Service Fabric garantiza que esta llamada se entregue toohello _mejor_ de las demás réplicas. Se trata de cualquier réplica ha progresado Hola mayoría. Hola motivo decimos siempre _sospecha_ dataloss es que es posible que esa réplica restantes hello tiene realmente todo el mismo estado tal y como lo hizo Hola principal cuando ha fallado. Sin embargo, ese estado toocompare lo, no hay ningún mecanismo de buena tooknow Service Fabric u operadores de seguro. En este momento, Service Fabric también se conoce Hola otras réplicas no son devueltos. Eso estaba decisión de hello realizada cuando se detiene esperando tooresolve de pérdida de quórum Hola propio. Hola hacer a continuación para servicio de hello suele ser toofreeze y espere a que intervención administrativa específica. ¿Por lo que lo que hace una implementación típica de hello `OnDataLossAsync` método hacer?
  - En primer lugar, registra que se ha desencadenado `OnDataLossAsync` y activa las alertas administrativas necesarias.
   - Normalmente en este punto, toopause y espere aún más las decisiones y toobe acciones manuales realizadas. Esto es porque incluso si existen copias de seguridad podrán necesitar toobe preparado. Por ejemplo, si dos servicios diferentes coordinan la información, las copias de seguridad que necesite toobe modificado en orden tooensure que una vez que la restauración de hello ocurre que información Hola esos dos servicios preocupa es coherente. 
  - A menudo también hay algunas otra telemetría o salida de aire del servicio de Hola. Estos metadatos pueden estar contenidos en otros servicios o registros. Esta información puede ser usado toodetermine necesario si se produjeron las llamadas recibe y procesa en hello principal que no estaban presentes en la réplica determinada de hello toothis de copia de seguridad o replicada. Estos pueden requerir copia de seguridad de toobe toohello reproducido o se agregó antes de restauración es factible.  
   - Comparaciones de hello restantes toothat de estado de la réplica incluido en las copias de seguridad que están disponibles. Si el uso de colecciones de confianza de Service Fabric de hello, a continuación, hay herramientas y los procesos disponible para hacerlo, se describen en [este artículo](service-fabric-reliable-services-backup-restore.md). objetivo de Hello es toosee si el estado Hola de réplica de hello es suficiente, o también pueden faltar qué copia de seguridad de Hola.
  - Una vez se realiza la comparación de hello y, si se ha completado la restauración de hello necesarios, código de servicio de Hola debe devolver true si se han realizado los cambios de estado. Si la réplica de hello había determinado que era Hola mejor disponible copia del estado de Hola y ha realizado ningún cambio, a continuación, devuelven false. True indica que _cualquier_ réplica restante ahora puede ser incoherente con esta. Se descartarán y se volverán a crear a partir de esta réplica. False indica que se realizó ningún cambio de estado, por lo que Hola otras réplicas pueden mantener lo tienen. 

Es muy importante que los autores de los servicios practiquen con escenarios de posible pérdida de datos y error antes de implementarlos en producción. tooprotect contra la posibilidad de Hola de dataloss, es importante tooperiodically [copia de seguridad Hola estado](service-fabric-reliable-services-backup-restore.md) de cualquiera de su almacén con redundancia geográfica de servicios con estado tooa. También debe asegurarse de que dispone de hello capacidad toorestore lo. Dado que se realizan copias de seguridad de los muchos servicios diferentes en momentos diferentes, deberá tooensure que después de una restauración de los servicios tienen una vista coherente entre sí. Por ejemplo, considere una situación donde un servicio genera un número y lo almacena y después lo envía servicio tooanother que también lo almacena. Después de una restauración, puede que descubra que Hola segundo servicio no tiene número de Hola Hola primero pero no así, porque su copia de seguridad no incluyó esa operación.

Si averigua que Hola restantes réplicas están toocontinue insuficiente de en un escenario de dataloss y no se puede reconstruir el estado de servicio de telemetría o de salida de aire, frecuencia de Hola de las copias de seguridad determina el mejor objetivo de punto de recuperación posible (RPO) . Service Fabric proporciona muchas herramientas para probar varios escenarios de error, incluido el cuórum permanente y la pérdida de datos que requieren la restauración a partir de una copia de seguridad. Estos escenarios se incluyen como parte de herramientas de capacidad de prueba de Service Fabric, administrados por hello error Analysis Services. Más información sobre las herramientas y los patrones disponible [aquí](service-fabric-testability-overview.md). 

> [!NOTE]
> Servicios del sistema también pueden verse afectado pérdida del quórum, con un impacto Hola está toohello específico servicio en cuestión. Por ejemplo, pérdida de quórum en el servicio de nomenclatura de hello afecta a la resolución de nombres, mientras que la pérdida de quórum en el servicio de administrador de conmutación por error de hello bloquea las conmutaciones por error y la nueva creación de servicio. Aunque Servicios del sistema de Service Fabric Hola sigan Hola mismo patrón como los servicios de administración de estado, no es recomendable que debería intentar toomove les fuera de pérdida de quórum y al dataloss posibles. recomendación de Hello en su lugar es demasiado[buscar soporte](service-fabric-support.md) toodetermine una solución que esté destinado tooyour de situación concreta.  Normalmente es preferible toosimply espera hasta Hola hacia abajo de réplicas de valor devueltos.
>

## <a name="availability-of-hello-service-fabric-cluster"></a>Disponibilidad de clúster de Service Fabric Hola
Por lo general, el propio clúster de Service Fabric hello es un entorno altamente distribuido con ningún punto único de error. Un error de cualquiera de los nodos no hará que disponibilidad o los problemas de confiabilidad de clúster de hello, principalmente porque servicios del sistema de Service Fabric Hola siguen Hola mismas instrucciones proporcionadas anteriormente: siempre se ejecutan con tres o más réplicas de forma predeterminada y los ejecutar servicios de sistema que no tienen estados en todos los nodos. red de Service Fabric subyacente de Hola y niveles de detección de errores se distribuyen totalmente. La mayoría de los servicios de sistema puede volverán a partir de los metadatos en el clúster de Hola o sabe cómo tooresynchronize su estado de otros lugares. disponibilidad de Hola de clúster de hello podría verse comprometida en si los servicios del sistema que se producen en quórum pérdida situaciones como las descritas anteriormente. En estos casos es posible no que pueda tooperform determinada operaciones en clúster de hello, como iniciar una actualización o implementar nuevos servicios, pero el propio clúster Hola sigue estando activa. Servicios en ejecución ya seguirá ejecutándose en estas condiciones, a menos que necesiten escrituras toohello sistema servicios toocontinue funciona. Por ejemplo, si Hola Administrador de conmutación por error está en pérdida de quórum todos los servicios seguirán toorun, pero todos los servicios que se producirá un error no estará tooautomatically capaz de reinicio, ya que esto requiere la participación de Hola de hello Administrador de conmutación por error. 

### <a name="failures-of-a-datacenter-or-azure-region"></a>Errores en un centro de datos o una región de Azure
En raras ocasiones, puede ser no está disponible temporalmente debido a un centro de datos físico tooloss de conectividad de red o de alimentación. En estos casos, los clústeres de Service Fabric y los servicios de ese centro de datos o la región de Azure dejarán de estar disponibles. Sin embargo, _los datos se conservan_. Para los clústeres que se ejecutan en Azure, puede ver las actualizaciones en las interrupciones en hello [página Estado Azure][azure-status-dashboard]. Hola destruye de evento muy poco probable que un centro de datos físico está total o parcialmente, los clústeres de tejido de servicio hospedados no existe o servicios de hello en ellos se perderán. Esto incluye cualquier estado del que no se haya realizado copia de seguridad fuera de ese centro de datos o esa región.

Hay dos estrategias distintas para las personas supervivientes Hola error permanente o sostenido de un único centro de datos o región. 

1. Ejecutar clústeres de Service Fabric independientes en varias de estas regiones y utilizar algún mecanismo de conmutación por error y conmutación por recuperación entre estos entornos. Este tipo de modelo de varios clústeres activos/activos o activos/ pasivos requiere código adicional de administración y operación. Esto también requiere la coordinación de las copias de seguridad de los servicios de hello en un centro de datos o región de modo que estén disponibles en otros centros de datos o regiones cuando uno se produce un error. 
2. Ejecutar un único clúster de Service Fabric que abarque varios centros de datos o regiones. Hola mínimos de configuración admitidos para esto es tres centros de datos o regiones. Hola número recomendado de regiones o centros de datos es cinco. Esto requiere una topología de clúster más compleja. Sin embargo, hello ventaja de este modelo es que error de un centro de datos o región se convierte de un desastre en un error normal. Estos errores pueden controlarse mediante mecanismos de Hola que funcionan para los clústeres en una única región. Los dominios de error, los dominios de actualización y las reglas de colocación de Service Fabric aseguran que las cargas de trabajo se distribuyen para tolerar los errores de normales. Para más información sobre las directivas que pueden ayudar a que los servicios funcionen en este tipo de clúster, lea sobre las [directivas de colocación](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)

### <a name="random-failures-leading-toocluster-failures"></a>Errores aleatorios iniciales toocluster errores
Tejido de servicio tiene el concepto de Hola de nodos de valor de inicialización. Se trata de nodos que mantienen la disponibilidad de Hola Hola clúster de subyacente. Estos nodos ayudarle a tooensure Hola clúster permanece estableciendo concesiones con otros nodos y que actúa como los elementos diferenciadores durante ciertos tipos de errores de red. Si errores aleatorios quitar una mayoría de nodos de valor de inicialización de hello en clúster de hello y no se incorporan volver, clúster de Hola se cierra automáticamente. En Azure, se administran automáticamente los nodos de valor de inicialización: que se distribuyen a través de error disponibles hello y dominios de actualización, y si se quita un nodo de raíz única de clúster de Hola se creará otro en su lugar. 

En los clústeres de Service Fabric independientes y Azure, Hola "Tipo de nodo principal" es hello aquel que se ejecuta inicializaciones de Hola. Al definir un tipo de nodo principal, Service Fabric automáticamente aprovechará número Hola de nodos que se proporciona mediante la creación de nodos de valor de inicialización de too9 y 9 réplicas de cada uno de los servicios del sistema Hola. Si un conjunto de errores aleatorios saca una mayoría de las réplicas de servicio de sistema al mismo tiempo, los servicios del sistema Hola entrará pérdida del quórum, tal y como se ha descrito anteriormente. Si una mayoría de nodos de valor de inicialización de Hola se pierden, se apagará clúster Hola poco después.

## <a name="next-steps"></a>Pasos siguientes
- Obtenga información acerca de cómo toosimulate distintos errores con hello [framework de la capacidad de prueba](service-fabric-testability-overview.md)
- Lea otros recursos sobre alta disponibilidad y recuperación ante desastres. Microsoft ha publicado una gran cantidad de instrucciones sobre estos temas. Mientras que algunos de estos documentos refieren toospecific técnicas para su uso en otros productos, que contienen muchas prácticas recomendadas generales que puede aplicar en el contexto de Service Fabric Hola así:
  - [Lista de comprobación de disponibilidad](../best-practices-availability-checklist.md)
  - [Exploración en profundidad de la recuperación ante desastres](../sql-database/sql-database-disaster-recovery-drills.md)
  - [Recuperación ante desastres y alta disponibilidad para aplicaciones de Azure][dr-ha-guide]
- Más información sobre las [opciones de soporte técnico de Service Fabric](service-fabric-support.md)

<!-- External links -->

[repair-partition-ps]: https://msdn.microsoft.com/library/mt163522.aspx
[azure-status-dashboard]:https://azure.microsoft.com/status/
[azure-regions]: https://azure.microsoft.com/regions/
[dr-ha-guide]: https://msdn.microsoft.com/library/azure/dn251004.aspx


<!-- Images -->

[sfx-cluster-map]: ./media/service-fabric-disaster-recovery/sfx-clustermap.png
