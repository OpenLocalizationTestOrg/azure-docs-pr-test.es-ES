---
title: aaaConfigure MPIO en el host conectado tooStorSimple Virtual Array | Documentos de Microsoft
description: "Describe cómo tooconfigure E/S de múltiples rutas (MPIO) de la matriz Virtual de StorSimple conecta host tooa ejecuta Windows Server 2012 R2."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 5b7a7f99-ee5b-4b7d-ab32-483a5a1fa504
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/01/2017
ms.author: alkohli
ms.openlocfilehash: 0e6df23bba29395329685cbf2c968675abb04cfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multipath-io-on-windows-server-host-for-hello-storsimple-virtual-array"></a>Configurar E/S de múltiples rutas en el host de Windows Server para hello StorSimple Virtual Array
## <a name="overview"></a>Información general
Este artículo describe cómo aplicar opciones de configuración específicas para volúmenes de StorSimple solo tooinstall característica de E/S de múltiples rutas (MPIO) en el host de Windows Server y, a continuación, comprobar MPIO para volúmenes de StorSimple. Hola, se asume que la matriz Virtual de StorSimple 1200 con dos interfaces de red está conectado tooa host de Windows Server con dos interfaces de red. información de Hello contenida en este artículo aplica solo toohello de matriz virtual. Para obtener información sobre los dispositivos de la serie StorSimple 8000, vaya demasiado[configurar MPIO para StorSimple host](storsimple-configure-mpio-windows-server.md). 

