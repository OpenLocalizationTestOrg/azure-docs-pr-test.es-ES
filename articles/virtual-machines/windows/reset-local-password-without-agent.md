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
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a>¿Cómo tooreset de contraseña de Windows local para la máquina virtual de Azure
Se puede restablecer la contraseña de Windows local de Hola de una máquina virtual en Azure con hello [portal de Azure o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) siempre que esté instalado el agente de invitado de Azure Hola. Este método es tooreset de modo principal de hello una contraseña para una VM de Azure. Si encuentra problemas con el agente de invitado de Azure de hello no responde o dan error tooinstall después de cargar una imagen personalizada, puede restablecer manualmente una contraseña de Windows. Este artículo detalla cómo tooreset la contraseña de una cuenta local mediante una asociación Hola tooanother de disco virtual de origen SO máquina virtual. 

> [!WARNING]
> Utilice este proceso solamente como último recurso. Pruebe siempre tooreset una contraseña mediante hello [portal de Azure o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) primero.
> 
> 

## <a name="overview-of-hello-process"></a>Información general del proceso de Hola
pasos de núcleo de Hola para llevar a cabo local restablezca la contraseña de una VM de Windows en Azure cuando no hay ningún agente de invitado de Azure de toohello de acceso es como sigue:

* Eliminar una VM de origen Hola. se conservan los discos virtuales de Hola.
* Adjuntar disco tooanother VM de la VM de origen Hola OS en hello misma ubicación dentro de su suscripción de Azure. Esta máquina virtual es hello de que se hace referencia tooas solución de problemas de máquina virtual.
* Con hello, solución de problemas de VM, cree algunos archivos de configuración en el disco del sistema operativo de la VM de origen Hola.
* Desconectar el disco de sistema operativo de la máquina virtual de Hola de hello VM de solución de problemas.
* Utilice un toocreate de plantilla de administrador de recursos una máquina virtual, con el disco virtual original de Hola.
* Cuando se arranca de máquina virtual nueva, Hola Hola archivos de configuración crear Hola actualizar la contraseña del usuario de hello necesario.

