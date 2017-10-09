---
title: Hola aaaDeploy servicio de administrador de dispositivos de StorSimple de Azure | Documentos de Microsoft
description: "Explica cómo toocreate y delete Hola servicio Administrador de dispositivos de StorSimple en hello portal de Azure y se describe cómo toomanage Hola clave de registro del servicio."
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
ms.date: 07/13/2017
ms.author: alkohli
ms.openlocfilehash: b84a907d6b735c8fee7bdc51f9c0074857297d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-8000-series-devices"></a>Implementación de servicio de administrador de dispositivos de StorSimple de Hola para dispositivos de la serie 8000 de StorSimple

## <a name="overview"></a>Información general

Hola servicio Administrador de dispositivos de StorSimple se ejecuta en Microsoft Azure y conecta a los dispositivos de StorSimple toomultiple. Después de crear el servicio de hello, utilizarla toomanage todos los dispositivos de hello toohello conectado el Administrador de dispositivos de StorSimple de servicio desde una única ubicación central, con lo que se minimiza el trabajo administrativo.

Este tutorial describen los pasos de hello necesarios para la creación de hello, eliminación, migración del servicio de Hola y la administración de Hola de clave de registro del servicio de Hola. información de Hello contenida en este artículo es aplicable solo tooStorSimple 8000 series los dispositivos. Para obtener más información sobre arreglos de discos virtuales de StorSimple, vaya demasiado[implementar un servicio de administrador de dispositivos de StorSimple para la matriz Virtual de StorSimple](storsimple-virtual-array-manage-service.md).

## <a name="create-a-service"></a>Crear un servicio
toocreate un servicio de administrador de dispositivos de StorSimple, necesita toohave:

* Una suscripción con un contrato Enterprise
* Una cuenta de Almacenamiento de Microsoft Azure activa.
* Hola información de facturación que se usa para la administración de acceso

Se permiten solo Hola suscripciones con un contrato Enterprise. No se admiten las suscripciones de Microsoft Sponsorship que permiten Hola portal de Azure clásico en hello portal de Azure. Verá Hola sigue el mensaje cuando se usa una suscripción no admitida:

![La suscripción no es válida](./media/storsimple-8000-manage-service/subscription-not-valid.jpg)

También puede elegir toogenerate en una cuenta de almacenamiento de forma predeterminada cuando se crea el servicio de Hola.

Un único servicio puede administrar varios dispositivos. Sin embargo, un dispositivo no puede abarcar varios servicios. Una gran empresa puede tener varios toowork de instancias de servicio con distintas suscripciones, organizaciones o incluso regiones de implementación. 

> [!NOTE]
> Necesita instancias independientes de los dispositivos serie 8000 de StorSimple toomanage del servicio de administrador de dispositivos de StorSimple y arreglos de discos virtuales de StorSimple.

Realizar Hola siguiendo los pasos toocreate un servicio.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]


Para cada servicio de administrador de dispositivos de StorSimple, existe Hola siguientes atributos:

* **Nombre** : nombre de Hola que se asignó el servicio de administrador de dispositivos de StorSimple de tooyour cuando se creó. **no se puede cambiar el nombre del servicio Hola después de crear el servicio de Hola. Esto también es cierto para otras entidades como dispositivos, volúmenes, contenedores de volúmenes y las directivas de copia de seguridad que no se pueden cambiar en hello portal de Azure.**
* **Estado** : Hola estado del servicio de hello, que puede ser **Active**, **crear**, o **Online**.
* **Ubicación** : Hola ubicación geográfica en qué hello StorSimple se implementará el dispositivo.
* **Suscripción** : hello suscripción que está asociado con el servicio de facturación.

## <a name="move-a-service-tooazure-portal"></a>Mover un portal tooAzure
Serie StorSimple 8000 puede administrarse ahora Hola portal de Azure. Si tiene un servicio toomanage hello StorSimple los dispositivos existentes, se recomienda que mueva su toohello service portal de Azure. Hola portal de Azure clásico para hello el servicio StorSimple Manager no está disponible después del 30 de septiembre de 2017.

