---
title: aaaCreate FQDN para una VM de Linux en hello portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un nombre de dominio completo o FQDN, para un administrador de recursos según la máquina virtual en hello portal de Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1494a0cb1caa62069c72096a739aee111ac8b383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-linux-vm"></a><span data-ttu-id="07ad5-103">Crear un nombre de dominio completo de hello portal de Azure para una VM de Linux</span><span class="sxs-lookup"><span data-stu-id="07ad5-103">Create a fully qualified domain name in hello Azure portal for a Linux VM</span></span>

<span data-ttu-id="07ad5-104">Cuando crea una máquina virtual (VM) en hello [portal de Azure](https://portal.azure.com), automáticamente se crea un recurso IP público para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="07ad5-104">When you create a virtual machine (VM) in hello [Azure portal](https://portal.azure.com), a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="07ad5-105">Utilice este Hola acceso de tooremotely de dirección IP virtual.</span><span class="sxs-lookup"><span data-stu-id="07ad5-105">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="07ad5-106">Aunque el portal de hello no crea un [nombre de dominio completo](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), o FQDN, puede agregar uno una vez hello máquina virtual creada.</span><span class="sxs-lookup"><span data-stu-id="07ad5-106">Although hello portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can add one once hello VM is created.</span></span> <span data-ttu-id="07ad5-107">En este artículo se muestra hello pasos toocreate un nombre DNS o el FQDN.</span><span class="sxs-lookup"><span data-stu-id="07ad5-107">This article demonstrates hello steps toocreate a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="07ad5-108">Creación de un FQDN</span><span class="sxs-lookup"><span data-stu-id="07ad5-108">Create a FQDN</span></span>
<span data-ttu-id="07ad5-109">En este artículo se supone que ya ha creado una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="07ad5-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="07ad5-110">Si es necesario, puede [crear una máquina virtual en el portal de hello](quick-create-portal.md) o [con hello Azure CLI](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="07ad5-110">If needed, you can [create a VM in hello portal](quick-create-portal.md) or [with hello Azure CLI](quick-create-cli.md).</span></span> <span data-ttu-id="07ad5-111">Una vez que la máquina virtual está en funcionamiento, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="07ad5-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="07ad5-112">Ahora puede conectarse remotamente toohello el nombre de máquina virtual con este DNS como con `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="07ad5-112">You can now connect remotely toohello VM using this DNS name such as with `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07ad5-113">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="07ad5-113">Next steps</span></span>
<span data-ttu-id="07ad5-114">Ahora que la máquina virtual tiene un nombre DNS y una IP pública, puede implementar marcos y servicios de aplicaciones comunes, como nginx, MongoDB, Docker, etc.</span><span class="sxs-lookup"><span data-stu-id="07ad5-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as nginx, MongoDB, Docker, etc.</span></span>

<span data-ttu-id="07ad5-115">También puede leer más sobre el [uso de Resource Manager](../../azure-resource-manager/resource-group-overview.md) para obtener sugerencias sobre la creación de las implementaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="07ad5-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

