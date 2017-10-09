---
title: "aaaAdvanced escalado automático con máquinas virtuales de Azure | Documentos de Microsoft"
description: "Usa Resource Manager y conjuntos de escalado de máquinas virtuales con varias reglas y perfiles que envían correo electrónico y llaman a direcciones URL de webhook con acciones de escalado."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 7e3576e2-4a2b-4736-b5ae-98c4689cdd2b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2016
ms.author: ancav
ms.openlocfilehash: ecb01e3094f715837b75ef07a7dbecdf0f2e78f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="9cef3-103">Configuración avanzada de escalado automático con plantillas de Resource Manager para conjuntos de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="9cef3-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="9cef3-104">Puede reducir y escalar horizontalmente los conjuntos de escalado de máquinas virtuales según umbrales de métricas de rendimiento, siguiendo una programación periódica o por una fecha determinada.</span><span class="sxs-lookup"><span data-stu-id="9cef3-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="9cef3-105">También puede configurar notificaciones de correo electrónico y webhook para las acciones de escalado.</span><span class="sxs-lookup"><span data-stu-id="9cef3-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="9cef3-106">Este tutorial muestra un ejemplo de configuración de todos estos objetos utilizando una plantilla de Resource Manager en un conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9cef3-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="9cef3-107">Mientras que en este tutorial se explica los pasos de Hola para conjuntos de escalas de VM, hello misma información aplica tooautoscaling [servicios en la nube](https://azure.microsoft.com/services/cloud-services/), y [servicio de aplicaciones: aplicaciones Web](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="9cef3-107">While this walkthrough explains hello steps for VM Scale Sets, hello same information applies tooautoscaling [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>
> <span data-ttu-id="9cef3-108">De una escala simple de entrada/salida de la configuración en un conjunto de escala de máquinas virtuales en función de una métrica de rendimiento simple como CPU, consulte toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) y [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documentos</span><span class="sxs-lookup"><span data-stu-id="9cef3-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="9cef3-109">Tutorial</span><span class="sxs-lookup"><span data-stu-id="9cef3-109">Walkthrough</span></span>
<span data-ttu-id="9cef3-110">En este tutorial, usaremos [Explorador de recursos de Azure](https://resources.azure.com/) tooconfigure y actualizar configuración de escalado automático de Hola para un conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="9cef3-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) tooconfigure and update hello autoscale setting for a scale set.</span></span> <span data-ttu-id="9cef3-111">Explorador de recursos de Azure es una manera sencilla de toomanage recursos de Azure a través de plantillas de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="9cef3-111">Azure Resource Explorer is an easy way toomanage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="9cef3-112">Si está la nueva herramienta de explorador de recursos de tooAzure, lea [esta introducción](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span><span class="sxs-lookup"><span data-stu-id="9cef3-112">If you are new tooAzure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="9cef3-113">Implemente un nuevo conjunto de escala con un valor de escalado automático básico.</span><span class="sxs-lookup"><span data-stu-id="9cef3-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="9cef3-114">En este artículo usa Hola de hello Galería de inicio rápido de Azure, que tiene una ventana de escala se establece con una plantilla básica de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="9cef3-114">This article uses hello one from hello Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="9cef3-115">Escala de Linux establece trabajo Hola igual.</span><span class="sxs-lookup"><span data-stu-id="9cef3-115">Linux scale sets work hello same way.</span></span>
2. <span data-ttu-id="9cef3-116">Una vez creado el conjunto de escalas de hello, navegar toohello recurso de conjunto de escala desde el Explorador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9cef3-116">After hello scale set is created, navigate toohello scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="9cef3-117">Ve a continuación hello en el nodo Microsoft.Insights.</span><span class="sxs-lookup"><span data-stu-id="9cef3-117">You see hello following under Microsoft.Insights node.</span></span>

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="9cef3-119">ejecución de la plantilla de Hello ha creado una configuración de escalado automático de forma predeterminada con el nombre de hello **'autoscalewad'**.</span><span class="sxs-lookup"><span data-stu-id="9cef3-119">hello template execution has created a default autoscale setting with hello name **'autoscalewad'**.</span></span> <span data-ttu-id="9cef3-120">En el lado derecho de hello, puede ver la definición completa de Hola de esta configuración de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="9cef3-120">On hello right-hand side, you can view hello full definition of this autoscale setting.</span></span> <span data-ttu-id="9cef3-121">En este caso, configuración de escalado automático de hello predeterminada incluye una regla de escalado horizontal y escalado en % en función de CPU.</span><span class="sxs-lookup"><span data-stu-id="9cef3-121">In this case, hello default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="9cef3-122">Ahora puede agregar más perfiles y reglas basadas en la programación de Hola o requisitos específicos.</span><span class="sxs-lookup"><span data-stu-id="9cef3-122">You can now add more profiles and rules based on hello schedule or specific requirements.</span></span> <span data-ttu-id="9cef3-123">Creamos una configuración de escalado automático con tres perfiles.</span><span class="sxs-lookup"><span data-stu-id="9cef3-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="9cef3-124">perfiles de toounderstand y reglas de escalado automático, revise [prácticas recomendadas de escalado automático](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="9cef3-124">toounderstand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="9cef3-125">Perfiles y reglas</span><span class="sxs-lookup"><span data-stu-id="9cef3-125">Profiles & Rules</span></span> | <span data-ttu-id="9cef3-126">Description</span><span class="sxs-lookup"><span data-stu-id="9cef3-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="9cef3-127">**Perfil**</span><span class="sxs-lookup"><span data-stu-id="9cef3-127">**Profile**</span></span> |<span data-ttu-id="9cef3-128">**Basado en rendimiento/métrica**</span><span class="sxs-lookup"><span data-stu-id="9cef3-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="9cef3-129">Regla</span><span class="sxs-lookup"><span data-stu-id="9cef3-129">Rule</span></span> |<span data-ttu-id="9cef3-130">Recuento de mensajes de cola de Bus de servicio > x</span><span class="sxs-lookup"><span data-stu-id="9cef3-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="9cef3-131">Regla</span><span class="sxs-lookup"><span data-stu-id="9cef3-131">Rule</span></span> |<span data-ttu-id="9cef3-132">Recuento de mensajes de cola de Bus de servicio > y</span><span class="sxs-lookup"><span data-stu-id="9cef3-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="9cef3-133">Regla</span><span class="sxs-lookup"><span data-stu-id="9cef3-133">Rule</span></span> |<span data-ttu-id="9cef3-134">CPU% > n</span><span class="sxs-lookup"><span data-stu-id="9cef3-134">CPU% > n</span></span> |
    | <span data-ttu-id="9cef3-135">Regla</span><span class="sxs-lookup"><span data-stu-id="9cef3-135">Rule</span></span> |<span data-ttu-id="9cef3-136">% de CPU < p</span><span class="sxs-lookup"><span data-stu-id="9cef3-136">CPU% < p</span></span> |
    | <span data-ttu-id="9cef3-137">**Perfil**</span><span class="sxs-lookup"><span data-stu-id="9cef3-137">**Profile**</span></span> |<span data-ttu-id="9cef3-138">**Horas de la mañana días de semana, (no hay reglas)**</span><span class="sxs-lookup"><span data-stu-id="9cef3-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="9cef3-139">**Perfil**</span><span class="sxs-lookup"><span data-stu-id="9cef3-139">**Profile**</span></span> |<span data-ttu-id="9cef3-140">**Día de lanzamiento de producto (no hay reglas)**</span><span class="sxs-lookup"><span data-stu-id="9cef3-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="9cef3-141">Este es un escenario hipotético de escalado que se utiliza para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9cef3-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="9cef3-142">**En función de carga** -me gustaría tooscale o según la carga de hello en mi aplicación hospedada en mi set.* de escala</span><span class="sxs-lookup"><span data-stu-id="9cef3-142">**Load based** - I'd like tooscale out or in based on hello load on my application hosted on my scale set.*</span></span>
    * <span data-ttu-id="9cef3-143">**Tamaño de la cola de mensajes** -usar una cola de Bus de servicio para la aplicación de toomy de mensajes entrantes de hello.</span><span class="sxs-lookup"><span data-stu-id="9cef3-143">**Message Queue size** - I use a Service Bus Queue for hello incoming messages toomy application.</span></span> <span data-ttu-id="9cef3-144">Uso de recuento de mensajes de la cola de Hola y % de CPU y configurar una tootrigger de perfil de manera predeterminada una acción de escalado si el número de mensajes o CPU aciertos Hola threshold.*</span><span class="sxs-lookup"><span data-stu-id="9cef3-144">I use hello queue's message count and CPU% and configure a default profile tootrigger a scale action if either of message count or CPU hits hello threshold.*</span></span>
    * <span data-ttu-id="9cef3-145">**Hora de la semana y día** -deseo un perfil de 'hora del día de hello' según repetición semanal denominado "Día de la semana de la mañana".</span><span class="sxs-lookup"><span data-stu-id="9cef3-145">**Time of week and day** - I want a weekly recurring 'time of hello day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="9cef3-146">En función de los datos históricos, saber es mejor toohave determinado número de VM instancias toohandle carga de la aplicación durante este time.*</span><span class="sxs-lookup"><span data-stu-id="9cef3-146">Based on historical data, I know it is better toohave certain number of VM instances toohandle my application's load during this time.*</span></span>
    * <span data-ttu-id="9cef3-147">**Fechas especiales**: agrego un perfil de "Día de lanzamiento de producto".</span><span class="sxs-lookup"><span data-stu-id="9cef3-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="9cef3-148">Planee con antelación para fechas específicas, por lo que mi aplicación es listo toohandle Hola carga debido a anuncios de marketing y cuando se coloque un nuevo producto en hello application.*</span><span class="sxs-lookup"><span data-stu-id="9cef3-148">I plan ahead for specific dates so my application is ready toohandle hello load due marketing announcements and when we put a new product in hello application.*</span></span>
    * <span data-ttu-id="9cef3-149">*últimos dos perfiles de Hello también pueden tener otras reglas según métrica de rendimiento dentro de ellos. En este caso, se decidió no toohave uno y en su lugar reglas basadas en toorely en la métrica de rendimiento de Hola de forma predeterminada. Las reglas son opcionales para los perfiles de repetición y basada en la fecha de Hola.*</span><span class="sxs-lookup"><span data-stu-id="9cef3-149">*hello last two profiles can also have other performance metric based rules within them. In this case, I decided not toohave one and instead toorely on hello default performance metric based rules. Rules are optional for hello recurring and date-based profiles.*</span></span>

    <span data-ttu-id="9cef3-150">Asignación de prioridades del motor de escalado automático de perfiles de Hola y reglas también se captura en hello [prácticas recomendadas de escalado automático](insights-autoscale-best-practices.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="9cef3-150">Autoscale engine's prioritization of hello profiles and rules is also captured in hello [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="9cef3-151">Para ver una lista de las métricas más comunes para el escalado automático, consulte [Métricas comunes de escalado automático](insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="9cef3-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="9cef3-152">Asegúrese de que se encuentra en hello **lectura/escritura** modo en el Explorador de recursos</span><span class="sxs-lookup"><span data-stu-id="9cef3-152">Make sure you are on hello **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, valor de escalado automático predeterminado](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="9cef3-154">Haga clic en Editar.</span><span class="sxs-lookup"><span data-stu-id="9cef3-154">Click Edit.</span></span> <span data-ttu-id="9cef3-155">**Reemplace** elemento perfiles' hello' en la configuración de escalado automático con hello siguiente configuración:</span><span class="sxs-lookup"><span data-stu-id="9cef3-155">**Replace** hello 'profiles' element in autoscale setting with hello following configuration:</span></span>

    ![perfiles](./media/insights-advanced-autoscale-vmss/profiles.png)

    ```
    {
            "name": "Perf_Based_Scale",
            "capacity": {
              "minimum": "2",
              "maximum": "12",
              "default": "2"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 10
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 3
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 85
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          },
          {
            "name": "Weekday_Morning_Hours_Scale",
            "capacity": {
              "minimum": "4",
              "maximum": "12",
              "default": "4"
            },
            "rules": [],
            "recurrence": {
              "frequency": "Week",
              "schedule": {
                "timeZone": "Pacific Standard Time",
                "days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
                ],
                "hours": [
                  6
                ],
                "minutes": [
                  0
                ]
              }
            }
          },
          {
            "name": "Product_Launch_Day",
            "capacity": {
              "minimum": "6",
              "maximum": "20",
              "default": "6"
            },
            "rules": [],
            "fixedDate": {
              "timeZone": "Pacific Standard Time",
              "start": "2016-06-20T00:06:00Z",
              "end": "2016-06-21T23:59:00Z"
            }
          }
    ```
    <span data-ttu-id="9cef3-157">Para los campos compatibles y sus valores, consulte la [documentación de la API de REST de escalado automático](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="9cef3-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="9cef3-158">Ahora la configuración de escalado automático contiene tres perfiles de Hola se ha explicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9cef3-158">Now your autoscale setting contains hello three profiles explained previously.</span></span>

7. <span data-ttu-id="9cef3-159">Por último, mire Hola escalado automático **notificación** sección.</span><span class="sxs-lookup"><span data-stu-id="9cef3-159">Finally, look at hello Autoscale **notification** section.</span></span> <span data-ttu-id="9cef3-160">Notificaciones de escalado automático le permiten toodo tres cosas cuando una implementación escalada o de acción se activó correctamente.</span><span class="sxs-lookup"><span data-stu-id="9cef3-160">Autoscale notifications allow you toodo three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="9cef3-161">Notifique a Hola, administrador y coadministradores de su suscripción</span><span class="sxs-lookup"><span data-stu-id="9cef3-161">Notify hello admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="9cef3-162">Enviar un correo electrónico a un conjunto de usuarios</span><span class="sxs-lookup"><span data-stu-id="9cef3-162">Email a set of users</span></span>
   - <span data-ttu-id="9cef3-163">Desencadenar una llamada de webhook.</span><span class="sxs-lookup"><span data-stu-id="9cef3-163">Trigger a webhook call.</span></span> <span data-ttu-id="9cef3-164">Cuando se desencadene, este webhook envía metadatos acerca de la condición de escalado automático de Hola y conjunto de escalado de Hola de recursos.</span><span class="sxs-lookup"><span data-stu-id="9cef3-164">When fired, this webhook sends metadata about hello autoscaling condition and hello scale set resource.</span></span> <span data-ttu-id="9cef3-165">toolearn más información acerca de la carga de Hola de webhook de escalado automático, consulte [Webhook configurar & notificaciones por correo electrónico para el escalado automático](insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="9cef3-165">toolearn more about hello payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="9cef3-166">Agregar Hola después de reemplazar configuración de escalado automático de toohello el **notificación** elemento cuyo valor es null</span><span class="sxs-lookup"><span data-stu-id="9cef3-166">Add hello following toohello Autoscale setting replacing your **notification** element whose value is null</span></span>

   ```
   "notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": true,
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

   <span data-ttu-id="9cef3-167">Aciertos **colocar** botón Explorador de recursos tooupdate Hola configuración de escalado automático.</span><span class="sxs-lookup"><span data-stu-id="9cef3-167">Hit **Put** button in Resource Explorer tooupdate hello autoscale setting.</span></span>

<span data-ttu-id="9cef3-168">Se ha actualizado una configuración en un tooinclude de conjunto de escalas de VM varios perfiles de escala de escalado automático y escalar las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="9cef3-168">You have updated an autoscale setting on a VM Scale set tooinclude multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cef3-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9cef3-169">Next Steps</span></span>
<span data-ttu-id="9cef3-170">Use estos toolearn de vínculos más información acerca de la escala automática.</span><span class="sxs-lookup"><span data-stu-id="9cef3-170">Use these links toolearn more about autoscaling.</span></span>

[<span data-ttu-id="9cef3-171">Solución de problemas de escalado automático de conjuntos de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="9cef3-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="9cef3-172">Métricas comunes de escalado automático</span><span class="sxs-lookup"><span data-stu-id="9cef3-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="9cef3-173">Procedimientos recomendados de escalado automático</span><span class="sxs-lookup"><span data-stu-id="9cef3-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="9cef3-174">Administración del escalado automático con PowerShell</span><span class="sxs-lookup"><span data-stu-id="9cef3-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="9cef3-175">Administración del escalado automático con CLI</span><span class="sxs-lookup"><span data-stu-id="9cef3-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="9cef3-176">Configuración de webhooks y notificaciones por correo electrónico en el escalado automático</span><span class="sxs-lookup"><span data-stu-id="9cef3-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)
