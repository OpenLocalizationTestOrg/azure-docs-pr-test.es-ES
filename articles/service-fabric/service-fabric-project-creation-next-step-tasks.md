---
title: "Pasos siguientes de la creación del proyecto de Service Fabric | Microsoft Docs"
description: "Este artículo contiene vínculos a un conjunto de tareas básicas de desarrollo para Service Fabric"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 74019850c507902d9ef7ec47a364fff234aaf32b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a><span data-ttu-id="90752-103">Su aplicación de Service Fabric y próximos pasos</span><span class="sxs-lookup"><span data-stu-id="90752-103">Your Service Fabric application and next steps</span></span>
<span data-ttu-id="90752-104">La aplicación Azure Service Fabric se ha creado.</span><span class="sxs-lookup"><span data-stu-id="90752-104">Your Azure Service Fabric application has been created.</span></span> <span data-ttu-id="90752-105">En este artículo se describe la preparación del proyecto y algunos posibles pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="90752-105">This article describes the makeup of your project and some potential next steps.</span></span>

## <a name="your-application"></a><span data-ttu-id="90752-106">Su aplicación</span><span class="sxs-lookup"><span data-stu-id="90752-106">Your application</span></span>
<span data-ttu-id="90752-107">Cada nueva aplicación incluye un proyecto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="90752-107">Every new application includes an application project.</span></span> <span data-ttu-id="90752-108">Puede haber uno o dos proyectos adicionales según el tipo de servicio elegido.</span><span class="sxs-lookup"><span data-stu-id="90752-108">There may be one or two additional projects, depending on the type of service chosen.</span></span>

### <a name="the-application-project"></a><span data-ttu-id="90752-109">El proyecto de aplicación</span><span class="sxs-lookup"><span data-stu-id="90752-109">The application project</span></span>
<span data-ttu-id="90752-110">El proyecto de aplicación consiste en:</span><span class="sxs-lookup"><span data-stu-id="90752-110">The application project consists of:</span></span>

* <span data-ttu-id="90752-111">Un conjunto de referencias a los servicios que conforman la aplicación.</span><span class="sxs-lookup"><span data-stu-id="90752-111">A set of references to the services that make up your application.</span></span>
* <span data-ttu-id="90752-112">Tres perfiles de publicación (1 nodo local, 5 nodos local y en la nube) que puede usar para conservar las preferencias para trabajar con entornos diferentes, tales como las preferencias relacionadas con un punto de conexión de clúster y si va a realizar implementaciones de actualización de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="90752-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use to maintain preferences for working with different environments--such as preferences related to a cluster endpoint and whether to perform upgrade deployments by default.</span></span>
* <span data-ttu-id="90752-113">Tres archivos de parámetro de aplicación (los mismos que se indican anteriormente) que puede usar para mantener configuraciones de aplicaciones específicas del entorno, como el número de particiones para crear un servicio.</span><span class="sxs-lookup"><span data-stu-id="90752-113">Three application parameter files (same as above) that you can use to maintain environment-specific application configurations, such as the number of partitions to create for a service.</span></span>
* <span data-ttu-id="90752-114">Un script de implementación que puede usar para implementar la aplicación desde la línea de comandos o como parte de una canalización de integración e implementación continua automatizada.</span><span class="sxs-lookup"><span data-stu-id="90752-114">A deployment script that you can use to deploy your application from the command line or as part of an automated continuous integration and deployment pipeline.</span></span>
* <span data-ttu-id="90752-115">El manifiesto de aplicación que describe la aplicación.</span><span class="sxs-lookup"><span data-stu-id="90752-115">The application manifest, which describes the application.</span></span> <span data-ttu-id="90752-116">Puede encontrar el manifiesto en la carpeta ApplicationPackageRoot.</span><span class="sxs-lookup"><span data-stu-id="90752-116">You can find the manifest under the ApplicationPackageRoot folder.</span></span>

