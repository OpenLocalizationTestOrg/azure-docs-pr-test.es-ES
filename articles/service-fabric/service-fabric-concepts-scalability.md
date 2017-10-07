---
title: aaaScalability de servicios de Service Fabric | Documentos de Microsoft
description: "Describe cómo los servicios de Service Fabric tooscale"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ed324f23-242f-47b7-af1a-e55c839e7d5d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5af06f8f71ad5dee32ba115b922842684867e654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-in-service-fabric"></a>Reducción horizontalmente de Service Fabric
Azure Service Fabric hace aplicaciones escalables toobuild fácil mediante la administración de servicios de hello, particiones y réplicas en nodos de Hola de un clúster. Ejecutan muchas cargas de trabajo en Hola el mismo uso de máximo de recursos de hardware permite, pero también proporciona flexibilidad en cuanto a cómo elegir tooscale las cargas de trabajo. 

El escalado en Service Fabric se realiza de varias maneras diferentes:

1. Escalado mediante la creación o eliminación de instancias de servicio sin estado
2. Escalado mediante la creación o eliminación de nuevos servicios con nombre
3. Escalado mediante la creación o eliminación de nuevas instancias de aplicaciones con nombre
4. Escalado mediante el uso de servicios particionados
5. Ajuste de escala agregando y quitando nodos de clúster de Hola 
6. Escalado mediante el uso de métricas de Cluster Resource Manager

## <a name="scaling-by-creating-or-removing-stateless-service-instances"></a>Escalado mediante la creación o eliminación de instancias de servicio sin estado
Uno de hello tooscale más sencilla de formas dentro de Service Fabric funciona con los servicios sin estado. Cuando se crea un servicio sin estado, obtendrá una oportunidad toodefine un `InstanceCount`. `InstanceCount`define cuántas copias en ejecución del código de dicho servicio se crean cuando se inicia el servicio de Hola. Supongamos, por ejemplo, que hay 100 nodos en clúster de Hola. Supongamos también que se crea un servicio con un `InstanceCount` de 10. En tiempo de ejecución, las 10 copias en ejecución del código de hello todos dejen de estar demasiado ocupadas (o pudieron no ser lo suficientemente ocupadas). Una manera de tooscale esa carga de trabajo es el número de hello toochange de instancias. Por ejemplo, un fragmento de código de supervisión o administración puede cambiar Hola existente número de instancias too50 o too5, dependiendo de si la carga de trabajo de Hola debe tooscale o alejar hello en función de carga. 

C#:

