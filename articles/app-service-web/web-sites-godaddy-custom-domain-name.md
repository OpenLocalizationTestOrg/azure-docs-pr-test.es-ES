---
title: "aaaConfigure un nombre de dominio personalizado en el servicio de aplicación de Azure (GoDaddy)"
description: "Obtenga información acerca de cómo nombre toouse un dominio de GoDaddy con aplicaciones Web de Azure"
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="47314-103">Configuración de un nombre de dominio personalizado en Azure App Service (adquirido directamente de GoDaddy)</span><span class="sxs-lookup"><span data-stu-id="47314-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="47314-104">Si ha adquirido el dominio a través de aplicaciones de Web del servicio de aplicación de Azure, consulte toohello paso final de [comprar dominio para las aplicaciones Web](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="47314-104">If you have purchased domain through Azure App Service Web Apps then refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="47314-105">Este artículo ofrece instrucciones acerca del uso de un nombre de dominio personalizado adquirido directamente en [Go Daddy](https://godaddy.com) con [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="47314-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="47314-106">Descripción de los registros DNS</span><span class="sxs-lookup"><span data-stu-id="47314-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="47314-107">Incorporación de un registro DNS para el dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="47314-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="47314-108">tooassociate su dominio personalizado con una aplicación web en el servicio de aplicaciones, debe agregar una nueva entrada en la tabla de hello DNS para su dominio personalizado mediante el uso de herramientas proporcionadas por GoDaddy.</span><span class="sxs-lookup"><span data-stu-id="47314-108">tooassociate your custom domain with a web app in App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="47314-109">Usar hello siguiendo las herramientas DNS de pasos toolocate Hola para GoDaddy.com</span><span class="sxs-lookup"><span data-stu-id="47314-109">Use hello following steps toolocate hello DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="47314-110">Iniciar sesión en tooyour cuenta con GoDaddy.com y seleccione **mi cuenta** y, a continuación, **administrar Mis dominios**.</span><span class="sxs-lookup"><span data-stu-id="47314-110">Log on tooyour account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="47314-111">Menú de lista desplegable seleccione Hola Hola nombre de dominio que desea toouse con la aplicación web de Azure y seleccione **administrar DNS**.</span><span class="sxs-lookup"><span data-stu-id="47314-111">Select hello drop-down menu for hello domain name that you wish toouse with your Azure web app and select **Manage DNS**.</span></span>
   
    ![Página de dominio personalizado para GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="47314-113">De hello **detalles del dominio** página, desplácese toohello **archivo de zona DNS** ficha. Se trata de una sección de hello usado para agregar y modificar registros de DNS para el nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="47314-113">From hello **Domain details** page, scroll toohello **DNS Zone File** tab. This is hello section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![Pestaña de archivo de zona DNS](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="47314-115">Seleccione **Add Record** tooadd un registro existente.</span><span class="sxs-lookup"><span data-stu-id="47314-115">Select **Add Record** tooadd an existing record.</span></span>
   
    <span data-ttu-id="47314-116">demasiado**editar** un registro existente, el icono de lápiz y papel de hello seleccione situado junto al registro de hello.</span><span class="sxs-lookup"><span data-stu-id="47314-116">too**edit** an existing record, select hello pen & paper icon beside hello record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="47314-117">Antes de agregar nuevos registros, tenga en cuenta que GoDaddy ya ha creado registros DNS de subdominios populares (llamados **Host** en el editor), como **email**, **files**, **mail** y otros.</span><span class="sxs-lookup"><span data-stu-id="47314-117">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="47314-118">Si el nombre de hello desea toouse ya existe, modificar registro existente de hello en lugar de crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="47314-118">If hello name you wish toouse already exists, modify hello existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="47314-119">Al agregar un registro, primero debe seleccionar el tipo de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="47314-119">When adding a record, you must first select hello record type.</span></span>
   
    ![seleccione el tipo de registro](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="47314-121">A continuación, debe proporcionar hello **Host** (Hola personalizado dominio o subdominio) y lo que **apunta a**.</span><span class="sxs-lookup"><span data-stu-id="47314-121">Next, you must provide hello **Host** (hello custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![agregue un registro de zona.](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="47314-123">Cuando se agrega un **un registro (host)** -debe establecer hello **Host** campo tooeither  **@**  (Esto representa como nombre del dominio raíz,  **contoso.com**,) * (un carácter comodín para la coincidencia de varios subdominios) u Hola subdominio que se va a toouse (por ejemplo, **www**.) Debe establecer hello **apunta a** campo toohello dirección IP de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="47314-123">When adding an **A (host) record** - you must set hello **Host** field tooeither **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or hello sub-domain you wish toouse (for example, **www**.) You must set hello **Points to** field toohello IP address of your Azure web app.</span></span>
   * <span data-ttu-id="47314-124">Cuando se agrega un **registro CNAME (alias)** -debe establecer hello **Host** campo toohello subdominio que se va toouse.</span><span class="sxs-lookup"><span data-stu-id="47314-124">When adding a **CNAME (alias) record** - you must set hello **Host** field toohello sub-domain you wish toouse.</span></span> <span data-ttu-id="47314-125">Por ejemplo, **www**.</span><span class="sxs-lookup"><span data-stu-id="47314-125">For example, **www**.</span></span> <span data-ttu-id="47314-126">Debe establecer hello **apunta a** campo toohello **. azurewebsites.net** nombre de dominio de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="47314-126">You must set hello **Points to** field toohello **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="47314-127">Por ejemplo, **contoso.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="47314-127">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="47314-128">Haga clic en **Agregar otro**.</span><span class="sxs-lookup"><span data-stu-id="47314-128">Click **Add Another**.</span></span>
5. <span data-ttu-id="47314-129">Seleccione **TXT** como tipo de registro de hello, a continuación, especifique un **Host** valo  **@**  y un **apunta a** valo  **&lt;yourwebappname&gt;. azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="47314-129">Select **TXT** as hello record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="47314-130">Este registro TXT se usa por Azure toovalidate que posee el dominio Hola descrito por hello un registro TXT primer registro u Hola.</span><span class="sxs-lookup"><span data-stu-id="47314-130">This TXT record is used by Azure toovalidate that you own hello domain described by hello A record or hello first TXT record.</span></span> <span data-ttu-id="47314-131">Una vez que el dominio de hello ha sido asignada toohello web aplicación Hola Portal de Azure, se puede quitar esta entrada de registro TXT.</span><span class="sxs-lookup"><span data-stu-id="47314-131">Once hello domain has been mapped toohello web app in hello Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="47314-132">Cuando haya terminado de agregar o modificar registros, haga clic en **finalizar** toosave cambios.</span><span class="sxs-lookup"><span data-stu-id="47314-132">When you have finished adding or modifying records, click **Finish** toosave changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a><span data-ttu-id="47314-133">Habilitar el nombre de dominio de hello en la aplicación web</span><span class="sxs-lookup"><span data-stu-id="47314-133">Enable hello domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="47314-134">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="47314-134">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="47314-135">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="47314-135">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="47314-136">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="47314-136">What's changed</span></span>
* <span data-ttu-id="47314-137">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="47314-137">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

