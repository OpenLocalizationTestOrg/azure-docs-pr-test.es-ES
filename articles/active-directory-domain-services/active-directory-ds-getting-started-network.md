---
title: "Azure Active Directory Domain Services: introducción | Microsoft Docs"
description: "Habilitación de Azure Active Directory Domain Services mediante Azure Portal (versión preliminar)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7f420d60862adf61e4f21e5abac2932a742bd55d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-portal-preview"></a><span data-ttu-id="26433-103">Habilitación de Azure Active Directory Domain Services mediante Azure Portal (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="26433-103">Enable Azure Active Directory Domain Services using the Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="26433-104">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="26433-104">Before you begin</span></span>
<span data-ttu-id="26433-105">Consulte [Consideraciones de red de Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="26433-105">Refer to [Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="26433-106">Tarea 2: Configuración de red</span><span class="sxs-lookup"><span data-stu-id="26433-106">Task 2: configure network settings</span></span>
<span data-ttu-id="26433-107">La siguiente tarea de configuración es crear una red virtual de Azure y una subred dedicada en ella.</span><span class="sxs-lookup"><span data-stu-id="26433-107">The next configuration task is to create an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="26433-108">Puede habilitar Azure Active Directory Domain Services en esta subred dentro de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="26433-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="26433-109">También puede seleccionar una red virtual existente y crear la subred dedicada en ella.</span><span class="sxs-lookup"><span data-stu-id="26433-109">You may also pick an existing virtual network and create the dedicated subnet within it.</span></span>

1. <span data-ttu-id="26433-110">Haga clic en **Red virtual** para seleccionar una red virtual.</span><span class="sxs-lookup"><span data-stu-id="26433-110">Click **Virtual network** to select a virtual network.</span></span>
2. <span data-ttu-id="26433-111">En la hoja **Elegir red virtual**, se ven todas las redes virtuales existentes.</span><span class="sxs-lookup"><span data-stu-id="26433-111">On the **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="26433-112">Solo se ven las redes virtuales que pertenecen al grupo de recursos y la ubicación de Azure que ha seleccionado en la página **Conceptos básicos** del asistente.</span><span class="sxs-lookup"><span data-stu-id="26433-112">You see only the virtual networks that belong to the resource group and Azure location you have selected on the **Basics** wizard page.</span></span>

3. <span data-ttu-id="26433-113">Elija la red virtual en la que Azure AD Domain Services debe habilitarse.</span><span class="sxs-lookup"><span data-stu-id="26433-113">Choose the virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="26433-114">Haga clic en **Crear nuevo** si prefiere crear una nueva red virtual.</span><span class="sxs-lookup"><span data-stu-id="26433-114">Click **Create new**, if you prefer to create a new virtual network.</span></span> <span data-ttu-id="26433-115">Se recomienda usar una subred dedicada para Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="26433-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="26433-116">Si elige una red virtual existente, [cree una subred dedicada con la extensión de redes virtuales](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) y después selecciónela.</span><span class="sxs-lookup"><span data-stu-id="26433-116">If you pick an existing virtual network, [create a dedicated subnet using the virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![Seleccionar una red virtual](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="26433-118">Haga clic en **Subred** para seleccionar la subred dedicada en esta red virtual, en la que va a habilitar su nuevo dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="26433-118">Click **Subnet** to pick the dedicated subnet in this virtual network, within which to enable your new managed domain.</span></span> <span data-ttu-id="26433-119">En la hoja **Crear subred**, especifique el nombre de la subred y haga clic en **Aceptar** cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="26433-119">In the **Create subnet** blade, specify a name for the subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="26433-120">Por ejemplo, cree una subred llamada 'DomainServices', lo que facilitará que otros administradores sepan lo que se implementa en la subred.</span><span class="sxs-lookup"><span data-stu-id="26433-120">For example, create a subnet with the name 'DomainServices', making it easy for other administrators to understand what is deployed within the subnet.</span></span>

    ![Elegir una subred en la red virtual](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="26433-122">**Directrices para seleccionar una subred**</span><span class="sxs-lookup"><span data-stu-id="26433-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="26433-123">Use una subred dedicada para Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="26433-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="26433-124">No implemente otras máquinas virtuales en esta subred.</span><span class="sxs-lookup"><span data-stu-id="26433-124">Do not deploy any other virtual machines to this subnet.</span></span> <span data-ttu-id="26433-125">Esta configuración permite configurar grupos de seguridad de red (NSG) para las cargas de trabajo o máquinas virtuales sin interrumpir el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="26433-125">This configuration enables you to configure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="26433-126">Para obtener detalles, vea [Consideraciones de red de Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="26433-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="26433-127">No seleccione la subred Gateway para implementar Azure AD Domain Services, porque no es una configuración admitida.</span><span class="sxs-lookup"><span data-stu-id="26433-127">Do not select the Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="26433-128">Asegúrese de que la subred que ha seleccionado tiene suficiente espacio de direcciones disponible (al menos entre 3 y 5 direcciones IP disponibles).</span><span class="sxs-lookup"><span data-stu-id="26433-128">Ensure that the subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="26433-129">Cuando haya terminado, haga clic en **Aceptar** para ir a la página **Grupo de administradores** del asistente.</span><span class="sxs-lookup"><span data-stu-id="26433-129">When you are done, click **OK** to move on to the **Administrator group** page of the wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="26433-130">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="26433-130">Next step</span></span>
[<span data-ttu-id="26433-131">Tarea 3: Configuración del grupo administrativo y habilitación de Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="26433-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
