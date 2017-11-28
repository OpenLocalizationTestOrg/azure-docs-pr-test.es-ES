---
title: "Comprobación del tráfico con la Comprobación del flujo de IP de Azure Network Watcher con REST | Microsoft Docs"
description: "En este artículo se describe cómo comprobar si se permite o se deniega el tráfico hacia o desde una máquina virtual"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 6d3ce00a7d4f9c0cd57fa8815625a1065b03b5b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="72b6c-103">Comprobar si se permite o se deniega el tráfico con la Comprobación del flujo de IP, un componente de Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="72b6c-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="72b6c-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="72b6c-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="72b6c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="72b6c-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="72b6c-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="72b6c-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="72b6c-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="72b6c-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="72b6c-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="72b6c-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="72b6c-109">La Comprobación del flujo de IP es una característica de Network Watcher que permite comprobar si se permite el tráfico hacia o desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="72b6c-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="72b6c-110">Se puede ejecutar la validación para el tráfico entrante o saliente.</span><span class="sxs-lookup"><span data-stu-id="72b6c-110">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="72b6c-111">Este escenario es útil para averiguar si una máquina virtual puede comunicarse con un recurso externo o con un back-end.</span><span class="sxs-lookup"><span data-stu-id="72b6c-111">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="72b6c-112">Comprobación del flujo de IP se puede usar para comprobar si las reglas de grupos de seguridad de red (NSG) se han configurado correctamente y solucionar los problemas de flujos que las reglas de NSG bloquean.</span><span class="sxs-lookup"><span data-stu-id="72b6c-112">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="72b6c-113">Otra razón para usar la Comprobación del flujo de IP es asegurarse de que el NSG está bloqueando correctamente el tráfico que quiere bloquear.</span><span class="sxs-lookup"><span data-stu-id="72b6c-113">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="72b6c-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="72b6c-114">Before you begin</span></span>

<span data-ttu-id="72b6c-115">ARMclient se usa para llamar a la API de REST con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72b6c-115">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="72b6c-116">ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="72b6c-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="72b6c-117">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create an Azure Network Watcher instance](network-watcher-create.md) (Creación de una instancia de Azure Network Watcher) para crear una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="72b6c-117">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="72b6c-118">Escenario</span><span class="sxs-lookup"><span data-stu-id="72b6c-118">Scenario</span></span>

<span data-ttu-id="72b6c-119">Este escenario usa la Comprobación del flujo de IP para verificar si una máquina virtual puede comunicarse con otra a través del puerto 443.</span><span class="sxs-lookup"><span data-stu-id="72b6c-119">This scenario uses IP flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="72b6c-120">Si se deniega el tráfico, devuelve la regla de seguridad que está denegando ese tráfico.</span><span class="sxs-lookup"><span data-stu-id="72b6c-120">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="72b6c-121">Para más información sobre la Comprobación del flujo de IP, vea [Introducción a la comprobación del flujo de IP](network-watcher-ip-flow-verify-overview.md).</span><span class="sxs-lookup"><span data-stu-id="72b6c-121">To learn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="72b6c-122">En este escenario, podrá:</span><span class="sxs-lookup"><span data-stu-id="72b6c-122">In this scenario, you:</span></span>

* <span data-ttu-id="72b6c-123">Recuperación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="72b6c-123">Retrieve a virtual machine</span></span>
* <span data-ttu-id="72b6c-124">Llamar a la Comprobación del flujo de IP</span><span class="sxs-lookup"><span data-stu-id="72b6c-124">Call IP flow verify</span></span>
* <span data-ttu-id="72b6c-125">Comprobar los resultados</span><span class="sxs-lookup"><span data-stu-id="72b6c-125">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="72b6c-126">Inicio de sesión con ARMClient</span><span class="sxs-lookup"><span data-stu-id="72b6c-126">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="72b6c-127">Recuperación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="72b6c-127">Retrieve a virtual machine</span></span>

