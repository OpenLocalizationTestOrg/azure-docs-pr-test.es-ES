---
title: Entrega continua con Visual Studio Team Services en Azure | Microsoft Docs
description: "Aprenda a configurar los proyectos de equipo de Visual Studio Team Services para que se compilen y se implementen automáticamente en la característica aplicación web de Servicio de aplicaciones de Azure o en los servicios en la nube."
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
ms.openlocfilehash: d80ce63eb7ddfd7c45726be887a772f9a7594b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services"></a><span data-ttu-id="29404-103">Entrega continua a Azure con Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="29404-103">Continuous delivery to Azure using Visual Studio Team Services</span></span>
<span data-ttu-id="29404-104">Puede configurar los proyectos de equipo de Visual Studio Team Services para que se compilen y se implementen automáticamente en las aplicaciones web de Azure o en los servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="29404-104">You can configure your Visual Studio Team Services team projects to automatically build and deploy to Azure web apps or cloud services.</span></span>  <span data-ttu-id="29404-105">Para obtener información sobre cómo configurar un sistema de compilación e implementación continuas con Team Foundation Server *local* , consulte [Entrega continua para Servicios en la nube de Azure](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="29404-105">(For information on how to set up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="29404-106">En este tutorial se supone que tiene instalados Visual Studio 2013 y el SDK de Azure.</span><span class="sxs-lookup"><span data-stu-id="29404-106">This tutorial assumes you have Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="29404-107">Si aún no tiene Visual Studio 2013, descárguelo; para ello, haga clic en el vínculo **Empezar de forma gratuita** en [www.visualstudio.com](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="29404-107">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="29404-108">Instale el SDK de Azure desde [aquí](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="29404-108">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="29404-109">Necesita una cuenta de Visual Studio Team Services para completar este tutorial: puede [abrir una cuenta de Visual Studio Team Services de forma gratuita](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="29404-109">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="29404-110">Para configurar un servicio en la nube que se compile e implemente automáticamente en Azure con Visual Studio Team Services, siga los pasos que aparecen a continuación:</span><span class="sxs-lookup"><span data-stu-id="29404-110">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="29404-111">1: Creación de un proyecto de equipo</span><span class="sxs-lookup"><span data-stu-id="29404-111">1: Create a team project</span></span>
<span data-ttu-id="29404-112">Siga las instrucciones que se describen [aquí](http://go.microsoft.com/fwlink/?LinkId=512980) para crear el proyecto de equipo y vincularlo a Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="29404-112">Follow the instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) to create your team project and link it to Visual Studio.</span></span> <span data-ttu-id="29404-113">En este tutorial se supone que usa Team Foundation Version Control (TFVC) como solución de control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="29404-113">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="29404-114">Si desea usar Git para el control de versiones, consulte [la versión Git de este tutorial](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span><span class="sxs-lookup"><span data-stu-id="29404-114">If you want to use Git for version control, see [the Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-to-source-control"></a><span data-ttu-id="29404-115">2: Protección de un proyecto para el control de código fuente</span><span class="sxs-lookup"><span data-stu-id="29404-115">2: Check in a project to source control</span></span>
1. <span data-ttu-id="29404-116">En Visual Studio, abra la solución que desee implementar o cree una nueva.</span><span class="sxs-lookup"><span data-stu-id="29404-116">In Visual Studio, open the solution you want to deploy, or create a new one.</span></span>
   <span data-ttu-id="29404-117">Puede implementar una aplicación web o un servicio en la nube (aplicación de Azure) siguiendo los pasos que se ofrecen en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="29404-117">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span>
   <span data-ttu-id="29404-118">Si desea crear una nueva solución, cree un proyecto de Servicio de nube de Azure o un proyecto de MVC de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="29404-118">If you want to create a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="29404-119">Asegúrese de que el proyecto se dirige a .NET Framework 4 o 4.5. Si está creando un proyecto de Servicio de nube, agregue un rol web de MVC de ASP.NET y un rol de trabajo y seleccione una aplicación de Internet para el rol web.</span><span class="sxs-lookup"><span data-stu-id="29404-119">Make sure that the project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for the web role.</span></span> <span data-ttu-id="29404-120">Cuando se le solicite, elija **Aplicación de Internet**.</span><span class="sxs-lookup"><span data-stu-id="29404-120">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="29404-121">Si desea crear una aplicación web, seleccione la plantilla de proyecto de aplicación web ASP.NET y, a continuación, MVC.</span><span class="sxs-lookup"><span data-stu-id="29404-121">If you want to create a web app, choose the ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="29404-122">Consulte [Crear una aplicación web de ASP.NET en Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="29404-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="29404-123">Actualmente, Visual Studio Team Services solo admite las implementaciones de integración continua de las aplicaciones web de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="29404-123">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="29404-124">Los proyectos de sitio web están fuera del alcance.</span><span class="sxs-lookup"><span data-stu-id="29404-124">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="29404-125">Abra el menú contextual de la solución y elija **Agregar solución al control de código fuente**.</span><span class="sxs-lookup"><span data-stu-id="29404-125">Open the context menu for the solution, and choose **Add Solution to Source Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="29404-126">Acepte o cambie los valores predeterminados y elija el botón **Aceptar** .</span><span class="sxs-lookup"><span data-stu-id="29404-126">Accept or change the defaults and choose the **OK** button.</span></span> <span data-ttu-id="29404-127">Una vez terminado el proceso, aparecerán los iconos de control de código fuente en el **Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="29404-127">Once the process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="29404-128">Abra el menú contextual de la solución y elija **Proteger**.</span><span class="sxs-lookup"><span data-stu-id="29404-128">Open the shortcut menu for the solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="29404-129">En el área **Cambios pendientes** de **Team Explorer**, escriba un comentario para la protección y elija el botón **Proteger**.</span><span class="sxs-lookup"><span data-stu-id="29404-129">In the **Pending Changes** area of **Team Explorer**, type a comment for the check-in and choose the **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="29404-130">Tenga en cuenta las opciones para incluir o excluir cambios concretos al realizar la protección.</span><span class="sxs-lookup"><span data-stu-id="29404-130">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="29404-131">Si los cambios deseados se excluyen, elija el vínculo **Incluir todo** .</span><span class="sxs-lookup"><span data-stu-id="29404-131">If desired changes are excluded, choose the **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="29404-132">3: Conexión del proyecto a Azure</span><span class="sxs-lookup"><span data-stu-id="29404-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="29404-133">Ahora que tiene un proyecto de equipo de VS Team Services con código fuente en él, ya puede conectar el proyecto de equipo a Azure.</span><span class="sxs-lookup"><span data-stu-id="29404-133">Now that you have a VS Team Services team project with some source code in it, you are ready to connect your team project to Azure.</span></span>  <span data-ttu-id="29404-134">En el [Portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), seleccione el servicio en la nube o la aplicación web, o bien cree unos nuevos haciendo clic en el icono **+** situado en la parte inferior izquierda y seleccionando **Servicio en la nube** o **Aplicación web** y, a continuación, **Creación rápida**.</span><span class="sxs-lookup"><span data-stu-id="29404-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the **+** icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="29404-135">Haga clic en el vínculo **Configurar publicación con Visual Studio Team Services** .</span><span class="sxs-lookup"><span data-stu-id="29404-135">Choose the **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="29404-136">En el asistente, escriba el nombre de la cuenta de Visual Studio Team Services en el cuadro de texto y haga clic en el vínculo **Autorizar ahora** .</span><span class="sxs-lookup"><span data-stu-id="29404-136">In the wizard, type the name of your Visual Studio Team Services account in the textbox and click the **Authorize Now** link.</span></span> <span data-ttu-id="29404-137">Puede que se le solicite que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="29404-137">You might be asked to sign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="29404-138">En el cuadro de diálogo emergente **Solicitud de conexión**, elija el botón **Aceptar** para autorizar a Azure a configurar su proyecto de equipo en VS Team Services.</span><span class="sxs-lookup"><span data-stu-id="29404-138">In the **Connection Request** pop-up dialog, choose the **Accept** button to authorize Azure to configure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="29404-139">Si la autorización se realiza correctamente, verá una lista desplegable que contiene los proyectos de equipo de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="29404-139">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="29404-140">Elija el nombre del proyecto de equipo que creó en los pasos anteriores y luego elija el botón con la marca de verificación del asistente.</span><span class="sxs-lookup"><span data-stu-id="29404-140">Choose  the name of team project that you created in the previous steps, and then choose the wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="29404-141">Una vez que el proyecto se haya vinculado, verá algunas instrucciones para proteger los cambios en el proyecto de equipo de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="29404-141">After your project is linked, you will see some instructions for checking in changes to your Visual Studio Team Services team project.</span></span>  <span data-ttu-id="29404-142">La próxima vez que se registre, Visual Studio Team Services compilará e implementará el proyecto en Azure.</span><span class="sxs-lookup"><span data-stu-id="29404-142">On your next check-in, Visual Studio Team Services will build and deploy your project to Azure.</span></span>  <span data-ttu-id="29404-143">Para probarlo ahora, haga clic en el vínculo **Proteger desde Visual Studio** y, luego, en **Iniciar Visual Studio** (o el botón equivalente de **Visual Studio** situado en la parte inferior de la pantalla del portal).</span><span class="sxs-lookup"><span data-stu-id="29404-143">Try this now by clicking the **Check In from Visual Studio** link, and then the **Launch Visual Studio** link (or the equivalent **Visual Studio** button at the bottom of the portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="29404-144">4: Desencadenamiento de una recompilación y nueva implementación del proyecto</span><span class="sxs-lookup"><span data-stu-id="29404-144">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="29404-145">En **Team Explorer** de Visual Studio, elija el vínculo **Explorador de control de código fuente**.</span><span class="sxs-lookup"><span data-stu-id="29404-145">In Visual Studio's **Team Explorer**, choose the **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="29404-146">Vaya hasta su archivo de solución y ábralo.</span><span class="sxs-lookup"><span data-stu-id="29404-146">Navigate to your solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="29404-147">En el **Explorador de soluciones**, abra un archivo y cámbielo.</span><span class="sxs-lookup"><span data-stu-id="29404-147">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="29404-148">Por ejemplo, cambie el archivo `_Layout.cshtml` de la carpeta Views\\Shared de un rol web de MVC.</span><span class="sxs-lookup"><span data-stu-id="29404-148">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="29404-149">Modifique el logotipo del sitio y elija **Ctrl+S** para guardar el archivo.</span><span class="sxs-lookup"><span data-stu-id="29404-149">Edit the logo for the site and choose **Ctrl+S** to save the file.</span></span>
   
    ![][18]
5. <span data-ttu-id="29404-150">En **Team Explorer**, haga clic en el vínculo **Cambios pendientes**.</span><span class="sxs-lookup"><span data-stu-id="29404-150">In **Team Explorer**, choose the **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="29404-151">Escriba un comentario y, luego, elija el botón **Proteger** .</span><span class="sxs-lookup"><span data-stu-id="29404-151">Enter a comment and then choose the **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="29404-152">Presione el botón **Inicio** para volver a la página principal de **Team Explorer**.</span><span class="sxs-lookup"><span data-stu-id="29404-152">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="29404-153">Haga clic en el vínculo **Compilaciones** para ver las compilaciones en curso.</span><span class="sxs-lookup"><span data-stu-id="29404-153">Choose the **Builds** link to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="29404-154">**Team Explorer** indica que se ha desencadenado una compilación para su protección.</span><span class="sxs-lookup"><span data-stu-id="29404-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="29404-155">Haga doble clic en el nombre de la compilación en curso para ver un registro detallado a medida que avanza la compilación.</span><span class="sxs-lookup"><span data-stu-id="29404-155">Double-click the name of the build in progress to view a detailed log as the build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="29404-156">Mientras la compilación está en curso, eche un vistazo a la definición de compilación que se creó al vincular TFS a Azure con el asistente.</span><span class="sxs-lookup"><span data-stu-id="29404-156">While the build is in-progress, take a look at the build definition that was created when you linked TFS to Azure by using the wizard.</span></span>  <span data-ttu-id="29404-157">Abra el menú contextual de la definición de compilación y elija **Editar definición de compilación**.</span><span class="sxs-lookup"><span data-stu-id="29404-157">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="29404-158">En la pestaña **Desencadenador** , verá que la definición de compilación se ha configurado para compilar en cada protección de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="29404-158">In the **Trigger** tab, you will see that the build definition is set to build on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="29404-159">En la pestaña **Proceso** , puede ver que el entorno de implementación se ha configurado con el nombre del servicio en la nube o de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="29404-159">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span> <span data-ttu-id="29404-160">Si trabaja con aplicaciones web, verá propiedades diferentes a las que se muestran aquí.</span><span class="sxs-lookup"><span data-stu-id="29404-160">If you are working with web apps, the properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="29404-161">Especifique los valores para las propiedades si desea que sean diferentes de los predeterminados.</span><span class="sxs-lookup"><span data-stu-id="29404-161">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="29404-162">Las propiedades para la publicación de Azure se encuentran en la sección **Implementación** .</span><span class="sxs-lookup"><span data-stu-id="29404-162">The properties for Azure publishing are in the **Deployment** section.</span></span>
    
     <span data-ttu-id="29404-163">En la tabla siguiente se muestran las propiedades disponibles en la sección **Implementación** :</span><span class="sxs-lookup"><span data-stu-id="29404-163">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="29404-164">Propiedad</span><span class="sxs-lookup"><span data-stu-id="29404-164">Property</span></span> | <span data-ttu-id="29404-165">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="29404-165">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="29404-166">Permitir certificados que no son de confianza</span><span class="sxs-lookup"><span data-stu-id="29404-166">Allow Untrusted Certificates</span></span> |<span data-ttu-id="29404-167">Si el valor es false, los certificados SSL deben estar firmados por una entidad de certificación raíz.</span><span class="sxs-lookup"><span data-stu-id="29404-167">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="29404-168">Permitir actualización</span><span class="sxs-lookup"><span data-stu-id="29404-168">Allow Upgrade</span></span> |<span data-ttu-id="29404-169">Permite actualizar una implementación existente en lugar de crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="29404-169">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="29404-170">Conserva la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="29404-170">Preserves the IP address.</span></span> |
    | <span data-ttu-id="29404-171">No eliminar</span><span class="sxs-lookup"><span data-stu-id="29404-171">Do Not Delete</span></span> |<span data-ttu-id="29404-172">Si el valor es true, no sobrescriba una implementación no relacionada existente (la actualización está permitida).</span><span class="sxs-lookup"><span data-stu-id="29404-172">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="29404-173">Ruta de acceso a la configuración de implementación</span><span class="sxs-lookup"><span data-stu-id="29404-173">Path to Deployment Settings</span></span> |<span data-ttu-id="29404-174">La ruta de acceso al archivo .pubxml de una aplicación web, en relación con la carpeta raíz del repositorio.</span><span class="sxs-lookup"><span data-stu-id="29404-174">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="29404-175">Se ignora para los servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="29404-175">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="29404-176">Entorno de implementación de SharePoint</span><span class="sxs-lookup"><span data-stu-id="29404-176">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="29404-177">La misma que el nombre de servicio.</span><span class="sxs-lookup"><span data-stu-id="29404-177">The same as the service name.</span></span> |
    | <span data-ttu-id="29404-178">Entorno de implementación de Azure</span><span class="sxs-lookup"><span data-stu-id="29404-178">Azure Deployment Environment</span></span> |<span data-ttu-id="29404-179">El nombre de la aplicación web o del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="29404-179">The web app or cloud service name.</span></span> |
12. <span data-ttu-id="29404-180">Si usa varias configuraciones de servicio (archivos .cscfg), puede especificar la configuración de servicio que desee en el valor **Compilación, Avanzada, Argumentos de MSBuild** .</span><span class="sxs-lookup"><span data-stu-id="29404-180">If you are using multiple service configurations (.cscfg files), you can specify the desired service configuration in the **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="29404-181">Por ejemplo, para usar ServiceConfiguration.Test.cscfg, establezca la opción de la línea de argumentos de MSBuild. `/p:TargetProfile=Test`</span><span class="sxs-lookup"><span data-stu-id="29404-181">For example, to use ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="29404-182">Llegados a este punto, la compilación debería haber finalizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="29404-182">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="29404-183">Si se hace doble clic en el nombre de la compilación, Visual Studio muestra un **Resumen de la compilación**en el que se incluyen los resultados de las pruebas de los proyectos de pruebas unitarias asociados.</span><span class="sxs-lookup"><span data-stu-id="29404-183">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="29404-184">En el [Portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885)puede ver la implementación asociada en la pestaña **Implementaciones** , al seleccionar el entorno de ensayo.</span><span class="sxs-lookup"><span data-stu-id="29404-184">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="29404-185">Vaya a la dirección URL del sitio.</span><span class="sxs-lookup"><span data-stu-id="29404-185">Browse to your site's URL.</span></span> <span data-ttu-id="29404-186">Para una aplicación web, simplemente haga clic en el botón **Examinar** de la barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="29404-186">For a web app, just click the **Browse** button on the command bar.</span></span> <span data-ttu-id="29404-187">Para un servicio en la nube, elija la dirección URL de la sección **Vista rápida** de la página **Panel** que muestra el entorno de ensayo de un servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="29404-187">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment for a cloud service.</span></span> <span data-ttu-id="29404-188">Las implementaciones de la integración continua para los servicios en la nube se publican de forma predeterminada en el entorno de ensayo.</span><span class="sxs-lookup"><span data-stu-id="29404-188">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="29404-189">Puede cambiarlo si configura la propiedad **Entorno del servicio de nube alternativo** en **Producción**.</span><span class="sxs-lookup"><span data-stu-id="29404-189">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="29404-190">Esta captura de pantalla indica en qué parte del sitio en la página del panel del servicio en la nube está la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="29404-190">This screenshot shows where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="29404-191">Se abrirá una nueva pestaña del explorador para mostrar el sitio que se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="29404-191">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="29404-192">Para los servicios en la nube, si realiza otros cambios en el proyecto, debe desencadenar más compilaciones y acumular varias implementaciones.</span><span class="sxs-lookup"><span data-stu-id="29404-192">For cloud services, if you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="29404-193">La última de ellas marcada como Activa.</span><span class="sxs-lookup"><span data-stu-id="29404-193">The latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="29404-194">5: Nueva implementación de una compilación anterior</span><span class="sxs-lookup"><span data-stu-id="29404-194">5: Redeploy an earlier build</span></span>
<span data-ttu-id="29404-195">Este paso se aplica a los servicios en la nube y es opcional.</span><span class="sxs-lookup"><span data-stu-id="29404-195">This step applies to cloud services and is optional.</span></span> <span data-ttu-id="29404-196">En el Portal de Azure clásico, seleccione una implementación anterior y haga clic en el botón **Volver a implementar** para devolver el sitio a una protección anterior.</span><span class="sxs-lookup"><span data-stu-id="29404-196">In the Azure classic portal, choose an earlier deployment and then choose the **Redeploy** button to rewind your site to an earlier check-in.</span></span>  <span data-ttu-id="29404-197">Tenga en cuenta que esto desencadenará una nueva compilación en TFS y creará una nueva entrada en el historial de implementaciones.</span><span class="sxs-lookup"><span data-stu-id="29404-197">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="29404-198">6: Cambio de la implementación de producción</span><span class="sxs-lookup"><span data-stu-id="29404-198">6: Change the Production deployment</span></span>
<span data-ttu-id="29404-199">Este paso solo se aplica a los servicios en la nube, no a las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="29404-199">This step applies only to cloud services, not web apps.</span></span> <span data-ttu-id="29404-200">Cuando esté preparado, puede promover el entorno de ensayo al de producción haciendo clic en el botón **Intercambiar** del Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="29404-200">When you are ready, you can promote the Staging environment to the production environment by choosing the **Swap** button in the Azure classic portal.</span></span> <span data-ttu-id="29404-201">El entorno de ensayo recién implementado se promueve a Producción y el anterior entorno de Producción, si lo hubiera, pasa a entorno de ensayo.</span><span class="sxs-lookup"><span data-stu-id="29404-201">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="29404-202">La implementación activa puede ser diferente para los entornos de producción y ensayo, pero el historial de implementación de las compilaciones recientes es el mismo independientemente del entorno.</span><span class="sxs-lookup"><span data-stu-id="29404-202">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="29404-203">7: Ejecución de pruebas unitarias</span><span class="sxs-lookup"><span data-stu-id="29404-203">7: Run unit tests</span></span>
<span data-ttu-id="29404-204">Este paso se aplica únicamente a las aplicaciones web, no a los servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="29404-204">This step applies only to web apps, not cloud services.</span></span> <span data-ttu-id="29404-205">Para establecer una prueba de calidad en su implementación, puede ejecutar pruebas unitarias y, en caso de error, puede detener la implementación.</span><span class="sxs-lookup"><span data-stu-id="29404-205">To put a quality gate on your deployment, you can run unit tests and if they fail, you can stop the deployment.</span></span>

1. <span data-ttu-id="29404-206">En Visual Studio, agregue un proyecto de prueba unitaria.</span><span class="sxs-lookup"><span data-stu-id="29404-206">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="29404-207">Agregue referencias de proyecto al proyecto que desee probar.</span><span class="sxs-lookup"><span data-stu-id="29404-207">Add project references to the project you want to test.</span></span>
   
   ![][40]
3. <span data-ttu-id="29404-208">Agregue algunas pruebas unitarias.</span><span class="sxs-lookup"><span data-stu-id="29404-208">Add some unit tests.</span></span> <span data-ttu-id="29404-209">Para empezar, haga una prueba ficticia que siempre se supere.</span><span class="sxs-lookup"><span data-stu-id="29404-209">To get started, try a dummy test that will always pass.</span></span>
   
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
4. <span data-ttu-id="29404-210">Edite la definición de la compilación, elija la pestaña **Proceso** y expanda el nodo **Prueba**.</span><span class="sxs-lookup"><span data-stu-id="29404-210">Edit the build definition, choose the **Process** tab, and expand the **Test** node.</span></span>
5. <span data-ttu-id="29404-211">Establezca **Suspender compilación tras error de pruebas** en True.</span><span class="sxs-lookup"><span data-stu-id="29404-211">Set the **Fail build on test failure** to True.</span></span> <span data-ttu-id="29404-212">Esto significa que la implementación no se producirá a menos que se superen las pruebas.</span><span class="sxs-lookup"><span data-stu-id="29404-212">This means that the deployment won't occur unless the tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="29404-213">Ponga en cola una nueva compilación.</span><span class="sxs-lookup"><span data-stu-id="29404-213">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="29404-214">Mientras se desarrolla la compilación, compruebe su progreso.</span><span class="sxs-lookup"><span data-stu-id="29404-214">While the build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="29404-215">Una vez terminada la compilación, compruebe los resultados de la prueba.</span><span class="sxs-lookup"><span data-stu-id="29404-215">When the build is done, check the test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="29404-216">Pruebe a crear una prueba que provoque un error.</span><span class="sxs-lookup"><span data-stu-id="29404-216">Try creating a test that will fail.</span></span> <span data-ttu-id="29404-217">Agregue una nueva prueba copiando la primera, cámbiele el nombre y comente que la línea de código que indica NotImplementedException es una excepción esperada.</span><span class="sxs-lookup"><span data-stu-id="29404-217">Add a new test by copying the first one, rename it, and comment out the line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="29404-218">Registre el cambio para poner en cola una nueva compilación.</span><span class="sxs-lookup"><span data-stu-id="29404-218">Check in the change to queue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="29404-219">Consulte los resultados de la prueba para ver los detalles del error.</span><span class="sxs-lookup"><span data-stu-id="29404-219">View the test results to see details about the failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="29404-220">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="29404-220">Next steps</span></span>
<span data-ttu-id="29404-221">Para obtener más información sobre las pruebas unitarias en Visual Studio Team Services, consulte [Ejecución de pruebas unitarias en una compilación](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span><span class="sxs-lookup"><span data-stu-id="29404-221">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="29404-222">Si usa Git, consulte [Uso compartido del código en Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) y [Implementación continua en Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="29404-222">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="29404-223">Para obtener más información sobre Visual Studio Team Services, consulte [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="29404-223">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

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
