---
title: registros de control de acceso de aaaManage en StorSimple | Documentos de Microsoft
description: "Describe cómo el control de acceso toouse registros toodetermine (ACR) qué hosts pueden conectarse tooa volumen en el dispositivo StorSimple Hola."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>Usar registros de control de acceso de hello StorSimple Manager servicio toomanage
## <a name="overview"></a>Información general
Registros de control de acceso (ACR) le permiten toospecify qué hosts pueden conectarse tooa volumen en el dispositivo StorSimple Hola. Acr se establecen volumen específico tooa y contener Hola iSCSI (iqn) de nombres completos de los hosts de Hola. Cuando un host intenta tooconnect tooa volumen, la comprobación de dispositivo de Hola Hola que ACR asociado a ese volumen para el nombre IQN de Hola y si se encuentra una coincidencia, hello se establezca la conexión. registros de control de acceso de Hello sección en hello **configurar** página muestra todos los registros de control de acceso de hello con hello correspondiente IQN de los hosts de Hola.

Este tutorial le explica Hola siguientes tareas comunes relacionadas con el ACR:

* Agregar un registro de control de acceso 
* Editar un registro de control de acceso 
* Eliminar un registro de control de acceso 

> [!IMPORTANT]
> * Al asignar un volumen de tooa ACR, tenga cuidado que volumen hello no es simultáneamente tenga acceso más de un host no agrupado porque esto podría dañar el volumen de Hola. 
> * Al eliminar un ACR de un volumen, asegúrese de que ese host correspondiente hello no se tiene acceso a volumen Hola porque Hola eliminación podría dar lugar a una interrupción de lectura y escritura.
> 
> 

## <a name="add-an-access-control-record"></a>Agregar un registro de control de acceso
Usar el servicio StorSimple Manager hello **configurar** página tooadd ACR. Normalmente, se asociará un ACR a un volumen.

Realizar Hola siguiendo los pasos tooadd un ACR.

#### <a name="tooadd-an-access-control-record"></a>tooadd un registro de control de acceso
1. En la página de inicio del servicio de hello, seleccione su servicio, haga doble clic en el nombre del servicio de hello y, a continuación, haga clic en hello **configurar** ficha.
2. Hola tabular listado en **registros de control de acceso**, proporcione un **nombre** para el ACR.
3. Proporcione el nombre IQN de Hola de su host de Windows en **nombre del iniciador iSCSI**. Hola tooget IQN del host Windows Server, Hola siguientes:
   
   * Inicie el iniciador iSCSI de Microsoft de hello en el host de Windows.
   * Hola **propiedades del iniciador iSCSI** ventana hello **configuración** ficha, seleccione y copie cadena Hola de hello **nombre del iniciador** campo.
   * Pegue esta cadena en hello **nombre del iniciador iSCSI** campo en la tabla de ACR Hola Hola portal de Azure clásico.
4. Haga clic en **guardar** hello toosave recién creado ACR. Hola tabular enumerar will ser tooreflect actualizado esta adición.

## <a name="edit-an-access-control-record"></a>Editar un registro de control de acceso
Usar hello **configurar** página Hola ACR Azure tooedit portal clásico. 

> [!NOTE]
> Puede modificar solo esos ACR que no están actualmente en uso. tooedit que un ACR asociado a un volumen que está actualmente en uso, primero debe realizar volumen Hola sin conexión.
> 
> 

Realizar Hola siguiendo los pasos tooedit un ACR.

#### <a name="tooedit-an-access-control-record"></a>tooedit un registro de control de acceso
1. En la página de inicio del servicio de hello, seleccione su servicio, haga doble clic en el nombre del servicio de hello y, a continuación, haga clic en hello **configurar** ficha.
2. En la lista tabular de Hola de registros de control de acceso de hello, mantenga el mouse sobre Hola ACR que desea toomodify.
3. Proporcione un nombre nuevo o el IQN de hello ACR.
4. Haga clic en **guardar** toosave Hola modificado el ACR. Hola tabular enumerar will ser tooreflect actualizado este cambio.

## <a name="delete-an-access-control-record"></a>Eliminar un registro de control de acceso
Usar hello **configurar** página Hola ACR Azure toodelete portal clásico. 

> [!NOTE]
> Solo puede eliminar esos ACR que no están actualmente en uso. toodelete que un ACR asociado a un volumen que está actualmente en uso, primero debe realizar volumen Hola sin conexión.
> 
> 

Realizar Hola siguiendo los pasos toodelete un registro de control de acceso.

#### <a name="toodelete-an-access-control-record"></a>toodelete un registro de control de acceso
1. En la página de inicio del servicio de hello, seleccione su servicio, haga doble clic en el nombre del servicio de hello y, a continuación, haga clic en hello **configurar** ficha.
2. En la lista tabular de Hola de registros de control de acceso (ACR) de hello, mantenga el mouse sobre Hola ACR que desea toodelete.
3. Un icono de eliminación (**x**) aparecerá en hello la columna extrema derecha para hello ACR que seleccione. Haga clic en hello **x** Hola de icono toodelete ACR.
4. Cuando se le solicite confirmación, haga clic en **Sí** toocontinue con eliminación de Hola. lista tabular de Hello estará actualizada tooreflect Hola eliminación.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información sobre la [administración de volúmenes de StorSimple](storsimple-manage-volumes.md).
* Obtenga más información sobre [utilizando Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).

