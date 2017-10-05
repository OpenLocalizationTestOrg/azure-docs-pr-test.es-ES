---
title: "Migración de máquinas virtuales Windows AWS a Azure | Microsoft Docs"
description: Migre una instancia de EC2 Windows de Amazon Web Services (AWS) a Azure Virtual Machines con Azure PowerShell.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: cynthn
ms.openlocfilehash: 7d2b498d3f84c4fd6cccf97c6d7781f293f5b395
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-to-azure-using-powershell"></a><span data-ttu-id="d9da5-103">Migración de una máquina virtual Windows de Amazon Web Services (AWS) a Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9da5-103">Move a Windows VM from Amazon Web Services (AWS) to Azure using PowerShell</span></span>

<span data-ttu-id="d9da5-104">Si va a evaluar las máquinas virtuales de Azure para hospedar las cargas de trabajo, puede exportar una instancia existente de la máquina virtual Windows de Amazon Web Services (AWS) EC2 y cargar el disco duro virtual (VHD) en Azure.</span><span class="sxs-lookup"><span data-stu-id="d9da5-104">If you are evaluating Azure virtual machines for hosting your workloads, you can export an existing Amazon Web Services (AWS) EC2 Windows VM instance then upload the virtual hard disk (VHD) to Azure.</span></span> <span data-ttu-id="d9da5-105">Una vez cargado el disco duro virtual, puede crear una nueva máquina virtual en Azure desde el disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="d9da5-105">Once the VHD is uploaded, you can create a new VM in Azure from the VHD.</span></span> 

