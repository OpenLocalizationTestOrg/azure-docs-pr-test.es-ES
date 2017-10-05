---
title: Consola y registros de streaming
description: "Información general de la consola y los registros de transmisión"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: 120ce6b115820728b9f853e9ff349beb0ef29c9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="streaming-logs-and-the-console"></a><span data-ttu-id="b9e99-103">Registros de transmisión y la consola</span><span class="sxs-lookup"><span data-stu-id="b9e99-103">Streaming Logs and the Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="b9e99-104">Registros de transmisión</span><span class="sxs-lookup"><span data-stu-id="b9e99-104">Streaming Logs</span></span>
<span data-ttu-id="b9e99-105">**Azure Portal** ofrece un visor de registros de streaming integrado que le permite ver los eventos de seguimiento desde las aplicaciones de **App Service** en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="b9e99-105">The **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="b9e99-106">Configurar esta característica requiere algunos pasos sencillos:</span><span class="sxs-lookup"><span data-stu-id="b9e99-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="b9e99-107">Escritura de seguimientos en el código.</span><span class="sxs-lookup"><span data-stu-id="b9e99-107">Write traces in your code</span></span>
* <span data-ttu-id="b9e99-108">Habilitación de **registros de diagnósticos** de aplicación para la aplicación</span><span class="sxs-lookup"><span data-stu-id="b9e99-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="b9e99-109">Vea la transmisión desde la interfaz de usuario de **registros de streaming** integrados en **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="b9e99-109">View the stream from the built-in **Streaming Logs** UI in the **Azure portal**.</span></span>

### <a name="how-to-write-traces-in-your-code"></a><span data-ttu-id="b9e99-110">Cómo escribir los seguimientos en el código</span><span class="sxs-lookup"><span data-stu-id="b9e99-110">How to write traces in your code</span></span>
<span data-ttu-id="b9e99-111">La escritura de seguimientos en el código es sencilla.</span><span class="sxs-lookup"><span data-stu-id="b9e99-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="b9e99-112">En C# es tan fácil como escribir el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="b9e99-112">In C# it's as easy as writing the following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="b9e99-113">La clase de seguimientos se encuentra en el espacio de nombres System.Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="b9e99-113">The Trace class lives in the System.Diagnostics namespace.</span></span>

<span data-ttu-id="b9e99-114">En una aplicación node.js, puede escribir este código para conseguir el mismo resultado:</span><span class="sxs-lookup"><span data-stu-id="b9e99-114">In a node.js app you can write this code to achieve the same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-to-enable-and-view-the-streaming-logs"></a><span data-ttu-id="b9e99-115">Habilitación y visualización de registros de transmisión</span><span class="sxs-lookup"><span data-stu-id="b9e99-115">How to enable and view the streaming logs</span></span>
<span data-ttu-id="b9e99-116">![][BrowseSitesScreenshot] El diagnóstico se habilita por aplicación.</span><span class="sxs-lookup"><span data-stu-id="b9e99-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="b9e99-117">Para comenzar, vaya al sitio en el que quiere habilitar esta característica.</span><span class="sxs-lookup"><span data-stu-id="b9e99-117">Start by browsing to the site you would like to enable this feature on.</span></span>  

<span data-ttu-id="b9e99-118">![][DiagnosticsLogs] En el menú de configuración, desplácese hacia abajo hasta la sección **Supervisión**y haga clic en **(1) Registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="b9e99-118">![][DiagnosticsLogs] From settings menu, scroll down to the **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="b9e99-119">Luego, **(2) habilite** **Registro de la aplicación (sistema de archivos)** o **Registro de la aplicación (blob)**. La opción **Nivel** le permite cambiar el nivel de gravedad del seguimiento que se captura.</span><span class="sxs-lookup"><span data-stu-id="b9e99-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** The **Level** option lets you change the severity level of traces to capture.</span></span> <span data-ttu-id="b9e99-120">Si solo se está intentando familiarizar con la característica, establezca el nivel en **Detallado** para asegurarse de que se recopilarán todas las instrucciones de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="b9e99-120">If you're just trying to get familiar with the feature, set the level to **Verbose** to ensure all of your trace statements are collected.</span></span>

<span data-ttu-id="b9e99-121">Haga clic en **SAVE** en la parte superior del cuadro y estará listo para ver los registros.</span><span class="sxs-lookup"><span data-stu-id="b9e99-121">Click **SAVE** at the top of the blade and you're ready to view logs.</span></span>

> [!NOTE]
> <span data-ttu-id="b9e99-122">Cuanto más alto sea el **nivel de gravedad**, más recursos del registro se consumen y más seguimientos se generarán.</span><span class="sxs-lookup"><span data-stu-id="b9e99-122">The higher the **severity level** the more resources are consumed to log and the more traces are produced.</span></span> <span data-ttu-id="b9e99-123">Asegúrese de que el **nivel de gravedad** está configurado en el nivel de detalle correcto para un sitio de producción o de alto tráfico.</span><span class="sxs-lookup"><span data-stu-id="b9e99-123">Make sure **severity level** is configured to the correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="b9e99-124">![][StreamingLogsScreenshot] Para ver los **registros de streaming** desde Azure Portal, haga clic en **(1) Secuencia de registro** también en la sección **Supervisión** del menú de configuración.</span><span class="sxs-lookup"><span data-stu-id="b9e99-124">![][StreamingLogsScreenshot] To view the **streaming logs** from within the Azure portal, click on **(1) Log Stream** also in the **Monitoring** section of the settings menu.</span></span> <span data-ttu-id="b9e99-125">Si la aplicación escribe instrucciones de seguimiento activamente, debe verlas en la **(2) interfaz de usuario de registros de streaming** prácticamente en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="b9e99-125">If your app is actively writing trace statements, then you should see them in the **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="b9e99-126">Consola</span><span class="sxs-lookup"><span data-stu-id="b9e99-126">Console</span></span>
<span data-ttu-id="b9e99-127">**Azure Portal** proporciona acceso a la consola para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b9e99-127">The **Azure portal** provides console access to your app.</span></span> <span data-ttu-id="b9e99-128">Puede explorar el sistema de archivos de la aplicación y ejecutar los scripts de cmd/powershell.</span><span class="sxs-lookup"><span data-stu-id="b9e99-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="b9e99-129">Se realizará la vinculación mediante los mismos permisos establecidos en el código de la aplicación en ejecución cuando se ejecuten los comandos de consola.</span><span class="sxs-lookup"><span data-stu-id="b9e99-129">You are bound by the same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="b9e99-130">El acceso a directorios protegidos o a scripts de ejecución que requieren permisos elevados están bloqueado.</span><span class="sxs-lookup"><span data-stu-id="b9e99-130">Access to protected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="b9e99-131">![][ConsoleScreenshot] En el menú de configuración, desplácese hacia abajo hasta la sección **Herramientas de desarrollo** y haga clic en **(1) Consola**; luego, la interfaz de usuario de la **(2) consola** aparece a la derecha.</span><span class="sxs-lookup"><span data-stu-id="b9e99-131">![][ConsoleScreenshot] From settings menu, scroll down to **Development Tools** section and click on **(1) Console** and the **(2) console** UI opens to the right.</span></span>

<span data-ttu-id="b9e99-132">Para familiarizarse con la **consola**, pruebe estos comandos básicos:</span><span class="sxs-lookup"><span data-stu-id="b9e99-132">To get familiar with the **console**, try basic commands like:</span></span>

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: ./media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: ./media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: ./media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: ./media/web-sites-streaming-logs-and-console/console.png
