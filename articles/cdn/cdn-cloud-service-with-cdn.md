---
title: aaaIntegrate un servicio de nube de Azure con red CDN de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodeploy un servicio de nube sirve contenido desde un punto de conexión de red CDN de Azure integrada"
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
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="3790d-103"><a name="intro"></a> Integración de un servicio en la nube con la Red de entrega de contenido (CDN) de Azure</span><span class="sxs-lookup"><span data-stu-id="3790d-103"><a name="intro"></a> Integrate a cloud service with Azure CDN</span></span>
<span data-ttu-id="3790d-104">Un servicio de nube puede integrarse con CDN de Azure, que sirve al contenido de la ubicación del servicio de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-104">A cloud service can be integrated with Azure CDN, serving any content from hello cloud service's location.</span></span> <span data-ttu-id="3790d-105">Esto deja de enfoque Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="3790d-105">This approach gives you hello following advantages:</span></span>

* <span data-ttu-id="3790d-106">Fácil implementación y actualización de imágenes, scripts y hojas de estilo en los directorios de proyecto del servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="3790d-106">Easily deploy and update images, scripts, and stylesheets in your cloud service's project directories</span></span>
* <span data-ttu-id="3790d-107">Actualizar fácilmente los paquetes de NuGet de hello en el servicio de nube, por ejemplo, jQuery o versiones de arranque</span><span class="sxs-lookup"><span data-stu-id="3790d-107">Easily upgrade hello NuGet packages in your cloud service, such as jQuery or Bootstrap versions</span></span>
* <span data-ttu-id="3790d-108">Administrar la aplicación Web y la red CDN en ser atendido contenido todas de hello misma interfaz de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3790d-108">Manage your Web application and your CDN-served content all from hello same Visual Studio interface</span></span>
* <span data-ttu-id="3790d-109">Flujo de trabajo de implementación unificado para la aplicación web y el contenido servido por CDN</span><span class="sxs-lookup"><span data-stu-id="3790d-109">Unified deployment workflow for your Web application and your CDN-served content</span></span>
* <span data-ttu-id="3790d-110">Integración de unión y minificación de ASP.NET con CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="3790d-110">Integrate ASP.NET bundling and minification with Azure CDN</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3790d-111">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="3790d-111">What you will learn</span></span>
<span data-ttu-id="3790d-112">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="3790d-112">In this tutorial, you will learn how to:</span></span>

