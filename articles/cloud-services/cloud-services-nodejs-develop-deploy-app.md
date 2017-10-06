---
title: "aaaNode.js Guía de introducción | Documentos de Microsoft"
description: "Conozca cómo toocreate una Node.js simple aplicación web e implementarlo tooan servicio de nube de Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a><span data-ttu-id="a246b-103">Compilar e implementar un tooan de aplicación Node.js servicio de nube de Azure</span><span class="sxs-lookup"><span data-stu-id="a246b-103">Build and deploy a Node.js application tooan Azure Cloud Service</span></span>

<span data-ttu-id="a246b-104">Este tutorial se muestra cómo un simple Node.js toocreate aplicación que se ejecuta en un servicio de nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="a246b-104">This tutorial shows how toocreate a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="a246b-105">Servicios en la nube son bloques de creación de hello de aplicaciones de nube escalables en Azure.</span><span class="sxs-lookup"><span data-stu-id="a246b-105">Cloud Services are hello building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="a246b-106">Permitir la separación de Hola y administración independiente y escalabilidad de los componentes front-end y back-end de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a246b-106">They allow hello separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="a246b-107">Los Servicios en la nube proporcionan una máquina virtual dedicada y robusta para hospedar cada rol de forma fiable.</span><span class="sxs-lookup"><span data-stu-id="a246b-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="a246b-108">Para obtener más información sobre los servicios en la nube, y cómo se comparan tooAzure sitios Web y máquinas virtuales, consulte [comparación de sitios Web de Azure, servicios en la nube y máquinas virtuales].</span><span class="sxs-lookup"><span data-stu-id="a246b-108">For more information on Cloud Services, and how they compare tooAzure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="a246b-109">¿Busca un sitio Web sencillo toobuild?</span><span class="sxs-lookup"><span data-stu-id="a246b-109">Looking toobuild a simple website?</span></span> <span data-ttu-id="a246b-110">Si el escenario solo requiere un sencillo front-end para sitios web, considere la posibilidad de [utilizar una aplicación web ligera].</span><span class="sxs-lookup"><span data-stu-id="a246b-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="a246b-111">Puede actualizar fácilmente tooa servicio en la nube que crezca su aplicación web y cambian sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="a246b-111">You can easily upgrade tooa Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="a246b-112">Siguiendo este tutorial, podrá compilar una aplicación web sencilla hospedada en un rol web.</span><span class="sxs-lookup"><span data-stu-id="a246b-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="a246b-113">Se usen tootest de emulador de proceso de hello su aplicación localmente, a continuación, implementarlo mediante herramientas de línea de comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a246b-113">You will use hello compute emulator tootest your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="a246b-114">aplicación Hello es una sencilla aplicación "Hola a todos":</span><span class="sxs-lookup"><span data-stu-id="a246b-114">hello application is a simple "hello world" application:</span></span>

