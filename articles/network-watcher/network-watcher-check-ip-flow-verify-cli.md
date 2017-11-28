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
ms.openlocfilehash: 128a00b4296994551e7e17838a51e6d9de180e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="8f359-103">Compruebe si el tráfico se permitirá o denegará tooor de una máquina virtual con IP flujo comprobar un componente de Monitor de red de Azure</span><span class="sxs-lookup"><span data-stu-id="8f359-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8f359-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8f359-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="8f359-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f359-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="8f359-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8f359-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="8f359-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8f359-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="8f359-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="8f359-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="8f359-109">Flujo de IP comprobar es una característica de Monitor de red que le permite tooverify si se permite el tráfico tooor desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8f359-109">IP Flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="8f359-110">Este escenario es útil tooget un estado actual del si una máquina virtual puede comunicarse un recurso externo tooan o back-end.</span><span class="sxs-lookup"><span data-stu-id="8f359-110">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="8f359-111">Flujo IP comprobar puede ser usado tooverify si las reglas del grupo de seguridad de red (NSG) se han configurado correctamente y solucionar los problemas flujos que se bloquean las reglas de NSG.</span><span class="sxs-lookup"><span data-stu-id="8f359-111">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="8f359-112">Otra razón para usar IP flujo Compruebe es que quiera bloquear el tráfico de tooensure está bloqueando correctamente hello NSG.</span><span class="sxs-lookup"><span data-stu-id="8f359-112">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

<span data-ttu-id="8f359-113">En este artículo usa la CLI de próxima generación para el modelo de implementación de administración de recursos hello, CLI de Azure 2.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="8f359-113">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="8f359-114">Hola tooperform los pasos de este artículo, deberá demasiado[instalar Hola interfaz de línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="8f359-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8f359-115">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="8f359-115">Before you begin</span></span>

<span data-ttu-id="8f359-116">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red o tiene una instancia existente de Monitor de red.</span><span class="sxs-lookup"><span data-stu-id="8f359-116">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="8f359-117">escenario de Hello también supone que un grupo de recursos con una máquina virtual válida existe toobe usa.</span><span class="sxs-lookup"><span data-stu-id="8f359-117">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="8f359-118">Escenario</span><span class="sxs-lookup"><span data-stu-id="8f359-118">Scenario</span></span>

<span data-ttu-id="8f359-119">Este escenario usa tooverify IP flujo comprobar si una máquina virtual puede comunicarse conocidos tooa dirección IP de Bing.</span><span class="sxs-lookup"><span data-stu-id="8f359-119">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooa known Bing IP address.</span></span> <span data-ttu-id="8f359-120">Si se deniega el tráfico de hello, devuelve la regla de seguridad de Hola que deniega ese tráfico.</span><span class="sxs-lookup"><span data-stu-id="8f359-120">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="8f359-121">toolearn más información acerca de IP flujo comprobar, visite [Introducción comprobar flujo de IP](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8f359-121">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="8f359-122">Obtención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8f359-122">Get a VM</span></span>

<span data-ttu-id="8f359-123">Flujo IP Compruebe tooor de tráfico de pruebas desde una dirección IP en un tooor de máquina virtual de un destino remoto.</span><span class="sxs-lookup"><span data-stu-id="8f359-123">IP flow verify tests traffic tooor from an IP address on a virtual machine tooor from a remote destination.</span></span> <span data-ttu-id="8f359-124">Un identificador de una máquina virtual se requiere para hello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8f359-124">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="8f359-125">Si ya conoce el identificador de Hola de hello toouse de máquina virtual, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="8f359-125">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-hello-nics"></a><span data-ttu-id="8f359-126">Obtener Hola NIC</span><span class="sxs-lookup"><span data-stu-id="8f359-126">Get hello NICS</span></span>

<span data-ttu-id="8f359-127">se necesita la dirección IP de Hola de una NIC en la máquina virtual de Hola, en este ejemplo recuperamos Hola NIC en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8f359-127">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="8f359-128">Si ya sabe Hola IP de direcciones que desea tootest en la máquina virtual de hello, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="8f359-128">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="8f359-129">Ejecución de la Comprobación del flujo de IP</span><span class="sxs-lookup"><span data-stu-id="8f359-129">Run IP flow verify</span></span>

<span data-ttu-id="8f359-130">Ahora que tenemos información Hola necesarios toorun Hola cmdlet, ejecutamos hello `az network watcher test-ip-flow` tráfico de cmdlet tootest Hola.</span><span class="sxs-lookup"><span data-stu-id="8f359-130">Now that we have hello information needed toorun hello cmdlet, we run hello `az network watcher test-ip-flow` cmdlet tootest hello traffic.</span></span> <span data-ttu-id="8f359-131">En este ejemplo, estamos utilizando dirección IP de la primera hello en la NIC de hello primero.</span><span class="sxs-lookup"><span data-stu-id="8f359-131">In this example, we are using hello first IP address on hello first NIC.</span></span>

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> <span data-ttu-id="8f359-132">Flujo de IP comprobar requiere que el recurso de máquina virtual de Hola se asigna toorun.</span><span class="sxs-lookup"><span data-stu-id="8f359-132">IP Flow verify requires that hello VM resource is allocated toorun.</span></span>

## <a name="review-results"></a><span data-ttu-id="8f359-133">Revisión de los resultados</span><span class="sxs-lookup"><span data-stu-id="8f359-133">Review Results</span></span>

<span data-ttu-id="8f359-134">Después de ejecutar `az network watcher test-ip-flow` Hola resultados se devuelven, en el ejemplo siguiente se hello es Hola devuelva resultados de hello anterior paso.</span><span class="sxs-lookup"><span data-stu-id="8f359-134">After running `az network watcher test-ip-flow` hello results are returned, hello following example is hello results returned from hello preceding step.</span></span>

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a><span data-ttu-id="8f359-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8f359-135">Next steps</span></span>

<span data-ttu-id="8f359-136">Si se está bloqueando el tráfico y no debe ser, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hacia abajo Hola red seguridad y el grupo de reglas de seguridad que se definen.</span><span class="sxs-lookup"><span data-stu-id="8f359-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

<span data-ttu-id="8f359-137">Obtenga información acerca de tooaudit la configuración de NSG visitando [auditoría red seguridad grupos (NSG) con el Monitor de red](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8f359-137">Learn tooaudit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
