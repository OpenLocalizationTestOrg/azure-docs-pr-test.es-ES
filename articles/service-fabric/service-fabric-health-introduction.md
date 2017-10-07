---
title: "supervisión de aaaHealth en Service Fabric | Documentos de Microsoft"
description: "Un Introducción toohello Azure Service Fabric el estado del modelo, que proporciona una supervisión de clúster de Hola y sus aplicaciones y servicios de supervisión."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 1d979210-b1eb-4022-be24-799fd9d8e003
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 904f36374ca6ca7e4caa1d43c92584e7e4c50087
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-health-monitoring"></a>Supervisión de estado del tejido de tooService de introducción
Azure Service Fabric presenta un modelo de mantenimiento que proporciona informes y datos de evaluación del mantenimiento completos, flexibles y extensibles. modelo de Hello permite la supervisión en tiempo casi real del estado de Hola de clúster de Hola y servicios de Hola que se ejecutan en él. Puede obtener con facilidad información sobre el mantenimiento, y corregir posibles problemas antes de que se propaguen y causen interrupciones masivas. Modelo típico de hello, servicios de enviar informes basados en sus vistas locales y que la información es agregan tooprovide una vista general de nivel de clúster.

Los componentes de Service Fabric utilizan este tooreport de modelo de mantenimiento enriquecido sus estados actuales. Puede usar Hola el estado del mismo mecanismo tooreport de las aplicaciones. Si invierte en informes sobre el mantenimiento de alta calidad, que capturan sus condiciones personalizadas, puede detectar y corregir problemas de la aplicación en ejecución mucho más fácilmente.

Hola que siguiente Microsoft Virtual Academy vídeo también describe modelo de estado de Service Fabric de Hola y cómo se utiliza:<center><a target="_blank" href="https://mva.microsoft.com/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-health-introduction/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

> [!NOTE]
> Comenzamos Hola mantenimiento subsistema tooaddress necesario para las actualizaciones supervisadas. Service Fabric proporciona actualizaciones de aplicación y clúster supervisadas que no garantizar la disponibilidad completa, tiempo de inactividad y toono mínima intervención del usuario. tooachieve estos objetivos, la actualización de hello comprueba el estado en función de configura las directivas de actualización. Una actualización puede continuar solo cuando el estado respeta los umbrales deseados. En caso contrario, actualización de Hola o revierte automáticamente o en pausa toogive administradores un problemas de hello toofix de oportunidad. toolearn más información acerca de las actualizaciones de aplicaciones, consulte [este artículo](service-fabric-application-upgrade.md).
> 
> 

## <a name="health-store"></a>Almacén de estado
el almacén de estado de Hola mantiene información relacionada con el estado sobre las entidades en clúster de Hola para facilitar la recuperación y la evaluación. Se implementa un Service Fabric conservada servicio con estado tooensure alta disponibilidad y escalabilidad. almacén de estado Hello forma parte del programa Hola a **fabric: / sistema** aplicación y está disponible cuando Hola clúster está activo y en ejecución.

## <a name="health-entities-and-hierarchy"></a>Jerarquía y entidades de mantenimiento
entidades de mantenimiento de Hola se organizan en una jerarquía lógica que captura las interacciones y las dependencias entre distintas entidades. almacén de estado de Hello automáticamente crea entidades de mantenimiento y jerarquía basada en los informes procedentes de los componentes de Service Fabric.

entidades de mantenimiento de Hello reflejan las entidades de Service Fabric Hola. (Por ejemplo, **entidad de la aplicación de mantenimiento** coincide con una instancia de la aplicación implementados en clúster de hello, mientras **entidad del nodo de estado** coincide con un nodo de clúster de Service Fabric.) captura la jerarquía de estado de Hola interacciones de Hola de las entidades del sistema hello y es la base de hello para la evaluación de mantenimiento avanzadas. Para obtener información sobre los conceptos clave de Service Fabric, consulte [Información general sobre la terminología de Service Fabric](service-fabric-technical-overview.md). Para obtener más información sobre la aplicación, consulte [Modelar una aplicación en Service Fabric](service-fabric-application-model.md).

jerarquía y entidades de mantenimiento de hello permiten Hola toobe de clúster y aplicaciones notificado, depurar y supervisar eficazmente. Proporciona un tipo de objeto, modelo de estado de Hello *granular* representación del estado de Hola de Hola muchos datos móviles en clúster de Hola.

![Entidades de mantenimiento.][1]
entidades de mantenimiento de Hello, organizadas en una jerarquía basada en relaciones primarias y secundarias.

