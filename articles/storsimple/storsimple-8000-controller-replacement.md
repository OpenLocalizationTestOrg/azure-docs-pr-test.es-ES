---
title: controlador de dispositivo de aaaReplace un StorSimple 8000 series | Documentos de Microsoft
description: "Explica cómo tooremove y reemplazar uno o ambos módulos de controlador en el dispositivo de la serie StorSimple 8000."
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
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 76d42529da42dff2a214fb840a52392a7f1a97ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-controller-module-on-your-storsimple-device"></a>Reemplazar un módulos de controladores en el dispositivo StorSimple
## <a name="overview"></a>Información general
Este tutorial le explica cómo tooremove y reemplazar uno o ambos módulos de controlador en un dispositivo de StorSimple. También se tratan Hola subyacente lógica para escenarios de sustitución de controlador único o doble de Hola.

> [!NOTE]
> Sustitución de un controlador de tooperforming anterior, se recomienda actualizar siempre la versión más reciente de controlador firmware toohello.
> 
> tooprevent dañar el dispositivo de StorSimple tooyour, no extraiga Hola controlador hasta que Hola LED se muestren como uno de hello siguientes:
> 
> * Todas las luces están apagadas.
> * El LED 3, el ![icono de marca de verificación verde](./media/storsimple-controller-replacement/HCS_GreenCheckIcon.png) y el ![icono de cruz roja](./media/storsimple-controller-replacement/HCS_RedCrossIcon.png) están parpadeando, y el LED 0 y el LED 7 están **encendidos**.


Hello en la tabla siguiente muestra hello admitida escenarios de sustitución del controlador.

