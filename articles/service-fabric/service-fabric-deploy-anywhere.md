---
title: "aaaCreate Azure Service Fabric clústeres en Windows Server y Linux | Documentos de Microsoft"
description: "Clústeres de Service Fabric ejecutar en Windows Server y Linux, lo que significa dejarán ser capaz de aplicaciones de Service Fabric toodeploy y el host desde cualquier lugar puede ejecutar Windows Server o Linux."
services: service-fabric
documentationcenter: .net
author: Chackdan
manager: timlt
editor: 
ms.assetid: 19ca51e8-69b9-4952-b4b5-4bf04cded217
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/08/2017
ms.author: chackdan
ms.openlocfilehash: 46d5f3d019339c57a0024f5a9d47d9018cca01a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-fabric-clusters-on-windows-server-or-linux"></a>Creación de clústeres de Service Fabric en Windows Server o Linux
Un clúster de Azure Service Fabric es un conjunto de máquinas físicas o virtuales conectadas a la red en las que se implementan y administran los microservicios. Una máquina física o virtual que forma parte de un clúster se denomina nodo del clúster. Clústeres pueden escalar toothousands de nodos. Si agrega el nuevo clúster de nodos toohello, Service Fabric vuelve a equilibrar réplicas hello de la partición de servicio y las instancias a través de hello mayor número de nodos. Mejora el rendimiento de la aplicación global y reduce la contención de toomemory de acceso. Si no se utilizan eficazmente nodos hello en clúster de hello, puede reducir número Hola de nodos de clúster de Hola. Service Fabric vuelve a volver a equilibrar réplicas de la partición de Hola y mejorar el uso de instancias a través de hello reducido número de nodos toomake de hardware de hello en cada nodo.

Service Fabric permite la creación de hello de clústeres de Service Fabric en las máquinas virtuales o equipos que ejecutan Windows Server o Linux. Esto significa que puede toodeploy y ejecuta aplicaciones de Service Fabric en cualquier entorno donde haya un conjunto de equipos de Windows Server o Linux que están conectados entre sí, ya sea de forma local, Microsoft Azure o con cualquier proveedor de nube.

## <a name="create-service-fabric-clusters-on-azure"></a>Creación de clústeres de Service Fabric en Azure
Creación de un clúster en Azure se realiza a través de una plantilla de modelo de recursos u Hola portal de Azure. Lectura [crear un clúster de Service Fabric mediante una plantilla de administrador de recursos](service-fabric-cluster-creation-via-arm.md) o [crear un clúster de Service Fabric de hello Azure portal](service-fabric-cluster-creation-via-portal.md) para obtener más información.

## <a name="supported-operating-systems-for-clusters-on-azure"></a>Sistemas operativos compatibles con clústeres en Azure
Son toocreate capaz de clústeres en máquinas virtuales que ejecutan estos sistemas operativos:

* Windows Server 2012 R2
* Windows Server 2016 
* Linux Ubuntu 16.04 (en versión preliminar pública) 

## <a name="create-service-fabric-standalone-clusters-on-premises-or-with-any-cloud-provider"></a>Creación de clústeres independientes de Service Fabric de forma local o con cualquier proveedor de nube
Service Fabric proporciona un paquete de instalación para toocreate independiente Service Fabric clústeres local o de cualquier proveedor de nube

Para más información sobre la configuración de clústeres independientes de Service Fabric en Windows Server, lea [Creación y administración de un clúster que se ejecute en Windows Server](service-fabric-cluster-creation-for-windows-server.md)

### <a name="any-cloud-deployments-vs-on-premises-deployments"></a>Implementaciones en la nube frente a implementaciones locales
Hola proceso para crear un clúster de Service Fabric local es similar toohello proceso de creación de un clúster en cualquier nube de su elección con un conjunto de máquinas virtuales. Hola pasos iniciales tooprovision Hola máquinas virtuales se rige por el proveedor de nube de Hola o entorno local que está usando. Una vez que tenga un conjunto de máquinas virtuales con conectividad de red habilitada entre ellos, a continuación, Hola pasos tooset paquete de Service Fabric hello, editar la configuración de clúster de hello, creación de clústeres de Hola y ejecutar scripts de administración son idénticas. Esto garantiza que sus conocimientos y experiencia de operar y administrar clústeres de Service Fabric es transferible cuando elige tootarget nuevos entornos de hospedaje.