[1]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy.png

las entidades de mantenimiento de Hello son:

* **Clúster**. Representa el estado de saludo de un clúster de Service Fabric. Informes de mantenimiento de clúster describen las condiciones que afectan al clúster completo Hola. Estas condiciones afectan a varias entidades en clúster de Hola u Hola propio. En función de la condición de hello, Informador de hello no puede restringir problema Hola abajo tooone o más elementos secundarios incorrecto. Algunos ejemplos son cerebro de hello del clúster Hola división debido a problemas de comunicación o creación de particiones de toonetwork.
* **Nodo**. Representa el estado de saludo de un nodo de Service Fabric. Informes de mantenimiento de nodo describen las condiciones que afectan a la funcionalidad de nodo de Hola. Por lo general afectan a todas las entidades de hello implementado en ejecución. Entre los ejemplos se incluyen que un nodo se quede sin espacio en disco (u otra propiedad de la máquina como la memoria o las conexiones) y cuando un nodo está inactivo. entidad del nodo de Hola se identifica por su nombre de nodo de hello (cadena).
* **Aplicación**. Representa el estado de saludo de una instancia de aplicación que se ejecuta en el clúster de Hola. Informes de mantenimiento de aplicación describen las condiciones que afectan a Hola estado general de la aplicación hello. No puede localizarse tooindividual los elementos secundarios (servicios o aplicaciones implementadas). Algunos ejemplos son interacción to-end de hello entre diferentes servicios en la aplicación hello. entidad de aplicación Hola se identifica mediante el nombre de la aplicación hello (URI).
* **Servicio**. Representa el estado de saludo de un servicio que se ejecuta en el clúster de Hola. Informes de mantenimiento del servicio se describen las condiciones que afectan a Hola el estado general del servicio de Hola. indicador de Hello no se puede reducir partición incorrecto de hello problema tooan o réplica. Entre los ejemplos se incluye una configuración del servicio (como un puerto o un recurso compartido de archivos externo) que causa problemas en todas las particiones. entidad de servicio de Hola se identifica por nombre de servicio de hello (URI).
* **Partición**. Representa el estado de saludo de una partición de servicio. Informes de mantenimiento de partición describen las condiciones que afectan al conjunto de réplicas entero Hola. Por ejemplo, al número de Hola de réplicas es inferior al recuento de destino y cuando una partición es pérdida de quórum. entidad de la partición de Hola se identifica por partición Hola identificador (GUID).
* **Réplica**. Representa el estado de saludo de una réplica de servicio con estado o una instancia de servicio sin estado. réplica de Hello es la unidad más pequeña de Hola que watchdogs y componentes del sistema pueden informar de una aplicación. Para los servicios con estado, algunos ejemplos son una réplica principal que no se puede replicar toosecondaries de operaciones y la replicación es lenta. Además, se puede notificar una instancia sin estado si se está quedando sin recursos o tiene problemas de conectividad. entidad de réplica de Hola se identifica mediante Hola partición hello y el identificador (GUID) réplica o instancia de identificador (long).
* **DeployedApplication**. Representa Hola mantenimiento de un *aplicación se ejecuta en un nodo*. Informes de estado de aplicación implementada describen la aplicación de toohello específicos de las condiciones en el nodo de Hola que no se reduce de tooservice paquetes que se implementen en hello mismo nodo. Algunos ejemplos son errores cuando no se puede descargar el paquete de aplicación en ese nodo y problemas de configuración de entidades de seguridad de la aplicación en el nodo de Hola. aplicación Hello implementado se identifica mediante el nombre de la aplicación (URI) y el nombre de nodo (cadena).
* **DeployedServicePackage**. Representa el estado de saludo de un paquete de servicio que se ejecuta en un nodo de clúster de Hola. Describe paquete de servicio de tooa específico de condiciones que no afectan a Hola otros paquetes de servicio en hello mismo nodo de hello misma aplicación. Algunos ejemplos son un paquete de código en el paquete de servicio de Hola que no se puede iniciar y un paquete de configuración que no se puede leer. paquete de servicio de Hello implementado se identifica por el nombre de la aplicación (URI), el nombre de nodo (cadena), nombre de manifiesto de servicio (cadena) e Id. de activación de paquete de servicio (cadena).

