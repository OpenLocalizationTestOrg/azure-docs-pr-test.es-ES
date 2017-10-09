---
title: 'Tutorial: DevOps con hello Portal de Azure | Documentos de Microsoft'
description: "Obtenga información acerca de Hola distintos flujos de trabajo de DevOps Hola Portal de Azure."
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a><span data-ttu-id="04068-103">Tutorial: DevOps con hello Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="04068-103">Tutorial: DevOps with hello Azure Portal</span></span>
<span data-ttu-id="04068-104">Hola plataforma Windows Azure está lleno de flujos de trabajo de DevOps flexibles.</span><span class="sxs-lookup"><span data-stu-id="04068-104">hello Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="04068-105">En este tutorial, aprenderá cómo las capacidades de hello tooleverage de hello toodevelop del Portal de Azure, probar, implementar, solucionar problemas, supervisar y administrar aplicaciones en ejecución.</span><span class="sxs-lookup"><span data-stu-id="04068-105">In this tutorial, you learn how tooleverage hello capabilities of hello Azure Portal toodevelop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="04068-106">Este tutorial se centra en los siguientes hello:</span><span class="sxs-lookup"><span data-stu-id="04068-106">This tutorial focuses on hello following:</span></span>

1. <span data-ttu-id="04068-107">Creación de una aplicación web y habilitación de la implementación continua</span><span class="sxs-lookup"><span data-stu-id="04068-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="04068-108">Desarrollo y prueba de una aplicación</span><span class="sxs-lookup"><span data-stu-id="04068-108">Develop and test an app</span></span>
3. <span data-ttu-id="04068-109">Supervisión y solución de problemas de una aplicación</span><span class="sxs-lookup"><span data-stu-id="04068-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="04068-110">Tareas generales de administración de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="04068-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="04068-111">Creación de una aplicación web y habilitación de la implementación continua</span><span class="sxs-lookup"><span data-stu-id="04068-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="04068-112">Crear una aplicación Web con [servicio de aplicaciones de Azure](https://azure.microsoft.com/services/app-service/), que se usará en el resto de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="04068-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in hello rest of this tutorial.</span></span> <span data-ttu-id="04068-113">Inicialmente, deberá habilitar la implementación continua desde el repositorio de código fuente en nuestro entorno de ejecución de Azure.</span><span class="sxs-lookup"><span data-stu-id="04068-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span></span>

