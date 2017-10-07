---
title: "aaaSet extremos en una VM de Linux clásica | Documentos de Microsoft"
description: "Obtenga información acerca de tooset extremos de una VM de Linux en hello Azure tooallow portal clásico comunicación con una máquina virtual de Linux en Azure"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f3749738-1109-4a1d-8635-40e4bd220e91
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 1c959d10dd1e20228fa4a20e1cc0205c1d12f185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-linux-classic-virtual-machine-in-azure"></a><span data-ttu-id="68f7c-103">¿Cómo tooset extremos en una máquina virtual de Linux clásica de Azure</span><span class="sxs-lookup"><span data-stu-id="68f7c-103">How tooset up endpoints on a Linux classic virtual machine in Azure</span></span>
<span data-ttu-id="68f7c-104">Todas las máquinas virtuales de Linux que se crean en Azure mediante el modelo de implementación clásica de hello pueden comunicarse automáticamente a través de un canal de red privada con otras máquinas virtuales en hello que mismo servicio o de red virtual en la nube.</span><span class="sxs-lookup"><span data-stu-id="68f7c-104">All Linux virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="68f7c-105">Sin embargo, los equipos de hello Internet u otras redes virtuales requieren máquina virtual del tooa de tráfico de los puntos de conexión toodirect Hola red de entrada.</span><span class="sxs-lookup"><span data-stu-id="68f7c-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="68f7c-106">Este artículo también está disponible para [máquinas virtuales Windows](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68f7c-106">This article is also available for [Windows virtual machines](../../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68f7c-107">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="68f7c-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="68f7c-108">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="68f7c-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="68f7c-109">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="68f7c-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="68f7c-110">Hola **el Administrador de recursos** modelo de implementación, puntos de conexión se configuran mediante **grupos de seguridad de red (NSG)**.</span><span class="sxs-lookup"><span data-stu-id="68f7c-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="68f7c-111">Para más información, consulte [Apertura de puertos y puntos de conexión](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68f7c-111">For more information, see [Opening ports and endpoints](../nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="68f7c-112">Al crear una máquina virtual Linux en hello portal de Azure, un punto de conexión de Secure Shell (SSH) es normalmente crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="68f7c-112">When you create a Linux virtual machine in hello Azure portal, an endpoint for Secure Shell (SSH) is typically created for you automatically.</span></span> <span data-ttu-id="68f7c-113">Puede configurar extremos adicionales al crear la máquina virtual de Hola o posteriormente según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="68f7c-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="68f7c-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="68f7c-114">Next steps</span></span>
* <span data-ttu-id="68f7c-115">También puede crear un punto de conexión de máquina virtual mediante hello [interfaz de línea de comandos de Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="68f7c-115">You can also create a VM endpoint by using hello [Azure Command-Line Interface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="68f7c-116">Ejecute hello **crear punto de conexión de máquina virtual de azure** comando.</span><span class="sxs-lookup"><span data-stu-id="68f7c-116">Run hello **azure vm endpoint create** command.</span></span>
* <span data-ttu-id="68f7c-117">Si ha creado una máquina virtual en el modelo de implementación del Administrador de recursos de hello, puede usar hello Azure CLI en el modo de administrador de recursos demasiado[crear grupos de seguridad de red](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol tráfico toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="68f7c-117">If you created a virtual machine in hello Resource Manager deployment model, you can use hello Azure CLI in Resource Manager mode too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-cli.md) toocontrol traffic toohello VM.</span></span>
