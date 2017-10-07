---
title: "aaaDeploy una tooa de aplicación de Azure Service Fabric clúster entidad | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy una tooa de aplicación parte del clúster."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: db16b6418fa2533ed915c8b6e612b7a8e7311bed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-party-cluster-in-azure"></a>Implementar un clúster de entidad en Azure tooa de aplicación
Este tutorial forma parte de una serie y muestra cómo toodeploy una tooa de aplicación de Azure Service Fabric clúster de entidad en Azure.

En la segunda parte de la serie de tutoriales de hello, aprenderá cómo:
> [!div class="checklist"]
> * Implementar un clúster remoto de tooa de aplicación con Visual Studio
> * Eliminar una aplicación de un clúster mediante de Service Fabric Explorer

En esta serie de tutoriales, se aprende a:
> [!div class="checklist"]
> * [Crear una aplicación de .NET Service Fabric](service-fabric-tutorial-create-dotnet-app.md)
> * Implementar el clúster remoto de hello aplicación tooa
> * [Configurar CI/CD con Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>Requisitos previos
Antes de empezar este tutorial:
- Si no tiene ninguna suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- [Instalar Visual Studio de 2017](https://www.visualstudio.com/) e instalar hello **desarrollo Azure** y **ASP.NET y desarrollo web** las cargas de trabajo.
- [Instalar Hola SDK del servicio de Fabric](service-fabric-get-started.md)

## <a name="download-hello-voting-sample-application"></a>Descargar la aplicación de ejemplo de Hola votación
Si no se ha generado la aplicación de ejemplo de Hola votación [primera parte de esta serie de tutoriales](service-fabric-tutorial-create-dotnet-app.md), puede descargarlo. En una ventana de comandos, ejecute hello después comando tooclone Hola ejemplo aplicación repositorio tooyour equipo local.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a>Configuración de un clúster de entidad
Clústeres de entidades son libres, por tiempo limitado para los clústeres Service Fabric hospedado en Azure y ejecutar, equipo de Service Fabric Hola que cualquiera puede implementar aplicaciones y obtener información acerca de la plataforma de Hola. ¡Gratis!

tooget acceso tooa clúster de entidad, visite el sitio de toothis: http://aka.ms/tryservicefabric y seguir Hola instrucciones tooget tooa clúster de acceso. Es necesario un Facebook o GitHub cuenta tooget acceso tooa clúster de entidad.

> [!NOTE]
> Clústeres de entidades no están protegidos, por lo que las aplicaciones y los datos que colocan en ellos pueden ser tooothers visible. No implemente cualquier cosa que no desea que los demás toosee. Estar tooread seguro a través de nuestras condiciones de uso para todos los detalles de Hola.

## <a name="configure-hello-listening-port"></a>Configurar el puerto de escucha de Hola
Cuando se crea el servicio front-end VotingWeb hello, Visual Studio selecciona aleatoriamente un puerto para hello servicio toolisten en.  Hola VotingWeb servicio actúa como front-end para esta aplicación hello y acepta el tráfico externo, así que vamos a enlazar ese tooa servicio fijada y conocer bien el puerto. En el Explorador de soluciones, abra *VotingWeb/PackageRoot/ServiceManifest.xml*.  Buscar hello **extremo** recursos Hola **recursos** sección y cambie hello **puerto** too80 de valor.

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

Actualizar también el valor de propiedad de dirección URL de la aplicación de hello en el proyecto de votación de Hola por lo que abre un explorador web toohello de puerto correcto al depurar utilizando 'F5'.  En el Explorador de soluciones, seleccione hello **votación** Hola de proyecto y actualice **dirección URL de la aplicación** propiedad.

![Dirección URL de la aplicación](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-hello-app-toohello-azure"></a>Implementar toohello de aplicación hello Azure
Ahora que la aplicación hello está listo, puede implementarlo toohello entidad clúster directamente desde Visual Studio.

1. Haga clic en **votación** en hello en el Explorador de soluciones y elija **publicar**.

    ![Cuadro de diálogo de publicación](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. Escriba Hola extremo de la conexión de hello entidad clúster Hola **extremo de la conexión** campo y haga clic en **publicar**.

    Una vez que publique hello tiene terminado, debe ser capaz de toosend una aplicación de toohello de solicitud a través de un explorador.

3. Abra había preferida explorador y escriba en la dirección del clúster hello (extremo de conexión de hello sin información de puerto hello: por ejemplo, win1kw5649s.westus.cloudapp.azure.com).

    Ahora debería ver Hola el mismo resultado que vio cuando se ejecuta la aplicación hello localmente.

    ![Respuesta de API desde el clúster](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-hello-application-from-a-cluster-using-service-fabric-explorer"></a>Quitar aplicación hello de un clúster mediante el Explorador de Service Fabric
Explorador de Service Fabric es un tooexplore de interfaz gráfica de usuario y administrar aplicaciones en un clúster de Service Fabric.

aplicación de hello tooremove de hello entidad clúster:

1. Examinar toohello Service Fabric Explorer, mediante vínculo Hola proporcionada por la página de registro de clúster de la entidad de Hola. Por ejemplo, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.

2. En el Explorador de Service Fabric, navegue toohello **fabric://Voting** nodo de treeview de hello en el lado izquierdo de Hola.

3. Haga clic en hello **acción** botón Hola derecho **Essentials** panel y elija **eliminar una aplicación**. Confirmar eliminación Hola instancia de la aplicación, lo que elimina la instancia de Hola de nuestra aplicación que se ejecuta en el clúster de Hola.

![Eliminación de una aplicación en Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-hello-application-type-from-a-cluster-using-service-fabric-explorer"></a>Quitar tipo de aplicación Hola de un clúster mediante el Explorador de Service Fabric
Las aplicaciones se implementan como tipos de aplicaciones en un clúster de Service Fabric, lo que permite toohave varias instancias y versiones de aplicación Hola que se ejecuta en el clúster de Hola. Una vez quitados los Hola ejecutando la instancia de nuestra aplicación, también se puede eliminar tipo hello, limpieza de hello toocomplete de implementación de Hola.

Para obtener más información sobre el modelo de aplicación de hello en Service Fabric, vea [modelar una aplicación de Service Fabric](service-fabric-application-model.md).

1. Navegue toohello **VotingType** nodo de treeview Hola.

2. Haga clic en hello **acción** botón Hola derecho **Essentials** panel y elija **anule tipo**. Confirme el tipo de aplicación Hola eliminando el aprovisionamiento.

![Deshacer el aprovisionamiento del tipo de aplicación en Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

Esto concluye el tutorial Hola.

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo:

> [!div class="checklist"]
> * Implementar un clúster remoto de tooa de aplicación con Visual Studio
> * Eliminar una aplicación de un clúster mediante de Service Fabric Explorer

Tutorial de antemano toohello siguiente:
> [!div class="nextstepaction"]
> [Configurar la integración continua con Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)