## <a name="detailed-steps"></a>Pasos detallados
Pruebe siempre tooreset una contraseña mediante hello [portal de Azure o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de intentar Hola pasos. Asegúrese de que tiene una copia de seguridad de la VM antes de empezar. 

1. Eliminar Hola afectadas VM en el portal de Azure. Eliminando Hola VM solo elimina metadatos hello, referencia de Hola de hello VM dentro de Azure. discos virtuales Hola se conservan cuando se elimina Hola VM:
   
   * Seleccione Hola VM Hola portal de Azure, haga clic en *eliminar*:
     
     ![Eliminación de la VM existente](./media/reset-local-password-without-agent/delete_vm.png)
2. Adjuntar toohello de disco de SO de la VM de origen de hello VM de solución de problemas. Hola, solución de problemas de máquina virtual debe estar en hello misma región que el disco del sistema operativo de la VM de origen de hello (como `West US`):
   
   * Seleccione Hola solución de problemas de VM en hello portal de Azure. Haga clic en *Discos* | *Asociar existente*:
     
     ![Conectar disco existente](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     Seleccione *archivo VHD* y, a continuación, seleccione cuenta de almacenamiento de Hola que contiene el origen de máquina virtual:
     
     ![Selección de la cuenta de almacenamiento](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     Seleccione el contenedor de origen Hola. Normalmente es el contenedor de origen de Hello *discos duros virtuales*:
     
     ![Selección del contenedor de almacenamiento](./media/reset-local-password-without-agent/disks_select_container.png)
     
     Seleccione tooattach de disco duro virtual del sistema operativo de Hola. Haga clic en *seleccione* proceso de Hola toocomplete:
     
     ![Seleccione el disco virtual de origen](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. Conectar toohello solución de problemas de máquina virtual mediante Escritorio remoto y asegúrese de disco del sistema operativo de la VM de origen de hello:
   
   * Seleccione Hola solución de problemas de VM en hello portal de Azure y haga clic en *conectar*.
   * Abra el archivo RDP de Hola que descarga. Escriba Hola username y password de hello VM de solución de problemas.
   * En el Explorador de archivos, busque el disco de datos de hello que ha adjuntado. Si hello origen en el que disco duro virtual de la máquina virtual hello solamente los datos disco conectado toohello solución de problemas de máquina virtual, debe ser la unidad F: hello:
     
     ![Visualización del disco de datos conectado](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. Crear `gpt.ini` en `\Windows\System32\GroupPolicy` en la unidad de la VM de origen de hello (si existe gpt.ini, cambie el nombre toogpt.ini.bak):
   
   > [!WARNING]
   > Asegúrese de que accidentalmente crear hello siguientes archivos en C:\Windows, Hola Hola VM de solución de problemas en la unidad del SO. Crear Hola siguientes archivos en la unidad de hello SO para el máquina virtual que se adjunta como un disco de datos de origen.
   > 
   > 
   
   * Agregar Hola siguiendo las líneas en hello `gpt.ini` archivo que ha creado:
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Creación de gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. Cree `scripts.ini` en `\Windows\System32\GroupPolicy\Machine\Scripts`. Asegúrese de que se muestran las carpetas ocultas. Si es necesario, cree hello `Machine` o `Scripts` carpetas.
   
   * Agregar Hola después Hola líneas `scripts.ini` archivo que ha creado:
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Creación de scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. Crear `FixAzureVM.cmd` en `\Windows\System32` con hello después de contenido, reemplazando `<username>` y `<newpassword>` con sus propios valores:
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![Creación de FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    Debe cumplir requisitos de complejidad de contraseña de hello configurado para la máquina virtual al definir la nueva contraseña de Hola.
7. En el portal de Azure, desconectar el disco de Hola de hello VM de solución de problemas:
   
   * Seleccione Hola solución de problemas de VM en hello portal de Azure, haga clic en *discos*.
   * Disco de datos de hello seleccione adjunta en el paso 2, haga clic en *separar*:
     
     ![Desasociación del disco](./media/reset-local-password-without-agent/detach_disk.png)
8. Antes de crear una máquina virtual, obtenga el disco del sistema operativo de origen de hello URI tooyour:
   
   * Cuenta de almacenamiento seleccione Hola Hola portal de Azure, haga clic en *Blobs*.
   * Seleccione el contenedor de Hola. Normalmente es el contenedor de origen de Hello *discos duros virtuales*:
     
     ![Seleccione el blob de la cuenta de almacenamiento](./media/reset-local-password-without-agent/select_storage_details.png)
     
     Seleccione el disco duro virtual de sistema operativo de máquina virtual de origen y haga clic en hello *copia* botón siguiente toohello *URL* nombre:
     
     ![Copia del URI de disco](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. Crear una máquina virtual del disco de sistema operativo de la VM de origen de hello:
   
   * Use [esta plantilla de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate una máquina virtual desde un disco duro virtual especializada. Haga clic en hello `Deploy tooAzure` Hola de botón tooopen portal de Azure con detalles con plantilla Hola rellenado automáticamente.
   * Si desea que tooretain toda la configuración anterior Hola de hello VM, seleccione *Editar plantilla* tooprovide su red virtual existente, la subred, el adaptador de red o la dirección IP pública.
   * Hola `OSDISKVHDURI` cuadro de texto del parámetro, Hola pegar obtener el URI de su disco duro virtual de origen de Hola anterior paso:
     
     ![Creación de una VM a partir de una plantilla](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. Después de hello nueva máquina virtual se está ejecutando, conéctese toohello máquina virtual mediante Escritorio remoto con la contraseña nueva Hola especificado en hello `FixAzureVM.cmd` secuencia de comandos.
11. Desde la sesión remota toohello nueva máquina virtual, Hola remove después archivos tooclean entorno hello:
    
    * De %windir%\System32
      * quite FixAzureVM.cmd
    * De %windir%\System32\GroupPolicy\Machine\
      * quite scripts.ini
    * De %windir%\System32\GroupPolicy
      * quitar gpt.ini (si gpt.ini existía antes y cambió de nombre toogpt.ini.bak, rename Hola .bak archivo back-toogpt.ini)

## <a name="next-steps"></a>Pasos siguientes
Si sigue sin poder conectarse mediante Escritorio remoto, vea hello [Guía de solución de problemas de RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Hola [detallada guía de solución de problemas de RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) examina métodos en lugar de pasos específicos de solución de problemas. También puede [abrir una solicitud de soporte técnico de Azure](https://azure.microsoft.com/support/options/) para obtener ayuda práctica.

