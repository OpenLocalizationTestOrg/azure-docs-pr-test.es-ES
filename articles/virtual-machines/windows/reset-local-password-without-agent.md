---
title: "Restablecimiento de una contraseña local de Windows sin el agente de Azure| Microsoft Docs"
description: "Restablecimiento de la contraseña de una cuenta de usuario de Windows local cuando el agente invitado de Azure no está instalado o funcionando en una VM"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: 880f5e5967298401fc2522124af3746d9906ffa8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-local-windows-password-for-azure-vm"></a><span data-ttu-id="a7408-103">Restablecimiento de una contraseña de Windows local para VM de Azure</span><span class="sxs-lookup"><span data-stu-id="a7408-103">How to reset local Windows password for Azure VM</span></span>
<span data-ttu-id="a7408-104">Puede restablecer la contraseña de Windows local de una VM en Azure mediante [Azure Portal o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) siempre que el agente invitado de Azure esté instalado.</span><span class="sxs-lookup"><span data-stu-id="a7408-104">You can reset the local Windows password of a VM in Azure using the [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) provided the Azure guest agent is installed.</span></span> <span data-ttu-id="a7408-105">Este método es la manera principal de restablecer una contraseña para una VM de Azure.</span><span class="sxs-lookup"><span data-stu-id="a7408-105">This method is the primary way to reset a password for an Azure VM.</span></span> <span data-ttu-id="a7408-106">Si tiene problemas con el agente de invitado de Azure, como puede ser que no responda o que no se pueda instalar después de cargar una imagen personalizada, puede restablecer manualmente una contraseña de Windows.</span><span class="sxs-lookup"><span data-stu-id="a7408-106">If you encounter issues with the Azure guest agent not responding, or failing to install after uploading a custom image, you can manually reset a Windows password.</span></span> <span data-ttu-id="a7408-107">En este artículo se detalla cómo restablecer la contraseña de una cuenta local asociando el disco virtual de SO de origen a otra VM.</span><span class="sxs-lookup"><span data-stu-id="a7408-107">This article details how to reset a local account password by attaching the source OS virtual disk to another VM.</span></span> 

> [!WARNING]
> <span data-ttu-id="a7408-108">Utilice este proceso solamente como último recurso.</span><span class="sxs-lookup"><span data-stu-id="a7408-108">Only use this process as a last resort.</span></span> <span data-ttu-id="a7408-109">Intente siempre restablecer una contraseña mediante [Azure Portal o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) primero.</span><span class="sxs-lookup"><span data-stu-id="a7408-109">Always try to reset a password using the [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) first.</span></span>
> 
> 

## <a name="overview-of-the-process"></a><span data-ttu-id="a7408-110">Información general del proceso</span><span class="sxs-lookup"><span data-stu-id="a7408-110">Overview of the process</span></span>
<span data-ttu-id="a7408-111">Los pasos principales para realizar un restablecimiento de contraseña para una VM con Windows en Azure cuando no hay acceso al agente invitado de Azure son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="a7408-111">The core steps for performing a local password reset for a Windows VM in Azure when there is no access to the Azure guest agent is as follows:</span></span>

* <span data-ttu-id="a7408-112">Eliminar la VM de origen.</span><span class="sxs-lookup"><span data-stu-id="a7408-112">Delete the source VM.</span></span> <span data-ttu-id="a7408-113">Los discos virtuales se conservan.</span><span class="sxs-lookup"><span data-stu-id="a7408-113">The virtual disks are retained.</span></span>
* <span data-ttu-id="a7408-114">Asociar el disco del SO de la máquina virtual de origen a otra máquina virtual con la misma ubicación dentro de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a7408-114">Attach the source VM's OS disk to another VM on the same location within your Azure subscription.</span></span> <span data-ttu-id="a7408-115">Se hace referencia a esta VM como la VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="a7408-115">This VM is referred to as the troubleshooting VM.</span></span>
* <span data-ttu-id="a7408-116">Con la VM para solucionar problemas, cree algunos archivos de configuración en el disco del SO de la VM de origen.</span><span class="sxs-lookup"><span data-stu-id="a7408-116">Using the troubleshooting VM, create some config files on the source VM's OS disk.</span></span>
* <span data-ttu-id="a7408-117">Desasocie el disco del SO de la VM de la VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="a7408-117">Detach the VM's OS disk from the troubleshooting VM.</span></span>
* <span data-ttu-id="a7408-118">Use una plantilla de Resource Manager para crear una VM mediante el disco virtual original.</span><span class="sxs-lookup"><span data-stu-id="a7408-118">Use a Resource Manager template to create a VM, using the original virtual disk.</span></span>
* <span data-ttu-id="a7408-119">Cuando se inicia la nueva VM, los archivos de configuración que crea actualizan la contraseña del usuario necesario.</span><span class="sxs-lookup"><span data-stu-id="a7408-119">When the new VM boots, the config files you create update the password of the required user.</span></span>

