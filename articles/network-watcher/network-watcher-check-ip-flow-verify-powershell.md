---
title: "tráfico de aaaverify con flujo de IP de Monitor de red de Azure Compruebe - PowerShell | Documentos de Microsoft"
description: "Este artículo se describe cómo toocheck si tooor de tráfico de una máquina virtual se permite o deniega con PowerShell"
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
ms.openlocfilehash: 924da1de1bd554e15816886f8e51d7f170f0e7ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="2a80d-103">Compruebe si el tráfico se permitirá o denegará tooor de una máquina virtual con el flujo de IP compruebe un componente de Monitor de red de Azure</span><span class="sxs-lookup"><span data-stu-id="2a80d-103">Check if traffic is allowed or denied tooor from a VM with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2a80d-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="2a80d-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="2a80d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a80d-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="2a80d-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2a80d-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="2a80d-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2a80d-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="2a80d-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="2a80d-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="2a80d-109">Flujo IP comprobar es una característica de Monitor de red que le permite tooverify si se permite el tráfico tooor desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2a80d-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="2a80d-110">Este escenario es útil tooget un estado actual del si una máquina virtual puede comunicarse un recurso externo tooan o back-end.</span><span class="sxs-lookup"><span data-stu-id="2a80d-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="2a80d-111">Flujo IP comprobar puede ser usado tooverify si las reglas del grupo de seguridad de red (NSG) se han configurado correctamente y solucionar los problemas flujos que se bloquean las reglas de NSG.</span><span class="sxs-lookup"><span data-stu-id="2a80d-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="2a80d-112">Otra razón para usar IP flujo Compruebe es que quiera bloquear el tráfico de tooensure está bloqueando correctamente hello NSG.</span><span class="sxs-lookup"><span data-stu-id="2a80d-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2a80d-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="2a80d-113">Before you begin</span></span>

<span data-ttu-id="2a80d-114">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red o tiene una instancia existente de Monitor de red.</span><span class="sxs-lookup"><span data-stu-id="2a80d-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="2a80d-115">escenario de Hello también supone que un grupo de recursos con una máquina virtual válida existe toobe usa.</span><span class="sxs-lookup"><span data-stu-id="2a80d-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="2a80d-116">Escenario</span><span class="sxs-lookup"><span data-stu-id="2a80d-116">Scenario</span></span>

<span data-ttu-id="2a80d-117">Este flujo de escenario usa IP comprobar tooverify si una máquina virtual puede comunicarse conocidos tooa dirección IP de Bing.</span><span class="sxs-lookup"><span data-stu-id="2a80d-117">This scenario uses IP flow verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="2a80d-118">Si se deniega el tráfico de hello, devuelve la regla de seguridad de Hola que deniega ese tráfico.</span><span class="sxs-lookup"><span data-stu-id="2a80d-118">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="2a80d-119">más información sobre el flujo IP comprobar, visite toolearn [flujo IP comprobar información general](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2a80d-119">toolearn more about IP flow verify, visit [IP flow verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="2a80d-120">Recuperación de Network Watcher</span><span class="sxs-lookup"><span data-stu-id="2a80d-120">Retrieve Network Watcher</span></span>

<span data-ttu-id="2a80d-121">Hola primer paso es instancia de Monitor de red de tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="2a80d-121">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="2a80d-122">Hola `$networkWatcher` pasa una variable toohello IP flujo comprobar cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2a80d-122">hello `$networkWatcher` variable is passed toohello IP flow verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="2a80d-123">Obtención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2a80d-123">Get a VM</span></span>

<span data-ttu-id="2a80d-124">Flujo IP Compruebe tooor de tráfico de pruebas desde una dirección IP en un tooor de máquina virtual de un destino remoto.</span><span class="sxs-lookup"><span data-stu-id="2a80d-124">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="2a80d-125">Un identificador de una máquina virtual se requiere para hello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2a80d-125">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="2a80d-126">Si ya conoce el identificador de Hola de hello toouse de máquina virtual, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="2a80d-126">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-hello-nics"></a><span data-ttu-id="2a80d-127">Obtener Hola NIC</span><span class="sxs-lookup"><span data-stu-id="2a80d-127">Get hello NICS</span></span>

<span data-ttu-id="2a80d-128">se necesita la dirección IP de Hola de una NIC en la máquina virtual de Hola, en este ejemplo recuperamos Hola NIC en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2a80d-128">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="2a80d-129">Si ya sabe Hola IP de direcciones que desea tootest en la máquina virtual de hello, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="2a80d-129">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="2a80d-130">Ejecución de la Comprobación del flujo de IP</span><span class="sxs-lookup"><span data-stu-id="2a80d-130">Run IP flow verify</span></span>

<span data-ttu-id="2a80d-131">Ahora que tenemos información Hola necesarios toorun Hola cmdlet, ejecutamos hello `Test-AzureRmNetworkWatcherIPFlow` tráfico de cmdlet tootest Hola.</span><span class="sxs-lookup"><span data-stu-id="2a80d-131">Now that we have hello information needed toorun hello cmdlet, we run hello `Test-AzureRmNetworkWatcherIPFlow` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="2a80d-132">En este ejemplo, estamos utilizando dirección IP de la primera hello en la NIC de hello primero.</span><span class="sxs-lookup"><span data-stu-id="2a80d-132">In this example, we are using hello first IP address on hello first NIC.</span></span>

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> <span data-ttu-id="2a80d-133">Flujo IP comprobar requiere que el recurso de máquina virtual de Hola se asigna toorun.</span><span class="sxs-lookup"><span data-stu-id="2a80d-133">IP flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="2a80d-134">Revisión de los resultados</span><span class="sxs-lookup"><span data-stu-id="2a80d-134">Review Results</span></span>

<span data-ttu-id="2a80d-135">Después de ejecutar `Test-AzureRmNetworkWatcherIPFlow` Hola resultados se devuelven, en el ejemplo siguiente se hello es Hola devuelva resultados de hello anterior paso.</span><span class="sxs-lookup"><span data-stu-id="2a80d-135">After running `Test-AzureRmNetworkWatcherIPFlow` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a><span data-ttu-id="2a80d-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2a80d-136">Next steps</span></span>

<span data-ttu-id="2a80d-137">Si se está bloqueando el tráfico y no debe ser, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hacia abajo Hola red seguridad y el grupo de reglas de seguridad que se definen.</span><span class="sxs-lookup"><span data-stu-id="2a80d-137">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













