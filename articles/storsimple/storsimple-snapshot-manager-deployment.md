---
title: "Administrador de instantáneas StorSimple aaaDeploy | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toodownload e instalar Hola Administrador de instantáneas de StorSimple, un complemento de MMC para administrar las características de copia de seguridad y protección de datos de StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: f0128f57-519e-49ec-9187-23575809cdbe
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: dd90cca2bbb3410bb8cd459fb1a3ff3fb5f2997b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-snapshot-manager-mmc-snap-in"></a>Implementar Hola complemento MMC de administrador de instantáneas StorSimple

## <a name="overview"></a>Información general
Hola StorSimple Snapshot Manager es un complemento de Microsoft Management Console (MMC) que simplifica la protección de datos y la administración de copia de seguridad en un entorno de Microsoft Azure StorSimple. Con Administrador de instantáneas StorSimple, puede administrar los datos de Microsoft Azure StorSimple de forma local y en la nube como un sistema de almacenamiento integrado y, por consiguiente, simplificar los procesos de copia de seguridad y restauración, así como reducir los costos. 

En este tutorial se describen los requisitos de configuración, así como los procedimientos para instalar, quitar y actualizar Administrador de instantáneas StorSimple.

> [!NOTE]
> * No puede usar el Administrador de instantáneas StorSimple toomanage Microsoft Azure StorSimple Virtual matrices (también conocido como StorSimple virtuales dispositivos locales).
> * Si tiene previsto tooinstall StorSimple Update 2 en el dispositivo StorSimple, ser seguro toodownload Hola última versión del Administrador de instantáneas de StorSimple e instalarlo **antes de instalar StorSimple Update 2**. la versión más reciente de Hola de StorSimple Snapshot Manager es compatible con versiones anteriores y funciona con todas las versiones publicadas de Microsoft Azure StorSimple. Si está utilizando la versión anterior de Hola de administrador de instantáneas de StorSimple, necesitará tooupdate TI (no necesita toouninstall Hola anterior versión antes de instalar la nueva versión de hello).


## <a name="storsimple-snapshot-manager-installation"></a>Instalación de Administrador de instantáneas StorSimple
Administrador de instantáneas StorSimple puede instalarse en equipos que ejecutan el sistema de operativo de Windows Server 2008 R2 SP1, Windows Server 2012 o Windows Server 2012 R2 Hola. En servidores que ejecutan Windows 2008 R2, también debe instalar Windows Server 2008 SP1 y Windows Management Framework 3.0.

Antes de instalar o actualizar Hola Administrador de instantáneas StorSimple complemento Hola Microsoft Management Console (MMC), asegúrese de que ese dispositivo de StorSimple de Microsoft Azure hello y servidor host estén configurados correctamente.

## <a name="configure-prerequisites"></a>Configuración de los requisitos previos
Hello pasos siguientes proporcionan una descripción general de las tareas de configuración que debe completar antes de instalar el Administrador de instantáneas StorSimple Hola. Para completar la configuración de Microsoft Azure StorSimple y la información de configuración, incluidos los requisitos del sistema y obtener instrucciones detalladas, consulte [Implementar el dispositivo StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).

> [!IMPORTANT]
> Antes de comenzar, revise hello [lista de comprobación de configuración de implementación](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist) y y [requisitos previos de implementación](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites) en [implementar el dispositivo de StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).
> <br>
> 
> 

### <a name="before-you-install-storsimple-snapshot-manager"></a>Antes de instalar Administrador de instantáneas StorSimple
1. Desempaquete, monte y conecte el dispositivo de Microsoft Azure StorSimple Hola tal y como se describe en [instalar el dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md) o [instalar su dispositivo 8600 StorSimple](storsimple-8600-hardware-installation.md).
2. Asegúrese de que el equipo host está ejecutando uno de los siguientes sistemas operativos de hello:
   
   * Windows Server 2008 R2 (en servidores que ejecutan Windows 2008 R2, también debe instalar Windows Server 2008 SP1 y Windows Management Framework 3.0)
   * Windows Server 2012
   * Windows Server 2012 R2
     
     Para un dispositivo StorSimple virtual, host de hello debe ser una máquina Virtual de Microsoft Azure.
