---
title: Comprar un nombre de dominio personalizado para Azure Web Apps
description: "Obtenga información sobre cómo comprar un nombre de dominio personalizado con una aplicación web en Azure App Service."
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
ms.openlocfilehash: 3cb22b935624041ab51e64028a1b668fd694f9b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="90b0f-103">Comprar un nombre de dominio personalizado para Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="90b0f-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="90b0f-104">Los dominios de App Service (versión preliminar) son dominios de nivel superior que se administran directamente en Azure.</span><span class="sxs-lookup"><span data-stu-id="90b0f-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="90b0f-105">Facilitan la administración de dominios personalizados para [Azure Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="90b0f-105">They make it easy to manage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="90b0f-106">En este tutorial se muestra cómo comprar un dominio de App Service y asignar nombres DNS a Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="90b0f-106">This tutorial shows you how to buy an App Service domain and assign DNS names to Azure Web Apps.</span></span>

<span data-ttu-id="90b0f-107">Este artículo trata sobre Azure App Service (Web Apps, API Apps, Mobile Apps y Logic Apps).</span><span class="sxs-lookup"><span data-stu-id="90b0f-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="90b0f-108">Para Azure Virtual Machines o Azure Storage, vea [Assign App Service domain to Azure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/) (Asignación del dominio de App Service a Azure Virtual Machines o Azure Storage).</span><span class="sxs-lookup"><span data-stu-id="90b0f-108">For Azure VM or Azure Storage, see [Assign App Service domain to Azure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="90b0f-109">Para Cloud Services, vea [Configuración de un nombre de dominio personalizado para un servicio en la nube de Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="90b0f-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90b0f-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="90b0f-110">Prerequisites</span></span>

<span data-ttu-id="90b0f-111">Para completar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="90b0f-111">To complete this tutorial:</span></span>

* <span data-ttu-id="90b0f-112">[Cree una aplicación de App Service](/azure/app-service/) o use alguna aplicación que haya creado para otro tutorial.</span><span class="sxs-lookup"><span data-stu-id="90b0f-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="prepare-the-app"></a><span data-ttu-id="90b0f-113">Preparación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="90b0f-113">Prepare the app</span></span>

<span data-ttu-id="90b0f-114">Para usar dominios personalizados en Azure Web Apps, el [plan de App Service](https://azure.microsoft.com/pricing/details/app-service/) de la aplicación web debe ser un nivel de pago (**Compartido**, **Básico**, **Estándar** o **Premium**).</span><span class="sxs-lookup"><span data-stu-id="90b0f-114">To use custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="90b0f-115">En este paso, asegúrese de que la aplicación web se encuentra en el plan de tarifa admitido.</span><span class="sxs-lookup"><span data-stu-id="90b0f-115">In this step, you make sure that the web app is in the supported pricing tier.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="90b0f-116">Inicio de sesión en Azure</span><span class="sxs-lookup"><span data-stu-id="90b0f-116">Sign in to Azure</span></span>

<span data-ttu-id="90b0f-117">Abra [Azure Portal](https://portal.azure.com) e inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="90b0f-117">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-to-the-app-in-the-azure-portal"></a><span data-ttu-id="90b0f-118">Navegue hasta la aplicación en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="90b0f-118">Navigate to the app in the Azure portal</span></span>

<span data-ttu-id="90b0f-119">En el menú izquierdo, seleccione **App Services** y, después, el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="90b0f-119">From the left menu, select **App Services**, and then select the name of the app.</span></span>

![Navegación en el portal a la aplicación de Azure](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="90b0f-121">Consulte la página de administración de la aplicación de App Service.</span><span class="sxs-lookup"><span data-stu-id="90b0f-121">You see the management page of the App Service app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="90b0f-122">Comprobar el plan de tarifa</span><span class="sxs-lookup"><span data-stu-id="90b0f-122">Check the pricing tier</span></span>

<span data-ttu-id="90b0f-123">En el panel de navegación izquierdo de la página de la aplicación, desplácese hasta la sección **Configuración** y seleccione **Escalar verticalmente (plan de App Service)**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-123">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menú Escalar verticalmente](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="90b0f-125">El nivel actual de la aplicación aparece resaltado con un cuadro azul.</span><span class="sxs-lookup"><span data-stu-id="90b0f-125">The app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="90b0f-126">Asegúrese de que la aplicación web no está en el nivel **Gratis**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-126">Check to make sure that the app is not in the **Free** tier.</span></span> <span data-ttu-id="90b0f-127">No se admiten DNS personalizados en el nivel **Gratis**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-127">Custom DNS is not supported in the **Free** tier.</span></span> 

![Comprobar plan de tarifa](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="90b0f-129">Si el plan de App Service no es **Gratuito**, cierre la página **Elegir un plan de tarifa** y vaya a [Comprar un dominio](#buy-the-domain).</span><span class="sxs-lookup"><span data-stu-id="90b0f-129">If the App Service plan is not **Free**, close the **Choose your pricing tier** page and skip to [Buy the domain](#buy-the-domain).</span></span>

### <a name="scale-up-the-app-service-plan"></a><span data-ttu-id="90b0f-130">Escalado verticalmente del plan de App Service</span><span class="sxs-lookup"><span data-stu-id="90b0f-130">Scale up the App Service plan</span></span>

<span data-ttu-id="90b0f-131">Seleccione alguno de los niveles de pago (**Compartido**, **Básico**, **Estándar** o **Premium**).</span><span class="sxs-lookup"><span data-stu-id="90b0f-131">Select any of the non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="90b0f-132">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-132">Click **Select**.</span></span>

![Comprobar plan de tarifa](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="90b0f-134">Cuando vea la siguiente notificación, significará que la operación de escalado se habrá completado.</span><span class="sxs-lookup"><span data-stu-id="90b0f-134">When you see the following notification, the scale operation is complete.</span></span>

![Confirmación de la operación de escalado](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-the-domain"></a><span data-ttu-id="90b0f-136">Comprar el dominio</span><span class="sxs-lookup"><span data-stu-id="90b0f-136">Buy the domain</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="90b0f-137">Inicio de sesión en Azure</span><span class="sxs-lookup"><span data-stu-id="90b0f-137">Sign in to Azure</span></span>
<span data-ttu-id="90b0f-138">Abra [Azure Portal](https://portal.azure.com/) e inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="90b0f-138">Open the [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="90b0f-139">Iniciar Comprar dominios</span><span class="sxs-lookup"><span data-stu-id="90b0f-139">Launch Buy domains</span></span>
<span data-ttu-id="90b0f-140">En la pestaña **Web Apps**, haga clic en el nombre de la aplicación web, seleccione **Configuración** y elija **Dominios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-140">In the **Web Apps** tab, click the name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="90b0f-141">En la página **Dominios personalizados**, haga clic en **Comprar dominios**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-141">In the **Custom domains** page, click **Buy domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-the-domain-purchase"></a><span data-ttu-id="90b0f-142">Configurar la compra del dominio</span><span class="sxs-lookup"><span data-stu-id="90b0f-142">Configure the domain purchase</span></span>

<span data-ttu-id="90b0f-143">En la página **Dominio de App Service**, escriba el nombre de dominio que quiere comprar en el cuadro **Buscar dominio** y escriba `Enter`.</span><span class="sxs-lookup"><span data-stu-id="90b0f-143">In the **App Service Domain** page, in the **Search for domain** box, type the domain name you want to buy and type `Enter`.</span></span> <span data-ttu-id="90b0f-144">Los dominios disponibles sugeridos se muestran justo debajo del cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="90b0f-144">The suggested available domains are shown just below the text box.</span></span> <span data-ttu-id="90b0f-145">Seleccione uno o varios dominios que quiera comprar.</span><span class="sxs-lookup"><span data-stu-id="90b0f-145">Select one or more domains you want to buy.</span></span> 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

<span data-ttu-id="90b0f-146">Haga clic en **Información de contacto** y rellene el formulario de información de contacto del dominio.</span><span class="sxs-lookup"><span data-stu-id="90b0f-146">Click the **Contact Information** and fill out the domain's contact information form.</span></span> <span data-ttu-id="90b0f-147">Cuando termine, haga clic en **Aceptar** para volver a la página Dominio de App Service.</span><span class="sxs-lookup"><span data-stu-id="90b0f-147">When finished, click **OK** to return to the App Service Domain page.</span></span>
   
<span data-ttu-id="90b0f-148">Es importante que rellene todos los campos obligatorios con la mayor precisión posible.</span><span class="sxs-lookup"><span data-stu-id="90b0f-148">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="90b0f-149">Los datos incorrectos para la información de contacto pueden producir un error al comprar los dominios.</span><span class="sxs-lookup"><span data-stu-id="90b0f-149">Incorrect data for contact information can result in failure to purchase domains.</span></span> 

<span data-ttu-id="90b0f-150">A continuación, seleccione las opciones que quiera para el dominio.</span><span class="sxs-lookup"><span data-stu-id="90b0f-150">Next, select the desired options for your domain.</span></span> <span data-ttu-id="90b0f-151">Para obtener explicaciones, vea la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="90b0f-151">See the following table for explanations:</span></span>

| <span data-ttu-id="90b0f-152">Configuración</span><span class="sxs-lookup"><span data-stu-id="90b0f-152">Setting</span></span> | <span data-ttu-id="90b0f-153">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="90b0f-153">Suggested Value</span></span> | <span data-ttu-id="90b0f-154">Descripción</span><span class="sxs-lookup"><span data-stu-id="90b0f-154">Description</span></span> |
|-|-|-|
|<span data-ttu-id="90b0f-155">Renovación automática</span><span class="sxs-lookup"><span data-stu-id="90b0f-155">Auto renew</span></span> | <span data-ttu-id="90b0f-156">**Habilitación**</span><span class="sxs-lookup"><span data-stu-id="90b0f-156">**Enable**</span></span> | <span data-ttu-id="90b0f-157">Renueva automáticamente el dominio de App Service cada año.</span><span class="sxs-lookup"><span data-stu-id="90b0f-157">Renews your App Service Domain automatically every year.</span></span> <span data-ttu-id="90b0f-158">En el momento de la renovación se cargará el mismo precio de compra en su tarjeta de crédito.</span><span class="sxs-lookup"><span data-stu-id="90b0f-158">Your credit card is charged the same purchase price at the time of renewal.</span></span> |
|<span data-ttu-id="90b0f-159">Protección de la privacidad</span><span class="sxs-lookup"><span data-stu-id="90b0f-159">Privacy protection</span></span> | <span data-ttu-id="90b0f-160">Habilitar</span><span class="sxs-lookup"><span data-stu-id="90b0f-160">Enable</span></span> | <span data-ttu-id="90b0f-161">Participe en "Protección de la privacidad", que se incluye en el precio de compra _gratuitamente_ (excepto para los dominios de nivel superior cuyo registro no admite la protección de la privacidad, como _.co.in_, _.co.uk_ y así sucesivamente).</span><span class="sxs-lookup"><span data-stu-id="90b0f-161">Opt in to "Privacy protection", which is included in the purchase price _for free_ (except for top-level domains whose registry do not support privacy protection, such as _.co.in_, _.co.uk_, and so on).</span></span> |
| <span data-ttu-id="90b0f-162">Asignar nombres de host predeterminados</span><span class="sxs-lookup"><span data-stu-id="90b0f-162">Assign default hostnames</span></span> | <span data-ttu-id="90b0f-163">**www** y **@**</span><span class="sxs-lookup"><span data-stu-id="90b0f-163">**www** and **@**</span></span> | <span data-ttu-id="90b0f-164">Seleccione los enlaces de nombre de host deseados, si quiere.</span><span class="sxs-lookup"><span data-stu-id="90b0f-164">Select the desired hostname bindings, if desired.</span></span> <span data-ttu-id="90b0f-165">Una vez completada la operación de compra de dominio, puede tener acceso a la aplicación web en los nombres de host seleccionados.</span><span class="sxs-lookup"><span data-stu-id="90b0f-165">When the domain purchase operation is complete, your web app can be accessed at the selected hostnames.</span></span> <span data-ttu-id="90b0f-166">Si la aplicación web está detrás de [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), no verá la opción para asignar el dominio raíz (@), ya que Traffic Manager no admite registros A.</span><span class="sxs-lookup"><span data-stu-id="90b0f-166">If the web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see the option to assign the root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="90b0f-167">Puede realizar cambios en las asignaciones de nombre de host una vez completada la compra del dominio.</span><span class="sxs-lookup"><span data-stu-id="90b0f-167">You can make changes to the hostname assignments after the domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="90b0f-168">Aceptar los términos y comprar</span><span class="sxs-lookup"><span data-stu-id="90b0f-168">Accept terms and purchase</span></span>

<span data-ttu-id="90b0f-169">Haga clic en **Condiciones legales** para consultar las condiciones y los gastos y, después, haga clic en **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-169">Click **Legal Terms** to review the terms and the charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="90b0f-170">Los dominios de App Service usan DNS de Azure para hospedar los dominios.</span><span class="sxs-lookup"><span data-stu-id="90b0f-170">App Service Domains use Azure DNS to host the domains.</span></span> <span data-ttu-id="90b0f-171">Además de la tarifa de registro del dominio, se aplican cargos de uso de DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="90b0f-171">In addition to the domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="90b0f-172">Para obtener más información, vea [DNS de Azure Precios](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="90b0f-172">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="90b0f-173">De nuevo en la hoja **Dominio de App Service**, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-173">Back in the **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="90b0f-174">Mientras la operación está en curso, verá las notificaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="90b0f-174">While the operation is in progress, you see the following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-the-hostnames"></a><span data-ttu-id="90b0f-175">Probar los nombres de host</span><span class="sxs-lookup"><span data-stu-id="90b0f-175">Test the hostnames</span></span>

<span data-ttu-id="90b0f-176">Si ha asignado nombres de host predeterminados a la aplicación web, también verá una notificación de operación correcta para cada nombre de host seleccionado.</span><span class="sxs-lookup"><span data-stu-id="90b0f-176">If you have assigned default hostnames to your web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="90b0f-177">También verá los nombres de host seleccionados en la página **Dominios personalizados**, en la sección **Nombres de host**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-177">You also see the selected hostnames in the **Custom domains** page, in the **Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="90b0f-178">Para probar los nombres de host, vaya a los nombres de host enumerados en el explorador.</span><span class="sxs-lookup"><span data-stu-id="90b0f-178">To test the hostnames, navigate to the listed hostnames in the browser.</span></span> <span data-ttu-id="90b0f-179">En el ejemplo de la captura de pantalla anterior, intente navegar a _kontoso.net_ y _www.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="90b0f-179">In the example in the preceding screenshot, try navigating to _kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-to-web-app"></a><span data-ttu-id="90b0f-180">Asignar nombres de host a la aplicación web</span><span class="sxs-lookup"><span data-stu-id="90b0f-180">Assign hostnames to web app</span></span>

<span data-ttu-id="90b0f-181">Si decide no asignar uno o varios nombres de host predeterminados a la aplicación web durante el proceso de compra, o si tiene que asignar un nombre de host que no aparece, puede asignar un nombre de host en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="90b0f-181">If you choose not to assign one or more default hostnames to your web app during the purchase process, or if you need to assign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="90b0f-182">También puede asignar nombres de host en el dominio de App Service a cualquier otra aplicación web.</span><span class="sxs-lookup"><span data-stu-id="90b0f-182">You can also assign hostnames in the App Service Domain to any other web app.</span></span> <span data-ttu-id="90b0f-183">Los pasos dependen de si el dominio de App Service y la aplicación web pertenecen a la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="90b0f-183">The steps depend on whether the App Service Domain and the web app belong to the same subscription.</span></span>

- <span data-ttu-id="90b0f-184">Suscripción diferente: asigne los registros DNS personalizados desde el dominio de App Service a la aplicación web como un dominio comprado de forma externa.</span><span class="sxs-lookup"><span data-stu-id="90b0f-184">Different subscription: Map custom DNS records from the App Service Domain to the web app like an externally purchased domain.</span></span> <span data-ttu-id="90b0f-185">Para obtener información sobre cómo agregar nombres DNS personalizados a un dominio de App Service, vea [Administrar los registros DNS personalizados](#custom).</span><span class="sxs-lookup"><span data-stu-id="90b0f-185">For information on adding custom DNS names to an App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="90b0f-186">Para asignar un dominio comprado externo a una aplicación web, vea [Asignar un nombre DNS personalizado a Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="90b0f-186">To map an external purchased domain to a web app, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="90b0f-187">La misma suscripción: siga los pasos que hay a continuación.</span><span class="sxs-lookup"><span data-stu-id="90b0f-187">Same subscription: Use the following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="90b0f-188">Iniciar Agregar nombre de host</span><span class="sxs-lookup"><span data-stu-id="90b0f-188">Launch add hostname</span></span>
<span data-ttu-id="90b0f-189">En la página **App Services**, seleccione el nombre de la aplicación web a la que quiere asignar los nombres de host, seleccione **Configuración** y después **Dominios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-189">In the **App Services** page, select the name of your web app that you want to assign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="90b0f-190">Asegúrese de que el dominio comprado aparece en la sección **Dominios de App Service**, pero no lo seleccione.</span><span class="sxs-lookup"><span data-stu-id="90b0f-190">Make sure that your purchased domain is listed in the **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="90b0f-191">Todos los dominios de App Service de la misma suscripción se muestran en la página **Dominios personalizados** de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="90b0f-191">All App Service Domains in the same subscription are shown in the web app's **Custom domains** page.</span></span> <span data-ttu-id="90b0f-192">Si el dominio está en la suscripción de la aplicación web, pero no puede verlo en la página **Dominios personalizados** de la aplicación web, intente volver a abrir la página **Dominios personalizados** o actualice la página web.</span><span class="sxs-lookup"><span data-stu-id="90b0f-192">If your domain is in the web app's subscription, but you cannot see it in the web app's **Custom domains** page, try reopening the **Custom domains** page or refresh the webpage.</span></span> <span data-ttu-id="90b0f-193">Compruebe también la campana de notificación situada en la parte superior de Azure Portal para ver el progreso o los errores de creación.</span><span class="sxs-lookup"><span data-stu-id="90b0f-193">Also, check the notification bell at the top of the Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="90b0f-194">Seleccione **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-194">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="90b0f-195">Configurar el nombre de host</span><span class="sxs-lookup"><span data-stu-id="90b0f-195">Configure hostname</span></span>
<span data-ttu-id="90b0f-196">En el cuadro de diálogo **Agregar nombre de host**, escriba el nombre de dominio completo de su dominio de App Service o cualquier subdominio.</span><span class="sxs-lookup"><span data-stu-id="90b0f-196">In the **Add hostname** dialog, type the fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="90b0f-197">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="90b0f-197">For example:</span></span>

- <span data-ttu-id="90b0f-198">kontoso.net</span><span class="sxs-lookup"><span data-stu-id="90b0f-198">kontoso.net</span></span>
- <span data-ttu-id="90b0f-199">www.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="90b0f-199">www.kontoso.net</span></span>
- <span data-ttu-id="90b0f-200">abc.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="90b0f-200">abc.kontoso.net</span></span>

<span data-ttu-id="90b0f-201">Cuando termine, seleccione **Validar**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-201">When finished, select **Validate**.</span></span> <span data-ttu-id="90b0f-202">El tipo de registro de nombre de host se selecciona automáticamente.</span><span class="sxs-lookup"><span data-stu-id="90b0f-202">The hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="90b0f-203">Seleccione **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-203">Select **Add hostname**.</span></span>

<span data-ttu-id="90b0f-204">Una vez completada la operación, verá una notificación de operación correcta para el nombre de host asignado.</span><span class="sxs-lookup"><span data-stu-id="90b0f-204">When the operation is complete, you see a success notification for the assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="90b0f-205">Cerrar Agregar nombre de host</span><span class="sxs-lookup"><span data-stu-id="90b0f-205">Close add hostname</span></span>
<span data-ttu-id="90b0f-206">En la página **Agregar nombre de host**, asigne otros nombres de host a la aplicación web, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="90b0f-206">In the **Add hostname** page, assign any other hostname to your web app, as desired.</span></span> <span data-ttu-id="90b0f-207">Cuando termine, cierre la página **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-207">When finished, close the **Add hostname** page.</span></span>

<span data-ttu-id="90b0f-208">Ahora debería ver el nombre de host recién asignado en la página **Dominios personalizados** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="90b0f-208">You should now see the newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-the-hostnames"></a><span data-ttu-id="90b0f-209">Probar los nombres de host</span><span class="sxs-lookup"><span data-stu-id="90b0f-209">Test the hostnames</span></span>

<span data-ttu-id="90b0f-210">Vaya a los nombres de host enumerados en el explorador.</span><span class="sxs-lookup"><span data-stu-id="90b0f-210">Navigate to the listed hostnames in the browser.</span></span> <span data-ttu-id="90b0f-211">En el ejemplo de la captura de pantalla anterior, intente navegar a _abc.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="90b0f-211">In the example in the preceding screenshot, try navigating to _abc.kontoso.net_.</span></span>

<a name="custom" />

## <a name="manage-custom-dns-records"></a><span data-ttu-id="90b0f-212">Administrar los registros DNS personalizados</span><span class="sxs-lookup"><span data-stu-id="90b0f-212">Manage custom DNS records</span></span>

<span data-ttu-id="90b0f-213">En Azure, los registros DNS para un dominio de App Service se administran mediante [DNS de Azure](https://azure.microsoft.com/services/dns/).</span><span class="sxs-lookup"><span data-stu-id="90b0f-213">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="90b0f-214">Puede agregar, quitar y actualizar los registros DNS, al igual que para un dominio comprado de forma externa.</span><span class="sxs-lookup"><span data-stu-id="90b0f-214">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="90b0f-215">Abrir Dominio de App Service</span><span class="sxs-lookup"><span data-stu-id="90b0f-215">Open App Service Domain</span></span>

<span data-ttu-id="90b0f-216">En Azure Portal, en el menú de la izquierda, seleccione **Más servicios** > **Dominios de App Service**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-216">In the Azure portal, from the left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="90b0f-217">Seleccione el dominio que se va a administrar.</span><span class="sxs-lookup"><span data-stu-id="90b0f-217">Select the domain to manage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="90b0f-218">Obtener acceso a la zona DNS</span><span class="sxs-lookup"><span data-stu-id="90b0f-218">Access DNS zone</span></span>

<span data-ttu-id="90b0f-219">En el menú de la izquierda del dominio, seleccione **Zona DNS**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-219">In the domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="90b0f-220">Esta acción abre la página [Zona DNS](../dns/dns-zones-records.md) de su dominio de App Service en DNS de Azure.</span><span class="sxs-lookup"><span data-stu-id="90b0f-220">This action opens the [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="90b0f-221">Para obtener información sobre cómo editar los registros DNS, vea [Administración de zonas DNS en Azure Portal](../dns/dns-operations-dnszones-portal.md).</span><span class="sxs-lookup"><span data-stu-id="90b0f-221">For information on how to edit DNS records, see [How to manage DNS Zones in the Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="90b0f-222">Cancelar la compra (eliminar el dominio)</span><span class="sxs-lookup"><span data-stu-id="90b0f-222">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="90b0f-223">Después de comprar el dominio de App Service, dispone de cinco días para cancelar la compra para obtener un reembolso completo.</span><span class="sxs-lookup"><span data-stu-id="90b0f-223">After you purchase the App Service Domain, you have five days to cancel your purchase for a full refund.</span></span> <span data-ttu-id="90b0f-224">Después de cinco días, puede eliminar el dominio de App Service, pero no puede recibir un reembolso.</span><span class="sxs-lookup"><span data-stu-id="90b0f-224">After five days, you can delete the App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="90b0f-225">Abrir Dominio de App Service</span><span class="sxs-lookup"><span data-stu-id="90b0f-225">Open App Service Domain</span></span>

<span data-ttu-id="90b0f-226">En Azure Portal, en el menú de la izquierda, seleccione **Más servicios** > **Dominios de App Service**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-226">In the Azure portal, from the left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="90b0f-227">Seleccione el dominio que quiera cancelar o eliminar.</span><span class="sxs-lookup"><span data-stu-id="90b0f-227">Select the domain to you want to cancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="90b0f-228">Eliminación de enlaces de nombre de host</span><span class="sxs-lookup"><span data-stu-id="90b0f-228">Delete hostname bindings</span></span>

<span data-ttu-id="90b0f-229">En el menú de la izquierda del dominio, seleccione **Enlaces de nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-229">In the domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="90b0f-230">Aquí se enumeran los enlaces de nombre de host de todos los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="90b0f-230">The hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="90b0f-231">No se puede eliminar el dominio de App Service hasta que se eliminen todos los enlaces de nombre de host.</span><span class="sxs-lookup"><span data-stu-id="90b0f-231">You cannot delete the App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="90b0f-232">Para eliminar todos los enlaces de nombre de host, seleccione **...** > **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-232">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="90b0f-233">Después de eliminarlos todos, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-233">After all the bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="90b0f-234">Cancelar o eliminar</span><span class="sxs-lookup"><span data-stu-id="90b0f-234">Cancel or delete</span></span>

<span data-ttu-id="90b0f-235">En el menú de la izquierda del dominio, seleccione **Información general**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-235">In the domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="90b0f-236">Si no ha transcurrido el período de cancelación en el dominio comprado, haga clic en **Cancelar compra**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-236">If the cancellation period on the purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="90b0f-237">De lo contrario, en su lugar verá el botón **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-237">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="90b0f-238">Para eliminar el dominio sin un reembolso, haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="90b0f-238">To delete the domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="90b0f-239">Haga clic en **Aceptar** para confirmar la operación.</span><span class="sxs-lookup"><span data-stu-id="90b0f-239">Select **OK** to confirm the operation.</span></span> <span data-ttu-id="90b0f-240">Si no quiere continuar, haga clic en cualquier lugar fuera del cuadro de diálogo de confirmación.</span><span class="sxs-lookup"><span data-stu-id="90b0f-240">If you don't want to proceed, click anywhere outside of the confirmation dialog.</span></span>

<span data-ttu-id="90b0f-241">Una vez completada la operación, el dominio se libera de la suscripción y vuelve a estar disponible para que otros usuarios lo compren.</span><span class="sxs-lookup"><span data-stu-id="90b0f-241">After the operation is complete, the domain is released from your subscription and available for anyone to purchase again.</span></span> 
