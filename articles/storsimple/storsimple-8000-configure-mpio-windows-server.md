---
title: aaaConfigure MPIO para el dispositivo StorSimple | Documentos de Microsoft
description: "Describe cómo tooconfigure E/S de múltiples rutas (MPIO) para el dispositivo StorSimple había conectado host tooa ejecuta Windows Server 2012 R2."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 7796524edc739826ba1e977161fc9988c6d316e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-for-your-storsimple-device"></a>Configurar E/S de múltiples rutas para el dispositivo StorSimple

Este tutorial describen los pasos de hello debe seguir tooinstall y usar la característica de E/S de múltiples rutas (MPIO) de hello en un host que ejecute Windows Server 2012 R2 y conectado tooa dispositivo físico StorSimple. Guía de Hello en este artículo aplica tooStorSimple 8000 series físico solo a los dispositivos. Actualmente, MPIO no se admite en StorSimple Cloud Appliance.

Microsoft genera compatibilidad con la característica de E/S de múltiples rutas (MPIO) de hello en Windows Server toohelp generar las configuraciones de SAN de alta disponibilidad, tolerancia. MPIO usa componentes de ruta de acceso física redundantes, adaptadores, cables y conmutadores: toocreate rutas de acceso lógicas entre el servidor de Hola y de dispositivo de almacenamiento de Hola. Si se produce un error de componente, provoque un toofail ruta de acceso lógica, lógica de múltiples rutas usa una ruta de acceso alternativa para E/S de modo que aplicaciones todavía pueden tener acceso a sus datos. Además dependiendo de la configuración MPIO puede mejorar el rendimiento mediante el equilibrio de carga de hello en estas rutas de acceso. Para más información, consulte [Introducción a E/S de múltiples rutas](https://technet.microsoft.com/library/cc725907.aspx "Introducción a E/S de múltiples rutas and features").

Para hello alta disponibilidad de la solución StorSimple MPIO debe configurarse en el dispositivo StorSimple. Cuando se instala MPIO en los servidores de host que ejecuta Windows Server 2012 R2, servidores de hello, a continuación, pueden tolerar un vínculo, red o errores de interfaz.

## <a name="mpio-configuration-summary"></a>Resumen de configuración de MPIO

MPIO es una característica opcional en Windows Server y no se instala de forma predeterminada. Se debe instalar como una característica a través del Administrador del servidor.

Siga estos tooconfigure pasos MPIO en el dispositivo de StorSimple:

* Paso 1: Instalar MPIO en el host de Windows Server de Hola
* Paso 2: configurar MPIO para volúmenes de StorSimple
* Paso 3: Montar volúmenes de StorSimple en el host de Hola
* Paso 4: configurar MPIO para alta disponibilidad y equilibrio de carga

Cada uno de los pasos anteriores de Hola se describe en las secciones siguientes de Hola.

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>Paso 1: Instalar MPIO en el host de Windows Server de Hola

tooinstall esta característica en el host de Windows Server, completar Hola siguiendo el procedimiento.

#### <a name="tooinstall-mpio-on-hello-host"></a>tooinstall MPIO en el host de Hola

1. Abra el Administrador del servidor en el host de Windows Server. De forma predeterminada, el administrador del servidor se inicia cuando un miembro del grupo de administradores de hello inicia sesión tooa equipo que ejecuta Windows Server 2012 R2 o Windows Server 2012. Hola, administrador del servidor ya no está abierto, haga clic en **Inicio > Administrador del servidor**.
   
   ![Administrador del servidor](./media/storsimple-configure-mpio-windows-server/IC740997.png)

2. Haga clic en **Administrador del servidor > Panel > Agregar roles y características**. Esto inicia hello **agregar Roles y características** asistente.
   
   ![Asistente para agregar roles y características 1](./media/storsimple-configure-mpio-windows-server/IC740998.png)
3. Hola **agregar Roles y características** asistente, realizar Hola pasos:
   
   1. En hello **antes de comenzar** página, haga clic en **siguiente**.
   2. En hello **Seleccionar tipo de instalación** , acepte la configuración predeterminada de Hola de **basada en roles o basada en características** instalación. Haga clic en **Siguiente**.
   
       ![Asistente para agregar roles y características 2](./media/storsimple-configure-mpio-windows-server/IC740999.png)
   3. En hello **Seleccionar servidor de destino** página, elija **seleccione un servidor de grupo de servidores de hello**. El servidor host debería detectarse automáticamente. Haga clic en **Siguiente**.
   4. En hello **seleccionar roles de servidor** página, haga clic en **siguiente**.
   5. En hello **seleccionar características** , seleccione **E/S de múltiples rutas**y haga clic en **siguiente**.
   
       ![Asistente para agregar roles y características 5](./media/storsimple-configure-mpio-windows-server/IC741000.png)
   6. En hello **Confirmar selecciones de instalación** página, confirme la selección de hello y, a continuación, seleccione **reinicie el servidor de destino Hola automáticamente si es necesario**, tal y como se muestra a continuación. Haga clic en **Instalar**.
   
       ![Asistente para agregar roles y características 8](./media/storsimple-configure-mpio-windows-server/IC741001.png)
   7. Se le notifica cuando se completa la instalación de Hola. Haga clic en **cerrar** Asistente de hello tooclose.
   
       ![Asistente para agregar roles y características 9](./media/storsimple-configure-mpio-windows-server/IC741002.png)

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>Paso 2: configurar MPIO para volúmenes de StorSimple

MPIO debe estar configurado tooidentify volúmenes de StorSimple. volúmenes de StorSimple de tooconfigure MPIO toorecognize, realizar Hola pasos.

#### <a name="tooconfigure-mpio-for-storsimple-volumes"></a>tooconfigure MPIO para volúmenes de StorSimple

1. Abra hello **configuración de MPIO**. Haga clic en **Administrador del servidor > Panel > Herramientas > MPIO**.
2. Hola **propiedades de MPIO** cuadro de diálogo, seleccione hello **detectar múltiples rutas** ficha.
3. Seleccione **Agregar compatibilidad con dispositivos iSCSI** y, luego, haga clic en **Agregar**.  
   ![Propiedades de MPIO &amp;gt; Detectar múltiples rutas](./media/storsimple-configure-mpio-windows-server/IC741003.png)
4. Reinicie el servidor de hello cuando se le solicite.
5. Hola **propiedades de MPIO** diálogo cuadro, haga clic en hello **dispositivos con MPIO** ficha. Haga clic en **agregar**.
    </br>![Propiedades de MPIO &amp;gt; Dispositivo con MPIO](./media/storsimple-configure-mpio-windows-server/IC741004.png)
6. Hola **agregar compatibilidad con MPIO** cuadro de diálogo **Id. de Hardware de dispositivo**, escriba el número de serie del dispositivo. tooget Hola acceso de dispositivo serie numérica, el servicio de administrador de dispositivos de StorSimple. Navegue demasiado**dispositivos > panel**. número de serie del dispositivo de Hola se muestra en hello derecho **vista rápida** panel del panel del dispositivo Hola.
    </br>
    ![Agregar compatibilidad con MPIO](./media/storsimple-configure-mpio-windows-server/IC741005.png)
7. Reinicie el servidor de hello cuando se le solicite.

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>Paso 3: Montar volúmenes de StorSimple en el host de Hola

Una vez configurado MPIO en Windows Server, volúmenes creados en el dispositivo de StorSimple de Hola se pueden montar y, a continuación, pueden aprovechar las ventajas de MPIO para redundancia. toomount un volumen, realizar Hola pasos.

#### <a name="toomount-volumes-on-hello-host"></a>volúmenes de toomount en host Hola

1. Abra hello **propiedades del iniciador iSCSI** ventana en el host de servidor de Windows hello. Haga clic en **Administrador del servidor > Panel > Herramientas > Iniciador iSCSI**.
2. Hola **propiedades del iniciador iSCSI** cuadro de diálogo, haga clic en la pestaña de detección de hello y, a continuación, haga clic en **detectar Portal de destino**.
3. Hola **detectar Portal de destino** diálogo cuadro, lleve a cabo Hola pasos:
   
   1. Escriba Hola dirección IP de puerto de datos del dispositivo StorSimple de hello (por ejemplo, escriba DATA 0).
   2. Haga clic en **Aceptar** tooreturn toohello **propiedades del iniciador iSCSI** cuadro de diálogo.
     
     > [!IMPORTANT]
     > **Si está utilizando una red privada para las conexiones iSCSI, escriba la dirección IP de hello del puerto de datos de Hola que está conectado toohello red privada.**
    
4. Repita los pasos 2 y 3 para una segunda interfaz de red (por ejemplo, DATA 1) en el dispositivo. No olvide que estas interfaces deben estar habilitadas para iSCSI. Para más información, consulte [Modificar las interfaces de red](storsimple-8000-modify-device-config.md#modify-network-interfaces).
5. Seleccione hello **destinos** ficha hello **propiedades del iniciador iSCSI** cuadro de diálogo. Debería ver el dispositivo StorSimple Hola destino IQN en **destinos detectados**.

   ![Propiedades del iniciador iSCSI > pestaña Destinos](./media/storsimple-configure-mpio-windows-server/IC741007.png)
   
6. Haga clic en **conectar** tooestablish una sesión de iSCSI con el dispositivo de StorSimple. A **conectar tooTarget** aparece el cuadro de diálogo.
7. Hola **conectar tooTarget** cuadro de diálogo, seleccione hello **habilitar múltiples rutas** casilla de verificación. Haga clic en **Avanzadas**.
8. Hola **configuración avanzada** diálogo cuadro, lleve a cabo Hola pasos:
   
   1. En hello **adaptador Local** lista desplegable, seleccione **iniciador iSCSI de Microsoft**.
   2. En hello **IP del iniciador** lista desplegable, seleccione Hola dirección IP host Hola.
   3. En hello **Portal de destino** lista desplegable IP, seleccione Hola IP de la interfaz de dispositivo.
   4. Haga clic en **Aceptar** tooreturn toohello **propiedades del iniciador iSCSI** cuadro de diálogo.
9. Haga clic en **Propiedades**. Hola **propiedades** cuadro de diálogo, haga clic en **Agregar sesión**.
10. Hola **conectar tooTarget** cuadro de diálogo, seleccione hello **habilitar múltiples rutas** casilla de verificación. Haga clic en **Avanzadas**.
11. Hola **configuración avanzada** cuadro de diálogo:

    1. En hello **adaptador Local** lista desplegable, seleccione iniciador de iSCSI de Microsoft.
    2. En hello **IP del iniciador** lista desplegable, host de toohello correspondiente de dirección IP de hello seleccione. En este caso, va a conectar dos interfaces de red en hello dispositivo tooa única interfaz de red en el host de Hola. Por lo tanto, esta interfaz es Hola igual que proporcionó para hello primera sesión.
    3. En hello **IP del Portal de destino** lista desplegable, dirección IP de hello seleccione para la segunda interfaz de datos Hola habilitado en el dispositivo de Hola.
    4. Haga clic en **Aceptar** cuadro de diálogo de propiedades del iniciador iSCSI de tooreturn toohello. Ha agregado un segundo destino toohello de sesión.
12. Abra **administración de equipos** desplazándose demasiado**el administrador del servidor > panel > Administración de equipos**. En el panel izquierdo de hello, haga clic en **almacenamiento > Administración de discos**. volumen de Hello creado en el dispositivo StorSimple Hola que dependen del host de toothis visible aparece bajo **administración de discos** como nuevos discos.
13. Inicialice el disco de Hola y crear un nuevo volumen. Durante el proceso de formato de hello, seleccione un tamaño de bloque de 64 KB.
    
    ![Administración de discos](./media/storsimple-configure-mpio-windows-server/IC741008.png)
14. En **administración de discos**, contextual hello **disco** y seleccione **propiedades**.
15. Hola StorSimple modelo ### **propiedades de dispositivo de disco de múltiples rutas** diálogo cuadro, haga clic en hello **MPIO** ficha.
    
    ![DeviceProp del disco de múltiples rutas StorSimple 8100.](./media/storsimple-configure-mpio-windows-server/IC741009.png)
16. Hola **nombre del DSM** sección, haga clic en **detalles** y compruebe que los parámetros de hello están establecidos toohello los parámetros predeterminados. parámetros de Hello predeterminados son:
    
    * Período de comprob. de ruta = 30
    * Número de reintentos = 3
    * Período de eliminación PDO = 20
    * Intervalo de reintento = 1
    * Comprobación de ruta habilitada = Sin seleccionar

> [!NOTE]
> **No modifique los parámetros predeterminados Hola.**


## <a name="step-4-configure-mpio-for-high-availability-and-load-balancing"></a>Paso 4: configurar MPIO para alta disponibilidad y equilibrio de carga

De múltiples rutas de acceso en función de alta disponibilidad y equilibrio de carga, varias sesiones deben agregarse manualmente toodeclare Hola diferentes rutas de acceso disponibles. Por ejemplo, si el host de hello tiene dos interfaces conectadas hello y tooSAN dispositivo tiene dos interfaces de tooSAN conectado, entonces tendrá cuatro sesiones configuradas con permutaciones de ruta de acceso adecuadas (solo dos sesiones será necesario si cada interfaz DATA e interfaz de host es en una subred IP diferente y no es enrutable).

**Se recomienda que haya al menos 8 sesiones paralelas activas entre dispositivos de Hola y el host de la aplicación.** Esto puede lograrse habilitando 4 interfaces de red en su sistema Windows Server. Usar interfaces de red físico o virtual a través de las tecnologías de virtualización de red en el nivel de sistema operativo o hardware de hello en el host de Windows Server. Con hello dos interfaces de red en el dispositivo de hello, esta configuración se crearán 8 sesiones activas. Esta configuración ayuda a optimizar el rendimiento de dispositivo y en la nube de Hola.

> [!IMPORTANT]
> **Recomendamos no combinar interfaces de red de 1 GbE y de 10 GbE. Si se usan dos interfaces de red, ambas interfaces deben ser Hola idéntico tipo.**

Hello siguiente procedimiento describe cómo hospedan sesiones tooadd cuando un dispositivo de StorSimple con dos interfaces de red está conectado tooa con dos interfaces de red. Le proporciona solo 4 sesiones. Siga este mismo procedimiento con un dispositivo de StorSimple con el host de red dos interfaces conectadas tooa con cuatro interfaces de red. Necesitará tooconfigure 8 en lugar de hello 4 sesiones que se describen aquí.

### <a name="tooconfigure-mpio-for-high-availability-and-load-balancing"></a>tooconfigure MPIO para alta disponibilidad y equilibrio de carga

1. Realizar una detección del destino de hello: Hola **propiedades del iniciador iSCSI** cuadro de diálogo de hello **detección** , haga clic en **detectar Portal**.
2. Hola **conectar tooTarget** diálogo cuadro, escriba la dirección IP de Hola de una de las interfaces de red del dispositivo de Hola.
3. Haga clic en **Aceptar** tooreturn toohello **propiedades del iniciador iSCSI** cuadro de diálogo.
4. Hola **propiedades del iniciador iSCSI** cuadro de diálogo, seleccione hello **destinos** ficha, resalte el destino de hello detectado y, a continuación, haga clic en **conectar**. Hola **conectar tooTarget** aparece el cuadro de diálogo.
5. Hola **conectar tooTarget** cuadro de diálogo:
   
   1. Deje Hola predeterminado seleccionado configuración de destino de **agregar esta conexión** toohello lista de destinos favoritos. Esto hace que el dispositivo de hello intentará automáticamente la conexión de hello toorestart cada vez que se reinicie el equipo.
   2. Seleccione hello **habilitar múltiples rutas** casilla de verificación.
   3. Haga clic en **Avanzadas**.
6. Hola **configuración avanzada** cuadro de diálogo:
   
   1. En hello **adaptador Local** lista desplegable, seleccione **iniciador iSCSI de Microsoft**.
   2. En hello **IP del iniciador** lista desplegable, seleccione Hola dirección IP host Hola.
   3. En hello **IP del Portal de destino** lista desplegable, dirección IP seleccione Hola Hola de interfaz de datos habilitada en el dispositivo de Hola.
   4. Haga clic en **Aceptar** cuadro de diálogo de propiedades del iniciador iSCSI de tooreturn toohello.
7. Haga clic en **propiedades**y en hello **propiedades** cuadro de diálogo, haga clic en **Agregar sesión**.
8. Hola **conectar tooTarget** cuadro de diálogo, seleccione hello **habilitar múltiples rutas** casilla de verificación y, a continuación, haga clic en **avanzadas**.
9. Hola **configuración avanzada** cuadro de diálogo:
   
   1. En hello **adaptador Local** lista desplegable, seleccione **iniciador iSCSI de Microsoft**.
   2. En hello **IP del iniciador** lista desplegable, seleccione Hola dirección IP correspondiente toohello segunda interfaz en el host de Hola.
   3. En hello **IP del Portal de destino** lista desplegable, dirección IP de hello seleccione para la segunda interfaz de datos Hola habilitado en el dispositivo de Hola.
   4. Haga clic en **Aceptar** tooreturn toohello **propiedades del iniciador iSCSI** cuadro de diálogo. Ya has agregado un segundo destino toohello de sesión.
10. Repita el destino de toohello de pasos del 8 al 10 tooadd sesiones adicionales (rutas de acceso). Con dos interfaces en el host de Hola y dos en el dispositivo de hello, puede agregar un total de cuatro sesiones.
11. Después de agregar las sesiones de hello deseado (rutas de acceso), en hello **propiedades del iniciador iSCSI** cuadro de diálogo, destino Hola seleccione y haga clic en **propiedades**. En la ficha sesiones del Hola de hello **propiedades** cuadro de diálogo, tenga en cuenta Hola cuatro identificadores de sesión que corresponden toohello posibles permutaciones de ruta. toocancel una sesión, seleccione Hola casilla de verificación siguiente tooa identificador de la sesión y, a continuación, haga clic en **desconexión**.
12. dispositivos de tooview presentados en las sesiones, seleccione hello **dispositivos** Hola de tooconfigure ficha Directiva MPIO para un dispositivo seleccionado, haga clic en **MPIO**. Hola **detalles del dispositivo** aparece el cuadro de diálogo. En hello **MPIO** ficha, puede seleccionar Hola adecuado **directiva de equilibrio de carga** configuración. También puede ver hello **Active** o **Standby** tipo de ruta de acceso.

## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre [utilizando Hola toomodify de servicio de administrador de dispositivos de StorSimple la configuración del dispositivo StorSimple](storsimple-8000-modify-device-config.md).

