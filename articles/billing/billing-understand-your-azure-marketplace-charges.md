---
title: "Descripción de los gastos de servicios externos de Azure | Microsoft Docs"
description: "Obtenga información sobre la facturación de los servicios externos, anteriormente conocidos como Marketplace, en Azure."
services: 
documentationcenter: 
author: adpick
manager: tonguyen
editor: 
tags: billing
ms.assetid: 5e0e2a3c-d111-4054-8508-0c111c1b749b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: adpick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 11701ce0162113ef6c8e056d3a30fe1d8f702f92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="864a0-103">Descripción de la facturación de Azure para gastos de servicios externos</span><span class="sxs-lookup"><span data-stu-id="864a0-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="864a0-104">Los servicios externos se solían llamar Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="864a0-104">External services used to be called Azure Marketplace.</span></span> <span data-ttu-id="864a0-105">Por lo general, son servicios publicados por parte de terceros que están disponibles para Azure, pero están completamente integrados en Azure.</span><span class="sxs-lookup"><span data-stu-id="864a0-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="864a0-106">Por ejemplo, ClearDB y SendGrid son servicios externos que puede adquirir en Azure, pero que no están publicados por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="864a0-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="864a0-107">Cuando aprovisiona un nuevo servicio externo o un recurso, aparece una advertencia:</span><span class="sxs-lookup"><span data-stu-id="864a0-107">When you provision a new external service or resource, a warning is shown:</span></span>

