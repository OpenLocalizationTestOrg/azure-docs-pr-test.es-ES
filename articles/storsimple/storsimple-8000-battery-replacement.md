---
title: "batería de aaaReplace de dispositivo de la serie 8000 de StorSimple de Microsoft Azure | Documentos de Microsoft"
description: "Describe cómo reemplazar tooremove y mantener el módulo de batería de reserva de hello en el dispositivo StorSimple."
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
ms.openlocfilehash: 5ac767807e6c3fd817d8d522629db2aceaac9bdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a>Reemplazar el módulo de batería de reserva de hello en el dispositivo StorSimple

## <a name="overview"></a>Información general
alojamiento principal Hola Power y módulo de refrigeración (PCM) en el dispositivo de StorSimple de Microsoft Azure tiene un paquete de baterías adicional. Este módulo proporciona alimentación para que hello dispositivo StorSimple puede guardar los datos si hay pérdida de alojamiento principal de toohello de alimentación de CA. Este módulo de batería es que se hace referencia tooas hello *módulo de batería de reserva*. módulo de batería de reserva de Hello existe únicamente para el alojamiento principal de hello en el dispositivo StorSimple (Hola alojamiento de EBOD no contiene un módulo de batería de reserva).

Este tutorial explica cómo realizar lo siguiente:

* Quitar el módulo de batería de reserva de Hola
* Instalar un nuevo módulo de baterías de reserva
* Mantener el módulo de batería de reserva de Hola

> [!IMPORTANT]
> Antes de quitar y reemplazar un módulo de baterías de reserva, revise la información de seguridad de Hola Hola [sustitución de componentes de hardware de introducción tooStorSimple](storsimple-8000-hardware-component-replacement.md).


## <a name="remove-hello-backup-battery-module"></a>Quitar el módulo de batería de reserva de Hola
módulo de batería de reserva de Hello para el dispositivo StorSimple es una unidad reemplazable en campo. Antes de instalarla en hello PCM, módulo de baterías de hello debe almacenarse en su embalaje original. Realizar Hola después de batería de reserva de pasos tooremove Hola.

#### <a name="tooremove-hello-backup-battery-module"></a>módulo de batería de reserva de hello tooremove
1. Hola portal de Azure, vaya tooyour módulo de servicio de administrador de dispositivos de StorSimple. Vaya demasiado**dispositivos** y, a continuación, seleccione el dispositivo de la lista de Hola de dispositivos. Navegue demasiado**Monitor** > **estado del Hardware**. En **componentes compartidos**, mire Hola estado de batería Hola.
2. Identifique el PCM de hello en qué Hola batería ha fallado. La figura 1 muestra hello parte posterior del dispositivo de StorSimple Hola.
   
    ![Backplane de módulos del gabinete principal del dispositivo](./media/storsimple-battery-replacement/IC740994.png)
   
    **Figura 1** Vista posterior del dispositivo primario que muestra los módulos PCM y del controlador
   
   | Etiqueta | Descripción |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Controlador 0 |
   | 4 |Controlador 1 |
   
    Como se muestra en el número 3 en la figura 2 hello, Hola supervisión indicador LED en PCM 0 que corresponde demasiado**error de batería** debe estar encendido.
   
    ![Backplane de supervisión de LED indicadores de supervisión del PCM del dispositivo](./media/storsimple-battery-replacement/IC740992.png)
   
    **Figura 2** Hola de mostrando parte posterior del PCM LED indicadores de supervisión
   
   | Etiqueta | Descripción |
   |:--- |:--- |
   | 1 |Error de corriente alterna |
   | 2 |Error del ventilador |
   | 3 |Error de la batería |
   | 4 |PCM correcto |
   | 5 |Error de alimentación de CD |
   | 6 |Batería en funcionamiento |
