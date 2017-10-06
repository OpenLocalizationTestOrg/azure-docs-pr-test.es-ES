---
title: registros de aaaStreaming y la consola
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
ms.openlocfilehash: bb4b8ce5358da12041e164dfff8f43790dd67924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-logs-and-hello-console"></a><span data-ttu-id="ddc54-103">Hello consola y los registros de streaming</span><span class="sxs-lookup"><span data-stu-id="ddc54-103">Streaming Logs and hello Console</span></span>
## <a name="streaming-logs"></a><span data-ttu-id="ddc54-104">Registros de transmisión</span><span class="sxs-lookup"><span data-stu-id="ddc54-104">Streaming Logs</span></span>
<span data-ttu-id="ddc54-105">Hola **portal de Azure** proporciona un visor de registro de transmisión por secuencias integrado que le permite ver los eventos de seguimiento de su **servicio de aplicaciones** aplicaciones en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="ddc54-105">hello **Azure portal** provides an integrated streaming log viewer that lets you view tracing events from your **App Service** apps in real time.</span></span>  

<span data-ttu-id="ddc54-106">Configurar esta característica requiere algunos pasos sencillos:</span><span class="sxs-lookup"><span data-stu-id="ddc54-106">Setting up this feature requires a few simple steps:</span></span>

* <span data-ttu-id="ddc54-107">Escritura de seguimientos en el código.</span><span class="sxs-lookup"><span data-stu-id="ddc54-107">Write traces in your code</span></span>
* <span data-ttu-id="ddc54-108">Habilitación de **registros de diagnósticos** de aplicación para la aplicación</span><span class="sxs-lookup"><span data-stu-id="ddc54-108">Enable Application **Diagnostic Logs** for your app</span></span>
* <span data-ttu-id="ddc54-109">Secuencia de Hola de vista de integradas de hello **registros de Streaming** interfaz de usuario en hello **portal de Azure**.</span><span class="sxs-lookup"><span data-stu-id="ddc54-109">View hello stream from hello built-in **Streaming Logs** UI in hello **Azure portal**.</span></span>

### <a name="how-toowrite-traces-in-your-code"></a><span data-ttu-id="ddc54-110">¿Cómo realiza el seguimiento de toowrite en el código</span><span class="sxs-lookup"><span data-stu-id="ddc54-110">How toowrite traces in your code</span></span>
<span data-ttu-id="ddc54-111">La escritura de seguimientos en el código es sencilla.</span><span class="sxs-lookup"><span data-stu-id="ddc54-111">Writing traces in your code is easy.</span></span>  <span data-ttu-id="ddc54-112">En C# es tan fácil como escribir el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="ddc54-112">In C# it's as easy as writing hello following code:</span></span>

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

<span data-ttu-id="ddc54-113">Hola clase Trace reside en el espacio de nombres de hello System.Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="ddc54-113">hello Trace class lives in hello System.Diagnostics namespace.</span></span>

<span data-ttu-id="ddc54-114">Puede escribir este código en una aplicación node.js tooachieve Hola el mismo resultado:</span><span class="sxs-lookup"><span data-stu-id="ddc54-114">In a node.js app you can write this code tooachieve hello same result:</span></span>

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a><span data-ttu-id="ddc54-115">¿Cómo tooenable y vista Hola registros de streaming</span><span class="sxs-lookup"><span data-stu-id="ddc54-115">How tooenable and view hello streaming logs</span></span>
<span data-ttu-id="ddc54-116">![][BrowseSitesScreenshot] El diagnóstico se habilita por aplicación.</span><span class="sxs-lookup"><span data-stu-id="ddc54-116">![][BrowseSitesScreenshot] Diagnostics are enabled on a per app basis.</span></span> <span data-ttu-id="ddc54-117">Comience por explorar sitio toohello que le gustaría tooenable esta característica en.</span><span class="sxs-lookup"><span data-stu-id="ddc54-117">Start by browsing toohello site you would like tooenable this feature on.</span></span>  

