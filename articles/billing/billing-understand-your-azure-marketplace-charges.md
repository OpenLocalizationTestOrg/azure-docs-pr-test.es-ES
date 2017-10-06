---
title: aaaUnderstand los cargos de servicio externos Azure | Documentos de Microsoft
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
ms.openlocfilehash: 1d2cb28319e2ab4eff753177220993cbf94c96ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="41581-103">Descripción de la facturación de Azure para gastos de servicios externos</span><span class="sxs-lookup"><span data-stu-id="41581-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="41581-104">Servicios externos utilizan toobe llamado Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="41581-104">External services used toobe called Azure Marketplace.</span></span> <span data-ttu-id="41581-105">Por lo general, son servicios publicados por parte de terceros que están disponibles para Azure, pero están completamente integrados en Azure.</span><span class="sxs-lookup"><span data-stu-id="41581-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="41581-106">Por ejemplo, ClearDB y SendGrid son servicios externos que puede adquirir en Azure, pero que no están publicados por Microsoft.</span><span class="sxs-lookup"><span data-stu-id="41581-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="41581-107">Cuando aprovisiona un nuevo servicio externo o un recurso, aparece una advertencia:</span><span class="sxs-lookup"><span data-stu-id="41581-107">When you provision a new external service or resource, a warning is shown:</span></span>

