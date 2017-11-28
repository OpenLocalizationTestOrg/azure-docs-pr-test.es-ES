---
title: "notificaciones de alerta de correo electrónico toosend de acciones de escalado automático de aaaUse y webhook. | Microsoft Docs"
description: "Vea cómo toocall de acciones de escalado automático de toouse web direcciones URL o enviar notificaciones por correo electrónico en el Monitor de Azure. "
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ancav
ms.openlocfilehash: f611a18f5a808412fbdd0c89e3addb36437064c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="24531-104">Usar el escalado automático acciones toosend correo electrónico y webhook notificaciones de alerta en el Monitor de Azure</span><span class="sxs-lookup"><span data-stu-id="24531-104">Use autoscale actions toosend email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="24531-105">En este artículo se muestra cómo configurar desencadenadores para que pueda llamar a direcciones URL web específicas o enviar mensajes de correo electrónico en función de las acciones de escalado automático en Azure.</span><span class="sxs-lookup"><span data-stu-id="24531-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="24531-106">Webhooks</span><span class="sxs-lookup"><span data-stu-id="24531-106">Webhooks</span></span>
<span data-ttu-id="24531-107">Webhooks le permiten sistemas de tooother de tooroute hello Azure notificaciones de alerta para las notificaciones personalizadas o posteriores al procesamiento.</span><span class="sxs-lookup"><span data-stu-id="24531-107">Webhooks allow you tooroute hello Azure alert notifications tooother systems for post-processing or custom notifications.</span></span> <span data-ttu-id="24531-108">Por ejemplo, enrutamiento tooservices alerta Hola que pueda controlar una entrada web solicitud toosend SMS, errores de registro, notifique a un equipo mediante chat o servicios de mensajería, etc. hello webhook URI debe ser un punto de conexión HTTP o HTTPS válida.</span><span class="sxs-lookup"><span data-stu-id="24531-108">For example, routing hello alert tooservices that can handle an incoming web request toosend SMS, log bugs, notify a team using chat or messaging services, etc. hello webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="24531-109">Email</span><span class="sxs-lookup"><span data-stu-id="24531-109">Email</span></span>
<span data-ttu-id="24531-110">Correo electrónico puede enviarse tooany dirección de correo electrónico válida.</span><span class="sxs-lookup"><span data-stu-id="24531-110">Email can be sent tooany valid email address.</span></span> <span data-ttu-id="24531-111">También se notificará a los administradores y coadministradores de suscripción de Hola donde se ejecuta la regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="24531-111">Administrators and co-administrators of hello subscription where hello rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="24531-112">Aplicaciones web y servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="24531-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="24531-113">Puede participar en de hello portal de Azure para los servicios de nube y granjas de servidores (aplicaciones Web).</span><span class="sxs-lookup"><span data-stu-id="24531-113">You can opt-in from hello Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="24531-114">Elija hello **escalar** métrica.</span><span class="sxs-lookup"><span data-stu-id="24531-114">Choose hello **scale by** metric.</span></span>