3. Asegúrese de que se cumplen todos los requisitos de configuración de Microsoft Azure StorSimple Hola. Para obtener más información, consulte demasiado[requisitos previos de implementación](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites).
4. Conectar el host de toohello de dispositivo de Hola y realizar la configuración inicial de Hola. Para obtener más información, consulte demasiado[pasos de implementación](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps).
5. Crear volúmenes en el dispositivo de hello, asignarles toohello host y compruebe que hospedan Hola puede montar y usarlos. Administrador de instantáneas StorSimple admite Hola siguientes tipos de volúmenes:
   
   * Volúmenes básicos
   * Volúmenes simples
   * Volúmenes dinámicos
   * Volúmenes dinámicos con reflejos (RAID 1)
   * Volúmenes compartidos de clúster
     
     Para obtener información sobre la creación de volúmenes en el dispositivo de StorSimple de Hola o dispositivo virtual StorSimple, vaya demasiado[paso 6: crear un volumen](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume), en [implementar el dispositivo de StorSimple local](storsimple-8000-deployment-walkthrough-u2.md).

## <a name="install-a-new-storsimple-snapshot-manager"></a>Instalación de un nuevo Administrador de instantáneas StorSimple
Antes de instalar el Administrador de instantáneas de StorSimple, asegúrese de que Hola volúmenes que creó en el dispositivo de StorSimple de Hola o dispositivo virtual StorSimple se montar, inicializar y con el formato descrito en [configurar los requisitos previos](#configure-prerequisites).

> [!IMPORTANT]
> * Para un dispositivo StorSimple virtual, host de hello debe ser una máquina Virtual de Microsoft Azure. 
> * host de Hola debe ejecutar Windows 2008 R2, Windows Server 2012 o Windows Server 2012 R2. Si el servidor ejecuta Windows Server 2008 R2, también debe instalar Windows Server 2008 SP1 y Windows Management Framework 3.0.
> * Debe configurar una conexión iSCSI desde el dispositivo de StorSimple de toohello de hello host antes de poder conectar Hola dispositivo tooStorSimple Administrador de instantáneas.

Siga estos toocomplete pasos una instalación nueva de administrador de instantáneas de StorSimple. Si va a instalar una actualización, vaya demasiado[actualizar o reinstalar el Administrador de instantáneas de StorSimple](#upgrade-or-reinstall-storsimple-snapshot-manager).

* Paso 1: Instalación de Administrador de instantáneas StorSimple 
* Paso 2: Conectar dispositivo tooa de administrador de instantáneas StorSimple 
* Paso 3: Comprobar el dispositivo de hello conexión toohello 

### <a name="step-1-install-storsimple-snapshot-manager"></a>Paso 1: Instalación de Administrador de instantáneas StorSimple
Usar hello siguiendo los pasos tooinstall Administrador de instantáneas StorSimple.

#### <a name="tooinstall-storsimple-snapshot-manager"></a>tooinstall Administrador de instantáneas StorSimple
1. Descargar el software de administrador de instantáneas StorSimple Hola (ir demasiado[StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220) Hola Microsoft Download Center) y se guarda localmente en el host de Hola.
2. En el Explorador de archivos, haga clic en carpeta comprimida de hello y, a continuación, haga clic en **extraer todo**.
3. Hola **extraer carpetas comprimidas (zip)** ventana, en hello **seleccionar un destino y extraer archivos** cuadro, escriba o busque la ruta de acceso de toohello dónde se desea toobe toofile extraído.
   
    > [!IMPORTANT]
    > Debe instalar el Administrador de instantáneas StorSimple en hello unidad C:.
    
4. Seleccione hello **mostrar archivos cuando haya finalizado extraídos** casilla de verificación y, a continuación, haga clic en **extraer**.
   
    ![Extracción del cuadro de diálogo de archivos](./media/storsimple-snapshot-manager-deployment/HCS_SSM_extract_files.png) 
5. Cuando haya finalizado la extracción de hello, abre la carpeta de destino de Hola. Haga doble clic en el icono de instalación de aplicación Hola que aparece en la carpeta de destino de Hola.
6. Cuando Hola **el programa de instalación correcta** aparece el mensaje, haga clic en **cerrar**. Debería ver el icono de administrador de instantáneas de StorSimple de hello en el escritorio.
   
    ![icono del escritorio](./media/storsimple-snapshot-manager-deployment/HCS_SSM_desktop_icon.png) 

### <a name="step-2-connect-storsimple-snapshot-manager-tooa-device"></a>Paso 2: Conectar dispositivo tooa de administrador de instantáneas StorSimple
Usar hello siguiendo los pasos tooconnect dispositivo de administrador de instantáneas StorSimple tooa StorSimple.

#### <a name="tooconnect-storsimple-snapshot-manager-tooa-device"></a>tooconnect dispositivo tooa de administrador de instantáneas StorSimple
1. Haga clic en el icono de administrador de instantáneas de StorSimple de hello en el escritorio. Aparecerá la ventana del Administrador de instantáneas StorSimple Hola. ventana Hello contiene un **ámbito** panel, un **resultados** panel y un **acciones** panel. 
   
    ![Interfaz de usuario de Administrador de instantáneas StorSimple](./media/storsimple-snapshot-manager-deployment/HCS_SSM_gui_panes.png)
   
   * Hola **ámbito** panel (panel izquierdo hello) contiene una lista de nodos organizados en una estructura de árbol. Puede expandir algunos nodos tooselect una vista o un nodo de toothat relacionados de datos específicos. Haga clic en tooexpand de icono de flecha de Hola o contraer un nodo. Haga clic en un elemento de hello **ámbito** panel toosee una lista de las acciones disponibles para ese elemento.
   * Hola **resultados** panel (panel central de hello) contiene información de estado detallada acerca de nodo de hello, vista o datos que seleccionó en hello **ámbito** panel.
   * Hola **acciones** panel enumera las operaciones de Hola que puede realizar en el nodo de hello, vista o datos que seleccionó en hello **ámbito** panel.
     
     Para obtener una descripción completa de la interfaz de usuario de administrador de instantáneas StorSimple hello, consulte [interfaz de usuario de administrador de instantáneas StorSimple](storsimple-use-snapshot-manager.md).
2. Hola **ámbito** panel, contextual hello **dispositivos** nodo y, a continuación, haga clic en **configurar un dispositivo**. Hola **configurar un dispositivo** aparece el cuadro de diálogo.
   
    ![Configurar un dispositivo](./media/storsimple-snapshot-manager-deployment/HCS_SSM_config_device.png) 
3. Hola **dispositivo** lista cuadro, Hola seleccione dirección IP de dispositivo de Microsoft Azure StorSimple Hola o dispositivo virtual. Hola **contraseña** cuadro de texto, una contraseña de administrador de instantáneas StorSimple Hola de tipo que ha creado para el dispositivo de Hola Hola portal de Azure. Haga clic en **Aceptar**.
4. Administrador de instantáneas StorSimple busca el dispositivo de Hola que identificó. Si hay dispositivos de Hola, Administrador de instantáneas StorSimple agrega una conexión. También puede [Compruebe Hola conexión toohello dispositivo](#to-verify-the-connection) tooconfirm que Hola conexión se agregó correctamente.
   
    Si el dispositivo de hello no está disponible por alguna razón, Administrador de instantáneas StorSimple devuelve un mensaje de error. Haga clic en **Aceptar** tooclose Hola mensaje de error y, a continuación, haga clic en **cancelar** tooclose hello **configurar un dispositivo** cuadro de diálogo.
5. Cuando se conecta el dispositivo tooa, Administrador de instantáneas StorSimple importa cada grupo de volúmenes configurado para ese dispositivo, siempre que hello grupo de volúmenes asociado las copias de seguridad. Los grupos de volúmenes que no tienen copias de seguridad asociadas no se importan. Además, las directivas de copia de seguridad que se crearon para un grupo de volúmenes no se importan. toosee Hola grupos importados, haga clic en la parte superior de hello **grupos de volúmenes** nodo Hola **ámbito** panel y haga clic en **alternar grupos importados**.

### <a name="step-3-verify-hello-connection-toohello-device"></a>Paso 3: Comprobar el dispositivo de hello conexión toohello
Usar hello después tooverify de pasos que el Administrador de instantáneas de StorSimple es toohello conectado el dispositivo de StorSimple.

#### <a name="tooverify-hello-connection"></a>conexión de hello tooverify
1. Hola **ámbito** panel, haga clic en hello **dispositivos** nodo.
   
    ![Estado del dispositivo de Administrador de instantáneas StorSimple](./media/storsimple-snapshot-manager-deployment/HCS_SSM_Device_status.png) 
2. Comprobar hello **resultados** panel: 
   
   * Si aparece un indicador verde en el icono de dispositivo de Hola y **disponible** aparece en hello **estado** columna, a continuación, dispositivo Hola está conectado. 
   * Si aparece un indicador rojo en el icono de dispositivo de hello y no disponible aparece en hello **estado** columna, a continuación, dispositivo hello no está conectado. 
   * Si **actualizando** aparece en hello **estado** columna y, a continuación, el Administrador de instantáneas de StorSimple está recuperando grupos de volúmenes y copias de seguridad asociadas para un dispositivo conectado.

## <a name="upgrade-or-reinstall-storsimple-snapshot-manager"></a>Actualización o reinstalación de Administrador de instantáneas StorSimple
Debe desinstalar el Administrador de instantáneas StorSimple completamente antes de actualizar o volver a instalar el software de Hola. 

Antes de reinstalar el Administrador de instantáneas de StorSimple, realice una copia hello StorSimple Snapshot Manager base de datos existente en el equipo de host de Hola. Esto guarda la información de configuración y las directivas de copia de seguridad de Hola para que pueda restaurar fácilmente estos datos de copia de seguridad.

Si va a actualizar o reinstalar Administrador de instantáneas StorSimple, siga estos pasos:

* Paso 1: Desinstalación de Administrador de instantáneas StorSimple 
* Paso 2: Realizar una copia de base de datos de administrador de instantáneas StorSimple Hola 
* Paso 3: Reinstalar el Administrador de instantáneas de StorSimple y restaurar la base de datos de Hola 

### <a name="step-1-uninstall-storsimple-snapshot-manager"></a>Paso 1: Desinstalación de Administrador de instantáneas StorSimple
Usar hello siguiendo los pasos toouninstall Administrador de instantáneas StorSimple.

#### <a name="toouninstall-storsimple-snapshot-manager"></a>toouninstall Administrador de instantáneas StorSimple
1. En el equipo de host de hello, abra hello **el Panel de Control**, haga clic en **programas**y, a continuación, haga clic en **programas y características**.
2. En el panel izquierdo de hello, haga clic en **desinstalar o cambiar un programa**.
3. Haga clic con el botón derecho en **StorSimple Snapshot Manager** y, después, haga clic en **Desinstalar**.
4. Esto inicia Hola programa de instalación de administrador de instantáneas StorSimple. Haga clic en **Modificar instalación** y, luego, haga clic en **Desinstalar**.
   
   > [!NOTE]
   > Si hay algún proceso MMC ejecutándose en segundo plano de hello, como el Administrador de instantáneas de StorSimple o administración de discos, se producirá un error en la desinstalación de Hola y recibirá un mensaje tooclose todas las instancias de MMC antes de intentan programa Hola de toouninstall. Seleccione **automáticamente, cierre las aplicaciones e intente toorestart ellos después de que el programa de instalación se complete**y, a continuación, haga clic en **Aceptar**.
   > 
   > 
5. Cuando desinstala Hola finalice el proceso, un **el programa de instalación correcta** aparece el mensaje. Haga clic en **Cerrar**.

### <a name="step-2-back-up-hello-storsimple-snapshot-manager-database"></a>Paso 2: Realizar una copia de base de datos de administrador de instantáneas StorSimple Hola
Usar hello siguiendo los pasos toocreate y guardar una copia de base de datos de administrador de instantáneas StorSimple Hola.

#### <a name="tooback-up-hello-database"></a>tooback la base de datos de Hola
1. Detener Hola servicio de administración de StorSimple de Microsoft:
   
   1. Inicie el Administrador del servidor.
   2. En el panel Administrador del servidor, de hello en hello **herramientas** menú, seleccione **Services**.
   3. En hello **servicios** página, seleccione **Microsoft StorSimple Management Service**.
   4. Hola haga panel, en **Microsoft StorSimple Management Service**, haga clic en **detener el servicio de hello**.
      
        ![Detener el servicio de administrador de dispositivos de StorSimple de Hola](./media/storsimple-snapshot-manager-deployment/HCS_SSM_stop_service.png)
2. Examinar tooC:\ProgramData\Microsoft\StorSimple\BACatalog. 
   
   > [!NOTE]
   > ProgramData es una carpeta oculta.
  
3. Buscar archivo XML del catálogo hello, copiar el archivo de Hola y almacenar Hola copiar en una ubicación segura o en la nube de Hola.
   
    ![Archivo de catálogo de copia de seguridad de StorSimple](./media/storsimple-snapshot-manager-deployment/HCS_SSM_bacatalog.png)
4. Reinicie Hola servicio de administración de StorSimple de Microsoft: 
   
   1. En el panel Administrador del servidor, de hello en hello **herramientas** menú, seleccione **Services**.
   2. En hello **servicios** página, seleccione hello **servicio de almacenamiento de Microsoft StorSimple Management**e.
   3. Hola haga panel, en **Microsoft StorSimple Management Service**, haga clic en **reiniciar servicio hello**. 

### <a name="step-3-reinstall-storsimple-snapshot-manager-and-restore-hello-database"></a>Paso 3: Reinstalar el Administrador de instantáneas de StorSimple y restaurar la base de datos de Hola
tooreinstall Administrador de instantáneas de StorSimple, siga los pasos de hello en [instalar un nuevo administrador de instantáneas de StorSimple](#install-a-new-storsimple-snapshot-manager). A continuación, usar hello después de la base de datos del Administrador de instantáneas StorSimple de procedimiento toorestore Hola.

#### <a name="toorestore-hello-database"></a>base de datos de toorestore Hola
1. Detener Hola servicio de administración de StorSimple de Microsoft:
   
   1. Inicie el Administrador del servidor.
   2. En el panel Administrador del servidor, de hello en hello **herramientas** menú, seleccione **Services**.
   3. En hello **servicios** página, seleccione **Microsoft StorSimple Management Service**.
   4. Hola haga panel, en **Microsoft StorSimple Management Service**, haga clic en **detener el servicio de hello**.
2. Examinar tooC:\ProgramData\Microsoft\StorSimple\BACatalog.
   
   > [!NOTE]
   > ProgramData es una carpeta oculta.
   > 
   > 
3. Eliminar el archivo XML del catálogo hello y reemplazarla con la versión de Hola que guardó anteriormente.
4. Reinicie Hola servicio de administración de StorSimple de Microsoft: 
   
   1. En el panel Administrador del servidor, de hello en hello **herramientas** menú, seleccione **Services**.
   2. En hello **servicios** página, seleccione **Microsoft StorSimple Management Service**.
   3. Hola haga panel, en **Microsoft StorSimple Management Service**, haga clic en **reiniciar servicio hello**.

## <a name="next-steps"></a>Pasos siguientes
* toolearn más sobre Administrador de instantáneas StorSimple, vaya demasiado[¿qué es el Administrador de instantáneas StorSimple?](storsimple-what-is-snapshot-manager.md).
* toolearn más información acerca de la interfaz de usuario de administrador de instantáneas StorSimple hello, vaya demasiado[interfaz de usuario de administrador de instantáneas StorSimple](storsimple-use-snapshot-manager.md).
* toolearn más sobre el uso de administrador de instantáneas de StorSimple, vaya demasiado[tooadminister Use el Administrador de instantáneas StorSimple la solución de StorSimple](storsimple-snapshot-manager-admin.md).

