---
title: aaaDeploy servicio de administrador de dispositivos de StorSimple | Documentos de Microsoft
description: "Explica cómo toocreate y delete Hola servicio Administrador de dispositivos de StorSimple en hello portal de Azure y se describe cómo toomanage Hola clave de registro del servicio."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a>Implementar el servicio de administrador de dispositivos de StorSimple de Hola para StorSimple Virtual Array
## <a name="overview"></a>Información general

Hola servicio Administrador de dispositivos de StorSimple se ejecuta en Microsoft Azure y conecta a los dispositivos de StorSimple toomultiple. Después de crear el servicio de hello, se pueden usar dispositivos de hello toomanage desde Hola Microsoft Azure portal se ejecuta en un explorador. Esto le permite toomonitor todos los dispositivos de hello toohello conectado el Administrador de dispositivos de StorSimple el servicio desde una única ubicación central, con lo que se minimiza el trabajo administrativo.

Hola comunes tareas relacionadas tooa servicio de administrador de dispositivos de StorSimple son:

* Crear un servicio
* Eliminar un servicio
* Obtener clave de registro del servicio de Hola
* Regenerar la clave de registro del servicio de Hola

Este tutorial describe cómo tooperform de Hola tareas anteriores. información de Hello contenida en este artículo es aplicable únicamente tooStorSimple Virtual las matrices. Para obtener más información acerca de la serie StorSimple 8000, vaya demasiado[implementar un servicio de StorSimple Manager](storsimple-manage-service.md).

## <a name="create-a-service"></a>Crear un servicio

toocreate un servicio, necesita toohave:

* Una suscripción con un contrato Enterprise
* Una cuenta de Almacenamiento de Microsoft Azure activa.
* Hola información de facturación que se usa para la administración de acceso

También puede elegir toogenerate en una cuenta de almacenamiento al crear el servicio de Hola.

Un único servicio puede administrar varios dispositivos. Sin embargo, un dispositivo no puede abarcar varios servicios. Una gran empresa puede tener varios toowork de instancias de servicio con distintas suscripciones, organizaciones o incluso regiones de implementación.

> [!NOTE]
> Necesita instancias independientes de los dispositivos serie 8000 de StorSimple toomanage del servicio de administrador de dispositivos de StorSimple y arreglos de discos virtuales de StorSimple.


Realizar Hola siguiendo los pasos toocreate un servicio.

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a>Eliminar un servicio

Antes de eliminar un servicio, asegúrese de que no lo esté utilizando ningún dispositivo conectado. Si el servicio de hello está en uso, desactive los dispositivos de hello conectado. Hola desactivar la operación se Hola conexión entre el dispositivo de Hola y el servicio de hello, pero conserva los datos del dispositivo hello en la nube de Hola.

> [!IMPORTANT]
> Después de elimina un servicio, no se puede revertir la operación de Hola. Cualquier dispositivo que estaba utilizando el servicio de hello deberá toobe antes de que se puede utilizar con otro servicio de restablecimiento de fábrica. En este escenario, los datos locales de hello en dispositivo hello, así como la configuración de hello, se perderán.
 

Realizar Hola siguiendo los pasos toodelete un servicio.

#### <a name="toodelete-a-service"></a>toodelete un servicio

1. Vaya demasiado**todos los recursos**. Busque el servicio StorSimple Device Manager. Seleccione servicio de Hola que desea toodelete.
   
    ![Seleccione toodelete de servicio](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. Vaya tooyour servicio panel tooensure no hay ningún dispositivo conectado toohello servicio. Si no hay ningún dispositivo registrado con este servicio, también verá un efecto de toohello de mensaje de pancarta. Hacer clic en **Eliminar**.
   
    ![Eliminar servicio](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. Cuando se le solicite confirmación, haga clic en **Sí** en la notificación de confirmación de Hola. 
   
    ![Confirmación de la eliminación del servicio](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. Puede tardar unos minutos para hello servicio toobe eliminado. Después de hello servicio se elimina correctamente, se le notificará.
   
    ![Eliminación del servicio correcta](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

se actualizará la lista de Hello de servicios.

 ![Lista de servicios actualizada](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a>Obtener clave de registro del servicio de Hola
Después de haber creado correctamente un servicio, deberá tooregister el dispositivo StorSimple con el servicio de Hola. tooregister el primer dispositivo de StorSimple, se necesita Hola clave de registro del servicio. tooregister dispositivos adicionales con un servicio existente de StorSimple, necesitará la clave de registro de hello y clave de cifrado de datos de servicio de hello (que se genera en el primer dispositivo de Hola durante el registro). Para obtener más información acerca de la clave de cifrado de datos del servicio de hello, consulte [seguridad de StorSimple](storsimple-security.md). Puede obtener clave de registro de hello accediendo hello **claves** hoja para el servicio.

Realizar Hola después de la clave de registro del servicio de pasos tooget Hola.

#### <a name="tooget-hello-service-registration-key"></a>clave de registro del servicio de tooget Hola
1. Hola **el Administrador de dispositivos de StorSimple** hoja, vaya demasiado**administración &gt;**  **claves**.
   
   ![Hoja de claves](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. Hola **claves** blade, se muestra una clave de registro del servicio. Copie la clave de registro de hello mediante el icono de copiar Hola. 

Mantenga la clave de registro del servicio de hello en una ubicación segura. Necesitará esta clave, así como clave de cifrado de datos del servicio de hello, tooregister dispositivos adicionales con este servicio. Después de obtener la clave de registro del servicio de hello, necesitará tooconfigure el dispositivo a través de hello Windows PowerShell para StorSimple interfaz.

## <a name="regenerate-hello-service-registration-key"></a>Regenerar la clave de registro del servicio de Hola
Necesitará una clave de registro del servicio de tooregenerate si es necesario tooperform rotación de claves o si ha cambiado la lista de Hola de administradores de servicios. Cuando vuelva a generar clave de hello, nueva clave de Hola se usa solo para registrar dispositivos subsiguientes. dispositivos de Hola que ya estaban registrados no se ven afectados por este proceso.

Realizar Hola siguiendo los pasos tooregenerate una clave de registro del servicio.

#### <a name="tooregenerate-hello-service-registration-key"></a>clave de registro del servicio de tooregenerate Hola
1. Hola **el Administrador de dispositivos de StorSimple** hoja, vaya demasiado**administración &gt;**  **claves**.
   
   ![Hoja de claves](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. Hola **claves** hoja, haga clic en **regenerar**.
   
   ![Haga clic en Regenerar](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. Hola **Regenerar clave de registro** hoja, revisión Hola requiere una acción cuando hello se vuelven a generar las claves. Todos los dispositivos subsiguientes Hola que están registrados con este servicio usará la nueva clave de registro de hello. Haga clic en **regenerar** tooconfirm. Se le notificará una vez completado el registro de hello.
   
   ![Confirmación de la clave regenerada](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. Aparecerá una nueva clave de registro de servicio.
   
    ![Confirmación de la clave regenerada](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   Copie esta clave y guárdela para registrar los dispositivos nuevos con este servicio.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[Introducción](storsimple-virtual-array-deploy1-portal-prep.md) con una matriz Virtual de StorSimple.
* Obtenga información acerca de cómo demasiado[administrar el dispositivo StorSimple](storsimple-ova-web-ui-admin.md).

