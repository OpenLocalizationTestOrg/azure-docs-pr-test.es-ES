---
title: aaaCapture una imagen de una VM de Windows Azure | Documentos de Microsoft
description: "Capturar una imagen de una máquina virtual de Windows Azure creada con el modelo de implementación clásica de Hola."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: b9bbc437012aa44295f90941c9d72e39509df28f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Capturar una imagen de una máquina virtual de Windows Azure creada con el modelo de implementación clásica de Hola.
> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Para obtener información del modelo de Resource Manager, vea [Capturar una imagen administrada de una máquina virtual generalizada en Azure](../capture-image-resource.md).

Este artículo muestra cómo toocapture una máquina virtual de Azure Windows por lo que puede usar como una imagen toocreate otras máquinas virtuales en ejecución. Esta imagen de disco del sistema operativo hello y los discos de datos que están acoplados toohello virtual machine. No incluye las configuraciones de redes, por lo que necesitará tooset configuraciones de red al crear otras máquinas virtuales que usan la imagen de Hola Hola.

Almacenes de Azure Hola imagen en **imágenes de máquina virtual (clásica)**, **proceso** Hola de servicio que se muestra al ver todos los servicios de Azure. Se trata de hello mismo lugar donde se almacenan las imágenes que ha cargado. Para obtener más información acerca de las imágenes, vea [Acerca de las imágenes para las máquinas virtuales](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).

## <a name="before-you-begin"></a>Antes de empezar
Estos pasos se supone que ya ha creado una máquina virtual de Azure y configuró el sistema operativo de hello, incluida la conexión de los discos de datos. Si aún no lo ha hecho todavía, vea Hola siguientes artículos para obtener información sobre cómo crear y preparar la máquina virtual de hello:

* [Cree una máquina virtual desde una imagen](createportal.md)
* [Cómo tooattach datos disco de máquina virtual de tooa](attach-disk.md)
* Asegúrese de que los roles de servidor hello son compatibles con Sysprep. Para más información, consulte [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)(Compatibilidad de Sysprep con roles de servidor).

> [!WARNING]
> Este proceso elimina la máquina virtual original Hola después de capturarla.
>
>

Toocapturing anterior una imagen de máquina virtual de Azure, se recomienda máquina virtual de destino de hello realizar copias de seguridad. Esto se puede hacer mediante Copia de seguridad de Azure. Para obtener más información, consulte [Copia de seguridad de máquinas virtuales de Azure](../../../backup/backup-azure-vms.md). Hay otras soluciones disponibles de socios certificados. toofind cuál es actualmente disponible, busque hello Azure Marketplace.

## <a name="capture-hello-virtual-machine"></a>Captura de máquina virtual de Hola
1. Hola [portal de Azure](http://portal.azure.com), **conectar** toohello virtual machine. Para obtener instrucciones, consulte [cómo toosign en la máquina virtual de tooa ejecuta Windows Server][How toosign in tooa virtual machine running Windows Server].
2. Abra una ventana de símbolo del sistema como administrador.
3. Cambie el directorio de hello demasiado`%windir%\system32\sysprep`, y, a continuación, ejecute sysprep.exe.
4. Hola **herramienta de preparación del sistema** aparece el cuadro de diálogo. Hola siguientes:

   * En **Acción de limpieza del sistema**, seleccione **Iniciar la configuración rápida (OOBE) del sistema**  y asegúrese de que la opción **Generalizar** está marcada. Para obtener más información acerca del uso de Sysprep, consulte [cómo tooUse Sysprep: Introducción][How tooUse Sysprep: An Introduction].
   * En **Opciones de apagado**, seleccione **Apagar**.
   * Haga clic en **Aceptar**.

   ![Ejecute Sysprep](./media/capture-image/SysprepGeneral.png)
5. Sysprep se cierra máquina virtual de hello, que cambia el estado de Hola de máquina virtual de Hola Hola portal de Azure demasiado**detenido**.
6. Hola portal de Azure, haga clic en **máquinas virtuales (clásicas)** y seleccione Hola máquina virtual que desee toocapture. Hola **imágenes de máquina virtual (clásica)** grupo aparece en **proceso** al ver **más servicios**.

7. En la barra de comandos de hello, haga clic en **capturar**.

   ![Capture la máquina virtual](./media/capture-image/CaptureVM.png)

   Hola **Hola de captura de máquina Virtual** aparece el cuadro de diálogo.

8. En **nombre de la imagen**, escriba un nombre para la nueva imagen de Hola. En **etiqueta de imagen**, escriba una etiqueta para la nueva imagen de Hola.

9. Haga clic en **ejecuté Sysprep en la máquina virtual de hello**. Esta casilla de verificación refiere a las acciones de toohello con Sysprep en los pasos 3 a 5. Una imagen _debe_ generalizarse mediante la ejecución de Sysprep antes de agregar un servidor de Windows conjunto tooyour de imagen de imágenes personalizadas.

10. Una vez completada la captura de hello, nueva imagen de hello esté disponible en hello **Marketplace**, Hola **proceso**, **imágenes de máquina virtual (clásica)** contenedor.

    ![Captura correcta de la imagen](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>Pasos siguientes
imagen de Hello es máquinas virtuales de listo toobe utiliza toocreate. toodo, creará una máquina virtual seleccionando hello **más servicios** elemento de menú en la parte inferior de hello del menú de servicios para hello, a continuación, **imágenes de máquina virtual (clásica)** en hello **proceso**grupo. Para obtener instrucciones, consulte [Creación de una máquina virtual desde una imagen](createportal.md).

[How toosign in tooa virtual machine running Windows Server]:connect-logon.md
[How tooUse Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[hello virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of hello virtual machine]: ./media/capture-image/CaptureVM.png
[Enter hello image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use hello captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
