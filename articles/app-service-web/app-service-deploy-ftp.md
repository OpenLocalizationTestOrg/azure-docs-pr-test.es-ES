---
title: "Implementación de su aplicación en Azure App Service mediante FTP/S | Microsoft Docs"
description: "Aprenda a implementar la aplicación en Azure App Service mediante FTP o FTPS."
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
ms.openlocfilehash: 9078abbc4ed7eff6975201443992f7bbb84bf57c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-your-app-to-azure-app-service-using-ftps"></a><span data-ttu-id="5e03d-103">Implementación de la aplicación en Azure App Service mediante FTP/S</span><span class="sxs-lookup"><span data-stu-id="5e03d-103">Deploy your app to Azure App Service using FTP/S</span></span>

<span data-ttu-id="5e03d-104">En este artículo se muestra cómo usar FTP o FTPS para implementar la aplicación web, el back-end de la aplicación móvil o la aplicación de API en [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="5e03d-104">This article shows you how to use FTP or FTPS to deploy your web app, mobile app backend, or API app to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="5e03d-105">El punto de conexión FTP/S de la aplicación ya está activo.</span><span class="sxs-lookup"><span data-stu-id="5e03d-105">The FTP/S endpoint for your app is already active.</span></span> <span data-ttu-id="5e03d-106">No se necesita ninguna configuración para habilitar la implementación de FTP/S.</span><span class="sxs-lookup"><span data-stu-id="5e03d-106">No configuration is necessary to enable FTP/S deployment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e03d-107">Continuamente se realizan acciones para mejorar la seguridad de la plataforma Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5e03d-107">We are continuously taking steps to improve Microsoft Azure Platform security.</span></span> <span data-ttu-id="5e03d-108">Como parte de este esfuerzo, se ha planeado la actualización de Aplicaciones web para las regiones de Centro de Alemania y Noreste de Alemania.</span><span class="sxs-lookup"><span data-stu-id="5e03d-108">As part of this ongoing effort an upgrade of Web Applications is planned for Germany Central and Germany Northeast regions.</span></span> <span data-ttu-id="5e03d-109">Durante dicha actualización, Web Apps deshabilitará el uso del protocolo FTP de texto sin formato para las implementaciones.</span><span class="sxs-lookup"><span data-stu-id="5e03d-109">During this Web Apps will be disabling the use of plain text FTP protocol for deployments.</span></span> <span data-ttu-id="5e03d-110">A nuestros clientes les recomendamos que usen FTPS en las implementaciones.</span><span class="sxs-lookup"><span data-stu-id="5e03d-110">Our recommendation to our customers is to switch to FTPS for deployments.</span></span> <span data-ttu-id="5e03d-111">No se espera que se interrumpa el servicio durante esta actualización, que se ha planeado que se realice el 5/9.</span><span class="sxs-lookup"><span data-stu-id="5e03d-111">We do not expect any disruption to your service during this upgrade which is planned for 9/5.</span></span> <span data-ttu-id="5e03d-112">Agradecemos su apoyo en este esfuerzo.</span><span class="sxs-lookup"><span data-stu-id="5e03d-112">We appreciate you support in this effort.</span></span>

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a><span data-ttu-id="5e03d-113">Paso1: Configurar credenciales de implementación</span><span class="sxs-lookup"><span data-stu-id="5e03d-113">Step 1: Set deployment credentials</span></span>

<span data-ttu-id="5e03d-114">Para acceder al servidor FTP de la aplicación, necesita en primer lugar credenciales de implementación.</span><span class="sxs-lookup"><span data-stu-id="5e03d-114">To access the FTP server for your app, you first need deployment credentials.</span></span> 

<span data-ttu-id="5e03d-115">Para establecer o restablecer las credenciales de implementación, consulte [Credenciales de implementación de Azure App Service](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="5e03d-115">To set or reset your deployment credentials, see [Azure App Service Deployment Credentials](app-service-deployment-credentials.md).</span></span> <span data-ttu-id="5e03d-116">Este tutorial muestra el uso de credenciales de nivel de usuario.</span><span class="sxs-lookup"><span data-stu-id="5e03d-116">This tutorial demonstrates the use of user-level credentials.</span></span>

## <a name="step-2-get-ftp-connection-information"></a><span data-ttu-id="5e03d-117">Paso 2: Obtener la información de conexión para FTP</span><span class="sxs-lookup"><span data-stu-id="5e03d-117">Step 2: Get FTP connection information</span></span>

1. <span data-ttu-id="5e03d-118">En [Azure Portal](https://portal.azure.com), abra la [hoja de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources) de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e03d-118">In the [Azure portal](https://portal.azure.com), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="5e03d-119">Seleccione **Información general** en el menú izquierdo y, a continuación, compruebe los valores de **FTP/usuario de implementación**, **Nombre del host FTP** y **Nombre del host FTPS**.</span><span class="sxs-lookup"><span data-stu-id="5e03d-119">Select **Overview** in the left menu, then note the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span> 

    ![Información de conexión FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > <span data-ttu-id="5e03d-121">El valor de usuario **FTP/usuario de implementación** tal como aparece en Azure Portal, incluido el nombre de la aplicación a fin de proporcionar el contexto adecuado para el servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="5e03d-121">The **FTP/Deployment User** user value as displayed by the Azure Portal including the app name in order to provide proper context for the FTP server.</span></span>
    > <span data-ttu-id="5e03d-122">Puede encontrar la misma información si selecciona **Propiedades** en el menú izquierdo.</span><span class="sxs-lookup"><span data-stu-id="5e03d-122">You can find the same information when you select **Properties** in the left menu.</span></span> 
    >
    > <span data-ttu-id="5e03d-123">Además, nunca se muestra la contraseña de la implementación.</span><span class="sxs-lookup"><span data-stu-id="5e03d-123">Also, the deployment password is never shown.</span></span> <span data-ttu-id="5e03d-124">Si olvida la contraseña de la implementación, vuelva al [Paso 1](#step1) y restablézcala.</span><span class="sxs-lookup"><span data-stu-id="5e03d-124">If you forget your deployment password, go back to [step 1](#step1) and reset your deployment password.</span></span>
    >
    >

## <a name="step-3-deploy-files-to-azure"></a><span data-ttu-id="5e03d-125">Paso 3: Implementar archivos en Azure</span><span class="sxs-lookup"><span data-stu-id="5e03d-125">Step 3: Deploy files to Azure</span></span>

1. <span data-ttu-id="5e03d-126">Desde el cliente de FTP ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use la información de conexión recopilada para conectarse a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e03d-126">From your FTP client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), use the connection information you gathered to connect to your app.</span></span>
3. <span data-ttu-id="5e03d-127">Copie los archivos y la estructura de directorio correspondiente al directorio [**/site/wwwroot** ](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure)en Azure (o el directorio **/site/wwwroot/App_Data/Jobs/** para WebJobs).</span><span class="sxs-lookup"><span data-stu-id="5e03d-127">Copy your files and their respective directory structure to the [**/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (or the **/site/wwwroot/App_Data/Jobs/** directory for WebJobs).</span></span>
4. <span data-ttu-id="5e03d-128">Vaya a la dirección URL de la aplicación para comprobar que la aplicación se está ejecutando correctamente.</span><span class="sxs-lookup"><span data-stu-id="5e03d-128">Browse to your app's URL to verify the app is running properly.</span></span> 

> [!NOTE] 
> <span data-ttu-id="5e03d-129">A diferencia de [las implementaciones basadas en Git](app-service-deploy-local-git.md), la implementación de FTP no es compatible con las automatizaciones de implementación siguientes:</span><span class="sxs-lookup"><span data-stu-id="5e03d-129">Unlike [Git-based deployments](app-service-deploy-local-git.md), FTP deployment doesn't support the following deployment automations:</span></span> 
>
> - <span data-ttu-id="5e03d-130">restauración de dependencias (como, por ejemplo, automatizaciones de NuGet, NPM, PIP y Composer)</span><span class="sxs-lookup"><span data-stu-id="5e03d-130">dependency restore (such as NuGet, NPM, PIP, and Composer automations)</span></span>
> - <span data-ttu-id="5e03d-131">compilación de archivos binarios de .NET</span><span class="sxs-lookup"><span data-stu-id="5e03d-131">compilation of .NET binaries</span></span>
> - <span data-ttu-id="5e03d-132">generación del archivo web.config (aquí se muestra un [ejemplo de Node.js](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span><span class="sxs-lookup"><span data-stu-id="5e03d-132">generation of web.config (here is a [Node.js example](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))</span></span>
> 
> <span data-ttu-id="5e03d-133">Debe restaurar, compilar y generar estos archivos necesarios de forma manual en la máquina local e implementarlos junto con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5e03d-133">You must restore, build, and generate these necessary files manually on your local machine and deploy them together with your app.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="5e03d-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5e03d-134">Next steps</span></span>

<span data-ttu-id="5e03d-135">Para ver escenarios de implementación más avanzados, pruebe [Implementación en Azure con Git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="5e03d-135">For more advanced deployment scenarios, try [deploying to Azure with Git](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="5e03d-136">La implementación basada en Git en Azure permite el control de versiones, la restauración de paquetes, MSBuild y mucho más.</span><span class="sxs-lookup"><span data-stu-id="5e03d-136">Git-based deployment to Azure enables version control, package restore, MSBuild, and more.</span></span>

## <a name="more-resources"></a><span data-ttu-id="5e03d-137">Más recursos</span><span class="sxs-lookup"><span data-stu-id="5e03d-137">More Resources</span></span>

* <span data-ttu-id="5e03d-138"><seg>
  [Creación de un sitio web PHP-MySQL e implementación con FTP](web-sites-php-mysql-deploy-use-ftp.md).</seg></span><span class="sxs-lookup"><span data-stu-id="5e03d-138">[Create a PHP-MySQL web app and deploy using FTP](web-sites-php-mysql-deploy-use-ftp.md).</span></span>
* [<span data-ttu-id="5e03d-139">Credenciales de implementación de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="5e03d-139">Azure App Service Deployment Credentials</span></span>](app-service-deploy-ftp.md)
