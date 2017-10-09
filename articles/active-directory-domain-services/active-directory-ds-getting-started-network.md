---
title: "Azure Active Directory Domain Services: introducción | Microsoft Docs"
description: Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure (vista previa)
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
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a><span data-ttu-id="da9f5-103">Habilitar Azure Active Directory Domain Services mediante Hola portal de Azure (vista previa)</span><span class="sxs-lookup"><span data-stu-id="da9f5-103">Enable Azure Active Directory Domain Services using hello Azure portal (Preview)</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="da9f5-104">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="da9f5-104">Before you begin</span></span>
<span data-ttu-id="da9f5-105">Consulte demasiado[consideraciones de red para servicios de dominio de Active Directory de Azure](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="da9f5-105">Refer too[Networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>


## <a name="task-2-configure-network-settings"></a><span data-ttu-id="da9f5-106">Tarea 2: Configuración de red</span><span class="sxs-lookup"><span data-stu-id="da9f5-106">Task 2: configure network settings</span></span>
<span data-ttu-id="da9f5-107">tarea de configuración siguiente Hello es toocreate una red virtual de Azure y una subred dedicada dentro de él.</span><span class="sxs-lookup"><span data-stu-id="da9f5-107">hello next configuration task is toocreate an Azure virtual network and a dedicated subnet within it.</span></span> <span data-ttu-id="da9f5-108">Puede habilitar Azure Active Directory Domain Services en esta subred dentro de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="da9f5-108">You enable Azure Active Directory Domain Services in this subnet within your virtual network.</span></span> <span data-ttu-id="da9f5-109">También puede elegir una red virtual existente y crear una subred de hello dedicado dentro de él.</span><span class="sxs-lookup"><span data-stu-id="da9f5-109">You may also pick an existing virtual network and create hello dedicated subnet within it.</span></span>

1. <span data-ttu-id="da9f5-110">Haga clic en **red Virtual** tooselect una red virtual.</span><span class="sxs-lookup"><span data-stu-id="da9f5-110">Click **Virtual network** tooselect a virtual network.</span></span>
2. <span data-ttu-id="da9f5-111">En hello **red virtual de elegir** hoja, verá todas las redes virtuales existentes.</span><span class="sxs-lookup"><span data-stu-id="da9f5-111">On hello **Choose virtual network** blade, you see all existing virtual networks.</span></span> <span data-ttu-id="da9f5-112">Vea solo Hola redes virtuales que pertenecen a grupo de recursos de toohello y ubicación de Azure que seleccionó en hello **Fundamentos** página del asistente.</span><span class="sxs-lookup"><span data-stu-id="da9f5-112">You see only hello virtual networks that belong toohello resource group and Azure location you have selected on hello **Basics** wizard page.</span></span>

3. <span data-ttu-id="da9f5-113">Elija la red virtual de hello en el que deben habilitarse servicios de dominio de AD de Azure.</span><span class="sxs-lookup"><span data-stu-id="da9f5-113">Choose hello virtual network in which Azure AD Domain Services should be enabled.</span></span> <span data-ttu-id="da9f5-114">Haga clic en **crear nuevo**, si lo prefiere toocreate una nueva red virtual.</span><span class="sxs-lookup"><span data-stu-id="da9f5-114">Click **Create new**, if you prefer toocreate a new virtual network.</span></span> <span data-ttu-id="da9f5-115">Se recomienda usar una subred dedicada para Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="da9f5-115">We highly recommend using a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="da9f5-116">Si elige una red virtual existente, [crear una subred dedicada con la extensión de redes virtuales de hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) y, a continuación, seleccione esa subred.</span><span class="sxs-lookup"><span data-stu-id="da9f5-116">If you pick an existing virtual network, [create a dedicated subnet using hello virtual networks extension](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and then pick that subnet.</span></span> 

    ![Seleccionar una red virtual](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. <span data-ttu-id="da9f5-118">Haga clic en **subred** toopick Hola subred dedicada en esta red virtual, en qué tooenable su nuevo administrado dominio.</span><span class="sxs-lookup"><span data-stu-id="da9f5-118">Click **Subnet** toopick hello dedicated subnet in this virtual network, within which tooenable your new managed domain.</span></span> <span data-ttu-id="da9f5-119">Hola **crear subred** hoja, especifique un nombre para la subred de Hola y haga clic en **Aceptar** cuando haya terminado.</span><span class="sxs-lookup"><span data-stu-id="da9f5-119">In hello **Create subnet** blade, specify a name for hello subnet, and click **OK** when you're done.</span></span> <span data-ttu-id="da9f5-120">Por ejemplo, puede crear una subred con el nombre de hello 'DomainServices', lo que facilita para otro administradores toounderstand lo que se implementa dentro de la subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="da9f5-120">For example, create a subnet with hello name 'DomainServices', making it easy for other administrators toounderstand what is deployed within hello subnet.</span></span>

    ![Seleccione la subred de red virtual de Hola](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > <span data-ttu-id="da9f5-122">**Directrices para seleccionar una subred**</span><span class="sxs-lookup"><span data-stu-id="da9f5-122">**Guidelines for selecting a subnet**</span></span>
  > 1. <span data-ttu-id="da9f5-123">Use una subred dedicada para Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="da9f5-123">Use a dedicated subnet for Azure AD Domain Services.</span></span> <span data-ttu-id="da9f5-124">No se implementa ninguna otra subred de toothis de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="da9f5-124">Do not deploy any other virtual machines toothis subnet.</span></span> <span data-ttu-id="da9f5-125">Esta configuración permite a tooconfigure grupos de seguridad de red (NSG) para las máquinas virtuales o las cargas de trabajo sin interrumpir el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="da9f5-125">This configuration enables you tooconfigure network security groups (NSGs) for your workloads/virtual machines without disrupting your managed domain.</span></span> <span data-ttu-id="da9f5-126">Para obtener detalles, vea [Consideraciones de red de Azure Active Directory Domain Services](active-directory-ds-networking.md).</span><span class="sxs-lookup"><span data-stu-id="da9f5-126">For details, see [networking considerations for Azure Active Directory Domain Services](active-directory-ds-networking.md).</span></span>
  2. <span data-ttu-id="da9f5-127">No seleccione subred de puerta de enlace de Hola para implementar los servicios de dominio de Active Directory de Azure, porque no es una configuración admitida.</span><span class="sxs-lookup"><span data-stu-id="da9f5-127">Do not select hello Gateway subnet for deploying Azure AD Domain Services, because it is not a supported configuration.</span></span>
  3. <span data-ttu-id="da9f5-128">Asegúrese de que ha seleccionado la subred hello tiene suficiente espacio de direcciones disponible - direcciones IP disponibles de al menos 3 a 5.</span><span class="sxs-lookup"><span data-stu-id="da9f5-128">Ensure that hello subnet you've selected has sufficient available address space - at least 3-5 available IP addresses.</span></span>
  >

5. <span data-ttu-id="da9f5-129">Cuando haya terminado, haga clic en **Aceptar** toomove en toohello **grupo de administradores** página del Asistente para saludo.</span><span class="sxs-lookup"><span data-stu-id="da9f5-129">When you are done, click **OK** toomove on toohello **Administrator group** page of hello wizard.</span></span>


## <a name="next-step"></a><span data-ttu-id="da9f5-130">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="da9f5-130">Next step</span></span>
[<span data-ttu-id="da9f5-131">Tarea 3: Configuración del grupo administrativo y habilitación de Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="da9f5-131">Task 3: configure administrative group and enable Azure AD Domain Services</span></span>](active-directory-ds-getting-started-admingroup.md)
