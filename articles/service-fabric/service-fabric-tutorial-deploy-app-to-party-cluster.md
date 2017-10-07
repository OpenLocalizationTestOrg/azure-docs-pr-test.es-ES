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
# <a name="deploy-an-application-tooa-party-cluster-in-azure"></a><span data-ttu-id="408ed-103">Implementar un clúster de entidad en Azure tooa de aplicación</span><span class="sxs-lookup"><span data-stu-id="408ed-103">Deploy an application tooa Party Cluster in Azure</span></span>
<span data-ttu-id="408ed-104">Este tutorial forma parte de una serie y muestra cómo toodeploy una tooa de aplicación de Azure Service Fabric clúster de entidad en Azure.</span><span class="sxs-lookup"><span data-stu-id="408ed-104">This tutorial is part two of a series and shows you how toodeploy an Azure Service Fabric application tooa Party Cluster in Azure.</span></span>

<span data-ttu-id="408ed-105">En la segunda parte de la serie de tutoriales de hello, aprenderá cómo:</span><span class="sxs-lookup"><span data-stu-id="408ed-105">In part two of hello tutorial series, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="408ed-106">Implementar un clúster remoto de tooa de aplicación con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="408ed-106">Deploy an application tooa remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="408ed-107">Eliminar una aplicación de un clúster mediante de Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="408ed-107">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="408ed-108">En esta serie de tutoriales, se aprende a:</span><span class="sxs-lookup"><span data-stu-id="408ed-108">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * [<span data-ttu-id="408ed-109">Crear una aplicación de .NET Service Fabric</span><span class="sxs-lookup"><span data-stu-id="408ed-109">Build a .NET Service Fabric application</span></span>](service-fabric-tutorial-create-dotnet-app.md)
> * <span data-ttu-id="408ed-110">Implementar el clúster remoto de hello aplicación tooa</span><span class="sxs-lookup"><span data-stu-id="408ed-110">Deploy hello application tooa remote cluster</span></span>
> * [<span data-ttu-id="408ed-111">Configurar CI/CD con Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="408ed-111">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="408ed-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="408ed-112">Prerequisites</span></span>
<span data-ttu-id="408ed-113">Antes de empezar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="408ed-113">Before you begin this tutorial:</span></span>
- <span data-ttu-id="408ed-114">Si no tiene ninguna suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="408ed-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="408ed-115">[Instalar Visual Studio de 2017](https://www.visualstudio.com/) e instalar hello **desarrollo Azure** y **ASP.NET y desarrollo web** las cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="408ed-115">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="408ed-116">Instalar Hola SDK del servicio de Fabric</span><span class="sxs-lookup"><span data-stu-id="408ed-116">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="download-hello-voting-sample-application"></a><span data-ttu-id="408ed-117">Descargar la aplicación de ejemplo de Hola votación</span><span class="sxs-lookup"><span data-stu-id="408ed-117">Download hello Voting sample application</span></span>
<span data-ttu-id="408ed-118">Si no se ha generado la aplicación de ejemplo de Hola votación [primera parte de esta serie de tutoriales](service-fabric-tutorial-create-dotnet-app.md), puede descargarlo.</span><span class="sxs-lookup"><span data-stu-id="408ed-118">If you did not build hello Voting sample application in [part one of this tutorial series](service-fabric-tutorial-create-dotnet-app.md), you can download it.</span></span> <span data-ttu-id="408ed-119">En una ventana de comandos, ejecute hello después comando tooclone Hola ejemplo aplicación repositorio tooyour equipo local.</span><span class="sxs-lookup"><span data-stu-id="408ed-119">In a command window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a><span data-ttu-id="408ed-120">Configuración de un clúster de entidad</span><span class="sxs-lookup"><span data-stu-id="408ed-120">Set up a Party Cluster</span></span>
<span data-ttu-id="408ed-121">Clústeres de entidades son libres, por tiempo limitado para los clústeres Service Fabric hospedado en Azure y ejecutar, equipo de Service Fabric Hola que cualquiera puede implementar aplicaciones y obtener información acerca de la plataforma de Hola.</span><span class="sxs-lookup"><span data-stu-id="408ed-121">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by hello Service Fabric team where anyone can deploy applications and learn about hello platform.</span></span> <span data-ttu-id="408ed-122">¡Gratis!</span><span class="sxs-lookup"><span data-stu-id="408ed-122">For free!</span></span>

<span data-ttu-id="408ed-123">tooget acceso tooa clúster de entidad, visite el sitio de toothis: http://aka.ms/tryservicefabric y seguir Hola instrucciones tooget tooa clúster de acceso.</span><span class="sxs-lookup"><span data-stu-id="408ed-123">tooget access tooa Party Cluster, browse toothis site: http://aka.ms/tryservicefabric and follow hello instructions tooget access tooa cluster.</span></span> <span data-ttu-id="408ed-124">Es necesario un Facebook o GitHub cuenta tooget acceso tooa clúster de entidad.</span><span class="sxs-lookup"><span data-stu-id="408ed-124">You need a Facebook or GitHub account tooget access tooa Party Cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="408ed-125">Clústeres de entidades no están protegidos, por lo que las aplicaciones y los datos que colocan en ellos pueden ser tooothers visible.</span><span class="sxs-lookup"><span data-stu-id="408ed-125">Party clusters are not secured, so your applications and any data you put in them may be visible tooothers.</span></span> <span data-ttu-id="408ed-126">No implemente cualquier cosa que no desea que los demás toosee.</span><span class="sxs-lookup"><span data-stu-id="408ed-126">Don't deploy anything you don't want others toosee.</span></span> <span data-ttu-id="408ed-127">Estar tooread seguro a través de nuestras condiciones de uso para todos los detalles de Hola.</span><span class="sxs-lookup"><span data-stu-id="408ed-127">Be sure tooread over our Terms of Use for all hello details.</span></span>

## <a name="configure-hello-listening-port"></a><span data-ttu-id="408ed-128">Configurar el puerto de escucha de Hola</span><span class="sxs-lookup"><span data-stu-id="408ed-128">Configure hello listening port</span></span>
<span data-ttu-id="408ed-129">Cuando se crea el servicio front-end VotingWeb hello, Visual Studio selecciona aleatoriamente un puerto para hello servicio toolisten en.</span><span class="sxs-lookup"><span data-stu-id="408ed-129">When hello VotingWeb front-end service is created, Visual Studio randomly selects a port for hello service toolisten on.</span></span>  <span data-ttu-id="408ed-130">Hola VotingWeb servicio actúa como front-end para esta aplicación hello y acepta el tráfico externo, así que vamos a enlazar ese tooa servicio fijada y conocer bien el puerto.</span><span class="sxs-lookup"><span data-stu-id="408ed-130">hello VotingWeb service acts as hello front-end for this application and accepts external traffic, so let's bind that service tooa fixed and well-know port.</span></span> <span data-ttu-id="408ed-131">En el Explorador de soluciones, abra *VotingWeb/PackageRoot/ServiceManifest.xml*.</span><span class="sxs-lookup"><span data-stu-id="408ed-131">In Solution Explorer, open  *VotingWeb/PackageRoot/ServiceManifest.xml*.</span></span>  <span data-ttu-id="408ed-132">Buscar hello **extremo** recursos Hola **recursos** sección y cambie hello **puerto** too80 de valor.</span><span class="sxs-lookup"><span data-stu-id="408ed-132">Find hello **Endpoint** resource in hello **Resources** section and change hello **Port** value too80.</span></span>

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

<span data-ttu-id="408ed-133">Actualizar también el valor de propiedad de dirección URL de la aplicación de hello en el proyecto de votación de Hola por lo que abre un explorador web toohello de puerto correcto al depurar utilizando 'F5'.</span><span class="sxs-lookup"><span data-stu-id="408ed-133">Also update hello Application URL property value in hello Voting project so a web browser opens toohello correct port when you debug using 'F5'.</span></span>  <span data-ttu-id="408ed-134">En el Explorador de soluciones, seleccione hello **votación** Hola de proyecto y actualice **dirección URL de la aplicación** propiedad.</span><span class="sxs-lookup"><span data-stu-id="408ed-134">In Solution Explorer, select hello **Voting** project and update hello **Application URL** property.</span></span>

![Dirección URL de la aplicación](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-hello-app-toohello-azure"></a><span data-ttu-id="408ed-136">Implementar toohello de aplicación hello Azure</span><span class="sxs-lookup"><span data-stu-id="408ed-136">Deploy hello app toohello Azure</span></span>
<span data-ttu-id="408ed-137">Ahora que la aplicación hello está listo, puede implementarlo toohello entidad clúster directamente desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="408ed-137">Now that hello application is ready, you can deploy it toohello Party Cluster direct from Visual Studio.</span></span>

1. <span data-ttu-id="408ed-138">Haga clic en **votación** en hello en el Explorador de soluciones y elija **publicar**.</span><span class="sxs-lookup"><span data-stu-id="408ed-138">Right-click **Voting** in hello Solution Explorer and choose **Publish**.</span></span>

    ![Cuadro de diálogo de publicación](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. <span data-ttu-id="408ed-140">Escriba Hola extremo de la conexión de hello entidad clúster Hola **extremo de la conexión** campo y haga clic en **publicar**.</span><span class="sxs-lookup"><span data-stu-id="408ed-140">Type in hello Connection Endpoint of hello Party Cluster in hello **Connection Endpoint** field and click **Publish**.</span></span>

    <span data-ttu-id="408ed-141">Una vez que publique hello tiene terminado, debe ser capaz de toosend una aplicación de toohello de solicitud a través de un explorador.</span><span class="sxs-lookup"><span data-stu-id="408ed-141">Once hello publish has finished, you should be able toosend a request toohello application via a browser.</span></span>

3. <span data-ttu-id="408ed-142">Abra había preferida explorador y escriba en la dirección del clúster hello (extremo de conexión de hello sin información de puerto hello: por ejemplo, win1kw5649s.westus.cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="408ed-142">Open you preferred browser and type in hello cluster address (hello connection endpoint without hello port information - for example, win1kw5649s.westus.cloudapp.azure.com).</span></span>

    <span data-ttu-id="408ed-143">Ahora debería ver Hola el mismo resultado que vio cuando se ejecuta la aplicación hello localmente.</span><span class="sxs-lookup"><span data-stu-id="408ed-143">You should now see hello same result as you saw when running hello application locally.</span></span>

    ![Respuesta de API desde el clúster](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-hello-application-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="408ed-145">Quitar aplicación hello de un clúster mediante el Explorador de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="408ed-145">Remove hello application from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="408ed-146">Explorador de Service Fabric es un tooexplore de interfaz gráfica de usuario y administrar aplicaciones en un clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="408ed-146">Service Fabric Explorer is a graphical user interface tooexplore and manage applications in a Service Fabric cluster.</span></span>

<span data-ttu-id="408ed-147">aplicación de hello tooremove de hello entidad clúster:</span><span class="sxs-lookup"><span data-stu-id="408ed-147">tooremove hello application from hello Party Cluster:</span></span>

1. <span data-ttu-id="408ed-148">Examinar toohello Service Fabric Explorer, mediante vínculo Hola proporcionada por la página de registro de clúster de la entidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="408ed-148">Browse toohello Service Fabric Explorer, using hello link provided by hello Party Cluster sign-up page.</span></span> <span data-ttu-id="408ed-149">Por ejemplo, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span><span class="sxs-lookup"><span data-stu-id="408ed-149">For example, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span></span>

2. <span data-ttu-id="408ed-150">En el Explorador de Service Fabric, navegue toohello **fabric://Voting** nodo de treeview de hello en el lado izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="408ed-150">In Service Fabric Explorer, navigate toohello **fabric://Voting** node in hello treeview on hello left-hand side.</span></span>

3. <span data-ttu-id="408ed-151">Haga clic en hello **acción** botón Hola derecho **Essentials** panel y elija **eliminar una aplicación**.</span><span class="sxs-lookup"><span data-stu-id="408ed-151">Click hello **Action** button in hello right-hand **Essentials** pane, and choose **Delete Application**.</span></span> <span data-ttu-id="408ed-152">Confirmar eliminación Hola instancia de la aplicación, lo que elimina la instancia de Hola de nuestra aplicación que se ejecuta en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="408ed-152">Confirm deleting hello application instance, which removes hello instance of our application running in hello cluster.</span></span>

![Eliminación de una aplicación en Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-hello-application-type-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="408ed-154">Quitar tipo de aplicación Hola de un clúster mediante el Explorador de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="408ed-154">Remove hello application type from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="408ed-155">Las aplicaciones se implementan como tipos de aplicaciones en un clúster de Service Fabric, lo que permite toohave varias instancias y versiones de aplicación Hola que se ejecuta en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="408ed-155">Applications are deployed as application types in a Service Fabric cluster, which enables you toohave multiple instances and versions of hello application running within hello cluster.</span></span> <span data-ttu-id="408ed-156">Una vez quitados los Hola ejecutando la instancia de nuestra aplicación, también se puede eliminar tipo hello, limpieza de hello toocomplete de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="408ed-156">After having removed hello running instance of our application, we can also remove hello type, toocomplete hello cleanup of hello deployment.</span></span>

<span data-ttu-id="408ed-157">Para obtener más información sobre el modelo de aplicación de hello en Service Fabric, vea [modelar una aplicación de Service Fabric](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="408ed-157">For more information about hello application model in Service Fabric, see [Model an application in Service Fabric](service-fabric-application-model.md).</span></span>

1. <span data-ttu-id="408ed-158">Navegue toohello **VotingType** nodo de treeview Hola.</span><span class="sxs-lookup"><span data-stu-id="408ed-158">Navigate toohello **VotingType** node in hello treeview.</span></span>

2. <span data-ttu-id="408ed-159">Haga clic en hello **acción** botón Hola derecho **Essentials** panel y elija **anule tipo**.</span><span class="sxs-lookup"><span data-stu-id="408ed-159">Click hello **Action** button in hello right-hand **Essentials** pane, and choose **Unprovision Type**.</span></span> <span data-ttu-id="408ed-160">Confirme el tipo de aplicación Hola eliminando el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="408ed-160">Confirm unprovisioning hello application type.</span></span>

![Deshacer el aprovisionamiento del tipo de aplicación en Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

<span data-ttu-id="408ed-162">Esto concluye el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="408ed-162">This concludes hello tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="408ed-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="408ed-163">Next steps</span></span>
<span data-ttu-id="408ed-164">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="408ed-164">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="408ed-165">Implementar un clúster remoto de tooa de aplicación con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="408ed-165">Deploy an application tooa remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="408ed-166">Eliminar una aplicación de un clúster mediante de Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="408ed-166">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="408ed-167">Tutorial de antemano toohello siguiente:</span><span class="sxs-lookup"><span data-stu-id="408ed-167">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="408ed-168">Configurar la integración continua con Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="408ed-168">Set up continuous integration using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)