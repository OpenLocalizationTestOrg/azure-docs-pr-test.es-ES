---
title: "Verificación del tráfico con la Comprobación del flujo de IP en Azure Network Watcher (Azure Portal) | Microsoft Docs"
description: "En este artículo se describe cómo comprobar si se permite o se deniega el tráfico hacia o desde una máquina virtual."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7db29c186cf6e6f3b40a680ab76f1d2763f806ba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="b9c84-103">Compruebe si se permite o se deniega el tráfico hacia o desde una máquina virtual con la Comprobación del flujo de IP, un componente de Azure Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="b9c84-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="b9c84-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b9c84-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="b9c84-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9c84-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="b9c84-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b9c84-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="b9c84-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b9c84-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="b9c84-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="b9c84-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="b9c84-109">La Comprobación del flujo de IP es una característica de Network Watcher que permite comprobar si se permite el tráfico hacia o desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b9c84-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="b9c84-110">Se puede ejecutar la validación para el tráfico entrante o saliente.</span><span class="sxs-lookup"><span data-stu-id="b9c84-110">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="b9c84-111">Este escenario es útil para averiguar si una máquina virtual puede comunicarse con un recurso externo o con otro recurso.</span><span class="sxs-lookup"><span data-stu-id="b9c84-111">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or another resource.</span></span> <span data-ttu-id="b9c84-112">La Comprobación del flujo de IP se puede usar para comprobar si las reglas de grupos de seguridad de red (NSG) se han configurado correctamente y solucionar los problemas de flujos que las reglas de NSG bloquean.</span><span class="sxs-lookup"><span data-stu-id="b9c84-112">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="b9c84-113">Otra razón para usar la Comprobación del flujo de IP es asegurarse de que el NSG está bloqueando correctamente el tráfico que quiere bloquear.</span><span class="sxs-lookup"><span data-stu-id="b9c84-113">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b9c84-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="b9c84-114">Before you begin</span></span>

<span data-ttu-id="b9c84-115">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create a Network Watcher](network-watcher-create.md) (Creación de una instancia de Network Watcher) o que ya tiene una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="b9c84-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="b9c84-116">En este escenario también se da por hecho que existe un grupo de recursos con una máquina virtual válida.</span><span class="sxs-lookup"><span data-stu-id="b9c84-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="b9c84-117">Escenario</span><span class="sxs-lookup"><span data-stu-id="b9c84-117">Scenario</span></span>

<span data-ttu-id="b9c84-118">Este escenario utiliza la Comprobación del flujo de IP para verificar si una máquina virtual puede comunicarse con otra a través del puerto 443.</span><span class="sxs-lookup"><span data-stu-id="b9c84-118">This scenario uses IP Flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="b9c84-119">Si se deniega el tráfico, devuelve la regla de seguridad que está denegando ese tráfico.</span><span class="sxs-lookup"><span data-stu-id="b9c84-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="b9c84-120">Para más información sobre la Comprobación del flujo de IP, vea la [introducción a la Comprobación del flujo de IP](network-watcher-ip-flow-verify-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b9c84-120">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="b9c84-121">Ejecución de la Comprobación del flujo de IP</span><span class="sxs-lookup"><span data-stu-id="b9c84-121">Run IP flow verify</span></span>

<span data-ttu-id="b9c84-122">Vaya a Network Watcher y haga clic en **Comprobación del flujo de IP**.</span><span class="sxs-lookup"><span data-stu-id="b9c84-122">Navigate to your Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="b9c84-123">Seleccione la máquina virtual y la interfaz de red de las que quiere verificar el tráfico.</span><span class="sxs-lookup"><span data-stu-id="b9c84-123">Select the virtual machine and network interface you want to verify traffic from.</span></span> <span data-ttu-id="b9c84-124">Escriba cualquier información adicional de filtrado y haga clic en **Comprobar**.</span><span class="sxs-lookup"><span data-stu-id="b9c84-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="b9c84-125">Después de hacer clic en **Comprobar**, se comprueba el flujo en función de los criterios establecidos.</span><span class="sxs-lookup"><span data-stu-id="b9c84-125">Once you click **Check**, the flow based on the criteria you provided is checked.</span></span> <span data-ttu-id="b9c84-126">El resultado es **Acceso permitido** o **Acceso denegado**.</span><span class="sxs-lookup"><span data-stu-id="b9c84-126">The result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="b9c84-127">Si se deniega el acceso, se proporciona las reglas de grupo de seguridad de red (NSG) y de seguridad que bloquean el tráfico.</span><span class="sxs-lookup"><span data-stu-id="b9c84-127">If access is denied, the Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="b9c84-128">Si la denegación del tráfico es el comportamiento esperado, la regla es correcta.</span><span class="sxs-lookup"><span data-stu-id="b9c84-128">If the denial of traffic is expected behavior, then the rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="b9c84-129">La Comprobación del flujo de IP requiere que el recurso de máquina virtual esté asignado.</span><span class="sxs-lookup"><span data-stu-id="b9c84-129">IP flow verify requires that the VM resource is allocated.</span></span>

<span data-ttu-id="b9c84-130">Como puede ver en la siguiente imagen, se permite el tráfico HTTPS saliente.</span><span class="sxs-lookup"><span data-stu-id="b9c84-130">As you can see from the following image, the outbound HTTPS traffic was allowed.</span></span>

![Información general sobre la comprobación del flujo de IP][1]

<span data-ttu-id="b9c84-132">Como se muestra en la imagen siguiente, el tráfico cambia a entrante y el puerto de entrada cambia a 123.</span><span class="sxs-lookup"><span data-stu-id="b9c84-132">As seen in the following image, traffic is changed to inbound and the inbound port changed to 123.</span></span> <span data-ttu-id="b9c84-133">Ahora se deniega el tráfico y aparece el mensaje "Acceso denegado" junto con las reglas del grupo de seguridad de red y de seguridad que deniegan el tráfico.</span><span class="sxs-lookup"><span data-stu-id="b9c84-133">Traffic is now denied, the message "Access denied" is provided along with the network security group and security rule that deny the traffic.</span></span>

![resultados de flujo de ip][2]

## <a name="next-steps"></a><span data-ttu-id="b9c84-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b9c84-135">Next steps</span></span>

<span data-ttu-id="b9c84-136">Si se está bloqueando el tráfico y no debería ser así, vea [Administración de grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) para realizar un seguimiento de las reglas del grupo de seguridad de red y de seguridad definidas.</span><span class="sxs-lookup"><span data-stu-id="b9c84-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













