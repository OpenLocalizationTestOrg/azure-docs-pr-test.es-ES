---
title: "Creación de una aplicación web de Azure que se ejecute en Linux | Microsoft Docs"
description: "Flujo de trabajo de creación de aplicaciones web para Azure Web App en Linux."
keywords: "azure app service, aplicación web, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 49091d4a85bed23927850f9c0bbc5ea8b6e8c9e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="2f356-104">Creación de una aplicación web de Azure que se ejecute en Linux</span><span class="sxs-lookup"><span data-stu-id="2f356-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-the-azure-portal-to-create-your-web-app"></a><span data-ttu-id="2f356-105">Uso de Azure Portal para crear una aplicación web</span><span class="sxs-lookup"><span data-stu-id="2f356-105">Use the Azure portal to create your web app</span></span>
<span data-ttu-id="2f356-106">Puede empezar a crear la aplicación web en Linux desde [Azure Portal](https://portal.azure.com) como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="2f356-106">You can start creating your web app on Linux from the [Azure portal](https://portal.azure.com) as shown in the following image:</span></span>

![Inicio de creación de una aplicación web en Azure Portal][1]

<span data-ttu-id="2f356-108">Aparecerá la hoja de **creación**, como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="2f356-108">Next, the **Create blade** opens as shown in the following image:</span></span>

![Hoja de creación][2]

1. <span data-ttu-id="2f356-110">Asigne un nombre a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="2f356-110">Give your web app a name.</span></span>
2. <span data-ttu-id="2f356-111">Elija un grupo de recursos existente o cree uno.</span><span class="sxs-lookup"><span data-stu-id="2f356-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="2f356-112">(Consulte las regiones disponibles en la [sección de limitaciones](app-service-linux-intro.md)).</span><span class="sxs-lookup"><span data-stu-id="2f356-112">(See available regions in the [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="2f356-113">Seleccione un plan de Azure App Service existente o cree uno.</span><span class="sxs-lookup"><span data-stu-id="2f356-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="2f356-114">(Consulte las notas del plan de App Service en la [sección de limitaciones](app-service-linux-intro.md)).</span><span class="sxs-lookup"><span data-stu-id="2f356-114">(See App Service plan notes in the [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="2f356-115">Elija la pila de aplicaciones que se va a utilizar.</span><span class="sxs-lookup"><span data-stu-id="2f356-115">Choose the application stack that you intend to use.</span></span> <span data-ttu-id="2f356-116">Puede elegir entre varias versiones de Node.js, PHP, .NET Core y Ruby.</span><span class="sxs-lookup"><span data-stu-id="2f356-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="2f356-117">Una vez que haya creado la aplicación, puede cambiar la pila de aplicaciones de la configuración de la aplicación como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="2f356-117">Once you have created the app, you can change the application stack from the application settings as shown in the following image:</span></span>

![Configuración de la aplicación][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="2f356-119">Implementación de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="2f356-119">Deploy your web app</span></span>
<span data-ttu-id="2f356-120">La elección de las **opciones de implementación** en el portal de administración brinda la opción de usar un repositorio de Git o GitHub local para implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f356-120">Choosing **deployment options** from the management portal gives you the option to use local Git or GitHub repository to deploy your application.</span></span> <span data-ttu-id="2f356-121">El resto de las instrucciones son similares a las de una aplicación web que no es de Linux.</span><span class="sxs-lookup"><span data-stu-id="2f356-121">The rest of the instructions are similar to those for a non-Linux web app.</span></span> <span data-ttu-id="2f356-122">Puede seguir las instrucciones descritas en [implementación de Git local](app-service-deploy-local-git.md) o [implementación continua](app-service-continuous-deployment.md) para implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2f356-122">You can follow the instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) to deploy your app.</span></span>

<span data-ttu-id="2f356-123">También puede usar FTP para cargar la aplicación al sitio.</span><span class="sxs-lookup"><span data-stu-id="2f356-123">You can also use FTP to upload your application to your site.</span></span> <span data-ttu-id="2f356-124">En la sección de registros de diagnóstico puede obtener el punto de conexión FTP para la aplicación web, como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="2f356-124">You can get the FTP endpoint for your web app from the diagnostics logs section as shown in the following image:</span></span>

![Registros de diagnóstico][4]

## <a name="next-steps"></a><span data-ttu-id="2f356-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2f356-126">Next steps</span></span>
* [<span data-ttu-id="2f356-127">¿Qué es Web App on Linux de Azure?</span><span class="sxs-lookup"><span data-stu-id="2f356-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="2f356-128">Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="2f356-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="2f356-129">Uso de Ruby en Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="2f356-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="2f356-130">Preguntas más frecuentes sobre Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="2f356-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
