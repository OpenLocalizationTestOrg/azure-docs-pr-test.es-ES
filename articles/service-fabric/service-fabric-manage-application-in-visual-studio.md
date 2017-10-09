---
title: aaaManage sus aplicaciones en Visual Studio | Documentos de Microsoft
description: Usar Visual Studio toocreate, desarrollar, paquete, implementar y depurar los servicios y aplicaciones de Service Fabric.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a>Utilizar la escritura de toosimplify de Visual Studio y administrar las aplicaciones de Service Fabric
Puede administrar los servicios y aplicaciones de Service Fabric de Azure a través de Visual Studio. Una vez que se haya [configurar el entorno de desarrollo](service-fabric-get-started.md), puede utilizar aplicaciones de Service Fabric toocreate de Visual Studio, agregar servicios, o un paquete, registro e implementar aplicaciones en el clúster de desarrollo local.

## <a name="deploy-your-service-fabric-application"></a>Implementar la aplicación de Service Fabric
De forma predeterminada, implementar una aplicación combina Hola siguiendo los pasos en una operación sencilla:

1. Crear paquete de aplicación Hola
2. Almacén de imágenes de toohello de paquete de aplicación de carga Hola
3. Registrar el tipo de aplicación Hola
4. Eliminación de cualquier instancia de aplicación en ejecución
5. Creación de una instancia de aplicación

En Visual Studio, al presionar **F5** implementa la aplicación y adjuntar a instancias de la aplicación hello depurador tooall. Puede usar **CTRL+F5** toodeploy una aplicación sin depurar o puede publicar tooa local o remota de clúster mediante el uso de hello perfil de publicación. Para obtener más información, consulte [publicar un clúster remoto tooa de aplicación mediante Visual Studio](service-fabric-publish-app-remote-cluster.md).

### <a name="application-debug-mode"></a>Application Debug Mode
Visual Studio proporciona una propiedad denominada **modo de depuración de la aplicación**, que controla cómo desea que la implementación de aplicaciones de Visual Studio toohandle como parte de la depuración.

#### <a name="tooset-hello-application-debug-mode-property"></a>Hola tooset propiedad modo de depuración de la aplicación
1. En hello Service Fabric aplicación del proyecto (*.sfproj) menú contextual, elija **propiedades** (o presione hello **F4** clave).
2. Hola **propiedades** (ventana), conjunto hello **modo de depuración de la aplicación** propiedad.

![Establecer la propiedad Application Debug Mode][debugmodeproperty]

#### <a name="application-debug-modes"></a>Modos de depuración de la aplicación

1. **Actualizar aplicación** este modo le permite cambiar de tooquickly y depurar su código y permite editar archivos web estáticos durante la depuración. Este modo solo funciona si el clúster de desarrollo local está en [modo 1 nodo](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).
2. **Quitar aplicación** causas Hola toobe de aplicación que se eliminan cuando finaliza la sesión de depuración de Hola.
3. **Actualizarán automáticamente** aplicación hello continúa toorun cuando finaliza la sesión de depuración de Hola. Hello siguiente sesión de depuración tratará implementación hello como una actualización. proceso de actualización de Hello conserva los datos que insertó en la sesión de depuración anterior.
4. **Mantener aplicaciones** Hola aplicación mantiene ejecutando en el clúster de hello cuando hello finaliza la sesión de depuración. Hola principio de hello siguiente sesión de depuración, se quitará la aplicación hello.

Para **actualización automática** se conservan los datos mediante la aplicación de capacidades de actualización de aplicación Hola de Service Fabric. Para obtener más información sobre la actualización de aplicaciones y cómo se realiza una actualización en un entorno real, consulte [Actualización de la aplicación de Service Fabric](service-fabric-application-upgrade.md).

## <a name="add-a-service-tooyour-service-fabric-application"></a>Agregar una aplicación de Service Fabric tooyour de servicio
Puede agregar nuevos servicios tooyour aplicación tooextend su funcionalidad.  tooensure que el servicio de hello está incluido en el paquete de aplicación, agregue el servicio de Hola a través de hello **nuevo servicio de Fabric...**  elemento de menú.

![Agregar un nuevo servicio de Service Fabric][newservice]

Seleccione una aplicación de tooyour Service Fabric tooadd de tipo de proyecto y especifique un nombre para el servicio de Hola.  Vea [elegir un marco de trabajo para el servicio](service-fabric-choose-framework.md) toohelp decidir qué servicio escriba toouse.

![Seleccione una aplicación Service Fabric servicio proyecto tipo tooadd tooyour][addserviceproject]

se agrega nuevo servicio de Hello tooyour solución y paquete de aplicación existente. Hola referencias de servicio y una instancia predeterminada del servicio será toohello agregado manifiesto de aplicación, lo que ha provocado Hola servicio toobe crea e inicia Hola vuela a que implementar la aplicación hello.

![nuevo servicio de Hola se agrega el manifiesto de aplicación tooyour][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a>Empaquetar la aplicación de Service Fabric
aplicación de hello toodeploy y su clúster de tooa de servicios, deberá toocreate un paquete de aplicación.  paquete de Hello organiza manifiesto de aplicación Hola, manifiestos de servicio y otros archivos necesarios en un diseño concreto.  Visual Studio configura y administra el paquete de hello en la carpeta del proyecto de aplicación de hello, en el directorio de hello 'pkg'.  Haga clic en **paquete** de hello **aplicación** crea el menú contextual o actualizaciones Hola paquete de aplicación.

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a>Eliminación de aplicaciones y tipos de aplicación mediante Cloud Explorer
Puede realizar operaciones de administración de clúster básico desde Visual Studio mediante el explorador en la nube, que también se puede iniciar desde hello **vista** menú. Por ejemplo, puede eliminar aplicaciones y deshacer el aprovisionamiento de tipos de aplicación en clústeres locales o remotos.

![Eliminación de una aplicación][removeapplication]

> [!TIP]
> Para obtener una mejor funcionalidad de administración de clúster, consulte [Visualización del clúster mediante Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Pasos siguientes
* [Modelo de aplicación de Service Fabric](service-fabric-application-model.md)
* [Implementación de la aplicación de Service Fabric](service-fabric-deploy-remove-applications.md)
* [Administración de los parámetros de la aplicación en varios entornos](service-fabric-manage-multiple-environment-app-configuration.md)
* [Depuración de la aplicación de Service Fabric](service-fabric-debugging-your-application.md)
* [Visualización del clúster mediante el Explorador de Service Fabric](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png