## <a name="detailed-steps"></a><span data-ttu-id="a7408-120">Pasos detallados</span><span class="sxs-lookup"><span data-stu-id="a7408-120">Detailed steps</span></span>
<span data-ttu-id="a7408-121">Intente siempre restablecer una contraseña mediante [Azure Portal o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de intentar llevar a cabo los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="a7408-121">Always try to reset a password using the [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before trying the following steps.</span></span> <span data-ttu-id="a7408-122">Asegúrese de que tiene una copia de seguridad de la VM antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="a7408-122">Make sure you have a backup of your VM before you start.</span></span> 

1. <span data-ttu-id="a7408-123">Elimine la VM afectada de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a7408-123">Delete the affected VM in Azure portal.</span></span> <span data-ttu-id="a7408-124">La eliminación de la VM, solo elimina los metadatos, la referencia de la VM dentro de Azure.</span><span class="sxs-lookup"><span data-stu-id="a7408-124">Deleting the VM only deletes the metadata, the reference of the VM within Azure.</span></span> <span data-ttu-id="a7408-125">Los discos virtuales se conservan cuando se elimina la VM:</span><span class="sxs-lookup"><span data-stu-id="a7408-125">The virtual disks are retained when the VM is deleted:</span></span>
   
   * <span data-ttu-id="a7408-126">Seleccione la VM en Azure Portal y haga clic en *Eliminar*:</span><span class="sxs-lookup"><span data-stu-id="a7408-126">Select the VM in the Azure portal, click *Delete*:</span></span>
     
     ![Eliminación de la VM existente](./media/reset-local-password-without-agent/delete_vm.png)
2. <span data-ttu-id="a7408-128">Asocie el disco del SO de la VM de origen a la VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="a7408-128">Attach the source VM’s OS disk to the troubleshooting VM.</span></span> <span data-ttu-id="a7408-129">La VM de solución de problemas debe estar en la misma región que el disco del SO de la VM de origen (como `West US`):</span><span class="sxs-lookup"><span data-stu-id="a7408-129">The troubleshooting VM must be in the same region as the source VM's OS disk (such as `West US`):</span></span>
   
   * <span data-ttu-id="a7408-130">Seleccione la VM de solución de problemas en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a7408-130">Select the troubleshooting VM in the Azure portal.</span></span> <span data-ttu-id="a7408-131">Haga clic en *Discos* | *Asociar existente*:</span><span class="sxs-lookup"><span data-stu-id="a7408-131">Click *Disks* | *Attach existing*:</span></span>
     
     ![Conectar disco existente](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     <span data-ttu-id="a7408-133">Seleccione *Archivo VHD* y seleccione la cuenta de almacenamiento que contiene su VM de origen:</span><span class="sxs-lookup"><span data-stu-id="a7408-133">Select *VHD File* and then select the storage account that contains your source VM:</span></span>
     
     ![Selección de la cuenta de almacenamiento](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     <span data-ttu-id="a7408-135">Seleccione el contenedor de origen.</span><span class="sxs-lookup"><span data-stu-id="a7408-135">Select the source container.</span></span> <span data-ttu-id="a7408-136">El contenedor de origen suele ser *vhds*:</span><span class="sxs-lookup"><span data-stu-id="a7408-136">The source container is typically *vhds*:</span></span>
     
     ![Selección del contenedor de almacenamiento](./media/reset-local-password-without-agent/disks_select_container.png)
     
     <span data-ttu-id="a7408-138">Seleccione el disco duro virtual de SO para asociar.</span><span class="sxs-lookup"><span data-stu-id="a7408-138">Select the OS vhd to attach.</span></span> <span data-ttu-id="a7408-139">Haga clic en *Seleccionar* para completar el proceso:</span><span class="sxs-lookup"><span data-stu-id="a7408-139">Click *Select* to complete the process:</span></span>
     
     ![Seleccione el disco virtual de origen](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. <span data-ttu-id="a7408-141">Conéctese a la VM de solución de problemas mediante Escritorio remoto y asegúrese de que el disco del SO de la VM de origen está visible:</span><span class="sxs-lookup"><span data-stu-id="a7408-141">Connect to the troubleshooting VM using Remote Desktop and ensure the source VM's OS disk is visible:</span></span>
   
   * <span data-ttu-id="a7408-142">Seleccione la VM de solución de problemas en Azure Portal y haga clic en *Conectar*.</span><span class="sxs-lookup"><span data-stu-id="a7408-142">Select the troubleshooting VM in the Azure portal and click *Connect*.</span></span>
   * <span data-ttu-id="a7408-143">Abra el archivo RDP que descarga.</span><span class="sxs-lookup"><span data-stu-id="a7408-143">Open the RDP file that downloads.</span></span> <span data-ttu-id="a7408-144">Escriba el nombre de usuario y la contraseña de la VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="a7408-144">Enter the username and password of the troubleshooting VM.</span></span>
   * <span data-ttu-id="a7408-145">En el Explorador de archivos, busque el disco de datos que se ha asociado.</span><span class="sxs-lookup"><span data-stu-id="a7408-145">In File Explorer, look for the data disk you attached.</span></span> <span data-ttu-id="a7408-146">Si el origen de disco duro virtual de la VM es el único disco de datos asociado a la VM de solución de problemas, debe ser la unidad F:</span><span class="sxs-lookup"><span data-stu-id="a7408-146">If the source VM’s VHD is the only data disk attached to the troubleshooting VM, it should be the F: drive:</span></span>
     
     ![Visualización del disco de datos conectado](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. <span data-ttu-id="a7408-148">Cree `gpt.ini` en `\Windows\System32\GroupPolicy` en la unidad de la VM de origen (si gpt.ini existe, cambie el nombre a gpt.ini.bak):</span><span class="sxs-lookup"><span data-stu-id="a7408-148">Create `gpt.ini` in `\Windows\System32\GroupPolicy` on the source VM’s drive (if gpt.ini exists, rename to gpt.ini.bak):</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="a7408-149">Asegúrese de que no crea accidentalmente los siguientes archivos en C:\Windows, la unidad del SO para la VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="a7408-149">Make sure that you do not accidentally create the following files in C:\Windows, the OS drive for the troubleshooting VM.</span></span> <span data-ttu-id="a7408-150">Cree los siguientes archivos en la unidad del SO para la VM que se asocia como disco de datos.</span><span class="sxs-lookup"><span data-stu-id="a7408-150">Create the following files in the OS drive for your source VM that is attached as a data disk.</span></span>
   > 
   > 
   
   * <span data-ttu-id="a7408-151">Agregue las líneas siguientes al archivo `gpt.ini` que creó:</span><span class="sxs-lookup"><span data-stu-id="a7408-151">Add the following lines into the `gpt.ini` file you created:</span></span>
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Creación de gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. <span data-ttu-id="a7408-153">Cree `scripts.ini` en `\Windows\System32\GroupPolicy\Machine\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="a7408-153">Create `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span></span> <span data-ttu-id="a7408-154">Asegúrese de que se muestran las carpetas ocultas.</span><span class="sxs-lookup"><span data-stu-id="a7408-154">Make sure hidden folders are shown.</span></span> <span data-ttu-id="a7408-155">Si es necesario, cree las carpetas `Machine` o `Scripts`.</span><span class="sxs-lookup"><span data-stu-id="a7408-155">If needed, create the `Machine` or `Scripts` folders.</span></span>
   
   * <span data-ttu-id="a7408-156">Agregue las líneas siguientes al archivo `scripts.ini` que creó:</span><span class="sxs-lookup"><span data-stu-id="a7408-156">Add the following lines the `scripts.ini` file you created:</span></span>
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Creación de scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. <span data-ttu-id="a7408-158">Crear `FixAzureVM.cmd` en `\Windows\System32` con el contenido siguiente, reemplazando `<username>` y `<newpassword>` por sus propios valores:</span><span class="sxs-lookup"><span data-stu-id="a7408-158">Create `FixAzureVM.cmd` in `\Windows\System32` with the following contents, replacing `<username>` and `<newpassword>` with your own values:</span></span>
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![Creación de FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    <span data-ttu-id="a7408-160">Al definir la nueva contraseña debe cumplir los requisitos de complejidad de contraseña configurada para la VM.</span><span class="sxs-lookup"><span data-stu-id="a7408-160">You must meet the configured password complexity requirements for your VM when defining the new password.</span></span>
7. <span data-ttu-id="a7408-161">En Azure Portal, desasocie el disco de la VM de solución de problemas:</span><span class="sxs-lookup"><span data-stu-id="a7408-161">In Azure portal, detach the disk from the troubleshooting VM:</span></span>
   
   * <span data-ttu-id="a7408-162">Seleccione la VM de solución de problemas en Azure Portal y haga clic en *Discos*.</span><span class="sxs-lookup"><span data-stu-id="a7408-162">Select the troubleshooting VM in the Azure portal, click *Disks*.</span></span>
   * <span data-ttu-id="a7408-163">Seleccione el disco de datos asociado en el paso 2, haga clic en *Desasociar*:</span><span class="sxs-lookup"><span data-stu-id="a7408-163">Select the data disk attached in step 2, click *Detach*:</span></span>
     
     ![Desasociación del disco](./media/reset-local-password-without-agent/detach_disk.png)
8. <span data-ttu-id="a7408-165">Antes de crear una VM, obtenga el URI en el disco del SO de origen:</span><span class="sxs-lookup"><span data-stu-id="a7408-165">Before you create a VM, obtain the URI to your source OS disk:</span></span>
   
   * <span data-ttu-id="a7408-166">Seleccione la cuenta de almacenamiento en Azure Portal y haga clic en *Blobs*.</span><span class="sxs-lookup"><span data-stu-id="a7408-166">Select the storage account in the Azure portal, click *Blobs*.</span></span>
   * <span data-ttu-id="a7408-167">Seleccione el contenedor.</span><span class="sxs-lookup"><span data-stu-id="a7408-167">Select the container.</span></span> <span data-ttu-id="a7408-168">El contenedor de origen suele ser *vhds*:</span><span class="sxs-lookup"><span data-stu-id="a7408-168">The source container is typically *vhds*:</span></span>
     
     ![Seleccione el blob de la cuenta de almacenamiento](./media/reset-local-password-without-agent/select_storage_details.png)
     
     <span data-ttu-id="a7408-170">Seleccione el disco duro virtual del sistema operativo de la VM y haga clic en el botón *Copiar* situado junto al nombre de *URL*:</span><span class="sxs-lookup"><span data-stu-id="a7408-170">Select your source VM OS VHD and click the *Copy* button next to the *URL* name:</span></span>
     
     ![Copia del URI de disco](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. <span data-ttu-id="a7408-172">Cree una VM desde el disco del SO de la VM de origen:</span><span class="sxs-lookup"><span data-stu-id="a7408-172">Create a VM from the source VM’s OS disk:</span></span>
   
   * <span data-ttu-id="a7408-173">Use [esta plantilla de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) para crear una VM desde un disco duro virtual especializado.</span><span class="sxs-lookup"><span data-stu-id="a7408-173">Use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) to create a VM from a specialized VHD.</span></span> <span data-ttu-id="a7408-174">Haga clic en el botón `Deploy to Azure` para abrir Azure Portal con los detalles de la plantilla rellenados automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a7408-174">Click the `Deploy to Azure` button to open the Azure portal with the templated details populated for you.</span></span>
   * <span data-ttu-id="a7408-175">Si desea conservar toda la configuración anterior de la VM, seleccione *Editar plantilla* para proporcionar la red virtual, la subred, el adaptador de red o la dirección IP pública existentes.</span><span class="sxs-lookup"><span data-stu-id="a7408-175">If you want to retain all the previous settings for the VM, select *Edit template* to provide your existing VNet, subnet, network adapter, or public IP.</span></span>
   * <span data-ttu-id="a7408-176">En el cuadro de texto del parámetro `OSDISKVHDURI`, pegue el URI de su disco duro virtual de origen obtenido en el paso anterior:</span><span class="sxs-lookup"><span data-stu-id="a7408-176">In the `OSDISKVHDURI` parameter text box, paste the URI of your source VHD obtain in the preceding step:</span></span>
     
     ![Creación de una VM a partir de una plantilla](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. <span data-ttu-id="a7408-178">Después de que la CM se ejecute, conéctese a la VM mediante Escritorio remoto con la nueva contraseña que especificó en el script `FixAzureVM.cmd`.</span><span class="sxs-lookup"><span data-stu-id="a7408-178">After the new VM is running, connect to the VM using Remote Desktop with the new password you specified in the `FixAzureVM.cmd` script.</span></span>
11. <span data-ttu-id="a7408-179">En la sesión remota respecto a la nueva VM, quite los archivos siguientes para limpiar el entorno:</span><span class="sxs-lookup"><span data-stu-id="a7408-179">From your remote session to the new VM, remove the following files to clean up the environment:</span></span>
    
    * <span data-ttu-id="a7408-180">De %windir%\System32</span><span class="sxs-lookup"><span data-stu-id="a7408-180">From %windir%\System32</span></span>
      * <span data-ttu-id="a7408-181">quite FixAzureVM.cmd</span><span class="sxs-lookup"><span data-stu-id="a7408-181">remove FixAzureVM.cmd</span></span>
    * <span data-ttu-id="a7408-182">De %windir%\System32\GroupPolicy\Machine\\</span><span class="sxs-lookup"><span data-stu-id="a7408-182">From %windir%\System32\GroupPolicy\Machine\\</span></span>
      * <span data-ttu-id="a7408-183">quite scripts.ini</span><span class="sxs-lookup"><span data-stu-id="a7408-183">remove scripts.ini</span></span>
    * <span data-ttu-id="a7408-184">De %windir%\System32\GroupPolicy</span><span class="sxs-lookup"><span data-stu-id="a7408-184">From %windir%\System32\GroupPolicy</span></span>
      * <span data-ttu-id="a7408-185">quite gpt.ini (si gpt.ini existía antes y cambió su nombre a gpt.ini.bak, vuelva a cambiar el nombre del archivo .bak a gpt.ini)</span><span class="sxs-lookup"><span data-stu-id="a7408-185">remove gpt.ini (if gpt.ini existed before, and you renamed it to gpt.ini.bak, rename the .bak file back to gpt.ini)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7408-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a7408-186">Next steps</span></span>
<span data-ttu-id="a7408-187">Si sigue sin poder conectarse mediante Escritorio remoto, consulte la [guía de solución de problemas de RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a7408-187">If you still cannot connect using Remote Desktop, see the [RDP troubleshooting guide](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="a7408-188">La [guía detallada de solución de problemas de RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) examina los métodos de solución de problemas en lugar de pasos específicos.</span><span class="sxs-lookup"><span data-stu-id="a7408-188">The [detailed RDP troubleshooting guide](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) looks at troubleshooting methods rather than specific steps.</span></span> <span data-ttu-id="a7408-189">También puede [abrir una solicitud de soporte técnico de Azure](https://azure.microsoft.com/support/options/) para obtener ayuda práctica.</span><span class="sxs-lookup"><span data-stu-id="a7408-189">You can also [open an Azure support request](https://azure.microsoft.com/support/options/) for hands-on assistance.</span></span>

