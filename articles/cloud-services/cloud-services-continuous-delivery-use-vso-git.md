---
title: Entrega continua con Git y Visual Studio Team Services en Azure | Microsoft Docs
description: "Aprenda a configurar los proyectos de equipo de Visual Studio Team Services para usar Git para que se compilen y se implementen automáticamente en la característica aplicación web de Servicio de aplicaciones de Azure o en los servicios en la nube."
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
ms.openlocfilehash: f4f5f231536bc381d17898ff2c592be821168a65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="4dba3-103">Entrega continua a Azure con Visual Studio Team Services y Git</span><span class="sxs-lookup"><span data-stu-id="4dba3-103">Continuous delivery to Azure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="4dba3-104">Puede usar proyectos de equipo de Visual Studio Team Services para hospedar en un repositorio Git el código fuente, y compilarlo e implementarlo automáticamente en aplicaciones web o servicios en la nube de Azure cada vez que se inserta una confirmación en el repositorio.</span><span class="sxs-lookup"><span data-stu-id="4dba3-104">You can use Visual Studio Team Services team projects to host a Git repository for your source code, and automatically build and deploy to Azure web apps or cloud services whenever you push a commit to the repository.</span></span>

<span data-ttu-id="4dba3-105">Necesitará Visual Studio 2013 y tener instalado el SDK de Azure.</span><span class="sxs-lookup"><span data-stu-id="4dba3-105">You'll need Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="4dba3-106">Si aún no tiene Visual Studio 2013, descárguelo; para ello, haga clic en el vínculo **Empezar de forma gratuita**[en www.visualstudio.com](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="4dba3-106">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="4dba3-107">Instale el SDK de Azure desde [aquí](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="4dba3-107">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="4dba3-108">Necesita una cuenta de Visual Studio Team Services para completar este tutorial: puede [abrir una cuenta de Visual Studio Team Services de forma gratuita](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="4dba3-108">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="4dba3-109">Para configurar un servicio en la nube que se compile e implemente automáticamente en Azure con Visual Studio Team Services, siga los pasos que aparecen a continuación:</span><span class="sxs-lookup"><span data-stu-id="4dba3-109">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="4dba3-110">1: Creación de un repositorio Git</span><span class="sxs-lookup"><span data-stu-id="4dba3-110">1: Create a Git repository</span></span>
1. <span data-ttu-id="4dba3-111">Si no tiene una cuenta de Visual Studio Team Services, puede obtenerla [aquí](http://go.microsoft.com/fwlink/?LinkId=397665).</span><span class="sxs-lookup"><span data-stu-id="4dba3-111">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="4dba3-112">Cuando cree un proyecto de equipo, elija Git como el sistema de control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="4dba3-112">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="4dba3-113">Siga las instrucciones para conectar Visual Studio al proyecto de equipo.</span><span class="sxs-lookup"><span data-stu-id="4dba3-113">Follow the instructions to connect Visual Studio to your team project.</span></span>
2. <span data-ttu-id="4dba3-114">En **Team Explorer**, haga clic en el vínculo **Clonar este repositorio**.</span><span class="sxs-lookup"><span data-stu-id="4dba3-114">In **Team Explorer**, choose the **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="4dba3-115">Especifique la ubicación de la copia local y elija el botón **Clonar** .</span><span class="sxs-lookup"><span data-stu-id="4dba3-115">Specify the location of the local copy and then choose the **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-to-the-repository"></a><span data-ttu-id="4dba3-116">2: Creación de un proyecto y su confirmación en el repositorio</span><span class="sxs-lookup"><span data-stu-id="4dba3-116">2: Create a project and commit it to the repository</span></span>
1. <span data-ttu-id="4dba3-117">En **Team Explorer**, en la sección **Soluciones**, elija el vínculo **Nuevo** para crear un nuevo proyecto en el repositorio local.</span><span class="sxs-lookup"><span data-stu-id="4dba3-117">In **Team Explorer**, in the **Solutions** section, choose the **New** link to create a new project in the local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="4dba3-118">Puede implementar una aplicación web o un servicio en la nube (aplicación de Azure) siguiendo los pasos que se ofrecen en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="4dba3-118">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span> <span data-ttu-id="4dba3-119">Cree un proyecto nuevo de Servicio en la nube de Azure o un proyecto nuevo de MVC de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4dba3-119">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="4dba3-120">Asegúrese de que el proyecto tiene como destino .NET Framework 4, o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="4dba3-120">Make sure that the project targets the .NET Framework 4 or later.</span></span> <span data-ttu-id="4dba3-121">Si va a crear un proyecto de servicio en la nube, agregue un rol web y un rol de trabajo de ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="4dba3-121">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="4dba3-122">Si desea crear una aplicación web, seleccione la plantilla de proyecto de **aplicación web ASP.NET** y, a continuación, **MVC**.</span><span class="sxs-lookup"><span data-stu-id="4dba3-122">If you want to create a web app, choose the **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="4dba3-123">Para obtener más información, consulte [Creación de una aplicación web ASP.NET en el Servicio de aplicaciones de Azure](../app-service-web/app-service-web-get-started-dotnet.md) .</span><span class="sxs-lookup"><span data-stu-id="4dba3-123">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="4dba3-124">Abra el menú contextual de la solución y elija **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="4dba3-124">Open the shortcut menu for the solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="4dba3-125">Si es la primera vez que usa Git en Visual Studio Team Services, deberá proporcionar alguna información que le identifique en Git.</span><span class="sxs-lookup"><span data-stu-id="4dba3-125">If this is the first time you've used Git in Visual Studio Team Services, you'll need to provide some information to identify yourself in Git.</span></span> <span data-ttu-id="4dba3-126">En el área **Cambios pendientes** de **Team Explorer**, escriba su nombre de usuario y dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="4dba3-126">In the **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="4dba3-127">Escriba un comentario para la confirmación y, a continuación, pulse el botón **Confirmar** .</span><span class="sxs-lookup"><span data-stu-id="4dba3-127">Enter a comment for the commit and then choose the **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="4dba3-128">Tenga en cuenta las opciones para incluir o excluir cambios concretos al realizar la protección.</span><span class="sxs-lookup"><span data-stu-id="4dba3-128">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="4dba3-129">Si los cambios que desea están excluidos, elija **Incluir todos**.</span><span class="sxs-lookup"><span data-stu-id="4dba3-129">If the changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="4dba3-130">Ahora ha confirmado los cambios en la copia local del repositorio.</span><span class="sxs-lookup"><span data-stu-id="4dba3-130">You've now committed the changes in your local copy of the repository.</span></span> <span data-ttu-id="4dba3-131">A continuación, sincronice dichos cambios con el servidor, para lo que debe elegir el vínculo **Sincronizar** .</span><span class="sxs-lookup"><span data-stu-id="4dba3-131">Next, sync those changes with the server by choosing the **Sync** link.</span></span>

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="4dba3-132">3: Conexión del proyecto a Azure</span><span class="sxs-lookup"><span data-stu-id="4dba3-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="4dba3-133">Ahora que tiene un repositorio Git en Visual Studio Team Services con código fuente, está en disposición de conectarlo a Azure.</span><span class="sxs-lookup"><span data-stu-id="4dba3-133">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready to connect your git repository to Azure.</span></span>  <span data-ttu-id="4dba3-134">En el [Portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), seleccione el servicio en la nube o la aplicación web, o bien cree unos nuevos haciendo clic en el icono + situado en la parte inferior izquierda y seleccionando **Servicio en la nube** o **Aplicación web** y, a continuación, **Creación rápida**.</span><span class="sxs-lookup"><span data-stu-id="4dba3-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the + icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="4dba3-135">Para servicios en la nube, elija el vínculo **Configurar publicación con Visual Studio Team Services** .</span><span class="sxs-lookup"><span data-stu-id="4dba3-135">For cloud services, choose the **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="4dba3-136">Para aplicaciones web, elija el vínculo **Configurar implementación desde control de código fuente** .</span><span class="sxs-lookup"><span data-stu-id="4dba3-136">For web apps, choose the **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="4dba3-137">En el asistente, escriba el nombre de la cuenta de Visual Studio Team Services en el cuadro de texto y elija el vínculo **Autorizar ahora** .</span><span class="sxs-lookup"><span data-stu-id="4dba3-137">In the wizard, type the name of your Visual Studio Team Services account in the textbox and choose the **Authorize Now** link.</span></span> <span data-ttu-id="4dba3-138">Puede que se le solicite que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="4dba3-138">You might be asked to sign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="4dba3-139">En el cuadro de diálogo emergente **Solicitud de conexión**, elija **Aceptar** para autorizar a Azure a que configure el proyecto del equipo en Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="4dba3-139">In the **Connection Request** pop-up dialog, choose **Accept** to authorize Azure to configure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="4dba3-140">Si la autorización se realiza correctamente, verá una lista desplegable que contiene los proyectos del equipo de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="4dba3-140">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="4dba3-141">Seleccione el nombre del proyecto de equipo que ha creado en los pasos anteriores y presione el botón de la marca de verificación del asistente.</span><span class="sxs-lookup"><span data-stu-id="4dba3-141">Select the name of team project that you created in the previous steps, and choose the wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="4dba3-142">La próxima vez que inserte una confirmación en el repositorio, Visual Studio Team Services creará e implementará su proyecto en Azure.</span><span class="sxs-lookup"><span data-stu-id="4dba3-142">The next time you push a commit to your repository, Visual Studio Team Services will build and deploy your project to Azure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="4dba3-143">4: Desencadenamiento de una recompilación y nueva implementación del proyecto</span><span class="sxs-lookup"><span data-stu-id="4dba3-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="4dba3-144">En Visual Studio, abra un archivo y cámbielo.</span><span class="sxs-lookup"><span data-stu-id="4dba3-144">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="4dba3-145">Por ejemplo, cambie el archivo `_Layout.cshtml` de la carpeta Views\\Shared de un rol web de MVC.</span><span class="sxs-lookup"><span data-stu-id="4dba3-145">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="4dba3-146">Edite el texto del pie de página del sitio y guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="4dba3-146">Edit the footer text for the site and save the file.</span></span>
   
    ![][18]
3. <span data-ttu-id="4dba3-147">En el **Explorador de soluciones**, abra el menú contextual del nodo de la solución, nodo del proyecto o archivo que cambió y elija **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="4dba3-147">In **Solution Explorer**, open the shortcut menu for the solution node, project node, or the file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="4dba3-148">Escriba un comentario y elija **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="4dba3-148">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="4dba3-149">Elija el vínculo **Sincronizar** .</span><span class="sxs-lookup"><span data-stu-id="4dba3-149">Choose the **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="4dba3-150">Elija el vínculo **Insertar** para insertar la confirmación en el repositorio en Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="4dba3-150">Choose the **Push** link to push your commit to the repository in Visual Studio Team Services.</span></span> <span data-ttu-id="4dba3-151">(También puede usar el botón **Sincronizar** para copiar las confirmaciones en el repositorio.</span><span class="sxs-lookup"><span data-stu-id="4dba3-151">(You can also use the **Sync** button to copy your commits to the repository.</span></span> <span data-ttu-id="4dba3-152">La diferencia es que **Sincronizar** también extrae los últimos cambios del repositorio).</span><span class="sxs-lookup"><span data-stu-id="4dba3-152">The difference is that **Sync** also pulls the latest changes from the repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="4dba3-153">Presione el botón **Inicio** para volver a la página principal de **Team Explorer**.</span><span class="sxs-lookup"><span data-stu-id="4dba3-153">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="4dba3-154">Elija **Compilaciones** para ver las compilaciones en curso.</span><span class="sxs-lookup"><span data-stu-id="4dba3-154">Choose **Builds** to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="4dba3-155">**Team Explorer** indica que se ha desencadenado una compilación para su protección.</span><span class="sxs-lookup"><span data-stu-id="4dba3-155">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="4dba3-156">Para ver un registro detallado del progreso de la compilación, haga doble clic en el nombre de la compilación en curso.</span><span class="sxs-lookup"><span data-stu-id="4dba3-156">To view a detailed log as the build progresses, double-click the name of the build in progress.</span></span>
10. <span data-ttu-id="4dba3-157">Mientras la compilación está en curso, eche un vistazo a la definición de compilación que se creó al vincular a Azure con el asistente.</span><span class="sxs-lookup"><span data-stu-id="4dba3-157">While the build is in-progress, take a look at the build definition that was created when you used the wizard to link to Azure.</span></span>  <span data-ttu-id="4dba3-158">Abra el menú contextual de la definición de la compilación y elija **Editar definición de compilación**.</span><span class="sxs-lookup"><span data-stu-id="4dba3-158">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="4dba3-159">En la pestaña **Desencadenador** , verá que la definición de compilación está configurada para compilar en cada protección de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4dba3-159">In the **Trigger** tab, you will see that the build definition is set to build on every check-in, by default.</span></span> <span data-ttu-id="4dba3-160">(Para un servicio en la nube, Visual Studio Team Services compila e implementa automáticamente la bifurcación principal en el entorno de ensayo.</span><span class="sxs-lookup"><span data-stu-id="4dba3-160">(For a cloud service, Visual Studio Team Services builds and deploys the master branch to the staging environment automatically.</span></span> <span data-ttu-id="4dba3-161">Aún así, tendrá que realizar un paso manual para implementar en el sitio activo.</span><span class="sxs-lookup"><span data-stu-id="4dba3-161">You still have to do a manual step to deploy to the live site.</span></span> <span data-ttu-id="4dba3-162">En el caso de una aplicación web que no tenga un entorno de ensayo, la bifurcación principal se implementa directamente en el sitio activo.</span><span class="sxs-lookup"><span data-stu-id="4dba3-162">For a web app that doesn't have staging environment, it deploys the master branch directly to the live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="4dba3-163">En la pestaña **Proceso** , puede ver que el entorno de implementación está configurado con el nombre del servicio en la nube o de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4dba3-163">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="4dba3-164">Especifique los valores para las propiedades si desea que sean diferentes de los predeterminados.</span><span class="sxs-lookup"><span data-stu-id="4dba3-164">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="4dba3-165">Las propiedades de la publicación de Azure se encuentran en la sección **Implementación** y es posible que también sea necesario definir los parámetros de MSBuild.</span><span class="sxs-lookup"><span data-stu-id="4dba3-165">The properties for Azure publishing are in the **Deployment** section, and you might also need to set MSBuild parameters.</span></span> <span data-ttu-id="4dba3-166">Por ejemplo, en un proyecto de servicio en la nube, para especificar una configuración del servicio que no sea "Nube", establezca los parámetros de MSbuild en `/p:TargetProfile=[YourProfile]`, donde *[YourProfile]* se ajusta a un archivo de configuración de servicio con un nombre como ServiceConfiguration.*YourProfile*.cscfg.</span><span class="sxs-lookup"><span data-stu-id="4dba3-166">For example, in a cloud service project, to specify a service configuration other than "Cloud", set the MSbuild parameters to `/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="4dba3-167">En la tabla siguiente se muestran las propiedades disponibles en la sección **Implementación** :</span><span class="sxs-lookup"><span data-stu-id="4dba3-167">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="4dba3-168">Propiedad</span><span class="sxs-lookup"><span data-stu-id="4dba3-168">Property</span></span> | <span data-ttu-id="4dba3-169">Valor predeterminado</span><span class="sxs-lookup"><span data-stu-id="4dba3-169">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="4dba3-170">Permitir certificados que no son de confianza</span><span class="sxs-lookup"><span data-stu-id="4dba3-170">Allow Untrusted Certificates</span></span> |<span data-ttu-id="4dba3-171">Si el valor es false, los certificados SSL deben estar firmados por una entidad de certificación raíz.</span><span class="sxs-lookup"><span data-stu-id="4dba3-171">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="4dba3-172">Permitir actualización</span><span class="sxs-lookup"><span data-stu-id="4dba3-172">Allow Upgrade</span></span> |<span data-ttu-id="4dba3-173">Permite actualizar una implementación existente en lugar de crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="4dba3-173">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="4dba3-174">Conserva la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="4dba3-174">Preserves the IP address.</span></span> |
    | <span data-ttu-id="4dba3-175">No eliminar</span><span class="sxs-lookup"><span data-stu-id="4dba3-175">Do Not Delete</span></span> |<span data-ttu-id="4dba3-176">Si el valor es true, no sobrescriba una implementación no relacionada existente (la actualización está permitida).</span><span class="sxs-lookup"><span data-stu-id="4dba3-176">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="4dba3-177">Ruta de acceso a la configuración de implementación</span><span class="sxs-lookup"><span data-stu-id="4dba3-177">Path to Deployment Settings</span></span> |<span data-ttu-id="4dba3-178">La ruta de acceso al archivo .pubxml de una aplicación web, en relación con la carpeta raíz del repositorio.</span><span class="sxs-lookup"><span data-stu-id="4dba3-178">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="4dba3-179">Se ignora para los servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="4dba3-179">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="4dba3-180">Entorno de implementación de SharePoint</span><span class="sxs-lookup"><span data-stu-id="4dba3-180">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="4dba3-181">La misma que el nombre de servicio.</span><span class="sxs-lookup"><span data-stu-id="4dba3-181">The same as the service name.</span></span> |
    | <span data-ttu-id="4dba3-182">Entorno de implementación de Azure</span><span class="sxs-lookup"><span data-stu-id="4dba3-182">Azure Deployment Environment</span></span> |<span data-ttu-id="4dba3-183">El nombre de la aplicación web o del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="4dba3-183">The web app or cloud service name.</span></span> |
14. <span data-ttu-id="4dba3-184">Llegados a este punto, la compilación debería haber finalizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="4dba3-184">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="4dba3-185">Si se hace doble clic en el nombre de la compilación, Visual Studio muestra un **Resumen de la compilación**en el que se incluyen los resultados de las pruebas de los proyectos de pruebas unitarias asociados.</span><span class="sxs-lookup"><span data-stu-id="4dba3-185">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="4dba3-186">En el [Portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885)puede ver la implementación asociada en la pestaña **Implementaciones** , al seleccionar el entorno de ensayo.</span><span class="sxs-lookup"><span data-stu-id="4dba3-186">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="4dba3-187">Vaya a la dirección URL del sitio.</span><span class="sxs-lookup"><span data-stu-id="4dba3-187">Browse to your site's URL.</span></span> <span data-ttu-id="4dba3-188">Para una aplicación web, elija el botón **Examinar** en el portal.</span><span class="sxs-lookup"><span data-stu-id="4dba3-188">For a web app, just choose  the **Browse** button in the portal.</span></span> <span data-ttu-id="4dba3-189">Para un servicio en la nube, elija la dirección URL de la sección **Vista rápida** de la página **Panel** que muestra el entorno de ensayo.</span><span class="sxs-lookup"><span data-stu-id="4dba3-189">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment.</span></span>
    
    <span data-ttu-id="4dba3-190">Las implementaciones de la integración continua para los servicios en la nube se publican de forma predeterminada en el entorno de ensayo.</span><span class="sxs-lookup"><span data-stu-id="4dba3-190">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="4dba3-191">Puede cambiarlo si configura la propiedad **Entorno del servicio de nube alternativo** en **Producción**.</span><span class="sxs-lookup"><span data-stu-id="4dba3-191">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="4dba3-192">Aquí es donde se encuentra la URL del sitio en la página del panel del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="4dba3-192">Here's where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="4dba3-193">Se abrirá una nueva pestaña del explorador para mostrar el sitio que se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="4dba3-193">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="4dba3-194">Si realiza otros cambios en el proyecto, activará más compilaciones y acumulará varias implementaciones.</span><span class="sxs-lookup"><span data-stu-id="4dba3-194">If you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="4dba3-195">La última de ellas marcada como Activa.</span><span class="sxs-lookup"><span data-stu-id="4dba3-195">The latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="4dba3-196">5: Nueva implementación de una compilación anterior</span><span class="sxs-lookup"><span data-stu-id="4dba3-196">5: Redeploy an earlier build</span></span>
<span data-ttu-id="4dba3-197">Este paso es opcional.</span><span class="sxs-lookup"><span data-stu-id="4dba3-197">This step is optional.</span></span> <span data-ttu-id="4dba3-198">En el Portal de Azure clásico, elija una implementación anterior y pulse **Volver a implementar** para devolver el sitio a una protección anterior.</span><span class="sxs-lookup"><span data-stu-id="4dba3-198">In the Azure classic portal, choose an earlier deployment and choose **Redeploy** to rewind your site to an earlier check-in.</span></span> <span data-ttu-id="4dba3-199">Tenga en cuenta que esto desencadenará una nueva compilación en TFS y creará una nueva entrada en el historial de implementaciones.</span><span class="sxs-lookup"><span data-stu-id="4dba3-199">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="4dba3-200">6: Cambio de la implementación de producción</span><span class="sxs-lookup"><span data-stu-id="4dba3-200">6: Change the Production deployment</span></span>
<span data-ttu-id="4dba3-201">Cuando esté listo, puede promover el entorno de ensayo al de producción, para lo que debe elegir **Intercambiar** en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="4dba3-201">When you are ready, you can promote the Staging environment to the Production environment by choosing **Swap** in the Azure classic portal.</span></span> <span data-ttu-id="4dba3-202">El entorno de ensayo recién implementado se promueve a Producción y el anterior entorno de Producción, si lo hubiera, pasa a entorno de ensayo.</span><span class="sxs-lookup"><span data-stu-id="4dba3-202">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="4dba3-203">La implementación activa puede ser diferente para los entornos de producción y ensayo, pero el historial de implementación de las compilaciones recientes es el mismo independientemente del entorno.</span><span class="sxs-lookup"><span data-stu-id="4dba3-203">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="4dba3-204">7: Implementación desde una bifurcación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4dba3-204">7: Deploy from a working branch.</span></span>
<span data-ttu-id="4dba3-205">Cuando usa Git, realiza cambios habitualmente en una bifurcación de trabajo y la integra en la bifurcación principal cuando el trabajo de desarrollo alcanza una fecha de finalización.</span><span class="sxs-lookup"><span data-stu-id="4dba3-205">When you use Git, you usually make changes in a working branch and integrate into the master branch when your development reaches a finished state.</span></span> <span data-ttu-id="4dba3-206">Durante la fase de desarrollo de un proyecto, querrá compilar e implementar la bifurcación de trabajo en Azure.</span><span class="sxs-lookup"><span data-stu-id="4dba3-206">During the development phase of a project, you'll want to build and deploy the working branch to Azure.</span></span>

1. <span data-ttu-id="4dba3-207">En **Team Explorer**, elija el botón **Inicio** y, a continuación, el botón **Bifurcaciones**.</span><span class="sxs-lookup"><span data-stu-id="4dba3-207">In **Team Explorer**, choose the **Home** button and then choose the **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="4dba3-208">Haga clic en el vínculo **Nueva bifurcación** .</span><span class="sxs-lookup"><span data-stu-id="4dba3-208">Choose the **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="4dba3-209">Escriba el nombre de la bifurcación, por ejemplo "trabajo", y elija **Crear bifurcación**.</span><span class="sxs-lookup"><span data-stu-id="4dba3-209">Enter the name of the branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="4dba3-210">De esta forma se crea una nueva bifurcación local.</span><span class="sxs-lookup"><span data-stu-id="4dba3-210">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="4dba3-211">Publique la bifurcación.</span><span class="sxs-lookup"><span data-stu-id="4dba3-211">Publish the branch.</span></span> <span data-ttu-id="4dba3-212">Elija el nombre de la bifurcación en **Bifurcaciones no publicadas** y elija **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="4dba3-212">Choose the branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="4dba3-213">De manera predeterminada, solo los cambios realizados en la bifurcación principal activan una compilación continua.</span><span class="sxs-lookup"><span data-stu-id="4dba3-213">By default, only changes to the master branch trigger a continuous build.</span></span> <span data-ttu-id="4dba3-214">Para configurar la compilación continua en una bifurcación de trabajo, elija la página **Compilaciones** de **Team Explorer** y elija **Editar definición de compilación**.</span><span class="sxs-lookup"><span data-stu-id="4dba3-214">To set up continuous build for a working branch, choose the **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="4dba3-215">Abra la pestaña **Configuración de origen** .</span><span class="sxs-lookup"><span data-stu-id="4dba3-215">Open the **Source Settings** tab.</span></span> <span data-ttu-id="4dba3-216">En **Bifurcaciones supervisadas para compilaciones de integración continua y graduales**, elija **Haga clic aquí para agregar una nueva fila**.</span><span class="sxs-lookup"><span data-stu-id="4dba3-216">Under **Monitored branches for continuous integration and build**, choose **Click here to add a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="4dba3-217">Especifique la bifurcación que ha creado, por ejemplo refs/heads/working.</span><span class="sxs-lookup"><span data-stu-id="4dba3-217">Specify the branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="4dba3-218">Realice un cambio en el código, abra el menú contextual del archivo modificado y elija **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="4dba3-218">Make a change in the code, open the shortcut menu for the changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="4dba3-219">Haga clic en el vínculo **Confirmaciones no sincronizadas** y elija el botón **Sincronizar** o el vínculo **Insertar** para copiar los cambios en la copia de la bifurcación de trabajo en Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="4dba3-219">Choose the **Unsynced Commits** link, and choose  the **Sync** button or the **Push** link to copy the changes to the copy of the working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="4dba3-220">Vaya a la vista **Compilaciones** y busque la compilación que se acaba de desencadenar para la bifurcación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4dba3-220">Navigate to the **Builds** view and find the build that just got triggered for the working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dba3-221">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4dba3-221">Next steps</span></span>
<span data-ttu-id="4dba3-222">Para ver más sugerencias sobre el uso de Git con Visual Studio Team Services, consulte [Desarrollo y uso compartido del código de Git con Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) y para más información sobre el uso de un repositorio de Git no administrado por Visual Studio Team Services para publicar en Azure, consulte [Implementación continua en Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="4dba3-222">To learn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services to publish to Azure, see [Continuous Deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="4dba3-223">Para obtener más información sobre Visual Studio Team Services, consulte [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="4dba3-223">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

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
