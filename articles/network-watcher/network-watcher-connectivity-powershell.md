---
title: 'conectividad de aaaCheck con Monitor de red de Azure: PowerShell | Documentos de Microsoft'
description: "Esta página se explica cómo tootest conectividad con Monitor de red con PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 4bcb90a72f178445c38b7bd7fc5054c5d0c200bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="10767-103">Comprobación de la conectividad con Azure Network Watcher mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="10767-103">Check connectivity with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="10767-104">Portal</span><span class="sxs-lookup"><span data-stu-id="10767-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="10767-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="10767-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="10767-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="10767-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="10767-107">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="10767-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="10767-108">Obtenga información acerca de cómo se puede establecer toouse conectividad tooverify si una conexión TCP directa de una tooa de máquina virtual tiene el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="10767-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="10767-109">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="10767-109">Before you begin</span></span>

<span data-ttu-id="10767-110">En este artículo se supone que tiene Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="10767-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="10767-111">Una instancia del Monitor de red en la región de Hola que desea toocheck conectividad.</span><span class="sxs-lookup"><span data-stu-id="10767-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="10767-112">Conectividad de toocheck de máquinas virtuales con.</span><span class="sxs-lookup"><span data-stu-id="10767-112">Virtual machines toocheck connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="10767-113">La comprobación de conectividad requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="10767-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="10767-114">Para instalar la extensión de hello en una máquina virtual de Windows, visite [extensión de máquina virtual de agente de Monitor de red de Azure para Windows](../virtual-machines/windows/extensions-nwa.md) y para la visita de VM de Linux [extensión de máquina virtual de agente de Monitor de red de Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="10767-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="10767-115">Registrar capacidades de vista previa de Hola</span><span class="sxs-lookup"><span data-stu-id="10767-115">Register hello preview capability</span></span>

<span data-ttu-id="10767-116">Conectividad está actualmente en versión preliminar pública, toouse esta característica necesita toobe registrado.</span><span class="sxs-lookup"><span data-stu-id="10767-116">Connectivity is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="10767-117">toodo, ejecución Hola siguiendo el ejemplo de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="10767-117">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="10767-118">registro de hello tooverify fue correcto, ejecute hello siguiendo el ejemplo de Powershell:</span><span class="sxs-lookup"><span data-stu-id="10767-118">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="10767-119">Si se ha registrado correctamente la característica de hello, salida de hello debe coincidir con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="10767-119">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName         ProviderName      RegistrationState
-----------         ------------      -----------------
AllowNetworkWatcherConnectivityCheck  Microsoft.Network Registered
```

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="10767-120">Compruebe la conectividad tooa virtual machine</span><span class="sxs-lookup"><span data-stu-id="10767-120">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="10767-121">Este ejemplo comprueba la máquina virtual de conectividad tooa destino en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="10767-121">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="10767-122">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="10767-122">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"
$destVMName = "Database0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName
$VM2 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $destVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationId $VM2.Id -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="10767-123">Response</span><span class="sxs-lookup"><span data-stu-id="10767-123">Response</span></span>

<span data-ttu-id="10767-124">Hola después de la respuesta es del anterior ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="10767-124">hello following response is from hello previous example.</span></span>  <span data-ttu-id="10767-125">En esta respuesta, Hola `ConnectionStatus` es **inaccesible**.</span><span class="sxs-lookup"><span data-stu-id="10767-125">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="10767-126">Puede ver que Hola a todos los sondeos errores de envío.</span><span class="sxs-lookup"><span data-stu-id="10767-126">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="10767-127">no se pudo conectividad Hello en dispositivo virtual Hola due tooa configurada por el usuario `NetworkSecurityRule` denominado **UserRule_Port80**, configurado tooblock el tráfico entrante en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="10767-127">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="10767-128">Esta información puede ser problemas de conexión de tooresearch usado.</span><span class="sxs-lookup"><span data-stu-id="10767-128">This information can be used tooresearch connection issues.</span></span>

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "c5222ea0-3213-4f85-a642-cee63217c2f3",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurat
                   ions/ipconfig1",
                       "NextHopIds": [
                         "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "9283a9f0-cc5e-4239-8f5e-ae0f3c19fbaa",
                       "Address": "10.1.2.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "0f1500cd-c512-4d43-b431-7267e4e67017"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "VirtualAppliance",
                       "Id": "0f1500cd-c512-4d43-b431-7267e4e67017",
                       "Address": "10.1.3.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfiguratio
                   ns/ipconfig1",
                       "NextHopIds": [
                         "a88940f8-5fbe-40da-8d99-1dee89240f64"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "NetworkSecurityRule",
                           "Context": [
                             {
                               "key": "RuleName",
                               "value": "UserRule_Port80"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "VnetLocal",
                       "Id": "a88940f8-5fbe-40da-8d99-1dee89240f64",
                       "Address": "10.1.4.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGrou
                   ps/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurati
                   ons/ipconfig1",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="validate-routing-issues"></a><span data-ttu-id="10767-129">Problemas de validación de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="10767-129">Validate routing issues</span></span>

<span data-ttu-id="10767-130">ejemplo de Hola comprueba la conectividad entre una máquina virtual y un extremo remoto.</span><span class="sxs-lookup"><span data-stu-id="10767-130">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="10767-131">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="10767-131">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress 13.107.21.200 -DestinationPort 80
```

### <a name="response"></a><span data-ttu-id="10767-132">Response</span><span class="sxs-lookup"><span data-stu-id="10767-132">Response</span></span>

