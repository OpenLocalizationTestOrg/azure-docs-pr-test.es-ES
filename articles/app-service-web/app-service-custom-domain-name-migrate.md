---
title: nombre de aaaMigrate un DNS de active tooAzure servicio de aplicaciones | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomigrate un nombre de dominio DNS personalizado que ya está asignado tooa live sitio tooAzure servicio de aplicaciones sin tiempo de inactividad."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a><span data-ttu-id="66156-103">Migrar un active tooAzure de nombre DNS servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="66156-103">Migrate an active DNS name tooAzure App Service</span></span>

<span data-ttu-id="66156-104">Este artículo muestra cómo un DNS de active toomigrate nombre demasiado[servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) sin tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="66156-104">This article shows you how toomigrate an active DNS name too[Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="66156-105">Cuando se migran un sitio en vivo y su nombre de dominio DNS tooApp servicio, ese nombre DNS ya está atendiendo a tráfico en vivo.</span><span class="sxs-lookup"><span data-stu-id="66156-105">When you migrate a live site and its DNS domain name tooApp Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="66156-106">Puede evitar tiempos de inactividad en la resolución DNS durante la migración de hello enlazando Hola active DNS nombre tooyour aplicación de servicio de aplicaciones de forma preferente.</span><span class="sxs-lookup"><span data-stu-id="66156-106">You can avoid downtime in DNS resolution during hello migration by binding hello active DNS name tooyour App Service app preemptively.</span></span>

<span data-ttu-id="66156-107">Si no le preocupa el tiempo de inactividad en la resolución de DNS, consulte [asignar un tooAzure de nombre DNS personalizado existente aplicaciones Web](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="66156-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66156-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="66156-108">Prerequisites</span></span>

<span data-ttu-id="66156-109">toocomplete este procedimiento:</span><span class="sxs-lookup"><span data-stu-id="66156-109">toocomplete this how-to:</span></span>

- <span data-ttu-id="66156-110">[Asegúrese de que la aplicación de App Service no esté en el nivel GRATIS](app-service-web-tutorial-custom-domain.md#checkpricing).</span><span class="sxs-lookup"><span data-stu-id="66156-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-hello-domain-name-preemptively"></a><span data-ttu-id="66156-111">Enlazar el nombre de dominio de hello forma preferente</span><span class="sxs-lookup"><span data-stu-id="66156-111">Bind hello domain name preemptively</span></span>

<span data-ttu-id="66156-112">Al enlazar un dominio personalizado de forma preferente, realizar dos procedimientos siguientes de hello antes de realizar cambios en los registros DNS:</span><span class="sxs-lookup"><span data-stu-id="66156-112">When you bind a custom domain preemptively, you accomplish both of hello following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="66156-113">Comprobar la propiedad del dominio</span><span class="sxs-lookup"><span data-stu-id="66156-113">Verify domain ownership</span></span>
- <span data-ttu-id="66156-114">Habilitar el nombre de dominio de hello para la aplicación</span><span class="sxs-lookup"><span data-stu-id="66156-114">Enable hello domain name for your app</span></span>

<span data-ttu-id="66156-115">Cuando finalmente se migra el nombre DNS personalizado de Hola antiguo sitio toohello aplicación de servicio de aplicaciones, no habrá ningún tiempo de inactividad en la resolución de DNS.</span><span class="sxs-lookup"><span data-stu-id="66156-115">When you finally migrate your custom DNS name from hello old site toohello App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="66156-116">Creación de un registro de comprobación de dominio</span><span class="sxs-lookup"><span data-stu-id="66156-116">Create domain verification record</span></span>

<span data-ttu-id="66156-117">propiedad del dominio tooverify, agregar un TXT grabar.</span><span class="sxs-lookup"><span data-stu-id="66156-117">tooverify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="66156-118">Hola registro TXT se asigna desde _awverify.&lt; subdominio >_ too_&lt;appname >. azurewebsites.net_.</span><span class="sxs-lookup"><span data-stu-id="66156-118">hello TXT record maps from _awverify.&lt;subdomain>_ too_&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="66156-119">Hola registro TXT que necesita depende de hello desea toomigrate de registro DNS.</span><span class="sxs-lookup"><span data-stu-id="66156-119">hello TXT record you need depends on hello DNS record you want toomigrate.</span></span> <span data-ttu-id="66156-120">Para obtener ejemplos, vea hello en la tabla siguiente (`@` normalmente representa Hola dominio raíz):</span><span class="sxs-lookup"><span data-stu-id="66156-120">For examples, see hello following table (`@` typically represents hello root domain):</span></span>  

| <span data-ttu-id="66156-121">Ejemplo de registro DNS</span><span class="sxs-lookup"><span data-stu-id="66156-121">DNS record example</span></span> | <span data-ttu-id="66156-122">Host TXT</span><span class="sxs-lookup"><span data-stu-id="66156-122">TXT Host</span></span> | <span data-ttu-id="66156-123">Valor TXT</span><span class="sxs-lookup"><span data-stu-id="66156-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="66156-124">@ (raíz)</span><span class="sxs-lookup"><span data-stu-id="66156-124">@ (root)</span></span> | <span data-ttu-id="66156-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="66156-125">_awverify_</span></span> | <span data-ttu-id="66156-126">_&lt;nombreaplic&gt;.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="66156-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="66156-127">www (sub)</span><span class="sxs-lookup"><span data-stu-id="66156-127">www (sub)</span></span> | <span data-ttu-id="66156-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="66156-128">_awverify.www_</span></span> | <span data-ttu-id="66156-129">_&lt;nombreaplic&gt;.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="66156-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="66156-130">\* (comodín)</span><span class="sxs-lookup"><span data-stu-id="66156-130">\* (wildcard)</span></span> | <span data-ttu-id="66156-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="66156-131">_awverify.\*_</span></span> | <span data-ttu-id="66156-132">_&lt;nombreaplic&gt;.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="66156-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="66156-133">En la página de registros DNS, tenga en cuenta los tipo de registro de hello de hello nombre DNS que desea toomigrate.</span><span class="sxs-lookup"><span data-stu-id="66156-133">In your DNS records page, note hello record type of hello DNS name you want toomigrate.</span></span> <span data-ttu-id="66156-134">App Service es compatible con las asignaciones de CNAME y registros A.</span><span class="sxs-lookup"><span data-stu-id="66156-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-hello-domain-for-your-app"></a><span data-ttu-id="66156-135">Habilitar el dominio de hello para la aplicación</span><span class="sxs-lookup"><span data-stu-id="66156-135">Enable hello domain for your app</span></span>

<span data-ttu-id="66156-136">Hola [portal de Azure](https://portal.azure.com), en Hola de navegación izquierdo de la página de la aplicación hello, seleccione **los dominios personalizados**.</span><span class="sxs-lookup"><span data-stu-id="66156-136">In hello [Azure portal](https://portal.azure.com), in hello left navigation of hello app page, select **Custom domains**.</span></span> 

![Menú Dominio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="66156-138">Hola **los dominios personalizados** página, seleccione hello  **+**  icono siguiente demasiado**Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="66156-138">In hello **Custom domains** page, select hello **+** icon next too**Add hostname**.</span></span>

![Agregar nombre de host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="66156-140">Nombre de dominio completo de tipo hello que agregó el registro TXT de hello, como `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="66156-140">Type hello fully qualified domain name that you added hello TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="66156-141">Para un dominio con caracteres comodín (como \*. contoso.com), puede utilizar cualquier nombre DNS que coincide con el dominio comodín Hola.</span><span class="sxs-lookup"><span data-stu-id="66156-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches hello wildcard domain.</span></span> 

<span data-ttu-id="66156-142">Seleccione **Validar**.</span><span class="sxs-lookup"><span data-stu-id="66156-142">Select **Validate**.</span></span>

<span data-ttu-id="66156-143">Hola **Agregar nombre de host** se activa el botón.</span><span class="sxs-lookup"><span data-stu-id="66156-143">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="66156-144">Asegúrese de que **tipo de registro de nombre de host** se establece los tipo de registro de DNS de toohello desea toomigrate.</span><span class="sxs-lookup"><span data-stu-id="66156-144">Make sure that **Hostname record type** is set toohello DNS record type you want toomigrate.</span></span>

<span data-ttu-id="66156-145">Seleccione **Agregar nombre de host**.</span><span class="sxs-lookup"><span data-stu-id="66156-145">Select **Add hostname**.</span></span>

![Agregar aplicación de toohello de nombre DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="66156-147">Puede tardar algún tiempo Hola nuevo nombre de host toobe reflejado en la aplicación hello **los dominios personalizados** página.</span><span class="sxs-lookup"><span data-stu-id="66156-147">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="66156-148">Intente actualizar los datos de saludo explorador tooupdate Hola.</span><span class="sxs-lookup"><span data-stu-id="66156-148">Try refreshing hello browser tooupdate hello data.</span></span>

![Registro CNAME agregado](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="66156-150">El nombre DNS personalizado ya estará habilitado en la aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="66156-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-hello-active-dns-name"></a><span data-ttu-id="66156-151">Asignar nombre de DNS de active Hola</span><span class="sxs-lookup"><span data-stu-id="66156-151">Remap hello active DNS name</span></span>

<span data-ttu-id="66156-152">Hello solo lo izquierdo toodo es reasignación su tooApp de toopoint registros DNS servicio activo.</span><span class="sxs-lookup"><span data-stu-id="66156-152">hello only thing left toodo is remapping your active DNS record toopoint tooApp Service.</span></span> <span data-ttu-id="66156-153">Derecha ahora, todavía señala tooyour del sitio antiguo.</span><span class="sxs-lookup"><span data-stu-id="66156-153">Right now, it still points tooyour old site.</span></span>

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a><span data-ttu-id="66156-154">Copie la dirección IP de la aplicación hello (solo para un registro)</span><span class="sxs-lookup"><span data-stu-id="66156-154">Copy hello app's IP address (A record only)</span></span>

<span data-ttu-id="66156-155">Si va a reasignar un registro CNAME, omita esta sección.</span><span class="sxs-lookup"><span data-stu-id="66156-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="66156-156">tooremap un registro, deberá dirección IP externa de la aplicación de servicio de aplicaciones de hello, que se muestra en hello **los dominios personalizados** página.</span><span class="sxs-lookup"><span data-stu-id="66156-156">tooremap an A record, you need hello App Service app's external IP address, which is shown in hello **Custom domains** page.</span></span>

<span data-ttu-id="66156-157">Hola cerrar **Agregar nombre de host** página seleccionando **X** en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="66156-157">Close hello **Add hostname** page by selecting **X** in hello upper-right corner.</span></span> 

<span data-ttu-id="66156-158">Hola **los dominios personalizados** página, copie la dirección IP de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="66156-158">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![Aplicación de navegación del portal tooAzure](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a><span data-ttu-id="66156-160">Actualizar el registro de DNS de Hola</span><span class="sxs-lookup"><span data-stu-id="66156-160">Update hello DNS record</span></span>

<span data-ttu-id="66156-161">Nuevo en la página de registros DNS de Hola de su proveedor de dominio, seleccione tooremap de registro de DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="66156-161">Back in hello DNS records page of your domain provider, select hello DNS record tooremap.</span></span>

<span data-ttu-id="66156-162">Para hello `contoso.com` raíz del ejemplo de un dominio, vuelva a asignar un registro A o CNAME hello como hello en los ejemplos de hello en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="66156-162">For hello `contoso.com` root domain example, remap hello A or CNAME record like hello examples in hello following table:</span></span> 

| <span data-ttu-id="66156-163">Ejemplo de FQDN</span><span class="sxs-lookup"><span data-stu-id="66156-163">FQDN example</span></span> | <span data-ttu-id="66156-164">Tipo de registro</span><span class="sxs-lookup"><span data-stu-id="66156-164">Record type</span></span> | <span data-ttu-id="66156-165">Host</span><span class="sxs-lookup"><span data-stu-id="66156-165">Host</span></span> | <span data-ttu-id="66156-166">Valor</span><span class="sxs-lookup"><span data-stu-id="66156-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="66156-167">contoso.com (raíz)</span><span class="sxs-lookup"><span data-stu-id="66156-167">contoso.com (root)</span></span> | <span data-ttu-id="66156-168">Una </span><span class="sxs-lookup"><span data-stu-id="66156-168">A</span></span> | `@` | <span data-ttu-id="66156-169">Dirección IP de [dirección IP de la aplicación de copia Hola](#info)</span><span class="sxs-lookup"><span data-stu-id="66156-169">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="66156-170">www.contoso.com (sub)</span><span class="sxs-lookup"><span data-stu-id="66156-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="66156-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="66156-171">CNAME</span></span> | `www` | <span data-ttu-id="66156-172">_&lt;nombreaplic&gt;.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="66156-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="66156-173">\*.contoso.com (comodín)</span><span class="sxs-lookup"><span data-stu-id="66156-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="66156-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="66156-174">CNAME</span></span> | _\*_ | <span data-ttu-id="66156-175">_&lt;nombreaplic&gt;.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="66156-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="66156-176">Guarde la configuración.</span><span class="sxs-lookup"><span data-stu-id="66156-176">Save your settings.</span></span>

<span data-ttu-id="66156-177">Consultas de DNS deben comenzar a resolver tooyour aplicación de servicio de aplicaciones inmediatamente después de que ocurra la propagación de DNS.</span><span class="sxs-lookup"><span data-stu-id="66156-177">DNS queries should start resolving tooyour App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66156-178">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="66156-178">Next steps</span></span>

<span data-ttu-id="66156-179">Obtenga información acerca de cómo toobind un personalizado SSL certificate tooApp servicio.</span><span class="sxs-lookup"><span data-stu-id="66156-179">Learn how toobind a custom SSL certificate tooApp Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="66156-180">Enlazar un tooAzure de certificado SSL personalizado aplicaciones Web existente</span><span class="sxs-lookup"><span data-stu-id="66156-180">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
