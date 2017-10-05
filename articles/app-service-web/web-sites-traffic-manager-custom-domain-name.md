---
title: "Configuración de un nombre de dominio personalizado para una aplicación web en Servicio de aplicaciones de Azure que usa el Administrador de tráfico para el equilibrio de carga."
description: "Use un nombre de dominio personalizado para un una aplicación web en el Servicio de aplicaciones de Azure que incluya el Administrador de tráfico para el equilibrio de carga."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 5f099201d9018a6f8577cb3daf127d09560fb94b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="53f4e-103">Configuración de un nombre de dominio personalizado para una aplicación web en Servicio de aplicaciones de Azure utilizando el Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="53f4e-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="53f4e-104">En este artículo se ofrecen instrucciones generales para usar un nombre de dominio personalizado con el Servicio de aplicaciones de Azure que usa el Administrador de tráfico para el equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="53f4e-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="53f4e-105">Descripción de los registros DNS</span><span class="sxs-lookup"><span data-stu-id="53f4e-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="53f4e-106">Configuración de las aplicaciones web para el modo estándar</span><span class="sxs-lookup"><span data-stu-id="53f4e-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="53f4e-107">Incorporación de un registro DNS para el dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="53f4e-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="53f4e-108">Si ha adquirido el dominio a través de Aplicaciones web del Servicio de aplicaciones de Azure, omita los pasos siguientes y consulte el paso final del artículo [Comprar dominio para Aplicaciones web](custom-dns-web-site-buydomains-web-app.md) .</span><span class="sxs-lookup"><span data-stu-id="53f4e-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="53f4e-109">Para asociar su dominio personalizado con una aplicación web del Servicio de aplicaciones de Azure, debe agregar una nueva entrada en la tabla DNS para el dominio personalizado mediante las herramientas proporcionadas por el registrador de dominios al que ha adquirido su nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="53f4e-109">To associate your custom domain with a web app in Azure App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by the domain registrar that you purchased your domain name from.</span></span> <span data-ttu-id="53f4e-110">Siga estos pasos para ubicar y utilizar las herramientas DNS.</span><span class="sxs-lookup"><span data-stu-id="53f4e-110">Use the following steps to locate and use the DNS tools.</span></span>

1. <span data-ttu-id="53f4e-111">Inicie sesión en su cuenta en el registrador de dominios y busque la página de administración de los registros DNS.</span><span class="sxs-lookup"><span data-stu-id="53f4e-111">Sign in to your account at your domain registrar, and look for a page for managing DNS records.</span></span> <span data-ttu-id="53f4e-112">Busque los vínculos o áreas del sitio etiquetados como **Nombre de dominio**, **DNS** o **Administración del servidor de nombres**.</span><span class="sxs-lookup"><span data-stu-id="53f4e-112">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="53f4e-113">A menudo se puede encontrar un vínculo a esta página al consultar la información de la cuenta y al buscar un vínculo como **Mis dominios**.</span><span class="sxs-lookup"><span data-stu-id="53f4e-113">Often a link to this page can be found be viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="53f4e-114">Cuando haya encontrado la página de administración para su nombre de dominio, busque un vínculo que le permita modificar los registros DNS.</span><span class="sxs-lookup"><span data-stu-id="53f4e-114">Once you have found the management page for your domain name, look for a link that allows you to edit the DNS records.</span></span> <span data-ttu-id="53f4e-115">Debe aparecer como **archivo Zona**, **Registros DNS** o como un vínculo de configuración de **Opciones avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="53f4e-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span></span>
   
   * <span data-ttu-id="53f4e-116">Esta página seguramente mostrará algunos que ya se han creado, como una entrada en la que se asocia "**@**" o "\*" a una página donde figuran los dominios.</span><span class="sxs-lookup"><span data-stu-id="53f4e-116">The page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span></span> <span data-ttu-id="53f4e-117">Es posible también que contenga registros para los subdominios más comunes, como **www**.</span><span class="sxs-lookup"><span data-stu-id="53f4e-117">It may also contain records for common sub-domains such as **www**.</span></span>
   * <span data-ttu-id="53f4e-118">Esta página mencionará los **registros CNAME**, o bien facilitará una lista desplegable donde podrá seleccionar un tipo de registro.</span><span class="sxs-lookup"><span data-stu-id="53f4e-118">The page will mention **CNAME records**, or provide a drop-down to select a record type.</span></span> <span data-ttu-id="53f4e-119">También es posible que mencione otros registros, como los **registros A** y los **registros MX**.</span><span class="sxs-lookup"><span data-stu-id="53f4e-119">It may also mention other records such as **A records** and **MX records**.</span></span> <span data-ttu-id="53f4e-120">En algunos casos, los registros CNAME tendrán otros nombres, como **Registro de Alias**.</span><span class="sxs-lookup"><span data-stu-id="53f4e-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span></span>
   * <span data-ttu-id="53f4e-121">Esta página contendrá también campos que le permiten **asignar** desde un **nombre de host** o un **nombre de dominio** hasta otro nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="53f4e-121">The page will also have fields that allow you to **map** from a **Host name** or **Domain name** to another domain name.</span></span>
3. <span data-ttu-id="53f4e-122">Aunque los detalles varían en función del registrador que se esté utilizando, en general se asigna *desde* el nombre del dominio personalizado (como **contoso.com**,) *hasta* el nombre de dominio de Traffic Manager (**contoso.trafficmanager.net**) usado para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="53f4e-122">While the specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* the Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="53f4e-123">Como alternativa, si un registro ya se está usando y necesita enlazar de forma preferente sus aplicaciones a él, puede crear otro registro CNAME.</span><span class="sxs-lookup"><span data-stu-id="53f4e-123">Alternatively, if a record is already in use and you need to preemptively bind your apps to it, you can create an additional CNAME record.</span></span> <span data-ttu-id="53f4e-124">Por ejemplo, para enlazar de forma preferente **www.contoso.com** a su aplicación web, cree un registro CNAME de **awverify.www** a **contoso.trafficmanager.net**.</span><span class="sxs-lookup"><span data-stu-id="53f4e-124">For example, to preemptively bind **www.contoso.com** to your web app, create a CNAME record from **awverify.www** to **contoso.trafficmanager.net**.</span></span> <span data-ttu-id="53f4e-125">Después, puede agregar "www.contoso.com" a la aplicación web sin cambiar el registro CNAME de "www".</span><span class="sxs-lookup"><span data-stu-id="53f4e-125">You can then add "www.contoso.com" to your Web App without changing the "www" CNAME record.</span></span> <span data-ttu-id="53f4e-126">Para más información, consulte [Creación de registros DNS para una aplicación web en un dominio personalizado][CREATEDNS].</span><span class="sxs-lookup"><span data-stu-id="53f4e-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
   > 
   > 
4. <span data-ttu-id="53f4e-127">Una vez que haya terminado de agregar o modificar registros DNS en su registrador, guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="53f4e-127">Once you have finished adding or modifying DNS records at your registrar, save the changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="53f4e-128">Habilitación del Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="53f4e-128">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="53f4e-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="53f4e-129">Next steps</span></span>
<span data-ttu-id="53f4e-130">Para más información, vea el [Centro para desarrolladores de Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="53f4e-130">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
