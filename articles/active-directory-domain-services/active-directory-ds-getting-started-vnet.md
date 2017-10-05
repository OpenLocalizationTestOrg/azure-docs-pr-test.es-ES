---
title: "Azure Active Directory Domain Services: Creación o selección de una red virtual | Microsoft Docs"
description: "Habilitación de Azure Active Directory Domain Services mediante el Portal de Azure clásico"
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
ms.openlocfilehash: 457519b00b65b0157effe2d4aba033a1c99852e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-or-select-a-virtual-network-for-azure-active-directory-domain-services"></a><span data-ttu-id="dbb9c-103">Creación o selección de una red virtual para Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="dbb9c-103">Create or select a virtual network for Azure Active Directory Domain Services</span></span>
## <a name="before-you-begin"></a><span data-ttu-id="dbb9c-104">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="dbb9c-104">Before you begin</span></span>
<span data-ttu-id="dbb9c-105">Consulte [Consideraciones de red de Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="dbb9c-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>

## <a name="task-2-create-an-azure-virtual-network"></a><span data-ttu-id="dbb9c-106">Tarea 2: Creación de una red virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="dbb9c-106">Task 2: Create an Azure virtual network</span></span>
<span data-ttu-id="dbb9c-107">La siguiente tarea de configuración es crear una red virtual de Azure y una subred dentro de ella.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-107">The next configuration task is to create an Azure virtual network and a subnet within it.</span></span> <span data-ttu-id="dbb9c-108">Puede habilitar Azure Active Directory Domain Services en esta subred dentro de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="dbb9c-109">Si ya tiene una red virtual que quiere usar, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-109">If you have an existing virtual network that you’d prefer to use, you can skip this step.</span></span>

> [!NOTE]
> <span data-ttu-id="dbb9c-110">Asegúrese de que la red virtual de Azure que cree o elija usar con Azure Active Directory Domain Services pertenezca a una región de Azure que sea compatible con estos servicios.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-110">Make sure that the Azure virtual network you create or choose to use with Azure Active Directory Domain Services belongs to an Azure region that's supported by Azure Active Directory Domain Services.</span></span> <span data-ttu-id="dbb9c-111">Consulte la página [Servicios de Azure por región](https://azure.microsoft.com/regions/#services/) para saber en qué regiones de Azure está disponible Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-111">To ascertain the Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
>
><span data-ttu-id="dbb9c-112">Anote el nombre de la red virtual para asegurarse de que selecciona la red virtual adecuada al habilitar Azure Active Directory Domain Services en un paso posterior de la configuración.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-112">Note the name of the virtual network to ensure that you select the right virtual network when you enable Azure Active Directory Domain Services in a subsequent configuration step.</span></span>


<span data-ttu-id="dbb9c-113">Para crear una red virtual de Azure en la que desee habilitar Azure Active Directory Domain Services, siga estas instrucciones de configuración:</span><span class="sxs-lookup"><span data-stu-id="dbb9c-113">To create an Azure virtual network in which you want to enable Azure Active Directory Domain Services, follow these configuration instructions:</span></span>

1. <span data-ttu-id="dbb9c-114">Vaya al [Portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="dbb9c-114">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="dbb9c-115">En el panel izquierdo, seleccione **Redes**.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-115">In the left pane, select **Networks**.</span></span>

    <span data-ttu-id="dbb9c-116">![Nodo Redes](./media/active-directory-domain-services-getting-started/networks-node.png)</span><span class="sxs-lookup"><span data-stu-id="dbb9c-116">![Networks node](./media/active-directory-domain-services-getting-started/networks-node.png)</span></span>  
    <span data-ttu-id="dbb9c-117">Se abre la ventana **Redes virtuales**.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-117">The **Virtual Networks** window opens.</span></span>
3. <span data-ttu-id="dbb9c-118">En la parte inferior de la ventana, haga clic en **Nuevo** en el panel de tareas.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-118">In the task pane at the bottom of the window, click **New**.</span></span>

    ![Ventana Redes virtuales](./media/active-directory-domain-services-getting-started/virtual-networks.png)
4. <span data-ttu-id="dbb9c-120">Haga clic en **Network Services** y seleccione **Virtual Network**.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-120">Click **Network Services**, and then select **Virtual Network**.</span></span>

    ![Red virtual: creación rápida](./media/active-directory-domain-services-getting-started/virtual-network-quickcreate.png)
5. <span data-ttu-id="dbb9c-122">Haga clic en **Creación rápida** para crear una red virtual.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-122">To create a virtual network, click **Quick Create**.</span></span>

6. <span data-ttu-id="dbb9c-123">Especifique un **nombre** para la red virtual y tenga en cuenta las acciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="dbb9c-123">Specify a **Name** for your virtual network, and consider doing the following:</span></span>
    * <span data-ttu-id="dbb9c-124">También puede elegir configurar el **Espacio de direcciones** o el **Número máximo de VM** para esta red.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-124">You can choose to configure **Address space** or **Maximum VM count** for this network.</span></span>
    * <span data-ttu-id="dbb9c-125">Por ahora, puede dejar la configuración del **servidor DNS** establecida en **Ninguna**.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-125">You can leave the **DNS server** setting as **None** for now.</span></span> <span data-ttu-id="dbb9c-126">Puede actualizar la configuración después de habilitar Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-126">You can update the setting after you enable Azure Active Directory Domain Services.</span></span>
7. <span data-ttu-id="dbb9c-127">Seleccione una región de Azure compatible en la lista desplegable **Ubicación**.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-127">In the **Location** drop-down list, select a supported Azure region.</span></span>  
    <span data-ttu-id="dbb9c-128">Consulte la página [Servicios de Azure por región](https://azure.microsoft.com/regions/#services/) para saber en qué regiones de Azure está disponible Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-128">To ascertain the Azure regions in which Azure Active Directory Domain Services is available, see [Azure services by region](https://azure.microsoft.com/regions/#services/).</span></span>
8. <span data-ttu-id="dbb9c-129">Para crear la red virtual, haga clic en **Crear una red virtual**.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-129">To create your virtual network, click **Create a Virtual Network**.</span></span>

    ![Creación de una red virtual para Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet.png)
9. <span data-ttu-id="dbb9c-131">Después de crear una red virtual, selecciónela y haga clic en la pestaña **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-131">After you've created a virtual network, select the name of the virtual network, and then click the **Configure** tab.</span></span>

    ![Creación de una subred](./media/active-directory-domain-services-getting-started/create-vnet-properties.png)
10. <span data-ttu-id="dbb9c-133">En **Espacios de direcciones de la red virtual**, haga clic en **Agregar subred**y, a continuación, especifique una subred con el nombre **AaddsSubnet**.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-133">Under **virtual network address spaces**, click **add subnet**, and then specify a subnet with the name **AaddsSubnet**.</span></span>

    ![Creación de una subred para Azure Active Directory Domain Services](./media/active-directory-domain-services-getting-started/create-vnet-add-subnet.png)

11. <span data-ttu-id="dbb9c-135">Haga clic en **Guardar** para crear la subred.</span><span class="sxs-lookup"><span data-stu-id="dbb9c-135">To create the subnet, click **Save**.</span></span>


## <a name="next-step"></a><span data-ttu-id="dbb9c-136">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="dbb9c-136">Next step</span></span>
[<span data-ttu-id="dbb9c-137">Tarea 3: Habilitación de Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="dbb9c-137">Task 3: enable Azure Active Directory Domain Services</span></span>](active-directory-ds-getting-started-enableaadds.md)