<span data-ttu-id="d9da5-106">En este tema se cubre la migración de una sola máquina virtual de AWS a Azure.</span><span class="sxs-lookup"><span data-stu-id="d9da5-106">This topic covers moving a single VM from AWS to Azure.</span></span> <span data-ttu-id="d9da5-107">Si quiere migrar máquinas virtuales de AWS a Azure en escala, consulte [Migrar máquinas virtuales de Amazon Web Services (AWS) a Azure con Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="d9da5-107">If you want to move VMs from AWS to Azure at scale, see [Migrate virtual machines in Amazon Web Services (AWS) to Azure with Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span></span>

## <a name="prepare-the-vm"></a><span data-ttu-id="d9da5-108">Preparación de la VM</span><span class="sxs-lookup"><span data-stu-id="d9da5-108">Prepare the VM</span></span> 
 
<span data-ttu-id="d9da5-109">Puede cargar VHD generalizados y especializados en Azure.</span><span class="sxs-lookup"><span data-stu-id="d9da5-109">You can upload both generalized and specialized VHDs to Azure.</span></span> <span data-ttu-id="d9da5-110">Todos requieren la preparación de la máquina virtual antes de la exportación desde AWS.</span><span class="sxs-lookup"><span data-stu-id="d9da5-110">Each type requires that you prepare the VM before exporting from AWS.</span></span> 

- <span data-ttu-id="d9da5-111">**VHD generalizado**: Se ha quitado toda la información de cuenta personal con Sysprep de un VHD generalizado.</span><span class="sxs-lookup"><span data-stu-id="d9da5-111">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="d9da5-112">Si tiene previsto usar VHD como una imagen desde la que crear nuevas VM, debe:</span><span class="sxs-lookup"><span data-stu-id="d9da5-112">If you intend to use the VHD as an image to create new VMs from, you should:</span></span> 
 
    * <span data-ttu-id="d9da5-113">[Preparación de una máquina virtual Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="d9da5-113">[Prepare a Windows VM](prepare-for-upload-vhd-image.md).</span></span>  
    * <span data-ttu-id="d9da5-114">Generalice la máquina virtual mediante Sysprep.</span><span class="sxs-lookup"><span data-stu-id="d9da5-114">Generalize the virtual machine using Sysprep.</span></span>  

 
- <span data-ttu-id="d9da5-115">**VHD especializado**: un disco duro virtual especializado mantiene las cuentas de usuario, las aplicaciones y otros datos de estado de la máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="d9da5-115">**Specialized VHD** - a specialized VHD maintains the user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="d9da5-116">Si tiene previsto usar el VHD como está para crear una nueva VM, asegúrese de completar los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="d9da5-116">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span>  
    * <span data-ttu-id="d9da5-117">[Preparar de un VHD de Windows para cargar en Azure](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="d9da5-117">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md).</span></span> <span data-ttu-id="d9da5-118">**No** generalice la VM mediante Sysprep.</span><span class="sxs-lookup"><span data-stu-id="d9da5-118">**Do not** generalize the VM using Sysprep.</span></span> 
    * <span data-ttu-id="d9da5-119">Quite todas las herramientas de virtualización de invitado y los agentes instalados en la VM (es decir, herramientas de VMware).</span><span class="sxs-lookup"><span data-stu-id="d9da5-119">Remove any guest virtualization tools and agents that are installed on the VM (i.e. VMware tools).</span></span> 
    * <span data-ttu-id="d9da5-120">Asegúrese de que la VM se configura para extraer su dirección IP y la configuración de DNS a través de DHCP.</span><span class="sxs-lookup"><span data-stu-id="d9da5-120">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="d9da5-121">Esto garantiza que el servidor obtiene una dirección IP dentro de la red virtual cuando se inicia.</span><span class="sxs-lookup"><span data-stu-id="d9da5-121">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span>  


## <a name="export-and-download-the-vhd"></a><span data-ttu-id="d9da5-122">Exportación y descarga del disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="d9da5-122">Export and download the VHD</span></span> 

<span data-ttu-id="d9da5-123">Exporte la instancia de EC2 a un disco duro virtual de un cubo de Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="d9da5-123">Export the EC2 instance to a VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="d9da5-124">Siga los pasos que se describen en el tema [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) (Exportación de una instancia como una máquina virtual con la importación/exportación de máquinas virtuales) de la documentación de Amazon y ejecute el comando [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) para exportar la instancia de EC2 a un archivo VHD.</span><span class="sxs-lookup"><span data-stu-id="d9da5-124">Follow the steps described in the Amazon documentation topic [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) and run the [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) command to export the EC2 instance to a VHD file.</span></span> 

<span data-ttu-id="d9da5-125">El archivo VHD exportado se guarda en el cubo de Amazon S3 que haya especificado.</span><span class="sxs-lookup"><span data-stu-id="d9da5-125">The exported VHD file is saved in the Amazon S3 bucket you specify.</span></span> <span data-ttu-id="d9da5-126">La sintaxis básica para exportar el disco duro virtual se encuentra justo debajo, solo tiene que reemplazar el texto del marcador de posición de <brackets> con su información.</span><span class="sxs-lookup"><span data-stu-id="d9da5-126">The basic syntax for exporting the VHD is below, just replace the placeholder text in <brackets> with your information.</span></span>

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

<span data-ttu-id="d9da5-127">Una vez exportado el disco duro virtual, siga las instrucciones de [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) (Descarga de objetos desde un cubo de S3) para descargar el archivo VHD desde el cubo de S3.</span><span class="sxs-lookup"><span data-stu-id="d9da5-127">Once the VHD has been exported, follow the instructions in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) to download the VHD file from the S3 bucket.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d9da5-128">Por la descarga del disco duro virtual, AWS cobra una tarifa de transferencia de datos.</span><span class="sxs-lookup"><span data-stu-id="d9da5-128">AWS charges data transfer fees for downloading the VHD.</span></span> <span data-ttu-id="d9da5-129">Consulte [Precios de Amazon S3](https://aws.amazon.com/s3/pricing/) para más información.</span><span class="sxs-lookup"><span data-stu-id="d9da5-129">See [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) for more information.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d9da5-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d9da5-130">Next steps</span></span>

<span data-ttu-id="d9da5-131">Ahora puede cargar el disco duro virtual en Azure y crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d9da5-131">Now you can upload the VHD to Azure and create a new VM.</span></span> 

- <span data-ttu-id="d9da5-132">Si ha ejecutado Sysprep en el origen para la **generalización** antes de exportarlo, consulte el artículo de [Carga de un disco duro virtual generalizado y creación de máquinas virtuales en Azure con él](upload-generalized-managed.md)</span><span class="sxs-lookup"><span data-stu-id="d9da5-132">If you ran Sysprep on your source to **generalize** it before exporting, see [Upload a generalized VHD and use it to create a new VMs in Azure](upload-generalized-managed.md)</span></span>
- <span data-ttu-id="d9da5-133">Si no ejecutó Sysprep antes de la exportación, se considera que el disco duro virtual es **especializado**; consulte el artículo de [Carga de un disco duro virtual especializado en Azure y creación de máquinas virtuales con él](create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="d9da5-133">If you did not run Sysprep before exporting, the VHD is considered **specialized**, see [Upload a specialized VHD to Azure and create a new VM](create-vm-specialized.md)</span></span>

 
