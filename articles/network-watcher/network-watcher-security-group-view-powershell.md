---
title: 'seguridad de red de aaaAnalyze con vista de grupo de seguridad de Azure red Monitor: PowerShell | Documentos de Microsoft'
description: "En este artículo se describe cómo toouse PowerShell tooanalyze un virtual máquinas seguridad con vista de grupo de seguridad."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04e76b49-6a1b-4d0f-9a9b-51cf2f4df5a2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5e1990d97899bd8585025ec13dd556ab2e034c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a><span data-ttu-id="2fd21-103">Análisis de seguridad de una máquina virtual con la vista de grupos de seguridad mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd21-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2fd21-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd21-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="2fd21-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2fd21-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="2fd21-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2fd21-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="2fd21-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="2fd21-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="2fd21-108">Vista de grupo de seguridad devuelve reglas de seguridad de red configurada y eficaz que están aplicados tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2fd21-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="2fd21-109">Esta capacidad es útil tooaudit y diagnosticar los grupos de seguridad de red y las reglas que se configuran en el tráfico de tooensure de una máquina virtual se está correctamente permitirá o denegará.</span><span class="sxs-lookup"><span data-stu-id="2fd21-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="2fd21-110">En este artículo, le mostraremos cómo configura tooretrieve hello y seguridad eficaz reglas tooa virtual machine con PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fd21-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using PowerShell</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2fd21-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="2fd21-111">Before you begin</span></span>

<span data-ttu-id="2fd21-112">En este escenario, ejecute hello `Get-AzureRmNetworkWatcherSecurityGroupView` información de la regla de seguridad de cmdlet tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="2fd21-112">In this scenario, you run hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tooretrieve hello security rule information.</span></span>

<span data-ttu-id="2fd21-113">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="2fd21-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="2fd21-114">Escenario</span><span class="sxs-lookup"><span data-stu-id="2fd21-114">Scenario</span></span>

<span data-ttu-id="2fd21-115">escenario de Hello descrito en este artículo recupera Hola configurado y las reglas de seguridad eficaz para una máquina virtual dada.</span><span class="sxs-lookup"><span data-stu-id="2fd21-115">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="2fd21-116">Recuperación de Network Watcher</span><span class="sxs-lookup"><span data-stu-id="2fd21-116">Retrieve Network Watcher</span></span>

<span data-ttu-id="2fd21-117">Hola primer paso es instancia de Monitor de red de tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="2fd21-117">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="2fd21-118">Esta variable se pasa toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2fd21-118">This variable is passed toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a><span data-ttu-id="2fd21-119">Obtención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2fd21-119">Get a VM</span></span>

<span data-ttu-id="2fd21-120">Una máquina virtual es necesario toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet en.</span><span class="sxs-lookup"><span data-stu-id="2fd21-120">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="2fd21-121">Hola de ejemplo siguiente obtiene un objeto de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2fd21-121">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="2fd21-122">Recuperación de la vista de grupos de seguridad</span><span class="sxs-lookup"><span data-stu-id="2fd21-122">Retrieve security group view</span></span>

<span data-ttu-id="2fd21-123">Hola siguiente paso es resultado de vista de grupo de seguridad de tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="2fd21-123">hello next step is tooretrieve hello security group view result.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-hello-results"></a><span data-ttu-id="2fd21-124">Ver los resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="2fd21-124">Viewing hello results</span></span>

<span data-ttu-id="2fd21-125">Hello en el ejemplo siguiente se es una respuesta reducida de los resultados de hello devueltos.</span><span class="sxs-lookup"><span data-stu-id="2fd21-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="2fd21-126">Hello resultados muestran todas las reglas de seguridad eficaz y aplicado hello en la máquina virtual de hello desglosado en grupos de **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, y  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="2fd21-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```
NetworkInterfaces : [
                      {
                        "NetworkInterfaceSecurityRules": [
                          {
                            "Name": "default-allow-rdp",
                            "Etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
                            "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/securityRules/default-allow-rdp",
                            "Protocol": "TCP",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "3389",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "Access": "Allow",
                            "Priority": 1000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "DefaultSecurityRules": [
                          {
                            "Name": "AllowVnetInBound",
                            "Id": "/subscriptions00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/defaultSecurityRules/",
                            "Description": "Allow inbound traffic from all VMs in VNET",
                            "Protocol": "*",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "*",
                            "SourceAddressPrefix": "VirtualNetwork",
                            "DestinationAddressPrefix": "VirtualNetwork",
                            "Access": "Allow",
                            "Priority": 65000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "EffectiveSecurityRules": [
                          {
                            "Name": "DefaultOutboundDenyAll",
                            "Protocol": "All",
                            "SourcePortRange": "0-65535",
                            "DestinationPortRange": "0-65535",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "ExpandedSourceAddressPrefix": [],
                            "ExpandedDestinationAddressPrefix": [],
                            "Access": "Deny",
                            "Priority": 65500,
                            "Direction": "Outbound"
                          },
                          ...
                        ]
                      }
                    ]
```

## <a name="next-steps"></a><span data-ttu-id="2fd21-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2fd21-127">Next steps</span></span>

<span data-ttu-id="2fd21-128">Visite [auditoría red seguridad grupos (NSG) con el Monitor de red](network-watcher-nsg-auditing-powershell.md) toolearn cómo tooautomate validación de grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="2fd21-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


