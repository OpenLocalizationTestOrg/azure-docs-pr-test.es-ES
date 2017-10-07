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
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a>Usar el escalado automático acciones toosend correo electrónico y webhook notificaciones de alerta en el Monitor de Azure
En este artículo se muestra cómo configurar desencadenadores para que pueda llamar a direcciones URL web específicas o enviar mensajes de correo electrónico en función de las acciones de escalado automático en Azure.  

## <a name="webhooks"></a>Webhooks
Webhooks le permiten sistemas de tooother de tooroute hello Azure notificaciones de alerta para las notificaciones personalizadas o posteriores al procesamiento. Por ejemplo, enrutamiento tooservices alerta Hola que pueda controlar una entrada web solicitud toosend SMS, errores de registro, notifique a un equipo mediante chat o servicios de mensajería, etc. hello webhook URI debe ser un punto de conexión HTTP o HTTPS válida.

## <a name="email"></a>Email
Correo electrónico puede enviarse tooany dirección de correo electrónico válida. También se notificará a los administradores y coadministradores de suscripción de Hola donde se ejecuta la regla de Hola.

## <a name="cloud-services-and-web-apps"></a>Aplicaciones web y servicios en la nube
Puede participar en de hello portal de Azure para los servicios de nube y granjas de servidores (aplicaciones Web).

* Elija hello **escalar** métrica.

![Escalar por](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a>Conjuntos de escalado de máquina virtual
Para las máquinas virtuales más recientes creadas con Resource Manager (conjuntos de escala de máquina virtual), puede configurar esto con la API de REST, las plantillas de Resource Manager, PowerShell y CLI. Aún no se encuentra disponible una interfaz de portal.
Cuando se utiliza la API de REST de Hola o plantilla de administrador de recursos, incluya el elemento de las notificaciones de hello con hello siguientes opciones.

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
| Campo | ¿Obligatorio? | Description |
| --- | --- | --- |
| operación |yes |el valor debe ser "Scale" |
| sendToSubscriptionAdministrator |yes |el valor debe ser "true" o "false" |
| sendToSubscriptionCoAdministrators |yes |el valor debe ser "true" o "false" |
| customEmails |yes |el valor puede ser null [] o una cadena de matriz de mensajes de correo electrónico |
| Webhooks |yes |el valor puede ser null o un identificador URI válido |
| serviceUri |yes |un identificador URI de https válido |
| propiedades |yes |el valor debe ser {} vacío o puede contener pares de clave y valor |

## <a name="authentication-in-webhooks"></a>Autenticación en Webhook
Hola webhook puede autenticar utilizando autenticación basada en el símbolo (token), en la que guardar hello webhook URI con un identificador de símbolo (token) como un parámetro de consulta. Por ejemplo, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue

## <a name="autoscale-notification-webhook-payload-schema"></a>Esquema de carga de Webhook de notificación de escalado automático
Cuando se genera la notificación de escalado automático de hello, hello metadatos siguientes se incluyen en la carga de webhook de hello:

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


| Campo | ¿Obligatorio? | Description |
| --- | --- | --- |
| status |yes |estado de Hola que indica que se ha generado una acción de escalado automático |
| operación |yes |Para un aumento de instancias, será "Escalar horizontalmente"; para una disminución de instancias, "Reducir horizontalmente". |
| contexto |yes |contexto de acción de escalado automático de Hola |
| timestamp |yes |Marca de tiempo cuando se activó la acción de escalado automático de Hola |
| id |Sí |Id. de administrador de recursos de configuración de escalado automático de Hola |
| name |Sí |nombre de Hola de configuración de escalado automático de Hola |
| details |Sí |Explicación de la acción de Hola que tardó el servicio de escalado automático de Hola y Hola cambio en el número de instancias de Hola |
| subscriptionId |Sí |Id. de suscripción de recurso de destino de Hola que se ajusta la escala |
| resourceGroupName |Sí |Nombre de grupo de recursos del recurso de destino de Hola que se ajusta la escala |
| resourceName |Sí |Nombre del recurso de destino de Hola que se ajusta la escala |
| resourceType |Sí |Hola tres valores admitidos: "microsoft.classiccompute/domainnames/slots/roles" - roles, "microsoft.compute/virtualmachinescalesets" - conjuntos de escalas de máquina Virtual y "Microsoft.Web/serverfarms -" aplicación Web de servicio en la nube |
| resourceId |Sí |Id. de administrador de recursos del recurso de destino de Hola que se ajusta la escala |
| portalLink |Sí |Página de resumen de toohello de enlace del portal Azure de recurso de destino de Hola |
| oldCapacity |Sí |Hola (antiguo) recuento de instancias actual cuando el escalado automático ha realizado una acción de escala |
| newCapacity |Sí |recuento de instancias nuevas de Hola que escalado automático escala recursos Hola demasiado|
| Propiedades |No |Opcional. Conjunto de pares <Clave, Valor> (por ejemplo, Diccionario <Cadena, Cadena>). campo de propiedades de Hello es opcional. En una interfaz de usuario personalizada o un flujo de trabajo de aplicación en función de lógica, puede escribir las claves y valores que se pueden pasar mediante la carga de Hola. Una forma alternativa de propiedades personalizadas de toopass hacer copia de llamada de webhook salida toohello es toouse hello webhook URI (como parámetros de consulta) |
