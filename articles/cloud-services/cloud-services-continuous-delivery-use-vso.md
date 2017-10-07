---
title: la entrega aaaContinuous con Visual Studio Team Services en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconfigure su Visual Studio Team Services proyectos de equipo de tooautomatically compilar e implementar la característica de la aplicación Web de toohello en los servicios en la nube o de servicio de aplicaciones de Azure."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a><span data-ttu-id="5c4c1-103">TooAzure la entrega continua con Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="5c4c1-103">Continuous delivery tooAzure using Visual Studio Team Services</span></span>
<span data-ttu-id="5c4c1-104">Puede configurar la compilación de tooautomatically de proyectos de equipo de Visual Studio Team Services e implementar tooAzure las aplicaciones web o servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-104">You can configure your Visual Studio Team Services team projects tooautomatically build and deploy tooAzure web apps or cloud services.</span></span>  <span data-ttu-id="5c4c1-105">(Para obtener información acerca de cómo tooset una copia de seguridad continuada de compilación e implementar el sistema mediante un *local* Team Foundation Server, vea [la entrega continua de los servicios de nube de Azure](cloud-services-dotnet-continuous-delivery.md).)</span><span class="sxs-lookup"><span data-stu-id="5c4c1-105">(For information on how tooset up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="5c4c1-106">Este tutorial se supone que Visual Studio 2013 y hello Azure SDK instalado.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-106">This tutorial assumes you have Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="5c4c1-107">Si ya no tiene Visual Studio 2013, descárguelo eligiendo hello **empiece de forma gratuita** vincular en [www.visualstudio.com](http://www.visualstudio.com). Instalación hello Azure SDK desde [aquí](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="5c4c1-107">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="5c4c1-108">Necesita un toocomplete de cuenta de Visual Studio Team Services este tutorial: puede [abrir una cuenta de Visual Studio Team Services gratis](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="5c4c1-108">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="5c4c1-109">tooset seguridad un tooautomatically de servicio de nube compilar e implementar tooAzure mediante el uso de Visual Studio Team Services, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-109">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="5c4c1-110">1: Creación de un proyecto de equipo</span><span class="sxs-lookup"><span data-stu-id="5c4c1-110">1: Create a team project</span></span>
<span data-ttu-id="5c4c1-111">Siga las instrucciones de hello [aquí](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate su equipo de proyecto y vincúlela tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-111">Follow hello instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate your team project and link it tooVisual Studio.</span></span> <span data-ttu-id="5c4c1-112">En este tutorial se supone que usa Team Foundation Version Control (TFVC) como solución de control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-112">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="5c4c1-113">Si desea toouse Git para el control de versiones, vea [versión de Git Hola de este tutorial](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span><span class="sxs-lookup"><span data-stu-id="5c4c1-113">If you want toouse Git for version control, see [hello Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-toosource-control"></a><span data-ttu-id="5c4c1-114">2: comprobar en un control de toosource de proyecto</span><span class="sxs-lookup"><span data-stu-id="5c4c1-114">2: Check in a project toosource control</span></span>
1. <span data-ttu-id="5c4c1-115">En Visual Studio, abra solución de hello desea toodeploy, o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-115">In Visual Studio, open hello solution you want toodeploy, or create a new one.</span></span>
   <span data-ttu-id="5c4c1-116">Puede implementar una aplicación web o un servicio de nube (aplicación de Azure) por hello siguiente los pasos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-116">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span>
   <span data-ttu-id="5c4c1-117">Si desea toocreate una nueva solución, cree un nuevo proyecto de servicio de nube de Azure o un nuevo proyecto de MVC de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-117">If you want toocreate a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="5c4c1-118">Asegúrese de que Hola proyecto tiene como destino .NET Framework 4 o 4.5 y si va a crear un proyecto de servicio de nube, agregue un rol web de ASP.NET MVC y un rol de trabajo y elija la aplicación de Internet para el rol web de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-118">Make sure that hello project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for hello web role.</span></span> <span data-ttu-id="5c4c1-119">Cuando se le solicite, elija **Aplicación de Internet**.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-119">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="5c4c1-120">Si desea toocreate una aplicación web, elija la plantilla de proyecto de aplicación Web ASP.NET de hello y, a continuación, elija MVC.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-120">If you want toocreate a web app, choose hello ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="5c4c1-121">Consulte [Crear una aplicación web de ASP.NET en Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5c4c1-121">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5c4c1-122">Actualmente, Visual Studio Team Services solo admite las implementaciones de integración continua de las aplicaciones web de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-122">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="5c4c1-123">Los proyectos de sitio web están fuera del alcance.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-123">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="5c4c1-124">Abra el menú contextual de hello para la solución de Hola y elija **Agregar solución tooSource Control**.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-124">Open hello context menu for hello solution, and choose **Add Solution tooSource Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="5c4c1-125">Aceptar o cambiar los valores predeterminados de Hola y elija hello **Aceptar** botón.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-125">Accept or change hello defaults and choose hello **OK** button.</span></span> <span data-ttu-id="5c4c1-126">Una vez completado el proceso de hello, iconos de control de código fuente aparecen en **el Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-126">Once hello process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="5c4c1-127">Abra el acceso directo de hello para la solución de Hola y elija **proteger**.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-127">Open hello shortcut menu for hello solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="5c4c1-128">Hola **cambios pendientes** área no cliente de **Team Explorer**, escriba un comentario para en el repositorio de Hola y elija hello **proteger** botón.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-128">In hello **Pending Changes** area of **Team Explorer**, type a comment for hello check-in and choose hello **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="5c4c1-129">Tenga en cuenta tooinclude de opciones de Hola o excluir cambios específicos cuando protegen.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-129">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="5c4c1-130">Si se desea se excluyen los cambios, elija hello **incluir todo** vínculo.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-130">If desired changes are excluded, choose hello **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="5c4c1-131">3: conectar Hola proyecto tooAzure</span><span class="sxs-lookup"><span data-stu-id="5c4c1-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="5c4c1-132">Ahora que tiene un proyecto de equipo de VS Team Services con algún código de origen en él, está listo tooconnect tooAzure del proyecto de su equipo.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-132">Now that you have a VS Team Services team project with some source code in it, you are ready tooconnect your team project tooAzure.</span></span>  <span data-ttu-id="5c4c1-133">Hola [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), seleccione la aplicación web o servicio de nube, o cree uno nuevo eligiendo hello  **+**  situado en la inferior izquierda de Hola y elegir **deserviciodenube** o **aplicación Web** y, a continuación, **creación rápida**.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello **+** icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="5c4c1-134">Elija hello **configurar la publicación con Visual Studio Team Services** vínculo.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-134">Choose hello **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="5c4c1-135">En el Asistente de hello, escriba el nombre de saludo de la cuenta de Visual Studio Team Services en el cuadro de texto de Hola y haga clic en hello **autorizar ahora** vínculo.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-135">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and click hello **Authorize Now** link.</span></span> <span data-ttu-id="5c4c1-136">Toosign en que se le pida.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-136">You might be asked toosign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="5c4c1-137">Hola **solicitud de conexión** cuadro de diálogo emergente, elija hello **Accept** botón tooauthorize Azure tooconfigure su equipo de proyecto de VS Team Services.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-137">In hello **Connection Request** pop-up dialog, choose hello **Accept** button tooauthorize Azure tooconfigure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="5c4c1-138">Si la autorización se realiza correctamente, verá una lista desplegable que contiene los proyectos de equipo de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-138">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="5c4c1-139">Elegir nombre de hello del proyecto de equipo que creó en los pasos anteriores de hello y, a continuación, elija el botón de marca de verificación del Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-139">Choose  hello name of team project that you created in hello previous steps, and then choose hello wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="5c4c1-140">Después de su proyecto está vinculado, verá algunas instrucciones para comprobar en el proyecto de equipo de Visual Studio Team Services tooyour de cambios.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-140">After your project is linked, you will see some instructions for checking in changes tooyour Visual Studio Team Services team project.</span></span>  <span data-ttu-id="5c4c1-141">En la siguiente comprobación, Visual Studio Team Services compilará e implementará el proyecto tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-141">On your next check-in, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>  <span data-ttu-id="5c4c1-142">Pruebe esto ahora haciendo clic en hello **insertar en el repositorio de Visual Studio** vincular y, a continuación, Hola **iniciar Visual Studio** vínculo (o hello equivalente **Visual Studio** situado en la parte inferior de Hola de pantalla de bienvenida portal).</span><span class="sxs-lookup"><span data-stu-id="5c4c1-142">Try this now by clicking hello **Check In from Visual Studio** link, and then hello **Launch Visual Studio** link (or hello equivalent **Visual Studio** button at hello bottom of hello portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="5c4c1-143">4: Desencadenamiento de una recompilación y nueva implementación del proyecto</span><span class="sxs-lookup"><span data-stu-id="5c4c1-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="5c4c1-144">En Visual Studio **Team Explorer**, elija hello **Explorador de Control de código fuente** vínculo.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-144">In Visual Studio's **Team Explorer**, choose hello **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="5c4c1-145">Navegar por el archivo de solución tooyour y ábralo.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-145">Navigate tooyour solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="5c4c1-146">En el **Explorador de soluciones**, abra un archivo y cámbielo.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-146">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="5c4c1-147">Por ejemplo, cambie el archivo hello `_Layout.cshtml` en vistas de hello\\carpeta compartida en un rol web MVC.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-147">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="5c4c1-148">Editar logotipo de hello para el sitio de Hola y elija **CTRL+s** archivo de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-148">Edit hello logo for hello site and choose **Ctrl+S** toosave hello file.</span></span>
   
    ![][18]
5. <span data-ttu-id="5c4c1-149">En **Team Explorer**, elija hello **cambios pendientes** vínculo.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-149">In **Team Explorer**, choose hello **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="5c4c1-150">Escriba un comentario y, a continuación, elija hello **proteger** botón.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-150">Enter a comment and then choose hello **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="5c4c1-151">Elija hello **principal** botón tooreturn toohello **Team Explorer** página principal.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-151">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="5c4c1-152">Elija hello **compilaciones** hello tooview de vínculo se basa en curso.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-152">Choose hello **Builds** link tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="5c4c1-153">**Team Explorer** indica que se ha desencadenado una compilación para su protección.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-153">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="5c4c1-154">A medida que progresa de compilación de hello, haga doble clic en el nombre de Hola de compilación de hello en curso tooview un registro detallado.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-154">Double-click hello name of hello build in progress tooview a detailed log as hello build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="5c4c1-155">Mientras compilación Hola está en curso, eche un vistazo en la definición de compilación de Hola que se creó si vincula TFS tooAzure mediante el Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-155">While hello build is in-progress, take a look at hello build definition that was created when you linked TFS tooAzure by using hello wizard.</span></span>  <span data-ttu-id="5c4c1-156">Abra el menú contextual de Hola de definición de compilación de Hola y elija **Editar definición de compilación**.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-156">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="5c4c1-157">Hola **desencadenador** pestaña, verá que definición de compilación de hello está activada toobuild de cada protección de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-157">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="5c4c1-158">Hola **proceso** ficha, puede ver el entorno de implementación de Hola se establece toohello nombre de la aplicación web o servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-158">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span> <span data-ttu-id="5c4c1-159">Si está trabajando con las aplicaciones web, propiedades de hello que verá será diferentes de los mostrados aquí.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-159">If you are working with web apps, hello properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="5c4c1-160">Si quiere que los valores diferentes a los valores predeterminados de hello, especifique valores para propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-160">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="5c4c1-161">Hello propiedades para la publicación de Azure están en hello **implementación** sección.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-161">hello properties for Azure publishing are in hello **Deployment** section.</span></span>
    
     <span data-ttu-id="5c4c1-162">Hello tabla siguiente muestran las propiedades disponibles Hola Hola **implementación** sección:</span><span class="sxs-lookup"><span data-stu-id="5c4c1-162">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="5c4c1-163">Propiedad</span><span class="sxs-lookup"><span data-stu-id="5c4c1-163">Property</span></span> | <span data-ttu-id="5c4c1-164">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="5c4c1-164">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="5c4c1-165">Permitir certificados que no son de confianza</span><span class="sxs-lookup"><span data-stu-id="5c4c1-165">Allow Untrusted Certificates</span></span> |<span data-ttu-id="5c4c1-166">Si el valor es false, los certificados SSL deben estar firmados por una entidad de certificación raíz.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-166">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="5c4c1-167">Permitir actualización</span><span class="sxs-lookup"><span data-stu-id="5c4c1-167">Allow Upgrade</span></span> |<span data-ttu-id="5c4c1-168">Permite Hola implementación tooupdate una implementación existente en lugar de crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-168">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="5c4c1-169">Conserva la dirección IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-169">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="5c4c1-170">No eliminar</span><span class="sxs-lookup"><span data-stu-id="5c4c1-170">Do Not Delete</span></span> |<span data-ttu-id="5c4c1-171">Si el valor es true, no sobrescriba una implementación no relacionada existente (la actualización está permitida).</span><span class="sxs-lookup"><span data-stu-id="5c4c1-171">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="5c4c1-172">Ruta de acceso tooDeployment configuración</span><span class="sxs-lookup"><span data-stu-id="5c4c1-172">Path tooDeployment Settings</span></span> |<span data-ttu-id="5c4c1-173">Hola ruta tooyour .pubxml archivo para una aplicación web, toohello relativa de carpeta de raíz del repositorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-173">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="5c4c1-174">Se ignora para los servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-174">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="5c4c1-175">Entorno de implementación de SharePoint</span><span class="sxs-lookup"><span data-stu-id="5c4c1-175">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="5c4c1-176">Hola igual que el nombre del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-176">hello same as hello service name.</span></span> |
    | <span data-ttu-id="5c4c1-177">Entorno de implementación de Azure</span><span class="sxs-lookup"><span data-stu-id="5c4c1-177">Azure Deployment Environment</span></span> |<span data-ttu-id="5c4c1-178">Hola aplicación o en la nube nombre de servicio web.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-178">hello web app or cloud service name.</span></span> |
12. <span data-ttu-id="5c4c1-179">Si utiliza varias configuraciones del servicio (archivos .cscfg), puede especificar configuración de servicios deseada de hello en hello **argumentos de compilación, opciones avanzadas, MSBuild** configuración.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-179">If you are using multiple service configurations (.cscfg files), you can specify hello desired service configuration in hello **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="5c4c1-180">Por ejemplo, toouse ServiceConfiguration.Test.cscfg, establezca los argumentos de MSBuild opción de línea de `/p:TargetProfile=Test`.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-180">For example, toouse ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="5c4c1-181">Llegados a este punto, la compilación debería haber finalizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-181">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="5c4c1-182">Si hace doble clic en nombre de la compilación de hello, Visual Studio muestra un **resumen de la compilación**, incluidos los resultados de pruebas de asociados proyectos de prueba unitaria.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-182">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="5c4c1-183">Hola [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), puede ver implementación Hola asociado en hello **implementaciones** pestaña cuando se selecciona Hola entorno de ensayo.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-183">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="5c4c1-184">Examinar dirección URL del sitio tooyour.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-184">Browse tooyour site's URL.</span></span> <span data-ttu-id="5c4c1-185">Para una aplicación web, simplemente haga clic en hello **examinar** botón de barra de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-185">For a web app, just click hello **Browse** button on hello command bar.</span></span> <span data-ttu-id="5c4c1-186">Para un servicio de nube, elija dirección URL de Hola Hola **vista rápida** sección de hello **panel** página que muestra el entorno de ensayo de Hola para un servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-186">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment for a cloud service.</span></span> <span data-ttu-id="5c4c1-187">Las implementaciones de integración continua para servicios en la nube están publicados toohello el entorno de ensayo de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-187">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="5c4c1-188">Puede cambiar esta configuración hello **entorno del servicio de nube alternativo** propiedad demasiado**producción**.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-188">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="5c4c1-189">Esta captura de pantalla muestra dónde hello que dirección URL del sitio se encuentra en la página del panel del servicio de hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-189">This screenshot shows where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="5c4c1-190">Una nueva pestaña de explorador abrirá el sitio de la ejecución de tooreveal.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-190">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="5c4c1-191">Para los servicios de nube, si realiza otro proyecto de tooyour de cambios, el desencadenador se más genera y se acumularán varias implementaciones.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-191">For cloud services, if you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="5c4c1-192">Hello más reciente marca como activo.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-192">hello latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="5c4c1-193">5: Nueva implementación de una compilación anterior</span><span class="sxs-lookup"><span data-stu-id="5c4c1-193">5: Redeploy an earlier build</span></span>
<span data-ttu-id="5c4c1-194">Este paso es opcional y aplica a los servicios de toocloud.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-194">This step applies toocloud services and is optional.</span></span> <span data-ttu-id="5c4c1-195">En Hola portal de Azure clásico, elija una implementación anterior y, a continuación, elija hello **volver a implementar** botón toorewind su tooan de sitio anteriormente en el repositorio.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-195">In hello Azure classic portal, choose an earlier deployment and then choose hello **Redeploy** button toorewind your site tooan earlier check-in.</span></span>  <span data-ttu-id="5c4c1-196">Tenga en cuenta que esto desencadenará una nueva compilación en TFS y creará una nueva entrada en el historial de implementaciones.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-196">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="5c4c1-197">6: cambiar la implementación de producción de hello</span><span class="sxs-lookup"><span data-stu-id="5c4c1-197">6: Change hello Production deployment</span></span>
<span data-ttu-id="5c4c1-198">Este paso aplica solo toocloud servicios, no a las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-198">This step applies only toocloud services, not web apps.</span></span> <span data-ttu-id="5c4c1-199">Cuando esté listo, puede promover Hola ensayo toohello entorno de producción eligiendo hello **intercambiar** botón Hola portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-199">When you are ready, you can promote hello Staging environment toohello production environment by choosing hello **Swap** button in hello Azure classic portal.</span></span> <span data-ttu-id="5c4c1-200">entorno de ensayo de Hello recién implementado es tooProduction promocionada y entorno de producción de hello anterior, si existe, se convierte en un entorno de ensayo.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-200">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="5c4c1-201">Hola implementación activa puede ser diferente para entornos de ensayo y producción de hello, pero el historial de implementación de Hola de compilaciones recientes es Hola igual independientemente del entorno.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-201">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="5c4c1-202">7: Ejecución de pruebas unitarias</span><span class="sxs-lookup"><span data-stu-id="5c4c1-202">7: Run unit tests</span></span>
<span data-ttu-id="5c4c1-203">Este paso aplica solo las aplicaciones de tooweb, no los servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-203">This step applies only tooweb apps, not cloud services.</span></span> <span data-ttu-id="5c4c1-204">tooput calidad es satisfactoria de su implementación, puede ejecutar pruebas unitarias y si produce un error, puede detener la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-204">tooput a quality gate on your deployment, you can run unit tests and if they fail, you can stop hello deployment.</span></span>

1. <span data-ttu-id="5c4c1-205">En Visual Studio, agregue un proyecto de prueba unitaria.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-205">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="5c4c1-206">Agregar proyecto de toohello de referencias de proyecto que desee tootest.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-206">Add project references toohello project you want tootest.</span></span>
   
   ![][40]
3. <span data-ttu-id="5c4c1-207">Agregue algunas pruebas unitarias.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-207">Add some unit tests.</span></span> <span data-ttu-id="5c4c1-208">tooget iniciado, intente una prueba ficticia que pasará siempre.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-208">tooget started, try a dummy test that will always pass.</span></span>
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. <span data-ttu-id="5c4c1-209">Editar definición de compilación de hello, elija hello **proceso** pestaña y expanda hello **prueba** nodo.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-209">Edit hello build definition, choose hello **Process** tab, and expand hello **Test** node.</span></span>
5. <span data-ttu-id="5c4c1-210">Conjunto hello **producirá un error compilación en caso de error de prueba** tooTrue.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-210">Set hello **Fail build on test failure** tooTrue.</span></span> <span data-ttu-id="5c4c1-211">Esto significa que no produjo la implementación de Hola a menos que superan las pruebas Hola.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-211">This means that hello deployment won't occur unless hello tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="5c4c1-212">Ponga en cola una nueva compilación.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-212">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="5c4c1-213">Mientras se desarrolla la compilación de hello, comprobar su progreso.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-213">While hello build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="5c4c1-214">Cuando se realiza la compilación de hello, compruebe los resultados de pruebas de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-214">When hello build is done, check hello test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="5c4c1-215">Pruebe a crear una prueba que provoque un error.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-215">Try creating a test that will fail.</span></span> <span data-ttu-id="5c4c1-216">Agregar una nueva prueba copiando Hola primero, cámbiele el nombre y comente la línea de saludo de código que indica que NotImplementedException es una excepción esperada.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-216">Add a new test by copying hello first one, rename it, and comment out hello line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="5c4c1-217">Comprobación de hello cambiar tooqueue una nueva compilación.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-217">Check in hello change tooqueue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="5c4c1-218">Ver detalles de toosee de resultados de pruebas de hello sobre los errores de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c4c1-218">View hello test results toosee details about hello failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="5c4c1-219">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5c4c1-219">Next steps</span></span>
<span data-ttu-id="5c4c1-220">Para obtener más información sobre las pruebas unitarias en Visual Studio Team Services, consulte [Ejecución de pruebas unitarias en una compilación](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span><span class="sxs-lookup"><span data-stu-id="5c4c1-220">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="5c4c1-221">Si usa Git, vea [compartir su código de Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) y [tooAzure servicio de aplicaciones de la implementación continua](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5c4c1-221">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="5c4c1-222">Para obtener más información sobre Visual Studio Team Services, consulte [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="5c4c1-222">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
