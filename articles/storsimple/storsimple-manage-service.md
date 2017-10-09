---
title: Hola aaaDeploy el servicio StorSimple Manager | Documentos de Microsoft
description: "Explica cómo toocreate y delete Hola el servicio StorSimple Manager Hola portal de Azure clásico y se describe cómo toomanage Hola clave de registro del servicio."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: bc1d5650-275c-42ed-bc77-cdb596f85943
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f49b647d91b03bb89ebd0e5cce196e50e3c00296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-manager-service-in-hello-azure-classic-portal"></a>Implementar el servicio de StorSimple Manager Hola Hola portal de Azure clásico

## <a name="overview"></a>Información general
Hola el servicio StorSimple Manager se ejecuta en Microsoft Azure y conecta a los dispositivos de StorSimple toomultiple. Después de crear el servicio de hello, se pueden usar dispositivos de hello toomanage desde Hola Microsoft Azure clásico portal se ejecuta en un explorador. Esto le permite toomonitor todos los dispositivos de Hola que están conectado toohello StorSimple Manager el servicio desde una única ubicación central, con lo que se minimiza el trabajo administrativo.

página de inicio del Administrador de StorSimple Hola enumera todos los servicios de StorSimple Manager de hello puede usar toomanage en los dispositivos de almacenamiento de StorSimple. Para cada servicio StorSimple Manager, Hola siguiente información se presenta en la página del Administrador de StorSimple de hello:

* **Nombre** : nombre de Hola que se asignó el servicio StorSimple Manager tooyour cuando se creó. **no se puede cambiar el nombre del servicio Hola después de crear el servicio de Hola. Esto también es cierto para otras entidades como dispositivos, volúmenes, contenedores de volúmenes y las directivas de copia de seguridad que no se pueden cambiar en hello portal de Azure clásico.**
* **Estado** : Hola estado del servicio de hello, que puede ser **Active**, **crear**, o **Online**.
* **Ubicación** : Hola ubicación geográfica en qué hello StorSimple se implementará el dispositivo.
* **Suscripción** : hello suscripción que está asociado con el servicio de facturación.

Hola tareas comunes que pueden realizarse a través de la página del Administrador de StorSimple de hello son:

* Crear un servicio
* Eliminar un servicio
* Obtener clave de registro del servicio de Hola
* Regenerar la clave de registro del servicio de Hola

Este tutorial se describe cómo tooperform de estas tareas.

## <a name="create-a-service"></a>Crear un servicio
Hola de uso **creación rápida** opción toocreate un servicio StorSimple Manager si desea que toodeploy el dispositivo StorSimple. toocreate un servicio, necesita toohave:

* Una suscripción con un contrato Enterprise
* Una cuenta de Almacenamiento de Microsoft Azure activa.
* Hola información de facturación que se usa para la administración de acceso

También puede elegir toogenerate en una cuenta de almacenamiento de forma predeterminada cuando se crea el servicio de Hola.

Un único servicio puede administrar varios dispositivos. Sin embargo, un dispositivo no puede abarcar varios servicios. Una gran empresa puede tener varios toowork de instancias de servicio con distintas suscripciones, organizaciones o incluso regiones de implementación. Tenga en cuenta que necesita separar instancias de dispositivos serie 8000 de StorSimple toomanage del servicio de StorSimple Manager y arreglos de discos virtuales de StorSimple.

> [!IMPORTANT] 
> Si tiene un servicio sin usar creado (ningún dispositivo que se realizaron las operaciones en este recurso) anterior tooAugust 2016, no se pueden administrar a través del portal de Azure o el portal de Azure clásico. Le recomendamos que cree un nuevo servicio en hello portal de Azure.

Realizar Hola siguiendo los pasos toocreate un servicio.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

