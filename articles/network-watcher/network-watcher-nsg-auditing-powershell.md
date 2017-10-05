---
title: "Automatización de la auditoría de grupos de seguridad de red con la vista de grupo de seguridad de Azure Network Watcher | Documentos de Microsoft"
description: "Esta página proporcionan instrucciones sobre cómo configurar la auditoría de un grupo de seguridad de red"
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
ms.openlocfilehash: a91da330e677c85f16f6f4e506613576b6507d7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a><span data-ttu-id="798b5-103">Automatización de la auditoría de grupos de seguridad de red con la vista de grupo de seguridad de Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="798b5-103">Automate NSG auditing with Azure Network Watcher Security group view</span></span>

<span data-ttu-id="798b5-104">Los clientes a menudo se enfrentan al desafío de comprobar la posición de seguridad de su infraestructura.</span><span class="sxs-lookup"><span data-stu-id="798b5-104">Customers are often faced with the challenge of verifying the security posture of their infrastructure.</span></span> <span data-ttu-id="798b5-105">Este desafío es similar para sus máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="798b5-105">This challenge is no different for their VMs in Azure.</span></span> <span data-ttu-id="798b5-106">Es importante contar con un perfil de seguridad similar basado en las reglas del grupo de seguridad de red (NSG) aplicadas.</span><span class="sxs-lookup"><span data-stu-id="798b5-106">It is important to have a similar security profile based on the Network Security Group (NSG) rules applied.</span></span> <span data-ttu-id="798b5-107">Mediante la vista de grupo de seguridad, ahora puede obtener la lista de reglas que se aplican a una máquina virtual dentro de un NSG.</span><span class="sxs-lookup"><span data-stu-id="798b5-107">Using the Security Group View, you can now get the list of rules applied to a VM within an NSG.</span></span> <span data-ttu-id="798b5-108">Puede definir un perfil de seguridad principal del NSG e iniciar la vista del grupo de seguridad con un ritmo semanal, comparar el resultado con el perfil principal y crear un informe.</span><span class="sxs-lookup"><span data-stu-id="798b5-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare the output to the golden profile and create a report.</span></span> <span data-ttu-id="798b5-109">De este modo puede identificar con facilidad todas las máquinas virtuales que no cumplen con el perfil de seguridad recomendado.</span><span class="sxs-lookup"><span data-stu-id="798b5-109">This way you can identify with ease all the VMs that do not conform to the prescribed security profile.</span></span>

