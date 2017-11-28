---
title: 'Tutorial: DevOps con Azure Portal | Microsoft Docs'
description: Aprenda acerca de los distintos flujos de trabajo de DevOps en el Portal de Azure.
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
ms.openlocfilehash: eec7d1402bdea4e5433c473dd713eed23aa80464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-devops-with-the-azure-portal"></a><span data-ttu-id="61f0f-103">Tutorial: DevOps con el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="61f0f-103">Tutorial: DevOps with the Azure Portal</span></span>
<span data-ttu-id="61f0f-104">La plataforma Azure está llena de flujos de trabajo de DevOps flexibles.</span><span class="sxs-lookup"><span data-stu-id="61f0f-104">The Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="61f0f-105">En este tutorial, aprenderá a aprovechar las funcionalidades del Portal de Azure para desarrollar, probar, implementar, solucionar problemas, supervisar y administrar las aplicaciones que se están ejecutando.</span><span class="sxs-lookup"><span data-stu-id="61f0f-105">In this tutorial, you learn how to leverage the capabilities of the Azure Portal to develop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="61f0f-106">Este tutorial se centra en lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="61f0f-106">This tutorial focuses on the following:</span></span>

1. <span data-ttu-id="61f0f-107">Creación de una aplicación web y habilitación de la implementación continua</span><span class="sxs-lookup"><span data-stu-id="61f0f-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="61f0f-108">Desarrollo y prueba de una aplicación</span><span class="sxs-lookup"><span data-stu-id="61f0f-108">Develop and test an app</span></span>
3. <span data-ttu-id="61f0f-109">Supervisión y solución de problemas de una aplicación</span><span class="sxs-lookup"><span data-stu-id="61f0f-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="61f0f-110">Tareas generales de administración de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="61f0f-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="61f0f-111">Creación de una aplicación web y habilitación de la implementación continua</span><span class="sxs-lookup"><span data-stu-id="61f0f-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="61f0f-112">Con el [Servicio de aplicaciones de Azure](https://azure.microsoft.com/services/app-service/), cree una aplicación web que utilizará en el resto de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="61f0f-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in the rest of this tutorial.</span></span> <span data-ttu-id="61f0f-113">Inicialmente, deberá habilitar la implementación continua desde el repositorio de código fuente en nuestro entorno de ejecución de Azure.</span><span class="sxs-lookup"><span data-stu-id="61f0f-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span></span>

