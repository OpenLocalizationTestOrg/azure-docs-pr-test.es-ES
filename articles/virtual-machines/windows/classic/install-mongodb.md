---
title: "aaaInstall MongoDB en una máquina virtual de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo se crea tooinstall MongoDB en una máquina virtual de Azure con el modelo de implementación clásica de hello ejecuta Windows Server."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: aafd86b4c49c6a97ae8a1a2191ae375b6c47483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="1d832-103">Instalación de MongoDB en una máquina virtual de Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="1d832-103">Install MongoDB on a Windows VM in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1d832-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1d832-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="1d832-105">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="1d832-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="1d832-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d832-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="1d832-107">tooinstall y configurar MongoDB utilizando el modelo de implementación del Administrador de recursos de hello, consulte [este artículo](../install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="1d832-107">tooinstall and configure MongoDB using hello Resource Manager deployment model, see [this article](../install-mongodb.md).</span></span>

<span data-ttu-id="1d832-108">[MongoDB][MongoDB] es una conocida base de datos NoSQL de código abierto y alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="1d832-108">[MongoDB][MongoDB] is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="1d832-109">En este artículo le guía por la creación de una máquina virtual de Windows Server (VM) con hello [portal de Azure][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="1d832-109">This article guides you through creating a Windows Server virtual machine (VM) using hello [Azure portal][AzurePortal].</span></span> <span data-ttu-id="1d832-110">A continuación, crear y adjuntar un toohello de disco de datos VM antes de instalar y configurar MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1d832-110">You then create and attach a data disk toohello VM before installing and configuring MongoDB.</span></span> <span data-ttu-id="1d832-111">Si tiene una máquina virtual existente en Azure que desearía toouse, también puede avanzar directamente demasiado[instalación y configuración de MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="1d832-111">If you have an existing VM in Azure that you would like toouse, you can jump straight too[installing and configuring MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span></span>

## <a name="create-a-virtual-machine-running-windows-server"></a><span data-ttu-id="1d832-112">Creación de una máquina virtual que ejecuta Windows Server</span><span class="sxs-lookup"><span data-stu-id="1d832-112">Create a virtual machine running Windows Server</span></span>
<span data-ttu-id="1d832-113">Siga estos toocreate instrucciones una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1d832-113">Follow these instructions toocreate a virtual machine.</span></span>

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> <span data-ttu-id="1d832-114">Puede agregar un extremo para MongoDB al crear la máquina virtual de Hola y configurarlo como sigue: nombre como **Mongo**, use **TCP** como protocolo de Hola y el conjunto ambos demasiado Hola puertos públicos y privados**27017**.</span><span class="sxs-lookup"><span data-stu-id="1d832-114">You can add an endpoint for MongoDB while creating hello virtual machine, and configure it as follows: name it as **Mongo**, use **TCP** as hello protocol, and set both hello public and private ports too**27017**.</span></span>
>
>

## <a name="attach-a-data-disk"></a><span data-ttu-id="1d832-115">Acoplamiento de un disco de datos</span><span class="sxs-lookup"><span data-stu-id="1d832-115">Attach a data disk</span></span>
<span data-ttu-id="1d832-116">almacenamiento de tooprovide para la máquina virtual de hello, adjuntar un disco de datos y e inicializarlo después para que Windows pueda usarlo.</span><span class="sxs-lookup"><span data-stu-id="1d832-116">tooprovide storage for hello virtual machine, attach a data disk and then initialize it so that Windows can use it.</span></span> <span data-ttu-id="1d832-117">Si ya tiene un disco de datos, puede conectar ese disco existente o conectar un disco vacío.</span><span class="sxs-lookup"><span data-stu-id="1d832-117">If you already have a data disk, you can attach that existing disk, or you can attach an empty disk.</span></span>

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

<span data-ttu-id="1d832-118">Para obtener instrucciones acerca de cómo inicializar disco hello, consulte "Cómo: inicializar un nuevo disco de datos en Windows Server" en [cómo tooattach datos de un disco de máquina virtual de Windows tooa](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="1d832-118">For instructions on initializing hello disk, see "How to: Initialize a new data disk in Windows Server" in [How tooattach a data disk tooa Windows virtual machine](attach-disk.md).</span></span>

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a><span data-ttu-id="1d832-119">Instalar y ejecutar MongoDB en la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="1d832-119">Install and run MongoDB on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a><span data-ttu-id="1d832-120">Resumen</span><span class="sxs-lookup"><span data-stu-id="1d832-120">Summary</span></span>
<span data-ttu-id="1d832-121">En este tutorial, aprendió cómo toocreate una máquina virtual que ejecuta Windows Server, remotamente conectar tooit y adjuntar un disco de datos.</span><span class="sxs-lookup"><span data-stu-id="1d832-121">In this tutorial, you learned how toocreate a virtual machine running Windows Server, remotely connect tooit, and attach a data disk.</span></span>  <span data-ttu-id="1d832-122">También habrá aprendido cómo tooinstall y configurar MongoDB en la máquina virtual basada en Windows de Hola.</span><span class="sxs-lookup"><span data-stu-id="1d832-122">You also learned how tooinstall and configure MongoDB on hello Windows-based virtual machine.</span></span> <span data-ttu-id="1d832-123">Ahora puedes acceder MongoDB en máquina virtual basada en Windows hello, por siguientes Hola temas avanzados de hello [la documentación de MongoDB][MongoDocs].</span><span class="sxs-lookup"><span data-stu-id="1d832-123">You can now access MongoDB on hello Windows-based virtual machine, by following hello advanced topics in hello [MongoDB documentation][MongoDocs].</span></span>

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

