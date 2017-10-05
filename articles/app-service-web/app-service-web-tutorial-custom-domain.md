---
title: Asignar un nombre DNS personalizado a Azure Web Apps | Microsoft Docs
description: "Aprenda a agregar un nombre de dominio DNS personalizado (dominio personal) a una aplicación web, un back-end de una aplicación móvil o una aplicación de API en Azure App Service."
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
ms.openlocfilehash: 973cda462e8d258cc848e1036891c7f8af043102
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="map-an-existing-custom-dns-name-to-azure-web-apps"></a><span data-ttu-id="aefbf-103">Asignar un nombre DNS personalizado a Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="aefbf-103">Map an existing custom DNS name to Azure Web Apps</span></span>

<span data-ttu-id="aefbf-104">[Azure Web Apps](app-service-web-overview.md) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="aefbf-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="aefbf-105">En este tutorial se muestra cómo asignar un nombre DNS personalizado a Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="aefbf-105">This tutorial shows you how to map an existing custom DNS name to Azure Web Apps.</span></span>

![Navegación en el portal a la aplicación de Azure](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="aefbf-107">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="aefbf-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aefbf-108">Asignar un subdominio (por ejemplo, `www.contoso.com`) mediante el uso de un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="aefbf-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="aefbf-109">Asignar un dominio raíz (por ejemplo, `contoso.com`) mediante el uso de un registro D</span><span class="sxs-lookup"><span data-stu-id="aefbf-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="aefbf-110">Asignar un dominio con comodín (por ejemplo, `*.contoso.com`) mediante el uso de un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="aefbf-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="aefbf-111">Automatizar la asignación de dominio con scripts</span><span class="sxs-lookup"><span data-stu-id="aefbf-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="aefbf-112">Puede usar un **registro CNAME** o un **registro A** para asignar un nombre DNS personalizado a App Service.</span><span class="sxs-lookup"><span data-stu-id="aefbf-112">You can use either a **CNAME record** or an **A record** to map a custom DNS name to App Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="aefbf-113">Se recomienda usar un CNAME para todos los nombres DNS personalizados, excepto un dominio raíz (por ejemplo, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="aefbf-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="aefbf-114">Para migrar un sitio en vivo y su nombre de dominio DNS a App Service, consulte [Migración de un nombre DNS activo a Azure App Service](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="aefbf-114">To migrate a live site and its DNS domain name to App Service, see [Migrate an active DNS name to Azure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aefbf-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="aefbf-115">Prerequisites</span></span>

<span data-ttu-id="aefbf-116">Para completar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="aefbf-116">To complete this tutorial:</span></span>

* <span data-ttu-id="aefbf-117">[Cree una aplicación de App Service](/azure/app-service/) o use alguna aplicación que haya creado para otro tutorial.</span><span class="sxs-lookup"><span data-stu-id="aefbf-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="aefbf-118">Adquiera un nombre de dominio y asegúrese de que tiene acceso al registro de DNS de su proveedor de dominio (por ejemplo, GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="aefbf-118">Purchase a domain name and make sure you have access to the DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="aefbf-119">Por ejemplo, para agregar entradas DNS para `contoso.com` y `www.contoso.com`, debe poder configurar las opciones de DNS del dominio raíz de `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="aefbf-119">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must be able to configure the DNS settings for the `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="aefbf-120">Si no tiene un nombre de dominio, considere la posibilidad de [comprar un dominio mediante Azure Portal](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="aefbf-120">If you don't have an existing domain name, consider [purchasing a domain using the Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-the-app"></a><span data-ttu-id="aefbf-121">Preparación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="aefbf-121">Prepare the app</span></span>

<span data-ttu-id="aefbf-122">Para asignar un nombre DNS personalizado a una aplicación web, el [plan de App Service](https://azure.microsoft.com/pricing/details/app-service/) de dicha aplicación debe ser un nivel de pago (**Compartido**, **Básico**, **Estándar** o **Premium**).</span><span class="sxs-lookup"><span data-stu-id="aefbf-122">To map a custom DNS name to a web app, the web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="aefbf-123">En este paso, asegúrese de que la aplicación de App Service se encuentra en el plan de tarifa compatible.</span><span class="sxs-lookup"><span data-stu-id="aefbf-123">In this step, you make sure that the App Service app is in the supported pricing tier.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="aefbf-124">Inicio de sesión en Azure</span><span class="sxs-lookup"><span data-stu-id="aefbf-124">Sign in to Azure</span></span>

<span data-ttu-id="aefbf-125">Abra [Azure Portal](https://portal.azure.com) e inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="aefbf-125">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-to-the-app-in-the-azure-portal"></a><span data-ttu-id="aefbf-126">Navegue hasta la aplicación en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="aefbf-126">Navigate to the app in the Azure portal</span></span>

<span data-ttu-id="aefbf-127">En el menú izquierdo, seleccione **App Services** y, después, el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aefbf-127">From the left menu, select **App Services**, and then select the name of the app.</span></span>

![Navegación en el portal a la aplicación de Azure](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="aefbf-129">Consulte la página de administración de la aplicación de App Service.</span><span class="sxs-lookup"><span data-stu-id="aefbf-129">You see the management page of the App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-the-pricing-tier"></a><span data-ttu-id="aefbf-130">Comprobar el plan de tarifa</span><span class="sxs-lookup"><span data-stu-id="aefbf-130">Check the pricing tier</span></span>

<span data-ttu-id="aefbf-131">En el panel de navegación izquierdo de la página de la aplicación, desplácese hasta la sección **Configuración** y seleccione **Escalar verticalmente (plan de App Service)**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-131">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menú Escalar verticalmente](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="aefbf-133">El nivel actual de la aplicación aparece resaltado con un cuadro azul.</span><span class="sxs-lookup"><span data-stu-id="aefbf-133">The app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="aefbf-134">Asegúrese de que la aplicación web no está en el nivel **Gratis**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-134">Check to make sure that the app is not in the **Free** tier.</span></span> <span data-ttu-id="aefbf-135">No se admiten DNS personalizados en el nivel **Gratis**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-135">Custom DNS is not supported in the **Free** tier.</span></span> 

![Comprobar plan de tarifa](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="aefbf-137">Si el plan de App Service no es **Gratis**, cierre la página **Elija su plan de tarifa** y vaya directamente a [Asignar un registro CNAME](#cname).</span><span class="sxs-lookup"><span data-stu-id="aefbf-137">If the App Service plan is not **Free**, close the **Choose your pricing tier** page and skip to [Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-the-app-service-plan"></a><span data-ttu-id="aefbf-138">Escalado verticalmente del plan de App Service</span><span class="sxs-lookup"><span data-stu-id="aefbf-138">Scale up the App Service plan</span></span>

<span data-ttu-id="aefbf-139">Seleccione alguno de los niveles de pago (**Compartido**, **Básico**, **Estándar** o **Premium**).</span><span class="sxs-lookup"><span data-stu-id="aefbf-139">Select any of the non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="aefbf-140">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-140">Click **Select**.</span></span>

![Comprobar plan de tarifa](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="aefbf-142">Cuando vea la siguiente notificación, significará que la operación de escalado se habrá completado.</span><span class="sxs-lookup"><span data-stu-id="aefbf-142">When you see the following notification, the scale operation is complete.</span></span>

![Confirmación de la operación de escalado](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="aefbf-144">Asignar un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="aefbf-144">Map a CNAME record</span></span>

<span data-ttu-id="aefbf-145">En el ejemplo del tutorial, agregue un registro CNAME para el subdominio `www` (por ejemplo, `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="aefbf-145">In the tutorial example, you add a CNAME record for the `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-cname-record"></a><span data-ttu-id="aefbf-146">Crear un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="aefbf-146">Create the CNAME record</span></span>

<span data-ttu-id="aefbf-147">Agregue un registro CNAME para asignar un subdominio al nombre de host predeterminado de la aplicación (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="aefbf-147">Add a CNAME record to map a subdomain to the app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="aefbf-148">En el caso del dominio `www.contoso.com` del ejemplo, agregue un registro CNAME que asigne el nombre `www` a `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="aefbf-148">For the `www.contoso.com` domain example, add a CNAME record that maps the name `www` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="aefbf-149">Después de agregar CNAME, la página de registros DNS es como la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="aefbf-149">After you add the CNAME, the DNS records page looks like the following example:</span></span>

![Navegación en el portal a la aplicación de Azure](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-the-cname-record-mapping-in-azure"></a><span data-ttu-id="aefbf-151">Habilitación de la asignación de registros CNAME en Azure</span><span class="sxs-lookup"><span data-stu-id="aefbf-151">Enable the CNAME record mapping in Azure</span></span>

<span data-ttu-id="aefbf-152">En el panel de navegación izquierdo de la página de la aplicación en Azure Portal, seleccione **Dominios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-152">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Menú Dominio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="aefbf-154">En la página **Dominios personalizados** de la aplicación, agregue el nombre DNS personalizado completo (`www.contoso.com`) a la lista.</span><span class="sxs-lookup"><span data-stu-id="aefbf-154">In the **Custom domains** page of the app, add the fully qualified custom DNS name (`www.contoso.com`) to the list.</span></span>

<span data-ttu-id="aefbf-155">Seleccione el icono **+** situado junto a **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-155">Select the **+** icon next to **Add hostname**.</span></span>

![Agregar nombre de host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="aefbf-157">Escriba el nombre de dominio completo para el que ha agregado un registro CNAME, como `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="aefbf-157">Type the fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="aefbf-158">Seleccione **Validar**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-158">Select **Validate**.</span></span>

<span data-ttu-id="aefbf-159">Se activa el botón **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-159">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="aefbf-160">Asegúrese de que en **Tipo de registro de nombre de host** está seleccionado **CNAME (www.example.com o cualquier subdominio)**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-160">Make sure that **Hostname record type** is set to **CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="aefbf-161">Seleccione **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-161">Select **Add hostname**.</span></span>

![Agregar nombre DNS a la aplicación](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="aefbf-163">El nuevo nombre de host puede tardar un tiempo en reflejarse en la página **Dominios personalizados** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aefbf-163">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="aefbf-164">Intente actualizar el explorador para actualizar los datos.</span><span class="sxs-lookup"><span data-stu-id="aefbf-164">Try refreshing the browser to update the data.</span></span>

![Registro CNAME agregado](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="aefbf-166">Si se olvidó de un paso o cometió un error tipográfico en alguna parte anteriormente, verá un error de comprobación en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="aefbf-166">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Error de comprobación](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="aefbf-168">Asignar un registro A</span><span class="sxs-lookup"><span data-stu-id="aefbf-168">Map an A record</span></span>

<span data-ttu-id="aefbf-169">En el ejemplo del tutorial, se agrega un registro A al dominio raíz (por ejemplo, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="aefbf-169">In the tutorial example, you add an A record for the root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-the-apps-ip-address"></a><span data-ttu-id="aefbf-170">Copiar la dirección IP de la aplicación</span><span class="sxs-lookup"><span data-stu-id="aefbf-170">Copy the app's IP address</span></span>

<span data-ttu-id="aefbf-171">Para asignar un registro A, se necesita la dirección IP externa de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aefbf-171">To map an A record, you need the app's external IP address.</span></span> <span data-ttu-id="aefbf-172">Dicha dirección IP se puede encontrar en la página **Dominios personalizados** de la aplicación en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="aefbf-172">You can find this IP address in the app's **Custom domains** page in the Azure portal.</span></span>

<span data-ttu-id="aefbf-173">En el panel de navegación izquierdo de la página de la aplicación en Azure Portal, seleccione **Dominios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-173">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Menú Dominio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="aefbf-175">En la página **Dominios personalizados**, copie la dirección IP de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aefbf-175">In the **Custom domains** page, copy the app's IP address.</span></span>

![Navegación en el portal a la aplicación de Azure](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-a-record"></a><span data-ttu-id="aefbf-177">Crear el registro A</span><span class="sxs-lookup"><span data-stu-id="aefbf-177">Create the A record</span></span>

<span data-ttu-id="aefbf-178">Para asignar un registro A a un aplicación, App Service requiere **dos** registros DNS:</span><span class="sxs-lookup"><span data-stu-id="aefbf-178">To map an A record to an app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="aefbf-179">Un registro **A** que se asigna a la dirección IP de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aefbf-179">An **A** record to map to the app's IP address.</span></span>
- <span data-ttu-id="aefbf-180">Un registro **TXT** que se asigna al nombre de host predeterminado de la aplicación `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="aefbf-180">A **TXT** record to map to the app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="aefbf-181">App Service usa este registro solo durante la configuración para comprobar que posee el dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="aefbf-181">App Service uses this record only at configuration time, to verify that you own the custom domain.</span></span> <span data-ttu-id="aefbf-182">Después de que el dominio personalizado se valida y se configura en App Service, puede eliminar el registro TXT.</span><span class="sxs-lookup"><span data-stu-id="aefbf-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="aefbf-183">En el dominio `contoso.com` del ejemplo, cree los registros D y TXT según la tabla siguiente (`@` suele representar el dominio raíz).</span><span class="sxs-lookup"><span data-stu-id="aefbf-183">For the `contoso.com` domain example, create the A and TXT records according to the following table (`@` typically represents the root domain).</span></span> 

| <span data-ttu-id="aefbf-184">Tipo de registro</span><span class="sxs-lookup"><span data-stu-id="aefbf-184">Record type</span></span> | <span data-ttu-id="aefbf-185">Host</span><span class="sxs-lookup"><span data-stu-id="aefbf-185">Host</span></span> | <span data-ttu-id="aefbf-186">Valor</span><span class="sxs-lookup"><span data-stu-id="aefbf-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="aefbf-187">Una </span><span class="sxs-lookup"><span data-stu-id="aefbf-187">A</span></span> | `@` | <span data-ttu-id="aefbf-188">Dirección IP de [Copiar la dirección IP de la aplicación](#info)</span><span class="sxs-lookup"><span data-stu-id="aefbf-188">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="aefbf-189">TXT</span><span class="sxs-lookup"><span data-stu-id="aefbf-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="aefbf-190">Cuando se agregan los registros, la página de registros DNS es como la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="aefbf-190">When the records are added, the DNS records page looks like the following example:</span></span>

![Página de registros DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-the-a-record-mapping-in-the-app"></a><span data-ttu-id="aefbf-192">Habilitar la asignación de registros A en la aplicación</span><span class="sxs-lookup"><span data-stu-id="aefbf-192">Enable the A record mapping in the app</span></span>

<span data-ttu-id="aefbf-193">De vuelta a la página **Dominios personalizados** de la aplicación en Azure Portal, agregue el nombre DNS personalizado completo (por ejemplo, `contoso.com`) a la lista.</span><span class="sxs-lookup"><span data-stu-id="aefbf-193">Back in the app's **Custom domains** page in the Azure portal, add the fully qualified custom DNS name (for example, `contoso.com`) to the list.</span></span>

<span data-ttu-id="aefbf-194">Seleccione el icono **+** situado junto a **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-194">Select the **+** icon next to **Add hostname**.</span></span>

![Agregar nombre de host](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="aefbf-196">Escriba el nombre de dominio completo para el que ha configurado el registro A, como `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="aefbf-196">Type the fully qualified domain name that you configured the A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="aefbf-197">Seleccione **Validar**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-197">Select **Validate**.</span></span>

<span data-ttu-id="aefbf-198">Se activa el botón **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-198">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="aefbf-199">Asegúrese de que el **tipo de registro de nombre de host** esté establecido en el **registro D (ejemplo.com)**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-199">Make sure that **Hostname record type** is set to **A record (example.com)**.</span></span>

<span data-ttu-id="aefbf-200">Seleccione **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-200">Select **Add hostname**.</span></span>

![Agregar nombre DNS a la aplicación](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="aefbf-202">El nuevo nombre de host puede tardar un tiempo en reflejarse en la página **Dominios personalizados** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aefbf-202">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="aefbf-203">Intente actualizar el explorador para actualizar los datos.</span><span class="sxs-lookup"><span data-stu-id="aefbf-203">Try refreshing the browser to update the data.</span></span>

![Registro D agregado](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="aefbf-205">Si se olvidó de un paso o cometió un error tipográfico en alguna parte anteriormente, verá un error de comprobación en la parte inferior de la página.</span><span class="sxs-lookup"><span data-stu-id="aefbf-205">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Error de comprobación](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="aefbf-207">Asignar un dominio con caracteres comodín</span><span class="sxs-lookup"><span data-stu-id="aefbf-207">Map a wildcard domain</span></span>

<span data-ttu-id="aefbf-208">En el ejemplo del tutorial, asigne un [nombre DNS con caracteres comodín](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (por ejemplo, `*.contoso.com`) a la aplicación de App Service mediante la adición de un registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="aefbf-208">In the tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) to the App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-cname-record"></a><span data-ttu-id="aefbf-209">Crear un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="aefbf-209">Create the CNAME record</span></span>

<span data-ttu-id="aefbf-210">Agregue un registro CNAME para asignar un nombre con caracteres comodín al nombre de host predeterminado de la aplicación (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="aefbf-210">Add a CNAME record to map a wildcard name to the app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="aefbf-211">En el dominio `*.contoso.com` del ejemplo, el registro CNAME asignará el nombre `*` a `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="aefbf-211">For the `*.contoso.com` domain example, the CNAME record will map the name `*` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="aefbf-212">Cuando se agrega CNAME, la página de registros DNS es como la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="aefbf-212">When the CNAME is added, the DNS records page looks like the following example:</span></span>

![Navegación en el portal a la aplicación de Azure](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-the-cname-record-mapping-in-the-app"></a><span data-ttu-id="aefbf-214">Habilitación de la asignación del registro CNAME en la aplicación</span><span class="sxs-lookup"><span data-stu-id="aefbf-214">Enable the CNAME record mapping in the app</span></span>

<span data-ttu-id="aefbf-215">Ahora puede agregar cualquier subdominio que coincida con el nombre con caracteres comodín a la aplicación (por ejemplo, `sub1.contoso.com` y `sub2.contoso.com` coinciden con `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="aefbf-215">You can now add any subdomain that matches the wildcard name to the app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="aefbf-216">En el panel de navegación izquierdo de la página de la aplicación en Azure Portal, seleccione **Dominios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-216">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Menú Dominio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="aefbf-218">Seleccione el icono **+** situado junto a **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-218">Select the **+** icon next to **Add hostname**.</span></span>

![Agregar nombre de host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="aefbf-220">Escriba un nombre de dominio completo que coincida con el dominio con caracteres comodín (por ejemplo, `sub1.contoso.com`) y, después, seleccione **Validar**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-220">Type a fully qualified domain name that matches the wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="aefbf-221">Se activa el botón **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-221">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="aefbf-222">Asegúrese de que en **Tipo de registro de nombre de host** está seleccionado **Registro CNAME (www.example.com o cualquier subdominio)**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-222">Make sure that **Hostname record type** is set to **CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="aefbf-223">Seleccione **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="aefbf-223">Select **Add hostname**.</span></span>

![Agregar nombre DNS a la aplicación](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="aefbf-225">El nuevo nombre de host puede tardar un tiempo en reflejarse en la página **Dominios personalizados** de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aefbf-225">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="aefbf-226">Intente actualizar el explorador para actualizar los datos.</span><span class="sxs-lookup"><span data-stu-id="aefbf-226">Try refreshing the browser to update the data.</span></span>

<span data-ttu-id="aefbf-227">Vuelva a seleccionar el icono **+** de nuevo para agregar otro nombre de host que coincida con el dominio con caracteres comodín.</span><span class="sxs-lookup"><span data-stu-id="aefbf-227">Select the **+** icon again to add another hostname that matches the wildcard domain.</span></span> <span data-ttu-id="aefbf-228">Por ejemplo, agregue `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="aefbf-228">For example, add `sub2.contoso.com`.</span></span>

![Registro CNAME agregado](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="aefbf-230">Probar en el explorador</span><span class="sxs-lookup"><span data-stu-id="aefbf-230">Test in browser</span></span>

<span data-ttu-id="aefbf-231">Desplácese a los nombres DNS que configuró anteriormente (por ejemplo, `contoso.com`, `www.contoso.com`, `sub1.contoso.com` y `sub2.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="aefbf-231">Browse to the DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Navegación en el portal a la aplicación de Azure](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="aefbf-233">Automatizar con scripts</span><span class="sxs-lookup"><span data-stu-id="aefbf-233">Automate with scripts</span></span>

<span data-ttu-id="aefbf-234">Puede automatizar la administración e dominios personalizados con scripts, mediante la [CLI de Azure](/cli/azure/install-azure-cli) o [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aefbf-234">You can automate management of custom domains with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="aefbf-235">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="aefbf-235">Azure CLI</span></span> 

<span data-ttu-id="aefbf-236">El comando siguiente agrega un nombre DNS personalizado configurado a una aplicación de App Service.</span><span class="sxs-lookup"><span data-stu-id="aefbf-236">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="aefbf-237">Para más información, consulte [Asignación de un dominio personalizado a una aplicación web](scripts/app-service-cli-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="aefbf-237">For more information, see [Map a custom domain to a web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="aefbf-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="aefbf-238">Azure PowerShell</span></span> 

<span data-ttu-id="aefbf-239">El comando siguiente agrega un nombre DNS personalizado configurado a una aplicación de App Service.</span><span class="sxs-lookup"><span data-stu-id="aefbf-239">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="aefbf-240">Para obtener más información, vea [Asignación de un dominio personalizado a una aplicación web](scripts/app-service-powershell-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="aefbf-240">For more information, see [Assign a custom domain to a web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aefbf-241">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aefbf-241">Next steps</span></span>

<span data-ttu-id="aefbf-242">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="aefbf-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aefbf-243">Asignar un subdominio mediante el uso de un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="aefbf-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="aefbf-244">Asignar un dominio raíz mediante el uso de un registro D</span><span class="sxs-lookup"><span data-stu-id="aefbf-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="aefbf-245">Asignar un dominio con comodín mediante el uso de un registro CNAME</span><span class="sxs-lookup"><span data-stu-id="aefbf-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="aefbf-246">Automatizar la asignación de dominio con scripts</span><span class="sxs-lookup"><span data-stu-id="aefbf-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="aefbf-247">Pase al siguiente tutorial para aprender a enlazar un certificado SSL personalizado a una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="aefbf-247">Advance to the next tutorial to learn how to bind a custom SSL certificate to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aefbf-248">Enlazar un certificado SSL personalizado a Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="aefbf-248">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
