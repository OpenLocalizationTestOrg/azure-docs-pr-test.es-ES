---
title: aaaReplace un PCM en el dispositivo StorSimple | Documentos de Microsoft
description: "Explica cómo tooremove y reemplazar Hola de alimentación y módulo de refrigeración (PCM) en el dispositivo StorSimple"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 24a158cb-0b79-4908-bb5a-431e48760f6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: cc19ccb29884557720f7538b90dfb05268330b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a>Reemplazar un Módulo de alimentación y de refrigeración en el dispositivo StorSimple
## <a name="overview"></a>Información general
Hola Power y módulo de refrigeración (PCM) en el dispositivo de StorSimple de Microsoft Azure consta de una fuente de alimentación y ventiladores de refrigeración que se controlan a través de los alojamientos EBOD y Hola principal. Hay un único modelo de PCM que está certificado para cada gabinete. alojamiento principal Hola está certificado para un PCM de 764 W y alojamiento de EBOD Hola está certificado para un PCM de 580 W. Aunque hello PCM para el alojamiento principal de Hola y el alojamiento de EBOD Hola son diferentes, el procedimiento de sustitución de hello es idéntico.

Este tutorial explica cómo realizar lo siguiente:

* Quitar un PCM
* Instalar un PCM de reemplazo

> [!IMPORTANT]
> Antes de quitar y reemplazar un PCM, revise la información de seguridad de hello en [sustitución de componentes de hardware de StorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="before-you-replace-a-pcm"></a>Antes de reemplazar un PCM
Tenga en cuenta Hola después problemas importantes antes de sustituir su PCM:

* Si Hola de alimentación de Hola se produce un error de PCM, deje instalado de módulo con hello, pero quitar el cable de alimentación de Hola. ventilador de Hello continuará corriente de tooreceive de alojamiento de Hola y continuar la refrigeración adecuada de tooprovide. Si se produce un error en el ventilador de hello, Hola PCM debe toobe sustituye de forma inmediata.
* Antes de quitar Hola PCM, desconecte power Hola Hola PCM si se desactiva el interruptor principal hello (si está presente) o retirando físicamente el cable de alimentación de Hola. Esto proporciona un sistema de tooyour de advertencia que un corte del suministro es inminente.
* Asegúrese de que ese Hola para que otro PCM es funcional continuar la operación del sistema antes de reemplazar Hola PCM con el. Tan pronto como sea posible, un PCM defectuoso debe sustituirse por un PCM totalmente operativo.
* Sustitución del módulo PCM toma solo algunos minutos toocomplete, pero debe realizarse dentro de 10 minutos de la eliminación de hello no se pudo PCM tooprevent sobrecalentamiento.
* Tenga en cuenta que Hola reemplazo 764 W PCM los módulos enviados de fábrica de hello no contienen módulo de batería de reserva de Hola. Deberá batería de hello tooremove desde el PCM con el error y, a continuación, insertarlo en sustitución de Hola de tooperforming anterior del módulo de reemplazo de Hola. Para obtener más información, vea cómo demasiado[quitar e inserte un módulo de batería de reserva](storsimple-battery-replacement.md).

## <a name="remove-a-pcm"></a>Quitar un PCM
Siga estas instrucciones cuando esté listo tooremove una potencia y módulo de refrigeración (PCM) de su dispositivo de StorSimple de Microsoft Azure.

> [!NOTE]
> Antes de quitar el PCM, compruebe que dispone de otro correcto para sustituirlo (764 W para el alojamiento principal hello) o 580 W para hello alojamiento de EBOD.
> 
> 

#### <a name="tooremove-a-pcm"></a>tooremove un PCM
1. Hola portal de Azure clásico, haga clic en **dispositivos** > **mantenimiento** > **estado del Hardware**. Comprobar el estado de Hola de componentes de PCM de hello en **componentes compartidos** tooidentify que ha fallado PCM:
   
   * Si se produce un error en una fuente de alimentación en PCM 0, Hola estado de **fuente de alimentación en PCM 0** será rojo.
   * Si se produce un error en una fuente de alimentación en PCM 1, Hola estado de **fuente de alimentación en PCM 1** será rojo.
   * Si se produce un error de ventilador de hello en PCM 1, Hola estado **refrigeración 0 para PCM 0** o **refrigeración 1 para PCM 0** será rojo.
2. Busque Hola PCM con error en hello realizar copia del alojamiento principal Hola. Si va a ejecutar un modelo 8600, identificar el alojamiento principal de Hola examinando Hola número de identificación de unidad de sistema se muestra en pantalla LED del panel frontal de Hola. Hola predeterminado es Id. de unidad que se muestra en el alojamiento principal hello **00**, mientras que el valor predeterminado de hello Id. de unidad se muestra en hello alojamiento de EBOD es **01**. Hello diagrama y la tabla siguientes explican panel frontal de Hola de pantalla de hello LED.
   
    ![Identificador del sistema en el panel frontal OPS](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     **Figura 1** panel frontal del dispositivo de Hola  
   
   | Etiqueta | Descripción |
   |:--- |:--- |
   | 1 |Botón Silencio |
   | 2 |Alimentación del sistema |
   | 3 |Error de módulo |
   | 4 |Error lógico |
   | 5 |Pantalla de identificación de la unidad |
3. Hola LED indicador Hola parte posterior del alojamiento principal Hola de supervisión también puede utilizarse tooidentify Hola PCM con el error. Vea Hola siguiente diagrama y tabla toounderstand cómo toouse Hola LED toolocate Hola PCM con el error. Por ejemplo, si hello LED correspondiente toohello **error de ventilador** está encendido, ventilador Hola ha producido un error. Del mismo modo, si hello LED correspondiente demasiado**error de CA** está encendido, fuente de alimentación de hello ha producido un error. 
   
    ![Backplane de LED indicadores de supervisión del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     **Figura 2** Parte posterior del PCM con LED indicadores
   
   | Etiqueta | Descripción |
   |:--- |:--- |
   | 1 |Error de corriente alterna |
   | 2 |Error del ventilador |
   | 3 |Error de la batería |
   | 4 |PCM correcto |
   | 5 |Error de alimentación de CD |
   | 6 |Batería en funcionamiento |
4. Consulte toohello siguiente diagrama de hello parte posterior del módulo PCM en hello StorSimple dispositivo toolocate Hola error. PCM 0 está a la izquierda de Hola y PCM 1 consiste en hello derecho. tabla de Hello siguiente explica los módulos de Hola.
   
     ![Backplane de módulos del gabinete principal del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     **Figura 3** Parte posterior de dispositivo con módulos de complementos 
   
   | Etiqueta | Descripción |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Controlador 0 |
   | 4 |Controlador 1 |
5. Activar Hola PCM con el error y desconecte la fuente de alimentación de Hola. Ahora puede quitar Hola PCM.
6. Tome los bloqueos temporales de Hola y Hola de hello PCM controlar entre el pulgar y el índice y apriételos identificador de hello tooopen juntos.
   
    ![Abrir el asa del PCM](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    **Figura 4** controlar Hola de apertura PCM
7. Agarre el identificador hello y quite Hola PCM.
   
    ![Quitar PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    **Figura 5** Removing Hola PCM

## <a name="install-a-replacement-pcm"></a>Instalar un PCM de reemplazo
Siga estos tooinstall instrucciones un PCM en el dispositivo StorSimple. Asegúrese de que haya insertado Hola batería de reserva módulo anterior tooinstalling Hola PCM de sustitución (se aplica solo PCM W de too764). Para obtener más información, vea cómo demasiado[quitar e inserte un módulo de batería de reserva](storsimple-battery-replacement.md).

#### <a name="tooinstall-a-pcm"></a>tooinstall un PCM
1. Compruebe que dispone de hello PCM de reemplazo correcto para este alojamiento. alojamiento principal Hola necesita un PCM de 764 W y Hola alojamiento de EBOD necesita un PCM de 580 W. No debería intentar toouse Hola PCM de 580 W alojamiento principal de Hola u Hola PCM de 764 W Hola alojamiento de EBOD. Hola siguiente imagen muestra donde tooidentify esta información en hello decir etiqueta pegada toohello PCM.
   
    ![Etiqueta del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    **Figura 6** Etiqueta del PCM
2. Busque el alojamiento de toohello de daños, prestando especial atención toohello conectores. 
   
   > [!NOTE]
   > **No instale el módulo de hello si algún pasador del conector está doblado.**
   > 
   > 
3. Con hello PCM controlar Hola abra posición, módulo de diapositiva hello en el alojamiento de Hola.
   
    ![Instalación del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    **Figura 7** instalar Hola PCM
4. Cierre manualmente el asa del PCM Hola. Debe oír un clic cuando se acople el cierre del asa Hola. 
   
   > [!NOTE]
   > tooensure que Hola patillas de conexión se han acoplado, puede tirar suavemente en hello identificador sin liberar el bloqueo temporal de Hola. Si Hola PCM se desliza hacia afuera, se referirá a que ese bloqueo Hola se cerró antes de conectores de hello ocupado.
   > 
   > 
5. Conecte la fuente de alimentación de toohello de cables de alimentación de Hola y toohello PCM.
6. Proteger una demanda Hola balas de relieve. 
7. Activar Hola PCM.
8. Reemplazo de hello fue correcta: Hola portal de Azure clásico de su servicio StorSimple Manager, navegue demasiado**dispositivos** > **mantenimiento**  >  **Estado del hardware**. En **componentes compartidos**, estado de Hola de hello PCM debe ser verde. 
   
   > [!NOTE]
   > Puede tardar unos minutos para la inicialización de toocompletely PCM de reemplazo de Hola.
   > 
   > 

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre el [Reemplazo de los componentes de hardware de StorSimple](storsimple-hardware-component-replacement.md).

