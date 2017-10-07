---
title: aaaHow toomanage almacenamiento de archivos de Azure de hello portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de almacenamiento de archivos de Azure de toouse hello toomanage de portal de Azure."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 385b99ac1c3d97ca79059ae8229afb53f1e825cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a>¿Cómo toouse almacenamiento de archivos de Azure de Hola Portal de Azure
Hola [portal de Azure](https://portal.azure.com) proporciona una interfaz de usuario para administrar el almacenamiento de archivos de Azure. Puede realizar Hola siguientes acciones desde el explorador web:

* Creación de un recurso compartido de archivos
* Cargar y descargar archivos tooand desde el recurso compartido de archivos.
* Supervisar el uso real de hello cada recurso compartido de archivos.
* Ajuste la cuota de tamaño del recurso compartido de archivos de Hola.
* Copie Hola montaje comandos toouse toomount compartir el archivo desde un cliente de Windows o Linux.

## <a name="create-file-share"></a>Creación de un recurso compartido de archivos
1. Inicie sesión en toohello portal de Azure.
2. En el menú de navegación de hello, haga clic en **cuentas de almacenamiento** o **cuentas de almacenamiento (clásica)**.
    
    ![Captura de pantalla que muestra cómo compartir archivos toocreate en el portal de Hola](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. Elija la cuenta de almacenamiento.

    ![Captura de pantalla que muestra cómo compartir archivos toocreate en el portal de Hola](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. Elija el servicio "Archivos".

    ![Captura de pantalla que muestra cómo compartir archivos toocreate en el portal de Hola](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. Haga clic en "Recursos compartidos de archivos" y siga Hola vínculo toocreate compartir el primer archivo.

    ![Captura de pantalla que muestra cómo compartir archivos toocreate en el portal de Hola](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. Rellene los nombre de recurso compartido de archivos de Hola y el tamaño de Hola de toocreate de recurso compartido (arriba too5120 GB) del archivo de hello su primer recurso compartido de archivos. Una vez que se ha creado el recurso compartido de archivos de hello, se puede montar desde cualquier sistema de archivos compatible con SMB 2.1 o SMB 3.0. Puede hacer clic en **cuota** Hola archivo recurso compartido toochange Hola tamaño de archivo hello too5120 GB. Consulte demasiado[Calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator/) costo de almacenamiento de información de hello tooestimate del uso de almacenamiento de archivos de Azure.

    ![Captura de pantalla que muestra cómo compartir archivos toocreate en el portal de Hola](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a>Carga y descarga de archivos
1. Elija un recurso compartido de archivos creado previamente.

    ![Captura de pantalla que muestra cómo tooupload y descarga los archivos de Hola portal](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. Haga clic en **cargar** para abrir la interfaz de usuario de Hola para cargar los archivos.

    ![Captura de pantalla que muestra cómo se tooupload los archivos desde el portal de Hola](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a>Conectar el recurso compartido de toofile
-  Haga clic en **conectar** para obtener la línea de comandos de Hola para el recurso compartido de archivos de montaje Hola de Windows y Linux. Para los usuarios de Linux, también puede hacer referencia demasiado[cómo toouse almacenamiento de archivos de Azure con Linux](storage-how-to-use-files-linux.md) para obtener más instrucciones de montaje para otras distribuciones de Linux.

    ![Captura de pantalla que muestra cómo toomount Hola recurso compartido de archivos](media/storage-file-how-to-use-files-portal/use-files-portal-connect.png)
-  Puede copiar Hola comandos para montar el archivo de recurso compartido en Windows o Linux y ejecución desde la máquina local o de máquina virtual de Azure.

    ![Captura de pantalla que muestra comandos de montaje de Hola para Windows y Linux](media/storage-file-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

**Sugerencia:**  
clave de acceso de cuenta de almacenamiento de toofind hello para el montaje, haga clic en **teclas de acceso de vista para esta cuenta de almacenamiento** final Hola de hello página Conectar.

## <a name="see-also"></a>Otras referencias
Consulte los vínculos siguientes para obtener más información acerca de Almacenamiento de archivos de Azure.

* [Preguntas más frecuentes](storage-files-faq.md)
* [Solución de problemas](storage-troubleshoot-file-connection-problems.md)