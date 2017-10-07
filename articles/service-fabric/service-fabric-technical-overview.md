---
title: "terminología de Azure Service Fabric aaaLearn | Documentos de Microsoft"
description: "Descripción sobre la terminología de Service Fabric. Describe la terminología clave conceptos y términos usados en el resto de Hola de documentación de Hola."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: chackdan;subramar
ms.assetid: 3a970679-e19e-43b3-9be8-71773f307c57
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/02/2017
ms.author: ryanwi
ms.openlocfilehash: 4781fc0527b8a58e534183249bc2759aded2730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-terminology-overview"></a>Información general sobre la terminología de Service Fabric
Service Fabric es una plataforma de sistemas distribuidos que resulta fácil toopackage, implementar y administrar microservicios escalables y confiables. Este tema detalles Hola terminología que se usa por Service Fabric toounderstand Hola términos utilizados en la documentación de Hola.

Hello conceptos descritos en esta sección también se tratan en hello siguientes vídeos de Microsoft Virtual Academy: <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">principales conceptos</a>, <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965">conceptos de tiempo de diseño</a>, y <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">conceptos de tiempo de ejecución</a>.

## <a name="infrastructure-concepts"></a>Conceptos de infraestructura
**Clúster**: conjunto de máquinas físicas o virtuales conectadas a la red en las que se implementan y administran los microservicios.  Clústeres pueden escalar toothousands de máquinas.

**Nodo**: cada una de las máquinas físicas o virtuales que forman parte de un clúster se denominan "nodo". A cada nodo se le asigna un nombre de nodo (una cadena). Los nodos tienen características como las propiedades de colocación. Cada máquina física o virtual tiene un servicio de Windows de inicio automático, `FabricHost.exe`, que empieza a ejecutarse en el arranque y luego inicia dos ejecutables: `Fabric.exe` y `FabricGateway.exe`. Estos dos ejecutables constituyen nodo Hola. En los escenarios de prueba, se pueden hospedar varios nodos en un solo equipo y máquina virtual mediante la ejecución de varias instancias de `Fabric.exe` y `FabricGateway.exe`.

## <a name="application-concepts"></a>Conceptos de las aplicaciones
**Tipo de aplicación**: Hola nombre/versión que se asignó tooa colección de tipos de servicio. Definido en un `ApplicationManifest.xml` de archivos, incrustado en un directorio del paquete de aplicación, que es, a continuación, copian el almacén de imágenes del clúster de Service Fabric toohello. A continuación, puede crear una aplicación con nombre de este tipo de aplicación en clúster de Hola.

Hola de lectura [modelo de aplicación](service-fabric-application-model.md) artículo para obtener más información.

**Paquete de aplicación**: un directorio de disco que contiene el tipo de aplicación Hola `ApplicationManifest.xml` archivo. Referencias Hola paquetes de servicio para cada tipo de servicio que conforma el tipo de aplicación Hola. archivos de Hello en el directorio del paquete de aplicación Hola son almacén de imágenes del clúster de tejido tooService copiada. Por ejemplo, un paquete de aplicación para un tipo de aplicaciones de correo electrónico podría contener paquete del servicio de cola de referencias tooa, un paquete de servicios de front-end y un paquete de servicios de base de datos.

**Con el nombre de aplicación**: después de un paquete de aplicación es el almacén de imágenes de toohello copiado, se crea una instancia de la aplicación hello en clúster de hello mediante la especificación de tipo de aplicación del paquete de aplicación Hola (mediante su nombre/versión). A cada instancia del tipo de aplicación se le asigna un nombre de URI similar al siguiente: `"fabric:/MyNamedApp"`. En un clúster se pueden crear varias aplicaciones con nombre de un único tipo de aplicación. También se pueden crear aplicaciones con nombre de diferentes tipos de aplicación. Cada aplicación con nombre se administra de manera independiente y tiene versiones independientes.      

**Tipo de servicio**: Hola nombre/versión asignados paquetes de código del servicio de tooa, paquetes de datos y paquetes de configuración. Definido en un `ServiceManifest.xml` archivo, incrustado en un directorio del paquete de servicio y el directorio del paquete de servicio de hello, a continuación, se hace referencia un paquete de aplicación `ApplicationManifest.xml` archivo. En el clúster de hello, después de crear una aplicación con nombre, puede crear un servicio con nombre desde uno de hello tipos de servicio del tipo de aplicación. Hola del tipo de servicio `ServiceManifest.xml` archivo describe el servicio de Hola.

Hola de lectura [modelo de aplicación](service-fabric-application-model.md) artículo para obtener más información.

Existen dos tipos de servicios:

