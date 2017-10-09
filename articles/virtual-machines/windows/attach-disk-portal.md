---
title: aaaAttach un tooa de disco de datos no administrados VM de Windows - Azure | Documentos de Microsoft
description: "¿Cómo tooattach nuevo o existente de los datos no administrados disco tooa VM de Windows en hello Azure portal mediante Hola modelo de implementación del Administrador de recursos."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>¿Cómo tooattach un datos no administrados disco tooa VM de Windows en hello portal de Azure

Este artículo muestra cómo tooattach nueva y existente sin administrar discos máquinas virtuales de tooWindows a través de hello portal de Azure. También puede [conectar un disco de datos mediante PowerShell](./attach-disk-ps.md). Antes de hacerlo, revise estas sugerencias:

* tamaño de Hola de máquina virtual de hello controla cuántos discos de datos que puede conectar. Para obtener más información, consulte [Tamaños de máquinas virtuales](sizes.md).
* toouse almacenamiento Premium, necesita una máquina virtual DS-series o GS-series. Puede utilizar discos de cuentas de almacenamiento premium y estándar con estas máquinas virtuales. Almacenamiento premium está disponible en determinadas regiones. Para obtener más información, consulte [Almacenamiento Premium: Almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* Para un disco nuevo, no es necesario toocreate lo primer porque Azure lo crea al adjuntarla.


También puede [conectar un disco de datos mediante Powershell](attach-disk-ps.md).


## <a name="find-hello-virtual-machine"></a>Encontró la máquina virtual de Hola
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú de Hola Hola izquierda, haga clic en **máquinas virtuales**.
3. Seleccione la máquina virtual de Hola de lista de Hola.
4. En la hoja de máquinas virtuales de hello, haga clic en **discos**.
   
Continúe siguiendo las instrucciones para conectar un [nuevo disco](#option-1-attach-a-new-disk) o un [disco existente](#option-2-attach-an-existing-disk).

## <a name="option-1-attach-and-initialize-a-new-disk"></a>Opción 1: adjunte e inicialice un disco nuevo
1. En hello **discos** hoja, haga clic en **+ Agregar disco de datos**.
2. Hola **conectar disco administrado** hoja, escriba un nombre para el disco de hello en **nombre** y, a continuación, seleccione **New (disco vacío)** en **como tipo de origen**.
3. En **contenedor de almacenamiento**, haga clic en hello **examinar** botón y busque la cuenta de almacenamiento de toohello y contenedor donde como Hola nuevo disco duro virtual toobe almacenado y, a continuación, haga clic en **seleccione**. 
  
   ![Revisar configuración de disco](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. Cuando haya terminado con la configuración de Hola Hola disco de datos, haga clic en **Aceptar**.
4. Nuevo en hello **discos** hoja, haga clic en **guardar** configuración de máquina virtual de tooadd Hola disco toohello.


### <a name="initialize-a-new-data-disk"></a>Inicio de un nuevo disco de datos

1. Conectar la máquina virtual de toohello. Para obtener instrucciones, consulte [cómo tooconnect y tooan virtual de Azure de inicio de sesión automático con Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
1. Haga clic en hello **iniciar** menú dentro de hello VM y escriba **diskmgmt.msc** y posicionamiento **ENTRAR**. Esto inicia el complemento Administración de discos Hola.
2. Administración de discos reconoce que tiene un disco nuevo sin inicializar y se abrirá la ventana de hello inicializar disco.
3. Asegúrese de que se ha seleccionado Hola nuevo disco y haga clic en **Aceptar** tooinitialize lo.
4. Hello nuevo disco aparece ahora como **sin asignar**. Haga doble clic en cualquier lugar en el disco de Hola y seleccione **nuevo volumen simple**. Hola **Asistente nuevo volumen Simple** inicia.
5. Vaya a través del Asistente de hello, mantener todos los valores predeterminados de hello, cuando haya terminado de seleccionar **finalizar**.
6. Cierre Administración de discos.
7. Obtiene un elemento emergente que necesita nuevo disco de tooformat Hola antes de utilizarla. Haga clic en **Dar formato al disco**.
8. Hola **dar formato al nuevo disco** cuadro de diálogo, configuración de comprobación de hello y, a continuación, haga clic en **iniciar**.
9. Recibe una advertencia que dar formato a discos de hello borra todos los datos de hello, haga clic en **Aceptar**.
10. Una vez completado el formato de hello, haga clic en **Aceptar**.


## <a name="option-2-attach-an-existing-disk"></a>Opción 2: Conectar un disco existente
1. En hello **discos** hoja, haga clic en **+ Agregar disco de datos**.
2. En hello **conectar disco no administrado** hoja, en **tipo de origen de** seleccione **blob existente**.

    ![Revisar configuración de disco](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. Haga clic en **examinar** toonavigate toohello cuenta de almacenamiento y contenedor donde hello disco duro virtual existente se encuentra. Haga clic en y Hola VHD y, a continuación, haga clic en **seleccione**.
4. Haga clic en **Aceptar** en hello **conectar disco no administrado** hoja.
5. Hola **discos** hoja, haga clic en **guardar** tooadd hello toohello configuración de hello máquina virtual.
   


## <a name="use-trim-with-standard-storage"></a>Uso de TRIM con el almacenamiento estándar

Si utiliza almacenamiento estándar (HDD), debe habilitar TRIM. TRIM descarta los bloques sin utilizar en el disco de Hola, por lo que solo se le facturará de almacenamiento que utiliza realmente. Esto puede suponerle un ahorro si crea archivos grandes y, luego, los elimina. 

Puede ejecutar esta opción de RECORTE de comando toocheck Hola. Abra un símbolo del sistema en su máquina virtual de Windows y escriba:

```
fsutil behavior query DisableDeleteNotify
```

Si el comando de hello devuelve 0, RECORTE está habilitada correctamente. Si devuelve 1, ejecute hello después tooenable comando RECORTE:
```
fsutil behavior set DisableDeleteNotify 0
```

Después de eliminar los datos desde el disco, puede asegurarse de operaciones de RECORTE de hello vaciadas correctamente mediante la ejecución de desfragmentación con RECORTE:

```
defrag.exe <volume:> -l
```

También puede asegurarse de todo el volumen de Hola se recorta por formatear volumen Hola.


## <a name="next-steps"></a>Pasos siguientes
Si la aplicación necesita que los datos de toouse Hola D: unidad toostore, puede [cambiar Hola la letra de unidad de disco temporal de Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

