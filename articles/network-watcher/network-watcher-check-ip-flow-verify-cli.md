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
ms.openlocfilehash: 0b52257a6c38a4392573672b7190d2269c2f145a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="8a826-103">Compruebe si se permite o se deniega el tráfico hacia o desde una máquina virtual con IP Flow Verify, un componente de Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="8a826-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8a826-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8a826-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="8a826-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a826-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="8a826-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8a826-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="8a826-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8a826-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="8a826-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="8a826-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="8a826-109">Comprobación del flujo de IP es una característica de Network Watcher que permite comprobar si se permite el tráfico hacia o desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8a826-109">IP Flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="8a826-110">Este escenario es útil para averiguar si una máquina virtual puede comunicarse con un recurso externo o con un back-end.</span><span class="sxs-lookup"><span data-stu-id="8a826-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="8a826-111">Comprobación del flujo de IP se puede usar para comprobar si las reglas de grupos de seguridad de red (NSG) se han configurado correctamente y solucionar los problemas de flujos que las reglas de NSG bloquean.</span><span class="sxs-lookup"><span data-stu-id="8a826-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="8a826-112">Otra razón para usar la Comprobación del flujo de IP es asegurarse de que el NSG está bloqueando correctamente el tráfico que quiere bloquear.</span><span class="sxs-lookup"><span data-stu-id="8a826-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

<span data-ttu-id="8a826-113">En este artículo se usa la CLI de próxima generación para el modelo de implementación de Resource Manager, la CLI de Azure 2.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="8a826-113">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="8a826-114">Para seguir los pasos de este artículo, es preciso [instalar la interfaz de la línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="8a826-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8a826-115">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="8a826-115">Before you begin</span></span>

<span data-ttu-id="8a826-116">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create a Network Watcher](network-watcher-create.md) (Creación de una instancia de Network Watcher) o que ya tiene una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="8a826-116">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="8a826-117">En este escenario también se da por hecho que existe un grupo de recursos con una máquina virtual válida.</span><span class="sxs-lookup"><span data-stu-id="8a826-117">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="8a826-118">Escenario</span><span class="sxs-lookup"><span data-stu-id="8a826-118">Scenario</span></span>

<span data-ttu-id="8a826-119">Este escenario utiliza IP Flow Verify para comprobar si una máquina virtual pueden comunicarse con una dirección IP de Bing conocida.</span><span class="sxs-lookup"><span data-stu-id="8a826-119">This scenario uses IP Flow Verify to verify if a virtual machine can talk to a known Bing IP address.</span></span> <span data-ttu-id="8a826-120">Si se deniega el tráfico, devuelve la regla de seguridad que está denegando ese tráfico.</span><span class="sxs-lookup"><span data-stu-id="8a826-120">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="8a826-121">Para más información sobre IP Flow Verify, consulte la [introducción a IP Flow Verify](network-watcher-ip-flow-verify-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8a826-121">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="8a826-122">Obtención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8a826-122">Get a VM</span></span>

<span data-ttu-id="8a826-123">La Comprobación del flujo de IP comprueba el tráfico hacia o desde la dirección IP de una máquina virtual, hacia o desde un destino remoto.</span><span class="sxs-lookup"><span data-stu-id="8a826-123">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span></span> <span data-ttu-id="8a826-124">Se necesita el identificador de una máquina virtual para ejecutar el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8a826-124">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="8a826-125">Si ya conoce el identificador de la máquina virtual que se va a usar, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="8a826-125">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-the-nics"></a><span data-ttu-id="8a826-126">Obtención de las NIC</span><span class="sxs-lookup"><span data-stu-id="8a826-126">Get the NICS</span></span>

<span data-ttu-id="8a826-127">Se necesita la dirección IP de una NIC en la máquina virtual; en este ejemplo, se recuperan las NIC de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8a826-127">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="8a826-128">Si ya conoce la dirección IP que desea probar en la máquina virtual, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="8a826-128">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="8a826-129">Ejecución de la Comprobación del flujo de IP</span><span class="sxs-lookup"><span data-stu-id="8a826-129">Run IP flow verify</span></span>

<span data-ttu-id="8a826-130">Ahora que tenemos la información necesaria para ejecutar el cmdlet `az network watcher test-ip-flow`, lo ejecutamos para comprobar el tráfico.</span><span class="sxs-lookup"><span data-stu-id="8a826-130">Now that we have the information needed to run the cmdlet, we run the `az network watcher test-ip-flow` cmdlet to test the traffic.</span></span> <span data-ttu-id="8a826-131">En este ejemplo, usamos la primera dirección IP en la primera NIC.</span><span class="sxs-lookup"><span data-stu-id="8a826-131">In this example, we are using the first IP address on the first NIC.</span></span>

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> <span data-ttu-id="8a826-132">Comprobación del flujo de IP requiere que el recurso de máquina virtual esté asignado para ejecución.</span><span class="sxs-lookup"><span data-stu-id="8a826-132">IP Flow verify requires that the VM resource is allocated to run.</span></span>

## <a name="review-results"></a><span data-ttu-id="8a826-133">Revisión de los resultados</span><span class="sxs-lookup"><span data-stu-id="8a826-133">Review Results</span></span>

<span data-ttu-id="8a826-134">Después de ejecutar `az network watcher test-ip-flow`, se devuelven los resultados. Los siguientes son los resultados devueltos por el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="8a826-134">After running `az network watcher test-ip-flow` the results are returned, the following example is the results returned from the preceding step.</span></span>

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a><span data-ttu-id="8a826-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8a826-135">Next steps</span></span>

<span data-ttu-id="8a826-136">Si se está bloqueando el tráfico y no debería ser así, consulte [Administración de grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para realizar un seguimiento del grupo de seguridad de red y de las reglas de seguridad definidas.</span><span class="sxs-lookup"><span data-stu-id="8a826-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

<span data-ttu-id="8a826-137">Para más información sobre cómo auditar la configuración de NSG, consulte [Automate NSG auditing with Azure Network Watcher Security group view](network-watcher-nsg-auditing-powershell.md) (Automatización de la auditoría de grupos de seguridad de red (NSG) con la vista de grupos de seguridad de Azure Network Watcher).</span><span class="sxs-lookup"><span data-stu-id="8a826-137">Learn to audit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
