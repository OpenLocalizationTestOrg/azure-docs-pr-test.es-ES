---
title: "auditoría de NSG aaaAutomate con vista de grupo de seguridad del Monitor de red de Azure | Documentos de Microsoft"
description: "Esta página proporciona instrucciones sobre cómo tooconfigure la auditoría de un grupo de seguridad de red"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 78a01bcf-74fe-402a-9812-285f3501f877
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 24fc418c433fceaf55a74b7c3b0e354dc46c8729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a>Automatización de la auditoría de grupos de seguridad de red con la vista de grupo de seguridad de Azure Network Watcher

Desafío de Hola de comprobación de la postura de seguridad de su infraestructura de Hola a menudo se enfrentan los clientes. Este desafío es similar para sus máquinas virtuales en Azure. Es importante toohave según reglas de grupo de seguridad de red (NSG) de hello aplicadas un perfil de seguridad similar. Hola vista de grupo de seguridad puede obtener ahora lista Hola de reglas que se aplican tooa VM dentro de un NSG. Puede definir un perfil de seguridad NSG dorado e iniciar vista de grupo de seguridad a un ritmo semanal y comparar el perfil de toohello dorada de salida de hello y crear un informe. Este modo puede identificar con facilidad todas las máquinas virtuales de Hola que no cumplen toohello lo prescrito, perfil de seguridad.

Si no está familiarizado con los grupos de seguridad de red, acuda al artículo sobre [Información general sobre seguridad de red](../virtual-network/virtual-networks-nsg.md)

## <a name="before-you-begin"></a>Antes de empezar

En este escenario, se compara un grupo de seguridad buena conocida de línea de base toohello ver los resultados devueltos para una máquina virtual.

Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red. escenario de Hello también supone que un grupo de recursos con una máquina virtual válida existe toobe usa.

## <a name="scenario"></a>Escenario

escenario de Hello descrito en este artículo obtiene la vista de grupo de seguridad de Hola para una máquina virtual.

En este escenario va a:

- Recuperar un conjunto de buenas reglas conocidas
- Recuperar una máquina virtual con una API de REST
- Obtener la vista de grupo de seguridad para una máquina virtual
- Evaluar la respuesta

## <a name="retrieve-rule-set"></a>Recuperación del conjunto de reglas

Hola primer paso en este ejemplo es toowork con una instantánea existente. el ejemplo siguiente se Hello es algunos json extraído de un grupo de seguridad de red existente utilizando hello `Get-AzureRmNetworkSecurityGroup` cmdlet que se usa como línea base de hello en este ejemplo.

```json
[
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "3389",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1000,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "default-allow-rdp",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/default-allow-rdp"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "111",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1010,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "MyRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/MyRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "112",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1020,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "My2ndRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/My2ndRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "5672",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Deny",
        "Priority":  1030,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "ThisRuleNeedsToStay",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/ThisRuleNeedsToStay"
    }
]
```

## <a name="convert-rule-set-toopowershell-objects"></a>Convertir objetos de tooPowerShell del conjunto de reglas

En este paso, estamos leyendo un archivo json que creó anteriormente con reglas de hello toobe esperado en hello grupo de seguridad de red para este ejemplo.

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a>Recuperación de Network Watcher

Hola siguiente paso es instancia de Monitor de red de tooretrieve Hola. Hola `$networkWatcher` pasa una variable toohello `AzureRmNetworkWatcherSecurityGroupView` cmdlet.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a>Obtención de una máquina virtual

Una máquina virtual es necesario toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet en. Hola de ejemplo siguiente obtiene un objeto de máquina virtual.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a>Recuperación de la vista de grupos de seguridad

Hola siguiente paso es resultado de vista de grupo de seguridad de tooretrieve Hola. El resultado es toohello comparados "baseline" json que se mostró anteriormente.

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-hello-results"></a>Analizar los resultados de Hola

respuesta de Hola se agrupa por interfaces de red. tipos diferentes de Hello de reglas devueltas son eficaces y reglas de seguridad predeterminadas. resultado de Hello adicional se divide en cómo se aplica, en una subred o una NIC virtual.

Hello siguiente script de PowerShell compara los resultados de Hola de hello tooan existente salida de vista de grupo de seguridad de un NSG. el ejemplo siguiente se Hello es un ejemplo sencillo de cómo se pueden comparar los resultados de hello con `Compare-Object` cmdlet.

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

Hola siguiente ejemplo es resultado de hello. Puede ver dos de las reglas de Hola que se encontraban en el primer conjunto de reglas hello no estaban presentes en la comparación de Hola.

```
Name                     : My2ndRuleDoNotDelete
Description              : 
Protocol                 : *
SourcePortRange          : *
DestinationPortRange     : 112
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Allow
Priority                 : 1020
Direction                : Inbound
SideIndicator            : <=

Name                     : ThisRuleNeedsToStay
Description              : 
Protocol                 : TCP
SourcePortRange          : *
DestinationPortRange     : 5672
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Deny
Priority                 : 1030
Direction                : Inbound
SideIndicator            : <=
```

## <a name="next-steps"></a>Pasos siguientes

Si se han cambiado la configuración, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hacia abajo Hola red seguridad y el grupo de reglas de seguridad que están en cuestión.













