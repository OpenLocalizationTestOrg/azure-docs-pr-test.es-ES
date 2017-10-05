---
title: "Instalación de MySQL en una máquina virtual con OpenSUSE | Microsoft Docs"
description: "Aprenda a instalar MySQL en una máquina virtual con OpenSUSE Linux en Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1594e10e-c314-455a-9efb-a89441de364b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/19/2016
ms.author: cynthn
ms.openlocfilehash: 01b798a25575b66f89057315ce80d6cc0cde53b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a><span data-ttu-id="0c612-103">Instalación de MySQL en una máquina virtual que ejecuta OpenSUSE Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="0c612-103">Install MySQL on a virtual machine running OpenSUSE Linux in Azure</span></span>
<span data-ttu-id="0c612-104">[MySQL][MySQL] es una conocida base de datos SQL de código abierto.</span><span class="sxs-lookup"><span data-stu-id="0c612-104">[MySQL][MySQL] is a popular, open-source SQL database.</span></span> <span data-ttu-id="0c612-105">En este tutorial se muestra cómo crear una máquina virtual que disponga de OpenSUSE Linux y, a continuación, instale MySQL.</span><span class="sxs-lookup"><span data-stu-id="0c612-105">This tutorial shows you how to create a virtual machine running OpenSUSE Linux, then install MySQL.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="0c612-106">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0c612-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0c612-107">En este artículo se trata el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="0c612-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="0c612-108">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="0c612-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a><span data-ttu-id="0c612-109">Creación de una máquina virtual que ejecuta OpenSUSE Linux</span><span class="sxs-lookup"><span data-stu-id="0c612-109">Create a virtual machine running OpenSUSE Linux</span></span>
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-the-virtual-machine"></a><span data-ttu-id="0c612-110">Instalación y ejecución de MySQL en la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0c612-110">Install and run MySQL on the virtual machine</span></span>
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="0c612-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0c612-111">Next steps</span></span>
<span data-ttu-id="0c612-112">Para obtener más información sobre MySQL, vea la [documentación de MySQ][MySQLDocs].</span><span class="sxs-lookup"><span data-stu-id="0c612-112">For details about MySQL, see the [MySQL Documentation][MySQLDocs].</span></span>

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com

