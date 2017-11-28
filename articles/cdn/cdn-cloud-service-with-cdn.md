---
title: "Integración de un servicio en la nube de Azure con la red CDN de Azure | Microsoft Docs"
description: "Aprenda a implementar un servicio en la nube que ofrece contenido de un punto de conexión de la red CDN de Azure integrado"
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f2849fe25fd0d5b3dc26598ffba7591cb7433161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="bba23-103"><a name="intro"></a> Integración de un servicio en la nube con la Red de entrega de contenido (CDN) de Azure</span><span class="sxs-lookup"><span data-stu-id="bba23-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="bba23-104">Un servicio en la nube puede integrarse con CDN de Azure, sirviendo cualquier contenido desde la ubicación del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="bba23-104">A cloud service can be integrated with Azure CDN, serving any content from the cloud service's location.</span></span> <span data-ttu-id="bba23-105">Este enfoque le ofrece las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="bba23-105">This approach gives you the following advantages:</span></span>

* <span data-ttu-id="bba23-106">Fácil implementación y actualización de imágenes, scripts y hojas de estilo en los directorios de proyecto del servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="bba23-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="bba23-107">Actualización fácil de los paquetes NuGet en el servicio en la nube, como versiones de jQuery o Bootstrap</span><span class="sxs-lookup"><span data-stu-id="bba23-107">Easily upgrade the NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="bba23-108">Administración de la aplicación web y del contenido servido por CDN desde la misma interfaz de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bba23-108">Manage your Web application and your CDN-served content all from the same Visual Studio interface</span></span>
* <span data-ttu-id="bba23-109">Flujo de trabajo de implementación unificado para la aplicación web y el contenido servido por CDN</span><span class="sxs-lookup"><span data-stu-id="bba23-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="bba23-110">Integración de unión y minificación de ASP.NET con CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="bba23-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="bba23-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="bba23-111">What you will learn</span></span>
<span data-ttu-id="bba23-112">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="bba23-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="bba23-113">Integración de un extremo de red CDN de Azure con el servicio en la nube y suministro de contenido estático en las páginas web desde CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="bba23-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="bba23-114">Configuración de los valores de la caché para el contenido estático en el servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="bba23-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="bba23-115">Suministro de contenido de acciones de controlador a través de la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="bba23-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="bba23-116">Suministro de contenido unido y minificado a través de la red CDN de Azure preservando al mismo tiempo la experiencia de depuración de scripts en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bba23-116">Serve bundled and minified content through Azure CDN while preserving the script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="bba23-117">Configuración de la reserva de los scripts y CSS cuando la red CDN de Azure está sin conexión</span><span class="sxs-lookup"><span data-stu-id="bba23-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="bba23-118">Lo que va a crear</span><span class="sxs-lookup"><span data-stu-id="bba23-118">What you will build</span></span>
<span data-ttu-id="bba23-119">Implementaremos un rol web de servicio en la nube mediante la plantilla predeterminada ASP.NET MVC, agregaremos código para servir contenido desde una red CDN de Azure integrada, como una imagen, los resultados de las acciones de controlador y los archivos predeterminados de JavaScript y CSS, y también escribiremos código para configurar el mecanismo de reserva de los paquetes servidos en caso de desconexión de red CDN.</span><span class="sxs-lookup"><span data-stu-id="bba23-119">You will deploy a cloud service Web role using the default ASP.NET MVC template, add code to serve content from an integrated Azure CDN, such as an image, controller action results, and the default JavaScript and CSS files, and also write code to configure the fallback mechanism for bundles served in the event that the CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="bba23-120">Qué necesita</span><span class="sxs-lookup"><span data-stu-id="bba23-120">What you will need</span></span>
<span data-ttu-id="bba23-121">Este tutorial cuenta con los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="bba23-121">This tutorial has the following prerequisites:</span></span>

