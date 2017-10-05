---
title: "Administración de una aplicación web en Servicio de aplicaciones de Azure"
description: "Vínculos a recursos para administrar una aplicación web en Servicio de aplicaciones de Azure."
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
ms.openlocfilehash: 9e19618a1b24bbdf3163ddfc3423c5c932dcd7af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="ad029-103">Administración de una aplicación web en Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="ad029-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="ad029-104">Este tema contiene vínculos a recursos para administrar una aplicación web en [Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="ad029-104">This topic contains links to resources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="ad029-105">La administración incluye todas las tareas que hacen que una aplicación web funcione sin problemas.</span><span class="sxs-lookup"><span data-stu-id="ad029-105">Management includes all of the tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="ad029-106">A lo largo de la vida de una aplicación web, llevará a cabo distintas tareas de administración, desde la implementación inicial hasta el funcionamiento normal, pasando por el mantenimiento y las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="ad029-106">Over the lifetime of a web app, you will perform different management tasks, as you move from initial deployment to normal operation, maintenance, and updates.</span></span>

<span data-ttu-id="ad029-107">Muchas tareas de administración de aplicaciones web se pueden hacer desde el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ad029-107">Many web app management tasks can be performed in the Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-to-production"></a><span data-ttu-id="ad029-108">Antes de implementar su aplicación web para la producción.</span><span class="sxs-lookup"><span data-stu-id="ad029-108">Before you deploy your web app to production</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="ad029-109">Elija un nivel</span><span class="sxs-lookup"><span data-stu-id="ad029-109">Choose a tier</span></span>
<span data-ttu-id="ad029-110">Servicio de aplicaciones de Azure se ofrece en cinco niveles: gratis, compartido, básico, estándar y premium.</span><span class="sxs-lookup"><span data-stu-id="ad029-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="ad029-111">Para obtener información acerca de las características y los precios de cada nivel, consulte [Detalles de precios](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="ad029-111">For information about the features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="ad029-112">[planes del Servicio de aplicaciones](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) le permiten agrupar varias aplicaciones web en el mismo nivel.</span><span class="sxs-lookup"><span data-stu-id="ad029-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under the same tier.</span></span>
* <span data-ttu-id="ad029-113">Siempre puede [cambiar los niveles](web-sites-scale.md) después de crear su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ad029-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="ad029-114">Configuración</span><span class="sxs-lookup"><span data-stu-id="ad029-114">Configuration</span></span>
<span data-ttu-id="ad029-115">Use el [Portal de Azure](https://portal.azure.com/) para establecer varias opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="ad029-115">Use the [Azure Portal](https://portal.azure.com/) to set various configuration options.</span></span> <span data-ttu-id="ad029-116">Para obtener detalles, consulte [Configuración de aplicaciones en el Servicio de aplicaciones de Azure](web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ad029-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="ad029-117">Esta es una lista de comprobación breve:</span><span class="sxs-lookup"><span data-stu-id="ad029-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="ad029-118">Seleccione **versiones de tiempo de ejecución** para .NET, PHP, Java o Python, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="ad029-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="ad029-119">Habilite **WebSockets** si su aplicación web usa el protocolo WebSocket.</span><span class="sxs-lookup"><span data-stu-id="ad029-119">Enable **WebSockets** if your web app uses the WebSocket protocol.</span></span> <span data-ttu-id="ad029-120">(Se incluyen las aplicaciones que usan [ASP.NET SignalR](http://www.asp.net/signalr) o [socket.io](web-sites-nodejs-chat-app-socketio.md)).</span><span class="sxs-lookup"><span data-stu-id="ad029-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="ad029-121">¿Ejecuta trabajos web continuamente?</span><span class="sxs-lookup"><span data-stu-id="ad029-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="ad029-122">Si es así, habilite la opción **Always On**.</span><span class="sxs-lookup"><span data-stu-id="ad029-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="ad029-123">Establezca el **documento predeterminado**, como index.html.</span><span class="sxs-lookup"><span data-stu-id="ad029-123">Set the **default document**, such as index.html.</span></span>

<span data-ttu-id="ad029-124">Además de estas opciones de configuración básicas, puede configurar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ad029-124">In addition to these basic configuration settings, you may want to configure the following:</span></span>

* <span data-ttu-id="ad029-125">**Capa de sockets seguros (SSL)** .</span><span class="sxs-lookup"><span data-stu-id="ad029-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="ad029-126">Para usar SSL con un nombre de dominio personalizado, debe obtener un certificado SSL y configurar la aplicación web para que lo use.</span><span class="sxs-lookup"><span data-stu-id="ad029-126">To use SSL with a custom domain name, you must get an SSL certificate and configure your web app to use it.</span></span> <span data-ttu-id="ad029-127">Consulte [Habilitación de HTTPS para una aplicación web en el Servicio de aplicaciones de Azure](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="ad029-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="ad029-128">**Nombre de dominio personalizado.**</span><span class="sxs-lookup"><span data-stu-id="ad029-128">**Custom domain name.**</span></span> <span data-ttu-id="ad029-129">Su aplicación web tiene automáticamente un subdominio en azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="ad029-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="ad029-130">Puede asociar un nombre de dominio personalizado, como contoso.com.</span><span class="sxs-lookup"><span data-stu-id="ad029-130">You can associate a custom domain name, such as contoso.com.</span></span> <span data-ttu-id="ad029-131">Consulte [Configuración de un nombre de dominio personalizado en el Servicio de aplicaciones de Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="ad029-131">See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="ad029-132">Configuración específica por idioma:</span><span class="sxs-lookup"><span data-stu-id="ad029-132">Language-specific configuration:</span></span>

* <span data-ttu-id="ad029-133">**PHP**: [configuración de PHP en Aplicaciones web del Servicio de aplicaciones de Azure](web-sites-php-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ad029-133">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="ad029-134">**Python**: [configuración de Python con Aplicaciones web del Servicio de aplicaciones de Azure](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="ad029-134">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="ad029-135">Cuando su aplicación web está en ejecución</span><span class="sxs-lookup"><span data-stu-id="ad029-135">While your web app is running</span></span>
<span data-ttu-id="ad029-136">Cuando la aplicación web está en ejecución, querrá asegurarse de que está disponible y de que se escala para satisfacer el tráfico de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="ad029-136">While your web app is running, you want to make sure it is available, and that it scales to meet user traffic.</span></span> <span data-ttu-id="ad029-137">También puede necesitar solucionar errores.</span><span class="sxs-lookup"><span data-stu-id="ad029-137">You may also need to troubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="ad029-138">Supervisión</span><span class="sxs-lookup"><span data-stu-id="ad029-138">Monitoring</span></span>
* <span data-ttu-id="ad029-139">Desde el Portal de Azure, puede [agregar métricas de rendimiento](web-sites-monitor.md) , como el uso de la CPU y el número de solicitudes de clientes.</span><span class="sxs-lookup"><span data-stu-id="ad029-139">Through the Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="ad029-140">[Escale su aplicación web](web-sites-scale.md) en respuesta al tráfico.</span><span class="sxs-lookup"><span data-stu-id="ad029-140">[Scale your web app](web-sites-scale.md) in response to traffic.</span></span> <span data-ttu-id="ad029-141">En función de su nivel, puede escalar el número de máquinas virtuales y/o el tamaño de las instancias de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ad029-141">Depending on your tier, you can scale the number of VMs and/or the size of the VM instances.</span></span> <span data-ttu-id="ad029-142">En los niveles estándar y premium, también puede configurar la autoescala para que la aplicación web escale automáticamente, bien según una programación fija, o bien en respuesta a la carga.</span><span class="sxs-lookup"><span data-stu-id="ad029-142">In the Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response to load.</span></span>  

### <a name="backups"></a><span data-ttu-id="ad029-143">Copias de seguridad</span><span class="sxs-lookup"><span data-stu-id="ad029-143">Backups</span></span>
* <span data-ttu-id="ad029-144">Establezca las [copias de seguridad automáticas](web-sites-backup.md) de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="ad029-144">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="ad029-145">Obtenga más información sobre las copias de seguridad en [este vídeo](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span><span class="sxs-lookup"><span data-stu-id="ad029-145">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="ad029-146">Conozca las opciones para la [recuperación de bases de datos](../sql-database/sql-database-business-continuity.md) en Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="ad029-146">Learn about the options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="ad029-147">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="ad029-147">Troubleshooting</span></span>
* <span data-ttu-id="ad029-148">Si se produce algún error, puede [solucionar los problemas en Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)usando registros de diagnóstico y depuración activa en la nube.</span><span class="sxs-lookup"><span data-stu-id="ad029-148">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in the cloud.</span></span> 
* <span data-ttu-id="ad029-149">Fuera de Visual Studio, hay varias formas de recopilar registros de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="ad029-149">Outside of Visual Studio, there are various ways to collect diagnostic logs.</span></span> <span data-ttu-id="ad029-150">Consulte [Habilitación del registro de diagnóstico para aplicaciones web en el Servicio de aplicaciones de Azure](web-sites-enable-diagnostic-log.md).</span><span class="sxs-lookup"><span data-stu-id="ad029-150">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="ad029-151">Para aplicaciones Node.js, consulte [Depuración de una aplicación Node.js en Servicio de aplicaciones de Azure](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="ad029-151">For Node.js applications, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="ad029-152">Restauración de datos</span><span class="sxs-lookup"><span data-stu-id="ad029-152">Restoring Data</span></span>
* <span data-ttu-id="ad029-153">[Restaure](web-sites-restore.md) una aplicación web de la que se creó una copia de seguridad anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ad029-153">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="ad029-154">Cuando actualiza la aplicación web</span><span class="sxs-lookup"><span data-stu-id="ad029-154">When you update your web app</span></span>
<span data-ttu-id="ad029-155">Si no ha habilitado las copias de seguridad automáticas, puede crear una [copia de seguridad manual](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="ad029-155">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="ad029-156">Puede usar una [implementación de ensayo](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="ad029-156">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="ad029-157">Esta opción le permite publicar actualizaciones en una implementación provisional que se ejecuta en paralelo a su implementación de producción.</span><span class="sxs-lookup"><span data-stu-id="ad029-157">This option lets you publish updates to a staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site to production]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


