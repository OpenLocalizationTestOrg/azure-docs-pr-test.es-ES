---
title: "aaaReset una contraseña de Windows local sin agente de Azure | Documentos de Microsoft"
description: "¿Cómo tooreset Hola contraseña de una cuenta de usuario de Windows local al agente de invitado de Azure de hello no está instalado ni funciona en una máquina virtual"
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
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a><span data-ttu-id="20656-103">¿Cómo tooreset de contraseña de Windows local para la máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="20656-103">How tooreset local Windows password for Azure VM</span></span>
<span data-ttu-id="20656-104">Se puede restablecer la contraseña de Windows local de Hola de una máquina virtual en Azure con hello [portal de Azure o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) siempre que esté instalado el agente de invitado de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="20656-104">You can reset hello local Windows password of a VM in Azure using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) provided hello Azure guest agent is installed.</span></span> <span data-ttu-id="20656-105">Este método es tooreset de modo principal de hello una contraseña para una VM de Azure.</span><span class="sxs-lookup"><span data-stu-id="20656-105">This method is hello primary way tooreset a password for an Azure VM.</span></span> <span data-ttu-id="20656-106">Si encuentra problemas con el agente de invitado de Azure de hello no responde o dan error tooinstall después de cargar una imagen personalizada, puede restablecer manualmente una contraseña de Windows.</span><span class="sxs-lookup"><span data-stu-id="20656-106">If you encounter issues with hello Azure guest agent not responding, or failing tooinstall after uploading a custom image, you can manually reset a Windows password.</span></span> <span data-ttu-id="20656-107">Este artículo detalla cómo tooreset la contraseña de una cuenta local mediante una asociación Hola tooanother de disco virtual de origen SO máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="20656-107">This article details how tooreset a local account password by attaching hello source OS virtual disk tooanother VM.</span></span> 

> [!WARNING]
> <span data-ttu-id="20656-108">Utilice este proceso solamente como último recurso.</span><span class="sxs-lookup"><span data-stu-id="20656-108">Only use this process as a last resort.</span></span> <span data-ttu-id="20656-109">Pruebe siempre tooreset una contraseña mediante hello [portal de Azure o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) primero.</span><span class="sxs-lookup"><span data-stu-id="20656-109">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) first.</span></span>
> 
> 

## <a name="overview-of-hello-process"></a><span data-ttu-id="20656-110">Información general del proceso de Hola</span><span class="sxs-lookup"><span data-stu-id="20656-110">Overview of hello process</span></span>
<span data-ttu-id="20656-111">pasos de núcleo de Hola para llevar a cabo local restablezca la contraseña de una VM de Windows en Azure cuando no hay ningún agente de invitado de Azure de toohello de acceso es como sigue:</span><span class="sxs-lookup"><span data-stu-id="20656-111">hello core steps for performing a local password reset for a Windows VM in Azure when there is no access toohello Azure guest agent is as follows:</span></span>

* <span data-ttu-id="20656-112">Eliminar una VM de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="20656-112">Delete hello source VM.</span></span> <span data-ttu-id="20656-113">se conservan los discos virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="20656-113">hello virtual disks are retained.</span></span>
* <span data-ttu-id="20656-114">Adjuntar disco tooanother VM de la VM de origen Hola OS en hello misma ubicación dentro de su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="20656-114">Attach hello source VM's OS disk tooanother VM on hello same location within your Azure subscription.</span></span> <span data-ttu-id="20656-115">Esta máquina virtual es hello de que se hace referencia tooas solución de problemas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="20656-115">This VM is referred tooas hello troubleshooting VM.</span></span>
* <span data-ttu-id="20656-116">Con hello, solución de problemas de VM, cree algunos archivos de configuración en el disco del sistema operativo de la VM de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="20656-116">Using hello troubleshooting VM, create some config files on hello source VM's OS disk.</span></span>
* <span data-ttu-id="20656-117">Desconectar el disco de sistema operativo de la máquina virtual de Hola de hello VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="20656-117">Detach hello VM's OS disk from hello troubleshooting VM.</span></span>
* <span data-ttu-id="20656-118">Utilice un toocreate de plantilla de administrador de recursos una máquina virtual, con el disco virtual original de Hola.</span><span class="sxs-lookup"><span data-stu-id="20656-118">Use a Resource Manager template toocreate a VM, using hello original virtual disk.</span></span>
* <span data-ttu-id="20656-119">Cuando se arranca de máquina virtual nueva, Hola Hola archivos de configuración crear Hola actualizar la contraseña del usuario de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="20656-119">When hello new VM boots, hello config files you create update hello password of hello required user.</span></span>