![Advertencia de compra de Marketplace](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="864a0-109">Los servicios externos los publican empresas distintas a Microsoft pero, a veces, los productos de Microsoft también se pueden clasificar como servicios externos.</span><span class="sxs-lookup"><span data-stu-id="864a0-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="864a0-110">Cómo se facturan los servicios externos</span><span class="sxs-lookup"><span data-stu-id="864a0-110">How external services are billed</span></span>
- <span data-ttu-id="864a0-111">Los servicios externos se facturan por separado.</span><span class="sxs-lookup"><span data-stu-id="864a0-111">External services are billed separately.</span></span> <span data-ttu-id="864a0-112">Los servicios externos se tratan como pedidos individuales dentro de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="864a0-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="864a0-113">El período de facturación para cada servicio se establece al adquirir el servicio.</span><span class="sxs-lookup"><span data-stu-id="864a0-113">The billing period for each service is set when you purchase the service.</span></span> <span data-ttu-id="864a0-114">No debe confundirse con el período de facturación de la suscripción en la que lo adquirió.</span><span class="sxs-lookup"><span data-stu-id="864a0-114">Not to be confused with the billing period of the subscription under which you purchased it.</span></span> <span data-ttu-id="864a0-115">Además, recibirá facturas independientes y se le cobrará en su tarjeta de crédito por separado.</span><span class="sxs-lookup"><span data-stu-id="864a0-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="864a0-116">Cada servicio externo tiene un modelo de facturación diferente.</span><span class="sxs-lookup"><span data-stu-id="864a0-116">Each external service has a different billing model.</span></span> <span data-ttu-id="864a0-117">Algunos servicios se facturan mediante la modalidad de pago por uso, mientras que otros utilizan un modelo basado en el pago mensual.</span><span class="sxs-lookup"><span data-stu-id="864a0-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="864a0-118">Necesitará una tarjeta de crédito para los servicios externos de Azure ya que no se pueden comprar servicios externos mediante el pago de factura.</span><span class="sxs-lookup"><span data-stu-id="864a0-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="864a0-119">No puede usar créditos mensuales gratuitos para los servicios externos.</span><span class="sxs-lookup"><span data-stu-id="864a0-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="864a0-120">Si usa una suscripción de Azure que incluye [créditos gratuitos](https://azure.microsoft.com/pricing/spending-limits/), estos no se podrán aplicar a las facturas de los servicios externos.</span><span class="sxs-lookup"><span data-stu-id="864a0-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied to external service bills.</span></span> <span data-ttu-id="864a0-121">Utilice una tarjeta de crédito para adquirir servicios externos.</span><span class="sxs-lookup"><span data-stu-id="864a0-121">Use a credit card to purchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-the-azure-portal"></a><span data-ttu-id="864a0-122">Visualización de los gastos y el historial de servicios externos en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="864a0-122">View external service spending and history in the Azure portal</span></span>
<span data-ttu-id="864a0-123">Puede ver una lista de los servicios externos que están en cada suscripción dentro de [Azure Portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="864a0-123">You can view a list of the external services that are on each subscription within the [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="864a0-124">Inicie sesión en [Azure Portal](https://portal.azure.com/) como administrador de cuenta.</span><span class="sxs-lookup"><span data-stu-id="864a0-124">Sign in to the [Azure portal](https://portal.azure.com/) as the account administrator.</span></span>
2. <span data-ttu-id="864a0-125">En el menú de concentrador, seleccione **Suscripción**.</span><span class="sxs-lookup"><span data-stu-id="864a0-125">In the Hub menu, select **Subscriptions**.</span></span>
   
    ![En el menú de concentrador, seleccione Suscripción.](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="864a0-127">En la hoja **Suscripciones**, seleccione la suscripción que desea ver y, a continuación, seleccione **Servicios externos**.</span><span class="sxs-lookup"><span data-stu-id="864a0-127">In the **Subscriptions** blade, select the subscription that you want to view, and then select **External services**.</span></span>
   
    ![Seleccione una suscripción en la hoja de facturación](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="864a0-129">Debería ver cada uno de los pedidos de servicios externos, el nombre del publicador, el nivel de servicio que haya comprado, el nombre que ha asignado al recurso y el estado actual del pedido.</span><span class="sxs-lookup"><span data-stu-id="864a0-129">You should see each of your external service orders, the publisher name, service tier you bought, name you gave the resource, and the current order status.</span></span> <span data-ttu-id="864a0-130">Seleccione un servicio externo para ver las facturas anteriores.</span><span class="sxs-lookup"><span data-stu-id="864a0-130">To see past bills, select an external service.</span></span>
   
    ![Seleccionar un servicio externo](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="864a0-132">Desde aquí, puede consultar los importes de facturas pasadas con el desglose de impuestos incluido.</span><span class="sxs-lookup"><span data-stu-id="864a0-132">From here, you can view past bill amounts including the tax breakdown.</span></span>
   
    ![Ver historial de facturación de los servicios externos](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="864a0-134">Visualización de los gastos de los servicios externos para los clientes de Contrato Enterprise (EA)</span><span class="sxs-lookup"><span data-stu-id="864a0-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="864a0-135">Los clientes de EA pueden ver los gastos de los servicios externos y descargar los informes en el portal de EA.</span><span class="sxs-lookup"><span data-stu-id="864a0-135">EA customers can see external service spending and download reports in the EA portal.</span></span> <span data-ttu-id="864a0-136">Lea el artículo sobre [Azure Marketplace para clientes de EA](https://ea.azure.com/helpdocs/azureMarketplace) para empezar a trabajar.</span><span class="sxs-lookup"><span data-stu-id="864a0-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) to get started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="864a0-137">Administración de los métodos de pago para pedidos de servicios externos</span><span class="sxs-lookup"><span data-stu-id="864a0-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="864a0-138">Actualice los métodos de pago para los pedidos de servicios externos en el [Centro de cuentas](https://account.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="864a0-138">Update your payment methods for external service orders from the [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="864a0-139">Si adquirió la suscripción con una cuenta profesional o educativa, debería [ponerse en contacto con el servicio de asistencia técnica](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para realizar cambios en el método de pago.</span><span class="sxs-lookup"><span data-stu-id="864a0-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to make changes to your payment method.</span></span>
> 
> 

1. <span data-ttu-id="864a0-140">Inicie sesión en el [Centro de cuentas](https://account.windowsazure.com/) y [vaya a la pestaña **Marketplace**](https://account.windowsazure.com/Store)</span><span class="sxs-lookup"><span data-stu-id="864a0-140">Sign in to the [Account Center](https://account.windowsazure.com/) and [navigate to the **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![Seleccione Marketplace en el Centro de cuentas](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="864a0-142">Seleccione el servicio externo que desea administrar</span><span class="sxs-lookup"><span data-stu-id="864a0-142">Select the external service you want to manage</span></span>
   
    ![Seleccione el servicio externo que desea administrar](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="864a0-144">En el lado derecho de la página, haga clic en **Cambiar método de pago**.</span><span class="sxs-lookup"><span data-stu-id="864a0-144">Click **Change payment method** on the right side of the page.</span></span> <span data-ttu-id="864a0-145">Este vínculo le permite acceder a un portal diferente para administrar la forma de pago.</span><span class="sxs-lookup"><span data-stu-id="864a0-145">This link brings you to a different portal to manage your payment method.</span></span>
   
    ![Resumen del pedido](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="864a0-147">Haga clic en **Editar información** y siga las instrucciones para actualizar su información de pago.</span><span class="sxs-lookup"><span data-stu-id="864a0-147">Click **Edit info** and follow instructions to update your payment information.</span></span>
   
    ![Seleccione Editar información](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="864a0-149">Cancelación de un pedido de servicio externo</span><span class="sxs-lookup"><span data-stu-id="864a0-149">Cancel an external service order</span></span>
<span data-ttu-id="864a0-150">Si desea cancelar el pedido de servicio externo, debe eliminar el recurso en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="864a0-150">If you want to cancel your external service order, delete the resource in the [Azure portal](https://portal.azure.com).</span></span>

![Eliminar recurso](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="864a0-152">¿Necesita ayuda?</span><span class="sxs-lookup"><span data-stu-id="864a0-152">Need help?</span></span> <span data-ttu-id="864a0-153">Póngase en contacto con el servicio de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="864a0-153">Contact support.</span></span>
<span data-ttu-id="864a0-154">Si tiene más preguntas, [póngase en contacto con el servicio de soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para resolver el problema rápidamente.</span><span class="sxs-lookup"><span data-stu-id="864a0-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>

