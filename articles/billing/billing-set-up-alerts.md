---
title: "Configuración de alertas de crédito o facturación para las suscripciones de Azure | Microsoft Docs"
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
ms.openlocfilehash: 7a1b579fdde831fdc3afa0a2aee4c24890216ed1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="b52a4-104">Configuración de alertas de crédito o facturación para las suscripciones de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b52a4-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="b52a4-105">Si es el administrador de cuenta de una suscripción a Azure, puede utilizar el servicio de alertas de facturación de Azure para crear alertas de facturación personalizadas que le ayudarán a supervisar y administrar la actividad de facturación de las cuentas de Azure.</span><span class="sxs-lookup"><span data-stu-id="b52a4-105">If you’re the Account Admin for an Azure subscription, you can use the Azure Billing Alert Service to create customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="b52a4-106">Este servicio está en versión preliminar, por lo que primero debe habilitarlo en la página Características de vista previa.</span><span class="sxs-lookup"><span data-stu-id="b52a4-106">This service is in preview, so you need to enable it in the Preview Features page first.</span></span>

## <a name="set-the-alert-threshold-and-email-recipients"></a><span data-ttu-id="b52a4-107">Establecimiento de los destinatarios de correo electrónico y del umbral de alerta</span><span class="sxs-lookup"><span data-stu-id="b52a4-107">Set the alert threshold and email recipients</span></span>
1. <span data-ttu-id="b52a4-108">Visite [la página Características de vista previa](https://account.windowsazure.com/PreviewFeatures) y habilite **Billing Alert Service** (Servicio de alertas de facturación).</span><span class="sxs-lookup"><span data-stu-id="b52a4-108">Visit [the Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="b52a4-109">Después de recibir la confirmación de correo electrónico de que el servicio de facturación está activado para su suscripción, visite [la página de suscripciones](https://account.windowsazure.com/Subscriptions) en el portal de cuentas.</span><span class="sxs-lookup"><span data-stu-id="b52a4-109">After you receive the email confirmation that the billing service is turned on for your subscription, visit [the Subscriptions page](https://account.windowsazure.com/Subscriptions) in the account portal.</span></span> <span data-ttu-id="b52a4-110">Haga clic en la suscripción que desea supervisar y después haga clic en **Alertas**.</span><span class="sxs-lookup"><span data-stu-id="b52a4-110">Click the subscription you want to monitor, and then click **Alerts**.</span></span>

    ![Captura de pantalla de la vista de suscripciones del Centro de cuentas de Azure, con las alertas resaltadas][Image1]

2. <span data-ttu-id="b52a4-112">Luego, haga clic en **Agregar alerta** para crear la primera alerta.</span><span class="sxs-lookup"><span data-stu-id="b52a4-112">Next, click **Add Alert** to create your first one.</span></span> <span data-ttu-id="b52a4-113">Puede configurar un total de cinco alertas de facturación por suscripción, con un umbral diferente y hasta dos destinatarios de correo electrónico para cada alerta.</span><span class="sxs-lookup"><span data-stu-id="b52a4-113">You can set up a total of five billing alerts per subscription, with a different threshold and up to two email recipients for each alert.</span></span>

    ![Captura de pantalla de la vista Alertas, donde puede agregar alertas][Image2]

3. <span data-ttu-id="b52a4-115">Cuando agregue una alerta, asígnele un nombre único, elija un umbral de gasto y elija las direcciones de correo electrónico a las que se enviarán las alertas.</span><span class="sxs-lookup"><span data-stu-id="b52a4-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose the email addresses where alerts are sent.</span></span> <span data-ttu-id="b52a4-116">Al configurar el umbral, podrá elegir un **Total de facturación** o un **Crédito monetario** desde la lista **Alerta** lista.</span><span class="sxs-lookup"><span data-stu-id="b52a4-116">When setting up the threshold, you can choose either a **Billing Total** or a **Monetary Credit** from the **Alert For** list.</span></span> <span data-ttu-id="b52a4-117">Para el total de facturación, se enviará una alerta cuando el gasto de la suscripción supere el umbral.</span><span class="sxs-lookup"><span data-stu-id="b52a4-117">For a billing total, an alert is sent when subscription spending exceeds the threshold.</span></span> <span data-ttu-id="b52a4-118">Para un crédito monetario, se enviará una alerta cuando los créditos monetarios caigan por debajo del límite.</span><span class="sxs-lookup"><span data-stu-id="b52a4-118">For a monetary credit, an alert is sent when monetary credits drop below the limit.</span></span> <span data-ttu-id="b52a4-119">Normalmente, los créditos monetarios se aplican a las suscripciones Evaluación gratuita y Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b52a4-119">Monetary credits usually apply to Free Trial and Visual Studio subscriptions.</span></span>

    ![Captura de pantalla de la vista de adición de alerta, donde puede configurar destinatarios][Image3]

<span data-ttu-id="b52a4-121">Azure admite cualquier dirección de correo electrónico pero no comprueba que la dirección de correo electrónico funcione. Por lo tanto, revise si hay errores ortográficos.</span><span class="sxs-lookup"><span data-stu-id="b52a4-121">Azure supports any email address but doesn't verify that the email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="b52a4-122">Comprobación de las alertas</span><span class="sxs-lookup"><span data-stu-id="b52a4-122">Check on your alerts</span></span>
<span data-ttu-id="b52a4-123">Después de configurar las alertas, el centro de cuentas enumera y muestra cuántas más se pueden configurar.</span><span class="sxs-lookup"><span data-stu-id="b52a4-123">After you set up alerts, the Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="b52a4-124">Para cada alerta, se mostrará la fecha y la hora de envío, si es una alerta de total de facturación o de crédito monetario, así como el límite configurado.</span><span class="sxs-lookup"><span data-stu-id="b52a4-124">For each alert, you see the date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and the limit you set up.</span></span> <span data-ttu-id="b52a4-125">El formato de fecha y hora es de 24 horas según el horario universal coordinado (UTC) y la fecha tiene el formato aaaa-mm-dd.</span><span class="sxs-lookup"><span data-stu-id="b52a4-125">The date and time format is 24-hour Universal Time Coordinate (UTC) and the date is yyyy-mm-dd format.</span></span> <span data-ttu-id="b52a4-126">Haga clic en el signo más de una alerta de la lista para modificarla o haga clic en la papelera para eliminarla.</span><span class="sxs-lookup"><span data-stu-id="b52a4-126">Click the plus sign for an alert in the list to edit it, or click the trash-can to delete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="b52a4-127">Alertas de facturación para los clientes del Contrato Enterprise (EA)</span><span class="sxs-lookup"><span data-stu-id="b52a4-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="b52a4-128">Los clientes EA pueden obtener alertas para cada departamento con una inscripción estableciendo cuotas de gastos.</span><span class="sxs-lookup"><span data-stu-id="b52a4-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="b52a4-129">Consulte [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) (Cuotas de gastos de departamento) en el portal EA para empezar a trabajar.</span><span class="sxs-lookup"><span data-stu-id="b52a4-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in the EA portal to get started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="b52a4-130">Más información sobre la administración de costos de Azure</span><span class="sxs-lookup"><span data-stu-id="b52a4-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="b52a4-131">Calcule los costos mediante la [calculadora de precios](https://azure.microsoft.com/pricing/calculator/), la [calculadora de costo total de propiedad](https://aka.ms/azure-tco-calculator) y cuando agregue un servicio.</span><span class="sxs-lookup"><span data-stu-id="b52a4-131">Estimate costs using the [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="b52a4-132">[Revise el uso y los costos con regularidad en Azure Portal](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="b52a4-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="b52a4-133">Active las [recomendaciones sobre el costo de Azure Advisor](../advisor/advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="b52a4-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="b52a4-134">Para obtener información, consulte [Introducción a la administración de costes y facturación de Azure](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="b52a4-134">To learn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
