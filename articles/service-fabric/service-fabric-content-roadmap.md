---
title: "más información sobre Azure Service Fabric aaaLearn | Documentos de Microsoft"
description: "Obtenga información acerca de los conceptos básicos de Hola y áreas principales de Azure Service Fabric. Proporciona información general de Service Fabric extendida y cómo toocreate microservicios."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/14/2017
ms.author: ryanwi
ms.openlocfilehash: 7fe8de777755be11635912613bb5b970e3fe3ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="so-you-want-toolearn-about-service-fabric"></a>¿Por lo que desee toolearn acerca de Service Fabric?
Azure Service Fabric es una plataforma de sistemas distribuidos que resulta fácil toopackage, implementar y administrar microservicios escalables y confiables.  Sin embargo, Service Fabric tiene un área de superficie grande, y hay mucho toolearn.  En este artículo se proporciona una sinopsis de Service Fabric y describe los conceptos básicos de hello, modelos de ciclo de vida de aplicación, pruebas, clústeres y la supervisión de estado de la programación. Hola de lectura [Introducción](service-fabric-overview.md) y [¿qué microservicios?](service-fabric-overview-microservices.md) para una introducción y cómo se Service Fabric pueden microservicios toocreate usado. En este artículo no contiene una lista completa de contenido, pero vincular toooverview y obtener artículos iniciadas para todas las áreas de Service Fabric. 

## <a name="core-concepts"></a>Conceptos principales
[Terminología de Service Fabric](service-fabric-technical-overview.md), [modelo de aplicación](service-fabric-application-model.md), y [admite modelos de programación](service-fabric-choose-framework.md) proporcionar varios conceptos y descripciones, pero aquí son conceptos básicos de Hola.

<table><tr><th>Conceptos principales</th><th>Tiempo de diseño</th><th>Tiempo de ejecución</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/CoreConceptsVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965"><img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">
<img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td></tr>
</table>

### <a name="design-time-application-type-service-type-application-package-and-manifest-service-package-and-manifest"></a>Tiempo de diseño: tipo de aplicación, tipo de servicio, paquete de aplicación y manifiesto de aplicación, paquete y manifiesto de servicio
Un tipo de aplicación es nombre/versión de Hola asignada tooa colección de tipos de servicio. Esto se define en un archivo *ApplicationManifest.xml*, que se inserta en un directorio del paquete de aplicación. Hello paquete de aplicación es, a continuación, copian almacén de imágenes del clúster de toohello Service Fabric. A continuación, puede crear una aplicación con nombre de este tipo de aplicación, que, a continuación, se ejecuta en el clúster de Hola. 

Un tipo de servicio es Hola nombre/versión asignados a los paquetes de código del servicio de tooa, paquetes de datos y paquetes de configuración. Esto se define en un archivo ServiceManifest.xml, que se inserta en un directorio del paquete de servicio. Hello directorio del paquete de servicio, a continuación, hace referencia a un paquete de aplicación *ApplicationManifest.xml* archivo. En el clúster de hello, después de crear una aplicación con nombre, puede crear un servicio con nombre desde uno de hello tipos de servicio del tipo de aplicación. Un tipo de servicio se describe en su archivo *ServiceManifest.xml*. tipo de servicio de Hola se compone de valores de la configuración del servicio de código ejecutable que se cargan en tiempo de ejecución, y datos estáticos, que es utilizados por el servicio de Hola.

![Tipos de aplicaciones de Service Fabric y tipos de servicio][cluster-imagestore-apptypes]

paquete de aplicación Hello es un directorio de disco que contiene el tipo de aplicación Hola *ApplicationManifest.xml* archivo, que hace referencia a los paquetes de servicios de Hola para cada tipo de servicio que conforma el tipo de aplicación Hola. Por ejemplo, un paquete de aplicación para un tipo de aplicaciones de correo electrónico podría contener paquete del servicio de cola de referencias tooa, un paquete de servicios de front-end y un paquete de servicios de base de datos. archivos de Hello en el directorio del paquete de aplicación Hola son almacén de imágenes del clúster de Service Fabric toohello copiada. 

