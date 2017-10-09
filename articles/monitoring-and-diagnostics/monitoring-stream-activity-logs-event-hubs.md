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
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a><span data-ttu-id="1b3a6-103">Transmitir hello Azure Activity Log tooEvent centros</span><span class="sxs-lookup"><span data-stu-id="1b3a6-103">Stream hello Azure Activity Log tooEvent Hubs</span></span>
<span data-ttu-id="1b3a6-104">Hola [ **Azure Activity Log** ](monitoring-overview-activity-logs.md) se puede transmitir casi en tiempo real tooany aplicación con opción de "Exportación" de hello integrada en el portal de Hola o habilitando Hola Id. de regla de Bus de servicio en un perfil de registro a través de Hola Cmdlets de PowerShell de Azure o Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-104">hello [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time tooany application using hello built-in “Export” option in hello portal, or by enabling hello Service Bus Rule Id in a Log Profile via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a><span data-ttu-id="1b3a6-105">¿Qué puede hacer con el registro de actividad de Hola y concentradores de eventos</span><span class="sxs-lookup"><span data-stu-id="1b3a6-105">What you can do with hello Activity Log and Event Hubs</span></span>
<span data-ttu-id="1b3a6-106">Aquí se muestran unos pocos maneras puede usar Hola capacidad para hello registro de actividad de streaming:</span><span class="sxs-lookup"><span data-stu-id="1b3a6-106">Here are just a few ways you might use hello streaming capability for hello Activity Log:</span></span>

