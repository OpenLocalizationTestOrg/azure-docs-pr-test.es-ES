---
title: "Diagnósticos de arranque de máquinas virtuales Linux en Azure | Microsoft Docs"
description: "Introducción a las dos características de depuración para máquinas virtuales Linux en Azure"
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
ms.openlocfilehash: 70254d39b5c6326166f7e29fdfc99533835502f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-boot-diagnostics-to-troubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="8d290-103">Instrucciones de uso de diagnósticos de arranque para solucionar problemas de máquinas virtuales Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="8d290-103">How to use boot diagnostics to troubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="8d290-104">Ahora se ofrece en Azure compatibilidad con dos características de depuración, Salida de la consola y Captura de pantalla, para el modelo de implementación de Resource Manager en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="8d290-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="8d290-105">Cuando lleva su propia imagen a Azure o incluso cuando arranca una de las imágenes de la plataforma, hay muchas razones por las que una máquina virtual puede entrar en un estado que no permita el arranque.</span><span class="sxs-lookup"><span data-stu-id="8d290-105">When bringing your own image to Azure or even booting one of the platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="8d290-106">Estas características le permiten diagnosticar y recuperar fácilmente las máquinas virtuales de los errores de arranque.</span><span class="sxs-lookup"><span data-stu-id="8d290-106">These features enable you to easily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="8d290-107">Para las máquinas virtuales Linux, puede ver fácilmente la salida de su registro de consola desde el portal:</span><span class="sxs-lookup"><span data-stu-id="8d290-107">For Linux Virtual Machines, you can easily view the output of your console log from the Portal:</span></span>

![Azure Portal](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="8d290-109">Sin embargo, para las máquinas virtuales Windows y Linux, Azure también le permite ver una captura de pantalla de la máquina virtual desde el hipervisor:</span><span class="sxs-lookup"><span data-stu-id="8d290-109">However, for both Windows and Linux Virtual Machines, Azure also enables you to see a screenshot of the VM from the hypervisor:</span></span>

![Error](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="8d290-111">Ambas características son compatibles para las máquinas virtuales de Azure en todas las regiones.</span><span class="sxs-lookup"><span data-stu-id="8d290-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="8d290-112">Tenga en cuenta que las capturas de pantalla y la salida pueden tardar hasta 10 minutos en aparecer en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="8d290-112">Note, screenshots, and output can take up to 10 minutes to appear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="8d290-113">Errores comunes de arranque</span><span class="sxs-lookup"><span data-stu-id="8d290-113">Common boot errors</span></span>

- [<span data-ttu-id="8d290-114">Problemas del sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="8d290-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="8d290-115">Problemas de kernel</span><span class="sxs-lookup"><span data-stu-id="8d290-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="8d290-116">Errores de FSTAB</span><span class="sxs-lookup"><span data-stu-id="8d290-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="8d290-117">Habilitación del diagnóstico en una nueva máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8d290-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="8d290-118">Cuando cree una máquina virtual desde la versión preliminar del portal, seleccione **Azure Resource Manager** en la lista desplegable de modelo de implementación:</span><span class="sxs-lookup"><span data-stu-id="8d290-118">When creating a new Virtual Machine from the Preview Portal, select the **Azure Resource Manager** from the deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="8d290-120">Configure la opción Supervisión para seleccionar la cuenta de almacenamiento donde desee colocar estos archivos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="8d290-120">Configure the Monitoring option to select the storage account where you would like to place these diagnostic files.</span></span>
 
    ![Creación de una máquina virtual](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="8d290-122">Si va a realizar la implementación con una plantilla de Azure Resource Manager, vaya al recurso de máquina virtual y anexe la sección de perfil de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="8d290-122">If you are deploying from an Azure Resource Manager template, navigate to your Virtual Machine resource and append the diagnostics profile section.</span></span> <span data-ttu-id="8d290-123">Recuerde usar el encabezado de versión de API "2015-06-15".</span><span class="sxs-lookup"><span data-stu-id="8d290-123">Remember to use the “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="8d290-124">El perfil de diagnóstico le permite seleccionar la cuenta de almacenamiento donde desea colocar estos registros.</span><span class="sxs-lookup"><span data-stu-id="8d290-124">The diagnostics profile enables you to select the storage account where you want to put these logs.</span></span>

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

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="8d290-125">Actualización de una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="8d290-125">Update an existing virtual machine</span></span>

<span data-ttu-id="8d290-126">Para habilitar el diagnóstico de arranque a través del portal, también puede actualizar una máquina virtual existente en el portal.</span><span class="sxs-lookup"><span data-stu-id="8d290-126">To enable boot diagnostics through the portal, you can also update an existing virtual machine through the portal.</span></span> <span data-ttu-id="8d290-127">Seleccione la opción Diagnósticos de arranque y guarde.</span><span class="sxs-lookup"><span data-stu-id="8d290-127">Select the Boot Diagnostics option and Save.</span></span> <span data-ttu-id="8d290-128">Reinicie la máquina virtual para que surta efecto.</span><span class="sxs-lookup"><span data-stu-id="8d290-128">Restart the VM to take effect.</span></span>

![Actualización de una máquina virtual existente](./media/boot-diagnostics/screenshot5.png)