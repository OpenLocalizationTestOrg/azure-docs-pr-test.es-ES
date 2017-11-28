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
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a><span data-ttu-id="3ba50-103">Automatización de la auditoría de grupos de seguridad de red con la vista de grupo de seguridad de Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="3ba50-103">Automate NSG auditing with Azure Network Watcher Security group view</span></span>

<span data-ttu-id="3ba50-104">Desafío de Hola de comprobación de la postura de seguridad de su infraestructura de Hola a menudo se enfrentan los clientes.</span><span class="sxs-lookup"><span data-stu-id="3ba50-104">Customers are often faced with hello challenge of verifying hello security posture of their infrastructure.</span></span> <span data-ttu-id="3ba50-105">Este desafío es similar para sus máquinas virtuales en Azure.</span><span class="sxs-lookup"><span data-stu-id="3ba50-105">This challenge is no different for their VMs in Azure.</span></span> <span data-ttu-id="3ba50-106">Es importante toohave según reglas de grupo de seguridad de red (NSG) de hello aplicadas un perfil de seguridad similar.</span><span class="sxs-lookup"><span data-stu-id="3ba50-106">It is important toohave a similar security profile based on hello Network Security Group (NSG) rules applied.</span></span> <span data-ttu-id="3ba50-107">Hola vista de grupo de seguridad puede obtener ahora lista Hola de reglas que se aplican tooa VM dentro de un NSG.</span><span class="sxs-lookup"><span data-stu-id="3ba50-107">Using hello Security Group View, you can now get hello list of rules applied tooa VM within an NSG.</span></span> <span data-ttu-id="3ba50-108">Puede definir un perfil de seguridad NSG dorado e iniciar vista de grupo de seguridad a un ritmo semanal y comparar el perfil de toohello dorada de salida de hello y crear un informe.</span><span class="sxs-lookup"><span data-stu-id="3ba50-108">You can define a golden NSG security profile and initiate Security Group View on a weekly cadence and compare hello output toohello golden profile and create a report.</span></span> <span data-ttu-id="3ba50-109">Este modo puede identificar con facilidad todas las máquinas virtuales de Hola que no cumplen toohello lo prescrito, perfil de seguridad.</span><span class="sxs-lookup"><span data-stu-id="3ba50-109">This way you can identify with ease all hello VMs that do not conform toohello prescribed security profile.</span></span>

