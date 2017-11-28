---
title: "configuración de aaaUsing PM2 para Node.js en la aplicación Web de Azure en Linux | Documentos de Microsoft"
description: "Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure"
keywords: azure app service, aplic. web, nodejs, pm2, linux, oss
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: fb420f32-6d74-49c7-992f-0ed5616e66e7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 923783ffe656e01c43318899d1a656b553ebb5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a><span data-ttu-id="dff7c-104">Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="dff7c-104">Use PM2 configuration for Node.js in Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="dff7c-105">Si establece tooNode.js de pila de aplicación hello para la aplicación Web de Azure en Linux, obtendrá Hola opción tooset un archivo de inicio de Node.js como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="dff7c-105">If you set hello application stack tooNode.js for Azure Web App on Linux, you get hello option tooset a Node.js startup file as shown in hello following image:</span></span>

![Establecer un archivo de inicio de Node.js][1]

<span data-ttu-id="dff7c-107">Puede usar esta opción toodo uno de hello siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="dff7c-107">You can use this option toodo one of hello following tasks:</span></span>

* <span data-ttu-id="dff7c-108">Especifique el script de inicio de hello para la aplicación Node.js (por ejemplo: /bin/server.js).</span><span class="sxs-lookup"><span data-stu-id="dff7c-108">Specify hello startup script for your Node.js app (for example: /bin/server.js).</span></span>
* <span data-ttu-id="dff7c-109">Especificar Hola PM2 toouse de archivo de configuración de la aplicación Node.js (por ejemplo: /foo/process.json).</span><span class="sxs-lookup"><span data-stu-id="dff7c-109">Specify hello PM2 configuration file toouse for your Node.js app (for example: /foo/process.json).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="dff7c-110">Si desea que su toorestart de procesos de Node.js automáticamente cuando se modifican determinados archivos, use configuración de PM2 Hola.</span><span class="sxs-lookup"><span data-stu-id="dff7c-110">If you want your Node.js processes toorestart automatically when certain files are modified, use hello PM2 configuration.</span></span> <span data-ttu-id="dff7c-111">En caso contrario, la aplicación no se reiniciará cuando recibe notificaciones de cambio (por ejemplo, cuando cambia el código de aplicación).</span><span class="sxs-lookup"><span data-stu-id="dff7c-111">Otherwise, your application won't restart when it receives change notifications (for example, when your application code changes).</span></span>
  > 
  > 

<span data-ttu-id="dff7c-112">Puede comprobar hello Node.js [Procesar documentación archivos](http://pm2.keymetrics.io/docs/usage/application-declaration/) para todas las opciones de Hola, pero aquí te mostramos un ejemplo de lo que puede usar como el archivo process.json:</span><span class="sxs-lookup"><span data-stu-id="dff7c-112">You can check hello Node.js [process file documentation](http://pm2.keymetrics.io/docs/usage/application-declaration/) for all hello options, but following is a sample of what you can use as your process.json file:</span></span>

        {
          "name"        : "worker",
          "script"      : "./bin/server.js",
          "instances"   : 1,
          "merge_logs"  : true,
          "log_date_format" : "YYYY-MM-DD HH:mm Z",
          "watch": ["./bin/server.js", "foo.txt"],
          "watch_options": {
            "followSymlinks": true,
            "usePolling"   : true,
            "interval"    : 5
          }
        }

<span data-ttu-id="dff7c-113">Toonote aspectos importantes en esta configuración son:</span><span class="sxs-lookup"><span data-stu-id="dff7c-113">Important things toonote in this configuration are:</span></span>

* <span data-ttu-id="dff7c-114">propiedad de "script" Hola especifica la secuencia de comandos de inicio de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dff7c-114">hello "script" property specifies your application's start script.</span></span>
* <span data-ttu-id="dff7c-115">propiedad de "instancias" Hello especifica cuántas instancias de hello nodo proceso toolaunch.</span><span class="sxs-lookup"><span data-stu-id="dff7c-115">hello "instances" property specifies how many instances of hello node process toolaunch.</span></span> <span data-ttu-id="dff7c-116">Si está ejecutando la aplicación en máquinas virtuales más grandes que tienen varios núcleos, es una buena idea toomaximize los recursos estableciendo un valor más alto aquí.</span><span class="sxs-lookup"><span data-stu-id="dff7c-116">If you are running your application on larger VMs that have multiple cores, it's a good idea toomaximize your resources by setting a higher value here.</span></span>
* <span data-ttu-id="dff7c-117">Hola "inspeccionar" matriz especifica todos los archivos que desee toorestart el proceso del nodo de Hola para cuando cambian.</span><span class="sxs-lookup"><span data-stu-id="dff7c-117">hello "watch" array specifies all files that you want toorestart hello node process for when they change.</span></span>
* <span data-ttu-id="dff7c-118">Para "watch_options" Hola, actualmente debe toospecify "usePolling" como true debido a la manera de hello que está montado el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dff7c-118">For hello "watch_options", you currently need toospecify "usePolling" as true because of hello way your application content is mounted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dff7c-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dff7c-119">Next steps</span></span>
* [<span data-ttu-id="dff7c-120">¿Qué es Web App on Linux de Azure?</span><span class="sxs-lookup"><span data-stu-id="dff7c-120">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="dff7c-121">Preguntas más frecuentes sobre Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="dff7c-121">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
