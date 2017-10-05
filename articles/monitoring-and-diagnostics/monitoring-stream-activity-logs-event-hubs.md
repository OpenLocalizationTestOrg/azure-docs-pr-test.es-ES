---
title: "Transmisión del registro de actividades de Azure a Events Hubs | Microsoft Docs"
description: Aprenda a transmitir el registro de actividad de Azure a centros de eventos.
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
ms.openlocfilehash: 88c5701279f370914fac68872d67b02a7571748a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="stream-the-azure-activity-log-to-event-hubs"></a><span data-ttu-id="e0893-103">Transmisión del registro de actividad de Azure a centros de eventos</span><span class="sxs-lookup"><span data-stu-id="e0893-103">Stream the Azure Activity Log to Event Hubs</span></span>
<span data-ttu-id="e0893-104">El [**registro de actividades de Azure**](monitoring-overview-activity-logs.md) se puede transmitir casi en tiempo real a cualquier aplicación mediante la opción Exportar integrada en el portal o habilitando el identificador de regla de Bus Services en un perfil de registro por medio de los cmdlets de Azure PowerShell o la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="e0893-104">The [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time to any application using the built-in “Export” option in the portal, or by enabling the Service Bus Rule Id in a Log Profile via the Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-the-activity-log-and-event-hubs"></a><span data-ttu-id="e0893-105">Qué se puede hacer con el registro de actividad y los centros de eventos</span><span class="sxs-lookup"><span data-stu-id="e0893-105">What you can do with the Activity Log and Event Hubs</span></span>
<span data-ttu-id="e0893-106">Estas son solo algunas formas de usar la funcionalidad de streaming para el registro de actividad:</span><span class="sxs-lookup"><span data-stu-id="e0893-106">Here are just a few ways you might use the streaming capability for the Activity Log:</span></span>

* <span data-ttu-id="e0893-107">**Transmisión a sistemas de registro y telemetría de terceros** : con el tiempo, el streaming de centros de eventos se convertirá en el mecanismo para canalizar el registro de actividad a sistemas de información de seguridad y administración de eventos (SIEM) y soluciones de análisis de registro de terceros.</span><span class="sxs-lookup"><span data-stu-id="e0893-107">**Stream to third-party logging and telemetry systems** – Over time, Event Hubs streaming will become the mechanism to pipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="e0893-108">**Creación de una plataforma personalizada de registro y telemetría** : si ya tiene una plataforma de telemetría personalizada o está pensando en crear una, la gran escalabilidad en cuanto a la suscripción y la publicación de los centros de eventos permite introducir el registro de actividad de manera flexible.</span><span class="sxs-lookup"><span data-stu-id="e0893-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, the highly scalable publish-subscribe nature of Event Hubs allows you to flexibly ingest the activity log.</span></span> [<span data-ttu-id="e0893-109">Consulte la guía de Dan Rosanova para usar centros de eventos en una plataforma de telemetría de escala global aquí.</span><span class="sxs-lookup"><span data-stu-id="e0893-109">See Dan Rosanova’s guide to using Event Hubs in a global scale telemetry platform here.</span></span>](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-the-activity-log"></a><span data-ttu-id="e0893-110">Habilitación del streaming del registro de actividad</span><span class="sxs-lookup"><span data-stu-id="e0893-110">Enable streaming of the Activity Log</span></span>
<span data-ttu-id="e0893-111">Puede habilitar el streaming del registro de actividad mediante programación o a través del portal.</span><span class="sxs-lookup"><span data-stu-id="e0893-111">You can enable streaming of the Activity Log either programmatically or via the portal.</span></span> <span data-ttu-id="e0893-112">En cualquier caso, puede seleccionar un espacio de nombres de Service Bus y una directiva de acceso compartido para dicho espacio de nombres. Además, se crea un Centro de eventos en ese espacio de nombres cuando se produce el primer nuevo evento del registro de actividades.</span><span class="sxs-lookup"><span data-stu-id="e0893-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when the first new Activity Log event occurs.</span></span> <span data-ttu-id="e0893-113">Si no tiene un espacio de nombres de Service Bus, primero debe crear uno.</span><span class="sxs-lookup"><span data-stu-id="e0893-113">If you do not have a Service Bus Namespace, you first need to create one.</span></span> <span data-ttu-id="e0893-114">Si anteriormente se han transmitido eventos del registro de actividades para este espacio de nombres de Service Bus, se reutilizará el Centro de eventos que se creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e0893-114">If you have previously streamed Activity Log events to this Service Bus Namespace, the Event Hub that was previously created will be reused.</span></span> <span data-ttu-id="e0893-115">La directiva de acceso compartido define los permisos que tiene el mecanismo de transmisión.</span><span class="sxs-lookup"><span data-stu-id="e0893-115">The shared access policy defines the permissions that the streaming mechanism has.</span></span> <span data-ttu-id="e0893-116">En la actualidad, para transmitir a un centro de Event Hubs, se necesitan permisos de **administración**, **envío** y **escucha**.</span><span class="sxs-lookup"><span data-stu-id="e0893-116">Today, streaming to an Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="e0893-117">Puede crear o modificar las directivas de acceso compartido del espacio de nombres del Bus de servicio en el Portal clásico en la pestaña "Configurar" para el espacio de nombres del Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="e0893-117">You can create or modify Service Bus Namespace shared access policies in the classic portal under the “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="e0893-118">Para actualizar el perfil de registro del registro de actividad para incluir la transmisión, el cliente debe tener el permiso ListKey en la regla de autorización de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="e0893-118">To update the Activity Log log profile to include streaming, the user making the change must have the ListKey permission on that Service Bus Authorization Rule.</span></span>

<span data-ttu-id="e0893-119">El espacio de nombres del centro de eventos o el bus de servicio no tiene que estar en la misma suscripción que la que emite los registros, siempre que el usuario que configura la configuración tenga acceso RBAC adecuado a ambas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="e0893-119">The service bus or event hub namespace does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="e0893-120">Mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e0893-120">Via Azure portal</span></span>
1. <span data-ttu-id="e0893-121">Vaya a la hoja de **registro de actividad** mediante el menú en el lado izquierdo del portal.</span><span class="sxs-lookup"><span data-stu-id="e0893-121">Navigate to the **Activity Log** blade using the menu on the left side of the portal.</span></span>
   
    ![Ir al registro de actividad en el portal](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="e0893-123">Haga clic en el botón **Exportar** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="e0893-123">Click the **Export** button at the top of the blade.</span></span>
   
    ![Botón Exportar en el portal](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="e0893-125">En la hoja que aparece, puede seleccionar las regiones para las que transmitir eventos y el espacio de nombres del Bus de servicio donde desea que se cree un centro de eventos para transmitirlos.</span><span class="sxs-lookup"><span data-stu-id="e0893-125">In the blade that appears, you can select the regions for which you would like to stream events and the Service Bus Namespace in which you would like an Event Hub to be created for streaming these events.</span></span>
   
    ![Exportar en hoja de registro de actividad](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="e0893-127">Haga clic en **Guardar** para guardar la configuración.</span><span class="sxs-lookup"><span data-stu-id="e0893-127">Click **Save** to save these settings.</span></span> <span data-ttu-id="e0893-128">La configuración se aplica inmediatamente a la suscripción.</span><span class="sxs-lookup"><span data-stu-id="e0893-128">The settings are immediately be applied to your subscription.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="e0893-129">Mediante cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0893-129">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="e0893-130">Si ya existe un perfil de registro, primero debe quitarlo.</span><span class="sxs-lookup"><span data-stu-id="e0893-130">If a log profile already exists, you first need to remove that profile.</span></span>

1. <span data-ttu-id="e0893-131">Use `Get-AzureRmLogProfile` para identificar si existe un perfil de registro.</span><span class="sxs-lookup"><span data-stu-id="e0893-131">Use `Get-AzureRmLogProfile` to identify if a log profile exists</span></span>
2. <span data-ttu-id="e0893-132">Si es así, use `Remove-AzureRmLogProfile` para quitarlo.</span><span class="sxs-lookup"><span data-stu-id="e0893-132">If so, use `Remove-AzureRmLogProfile` to remove it.</span></span>
3. <span data-ttu-id="e0893-133">Use `Set-AzureRmLogProfile` para crear un perfil:</span><span class="sxs-lookup"><span data-stu-id="e0893-133">Use `Set-AzureRmLogProfile` to create a profile:</span></span>

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

<span data-ttu-id="e0893-134">El identificador de regla del Bus de servicio es una cadena con este formato: por ejemplo, {Id. de recurso del Bus de servicio}/authorizationrules/{nombre de clave}.</span><span class="sxs-lookup"><span data-stu-id="e0893-134">The Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span></span> 

### <a name="via-azure-cli"></a><span data-ttu-id="e0893-135">Mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e0893-135">Via Azure CLI</span></span>
<span data-ttu-id="e0893-136">Si ya existe un perfil de registro, primero debe quitarlo.</span><span class="sxs-lookup"><span data-stu-id="e0893-136">If a log profile already exists, you first need to remove that profile.</span></span>

1. <span data-ttu-id="e0893-137">Use `azure insights logprofile list` para identificar si existe un perfil de registro.</span><span class="sxs-lookup"><span data-stu-id="e0893-137">Use `azure insights logprofile list` to identify if a log profile exists</span></span>
2. <span data-ttu-id="e0893-138">Si es así, use `azure insights logprofile delete` para quitarlo.</span><span class="sxs-lookup"><span data-stu-id="e0893-138">If so, use `azure insights logprofile delete` to remove it.</span></span>
3. <span data-ttu-id="e0893-139">Use `azure insights logprofile add` para crear un perfil:</span><span class="sxs-lookup"><span data-stu-id="e0893-139">Use `azure insights logprofile add` to create a profile:</span></span>

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

<span data-ttu-id="e0893-140">El identificador de regla del Bus de servicio es una cadena con este formato: `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="e0893-140">The Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

## <a name="how-do-i-consume-the-log-data-from-event-hubs"></a><span data-ttu-id="e0893-141">¿Cómo se consumen los datos de registro procedentes de centros de eventos?</span><span class="sxs-lookup"><span data-stu-id="e0893-141">How do I consume the log data from Event Hubs?</span></span>
<span data-ttu-id="e0893-142">[El esquema para el registro de actividades está disponible aquí](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="e0893-142">[The schema for the Activity Log is available here](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="e0893-143">Cada evento está en una matriz de blobs JSON denominados "registros".</span><span class="sxs-lookup"><span data-stu-id="e0893-143">Each event is in an array of JSON blobs called “records.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0893-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e0893-144">Next Steps</span></span>
* [<span data-ttu-id="e0893-145">(Archivado del registro de actividades en una cuenta de almacenamiento)</span><span class="sxs-lookup"><span data-stu-id="e0893-145">Archive the Activity Log to a storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="e0893-146">Lea la información general sobre el registro de actividades de Azure</span><span class="sxs-lookup"><span data-stu-id="e0893-146">Read the overview of the Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="e0893-147">Configure una alerta basada en un evento del registro de actividades</span><span class="sxs-lookup"><span data-stu-id="e0893-147">Set up an alert based on an Activity Log event</span></span>](insights-auditlog-to-webhook-email.md)

