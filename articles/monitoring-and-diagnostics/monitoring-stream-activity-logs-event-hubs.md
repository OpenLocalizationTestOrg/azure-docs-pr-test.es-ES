---
title: aaaStream hello Azure Activity Log tooEvent concentradores | Documentos de Microsoft
description: "Obtenga información acerca de cómo toostream Hola tooEvent centros de registro de actividad de Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 336f92771b9d4379ad9dbcadc6997dfae7fae7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a>Transmitir hello Azure Activity Log tooEvent centros
Hola [ **Azure Activity Log** ](monitoring-overview-activity-logs.md) se puede transmitir casi en tiempo real tooany aplicación con opción de "Exportación" de hello integrada en el portal de Hola o habilitando Hola Id. de regla de Bus de servicio en un perfil de registro a través de Hola Cmdlets de PowerShell de Azure o Azure CLI.

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a>¿Qué puede hacer con el registro de actividad de Hola y concentradores de eventos
Aquí se muestran unos pocos maneras puede usar Hola capacidad para hello registro de actividad de streaming:

* **Transmitir los sistemas de registro y telemetría de toothird terceros** – con el tiempo, los concentradores de eventos de transmisión por secuencias se convertirá en hello mecanismo toopipe el registro de actividad en terceros SIEM y soluciones de análisis de registro.
* **Crear una plataforma de registro y telemetría personalizada** : si ya tiene una plataforma de telemetría personalizada o son solo pensar en uno, Hola altamente escalable publicación / suscripción de edificio naturaleza de los centros de eventos permite tooflexibly introducir Hola registro de actividades. [Consulte toousing de guía de Dan Rosanova centros de eventos en una plataforma de telemetría de escala global.](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a>Habilite el streaming de hello registro de actividad
Puede habilitar la transmisión por secuencias de registro de actividad de hello mediante programación o a través del portal de Hola. En cualquier caso, se elige un Namespace de Bus de servicio y una directiva de acceso compartido para ese espacio de nombres y un concentrador de eventos se crea en ese espacio de nombres cuando se produce el primer evento nuevo registro de actividad Hola. Si no tiene un Namespace de Bus de servicio, primero debe toocreate uno. Si anteriormente se transmitido por secuencias de eventos de registro de actividad toothis Namespace de Bus de servicio, se reutilizarán Hola concentrador de eventos que se creó anteriormente. Directiva de acceso compartido de Hello define los permisos de Hola que tiene el mecanismo de transmisión por secuencias de Hola. En la actualidad, streaming centros de eventos de tooan requiere **administrar**, **enviar**, y **escuchar** permisos. Puede crear o modificar las directivas de acceso de Namespace de Bus de servicio compartido en el portal clásico de hello en la ficha de "Configurar" hello para el Namespace de Bus de servicio. tooupdate Hola tooinclude streaming de perfil de registro de registro de actividad, usuario de Hola que realiza el cambio de hello debe tener permiso de ListKey de hello en esa regla de autorización de Bus de servicio.

Hello espacio de nombres de concentrador de eventos o de bus de servicio no tiene toobe en hello misma suscripción que Hola emitir registros como usuario de Hola que configura los valores de hello tiene suscripciones de tooboth de acceso RBAC adecuadas.

### <a name="via-azure-portal"></a>Mediante el Portal de Azure
1. Navegue toohello **registro de actividad** hoja con menú de hello en hello izquierda del portal de Hola.
   
    ![Navegue tooActivity registro en el portal](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Haga clic en hello **exportar** situado en la parte superior de Hola de hoja de Hola.
   
    ![Botón Exportar en el portal](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. En la hoja de Hola que aparece, puede seleccionar las regiones de hello para el que desea eventos toostream y Namespace de Bus de servicio de hello en el que desea una toobe de concentrador de eventos creado para la transmisión por secuencias estos eventos.
   
    ![Exportar en hoja de registro de actividad](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. Haga clic en **guardar** toosave esta configuración. configuración de Hello inmediatamente se pueden suscripción tooyour aplicada.

### <a name="via-powershell-cmdlets"></a>Mediante cmdlets de PowerShell
Si ya existe un perfil de registro, primero debe tooremove dicho perfil.

1. Use `Get-AzureRmLogProfile` tooidentify si existe un perfil de registro
2. Si es así, utilice `Remove-AzureRmLogProfile` tooremove lo.
3. Use `Set-AzureRmLogProfile` toocreate un perfil:

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

Hola Id. de regla de Bus de servicio es una cadena con este formato: {Id. de recurso de bus de servicio} /authorizationrules/ {nombre de clave}, por ejemplo 

### <a name="via-azure-cli"></a>Mediante la CLI de Azure
Si ya existe un perfil de registro, primero debe tooremove dicho perfil.

1. Use `azure insights logprofile list` tooidentify si existe un perfil de registro
2. Si es así, utilice `azure insights logprofile delete` tooremove lo.
3. Use `azure insights logprofile add` toocreate un perfil:

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

Hola Id. de regla de Bus de servicio es una cadena con este formato: `{service bus resource ID}/authorizationrules/{key name}`.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>¿Cómo se puede consumir datos de registro de hello de centros de eventos?
[esquema de Hello para el registro de actividad de Hola está disponible aquí](monitoring-overview-activity-logs.md). Cada evento está en una matriz de blobs JSON denominados "registros".

## <a name="next-steps"></a>Pasos siguientes
* [Hola archivo cuenta de almacenamiento tooa de registro de actividad](monitoring-archive-activity-log.md)
* [Información general de Hola de lectura de hello Azure Activity Log](monitoring-overview-activity-logs.md)
* [Configure una alerta basada en un evento del registro de actividades](insights-auditlog-to-webhook-email.md)

