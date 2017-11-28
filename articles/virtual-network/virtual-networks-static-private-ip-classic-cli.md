---
title: "aaaConfigure de direcciones IP privadas para las máquinas virtuales (clásicas) - 1.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure de direcciones IP privadas de máquinas virtuales (clásicas) mediante hello Azure interfaz de línea de comandos (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a><span data-ttu-id="0b9e0-103">Configurar las direcciones IP privadas para una máquina virtual (clásica) mediante Hola 1.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="0b9e0-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="0b9e0-104">Este artículo trata el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="0b9e0-105">También puede [administrar una dirección IP privada estática en el modelo de implementación del Administrador de recursos de hello](virtual-networks-static-private-ip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0b9e0-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-cli.md).</span></span>

<span data-ttu-id="0b9e0-106">comandos de CLI de Azure de ejemplo de Hola a continuación esperan un entorno simple ya creado.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-106">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="0b9e0-107">Si desea toorun comandos de hello, que se muestran en este documento, en primer lugar crear entorno de prueba de Hola se describe en [crear una red virtual](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0b9e0-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="0b9e0-108">¿Cómo toospecify una privada de direcciones IP estáticas al crear una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0b9e0-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="0b9e0-109">toocreate una nueva máquina virtual denominada *DNS01* en un nuevo servicio de nube denominado *TestService* en función de escenario de hello anterior, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0b9e0-109">toocreate a new VM named *DNS01* in a new cloud service named *TestService* based on hello scenario above, follow these steps:</span></span>

1. <span data-ttu-id="0b9e0-110">Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="0b9e0-111">Ejecute hello **crear servicio de azure** comando servicio en la nube toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-111">Run hello **azure service create** command toocreate hello cloud service.</span></span>
   
        azure service create TestService --location uscentral
   
    <span data-ttu-id="0b9e0-112">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="0b9e0-112">Expected output:</span></span>
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. <span data-ttu-id="0b9e0-113">Ejecute hello **azure crear vm** comando toocreate hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-113">Run hello **azure create vm** command toocreate hello VM.</span></span> <span data-ttu-id="0b9e0-114">Observe el valor de Hola para una dirección IP privada estática.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-114">Notice hello value for a static private IP address.</span></span> <span data-ttu-id="0b9e0-115">lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-115">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    <span data-ttu-id="0b9e0-116">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="0b9e0-116">Expected output:</span></span>
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * <span data-ttu-id="0b9e0-117">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-117">**-l (or --location)**.</span></span> <span data-ttu-id="0b9e0-118">Región de Azure donde se creará Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-118">Azure region where hello VM will be created.</span></span> <span data-ttu-id="0b9e0-119">En este escenario, *centralus*.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-119">For our scenario, *centralus*.</span></span>
   * <span data-ttu-id="0b9e0-120">**-n (o --vm-name)**.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-120">**-n (or --vm-name)**.</span></span> <span data-ttu-id="0b9e0-121">Nombre de hello VM toobe creado.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-121">Name of hello VM toobe created.</span></span>
   * <span data-ttu-id="0b9e0-122">**-w (o --virtual-network-name)**.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-122">**-w (or --virtual-network-name)**.</span></span> <span data-ttu-id="0b9e0-123">Nombre de red virtual donde se creará Hola VM hello.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-123">Name of hello VNet where hello VM will be created.</span></span> 
   * <span data-ttu-id="0b9e0-124">**-S (o --static-ip)**.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-124">**-S (or --static-ip)**.</span></span> <span data-ttu-id="0b9e0-125">Privada dirección IP estática para hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-125">Static private IP address for hello VM.</span></span>
   * <span data-ttu-id="0b9e0-126">**TestService**.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-126">**TestService**.</span></span> <span data-ttu-id="0b9e0-127">Nombre del servicio de nube de Hola donde se creará Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-127">Name of hello cloud service where hello VM will be created.</span></span>
   * <span data-ttu-id="0b9e0-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span></span> <span data-ttu-id="0b9e0-129">Imagen que se utiliza toocreate hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-129">Image used toocreate hello VM.</span></span>
   * <span data-ttu-id="0b9e0-130">**adminuser**.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-130">**adminuser**.</span></span> <span data-ttu-id="0b9e0-131">Administrador local para la máquina virtual de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-131">Local administrator for hello Windows VM.</span></span>
   * <span data-ttu-id="0b9e0-132">**AdminP@ssw0rd**.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-132">**AdminP@ssw0rd**.</span></span> <span data-ttu-id="0b9e0-133">Contraseña de administrador local para la máquina virtual de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="0b9e0-133">Local administrator password for hello Windows VM.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="0b9e0-134">¿Cómo tooretrieve dirección IP estática privada información de dirección de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0b9e0-134">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="0b9e0-135">información de hello máquinas virtuales crean con script de Hola anterior, ejecutar el siguiente comando de CLI de Azure de Hola de direcciones IP privada estático de tooview hello y observe el valor de hello para *StaticIP red*:</span><span class="sxs-lookup"><span data-stu-id="0b9e0-135">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello value for *Network StaticIP*:</span></span>

    azure vm static-ip show DNS01

<span data-ttu-id="0b9e0-136">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="0b9e0-136">Expected output:</span></span>

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="0b9e0-137">¿Cómo tooremove una privada de direcciones IP estáticas de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0b9e0-137">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="0b9e0-138">tooremove Hola privada dirección IP estática agregado toohello VM en script de Hola anteriormente, Hola ejecución siguiente comando de CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="0b9e0-138">tooremove hello static private IP address added toohello VM in hello script above, run hello following Azure CLI command:</span></span>

    azure vm static-ip remove DNS01

<span data-ttu-id="0b9e0-139">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="0b9e0-139">Expected output:</span></span>

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a><span data-ttu-id="0b9e0-140">¿Cómo tooadd un tooan IP estática privada VM existente</span><span class="sxs-lookup"><span data-stu-id="0b9e0-140">How tooadd a static private IP tooan existing VM</span></span>
<span data-ttu-id="0b9e0-141">tooadd una toohello de dirección IP privada estática máquinas virtuales creadas con script de Hola anteriormente, ejecución el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0b9e0-141">tooadd a static private IP address toohello VM created using hello script above, runt he following command:</span></span>

    azure vm static-ip set DNS01 192.168.1.101

<span data-ttu-id="0b9e0-142">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="0b9e0-142">Expected output:</span></span>

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a><span data-ttu-id="0b9e0-143">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0b9e0-143">Next steps</span></span>
* <span data-ttu-id="0b9e0-144">Obtenga más información acerca de las [direcciones IP públicas reservadas](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="0b9e0-144">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="0b9e0-145">Obtenga información sobre las [direcciones IP públicas a nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="0b9e0-145">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="0b9e0-146">Consulte hello [API de REST para IP reservadas](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="0b9e0-146">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

