---
title: aaaOverview de Service Fabric y contenedores | Documentos de Microsoft
description: "Información general de Service Fabric y Hola el uso de aplicaciones de microservicio toodeploy de contenedores. Este artículo proporciona información general del proceso de contenedores se pueden utilizar y Hola capacidades disponibles en Service Fabric."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: c98b3fcb-c992-4dd9-b67d-2598a9bf8aab
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: fce94c4b476351c90f23f706aab8bc17319cce22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-and-containers"></a>Service Fabric y contenedores
> [!NOTE]
> Esta característica se encuentra en su versión preliminar para Linux.  Implementar contenedores de clúster de Service Fabric tooa en Windows 10 no se admite aún (próximamente). 
>   

## <a name="introduction"></a>Introducción
Azure Service Fabric es un [orquestador](service-fabric-cluster-resource-manager-introduction.md) de servicios a través de un clúster de máquinas, con años de uso y optimización en servicios de escala masiva de Microsoft. Los servicios se pueden desarrollar en muchos sentidos, utilizasen hello [modelos de programación de Service Fabric](service-fabric-choose-framework.md) toodeploying [invitado ejecutables](service-fabric-deploy-existing-app.md). De forma predeterminada Service Fabric permite implementar y activar estos servicios como procesos. Procesos proporcionan activación de hello más rápida y mayor uso de densidad de recursos de hello en un clúster. Service Fabric puede implementar también servicios en imágenes de contenedor. Lo que es importante, puede mezclar los servicios de procesos y servicios en los contenedores de hello misma aplicación. 

## <a name="containers-and-service-fabric-roadmap"></a>Contenedores y mapa de ruta de Service Fabric
En las próximas versiones, están previstas muchas mejoras para la organización de los contenedores con Service Fabric. Entre ellas, características para una mejor conexión de red con compatibilidad con redes virtuales en una aplicación, características de seguridad, diagnósticos mejorados y compatibilidad con herramientas. Service Fabric permite aplicaciones toocreate mezclar contenedores empaquetados con el código existente (por ejemplo, aplicaciones de IIS MVC) con los servicios desarrollados con modelos de programación de Service Fabric Hola.  Puede ejecutar varias de estas aplicaciones en un único clúster. 

## <a name="what-are-containers"></a>¿Qué son los contenedores?
Se encapsulan contenedores, puede implementables individualmente componentes que se ejecutan como instancias aisladas en Hola mismo kernel tootake aprovechar virtualización que proporciona un sistema operativo. Por lo tanto, cada aplicación y sus bibliotecas en tiempo de ejecución, las dependencias y el sistema se ejecutan dentro de un contenedor con acceso completo y privada toohello del propio aislado vista del contenedor de construcciones de sistema operativo. Junto con la portabilidad, este grado de aislamiento de seguridad y recursos es la ventaja principal de hello para el uso de contenedores con Service Fabric, que ejecuta los servicios de procesos en caso contrario.

Los contenedores son una tecnología de virtualización que virtualiza el sistema operativo subyacente de Hola desde las aplicaciones. Los contenedores proporcionan un entorno inmutable para aplicaciones toorun con diversos grados de aislamiento. Los contenedores se ejecutan directamente sobre el kernel de Hola y tienen una vista aislada del sistema de archivos de Hola y otros recursos. Las máquinas de toovirtual comparados, contenedores tienen Hola siguientes ventajas:

* **Pequeño**: contenedores utilizan un único espacio y capa de versiones y actualizaciones tooincrease eficacia de almacenamiento.
* **Fast**: contenedores no tienen tooboot un sistema operativo completo, para que pueden iniciar con mayor rapidez, normalmente en segundos.
* **Portabilidad**: una imagen de la aplicación en contenedores puede ser toorun migrado en la nube de hello, de forma local, dentro de máquinas virtuales, o directamente en las máquinas virtuales.
* **La regulación de recursos**: un contenedor puede limitar los recursos físicos de Hola que puede utilizar en su host.

## <a name="container-types"></a>Tipos de contenedor
Service Fabric admite contenedores en Linux y Windows y también admite el modo de aislamiento de Hyper-V en hello este último. 

### <a name="docker-containers-on-linux"></a>Contenedores de Docker en Linux
Docker ofrece toocreate de las API de alto nivel y administrar contenedores sobre contenedores de kernel de Linux. Centro de docker es un repositorio central toostore y recuperar imágenes del contenedor.
Para obtener un tutorial, vea [implementar un tooService de contenedor de Docker tejido](service-fabric-get-started-containers-linux.md).

### <a name="windows-server-containers"></a>Contenedores de Windows Server
Windows Server 2016 ofrece dos tipos diferentes de contenedores que se diferencian en el nivel de Hola de aislamiento proporcionado. Contenedores de Windows Server y Docker son similares porque ambos tienen el espacio de nombres y el archivo aislamiento pero el recurso compartido de hello kernel del sistema con que se ejecutan en el host de Hola. En Linux, este aislamiento tradicionalmente lo han proporcionado los `cgroups` y `namespaces`, y los contenedores de Windows Server se comportan de forma parecida.