granularidad de Hola de modelo de estado de hello resulta fácil toodetect y solucionar problemas. Por ejemplo, si un servicio no responde, es posible tooreport que Hola la instancia de la aplicación está en mal estado. Informes en que nivel no es lo ideal, sin embargo, porque problema Hola podría no afectar a todos los servicios de hello dentro de esa aplicación. informe de Hello debería estar servicio toohello aplicados en mal estado o una partición de tooa secundarios específicos, si toothat partición de puntos de obtener más información. Hola datos automáticamente superficies a través de la jerarquía de hello y una partición incorrecto se hacen visibles en los niveles de servicio y de aplicación. Esta agregación ayuda a toopinpoint y resolver la causa de hello del problema de hello más rápidamente.

jerarquía de estado de Hola se compone de las relaciones de elementos primarios y secundarios. Los clústeres se componen de nodos y aplicaciones. Las aplicaciones tienen servicios y aplicaciones implementadas. Las aplicaciones implementadas han implementado paquetes de servicio. Los servicios tienen particiones y cada partición tiene una o más réplicas. Hay una relación especial entre los nodos y las entidades implementadas. Un nodo incorrecto devuelto por su componente de sistema de autoridad, Hola Failover Manager service afecta a Hola implementar aplicaciones, paquetes de servicios y réplicas implementadas en él.

jerarquía de estado de Hello representa el estado más reciente de hello del sistema Hola basándose en los informes de estado más recientes de hello, que es información casi en tiempo real.
Hola mismas entidades basadas en lógica específica de la aplicación o condiciones que se supervisan personalizadas pueden notificar watchdogs internos y externos. Informes de usuario coexistan con hello informes del sistema.

Planee tooinvest en cuanto a cómo diseñar toohealth tooreport y que responden durante el saludo de un servicio de nube de gran tamaño. Este servicio inicial hace toodebug más fácil de servicio de hello, supervisar y poner en funcionamiento.

## <a name="health-states"></a>Estados de mantenimiento
Service Fabric utiliza tres toodescribe de Estados de mantenimiento si una entidad es correcto o no: correcto, advertencia y error. Cualquier informe envía el almacén de estado de toohello debe especificar uno de estos Estados. resultado de evaluación de mantenimiento de Hello es uno de estos Estados.

Hola posible [Estados de mantenimiento](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthstate) son:

* **OK**(Correcto). entidad de Hello es correcto. No hay ningún problema conocido notificado en ella o en sus elementos secundarios (en los casos aplicables).
* **Warning**(Advertencia). entidad de Hello tiene algunos problemas, pero todavía puede funcionar correctamente. Por ejemplo, hay retrasos, pero todavía no causan problemas funcionales. En algunos casos, condición de advertencia de hello puede corregir sin intervención externa. En estas ocasiones, los informes de mantenimiento aumentan el conocimiento y proporcionan visibilidad sobre lo que está sucediendo. En otros casos, puede degradar la condición de advertencia de Hola en un problema grave sin intervención del usuario.
* **Error**. entidad de Hello está en mal estado. Deben adoptarse medidas toofix estado de Hola de entidad de hello, ya que no puede funcionar correctamente.
* **Unknown**(Desconocido). entidad de Hello no existe en el almacén de estado de Hola. Este resultado se puede obtener de las consultas de hello distribuida que combinación los resultados de varios componentes. Por ejemplo, consulta de lista de nodo de hello get va demasiado**FailoverManager**, **ClusterManager**, y **HealthManager**; obtener aplicación de consulta de lista se queda demasiado **ClusterManager** y **HealthManager**. Estas consultas combinan los resultados de varios componentes del sistema. Si otro componente del sistema devuelve una entidad que no está presente en health store, hello resultado combinado tiene desconocido estado de mantenimiento. Una entidad no está en almacén porque aún no se han procesado informes de mantenimiento o entidad Hola limpia después de su eliminación.

## <a name="health-policies"></a>Directivas de mantenimiento
almacén de estado de Hello aplica toodetermine de directivas de mantenimiento si una entidad es correcto en función de sus informes y sus elementos secundarios.

> [!NOTE]
> Las directivas de mantenimiento se pueden especificar en el manifiesto de clúster de hello (para la evaluación de mantenimiento de clúster y el nodo) o en el manifiesto de aplicación Hola (para evaluación de la aplicación y cualquiera de sus elementos secundarios). Las solicitudes de evaluación del estado también pueden pasar directivas de evaluación de estado personalizadas, que solo se usan para esa evaluación.
> 
> 

De forma predeterminada, Service Fabric aplica reglas estrictas (todo lo que debe ser correcto) para la relación jerárquica de elementos primarios y secundarios de Hola. Si tan solo uno de los elementos secundarios de hello tiene un evento incorrecto, primario Hola se considera incorrecto.

