---
title: Direcciones IP compartidas en Azure DevTest Labs | Microsoft Docs
description: "Obtenga información sobre cómo Azure DevTest Labs usa direcciones IP compartidas para minimizar las direcciones IP públicas necesarias para acceder a las máquinas virtuales de su laboratorio."
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
ms.openlocfilehash: 9f6e1980bf5ea5b41da98a135d89f1c5159921a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="afb63-103">Direcciones IP compartidas en Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="afb63-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="afb63-104">Las máquinas virtuales de laboratorio de Azure DevTest Labs comparten la misma dirección para minimizar el número de direcciones IP públicas necesarias para acceder a estas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="afb63-104">Azure DevTest Labs lets lab VMs share the same public IP address to minimize the number of public IP addresses required to access your individual lab VMs.</span></span>  <span data-ttu-id="afb63-105">En este artículo se describe cómo funcionan las direcciones IP compartidas y sus opciones de configuración relacionadas.</span><span class="sxs-lookup"><span data-stu-id="afb63-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="afb63-106">Configuración de IP compartidas</span><span class="sxs-lookup"><span data-stu-id="afb63-106">Shared IP setting</span></span>

<span data-ttu-id="afb63-107">Cuando se crea un laboratorio, reside en una subred de una red virtual.</span><span class="sxs-lookup"><span data-stu-id="afb63-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="afb63-108">De forma predeterminada, esta subred se crea con la opción **Habilitar IP pública compartida** establecida en *Sí*.</span><span class="sxs-lookup"><span data-stu-id="afb63-108">By default, this subnet is created with **Enable shared public IP** set to *Yes*.</span></span>  <span data-ttu-id="afb63-109">Esta configuración crea una dirección IP pública para toda la subred.</span><span class="sxs-lookup"><span data-stu-id="afb63-109">This configuration creates one public IP address for the entire subnet.</span></span>  <span data-ttu-id="afb63-110">Para obtener más información sobre cómo configurar redes virtuales y subredes, vea [Configuración de una red virtual en Azure DevTest Labs](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="afb63-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![Nueva subred de laboratorio](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="afb63-112">Para habilitar esta opción en laboratorios existentes, seleccione **Configuration and policies (Directivas y configuración) > Redes virtuales**.</span><span class="sxs-lookup"><span data-stu-id="afb63-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="afb63-113">Después, seleccione una red virtual de la lista y elija **HABILITAR IP PÚBLICA COMPARTIDA**  para la subred seleccionada.</span><span class="sxs-lookup"><span data-stu-id="afb63-113">Then, select a virtual network from the list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="afb63-114">También puede deshabilitar esta opción en cualquier laboratorio si no quiere compartir una dirección IP pública en todas las máquinas virtuales del laboratorio.</span><span class="sxs-lookup"><span data-stu-id="afb63-114">You can also disable this option in any lab if you don't want to share a public IP address across lab VMs.</span></span>

<span data-ttu-id="afb63-115">Las máquinas virtuales creadas en este laboratorio usarán una dirección IP compartida de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="afb63-115">Any VMs created in this lab default to using a shared IP.</span></span>  <span data-ttu-id="afb63-116">Al crear la máquina virtual, esta configuración se puede encontrar en la hoja **Configuración avanzada**, bajo **Configuración de dirección IP**.</span><span class="sxs-lookup"><span data-stu-id="afb63-116">When creating the VM, this setting can be observed in the **Advanced settings** blade under **IP address configuration**.</span></span>

![Nueva máquina virtual](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="afb63-118">**Compartido:** todas las máquinas virtuales creadas como **Compartido** se colocan en un solo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="afb63-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="afb63-119">Se asigna una sola dirección IP al grupo de recursos y todas las máquinas virtuales usarán esa dirección IP.</span><span class="sxs-lookup"><span data-stu-id="afb63-119">A single IP address is assigned for that RG and all VMs in the RG will use that IP address.</span></span>
- <span data-ttu-id="afb63-120">**Público:** todas las máquinas virtuales que se crean tienen su propia dirección IP y se crean en su propio grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="afb63-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="afb63-121">**Privado:** todas las máquinas virtuales que se crean usan una dirección IP privada.</span><span class="sxs-lookup"><span data-stu-id="afb63-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="afb63-122">No podrá conectarse a estas máquinas virtuales directamente desde Internet mediante Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="afb63-122">You will not be able to connect to this VM directly from the internet with Remote Desktop.</span></span>

<span data-ttu-id="afb63-123">Siempre que se agrega una máquina virtual con la dirección IP compartida a la subred, DevTest Labs agrega automáticamente la máquina virtual a un equilibrador de carga y le asigna un número de puerto TCP en la dirección IP pública, que se reenvía al puerto RDP de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="afb63-123">Whenever a VM with shared IP enabled is added to the subnet, DevTest Labs automatically adds the VM to a load balancer and assigns a TCP port number on the public IP address, forwarding to the RDP port on the VM.</span></span>  

## <a name="using-the-shared-ip"></a><span data-ttu-id="afb63-124">Uso de la dirección IP compartida</span><span class="sxs-lookup"><span data-stu-id="afb63-124">Using the shared IP</span></span>

- <span data-ttu-id="afb63-125">**Usuarios de Linux:** use SSH para conectarse a la máquina virtual con la dirección IP o el nombre de dominio completo, seguido de dos puntos y del puerto.</span><span class="sxs-lookup"><span data-stu-id="afb63-125">**Linux users:** SSH to the VM by using the IP address or fully qualified domain name, followed by a colon, followed by the port.</span></span> <span data-ttu-id="afb63-126">Por ejemplo, en la imagen siguiente, la dirección RDP para conectarse a la máquina virtual es `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="afb63-126">For example, in the image below, the RDP address to connect to the VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![Ejemplo de máquina virtual](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="afb63-128">**Usuarios de Windows:** en Azure Portal, seleccione el botón **Conectar** para descargar un archivo RDP preconfigurado y acceder a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="afb63-128">**Windows users:** Select the **Connect** button on the Azure portal to download a pre-configured RDP file and access the VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afb63-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="afb63-129">Next steps</span></span>

* [<span data-ttu-id="afb63-130">Definición de directivas de laboratorio en Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="afb63-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="afb63-131">Configuración de una red virtual en Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="afb63-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





