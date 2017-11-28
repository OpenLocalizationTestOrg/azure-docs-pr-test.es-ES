---
title: "aaaUsing Ruby en la aplicación de Web de servicio de aplicación de Azure en Linux | Documentos de Microsoft"
description: Uso de Ruby en Web App on Linux de Azure App Service
keywords: "azure app service, web app, preguntas más frecuentes, linux, oss, ruby"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 45692cb3bf1da9ff65b9466055029bfaef8b7d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a><span data-ttu-id="7c163-104">Uso de Ruby en Web App on Linux</span><span class="sxs-lookup"><span data-stu-id="7c163-104">Using Ruby in Web App on Linux</span></span> #

<span data-ttu-id="7c163-105">Con hello más reciente actualización tooour back-end, se introdujo compatibilidad para v.2.3 Ruby.</span><span class="sxs-lookup"><span data-stu-id="7c163-105">With hello latest update tooour backend, we introduced support for Ruby v.2.3.</span></span> <span data-ttu-id="7c163-106">Establecer la configuración de hello de la aplicación web de Linux, puede cambiar la pila de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="7c163-106">By setting hello configuration of your Linux web app, you can change hello application stack.</span></span>

## <a name="using-hello-azure-portal"></a><span data-ttu-id="7c163-107">Uso de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="7c163-107">Using hello Azure portal</span></span> ##

<span data-ttu-id="7c163-108">En menú nuevo Hola Hola [portal de Azure](https://portal.azure.com), puede elegir toocreate una aplicación Web en Linux Hola Web + opción teléfono móvil como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="7c163-108">From hello new menu in hello [Azure portal](https://portal.azure.com), you can choose toocreate a Web App on Linux from hello Web + Mobile option as shown in hello following image:</span></span>

![Empezar a crear una aplicación web en hello portal de Azure][1]

<span data-ttu-id="7c163-110">A continuación, Hola **Crear hoja** abre tal como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="7c163-110">Next, hello **Create blade** opens as shown in hello following image:</span></span>

![hoja de creación de Hello][2]

1. <span data-ttu-id="7c163-112">Asigne un nombre a la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7c163-112">Give your web app a name.</span></span>
2. <span data-ttu-id="7c163-113">Elija un grupo de recursos existente o cree uno.</span><span class="sxs-lookup"><span data-stu-id="7c163-113">Choose an existing resource group or create a new one.</span></span> <span data-ttu-id="7c163-114">(Vea las regiones disponibles en hello [sección limitaciones](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="7c163-114">(See available regions in hello [limitations section](app-service-linux-intro.md).)</span></span>
3. <span data-ttu-id="7c163-115">Seleccione un plan de Azure App Service existente o cree uno.</span><span class="sxs-lookup"><span data-stu-id="7c163-115">Choose an existing Azure App Service plan or create a new one.</span></span> <span data-ttu-id="7c163-116">(Vea las notas del plan de servicio de aplicaciones en hello [sección limitaciones](app-service-linux-intro.md).)</span><span class="sxs-lookup"><span data-stu-id="7c163-116">(See App Service plan notes in hello [limitations section](app-service-linux-intro.md).)</span></span>
4. <span data-ttu-id="7c163-117">Elija Hola Ruby en las pilas de hello en tiempo de ejecución integrada.</span><span class="sxs-lookup"><span data-stu-id="7c163-117">Choose hello Ruby from hello Built-in Runtime stacks.</span></span>

<span data-ttu-id="7c163-118">Después de que se crea la aplicación web Ruby, puede implementar tooit usando Git o FTP.</span><span class="sxs-lookup"><span data-stu-id="7c163-118">After your Ruby web app gets created, you can deploy tooit using Git or FTP.</span></span>

<span data-ttu-id="7c163-119">toolearn Obtenga más información sobre cómo crear una aplicación Ruby, comprobar hello [Guía de introducción de get](app-service-linux-ruby-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="7c163-119">toolearn more about creating a Ruby app, check hello [get started guide](app-service-linux-ruby-get-started.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c163-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7c163-120">Next steps</span></span>
* [<span data-ttu-id="7c163-121">¿Qué es Web App on Linux?</span><span class="sxs-lookup"><span data-stu-id="7c163-121">What is Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="7c163-122">TooAzure de implementación de Git local servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="7c163-122">Local Git Deployment tooAzure App Service</span></span>](app-service-deploy-local-git.md)
* [<span data-ttu-id="7c163-123">Preguntas más frecuentes sobre Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7c163-123">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)
* [<span data-ttu-id="7c163-124">Creación de una aplicación de Ruby con una aplicación web de Azure en Linux</span><span class="sxs-lookup"><span data-stu-id="7c163-124">Create a Ruby App with Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png