![Un explorador web Mostrar página web de Hola Hola a todos][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="a246b-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a246b-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="a246b-117">Este tutorial usa PowerShell de Azure, que requiere Windows.</span><span class="sxs-lookup"><span data-stu-id="a246b-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="a246b-118">Instale y configure [Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="a246b-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="a246b-119">Descargue e instale hello [Azure SDK para .NET 2.7].</span><span class="sxs-lookup"><span data-stu-id="a246b-119">Download and install hello [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="a246b-120">Hola, instalar el programa de instalación, seleccione:</span><span class="sxs-lookup"><span data-stu-id="a246b-120">In hello install setup, select:</span></span>
  * <span data-ttu-id="a246b-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="a246b-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="a246b-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="a246b-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="a246b-123">Cree un proyecto del servicio de nube de Azure</span><span class="sxs-lookup"><span data-stu-id="a246b-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="a246b-124">Lleve a cabo Hola después tareas toocreate un nuevo proyecto de servicio de nube de Azure, junto con scaffolding de Node.js básica:</span><span class="sxs-lookup"><span data-stu-id="a246b-124">Perform hello following tasks toocreate a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="a246b-125">Ejecutar **Windows PowerShell** como administrador; de hello **menú Inicio** o **pantalla Inicio**, busque **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="a246b-125">Run **Windows PowerShell** as Administrator; from hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="a246b-126">[Conectar PowerShell] tooyour suscripción.</span><span class="sxs-lookup"><span data-stu-id="a246b-126">[Connect PowerShell] tooyour subscription.</span></span>
3. <span data-ttu-id="a246b-127">Escriba Hola después proyecto Hola de PowerShell cmdlet toocreate toocreate:</span><span class="sxs-lookup"><span data-stu-id="a246b-127">Enter hello following PowerShell cmdlet toocreate toocreate hello project:</span></span>

        New-AzureServiceProject helloworld

    ![resultado de Hello de comando de hello New-AzureService helloworld][hello result of hello New-AzureService helloworld command]

    <span data-ttu-id="a246b-129">Hola **AzureServiceProject New** genera una estructura básica para publicar un tooa de aplicación Node.js servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="a246b-129">hello **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application tooa Cloud Service.</span></span> <span data-ttu-id="a246b-130">Contiene archivos de configuración necesarios para la publicación tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a246b-130">It contains configuration files necessary for publishing tooAzure.</span></span> <span data-ttu-id="a246b-131">cmdlet de Hello también cambia el directorio de toohello del directorio de trabajo para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="a246b-131">hello cmdlet also changes your working directory toohello directory for hello service.</span></span>

    <span data-ttu-id="a246b-132">Hola crea Hola siguientes archivos:</span><span class="sxs-lookup"><span data-stu-id="a246b-132">hello cmdlet creates hello following files:</span></span>

   * <span data-ttu-id="a246b-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** y **ServiceDefinition.csdef**: estos archivos específicos de Azure son necesarios para publicar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a246b-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="a246b-134">Para obtener más información, consulte [Información general de la creación de un servicio hospedado para Azure].</span><span class="sxs-lookup"><span data-stu-id="a246b-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="a246b-135">**deploymentSettings.json**: almacena la configuración local que se usa por hello cmdlets de implementación de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a246b-135">**deploymentSettings.json**: Stores local settings that are used by hello Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="a246b-136">Escriba Hola después comando tooadd un nuevo rol web:</span><span class="sxs-lookup"><span data-stu-id="a246b-136">Enter hello following command tooadd a new web role:</span></span>

       Add-AzureNodeWebRole

   ![salida de Hello de hello comando Add-AzureNodeWebRole][hello output of hello Add-AzureNodeWebRole command]

   <span data-ttu-id="a246b-138">Hola **Add-AzureNodeWebRole** crea una aplicación básica de Node.js.</span><span class="sxs-lookup"><span data-stu-id="a246b-138">hello **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="a246b-139">También modifica hello **. csfg** y **.csdef** tooadd entradas de configuración para el nuevo rol de Hola de archivos.</span><span class="sxs-lookup"><span data-stu-id="a246b-139">It also modifies hello **.csfg** and **.csdef** files tooadd configuration entries for hello new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a246b-140">Si no especifica un nombre de rol, se usa el nombre predeterminado.</span><span class="sxs-lookup"><span data-stu-id="a246b-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="a246b-141">Puede proporcionar un nombre como primer parámetro de cmdlet hello:`Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="a246b-141">You can provide a name as hello first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="a246b-142">aplicación Node.js de Hello se define en el archivo hello **server.js**, ubicada en el directorio de hello para el rol web de hello (**WebRole1** de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="a246b-142">hello Node.js app is defined in hello file **server.js**, located in hello directory for hello web role (**WebRole1** by default).</span></span> <span data-ttu-id="a246b-143">Este es el código de hello.</span><span class="sxs-lookup"><span data-stu-id="a246b-143">Here is hello code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="a246b-144">Este código es básicamente Hola igual Hola "¡Hello World" de ejemplo de Hola [nodejs.org] sitio Web, excepto en que utiliza el número de puerto de hello asignado por el entorno de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="a246b-144">This code is essentially hello same as hello "Hello World" sample on hello [nodejs.org] website, except it uses hello port number assigned by hello cloud environment.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="a246b-145">Implementar Hola aplicación tooAzure</span><span class="sxs-lookup"><span data-stu-id="a246b-145">Deploy hello application tooAzure</span></span>

> [!NOTE]
> <span data-ttu-id="a246b-146">toocomplete este tutorial, necesita una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="a246b-146">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="a246b-147">Puede [activar sus beneficios de suscriptor a MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) o [registrarse para obtener una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span><span class="sxs-lookup"><span data-stu-id="a246b-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-hello-azure-publishing-settings"></a><span data-ttu-id="a246b-148">Descargar hello Azure configuración de publicación</span><span class="sxs-lookup"><span data-stu-id="a246b-148">Download hello Azure publishing settings</span></span>
<span data-ttu-id="a246b-149">toodeploy tooAzure de su aplicación, primero debe descargar Hola publicar la configuración de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a246b-149">toodeploy your application tooAzure, you must first download hello publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="a246b-150">Ejecute hello siguiente cmdlet de PowerShell de Azure:</span><span class="sxs-lookup"><span data-stu-id="a246b-150">Run hello following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="a246b-151">Esto va a usar el explorador toonavigate toohello publicar la página de descarga de configuración.</span><span class="sxs-lookup"><span data-stu-id="a246b-151">This will use your browser toonavigate toohello publish settings download page.</span></span> <span data-ttu-id="a246b-152">Es posible que toolog solicitada con una Account de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a246b-152">You may be prompted toolog in with a Microsoft Account.</span></span> <span data-ttu-id="a246b-153">Si es así, usar cuenta de hello asociada con su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a246b-153">If so, use hello account associated with your Azure subscription.</span></span>

   <span data-ttu-id="a246b-154">Guardar Hola descarga puedan acceder fácilmente a la ubicación del archivo tooa de perfil.</span><span class="sxs-lookup"><span data-stu-id="a246b-154">Save hello downloaded profile tooa file location you can easily access.</span></span>
2. <span data-ttu-id="a246b-155">Ejecutar la siguiente cmdlet tooimport Hola descargó el perfil de publicación:</span><span class="sxs-lookup"><span data-stu-id="a246b-155">Run following cmdlet tooimport hello publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > <span data-ttu-id="a246b-156">Después de importar hello, configuración de publicación, considere la posibilidad de eliminar Hola descargado el archivo .publishSettings, ya que contiene información que podría permitir que alguien tooaccess tu cuenta.</span><span class="sxs-lookup"><span data-stu-id="a246b-156">After importing hello publish settings, consider deleting hello downloaded .publishSettings file, because it contains information that could allow someone tooaccess your account.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="a246b-157">Publicar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="a246b-157">Publish hello application</span></span>
<span data-ttu-id="a246b-158">toopublish, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a246b-158">toopublish, run hello following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="a246b-159">**-ServiceName** especifica el nombre de hello para la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a246b-159">**-ServiceName** specifies hello name for hello deployment.</span></span> <span data-ttu-id="a246b-160">Debe ser un nombre único, de lo contrario Hola publicar proceso producirá un error.</span><span class="sxs-lookup"><span data-stu-id="a246b-160">This must be a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="a246b-161">Hola **Get-Date** elementos de fijación de comando en una cadena de fecha y hora que debe realizar nombre hello único.</span><span class="sxs-lookup"><span data-stu-id="a246b-161">hello **Get-Date** command tacks on a date/time string that should make hello name unique.</span></span>
* <span data-ttu-id="a246b-162">**-Location** especifica el centro de datos de Hola que se hospedará la aplicación hello en.</span><span class="sxs-lookup"><span data-stu-id="a246b-162">**-Location** specifies hello datacenter that hello application will be hosted in.</span></span> <span data-ttu-id="a246b-163">una lista de centros de datos disponibles, utilice hello toosee **AzureLocation Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a246b-163">toosee a list of available datacenters, use hello **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="a246b-164">**-Ejecute** abre una ventana del explorador y navega toohello hospedado servicio una vez completada la implementación.</span><span class="sxs-lookup"><span data-stu-id="a246b-164">**-Launch** opens a browser window and navigates toohello hosted service after deployment has completed.</span></span>

<span data-ttu-id="a246b-165">Después de la publicación se realiza correctamente, verá un siguiente toohello similar de respuesta:</span><span class="sxs-lookup"><span data-stu-id="a246b-165">After publishing succeeds, you will see a response similar toohello following:</span></span>

![salida de Hello de hello comando Publish-AzureService][hello output of hello Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="a246b-167">Puede tardar varios minutos para toodeploy de aplicación hello y están disponible cuando se publicó por primera vez.</span><span class="sxs-lookup"><span data-stu-id="a246b-167">It can take several minutes for hello application toodeploy and become available when first published.</span></span>

<span data-ttu-id="a246b-168">Cuando haya completado la implementación de hello, una ventana del explorador abrirá y navegar por el servicio en la nube toohello.</span><span class="sxs-lookup"><span data-stu-id="a246b-168">Once hello deployment has completed, a browser window will open and navigate toohello cloud service.</span></span>

![Una ventana del explorador mostrar hello hello world página; dirección URL de Hello indica página Hola se hospeda en Azure.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

<span data-ttu-id="a246b-170">La aplicación ya se está ejecutando en Azure.</span><span class="sxs-lookup"><span data-stu-id="a246b-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="a246b-171">Hola **AzureServiceProject publicar** cmdlet realiza Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="a246b-171">hello **Publish-AzureServiceProject** cmdlet performs hello following steps:</span></span>

1. <span data-ttu-id="a246b-172">Crea un paquete toodeploy.</span><span class="sxs-lookup"><span data-stu-id="a246b-172">Creates a package toodeploy.</span></span> <span data-ttu-id="a246b-173">paquete de Hello contiene todos los archivos de hello en la carpeta de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a246b-173">hello package contains all hello files in your application folder.</span></span>
2. <span data-ttu-id="a246b-174">Crea una nueva **cuenta de almacenamiento** si no hay ninguna disponible.</span><span class="sxs-lookup"><span data-stu-id="a246b-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="a246b-175">Hola cuenta de almacenamiento de Azure es paquete de aplicación Hola toostore usado durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="a246b-175">hello Azure storage account is used toostore hello application package during deployment.</span></span> <span data-ttu-id="a246b-176">Puede eliminar cuenta de almacenamiento de hello después de que se realice la implementación.</span><span class="sxs-lookup"><span data-stu-id="a246b-176">You can safely delete hello storage account after deployment is done.</span></span>
3. <span data-ttu-id="a246b-177">Crea un nuevo **servicio en la nube** si no hay ninguno disponible.</span><span class="sxs-lookup"><span data-stu-id="a246b-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="a246b-178">A **servicio en la nube** es contenedor hello en el que se hospeda la aplicación cuando está implementado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a246b-178">A **cloud service** is hello container in which your application is hosted when it is deployed tooAzure.</span></span> <span data-ttu-id="a246b-179">Para obtener más información, consulte [Información general de la creación de un servicio hospedado para Azure].</span><span class="sxs-lookup"><span data-stu-id="a246b-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="a246b-180">Publica tooAzure de paquete de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a246b-180">Publishes hello deployment package tooAzure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="a246b-181">Detención y eliminación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="a246b-181">Stopping and deleting your application</span></span>
<span data-ttu-id="a246b-182">Después de implementar la aplicación, puede que desee toodisable, por lo que puede evitar costos adicionales.</span><span class="sxs-lookup"><span data-stu-id="a246b-182">After deploying your application, you may want toodisable it so you can avoid extra costs.</span></span> <span data-ttu-id="a246b-183">Azure factura las instancias de rol web por hora consumida de tiempo de servidor.</span><span class="sxs-lookup"><span data-stu-id="a246b-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="a246b-184">Hora del servidor se consume una vez implementada la aplicación, incluso si instancias de hello no se están ejecutando y están en estado de hello detenido.</span><span class="sxs-lookup"><span data-stu-id="a246b-184">Server time is consumed once your application is deployed, even if hello instances are not running and are in hello stopped state.</span></span>

1. <span data-ttu-id="a246b-185">En la ventana de Windows PowerShell de hello, detener la implementación de servicio de hello creado en la sección anterior de hello con hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a246b-185">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="a246b-186">Deteniendo el servicio de hello puede tardar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="a246b-186">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="a246b-187">Cuando se detiene el servicio de hello, recibirá un mensaje que indica que se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="a246b-187">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![estado de saludo del comando de hello Stop-AzureService][hello status of hello Stop-AzureService command]
2. <span data-ttu-id="a246b-189">servicio de hello toodelete, Hola llamada siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a246b-189">toodelete hello service, call hello following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="a246b-190">Cuando se le solicite, escriba **Y** toodelete servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="a246b-190">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="a246b-191">Eliminando el servicio de hello puede tardar varios minutos.</span><span class="sxs-lookup"><span data-stu-id="a246b-191">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="a246b-192">Después de que se ha eliminado el servicio de hello recibirá un mensaje que indica que el servicio de Hola se eliminó.</span><span class="sxs-lookup"><span data-stu-id="a246b-192">After hello service has been deleted you receive a message indicating that hello service was deleted.</span></span>

   ![estado de saludo del comando de hello Remove-AzureService][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="a246b-194">Eliminando el servicio de hello no eliminar la cuenta de almacenamiento de Hola que se creó cuando se publicó inicialmente servicio hello y continuará toobe facturada almacenamiento utilizado.</span><span class="sxs-lookup"><span data-stu-id="a246b-194">Deleting hello service does not delete hello storage account that was created when hello service was initially published, and you will continue toobe billed for storage used.</span></span> <span data-ttu-id="a246b-195">Si nada más usa el almacenamiento de hello, quizá le interese toodelete lo.</span><span class="sxs-lookup"><span data-stu-id="a246b-195">If nothing else is using hello storage, you may want toodelete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a246b-196">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a246b-196">Next steps</span></span>
<span data-ttu-id="a246b-197">Para obtener más información, vea hello [Centro para desarrolladores de Node.js].</span><span class="sxs-lookup"><span data-stu-id="a246b-197">For more information, see hello [Node.js Developer Center].</span></span>

<!-- URL List -->

[comparación de sitios Web de Azure, servicios en la nube y máquinas virtuales]: ../app-service-web/choose-web-site-cloud-service-vm.md
[utilizar una aplicación web ligera]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Azure SDK para .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[Conectar PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Información general de la creación de un servicio hospedado para Azure]: https://azure.microsoft.com/documentation/services/cloud-services/
[Centro para desarrolladores de Node.js]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