### <a name="cluster-health-policy"></a>Directiva de mantenimiento de clúster
Hola [directiva de mantenimiento de clúster](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy) es tooevaluate usa el estado del clúster Hola Estados de mantenimiento de estado y el nodo. Hola directiva puede definirse en el manifiesto de clúster de Hola. Si no está presente, se utiliza la directiva predeterminada de hello (cero errores permitidos).
Directiva de mantenimiento de clúster de Hello contiene:

* [ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.considerwarningaserror). Especifica si el estado de advertencia tootreat notifica como errores durante la evaluación de mantenimiento. Valor predeterminado: false.
* [MaxPercentUnhealthyApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthyapplications). Especifica el porcentaje máximo de permitido Hola de aplicaciones que pueden estar mal estado antes de clúster Hola se considera en error.
* [MaxPercentUnhealthyNodes](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthynodes). Especifica el porcentaje permitido máximo de Hola de nodos que pueden estar mal estado antes de que se considere clúster Hola error. En los clústeres de gran tamaño, algunos nodos son siempre hacia abajo o out para realizar reparaciones, por lo que este porcentaje debe ser tootolerate configurado que.
* [ApplicationTypeHealthPolicyMap](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.applicationtypehealthpolicymap). asignación de directiva de mantenimiento de tipo de aplicación de Hello puede usarse durante tipos especiales de aplicación de clúster mantenimiento evaluación toodescribe. De forma predeterminada, todas las aplicaciones se colocan en un grupo y se evalúan con MaxPercentUnhealthyApplications. Si algunos tipos de aplicaciones deben tratarse de manera diferente, puede sacarse de grupo global de Hola. En su lugar, se evalúan en porcentajes de hello asociados con su nombre de tipo de aplicación en el mapa de Hola. Por ejemplo, en un clúster hay miles de aplicaciones de distintos tipos y algunas instancias de la aplicación de control de un tipo especial de aplicación. aplicaciones de control de Hello nunca deben estar en error. Puede especificar global MaxPercentUnhealthyApplications too20% tootolerate algunos errores, pero para hello tipo de aplicación "ControlApplicationType" hello MaxPercentUnhealthyApplications too0. De esta forma, si algunas de hello muchas aplicaciones tienen un estado incorrecto, pero por debajo del porcentaje de mal estado global de hello, sería clúster Hola evalúa tooWarning. Un estado de advertencia no afecta a la actualización del clúster ni a ninguna supervisión desencadenada por el estado de mantenimiento de Error. Pero incluso un control aplicación error hará clúster incorrecto, lo que desencadena la reversión o se detiene la actualización de los clústeres de hello, dependiendo de la configuración de la actualización de Hola.
  Para los tipos de aplicación de hello definidos en mapa de hello, todas las instancias de la aplicación se realizan fuera del grupo global de Hola de aplicaciones. Se evalúan según el número total de Hola de aplicaciones del tipo de aplicación Hola, con hello MaxPercentUnhealthyApplications específicos de Hola se asigna. Resto de Hola de aplicaciones de hello permanecen en el grupo global de Hola y se evalúan con MaxPercentUnhealthyApplications.

Hola siguiente ejemplo es un extracto de un manifiesto de clúster. toodefine entradas de asignación de tipos de aplicación Hola, nombre de parámetro de prefijo Hola con"ApplicationTypeMaxPercentUnhealthyApplications", seguido por el nombre del tipo de aplicación Hola.

```xml
<FabricSettings>
  <Section Name="HealthManager/ClusterHealthPolicy">
    <Parameter Name="ConsiderWarningAsError" Value="False" />
    <Parameter Name="MaxPercentUnhealthyApplications" Value="20" />
    <Parameter Name="MaxPercentUnhealthyNodes" Value="20" />
    <Parameter Name="ApplicationTypeMaxPercentUnhealthyApplications-ControlApplicationType" Value="0" />
  </Section>
</FabricSettings>
```

### <a name="application-health-policy"></a>Directiva de mantenimiento de aplicación
Hola [directiva de mantenimiento de la aplicación](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy) describe cómo se realiza la evaluación de Hola de agregación de eventos y estados secundarios para las aplicaciones y sus elementos secundarios. Se puede definir en el manifiesto de aplicación Hola **ApplicationManifest.xml**, en el paquete de aplicación Hola. Si no se especifica ninguna directiva, Service Fabric se da por supuesto que la entidad de hello es incorrecto si tiene un informe de mantenimiento o un elemento secundario en el estado de mantenimiento de advertencia o error Hola.
Puede configurar directivas de Hello son:

