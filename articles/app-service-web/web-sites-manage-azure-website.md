---
title: "aaaManage una aplicación web en el servicio de aplicación de Azure"
description: "Tooresources de vínculos para administrar una aplicación web en el servicio de aplicaciones de Azure."
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="5ea7c-103">Administración de una aplicación web en Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="5ea7c-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="5ea7c-104">Este tema contiene vínculos tooresources para administrar una aplicación web en [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="5ea7c-104">This topic contains links tooresources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="5ea7c-105">La administración incluye todas las tareas de Hola que mantener la aplicación web que se ejecuta sin problemas.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-105">Management includes all of hello tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="5ea7c-106">Sobre Hola mientras dura una aplicación web, realizará las tareas de administración diferente, al pasar de las actualizaciones, el mantenimiento y el funcionamiento de toonormal de implementación inicial.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-106">Over hello lifetime of a web app, you will perform different management tasks, as you move from initial deployment toonormal operation, maintenance, and updates.</span></span>

<span data-ttu-id="5ea7c-107">Muchas tareas de administración de la aplicación web pueden realizarse en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-107">Many web app management tasks can be performed in hello Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-tooproduction"></a><span data-ttu-id="5ea7c-108">Antes de implementar su tooproduction de aplicación web</span><span class="sxs-lookup"><span data-stu-id="5ea7c-108">Before you deploy your web app tooproduction</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="5ea7c-109">Elija un nivel</span><span class="sxs-lookup"><span data-stu-id="5ea7c-109">Choose a tier</span></span>
<span data-ttu-id="5ea7c-110">Servicio de aplicaciones de Azure se ofrece en cinco niveles: gratis, compartido, básico, estándar y premium.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="5ea7c-111">Para obtener información sobre las características de Hola y precios para cada nivel, consulte [detalles de precios](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="5ea7c-111">For information about hello features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="5ea7c-112">[Planes de servicio de aplicaciones](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) permiten agrupar varias aplicaciones web en hello mismo nivel.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under hello same tier.</span></span>
* <span data-ttu-id="5ea7c-113">Siempre puede [cambiar los niveles](web-sites-scale.md) después de crear su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="5ea7c-114">Configuración</span><span class="sxs-lookup"><span data-stu-id="5ea7c-114">Configuration</span></span>
<span data-ttu-id="5ea7c-115">Hola de uso [Portal de Azure](https://portal.azure.com/) tooset distintas opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-115">Use hello [Azure Portal](https://portal.azure.com/) tooset various configuration options.</span></span> <span data-ttu-id="5ea7c-116">Para obtener detalles, consulte [Configuración de aplicaciones en el Servicio de aplicaciones de Azure](web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5ea7c-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="5ea7c-117">Esta es una lista de comprobación breve:</span><span class="sxs-lookup"><span data-stu-id="5ea7c-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="5ea7c-118">Seleccione **versiones de tiempo de ejecución** para .NET, PHP, Java o Python, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="5ea7c-119">Habilitar **WebSockets** si la aplicación web usa el protocolo de WebSocket de Hola.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-119">Enable **WebSockets** if your web app uses hello WebSocket protocol.</span></span> <span data-ttu-id="5ea7c-120">(Se incluyen las aplicaciones que usan [ASP.NET SignalR](http://www.asp.net/signalr) o [socket.io](web-sites-nodejs-chat-app-socketio.md)).</span><span class="sxs-lookup"><span data-stu-id="5ea7c-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="5ea7c-121">¿Ejecuta trabajos web continuamente?</span><span class="sxs-lookup"><span data-stu-id="5ea7c-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="5ea7c-122">Si es así, habilite la opción **Always On**.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="5ea7c-123">Conjunto hello **documento predeterminado**, como index.html.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-123">Set hello **default document**, such as index.html.</span></span>

<span data-ttu-id="5ea7c-124">En suma toothese configuración básica, puede que desee siguiente de Hola tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="5ea7c-124">In addition toothese basic configuration settings, you may want tooconfigure hello following:</span></span>

* <span data-ttu-id="5ea7c-125">**Capa de sockets seguros (SSL)** .</span><span class="sxs-lookup"><span data-stu-id="5ea7c-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="5ea7c-126">toouse SSL con un nombre de dominio personalizado, debe obtener una SSL de certificados y configurar su toouse de aplicación web se.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-126">toouse SSL with a custom domain name, you must get an SSL certificate and configure your web app toouse it.</span></span> <span data-ttu-id="5ea7c-127">Consulte [Habilitación de HTTPS para una aplicación web en el Servicio de aplicaciones de Azure](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="5ea7c-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="5ea7c-128">**Nombre de dominio personalizado.**</span><span class="sxs-lookup"><span data-stu-id="5ea7c-128">**Custom domain name.**</span></span> <span data-ttu-id="5ea7c-129">Su aplicación web tiene automáticamente un subdominio en azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="5ea7c-130">Puede asociar un nombre de dominio personalizado, como contoso.com. Consulte [Configuración de un nombre de dominio personalizado en el Servicio de aplicaciones de Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="5ea7c-130">You can associate a custom domain name, such as contoso.com. See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="5ea7c-131">Configuración específica por idioma:</span><span class="sxs-lookup"><span data-stu-id="5ea7c-131">Language-specific configuration:</span></span>

* <span data-ttu-id="5ea7c-132">**PHP**: [configuración de PHP en Aplicaciones web del Servicio de aplicaciones de Azure](web-sites-php-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5ea7c-132">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="5ea7c-133">**Python**: [configuración de Python con Aplicaciones web del Servicio de aplicaciones de Azure](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="5ea7c-133">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="5ea7c-134">Cuando su aplicación web está en ejecución</span><span class="sxs-lookup"><span data-stu-id="5ea7c-134">While your web app is running</span></span>
<span data-ttu-id="5ea7c-135">Mientras se ejecuta la aplicación web, desea toomake que está disponible y se escala toomeet tráfico de usuario.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-135">While your web app is running, you want toomake sure it is available, and that it scales toomeet user traffic.</span></span> <span data-ttu-id="5ea7c-136">También puede que tenga errores de tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-136">You may also need tootroubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="5ea7c-137">Supervisión</span><span class="sxs-lookup"><span data-stu-id="5ea7c-137">Monitoring</span></span>
* <span data-ttu-id="5ea7c-138">A través de hello Portal de Azure, también puede [agregar las métricas de rendimiento](web-sites-monitor.md) como el uso de CPU y el número de solicitudes de cliente.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-138">Through hello Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="5ea7c-139">[Escalar la aplicación web](web-sites-scale.md) en tootraffic de respuesta.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-139">[Scale your web app](web-sites-scale.md) in response tootraffic.</span></span> <span data-ttu-id="5ea7c-140">Dependiendo de la capa, puede escalar número de Hola de máquinas virtuales o el tamaño de Hola de instancias de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-140">Depending on your tier, you can scale hello number of VMs and/or hello size of hello VM instances.</span></span> <span data-ttu-id="5ea7c-141">En hello estándar y niveles de Premium, también puede configurar escalado automático, por lo que la aplicación web se escala automáticamente, según una programación fija o en tooload de respuesta.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-141">In hello Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response tooload.</span></span>  

### <a name="backups"></a><span data-ttu-id="5ea7c-142">Copias de seguridad</span><span class="sxs-lookup"><span data-stu-id="5ea7c-142">Backups</span></span>
* <span data-ttu-id="5ea7c-143">Establezca las [copias de seguridad automáticas](web-sites-backup.md) de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-143">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="5ea7c-144">Obtenga más información sobre las copias de seguridad en [este vídeo](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span><span class="sxs-lookup"><span data-stu-id="5ea7c-144">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="5ea7c-145">Obtenga información acerca de las opciones de Hola para [recuperación de la base de datos](../sql-database/sql-database-business-continuity.md) en la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-145">Learn about hello options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="5ea7c-146">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="5ea7c-146">Troubleshooting</span></span>
* <span data-ttu-id="5ea7c-147">Si algo va mal, puede [solución de problemas en Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), usando los registros de diagnóstico y depuración en la nube de hello activa.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-147">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in hello cloud.</span></span> 
* <span data-ttu-id="5ea7c-148">Fuera de Visual Studio, hay varios registros de diagnóstico de toocollect maneras.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-148">Outside of Visual Studio, there are various ways toocollect diagnostic logs.</span></span> <span data-ttu-id="5ea7c-149">Consulte [Habilitación del registro de diagnóstico para aplicaciones web en el Servicio de aplicaciones de Azure](web-sites-enable-diagnostic-log.md).</span><span class="sxs-lookup"><span data-stu-id="5ea7c-149">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="5ea7c-150">Para las aplicaciones Node.js, vea [cómo toodebug una Node.js web aplicación de servicio de aplicaciones de Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="5ea7c-150">For Node.js applications, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="5ea7c-151">Restauración de datos</span><span class="sxs-lookup"><span data-stu-id="5ea7c-151">Restoring Data</span></span>
* <span data-ttu-id="5ea7c-152">[Restaure](web-sites-restore.md) una aplicación web de la que se creó una copia de seguridad anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-152">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="5ea7c-153">Cuando actualiza la aplicación web</span><span class="sxs-lookup"><span data-stu-id="5ea7c-153">When you update your web app</span></span>
<span data-ttu-id="5ea7c-154">Si no ha habilitado las copias de seguridad automáticas, puede crear una [copia de seguridad manual](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="5ea7c-154">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="5ea7c-155">Puede usar una [implementación de ensayo](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="5ea7c-155">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="5ea7c-156">Esta opción le permite publicar tooa actualizaciones implementación que se ejecuta en paralelo de ensayo con la implementación de producción.</span><span class="sxs-lookup"><span data-stu-id="5ea7c-156">This option lets you publish updates tooa staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


