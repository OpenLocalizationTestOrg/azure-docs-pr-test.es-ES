---
title: "aaaSet extremos en una VM de Windows clásico | Documentos de Microsoft"
description: "Obtenga información acerca de tooset extremos de una VM de Windows en hello Azure tooallow portal clásico comunicación con una máquina virtual de Windows en Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="2fadf-103">¿Cómo tooset extremos en una máquina virtual de Windows clásica de Azure</span><span class="sxs-lookup"><span data-stu-id="2fadf-103">How tooset up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="2fadf-104">Hola a todas las ventanas de máquinas virtuales que cree en Azure mediante el modelo de implementación clásica de hello pueden comunicarse automáticamente a través de un canal de red privada con otras máquinas virtuales en el mismo servicio en la nube o red virtual.</span><span class="sxs-lookup"><span data-stu-id="2fadf-104">All Windows virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="2fadf-105">Sin embargo, los equipos de hello Internet u otras redes virtuales requieren máquina virtual del tooa de tráfico de los puntos de conexión toodirect Hola red de entrada.</span><span class="sxs-lookup"><span data-stu-id="2fadf-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="2fadf-106">Este artículo también está disponible para [máquinas virtuales Linux](../../linux/classic/setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="2fadf-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2fadf-107">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2fadf-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="2fadf-108">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="2fadf-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="2fadf-109">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2fadf-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="2fadf-110">Hola **el Administrador de recursos** modelo de implementación, puntos de conexión se configuran mediante **grupos de seguridad de red (NSG)**.</span><span class="sxs-lookup"><span data-stu-id="2fadf-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="2fadf-111">Para obtener más información, consulte [permitir acceso externo tooyour VM con Hola portal de Azure](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2fadf-111">For more information, see [Allow external access tooyour VM using hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="2fadf-112">Cuando crea una máquina virtual Windows Hola portal de Azure, los puntos de conexión comunes como las de escritorio remoto y acceso remoto a Windows PowerShell son normalmente crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2fadf-112">When you create a Windows virtual machine in hello Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="2fadf-113">Puede configurar extremos adicionales al crear la máquina virtual de Hola o posteriormente según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2fadf-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="2fadf-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2fadf-114">Next steps</span></span>
* <span data-ttu-id="2fadf-115">toouse un tooset de cmdlet de PowerShell de Azure un punto de conexión de máquina virtual, consulte [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="2fadf-115">toouse an Azure PowerShell cmdlet tooset up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="2fadf-116">toouse un toomanage de cmdlet de PowerShell de Azure una ACL en un extremo, vea [listas de control de acceso de administración (ACL) para los puntos de conexión mediante el uso de PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2fadf-116">toouse an Azure PowerShell cmdlet toomanage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="2fadf-117">Si ha creado una máquina virtual en el modelo de implementación del Administrador de recursos de hello, puede usar Azure PowerShell demasiado[crear grupos de seguridad de red](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol tráfico toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2fadf-117">If you created a virtual machine in hello Resource Manager deployment model, you can use Azure PowerShell too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol traffic toohello VM.</span></span>