* <span data-ttu-id="1b3a6-107">**Transmitir los sistemas de registro y telemetría de toothird terceros** – con el tiempo, los concentradores de eventos de transmisión por secuencias se convertirá en hello mecanismo toopipe el registro de actividad en terceros SIEM y soluciones de análisis de registro.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-107">**Stream toothird-party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="1b3a6-108">**Crear una plataforma de registro y telemetría personalizada** : si ya tiene una plataforma de telemetría personalizada o son solo pensar en uno, Hola altamente escalable publicación / suscripción de edificio naturaleza de los centros de eventos permite tooflexibly introducir Hola registro de actividades.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest hello activity log.</span></span> [<span data-ttu-id="1b3a6-109">Consulte toousing de guía de Dan Rosanova centros de eventos en una plataforma de telemetría de escala global.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-109">See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here.</span></span>](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a><span data-ttu-id="1b3a6-110">Habilite el streaming de hello registro de actividad</span><span class="sxs-lookup"><span data-stu-id="1b3a6-110">Enable streaming of hello Activity Log</span></span>
<span data-ttu-id="1b3a6-111">Puede habilitar la transmisión por secuencias de registro de actividad de hello mediante programación o a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-111">You can enable streaming of hello Activity Log either programmatically or via hello portal.</span></span> <span data-ttu-id="1b3a6-112">En cualquier caso, se elige un Namespace de Bus de servicio y una directiva de acceso compartido para ese espacio de nombres y un concentrador de eventos se crea en ese espacio de nombres cuando se produce el primer evento nuevo registro de actividad Hola.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when hello first new Activity Log event occurs.</span></span> <span data-ttu-id="1b3a6-113">Si no tiene un Namespace de Bus de servicio, primero debe toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-113">If you do not have a Service Bus Namespace, you first need toocreate one.</span></span> <span data-ttu-id="1b3a6-114">Si anteriormente se transmitido por secuencias de eventos de registro de actividad toothis Namespace de Bus de servicio, se reutilizarán Hola concentrador de eventos que se creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-114">If you have previously streamed Activity Log events toothis Service Bus Namespace, hello Event Hub that was previously created will be reused.</span></span> <span data-ttu-id="1b3a6-115">Directiva de acceso compartido de Hello define los permisos de Hola que tiene el mecanismo de transmisión por secuencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-115">hello shared access policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="1b3a6-116">En la actualidad, streaming centros de eventos de tooan requiere **administrar**, **enviar**, y **escuchar** permisos.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-116">Today, streaming tooan Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="1b3a6-117">Puede crear o modificar las directivas de acceso de Namespace de Bus de servicio compartido en el portal clásico de hello en la ficha de "Configurar" hello para el Namespace de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-117">You can create or modify Service Bus Namespace shared access policies in hello classic portal under hello “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="1b3a6-118">tooupdate Hola tooinclude streaming de perfil de registro de registro de actividad, usuario de Hola que realiza el cambio de hello debe tener permiso de ListKey de hello en esa regla de autorización de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-118">tooupdate hello Activity Log log profile tooinclude streaming, hello user making hello change must have hello ListKey permission on that Service Bus Authorization Rule.</span></span>

<span data-ttu-id="1b3a6-119">Hello espacio de nombres de concentrador de eventos o de bus de servicio no tiene toobe en hello misma suscripción que Hola emitir registros como usuario de Hola que configura los valores de hello tiene suscripciones de tooboth de acceso RBAC adecuadas.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-119">hello service bus or event hub namespace does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="1b3a6-120">Mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1b3a6-120">Via Azure portal</span></span>
1. <span data-ttu-id="1b3a6-121">Navegue toohello **registro de actividad** hoja con menú de hello en hello izquierda del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-121">Navigate toohello **Activity Log** blade using hello menu on hello left side of hello portal.</span></span>
   
    ![Navegue tooActivity registro en el portal](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="1b3a6-123">Haga clic en hello **exportar** situado en la parte superior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-123">Click hello **Export** button at hello top of hello blade.</span></span>
   
    ![Botón Exportar en el portal](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="1b3a6-125">En la hoja de Hola que aparece, puede seleccionar las regiones de hello para el que desea eventos toostream y Namespace de Bus de servicio de hello en el que desea una toobe de concentrador de eventos creado para la transmisión por secuencias estos eventos.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-125">In hello blade that appears, you can select hello regions for which you would like toostream events and hello Service Bus Namespace in which you would like an Event Hub toobe created for streaming these events.</span></span>
   
    ![Exportar en hoja de registro de actividad](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="1b3a6-127">Haga clic en **guardar** toosave esta configuración.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-127">Click **Save** toosave these settings.</span></span> <span data-ttu-id="1b3a6-128">configuración de Hello inmediatamente se pueden suscripción tooyour aplicada.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-128">hello settings are immediately be applied tooyour subscription.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="1b3a6-129">Mediante cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b3a6-129">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="1b3a6-130">Si ya existe un perfil de registro, primero debe tooremove dicho perfil.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-130">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="1b3a6-131">Use `Get-AzureRmLogProfile` tooidentify si existe un perfil de registro</span><span class="sxs-lookup"><span data-stu-id="1b3a6-131">Use `Get-AzureRmLogProfile` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="1b3a6-132">Si es así, utilice `Remove-AzureRmLogProfile` tooremove lo.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-132">If so, use `Remove-AzureRmLogProfile` tooremove it.</span></span>
3. <span data-ttu-id="1b3a6-133">Use `Set-AzureRmLogProfile` toocreate un perfil:</span><span class="sxs-lookup"><span data-stu-id="1b3a6-133">Use `Set-AzureRmLogProfile` toocreate a profile:</span></span>

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

<span data-ttu-id="1b3a6-134">Hola Id. de regla de Bus de servicio es una cadena con este formato: {Id. de recurso de bus de servicio} /authorizationrules/ {nombre de clave}, por ejemplo</span><span class="sxs-lookup"><span data-stu-id="1b3a6-134">hello Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span></span> 

### <a name="via-azure-cli"></a><span data-ttu-id="1b3a6-135">Mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="1b3a6-135">Via Azure CLI</span></span>
<span data-ttu-id="1b3a6-136">Si ya existe un perfil de registro, primero debe tooremove dicho perfil.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-136">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="1b3a6-137">Use `azure insights logprofile list` tooidentify si existe un perfil de registro</span><span class="sxs-lookup"><span data-stu-id="1b3a6-137">Use `azure insights logprofile list` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="1b3a6-138">Si es así, utilice `azure insights logprofile delete` tooremove lo.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-138">If so, use `azure insights logprofile delete` tooremove it.</span></span>
3. <span data-ttu-id="1b3a6-139">Use `azure insights logprofile add` toocreate un perfil:</span><span class="sxs-lookup"><span data-stu-id="1b3a6-139">Use `azure insights logprofile add` toocreate a profile:</span></span>

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

<span data-ttu-id="1b3a6-140">Hola Id. de regla de Bus de servicio es una cadena con este formato: `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="1b3a6-140">hello Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="1b3a6-141">¿Cómo se puede consumir datos de registro de hello de centros de eventos?</span><span class="sxs-lookup"><span data-stu-id="1b3a6-141">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="1b3a6-142">[esquema de Hello para el registro de actividad de Hola está disponible aquí](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="1b3a6-142">[hello schema for hello Activity Log is available here](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="1b3a6-143">Cada evento está en una matriz de blobs JSON denominados "registros".</span><span class="sxs-lookup"><span data-stu-id="1b3a6-143">Each event is in an array of JSON blobs called “records.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b3a6-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1b3a6-144">Next Steps</span></span>
* [<span data-ttu-id="1b3a6-145">Hola archivo cuenta de almacenamiento tooa de registro de actividad</span><span class="sxs-lookup"><span data-stu-id="1b3a6-145">Archive hello Activity Log tooa storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="1b3a6-146">Información general de Hola de lectura de hello Azure Activity Log</span><span class="sxs-lookup"><span data-stu-id="1b3a6-146">Read hello overview of hello Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="1b3a6-147">Configure una alerta basada en un evento del registro de actividades</span><span class="sxs-lookup"><span data-stu-id="1b3a6-147">Set up an alert based on an Activity Log event</span></span>](insights-auditlog-to-webhook-email.md)