## <a name="delete-a-service"></a>Eliminar un servicio
Antes de eliminar un servicio, asegúrese de que no lo esté utilizando ningún dispositivo conectado. Si el servicio de hello está en uso, desactive los dispositivos de hello conectado. Hola desactivar la operación se Hola conexión entre el dispositivo de Hola y el servicio de hello, pero conserva los datos del dispositivo hello en la nube de Hola.

> [!IMPORTANT] 
> Después de elimina un servicio, no se puede revertir la operación de Hola. Cualquier dispositivo que estaba utilizando el servicio de hello deberá toobe antes de que se puede utilizar con otro servicio de restablecimiento de fábrica. En este escenario, los datos locales de hello en dispositivo hello, así como la configuración de hello, se perderán.

Realizar Hola siguiendo los pasos toodelete un servicio.

### <a name="toodelete-a-service"></a>toodelete un servicio
1. En hello **el servicio StorSimple Manager** página servicio Hola select que desea toodelete.
2. Haga clic en **eliminar** final Hola de página Hola.
3. Haga clic en **Sí** en la notificación de confirmación de Hola. Puede tardar unos minutos para hello servicio toobe eliminado.

## <a name="get-hello-service-registration-key"></a>Obtener clave de registro del servicio de Hola
Después de haber creado correctamente un servicio, deberá tooregister el dispositivo StorSimple con el servicio de Hola. tooregister el primer dispositivo de StorSimple, se necesita Hola clave de registro del servicio. tooregister dispositivos adicionales con un servicio existente de StorSimple, necesitará la clave de registro de hello y clave de cifrado de datos de servicio de hello (que se genera en el primer dispositivo de Hola durante el registro). Para obtener más información acerca de la clave de cifrado de datos del servicio de hello, consulte [seguridad de StorSimple](storsimple-security.md). Puede obtener clave de registro de hello, acceda a **clave de registro** en hello **servicios** página.

Realizar Hola después de la clave de registro del servicio de pasos tooget Hola.

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

Mantenga la clave de registro del servicio de hello en una ubicación segura. Necesitará esta clave, así como clave de cifrado de datos del servicio de hello, tooregister dispositivos adicionales con este servicio. Después de obtener la clave de registro del servicio de hello, necesitará tooconfigure el dispositivo a través de hello Windows PowerShell para StorSimple interfaz.

Para obtener más información acerca de cómo toouse esta clave, consulte el registro [paso 3: Configure y registre el dispositivo de Hola a través de Windows PowerShell para StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-hello-service-registration-key"></a>Regenerar la clave de registro del servicio de Hola
Necesitará una clave de registro del servicio de tooregenerate si es necesario tooperform rotación de claves o si ha cambiado la lista de Hola de administradores de servicios. Cuando vuelva a generar clave de hello, nueva clave de Hola se usa solo para registrar dispositivos subsiguientes. dispositivos de Hola que ya estaban registrados no se ven afectados por este proceso.

Realizar Hola siguiendo los pasos tooregenerate una clave de registro del servicio.

### <a name="tooregenerate-hello-service-registration-key"></a>clave de registro del servicio de tooregenerate Hola
1. En hello **el servicio StorSimple Manager** página, haga clic en **clave de registro**.
2. Hola **clave de registro del servicio** cuadro de diálogo, haga clic en **regenerar**.
3. Aparecerá un mensaje de confirmación. Haga clic en **Aceptar** toocontinue con regeneración Hola.
4. Aparecerá una nueva clave de registro de servicio.
5. Copie esta clave y guárdela para registrar los dispositivos nuevos con este servicio.
6. Haga clic en el icono de verificación de Hola ![Icono de marca de verificación](./media/storsimple-manage-service/HCS_CheckIcon.png) tooclose este cuadro de diálogo.

## <a name="next-steps"></a>Pasos siguientes
* Obtener más información sobre hello [proceso de implementación de StorSimple](storsimple-deployment-walkthrough-u2.md).
* Obtenga más información sobre cómo [administrar su cuenta de almacenamiento de StorSimple](storsimple-manage-storage-accounts.md).
* Más información acerca de cómo demasiado[uso Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).