<span data-ttu-id="10767-133">En el siguiente ejemplo de Hola Hola `ConnectionStatus` se muestra como **inaccesible**.</span><span class="sxs-lookup"><span data-stu-id="10767-133">In hello following example, hello `ConnectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="10767-134">Hola `Hops` obtener más información, consulte en `Issues` que se bloqueó el tráfico de hello due tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="10767-134">In hello `Hops` details, you can see under `Issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span> 

```
ConnectionStatus : Unreachable
AvgLatencyInMs   : 
MinLatencyInMs   : 
MaxLatencyInMs   : 
ProbesSent       : 100
ProbesFailed     : 100
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "b4f7bceb-07a3-44ca-8bae-adec6628225f",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "3fee8adf-692f-4523-b742-f6fdf6da6584"
                       ],
                       "Issues": [
                         {
                           "Origin": "Outbound",
                           "Severity": "Error",
                           "Type": "UserDefinedRoute",
                           "Context": [
                             {
                               "key": "RouteType",
                               "value": "User"
                             }
                           ]
                         }
                       ]
                     },
                     {
                       "Type": "Destination",
                       "Id": "3fee8adf-692f-4523-b742-f6fdf6da6584",
                       "Address": "13.107.21.200",
                       "ResourceId": "Unknown",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-website-latency"></a><span data-ttu-id="10767-135">Comprobación de la latencia del sitio web</span><span class="sxs-lookup"><span data-stu-id="10767-135">Check website latency</span></span>

<span data-ttu-id="10767-136">Hello en el ejemplo siguiente se busca en hello conectividad tooa sitio Web.</span><span class="sxs-lookup"><span data-stu-id="10767-136">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="10767-137">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="10767-137">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress http://bing.com/
```

### <a name="response"></a><span data-ttu-id="10767-138">Response</span><span class="sxs-lookup"><span data-stu-id="10767-138">Response</span></span>

<span data-ttu-id="10767-139">Hola después de respuesta, puede ver hello `ConnectionStatus` se muestra como **alcanzable**.</span><span class="sxs-lookup"><span data-stu-id="10767-139">In hello following response, you can see hello `ConnectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="10767-140">Cuando una conexión se establece correctamente, se proporcionan los valores de latencia.</span><span class="sxs-lookup"><span data-stu-id="10767-140">When a connection is successful, latency values are provided.</span></span>

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 7
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "1f0e3415-27b0-4bf7-a59d-3e19fb854e3e",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "f99f2bd1-42e8-4bbf-85b6-5d21d00c84e0",
                       "Address": "204.79.197.200",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="10767-141">Compruebe el punto de conexión de almacenamiento de tooa de conectividad</span><span class="sxs-lookup"><span data-stu-id="10767-141">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="10767-142">Hola de ejemplo siguiente prueba la conectividad de Hola desde una cuenta de almacenamiento de máquina virtual tooa blog.</span><span class="sxs-lookup"><span data-stu-id="10767-142">hello following example tests hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="10767-143">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="10767-143">Example</span></span>

```powershell
$rgName = "ContosoRG"
$sourceVMName = "MultiTierApp0"

$RG = Get-AzureRMResourceGroup -Name $rgName

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $RG.Location }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

$VM1 = Get-AzureRMVM -ResourceGroupName $rgName | Where-Object -Property Name -EQ $sourceVMName

Test-AzureRmNetworkWatcherConnectivity -NetworkWatcher $networkWatcher -SourceId $VM1.Id -DestinationAddress https://contosostorageexample.blob.core.windows.net/ 
```

### <a name="response"></a><span data-ttu-id="10767-144">Response</span><span class="sxs-lookup"><span data-stu-id="10767-144">Response</span></span>

<span data-ttu-id="10767-145">Hola siguiente json es respuesta de ejemplo de Hola de ejecución del cmdlet anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="10767-145">hello following json is hello example response from running hello previous cmdlet.</span></span> <span data-ttu-id="10767-146">Como el destino de hello es accesible, Hola `ConnectionStatus` propiedad se muestra como **alcanzable**.</span><span class="sxs-lookup"><span data-stu-id="10767-146">As hello destination is reachable, hello `ConnectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="10767-147">Se proporcionan detalles de hello sobre Hola número de saltos necesarios tooreach Hola almacenamiento de blobs y la latencia.</span><span class="sxs-lookup"><span data-stu-id="10767-147">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```
ConnectionStatus : Reachable
AvgLatencyInMs   : 1
MinLatencyInMs   : 0
MaxLatencyInMs   : 8
ProbesSent       : 100
ProbesFailed     : 0
Hops             : [
                     {
                       "Type": "Source",
                       "Id": "9e7f61d9-fb45-41db-83e2-c815a919b8ed",
                       "Address": "10.1.1.4",
                       "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
                       "NextHopIds": [
                         "1e6d4b3c-7964-4afd-b959-aaa746ee0f15"
                       ],
                       "Issues": []
                     },
                     {
                       "Type": "Internet",
                       "Id": "1e6d4b3c-7964-4afd-b959-aaa746ee0f15",
                       "Address": "13.71.200.248",
                       "ResourceId": "Internet",
                       "NextHopIds": [],
                       "Issues": []
                     }
                   ]
```

## <a name="next-steps"></a><span data-ttu-id="10767-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="10767-148">Next steps</span></span>

<span data-ttu-id="10767-149">Para comprobar si se permite cierto tráfico hacia o desde la máquina virtual, vea cómo [consultar la Comprobación del flujo de IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="10767-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<span data-ttu-id="10767-150">Si se está bloqueando el tráfico y no debe ser, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hacia abajo Hola red seguridad y el grupo de reglas de seguridad que se definen.</span><span class="sxs-lookup"><span data-stu-id="10767-150">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<!-- Image references -->














