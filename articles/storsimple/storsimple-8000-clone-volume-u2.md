---
title: aaaClone un volumen en serie StorSimple 8000 | Documentos de Microsoft
description: "Describe tipos de clon diferentes de Hola y el uso y explica cómo puede utilizar un tooclone un volumen individual de conjunto de copia de seguridad en un dispositivo de la serie StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: 4f7e1f62f17c7b2bd72820a00a5ab87b7e192332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-tooclone-a-volume"></a>Usar el servicio de administrador de dispositivos de StorSimple de hello en tooclone portal Azure un volumen

## <a name="overview"></a>Información general

Este tutorial describe cómo puede utilizar un tooclone del conjunto de copia de seguridad un volumen individual mediante hello **catálogo de copia de seguridad** hoja. También explica diferenciar en hello *transitorio* y *permanente* clones. Guía de Hello en este tutorial aplica a dispositivo de la serie StorSimple 8000 hello tooall con Update 3 o posterior.

Hola servicio Administrador de dispositivos de StorSimple **catálogo de copia de seguridad** hoja muestra todos los conjuntos de copia de seguridad de Hola que se crean cuando se realizan copias de seguridad manuales o automatizadas. A continuación, puede seleccionar un volumen en un conjunto de copia de seguridad tooclone.

 ![Lista de conjuntos de copia de seguridad](./media/storsimple-8000-clone-volume-u2/bucatalog.png)

## <a name="considerations-for-cloning-a-volume"></a>Consideraciones sobre la clonación de un volumen

Considere la posibilidad de hello siguiente información al clonar un volumen.

- Un clon comporta en hello misma manera que un volumen normal. Cualquier operación que sea posible en un volumen está disponible para que se clona Hola.

- La copia de seguridad predeterminada y la supervisión se deshabilitan automáticamente en un volumen clonado. Necesitaría tooconfigure un volumen clonado para las copias de seguridad.

- Un volumen anclado localmente se clona como un volumen en capas. Si necesita hello toobe volumen clonado anclado localmente, puede convertir el volumen de tooa anclado localmente de clon de hello después de una operación de clonación Hola se ha completado correctamente. Para obtener información sobre cómo convertir un tooa de volumen en capas localmente anclado volumen, consulte demasiado[cambiar el tipo de volumen hello](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).

- Si intentas tooconvert que un volumen clonado de toolocally en capas anclado inmediatamente después de la clonación (cuando todavía es un clon transitorio), se produce un error en la conversión de hello con hello mensaje de error siguiente:

    `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.`

    Se recibe este error sólo si está clonando en tooa otro dispositivo. Puede convertir correctamente Hola volumen toolocally anclado si convierte primero clonación permanente de hello clonación transitoria tooa. Crear una instantánea de nube de hello clonación transitoria tooconvert se tooa de clonación permanente.

## <a name="create-a-clone-of-a-volume"></a>Crear un clon de un volumen

Puede crear un clon en Hola mismo dispositivo, otro dispositivo o incluso un dispositivo de nube mediante el uso de una variable local o instantánea en la nube.

procedimiento de Hello siguiente describe cómo toocreate un clon de hello copia de seguridad de catálogo.  Un clon de tooinitiate método alternativo es toogo demasiado**volúmenes**, seleccione un volumen, a continuación, haga clic en el menú contextual de tooinvoke hello y seleccione **clon**.

Realizar Hola siguiendo los pasos toocreate un clon del volumen de catálogo de copia de seguridad de Hola.

#### <a name="tooclone-a-volume"></a>tooclone un volumen

1. Servicio de administrador de dispositivos de StorSimple tooyour y, a continuación, haga clic en **catálogo de copia de seguridad**.

2. Seleccione una copia de seguridad de la siguiente manera:
   
   1. Seleccionar dispositivo apropiados de Hola.
   2. En la lista desplegable de hello, elija la que desea tooselect de directiva de copia de seguridad o volumen de Hola para copia de seguridad de Hola.
   3. Especifique el intervalo de tiempo de Hola.
   4. Haga clic en **aplicar** tooexecute esta consulta.

    Hello deben aparecer copias de seguridad asociadas con la directiva de copia de seguridad o volumen de hello seleccionado en lista de Hola de conjuntos de copia de seguridad.
   
    ![Lista de conjuntos de copia de seguridad](./media/storsimple-8000-clone-volume-u2/bucatalog.png)
     