Un paquete de servicio es un directorio de disco que contenga del tipo de servicio de hello *ServiceManifest.xml* archivo, que hace referencia a código de hello, datos estáticos y paquetes de configuración para el tipo de servicio de Hola. del tipo de aplicación Hola hace referencia a los archivos de Hello en el directorio del paquete de servicio de hello *ApplicationManifest.xml* archivo. Por ejemplo, un paquete de servicio podría hacer referencia a código de toohello, los datos estáticos y los paquetes de configuración que componen un servicio de base de datos.

### <a name="run-time-clusters-and-nodes-named-applications-named-services-partitions-and-replicas"></a>Tiempo de ejecución: clústeres y nodos, aplicaciones con nombre, servicios con nombre, particiones y réplicas
Un [clúster de Service Fabric](service-fabric-deploy-anywhere.md) es un conjunto de máquinas físicas o virtuales conectadas a la red, en las que se implementan y administran los microservicios. Clústeres pueden escalar toothousands de máquinas.

Cada una de las máquinas físicas o virtuales que forman parte de un clúster se denominan nodo. A cada nodo se le asigna un nombre de nodo (una cadena). Los nodos tienen características como las propiedades de colocación. Cada máquina física o virtual tiene un servicio de Windows de inicio automático, `FabricHost.exe`, que empieza a ejecutarse en el arranque y luego inicia dos ejecutables: `Fabric.exe` y `FabricGateway.exe`. Estos dos ejecutables constituyen nodo Hola. En los escenarios de prueba o desarrollo, se pueden hospedar varios nodos en un solo equipo o máquina virtual mediante la ejecución de varias instancias de `Fabric.exe` y `FabricGateway.exe`.

Una aplicación con nombre es una colección de servicios con nombre que realizan una o varias funciones determinadas. Un servicio realiza una función completa e independiente (puede iniciarse y ejecutarse independientemente de otros servicios) y se compone de código, configuración y datos. Después de un paquete de aplicación es el almacén de imágenes de toohello copiado, cree una instancia de la aplicación hello en clúster de hello mediante la especificación de tipo de aplicación del paquete de aplicación Hola (mediante su nombre/versión). A cada instancia del tipo de aplicación se le asigna un nombre de identificador URI similar a *fabric:/MyNamedApp*. En un clúster se pueden crear varias aplicaciones con nombre de un único tipo de aplicación. También se pueden crear aplicaciones con nombre de diferentes tipos de aplicación. Cada aplicación con nombre se administra de manera independiente y tiene versiones independientes.

Después de crear una aplicación con nombre, puede crear una instancia de uno de sus tipos de servicio (un servicio con nombre) en clúster de hello mediante la especificación de tipo de servicio de hello (mediante su nombre/versión). A cada instancia del tipo de servicio se le asigna un nombre de URI cuyo ámbito es el URI de su aplicación con nombre. Por ejemplo, si crea un servicio dentro de una aplicación con el nombre "MyNamedApp" con el nombre "MyDatabase", Hola URI el siguiente aspecto: *fabric: / MyNamedApp/MyDatabase*. En una aplicación con nombre, puede crear uno o varios servicios con nombre. Todos los servicios con nombre pueden tener su propio esquema de partición y cuentas de instancia o réplica. 

Hay dos tipos de servicios: con y sin estado. Los servicios sin estado pueden almacenar el estado persistente en un servicio de almacenamiento externo como Azure Storage, Azure SQL Database o Azure Cosmos DB. Usar un servicio sin estado al servicio de hello no tiene ningún almacenamiento persistente. Un servicio con estado usa Service Fabric toomanage el estado de su servicio a través de sus colecciones confiable o Reliable Actors modelos de programación. 

Al crear un servicio con nombre, especifique un esquema de partición. Los servicios con grandes cantidades de estado de dividen los datos de hello en particiones. Cada partición es responsable de una parte de todo el estado del servicio de hello, que se reparte entre los nodos del clúster de Hola Hola. Dentro de una partición, los servicios con nombre sin estado tienen instancias, mientras que los servicios con nombre con estado tienen réplicas. Normalmente, los servicios con nombre sin estado solo tienen una partición, ya que no tienen un estado interno. Los servicios con nombre con estado mantienen su estado dentro de las réplicas y cada partición tiene su propio conjunto de réplicas. Operaciones de lectura y escritura se realizan en una réplica (llamada hello principal). Toostate de cambios de operaciones de escritura replica toomultiple otras réplicas (denominados secundarias activas). 