* [ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.considerwarningaserror.aspx). Especifica si el estado de advertencia tootreat notifica como errores durante la evaluación de mantenimiento. Valor predeterminado: false.
* [MaxPercentUnhealthyDeployedApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.maxpercentunhealthydeployedapplications). Especifica el porcentaje de hello máximo tolerado de aplicaciones implementadas que puede ser incorrecto antes de que se considera la aplicación hello en error. Este porcentaje se calcula dividiendo el número de Hola de aplicaciones implementadas en mal estado número Hola de nodos que las aplicaciones de hello tiene actualmente implementadas en clústeres de Hola. cálculo de Hola redondea tootolerate un error en un número reducido de nodos. Porcentaje de predeterminado: cero.
* [DefaultServiceTypeHealthPolicy](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.defaultservicetypehealthpolicy). Especifica Hola directiva predeterminada del servicio tipo mantenimiento, que reemplaza la directiva de mantenimiento de hello predeterminada para todos los tipos de servicio en la aplicación hello.
* [ServiceTypeHealthPolicyMap](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.servicetypehealthpolicymap). Proporciona un mapa de las directivas de mantenimiento de servicios por tipo de servicio. Estas directivas reemplazar directivas de mantenimiento de tipo de servicio de hello predeterminado para cada tipo de servicio especificado. Por ejemplo, si una aplicación tiene un tipo de servicio de estado de la puerta de enlace y un tipo de servicio de motor con estado, puede configurar las directivas de mantenimiento de Hola la evaluación de manera diferente. Cuando se especifica la directiva al tipo de servicio, puede obtener un control más detallado del estado de Hola de servicio de Hola.

### <a name="service-type-health-policy"></a>Directiva de mantenimiento de tipo de servicio
Hola [directiva de mantenimiento del tipo de servicio](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy) especifica cómo tooevaluate y agregado Hola servicios y Hola elementos secundarios de servicios. Directiva de Hello contiene:

* [MaxPercentUnhealthyPartitionsPerService](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthypartitionsperservice). Especifica el porcentaje de hello máximo tolerado de particiones en mal estado antes de que un servicio se considera incorrecto. Porcentaje de predeterminado: cero.
* [MaxPercentUnhealthyReplicasPerPartition](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyreplicasperpartition). Especifica el porcentaje de hello máximo tolerado de réplicas en mal estado antes de que una partición se considera incorrecto. Porcentaje de predeterminado: cero.
* [MaxPercentUnhealthyServices](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyservices). Especifica el porcentaje de hello máximo tolerado de servicios en mal estado antes de aplicación hello se considera incorrecto. Porcentaje de predeterminado: cero.

Hola siguiente ejemplo es un extracto de un manifiesto de aplicación:

```xml
    <Policies>
        <HealthPolicy ConsiderWarningAsError="true" MaxPercentUnhealthyDeployedApplications="20">
            <DefaultServiceTypeHealthPolicy
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="10"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="FrontEndServiceType"
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="20"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="BackEndServiceType"
                   MaxPercentUnhealthyServices="20"
                   MaxPercentUnhealthyPartitionsPerService="0"
                   MaxPercentUnhealthyReplicasPerPartition="0">
            </ServiceTypeHealthPolicy>
        </HealthPolicy>
    </Policies>
```

## <a name="health-evaluation"></a>Evaluación de estado
Los usuarios y servicios automatizados pueden evaluar el mantenimiento de cualquier entidad en cualquier momento. tooevaluate estado de una entidad, agregados de almacén de estado de hello todos los Estados informa de una entidad de Hola y se evalúa como todos sus nodos secundarios (si procede). algoritmo de agregación de mantenimiento de Hello usa las directivas de mantenimiento que especifican cómo informes de mantenimiento del tooevaluate y cómo Estados de mantenimiento de secundarios de tooaggregate (si procede).

### <a name="health-report-aggregation"></a>Agregación de informes de mantenimiento
Una entidad puede tener varios informes de mantenimiento enviados por informadores diferentes (componentes del sistema o guardianes) en diferentes propiedades. Hola agregación utiliza hello las directivas de mantenimiento asociados, en particular Hola a ConsiderWarningAsError miembro de la aplicación o directiva de mantenimiento del clúster. ConsiderWarningAsError especifica cómo tooevaluate advertencias.

Hello estado agregado desencadena hello *peor* informes de mantenimiento de una entidad de Hola. Si hay informes de estado de al menos un error, hello estado agregado es un error.

![Agregación de informe de mantenimiento a informe de errores.][2]

