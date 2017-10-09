---
title: Modelo de hospedaje de servicio tejido aaaAzure | Documentos de Microsoft
description: "Describe la relación entre las réplicas o las instancias de un servicio implementado de Service Fabric y el proceso de host de servicio."
services: service-fabric
documentationcenter: .net
author: harahma
manager: timlt
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/15/2017
ms.author: harahma
ms.openlocfilehash: 30e0ba19cd672a722f76477a311ecef7c213b055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-hosting-model"></a>Modelo de hospedaje de Service Fabric
Este artículo proporciona una visión general de la aplicación que hospeda modelos proporcionados por Service Fabric y describe las diferencias de hello entre hello **proceso compartido** y **proceso exclusivo** modelos. Describe el aspecto de una aplicación implementada en un nodo de Service Fabric y una relación entre las réplicas (o instancias) de servicio de Hola y el proceso de host de servicio de Hola.

Antes de continuar, asegúrese de que está familiarizado con el [Modelo de aplicación de Service Fabric][a1] y de que conoce los diferentes conceptos y la relación entre ellos. 

> [!NOTE]
> En este artículo, para simplificar, a menos que se mencione explícitamente:
>
> - Todos los usos de la palabra *réplica* hace referencia a una réplica de un servicio con estado o una instancia de un servicio statless tooboth.
> - *CodePackage* tratados equivale demasiado*ServiceHost* proceso que se registra un *ServiceType* y réplicas de hosts de servicios, que *ServiceType*.
>

toounderstand Hola modelo de hospedaje, permítanos dirigirle a través de un ejemplo. Se supone que hay una instancia de *ApplicationType* llamada "MyAppType" que tiene un valor de *ServiceType* "MyServiceType" proporcionado por *ServicePackage* "MyServicePackage" que incluye una instancia de *CodePackage* "MyCodePackage" que registra *ServiceType* "MyServiceType" cuando se ejecuta.

Por ejemplo, hay un clúster de 3 nodos y se crea una *aplicación* **fabric:/App1** de tipo "MyAppType". Dentro de la *aplicación* **fabric:/App1**, se crea un servicio **fabric:/App1/ServiceA** de tipo "MyServiceType" que tiene 2 particiones (**P1** & **P2**) y 3 réplicas por cada partición. Hello siguiente diagrama muestra vista Hola de esta aplicación tal como se termina implementado en un nodo.

<center>
![Vista del nodo de la aplicación implementada][node-view-one]
</center>

Service Fabric activado 'MyServicePackage', que se inicia 'MyCodePackage', que estará hospedando, es decir, las réplicas de las particiones de hello **P1** & **P2**. Tenga en cuenta que todos los nodos Hola Hola clúster tendrá la misma vista dado que elegimos número de réplicas por partición toonumber igual de nodos de clúster de Hola. Se va a crear otro servicio **fabric:/App1/ServiceB** en la aplicación **fabric:/App1** que tiene 1 partición (**P3**) y 3 réplicas por cada partición. Diagrama siguiente muestra la nueva vista de hello en el nodo de hello:

<center>
![Vista del nodo de la aplicación implementada][node-view-two]
</center>

Como podemos ver Service Fabric colocar la nueva réplica de partición de hello **P3** del servicio **fabric: / App1/ServiceB** en la activación existente de Hola de 'MyServicePackage'. Ahora se crea otra *aplicación* **fabric:/App2** de tipo "MyAppType" y, dentro de **fabric:/App2**, se crea el servicio **fabric:/App2/ServiceA**, que tiene 2 particiones (**P4** & **P5**) y 3 por cada partición. Después de diagramas muestran nueva vista del nodo hello:

<center>
![Vista del nodo de la aplicación implementada][node-view-three]
</center>

En esta ocasión, Service Fabric ha activado una nueva copia de "MyServicePackage" que inicia una nueva copia de "MyCodePackage", y las réplicas de las dos particiones del servicio **fabric:/App2/ServiceA** (es decir, **P4** & **P5**) se colocan en esta nueva copia "MyCodePackage".

