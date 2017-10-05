---
title: "Configuración de un nombre de dominio personalizado en Cloud Services | Microsoft Docs"
description: "Aprenda a exponer su aplicación o sus datos de Azure en Internet en un dominio personalizado mediante la configuración de sus valores DNS.  Estos ejemplos usan el Portal de Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: cf43d86dddc3a68573e1ba1b09118c54f0b16bc5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="35c6c-104">Configuración de un nombre de dominio personalizado para un servicio en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="35c6c-104">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="35c6c-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="35c6c-105">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="35c6c-106">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="35c6c-106">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="35c6c-107">Cuando se crea un servicio en la nube, Azure lo asigna a un subdominio de **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="35c6c-107">When you create a Cloud Service, Azure assigns it to a subdomain of **cloudapp.net**.</span></span> <span data-ttu-id="35c6c-108">Por ejemplo, si el nombre del servicio en la nube es "contoso", los usuarios podrán tener acceso a la aplicación en una dirección URL como http://contoso.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="35c6c-108">For example, if your Cloud Service is named "contoso", your users will be able to access your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="35c6c-109">Azure también asigna una dirección IP virtual.</span><span class="sxs-lookup"><span data-stu-id="35c6c-109">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="35c6c-110">Sin embargo, también puede exponer su aplicación en su propio nombre de dominio, como **contoso.com**. En este artículo se explica cómo reservar o configurar un nombre de dominio personalizado para los roles web de servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="35c6c-110">However, you can also expose your application on your own domain name, such as **contoso.com**. This article explains how to reserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="35c6c-111">¿Ya entiende qué son los registros CNAME y D?</span><span class="sxs-lookup"><span data-stu-id="35c6c-111">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="35c6c-112">[Omita la explicación](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="35c6c-112">[Jump past the explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="35c6c-113">Los procedimientos de esta tarea se aplican a los servicios en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="35c6c-113">The procedures in this task apply to Azure Cloud Services.</span></span> <span data-ttu-id="35c6c-114">Para Servicios de aplicaciones, consulte [este artículo](../app-service-web/web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="35c6c-114">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="35c6c-115">Para las cuentas de almacenamiento, consulte [este artículo](../storage/blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="35c6c-115">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

<p/>

