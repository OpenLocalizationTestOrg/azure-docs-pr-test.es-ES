---
title: registros de control de acceso de aaaManage en StorSimple | Documentos de Microsoft
description: "Describe cómo el control de acceso toouse registros toodetermine (ACR) qué hosts pueden conectarse tooa volumen en el dispositivo StorSimple Hola."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>Usar registros de control de acceso de hello StorSimple Manager servicio toomanage

## <a name="overview"></a>Información general
Registros de control de acceso (ACR) le permiten toospecify qué hosts pueden conectarse tooa volumen en el dispositivo StorSimple Hola. Acr se establecen volumen específico tooa y contener Hola iSCSI (iqn) de nombres completos de los hosts de Hola. Cuando un host intenta tooconnect tooa volumen, la comprobación de dispositivo de Hola Hola que ACR asociado a ese volumen para el nombre IQN de Hola y si se encuentra una coincidencia, hello se establezca la conexión. Hola registros de control de acceso en hello **configuración** sección de la hoja de servicio del Administrador de dispositivos de StorSimple mostrar todos los registros de control de acceso de hello con hello correspondiente IQN de los hosts de Hola.

Este tutorial le explica Hola siguientes tareas comunes relacionadas con el ACR:

* Agregar un registro de control de acceso
* Editar un registro de control de acceso
* Eliminar un registro de control de acceso

> [!IMPORTANT]
> * Al asignar un volumen de tooa ACR, tenga cuidado que volumen hello no es simultáneamente tenga acceso más de un host no agrupado porque esto podría dañar el volumen de Hola.
> * Al eliminar un ACR de un volumen, asegúrese de que ese host correspondiente hello no se tiene acceso a volumen Hola porque Hola eliminación podría dar lugar a una interrupción de lectura y escritura.

## <a name="get-hello-iqn"></a>Obtener Hola IQN

Realizar Hola siguiendo los pasos tooget Hola IQN de un host de Windows que ejecuta Windows Server 2012.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a>Agregar un registro de control de acceso
Usar hello **configuración** sección en hello Administrador de dispositivos de StorSimple servicio hoja tooadd ACR. Normalmente, se asociará un ACR a un volumen.

Realizar Hola siguiendo los pasos tooadd un ACR.

#### <a name="tooadd-an-acr"></a>tooadd un ACR

1. Servicio de administrador de dispositivos de StorSimple tooyour go, haga doble clic Hola nombre del servicio y, a continuación, en hello **configuración** sección, haga clic en **registros de control de acceso**.
2. Hola **registros de control de acceso** hoja, haga clic en **+ agregar ACR**.

    ![Hacer clic en Agregar ACR](./media/storsimple-8000-manage-acrs/createacr1.png)

3. Hola **agregar ACR** hoja, Hola lo siguiente:

    1. Proporcione un Nombre para el ACR.
    
    2. Proporcione el nombre IQN de Hola de su host de Windows Server en **iSCSI nombre de iniciador (IQN)**.

    3. Haga clic en **agregar** toocreate Hola ACR.

        ![Hacer clic en Agregar ACR](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  Hola recién agregado que ACR se mostrará en la lista tabular de Hola de ACR.

    ![Hacer clic en Agregar ACR](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a>Editar un registro de control de acceso
Usar hello **configuración** sección en hello Administrador de dispositivos de StorSimple servicio hoja tooedit ACR.

> [!NOTE]
> Es recomendable que modifique solo los ACR que no están actualmente en uso. tooedit que un ACR asociado a un volumen que está actualmente en uso, primero debe realizar volumen Hola sin conexión.

Realizar Hola siguiendo los pasos tooedit un ACR.

#### <a name="tooedit-an-access-control-record"></a>tooedit un registro de control de acceso
1.  Servicio de administrador de dispositivos de StorSimple tooyour go, haga doble clic Hola nombre del servicio y, a continuación, en hello **configuración** sección, haga clic en **registros de control de acceso**.

    ![Vaya tooaccess controlar registros](./media/storsimple-8000-manage-acrs/createacr1.png)

2. En la lista tabular de Hola de registros de control de acceso de hello, haga clic en y seleccione Hola ACR que desea toomodify.

    ![Edición de registros de control de acceso](./media/storsimple-8000-manage-acrs/editacr1.png)

3. Hola **registro de control de acceso de edición** hoja, proporcionar un host distinto de tooanother IQN correspondiente.

    ![Edición de registros de control de acceso](./media/storsimple-8000-manage-acrs/editacr2.png)

4. Haga clic en **Guardar**. Cuando se le pida confirmación, haga clic en **Sí**. 

    ![Edición de registros de control de acceso](./media/storsimple-8000-manage-acrs/editacr3.png)

5. Se le notificará cuando se actualiza Hola ACR. lista tabular de Hello también actualiza los cambios de hello tooreflect.

   
## <a name="delete-an-access-control-record"></a>Eliminar un registro de control de acceso
Usar hello **configuración** sección en hello Administrador de dispositivos de StorSimple servicio hoja toodelete ACR.

> [!NOTE]
> Solo puede eliminar esos ACR que no están actualmente en uso. toodelete que un ACR asociado a un volumen que está actualmente en uso, primero debe realizar volumen Hola sin conexión.

Realizar Hola siguiendo los pasos toodelete un registro de control de acceso.

#### <a name="toodelete-an-access-control-record"></a>toodelete un registro de control de acceso
1.  Servicio de administrador de dispositivos de StorSimple tooyour go, haga doble clic Hola nombre del servicio y, a continuación, en hello **configuración** sección, haga clic en **registros de control de acceso**.

    ![Vaya tooaccess controlar registros](./media/storsimple-8000-manage-acrs/createacr1.png)

2. En la lista tabular de Hola de registros de control de acceso de hello, haga clic en y seleccione Hola ACR que desea toodelete.

    ![Vaya tooaccess controlar registros](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. Haga clic en el menú contextual de tooinvoke hello y seleccione **eliminar**.

    ![Vaya tooaccess controlar registros](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. Cuando se le pida confirmación, revise la información de hello y, a continuación, haga clic en **eliminar**.

    ![Vaya tooaccess controlar registros](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. Se le notificará cuando se complete la eliminación de Hola. lista tabular de Hello es tooreflect actualizada Hola eliminación.

    ![Vaya tooaccess controlar registros](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información sobre la [administración de volúmenes de StorSimple](storsimple-8000-manage-volumes-u2.md).
* Obtenga más información sobre [utilizando Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

