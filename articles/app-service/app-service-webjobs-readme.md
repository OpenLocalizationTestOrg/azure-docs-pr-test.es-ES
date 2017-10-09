---
title: "aaaWebJobs en el servicio de aplicación de Azure"
description: "Obtenga información acerca de cómo comprueba toobuild WebJobs toorun fondo, interactuar con los servicios como el almacenamiento y el Bus de servicio y crear las tareas programadas."
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
ms.openlocfilehash: 25c24bfe71a64036cd48e58f471995b4a06e3b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-webjobs-in-azure-app-service"></a><span data-ttu-id="5bb91-103">Uso de WebJobs en Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="5bb91-103">Using WebJobs in Azure App Service</span></span>
<span data-ttu-id="5bb91-104">En este artículo se vincula toodocumentation recursos acerca de cómo toouse WebJobs de Azure y Hola SDK de WebJobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="5bb91-104">This article links toodocumentation resources about how toouse Azure WebJobs and hello Azure WebJobs SDK.</span></span> <span data-ttu-id="5bb91-105">WebJobs de Azure proporcionan un secuencias de comandos de toorun de forma sencilla o procesos en segundo plano programas como en [aplicación del servicio de aplicaciones Web](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="5bb91-105">Azure WebJobs provide an easy way toorun scripts or programs as background processes on [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="5bb91-106">Puede cargar y ejecutar un archivo ejecutable como cmd, bat, exe (.NET), ps1, sh, php, py, js y jar.</span><span class="sxs-lookup"><span data-stu-id="5bb91-106">You can upload and run an executable file such as as cmd, bat, exe (.NET), ps1, sh, php, py, js and jar.</span></span> <span data-ttu-id="5bb91-107">Estos programas se ejecutan como WebJobs según una programación (cron) o de forma continua.</span><span class="sxs-lookup"><span data-stu-id="5bb91-107">These programs run as WebJobs on a schedule (cron) or continuously.</span></span>

<span data-ttu-id="5bb91-108">Hola SDK de WebJobs resulta más fácil toouse almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="5bb91-108">hello WebJobs SDK makes it easier toouse Azure Storage.</span></span> <span data-ttu-id="5bb91-109">Hola SDK de WebJobs tiene un enlace y un sistema de desencadenador que funciona con almacenamiento de Blobs de Microsoft Azure, colas y tablas, así como las colas de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="5bb91-109">hello WebJobs SDK has a binding and trigger system which works with Microsoft Azure Storage Blobs, Queues and Tables as well as Service Bus Queues.</span></span>

<span data-ttu-id="5bb91-110">La creación, implementación y administración de WebJobs se realiza de manera fluida gracias al conjunto de herramientas integradas en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5bb91-110">Creating, deploying, and managing WebJobs is seamless with integrated tooling in Visual Studio.</span></span> <span data-ttu-id="5bb91-111">Puede crear WebJobs a partir de plantillas, así como publicarlos y administrarlos (procesos de ejecución, detención, supervisión o implementación).</span><span class="sxs-lookup"><span data-stu-id="5bb91-111">You can create WebJobs from templates, publish, and manage (run/stop/monitor/debug) them.</span></span>

<span data-ttu-id="5bb91-112">panel de WebJobs de Hola Hola portal de Azure proporciona capacidades de administración eficaces que ofrecen un control total sobre la ejecución de Hola de trabajos Web, incluidas capacidad de hello tooinvoke funciones individuales dentro de trabajos Web.</span><span class="sxs-lookup"><span data-stu-id="5bb91-112">hello WebJobs dashboard in hello Azure portal provides powerful management capabilities that give you full control over hello execution of WebJobs, including hello ability tooinvoke individual functions within WebJobs.</span></span> <span data-ttu-id="5bb91-113">panel de Hola también muestra los tiempos de ejecución de función y la salida del registro.</span><span class="sxs-lookup"><span data-stu-id="5bb91-113">hello dashboard also displays function runtimes and logging output.</span></span>

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

