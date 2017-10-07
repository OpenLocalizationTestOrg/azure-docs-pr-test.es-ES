---
title: aaaTroubleshoot errores al eliminar las cuentas de almacenamiento de Azure, los contenedores o los discos duros virtuales | Documentos de Microsoft
description: "Solución de los errores que aparecen al eliminar cuentas de almacenamiento, contenedores o VHD de Azure"
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 77361593e2c924d39aba853e0807dc3188f50e60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a>Solución de los errores que aparecen al eliminar cuentas de almacenamiento, contenedores o VHD de Azure

Podría recibir errores cuando intente toodelete una cuenta de almacenamiento de Azure, el contenedor o el disco duro virtual (VHD) en hello [portal de Azure](https://portal.azure.com). Este artículo proporciona una solución de problemas de orientación toohelp resolución hello en una implementación de Azure Resource Manager.

Si este artículo no resuelve el problema de Azure, visite Hola foros de Azure en [MSDN y el desbordamiento de la pila](https://azure.microsoft.com/support/forums/). Puede publicar su problema en estos foros o too@AzureSupport en Twitter. Además, puede registrar una solicitud de soporte técnico de Azure seleccionando **obtener asistencia** en hello [soporte técnico de Azure](https://azure.microsoft.com/support/options/) sitio.

## <a name="symptoms"></a>Síntomas
### <a name="scenario-1"></a>Escenario 1.
Cuando intente toodelete un disco duro virtual en una cuenta de almacenamiento en una implementación de administrador de recursos, recibirá Hola mensaje de error siguiente:

**No se pudo blob toodelete 'vhds/BlobName.vhd'. Error: Hay una concesión de blob de Hola y se especificó ningún identificador de concesión en la solicitud de saludo.**

Este problema puede producirse debido a una máquina virtual (VM) tiene una concesión en hello VHD que se está intentando toodelete.

### <a name="scenario-2"></a>Escenario 2.
Cuando intente toodelete un contenedor en una cuenta de almacenamiento en una implementación de administrador de recursos, recibirá Hola mensaje de error siguiente:

**Error de contenedor de almacenamiento de toodelete 'VHD'. Error: Hay una concesión en el contenedor de Hola y se especificó ningún identificador de concesión en la solicitud de saludo.**

Este problema puede producirse como contenedor de hello tiene un disco duro virtual que está bloqueado en estado de concesión de Hola.

### <a name="scenario-3"></a>Escenario 3.
Cuando intente toodelete una cuenta de almacenamiento en una implementación de administrador de recursos, recibirá Hola mensaje de error siguiente:

**Error de cuenta de almacenamiento toodelete 'StorageAccountName'. Error: no se puede eliminar la cuenta de almacenamiento de hello debido artefactos tooits está en uso.**

Este problema puede producirse porque la cuenta de almacenamiento de hello contiene un disco duro virtual que se encuentra en estado de concesión de Hola.

## <a name="solution"></a>Solución 
tooresolve estos problemas, debe identificar el disco duro virtual que está provocando el error de Hola Hola y Hola asociados máquina virtual. A continuación, separar Hola VHD de hello VM (para los discos de datos) o eliminar Hola máquina virtual que está usando Hola VHD (en el caso de discos de sistema operativo). Esto quita concesión Hola Hola VHD y permite toobe eliminado. 

toodo, utilice uno de hello siguientes métodos:

### <a name="method-1---use-azure-storage-explorer"></a>Método 1: Usar el Explorador Azure Storage

### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>Hola de identificación de paso 1 disco duro virtual que impiden la eliminación de la cuenta de almacenamiento de Hola

1. Cuando se elimina la cuenta de almacenamiento de hello, aparecerá un cuadro de diálogo de mensaje como siguiente hello: 

    ![mensaje al eliminar la cuenta de almacenamiento de Hola](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Comprobar hello **dirección URL de disco** tooidentify cuenta de almacenamiento de Hola y Hola VHD que evita tener que eliminan la cuenta de almacenamiento de Hola. En el siguiente ejemplo de Hola Hola cadena antes de ". blob.core.windows.net" es el nombre de cuenta de almacenamiento de Hola y "SCCM2012-2015-08-28.vhd" es el nombre de disco duro virtual de Hola.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-hello-vhd-by-using-azure-storage-explorer"></a>Hola de eliminación del paso 2 VHD mediante el Explorador de almacenamiento de Azure

1. Descarga e instale Hola versión más reciente de [Azure Storage Explorer](http://storageexplorer.com/). Esta herramienta es una aplicación independiente de Microsoft que le permite trabajar de tooeasily con datos de almacenamiento de Azure en Windows, Mac OS y Linux.
2. Abra el Explorador de Azure Storage, seleccione ![icono de cuenta](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) en la barra de la izquierda hello, seleccione el entorno de Azure y, a continuación, inicie sesión en.

3. Seleccione todas las suscripciones o suscripción de Hola que contiene la cuenta de almacenamiento de hello que desea toodelete.

    ![agregar suscripción](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. Vaya toohello cuenta de almacenamiento que se obtiene de Hola disco dirección URL anterior, seleccione Hola **contenedores de blobs** > **discos duros virtuales** y busque Hola VHD que evita tener que eliminar la cuenta de almacenamiento de Hola.
5. Si se encuentra Hola VHD, compruebe hello **nombre de máquina virtual** hello de la columna toofind máquina virtual que está usando este disco duro virtual.

    ![Seleccionar máquina virtual](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. Quitar concesión Hola de hello VHD mediante el portal de Azure. Para obtener más información, consulte [Remove concesión Hola Hola VHD](#remove-the-lease-from-the-vhd). 

7. Paso toohello Azure Storage Explorer, haga clic en hello VHD y, a continuación, seleccione Eliminar.

8. Eliminar cuenta de almacenamiento de Hola.

### <a name="method-2---use-azure-portal"></a>Método 2: Usar Azure Portal 

#### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>Paso 1: Identificar el disco duro virtual que impiden la eliminación de la cuenta de almacenamiento de Hola Hola

1. Cuando se elimina la cuenta de almacenamiento de hello, aparecerá un cuadro de diálogo de mensaje como siguiente hello: 

    ![mensaje al eliminar la cuenta de almacenamiento de Hola](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Comprobar hello **dirección URL de disco** tooidentify cuenta de almacenamiento de Hola y Hola VHD que evita tener que eliminan la cuenta de almacenamiento de Hola. En el siguiente ejemplo de Hola Hola cadena antes de ". blob.core.windows.net" es el nombre de cuenta de almacenamiento de Hola y "SCCM2012-2015-08-28.vhd" es el nombre de disco duro virtual de Hola.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
3. En el menú del concentrador hello, seleccione **todos los recursos**. Vaya toohello cuenta de almacenamiento y, a continuación, seleccione **Blobs** > **discos duros virtuales**.

    ![Captura de pantalla de portal de hello, con la cuenta de almacenamiento de Hola y el contenedor de "VHD" hello resaltado](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. Busque Hola VHD que se obtiene de dirección URL de disco de hello anteriormente. A continuación, determinar qué máquina virtual está usando Hola VHD. Por lo general, puede determinar qué máquina virtual contiene Hola VHD mediante la comprobación de nombre de hello VHD:

Máquina virtual en el modelo de desarrollo mediante Resource Manager

   * Los discos de sistema operativo suelen seguir esta convención de nomenclatura: NombreVM-AAAA-MM-DD-HHMMSS.vhd
   * Los discos de sistema operativo suelen seguir esta convención de nomenclatura: NombreVM-AAAA-MM-DD-HHMMSS.vhd

Máquina virtual en modelo de desarrollo clásico

   * Los discos de sistema operativo suelen seguir esta convención de nomenclatura: NombreServicioEnLaNube-NombreVM-AAAA-MM-DD-HHMMSS.vhd
   * Los discos de datos suelen seguir esta convención de nomenclatura: NombreServicioEnLaNube-NombreVM-AAAA-MM-DD-HHMMSS.vhd

#### <a name="step-2-remove-hello-lease-from-hello-vhd"></a>Paso 2: Quitar la concesión de Hola de hello VHD

[Quitar la concesión de Hola de hello VHD](#remove-the-lease-from-the-vhd)y, a continuación, eliminar la cuenta de almacenamiento de Hola.

## <a name="what-is-a-lease"></a>¿Qué es una concesión?
Una concesión es un bloqueo que puede ser usado toocontrol acceso tooa blob (por ejemplo, un disco duro virtual). Cuando se concede un blob, sólo los propietarios de Hola de concesión de hello pueden tener acceso a los blobs de Hola. Una concesión es importante para hello siguientes motivos:

* Se evita que daños en los datos si varios propietarios intente toowrite toohello misma parte del blob de hello en hello mismo tiempo.
* Se evita que el blob de Hola se elimine si algo lo esté usando activamente (por ejemplo, una máquina virtual).
* Impide que la cuenta de almacenamiento de Hola eliminando si algo lo esté usando activamente (por ejemplo, una máquina virtual).

### <a name="remove-hello-lease-from-hello-vhd"></a>Quitar la concesión de Hola de hello VHD
Si hello VHD es un disco del sistema operativo, debe eliminar concesión de hello VM tooremove hello:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En hello **concentrador** menú, seleccione **máquinas virtuales**.
3. Seleccione Hola máquina virtual que contiene una concesión en hello VHD.
4. Asegúrese de que no esté usando activamente máquina virtual de Hola y que ya no necesita Hola máquina virtual.
5. En parte superior de Hola de hello **detalles de la máquina virtual** hoja, seleccione **eliminar**y, a continuación, haga clic en **Sí** tooconfirm.
6. Hola máquina virtual debe eliminarse, pero se puede conservar Hola VHD. Sin embargo, Hola VHD ya no debe tener una concesión en él. Puede tardar unos minutos para hello concesión toobe publicado. tooverify que Hola concesión se libera, vaya demasiado**todos los recursos** > **nombre de la cuenta de almacenamiento** > **Blobs**  >  **discos duros virtuales**. Hola **Blob propiedades** panel, hello **estado de concesión** valor debe ser **desbloqueado**.

Si hello VHD es un disco de datos, separe Hola VHD de concesión de hello VM tooremove hello:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En hello **concentrador** menú, seleccione **máquinas virtuales**.
3. Seleccione Hola máquina virtual que contiene una concesión en hello VHD.
4. Seleccione **discos** en hello **detalles de la máquina virtual** hoja.
5. Seleccionar disco de datos de Hola que mantiene una concesión en hello VHD. Puede determinar qué disco duro virtual se adjunta en disco de hello mediante la comprobación de la dirección URL de Hola de hello VHD.
6. Determinar con exactitud que nada esté usando activamente el disco de datos de Hola.
7. Haga clic en **separar** en hello **disco detalles** hoja.
8. Ahora se debe desconectar el disco Hola de hello VM y Hola VHD ya no debe tener una concesión en él. Puede tardar unos minutos para hello concesión toobe publicado. se ha liberado tooverify que Hola concesión, vaya demasiado**todos los recursos** > **nombre de la cuenta de almacenamiento** > **Blobs**  >  **discos duros virtuales**. Hola **Blob propiedades** panel, hello **estado de concesión** valor debe ser **desbloqueado**.

## <a name="next-steps"></a>Pasos siguientes
* [Eliminar una cuenta de almacenamiento](storage-create-storage-account.md#delete-a-storage-account)
* [Cómo toobreak Hola bloquea concesión de almacenamiento de blobs de Microsoft Azure (PowerShell)](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
