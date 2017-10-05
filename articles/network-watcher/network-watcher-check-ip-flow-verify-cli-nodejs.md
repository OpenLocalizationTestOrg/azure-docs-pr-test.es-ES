---
title: "Comprobación del tráfico con IP Flow Verify en Azure Network Watcher con la CLI de Azure | Microsoft Docs"
description: "En este artículo se describe cómo comprobar si se permite o se deniega el tráfico hacia o desde una máquina virtual con la CLI de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c5fe6c662b3ee2a443904b0f12cbfd495d9bc85e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="34610-103">Compruebe si se permite o se deniega el tráfico hacia o desde una máquina virtual con IP Flow Verify, un componente de Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="34610-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="34610-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="34610-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="34610-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="34610-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="34610-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="34610-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="34610-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="34610-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="34610-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="34610-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="34610-109">Comprobación del flujo de IP es una característica de Network Watcher que permite comprobar si se permite el tráfico hacia o desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="34610-109">IP Flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="34610-110">Este escenario es útil para averiguar si una máquina virtual puede comunicarse con un recurso externo o con un back-end.</span><span class="sxs-lookup"><span data-stu-id="34610-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="34610-111">Comprobación del flujo de IP se puede usar para comprobar si las reglas de grupos de seguridad de red (NSG) se han configurado correctamente y solucionar los problemas de flujos que las reglas de NSG bloquean.</span><span class="sxs-lookup"><span data-stu-id="34610-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="34610-112">Otra razón para usar la Comprobación del flujo de IP es asegurarse de que el NSG está bloqueando correctamente el tráfico que quiere bloquear.</span><span class="sxs-lookup"><span data-stu-id="34610-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

<span data-ttu-id="34610-113">En este artículo, se utiliza la multiplataforma Azure CLI 1.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="34610-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="34610-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="34610-114">Before you begin</span></span>

<span data-ttu-id="34610-115">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create a Network Watcher](network-watcher-create.md) (Creación de una instancia de Network Watcher) o que ya tiene una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="34610-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="34610-116">En este escenario también se da por hecho que existe un grupo de recursos con una máquina virtual válida.</span><span class="sxs-lookup"><span data-stu-id="34610-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="34610-117">Escenario</span><span class="sxs-lookup"><span data-stu-id="34610-117">Scenario</span></span>

<span data-ttu-id="34610-118">Este escenario utiliza IP Flow Verify para comprobar si una máquina virtual pueden comunicarse con una dirección IP de Bing conocida.</span><span class="sxs-lookup"><span data-stu-id="34610-118">This scenario uses IP Flow Verify to verify if a virtual machine can talk to a known Bing IP address.</span></span> <span data-ttu-id="34610-119">Si se deniega el tráfico, devuelve la regla de seguridad que está denegando ese tráfico.</span><span class="sxs-lookup"><span data-stu-id="34610-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="34610-120">Para más información sobre IP Flow Verify, consulte la [introducción a IP Flow Verify](network-watcher-ip-flow-verify-overview.md).</span><span class="sxs-lookup"><span data-stu-id="34610-120">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>


## <a name="get-a-vm"></a><span data-ttu-id="34610-121">Obtención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="34610-121">Get a VM</span></span>

<span data-ttu-id="34610-122">La Comprobación del flujo de IP comprueba el tráfico hacia o desde la dirección IP de una máquina virtual, hacia o desde un destino remoto.</span><span class="sxs-lookup"><span data-stu-id="34610-122">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span></span> <span data-ttu-id="34610-123">Se necesita el identificador de una máquina virtual para ejecutar el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="34610-123">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="34610-124">Si ya conoce el identificador de la máquina virtual que se va a usar, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="34610-124">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-the-nics"></a><span data-ttu-id="34610-125">Obtención de las NIC</span><span class="sxs-lookup"><span data-stu-id="34610-125">Get the NICS</span></span>

<span data-ttu-id="34610-126">Se necesita la dirección IP de una NIC en la máquina virtual; en este ejemplo, se recuperan las NIC de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="34610-126">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="34610-127">Si ya conoce la dirección IP que desea probar en la máquina virtual, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="34610-127">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="34610-128">Ejecución de la Comprobación del flujo de IP</span><span class="sxs-lookup"><span data-stu-id="34610-128">Run IP flow verify</span></span>

<span data-ttu-id="34610-129">Ahora que tenemos la información necesaria para ejecutar el cmdlet `network watcher ip-flow-verify`, lo ejecutamos para comprobar el tráfico.</span><span class="sxs-lookup"><span data-stu-id="34610-129">Now that we have the information needed to run the cmdlet, we run the `network watcher ip-flow-verify` cmdlet to test the traffic.</span></span> <span data-ttu-id="34610-130">En este ejemplo, usamos la primera dirección IP en la primera NIC.</span><span class="sxs-lookup"><span data-stu-id="34610-130">In this example, we are using the first IP address on the first NIC.</span></span>

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> <span data-ttu-id="34610-131">Comprobación del flujo de IP requiere que el recurso de máquina virtual esté asignado para ejecución.</span><span class="sxs-lookup"><span data-stu-id="34610-131">IP Flow verify requires that the VM resource is allocated to run.</span></span>

## <a name="review-results"></a><span data-ttu-id="34610-132">Revisión de los resultados</span><span class="sxs-lookup"><span data-stu-id="34610-132">Review Results</span></span>

<span data-ttu-id="34610-133">Después de ejecutar `network watcher ip-flow-verify`, se devuelven los resultados. Los siguientes son los resultados devueltos por el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="34610-133">After running `network watcher ip-flow-verify` the results are returned, the following example is the results returned from the preceding step.</span></span>

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a><span data-ttu-id="34610-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34610-134">Next steps</span></span>

<span data-ttu-id="34610-135">Si se está bloqueando el tráfico y no debería ser así, consulte [Administración de grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para realizar un seguimiento del grupo de seguridad de red y de las reglas de seguridad definidas.</span><span class="sxs-lookup"><span data-stu-id="34610-135">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

<span data-ttu-id="34610-136">Para más información sobre cómo auditar la configuración de NSG, consulte [Automate NSG auditing with Azure Network Watcher Security group view](network-watcher-nsg-auditing-powershell.md) (Automatización de la auditoría de grupos de seguridad de red (NSG) con la vista de grupos de seguridad de Azure Network Watcher).</span><span class="sxs-lookup"><span data-stu-id="34610-136">Learn to audit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
