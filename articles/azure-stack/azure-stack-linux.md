---
title: Invitados de aaaLinux en la pila de Azure | Documentos de Microsoft
description: "Aprenda a crear máquinas virtuales basadas en Linux en Azure Stack."
services: azure-stack
documentationcenter: 
author: anjayajodha
manager: byronr
editor: 
ms.assetid: d2155c59-902e-4f63-ac58-d19e6a765380
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: anajod
ms.openlocfilehash: 225bed7d630b676ca760add25731e347516b5bf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-linux-virtual-machines-on-azure-stack"></a><span data-ttu-id="76250-103">Implementación de máquinas virtuales Linux en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="76250-103">Deploy Linux virtual machines on Azure Stack</span></span>
<span data-ttu-id="76250-104">Puede implementar máquinas virtuales Linux en hello Kit de desarrollo de pila de Azure mediante la adición de una imagen basada en Linux en hello Azure Marketplace de pila.</span><span class="sxs-lookup"><span data-stu-id="76250-104">You can deploy Linux virtual machines on hello Azure Stack Development Kit by adding a Linux-based image into hello Azure Stack Marketplace.</span></span> <span data-ttu-id="76250-105">Varios proveedores de Linux han proporcionado imágenes que se pueden agregar a Azure Stack Development Kit o puede crear las suyas propias.</span><span class="sxs-lookup"><span data-stu-id="76250-105">Several Linux vendors have provided images that can be added into an Azure Stack Development Kit or you can build your own.</span></span>