<span data-ttu-id="72b6c-128">Ejecute el siguiente script para devolver una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="72b6c-128">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="72b6c-129">El siguiente código necesita valores para las variables:</span><span class="sxs-lookup"><span data-stu-id="72b6c-129">The following code needs values for the variables:</span></span>

* <span data-ttu-id="72b6c-130">**subscriptionId**: el identificador de suscripción que se usa.</span><span class="sxs-lookup"><span data-stu-id="72b6c-130">**subscriptionId** - The subscription Id to use.</span></span>
* <span data-ttu-id="72b6c-131">**resourceGroupName**: el nombre de un grupo de recursos que contiene máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="72b6c-131">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="72b6c-132">La información que se necesita es el identificador del tipo `Microsoft.Compute/virtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="72b6c-132">The information that is needed is the id under the type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="72b6c-133">Los resultados deberían parecerse al siguiente código de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="72b6c-133">The results should be similar to the following code sample:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a><span data-ttu-id="72b6c-134">Llamar a la Comprobación del flujo de IP</span><span class="sxs-lookup"><span data-stu-id="72b6c-134">Call IP flow Verify</span></span>

<span data-ttu-id="72b6c-135">En el ejemplo siguiente se crea una solicitud para comprobar el tráfico de una máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="72b6c-135">The following example creates a request to verify the traffic for a specified virtual machine.</span></span> <span data-ttu-id="72b6c-136">La respuesta se devuelve si se permite el tráfico o si se deniega el tráfico.</span><span class="sxs-lookup"><span data-stu-id="72b6c-136">The response returns if the traffic is allowed or if the traffic is denied.</span></span> <span data-ttu-id="72b6c-137">Si se deniega el tráfico, también devuelve la regla que bloquea el tráfico.</span><span class="sxs-lookup"><span data-stu-id="72b6c-137">If traffic is denied it also returns what rule blocks the traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="72b6c-138">La Comprobación del flujo de IP requiere que el recurso de máquina virtual esté asignado.</span><span class="sxs-lookup"><span data-stu-id="72b6c-138">IP flow verify requires that the VM resource is allocated.</span></span>

<span data-ttu-id="72b6c-139">El script requiere el identificador de recurso de una máquina virtual y de una tarjeta de interfaz de red en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="72b6c-139">The script requires the resource Id of a virtual machine and of a network interface card on the virtual machine.</span></span> <span data-ttu-id="72b6c-140">Estos valores los proporciona la salida anterior.</span><span class="sxs-lookup"><span data-stu-id="72b6c-140">These values are provided by the preceding output.</span></span>

> [!Important]
> <span data-ttu-id="72b6c-141">En todas las llamadas a la REST de Network Watcher, el nombre del grupo de recursos del identificador URI de la solicitud es el que contiene la instancia de Network Watcher, no los recursos sobre los que realiza las acciones de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="72b6c-141">For all Network Watcher REST calls the resource group name in the request URI is the one that contains the Network Watcher instance, not the resources you are performing the diagnostic actions on.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-the-results"></a><span data-ttu-id="72b6c-142">Descripción de los resultados</span><span class="sxs-lookup"><span data-stu-id="72b6c-142">Understanding the results</span></span>

<span data-ttu-id="72b6c-143">La respuesta que recibe indica si el tráfico se permite o deniega.</span><span class="sxs-lookup"><span data-stu-id="72b6c-143">The response you get back tells you whether the traffic is allowed or denied.</span></span> <span data-ttu-id="72b6c-144">La respuesta es similar a uno de los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="72b6c-144">The response looks like one of the following examples:</span></span>

<span data-ttu-id="72b6c-145">**Se permite**</span><span class="sxs-lookup"><span data-stu-id="72b6c-145">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="72b6c-146">**Se deniega**</span><span class="sxs-lookup"><span data-stu-id="72b6c-146">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="72b6c-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="72b6c-147">Next steps</span></span>

<span data-ttu-id="72b6c-148">Si el tráfico sufre bloqueos, y no debería ser así, consulte [Administración de grupos de seguridad de red mediante el portal](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para más información acerca de los grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="72b6c-148">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to learn more about Network Security Groups.</span></span>












