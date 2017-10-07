---
title: "sustitución de componentes de hardware aaaStorSimple | Documentos de Microsoft"
description: "Describe cómo reemplazar el toosafely Hola PCM, batería, módulos de controlador, controladores EBOD, unidades de disco y chasis de un dispositivo de StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e8087ba7-0b66-4f59-8988-e53aad52ee21
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 472d9dc1c31b61550fe079cc9b9419510487db3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-hardware-component-on-your-storsimple-8000-series-device"></a>Sustitución de un componente de hardware en el dispositivo StorSimple serie 8000

## <a name="overview"></a>Información general
tutoriales de reemplazo de componentes de hardware de Hola describen los componentes de hardware de Hola de su Microsoft Azure StorSimple 8000 series hello y dispositivo pasos necesario tooremove y reemplazan. En este artículo se describen los iconos de seguridad de hello, proporciona punteros toohello detallados tutoriales y listas de Hola componentes que son reemplazables.

> [!IMPORTANT]
> Antes de intentar tooremove o reemplace cualquier componente de StorSimple, asegúrese de que revisa hello [convenciones de iconos de seguridad](#safety-icon-conventions) y otros [precauciones de seguridad](storsimple-safety.md).
> 
> 

### <a name="safety-icon-conventions"></a>Convenciones de iconos de seguridad
Hello tabla siguiente describen los iconos de seguridad Hola utilizados en estos tutoriales. Preste mucha atención iconos de seguridad toothese a medida que vaya a través de hello pasos tooremove y reemplaza los componentes del dispositivo.

| Icono | Texto | Información adicional |
|:--- |:--- |:--- |
| ![Icono Advertencia](./media/storsimple-hardware-component-replacement/Warning.png) |**PELIGRO** |Indica una situación peligrosa que, si no se evita, causará la muerte o lesiones graves. Esta palabra de aviso es situaciones más extremas toohello limitado. |
| ![Icono Advertencia](./media/storsimple-hardware-component-replacement/Warning.png) |**¡ADVERTENCIA** |Indica una situación peligrosa que, si no se evita, podría causar la muerte o lesiones graves. |
| ![Icono Precaución](./media/storsimple-hardware-component-replacement/Caution.png) |**PRECAUCIÓN** |Indica una situación peligrosa que, si no se evita, podría causar lesiones leves o graves. |
| ![Icono Aviso](./media/storsimple-hardware-component-replacement/NoticeIcon.png) |**AVISO:** |Indica información considerada importante, pero no relacionada con la peligrosidad. |
| ![Icono Descarga eléctrica](./media/storsimple-hardware-component-replacement/Electric.png) |**Peligro de descarga eléctrica** |Indica alto voltaje. |
| ![Icono Peso pesado](./media/storsimple-hardware-component-replacement/Weight.png) |**Peso pesado** | |
| ![Icono No contiene piezas reparables por el usuario](./media/storsimple-hardware-component-replacement/NoUserServiceableParts.png) |**No contiene piezas reparables por el usuario** |No acceder sin la formación adecuada. |
| ![Icono Leer instrucciones](./media/storsimple-hardware-component-replacement/ReadInstructions.png) |**Lea todas las instrucciones primero** | |
| ![Icono Sugerencia peligrosa](./media/storsimple-hardware-component-replacement/TipHazard.png) |**Sugerencia peligrosa** | |

### <a name="before-you-begin"></a>Antes de empezar
Familiarícese con la información de seguridad de hello acerca de los iconos de dispositivo y de seguridad utilizado en este tutorial. Vaya demasiado[con seguridad, instalar y utilizar su dispositivo StorSimple](storsimple-safety.md) para obtener información completa. Estar seguro de hello tooreview [precauciones de seguridad](storsimple-safety.md#handling-precautions) antes de controlar el dispositivo StorSimple. 

Antes de intentar tooreplace un componente, considere la posibilidad de hello siguiente información.

![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png)![Electrical Shock Icon](./media/storsimple-hardware-component-replacement/Electric.png)**¡ADVERTENCIA** 

* Conecte una buena descarga a tierra en sí mismo mediante una descarga electrostática o alfombra antiestática al manipular los módulos y los componentes del dispositivo StorSimple.
* No toque los circuitos. Usar identificadores de hello proporcionado y guías de manipular componentes que puedan tener circuitos expuestos.

![Warning Icon](./media/storsimple-hardware-component-replacement/Warning.png)![Notice Icon](./media/storsimple-hardware-component-replacement/NoticeIcon.png)**AVISO:**

Al reemplazar un módulo, **nunca deje un receptáculo vacío en la parte posterior de hello del alojamiento de hello**. Obtenga un recambio o módulo vacío antes de quitar la parte con problemas Hola.

## <a name="hardware-component-replacement-procedures"></a>Procedimientos de reemplazo de los componentes de hardware
El dispositivo de la serie StorSimple 8000 consta de varios módulos de complemento principal de Hola o alojamientos de EBOD. Hola 8100 tiene un único alojamiento principal, mientras que Hola 8600 es un dispositivo de doble alojamiento con un alojamiento principal y alojamiento de EBOD.

en hello las tablas siguientes se resumen los componentes de hardware principales de Hello en el dispositivo. Haga clic en el vínculo de Hola Hola **procedimiento de sustitución** columna toogo toohello asociados tutorial.

| Componentes | # Present | ¿Módulo de complemento? | Procedimiento de reemplazo |
|:--- |:--- |:--- |:--- |
| Chasis |1 |No |[Reemplazar el chasis de hello en el dispositivo StorSimple](storsimple-chassis-replacement.md) |
| Controladores principales |2 |Sí |[Reemplazar un módulos de controladores en el dispositivo StorSimple](storsimple-controller-replacement.md) |
| Módulos de alimentación y refrigeración (PCM) de 764 W |2 |Sí |[Reemplazar un Módulo de alimentación y de refrigeración en el dispositivo StorSimple](storsimple-power-cooling-module-replacement.md) |
| Batería de reserva |2 |Sí |[Reemplazar el módulo de batería de reserva de hello en el dispositivo StorSimple](storsimple-battery-replacement.md) |
| Unidades de disco |12 |Sí |[Reemplazar un disco duro en el dispositivo StorSimple](storsimple-disk-drive-replacement.md) |

**Tabla 1** componentes de Hardware de alojamiento principal Hola

alojamiento principal de Hola y el alojamiento de EBOD Hola difieren en sus módulos de E/S. Además, PCM Hola vataje distinto. Hola PCM en el alojamiento principal Hola 764 W, mientras que los de hello alojamiento de EBOD son de 580 w. PCM Hola Hola principal alojamiento también contienen un módulo de batería de reserva.

| Componentes | # Present | ¿Módulo de complemento? | Procedimiento de reemplazo |
|:--- |:--- |:--- |:--- |
| Chasis |1 |No |[Reemplazar el chasis de hello en el dispositivo StorSimple](storsimple-chassis-replacement.md) |
| Controladores EBOD |2 |Sí |[Reemplazar un controlador EBOD en el dispositivo StorSimple](storsimple-ebod-controller-replacement.md) |
| Módulos de alimentación y refrigeración (PCM) de 580 W |2 |Sí |[Reemplazar un Módulo de alimentación y de refrigeración en el dispositivo StorSimple](storsimple-power-cooling-module-replacement.md) |
| Unidades de disco |12 |Sí |[Reemplazar un disco duro en el dispositivo StorSimple](storsimple-disk-drive-replacement.md) |

**Tabla 2** componentes de Hardware de hello alojamiento de EBOD

módulos de complemento de Hello en dispositivo Hola se resaltan en hello después diagramas frontales y traseros. Puede utilizar estos ubicación de Hola de diagramas toodetermine de hello distintos módulos de complemento si es necesaria su sustitución. diagrama frontal Hello muestra las unidades de disco de hello, Hola diagramas y posterior de hello EBOD alojamiento y alojamiento principal Hola mostrar hello módulos plug-in.

![Plano frontal de dispositivo con unidades de disco](./media/storsimple-hardware-component-replacement/IC741028.png)

**Figura 1** parte frontal del dispositivo de Hola

| Etiqueta | Description |
|:--- |:--- |
| 0 - 11 |Unidades de discos (total de 12) |

Alojamiento principal de Hola y el alojamiento de EBOD Hola tienen módulos portadores de unidades. chasis de Hello aloja doce 3,5" unidades de disco en un formato de 3 por 4.

![Backplane de módulos del gabinete principal del dispositivo](./media/storsimple-hardware-component-replacement/IC740994.png)

**Figura 2** parte posterior del alojamiento principal Hola

| Etiqueta | Descripción |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |Controlador 0 |
| 4 |Controlador 1 |

![Backplane de módulos de complementos del gabinete EBOD del dispositivo](./media/storsimple-hardware-component-replacement/IC769599.png)

**Figura 3** reverso Hola alojamiento de EBOD

| Etiqueta | Descripción |
|:--- |:--- |
| 1 |PCM 0 |
| 2 |PCM 1 |
| 3 |Controlador EBOD 0 |
| 4 |Controlador EBOD 1 |

## <a name="field-replaceable-units"></a>Unidades reemplazables en campo
Hola siguientes unidades reemplazables en campo (FRU) está disponible para el dispositivo StorSimple:

* Chasis (incluido el panel de las operaciones integradas de hello)
* PCM de 764 W de CA
* PCM de 580 W de CA
* Unidad de disco duro con módulo transportador de unidades
* Módulos de controladores
* Módulos de controladores EBOD
* Módulo de batería de reserva
* Kit de guías de montaje en bastidor

Por favor, [póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) tooorder cualquiera de estas unidades de sustitución.

## <a name="next-steps"></a>Pasos siguientes
Revise todas [información de seguridad](storsimple-safety.md) antes de intentar tooreplace un componente de hardware de StorSimple.