1. <span data-ttu-id="61f0f-114">Inicie sesión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="61f0f-114">Sign into the Azure Portal</span></span>
2. <span data-ttu-id="61f0f-115">Elija **App Services** &gt; **icono Agregar** y escriba un nombre, elija su suscripción y cree un grupo de recursos para que actúe como contenedor del servicio.</span><span class="sxs-lookup"><span data-stu-id="61f0f-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group to serve as the container for the service.</span></span>
   
   <span data-ttu-id="61f0f-116">Los grupos de recursos permiten administrar diversos aspectos de la solución, como la facturación, las implementaciones y la supervisión, como un solo grupo mediante [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61f0f-116">Resource groups allow you to manage various aspects of the solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![imagen1][image1]
3. <span data-ttu-id="61f0f-118">Transcurridos unos segundos,el Servicio de aplicaciones se ha creado.</span><span class="sxs-lookup"><span data-stu-id="61f0f-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="61f0f-119">Dedique unos minutos a explorar las diversas opciones de menú para el servicio en el portal.</span><span class="sxs-lookup"><span data-stu-id="61f0f-119">Take a few minutes to explore the various menu options for the service in the portal.</span></span>
   
   ![imagen2][image2]    
4. <span data-ttu-id="61f0f-121">Haga clic en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="61f0f-121">Click the URL.</span></span> <span data-ttu-id="61f0f-122">Observe la variedad de opciones disponibles para herramientas y repositorios.</span><span class="sxs-lookup"><span data-stu-id="61f0f-122">Notice the variety of available choices for tools and repositories.</span></span> <span data-ttu-id="61f0f-123">También puede usar los lenguajes y plataformas que prefiera, incluidos .NET, Java y Ruby.</span><span class="sxs-lookup"><span data-stu-id="61f0f-123">You can also use the languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![imagen3][image3]    
5. <span data-ttu-id="61f0f-125">El Portal de Azure hace que la implementación continua sea un proceso fácil con solo unos pocos pasos sencillos.</span><span class="sxs-lookup"><span data-stu-id="61f0f-125">The Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="61f0f-126">En el Portal de Azure, elija Configuración en el icono para el Servicio de aplicaciones que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="61f0f-126">In the Azure portal, choose settings from the icon for the app service you just created.</span></span>
   
   ![imagen4][image4]
   
   <span data-ttu-id="61f0f-128">En la hoja que se abre a la derecha, desplácese hasta la sección de publicación.</span><span class="sxs-lookup"><span data-stu-id="61f0f-128">From the blade that opens on the right, scroll to the publishing section.</span></span>
   
   ![imagen5][image5]
6. <span data-ttu-id="61f0f-130">A continuación, configure algunas opciones para habilitar la implementación continua para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61f0f-130">Next, configure some settings to enable continuous deployment for the app.</span></span> <span data-ttu-id="61f0f-131">Haga clic en el origen de la implementación y haga clic en Elegir origen.</span><span class="sxs-lookup"><span data-stu-id="61f0f-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="61f0f-132">Observe la variedad de opciones disponibles para los orígenes del repositorio.</span><span class="sxs-lookup"><span data-stu-id="61f0f-132">Notice the variety of options you have for repository sources.</span></span>
   
   ![imagen6][image6]
7. <span data-ttu-id="61f0f-134">En este ejemplo, elija GitHub.</span><span class="sxs-lookup"><span data-stu-id="61f0f-134">For this example choose GitHub.</span></span> <span data-ttu-id="61f0f-135">También puede elegir el repositorio que prefiera y configurar las credenciales de autorización.</span><span class="sxs-lookup"><span data-stu-id="61f0f-135">Optionally choose the repository of your choice and setup the authorization credentials.</span></span>
   
   ![imagen7][image7]
8. <span data-ttu-id="61f0f-137">Después de la autorización en el repositorio, puede elegir un proyecto y una rama que desee implementar.</span><span class="sxs-lookup"><span data-stu-id="61f0f-137">After authorization to your repository, you can then choose a project and branch you wish to deploy.</span></span> <span data-ttu-id="61f0f-138">Hay varios ejemplos ficticios que se enumeran a continuación.</span><span class="sxs-lookup"><span data-stu-id="61f0f-138">There are several fictitious sample examples listed below.</span></span>
   
   ![imagen8][image8]
9. <span data-ttu-id="61f0f-140">Una vez elegido el proyecto y la rama, haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="61f0f-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="61f0f-141">Debería empezar a ver las notificaciones de una implementación.</span><span class="sxs-lookup"><span data-stu-id="61f0f-141">You should start to see notifications of a deployment.</span></span>
   
   ![imagen9][image9]
10. <span data-ttu-id="61f0f-143">Vuelva a GitHub para ver el webhook que se creó para integrar el repositorio de control de origen con Azure.</span><span class="sxs-lookup"><span data-stu-id="61f0f-143">Navigate back to GitHub to see the webhook that was created to integrate the source control repo with Azure.</span></span> <span data-ttu-id="61f0f-144">Azure Portal permite la integración con GitHub con unos pocos pasos sencillos.</span><span class="sxs-lookup"><span data-stu-id="61f0f-144">The Azure Portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![imagen10][image10]
11. <span data-ttu-id="61f0f-146">Para demostrar la implementación continua, puede agregar rápidamente algún contenido al repositorio.</span><span class="sxs-lookup"><span data-stu-id="61f0f-146">To demonstrate continuous deployment, you quickly add some content to the repository.</span></span> <span data-ttu-id="61f0f-147">Para ver un ejemplo simple, agregue un archivo de texto de ejemplo a un repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="61f0f-147">For a simple example, add a sample text file to a GitHub repo.</span></span> <span data-ttu-id="61f0f-148">Puede usar .NET, Ruby, Python o algún otro tipo de aplicación con el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="61f0f-148">You are free to use .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="61f0f-149">Puede agregar un archivo de texto o una aplicación de ASP.NET MVC, Java o Ruby en el repositorio que elija.</span><span class="sxs-lookup"><span data-stu-id="61f0f-149">Feel free to add a text file, ASP.NET MVC, Java, or Ruby application to the repo of your choice.</span></span>
    
    ![imagen11][image11]
12. <span data-ttu-id="61f0f-151">Después de confirmar los cambios en el repositorio, verá que una nueva implementación se inicia en el área de notificaciones del Portal.</span><span class="sxs-lookup"><span data-stu-id="61f0f-151">After committing changes to your repository, you see a new deployment initiate in the portal notifications area.</span></span> <span data-ttu-id="61f0f-152">Si no ve los cambios rápidamente después de confirmar en el repositorio, haga clic en Sincronizar.</span><span class="sxs-lookup"><span data-stu-id="61f0f-152">Click Sync if you do not quickly see changes after committing to your repository.</span></span>
    
    ![imagen12][image12]
13. <span data-ttu-id="61f0f-154">En este momento, si intenta cargar la página para el Servicio de aplicaciones, puede recibir un error 403.</span><span class="sxs-lookup"><span data-stu-id="61f0f-154">At this point, if you try and load the page for the app service, you may receive a 403 error.</span></span> <span data-ttu-id="61f0f-155">En este ejemplo, se debe a que no hay ninguna configuración de documentos predeterminada típica para la página, como por ejemplo, un archivo como index.htm o default.html.</span><span class="sxs-lookup"><span data-stu-id="61f0f-155">In this example, it is because there is no typical default document setup for the page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="61f0f-156">Puede resolverlo rápidamente con las herramientas del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="61f0f-156">You can quickly remedy this with the tooling in the Azure Portal.</span></span>  <span data-ttu-id="61f0f-157">En Azure Portal, elija Configuración &gt; Configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61f0f-157">In the Azure Portal choose Settings &gt; Application Settings.</span></span>
    
     ![imagen13][image13]
14. <span data-ttu-id="61f0f-159">Se abre una hoja de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61f0f-159">A blade opens for application settings.</span></span> <span data-ttu-id="61f0f-160">Escriba el nombre de la página ,"SamplePage.html", y haga clic en Guardar.</span><span class="sxs-lookup"><span data-stu-id="61f0f-160">Enter the name of the page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="61f0f-161">Dedique unos minutos a explorar los demás valores.</span><span class="sxs-lookup"><span data-stu-id="61f0f-161">Take a few minutes to explore the other settings.</span></span>
    
    ![imagen14][image14]
15. <span data-ttu-id="61f0f-163">Si lo desea, actualice la dirección URL del explorador para asegurarse de que ver los cambios previstos.</span><span class="sxs-lookup"><span data-stu-id="61f0f-163">Optionally refresh your browser URL to ensure you see the expected changes.</span></span> <span data-ttu-id="61f0f-164">En este caso, ahora hay algún texto simple en la página.</span><span class="sxs-lookup"><span data-stu-id="61f0f-164">In this case, there is some simple text now populating the page.</span></span> <span data-ttu-id="61f0f-165">Cada cambio adicional en el repositorio dará como resultado una nueva implementación automática.</span><span class="sxs-lookup"><span data-stu-id="61f0f-165">Each additional change to the repository would result in a new automatic deployment.</span></span>
    
    ![imagen15][image15]
    
    <span data-ttu-id="61f0f-167">Habilitar la implementación continua con el Portal de Azure es sencillo.</span><span class="sxs-lookup"><span data-stu-id="61f0f-167">Enabling continuous deployment with the Azure Portal is an easy experience.</span></span> <span data-ttu-id="61f0f-168">También puede crear canalizaciones de entrega de versiones más complejas y usar muchas otras técnicas con el control de origen existente y sistemas de integración continua para implementar en Azure, como aprovechar la generación automatizada y los sistemas de administración de versiones.</span><span class="sxs-lookup"><span data-stu-id="61f0f-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems to deploy to Azure, such as leveraging automated build and release management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="61f0f-169">Desarrollo y prueba de una aplicación</span><span class="sxs-lookup"><span data-stu-id="61f0f-169">Develop and test an app</span></span>
<span data-ttu-id="61f0f-170">A continuación, realice algunos cambios en el código base e implemente rápidamente los cambios.</span><span class="sxs-lookup"><span data-stu-id="61f0f-170">Next, make some changes to the code base and rapidly deploy those changes.</span></span> <span data-ttu-id="61f0f-171">También configurará algunas pruebas de rendimiento para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="61f0f-171">You will also setup up some performance testing for the Web app.</span></span>

1. <span data-ttu-id="61f0f-172">En el panel de navegación del Portal de Azure, elija Servicios de aplicaciones y busque el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="61f0f-172">In the Azure Portal choose App Services from the navigation pane, and locate your App Service.</span></span>
   
   ![imagen16][image16]
2. <span data-ttu-id="61f0f-174">Haga clic en Herramientas.</span><span class="sxs-lookup"><span data-stu-id="61f0f-174">Click Tools</span></span>
   
   ![imagen17][image17]
3. <span data-ttu-id="61f0f-176">Observe la categoría de desarrollo en Herramientas.</span><span class="sxs-lookup"><span data-stu-id="61f0f-176">Notice the develop category under Tools.</span></span> <span data-ttu-id="61f0f-177">Hay varias herramientas útiles aquí que nos permiten trabajar con aplicaciones sin salir del Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="61f0f-177">There are several useful tools here that allow us to work with apps without leaving the Azure Portal.</span></span> <span data-ttu-id="61f0f-178">Haga clic en Consola.</span><span class="sxs-lookup"><span data-stu-id="61f0f-178">Click on Console.</span></span>
   
   ![imagen18][image18]
4. <span data-ttu-id="61f0f-180">En la ventana de la consola, puede emitir comandos dinámicos para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61f0f-180">In the console window, you can issue live commands for your app.</span></span> <span data-ttu-id="61f0f-181">Escriba el comando dir y presione Entrar.</span><span class="sxs-lookup"><span data-stu-id="61f0f-181">Type the dir command and hit enter.</span></span> <span data-ttu-id="61f0f-182">Observe que los comandos que requieren privilegios elevados no funcionan.</span><span class="sxs-lookup"><span data-stu-id="61f0f-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![imagen19][image19]
5. <span data-ttu-id="61f0f-184">Vuelva a la categoría Desarrollo y elija Visual Studio Online.</span><span class="sxs-lookup"><span data-stu-id="61f0f-184">Move back to the Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="61f0f-185">Nota: Visual Studio Online ahora se llama Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="61f0f-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span></span>
   
   ![imagen20][image20]
6. <span data-ttu-id="61f0f-187">Active la experiencia de edición en el explorador para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61f0f-187">Toggle on the in-browser editing experience for your App.</span></span>
   
   ![imagen21][image21]
7. <span data-ttu-id="61f0f-189">Se instala una extensión web para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61f0f-189">A web extension installs for your app.</span></span> <span data-ttu-id="61f0f-190">Las extensiones agregan funcionalidades a las aplicaciones de Azure de forma rápida y sencilla.</span><span class="sxs-lookup"><span data-stu-id="61f0f-190">Extensions quickly and easily add functionality to apps in Azure.</span></span> <span data-ttu-id="61f0f-191">Observe algunos de los otros tipos de extensión disponibles en la siguiente captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="61f0f-191">Notice some of the other extension types available in the screenshot below.</span></span>
   
   ![imagen22][image22]
8. <span data-ttu-id="61f0f-193">Una vez instalada la extensión Visual Studio Online, haga clic en Ir.</span><span class="sxs-lookup"><span data-stu-id="61f0f-193">Once the Visual Studio Online extension installs, click Go.</span></span>
   
   ![imagen23][image23]
9. <span data-ttu-id="61f0f-195">Se abre una pestaña del explorador donde verá un IDE de desarrollo directamente en el explorador.</span><span class="sxs-lookup"><span data-stu-id="61f0f-195">A browser tab opens where you see a development IDE directly in the browser.</span></span> <span data-ttu-id="61f0f-196">Tenga en cuenta que la siguiente experiencia está en Chrome.</span><span class="sxs-lookup"><span data-stu-id="61f0f-196">Notice the experience below is in Chrome.</span></span>
   
   ![imagen24][image24]
10. <span data-ttu-id="61f0f-198">Puede realizar varias actividades, tales como editar archivos, agregar archivos y carpetas, y descargar contenido desde el sitio activo.</span><span class="sxs-lookup"><span data-stu-id="61f0f-198">You can perform several activities such as edit files, add files and folders, and download content from the live site.</span></span> <span data-ttu-id="61f0f-199">Realice una operación de edición rápida en el archivo SamplePage.html.</span><span class="sxs-lookup"><span data-stu-id="61f0f-199">Make a quick edit to the SamplePage.html file.</span></span>
    
    ![imagen25][image25]
11. <span data-ttu-id="61f0f-201">En unos momentos, los cambios se guardan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="61f0f-201">In a few moments, the changes are automatically saved.</span></span> <span data-ttu-id="61f0f-202">Si vuelve a la página, puede ver los cambios.</span><span class="sxs-lookup"><span data-stu-id="61f0f-202">If you navigate back to the page, you can see the changes.</span></span> <span data-ttu-id="61f0f-203">Tenga en cuenta que es muy posible que las modificaciones dinámicas como estas no sean adecuadas para entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="61f0f-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="61f0f-204">Sin embargo, las herramientas hacen que sea muy fácil realizar cambios rápidos para entornos de prueba y desarrollo.</span><span class="sxs-lookup"><span data-stu-id="61f0f-204">However, the tools make it very easy to make quick changes for dev and test environments.</span></span>
    
    ![imagen26][image26]
    
    ![imagen27][image27]
12. <span data-ttu-id="61f0f-207">Vuelva a la hoja de herramientas y, en la categoría Desarrollo, haga clic en Prueba de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="61f0f-207">Move back to the tools blade and under the Develop category, click on Performance Test.</span></span>
    
    ![imagen28][image28]
13. <span data-ttu-id="61f0f-209">Debe establecer una cuenta de servicios del equipo.</span><span class="sxs-lookup"><span data-stu-id="61f0f-209">You need to set a team services account.</span></span> <span data-ttu-id="61f0f-210">Consulte aquí para ver más detalles: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span><span class="sxs-lookup"><span data-stu-id="61f0f-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span></span>
14. <span data-ttu-id="61f0f-211">Haga clic en Nuevo para crear una prueba de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="61f0f-211">Click on New to create a performance test.</span></span>
    
    ![imagen29][image29]
    
    <span data-ttu-id="61f0f-213">Configure los diversos valores y haga clic en Ejecutar prueba, en la parte inferior del cuadro de diálogo, para iniciar una prueba de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="61f0f-213">Configure the various values and click Run Test at the bottom of the dialogue to initiate a performance test.</span></span>
    
    ![imagen30][image30]
    
    ![imagen31][image31]
15. <span data-ttu-id="61f0f-216">Una vez que la prueba comienza a ejecutarse, puede supervisar el estado.</span><span class="sxs-lookup"><span data-stu-id="61f0f-216">Once the test starts running, you can monitor the state.</span></span>
    
    ![imagen32][image32]
    
    <span data-ttu-id="61f0f-218">Una vez finalizada la prueba, al hacer clic en el resultado se muestran más detalles.</span><span class="sxs-lookup"><span data-stu-id="61f0f-218">Once the test finishes, clicking on the result shows more details.</span></span>
    
    ![imagen33][image33]
16. <span data-ttu-id="61f0f-220">En este ejemplo, ha creado la ejecución de una pequeña prueba, por lo que los datos que se analizarán son limitados, pero se pueden ver varias métricas, así como volver a ejecutar la prueba desde esta vista.</span><span class="sxs-lookup"><span data-stu-id="61f0f-220">In this example, you created a small test run, so there is limited data to analyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="61f0f-221">Gracias al Portal de Azure, el proceso de crear, ejecutar y analizar pruebas de rendimiento web es fácil.</span><span class="sxs-lookup"><span data-stu-id="61f0f-221">The Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="61f0f-222">Las siguientes capturas de pantalla muestran los datos de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="61f0f-222">The screenshots below display the performance data.</span></span>
    
    ![imagen34][image34]
    
    ![imagen35][image35]
    
    ![imagen36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="61f0f-226">Supervisión y solución de problemas de una aplicación</span><span class="sxs-lookup"><span data-stu-id="61f0f-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="61f0f-227">Azure proporciona muchas funcionalidades de supervisión y solución de problemas de las aplicaciones que se ejecutan.</span><span class="sxs-lookup"><span data-stu-id="61f0f-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="61f0f-228">En el Portal de Azure para nuestra aplicación web, elija Herramientas.</span><span class="sxs-lookup"><span data-stu-id="61f0f-228">In the Azure Portal for our Web app choose Tools.</span></span>
   
   ![imagen37][image37]
2. <span data-ttu-id="61f0f-230">En la categoría Solucionar problemas, observe las diversas opciones para utilizar las herramientas con el fin de solucionar posibles problemas con una aplicación en ejecución.</span><span class="sxs-lookup"><span data-stu-id="61f0f-230">Under the Troubleshoot category, notice the various choices for using tools to troubleshoot potential issues with a running app.</span></span> <span data-ttu-id="61f0f-231">Puede hacer cosas como supervisar el tráfico HTTP dinámico, habilitar la recuperación automática, ver registros, etc.</span><span class="sxs-lookup"><span data-stu-id="61f0f-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![imagen38][image38]
3. <span data-ttu-id="61f0f-233">Elija Métricas del sitio para obtener rápidamente una vista de algunos códigos HTTP.</span><span class="sxs-lookup"><span data-stu-id="61f0f-233">Choose Site Metrics to quickly get a view of some HTTP codes.</span></span>
   
   ![imagen39][image39]
4. <span data-ttu-id="61f0f-235">Elija Diagnóstico como el Servicio.</span><span class="sxs-lookup"><span data-stu-id="61f0f-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="61f0f-236">Elija el tipo de aplicación, a continuación, Ejecutar.</span><span class="sxs-lookup"><span data-stu-id="61f0f-236">Choose your application type, then choose Run.</span></span>
   
   ![imagen40][image40]
   
   <span data-ttu-id="61f0f-238">Comienza una recopilación.</span><span class="sxs-lookup"><span data-stu-id="61f0f-238">A collection begins.</span></span>
   
   ![imagen41][image41]
5. <span data-ttu-id="61f0f-240">Puede elegir el registro adecuado para diagnosticar posibles problemas.</span><span class="sxs-lookup"><span data-stu-id="61f0f-240">You may choose the appropriate log to diagnose potential issues.</span></span> <span data-ttu-id="61f0f-241">Debe habilitar el registro para ver todas las opciones de datos disponibles, como los registros de HTTP.</span><span class="sxs-lookup"><span data-stu-id="61f0f-241">You need to enable logging to see all of the available data options such as HTTP Logs.</span></span>
   
   ![imagen42][image42]
   
   <span data-ttu-id="61f0f-243">Para descargar y analizar un informe de análisis DebugDiag que ayuda a encontrar posibles problemas, haga clic en el archivo de volcado de memoria.</span><span class="sxs-lookup"><span data-stu-id="61f0f-243">By clicking on the Memory Dump file you can download and analyze a DebugDiag analysis report to help find potential issues.</span></span>
   
   ![imagen43][image43]
6. <span data-ttu-id="61f0f-245">Para ver más datos, debe habilitar el registro adicional.</span><span class="sxs-lookup"><span data-stu-id="61f0f-245">To view more data, you need to enable additional logging.</span></span> <span data-ttu-id="61f0f-246">En el Portal de Azure, vaya a la aplicación web y elija Configuración.</span><span class="sxs-lookup"><span data-stu-id="61f0f-246">In the Azure Portal, navigate to the Web app and choose Settings.</span></span>
   
   ![imagen44][image44]
7. <span data-ttu-id="61f0f-248">Desplácese a la categoría de características y elija Registros de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="61f0f-248">Scroll down to the features category, and choose Diagnostic logs.</span></span>
   
      ![imagen45][image45]
8. <span data-ttu-id="61f0f-250">Observe las diversas opciones para el registro.</span><span class="sxs-lookup"><span data-stu-id="61f0f-250">Notice the various options for logging.</span></span> <span data-ttu-id="61f0f-251">Active el registro del servidor web y haga clic en Guardar.</span><span class="sxs-lookup"><span data-stu-id="61f0f-251">Toggle on Web server logging and click save.</span></span>
   
   ![imagen46][image46]
9. <span data-ttu-id="61f0f-253">Vuelva al área de herramientas de la aplicación y elija Diagnóstico como un servicio y haga clic en Ejecutar para volver a ejecutar la recopilación de datos.</span><span class="sxs-lookup"><span data-stu-id="61f0f-253">Move back to the tools area for the app and choose Diagnostics as a service and click Run to rerun the data collection.</span></span>
   
   ![imagen47][image47]
10. <span data-ttu-id="61f0f-255">Con la opción de registro de HTTP habilitada, ahora verá los datos recopilados para los registros de HTTP.</span><span class="sxs-lookup"><span data-stu-id="61f0f-255">With the HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![imagen48][image48]
11. <span data-ttu-id="61f0f-257">Al hacer clic en el registro de archivos HTML se genera un completo informe basado en explorador para una investigación más detallada.</span><span class="sxs-lookup"><span data-stu-id="61f0f-257">By clicking the HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![imagen49][image49]
12. <span data-ttu-id="61f0f-259">Vuelva a la sección de herramientas en el Portal de Azure para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61f0f-259">Move back to the tools section in the Azure Portal for the app.</span></span> <span data-ttu-id="61f0f-260">Desplácese a la sección Herramientas y elija Explorador de procesos.</span><span class="sxs-lookup"><span data-stu-id="61f0f-260">Scroll to the Tools section and choose Process Explorer.</span></span>
    
    ![imagen50][image50]
13. <span data-ttu-id="61f0f-262">Al elegir Explorador de procesos, puede ver detalles sobre los procesos en ejecución.</span><span class="sxs-lookup"><span data-stu-id="61f0f-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="61f0f-263">Observe a continuación que puede profundizar en los procesos e incluso terminarlos todos desde el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="61f0f-263">Notice below you can drill into processes and even kill processes all from the Azure Portal.</span></span>
    
    ![imagen51][image51]
    
    ![imagen52][image52]
14. <span data-ttu-id="61f0f-266">Vuelva a la hoja Configuración, situada a la izquierda.</span><span class="sxs-lookup"><span data-stu-id="61f0f-266">Move back to the Settings blade on the left.</span></span> <span data-ttu-id="61f0f-267">Haga clic en Nueva solicitud de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="61f0f-267">Click New support request.</span></span>
    
    ![imagen53][image53]
15. <span data-ttu-id="61f0f-269">En la hoja de la derecha, puede rellenar los detalles acerca de los problemas, escribir la información de contacto e incluso cargar datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="61f0f-269">From the blade on the right, you can fill out details about the issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="61f0f-270">Gracias al Portal de Azure, trabajar con el soporte técnico de Microsoft es una experiencia perfecta.</span><span class="sxs-lookup"><span data-stu-id="61f0f-270">The Azure Portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![imagen54][image54]
    
    ![imagen55][image55]
    
    <span data-ttu-id="61f0f-273">El Portal de Azure ayuda a proporcionar experiencias de herramientas eficaces y familiares para ayudarle a supervisar y solucionar problemas de nuestras aplicaciones en ejecución.</span><span class="sxs-lookup"><span data-stu-id="61f0f-273">The Azure Portal helps provide powerful and familiar tooling experiences to help monitor and troubleshoot our running applications.</span></span> <span data-ttu-id="61f0f-274">También es posible tomar medidas rápidamente mediante la realización de tareas como reciclar procesos, habilitar y deshabilitar diversas colecciones de datos e incluso realizar la integración con el soporte técnico profesional de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="61f0f-274">You are also able to take action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="61f0f-275">Administración general de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="61f0f-275">General Application Management</span></span>
<span data-ttu-id="61f0f-276">Al administrar aplicaciones, a menudo necesitará realizar una amplia serie de actividades, como la configuración de estrategias de copia de seguridad, la implementación y administración de proveedores de identidades y la configuración de control de acceso basado en roles.</span><span class="sxs-lookup"><span data-stu-id="61f0f-276">When managing applications, you often need to perform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="61f0f-277">Al igual que con otras experiencias de DevOps, la plataforma Azure integra estas tareas directamente en el portal.</span><span class="sxs-lookup"><span data-stu-id="61f0f-277">As with the other DevOps experiences, the Azure platform integrates these tasks directly into the portal.</span></span>

1. <span data-ttu-id="61f0f-278">Para mantener segura la aplicación web frente a la pérdida de datos debe configurar copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="61f0f-278">To ensure you are keeping the Web App safe from data loss you need to configure backups.</span></span> <span data-ttu-id="61f0f-279">Vaya al área Configuración de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="61f0f-279">Navigate to the Settings area for your Web app.</span></span>
   
   ![imagen56][image56]
2. <span data-ttu-id="61f0f-281">En la hoja de la derecha, desplácese a la categoría Características.</span><span class="sxs-lookup"><span data-stu-id="61f0f-281">In the blade on the right, scroll down to the Features category.</span></span>
   
    ![imagen57][image57]
3. <span data-ttu-id="61f0f-283">Elija Copias de seguridad; se abre una hoja a la derecha.</span><span class="sxs-lookup"><span data-stu-id="61f0f-283">Choose Backups; a blade opens on the right.</span></span>
   
   ![imagen58][image58]
4. <span data-ttu-id="61f0f-285">Haga clic en Configurar, elija una cuenta de almacenamiento en la hoja de la derecha.</span><span class="sxs-lookup"><span data-stu-id="61f0f-285">Click Configure, choose a storage account from the blade on the right.</span></span>
   
   ![imagen59][image59]
5. <span data-ttu-id="61f0f-287">Ahora cree y elija un contenedor de almacenamiento para guardar las copias de seguridad.</span><span class="sxs-lookup"><span data-stu-id="61f0f-287">Now create and choose a storage container to hold your backups.</span></span> <span data-ttu-id="61f0f-288">Haga clic en Crear en la parte inferior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="61f0f-288">Click create at the bottom of the blade.</span></span> <span data-ttu-id="61f0f-289">A continuación, seleccione el contenedor.</span><span class="sxs-lookup"><span data-stu-id="61f0f-289">Then select the container.</span></span>
   
   ![imagen60][image60]
6. <span data-ttu-id="61f0f-291">Una vez elegido el contenedor, puede configurar las programaciones y las copias de seguridad de las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="61f0f-291">Once you have chosen the container, you can configure schedules, as well as setup backups for your databases.</span></span> <span data-ttu-id="61f0f-292">En este escenario, haga clic en el icono Guardar.</span><span class="sxs-lookup"><span data-stu-id="61f0f-292">For this scenario, click the save icon.</span></span>
   
    ![imagen61][image61]
7. <span data-ttu-id="61f0f-294">Después de guardar, desplácese a Copias de seguridad, en la hoja de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="61f0f-294">After saving, scroll back to the blade on the left for Backups.</span></span> <span data-ttu-id="61f0f-295">Haga clic en Realizar copia de seguridad ahora para realizar copias de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61f0f-295">Click Backup Now to back the application.</span></span>
   
    ![imagen62][image62]
8. <span data-ttu-id="61f0f-297">En unos momentos, verá una copia de seguridad creada.</span><span class="sxs-lookup"><span data-stu-id="61f0f-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="61f0f-298">Observe la opción Restaurar ahora en la captura de pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="61f0f-298">Notice the Restore Now option on the screen-shot below.</span></span>
   
    ![imagen63][image63]
9. <span data-ttu-id="61f0f-300">Haga clic en Restaurar ahora y examine las opciones de la hoja de la derecha.</span><span class="sxs-lookup"><span data-stu-id="61f0f-300">Click on Restore Now and examine the options to the blade on the right.</span></span> <span data-ttu-id="61f0f-301">Puede elegir una copia de seguridad adecuada y restaurar fácilmente a un estado anterior según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="61f0f-301">You can choose an appropriate backup and easily restore to an earlier state as necessary.</span></span> <span data-ttu-id="61f0f-302">El Portal de Azure nos ha ayudado a habilitar fácilmente una estrategia de recuperación ante desastres simple para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61f0f-302">The Azure portal has helped us easily enable a simple disaster recovery strategy for the app.</span></span>
   
    ![imagen64][image64]
10. <span data-ttu-id="61f0f-304">Vuelva a la hoja Configuración, situada a la izquierda, y en Características, elija Autenticación/autorización.</span><span class="sxs-lookup"><span data-stu-id="61f0f-304">Move back to the Settings blade on the left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![imagen65][image65]
11. <span data-ttu-id="61f0f-306">En la hoja de la derecha, elija Autenticación del servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="61f0f-306">In the blade on the right choose App Service Authentication.</span></span> <span data-ttu-id="61f0f-307">Observe la variedad de opciones que puede configurar con proveedores conocidos.</span><span class="sxs-lookup"><span data-stu-id="61f0f-307">Notice the variety of options you can configure with popular providers.</span></span>
    
     ![imagen66][image66]
12. <span data-ttu-id="61f0f-309">Elija el proveedor que prefiera y observe las opciones para el ámbito.</span><span class="sxs-lookup"><span data-stu-id="61f0f-309">Choose the provider of your choice and notice the options for the scope.</span></span> <span data-ttu-id="61f0f-310">Puede proporcionar un Id. de la aplicación y un Secreto de la aplicación y habilitar rápidamente la autenticación de Facebook para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61f0f-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for the app.</span></span> <span data-ttu-id="61f0f-311">El Portal de Azure habilita la autenticación como una solución de llave en mano para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="61f0f-311">The Azure Portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![imagen67][image67]
13. <span data-ttu-id="61f0f-313">Vuelva a la hoja Configuración y elija Usuarios en la categoría Administración de recursos.</span><span class="sxs-lookup"><span data-stu-id="61f0f-313">Move back to the Settings blade and choose Users under the Resource Management category.</span></span>
    
     ![imagen68][image68]
14. <span data-ttu-id="61f0f-315">En la hoja de la derecha, examine las diversas opciones para agregar roles y usuarios.</span><span class="sxs-lookup"><span data-stu-id="61f0f-315">In the blade on the right examine the various options for adding roles and users.</span></span> <span data-ttu-id="61f0f-316">El Portal de Azure permite un control fácil de la aplicación mediante RBAC (control de acceso basado en rol).</span><span class="sxs-lookup"><span data-stu-id="61f0f-316">The Azure Portal lets you easily control RBAC (Role-based access control) for the application.</span></span>
    
     ![imagen69][image69]

## <a name="summary"></a><span data-ttu-id="61f0f-318">Resumen</span><span class="sxs-lookup"><span data-stu-id="61f0f-318">Summary</span></span>
<span data-ttu-id="61f0f-319">En este tutorial se muestra parte de la capacidad de la plataforma Azure al habilitar rápidamente la implementación continua para una aplicación web, efectuar diversas actividades de desarrollo y prueba, supervisar y solucionar problemas de una aplicación activa y, por último, administrar estrategias clave como la recuperación ante desastres, identidades y control de acceso basado en roles.</span><span class="sxs-lookup"><span data-stu-id="61f0f-319">This tutorial demonstrated some of the power with the Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="61f0f-320">La plataforma Azure proporciona una experiencia integrada para estos flujos de trabajo de DevOps y permite trabajar eficazmente al permanecer en el contexto para la tarea en cuestión.</span><span class="sxs-lookup"><span data-stu-id="61f0f-320">The Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for the task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61f0f-321">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="61f0f-321">Next steps</span></span>
* <span data-ttu-id="61f0f-322">Azure Resource Manager es importante para habilitar DevOps en la plataforma Azure.</span><span class="sxs-lookup"><span data-stu-id="61f0f-322">Azure Resource Manager is important for enabling DevOps on the Azure platform.</span></span>  <span data-ttu-id="61f0f-323">Para más información, visite [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61f0f-323">To learn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="61f0f-324">Para más información acerca de la implementación del Servicio de aplicaciones de Azure, visite [Documentación de implementación del Servicio de aplicaciones de Azure](../app-service-web/web-sites-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="61f0f-324">To learn more about Azure App Service deployment visit [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md)</span></span>

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
