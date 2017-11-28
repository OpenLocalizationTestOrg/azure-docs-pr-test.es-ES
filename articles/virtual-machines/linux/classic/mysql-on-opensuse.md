---
title: aaaInstall MySQL en una VM OpenSUSE | Documentos de Microsoft
description: "Obtenga información acerca de tooinstall MySQL en un equipo de OpenSUSE Linux VMirtual en Azure."
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
ms.openlocfilehash: 8f96d29f29cb9c466dd7fdaf92b378783fdaacd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-running-opensuse-linux-in-azure"></a><span data-ttu-id="8bf0f-103">Instalación de MySQL en una máquina virtual que ejecuta OpenSUSE Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="8bf0f-103">Install MySQL on a virtual machine running OpenSUSE Linux in Azure</span></span>
<span data-ttu-id="8bf0f-104">[MySQL][MySQL] es una conocida base de datos SQL de código abierto.</span><span class="sxs-lookup"><span data-stu-id="8bf0f-104">[MySQL][MySQL] is a popular, open-source SQL database.</span></span> <span data-ttu-id="8bf0f-105">Este tutorial muestra cómo toocreate una máquina virtual con OpenSUSE Linux, a continuación, instalar MySQL.</span><span class="sxs-lookup"><span data-stu-id="8bf0f-105">This tutorial shows you how toocreate a virtual machine running OpenSUSE Linux, then install MySQL.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="8bf0f-106">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8bf0f-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8bf0f-107">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="8bf0f-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="8bf0f-108">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8bf0f-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<br>

## <a name="create-a-virtual-machine-running-opensuse-linux"></a><span data-ttu-id="8bf0f-109">Creación de una máquina virtual que ejecuta OpenSUSE Linux</span><span class="sxs-lookup"><span data-stu-id="8bf0f-109">Create a virtual machine running OpenSUSE Linux</span></span>
[!INCLUDE [create-and-configure-opensuse-vm-in-portal](../../../../includes/create-and-configure-opensuse-vm-in-portal.md)]

## <a name="install-and-run-mysql-on-hello-virtual-machine"></a><span data-ttu-id="8bf0f-110">Instalar y ejecutar MySQL en la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="8bf0f-110">Install and run MySQL on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mysql-on-opensuse-vm](../../../../includes/install-and-run-mysql-on-opensuse-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="8bf0f-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8bf0f-111">Next steps</span></span>
<span data-ttu-id="8bf0f-112">Para obtener más información acerca de MySQL, vea hello [documentación de MySQL][MySQLDocs].</span><span class="sxs-lookup"><span data-stu-id="8bf0f-112">For details about MySQL, see hello [MySQL Documentation][MySQLDocs].</span></span>

[MySQLDocs]:http://dev.mysql.com/doc/index-topic.html
[MySQL]:http://www.mysql.com

