---
title: credenciales de cuenta de almacenamiento de StorSimple Virtual Array aaaManage | Documentos de Microsoft
description: "Explica cómo utilizar los hello tooadd de la página de configuración del Administrador de dispositivos de StorSimple, editar, eliminar o las claves de seguridad de hello girar las credenciales de cuenta de almacenamiento asociados con hello StorSimple Virtual Array."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 234bf8bb-d5fe-40be-9d25-721d7482bc3b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: 22a0341eae0b89020065be4dbfaae77999f8be0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-storage-account-credentials-for-storsimple-virtual-array"></a>Credenciales de cuenta de almacenamiento use el Administrador de dispositivos de StorSimple toomanage de StorSimple Virtual Array

## <a name="overview"></a>Información general
Hola **configuración** sección del módulo de servicio de administrador de dispositivos de StorSimple de hello de la matriz Virtual de StorSimple presenta los parámetros de servicio global de Hola que pueden crearse en hello el servicio StorSimple Manager. Estos parámetros pueden ser aplicados tooall Hola dispositivos toohello servicio conectado e incluyen:

* Credenciales de la cuenta de almacenamiento
* Registros de control de acceso
  
  ![Panel del servicio Device Manager](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccts-dashboard.png)  

En este tutorial se explica cómo puede agregar, editar o eliminar cuentas de almacenamiento de StorSimple Virtual Array. información de Hello en este tutorial solo aplica toohello StorSimple Virtual Array. Para obtener información sobre cómo las cuentas de almacenamiento de toomanage en 8000 serie, consulte [uso Hola toomanage de servicio de StorSimple Manager su cuenta de almacenamiento](storsimple-manage-storage-accounts.md).

Cuenta de almacenamiento de credenciales de contengan credenciales de Hola que Hola dispositivo usa tooaccess su cuenta de almacenamiento con su proveedor de servicios de nube. Para las cuentas de almacenamiento de Microsoft Azure, son credenciales como nombre de la cuenta de hello y clave de acceso principal de Hola.

En hello **credenciales de la cuenta de almacenamiento** hoja, una cuenta de almacenamiento todas las credenciales que se crean para hello facturación de suscripción se muestran en formato tabular que contiene Hola siguiente información:

* **Nombre** : Hola nombre exclusivo asignado toohello cuenta cuando se creó.
* **Se ha habilitado SSL** : si hello SSL está habilitado y la comunicación de dispositivos a la nube es a través de canal seguro Hola.
  
  ![Sección de configuración](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccountcredentials-blade.png)

las tareas más comunes de Hello relacionada con las credenciales de cuenta de toostorage que se pueden realizar en hello **credenciales de la cuenta de almacenamiento** hoja son:

* Incorporación de una credencial de cuenta de almacenamiento
* Edición de una credencial de cuenta de almacenamiento
* Eliminación de una credencial de cuenta de almacenamiento

## <a name="types-of-storage-account-credentials"></a>Tipos de credenciales de cuenta de almacenamiento
Hay tres tipos de credenciales de cuentas de almacenamiento que se pueden usar con el dispositivo StorSimple.

