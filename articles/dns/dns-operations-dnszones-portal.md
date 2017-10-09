---
title: 'aaaManage DNS zonas en DNS de Azure: portal de Azure | Documentos de Microsoft'
description: "Puede administrar zonas DNS con hello portal de Azure. Este artículo describe cómo eliminar tooupdate y cómo crear las zonas DNS en el DNS de Azure"
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
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a><span data-ttu-id="26ea2-104">¿Cómo toomanage zonas de DNS en Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="26ea2-104">How toomanage DNS Zones in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="26ea2-105">Portal</span><span class="sxs-lookup"><span data-stu-id="26ea2-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="26ea2-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="26ea2-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="26ea2-107">CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="26ea2-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="26ea2-108">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="26ea2-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="26ea2-109">Este artículo muestra cómo toomanage su DNS zonas mediante el uso de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="26ea2-109">This article shows you how toomanage your DNS zones by using hello Azure portal.</span></span> <span data-ttu-id="26ea2-110">También puede administrar las zonas DNS con hello multiplataforma [CLI de Azure](dns-operations-dnszones-cli.md) o hello Azure [PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="26ea2-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="26ea2-111">Creación de una zona DNS</span><span class="sxs-lookup"><span data-stu-id="26ea2-111">Create a DNS zone</span></span>

1. <span data-ttu-id="26ea2-112">Inicie sesión en toohello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="26ea2-112">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="26ea2-113">En el menú del concentrador hello, haga clic en y haga clic en **nuevo > redes >** y, a continuación, haga clic en **zona DNS** hoja de zona de DNS crear de tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="26ea2-113">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Zona DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="26ea2-115">En hello **zona DNS crear** escriba Hola después valores hoja, haga clic en **crear**:</span><span class="sxs-lookup"><span data-stu-id="26ea2-115">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>


   | <span data-ttu-id="26ea2-116">**Configuración**</span><span class="sxs-lookup"><span data-stu-id="26ea2-116">**Setting**</span></span> | <span data-ttu-id="26ea2-117">**Valor**</span><span class="sxs-lookup"><span data-stu-id="26ea2-117">**Value**</span></span> | <span data-ttu-id="26ea2-118">**Detalles**</span><span class="sxs-lookup"><span data-stu-id="26ea2-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="26ea2-119">**Name**</span><span class="sxs-lookup"><span data-stu-id="26ea2-119">**Name**</span></span>|<span data-ttu-id="26ea2-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="26ea2-120">contoso.com</span></span>|<span data-ttu-id="26ea2-121">nombre de Hola de zona DNS de Hola</span><span class="sxs-lookup"><span data-stu-id="26ea2-121">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="26ea2-122">**Suscripción**</span><span class="sxs-lookup"><span data-stu-id="26ea2-122">**Subscription**</span></span>|<span data-ttu-id="26ea2-123">[Su suscripción]</span><span class="sxs-lookup"><span data-stu-id="26ea2-123">[Your subscription]</span></span>|<span data-ttu-id="26ea2-124">Seleccione una zona DNS de suscripción toocreate hello en.</span><span class="sxs-lookup"><span data-stu-id="26ea2-124">Select a subscription toocreate hello DNS zone in.</span></span>|
   |<span data-ttu-id="26ea2-125">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="26ea2-125">**Resource group**</span></span>|<span data-ttu-id="26ea2-126">**Crear nuevo:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="26ea2-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="26ea2-127">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="26ea2-127">Create a resource group.</span></span> <span data-ttu-id="26ea2-128">nombre de grupo de recursos de Hello debe ser único dentro de la suscripción de Hola que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="26ea2-128">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="26ea2-129">más información acerca de los grupos de recursos, leer hello toolearn [el Administrador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) artículo de información general.</span><span class="sxs-lookup"><span data-stu-id="26ea2-129">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="26ea2-130">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="26ea2-130">**Location**</span></span>|<span data-ttu-id="26ea2-131">Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="26ea2-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="26ea2-132">grupo de recursos de Hello hace referencia la ubicación de toohello Hola del grupo de recursos y no tiene ningún efecto en la zona DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="26ea2-132">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="26ea2-133">ubicación de la zona DNS Hola siempre es "global" y no se muestra.</span><span class="sxs-lookup"><span data-stu-id="26ea2-133">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="26ea2-134">Enumeración de zonas DNS</span><span class="sxs-lookup"><span data-stu-id="26ea2-134">List DNS zones</span></span>

<span data-ttu-id="26ea2-135">En la consulta Hola portal de Azure, navegue demasiado**más servicios** > **redes** > **zonas DNS**.</span><span class="sxs-lookup"><span data-stu-id="26ea2-135">In hello Azure portal, navigate too**More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="26ea2-136">Cada zona DNS tiene su propio recurso, información como el número de conjuntos de registros y los servidores de nombres están visibles en esta vista.</span><span class="sxs-lookup"><span data-stu-id="26ea2-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="26ea2-137">columna de Hello **servidores de nombres** no está en la vista predeterminada de hello, tooadd clic **columnas**, seleccione **servidores de nombres** y haga clic en **realiza**.</span><span class="sxs-lookup"><span data-stu-id="26ea2-137">hello column **NAME SERVERS** is not in hello default view, tooadd it click **Columns**, select **Name servers** and click **Done**.</span></span>

![enumeración de zonas DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="26ea2-139">Eliminar una zona DNS</span><span class="sxs-lookup"><span data-stu-id="26ea2-139">Delete a DNS zone</span></span>

<span data-ttu-id="26ea2-140">Navegue tooa zona DNS en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="26ea2-140">Navigate tooa DNS zone in hello portal.</span></span> <span data-ttu-id="26ea2-141">En hello **zona DNS** hoja, haga clic en **elimine la zona**.</span><span class="sxs-lookup"><span data-stu-id="26ea2-141">On hello **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="26ea2-142">Son tooconfirm solicitada son que deseaba un zona DNS toodelete Hola.</span><span class="sxs-lookup"><span data-stu-id="26ea2-142">You are prompted tooconfirm you are wanting toodelete hello DNS zone.</span></span> <span data-ttu-id="26ea2-143">Eliminar una zona DNS, también elimina todos los registros de Hola que figuran en la zona de Hola.</span><span class="sxs-lookup"><span data-stu-id="26ea2-143">Deleting a DNS zone also deletes all hello records that are contained in hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26ea2-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="26ea2-144">Next steps</span></span>

<span data-ttu-id="26ea2-145">Obtenga información acerca de cómo toowork con la zona DNS y registros visitando [Introducción a DNS de Azure mediante el portal de Azure de hello](dns-getstarted-portal.md).</span><span class="sxs-lookup"><span data-stu-id="26ea2-145">Learn how toowork with your DNS Zone and records by visiting [Get started with Azure DNS using hello Azure portal](dns-getstarted-portal.md).</span></span>
