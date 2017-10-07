---
title: aaaHow toocreate una imagen de plantilla personalizada para Azure RemoteApp | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una plantilla personalizada de la imagen de Azure RemoteApp. Puede usar esta plantilla con una colección híbrida o en la nube."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: b9ec5b51-f7cd-470b-8545-d0fd714c5982
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9e3a0b2d3cc56177ea51406e6cecfe19ff235340
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-custom-template-image-for-azure-remoteapp"></a>¿Cómo toocreate una plantilla personalizada de la imagen de Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

RemoteApp de Azure utiliza un toohost de imagen de plantilla de Windows Server 2012 R2 en todos los programas de Hola que desee tooshare con los usuarios. toocreate una imagen de plantilla RemoteApp personalizada, puede comenzar con una imagen existente o cree uno nuevo. 

> [!TIP]
> ¿Sabía que ahora puede crear una imagen a partir de una máquina virtual de Azure? Una historia real y se reduce la cantidad de Hola de tiempo se toma tooimport Hola imagen. Consulte los pasos de Hola [aquí](remoteapp-image-on-azurevm.md).
> 
> 

requisitos de Hello para la imagen de Hola que se pueden cargar para su uso con Azure RemoteApp son:

* tamaño de la imagen de Hello debe ser un múltiplo de MB. Si intentas tooupload una imagen que no es un múltiplo exacto, se producirá un error en la carga de Hola.
* tamaño de la imagen de Hello debe ser 127 GB o menor.
* Debe estar en un archivo VHD (los archivos VHDX [unidades de disco duro virtuales de Hyper-V] no se admiten actualmente).
* Hola VHD no debe ser una máquina virtual de generación 2.
* Hola VHD puede ser de tamaño fijo o de expansión dinámica. Un disco duro virtual de expansión dinámica se recomienda porque toma menos tooAzure tooupload de tiempo que un archivo de disco duro virtual de tamaño fijo.
* disco de Hello debe inicializarse con estilo de partición de registro de arranque maestro (MBR) Hola. no se admite el estilo de partición GPT (tabla) de particiones GUID Hola.
* Hola VHD debe contener una única instalación de Windows Server 2012 R2. Puede contener varios volúmenes, pero uno de ellos con una instalación de Windows.
* deben estar instalados el rol de Host de sesión de escritorio remoto (RDSH) de Hola y la característica experiencia de escritorio de Hola.
* rol de agente de conexión a Escritorio remoto de Hello debe *no* instalarse.
* Sistema de archivos cifrados (EFS) de Hello debe deshabilitarse.
* Hello imagen debe estar preparada con Sysprep mediante parámetros de hello **/oobe /generalize /shutdown** (no usar hello **/mode: VM** parámetro).
* No se admite la carga de su VHD desde una cadena de instantáneas.

**Antes de empezar**

Necesita toodo Hola siguiente antes de crear el servicio de hello:

