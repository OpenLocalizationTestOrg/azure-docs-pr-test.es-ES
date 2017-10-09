---
title: aaaStorSimple 8000 componentes de hardware de la serie y el estado | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomonitor Hola componentes de hardware del dispositivo de StorSimple a través del servicio Administrador de dispositivos de StorSimple Hola."
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
ms.date: 04/04/2017
ms.author: alkohli
ms.openlocfilehash: 85b398e4b1a6b8921792b8945331325940082eb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomonitor-hardware-components-and-status"></a>Utilizar componentes de hardware de toomonitor de servicio de administrador de dispositivos de StorSimple de Hola y estado
## <a name="overview"></a>Información general
Este artículo describe Hola distintos componentes físicos y lógicos en el dispositivo local de la serie StorSimple 8000. También se explica cómo toomonitor Hola estado del componente de dispositivo mediante el uso de hello **estado de hardware y estado** hoja Hola servicio Administrador de dispositivos de StorSimple.

Hola **estado de hardware y estado** hoja muestra el estado de hardware de Hola de todos los componentes del dispositivo de StorSimple Hola.

En la lista de Hola de componentes para 8100, hay tres secciones que describen:

* **Componentes compartidos** : estos no son parte de controladores de hello, como unidades de disco, alojamiento, componentes PCM y temperatura PCM, tensión de línea y sensores de corriente de línea.
* **Componentes del controlador 0** : componentes de Hola que residen en el controlador 0, por ejemplo, el controlador, expansor y conector SAS, sensores de temperatura del controlador y Hola varias interfaces de red.
* **Componentes del controlador 1** : Hola componentes que constituyen el controlador 1, similar toothose detallado en el controlador 0.

Un dispositivo 8600 tiene componentes adicionales que se corresponden toohello alojamiento extendido grupo de discos (EBOD). En la lista de Hola de componentes, hay cinco secciones. De estos, hay tres secciones que contienen componentes de hello en el alojamiento principal de Hola y son idéntico toohello las descritas para 8100. Hay dos secciones adicionales para hello alojamiento de EBOD que describen:

* **Componentes del controlador de EBOD 0** : Hola componentes que residen en el alojamiento de EBOD 0, tales como controlador EBOD hello, sensores de temperatura de expansor y conector y controlador SAS.
* **Componentes de 1 del controlador de EBOD** : Hola componentes que constituyen el alojamiento de EBOD 1, toothose similar detallados en el alojamiento de EBOD 0.
* **Componentes compartidos de alojamiento EBOD** : componentes de hello presentes en el alojamiento de EBOD hello y PCM que no forman parte del controlador de EBOD Hola.

> [!NOTE]
> **estado de hardware de Hello no está disponible para un dispositivo de nube de StorSimple (8010/8020).**


## <a name="monitor-hello-hardware-status"></a>Supervisar el estado del hardware Hola
Lleve a cabo Hola después de estado de hardware de pasos tooview Hola de un componente de dispositivo:

1. Navegue demasiado**dispositivos**, seleccione un dispositivo de StorSimple específico. Vaya demasiado**Monitor > estado del Hardware**.

    ![](./media/storsimple-8000-monitor-hardware-status/hw-health1.png)

