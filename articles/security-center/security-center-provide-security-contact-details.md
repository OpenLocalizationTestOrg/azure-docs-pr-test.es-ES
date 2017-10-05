---
title: "Provisión de detalles de contacto de seguridad en Azure Security Center | Microsoft Docs"
description: "En este documento se muestra cómo proporcionar detalles de contacto de seguridad en Azure Security Center."
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
ms.openlocfilehash: 1a6e5e915745dd3588fbc54b353daa947b1c4289
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a><span data-ttu-id="9d103-103">Proporcionar detalles de contacto de seguridad en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="9d103-103">Provide security contact details in Azure Security Center</span></span>
<span data-ttu-id="9d103-104">Azure Security Center recomendará que proporcione los detalles de contacto de seguridad para su suscripción de Azure si no lo ha hecho ya.</span><span class="sxs-lookup"><span data-stu-id="9d103-104">Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already.</span></span> <span data-ttu-id="9d103-105">Esta información la utilizará Microsoft para ponerse en contacto con usted si Microsoft Security Response Center (MSRC) detecta que un tercero no autorizado o ilegal ha accedido a los datos de clientes.</span><span class="sxs-lookup"><span data-stu-id="9d103-105">This information will be used by Microsoft to contact you if the Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party.</span></span> <span data-ttu-id="9d103-106">MSRC lleva a cabo una selecta supervisión de seguridad de la red e infraestructura de Azure y recibe información sobre amenazas y quejas sobre abusos de terceros.</span><span class="sxs-lookup"><span data-stu-id="9d103-106">MSRC performs select security monitoring of the Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.</span></span>

<span data-ttu-id="9d103-107">Se envía una notificación de correo electrónico en la primera repetición diaria de una alerta y solo en aquellas con un nivel de gravedad elevado.</span><span class="sxs-lookup"><span data-stu-id="9d103-107">An email notification is sent on the first daily occurrence of an alert and only for high severity alerts.</span></span> <span data-ttu-id="9d103-108">Las preferencias de correo electrónico solo pueden configurarse para las directivas de suscripción.</span><span class="sxs-lookup"><span data-stu-id="9d103-108">Email preferences can only be configured for subscription policies.</span></span> <span data-ttu-id="9d103-109">Los grupos de recursos de una suscripción heredan esta configuración.</span><span class="sxs-lookup"><span data-stu-id="9d103-109">Resource groups within a subscription will inherit these settings.</span></span>

> [!NOTE]
> <span data-ttu-id="9d103-110">En este documento se presenta el servicio mediante una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9d103-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="9d103-111">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="9d103-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="9d103-112">Implementación de la recomendación</span><span class="sxs-lookup"><span data-stu-id="9d103-112">Implement the recommendation</span></span>
1. <span data-ttu-id="9d103-113">En la hoja **Recomendaciones**, seleccione **Proporcionar detalles de contacto de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="9d103-113">In the **Recommendations** blade, select **Provide security contact details**.</span></span>
   <span data-ttu-id="9d103-114">![Proporcionar contacto de seguridad][1]</span><span class="sxs-lookup"><span data-stu-id="9d103-114">![Provide security contact][1]</span></span>
2. <span data-ttu-id="9d103-115">Se abre la hoja **Proporcionar detalles de contacto de seguridad**.</span><span class="sxs-lookup"><span data-stu-id="9d103-115">This opens the blade **Provide security contact details**.</span></span> <span data-ttu-id="9d103-116">Seleccione la suscripción de Azure sobre la que desea proporcionar información de contacto.</span><span class="sxs-lookup"><span data-stu-id="9d103-116">Select the Azure subscription to provide contact information on.</span></span>
   <span data-ttu-id="9d103-117">![Proporcionar detalles de contacto de seguridad][2]</span><span class="sxs-lookup"><span data-stu-id="9d103-117">![Provide security contact details][2]</span></span>
3. <span data-ttu-id="9d103-118">Se abre una segunda hoja **Proporcionar datos de los contactos de seguridad** .</span><span class="sxs-lookup"><span data-stu-id="9d103-118">A second **Provide security contact details** blade opens.</span></span>

   * <span data-ttu-id="9d103-119">Escriba la dirección de correo electrónico del contacto de seguridad o direcciones separadas por comas.</span><span class="sxs-lookup"><span data-stu-id="9d103-119">Enter the security contact email address or addresses separated by commas.</span></span> <span data-ttu-id="9d103-120">No hay un límite en el número de direcciones de correo electrónico que se pueden escribir.</span><span class="sxs-lookup"><span data-stu-id="9d103-120">There is not a limit to the number of email addresses that you can enter.</span></span>
   * <span data-ttu-id="9d103-121">Escriba un número de teléfono internacional de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9d103-121">Enter one security contact international phone number.</span></span>
   * <span data-ttu-id="9d103-122">Para recibir correos electrónicos de alertas de gravedad alta, active la opción **Send me emails about alert**(Enviar correos electrónicos de alertas).</span><span class="sxs-lookup"><span data-stu-id="9d103-122">To receive emails about high severity alerts, turn on the option **Send me emails about alerts**.</span></span>
   * <span data-ttu-id="9d103-123">Más adelante, tendrá la opción de enviar notificaciones por correo electrónico a los propietarios de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="9d103-123">In the future, you will have the option to send email notifications to subscription owners.</span></span> <span data-ttu-id="9d103-124">De momento, esta opción aparece atenuada.</span><span class="sxs-lookup"><span data-stu-id="9d103-124">This option is currently grayed out.</span></span>
   * <span data-ttu-id="9d103-125">Seleccione **Aceptar** para aplicar la información de contacto de seguridad a su suscripción.</span><span class="sxs-lookup"><span data-stu-id="9d103-125">Select **OK** to apply the security contact information to your subscription.</span></span>

## <a name="see-also"></a><span data-ttu-id="9d103-126">Consulte también</span><span class="sxs-lookup"><span data-stu-id="9d103-126">See also</span></span>
<span data-ttu-id="9d103-127">Para más información sobre el Centro de seguridad, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="9d103-127">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="9d103-128">[Establecimiento de directivas de seguridad en Azure Security Center](security-center-policies.md): aprenda a configurar directivas de seguridad para las suscripciones y los grupos de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d103-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="9d103-129">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d103-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="9d103-130">[Supervisión del estado de seguridad en Azure Security Center](security-center-monitoring.md): obtenga información sobre cómo supervisar el mantenimiento de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d103-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="9d103-131">[Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md): obtenga información sobre cómo administrar y responder a alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="9d103-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="9d103-132">[Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md): aprenda a supervisar el estado de mantenimiento de las soluciones de asociados.</span><span class="sxs-lookup"><span data-stu-id="9d103-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="9d103-133">[Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md): busque las preguntas más frecuentes sobre cómo usar el servicio.</span><span class="sxs-lookup"><span data-stu-id="9d103-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="9d103-134">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): obtenga las últimas noticias e información sobre la seguridad en Azure.</span><span class="sxs-lookup"><span data-stu-id="9d103-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
