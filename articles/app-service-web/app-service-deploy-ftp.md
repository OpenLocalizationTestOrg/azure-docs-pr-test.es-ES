---
title: "aaaDeploy el servicio de aplicaciones mediante FTP/S de aplicación tooAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodeploy su tooAzure de aplicación mediante el servicio de aplicaciones de FTP o FTPS."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a><span data-ttu-id="49c86-103">Implementar el servicio de aplicaciones mediante FTP/S tooAzure de aplicación</span><span class="sxs-lookup"><span data-stu-id="49c86-103">Deploy your app tooAzure App Service using FTP/S</span></span>

<span data-ttu-id="49c86-104">Este artículo muestra cómo toouse FTP o FTPS toodeploy su aplicación web, una aplicación móvil back-end o una aplicación de API demasiado[servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="49c86-104">This article shows you how toouse FTP or FTPS toodeploy your web app, mobile app backend, or API app too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="49c86-105">punto de conexión de Hello FTP/S para la aplicación ya está activo.</span><span class="sxs-lookup"><span data-stu-id="49c86-105">hello FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="49c86-106">Implementación de necesario tooenable FTP/S no es ninguna configuración.</span><span class="sxs-lookup"><span data-stu-id="49c86-106">No configuration is necessary tooenable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49c86-107">Nos quedamos con continuamente pasos tooimprove seguridad de la plataforma Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="49c86-107">We are continuously taking steps tooimprove Microsoft Azure Platform security.</span></span> <span data-ttu-id="49c86-108">Como parte de este esfuerzo, se ha planeado la actualización de Aplicaciones web para las regiones de Centro de Alemania y Noreste de Alemania.</span><span class="sxs-lookup"><span data-stu-id="49c86-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="49c86-109">Durante esta aplicaciones Web se puede deshabilitar el uso de hello del protocolo de texto sin formato FTP para las implementaciones.</span><span class="sxs-lookup"><span data-stu-id="49c86-109">During this Web Apps will be disabling hello use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="49c86-110">Nuestros clientes de tooour recomendación es tooswitch tooFTPS para las implementaciones.</span><span class="sxs-lookup"><span data-stu-id="49c86-110">Our recommendation tooour customers is tooswitch tooFTPS for deployments.</span></span> <span data-ttu-id="49c86-111">No esperamos que cualquier servicio de tooyour de interrupción durante la actualización se ha planeado 9/5.</span><span class="sxs-lookup"><span data-stu-id="49c86-111">We do not expect any disruption tooyour service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="49c86-112">Agradecemos su apoyo en este esfuerzo.</span><span class="sxs-lookup"><span data-stu-id="49c86-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="49c86-113">Paso1: Configurar credenciales de implementación</span><span class="sxs-lookup"><span data-stu-id="49c86-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="49c86-114">servidor de hello FTP tooaccess para la aplicación, primero debe credenciales de implementación.</span><span class="sxs-lookup"><span data-stu-id="49c86-114">tooaccess hello FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="49c86-115">tooset o restablecer las credenciales de implementación, consulte [credenciales de implementación de servicio de aplicación de Azure](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="49c86-115">tooset or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="49c86-116">Este tutorial muestra el uso de Hola de credenciales de nivel de usuario.</span><span class="sxs-lookup"><span data-stu-id="49c86-116">This tutorial demonstrates hello use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="49c86-117">Paso 2: Obtener la información de conexión para FTP</span><span class="sxs-lookup"><span data-stu-id="49c86-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="49c86-118">Hola [portal de Azure](https://portal.azure.com), abra la aplicación [hoja de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="49c86-118">In hello [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="49c86-119">Seleccione **información general sobre** en el menú izquierdo de hello y, a continuación, tenga en cuenta los valores de hello para **usuario de implementación/FTP**, **nombre de Host FTP**, y **nombre de Host FTPS**.</span><span class="sxs-lookup"><span data-stu-id="49c86-119">Select **Overview** in hello left menu, then note hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![Información de conexión FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="49c86-121">Hola **usuario de implementación/FTP** valor de usuario, como se muestra en Hola Portal de Azure, incluido el nombre de aplicación hello en contexto adecuado de orden tooprovide para servidor hello FTP.</span><span class="sxs-lookup"><span data-stu-id="49c86-121">hello **FTP/Deployment User** user value as displayed by hello Azure Portal including hello app name in order tooprovide proper context for hello FTP server.</span></span>
    > <span data-ttu-id="49c86-122">Puede encontrar Hola la misma información cuando se selecciona **propiedades** en el menú de la izquierda Hola.</span><span class="sxs-lookup"><span data-stu-id="49c86-122">You can find hello same information when you select **Properties** in hello left menu.</span></span> 
    >
    > <span data-ttu-id="49c86-123">Además, nunca se muestra la contraseña de la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="49c86-123">Also, hello deployment password is never shown.</span></span> <span data-ttu-id="49c86-124">Si olvida la contraseña de la implementación, vuelva demasiado[Paso1](#step1) y restablezca la contraseña de la implementación.</span><span class="sxs-lookup"><span data-stu-id="49c86-124">If you forget your deployment password, go back too[step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-tooazure"></a><span data-ttu-id="49c86-125">Paso 3: Implementar archivos tooAzure</span><span class="sxs-lookup"><span data-stu-id="49c86-125">Step 3: Deploy files tooAzure</span></span>

1. <span data-ttu-id="49c86-126">Desde el cliente FTP ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etcetera), use información de conexión de Hola que recopiló tooconnect tooyour aplicación.</span><span class="sxs-lookup"><span data-stu-id="49c86-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use hello connection information you gathered tooconnect tooyour app.</span></span>
3. <span data-ttu-id="49c86-127">Copiar los archivos y su toohello de la estructura de directorios respectivos [ **/sitio/wwwroot** directorio](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) en Azure (o hello **/sitio/wwwroot/App_Data/trabajos/** directorio Trabajos Web).</span><span class="sxs-lookup"><span data-stu-id="49c86-127">Copy your files and their respective directory structure toohello [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or hello **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="49c86-128">Aplicación de la aplicación de exploración tooyour URL tooverify hello se está ejecutando correctamente.</span><span class="sxs-lookup"><span data-stu-id="49c86-128">Browse tooyour app's URL tooverify hello app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="49c86-129">A diferencia de [las implementaciones basadas en Git](app-service-deploy-local-git.md), implementación de FTP no es compatible con hello después automatizaciones de implementación:</span><span class="sxs-lookup"><span data-stu-id="49c86-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support hello following deployment automations:</span></span> 
>
> - <span data-ttu-id="49c86-130">restauración de dependencias (como, por ejemplo, automatizaciones de NuGet, NPM, PIP y Composer)</span><span class="sxs-lookup"><span data-stu-id="49c86-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="49c86-131">compilación de archivos binarios de .NET</span><span class="sxs-lookup"><span data-stu-id="49c86-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="49c86-132">generación del archivo web.config (aquí se muestra un [ejemplo de Node.js](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="49c86-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="49c86-133">Debe restaurar, compilar y generar estos archivos necesarios de forma manual en la máquina local e implementarlos junto con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="49c86-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="49c86-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="49c86-134">Next steps</span></span>

<span data-ttu-id="49c86-135">Para ver escenarios de implementación más avanzados, pruebe [implementar tooAzure con Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="49c86-135">For more advanced deployment scenarios, try [deploying tooAzure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="49c86-136">Implementación basada en GIT tooAzure permite el control de versiones, la restauración del paquete, MSBuild y mucho más.</span><span class="sxs-lookup"><span data-stu-id="49c86-136">Git-based deployment tooAzure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="49c86-137">Más recursos</span><span class="sxs-lookup"><span data-stu-id="49c86-137">More Resources</span></span>

* <span data-ttu-id="49c86-138"><seg>
  [Creación de un sitio web PHP-MySQL e implementación con FTP](web-sites-php-mysql-deploy-use-ftp.md).</seg></span><span class="sxs-lookup"><span data-stu-id="49c86-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="49c86-139">Credenciales de implementación de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="49c86-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