![Advertencia de compra de Marketplace](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="41581-109">Los servicios externos los publican empresas distintas a Microsoft pero, a veces, los productos de Microsoft también se pueden clasificar como servicios externos.</span><span class="sxs-lookup"><span data-stu-id="41581-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="41581-110">Cómo se facturan los servicios externos</span><span class="sxs-lookup"><span data-stu-id="41581-110">How external services are billed</span></span>
- <span data-ttu-id="41581-111">Los servicios externos se facturan por separado.</span><span class="sxs-lookup"><span data-stu-id="41581-111">External services are billed separately.</span></span> <span data-ttu-id="41581-112">Los servicios externos se tratan como pedidos individuales dentro de la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="41581-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="41581-113">período de facturación de Hola para cada servicio se establece al adquirir un servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="41581-113">hello billing period for each service is set when you purchase hello service.</span></span> <span data-ttu-id="41581-114">No toobe confundirse con el período de facturación de Hola de suscripción de hello en el que lo adquirió.</span><span class="sxs-lookup"><span data-stu-id="41581-114">Not toobe confused with hello billing period of hello subscription under which you purchased it.</span></span> <span data-ttu-id="41581-115">Además, recibirá facturas independientes y se le cobrará en su tarjeta de crédito por separado.</span><span class="sxs-lookup"><span data-stu-id="41581-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="41581-116">Cada servicio externo tiene un modelo de facturación diferente.</span><span class="sxs-lookup"><span data-stu-id="41581-116">Each external service has a different billing model.</span></span> <span data-ttu-id="41581-117">Algunos servicios se facturan mediante la modalidad de pago por uso, mientras que otros utilizan un modelo basado en el pago mensual.</span><span class="sxs-lookup"><span data-stu-id="41581-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="41581-118">Necesitará una tarjeta de crédito para los servicios externos de Azure ya que no se pueden comprar servicios externos mediante el pago de factura.</span><span class="sxs-lookup"><span data-stu-id="41581-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="41581-119">No puede usar créditos mensuales gratuitos para los servicios externos.</span><span class="sxs-lookup"><span data-stu-id="41581-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="41581-120">Si usa una suscripción de Azure que incluye [libre créditos](https://azure.microsoft.com/pricing/spending-limits/), no pueden ser facturas de servicio tooexternal aplicada.</span><span class="sxs-lookup"><span data-stu-id="41581-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied tooexternal service bills.</span></span> <span data-ttu-id="41581-121">Usar una tarjeta de crédito toopurchase los servicios externos.</span><span class="sxs-lookup"><span data-stu-id="41581-121">Use a credit card toopurchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-hello-azure-portal"></a><span data-ttu-id="41581-122">Gastos de servicio externo de vista y el historial en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="41581-122">View external service spending and history in hello Azure portal</span></span>
<span data-ttu-id="41581-123">Puede ver una lista de servicios externos de Hola que se encuentran en cada suscripción hello [portal de Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="41581-123">You can view a list of hello external services that are on each subscription within hello [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="41581-124">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) como administrador de la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="41581-124">Sign in toohello [Azure portal](https://portal.azure.com/) as hello account administrator.</span></span>
2. <span data-ttu-id="41581-125">En el menú del concentrador hello, seleccione **suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="41581-125">In hello Hub menu, select **Subscriptions**.</span></span>
   
    ![Seleccione las suscripciones en el menú del concentrador de Hola](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="41581-127">Hola **suscripciones** hoja, suscripción de hello select que desee tooview y, a continuación, seleccione **servicios externos**.</span><span class="sxs-lookup"><span data-stu-id="41581-127">In hello **Subscriptions** blade, select hello subscription that you want tooview, and then select **External services**.</span></span>
   
    ![Seleccione una suscripción en la hoja facturación Hola](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="41581-129">Debería ver cada uno de los pedidos de servicio externo, el nombre del publicador de hello, que compró el nivel de servicio, nombre que asignó recursos hello y estado actual de la orden de Hola.</span><span class="sxs-lookup"><span data-stu-id="41581-129">You should see each of your external service orders, hello publisher name, service tier you bought, name you gave hello resource, and hello current order status.</span></span> <span data-ttu-id="41581-130">toosee más allá de las facturas, seleccione un servicio externo.</span><span class="sxs-lookup"><span data-stu-id="41581-130">toosee past bills, select an external service.</span></span>
   
    ![Seleccionar un servicio externo](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="41581-132">Desde aquí, puede ver más allá de los importes de factura incluidos desglose de impuestos Hola.</span><span class="sxs-lookup"><span data-stu-id="41581-132">From here, you can view past bill amounts including hello tax breakdown.</span></span>
   
    ![Ver historial de facturación de los servicios externos](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="41581-134">Visualización de los gastos de los servicios externos para los clientes de Contrato Enterprise (EA)</span><span class="sxs-lookup"><span data-stu-id="41581-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="41581-135">Los clientes EA pueden ver gastos de servicio externo y descargar informes del portal EA Hola.</span><span class="sxs-lookup"><span data-stu-id="41581-135">EA customers can see external service spending and download reports in hello EA portal.</span></span> <span data-ttu-id="41581-136">Vea [Azure Marketplace para clientes EA](https://ea.azure.com/helpdocs/azureMarketplace) tooget iniciado.</span><span class="sxs-lookup"><span data-stu-id="41581-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) tooget started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="41581-137">Administración de los métodos de pago para pedidos de servicios externos</span><span class="sxs-lookup"><span data-stu-id="41581-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="41581-138">Actualizar los métodos de pago para los pedidos de servicio externo de hello [centro de cuentas de](https://account.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="41581-138">Update your payment methods for external service orders from hello [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="41581-139">Si adquirió la suscripción con una cuenta de empresa o centro educativo, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake cambia el método de pago tooyour.</span><span class="sxs-lookup"><span data-stu-id="41581-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toomake changes tooyour payment method.</span></span>
> 
> 

1. <span data-ttu-id="41581-140">Inicie sesión en toohello [centro de cuentas de](https://account.windowsazure.com/) y [navegue toohello **marketplace** ficha](https://account.windowsazure.com/Store)</span><span class="sxs-lookup"><span data-stu-id="41581-140">Sign in toohello [Account Center](https://account.windowsazure.com/) and [navigate toohello **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![Seleccione marketplace en Centro de cuentas de Hola](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="41581-142">Seleccione servicio externo de Hola que desee toomanage</span><span class="sxs-lookup"><span data-stu-id="41581-142">Select hello external service you want toomanage</span></span>
   
    ![Seleccione servicio externo de Hola que desee toomanage](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="41581-144">Haga clic en **Cambiar método de pago** en hello derecha de la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="41581-144">Click **Change payment method** on hello right side of hello page.</span></span> <span data-ttu-id="41581-145">Este vínculo abre tooa diferentes portal toomanage su método de pago.</span><span class="sxs-lookup"><span data-stu-id="41581-145">This link brings you tooa different portal toomanage your payment method.</span></span>
   
    ![Resumen del pedido](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="41581-147">Haga clic en **editar la información** y siga las instrucciones tooupdate su información de pago.</span><span class="sxs-lookup"><span data-stu-id="41581-147">Click **Edit info** and follow instructions tooupdate your payment information.</span></span>
   
    ![Seleccione Editar información](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="41581-149">Cancelación de un pedido de servicio externo</span><span class="sxs-lookup"><span data-stu-id="41581-149">Cancel an external service order</span></span>
<span data-ttu-id="41581-150">Si desea toocancel su pedido de servicio externo, eliminar el recurso de Hola Hola [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="41581-150">If you want toocancel your external service order, delete hello resource in hello [Azure portal](https://portal.azure.com).</span></span>

![Eliminar recurso](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="41581-152">¿Necesita ayuda?</span><span class="sxs-lookup"><span data-stu-id="41581-152">Need help?</span></span> <span data-ttu-id="41581-153">Póngase en contacto con el servicio de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="41581-153">Contact support.</span></span>
<span data-ttu-id="41581-154">Si sigue teniendo preguntas, [póngase en contacto con soporte técnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget rápidamente para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="41581-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>