## <a name="download-an-image"></a><span data-ttu-id="76250-106">Descarga de una imagen</span><span class="sxs-lookup"><span data-stu-id="76250-106">Download an image</span></span>
1. <span data-ttu-id="76250-107">Descargue y extraiga una imagen compatible con Azure pila Hola siguientes vínculos o preparar su propia:</span><span class="sxs-lookup"><span data-stu-id="76250-107">Download and extract an Azure Stack-compatible image from hello following links, or prepare your own:</span></span>
   
   * [<span data-ttu-id="76250-108">Bitnami</span><span class="sxs-lookup"><span data-stu-id="76250-108">Bitnami</span></span>](https://bitnami.com/azure-stack)
   * [<span data-ttu-id="76250-109">CentOS</span><span class="sxs-lookup"><span data-stu-id="76250-109">CentOS</span></span>](http://olstacks.cloudapp.net/latest/)
   * [<span data-ttu-id="76250-110">CoreOS</span><span class="sxs-lookup"><span data-stu-id="76250-110">CoreOS</span></span>](https://stable.release.core-os.net/amd64-usr/current/coreos_production_azure_image.vhd.bz2)
   * [<span data-ttu-id="76250-111">SuSE</span><span class="sxs-lookup"><span data-stu-id="76250-111">SuSE</span></span>](https://download.suse.com/Download?buildid=VCFi7y7MsFQ~)
   * <span data-ttu-id="76250-112">[Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="76250-112">[Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
2. <span data-ttu-id="76250-113">Extraiga la imagen de hello VHD si es necesario y [Agregar imagen de hello toohello Marketplace](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="76250-113">Extract hello image VHD if necessary and [add hello image toohello Marketplace](azure-stack-add-vm-image.md).</span></span> <span data-ttu-id="76250-114">Asegúrese de que ese hello `OSType` parámetro está establecido demasiado`Linux`.</span><span class="sxs-lookup"><span data-stu-id="76250-114">Make sure that hello `OSType` parameter is set too`Linux`.</span></span>
3. <span data-ttu-id="76250-115">Una vez agregado Hola imagen toohello Marketplace, se crea un elemento de Marketplace y puede implementar una máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="76250-115">After you've added hello image toohello Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span></span>

## <a name="prepare-your-own-image"></a><span data-ttu-id="76250-116">Preparación de su propia imagen</span><span class="sxs-lookup"><span data-stu-id="76250-116">Prepare your own image</span></span>
1. <span data-ttu-id="76250-117">Preparar su propia imagen de Linux mediante uno de hello siguiendo las instrucciones:</span><span class="sxs-lookup"><span data-stu-id="76250-117">Prepare your own Linux image using one of hello following instructions:</span></span>
   
   * [<span data-ttu-id="76250-118">Distribuciones basadas en CentOS</span><span class="sxs-lookup"><span data-stu-id="76250-118">CentOS-based Distributions</span></span>](../virtual-machines/linux/create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="76250-119">Debian Linux</span><span class="sxs-lookup"><span data-stu-id="76250-119">Debian Linux</span></span>](../virtual-machines/linux/debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="76250-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="76250-120">Oracle Linux</span></span>](../virtual-machines/linux/oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="76250-121">Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="76250-121">Red Hat Enterprise Linux</span></span>](../virtual-machines/linux/redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="76250-122">SLES y openSUSE</span><span class="sxs-lookup"><span data-stu-id="76250-122">SLES & openSUSE</span></span>](../virtual-machines/linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [<span data-ttu-id="76250-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="76250-123">Ubuntu</span></span>](../virtual-machines/linux/create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="76250-124">Descargue e instale hello [agente Linux de Azure](https://github.com/Azure/WALinuxAgent/)</span><span class="sxs-lookup"><span data-stu-id="76250-124">Download and install hello [Azure Linux Agent](https://github.com/Azure/WALinuxAgent/)</span></span>
   
    <span data-ttu-id="76250-125">Hola versión del agente de Linux de Azure 2.1.3 o posterior es necesario tooprovision la VM de Linux en la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="76250-125">hello Azure Linux Agent version 2.1.3 or higher is required tooprovision your Linux VM on Azure Stack.</span></span> <span data-ttu-id="76250-126">Muchas de las distribuciones de hello mencionadas anteriormente ya incluyen esta versión de agente de Hola o superior como un paquete en sus repositorios (suele denominarse `WALinuxAgent` o `walinuxagent`).</span><span class="sxs-lookup"><span data-stu-id="76250-126">Many of hello distributions listed above already include this version of hello agent or higher as a package in their repositories (typically called `WALinuxAgent` or `walinuxagent`).</span></span> <span data-ttu-id="76250-127">Sin embargo, si hello versión del paquete de agente de Azure de hello es menor que 2.1.3 (es decir, 2.0.18 o inferior), tendrá que instalar manualmente el agente de Hola.</span><span class="sxs-lookup"><span data-stu-id="76250-127">However, if hello version of hello Azure agent package is less than 2.1.3 (i.e. 2.0.18 or lower), then you must install hello agent manually.</span></span> <span data-ttu-id="76250-128">puede determinar la versión de Hola instalado desde el nombre del paquete de Hola o mediante la ejecución de `/usr/sbin/waagent -version` en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="76250-128">hello installed version can be determined either from hello package name or by running `/usr/sbin/waagent -version` on hello VM.</span></span>
   
    <span data-ttu-id="76250-129">Siga las instrucciones de hello debajo de agente de Linux de Azure de hello tooinstall de manualmente:</span><span class="sxs-lookup"><span data-stu-id="76250-129">Follow hello instructions below tooinstall hello Azure Linux agent manually -</span></span>
   
   * <span data-ttu-id="76250-130">En primer lugar, descargue Hola de agente de Linux de Azure más reciente de [GitHub](https://github.com/Azure/WALinuxAgent/releases), ejemplo:</span><span class="sxs-lookup"><span data-stu-id="76250-130">First, download hello latest Azure Linux agent from [GitHub](https://github.com/Azure/WALinuxAgent/releases), example:</span></span>
     
            # wget https://github.com/Azure/WALinuxAgent/archive/v2.2.0.tar.gz
   * <span data-ttu-id="76250-131">Desempaquetar Hola agente de Azure:</span><span class="sxs-lookup"><span data-stu-id="76250-131">Unpack hello Azure agent:</span></span>
     
            # tar -vzxf v2.2.0.tar.gz
   * <span data-ttu-id="76250-132">Instale python-setuptools</span><span class="sxs-lookup"><span data-stu-id="76250-132">Install python-setuptools</span></span>
     
        <span data-ttu-id="76250-133">**Debian y Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="76250-133">**Debian / Ubuntu**</span></span>
     
            # sudo apt-get update
            # sudo apt-get install python-setuptools
     
        <span data-ttu-id="76250-134">**Ubuntu 16.04+**</span><span class="sxs-lookup"><span data-stu-id="76250-134">**Ubuntu 16.04+**</span></span>
     
            # sudo apt-get install python3-setuptools
     
        <span data-ttu-id="76250-135">**RHEL, CentOS y Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="76250-135">**RHEL / CentOS / Oracle Linux**</span></span>
     
            # sudo yum install python-setuptools
   * <span data-ttu-id="76250-136">Instalar Hola agente de Azure:</span><span class="sxs-lookup"><span data-stu-id="76250-136">Install hello Azure agent:</span></span>
     
            # cd WALinuxAgent-2.2.0
            # sudo python setup.py install --register-service
     
     <span data-ttu-id="76250-137">Sistemas con Python 2.x y 3.x instalado de Python side-by-side pueden necesitar hello toorun siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="76250-137">Systems with Python 2.x and Python 3.x installed side-by-side may need toorun hello following command:</span></span>
     
         sudo python3 setup.py install --register-service
     <span data-ttu-id="76250-138">Para obtener más información, vea Hola agente Linux de Azure [Léame](https://github.com/Azure/WALinuxAgent/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="76250-138">For more information, see hello Azure Linux Agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md).</span></span>
3. <span data-ttu-id="76250-139">[Agregar imagen de hello toohello Marketplace](azure-stack-add-vm-image.md).</span><span class="sxs-lookup"><span data-stu-id="76250-139">[Add hello image toohello Marketplace](azure-stack-add-vm-image.md).</span></span> <span data-ttu-id="76250-140">Asegúrese de que ese hello `OSType` parámetro está establecido demasiado`Linux`.</span><span class="sxs-lookup"><span data-stu-id="76250-140">Make sure that hello `OSType` parameter is set too`Linux`.</span></span>
4. <span data-ttu-id="76250-141">Una vez agregado Hola imagen toohello Marketplace, se crea un elemento de Marketplace y puede implementar una máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="76250-141">After you've added hello image toohello Marketplace, a Marketplace item is created and you can deploy a Linux virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76250-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="76250-142">Next steps</span></span>
[<span data-ttu-id="76250-143">Preguntas frecuentes acerca de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="76250-143">Frequently asked questions for Azure Stack</span></span>](azure-stack-faq.md)

