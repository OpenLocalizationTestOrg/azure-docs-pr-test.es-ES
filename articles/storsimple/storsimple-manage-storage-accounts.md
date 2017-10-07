---
title: aaaManage su cuenta de almacenamiento de StorSimple | Documentos de Microsoft
description: "Explica cómo puede usar hello tooadd de la página de configuración de StorSimple Manager, editar, eliminar o las claves de seguridad de hello girar para una cuenta de almacenamiento."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 93207c40-e0eb-489e-8724-59fb94907081
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/29/2016
ms.author: v-sharos
ms.openlocfilehash: 78f408818ee8532dfaac445200048145547c987c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-storage-account"></a>Usar toomanage de servicio de StorSimple Manager Hola su cuenta de almacenamiento
## <a name="overview"></a>Información general
Hola **configurar** página presenta todos los parámetros de servicio global de Hola que pueden crearse en hello el servicio StorSimple Manager. Estos parámetros pueden ser aplicados tooall Hola dispositivos toohello servicio conectado e incluyen:

* Cuentas de almacenamiento 
* Plantillas de ancho de banda 
* Registros de control de acceso 

Este tutorial le explica cómo puede usar hello **configurar** página tooadd, editar o eliminar cuentas de almacenamiento, o cambiar las claves de seguridad de Hola para una cuenta de almacenamiento.

 ![Página Configurar](./media/storsimple-manage-storage-accounts/HCS_ConfigureService.png)  

Las cuentas de almacenamiento contienen credenciales de Hola que Hola tooaccess de dispositivo usa la cuenta de almacenamiento con su proveedor de servicios de nube. Para las cuentas de almacenamiento de Microsoft Azure, son credenciales como nombre de la cuenta de hello y clave de acceso principal de Hola. 

En hello **configurar** página, todo el almacenamiento de las cuentas que se crean para hello facturación de suscripción se muestran en formato tabular que contiene Hola siguiente información:

* **Nombre** : Hola nombre exclusivo asignado toohello cuenta cuando se creó.
* **Se ha habilitado SSL** : si hello SSL está habilitado y la comunicación de dispositivos a la nube es a través de canal seguro Hola.
* **Utilizado por** : Hola número de volúmenes que usan la cuenta de almacenamiento de Hola.

las tareas más comunes de Hello relacionados con cuentas toostorage que pueden realizarse en hello **configurar** son:

* Agregar una cuenta de almacenamiento 
* Editar una cuenta de almacenamiento 
* Eliminar una cuenta de almacenamiento 
* Rotación de claves de cuentas de almacenamiento 

## <a name="types-of-storage-accounts"></a>Tipos de cuentas de almacenamiento
Hay tres tipos de cuentas de almacenamiento que se pueden usar con el dispositivo StorSimple.

