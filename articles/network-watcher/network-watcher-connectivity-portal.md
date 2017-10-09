---
title: 'conectividad de aaaCheck con Monitor de red de Azure: portal de Azure | Documentos de Microsoft'
description: "Esta página explica cómo comprobar la conectividad de toouse con Monitor de red con hello portal de Azure"
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
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="206a7-103">Compruebe la conectividad con el Monitor de red de Azure con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="206a7-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="206a7-104">Portal</span><span class="sxs-lookup"><span data-stu-id="206a7-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="206a7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="206a7-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="206a7-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="206a7-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="206a7-107">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="206a7-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="206a7-108">Obtenga información acerca de cómo se puede establecer toouse conectividad tooverify si una conexión TCP directa de una tooa de máquina virtual tiene el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="206a7-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="206a7-109">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="206a7-109">Before you begin</span></span>

<span data-ttu-id="206a7-110">En este artículo se supone que tiene Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="206a7-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="206a7-111">Una instancia del Monitor de red en la región de Hola que desea toocheck conectividad.</span><span class="sxs-lookup"><span data-stu-id="206a7-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="206a7-112">Conectividad de toocheck de máquinas virtuales con.</span><span class="sxs-lookup"><span data-stu-id="206a7-112">Virtual machines toocheck connectivity with.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="206a7-113">La comprobación de conectividad requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="206a7-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="206a7-114">Para instalar la extensión de hello en una máquina virtual de Windows, visite [extensión de máquina virtual de agente de Monitor de red de Azure para Windows](../virtual-machines/windows/extensions-nwa.md) y para la visita de VM de Linux [extensión de máquina virtual de agente de Monitor de red de Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="206a7-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="206a7-115">Compruebe la conectividad tooa virtual machine</span><span class="sxs-lookup"><span data-stu-id="206a7-115">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="206a7-116">Este ejemplo comprueba la máquina virtual de conectividad tooa destino en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="206a7-116">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

<span data-ttu-id="206a7-117">Navegue tooyour Monitor de red y haga clic en **comprobación de conectividad (versión preliminar)**.</span><span class="sxs-lookup"><span data-stu-id="206a7-117">Navigate tooyour Network Watcher and click **Connectivity check (Preview)**.</span></span> <span data-ttu-id="206a7-118">Seleccione toocheck conectividad de máquina virtual de Hola de.</span><span class="sxs-lookup"><span data-stu-id="206a7-118">Select hello virtual machine toocheck connectivity from.</span></span> <span data-ttu-id="206a7-119">Hola **destino** sección elija **seleccione una máquina virtual** y elija la máquina virtual correcta de Hola y tootest de puerto.</span><span class="sxs-lookup"><span data-stu-id="206a7-119">In hello **Destination** section choose **Select a virtual machine** and choose hello correct virtual machine and port tootest.</span></span>

<span data-ttu-id="206a7-120">Una vez que pulses **comprobar**, se comprueban la conectividad de hello entre máquinas virtuales Hola Hola el puerto especificado.</span><span class="sxs-lookup"><span data-stu-id="206a7-120">Once you click **Check**, hello connectivity between hello virtual machines on hello port specified are checked.</span></span> <span data-ttu-id="206a7-121">En el ejemplo de Hola, Hola destino VM es inaccesible, se muestra una lista de saltos.</span><span class="sxs-lookup"><span data-stu-id="206a7-121">In hello example, hello destination VM is unreachable, a listing of hops are shown.</span></span>

![Resultados de la comprobación de la conectividad de una máquina virtual][1]

## <a name="check-remote-endpoint-connectivity"></a><span data-ttu-id="206a7-123">Comprobación de la conectividad de un punto de conexión remoto</span><span class="sxs-lookup"><span data-stu-id="206a7-123">Check remote endpoint connectivity</span></span>

<span data-ttu-id="206a7-124">conectividad de hello toocheck y el extremo remoto de tooa de latencia, elija hello **especificar manualmente** botón de opción de hello **destino** sección, especifique la dirección url de Hola y el puerto de Hola y haga clic en **comprobar** .</span><span class="sxs-lookup"><span data-stu-id="206a7-124">toocheck hello connectivity and latency tooa remote endpoint, choose hello **Specify manually** radio button in hello **Destination** section, input hello url and hello port and click **Check**.</span></span>  <span data-ttu-id="206a7-125">Se utiliza para puntos de conexión remotos como sitios web y puntos de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="206a7-125">This is used for remote endpoints like websites and storage endpoints.</span></span>

![Resultados de la comprobación de conectividad para un sitio web][2]

## <a name="next-steps"></a><span data-ttu-id="206a7-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="206a7-127">Next steps</span></span>

<span data-ttu-id="206a7-128">Obtenga información acerca de la captura de paquetes de tooautomate con las alertas de la máquina Virtual mediante la visualización [crear una captura de paquetes desencadenadas alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="206a7-128">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="206a7-129">Para comprobar si se permite cierto tráfico hacia o desde la máquina virtual, vea cómo [consultar la Comprobación del flujo de IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="206a7-129">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
