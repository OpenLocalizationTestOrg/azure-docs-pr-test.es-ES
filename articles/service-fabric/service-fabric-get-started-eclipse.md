---
title: aaaAzure Service Fabric complemento para Eclipse | Documentos de Microsoft
description: Empezar a trabajar con hello Service Fabric complemento para Eclipse.
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="c0e31-103">Complemento de Service Fabric para el desarrollo de aplicaciones Java de Eclipse</span><span class="sxs-lookup"><span data-stu-id="c0e31-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="c0e31-104">Eclipse es uno de hello más usada en entornos de desarrollo (IDE) de integrados para los desarrolladores de Java.</span><span class="sxs-lookup"><span data-stu-id="c0e31-104">Eclipse is one of hello most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="c0e31-105">En este artículo se describe cómo tooset seguridad su toowork del entorno de desarrollo Eclipse con Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c0e31-105">In this article, we describe how tooset up your Eclipse development environment toowork with Azure Service Fabric.</span></span> <span data-ttu-id="c0e31-106">Obtenga información acerca de cómo tooinstall Hola Service Fabric complemento, crear una aplicación de Service Fabric e implementar su Service Fabric aplicación tooa local o remoto Service Fabric clúster en Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="c0e31-106">Learn how tooinstall hello Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application tooa local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="c0e31-107">Instalar o actualizar Hola Service Fabric complemento de Eclipse Neon</span><span class="sxs-lookup"><span data-stu-id="c0e31-107">Install or update hello Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="c0e31-108">En Eclipse se puede instalar un complemento Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c0e31-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="c0e31-109">Hola complemento puede ayudar a simplificar el proceso de Hola de compilar e implementar servicios de Java.</span><span class="sxs-lookup"><span data-stu-id="c0e31-109">hello plug-in can help simplify hello process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="c0e31-110">Asegúrese de que tiene la versión más reciente de Hola de Eclipse Neon y versión más reciente de Hola de Buildship (1.0.17 o una versión posterior) instalado:</span><span class="sxs-lookup"><span data-stu-id="c0e31-110">Ensure that you have hello latest version of Eclipse Neon and hello latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="c0e31-111">versiones de hello toocheck de componentes instalados, en Eclipse Neon, vaya demasiado**ayuda** > **detalles de instalación**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-111">toocheck hello versions of installed components, in Eclipse Neon, go too**Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="c0e31-112">vea tooupdate Buildship, [Buildship Eclipse: complementos Eclipse para Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="c0e31-112">tooupdate Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="c0e31-113">toocheck para e instalar actualizaciones para Neon de Eclipse, vaya demasiado**ayuda** > **buscar actualizaciones**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-113">toocheck for and install updates for Eclipse Neon, go too**Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="c0e31-114">Hola tooinstall Service Fabric complemento Neon de Eclipse, vaya demasiado**ayuda** > **instalar nuevo Software**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-114">tooinstall hello Service Fabric plug-in, in Eclipse Neon, go too**Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="c0e31-115">Hola **trabajar con** cuadro, escriba **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-115">In hello **Work with** box, enter **http://dl.microsoft.com/eclipse**.</span></span>
  2.    <span data-ttu-id="c0e31-116">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-116">Click **Add**.</span></span>

         ![Complemento Service Fabric para Eclipse Neon][sf-eclipse-plugin-install]
  3.    <span data-ttu-id="c0e31-118">Seleccione Hola Service Fabric complemento y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-118">Select hello Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="c0e31-119">Complete los pasos de instalación de hello y, a continuación, acepte los términos de licencia del Software de Microsoft de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0e31-119">Complete hello installation steps, and then accept hello Microsoft Software License Terms.</span></span>

