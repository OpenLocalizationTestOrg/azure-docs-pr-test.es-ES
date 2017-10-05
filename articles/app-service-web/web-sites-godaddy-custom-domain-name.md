---
title: "Configuración de un nombre de dominio personalizado en Azure App Service (GoDaddy)"
description: "Obtenga información acerca de cómo usar un nombre de dominio de GoDaddy con Azure Web Apps"
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
ms.openlocfilehash: 158c5dc06f83e16633d3c2fbb4eb27d3e8af030c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="a1c36-103">Configuración de un nombre de dominio personalizado en Azure App Service (adquirido directamente de GoDaddy)</span><span class="sxs-lookup"><span data-stu-id="a1c36-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="a1c36-104">Si ha adquirido el dominio a través de Azure App Service Web Apps, consulte el paso final de [Comprar dominio para Web Apps](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="a1c36-104">If you have purchased domain through Azure App Service Web Apps then refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="a1c36-105">Este artículo ofrece instrucciones acerca del uso de un nombre de dominio personalizado adquirido directamente en [Go Daddy](https://godaddy.com) con [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="a1c36-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="a1c36-106">Descripción de los registros DNS</span><span class="sxs-lookup"><span data-stu-id="a1c36-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="a1c36-107">Incorporación de un registro DNS para el dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="a1c36-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="a1c36-108">Para asociar el dominio personalizado a una aplicación web de App Service, debe agregar una nueva entrada en la tabla DNS para su dominio personalizado usando las herramientas proporcionadas por GoDaddy.</span><span class="sxs-lookup"><span data-stu-id="a1c36-108">To associate your custom domain with a web app in App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="a1c36-109">Utilice los pasos siguientes para localizar las herramientas DNS de GoDaddy.com.</span><span class="sxs-lookup"><span data-stu-id="a1c36-109">Use the following steps to locate the DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="a1c36-110">Inicie sesión en su cuenta con GoDaddy.com, seleccione **My Account** (Mi cuenta) y, a continuación, **Manage my domains** (Administrar mis dominios).</span><span class="sxs-lookup"><span data-stu-id="a1c36-110">Log on to your account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="a1c36-111">Seleccione el menú desplegable del nombre de dominio que quiere usar con la aplicación web de Azure y seleccione **Administrar DNS**.</span><span class="sxs-lookup"><span data-stu-id="a1c36-111">Select the drop-down menu for the domain name that you wish to use with your Azure web app and select **Manage DNS**.</span></span>
   
    ![Página de dominio personalizado para GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="a1c36-113">En la página **Domain details** (Detalles de dominio), desplácese a la pestaña **DNS Zone File** (Archivo de zona DNS).</span><span class="sxs-lookup"><span data-stu-id="a1c36-113">From the **Domain details** page, scroll to the **DNS Zone File** tab.</span></span> <span data-ttu-id="a1c36-114">Esta es la sección que se utiliza para agregar y modificar los registros DNS para el nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="a1c36-114">This is the section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![Pestaña de archivo de zona DNS](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="a1c36-116">Seleccione **Add Record** (Agregar registro) para agregar un registro existente.</span><span class="sxs-lookup"><span data-stu-id="a1c36-116">Select **Add Record** to add an existing record.</span></span>
   
    <span data-ttu-id="a1c36-117">Seleccione el icono de lápiz y papel junto al registro para **editar** un registro existente.</span><span class="sxs-lookup"><span data-stu-id="a1c36-117">To **edit** an existing record, select the pen & paper icon beside the record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a1c36-118">Antes de agregar nuevos registros, tenga en cuenta que GoDaddy ya ha creado registros DNS de subdominios populares (llamados **Host** en el editor), como **email**, **files**, **mail** y otros.</span><span class="sxs-lookup"><span data-stu-id="a1c36-118">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="a1c36-119">Si el nombre que desea utilizar ya existe, modifique el registro actual en lugar de crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="a1c36-119">If the name you wish to use already exists, modify the existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="a1c36-120">Al agregar un registro, primero debe seleccionar el tipo de registro.</span><span class="sxs-lookup"><span data-stu-id="a1c36-120">When adding a record, you must first select the record type.</span></span>
   
    ![seleccione el tipo de registro](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="a1c36-122">A continuación, debe proporcionar el **Host** (el subdominio o dominio personalizado) y a qué **apunta**.</span><span class="sxs-lookup"><span data-stu-id="a1c36-122">Next, you must provide the **Host** (the custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![agregue un registro de zona.](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="a1c36-124">Al agregar un **registro A (host)**, se debe establecer el campo **Host** en **@** (esto representa el nombre de dominio raíz, como **contoso.com**), * (un comodín para que se corresponda con varios subdominios) o el subdominio que quiere usar (por ejemplo, **www**). Debe establecer el campo **Apunta a** en la dirección IP de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1c36-124">When adding an **A (host) record** - you must set the **Host** field to either **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or the sub-domain you wish to use (for example, **www**.) You must set the **Points to** field to the IP address of your Azure web app.</span></span>
   * <span data-ttu-id="a1c36-125">Al agregar un **registro CNAME (alias)**, debe configurar el campo **Host** en el subdominio que desee usar.</span><span class="sxs-lookup"><span data-stu-id="a1c36-125">When adding a **CNAME (alias) record** - you must set the **Host** field to the sub-domain you wish to use.</span></span> <span data-ttu-id="a1c36-126">Por ejemplo, **www**.</span><span class="sxs-lookup"><span data-stu-id="a1c36-126">For example, **www**.</span></span> <span data-ttu-id="a1c36-127">Debe definir el campo **Points to** en el nombre de dominio **.azurewebsites.net** de su aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1c36-127">You must set the **Points to** field to the **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="a1c36-128">Por ejemplo, **contoso.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="a1c36-128">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="a1c36-129">Haga clic en **Agregar otro**.</span><span class="sxs-lookup"><span data-stu-id="a1c36-129">Click **Add Another**.</span></span>
5. <span data-ttu-id="a1c36-130">Seleccione **TXT** como el tipo de registro, a continuación, especifique un valor de **Host** de **@** y un valor de **Points to** (Apunta a) de **&lt;yourwebappname&gt;.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="a1c36-130">Select **TXT** as the record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a1c36-131">Azure usa este registro TXT para comprobar que el dominio descrito por el registro A o el primer registro TXT es en efecto suyo.</span><span class="sxs-lookup"><span data-stu-id="a1c36-131">This TXT record is used by Azure to validate that you own the domain described by the A record or the first TXT record.</span></span> <span data-ttu-id="a1c36-132">Una vez que el dominio se haya asignado a la aplicación web en Azure Portal, se podrá eliminar la entrada del registro TXT.</span><span class="sxs-lookup"><span data-stu-id="a1c36-132">Once the domain has been mapped to the web app in the Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="a1c36-133">Cuando haya terminado de agregar o modificar los registros, haga clic en **Finish** (Finalizar) para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="a1c36-133">When you have finished adding or modifying records, click **Finish** to save changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-the-domain-name-on-your-web-app"></a><span data-ttu-id="a1c36-134">Habilitación del nombre de dominio en su aplicación web</span><span class="sxs-lookup"><span data-stu-id="a1c36-134">Enable the domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="a1c36-135">Si desea empezar a trabajar con Azure App Service antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba de App Service](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en App Service.</span><span class="sxs-lookup"><span data-stu-id="a1c36-135">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a1c36-136">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="a1c36-136">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="a1c36-137">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="a1c36-137">What's changed</span></span>
* <span data-ttu-id="a1c36-138">Para obtener una guía del cambio de Websites a App Service, consulte: [Azure App Service y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="a1c36-138">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

