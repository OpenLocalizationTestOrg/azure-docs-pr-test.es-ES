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
# <a name="log-analytics-for-network-security-groups-nsgs"></a>Análisis del registro para grupos de seguridad de red (NSG)

Puede habilitar Hola siguientes categorías de registro de diagnóstico para los NSG:

* **Evento:** contiene entradas para lo NSG son reglas tooVMs aplicados y roles de una instancia en función de la dirección MAC. estado de Hola para que estas reglas se recopila cada 60 segundos.
* **Contador de regla:** contiene entradas para el número de veces cada NSG de regla se aplica toodeny o permitir el tráfico.

> [!NOTE]
> Registros de diagnóstico solo están disponibles para los NSG implementados a través del modelo de implementación de hello Azure Resource Manager. No se puede habilitar el registro de diagnóstico para los NSG implementado a través del modelo de implementación clásica de Hola. Para entender mejor de los modelos de hello dos, hacen referencia a hello [modelos de implementación de Azure descripción](../resource-manager-deployment-model.md) artículo.

El registro de actividad (conocido anteriormente como registro operativo o de auditoría) está habilitado de forma predeterminada para los NSG creados a través de cualquier modelo de implementación de Azure. toodetermine qué operaciones se completaron en NSG en el registro de actividad de hello, busque las entradas que contienen los siguientes tipos de recursos de hello: 

- Microsoft.ClassicNetwork/networkSecurityGroups 
- Microsoft.ClassicNetwork/networkSecurityGroups/securityRules
- Microsoft.Network/networkSecurityGroups
- Microsoft.Network/networkSecurityGroups/securityRules 

Hola de lectura [información general de hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) artículo toolearn más información acerca de los registros de actividad. 

## <a name="enable-diagnostic-logging"></a>Activación del registro de diagnóstico

Debe habilitar el registro de diagnóstico para *cada* NSG desea toocollect datos de. Hola [información general de Azure registros de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artículo explica dónde se pueden enviar registros de diagnóstico. Si no tienes un NSG existente, Hola completa los pasos de hello [crear un grupo de seguridad de red](virtual-networks-create-nsg-arm-pportal.md) toocreate artículo uno. Puede habilitar NSG mediante cualquiera de los siguientes métodos de Hola de registro de diagnóstico:

### <a name="azure-portal"></a>Azure Portal

registro de tooenable portal toouse hello, inicio de sesión toohello [portal](https://portal.azure.com). Haga clic en **Más servicios** y, a continuación, escriba *grupos de seguridad de red*. Seleccione hello NSG desea tooenable para el registro. Siga las instrucciones de Hola para los recursos de proceso no Hola [habilitar registros de diagnóstico en el portal de hello](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artículo. Seleccione **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, o las dos categorías de registros.

### <a name="powershell"></a>PowerShell

toouse PowerShell tooenable registro, siga las instrucciones de Hola Hola [habilitar registros de diagnóstico a través de PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artículo. Evaluar Hola siguiente información antes de entrar en un comando de artículo hello:

- Puede determinar Hola valor toouse para hello `-ResourceId` parámetro sustituyendo Hola después [texto], según corresponda, a continuación, escriba el comando de hello `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`. salida de Hello Id. de comando hello parece demasiado*/Subscriptions / [nombre de suscripción Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.
- Si solo desea toocollect datos de categoría de registro agregar `-Categories [category]` toohello final del comando de hello en el artículo hello, donde categoría sea *NetworkSecurityGroupEvent* o *NetworkSecurityGroupRuleCounter*. Si no utiliza hello `-Categories` parámetro, la recopilación de datos está habilitada para el registro de categorías.

### <a name="azure-command-line-interface-cli"></a>Interfaz de la línea de comandos (CLI) de Azure

toouse Hola registro tooenable CLI, siga las instrucciones de Hola Hola [habilitar registros de diagnóstico mediante la CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs) artículo. Evaluar Hola siguiente información antes de entrar en un comando de artículo hello:

- Puede determinar Hola valor toouse para hello `-ResourceId` parámetro sustituyendo Hola después [texto], según corresponda, a continuación, escriba el comando de hello `azure network nsg show [resource-group-name] [nsg-name]`. salida de Hello Id. de comando hello parece demasiado*/Subscriptions / [nombre de suscripción Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG]*.
- Si solo desea toocollect datos de categoría de registro agregar `-Categories [category]` toohello final del comando de hello en el artículo hello, donde categoría sea *NetworkSecurityGroupEvent* o *NetworkSecurityGroupRuleCounter*. Si no utiliza hello `-Categories` parámetro, la recopilación de datos está habilitada para el registro de categorías.

## <a name="logged-data"></a>Datos registrados

Se escriben datos con formato JSON para ambos registros. datos específicos de Hello escritos para cada tipo de registro aparece en hello las secciones siguientes:

### <a name="event-log"></a>Registro de eventos
Este registro contiene información acerca de qué NSG reglas tooVMs aplicados e instancias de rol de servicio, en función de la dirección MAC en la nube. Después de los datos de ejemplo de Hola se registra para cada evento:

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

### <a name="rule-counter-log"></a>Registro de contador de regla

Este registro contiene información sobre cada tooresources regla aplicada. Hello datos de ejemplo siguiente se registran cada vez que se aplica una regla:

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

## <a name="view-and-analyze-logs"></a>Visualización y análisis de los registros

toolearn cómo tooview actividad registrar los datos, leer hello [información general de hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artículo. toolearn cómo tooview diagnóstico registrar los datos, leer hello [información general de Azure registros de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artículo. Si envía datos de diagnóstico tooLog análisis, puede usar hello [análisis de grupo de seguridad de red de Azure](../log-analytics/log-analytics-azure-networking-analytics.md) solución de administración de (versión preliminar) para visión mejorada. 