3. Hola tooremove PCM con una batería averiada, siga los pasos de hello en [quite el PCM con](storsimple-power-cooling-module-replacement.md#remove-a-pcm).
4. Con hello PCM extraído, elevación y batería Hola girar módulo controlar hacia arriba tal como se indica en la figura siguiente de Hola y extraer la batería de hello tooremove.
   
    ![Quitar batería del PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    **Figura 3** quitando batería de Hola de hello PCM
5. Coloque el módulo de hello en unidad reemplazable en campo Hola empaquetado.
6. Devolver Hola unidad defectuosa tooMicrosoft de servicio y gestión adecuados.

## <a name="install-a-new-backup-battery-module"></a>Instalar un nuevo módulo de baterías de reserva
Realizar Hola después de módulo de baterías de sustitución pasos tooinstall hello en Hola PCM del alojamiento principal de hello de dispositivo StorSimple.

#### <a name="tooinstall-hello-battery-module"></a>módulo de baterías de hello tooinstall
1. Coloque el módulo de batería de reserva de hello en la orientación correcta de Hola Hola PCM.
2. Presione hacia abajo el módulo de baterías de hello controlar conector de todas las Hola forma tooseat Hola.
3. Reemplace Hola PCM en el alojamiento principal Hola siguiendo las instrucciones de hello en [reemplazar una alimentación y refrigeración módulo en el dispositivo StorSimple](storsimple-power-cooling-module-replacement.md).
4. Una vez completada la sustitución de hello, vaya tooyour dispositivo y, a continuación, vaya demasiado**Monitor** > **estado del Hardware** Hola portal de Azure. Comprobar estado de Hola de hello batería toomake seguro de que Hola instalación es correcta. Estado verde indica que la batería de hello es correcto.

## <a name="maintain-hello-backup-battery-module"></a>Mantener el módulo de batería de reserva de Hola
En el dispositivo StorSimple, módulo de batería de reserva de hello proporciona controlador toohello de energía durante un evento de pérdida de energía. Permite hello StorSimple dispositivo toosave datos críticos anterior tooshutting hacia abajo de una manera controlada. Con dos baterías totalmente cargadas en hello PCM, sistema de hello puede controlar dos eventos de corte consecutivos.

Hola portal de Azure, Hola **estado del Hardware** en hello **Monitor** hoja indica si está funcionando mal batería Hola o de obsolescencia de saludo se está agotando. estado de la batería de Hola se indica mediante **batería en PCM 0** o **batería en PCM 1** en **componentes compartidos**. Esta hoja muestra un estado **DEGRADADO** cuando se aproxima el final del ciclo de vida, y **ERROR** cuando se alcanza el final del ciclo de vida.

> [!NOTE]
> Hola batería puede mostrar **error** cuando necesita simplemente toobe cobra.


Si hello **degradado** aparece estado, se recomienda Hola siguiendo el curso de acción:

* sistema de Hola que haya tenido una pérdida de energía reciente o baterías Hola pueden se está llevando a cabo mantenimiento periódico. Observe el sistema de Hola durante 12 horas antes de continuar.
  
  * Si el estado de hello sigue siendo **degradado** después de 12 horas de alimentación de tooAC de conexión continua con hello de controladores y PCM en ejecución, a continuación, Hola batería debe toobe reemplazado. [Póngase en contacto con Microsoft Support](storsimple-8000-contact-microsoft-support.md) para obtener un módulo de baterías de reserva de reemplazo.
  * Si se convierte en un estado de hello correcto después de 12 horas, batería Hola está operativo y solo necesita un coste de mantenimiento.
* Si no ha habido un corte de alimentación de CA y Hola PCM asociado esté encendido y conectado tooAC power, batería Hola debe toobe reemplazado. [Póngase en contacto con Microsoft Support](storsimple-8000-contact-microsoft-support.md) tooorder un módulo de batería de reserva de reemplazo.

> [!IMPORTANT]
> Dispose de hello error batería según toonational y la normativa regional.

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre el [Reemplazo de los componentes de hardware de StorSimple](storsimple-8000-hardware-component-replacement.md).