Una entidad de mantenimiento con uno o más informes de mantenimiento de error se evalúa como Error. Hello mismo puede decirse de un informe de estado caducados, independientemente de su estado de mantenimiento.

[2]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-error.png

Si no hay ningún informe de error y una o varias advertencias, hello estado agregado es advertencia o error, dependiendo de la marca de hello ConsiderWarningAsError directiva.

![Agregación de informe de mantenimiento a informe de advertencias y ConsiderWarningAsError establecido en false.][3]

Agregación de informe de mantenimiento con los informes de advertencia y ConsiderWarningAsError establece toofalse (valor predeterminado).

[3]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-warning.png

### <a name="child-health-aggregation"></a>Agregación de mantenimiento de elementos secundarios
Hello estado agregado de una entidad refleja Estados de mantenimiento de hello secundario (si procede). algoritmo de Hola para agregar estados de mantenimiento de secundarios utiliza hello las directivas de mantenimiento aplicables en función del tipo de entidad de Hola.

![Agregación de mantenimiento de entidades secundarias.][4]

Agregación de elementos secundarios basada en directivas de mantenimiento.

[4]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy-eval.png

Después de almacén de estado de hello ha evaluado a todos los elementos secundarios de hello, agrega sus Estados de mantenimiento en función de hello configura el porcentaje máximo de elementos secundarios incorrecto. Este porcentaje se toma de directiva de hello en función de tipo de entidad y secundarios de Hola.

* Si todos los elementos secundarios tienen estados Aceptar, Hola secundarios agregados el estado es correcto.
* Si los niños tienen Aceptar y Estados de advertencia, estado de mantenimiento de hello agregados secundarios es una advertencia.
* Si hay elementos secundarios con los Estados de error que no se respetan el máximo de hello porcentaje permitido de elementos secundarios incorrecto, hello estado agregado es un error.
* Si los elementos secundarios de hello con hello de respecto de los Estados de error máximo porcentaje permitido de elementos secundarios incorrecto, Hola le avisa de estado de mantenimiento agregado.

## <a name="health-reporting"></a>Informes de mantenimiento
Tanto los componentes del sistema como los guardianes internos o externos pueden generar informes de las entidades de Service Fabric. Asegúrese de Informadores de Hello *local* determinaciones de mantenimiento de Hola de entidades de hello supervisado, según las condiciones de saludo está supervisando. No deben toolook en cualquier estado global o agregar datos. Hola deseado quedará toohave simple Informadores y organismos no complejos que necesitan toolook en tooinfer de muchas cosas qué toosend de información.

almacén de estado del toohello toosend de datos de estado, un indicador de entidad de hello afectado tooidentify es necesario y crear un informe de mantenimiento. informe de hello toosend, use hello [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth) API, informe de mantenimiento de las API expuestas en hello `Partition` o `CodePackageActivationContext` objetos, cmdlets de PowerShell o REST.

### <a name="health-reports"></a>Informes de mantenimiento
Hola [informes de mantenimiento](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthreport) para cada una de las entidades de hello en clúster de hello contienen Hola siguiente información:

