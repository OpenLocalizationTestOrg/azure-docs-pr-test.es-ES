---
title: un servicio de aplicaciones de Azure CDN tooan aaaAdd | Documentos de Microsoft
description: "Agregue un toocache de servicio de aplicaciones de Azure de red de entrega de contenido (CDN) tooan y entregar los archivos estáticos desde servidores clientes de tooyour cerrar todo Hola a todos."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a><span data-ttu-id="32d48-103">Agregar un servicio de aplicaciones de Azure tooan de red de entrega de contenido (CDN)</span><span class="sxs-lookup"><span data-stu-id="32d48-103">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>

<span data-ttu-id="32d48-104">[Red de entrega de contenido (CDN) Azure](../cdn/cdn-overview.md) almacena en caché contenido web estático en el rendimiento máximo de tooprovide situadas estratégicamente para entregar contenido toousers.</span><span class="sxs-lookup"><span data-stu-id="32d48-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations tooprovide maximum throughput for delivering content toousers.</span></span> <span data-ttu-id="32d48-105">CDN Hola también reduce la carga del servidor en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="32d48-105">hello CDN also decreases server load on your web app.</span></span> <span data-ttu-id="32d48-106">Este tutorial se muestra cómo tooadd CDN de Azure tooa [aplicación web en el servicio de aplicación de Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32d48-106">This tutorial shows how tooadd Azure CDN tooa [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="32d48-107">Aquí es página principal de Hola de hello ejemplo sitio HTML estático que va a trabajar con:</span><span class="sxs-lookup"><span data-stu-id="32d48-107">Here's hello home page of hello sample static HTML site that you'll work with:</span></span>

![Página de inicio de la aplicación de ejemplo](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="32d48-109">Temas que se abordarán:</span><span class="sxs-lookup"><span data-stu-id="32d48-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="32d48-110">Crear un punto de conexión de CDN.</span><span class="sxs-lookup"><span data-stu-id="32d48-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="32d48-111">Actualizar los recursos en caché.</span><span class="sxs-lookup"><span data-stu-id="32d48-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="32d48-112">Versiones de toocontrol almacenado en memoria caché de cadenas de consulta de uso.</span><span class="sxs-lookup"><span data-stu-id="32d48-112">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="32d48-113">Usar un dominio personalizado para el extremo de red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-113">Use a custom domain for hello CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32d48-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="32d48-114">Prerequisites</span></span>

<span data-ttu-id="32d48-115">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="32d48-115">toocomplete this tutorial:</span></span>

- [<span data-ttu-id="32d48-116">Instalación de Git</span><span class="sxs-lookup"><span data-stu-id="32d48-116">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="32d48-117">Instalación de la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="32d48-117">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a><span data-ttu-id="32d48-118">Crear una aplicación web de Hola</span><span class="sxs-lookup"><span data-stu-id="32d48-118">Create hello web app</span></span>

<span data-ttu-id="32d48-119">aplicación web de toocreate hello que trabajará con seguimiento hello [inicio rápido HTML estático](app-service-web-get-started-html.md) a través de hello **examinar toohello aplicación** paso.</span><span class="sxs-lookup"><span data-stu-id="32d48-119">toocreate hello web app that you'll work with, follow hello [static HTML quickstart](app-service-web-get-started-html.md) through hello **Browse toohello app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="32d48-120">Tenga listo un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="32d48-120">Have a custom domain ready</span></span>

<span data-ttu-id="32d48-121">paso de toocomplete Hola dominio personalizado de este tutorial, necesita tooown un dominio personalizado y tener del registro DNS de acceso tooyour para su proveedor de dominio (por ejemplo, GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="32d48-121">toocomplete hello custom domain step of this tutorial, you need tooown a custom domain and have access tooyour DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="32d48-122">Por ejemplo, tooadd entradas DNS para `contoso.com` y `www.contoso.com`, debe tener la configuración de DNS de acceso tooconfigure Hola para hello `contoso.com` dominio raíz.</span><span class="sxs-lookup"><span data-stu-id="32d48-122">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must have access tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

<span data-ttu-id="32d48-123">Si ya no tiene un nombre de dominio, considere la posibilidad de siguientes hello [tutorial de dominio de servicio de aplicaciones](custom-dns-web-site-buydomains-web-app.md) toopurchase un dominio con Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="32d48-123">If you don't already have a domain name, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="32d48-124">Inicie sesión en toohello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="32d48-124">Log in toohello Azure portal</span></span>

<span data-ttu-id="32d48-125">Abra un explorador y navegue toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="32d48-125">Open a browser and navigate toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="32d48-126">Creación de un perfil y un punto de conexión de CDN</span><span class="sxs-lookup"><span data-stu-id="32d48-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="32d48-127">Hola barra de navegación izquierda, seleccione **servicios de aplicaciones**y, a continuación, seleccione aplicación hello que creó en hello [inicio rápido HTML estático](app-service-web-get-started-html.md).</span><span class="sxs-lookup"><span data-stu-id="32d48-127">In hello left navigation, select **App Services**, and then select hello app that you created in hello [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![Seleccione la aplicación de servicio de aplicaciones en portal de Hola](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="32d48-129">Hola **servicio de aplicaciones** página Hola **configuración** sección, seleccione **redes > Configurar CDN de Azure para la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="32d48-129">In hello **App Service** page, in hello **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![Seleccione la red CDN en portal de Hola](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="32d48-131">Hola **red de entrega de contenido de Azure** , proporcione hello **nuevo extremo** configuración como se especifica en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-131">In hello **Azure Content Delivery Network** page, provide hello **New endpoint** settings as specified in hello table.</span></span>

![Crear un perfil y punto de conexión en el portal de Hola](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="32d48-133">Configuración</span><span class="sxs-lookup"><span data-stu-id="32d48-133">Setting</span></span> | <span data-ttu-id="32d48-134">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="32d48-134">Suggested value</span></span> | <span data-ttu-id="32d48-135">Descripción</span><span class="sxs-lookup"><span data-stu-id="32d48-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="32d48-136">**Perfil de CDN**</span><span class="sxs-lookup"><span data-stu-id="32d48-136">**CDN profile**</span></span> | <span data-ttu-id="32d48-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="32d48-137">myCDNProfile</span></span> | <span data-ttu-id="32d48-138">Seleccione **crear nuevo** toocreate un perfil de CDN.</span><span class="sxs-lookup"><span data-stu-id="32d48-138">Select **Create new** toocreate a CDN profile.</span></span> <span data-ttu-id="32d48-139">Un perfil de CDN es una colección de puntos de conexión de red CDN Hola mismo nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="32d48-139">A CDN profile is a collection of CDN endpoints with hello same pricing tier.</span></span> |
| <span data-ttu-id="32d48-140">**Plan de tarifa**</span><span class="sxs-lookup"><span data-stu-id="32d48-140">**Pricing tier**</span></span> | <span data-ttu-id="32d48-141">Estándar de Akamai</span><span class="sxs-lookup"><span data-stu-id="32d48-141">Standard Akamai</span></span> | <span data-ttu-id="32d48-142">Hola [tarifa](../cdn/cdn-overview.md#azure-cdn-features) especifica el proveedor de Hola y características disponibles.</span><span class="sxs-lookup"><span data-stu-id="32d48-142">hello [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies hello provider and available features.</span></span> <span data-ttu-id="32d48-143">En este tutorial, usamos Akamai estándar.</span><span class="sxs-lookup"><span data-stu-id="32d48-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="32d48-144">**Nombre del punto de conexión de CDN**</span><span class="sxs-lookup"><span data-stu-id="32d48-144">**CDN endpoint name**</span></span> | <span data-ttu-id="32d48-145">Cualquier nombre que sea único en el dominio de hello azureedge.net</span><span class="sxs-lookup"><span data-stu-id="32d48-145">Any name that is unique in hello azureedge.net domain</span></span> | <span data-ttu-id="32d48-146">Obtener acceso a los recursos almacenados en caché en el dominio de hello  *\<endpointname >. azureedge.net*.</span><span class="sxs-lookup"><span data-stu-id="32d48-146">You access your cached resources at hello domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="32d48-147">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="32d48-147">Select **Create**.</span></span>

<span data-ttu-id="32d48-148">Azure crea el perfil de Hola y de punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="32d48-148">Azure creates hello profile and endpoint.</span></span> <span data-ttu-id="32d48-149">nuevo punto de conexión de Hello aparece en hello **extremos** lista Hola sintonía, y cuando se aprovisiona Hola estado **ejecutando**.</span><span class="sxs-lookup"><span data-stu-id="32d48-149">hello new endpoint appears in hello **Endpoints** list on hello same page, and when it's provisioned hello status is **Running**.</span></span>

![Nuevo punto de conexión en la lista](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="32d48-151">Hola extremo de red CDN de prueba</span><span class="sxs-lookup"><span data-stu-id="32d48-151">Test hello CDN endpoint</span></span>

<span data-ttu-id="32d48-152">Si ha seleccionado el plan de tarifa de Verizon, la propagación del punto de conexión suele tardar unos 90 minutos.</span><span class="sxs-lookup"><span data-stu-id="32d48-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="32d48-153">En Akamai, la propagación tarda unos minutos</span><span class="sxs-lookup"><span data-stu-id="32d48-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="32d48-154">aplicación de ejemplo de Hola tiene un `index.html` archivo y *css*, *img*, y *js* carpetas que contienen otros activos estáticos.</span><span class="sxs-lookup"><span data-stu-id="32d48-154">hello sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="32d48-155">Hola contenido de las rutas de acceso para todos estos archivos Hola igual al extremo de red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-155">hello content paths for all of these files are hello same at hello CDN endpoint.</span></span> <span data-ttu-id="32d48-156">Por ejemplo, redes de hello las siguientes direcciones URL de acceso hello *bootstrap.css* archivo Hola *css* carpeta:</span><span class="sxs-lookup"><span data-stu-id="32d48-156">For example, both of hello following URLs access hello *bootstrap.css* file in hello *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="32d48-157">Navegar por un toohello explorador después de la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="32d48-157">Navigate a browser toohello following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![Página de inicio de la aplicación de ejemplo servida desde la red CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="32d48-159">Vea Hola misma página que se ha ejecutado anteriormente en una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="32d48-159">You see hello same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="32d48-160">Red CDN de Azure recuperado activos de la aplicación web de hello origen y sirve de punto de conexión de red CDN Hola</span><span class="sxs-lookup"><span data-stu-id="32d48-160">Azure CDN has retrieved hello origin web app's assets and is serving them from hello CDN endpoint</span></span>

<span data-ttu-id="32d48-161">tooensure que esta página se almacena en caché en hello CDN, página de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-161">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> <span data-ttu-id="32d48-162">Dos solicitudes para hello mismo activo a veces son necesarias para hello toocache CDN Hola contenido solicitado.</span><span class="sxs-lookup"><span data-stu-id="32d48-162">Two requests for hello same asset are sometimes required for hello CDN toocache hello requested content.</span></span>

<span data-ttu-id="32d48-163">Para más información acerca de cómo crear perfiles y puntos de conexión de Azure CDN, consulte [Introducción a Azure CDN](../cdn/cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="32d48-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-hello-cdn"></a><span data-ttu-id="32d48-164">Purgar CDN Hola</span><span class="sxs-lookup"><span data-stu-id="32d48-164">Purge hello CDN</span></span>

<span data-ttu-id="32d48-165">CDN Hola actualiza periódicamente los recursos de aplicación web de origen de hello en función de la configuración de hello time-to-live (TTL).</span><span class="sxs-lookup"><span data-stu-id="32d48-165">hello CDN periodically refreshes its resources from hello origin web app based on hello time-to-live (TTL) configuration.</span></span> <span data-ttu-id="32d48-166">TTL predeterminado de Hello es siete días.</span><span class="sxs-lookup"><span data-stu-id="32d48-166">hello default TTL is seven days.</span></span>

<span data-ttu-id="32d48-167">En ocasiones tendrá que toorefresh Hola CDN antes de hello caducidad de TTL: por ejemplo, cuando se implementa la aplicación web de toohello contenido actualizado.</span><span class="sxs-lookup"><span data-stu-id="32d48-167">At times you might need toorefresh hello CDN before hello TTL expiration -- for example, when you deploy updated content toohello web app.</span></span> <span data-ttu-id="32d48-168">tootrigger una actualización, puede purgar manualmente los recursos de red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-168">tootrigger a refresh, you can manually purge hello CDN resources.</span></span> 

<span data-ttu-id="32d48-169">En esta sección del tutorial de hello, implementar una aplicación web de toohello de cambio y purgar Hola CDN tootrigger Hola CDN toorefresh su memoria caché.</span><span class="sxs-lookup"><span data-stu-id="32d48-169">In this section of hello tutorial, you deploy a change toohello web app and purge hello CDN tootrigger hello CDN toorefresh its cache.</span></span>

### <a name="deploy-a-change-toohello-web-app"></a><span data-ttu-id="32d48-170">Implementar una aplicación web de toohello de cambio</span><span class="sxs-lookup"><span data-stu-id="32d48-170">Deploy a change toohello web app</span></span>

<span data-ttu-id="32d48-171">Abra hello `index.html` de archivos y agregue "-V2" toohello H1 encabezado, tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="32d48-171">Open hello `index.html` file and add "- V2" toohello H1 heading, as shown in hello following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="32d48-172">Confirmar el cambio y lo implementará en la aplicación web de toohello.</span><span class="sxs-lookup"><span data-stu-id="32d48-172">Commit your change and deploy it toohello web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="32d48-173">Una vez completada la implementación, examinar toohello dirección URL de aplicación web y ver Hola cambian.</span><span class="sxs-lookup"><span data-stu-id="32d48-173">Once deployment has completed, browse toohello web app URL and you see hello change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![V2 en el título de la aplicación web](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="32d48-175">Examinar toohello CDN dirección URL del extremo para la página principal de Hola y no se ve Hola cambiar porque la versión almacenada en caché de hello en CDN Hola no ha expirado todavía.</span><span class="sxs-lookup"><span data-stu-id="32d48-175">Browse toohello CDN endpoint URL for hello home page and you don't see hello change because hello cached version in hello CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![Sin título V2 en la red CDN](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a><span data-ttu-id="32d48-177">Purgar Hola CDN en el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="32d48-177">Purge hello CDN in hello portal</span></span>

<span data-ttu-id="32d48-178">tootrigger Hola CDN tooupdate su versión almacenada en caché, purgar CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-178">tootrigger hello CDN tooupdate its cached version, purge hello CDN.</span></span>

<span data-ttu-id="32d48-179">En hello portal de navegación izquierdo, seleccione **grupos de recursos**y, a continuación, seleccione grupo de recursos de Hola que creó para la aplicación web (myResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="32d48-179">In hello portal left navigation, select **Resource groups**, and then select hello resource group that you created for your web app (myResourceGroup).</span></span>

![Selección de un grupo de recursos](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="32d48-181">En lista de Hola de recursos, seleccione el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="32d48-181">In hello list of resources, select your CDN endpoint.</span></span>

![Selección del punto de conexión](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="32d48-183">En parte superior de Hola de hello **extremo** página, haga clic en **purgar**.</span><span class="sxs-lookup"><span data-stu-id="32d48-183">At hello top of hello **Endpoint** page, click **Purge**.</span></span>

![Seleccionar Purgar](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="32d48-185">Escriba Hola contenido las rutas de acceso que se va toopurge.</span><span class="sxs-lookup"><span data-stu-id="32d48-185">Enter hello content paths you wish toopurge.</span></span> <span data-ttu-id="32d48-186">Puede pasar un toopurge de ruta de acceso completa del archivo de un archivo individual o un toopurge de segmento de ruta de acceso y actualizar todo el contenido de una carpeta.</span><span class="sxs-lookup"><span data-stu-id="32d48-186">You can pass a complete file path toopurge an individual file, or a path segment toopurge and refresh all content in a folder.</span></span> <span data-ttu-id="32d48-187">Puesto que ha cambiado `index.html`, asegúrese de que es una de las rutas de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-187">Since you changed `index.html`, make sure that is one of hello paths.</span></span>

<span data-ttu-id="32d48-188">En hello parte inferior de la página de hello, seleccione **purgar**.</span><span class="sxs-lookup"><span data-stu-id="32d48-188">At hello bottom of hello page, select **Purge**.</span></span>

![Página Purgar](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a><span data-ttu-id="32d48-190">Compruebe que Hola que CDN se actualiza</span><span class="sxs-lookup"><span data-stu-id="32d48-190">Verify that hello CDN is updated</span></span>

<span data-ttu-id="32d48-191">Espere hasta que la solicitud de purga de hello finaliza el procesamiento, normalmente un par de minutos.</span><span class="sxs-lookup"><span data-stu-id="32d48-191">Wait until hello purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="32d48-192">toosee Hola estado actual, un icono de campana Hola seleccione parte superior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-192">toosee hello current status, select hello bell icon at hello top of hello page.</span></span> 

![Notificación de purga](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="32d48-194">Examinar dirección URL del extremo CDN de toohello para `index.html`, y ahora verá Hola V2 agregó toohello título en la página de inicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-194">Browse toohello CDN endpoint URL for `index.html`, and now you see hello V2 that you added toohello title on hello home page.</span></span> <span data-ttu-id="32d48-195">Esto muestra que se ha actualizado la caché de la red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-195">This shows that hello CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![V2 en el título en la red CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="32d48-197">Para más información, consulte [Purgar un punto de conexión de Azure CDN](../cdn/cdn-purge-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="32d48-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-tooversion-content"></a><span data-ttu-id="32d48-198">Usar el contenido de tooversion de cadenas de consulta</span><span class="sxs-lookup"><span data-stu-id="32d48-198">Use query strings tooversion content</span></span>

<span data-ttu-id="32d48-199">Hola CDN de Azure ofrece Hola siguientes opciones de comportamiento de almacenamiento en caché:</span><span class="sxs-lookup"><span data-stu-id="32d48-199">hello Azure CDN offers hello following caching behavior options:</span></span>

* <span data-ttu-id="32d48-200">Pasar por alto las cadenas de consulta</span><span class="sxs-lookup"><span data-stu-id="32d48-200">Ignore query strings</span></span>
* <span data-ttu-id="32d48-201">Omitir el almacenamiento en caché de cadenas de consulta</span><span class="sxs-lookup"><span data-stu-id="32d48-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="32d48-202">Almacenar en caché todas las URL únicas</span><span class="sxs-lookup"><span data-stu-id="32d48-202">Cache every unique URL</span></span> 

<span data-ttu-id="32d48-203">Hola primero de ellos es el valor predeterminado de hello, lo que significa que hay solo una versión almacenada en caché de un recurso, independientemente de la cadena de consulta de hello en dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-203">hello first of these is hello default, which means there is only one cached version of an asset regardless of hello query string in hello URL.</span></span> 

<span data-ttu-id="32d48-204">En esta sección del tutorial de hello, cambiar Hola almacenamiento en caché comportamiento toocache todas las URL únicas.</span><span class="sxs-lookup"><span data-stu-id="32d48-204">In this section of hello tutorial, you change hello caching behavior toocache every unique URL.</span></span>

### <a name="change-hello-cache-behavior"></a><span data-ttu-id="32d48-205">Cambiar el comportamiento de la caché de Hola</span><span class="sxs-lookup"><span data-stu-id="32d48-205">Change hello cache behavior</span></span>

<span data-ttu-id="32d48-206">En el portal de Azure hello **punto de conexión de red CDN** página, seleccione **caché**.</span><span class="sxs-lookup"><span data-stu-id="32d48-206">In hello Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="32d48-207">Seleccione **almacenar en caché todas las URL únicas** de hello **comportamiento almacenamiento en caché de cadena de consulta** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="32d48-207">Select **Cache every unique URL** from hello **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="32d48-208">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="32d48-208">Select **Save**.</span></span>

![Selección del comportamiento de almacenamiento de cadenas de consulta en caché](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="32d48-210">Compruebe que las direcciones URL únicas se almacenan en caché por separado</span><span class="sxs-lookup"><span data-stu-id="32d48-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="32d48-211">En un explorador, navegue toohello portada en el extremo de red CDN Hola, pero incluir una cadena de consulta:</span><span class="sxs-lookup"><span data-stu-id="32d48-211">In a browser, navigate toohello home page at hello CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="32d48-212">CDN Hola devuelve Hola actual aplicación contenido web, que incluye "V2" en el encabezado de Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-212">hello CDN returns hello current web app content, which includes "V2" in hello heading.</span></span> 

<span data-ttu-id="32d48-213">tooensure que esta página se almacena en caché en hello CDN, página de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-213">tooensure that this page is cached in hello CDN, refresh hello page.</span></span> 

<span data-ttu-id="32d48-214">Abra `index.html` y cambiar "V2" demasiado "V3" e implementar el cambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-214">Open `index.html` and change "V2" too"V3", and deploy hello change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="32d48-215">En un explorador, vaya dirección URL del extremo CDN de toohello con una nueva cadena de consulta como `q=2`.</span><span class="sxs-lookup"><span data-stu-id="32d48-215">In a browser, go toohello CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="32d48-216">CDN Hola obtiene Hola actual `index.html` de archivos y muestra "V3".</span><span class="sxs-lookup"><span data-stu-id="32d48-216">hello CDN gets hello current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="32d48-217">Pero si se desplaza el punto de conexión de red CDN de toohello con hello `q=1` cadena de consulta, vea "V2".</span><span class="sxs-lookup"><span data-stu-id="32d48-217">But if you navigate toohello CDN endpoint with hello `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![V3 en el título en la red CDN, cadena de consulta 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![V2 en el título en la red CDN, cadena de consulta 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="32d48-220">Este resultado muestra que cada cadena de consulta se trata de manera diferente:</span><span class="sxs-lookup"><span data-stu-id="32d48-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="32d48-221">q = 1 se usó antes, por lo que se devuelve contenido almacenado en caché (V2).</span><span class="sxs-lookup"><span data-stu-id="32d48-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="32d48-222">q = 2 es nuevo, por lo que el contenido de aplicación web más reciente Hola se recuperan y se devolverán (V3).</span><span class="sxs-lookup"><span data-stu-id="32d48-222">q=2 is new, so hello latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="32d48-223">Para más información, consulte [Control del comportamiento del almacenamiento en caché de Azure CDN con cadenas de consulta](../cdn/cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="32d48-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a><span data-ttu-id="32d48-224">Asignar un punto de conexión de red CDN de tooa de dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="32d48-224">Map a custom domain tooa CDN endpoint</span></span>

<span data-ttu-id="32d48-225">Se asignará el extremo de red CDN de tooyour de dominio personalizado mediante la creación de un registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="32d48-225">You'll map your custom domain tooyour CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="32d48-226">Un registro CNAME es una característica DNS que se asigna a un dominio de destino de tooa de dominio de origen.</span><span class="sxs-lookup"><span data-stu-id="32d48-226">A CNAME record is a DNS feature that maps a source domain tooa destination domain.</span></span> <span data-ttu-id="32d48-227">Por ejemplo, podría asignar `cdn.contoso.com` o `static.contoso.com` demasiado`contoso.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="32d48-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` too`contoso.azureedge.net`.</span></span>

<span data-ttu-id="32d48-228">Si no tiene un dominio personalizado, considere la posibilidad de siguientes hello [tutorial de dominio de servicio de aplicaciones](custom-dns-web-site-buydomains-web-app.md) toopurchase un dominio con Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="32d48-228">If you don't have a custom domain, consider following hello [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) toopurchase a domain using hello Azure portal.</span></span> 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a><span data-ttu-id="32d48-229">Buscar Hola hostname toouse con hello CNAME</span><span class="sxs-lookup"><span data-stu-id="32d48-229">Find hello hostname toouse with hello CNAME</span></span>

<span data-ttu-id="32d48-230">Hola portal de Azure **extremo** página, asegúrese de que **Introducción** está seleccionado en hello dejado de navegación y, a continuación, seleccione hello **+ dominio personalizado** situado en la parte superior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-230">In hello Azure portal **Endpoint** page, make sure **Overview** is selected in hello left navigation, and then select hello **+ Custom Domain** button at hello top of hello page.</span></span>

![Seleccionar Agregar dominio personalizado](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="32d48-232">Hola **agregar un dominio personalizado** página, verá toouse de nombre de host de punto de conexión de hello al crear un registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="32d48-232">In hello **Add a custom domain** page, you see hello endpoint host name toouse in creating a CNAME record.</span></span> <span data-ttu-id="32d48-233">nombre de host de Hola se deriva de las direcciones URL de extremo de red CDN:  **&lt;EndpointName >. azureedge.net**.</span><span class="sxs-lookup"><span data-stu-id="32d48-233">hello host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![Página Agregar dominio](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a><span data-ttu-id="32d48-235">Configurar Hola CNAME con su registrador de dominios</span><span class="sxs-lookup"><span data-stu-id="32d48-235">Configure hello CNAME with your domain registrar</span></span>

<span data-ttu-id="32d48-236">Navegar por el sitio web del registrador de dominios de tooyour y busque la sección hello para la creación de registros DNS.</span><span class="sxs-lookup"><span data-stu-id="32d48-236">Navigate tooyour domain registrar's web site, and locate hello section for creating DNS records.</span></span> <span data-ttu-id="32d48-237">Podría encontrarlo en una sección como **Nombre de dominio**, **DNS** o **Administración del servidor de nombres**.</span><span class="sxs-lookup"><span data-stu-id="32d48-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="32d48-238">Busque la sección de Hola para administrar registros CNAME.</span><span class="sxs-lookup"><span data-stu-id="32d48-238">Find hello section for managing CNAMEs.</span></span> <span data-ttu-id="32d48-239">Puede tener una página de configuración avanzada de toogo tooan y buscar palabras hello CNAME, Alias o subdominios.</span><span class="sxs-lookup"><span data-stu-id="32d48-239">You may have toogo tooan advanced settings page and look for hello words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="32d48-240">Crear un registro CNAME que asigne el subdominio elegido (por ejemplo, **estático** o **cdn**) toohello **nombre de host del punto de conexión** se muestra anteriormente en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) toohello **Endpoint host name** shown earlier in hello portal.</span></span> 

### <a name="enter-hello-custom-domain-in-azure"></a><span data-ttu-id="32d48-241">Escriba el dominio personalizado de hello en Azure</span><span class="sxs-lookup"><span data-stu-id="32d48-241">Enter hello custom domain in Azure</span></span>

<span data-ttu-id="32d48-242">Devolver toohello **agregar un dominio personalizado** página y escriba su dominio personalizado, incluido el subdominio de hello, en el cuadro de diálogo de Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-242">Return toohello **Add a custom domain** page, and enter your custom domain, including hello subdomain, in hello dialog box.</span></span> <span data-ttu-id="32d48-243">Por ejemplo, escriba: `cdn.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="32d48-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="32d48-244">Azure comprueba que existe el registro CNAME de hello para el nombre de dominio de Hola que ha escrito.</span><span class="sxs-lookup"><span data-stu-id="32d48-244">Azure verifies that hello CNAME record exists for hello domain name you have entered.</span></span> <span data-ttu-id="32d48-245">Si Hola CNAME es correcto, se valida su dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="32d48-245">If hello CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="32d48-246">Puede tardar tiempo para los servidores de tooname de hello CNAME toopropagate registro de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="32d48-246">It can take time for hello CNAME record toopropagate tooname servers on hello Internet.</span></span> <span data-ttu-id="32d48-247">Si el dominio no se valida inmediatamente, espere unos minutos e inténtelo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="32d48-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-hello-custom-domain"></a><span data-ttu-id="32d48-248">Dominio personalizado de prueba Hola</span><span class="sxs-lookup"><span data-stu-id="32d48-248">Test hello custom domain</span></span>

<span data-ttu-id="32d48-249">En un explorador, navegue toohello `index.html` archivo utilizando su dominio personalizado (por ejemplo, `cdn.contoso.com/index.html`) tooverify que es el resultado de Hola Hola igual como cuándo pasan directamente demasiado`<endpointname>azureedge.net/index.html`.</span><span class="sxs-lookup"><span data-stu-id="32d48-249">In a browser, navigate toohello `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) tooverify that hello result is hello same as when you go directly too`<endpointname>azureedge.net/index.html`.</span></span>

![Página de inicio de la aplicación de ejemplo utilizando la dirección URL de dominio personalizado](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="32d48-251">Para obtener más información, consulte [dominio personalizado de CDN de Azure de mapa tooa contenido](../cdn/cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="32d48-251">For more information, see [Map Azure CDN content tooa custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="32d48-252">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="32d48-252">Next steps</span></span>

<span data-ttu-id="32d48-253">¿Qué ha aprendido?</span><span class="sxs-lookup"><span data-stu-id="32d48-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="32d48-254">Crear un punto de conexión de CDN.</span><span class="sxs-lookup"><span data-stu-id="32d48-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="32d48-255">Actualizar los recursos en caché.</span><span class="sxs-lookup"><span data-stu-id="32d48-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="32d48-256">Versiones de toocontrol almacenado en memoria caché de cadenas de consulta de uso.</span><span class="sxs-lookup"><span data-stu-id="32d48-256">Use query strings toocontrol cached versions.</span></span>
> * <span data-ttu-id="32d48-257">Usar un dominio personalizado para el extremo de red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="32d48-257">Use a custom domain for hello CDN endpoint.</span></span>

<span data-ttu-id="32d48-258">Obtenga información acerca de cómo los artículos toooptimize de rendimiento de red CDN Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="32d48-258">Learn how toooptimize CDN performance in hello following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="32d48-259">Mejora del rendimiento comprimiendo archivos en la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="32d48-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="32d48-260">Carga previa de activos en un punto de conexión de CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="32d48-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