Hola opción toomigrate toohello portal de Azure está disponible en fases. Si no ve un portal de opción toomigrate tooAzure pero desea toomove y ha revisado el impacto de saludo de la migración como se documenta en hello [consideraciones para transición](#considerations-for-transition), también puede [enviar una solicitud de](https://aka.ms/ss8000-cx-signup).

### <a name="considerations-for-transition"></a>Consideraciones sobre la transición

Revisar el impacto de Hola de migración toohello nuevo portal de Azure antes de continuar servicio Hola.

#### <a name="before-you-transition"></a>Antes de realizar la transición

* El dispositivo ejecuta la versión Update 3.0 o posterior. Si el dispositivo está ejecutando una versión anterior, instale las actualizaciones más recientes de Hola. Para obtener más información, consulte demasiado[instalar Update 4](storsimple-8000-install-update-4.md). Si usa StorSimple Cloud Appliance (8010/8020), cree una aplicación de nube con la actualización 4.0. 

* Una vez haya toohello transición nuevo portal de Azure, no puede usar hello Azure toomanage portal clásico en el dispositivo StorSimple.

* transición de Hello es no provocan interrupciones y no hay ningún tiempo de inactividad para el dispositivo de Hola.

* Todos los administradores de dispositivos de StorSimple de hello en hello especificado se realiza la transición de suscripción.

#### <a name="during-hello-transition"></a>Durante la transición de Hola

* No puede administrar el dispositivo desde el portal de Hola.
* Por ejemplo, las copias de seguridad programadas y niveles continúan toooccur.
* No elimine Hola antiguos administradores de dispositivos de StorSimple mientras se realiza la transición de Hola.

#### <a name="after-hello-transition"></a>Después de la transición de Hola

* Ya no puede administrar los dispositivos desde portal clásico de Hola.

* no se admiten los cmdlets de PowerShell de administración de servicio de Azure (ASM) existentes de Hola. Actualizar toomanage de secuencias de comandos de hello en los dispositivos a través de hello Azure Resource Manager.

* Se conserva la configuración del servicio y el dispositivo. Todos los volúmenes y las copias de seguridad también son transición toohello portal de Azure.

### <a name="begin-transition"></a>Iniciar la transición

Realizar Hola siguiendo los pasos tootransition el toohello service portal de Azure.

1. Vaya tooyour el servicio StorSimple Manager existente en el portal clásico de Hola.

2. Verá una notificación que le informa de que el servicio de administrador de dispositivos de StorSimple de hello ahora está disponible en hello portal de Azure. Tenga en cuenta que en hello portal de Azure, servicio de hello tooas que se hace referencia el servicio de administrador de dispositivos de StorSimple.

    ![Notificación de la migración](./media/storsimple-8000-manage-service/service-transition1.jpg)

    1. Asegúrese de que ha revisado las consecuencias de Hola de migración.
    2. Revise la lista de Hola de administradores de dispositivos de StorSimple que se va a mover desde portal clásico de Hola.

3. Haga clic en **Migrar**. transición de Hello comienza y toma toocomplete unos minutos.

Una vez completada la transición de hello, puede administrar los dispositivos a través de hello servicio Administrador de dispositivos de StorSimple en hello portal de Azure.

En hello portal de Azure, solo Hola dispositivos StorSimple ejecuta Update 3.0 y versiones posteriores se admiten. dispositivos de Hola que ejecutan versiones anteriores tienen compatibilidad limitada. Hola después summrizes tabla qué operaciones se admiten en dispositivo Hola ejecutando versios anterior tooUpdate 3.0, una vez que se migraron de hello clásico toohello portal de Azure.

| Operación                                                                                                                       | Compatible      |
|---------------------------------------------------------------------------------------------------------------------------------|----------------|
| Registrar un dispositivo                                                                                                               | Sí            |
| Configurar opciones de dispositivo como generales, de red y de seguridad                                                                | Sí            |
| Buscar, descargar e instalar actualizaciones                                                                                             | Sí            |
| Desactivar un dispositivo                                                                                                               | Sí            |
| Eliminar un dispositivo                                                                                                                   | Sí            |
| Crear, modificar y eliminar un contenedor de volúmenes                                                                                   | No             |
| Crear, modificar y eliminar un volumen                                                                                             | No             |
| Crear, modificar y eliminar una directiva de copia de seguridad                                                                                      | No             |
| Creación de una copia de seguridad manual                                                                                                            | No             |
| Realizar una copia de seguridad programada                                                                                                         | No aplicable |
| Restaurar desde un conjunto de copias de seguridad                                                                                                        | No             |
| Clonar dispositivo tooa ejecuta Update 3.0 y versiones posteriores <br> dispositivo de origen de Hola está ejecutando la versión anterior tooUpdate 3.0.                                | Sí            |
| Clonar dispositivo tooa ejecutando versiones anteriores tooUpdate 3.0                                                                          | No             |
| Conmutación por error como dispositivo de origen <br> (desde un dispositivo ejecutando versiones anteriores tooUpdate 3.0 tooa dispositivo ejecuta Update 3.0 y versiones posteriores)                                                               | Sí            |
| Conmutación por error como dispositivo de destino <br> (dispositivo de tooa ejecutando software de versión anterior tooUpdate 3.0)                                                                                   | No             |
| Desactivar una alerta                                                                                                                  | Sí            |
| Ver las directivas de copia de seguridad, el catálogo de copias de seguridad, volúmenes, contenedores de volúmenes, gráficos de supervisión, trabajos y alertas creadas en el Portal clásico | Sí            |
| Activar y desactivar los controladores de dispositivo                                                                                              | Sí            |


## <a name="delete-a-service"></a>Eliminar un servicio

Antes de eliminar un servicio, asegúrese de que no lo esté utilizando ningún dispositivo conectado. Si el servicio de hello está en uso, desactive los dispositivos de hello conectado. Hola desactivar la operación se Hola conexión entre el dispositivo de Hola y el servicio de hello, pero conserva los datos del dispositivo hello en la nube de Hola.

> [!IMPORTANT]
> Después de elimina un servicio, no se puede revertir la operación de Hola. Cualquier dispositivo que estaba utilizando el servicio de hello necesita toobe restablecer toofactory los valores predeterminados antes de que se puede utilizar con otro servicio. En este escenario, los datos locales de hello en dispositivo hello, así como la configuración de hello, se pierde.

Realizar Hola siguiendo los pasos toodelete un servicio.

### <a name="toodelete-a-service"></a>toodelete un servicio

1. Búsqueda para el servicio de hello desea toodelete. Haga clic en **recursos** icono y, a continuación, entrada Hola toosearch términos adecuado. En los resultados de búsqueda de hello, haga clic en servicio de Hola que desee toodelete.

    ![Toodelete de servicio de búsqueda](./media/storsimple-8000-manage-service/deletessdevman1.png)

2. Esto le llevará el módulo de servicio del Administrador de dispositivos de StorSimple de toohello. Hacer clic en **Eliminar**.

    ![Eliminar servicio](./media/storsimple-8000-manage-service/deletessdevman2.png)

3. Haga clic en **Sí** en la notificación de confirmación de Hola. Puede tardar unos minutos para hello servicio toobe eliminado.

    ![Confirmar eliminación](./media/storsimple-8000-manage-service/deletessdevman3.png)

## <a name="get-hello-service-registration-key"></a>Obtener clave de registro del servicio de Hola

Después de haber creado correctamente un servicio, deberá tooregister el dispositivo StorSimple con el servicio de Hola. tooregister el primer dispositivo de StorSimple, se necesita Hola clave de registro del servicio. tooregister dispositivos adicionales con un servicio existente de StorSimple, necesitará clave de registro de hello y clave de cifrado de datos de servicio de hello (que se genera en el primer dispositivo de Hola durante el registro). Para obtener más información acerca de la clave de cifrado de datos del servicio de hello, consulte [seguridad de StorSimple](storsimple-8000-security.md). Puede obtener clave de registro de hello, acceda a **claves** en la hoja de administrador de dispositivos de StorSimple.

Realizar Hola después de la clave de registro del servicio de pasos tooget Hola.

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

Mantenga la clave de registro del servicio de hello en una ubicación segura. Necesitará esta clave, así como clave de cifrado de datos del servicio de hello, tooregister dispositivos adicionales con este servicio. Después de obtener la clave de registro del servicio de hello, debe configurar el dispositivo a través de hello Windows PowerShell para StorSimple interfaz.

Para obtener más información acerca de cómo toouse esta clave, consulte el registro [paso 3: Configure y registre el dispositivo de Hola a través de Windows PowerShell para StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-hello-service-registration-key"></a>Regenerar la clave de registro del servicio de Hola
Debe tooregenerate una clave de registro del servicio si es necesario tooperform rotación de claves o si ha cambiado la lista de Hola de administradores de servicios. Cuando vuelva a generar clave de hello, nueva clave de Hola se usa solo para registrar dispositivos subsiguientes. dispositivos de Hola que ya estaban registrados no se ven afectados por este proceso.

Realizar Hola siguiendo los pasos tooregenerate una clave de registro del servicio.

### <a name="tooregenerate-hello-service-registration-key"></a>clave de registro del servicio de tooregenerate Hola
1. Hola **el Administrador de dispositivos de StorSimple** hoja, vaya demasiado**administración &gt;**  **claves**.
    
    ![Hoja de claves](./media/storsimple-8000-manage-service/regenregkey2.png)

2. Hola **claves** hoja, haga clic en **regenerar**.

    ![Haga clic en Regenerar](./media/storsimple-8000-manage-service/regenregkey3.png)
3. Hola **Regenerar clave de registro** hoja, revisión Hola requiere una acción cuando hello se vuelven a generar las claves. Todos los dispositivos subsiguientes Hola que están registrados con este servicio usan nueva clave de registro de hello. Haga clic en **regenerar** tooconfirm. Se le notifica una vez completada la regeneración de Hola.

    ![Confirmar regeneración](./media/storsimple-8000-manage-service/regenregkey4.png)

4. Aparecerá una nueva clave de registro de servicio.

5. Copie esta clave y guárdela para registrar los dispositivos nuevos con este servicio.



## <a name="change-hello-service-data-encryption-key"></a>Cambiar la clave de cifrado de datos del servicio de Hola
Claves de cifrado de datos de servicio son tooencrypt usado cliente confidencial datos, como las credenciales de cuenta de almacenamiento, que se envían desde el dispositivo de StorSimple de toohello de servicio de StorSimple Manager. Necesitará toochange estas claves periódicamente si su organización de TI tiene una directiva de rotación de claves en dispositivos de almacenamiento de Hola. Hello proceso de cambio de clave puede ser ligeramente diferente dependiendo de si hay un único dispositivo o varios dispositivos administrados por el servicio StorSimple Manager Hola. Para obtener más información, consulte demasiado[StorSimple seguridad y protección de datos](storsimple-8000-security.md).

Cambiar clave de cifrado de datos de servicio de hello es un proceso de 3 pasos:

1. Usar scripts de Windows PowerShell para el Administrador de recursos de Azure, autorizar una clave de cifrado de datos de servicio de dispositivo toochange Hola.
2. Uso de Windows PowerShell para StorSimple, iniciar el cambio de clave de cifrado de datos de servicio de Hola.
3. Si tiene más de un dispositivo de StorSimple, actualizar clave de cifrado de datos de servicio de hello en hello otros dispositivos.

### <a name="step-1-use-windows-powershell-script-tooauthorize-a-device-toochange-hello-service-data-encryption-key"></a>Paso 1: Usar Windows PowerShell script tooAuthorize una clave de cifrado de datos de servicio de dispositivo toochange Hola
Por lo general, Administrador de dispositivos de hello solicitará que Administrador de servicio de hello autorizar un claves de cifrado de datos del servicio de toochange de dispositivo. Administrador de servicios de Hello autorizará, a continuación, una clave de hello dispositivos toochange Hola.

Este paso se realiza mediante script de Hola según el Administrador de recursos de Azure. Administrador de servicios de Hello puede seleccionar un dispositivo elegible toobe autorizado. dispositivo de Hello es, a continuación, el proceso de cambio de clave de cifrado de datos del servicio de toostart autorizados Hola. 

Para obtener más información sobre el uso de script de Hola, vaya demasiado[Authorize ServiceEncryptionRollover.ps1](https://github.com/anoobbacker/storsimpledevicemgmttools/blob/master/Authorize-ServiceEncryptionRollover.ps1)

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>¿Los dispositivos que pueden autorizarse claves de cifrado de datos de servicio de toochange?
Un dispositivo debe cumplir Hola siguiendo criterios antes de cambios de clave de cifrado de datos de servicio de tooinitiate autorizados:

* dispositivo de Hello debe estar en línea toobe apto para la autorización de cambio de clave de cifrado de datos de servicio.
* Puede autorizar Hola mismo dispositivo nuevo después de 30 minutos si el cambio de la clave de hello no haya iniciado.
* Puede autorizar a un dispositivo distinto, siempre que no ha iniciado cambio de clave de hello hello de dispositivo autorizado anteriormente. Después de que se ha autorizado el nuevo dispositivo de hello, dispositivo antiguo de hello no puede iniciar el cambio de Hola.
* No se puede autorizar a un dispositivo mientras está en curso Hola sustitución de la clave de cifrado de datos del servicio de Hola.
* Puede autorizar a un dispositivo cuando algunos de los dispositivos de hello registrados con el servicio de Hola han sustituido el cifrado Hola mientras que otros no. 

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>Paso 2: Usar Windows PowerShell para el cambio clave del cifrado de datos de StorSimple tooinitiate Hola servicio
Este paso se realiza en hello Windows PowerShell para StorSimple interfaz en hello había autorizado dispositivo StorSimple.

> [!NOTE]
> Puede realizarse ninguna operación en hello portal de Azure de su servicio StorSimple Manager hasta que se complete la sustitución de claves de Hola.
> 
> 

Si usas la interfaz de Windows PowerShell de hello dispositivo consola serie tooconnect toohello, realizar Hola pasos.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>cambiar la clave de cifrado de datos del servicio de tooinitiate Hola
1. Seleccione la opción 1 toolog en con acceso completo.
2. En hello símbolo del sistema, escriba:
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Una vez Hola cmdlet se haya completado correctamente, obtendrá una nueva clave de cifrado de datos del servicio. Copie y guarde esta clave para usarla en el paso 3 de este proceso. Esta clave será usa tooupdate Hola todos los restantes dispositivos registrados con el servicio StorSimple Manager Hola.
   
   > [!NOTE]
   > Este proceso debe iniciarse en las cuatro horas siguientes a la autorización de un dispositivo de StorSimple.
   > 
   > 
   
   Esta nueva clave, a continuación, se envía toohello servicio toobe insertada tooall Hola los dispositivos que están registrados con el servicio de Hola. A continuación, aparecerá una alerta en panel de servicio de Hola. servicio de Hola se deshabilitará todas las operaciones de hello en los dispositivos de hello registrado y Administrador de dispositivos de hello deberá, a continuación, clave de cifrado de datos de servicio de tooupdate hello en hello otros dispositivos. Sin embargo, hello E/s (hosts que envían datos en la nube toohello) no se interrumpirán.
   
   Si tiene un único dispositivo registrado servicio tooyour, proceso de sustitución de hello ahora está completa y puede omitir el paso siguiente de Hola. Si tiene varios dispositivos registrados tooyour servicio, continúe toostep 3.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>Paso 3: Actualizar la clave de cifrado de datos de servicio de hello en otros dispositivos de StorSimple
Estos pasos deben realizarse en la interfaz de Windows PowerShell de hello del dispositivo StorSimple si tiene varios dispositivos registrados tooyour el servicio StorSimple Manager. clave de Hola que obtuvo en el paso 2 debe ser usado tooupdate todos Hola restantes registrado con el servicio StorSimple Manager hello de dispositivo de StorSimple.

Realizar Hola siguiendo el cifrado de datos de servicio de pasos tooupdate hello en el dispositivo.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>clave de cifrado de datos del servicio de tooupdate Hola
1. Usar Windows PowerShell para StorSimple tooconnect toohello consola. Seleccione la opción 1 toolog en con acceso completo.
2. En hello símbolo del sistema, escriba:
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Proporcione la clave de cifrado de datos de servicio de Hola que obtuvo en [paso 2: usar Windows PowerShell para el cambio clave del cifrado de datos de StorSimple tooinitiate Hola servicio](#to-initiate-the-service-data-encryption-key-change).


## <a name="next-steps"></a>Pasos siguientes
* Obtener más información sobre hello [proceso de implementación de StorSimple](storsimple-8000-deployment-walkthrough-u2.md).
* Obtenga más información sobre cómo [administrar su cuenta de almacenamiento de StorSimple](storsimple-8000-manage-storage-accounts.md).
* Más información acerca de cómo demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).
