---
title: "aaaConfigure un nombre de dominio personalizado para una aplicación web en el servicio de aplicaciones de Azure que utiliza el Administrador de tráfico de equilibrio de carga."
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
ms.openlocfilehash: dfde5fc6b445b30b10e03dcb03e8d072130d9377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="5f156-103">Configuración de un nombre de dominio personalizado para una aplicación web en Servicio de aplicaciones de Azure utilizando el Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="5f156-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="5f156-104">En este artículo se ofrecen instrucciones generales para usar un nombre de dominio personalizado con el Servicio de aplicaciones de Azure que usa el Administrador de tráfico para el equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="5f156-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="5f156-105">Descripción de los registros DNS</span><span class="sxs-lookup"><span data-stu-id="5f156-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="5f156-106">Configuración de las aplicaciones web para el modo estándar</span><span class="sxs-lookup"><span data-stu-id="5f156-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="5f156-107">Incorporación de un registro DNS para el dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="5f156-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="5f156-108">Si ha adquirido el dominio a través de aplicaciones de Web del servicio de aplicación de Azure, a continuación, omita los pasos y consulte toohello paso final de [comprar dominio para las aplicaciones Web](custom-dns-web-site-buydomains-web-app.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="5f156-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="5f156-109">tooassociate su dominio personalizado con una aplicación web en el servicio de aplicación de Azure, debe agregar una nueva entrada en la tabla de hello DNS para su dominio personalizado mediante el uso de herramientas proporcionadas por el registrador de dominios de Hola que adquirió su nombre de dominio de.</span><span class="sxs-lookup"><span data-stu-id="5f156-109">tooassociate your custom domain with a web app in Azure App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by hello domain registrar that you purchased your domain name from.</span></span> <span data-ttu-id="5f156-110">Utilice Hola siguiendo los pasos toolocate y herramientas DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="5f156-110">Use hello following steps toolocate and use hello DNS tools.</span></span>

1. <span data-ttu-id="5f156-111">Inicie sesión en la cuenta de tooyour en el registrador de dominios y busque una página para administrar los registros DNS.</span><span class="sxs-lookup"><span data-stu-id="5f156-111">Sign in tooyour account at your domain registrar, and look for a page for managing DNS records.</span></span> <span data-ttu-id="5f156-112">Busque los vínculos correspondientes o áreas del sitio de hello etiquetada como **nombre de dominio**, **DNS**, o **gestión de nombre de servidor**.</span><span class="sxs-lookup"><span data-stu-id="5f156-112">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="5f156-113">A menudo un vínculo de página toothis puede encontrarse puede ver la información de cuenta y, a continuación, busca un vínculo como **Mis dominios**.</span><span class="sxs-lookup"><span data-stu-id="5f156-113">Often a link toothis page can be found be viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="5f156-114">Una vez haya encontrado la página de administración de hello para el nombre de dominio, busque un vínculo que permite los registros DNS de hello tooedit.</span><span class="sxs-lookup"><span data-stu-id="5f156-114">Once you have found hello management page for your domain name, look for a link that allows you tooedit hello DNS records.</span></span> <span data-ttu-id="5f156-115">Debe aparecer como **archivo Zona**, **Registros DNS** o como un vínculo de configuración de **Opciones avanzadas**.</span><span class="sxs-lookup"><span data-stu-id="5f156-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span></span>
   
   * <span data-ttu-id="5f156-116">página de Hello probablemente tendrá unos registros ya creados, por ejemplo, una asociación de entrada '**@**'o'\*' con una página 'estacionamiento de dominio'.</span><span class="sxs-lookup"><span data-stu-id="5f156-116">hello page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span></span> <span data-ttu-id="5f156-117">Es posible también que contenga registros para los subdominios más comunes, como **www**.</span><span class="sxs-lookup"><span data-stu-id="5f156-117">It may also contain records for common sub-domains such as **www**.</span></span>
   * <span data-ttu-id="5f156-118">página de Hola se menciona **registros CNAME**, o proporcionar un tooselect de la lista desplegable un tipo de registro.</span><span class="sxs-lookup"><span data-stu-id="5f156-118">hello page will mention **CNAME records**, or provide a drop-down tooselect a record type.</span></span> <span data-ttu-id="5f156-119">También es posible que mencione otros registros, como los **registros A** y los **registros MX**.</span><span class="sxs-lookup"><span data-stu-id="5f156-119">It may also mention other records such as **A records** and **MX records**.</span></span> <span data-ttu-id="5f156-120">En algunos casos, los registros CNAME tendrán otros nombres, como **Registro de Alias**.</span><span class="sxs-lookup"><span data-stu-id="5f156-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span></span>
   * <span data-ttu-id="5f156-121">página de Hello también tendrá los campos que permiten demasiado**mapa** desde una **nombre de Host** o **nombre de dominio** tooanother nombre de dominio.</span><span class="sxs-lookup"><span data-stu-id="5f156-121">hello page will also have fields that allow you too**map** from a **Host name** or **Domain name** tooanother domain name.</span></span>
3. <span data-ttu-id="5f156-122">Aunque los detalles de Hola de cada registrador varían, por lo general se asigna *de* nombre de dominio personalizado (como **contoso.com**,) *a* nombre de dominio de Traffic Manager de hello (**contoso.trafficmanager.net**) que se utiliza para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="5f156-122">While hello specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* hello Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5f156-123">O bien, si un registro ya está en uso y necesita toopreemptively enlazar su tooit de aplicaciones, puede crear un registro CNAME adicional.</span><span class="sxs-lookup"><span data-stu-id="5f156-123">Alternatively, if a record is already in use and you need toopreemptively bind your apps tooit, you can create an additional CNAME record.</span></span> <span data-ttu-id="5f156-124">Por ejemplo, enlace de toopreemptively **www.contoso.com** tooyour web app, cree un registro CNAME de **awverify.www** demasiado**contoso.trafficmanager.net**.</span><span class="sxs-lookup"><span data-stu-id="5f156-124">For example, toopreemptively bind **www.contoso.com** tooyour web app, create a CNAME record from **awverify.www** too**contoso.trafficmanager.net**.</span></span> <span data-ttu-id="5f156-125">A continuación, puede agregar tooyour "www.contoso.com" aplicación Web sin cambiar el registro CNAME de Hola "www".</span><span class="sxs-lookup"><span data-stu-id="5f156-125">You can then add "www.contoso.com" tooyour Web App without changing hello "www" CNAME record.</span></span> <span data-ttu-id="5f156-126">Para más información, consulte [Creación de registros DNS para una aplicación web en un dominio personalizado][CREATEDNS].</span><span class="sxs-lookup"><span data-stu-id="5f156-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
   > 
   > 
4. <span data-ttu-id="5f156-127">Cuando haya terminado de agregar o modificar los registros DNS en el registrador, guardar los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="5f156-127">Once you have finished adding or modifying DNS records at your registrar, save hello changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="5f156-128">Habilitación del Administrador de tráfico</span><span class="sxs-lookup"><span data-stu-id="5f156-128">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="5f156-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5f156-129">Next steps</span></span>
<span data-ttu-id="5f156-130">Para obtener más información, vea hello [Centro para desarrolladores de Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="5f156-130">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