Hello siguiente diagrama muestra hello relación entre las aplicaciones y las instancias de servicio, particiones y réplicas.

![Particiones y réplicas dentro de un servicio][cluster-application-instances]

### <a name="partitioning-scaling-and-availability"></a>Creación de particiones, escalado y disponibilidad
[Creación de particiones](service-fabric-concepts-partitioning.md) no es único tooService tejido. Una forma conocida de partición es la partición de datos o particionamiento. Los servicios con estado con grandes cantidades de estado de dividen los datos de hello en particiones. Cada partición es responsable de una parte de todo el estado del servicio de Hola Hola. 

réplicas de Hola de cada partición se reparten entre los nodos del clúster de hello, que permite a estado de su servicio con nombre demasiado[escala](service-fabric-concepts-scalability.md). Como datos de hello crezca, particiones crecen y Service Fabric vuelve a equilibrar las particiones a través del uso eficaz de toomake de nodos de los recursos de hardware. Si agrega el nuevo clúster de nodos toohello, Service Fabric se reequilibrar réplicas de la partición de hello en hello mayor número de nodos. Mejora el rendimiento de la aplicación global y reduce la contención de toomemory de acceso. Si no se utilizan eficazmente nodos hello en clúster de hello, puede reducir número Hola de nodos de clúster de Hola. Service Fabric vuelve a volver a equilibrar réplicas de la partición de hello en hello reducido número de nodos toomake mejorar el uso de hardware de hello en cada nodo.

Dentro de una partición, los servicios con nombre sin estado tienen instancias, mientras que los servicios con nombre con estado tienen réplicas. Normalmente, los servicios con nombre sin estado solo tienen una partición, ya que no tienen un estado interno. proporcionan instancias de la partición de Hola para [disponibilidad](service-fabric-availability-services.md). Si se produce un error en una instancia, otras instancias continúan toooperate normalmente y, a continuación, Service Fabric crea una nueva instancia. Los servicios con nombre con estado mantienen su estado dentro de las réplicas y cada partición tiene su propio conjunto de réplicas. Operaciones de lectura y escritura se realizan en una réplica (llamada hello principal). Toostate de cambios de operaciones de escritura replica toomultiple otras réplicas (denominados secundarias activas). Si falla una réplica, Service Fabric genera una nueva réplica de réplicas de hello existentes.

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Microservicios de Service Fabric con estado y sin estado
Service Fabric también permite que las aplicaciones de toobuild que constan de microservicios o contenedores. Microservicios sin estado (por ejemplo, las puertas de enlace de protocolo y servidores proxy web) no mantienen un estado mutable fuera de una solicitud y su respuesta de servicio de Hola. Los roles de trabajo de los servicios en la nube de Azure son un ejemplo de servicio sin estado. Microservicios con estado (por ejemplo, las cuentas de usuario, las bases de datos, dispositivos, compra Amazon y colas) mantienen un estado mutable, autorizado más allá de la solicitud de Hola y su respuesta. Actualmente, las aplicaciones de escala de Internet se componen de una combinación de microservicios con estado y sin estado. 

Una clave differentation con Service Fabric es la gran importancia en la creación de servicios con estado, ya sea con hello [integrada en modelos de programación ](service-fabric-choose-framework.md) o con los servicios con estado en contenedores. Hola [escenarios de aplicación](service-fabric-application-scenarios.md) describen escenarios de Hola donde se usan los servicios con estado.

¿Por qué tener microservicios con estado junto con otras sin estado? Hola dos razones principales por son:

