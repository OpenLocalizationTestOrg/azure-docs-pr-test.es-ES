---
title: plantillas de ancho de banda de aaaManage para la serie 8000 de StorSimple | Documentos de Microsoft
description: "Describe cómo plantillas de ancho de banda de StorSimple toomanage, que le permiten toocontrol consumo de ancho de banda."
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: ebcd1824d7bb9e4c235194c04edbfe8001a3e794
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-bandwidth-templates"></a>Usar plantillas de ancho de banda de hello Administrador de dispositivos de StorSimple servicio toomanage StorSimple

## <a name="overview"></a>Información general

Plantillas de ancho de banda permiten uso de ancho de banda de red de tooconfigure entre varios programas según la hora del día tootier Hola datos de hello StorSimple dispositivo toohello la nube.

Mediante programaciones de limitación de ancho de banda puede:

* Especificar programaciones de ancho de banda personalizado según los usos de la red de hello cargas de trabajo.
* Centralizar la administración y reutilizar las programaciones de hello en varios dispositivos de forma fácil y transparente.

> [!NOTE]
> Esta característica está disponible solo para dispositivos físicos de StorSimple (modelos 8100 y 8600) y no para StorSimple Cloud Appliances (modelos 8010 y 8020).


## <a name="hello-bandwidth-templates-blade"></a>hoja de plantillas de ancho de banda de Hola

Hola **plantillas de ancho de banda** hoja tiene todas las plantillas de ancho de banda de hello para el servicio en un formato tabular y contiene Hola siguiente información:

* **Nombre** : una plantilla de ancho de banda de toohello nombre único que se asigna cuando se creó.
* **Programación** : Hola número de programaciones contenidas en una plantilla de ancho de banda determinado.
* **Utilizado por** : Hola número de volúmenes que usan plantillas de ancho de banda de Hola.

También puede encontrar información adicional toohelp configurar plantillas de ancho de banda en:

* [Preguntas y respuestas acerca de las plantillas de ancho de banda](#questions-and-answers-about-bandwidth-templates)
* [Procedimientos recomendados para plantillas de ancho de banda](#best-practices-for-bandwidth-templates)

## <a name="add-a-bandwidth-template"></a>Agregar una plantilla de ancho de banda

Realizar Hola siguiendo los pasos toocreate una nueva plantilla de ancho de banda.

#### <a name="tooadd-a-bandwidth-template"></a>tooadd una plantilla de ancho de banda

1. Servicio de administrador de dispositivos de StorSimple tooyour go, haga clic en **plantillas de ancho de banda** y, a continuación, haga clic en **+ plantilla de ancho de banda de agregar**.

    ![Hacer clic en + Agregar plantilla de ancho de banda](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp1.png)

2. Hola **agregar una plantilla de ancho de banda** hoja, Hola lo siguiente:
   
    1. Especifique un nombre único para la plantilla de ancho de banda.
    2. Defina una programación de ancho de banda. toocreate una programación:
   
        1. Desde la lista desplegable de hello, elija hello **días** de Hola Hola de semana se configura la programación de. Puede seleccionar varios días.        
        
        2. Escriba una **hora de inicio** en formato _hh:mm_. Esto es cuando se iniciará la programación de Hola.

        3. Escriba una **hora de finalización** en formato _hh:mm_. Esto resulta dejará de programación de Hola.
      
           > [!NOTE]
           > No se permiten las programaciones superpuestas. Si hello horas de inicio y finalización dará como resultado una programación superpuesta, verá un efecto de toothat de mensaje de error.

        4. Especificar hello **velocidad de ancho de banda**. Se trata de ancho de banda de hello en Megabits por segundo (Mbps) utilizado por el dispositivo StorSimple en operaciones relacionadas con hello nube (cargas y descargas). Proporcione un número entre 1 y 1.000 para este campo.

            ![Definir programación de ancho de banda](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp2.png)
         
            Repita Hola anteriormente pasos toodefine varias programaciones para la plantilla hasta que haya terminado.

        5. Haga clic en **agregar** toostart crear una plantilla de ancho de banda. Hola creado plantilla se agrega toohello lista de plantillas de ancho de banda.
      

## <a name="edit-a-bandwidth-template"></a>Editar una plantilla de ancho de banda

Realizar Hola siguiendo los pasos tooedit una plantilla de ancho de banda.

### <a name="tooedit-a-bandwidth-template"></a>tooedit una plantilla de ancho de banda

1. Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **plantillas de ancho de banda**.
2. En la lista Hola de plantillas de ancho de banda, seleccione plantilla de hello desea toodelete. Haga clic en y en el menú contextual de hello, seleccione **eliminar**.
3. Cuando se le pida confirmación, haga clic en **Aceptar**. Esto debería eliminar la plantilla de ancho de banda de Hola. 
4. Hola lista de plantillas de ancho de banda de actualizaciones de eliminación de hello tooreflect.

> [!NOTE]
> No se puede guardar los cambios si Hola editado superposiciones de programación con una programación existente en la plantilla de ancho de banda de Hola que va a modificar.

## <a name="delete-a-bandwidth-template"></a>Eliminar una plantilla de ancho de banda

Realizar Hola siguiendo los pasos toodelete una plantilla de ancho de banda.

#### <a name="toodelete-a-bandwidth-template"></a>toodelete una plantilla de ancho de banda

1. Servicio de administrador de dispositivos de StorSimple tooyour y haga clic en **plantillas de ancho de banda**.
2. En la lista Hola de plantillas de ancho de banda, seleccione plantilla de hello desea toodelete. Haga clic en y desde el menú contextual de hello, seleccione Eliminar.
3. Cuando se le pida confirmación, haga clic en **Aceptar**. Esto debería eliminar la plantilla de ancho de banda de Hola.
4. Hola lista de plantillas de ancho de banda de actualizaciones de eliminación de hello tooreflect.

Si la plantilla de hello está en uso por los volúmenes, no se permitirá toodelete lo. Verá un mensaje de error que indica que la plantilla Hola está en uso. Se mostrará un cuadro de diálogo de mensaje de error le avisa de que se deben quitar todas las plantillas de toohello de referencias de Hola.

Puede eliminar todas las plantillas de toohello de referencias de hello accediendo hello **contenedores de volúmenes** página y modificar los contenedores de volúmenes de Hola que usen esta plantilla para que usen otra plantilla o usar un ancho de banda ilimitado o personalizado configuración de. Cuando se han quitado todas las referencias de hello, puede eliminar la plantilla de Hola.

## <a name="use-a-default-bandwidth-template"></a>Usar una plantilla de ancho de banda predeterminada

Una plantilla de ancho de banda predeterminada se proporciona y se utiliza contenedores de volúmenes mediante controles de ancho de banda de tooenforce predeterminados al obtener acceso a la nube de Hola. plantilla predeterminada de Hello también sirve como referencia para los usuarios que crean sus propias plantillas. Hola los detalles de esta plantilla predeterminada son:

* **Nombre** : noches y fines de semana ilimitados
* **Programación** : una sola programación de lunes tooFriday que aplica una velocidad de ancho de banda de 1 Mbps entre las 8 A.M. y las 5 P.M. hora del dispositivo. se establece ancho de banda de Hello tooUnlimited para el resto de saludo de la semana de Hola.

se puede editar la plantilla predeterminada de Hola. se realiza el seguimiento de uso de Hola de esta plantilla (incluidas las versiones editadas).

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a>Crear una plantilla de ancho de banda para todo el día que comience a una hora especificada

Siga este toocreate procedimiento una programación que empieza en un momento determinado y se ejecuta todo el día. En el ejemplo de Hola, programación de hello inicia a las 9 AM de mañana hello y se ejecuta hasta Hola 9 AM por la mañana siguiente. Es importante toonote que Hola inicio y las horas de finalización de una programación determinada deben estar en hello mismo 24 horas programar y no puede abarcar varios días. Si necesita tooset las plantillas de ancho de banda que abarcan varios días, deberá toouse varias programaciones (como se muestra en el ejemplo de Hola).

#### <a name="toocreate-an-all-day-bandwidth-template"></a>toocreate una plantilla de ancho de banda para todo el día

1. Crear una programación que se inicia a las 9 AM de mañana hello y se ejecuta hasta medianoche.
2. Agregar otra programación. Configurar Hola segunda programación toorun desde medianoche hasta las 9 AM de mañana Hola.
3. Guarde la plantilla de ancho de banda de Hola.

programación compuesta de Hello, a continuación, se inicie en el momento de su elección y ejecute todo el día.

## <a name="questions-and-answers-about-bandwidth-templates"></a>Preguntas y respuestas acerca de las plantillas de ancho de banda

**P**. Controles de toobandwidth ¿qué ocurre cuando haya entre programaciones Hola? (Una programación ha terminado y todavía no se ha iniciado otra).

**R**. En estos casos, no se utilizará ningún control de ancho de banda. Esto significa que ese dispositivo Hola puede usar ancho de banda ilimitado cuando mueva el nivel de datos toohello en la nube.

**P**. ¿Puede modificar las plantillas de ancho de banda en un dispositivo sin conexión?

**R**. No será capaz de toomodify plantillas de ancho de banda en los contenedores de volúmenes si Hola correspondiente dispositivo está desconectado.

**P**. ¿Puede editar una plantilla de ancho de banda asociada a un contenedor de volúmenes cuando los volúmenes de hello asociado están sin conexión?

**R**. Puede modificar una plantilla de ancho de banda asociada a un contenedor de volúmenes cuyos volúmenes están sin conexión. Tenga en cuenta que cuando los volúmenes sin conexión, no se pueden mover ningún dato de la nube de hello dispositivo toohello.

**P**. ¿Puede eliminar una plantilla predeterminada?

**R**. Aunque puede eliminar una plantilla predeterminada, no es una buena idea toodo así. uso de Hola de una plantilla predeterminada, incluidas las versiones modificadas, se realiza el seguimiento. Hola datos de seguimiento se analiza y en transcurso Hola de tiempo, es plantilla predeterminada de uso tooimprove Hola.

**P**. ¿Cómo determina que las plantillas de ancho de banda necesitan toobe modificado?

**R**. Uno de hello signos que necesita plantillas de ancho de banda de hello toomodify está cuando se inicia ver Hola red lenta o se retrae varias veces en un día. Si esto ocurre, supervisar la red de almacenamiento y el uso de hello examinando los gráficos de rendimiento de red y la E/S de Hola.

De datos de rendimiento de red de hello, identifique Hola hora del día y Hola contenedores de volúmenes en qué Hola se produce un cuello de botella de red. Si esto sucede cuando los datos se están toohello en capas en la nube (Obtenga esta información del rendimiento de E/S para todos los contenedores de volumen para dispositivos toocloud), será necesario plantillas de ancho de banda de hello toomodify asociadas a los contenedores de volumen.

Después de modifica Hola plantillas están en uso, necesitará red de hello toomonitor nuevo para las latencias importantes. Si aún existen, deberá toorevisit sus plantillas de ancho de banda.

**P**. ¿Qué ocurre si varios contenedores de volumen en mi dispositivo tienen programaciones que se superponen pero aplican distintos límites tooeach?

**R**. Supongamos que tiene un dispositivo con 3 contenedores de volúmenes. Hello programaciones asociadas a estos contenedores completamente se superponen. Para cada uno de estos contenedores, límites de ancho de banda de hello usa son 5, 10 y 15 Mbps respectivamente. Cuando se producen E/S en todos estos contenedores en hello puede aplicarse el mismo tiempo, como mínimo Hola Hola 3 límites de ancho de banda: en este caso, serían 5 Mbps como estos recursos compartidos de las solicitudes de E/S de salida Hola misma cola.

## <a name="best-practices-for-bandwidth-templates"></a>Prácticas recomendadas para plantillas de ancho de banda

Siga estas prácticas recomendadas para el dispositivo StorSimple:

* Configurar plantillas de ancho de banda en su dispositivo tooenable límite variable del rendimiento de la red de Hola por dispositivo de hello en distintos momentos del día de Hola. Cuando se utilizan estas plantillas de ancho de banda con programaciones de copia de seguridad, pueden aprovechar eficazmente el ancho de banda de red adicional para las operaciones de nube durante las horas de menos tráfico.
* Calcular Hola ancho de banda real necesario para una implementación concreta en función de tamaño de Hola de implementación de Hola y el objetivo de tiempo de recuperación necesario hello (RTO).

## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre [utilizando Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