| Caso | Escenario de reemplazo | Procedimiento aplicable |
|:--- |:--- |:--- |
| 1 |Un controlador está en estado de error, hello otro controlador es correcto y activo. |[Único reemplazo de controlador](#replace-a-single-controller), que describe hello [lógica detrás de un reemplazo de controlador único](#single-controller-replacement-logic), así como de hello [pasos de sustitución](#single-controller-replacement-steps). |
| 2 |Ambos controladores Hola fallaron y requieren sustitución. chasis de Hello, discos y alojamiento de disco están en buenas condiciones. |[Sustitución de controlador doble](#replace-both-controllers), que describe hello [lógica detrás de un reemplazo de controlador doble](#dual-controller-replacement-logic), así como de hello [pasos de sustitución](#dual-controller-replacement-steps). |
| 3 |Controladores de Hola mismo dispositivo o se intercambian desde diferentes dispositivos. chasis de Hello, discos y alojamientos de disco están en buenas condiciones. |Aparecerá un mensaje de alerta de error de falta de coincidencia de ranura. |
| 4 |Falta un controlador y Hola otro se produce un error de controlador. |[Sustitución de controlador doble](#replace-both-controllers), que describe hello [lógica detrás de un reemplazo de controlador doble](#dual-controller-replacement-logic), así como de hello [pasos de sustitución](#dual-controller-replacement-steps). |
| 5 |Error de uno o ambos controladores. No se puede tener acceso a dispositivo de Hola a través de la consola serie de Hola o comunicación remota de Windows PowerShell. |[Póngase en contacto con el servicio técnico de Microsoft](storsimple-8000-contact-microsoft-support.md) para un procedimiento de reemplazo manual de los controladores. |
| 6 |controladores de Hello tienen una versión de compilación diferente, que puede ser debido a:<ul><li>Los controladores tienen una versión de software diferente.</li><li>Los controladores tienen una versión de firmware diferente.</li></ul> |Si son diferentes versiones de software de controlador de hello, lógica de sustitución de Hola detecta y actualizaciones Hola versión del software de controlador de sustitución de Hola.<br><br>Si son diferentes versiones de firmware del controlador de Hola y es la versión de firmware anterior hello **no** puede actualizar automáticamente, que aparecerá un mensaje de alerta en hello portal de Azure. Debe buscar actualizaciones e instalar las actualizaciones de firmware de Hola.</br></br>Si son diferentes versiones de firmware del controlador de Hola y es puede actualizar automáticamente la versión de firmware anterior hello, lógica de sustitución de controlador de hello lo detectará y, después de que se inicie el controlador de hello, firmware de Hola se actualizarán automáticamente. |

Deberá tooremove un módulo de controlador si ha producido un error. Uno o ambos módulos de controlador de hello pueden producir un error, lo que puede traducirse en una sustitución de controlador único o reemplazo de controlador doble. Para los procedimientos de reemplazo y lógica de hello detrás de ellos, vea Hola siguiente:

* [Reemplazar un único controlador](#replace-a-single-controller)
* [Reemplazar ambos controladores](#replace-both-controllers)
* [Quitar un controlador](#remove-a-controller)
* [Insertar un controlador](#insert-a-controller)
* [Identificar controlador activo de hello en el dispositivo](#identify-the-active-controller-on-your-device)

> [!IMPORTANT]
> Antes de quitar y reemplazar un controlador, revise la información de seguridad de hello en [sustitución de componentes de hardware de StorSimple](storsimple-8000-hardware-component-replacement.md).
> 
> 

## <a name="replace-a-single-controller"></a>Reemplazar un único controlador
Cuando uno de hello dos controladores de dispositivo de Microsoft Azure StorSimple Hola ha fallado, no funciona bien o falta, deberá tooreplace un único controlador.

### <a name="single-controller-replacement-logic"></a>Lógica de reemplazo de un único controlador
En una sustitución de controlador único, primero debe quitar Hola controlador con error. (Hola restantes en el dispositivo de hello es Hola controlador activo.) Cuando se inserta el controlador de sustitución de hello, hello realizan acciones siguientes:

1. controlador de sustitución de Hello empieza inmediatamente a comunicarse con el dispositivo de StorSimple Hola.
2. Una instantánea de hello disco virtual (VHD) para el controlador activo Hola se copia en el controlador de sustitución de Hola.
3. instantánea de Hola se modifica para que cuando se inicia en el controlador de sustitución de Hola desde este VHD, se reconocerá como un controlador en espera.
4. Cuando termine las modificaciones de hello, controlador de sustitución de Hola se iniciará como controlador en espera de Hola.
5. Cuando se ejecutan ambos controladores hello, clúster de hello pone en línea.

### <a name="single-controller-replacement-steps"></a>Pasos de reemplazo de un único controlador
Completar Hola siguientes pasos si se produce un error en uno de los controladores de hello en el dispositivo de StorSimple de Microsoft Azure. (hello otro controlador debe estar activo y ejecutándose. Si ambos controladores de errores o funcionan mal, vaya demasiado[pasos de sustitución de controlador doble](#dual-controller-replacement-steps).)

> [!NOTE]
> Puede tardar 30 y 45 minutos para hello controlador toorestart y recuperarse completamente de procedimiento de sustitución de controlador único Hola. tiempo total de Hola para todo procedimiento hello, incluida la conexión de cables de hello, es de aproximadamente 2 horas.


#### <a name="tooremove-a-single-failed-controller-module"></a>tooremove un módulo de controlador error único
1. Hola Azure portal, vaya toohello servicio de administrador de dispositivos de StorSimple, haga clic en **dispositivos**y, a continuación, haga clic en nombre de hello de dispositivo de Hola que desea toomonitor.
2. Vaya demasiado**Monitor > estado del Hardware**. estado de saludo del controlador 0 o controlador 1 debe ser rojo, lo que indica un error.
   
   > [!NOTE]
   > Hola controlador con error en una sustitución de controlador único siempre es un controlador en espera.
   
3. Utilice hello después de módulo de controlador con error de tabla toolocate Hola y la figura 1.
   
    ![Backplane de módulos del gabinete principal del dispositivo](./media/storsimple-controller-replacement/IC740994.png)
   
    **Figura 1** Parte posterior del dispositivo StorSimple
   
   | Etiqueta | Descripción |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Controlador 0 |
   | 4 |Controlador 1 |
4. En controlador con error hello, quite todos los cables de red de hello conectado de puertos de datos de Hola. Si está utilizando un modelo 8600, quitar también Hola que SAS cables que conectan el controlador de EBOD de hello controlador toohello.
5. Siga los pasos de hello en [quitar un controlador](#remove-a-controller) hello tooremove error al controlador.
6. Se quitó el repuesto de fábrica de instalación Hola Hola misma ranura de qué controlador errores de Hola. Esto desencadena la lógica de sustitución de controlador único Hola. Para más información, consulte la [lógica de reemplazo de un único controlador](#single-controller-replacement-logic).
7. Lógica de sustitución de controlador único Hola avanza en segundo plano de hello, vuelva a conectar los cables de Hola. Tomar tooconnect cuidado que Hola a todos los cables de hello exactamente igual que estaban conectados antes de sustitución de Hola.
8. Una vez reiniciado el controlador de hello, comprobar hello **estado del controlador** hello y **estado del clúster** en hello Azure tooverify portal que Hola controlador está en estado correcto tooa atrás y está en modo de espera.

> [!NOTE]
> Si va a supervisar dispositivos de Hola a través de la consola serie de hello, pueden producirse varios reinicios mientras controlador Hola se recupera del procedimiento de reemplazo de Hola. Cuando se presenta el menú de consola serie de hello, a continuación, sabrá que el reemplazo de hello ha finalizado. Si no aparece el menú de Hola dentro de dos horas a partir del comienzo de la sustitución de controlador de hello, [póngase en contacto con Microsoft Support](storsimple-8000-contact-microsoft-support.md).
>
> A partir de Update 4, también puede usar el cmdlet de Hola `Get-HCSControllerReplacementStatus` en la interfaz de Windows PowerShell de hello del estado de hello toomonitor hello de dispositivo del proceso de reemplazo de controlador de Hola.
> 

## <a name="replace-both-controllers"></a>Reemplazar ambos controladores
Cuando ambos controladores de dispositivo de Microsoft Azure StorSimple Hola han producido un error, un funcionamiento defectuoso o faltan, debe tooreplace ambos controladores. 

### <a name="dual-controller-replacement-logic"></a>Lógica de reemplazo de dos controladores
En un reemplazo de dos controladores, primero extraiga ambos controladores defectuoso y, a continuación, inserte reemplazos. Cuando se insertan dos controladores de sustitución hello, hello realizan acciones siguientes:

1. controlador de sustitución de Hello en la ranura 0 comprueba siguiente hello:
   
   1. ¿Está usando las versiones actuales de firmware de Hola y el software?
   2. ¿Es una parte del clúster de hello?
   3. Controlador del mismo nivel de hello ejecutando y está en el clúster?
      
      Si ninguna de estas condiciones son verdaderas, controlador de hello busca de copia de seguridad diaria hello más reciente (ubicado en hello **nonDOMstorage** en la unidad S). controlador de Hello copia instantánea más reciente de Hola de hello VHD de copia de seguridad de Hola.
2. controlador de Hello en la ranura 0 usa Hola instantánea tooimage propio.
3. Mientras tanto, controlador de hello en la ranura 1 espera para la creación de imágenes de controlador 0 toocomplete Hola y de inicio.
4. Una vez iniciado el controlador 0, el controlador 1 detecta clúster Hola creado por el controlador 0, lo que desencadena la lógica de sustitución de controlador único Hola. Para más información, consulte la [lógica de reemplazo de un único controlador](#single-controller-replacement-logic).
5. Después, ambos controladores estarán en ejecución y Hola clúster estará en línea.

> [!IMPORTANT]
> Después de una sustitución de controlador doble, una vez configurado el dispositivo de StorSimple de hello, es esencial que realice un manual de copia de seguridad del dispositivo de Hola. Las copias de seguridad de configuración de dispositivo diarias no se producen hasta después de que hayan transcurrido 24 horas. Trabajar con [Microsoft Support](storsimple-8000-contact-microsoft-support.md) toomake una copia de seguridad manual del dispositivo.


### <a name="dual-controller-replacement-steps"></a>pasos de reemplazo de dos controladores
Este flujo de trabajo es necesaria cuando ambos controladores de hello en el dispositivo StorSimple de Azure de Microsoft han fallado. Esto podría suceder en un centro de datos en el que sistema de refrigeración Hola deja de funcionar y, como resultado, ambos controladores Hola producirá un error en un breve período de tiempo. Dependiendo de si el dispositivo de StorSimple Hola se activa o desactiva y si está utilizando un 8600 o un modelo 8100, un conjunto diferente de pasos es obligatorio.

> [!IMPORTANT]
> Puede tardar 45 minutos too1 hora Hola controlador toorestart y recuperarse completamente de un procedimiento de reemplazo de controlador doble. tiempo total de Hola para todo procedimiento hello, incluida la conexión de cables de hello, es de aproximadamente 2,5 horas.

#### <a name="tooreplace-both-controller-modules"></a>tooreplace ambos módulos de controlador
1. Si se desactiva el dispositivo de hello, omita este paso y vaya toohello siguiente paso. Si está activado el dispositivo de hello, desactivar el dispositivo de Hola.
   
   1. Si está utilizando un modelo 8600, desactive la opción alojamiento principal de hello primero y, a continuación, desactive la opción Hola alojamiento de EBOD.
   2. Espere a que el dispositivo de Hola se apague por completo. Todos los LED de Hola Hola parte posterior del dispositivo de hello estará desactivada.
2. Quite todos los cables de red de Hola que están conectados toohello puertos de datos. Si está utilizando un modelo 8600, quitar también Hola que SAS cables que conectan el alojamiento de EBOD toohello de hello alojamiento principal.
3. Quite ambos controladores de dispositivo de StorSimple Hola. Para más información, consulte la sección sobre [cómo quitar un controlador](#remove-a-controller).
4. Inserte el repuesto de fábrica de Hola para controlador 0 en primer lugar y, a continuación, instale el controlador 1. Para más información, consulte la sección sobre [cómo insertar un controlador](#insert-a-controller). Esto desencadena la lógica de sustitución de controlador doble Hola. Para más información, consulte la [lógica de reemplazo de dos controladores](#dual-controller-replacement-logic).
5. Lógica de sustitución de controlador de hello avanza en segundo plano de hello, vuelva a conectar los cables de Hola. Tomar tooconnect cuidado que Hola a todos los cables de hello exactamente igual que estaban conectados antes de sustitución de Hola. Vea Hola instrucciones detalladas para el modelo en hello Cable de la sección de dispositivos de [instalar el dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md) o [instalar su dispositivo 8600 StorSimple](storsimple-8600-hardware-installation.md).
6. Encienda el dispositivo de StorSimple Hola. Si está usando un modelo 8600:
   
   1. Asegúrese de que ese Hola alojamiento de EBOD encender primero.
   2. Espere hasta que se ejecuta Hola alojamiento de EBOD.
   3. Encienda el alojamiento principal Hola.
   4. Primer controlador de hello reiniciado y en buen estado, Hola sistema estará en ejecución.
      
      > [!NOTE]
      > Si va a supervisar dispositivos de Hola a través de la consola serie de hello, pueden producirse varios reinicios mientras controlador Hola se recupera del procedimiento de reemplazo de Hola. Cuando aparezca el menú de consola serie de hello, a continuación, sabrá que el reemplazo de hello ha finalizado. Si no aparece el menú Hola plazo de 2,5 horas a partir del comienzo de la sustitución de controlador de hello, [póngase en contacto con Microsoft Support](storsimple-8000-contact-microsoft-support.md).
     
## <a name="remove-a-controller"></a>Quitar un controlador
Usar hello siguiendo el procedimiento tooremove un módulo del controlador dañado de dispositivo StorSimple.

> [!NOTE]
> Hola siguientes ilustraciones es para controlador 0. Para el controlador 1, estos se revertirán.


#### <a name="tooremove-a-controller-module"></a>tooremove un módulo de controlador
1. Tome el enganche del módulo Hola entre el pulgar y el índice.
2. Sacuda suavemente el pulgar y el índice juntos toorelease Hola enganche del controlador.
   
    ![Liberación del pestillo del controlador](./media/storsimple-controller-replacement/IC741047.png)
   
    **Figura 2** Liberación del pestillo del controlador
3. Usar bloqueos temporales de Hola como un controlador de identificador tooslide Hola fuera del chasis de Hola.
   
    ![Deslizamiento del controlador fuera del chasis](./media/storsimple-controller-replacement/IC741048.png)
   
    **Figura 3** deslizamiento del controlador Hola fuera del chasis de Hola

## <a name="insert-a-controller"></a>Insertar un controlador
Usar hello siguiendo el procedimiento tooinstall un módulo de controlador suministrado de fábrica después de quitar un módulo defectuoso del dispositivo StorSimple.

#### <a name="tooinstall-a-controller-module"></a>tooinstall un módulo de controlador
1. Comprobar toosee si hay cualquier toohello daños conectores de interfaz. No instale el módulo de hello si cualquiera de las patillas de conexión de hello está dañado o doblado.
2. Deslice el módulo de controlador de hello en el chasis de hello mientras Hola bloqueo completamente liberado.
   
    ![Deslizamiento del controlador hacia el chasis](./media/storsimple-controller-replacement/IC741053.png)
   
    **Figura 4** deslizamiento del controlador en el chasis de Hola
3. Inserta el módulo de controlador de hello, empezar cerrando bloqueo de hello al módulo de controlador de hello toopush ininterrumpido en el chasis de Hola. bloqueo de Hola se acoplará controlador de hello tooguide en su lugar.
   
    ![Cierre del pestillo del controlador](./media/storsimple-controller-replacement/IC741054.png)
   
    **Figura 5** cerrando bloqueo de controlador de Hola
4. Habrá terminado cuando el bloqueo de Hola se ajuste en su lugar. Hola **Aceptar** LED debe estar encendido.
   
   > [!NOTE]
   > Esta operación puede tardar too5 minutos para los controladores de Hola y Hola tooactivate LED.
  
5. tooverify que la sustitución de hello es correcta, Hola portal de Azure, vaya tooyour dispositivo y, a continuación, navegue demasiado**Monitor** > **estado del Hardware**y asegúrese de que los controladores 0 y controlador 1 están en buenas condiciones (el estado es verde).

## <a name="identify-hello-active-controller-on-your-device"></a>Identificar controlador activo de hello en el dispositivo
Hay muchas situaciones, como sustitución del registro o controlador de dispositivo por primera vez, que requieren que el controlador activo de hello toolocate en un dispositivo de StorSimple. controlador activo Hola procesa todas las operaciones Hola de redes y firmware de disco. Puede usar cualquiera de Hola siguiente controlador de métodos tooidentify Hola activo:

* [Usar controlador activo de hello tooidentify portal Azure Hola](#use-the-azure-portal-to-identify-the-active-controller)
* [Usar Windows PowerShell para el controlador activo de StorSimple tooidentify Hola](#use-windows-powershell-for-storsimple-to-identify-the-active-controller)
* [Comprobación de hello tooidentify dispositivo físico Hola controlador activo](#check-the-physical-device-to-identify-the-active-controller)

A continuación se describe cada uno de estos procedimientos.

### <a name="use-hello-azure-portal-tooidentify-hello-active-controller"></a>Usar controlador activo de hello tooidentify portal Azure Hola
En Hola portal de Azure, vaya tooyour dispositivo y, a continuación, demasiado**Monitor** > **estado del Hardware**y desplácese toohello **controladores** sección. Aquí puede comprobar qué controlador está activo.

![Identificación del controlador activo en Azure Portal](./media/storsimple-controller-replacement/IC752072.png)

**Figura 6** controlador activo de hello mostrando de portal de Azure

### <a name="use-windows-powershell-for-storsimple-tooidentify-hello-active-controller"></a>Usar Windows PowerShell para el controlador activo de StorSimple tooidentify Hola
Al acceder al dispositivo a través de la consola serie hello, se presenta un mensaje de pancarta. mensaje de pancarta Hello contiene información de dispositivos básicos como modelo hello, nombre, versión de software instalada y estado del controlador de Hola que está obteniendo acceso. Hola siguiente imagen muestra un ejemplo de un mensaje de pancarta:

![Mensaje de banner en serie](./media/storsimple-controller-replacement/IC741098.png)

**Figura 7** Mensaje de banner que muestra que el controlador 0 está Activo

Puede utilizar toodetermine de mensaje de pancarta Hola si Hola controlador se encuentra conectado toois activo o pasivo.

### <a name="check-hello-physical-device-tooidentify-hello-active-controller"></a>Comprobación de hello tooidentify dispositivo físico Hola controlador activo
controlador activo de tooidentify hello en el dispositivo, localice el LED azul de Hola anteriormente puerto Hola parte posterior del alojamiento principal de Hola Hola DATA 5.

Si este LED parpadea, hello controlador está activo y hello otro controlador está en modo de espera. Usar hello después de diagrama y de la tabla como ayuda.

![Plano anterior de la caja principal del dispositivo con los puertos de datos](./media/storsimple-controller-replacement/IC741055.png)

**Figura 8** Parte posterior del gabinete principal con los puertos de datos y LED de supervisión

| Etiqueta | Description |
|:--- |:--- |
| 1-6 |DATOS 0: 5 puertos de red |
| 7 |LED azul |

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre el [Reemplazo de los componentes de hardware de StorSimple](storsimple-8000-hardware-component-replacement.md).

