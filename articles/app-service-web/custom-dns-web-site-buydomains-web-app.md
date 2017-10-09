---
title: aaaBuy un nombre de dominio personalizado para aplicaciones Web de Azure
description: "Obtenga información acerca de cómo el nombre de toobuy un dominio personalizado con una aplicación web en el servicio de aplicaciones de Azure."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="4919b-103">Comprar un nombre de dominio personalizado para Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="4919b-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="4919b-104">Los dominios de App Service (versión preliminar) son dominios de nivel superior que se administran directamente en Azure.</span><span class="sxs-lookup"><span data-stu-id="4919b-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="4919b-105">Hacen que los dominios personalizados fácil toomanage [aplicaciones Web de Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4919b-105">They make it easy toomanage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="4919b-106">Este tutorial muestra cómo toobuy un dominio de servicio de aplicaciones y asigne DNS nombres tooAzure las aplicaciones Web.</span><span class="sxs-lookup"><span data-stu-id="4919b-106">This tutorial shows you how toobuy an App Service domain and assign DNS names tooAzure Web Apps.</span></span>

<span data-ttu-id="4919b-107">Este artículo trata sobre Azure App Service (Web Apps, API Apps, Mobile Apps y Logic Apps).</span><span class="sxs-lookup"><span data-stu-id="4919b-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="4919b-108">Para la máquina virtual de Azure o el almacenamiento de Azure, consulte [tooAzure de dominio de servicio de aplicaciones asignar VM o almacenamiento de Azure](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span><span class="sxs-lookup"><span data-stu-id="4919b-108">For Azure VM or Azure Storage, see [Assign App Service domain tooAzure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="4919b-109">Para Cloud Services, vea [Configuración de un nombre de dominio personalizado para un servicio en la nube de Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4919b-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4919b-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4919b-110">Prerequisites</span></span>

<span data-ttu-id="4919b-111">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="4919b-111">toocomplete this tutorial:</span></span>

* <span data-ttu-id="4919b-112">[Cree una aplicación de App Service](/azure/app-service/) o use alguna aplicación que haya creado para otro tutorial.</span><span class="sxs-lookup"><span data-stu-id="4919b-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="prepare-hello-app"></a><span data-ttu-id="4919b-113">Preparar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="4919b-113">Prepare hello app</span></span>

<span data-ttu-id="4919b-114">toouse dominios personalizados en aplicaciones Web de Azure, la aplicación web [plan de servicio de aplicaciones](https://azure.microsoft.com/pricing/details/app-service/) debe ser una capa de pagada (**Shared**, **básica**, **estándar**, o **Premium**).</span><span class="sxs-lookup"><span data-stu-id="4919b-114">toouse custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="4919b-115">En este paso, asegúrese de que dicha aplicación hello es Hola admitido nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="4919b-115">In this step, you make sure that hello web app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="4919b-116">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="4919b-116">Sign in tooAzure</span></span>

<span data-ttu-id="4919b-117">Abra hello [portal de Azure](https://portal.azure.com) e inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="4919b-117">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="4919b-118">Navegue toohello aplicación Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4919b-118">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="4919b-119">En el menú izquierdo de hello, seleccione **servicios de aplicaciones**y, a continuación, seleccione nombre de Hola de aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="4919b-119">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="4919b-121">Verá que la página de administración de Hola de hello aplicación de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4919b-121">You see hello management page of hello App Service app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="4919b-122">Hola de comprobación de nivel de precios</span><span class="sxs-lookup"><span data-stu-id="4919b-122">Check hello pricing tier</span></span>

<span data-ttu-id="4919b-123">Hola a la izquierda de la página de la aplicación hello, desplácese toohello **configuración** sección y seleccione **escalar verticalmente (plan de servicio de aplicaciones)**.</span><span class="sxs-lookup"><span data-stu-id="4919b-123">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menú Escalar verticalmente](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="4919b-125">nivel actual de la aplicación Hello aparece resaltado por un borde azul.</span><span class="sxs-lookup"><span data-stu-id="4919b-125">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="4919b-126">Compruebe que dicha aplicación hello no esté en hello toomake **libre** capa.</span><span class="sxs-lookup"><span data-stu-id="4919b-126">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="4919b-127">DNS personalizado no se admite en hello **libre** capa.</span><span class="sxs-lookup"><span data-stu-id="4919b-127">Custom DNS is not supported in hello **Free** tier.</span></span> 

![Comprobar plan de tarifa](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="4919b-129">Si hello plan de servicio de aplicaciones no es **libre**, cierre hello **elegir el nivel de precios** página y omitir demasiado[dominio Hola de compra](#buy-the-domain).</span><span class="sxs-lookup"><span data-stu-id="4919b-129">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Buy hello domain](#buy-the-domain).</span></span>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="4919b-130">Escalar verticalmente Hola plan de servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4919b-130">Scale up hello App Service plan</span></span>

<span data-ttu-id="4919b-131">Seleccione cualquiera de los niveles de hello no disponibles (**Shared**, **básica**, **estándar**, o **Premium**).</span><span class="sxs-lookup"><span data-stu-id="4919b-131">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="4919b-132">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="4919b-132">Click **Select**.</span></span>

![Comprobar plan de tarifa](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="4919b-134">Cuando vea Hola siguientes a la notificación, la operación de escalado de hello está completa.</span><span class="sxs-lookup"><span data-stu-id="4919b-134">When you see hello following notification, hello scale operation is complete.</span></span>

![Confirmación de la operación de escalado](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a><span data-ttu-id="4919b-136">Comprar Hola dominio</span><span class="sxs-lookup"><span data-stu-id="4919b-136">Buy hello domain</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="4919b-137">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="4919b-137">Sign in tooAzure</span></span>
<span data-ttu-id="4919b-138">Abra hello [portal de Azure](https://portal.azure.com/) e inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="4919b-138">Open hello [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="4919b-139">Iniciar Comprar dominios</span><span class="sxs-lookup"><span data-stu-id="4919b-139">Launch Buy domains</span></span>
<span data-ttu-id="4919b-140">Hola **aplicaciones Web** , haga clic en nombre de saludo de la aplicación web, seleccione **configuración**y, a continuación, seleccione **los dominios personalizados**</span><span class="sxs-lookup"><span data-stu-id="4919b-140">In hello **Web Apps** tab, click hello name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="4919b-141">Hola **los dominios personalizados** página, haga clic en **comprar dominios**.</span><span class="sxs-lookup"><span data-stu-id="4919b-141">In hello **Custom domains** page, click **Buy domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a><span data-ttu-id="4919b-142">Configurar la compra de dominio Hola</span><span class="sxs-lookup"><span data-stu-id="4919b-142">Configure hello domain purchase</span></span>

<span data-ttu-id="4919b-143">Hola **dominio de aplicación de servicio** página Hola **Buscar dominio** cuadro, nombre de dominio de tipo hello desea toobuy y el tipo de `Enter`.</span><span class="sxs-lookup"><span data-stu-id="4919b-143">In hello **App Service Domain** page, in hello **Search for domain** box, type hello domain name you want toobuy and type `Enter`.</span></span> <span data-ttu-id="4919b-144">Hello sugeridos dominios disponibles aparecen justo debajo de cuadro de texto de Hola.</span><span class="sxs-lookup"><span data-stu-id="4919b-144">hello suggested available domains are shown just below hello text box.</span></span> <span data-ttu-id="4919b-145">Seleccione uno o varios dominios que desee toobuy.</span><span class="sxs-lookup"><span data-stu-id="4919b-145">Select one or more domains you want toobuy.</span></span> 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

<span data-ttu-id="4919b-146">Haga clic en hello **información de contacto** y rellene el formulario de información de contacto del dominio Hola.</span><span class="sxs-lookup"><span data-stu-id="4919b-146">Click hello **Contact Information** and fill out hello domain's contact information form.</span></span> <span data-ttu-id="4919b-147">Cuando termine, haga clic en **Aceptar** página de dominio de aplicación de servicio de tooreturn toohello.</span><span class="sxs-lookup"><span data-stu-id="4919b-147">When finished, click **OK** tooreturn toohello App Service Domain page.</span></span>
   
<span data-ttu-id="4919b-148">Es importante que rellene todos los campos obligatorios con la mayor precisión posible.</span><span class="sxs-lookup"><span data-stu-id="4919b-148">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="4919b-149">Dominios de error toopurchase pueden producir datos incorrectos para la información de contacto.</span><span class="sxs-lookup"><span data-stu-id="4919b-149">Incorrect data for contact information can result in failure toopurchase domains.</span></span> 

<span data-ttu-id="4919b-150">A continuación, seleccione opciones de hello deseado para el dominio.</span><span class="sxs-lookup"><span data-stu-id="4919b-150">Next, select hello desired options for your domain.</span></span> <span data-ttu-id="4919b-151">Vea Hola para obtener una explicación en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="4919b-151">See hello following table for explanations:</span></span>

| <span data-ttu-id="4919b-152">Configuración</span><span class="sxs-lookup"><span data-stu-id="4919b-152">Setting</span></span> | <span data-ttu-id="4919b-153">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="4919b-153">Suggested Value</span></span> | <span data-ttu-id="4919b-154">Descripción</span><span class="sxs-lookup"><span data-stu-id="4919b-154">Description</span></span> |
|-|-|-|
|<span data-ttu-id="4919b-155">Renovación automática</span><span class="sxs-lookup"><span data-stu-id="4919b-155">Auto renew</span></span> | <span data-ttu-id="4919b-156">**Habilitación**</span><span class="sxs-lookup"><span data-stu-id="4919b-156">**Enable**</span></span> | <span data-ttu-id="4919b-157">Renueva automáticamente el dominio de App Service cada año.</span><span class="sxs-lookup"><span data-stu-id="4919b-157">Renews your App Service Domain automatically every year.</span></span> <span data-ttu-id="4919b-158">La tarjeta de crédito se cobra Hola mismo precio de compra en tiempo de Hola de renovación.</span><span class="sxs-lookup"><span data-stu-id="4919b-158">Your credit card is charged hello same purchase price at hello time of renewal.</span></span> |
|<span data-ttu-id="4919b-159">Protección de la privacidad</span><span class="sxs-lookup"><span data-stu-id="4919b-159">Privacy protection</span></span> | <span data-ttu-id="4919b-160">Habilitar</span><span class="sxs-lookup"><span data-stu-id="4919b-160">Enable</span></span> | <span data-ttu-id="4919b-161">Participar en demasiado "Protección de la privacidad", que se incluye en el precio de compra de hello _gratuitamente_ (excepto para los dominios de nivel superior cuyo registro no admiten la protección de la privacidad, como _. co.in_, _. Co.uk_, y así sucesivamente).</span><span class="sxs-lookup"><span data-stu-id="4919b-161">Opt in too"Privacy protection", which is included in hello purchase price _for free_ (except for top-level domains whose registry do not support privacy protection, such as _.co.in_, _.co.uk_, and so on).</span></span> |
| <span data-ttu-id="4919b-162">Asignar nombres de host predeterminados</span><span class="sxs-lookup"><span data-stu-id="4919b-162">Assign default hostnames</span></span> | <span data-ttu-id="4919b-163">**www** y **@**</span><span class="sxs-lookup"><span data-stu-id="4919b-163">**www** and **@**</span></span> | <span data-ttu-id="4919b-164">Seleccione Hola deseado enlaces de nombre de host, si lo desea.</span><span class="sxs-lookup"><span data-stu-id="4919b-164">Select hello desired hostname bindings, if desired.</span></span> <span data-ttu-id="4919b-165">Cuando se completa la operación de compra de dominio de hello, la aplicación web puede tener acceso en los nombres de host de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="4919b-165">When hello domain purchase operation is complete, your web app can be accessed at hello selected hostnames.</span></span> <span data-ttu-id="4919b-166">Si la aplicación de hello web está detrás de [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), no ve el dominio raíz Hola de hello opción tooassign (@), ya que el Administrador de tráfico no no registros a soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="4919b-166">If hello web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see hello option tooassign hello root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="4919b-167">Puede realizar cambios en las asignaciones de nombre de host toohello una vez completada la compra de dominio Hola.</span><span class="sxs-lookup"><span data-stu-id="4919b-167">You can make changes toohello hostname assignments after hello domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="4919b-168">Aceptar los términos y comprar</span><span class="sxs-lookup"><span data-stu-id="4919b-168">Accept terms and purchase</span></span>

<span data-ttu-id="4919b-169">Haga clic en **condiciones legales** tooreview términos de Hola y cargos de hello, a continuación, haga clic en **comprar**.</span><span class="sxs-lookup"><span data-stu-id="4919b-169">Click **Legal Terms** tooreview hello terms and hello charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="4919b-170">Los dominios de servicio de aplicaciones utilizan dominios de DNS de Azure toohost Hola.</span><span class="sxs-lookup"><span data-stu-id="4919b-170">App Service Domains use Azure DNS toohost hello domains.</span></span> <span data-ttu-id="4919b-171">Además toohello dominio la inscripción, aplicarán cargos de uso de DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="4919b-171">In addition toohello domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="4919b-172">Para obtener más información, vea [DNS de Azure Precios](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="4919b-172">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="4919b-173">Nuevo en hello **dominio de aplicación de servicio** página, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4919b-173">Back in hello **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="4919b-174">Mientras está en curso la operación de hello, vea Hola siguientes notificaciones:</span><span class="sxs-lookup"><span data-stu-id="4919b-174">While hello operation is in progress, you see hello following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="4919b-175">Nombres de host de prueba Hola</span><span class="sxs-lookup"><span data-stu-id="4919b-175">Test hello hostnames</span></span>

<span data-ttu-id="4919b-176">Si ha asignado la aplicación web de forma predeterminada los nombres de host tooyour, verá una notificación de éxito para cada nombre de host seleccionado.</span><span class="sxs-lookup"><span data-stu-id="4919b-176">If you have assigned default hostnames tooyour web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="4919b-177">También verá los nombres de host seleccionado de Hola Hola **los dominios personalizados** página Hola **los nombres de host** sección.</span><span class="sxs-lookup"><span data-stu-id="4919b-177">You also see hello selected hostnames in hello **Custom domains** page, in hello **Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="4919b-178">nombres de host de hello tootest, navegue toohello muestran los nombres de host en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="4919b-178">tootest hello hostnames, navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="4919b-179">En el ejemplo de Hola Hola anterior captura de pantalla, intente navegar too_kontoso.net_ y _www.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="4919b-179">In hello example in hello preceding screenshot, try navigating too_kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-tooweb-app"></a><span data-ttu-id="4919b-180">Asignar nombres de host tooweb aplicación</span><span class="sxs-lookup"><span data-stu-id="4919b-180">Assign hostnames tooweb app</span></span>

<span data-ttu-id="4919b-181">Si elige no tooassign uno o más de forma predeterminada los nombres de host tooyour web app durante Hola proceso de compra, o si necesita un nombre de host tooassign no aparece, puede asignar un nombre de host en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="4919b-181">If you choose not tooassign one or more default hostnames tooyour web app during hello purchase process, or if you need tooassign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="4919b-182">También puede asignar nombres de host en hello tooany de dominio de aplicación de servicio de otra aplicación web.</span><span class="sxs-lookup"><span data-stu-id="4919b-182">You can also assign hostnames in hello App Service Domain tooany other web app.</span></span> <span data-ttu-id="4919b-183">Hello pasos dependen de si Hola dominio de aplicación de servicio y aplicación web de hello pertenecen toohello misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="4919b-183">hello steps depend on whether hello App Service Domain and hello web app belong toohello same subscription.</span></span>

- <span data-ttu-id="4919b-184">Otra suscripción: asignar los registros DNS personalizados de dominio de aplicación de servicio de aplicación web hello toohello como un dominio externamente adquirido.</span><span class="sxs-lookup"><span data-stu-id="4919b-184">Different subscription: Map custom DNS records from hello App Service Domain toohello web app like an externally purchased domain.</span></span> <span data-ttu-id="4919b-185">Para obtener información acerca de DNS personalizado agregar nombres tooan dominio de aplicación de servicio, consulte [administrar registros DNS personalizados](#custom).</span><span class="sxs-lookup"><span data-stu-id="4919b-185">For information on adding custom DNS names tooan App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="4919b-186">toomap una aplicación web de tooa dominio adquiridas externo, vea [asignar un tooAzure de nombre DNS personalizado existente aplicaciones Web](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="4919b-186">toomap an external purchased domain tooa web app, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="4919b-187">Misma suscripción: Hola uso pasos.</span><span class="sxs-lookup"><span data-stu-id="4919b-187">Same subscription: Use hello following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="4919b-188">Iniciar Agregar nombre de host</span><span class="sxs-lookup"><span data-stu-id="4919b-188">Launch add hostname</span></span>
<span data-ttu-id="4919b-189">Hola **servicios de aplicaciones** página, el nombre de hello select de la aplicación web que desee tooassign los nombres de host, seleccione **configuración**y, a continuación, seleccione **los dominios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="4919b-189">In hello **App Services** page, select hello name of your web app that you want tooassign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="4919b-190">Asegúrese de que su dominio adquirida en hello **dominios del servicio de aplicación** sección, pero no seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="4919b-190">Make sure that your purchased domain is listed in hello **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="4919b-191">Todos los dominios de servicio de aplicación Hola misma suscripción se muestran en la aplicación web de hello **los dominios personalizados** página.</span><span class="sxs-lookup"><span data-stu-id="4919b-191">All App Service Domains in hello same subscription are shown in hello web app's **Custom domains** page.</span></span> <span data-ttu-id="4919b-192">Si el dominio está en la suscripción de la aplicación de hello web, pero no puede verlo en la aplicación web de hello **los dominios personalizados** página, intente volver a abrir hello **los dominios personalizados** página o actualice la página Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="4919b-192">If your domain is in hello web app's subscription, but you cannot see it in hello web app's **Custom domains** page, try reopening hello **Custom domains** page or refresh hello webpage.</span></span> <span data-ttu-id="4919b-193">Además, compruebe la campana de notificación Hola princip Hola de hello portal de Azure para errores de progreso o de creación.</span><span class="sxs-lookup"><span data-stu-id="4919b-193">Also, check hello notification bell at hello top of hello Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="4919b-194">Seleccione **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="4919b-194">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="4919b-195">Configurar el nombre de host</span><span class="sxs-lookup"><span data-stu-id="4919b-195">Configure hostname</span></span>
<span data-ttu-id="4919b-196">Hola **Agregar nombre de host** cuadro de diálogo, escribe el nombre de dominio completo de Hola de su dominio de aplicación de servicio o cualquier subdominio.</span><span class="sxs-lookup"><span data-stu-id="4919b-196">In hello **Add hostname** dialog, type hello fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="4919b-197">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4919b-197">For example:</span></span>

- <span data-ttu-id="4919b-198">kontoso.net</span><span class="sxs-lookup"><span data-stu-id="4919b-198">kontoso.net</span></span>
- <span data-ttu-id="4919b-199">www.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="4919b-199">www.kontoso.net</span></span>
- <span data-ttu-id="4919b-200">abc.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="4919b-200">abc.kontoso.net</span></span>

<span data-ttu-id="4919b-201">Cuando termine, seleccione **Validar**.</span><span class="sxs-lookup"><span data-stu-id="4919b-201">When finished, select **Validate**.</span></span> <span data-ttu-id="4919b-202">tipo de registro de nombre de host de Hola se selecciona automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4919b-202">hello hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="4919b-203">Seleccione **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="4919b-203">Select **Add hostname**.</span></span>

<span data-ttu-id="4919b-204">Cuando se completa la operación de hello, verá una notificación de éxito para hello asigna el nombre de host.</span><span class="sxs-lookup"><span data-stu-id="4919b-204">When hello operation is complete, you see a success notification for hello assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="4919b-205">Cerrar Agregar nombre de host</span><span class="sxs-lookup"><span data-stu-id="4919b-205">Close add hostname</span></span>
<span data-ttu-id="4919b-206">Hola **Agregar nombre de host** página, asignar cualquier otro nombre de host tooyour aplicación web, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4919b-206">In hello **Add hostname** page, assign any other hostname tooyour web app, as desired.</span></span> <span data-ttu-id="4919b-207">Cuando haya terminado, cierre hello **Agregar nombre de host** página.</span><span class="sxs-lookup"><span data-stu-id="4919b-207">When finished, close hello **Add hostname** page.</span></span>

<span data-ttu-id="4919b-208">Ahora debería ver Hola acaban de asignar hostname(s) en la aplicación **los dominios personalizados** página.</span><span class="sxs-lookup"><span data-stu-id="4919b-208">You should now see hello newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="4919b-209">Nombres de host de prueba Hola</span><span class="sxs-lookup"><span data-stu-id="4919b-209">Test hello hostnames</span></span>

<span data-ttu-id="4919b-210">Navegar por los nombres de host toohello aparece en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="4919b-210">Navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="4919b-211">En el ejemplo de Hola Hola anterior captura de pantalla, pruebe a navegar por too_abc.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="4919b-211">In hello example in hello preceding screenshot, try navigating too_abc.kontoso.net_.</span></span>

<a name="custom" />

## <a name="manage-custom-dns-records"></a><span data-ttu-id="4919b-212">Administrar los registros DNS personalizados</span><span class="sxs-lookup"><span data-stu-id="4919b-212">Manage custom DNS records</span></span>

<span data-ttu-id="4919b-213">En Azure, los registros DNS para un dominio de App Service se administran mediante [DNS de Azure](https://azure.microsoft.com/services/dns/).</span><span class="sxs-lookup"><span data-stu-id="4919b-213">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="4919b-214">Puede agregar, quitar y actualizar los registros DNS, al igual que para un dominio comprado de forma externa.</span><span class="sxs-lookup"><span data-stu-id="4919b-214">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="4919b-215">Abrir Dominio de App Service</span><span class="sxs-lookup"><span data-stu-id="4919b-215">Open App Service Domain</span></span>

<span data-ttu-id="4919b-216">En el portal de Azure, desde el menú de la izquierda, Hola Hola seleccione **más servicios** > **dominios de aplicación de servicio**.</span><span class="sxs-lookup"><span data-stu-id="4919b-216">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="4919b-217">Seleccione Hola dominio toomanage.</span><span class="sxs-lookup"><span data-stu-id="4919b-217">Select hello domain toomanage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="4919b-218">Obtener acceso a la zona DNS</span><span class="sxs-lookup"><span data-stu-id="4919b-218">Access DNS zone</span></span>

<span data-ttu-id="4919b-219">En el menú de la izquierda del dominio hello, seleccione **zona DNS**.</span><span class="sxs-lookup"><span data-stu-id="4919b-219">In hello domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="4919b-220">Esta acción abre hello [zona DNS](../dns/dns-zones-records.md) página de su dominio de aplicación de servicio en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="4919b-220">This action opens hello [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="4919b-221">Para obtener información acerca de cómo tooedit los registros DNS, consulte [cómo toomanage zonas de DNS en Hola portal de Azure](../dns/dns-operations-dnszones-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4919b-221">For information on how tooedit DNS records, see [How toomanage DNS Zones in hello Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="4919b-222">Cancelar la compra (eliminar el dominio)</span><span class="sxs-lookup"><span data-stu-id="4919b-222">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="4919b-223">Después de adquirir Hola dominio de aplicación de servicio, tendrá cinco días toocancel la compra para obtener un reembolso completo.</span><span class="sxs-lookup"><span data-stu-id="4919b-223">After you purchase hello App Service Domain, you have five days toocancel your purchase for a full refund.</span></span> <span data-ttu-id="4919b-224">Después de cinco días, puede eliminar Hola dominio de aplicación de servicio, pero no puede recibir un reembolso.</span><span class="sxs-lookup"><span data-stu-id="4919b-224">After five days, you can delete hello App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="4919b-225">Abrir Dominio de App Service</span><span class="sxs-lookup"><span data-stu-id="4919b-225">Open App Service Domain</span></span>

<span data-ttu-id="4919b-226">En el portal de Azure, desde el menú de la izquierda, Hola Hola seleccione **más servicios** > **dominios de aplicación de servicio**.</span><span class="sxs-lookup"><span data-stu-id="4919b-226">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="4919b-227">Hola seleccione dominio tooyou desea toocancel o eliminar.</span><span class="sxs-lookup"><span data-stu-id="4919b-227">Select hello domain tooyou want toocancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="4919b-228">Eliminación de enlaces de nombre de host</span><span class="sxs-lookup"><span data-stu-id="4919b-228">Delete hostname bindings</span></span>

<span data-ttu-id="4919b-229">En el menú de la izquierda del dominio hello, seleccione **enlaces de nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="4919b-229">In hello domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="4919b-230">aquí se muestran los enlaces de nombre de host de Hola de todos los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="4919b-230">hello hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="4919b-231">No se puede eliminar Hola dominio de aplicación de servicio hasta que se eliminen todos los enlaces de nombre de host.</span><span class="sxs-lookup"><span data-stu-id="4919b-231">You cannot delete hello App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="4919b-232">Para eliminar todos los enlaces de nombre de host, seleccione **...** > **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="4919b-232">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="4919b-233">Después de eliminarán todos los enlaces de hello, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="4919b-233">After all hello bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="4919b-234">Cancelar o eliminar</span><span class="sxs-lookup"><span data-stu-id="4919b-234">Cancel or delete</span></span>

<span data-ttu-id="4919b-235">En el menú de la izquierda del dominio hello, seleccione **Introducción**.</span><span class="sxs-lookup"><span data-stu-id="4919b-235">In hello domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="4919b-236">Si no ha transcurrido el período de cancelación de hello en el dominio de hello adquirida, seleccione **Cancelar compra**.</span><span class="sxs-lookup"><span data-stu-id="4919b-236">If hello cancellation period on hello purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="4919b-237">De lo contrario, en su lugar verá el botón **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="4919b-237">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="4919b-238">dominio de hello toodelete sin un reembolso, seleccione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="4919b-238">toodelete hello domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="4919b-239">Seleccione **Aceptar** operación de hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="4919b-239">Select **OK** tooconfirm hello operation.</span></span> <span data-ttu-id="4919b-240">Si no desea tooproceed, haga clic en cualquier lugar fuera del cuadro de diálogo de confirmación de Hola.</span><span class="sxs-lookup"><span data-stu-id="4919b-240">If you don't want tooproceed, click anywhere outside of hello confirmation dialog.</span></span>

<span data-ttu-id="4919b-241">Una vez completada la operación de hello, dominio hello es publicadas desde su suscripción y están disponibles para todo aquel que toopurchase de nuevo.</span><span class="sxs-lookup"><span data-stu-id="4919b-241">After hello operation is complete, hello domain is released from your subscription and available for anyone toopurchase again.</span></span> 
