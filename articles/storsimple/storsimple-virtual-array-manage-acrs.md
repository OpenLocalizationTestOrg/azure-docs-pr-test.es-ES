---
title: registros de control de acceso de aaaManage para StorSimple Virtual Array | Documentos de Microsoft
description: "Describe cómo el control de acceso toomanage registros toodetermine (ACR) qué hosts pueden conectarse tooa volumen hello StorSimple Virtual Array."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a>Use el Administrador de dispositivos de StorSimple toomanage registros de control de acceso para StorSimple Virtual Array

## <a name="overview"></a>Información general

Registros de control de acceso (ACR) le permiten toospecify qué hosts pueden conectarse tooa volumen hello StorSimple Virtual Array (también conocido como hello StorSimple en dispositivo virtual local). Acr se establecen volumen específico tooa y contener Hola iSCSI (iqn) de nombres completos de los hosts de Hola. Cuando un host intenta tooconnect tooa volumen, dispositivo Hola comprueba Hola ACR asociado a ese volumen para el nombre IQN de hello y, si hay una coincidencia, se establece conexión Hola. Hola **registros de control de acceso** hoja dentro de hello **configuración** sección de su servicio de administrador de dispositivos muestra todos los registros de control de acceso de hello con hello correspondiente IQN de los hosts de Hola.

![Administrar registros de control de acceso](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

Este tutorial le explica Hola siguientes tareas comunes relacionadas con el ACR:

* Obtener Hola IQN
* Agregar un registro de control de acceso
* Editar un registro de control de acceso
* Eliminar un registro de control de acceso

> [!IMPORTANT]
> 
> * Al asignar un volumen de tooa ACR, tenga cuidado que volumen hello no es simultáneamente tenga acceso más de un host no agrupado porque esto podría dañar el volumen de Hola.
> * Al eliminar un ACR de un volumen, asegúrese de que ese host correspondiente hello no se tiene acceso a volumen Hola porque Hola eliminación podría dar lugar a una interrupción de lectura y escritura.


## <a name="get-hello-iqn"></a>Obtener Hola IQN

Realizar Hola siguiendo los pasos tooget Hola IQN de un host de Windows que ejecuta Windows Server 2012.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a>Adición de ACR

Usa **registros de control de acceso** hoja dentro de hello **configuración** sección de su tooadd de servicio de administrador de dispositivos de StorSimple ACR. Normalmente, se asociará un ACR a un volumen.

Para obtener información sobre cómo asociar un ACR a un volumen, consulte demasiado[agregar un volumen](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).

> [!IMPORTANT]
> Al asignar un volumen de tooa ACR, tenga cuidado que volumen hello no es simultáneamente tenga acceso más de un host no agrupado porque esto podría dañar el volumen de Hola.


Realizar Hola siguiendo los pasos tooadd un ACR.

#### <a name="tooadd-an-acr"></a>tooadd un ACR

1. En la página de inicio del servicio de hello, seleccione su servicio, haga doble clic Hola nombre del servicio y, a continuación, en hello **configuración** sección, haga clic en **registros de control de acceso**.
2. Hola **registros de control de acceso** hoja, haga clic en **agregar**.
3. Hola **agregar ACR** hoja, Hola siguientes:
   
    1. Proporcione un **Nombre** para el ACR.
    
    2. En **nombre del iniciador iSCSI**, proporcione el nombre IQN de Hola de su host de Windows. Hola tooget IQN del host Windows Server, Hola siguientes:
   
    3. Inicie el iniciador iSCSI de Microsoft de hello en el host de Windows. En la ventana de propiedades del iniciador de iSCSI de hello en hello **configuración** ficha, seleccione y copie cadena Hola de hello **nombre del iniciador** campo.
    Pegue esta cadena en hello **IQN** campo hello **agregar ACR** hoja.
   
    6. Haga clic en **agregar** tooadd Hola ACR.  
   
        ![Incorporación de registros de control de acceso](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. Hola lista tabular es tooreflect actualizado esta adición.

## <a name="edit-an-acr"></a>Edición de un ACR

Usar hello **registros de control de acceso** hoja dentro de hello **configuración** sección de su servicio de administrador de dispositivos en hello ACR tooedit de portal de Azure.

> [!NOTE]
> No debe modificar un ACR que esté en uso. tooedit que un ACR asociado a un volumen que está actualmente en uso, primero debe realizar volumen Hola sin conexión.


Realizar Hola siguiendo los pasos tooedit un ACR.

#### <a name="tooedit-an-acr"></a>tooedit un ACR

1. En la página de inicio del servicio de hello, seleccione su servicio, haga doble clic Hola nombre del servicio y, a continuación, en hello **configuración** sección, **registros de control de acceso**.
2. Hola **registros de control de acceso** hoja, de la lista tabular de Hola de registros de control de acceso de hello, haga doble clic en hello ACR que desea toomodify.
3. Hola **registros de control de acceso de edición** hoja, Hola siguientes:
   
    1. Fuente de alimentación hello IQN de hello ACR.
   
    2. Haga clic en **guardar** en parte superior de Hola de hello hoja toosave Hola modificado el ACR. Vea Hola siguiente mensaje de confirmación:
   
        ![Edición de registros de control de acceso](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a>Eliminar un registro de control de acceso

Usar hello **configuración** página Hola ACR toodelete de portal de Azure.

> [!NOTE]
> 
> * No debe eliminar un ACR que esté en uso. toodelete que un ACR asociado a un volumen que está actualmente en uso, primero debe realizar volumen Hola sin conexión.
> * Al eliminar un ACR de un volumen, asegúrese de que ese host correspondiente hello no se tiene acceso a volumen Hola porque Hola eliminación podría dar lugar a una interrupción de lectura y escritura.


Realizar Hola siguiendo los pasos toodelete un registro de control de acceso.

#### <a name="toodelete-an-access-control-record"></a>toodelete un registro de control de acceso

1. En la página de inicio del servicio de hello, seleccione su servicio, haga doble clic Hola nombre del servicio y, a continuación, en hello **configuración** sección, **registros de control de acceso**.

2. Hola **registros de control de acceso** hoja, de la lista tabular de Hola de registros de control de acceso de hello, haga doble clic en hello ACR que desea toodelete.

3. En la hoja de registros de control de acceso de hello editar, haga clic en **eliminar**.
   
    ![Eliminación de ACR](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. Cuando se le solicite confirmación, haga clic en **eliminar** toocontinue con eliminación de Hola. lista tabular de Hello es tooreflect actualizada Hola eliminación.
   
   ![Mensaje de advertencia](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a>Pasos siguientes

* Obtenga más información sobre la [adición de volúmenes y la configuración de ACR](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).

