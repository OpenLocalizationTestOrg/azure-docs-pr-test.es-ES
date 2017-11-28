---
title: "Creación de una máquina virtual Linux mediante la CLI de Azure 1.0 | Microsoft Docs"
description: "Aprenda a crear una máquina virtual Linux con la CLI de Azure 1.0 mediante el modelo de implementación clásica"
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
ms.openlocfilehash: 8ddbacbbb70c0cf1a2537fab4d981a316610a4d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-classic-linux-vm-with-the-azure-cli-10"></a><span data-ttu-id="1102e-103">Creación de una máquina virtual Linux con la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="1102e-103">How to Create a Classic Linux VM with the Azure CLI 1.0</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="1102e-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1102e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1102e-105">En este artículo se trata el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="1102e-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="1102e-106">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="1102e-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="1102e-107">Para la versión de Resource Manager, consulte [aquí](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1102e-107">For the Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="1102e-108">En este tema se describe cómo crear una máquina virtual (VM) Linux con la CLI de Azure 1.0 mediante el modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="1102e-108">This topic describes how to create a Linux virtual machine (VM) with the Azure CLI 1.0 using the Classic deployment model.</span></span> <span data-ttu-id="1102e-109">Vamos a usar una imagen de Linux de una de las **IMÁGENES** disponibles en Azure.</span><span class="sxs-lookup"><span data-stu-id="1102e-109">We use a Linux image from the available **IMAGES** on Azure.</span></span> <span data-ttu-id="1102e-110">Los comandos de la CLI de Azure 1.0 ofrecen, entre otras, las siguientes opciones de configuración:</span><span class="sxs-lookup"><span data-stu-id="1102e-110">The Azure CLI 1.0 commands give the following configuration choices, among others:</span></span>

* <span data-ttu-id="1102e-111">Conexión de la VM a una red virtual</span><span class="sxs-lookup"><span data-stu-id="1102e-111">Connecting the VM to a virtual network</span></span>
* <span data-ttu-id="1102e-112">Adición de la VM a un servicio en la nube existente</span><span class="sxs-lookup"><span data-stu-id="1102e-112">Adding the VM to an existing cloud service</span></span>
* <span data-ttu-id="1102e-113">Incorporación de la máquina virtual a una cuenta de almacenamiento existente</span><span class="sxs-lookup"><span data-stu-id="1102e-113">Adding the VM to an existing storage account</span></span>
* <span data-ttu-id="1102e-114">Incorporación de la máquina virtual a un conjunto de disponibilidad o una ubicación</span><span class="sxs-lookup"><span data-stu-id="1102e-114">Adding the VM to an availability set or location</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1102e-115">Si desea que la máquina virtual use una red virtual, con el fin de poder conectarse a ella directamente mediante un nombre de host o configurar conexiones entre locales, asegúrese de que especifica la red virtual al crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1102e-115">If you want your VM to use a virtual network so you can connect to it directly by hostname or set up cross-premises connections, make sure you specify the virtual network when you create the VM.</span></span> <span data-ttu-id="1102e-116">Puede configurarse una máquina virtual para que se una a una red virtual solo cuando se cree la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1102e-116">A VM can be configured to join a virtual network only when you create the VM.</span></span> <span data-ttu-id="1102e-117">Para obtener detalles acerca de las redes virtuales, consulte [Información general sobre redes virtuales de Azure](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span><span class="sxs-lookup"><span data-stu-id="1102e-117">For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span></span>
> 
> 

## <a name="how-to-create-a-linux-vm-using-the-classic-deployment-model"></a><span data-ttu-id="1102e-118">Creación de una máquina virtual Linux mediante el modelo de implementación clásica</span><span class="sxs-lookup"><span data-stu-id="1102e-118">How to create a Linux VM using the Classic deployment model</span></span>
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

