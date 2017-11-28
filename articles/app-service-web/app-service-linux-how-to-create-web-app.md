---
title: "aaaCreate un Azure web de aplicación que se ejecuta en Linux | Documentos de Microsoft"
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
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a><span data-ttu-id="b80e3-104">Creación de una aplicación web de Azure que se ejecute en Linux</span><span class="sxs-lookup"><span data-stu-id="b80e3-104">Create an Azure web app running on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a><span data-ttu-id="b80e3-105">Usar la aplicación web de hello toocreate de portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b80e3-105">Use hello Azure portal toocreate your web app</span></span>
<span data-ttu-id="b80e3-106">Puede empezar a crear la aplicación web en Linux de hello [portal de Azure](https://portal.azure.com) tal como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="b80e3-106">You can start creating your web app on Linux from hello [Azure portal](https://portal.azure.com) as shown in hello following image:</span></span>

![Empezar a crear una aplicación web en hello portal de Azure][1]

<span data-ttu-id="b80e3-108">A continuación, Hola **Crear hoja** abre tal como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="b80e3-108">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![hoja de creación de Hello][2]

1. <span data-ttu-id="b80e3-110">Asigne un nombre a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="b80e3-110">Give your web app a name.</span></span>
2. <span data-ttu-id="b80e3-111">Elija un grupo de recursos existente o cree uno.</span><span class="sxs-lookup"><span data-stu-id="b80e3-111">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="b80e3-112">(Vea las regiones disponibles en hello [sección limitaciones](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="b80e3-112">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="b80e3-113">Seleccione un plan de Azure App Service existente o cree uno.</span><span class="sxs-lookup"><span data-stu-id="b80e3-113">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="b80e3-114">(Vea las notas del plan de servicio de aplicaciones en hello [sección limitaciones](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="b80e3-114">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="b80e3-115">Elija la aplicación hello pila que piensa toouse.</span><span class="sxs-lookup"><span data-stu-id="b80e3-115">Choose hello application stack that you intend toouse.</span></span> <span data-ttu-id="b80e3-116">Puede elegir entre varias versiones de Node.js, PHP, .NET Core y Ruby.</span><span class="sxs-lookup"><span data-stu-id="b80e3-116">You can choose between several versions of Node.js, PHP, .Net Core, and Ruby.</span></span>

<span data-ttu-id="b80e3-117">Una vez haya creado la aplicación hello, puede cambiar la pila de la aplicación hello de configuración de la aplicación hello tal como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="b80e3-117">Once you have created hello app, you can change hello application stack from hello application settings as shown in hello following image:</span></span>

![Configuración de la aplicación][3]

## <a name="deploy-your-web-app"></a><span data-ttu-id="b80e3-119">Implementación de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="b80e3-119">Deploy your web app</span></span>
<span data-ttu-id="b80e3-120">Elegir **opciones de implementación** de proporciona portal de administración de Hola Hola opción toouse local Git o GitHub repositorio toodeploy la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b80e3-120">Choosing **deployment options** from hello management portal gives you hello option toouse local Git or GitHub repository toodeploy your application.</span></span> <span data-ttu-id="b80e3-121">resto de Hola de instrucciones de hello son toothose similar para una aplicación web de Linux no.</span><span class="sxs-lookup"><span data-stu-id="b80e3-121">hello rest of hello instructions are similar toothose for a non-Linux web app.</span></span> <span data-ttu-id="b80e3-122">Puede seguir las instrucciones de hello en [implementación de Git local](app-service-deploy-local-git.md) o [implementación continua](app-service-continuous-deployment.md) toodeploy la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b80e3-122">You can follow hello instructions in [local Git deployment](app-service-deploy-local-git.md) or [continuous deployment](app-service-continuous-deployment.md) toodeploy your app.</span></span>

<span data-ttu-id="b80e3-123">También puede utilizar tooupload FTP en el sitio de tooyour de aplicación.</span><span class="sxs-lookup"><span data-stu-id="b80e3-123">You can also use FTP tooupload your application tooyour site.</span></span> <span data-ttu-id="b80e3-124">Puede obtener el punto de conexión de hello FTP para su aplicación web diagnósticos Hola de sección de registros como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="b80e3-124">You can get hello FTP endpoint for your web app from hello diagnostics logs section as shown in hello following image:</span></span>

![Registros de diagnóstico][4]

## <a name="next-steps"></a><span data-ttu-id="b80e3-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b80e3-126">Next steps</span></span>
* [<span data-ttu-id="b80e3-127">¿Qué es Web App on Linux de Azure?</span><span class="sxs-lookup"><span data-stu-id="b80e3-127">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="b80e3-128">Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="b80e3-128">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="b80e3-129">Uso de Ruby en Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b80e3-129">Using Ruby in Azure App Service Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="b80e3-130">Preguntas más frecuentes sobre Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b80e3-130">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
