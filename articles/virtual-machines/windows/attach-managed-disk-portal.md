---
title: aaaAttach un tooa de disco de datos administrados VM de Windows - Azure | Documentos de Microsoft
description: "El modo tooattach nueva administra datos disco tooa VM de Windows en hello Azure portal mediante Hola modelo de implementación del Administrador de recursos."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>¿Cómo tooattach un datos administrados disco tooa VM de Windows en hello portal de Azure

Este artículo muestra cómo tooattach una nueva datos administrada disco máquinas virtuales de tooWindows a través de hello portal de Azure. Antes de hacerlo, revise estas sugerencias:

* tamaño de Hola de máquina virtual de hello controla cuántos discos de datos que puede conectar. Para obtener más información, consulte [Tamaños de máquinas virtuales](sizes.md).
* Para un disco nuevo, no es necesario toocreate lo primer porque Azure lo crea al adjuntarla.

También puede [conectar un disco de datos mediante Powershell](attach-disk-ps.md).



## <a name="add-a-data-disk"></a>Agregar un disco de datos
1. En el menú de Hola Hola izquierda, haga clic en **máquinas virtuales**.
2. Seleccione la máquina virtual de Hola de lista de Hola.
3. En la hoja de la máquina virtual de hello, haga clic en **discos**.
   4. En hello **discos** hoja, haga clic en **+ Agregar disco de datos**.
5. En la lista desplegable para nuevo disco de Hola Hola, seleccione **crear vacío**.
6. Hola **disco administrado crear** hoja, escriba un nombre para el disco de Hola y ajuste Hola otras opciones según sea necesario. Cuando haya terminado, haga clic en **Crear**.
7. Hola **discos** hoja, haga clic en Guardar toosave Hola nueva configuración de disco para hello máquina virtual.
6. Después de Azure crea el disco de Hola y lo adjunta toohello virtual machine, nuevo disco de hello aparece en la configuración de disco de la máquina virtual hello en **discos de datos**.


## <a name="initialize-a-new-data-disk"></a>Inicio de un nuevo disco de datos

1. Conectar toohello máquina virtual.
1. Haga clic en el menú de inicio de hello dentro de hello VM y tipo **diskmgmt.msc** y posicionamiento **ENTRAR**. Esto iniciará el complemento Administración de discos Hola.
2. Administración de discos reconocerá que tenga un disco nuevo, no inicializado y se abrirá la ventana de hello inicializar disco.
3. Asegúrese de que se ha seleccionado Hola nuevo disco y haga clic en **Aceptar** tooinitialize lo.
4. nuevo disco de Hello aparecerá ahora como **sin asignar**. Haga doble clic en cualquier lugar en el disco de Hola y seleccione **nuevo volumen simple**. Hola **Asistente nuevo volumen Simple** se iniciará.
5. Vaya a través del Asistente de hello, mantener todos los valores predeterminados de hello, cuando haya terminado de seleccionar **finalizar**.
6. Cierre Administración de discos.
7. Aparecerá una ventana emergente que necesita nuevo disco de tooformat Hola antes de utilizarla. Haga clic en **Dar formato al disco**.
8. Hola **dar formato al nuevo disco** cuadro de diálogo, configuración de comprobación de hello y, a continuación, haga clic en **iniciar**.
9. Recibirá una advertencia que dar formato a discos de Hola se eliminarán todos los datos de hello, haga clic en **Aceptar**.
10. Una vez completado el formato de hello, haga clic en **Aceptar**.

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