* [<span data-ttu-id="3790d-113">Integración de un extremo de red CDN de Azure con el servicio en la nube y suministro de contenido estático en las páginas web desde CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="3790d-113">Integrate an Azure CDN endpoint with your cloud service and serve static content in your Web pages from Azure CDN</span></span>](#deploy)
* [<span data-ttu-id="3790d-114">Configuración de los valores de la caché para el contenido estático en el servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="3790d-114">Configure cache settings for static content in your cloud service</span></span>](#caching)
* [<span data-ttu-id="3790d-115">Suministro de contenido de acciones de controlador a través de la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="3790d-115">Serve content from controller actions through Azure CDN</span></span>](#controller)
* [<span data-ttu-id="3790d-116">Servir empaquetan y reduce el contenido a través de la red CDN de Azure conservando la experiencia en Visual Studio de depuración de script de Hola</span><span class="sxs-lookup"><span data-stu-id="3790d-116">Serve bundled and minified content through Azure CDN while preserving hello script debugging experience in Visual Studio</span></span>](#bundling)
* [<span data-ttu-id="3790d-117">Configuración de la reserva de los scripts y CSS cuando la red CDN de Azure está sin conexión</span><span class="sxs-lookup"><span data-stu-id="3790d-117">Configure fallback your scripts and CSS when your Azure CDN is offline</span></span>](#fallback)

## <a name="what-you-will-build"></a><span data-ttu-id="3790d-118">Lo que va a crear</span><span class="sxs-lookup"><span data-stu-id="3790d-118">What you will build</span></span>
<span data-ttu-id="3790d-119">Implementar un rol de Web de servicio de nube mediante predeterminado Hola plantilla de ASP.NET MVC, agregará contenido de tooserve de código de una CDN de Azure integrada, como una imagen, los resultados de acción de controlador y archivos de JavaScript y CSS de predeterminados hello y también escribir hello tooconfigure de código mecanismo de reserva para agrupaciones atendido en caso de hello ese CDN Hola está sin conexión.</span><span class="sxs-lookup"><span data-stu-id="3790d-119">You will deploy a cloud service Web role using hello default ASP.NET MVC template, add code tooserve content from an integrated Azure CDN, such as an image, controller action results, and hello default JavaScript and CSS files, and also write code tooconfigure hello fallback mechanism for bundles served in hello event that hello CDN is offline.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="3790d-120">Qué necesita</span><span class="sxs-lookup"><span data-stu-id="3790d-120">What you will need</span></span>
<span data-ttu-id="3790d-121">Este tutorial tiene Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="3790d-121">This tutorial has hello following prerequisites:</span></span>

* <span data-ttu-id="3790d-122">Una [cuenta de Microsoft Azure activa](/account/)</span><span class="sxs-lookup"><span data-stu-id="3790d-122">An active [Microsoft Azure account](/account/)</span></span>
* <span data-ttu-id="3790d-123">Visual Studio 2015 con el [SDK de Azure](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="3790d-123">Visual Studio 2015 with [Azure SDK](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)</span></span>

> [!NOTE]
> <span data-ttu-id="3790d-124">Necesita una cuenta de Azure toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="3790d-124">You need an Azure account toocomplete this tutorial:</span></span>
> 
> * <span data-ttu-id="3790d-125">También puede [abrir una cuenta de Azure de forma gratuita](https://azure.microsoft.com/pricing/free-trial/) -obtendrá créditos puede usar tootry los servicios de Azure de pago e incluso después de que se utilizan hasta puede mantener la cuenta de hello y libre de usar servicios de Azure, como sitios Web.</span><span class="sxs-lookup"><span data-stu-id="3790d-125">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use tootry out paid Azure services, and even after they're used up you can keep hello account and use free Azure services, such as Websites.</span></span>
> * <span data-ttu-id="3790d-126">Puede [activar las ventajas de suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Su suscripción a MSDN le proporciona crédito todos los meses que puede utilizar para servicios de Azure de pago.</span><span class="sxs-lookup"><span data-stu-id="3790d-126">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a><span data-ttu-id="3790d-127">un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="3790d-127">Deploy a cloud service</span></span>
<span data-ttu-id="3790d-128">En esta sección, se implementar predeterminado Hola plantilla de aplicación de ASP.NET MVC en Visual Studio 2015 tooa rol de Web de servicio de nube y, a continuación, se integre con un nuevo extremo de red CDN.</span><span class="sxs-lookup"><span data-stu-id="3790d-128">In this section, you will deploy hello default ASP.NET MVC application template in Visual Studio 2015 tooa cloud service Web role, and then integrate it with a new CDN endpoint.</span></span> <span data-ttu-id="3790d-129">Siga estas instrucciones hello:</span><span class="sxs-lookup"><span data-stu-id="3790d-129">Follow hello instructions below:</span></span>

1. <span data-ttu-id="3790d-130">En Visual Studio 2015, crear un nuevo servicio de nube de Azure desde la barra de menús de hello yendo demasiado**archivo > Nuevo > proyecto > nube > servicio de nube de Azure**.</span><span class="sxs-lookup"><span data-stu-id="3790d-130">In Visual Studio 2015, create a new Azure cloud service from hello menu bar by going too**File > New > Project > Cloud > Azure Cloud Service**.</span></span> <span data-ttu-id="3790d-131">Asígnele un nombre y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3790d-131">Give it a name and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. <span data-ttu-id="3790d-132">Seleccione **rol Web de ASP.NET** y haga clic en hello  **>**  botón.</span><span class="sxs-lookup"><span data-stu-id="3790d-132">Select **ASP.NET Web Role** and click hello **>** button.</span></span> <span data-ttu-id="3790d-133">Haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="3790d-133">Click OK.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. <span data-ttu-id="3790d-134">Seleccione **MVC** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3790d-134">Select **MVC** and click **OK**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. <span data-ttu-id="3790d-135">Ahora, publicar este tooan de rol Web servicio de nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="3790d-135">Now, publish this Web role tooan Azure cloud service.</span></span> <span data-ttu-id="3790d-136">Haga clic en proyecto de servicio de nube de Hola y seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="3790d-136">Right-click hello cloud service project and select **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. <span data-ttu-id="3790d-137">Si todavía no se ha suscrito a Microsoft Azure, haga clic en hello **agregar una cuenta...**  Hola de lista desplegable y haga clic en **agregar una cuenta** elemento de menú.</span><span class="sxs-lookup"><span data-stu-id="3790d-137">If you have not yet signed into Microsoft Azure, click hello **Add an account...** dropdown and click hello **Add an account** menu item.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. <span data-ttu-id="3790d-138">En la página de inicio de sesión hello, inicie sesión con hello cuenta de Microsoft que usó tooactivate su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="3790d-138">In hello sign-in page, sign in with hello Microsoft account you used tooactivate your Azure account.</span></span>
7. <span data-ttu-id="3790d-139">Una vez que haya iniciado la sesión, haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="3790d-139">Once you're signed in, click **Next**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. <span data-ttu-id="3790d-140">Suponiendo que no haya creado un servicio en la nube o una cuenta de almacenamiento, Visual Studio le ayudará a crear ambos.</span><span class="sxs-lookup"><span data-stu-id="3790d-140">Assuming that you haven't created a cloud service or storage account, Visual Studio will help you create both.</span></span> <span data-ttu-id="3790d-141">Hola **crear servicio en la nube y cuenta** cuadro de diálogo, nombre de servicio que desee de tipo hello y región deseada Hola select.</span><span class="sxs-lookup"><span data-stu-id="3790d-141">In hello **Create Cloud Service and Account** dialog, type hello desired service name and select hello desired region.</span></span> <span data-ttu-id="3790d-142">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3790d-142">Then, click **Create**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. <span data-ttu-id="3790d-143">Hola, página de configuración de publicación, comprobar la configuración de Hola y haga clic en **publicar**.</span><span class="sxs-lookup"><span data-stu-id="3790d-143">In hello publish settings page, verify hello configuration and click **Publish**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > <span data-ttu-id="3790d-144">proceso de publicación de Hola para servicios en la nube tarda mucho tiempo.</span><span class="sxs-lookup"><span data-stu-id="3790d-144">hello publishing process for cloud services takes a long time.</span></span> <span data-ttu-id="3790d-145">Hola habilitar Web Deploy para la opción de todos los roles puede dificultar la depuración de servicio en la nube mucho más rápido proporcionando actualizaciones rápido (aunque temporal) tooyour roles Web.</span><span class="sxs-lookup"><span data-stu-id="3790d-145">hello Enable Web Deploy for all roles option can make debugging your cloud service much quicker by providing fast (but temporary) updates tooyour Web roles.</span></span> <span data-ttu-id="3790d-146">Para obtener más información sobre esta opción, vea [publicar un servicio de nube mediante herramientas de Azure de hello](http://msdn.microsoft.com/library/ff683672.aspx).</span><span class="sxs-lookup"><span data-stu-id="3790d-146">For more information on this option, see [Publishing a Cloud Service using hello Azure Tools](http://msdn.microsoft.com/library/ff683672.aspx).</span></span>
   > 
   > 
   
    <span data-ttu-id="3790d-147">Cuando Hola **Microsoft Azure Activity Log** muestra que el estado de publicación es **completado**, creará un punto de conexión de red CDN que se integra con este servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="3790d-147">When hello **Microsoft Azure Activity Log** shows that publishing status is **Completed**, you will create a CDN endpoint that's integrated with this cloud service.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="3790d-148">Si, después de publicarlo, servicio de nube de hello implementado muestra una pantalla de error, es probable porque está usando el servicio de nube de Hola que ha implementado un [invitado SO que no incluye .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span><span class="sxs-lookup"><span data-stu-id="3790d-148">If, after publishing, hello deployed cloud service displays an error screen, it's likely because hello cloud service you've deployed is using a [guest OS that does not include .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).</span></span>  <span data-ttu-id="3790d-149">Puede solucionar este problema mediante la [implementación de .NET 4.5.2 como tarea de inicio](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="3790d-149">You can work around this issue by [deploying .NET 4.5.2 as a startup task](../cloud-services/cloud-services-dotnet-install-dotnet.md).</span></span>
   > 
   > 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="3790d-150">Crear un nuevo perfil de CDN</span><span class="sxs-lookup"><span data-stu-id="3790d-150">Create a new CDN profile</span></span>
<span data-ttu-id="3790d-151">Un perfil de red de entrega de contenido es una colección de puntos de conexión de red de entrega de contenido.</span><span class="sxs-lookup"><span data-stu-id="3790d-151">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="3790d-152">Cada perfil contiene uno o más de estos puntos de conexión de CDN.</span><span class="sxs-lookup"><span data-stu-id="3790d-152">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="3790d-153">Puede ser conveniente toouse varios tooorganize perfiles los extremos de red CDN el dominio de internet, las aplicaciones web u otros criterios.</span><span class="sxs-lookup"><span data-stu-id="3790d-153">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!TIP]
> <span data-ttu-id="3790d-154">Si ya tiene un perfil de CDN que desea toouse para este tutorial, continúe demasiado[crear un nuevo extremo CDN](#create-a-new-cdn-endpoint).</span><span class="sxs-lookup"><span data-stu-id="3790d-154">If you already have a CDN profile that you want toouse for this tutorial, proceed too[Create a new CDN endpoint](#create-a-new-cdn-endpoint).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="3790d-155">Crear un nuevo extremo de CDN</span><span class="sxs-lookup"><span data-stu-id="3790d-155">Create a new CDN endpoint</span></span>
<span data-ttu-id="3790d-156">**toocreate un nuevo extremo de red CDN para la cuenta de almacenamiento**</span><span class="sxs-lookup"><span data-stu-id="3790d-156">**toocreate a new CDN endpoint for your storage account**</span></span>

1. <span data-ttu-id="3790d-157">Hola [Portal de administración de Azure](https://portal.azure.com), navegar por el perfil de CDN tooyour.</span><span class="sxs-lookup"><span data-stu-id="3790d-157">In hello [Azure Management Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="3790d-158">Puede haber anclarlo toohello panel en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-158">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="3790d-159">Si no es así, se encontrará, haciendo clic en **examinar**, a continuación, **perfiles de red CDN**, y haga clic en el perfil de hello tiene previsto tooadd del extremo que.</span><span class="sxs-lookup"><span data-stu-id="3790d-159">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="3790d-160">aparece la hoja de perfil CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-160">hello CDN profile blade appears.</span></span>
   
    ![Perfil de CDN][cdn-profile-settings]
2. <span data-ttu-id="3790d-162">Haga clic en hello **Agregar extremo** botón.</span><span class="sxs-lookup"><span data-stu-id="3790d-162">Click hello **Add Endpoint** button.</span></span>
   
    ![Botón Agregar punto de conexión][cdn-new-endpoint-button]
   
    <span data-ttu-id="3790d-164">Hola **agregar un punto de conexión** aparece hoja.</span><span class="sxs-lookup"><span data-stu-id="3790d-164">hello **Add an endpoint** blade appears.</span></span>
   
    ![Hoja Agregar punto de conexión][cdn-add-endpoint]
3. <span data-ttu-id="3790d-166">Escriba un **Nombre** para este punto de conexión de red de entrega de contenido.</span><span class="sxs-lookup"><span data-stu-id="3790d-166">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="3790d-167">Este nombre será tooaccess usa los recursos almacenados en caché en el dominio de hello `<EndpointName>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="3790d-167">This name will be used tooaccess your cached resources at hello domain `<EndpointName>.azureedge.net`.</span></span>
4. <span data-ttu-id="3790d-168">Hola **tipo de origen** lista desplegable, seleccione *servicio en la nube*.</span><span class="sxs-lookup"><span data-stu-id="3790d-168">In hello **Origin type** dropdown, select *Cloud service*.</span></span>  
5. <span data-ttu-id="3790d-169">Hola **nombre de host de origen** de lista desplegable, seleccione el servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="3790d-169">In hello **Origin hostname** dropdown, select your cloud service.</span></span>
6. <span data-ttu-id="3790d-170">Deje los valores predeterminados de Hola para **ruta de acceso de origen**, **encabezado de host de origen**, y **puerto de protocolo/origen**.</span><span class="sxs-lookup"><span data-stu-id="3790d-170">Leave hello defaults for **Origin path**, **Origin host header**, and **Protocol/Origin port**.</span></span>  <span data-ttu-id="3790d-171">Debe especificar al menos un protocolo (HTTP o HTTPS).</span><span class="sxs-lookup"><span data-stu-id="3790d-171">You must specify at least one protocol (HTTP or HTTPS).</span></span>
7. <span data-ttu-id="3790d-172">Haga clic en hello **agregar** toocreate botón Hola nuevo punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="3790d-172">Click hello **Add** button toocreate hello new endpoint.</span></span>
8. <span data-ttu-id="3790d-173">Una vez que se crea el extremo de hello, aparece en una lista de puntos de conexión para el perfil de Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-173">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="3790d-174">vista de lista de Hello muestra hello URL toouse tooaccess almacenado en memoria caché de contenido, así como dominio de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-174">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
   
    ![Punto de conexión de CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > <span data-ttu-id="3790d-176">punto de conexión de Hello no inmediatamente estará disponible para su uso.</span><span class="sxs-lookup"><span data-stu-id="3790d-176">hello endpoint will not immediately be available for use.</span></span>  <span data-ttu-id="3790d-177">Puede tardar minutos too90 hello toopropagate de registro a través de la red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-177">It can take up too90 minutes for hello registration toopropagate through hello CDN network.</span></span> <span data-ttu-id="3790d-178">Los usuarios que intenten nombre de dominio de red CDN Hola de toouse inmediatamente pueden recibir el código de estado 404 hasta que esté disponible a través de la red CDN Hola contenido Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-178">Users who try toouse hello CDN domain name immediately may receive status code 404 until hello content is available via hello CDN.</span></span>
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a><span data-ttu-id="3790d-179">Hola extremo de red CDN de prueba</span><span class="sxs-lookup"><span data-stu-id="3790d-179">Test hello CDN endpoint</span></span>
<span data-ttu-id="3790d-180">Cuando es el estado de publicación de hello **completado**, abra una ventana del explorador y navegue demasiado**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span><span class="sxs-lookup"><span data-stu-id="3790d-180">When hello publishing status is **Completed**, open a browser window and navigate too**http://<cdnName>*.azureedge.net/Content/bootstrap.css**.</span></span> <span data-ttu-id="3790d-181">En nuestra instalación, esta URL es:</span><span class="sxs-lookup"><span data-stu-id="3790d-181">In my setup, this URL is:</span></span>

    http://camservice.azureedge.net/Content/bootstrap.css

<span data-ttu-id="3790d-182">Que corresponde a toohello después de la dirección URL de origen en el extremo de red CDN Hola:</span><span class="sxs-lookup"><span data-stu-id="3790d-182">Which corresponds toohello following origin URL at hello CDN endpoint:</span></span>

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

<span data-ttu-id="3790d-183">Cuando se desplaza demasiado**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, según el navegador, será toodownload solicitada o abrir hello bootstrap.css que que procede de la aplicación Web publicada.</span><span class="sxs-lookup"><span data-stu-id="3790d-183">When you navigate too**http://*&lt;cdnName>*.azureedge.net/Content/bootstrap.css**, depending on your browser, you will be prompted toodownload or open hello bootstrap.css that came from your published Web app.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

<span data-ttu-id="3790d-184">Puede acceder de forma parecida a cualquier dirección URL de acceso público en **http://*&lt;serviceName>*.cloudapp.net/** directamente desde el punto de conexión de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="3790d-184">You can similarly access any publicly accessible URL at **http://*&lt;serviceName>*.cloudapp.net/**, straight from your CDN endpoint.</span></span> <span data-ttu-id="3790d-185">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3790d-185">For example:</span></span>

* <span data-ttu-id="3790d-186">Un archivo .js de ruta de acceso / script de Hola</span><span class="sxs-lookup"><span data-stu-id="3790d-186">A .js file from hello /Script path</span></span>
* <span data-ttu-id="3790d-187">Cualquier archivo de contenido de Hola/Content ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="3790d-187">Any content file from hello /Content path</span></span>
* <span data-ttu-id="3790d-188">Cualquier controlador/acción</span><span class="sxs-lookup"><span data-stu-id="3790d-188">Any controller/action</span></span>
* <span data-ttu-id="3790d-189">Si la cadena de consulta de hello está habilitada en el punto de conexión de red CDN, cualquier dirección URL con cadenas de consulta</span><span class="sxs-lookup"><span data-stu-id="3790d-189">If hello query string is enabled at your CDN endpoint, any URL with query strings</span></span>

<span data-ttu-id="3790d-190">De hecho, con hello por encima de la configuración, puede hospedar un servicio nube todo Hola desde  **http://*&lt;cdnName >*.azureedge.net/**. Si desplaza demasiado**http://camservice.azureedge.net/ **, se pueden transferir el resultado de acción de Hola de Home/Index.</span><span class="sxs-lookup"><span data-stu-id="3790d-190">In fact, with hello above configuration, you can host hello entire cloud service from **http://*&lt;cdnName>*.azureedge.net/**. If I navigate too**http://camservice.azureedge.net/**, I get hello action result from Home/Index.</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

<span data-ttu-id="3790d-191">Esto no significa, sin embargo, que siempre es un tooserve buena idea un servicio de nube todo a través de la red CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="3790d-191">This does not mean, however, that it's always a good idea tooserve an entire cloud service through Azure CDN.</span></span> 

<span data-ttu-id="3790d-192">Una CDN con la optimización de entrega estático no necesariamente acelerar la entrega de activos dinámicas que no están diseñadas toobe almacenado en memoria caché o se actualizan con mucha frecuencia, ya que la CDN Hola debe extraiga una nueva versión del recurso de Hola de servidor de origen de hello muy a menudo.</span><span class="sxs-lookup"><span data-stu-id="3790d-192">A CDN with static delivery optimization does not necessarily speed up delivery of dynamic assets which are not meant toobe cached, or are updated very frequently, since hello CDN must pull a new version of hello asset from hello Origin server very often.</span></span> <span data-ttu-id="3790d-193">En este escenario, puede habilitar [aceleración de sitio dinámico](cdn-dynamic-site-acceleration.md) optimización (DSA) en el punto de conexión que utiliza varios toospeed técnicas la entrega de activos dinámicos no almacenable en caché.</span><span class="sxs-lookup"><span data-stu-id="3790d-193">For this scenario, you can enable [Dynamic Site Acceleration](cdn-dynamic-site-acceleration.md) optimization (DSA) on your CDN endpoint which uses various techniques toospeed up delivery of non-cacheable dynamic assets.</span></span> 

<span data-ttu-id="3790d-194">Si tiene un sitio con una combinación de contenido estático y dinámico, puede elegir tooserve el contenido estático de CDN con un tipo de optimización estático (por ejemplo, entrega de web general) y contenido dinámico tooserve directamente desde el servidor de origen de Hola o a través de una CDN punto de conexión con la optimización de DSA activada caso por caso.</span><span class="sxs-lookup"><span data-stu-id="3790d-194">If you have a site with a mix of static and dynamic content, you can choose tooserve your static content from CDN with a static optimization type (such as general web delivery), and tooserve dynamic content either directly from hello origin server, or through a CDN endpoint with DSA optimization turned on a case-by-case basis.</span></span> <span data-ttu-id="3790d-195">toothat final, ya ha visto cómo los archivos de contenido individuales tooaccess desde el punto de conexión de red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-195">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="3790d-196">Le mostrará cómo tooserve una acción de un controlador específico a través de un punto de conexión de red CDN concreto en servir contenido de las acciones de controlador a través de la red CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="3790d-196">I will show you how tooserve a specific controller action through a specific CDN endpoint in Serve content from controller actions through Azure CDN.</span></span>

<span data-ttu-id="3790d-197">alternativa de Hello es toodetermine qué contenido tooserve de red CDN de Azure de forma caso por caso en el servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="3790d-197">hello alternative is toodetermine which content tooserve from Azure CDN on a case-by-case basis in your cloud service.</span></span> <span data-ttu-id="3790d-198">toothat final, ya ha visto cómo los archivos de contenido individuales tooaccess desde el punto de conexión de red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-198">toothat end, you have already seen how tooaccess individual content files from hello CDN endpoint.</span></span> <span data-ttu-id="3790d-199">Le mostrará cómo tooserve una acción de un controlador específico a través de Hola extremo de red CDN en [servir el contenido de las acciones de controlador a través de la red CDN de Azure](#controller).</span><span class="sxs-lookup"><span data-stu-id="3790d-199">I will show you how tooserve a specific controller action through hello CDN endpoint in [Serve content from controller actions through Azure CDN](#controller).</span></span>

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a><span data-ttu-id="3790d-200">Configuración de las opciones de caché para los archivos estáticos del servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="3790d-200">Configure caching options for static files in your cloud service</span></span>
<span data-ttu-id="3790d-201">Con la integración de CDN de Azure en su servicio en la nube, puede especificar cómo desea estático toobe contenido en caché en el extremo de red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-201">With Azure CDN integration in your cloud service, you can specify how you want static content toobe cached in hello CDN endpoint.</span></span> <span data-ttu-id="3790d-202">toodo, abra *Web.config* de su rol Web de proyecto (por ejemplo, WebRole1) y agregue un `<staticContent>` elemento demasiado`<system.webServer>`.</span><span class="sxs-lookup"><span data-stu-id="3790d-202">toodo this, open *Web.config* from your Web role project (e.g. WebRole1) and add a `<staticContent>` element too`<system.webServer>`.</span></span> <span data-ttu-id="3790d-203">Hola XML siguiente configura Hola caché tooexpire en 3 días.</span><span class="sxs-lookup"><span data-stu-id="3790d-203">hello XML below configures hello cache tooexpire in 3 days.</span></span>  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

<span data-ttu-id="3790d-204">Una vez hecho esto, todos los archivos estáticos en el servicio de nube observará Hola igual de regla en la memoria caché de la red CDN.</span><span class="sxs-lookup"><span data-stu-id="3790d-204">Once you do this, all static files in your cloud service will observe hello same rule in your CDN cache.</span></span> <span data-ttu-id="3790d-205">Para un control más granular de la configuración de la caché, agregue un archivo *Web.config* a una carpeta y agregue ahí su configuración.</span><span class="sxs-lookup"><span data-stu-id="3790d-205">For more granular control of cache settings, add a *Web.config* file into a folder and add your settings there.</span></span> <span data-ttu-id="3790d-206">Por ejemplo, agregar un *Web.config* archivo toohello *\Content* carpeta y reemplazar Hola contenido con hello continuación de XML:</span><span class="sxs-lookup"><span data-stu-id="3790d-206">For example, add a *Web.config* file toohello *\Content* folder and replace hello content with hello following XML:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

<span data-ttu-id="3790d-207">Esta configuración hace que todos los archivos estáticos de hello *\Content* toobe de carpeta en caché durante 15 días.</span><span class="sxs-lookup"><span data-stu-id="3790d-207">This setting causes all static files from hello *\Content* folder toobe cached for 15 days.</span></span>

<span data-ttu-id="3790d-208">Para obtener más información acerca de cómo hello tooconfigure `<clientCache>` elemento, vea [memoria caché del cliente &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span><span class="sxs-lookup"><span data-stu-id="3790d-208">For more information on how tooconfigure hello `<clientCache>` element, see [Client Cache &lt;clientCache>](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).</span></span>

<span data-ttu-id="3790d-209">En [servir el contenido de las acciones de controlador a través de la red CDN de Azure](#controller), también le mostrará cómo puede configurar configuración de caché de resultados de la acción de controlador en caché la red CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-209">In [Serve content from controller actions through Azure CDN](#controller), I will also show you how you can configure cache settings for controller action results in hello CDN cache.</span></span>

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a><span data-ttu-id="3790d-210">Suministro de contenido de acciones de controlador a través de la red CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="3790d-210">Serve content from controller actions through Azure CDN</span></span>
<span data-ttu-id="3790d-211">Al integrar un rol Web de servicio de nube con la red CDN de Azure, es tooserve es relativamente fácil de contenido de las acciones de controlador a través de hello CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="3790d-211">When you integrate a cloud service Web role with Azure CDN, it is relatively easy tooserve content from controller actions through hello Azure CDN.</span></span> <span data-ttu-id="3790d-212">Aparte de servir la nube de servicio directamente a través de la red CDN de Azure (que se muestra anteriormente), [Maarten Balliauw](https://twitter.com/maartenballiauw) muestra cómo toodo con realizar un recorrido divertido MemeGenerator controlador [reducir la latencia en web Hola con hello CDN de Azure ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span><span class="sxs-lookup"><span data-stu-id="3790d-212">Other than serving your cloud service directly through Azure CDN (demonstrated above), [Maarten Balliauw](https://twitter.com/maartenballiauw) shows you how toodo it with a fun MemeGenerator controller in [Reducing latency on hello web with hello Azure CDN](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN).</span></span> <span data-ttu-id="3790d-213">Aquí simplemente lo vamos a reproducir.</span><span class="sxs-lookup"><span data-stu-id="3790d-213">I will simply reproduce it here.</span></span>

<span data-ttu-id="3790d-214">Imagine que en su servicio en la nube que desee memes toogenerate basada en una imagen de Chuck Norris jóvenes (fotografías por [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="3790d-214">Suppose in your cloud service you want toogenerate memes based on a young Chuck Norris image (photo by [Alan Light](http://www.flickr.com/photos/alan-light/218493788/)) like this:</span></span>

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

<span data-ttu-id="3790d-215">Tiene un sencillo `Index` acción que permite a los clientes de hello toospecify superlativas de hello en imagen de hello, a continuación, genera Hola personaje una vez que acción posterior a la toohello.</span><span class="sxs-lookup"><span data-stu-id="3790d-215">You have a simple `Index` action that allows hello customers toospecify hello superlatives in hello image, then generates hello meme once they post toohello action.</span></span> <span data-ttu-id="3790d-216">Puesto que es Chuck Norris, se podría esperar este toobecome página bastante popular globalmente.</span><span class="sxs-lookup"><span data-stu-id="3790d-216">Since it's Chuck Norris, you would expect this page toobecome wildly popular globally.</span></span> <span data-ttu-id="3790d-217">Este es un buen ejemplo de servir contenido dinámico con CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="3790d-217">This is a good example of serving semi-dynamic content with Azure CDN.</span></span>

<span data-ttu-id="3790d-218">Siga pasos anteriores toosetup con hello esta acción de controlador:</span><span class="sxs-lookup"><span data-stu-id="3790d-218">Follow hello steps above toosetup this controller action:</span></span>

1. <span data-ttu-id="3790d-219">Hola *\Controllers* carpeta, cree un archivo .cs denominado *MemeGeneratorController.cs* y reemplazar Hola contenido con hello siguiendo el código.</span><span class="sxs-lookup"><span data-stu-id="3790d-219">In hello *\Controllers* folder, create a new .cs file called *MemeGeneratorController.cs* and replace hello content with hello following code.</span></span> <span data-ttu-id="3790d-220">Ser parte resaltada de hello tooreplace seguro con el nombre de red CDN.</span><span class="sxs-lookup"><span data-stu-id="3790d-220">Be sure tooreplace hello highlighted portion with your CDN name.</span></span>  
   
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
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
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
2. <span data-ttu-id="3790d-221">Pulse el botón derecho en el valor predeterminado de hello `Index()` acción y seleccione **agregar vista**.</span><span class="sxs-lookup"><span data-stu-id="3790d-221">Right-click in hello default `Index()` action and select **Add View**.</span></span>
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. <span data-ttu-id="3790d-222">Acepte la configuración de Hola a continuación y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="3790d-222">Accept hello settings below and click **Add**.</span></span>
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. <span data-ttu-id="3790d-223">Hola abrir nueva *Views\MemeGenerator\Index.cshtml* y reemplazar el contenido de hello con hello sigue HTML simple para enviar superlativas hello:</span><span class="sxs-lookup"><span data-stu-id="3790d-223">Open hello new *Views\MemeGenerator\Index.cshtml* and replace hello content with hello following simple HTML for submitting hello superlatives:</span></span>
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. <span data-ttu-id="3790d-224">Vuelva a publicar el servicio de nube de Hola y navegue demasiado**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** en el explorador.</span><span class="sxs-lookup"><span data-stu-id="3790d-224">Publish hello cloud service again and navigate too**http://*&lt;serviceName>*.cloudapp.net/MemeGenerator/Index** in your browser.</span></span>

<span data-ttu-id="3790d-225">Cuando se envían los valores del formulario Hola demasiado`/MemeGenerator/Index`, hello `Index_Post` método de acción devuelve un vínculo toohello `Show` método de acción con el identificador de entrada respectivos Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-225">When you submit hello form values too`/MemeGenerator/Index`, hello `Index_Post` action method returns a link toohello `Show` action method with hello respective input identifier.</span></span> <span data-ttu-id="3790d-226">Al hacer clic en el vínculo de hello, alcanzar Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="3790d-226">When you click hello link, you reach hello following code:</span></span>  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

<span data-ttu-id="3790d-227">Si se asocia el depurador local, obtendrá experiencia de depuración normal de hello con una redirección local.</span><span class="sxs-lookup"><span data-stu-id="3790d-227">If your local debugger is attached, then you will get hello regular debug experience with a local redirect.</span></span> <span data-ttu-id="3790d-228">Si se está ejecutando en el servicio de nube de hello, redirigirá al:</span><span class="sxs-lookup"><span data-stu-id="3790d-228">If it's running in hello cloud service, then it will redirect to:</span></span>

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

<span data-ttu-id="3790d-229">Que corresponde a toohello después de la dirección URL de origen en el punto de conexión:</span><span class="sxs-lookup"><span data-stu-id="3790d-229">Which corresponds toohello following origin URL at your CDN endpoint:</span></span>

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


<span data-ttu-id="3790d-230">A continuación, puede usar hello `OutputCacheAttribute` atributo hello `Generate` toospecify método cómo debe almacenarse en caché el resultado de acción de hello, que respeta la CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="3790d-230">You can then use hello `OutputCacheAttribute` attribute on hello `Generate` method toospecify how hello action result should be cached, which Azure CDN will honor.</span></span> <span data-ttu-id="3790d-231">código de Hello siguiente especifica una expiración de caché de 1 hora (3600 segundos).</span><span class="sxs-lookup"><span data-stu-id="3790d-231">hello code below specify a cache expiration of 1 hour (3,600 seconds).</span></span>

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

<span data-ttu-id="3790d-232">Del mismo modo, puede servir el contenido de cualquier acción de controlador en el servicio de nube a través de la red CDN de Azure, con la opción de almacenamiento en caché de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="3790d-232">Likewise, you can serve up content from any controller action in your cloud service through your Azure CDN, with hello desired caching option.</span></span>

<span data-ttu-id="3790d-233">En la siguiente sección hello, mostraré cómo tooserve Hola agrupadas y reduce las secuencias de comandos y CSS a través de la red CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="3790d-233">In hello next section, I will show you how tooserve hello bundled and minified scripts and CSS through Azure CDN.</span></span>

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a><span data-ttu-id="3790d-234">Integración de unión y minificación de ASP.NET con CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="3790d-234">Integrate ASP.NET bundling and minification with Azure CDN</span></span>
<span data-ttu-id="3790d-235">Hojas de estilos CSS y secuencias de comandos cambian con poca frecuencia y son los principales candidatos para la caché de Azure CDN Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-235">Scripts and CSS stylesheets change infrequently and are prime candidates for hello Azure CDN cache.</span></span> <span data-ttu-id="3790d-236">Rol Web que se sirva Hola todo a través de la red CDN de Azure es toointegrate de manera más fácil de hello agrupación y minificación con CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="3790d-236">Serving hello entire Web role through your Azure CDN is hello easiest way toointegrate bundling and minification with Azure CDN.</span></span> <span data-ttu-id="3790d-237">Sin embargo, como puede que no desee toodo esto, le mostrará cómo toodo mientras conserva Hola había deseado Developer experiencia de ASP.NET agrupar y minificar, como:</span><span class="sxs-lookup"><span data-stu-id="3790d-237">However, as you may not want toodo this, I will show you how toodo it while preserving hello desired develper experience of ASP.NET bundling and minification, such as:</span></span>

* <span data-ttu-id="3790d-238">Gran experiencia en el modo de depuración</span><span class="sxs-lookup"><span data-stu-id="3790d-238">Great debug mode experience</span></span>
* <span data-ttu-id="3790d-239">Implementación optimizada</span><span class="sxs-lookup"><span data-stu-id="3790d-239">Streamlined deployment</span></span>
* <span data-ttu-id="3790d-240">Actualizaciones inmediatas tooclients para las actualizaciones de versión de secuencia de comandos/CSS</span><span class="sxs-lookup"><span data-stu-id="3790d-240">Immediate updates tooclients for script/CSS version upgrades</span></span>
* <span data-ttu-id="3790d-241">Mecanismo de reserva cuando el extremo de red CDN falla</span><span class="sxs-lookup"><span data-stu-id="3790d-241">Fallback mechanism when your CDN endpoint fails</span></span>
* <span data-ttu-id="3790d-242">Menor modificación del código</span><span class="sxs-lookup"><span data-stu-id="3790d-242">Minimize code modification</span></span>

<span data-ttu-id="3790d-243">Hola **WebRole1** proyecto que creó en [integrar un punto de conexión de red CDN de Azure con su sitio Web de Azure y servir contenido estático en las páginas Web de la red CDN de Azure](#deploy), abra *App_Start\ BundleConfig.cs* y eche un vistazo a hello `bundles.Add()` llamadas al método.</span><span class="sxs-lookup"><span data-stu-id="3790d-243">In hello **WebRole1** project that you created in [Integrate an Azure CDN endpoint with your Azure website and serve static content in your Web pages from Azure CDN](#deploy), open *App_Start\BundleConfig.cs* and take a look at hello `bundles.Add()` method calls.</span></span>

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

<span data-ttu-id="3790d-244">Hola primero `bundles.Add()` instrucción agrega una agrupación de scripts en el directorio virtual de hello `~/bundles/jquery`.</span><span class="sxs-lookup"><span data-stu-id="3790d-244">hello first `bundles.Add()` statement adds a script bundle at hello virtual directory `~/bundles/jquery`.</span></span> <span data-ttu-id="3790d-245">A continuación, abra *Views\Shared\_Layout.cshtml* toosee cómo se representa la etiqueta de agrupación de script de Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-245">Then, open *Views\Shared\_Layout.cshtml* toosee how hello script bundle tag is rendered.</span></span> <span data-ttu-id="3790d-246">Debe ser hello toofind pueda después de la línea de código Razor:</span><span class="sxs-lookup"><span data-stu-id="3790d-246">You should be able toofind hello following line of Razor code:</span></span>

    @Scripts.Render("~/bundles/jquery")

<span data-ttu-id="3790d-247">Cuando se ejecuta este código Razor en función de hello Web de Azure, se representará un `<script>` etiqueta para hello script siguiente toohello similar de agrupación:</span><span class="sxs-lookup"><span data-stu-id="3790d-247">When this Razor code is run in hello Azure Web role, it will render a `<script>` tag for hello script bundle similar toohello following:</span></span>

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

<span data-ttu-id="3790d-248">Sin embargo, cuando se ejecuta en Visual Studio escribiendo `F5`, representará individualmente cada archivo de script de agrupación de Hola (en caso de hello anterior, solo un archivo de scripts está en agrupación de hello):</span><span class="sxs-lookup"><span data-stu-id="3790d-248">However, when it is run in Visual Studio by typing `F5`, it will render each script file in hello bundle individually (in hello case above, only one script file is in hello bundle):</span></span>

    <script src="/Scripts/jquery-1.10.2.js"></script>

<span data-ttu-id="3790d-249">Esto le permite toodebug código de JavaScript de hello en el entorno de desarrollo mientras lo que reduce las conexiones de cliente simultáneas (unión) y se mejora el archivo descargar rendimiento (minificación) en producción.</span><span class="sxs-lookup"><span data-stu-id="3790d-249">This enables you toodebug hello JavaScript code in your development environment while reducing concurrent client connections (bundling) and improving file download performance (minification) in production.</span></span> <span data-ttu-id="3790d-250">Es un toopreserve característica excelente con la integración de CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="3790d-250">It's a great feature toopreserve with Azure CDN integration.</span></span> <span data-ttu-id="3790d-251">Además, puesto que la agrupación de hello representa ya contiene una cadena de versión generada automáticamente, desea tooreplicate que funcionalidad Hola por lo que cada vez que actualice su versión de jQuery a través de NuGet, se puede actualizar en el cliente hello tan pronto como es posible.</span><span class="sxs-lookup"><span data-stu-id="3790d-251">Furthermore, since hello rendered bundle already contains an automatically generated version string, you want tooreplicate that functionality so hello whenever you update your jQuery version through NuGet, it can be updated at hello client side as soon as possible.</span></span>

<span data-ttu-id="3790d-252">Siga los pasos de Hola por debajo de la agrupación de ASP.NET de toointegration y minificación con el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="3790d-252">Follow hello steps below toointegration ASP.NET bundling and minification with your CDN endpoint.</span></span>

1. <span data-ttu-id="3790d-253">En *App_Start\BundleConfig.cs*, modificar hello `bundles.Add()` toouse métodos otra [constructor agrupación](http://msdn.microsoft.com/library/jj646464.aspx), que especifica una dirección de red CDN.</span><span class="sxs-lookup"><span data-stu-id="3790d-253">Back in *App_Start\BundleConfig.cs*, modify hello `bundles.Add()` methods toouse a different [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), one that specifies a CDN address.</span></span> <span data-ttu-id="3790d-254">toodo, Hola reemplazar `RegisterBundles` definición de método con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="3790d-254">toodo this, replace hello `RegisterBundles` method definition with hello following code:</span></span>  
   
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
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    <span data-ttu-id="3790d-255">Ser seguro tooreplace `<yourCDNName>` con nombre hello la red CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="3790d-255">Be sure tooreplace `<yourCDNName>` with hello name of your Azure CDN.</span></span>
   
    <span data-ttu-id="3790d-256">En palabras sencillas, se establece `bundles.UseCdn = true` y agrega una agrupación de tooeach de dirección URL de CDN cuidadosamente diseñada.</span><span class="sxs-lookup"><span data-stu-id="3790d-256">In plain words, you are setting `bundles.UseCdn = true` and added a carefully crafted CDN URL tooeach bundle.</span></span> <span data-ttu-id="3790d-257">Por ejemplo, hello primer constructor en el código de hello:</span><span class="sxs-lookup"><span data-stu-id="3790d-257">For example, hello first constructor in hello code:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    <span data-ttu-id="3790d-258">se Hola igual que:</span><span class="sxs-lookup"><span data-stu-id="3790d-258">is hello same as:</span></span>
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    <span data-ttu-id="3790d-259">Este constructor indica a ASP.NET agrupar y minificar toorender de archivos de script individuales cuando depura localmente, pero use Hola especificado CDN dirección tooaccess hello secuencia de comandos en cuestión.</span><span class="sxs-lookup"><span data-stu-id="3790d-259">This constructor tells ASP.NET bundling and minification toorender individual script files when debugged locally, but use hello specified CDN address tooaccess hello script in question.</span></span> <span data-ttu-id="3790d-260">Sin embargo, observe dos características importantes con esta URL de red CDN diseñada especialmente:</span><span class="sxs-lookup"><span data-stu-id="3790d-260">However, note two important characteristics with this carefully crafted CDN URL:</span></span>
   
   * <span data-ttu-id="3790d-261">origen de Hola para esta dirección URL de la red CDN es `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, que es realmente Hola de directorio virtual de la agrupación de scripts de hello en el servicio de nube.</span><span class="sxs-lookup"><span data-stu-id="3790d-261">hello origin for this CDN URL is `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, which is actually hello virtual directory of hello script bundle in your cloud service.</span></span>
   * <span data-ttu-id="3790d-262">Puesto que utiliza el constructor de la red CDN, etiqueta de script CDN para agrupación Hola Hola ya no contiene cadena de versión de Hola generada automáticamente en hello representado la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="3790d-262">Since you are using CDN constructor, hello CDN script tag for hello bundle no longer contains hello automatically generated version string in hello rendered URL.</span></span> <span data-ttu-id="3790d-263">También debe generar manualmente una cadena de versión único cada vez que agrupación de scripts de Hola se tooforce modificado se pierda una memoria caché en la red CDN de Azure.</span><span class="sxs-lookup"><span data-stu-id="3790d-263">You must manually generate a unique version string every time hello script bundle is modified tooforce a cache miss at your Azure CDN.</span></span> <span data-ttu-id="3790d-264">Hola al mismo tiempo, esta cadena de versión único debe permanecer constante a través de la vida de Hola Hola implementación toomaximize de aciertos de caché en la red CDN de Azure después de implementa el paquete de saludo.</span><span class="sxs-lookup"><span data-stu-id="3790d-264">At hello same time, this unique version string must remain constant through hello life of hello deployment toomaximize cache hits at your Azure CDN after hello bundle is deployed.</span></span>
   * <span data-ttu-id="3790d-265">Hola de cadena de consulta v = < W.X.Y.Z > extracciones de *Properties\AssemblyInfo* en su proyecto de rol Web.</span><span class="sxs-lookup"><span data-stu-id="3790d-265">hello query string v=<W.X.Y.Z> pulls from *Properties\AssemblyInfo.cs* in your Web role project.</span></span> <span data-ttu-id="3790d-266">Puede tener un flujo de trabajo de implementación que incluya incrementar la versión del ensamblado hello cada vez que publique tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3790d-266">You can have a deployment workflow that includes incrementing hello assembly version every time you publish tooAzure.</span></span> <span data-ttu-id="3790d-267">O bien, simplemente puede modificar *Properties\AssemblyInfo* en la cadena de versión de proyecto tooautomatically incremento Hola cada vez que compile, utilizando el carácter comodín de hello ' *'.</span><span class="sxs-lookup"><span data-stu-id="3790d-267">Or, you can just modify *Properties\AssemblyInfo.cs* in your project tooautomatically increment hello version string every time you build, using hello wildcard character '*'.</span></span> <span data-ttu-id="3790d-268">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3790d-268">For example:</span></span>
     
        <span data-ttu-id="3790d-269">[assembly: AssemblyVersion("1.0.0.*")]</span><span class="sxs-lookup"><span data-stu-id="3790d-269">[assembly: AssemblyVersion("1.0.0.*")]</span></span>
     
     <span data-ttu-id="3790d-270">Otro toostreamline de estrategia generando una cadena única para la vida de una implementación de hello funcionará aquí.</span><span class="sxs-lookup"><span data-stu-id="3790d-270">Any other strategy toostreamline generating a unique string for hello life of a deployment will work here.</span></span>
2. <span data-ttu-id="3790d-271">Volver a publicar Hola nube acceso y el servicio Hola página principal.</span><span class="sxs-lookup"><span data-stu-id="3790d-271">Republish hello cloud service and access hello home page.</span></span>
3. <span data-ttu-id="3790d-272">Hola de la vista código HTML de la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-272">View hello HTML code for hello page.</span></span> <span data-ttu-id="3790d-273">Debe ser capaz de toosee Hola representan con una cadena de versión único cada vez que vuelve a publicar servicio en la nube tooyour cambios de dirección URL de CDN.</span><span class="sxs-lookup"><span data-stu-id="3790d-273">You should be able toosee hello CDN URL rendered, with a unique version string every time you republish changes tooyour cloud service.</span></span> <span data-ttu-id="3790d-274">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3790d-274">For example:</span></span>  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. <span data-ttu-id="3790d-275">En Visual Studio, depurar el servicio de nube de hello en Visual Studio escribiendo `F5`.,</span><span class="sxs-lookup"><span data-stu-id="3790d-275">In Visual Studio, debug hello cloud service in Visual Studio by typing `F5`.,</span></span>
5. <span data-ttu-id="3790d-276">Hola de la vista código HTML de la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-276">View hello HTML code for hello page.</span></span> <span data-ttu-id="3790d-277">Aún verá cada archivo de script procesado de forma individual para que pueda tener una experiencia de depuración coherente en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3790d-277">You will still see each script file individually rendered so that you can have a consistent debug experience in Visual Studio.</span></span>  
   
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

## <a name="fallback-mechanism-for-cdn-urls"></a><span data-ttu-id="3790d-278">Mecanismo de reserva para URL de red CDN</span><span class="sxs-lookup"><span data-stu-id="3790d-278">Fallback mechanism for CDN URLs</span></span>
<span data-ttu-id="3790d-279">Cuando se produce un error en el punto de conexión de red CDN de Azure por cualquier motivo, desea que la página Web toobe inteligentes suficiente tooaccess su servidor Web de origen como opción de reserva de hello para la carga de JavaScript o arranque.</span><span class="sxs-lookup"><span data-stu-id="3790d-279">When your Azure CDN endpoint fails for any reason, you want your Web page toobe smart enough tooaccess your origin Web server as hello fallback option for loading JavaScript or Bootstrap.</span></span> <span data-ttu-id="3790d-280">Es lo suficientemente grave como toolose imágenes en el sitio Web debido a falta de disponibilidad de tooCDN, pero mucho más grave funcionalidad de página fundamental de toolose proporcionada por los scripts y hojas de estilos.</span><span class="sxs-lookup"><span data-stu-id="3790d-280">It's serious enough toolose images on your website due tooCDN unavailability, but much more severe toolose crucial page functionality provided by your scripts and stylesheets.</span></span>

<span data-ttu-id="3790d-281">Hola [agrupación](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) clase contiene una propiedad denominada [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) que permite el mecanismo de reserva de hello tooconfigure error de red CDN.</span><span class="sxs-lookup"><span data-stu-id="3790d-281">hello [Bundle](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) class contains a property called [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) that enables you tooconfigure hello fallback mechanism for CDN failure.</span></span> <span data-ttu-id="3790d-282">toouse esta propiedad, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="3790d-282">toouse this property, follow hello steps below:</span></span>

1. <span data-ttu-id="3790d-283">En su proyecto de rol Web, abra *App_Start\BundleConfig.cs*, que ha agregado una dirección URL de la red CDN en cada [constructor agrupación](http://msdn.microsoft.com/library/jj646464.aspx)y realice el siguiente Hola resaltado cambia tooadd mecanismo de reserva toohello agrupaciones de forma predeterminada:</span><span class="sxs-lookup"><span data-stu-id="3790d-283">In your Web role project, open *App_Start\BundleConfig.cs*, where you added a CDN URL in each [Bundle constructor](http://msdn.microsoft.com/library/jj646464.aspx), and make hello following highlighted changes tooadd fallback mechanism toohello default bundles:</span></span>  
   
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
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
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
   
    <span data-ttu-id="3790d-284">Cuando `CdnFallbackExpression` es no es null, secuencia de comandos se aplica en tootest Hola HTML si la agrupación de Hola se ha cargado correctamente y, si no es así, obtener acceso a Hola paquete directamente desde el servidor Web de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-284">When `CdnFallbackExpression` is not null, script is injected into hello HTML tootest whether hello bundle is loaded successfully and, if not, access hello bundle directly from hello origin Web server.</span></span> <span data-ttu-id="3790d-285">Esta propiedad debe toobe conjunto tooa JavaScript expresión que comprueba si el paquete de red CDN respectivo Hola está cargado correctamente.</span><span class="sxs-lookup"><span data-stu-id="3790d-285">This property needs toobe set tooa JavaScript expression that tests whether hello respective CDN bundle is loaded properly.</span></span> <span data-ttu-id="3790d-286">expresión de Hello necesarios tootest difiere de cada paquete de contenido de toohello correspondiente.</span><span class="sxs-lookup"><span data-stu-id="3790d-286">hello expression needed tootest each bundle differs according toohello content.</span></span> <span data-ttu-id="3790d-287">Para paquetes de forma predeterminada Hola anteriores:</span><span class="sxs-lookup"><span data-stu-id="3790d-287">For hello default bundles above:</span></span>
   
   * <span data-ttu-id="3790d-288">`window.jquery` se define en jquery-{version}.js</span><span class="sxs-lookup"><span data-stu-id="3790d-288">`window.jquery` is defined in jquery-{version}.js</span></span>
   * <span data-ttu-id="3790d-289">`$.validator` se define en jquery.validate.js</span><span class="sxs-lookup"><span data-stu-id="3790d-289">`$.validator` is defined in jquery.validate.js</span></span>
   * <span data-ttu-id="3790d-290">`window.Modernizr` se define en modernizer-{version}.js</span><span class="sxs-lookup"><span data-stu-id="3790d-290">`window.Modernizr` is defined in modernizer-{version}.js</span></span>
   * <span data-ttu-id="3790d-291">`$.fn.modal` se define en bootstrap.js</span><span class="sxs-lookup"><span data-stu-id="3790d-291">`$.fn.modal` is defined in bootstrap.js</span></span>
     
     <span data-ttu-id="3790d-292">Puede que haya observado que no establecido CdnFallbackExpression para hello `~/Cointent/css` agrupación.</span><span class="sxs-lookup"><span data-stu-id="3790d-292">You might have noticed that I did not set CdnFallbackExpression for hello `~/Cointent/css` bundle.</span></span> <span data-ttu-id="3790d-293">Esto es porque actualmente hay un [error en System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) que inserta un `<script>` etiqueta para hello espera reserva CSS en lugar de hello `<link>` etiqueta.</span><span class="sxs-lookup"><span data-stu-id="3790d-293">This is because currently there is a [bug in System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) that injects a `<script>` tag for hello fallback CSS instead of hello expected `<link>` tag.</span></span>
     
     <span data-ttu-id="3790d-294">Sin embargo, existe una buena [solución de reserva de paquetes de estilo](https://github.com/EmberConsultingGroup/StyleBundleFallback) que ofrece [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span><span class="sxs-lookup"><span data-stu-id="3790d-294">There is, however, a good [Style Bundle Fallback](https://github.com/EmberConsultingGroup/StyleBundleFallback) offered by [Ember Consulting Group](https://github.com/EmberConsultingGroup).</span></span>
2. <span data-ttu-id="3790d-295">solución de Hola de toouse de CSS, cree un nuevo archivo .cs en su proyecto de rol Web *App_Start* carpeta denominada *StyleBundleExtensions.cs*y reemplazar su contenido con hello [código GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span><span class="sxs-lookup"><span data-stu-id="3790d-295">toouse hello workaround for CSS, create a new .cs file in your Web role project's *App_Start* folder called *StyleBundleExtensions.cs*, and replace its content with hello [code from GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).</span></span>
3. <span data-ttu-id="3790d-296">En *App_Start\StyleFundleExtensions.cs*, cambiar el nombre del rol de hello espacio de nombres tooyour Web (por ejemplo, **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="3790d-296">In *App_Start\StyleFundleExtensions.cs*, rename hello namespace tooyour Web role's name (e.g. **WebRole1**).</span></span>
4. <span data-ttu-id="3790d-297">Vuelva demasiado`App_Start\BundleConfig.cs` y modificar Hola última `bundles.Add` instrucción con hello después el código que aparece resaltado:</span><span class="sxs-lookup"><span data-stu-id="3790d-297">Go back too`App_Start\BundleConfig.cs` and modify hello last `bundles.Add` statement with hello following highlighted code:</span></span>  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    <span data-ttu-id="3790d-298">Este nuevo método de extensión usa Hola misma idea tooinject script Hola HTML toocheck Hola DOM para hello una coincidencia de nombre de clase, el nombre de la regla y el valor de regla definidos en la agrupación CSS de Hola y corresponden a las fechas toohello back-origen Web server si se produce un error de coincidencia de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="3790d-298">This new extension method uses hello same idea tooinject script in hello HTML toocheck hello DOM for hello a matching class name, rule name, and rule value defined in hello CSS bundle, and falls back toohello origin Web server if it fails toofind hello match.</span></span>
5. <span data-ttu-id="3790d-299">Publicar servicio en la nube Hola nuevo y página principal de Hola de acceso.</span><span class="sxs-lookup"><span data-stu-id="3790d-299">Publish hello cloud service again and access hello home page.</span></span>
6. <span data-ttu-id="3790d-300">Hola de la vista código HTML de la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="3790d-300">View hello HTML code for hello page.</span></span> <span data-ttu-id="3790d-301">Debería encontrar scripts insertado similar toohello siguiente:</span><span class="sxs-lookup"><span data-stu-id="3790d-301">You should find injected scripts similar toohello following:</span></span>    
   
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

    <span data-ttu-id="3790d-302">Tenga en cuenta que script insertado para agrupación CSS de hello todavía contiene restantes malicioso de Hola de hello `CdnFallbackExpression` propiedad en línea hello:</span><span class="sxs-lookup"><span data-stu-id="3790d-302">Note that injected script for hello CSS bundle still contains hello errant remnant from hello `CdnFallbackExpression` property in hello line:</span></span>

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    <span data-ttu-id="3790d-303">Pero, puesto que la primera parte de Hola de hello || expresión siempre devolverá true (en línea hello directamente encima), función de la sección de hello nunca se ejecutará.</span><span class="sxs-lookup"><span data-stu-id="3790d-303">But since hello first part of hello || expression will always return true (in hello line directly above that), hello document.write() function will never run.</span></span>

## <a name="more-information"></a><span data-ttu-id="3790d-304">Más información</span><span class="sxs-lookup"><span data-stu-id="3790d-304">More Information</span></span>
* [<span data-ttu-id="3790d-305">Información general de hello red de entrega de contenido (CDN) de Azure</span><span class="sxs-lookup"><span data-stu-id="3790d-305">Overview of hello Azure Content Delivery Network (CDN)</span></span>](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [<span data-ttu-id="3790d-306">Uso de CDN de Azure</span><span class="sxs-lookup"><span data-stu-id="3790d-306">Using Azure CDN</span></span>](cdn-create-new-endpoint.md)
* [<span data-ttu-id="3790d-307">Unión y minificación de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="3790d-307">ASP.NET Bundling and Minification</span></span>](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
