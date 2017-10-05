---
title: WebJobs en Servicio de aplicaciones de Azure
description: Aprenda a crear WebJobs para ejecutar pruebas en segundo plano, interactuar con servicios como Almacenamiento y Bus de servicio, y crear tareas programadas.
services: app-service
documentationcenter: 
author: christopheranderson
manager: erikre
editor: mollybos
ms.assetid: 85975432-04c9-4b83-b937-b30c082d52a1
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2015
ms.author: chrande
ms.openlocfilehash: 1ca6d2eabe9781a8bb09fc5948ed306e3e8b013c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="6cc76-103">Uso de WebJobs en Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="6cc76-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="6cc76-104">En este artículo se ofrecen vínculos a recursos de documentación sobre cómo usar WebJobs de Azure y el SDK de WebJobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="6cc76-104">This article links to documentation resources about how to use Azure WebJobs and the Azure WebJobs SDK.</span></span> <span data-ttu-id="6cc76-105">WebJobs de Azure proporciona una manera fácil de ejecutar scripts o programas como procesos en segundo plano en [Aplicaciones web del Servicio de aplicaciones](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="6cc76-105">Azure WebJobs provide an easy way to run scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="6cc76-106">Puede cargar y ejecutar un archivo ejecutable como cmd, bat, exe (.NET), ps1, sh, php, py, js y jar.</span><span class="sxs-lookup"><span data-stu-id="6cc76-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="6cc76-107">Estos programas se ejecutan como WebJobs según una programación (cron) o de forma continua.</span><span class="sxs-lookup"><span data-stu-id="6cc76-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="6cc76-108">El SDK de WebJobs facilita el uso del Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="6cc76-108">The WebJobs SDK makes it easier to use Azure Storage.</span></span> <span data-ttu-id="6cc76-109">El SDK de WebJobs tiene un sistema de enlace y desencadenador que funciona con Blobs de almacenamiento, Colas y Tablas de Microsoft Azure, así como con Colas de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="6cc76-109">The WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="6cc76-110">La creación, implementación y administración de WebJobs se realiza de manera fluida gracias al conjunto de herramientas integradas en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6cc76-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="6cc76-111">Puede crear WebJobs a partir de plantillas, así como publicarlos y administrarlos (procesos de ejecución, detención, supervisión o implementación).</span><span class="sxs-lookup"><span data-stu-id="6cc76-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="6cc76-112">El panel de WebJobs en el Portal de Azure proporciona capacidades de administración eficaces que ofrecen un control completo sobre la ejecución de WebJobs, incluida la capacidad para invocar funciones individuales dentro de WebJobs.</span><span class="sxs-lookup"><span data-stu-id="6cc76-112">The WebJobs dashboard in the Azure portal provides powerful management capabilities that give you full control over the execution of WebJobs, including the ability to invoke individual functions within WebJobs.</span></span> <span data-ttu-id="6cc76-113">El panel también muestra los tiempos de ejecución de las funciones y el resultado del registro.</span><span class="sxs-lookup"><span data-stu-id="6cc76-113">The dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

