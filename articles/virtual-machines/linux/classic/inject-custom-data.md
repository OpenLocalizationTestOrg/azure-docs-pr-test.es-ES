---
title: "Inyección de datos en VM de Linux en Azure | Microsoft Docs"
description: "En este tema se describe cómo inyectar datos personalizados en una máquina virtual de Azure cuando se crea la instancia y cómo localizar dichos datos en Windows o Linux."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: d376093c-e01d-4ee3-a826-2b5a35caaa7e
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 8dd04c26f10950b13fe0689a96b3e12250715019
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="injecting-custom-data-into-an-azure-virtual-machine"></a><span data-ttu-id="9f867-103">Inyección de datos personalizados en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="9f867-103">Injecting custom data into an Azure virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="9f867-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9f867-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9f867-105">En este artículo se trata el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="9f867-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="9f867-106">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="9f867-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="9f867-107">Para más información sobre el uso de la extensión de script personalizado con el modelo de Resource Manager, consulte [aquí](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9f867-107">For information about using the Custom Script Extension with the Resource Manager model, see [here](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-inject-custom-data](../../../../includes/virtual-machines-common-classic-inject-custom-data.md)]

