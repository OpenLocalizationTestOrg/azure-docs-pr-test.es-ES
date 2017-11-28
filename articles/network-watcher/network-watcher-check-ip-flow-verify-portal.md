---
title: "comprobar de tráfico de aaaVerify con flujo de IP de Monitor de red de Azure: portal de Azure | Documentos de Microsoft"
description: "Este artículo se describe cómo toocheck si se permite o deniega el tráfico tooor desde una máquina virtual"
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
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="f9a65-103">Compruebe si el tráfico se permitirá o denegará tooor de una máquina virtual con IP flujo comprobar un componente de Monitor de red de Azure</span><span class="sxs-lookup"><span data-stu-id="f9a65-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f9a65-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f9a65-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="f9a65-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f9a65-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="f9a65-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f9a65-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="f9a65-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f9a65-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="f9a65-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="f9a65-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="f9a65-109">Flujo IP comprobar es una característica de Monitor de red que le permite tooverify si se permite el tráfico tooor desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f9a65-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="f9a65-110">validación de Hola se puede ejecutar para el tráfico entrante o saliente.</span><span class="sxs-lookup"><span data-stu-id="f9a65-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="f9a65-111">Este escenario es útil tooget un estado actual del si una máquina virtual puede comunicarse un recurso externo tooan o algún otro recurso.</span><span class="sxs-lookup"><span data-stu-id="f9a65-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or another resource.</span></span> <span data-ttu-id="f9a65-112">Flujo IP comprobar puede ser usado tooverify si las reglas del grupo de seguridad de red (NSG) se han configurado correctamente y solucionar los problemas flujos que se bloquean las reglas de NSG.</span><span class="sxs-lookup"><span data-stu-id="f9a65-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="f9a65-113">Otra razón para usar IP flujo Compruebe es que quiera bloquear el tráfico de tooensure está bloqueando correctamente hello NSG.</span><span class="sxs-lookup"><span data-stu-id="f9a65-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f9a65-114">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="f9a65-114">Before you begin</span></span>

<span data-ttu-id="f9a65-115">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red o tiene una instancia existente de Monitor de red.</span><span class="sxs-lookup"><span data-stu-id="f9a65-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="f9a65-116">escenario de Hello también supone que un grupo de recursos con una máquina virtual válida existe toobe usa.</span><span class="sxs-lookup"><span data-stu-id="f9a65-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="f9a65-117">Escenario</span><span class="sxs-lookup"><span data-stu-id="f9a65-117">Scenario</span></span>

<span data-ttu-id="f9a65-118">Este escenario utiliza tooverify IP flujo comprobar si una máquina virtual puede comunicarse tooanother máquina a través del puerto 443.</span><span class="sxs-lookup"><span data-stu-id="f9a65-118">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="f9a65-119">Si se deniega el tráfico de hello, devuelve la regla de seguridad de Hola que deniega ese tráfico.</span><span class="sxs-lookup"><span data-stu-id="f9a65-119">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="f9a65-120">toolearn más información acerca de IP flujo comprobar, visite [Introducción comprobar flujo de IP](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f9a65-120">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="f9a65-121">Ejecución de la Comprobación del flujo de IP</span><span class="sxs-lookup"><span data-stu-id="f9a65-121">Run IP flow verify</span></span>

<span data-ttu-id="f9a65-122">Navegue tooyour Monitor de red y haga clic en **comprobar flujo IP**.</span><span class="sxs-lookup"><span data-stu-id="f9a65-122">Navigate tooyour Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="f9a65-123">Seleccionar máquina virtual de Hola y la interfaz de red que desee tooverify tráfico desde.</span><span class="sxs-lookup"><span data-stu-id="f9a65-123">Select hello virtual machine and network interface you want tooverify traffic from.</span></span> <span data-ttu-id="f9a65-124">Escriba cualquier información adicional de filtrado y haga clic en **Comprobar**.</span><span class="sxs-lookup"><span data-stu-id="f9a65-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="f9a65-125">Una vez que pulses **comprobar**, se comprueba el flujo de hello en función de criterios de hello proporcionada.</span><span class="sxs-lookup"><span data-stu-id="f9a65-125">Once you click **Check**, hello flow based on hello criteria you provided is checked.</span></span> <span data-ttu-id="f9a65-126">resultado de Hello sea **acceso permitido** o **acceso denegado**.</span><span class="sxs-lookup"><span data-stu-id="f9a65-126">hello result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="f9a65-127">Si se deniega el acceso, Hola grupo de seguridad de red (NSG) y se proporciona la regla de seguridad que bloquee el tráfico.</span><span class="sxs-lookup"><span data-stu-id="f9a65-127">If access is denied, hello Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="f9a65-128">Si la denegación de Hola de tráfico es el comportamiento esperado, regla de hello fue correcta.</span><span class="sxs-lookup"><span data-stu-id="f9a65-128">If hello denial of traffic is expected behavior, then hello rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="f9a65-129">Flujo IP comprobar requiere que se asigna el recurso de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9a65-129">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="f9a65-130">Como puede ver de hello después de la imagen, se permite el tráfico HTTPS saliente Hola.</span><span class="sxs-lookup"><span data-stu-id="f9a65-130">As you can see from hello following image, hello outbound HTTPS traffic was allowed.</span></span>

![Información general sobre la comprobación del flujo de IP][1]

<span data-ttu-id="f9a65-132">Tal como se muestra en hello después de la imagen, se cambia el tráfico hello y tooinbound too123 de cambiar el puerto de entrada.</span><span class="sxs-lookup"><span data-stu-id="f9a65-132">As seen in hello following image, traffic is changed tooinbound and hello inbound port changed too123.</span></span> <span data-ttu-id="f9a65-133">Ahora se deniega el tráfico, mensaje de bienvenida de "Acceso denegado" se proporciona junto con hello seguridad y el grupo de regla de seguridad que deniegan el tráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="f9a65-133">Traffic is now denied, hello message "Access denied" is provided along with hello network security group and security rule that deny hello traffic.</span></span>

![resultados de flujo de ip][2]

## <a name="next-steps"></a><span data-ttu-id="f9a65-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f9a65-135">Next steps</span></span>

<span data-ttu-id="f9a65-136">Si se está bloqueando el tráfico y no debe ser, consulte [administrar grupos de seguridad de red](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hacia abajo Hola red seguridad y el grupo de reglas de seguridad que se definen.</span><span class="sxs-lookup"><span data-stu-id="f9a65-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