## <a name="detailed-steps"></a><span data-ttu-id="20656-120">Pasos detallados</span><span class="sxs-lookup"><span data-stu-id="20656-120">Detailed steps</span></span>
<span data-ttu-id="20656-121">Pruebe siempre tooreset una contraseña mediante hello [portal de Azure o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de intentar Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="20656-121">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before trying hello following steps.</span></span> <span data-ttu-id="20656-122">Asegúrese de que tiene una copia de seguridad de la VM antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="20656-122">Make sure you have a backup of your VM before you start.</span></span> 

1. <span data-ttu-id="20656-123">Eliminar Hola afectadas VM en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="20656-123">Delete hello affected VM in Azure portal.</span></span> <span data-ttu-id="20656-124">Eliminando Hola VM solo elimina metadatos hello, referencia de Hola de hello VM dentro de Azure.</span><span class="sxs-lookup"><span data-stu-id="20656-124">Deleting hello VM only deletes hello metadata, hello reference of hello VM within Azure.</span></span> <span data-ttu-id="20656-125">discos virtuales Hola se conservan cuando se elimina Hola VM:</span><span class="sxs-lookup"><span data-stu-id="20656-125">hello virtual disks are retained when hello VM is deleted:</span></span>
   
   * <span data-ttu-id="20656-126">Seleccione Hola VM Hola portal de Azure, haga clic en *eliminar*:</span><span class="sxs-lookup"><span data-stu-id="20656-126">Select hello VM in hello Azure portal, click *Delete*:</span></span>
     
     ![Eliminación de la VM existente](./media/reset-local-password-without-agent/delete_vm.png)
2. <span data-ttu-id="20656-128">Adjuntar toohello de disco de SO de la VM de origen de hello VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="20656-128">Attach hello source VM’s OS disk toohello troubleshooting VM.</span></span> <span data-ttu-id="20656-129">Hola, solución de problemas de máquina virtual debe estar en hello misma región que el disco del sistema operativo de la VM de origen de hello (como `West US`):</span><span class="sxs-lookup"><span data-stu-id="20656-129">hello troubleshooting VM must be in hello same region as hello source VM's OS disk (such as `West US`):</span></span>
   
   * <span data-ttu-id="20656-130">Seleccione Hola solución de problemas de VM en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="20656-130">Select hello troubleshooting VM in hello Azure portal.</span></span> <span data-ttu-id="20656-131">Haga clic en *Discos* | *Asociar existente*:</span><span class="sxs-lookup"><span data-stu-id="20656-131">Click *Disks* | *Attach existing*:</span></span>
     
     ![Conectar disco existente](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     <span data-ttu-id="20656-133">Seleccione *archivo VHD* y, a continuación, seleccione cuenta de almacenamiento de Hola que contiene el origen de máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="20656-133">Select *VHD File* and then select hello storage account that contains your source VM:</span></span>
     
     ![Selección de la cuenta de almacenamiento](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     <span data-ttu-id="20656-135">Seleccione el contenedor de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="20656-135">Select hello source container.</span></span> <span data-ttu-id="20656-136">Normalmente es el contenedor de origen de Hello *discos duros virtuales*:</span><span class="sxs-lookup"><span data-stu-id="20656-136">hello source container is typically *vhds*:</span></span>
     
     ![Selección del contenedor de almacenamiento](./media/reset-local-password-without-agent/disks_select_container.png)
     
     <span data-ttu-id="20656-138">Seleccione tooattach de disco duro virtual del sistema operativo de Hola.</span><span class="sxs-lookup"><span data-stu-id="20656-138">Select hello OS vhd tooattach.</span></span> <span data-ttu-id="20656-139">Haga clic en *seleccione* proceso de Hola toocomplete:</span><span class="sxs-lookup"><span data-stu-id="20656-139">Click *Select* toocomplete hello process:</span></span>
     
     ![Seleccione el disco virtual de origen](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. <span data-ttu-id="20656-141">Conectar toohello solución de problemas de máquina virtual mediante Escritorio remoto y asegúrese de disco del sistema operativo de la VM de origen de hello:</span><span class="sxs-lookup"><span data-stu-id="20656-141">Connect toohello troubleshooting VM using Remote Desktop and ensure hello source VM's OS disk is visible:</span></span>
   
   * <span data-ttu-id="20656-142">Seleccione Hola solución de problemas de VM en hello portal de Azure y haga clic en *conectar*.</span><span class="sxs-lookup"><span data-stu-id="20656-142">Select hello troubleshooting VM in hello Azure portal and click *Connect*.</span></span>
   * <span data-ttu-id="20656-143">Abra el archivo RDP de Hola que descarga.</span><span class="sxs-lookup"><span data-stu-id="20656-143">Open hello RDP file that downloads.</span></span> <span data-ttu-id="20656-144">Escriba Hola username y password de hello VM de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="20656-144">Enter hello username and password of hello troubleshooting VM.</span></span>
   * <span data-ttu-id="20656-145">En el Explorador de archivos, busque el disco de datos de hello que ha adjuntado.</span><span class="sxs-lookup"><span data-stu-id="20656-145">In File Explorer, look for hello data disk you attached.</span></span> <span data-ttu-id="20656-146">Si hello origen en el que disco duro virtual de la máquina virtual hello solamente los datos disco conectado toohello solución de problemas de máquina virtual, debe ser la unidad F: hello:</span><span class="sxs-lookup"><span data-stu-id="20656-146">If hello source VM’s VHD is hello only data disk attached toohello troubleshooting VM, it should be hello F: drive:</span></span>
     
     ![Visualización del disco de datos conectado](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. <span data-ttu-id="20656-148">Crear `gpt.ini` en `\Windows\System32\GroupPolicy` en la unidad de la VM de origen de hello (si existe gpt.ini, cambie el nombre toogpt.ini.bak):</span><span class="sxs-lookup"><span data-stu-id="20656-148">Create `gpt.ini` in `\Windows\System32\GroupPolicy` on hello source VM’s drive (if gpt.ini exists, rename toogpt.ini.bak):</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="20656-149">Asegúrese de que accidentalmente crear hello siguientes archivos en C:\Windows, Hola Hola VM de solución de problemas en la unidad del SO.</span><span class="sxs-lookup"><span data-stu-id="20656-149">Make sure that you do not accidentally create hello following files in C:\Windows, hello OS drive for hello troubleshooting VM.</span></span> <span data-ttu-id="20656-150">Crear Hola siguientes archivos en la unidad de hello SO para el máquina virtual que se adjunta como un disco de datos de origen.</span><span class="sxs-lookup"><span data-stu-id="20656-150">Create hello following files in hello OS drive for your source VM that is attached as a data disk.</span></span>
   > 
   > 
   
   * <span data-ttu-id="20656-151">Agregar Hola siguiendo las líneas en hello `gpt.ini` archivo que ha creado:</span><span class="sxs-lookup"><span data-stu-id="20656-151">Add hello following lines into hello `gpt.ini` file you created:</span></span>
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Creación de gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. <span data-ttu-id="20656-153">Cree `scripts.ini` en `\Windows\System32\GroupPolicy\Machine\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="20656-153">Create `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span></span> <span data-ttu-id="20656-154">Asegúrese de que se muestran las carpetas ocultas.</span><span class="sxs-lookup"><span data-stu-id="20656-154">Make sure hidden folders are shown.</span></span> <span data-ttu-id="20656-155">Si es necesario, cree hello `Machine` o `Scripts` carpetas.</span><span class="sxs-lookup"><span data-stu-id="20656-155">If needed, create hello `Machine` or `Scripts` folders.</span></span>
   
   * <span data-ttu-id="20656-156">Agregar Hola después Hola líneas `scripts.ini` archivo que ha creado:</span><span class="sxs-lookup"><span data-stu-id="20656-156">Add hello following lines hello `scripts.ini` file you created:</span></span>
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Creación de scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. <span data-ttu-id="20656-158">Crear `FixAzureVM.cmd` en `\Windows\System32` con hello después de contenido, reemplazando `<username>` y `<newpassword>` con sus propios valores:</span><span class="sxs-lookup"><span data-stu-id="20656-158">Create `FixAzureVM.cmd` in `\Windows\System32` with hello following contents, replacing `<username>` and `<newpassword>` with your own values:</span></span>
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![Creación de FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    <span data-ttu-id="20656-160">Debe cumplir requisitos de complejidad de contraseña de hello configurado para la máquina virtual al definir la nueva contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="20656-160">You must meet hello configured password complexity requirements for your VM when defining hello new password.</span></span>
7. <span data-ttu-id="20656-161">En el portal de Azure, desconectar el disco de Hola de hello VM de solución de problemas:</span><span class="sxs-lookup"><span data-stu-id="20656-161">In Azure portal, detach hello disk from hello troubleshooting VM:</span></span>
   
   * <span data-ttu-id="20656-162">Seleccione Hola solución de problemas de VM en hello portal de Azure, haga clic en *discos*.</span><span class="sxs-lookup"><span data-stu-id="20656-162">Select hello troubleshooting VM in hello Azure portal, click *Disks*.</span></span>
   * <span data-ttu-id="20656-163">Disco de datos de hello seleccione adjunta en el paso 2, haga clic en *separar*:</span><span class="sxs-lookup"><span data-stu-id="20656-163">Select hello data disk attached in step 2, click *Detach*:</span></span>
     
     ![Desasociación del disco](./media/reset-local-password-without-agent/detach_disk.png)
8. <span data-ttu-id="20656-165">Antes de crear una máquina virtual, obtenga el disco del sistema operativo de origen de hello URI tooyour:</span><span class="sxs-lookup"><span data-stu-id="20656-165">Before you create a VM, obtain hello URI tooyour source OS disk:</span></span>
   
   * <span data-ttu-id="20656-166">Cuenta de almacenamiento seleccione Hola Hola portal de Azure, haga clic en *Blobs*.</span><span class="sxs-lookup"><span data-stu-id="20656-166">Select hello storage account in hello Azure portal, click *Blobs*.</span></span>
   * <span data-ttu-id="20656-167">Seleccione el contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="20656-167">Select hello container.</span></span> <span data-ttu-id="20656-168">Normalmente es el contenedor de origen de Hello *discos duros virtuales*:</span><span class="sxs-lookup"><span data-stu-id="20656-168">hello source container is typically *vhds*:</span></span>
     
     ![Seleccione el blob de la cuenta de almacenamiento](./media/reset-local-password-without-agent/select_storage_details.png)
     
     <span data-ttu-id="20656-170">Seleccione el disco duro virtual de sistema operativo de máquina virtual de origen y haga clic en hello *copia* botón siguiente toohello *URL* nombre:</span><span class="sxs-lookup"><span data-stu-id="20656-170">Select your source VM OS VHD and click hello *Copy* button next toohello *URL* name:</span></span>
     
     ![Copia del URI de disco](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. <span data-ttu-id="20656-172">Crear una máquina virtual del disco de sistema operativo de la VM de origen de hello:</span><span class="sxs-lookup"><span data-stu-id="20656-172">Create a VM from hello source VM’s OS disk:</span></span>
   
   * <span data-ttu-id="20656-173">Use [esta plantilla de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate una máquina virtual desde un disco duro virtual especializada.</span><span class="sxs-lookup"><span data-stu-id="20656-173">Use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate a VM from a specialized VHD.</span></span> <span data-ttu-id="20656-174">Haga clic en hello `Deploy tooAzure` Hola de botón tooopen portal de Azure con detalles con plantilla Hola rellenado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="20656-174">Click hello `Deploy tooAzure` button tooopen hello Azure portal with hello templated details populated for you.</span></span>
   * <span data-ttu-id="20656-175">Si desea que tooretain toda la configuración anterior Hola de hello VM, seleccione *Editar plantilla* tooprovide su red virtual existente, la subred, el adaptador de red o la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="20656-175">If you want tooretain all hello previous settings for hello VM, select *Edit template* tooprovide your existing VNet, subnet, network adapter, or public IP.</span></span>
   * <span data-ttu-id="20656-176">Hola `OSDISKVHDURI` cuadro de texto del parámetro, Hola pegar obtener el URI de su disco duro virtual de origen de Hola anterior paso:</span><span class="sxs-lookup"><span data-stu-id="20656-176">In hello `OSDISKVHDURI` parameter text box, paste hello URI of your source VHD obtain in hello preceding step:</span></span>
     
     ![Creación de una VM a partir de una plantilla](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. <span data-ttu-id="20656-178">Después de hello nueva máquina virtual se está ejecutando, conéctese toohello máquina virtual mediante Escritorio remoto con la contraseña nueva Hola especificado en hello `FixAzureVM.cmd` secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="20656-178">After hello new VM is running, connect toohello VM using Remote Desktop with hello new password you specified in hello `FixAzureVM.cmd` script.</span></span>
11. <span data-ttu-id="20656-179">Desde la sesión remota toohello nueva máquina virtual, Hola remove después archivos tooclean entorno hello:</span><span class="sxs-lookup"><span data-stu-id="20656-179">From your remote session toohello new VM, remove hello following files tooclean up hello environment:</span></span>
    
    * <span data-ttu-id="20656-180">De %windir%\System32</span><span class="sxs-lookup"><span data-stu-id="20656-180">From %windir%\System32</span></span>
      * <span data-ttu-id="20656-181">quite FixAzureVM.cmd</span><span class="sxs-lookup"><span data-stu-id="20656-181">remove FixAzureVM.cmd</span></span>
    * <span data-ttu-id="20656-182">De %windir%\System32\GroupPolicy\Machine\\</span><span class="sxs-lookup"><span data-stu-id="20656-182">From %windir%\System32\GroupPolicy\Machine\\</span></span>
      * <span data-ttu-id="20656-183">quite scripts.ini</span><span class="sxs-lookup"><span data-stu-id="20656-183">remove scripts.ini</span></span>
    * <span data-ttu-id="20656-184">De %windir%\System32\GroupPolicy</span><span class="sxs-lookup"><span data-stu-id="20656-184">From %windir%\System32\GroupPolicy</span></span>
      * <span data-ttu-id="20656-185">quitar gpt.ini (si gpt.ini existía antes y cambió de nombre toogpt.ini.bak, rename Hola .bak archivo back-toogpt.ini)</span><span class="sxs-lookup"><span data-stu-id="20656-185">remove gpt.ini (if gpt.ini existed before, and you renamed it toogpt.ini.bak, rename hello .bak file back toogpt.ini)</span></span>

## <a name="next-steps"></a><span data-ttu-id="20656-186">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="20656-186">Next steps</span></span>
<span data-ttu-id="20656-187">Si sigue sin poder conectarse mediante Escritorio remoto, vea hello [Guía de solución de problemas de RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="20656-187">If you still cannot connect using Remote Desktop, see hello [RDP troubleshooting guide](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="20656-188">Hola [detallada guía de solución de problemas de RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) examina métodos en lugar de pasos específicos de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="20656-188">hello [detailed RDP troubleshooting guide](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) looks at troubleshooting methods rather than specific steps.</span></span> <span data-ttu-id="20656-189">También puede [abrir una solicitud de soporte técnico de Azure](https://azure.microsoft.com/support/options/) para obtener ayuda práctica.</span><span class="sxs-lookup"><span data-stu-id="20656-189">You can also [open an Azure support request](https://azure.microsoft.com/support/options/) for hands-on assistance.</span></span>

