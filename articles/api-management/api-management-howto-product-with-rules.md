---
title: "aaaProtect su API con administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooprotect su API con las cuotas y la limitación de las directivas (limitación de velocidad)."
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
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a><span data-ttu-id="8759f-103">Protección de su API con límites de frecuencia mediante Azure API Management</span><span class="sxs-lookup"><span data-stu-id="8759f-103">Protect your API with rate limits using Azure API Management</span></span>
<span data-ttu-id="8759f-104">Esta guía muestra lo fácil que es tooadd protección para el API de back-end mediante la configuración de directivas de límite y la cuota de la tasa con la administración de API de Azure.</span><span class="sxs-lookup"><span data-stu-id="8759f-104">This guide shows you how easy it is tooadd protection for your backend API by configuring rate limit and quota policies with Azure API Management.</span></span>

<span data-ttu-id="8759f-105">En este tutorial, aprenderá a crear un producto de "Prueba gratuita" API que permite a los desarrolladores toomake too10 llamadas por minuto e instalación tooa máximo de 200 llamadas por semana tooyour API con hello [limitar la tasa de llamadas por suscripción](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) y [ Establecer la cuota de uso por suscripción](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) directivas.</span><span class="sxs-lookup"><span data-stu-id="8759f-105">In this tutorial, you will create a "Free Trial" API product that allows developers toomake up too10 calls per minute and up tooa maximum of 200 calls per week tooyour API using hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="8759f-106">Podrá publicar API hello y probar la directiva de límite de velocidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-106">You will then publish hello API and test hello rate limit policy.</span></span>

<span data-ttu-id="8759f-107">Más avanzados limitación escenarios con hello [límite de velocidad por clave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) y [cuota por clave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) directivas, vea [solicitud avanzada limitación con administración de API de Azure](api-management-sample-flexible-throttling.md).</span><span class="sxs-lookup"><span data-stu-id="8759f-107">For more advanced throttling scenarios using hello [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies, see [Advanced request throttling with Azure API Management](api-management-sample-flexible-throttling.md).</span></span>

## <span data-ttu-id="8759f-108"><a name="create-product"></a>toocreate un producto</span><span class="sxs-lookup"><span data-stu-id="8759f-108"><a name="create-product"> </a>toocreate a product</span></span>
<span data-ttu-id="8759f-109">En este paso, creará un producto de evaluación gratuita que no requiere aprobación de suscripción.</span><span class="sxs-lookup"><span data-stu-id="8759f-109">In this step, you will create a Free Trial product that does not require subscription approval.</span></span>

> [!NOTE]
> <span data-ttu-id="8759f-110">Si ya tiene un producto configurado y desea toouse, para este tutorial, puede saltar a continuación demasiado[configurar directivas de límite y la cuota de tasa de llamadas] [ Configure call rate limit and quota policies] y siga el tutorial de Hola desde ahí con el producto en lugar de producto de evaluación gratuita de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-110">If you already have a product configured and want toouse it for this tutorial, you can jump ahead too[Configure call rate limit and quota policies][Configure call rate limit and quota policies] and follow hello tutorial from there using your product in place of hello Free Trial product.</span></span>
> 
> 

<span data-ttu-id="8759f-111">tooget iniciado, haga clic en **portal para desarrolladores de** Hola Portal de Azure para el servicio de administración de API.</span><span class="sxs-lookup"><span data-stu-id="8759f-111">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portal del publicador][api-management-management-console]