<span data-ttu-id="ddc54-118">![][DiagnosticsLogs]En el menú de configuración, desplácese hacia abajo toohello **supervisión** sección y haga clic en **(1) registros de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="ddc54-118">![][DiagnosticsLogs] From settings menu, scroll down toohello **Monitoring** section and click on **(1) Diagnostic Logs**.</span></span> <span data-ttu-id="ddc54-119">A continuación, **enable (2)** **(Filesystem) de registro de aplicaciones** o **(blob) de registro de aplicaciones** hello **nivel** opción permite cambiar Hola nivel de gravedad de seguimientos toocapture.</span><span class="sxs-lookup"><span data-stu-id="ddc54-119">Then **(2) enable** **Application Logging (Filesystem)** or **Application Logging (blob)** hello **Level** option lets you change hello severity level of traces toocapture.</span></span> <span data-ttu-id="ddc54-120">Si simplemente está tratando de tooget familiarizado con la característica de hello, establecer el nivel de hello demasiado**detallado** tooensure todas las instrucciones de seguimiento se recopilan.</span><span class="sxs-lookup"><span data-stu-id="ddc54-120">If you're just trying tooget familiar with hello feature, set hello level too**Verbose** tooensure all of your trace statements are collected.</span></span>

<span data-ttu-id="ddc54-121">Haga clic en **guardar** princip Hola de hoja de Hola y está listo tooview registros.</span><span class="sxs-lookup"><span data-stu-id="ddc54-121">Click **SAVE** at hello top of hello blade and you're ready tooview logs.</span></span>

> [!NOTE]
> <span data-ttu-id="ddc54-122">Hola Hola superior **nivel de gravedad** hello más recursos son consumido toolog y Hola se producen varios seguimientos.</span><span class="sxs-lookup"><span data-stu-id="ddc54-122">hello higher hello **severity level** hello more resources are consumed toolog and hello more traces are produced.</span></span> <span data-ttu-id="ddc54-123">Asegúrese de que **nivel de gravedad** está configurado toohello detalle correcto para un sitio de mucho tráfico o de producción.</span><span class="sxs-lookup"><span data-stu-id="ddc54-123">Make sure **severity level** is configured toohello correct verbosity for a production or high traffic site.</span></span> 
> 
> 

<span data-ttu-id="ddc54-124">![][StreamingLogsScreenshot]Hola tooview **los registros de streaming** desde dentro de hello portal de Azure, haga clic en **secuencia de registro (1)** también en hello **supervisión** sección del menú de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddc54-124">![][StreamingLogsScreenshot] tooview hello **streaming logs** from within hello Azure portal, click on **(1) Log Stream** also in hello **Monitoring** section of hello settings menu.</span></span> <span data-ttu-id="ddc54-125">Si la aplicación está escribiendo activamente las instrucciones de seguimiento, debería ver Hola **(2) de transmisión por secuencias registra la interfaz de usuario** casi en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="ddc54-125">If your app is actively writing trace statements, then you should see them in hello **(2) streaming logs UI** in near real time.</span></span>

## <a name="console"></a><span data-ttu-id="ddc54-126">Consola</span><span class="sxs-lookup"><span data-stu-id="ddc54-126">Console</span></span>
<span data-ttu-id="ddc54-127">Hola **portal de Azure** proporciona la aplicación de consola acceso tooyour.</span><span class="sxs-lookup"><span data-stu-id="ddc54-127">hello **Azure portal** provides console access tooyour app.</span></span> <span data-ttu-id="ddc54-128">Puede explorar el sistema de archivos de la aplicación y ejecutar los scripts de cmd/powershell.</span><span class="sxs-lookup"><span data-stu-id="ddc54-128">You can explore your app's file system and run powershell/cmd scripts.</span></span> <span data-ttu-id="ddc54-129">Se enlazan por hello mismos permisos establecidos como la ejecución de código de aplicación al ejecutar comandos de la consola.</span><span class="sxs-lookup"><span data-stu-id="ddc54-129">You are bound by hello same permissions set as your running app code when executing console commands.</span></span> <span data-ttu-id="ddc54-130">Directorios de tooprotected de acceso o ejecutar scripts que requieren permisos elevados está bloqueado.</span><span class="sxs-lookup"><span data-stu-id="ddc54-130">Access tooprotected directories or running scripts that require elevated permissions is blocked.</span></span>  

<span data-ttu-id="ddc54-131">![][ConsoleScreenshot]En el menú de configuración, desplácese hacia abajo demasiado**herramientas de desarrollo** sección y haga clic en **(1) consola** hello y **(2) consola** toohello derecha abre la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="ddc54-131">![][ConsoleScreenshot] From settings menu, scroll down too**Development Tools** section and click on **(1) Console** and hello **(2) console** UI opens toohello right.</span></span>

<span data-ttu-id="ddc54-132">tooget familiarizado con hello **consola**, intente comandos básicos, como:</span><span class="sxs-lookup"><span data-stu-id="ddc54-132">tooget familiar with hello **console**, try basic commands like:</span></span>

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
