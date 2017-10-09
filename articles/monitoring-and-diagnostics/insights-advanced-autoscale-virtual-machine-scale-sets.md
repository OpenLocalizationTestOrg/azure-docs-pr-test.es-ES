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
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a>Configuración avanzada de escalado automático con plantillas de Resource Manager para conjuntos de escalado de máquinas virtuales
Puede reducir y escalar horizontalmente los conjuntos de escalado de máquinas virtuales según umbrales de métricas de rendimiento, siguiendo una programación periódica o por una fecha determinada. También puede configurar notificaciones de correo electrónico y webhook para las acciones de escalado. Este tutorial muestra un ejemplo de configuración de todos estos objetos utilizando una plantilla de Resource Manager en un conjunto de escalado de máquinas virtuales.

> [!NOTE]
> Mientras que en este tutorial se explica los pasos de Hola para conjuntos de escalas de VM, hello misma información aplica tooautoscaling [servicios en la nube](https://azure.microsoft.com/services/cloud-services/), y [servicio de aplicaciones: aplicaciones Web](https://azure.microsoft.com/services/app-service/web/).
> De una escala simple de entrada/salida de la configuración en un conjunto de escala de máquinas virtuales en función de una métrica de rendimiento simple como CPU, consulte toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) y [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documentos
>
>

## <a name="walkthrough"></a>Tutorial
En este tutorial, usaremos [Explorador de recursos de Azure](https://resources.azure.com/) tooconfigure y actualizar configuración de escalado automático de Hola para un conjunto de escala. Explorador de recursos de Azure es una manera sencilla de toomanage recursos de Azure a través de plantillas de administrador de recursos. Si está la nueva herramienta de explorador de recursos de tooAzure, lea [esta introducción](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).

1. Implemente un nuevo conjunto de escala con un valor de escalado automático básico. En este artículo usa Hola de hello Galería de inicio rápido de Azure, que tiene una ventana de escala se establece con una plantilla básica de escalado automático. Escala de Linux establece trabajo Hola igual.
2. Una vez creado el conjunto de escalas de hello, navegar toohello recurso de conjunto de escala desde el Explorador de recursos de Azure. Ve a continuación hello en el nodo Microsoft.Insights.

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    ejecución de la plantilla de Hello ha creado una configuración de escalado automático de forma predeterminada con el nombre de hello **'autoscalewad'**. En el lado derecho de hello, puede ver la definición completa de Hola de esta configuración de escalado automático. En este caso, configuración de escalado automático de hello predeterminada incluye una regla de escalado horizontal y escalado en % en función de CPU.  

3. Ahora puede agregar más perfiles y reglas basadas en la programación de Hola o requisitos específicos. Creamos una configuración de escalado automático con tres perfiles. perfiles de toounderstand y reglas de escalado automático, revise [prácticas recomendadas de escalado automático](insights-autoscale-best-practices.md).  

    | Perfiles y reglas | Description |
    |--- | --- |
    | **Perfil** |**Basado en rendimiento/métrica** |
    | Regla |Recuento de mensajes de cola de Bus de servicio > x |
    | Regla |Recuento de mensajes de cola de Bus de servicio > y |
    | Regla |CPU% > n |
    | Regla |% de CPU < p |
    | **Perfil** |**Horas de la mañana días de semana, (no hay reglas)** |
    | **Perfil** |**Día de lanzamiento de producto (no hay reglas)** |

4. Este es un escenario hipotético de escalado que se utiliza para este tutorial.

    * **En función de carga** -me gustaría tooscale o según la carga de hello en mi aplicación hospedada en mi set.* de escala
    * **Tamaño de la cola de mensajes** -usar una cola de Bus de servicio para la aplicación de toomy de mensajes entrantes de hello. Uso de recuento de mensajes de la cola de Hola y % de CPU y configurar una tootrigger de perfil de manera predeterminada una acción de escalado si el número de mensajes o CPU aciertos Hola threshold.*
    * **Hora de la semana y día** -deseo un perfil de 'hora del día de hello' según repetición semanal denominado "Día de la semana de la mañana". En función de los datos históricos, saber es mejor toohave determinado número de VM instancias toohandle carga de la aplicación durante este time.*
    * **Fechas especiales**: agrego un perfil de "Día de lanzamiento de producto". Planee con antelación para fechas específicas, por lo que mi aplicación es listo toohandle Hola carga debido a anuncios de marketing y cuando se coloque un nuevo producto en hello application.*
    * *últimos dos perfiles de Hello también pueden tener otras reglas según métrica de rendimiento dentro de ellos. En este caso, se decidió no toohave uno y en su lugar reglas basadas en toorely en la métrica de rendimiento de Hola de forma predeterminada. Las reglas son opcionales para los perfiles de repetición y basada en la fecha de Hola.*

    Asignación de prioridades del motor de escalado automático de perfiles de Hola y reglas también se captura en hello [prácticas recomendadas de escalado automático](insights-autoscale-best-practices.md) artículo.
    Para ver una lista de las métricas más comunes para el escalado automático, consulte [Métricas comunes de escalado automático](insights-autoscale-common-metrics.md).

5. Asegúrese de que se encuentra en hello **lectura/escritura** modo en el Explorador de recursos

    ![Autoscalewad, valor de escalado automático predeterminado](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. Haga clic en Editar. **Reemplace** elemento perfiles' hello' en la configuración de escalado automático con hello siguiente configuración:

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
    Para los campos compatibles y sus valores, consulte la [documentación de la API de REST de escalado automático](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx). Ahora la configuración de escalado automático contiene tres perfiles de Hola se ha explicado anteriormente.

7. Por último, mire Hola escalado automático **notificación** sección. Notificaciones de escalado automático le permiten toodo tres cosas cuando una implementación escalada o de acción se activó correctamente.
   - Notifique a Hola, administrador y coadministradores de su suscripción
   - Enviar un correo electrónico a un conjunto de usuarios
   - Desencadenar una llamada de webhook. Cuando se desencadene, este webhook envía metadatos acerca de la condición de escalado automático de Hola y conjunto de escalado de Hola de recursos. toolearn más información acerca de la carga de Hola de webhook de escalado automático, consulte [Webhook configurar & notificaciones por correo electrónico para el escalado automático](insights-autoscale-to-webhook-email.md).

   Agregar Hola después de reemplazar configuración de escalado automático de toohello el **notificación** elemento cuyo valor es null

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

   Aciertos **colocar** botón Explorador de recursos tooupdate Hola configuración de escalado automático.

Se ha actualizado una configuración en un tooinclude de conjunto de escalas de VM varios perfiles de escala de escalado automático y escalar las notificaciones.

## <a name="next-steps"></a>Pasos siguientes
Use estos toolearn de vínculos más información acerca de la escala automática.

[Solución de problemas de escalado automático de conjuntos de escalado de máquinas virtuales](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[Métricas comunes de escalado automático](insights-autoscale-common-metrics.md)

[Procedimientos recomendados de escalado automático](insights-autoscale-best-practices.md)

[Administración del escalado automático con PowerShell](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[Administración del escalado automático con CLI](insights-cli-samples.md#autoscale)

[Configuración de webhooks y notificaciones por correo electrónico en el escalado automático](insights-autoscale-to-webhook-email.md)
