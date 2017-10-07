---
title: "aaaMove una tooAzure de las máquinas virtuales de Windows AWS | Documentos de Microsoft"
description: "Mover un tooAzure de instancia de Amazon Web Services (AWS) EC2 Windows máquinas virtuales con PowerShell de Azure."
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
ms.openlocfilehash: f912c28d3ffe585162c3add715a1318ac3cd4643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-from-amazon-web-services-aws-tooazure-using-powershell"></a><span data-ttu-id="f54d9-103">Mover una máquina virtual de Windows de tooAzure de Amazon Web Services (AWS) mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="f54d9-103">Move a Windows VM from Amazon Web Services (AWS) tooAzure using PowerShell</span></span>

<span data-ttu-id="f54d9-104">Si va a evaluar máquinas virtuales de Azure para hospedar las cargas de trabajo, puede exportar una instancia existente de la máquina virtual de Windows de Amazon Web Services (AWS) EC2 luego cargar hello tooAzure de disco duro virtual (VHD).</span><span class="sxs-lookup"><span data-stu-id="f54d9-104">If you are evaluating Azure virtual machines for hosting your workloads, you can export an existing Amazon Web Services (AWS) EC2 Windows VM instance then upload hello virtual hard disk (VHD) tooAzure.</span></span> <span data-ttu-id="f54d9-105">Una vez Hola generalizada, puede crear una nueva máquina virtual en Azure de hello VHD.</span><span class="sxs-lookup"><span data-stu-id="f54d9-105">Once hello VHD is uploaded, you can create a new VM in Azure from hello VHD.</span></span> 

<span data-ttu-id="f54d9-106">Este tema cubre la migración de una sola máquina virtual desde AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f54d9-106">This topic covers moving a single VM from AWS tooAzure.</span></span> <span data-ttu-id="f54d9-107">Si desea que las máquinas virtuales de toomove de AWS tooAzure a escala, vea [Migre máquinas virtuales de Amazon Web Services (AWS) tooAzure con Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="f54d9-107">If you want toomove VMs from AWS tooAzure at scale, see [Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery](../../site-recovery/site-recovery-migrate-aws-to-azure.md).</span></span>

## <a name="prepare-hello-vm"></a><span data-ttu-id="f54d9-108">Preparar Hola VM</span><span class="sxs-lookup"><span data-stu-id="f54d9-108">Prepare hello VM</span></span> 
 
<span data-ttu-id="f54d9-109">Puede cargar tooAzure de discos duros virtuales especializada y generalizada.</span><span class="sxs-lookup"><span data-stu-id="f54d9-109">You can upload both generalized and specialized VHDs tooAzure.</span></span> <span data-ttu-id="f54d9-110">Cada tipo requiere que preparar Hola VM antes de exportar desde AWS.</span><span class="sxs-lookup"><span data-stu-id="f54d9-110">Each type requires that you prepare hello VM before exporting from AWS.</span></span> 