![Escalar por](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="24531-116">Conjuntos de escalado de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="24531-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="24531-117">Para las máquinas virtuales más recientes creadas con Resource Manager (conjuntos de escala de máquina virtual), puede configurar esto con la API de REST, las plantillas de Resource Manager, PowerShell y CLI.</span><span class="sxs-lookup"><span data-stu-id="24531-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="24531-118">Aún no se encuentra disponible una interfaz de portal.</span><span class="sxs-lookup"><span data-stu-id="24531-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="24531-119">Cuando se utiliza la API de REST de Hola o plantilla de administrador de recursos, incluya el elemento de las notificaciones de hello con hello siguientes opciones.</span><span class="sxs-lookup"><span data-stu-id="24531-119">When using hello REST API or Resource Manager template, include hello notifications element with hello following options.</span></span>

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]
```
| <span data-ttu-id="24531-120">Campo</span><span class="sxs-lookup"><span data-stu-id="24531-120">Field</span></span> | <span data-ttu-id="24531-121">¿Obligatorio?</span><span class="sxs-lookup"><span data-stu-id="24531-121">Mandatory?</span></span> | <span data-ttu-id="24531-122">Description</span><span class="sxs-lookup"><span data-stu-id="24531-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24531-123">operación</span><span class="sxs-lookup"><span data-stu-id="24531-123">operation</span></span> |<span data-ttu-id="24531-124">yes</span><span class="sxs-lookup"><span data-stu-id="24531-124">yes</span></span> |<span data-ttu-id="24531-125">el valor debe ser "Scale"</span><span class="sxs-lookup"><span data-stu-id="24531-125">value must be "Scale"</span></span> |
| <span data-ttu-id="24531-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="24531-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="24531-127">yes</span><span class="sxs-lookup"><span data-stu-id="24531-127">yes</span></span> |<span data-ttu-id="24531-128">el valor debe ser "true" o "false"</span><span class="sxs-lookup"><span data-stu-id="24531-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="24531-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="24531-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="24531-130">yes</span><span class="sxs-lookup"><span data-stu-id="24531-130">yes</span></span> |<span data-ttu-id="24531-131">el valor debe ser "true" o "false"</span><span class="sxs-lookup"><span data-stu-id="24531-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="24531-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="24531-132">customEmails</span></span> |<span data-ttu-id="24531-133">yes</span><span class="sxs-lookup"><span data-stu-id="24531-133">yes</span></span> |<span data-ttu-id="24531-134">el valor puede ser null [] o una cadena de matriz de mensajes de correo electrónico</span><span class="sxs-lookup"><span data-stu-id="24531-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="24531-135">Webhooks</span><span class="sxs-lookup"><span data-stu-id="24531-135">webhooks</span></span> |<span data-ttu-id="24531-136">yes</span><span class="sxs-lookup"><span data-stu-id="24531-136">yes</span></span> |<span data-ttu-id="24531-137">el valor puede ser null o un identificador URI válido</span><span class="sxs-lookup"><span data-stu-id="24531-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="24531-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="24531-138">serviceUri</span></span> |<span data-ttu-id="24531-139">yes</span><span class="sxs-lookup"><span data-stu-id="24531-139">yes</span></span> |<span data-ttu-id="24531-140">un identificador URI de https válido</span><span class="sxs-lookup"><span data-stu-id="24531-140">a valid https Uri</span></span> |
| <span data-ttu-id="24531-141">propiedades</span><span class="sxs-lookup"><span data-stu-id="24531-141">properties</span></span> |<span data-ttu-id="24531-142">yes</span><span class="sxs-lookup"><span data-stu-id="24531-142">yes</span></span> |<span data-ttu-id="24531-143">el valor debe ser {} vacío o puede contener pares de clave y valor</span><span class="sxs-lookup"><span data-stu-id="24531-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="24531-144">Autenticación en Webhook</span><span class="sxs-lookup"><span data-stu-id="24531-144">Authentication in webhooks</span></span>
<span data-ttu-id="24531-145">Hola webhook puede autenticar utilizando autenticación basada en el símbolo (token), en la que guardar hello webhook URI con un identificador de símbolo (token) como un parámetro de consulta.</span><span class="sxs-lookup"><span data-stu-id="24531-145">hello webhook can authenticate using token-based authentication, where you save hello webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="24531-146">Por ejemplo, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="24531-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="24531-147">Esquema de carga de Webhook de notificación de escalado automático</span><span class="sxs-lookup"><span data-stu-id="24531-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="24531-148">Cuando se genera la notificación de escalado automático de hello, hello metadatos siguientes se incluyen en la carga de webhook de hello:</span><span class="sxs-lookup"><span data-stu-id="24531-148">When hello autoscale notification is generated, hello following metadata is included in hello webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' toocapacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| <span data-ttu-id="24531-149">Campo</span><span class="sxs-lookup"><span data-stu-id="24531-149">Field</span></span> | <span data-ttu-id="24531-150">¿Obligatorio?</span><span class="sxs-lookup"><span data-stu-id="24531-150">Mandatory?</span></span> | <span data-ttu-id="24531-151">Description</span><span class="sxs-lookup"><span data-stu-id="24531-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24531-152">status</span><span class="sxs-lookup"><span data-stu-id="24531-152">status</span></span> |<span data-ttu-id="24531-153">yes</span><span class="sxs-lookup"><span data-stu-id="24531-153">yes</span></span> |<span data-ttu-id="24531-154">estado de Hola que indica que se ha generado una acción de escalado automático</span><span class="sxs-lookup"><span data-stu-id="24531-154">hello status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="24531-155">operación</span><span class="sxs-lookup"><span data-stu-id="24531-155">operation</span></span> |<span data-ttu-id="24531-156">yes</span><span class="sxs-lookup"><span data-stu-id="24531-156">yes</span></span> |<span data-ttu-id="24531-157">Para un aumento de instancias, será "Escalar horizontalmente"; para una disminución de instancias, "Reducir horizontalmente".</span><span class="sxs-lookup"><span data-stu-id="24531-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="24531-158">contexto</span><span class="sxs-lookup"><span data-stu-id="24531-158">context</span></span> |<span data-ttu-id="24531-159">yes</span><span class="sxs-lookup"><span data-stu-id="24531-159">yes</span></span> |<span data-ttu-id="24531-160">contexto de acción de escalado automático de Hola</span><span class="sxs-lookup"><span data-stu-id="24531-160">hello autoscale action context</span></span> |
| <span data-ttu-id="24531-161">timestamp</span><span class="sxs-lookup"><span data-stu-id="24531-161">timestamp</span></span> |<span data-ttu-id="24531-162">yes</span><span class="sxs-lookup"><span data-stu-id="24531-162">yes</span></span> |<span data-ttu-id="24531-163">Marca de tiempo cuando se activó la acción de escalado automático de Hola</span><span class="sxs-lookup"><span data-stu-id="24531-163">Time stamp when hello autoscale action was triggered</span></span> |
| <span data-ttu-id="24531-164">id</span><span class="sxs-lookup"><span data-stu-id="24531-164">id</span></span> |<span data-ttu-id="24531-165">Sí</span><span class="sxs-lookup"><span data-stu-id="24531-165">Yes</span></span> |<span data-ttu-id="24531-166">Id. de administrador de recursos de configuración de escalado automático de Hola</span><span class="sxs-lookup"><span data-stu-id="24531-166">Resource Manager ID of hello autoscale setting</span></span> |
| <span data-ttu-id="24531-167">name</span><span class="sxs-lookup"><span data-stu-id="24531-167">name</span></span> |<span data-ttu-id="24531-168">Sí</span><span class="sxs-lookup"><span data-stu-id="24531-168">Yes</span></span> |<span data-ttu-id="24531-169">nombre de Hola de configuración de escalado automático de Hola</span><span class="sxs-lookup"><span data-stu-id="24531-169">hello name of hello autoscale setting</span></span> |
| <span data-ttu-id="24531-170">details</span><span class="sxs-lookup"><span data-stu-id="24531-170">details</span></span> |<span data-ttu-id="24531-171">Sí</span><span class="sxs-lookup"><span data-stu-id="24531-171">Yes</span></span> |<span data-ttu-id="24531-172">Explicación de la acción de Hola que tardó el servicio de escalado automático de Hola y Hola cambio en el número de instancias de Hola</span><span class="sxs-lookup"><span data-stu-id="24531-172">Explanation of hello action that hello autoscale service took and hello change in hello instance count</span></span> |
| <span data-ttu-id="24531-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="24531-173">subscriptionId</span></span> |<span data-ttu-id="24531-174">Sí</span><span class="sxs-lookup"><span data-stu-id="24531-174">Yes</span></span> |<span data-ttu-id="24531-175">Id. de suscripción de recurso de destino de Hola que se ajusta la escala</span><span class="sxs-lookup"><span data-stu-id="24531-175">Subscription ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="24531-176">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="24531-176">resourceGroupName</span></span> |<span data-ttu-id="24531-177">Sí</span><span class="sxs-lookup"><span data-stu-id="24531-177">Yes</span></span> |<span data-ttu-id="24531-178">Nombre de grupo de recursos del recurso de destino de Hola que se ajusta la escala</span><span class="sxs-lookup"><span data-stu-id="24531-178">Resource Group name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="24531-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="24531-179">resourceName</span></span> |<span data-ttu-id="24531-180">Sí</span><span class="sxs-lookup"><span data-stu-id="24531-180">Yes</span></span> |<span data-ttu-id="24531-181">Nombre del recurso de destino de Hola que se ajusta la escala</span><span class="sxs-lookup"><span data-stu-id="24531-181">Name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="24531-182">resourceType</span><span class="sxs-lookup"><span data-stu-id="24531-182">resourceType</span></span> |<span data-ttu-id="24531-183">Sí</span><span class="sxs-lookup"><span data-stu-id="24531-183">Yes</span></span> |<span data-ttu-id="24531-184">Hola tres valores admitidos: "microsoft.classiccompute/domainnames/slots/roles" - roles, "microsoft.compute/virtualmachinescalesets" - conjuntos de escalas de máquina Virtual y "Microsoft.Web/serverfarms -" aplicación Web de servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="24531-184">hello three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="24531-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="24531-185">resourceId</span></span> |<span data-ttu-id="24531-186">Sí</span><span class="sxs-lookup"><span data-stu-id="24531-186">Yes</span></span> |<span data-ttu-id="24531-187">Id. de administrador de recursos del recurso de destino de Hola que se ajusta la escala</span><span class="sxs-lookup"><span data-stu-id="24531-187">Resource Manager ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="24531-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="24531-188">portalLink</span></span> |<span data-ttu-id="24531-189">Sí</span><span class="sxs-lookup"><span data-stu-id="24531-189">Yes</span></span> |<span data-ttu-id="24531-190">Página de resumen de toohello de enlace del portal Azure de recurso de destino de Hola</span><span class="sxs-lookup"><span data-stu-id="24531-190">Azure portal link toohello summary page of hello target resource</span></span> |
| <span data-ttu-id="24531-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="24531-191">oldCapacity</span></span> |<span data-ttu-id="24531-192">Sí</span><span class="sxs-lookup"><span data-stu-id="24531-192">Yes</span></span> |<span data-ttu-id="24531-193">Hola (antiguo) recuento de instancias actual cuando el escalado automático ha realizado una acción de escala</span><span class="sxs-lookup"><span data-stu-id="24531-193">hello current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="24531-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="24531-194">newCapacity</span></span> |<span data-ttu-id="24531-195">Sí</span><span class="sxs-lookup"><span data-stu-id="24531-195">Yes</span></span> |<span data-ttu-id="24531-196">recuento de instancias nuevas de Hola que escalado automático escala recursos Hola demasiado</span><span class="sxs-lookup"><span data-stu-id="24531-196">hello new instance count that Autoscale scaled hello resource too</span></span>|
| <span data-ttu-id="24531-197">Propiedades</span><span class="sxs-lookup"><span data-stu-id="24531-197">Properties</span></span> |<span data-ttu-id="24531-198">No</span><span class="sxs-lookup"><span data-stu-id="24531-198">No</span></span> |<span data-ttu-id="24531-199">Opcional.</span><span class="sxs-lookup"><span data-stu-id="24531-199">Optional.</span></span> <span data-ttu-id="24531-200">Conjunto de pares <Clave, Valor> (por ejemplo, Diccionario <Cadena, Cadena>).</span><span class="sxs-lookup"><span data-stu-id="24531-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="24531-201">campo de propiedades de Hello es opcional.</span><span class="sxs-lookup"><span data-stu-id="24531-201">hello properties field is optional.</span></span> <span data-ttu-id="24531-202">En una interfaz de usuario personalizada o un flujo de trabajo de aplicación en función de lógica, puede escribir las claves y valores que se pueden pasar mediante la carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="24531-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using hello payload.</span></span> <span data-ttu-id="24531-203">Una forma alternativa de propiedades personalizadas de toopass hacer copia de llamada de webhook salida toohello es toouse hello webhook URI (como parámetros de consulta)</span><span class="sxs-lookup"><span data-stu-id="24531-203">An alternate way toopass custom properties back toohello outgoing webhook call is toouse hello webhook URI itself (as query parameters)</span></span> |