* [Suscríbase](https://azure.microsoft.com/services/remoteapp/) a RemoteApp.
* Crear una cuenta de usuario en Active Directory toouse como Hola cuenta de servicio de RemoteApp. Restrinja los permisos de Hola para esta cuenta para que sólo puede unirse a dominio de toohello máquinas. Consulte [Configuración de Azure Active Directory para RemoteApp](remoteapp-ad.md) para obtener más información.
* Recopile información sobre la red local: dirección IP de información y detalles de dispositivos VPN.
* Instalar hello [Azure PowerShell](/powershell/azure/overview) módulo.
* Recopilar información acerca de los usuarios de Hola que desee tener acceso toogrant a. Esta información puede ser información de cuentas de Microsoft o información de cuentas de trabajo de Active Directory de usuarios.

## <a name="create-a-template-image"></a>Creación de una imagen de plantilla
Estos son los pasos de alto nivel de hello toocreate una nueva imagen de plantilla desde el principio:

1. Busque un DVD o una imagen ISO de actualización de Windows Server 2012 R2.
2. Cree un archivo VHD.
3. Instale Windows Server 2012 R2.
4. Instalar el rol de Host de sesión de escritorio remoto (RDSH) de Hola y la característica experiencia de escritorio de Hola.
5. Instale las características adicionales que necesitan sus aplicaciones.
6. Instale y configure sus aplicaciones. aplicaciones de uso compartido de toomake más fácil, agregar las aplicaciones o programas que desee tooshare toohello **iniciar** menú de imagen de hello, específicamente en **%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs.
7. Realice cualquier configuración adicional de Windows que requieran sus aplicaciones.
8. Deshabilitar el sistema de archivos cifrados (EFS) de Hola.
9. **REQUIRED:** vaya tooWindows Update e instale todas las actualizaciones importantes.
10. Imagen de Hola SYSPREP.

Hello pasos detallados para crear una nueva imagen son:

1. Busque un DVD o una imagen ISO de actualización de Windows Server 2012 R2.
2. Cree un archivo VHD usando Administración de discos.
   
   1. Inicie Administración de discos (diskmgmt.msc).
   2. Cree un archivo VHD que se expanda dinámicamente con un tamaño mínimo de 40 GB. (Cantidad de Hola de estimación del espacio necesario para Windows, sus aplicaciones y las personalizaciones. Windows Server con rol de hello RDSH y la característica experiencia de escritorio instalada requerirá aproximadamente 10 GB de espacio).
      
      1. Haga clic en **Acción > Crear VHD**.
      2. Especifique la ubicación de hello, el tamaño y formato de disco duro virtual. Seleccione **Expansión dinámica** y haga clic en **Aceptar**.
      
      Esto se ejecutará durante varios segundos. Una vez completada Hola creación de disco duro virtual, verá un nuevo disco sin cualquier letra de unidad y está en estado "No inicializado" en la consola de administración de discos de Hola.
      
      * Haga clic en el disco de hello (no el espacio sin asignar de hello) y, a continuación, haga clic en **inicializar disco**. Seleccione **MBR** (Master Boot Record) como estilo de partición de hello y, a continuación, haga clic en **Aceptar**.
      * Crear un nuevo volumen: haga clic en hello espacio sin asignar y, a continuación, haga clic en **nuevo volumen Simple**. Puede aceptar valores predeterminados de hello en el Asistente de hello, pero asegúrese de que asignar un posibles problemas de unidad letra tooavoid al cargar imagen de plantilla de Hola.
      * Haga clic en el disco de hello y, a continuación, haga clic en **ocultar VHD**.
3. Instale Windows Server 2012 R2:
   
   1. Cree una nueva máquina virtual. Usar hello nuevo Asistente para la máquina Virtual en el Administrador de Hyper-V o cliente Hyper-V.
      1. En la página Especificar generación de hello, elija **generación 1**.
      2. En la página Conectar disco duro Virtual de hello, seleccione **usar un disco duro virtual existente**y examinar toohello disco duro virtual que creó en el paso anterior de Hola.
      3. En la página de opciones de instalación de hello, seleccione **instalar un sistema operativo desde un CD/DVD_ROM arranque**y, a continuación, Seleccionar ubicación de Hola de los medios de instalación de Windows Server 2012 R2.
      4. Elija otras opciones de hello asistente necesario tooinstall Windows y las aplicaciones. Finalice al Asistente de Hola.
   2. Cuando finalice el Asistente de hello, editar la configuración de Hola de máquina virtual de Hola y realice los cambios necesarios tooinstall Windows y los programas, como el número de procesadores virtuales, hello y, a continuación, haga clic en **Aceptar**.
   3. Conectar máquina virtual de toohello e instale Windows Server 2012 R2.
4. Instalar el rol de Host de sesión de escritorio remoto (RDSH) de Hola y la característica experiencia de escritorio de hello:
   1. Inicie Administrador de servidores.
   2. Haga clic en **agregar Roles y características** en pantalla de bienvenida de Hola o de hello **administrar** menú.
   3. Haga clic en **siguiente** en la página de hello antes de comenzar.
   4. Seleccione **Instalación basada en características o en roles** y haga clic en **Siguiente**.
   5. Seleccione el equipo local de Hola de lista de hello y, a continuación, haga clic en **siguiente**.
   6. Seleccione **Servicios de Escritorio remoto** y haga clic en **Siguiente**.
   7. Expanda **Infraestructura e interfaces de usuario** y seleccione **Experiencia de escritorio**.
   8. Haga clic en **Agregar características** y después en **Siguiente**.
   9. En la página de servicios de escritorio remoto de hello, haga clic en **siguiente**.
   10. Haga clic en **Host de sesión de Escritorio remoto**.
   11. Haga clic en **Agregar características** y después en **Siguiente**.
   12. En la página de selecciones de instalación de confirmar hello, seleccione **reinicie el servidor de destino Hola automáticamente si es necesario**y, a continuación, haga clic en **Sí** Hola reinicio advertencia.
   13. Haga clic en **Instalar**. Hola equipo se reiniciará.
5. Instalar características adicionales que necesitan las aplicaciones, como Hola .NET Framework 3.5. características de hello tooinstall, ejecute hello agregar Roles y características de asistente.
6. Instalar y configurar programas de Hola y aplicaciones que desea toopublish a través de RemoteApp.

> [!IMPORTANT]
> Instalar el rol de hello RDSH antes de instalar aplicaciones tooensure que se han detectado problemas con la compatibilidad de aplicaciones antes de que sea la imagen de Hola cargado tooRemoteApp.
> 
> Asegúrese de que una aplicación de tooyour de acceso directo (**.lnk** archivo) aparece en hello **iniciar** menú para todos los usuarios (%systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs). Asegúrese también de ese icono Hola vea Hola **iniciar** menú es lo que desea toosee de los usuarios. Si no es así, cámbielo. (No *tienen* menú de inicio de tooadd Hola aplicación toohello, pero resulta mucho más fácil de aplicación de hello toopublish en RemoteApp. En caso contrario, tiene ruta de instalación de hello tooprovide de aplicación hello cuando se publica la aplicación hello.)
> 
> 

1. Realice cualquier configuración adicional de Windows que requieran sus aplicaciones.
2. Deshabilitar el sistema de archivos cifrados (EFS) de Hola. Ejecute el siguiente comando en una ventana de comandos con privilegios elevados de hello:
   
     Fsutil behavior set disableencryption 1
   
   Como alternativa, puede establecer o agregar Hola siguiente valor DWORD en el registro de hello:
   
     HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableEncryption = 1
3. Si va a crear la imagen dentro de una máquina virtual de Azure, cambie el nombre hello  **\%windir%\Panther\Unattend.xml** de archivos, como Esto bloqueará el script de carga de hello usar más adelante desde el trabajo. Cambiar nombre de Hola de este archivo tooUnattend.old por lo que seguirá disponiendo de archivo hello por si tuviera toorevert la implementación.
4. Vaya tooWindows Update e instale todas las actualizaciones importantes. Puede que tenga Windows Update varias veces tooget toorun todas las actualizaciones. (A veces se instala una actualización, y esa misma actualización requiere una actualización).
5. Imagen de Hola SYSPREP. En un símbolo del sistema con privilegios elevados, ejecute el siguiente comando de Hola:
   
   **C:\Windows\System32\sysprep\sysprep.exe /generalize /oobe /shutdown**
   
   **Nota:** no utilice hello **/mode: VM** conmutador de hello SYSPREP comando incluso si se trata de una máquina virtual.

## <a name="next-steps"></a>Pasos siguientes
Ahora que tiene la imagen de plantilla personalizada, debe tooupload que tooyour imagen colección RemoteApp. Utilice información de Hola Hola siguiendo artículos toocreate la colección:

* [¿Cómo toocreate una colección híbrida de RemoteApp](remoteapp-create-hybrid-deployment.md)
* [¿Cómo toocreate una colección en la nube de RemoteApp](remoteapp-create-cloud-deployment.md)