Contenedores de Hyper-V de Windows ofrecen mayor aislamiento y seguridad porque cada contenedor no comparte el kernel del sistema operativo de hello con otros contenedores o con el host de Hola. Con este mayor nivel de aislamiento de seguridad, los contenedores de Hyper-V están diseñados para escenarios hostiles y multiinquilino.
Para obtener un tutorial, vea [implementar un tooService de contenedor de Windows Fabric](service-fabric-get-started-containers.md).

Hello en la ilustración siguiente se muestra hello tipos diferentes de los niveles de virtualización y aislamiento disponibles en el sistema operativo de Hola.
![Plataforma de Service Fabric][Image1]

## <a name="scenarios-for-using-containers"></a>Escenarios de uso de contenedores
Ejemplos típicos de buena elección de contenedor:

* **IIS levantar y mover**: si dispone de [ASP.NET MVC](https://www.asp.net/mvc) aplicaciones que quieran toocontinue toouse, colóquelos en un contenedor en lugar de migrarlos tooASP.NET Core. Estas aplicaciones de ASP.NET MVC dependen de Internet Information Services (IIS). Puede empaquetar estas aplicaciones en las imágenes del contenedor de hello creados previamente la imagen de IIS e implementarlas con Service Fabric. Vea [imágenes de contenedores en Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/quick_start/quick_start_images) para obtener información acerca de cómo toocreate imágenes IIS.
* **Combinación de contenedores y microservicios de Service Fabric**: use una imagen de contenedor existente para la parte de la aplicación. Por ejemplo, podría usar hello [contenedor NGINX](https://hub.docker.com/_/nginx/) front-end de web de Hola de las aplicaciones y servicios con estado para hello cálculo más intensivo de back-end.
* **Reducir el impacto de los servicios de "vecino ruidoso"**: puede utilizar la capacidad de regulación de recursos Hola de recursos de hello toorestrict de contenedores que utiliza un servicio en un host. Si servicios pueden consumir muchos recursos y afectar al rendimiento de Hola de otros usuarios (por ejemplo, una operación de larga duración, tipo de consulta), considere la posibilidad de colocar estos servicios en contenedores que tienen el regulador de recursos.

## <a name="service-fabric-support-for-containers"></a>Compatibilidad de los contenedores con Service Fabric
Service Fabric admite actualmente la implementación de contenedores de Docker en contenedores de Linux y Windows Server en Windows Server 2016, además de compatibilidad con el modo de aislamiento de Hyper-V. 

Hola Service Fabric [modelo de aplicación](service-fabric-application-model.md), un contenedor representa un host de aplicación en la que varios servicios se colocan las réplicas. Service Fabric puede ejecutar cualquier contenedor, y escenario de hello es similar toohello [invitados ejecutable](service-fabric-deploy-existing-app.md), donde se empaqueta una aplicación existente dentro de un contenedor. Este escenario es hello-caso de uso común para los contenedores y ejemplos incluyen la ejecución de una aplicación escrita utilizando cualquier lenguaje o marcos de trabajo, pero no usa modelos de programación de Service Fabric integrados Hola.

Además, también puede ejecutar los servicios de Service Fabric dentro de contenedores. Compatibilidad con los servicios de Service Fabric ejecución dentro de contenedores está limitado en la actualidad, pero toobe mejorada en las próximas versiones.

* **Los servicios sin estado confiables dentro de contenedores**: servicios sin estado confiable mediante servicios confiables Hola modelos de programación solo se admiten en Linux. Está prevista la compatibilidad con Reliable Stateless Services en contenedores de Windows en futuras versiones.
* **Servicios con estado dentro de contenedores**: estos servicios usan el modelo de programación de hello Reliable Actors o servicios de confianza. La compatibilidad con la ejecución de servicios con estado en contenedores se agregará en una versión futura.

Service Fabric tiene varias funcionalidades de contenedor que le ayudarán a crear aplicaciones que se componen de microservicios en contenedores. Hola de ofertas de Service Fabric después de capacidades para servicios en contenedores de:

* Activación e implementación de la imagen de contenedor.
* La regulación de recursos.
* La autenticación de repositorios.
* Asignación de puertos de toohost de puerto del contenedor.
* La detección y comunicación entre contenedores.
* Capacidad tooconfigure y establecer variables de entorno.

## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha aprendido acerca de los contenedores y que Service Fabric es un orquestador de contenedores y las características compatibles con los contenedores. Como paso siguiente, se pasa a través de ejemplos de cada uno de hello características tooshow cómo toouse ellos.

[Implementar un tooService de contenedor de Windows Fabric en Windows Server 2016](service-fabric-get-started-containers.md)

[Implementar un tooService de contenedor de Docker Fabric en Linux](service-fabric-get-started-containers-linux.md)

[Image1]: media/service-fabric-containers/Service-Fabric-Types-of-Isolation.png
