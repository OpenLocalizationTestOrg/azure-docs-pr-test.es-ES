---
title: "aaaConfigure de direcciones IP privadas para las máquinas virtuales (clásico): portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure de direcciones IP privadas de máquinas virtuales (clásicas) mediante Hola portal de Azure."
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
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a><span data-ttu-id="bd752-103">Configurar las direcciones IP privadas para una máquina virtual (clásica) mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bd752-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="bd752-104">Este artículo trata el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="bd752-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="bd752-105">También puede [administrar una dirección IP privada estática en el modelo de implementación del Administrador de recursos de hello](virtual-networks-static-private-ip-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="bd752-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="bd752-106">siguientes pasos de ejemplo de Hola esperan un entorno simple ya creado.</span><span class="sxs-lookup"><span data-stu-id="bd752-106">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="bd752-107">Si desea toorun pasos de hello, que se muestran en este documento, en primer lugar crear entorno de prueba de Hola se describe en [crear una red virtual](virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="bd752-107">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="bd752-108">¿Cómo toospecify una privada de direcciones IP estáticas al crear una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bd752-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="bd752-109">una máquina virtual denominada toocreate *DNS01* en hello *front-end* subred de una red virtual denominada *TestVNet* con una dirección IP estática privada de *192.168.1.101*, Siga los pasos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="bd752-109">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="bd752-110">Desde un explorador, navegue toohttp://portal.azure.com y, si es necesario, inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd752-110">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="bd752-111">Haga clic en **NEW** > **proceso** > **Windows Server 2012 R2 Datacenter**, tenga en cuenta que hello **seleccionar un modelo de implementación** lista ya se muestran **clásico**y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="bd752-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="bd752-113">Hola **crear VM** hoja, escriba nombre Hola de hello VM toobe creado (*DNS01* en nuestro escenario), Hola cuenta de administrador local y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="bd752-113">In hello **Create VM** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="bd752-115">Haga clic en **Configuración opcional** > **Red** > **Virtual Network** y en **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="bd752-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="bd752-116">Si **TestVNet** no está disponible, asegúrese de que está utilizando hello *Central US* ubicación y se ha creado el entorno de prueba de hello descrito al principio de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="bd752-116">If **TestVNet** is not available, make sure you are using hello *Central US* location and have created hello test environment described at hello beginning of this article.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="bd752-118">Hola **red** hoja, asegúrese de que Hola la subred seleccionada actualmente es *front-end*, a continuación, haga clic en **direcciones IP**, en **delaasignacióndedireccionesIP** haga clic en **estático**y, a continuación, escriba *192.168.1.101* para **dirección IP** tal como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="bd752-118">In hello **Network** blade, make sure hello subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="bd752-120">Haga clic en **Aceptar** en hello **direcciones IP** blade, a continuación, haga clic en **Aceptar** en hello **red** hoja y haga clic en **Aceptar**Hola **configuración opcional** hoja.</span><span class="sxs-lookup"><span data-stu-id="bd752-120">Click **OK** in hello **IP addresses** blade, then click **OK** in hello **Network** blade, and click **OK** in hello **Optional config** blade.</span></span>
7. <span data-ttu-id="bd752-121">Hola **crear VM** hoja, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="bd752-121">In hello **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="bd752-122">Aviso Hola mosaico siguientes aparecen en el panel.</span><span class="sxs-lookup"><span data-stu-id="bd752-122">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="bd752-124">¿Cómo tooretrieve dirección IP estática privada información de dirección de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bd752-124">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="bd752-125">tooview Hola privada información direcciones IP estáticas para hello máquinas virtuales crean con hello los pasos descritos anteriormente, ejecute los pasos de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="bd752-125">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="bd752-126">En el portal de Azure de Azure de hello, haga clic en **examinar todos los** > **máquinas virtuales (clásicas)** > **DNS01**  >   **Todas las configuraciones** > **direcciones IP** y observe Hola asignación de direcciones IP y la dirección IP, tal como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="bd752-126">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice hello IP address assignment and IP address as seen below.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="bd752-128">¿Cómo tooremove una privada de direcciones IP estáticas de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bd752-128">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="bd752-129">tooremove Hola privada dirección IP estática de hello virtual creado anteriormente, siga los pasos de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="bd752-129">tooremove hello static private IP address from hello VM created above, follow hello steps below.</span></span>

1. <span data-ttu-id="bd752-130">De hello **direcciones IP** hoja mostrado anteriormente, haga clic en **dinámica** toohello derecha de **asignación de direcciones IP**, a continuación, haga clic en **guardar**y, a continuación, Haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="bd752-130">From hello **IP addresses** blade shown above, click **Dynamic** toohello right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Creación de una VM en el Portal de Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="bd752-132">Cómo tooadd una dirección IP estática privada direccionan tooan existente de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bd752-132">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="bd752-133">tooadd una toohello de dirección IP privada máquinas virtuales creadas mediante Hola pasos anteriores, estático, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="bd752-133">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="bd752-134">De hello **direcciones IP** hoja mostrado anteriormente, haga clic en **estático** toohello derecha de **asignación de direcciones IP**.</span><span class="sxs-lookup"><span data-stu-id="bd752-134">From hello **IP addresses** blade shown above, click **Static** toohello right of **IP address assignment**.</span></span>
2. <span data-ttu-id="bd752-135">Escriba *192.168.1.101* en **Dirección IP** y haga clic en **Guardar** y en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="bd752-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd752-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bd752-136">Next steps</span></span>
* <span data-ttu-id="bd752-137">Obtenga más información acerca de las [direcciones IP públicas reservadas](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="bd752-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="bd752-138">Obtenga información sobre las [direcciones IP públicas a nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="bd752-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="bd752-139">Consulte hello [API de REST para IP reservadas](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="bd752-139">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

