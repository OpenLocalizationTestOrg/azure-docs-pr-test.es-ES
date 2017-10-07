---
title: "dispositivos con el Administrador de instantáneas de StorSimple de aaaManage | Documentos de Microsoft"
description: "Describe cómo toouse Hola instantáneas de StorSimple Manager MMC complemento tooconnect y administrar dispositivos de StorSimple."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 966ecbe3-a7fa-4752-825f-6694dd949946
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 7a2a2ca830e4ea6eb4b01f2542958df3871c1700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooconnect-and-manage-storsimple-devices"></a>Use el Administrador de instantáneas StorSimple tooconnect y administrar dispositivos de StorSimple
## <a name="overview"></a>Información general
Puede usar los nodos en hello Administrador de instantáneas StorSimple **ámbito** panel tooverify importa los datos del dispositivo StorSimple y actualizar los dispositivos de almacenamiento conectados. Además, al hacer clic en hello **dispositivos** nodo, puede ver una lista de dispositivos conectados y la información de estado correspondiente en hello **resultados** panel.

![Dispositivos conectados](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_connect_devices.png)

**Ilustración 1: Dispositivo conectado a Administrador de instantáneas StorSimple** 

En función de su **vista** selecciones, hello **resultados** panel muestra hello después de obtener información acerca de cada dispositivo. (Para obtener más información acerca de cómo configurar una vista, vaya demasiado[menú Ver](storsimple-use-snapshot-manager.md#view-menu).

| Columna Resultados | Descripción |
|:--- |:--- |
| Nombre |nombre de Hello de dispositivo de hello como está configurado en hello portal de Azure clásico |
| Modelo |número de modelo de Hello de dispositivo de Hola |
| Versión |versión de Hola de software de hello instalado en el dispositivo de Hola |
| Estado |Si el dispositivo de hello está disponible |
| Última sincronización |Fecha y hora cuando se sincronizó por última vez el dispositivo de Hola |
| Nº de serie |número de serie de Hello de dispositivo de Hola |

Si hace doble clic en hello **dispositivos** nodo Hola **ámbito** panel, puede seleccionar de hello siguientes acciones:

* Incorporación o remplazo de un dispositivo
* Conexión de un dispositivo y comprobación de las importaciones
* Actualización de los dispositivos conectados

Si hace clic en hello **dispositivos** nombre de nodo y, a continuación, haga un dispositivo en hello **resultados** panel, puede seleccionar de hello siguientes acciones:

* Autenticar un dispositivo
* Vista de detalles de dispositivo
* Actualizar un dispositivo
* Eliminación de una configuración de dispositivo
* Cambiar una contraseña de dispositivo

> [!NOTE]
> Todas estas acciones también están disponibles en hello **acciones** panel.


Este tutorial le explica cómo toouse tooconnect de administrador de instantáneas StorSimple y administrar dispositivos y realizar Hola siguientes tareas:

* Incorporación o remplazo de un dispositivo
* Conexión de un dispositivo y comprobación de las importaciones
* Actualización de los dispositivos conectados
* Autenticar un dispositivo
* Vista de detalles de dispositivo
* Actualización de un dispositivo individual
* Eliminación de una configuración de dispositivo
* Cambio de una contraseña de dispositivo caducada
* Reemplazo de un dispositivo con errores

> [!NOTE]
> Para obtener información general sobre el uso de la interfaz de administrador de instantáneas de StorSimple de hello, vaya demasiado[interfaz de usuario de administrador de instantáneas StorSimple](storsimple-use-snapshot-manager.md).


## <a name="add-or-replace-a-device"></a>Incorporación o remplazo de un dispositivo
Usar hello siguiendo el procedimiento tooadd o reemplazar un dispositivo de StorSimple.

#### <a name="tooadd-or-replace-a-device"></a>tooadd o reemplazar un dispositivo
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, contextual hello **dispositivos** nodo y, a continuación, haga clic en **configurar un dispositivo**. Hola **configurar un dispositivo** aparece el cuadro de diálogo.
   
    ![Configuración de un dispositivo StorSimple](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_config_device.png) 
3. Hola **dispositivo** cuadro desplegable, seleccione Hola dirección IP de dispositivo Hola o dispositivo virtual. 
4. Hola **contraseña** cuadro de texto, una contraseña de administrador de instantáneas StorSimple Hola de tipo que ha creado para el dispositivo de Hola Hola portal de Azure clásico. Haga clic en **Aceptar**. Administrador de instantáneas StorSimple busca el dispositivo de Hola que identificó. 
   
   * Si hay dispositivos de Hola, Administrador de instantáneas StorSimple agrega una conexión.
   * Si el dispositivo de hello no está disponible por alguna razón, Administrador de instantáneas StorSimple devuelve un mensaje de error. Haga clic en **Aceptar** tooclose Hola mensaje de error y, a continuación, haga clic en **cancelar** tooclose hello **configurar un dispositivo** cuadro de diálogo.

## <a name="connect-a-device-and-verify-imports"></a>Conexión de un dispositivo y comprobación de las importaciones
Usar hello siguiendo el procedimiento tooconnect un dispositivo de StorSimple y compruebe que se han importado los grupos de volúmenes existentes que tienen asociados a las copias de seguridad.

#### <a name="tooconnect-a-device-and-verify-imports"></a>tooconnect un dispositivo y comprobar las importaciones
1. tooconnect un tooStorSimple dispositivo del Administrador de instantáneas, siga las instrucciones de hello en Agregar o reemplazar un dispositivo. Cuando se conecta el dispositivo tooa, Administrador de instantáneas StorSimple responde como se indica a continuación:
   
   * Si el dispositivo de hello no está disponible por alguna razón, Administrador de instantáneas StorSimple devuelve un mensaje de error. 
   
   * Si hay dispositivos de Hola, Administrador de instantáneas StorSimple agrega una conexión. Cuando se selecciona el dispositivo de hello, aparece en hello **resultados** panel, y el campo de estado de hello indica que el dispositivo Hola se **disponible**. Administrador de instantáneas StorSimple importa los grupos de volúmenes configurados para el dispositivo de hello, siempre que los grupos de volúmenes de hello tengan asociadas a las copias de seguridad. Las directivas de copia de seguridad no se importan. Los grupos de volúmenes que no tienen copias de seguridad asociadas no se importan.
2. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
3. Nodo superior de contextual Hola Hola **ámbito** panel y, a continuación, haga clic en **alternar visualización de importaciones**.
   
    ![Selección de Alternar visualización de importaciones](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Toggle_Imports_Display.png) 
4. Hola **alternar visualización de importaciones** aparece el cuadro de diálogo, que muestra el estado de Hola de hello importa grupos de volúmenes y copias de seguridad. Haga clic en **Aceptar**.

Después de que se hayan importado correctamente las copias de seguridad y grupos de volúmenes de hello, puede utilizar Administrador de instantáneas StorSimple toomanage ellas, exactamente como administraría los grupos de volúmenes y copias de seguridad que creó y configuró con el Administrador de instantáneas de StorSimple. 

## <a name="refresh-connected-devices"></a>Actualización de los dispositivos conectados
Usar hello siguiendo el procedimiento toosynchronize Hola conectado StorSimple dispositivos con el Administrador de instantáneas de StorSimple.

#### <a name="toorefresh-connected-devices"></a>toorefresh los dispositivos conectados
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, haga clic en **dispositivos**y, a continuación, haga clic en **actualizar dispositivos**. Esto sincroniza dispositivos Hola conectado con el Administrador de instantáneas de StorSimple para que pueda ver grupos de volúmenes de Hola y copias de seguridad, incluidas las adiciones recientes. 
   
    ![Actualizar dispositivos de StorSimple de Hola](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Refresh_devices.png)

Hola **actualizar dispositivos** acción recupera los nuevos grupos de volúmenes y copias de seguridad de dispositivos conectados. A diferencia de hello **volver a examinar volúmenes** acción disponible para hello **volúmenes** nodo, **actualizar dispositivos** no restaura el registro de copia de seguridad de Hola.

## <a name="authenticate-a-device"></a>Autenticar un dispositivo
Usar hello siguiendo el procedimiento tooauthenticate un dispositivo de StorSimple con el Administrador de instantáneas de StorSimple.

#### <a name="tooauthenticate-a-device"></a>tooauthenticate un dispositivo
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, haga clic en **dispositivos**.
3. Hola **resultados** panel, haga clic en nombre de hello de dispositivo de hello y, a continuación, haga clic en **Authenticate**.
4. Hola **Authenticate** aparece el cuadro de diálogo. Escriba la contraseña del dispositivo hello y, a continuación, haga clic en **Aceptar**.
   
    ![Cuadro de diálogo autenticar](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Authenticate.png) 

## <a name="view-device-details"></a>Vista de detalles de dispositivo
Usar hello procedimiento tooview Hola detalles de un dispositivo de StorSimple siguientes y, si es necesario, vuelva a sincronizar el dispositivo de hello con el Administrador de instantáneas de StorSimple.

#### <a name="tooview-and-resynchronize-device-details"></a>Detalles del dispositivo tooview y vuelven a sincronizar
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, haga clic en **dispositivos**.
3. Hola **resultados** panel, haga clic en nombre de hello de dispositivo de hello y, a continuación, haga clic en **detalles**.

4. Hola **detalles del dispositivo** aparece el cuadro de diálogo. Este cuadro muestra el nombre de hello, modelo, versión, número de serie, estado, destino iSCSI nombre completo (IQN) y última fecha de sincronización y la hora.

* Haga clic en **Resync** dispositivo de toosynchronize Hola.
* Haga clic en **Aceptar** o **cancelar** cuadro de diálogo de tooclose Hola.
  
  ![Detalles del dispositivo](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Device_details.png) 

## <a name="refresh-an-individual-device"></a>Actualización de un dispositivo individual
Usar hello siguiendo el procedimiento tooresynchronize un dispositivo de StorSimple individual con el Administrador de instantáneas de StorSimple.

#### <a name="toorefresh-a-device"></a>toorefresh un dispositivo
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple. 
2. Hola **ámbito** panel, haga clic en **dispositivos**. 
3. Hola **resultados** panel, haga clic en nombre de hello de dispositivo de hello y, a continuación, haga clic en **actualizar dispositivo**. Esto sincroniza el dispositivo Hola con el Administrador de instantáneas de StorSimple.

## <a name="delete-a-device-configuration"></a>Eliminación de una configuración de dispositivo
Usar hello siguiendo el procedimiento toodelete una determinada configuración de dispositivo de StorSimple desde el Administrador de instantáneas de StorSimple.

#### <a name="toodelete-a-device-configuration"></a>toodelete una configuración de dispositivo
1. Haga clic en el icono del escritorio de hello toostart Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, haga clic en **dispositivos**. 
3. Hola **resultados** panel, haga clic en nombre de hello de dispositivo de hello y, a continuación, haga clic en **eliminar**. 
4. aparece el siguiente mensaje de Hola. Haga clic en **Sí** toodelete Hola configuración o haga clic en **n** eliminación de hello toocancel.
   
    ![Eliminación de la configuración del dispositivo](./media/storsimple-snapshot-manager-manage-devices/HCS_SSM_DeleteDevice.png)

## <a name="change-an-expired-device-password"></a>Cambio de una contraseña de dispositivo caducada
Debe escribir un tooauthenticate contraseña un dispositivo de StorSimple con el Administrador de instantáneas de StorSimple. Esta contraseña se configura cuando se usa tooset de interfaz de Windows PowerShell de hello dispositivo Hola. Sin embargo, puede expirar la contraseña de Hola. Si esto ocurre, puede usar la contraseña de hello Azure toochange portal clásico de Hola. A continuación, porque el dispositivo de Hola se configuró en el Administrador de instantáneas de StorSimple antes de que caduque la contraseña de hello, debe volver a autenticarse dispositivo hello en el Administrador de instantáneas de StorSimple.

#### <a name="toochange-hello-expired-password"></a>contraseña expirada de hello toochange
1. Hola portal de Azure clásico, inicie el servicio StorSimple Manager Hola.
2. Haga clic en **dispositivos** > **configurar** para dispositivo Hola.
3. Desplácese hacia abajo toohello sección Administrador de instantáneas StorSimple. Escriba una contraseña que tenga 14 o 15 caracteres. Asegúrese de que esa contraseña hello contiene una combinación de caracteres en mayúsculas, minúsculas, numéricos y especiales.
4. Vuelva a escribir Hola contraseña tooconfirm lo.
5. Haga clic en **guardar** final Hola de página Hola.

#### <a name="toore-authenticate-hello-device"></a>toore-autenticar Hola dispositivo
1. Inicie Administrador de instantáneas StorSimple.
2. Hola **ámbito** panel, haga clic en **dispositivos**. Aparece una lista de dispositivos configurados en hello **resultados** panel.
3. Seleccionar dispositivo de hello, menú contextual y, a continuación, haga clic en **Authenticate**.
4. Hola **Authenticate** ventana, escriba Hola nueva contraseña.
5. Seleccionar dispositivo de hello, menú contextual y seleccione **actualizar dispositivo**. Esto sincroniza el dispositivo Hola con el Administrador de instantáneas de StorSimple.

## <a name="replace-a-failed-device"></a>Reemplazo de un dispositivo con errores
Si un dispositivo de StorSimple se produce un error y se reemplaza por un dispositivo de suspensión (conmutación por error), Hola uso siguiendo los pasos tooconnect vista y toohello nuevo dispositivo Hola copias de seguridad asociadas.

#### <a name="tooconnect-tooa-new-device-after-failover"></a>tooconnect tooa nuevo dispositivo después de la conmutación por error
1. Volver a configurar el nuevo dispositivo de hello iSCSI conexión toohello. Para obtener instrucciones, vaya demasiado "paso 7: montar, inicializar y formato a un volumen" en [implementar el dispositivo de StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).

> [!NOTE]
> Si el nuevo dispositivo de StorSimple Hola ha hello misma dirección IP que Hola antiguo, es posible que tooconnect capaz de la configuración antigua de Hola.


1. Detener Hola servicio de administración de StorSimple de Microsoft:
   
   1. Inicie el Administrador del servidor.
   2. En el panel Administrador del servidor, de hello en hello **herramientas** menú, seleccione **Services**.
   3. En hello **servicios** (ventana), seleccione hello **Microsoft StorSimple Management Service**.
   4. Hola haga panel, en **Microsoft StorSimple Management Service**, haga clic en **detener el servicio de hello**.
2. Quitar dispositivo antiguo de hello configuración información toohello relacionados:
   
   1. En el Explorador de archivos, busque tooC:\ProgramData\Microsoft\StorSimple\BACatalog.
   2. Eliminar archivos de hello en la carpeta BACatalog de Hola.
3. Reinicie Hola servicio de administración de StorSimple de Microsoft:
   
   1. En el panel Administrador del servidor, de hello en hello **herramientas** menú, seleccione **Services**.
   2. En hello **servicios** (ventana), seleccione hello **Microsoft StorSimple Management Service**.
   3. Hola haga panel, en **Microsoft StorSimple Management Service**, haga clic en **reiniciar servicio hello**.
4. Inicie Administrador de instantáneas StorSimple.
5. dispositivo tooconfigure Hola de nuevo StorSimple, Hola completa los pasos en el paso 2: conectar un dispositivo de StorSimple en [implementar Administrador de instantáneas de StorSimple](storsimple-snapshot-manager-deployment.md).
6. Nodo de nivel superior contextual Hola Hola **ámbito** panel (Administrador de instantáneas de StorSimple en el ejemplo de Hola) y, a continuación, haga clic en **alternar visualización de importaciones**. 
7. Aparece un mensaje cuando Hola importa grupos de volúmenes y copias de seguridad están visibles en el Administrador de instantáneas de StorSimple. Haga clic en **Aceptar**.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[usar Administrador de instantáneas StorSimple tooadminister su solución de StorSimple](storsimple-snapshot-manager-admin.md).
* Obtenga información acerca de cómo demasiado[usar Administrador de instantáneas StorSimple tooview y administrar volúmenes](storsimple-snapshot-manager-manage-volumes.md).