> <span data-ttu-id="8759f-113">Si aún no ha creado una instancia de servicio de administración de API, consulte [crear una instancia de servicio de administración de API] [ Create an API Management service instance] en hello [administrar su primera API de administración de API de Azure] [ Manage your first API in Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="8759f-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API in Azure API Management][Manage your first API in Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="8759f-114">Haga clic en **productos** en hello **administración de API** menú Hola toodisplay izquierdo Hola **productos** página.</span><span class="sxs-lookup"><span data-stu-id="8759f-114">Click **Products** in hello **API Management** menu on hello left toodisplay hello **Products** page.</span></span>

![Add product][api-management-add-product]

<span data-ttu-id="8759f-116">Haga clic en **agregar producto** toodisplay hello **Agregar nuevo producto** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="8759f-116">Click **Add product** toodisplay hello **Add new product** dialog box.</span></span>

![Agregar nuevo producto][api-management-new-product-window]

<span data-ttu-id="8759f-118">Hola **título** , escriba **gratuita**.</span><span class="sxs-lookup"><span data-stu-id="8759f-118">In hello **Title** box, type **Free Trial**.</span></span>

<span data-ttu-id="8759f-119">Hola **descripción** cuadro, Hola de tipo siguiente texto: **suscriptores van a ser capaz de toorun 10 llamadas por minuto seguridad tooa máximo de 200 llamadas/semana después del cual se deniega el acceso.**</span><span class="sxs-lookup"><span data-stu-id="8759f-119">In hello **Description** box, type hello following text: **Subscribers will be able toorun 10 calls/minute up tooa maximum of 200 calls/week after which access is denied.**</span></span>

<span data-ttu-id="8759f-120">Los productos de API Management pueden estar abiertos o protegidos.</span><span class="sxs-lookup"><span data-stu-id="8759f-120">Products in API Management can be protected or open.</span></span> <span data-ttu-id="8759f-121">Productos protegidos deben ser toobefore suscrito se pueden usar.</span><span class="sxs-lookup"><span data-stu-id="8759f-121">Protected products must be subscribed toobefore they can be used.</span></span> <span data-ttu-id="8759f-122">mientras que los productos abiertos pueden usarse sin suscripción.</span><span class="sxs-lookup"><span data-stu-id="8759f-122">Open products can be used without a subscription.</span></span> <span data-ttu-id="8759f-123">Asegúrese de que **requieren suscripción** es toocreate seleccionado un producto protegido que requiere una suscripción.</span><span class="sxs-lookup"><span data-stu-id="8759f-123">Ensure that **Require subscription** is selected toocreate a protected product that requires a subscription.</span></span> <span data-ttu-id="8759f-124">Se trata de una configuración predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-124">This is hello default setting.</span></span>

<span data-ttu-id="8759f-125">Si desea que un administrador tooreview y Aceptar o rechazar suscripción intenta toothis producto, seleccione **requieren la aprobación de suscripción**.</span><span class="sxs-lookup"><span data-stu-id="8759f-125">If you want an administrator tooreview and accept or reject subscription attempts toothis product, select **Require subscription approval**.</span></span> <span data-ttu-id="8759f-126">Si no se selecciona la casilla de verificación de hello, intentos de suscripción será aprobada automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8759f-126">If hello check box is not selected, subscription attempts will be auto-approved.</span></span> <span data-ttu-id="8759f-127">En este ejemplo, las suscripciones se aprueban automáticamente, por lo que no se active la casilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-127">In this example, subscriptions are automatically approved, so do not select hello box.</span></span>

<span data-ttu-id="8759f-128">cuentas de desarrollador tooallow toosubscribe toohello nuevo producto de varias veces, seleccione hello **permitir múltiples suscripciones simultáneas** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="8759f-128">tooallow developer accounts toosubscribe multiple times toohello new product, select hello **Allow multiple simultaneous subscriptions** check box.</span></span> <span data-ttu-id="8759f-129">En este tutorial no se usan varias suscripciones simultáneas; por tanto, no active la casilla.</span><span class="sxs-lookup"><span data-stu-id="8759f-129">This tutorial does not utilize multiple simultaneous subscriptions, so leave it unchecked.</span></span>

<span data-ttu-id="8759f-130">Después de introducen todos los valores, haga clic en **guardar** producto de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8759f-130">After all values are entered, click **Save** toocreate hello product.</span></span>

![Product added][api-management-product-added]

<span data-ttu-id="8759f-132">De forma predeterminada, los nuevos productos están toousers visible en hello **administradores** grupo.</span><span class="sxs-lookup"><span data-stu-id="8759f-132">By default, new products are visible toousers in hello **Administrators** group.</span></span> <span data-ttu-id="8759f-133">Vamos hello tooadd **a los desarrolladores** grupo.</span><span class="sxs-lookup"><span data-stu-id="8759f-133">We are going tooadd hello **Developers** group.</span></span> <span data-ttu-id="8759f-134">Haga clic en **gratuita**y, a continuación, haga clic en hello **visibilidad** ficha.</span><span class="sxs-lookup"><span data-stu-id="8759f-134">Click **Free Trial**, and then click hello **Visibility** tab.</span></span>

> <span data-ttu-id="8759f-135">Administración de API, los grupos son utilizados toomanage Hola visibilidad de toodevelopers de productos.</span><span class="sxs-lookup"><span data-stu-id="8759f-135">In API Management, groups are used toomanage hello visibility of products toodevelopers.</span></span> <span data-ttu-id="8759f-136">Productos conceder toogroups de visibilidad, y los desarrolladores pueden ver y suscribirse toohello productos que son grupos de toohello visible en la que pertenecen.</span><span class="sxs-lookup"><span data-stu-id="8759f-136">Products grant visibility toogroups, and developers can view and subscribe toohello products that are visible toohello groups in which they belong.</span></span> <span data-ttu-id="8759f-137">Para obtener más información, consulte [cómo toocreate y use los grupos de administración de API de Azure][How toocreate and use groups in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="8759f-137">For more information, see [How toocreate and use groups in Azure API Management][How toocreate and use groups in Azure API Management].</span></span>
> 
> 

![Add developers group][api-management-add-developers-group]

<span data-ttu-id="8759f-139">Seleccione hello **a los desarrolladores** casilla de verificación y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="8759f-139">Select hello **Developers** check box, and then click **Save**.</span></span>

## <span data-ttu-id="8759f-140"><a name="add-api"></a>tooadd una API toohello producto</span><span class="sxs-lookup"><span data-stu-id="8759f-140"><a name="add-api"> </a>tooadd an API toohello product</span></span>
<span data-ttu-id="8759f-141">En este paso del tutorial de hello, agregaremos Hola eco API toohello nuevo gratuita producto.</span><span class="sxs-lookup"><span data-stu-id="8759f-141">In this step of hello tutorial, we will add hello Echo API toohello new Free Trial product.</span></span>

> <span data-ttu-id="8759f-142">Cada instancia de servicio de administración de API viene preconfigurado con una API de eco que se pueden tooexperiment usado con y obtener información acerca de la API de administración.</span><span class="sxs-lookup"><span data-stu-id="8759f-142">Each API Management service instance comes pre-configured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="8759f-143">Para más información, consulte [Administración de su primera API en Azure API Management][Manage your first API in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="8759f-143">For more information, see [Manage your first API in Azure API Management][Manage your first API in Azure API Management].</span></span>
> 
> 

<span data-ttu-id="8759f-144">Haga clic en **productos** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **gratuita** producto de hello tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="8759f-144">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="8759f-146">Haga clic en **tooproduct agregar API**.</span><span class="sxs-lookup"><span data-stu-id="8759f-146">Click **Add API tooproduct**.</span></span>

![Agregar API tooproduct][api-management-add-api]

<span data-ttu-id="8759f-148">Seleccione **Echo API** (API Eco ) y luego haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="8759f-148">Select **Echo API**, and then click **Save**.</span></span>

![Add Echo API][api-management-add-echo-api]

## <span data-ttu-id="8759f-150"><a name="policies"></a>tooconfigure las directivas de límite y la cuota de tasa de llamadas</span><span class="sxs-lookup"><span data-stu-id="8759f-150"><a name="policies"> </a>tooconfigure call rate limit and quota policies</span></span>
<span data-ttu-id="8759f-151">Límites de velocidad y las cuotas se configuran en el editor de directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-151">Rate limits and quotas are configured in hello policy editor.</span></span> <span data-ttu-id="8759f-152">las directivas de Hello dos que se va a agregar en este tutorial son hello [limitar la tasa de llamadas por suscripción](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) y [establecer la cuota de uso por suscripción](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) directivas.</span><span class="sxs-lookup"><span data-stu-id="8759f-152">hello two policies we will be adding in this tutorial are hello [Limit call rate per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota per subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) policies.</span></span> <span data-ttu-id="8759f-153">Estas directivas deben aplicarse en el ámbito del producto de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-153">These policies must be applied at hello product scope.</span></span>

<span data-ttu-id="8759f-154">Haga clic en **directivas** en hello **administración de API** menú de hello izquierda.</span><span class="sxs-lookup"><span data-stu-id="8759f-154">Click **Policies** under hello **API Management** menu on hello left.</span></span> <span data-ttu-id="8759f-155">Hola **producto** lista, haga clic en **gratuita**.</span><span class="sxs-lookup"><span data-stu-id="8759f-155">In hello **Product** list, click **Free Trial**.</span></span>

![Product policy][api-management-product-policy]

<span data-ttu-id="8759f-157">Haga clic en **Agregar directiva** tooimport Hola plantilla de directiva y empezar a crear directivas de cuota y el límite de velocidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-157">Click **Add Policy** tooimport hello policy template and begin creating hello rate limit and quota policies.</span></span>

![Add policy][api-management-add-policy]

<span data-ttu-id="8759f-159">Tasa límite y la cuota directivas son entrante, por lo que posición Hola cursor en el elemento de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-159">Rate limit and quota policies are inbound policies, so position hello cursor in hello inbound element.</span></span>

![Policy editor][api-management-policy-editor-inbound]

<span data-ttu-id="8759f-161">Desplácese por la lista de directivas de Hola y busque hello **limitar la tasa de llamadas por suscripción** entrada de directiva.</span><span class="sxs-lookup"><span data-stu-id="8759f-161">Scroll through hello list of policies and locate hello **Limit call rate per subscription** policy entry.</span></span>

![Policy statements][api-management-limit-policies]

<span data-ttu-id="8759f-163">Después de hello cursor se coloca en hello **entrada** elemento de directiva, haga clic en la flecha de hello junto a **limitar la tasa de llamadas por suscripción** tooinsert su plantilla de directiva.</span><span class="sxs-lookup"><span data-stu-id="8759f-163">After hello cursor is positioned in hello **inbound** policy element, click hello arrow beside **Limit call rate per subscription** tooinsert its policy template.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

<span data-ttu-id="8759f-164">Como puede ver en el fragmento de código de hello, directiva de hello permite establecer límites para el producto Hola API y operaciones.</span><span class="sxs-lookup"><span data-stu-id="8759f-164">As you can see from hello snippet, hello policy allows setting limits for hello product's APIs and operations.</span></span> <span data-ttu-id="8759f-165">En este tutorial se utilizará no esa capacidad, por lo que elimina hello **api** y **operación** elementos de hello **límite de velocidad** elemento, de forma que solo Hola externa**límite de velocidad** elemento permanece, tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-165">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **rate-limit** element, such that only hello outer **rate-limit** element remains, as shown in hello following example.</span></span>

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

<span data-ttu-id="8759f-166">En el producto de evaluación gratuita de hello, velocidad máxima permitida de llamadas de hello es 10 llamadas por minuto, así que escriba **10** como valor de Hola de hello **llamadas** atributo, y **60** para hello **período de renovación** atributo.</span><span class="sxs-lookup"><span data-stu-id="8759f-166">In hello Free Trial product, hello maximum allowable call rate is 10 calls per minute, so type **10** as hello value for hello **calls** attribute, and **60** for hello **renewal-period** attribute.</span></span>

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

<span data-ttu-id="8759f-167">Hola tooconfigure **establecer la cuota de uso por suscripción** directiva, posición el cursor se encuentra justo debajo Hola recién agregado **límite de velocidad** elemento dentro de hello **entrada** elemento y, a continuación, busque y haga clic en hello flecha toohello a la izquierda de **establecer la cuota de uso por suscripción**.</span><span class="sxs-lookup"><span data-stu-id="8759f-167">tooconfigure hello **Set usage quota per subscription** policy, position your cursor immediately below hello newly added **rate-limit** element within hello **inbound** element, and then locate and click hello arrow toohello left of **Set usage quota per subscription**.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

<span data-ttu-id="8759f-168">Del mismo modo toohello **establecer la cuota de uso por suscripción** directiva, **establecer la cuota de uso por suscripción** directiva permite configurar extremos para en las operaciones y las API del producto de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-168">Similarly toohello **Set usage quota per subscription** policy, **Set usage quota per subscription** policy allows setting caps for on hello product's APIs and operations.</span></span> <span data-ttu-id="8759f-169">En este tutorial se utilizará no esa capacidad, por lo que elimina hello **api** y **operación** elementos de hello **cuota** elemento, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-169">In this tutorial we will not use that capability, so delete hello **api** and **operation** elements from hello **quota** element, as shown in hello following example.</span></span>

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

<span data-ttu-id="8759f-170">Las cuotas pueden basarse en número de Hola de llamadas por intervalo, el ancho de banda o ambos.</span><span class="sxs-lookup"><span data-stu-id="8759f-170">Quotas can be based on hello number of calls per interval, bandwidth, or both.</span></span> <span data-ttu-id="8759f-171">En este tutorial, no nos estamos limitación en función de ancho de banda, por lo que elimine hello **ancho de banda** atributo.</span><span class="sxs-lookup"><span data-stu-id="8759f-171">In this tutorial, we are not throttling based on bandwidth, so delete hello **bandwidth** attribute.</span></span>

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

<span data-ttu-id="8759f-172">En el producto de evaluación gratuita de hello, cuota de hello es 200 llamadas por semana.</span><span class="sxs-lookup"><span data-stu-id="8759f-172">In hello Free Trial product, hello quota is 200 calls per week.</span></span> <span data-ttu-id="8759f-173">Especifique **200** como valor de Hola de hello **llamadas** de atributo y, a continuación, especifique **604800** como valor de Hola de hello **período de renovación** atributo.</span><span class="sxs-lookup"><span data-stu-id="8759f-173">Specify **200** as hello value for hello **calls** attribute, and then specify **604800** as hello value for hello **renewal-period** attribute.</span></span>

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> <span data-ttu-id="8759f-174">Los intervalos de directiva se especifican en segundos.</span><span class="sxs-lookup"><span data-stu-id="8759f-174">Policy intervals are specified in seconds.</span></span> <span data-ttu-id="8759f-175">intervalo de saludo toocalculate durante una semana, puede multiplicar número Hola de días (7) mediante el número de horas en un día (24) por número de Hola de minutos durante una hora (60) mediante el número de segundos en un minuto (60) Hola Hola: 7 * 24 * 60 * 60 = 604800.</span><span class="sxs-lookup"><span data-stu-id="8759f-175">toocalculate hello interval for a week, you can multiply hello number of days (7) by hello number of hours in a day (24) by hello number of minutes in an hour (60) by hello number of seconds in a minute (60): 7 * 24 * 60 * 60 = 604800.</span></span>
> 
> 

<span data-ttu-id="8759f-176">Cuando haya terminado de configurar la directiva de hello, debe coincidir con el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-176">When you have finished configuring hello policy, it should match hello following example.</span></span>

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

<span data-ttu-id="8759f-177">Después de hello deseado se configuran las directivas, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="8759f-177">After hello desired policies are configured, click **Save**.</span></span>

![Save policy][api-management-policy-save]

## <span data-ttu-id="8759f-179"><a name="publish-product"></a> producto de hello toopublish</span><span class="sxs-lookup"><span data-stu-id="8759f-179"><a name="publish-product"> </a> toopublish hello product</span></span>
<span data-ttu-id="8759f-180">Ahora que hello hello las API se agregan y se configuran las directivas de hello, producto Hola debe publicarse para que los desarrolladores pueden usar.</span><span class="sxs-lookup"><span data-stu-id="8759f-180">Now that hello hello APIs are added and hello policies are configured, hello product must be published so that it can be used by developers.</span></span> <span data-ttu-id="8759f-181">Haga clic en **productos** de hello **administración de API** menú Hola izquierda y, a continuación, haga clic en **gratuita** producto de hello tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="8759f-181">Click **Products** from hello **API Management** menu on hello left, and then click **Free Trial** tooconfigure hello product.</span></span>

![Configure product][api-management-configure-product]

<span data-ttu-id="8759f-183">Haga clic en **publicar**y, a continuación, haga clic en **Sí, publicarlo** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="8759f-183">Click **Publish**, and then click **Yes, publish it** tooconfirm.</span></span>

![Publish product][api-management-publish-product]

## <span data-ttu-id="8759f-185"><a name="subscribe-account"></a>toosubscribe un producto de toohello de cuenta de desarrollador</span><span class="sxs-lookup"><span data-stu-id="8759f-185"><a name="subscribe-account"> </a>toosubscribe a developer account toohello product</span></span>
<span data-ttu-id="8759f-186">Ahora se publica ese producto hello, es tooand toobe disponibles suscrito la usan los programadores.</span><span class="sxs-lookup"><span data-stu-id="8759f-186">Now that hello product is published, it is available toobe subscribed tooand used by developers.</span></span>

> <span data-ttu-id="8759f-187">Los administradores de una instancia de la administración de API son producto tooevery automáticamente suscrito.</span><span class="sxs-lookup"><span data-stu-id="8759f-187">Administrators of an API Management instance are automatically subscribed tooevery product.</span></span> <span data-ttu-id="8759f-188">En este paso del tutorial, se suscribirá uno de producto de evaluación gratuita de hello desarrollador sin privilegios de administrador cuentas toohello.</span><span class="sxs-lookup"><span data-stu-id="8759f-188">In this tutorial step, we will subscribe one of hello non-administrator developer accounts toohello Free Trial product.</span></span> <span data-ttu-id="8759f-189">Si la cuenta de desarrollador forma parte del rol de administradores de hello, después, puede seguir este paso, incluso si ya está suscrito.</span><span class="sxs-lookup"><span data-stu-id="8759f-189">If your developer account is part of hello Administrators role, then you can follow along with this step, even though you are already subscribed.</span></span>
> 
> 

<span data-ttu-id="8759f-190">Haga clic en **usuarios** en hello **administración de API** menú Hola izquierda y, a continuación, haga clic en nombre de saludo de la cuenta de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="8759f-190">Click **Users** on hello **API Management** menu on hello left, and then click hello name of your developer account.</span></span> <span data-ttu-id="8759f-191">En este ejemplo, estamos utilizando hello **Clayton Gragg** cuenta de desarrollador.</span><span class="sxs-lookup"><span data-stu-id="8759f-191">In this example, we are using hello **Clayton Gragg** developer account.</span></span>

![Configure developer][api-management-configure-developer]

<span data-ttu-id="8759f-193">Haga clic en **Agregar suscripción**.</span><span class="sxs-lookup"><span data-stu-id="8759f-193">Click **Add Subscription**.</span></span>

![Agregar suscripción][api-management-add-subscription-menu]

<span data-ttu-id="8759f-195">Seleccione **Evaluación gratuita** y, después, haga clic en **Suscribirse**.</span><span class="sxs-lookup"><span data-stu-id="8759f-195">Select **Free Trial**, and then click **Subscribe**.</span></span>

![Agregar suscripción][api-management-add-subscription]

> [!NOTE]
> <span data-ttu-id="8759f-197">En este tutorial, varias suscripciones simultáneas no están habilitadas para el producto de evaluación gratuita de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-197">In this tutorial, multiple simultaneous subscriptions are not enabled for hello Free Trial product.</span></span> <span data-ttu-id="8759f-198">Si se hubieran, sería tooname solicitadas Hola suscripción, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-198">If they were, you would be prompted tooname hello subscription, as shown in hello following example.</span></span>
> 
> 

![Agregar suscripción][api-management-add-subscription-multiple]

<span data-ttu-id="8759f-200">Después de hacer clic **suscribir**, producto Hola aparece en hello **suscripción** lista para el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-200">After clicking **Subscribe**, hello product appears in hello **Subscription** list for hello user.</span></span>

![Subscription added][api-management-subscription-added]

## <span data-ttu-id="8759f-202"><a name="test-rate-limit"></a>toocall un límite de velocidad de Hola de operación y prueba</span><span class="sxs-lookup"><span data-stu-id="8759f-202"><a name="test-rate-limit"> </a>toocall an operation and test hello rate limit</span></span>
<span data-ttu-id="8759f-203">Ahora que hello producto de evaluación gratuita se configura y se publica, podemos llamar a algunas operaciones y probar la directiva de límite de velocidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-203">Now that hello Free Trial product is configured and published, we can call some operations and test hello rate limit policy.</span></span>
<span data-ttu-id="8759f-204">Portal para desarrolladores de conmutador toohello haciendo clic en **portal para desarrolladores de** en el menú de hello superior derecha.</span><span class="sxs-lookup"><span data-stu-id="8759f-204">Switch toohello developer portal by clicking **Developer portal** in hello upper-right menu.</span></span>

![portal para desarrolladores][api-management-developer-portal-menu]

<span data-ttu-id="8759f-206">Haga clic en **API** en Hola menú superior y, a continuación, haga clic en **API de eco**.</span><span class="sxs-lookup"><span data-stu-id="8759f-206">Click **APIs** in hello top menu, and then click **Echo API**.</span></span>

![portal para desarrolladores][api-management-developer-portal-api-menu]

<span data-ttu-id="8759f-208">Haga clic en **GET Resource** (Recurso GET) y, después, en **Pruébelo**.</span><span class="sxs-lookup"><span data-stu-id="8759f-208">Click **GET Resource**, and then click **Try it**.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="8759f-210">Mantener valores de parámetro de predeterminado de hello y, a continuación, seleccione la clave de suscripción para el producto de evaluación gratuita de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-210">Keep hello default parameter values, and then select your subscription key for hello Free Trial product.</span></span>

![Subscription key][api-management-select-key]

> [!NOTE]
> <span data-ttu-id="8759f-212">Si tiene varias suscripciones, ser seguro de clave de Hola de tooselect para **gratuita**, o más directivas de Hola que se configuraron en pasos anteriores hello no estará en vigor.</span><span class="sxs-lookup"><span data-stu-id="8759f-212">If you have multiple subscriptions, be sure tooselect hello key for **Free Trial**, or else hello policies that were configured in hello previous steps won't be in effect.</span></span>
> 
> 

<span data-ttu-id="8759f-213">Haga clic en **enviar**y, a continuación, ver la respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-213">Click **Send**, and then view hello response.</span></span> <span data-ttu-id="8759f-214">Hola Nota **estado de respuesta** de **200 Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8759f-214">Note hello **Response status** of **200 OK**.</span></span>

![Operation results][api-management-http-get-results]

<span data-ttu-id="8759f-216">Haga clic en **enviar** a una velocidad mayor que la directiva de límite de velocidad de Hola de 10 llamadas por minuto.</span><span class="sxs-lookup"><span data-stu-id="8759f-216">Click **Send** at a rate greater than hello rate limit policy of 10 calls per minute.</span></span> <span data-ttu-id="8759f-217">Después de que se supera la directiva de límite de velocidad de hello, el estado de respuesta **429 demasiado muchas solicitudes** se devuelve.</span><span class="sxs-lookup"><span data-stu-id="8759f-217">After hello rate limit policy is exceeded, a response status of **429 Too Many Requests** is returned.</span></span>

![Operation results][api-management-http-get-429]

<span data-ttu-id="8759f-219">Hola **contenido de la respuesta** indica Hola restantes intervalo antes de reintentos se realice correctamente.</span><span class="sxs-lookup"><span data-stu-id="8759f-219">hello **Response content** indicates hello remaining interval before retries will be successful.</span></span>

<span data-ttu-id="8759f-220">Cuando la directiva de límite de velocidad de Hola de 10 llamadas por minuto está habilitada, las llamadas subsiguientes se producirá un error hasta que hayan transcurrido 60 segundos de hello primer de producto de toohello de hello 10 llamadas correctas antes de que se ha superado el límite de velocidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="8759f-220">When hello rate limit policy of 10 calls per minute is in effect, subsequent calls will fail until 60 seconds have elapsed from hello first of hello 10 successful calls toohello product before hello rate limit was exceeded.</span></span> <span data-ttu-id="8759f-221">En este ejemplo, hello restantes intervalo es 54 segundos.</span><span class="sxs-lookup"><span data-stu-id="8759f-221">In this example, hello remaining interval is 54 seconds.</span></span>

## <span data-ttu-id="8759f-222"><a name="next-steps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8759f-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="8759f-223">Vea una demostración de establecer límites de velocidad y las cuotas en hello después de vídeo.</span><span class="sxs-lookup"><span data-stu-id="8759f-223">Watch a demo of setting rate limits and quotas in hello following video.</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
