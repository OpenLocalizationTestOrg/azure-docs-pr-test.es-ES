---
title: "Azure Active Directory Domain Services: Creación o selección de una red virtual | Microsoft Docs"
description: "Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure clásico"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 13ab1608-e3d8-40de-9f7b-9b5b42199af4
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 212c741b20e846742d94f70342c4263ce8984153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a><span data-ttu-id="469c7-103">Creación o selección de una red virtual para Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="469c7-103">Create or select a virtual network for Azure Active Directory Domain Services</span></span>
## <a name="before-you-begin"></a><span data-ttu-id="469c7-104">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="469c7-104">Before you begin</span></span>
<span data-ttu-id="469c7-105">Consulte demasiado[consideraciones de red para servicios de dominio de Active Directory de Azure](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="469c7-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>

## <a name="task-2-create-an-azure-virtual-network"></a><span data-ttu-id="469c7-106">Tarea 2: Creación de una red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="469c7-106">Task 2: Create an Azure virtual network</span></span>
<span data-ttu-id="469c7-107">tarea de configuración siguiente Hello es toocreate una red virtual de Azure y una subred dentro de él.</span><span class="sxs-lookup"><span data-stu-id="469c7-107">hello next configuration task is toocreate an Azure virtual network and a subnet within it.</span></span> <span data-ttu-id="469c7-108">Puede habilitar Azure Active Directory Domain Services en esta subred dentro de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="469c7-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="469c7-109">Si tiene una red virtual existente que prefiere toouse, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="469c7-109">If you have an existing virtual network that you’d prefer toouse, you can skip this step.</span></span>

> [!NOTE]
> <span data-ttu-id="469c7-110">Asegúrese de que ese Hola red virtual de Azure cree o elija toouse con servicios de dominio de Active Directory de Azure pertenece tooan región de Azure es compatible con servicios de dominio de Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="469c7-110">Make sure that hello Azure virtual network you create or choose toouse with Azure Active Directory Domain Services belongs tooan Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="469c7-111">tooascertain Hola regiones de Azure en el que está disponible servicios de dominio de Active Directory de Azure, consulte [servicios de Azure por región](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="469c7-111">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
>
><span data-ttu-id="469c7-112">Anote el nombre de Hola de hello tooensure de red virtual que seleccione red virtual derecha hello cuando se habilita servicios de dominio de Active Directory de Azure en un paso de configuración posteriores.</span><span class="sxs-lookup"><span data-stu-id="469c7-112">Note hello name of hello virtual network tooensure that you select hello right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span></span>


<span data-ttu-id="469c7-113">toocreate una red virtual de Azure en el que desea tooenable Azure Active Directory Domain Services, siga estas instrucciones de configuración:</span><span class="sxs-lookup"><span data-stu-id="469c7-113">toocreate an Azure virtual network in which you want tooenable Azure Active Directory Domain Services, follow these configuration instructions:</span></span>

1. <span data-ttu-id="469c7-114">Vaya toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="469c7-114">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="469c7-115">En el panel izquierdo de hello, seleccione **redes**.</span><span class="sxs-lookup"><span data-stu-id="469c7-115">In hello left pane, select **Networks**.</span></span>

    <span data-ttu-id="469c7-116">![Nodo Redes](./media/active-directory-domain-services-getting-started/networks-node.png)</span><span class="sxs-lookup"><span data-stu-id="469c7-116">![Networks node](./media/active-directory-domain-services-getting-started/networks-node.png)</span></span>  
    <span data-ttu-id="469c7-117">Hola **redes virtuales** abre la ventana.</span><span class="sxs-lookup"><span data-stu-id="469c7-117">hello **Virtual Networks** window opens.</span></span>
3. <span data-ttu-id="469c7-118">En el panel de tareas de hello en parte inferior de Hola de ventana hello, haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="469c7-118">In hello task pane at hello bottom of hello window, click **New**.</span></span>

    ![Ventana Redes virtuales](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. <span data-ttu-id="469c7-120">Haga clic en **Network Services** y seleccione **Virtual Network**.</span><span class="sxs-lookup"><span data-stu-id="469c7-120">Click **Network Services**, and then select **Virtual Network**.</span></span>

    ![Red virtual: creación rápida](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. <span data-ttu-id="469c7-122">Haga clic en una red virtual, toocreate **creación rápida**.</span><span class="sxs-lookup"><span data-stu-id="469c7-122">toocreate a virtual network, click **Quick Create**.</span></span>

6. <span data-ttu-id="469c7-123">Especifique un **nombre** para su máquina de red y considere la posibilidad de acciones Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="469c7-123">Specify a **Name** for your virtual network, and consider doing hello following:</span></span>
    * <span data-ttu-id="469c7-124">Puede elegir tooconfigure **espacio de direcciones** o **recuento máximo de VM** para esta red.</span><span class="sxs-lookup"><span data-stu-id="469c7-124">You can choose tooconfigure **Address space** or **Maximum VM count** for this network.</span></span>
    * <span data-ttu-id="469c7-125">Puede dejar hello **servidor DNS** establecer como **ninguno** por ahora.</span><span class="sxs-lookup"><span data-stu-id="469c7-125">You can leave hello **DNS server** setting as **None** for now.</span></span> <span data-ttu-id="469c7-126">Puede actualizar la configuración de hello después de habilitar servicios de dominio de Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="469c7-126">You can update hello setting after you enable Azure Active Directory Domain Services.</span></span>
7. <span data-ttu-id="469c7-127">Hola **ubicación** lista desplegable, seleccione una región de Azure admitida.</span><span class="sxs-lookup"><span data-stu-id="469c7-127">In hello **Location** drop-down list, select a supported Azure region.</span></span>  
    <span data-ttu-id="469c7-128">tooascertain Hola regiones de Azure en el que está disponible servicios de dominio de Active Directory de Azure, consulte [servicios de Azure por región](https://azure.microsoft.com/regions/#services/).</span><span class="sxs-lookup"><span data-stu-id="469c7-128">tooascertain hello Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
8. <span data-ttu-id="469c7-129">toocreate la red virtual, haga clic en **crear una red Virtual**.</span><span class="sxs-lookup"><span data-stu-id="469c7-129">toocreate your virtual network, click **Create a Virtual Network**.</span></span>

    ![Creación de una red virtual para Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. <span data-ttu-id="469c7-131">Después de crear una red virtual, seleccione Hola nombre de red virtual de hello y, a continuación, haga clic en hello **configurar** ficha.</span><span class="sxs-lookup"><span data-stu-id="469c7-131">After you've created a virtual network, select hello name of hello virtual network, and then click hello **Configure** tab.</span></span>

    ![Creación de una subred](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. <span data-ttu-id="469c7-133">En **espacios de direcciones de red virtual**, haga clic en **Agregar subred**y, a continuación, especifique una subred con el nombre de hello **AaddsSubnet**.</span><span class="sxs-lookup"><span data-stu-id="469c7-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with hello name **AaddsSubnet**.</span></span>

    ![Creación de una subred para Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. <span data-ttu-id="469c7-135">toocreate Hola subred, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="469c7-135">toocreate hello subnet, click **Save**.</span></span>


## <a name="next-step"></a><span data-ttu-id="469c7-136">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="469c7-136">Next step</span></span>
[<span data-ttu-id="469c7-137">Tarea 3: Habilitación de Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="469c7-137">Task 3: enable Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-enableaadds.md)
