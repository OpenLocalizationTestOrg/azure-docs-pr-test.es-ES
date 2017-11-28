---
title: detalles de contacto de seguridad aaaProvide en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo seguridad tooprovide en contacto con los detalles en el centro de seguridad de Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 6c378c9c84c6e4fce70b2541e4cc121018700269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="24358-103">Proporcionar detalles de contacto de seguridad en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="24358-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="24358-104">Azure Security Center recomendará que proporcione los detalles de contacto de seguridad para su suscripción de Azure si no lo ha hecho ya.</span><span class="sxs-lookup"><span data-stu-id="24358-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="24358-105">Toocontact Microsoft usará esta información si Hola Microsoft Security Response Center (MSRC) detecta que una entidad ilegal o no autorizada ha obtenido acceso a los datos de clientes.</span><span class="sxs-lookup"><span data-stu-id="24358-105">This information will be used by Microsoft toocontact you if hello Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="24358-106">MSRC realiza una supervisión de infraestructura y de red de Azure Hola seleccione seguridad y recibe las quejas de inteligencia y controlar el abuso de amenaza de terceros.</span><span class="sxs-lookup"><span data-stu-id="24358-106">MSRC performs select security monitoring of hello Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="24358-107">Se envía una notificación de correo electrónico en hello primera diaria aparición de una alerta y solo las alertas de gravedad alta.</span><span class="sxs-lookup"><span data-stu-id="24358-107">An email notification is sent on hello first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="24358-108">Las preferencias de correo electrónico solo pueden configurarse para las directivas de suscripción.</span><span class="sxs-lookup"><span data-stu-id="24358-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="24358-109">Los grupos de recursos de una suscripción heredan esta configuración.</span><span class="sxs-lookup"><span data-stu-id="24358-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="24358-110">Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="24358-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="24358-111">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="24358-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="24358-112">Implementar la recomendación de Hola</span><span class="sxs-lookup"><span data-stu-id="24358-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="24358-113">Hola **recomendaciones** hoja, seleccione **proporcionar detalles de contacto de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="24358-113">In hello **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="24358-114">![Proporcionar contacto de seguridad][1]</span><span class="sxs-lookup"><span data-stu-id="24358-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="24358-115">Esto abre una hoja de hello **proporcionar detalles de contacto de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="24358-115">This opens hello blade **Provide security contact details**.</span></span> <span data-ttu-id="24358-116">Seleccione esta opción información de contacto tooprovide Hola suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="24358-116">Select hello Azure subscription tooprovide contact information on.</span></span>
   <span data-ttu-id="24358-117">![Proporcionar datos de los contactos de seguridad][2]</span><span class="sxs-lookup"><span data-stu-id="24358-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="24358-118">Se abre una segunda hoja **Proporcionar datos de los contactos de seguridad** .</span><span class="sxs-lookup"><span data-stu-id="24358-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="24358-119">Escriba la dirección de correo electrónico de contacto de seguridad de Hola o direcciones separadas por comas.</span><span class="sxs-lookup"><span data-stu-id="24358-119">Enter hello security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="24358-120">No es un toohello limitar el número de direcciones de correo electrónico que se pueden escribir.</span><span class="sxs-lookup"><span data-stu-id="24358-120">There is not a limit toohello number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="24358-121">Escriba un número de teléfono internacional de seguridad.</span><span class="sxs-lookup"><span data-stu-id="24358-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="24358-122">mensajes de correo electrónico tooreceive sobre alertas de gravedad alta, activar la opción hello **Enviarme correos electrónicos sobre alertas**.</span><span class="sxs-lookup"><span data-stu-id="24358-122">tooreceive emails about high severity alerts, turn on hello option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="24358-123">Hola futura, tendrá propietarios de toosubscription de notificaciones de correo electrónico de hello opción toosend.</span><span class="sxs-lookup"><span data-stu-id="24358-123">In hello future, you will have hello option toosend email notifications toosubscription owners.</span></span> <span data-ttu-id="24358-124">De momento, esta opción aparece atenuada.</span><span class="sxs-lookup"><span data-stu-id="24358-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="24358-125">Seleccione **Aceptar** seguridad de hello tooapply póngase en contacto con suscripción de tooyour de información.</span><span class="sxs-lookup"><span data-stu-id="24358-125">Select **OK** tooapply hello security contact information tooyour subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="24358-126">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="24358-126">See also</span></span>
<span data-ttu-id="24358-127">toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="24358-127">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="24358-128">[Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="24358-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="24358-129">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="24358-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="24358-130">[Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="24358-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="24358-131">[Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.</span><span class="sxs-lookup"><span data-stu-id="24358-131">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="24358-132">[Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="24358-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="24358-133">[Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="24358-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="24358-134">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : obtener información y noticias de seguridad de Azure más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="24358-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