2. Busque hello **componentes de Hardware** sección y elija una de los componentes disponibles de Hola. Simplemente haga clic en lista de hello componentes etiqueta tooexpand hello y ver estado de Hola de hello diversos componentes del dispositivo. Vea hello [lista de componentes detallados para el alojamiento principal hello](#component-list-for-primary-enclosure-of-storsimple-device) hello y [lista de componentes detallados para hello alojamiento de EBOD](#component-list-for-ebod-enclosure-of-storsimple-device).

    ![](./media/storsimple-8000-monitor-hardware-status/hw-health2.png)

3. Usar hello siguiendo el estado del componente de hello toointerpret del esquema de codificación de color:
   
   * **Marca de verificación verde**: denota un componente correcto con estado **OK**.
   * **Amarillo**: denota un componente degradado en estado de **Advertencia**.
   * **Signo de exclamación rojo**: denota un componente erróneo que tiene un estado de **Error**.
   * **Blanco con texto negro** : denota un componente que no está presente.
   
   Hello captura de pantalla siguiente muestra un dispositivo que tiene componentes de **Aceptar**, **advertencia**, y **error** estado.
       
   ![](./media/storsimple-8000-monitor-hardware-status/hw-health3.png)

   Hola expansión **lista de componentes compartidos**, podemos ver ese clúster NVRAM y Hola Hola se degradan.

   ![](./media/storsimple-8000-monitor-hardware-status/hw-health5.png)

   Hola expansión **componentes del controlador 1** lista, podemos ver error ese nodo de clúster Hola.  

   ![](./media/storsimple-8000-monitor-hardware-status/hw-health4.png)  

4. Si se encuentra un componente que no está en estado **Correcto** , póngase en contacto con el soporte técnico de Microsoft. Si las alertas están habilitadas en el dispositivo, recibirá una alerta por correo electrónico. Si necesita tooreplace un componente de hardware con errores, consulte [sustitución de componentes de hardware de StorSimple](storsimple-hardware-component-replacement.md).

## <a name="component-list-for-primary-enclosure-of-storsimple-device"></a>Lista de componentes de la caja principal del dispositivo StorSimple
Hello tabla siguiente se describe Hola componentes físicos y lógicos contenidos en hello alojamiento principal (presente en 8100 y 8600) del dispositivo de StorSimple local.

| Componente | Módulo | Tipo | Ubicación | ¿Unidad reemplazable en campo (FRU)? | Description |
| --- | --- | --- | --- | --- | --- |
| Unidad en la ranura [0-11] |Unidades de disco |Física |Compartido |Sí |Se presenta una línea para cada uno de hello SSD o unidades de hello HDD de alojamiento principal Hola. |
| Sensor de temperatura ambiente |Revestimiento |Física |Compartido |No |Medidas Hola temperatura dentro del chasis de Hola. |
| Sensor de temperatura de plano medio |Revestimiento |Física |Compartido |No |Medidas Hola temperatura del plano intermedio Hola. |
| Alarma audible |Revestimiento |Física |Compartido |No |Indica si el subsistema de alarma audible hello en el chasis de hello es funcional. |
| Revestimiento |Revestimiento |Física |Compartido |Sí |Indica la presencia de Hola de un chasis. |
| Configuración del revestimiento |Revestimiento |Física |Compartido |No |Se refiere toohello panel frontal del chasis de Hola. |
| Sensores de voltaje de línea |PCM |Física |Compartido |No |Diversos sensores de voltaje de línea tienen muestran su estado, que indica si se mide Hola voltaje está dentro de la tolerancia. |
| Sensores de corriente de línea |PCM |Física |Compartido |No |Numerosos sensores de corriente de línea tienen muestran su estado, lo que indica si hello corriente medida se encuentra dentro de la tolerancia. |
| Sensores de temperatura en el PCM |PCM |Física |Compartido |No |Diversos sensores de temperatura, como sensores de entrada y zona activa muestran su estado, que indica si Hola mide la temperatura es dentro de la tolerancia. |
| Fuente de alimentación [0-1] |PCM |Física |Compartido |Sí |Se presenta una línea para cada una de las fuentes de alimentación de Hola Hola dos PCM ubicados en hello parte posterior del dispositivo de Hola. |
| Refrigeración [0-1] |PCM |Física |Compartido |Sí |Se presenta una línea para cada uno de hello cuatro ventiladores de refrigeración que residen en hello dos PCM. |
| Batería [0-1] |PCM |Física |Compartido |Sí |Se presenta una línea para cada uno de los módulos de batería de reserva de Hola que estén colocados en hello PCM. |
| Metis |N/D |Lógicos |Compartido |N/D |Muestra el estado de Hola de baterías de hello: si necesitan cargarse y están llegando al final de ciclo de vida. |
| Clúster |N/D |Lógicos |Compartido |N/D |Muestra Hola estado del clúster entre dos módulos de controlador integrados Hola Hola que se crea. |
| Nodo de clúster |N/D |Lógicos |Compartido |N/D |Indica el estado de Hola de controlador de hello como parte del clúster de Hola. |
| Quórum de clúster |N/D |Lógicos | |N/D |Indica la presencia de Hola de pertenencia de disco de mayoría Hola Hola bloque de almacenamiento de disco duro. |
| Espacio de datos de la unidad de disco duro |N/D |Lógicos |Compartido |N/D |espacio de almacenamiento de Hola que se usa para los datos en bloque de almacenamiento de hello unidad de disco duro (HDD). |
| Espacio de administración de la unidad de disco duro |N/D |Lógicos |Compartido |N/D |reserva de espacio de Hola Hola grupo de almacenamiento del HDD para tareas de administración. |
| Espacio de quórum de la unidad de disco duro |N/D |Lógicos |Compartido |N/D |reserva de espacio de Hola Hola bloque de almacenamiento de disco duro de quórum de clúster. |
| Espacio de reemplazo de la unidad de disco duro |N/D |Lógicos |Compartido |N/D |reserva de espacio de Hola Hola bloque de almacenamiento HDD de reemplazo de controlador. |
| Espacio de datos de la unidad de estado sólido |N/D |Lógicos |Compartido |N/D |espacio de almacenamiento de Hello utilizado para los datos en bloque de almacenamiento de hello estado sólido (SSD) de la unidad. |
| Espacio de NVRAM de la unidad de estado sólido |N/D |Lógicos |Compartido |N/D |espacio de almacenamiento de Hola Hola bloque de almacenamiento SSD dedicado para la lógica de NVRAM. |
| Grupo de almacenamiento de la unidad de disco duro |N/D |Lógicos |Compartido |N/D |Muestra Hola estado Hola lógica del grupo de almacenamiento que se crea desde los dispositivos HDD. |
| Grupo de almacenamiento de la unidad de estado sólido |N/D |Lógicos |Compartido |N/D |Muestra Hola estado Hola lógica del grupo de almacenamiento que se crea a partir de SSD de dispositivo. |
| Controller [0-1] [estado] |E/S |Física |Controller |Sí |Muestra el estado de Hola de controlador de hello, y si está en modo activo o en espera en el chasis de Hola. |
| Sensores de temperatura en el controlador |E/S |Física |Controller |No |Diversos sensores de temperatura, como módulo de E/S, la temperatura de la CPU sensores DIMM y PCIe tengan muestran su estado, que indica si se permite o no Hola temperatura se encuentra dentro de la tolerancia. |
| Ampliador SAS |E/S |Física |Controller |No |Indica el estado de Hola de hello serie adjunto SCSI (SAS) Ampliador, que es usado tooconnect Hola almacenamiento integrado toohello controlador. |
| Conector SAS [0-1] |E/S |Física |Controller |No |Indica el estado de Hola de cada conector SAS, que es usado tooconnect integrada almacenamiento toohello SAS expansor. |
| Interconexión de plano medio de SBB |E/S |Física |Controller |No |Indica estado Hola de conector de plano intermedio hello, que es usado tooconnect cada plano intermedio toohello de controlador. |
| Núcleo del procesador |E/S |Física |Controller |No |Indica el estado de Hola Hola de núcleos de procesador de cada controlador. |
| Potencia de la electrónica del revestimiento |E/S |Física |Controller |No |Indica el estado de saludo del sistema de alimentación de hello usada por el alojamiento de Hola. |
| Diagnóstico de la electrónica del revestimiento |E/S |Física |Controller |No |Indica el estado de Hola de subsistemas de diagnóstico de hello proporcionado por el controlador de Hola. |
| Controlador de administración de placa base (BMC) |E/S |Física |Controller |No |Indica el estado de saludo del controlador de administración de placa base de hello (BMC), que es un procesador de servicios especializado que supervisa el dispositivo de hardware de Hola a través de sensores y se comunica con el administrador del sistema hello mediante una conexión independiente. |
| Ethernet |E/S |Física |Controller |No |Indica el estado de Hola de cada una de las interfaces de red de hello, es decir, administración de Hola y puertos de datos proporcionados en el controlador de Hola. |
| NVRAM |E/S |Física |Controller |No |Indica el estado de Hola de NVRAM, una memoria de acceso aleatorio no volátil respaldada por batería Hola que sirve de información crítica para la aplicación de tooretain en caso de hello de corte de suministro eléctrico. |

## <a name="component-list-for-ebod-enclosure-of-storsimple-device"></a>Lista de componentes de la caja EBOD del dispositivo StorSimple
Hello tabla siguiente se describe Hola componentes físicos y lógicos contenidos en hello alojamiento de EBOD (solo está presente en el modelo 8600) del dispositivo de StorSimple local.

| Componente | Módulo | Tipo | Ubicación | ¿FRU? | Description |
| --- | --- | --- | --- | --- | --- |
| Unidad en la ranura [0-11] |Unidades de disco |Física |Compartido |Sí |Se presenta una línea para cada uno de hello que las unidades de disco duro en la parte delantera de Hola de hello alojamiento de EBOD. |
| Sensor de temperatura ambiente |Revestimiento |Física |Compartido |No |Medidas Hola temperatura dentro del chasis de Hola. |
| Sensor de temperatura de plano medio |Revestimiento |Física |Compartido |No |Medidas Hola temperatura del plano intermedio Hola. |
| Alarma audible |Revestimiento |Física |Compartido |No |Indica si el subsistema de alarma audible hello en el chasis de hello es funcional. |
| Revestimiento |Revestimiento |Física |Compartido |Sí |Indica la presencia de Hola de un chasis. |
| Configuración del revestimiento |Revestimiento |Física |Compartido |No |Se refiere toohello OPS u Hola el panel frontal del chasis de Hola. |
| Sensores de voltaje de línea |PCM |Física |Compartido |No |Diversos sensores de voltaje de línea tienen muestran su estado, que indica si se mide Hola voltaje está dentro de la tolerancia. |
| Sensores de corriente de línea |PCM |Física |Compartido |No |Numerosos sensores de corriente de línea tienen muestran su estado, lo que indica si hello corriente medida se encuentra dentro de la tolerancia. |
| Sensores de temperatura en el PCM |PCM |Física |Compartido |No |Diversos sensores de temperatura, como sensores de entrada y zona activa muestran su estado, lo que indica si Hola mide la temperatura es dentro de la tolerancia. |
| Fuente de alimentación [0-1] |PCM |Física |Compartido |Sí |Se presenta una línea para cada una de las fuentes de alimentación de Hola Hola dos PCM ubicados en hello parte posterior del dispositivo de Hola. |
| Refrigeración [0-1] |PCM |Física |Compartido |Sí |Se presenta una línea para cada uno de hello cuatro ventiladores de refrigeración que residen en hello dos PCM. |
| Almacenamiento local [HDD] |N/D |Lógicos |Compartido |N/D |Muestra Hola estado Hola lógica del grupo de almacenamiento que se crea desde los dispositivos HDD. |
| Controller [0-1] [estado] |E/S |Física |Controller |Sí |Muestra Hola estado de los controladores de hello en el módulo EBOD Hola. |
| Sensores de temperatura en el EBOD |E/S |Física |Controller |No |Diversos sensores de temperatura de cada controlador tienen muestran su estado, que indica si la temperatura Hola se encuentra dentro de la tolerancia. |
| Ampliador SAS |E/S |Física |Controller |No |Indica el estado de saludo del Ampliador SAS de hello, que es usado tooconnect Hola almacenamiento integrado toohello controlador. |
| Conector SAS [0-2] |E/S |Física |Controller |No |Indica el estado de Hola de cada conector SAS, que es usado tooconnect integrada almacenamiento toohello SAS expansor. |
| Interconexión de plano medio de SBB |E/S |Física |Controller |No |Indica estado Hola de conector de plano intermedio hello, que es usado tooconnect cada plano intermedio toohello de controlador. |
| Potencia de la electrónica del revestimiento |E/S |Física |Controller |No |Indica el estado de saludo del sistema de alimentación de hello usada por el alojamiento de Hola. |
| Diagnóstico de la electrónica del revestimiento |E/S |Física |Controller |No |Indica el estado de Hola de subsistemas de diagnóstico de hello proporcionado por el controlador de Hola. |
| Controlador de conexión toodevice |E/S |Física |Controller |No |Indica el estado de Hola de conexión de hello entre el módulo de E/S EBOD Hola y el controlador de dispositivo de Hola. |

## <a name="next-steps"></a>Pasos siguientes
* toouse Hola a tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo, vaya demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).
* Si necesita tootroubleshoot un componente de dispositivo que tiene un estado degradado o con error, consulte demasiado[StorSimple supervisar los indicadores](storsimple-monitoring-indicators.md).
* tooreplace un componente de hardware con errores, vea [sustitución de componentes de hardware de StorSimple](storsimple-hardware-component-replacement.md).
* Si continúa tooexperience problemas del dispositivo, [póngase en contacto con Microsoft Support](storsimple-8000-contact-microsoft-support.md).