* **Credenciales de la cuenta de almacenamiento generada automáticamente** – como sugiere su nombre hello, este tipo de credencial de la cuenta de almacenamiento se genera automáticamente cuando se crea el servicio de Hola. toolearn más información acerca de cómo se crea esta credencial de cuenta de almacenamiento, consulte [crear un nuevo servicio](storsimple-virtual-array-manage-service.md#create-a-service).
* **las credenciales de cuenta de almacenamiento en la suscripción al servicio de Hola** : se trata de cuenta de almacenamiento de Azure de hello las credenciales que están asociadas a Hola misma suscripción que el servicio de Hola. toolearn más información acerca de cómo se crean estas credenciales de cuenta de almacenamiento, consulte [sobre cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md).
* **las credenciales de cuenta de almacenamiento fuera de la suscripción al servicio Hola** : se trata de credenciales de cuenta de almacenamiento de Azure de Hola que no están asociadas con el servicio y servicio Hola existía antes probablemente se creó.

## <a name="add-a-storage-account-credential"></a>Incorporación de una credencial de cuenta de almacenamiento
Puede agregar una configuración del servicio de administrador de dispositivos de StorSimple de almacenamiento cuenta credencial tooyour proporcionando un único credenciales de acceso y nombre descriptivas que están vinculados toohello cuenta de almacenamiento. También tiene opción de Hola de habilitar Hola secure sockets layer (SSL) modo toocreate un canal seguro para la comunicación de red entre su dispositivo y hello en la nube.

Puede crear varias cuentas para un proveedor de servicios en la nube determinado. Mientras se está guardando la credencial de cuenta de almacenamiento de hello, servicio de hello intenta toocommunicate con su proveedor de servicios de nube. en este momento, se autentican las credenciales de Hola y material de acceso de Hola que ha proporcionado. Solo si Hola autenticación se realiza correctamente, se crea una credencial de cuenta de almacenamiento. Si se produce un error en la autenticación de hello, se muestra un mensaje de error adecuado.

Usar hello después de credenciales de la cuenta de almacenamiento de Azure de procedimientos tooadd:

* tooadd una credencial de cuenta de almacenamiento que tenga Hola misma suscripción de Azure como servicio de administrador de dispositivos de Hola
* tooadd una credencial de la cuenta de almacenamiento de Azure que está fuera de la suscripción al servicio de administrador de dispositivos Hola

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>tooadd una credencial de cuenta de almacenamiento que tenga Hola misma suscripción de Azure como servicio de administrador de dispositivos de Hola

1. Navegue tooyour servicio de administrador de dispositivos, seleccione y haga doble clic en él. Se abrirá hello **Introducción** hoja.
2. Seleccione **credenciales de la cuenta de almacenamiento** en hello **configuración** sección.
3. Haga clic en **Agregar**.
4. Hola **agregar una cuenta de almacenamiento** hoja, Hola siguientes:
   
    1. En **Suscripción**, seleccione **Actual**.
    2. Proporcione el nombre de saludo de la cuenta de almacenamiento de Azure.
    3. Seleccione **habilitar** toocreate un canal seguro para la comunicación de red entre la nube de hello y el dispositivo de StorSimple. Seleccione **Deshabilitar** solo si está trabajando en una nube privada.
    4. Haga clic en **Agregar**. Se le notifica una vez creada correctamente de la cuenta de almacenamiento de Hola.<br></br>
   
        ![Incorporación de una credencial de cuenta de almacenamiento existente](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

#### <a name="tooadd-an-azure-storage-account-credential-that-is-outside-of-hello-device-manager-service-subscription"></a>tooadd una credencial de la cuenta de almacenamiento de Azure que está fuera de la suscripción al servicio de administrador de dispositivos Hola

1. Navegue tooyour servicio de administrador de dispositivos, seleccione y haga doble clic en él. Se abrirá hello **Introducción** hoja.
2. Seleccione **credenciales de la cuenta de almacenamiento** en hello **configuración** sección. Esta acción muestra las credenciales de cuenta de almacenamiento existente asociadas con el servicio de administrador de dispositivos de StorSimple de hello.
3. Haga clic en **Agregar**.
4. Hola **agregar una cuenta de almacenamiento** hoja, Hola siguientes:
   
    1. En **Suscripción**, seleccione **Otro**.
   
    2. Proporcione el nombre de saludo de la credencial de la cuenta de almacenamiento de Azure.
   
    3. Hola **clave de acceso de cuenta de almacenamiento** cuadro de texto, fuente de alimentación Hola clave de acceso principal para la credencial de la cuenta de almacenamiento de Azure. tooget esta clave, vaya toohello servicio de almacenamiento de Azure, seleccione la credencial de la cuenta de almacenamiento y haga clic en **administrar claves de cuenta**. Ahora puede copiar la clave de acceso principal de Hola.
   
    4. tooenable SSL, haga clic en hello **habilitar** botón toocreate un canal seguro para la comunicación de red entre la nube de hello y servicio de administrador de dispositivos de StorSimple. Haga clic en hello **deshabilitar** botón sólo si está trabajando en una nube privada.
   
    5. Haga clic en **Agregar**. Se le notifica después de credencial de cuenta de almacenamiento de Hola se creó correctamente.

5. credencial de cuenta de almacenamiento de Hello recién creado se muestra en la hoja de servicio de StorSimple configurar el Administrador de dispositivos de hello en **credenciales de la cuenta de almacenamiento**.
   
    ![Agregar una credencial de cuenta de almacenamiento fuera de hello suscripción al servicio de administrador de dispositivos](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-outside-storageacct.png)

## <a name="edit-a-storage-account-credential"></a>Edición de una credencial de cuenta de almacenamiento
Puede editar una credencial de cuenta de almacenamiento utilizada por su dispositivo. Si edita una credencial de cuenta de almacenamiento que está actualmente en uso, Hola campos disponibles toomodify son clave de acceso de Hola y el modo SSL de Hola de credencial de cuenta de almacenamiento de Hola. Puede especificar la clave de acceso de almacenamiento nueva Hola o modificar hello **habilitar modo SSL** selección y guardar la configuración de hello actualizado.

#### <a name="tooedit-a-storage-account-credential"></a>tooedit una credencial de cuenta de almacenamiento
1. Navegue tooyour servicio de administrador de dispositivos, seleccione y haga doble clic en él. Se abrirá hello **Introducción** hoja.
2. Seleccione **credenciales de la cuenta de almacenamiento** en hello **configuración** sección. Esta acción muestra las credenciales de cuenta de almacenamiento existente asociadas con el servicio de administrador de dispositivos de StorSimple de hello.
3. En la lista tabular de Hola de credenciales de la cuenta de almacenamiento, seleccione y haga doble clic en la cuenta de hello que desea que toomodify.
4. En credencial de cuenta de almacenamiento de hello **propiedades** hoja, Hola siguientes:
   
   1. Si es necesario, puede modificar hello **habilitar SSL** selección del modo.
   2. Puede elegir tooregenerate las claves de acceso de credencial de cuenta de almacenamiento. Para obtener más información, consulte [regenerar claves de cuenta de almacenamiento de hello](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys). Proporcione la clave de credencial en la cuenta de almacenamiento de hello nueva. Para una cuenta de almacenamiento de Azure, esta es la clave de acceso principal de Hola.
   3. Haga clic en **guardar** en parte superior de Hola de hello **propiedades** configuración de hello toosave de hoja. configuración de Hola se actualiza en hello **credenciales de la cuenta de almacenamiento** hoja.
      
      ![Edición de una credencial de cuenta de almacenamiento](./media/storsimple-virtual-array-manage-storage-accounts/ova-edit-storageacct.png)

## <a name="delete-a-storage-account-credential"></a>Eliminación de una credencial de cuenta de almacenamiento
> [!IMPORTANT]
> Solo puede eliminar una credencial de cuenta de almacenamiento si no está en uso. Si una credencial de cuenta de almacenamiento está en uso, se le notificará.
> 
> 

#### <a name="toodelete-a-storage-account-credential"></a>toodelete una credencial de cuenta de almacenamiento
1. Navegue tooyour servicio de administrador de dispositivos, seleccione y haga doble clic en él. Se abrirá hello **Introducción** hoja.
2. Seleccione **credenciales de la cuenta de almacenamiento** en hello **configuración** sección. Esta acción muestra las credenciales de cuenta de almacenamiento existente asociadas con el servicio de administrador de dispositivos de StorSimple de hello.
3. En la lista tabular de Hola de credenciales de la cuenta de almacenamiento, seleccione y haga doble clic en la cuenta de hello que desea que toodelete.
4. En credencial de cuenta de almacenamiento de hello **propiedades** hoja, Hola siguientes:
   
   1. Haga clic en **eliminar** credenciales de hello toodelete.
   2. Cuando se le solicite confirmación, haga clic en **Sí** toocontinue con eliminación de Hola. lista tabular de Hello es tooreflect actualizada Hola cambios.
      
      ![Eliminación de una credencial de cuenta de almacenamiento](./media/storsimple-virtual-array-manage-storage-accounts/ova-del-storageacct.png)

## <a name="synchronizing-storage-account-credential-keys"></a>Sincronización de las claves de la credencial de cuenta de almacenamiento.
Por motivos de seguridad, la rotación de claves suele ser un requisito en los centros de datos. Un administrador de Microsoft Azure puede volver a generar o cambiar clave primaria o secundaria de hello accediendo directamente la credencial de cuenta de almacenamiento de hello (a través de Hola servicio de almacenamiento de Microsoft Azure). Hola servicio Administrador de dispositivos de StorSimple no experimenta este cambio automáticamente.

tooinform el servicio del Administrador de dispositivos de StorSimple de Hola de cambio de hello, deberá servicio de administrador de dispositivos de StorSimple de tooaccess hello, almacenamiento de Hola de acceso de credencial de cuenta y, a continuación, sincronizar clave principal o secundaria de hello (según lo que se haya cambiado). servicio de Hello, a continuación, obtiene la clave más reciente de hello, cifra las claves de Hola y envía el dispositivo de toohello clave de cifrado de Hola.

#### <a name="toosynchronize-keys-for-storage-account-credentials-in-hello-same-subscription-as-hello-service-azure-only"></a>las claves de toosynchronize las credenciales de cuenta de almacenamiento de Hola misma suscripción que el servicio de hello (solo Azure)
1. En la hoja de inicio del servicio de hello, seleccione su servicio, haga doble clic Hola nombre del servicio y, a continuación, en hello **configuración** sección, haga clic en **credenciales de la cuenta de almacenamiento**.
2. En hello **credenciales de la cuenta de almacenamiento** hoja, en hello lista de credenciales de la cuenta de almacenamiento, seleccione credencial de cuenta de almacenamiento de hello cuyas claves que desea toosynchronize.
3. Hola **propiedades** hoja para hello seleccionada credencial de la cuenta de almacenamiento, Hola siguientes:
   
    1. Haga clic en **Más** y, a continuación, haga clic en **Clave de acceso de sincronización**.
   
    2. Cuando se le solicite confirmación, haga clic en **sincronizar clave** sincronización de hello toocomplete.
    
4. Hola servicio Administrador de dispositivos de StorSimple, se necesita la clave de Hola de tooupdate que previamente se ha modificado en hello servicio de almacenamiento de Microsoft Azure. Hola **clave de cuenta de almacenamiento de sincronizar** hoja, si la clave de acceso principal de Hola se ha cambiado (regenerado), haga clic en primaria y, a continuación, haga clic en **sincronizar clave**. Si se ha cambiado la clave secundaria de hello, haga clic en **secundaria**y, a continuación, haga clic en **sincronizar clave**.
   
    ![Sincronización de la clave de acceso](./media/storsimple-virtual-array-manage-storage-accounts/ova-sync-acess-key.png)

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[administrar la matriz Virtual de StorSimple](storsimple-ova-web-ui-admin.md).

