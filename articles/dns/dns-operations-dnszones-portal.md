---
title: "Administración de zonas DNS en DNS de Azure - Azure Portal | Microsoft Docs"
description: "Puede administrar zonas DNS con Azure Portal. Este artículo describe cómo actualizar, eliminar y crear zonas DNS en Azure DNS"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 69a509612e6204fc93dd42bf2fe69cb165b5777c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-the-azure-portal"></a><span data-ttu-id="426b1-104">Administración de zonas DNS en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="426b1-104">How to manage DNS Zones in the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="426b1-105">Portal</span><span class="sxs-lookup"><span data-stu-id="426b1-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="426b1-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="426b1-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="426b1-107">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="426b1-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="426b1-108">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="426b1-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="426b1-109">En este artículo se muestra cómo administrar sus zonas DNS mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="426b1-109">This article shows you how to manage your DNS zones by using the Azure portal.</span></span> <span data-ttu-id="426b1-110">También se pueden administrar las zonas DNS mediante la [CLI de Azure](dns-operations-dnszones-cli.md) multiplataforma o Azure [PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="426b1-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="426b1-111">Creación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="426b1-111">Create a DNS zone</span></span>

1. <span data-ttu-id="426b1-112">Inicie sesión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="426b1-112">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="426b1-113">En el menú Concentrador, haga clic en **Nuevo > Redes >** y, luego, en **Zona DNS** para abrir la hoja Crear zona DNS.</span><span class="sxs-lookup"><span data-stu-id="426b1-113">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![Zona DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="426b1-115">En la hoja **Crear zona DNS**, escriba los valores siguientes y haga clic en **Crear**:</span><span class="sxs-lookup"><span data-stu-id="426b1-115">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>


   | <span data-ttu-id="426b1-116">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="426b1-116">**Setting**</span></span> | <span data-ttu-id="426b1-117">**Valor**</span><span class="sxs-lookup"><span data-stu-id="426b1-117">**Value**</span></span> | <span data-ttu-id="426b1-118">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="426b1-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="426b1-119">**Name**</span><span class="sxs-lookup"><span data-stu-id="426b1-119">**Name**</span></span>|<span data-ttu-id="426b1-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="426b1-120">contoso.com</span></span>|<span data-ttu-id="426b1-121">El nombre de la zona DNS</span><span class="sxs-lookup"><span data-stu-id="426b1-121">The name of the DNS zone</span></span>|
   |<span data-ttu-id="426b1-122">**Suscripción**</span><span class="sxs-lookup"><span data-stu-id="426b1-122">**Subscription**</span></span>|<span data-ttu-id="426b1-123">[Su suscripción]</span><span class="sxs-lookup"><span data-stu-id="426b1-123">[Your subscription]</span></span>|<span data-ttu-id="426b1-124">Seleccione la suscripción en la que se creará la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="426b1-124">Select a subscription to create the DNS zone in.</span></span>|
   |<span data-ttu-id="426b1-125">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="426b1-125">**Resource group**</span></span>|<span data-ttu-id="426b1-126">**Crear nuevo:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="426b1-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="426b1-127">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="426b1-127">Create a resource group.</span></span> <span data-ttu-id="426b1-128">El nombre del grupo de recursos debe ser único dentro de la suscripción seleccionada.</span><span class="sxs-lookup"><span data-stu-id="426b1-128">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="426b1-129">Para más información sobre los grupos de recursos, lea el artículo [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="426b1-129">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="426b1-130">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="426b1-130">**Location**</span></span>|<span data-ttu-id="426b1-131">Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="426b1-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="426b1-132">El grupo de recursos se refiere a la ubicación del grupo de recursos y no tiene efecto alguno sobre la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="426b1-132">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="426b1-133">La ubicación de la zona DNS siempre es "global" y no se muestra.</span><span class="sxs-lookup"><span data-stu-id="426b1-133">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="426b1-134">Enumeración de zonas DNS</span><span class="sxs-lookup"><span data-stu-id="426b1-134">List DNS zones</span></span>

<span data-ttu-id="426b1-135">En Azure Portal, vaya a **Más servicios** > **Redes** > **Zonas DNS**.</span><span class="sxs-lookup"><span data-stu-id="426b1-135">In the Azure portal, navigate to **More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="426b1-136">Cada zona DNS tiene su propio recurso, información como el número de conjuntos de registros y los servidores de nombres están visibles en esta vista.</span><span class="sxs-lookup"><span data-stu-id="426b1-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="426b1-137">La columna **SERVIDORES DE NOMBRES** no está en la vista predeterminada; para agregarla, haga clic en **Columnas**, seleccione **Servidores de nombres** y haga clic en **Listo**.</span><span class="sxs-lookup"><span data-stu-id="426b1-137">The column **NAME SERVERS** is not in the default view, to add it click **Columns**, select **Name servers** and click **Done**.</span></span>

![enumeración de zonas DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="426b1-139">Eliminar una zona DNS</span><span class="sxs-lookup"><span data-stu-id="426b1-139">Delete a DNS zone</span></span>

<span data-ttu-id="426b1-140">Navegue a una zona DNS en el portal.</span><span class="sxs-lookup"><span data-stu-id="426b1-140">Navigate to a DNS zone in the portal.</span></span> <span data-ttu-id="426b1-141">En la hoja **Zona DNS**, haga clic en **Eliminar zona**.</span><span class="sxs-lookup"><span data-stu-id="426b1-141">On the **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="426b1-142">Se le pide que confirme si desea eliminar la zona DNS.</span><span class="sxs-lookup"><span data-stu-id="426b1-142">You are prompted to confirm you are wanting to delete the DNS zone.</span></span> <span data-ttu-id="426b1-143">Al eliminar una zona DNS, también se eliminan todos los registros contenidos en la zona.</span><span class="sxs-lookup"><span data-stu-id="426b1-143">Deleting a DNS zone also deletes all the records that are contained in the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="426b1-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="426b1-144">Next steps</span></span>

<span data-ttu-id="426b1-145">Aprenda a trabajar con la zona y registros DNS en [Introducción a DNS de Azure con Azure Portal](dns-getstarted-portal.md).</span><span class="sxs-lookup"><span data-stu-id="426b1-145">Learn how to work with your DNS Zone and records by visiting [Get started with Azure DNS using the Azure portal](dns-getstarted-portal.md).</span></span>