### <a name="stateless-service"></a><span data-ttu-id="90752-117">Servicio sin estado</span><span class="sxs-lookup"><span data-stu-id="90752-117">Stateless service</span></span>
<span data-ttu-id="90752-118">Cuando se agrega un nuevo servicio sin estado, Visual Studio agrega un proyecto de servicio a la solución que incluye un tipo que se hereda de `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="90752-118">When you add a new stateless service, Visual Studio adds a service project to your solution that includes a type descended from `StatelessService`.</span></span> <span data-ttu-id="90752-119">El servicio incrementa una variable local en un contador.</span><span class="sxs-lookup"><span data-stu-id="90752-119">The service increments a local variable in a counter.</span></span>

### <a name="stateful-service"></a><span data-ttu-id="90752-120">Servicio con estado</span><span class="sxs-lookup"><span data-stu-id="90752-120">Stateful service</span></span>
<span data-ttu-id="90752-121">Cuando se agrega un nuevo servicio con estado, Visual Studio agrega un proyecto de servicio a la solución que incluye un tipo que se hereda de `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="90752-121">When you add a new stateful service, Visual Studio adds a service project to your solution that includes a type descended from `StatefulService`.</span></span> <span data-ttu-id="90752-122">El servicio incrementa un contador en su método `RunAsync` y almacena el resultado en una clase `ReliableDictionary`.</span><span class="sxs-lookup"><span data-stu-id="90752-122">The service increments a counter in its `RunAsync` method and stores the result in a `ReliableDictionary`.</span></span>

### <a name="actor-service"></a><span data-ttu-id="90752-123">Servicio de actor</span><span class="sxs-lookup"><span data-stu-id="90752-123">Actor service</span></span>
<span data-ttu-id="90752-124">Cuando se agrega una nueva instancia de Reliable Actors, Visual Studio agrega dos proyectos a la solución: un proyecto de actor y un proyecto de interfaz.</span><span class="sxs-lookup"><span data-stu-id="90752-124">When you add a new reliable actor, Visual Studio adds two projects to your solution: an actor project and an interface project.</span></span>

<span data-ttu-id="90752-125">El proyecto de actor proporciona métodos para configurar y obtener el valor de un contador que se conserva de forma confiable dentro de estado del actor.</span><span class="sxs-lookup"><span data-stu-id="90752-125">The actor project provides methods for setting and getting the value of a counter that is reliably persisted within the actor's state.</span></span> <span data-ttu-id="90752-126">El proyecto de interfaz proporciona una interfaz que pueden usar otros servicios para invocar al actor.</span><span class="sxs-lookup"><span data-stu-id="90752-126">The interface project provides an interface that other services can use to invoke the actor.</span></span>