1. <span data-ttu-id="04068-114">Hola de inicio de sesión en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="04068-114">Sign into hello Azure Portal</span></span>
2. <span data-ttu-id="04068-115">Elija **servicios de aplicaciones** &gt; **icono Agregar** y escriba un nombre, elija su suscripción y crear un nuevo tooserve de grupo de recursos como contenedor de hello para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group tooserve as hello container for hello service.</span></span>
   
   <span data-ttu-id="04068-116">Los grupos de recursos permiten toomanage distintos aspectos de solución de hello como la facturación, implementaciones y supervisión todos como un único grupo a través de [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04068-116">Resource groups allow you toomanage various aspects of hello solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![imagen1][image1]
3. <span data-ttu-id="04068-118">Transcurridos unos segundos,el Servicio de aplicaciones se ha creado.</span><span class="sxs-lookup"><span data-stu-id="04068-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="04068-119">Tomar Hola de tooexplore de unos minutos diversas opciones de menú para un servicio hello en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-119">Take a few minutes tooexplore hello various menu options for hello service in hello portal.</span></span>
   
   ![imagen2][image2]    
4. <span data-ttu-id="04068-121">Haga clic en la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-121">Click hello URL.</span></span> <span data-ttu-id="04068-122">Tenga en cuenta diversos Hola opciones disponibles para las herramientas y repositorios.</span><span class="sxs-lookup"><span data-stu-id="04068-122">Notice hello variety of available choices for tools and repositories.</span></span> <span data-ttu-id="04068-123">También puede utilizar lenguajes de Hola y marcos de su elección como. NET, Java y Ruby.</span><span class="sxs-lookup"><span data-stu-id="04068-123">You can also use hello languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![imagen3][image3]    
5. <span data-ttu-id="04068-125">Hola portal de Azure hace que la implementación continua un proceso sencillo que implica unos pocos pasos sencillos.</span><span class="sxs-lookup"><span data-stu-id="04068-125">hello Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="04068-126">Hola portal de Azure, elija Configuración en el icono de hello para el servicio de aplicaciones de Hola que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="04068-126">In hello Azure portal, choose settings from hello icon for hello app service you just created.</span></span>
   
   ![imagen4][image4]
   
   <span data-ttu-id="04068-128">De hoja de Hola que se abre en hello derecho, desplácese toohello sección de la publicación.</span><span class="sxs-lookup"><span data-stu-id="04068-128">From hello blade that opens on hello right, scroll toohello publishing section.</span></span>
   
   ![imagen5][image5]
6. <span data-ttu-id="04068-130">A continuación, configure algunas implementación continua de tooenable de configuración para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="04068-130">Next, configure some settings tooenable continuous deployment for hello app.</span></span> <span data-ttu-id="04068-131">Haga clic en el origen de la implementación y haga clic en Elegir origen.</span><span class="sxs-lookup"><span data-stu-id="04068-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="04068-132">Tenga en cuenta diversos Hola de opciones disponibles para los orígenes del repositorio.</span><span class="sxs-lookup"><span data-stu-id="04068-132">Notice hello variety of options you have for repository sources.</span></span>
   
   ![imagen6][image6]
7. <span data-ttu-id="04068-134">En este ejemplo, elija GitHub.</span><span class="sxs-lookup"><span data-stu-id="04068-134">For this example choose GitHub.</span></span> <span data-ttu-id="04068-135">Opcionalmente, elija repositorio Hola de su elección y configurar las credenciales de autorización de Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-135">Optionally choose hello repository of your choice and setup hello authorization credentials.</span></span>
   
   ![imagen7][image7]
8. <span data-ttu-id="04068-137">Después de repositorio de tooyour de autorización, a continuación, puede elegir un proyecto y una rama que se va toodeploy.</span><span class="sxs-lookup"><span data-stu-id="04068-137">After authorization tooyour repository, you can then choose a project and branch you wish toodeploy.</span></span> <span data-ttu-id="04068-138">Hay varios ejemplos ficticios que se enumeran a continuación.</span><span class="sxs-lookup"><span data-stu-id="04068-138">There are several fictitious sample examples listed below.</span></span>
   
   ![imagen8][image8]
9. <span data-ttu-id="04068-140">Una vez elegido el proyecto y la rama, haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="04068-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="04068-141">Debe iniciar las notificaciones de toosee de una implementación.</span><span class="sxs-lookup"><span data-stu-id="04068-141">You should start toosee notifications of a deployment.</span></span>
   
   ![imagen9][image9]
10. <span data-ttu-id="04068-143">Navegue tooGitHub atrás toosee hello webhook al que se ha creado el repositorio de control de código fuente de hello toointegrate con Azure.</span><span class="sxs-lookup"><span data-stu-id="04068-143">Navigate back tooGitHub toosee hello webhook that was created toointegrate hello source control repo with Azure.</span></span> <span data-ttu-id="04068-144">Hola Portal de Azure habilita la integración con GitHub con solo unos pocos pasos sencillos.</span><span class="sxs-lookup"><span data-stu-id="04068-144">hello Azure Portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![imagen10][image10]
11. <span data-ttu-id="04068-146">toodemonstrate implementación continua, agregar rápidamente algunos repositorio toohello contenido.</span><span class="sxs-lookup"><span data-stu-id="04068-146">toodemonstrate continuous deployment, you quickly add some content toohello repository.</span></span> <span data-ttu-id="04068-147">Para obtener un ejemplo simple, agregue un repositorio de GitHub ejemplo tooa de archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="04068-147">For a simple example, add a sample text file tooa GitHub repo.</span></span> <span data-ttu-id="04068-148">Son .NET toouse libre, Ruby, Python o algún otro tipo de aplicación con el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="04068-148">You are free toouse .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="04068-149">Cree tooadd disponible un archivo de texto, repositorio de toohello de aplicación de MVC de ASP.NET, Java o Ruby de su elección.</span><span class="sxs-lookup"><span data-stu-id="04068-149">Feel free tooadd a text file, ASP.NET MVC, Java, or Ruby application toohello repo of your choice.</span></span>
    
    ![imagen11][image11]
12. <span data-ttu-id="04068-151">Después de confirmar el repositorio de tooyour de cambios, verá una nueva implementación se inician en el área de notificaciones de portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-151">After committing changes tooyour repository, you see a new deployment initiate in hello portal notifications area.</span></span> <span data-ttu-id="04068-152">Si no ve rápidamente cambios después de confirmar tooyour repositorio, haga clic en sincronizar.</span><span class="sxs-lookup"><span data-stu-id="04068-152">Click Sync if you do not quickly see changes after committing tooyour repository.</span></span>
    
    ![imagen12][image12]
13. <span data-ttu-id="04068-154">En este momento, si intenta cargar página hello para el servicio de aplicaciones de hello, recibirá un error 403.</span><span class="sxs-lookup"><span data-stu-id="04068-154">At this point, if you try and load hello page for hello app service, you may receive a 403 error.</span></span> <span data-ttu-id="04068-155">En este ejemplo, es porque no hay ninguna configuración de documento predeterminado para la página de Hola como un archivo como index.htm o default.html.</span><span class="sxs-lookup"><span data-stu-id="04068-155">In this example, it is because there is no typical default document setup for hello page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="04068-156">Puede resolverlo rápidamente con hello tooling Hola Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="04068-156">You can quickly remedy this with hello tooling in hello Azure Portal.</span></span>  <span data-ttu-id="04068-157">Hola Portal de Azure, elija configuración &gt; configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="04068-157">In hello Azure Portal choose Settings &gt; Application Settings.</span></span>
    
     ![imagen13][image13]
14. <span data-ttu-id="04068-159">Se abre una hoja de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="04068-159">A blade opens for application settings.</span></span> <span data-ttu-id="04068-160">Escriba el nombre de Hola de página Hola "SamplePage.html" y haga clic en Guardar.</span><span class="sxs-lookup"><span data-stu-id="04068-160">Enter hello name of hello page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="04068-161">Tienen otras configuraciones de Hola de tooexplore de unos minutos.</span><span class="sxs-lookup"><span data-stu-id="04068-161">Take a few minutes tooexplore hello other settings.</span></span>
    
    ![imagen14][image14]
15. <span data-ttu-id="04068-163">Opcionalmente, actualice su tooensure de dirección URL de explorador se verán los cambios de hello espera.</span><span class="sxs-lookup"><span data-stu-id="04068-163">Optionally refresh your browser URL tooensure you see hello expected changes.</span></span> <span data-ttu-id="04068-164">En este caso, hay algunos textos ahora rellenar página Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-164">In this case, there is some simple text now populating hello page.</span></span> <span data-ttu-id="04068-165">Cada repositorio de toohello cambios adicionales se crearán una nueva implementación automática.</span><span class="sxs-lookup"><span data-stu-id="04068-165">Each additional change toohello repository would result in a new automatic deployment.</span></span>
    
    ![imagen15][image15]
    
    <span data-ttu-id="04068-167">Habilitar la implementación continua con hello Portal de Azure es una experiencia sencilla.</span><span class="sxs-lookup"><span data-stu-id="04068-167">Enabling continuous deployment with hello Azure Portal is an easy experience.</span></span> <span data-ttu-id="04068-168">También puede crear canalizaciones de versión más complejas y usar muchas otras técnicas con control de código fuente existente y tooAzure de toodeploy de sistemas de integración continua, como utilizar la compilación automatizada y sistemas de administración de versión.</span><span class="sxs-lookup"><span data-stu-id="04068-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems toodeploy tooAzure, such as leveraging automated build and release management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="04068-169">Desarrollo y prueba de una aplicación</span><span class="sxs-lookup"><span data-stu-id="04068-169">Develop and test an app</span></span>
<span data-ttu-id="04068-170">A continuación, modificar algunos toohello código base e implementar rápidamente los cambios.</span><span class="sxs-lookup"><span data-stu-id="04068-170">Next, make some changes toohello code base and rapidly deploy those changes.</span></span> <span data-ttu-id="04068-171">También configurará el rendimiento de algunas pruebas para la aplicación Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-171">You will also setup up some performance testing for hello Web app.</span></span>

1. <span data-ttu-id="04068-172">Hola Portal de Azure elija Servicios de aplicaciones de panel de navegación de Hola y busque el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="04068-172">In hello Azure Portal choose App Services from hello navigation pane, and locate your App Service.</span></span>
   
   ![imagen16][image16]
2. <span data-ttu-id="04068-174">Haga clic en Herramientas.</span><span class="sxs-lookup"><span data-stu-id="04068-174">Click Tools</span></span>
   
   ![imagen17][image17]
3. <span data-ttu-id="04068-176">Tenga en cuenta Hola categoría en herramientas de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="04068-176">Notice hello develop category under Tools.</span></span> <span data-ttu-id="04068-177">Hay varias herramientas útiles aquí que nos permiten toowork con aplicaciones sin salir de hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="04068-177">There are several useful tools here that allow us toowork with apps without leaving hello Azure Portal.</span></span> <span data-ttu-id="04068-178">Haga clic en Consola.</span><span class="sxs-lookup"><span data-stu-id="04068-178">Click on Console.</span></span>
   
   ![imagen18][image18]
4. <span data-ttu-id="04068-180">En la ventana de la consola de hello, puede emitir comandos en vivo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="04068-180">In hello console window, you can issue live commands for your app.</span></span> <span data-ttu-id="04068-181">Comando dir de tipo hello y presione ENTRAR.</span><span class="sxs-lookup"><span data-stu-id="04068-181">Type hello dir command and hit enter.</span></span> <span data-ttu-id="04068-182">Observe que los comandos que requieren privilegios elevados no funcionan.</span><span class="sxs-lookup"><span data-stu-id="04068-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![imagen19][image19]
5. <span data-ttu-id="04068-184">Retroceder toohello desarrollar categoría y elija Visual Studio Online.</span><span class="sxs-lookup"><span data-stu-id="04068-184">Move back toohello Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="04068-185">Nota: Visual Studio Online ahora se llama Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="04068-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span></span>
   
   ![imagen20][image20]
6. <span data-ttu-id="04068-187">Alternar en la experiencia de edición de hello en el Explorador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="04068-187">Toggle on hello in-browser editing experience for your App.</span></span>
   
   ![imagen21][image21]
7. <span data-ttu-id="04068-189">Se instala una extensión web para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="04068-189">A web extension installs for your app.</span></span> <span data-ttu-id="04068-190">Extensiones de forma rápida y sencilla agregan funcionalidad tooapps en Azure.</span><span class="sxs-lookup"><span data-stu-id="04068-190">Extensions quickly and easily add functionality tooapps in Azure.</span></span> <span data-ttu-id="04068-191">Tenga en cuenta algunas de hello otros tipos de extensiones disponibles en la siguiente captura de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-191">Notice some of hello other extension types available in hello screenshot below.</span></span>
   
   ![imagen22][image22]
8. <span data-ttu-id="04068-193">Una vez que instala Hola extensión de Visual Studio Online, haga clic en Ir.</span><span class="sxs-lookup"><span data-stu-id="04068-193">Once hello Visual Studio Online extension installs, click Go.</span></span>
   
   ![imagen23][image23]
9. <span data-ttu-id="04068-195">Un explorador pestaña abre donde verá un desarrollo IDE directamente en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-195">A browser tab opens where you see a development IDE directly in hello browser.</span></span> <span data-ttu-id="04068-196">Experiencia de hello aviso siguiente está en Chrome.</span><span class="sxs-lookup"><span data-stu-id="04068-196">Notice hello experience below is in Chrome.</span></span>
   
   ![imagen24][image24]
10. <span data-ttu-id="04068-198">Puede realizar varias actividades, como editar archivos, agregar archivos y carpetas y descargar el contenido del sitio de hello en vivo.</span><span class="sxs-lookup"><span data-stu-id="04068-198">You can perform several activities such as edit files, add files and folders, and download content from hello live site.</span></span> <span data-ttu-id="04068-199">Cree un archivo de SamplePage.html toohello de edición rápida.</span><span class="sxs-lookup"><span data-stu-id="04068-199">Make a quick edit toohello SamplePage.html file.</span></span>
    
    ![imagen25][image25]
11. <span data-ttu-id="04068-201">En unos instantes, cambios de Hola se guardan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="04068-201">In a few moments, hello changes are automatically saved.</span></span> <span data-ttu-id="04068-202">Si navega toohello back-página, puede ver los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-202">If you navigate back toohello page, you can see hello changes.</span></span> <span data-ttu-id="04068-203">Tenga en cuenta que es muy posible que las modificaciones dinámicas como estas no sean adecuadas para entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="04068-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="04068-204">No obstante, herramientas de Hola hacerla toomake muy fácil cambios rápidos para desarrollo y entornos de prueba.</span><span class="sxs-lookup"><span data-stu-id="04068-204">However, hello tools make it very easy toomake quick changes for dev and test environments.</span></span>
    
    ![imagen26][image26]
    
    ![imagen27][image27]
12. <span data-ttu-id="04068-207">Retroceder toohello hoja de herramientas y en la categoría de desarrollar hello, haga clic en prueba de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="04068-207">Move back toohello tools blade and under hello Develop category, click on Performance Test.</span></span>
    
    ![imagen28][image28]
13. <span data-ttu-id="04068-209">Debe tooset una cuenta de servicios del equipo.</span><span class="sxs-lookup"><span data-stu-id="04068-209">You need tooset a team services account.</span></span> <span data-ttu-id="04068-210">Consulte aquí para ver más detalles: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span><span class="sxs-lookup"><span data-stu-id="04068-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span></span>
14. <span data-ttu-id="04068-211">Haga clic en nuevo toocreate una prueba de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="04068-211">Click on New toocreate a performance test.</span></span>
    
    ![imagen29][image29]
    
    <span data-ttu-id="04068-213">Configurar Hola distintos valores y haga clic en Ejecutar prueba final Hola de hello diálogo tooinitiate una prueba de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="04068-213">Configure hello various values and click Run Test at hello bottom of hello dialogue tooinitiate a performance test.</span></span>
    
    ![imagen30][image30]
    
    ![imagen31][image31]
15. <span data-ttu-id="04068-216">Una vez que la prueba de hello comienza a ejecutarse, puede supervisar el estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-216">Once hello test starts running, you can monitor hello state.</span></span>
    
    ![imagen32][image32]
    
    <span data-ttu-id="04068-218">Una vez finalizada la prueba de hello, al hacer clic en el resultado de hello muestran más detalles.</span><span class="sxs-lookup"><span data-stu-id="04068-218">Once hello test finishes, clicking on hello result shows more details.</span></span>
    
    ![imagen33][image33]
16. <span data-ttu-id="04068-220">En este ejemplo, se creó una prueba pequeña que se ejecutan, por lo que hay datos limitado tooanalyze, pero se pueden ver varias métricas así como volver a ejecutar la prueba desde esta vista.</span><span class="sxs-lookup"><span data-stu-id="04068-220">In this example, you created a small test run, so there is limited data tooanalyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="04068-221">Hola Portal de Azure permite crear, ejecutar y analizar pruebas de rendimiento web en un proceso sencillo.</span><span class="sxs-lookup"><span data-stu-id="04068-221">hello Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="04068-222">Hola de capturas de pantalla siguientes muestran datos de rendimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-222">hello screenshots below display hello performance data.</span></span>
    
    ![imagen34][image34]
    
    ![imagen35][image35]
    
    ![imagen36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="04068-226">Supervisión y solución de problemas de una aplicación</span><span class="sxs-lookup"><span data-stu-id="04068-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="04068-227">Azure proporciona muchas funcionalidades de supervisión y solución de problemas de las aplicaciones que se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="04068-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="04068-228">Hola Portal de Azure para nuestra aplicación Web, elija Herramientas.</span><span class="sxs-lookup"><span data-stu-id="04068-228">In hello Azure Portal for our Web app choose Tools.</span></span>
   
   ![imagen37][image37]
2. <span data-ttu-id="04068-230">En la categoría de solución de problemas de hello, fíjese en hello las distintas opciones de uso de posibles problemas de herramientas tootroubleshoot con una aplicación en ejecución.</span><span class="sxs-lookup"><span data-stu-id="04068-230">Under hello Troubleshoot category, notice hello various choices for using tools tootroubleshoot potential issues with a running app.</span></span> <span data-ttu-id="04068-231">Puede hacer cosas como supervisar el tráfico HTTP dinámico, habilitar la recuperación automática, ver registros, etc.</span><span class="sxs-lookup"><span data-stu-id="04068-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![imagen38][image38]
3. <span data-ttu-id="04068-233">Elegir métricas del sitio tooquickly get en una vista de algunos códigos HTTP.</span><span class="sxs-lookup"><span data-stu-id="04068-233">Choose Site Metrics tooquickly get a view of some HTTP codes.</span></span>
   
   ![imagen39][image39]
4. <span data-ttu-id="04068-235">Elija Diagnóstico como el Servicio.</span><span class="sxs-lookup"><span data-stu-id="04068-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="04068-236">Elija el tipo de aplicación, a continuación, Ejecutar.</span><span class="sxs-lookup"><span data-stu-id="04068-236">Choose your application type, then choose Run.</span></span>
   
   ![imagen40][image40]
   
   <span data-ttu-id="04068-238">Comienza una recopilación.</span><span class="sxs-lookup"><span data-stu-id="04068-238">A collection begins.</span></span>
   
   ![imagen41][image41]
5. <span data-ttu-id="04068-240">Puede elegir toodiagnose posibles problemas de registro adecuado de Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-240">You may choose hello appropriate log toodiagnose potential issues.</span></span> <span data-ttu-id="04068-241">Necesita tooenable registro toosee todos los datos disponibles de hello opciones, como los registros de HTTP.</span><span class="sxs-lookup"><span data-stu-id="04068-241">You need tooenable logging toosee all of hello available data options such as HTTP Logs.</span></span>
   
   ![imagen42][image42]
   
   <span data-ttu-id="04068-243">Haciendo clic en el archivo de volcado de memoria de hello puede descargar y analizar un DebugDiag toohelp de informe de análisis buscar posibles problemas.</span><span class="sxs-lookup"><span data-stu-id="04068-243">By clicking on hello Memory Dump file you can download and analyze a DebugDiag analysis report toohelp find potential issues.</span></span>
   
   ![imagen43][image43]
6. <span data-ttu-id="04068-245">tooview más datos, necesita tooenable inicio de sesión adicional.</span><span class="sxs-lookup"><span data-stu-id="04068-245">tooview more data, you need tooenable additional logging.</span></span> <span data-ttu-id="04068-246">Hola Portal de Azure, navegue toohello Web app y elija la configuración.</span><span class="sxs-lookup"><span data-stu-id="04068-246">In hello Azure Portal, navigate toohello Web app and choose Settings.</span></span>
   
   ![imagen44][image44]
7. <span data-ttu-id="04068-248">Desplácese hacia abajo de la categoría de características de toohello y elija registros de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="04068-248">Scroll down toohello features category, and choose Diagnostic logs.</span></span>
   
      ![imagen45][image45]
8. <span data-ttu-id="04068-250">Tenga en cuenta Hola varias opciones para el registro.</span><span class="sxs-lookup"><span data-stu-id="04068-250">Notice hello various options for logging.</span></span> <span data-ttu-id="04068-251">Active el registro del servidor web y haga clic en Guardar.</span><span class="sxs-lookup"><span data-stu-id="04068-251">Toggle on Web server logging and click save.</span></span>
   
   ![imagen46][image46]
9. <span data-ttu-id="04068-253">Retroceder toohello área de herramientas para la aplicación hello y elija diagnóstico como un servicio y haga clic en la recopilación de datos de ejecución toorerun Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-253">Move back toohello tools area for hello app and choose Diagnostics as a service and click Run toorerun hello data collection.</span></span>
   
   ![imagen47][image47]
10. <span data-ttu-id="04068-255">Con la configuración del registro de hello HTTP está habilitada, verá ahora los datos recopilados para registros de HTTP.</span><span class="sxs-lookup"><span data-stu-id="04068-255">With hello HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![imagen48][image48]
11. <span data-ttu-id="04068-257">Haciendo clic en registro de archivos de hello HTML, generar un informe enriquecido basada en explorador para que lo investiguen.</span><span class="sxs-lookup"><span data-stu-id="04068-257">By clicking hello HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![imagen49][image49]
12. <span data-ttu-id="04068-259">Retroceder la sección de herramientas de toohello en hello Portal de Azure para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="04068-259">Move back toohello tools section in hello Azure Portal for hello app.</span></span> <span data-ttu-id="04068-260">Desplácese a la sección de herramientas de toohello y elija Process Explorer.</span><span class="sxs-lookup"><span data-stu-id="04068-260">Scroll toohello Tools section and choose Process Explorer.</span></span>
    
    ![imagen50][image50]
13. <span data-ttu-id="04068-262">Al elegir Explorador de procesos, puede ver detalles sobre los procesos en ejecución.</span><span class="sxs-lookup"><span data-stu-id="04068-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="04068-263">Aviso debajo de usted puede profundizar en los procesos e incluso terminar procesos desde Hola Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="04068-263">Notice below you can drill into processes and even kill processes all from hello Azure Portal.</span></span>
    
    ![imagen51][image51]
    
    ![imagen52][image52]
14. <span data-ttu-id="04068-266">Retroceder toohello hoja de configuración de hello izquierda.</span><span class="sxs-lookup"><span data-stu-id="04068-266">Move back toohello Settings blade on hello left.</span></span> <span data-ttu-id="04068-267">Haga clic en Nueva solicitud de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="04068-267">Click New support request.</span></span>
    
    ![imagen53][image53]
15. <span data-ttu-id="04068-269">De hoja Hola Hola derecho, rellene los detalles sobre los problemas de hello, escriba la información de contacto e incluso cargar datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="04068-269">From hello blade on hello right, you can fill out details about hello issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="04068-270">Hola Portal de Azure permite trabajar con el soporte técnico de Microsoft una experiencia sin problemas.</span><span class="sxs-lookup"><span data-stu-id="04068-270">hello Azure Portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![imagen54][image54]
    
    ![imagen55][image55]
    
    <span data-ttu-id="04068-273">Hola Portal de Azure ayuda a proporcionar eficaz y familiar tooling experiencias toohelp supervisar y solucionar problemas de nuestras aplicaciones en ejecución.</span><span class="sxs-lookup"><span data-stu-id="04068-273">hello Azure Portal helps provide powerful and familiar tooling experiences toohelp monitor and troubleshoot our running applications.</span></span> <span data-ttu-id="04068-274">También es capaz de tootake acción rápidamente mediante la realización de tareas, como el reciclaje de procesos, habilitar y deshabilitar diversas colecciones de datos e incluso integrar con soporte técnico profesional de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="04068-274">You are also able tootake action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="04068-275">Administración general de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="04068-275">General Application Management</span></span>
<span data-ttu-id="04068-276">Al administrar las aplicaciones, suelen necesitar tooperform una amplia variedad de actividades como la configuración de las estrategias de copia de seguridad, implementar y administrar proveedores de identidades y cómo configurar el control de acceso basado en roles.</span><span class="sxs-lookup"><span data-stu-id="04068-276">When managing applications, you often need tooperform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="04068-277">Como con hello otras experiencias de DevOps, Hola plataforma Windows Azure estas tareas integra directamente en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-277">As with hello other DevOps experiences, hello Azure platform integrates these tasks directly into hello portal.</span></span>

1. <span data-ttu-id="04068-278">tooensure mantiene Hola aplicación Web protegida de la pérdida de datos necesita las copias de seguridad de tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="04068-278">tooensure you are keeping hello Web App safe from data loss you need tooconfigure backups.</span></span> <span data-ttu-id="04068-279">Navegue toohello área de configuración de la aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="04068-279">Navigate toohello Settings area for your Web app.</span></span>
   
   ![imagen56][image56]
2. <span data-ttu-id="04068-281">En la hoja de hello en hello derecho, desplácese hacia abajo toohello categoría de características.</span><span class="sxs-lookup"><span data-stu-id="04068-281">In hello blade on hello right, scroll down toohello Features category.</span></span>
   
    ![imagen57][image57]
3. <span data-ttu-id="04068-283">Elija las copias de seguridad; se abre una hoja en hello derecho.</span><span class="sxs-lookup"><span data-stu-id="04068-283">Choose Backups; a blade opens on hello right.</span></span>
   
   ![imagen58][image58]
4. <span data-ttu-id="04068-285">Haga clic en configurar, seleccione una cuenta de almacenamiento de hoja Hola Hola derecho.</span><span class="sxs-lookup"><span data-stu-id="04068-285">Click Configure, choose a storage account from hello blade on hello right.</span></span>
   
   ![imagen59][image59]
5. <span data-ttu-id="04068-287">Ahora cree y elija un toohold del contenedor de almacenamiento de las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="04068-287">Now create and choose a storage container toohold your backups.</span></span> <span data-ttu-id="04068-288">Haga clic en crear final Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-288">Click create at hello bottom of hello blade.</span></span> <span data-ttu-id="04068-289">A continuación, seleccione el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-289">Then select hello container.</span></span>
   
   ![imagen60][image60]
6. <span data-ttu-id="04068-291">Una vez que haya elegido el contenedor de hello, puede configurar programaciones, así como las copias de seguridad el programa de instalación para las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="04068-291">Once you have chosen hello container, you can configure schedules, as well as setup backups for your databases.</span></span> <span data-ttu-id="04068-292">En este escenario, haga clic en hello guardar icono.</span><span class="sxs-lookup"><span data-stu-id="04068-292">For this scenario, click hello save icon.</span></span>
   
    ![imagen61][image61]
7. <span data-ttu-id="04068-294">Después de guardar, desplácese toohello back-hoja de hello izquierda para copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="04068-294">After saving, scroll back toohello blade on hello left for Backups.</span></span> <span data-ttu-id="04068-295">Haga clic en la aplicación de hello tooback copia de seguridad ahora.</span><span class="sxs-lookup"><span data-stu-id="04068-295">Click Backup Now tooback hello application.</span></span>
   
    ![imagen62][image62]
8. <span data-ttu-id="04068-297">En unos momentos, verá una copia de seguridad creada.</span><span class="sxs-lookup"><span data-stu-id="04068-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="04068-298">Hola aviso Restaurar ahora una opción en hello captura de pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="04068-298">Notice hello Restore Now option on hello screen-shot below.</span></span>
   
    ![imagen63][image63]
9. <span data-ttu-id="04068-300">Haga clic en Restaurar ahora y examine la hoja de toohello opciones de hello en hello derecho.</span><span class="sxs-lookup"><span data-stu-id="04068-300">Click on Restore Now and examine hello options toohello blade on hello right.</span></span> <span data-ttu-id="04068-301">Puede elegir que una copia de seguridad adecuada y sencilla restauración tooan anteriormente estado según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="04068-301">You can choose an appropriate backup and easily restore tooan earlier state as necessary.</span></span> <span data-ttu-id="04068-302">Hola portal de Azure nos ha ayudado a habilitar fácilmente una estrategia de recuperación ante desastres simple para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="04068-302">hello Azure portal has helped us easily enable a simple disaster recovery strategy for hello app.</span></span>
   
    ![imagen64][image64]
10. <span data-ttu-id="04068-304">Mover hoja de configuración de toohello de hello izquierda y en las funciones y elija autenticación/autorización.</span><span class="sxs-lookup"><span data-stu-id="04068-304">Move back toohello Settings blade on hello left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![imagen65][image65]
11. <span data-ttu-id="04068-306">En la hoja de hello en hello derecha Seleccione autenticación de servicio de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="04068-306">In hello blade on hello right choose App Service Authentication.</span></span> <span data-ttu-id="04068-307">Tenga en cuenta diversos Hola de opciones que puede configurar con los proveedores más conocidos.</span><span class="sxs-lookup"><span data-stu-id="04068-307">Notice hello variety of options you can configure with popular providers.</span></span>
    
     ![imagen66][image66]
12. <span data-ttu-id="04068-309">Elegir el proveedor de Hola de su elección y observe las opciones de hello para el ámbito de Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-309">Choose hello provider of your choice and notice hello options for hello scope.</span></span> <span data-ttu-id="04068-310">Puede proporcionar un Id. de aplicación y el secreto de la aplicación y habilitar rápidamente la autenticación de Facebook para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="04068-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for hello app.</span></span> <span data-ttu-id="04068-311">Hola Portal de Azure habilita la autenticación como una solución integrada para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="04068-311">hello Azure Portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![imagen67][image67]
13. <span data-ttu-id="04068-313">Retroceder toohello hoja de configuración y elija los usuarios en la categoría de administración de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="04068-313">Move back toohello Settings blade and choose Users under hello Resource Management category.</span></span>
    
     ![imagen68][image68]
14. <span data-ttu-id="04068-315">En la hoja de hello en hello derecho examinar Hola diversas opciones para agregar roles y usuarios.</span><span class="sxs-lookup"><span data-stu-id="04068-315">In hello blade on hello right examine hello various options for adding roles and users.</span></span> <span data-ttu-id="04068-316">Hola Portal de Azure le permite controlar fácilmente RBAC (control de acceso basado en roles) para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="04068-316">hello Azure Portal lets you easily control RBAC (Role-based access control) for hello application.</span></span>
    
     ![imagen69][image69]

## <a name="summary"></a><span data-ttu-id="04068-318">Resumen</span><span class="sxs-lookup"><span data-stu-id="04068-318">Summary</span></span>
<span data-ttu-id="04068-319">Este tutorial muestra algunos de alimentación de hello con hello plataforma Windows Azure rápidamente lo que permite una implementación continua para una aplicación web, realizar distintos del desarrollo y actividades de prueba, supervisión y solución de problemas de una aplicación activa y finalmente administrar clave estrategias como la recuperación ante desastres, identidad y control de acceso basado en roles.</span><span class="sxs-lookup"><span data-stu-id="04068-319">This tutorial demonstrated some of hello power with hello Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="04068-320">Hola plataforma Windows Azure permite una experiencia integrada para estos flujos de trabajo de DevOps, y también puede trabajar eficazmente mantenerse en el contexto para la tarea de hello en cuestión.</span><span class="sxs-lookup"><span data-stu-id="04068-320">hello Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for hello task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04068-321">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="04068-321">Next steps</span></span>
* <span data-ttu-id="04068-322">Administrador de recursos de Azure es importante para habilitar DevOps en hello plataforma Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="04068-322">Azure Resource Manager is important for enabling DevOps on hello Azure platform.</span></span>  <span data-ttu-id="04068-323">toolearn más visitar [Introducción a Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04068-323">toolearn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="04068-324">toolearn más acerca de la implementación de servicio de aplicaciones de Azure, visite [implementar su aplicación de servicio de aplicación tooAzure](../app-service-web/web-sites-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="04068-324">toolearn more about Azure App Service deployment visit [Deploy your app tooAzure App Service](../app-service-web/web-sites-deploy.md)</span></span>

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