> [!TIP]
> <span data-ttu-id="35c6c-116">Póngase en marcha más rápido: use el NUEVO [tutorial guiado](http://support.microsoft.com/kb/2990804)de Azure.</span><span class="sxs-lookup"><span data-stu-id="35c6c-116">Get going faster--use the NEW Azure [guided walkthrough](http://support.microsoft.com/kb/2990804)!</span></span>  <span data-ttu-id="35c6c-117">Con este tutorial, asociar un nombre de dominio personalizado y proteger las comunicaciones (SSL) con los servicios en la nube de Azure o Sitios web Azure es facilísimo.</span><span class="sxs-lookup"><span data-stu-id="35c6c-117">It makes associating a custom domain name AND securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="35c6c-118">Descripción de los registros D y CNAME</span><span class="sxs-lookup"><span data-stu-id="35c6c-118">Understand CNAME and A records</span></span>
<span data-ttu-id="35c6c-119">Los registros D y CNAME (o registros de alias) le permiten asociar un nombre de dominio a un servidor específico (o, en este caso, servicio). Sin embargo, cada uno funciona de manera distinta.</span><span class="sxs-lookup"><span data-stu-id="35c6c-119">CNAME (or alias records) and A records both allow you to associate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="35c6c-120">Existen también algunas consideraciones específicas al usar los registros D con los Servicios en la nube de Azure que debe considerar antes de decidir cuál usar.</span><span class="sxs-lookup"><span data-stu-id="35c6c-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which to use.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="35c6c-121">Registro de CNAME o Alias</span><span class="sxs-lookup"><span data-stu-id="35c6c-121">CNAME or Alias record</span></span>
<span data-ttu-id="35c6c-122">Un registro CNAME asigna un dominio *específico* , como **contoso.com** or **www.contoso.com**, a un nombre de dominio canónico.</span><span class="sxs-lookup"><span data-stu-id="35c6c-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, to a canonical domain name.</span></span> <span data-ttu-id="35c6c-123">En este caso, el nombre de dominio canónico es el nombre de dominio **[myapp].cloudapp.net** de su aplicación hospedada de Azure.</span><span class="sxs-lookup"><span data-stu-id="35c6c-123">In this case, the canonical domain name is the **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="35c6c-124">Una vez creado, el CNAME crea un alias para **[myapp].cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="35c6c-124">Once created, the CNAME creates an alias for the **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="35c6c-125">La entrada de CNAME se resolverá en la dirección IP del servicio de **[myapp].cloudapp.net** de manera automática, por lo que si la dirección IP del servicio en la nube cambia, no es preciso realizar ninguna acción.</span><span class="sxs-lookup"><span data-stu-id="35c6c-125">The CNAME entry will resolve to the IP address of your **[myapp].cloudapp.net** service automatically, so if the IP address of the cloud service changes, you do not have to take any action.</span></span>

> [!NOTE]
> <span data-ttu-id="35c6c-126">Algunos registradores de dominio solo permiten asignar subdominios cuando se utiliza un registro CNAME, como www.contoso.com, no nombres de raíz, como contoso.com. Para obtener más información acerca de los registros CNAME, consulte la documentación que proporciona el registrador, [la entrada de Wikipedia sobre el registro CNAME](http://en.wikipedia.org/wiki/CNAME_record) o el documento [Nombres de dominio IETF: implementación y especificación (en inglés)](http://tools.ietf.org/html/rfc1035).</span><span class="sxs-lookup"><span data-stu-id="35c6c-126">Some domain registrars only allow you to map subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see the documentation provided by your registrar, [the Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or the [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="35c6c-127">Registro D</span><span class="sxs-lookup"><span data-stu-id="35c6c-127">A record</span></span>
<span data-ttu-id="35c6c-128">El registro *D* asigna un dominio, como **contoso.com** o **www.contoso.com**, *o un nombre de dominio con comodín* como **\*.contoso.com**, a una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="35c6c-128">An *A* record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, to an IP address.</span></span> <span data-ttu-id="35c6c-129">En el caso de un servicio en la nube de Azure, la IP virtual del servicio.</span><span class="sxs-lookup"><span data-stu-id="35c6c-129">In the case of an Azure Cloud Service, the virtual IP of the service.</span></span> <span data-ttu-id="35c6c-130">Por lo tanto, el principal beneficio de un registro D en relación con un registro CNAME es que puede disponer de una entrada que utilice un carácter comodín, como \***.contoso.com**, que administraría las solicitudes de varios subdominios como **mail.contoso.com**, **login.contoso.com** o **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="35c6c-130">So the main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="35c6c-131">Puesto que un registro D se asigna a una dirección IP estática, no puede resolver automáticamente cambios en la dirección IP de su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="35c6c-131">Since an A record is mapped to a static IP address, it cannot automatically resolve changes to the IP address of your Cloud Service.</span></span> <span data-ttu-id="35c6c-132">La dirección IP que usa el Servicio en la nube se asigna la primera vez que se implementa en una ranura vacía (producción o ensayo). Si elimina la implementación para la ranura, Azure libera la dirección IP y a toda implementación posterior en la ranura se le podrá dar una dirección IP nueva.</span><span class="sxs-lookup"><span data-stu-id="35c6c-132">The IP address used by your Cloud Service is allocated the first time you deploy to an empty slot (either production or staging.) If you delete the deployment for the slot, the IP address is released by Azure and any future deployments to the slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="35c6c-133">De manera conveniente, la dirección IP de una ranura de implementación dada (producción o ensayo) se mantiene cuando se realiza un intercambio entre las implementaciones de ensayo y producción o se realiza una actualización local de una implementación existente.</span><span class="sxs-lookup"><span data-stu-id="35c6c-133">Conveniently, the IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="35c6c-134">Para obtener más información sobre la realización de estas acciones, consulte [Administración de servicios en la nube](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="35c6c-134">For more information on performing these actions, see [How to manage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="35c6c-135">Incorporación de un CNAME al dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="35c6c-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="35c6c-136">Para crear un registro CNAME, debe agregar una nueva entrada en la tabla DNS para el dominio personalizado mediante las herramientas proporcionadas por el registrador.</span><span class="sxs-lookup"><span data-stu-id="35c6c-136">To create a CNAME record, you must add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="35c6c-137">Cada registrador dispone de un método similar pero ligeramente distinto de especificación de un registro CNAME. Sin embargo, los conceptos son los mismos.</span><span class="sxs-lookup"><span data-stu-id="35c6c-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but the concepts are the same.</span></span>

1. <span data-ttu-id="35c6c-138">Use uno de estos métodos para buscar el nombre de dominio **.cloudapp.net** asignado a su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="35c6c-138">Use one of these methods to find the **.cloudapp.net** domain name assigned to your cloud service.</span></span>
   
   * <span data-ttu-id="35c6c-139">Inicie sesión en [Azure Portal], seleccione el servicio en la nube, busque la sección **Conceptos básicos** y, luego, busque la entrada **Dirección URL del sitio**.</span><span class="sxs-lookup"><span data-stu-id="35c6c-139">Login to the [Azure portal], select your cloud service, look at the **Essentials** section and then find the **Site URL** entry.</span></span>
     
       ![sección de vista rápida que muestra la dirección URL del sitio][csurl]
     
       <span data-ttu-id="35c6c-141">**O bien**</span><span class="sxs-lookup"><span data-stu-id="35c6c-141">**OR**</span></span>
   * <span data-ttu-id="35c6c-142">Instale y configure [Azure Powershell](/powershell/azure/overview)y, luego, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="35c6c-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="35c6c-143">Guarde el nombre de dominio que se usó en la URL devuelta por cualquier método, ya que lo necesitará al crear un registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="35c6c-143">Save the domain name used in the URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="35c6c-144">Inicie sesión en el sitio web del registrador DNS y vaya a la página de administración de DNS.</span><span class="sxs-lookup"><span data-stu-id="35c6c-144">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="35c6c-145">Busque los vínculos o áreas del sitio etiquetados como **Nombre de dominio**, **DNS** o **Administración del servidor de nombres**.</span><span class="sxs-lookup"><span data-stu-id="35c6c-145">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="35c6c-146">Ahora busque el lugar en el que puede seleccionar o especificar los registros CNAME.</span><span class="sxs-lookup"><span data-stu-id="35c6c-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="35c6c-147">Es posible que tenga que seleccionar el tipo de registro de un menú desplegable o ir a una página de configuración avanzada.</span><span class="sxs-lookup"><span data-stu-id="35c6c-147">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span> <span data-ttu-id="35c6c-148">Debe buscar las palabras **CNAME**, **Alias** o **Subdominios**.</span><span class="sxs-lookup"><span data-stu-id="35c6c-148">You should look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="35c6c-149">También debe proporcionar el alias del dominio o subdominio para el registro CNAME, como **www** si desea crear un alias para **www.customdomain.com**. Si desea crear un alias para el dominio raíz, puede enumerarse como el símbolo "**@**" en las herramientas de DNS del registrador.</span><span class="sxs-lookup"><span data-stu-id="35c6c-149">You must also provide the domain or subdomain alias for the CNAME, such as **www** if you want to create an alias for **www.customdomain.com**. If you want to create an alias for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="35c6c-150">A continuación, debe proporcionar un nombre de host canónico que, en este caso, es el dominio **cloudapp.net** de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="35c6c-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="35c6c-151">Por ejemplo, el siguiente registro CNAME reenvía todo el tráfico de **www.contoso.com** a **contoso.cloudapp.net**, el nombre de dominio personalizado de su aplicación implementada:</span><span class="sxs-lookup"><span data-stu-id="35c6c-151">For example, the following CNAME record forwards all traffic from **www.contoso.com** to **contoso.cloudapp.net**, the custom domain name of your deployed application:</span></span>

| <span data-ttu-id="35c6c-152">Alias/Nombre de host/Subdominio</span><span class="sxs-lookup"><span data-stu-id="35c6c-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="35c6c-153">Dominio canónico</span><span class="sxs-lookup"><span data-stu-id="35c6c-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="35c6c-154">www</span><span class="sxs-lookup"><span data-stu-id="35c6c-154">www</span></span> |<span data-ttu-id="35c6c-155">contoso.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="35c6c-155">contoso.cloudapp.net</span></span> |

> [!NOTE]
> <span data-ttu-id="35c6c-156">Los visitantes de **www.contoso.com** no verán nunca el verdadero host (contoso.cloudapp.net), por lo que el usuario final no percibirá el proceso de desvío.</span><span class="sxs-lookup"><span data-stu-id="35c6c-156">A visitor of **www.contoso.com** will never see the true host (contoso.cloudapp.net), so the forwarding process is invisible to the end user.</span></span>
> 
> <span data-ttu-id="35c6c-157">El ejemplo anterior solo se aplica al tráfico en el subdominio **www** .</span><span class="sxs-lookup"><span data-stu-id="35c6c-157">The example above only applies to traffic at the **www** subdomain.</span></span> <span data-ttu-id="35c6c-158">Puesto que no puede usar caracteres comodín con registros CNAME, debe crear un CNAME para cada dominio/subdominio.</span><span class="sxs-lookup"><span data-stu-id="35c6c-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="35c6c-159">Si desea dirigir el tráfico desde subdominios, como *.contoso.com, a su dirección cloudapp.net, puede configurar una entrada **Redirección de URL** o **Desvío de URL en la configuración de DNS** o crear un registro D.</span><span class="sxs-lookup"><span data-stu-id="35c6c-159">If you want to direct  traffic from subdomains, such as *.contoso.com, to your cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="35c6c-160">Agregar un registro D para el dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="35c6c-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="35c6c-161">Para crear un registro D, primero debe buscar la dirección IP virtual de su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="35c6c-161">To create an A record, you must first find the virtual IP address of your cloud service.</span></span> <span data-ttu-id="35c6c-162">A continuación, agregue una entrada en la tabla DNS para el dominio personalizado mediante las herramientas proporcionadas por el registrador.</span><span class="sxs-lookup"><span data-stu-id="35c6c-162">Then add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="35c6c-163">Cada registrador dispone de un método similar pero ligeramente distinto de especificación de un registro D. Sin embargo, los conceptos son los mismos.</span><span class="sxs-lookup"><span data-stu-id="35c6c-163">Each registrar has a similar but slightly different method of specifying an A record, but the concepts are the same.</span></span>

1. <span data-ttu-id="35c6c-164">Use uno de los siguientes métodos para obtener la dirección IP de su servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="35c6c-164">Use one of the following methods to get the IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="35c6c-165">Inicie sesión en [Azure Portal], seleccione el servicio en la nube, busque la sección **Conceptos básicos** y, a continuación, busque la entrada **Direcciones IP públicas**.</span><span class="sxs-lookup"><span data-stu-id="35c6c-165">Login to the [Azure portal], select your cloud service, look at the **Essentials** section and then find the **Public IP addresses** entry.</span></span>
     
       ![sección de vista rápida que muestra la IP virtual][vip]
     
       <span data-ttu-id="35c6c-167">**O bien**</span><span class="sxs-lookup"><span data-stu-id="35c6c-167">**OR**</span></span>
   * <span data-ttu-id="35c6c-168">Instale y configure [Azure Powershell](/powershell/azure/overview)y, luego, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="35c6c-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="35c6c-169">Guarde la dirección IP, debido a que la necesitará cuando cree un registro D.</span><span class="sxs-lookup"><span data-stu-id="35c6c-169">Save the IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="35c6c-170">Inicie sesión en el sitio web del registrador DNS y vaya a la página de administración de DNS.</span><span class="sxs-lookup"><span data-stu-id="35c6c-170">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="35c6c-171">Busque los vínculos o áreas del sitio etiquetados como **Nombre de dominio**, **DNS** o **Administración del servidor de nombres**.</span><span class="sxs-lookup"><span data-stu-id="35c6c-171">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="35c6c-172">Ahora busque el lugar en el que puede seleccionar o especificar los registros D.</span><span class="sxs-lookup"><span data-stu-id="35c6c-172">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="35c6c-173">Es posible que tenga que seleccionar el tipo de registro de un menú desplegable o ir a una página de configuración avanzada.</span><span class="sxs-lookup"><span data-stu-id="35c6c-173">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span>
4. <span data-ttu-id="35c6c-174">Seleccione o especifique el dominio o subdominio que usará el registro D.</span><span class="sxs-lookup"><span data-stu-id="35c6c-174">Select or enter the domain or subdomain that will use this A record.</span></span> <span data-ttu-id="35c6c-175">Por ejemplo, seleccione **www** si desea crear un alias para **www.customdomain.com**. Si desea crear una entrada de comodín para todos los subdominios, especifique '*****'.</span><span class="sxs-lookup"><span data-stu-id="35c6c-175">For example, select **www** if you want to create an alias for **www.customdomain.com**. If you want to create a wildcard entry for all subdomains, enter '*****'.</span></span> <span data-ttu-id="35c6c-176">De esta forma, se incluirán todos los subdominios como **mail.customdomain.com**, **login.customdomain.com** y **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="35c6c-176">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="35c6c-177">Si desea crear un registro D para el dominio raíz, puede enumerarse como el símbolo "**@**" en las herramientas de DNS del registrador.</span><span class="sxs-lookup"><span data-stu-id="35c6c-177">If you want to create an A record for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="35c6c-178">Especifique la dirección IP del servicio en la nube en el campo proporcionado.</span><span class="sxs-lookup"><span data-stu-id="35c6c-178">Enter the IP address of your cloud service in the provided field.</span></span> <span data-ttu-id="35c6c-179">De esta forma, se asocia la entrada del dominio utilizada en el registro D a la dirección IP de la implementación del servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="35c6c-179">This associates the domain entry used in the A record with the IP address of your cloud service deployment.</span></span>

<span data-ttu-id="35c6c-180">Por ejemplo, el siguiente registro D desvía todo el tráfico de **contoso.com** a **137.135.70.239**, la dirección IP de su aplicación implementada:</span><span class="sxs-lookup"><span data-stu-id="35c6c-180">For example, the following A record forwards all traffic from **contoso.com** to **137.135.70.239**, the IP address of your deployed application:</span></span>

| <span data-ttu-id="35c6c-181">Nombre de host/Subdominio</span><span class="sxs-lookup"><span data-stu-id="35c6c-181">Host name/Subdomain</span></span> | <span data-ttu-id="35c6c-182">Dirección IP</span><span class="sxs-lookup"><span data-stu-id="35c6c-182">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="35c6c-183">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="35c6c-183">137.135.70.239</span></span> |

<span data-ttu-id="35c6c-184">En este ejemplo se crea un registro D para el dominio raíz.</span><span class="sxs-lookup"><span data-stu-id="35c6c-184">This example demonstrates creating an A record for the root domain.</span></span> <span data-ttu-id="35c6c-185">Si desea crear una entrada de comodín para incluir todos los subdominios, debe especificar '*****' como subdominio.</span><span class="sxs-lookup"><span data-stu-id="35c6c-185">If you wish to create a wildcard entry to cover all subdomains, you would enter '*****' as the subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="35c6c-186">Las direcciones IP en Azure son dinámicas de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="35c6c-186">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="35c6c-187">Probablemente querrá usar una [dirección IP reservada](../virtual-network/virtual-networks-reserved-public-ip.md) para asegurarse de que la dirección IP no cambia.</span><span class="sxs-lookup"><span data-stu-id="35c6c-187">You will probably want to use a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) to ensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="35c6c-188">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="35c6c-188">Next steps</span></span>
* [<span data-ttu-id="35c6c-189">Administración de servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="35c6c-189">How to Manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="35c6c-190">Asignación del contenido de la red CDN a un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="35c6c-190">How to Map CDN Content to a Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="35c6c-191">[Configuración general de su servicio en la nube](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="35c6c-191">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="35c6c-192">Obtenga información sobre cómo [implementar un servicio en la nube](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="35c6c-192">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="35c6c-193">Configuración de [certificados ssl](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="35c6c-193">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates the subdomain with the storage account]: #create-cname
[Azure Portal]: https://portal.azure.com
[vip]: ./media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name-portal/csurl.png
