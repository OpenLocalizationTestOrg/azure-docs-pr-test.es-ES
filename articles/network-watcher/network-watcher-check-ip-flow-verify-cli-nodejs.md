---
title: "tráfico de aaaVerify con Azure red Monitor IP flujo comprobar - CLI de Azure | Documentos de Microsoft"
description: "Este artículo se describe cómo toocheck si tooor de tráfico de una máquina virtual se permite o deniega con CLI de Azure"
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
ms.openlocfilehash: c6becc5c142837b04d15490b2b3bd11124434570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="d235e-103">Compruebe si el tráfico se permitirá o denegará tooor de una máquina virtual con IP flujo comprobar un componente de Monitor de red de Azure</span><span class="sxs-lookup"><span data-stu-id="d235e-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d235e-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d235e-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="d235e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d235e-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="d235e-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d235e-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="d235e-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d235e-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="d235e-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="d235e-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="d235e-109">Flujo de IP comprobar es una característica de Monitor de red que le permite tooverify si se permite el tráfico tooor desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d235e-109">IP Flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="d235e-110">Este escenario es útil tooget un estado actual del si una máquina virtual puede comunicarse un recurso externo tooan o back-end.</span><span class="sxs-lookup"><span data-stu-id="d235e-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="d235e-111">Flujo IP comprobar puede ser usado tooverify si las reglas del grupo de seguridad de red (NSG) se han configurado correctamente y solucionar los problemas flujos que se bloquean las reglas de NSG.</span><span class="sxs-lookup"><span data-stu-id="d235e-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="d235e-112">Otra razón para usar IP flujo Compruebe es que quiera bloquear el tráfico de tooensure está bloqueando correctamente hello NSG.</span><span class="sxs-lookup"><span data-stu-id="d235e-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

<span data-ttu-id="d235e-113">En este artículo, se utiliza la multiplataforma Azure CLI 1.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="d235e-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d235e-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="d235e-114">Before you begin</span></span>

<span data-ttu-id="d235e-115">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red o tiene una instancia existente de Monitor de red.</span><span class="sxs-lookup"><span data-stu-id="d235e-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="d235e-116">escenario de Hello también supone que un grupo de recursos con una máquina virtual válida existe toobe usa.</span><span class="sxs-lookup"><span data-stu-id="d235e-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="d235e-117">Escenario</span><span class="sxs-lookup"><span data-stu-id="d235e-117">Scenario</span></span>

<span data-ttu-id="d235e-118">Este escenario usa tooverify IP flujo comprobar si una máquina virtual puede comunicarse conocidos tooa dirección IP de Bing.</span><span class="sxs-lookup"><span data-stu-id="d235e-118">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="d235e-119">Si se deniega el tráfico de hello, devuelve la regla de seguridad de Hola que deniega ese tráfico.</span><span class="sxs-lookup"><span data-stu-id="d235e-119">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="d235e-120">toolearn más información acerca de IP flujo comprobar, visite [Introducción comprobar flujo de IP](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d235e-120">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>


## <a name="get-a-vm"></a><span data-ttu-id="d235e-121">Obtención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="d235e-121">Get a VM</span></span>

<span data-ttu-id="d235e-122">Flujo IP Compruebe tooor de tráfico de pruebas desde una dirección IP en un tooor de máquina virtual de un destino remoto.</span><span class="sxs-lookup"><span data-stu-id="d235e-122">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="d235e-123">Un identificador de una máquina virtual se requiere para hello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d235e-123">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="d235e-124">Si ya conoce el identificador de Hola de hello toouse de máquina virtual, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="d235e-124">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-hello-nics"></a><span data-ttu-id="d235e-125">Obtener Hola NIC</span><span class="sxs-lookup"><span data-stu-id="d235e-125">Get hello NICS</span></span>

<span data-ttu-id="d235e-126">se necesita la dirección IP de Hola de una NIC en la máquina virtual de Hola, en este ejemplo recuperamos Hola NIC en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d235e-126">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="d235e-127">Si ya sabe Hola IP de direcciones que desea tootest en la máquina virtual de hello, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="d235e-127">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="d235e-128">Ejecución de la Comprobación del flujo de IP</span><span class="sxs-lookup"><span data-stu-id="d235e-128">Run IP flow verify</span></span>

<span data-ttu-id="d235e-129">Ahora que tenemos información Hola necesarios toorun Hola cmdlet, ejecutamos hello `network watcher ip-flow-verify` tráfico de cmdlet tootest Hola.</span><span class="sxs-lookup"><span data-stu-id="d235e-129">Now that we have hello information needed toorun hello cmdlet, we run hello `network watcher ip-flow-verify` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="d235e-130">En este ejemplo, estamos utilizando dirección IP de la primera hello en la NIC de hello primero.</span><span class="sxs-lookup"><span data-stu-id="d235e-130">In this example, we are using hello first IP address on hello first NIC.</span></span>

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> <span data-ttu-id="d235e-131">Flujo de IP comprobar requiere que el recurso de máquina virtual de Hola se asigna toorun.</span><span class="sxs-lookup"><span data-stu-id="d235e-131">IP Flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="d235e-132">Revisión de los resultados</span><span class="sxs-lookup"><span data-stu-id="d235e-132">Review Results</span></span>

<span data-ttu-id="d235e-133">Después de ejecutar `network watcher ip-flow-verify` Hola resultados se devuelven, en el ejemplo siguiente se hello es Hola devuelva resultados de hello anterior paso.</span><span class="sxs-lookup"><span data-stu-id="d235e-133">After running `network watcher ip-flow-verify` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a><span data-ttu-id="d235e-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d235e-134">Next steps</span></span>

<span data-ttu-id="d235e-135">Si se está bloqueando el tráfico y no debe ser, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hacia abajo Hola red seguridad y el grupo de reglas de seguridad que se definen.</span><span class="sxs-lookup"><span data-stu-id="d235e-135">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<span data-ttu-id="d235e-136">Obtenga información acerca de tooaudit la configuración de NSG visitando [auditoría red seguridad grupos (NSG) con el Monitor de red](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d235e-136">Learn tooaudit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
