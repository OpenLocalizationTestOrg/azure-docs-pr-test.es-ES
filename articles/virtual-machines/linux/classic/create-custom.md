---
title: "aaaCreate una VM de Linux clásica con Hola 1.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual de Linux con el uso de hello Azure CLI 1.0 Hola modelo de implementación clásica"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a><span data-ttu-id="cbc0a-103">¿Cómo tooCreate una VM de Linux clásica con Hola 1.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="cbc0a-103">How tooCreate a Classic Linux VM with hello Azure CLI 1.0</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="cbc0a-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="cbc0a-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cbc0a-105">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="cbc0a-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="cbc0a-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbc0a-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="cbc0a-107">Para la versión del Administrador de recursos de hello, consulte [aquí](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cbc0a-107">For hello Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="cbc0a-108">Este tema describe cómo toocreate una máquina virtual de Linux (VM) con el uso de hello Azure CLI 1.0 Hola modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="cbc0a-108">This topic describes how toocreate a Linux virtual machine (VM) with hello Azure CLI 1.0 using hello Classic deployment model.</span></span> <span data-ttu-id="cbc0a-109">Se utiliza una imagen de Linux de hello disponible **imágenes** en Azure.</span><span class="sxs-lookup"><span data-stu-id="cbc0a-109">We use a Linux image from hello available **IMAGES** on Azure.</span></span> <span data-ttu-id="cbc0a-110">comandos de Hello 1.0 de CLI de Azure permiten Hola siguientes opciones de configuración, entre otros:</span><span class="sxs-lookup"><span data-stu-id="cbc0a-110">hello Azure CLI 1.0 commands give hello following configuration choices, among others:</span></span>

* <span data-ttu-id="cbc0a-111">Conexión de red virtual de hello VM tooa</span><span class="sxs-lookup"><span data-stu-id="cbc0a-111">Connecting hello VM tooa virtual network</span></span>
* <span data-ttu-id="cbc0a-112">Agregar servicio de nube existente de hello VM tooan</span><span class="sxs-lookup"><span data-stu-id="cbc0a-112">Adding hello VM tooan existing cloud service</span></span>
* <span data-ttu-id="cbc0a-113">Agregar cuenta de almacenamiento existente de hello VM tooan</span><span class="sxs-lookup"><span data-stu-id="cbc0a-113">Adding hello VM tooan existing storage account</span></span>
* <span data-ttu-id="cbc0a-114">Agregar conjunto de disponibilidad de hello VM tooan o ubicación</span><span class="sxs-lookup"><span data-stu-id="cbc0a-114">Adding hello VM tooan availability set or location</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbc0a-115">Si desea que su toouse de máquina virtual una red virtual para que pueda conectarse tooit directamente por el nombre de host o configurar las conexiones entre entornos, asegúrese de que especificar red virtual de Hola cuando creas Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cbc0a-115">If you want your VM toouse a virtual network so you can connect tooit directly by hostname or set up cross-premises connections, make sure you specify hello virtual network when you create hello VM.</span></span> <span data-ttu-id="cbc0a-116">Una máquina virtual solo puede tener toojoin configurado una red virtual cuando cree Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cbc0a-116">A VM can be configured toojoin a virtual network only when you create hello VM.</span></span> <span data-ttu-id="cbc0a-117">Para obtener detalles acerca de las redes virtuales, consulte [Información general sobre redes virtuales de Azure](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span><span class="sxs-lookup"><span data-stu-id="cbc0a-117">For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span></span>
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a><span data-ttu-id="cbc0a-118">¿Cómo toocreate una VM de Linux con Hola modelo de implementación clásica</span><span class="sxs-lookup"><span data-stu-id="cbc0a-118">How toocreate a Linux VM using hello Classic deployment model</span></span>
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