característica MPIO de Hello en configuraciones de almacenamiento de alta disponibilidad y tolerancia de compilación de Ayuda de Windows Server. MPIO usa componentes de ruta de acceso física redundantes, adaptadores, cables y conmutadores: toocreate rutas de acceso lógicas entre el servidor de Hola y de dispositivo de almacenamiento de Hola. Si se produce un error de componente, provoque un toofail ruta de acceso lógica, lógica de múltiples rutas usa una ruta de acceso alternativa para E/S de modo que aplicaciones todavía pueden tener acceso a sus datos. Además dependiendo de la configuración MPIO puede mejorar el rendimiento al volver a equilibrar la carga de hello en estas rutas de acceso. Para más información, consulte [Introducción a E/S de múltiples rutas](https://technet.microsoft.com/library/cc725907.aspx "Introducción a E/S de múltiples rutas and features").

Para hello alta disponibilidad de la solución de StorSimple, configurar MPIO en hello tooyour conectado de hosts de Windows Server StorSimple Virtual Array (modelo de 1200). servidores de host de Hello, a continuación, pueden tolerar un vínculo, red o errores de interfaz. 

Necesitará toofollow estos tooconfigure pasos MPIO: 

* Requisitos previos de configuración
* Paso 1: Instalar MPIO en el host de Windows Server de Hola
* Paso 2: configurar MPIO para volúmenes de StorSimple
* Paso 3: Montar volúmenes de StorSimple en el host de Hola

Cada uno de hello por encima de los pasos se explica en las secciones siguientes de Hola.

## <a name="prerequisites"></a>Requisitos previos
Esta sección detallan los requisitos previos de hello configuración de host de Windows Server de Hola y de la matriz virtual.

### <a name="on-windows-server-host"></a>En el host de Windows Server
* Asegúrese de que el host de Windows Server tiene dos interfaces de red habilitadas.

### <a name="on-storsimple-virtual-array"></a>En StorSimple Virtual Array
* matriz virtual Hola debe configurarse como un servidor de iSCSI. más información, consulte toolearn [configurar matriz virtual como un servidor de iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md). Una o varias interfaces de red deben estar habilitadas en la matriz de Hola.   
* interfaces de red de Hello en la matriz virtual deben ser accesibles desde el host de Windows Server de Hola.
* Deben crearse uno o más volúmenes en la matriz virtual de StorSimple. más información, consulte toolearn [agregar un volumen](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume) en la matriz Virtual de StorSimple. En este procedimiento, creamos 3 volúmenes (1 anclado localmente y 2 en capas tal como se muestra a continuación) en la matriz virtual Hola.
  
    ![mpio0](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio0.png)

### <a name="hardware-configuration-for-storsimple-virtual-array"></a>Configuración de hardware para StorSimple Virtual Array
Hola siguiente ilustración muestra la configuración de hardware de Hola para lograr alta disponibilidad y equilibrio de carga de múltiples rutas para el host de Windows Server y de StorSimple Virtual Array utilizadas en este procedimiento.

![Configuración de hardware de mpio](./media/storsimple-virtual-array-configure-mpio-windows-server/1200hardwareconfig.png)

Como se muestra en hello anterior figura:

* StorSimple Virtual Array aprovisionado en Hyper-V es un dispositivo activo de nodo único configurado como un servidor iSCSI.
* Se habilitan dos interfaces de red virtual en la matriz. En la interfaz de usuario de la matriz virtual web local de hello, compruebe que los dos interfaces de red están habilitadas desplazándose demasiado**configuración de red** tal y como se muestra a continuación:
  
    ![Interfaces de red habilitadas en 1200](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio9.png)
  
    Nota Hola IPv4 direcciones de hello habilitado (Ethernet, Ethernet 2 de forma predeterminada) de interfaces de red y guardar para su uso posterior en el host de Hola.
* Se habilitan dos interfaces de red en el host de Windows Server. Si hello conectados interfaces de host y la matriz se encuentran en Hola misma subred, habrá 4 rutas disponibles. Este era el caso de hello en este procedimiento. Sin embargo, si cada interfaz de red en la interfaz de matriz y el host de Hola se encuentran en una subred IP diferente (y no enrutables), a continuación, las rutas de acceso de solo 2 estará disponibles.

## <a name="step-1-install-mpio-on-hello-windows-server-host"></a>Paso 1: Instalar MPIO en el host de Windows Server de Hola
MPIO es una característica opcional en Windows Server y no se instala de forma predeterminada. Se debe instalar como una característica a través del Administrador del servidor. tooinstall esta característica en el host de Windows Server, completar Hola siguiendo el procedimiento.

[!INCLUDE [storsimple-install-mpio-windows-server-host](../../includes/storsimple-install-mpio-windows-server-host.md)]

## <a name="step-2-configure-mpio-for-storsimple-volumes"></a>Paso 2: configurar MPIO para volúmenes de StorSimple
MPIO debe volúmenes de StorSimple de tooidentify toobe configurado. volúmenes de StorSimple de tooconfigure MPIO toorecognize, realizar Hola pasos.

[!INCLUDE [storsimple-configure-mpio-volumes](../../includes/storsimple-configure-mpio-volumes.md)]

## <a name="step-3-mount-storsimple-volumes-on-hello-host"></a>Paso 3: Montar volúmenes de StorSimple en el host de Hola
Una vez configurado MPIO en Windows Server, volúmenes creados en la matriz de StorSimple de Hola se pueden montar y, a continuación, pueden aprovechar las ventajas de MPIO para redundancia. toomount un volumen, realizar Hola pasos.

#### <a name="toomount-volumes-on-hello-host"></a>volúmenes de toomount en host Hola
1. Abra hello **propiedades del iniciador iSCSI** ventana en el host de servidor de Windows hello. Vaya demasiado**el administrador del servidor > panel > Herramientas > iniciador iSCSI**.
2. Hola **propiedades del iniciador iSCSI** cuadro de diálogo, haga clic en **detección**y, a continuación, haga clic en **detectar Portal de destino**.
3. Hola **detectar Portal de destino** diálogo cuadro, Hola siguientes:
   
    1. Escriba la dirección IP de Hola de interfaz de red habilitado primera hello en la matriz Virtual de StorSimple. De forma predeterminada, el valor de configuración sería **Ethernet**. 
    2. Haga clic en **Aceptar** tooreturn toohello **propiedades del iniciador iSCSI** cuadro de diálogo.
     
    > [!IMPORTANT]
    > Si está utilizando una red privada para las conexiones iSCSI, escriba la dirección IP de hello del puerto de datos de Hola que está conectado toohello red privada.
     
4. Repita los pasos 2 y 3 para una segunda interfaz de red (por ejemplo, Ethernet 2) en la matriz. 
5. Seleccione hello **destinos** ficha hello **propiedades del iniciador iSCSI** cuadro de diálogo. Para la matriz virtual, debería ver la superficie de cada volumen como un destino en **Destinos detectados**. En este caso, se descubren tres destinos (volúmenes toothree correspondiente).
   
    ![mpio1](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio1.png)
6. Haga clic en **conectar** tooestablish una sesión de iSCSI con la matriz Virtual de StorSimple. A **conectar tooTarget** se abre el cuadro de diálogo. Seleccione hello **habilitar múltiples rutas** casilla de verificación. Haga clic en **Avanzadas**.
   
    ![mpio2](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio2.png)
7. Hola **configuración avanzada** diálogo cuadro, Hola siguientes:                                        
   
    1. En hello **adaptador Local** lista desplegable, seleccione **iniciador iSCSI de Microsoft**.
    2. En hello **IP del iniciador** lista desplegable, seleccione Hola dirección IP host Hola.
    3. En hello **Portal de destino** lista desplegable IP, seleccione Hola IP de interfaz de la matriz.
    4. Haga clic en **Aceptar** tooreturn toohello **propiedades del iniciador iSCSI** cuadro de diálogo.
     
        ![mpio3](./media/storsimple-ova-configure-mpio-windows-server/mpio3.png)

8. Haga clic en **Propiedades**. 
   
    ![mpio4](./media/storsimple-ova-configure-mpio-windows-server/mpio4.png)

9. Hola **propiedades** cuadro de diálogo, haga clic en **Agregar sesión**.
   
   ![mpio5](./media/storsimple-ova-configure-mpio-windows-server/mpio5.png)
10. Hola **conectar tooTarget** cuadro de diálogo, seleccione hello **habilitar múltiples rutas** casilla de verificación. Haga clic en **Avanzadas**.
11. Hola **configuración avanzada** cuadro de diálogo:                                        
    
    1. En hello **adaptador Local** lista desplegable, seleccione iniciador de iSCSI de Microsoft.

    2. En hello **IP del iniciador** lista desplegable, host de toohello correspondiente de dirección IP de hello seleccione. En este caso, va a conectar dos interfaces de red en hello matriz tooa única interfaz de red en el host de Hola. Por lo tanto, esta interfaz es Hola igual que proporcionó para hello primera sesión.

    3. En hello **IP del Portal de destino** lista desplegable, dirección IP de hello seleccione para la segunda interfaz de datos Hola habilitado en la matriz de Hola.

    4. Haga clic en **Aceptar** cuadro de diálogo de propiedades del iniciador iSCSI de tooreturn toohello. Ha agregado un segundo destino toohello de sesión.
      
       ![mpio11](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio11.png)
    
    5. Después de agregar las sesiones de hello deseado (rutas de acceso), en hello **propiedades del iniciador iSCSI** cuadro de diálogo, destino Hola seleccione y haga clic en **propiedades**. En la ficha sesiones del Hola de hello **propiedades** cuadro de diálogo, tenga en cuenta Hola cuatro identificadores de sesión que corresponden toohello posibles permutaciones de ruta. toocancel una sesión, seleccione Hola casilla de verificación siguiente tooa identificador de la sesión y, a continuación, haga clic en **desconexión**.

    6. dispositivos de tooview presentados en las sesiones, seleccione hello **dispositivos** Hola de tooconfigure ficha Directiva MPIO para un dispositivo seleccionado, haga clic en **MPIO**.

    7. Hola **detalles** aparecerá el cuadro de diálogo. En hello **MPIO** ficha, puede seleccionar Hola adecuado **directiva de equilibrio de carga** configuración. También puede ver hello **Active** o **Standby** tipo de ruta de acceso.
12. Repita el destino de toohello de pasos del 8 al 11 tooadd sesiones adicionales (rutas de acceso). Con dos interfaces en el host de Hola y dos de la matriz virtual hello, puede agregar un total de cuatro sesiones para cada destino. 
    
    ![mpio14](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio14.png)
13. Necesitará toorepeat estos pasos para cada volumen (superficies como destino).
    
    ![mpio 15](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio15.png)
14. Abra **administración de equipos** desplazándose demasiado**el administrador del servidor > panel > Administración de equipos**. En el panel izquierdo de hello, haga clic en **almacenamiento > Administración de discos**. Hello volúmenes creados en hello StorSimple Virtual Array que dependen del host de toothis visible aparecerá en **administración de discos** como nuevos discos.
15. Inicialice el disco de Hola y crear un nuevo volumen. Durante el proceso de formato de hello, seleccione un tamaño de unidad de asignación (AUS) de 64 KB. Repita el proceso de Hola para todos los volúmenes disponibles Hola.
    
    ![Administración de discos](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio20.png)
16. En **administración de discos**, contextual hello **disco** y seleccione **propiedades**.
17. Hola **propiedades de dispositivo de disco de múltiples rutas** diálogo cuadro, haga clic en hello **MPIO** ficha.
    
    ![Propiedades de disco](./media/storsimple-virtual-array-configure-mpio-windows-server/mpio21.png)
18. Hola **nombre del DSM** sección, haga clic en **detalles** y compruebe que los parámetros de hello están establecidos toohello los parámetros predeterminados. parámetros de Hello predeterminados son:
    
    * Período de comprob. de ruta = 30
    * Número de reintentos = 3
    * Período de eliminación PDO = 20
    * Intervalo de reintento = 1
    * Comprobación de ruta habilitada = Sin seleccionar
    
    > [!NOTE]
    > **No modifique los parámetros predeterminados Hola.**
   
## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre [utilizando Hola tooadminister de servicio de administrador de dispositivos de StorSimple la matriz Virtual de StorSimple](storsimple-virtual-array-manager-service-administration.md).

