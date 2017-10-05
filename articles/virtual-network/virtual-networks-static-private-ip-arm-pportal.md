---
title: "Configuración de direcciones IP privadas para máquinas virtuales (Azure Portal) | Microsoft Docs"
description: "Obtenga información sobre cómo configurar direcciones IP privadas para máquinas virtuales mediante Azure Portal."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 672462fad715758e50680fa5bade4b1f9d50e6e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-portal"></a><span data-ttu-id="6f16f-103">Configuración de direcciones IP privadas para una máquina virtual mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6f16f-103">Configure private IP addresses for a virtual machine using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6f16f-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6f16f-104">Azure portal</span></span>](virtual-networks-static-private-ip-arm-pportal.md)
> * [<span data-ttu-id="6f16f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f16f-105">PowerShell</span></span>](virtual-networks-static-private-ip-arm-ps.md)
> * [<span data-ttu-id="6f16f-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="6f16f-106">Azure CLI</span></span>](virtual-networks-static-private-ip-arm-cli.md)
> * [<span data-ttu-id="6f16f-107">Portal de Azure (clásico)</span><span class="sxs-lookup"><span data-stu-id="6f16f-107">Azure portal (Classic)</span></span>](virtual-networks-static-private-ip-classic-pportal.md)
> * [<span data-ttu-id="6f16f-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="6f16f-108">PowerShell (Classic)</span></span>](virtual-networks-static-private-ip-classic-ps.md)
> * [<span data-ttu-id="6f16f-109">CLI de Azure (clásico)</span><span class="sxs-lookup"><span data-stu-id="6f16f-109">Azure CLI (Classic)</span></span>](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="6f16f-110">Este artículo trata sobre el modelo de implementación del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="6f16f-110">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="6f16f-111">También puedes [Administrar la dirección IP privada estática en el modelo de implementación clásica](virtual-networks-static-private-ip-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="6f16f-111">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="6f16f-112">En los siguientes pasos de ejemplo se presupone que ya se ha creado un entorno simple.</span><span class="sxs-lookup"><span data-stu-id="6f16f-112">The sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="6f16f-113">Si desea ejecutar los pasos que aparecen en este documento, cree primero el entorno de prueba descrito en [creación de una red virtual](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="6f16f-113">If you want to run the steps as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).</span></span>

## <a name="how-to-create-a-vm-for-testing-static-private-ip-addresses"></a><span data-ttu-id="6f16f-114">Creación de una VM para probar las direcciones IP privadas estáticas</span><span class="sxs-lookup"><span data-stu-id="6f16f-114">How to create a VM for testing static private IP addresses</span></span>
<span data-ttu-id="6f16f-115">No se puede establecer una dirección IP privada estática durante la creación de una VM en el modo de implementación del Administrador de recursos mediante el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="6f16f-115">You cannot set a static private IP address during the creation of a VM in the Resource Manager deployment mode by using the Azure portal.</span></span> <span data-ttu-id="6f16f-116">En primer lugar debe crear la VM, tehn establece la IP privada como estática.</span><span class="sxs-lookup"><span data-stu-id="6f16f-116">You must create the VM first, tehn set its private IP to be static.</span></span>

<span data-ttu-id="6f16f-117">Para crear una VM denominada *DNS01* en la subred *FrontEnd* de una red virtual denominada *TestVNet*, siga los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="6f16f-117">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet*, follow the steps below.</span></span>

1. <span data-ttu-id="6f16f-118">Desde un explorador, vaya a http://portal.azure.com y, si fuera necesario, inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="6f16f-118">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="6f16f-119">Haga clic en **NUEVO** > **Proceso** > **Windows Server 2012 R2 Datacenter**. Tenga en cuenta que la lista **Seleccionar un modelo de implementación** ya muestre **Resource Manager** y, después, haga clic en **Crear**, como se muestra en la figura siguiente.</span><span class="sxs-lookup"><span data-stu-id="6f16f-119">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that the **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in the figure below.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. <span data-ttu-id="6f16f-121">En la hoja **Básico** , especifique el nombre de la VM que se va a crear (*DNS01* en nuestro escenario), la cuenta de administrador local y la contraseña, como se muestra en la figura siguiente.</span><span class="sxs-lookup"><span data-stu-id="6f16f-121">In the **Basics** blade, enter the name of the VM to be created (*DNS01* in our scenario), the local administrator account, and password, as seen in the figure below.</span></span>
   
    ![Hoja Básico](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. <span data-ttu-id="6f16f-123">Asegúrese de que la **Ubicación** seleccionada sea *Centro de EE. UU.* y, después, haga clic en **Seleccionar existente** en **Grupo de recursos**. Después, haga clic de nuevo en **Grupo de recursos**, luego en *TestRG* y, después, en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6f16f-123">Make sure the **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.</span></span>
   
    ![Hoja Básico](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. <span data-ttu-id="6f16f-125">En la hoja **Elegir un tamaño**, seleccione **A1 Estándar** y, después, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="6f16f-125">In the **Choose a size** blade, select **A1 Standard**, and then click **Select**.</span></span>
   
    ![Selección de una hoja de tamaño](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. <span data-ttu-id="6f16f-127">En la hoja **Configuración**, asegúrese de que se establecen las siguientes propiedades con los siguientes valores y, después, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6f16f-127">In teh **Settings** blade, make sure the following properties are set are set with the values below, and then click **OK**.</span></span>
   
    <span data-ttu-id="6f16f-128">-**Cuenta de almacenamiento**: *vnetstorage*</span><span class="sxs-lookup"><span data-stu-id="6f16f-128">-**Storage account**: *vnetstorage*</span></span>
   
   * <span data-ttu-id="6f16f-129">**Red**: *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="6f16f-129">**Network**: *TestVNet*</span></span>
   * <span data-ttu-id="6f16f-130">**Subred**: *FrontEnd*</span><span class="sxs-lookup"><span data-stu-id="6f16f-130">**Subnet**: *FrontEnd*</span></span>
     
     ![Selección de una hoja de tamaño](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. <span data-ttu-id="6f16f-132">En la hoja **Resumen**, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6f16f-132">In the **Summary** blade, click **OK**.</span></span> <span data-ttu-id="6f16f-133">Observe el icono siguiente que aparece en el panel.</span><span class="sxs-lookup"><span data-stu-id="6f16f-133">Notice the tile below displayed in your dashboard.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="6f16f-135">Recuperación de la información de la dirección IP privada estática para una VM</span><span class="sxs-lookup"><span data-stu-id="6f16f-135">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="6f16f-136">Para ver la información de la dirección IP privada estática para la VM que creó con los pasos anteriores, ejecute los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="6f16f-136">To view the static private IP address information for the VM created with the steps above, execute the steps below.</span></span>

1. <span data-ttu-id="6f16f-137">En Azure Portal, haga clic en **EXAMINAR TODO** > **Máquinas virtuales** > **DNS01** > **Toda la configuración** > **Interfaces de red** y, después, haga clic en la única interfaz de red que aparece.</span><span class="sxs-lookup"><span data-stu-id="6f16f-137">From the Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on the only network interface listed.</span></span>
   
    ![Implementación del icono de máquina virtual](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. <span data-ttu-id="6f16f-139">En la hoja **Interfaz de red**, haga clic en **Toda la configuración** > **Direcciones IP** y vea los valores **Asignación** y **Dirección IP**.</span><span class="sxs-lookup"><span data-stu-id="6f16f-139">In the **Network interface** blade, click **All settings** > **IP addresses** and notice the **Assignment** and **IP address** values.</span></span>
   
    ![Implementación del icono de máquina virtual](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="6f16f-141">Adición de una dirección IP privada estática a una VM existente</span><span class="sxs-lookup"><span data-stu-id="6f16f-141">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="6f16f-142">Para agregar una dirección IP privada estática a la VM creada con los pasos anteriores, siga los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="6f16f-142">To add a static private IP address to the VM created using the steps above, follow the steps below:</span></span>

1. <span data-ttu-id="6f16f-143">En la hoja **Direcciones IP** que se muestra a continuación, haga clic en **Estática** en **Asignación**.</span><span class="sxs-lookup"><span data-stu-id="6f16f-143">From the **IP addresses** blade shown above, click **Static** under **Assignment**.</span></span>
2. <span data-ttu-id="6f16f-144">Escriba *192.168.1.101* en **Dirección IP** y, después, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6f16f-144">Type *192.168.1.101* for **IP address**, and then click **Save**.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> <span data-ttu-id="6f16f-146">Si después de hacer clic en **Guardar** se da cuenta de que la asignación sigue establecida en **Dinámica**, significa que la dirección IP que ha escrito sigue estando en uso.</span><span class="sxs-lookup"><span data-stu-id="6f16f-146">If after clicking **Save** you notice that the assignment is still set to **Dynamic**, it means that the IP address you typed is already in use.</span></span> <span data-ttu-id="6f16f-147">Pruebe una dirección IP distinta.</span><span class="sxs-lookup"><span data-stu-id="6f16f-147">Try a different IP address.</span></span>
> 
> 

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="6f16f-148">Eliminación de una dirección IP privada estática de una VM</span><span class="sxs-lookup"><span data-stu-id="6f16f-148">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="6f16f-149">Para quitar la dirección IP privada estática de la máquina virtual creada anteriormente, siga este paso:</span><span class="sxs-lookup"><span data-stu-id="6f16f-149">To remove the static private IP address from the VM created above, complete the following step:</span></span>

<span data-ttu-id="6f16f-150">En la hoja **Direcciones IP** que se muestra arriba, haga clic en **Dinámica** en **Asignación** y, después, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="6f16f-150">From the **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f16f-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6f16f-151">Next steps</span></span>
* <span data-ttu-id="6f16f-152">Obtenga más información acerca de las [direcciones IP públicas reservadas](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="6f16f-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="6f16f-153">Obtenga información sobre las [direcciones IP públicas a nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="6f16f-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="6f16f-154">Consulte las [API de REST de IP reservada](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f16f-154">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

