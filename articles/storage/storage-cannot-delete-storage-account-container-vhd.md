---
title: "eliminar cuentas de almacenamiento de Azure, los contenedores o los discos duros virtuales en una implementación clásica de aaaTroubleshoot | Documentos de Microsoft"
description: "Solución de problemas de eliminación de cuentas de almacenamiento de Azure, contenedores o discos duros virtuales"
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 6bbfa032e1968718c623227bb426d553e2951075
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a>Solución de problemas de eliminación de cuentas de almacenamiento de Azure, contenedores o discos duros virtuales
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

Puede recibir errores al intentar cuenta de almacenamiento de Azure de hello toodelete, contenedor o VHD en hello [portal de Azure](https://portal.azure.com/) o hello [portal de Azure clásico](https://manage.windowsazure.com/). problemas de Hello pueden deberse a Hola siguientes circunstancias:

* Cuando se elimina una máquina virtual, disco de Hola y de disco duro virtual no se eliminan automáticamente. Que puede ser motivo Hola error en eliminación de la cuenta de almacenamiento. No eliminamos disco Hola para que pueda utilizar Hola disco toomount otra máquina virtual.
* Sigue siendo una concesión en un blob de disco o hello que esté asociada con el disco de Hola.
* Sigue siendo una imagen de máquina virtual que está usando una cuenta de almacenamiento, un contenedor o un blob.

Si el problema de Azure no se trata en este artículo, visite Hola foros de Azure en [MSDN y Hola desbordamiento de la pila](https://azure.microsoft.com/support/forums/). Puede publicar su problema en estos foros o too@AzureSupport en Twitter. Además, puede registrar una solicitud de soporte técnico de Azure seleccionando **obtener asistencia** en hello [soporte técnico de Azure](https://azure.microsoft.com/support/options/) sitio.

## <a name="symptoms"></a>Síntomas
Hola siguiente sección enumera los errores comunes que puede producirse cuando intenta las cuentas de almacenamiento de Azure de hello toodelete, contenedores o discos duros virtuales.

### <a name="scenario-1-unable-toodelete-a-storage-account"></a>Escenario 1: No se puede toodelete una cuenta de almacenamiento
Cuando se desplaza toohello cuenta de almacenamiento clásicas en hello [portal de Azure](https://portal.azure.com/) y seleccione **eliminar**, puede aparecer con una lista de objetos que impiden la eliminación de cuenta de almacenamiento de hello:

  ![Imagen de error al eliminar la cuenta de almacenamiento de Hola](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

Cuando se desplaza la cuenta de almacenamiento de toohello en hello [portal de Azure clásico](https://manage.windowsazure.com/) y seleccione **eliminar**, es posible que vea uno de hello siguientes errores:

- *La cuenta de almacenamiento StorageAccountName contiene imágenes de máquina virtual. Asegúrese de que estas imágenes de máquina virtual se quiten antes de eliminar esta cuenta de almacenamiento*.

- *Error de cuenta de almacenamiento toodelete < virtual-storage-account-name >. Cuenta de almacenamiento no se puede toodelete < virtual-storage-account-name >: ' cuenta de almacenamiento < virtual-storage-account-name > tiene algunas imágenes o discos activos. Controle que se quiten las imágenes y los discos antes de eliminar esta cuenta de almacenamiento.'.*

- *La cuenta de almacenamiento &lt;nombre-de-cuenta-de-almacenamiento-de-vm&gt; tiene algunas imágenes o discos activos; por ejemplo, xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Controle que se quiten las imágenes y los discos antes de eliminar esta cuenta de almacenamiento.*

- *La cuenta de almacenamiento &lt;nombre-de-cuenta-de-almacenamiento&gt; tiene 1 contenedor que tiene artefactos de imagen o disco activos. Asegúrese de que estos artefactos se quitan del repositorio de imágenes de hello antes de eliminar esta cuenta de almacenamiento*.

- *Error en el envío. La cuenta de almacenamiento &lt;nombre-de-cuenta-de-almacenamiento-de-vm&gt; tiene 1 contenedor que tiene artefactos de imagen o disco activos. Asegúrese de que estos artefactos se quitan del repositorio de imágenes de hello antes de eliminar esta cuenta de almacenamiento. Cuando intente toodelete una cuenta de almacenamiento y hay sigue activos discos asociados con él, verá un mensaje que indica hay discos activos que necesitan toobe eliminar*.

### <a name="scenario-2-unable-toodelete-a-container"></a>Escenario 2: No se puede toodelete un contenedor
Al tratar de contenedor de almacenamiento de toodelete hello, podría ver Hola siguiente error:

*Contenedor de almacenamiento de toodelete errores <container name>. Error: ' actualmente hay una concesión en el contenedor de Hola y se especificó ningún identificador de concesión en la solicitud de hello*.

O

*Hola siguientes discos de máquina virtual usa blobs en este contenedor y, por lo que no se puede eliminar el contenedor de hello: VirtualMachineDiskName1, VirtualMachineDiskName2,...*

### <a name="scenario-3-unable-toodelete-a-vhd"></a>Escenario 3: No se puede toodelete un disco duro virtual
Después de eliminar una máquina virtual y, a continuación, intente toodelete Hola blobs para hello asocian discos duros virtuales, podría recibir el siguiente mensaje de Hola:

*Blob toodelete error ' ruta de acceso/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: ' actualmente hay una concesión de blob de Hola y se especificó ningún identificador de concesión en la solicitud de saludo.*

O

*BLOB 'BlobName.vhd' está en uso como disco de máquina virtual 'VirtualMachineDiskName', por lo que no se puede eliminar el blob de Hola.*

## <a name="solution"></a>Solución
tooresolve problemas más comunes de hello, intente Hola siguiente método:

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-hello-storage-account-container-or-vhd"></a>Paso 1: Eliminar todos los discos que impiden la eliminación de la cuenta de almacenamiento de hello, el contenedor o el disco duro virtual
1. Cambiar toohello [portal de Azure clásico](https://manage.windowsazure.com/).
2. Seleccione **MÁQUINA VIRTUAL** > **DISCOS**.

    ![Imagen de discos en máquinas virtuales en el Portal de Azure clásico.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. Buscar discos de Hola que están asociados con la cuenta de almacenamiento de hello, contenedor o disco duro virtual que desea toodelete. Al comprobar la ubicación de hello del disco de hello, encontrará Hola asociado de cuenta de almacenamiento, contenedor o disco duro virtual.

    ![Imagen que muestra la información de ubicación de los discos en el Portal de Azure clásico](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. Eliminar discos hello mediante uno de los siguientes métodos de hello:

  - Si no hay ninguna máquina virtual aparece en hello **conectado a** campo del disco de hello, puede eliminar disco Hola directamente.

  - Si hello es un disco de datos, siga estos pasos:

    1. Compruebe el nombre de Hola de hello VM que Hola disco está conectado a.
    2. Vaya demasiado**máquinas virtuales** > **instancias**y, a continuación, busque Hola máquina virtual.
    3. Asegúrese de que no esté usando activamente disco Hola.
    4. Seleccione **ocultar disco** final Hola de disco de hello toodetach portal Hola.
    5. Vaya demasiado**máquinas virtuales** > **discos**y esperar hello **conectado a** tooturn de campo en blanco. Esto indica disco Hola correctamente se ha desasociado de hello máquina virtual.
    6. Seleccione **eliminar** final Hola de **máquinas virtuales** > **discos** disco de hello toodelete.

  - Si el disco de hello es un sistema operativo (hello **OS contiene** campo tiene un valor como Windows) y adjunta tooa máquina virtual, siga estos pasos toodelete Hola VM. no se puede desasociar el disco del sistema operativo Hello, así tendremos concesión de toodelete Hola VM toorelease Hola.

    1. Compruebe el nombre de Hola de Hola Hola de máquina Virtual A que disco de datos está conectado.  
    2. Vaya demasiado**máquinas virtuales** > **instancias**, y, a continuación, seleccione Hola VM que Hola disco está conectado a.
    3. Asegúrese de que no esté usando activamente máquina virtual de Hola y que ya no necesita Hola máquina virtual.
    4. Seleccione Hola VM Hola disco está conectado a, a continuación, seleccione **eliminar** > **Hola de eliminación de discos conectados**.
    5. Vaya demasiado**máquinas virtuales** > **discos**y esperar Hola disco toodisappear.  Puede tardar unos minutos para este toooccur y puede que necesite toorefresh página de Hola.
    6. Si el disco de hello no desaparece, espere hello **conectado a** tooturn de campo en blanco. Esto indica disco Hola totalmente se ha desasociado de hello máquina virtual.  A continuación, seleccione el disco de Hola y seleccione **eliminar** final Hola de hello páginas toodelete Hola disco.


   > [!NOTE]
   > Si un disco está conectado tooa VM, no será capaz de toodelete lo. Los discos se desconectan de una máquina virtual eliminada de forma asincrónica. Pueden tardar unos minutos después de elimina Hola VM para este tooclear campo seguridad.
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-hello-storage-account-or-container"></a>Paso 2: Elimine las imágenes de máquina virtual que impiden la eliminación de cuenta de almacenamiento de Hola o contenedor
1. Cambiar toohello [portal de Azure clásico](https://manage.windowsazure.com/).
2. Seleccione **máquina VIRTUAL** > **imágenes**y, a continuación, eliminar imágenes de Hola que están asociadas a la cuenta de almacenamiento de hello, el contenedor o el disco duro virtual.

    Después de eso, cuenta de almacenamiento de toodelete hello, contenedor o VHD vuelva a intentarlo.

> [!WARNING]
> Prepararse nada tooback seguro de que desea toosave antes de eliminar la cuenta de hello. La eliminación de un VHD, blob, tabla, cola o archivo tiene carácter permanente una vez realizada. Asegúrese de que el recurso de hello no está en uso.
>
>

## <a name="about-hello-stopped-deallocated-status"></a>Acerca de hello estado detenido (desasignado)
Las máquinas virtuales que se crearon en el modelo de implementación clásica de Hola y que se han conservado tendrá hello **detenido (desasignado)** estado en cualquier hello [portal de Azure](https://portal.azure.com/) o [portal de Azure clásico ](https://manage.windowsazure.com/).

**Portal de Azure clásico**:

![Estado Detenido (desasignado) de VM en el Portal de Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

**Portal de Azure**:

![Estado Detenido (desasignado) de VM en el Portal de Azure clásico.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

Un estado "Detenido (desasignado)" libera los recursos de equipo de hello, como Hola CPU, memoria y red. Sin embargo, los discos de Hello, todavía se conservan para que se puede volver a crear rápidamente Hola VM si es necesario. Estos discos se crean encima de los discos duros virtuales que están respaldados por Almacenamiento de Azure. cuenta de almacenamiento de Hello tiene estos discos duros virtuales y discos de hello tienen concesiones en los discos duros virtuales.

## <a name="next-steps"></a>Pasos siguientes
* [Eliminar una cuenta de almacenamiento](storage-create-storage-account.md#delete-a-storage-account)
