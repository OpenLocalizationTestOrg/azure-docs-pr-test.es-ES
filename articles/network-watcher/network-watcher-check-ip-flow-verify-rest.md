---
title: "tráfico de aaaVerify con flujo de IP de Monitor de red de Azure Compruebe - REST | Documentos de Microsoft"
description: "Este artículo se describe cómo toocheck si se permite o deniega el tráfico tooor desde una máquina virtual"
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
ms.openlocfilehash: 956db0d326db597c6c402a9e8d4a5522c47c02d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="6dda4-103">Comprobar si se permite o se deniega el tráfico con la Comprobación del flujo de IP, un componente de Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="6dda4-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6dda4-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6dda4-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="6dda4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6dda4-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="6dda4-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6dda4-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="6dda4-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6dda4-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="6dda4-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="6dda4-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="6dda4-109">Flujo IP comprobar es una característica de Monitor de red que le permite tooverify si se permite el tráfico tooor desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6dda4-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="6dda4-110">validación de Hola se puede ejecutar para el tráfico entrante o saliente.</span><span class="sxs-lookup"><span data-stu-id="6dda4-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="6dda4-111">Este escenario es útil tooget un estado actual del si una máquina virtual puede comunicarse un recurso externo tooan o back-end.</span><span class="sxs-lookup"><span data-stu-id="6dda4-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="6dda4-112">Flujo IP comprobar puede ser usado tooverify si las reglas del grupo de seguridad de red (NSG) se han configurado correctamente y solucionar los problemas flujos que se bloquean las reglas de NSG.</span><span class="sxs-lookup"><span data-stu-id="6dda4-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="6dda4-113">Otra razón para usar IP flujo Compruebe es que quiera bloquear el tráfico de tooensure está bloqueando correctamente hello NSG.</span><span class="sxs-lookup"><span data-stu-id="6dda4-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6dda4-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="6dda4-114">Before you begin</span></span>

<span data-ttu-id="6dda4-115">ARMclient es la API de REST de hello toocall utilizados mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6dda4-115">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="6dda4-116">ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="6dda4-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="6dda4-117">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="6dda4-117">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="6dda4-118">Escenario</span><span class="sxs-lookup"><span data-stu-id="6dda4-118">Scenario</span></span>

