---
title: "Protección de la API con Azure API Management | Microsoft Docs"
description: "Aprenda a proteger su API con directivas de cuotas y limitaciones (limitación de frecuencia)."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 5553bcb8f9fd38630f694151dc644a684266387c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a><span data-ttu-id="3a749-103">Protección de su API con límites de frecuencia mediante Azure API Management</span><span class="sxs-lookup"><span data-stu-id="3a749-103">Protect your API with rate limits using Azure API Management</span></span>
<span data-ttu-id="3a749-104">Esta guía muestra lo fácil que es agregar protección para la API de back-end mediante la configuración de directivas de cuota y límite de frecuencia con Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="3a749-104">This guide shows you how easy it is to add protection for your backend API by configuring rate limit and quota policies with Azure API Management.</span></span>

<span data-ttu-id="3a749-105">En este tutorial, creará un producto de API de "evaluación gratuita" que permita a los desarrolladores realizar hasta 10 llamadas por minuto y hasta un máximo de 200 llamadas por semana a la API mediante las directivas [Limitar la frecuencia de llamadas por suscripción](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) y [Establecer la cuota de uso por suscripción](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota).</span><span class="sxs-lookup"><span data-stu-id="3a749-105">In this tutorial, you will create a "Free Trial" API product that allows developers to make up to 10 calls per minute and up to a maximum of 200 calls per week to your API using the [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="3a749-106">A continuación, publicará la API y probará la directiva de límite de frecuencia.</span><span class="sxs-lookup"><span data-stu-id="3a749-106">You will then publish the API and test the rate limit policy.</span></span>

<span data-ttu-id="3a749-107">Para más información sobre escenarios de limitación avanzados mediante las directivas [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) y [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey), consulte [Limitación avanzada de solicitudes con Azure API Management](api-management-sample-flexible-throttling.md).</span><span class="sxs-lookup"><span data-stu-id="3a749-107">For more advanced throttling scenarios using the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies, see [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md).</span></span>

## <span data-ttu-id="3a749-108"><a name="create-product"> </a>Para crear un producto</span><span class="sxs-lookup"><span data-stu-id="3a749-108"><a name="create-product"> </a>To create a product</span></span>
<span data-ttu-id="3a749-109">En este paso, creará un producto de evaluación gratuita que no requiere aprobación de suscripción.</span><span class="sxs-lookup"><span data-stu-id="3a749-109">In this step, you will create a Free Trial product that does not require subscription approval.</span></span>

> [!NOTE]
> <span data-ttu-id="3a749-110">Si ya tiene un producto configurado y desea usarlo para este tutorial, puede pasar la sección [Configurar directivas de cuota y límite de frecuencia][Configure call rate limit and quota policies] y seguir el tutorial a partir de ahí con su producto en lugar de con el producto de evaluación gratuita.</span><span class="sxs-lookup"><span data-stu-id="3a749-110">If you already have a product configured and want to use it for this tutorial, you can jump ahead to [Configure call rate limit and quota policies][Configure call rate limit and quota policies] and follow the tutorial from there using your product in place of the Free Trial product.</span></span>
> 
> 

<span data-ttu-id="3a749-111">Para comenzar, haga clic en **Portal para editores** en Azure Portal para el servicio API Management.</span><span class="sxs-lookup"><span data-stu-id="3a749-111">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portal del publicador][api-management-management-console]

