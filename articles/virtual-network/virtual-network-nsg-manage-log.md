---
title: aaaMonitor operaciones, eventos y contadores de NSG | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooenable contadores, eventos y registro operativo para NSG"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2e699078-043f-48bd-8aa8-b011a32d98ca
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/31/2017
ms.author: jdial
ms.openlocfilehash: f16f1a0ad693028ee7aba21574b5c8ddfcd27096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a><span data-ttu-id="8ff28-103">Análisis del registro para grupos de seguridad de red (NSG)</span><span class="sxs-lookup"><span data-stu-id="8ff28-103">Log analytics for network security groups (NSGs)</span></span>

<span data-ttu-id="8ff28-104">Puede habilitar Hola siguientes categorías de registro de diagnóstico para los NSG:</span><span class="sxs-lookup"><span data-stu-id="8ff28-104">You can enable hello following diagnostic log categories for NSGs:</span></span>

* <span data-ttu-id="8ff28-105">**Evento:** contiene entradas para lo NSG son reglas tooVMs aplicados y roles de una instancia en función de la dirección MAC.</span><span class="sxs-lookup"><span data-stu-id="8ff28-105">**Event:** Contains entries for which NSG rules are applied tooVMs and instance roles based on MAC address.</span></span> <span data-ttu-id="8ff28-106">estado de Hola para que estas reglas se recopila cada 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="8ff28-106">hello status for these rules is collected every 60 seconds.</span></span>
* <span data-ttu-id="8ff28-107">**Contador de regla:** contiene entradas para el número de veces cada NSG de regla se aplica toodeny o permitir el tráfico.</span><span class="sxs-lookup"><span data-stu-id="8ff28-107">**Rule counter:** Contains entries for how many times each NSG rule is applied toodeny or allow traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="8ff28-108">Registros de diagnóstico solo están disponibles para los NSG implementados a través del modelo de implementación de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8ff28-108">Diagnostic logs are only available for NSGs deployed through hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="8ff28-109">No se puede habilitar el registro de diagnóstico para los NSG implementado a través del modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ff28-109">You cannot enable diagnostic logging for NSGs deployed through hello classic deployment model.</span></span> <span data-ttu-id="8ff28-110">Para entender mejor de los modelos de hello dos, hacen referencia a hello [modelos de implementación de Azure descripción](../resource-manager-deployment-model.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="8ff28-110">For a better understanding of hello two models, reference hello [Understanding Azure deployment models](../resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="8ff28-111">El registro de actividad (conocido anteriormente como registro operativo o de auditoría) está habilitado de forma predeterminada para los NSG creados a través de cualquier modelo de implementación de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ff28-111">Activity logging (previously known as audit or operational logs) is enabled by default for NSGs created through either Azure deployment model.</span></span> <span data-ttu-id="8ff28-112">toodetermine qué operaciones se completaron en NSG en el registro de actividad de hello, busque las entradas que contienen los siguientes tipos de recursos de hello:</span><span class="sxs-lookup"><span data-stu-id="8ff28-112">toodetermine which operations were completed on NSGs in hello activity log, look for entries that contain hello following resource types:</span></span> 

- <span data-ttu-id="8ff28-113">Microsoft.ClassicNetwork/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="8ff28-113">Microsoft.ClassicNetwork/networkSecurityGroups</span></span> 
- <span data-ttu-id="8ff28-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="8ff28-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span></span>
- <span data-ttu-id="8ff28-115">Microsoft.Network/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="8ff28-115">Microsoft.Network/networkSecurityGroups</span></span>
- <span data-ttu-id="8ff28-116">Microsoft.Network/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="8ff28-116">Microsoft.Network/networkSecurityGroups/securityRules</span></span> 

<span data-ttu-id="8ff28-117">Hola de lectura [información general de hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) artículo toolearn más información acerca de los registros de actividad.</span><span class="sxs-lookup"><span data-stu-id="8ff28-117">Read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) article toolearn more about activity logs.</span></span> 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="8ff28-118">Activación del registro de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="8ff28-118">Enable diagnostic logging</span></span>

<span data-ttu-id="8ff28-119">Debe habilitar el registro de diagnóstico para *cada* NSG desea toocollect datos de.</span><span class="sxs-lookup"><span data-stu-id="8ff28-119">Diagnostic logging must be enabled for *each* NSG you want toocollect data for.</span></span> <span data-ttu-id="8ff28-120">Hola [información general de Azure registros de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artículo explica dónde se pueden enviar registros de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="8ff28-120">hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article explains where diagnostic logs can be sent.</span></span> <span data-ttu-id="8ff28-121">Si no tienes un NSG existente, Hola completa los pasos de hello [crear un grupo de seguridad de red](virtual-networks-create-nsg-arm-pportal.md) toocreate artículo uno.</span><span class="sxs-lookup"><span data-stu-id="8ff28-121">If you don't have an existing NSG, complete hello steps in hello [Create a network security group](virtual-networks-create-nsg-arm-pportal.md) article toocreate one.</span></span> <span data-ttu-id="8ff28-122">Puede habilitar NSG mediante cualquiera de los siguientes métodos de Hola de registro de diagnóstico:</span><span class="sxs-lookup"><span data-stu-id="8ff28-122">You can enable NSG diagnostic logging using any of hello following methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="8ff28-123">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8ff28-123">Azure portal</span></span>

<span data-ttu-id="8ff28-124">registro de tooenable portal toouse hello, inicio de sesión toohello [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8ff28-124">toouse hello portal tooenable logging, login toohello [portal](https://portal.azure.com).</span></span> <span data-ttu-id="8ff28-125">Haga clic en **Más servicios** y, a continuación, escriba *grupos de seguridad de red*.</span><span class="sxs-lookup"><span data-stu-id="8ff28-125">Click **More services**, then type *network security groups*.</span></span> <span data-ttu-id="8ff28-126">Seleccione hello NSG desea tooenable para el registro.</span><span class="sxs-lookup"><span data-stu-id="8ff28-126">Select hello NSG you want tooenable logging for.</span></span> <span data-ttu-id="8ff28-127">Siga las instrucciones de Hola para los recursos de proceso no Hola [habilitar registros de diagnóstico en el portal de hello](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artículo.</span><span class="sxs-lookup"><span data-stu-id="8ff28-127">Follow hello instructions for non-compute resources in hello [Enable diagnostic logs in hello portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="8ff28-128">Seleccione **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, o las dos categorías de registros.</span><span class="sxs-lookup"><span data-stu-id="8ff28-128">Select **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, or both categories of logs.</span></span>

### <a name="powershell"></a><span data-ttu-id="8ff28-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ff28-129">PowerShell</span></span>

<span data-ttu-id="8ff28-130">toouse PowerShell tooenable registro, siga las instrucciones de Hola Hola [habilitar registros de diagnóstico a través de PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artículo.</span><span class="sxs-lookup"><span data-stu-id="8ff28-130">toouse PowerShell tooenable logging, follow hello instructions in hello [Enable diagnostic logs via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="8ff28-131">Evaluar Hola siguiente información antes de entrar en un comando de artículo hello:</span><span class="sxs-lookup"><span data-stu-id="8ff28-131">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="8ff28-132">Puede determinar Hola valor toouse para hello `-ResourceId` parámetro sustituyendo Hola después [texto], según corresponda, a continuación, escriba el comando de hello `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span><span class="sxs-lookup"><span data-stu-id="8ff28-132">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span></span> <span data-ttu-id="8ff28-133">salida de Hello Id. de comando hello parece demasiado*/Subscriptions / [nombre de suscripción Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.</span><span class="sxs-lookup"><span data-stu-id="8ff28-133">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="8ff28-134">Si solo desea toocollect datos de categoría de registro agregar `-Categories [category]` toohello final del comando de hello en el artículo hello, donde categoría sea *NetworkSecurityGroupEvent* o *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="8ff28-134">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="8ff28-135">Si no utiliza hello `-Categories` parámetro, la recopilación de datos está habilitada para el registro de categorías.</span><span class="sxs-lookup"><span data-stu-id="8ff28-135">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

### <a name="azure-command-line-interface-cli"></a><span data-ttu-id="8ff28-136">Interfaz de la línea de comandos (CLI) de Azure</span><span class="sxs-lookup"><span data-stu-id="8ff28-136">Azure command-line interface (CLI)</span></span>

<span data-ttu-id="8ff28-137">toouse Hola registro tooenable CLI, siga las instrucciones de Hola Hola [habilitar registros de diagnóstico mediante la CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artículo.</span><span class="sxs-lookup"><span data-stu-id="8ff28-137">toouse hello CLI tooenable logging, follow hello instructions in hello [Enable diagnostic logs via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) article.</span></span> <span data-ttu-id="8ff28-138">Evaluar Hola siguiente información antes de entrar en un comando de artículo hello:</span><span class="sxs-lookup"><span data-stu-id="8ff28-138">Evaluate hello following information before entering a command from hello article:</span></span>

- <span data-ttu-id="8ff28-139">Puede determinar Hola valor toouse para hello `-ResourceId` parámetro sustituyendo Hola después [texto], según corresponda, a continuación, escriba el comando de hello `azure network nsg show [resource-group-name] [nsg-name]`.</span><span class="sxs-lookup"><span data-stu-id="8ff28-139">You can determine hello value toouse for hello `-ResourceId` parameter by replacing hello following [text], as appropriate, then entering hello command `azure network nsg show [resource-group-name] [nsg-name]`.</span></span> <span data-ttu-id="8ff28-140">salida de Hello Id. de comando hello parece demasiado*/Subscriptions / [nombre de suscripción Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.</span><span class="sxs-lookup"><span data-stu-id="8ff28-140">hello ID output from hello command looks similar too*/subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="8ff28-141">Si solo desea toocollect datos de categoría de registro agregar `-Categories [category]` toohello final del comando de hello en el artículo hello, donde categoría sea *NetworkSecurityGroupEvent* o *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="8ff28-141">If you only want toocollect data from log category add `-Categories [category]` toohello end of hello command in hello article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="8ff28-142">Si no utiliza hello `-Categories` parámetro, la recopilación de datos está habilitada para el registro de categorías.</span><span class="sxs-lookup"><span data-stu-id="8ff28-142">If you don't use hello `-Categories` parameter, data collection is enabled for both log categories.</span></span>

## <a name="logged-data"></a><span data-ttu-id="8ff28-143">Datos registrados</span><span class="sxs-lookup"><span data-stu-id="8ff28-143">Logged data</span></span>

<span data-ttu-id="8ff28-144">Se escriben datos con formato JSON para ambos registros.</span><span class="sxs-lookup"><span data-stu-id="8ff28-144">JSON-formatted data is written for both logs.</span></span> <span data-ttu-id="8ff28-145">datos específicos de Hello escritos para cada tipo de registro aparece en hello las secciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="8ff28-145">hello specific data written for each log type is listed in hello following sections:</span></span>

### <a name="event-log"></a><span data-ttu-id="8ff28-146">Registro de eventos</span><span class="sxs-lookup"><span data-stu-id="8ff28-146">Event log</span></span>
<span data-ttu-id="8ff28-147">Este registro contiene información acerca de qué NSG reglas tooVMs aplicados e instancias de rol de servicio, en función de la dirección MAC en la nube.</span><span class="sxs-lookup"><span data-stu-id="8ff28-147">This log contains information about which NSG rules are applied tooVMs and cloud service role instances, based on MAC address.</span></span> <span data-ttu-id="8ff28-148">Después de los datos de ejemplo de Hola se registra para cada evento:</span><span class="sxs-lookup"><span data-stu-id="8ff28-148">hello following example data is logged for each event:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupEvent",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION-ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupEvents",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-B791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "priority":1000,
        "type":"allow",
        "conditions":{
            "protocols":"6",
            "destinationPortRange":"3389-3389",
            "sourcePortRange":"0-65535",
            "sourceIP":"0.0.0.0/0",
            "destinationIP":"0.0.0.0/0"
            }
        }
}
```

### <a name="rule-counter-log"></a><span data-ttu-id="8ff28-149">Registro de contador de regla</span><span class="sxs-lookup"><span data-stu-id="8ff28-149">Rule counter log</span></span>

<span data-ttu-id="8ff28-150">Este registro contiene información sobre cada tooresources regla aplicada.</span><span class="sxs-lookup"><span data-stu-id="8ff28-150">This log contains information about each rule applied tooresources.</span></span> <span data-ttu-id="8ff28-151">Hello datos de ejemplo siguiente se registran cada vez que se aplica una regla:</span><span class="sxs-lookup"><span data-stu-id="8ff28-151">hello following example data is logged each time a rule is applied:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupRuleCounter",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]TESTRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupCounters",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "type":"allow",
        "matchedConnections":125
        }
}
```

## <a name="view-and-analyze-logs"></a><span data-ttu-id="8ff28-152">Visualización y análisis de los registros</span><span class="sxs-lookup"><span data-stu-id="8ff28-152">View and analyze logs</span></span>

<span data-ttu-id="8ff28-153">toolearn cómo tooview actividad registrar los datos, leer hello [información general de hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="8ff28-153">toolearn how tooview activity log data, read hello [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="8ff28-154">toolearn cómo tooview diagnóstico registrar los datos, leer hello [información general de Azure registros de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="8ff28-154">toolearn how tooview diagnostic log data, read hello [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="8ff28-155">Si envía datos de diagnóstico tooLog análisis, puede usar hello [análisis de grupo de seguridad de red de Azure](../log-analytics/log-analytics-azure-networking-analytics.md) solución de administración de (versión preliminar) para visión mejorada.</span><span class="sxs-lookup"><span data-stu-id="8ff28-155">If you send diagnostics data tooLog Analytics, you can use hello [Azure Network Security Group analytics](../log-analytics/log-analytics-azure-networking-analytics.md) (preview) management solution for enhanced insights.</span></span> 
