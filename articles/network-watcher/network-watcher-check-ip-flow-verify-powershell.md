---
title: "Comprobación del tráfico con la Comprobación del flujo de IP de Azure Network Watcher con PowerShell | Microsoft Docs"
description: "En este artículo se describe cómo comprobar si se permite o se deniega el tráfico hacia o desde una máquina virtual mediante PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: bf0c01a9af0e28647d11ad89a9d164716d5c8312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="94c73-103">Comprobar si se permite o se deniega el tráfico hacia o desde una máquina virtual con la Comprobación del flujo de IP, un componente de Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="94c73-103">Check if traffic is allowed or denied to or from a VM with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="94c73-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="94c73-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="94c73-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="94c73-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="94c73-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="94c73-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="94c73-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="94c73-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="94c73-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="94c73-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="94c73-109">La Comprobación del flujo de IP es una característica de Network Watcher que permite comprobar si se permite el tráfico hacia o desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="94c73-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="94c73-110">Este escenario es útil para averiguar si una máquina virtual puede comunicarse con un recurso externo o con un back-end.</span><span class="sxs-lookup"><span data-stu-id="94c73-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="94c73-111">Comprobación del flujo de IP se puede usar para comprobar si las reglas de grupos de seguridad de red (NSG) se han configurado correctamente y solucionar los problemas de flujos que las reglas de NSG bloquean.</span><span class="sxs-lookup"><span data-stu-id="94c73-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="94c73-112">Otra razón para usar la Comprobación del flujo de IP es asegurarse de que el NSG está bloqueando correctamente el tráfico que quiere bloquear.</span><span class="sxs-lookup"><span data-stu-id="94c73-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="94c73-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="94c73-113">Before you begin</span></span>

<span data-ttu-id="94c73-114">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create a Network Watcher](network-watcher-create.md) (Creación de una instancia de Network Watcher) o que ya tiene una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="94c73-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="94c73-115">En este escenario también se da por hecho que existe un grupo de recursos con una máquina virtual válida.</span><span class="sxs-lookup"><span data-stu-id="94c73-115">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="94c73-116">Escenario</span><span class="sxs-lookup"><span data-stu-id="94c73-116">Scenario</span></span>

<span data-ttu-id="94c73-117">Este escenario usa la comprobación del flujo de IP para comprobar si una máquina virtual pueden comunicarse con una dirección IP de Bing conocida.</span><span class="sxs-lookup"><span data-stu-id="94c73-117">This scenario uses IP flow verify to verify if a virtual machine can talk to a known Bing IP address.</span></span> <span data-ttu-id="94c73-118">Si se deniega el tráfico, devuelve la regla de seguridad que está denegando ese tráfico.</span><span class="sxs-lookup"><span data-stu-id="94c73-118">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="94c73-119">Para más información sobre la Comprobación del flujo de IP, vea [Introducción a la comprobación del flujo de IP](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="94c73-119">To learn more about IP flow verify, visit [IP flow verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="94c73-120">Recuperación de Network Watcher</span><span class="sxs-lookup"><span data-stu-id="94c73-120">Retrieve Network Watcher</span></span>

<span data-ttu-id="94c73-121">El primer paso consiste en recuperar la instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="94c73-121">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="94c73-122">La variable `$networkWatcher` pasa al cmdlet Comprobación del flujo de IP.</span><span class="sxs-lookup"><span data-stu-id="94c73-122">The `$networkWatcher` variable is passed to the IP flow verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="94c73-123">Obtención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="94c73-123">Get a VM</span></span>

<span data-ttu-id="94c73-124">La Comprobación del flujo de IP comprueba el tráfico hacia o desde la dirección IP de una máquina virtual, hacia o desde un destino remoto.</span><span class="sxs-lookup"><span data-stu-id="94c73-124">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span></span> <span data-ttu-id="94c73-125">Se necesita el identificador de una máquina virtual para ejecutar el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="94c73-125">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="94c73-126">Si ya conoce el identificador de la máquina virtual que se va a usar, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="94c73-126">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-the-nics"></a><span data-ttu-id="94c73-127">Obtención de las NIC</span><span class="sxs-lookup"><span data-stu-id="94c73-127">Get the NICS</span></span>

<span data-ttu-id="94c73-128">Se necesita la dirección IP de una NIC en la máquina virtual; en este ejemplo, se recuperan las NIC de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="94c73-128">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="94c73-129">Si ya conoce la dirección IP que desea probar en la máquina virtual, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="94c73-129">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="94c73-130">Ejecución de la Comprobación del flujo de IP</span><span class="sxs-lookup"><span data-stu-id="94c73-130">Run IP flow verify</span></span>

<span data-ttu-id="94c73-131">Ahora que tenemos la información necesaria para ejecutar el cmdlet `Test-AzureRmNetworkWatcherIPFlow`, lo ejecutamos para comprobar el tráfico.</span><span class="sxs-lookup"><span data-stu-id="94c73-131">Now that we have the information needed to run the cmdlet, we run the `Test-AzureRmNetworkWatcherIPFlow` cmdlet to test the traffic.</span></span> <span data-ttu-id="94c73-132">En este ejemplo, usamos la primera dirección IP en la primera NIC.</span><span class="sxs-lookup"><span data-stu-id="94c73-132">In this example, we are using the first IP address on the first NIC.</span></span>

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> <span data-ttu-id="94c73-133">La comprobación del flujo de IP requiere que el recurso de máquina virtual esté asignado para ejecución.</span><span class="sxs-lookup"><span data-stu-id="94c73-133">IP flow verify requires that the VM resource is allocated to run.</span></span>

## <a name="review-results"></a><span data-ttu-id="94c73-134">Revisión de los resultados</span><span class="sxs-lookup"><span data-stu-id="94c73-134">Review Results</span></span>

<span data-ttu-id="94c73-135">Después de ejecutar `Test-AzureRmNetworkWatcherIPFlow`, se devuelven los resultados. Los siguientes son los resultados devueltos por el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="94c73-135">After running `Test-AzureRmNetworkWatcherIPFlow` the results are returned, the following example is the results returned from the preceding step.</span></span>

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a><span data-ttu-id="94c73-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="94c73-136">Next steps</span></span>

<span data-ttu-id="94c73-137">Si se está bloqueando el tráfico y no debería ser así, vea [Administración de grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para realizar un seguimiento de las reglas del grupo de seguridad de red y de seguridad definidas.</span><span class="sxs-lookup"><span data-stu-id="94c73-137">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