> <span data-ttu-id="3a749-113">Si aún no ha creado ninguna instancia del servicio de API Management, consulte [Creación de una instancia del servicio API Management][Create an API Management service instance] en el tutorial [Administración de su primera API en Azure API Management][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="3a749-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Manage your first API in Azure API Management][Manage your first API in Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="3a749-114">Haga clic en **Productos** en el menú **API Management** a la izquierda para mostrar la página **Productos**.</span><span class="sxs-lookup"><span data-stu-id="3a749-114">Click **Products** in the **API Management** menu on the left to display the **Products** page.</span></span>

![Add product][api-management-add-product]

<span data-ttu-id="3a749-116">Haga clic en **Agregar producto** para mostrar el cuadro de diálogo **Agregar nuevo producto**.</span><span class="sxs-lookup"><span data-stu-id="3a749-116">Click **Add product** to display the **Add new product** dialog box.</span></span>

![Agregar nuevo producto][api-management-new-product-window]

<span data-ttu-id="3a749-118">En el cuadro **Título** escriba **Evaluación gratuita**.</span><span class="sxs-lookup"><span data-stu-id="3a749-118">In the **Title** box, type **Free Trial**.</span></span>

<span data-ttu-id="3a749-119">En el cuadro **Descripción**, escriba **Los suscriptores podrán realizar 10 llamadas/minuto hasta un máximo de 200 llamadas/semana; después, el acceso se denegará.**</span><span class="sxs-lookup"><span data-stu-id="3a749-119">In the **Description** box, type the following text: **Subscribers will be able to run 10 calls/minute up to a maximum of 200 calls/week after which access is denied.**</span></span>

<span data-ttu-id="3a749-120">Los productos de API Management pueden estar abiertos o protegidos.</span><span class="sxs-lookup"><span data-stu-id="3a749-120">Products in API Management can be protected or open.</span></span> <span data-ttu-id="3a749-121">Para poder usar los productos protegidos es necesario suscribirse antes a ellos,</span><span class="sxs-lookup"><span data-stu-id="3a749-121">Protected products must be subscribed to before they can be used.</span></span> <span data-ttu-id="3a749-122">mientras que los productos abiertos pueden usarse sin suscripción.</span><span class="sxs-lookup"><span data-stu-id="3a749-122">Open products can be used without a subscription.</span></span> <span data-ttu-id="3a749-123">Asegúrese de que la opción **Requerir suscripción** está seleccionada para crear un producto protegido que requiera una suscripción.</span><span class="sxs-lookup"><span data-stu-id="3a749-123">Ensure that **Require subscription** is selected to create a protected product that requires a subscription.</span></span> <span data-ttu-id="3a749-124">Esta es la configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3a749-124">This is the default setting.</span></span>

<span data-ttu-id="3a749-125">Si desea que un administrador revise y acepte o rechace los intentos de suscripción a este producto, active **Requerir aprobación de suscripción**.</span><span class="sxs-lookup"><span data-stu-id="3a749-125">If you want an administrator to review and accept or reject subscription attempts to this product, select **Require subscription approval**.</span></span> <span data-ttu-id="3a749-126">Si la casilla no está seleccionada, los intentos de suscripción se aprobarán automáticamente.</span><span class="sxs-lookup"><span data-stu-id="3a749-126">If the check box is not selected, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="3a749-127">En este ejemplo, las suscripciones se aprueban automáticamente, por lo que no tiene que seleccionar la casilla.</span><span class="sxs-lookup"><span data-stu-id="3a749-127">In this example, subscriptions are automatically approved, so do not select the box.</span></span>

<span data-ttu-id="3a749-128">Para permitir que las cuentas de desarrollador se suscriban varias veces al nuevo producto, active la casilla **Permitir varias suscripciones simultáneas** .</span><span class="sxs-lookup"><span data-stu-id="3a749-128">To allow developer accounts to subscribe multiple times to the new product, select the **Allow multiple simultaneous subscriptions** check box.</span></span> <span data-ttu-id="3a749-129">En este tutorial no se usan varias suscripciones simultáneas; por tanto, no active la casilla.</span><span class="sxs-lookup"><span data-stu-id="3a749-129">This tutorial does not utilize multiple simultaneous subscriptions, so leave it unchecked.</span></span>

<span data-ttu-id="3a749-130">Una vez especificados todos los valores, haga clic en **Guardar** para crear el producto.</span><span class="sxs-lookup"><span data-stu-id="3a749-130">After all values are entered, click **Save** to create the product.</span></span>

![Product added][api-management-product-added]

<span data-ttu-id="3a749-132">De forma predeterminada, los usuarios pueden ver los nuevos productos en el grupo **Administradores** .</span><span class="sxs-lookup"><span data-stu-id="3a749-132">By default, new products are visible to users in the **Administrators** group.</span></span> <span data-ttu-id="3a749-133">Vamos a agregar el grupo **Desarrolladores** .</span><span class="sxs-lookup"><span data-stu-id="3a749-133">We are going to add the **Developers** group.</span></span> <span data-ttu-id="3a749-134">Haga clic en **Evaluación gratuita** y, después, en la pestaña **Visibilidad**.</span><span class="sxs-lookup"><span data-stu-id="3a749-134">Click **Free Trial**, and then click the **Visibility** tab.</span></span>

> <span data-ttu-id="3a749-135">En API Management, los grupos se usan para administrar la visibilidad de productos para los desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="3a749-135">In API Management, groups are used to manage the visibility of products to developers.</span></span> <span data-ttu-id="3a749-136">Los productos conceden visibilidad a los grupos y los desarrolladores pueden ver los productos visibles a los grupos a los que pertenecen y suscribirse a ellos.</span><span class="sxs-lookup"><span data-stu-id="3a749-136">Products grant visibility to groups, and developers can view and subscribe to the products that are visible to the groups in which they belong.</span></span> <span data-ttu-id="3a749-137">Para más información, consulte [Creación y uso de grupos en Azure API Management][How to create and use groups in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="3a749-137">For more information, see [How to create and use groups in Azure API Management][How to create and use groups in Azure API Management].</span></span>
> 
> 

![Add developers group][api-management-add-developers-group]

<span data-ttu-id="3a749-139">Seleccione la casilla **Desarrolladores** y, a continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3a749-139">Select the **Developers** check box, and then click **Save**.</span></span>

## <span data-ttu-id="3a749-140"><a name="add-api"> </a>Para agregar una API al producto</span><span class="sxs-lookup"><span data-stu-id="3a749-140"><a name="add-api"> </a>To add an API to the product</span></span>
<span data-ttu-id="3a749-141">En este paso del tutorial, agregaremos la API Eco al nuevo producto Prueba gratuita.</span><span class="sxs-lookup"><span data-stu-id="3a749-141">In this step of the tutorial, we will add the Echo API to the new Free Trial product.</span></span>

> <span data-ttu-id="3a749-142">Cada instancia del servicio API Management viene previamente configurada con una API Eco que se puede usar para experimentar con API Management y aprender de esta.</span><span class="sxs-lookup"><span data-stu-id="3a749-142">Each API Management service instance comes pre-configured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="3a749-143">Para más información, consulte [Administración de su primera API en Azure API Management][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="3a749-143">For more information, see [Manage your first API in Azure API Management][Manage your first API in Azure API Management].</span></span>
> 
> 

<span data-ttu-id="3a749-144">Haga clic en **Productos** en el menú **API Management** a la izquierda y luego haga clic en **Evaluación gratuita** para configurar el producto.</span><span class="sxs-lookup"><span data-stu-id="3a749-144">Click **Products** from the **API Management** menu on the left, and then click **Free Trial** to configure the product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="3a749-146">Haga clic en **Agregar API al producto**.</span><span class="sxs-lookup"><span data-stu-id="3a749-146">Click **Add API to product**.</span></span>

![Agregar API al producto][api-management-add-api]

<span data-ttu-id="3a749-148">Seleccione **Echo API** (API Eco ) y luego haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3a749-148">Select **Echo API**, and then click **Save**.</span></span>

![Add Echo API][api-management-add-echo-api]

## <span data-ttu-id="3a749-150"><a name="policies"> </a>Para configurar las directivas de límite de frecuencia de llamadas y de cuota</span><span class="sxs-lookup"><span data-stu-id="3a749-150"><a name="policies"> </a>To configure call rate limit and quota policies</span></span>
<span data-ttu-id="3a749-151">Los límites de tasa y las cuotas se configuran en el editor de directivas.</span><span class="sxs-lookup"><span data-stu-id="3a749-151">Rate limits and quotas are configured in the policy editor.</span></span> <span data-ttu-id="3a749-152">Las dos directivas que se van a agregar en este tutorial son [Limitar la frecuencia de llamadas por suscripción](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) y [Establecer la cuota de uso por suscripción](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota).</span><span class="sxs-lookup"><span data-stu-id="3a749-152">The two policies we will be adding in this tutorial are the [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="3a749-153">Estas directivas deben aplicarse en el ámbito del producto.</span><span class="sxs-lookup"><span data-stu-id="3a749-153">These policies must be applied at the product scope.</span></span>

<span data-ttu-id="3a749-154">Haga clic en **Directivas** en el menú **API Management** de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="3a749-154">Click **Policies** under the **API Management** menu on the left.</span></span> <span data-ttu-id="3a749-155">En la lista **Producto**, haga clic en **Evaluación gratuita**.</span><span class="sxs-lookup"><span data-stu-id="3a749-155">In the **Product** list, click **Free Trial**.</span></span>

![Product policy][api-management-product-policy]

<span data-ttu-id="3a749-157">Haga clic en **Agregar directiva** para importar la plantilla de directivas y comenzar a crear la directiva de límite de frecuencia y de cuota.</span><span class="sxs-lookup"><span data-stu-id="3a749-157">Click **Add Policy** to import the policy template and begin creating the rate limit and quota policies.</span></span>

![Agregar directiva][api-management-add-policy]

<span data-ttu-id="3a749-159">Las directivas de límite de tasa y de cuota son directivas de entrada, por lo que debe posicionar el cursor en el elemento inbound.</span><span class="sxs-lookup"><span data-stu-id="3a749-159">Rate limit and quota policies are inbound policies, so position the cursor in the inbound element.</span></span>

![Policy editor][api-management-policy-editor-inbound]

<span data-ttu-id="3a749-161">Desplácese por la lista de directivas y busque la entrada de directiva para **limitar la frecuencia de llamadas por suscripción**.</span><span class="sxs-lookup"><span data-stu-id="3a749-161">Scroll through the list of policies and locate the **Limit call rate per subscription** policy entry.</span></span>

![Policy statements][api-management-limit-policies]

<span data-ttu-id="3a749-163">Una vez que el cursor se ha situado en el elemento de directiva **inbound**, haga clic en la flecha situada junto a **Limitar la frecuencia de llamadas por suscripción** para insertar su plantilla de directiva.</span><span class="sxs-lookup"><span data-stu-id="3a749-163">After the cursor is positioned in the **inbound** policy element, click the arrow beside **Limit call rate per subscription** to insert its policy template.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

<span data-ttu-id="3a749-164">Como puede ver por el fragmento de código, la directiva permite establecer los límites de las API y las operaciones del producto.</span><span class="sxs-lookup"><span data-stu-id="3a749-164">As you can see from the snippet, the policy allows setting limits for the product's APIs and operations.</span></span> <span data-ttu-id="3a749-165">En este tutorial no se usará esa funcionalidad, así que elimine los elementos **api** y **operation** del elemento **rate-limit**, de forma que solo quede el elemento **rate-limit** exterior, como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="3a749-165">In this tutorial we will not use that capability, so delete the **api** and **operation** elements from the **rate-limit** element, such that only the outer **rate-limit** element remains, as shown in the following example.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

<span data-ttu-id="3a749-166">En el producto de evaluación gratuita, la tasa máxima de llamadas permitida es de 10 llamadas por minuto; por tanto, escriba **10** como el valor para el atributo **calls** y **60** para el atributo **renewal-period**.</span><span class="sxs-lookup"><span data-stu-id="3a749-166">In the Free Trial product, the maximum allowable call rate is 10 calls per minute, so type **10** as the value for the **calls** attribute, and **60** for the **renewal-period** attribute.</span></span>

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

<span data-ttu-id="3a749-167">Para configurar la directiva **Establecer la cuota de uso por suscripción**, sitúe el cursor inmediatamente debajo del elemento **rate-limit** recién agregado dentro del elemento **inbound** y haga clic en la flecha situada a la izquierda de **Establecer la cuota de uso por suscripción**.</span><span class="sxs-lookup"><span data-stu-id="3a749-167">To configure the **Set usage quota per subscription** policy, position your cursor immediately below the newly added **rate-limit** element within the **inbound** element, and then locate and click the arrow to the left of **Set usage quota per subscription**.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

<span data-ttu-id="3a749-168">Al igual que la directiva **Limitar la frecuencia de llamadas por suscripción**, la directiva **Establecer la cuota de uso por suscripción** permite configurar los límites de las APY y las operaciones del producto.</span><span class="sxs-lookup"><span data-stu-id="3a749-168">Similarly to the **Set usage quota per subscription** policy, **Set usage quota per subscription** policy allows setting caps for on the product's APIs and operations.</span></span> <span data-ttu-id="3a749-169">En este tutorial no se usará esa funcionalidad, así que elimine los elementos **api** y **operation** del elemento **quota**, como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="3a749-169">In this tutorial we will not use that capability, so delete the **api** and **operation** elements from the **quota** element, as shown in the following example.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

<span data-ttu-id="3a749-170">Las cuotas se pueden basar en el número de llamadas por intervalo, ancho de banda o ambos.</span><span class="sxs-lookup"><span data-stu-id="3a749-170">Quotas can be based on the number of calls per interval, bandwidth, or both.</span></span> <span data-ttu-id="3a749-171">En este tutorial no estamos fijando límites en función del ancho de banda, por lo que puede eliminar el atributo **bandwidth** .</span><span class="sxs-lookup"><span data-stu-id="3a749-171">In this tutorial, we are not throttling based on bandwidth, so delete the **bandwidth** attribute.</span></span>

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

<span data-ttu-id="3a749-172">En el producto Prueba gratuita, la cuota es de 200 llamadas por semana.</span><span class="sxs-lookup"><span data-stu-id="3a749-172">In the Free Trial product, the quota is 200 calls per week.</span></span> <span data-ttu-id="3a749-173">Especifique **200** como el valor del atributo **calls** y **604800** como el valor de **renewal-period**.</span><span class="sxs-lookup"><span data-stu-id="3a749-173">Specify **200** as the value for the **calls** attribute, and then specify **604800** as the value for the **renewal-period** attribute.</span></span>

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> <span data-ttu-id="3a749-174">Los intervalos de directiva se especifican en segundos.</span><span class="sxs-lookup"><span data-stu-id="3a749-174">Policy intervals are specified in seconds.</span></span> <span data-ttu-id="3a749-175">Para calcular el intervalo para una semana, puede multiplicar el número de días (7) por el número de horas de un día (24) por el número de minutos de una hora (60) por el número de segundos de un minuto (60): 7 * 24 * 60 * 60 = 604800.</span><span class="sxs-lookup"><span data-stu-id="3a749-175">To calculate the interval for a week, you can multiply the number of days (7) by the number of hours in a day (24) by the number of minutes in an hour (60) by the number of seconds in a minute (60): 7 * 24 * 60 * 60 = 604800.</span></span>
> 
> 

<span data-ttu-id="3a749-176">Cuando haya terminado de configurar la directiva, debe coincidir con el siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3a749-176">When you have finished configuring the policy, it should match the following example.</span></span>

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

<span data-ttu-id="3a749-177">Una vez configuradas las directivas deseadas, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3a749-177">After the desired policies are configured, click **Save**.</span></span>

![Save policy][api-management-policy-save]

## <span data-ttu-id="3a749-179"><a name="publish-product"> </a> Para publicar el producto</span><span class="sxs-lookup"><span data-stu-id="3a749-179"><a name="publish-product"> </a> To publish the product</span></span>
<span data-ttu-id="3a749-180">Ahora que se agregaron las API y se configuraron las directivas, el producto debe publicarse para que los desarrolladores puedan usarlo.</span><span class="sxs-lookup"><span data-stu-id="3a749-180">Now that the the APIs are added and the policies are configured, the product must be published so that it can be used by developers.</span></span> <span data-ttu-id="3a749-181">Haga clic en **Productos** en el menú **API Management** a la izquierda y luego haga clic en **Evaluación gratuita** para configurar el producto.</span><span class="sxs-lookup"><span data-stu-id="3a749-181">Click **Products** from the **API Management** menu on the left, and then click **Free Trial** to configure the product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="3a749-183">Haga clic en **Publicar** y luego en **Sí, publicarlo** para confirmar la operación.</span><span class="sxs-lookup"><span data-stu-id="3a749-183">Click **Publish**, and then click **Yes, publish it** to confirm.</span></span>

![Publish product][api-management-publish-product]

## <span data-ttu-id="3a749-185"><a name="subscribe-account"> </a>Suscripción de una cuenta de desarrollador al producto</span><span class="sxs-lookup"><span data-stu-id="3a749-185"><a name="subscribe-account"> </a>To subscribe a developer account to the product</span></span>
<span data-ttu-id="3a749-186">Ahora que el producto se ha publicado, estará disponible para suscribirse a él y que los desarrolladores lo usen.</span><span class="sxs-lookup"><span data-stu-id="3a749-186">Now that the product is published, it is available to be subscribed to and used by developers.</span></span>

> <span data-ttu-id="3a749-187">Los administradores de una instancia de API Management se suscriben automáticamente a cada producto.</span><span class="sxs-lookup"><span data-stu-id="3a749-187">Administrators of an API Management instance are automatically subscribed to every product.</span></span> <span data-ttu-id="3a749-188">En este paso del tutorial suscribiremos una de las cuentas de desarrollador que no es de administrador al producto Prueba gratuita.</span><span class="sxs-lookup"><span data-stu-id="3a749-188">In this tutorial step, we will subscribe one of the non-administrator developer accounts to the Free Trial product.</span></span> <span data-ttu-id="3a749-189">Si la cuenta de desarrollador es parte del rol Administradores, puede seguir con este paso aunque esté suscrito.</span><span class="sxs-lookup"><span data-stu-id="3a749-189">If your developer account is part of the Administrators role, then you can follow along with this step, even though you are already subscribed.</span></span>
> 
> 

<span data-ttu-id="3a749-190">Haga clic en **Usuarios** en el menú **API Management** a la izquierda y haga clic en el nombre de su cuenta de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="3a749-190">Click **Users** on the **API Management** menu on the left, and then click the name of your developer account.</span></span> <span data-ttu-id="3a749-191">En este ejemplo usamos la cuenta del desarrollador **Clayton Gragg** .</span><span class="sxs-lookup"><span data-stu-id="3a749-191">In this example, we are using the **Clayton Gragg** developer account.</span></span>

![Configure developer][api-management-configure-developer]

<span data-ttu-id="3a749-193">Haga clic en **Agregar suscripción**.</span><span class="sxs-lookup"><span data-stu-id="3a749-193">Click **Add Subscription**.</span></span>

![Agregar suscripción][api-management-add-subscription-menu]

<span data-ttu-id="3a749-195">Seleccione **Evaluación gratuita** y, después, haga clic en **Suscribirse**.</span><span class="sxs-lookup"><span data-stu-id="3a749-195">Select **Free Trial**, and then click **Subscribe**.</span></span>

![Agregar suscripción][api-management-add-subscription]

> [!NOTE]
> <span data-ttu-id="3a749-197">En este tutorial, no está habilitada la posibilidad de varias suscripciones simultáneas para el producto de evaluación gratuita.</span><span class="sxs-lookup"><span data-stu-id="3a749-197">In this tutorial, multiple simultaneous subscriptions are not enabled for the Free Trial product.</span></span> <span data-ttu-id="3a749-198">Si lo estuvieran, se le pediría que pusiera un nombre a la suscripción, tal como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="3a749-198">If they were, you would be prompted to name the subscription, as shown in the following example.</span></span>
> 
> 

![Agregar suscripción][api-management-add-subscription-multiple]

<span data-ttu-id="3a749-200">Después de hacer clic **Suscribirse**, el producto aparece en la lista **Suscripción** del usuario.</span><span class="sxs-lookup"><span data-stu-id="3a749-200">After clicking **Subscribe**, the product appears in the **Subscription** list for the user.</span></span>

![Subscription added][api-management-subscription-added]

## <span data-ttu-id="3a749-202"><a name="test-rate-limit"> </a>Para llamar a una operación y prueba del límite de frecuencia</span><span class="sxs-lookup"><span data-stu-id="3a749-202"><a name="test-rate-limit"> </a>To call an operation and test the rate limit</span></span>
<span data-ttu-id="3a749-203">Ahora que el producto Prueba gratuita está configurado y publicado, podemos llamar a algunas operaciones y probar la directiva de límite de tasa.</span><span class="sxs-lookup"><span data-stu-id="3a749-203">Now that the Free Trial product is configured and published, we can call some operations and test the rate limit policy.</span></span>
<span data-ttu-id="3a749-204">Haga clic en **Portal para desarrolladores** en el menú superior derecho para cambiar al portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="3a749-204">Switch to the developer portal by clicking **Developer portal** in the upper-right menu.</span></span>

![portal para desarrolladores][api-management-developer-portal-menu]

<span data-ttu-id="3a749-206">Haga clic en **API** en el menú superior y, después, en **Echo API** (API Eco).</span><span class="sxs-lookup"><span data-stu-id="3a749-206">Click **APIs** in the top menu, and then click **Echo API**.</span></span>

![portal para desarrolladores][api-management-developer-portal-api-menu]

<span data-ttu-id="3a749-208">Haga clic en **GET Resource** (Recurso GET) y, después, en **Pruébelo**.</span><span class="sxs-lookup"><span data-stu-id="3a749-208">Click **GET Resource**, and then click **Try it**.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="3a749-210">Mantenga los valores predeterminados de los parámetros y seleccione la clave de suscripción para el producto de evaluación gratuita.</span><span class="sxs-lookup"><span data-stu-id="3a749-210">Keep the default parameter values, and then select your subscription key for the Free Trial product.</span></span>

![Subscription key][api-management-select-key]

> [!NOTE]
> <span data-ttu-id="3a749-212">Si tiene varias suscripciones, asegúrese de seleccionar la clave para **Prueba gratuita**ya que, de lo contrario, las directivas configuradas en los pasos anteriores no entrarán en vigor.</span><span class="sxs-lookup"><span data-stu-id="3a749-212">If you have multiple subscriptions, be sure to select the key for **Free Trial**, or else the policies that were configured in the previous steps won't be in effect.</span></span>
> 
> 

<span data-ttu-id="3a749-213">Haga clic en **Enviar**y vea la respuesta.</span><span class="sxs-lookup"><span data-stu-id="3a749-213">Click **Send**, and then view the response.</span></span> <span data-ttu-id="3a749-214">Observe el **Estado de respuesta** de **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="3a749-214">Note the **Response status** of **200 OK**.</span></span>

![Operation results][api-management-http-get-results]

<span data-ttu-id="3a749-216">Haga clic en **Enviar** en una frecuencia mayor que la directiva del límite de frecuencia de 10 llamadas por minuto.</span><span class="sxs-lookup"><span data-stu-id="3a749-216">Click **Send** at a rate greater than the rate limit policy of 10 calls per minute.</span></span> <span data-ttu-id="3a749-217">Una vez superada la directiva del límite de frecuencia, se devolverá un estado de respuesta de **429 Too many Requests** .</span><span class="sxs-lookup"><span data-stu-id="3a749-217">After the rate limit policy is exceeded, a response status of **429 Too Many Requests** is returned.</span></span>

![Operation results][api-management-http-get-429]

<span data-ttu-id="3a749-219">El valor de **Contenido de respuesta** indica el intervalo restante antes de que los reintentos sean correctos.</span><span class="sxs-lookup"><span data-stu-id="3a749-219">The **Response content** indicates the remaining interval before retries will be successful.</span></span>

<span data-ttu-id="3a749-220">Cuando la directiva de límite de tasa de 10 llamadas por minuto se aplique, las llamadas posteriores no se podrán realizar hasta que transcurran 60 segundos desde la primera de las 10 llamadas correctas al producto antes de que se superara el límite de tasa.</span><span class="sxs-lookup"><span data-stu-id="3a749-220">When the rate limit policy of 10 calls per minute is in effect, subsequent calls will fail until 60 seconds have elapsed from the first of the 10 successful calls to the product before the rate limit was exceeded.</span></span> <span data-ttu-id="3a749-221">En este ejemplo, el intervalo restante es 54 segundos.</span><span class="sxs-lookup"><span data-stu-id="3a749-221">In this example, the remaining interval is 54 seconds.</span></span>

## <span data-ttu-id="3a749-222"><a name="next-steps"> </a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3a749-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="3a749-223">Vea una demostración de la configuración de cuotas y límites de frecuencia en el siguiente vídeo.</span><span class="sxs-lookup"><span data-stu-id="3a749-223">Watch a demo of setting rate limits and quotas in the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How to create and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers to a product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API to the product]: #add-api
[Publish the product]: #publish-product
[Subscribe a developer account to the product]: #subscribe-account
[Call an operation and test the rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