* **SourceId**. Cadena que identifica de forma única Informador de Hola de evento de estado de Hola.
* **Identificador de entidad**. Identifica la entidad de Hola donde se aplica el informe de Hola. Difiere en función de hello [tipo de entidad](service-fabric-health-introduction.md#health-entities-and-hierarchy):
  
  * Clúster. Ninguno.
  * Nodo. Nombre de nodo (cadena).
  * Aplicación. Nombre de aplicación (identificador URI). Representa el nombre de Hola de instancia de la aplicación hello implementado en clúster de Hola.
  * Servicio. Nombre de servicio (identificador URI). Representa el nombre de Hola de instancia de servicio de hello implementado en clúster de Hola.
  * Partición. Identificador de partición (GUID). Representa el identificador único de partición de Hola.
  * Réplica. Id. de réplica de servicio con estado de Hola o Id. de instancia de servicio sin estado de hello (INT64).
  * DeployedApplication. Nombre de aplicación (identificador URI) y nombre de nodo (cadena).
  * DeployedServicePackage. Nombre de aplicación (identificador URI), nombre de nodo (cadena) y nombre de manifiesto de servicio (cadena).
* **Propiedad**. A *cadena* (no una enumeración fija) que permite que el indicador de hello toocategorize Hola estado eventos para una propiedad específica de la entidad de Hola. Por ejemplo, un indicador puede enviar informes de mantenimiento de Hola de propiedad de "Almacenamiento" hello Node01 e indicador B puede enviar informes de estado de Hola de propiedad de "Conectividad" hello Node01. En el almacén de estado de hello, estos informes se tratan como eventos de mantenimiento independiente de hello Node01 entidad.
* **Descripción**. Una cadena que permite un tooprovide Informador información detallada sobre eventos de estado de Hola. **SourceId**, **propiedad**, y **HealthState** debe describir completamente informe de Hola. Descripción de Hello agrega información legible sobre informes de Hola. texto Hello facilita a los administradores y usuarios informe de mantenimiento de hello toounderstand.
* **HealthState**. Un [enumeración](service-fabric-health-introduction.md#health-states) que describe el estado de mantenimiento de Hola de informe de Hola. Hola valores aceptados son Aceptar, advertencia y Error.
* **TimeToLive**. Un intervalo de tiempo que indica cuánto tiempo informe de mantenimiento de hello es válido. Junto con **RemoveWhenExpired**, permite saber cómo tooevaluate expirado eventos de almacén de estado de Hola. De forma predeterminada, el valor de hello es infinito y, informe hello es válido para siempre.
* **RemoveWhenExpired**. Un valor booleano. Si establece tootrue, Hola mantenimiento expirada informe automáticamente se quita del almacén de estado de Hola e informe hello no afecta a la evaluación de mantenimiento de entidad. Utiliza al informe hello es válida durante un período especificado de tiempo solo e Informador de hello no necesita tooexplicitly vaciarla si. También ha utilizado toodelete informes de almacén de estado de hello (por ejemplo, un guardián se cambia y deja de enviar informes con origen anterior y la propiedad). Puede enviar un informe con un breve TimeToLive junto con RemoveWhenExpired tooclear hasta cualquier estado anterior del almacén de estado de Hola. Si el valor de Hola se establece toofalse, hello informe han expirado se trata como un error en la evaluación de mantenimiento de Hola. valor false Hola señales de almacén de estado de toohello que ese origen Hola debería notificar periódicamente en esta propiedad. Si no es así, a continuación, debe haber algún problema con guardián Hola. estado del guardián Hola se captura teniendo en cuenta los eventos de Hola como un error.
* **SequenceNumber**. Un entero positivo que necesita toobe creciente, representa el orden de Hola de hello informes. Se utiliza por hello almacén toodetect obsoletos informes de mantenimiento que se reciben en tiempo de ejecución debido a retrasos en la red u otros problemas. Un informe se rechaza si el número de secuencia de hello es menor o igual número toohello aplicado más recientemente para Hola misma entidad, origen y propiedad. Si no se especifica, se genera automáticamente el número de secuencia de Hola. Es necesario tooput en número de secuencia de hello solo cuando se notifican en las transiciones de estado. En esta situación, el origen de hello debe tooremember qué informes se envían y mantener la información de hello para la recuperación de conmutación por error.

Estos cuatro datos (SourceId, entity identifier, Property y HealthState) se requieren en todos los informes de mantenimiento. Hola SourceId cadena no se permite toostart con prefijo Hola "**System.**", que está reservado para los informes del sistema. Para hello misma entidad, hay solo un informe para hello mismo origen y propiedad. Varios informes de Hola mismo origen y de reemplazo de propiedad entre sí en hello mantenimiento del lado cliente (si se procesan por lotes) o en el lado de almacén de estado de Hola. reemplazo de Hola se basa en los números de secuencia; los informes más recientes (con números de secuencia más altos) reemplazan informes anteriores.

### <a name="health-events"></a>Eventos de estado
Internamente, el almacén de estado de hello mantiene [eventos de estado](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthevent), que contiene toda la información de Hola de los informes de Hola y metadatos adicionales. metadatos de Hello incluyen el tiempo de hello informe Hola facilitó a toohello cliente de estado y tiempo Hola que se modificó en el lado del servidor de Hola. devuelven los eventos de estado de Hello [consultas de estado](service-fabric-view-entities-aggregated-health.md#health-queries).

Hello metadatos agregada contienen:

* **SourceUtcTimestamp**. informe Hola Hola se asignó el cliente de estado de toohello (hora de Universal coordinada).
* **LastModifiedUtcTimestamp**. informe de Hola Hola se modificó por última vez en el lado del servidor de hello (hora de Universal coordinada).
* **IsExpired**. Un indicador tooindicate si informe Hola ha expirado cuando Hola se ha ejecutado por el almacén de estado de Hola. Un evento ha expirado solo si RemoveWhenExpired está establecido en false. En caso contrario, el evento de hello no devuelto por la consulta y se quita del almacén de Hola.
* **LastOkTransitionAt**, **LastWarningTransitionAt**, **LastErrorTransitionAt**. Hola última hora de las transiciones de Aceptar, advertencia o error. Estos campos proporcionan historial Hola de transiciones de estado de mantenimiento de Hola para eventos de Hola.

campos de transición de estado de Hola se pueden usar para las alertas más inteligentes o información de eventos de estado "historial". Habilitan escenarios como:

* Alertar cuando una propiedad ha estado en los estados Advertencia o Error durante más de X minutos. Comprobación de condición de Hola durante un período de tiempo evita las alertas en condiciones temporales. Por ejemplo, se puede traducir una alerta si se ha advertencia de estado de mantenimiento de Hola durante más de cinco minutos en (estado == advertencia y ahora - LastWarningTransitionTime > 5 minutos).
* Alerta sólo en las condiciones que han cambiado en hello última X minutos. Si un informe ya estaba error antes de hello especificado de tiempo, se puede omitir porque ya se indicó anteriormente.
* Si una propiedad alterna entre Advertencia y Error, determine cuánto tiempo ha sido incorrecta (es decir, que no ha sido correcta). Por ejemplo, se puede traducir una alerta si la propiedad de hello no ha sido correcto durante más de cinco minutos en (HealthState! = Aceptar y ahora - LastOkTransitionTime > 5 minutos).

## <a name="example-report-and-evaluate-application-health"></a>Ejemplo: informar y evaluar el mantenimiento de una aplicación
Hello en el ejemplo siguiente se envía un informe de mantenimiento a través de PowerShell en la aplicación hello **fabric: / WordCount** de origen de hello **MyWatchdog**. informe de mantenimiento de Hello contiene información sobre la propiedad de estado de Hola "disponibilidad" en un estado de error, con TimeToLive infinito. A continuación, consulta el estado de aplicación hello, que devuelve agrega hello y errores de estado de mantenimiento notificado eventos de estado de lista de Hola de eventos de estado.

```powershell
PS C:\> Send-ServiceFabricApplicationHealthReport –ApplicationName fabric:/WordCount –SourceId "MyWatchdog" –HealthProperty "Availability" –HealthState Error

PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            :
                                  Error event: SourceId='MyWatchdog', Property='Availability'.

ServiceHealthStates             :
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error

                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok

DeployedApplicationHealthStates :
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok

HealthEvents                    :
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 360
                                  SentAt                : 3/22/2016 7:56:53 PM
                                  ReceivedAt            : 3/22/2016 7:56:53 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 3/22/2016 7:56:53 PM, LastWarning = 1/1/0001 12:00:00 AM

                                  SourceId              : MyWatchdog
                                  Property              : Availability
                                  HealthState           : Error
                                  SequenceNumber        : 131032204762818013
                                  SentAt                : 3/23/2016 3:27:56 PM
                                  ReceivedAt            : 3/23/2016 3:27:56 PM
                                  TTL                   : Infinite
                                  Description           :
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Ok->Error = 3/23/2016 3:27:56 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="health-model-usage"></a>Uso del modelo de estado
modelo de estado de Hello permite servicios en la nube y tooscale de plataforma de Service Fabric subyacente hello, porque la determinación de la supervisión y mantenimiento se distribuye entre los distintos monitores de hello en clúster de Hola.
Otros sistemas tienen un servicio único y centralizado en nivel de clúster de Hola que analiza todos los hello *potencialmente* emitido por servicios de información útil. Este enfoque dificulta su escalabilidad. Lo también no les permite obtener información específica de toocollect toohelp identificar problemas y posibles problemas como causa del cierre toohello como sea posible.

modelo de estado de Hola se utiliza con un alto grado de supervisión y diagnóstico, para evaluar el estado del clúster y la aplicación y para las actualizaciones supervisadas. Otros servicios usar mantenimiento tooperform de datos automática repara, generación el historial de mantenimiento del clúster y emiten alertas en determinadas condiciones.

## <a name="next-steps"></a>Pasos siguientes
[Vista de los informes de estado de Service Fabric](service-fabric-view-entities-aggregated-health.md)

[Uso de informes de mantenimiento del sistema para solucionar problemas](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[¿Cómo tooreport y comprobación de estado de servicio](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Incorporación de informes de mantenimiento de Service Fabric personalizados](service-fabric-report-health.md)

[Supervisión y diagnóstico de los servicios localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Actualización de la aplicación de Service Fabric](service-fabric-application-upgrade.md)

