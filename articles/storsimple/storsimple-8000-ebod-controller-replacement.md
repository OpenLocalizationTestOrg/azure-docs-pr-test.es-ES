---
title: un controlador de StorSimple 8600 EBOD aaaReplace | Documentos de Microsoft
description: "Explica cómo tooremove y reemplazar uno o ambos controladores EBOD en un dispositivo de StorSimple 8600."
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
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 8343ed6f48ae97fc9204452f85e1936bfb1d6919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a>Reemplazar un controlador EBOD en el dispositivo StorSimple

## <a name="overview"></a>Información general
Este tutorial le explica cómo tooreplace un módulo de controlador EBOD defectuoso en el dispositivo de StorSimple de Microsoft Azure. tooreplace un módulo de controlador EBOD, necesitará:

* Quitar el controlador EBOD dañado Hola
* Instalar un nuevo controlador EBOD

Considere la posibilidad de hello siguiente información antes de empezar:

* Los módulos EBOD vacíos deben insertarse en todas las ranuras sin usar. Hola alojamiento no se refrigerará correctamente si una ranura queda abierta.
* controlador de EBOD Hello es intercambiable en caliente y se puede quitar o reemplazar. No quite un módulo defectuoso hasta que tenga un reemplazo. Cuando se inicia el proceso de reemplazo de hello, debe completarlo en el plazo de 10 minutos.

> [!IMPORTANT]
> Antes de intentar tooremove o reemplace cualquier componente de StorSimple, asegúrese de que revisa hello [convenciones de iconos de seguridad](storsimple-safety.md#safety-icon-conventions) y otros [precauciones de seguridad](storsimple-safety.md).

## <a name="remove-an-ebod-controller"></a>Quitar un controlador EBOD
Antes de reemplazar Hola error módulo del controlador EBOD en el dispositivo StorSimple, asegúrese de que ese Hola otro módulo de controlador EBOD esté activo y en funcionamiento. Hello procedimiento y la tabla siguientes explican cómo tooremove Hola módulo del controlador EBOD.

#### <a name="tooremove-an-ebod-module"></a>tooremove un módulo de EBOD
1. Hola abrir portal de Azure.
2. Vaya tooyour dispositivos del sistema y desplácese demasiado**configuración** > **estado del Hardware**y compruebe el estado Hola de hello LED de hello módulo del controlador es verde y hello LED para hello no se pudo Módulo de controlador EBOD está en rojo.
3. Busque el módulo del controlador EBOD de hello no se pudo en hello parte posterior del dispositivo de Hola.
4. Quite los cables de Hola que conectan el controlador toohello módulo de hello EBOD controlador antes de realizar el módulo de EBOD de hello del sistema de Hola.
5. Tome nota del puerto SAS exacto de Hola de módulo del controlador EBOD Hola que estaba conectado toohello controlador. Será necesario toorestore configuración de toothis del sistema de hello después de reemplazar el módulo EBOD Hola.
   
   > [!NOTE]
   > Normalmente, se trata de puerto A, que se etiqueta como **hospedar en** Hola siguiente diagrama.
   
    ![Plano anterior del controlador EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     **Figura 1** Parte posterior del módulo EBOD
   
   | Etiqueta | Descripción |
   |:--- |:--- |
   | 1 |LED de error |
   | 2 |LED de encendido |
   | 3 |Conectores SAS |
   | 4 |LED SAS |
   | 5 |Puertos en serie para uso en fábrica únicamente |
   | 6 |Puerto A (Alojar en) |
   | 7 |Puerto B (Alojar en) |
   | 8 |Puerto C (solo para uso de fábrica) |

## <a name="install-a-new-ebod-controller"></a>Instalar un nuevo controlador EBOD
Hello procedimiento y la tabla siguientes explican cómo tooinstall un módulo de controlador EBOD en el dispositivo StorSimple.

#### <a name="tooinstall-an-ebod-controller"></a>tooinstall un controlador de EBOD
1. Compruebe hello EBOD del dispositivo si hay daños, especialmente el conector de interfaz toohello. No instale el nuevo controlador de EBOD Hola si algún pasador está doblado.
2. Con bloqueos temporales de Hola Hola abra posición, módulo de diapositiva hello en el alojamiento de hello hasta Hola bloqueos se acoplen.
   
    ![Instalación del controlador EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    **Figura 2** instalar Hola controlador de ebod
3. Bloqueo de cierre Hola. Debe oír un clic cuando se acople el bloqueo temporal de Hola.
   
    ![Liberación del pestillo EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    **Figura 3** cerrando bloqueo de módulo EBOD Hola
4. Vuelva a conectar los cables de Hola. Usar configuración exacta de Hola que ya estaba presente antes de sustitución de Hola. Vea Hola después de diagrama y de la tabla para obtener más información acerca de cómo los cables de hello tooconnect.
   
    ![Cableado del dispositivo 4U para alimentación](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    **Figura 4**. Reconexión de los cables
   
   | Etiqueta | Descripción |
   |:--- |:--- |
   | 1 |Receptáculo principal |
   | 2 |PCM 0 |
   | 3 |PCM 1 |
   | 4 |Controlador 0 |
   | 5 |Controlador 1 |
   | 6 |Controlador EBOD 0 |
   | 7 |Controlador EBOD 1 |
   | 8 |Receptáculo EBOD |
   | 9 |Unidades de distribución de energía |

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre el [Reemplazo de los componentes de hardware de StorSimple](storsimple-8000-hardware-component-replacement.md).

