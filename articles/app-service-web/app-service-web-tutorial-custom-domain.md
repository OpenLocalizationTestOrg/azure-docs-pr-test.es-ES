---
title: aaaMap un DNS personalizado existente nombre de las aplicaciones Web tooAzure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooadd un dominio DNS personalizado existente nombre de aplicación de web (dominio personal) tooa, back-end de aplicación móvil o aplicación de API de servicio de aplicaciones de Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a><span data-ttu-id="71559-103">Asignar un tooAzure de nombre DNS personalizado existente aplicaciones Web</span><span class="sxs-lookup"><span data-stu-id="71559-103">Map an existing custom DNS name tooAzure Web Apps</span></span>

<span data-ttu-id="71559-104">[Azure Web Apps](app-service-web-overview.md) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="71559-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="71559-105">Este tutorial muestra cómo toomap un DNS personalizado existente nombre tooAzure las aplicaciones Web.</span><span class="sxs-lookup"><span data-stu-id="71559-105">This tutorial shows you how toomap an existing custom DNS name tooAzure Web Apps.</span></span>

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="71559-107">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="71559-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="71559-108">Asignar un subdominio (por ejemplo, `www.contoso.com`) mediante el uso de un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="71559-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="71559-109">Asignar un dominio raíz (por ejemplo, `contoso.com`) mediante el uso de un registro D</span><span class="sxs-lookup"><span data-stu-id="71559-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="71559-110">Asignar un dominio con comodín (por ejemplo, `*.contoso.com`) mediante el uso de un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="71559-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="71559-111">Automatizar la asignación de dominio con scripts</span><span class="sxs-lookup"><span data-stu-id="71559-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="71559-112">Puede usar un **registro CNAME** o un **un registro** toomap un DNS personalizado nombre tooApp servicio.</span><span class="sxs-lookup"><span data-stu-id="71559-112">You can use either a **CNAME record** or an **A record** toomap a custom DNS name tooApp Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="71559-113">Se recomienda usar un CNAME para todos los nombres DNS personalizados, excepto un dominio raíz (por ejemplo, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="71559-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="71559-114">toomigrate un sitio en vivo y su nombre de dominio DNS tooApp servicio, consulte [migrar un tooAzure de nombre DNS servicio de aplicaciones active](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="71559-114">toomigrate a live site and its DNS domain name tooApp Service, see [Migrate an active DNS name tooAzure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71559-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="71559-115">Prerequisites</span></span>

<span data-ttu-id="71559-116">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="71559-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="71559-117">[Cree una aplicación de App Service](/azure/app-service/) o use alguna aplicación que haya creado para otro tutorial.</span><span class="sxs-lookup"><span data-stu-id="71559-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="71559-118">Comprar un nombre de dominio y asegúrese de que dispone del registro DNS de acceso toohello para su proveedor de dominio (por ejemplo, GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="71559-118">Purchase a domain name and make sure you have access toohello DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="71559-119">Por ejemplo, tooadd entradas DNS para `contoso.com` y `www.contoso.com`, debe ser la configuración de DNS de hello tooconfigure capaz de hello `contoso.com` dominio raíz.</span><span class="sxs-lookup"><span data-stu-id="71559-119">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must be able tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="71559-120">Si no tiene un dominio existente de nombres, considere la posibilidad de [comprar un dominio con Hola portal de Azure](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="71559-120">If you don't have an existing domain name, consider [purchasing a domain using hello Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-hello-app"></a><span data-ttu-id="71559-121">Preparar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="71559-121">Prepare hello app</span></span>

<span data-ttu-id="71559-122">toomap una personalizado DNS nombre tooa la aplicación web, aplicación web de hello [plan de servicio de aplicaciones](https://azure.microsoft.com/pricing/details/app-service/) debe ser una capa de pagada (**Shared**, **básica**, **estándar**, o  **Premium**).</span><span class="sxs-lookup"><span data-stu-id="71559-122">toomap a custom DNS name tooa web app, hello web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="71559-123">En este paso, asegúrese de que ese servicio de aplicaciones de aplicación se encuentre en Hola Hola admite el nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="71559-123">In this step, you make sure that hello App Service app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="71559-124">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="71559-124">Sign in tooAzure</span></span>

<span data-ttu-id="71559-125">Abra hello [portal de Azure](https://portal.azure.com) e inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="71559-125">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="71559-126">Navegue toohello aplicación Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="71559-126">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="71559-127">En el menú izquierdo de hello, seleccione **servicios de aplicaciones**y, a continuación, seleccione nombre de Hola de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="71559-127">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="71559-129">Verá que la página de administración de Hola de hello aplicación de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="71559-129">You see hello management page of hello App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="71559-130">Hola de comprobación de nivel de precios</span><span class="sxs-lookup"><span data-stu-id="71559-130">Check hello pricing tier</span></span>

<span data-ttu-id="71559-131">Hola a la izquierda de la página de la aplicación hello, desplácese toohello **configuración** sección y seleccione **escalar verticalmente (plan de servicio de aplicaciones)**.</span><span class="sxs-lookup"><span data-stu-id="71559-131">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menú Escalar verticalmente](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="71559-133">nivel actual de la aplicación Hello aparece resaltado por un borde azul.</span><span class="sxs-lookup"><span data-stu-id="71559-133">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="71559-134">Compruebe que dicha aplicación hello no esté en hello toomake **libre** capa.</span><span class="sxs-lookup"><span data-stu-id="71559-134">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="71559-135">DNS personalizado no se admite en hello **libre** capa.</span><span class="sxs-lookup"><span data-stu-id="71559-135">Custom DNS is not supported in hello **Free** tier.</span></span> 

![Comprobar plan de tarifa](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="71559-137">Si hello plan de servicio de aplicaciones no es **libre**, cierre hello **elegir el nivel de precios** página y omitir demasiado[asignar un registro CNAME](#cname).</span><span class="sxs-lookup"><span data-stu-id="71559-137">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="71559-138">Escalar verticalmente Hola plan de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="71559-138">Scale up hello App Service plan</span></span>

<span data-ttu-id="71559-139">Seleccione cualquiera de los niveles de hello no disponibles (**Shared**, **básica**, **estándar**, o **Premium**).</span><span class="sxs-lookup"><span data-stu-id="71559-139">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="71559-140">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="71559-140">Click **Select**.</span></span>

![Comprobar plan de tarifa](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="71559-142">Cuando vea Hola siguientes a la notificación, la operación de escalado de hello está completa.</span><span class="sxs-lookup"><span data-stu-id="71559-142">When you see hello following notification, hello scale operation is complete.</span></span>

![Confirmación de la operación de escalado](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="71559-144">Asignar un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="71559-144">Map a CNAME record</span></span>

<span data-ttu-id="71559-145">En el ejemplo hello del tutorial, agregará un registro CNAME para hello `www` subdominio (por ejemplo, `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="71559-145">In hello tutorial example, you add a CNAME record for hello `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="71559-146">Crear registro CNAME Hola</span><span class="sxs-lookup"><span data-stu-id="71559-146">Create hello CNAME record</span></span>

<span data-ttu-id="71559-147">Agregar un toomap registro CNAME en el nombre de host de la aplicación de toohello subdominio predeterminado (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="71559-147">Add a CNAME record toomap a subdomain toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="71559-148">Para hello `www.contoso.com` ejemplo de un dominio, agregue un registro CNAME que asigna nombre hello `www` demasiado`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="71559-148">For hello `www.contoso.com` domain example, add a CNAME record that maps hello name `www` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="71559-149">Después de agregar Hola CNAME, página de registros DNS de hello aspecto Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="71559-149">After you add hello CNAME, hello DNS records page looks like hello following example:</span></span>

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a><span data-ttu-id="71559-151">Habilitar asignación de registro CNAME de hello en Azure</span><span class="sxs-lookup"><span data-stu-id="71559-151">Enable hello CNAME record mapping in Azure</span></span>

<span data-ttu-id="71559-152">Hola dejado de navegación de página de la aplicación Hola Hola portal de Azure, seleccione **los dominios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="71559-152">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menú Dominio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="71559-154">Hola **los dominios personalizados** página de la aplicación hello, agregar Hola personalizado nombre DNS completo (`www.contoso.com`) toohello lista.</span><span class="sxs-lookup"><span data-stu-id="71559-154">In hello **Custom domains** page of hello app, add hello fully qualified custom DNS name (`www.contoso.com`) toohello list.</span></span>

<span data-ttu-id="71559-155">Seleccione hello  **+**  icono siguiente demasiado**Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="71559-155">Select hello **+** icon next too**Add hostname**.</span></span>

![Agregar nombre de host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="71559-157">Nombre de dominio completo de tipo hello que ha agregado un registro CNAME, como `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="71559-157">Type hello fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="71559-158">Seleccione **Validar**.</span><span class="sxs-lookup"><span data-stu-id="71559-158">Select **Validate**.</span></span>

<span data-ttu-id="71559-159">Hola **Agregar nombre de host** se activa el botón.</span><span class="sxs-lookup"><span data-stu-id="71559-159">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="71559-160">Asegúrese de que **tipo de registro de nombre de host** se establece demasiado**CNAME (www.example.com o cualquier subdominio)**.</span><span class="sxs-lookup"><span data-stu-id="71559-160">Make sure that **Hostname record type** is set too**CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="71559-161">Seleccione **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="71559-161">Select **Add hostname**.</span></span>

![Agregar aplicación de toohello de nombre DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="71559-163">Puede tardar algún tiempo Hola nuevo nombre de host toobe reflejado en la aplicación hello **los dominios personalizados** página.</span><span class="sxs-lookup"><span data-stu-id="71559-163">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="71559-164">Intente actualizar los datos de saludo explorador tooupdate Hola.</span><span class="sxs-lookup"><span data-stu-id="71559-164">Try refreshing hello browser tooupdate hello data.</span></span>

![Registro CNAME agregado](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="71559-166">Si falta un paso o cometió un alguna versión anterior, verá un error de comprobación en parte inferior de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="71559-166">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Error de comprobación](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="71559-168">Asignar un registro A</span><span class="sxs-lookup"><span data-stu-id="71559-168">Map an A record</span></span>

<span data-ttu-id="71559-169">En el ejemplo de tutorial de hello, agregar un registro a para el dominio raíz de hello (por ejemplo, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="71559-169">In hello tutorial example, you add an A record for hello root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a><span data-ttu-id="71559-170">Copie la dirección IP de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="71559-170">Copy hello app's IP address</span></span>

<span data-ttu-id="71559-171">toomap un registro, necesita la dirección IP externa de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="71559-171">toomap an A record, you need hello app's external IP address.</span></span> <span data-ttu-id="71559-172">Puede encontrar esta dirección IP en la aplicación hello **los dominios personalizados** página Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="71559-172">You can find this IP address in hello app's **Custom domains** page in hello Azure portal.</span></span>

<span data-ttu-id="71559-173">Hola dejado de navegación de página de la aplicación Hola Hola portal de Azure, seleccione **los dominios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="71559-173">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menú Dominio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="71559-175">Hola **los dominios personalizados** página, copie la dirección IP de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="71559-175">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a><span data-ttu-id="71559-177">Crear registro Hola</span><span class="sxs-lookup"><span data-stu-id="71559-177">Create hello A record</span></span>

<span data-ttu-id="71559-178">toomap un registro tooan aplicación, servicio de aplicaciones requiere **dos** registros DNS:</span><span class="sxs-lookup"><span data-stu-id="71559-178">toomap an A record tooan app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="71559-179">Un **A** registrar la dirección IP de la aplicación de toomap toohello.</span><span class="sxs-lookup"><span data-stu-id="71559-179">An **A** record toomap toohello app's IP address.</span></span>
- <span data-ttu-id="71559-180">A **TXT** registrar el nombre de host de la aplicación de toomap toohello predeterminado `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="71559-180">A **TXT** record toomap toohello app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="71559-181">Servicio de aplicaciones usa este registro solo durante la configuración, tooverify que posee el dominio personalizado de Hola.</span><span class="sxs-lookup"><span data-stu-id="71559-181">App Service uses this record only at configuration time, tooverify that you own hello custom domain.</span></span> <span data-ttu-id="71559-182">Después de que el dominio personalizado se valida y se configura en App Service, puede eliminar el registro TXT.</span><span class="sxs-lookup"><span data-stu-id="71559-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="71559-183">Para hello `contoso.com` ejemplo de un dominio, crear registros de A y TXT Hola según toohello en la tabla siguiente (`@` normalmente representa Hola dominio raíz).</span><span class="sxs-lookup"><span data-stu-id="71559-183">For hello `contoso.com` domain example, create hello A and TXT records according toohello following table (`@` typically represents hello root domain).</span></span> 

| <span data-ttu-id="71559-184">Tipo de registro</span><span class="sxs-lookup"><span data-stu-id="71559-184">Record type</span></span> | <span data-ttu-id="71559-185">Host</span><span class="sxs-lookup"><span data-stu-id="71559-185">Host</span></span> | <span data-ttu-id="71559-186">Valor</span><span class="sxs-lookup"><span data-stu-id="71559-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="71559-187">Una </span><span class="sxs-lookup"><span data-stu-id="71559-187">A</span></span> | `@` | <span data-ttu-id="71559-188">Dirección IP de [dirección IP de la aplicación de copia Hola](#info)</span><span class="sxs-lookup"><span data-stu-id="71559-188">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="71559-189">TXT</span><span class="sxs-lookup"><span data-stu-id="71559-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="71559-190">Cuando se agregan registros hello, Hola página de registros DNS es similar a Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="71559-190">When hello records are added, hello DNS records page looks like hello following example:</span></span>

![Página de registros DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a><span data-ttu-id="71559-192">Habilitar una asignación de registro de la aplicación hello Hola</span><span class="sxs-lookup"><span data-stu-id="71559-192">Enable hello A record mapping in hello app</span></span>

<span data-ttu-id="71559-193">En la aplicación hello **los dominios personalizados** página Hola portal de Azure, agregue Hola personalizado nombre DNS completo (por ejemplo, `contoso.com`) toohello lista.</span><span class="sxs-lookup"><span data-stu-id="71559-193">Back in hello app's **Custom domains** page in hello Azure portal, add hello fully qualified custom DNS name (for example, `contoso.com`) toohello list.</span></span>

<span data-ttu-id="71559-194">Seleccione hello  **+**  icono siguiente demasiado**Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="71559-194">Select hello **+** icon next too**Add hostname**.</span></span>

![Agregar nombre de host](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="71559-196">Nombre de dominio completo de tipo hello que ha configurado como registro de hello A, `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="71559-196">Type hello fully qualified domain name that you configured hello A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="71559-197">Seleccione **Validar**.</span><span class="sxs-lookup"><span data-stu-id="71559-197">Select **Validate**.</span></span>

<span data-ttu-id="71559-198">Hola **Agregar nombre de host** se activa el botón.</span><span class="sxs-lookup"><span data-stu-id="71559-198">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="71559-199">Asegúrese de que **tipo de registro de nombre de host** se establece demasiado**un registro (ejemplo.com)**.</span><span class="sxs-lookup"><span data-stu-id="71559-199">Make sure that **Hostname record type** is set too**A record (example.com)**.</span></span>

<span data-ttu-id="71559-200">Seleccione **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="71559-200">Select **Add hostname**.</span></span>

![Agregar aplicación de toohello de nombre DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="71559-202">Puede tardar algún tiempo Hola nuevo nombre de host toobe reflejado en la aplicación hello **los dominios personalizados** página.</span><span class="sxs-lookup"><span data-stu-id="71559-202">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="71559-203">Intente actualizar los datos de saludo explorador tooupdate Hola.</span><span class="sxs-lookup"><span data-stu-id="71559-203">Try refreshing hello browser tooupdate hello data.</span></span>

![Registro D agregado](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="71559-205">Si falta un paso o cometió un alguna versión anterior, verá un error de comprobación en parte inferior de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="71559-205">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Error de comprobación](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="71559-207">Asignar un dominio con caracteres comodín</span><span class="sxs-lookup"><span data-stu-id="71559-207">Map a wildcard domain</span></span>

<span data-ttu-id="71559-208">En el ejemplo de tutorial de hello, asigne un [nombre DNS de carácter comodín](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (por ejemplo, `*.contoso.com`) toohello aplicación de servicio de aplicaciones mediante la adición de un registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="71559-208">In hello tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) toohello App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="71559-209">Crear registro CNAME Hola</span><span class="sxs-lookup"><span data-stu-id="71559-209">Create hello CNAME record</span></span>

<span data-ttu-id="71559-210">Agregar un toomap registro CNAME en el nombre de host de la aplicación toohello de nombre de carácter comodín predeterminado (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="71559-210">Add a CNAME record toomap a wildcard name toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="71559-211">Para hello `*.contoso.com` ejemplo de un dominio, Hola registro CNAME asignará el nombre de hello `*` demasiado`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="71559-211">For hello `*.contoso.com` domain example, hello CNAME record will map hello name `*` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="71559-212">Cuando se agrega Hola CNAME, Hola página de registros DNS es similar a Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="71559-212">When hello CNAME is added, hello DNS records page looks like hello following example:</span></span>

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a><span data-ttu-id="71559-214">Habilitar asignación de registro CNAME de hello en la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="71559-214">Enable hello CNAME record mapping in hello app</span></span>

<span data-ttu-id="71559-215">Ahora puede agregar cualquier subdominio que coincida con la aplicación de hello comodín nombre toohello (por ejemplo, `sub1.contoso.com` y `sub2.contoso.com` coincide con `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="71559-215">You can now add any subdomain that matches hello wildcard name toohello app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="71559-216">Hola dejado de navegación de página de la aplicación Hola Hola portal de Azure, seleccione **los dominios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="71559-216">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menú Dominio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="71559-218">Seleccione hello  **+**  icono siguiente demasiado**Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="71559-218">Select hello **+** icon next too**Add hostname**.</span></span>

![Agregar nombre de host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="71559-220">Escriba un nombre de dominio completo que coincide con el dominio de hello comodín (por ejemplo, `sub1.contoso.com`) y, a continuación, seleccione **validar**.</span><span class="sxs-lookup"><span data-stu-id="71559-220">Type a fully qualified domain name that matches hello wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="71559-221">Hola **Agregar nombre de host** se activa el botón.</span><span class="sxs-lookup"><span data-stu-id="71559-221">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="71559-222">Asegúrese de que **tipo de registro de nombre de host** se establece demasiado**registro CNAME (www.example.com o cualquier subdominio)**.</span><span class="sxs-lookup"><span data-stu-id="71559-222">Make sure that **Hostname record type** is set too**CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="71559-223">Seleccione **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="71559-223">Select **Add hostname**.</span></span>

![Agregar aplicación de toohello de nombre DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="71559-225">Puede tardar algún tiempo Hola nuevo nombre de host toobe reflejado en la aplicación hello **los dominios personalizados** página.</span><span class="sxs-lookup"><span data-stu-id="71559-225">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="71559-226">Intente actualizar los datos de saludo explorador tooupdate Hola.</span><span class="sxs-lookup"><span data-stu-id="71559-226">Try refreshing hello browser tooupdate hello data.</span></span>

<span data-ttu-id="71559-227">Seleccione hello  **+**  icono nuevo tooadd otro nombre de host que coincide con el dominio comodín Hola.</span><span class="sxs-lookup"><span data-stu-id="71559-227">Select hello **+** icon again tooadd another hostname that matches hello wildcard domain.</span></span> <span data-ttu-id="71559-228">Por ejemplo, agregue `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="71559-228">For example, add `sub2.contoso.com`.</span></span>

![Registro CNAME agregado](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="71559-230">Probar en el explorador</span><span class="sxs-lookup"><span data-stu-id="71559-230">Test in browser</span></span>

<span data-ttu-id="71559-231">Examinar toohello nombres DNS que configuró anteriormente (por ejemplo, `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, y `sub2.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="71559-231">Browse toohello DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="71559-233">Automatizar con scripts</span><span class="sxs-lookup"><span data-stu-id="71559-233">Automate with scripts</span></span>

<span data-ttu-id="71559-234">Se puede automatizar la administración de dominios personalizados con secuencias de comandos, mediante hello [CLI de Azure](/cli/azure/install-azure-cli) o [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="71559-234">You can automate management of custom domains with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="71559-235">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="71559-235">Azure CLI</span></span> 

<span data-ttu-id="71559-236">Hola siguiente comando agrega un tooan de nombre DNS personalizado configurado aplicación de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="71559-236">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="71559-237">Para obtener más información, consulte [asignar una aplicación web de tooa de dominio personalizado](scripts/app-service-cli-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="71559-237">For more information, see [Map a custom domain tooa web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="71559-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="71559-238">Azure PowerShell</span></span> 

<span data-ttu-id="71559-239">Hola siguiente comando agrega un tooan de nombre DNS personalizado configurado aplicación de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="71559-239">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="71559-240">Para obtener más información, consulte [asignar una aplicación web de tooa de dominio personalizado](scripts/app-service-powershell-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="71559-240">For more information, see [Assign a custom domain tooa web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="71559-241">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="71559-241">Next steps</span></span>

<span data-ttu-id="71559-242">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="71559-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="71559-243">Asignar un subdominio mediante el uso de un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="71559-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="71559-244">Asignar un dominio raíz mediante el uso de un registro D</span><span class="sxs-lookup"><span data-stu-id="71559-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="71559-245">Asignar un dominio con comodín mediante el uso de un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="71559-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="71559-246">Automatizar la asignación de dominio con scripts</span><span class="sxs-lookup"><span data-stu-id="71559-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="71559-247">Avanzar toohello siguiente tutorial toolearn cómo toobind un personalizado SSL certificate tooa web app.</span><span class="sxs-lookup"><span data-stu-id="71559-247">Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="71559-248">Enlazar un tooAzure de certificado SSL personalizado aplicaciones Web existente</span><span class="sxs-lookup"><span data-stu-id="71559-248">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