* **Las cuentas de almacenamiento generada automáticamente** – como sugiere su nombre hello, este tipo de cuenta de almacenamiento se genera automáticamente cuando se crea el servicio de Hola. toolearn más información acerca de cómo se crea esta cuenta de almacenamiento, consulte [paso 1: crear un nuevo servicio](storsimple-deployment-walkthrough-u1.md#step-1-create-a-new-service) en [implementar el dispositivo de StorSimple local](storsimple-deployment-walkthrough.md). 
* **Cuentas de almacenamiento en la suscripción al servicio Hola** : estas son cuentas de almacenamiento de Azure de Hola que están asociadas con hello misma suscripción que el servicio de Hola. toolearn más información acerca de cómo se crean estas cuentas de almacenamiento, consulte [sobre cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md). 
* **Las cuentas de almacenamiento fuera de la suscripción al servicio Hola** : estas son cuentas de almacenamiento de Azure de Hola que no están asociadas con el servicio y servicio de hello existía antes probablemente se creó.

## <a name="add-a-storage-account"></a>Agregar una cuenta de almacenamiento
Puede agregar una cuenta de almacenamiento proporcionando un único credenciales de acceso y nombre descriptivas que están vinculados toohello cuenta de almacenamiento (con el proveedor de servicios de nube especificado de hello). También tiene opción de Hola de habilitar Hola secure sockets layer (SSL) modo toocreate un canal seguro para la comunicación de red entre su dispositivo y hello en la nube.

Puede crear varias cuentas para un proveedor de servicios en la nube determinado. Tenga en cuenta, sin embargo, que después de crea una cuenta de almacenamiento, no se puede cambiar el proveedor de servicios de nube de Hola.

Mientras se está guardando la cuenta de almacenamiento de hello, servicio de hello intenta toocommunicate con su proveedor de servicios de nube. las credenciales de Hola y material de acceso de Hola que ha proporcionado se autenticarán en este momento. Solo si Hola autenticación se realiza correctamente, se crea una cuenta de almacenamiento. Si se produce un error en la autenticación de hello, se mostrará un mensaje de error adecuado.

Las cuentas de almacenamiento de Resource Manager creadas en el Portal de Azure también son compatibles con StorSimple. Hola cuentas de almacenamiento no se mostrarán en la lista desplegable de hello para la selección al tratar de toocreate un contenedor de volúmenes, el Administrador de recursos Hola solo se mostrarán las cuentas creadas en portal de Azure clásico Hola de almacenamiento. Las cuentas de almacenamiento de administrador de recursos deberá toobe agregar utilizando Hola procedimiento tooadd una cuenta de almacenamiento se describe a continuación.

> [!NOTE]
> procedimiento de Hola para agregar una cuenta de almacenamiento varía en función de la versión de software de StorSimple Hola que está usando. Estar seguro de procedimiento correcto de Hola de toofollow para su versión de StorSimple.
> 
> 

[!INCLUDE [add-a-storage-account-update1](../../includes/storsimple-configure-new-storage-account-u1.md)]

[!INCLUDE [add-a-storage-account](../../includes/storsimple-configure-new-storage-account.md)]

## <a name="edit-a-storage-account"></a>Editar una cuenta de almacenamiento
Puede editar una cuenta de almacenamiento usada por un contenedor de volúmenes. Si edita una cuenta de almacenamiento que está actualmente en uso, hello solo campo disponible toomodify es Hola tecla de acceso para la cuenta de almacenamiento de Hola. Puede proporcionar la nueva clave de acceso de almacenamiento hello y guardar la configuración de hello actualizado.

#### <a name="tooedit-a-storage-account"></a>tooedit una cuenta de almacenamiento
1. En la página de inicio del servicio de hello, seleccione su servicio, haga doble clic en el nombre del servicio de hello y, a continuación, haga clic en **configurar**.
2. Haga clic en **Agregar/editar cuentas de almacenamiento**.
3. Hola **Agregar/editar cuentas de almacenamiento** cuadro de diálogo:
   
   1. En la lista desplegable de Hola de **cuentas de almacenamiento**, elija una cuenta existente que desearía toomodify. También puede incluir cuentas de almacenamiento de Hola que se generaron automáticamente cuando se creó por primera vez el servicio de Hola.
   2. Si es necesario, puede modificar hello **habilitar modo SSL** selección.
   3. Puede elegir toorotate las claves de acceso de la cuenta de almacenamiento. Vea [rotación de las cuentas de almacenamiento de claves](#key-rotation-of-storage-accounts) para obtener más información acerca de cómo tooperform rotación de claves.
   4. Haga clic en el icono de verificación de hello ![icono de comprobación](./media/storsimple-manage-storage-accounts/HCS_CheckIcon.png) configuración de toosave Hola. se actualizará la configuración de Hello en hello **configurar** página. Haga clic en **guardar** toosave Hola la configuración actualizó recientemente.
      
      ![Editar una cuenta de almacenamiento](./media/storsimple-manage-storage-accounts/HCs_AddEditStorageAccount.png)

## <a name="delete-a-storage-account"></a>Eliminar una cuenta de almacenamiento
> [!IMPORTANT]
> Puede eliminar una cuenta de almacenamiento solo si no la usa un contenedor de volúmenes. Si se utiliza una cuenta de almacenamiento por un contenedor de volumen, primero elimine contenedor de volúmenes de hello y, a continuación, eliminar cuenta de almacenamiento de hello asociado.
> 
> 

#### <a name="toodelete-a-storage-account"></a>toodelete una cuenta de almacenamiento
1. En la página de aterrizaje de servicio de StorSimple Manager hello, seleccione su servicio, haga doble clic en el nombre del servicio de hello y, a continuación, haga clic en **configurar**.
2. En la lista tabular de Hola de cuentas de almacenamiento, mantenga el mouse sobre la cuenta de hello que desea toodelete.
3. Un icono de eliminación (**x**) aparecerán en la columna derecha extreme de Hola para esa cuenta de almacenamiento. Haga clic en hello **x** credenciales de icono toodelete Hola.
4. Cuando se le solicite confirmación, haga clic en **Sí** toocontinue con eliminación de Hola. lista tabular de Hello estará actualizada tooreflect Hola cambios.

## <a name="key-rotation-of-storage-accounts"></a>Rotación de claves de cuentas de almacenamiento
Por motivos de seguridad, la rotación de claves suele ser un requisito en los centros de datos. 

> [!NOTE]
> Hola procedimiento de rotación de hello y la información de rotación de claves aplica solo las cuentas de almacenamiento de Azure de tooMicrosoft. Si usa otro proveedor de servicios en la nube, puede administrar claves de cuenta de almacenamiento a través del panel de ese proveedor.
> 
> 

Cada suscripción de Microsoft Azure puede tener una o más cuentas de almacenamiento asociadas. cuentas de Hello acceso toothese se controla mediante la suscripción de Hola y teclas de acceso para cada cuenta de almacenamiento. 

Cuando se crea una cuenta de almacenamiento, Microsoft Azure genera dos claves de acceso de almacenamiento de 512 bits que se utilizan para la autenticación cuando se tiene acceso a la cuenta de almacenamiento de Hola. Tener dos claves de acceso de almacenamiento permite las claves de hello tooregenerate con ningún servicio de almacenamiento de tooyour de interrupción o un servicio de toothat de acceso. clave que está actualmente en uso Hello es hello *principal* hello y clave clave copia de seguridad es que se hace referencia tooas hello *secundaria* clave. Una de estas dos claves debe suministrarse cuando el dispositivo de Microsoft Azure StorSimple tiene acceso a su proveedor de servicios de almacenamiento en la nube.

## <a name="what-is-key-rotation"></a>¿Qué es la rotación de claves?
Por lo general, aplicaciones usan solo una de hello claves tooaccess los datos. Después de un determinado período de tiempo, puede tener sus aplicaciones cambiar clave de segundo toousing Hola. Después de que haya cambiado la clave secundaria de toohello de aplicaciones, puede retirar la primera clave de hello y, a continuación, genere una nueva clave. Mediante Hola dos claves de esta forma permite que los datos de toohello de acceso de las aplicaciones sin tiempo de inactividad.

claves de cuenta de almacenamiento de Hello siempre se almacenan en el servicio de hello en un formato cifrado. Sin embargo, se puede restablecer mediante Hola el servicio StorSimple Manager. servicio de Hello puede obtener la clave principal de Hola y la clave secundaria para todos Hola cuentas de almacenamiento de hello genera la misma suscripción, incluidas las cuentas creadas en el servicio de almacenamiento de hello, así como cuentas de almacenamiento predeterminadas de Hola Hola cuando el servicio StorSimple Manager primero se creó el servicio. Hola servicio StorSimple Manager siempre obtendrá estas claves de hello portal de Azure clásico y, a continuación, almacenarlos de forma cifrada.

## <a name="rotation-workflow"></a>Flujo de trabajo de rotación
Un administrador de Microsoft Azure puede volver a generar o cambiar clave primaria o secundaria de hello tengan acceso directo a la cuenta de almacenamiento de hello (a través de Hola servicio de almacenamiento de Microsoft Azure). Hola el servicio StorSimple Manager no experimenta este cambio automáticamente.

servicio de StorSimple Manager tooinform Hola de cambio de hello, necesitará el servicio StorSimple Manager de tooaccess hello, tener acceso a la cuenta de almacenamiento de hello y, a continuación, sincronizar clave principal o secundaria de hello (según lo que se haya cambiado). servicio de Hello, a continuación, obtiene la clave más reciente de hello, cifra las claves de Hola y envía el dispositivo de toohello clave de cifrado de Hola.

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service-azure-only"></a>las claves de toosynchronize para cuentas de almacenamiento de Hola misma suscripción que el servicio de hello (solo Azure)
1. En hello **servicios** página, haga clic en hello **configurar** ficha.
2. Haga clic en **Agregar/editar cuentas de almacenamiento**.
3. En el cuadro de diálogo de Hola Hola siguientes:
   
   1. Seleccione la cuenta de almacenamiento de hello con clave de Hola que desea toosynchronize. claves de cuenta de almacenamiento de Hola se cifran cuando se muestran.
   2. En el servicio StorSimple Manager hello, se necesita la clave de Hola de tooupdate que previamente se ha modificado en hello servicio de almacenamiento de Microsoft Azure. Si la clave de acceso principal de Hola se ha cambiado (regenerado), haga clic en **sincronizar clave principal**. Si se ha cambiado la clave secundaria de hello, haga clic en **sincronizar clave secundaria**.
      
      ![sincronizar claves](./media/storsimple-manage-storage-accounts/HCS_KeyRotationStorageAccountSameSubscriptionAsService.png)

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a>claves de toosynchronize las cuentas de almacenamiento fuera de la suscripción al servicio Hola
1. En hello **servicios** página, haga clic en hello **configurar** ficha.
2. Haga clic en **Agregar/editar cuentas de almacenamiento**.
3. En el cuadro de diálogo de Hola Hola siguientes:
   
   1. Seleccione la cuenta de almacenamiento de hello con clave de acceso de Hola que desea tooupdate.
   2. Necesitará la clave de acceso de almacenamiento tooupdate Hola Hola el servicio StorSimple Manager. En este caso, puede ver la clave de acceso de almacenamiento de Hola. Escriba una clave nueva Hola Hola **clave de acceso de cuenta de almacenamiento**y cuadro. 
   3. Guarde los cambios. Ahora debería estar actualizada la clave de acceso de la cuenta de almacenamiento.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información acerca de la [Seguridad de StorSimple](storsimple-security.md).
* Obtenga más información sobre [utilizando Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).

