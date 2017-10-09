---
title: "aaaSet las alertas de crédito o de facturación para las suscripciones de Azure | Documentos de Microsoft"
description: "Describe cómo puede configurar alertas en su factura de Azure para que pueda evitar sorpresas de facturación."
keywords: "alerta de crédito, alerta de facturación"
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 711b9c72c59874792b0e229cdc5ec0fa517c24c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="84b56-104">Configuración de alertas de crédito o facturación para las suscripciones de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="84b56-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="84b56-105">Si le hello Administrador de cuenta para una suscripción de Azure, puede usar hello Azure facturación servicio de alertas de facturación toocreate personalizado las alertas que le ayudan a supervisar y administrar la actividad de facturación para las cuentas de Azure.</span><span class="sxs-lookup"><span data-stu-id="84b56-105">If you’re hello Account Admin for an Azure subscription, you can use hello Azure Billing Alert Service toocreate customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="84b56-106">Este servicio está en vista previa, por lo que necesita tooenable, en la página de características de vista previa de hello en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="84b56-106">This service is in preview, so you need tooenable it in hello Preview Features page first.</span></span>

## <a name="set-hello-alert-threshold-and-email-recipients"></a><span data-ttu-id="84b56-107">Configurar destinatarios de umbral y el correo electrónico de alerta Hola</span><span class="sxs-lookup"><span data-stu-id="84b56-107">Set hello alert threshold and email recipients</span></span>
1. <span data-ttu-id="84b56-108">Visite [página de características de vista previa de hello](https://account.windowsazure.com/PreviewFeatures) y habilitar **servicio de alertas de facturación**.</span><span class="sxs-lookup"><span data-stu-id="84b56-108">Visit [hello Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="84b56-109">Después de recibir la confirmación por correo electrónico de Hola que está activado el servicio de facturación de Hola para su suscripción, visite [página de suscripciones de hello](https://account.windowsazure.com/Subscriptions) en portal de cuentas de Hola.</span><span class="sxs-lookup"><span data-stu-id="84b56-109">After you receive hello email confirmation that hello billing service is turned on for your subscription, visit [hello Subscriptions page](https://account.windowsazure.com/Subscriptions) in hello account portal.</span></span> <span data-ttu-id="84b56-110">Haga clic en hello suscripción que desee toomonitor y, a continuación, haga clic en **alertas**.</span><span class="sxs-lookup"><span data-stu-id="84b56-110">Click hello subscription you want toomonitor, and then click **Alerts**.</span></span>

    ![Captura de pantalla de vista de suscripciones de hello del centro de cuentas de Azure, con las alertas destacadas][Image1]

2. <span data-ttu-id="84b56-112">A continuación, haga clic en **Agregar alerta** toocreate primera vez.</span><span class="sxs-lookup"><span data-stu-id="84b56-112">Next, click **Add Alert** toocreate your first one.</span></span> <span data-ttu-id="84b56-113">Puede establecer un total de cinco alertas de facturación por suscripción, con un umbral diferente e instalación tootwo destinatarios de correo electrónico para cada alerta.</span><span class="sxs-lookup"><span data-stu-id="84b56-113">You can set up a total of five billing alerts per subscription, with a different threshold and up tootwo email recipients for each alert.</span></span>

    ![Vista de alertas de captura de pantalla de hello, donde puede agregar alerta][Image2]

3. <span data-ttu-id="84b56-115">Cuando se agrega una alerta, asígnele un nombre único, elija un umbral de gasto y elija Hola direcciones de correo electrónico donde se envían las alertas.</span><span class="sxs-lookup"><span data-stu-id="84b56-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose hello email addresses where alerts are sent.</span></span> <span data-ttu-id="84b56-116">Al configurar el umbral de hello, puede elegir un **Total de facturación** o un **un crédito monetario** de hello **alerta para** lista.</span><span class="sxs-lookup"><span data-stu-id="84b56-116">When setting up hello threshold, you can choose either a **Billing Total** or a **Monetary Credit** from hello **Alert For** list.</span></span> <span data-ttu-id="84b56-117">Para obtener un total de facturación, se envía una alerta cuando el gasto de la suscripción supera el umbral de Hola.</span><span class="sxs-lookup"><span data-stu-id="84b56-117">For a billing total, an alert is sent when subscription spending exceeds hello threshold.</span></span> <span data-ttu-id="84b56-118">Para un crédito monetario, se envía una alerta cuando los créditos monetarios caen por debajo del límite de Hola.</span><span class="sxs-lookup"><span data-stu-id="84b56-118">For a monetary credit, an alert is sent when monetary credits drop below hello limit.</span></span> <span data-ttu-id="84b56-119">Créditos monetarios normalmente son aplicables a las suscripciones de prueba y Visual Studio tooFree.</span><span class="sxs-lookup"><span data-stu-id="84b56-119">Monetary credits usually apply tooFree Trial and Visual Studio subscriptions.</span></span>

    ![Captura de pantalla de la vista de alerta suma hello, donde puede configurar los destinatarios][Image3]

<span data-ttu-id="84b56-121">Azure admite cualquier dirección de correo electrónico pero no comprobar que la dirección de correo electrónico de hello funcione, así que revise si hay errores ortográficos.</span><span class="sxs-lookup"><span data-stu-id="84b56-121">Azure supports any email address but doesn't verify that hello email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="84b56-122">Comprobación de las alertas</span><span class="sxs-lookup"><span data-stu-id="84b56-122">Check on your alerts</span></span>
<span data-ttu-id="84b56-123">Después de configurar las alertas, Hola centro de cuentas enumera y muestra cuántas más puede configurar.</span><span class="sxs-lookup"><span data-stu-id="84b56-123">After you set up alerts, hello Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="84b56-124">Para cada alerta, verá Hola límite de fecha y hora de envío, si se trata de una alerta para el Total de facturación o un crédito monetario y Hola que configurar.</span><span class="sxs-lookup"><span data-stu-id="84b56-124">For each alert, you see hello date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and hello limit you set up.</span></span> <span data-ttu-id="84b56-125">formato de fecha y hora de Hello es 24 horas horario Universal coordinado (UTC) y fecha de hello es el formato aaaa-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="84b56-125">hello date and time format is 24-hour Universal Time Coordinate (UTC) and hello date is yyyy-mm-dd format.</span></span> <span data-ttu-id="84b56-126">Haga clic en hello más firmarlo de una alerta en hello lista tooedit o haga clic en hello-Papelera toodelete lo.</span><span class="sxs-lookup"><span data-stu-id="84b56-126">Click hello plus sign for an alert in hello list tooedit it, or click hello trash-can toodelete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="84b56-127">Alertas de facturación para los clientes del Contrato Enterprise (EA)</span><span class="sxs-lookup"><span data-stu-id="84b56-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="84b56-128">Los clientes EA pueden obtener alertas para cada departamento con una inscripción estableciendo cuotas de gastos.</span><span class="sxs-lookup"><span data-stu-id="84b56-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="84b56-129">Vea [las cuotas de gastos de departamento](https://ea.azure.com/helpdocs/departmentSpendingQuotas) en hello EA portal tooget iniciado.</span><span class="sxs-lookup"><span data-stu-id="84b56-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in hello EA portal tooget started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="84b56-130">Más información sobre la administración de costos de Azure</span><span class="sxs-lookup"><span data-stu-id="84b56-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="84b56-131">Estimar los costos mediante hello [Calculadora de precios](https://azure.microsoft.com/pricing/calculator/), [costo total de calculadora de propiedad](https://aka.ms/azure-tco-calculator), y cuando se agrega un servicio.</span><span class="sxs-lookup"><span data-stu-id="84b56-131">Estimate costs using hello [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="84b56-132">[Revise el uso y los costos con regularidad en Azure Portal](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="84b56-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="84b56-133">Active las [recomendaciones sobre el costo de Azure Advisor](../advisor/advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="84b56-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="84b56-134">más información, consulte toolearn [instrucciones para la administración de Azure costo](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="84b56-134">toolearn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