<span data-ttu-id="6dda4-119">Este escenario utiliza IP flujo Compruebe tooverify si una máquina virtual puede comunicarse tooanother máquina a través del puerto 443.</span><span class="sxs-lookup"><span data-stu-id="6dda4-119">This scenario uses IP flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="6dda4-120">Si se deniega el tráfico de hello, devuelve la regla de seguridad de Hola que deniega ese tráfico.</span><span class="sxs-lookup"><span data-stu-id="6dda4-120">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="6dda4-121">toolearn más información acerca del flujo IP Verify, visite [flujo IP comprobar información general](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="6dda4-121">toolearn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="6dda4-122">En este escenario, podrá:</span><span class="sxs-lookup"><span data-stu-id="6dda4-122">In this scenario, you:</span></span>

* <span data-ttu-id="6dda4-123">Recuperación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6dda4-123">Retrieve a virtual machine</span></span>
* <span data-ttu-id="6dda4-124">Llamar a la Comprobación del flujo de IP</span><span class="sxs-lookup"><span data-stu-id="6dda4-124">Call IP flow verify</span></span>
* <span data-ttu-id="6dda4-125">Comprobar los resultados</span><span class="sxs-lookup"><span data-stu-id="6dda4-125">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="6dda4-126">Inicio de sesión con ARMClient</span><span class="sxs-lookup"><span data-stu-id="6dda4-126">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="6dda4-127">Recuperación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6dda4-127">Retrieve a virtual machine</span></span>

<span data-ttu-id="6dda4-128">Ejecutar Hola después tooreturn de secuencia de comandos en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6dda4-128">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="6dda4-129">Hello siguiente código necesita valores para las variables de hello:</span><span class="sxs-lookup"><span data-stu-id="6dda4-129">hello following code needs values for hello variables:</span></span>

* <span data-ttu-id="6dda4-130">**Id. de suscripción** -Hola toouse de Id. de suscripción.</span><span class="sxs-lookup"><span data-stu-id="6dda4-130">**subscriptionId** - hello subscription Id toouse.</span></span>
* <span data-ttu-id="6dda4-131">**resourceGroupName** : hello nombre de un grupo de recursos que contiene máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6dda4-131">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="6dda4-132">información que se necesita Hello es Id. de hello en tipo hello `Microsoft.Compute/virtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="6dda4-132">hello information that is needed is hello id under hello type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="6dda4-133">resultados de Hello deberían ser similar toohello siguiendo el ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="6dda4-133">hello results should be similar toohello following code sample:</span></span>

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

## <a name="call-ip-flow-verify"></a><span data-ttu-id="6dda4-134">Llamar a la Comprobación del flujo de IP</span><span class="sxs-lookup"><span data-stu-id="6dda4-134">Call IP flow Verify</span></span>

<span data-ttu-id="6dda4-135">Hello en el ejemplo siguiente se crea un tráfico de hello tooverify de solicitud para una máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="6dda4-135">hello following example creates a request tooverify hello traffic for a specified virtual machine.</span></span> <span data-ttu-id="6dda4-136">respuesta de Hello devuelve si se permite el tráfico de Hola o si se deniega el tráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dda4-136">hello response returns if hello traffic is allowed or if hello traffic is denied.</span></span> <span data-ttu-id="6dda4-137">Si se deniega el tráfico también devuelve los bloques de reglas Hola tráfico.</span><span class="sxs-lookup"><span data-stu-id="6dda4-137">If traffic is denied it also returns what rule blocks hello traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="6dda4-138">Flujo IP comprobar requiere que se asigna el recurso de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dda4-138">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="6dda4-139">script de Hola requiere recursos Hola Id. de una máquina virtual y de una tarjeta de interfaz de red en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dda4-139">hello script requires hello resource Id of a virtual machine and of a network interface card on hello virtual machine.</span></span> <span data-ttu-id="6dda4-140">Estos valores se proporcionan con hello anterior de salida.</span><span class="sxs-lookup"><span data-stu-id="6dda4-140">These values are provided by hello preceding output.</span></span>

> [!Important]
> <span data-ttu-id="6dda4-141">Para el resto de Monitor de red llamadas Hola nombre de grupo de recursos en solicitud de hello que URI es hello uno que contiene la instancia del Monitor de red de hello, no se está realizando acciones de diagnóstico de hello en recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dda4-141">For all Network Watcher REST calls hello resource group name in hello request URI is hello one that contains hello Network Watcher instance, not hello resources you are performing hello diagnostic actions on.</span></span>

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

## <a name="understanding-hello-results"></a><span data-ttu-id="6dda4-142">Descripción de los resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="6dda4-142">Understanding hello results</span></span>

<span data-ttu-id="6dda4-143">respuesta de Hello que regresar indica si se permite o deniega el tráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="6dda4-143">hello response you get back tells you whether hello traffic is allowed or denied.</span></span> <span data-ttu-id="6dda4-144">respuesta de Hello es similar a uno de hello en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6dda4-144">hello response looks like one of hello following examples:</span></span>

<span data-ttu-id="6dda4-145">**Se permite**</span><span class="sxs-lookup"><span data-stu-id="6dda4-145">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="6dda4-146">**Se deniega**</span><span class="sxs-lookup"><span data-stu-id="6dda4-146">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="6dda4-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6dda4-147">Next steps</span></span>

<span data-ttu-id="6dda4-148">Si se está bloqueando el tráfico y no debe ser, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn más acerca de los grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="6dda4-148">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn more about Network Security Groups.</span></span>