* **Stateless:** usar un servicio sin estado al estado persistente del servicio de Hola se almacena en un servicio de almacenamiento externo, como el almacenamiento de Azure, base de datos de SQL Azure o base de datos de Azure Cosmos. Usar un servicio sin estado al servicio de hello no tiene ningún almacenamiento persistente. Por ejemplo, un servicio de calculadora donde los valores se pasan toohello servicio, se realiza un cálculo con estos valores y se devuelve un resultado.
* **Con estado:** utilice un servicio con estado cuando desee Service Fabric toomanage el estado de su servicio a través de sus colecciones confiable o Reliable Actors modelos de programación. Especifique cuántas particiones que desea toospread su estado sobre (para escalabilidad) al crear un servicio con nombre. Especificar cuántas veces tooreplicate su estado en todos los nodos (para la confiabilidad). Todos los servicios con nombre tienen una única réplica principal y varias réplicas secundarias. Modificar el estado de su servicio con nombre escribiendo toohello de réplica principal. Tejido de servicio, a continuación, replica este estado tooall Hola réplicas secundarias mantiene su estado sincronizado. Service Fabric detecta automáticamente cuando se produce un error de una réplica principal y promociona una réplica principal de tooa de réplica secundaria existente. Seguidamente, Service Fabric crea una nueva réplica secundaria.  

**Paquete de servicio**: un directorio de disco que contenga del tipo de servicio de hello `ServiceManifest.xml` archivo. Este archivo hace referencia a código de hello, datos estáticos y paquetes de configuración para el tipo de servicio de Hola. del tipo de aplicación Hola hace referencia a los archivos de Hello en el directorio del paquete de servicio de hello `ApplicationManifest.xml` archivo. Por ejemplo, un paquete de servicio podría hacer referencia a código de toohello, los datos estáticos y los paquetes de configuración que componen un servicio de base de datos.

**Con el nombre de servicio**: después de crear una aplicación con nombre, puede crear una instancia de uno de sus tipos de servicio en clúster de hello mediante la especificación de tipo de servicio de hello (mediante su nombre/versión). A cada instancia del tipo de servicio se le asigna un nombre de URI cuyo ámbito es el URI de su aplicación con nombre. Por ejemplo, si crea un servicio dentro de una aplicación con el nombre "MyNamedApp" con el nombre "MyDatabase", Hola URI el siguiente aspecto: `"fabric:/MyNamedApp/MyDatabase"`. En una aplicación con nombre, se pueden crear varios servicios con nombre. Todos los servicios con nombre pueden tener su propio esquema de partición y cuentas de instancia o réplica.

**Paquete de código**: un directorio de disco que contiene los archivos ejecutables del tipo de servicio de hello (normalmente archivos EXE o DLL). del tipo de servicio de hello hace referencia a los archivos de Hello en el directorio del paquete de código de hello `ServiceManifest.xml` archivo. Cuando se crea un servicio con nombre, el paquete de código de hello es nodo copiado toohello o hello toorun seleccionado de nodos con el nombre de servicio. A continuación, el código de hello comienza a ejecutarse. Hay dos tipos de ejecutables de paquetes de código:

* **Archivos ejecutables de invitado**: archivos ejecutables que se ejecutan como-está en el sistema de operativo de host de hello (Windows o Linux). Es decir, estos ejecutables no no vínculo tooor referencia los archivos de Service Fabric en tiempo de ejecución y, por tanto, no utilizan los modelos de programación de Service Fabric. Estos ejecutables son no se puede toouse que Hola de algunas características de Service Fabric como nombres de servicio para la detección de punto de conexión. Archivos ejecutables de invitado no pueden informar de instancia de servicio de tooeach específico de las métricas de carga.
* **Ejecutables de Host del servicio**: archivos ejecutables que utilizan Service Fabric modelos de programación al vincular archivos de tiempo de ejecución de tejido tooService, habilitar características de Service Fabric. Por ejemplo, una instancia del servicio con nombre puede registrar puntos de conexión con en el servicio de nombres de Service Fabric y también puede notificar métricas de carga.      

**Paquete de datos**: un directorio de disco que contiene archivos de datos estáticos, de sólo lectura del tipo de servicio de hello (normalmente archivos de fotos, dispositivos de sonido y vídeo). del tipo de servicio de hello hace referencia a los archivos de Hello en el directorio del paquete de datos de hello `ServiceManifest.xml` archivo. Cuando se crea un servicio con nombre, el paquete de datos de hello es nodo copiado toohello o hello toorun seleccionado de nodos con el nombre de servicio.  código de Hello empieza a ejecutarse y ahora puede tener acceso a archivos de datos de Hola.

**Paquete de configuración**: archivos de configuración de solo lectura de un directorio de disco que contiene estático del tipo de servicio de hello, (normalmente archivos de texto). del tipo de servicio de hello hace referencia a los archivos de Hello en el directorio del paquete de configuración de hello `ServiceManifest.xml` archivo. Cuando se crea un servicio con nombre, archivos de hello en el paquete de configuración de hello son copiado toohello uno o más hello toorun seleccionado de nodos denominado service. A continuación, código de hello empieza a ejecutarse y ahora puede tener acceso a archivos de configuración de Hola.