### <a name="benefits-of-creating-standalone-service-fabric-clusters"></a>Ventajas de crear clústeres independientes de Service Fabric
* Es libre toochoose cualquier nube proveedor toohost el clúster.
* Aplicaciones de Service Fabric, una vez escritas, se pueden ejecutar en varios entornos de hospedaje con cambios mínimos toono.
* Conocimiento de la creación de aplicaciones de Service Fabric lleva a través de un tooanother de entorno de hospedaje.
* Experiencia operativa de la ejecución y administración de Service Fabric clústeres realiza a través de un entorno tooanother.
* Existe una amplia cobertura de clientes sin limitaciones derivadas de las restricciones del entorno de hospedaje.
* Un nivel adicional de confiabilidad y la protección contra interrupciones generalizadas existe porque puede mover servicios Hola sobre el entorno de implementación de tooanother si un centro de datos o proveedor de nube tiene un apagón.

## <a name="supported-operating-systems-for-standalone-clusters"></a>Sistemas operativos compatibles con clústeres independientes
Son toocreate capaz de clústeres en las máquinas virtuales o equipos que ejecutan estos sistemas operativos:

* Windows Server 2012 R2
* Windows Server 2016 
* Linux (próximamente)

## <a name="advantages-of-service-fabric-clusters-on-azure-over-standalone-service-fabric-clusters-created-on-premises"></a>Ventajas de los clústeres de Service Fabric en Azure frente a los clústeres independientes de Service Fabric creados de forma local
Clústeres de Service Fabric se ejecuta en Azure proporciona ventajas sobre la opción de hello en local, por lo que si no tiene necesidades específicas de donde se ejecutan los clústeres, a continuación, se recomienda que se ejecute en Azure. En Azure, se proporcionan una integración con otros servicios, lo que facilita las operaciones y administración de clúster de Hola y más confiable y características de Azure.

* **Portal de Azure:** portal de Azure resulta fácil toocreate y administrar clústeres.
* **Azure Resource Manager:** uso del Administrador de recursos de Azure permite una administración sencilla de todos los recursos usados por clúster hello como una unidad y simplifica el seguimiento del costo y la facturación.
* **Clúster de Service Fabric como recurso de Azure** Un clúster de Service Fabric es un recurso de ARM, por tanto, puede ajustarlo como hace con otros recursos de ARM en Azure.
* **Integración con la infraestructura de Azure** Service Fabric se coordina con hello subyacente infraestructura de Azure para el sistema operativo, red y otras actualizaciones tooimprove disponibilidad y confiabilidad de las aplicaciones.  
* **Diagnósticos:** en Azure se proporciona la integración con Diagnósticos y Log Analytics de Azure.
* **La escala automática:** para los clústeres en Azure, es proporcionar una funcionalidad integrada de escalado automático debido a conjuntos de escalas de máquina tooVirtual. En otros entornos de nube y local, tendrá toobuild su propia función o escala manualmente mediante hello las API que expone Service Fabric para escalar los clústeres de escalado automático.

## <a name="next-steps"></a>Pasos siguientes

* Creación de un clúster en máquinas virtuales o equipos que ejecutan Windows Server: [Creación y administración de un clúster que se ejecute en Windows Server](service-fabric-cluster-creation-for-windows-server.md)
* Creación de un clúster en máquinas virtuales o equipos que ejecutan Linux: [Service Fabric en Linux](service-fabric-linux-overview.md)
* Más información sobre las [opciones de soporte técnico de Service Fabric](service-fabric-support.md)

