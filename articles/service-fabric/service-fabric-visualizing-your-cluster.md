---
title: "aaaVisualizing su clúster mediante el Explorador de Service Fabric | Documentos de Microsoft"
description: "El Explorador de Service Fabric es una herramienta basada en web para inspeccionar y administrar aplicaciones y nodos en la nube en un clúster de Service Fabric de Microsoft Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a>Visualización del clúster mediante el Explorador de Service Fabric
El Explorador de Service Fabric es una herramienta web para inspeccionar y administrar aplicaciones y nodos en un clúster de Azure Service Fabric. Explorador de Service Fabric se hospeda directamente en clúster de hello, por lo que siempre está disponible, independientemente de donde se está ejecutando el clúster.

## <a name="video-tutorial"></a>Tutorial en vídeo

toolearn cómo ver toouse Service Fabric Explorer Hola después de vídeo Microsoft Virtual Academy:

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a>Conectar tooService Fabric Explorer
Si ha seguido las instrucciones de hello demasiado[preparar el entorno de desarrollo](service-fabric-get-started.md), puede iniciar el Explorador de Service Fabric en el clúster local desplazándose toohttp://localhost:19080 / explorador.

## <a name="understand-hello-service-fabric-explorer-layout"></a>Entender el diseño del explorador de Service Fabric Hola
Puede navegar a través del explorador de Service Fabric mediante árbol Hola Hola izquierda. En raíz de Hola de árbol de hello, panel de clúster de hello proporciona información general del clúster, incluido un resumen de la aplicación y el estado de nodo.