## <a name="shared-process-model"></a>Modelo de proceso compartido
Lo que hemos visto anteriormente es el predeterminado de hello proporcionada por Service Fabric de modelo para alojamiento y es conoce tooas **proceso compartido** modelo. En este modelo, para un determinado *aplicación*, solo una copia de un determinado *ServicePackage* se activa en un *nodo* (que empieza Hola todos los *CodePackages* contenidas en ella) y todos los Hola réplicas de todos los servicios de un determinado *ServiceType* se colocan en hello *CodePackage* que registra *ServiceType*. En otras palabras, Hola a todas las réplicas de todos los servicios de un determinado *ServiceType* compartir Hola mismo proceso.

## <a name="exclusive-process-model"></a>Modelo de proceso exclusivo
Hello otro modelo de hospedaje proporcionado por Service Fabric es **proceso exclusivo** modelo. En este modelo, en un determinado *nodo*, para colocar cada réplica, Service Fabric activa una nueva copia del *ServicePackage* (que empieza Hola todos los *CodePackages* contenidas en ella ) y réplica se coloca en hello *CodePackage* ese Hola registrado *ServiceType* de hello servicio toowhich pertenece la réplica. En otras palabras, cada réplica reside en su propio proceso dedicado. 

Este modelo se admite a partir de la versión 5.6 de Service Fabric. **Proceso exclusivo** modelo se puede seleccionar en el momento de Hola de creación de servicio de hello (mediante [PowerShell][p1], [REST] [ r1]o [FabricClient][c1]) mediante la especificación de **ServicePackageActivationMode** como 'ExclusiveProcess'.

```powershell
PS C:\>New-ServiceFabricService -ApplicationName "fabric:/App1" -ServiceName "fabric:/App1/ServiceA" -ServiceTypeName "MyServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1 -ServicePackageActivationMode "ExclusiveProcess"
```

```csharp
var serviceDescription = new StatelessServiceDescription
{
    ApplicationName = new Uri("fabric:/App1"),
    ServiceName = new Uri("fabric:/App1/ServiceA"),
    ServiceTypeName = "MyServiceType",
    PartitionSchemeDescription = new SingletonPartitionSchemeDescription(),
    InstanceCount = -1,
    ServicePackageActivationMode = ServicePackageActivationMode.ExclusiveProcess
};

var fabricClient = new FabricClient(clusterEndpoints);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Si el manifiesto de aplicación contiene un servicio predeterminado, puede elegir el modelo de **proceso exclusivo** si especifica el atributo **ServicePackageActivationMode** como se muestra a continuación:

```xml
<DefaultServices>
  <Service Name="MyService" ServicePackageActivationMode="ExclusiveProcess">
    <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
      <SingletonPartition/>
    </StatelessService>
  </Service>