* <span data-ttu-id="bba23-122">Una [cuenta de Microsoft Azure activa](/account/)</span><span class="sxs-lookup"><span data-stu-id="bba23-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="bba23-123">Visual Studio 2015 con el [SDK de Azure](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="bba23-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="bba23-124">Para completar este tutorial, deberá tener una cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="bba23-124">You need an Azure account to complete this tutorial:</span></span>
> 
> * <span data-ttu-id="bba23-125">Puede [abrir una cuenta de Azure de manera gratuita](https://azure.microsoft.com/pricing/free-trial/) - Obtiene crédito que puede utilizar para probar los servicios de Azure de pago, e incluso una vez agotado este podrá mantener la cuenta y utilizar servicios gratuitos de Azure, como Sitios web.</span><span class="sxs-lookup"><span data-stu-id="bba23-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="bba23-126">Puede [activar las ventajas de suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Su suscripción a MSDN le proporciona crédito todos los meses que puede utilizar para servicios de Azure de pago.</span><span class="sxs-lookup"><span data-stu-id="bba23-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="bba23-127">un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="bba23-127">Deploy a cloud service</span></span>
<span data-ttu-id="bba23-128">En esta sección, implementará la plantilla de aplicación predeterminada ASP.NET MVC de Visual Studio 2015 en un rol web de servicio en la nube, y luego la integrará con un nuevo punto de conexión de red CDN.</span><span class="sxs-lookup"><span data-stu-id="bba23-128">In this section, you will deploy the default ASP.NET MVC application template in Visual Studio 2015 to a cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="bba23-129">Siga las instrucciones que se describen a continuación:</span><span class="sxs-lookup"><span data-stu-id="bba23-129">Follow the instructions below:</span></span>

1. <span data-ttu-id="bba23-130">En Visual Studio 2015, cree un nuevo servicio en la nube de Azure desde la barra de menús; para ello, debe ir a **Archivo > Nuevo > Proyecto > Nube > Servicio en la nube de Azure**.</span><span class="sxs-lookup"><span data-stu-id="bba23-130">In Visual Studio 2015, create a new Azure cloud service from the menu bar by going to **File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="bba23-131">Asígnele un nombre y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bba23-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="bba23-132">Seleccione **Rol web de ASP.NET** y haga clic en el botón **>**.</span><span class="sxs-lookup"><span data-stu-id="bba23-132">Select **ASP.NET Web Role** and click the **>** button.</span></span> <span data-ttu-id="bba23-133">Haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="bba23-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="bba23-134">Seleccione **MVC** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bba23-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="bba23-135">Ahora, publique este rol web en un servicio en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="bba23-135">Now, publish this Web role to an Azure cloud service.</span></span> <span data-ttu-id="bba23-136">Haga clic con el botón derecho en el proyecto del servicio en la nube y seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="bba23-136">Right-click the cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="bba23-137">Si aún no ha iniciado sesión en Microsoft Azure, haga clic en la lista desplegable **Agregar una cuenta...** y, después, en la opción de menú **Agregar una cuenta**.</span><span class="sxs-lookup"><span data-stu-id="bba23-137">If you have not yet signed into Microsoft Azure, click the **Add an account...** dropdown and click the **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="bba23-138">En la página de inicio de sesión, inicie sesión con la cuenta de Microsoft que ha usado para activar su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="bba23-138">In the sign-in page, sign in with the Microsoft account you used to activate your Azure account.</span></span>
7. <span data-ttu-id="bba23-139">Una vez que haya iniciado la sesión, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bba23-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="bba23-140">Suponiendo que no haya creado un servicio en la nube o una cuenta de almacenamiento, Visual Studio le ayudará a crear ambos.</span><span class="sxs-lookup"><span data-stu-id="bba23-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="bba23-141">En el cuadro de diálogo **Crear cuenta y servicio en la nube** , escriba el nombre de servicio deseado y seleccione la región que quiera.</span><span class="sxs-lookup"><span data-stu-id="bba23-141">In the **Create Cloud Service and Account** dialog, type the desired service name and select the desired region.</span></span> <span data-ttu-id="bba23-142">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bba23-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="bba23-143">En la página de configuración de publicación, compruebe la configuración y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="bba23-143">In the publish settings page, verify the configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="bba23-144">El proceso de publicación de los servicios en la nube tarda mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="bba23-144">The publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="bba23-145">La opción Habilitar la implementación web en todos los roles puede acelerar la depuración del servicio en la nube al proporcionar actualizaciones rápidas (pero temporales) para los roles web.</span><span class="sxs-lookup"><span data-stu-id="bba23-145">The Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates to your Web roles.</span></span> <span data-ttu-id="bba23-146">Para obtener más información sobre esta opción, consulte [Publicar un servicio en la nube mediante Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="bba23-146">For more information on this option, see [Publishing a Cloud Service using the Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="bba23-147">Cuando el **Registro de actividad de Microsoft Azure** muestre que el estado de publicación es **Completado**, creará un punto de conexión de la red CDN que se integra con este servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="bba23-147">When the **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="bba23-148">Si, tras la publicación, el servicio en la nube implementado muestra una pantalla de error, es probable que se deba a que el servicio en la nube que está usando ha implementado un [SO invitado que no incluye .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span><span class="sxs-lookup"><span data-stu-id="bba23-148">If, after publishing, the deployed cloud service displays an error screen, it's likely because the cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="bba23-149">Puede solucionar este problema mediante la [implementación de .NET 4.5.2 como tarea de inicio](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="bba23-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="bba23-150">Crear un nuevo perfil de CDN</span><span class="sxs-lookup"><span data-stu-id="bba23-150">Create a new CDN profile</span></span>
<span data-ttu-id="bba23-151">Un perfil de red de entrega de contenido es una colección de puntos de conexión de red de entrega de contenido.</span><span class="sxs-lookup"><span data-stu-id="bba23-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="bba23-152">Cada perfil contiene uno o más de estos puntos de conexión de CDN.</span><span class="sxs-lookup"><span data-stu-id="bba23-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="bba23-153">Puede que quiera usar varios perfiles para organizar sus puntos de conexión de la red CDN por dominio de Internet, aplicación web o cualquier otro criterio.</span><span class="sxs-lookup"><span data-stu-id="bba23-153">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="bba23-154">Si ya tiene un perfil de red CDN que quiere usar para este tutorial, continúe con el paso [Crear un nuevo extremo de CDN](#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="bba23-154">If you already have a CDN profile that you want to use for this tutorial, proceed to [Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="bba23-155">Crear un nuevo extremo de CDN</span><span class="sxs-lookup"><span data-stu-id="bba23-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="bba23-156">**Para crear un nuevo extremo de una red CDN para una cuenta de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="bba23-156">**To create a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="bba23-157">En el [Portal de administración de Azure](https://portal.azure.com), vaya a su perfil de CDN.</span><span class="sxs-lookup"><span data-stu-id="bba23-157">In the [Azure Management Portal](https://portal.azure.com), navigate to your CDN profile.</span></span>  <span data-ttu-id="bba23-158">Puede haberlo anclado al panel en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="bba23-158">You may have pinned it to the dashboard in the previous step.</span></span>  <span data-ttu-id="bba23-159">Si no lo hace, para encontrarlo, haga clic en **Examinar**, en **Perfiles de CDN** y, luego, haga clic en el perfil al que planea agregar el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="bba23-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span></span>
   
    <span data-ttu-id="bba23-160">Aparece la hoja del perfil de CDN.</span><span class="sxs-lookup"><span data-stu-id="bba23-160">The CDN profile blade appears.</span></span>
   
    ![Perfil de CDN][cdn-profile-settings]
2. <span data-ttu-id="bba23-162">Haga clic en el botón **Agregar extremo** .</span><span class="sxs-lookup"><span data-stu-id="bba23-162">Click the **Add Endpoint** button.</span></span>
   
    ![Botón Agregar punto de conexión][cdn-new-endpoint-button]
   
    <span data-ttu-id="bba23-164">Aparecerá la hoja **Agregar un extremo** .</span><span class="sxs-lookup"><span data-stu-id="bba23-164">The **Add an endpoint** blade appears.</span></span>
   
    ![Hoja Agregar punto de conexión][cdn-add-endpoint]
3. <span data-ttu-id="bba23-166">Escriba un **Nombre** para este punto de conexión de red de entrega de contenido.</span><span class="sxs-lookup"><span data-stu-id="bba23-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="bba23-167">Este nombre se usará para obtener acceso a sus recursos almacenados en caché en el dominio `<EndpointName>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="bba23-167">This name will be used to access your cached resources at the domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="bba23-168">En la lista desplegable **Tipo de origen** , seleccione *Servicio en la nube*.</span><span class="sxs-lookup"><span data-stu-id="bba23-168">In the **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="bba23-169">En la lista desplegable **Nombre de host de origen** , seleccione su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="bba23-169">In the **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="bba23-170">Deje los valores predeterminados de **Ruta de acceso de origen**, **Encabezado de host de origen** y **Protocolo/puerto de origen**.</span><span class="sxs-lookup"><span data-stu-id="bba23-170">Leave the defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="bba23-171">Debe especificar al menos un protocolo (HTTP o HTTPS).</span><span class="sxs-lookup"><span data-stu-id="bba23-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="bba23-172">Haga clic en el botón **Agregar** para crear el nuevo punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="bba23-172">Click the **Add** button to create the new endpoint.</span></span>
8. <span data-ttu-id="bba23-173">Una vez creado el punto de conexión, aparecerá en la lista de puntos de conexión del perfil.</span><span class="sxs-lookup"><span data-stu-id="bba23-173">Once the endpoint is created, it appears in a list of endpoints for the profile.</span></span> <span data-ttu-id="bba23-174">La visualización de la lista muestra la URL que se debe utilizar para tener acceso al contenido en caché, así como al dominio de origen.</span><span class="sxs-lookup"><span data-stu-id="bba23-174">The list view shows the URL to use to access cached content, as well as the origin domain.</span></span>
   
    ![Punto de conexión de CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="bba23-176">El punto de conexión no estará disponible inmediatamente para su uso.</span><span class="sxs-lookup"><span data-stu-id="bba23-176">The endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="bba23-177">Se pueden tardar hasta 90 minutos en que el registro se propague a través de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="bba23-177">It can take up to 90 minutes for the registration to propagate through the CDN network.</span></span> <span data-ttu-id="bba23-178">Es posible que los usuarios que intenten usar el nombre de dominio de la red CDN de forma inmediata reciban el código de estado 404 hasta que el contenido esté disponible a través de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="bba23-178">Users who try to use the CDN domain name immediately may receive status code 404 until the content is available via the CDN.</span></span>
   > 
   > 

## <a name="test-the-cdn-endpoint"></a><span data-ttu-id="bba23-179">Probar el punto de conexión de CDN</span><span class="sxs-lookup"><span data-stu-id="bba23-179">Test the CDN endpoint</span></span>
<span data-ttu-id="bba23-180">Cuando el estado de publicación sea **Completado** abra una ventana del explorador y navegue a **http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="bba23-180">When the publishing status is **Completed**, open a browser window and navigate to **http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="bba23-181">En nuestra instalación, esta URL es:</span><span class="sxs-lookup"><span data-stu-id="bba23-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="bba23-182">Esta URL corresponde a la siguiente URL de origen en el extremo de red CDN:</span><span class="sxs-lookup"><span data-stu-id="bba23-182">Which corresponds to the following origin URL at the CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="bba23-183">Cuando navegue a **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css** en función del explorador que haya usado, se le solicitará que descargue o abra el archivo bootstrap.css proveniente de la aplicación web publicada.</span><span class="sxs-lookup"><span data-stu-id="bba23-183">When you navigate to **http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted to download or open the bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="bba23-184">Puede acceder de forma parecida a cualquier dirección URL de acceso público en **http://*&lt;serviceName>*.cloudapp.net/** directamente desde el punto de conexión de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="bba23-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="bba23-185">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bba23-185">For example:</span></span>

* <span data-ttu-id="bba23-186">Un archivo .js desde la ruta /Script</span><span class="sxs-lookup"><span data-stu-id="bba23-186">A .js file from the /Script path</span></span>
* <span data-ttu-id="bba23-187">Cualquier archivo de contenido desde la ruta /Content</span><span class="sxs-lookup"><span data-stu-id="bba23-187">Any content file from the /Content path</span></span>
* <span data-ttu-id="bba23-188">Cualquier controlador/acción</span><span class="sxs-lookup"><span data-stu-id="bba23-188">Any controller/action</span></span>
* <span data-ttu-id="bba23-189">Si la cadena de consulta está habilitada en el extremo de red CDN, cualquier URL con cadenas de consulta</span><span class="sxs-lookup"><span data-stu-id="bba23-189">If the query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="bba23-190">De hecho, con la configuración anterior, es posible hospedar todo el servicio en la nube desde **http://*&lt;cdnName>*.azureedge.net/**.</span><span class="sxs-lookup"><span data-stu-id="bba23-190">In fact, with the above configuration, you can host the entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**.</span></span> <span data-ttu-id="bba23-191">Si se va a **http://camservice.azureedge.net/**, el resultado de la acción se obtiene de Home/Index.</span><span class="sxs-lookup"><span data-stu-id="bba23-191">If I navigate to **http://camservice.azureedge.net/**, I get the action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="bba23-192">Esto no significa, sin embargo, que sea siempre una buena idea suministrar un servicio en la nube entero a través de la red CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="bba23-192">This does not mean, however, that it's always a good idea to serve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="bba23-193">Una red CDN con optimización de entrega estática no acelera necesariamente la entrega de recursos dinámicos que no estén diseñados para almacenarse en caché o se actualicen con mucha frecuencia, ya que la red CDN debe extraer una nueva versión del recurso desde el servidor de origen muy a menudo.</span><span class="sxs-lookup"><span data-stu-id="bba23-193">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant to be cached, or are updated very frequently, since the CDN must pull a new version of the asset from the Origin server very often.</span></span> <span data-ttu-id="bba23-194">En este escenario, puede habilitar la optimización [Aceleración de sitios dinámicos](cdn-dynamic-site-acceleration.md) (DSA) en el punto de conexión de la red CDN que usa varias técnicas para acelerar la entrega de recursos dinámicos que no se pueden almacenar en caché.</span><span class="sxs-lookup"><span data-stu-id="bba23-194">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques to speed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="bba23-195">Si tiene un sitio con una combinación de contenido estático y dinámico, puede servir el contenido estático de la red CDN con un tipo de optimización estático (por ejemplo, entrega de web general); asimismo, puede servir el contenido dinámico directamente desde el servidor de origen, o a través de un punto de conexión de red CDN con la optimización DSA activada caso por caso.</span><span class="sxs-lookup"><span data-stu-id="bba23-195">If you have a site with a mix of static and dynamic content, you can choose to serve your static content from CDN with a static optimization type (such as general web delivery), and to serve dynamic content either directly from the origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="bba23-196">Para tal fin, ya ha visto cómo acceder a archivos de contenido individuales desde el extremo de red CDN.</span><span class="sxs-lookup"><span data-stu-id="bba23-196">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="bba23-197">Le mostraremos cómo servir una acción de controlador específica a través de un punto de conexión de red CDN específico en la sección Suministro de contenido de acciones de controlador a través de la red CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="bba23-197">I will show you how to serve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="bba23-198">La alternativa es determinar qué contenido servir desde CDN de Azure según el caso en el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="bba23-198">The alternative is to determine which content to serve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="bba23-199">Para tal fin, ya ha visto cómo acceder a archivos de contenido individuales desde el extremo de red CDN.</span><span class="sxs-lookup"><span data-stu-id="bba23-199">To that end, you have already seen how to access individual content files from the CDN endpoint.</span></span> <span data-ttu-id="bba23-200">Le mostraremos cómo servir una acción de controlador específica a través del extremo de red CDN en [Suministro de contenido de acciones de controlador a través de la red CDN de Azure](#controller).</span><span class="sxs-lookup"><span data-stu-id="bba23-200">I will show you how to serve a specific controller action through the CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="bba23-201">Configuración de las opciones de caché para los archivos estáticos del servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="bba23-201">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="bba23-202">Con la integración de la red CDN de Azure en el servicio en la nube, puede especificar cómo quiere que el contenido estático se almacene en la caché en el extremo de red CDN.</span><span class="sxs-lookup"><span data-stu-id="bba23-202">With Azure CDN integration in your cloud service, you can specify how you want static content to be cached in the CDN endpoint.</span></span> <span data-ttu-id="bba23-203">Para ello, abra *Web.config* desde su proyecto de rol web (por ejemplo, WebRole1) y agregue un elemento `<staticContent>` a `<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="bba23-203">To do this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element to `<system.webServer>`.</span></span> <span data-ttu-id="bba23-204">El XML siguiente configura la caché para que caduque en tres días.</span><span class="sxs-lookup"><span data-stu-id="bba23-204">The XML below configures the cache to expire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="bba23-205">Una vez realizado esto, todos los archivos estáticos del servicio en la nube observarán la misma regla en la caché de red CDN.</span><span class="sxs-lookup"><span data-stu-id="bba23-205">Once you do this, all static files in your cloud service will observe the same rule in your CDN cache.</span></span> <span data-ttu-id="bba23-206">Para un control más granular de la configuración de la caché, agregue un archivo *Web.config* a una carpeta y agregue ahí su configuración.</span><span class="sxs-lookup"><span data-stu-id="bba23-206">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="bba23-207">Por ejemplo, agregue un archivo *Web.config* a la carpeta *\Content* y sustituya el contenido por el siguiente XML:</span><span class="sxs-lookup"><span data-stu-id="bba23-207">For example, add a *Web.config* file to the *\Content* folder and replace the content with the following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="bba23-208">Esta configuración hace que todos los archivos estáticos de la carpeta *\Content* se almacenen en la caché durante 15 días.</span><span class="sxs-lookup"><span data-stu-id="bba23-208">This setting causes all static files from the *\Content* folder to be cached for 15 days.</span></span>

<span data-ttu-id="bba23-209">Para más información sobre cómo configurar el elemento `<clientCache>` consulte [Caché de cliente &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span><span class="sxs-lookup"><span data-stu-id="bba23-209">For more information on how to configure the `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="bba23-210">En [Suministro de contenido de acciones de controlador a través de la red CDN de Azure](#controller)también le mostraremos cómo configurar los valores de caché para los resultados de las acciones de controlador en la memoria caché de CDN.</span><span class="sxs-lookup"><span data-stu-id="bba23-210">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in the CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="bba23-211">Suministro de contenido de acciones de controlador a través de la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="bba23-211">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="bba23-212">Cuando integra un rol web de servicio en la nube con CDN de Azure, es relativamente fácil servir contenido de acciones de controlador a través de la red CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="bba23-212">When you integrate a cloud service Web role with Azure CDN, it is relatively easy to serve content from controller actions through the Azure CDN.</span></span> <span data-ttu-id="bba23-213">Además de atender el servicio en la nube directamente a través de la red CDN de Azure (como se ha mostrado anteriormente), [Maarten Balliauw](https://twitter.com/maartenballiauw) muestra cómo hacerlo con un divertido controlador MemeGenerator en [Reducing latency on the web with the Windows Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN) (Reducción de la latencia en la Web con la red CDN de Azure).</span><span class="sxs-lookup"><span data-stu-id="bba23-213">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how to do it with a fun MemeGenerator controller in [Reducing latency on the web with the Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="bba23-214">Aquí simplemente lo vamos a reproducir.</span><span class="sxs-lookup"><span data-stu-id="bba23-214">I will simply reproduce it here.</span></span>

<span data-ttu-id="bba23-215">Suponga que desea generar en su servicio en la nube memes basados en una imagen de Chuck Norris de joven (foto de [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) como esta:</span><span class="sxs-lookup"><span data-stu-id="bba23-215">Suppose in your cloud service you want to generate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="bba23-216">Tiene una acción `Index` sencilla que permite a los clientes especificar los superlativos de la imagen y que luego genera el meme una vez que publican la acción.</span><span class="sxs-lookup"><span data-stu-id="bba23-216">You have a simple `Index` action that allows the customers to specify the superlatives in the image, then generates the meme once they post to the action.</span></span> <span data-ttu-id="bba23-217">Dado que se trata de Chuck Norris, esperará que esta página se haga ampliamente popular en todo el mundo.</span><span class="sxs-lookup"><span data-stu-id="bba23-217">Since it's Chuck Norris, you would expect this page to become wildly popular globally.</span></span> <span data-ttu-id="bba23-218">Este es un buen ejemplo de servir contenido dinámico con CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="bba23-218">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="bba23-219">Siga los pasos anteriores para configurar esta acción de controlador:</span><span class="sxs-lookup"><span data-stu-id="bba23-219">Follow the steps above to setup this controller action:</span></span>

1. <span data-ttu-id="bba23-220">En la carpeta *\Controllers*, cree un nuevo archivo .cs llamado *MemeGeneratorController.cs* y sustituya el contenido por el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="bba23-220">In the *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace the content with the following code.</span></span> <span data-ttu-id="bba23-221">Asegúrese de sustituir la parte resaltada por su nombre de red CDN.</span><span class="sxs-lookup"><span data-stu-id="bba23-221">Be sure to replace the highlighted portion with your CDN name.</span></span>  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve the debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. <span data-ttu-id="bba23-222">Haga clic con el botón derecho en la acción `Index()` predeterminada y seleccione **Agregar vista**.</span><span class="sxs-lookup"><span data-stu-id="bba23-222">Right-click in the default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="bba23-223">Acepte la configuración que se indica a continuación y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="bba23-223">Accept the settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="bba23-224">Abra el nuevo archivo *Views\MemeGenerator\Index.cshtml* y sustituya el contenido por el siguiente HTML simple para enviar los superlativos:</span><span class="sxs-lookup"><span data-stu-id="bba23-224">Open the new *Views\MemeGenerator\Index.cshtml* and replace the content with the following simple HTML for submitting the superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="bba23-225">Vuelva a publicar el servicio en la nube y navegue a **http://*&lt;nombreServicio>*.cloudapp.net/MemeGenerator/Index** en el explorador.</span><span class="sxs-lookup"><span data-stu-id="bba23-225">Publish the cloud service again and navigate to **http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="bba23-226">Cuando envía los valores de formulario a `/MemeGenerator/Index`, el método de acción `Index_Post` devuelve un vínculo al método de acción `Show` con el identificador de entrada respectivo.</span><span class="sxs-lookup"><span data-stu-id="bba23-226">When you submit the form values to `/MemeGenerator/Index`, the `Index_Post` action method returns a link to the `Show` action method with the respective input identifier.</span></span> <span data-ttu-id="bba23-227">Cuando hace clic en el vínculo, llega al siguiente código:</span><span class="sxs-lookup"><span data-stu-id="bba23-227">When you click the link, you reach the following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve the debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="bba23-228">Si su depurador local está conectado, obtendrá la experiencia de depuración normal con una redirección local.</span><span class="sxs-lookup"><span data-stu-id="bba23-228">If your local debugger is attached, then you will get the regular debug experience with a local redirect.</span></span> <span data-ttu-id="bba23-229">Si se está ejecutando en el servicio en la nube, realizará la redirección a:</span><span class="sxs-lookup"><span data-stu-id="bba23-229">If it's running in the cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="bba23-230">Que corresponde a la siguiente URL de origen en el extremo de red CDN:</span><span class="sxs-lookup"><span data-stu-id="bba23-230">Which corresponds to the following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="bba23-231">Luego puede usar el atributo `OutputCacheAttribute` en el método `Generate` para especificar cómo se debería almacenar en caché el resultado de la acción, que atenderá CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="bba23-231">You can then use the `OutputCacheAttribute` attribute on the `Generate` method to specify how the action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="bba23-232">El siguiente código especifica una caducidad de la caché de una hora (3.600 segundos).</span><span class="sxs-lookup"><span data-stu-id="bba23-232">The code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="bba23-233">Igualmente, puede servir contenido de cualquier acción de controlador del servicio en la nube a través de su CDN de Azure, con la opción de almacenamiento en caché deseada.</span><span class="sxs-lookup"><span data-stu-id="bba23-233">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with the desired caching option.</span></span>

<span data-ttu-id="bba23-234">En la siguiente sección, le mostraremos cómo servir los scripts y CSS unidos y minificados a través de la red CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="bba23-234">In the next section, I will show you how to serve the bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="bba23-235">Integración de unión y minificación de ASP.NET con CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="bba23-235">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="bba23-236">Los scripts y las hojas de estilo CSS cambian con poca frecuencia y son los principales candidatos para la caché de red CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="bba23-236">Scripts and CSS stylesheets change infrequently and are prime candidates for the Azure CDN cache.</span></span> <span data-ttu-id="bba23-237">Prestar servicio al rol web entero a través de la red CDN de Azure es la manera más fácil de integrar unión y minificación con CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="bba23-237">Serving the entire Web role through your Azure CDN is the easiest way to integrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="bba23-238">Sin embargo, como es posible que no quiera hacer esto, le mostraremos cómo hacerlo conservando la experiencia deseada del desarrollador en unión y minificación de ASP.NET, como:</span><span class="sxs-lookup"><span data-stu-id="bba23-238">However, as you may not want to do this, I will show you how to do it while preserving the desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="bba23-239">Gran experiencia en el modo de depuración</span><span class="sxs-lookup"><span data-stu-id="bba23-239">Great debug mode experience</span></span>
* <span data-ttu-id="bba23-240">Implementación optimizada</span><span class="sxs-lookup"><span data-stu-id="bba23-240">Streamlined deployment</span></span>
* <span data-ttu-id="bba23-241">Actualizaciones inmediatas a clientes de actualizaciones de versión de script/CSS</span><span class="sxs-lookup"><span data-stu-id="bba23-241">Immediate updates to clients for script/CSS version upgrades</span></span>
* <span data-ttu-id="bba23-242">Mecanismo de reserva cuando el extremo de red CDN falla</span><span class="sxs-lookup"><span data-stu-id="bba23-242">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="bba23-243">Menor modificación del código</span><span class="sxs-lookup"><span data-stu-id="bba23-243">Minimize code modification</span></span>

<span data-ttu-id="bba23-244">En el proyecto **WebRole1** que creó en [Integración de un servicio en la nube con la Red de entrega de contenido (CDN) de Azure](#deploy), abra *App_Start\BundleConfig.cs* y examine las llamadas del método `bundles.Add()`.</span><span class="sxs-lookup"><span data-stu-id="bba23-244">In the **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at the `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="bba23-245">La primera instrucción `bundles.Add()` agrega un paquete de scripts en el directorio virtual `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="bba23-245">The first `bundles.Add()` statement adds a script bundle at the virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="bba23-246">A continuación, abra *Views\Shared\_Layout.cshtml* para ver cómo se procesa la etiqueta del paquete de scripts.</span><span class="sxs-lookup"><span data-stu-id="bba23-246">Then, open *Views\Shared\_Layout.cshtml* to see how the script bundle tag is rendered.</span></span> <span data-ttu-id="bba23-247">Encontrará la siguiente línea de código Razor:</span><span class="sxs-lookup"><span data-stu-id="bba23-247">You should be able to find the following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="bba23-248">Cuando este código Razor se ejecute en el rol web de Azure, procesará una etiqueta `<script>` para el paquete de scripts similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="bba23-248">When this Razor code is run in the Azure Web role, it will render a `<script>` tag for the script bundle similar to the following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="bba23-249">Sin embargo, cuando se ejecute en Visual Studio mediante `F5`, procesará cada archivo de script del paquete de forma individual (en el caso anterior, solo hay un archivo de script en el paquete):</span><span class="sxs-lookup"><span data-stu-id="bba23-249">However, when it is run in Visual Studio by typing `F5`, it will render each script file in the bundle individually (in the case above, only one script file is in the bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="bba23-250">Esto permite depurar el código JavaScript de su entorno de desarrollo y, al mismo tiempo, reducir las conexiones cliente simultáneas (unión) y mejorar el rendimiento de la descarga de archivos (minificación) en producción.</span><span class="sxs-lookup"><span data-stu-id="bba23-250">This enables you to debug the JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="bba23-251">Es una excelente característica para preservar con la integración de red CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="bba23-251">It's a great feature to preserve with Azure CDN integration.</span></span> <span data-ttu-id="bba23-252">Además, como el paquete procesado ya contiene una cadena de versión generada automáticamente, querrá replicar esa funcionalidad para que cada vez que actualice su versión de jQuery a través de NuGet, se pueda actualizar en el cliente lo antes posible.</span><span class="sxs-lookup"><span data-stu-id="bba23-252">Furthermore, since the rendered bundle already contains an automatically generated version string, you want to replicate that functionality so the whenever you update your jQuery version through NuGet, it can be updated at the client side as soon as possible.</span></span>

<span data-ttu-id="bba23-253">Siga estos pasos para la integración de la unión y minificación de ASP.NET con el extremo de red CDN.</span><span class="sxs-lookup"><span data-stu-id="bba23-253">Follow the steps below to integration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="bba23-254">De vuelta en *App_Start\BundleConfig.cs*, modifique los métodos `bundles.Add()` para usar un [constructor de paquetes](http://msdn.microsoft.com/library/jj646464.aspx) diferente, uno que especifique una dirección de CDN.</span><span class="sxs-lookup"><span data-stu-id="bba23-254">Back in *App_Start\BundleConfig.cs*, modify the `bundles.Add()` methods to use a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="bba23-255">Para ello, reemplace la definición del método `RegisterBundles` por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="bba23-255">To do this, replace the `RegisterBundles` method definition with the following code:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you're
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="bba23-256">Asegúrese de sustituir `<yourCDNName>` por el nombre de su CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="bba23-256">Be sure to replace `<yourCDNName>` with the name of your Azure CDN.</span></span>
   
    <span data-ttu-id="bba23-257">En otras palabras, ha configurado `bundles.UseCdn = true` y agregado una dirección URL de red CDN diseñada especialmente para cada paquete.</span><span class="sxs-lookup"><span data-stu-id="bba23-257">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL to each bundle.</span></span> <span data-ttu-id="bba23-258">Por ejemplo, el primer constructor del código:</span><span class="sxs-lookup"><span data-stu-id="bba23-258">For example, the first constructor in the code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="bba23-259">es igual que:</span><span class="sxs-lookup"><span data-stu-id="bba23-259">is the same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="bba23-260">Este constructor indica que en la unión y minificación de ASP.NET se procesen archivos de script individuales cuando se depuren localmente, pero que se use la dirección de red CDN especificada para acceder al script en cuestión.</span><span class="sxs-lookup"><span data-stu-id="bba23-260">This constructor tells ASP.NET bundling and minification to render individual script files when debugged locally, but use the specified CDN address to access the script in question.</span></span> <span data-ttu-id="bba23-261">Sin embargo, observe dos características importantes con esta URL de red CDN diseñada especialmente:</span><span class="sxs-lookup"><span data-stu-id="bba23-261">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="bba23-262">El origen de esta URL de red CDN es `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, que es realmente el directorio virtual del paquete de scripts en su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="bba23-262">The origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually the virtual directory of the script bundle in your cloud service.</span></span>
   * <span data-ttu-id="bba23-263">Como está usando el constructor de red CDN, la etiqueta de script de red CDN del paquete ya no contiene la cadena de versión generada automáticamente en la URL procesada.</span><span class="sxs-lookup"><span data-stu-id="bba23-263">Since you are using CDN constructor, the CDN script tag for the bundle no longer contains the automatically generated version string in the rendered URL.</span></span> <span data-ttu-id="bba23-264">Debe generar manualmente una cadena de versión única cada vez que se modifique el paquete de scripts con el fin de forzar un error de caché en la red CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="bba23-264">You must manually generate a unique version string every time the script bundle is modified to force a cache miss at your Azure CDN.</span></span> <span data-ttu-id="bba23-265">Al mismo tiempo, esta cadena de versión única debe permanecer constante lo que dure la implementación para aumentar los aciertos de la caché en la red CDN de Azure después de implementarse el paquete.</span><span class="sxs-lookup"><span data-stu-id="bba23-265">At the same time, this unique version string must remain constant through the life of the deployment to maximize cache hits at your Azure CDN after the bundle is deployed.</span></span>
   * <span data-ttu-id="bba23-266">La cadena de consulta v=<W.X.Y.Z> se extrae de *Properties\AssemblyInfo.cs* en el proyecto de rol web.</span><span class="sxs-lookup"><span data-stu-id="bba23-266">The query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="bba23-267">Puede tener un flujo de trabajo de implementación que incluya incrementar la versión de ensamblado cada vez que publica en Azure.</span><span class="sxs-lookup"><span data-stu-id="bba23-267">You can have a deployment workflow that includes incrementing the assembly version every time you publish to Azure.</span></span> <span data-ttu-id="bba23-268">O bien, puede modificar *Properties\AssemblyInfo.cs* en su proyecto para incrementar automáticamente la cadena de versión cada vez que compila, mediante el carácter comodín '*'.</span><span class="sxs-lookup"><span data-stu-id="bba23-268">Or, you can just modify *Properties\AssemblyInfo.cs* in your project to automatically increment the version string every time you build, using the wildcard character '*'.</span></span> <span data-ttu-id="bba23-269">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bba23-269">For example:</span></span>
     
        <span data-ttu-id="bba23-270">[assembly: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="bba23-270">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="bba23-271">Cualquier otra estrategia para optimizar la generación de una cadena única durante una implementación funcionará aquí.</span><span class="sxs-lookup"><span data-stu-id="bba23-271">Any other strategy to streamline generating a unique string for the life of a deployment will work here.</span></span>
2. <span data-ttu-id="bba23-272">Vuelva a publicar el servicio en la nube y acceda a la página principal.</span><span class="sxs-lookup"><span data-stu-id="bba23-272">Republish the cloud service and access the home page.</span></span>
3. <span data-ttu-id="bba23-273">Vea el código HTML de la página.</span><span class="sxs-lookup"><span data-stu-id="bba23-273">View the HTML code for the page.</span></span> <span data-ttu-id="bba23-274">Debería poder ver la URL de red CDN procesada, con una cadena de versión única cada vez que vuelve a publicar los cambios en el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="bba23-274">You should be able to see the CDN URL rendered, with a unique version string every time you republish changes to your cloud service.</span></span> <span data-ttu-id="bba23-275">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bba23-275">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="bba23-276">En Visual Studio, depure el servicio en la nube con `F5`.</span><span class="sxs-lookup"><span data-stu-id="bba23-276">In Visual Studio, debug the cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="bba23-277">Vea el código HTML de la página.</span><span class="sxs-lookup"><span data-stu-id="bba23-277">View the HTML code for the page.</span></span> <span data-ttu-id="bba23-278">Aún verá cada archivo de script procesado de forma individual para que pueda tener una experiencia de depuración coherente en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bba23-278">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="bba23-279">Mecanismo de reserva para URL de red CDN</span><span class="sxs-lookup"><span data-stu-id="bba23-279">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="bba23-280">Cuando el extremo de red CDN de Azure no funcione por cualquier motivo, querrá que su página web sea lo bastante inteligente como para acceder al servidor web de origen como opción de reserva para cargar JavaScript o Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="bba23-280">When your Azure CDN endpoint fails for any reason, you want your Web page to be smart enough to access your origin Web server as the fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="bba23-281">Es grave perder imágenes en su sitio web debido a la falta de disponibilidad de la red CDN, pero aún es más grave perder la funcionalidad esencial de página que proporcionan sus scripts y hojas de estilos.</span><span class="sxs-lookup"><span data-stu-id="bba23-281">It's serious enough to lose images on your website due to CDN unavailability, but much more severe to lose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="bba23-282">La clase [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) contiene una propiedad llamada [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) que le permite configurar el mecanismo de reserva en caso de error de red CDN.</span><span class="sxs-lookup"><span data-stu-id="bba23-282">The [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you to configure the fallback mechanism for CDN failure.</span></span> <span data-ttu-id="bba23-283">Para usar esta propiedad, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="bba23-283">To use this property, follow the steps below:</span></span>

1. <span data-ttu-id="bba23-284">En el proyecto de rol web, abra *App_Start\BundleConfig.cs*, donde agregó una dirección URL de CDN en cada [constructor de agrupaciones](http://msdn.microsoft.com/library/jj646464.aspx), y realice los siguientes cambios que se resaltan para agregar un mecanismo de reserva a las agrupaciones predeterminadas:</span><span class="sxs-lookup"><span data-stu-id="bba23-284">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make the following highlighted changes to add fallback mechanism to the default bundles:</span></span>  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
            // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="bba23-285">Cuando `CdnFallbackExpression` no tiene un valor null, el script se inserta en el código HTML para probar si el paquete está cargado correctamente y, en caso contrario, obtener acceso al paquete directamente desde el servidor web de origen.</span><span class="sxs-lookup"><span data-stu-id="bba23-285">When `CdnFallbackExpression` is not null, script is injected into the HTML to test whether the bundle is loaded successfully and, if not, access the bundle directly from the origin Web server.</span></span> <span data-ttu-id="bba23-286">Esta propiedad se debe configurar como una expresión de JavaScript que prueba si el paquete de red CDN respectivo se ha cargado correctamente.</span><span class="sxs-lookup"><span data-stu-id="bba23-286">This property needs to be set to a JavaScript expression that tests whether the respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="bba23-287">La expresión necesaria para probar cada paquete es diferente según el contenido.</span><span class="sxs-lookup"><span data-stu-id="bba23-287">The expression needed to test each bundle differs according to the content.</span></span> <span data-ttu-id="bba23-288">En el caso de los paquetes predeterminados anteriores:</span><span class="sxs-lookup"><span data-stu-id="bba23-288">For the default bundles above:</span></span>
   
   * <span data-ttu-id="bba23-289">`window.jquery` se define en jquery-{version}.js</span><span class="sxs-lookup"><span data-stu-id="bba23-289">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="bba23-290">`$.validator` se define en jquery.validate.js</span><span class="sxs-lookup"><span data-stu-id="bba23-290">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="bba23-291">`window.Modernizr` se define en modernizer-{version}.js</span><span class="sxs-lookup"><span data-stu-id="bba23-291">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="bba23-292">`$.fn.modal` se define en bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="bba23-292">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="bba23-293">Habrá observado que no hemos configurado CdnFallbackExpression para el paquete `~/Cointent/css` .</span><span class="sxs-lookup"><span data-stu-id="bba23-293">You might have noticed that I did not set CdnFallbackExpression for the `~/Cointent/css` bundle.</span></span> <span data-ttu-id="bba23-294">El motivo es que actualmente hay un [error en System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) que inyecta una etiqueta `<script>` para la CSS de reserva en lugar de la etiqueta `<link>` esperada.</span><span class="sxs-lookup"><span data-stu-id="bba23-294">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for the fallback CSS instead of the expected `<link>` tag.</span></span>
     
     <span data-ttu-id="bba23-295">Sin embargo, existe una buena [solución de reserva de paquetes de estilo](https://github.com/EmberConsultingGroup/StyleBundleFallback) que ofrece [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="bba23-295">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="bba23-296">Para usar la solución alternativa para CSS, cree un nuevo archivo .cs en la carpeta *App_Start* del proyecto de rol web llamado *StyleBundleExtensions.cs* y reemplace su contenido por el [código de GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="bba23-296">To use the workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with the [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="bba23-297">En *App_Start\StyleFundleExtensions.cs*, cambie el nombre del espacio de nombres por el nombre del rol web (por ejemplo, **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="bba23-297">In *App_Start\StyleFundleExtensions.cs*, rename the namespace to your Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="bba23-298">Vuelva a `App_Start\BundleConfig.cs` y modifique la última instrucción `bundles.Add` con el siguiente código resaltado:</span><span class="sxs-lookup"><span data-stu-id="bba23-298">Go back to `App_Start\BundleConfig.cs` and modify the last `bundles.Add` statement with the following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="bba23-299">Este nuevo método de extensión usa la misma idea para inyectar el script en el código HTML a fin de comprobar si hay una coincidencia en el DOM para un nombre de clase, nombre de regla o valor de regla definidos en el paquete de CSS y, en caso de no encontrarla, recurre al servidor web de origen.</span><span class="sxs-lookup"><span data-stu-id="bba23-299">This new extension method uses the same idea to inject script in the HTML to check the DOM for the a matching class name, rule name, and rule value defined in the CSS bundle, and falls back to the origin Web server if it fails to find the match.</span></span>
5. <span data-ttu-id="bba23-300">Publicar el servicio en la nube y acceda a la página principal.</span><span class="sxs-lookup"><span data-stu-id="bba23-300">Publish the cloud service again and access the home page.</span></span>
6. <span data-ttu-id="bba23-301">Vea el código HTML de la página.</span><span class="sxs-lookup"><span data-stu-id="bba23-301">View the HTML code for the page.</span></span> <span data-ttu-id="bba23-302">Debería encontrar scripts inyectados simulares a los siguientes:</span><span class="sxs-lookup"><span data-stu-id="bba23-302">You should find injected scripts similar to the following:</span></span>    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    <span data-ttu-id="bba23-303">Observe que el script inyectado para el paquete de CSS contiene aún el residuo errante de la propiedad `CdnFallbackExpression` en la línea:</span><span class="sxs-lookup"><span data-stu-id="bba23-303">Note that injected script for the CSS bundle still contains the errant remnant from the `CdnFallbackExpression` property in the line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="bba23-304">Pero como la primera parte de la expresión || siempre devolverá true (en la línea directamente encima de esa), la función document.write() nunca se ejecutará.</span><span class="sxs-lookup"><span data-stu-id="bba23-304">But since the first part of the || expression will always return true (in the line directly above that), the document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="bba23-305">Más información</span><span class="sxs-lookup"><span data-stu-id="bba23-305">More Information</span></span>
* [<span data-ttu-id="bba23-306">Información general de la red de entrega de contenido (CDN) de Azure</span><span class="sxs-lookup"><span data-stu-id="bba23-306">Overview of the Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="bba23-307">Uso de CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="bba23-307">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="bba23-308">Unión y minificación de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="bba23-308">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