<span data-ttu-id="798b5-110">Si no está familiarizado con los grupos de seguridad de red, acuda al artículo sobre [Información general sobre seguridad de red](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="798b5-110">If you are unfamiliar with Network Security Groups, visit [Network Security Overview](../virtual-network/virtual-networks-nsg.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="798b5-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="798b5-111">Before you begin</span></span>

<span data-ttu-id="798b5-112">En este escenario, se compara una línea base buena conocida con los resultados de la vista de grupo de seguridad devueltos para una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="798b5-112">In this scenario, you compare a known good baseline to the security group view results returned for a virtual machine.</span></span>

<span data-ttu-id="798b5-113">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create an Azure Network Watcher instance](network-watcher-create.md) (Creación de una instancia de Azure Network Watcher) para crear una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="798b5-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="798b5-114">En este escenario también se da por hecho que existe un grupo de recursos con una máquina virtual válida.</span><span class="sxs-lookup"><span data-stu-id="798b5-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="798b5-115">Escenario</span><span class="sxs-lookup"><span data-stu-id="798b5-115">Scenario</span></span>

<span data-ttu-id="798b5-116">El escenario descrito en este artículo obtiene la vista de grupo de seguridad para una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="798b5-116">The scenario covered in this article gets the security group view for a virtual machine.</span></span>

<span data-ttu-id="798b5-117">En este escenario va a:</span><span class="sxs-lookup"><span data-stu-id="798b5-117">In this scenario, you will:</span></span>

- <span data-ttu-id="798b5-118">Recuperar un conjunto de buenas reglas conocidas</span><span class="sxs-lookup"><span data-stu-id="798b5-118">Retrieve a known good rule set</span></span>
- <span data-ttu-id="798b5-119">Recuperar una máquina virtual con una API de REST</span><span class="sxs-lookup"><span data-stu-id="798b5-119">Retrieve a virtual machine with Rest API</span></span>
- <span data-ttu-id="798b5-120">Obtener la vista de grupo de seguridad para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="798b5-120">Get security group view for virtual machine</span></span>
- <span data-ttu-id="798b5-121">Evaluar la respuesta</span><span class="sxs-lookup"><span data-stu-id="798b5-121">Evaluate Response</span></span>

## <a name="retrieve-rule-set"></a><span data-ttu-id="798b5-122">Recuperación del conjunto de reglas</span><span class="sxs-lookup"><span data-stu-id="798b5-122">Retrieve rule set</span></span>

<span data-ttu-id="798b5-123">El primer paso en este ejemplo es trabajar con una línea base existente.</span><span class="sxs-lookup"><span data-stu-id="798b5-123">The first step in this example is to work with an existing baseline.</span></span> <span data-ttu-id="798b5-124">El ejemplo siguiente es un json extraído de un grupo de seguridad de red existente mediante el cmdlet `Get-AzureRmNetworkSecurityGroup` que se utiliza como línea de base para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="798b5-124">The following example is some json extracted from an existing Network Security Group using the `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as the baseline for this example.</span></span>

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

## <a name="convert-rule-set-to-powershell-objects"></a><span data-ttu-id="798b5-125">Conversión de los conjuntos de reglas en objetos de PowerShell</span><span class="sxs-lookup"><span data-stu-id="798b5-125">Convert rule set to PowerShell objects</span></span>

<span data-ttu-id="798b5-126">En este paso, leemos un archivo json que se creó anteriormente con las reglas que se espera que estén en el grupo de seguridad de red para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="798b5-126">In this step, we are reading a json file that was created earlier with the rules that are expected to be on the Network Security Group for this example.</span></span>

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a><span data-ttu-id="798b5-127">Recuperación de Network Watcher</span><span class="sxs-lookup"><span data-stu-id="798b5-127">Retrieve Network Watcher</span></span>

<span data-ttu-id="798b5-128">El siguiente paso es recuperar la instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="798b5-128">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="798b5-129">La variable `$networkWatcher` se pasa al cmdlet `AzureRmNetworkWatcherSecurityGroupView`.</span><span class="sxs-lookup"><span data-stu-id="798b5-129">The `$networkWatcher` variable is passed to the `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="798b5-130">Obtención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="798b5-130">Get a VM</span></span>

<span data-ttu-id="798b5-131">Se necesita una máquina virtual para ejecutar el cmdlet `Get-AzureRmNetworkWatcherSecurityGroupView`.</span><span class="sxs-lookup"><span data-stu-id="798b5-131">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="798b5-132">En el ejemplo siguiente se obtiene un objeto de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="798b5-132">The following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="798b5-133">Recuperación de la vista de grupos de seguridad</span><span class="sxs-lookup"><span data-stu-id="798b5-133">Retrieve security group view</span></span>

<span data-ttu-id="798b5-134">El siguiente paso es recuperar el resultado de la vista de grupos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="798b5-134">The next step is to retrieve the security group view result.</span></span> <span data-ttu-id="798b5-135">Este resultado se compara con el json de "línea base" que se mostró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="798b5-135">This result is compared to the "baseline" json that was shown earlier.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-the-results"></a><span data-ttu-id="798b5-136">Análisis de los resultados</span><span class="sxs-lookup"><span data-stu-id="798b5-136">Analyzing the results</span></span>

<span data-ttu-id="798b5-137">La respuesta se agrupa por interfaces de red.</span><span class="sxs-lookup"><span data-stu-id="798b5-137">The response is grouped by Network interfaces.</span></span> <span data-ttu-id="798b5-138">Los diferentes tipos de reglas devueltas son reglas de seguridad efectivas y predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="798b5-138">The different types of rules returned are effective and default security rules.</span></span> <span data-ttu-id="798b5-139">El resultado se divide más por la forma en la que se aplica,bien en una subred o una NIC virtual.</span><span class="sxs-lookup"><span data-stu-id="798b5-139">The result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span></span>

<span data-ttu-id="798b5-140">El siguiente script de PowerShell compara los resultados de la vista de grupo de seguridad con una salida existente de un NSG.</span><span class="sxs-lookup"><span data-stu-id="798b5-140">The following PowerShell script compares the results of the Security Group View to an existing output of an NSG.</span></span> <span data-ttu-id="798b5-141">El siguiente es un ejemplo sencillo de cómo se puedan comparar los resultados con el cmdlet `Compare-Object`.</span><span class="sxs-lookup"><span data-stu-id="798b5-141">The following example is a simple example of how the results can be compared with `Compare-Object` cmdlet.</span></span>

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

<span data-ttu-id="798b5-142">El ejemplo siguiente es el resultado.</span><span class="sxs-lookup"><span data-stu-id="798b5-142">The following example is the result.</span></span> <span data-ttu-id="798b5-143">Puede ver que dos de las reglas que estaban en el primer conjunto de reglas no estaban presentes en la comparación.</span><span class="sxs-lookup"><span data-stu-id="798b5-143">You can see two of the rules that were in the first rule set were not present in the comparison.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="798b5-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="798b5-144">Next steps</span></span>

<span data-ttu-id="798b5-145">Si se cambió la configuración, consulte [Administración de grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para realizar un seguimiento de los grupos de seguridad de red y las reglas de seguridad que pueden estar afectados.</span><span class="sxs-lookup"><span data-stu-id="798b5-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are in question.</span></span>