</DefaultServices>
```
Continuando con el ejemplo anterior, permite crear otro servicio **fabric: / App1/ServiceC** en aplicación **fabric: / App1** que tiene 2 particiones (diga **P6**  &  **P7**) y 3 réplicas por partición con **ServicePackageActivationMode** establecer 'too'ExclusiveProcess. Diagrama siguiente muestra la nueva vista en el nodo de hello:

<center>
![Vista del nodo de la aplicación implementada][node-view-four]
</center>

Como se puede observar, Service Fabric ha activado dos copias de "MyServicePackage" (una para cada réplica de la partición **P6** & **P7**) y ha colocado cada réplica en su copia dedicada de *CodePackage*. Es otro toonote de lo aquí, cuando **proceso exclusivo** se utiliza el modelo, para un determinado *aplicación*, varias copias de un determinado *ServicePackage* pueden estar activas en un  *Nodo*. En el ejemplo anterior, se observa que hay tres copias de "MyServicePackage" activas para **fabric:/App1**. Cada una de estas copias activas de "MyServicePackage" tiene un **ServicePackageAtivationId** asociado a ella que identifica dicha copia en la *aplicación* **fabric:/App1**.

Si solo se usa el modelo de **proceso compartido** para una *aplicación*, como **fabric:/App2** en el ejemplo anterior, solo hay una copia activa de *ServicePackage* en un *nodo*, y **ServicePackageAtivationId** en esta activación de *ServicePackage* es una "cadena vacía".

> [!NOTE]
>- **Proceso compartido** modelo para alojamiento corresponde demasiado**ServicePackageAtivationMode** igual **SharedProcess**. Se trata de predeterminado Hola modelo para alojamiento y **ServicePackageAtivationMode** no es necesario especificar en tiempo de Hola de creación de servicio de Hola.
>
>- **Proceso exclusivo** modelo para alojamiento corresponde demasiado**ServicePackageAtivationMode** igual **ExclusiveProcess** y necesita toobe especifica explícitamente en tiempo de Hola de creación de hello servicio. 
>
>- Modelo de hospedaje de un servicio puede conocerse consultando hello [descripción del servicio] [ p2] y examinando el valor de **ServicePackageAtivationMode**.
>
>

## <a name="working-with-deployed-service-package"></a>Trabajo con el paquete de servicio implementado
A una copia activa de *ServicePackage* en un nodo se le denomina [paquete de servicio implementado][p3]. Como se mencionó anteriormente, cuando **proceso exclusivo** modelo se utiliza para crear servicios, para un determinado *aplicación*, pueden producirse errores servicio implementado varios paquetes para hello mismo  *ServicePackage*. Al realizar operaciones como paquete de servicio específico toodeployed [informar sobre el estado de un paquete de servicio implementado] [ p4] o [reiniciar el paquete de código de un paquete de servicio implementado] [ p5] etc., **ServicePackageActivationId** toobe necesidades proporciona tooidentify un paquete específico de servicio implementado.

 **ServicePackageActivationId** de un servicio implementado el paquete puede obtenerse consultando la lista de Hola de [paquetes de servicio implementados] [ p3] en un nodo. Cuando se consultan [implementa tipos de servicio][p6], [implementa réplicas] [ p7] y [implementado paquetes de código] [ p8] en un nodo, resultado de la consulta de hello también contiene hello **ServicePackageActivationId** del paquete de servicio principal implementada.

> [!NOTE]
>- En el modelo de hospedaje de **proceso compartido** de un *nodo* concreto para una *aplicación* determinada, solo se activa una copia de un *ServicePackage*. Tiene **ServicePackageActivationId** igual demasiado*una cadena vacía* y no es necesario especificar mientras las operaciones relacionadas con el paquete de servicio implementado de rendimiento. 
>
> - En el modelo de hospedaje de **proceso exclusivo** de un *nodo* concreto para una *aplicación* determinada, pueden activarse una o varias copias de *ServicePackage*. Cada activación tiene un *no vacía* **ServicePackageActivationId** y toobe especifican mientras que las operaciones relacionadas con el paquete de servicio implementado rendimiento es necesario. 
>
> - Si **ServicePackageActivationId** es ommited el valor predeterminado es too'empty cadena '. Si un servicio implementado del paquete que se activó en **proceso compartido** modelo está presente, a continuación, se realizará la operación en él, en caso contrario, la operación de Hola se producirá un error.
>
> - No se recomienda tooquery una vez y caché **ServicePackageActivationId** ya que se genera dinámicamente y se puede cambiar por varias razones. Antes de realizar una operación que necesita **ServicePackageActivationId**, primero debe consultar la lista de Hola de [paquetes de servicio implementados] [ p3] en un nodo y, después, use  *ServicePackageActivationId** de operación original de consulta resultado tooperform Hola.
>
>

## <a name="guest-executable-and-container-applications"></a>Aplicaciones de contenedor y de archivo ejecutable invitado
Service Fabric trata las aplicaciones de [archivo ejecutable invitado][a2] y de [contenedor][a3] como servicios con estado con almacenamiento; es decir, no hay runtime de Service Fabric en *ServiceHost* (un proceso o contenedor). Como se trata de servicios con almacenamiento, el número de réplicas por *ServiceHost* no es aplicable para estos servicios. Hola configuración más común utilizado con estos servicios es única partición con [InstanceCount] [ c2] igual demasiado-1 (es decir, una copia del código de servicio de hello ejecuta en cada nodo del clúster). 

Hola predeterminado **ServicePackageActivationMode** para estos servicios es **SharedProcess** en cuyo caso Service Fabric solo activa una copia de *ServicePackage* en un *Nodo* para un determinado *aplicación* lo que significa que solo una copia del código de servicio se ejecutará una *nodo*. Si desea que varias copias de los toorun de código de servicio en un *nodo* cuando se crean varios servicios (*Service1* demasiado*ServiceN*) de *ServiceType* (especificado en *ServiceManifest*) o cuando el servicio está con varias particiones, debe especificar **ServicePackageActivationMode** como **ExclusiveProcess**en tiempo de Hola de creación de servicio de Hola.

## <a name="changing-hosting-model-of-an-existing-service"></a>Cambio del modelo de hospedaje de un servicio existente
Cambiar el modelo de hospedaje de un servicio existente de **proceso compartido** demasiado**proceso exclusivo** y viceversa a través de actualizar o mecanismo de actualización (o especificación de aplicación de servicio predeterminados manifiesto) no se admite actualmente. La compatibilidad con esta característica se incluirá en futuras versiones.

## <a name="choosing-between-shared-process-and-exclusive-process-model"></a>Elección del modelo de proceso compartido o exclusivo
Estos modelos de hospedaje tienen sus ventajas e inconvenientes tanto el usuario debe tooevaluate cuál se adapta mejor a sus requisitos. **Proceso compartido** modelo permite una mejor utilización de recursos del SO porque se generan menos procesos, Hola varias réplicas en el mismo proceso puede compartir puertos, etcetera. Sin embargo, si una de las réplicas de hello produce un error donde debe toobring hacia abajo de host de servicio de hello, afectará a todas las demás réplicas en el mismo proceso.

 El modelo de **proceso exclusivo** ofrece un aislamiento mejorado de cada réplica en su propio proceso, por lo que la réplica que presenta un comportamiento incorrecto no afectará a las demás. Se trata práctica en casos donde uso compartido de puertos no es compatible con el protocolo de comunicación de Hola. Facilita la regulación de recursos de tooapply de capacidad de hello en nivel de réplica. Hola en otra parte, **proceso exclusivo** consumirá más recursos de sistema operativo tal y como lo genera un proceso para cada réplica en el nodo de Hola.

## <a name="exclusive-process-model-and-application-model-considerations"></a>Consideraciones sobre el modelo de proceso exclusivo y el modelo de aplicación
Hola recomienda forma toomodel la aplicación de Service Fabric es tookeep una *ServiceType* por *ServicePackage* y este modelo funciona bien para la mayoría de las aplicaciones de Hola. 

Sin embargo, tooenable especiales escenarios donde un *ServiceType* por *ServicePackage* puede no ser deseable, funcionalmente, Service Fabric permite toohave más de una *ServiceType* por *ServicePackage* (y una *CodePackage* puede registrar más de un *ServiceType*). Siguientes son algunos de los escenarios de Hola donde estas configuraciones pueden ser útiles:

- Utilización de recursos del sistema operativo toooptimize que desee generando menos procesos y tener una mayor densidad de réplica por proceso.
- Réplicas de diferentes ServiceTypes deben tooshare algunos datos comunes que tiene una alta inicialización o el costo de memoria.
- Tiene una oferta de servicio gratuito y desea tooput un límite en la utilización de recursos colocando todas las réplicas del servicio de hello en el mismo proceso.

El modelo de hospedaje de **proceso exclusivo** no es coherente con el modelo de aplicación que tiene varias instancias de *ServiceTypes* por cada *ServicePackage*. Se trata porque varios *ServiceTypes* por *ServicePackage* tooachieve diseñada recurso mayor uso compartido entre las réplicas y permite una mayor densidad de réplica por proceso. Se trata de contraria toowhat **proceso exclusivo** modelo está diseñado tooachieve.

Considere la posibilidad de caso de hello de varios *ServiceTypes* por *ServicePackage* con diferentes *CodePackage* registrar cada *ServiceType*. Por ejemplo, existe un *ServicePackage* "MultiTypeServicePackge" que tiene dos *CodePackages*:

- "MyCodePackageA", que registra el *ServiceType* "MyServiceTypeA".
- "MyCodePackageB", que registra el *ServiceType* "MyServiceTypeB".

Ahora, por ejemplo, se crea una *aplicación* **fabric:/SpecialApp** y, dentro de **fabric:/SpecialApp**, se crean los dos servicios siguientes con el modelo de **proceso exclusivo**:

- El servicio **fabric:/SpecialApp/ServiceA** de tipo "MyServiceTypeA" con dos particiones (**P1** y **P2**) y 3 réplicas por partición.
- El servicio **fabric:/SpecialApp/ServiceB** de tipo "MyServiceTypeB" con dos particiones (**P3** y **P4**) y 3 réplicas por partición.

En un nodo determinado, ambos servicios Hola tendrá dos réplicas. Ya que hemos usado **proceso exclusivo** servicios del modelo toocreate hello, Service Fabric activará una nueva copia de 'MyServicePackge' para cada réplica. Cada activación de "MultiTypeServicePackge" iniciará una copia de "MyCodePackageA" y "MyCodePackageB". Sin embargo, solo uno de 'MyCodePackageA' o 'MyCodePackageB' hospedará la réplica de hello para el que se activó 'MultiTypeServicePackge'. Diagrama siguiente muestra la vista de nodo de hello:

<center>
![Vista del nodo de la aplicación implementada][node-view-five]
</center>

 Como se puede observar en la activación de Hola de 'MultiTypeServicePackge' para la réplica de partición **P1** del servicio **fabric: / SpecialApp/Services como**, 'MyCodePackageA' hospeda la réplica de Hola y ' MyCodePackageB' está solo en funcionamiento. De forma similar, en la activación de 'MultiTypeServicePackge' para la réplica de partición **P3** del servicio **fabric: / SpecialApp/ServiceB**, 'MyCodePackageB' hospeda la réplica de Hola y es 'MyCodePackageA' simplemente activa y en funcionamiento y así sucesivamente. Por lo tanto, más Hola número de *CodePackages* (registrar diferentes *ServiceTypes*) por *ServicePackage*, mayor será el uso de recursos redundantes. 
 
 Hola en otra parte Si creamos servicios **fabric: / SpecialApp/Services como** y **fabric: / SpecialApp/ServiceB** con **proceso compartido** modelar, will Service Fabric activar solo una copia de 'MultiTypeServicePackge' para *aplicación* **fabric: / SpecialApp** (tal y como se ha explicado anteriormente). 'MyCodePackageA' hospedará todas las réplicas de servicio **fabric: / SpecialApp/Services como** (o de cualquier servicio de tipo 'MyServiceTypeA' toobe más preciso) y 'MyCodePackageB' hospedará todas las réplicas de servicio **fabric: / SpecialApp/ServiceB** (o de cualquier servicio de tipo 'MyServiceTypeB' toobe más preciso). Diagrama siguiente muestra la vista de nodo de hello en esta configuración: 

<center>
![Vista del nodo de la aplicación implementada][node-view-six]
</center>

Hola ejemplo anterior, puede que piense si 'MyCodePackageA' registra 'MyServiceTypeA' y 'MyServiceTypeB' y no hay ningún 'MyCodePackageB', habrá no redundante *CodePackage* ejecutando. Este planteamiento es correcto, pero, como se ha mencionado anteriormente, este modelo de aplicación no es compatible con el modelo de hospedaje de **proceso exclusivo**. Si el objetivo es tooput cada réplica en su propio dedicado de proceso y volver a registrar ambos *ServiceTypes* desde el mismo *CodePackage* no es necesario y colocar cada *ServiceType* en su propio *ServicePacakge* es una elección más natural.

## <a name="next-steps"></a>Pasos siguientes
[Empaquetar una aplicación] [ a4] y obtener toodeploy listo.

[Implementar y quitar aplicaciones] [ a5] describe cómo toouse instancias de la aplicación de toomanage de PowerShell.

<!--Image references-->
[node-view-one]: ./media/service-fabric-hosting-model/node-view-one.png
[node-view-two]: ./media/service-fabric-hosting-model/node-view-two.png
[node-view-three]: ./media/service-fabric-hosting-model/node-view-three.png
[node-view-four]: ./media/service-fabric-hosting-model/node-view-four.png
[node-view-five]: ./media/service-fabric-hosting-model/node-view-five.png
[node-view-six]: ./media/service-fabric-hosting-model/node-view-six.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[a1]: service-fabric-application-model.md
[a2]: service-fabric-deploy-existing-app.md
[a3]: service-fabric-containers-overview.md
[a4]: service-fabric-package-apps.md
[a5]: service-fabric-deploy-remove-applications.md

[r1]: https://docs.microsoft.com/rest/api/servicefabric/sfclient-api-createservice

[c1]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync
[c2]: https://docs.microsoft.com/dotnet/api/system.fabric.description.statelessservicedescription.instancecount

[p1]: https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricservice
[p2]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricservicedescription
[p3]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicePackage
[p4]: https://docs.microsoft.com/powershell/servicefabric/vlatest/send-servicefabricdeployedservicepackagehealthreport
[p5]: https://docs.microsoft.com/powershell/servicefabric/vlatest/restart-servicefabricdeployedcodepackage
[p6]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicetype
[p7]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedreplica
[p8]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedcodepackage