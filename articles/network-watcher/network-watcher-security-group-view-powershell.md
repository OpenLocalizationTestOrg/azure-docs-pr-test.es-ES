---
title: "Análisis de la seguridad de red con la vista de grupos de seguridad de Azure Network Watcher (PowerShell) | Microsoft Docs"
description: "En este artículo se describe cómo utilizar PowerShell para analizar la seguridad de máquinas virtuales con la vista de grupos de seguridad."
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
ms.openlocfilehash: 363fdd9f1de933bb4050f91e1e111aaf3e419058
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a><span data-ttu-id="c4a1e-103">Análisis de seguridad de una máquina virtual con la vista de grupos de seguridad mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4a1e-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c4a1e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4a1e-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="c4a1e-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c4a1e-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="c4a1e-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c4a1e-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="c4a1e-107">API DE REST</span><span class="sxs-lookup"><span data-stu-id="c4a1e-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="c4a1e-108">La vista de grupos de seguridad devuelve las reglas de seguridad de red configuradas y vigentes que se aplican a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4a1e-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="c4a1e-109">Esta funcionalidad resulta útil para auditar y diagnosticar los grupos de seguridad de red y las reglas que están configuradas en una máquina virtual para asegurarse de que el tráfico se está permitiendo o denegando correctamente.</span><span class="sxs-lookup"><span data-stu-id="c4a1e-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="c4a1e-110">En este artículo se muestra cómo recuperar las reglas de seguridad configuradas y vigentes para una máquina virtual mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4a1e-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using PowerShell</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c4a1e-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="c4a1e-111">Before you begin</span></span>

<span data-ttu-id="c4a1e-112">En este escenario, se ejecuta el cmdlet `Get-AzureRmNetworkWatcherSecurityGroupView` para recuperar la información de la regla de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c4a1e-112">In this scenario, you run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet to retrieve the security rule information.</span></span>

<span data-ttu-id="c4a1e-113">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create an Azure Network Watcher instance](network-watcher-create.md) (Creación de una instancia de Azure Network Watcher) para crear una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="c4a1e-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="c4a1e-114">Escenario</span><span class="sxs-lookup"><span data-stu-id="c4a1e-114">Scenario</span></span>

<span data-ttu-id="c4a1e-115">El escenario descrito en este artículo recupera las reglas de seguridad configuradas y vigentes para una máquina virtual dada.</span><span class="sxs-lookup"><span data-stu-id="c4a1e-115">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="c4a1e-116">Recuperación de Network Watcher</span><span class="sxs-lookup"><span data-stu-id="c4a1e-116">Retrieve Network Watcher</span></span>

<span data-ttu-id="c4a1e-117">El primer paso consiste en recuperar la instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="c4a1e-117">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="c4a1e-118">Esta variable se pasa al cmdlet `Get-AzureRmNetworkWatcherSecurityGroupView`.</span><span class="sxs-lookup"><span data-stu-id="c4a1e-118">This variable is passed to the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a><span data-ttu-id="c4a1e-119">Obtención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c4a1e-119">Get a VM</span></span>

<span data-ttu-id="c4a1e-120">Se necesita una máquina virtual para ejecutar el cmdlet `Get-AzureRmNetworkWatcherSecurityGroupView`.</span><span class="sxs-lookup"><span data-stu-id="c4a1e-120">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="c4a1e-121">En el ejemplo siguiente se obtiene un objeto de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c4a1e-121">The following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="c4a1e-122">Recuperación de la vista de grupos de seguridad</span><span class="sxs-lookup"><span data-stu-id="c4a1e-122">Retrieve security group view</span></span>

<span data-ttu-id="c4a1e-123">El siguiente paso es recuperar el resultado de la vista de grupos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c4a1e-123">The next step is to retrieve the security group view result.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-the-results"></a><span data-ttu-id="c4a1e-124">Visualización de los resultados</span><span class="sxs-lookup"><span data-stu-id="c4a1e-124">Viewing the results</span></span>

<span data-ttu-id="c4a1e-125">El ejemplo siguiente es una respuesta reducida de los resultados devueltos.</span><span class="sxs-lookup"><span data-stu-id="c4a1e-125">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="c4a1e-126">Los resultados muestran todas las reglas de seguridad vigentes y aplicadas en la máquina virtual, clasificadas en los grupos **NetworkInterfaceSecurityRules**, **DefaultSecurityRules** y **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="c4a1e-126">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c4a1e-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c4a1e-127">Next steps</span></span>

<span data-ttu-id="c4a1e-128">Visite [Automate NSG auditing with Azure Network Watcher Security group view](network-watcher-nsg-auditing-powershell.md) (Automatización de la auditoría de grupos de seguridad de red (NSG) con la vista de grupos de seguridad de Azure Network Watcher) para aprender a automatizar la validación de grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="c4a1e-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>


