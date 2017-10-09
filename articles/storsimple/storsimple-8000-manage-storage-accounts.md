---
title: aaaManage las credenciales de la cuenta de almacenamiento de StorSimple para dispositivos de la serie 8000 de StorSimple de Microsoft Azure | Documentos de Microsoft
description: "Explica cómo puede usar hello tooadd de la página de configuración del Administrador de dispositivos de StorSimple, editar, eliminar o las claves de seguridad de hello girar para una cuenta de almacenamiento."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 132ee46509b39db4d1b97b0f1077800a253e8da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-storage-account-credentials"></a>Usar toomanage de servicio del Administrador de dispositivos de StorSimple de hello las credenciales de cuenta de almacenamiento

## <a name="overview"></a>Información general

Hola **configuración** sección en la hoja de servicio del Administrador de dispositivos de StorSimple de hello presenta todos los parámetros de servicio global de Hola que pueden crearse en hello servicio Administrador de dispositivos de StorSimple. Estos parámetros pueden ser aplicados tooall Hola dispositivos toohello servicio conectado e incluyen:

* Credenciales de la cuenta de almacenamiento
* Plantillas de ancho de banda 
* Registros de control de acceso 

Este tutorial le explica cómo tooadd, modificar o eliminar las credenciales de cuenta de almacenamiento o rotar claves de seguridad de Hola para una cuenta de almacenamiento.

 ![Lista de credenciales de cuenta de almacenamiento](./media/storsimple-8000-manage-storage-accounts/createnewstorageacct6.png)  

Las cuentas de almacenamiento contienen credenciales de Hola que Hola tooaccess de usos de dispositivo de StorSimple en su cuenta de almacenamiento con su proveedor de servicios de nube. Para las cuentas de almacenamiento de Microsoft Azure, son credenciales como nombre de la cuenta de hello y clave de acceso principal de Hola. 

En hello **credenciales de la cuenta de almacenamiento** hoja, todo el almacenamiento de las cuentas que se crean para hello facturación de suscripción se muestran en formato tabular que contiene Hola siguiente información:

* **Nombre** : Hola nombre exclusivo asignado toohello cuenta cuando se creó.
* **Se ha habilitado SSL** : si hello SSL está habilitado y la comunicación de dispositivos a la nube es a través de canal seguro Hola.
* **Utilizado por** : Hola número de volúmenes que usan la cuenta de almacenamiento de Hola.

Hola más comunes las tareas relacionadas toostorage cuentas que se pueden realizar son:

* Agregar una cuenta de almacenamiento 
* Editar una cuenta de almacenamiento 
* Eliminar una cuenta de almacenamiento 
* Rotación de claves de cuentas de almacenamiento 

## <a name="types-of-storage-accounts"></a>Tipos de cuentas de almacenamiento

Hay tres tipos de cuentas de almacenamiento que se pueden usar con el dispositivo StorSimple.