* Puede compilar alto rendimiento, baja latencia, procesamiento tolerantes a errores de transacciones en línea (OLTP) de servicios para mantener el código y datos cerrar en Hola mismo equipo. Algunos ejemplos son interfaces de usuario interactivas, búsqueda, sistemas de Internet de las cosas (IoT), sistemas de comercialización, sistemas de detección de fraudes y procesamiento de tarjetas de crédito y, además, administración de registros personales.
* Puede simplificar el diseño de la aplicación. Con estado microservicios eliminan la necesidad de Hola de colas adicionales y las memorias caché, que normalmente son necesarios los requisitos de disponibilidad y la latencia de hello tooaddress de una aplicación puramente sin estado. Servicios con estado naturalmente son de alta disponibilidad y baja latencia, lo que reduce el número de Hola de móvil toomanage partes de la aplicación como un todo.

## <a name="supported-programming-models"></a>Modelos de programación admitidos
Service Fabric ofrece toowrite de varias maneras y administre sus servicios. Servicios pueden utilizar hello las API de tejido de servicio tootake aprovechar características y marcos de aplicaciones de la plataforma de Hola. Los servicios también pueden ser cualquier programa ejecutable compilado escrito en cualquier lenguaje y hospedado en un clúster de Service Fabric. Para más información, consulte [Modelos de programación admitidos](service-fabric-choose-framework.md).

### <a name="containers"></a>Contenedores
De forma predeterminada, Service Fabric implementa y activa estos servicios como procesos. Service Fabric puede implementar también servicios en [contenedores](service-fabric-containers-overview.md). Lo que es importante, puede mezclar los servicios de procesos y servicios en los contenedores de hello misma aplicación. Service Fabric admite la implementación de contenedores de Linux/contenedores de Windows en Windows Server 2016. Puede usar Service Fabric para implementar aplicaciones existentes y servicios con o sin estado en un contenedor. 

### <a name="reliable-services"></a>Reliable Services
[Servicios de confianza](service-fabric-reliable-services-introduction.md) es un marco de trabajo ligera para escribir servicios que se integran con la plataforma de Service Fabric hello y aprovechan el conjunto completo de Hola de características de la plataforma. Servicios de confianza pueden ser sin estado (similar toomost servicio plataformas, como servidores web o Roles de trabajo de servicios en la nube), donde se conserva el estado en una solución externa, como base de datos de Azure o almacenamiento de tabla de Azure. Servicios de confianza también pueden ser con estado, donde se conserva el estado directamente en el servicio de hello utilizando colecciones confiable. El estado cuenta con una [alta disponibilidad](service-fabric-availability-services.md) mediante la replicación y se distribuye a través de [particiones](service-fabric-concepts-partitioning.md), todo administrado automáticamente por Service Fabric.

### <a name="reliable-actors"></a>Reliable Actors
Se basa en servicios de confianza, Hola [Actor confiable](service-fabric-reliable-actors-introduction.md) framework es un marco de aplicación que implementa el patrón de Actor Virtual hello, basándose en el patrón de diseño de hello actor. marco de Actor confiable de Hello usa unidades independientes del proceso y el estado con la ejecución de un único subproceso denominada actores. Hola Actor confiable proporciona el marco de trabajo se crea en comunicación para actores y persistencia de estado establecido previamente y las configuraciones de escalado horizontal.

### <a name="aspnet-core"></a>ASP.NET Core
Service Fabric se integra con [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) como un modelo de programación de primera clase para la creación de aplicaciones API y web

### <a name="guest-executables"></a>Ejecutables de invitado
Un [ejecutable de invitado](service-fabric-deploy-existing-app.md) es un ejecutable arbitrario y existente, escrito en cualquier lenguaje, que se hospeda en un clúster de Service Fabric junto con otros servicios. Los ejecutables de invitado no se integran directamente con las API de Service Fabric. Sin embargo seguir benefician de características Hola ofertas de plataforma, como personalizada del estado y cargar informes y detectabilidad del servicio mediante una llamada a las API de REST. También tienen soporte técnico completo de ciclo de vida de aplicación. 