```csharp
StatelessServiceUpdateDescription updateDescription = new StatelessServiceUpdateDescription(); 
updateDescription.InstanceCount = 50;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

Powershell:

```posh
Update-ServiceFabricService -Stateless -ServiceName $serviceName -InstanceCount 50
```
### <a name="using-dynamic-instance-count"></a>Uso de recuento de instancias dinámicas
Específicamente para los servicios sin estado, Service Fabric ofrece un recuento de instancias de manera automática toochange Hola. Esto permite Hola servicio tooscale dinámicamente con número de Hola de nodos que están disponibles. Hola forma tooopt de este comportamiento es recuento de instancias de hello tooset = -1. InstanceCount = -1 es un tooService de instrucción tejido que dice "Ejecutar este servicio sin estado en todos los nodos". Si se cambia el número de Hola de nodos, Service Fabric cambia automáticamente toomatch de recuento de instancia de hello, asegurándose de que el servicio de hello está ejecutando en todos los nodos válidos. 

C#:

```csharp
StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
//Set other service properties necessary for creation....
serviceDescription.InstanceCount = -1;
await fc.ServiceManager.CreateServiceAsync(serviceDescription);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName -Stateless -PartitionSchemeSingleton -InstanceCount "-1"
```

## <a name="scaling-by-creating-or-removing-new-named-services"></a>Escalado mediante la creación o eliminación de nuevos servicios con nombre
Una instancia con nombre de servicio es una instancia específica de un tipo de servicio (vea [ciclo de vida de aplicación de Service Fabric](service-fabric-application-lifecycle.md)) dentro de alguna instancia con nombre de aplicación en clúster de Hola. 

Las nuevas instancias de servicio con nombre se pueden crear (o quitar) a medida que los servicios estén más o menos ocupados. Esto permite toobe solicitudes repartidos más instancias de servicio, normalmente lo carga en toodecrease de servicios existente. Al crear servicios, Hola, Administrador de recursos de clúster de tejido de servicio coloca servicios hello en clúster de Hola de manera distribuida. decisiones exacta Hola se rigen por hello [métricas](service-fabric-cluster-resource-manager-metrics.md) en clúster de Hola y otras reglas de selección de ubicación. Los servicios se pueden crear varias maneras diferentes, pero hello más comunes son ya sea a través de acciones administrativas como alguien llamando a [ `New-ServiceFabricService` ](https://docs.microsoft.com/en-us/powershell/module/servicefabric/new-servicefabricservice?view=azureservicefabricps), o mediante una llamada de código [ `CreateServiceAsync` ](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync?view=azure-dotnet). `CreateServiceAsync`Puede incluso llamar desde dentro de otros servicios que se ejecutan en el clúster de Hola.

La creación de servicios dinámicamente puede usarse en todo tipo de escenarios y es un patrón común. Por ejemplo, considere la posibilidad de un servicio con estado que representa un flujo de trabajo determinado. Que representa el trabajo de llamadas van tooshow toothis servicio y este servicio es continuo tooexecute Hola pasos toothat flujo de trabajo y registro del progreso. 

¿Cómo realizaría esta escala del servicio determinado? Hello servicio podría ser apto para multiempresa en alguna forma y llamadas de aceptación y comenzar mismos pasos para distintas instancias del programa Hola a todos a la vez el flujo de trabajo. Sin embargo, que puede dificultar el código de hello, desde ahora tiene tooworry sobre distintas instancias del programa Hola a mismo flujo de trabajo, todo en distintas fases y desde diferentes clientes. Además, Hola a controlar varios flujos de trabajo en hello al mismo tiempo no se soluciona el problema de escala. Esto es porque en algún momento este servicio consumirá demasiados toofit de recursos en un equipo determinado. Muchos servicios que no se creó este patrón en primer lugar de hello también experimentan dificultades debido a un cuello de botella inherente de toosome o ralentiza la ejecución en su código. Estos tipos de problemas de hacer que el servicio de hello no toowork también cuando obtiene mayor número de Hola de flujos de trabajo simultáneas que está realizando el seguimiento.  

Una solución es toocreate una instancia de este servicio para cada instancia de flujo de trabajo de hello diferentes que desee tootrack. Esto es un patrón excelente y funciona si el servicio de hello es con o sin estado. Para este toowork patrón, hay normalmente otro servicio que actúa como un "servicio de administrador de cargas de trabajo". trabajo de Hola de este servicio es tooreceive solicitudes y tooroute esos servicios de tooother de solicitudes. Administrador Hola puede crear dinámicamente una instancia de servicio de carga de trabajo de hello cuando recibe mensajes de bienvenida y, a continuación, pasar en services toothose de solicitudes. servicio de administrador de Hello también podría recibir devoluciones de llamada cuando un servicio de flujo de trabajo determinado complete su trabajo. Cuando el Administrador de hello recibe estas devoluciones de llamada podría eliminar esa instancia de servicio de flujo de trabajo de Hola o dejarla si se esperan más llamadas. 

Las versiones avanzadas de este tipo de administrador de incluso pueden crear grupos de servicios de Hola que administra. grupo de Hello ayuda a garantizar que, cuando llega una nueva solicitud de no tener toowait para hello servicio toospin hasta. En su lugar, el Administrador de hello puede elegir un servicio de flujo de trabajo que no está ocupado actualmente desde el grupo de hello, o enrutar de forma aleatoria. Mantener un grupo de servicios disponibles hace que las nuevas solicitudes de control con mayor rapidez, ya que es menos probable que dicha solicitud hello tiene toowait para un nuevo toobe de servicio Active. La creación de nuevos servicios es rápida, pero no es libre o instantánea. grupo de Hello ayuda a minimizar Hola cantidad de tiempo de solicitud de hello tiene toowait antes de que se están atendidas. A menudo verá este patrón de administrador y de grupo cuando los tiempos de respuesta más importan Hola. Solicitud de hello puesta en cola y crear servicio hello en segundo plano de Hola y _, a continuación,_ pasarlo también es un patrón de administrador populares, como es crear y eliminar servicios basados en algún servicio de seguimiento de cantidad de Hola de trabajo que actualmente tiene pendiente. 

## <a name="scaling-by-creating-or-removing-new-named-application-instances"></a>Escalado mediante la creación o eliminación de nuevas instancias de aplicaciones con nombre
Crear y eliminar instancias de toda la aplicación es el patrón toohello similar de creación y eliminación de servicios. Este patrón, hay algún servicio de administrador que está realizando la decisión de hello en función de las solicitudes de Hola que está viendo e información Hola está recibiendo Hola otros servicios en clúster de Hola. 

¿Cuándo se debe crear una nueva instancia de aplicación con nombre en lugar de crear nuevas instancias de servicio con nombre en alguna aplicación ya existente? Hay algunos casos:

  * la nueva instancia de la aplicación de Hello es para un cliente cuyo código necesita toorun en alguna identidad concreta o configuración de seguridad.
    * Service Fabric permite definir toorun de paquetes de códigos diferentes con identidades determinadas. En orden toolaunch hello mismo paquete de código con identidades diferentes, las activaciones de hello necesario toooccur en instancias de aplicación diferente. Considere la posibilidad de un caso en el que tenga cargas de trabajo implementadas de un cliente existente. Estos pueden ejecutar bajo una identidad concreta para que pueda supervisar y controlar sus tooother acceder a recursos, como bases de datos remotas u otros sistemas. En este caso, cuando un nuevo cliente se suscribe, probablemente no es conveniente tooactivate código de hello mismo contexto (espacio de proceso). Aunque es posible, esto dificulta que los tooact de código de servicio en contexto de Hola de una identidad concreta. Por lo general, debe tener más código de administración de identidad, aislamiento y seguridad. En lugar de usar diferentes con el nombre de servicio instancias dentro Hola la misma instancia de aplicación y, por tanto, Hola mismo espacio de proceso, puede utilizar distintas instancias con nombre de aplicación de tejido de servicio. Esto hace más fácil de contextos de identidad diferentes toodefine.
  * la nueva instancia de la aplicación de Hello también actúa como un medio de configuración
    * De forma predeterminada, todos Hola denominado instancias de servicio de un tipo de servicio determinado dentro de una instancia de la aplicación se ejecutarán en hello mismo proceso en un nodo determinado. Esto significa que aunque puede configurar cada instancia de servicio de forma diferente, hacerlo es complicado. Servicios deben tener algunos token usan toolook seguridad su configuración dentro de un paquete de configuración. Normalmente esto es simplemente el nombre del servicio de Hola. Esto funciona bien, pero acopla con nombres de toohello de configuración de Hola Hola individuales con nombre de instancias de servicio dentro de esa instancia de la aplicación. Esto puede resultar confuso y disco duro toomanage desde configuración suele ser un artefacto de tiempo de diseño con valores específicos de la instancia de aplicación. Crear más servicios siempre significa las actualizaciones de aplicaciones más información de hello toochange dentro de paquetes de configuración de Hola o toodeploy nuevos para que su información específica, pueden buscar servicios nuevos de Hola. A menudo resulta más fácil toocreate una instancia con nombre de aplicación totalmente nueva. A continuación, puede utilizar tooset de parámetros de aplicación Hola cualquier configuración es necesaria para los servicios de Hola. Este modo todos los servicios de Hola que se crean dentro de ese de instancia con nombre de aplicación puede heredar valores de configuración particulares. Por ejemplo, en lugar de tener un único archivo de configuración con las opciones de Hola y las personalizaciones de todos los clientes, como secretos o por los límites de recursos del cliente, en su lugar, tendrás que una instancia de aplicación diferente para cada cliente con esta configuración se reemplaza. 
  * nueva aplicación de Hello actúa como un límite de actualización
    * Dentro de Service Fabric, las instancias de aplicación con nombre diferentes actúan como límites para la actualización. Una actualización de una instancia con nombre de aplicación no afectará al código de hello que está ejecutando otra instancia de aplicación con nombre. Hello distintas aplicaciones terminará ejecutan versiones diferentes del mismo código de hello en hello mismos nodos. Esto puede ser un factor cuando necesite toomake una decisión escala porque se puede elegir que si el nuevo código de hello debe seguir Hola mismo actualiza como otro servicio o no. Por ejemplo, supongamos que una llamada llega al servicio de administrador de Hola que se encarga de ajuste de escala en las cargas de trabajo de un cliente determinado creando y eliminando los servicios de forma dinámica. En este caso no obstante, llamada hello es para una carga de trabajo asociado con un _nueva_ al cliente. Mayoría de los clientes que estar aisladas entre sí no solo por razones de seguridad y la configuración de hello indicadas anteriormente, pero porque ofrece mayor flexibilidad en cuanto a ejecutando versiones específicas de software de Hola y de elegir cuándo actualizará. También puede crear una nueva instancia de la aplicación y crear servicio Hola allí simplemente toofurther partición Hola cantidad de los servicios que se tocan cualquier una actualización. Las instancias de aplicaciones independientes proporcionan mayor granularidad al realizar las actualizaciones de aplicación y también permiten las pruebas A/B y las implementaciones Azul/Verde. 
  * instancia de aplicación existente de Hello está lleno
    * En Service Fabric, [capacidad de las aplicaciones](service-fabric-cluster-resource-manager-application-groups.md) es un concepto que puede usar la cantidad de hello toocontrol de recursos disponibles para instancias de aplicación determinado. Por ejemplo, puede decidir que un servicio determinado necesita toohave otra instancia que se creó en orden tooscale. Sin embargo, esta instancia de aplicación está fuera de su capacidad para una métrica determinada. Si este cliente en particular o la carga de trabajo todavía se debe conceder más recursos, a continuación, se podría aumentar capacidad existente de Hola para esa aplicación o cree una nueva aplicación. 

## <a name="scaling-at-hello-partition-level"></a>Ajuste de escala en el nivel de partición de Hola
Service Fabric es compatible con la creación de particiones. La partición divide un servicio en varias secciones lógicas y físicas, cada una de las cuales actúa independientemente. Esto es útil con los servicios con estado, ya que ningún otro conjunto de réplicas tiene toohandle todas las llamadas de Hola y manipular todo Estado Hola al mismo tiempo. Hola [información general de creación de particiones](service-fabric-concepts-partitioning.md) proporciona información sobre los tipos de Hola de esquemas de partición que se admiten. réplicas de Hola de cada partición se reparten entre nodos de hello en un clúster, la distribución de carga de dicho servicio y asegurarse de que ninguno de estos servicios Hola como un todo o cualquier partición tiene un único punto de error. 

Considere la posibilidad de que un servicio que usa un esquema de particiones de intervalo con una clave baja de 0, una clave alta de 99 y un recuento de 4 particiones. En un clúster de tres nodos, podría dispuesto servicio Hola con cuatro réplicas que comparten recursos de hello en cada nodo tal y como se muestra aquí:

<center>
![Diseño de partición con tres nodos](./media/service-fabric-concepts-scalability/layout-three-nodes.png)
</center>

Si se aumenta el número de Hola de nodos, Service Fabric moverá algunas de las réplicas existentes de hello no existe. Por ejemplo, supongamos que aumenta el número de Hola de nodos toofour y obtengan redistribuir réplicas Hola. Ahora el servicio de hello tiene ahora tres réplicas que se ejecutan en cada nodo, cada uno de ellos que pertenecen toodifferent particiones. Esto permite una mejor utilización de recursos desde el nuevo nodo de hello no está frío. Normalmente, también aumenta el rendimiento ya que cada servicio tiene más tooit de recursos disponibles.

<center>
![Diseño de partición con cuatro nodos](./media/service-fabric-concepts-scalability/layout-four-nodes.png)
</center>

## <a name="scaling-by-using-hello-service-fabric-cluster-resource-manager-and-metrics"></a>Ajuste de escala mediante Hola, Administrador de recursos de clúster de Service Fabric y métricas
[Las métricas](service-fabric-cluster-resource-manager-metrics.md) son cómo services express su tooService de consumo de recursos tejido. Usar las métricas le ofrece Hola, Administrador de recursos del clúster un tooreorganize oportunidad y optimizar el diseño de Hola de clúster de Hola. Por ejemplo, puede haber una gran cantidad de recursos de clúster de hello, pero no se pueden asignar servicios toohello que actualmente se están realizando el trabajo. Usar las métricas de permite hello tooreorganize del Administrador de recursos del clúster Hola clúster tooensure que los servicios tienen acceso toohello de recursos disponibles. 


## <a name="scaling-by-adding-and-removing-nodes-from-hello-cluster"></a>Ajuste de escala agregando y quitando nodos de clúster de Hola 
Otra opción para ajustar la escala con Service Fabric es el tamaño de Hola de toochange de clúster de Hola. Cambiar el tamaño de Hola de clúster de hello significa agregar o quitar nodos en uno o varios de los tipos de nodos de hello en clúster de Hola. Por ejemplo, considere un caso de que todos los nodos de hello en clúster de hello estén activos. Esto significa que los recursos del clúster de hello son casi todo consumido. En este caso, agregar más toohello nodos clúster es Hola mejor manera tooscale. Una vez que los nuevos nodos de hello unir Hola Hola de clúster Administrador de recursos de clúster de tejido de servicio mueve toothem de servicios, resultante total menos carga en los nodos existentes Hola. Para servicios sin estado con un recuento de instancias = -1, se crean automáticamente más instancias de servicio. Esto permite que algunos toomove de llamadas de hello existente nodos toohello nuevos nodos. 

Agregar y quitar nodos toohello clúster puede realizarse a través del módulo de PowerShell del Administrador de recursos del servicio tejido Azure Hola.

```posh
Add-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName  -NumberOfNodesToAdd 5 
Remove-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName -NumberOfNodesToRemove 5
```

## <a name="putting-it-all-together"></a>Resumen
¡Eche todas las ideas de Hola que se ha explicado aquí y hablar a través de un ejemplo. Considere la posibilidad de hello después de servicio: está tratando de toobuild un servicio que actúa como una libreta de direcciones, que contiene información de contacto y toonames. 

Derecha por adelantado tiene una serie de preguntas relacionadas tooscale: ¿cuántos usuarios hay toohave continua? ¿Cuántos contactos almacenará cada usuario? Cuando se permanente configurar el servicio para hello primera vez es difícil intentar toofigure esto es todo. Supongamos que va toogo con un único servicio estático con un número de partición específica. consecuencias de Hola de selección Hola incorrecto de recuento de particiones puede causar problemas de escalabilidad de toohave más tarde. De igual forma, incluso si elige el recuento de derecho de hello que podría no tener toda la información de hello debe. Por ejemplo, también se tienen toodecide Hola tamaño de clúster de Hola por adelantado, tanto en términos de número de Hola de nodos y sus tamaños. Su disco duro normalmente toopredict cuántos recursos un servicio va tooconsume durante su vida útil. También puede ser tooknow disco duro antes de patrón de tráfico de Hola de tiempo que el servicio de hello ve realmente. Por ejemplo, personas maybe agregar y quitar sus contactos sólo lo primero de mañana hello, o puede ser se distribuye por igual durante Hola de día de Hola. Se basa en el objeto que tenga tooscale y dinámicamente. Quizá puede obtener información toopredict cuando se vayan tooneed tooscale y, pero en cualquier caso que probablemente vaya consumo de recursos de tooneed tooreact toochanging por el servicio. Esto puede implicar cambiar el tamaño de Hola de clúster de hello en orden tooprovide más recursos cuando la reorganización de uso de recursos existentes no es suficiente. 

Pero ¿por qué incluso intente toopick un esquema de partición único out para todos los usuarios? ¿Por qué limitarse tooone servicio y un clúster estático? situación real de Hello es normalmente más dinámica. 

Al compilar para la escala, considere la posibilidad de seguir un patrón dinámico de Hola. Puede que necesite tooadapt se tooyour situación:

1. En lugar de intentar toopick un esquema de partición para todos los usuarios por adelantado, crear un "servicio de administrador".
2. trabajo de Hello del servicio del Administrador de hello es toolook en la información del cliente cuando se registren para el servicio. A continuación, según esa información de servicio de administrador de hello cree una instancia de su _real_ servicio de almacenamiento de información de contacto _solo para ese cliente_. Si requieren configuración específica, aislamiento o las actualizaciones, también puede decidir toospin una instancia de la aplicación para este cliente. 

Este patrón dinámico de creación implica muchas ventajas:

  - No se trata de recuento de partición correcta de hello tooguess para todos los usuarios por adelantado o crear un servicio único que es infinitamente escalable por sí mismo. 
  - Distintos usuarios no tienen hello toohave misma partición recuento, número de réplicas, las restricciones de posición, métricas, carga de forma predeterminada, los nombres de servicio, configuración de dns ni ninguno de hello otras propiedades especificadas en el servicio de Hola o nivel de aplicación. 
  - Obtiene una segmentación de datos adicional. Cada cliente tiene su propia copia del servicio de Hola
    - El servicio de cada cliente se puede configurar de forma distinta y se le puede conceder más o menos recursos, con más o menos particiones o réplicas según sea necesario en función de la escala esperada.
      - Por ejemplo, cliente hello pagaste Hola nivel "Gold": se obtienen más réplicas o recuento de particiones mayor y potencialmente recursos dedicados tootheir servicios a través de las capacidades de las métricas y la aplicación.
      - O supongamos proporciona información que indica el número de Hola de contactos que necesitan era "Pequeño", obtendrían solo algunas particiones o incluso puede poner en un grupo de servicios compartidos con otros clientes.
  - No ejecuta una serie de instancias de servicio o réplicas mientras espera para los clientes tooshow seguridad
  - Si alguna vez deja de tener un cliente, a continuación, quite su información de su servicio es tan simple como que el Administrador de hello eliminar ese servicio o aplicación que lo creó.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre conceptos de Service Fabric, vea Hola siguientes artículos:

* [Disponibilidad de los servicios de Service Fabric](service-fabric-availability-services.md)
* [Creación de particiones de los servicios de Service Fabric](service-fabric-concepts-partitioning.md)