* **Las cuentas de almacenamiento generada automáticamente** – como sugiere su nombre hello, este tipo de cuenta de almacenamiento se genera automáticamente cuando se crea el servicio de Hola. toolearn más información acerca de cómo se crea esta cuenta de almacenamiento, consulte [paso 1: crear un nuevo servicio](storsimple-8000-deployment-walkthrough-u2.md#step-1-create-a-new-service) en [implementar el dispositivo de StorSimple local](storsimple-8000-deployment-walkthrough-u2.md). 
* **Cuentas de almacenamiento en la suscripción al servicio Hola** : estas son cuentas de almacenamiento de Azure de Hola que están asociadas con hello misma suscripción que el servicio de Hola. toolearn más información acerca de cómo se crean estas cuentas de almacenamiento, consulte [sobre cuentas de almacenamiento de Azure](../storage/common/storage-create-storage-account.md). 
* **Las cuentas de almacenamiento fuera de la suscripción al servicio Hola** : estas son cuentas de almacenamiento de Azure de Hola que no están asociadas con el servicio y servicio de hello existía antes probablemente se creó.

## <a name="add-a-storage-account"></a>Agregar una cuenta de almacenamiento

Puede agregar una cuenta de almacenamiento proporcionando un único credenciales de acceso y nombre descriptivas que están vinculados toohello cuenta de almacenamiento (con el proveedor de servicios de nube especificado de hello). También tiene opción de Hola de habilitar Hola secure sockets layer (SSL) modo toocreate un canal seguro para la comunicación de red entre su dispositivo y hello en la nube.

Puede crear varias cuentas para un proveedor de servicios en la nube determinado. Tenga en cuenta, sin embargo, que después de crea una cuenta de almacenamiento, no se puede cambiar el proveedor de servicios de nube de Hola.

Mientras se está guardando la cuenta de almacenamiento de hello, servicio de hello intenta toocommunicate con su proveedor de servicios de nube. las credenciales de Hola y material de acceso de Hola que ha proporcionado se autenticarán en este momento. Solo si Hola autenticación se realiza correctamente, se crea una cuenta de almacenamiento. Si se produce un error en la autenticación de hello, se mostrará un mensaje de error adecuado.

Usar hello después de credenciales de la cuenta de almacenamiento de Azure de procedimientos tooadd:

* tooadd una credencial de cuenta de almacenamiento que tenga Hola misma suscripción de Azure como servicio de administrador de dispositivos de Hola
* tooadd una credencial de la cuenta de almacenamiento de Azure que está fuera de la suscripción al servicio de administrador de dispositivos Hola

[!INCLUDE [add-a-storage-account-update2](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

#### <a name="tooadd-an-azure-storage-account-credential-outside-of-hello-storsimple-device-manager-service-subscription"></a>tooadd una credencial de la cuenta de almacenamiento de Azure fuera de la suscripción al servicio de administrador de dispositivos de StorSimple Hola

1. Navegue tooyour servicio de administrador de dispositivos de StorSimple, seleccione y haga doble clic en él. Se abrirá hello **Introducción** hoja.
2. Seleccione **credenciales de la cuenta de almacenamiento** en hello **configuración** sección. Esta acción muestra las credenciales de cuenta de almacenamiento existente asociadas con el servicio de administrador de dispositivos de StorSimple de hello.
3. Haga clic en **Agregar**.
4. Hola **agregar una credencial de cuenta de almacenamiento** hoja, Hola siguientes:
   
    1. En **Suscripción**, seleccione **Otro**.
   
    2. Proporcione el nombre de saludo de la credencial de la cuenta de almacenamiento de Azure.
   
    3. Hola **clave de acceso de cuenta de almacenamiento** cuadro de texto, fuente de alimentación Hola clave de acceso principal para la credencial de la cuenta de almacenamiento de Azure. tooget esta clave, vaya toohello servicio de almacenamiento de Azure, seleccione la credencial de la cuenta de almacenamiento y haga clic en **administrar claves de cuenta**. Ahora puede copiar la clave de acceso principal de Hola.
   
    4. tooenable SSL, haga clic en hello **habilitar** botón toocreate un canal seguro para la comunicación de red entre la nube de hello y servicio de administrador de dispositivos de StorSimple. Haga clic en hello **deshabilitar** botón sólo si está trabajando en una nube privada.
   
    5. Haga clic en **Agregar**. Se le notifica después de credencial de cuenta de almacenamiento de Hola se creó correctamente.

5. credencial de cuenta de almacenamiento de Hello recién creado se muestra en la hoja de servicio de StorSimple configurar el Administrador de dispositivos de hello en **credenciales de la cuenta de almacenamiento**.
   


## <a name="edit-a-storage-account"></a>Editar una cuenta de almacenamiento

Puede editar una cuenta de almacenamiento usada por un contenedor de volúmenes. Si edita una cuenta de almacenamiento que está actualmente en uso, hello solo campo disponible toomodify es Hola tecla de acceso para la cuenta de almacenamiento de Hola. Puede proporcionar la nueva clave de acceso de almacenamiento hello y guardar la configuración de hello actualizado.

#### <a name="tooedit-a-storage-account"></a>tooedit una cuenta de almacenamiento

1. Servicio de administrador de dispositivos de StorSimple de tooyour go. Hola **configuración** sección, haga clic en **credenciales de la cuenta de almacenamiento**.

    ![Credenciales de la cuenta de almacenamiento](./media/storsimple-8000-manage-storage-accounts/editstorageacct1.png)

2. Hola **credenciales de la cuenta de almacenamiento** hoja, en lista de Hola de credenciales de cuenta de almacenamiento, seleccionadas y haga clic en uno que se va tooedit Hola. 

3. Puede modificar hello **habilitar SSL** selección. También puede hacer clic en **más...**  y, a continuación, seleccione **toorotate clave de acceso de sincronización** las claves de acceso de la cuenta de almacenamiento. Vaya demasiado[rotación de las cuentas de almacenamiento de claves](#key-rotation-of-storage-accounts) para obtener más información sobre cómo tooperform rotación de claves. Una vez que haya modificado la configuración de hello, haga clic en **guardar**. 

    ![Guardar credenciales de la cuenta de almacenamiento editada](./media/storsimple-8000-manage-storage-accounts/editstorageacct3.png)

4. Cuando se le pida confirmación, haga clic en **Sí**. 

    ![Confirmar modificaciones](./media/storsimple-8000-manage-storage-accounts/editstorageacct4.png)

configuración de Hola se actualiza y se guardan para su cuenta de almacenamiento. 

## <a name="delete-a-storage-account"></a>Eliminar una cuenta de almacenamiento

> [!IMPORTANT]
> Puede eliminar una cuenta de almacenamiento solo si no la usa un contenedor de volúmenes. Si se utiliza una cuenta de almacenamiento por un contenedor de volumen, primero elimine contenedor de volúmenes de hello y, a continuación, eliminar cuenta de almacenamiento de hello asociado.

#### <a name="toodelete-a-storage-account"></a>toodelete una cuenta de almacenamiento

1. Servicio de administrador de dispositivos de StorSimple de tooyour go. Hola **configuración** sección, haga clic en **credenciales de la cuenta de almacenamiento**.

2. En la lista tabular de Hola de cuentas de almacenamiento, mantenga el mouse sobre la cuenta de hello que desea toodelete. Haga clic en el menú contextual de tooinvoke hello y haga clic en **eliminar**.

    ![Eliminar credenciales de la cuenta de almacenamiento](./media/storsimple-8000-manage-storage-accounts/deletestorageacct1.png)

3. Cuando se le solicite confirmación, haga clic en **Sí** toocontinue con eliminación de Hola. lista tabular de Hello estará actualizada tooreflect Hola cambios.

    ![Confirmar eliminación](./media/storsimple-8000-manage-storage-accounts/deletestorageacct2.png)

## <a name="key-rotation-of-storage-accounts"></a>Rotación de claves de cuentas de almacenamiento

Por motivos de seguridad, la rotación de claves suele ser un requisito en los centros de datos. Cada suscripción de Microsoft Azure puede tener una o más cuentas de almacenamiento asociadas. cuentas de Hello acceso toothese se controla mediante la suscripción de Hola y teclas de acceso para cada cuenta de almacenamiento. 

Cuando se crea una cuenta de almacenamiento, Microsoft Azure genera dos claves de acceso de almacenamiento de 512 bits que se utilizan para la autenticación cuando se tiene acceso a la cuenta de almacenamiento de Hola. Tener dos claves de acceso de almacenamiento permite las claves de hello tooregenerate con ningún servicio de almacenamiento de tooyour de interrupción o un servicio de toothat de acceso. clave que está actualmente en uso Hello es hello *principal* hello y clave clave copia de seguridad es que se hace referencia tooas hello *secundaria* clave. Una de estas dos claves debe suministrarse cuando el dispositivo de Microsoft Azure StorSimple tiene acceso a su proveedor de servicios de almacenamiento en la nube.

## <a name="what-is-key-rotation"></a>¿Qué es la rotación de claves?

Por lo general, aplicaciones usan solo una de hello claves tooaccess los datos. Después de un determinado período de tiempo, puede tener sus aplicaciones cambiar clave de segundo toousing Hola. Después de que haya cambiado la clave secundaria de toohello de aplicaciones, puede retirar la primera clave de hello y, a continuación, genere una nueva clave. Mediante Hola dos claves de esta forma permite que los datos de toohello de acceso de las aplicaciones sin tiempo de inactividad.

claves de cuenta de almacenamiento de Hello siempre se almacenan en el servicio de hello en un formato cifrado. Sin embargo, se puede restablecer mediante Hola servicio Administrador de dispositivos de StorSimple. servicio de Hello puede obtener la clave principal de Hola y clave secundaria para todos Hola cuentas de almacenamiento de hello genera la misma suscripción, incluidas las cuentas creadas en el servicio de almacenamiento de hello, así como cuentas de almacenamiento predeterminadas de Hola Hola cuando el Administrador de dispositivos StorSimple primero se creó el servicio. Hola servicio Administrador de dispositivos de StorSimple siempre obtendrá estas claves de hello portal de Azure clásico y, a continuación, almacenarlos de forma cifrada.

## <a name="rotation-workflow"></a>Flujo de trabajo de rotación

Un administrador de Microsoft Azure puede volver a generar o cambiar clave primaria o secundaria de hello tengan acceso directo a la cuenta de almacenamiento de hello (a través de Hola servicio de almacenamiento de Microsoft Azure). Hola servicio Administrador de dispositivos de StorSimple no experimenta este cambio automáticamente.

servicio de administrador de dispositivos de StorSimple de hello tooinform de cambio de hello, necesitará tooaccess servicio de administrador de dispositivos de StorSimple de hello, tener acceso a la cuenta de almacenamiento de hello y, a continuación, sincronizar clave principal o secundaria de hello (según lo que se haya cambiado). servicio de Hello, a continuación, obtiene la clave más reciente de hello, cifra las claves de Hola y envía el dispositivo de toohello clave de cifrado de Hola.

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service"></a>las claves de toosynchronize para cuentas de almacenamiento de Hola misma suscripción que el servicio de Hola 
1. Servicio de administrador de dispositivos de StorSimple de tooyour go. Hola **configuración** sección, haga clic en **credenciales de la cuenta de almacenamiento**.
2. En la lista tabular de Hola de cuentas de almacenamiento, haga clic en hello uno que desea toomodify. 

    ![sincronizar claves](./media/storsimple-8000-manage-storage-accounts/syncaccesskey1.png)

3. Haga clic en **... Más** y, a continuación, seleccione **toorotate clave de acceso de sincronización**.   

    ![sincronizar claves](./media/storsimple-8000-manage-storage-accounts/syncaccesskey2.png)

4. Hola servicio Administrador de dispositivos de StorSimple, se necesita la clave de Hola de tooupdate que previamente se ha modificado en hello servicio de almacenamiento de Microsoft Azure. Si la clave de acceso principal de Hola se ha cambiado (regenerado), seleccione **principal** clave. Si se ha cambiado la clave secundaria de hello, seleccione **secundaria** clave. Haga clic en **Sincronizar clave**.
      
      ![sincronizar claves](./media/storsimple-8000-manage-storage-accounts/syncaccesskey3.png)

Se le notificará una vez clave Hola correctamente sycnhronized.

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a>claves de toosynchronize las cuentas de almacenamiento fuera de la suscripción al servicio Hola
1. En hello **servicios** página, haga clic en hello **configurar** ficha.
2. Haga clic en **Agregar/editar cuentas de almacenamiento**.
3. En el cuadro de diálogo de Hola Hola siguientes:
   
   1. Seleccione la cuenta de almacenamiento de hello con clave de acceso de Hola que desea tooupdate.
   2. Necesitará la clave de acceso de almacenamiento tooupdate Hola Hola servicio Administrador de dispositivos de StorSimple. En este caso, puede ver la clave de acceso de almacenamiento de Hola. Escriba una clave nueva Hola Hola **clave de acceso de cuenta de almacenamiento** cuadro. 
   3. Guarde los cambios. Ahora debería estar actualizada la clave de acceso de la cuenta de almacenamiento.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información acerca de la [Seguridad de StorSimple](storsimple-8000-security.md).
* Obtenga más información sobre [utilizando Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

