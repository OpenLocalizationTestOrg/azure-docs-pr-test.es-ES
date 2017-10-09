---
title: aaaUnderstand compartido direcciones IP en los laboratorios de desarrollo y pruebas de Azure | Documentos de Microsoft
description: "Obtener información sobre cómo laboratorios de desarrollo y pruebas de Azure usa compartido IP direcciones toominimize Hola pública IP direcciones necesarios tooaccess el laboratorio, máquinas virtuales."
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="fef4b-103">Direcciones IP compartidas en Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="fef4b-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="fef4b-104">Laboratorio de permite los laboratorios de desarrollo y pruebas Azure recurso compartido de las máquinas virtuales Hola pública IP dirección toominimize Hola tantos pública IP direcciones necesarios tooaccess el laboratorio individual de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="fef4b-104">Azure DevTest Labs lets lab VMs share hello same public IP address toominimize hello number of public IP addresses required tooaccess your individual lab VMs.</span></span>  <span data-ttu-id="fef4b-105">En este artículo se describe cómo funcionan las direcciones IP compartidas y sus opciones de configuración relacionadas.</span><span class="sxs-lookup"><span data-stu-id="fef4b-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="fef4b-106">Configuración de IP compartidas</span><span class="sxs-lookup"><span data-stu-id="fef4b-106">Shared IP setting</span></span>

<span data-ttu-id="fef4b-107">Cuando se crea un laboratorio, reside en una subred de una red virtual.</span><span class="sxs-lookup"><span data-stu-id="fef4b-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="fef4b-108">De forma predeterminada, esta subred se crea con **habilitar la IP pública compartida** establecido demasiado*Sí*.</span><span class="sxs-lookup"><span data-stu-id="fef4b-108">By default, this subnet is created with **Enable shared public IP** set too*Yes*.</span></span>  <span data-ttu-id="fef4b-109">Esta configuración crea una dirección IP pública para la subred todo Hola.</span><span class="sxs-lookup"><span data-stu-id="fef4b-109">This configuration creates one public IP address for hello entire subnet.</span></span>  <span data-ttu-id="fef4b-110">Para obtener más información sobre cómo configurar redes virtuales y subredes, vea [Configuración de una red virtual en Azure DevTest Labs](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="fef4b-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![Nueva subred de laboratorio](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="fef4b-112">Para habilitar esta opción en laboratorios existentes, seleccione **Configuration and policies (Directivas y configuración) > Redes virtuales**.</span><span class="sxs-lookup"><span data-stu-id="fef4b-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="fef4b-113">A continuación, seleccione una red virtual de lista de Hola y elija **habilitar IP pública compartido** para una subred seleccionada.</span><span class="sxs-lookup"><span data-stu-id="fef4b-113">Then, select a virtual network from hello list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="fef4b-114">También puede deshabilitar esta opción en cualquier laboratorio si no desea tooshare una dirección IP pública a través de las máquinas virtuales del laboratorio.</span><span class="sxs-lookup"><span data-stu-id="fef4b-114">You can also disable this option in any lab if you don't want tooshare a public IP address across lab VMs.</span></span>

<span data-ttu-id="fef4b-115">Todas las máquinas virtuales crean en este toousing de manera predeterminada de laboratorio una dirección IP compartida.</span><span class="sxs-lookup"><span data-stu-id="fef4b-115">Any VMs created in this lab default toousing a shared IP.</span></span>  <span data-ttu-id="fef4b-116">Al crear Hola VM, esta configuración se puede observar en hello **configuración avanzada** hoja bajo **configuración de dirección IP**.</span><span class="sxs-lookup"><span data-stu-id="fef4b-116">When creating hello VM, this setting can be observed in hello **Advanced settings** blade under **IP address configuration**.</span></span>

![Nueva máquina virtual](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="fef4b-118">**Compartido:** todas las máquinas virtuales creadas como **Compartido** se colocan en un solo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="fef4b-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="fef4b-119">Se asigna una dirección IP única para que RG y todas las máquinas virtuales en hello RG usará esa dirección IP.</span><span class="sxs-lookup"><span data-stu-id="fef4b-119">A single IP address is assigned for that RG and all VMs in hello RG will use that IP address.</span></span>
- <span data-ttu-id="fef4b-120">**Público:** todas las máquinas virtuales que se crean tienen su propia dirección IP y se crean en su propio grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="fef4b-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="fef4b-121">**Privado:** todas las máquinas virtuales que se crean usan una dirección IP privada.</span><span class="sxs-lookup"><span data-stu-id="fef4b-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="fef4b-122">Es posible no que pueda tooconnect toothis VM directamente desde Hola internet con Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="fef4b-122">You will not be able tooconnect toothis VM directly from hello internet with Remote Desktop.</span></span>

<span data-ttu-id="fef4b-123">Siempre que una máquina virtual con la dirección IP compartida habilitado se agrega toohello subred, laboratorios de desarrollo y pruebas agrega equilibrador de carga de hello VM tooa automáticamente y se asigna a un número de puerto TCP en la dirección IP pública de hello, toohello de reenvío de puerto de RDP en hello VM.</span><span class="sxs-lookup"><span data-stu-id="fef4b-123">Whenever a VM with shared IP enabled is added toohello subnet, DevTest Labs automatically adds hello VM tooa load balancer and assigns a TCP port number on hello public IP address, forwarding toohello RDP port on hello VM.</span></span>  

## <a name="using-hello-shared-ip"></a><span data-ttu-id="fef4b-124">Usar Hola compartidos IP</span><span class="sxs-lookup"><span data-stu-id="fef4b-124">Using hello shared IP</span></span>

- <span data-ttu-id="fef4b-125">**Los usuarios de Linux:** SSH toohello VM mediante el uso de la dirección IP de Hola o nombre de dominio completo, seguido de dos puntos, seguido por puerto Hola.</span><span class="sxs-lookup"><span data-stu-id="fef4b-125">**Linux users:** SSH toohello VM by using hello IP address or fully qualified domain name, followed by a colon, followed by hello port.</span></span> <span data-ttu-id="fef4b-126">Por ejemplo, en la imagen de hello siguiente, Hola RDP direcciones toohello tooconnect VM es `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="fef4b-126">For example, in hello image below, hello RDP address tooconnect toohello VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![Ejemplo de máquina virtual](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="fef4b-128">**Los usuarios de Windows:** Hola seleccione **conectar** situado en hello toodownload portal Azure un archivo RDP configurado previamente y tener acceso a Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="fef4b-128">**Windows users:** Select hello **Connect** button on hello Azure portal toodownload a pre-configured RDP file and access hello VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fef4b-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fef4b-129">Next steps</span></span>

* [<span data-ttu-id="fef4b-130">Definición de directivas de laboratorio en Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="fef4b-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="fef4b-131">Configuración de una red virtual en Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="fef4b-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





