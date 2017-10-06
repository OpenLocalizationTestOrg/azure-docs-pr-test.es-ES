---
title: aaaUpload VHD archivo laboratorios de desarrollo y pruebas de tooAzure mediante el Explorador de almacenamiento de Microsoft Azure | Documentos de Microsoft
description: Cargar la cuenta de almacenamiento del toolab del archivo de disco duro virtual mediante el Explorador de almacenamiento de Microsoft Azure
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a>Cargar la cuenta de almacenamiento del toolab del archivo de disco duro virtual mediante el Explorador de almacenamiento de Microsoft Azure

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

En los laboratorios de desarrollo y pruebas de Azure, archivos de disco duro virtual pueden ser toocreate usa imágenes personalizadas, que son máquinas virtuales de tooprovision usado. Este artículo se explica cómo toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) cuenta de almacenamiento del laboratorio de tooa de archivos tooupload un disco duro virtual. Una vez que haya cargado el archivo VHD, Hola [pasos siguientes sección](#next-steps) enumera algunos artículos que ilustran cómo toocreate una imagen personalizada de hello carga archivo de disco duro virtual. Para más información sobre discos y discos duros virtuales en Azure, consulte [Acerca de los discos y los discos duros virtuales para máquinas virtuales](../virtual-machines/linux/about-disks-and-vhds.md).

## <a name="step-by-step-instructions"></a>Instrucciones paso a paso

Hola después de recorrido de pasos a través de la carga de un disco duro virtual archivo laboratorios tooDevTest con [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).

1. [Descargue e instale la versión más reciente de Hola de hello Microsoft Azure Storage Explorer](http://www.storageexplorer.com).

1. Obtener nombre de Hola de cuenta de almacenamiento del laboratorio de hello mediante Hola portal de Azure:

    1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
    
    1. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.
    
    1. En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.  
    
    1. En la hoja del laboratorio de hello, seleccione **configuración**. 
    
    1. En el laboratorio de hello **configuración** hoja, seleccione **imágenes personalizadas (VHD)**.
    
    1. En hello **imágenes personalizadas** hoja, seleccione **+ agregar**. 
    
    1. En hello **imagen personalizada** hoja, seleccione **VHD**.
    
    1. En hello **VHD** hoja, seleccione **cargar un VHD con PowerShell**.
    
        ![Carga del VHD mediante PowerShell][0]
    
    1. Hola **cargar una imagen con PowerShell** hoja muestra una llamada toohello **Add-AzureVhd** cmdlet. Hola primer parámetro (*destino*) contiene el nombre de cuenta de almacenamiento de Hola para laboratorio Hola Hola siguiendo el formato:
    
        https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/... 

    1. Tome nota del nombre de cuenta de almacenamiento de hello tal como se utiliza en pasos posteriores.
    
1. Conectar tooan cuenta de suscripción de Azure mediante el Explorador de almacenamiento.

    > [!TIP] 
    > 
    > El Explorador de Storage admite varias opciones de conexión. Esta sección muestra la cuenta de almacenamiento tooa conexión asociada a su suscripción de Azure. toosee Hola otras opciones de conexión admitidos por el Explorador de almacenamiento, consulte el artículo toohello, [introducción con el Explorador de almacenamiento](../vs-azure-tools-storage-manage-with-storage-explorer.md).
 
    1. Abra el Explorador de Storage.
    
    1. En el Explorador de Storage, seleccione **Azure Account settings** (Configuración de la cuenta de Azure). 
    
        ![Configuración de la cuenta de Azure][1]
    
    1. panel izquierdo de Hello muestra las cuentas de Microsoft de Hola que ha iniciado la sesión. cuenta de tooconnect tooanother, seleccione **agregar una cuenta**y siga hello toosign de cuadros de diálogo con una cuenta de Microsoft que está asociada con al menos una suscripción activa de Azure.
    
        ![Agregar una cuenta][2]
    
    1. Una vez que inicie sesión correctamente con una cuenta de Microsoft, panel izquierdo de hello rellena con hello Azure suscripciones asociadas a esa cuenta. Seleccione Hola suscripciones de Azure con el que desea toowork y, a continuación, seleccione **aplicar**. (Seleccione **todas las suscripciones** alterna Hola selección de todo o enumera ningún hello las suscripciones de Azure.)
    
        ![Selección de suscripciones de Azure][3]
    
    1. panel izquierdo de Hello muestra las cuentas de almacenamiento de hello asociadas con suscripciones de Azure Hola seleccionado.
    
        ![Suscripciones de Azure seleccionadas][4]

1. Busque la cuenta de almacenamiento del laboratorio de hello:

    1. En el panel izquierdo del explorador de almacenamiento de hello, busque y expanda el nodo de Hola para suscripción de Azure que posee el laboratorio de Hola Hola.
    
    1. En el nodo de la suscripción de hello, expanda **cuentas de almacenamiento**.

    1. Expandir los nodos del laboratorio de hello almacenamiento cuenta nodo tooreveal para **contenedores de blobs**, **recursos compartidos de archivos**, **colas**, y **tablas**.
    
    1. Expanda hello **contenedores de blobs** nodo.
    
    1. Seleccionar toodisplay del contenedor de blob de hello cargas de su contenido en el panel derecho de Hola.
        
        ![Directorio de carga][5]

1. Cargar archivo de disco duro virtual de hello mediante el Explorador de almacenamiento:

    1. En el panel derecho del explorador de almacenamiento de hello, verá una lista de blobs de Hola Hola **carga** contenedor de blob de cuenta de almacenamiento del laboratorio de Hola. En la barra de herramientas de editor de blob de hello, seleccione **cargar** 
        
        ![Botón Cargar][6]
    
    1. De hello **cargar** menú desplegable, seleccione **cargar archivos...** .
    
    1. En hello **cargar archivos** cuadro de diálogo, los puntos suspensivos Hola select.
        
        ![Selección del archivo][8]  

    1. En hello **tooupload Seleccione archivos** cuadro de diálogo Examinar toohello deseado archivo VHD, selecciónelo y, a continuación, seleccione **abiertos**.
    
    1. Cuando se devuelve toohello **cargar archivos** cuadro de diálogo, cambio **tipo de Blob** demasiado**Blob en páginas**.
    
    1. Seleccione **Cargar**.

        ![Selección del archivo][9]  
    
    1. Hola Explorador de almacenamiento **registro de actividad** panel muestra el estado de la descarga de hello (junto con vínculos toocancel Hola carga). proceso de Hola de cargar un archivo de disco duro virtual puede ser larga según el tamaño de hello del archivo de disco duro virtual de hello y la velocidad de conexión. 

        ![Estado del archivo de carga][10]  

## <a name="next-steps"></a>Pasos siguientes

- [Crear una imagen personalizada en los laboratorios de desarrollo y pruebas de Azure desde un archivo de disco duro virtual mediante Hola portal de Azure](devtest-lab-create-template.md)
- [Creación de una imagen personalizada en Azure DevTest Labs a partir de un archivo VHD mediante PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