3. Expandir tooview Hola asociado volúmenes de hello conjunto de copia de seguridad. Estos volúmenes deben realizarse sin conexión en el host de Hola y el dispositivo antes de que pueda restaurarlos al completo. Obtener acceso a los volúmenes de hello en hello **volúmenes** hoja de su dispositivo y, a continuación, Hola de seguimiento de los pasos de [desconectar un volumen](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake ellos sin conexión.
   
   > [!IMPORTANT]
   > Asegúrese de que haya desconectado Hola volúmenes en el host de hello en primer lugar, antes de poner sin conexión los volúmenes de hello en dispositivo Hola. Si no se realiza sin conexión los volúmenes de hello en el host de hello, pudieron causar daños toodata.
   
4. Desplácese atrás toohello **catálogo de copia de seguridad** y seleccione un volumen en un conjunto de copia de seguridad. Haga clic en y, a continuación, desde el menú contextual de hello, seleccione **clon**.

   ![Lista de conjuntos de copia de seguridad](./media/storsimple-8000-clone-volume-u2/clonevol3b.png) 

3. Hola **clon** hoja, Hola lo siguiente:
   
    1. Identifique un dispositivo de destino. Se trata de ubicación de Hola donde se creará la clonación de Hola. Puede elegir Hola mismo dispositivo o especificar otro dispositivo.

      > [!NOTE]
      > Asegúrese de que capacidad de hello requerida para que se clona hello es inferior al capacidad Hola disponible en el dispositivo de destino de Hola.
       
    2. Especifique un nombre de volumen único para el clon. Hola nombre debe contener entre 3 y 127 caracteres.
      
        > [!NOTE]
        > Hola **clon volumen como** campo estará **"en capas"** incluso si se clonar un volumen anclado localmente. No se puede cambiar esta configuración; Sin embargo, si necesita hello toobe volumen clonado también anclado localmente, se puede convertir volumen de hello clon tooa anclado localmente después de crear el clon de hello correctamente. Para obtener información sobre cómo convertir un tooa de volumen en capas localmente anclado volumen, consulte demasiado[cambiar el tipo de volumen hello](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).
          
    3. En **hosts conectados**, especifique un registro de control de acceso (ACR) para que se clona Hola. Puede agregar un nuevo ACR o elegir de lista existente de Hola. Hola ACR determinan qué hosts pueden acceder a este clon.
      
        ![Lista de conjuntos de copia de seguridad](./media/storsimple-8000-clone-volume-u2/clonevol3a.png) 

    4. Haga clic en **clon** operación de hello toocomplete.

4. Se inicia un trabajo de clonación y se le notificará cuando clon Hola se creó correctamente. Haga clic en la notificación de trabajo de Hola o visite demasiado**trabajos** trabajo de clonación de hoja toomonitor Hola.

    ![Lista de conjuntos de copia de seguridad](./media/storsimple-8000-clone-volume-u2/clonevol5.png)

7. Una vez completado el trabajo de clonación de hello, tooyour dispositivo y, a continuación, haga clic en **volúmenes**. En la lista de Hola de volúmenes, verá clon Hola que acaba de crear en hello mismo contenedor de volumen que tiene el volumen de origen de Hola.

    ![Lista de conjuntos de copia de seguridad](./media/storsimple-8000-clone-volume-u2/clonevol6.png)

Los clones que se creen de esta forma son clones transitorios. Para obtener más información acerca de los tipos de clon, consulte [Clones transitorios frente a clones permanentes](#transient-vs-permanent-clones).


## <a name="transient-vs-permanent-clones"></a>Clones transitorios frente a clones permanentes
Clones transitorios se crean solo cuando se clona tooanother dispositivo. Puede clonar un volumen específico desde el conjunto de copia de seguridad tooa otro dispositivo administrado por hello Administrador de dispositivos de StorSimple. clonación transitoria Hello tiene referencias toohello datos en el volumen original de Hola y utiliza esa tooread de datos y la escritura de manera local en el dispositivo de destino de Hola.

Después de tomar una instantánea de un clon transitorio en la nube, clon resultante de hello es un *permanente* clon. Durante este proceso, una copia de datos de Hola se crea en la nube de Hola y Hola toocopy tiempo que estos datos viene determinados por el tamaño de Hola de los datos de Hola y Hola latencias de Azure (Esto es una copia de Azure en Azure). Este proceso puede tardar días tooweeks. clonación transitoria Hola se convierte en una clonación permanente y no tiene ninguna referencias toohello datos del volumen original que se clonó desde.

## <a name="scenarios-for-transient-and-permanent-clones"></a>Escenarios para clones transitorios y permanentes
Hola siguientes secciones describe situaciones de ejemplo en el que se pueden usar clones transitorios y permanentes.

### <a name="item-level-recovery-with-a-transient-clone"></a>Recuperación de nivel de elemento con un clon transitorio
Debe toorecover un archivo de presentación de Microsoft PowerPoint de un año de antigüedad. El Administrador de TI identifica la copia de seguridad específica de Hola desde ese momento y, a continuación, filtros Hola volumen. Administrador de Hello clona el volumen de hello, busca el archivo hello que desea obtener y proporciona tooyou. En este escenario, se usa un clon transitorio.

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>Realización de pruebas en el entorno de producción de hello con una clonación permanente
Deberá tooverify un error de prueba en el entorno de producción de hello. Crear un clon del volumen de hello en el entorno de producción de hello y, a continuación, cree una instantánea de nube de este toocreate clonar un volumen clonado independiente. En este escenario, se usa un clon permanente.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[restaurar un volumen de StorSimple a partir de un conjunto de copia de seguridad](storsimple-8000-restore-from-backup-set-u2.md).
* Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