**Contenedores**: de forma predeterminada Service Fabric permite implementar y activar estos servicios como procesos. Service Fabric puede implementar también servicios en imágenes de contenedor. Los contenedores son una tecnología de virtualización que virtualiza el sistema operativo subyacente de Hola desde las aplicaciones. Una aplicación y sus bibliotecas en tiempo de ejecución, las dependencias y el sistema se ejecutan dentro de un contenedor con acceso completo y privada toohello del propio aislado vista del contenedor de construcciones de sistema operativo. Service Fabric admite contenedores de Docker de los contenedores de Linux y Windows Server.  Para obtener más información, lea el artículos sobre [Service Fabric y los contenedores](service-fabric-containers-overview.md).

**Esquema de partición**: al crear un servicio con nombre, especifique un esquema de partición. Los servicios con grandes cantidades de estado de dividen los datos de hello en particiones, que se propaga el estado de hello en todos los nodos del clúster de Hola. Esto permite tooscale de estado de su servicio con nombre. Dentro de una partición, los servicios con nombre sin estado tienen instancias, mientras que los servicios con nombre con estado tienen réplicas. Normalmente, los servicios con nombre sin estado solo tienen una partición, ya que no tienen un estado interno. proporcionan instancias de la partición de Hola para disponibilidad; Si se produce un error en una instancia, otras instancias continúan toooperate normalmente y, a continuación, Service Fabric creará una nueva instancia. Con estado denominado services mantienen su estado en las réplicas y cada partición tiene su propio conjunto de réplicas con todos los Estados de Hola que se mantienen sincronizados. Si falla una réplica, Service Fabric genera una nueva réplica de réplicas de hello existentes.

Hola de lectura [servicios confiables de partición Service Fabric](service-fabric-concepts-partitioning.md) artículo para obtener más información.

## <a name="system-services"></a>Servicios del sistema
Hay servicios del sistema que se crean en cada clúster que proporcionan capacidades de la plataforma de Hola de Service Fabric.

**Servicio de nombres**: clúster de Fabric de cada servicio tiene un servicio de nomenclatura, que se resuelve la ubicación de tooa de nombres del servicio en clúster de Hola. Administrar nombres de servicio de Hola y propiedades, tooan similar internet servicio de nombres de dominio (DNS) para el clúster de Hola. Los clientes comunican con seguridad con cualquier nodo de clúster hello mediante Hola Naming Service tooresolve un nombre de servicio y su ubicación.  Las aplicaciones mover en clúster de hello como vencimiento toofailures, equilibrar los recursos u Hola cambiar el tamaño de clúster de Hola. Puede desarrollar servicios y clientes que resolver la ubicación de red actual de Hola. Los clientes obtener dirección IP de hello real del equipo y el puerto donde se está ejecutando actualmente.

Lectura [comunicar con los servicios de](service-fabric-connect-and-communicate-with-services.md) para obtener más información en la comunicación de cliente y el servicio de hello API que funcionan con hello servicio de nombres.

**Servicio de almacenamiento de imágenes**: cada clúster de Service Fabric tiene un servicio de almacenamiento de imágenes donde se guardan los paquetes de aplicación implementados y con versión. Copie un toohello de paquete de aplicación Image Store y, a continuación, registrar el tipo de aplicación Hola dentro de ese paquete de aplicación. Después de aprovisiona el tipo de aplicación Hola, cree una aplicación con nombre de él. Puede anular el registro de un tipo de aplicación de hello el servicio de almacenamiento de la imagen después de que todas sus aplicaciones con nombre que se haya eliminado.

Lectura [comprender la configuración de hello ImageStoreConnectionString](service-fabric-image-store-connection-string.md) para obtener más información acerca de hello el servicio de almacenamiento de la imagen.

Hola de lectura [implementar una aplicación](service-fabric-deploy-remove-applications.md) artículo para obtener más información sobre la implementación de servicio de almacén de imágenes de aplicaciones toohello.

## <a name="built-in-programming-models"></a>Modelos de programación integrados
Para que los servicios de Service Fabric toobuild existen modelos de programación de .NET Framework:

**Servicios de confianza**: toobuild con y sin estado servicios de una API. Los servicios con estado almacenan su estado en Reliable Collections (como un diccionario o una cola). También obtendrá tooplug en varias pilas de comunicación como la API de Web y Windows Communication Foundation (WCF).

**Reliable Actors**: An toobuild con y sin estado objetos de la API a través del modelo de programación de Actor virtual Hola. Este modelo puede resultar útil cuando hay muchas unidades independientes de cálculo/estado. Dado que este modelo utiliza un modelo de subprocesos a su vez, es mejor código tooavoid que llama a los actores tooother o servicios, puesto que un actor individual no puede procesar las demás solicitudes entrantes hasta que se completen todas sus solicitudes salientes.

Hola de lectura [elegir un modelo de programación para el servicio](service-fabric-choose-framework.md) artículo para obtener más información.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de Service Fabric:

* [Información general de Service Fabric](service-fabric-overview.md)
* [¿Por qué un microservicios enfocar toobuilding aplicaciones?](service-fabric-overview-microservices.md)
* [Escenarios de aplicación](service-fabric-application-scenarios.md)