### <a name="stateless-web-api"></a><span data-ttu-id="90752-127">API web sin estado</span><span class="sxs-lookup"><span data-stu-id="90752-127">Stateless Web API</span></span>
<span data-ttu-id="90752-128">El proyecto de API web sin estado proporciona un servicio web básico que puede usar para abrir la aplicación en clientes externos.</span><span class="sxs-lookup"><span data-stu-id="90752-128">The stateless Web API project provides a basic web service that you can use to open your application to external clients.</span></span> <span data-ttu-id="90752-129">Para más información sobre cómo ver el proyecto estructurado, consulte [Introducción a los servicios de la API web de Microsoft Azure Service Fabric con autohospedaje OWIN](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="90752-129">For more information about how the project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span></span>


### <a name="aspnet-core"></a><span data-ttu-id="90752-130">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="90752-130">ASP.NET core</span></span>
<span data-ttu-id="90752-131">El SDK de Service Fabric ofrece el mismo conjunto de plantillas de ASP.NET Core que las disponibles para los proyectos independientes de ASP.NET Core: una vacía, una de [API web][aspnet-webapi] y una de [aplicación web][aspnet-webapp].</span><span class="sxs-lookup"><span data-stu-id="90752-131">The Service Fabric SDK provides the same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span></span>

### <a name="guest-executables-and-guest-containers"></a><span data-ttu-id="90752-132">Ejecutables y contenedores de invitado</span><span class="sxs-lookup"><span data-stu-id="90752-132">Guest executables and guest containers</span></span>

<span data-ttu-id="90752-133">Un invitado (guest) de Service Fabric es un servicio que no se compila con los modelos de programación de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="90752-133">A Service Fabric 'guest' is a service that is not built with the platform's programming models.</span></span> <span data-ttu-id="90752-134">Puede empaquetar los archivos binarios para un invitado [directamente en el paquete de aplicación](service-fabric-deploy-existing-app.md) o [a través de una imagen de contenedor](service-fabric-deploy-container.md).</span><span class="sxs-lookup"><span data-stu-id="90752-134">You can package the binaries for a guest either [directly in the application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span></span> <span data-ttu-id="90752-135">En ambos casos, Visual Studio crea los artefactos necesarios en la carpeta **ApplicationPackageRoot** del proyecto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="90752-135">In both cases, Visual Studio creates the necessary artifacts in the **ApplicationPackageRoot** folder of the application project.</span></span> <span data-ttu-id="90752-136">Visual Studio no creará un proyecto de servicio porque el código ya existe en otra parte.</span><span class="sxs-lookup"><span data-stu-id="90752-136">Visual Studio will not create a new service project because the code already exists elsewhere.</span></span> <span data-ttu-id="90752-137">Si desea administrar los proyectos de invitado junto con el proyecto de aplicación de Service Fabric, puede agregarlos a la misma solución de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="90752-137">If you would like to manage your guest projects alongside the Service Fabric application project, you can add them to the same Visual Studio solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90752-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="90752-138">Next steps</span></span>
### <a name="create-an-azure-cluster"></a><span data-ttu-id="90752-139">Creación de un clúster de Azure</span><span class="sxs-lookup"><span data-stu-id="90752-139">Create an Azure cluster</span></span>
<span data-ttu-id="90752-140">El SDK de Service Fabric proporciona un clúster local para desarrollo y pruebas.</span><span class="sxs-lookup"><span data-stu-id="90752-140">The Service Fabric SDK provides a local cluster for development and testing.</span></span> <span data-ttu-id="90752-141">Para crear un clúster en Azure, consulte el artículo sobre la [configuración de un clúster de Service Fabric en Azure mediante Azure Portal][create-cluster-in-portal].</span><span class="sxs-lookup"><span data-stu-id="90752-141">To create a cluster in Azure, see [Setting up a Service Fabric cluster from the Azure portal][create-cluster-in-portal].</span></span>

### <a name="publish-your-application-to-azure"></a><span data-ttu-id="90752-142">Publicación de su aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="90752-142">Publish your application to Azure</span></span>
<span data-ttu-id="90752-143">Puede publicar su aplicación directamente desde Visual Studio a un clúster de Azure.</span><span class="sxs-lookup"><span data-stu-id="90752-143">You can publish your application directly from Visual Studio to an Azure cluster.</span></span> <span data-ttu-id="90752-144">Para aprender cómo hacerlo, consulte el artículo sobre la [publicación de la aplicación en Azure][publish-app-to-azure].</span><span class="sxs-lookup"><span data-stu-id="90752-144">To learn how, see [Publishing your application to Azure][publish-app-to-azure].</span></span>

### <a name="use-service-fabric-explorer-to-visualize-your-cluster"></a><span data-ttu-id="90752-145">Uso del explorador de Service Fabric para visualizar el clúster</span><span class="sxs-lookup"><span data-stu-id="90752-145">Use Service Fabric Explorer to visualize your cluster</span></span>
<span data-ttu-id="90752-146">El Explorador de Service Fabric ofrece una forma sencilla de visualizar el clúster, como las aplicaciones implementadas y el diseño físico.</span><span class="sxs-lookup"><span data-stu-id="90752-146">Service Fabric Explorer offers an easy way to visualize your cluster, including deployed applications and physical layout.</span></span> <span data-ttu-id="90752-147">Para aprender más, consulte el artículo sobre la [visualización del clúster mediante el Explorador de Service Fabric][visualize-with-sfx].</span><span class="sxs-lookup"><span data-stu-id="90752-147">To learn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span></span>

### <a name="version-and-upgrade-your-services"></a><span data-ttu-id="90752-148">Control de versiones y actualización de los servicios</span><span class="sxs-lookup"><span data-stu-id="90752-148">Version and upgrade your services</span></span>
<span data-ttu-id="90752-149">Service Fabric permite el control de versiones independiente y la actualización de servicios independientes en una aplicación.</span><span class="sxs-lookup"><span data-stu-id="90752-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span></span> <span data-ttu-id="90752-150">Para aprender más, consulte el artículo sobre el [Control de versiones y la actualización de los servicios][app-upgrade-tutorial].</span><span class="sxs-lookup"><span data-stu-id="90752-150">To learn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span></span>

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a><span data-ttu-id="90752-151">Configuración de la integración continua con Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="90752-151">Configure continuous integration with Visual Studio Team Services</span></span>
<span data-ttu-id="90752-152">Para aprender cómo puede configurar un proceso de integración continua para su aplicación de Service Fabric, consulte el artículo sobre la [configuración de la integración continua con Visual Studio Team Services][ci-with-vso].</span><span class="sxs-lookup"><span data-stu-id="90752-152">To learn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span></span>

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