<span data-ttu-id="c0e31-120">Si ya tiene Hola complemento Service Fabric instalado, asegúrese de que tiene la versión más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0e31-120">If you already have hello Service Fabric plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="c0e31-121">toocheck si hay actualizaciones disponibles, vaya demasiado**ayuda** > **detalles de instalación**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-121">toocheck for available updates, go too**Help** > **Installation Details**.</span></span> <span data-ttu-id="c0e31-122">En la lista Hola de complementos instalados, seleccione Service Fabric y, a continuación, haga clic en **actualización**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-122">In hello list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="c0e31-123">Se instalarán las actualizaciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="c0e31-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="c0e31-124">Si instalar o actualizar Hola Service Fabric complemento es lenta, podría ser debido a la configuración de Eclipse tooan.</span><span class="sxs-lookup"><span data-stu-id="c0e31-124">If installing or updating hello Service Fabric plug-in is slow, it might be due tooan Eclipse setting.</span></span> <span data-ttu-id="c0e31-125">Eclipse recopila metadatos en todos los sitios de tooupdate de cambios que están registrados con la instancia de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="c0e31-125">Eclipse collects metadata on all changes tooupdate sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="c0e31-126">toospeed proceso Hola de buscar e instalar una actualización de complemento de Service Fabric, vaya demasiado**sitios de Software disponibles**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-126">toospeed up hello process of checking for and installing a Service Fabric plug-in update, go too**Available Software Sites**.</span></span> <span data-ttu-id="c0e31-127">Desactive las casillas de verificación de Hola para todos los sitios excepto Hola uno que señala la ubicación del complemento de Service Fabric toohello (http://dl.microsoft.com/eclipse/azure/servicefabric).</span><span class="sxs-lookup"><span data-stu-id="c0e31-127">Clear hello check boxes for all sites except for hello one that points toohello Service Fabric plug-in location (http://dl.microsoft.com/eclipse/azure/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="c0e31-128">Creación de una aplicación de Service Fabric en Eclipse</span><span class="sxs-lookup"><span data-stu-id="c0e31-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="c0e31-129">En Eclipse Neon, vaya demasiado**archivo** > **New** > **otros**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-129">In Eclipse Neon, go too**File** > **New** > **Other**.</span></span> <span data-ttu-id="c0e31-130">Seleccione **Service Fabric Project** (Proyecto de Service Fabric) y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="c0e31-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Página 1 del nuevo proyecto de Service Fabric][create-application/p1]

2.  <span data-ttu-id="c0e31-132">Escriba el nombre del proyecto y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="c0e31-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Página 2 del nuevo proyecto de Service Fabric][create-application/p2]

3.  <span data-ttu-id="c0e31-134">En la lista Hola de plantillas, seleccione **plantilla de servicio**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-134">In hello list of templates, select **Service Template**.</span></span> <span data-ttu-id="c0e31-135">Seleccione el tipo de plantilla de servicio (Actor, Stateless, Container o Guest Binary) y, después, haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="c0e31-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Página 3 del nuevo proyecto de Service Fabric][create-application/p3]

4.  <span data-ttu-id="c0e31-137">Escriba el nombre de servicio de Hola y detalles de servicio y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-137">Enter hello service name and service details, and then click **Finish**.</span></span>

    ![Página 4 del nuevo proyecto de Service Fabric][create-application/p4]

5. <span data-ttu-id="c0e31-139">Al crear su primer proyecto de Service Fabric en hello **abrir perspectiva asociados** cuadro de diálogo, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-139">When you create your first Service Fabric project, in hello **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Página 5 del nuevo proyecto de Service Fabric][create-application/p5]