## <a name="application-lifecycle"></a>Ciclo de vida de aplicación
Como con otras plataformas, una aplicación de Service Fabric normalmente pasa por hello siguientes fases: diseño, desarrollo, pruebas, implementación, actualización, mantenimiento y eliminación. Service Fabric proporciona compatibilidad de primera clase para ciclo de vida completo de la aplicación hello de aplicaciones en la nube, desde el desarrollo hasta la implementación, la administración diaria y la retirada de tooeventual de mantenimiento. modelo de servicio de Hello permite varios tooparticipate diferentes roles de forma independiente en ciclo de vida de aplicación Hola. [Ciclo de vida de aplicación de Service Fabric](service-fabric-application-lifecycle.md) proporciona una introducción de las API de hello y cómo se utilizan por las distintas funciones de hello en fases de Hola de ciclo de vida de aplicación Hola Service Fabric. 

ciclo de vida de aplicación completo de Hello puede administrarse con [cmdlets de PowerShell](/powershell/module/ServiceFabric/), [API de C#](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient), [API Java](/java/api/system.fabric._application_management_client), y [API de REST](/rest/api/servicefabric/). También puede configurar canalizaciones de implementación continua e integración continua con herramientas como [Visual Studio Team Services](service-fabric-set-up-continuous-integration.md) o [Jenkins](service-fabric-cicd-your-linux-java-application-with-jenkins.md).

Hello vídeo de Microsoft Virtual Academy siguiente se describe cómo toomanage el ciclo de vida de la aplicación:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=My3Ka56yC_6106218965">
<img src="./media/service-fabric-content-roadmap/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="test-applications-and-services"></a>Prueba de aplicaciones y servicios
toocreate realmente servicios de nube escala, es fundamental tooverify que las aplicaciones y servicios pueden resistir errores reales. Hola error Analysis Services está diseñado para probar los servicios que se generan en el tejido de servicio. Con hello [servicio de análisis de errores](service-fabric-testability-overview.md), puede inducir a errores significativos y ejecutar escenarios de prueba completada en sus aplicaciones. Estos errores y escenarios de probar y validar Hola numerosos Estados y transiciones que experimentará un servicio a lo largo de su duración, en forma controlada, segura y coherente.

Las [acciones](service-fabric-testability-actions.md) están orientadas a un servicio de prueba mediante errores individuales. Un programador del servicio puede utilizar como bloques de creación toowrite complicado escenarios. Los ejemplos de errores simulados son:

* Reinicie un nodo toosimulate cualquier número de situaciones donde se reinicia una máquina o una máquina virtual.
* Mueve una réplica del equilibrio de carga de servicio con estado toosimulate, conmutación por error o actualización de la aplicación.
* Invocar la pérdida de quórum en un toocreate una situación donde las operaciones de escritura no pueden continuar porque no hay suficientes datos nuevos de tooaccept de "copia de seguridad" o "secundario" réplicas de servicio con estado.
* Invocar la pérdida de datos en un toocreate una situación donde todo el estado en memoria se borra completamente fuera de servicio con estado.

Los [escenarios](service-fabric-testability-scenarios.md) son operaciones complejas compuestas por una o varias acciones. Hola error Analysis Services proporciona dos escenarios completos integrados:

* [Escenario de caos](service-fabric-controlled-chaos.md)-simula continuados, intercalados errores (estable e incorrectas) a lo largo de clúster de Hola durante períodos ampliados de tiempo.
* [Escenario de conmutación por error](service-fabric-testability-scenarios.md#failover-test)-una versión del escenario de prueba de caos Hola destinado a una partición de servicio específico mientras no se ve afectada otros servicios.

## <a name="clusters"></a>Clústeres
Un [clúster de Service Fabric](service-fabric-deploy-anywhere.md) es un conjunto de máquinas físicas o virtuales conectadas a la red, en las que se implementan y administran los microservicios. Clústeres pueden escalar toothousands de máquinas. Una máquina física o virtual que forma parte de un clúster se denomina nodo del clúster. A cada nodo se le asigna un nombre de nodo (una cadena). Los nodos tienen características como las propiedades de colocación. Cada máquina física o virtual tiene un servicio de inicio automático, `FabricHost.exe`, que empieza a ejecutarse en el arranque y luego inicia dos ejecutables: Fabric.exe y FabricGateway.exe. Estos dos ejecutables constituyen nodo Hola. En los escenarios de prueba, se pueden hospedar varios nodos en un solo equipo y máquina virtual mediante la ejecución de varias instancias de `Fabric.exe` y `FabricGateway.exe`.

Los clústeres de Service Fabric se pueden crear en cualquier máquina virtual o física que ejecute Windows Server o Linux. Son capaz de toodeploy y ejecutar aplicaciones de Service Fabric en cualquier entorno donde haya un conjunto de equipos de Windows Server o Linux que están conectados entre sí: local, en Microsoft Azure, o de cualquier proveedor de nube.

Hello siguiente vídeo de Microsoft Virtual Academy describe Service Fabric clústeres:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/ClusterOverview.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="clusters-on-azure"></a>Clústeres en Azure
Clústeres de Service Fabric en ejecución en Azure proporciona integración con otras características de Azure y servicios, lo que facilita las operaciones y administración de clúster de Hola y más confiable. Un clúster es un recurso de Azure Resource Manager, que permite modelar clústeres como cualquier otro recurso de Azure. El Administrador de recursos también proporciona una administración sencilla de todos los recursos usados por clúster hello como una sola unidad. Los clústeres de Azure se integran con Diagnósticos de Azure y Log Analytics. Los tipos de nodo de clúster son [conjuntos de escalado de máquinas virtuales](/azure/virtual-machine-scale-sets/index), por lo que la funcionalidad de escalado automático está integrada.

Puede crear un clúster en Azure a través de hello [portal de Azure](service-fabric-cluster-creation-via-portal.md), desde un [plantilla](service-fabric-cluster-creation-via-arm.md), o de [Visual Studio](service-fabric-cluster-creation-via-visual-studio.md).

vista previa de Hola de Service Fabric en Linux permite toobuild, implementar y administrar las aplicaciones de alta disponibilidad, altamente escalables en Linux tal como haría en Windows. los marcos de trabajo de Service Fabric de Hello (servicios de confianza y actores confiable) están disponibles en Java en Linux, en suma tooC # (.NET Core). Puede compilar igualmente [servicios ejecutables invitados](service-fabric-deploy-existing-app.md) con cualquier lenguaje o marco. Además, vista previa de hello también admite la organización de los contenedores de Docker. Contenedores de docker pueden ejecutar archivos ejecutables de invitado o servicios de Service Fabric nativos, que utilizan los marcos de trabajo de Service Fabric Hola. Para más información, vea [Service Fabric en Azure](service-fabric-linux-overview.md).

Como Service Fabric en Linux es una versión preliminar, hay algunas características que se admiten en Windows pero no en Linux. más información, lea toolearn [diferencias entre Service Fabric en Linux y Windows](service-fabric-linux-windows-differences.md).

### <a name="standalone-clusters"></a>Clústeres independientes
Service Fabric proporciona un paquete de instalación para toocreate independiente Service Fabric clústeres local o de cualquier proveedor de nube. Independiente clústeres ofrecen a Hola libertad toohost un clúster siempre que lo desee. Si los datos son toocompliance de asunto o restricciones legales o desea tookeep datos local, puede alojar su propio clúster y aplicaciones. Aplicaciones de Service Fabric pueden ejecutar en varios entornos de hospedaje sin realizar ningún cambio, por lo que sus conocimientos de creación de aplicaciones lleva a través de un tooanother de entorno de hospedaje. 

[Creación del primer clúster independiente de Service Fabric](service-fabric-get-started-standalone-cluster.md)

Aún no se admiten clústeres de Linux independientes.

### <a name="cluster-security"></a>Seguridad de clúster
Clústeres deben ser segura tooprevent no autorizado a los usuarios conecten clúster tooyour, especialmente cuando tiene las cargas de trabajo de producción en ejecución. Aunque es posible toocreate un clúster no seguro, esto permite que los usuarios anónimos tooconnect tooit si los extremos de administración están expuestos toohello internet pública. No es posible toolater Habilitar seguridad en un clúster no segura: seguridad de clúster está habilitada en el momento de creación de clúster.

escenarios de seguridad de clúster de Hello son:
* Seguridad de nodo a nodo
* Seguridad de cliente a nodo
* Control de acceso basado en roles (RBAC)

Para más información, lea [Proteger un clúster](service-fabric-cluster-security.md).

### <a name="scaling"></a>Escalado
Si agrega el nuevo clúster de nodos toohello, Service Fabric vuelve a equilibrar réplicas de la partición de Hola y las instancias a través de hello mayor número de nodos. Mejora el rendimiento de la aplicación global y reduce la contención de toomemory de acceso. Si no se utilizan eficazmente nodos hello en clúster de hello, puede reducir número Hola de nodos de clúster de Hola. Service Fabric vuelve a volver a equilibrar réplicas de la partición de Hola y mejorar el uso de instancias a través de hello reducido número de nodos toomake de hardware de hello en cada nodo. Puede escalar clústeres en Azure [manualmente](service-fabric-cluster-scale-up-down.md) o [mediante programación](service-fabric-cluster-programmatic-scaling.md). Los clústeres independientes se pueden escalar [manualmente](service-fabric-cluster-windows-server-add-remove-nodes.md).

### <a name="cluster-upgrades"></a>Actualizaciones de clústeres
Periódicamente, se publican nuevas versiones del tiempo de ejecución de hello Service Fabric. Realice actualizaciones en tiempo de ejecución o de Service Fabric en el clúster, a fin de que siempre ejecute una [versión compatible](service-fabric-support.md). Además se actualiza toofabric, también puede actualizar la configuración del clúster como certificados o puertos de la aplicación.

Un clúster de Service Fabric es un recurso de su propiedad administrado parcialmente por Microsoft. Microsoft es responsable de la aplicación de revisiones Hola subyacente SO y realizar actualizaciones de tejido en el clúster. Puede establecer a su tejido automática de tooreceive de clúster de las actualizaciones, cuando Microsoft publica una nueva versión, o elegir tooselect una versión compatible de tejido que desee. Las actualizaciones de tejido y configuración se pueden establecer a través del portal de Azure de Hola o a través del Administrador de recursos. Para más información, lea [Actualización de un clúster de Azure Service Fabric](service-fabric-cluster-upgrade.md). 

Un clúster independiente es un recurso que es totalmente de su propiedad. Usted es responsable de la aplicación de revisiones Hola subyacente OS e iniciar las actualizaciones de tejido. Si el clúster se puede conectar demasiado[https://www.microsoft.com/download](https://www.microsoft.com/download), puede establecer la descarga de tooautomatically de clúster y aprovisionar Hola tejido de servicio nuevo paquete en tiempo de ejecución. A continuación, podría iniciar actualización Hola. Si no se puede obtener acceso su clúster [https://www.microsoft.com/download](https://www.microsoft.com/download), puede descargar manualmente el paquete en tiempo de ejecución de la nueva Hola desde un equipo conectado internet y, a continuación, iniciar la actualización de Hola. Para más información, lea [Actualización de un clúster independiente de Azure Service Fabric](service-fabric-cluster-upgrade-windows-server.md).

## <a name="health-monitoring"></a>Supervisión del estado
Service Fabric presenta un [modelo de estado](service-fabric-health-introduction.md) diseñado tooflag clúster en mal estado y las condiciones de aplicación en entidades concretas (por ejemplo, los nodos del clúster y las réplicas de servicio). modelo de estado de Hello usa Informadores de mantenimiento (componentes del sistema y watchdogs). objetivo de Hello es fácil y rápido un diagnóstico más detallado y reparación. Escritores del servicio necesitan toothink por adelantado sobre el estado y cómo demasiado[informes sobre el estado de diseño](service-fabric-report-health.md#design-health-reporting). Cualquier condición que puede afectar el estado debería aparecer en, sobre todo si puede ayudar a problemas de marca cerrar toohello raíz. información de estado de Hello puede ahorrar tiempo y esfuerzo en depuración e investigación una vez Hola servicio está en funcionamiento y se ejecuta a escala en producción.

monitor de Informadores de Service Fabric Hola identifica las condiciones de interés. Informan sobre esas condiciones en función de su vista local. Hola [almacén de estado](service-fabric-health-introduction.md#health-store) agrega datos de estado enviados por todos los toodetermine Informadores si las entidades son globalmente correcto. modelo de Hello es toouse enriquecido, flexible y fácil de toobe previsto. calidad de Hola de informes de estado de hello determina la precisión de Hola de vista de estado de Hola de clúster de Hola. Los falsos positivos que muestran erróneamente problemas pueden afectar negativamente a las actualizaciones u otros servicios que usan datos de mantenimiento. Ejemplos de estos servicios son los servicios de reparación y los mecanismos de alerta. Por lo tanto, algunas consideraciones es informes tooprovide necesarios que capturan las condiciones de interés en hello mejor manera posible.

Los informes pueden elaborarse a partir de:
* Hola supervisa réplicas del servicio de Service Fabric o instancia.
* Guardianes internos implementados como un servicio de Service Fabric (por ejemplo, un servicio sin estado de Service Fabric que supervisa las condiciones y los informes de problemas). watchdogs Hola pueden implementarse en todos los nodos o pueden ser servicio de afinidad toohello supervisado.
* Watchdogs internos que se ejecutan en nodos de Service Fabric Hola pero no se implementan como servicios de Service Fabric.
* Externo watchdogs ese recurso Hola de sondeo de clúster de Service Fabric Hola exterior (por ejemplo, servicio de supervisión como Gomez).

Fuera del cuadro de hello, componentes de Service Fabric informan estado en todas las entidades de clúster de Hola. Los [informes de mantenimiento del sistema](service-fabric-understand-and-troubleshoot-with-system-health-reports.md) proporcionan visibilidad en el clúster y funcionalidad de la aplicación, además de marcar problemas a través del estado. Para aplicaciones y servicios, informes de mantenimiento del sistema comprueban que las entidades se implementan y se comportan correctamente desde la perspectiva de Hola de tiempo de ejecución de hello Service Fabric. informes de Hello no proporcionan ninguna supervisión de estado de lógica de negocios de Hola de servicio de Hola o detectar procesos bloqueados. lógica de tooadd información específica tooyour servicio de mantenimiento, [implementar informes sobre el estado personalizado](service-fabric-report-health.md) en los servicios.

Service Fabric proporciona varias maneras de demasiado[ver informes de mantenimiento](service-fabric-view-entities-aggregated-health.md) agregado en el almacén de estado de hello:
* [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) y otras herramientas de visualización.
* Consultas de estado (a través de [PowerShell](/powershell/module/ServiceFabric/), hello [C# FabricClient APIs](/api/system.fabric.fabricclient.healthclient) y [Java FabricClient APIs](/java/api/system.fabric._health_client), o [API de REST](/rest/api/servicefabric)).
* Generales consultas que devuelven una lista de entidades que tienen el estado como una de las propiedades de hello (a través de PowerShell, API de Hola o REST).

Hola que siguiente Microsoft Virtual Academy vídeo describe el modelo de estado de Service Fabric de Hola y cómo se utiliza:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-content-roadmap/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo toocreate una [clúster en Azure](service-fabric-cluster-creation-via-portal.md) o un [clúster independiente en Windows](service-fabric-cluster-creation-for-windows-server.md).
* Intente crear un servicio mediante hello [servicios confiables](service-fabric-reliable-services-quick-start.md) o [Reliable Actors](service-fabric-reliable-actors-get-started.md) modelos de programación.
* Obtenga información acerca de cómo demasiado[migrar servicios de nube de](service-fabric-cloud-services-migration-differences.md).
* Obtenga información acerca de demasiado[supervisar y diagnosticar servicios](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). 
* Obtenga información acerca de demasiado[probar sus aplicaciones y servicios](service-fabric-testability-overview.md).
* Obtenga información acerca de demasiado[administrar y organizar recursos de clúster](service-fabric-cluster-resource-manager-introduction.md).
* Buscar a través de hello [ejemplos de Service Fabric](http://aka.ms/servicefabricsamples).
* Más información sobre las [opciones de soporte técnico de Service Fabric](service-fabric-support.md).
* Hola de lectura [blog del equipo](https://blogs.msdn.microsoft.com/azureservicefabric/) artículos y anuncios.


[cluster-application-instances]: media/service-fabric-content-roadmap/cluster-application-instances.png
[cluster-imagestore-apptypes]: ./media/service-fabric-content-roadmap/cluster-imagestore-apptypes.png
