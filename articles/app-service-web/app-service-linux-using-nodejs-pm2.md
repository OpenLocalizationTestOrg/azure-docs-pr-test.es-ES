---
title: "Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure | Microsoft Docs"
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
ms.openlocfilehash: 5002400a673e2c5cc4290bab488b839fb2282966
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a><span data-ttu-id="cc182-104">Uso de la configuración de PM2 para Node.js en Web App on Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="cc182-104">Use PM2 configuration for Node.js in Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="cc182-105">Si establece la pila de aplicaciones en Node.js para Web App on Linux de Azure, tiene la opción de establecer un archivo de inicio de Node.js, como se muestra en la siguiente imagen:</span><span class="sxs-lookup"><span data-stu-id="cc182-105">If you set the application stack to Node.js for Azure Web App on Linux, you get the option to set a Node.js startup file as shown in the following image:</span></span>

![Establecer un archivo de inicio de Node.js][1]

<span data-ttu-id="cc182-107">Se puede utilizar esta opción para realizar una de las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="cc182-107">You can use this option to do one of the following tasks:</span></span>

* <span data-ttu-id="cc182-108">Especificar el script de inicio de una aplicación de Node.js (por ejemplo: /bin/server.js).</span><span class="sxs-lookup"><span data-stu-id="cc182-108">Specify the startup script for your Node.js app (for example: /bin/server.js).</span></span>
* <span data-ttu-id="cc182-109">Especificar el archivo de configuración de PM2 que se va a usar para una aplicación de Node.js (por ejemplo: /foo/process.json).</span><span class="sxs-lookup"><span data-stu-id="cc182-109">Specify the PM2 configuration file to use for your Node.js app (for example: /foo/process.json).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="cc182-110">Si desea que los procesos de Node.js se reinicien automáticamente al modificar determinados archivos, utilice la configuración de PM2.</span><span class="sxs-lookup"><span data-stu-id="cc182-110">If you want your Node.js processes to restart automatically when certain files are modified, use the PM2 configuration.</span></span> <span data-ttu-id="cc182-111">En caso contrario, la aplicación no se reiniciará cuando recibe notificaciones de cambio (por ejemplo, cuando cambia el código de aplicación).</span><span class="sxs-lookup"><span data-stu-id="cc182-111">Otherwise, your application won't restart when it receives change notifications (for example, when your application code changes).</span></span>
  > 
  > 

<span data-ttu-id="cc182-112">En la [documentación del archivo de proceso](http://pm2.keymetrics.io/docs/usage/application-declaration/) de Node.js puede consultar todas las opciones, pero a continuación encontrará un ejemplo de lo que puede usar como archivo process.json:</span><span class="sxs-lookup"><span data-stu-id="cc182-112">You can check the Node.js [process file documentation](http://pm2.keymetrics.io/docs/usage/application-declaration/) for all the options, but following is a sample of what you can use as your process.json file:</span></span>

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

<span data-ttu-id="cc182-113">En esta configuración debe tenerse en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cc182-113">Important things to note in this configuration are:</span></span>

* <span data-ttu-id="cc182-114">La propiedad "script" especifica el script de inicio de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cc182-114">The "script" property specifies your application's start script.</span></span>
* <span data-ttu-id="cc182-115">La propiedad "instances" especifica el número de instancias del proceso de nodo que se inician.</span><span class="sxs-lookup"><span data-stu-id="cc182-115">The "instances" property specifies how many instances of the node process to launch.</span></span> <span data-ttu-id="cc182-116">Si la aplicación se ejecuta en máquinas virtuales mayores, con varios núcleos, se recomienda maximizar los recursos, para lo que hay que establecer un valor mayor aquí.</span><span class="sxs-lookup"><span data-stu-id="cc182-116">If you are running your application on larger VMs that have multiple cores, it's a good idea to maximize your resources by setting a higher value here.</span></span>
* <span data-ttu-id="cc182-117">La matriz "watch" especifica todos los archivos que se desean para reiniciar el proceso del nodo cuando cambian.</span><span class="sxs-lookup"><span data-stu-id="cc182-117">The "watch" array specifies all files that you want to restart the node process for when they change.</span></span>
* <span data-ttu-id="cc182-118">Para "watch_options", actualmente es preciso especificar "usePolling" como true, debido al modo en que se monta el contenido de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cc182-118">For the "watch_options", you currently need to specify "usePolling" as true because of the way your application content is mounted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc182-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cc182-119">Next steps</span></span>
* [<span data-ttu-id="cc182-120">¿Qué es Web App on Linux de Azure?</span><span class="sxs-lookup"><span data-stu-id="cc182-120">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="cc182-121">Preguntas más frecuentes sobre Web App on Linux de Azure App Service</span><span class="sxs-lookup"><span data-stu-id="cc182-121">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
