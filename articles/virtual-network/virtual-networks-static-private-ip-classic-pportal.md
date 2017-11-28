---
title: "Configuración de direcciones IP privadas para máquinas virtuales (clásicas): Azure Portal | Microsoft Docs"
description: "Obtenga información sobre cómo configurar direcciones IP privadas para máquinas virtuales (clásicas) mediante Azure Portal."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bde6de3495c2909b63b1f85e420a4ff5e7ac2c1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-the-azure-portal"></a><span data-ttu-id="391ee-103">Configuración de direcciones IP privadas para una máquina virtual (clásica) mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="391ee-103">Configure private IP addresses for a virtual machine (Classic) using the Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="391ee-104">Este artículo trata sobre el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="391ee-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="391ee-105">También puede [administrar la dirección IP privada estática en el modelo de implementación del Administrador de recursos](virtual-networks-static-private-ip-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="391ee-105">You can also [manage a static private IP address in the Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="391ee-106">En los siguientes pasos de ejemplo se presupone que ya se ha creado un entorno simple.</span><span class="sxs-lookup"><span data-stu-id="391ee-106">The sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="391ee-107">Si desea ejecutar los pasos que aparecen en este documento, cree primero el entorno de prueba descrito en [creación de una red virtual](virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="391ee-107">If you want to run the steps as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-to-specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="391ee-108">Especificación de una dirección IP privada estática al crear una VM</span><span class="sxs-lookup"><span data-stu-id="391ee-108">How to specify a static private IP address when creating a VM</span></span>
<span data-ttu-id="391ee-109">Para crear una máquina virtual denominada *DNS01* en la subred *FrontEnd* de una red virtual denominada *TestVNet* con una dirección IP privada estática de *192.168.1.101*, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="391ee-109">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="391ee-110">Desde un explorador, vaya a http://portal.azure.com y, si fuera necesario, inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="391ee-110">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="391ee-111">Haga clic en **NUEVO** > **Compute** > **Windows Server 2012 R2 Datacenter**. Observe que la lista **Seleccionar un modelo de implementación** ya muestra **Clásico**. Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="391ee-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that the **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="391ee-113">En la hoja **Crear VM** , especifique el nombre de la VM que se va a crear (*DNS01* en nuestro escenario), la cuenta de administrador local y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="391ee-113">In the **Create VM** blade, enter the name of the VM to be created (*DNS01* in our scenario), the local administrator account, and password.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="391ee-115">Haga clic en **Configuración opcional** > **Red** > **Virtual Network** y en **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="391ee-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="391ee-116">Si **TestVNet** no está disponible, asegúrese de que usa la ubicación *Centro de EE. UU.* y que ha creado el entorno de prueba descrito al principio de este artículo.</span><span class="sxs-lookup"><span data-stu-id="391ee-116">If **TestVNet** is not available, make sure you are using the *Central US* location and have created the test environment described at the beginning of this article.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="391ee-118">En la hoja **Red**, asegúrese de que la subred seleccionada actualmente sea *FrontEnd* y haga clic en **Direcciones IP**; en **Asignación de dirección IP**, haga clic en **Estática** y especifique *192.168.1.101* para **Dirección IP** como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="391ee-118">In the **Network** blade, make sure the subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="391ee-120">Haga clic en **Aceptar** en la hoja **Direcciones IP** y en **Aceptar** en la hoja **Red**. Después, haga clic en **Aceptar** en la hoja **Configuración opcional**.</span><span class="sxs-lookup"><span data-stu-id="391ee-120">Click **OK** in the **IP addresses** blade, then click **OK** in the **Network** blade, and click **OK** in the **Optional config** blade.</span></span>
7. <span data-ttu-id="391ee-121">En la hoja **Crear máquina virtual**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="391ee-121">In the **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="391ee-122">Observe el icono siguiente que aparece en el panel.</span><span class="sxs-lookup"><span data-stu-id="391ee-122">Notice the tile below displayed in your dashboard.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="391ee-124">Recuperación de la información de la dirección IP privada estática para una VM</span><span class="sxs-lookup"><span data-stu-id="391ee-124">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="391ee-125">Para ver la información de la dirección IP privada estática para la VM que creó con los pasos anteriores, ejecute los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="391ee-125">To view the static private IP address information for the VM created with the steps above, execute the steps below.</span></span>

1. <span data-ttu-id="391ee-126">En Azure Portal, haga clic en **EXAMINAR TODO** > **Máquinas virtuales (clásico)** > **DNS01** > **Toda la configuración** > **Direcciones IP** y observe la asignación de dirección IP y la dirección IP que se muestran a continuación.</span><span class="sxs-lookup"><span data-stu-id="391ee-126">From the Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice the IP address assignment and IP address as seen below.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="391ee-128">Eliminación de una dirección IP privada estática de una VM</span><span class="sxs-lookup"><span data-stu-id="391ee-128">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="391ee-129">Para quitar la dirección IP privada estática de la VM creada anteriormente, siga los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="391ee-129">To remove the static private IP address from the VM created above, follow the steps below.</span></span>

1. <span data-ttu-id="391ee-130">En la hoja **Direcciones IP** que aparece a continuación, haga clic en **Dinámica** a la derecha de **Asignación de dirección IP**, en **Guardar** y después en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="391ee-130">From the **IP addresses** blade shown above, click **Dynamic** to the right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="391ee-132">Adición de una dirección IP privada estática a una VM existente</span><span class="sxs-lookup"><span data-stu-id="391ee-132">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="391ee-133">Para agregar una dirección IP privada estática a la VM creada con los pasos anteriores, siga los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="391ee-133">To add a static private IP address to the VM created using the steps above, follow the steps below:</span></span>

1. <span data-ttu-id="391ee-134">En la hoja **Direcciones IP** que se muestra a continuación, haga clic en **Estática** a la derecha de **Asignación de dirección IP**.</span><span class="sxs-lookup"><span data-stu-id="391ee-134">From the **IP addresses** blade shown above, click **Static** to the right of **IP address assignment**.</span></span>
2. <span data-ttu-id="391ee-135">Escriba *192.168.1.101* en **Dirección IP** y haga clic en **Guardar** y en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="391ee-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="391ee-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="391ee-136">Next steps</span></span>
* <span data-ttu-id="391ee-137">Obtenga más información acerca de las [direcciones IP públicas reservadas](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="391ee-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="391ee-138">Obtenga información sobre las [direcciones IP públicas a nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="391ee-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="391ee-139">Consulte las [API de REST de IP reservada](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="391ee-139">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