- <span data-ttu-id="f54d9-111">**VHD generalizado**: Se ha quitado toda la información de cuenta personal con Sysprep de un VHD generalizado.</span><span class="sxs-lookup"><span data-stu-id="f54d9-111">**Generalized VHD** - a generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="f54d9-112">Si piensa toouse Hola VHD como una imagen toocreate nuevas máquinas virtuales desde, debe:</span><span class="sxs-lookup"><span data-stu-id="f54d9-112">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span> 
 
    * <span data-ttu-id="f54d9-113">[Preparación de una máquina virtual Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="f54d9-113">[Prepare a Windows VM](prepare-for-upload-vhd-image.md).</span></span>  
    * <span data-ttu-id="f54d9-114">Generalice la máquina virtual de hello mediante Sysprep.</span><span class="sxs-lookup"><span data-stu-id="f54d9-114">Generalize hello virtual machine using Sysprep.</span></span>  

 
- <span data-ttu-id="f54d9-115">**Especializado VHD** -un disco duro virtual especializado mantiene las cuentas de usuario de hello, aplicaciones y otros datos de estado de la máquina virtual original.</span><span class="sxs-lookup"><span data-stu-id="f54d9-115">**Specialized VHD** - a specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="f54d9-116">Si piensa toouse Hola VHD como-es toocreate una nueva máquina virtual, asegúrese de que se completa Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="f54d9-116">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span>  
    * <span data-ttu-id="f54d9-117">[Preparar una tooAzure de tooupload de disco duro virtual de Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="f54d9-117">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> <span data-ttu-id="f54d9-118">**No** generalizar Hola VM con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="f54d9-118">**Do not** generalize hello VM using Sysprep.</span></span> 
    * <span data-ttu-id="f54d9-119">Quite todas las herramientas de virtualización de invitado y los agentes instalados en hello VM (es decir, herramientas de VMware).</span><span class="sxs-lookup"><span data-stu-id="f54d9-119">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span> 
    * <span data-ttu-id="f54d9-120">Asegúrese de hello VM es toopull configurado su dirección IP y la configuración de DNS a través de DHCP.</span><span class="sxs-lookup"><span data-stu-id="f54d9-120">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="f54d9-121">Esto garantiza que el servidor hello Obtiene una dirección IP dentro de la red virtual de hello cuando se inicia.</span><span class="sxs-lookup"><span data-stu-id="f54d9-121">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span>  


## <a name="export-and-download-hello-vhd"></a><span data-ttu-id="f54d9-122">Exportar y descargar Hola VHD</span><span class="sxs-lookup"><span data-stu-id="f54d9-122">Export and download hello VHD</span></span> 

<span data-ttu-id="f54d9-123">Exportar Hola EC2 instancia tooa disco duro virtual en un depósito de S3 de Amazon.</span><span class="sxs-lookup"><span data-stu-id="f54d9-123">Export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="f54d9-124">Siga los pasos de hello descritos en el tema de documentación de Amazon hello [exportar como una máquina virtual usando VM importación y exportación de una instancia](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) ejecución hello y [crear instancia-export-tareas](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) comando tooexport hello EC2 archivo de disco duro virtual de tooa de instancia.</span><span class="sxs-lookup"><span data-stu-id="f54d9-124">Follow hello steps described in hello Amazon documentation topic [Exporting an Instance as a VM Using VM Import/Export](http://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) and run hello [create-instance-export-task](http://docs.aws.amazon.com/cli/latest/reference/ec2/create-instance-export-task.html) command tooexport hello EC2 instance tooa VHD file.</span></span> 

<span data-ttu-id="f54d9-125">Hello VHD archivo exportado se guarda en el cubo de hello Amazon S3 que especifique.</span><span class="sxs-lookup"><span data-stu-id="f54d9-125">hello exported VHD file is saved in hello Amazon S3 bucket you specify.</span></span> <span data-ttu-id="f54d9-126">Hello sintaxis básica para exportar Hola VHD está por debajo, solo tiene que reemplazar texto de marcador de posición de hello en <brackets> con su información.</span><span class="sxs-lookup"><span data-stu-id="f54d9-126">hello basic syntax for exporting hello VHD is below, just replace hello placeholder text in <brackets> with your information.</span></span>

```
aws ec2 create-instance-export-task --instance-id <instanceID> --target-environment Microsoft \
  --export-to-s3-task DiskImageFormat=VHD,ContainerFormat=ova,S3Bucket=<bucket>,S3Prefix=<prefix>
```

<span data-ttu-id="f54d9-127">Una vez que se ha exportado Hola VHD, siga las instrucciones de hello en [cómo descargar un objeto de un depósito de S3?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) hello toodownload VHD de archivos de depósitos de hello S3.</span><span class="sxs-lookup"><span data-stu-id="f54d9-127">Once hello VHD has been exported, follow hello instructions in [How Do I Download an Object from an S3 Bucket?](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/download-objects.html) toodownload hello VHD file from hello S3 bucket.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f54d9-128">AWS cargos por las cuotas de transferencia de datos para la descarga de hello VHD.</span><span class="sxs-lookup"><span data-stu-id="f54d9-128">AWS charges data transfer fees for downloading hello VHD.</span></span> <span data-ttu-id="f54d9-129">Consulte [Precios de Amazon S3](https://aws.amazon.com/s3/pricing/) para más información.</span><span class="sxs-lookup"><span data-stu-id="f54d9-129">See [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/) for more information.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f54d9-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f54d9-130">Next steps</span></span>

<span data-ttu-id="f54d9-131">Ahora puede cargar tooAzure de disco duro virtual de Hola y crear una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f54d9-131">Now you can upload hello VHD tooAzure and create a new VM.</span></span> 

- <span data-ttu-id="f54d9-132">Si ha ejecutado Sysprep en el origen demasiado**generalizar** , antes de exportar, vea [cargar un disco duro virtual generalizado y utilizar toocreate un nuevas máquinas virtuales de Azure](upload-generalized-managed.md)</span><span class="sxs-lookup"><span data-stu-id="f54d9-132">If you ran Sysprep on your source too**generalize** it before exporting, see [Upload a generalized VHD and use it toocreate a new VMs in Azure](upload-generalized-managed.md)</span></span>
- <span data-ttu-id="f54d9-133">Si no se ejecutó Sysprep antes de exportar, hello VHD se considera **especializada**, consulte [cargar un tooAzure especializada de VHD y crear una nueva máquina virtual](create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="f54d9-133">If you did not run Sysprep before exporting, hello VHD is considered **specialized**, see [Upload a specialized VHD tooAzure and create a new VM](create-vm-specialized.md)</span></span>

 