<span data-ttu-id="3ba50-110">Si no está familiarizado con los grupos de seguridad de red, acuda al artículo sobre [Información general sobre seguridad de red](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="3ba50-110">If you are unfamiliar with Network Security Groups, visit [Network Security Overview](../virtual-network/virtual-networks-nsg.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3ba50-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="3ba50-111">Before you begin</span></span>

<span data-ttu-id="3ba50-112">En este escenario, se compara un grupo de seguridad buena conocida de línea de base toohello ver los resultados devueltos para una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3ba50-112">In this scenario, you compare a known good baseline toohello security group view results returned for a virtual machine.</span></span>

<span data-ttu-id="3ba50-113">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="3ba50-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="3ba50-114">escenario de Hello también supone que un grupo de recursos con una máquina virtual válida existe toobe usa.</span><span class="sxs-lookup"><span data-stu-id="3ba50-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="3ba50-115">Escenario</span><span class="sxs-lookup"><span data-stu-id="3ba50-115">Scenario</span></span>

<span data-ttu-id="3ba50-116">escenario de Hello descrito en este artículo obtiene la vista de grupo de seguridad de Hola para una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3ba50-116">hello scenario covered in this article gets hello security group view for a virtual machine.</span></span>

<span data-ttu-id="3ba50-117">En este escenario va a:</span><span class="sxs-lookup"><span data-stu-id="3ba50-117">In this scenario, you will:</span></span>

- <span data-ttu-id="3ba50-118">Recuperar un conjunto de buenas reglas conocidas</span><span class="sxs-lookup"><span data-stu-id="3ba50-118">Retrieve a known good rule set</span></span>
- <span data-ttu-id="3ba50-119">Recuperar una máquina virtual con una API de REST</span><span class="sxs-lookup"><span data-stu-id="3ba50-119">Retrieve a virtual machine with Rest API</span></span>
- <span data-ttu-id="3ba50-120">Obtener la vista de grupo de seguridad para una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3ba50-120">Get security group view for virtual machine</span></span>
- <span data-ttu-id="3ba50-121">Evaluar la respuesta</span><span class="sxs-lookup"><span data-stu-id="3ba50-121">Evaluate Response</span></span>

## <a name="retrieve-rule-set"></a><span data-ttu-id="3ba50-122">Recuperación del conjunto de reglas</span><span class="sxs-lookup"><span data-stu-id="3ba50-122">Retrieve rule set</span></span>

<span data-ttu-id="3ba50-123">Hola primer paso en este ejemplo es toowork con una instantánea existente.</span><span class="sxs-lookup"><span data-stu-id="3ba50-123">hello first step in this example is toowork with an existing baseline.</span></span> <span data-ttu-id="3ba50-124">el ejemplo siguiente se Hello es algunos json extraído de un grupo de seguridad de red existente utilizando hello `Get-AzureRmNetworkSecurityGroup` cmdlet que se usa como línea base de hello en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3ba50-124">hello following example is some json extracted from an existing Network Security Group using hello `Get-AzureRmNetworkSecurityGroup` cmdlet that is used as hello baseline for this example.</span></span>

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

## <a name="convert-rule-set-toopowershell-objects"></a><span data-ttu-id="3ba50-125">Convertir objetos de tooPowerShell del conjunto de reglas</span><span class="sxs-lookup"><span data-stu-id="3ba50-125">Convert rule set tooPowerShell objects</span></span>

<span data-ttu-id="3ba50-126">En este paso, estamos leyendo un archivo json que creó anteriormente con reglas de hello toobe esperado en hello grupo de seguridad de red para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3ba50-126">In this step, we are reading a json file that was created earlier with hello rules that are expected toobe on hello Network Security Group for this example.</span></span>

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a><span data-ttu-id="3ba50-127">Recuperación de Network Watcher</span><span class="sxs-lookup"><span data-stu-id="3ba50-127">Retrieve Network Watcher</span></span>

<span data-ttu-id="3ba50-128">Hola siguiente paso es instancia de Monitor de red de tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="3ba50-128">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="3ba50-129">Hola `$networkWatcher` pasa una variable toohello `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3ba50-129">hello `$networkWatcher` variable is passed toohello `AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="3ba50-130">Obtención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3ba50-130">Get a VM</span></span>

<span data-ttu-id="3ba50-131">Una máquina virtual es necesario toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet en.</span><span class="sxs-lookup"><span data-stu-id="3ba50-131">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="3ba50-132">Hola de ejemplo siguiente obtiene un objeto de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3ba50-132">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="3ba50-133">Recuperación de la vista de grupos de seguridad</span><span class="sxs-lookup"><span data-stu-id="3ba50-133">Retrieve security group view</span></span>

<span data-ttu-id="3ba50-134">Hola siguiente paso es resultado de vista de grupo de seguridad de tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="3ba50-134">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="3ba50-135">El resultado es toohello comparados "baseline" json que se mostró anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3ba50-135">This result is compared toohello "baseline" json that was shown earlier.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-hello-results"></a><span data-ttu-id="3ba50-136">Analizar los resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="3ba50-136">Analyzing hello results</span></span>

<span data-ttu-id="3ba50-137">respuesta de Hola se agrupa por interfaces de red.</span><span class="sxs-lookup"><span data-stu-id="3ba50-137">hello response is grouped by Network interfaces.</span></span> <span data-ttu-id="3ba50-138">tipos diferentes de Hello de reglas devueltas son eficaces y reglas de seguridad predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="3ba50-138">hello different types of rules returned are effective and default security rules.</span></span> <span data-ttu-id="3ba50-139">resultado de Hello adicional se divide en cómo se aplica, en una subred o una NIC virtual.</span><span class="sxs-lookup"><span data-stu-id="3ba50-139">hello result is further broken down by how it is applied, either on a subnet or a virtual NIC.</span></span>

<span data-ttu-id="3ba50-140">Hello siguiente script de PowerShell compara los resultados de Hola de hello tooan existente salida de vista de grupo de seguridad de un NSG.</span><span class="sxs-lookup"><span data-stu-id="3ba50-140">hello following PowerShell script compares hello results of hello Security Group View tooan existing output of an NSG.</span></span> <span data-ttu-id="3ba50-141">el ejemplo siguiente se Hello es un ejemplo sencillo de cómo se pueden comparar los resultados de hello con `Compare-Object` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3ba50-141">hello following example is a simple example of how hello results can be compared with `Compare-Object` cmdlet.</span></span>

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

<span data-ttu-id="3ba50-142">Hola siguiente ejemplo es resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="3ba50-142">hello following example is hello result.</span></span> <span data-ttu-id="3ba50-143">Puede ver dos de las reglas de Hola que se encontraban en el primer conjunto de reglas hello no estaban presentes en la comparación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3ba50-143">You can see two of hello rules that were in hello first rule set were not present in hello comparison.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3ba50-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3ba50-144">Next steps</span></span>

<span data-ttu-id="3ba50-145">Si se han cambiado la configuración, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hacia abajo Hola red seguridad y el grupo de reglas de seguridad que están en cuestión.</span><span class="sxs-lookup"><span data-stu-id="3ba50-145">If settings have been changed, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are in question.</span></span>













