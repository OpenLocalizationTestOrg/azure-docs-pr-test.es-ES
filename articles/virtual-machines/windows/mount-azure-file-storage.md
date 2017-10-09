---
title: aaaMount almacenamiento de archivos de Azure desde una VM de Windows Azure | Documentos de Microsoft
description: "Almacene el archivo en la nube de hello con almacenamiento de archivos de Azure y montar el recurso compartido de archivos de nube desde una máquina virtual (VM) de Azure."
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a>Uso de recursos compartidos de archivos de Azure con máquinas virtuales de Windows 

Puede usar recursos compartidos de archivos de Azure como los archivos de toostore y acceso de una forma de la máquina virtual. Por ejemplo, puede almacenar una secuencia de comandos o un archivo de configuración de aplicación que desea que su tooshare de máquinas virtuales. En este tema, le mostramos cómo toocreate y montaje un Azure recurso compartido de archivos y cómo tooupload y descarga los archivos.

## <a name="connect-tooa-file-share-from-a-vm"></a>Conectar el recurso compartido de archivos de tooa de una máquina virtual

En esta sección se da por supuesto que ya tiene un archivo de recurso compartido que desee tooconnect a. Si necesita toocreate uno, consulte [crear un recurso compartido de archivos](#create-a-file-share) más adelante en este tema.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú de la izquierda hello, haga clic en **cuentas de almacenamiento**.
3. Elija la cuenta de almacenamiento.
4. Hola **Introducción** página, en **servicios**, seleccione **archivos**.
5. Seleccione un recurso compartido de archivos.
6. Haga clic en **conectar** tooopen una página que muestra la sintaxis de línea de comandos de hello para el montaje Hola el recurso compartido de archivos de Windows o Linux.
7. Resalte Hola sintaxis de comando de Hola y péguelo en el Bloc de notas o en otro lugar donde se puede acceder fácilmente a ella. 
8. Editar líder en hello sintaxis tooremove Hola ** > ** y reemplace *[letra de unidad]* con una letra de unidad de hello (por ejemplo, **Y:**) que desee que el recurso compartido de archivos de toomount Hola.
8. Conéctese tooyour VM y abra un símbolo del sistema.
9. Pegar en hello editado la sintaxis de la conexión y presione **ENTRAR**.
10. Cuando se ha creado la conexión de hello, obtendrá un mensaje de bienvenida de **Hola comando se completó correctamente.**
11. Compruebe la conexión de hello escribiendo en hello letra tooswitch toothat la unidad y, a continuación, escriba **dir** toosee contenido de Hola Hola recurso compartido de archivos.



## <a name="create-a-file-share"></a>Creación de un recurso compartido de archivos 
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú de la izquierda hello, haga clic en **cuentas de almacenamiento**.
3. Elija la cuenta de almacenamiento.
4. Hola **Introducción** página, en **servicios**, seleccione **archivos**.
5. En la página de servicio de archivos de hello, haga clic en **+ recurso compartido de archivos** toocreate compartir el primer archivo. \
6. Rellene el nombre de recurso compartido de archivo Hola. Pueden usarse minúsculas, números y guiones individuales en los nombres de recurso compartido de archivos. Hola nombre no puede empezar con un guión y no se puede usar varios guiones consecutivos. 
7. Puede estar relleno en un límite de tamaño archivo hello, too5120 GB.
8. Haga clic en **Aceptar** recurso compartido de archivos de toodeploy Hola.
   
## <a name="upload-files"></a>Carga de archivos
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú de la izquierda hello, haga clic en **cuentas de almacenamiento**.
3. Elija la cuenta de almacenamiento.
4. Hola **Introducción** página, en **servicios**, seleccione **archivos**.
5. Seleccione un recurso compartido de archivos.
6. Haga clic en **cargar** tooopen hello **cargar archivos** página.
7. Haga clic en toobrowse de icono de carpeta de hello su sistema de archivos local para un tooupload de archivo.   
8. Haga clic en **cargar** recurso compartido de archivos de tooupload Hola archivo toohello.

## <a name="download-files"></a>Descarga de archivos
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú de la izquierda hello, haga clic en **cuentas de almacenamiento**.
3. Elija la cuenta de almacenamiento.
4. Hola **Introducción** página, en **servicios**, seleccione **archivos**.
5. Seleccione un recurso compartido de archivos.
6. Haga doble clic en el archivo hello y elija **descargar** toodownload se tooyour de equipo local.
   

## <a name="next-steps"></a>Pasos siguientes

También puede crear y administrar recursos compartidos de archivos con PowerShell. Para más información, vea [Introducción a Azure File Storage en Windows](../../storage/files/storage-dotnet-how-to-use-files.md).
