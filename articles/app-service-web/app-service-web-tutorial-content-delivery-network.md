---
title: "Adición de una red CDN a una instancia de Azure App Service | Microsoft Docs"
description: "Agregue una red de entrega de contenido a Azure App Service para almacenar en memoria caché y entregar archivos estáticos desde servidores próximos a sus clientes en todo el mundo."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 257b75d01f3904661c1a188a2d53ffcb74f48f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-content-delivery-network-cdn-to-an-azure-app-service"></a><span data-ttu-id="31524-103">Incorporación de una red de entrega de contenido a Azure App Service</span><span class="sxs-lookup"><span data-stu-id="31524-103">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>

<span data-ttu-id="31524-104">[Azure Content Delivery Network](../cdn/cdn-overview.md) almacena en caché contenido web estático en ubicaciones colocadas estratégicamente para obtener el máximo rendimiento a la hora de proporcionar contenido a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="31524-104">[Azure Content Delivery Network (CDN)](../cdn/cdn-overview.md) caches static web content at strategically placed locations to provide maximum throughput for delivering content to users.</span></span> <span data-ttu-id="31524-105">CDN también reduce la carga del servidor en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="31524-105">The CDN also decreases server load on your web app.</span></span> <span data-ttu-id="31524-106">Este tutorial muestra cómo agregar Azure CDN a una [aplicación web de Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="31524-106">This tutorial shows how to add Azure CDN to a [web app in Azure App Service](app-service-web-overview.md).</span></span> 

<span data-ttu-id="31524-107">Esta es la página de inicio del ejemplo del sitio HTML estático que se utilizará:</span><span class="sxs-lookup"><span data-stu-id="31524-107">Here's the home page of the sample static HTML site that you'll work with:</span></span>

![Página de inicio de la aplicación de ejemplo](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

<span data-ttu-id="31524-109">Temas que se abordarán:</span><span class="sxs-lookup"><span data-stu-id="31524-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="31524-110">Crear un punto de conexión de CDN.</span><span class="sxs-lookup"><span data-stu-id="31524-110">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="31524-111">Actualizar los recursos en caché.</span><span class="sxs-lookup"><span data-stu-id="31524-111">Refresh cached assets.</span></span>
> * <span data-ttu-id="31524-112">Utilizar cadenas de consulta para controlar las versiones en caché.</span><span class="sxs-lookup"><span data-stu-id="31524-112">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="31524-113">Utilizar un dominio personalizado para el punto de conexión de CDN.</span><span class="sxs-lookup"><span data-stu-id="31524-113">Use a custom domain for the CDN endpoint.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31524-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="31524-114">Prerequisites</span></span>

<span data-ttu-id="31524-115">Para completar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="31524-115">To complete this tutorial:</span></span>

- [<span data-ttu-id="31524-116">Instalación de Git</span><span class="sxs-lookup"><span data-stu-id="31524-116">Install Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="31524-117">Instalación de la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="31524-117">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-web-app"></a><span data-ttu-id="31524-118">Creación de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="31524-118">Create the web app</span></span>

<span data-ttu-id="31524-119">Para crear la aplicación web con la que va a trabajar, siga el [tutorial de inicio rápido de HTML estático](app-service-web-get-started-html.md) mediante el paso de **búsqueda de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="31524-119">To create the web app that you'll work with, follow the [static HTML quickstart](app-service-web-get-started-html.md) through the **Browse to the app** step.</span></span>

### <a name="have-a-custom-domain-ready"></a><span data-ttu-id="31524-120">Tenga listo un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="31524-120">Have a custom domain ready</span></span>

<span data-ttu-id="31524-121">Para realizar el paso de dominio personalizado de este tutorial, debe tener un dominio personalizado y tener acceso al Registro DNS del proveedor de dominios (por ejemplo, GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="31524-121">To complete the custom domain step of this tutorial, you need to own a custom domain and have access to your DNS registry for your domain provider (such as GoDaddy).</span></span> <span data-ttu-id="31524-122">Por ejemplo, para agregar entradas DNS para `contoso.com` y `www.contoso.com`, debe tener acceso para configurar las opciones de configuración DNS del dominio raíz `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="31524-122">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must have access to configure the DNS settings for the `contoso.com` root domain.</span></span>

<span data-ttu-id="31524-123">Si aún no tiene un nombre de dominio, puede seguir el tutorial [Comprar y configurar un nombre de dominio personalizado en Azure App Service](custom-dns-web-site-buydomains-web-app.md) para comprar un dominio mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="31524-123">If you don't already have a domain name, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="31524-124">Iniciar sesión en el portal de Azure</span><span class="sxs-lookup"><span data-stu-id="31524-124">Log in to the Azure portal</span></span>

<span data-ttu-id="31524-125">Abra un explorador y vaya a [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="31524-125">Open a browser and navigate to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-a-cdn-profile-and-endpoint"></a><span data-ttu-id="31524-126">Creación de un perfil y un punto de conexión de CDN</span><span class="sxs-lookup"><span data-stu-id="31524-126">Create a CDN profile and endpoint</span></span>

<span data-ttu-id="31524-127">En el panel de navegación izquierdo, seleccione **App Services** y, a continuación, seleccione la aplicación que creó en el tutorial [Creación de una aplicación web HTML estática en Azure en cinco minutos](app-service-web-get-started-html.md).</span><span class="sxs-lookup"><span data-stu-id="31524-127">In the left navigation, select **App Services**, and then select the app that you created in the [static HTML quickstart](app-service-web-get-started-html.md).</span></span>

![Selección de la aplicación de App Service en el portal](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

<span data-ttu-id="31524-129">En la página **App Service**, en la sección **Configuración**, seleccione **Redes > Configurar Azure CDN para la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="31524-129">In the **App Service** page, in the **Settings** section, select **Networking > Configure Azure CDN for your app**.</span></span>

![Selección de la instancia de CDN en el portal](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

<span data-ttu-id="31524-131">En la página **Azure Content Delivery Network**, proporcione la configuración del **Nuevo punto de conexión** tal y como se especifica en la tabla.</span><span class="sxs-lookup"><span data-stu-id="31524-131">In the **Azure Content Delivery Network** page, provide the **New endpoint** settings as specified in the table.</span></span>

![Creación del perfil y el punto de conexión en el portal](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| <span data-ttu-id="31524-133">Configuración</span><span class="sxs-lookup"><span data-stu-id="31524-133">Setting</span></span> | <span data-ttu-id="31524-134">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="31524-134">Suggested value</span></span> | <span data-ttu-id="31524-135">Descripción</span><span class="sxs-lookup"><span data-stu-id="31524-135">Description</span></span> |
| ------- | --------------- | ----------- |
| <span data-ttu-id="31524-136">**Perfil de CDN**</span><span class="sxs-lookup"><span data-stu-id="31524-136">**CDN profile**</span></span> | <span data-ttu-id="31524-137">myCDNProfile</span><span class="sxs-lookup"><span data-stu-id="31524-137">myCDNProfile</span></span> | <span data-ttu-id="31524-138">Seleccione **Crear nuevo** para crear un nuevo perfil de red CDN.</span><span class="sxs-lookup"><span data-stu-id="31524-138">Select **Create new** to create a CDN profile.</span></span> <span data-ttu-id="31524-139">Un perfil de CDN es una colección de puntos de conexión de CDN con el mismo plan de tarifa.</span><span class="sxs-lookup"><span data-stu-id="31524-139">A CDN profile is a collection of CDN endpoints with the same pricing tier.</span></span> |
| <span data-ttu-id="31524-140">**Plan de tarifa**</span><span class="sxs-lookup"><span data-stu-id="31524-140">**Pricing tier**</span></span> | <span data-ttu-id="31524-141">Estándar de Akamai</span><span class="sxs-lookup"><span data-stu-id="31524-141">Standard Akamai</span></span> | <span data-ttu-id="31524-142">El [plan de tarifa](../cdn/cdn-overview.md#azure-cdn-features) especifica el proveedor y las características disponibles.</span><span class="sxs-lookup"><span data-stu-id="31524-142">The [pricing tier](../cdn/cdn-overview.md#azure-cdn-features) specifies the provider and available features.</span></span> <span data-ttu-id="31524-143">En este tutorial, usamos Akamai estándar.</span><span class="sxs-lookup"><span data-stu-id="31524-143">In this tutorial, we are using Standard Akamai.</span></span> |
| <span data-ttu-id="31524-144">**Nombre del punto de conexión de CDN**</span><span class="sxs-lookup"><span data-stu-id="31524-144">**CDN endpoint name**</span></span> | <span data-ttu-id="31524-145">Cualquier nombre que sea único en el dominio azureedge.net</span><span class="sxs-lookup"><span data-stu-id="31524-145">Any name that is unique in the azureedge.net domain</span></span> | <span data-ttu-id="31524-146">Accederá a los recursos en caché en el dominio  *\<nombrePuntoConexión>.azureedge.net*.</span><span class="sxs-lookup"><span data-stu-id="31524-146">You access your cached resources at the domain *\<endpointname>.azureedge.net*.</span></span>

<span data-ttu-id="31524-147">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="31524-147">Select **Create**.</span></span>

<span data-ttu-id="31524-148">Azure crea el perfil y el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="31524-148">Azure creates the profile and endpoint.</span></span> <span data-ttu-id="31524-149">El nuevo punto de conexión aparece en la lista **Puntos de conexión** de la misma página y, una vez aprovisionado, el estado es **En ejecución**.</span><span class="sxs-lookup"><span data-stu-id="31524-149">The new endpoint appears in the **Endpoints** list on the same page, and when it's provisioned the status is **Running**.</span></span>

![Nuevo punto de conexión en la lista](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-the-cdn-endpoint"></a><span data-ttu-id="31524-151">Probar el punto de conexión de CDN</span><span class="sxs-lookup"><span data-stu-id="31524-151">Test the CDN endpoint</span></span>

<span data-ttu-id="31524-152">Si ha seleccionado el plan de tarifa de Verizon, la propagación del punto de conexión suele tardar unos 90 minutos.</span><span class="sxs-lookup"><span data-stu-id="31524-152">If you selected Verizon pricing tier, it typically takes about 90 minutes for endpoint propagation.</span></span> <span data-ttu-id="31524-153">En Akamai, la propagación tarda unos minutos</span><span class="sxs-lookup"><span data-stu-id="31524-153">For Akamai, it takes a couple minutes for propagation</span></span>

<span data-ttu-id="31524-154">La aplicación de ejemplo tiene un archivo `index.html` y las carpetas *css*, *img* y *js*, que contienen otros recursos estáticos.</span><span class="sxs-lookup"><span data-stu-id="31524-154">The sample app has an `index.html` file and *css*, *img*, and *js* folders that contain other static assets.</span></span> <span data-ttu-id="31524-155">Las rutas de acceso de contenido para todos estos archivos son las mismas en el punto de conexión de CDN.</span><span class="sxs-lookup"><span data-stu-id="31524-155">The content paths for all of these files are the same at the CDN endpoint.</span></span> <span data-ttu-id="31524-156">Por ejemplo, las siguientes direcciones URL acceden ambas al archivo *bootstrap.css* en la carpeta *css*:</span><span class="sxs-lookup"><span data-stu-id="31524-156">For example, both of the following URLs access the *bootstrap.css* file in the *css* folder:</span></span>

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

<span data-ttu-id="31524-157">Mediante un explorador, vaya la dirección URL siguiente:</span><span class="sxs-lookup"><span data-stu-id="31524-157">Navigate a browser to the following URL:</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![Página de inicio de la aplicación de ejemplo servida desde la red CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 <span data-ttu-id="31524-159">Verá la misma página que ejecutó anteriormente en una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="31524-159">You see the same page that you ran earlier in an Azure web app.</span></span> <span data-ttu-id="31524-160">Azure CDN ha recuperado los recursos de la aplicación web original y los sirve desde el punto de conexión de CDN.</span><span class="sxs-lookup"><span data-stu-id="31524-160">Azure CDN has retrieved the origin web app's assets and is serving them from the CDN endpoint</span></span>

<span data-ttu-id="31524-161">Para asegurarse de que esta página se almacena en caché en la red CDN, actualice la página.</span><span class="sxs-lookup"><span data-stu-id="31524-161">To ensure that this page is cached in the CDN, refresh the page.</span></span> <span data-ttu-id="31524-162">En ocasiones se necesitan dos solicitudes del mismo recurso para que la red CDN almacene en memoria caché el contenido solicitado.</span><span class="sxs-lookup"><span data-stu-id="31524-162">Two requests for the same asset are sometimes required for the CDN to cache the requested content.</span></span>

<span data-ttu-id="31524-163">Para más información acerca de cómo crear perfiles y puntos de conexión de Azure CDN, consulte [Introducción a Azure CDN](../cdn/cdn-create-new-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="31524-163">For more information about creating Azure CDN profiles and endpoints, see [Getting started with Azure CDN](../cdn/cdn-create-new-endpoint.md).</span></span>

## <a name="purge-the-cdn"></a><span data-ttu-id="31524-164">Purga de la red CDN</span><span class="sxs-lookup"><span data-stu-id="31524-164">Purge the CDN</span></span>

<span data-ttu-id="31524-165">La red CDN actualiza periódicamente los recursos desde la aplicación web original en función de la configuración del período de vida (TTL).</span><span class="sxs-lookup"><span data-stu-id="31524-165">The CDN periodically refreshes its resources from the origin web app based on the time-to-live (TTL) configuration.</span></span> <span data-ttu-id="31524-166">El TTL predeterminado es siete días.</span><span class="sxs-lookup"><span data-stu-id="31524-166">The default TTL is seven days.</span></span>

<span data-ttu-id="31524-167">En ocasiones podría necesitar actualizar la red CDN antes de la expiración del TTL; por ejemplo, al implementar contenido actualizado en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="31524-167">At times you might need to refresh the CDN before the TTL expiration -- for example, when you deploy updated content to the web app.</span></span> <span data-ttu-id="31524-168">Para desencadenar una actualización, puede purgar manualmente los recursos de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="31524-168">To trigger a refresh, you can manually purge the CDN resources.</span></span> 

<span data-ttu-id="31524-169">En esta sección del tutorial, se implementará un cambio en la aplicación web y se purgará la red CDN para desencadenar la actualización de su caché.</span><span class="sxs-lookup"><span data-stu-id="31524-169">In this section of the tutorial, you deploy a change to the web app and purge the CDN to trigger the CDN to refresh its cache.</span></span>

### <a name="deploy-a-change-to-the-web-app"></a><span data-ttu-id="31524-170">Implementación de cambios en la aplicación web</span><span class="sxs-lookup"><span data-stu-id="31524-170">Deploy a change to the web app</span></span>

<span data-ttu-id="31524-171">Abra el archivo `index.html` y agregue "- V2" al encabezado H1, como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="31524-171">Open the `index.html` file and add "- V2" to the H1 heading, as shown in the following example:</span></span> 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

<span data-ttu-id="31524-172">Confirme el cambio e impleméntelo en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="31524-172">Commit your change and deploy it to the web app.</span></span>

```bash
git commit -am "version 2"
git push azure master
```

<span data-ttu-id="31524-173">Una vez finalizada la implementación, vaya a la dirección URL de la aplicación web y podrá ver el cambio.</span><span class="sxs-lookup"><span data-stu-id="31524-173">Once deployment has completed, browse to the web app URL and you see the change.</span></span>

```
http://<appname>.azurewebsites.net/index.html
```

![V2 en el título de la aplicación web](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

<span data-ttu-id="31524-175">Vaya a la dirección URL de la página de inicio del punto de conexión de CDN y no verá el cambio porque la versión almacenada en caché en la red CDN no ha expirado todavía.</span><span class="sxs-lookup"><span data-stu-id="31524-175">Browse to the CDN endpoint URL for the home page and you don't see the change because the cached version in the CDN hasn't expired yet.</span></span> 

```
http://<endpointname>.azureedge.net/index.html
```

![Sin título V2 en la red CDN](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-the-cdn-in-the-portal"></a><span data-ttu-id="31524-177">Purga de la red CDN en el portal</span><span class="sxs-lookup"><span data-stu-id="31524-177">Purge the CDN in the portal</span></span>

<span data-ttu-id="31524-178">Para hacer que la red CDN actualice la versión almacenada en caché, purgue la red CDN.</span><span class="sxs-lookup"><span data-stu-id="31524-178">To trigger the CDN to update its cached version, purge the CDN.</span></span>

<span data-ttu-id="31524-179">En el área de navegación izquierda del portal, seleccione **Grupos de recursos** y, a continuación, seleccione el grupo de recursos que ha creado para la aplicación web (myResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="31524-179">In the portal left navigation, select **Resource groups**, and then select the resource group that you created for your web app (myResourceGroup).</span></span>

![Selección de un grupo de recursos](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

<span data-ttu-id="31524-181">En la lista de recursos, seleccione el punto de conexión de CDN.</span><span class="sxs-lookup"><span data-stu-id="31524-181">In the list of resources, select your CDN endpoint.</span></span>

![Selección del punto de conexión](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

<span data-ttu-id="31524-183">En la parte superior de la página **Punto de conexión**, haga clic en **Purgar**.</span><span class="sxs-lookup"><span data-stu-id="31524-183">At the top of the **Endpoint** page, click **Purge**.</span></span>

![Seleccionar Purgar](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

<span data-ttu-id="31524-185">Escriba las rutas de acceso al contenido que desea purgar.</span><span class="sxs-lookup"><span data-stu-id="31524-185">Enter the content paths you wish to purge.</span></span> <span data-ttu-id="31524-186">Puede pasar una ruta de acceso de archivo completa para purgar un archivo individual, o un segmento de ruta de acceso para purgar y actualizar todo el contenido de una carpeta.</span><span class="sxs-lookup"><span data-stu-id="31524-186">You can pass a complete file path to purge an individual file, or a path segment to purge and refresh all content in a folder.</span></span> <span data-ttu-id="31524-187">Puesto que ha cambiado `index.html`, asegúrese de que es una de las rutas de acceso.</span><span class="sxs-lookup"><span data-stu-id="31524-187">Since you changed `index.html`, make sure that is one of the paths.</span></span>

<span data-ttu-id="31524-188">En la parte inferior de la página, seleccione **Purgar**.</span><span class="sxs-lookup"><span data-stu-id="31524-188">At the bottom of the page, select **Purge**.</span></span>

![Página Purgar](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-the-cdn-is-updated"></a><span data-ttu-id="31524-190">Compruebe que se ha actualizado la red CDN</span><span class="sxs-lookup"><span data-stu-id="31524-190">Verify that the CDN is updated</span></span>

<span data-ttu-id="31524-191">Espere hasta que la solicitud de purga finalice el procesamiento; por lo general, un par de minutos.</span><span class="sxs-lookup"><span data-stu-id="31524-191">Wait until the purge request finishes processing, typically a couple of minutes.</span></span> <span data-ttu-id="31524-192">Para ver el estado actual, seleccione el icono de campana en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="31524-192">To see the current status, select the bell icon at the top of the page.</span></span> 

![Notificación de purga](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

<span data-ttu-id="31524-194">Vaya a la dirección URL del punto de conexión de CDN de `index.html` y ahora verá el texto V2 que agregó al título de la página principal.</span><span class="sxs-lookup"><span data-stu-id="31524-194">Browse to the CDN endpoint URL for `index.html`, and now you see the V2 that you added to the title on the home page.</span></span> <span data-ttu-id="31524-195">Esto muestra que se ha actualizado la caché de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="31524-195">This shows that the CDN cache has been refreshed.</span></span>

```
http://<endpointname>.azureedge.net/index.html
```

![V2 en el título en la red CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

<span data-ttu-id="31524-197">Para más información, consulte [Purgar un punto de conexión de Azure CDN](../cdn/cdn-purge-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="31524-197">For more information, see [Purge an Azure CDN endpoint](../cdn/cdn-purge-endpoint.md).</span></span> 

## <a name="use-query-strings-to-version-content"></a><span data-ttu-id="31524-198">Utilizar cadenas de consulta para versiones del contenido</span><span class="sxs-lookup"><span data-stu-id="31524-198">Use query strings to version content</span></span>

<span data-ttu-id="31524-199">Azure CDN ofrece las siguientes opciones de comportamiento de almacenamiento en caché:</span><span class="sxs-lookup"><span data-stu-id="31524-199">The Azure CDN offers the following caching behavior options:</span></span>

* <span data-ttu-id="31524-200">Pasar por alto las cadenas de consulta</span><span class="sxs-lookup"><span data-stu-id="31524-200">Ignore query strings</span></span>
* <span data-ttu-id="31524-201">Omitir el almacenamiento en caché de cadenas de consulta</span><span class="sxs-lookup"><span data-stu-id="31524-201">Bypass caching for query strings</span></span>
* <span data-ttu-id="31524-202">Almacenar en caché todas las URL únicas</span><span class="sxs-lookup"><span data-stu-id="31524-202">Cache every unique URL</span></span> 

<span data-ttu-id="31524-203">El primero de ellos es el comportamiento predeterminado, lo que significa que solo hay una versión almacenada en caché de un recurso, independientemente de la cadena de consulta utilizada en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="31524-203">The first of these is the default, which means there is only one cached version of an asset regardless of the query string in the URL.</span></span> 

<span data-ttu-id="31524-204">En esta sección del tutorial, cambiará el comportamiento de almacenamiento en caché para almacenar en caché todas las direcciones URL únicas.</span><span class="sxs-lookup"><span data-stu-id="31524-204">In this section of the tutorial, you change the caching behavior to cache every unique URL.</span></span>

### <a name="change-the-cache-behavior"></a><span data-ttu-id="31524-205">Cambio del comportamiento de la memoria caché</span><span class="sxs-lookup"><span data-stu-id="31524-205">Change the cache behavior</span></span>

<span data-ttu-id="31524-206">En la página **Punto de conexión de CDN** de Azure Portal, seleccione **Caché**.</span><span class="sxs-lookup"><span data-stu-id="31524-206">In the Azure portal **CDN Endpoint** page, select **Cache**.</span></span>

<span data-ttu-id="31524-207">Seleccione **Almacenar en caché todas las URL únicas** en la lista desplegable **Comportamiento del almacenamiento en caché de cadenas de consulta**.</span><span class="sxs-lookup"><span data-stu-id="31524-207">Select **Cache every unique URL** from the **Query string caching behavior** drop-down list.</span></span>

<span data-ttu-id="31524-208">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="31524-208">Select **Save**.</span></span>

![Selección del comportamiento de almacenamiento de cadenas de consulta en caché](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a><span data-ttu-id="31524-210">Compruebe que las direcciones URL únicas se almacenan en caché por separado</span><span class="sxs-lookup"><span data-stu-id="31524-210">Verify that unique URLs are cached separately</span></span>

<span data-ttu-id="31524-211">En un explorador, vaya a la página de inicio del punto de conexión de CDN, pero incluya una cadena de consulta:</span><span class="sxs-lookup"><span data-stu-id="31524-211">In a browser, navigate to the home page at the CDN endpoint, but include a query string:</span></span> 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

<span data-ttu-id="31524-212">La red CDN devuelve el contenido de la aplicación web actual, que incluye "V2" en el encabezado.</span><span class="sxs-lookup"><span data-stu-id="31524-212">The CDN returns the current web app content, which includes "V2" in the heading.</span></span> 

<span data-ttu-id="31524-213">Para asegurarse de que esta página se almacena en caché en la red CDN, actualice la página.</span><span class="sxs-lookup"><span data-stu-id="31524-213">To ensure that this page is cached in the CDN, refresh the page.</span></span> 

<span data-ttu-id="31524-214">Abra `index.html`, cambie "V2" por "V3" e implemente el cambio.</span><span class="sxs-lookup"><span data-stu-id="31524-214">Open `index.html` and change "V2" to "V3", and deploy the change.</span></span> 

```bash
git commit -am "version 3"
git push azure master
```

<span data-ttu-id="31524-215">En un explorador, vaya a la dirección URL del punto de conexión CDN con una nueva cadena de consulta como `q=2`.</span><span class="sxs-lookup"><span data-stu-id="31524-215">In a browser, go to the CDN endpoint URL with a new query string such as `q=2`.</span></span> <span data-ttu-id="31524-216">La red CDN obtiene el archivo `index.html` actual y muestra "V3".</span><span class="sxs-lookup"><span data-stu-id="31524-216">The CDN gets the current `index.html` file and displays "V3".</span></span>  <span data-ttu-id="31524-217">Sin embargo, si navega hasta el punto de conexión de CDN con la cadena de consulta `q=1`, verá "V2".</span><span class="sxs-lookup"><span data-stu-id="31524-217">But if you navigate to the CDN endpoint with the `q=1` query string, you see "V2".</span></span>

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![V3 en el título en la red CDN, cadena de consulta 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![V2 en el título en la red CDN, cadena de consulta 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

<span data-ttu-id="31524-220">Este resultado muestra que cada cadena de consulta se trata de manera diferente:</span><span class="sxs-lookup"><span data-stu-id="31524-220">This output shows that each query string is treated differently:</span></span>

* <span data-ttu-id="31524-221">q = 1 se usó antes, por lo que se devuelve contenido almacenado en caché (V2).</span><span class="sxs-lookup"><span data-stu-id="31524-221">q=1 was used before, so cached contents are returned (V2).</span></span>
* <span data-ttu-id="31524-222">q = 2 es nuevo, por lo que se recupera y se devuelve el contenido de aplicación web más reciente (V3).</span><span class="sxs-lookup"><span data-stu-id="31524-222">q=2 is new, so the latest web app contents are retrieved and returned (V3).</span></span>

<span data-ttu-id="31524-223">Para más información, consulte [Control del comportamiento del almacenamiento en caché de Azure CDN con cadenas de consulta](../cdn/cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="31524-223">For more information, see [Control Azure CDN caching behavior with query strings](../cdn/cdn-query-string.md).</span></span>

## <a name="map-a-custom-domain-to-a-cdn-endpoint"></a><span data-ttu-id="31524-224">Asignación de un dominio personalizado a un punto de conexión de CDN</span><span class="sxs-lookup"><span data-stu-id="31524-224">Map a custom domain to a CDN endpoint</span></span>

<span data-ttu-id="31524-225">Se asigna el dominio personalizado al punto de conexión de CDN mediante la creación de un registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="31524-225">You'll map your custom domain to your CDN Endpoint by creating a CNAME record.</span></span> <span data-ttu-id="31524-226">Un registro CNAME es una característica DNS que asigna un dominio de origen a un dominio de destino.</span><span class="sxs-lookup"><span data-stu-id="31524-226">A CNAME record is a DNS feature that maps a source domain to a destination domain.</span></span> <span data-ttu-id="31524-227">Por ejemplo, podría asignar `cdn.contoso.com` o `static.contoso.com` a `contoso.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="31524-227">For example, you might map `cdn.contoso.com` or `static.contoso.com` to `contoso.azureedge.net`.</span></span>

<span data-ttu-id="31524-228">Si no tiene un dominio personalizado, puede seguir el tutorial [Comprar y configurar un nombre de dominio personalizado en Azure App Service](custom-dns-web-site-buydomains-web-app.md) para comprar un dominio mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="31524-228">If you don't have a custom domain, consider following the [App Service domain tutorial](custom-dns-web-site-buydomains-web-app.md) to purchase a domain using the Azure portal.</span></span> 

### <a name="find-the-hostname-to-use-with-the-cname"></a><span data-ttu-id="31524-229">Búsqueda del nombre de host que se utilizará con el registro CNAME</span><span class="sxs-lookup"><span data-stu-id="31524-229">Find the hostname to use with the CNAME</span></span>

<span data-ttu-id="31524-230">En la página **Punto de conexión** de Azure Portal, asegúrese de que **Introducción** está seleccionado en el panel de navegación izquierdo y, a continuación, seleccione el botón **+ Dominio personalizado**, en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="31524-230">In the Azure portal **Endpoint** page, make sure **Overview** is selected in the left navigation, and then select the **+ Custom Domain** button at the top of the page.</span></span>

![Seleccionar Agregar dominio personalizado](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

<span data-ttu-id="31524-232">En la página **Agregar un dominio personalizado**, verá el nombre de host del punto de conexión que debe utilizar para crear un registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="31524-232">In the **Add a custom domain** page, you see the endpoint host name to use in creating a CNAME record.</span></span> <span data-ttu-id="31524-233">El nombre de host se deriva de la dirección URL del punto de conexión de CDN: **&lt;NombrePuntoConexión>.azureedge.net**.</span><span class="sxs-lookup"><span data-stu-id="31524-233">The host name is derived from your CDN endpoint URL: **&lt;EndpointName>.azureedge.net**.</span></span> 

![Página Agregar dominio](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-the-cname-with-your-domain-registrar"></a><span data-ttu-id="31524-235">Configuración del registro CNAME con su registrador de dominios</span><span class="sxs-lookup"><span data-stu-id="31524-235">Configure the CNAME with your domain registrar</span></span>

<span data-ttu-id="31524-236">Navegue al sitio web del registrador y localice la sección para crear registros DNS.</span><span class="sxs-lookup"><span data-stu-id="31524-236">Navigate to your domain registrar's web site, and locate the section for creating DNS records.</span></span> <span data-ttu-id="31524-237">Podría encontrarlo en una sección como **Nombre de dominio**, **DNS** o **Administración del servidor de nombres**.</span><span class="sxs-lookup"><span data-stu-id="31524-237">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>

<span data-ttu-id="31524-238">Busque la sección para la administración de CNAME.</span><span class="sxs-lookup"><span data-stu-id="31524-238">Find the section for managing CNAMEs.</span></span> <span data-ttu-id="31524-239">Tiene que dirigirse a la página de configuración avanzada y buscar las palabras CNAME, Alias o Subdomains.</span><span class="sxs-lookup"><span data-stu-id="31524-239">You may have to go to an advanced settings page and look for the words CNAME, Alias, or Subdomains.</span></span>

<span data-ttu-id="31524-240">Cree un nuevo registro CNAME que asigne el subdominio elegido (por ejemplo, **static** o **cdn**) al **nombre de host del punto de conexión** que se mostró anteriormente en el portal.</span><span class="sxs-lookup"><span data-stu-id="31524-240">Create a CNAME record that maps your chosen subdomain (for example, **static** or **cdn**) to the **Endpoint host name** shown earlier in the portal.</span></span> 

### <a name="enter-the-custom-domain-in-azure"></a><span data-ttu-id="31524-241">Escriba el dominio personalizado en Azure</span><span class="sxs-lookup"><span data-stu-id="31524-241">Enter the custom domain in Azure</span></span>

<span data-ttu-id="31524-242">Vuelva a la página **Agregar un dominio personalizado** y escriba su dominio personalizado, incluido el subdominio, en el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="31524-242">Return to the **Add a custom domain** page, and enter your custom domain, including the subdomain, in the dialog box.</span></span> <span data-ttu-id="31524-243">Por ejemplo, escriba: `cdn.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="31524-243">For example, enter `cdn.contoso.com`.</span></span>   
   
<span data-ttu-id="31524-244">Azure comprobará que el registro CNAME existe para el nombre de dominio que ha escrito.</span><span class="sxs-lookup"><span data-stu-id="31524-244">Azure verifies that the CNAME record exists for the domain name you have entered.</span></span> <span data-ttu-id="31524-245">Si el registro CNAME es correcto, el dominio personalizado se valida.</span><span class="sxs-lookup"><span data-stu-id="31524-245">If the CNAME is correct, your custom domain is validated.</span></span>

<span data-ttu-id="31524-246">La propagación del registro CNAME en los servidores de nombres de Internet puede llevar cierto tiempo.</span><span class="sxs-lookup"><span data-stu-id="31524-246">It can take time for the CNAME record to propagate to name servers on the Internet.</span></span> <span data-ttu-id="31524-247">Si el dominio no se valida inmediatamente, espere unos minutos e inténtelo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="31524-247">If your domain is not validated immediately, wait a few minutes and try again.</span></span>

### <a name="test-the-custom-domain"></a><span data-ttu-id="31524-248">Prueba del dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="31524-248">Test the custom domain</span></span>

<span data-ttu-id="31524-249">En un explorador, vaya hasta el archivo `index.html` utilizando su dominio personalizado (por ejemplo, `cdn.contoso.com/index.html`) para comprobar que el resultado es el mismo que cuando va directamente a `<endpointname>azureedge.net/index.html`.</span><span class="sxs-lookup"><span data-stu-id="31524-249">In a browser, navigate to the `index.html` file using your custom domain (for example, `cdn.contoso.com/index.html`) to verify that the result is the same as when you go directly to `<endpointname>azureedge.net/index.html`.</span></span>

![Página de inicio de la aplicación de ejemplo utilizando la dirección URL de dominio personalizado](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

<span data-ttu-id="31524-251">Para más información, consulte [Asignación del contenido de la red CDN de Azure a un dominio personalizado](../cdn/cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="31524-251">For more information, see [Map Azure CDN content to a custom domain](../cdn/cdn-map-content-to-custom-domain.md).</span></span>

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="31524-252">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="31524-252">Next steps</span></span>

<span data-ttu-id="31524-253">¿Qué ha aprendido?</span><span class="sxs-lookup"><span data-stu-id="31524-253">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="31524-254">Crear un punto de conexión de CDN.</span><span class="sxs-lookup"><span data-stu-id="31524-254">Create a CDN endpoint.</span></span>
> * <span data-ttu-id="31524-255">Actualizar los recursos en caché.</span><span class="sxs-lookup"><span data-stu-id="31524-255">Refresh cached assets.</span></span>
> * <span data-ttu-id="31524-256">Utilizar cadenas de consulta para controlar las versiones en caché.</span><span class="sxs-lookup"><span data-stu-id="31524-256">Use query strings to control cached versions.</span></span>
> * <span data-ttu-id="31524-257">Utilizar un dominio personalizado para el punto de conexión de CDN.</span><span class="sxs-lookup"><span data-stu-id="31524-257">Use a custom domain for the CDN endpoint.</span></span>

<span data-ttu-id="31524-258">Aprenda cómo optimizar el rendimiento de CDN en los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="31524-258">Learn how to optimize CDN performance in the following articles:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="31524-259">Mejora del rendimiento comprimiendo archivos en la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="31524-259">Improve performance by compressing files in Azure CDN</span></span>](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="31524-260">Carga previa de activos en un punto de conexión de CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="31524-260">Pre-load assets on an Azure CDN endpoint</span></span>](../cdn/cdn-preload-endpoint.md)
