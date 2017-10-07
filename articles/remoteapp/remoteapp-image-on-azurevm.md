---
title: "aaaCreate una imagen de Azure RemoteApp se basa en una máquina virtual de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una imagen de Azure RemoteApp a partir de una máquina virtual de Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a>Creación de una imagen de Azure RemoteApp basada en una máquina virtual de Azure
> [!IMPORTANT]
> Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017. Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.
> 
> 

Puede crear imágenes de Azure RemoteApp (que contienen aplicaciones de Hola que comparte en la colección) de una máquina virtual de Azure. También puede elegir toouse una imagen de máquina virtual que agregamos la Galería de imágenes de máquina virtual de Azure toohello que cumple todos los requisitos de imagen de Azure RemoteApp hello: puede usar esa imagen de máquina virtual como un punto de partida para su propia máquina virtual, si desea. Busque imágenes de "Windows Server escritorio remoto" hello en la biblioteca de Hola.

Hay dos toocreate pasos según su propia imagen en una máquina virtual de Azure: crear imagen de hello y, a continuación, cargarlo desde hello Azure VM biblioteca tooAzure RemoteApp.

## <a name="create-a-custom-image-based-on-an-azure-vm"></a>Creación de una imagen personalizada basada en una máquina virtual de Azure
Use estos toocreate pasos una imagen basada en una máquina virtual de Azure.

1. Cree una máquina virtual de Azure. Puede usar Hola "Host a sesión remota de escritorio de Windows Server" o "Windows Server remoto escritorio sesión Host con Microsoft Office 365 ProPlus" imagen de Hola desde galería de imágenes de máquina virtual de Azure Hola. Esta imagen cumple todos los requisitos de imagen de plantilla de RemoteApp de Azure de Hola.
   
    Para obtener información detallada, vea [Creación de una máquina virtual que ejecuta Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. Conectar toohello máquina virtual e instalar y configurar aplicaciones de Hola que desea que tooshare a través de RemoteApp. Asegúrese de tooperform seguro de las configuraciones de Windows adicionales requeridas por las aplicaciones.
   
    Para obtener más información, consulte [cómo tooLog en tooa Máquina Virtual que ejecuta Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Si está utilizando uno de imágenes de Host de sesión de escritorio remoto de Windows Server de hello, hay una secuencia de comandos de validación incluye que asegure que la máquina virtual cumple Hola RemoteApp pre-reqs. secuencia de comandos de toorun, haga doble clic en **ValidateRemoteAppImage** en el escritorio de Hola. Asegúrese de que todos los errores notificados por el script de Hola se corrigen antes del paso siguiente de toohello de continuar.
4. SYSPREP /generalize y capturar imagen de Hola. Vea [cómo tooCapture una tooUse de máquina Virtual de Windows como una plantilla de](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) para obtener instrucciones.

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a>Importar imagen hello en la biblioteca de imágenes de hello Azure RemoteApp
Use estos nueva imagen de pasos tooimport hello en Azure RemoteApp:

1. Hola **imágenes de plantilla** ficha:
   
   * Si no dispone de imágenes existentes, haga clic en **Carga o importación de una imagen de plantilla**.
   * Si ya tiene al menos una imagen, haga clic en  **+**  tooadd una nueva imagen.
2. Seleccione **Importar una imagen de la biblioteca de máquinas virtuales** y haga clic en **Siguiente**.
3. En la página siguiente de hello, seleccione la imagen personalizada de lista de Hola y compruebe que ha seguido los pasos de hello aparece cuando se creó la imagen. Haga clic en **Siguiente**.
4. Escriba un nombre para la nueva imagen de RemoteApp hello y Seleccionar ubicación de Hola y luego haga clic en el proceso de importación de hello marca de verificación toostart Hola.

> [!NOTE]
> Puede importar imágenes desde cualquier ubicación de Azure compatible con máquinas virtuales de Azure tooany ubicación de Azure compatible con Azure RemoteApp. Función ubicaciones Hola importación Hola puede durar too25 minutos.
> 
> 

Ahora está listo toocreate la nueva colección, ya sea un [nube](remoteapp-create-cloud-deployment.md) colección o [híbrida](remoteapp-create-hybrid-deployment.md), en función de sus necesidades.

