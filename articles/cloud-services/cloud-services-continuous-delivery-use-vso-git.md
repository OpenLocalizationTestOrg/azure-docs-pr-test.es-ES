---
title: entrega aaaContinuous con Git y Visual Studio Team Services en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconfigure su Visual Studio Team Services proyectos de equipo de toouse Git tooautomatically compilar e implementar la característica de la aplicación Web de toohello en los servicios en la nube o de servicio de aplicaciones de Azure."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="60f47-103">TooAzure la entrega continua con Visual Studio Team Services y Git</span><span class="sxs-lookup"><span data-stu-id="60f47-103">Continuous delivery tooAzure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="60f47-104">Puede usar toohost de proyectos de equipo de Visual Studio Team Services un repositorio Git para el código fuente y automáticamente de compilación e implementar tooAzure las aplicaciones web o servicios en la nube siempre que realice una inserción un repositorio de toohello de confirmación.</span><span class="sxs-lookup"><span data-stu-id="60f47-104">You can use Visual Studio Team Services team projects toohost a Git repository for your source code, and automatically build and deploy tooAzure web apps or cloud services whenever you push a commit toohello repository.</span></span>

<span data-ttu-id="60f47-105">Necesitará Visual Studio 2013 y hello Azure SDK instalado.</span><span class="sxs-lookup"><span data-stu-id="60f47-105">You'll need Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="60f47-106">Si ya no tiene Visual Studio 2013, descárguelo eligiendo hello **empiece de forma gratuita** vincular en [www.visualstudio.com](http://www.visualstudio.com). Instalación hello Azure SDK desde [aquí](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="60f47-106">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="60f47-107">Necesita un toocomplete de cuenta de Visual Studio Team Services este tutorial: puede [abrir una cuenta de Visual Studio Team Services gratis](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="60f47-107">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="60f47-108">tooset seguridad un tooautomatically de servicio de nube compilar e implementar tooAzure mediante el uso de Visual Studio Team Services, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="60f47-108">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="60f47-109">1: Creación de un repositorio Git</span><span class="sxs-lookup"><span data-stu-id="60f47-109">1: Create a Git repository</span></span>
1. <span data-ttu-id="60f47-110">Si no tiene una cuenta de Visual Studio Team Services, puede obtenerla [aquí](http://go.microsoft.com/fwlink/?LinkId=397665).</span><span class="sxs-lookup"><span data-stu-id="60f47-110">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="60f47-111">Cuando cree un proyecto de equipo, elija Git como el sistema de control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="60f47-111">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="60f47-112">Siga el proyecto de equipo de hello instrucciones tooconnect Visual Studio tooyour.</span><span class="sxs-lookup"><span data-stu-id="60f47-112">Follow hello instructions tooconnect Visual Studio tooyour team project.</span></span>
2. <span data-ttu-id="60f47-113">En **Team Explorer**, elija hello **clonar este repositorio** vínculo.</span><span class="sxs-lookup"><span data-stu-id="60f47-113">In **Team Explorer**, choose hello **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="60f47-114">Especificar ubicación de Hola de copia local de hello y, a continuación, elija hello **clon** botón.</span><span class="sxs-lookup"><span data-stu-id="60f47-114">Specify hello location of hello local copy and then choose hello **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a><span data-ttu-id="60f47-115">2: crear un proyecto y confirmar toohello repositorio</span><span class="sxs-lookup"><span data-stu-id="60f47-115">2: Create a project and commit it toohello repository</span></span>
1. <span data-ttu-id="60f47-116">En **Team Explorer**, Hola **soluciones** sección, elija hello **New** vincular toocreate un proyecto nuevo en el repositorio local de Hola.</span><span class="sxs-lookup"><span data-stu-id="60f47-116">In **Team Explorer**, in hello **Solutions** section, choose hello **New** link toocreate a new project in hello local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="60f47-117">Puede implementar una aplicación web o un servicio de nube (aplicación de Azure) por hello siguiente los pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="60f47-117">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span> <span data-ttu-id="60f47-118">Cree un proyecto nuevo de Servicio en la nube de Azure o un proyecto nuevo de MVC de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="60f47-118">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="60f47-119">Asegúrese de que el destino del proyecto de Hola Hola .NET Framework 4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="60f47-119">Make sure that hello project targets hello .NET Framework 4 or later.</span></span> <span data-ttu-id="60f47-120">Si va a crear un proyecto de servicio en la nube, agregue un rol web y un rol de trabajo de ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="60f47-120">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="60f47-121">Si desea toocreate una aplicación web, elija hello **aplicación Web ASP.NET** plantilla de proyecto y, a continuación, elija **MVC**.</span><span class="sxs-lookup"><span data-stu-id="60f47-121">If you want toocreate a web app, choose hello **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="60f47-122">Para obtener más información, consulte [Creación de una aplicación web ASP.NET en el Servicio de aplicaciones de Azure](../app-service-web/app-service-web-get-started-dotnet.md) .</span><span class="sxs-lookup"><span data-stu-id="60f47-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="60f47-123">Abra el acceso directo de hello para la solución de Hola y elija **confirmar**.</span><span class="sxs-lookup"><span data-stu-id="60f47-123">Open hello shortcut menu for hello solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="60f47-124">Si se trata de hello primera vez que se ha usado Git en Visual Studio Team Services, necesitará tooprovide algunos tooidentify información por sí mismo en Git.</span><span class="sxs-lookup"><span data-stu-id="60f47-124">If this is hello first time you've used Git in Visual Studio Team Services, you'll need tooprovide some information tooidentify yourself in Git.</span></span> <span data-ttu-id="60f47-125">Hola **cambios pendientes** área no cliente de **Team Explorer**, escriba el nombre de usuario y dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="60f47-125">In hello **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="60f47-126">Escriba un comentario para la confirmación de hello y, a continuación, elija hello **confirmación** botón.</span><span class="sxs-lookup"><span data-stu-id="60f47-126">Enter a comment for hello commit and then choose hello **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="60f47-127">Tenga en cuenta tooinclude de opciones de Hola o excluir cambios específicos cuando protegen.</span><span class="sxs-lookup"><span data-stu-id="60f47-127">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="60f47-128">Si cambia de Hola quiere que se excluyen, elija **incluyen todos los**.</span><span class="sxs-lookup"><span data-stu-id="60f47-128">If hello changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="60f47-129">Ha ahora Hola confirma los cambios en una copia local del repositorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="60f47-129">You've now committed hello changes in your local copy of hello repository.</span></span> <span data-ttu-id="60f47-130">A continuación, sincroniza esos cambios con el servidor de hello eligiendo hello **sincronización** vínculo.</span><span class="sxs-lookup"><span data-stu-id="60f47-130">Next, sync those changes with hello server by choosing hello **Sync** link.</span></span>

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="60f47-131">3: conectar Hola proyecto tooAzure</span><span class="sxs-lookup"><span data-stu-id="60f47-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="60f47-132">Ahora que tiene un repositorio de Git en Visual Studio Team Services con algún código fuente en ella, está listo tooconnect su tooAzure de repositorio de git.</span><span class="sxs-lookup"><span data-stu-id="60f47-132">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready tooconnect your git repository tooAzure.</span></span>  <span data-ttu-id="60f47-133">Hola [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), seleccione la aplicación web o servicio de nube, o cree uno nuevo eligiendo Hola + situado en inferior izquierda de Hola y elegir **servicio de nube** o **Web App**y, a continuación, **creación rápida**.</span><span class="sxs-lookup"><span data-stu-id="60f47-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello + icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="60f47-134">Servicios de nube, elija hello **configurar la publicación con Visual Studio Team Services** vínculo.</span><span class="sxs-lookup"><span data-stu-id="60f47-134">For cloud services, choose hello **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="60f47-135">Para las aplicaciones web, elija hello **configurar implementación desde control de código fuente** vínculo.</span><span class="sxs-lookup"><span data-stu-id="60f47-135">For web apps, choose hello **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="60f47-136">En el Asistente de hello, escriba el nombre de hello de la cuenta de Visual Studio Team Services en el cuadro de texto de Hola y elija hello **autorizar ahora** vínculo.</span><span class="sxs-lookup"><span data-stu-id="60f47-136">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and choose hello **Authorize Now** link.</span></span> <span data-ttu-id="60f47-137">Toosign en que se le pida.</span><span class="sxs-lookup"><span data-stu-id="60f47-137">You might be asked toosign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="60f47-138">Hola **solicitud de conexión** cuadro de diálogo emergente, elija **Accept** tooauthorize tooconfigure Azure su equipo de proyecto en Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="60f47-138">In hello **Connection Request** pop-up dialog, choose **Accept** tooauthorize Azure tooconfigure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="60f47-139">Si la autorización se realiza correctamente, verá una lista desplegable que contiene los proyectos del equipo de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="60f47-139">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="60f47-140">Seleccionar nombre de hello del proyecto de equipo que creó en los pasos anteriores de Hola y elija el botón de marca de verificación del Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="60f47-140">Select hello name of team project that you created in hello previous steps, and choose hello wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="60f47-141">Hola próxima vez que se insertará un repositorio de tooyour de confirmación, Visual Studio Team Services compilará e implementará el proyecto tooAzure.</span><span class="sxs-lookup"><span data-stu-id="60f47-141">hello next time you push a commit tooyour repository, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="60f47-142">4: Desencadenamiento de una recompilación y nueva implementación del proyecto</span><span class="sxs-lookup"><span data-stu-id="60f47-142">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="60f47-143">En Visual Studio, abra un archivo y cámbielo.</span><span class="sxs-lookup"><span data-stu-id="60f47-143">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="60f47-144">Por ejemplo, cambie el archivo hello `_Layout.cshtml` en vistas de hello\\carpeta compartida en un rol web MVC.</span><span class="sxs-lookup"><span data-stu-id="60f47-144">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="60f47-145">Editar texto de pie de página de hello para el sitio de Hola y guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="60f47-145">Edit hello footer text for hello site and save hello file.</span></span>
   
    ![][18]
3. <span data-ttu-id="60f47-146">En **el Explorador de soluciones**, abra el menú contextual de Hola para hello nodo de la solución, el nodo del proyecto u Hola de archivos que se modificó y, a continuación, elija **confirmar**.</span><span class="sxs-lookup"><span data-stu-id="60f47-146">In **Solution Explorer**, open hello shortcut menu for hello solution node, project node, or hello file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="60f47-147">Escriba un comentario y elija **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="60f47-147">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="60f47-148">Elija hello **sincronización** vínculo.</span><span class="sxs-lookup"><span data-stu-id="60f47-148">Choose hello **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="60f47-149">Elija hello **Push** vincular toopush el repositorio de toohello de confirmación en Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="60f47-149">Choose hello **Push** link toopush your commit toohello repository in Visual Studio Team Services.</span></span> <span data-ttu-id="60f47-150">(También puede usar hello **sincronización** botón toocopy el repositorio de toohello confirmaciones.</span><span class="sxs-lookup"><span data-stu-id="60f47-150">(You can also use hello **Sync** button toocopy your commits toohello repository.</span></span> <span data-ttu-id="60f47-151">Hola diferencia es que **sincronización** también extrae Hola cambios más recientes desde el repositorio de Hola.)</span><span class="sxs-lookup"><span data-stu-id="60f47-151">hello difference is that **Sync** also pulls hello latest changes from hello repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="60f47-152">Elija hello **principal** botón tooreturn toohello **Team Explorer** página principal.</span><span class="sxs-lookup"><span data-stu-id="60f47-152">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="60f47-153">Elija **compilaciones** tooview Hola se basa en curso.</span><span class="sxs-lookup"><span data-stu-id="60f47-153">Choose **Builds** tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="60f47-154">**Team Explorer** indica que se ha desencadenado una compilación para su protección.</span><span class="sxs-lookup"><span data-stu-id="60f47-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="60f47-155">tooview un registro detallado que Hola compilación progresa, haga doble clic en nombre de Hola de compilación de hello en curso.</span><span class="sxs-lookup"><span data-stu-id="60f47-155">tooview a detailed log as hello build progresses, double-click hello name of hello build in progress.</span></span>
10. <span data-ttu-id="60f47-156">Mientras compilación Hola está en curso, eche un vistazo en la definición de compilación de Hola que se creó cuando se usa Hola Asistente toolink tooAzure.</span><span class="sxs-lookup"><span data-stu-id="60f47-156">While hello build is in-progress, take a look at hello build definition that was created when you used hello wizard toolink tooAzure.</span></span>  <span data-ttu-id="60f47-157">Abra el menú contextual de Hola de definición de compilación de Hola y elija **Editar definición de compilación**.</span><span class="sxs-lookup"><span data-stu-id="60f47-157">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="60f47-158">Hola **desencadenador** pestaña, verá que definición de compilación de Hola se establece toobuild en cada en el repositorio, de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="60f47-158">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in, by default.</span></span> <span data-ttu-id="60f47-159">(Para un servicio de nube, Visual Studio Team Services genera e implementa Hola bifurcación principal toohello automáticamente, el entorno de ensayo.</span><span class="sxs-lookup"><span data-stu-id="60f47-159">(For a cloud service, Visual Studio Team Services builds and deploys hello master branch toohello staging environment automatically.</span></span> <span data-ttu-id="60f47-160">Todavía tiene toodo un sitio de paso manual toodeploy toohello en vivo.</span><span class="sxs-lookup"><span data-stu-id="60f47-160">You still have toodo a manual step toodeploy toohello live site.</span></span> <span data-ttu-id="60f47-161">Para una aplicación web que no tiene el entorno de ensayo, se implementa la bifurcación principal de hello directamente toohello live sitio.</span><span class="sxs-lookup"><span data-stu-id="60f47-161">For a web app that doesn't have staging environment, it deploys hello master branch directly toohello live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="60f47-162">Hola **proceso** ficha, puede ver el entorno de implementación de Hola se establece toohello nombre de la aplicación web o servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="60f47-162">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="60f47-163">Si quiere que los valores diferentes a los valores predeterminados de hello, especifique valores para propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="60f47-163">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="60f47-164">Hello propiedades para la publicación de Azure están en hello **implementación** sección y también puede tener parámetros de MSBuild tooset.</span><span class="sxs-lookup"><span data-stu-id="60f47-164">hello properties for Azure publishing are in hello **Deployment** section, and you might also need tooset MSBuild parameters.</span></span> <span data-ttu-id="60f47-165">Por ejemplo, en un proyecto de servicio de nube, toospecify una configuración del servicio distinto de "Nube", establezca demasiado parámetros de MSbuild hello`/p:TargetProfile=[YourProfile]` donde *[YourProfile]* coincide con un archivo de configuración de servicio con un nombre como ServiceConfiguration. *YourProfile*.cscfg.</span><span class="sxs-lookup"><span data-stu-id="60f47-165">For example, in a cloud service project, toospecify a service configuration other than "Cloud", set hello MSbuild parameters too`/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="60f47-166">Hello tabla siguiente muestran las propiedades disponibles Hola Hola **implementación** sección:</span><span class="sxs-lookup"><span data-stu-id="60f47-166">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="60f47-167">Propiedad</span><span class="sxs-lookup"><span data-stu-id="60f47-167">Property</span></span> | <span data-ttu-id="60f47-168">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="60f47-168">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="60f47-169">Permitir certificados que no son de confianza</span><span class="sxs-lookup"><span data-stu-id="60f47-169">Allow Untrusted Certificates</span></span> |<span data-ttu-id="60f47-170">Si el valor es false, los certificados SSL deben estar firmados por una entidad de certificación raíz.</span><span class="sxs-lookup"><span data-stu-id="60f47-170">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="60f47-171">Permitir actualización</span><span class="sxs-lookup"><span data-stu-id="60f47-171">Allow Upgrade</span></span> |<span data-ttu-id="60f47-172">Permite Hola implementación tooupdate una implementación existente en lugar de crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="60f47-172">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="60f47-173">Conserva la dirección IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="60f47-173">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="60f47-174">No eliminar</span><span class="sxs-lookup"><span data-stu-id="60f47-174">Do Not Delete</span></span> |<span data-ttu-id="60f47-175">Si el valor es true, no sobrescriba una implementación no relacionada existente (la actualización está permitida).</span><span class="sxs-lookup"><span data-stu-id="60f47-175">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="60f47-176">Ruta de acceso tooDeployment configuración</span><span class="sxs-lookup"><span data-stu-id="60f47-176">Path tooDeployment Settings</span></span> |<span data-ttu-id="60f47-177">Hola ruta tooyour .pubxml archivo para una aplicación web, toohello relativa de carpeta de raíz del repositorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="60f47-177">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="60f47-178">Se ignora para los servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="60f47-178">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="60f47-179">Entorno de implementación de SharePoint</span><span class="sxs-lookup"><span data-stu-id="60f47-179">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="60f47-180">Hola igual que el nombre del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="60f47-180">hello same as hello service name.</span></span> |
    | <span data-ttu-id="60f47-181">Entorno de implementación de Azure</span><span class="sxs-lookup"><span data-stu-id="60f47-181">Azure Deployment Environment</span></span> |<span data-ttu-id="60f47-182">Hola aplicación o en la nube nombre de servicio web.</span><span class="sxs-lookup"><span data-stu-id="60f47-182">hello web app or cloud service name.</span></span> |
14. <span data-ttu-id="60f47-183">Llegados a este punto, la compilación debería haber finalizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="60f47-183">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="60f47-184">Si hace doble clic en nombre de la compilación de hello, Visual Studio muestra un **resumen de la compilación**, incluidos los resultados de pruebas de asociados proyectos de prueba unitaria.</span><span class="sxs-lookup"><span data-stu-id="60f47-184">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="60f47-185">Hola [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), puede ver implementación Hola asociado en hello **implementaciones** pestaña cuando se selecciona Hola entorno de ensayo.</span><span class="sxs-lookup"><span data-stu-id="60f47-185">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="60f47-186">Examinar dirección URL del sitio tooyour.</span><span class="sxs-lookup"><span data-stu-id="60f47-186">Browse tooyour site's URL.</span></span> <span data-ttu-id="60f47-187">Para una aplicación web, sólo tiene que elegir hello **examinar** botón en hello portal.</span><span class="sxs-lookup"><span data-stu-id="60f47-187">For a web app, just choose  hello **Browse** button in hello portal.</span></span> <span data-ttu-id="60f47-188">Para un servicio de nube, elija dirección URL de Hola Hola **vista rápida** sección de hello **panel** página que muestra el entorno de ensayo de Hola.</span><span class="sxs-lookup"><span data-stu-id="60f47-188">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment.</span></span>
    
    <span data-ttu-id="60f47-189">Las implementaciones de integración continua para servicios en la nube están publicados toohello el entorno de ensayo de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="60f47-189">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="60f47-190">Puede cambiar esta configuración hello **entorno del servicio de nube alternativo** propiedad demasiado**producción**.</span><span class="sxs-lookup"><span data-stu-id="60f47-190">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="60f47-191">Aquí es donde es la dirección URL del sitio de hello en la página del panel del servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="60f47-191">Here's where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="60f47-192">Una nueva pestaña de explorador abrirá el sitio de la ejecución de tooreveal.</span><span class="sxs-lookup"><span data-stu-id="60f47-192">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="60f47-193">Si realiza otros cambios tooyour proyecto, desencadenador más se compila y se acumularán varias implementaciones.</span><span class="sxs-lookup"><span data-stu-id="60f47-193">If you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="60f47-194">Hola más reciente uno está marcado como activo.</span><span class="sxs-lookup"><span data-stu-id="60f47-194">hello latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="60f47-195">5: Nueva implementación de una compilación anterior</span><span class="sxs-lookup"><span data-stu-id="60f47-195">5: Redeploy an earlier build</span></span>
<span data-ttu-id="60f47-196">Este paso es opcional.</span><span class="sxs-lookup"><span data-stu-id="60f47-196">This step is optional.</span></span> <span data-ttu-id="60f47-197">En Hola portal de Azure clásico, elija una implementación anterior y elija **volver a implementar** toorewind su tooan de sitio anteriormente en el repositorio.</span><span class="sxs-lookup"><span data-stu-id="60f47-197">In hello Azure classic portal, choose an earlier deployment and choose **Redeploy** toorewind your site tooan earlier check-in.</span></span> <span data-ttu-id="60f47-198">Tenga en cuenta que esto desencadenará una nueva compilación en TFS y creará una nueva entrada en el historial de implementaciones.</span><span class="sxs-lookup"><span data-stu-id="60f47-198">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="60f47-199">6: cambiar la implementación de producción de hello</span><span class="sxs-lookup"><span data-stu-id="60f47-199">6: Change hello Production deployment</span></span>
<span data-ttu-id="60f47-200">Cuando esté listo, puede promover Hola ensayo toohello entorno de producción eligiendo **intercambiar** Hola portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="60f47-200">When you are ready, you can promote hello Staging environment toohello Production environment by choosing **Swap** in hello Azure classic portal.</span></span> <span data-ttu-id="60f47-201">entorno de ensayo de Hello recién implementado es tooProduction promocionada y entorno de producción de hello anterior, si existe, se convierte en un entorno de ensayo.</span><span class="sxs-lookup"><span data-stu-id="60f47-201">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="60f47-202">Hola implementación activa puede ser diferente para entornos de ensayo y producción de hello, pero el historial de implementación de Hola de compilaciones recientes es Hola igual independientemente del entorno.</span><span class="sxs-lookup"><span data-stu-id="60f47-202">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="60f47-203">7: Implementación desde una bifurcación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="60f47-203">7: Deploy from a working branch.</span></span>
<span data-ttu-id="60f47-204">Al usar Git, normalmente realizar cambios en una bifurcación de trabajo e integrar en la bifurcación principal de hello cuando el desarrollo de su alcance un estado finalizado.</span><span class="sxs-lookup"><span data-stu-id="60f47-204">When you use Git, you usually make changes in a working branch and integrate into hello master branch when your development reaches a finished state.</span></span> <span data-ttu-id="60f47-205">Durante la fase de desarrollo de Hola de un proyecto, podrá desea toobuild e implementar tooAzure de bifurcación de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="60f47-205">During hello development phase of a project, you'll want toobuild and deploy hello working branch tooAzure.</span></span>

1. <span data-ttu-id="60f47-206">En **Team Explorer**, elija hello **inicio** botón y, a continuación, elija hello **bifurcaciones** botón.</span><span class="sxs-lookup"><span data-stu-id="60f47-206">In **Team Explorer**, choose hello **Home** button and then choose hello **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="60f47-207">Elija hello **nueva bifurcación** vínculo.</span><span class="sxs-lookup"><span data-stu-id="60f47-207">Choose hello **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="60f47-208">Especificar nombre de saludo de la bifurcación de hello, como "trabajando" y elegir **crear la bifurcación**.</span><span class="sxs-lookup"><span data-stu-id="60f47-208">Enter hello name of hello branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="60f47-209">De esta forma se crea una nueva bifurcación local.</span><span class="sxs-lookup"><span data-stu-id="60f47-209">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="60f47-210">Publicar bifurcación Hola.</span><span class="sxs-lookup"><span data-stu-id="60f47-210">Publish hello branch.</span></span> <span data-ttu-id="60f47-211">Elija el nombre de rama hello en **bifurcaciones se anuló la publicación**y elija **publicar**.</span><span class="sxs-lookup"><span data-stu-id="60f47-211">Choose hello branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="60f47-212">De forma predeterminada, solo cambia el desencadenador de bifurcación principal toohello una compilación continua.</span><span class="sxs-lookup"><span data-stu-id="60f47-212">By default, only changes toohello master branch trigger a continuous build.</span></span> <span data-ttu-id="60f47-213">tooset una compilación continua de una bifurcación de trabajo, elija hello **compilaciones** página **Team Explorer**y elija **Editar definición de compilación**.</span><span class="sxs-lookup"><span data-stu-id="60f47-213">tooset up continuous build for a working branch, choose hello **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="60f47-214">Abra hello **configuración del origen de** ficha. En **supervisan ramas para la integración continua y compilación**, elija **haga clic aquí tooadd una nueva fila**.</span><span class="sxs-lookup"><span data-stu-id="60f47-214">Open hello **Source Settings** tab. Under **Monitored branches for continuous integration and build**, choose **Click here tooadd a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="60f47-215">Especificar la rama de hello que haya creado, tales como refs o cabezales de trabajo.</span><span class="sxs-lookup"><span data-stu-id="60f47-215">Specify hello branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="60f47-216">Realizar un cambio en el código de hello, menú contextual abierto Hola Hola cambiado archivo y, a continuación, elija **confirmar**.</span><span class="sxs-lookup"><span data-stu-id="60f47-216">Make a change in hello code, open hello shortcut menu for hello changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="60f47-217">Elija hello **confirmaciones no sincronizadas** de vínculo y elija hello **sincronización** botón o hello **Push** hello toocopy de vínculo cambia toohello copia de rama de trabajo de hello en Visual Studio Servicios del equipo.</span><span class="sxs-lookup"><span data-stu-id="60f47-217">Choose hello **Unsynced Commits** link, and choose  hello **Sync** button or hello **Push** link toocopy hello changes toohello copy of hello working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="60f47-218">Navegue toohello **compilaciones** ver y buscar compilación Hola que simplemente se obtuvo desencadena de rama de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="60f47-218">Navigate toohello **Builds** view and find hello build that just got triggered for hello working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60f47-219">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="60f47-219">Next steps</span></span>
<span data-ttu-id="60f47-220">toolearn más sugerencias sobre cómo usar Git con Visual Studio Team Services, consulte [desarrollar y compartir su código de Git con Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) y para obtener información sobre el uso de un repositorio Git que no está administrado por toopublish de Visual Studio Team Services tooAzure, consulte [tooAzure servicio de aplicaciones de la implementación continua](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="60f47-220">toolearn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services toopublish tooAzure, see [Continuous Deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="60f47-221">Para obtener más información sobre Visual Studio Team Services, consulte [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="60f47-221">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
