---
title: "aaaConfigure de direcciones IP privadas para las máquinas virtuales: portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure de direcciones IP privadas de máquinas virtuales mediante Hola portal de Azure."
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
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="c8d46-103">Configurar las direcciones IP privadas para una máquina virtual mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c8d46-103">Configure private IP addresses for a virtual machine using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c8d46-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c8d46-104">Azure portal</span></span>](virtual-networks-static-private-ip-arm-pportal.md)
> * [<span data-ttu-id="c8d46-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8d46-105">PowerShell</span></span>](virtual-networks-static-private-ip-arm-ps.md)
> * [<span data-ttu-id="c8d46-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c8d46-106">Azure CLI</span></span>](virtual-networks-static-private-ip-arm-cli.md)
> * [<span data-ttu-id="c8d46-107">Portal de Azure (clásico)</span><span class="sxs-lookup"><span data-stu-id="c8d46-107">Azure portal (Classic)</span></span>](virtual-networks-static-private-ip-classic-pportal.md)
> * [<span data-ttu-id="c8d46-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="c8d46-108">PowerShell (Classic)</span></span>](virtual-networks-static-private-ip-classic-ps.md)
> * [<span data-ttu-id="c8d46-109">CLI de Azure (clásico)</span><span class="sxs-lookup"><span data-stu-id="c8d46-109">Azure CLI (Classic)</span></span>](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="c8d46-110">Este artículo trata el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8d46-110">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="c8d46-111">También puede [administrar dirección IP privada estática en el modelo de implementación clásica de hello](virtual-networks-static-private-ip-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="c8d46-111">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="c8d46-112">siguientes pasos de ejemplo de Hola esperan un entorno simple ya creado.</span><span class="sxs-lookup"><span data-stu-id="c8d46-112">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="c8d46-113">Si desea toorun pasos de hello, que se muestran en este documento, en primer lugar crear entorno de prueba de Hola se describe en [crear una red virtual](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="c8d46-113">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).</span></span>

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a><span data-ttu-id="c8d46-114">Cómo aborda toocreate una máquina virtual para la prueba de dirección IP estática privada</span><span class="sxs-lookup"><span data-stu-id="c8d46-114">How toocreate a VM for testing static private IP addresses</span></span>
<span data-ttu-id="c8d46-115">No se puede establecer una dirección IP privada estática durante la creación de hello de una máquina virtual en el modo de implementación del Administrador de recursos de hello mediante Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="c8d46-115">You cannot set a static private IP address during hello creation of a VM in hello Resource Manager deployment mode by using hello Azure portal.</span></span> <span data-ttu-id="c8d46-116">Primero deberá crear Hola VM, tehn establecer su privada toobe IP estática.</span><span class="sxs-lookup"><span data-stu-id="c8d46-116">You must create hello VM first, tehn set its private IP toobe static.</span></span>

<span data-ttu-id="c8d46-117">una máquina virtual denominada toocreate *DNS01* en hello *front-end* subred de una red virtual con el nombre *TestVNet*, siga estos pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="c8d46-117">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet*, follow hello steps below.</span></span>

1. <span data-ttu-id="c8d46-118">Desde un explorador, navegue toohttp://portal.azure.com y, si es necesario, inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="c8d46-118">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="c8d46-119">Haga clic en **NEW** > **proceso** > **Windows Server 2012 R2 Datacenter**, tenga en cuenta que hello **seleccionar un modelo de implementación** lista ya se muestran **el Administrador de recursos**y, a continuación, haga clic en **crear**, como se muestra en la siguiente ilustración de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8d46-119">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in hello figure below.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. <span data-ttu-id="c8d46-121">Hola **Fundamentos** hoja, escriba nombre Hola de hello VM toobe creado (*DNS01* en nuestro escenario), Hola cuenta de administrador local y la contraseña, como se muestra en la siguiente ilustración de Hola.</span><span class="sxs-lookup"><span data-stu-id="c8d46-121">In hello **Basics** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password, as seen in hello figure below.</span></span>
   
    ![Hoja Básico](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. <span data-ttu-id="c8d46-123">Realizar Hola seguro **ubicación** seleccionado es *Central US*, a continuación, haga clic en **seleccione existente** en **grupo de recursos**, a continuación, haga clic en **Grupo de recursos** , a continuación, haga clic en el nuevo, *TestRG*y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c8d46-123">Make sure hello **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.</span></span>
   
    ![Hoja Básico](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. <span data-ttu-id="c8d46-125">Hola **elegir un tamaño de** hoja, seleccione **estándar A1**y, a continuación, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="c8d46-125">In hello **Choose a size** blade, select **A1 Standard**, and then click **Select**.</span></span>
   
    ![Selección de una hoja de tamaño](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. <span data-ttu-id="c8d46-127">En el **configuración** hoja, asegúrese de hello seguro propiedades siguientes se establecen se establecen con valores de hello siguiente y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c8d46-127">In teh **Settings** blade, make sure hello following properties are set are set with hello values below, and then click **OK**.</span></span>
   
    <span data-ttu-id="c8d46-128">-**Cuenta de almacenamiento**: *vnetstorage*</span><span class="sxs-lookup"><span data-stu-id="c8d46-128">-**Storage account**: *vnetstorage*</span></span>
   
   * <span data-ttu-id="c8d46-129">**Red**: *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="c8d46-129">**Network**: *TestVNet*</span></span>
   * <span data-ttu-id="c8d46-130">**Subred**: *FrontEnd*</span><span class="sxs-lookup"><span data-stu-id="c8d46-130">**Subnet**: *FrontEnd*</span></span>
     
     ![Selección de una hoja de tamaño](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. <span data-ttu-id="c8d46-132">Hola **resumen** hoja, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c8d46-132">In hello **Summary** blade, click **OK**.</span></span> <span data-ttu-id="c8d46-133">Aviso Hola mosaico siguientes aparecen en el panel.</span><span class="sxs-lookup"><span data-stu-id="c8d46-133">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="c8d46-135">¿Cómo tooretrieve dirección IP estática privada información de dirección de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c8d46-135">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="c8d46-136">tooview Hola privada información direcciones IP estáticas para hello máquinas virtuales crean con hello los pasos descritos anteriormente, ejecute los pasos de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="c8d46-136">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="c8d46-137">En el portal de Azure de Azure de hello, haga clic en **examinar todos los** > **máquinas virtuales** > **DNS01** > **todos configuración de** > **interfaces de red** y, a continuación, haga clic en hello única interfaz de red enumerado.</span><span class="sxs-lookup"><span data-stu-id="c8d46-137">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on hello only network interface listed.</span></span>
   
    ![Implementación del icono de máquina virtual](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. <span data-ttu-id="c8d46-139">Hola **interfaz de red** hoja, haga clic en **toda la configuración de** > **direcciones IP** aviso hello y **asignación** y **Dirección IP** valores.</span><span class="sxs-lookup"><span data-stu-id="c8d46-139">In hello **Network interface** blade, click **All settings** > **IP addresses** and notice hello **Assignment** and **IP address** values.</span></span>
   
    ![Implementación del icono de máquina virtual](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="c8d46-141">Cómo tooadd una dirección IP estática privada direccionan tooan existente de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c8d46-141">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="c8d46-142">tooadd una toohello de dirección IP privada máquinas virtuales creadas mediante Hola pasos anteriores, estático, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c8d46-142">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="c8d46-143">De hello **direcciones IP** hoja mostrado anteriormente, haga clic en **estático** en **asignación**.</span><span class="sxs-lookup"><span data-stu-id="c8d46-143">From hello **IP addresses** blade shown above, click **Static** under **Assignment**.</span></span>
2. <span data-ttu-id="c8d46-144">Escriba *192.168.1.101* en **Dirección IP** y, después, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="c8d46-144">Type *192.168.1.101* for **IP address**, and then click **Save**.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> <span data-ttu-id="c8d46-146">Si después de hacer clic en **guardar** tenga en cuenta que la asignación de hello sigue establecida demasiado**dinámica**, significa que la dirección IP de Hola que escribió ya está en uso.</span><span class="sxs-lookup"><span data-stu-id="c8d46-146">If after clicking **Save** you notice that hello assignment is still set too**Dynamic**, it means that hello IP address you typed is already in use.</span></span> <span data-ttu-id="c8d46-147">Pruebe una dirección IP distinta.</span><span class="sxs-lookup"><span data-stu-id="c8d46-147">Try a different IP address.</span></span>
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="c8d46-148">¿Cómo tooremove una privada de direcciones IP estáticas de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c8d46-148">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="c8d46-149">tooremove Hola privada dirección IP estática de hello máquina virtual creada anteriormente, complete Hola siguiendo el paso:</span><span class="sxs-lookup"><span data-stu-id="c8d46-149">tooremove hello static private IP address from hello VM created above, complete hello following step:</span></span>

<span data-ttu-id="c8d46-150">De hello **direcciones IP** hoja mostrado anteriormente, haga clic en **dinámica** en **asignación**y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="c8d46-150">From hello **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8d46-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c8d46-151">Next steps</span></span>
* <span data-ttu-id="c8d46-152">Obtenga más información acerca de las [direcciones IP públicas reservadas](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="c8d46-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="c8d46-153">Obtenga información sobre las [direcciones IP públicas a nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="c8d46-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="c8d46-154">Consulte hello [API de REST para IP reservadas](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8d46-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