![Panel de clúster del Explorador de Service Fabric][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a>Ver el diseño del clúster de Hola
Los nodos de un clúster de Service Fabric se colocan en una cuadrícula bidimensional de dominios de error y dominios de actualización. Esta ubicación se asegura de que las aplicaciones siguen estando disponibles en presencia de Hola de errores de hardware y las actualizaciones de aplicaciones. Puede ver cómo se diseña el clúster actual hello mediante el mapa de clúster de Hola.

![Mapa de clúster del Explorador de Service Fabric][sfx-cluster-map]

### <a name="view-applications-and-services"></a>Visualización de aplicaciones y servicios
clúster de Hello contiene dos subárboles: uno para las aplicaciones y otro para los nodos.

Puede utilizar toonavigate de vista de aplicación Hola a través de la jerarquía lógica de Service Fabric: las aplicaciones, servicios, particiones y réplicas.

En el siguiente ejemplo de Hola, Hola aplicación **MyApp** consta de dos servicios, **MyStatefulService** y **WebService**. Como **MyStatefulService** es un servicio con estado, incluye una partición con una réplica principal y dos réplicas secundarias. Por el contrario, el servicio WebSvcService no tiene estado y contiene una única instancia.

![Vista de aplicación del explorador de Service Fabric][sfx-application-tree]

En cada nivel del árbol de hello, panel principal hello muestra la información pertinente sobre elemento Hola. Por ejemplo, puede ver el estado de mantenimiento de Hola y la versión para un servicio determinado.

![Panel Essentials del explorador de Service Fabric][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a>Ver los nodos del clúster de Hola
vista de nodo de Hello muestra el diseño físico de Hola de clúster de Hola. Para un nodo determinado, puede comprobar qué aplicaciones tienen el código implementado en ese nodo. Más específicamente, puede ver qué réplicas están en ejecución.

## <a name="actions"></a>Acciones
Explorador de Service Fabric ofrece una forma rápida tooinvoke acciones en nodos, aplicaciones y servicios en el clúster.

Por ejemplo, toodelete una instancia de la aplicación, elija aplicación hello de árbol de Hola Hola izquierda y, a continuación, elija **acciones** > **eliminar una aplicación**.

![Eliminación de una aplicación en el explorador de Service Fabric][sfx-delete-application]

> [!TIP]
> Puede realizar Hola mismas acciones, haga clic en siguiente tooeach elemento de hello puntos suspensivos.
>
>

Hello tabla siguiente enumeran las acciones de hello disponibles para cada entidad:

| **Entidad** | **Acción** | **Descripción** |
| --- | --- | --- |
| Tipo de aplicación |Tipo de anulación de aprovisionamiento |Quita el paquete de aplicación Hola del clúster de hello almacén de imágenes. Requiere que todas las aplicaciones de ese toobe tipo quitado primero. |
| Application |Eliminar aplicación |Eliminar aplicación hello, incluidos todos sus servicios y su estado (si existe). |
| Servicio |Eliminar servicio |Eliminar servicio hello y su estado (si existe). |
| Nodo |Activar |Activación del nodo de Hola. |
| Nodo | Desactivar (pausa) | Pausar el nodo de hello en su estado actual. Servicios seguirán toorun pero Service Fabric no proactivamente mover nada en o desactivar, a menos que sea necesario tooprevent una interrupción o incoherencia en los datos. Esta acción es tooenable normalmente se usan los servicios en un tooensure de nodo específico que no se mueven durante la inspección de depuración. | |
| Nodo | Desactivar (reiniciar) | Saque todos los servicios de la memoria de un nodo y cierre los servicios persistentes de forma segura. Se utiliza normalmente cuando los procesos de host de Hola o máquina necesidad toobe reinicia. | |
| Nodo | Desactivar (quitar datos) | Cerrar todos los servicios que se ejecutan en el nodo de hello después de la creación de réplicas de reserva suficiente. Se utiliza normalmente cuando un nodo (o al menos su almacenamiento) se está sacando permanentemente de circulación. | |
| Nodo | Quitar el estado del nodo | Quitar información de réplicas de un nodo de clúster de Hola. Se utiliza normalmente cuando un nodo con error ya se considera irrecuperable. | |
| Nodo | Reiniciar | Simular un error de nodo, reinicie el nodo de Hola. Puede encontrar más información [aquí](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps) | |

Puesto que muchas acciones son destructivas, es posible que más frecuentes tooconfirm su intención antes de que finalice la acción de Hola.

> [!TIP]
> Todas las acciones que pueden realizarse a través del explorador de Service Fabric también pueden realizarse a través de PowerShell o una API de REST, tooenable automatización.
>
>

También puede utilizar instancias de la aplicación de explorador de Service Fabric toocreate para un tipo de aplicación determinada y la versión. Elija el tipo de aplicación de hello en la vista de árbol de hello, haga clic en hello **crear instancia de aplicación** versión toohello siguiente vínculo que se desea en el panel derecho de Hola.

![Creación de una instancia de aplicación en Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> En la actualidad, no se pueden parametrizar las instancias de aplicaciones creadas mediante Service Fabric Explorer. Se crean utilizando los valores de parámetros predeterminados.
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a>Conectar el clúster de tejido de servicio remoto tooa
Si conoce el punto de conexión del clúster de Hola y tiene los permisos necesarios pueden tener acceso a Service Fabric Explorer desde cualquier explorador. Esto es porque el Explorador de Service Fabric es simplemente otro servicio que se ejecuta en el clúster de Hola.

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a>Detectar extremo de Service Fabric Explorer Hola para un clúster remoto
tooreach Service Fabric Explorer para un clúster determinado, seleccione el explorador para:

http://&lt;su-punto-de-conexión-de-clúster&gt;:19080/Explorer

Para los clústeres de Azure, dirección URL completa de hello también está disponible en el panel de essentials de clúster Hola de hello portal de Azure.

### <a name="connect-tooa-secure-cluster"></a>Conectar el clúster segura tooa
Puede controlar el clúster de Service Fabric de tooyour de cliente acceso con certificados o usar Azure Active Directory (AAD).

Si intentas tooconnect tooService Fabric Explorer en un clúster de seguro, a continuación, dependiendo de la configuración del clúster de hello podrá ser toopresent requiere un certificado de cliente o inicie sesión con AAD.

## <a name="next-steps"></a>Pasos siguientes
* [Información general sobre Testability](service-fabric-testability-overview.md)
* [Administración de aplicaciones de Service Fabric en Visual Studio](service-fabric-manage-application-in-visual-studio.md)
* [Implementación de aplicaciones de Service Fabric con PowerShell](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