6.  <span data-ttu-id="c0e31-141">Así es el nuevo proyecto:</span><span class="sxs-lookup"><span data-stu-id="c0e31-141">Your new project looks like this:</span></span>

    ![Página 6 del nuevo proyecto de Service Fabric][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="c0e31-143">Creación e implementación de una aplicación de Service Fabric en Eclipse</span><span class="sxs-lookup"><span data-stu-id="c0e31-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="c0e31-144">Haga clic con el botón derecho en la nueva aplicación de Service Fabric y, después, seleccione **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Menú contextual de Service Fabric][publish/RightClick]

2. <span data-ttu-id="c0e31-146">En el submenú de hello, seleccione opción de Hola que desee:</span><span class="sxs-lookup"><span data-stu-id="c0e31-146">In hello submenu, select hello option you want:</span></span>
    -   <span data-ttu-id="c0e31-147">aplicación de hello toobuild sin limpiar, haga clic en **aplicación generar**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-147">toobuild hello application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="c0e31-148">Haga clic en una compilación limpia de la aplicación hello, toodo **volver a generar aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-148">toodo a clean build of hello application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="c0e31-149">aplicación de hello tooclean de artefactos integrados, haga clic en **aplicación limpia**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-149">tooclean hello application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="c0e31-150">Desde este menú también se puede implementar, anular la implementación y publicar una aplicación:</span><span class="sxs-lookup"><span data-stu-id="c0e31-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="c0e31-151">clúster local de toodeploy tooyour, haga clic en **implementar aplicación**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-151">toodeploy tooyour local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="c0e31-152">Hola **publicar aplicación de** cuadro de diálogo, seleccione un perfil de publicación:</span><span class="sxs-lookup"><span data-stu-id="c0e31-152">In hello **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="c0e31-153">**Local.json**</span><span class="sxs-lookup"><span data-stu-id="c0e31-153">**Local.json**</span></span>
        -  <span data-ttu-id="c0e31-154">**Cloud.json**</span><span class="sxs-lookup"><span data-stu-id="c0e31-154">**Cloud.json**</span></span>

     <span data-ttu-id="c0e31-155">Estos archivos de JavaScript Object Notation (JSON) almacenan información (por ejemplo, los extremos de conexión e información de seguridad) que es necesario tooconnect tooyour local o un clúster en la nube (Azure).</span><span class="sxs-lookup"><span data-stu-id="c0e31-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required tooconnect tooyour local or cloud (Azure) cluster.</span></span>

  ![Menú Publish (Publicar) de Service Fabric][publish/Publish]

<span data-ttu-id="c0e31-157">Una manera alternativa de toodeploy Service Fabric se ejecute la aplicación mediante el uso de Eclipse configuraciones.</span><span class="sxs-lookup"><span data-stu-id="c0e31-157">An alternate way toodeploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="c0e31-158">Vaya demasiado**ejecutar** > **configuraciones de ejecución de**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-158">Go too**Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="c0e31-159">En **Gradle proyecto**, seleccione hello **ServiceFabricDeployer** configuración de ejecución.</span><span class="sxs-lookup"><span data-stu-id="c0e31-159">Under **Gradle Project**, select hello **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="c0e31-160">En panel derecho de hello, en hello **argumentos** ficha, para **publishProfile**, seleccione **local** o **nube**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-160">In hello right pane, on hello **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="c0e31-161">valor predeterminado de Hello es **local**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-161">hello default is **local**.</span></span> <span data-ttu-id="c0e31-162">toodeploy tooa remoto o un clúster en la nube, seleccione **nube**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-162">toodeploy tooa remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="c0e31-163">tooensure que se rellena la información adecuada de Hola Hola perfiles de publicación, edite **Local.json** o **Cloud.json** según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c0e31-163">tooensure that hello proper information is populated in hello publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="c0e31-164">Puede agregar o actualizar los detalles del punto de conexión y las credenciales de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c0e31-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="c0e31-165">Asegúrese de que **Working Directory** señala aplicación toohello desea toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c0e31-165">Ensure that **Working Directory** points toohello application you want toodeploy.</span></span> <span data-ttu-id="c0e31-166">toochange Hola aplicación, haga clic en hello **área de trabajo** botón y, a continuación, seleccione aplicación Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="c0e31-166">toochange hello application, click hello **Workspace** button, and then select hello application you want.</span></span>
  6.    <span data-ttu-id="c0e31-167">Haga clic en **Apply** (Aplicar) y luego en **Run** (Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="c0e31-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="c0e31-168">La aplicación se compila e implementa en un momento.</span><span class="sxs-lookup"><span data-stu-id="c0e31-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="c0e31-169">Puede supervisar el estado de implementación de hello en el Explorador de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c0e31-169">You can monitor hello deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a><span data-ttu-id="c0e31-170">Agregar un tooyour de servicio de Service Fabric aplicación Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c0e31-170">Add a Service Fabric service tooyour Service Fabric application</span></span>

<span data-ttu-id="c0e31-171">Hola tooadd una Service Fabric tooan existente Service Fabric aplicación de servicio, lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c0e31-171">tooadd a Service Fabric service tooan existing Service Fabric application, do hello following steps:</span></span>

1.  <span data-ttu-id="c0e31-172">Menú contextual proyecto de hello desea tooadd un servicio y, a continuación, haga clic en **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-172">Right-click hello project you want tooadd a service to, and then click **Service Fabric**.</span></span>

    ![Página 1 de Agregar servicio de Service Fabric][add-service/p1]

2.  <span data-ttu-id="c0e31-174">Haga clic en **Agregar servicio de Fabric**, y Hola completo conjunto de pasos tooadd un proyecto de servicio toohello.</span><span class="sxs-lookup"><span data-stu-id="c0e31-174">Click **Add Service Fabric Service**, and complete hello set of steps tooadd a service toohello project.</span></span>
3.  <span data-ttu-id="c0e31-175">Plantilla de servicio de hello SELECT que desee tooadd tooyour proyecto y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-175">Select hello service template you want tooadd tooyour project, and then click **Next**.</span></span>

    ![Página 2 de Agregar servicio de Service Fabric][add-service/p2]

4.  <span data-ttu-id="c0e31-177">Escriba el nombre del servicio de hello (y otros detalles, según sea necesario) y, a continuación, haga clic en hello **Agregar servicio** botón.</span><span class="sxs-lookup"><span data-stu-id="c0e31-177">Enter hello service name (and other details, as needed), and then click hello **Add Service** button.</span></span>  

    ![Página 3 de Agregar servicio de Service Fabric][add-service/p3]

5.  <span data-ttu-id="c0e31-179">Después de agrega el servicio de hello, la estructura del proyecto global tiene un aspecto similar toohello después de proyecto:</span><span class="sxs-lookup"><span data-stu-id="c0e31-179">After hello service is added, your overall project structure looks similar toohello following project:</span></span>

    ![Página 4 de Agregar servicio de Service Fabric][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a><span data-ttu-id="c0e31-181">Edición de las versiones de manifiesto de su aplicación Java de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c0e31-181">Edit Manifest versions of your Service Fabric Java application</span></span>

<span data-ttu-id="c0e31-182">versiones de manifiesto tooedit, haga clic con el botón secundario en el proyecto de hello, vaya demasiado**Service Fabric** y seleccione **editar versiones de manifiesto...**  de lista desplegable del menú Hola.</span><span class="sxs-lookup"><span data-stu-id="c0e31-182">tooedit manifest versions, right click on hello project, go too**Service Fabric** and select **Edit Manifest Versions...** from hello menu dropdown.</span></span> <span data-ttu-id="c0e31-183">En el Asistente de hello, puede actualizar versiones de manifiesto de hello para el manifiesto del servicio de aplicación manifiesto y versiones de hello para **código**, **Config** y **datos** paquetes.</span><span class="sxs-lookup"><span data-stu-id="c0e31-183">In hello wizard, you can update hello manifest versions for application manifest, service manifest and hello versions for **Code**, **Config** and **Data** packages.</span></span>

<span data-ttu-id="c0e31-184">Si activa la opción de hello **actualizar automáticamente la aplicación y las versiones de servicio** y, a continuación, actualizar una versión, las versiones de manifiesto de hello, a continuación, se actualizará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="c0e31-184">If you check hello option **Automatically update application and service versions** and then update a version, then hello manifest versions will be automatically updated.</span></span> <span data-ttu-id="c0e31-185">toogive un ejemplo, primero selecciona casilla de verificación de hello, versión de Hola de actualización de **código** versión de 0.0.0 too0.0.1 y haga clic en **finalizar**, versión del manifiesto y el manifiesto de aplicación de servicio, a continuación, versión será too0.0.1 actualizan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="c0e31-185">toogive an example, you first select hello check-box, then update hello version of **Code** version from 0.0.0 too0.0.1 and click on **Finish**, then service manifest version and application manifest version will be automatically updated too0.0.1.</span></span>

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="c0e31-186">Actualización de la aplicación Java de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c0e31-186">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="c0e31-187">Para un escenario de actualización, diga creaste hello **App1** proyecto usando Hola Service Fabric complemento de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="c0e31-187">For an upgrade scenario, say you created hello **App1** project by using hello Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="c0e31-188">Se implementó mediante Hola complemento toocreate una aplicación denominada **fabric: / App1Application**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-188">You deployed it by using hello plug-in toocreate an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="c0e31-189">tipo de aplicación Hello es **App1AppicationType**, y la versión de la aplicación hello es 1.0.</span><span class="sxs-lookup"><span data-stu-id="c0e31-189">hello application type is **App1AppicationType**, and hello application version is 1.0.</span></span> <span data-ttu-id="c0e31-190">Ahora, desea tooupgrade la aplicación sin interrumpir la disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="c0e31-190">Now, you want tooupgrade your application without interrupting availability.</span></span>

<span data-ttu-id="c0e31-191">En primer lugar, realice los cambios tooyour aplicación y, a continuación, volver a generar servicio Hola modificado.</span><span class="sxs-lookup"><span data-stu-id="c0e31-191">First, make any changes tooyour application, and then rebuild hello modified service.</span></span> <span data-ttu-id="c0e31-192">Hola de actualización modifica (ServiceManifest.xml) del archivo de manifiesto del servicio con las versiones de hello actualizado para servicio de hello (y código, configuración o datos, según corresponda).</span><span class="sxs-lookup"><span data-stu-id="c0e31-192">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="c0e31-193">Además, modificar el manifiesto de la aplicación hello (ApplicationManifest.xml) con el número de versión de Hola actualizado para aplicación hello y Hola servicio modificado.</span><span class="sxs-lookup"><span data-stu-id="c0e31-193">Also, modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application and hello modified service.</span></span>  

<span data-ttu-id="c0e31-194">tooupgrade la aplicación mediante el uso de neón de Eclipse, puede crear un perfil de configuración de ejecución duplicados.</span><span class="sxs-lookup"><span data-stu-id="c0e31-194">tooupgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="c0e31-195">A continuación, utilice el tooupgrade la aplicación según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="c0e31-195">Then, use it tooupgrade your application as needed.</span></span>

1.  <span data-ttu-id="c0e31-196">Vaya demasiado**ejecutar** > **configuraciones de ejecución de**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-196">Go too**Run** > **Run Configurations**.</span></span> <span data-ttu-id="c0e31-197">En el panel izquierdo de hello, haga clic en hello pequeña flecha toohello a la izquierda de **Gradle proyecto**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-197">In hello left pane, click hello small arrow toohello left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="c0e31-198">Haga clic con el botón derecho en **ServiceFabricDeployer** y seleccione **Duplicate** (Duplicar).</span><span class="sxs-lookup"><span data-stu-id="c0e31-198">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="c0e31-199">Escriba un nuevo nombre para esta configuración, por ejemplo, **ServiceFabricUpgrader**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-199">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="c0e31-200">En el panel derecho de hello, en hello **argumentos** , modifique **- ipconfig = 'implementar'** demasiado**- ipconfig = 'actualizar'**y, a continuación, haga clic en **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="c0e31-200">In hello right panel, on hello **Arguments** tab, change **-Pconfig='deploy'** too**-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="c0e31-201">Este proceso crea y guarda un perfil de configuración de ejecución pueden usar en cualquier tooupgrade tiempo su aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0e31-201">This process creates and saves a run configuration profile you can use at any time tooupgrade your application.</span></span> <span data-ttu-id="c0e31-202">También obtiene versión del tipo de aplicación actualizada más reciente de Hola desde el archivo de manifiesto de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="c0e31-202">It also gets hello latest updated application type version from hello application manifest file.</span></span>

<span data-ttu-id="c0e31-203">actualización de la aplicación Hello tarda unos minutos.</span><span class="sxs-lookup"><span data-stu-id="c0e31-203">hello application upgrade takes a few minutes.</span></span> <span data-ttu-id="c0e31-204">Puede supervisar la actualización de la aplicación hello en el Explorador de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c0e31-204">You can monitor hello application upgrade in Service Fabric Explorer.</span></span>

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="c0e31-205">Migrar toobe de aplicaciones de Java de tejido de servicio anterior utilizado con Maven</span><span class="sxs-lookup"><span data-stu-id="c0e31-205">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="c0e31-206">Recientemente se han transferido bibliotecas de Java de tejido de servicio desde el repositorio de tooMaven del SDK de Java del tejido de servicio.</span><span class="sxs-lookup"><span data-stu-id="c0e31-206">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="c0e31-207">Mientras que las aplicaciones nuevas de hello generar usando Eclipse, generará más reciente de los proyectos actualizados (que serán capaz de toowork con Maven), puede actualizar su tejido de servicio existente sin estado o las aplicaciones de Java de actor, que usaba Hola SDK de Java del tejido de servicio versiones anteriores, toouse Hola Java de tejido de servicio las dependencias de Maven.</span><span class="sxs-lookup"><span data-stu-id="c0e31-207">While hello new applications you generate using Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="c0e31-208">Siga los pasos de hello mencionados [aquí](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure la aplicación anterior funcione con Maven.</span><span class="sxs-lookup"><span data-stu-id="c0e31-208">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
