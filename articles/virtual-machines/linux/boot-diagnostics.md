---
title: "aaaBoot diagnósticos para máquinas virtuales de Linux en Azure | Documento de Microsoft"
description: "Información general sobre Hola dos características de depuración para las máquinas virtuales de Linux en Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="e10fd-103">¿Cómo toouse arrancar las máquinas virtuales Linux diagnósticos tootroubleshoot en Azure</span><span class="sxs-lookup"><span data-stu-id="e10fd-103">How toouse boot diagnostics tootroubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="e10fd-104">Ahora se ofrece en Azure compatibilidad con dos características de depuración, Salida de la consola y Captura de pantalla, para el modelo de implementación de Resource Manager en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="e10fd-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="e10fd-105">Al volver a poner su propia imagen tooAzure o incluso arranque uno de imágenes de la plataforma de hello, puede haber muchas razones, ¿por qué se obtiene una máquina Virtual en un estado no sean de arranque.</span><span class="sxs-lookup"><span data-stu-id="e10fd-105">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="e10fd-106">Estos permiten características tooeasily, diagnosticar y recuperarse de las máquinas virtuales de los errores de arranque.</span><span class="sxs-lookup"><span data-stu-id="e10fd-106">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="e10fd-107">Para máquinas de virtuales de Linux, puede ver fácilmente salida de hello de su registro de la consola de hello Portal:</span><span class="sxs-lookup"><span data-stu-id="e10fd-107">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Azure Portal](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="e10fd-109">Sin embargo, Windows y máquinas virtuales de Linux, Azure también permite toosee una captura de pantalla de hello VM desde el hipervisor de hello:</span><span class="sxs-lookup"><span data-stu-id="e10fd-109">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Error](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="e10fd-111">Ambas características son compatibles para las máquinas virtuales de Azure en todas las regiones.</span><span class="sxs-lookup"><span data-stu-id="e10fd-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="e10fd-112">Tenga en cuenta, capturas de pantalla y salida pueden tardar hasta too10 minutos tooappear en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e10fd-112">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="e10fd-113">Errores comunes de arranque</span><span class="sxs-lookup"><span data-stu-id="e10fd-113">Common boot errors</span></span>

- [<span data-ttu-id="e10fd-114">Problemas del sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="e10fd-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="e10fd-115">Problemas de kernel</span><span class="sxs-lookup"><span data-stu-id="e10fd-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="e10fd-116">Errores de FSTAB</span><span class="sxs-lookup"><span data-stu-id="e10fd-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="e10fd-117">Habilitación del diagnóstico en una nueva máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e10fd-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="e10fd-118">Al crear una nueva máquina Virtual desde el Portal de vista previa de hello, seleccione hello **Azure Resource Manager** de lista desplegable de modelo de implementación de hello:</span><span class="sxs-lookup"><span data-stu-id="e10fd-118">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="e10fd-120">Configurar Hola cuenta de almacenamiento de hello en tooselect de supervisión opción que desee que tooplace estos archivos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="e10fd-120">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![Creación de una máquina virtual](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="e10fd-122">Si va a implementar desde una plantilla de Azure Resource Manager, navegue tooyour recurso de máquina Virtual y anexar la sección de perfil de diagnóstico de Hola.</span><span class="sxs-lookup"><span data-stu-id="e10fd-122">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="e10fd-123">Recuerde que el encabezado de la versión de API de "2015-06-15" toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="e10fd-123">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="e10fd-124">perfil de diagnóstico de Hello permite cuenta de almacenamiento de hello tooselect donde desea tooput estos registros.</span><span class="sxs-lookup"><span data-stu-id="e10fd-124">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="e10fd-125">Actualización de una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="e10fd-125">Update an existing virtual machine</span></span>

<span data-ttu-id="e10fd-126">diagnóstico de arranque de tooenable a través del portal de hello, también puede actualizar una máquina virtual existente a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="e10fd-126">tooenable boot diagnostics through hello portal, you can also update an existing virtual machine through hello portal.</span></span> <span data-ttu-id="e10fd-127">Diagnóstico de arranque de hello seleccione opción y guardar.</span><span class="sxs-lookup"><span data-stu-id="e10fd-127">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="e10fd-128">Reinicie el efecto de hello VM tootake.</span><span class="sxs-lookup"><span data-stu-id="e10fd-128">Restart hello VM tootake effect.</span></span>

![Actualización de una máquina virtual existente](./media/boot-diagnostics/screenshot5.png)