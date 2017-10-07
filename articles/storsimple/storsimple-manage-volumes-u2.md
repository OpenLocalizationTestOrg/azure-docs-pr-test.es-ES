---
title: "aaaManage los volúmenes de StorSimple (U2) | Documentos de Microsoft"
description: "Explica cómo tooadd, modificar, supervisar y eliminar volúmenes de StorSimple y cómo tootake ellos sin conexión si es necesario."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 57896932-0aa5-4805-970c-d13403ae7551
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/28/2016
ms.author: alkohli
ms.openlocfilehash: 8b64f1d92023646cdf881882854d9bc5d7334a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes-update-2"></a>Usar hello StorSimple Manager servicio toomanage volúmenes (actualización 2)
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>Información general
Este tutorial le explica cómo toouse Hola toocreate de servicio de StorSimple Manager y administrar los volúmenes en el dispositivo de StorSimple de Hola y el dispositivo virtual StorSimple Update 2 instalado.

Hola el servicio StorSimple Manager es una extensión en hello portal de Azure clásico que le permite administrar la solución de StorSimple de una única interfaz web. En volúmenes de toomanaging de suma, puede usar toocreate de servicio de StorSimple Manager hello y administrar los servicios de StorSimple, ver y administrar dispositivos, ver alertas y ver y administrar las directivas de copia de seguridad y el catálogo de copia de seguridad de Hola.

## <a name="volume-types"></a>Tipos de volúmenes
Los volúmenes de StorSimple pueden ser:

* **Anclado localmente volúmenes**: los datos en estos volúmenes permanecen en el dispositivo StorSimple local hello en todo momento.
* **En niveles volúmenes**: datos de estos volúmenes pueden retrasar toohello en la nube.

Un volumen de archivo es un tipo de volumen en capas. Hola desduplicación fragmento tamaño usado para los volúmenes de archivado permite segmentos de mayor tootransfer de hello dispositivo de datos toohello en la nube. 

Si es necesario, puede cambiar el tipo de volumen Hola de tootiered local o de toolocal en capas. Para obtener más información, consulte demasiado[cambiar el tipo de volumen hello](#change-the-volume-type).

### <a name="locally-pinned-volumes"></a>Volúmenes anclados localmente
Los volúmenes anclados localmente son totalmente aprovisionados volúmenes que no capa de datos toohello en la nube, lo que garantiza que local garantiza de datos principales, independientemente de conectividad en la nube. Los datos de los volúmenes anclados localmente no se desduplican ni comprimen, pero las instantáneas de dichos volúmenes se desduplican. 

Los volúmenes anclados localmente están totalmente aprovisionados, por lo que debe haber espacio suficiente en el dispositivo cuando los crea. Puede aprovisionar volúmenes anclados localmente tooa tamaño máximo de 8 TB en el dispositivo de StorSimple 8100 hello y 20 TB en dispositivo 8600 de Hola. StorSimple reserva el espacio local restantes hello en dispositivo Hola de instantáneas, metadatos y el procesamiento de datos. Puede aumentar tamaño de Hola de un volumen anclado localmente toohello espacio máximo disponible, pero no se puede reducir tamaño de Hola de un volumen una vez creado.

Cuando se crea un volumen anclado localmente, se reduce el espacio disponible de hello para la creación de volúmenes en capas. Hola inversa también es cierto: si tiene volúmenes en capas existentes, espacio de hello disponible para crear localmente anclado volúmenes será inferior a los límites máximos Hola indicados anteriormente. Para obtener más información sobre los volúmenes locales, consulte toohello [preguntas más frecuentes sobre los volúmenes anclados localmente](storsimple-local-volume-faq.md).   

### <a name="tiered-volumes"></a>Volúmenes en capas
Los volúmenes en capas son volúmenes con aprovisionamiento fino en qué Hola con frecuencia datos de acceso permanece local en el dispositivo de Hola y menos datos utilizados con frecuencia es automáticamente en niveles toohello en la nube. El aprovisionamiento fino es una tecnología de virtualización en el que el almacenamiento disponible parece tooexceed los recursos físicos. En lugar de reservar almacenamiento suficiente de antemano, StorSimple usa tooallocate de aprovisionamiento fino suficiente requisitos de espacio en toomeet actual. naturaleza elástica de Hola de almacenamiento en nube facilita este enfoque porque StorSimple puede aumentar o disminuir toomeet cambiantes exigencias de almacenamiento de nube.

Si utilizas Hola volumen en capas para los datos de archivo, seleccione hello **usar este volumen de datos acceso menos frecuente archivados** casilla de verificación cambia el tamaño del fragmento de desduplicación de Hola para su volumen too512 KB. Si no selecciona esta opción, el volumen en capas correspondiente de Hola utilizará un tamaño de fragmento de 64 KB. Un tamaño de fragmento de desduplicación permite la transferencia de hello tooexpedite hello de dispositivo de nube de toohello de los datos de archivo grande.

> [!NOTE]
> Archivo volúmenes creados con una versión 2 de anteriores a la actualización de StorSimple se importarán como en capas con hello archivado casilla activada.
> 
> 

### <a name="provisioned-capacity"></a>Capacidad aprovisionada
Consulte toohello máxima capacidad aprovisionada para cada tipo de dispositivo y el volumen en la tabla siguiente. (Tenga en cuenta que los volúmenes anclados localmente no están disponibles en un dispositivo virtual).

|  | Tamaño máximo del volumen en capas | Tamaño máximo del volumen anclado localmente |
| --- | --- | --- |
| **Dispositivos físicos** | | |
| 8100 |64 TB |8 TB |
| 8600 |64 TB |20 TB |
| **Dispositivos virtuales** | | |
| 8010 |30 TB |N/D |
| 8020 |64 TB |N/D |

## <a name="hello-volumes-page"></a>página de volúmenes de Hola
Hola **volúmenes** página permite los volúmenes de almacenamiento de hello toomanage que se ha aprovisionado en el dispositivo de StorSimple de Microsoft Azure de Hola para sus iniciadores (servidores). Muestra la lista de Hola de volúmenes en el dispositivo StorSimple.

 ![Página de volúmenes](./media/storsimple-manage-volumes-u2/VolumePage.png)

Un volumen se compone de una serie de atributos:

* **Nombre del volumen** : un nombre descriptivo que debe ser únicos y ayuda a identificar el volumen de Hola. Este nombre también se usa en los informes de supervisión cuando se filtra por un volumen específico.
* **Estado** : puede estar conectado o desconectado. Si un volumen está sin conexión, no es visible tooinitiators (servidores) que se permiten acceso toouse Hola volumen.
* **Capacidad** : especifica la cantidad total de Hola de datos que se pueden almacenar por el iniciador de hello (servidor). Los volúmenes anclados localmente se aprovisionan por completo y residen en el dispositivo StorSimple Hola. Aprovisionamiento fino de los volúmenes en capas y Hola datos se desduplican. Con volúmenes con aprovisionamiento fino, el dispositivo no preasigne la capacidad de almacenamiento físico internamente o en la nube de hello según la capacidad del volumen tooconfigured. capacidad del volumen Hola se asigna y consume a demanda.
* **Tipo de** : indica si el volumen de hello es **"en capas"** (Hola predeterminado) o **anclado localmente**.
* **Copia de seguridad** : indica si existe una directiva de copia de seguridad predeterminada para el volumen de Hola.
* **Acceso** – especifica iniciadores de hello (servidores) que se permiten acceso toothis volumen. Los iniciadores que no sean miembros del registro de control de acceso (ACR) que está asociado a Hola volumen no verán el volumen de Hola.
* **Supervisión** : especifica si se está supervisando un volumen. Un volumen tendrá la supervisión habilitada de forma predeterminada cuando se crea. Sin embargo, la supervisión estará deshabilitada para un clon del volumen. tooenable supervisión de un volumen, siga las instrucciones de hello en [supervisar un volumen](#monitor-a-volume). 

Use las instrucciones de hello en este hello tooperform tutorial siguiente las tareas:

* Agregar un volumen 
* Modificar un volumen 
* Cambiar el tipo de volumen Hola
* Eliminar un volumen 
* Desconectar un volumen 
* Supervisar un volumen 

## <a name="add-a-volume"></a>Agregar un volumen
Ya [creó un volumen](storsimple-deployment-walkthrough-u2.md#step-6-create-a-volume) durante la implementación de la solución de StorSimple. El procedimiento para agregar un volumen es similar.

#### <a name="tooadd-a-volume"></a>tooadd un volumen
1. En hello **dispositivos** , seleccione dispositivos hello, haga doble clic en él y, a continuación, haga clic en hello **contenedores de volúmenes** ficha.
2. Seleccione un contenedor de volúmenes de lista de Hola y haga doble clic en él tooaccess Hola volúmenes asociados con el contenedor de Hola.
3. Haga clic en **agregar** final Hola de página Hola. inicia el asistente Agregar un volumen de Hola.
   
     ![Agregar configuración básica del asistente de volumen](./media/storsimple-manage-volumes-u2/TieredVolEx.png)
4. Hola, agregar un asistente de volumen, en **configuración básica**, Hola siguientes:
   
   1. Proporcione un **Nombre** para el volumen.
   2. Seleccione un **tipo de uso** desde la lista desplegable de Hola. Para las cargas de trabajo que requieren datos toobe disponible localmente en el dispositivo de hello en todo momento, seleccione **anclado localmente**. Para todos los demás tipos de datos, seleccione **En capas**. (**"En capas"** es Hola predeterminado.)
   3. Si seleccionó **"en capas"** en el paso 2, puede seleccionar hello **usar este volumen de datos acceso menos frecuente archivados** casilla de verificación tooconfigure un volumen archivado.
   4. Escriba hello **capacidad aprovisionada** para su volumen en GB o TB. Para conocer los tamaños máximos de cada dispositivo y tipo de volumen, consulte [Capacidad aprovisionada](#provisioned-capacity) . Mire hello **capacidad disponible** toodetermine cuánto almacenamiento está disponible en el dispositivo.
5. Haga clic en el icono de flecha de Hola![Icono de flecha](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png). Si está configurando un volumen anclado localmente, verá el siguiente mensaje de Hola.
   
    ![Cambiar el mensaje de tipo de volumen](./media/storsimple-manage-volumes-u2/LocalVolEx.png)
6. Haga clic en el icono de flecha de hello ![icono de flecha](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png)nuevo toogo toohello **configuración adicional** página.
   
    ![Agregar configuración adicional del asistente de volumen](./media/storsimple-manage-volumes-u2/AddVolume2.png)<br>
7. En **Configuración adicional**, agregue un nuevo registro de control de acceso (ACR):
   
   1. Seleccione un registro de control de acceso (ACR) de la lista desplegable de Hola. También puede agregar un nuevo ACR. Acr determinan qué hosts pueden acceder a los volúmenes de hello coincidente IQN de host con el que aparece en el registro de hello. Si no especifica un ACR, verá el siguiente mensaje de Hola.
      
        ![Especificar ACR](./media/storsimple-manage-volumes-u2/SpecifyACR.png)
   2. Le recomendamos que seleccione hello **habilitar una copia de seguridad predeterminado para este volumen** casilla de verificación.
   3. Haga clic en el icono de verificación de Hola ![Icono de marca de verificación](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) volumen de hello toocreate con hello especificó los valores.

El nuevo volumen ahora está listo toouse.

> [!NOTE]
> Si crea un volumen anclado localmente y, a continuación, crear otro localmente anclados volumen inmediatamente después, se ejecutan los trabajos de creación de volumen de hello secuencialmente. primer trabajo de creación de volumen Hola debe finalizar para que pueda comenzar el siguiente trabajo de creación de volumen Hola.
> 
> 

## <a name="modify-a-volume"></a>Modificar un volumen
Modificar un volumen cuando necesite tooexpand, o cambiar Hola hosts que tienen acceso a los volúmenes de Hola.

> [!IMPORTANT]
> * Si modifica el tamaño del volumen de hello en dispositivo de hello, el tamaño del volumen de hello debe toobe cambia en el host de hello así. 
> * pasos de lado del host de Hello descritos aquí son para Windows Server 2012 (2012R2). Los procedimientos para Linux u otros sistemas operativos de host serán diferentes. Consulte instrucciones del sistema operativo host tooyour al modificar el volumen de hello en un host que ejecuta otro sistema operativo. 
> 
> 

#### <a name="toomodify-a-volume"></a>toomodify un volumen
1. En hello **dispositivos** , seleccione dispositivos hello, haga doble clic en él y, a continuación, haga clic en hello **contenedores de volúmenes** ficha.
2. Seleccione un contenedor de volúmenes de lista de Hola y haga doble clic en él volúmenes de hello tooview asociados con el contenedor de Hola.
3. Seleccione un volumen y, en la parte inferior de Hola de página de hello, haga clic en **modificar**. se inicia el Asistente de Hello Modificar volumen.
4. Hola modificar el Asistente para volumen, en **configuración básica**, puede hacer siguiente hello:
   
   * Editar hello **nombre**.
   * Convertir hello **tipo de uso** desde tootiered anclado localmente o desde toolocally en capas anclado (vea [cambiar el tipo de volumen hello](#change-the-volume-type) para obtener más información).
   * Aumentar hello **capacidad aprovisionada**. Hola **capacidad aprovisionada** solo puede incrementarse. No se puede reducir un volumen después de crearlo.
5. En **configuración adicional**, puede modificar Hola ACR, siempre que el volumen de hello está sin conexión. Si el volumen de hello está en línea, deberá tootake primero sin conexión. Consulte los pasos de toohello en [desconectar un volumen](#take-a-volume-offline) toomodifying anterior Hola ACR.
   
   > [!NOTE]
   > No se puede cambiar hello **habilitar una copia de seguridad predeterminado** opción volumen Hola.
   > 
   > 
6. Guarde los cambios haciendo clic en el icono de verificación de Hola ![icono de marca de verificación](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png). Hola portal de Azure clásico mostrará un mensaje de volumen de actualización. Mostrará un mensaje de confirmación cuando se ha actualizado correctamente el volumen de Hola.
7. Si se va a expandir un volumen, complete Hola siguiendo los pasos en el equipo de host de Windows:
   
   1. Vaya demasiado**administración de equipos** ->**administración de discos**.
   2. Haga clic con el botón derecho en **Administración de discos** y seleccione **Volver a examinar los discos**.
   3. En lista de Hola de discos, seleccione el volumen de Hola que ha actualizado, contextual y, a continuación, seleccione **Extender volumen**. se inicia el Asistente para extender volúmenes de Hola. Haga clic en **Siguiente**.
   4. Complete el Asistente de hello, acepte los valores predeterminados de Hola. Una vez finalizado el Asistente de hello, volumen de hello debe mostrar hello mayor tamaño.
      
      > [!NOTE]
      > Si expanda un volumen anclado localmente y, a continuación, otro localmente anclados volumen inmediatamente después, se ejecutan trabajos de expansión del volumen de hello secuencialmente. primer trabajo de expansión del volumen Hola debe finalizar para que pueda comenzar el siguiente trabajo de expansión del volumen Hola.
      > 
      > 

![Vídeo disponible](./media/storsimple-manage-volumes-u2/Video_icon.png)**Vídeo disponible**

toowatch un vídeo que muestra cómo tooexpand un volumen, haga clic en [aquí](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).

## <a name="change-hello-volume-type"></a>Cambiar el tipo de volumen Hola
Puede cambiar el tipo de volumen Hola de toolocally en capas anclado o de tootiered anclado localmente. Sin embargo, esta conversión no debería tener lugar con frecuencia. Algunas de las razones para convertir un volumen de toolocally en capas anclado son:

* Garantías locales respecto a la disponibilidad de datos y el rendimiento.
* Eliminación de problemas de conectividad y latencias en la nube.

Normalmente, estos son pequeños volúmenes existentes que desea tooaccess con frecuencia. Un volumen anclado localmente está aprovisionado por completo cuando se crea. Si va a convertir un volumen de volumen en capas tooa anclado localmente, StorSimple comprueba que haya espacio suficiente en el dispositivo antes de iniciar la conversión de Hola. Si no tiene suficiente espacio, recibirá un error y se cancelará la operación de Hola. 

> [!NOTE]
> Antes de comenzar una conversión de en capas toolocally anclado, asegúrese de que consideres Hola requisitos de espacio de las otras cargas de trabajo. 
> 
> 

Puede ser conveniente toochange un tooa volumen anclado localmente en niveles de volumen si necesita espacio adicional tooprovision otros volúmenes. Al convertir tootiered de volumen de hello anclado localmente, Hola capacidad disponible en los incrementos de dispositivo de Hola por tamaño de hello de la capacidad de hello publicado. Si los problemas de conectividad evitan la conversión de Hola de un volumen de hello tipo local toohello en niveles tipo, hello volumen local que va a mostrar propiedades de un volumen en capas hasta que se complete la conversión de Hola. Esto es porque pueden que algunos datos hayan esparcido toohello en la nube. Estos datos volcados seguirán toooccupy espacio local en dispositivo Hola que no se liberarán hasta que la operación de Hola se reinicia y se completó.

> [!NOTE]
> La conversión de un volumen puede tardar algún tiempo y una conversión no se puede cancelar una vez que se ha iniciado. Hola volumen permanece en línea durante la conversión de hello y puede realizar copias de seguridad, pero no se puede expandir o restaurar el volumen de hello mientras conversión Hola lleva a cabo.  
> 
> 

Conversión de un volumen en capas tooa anclado localmente puede afectar negativamente el rendimiento del dispositivo. Además, Hola después factores podría aumentar Hola tiempo de conversión de Hola toocomplete:

* No hay suficiente ancho de banda.
* No hay ninguna copia de seguridad actual.

efectos de hello toominimize que podrían tener estos factores:

* Revise su directivas de límite de ancho de banda y asegúrese de que haya disponible un ancho de banda dedicado de 40 Mbps.
* Programar la conversión de Hola durante horas de poca actividad.
* Tome una instantánea en la nube antes de empezar la conversión de Hola.

Si va a convertir varios volúmenes (compatible con distintas cargas de trabajo), a continuación, debe dar prioridad conversión del volumen de Hola para que los volúmenes mayor prioridad se convierten en primer lugar. Por ejemplo, debe convertir los volúmenes que hospedan máquinas virtuales o volúmenes con cargas de trabajo SQL antes que los volúmenes con cargas de trabajo de recursos compartidos de archivos.

#### <a name="toochange-hello-volume-type"></a>tipo de volumen de hello toochange
1. En hello **dispositivos** , seleccione dispositivos hello, haga doble clic en él y, a continuación, haga clic en hello **contenedores de volúmenes** ficha.
2. Seleccione un contenedor de volúmenes de lista de Hola y haga doble clic en él volúmenes de hello tooview asociados con el contenedor de Hola.
3. Seleccione un volumen y, en la parte inferior de Hola de página de hello, haga clic en **modificar**. se inicia el Asistente de Hello Modificar volumen.
4. En hello **configuración básica** página, cambie el tipo de uso de hello, seleccione Nuevo tipo de hello en hello **tipo de uso** lista desplegable.
   
   * Si va a cambiar el tipo de hello demasiado**anclado localmente**, StorSimple comprobará toosee si no hay capacidad suficiente.
   * Si va a cambiar el tipo de hello demasiado**"en capas"** y este volumen se usará para los datos de archivo, seleccione hello **usar este volumen de datos acceso menos frecuente archivados** casilla de verificación.
     
       ![Casilla de verificación de archivo](./media/storsimple-manage-volumes-u2/ModifyTieredVolEx.png)
5. Haga clic en el icono de flecha de hello ![icono de flecha](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) toogo toohello **configuración adicional** página. Si está configurando un volumen anclado localmente, hello aparece siguiente mensaje.
   
    ![Cambiar el mensaje de tipo de volumen](./media/storsimple-manage-volumes-u2/ModifyLocalVolEx.png)
6. Haga clic en el icono de flecha de Hola ![Icono de flecha](./media/storsimple-manage-volumes-u2/HCS_ArrowIcon.png) nuevo toocontinue.
7. Haga clic en el icono de verificación de Hola ![Icono de marca de verificación](./media/storsimple-manage-volumes-u2/HCS_CheckIcon.png) proceso de conversión de toostart Hola. Hola portal de Azure mostrará un mensaje de volumen de actualización. Mostrará un mensaje de confirmación cuando se ha actualizado correctamente el volumen de Hola.

## <a name="take-a-volume-offline"></a>Desconectar un volumen
Puede que necesite tootake un volumen sin conexión cuando piensa toomodify lo o delete. Cuando un volumen está desconectado, no está disponible para el acceso de lectura y escritura. Necesitará tootake Hola volumen sin conexión en el host de hello, así como en el dispositivo de Hola. 

#### <a name="tootake-a-volume-offline"></a>tootake un volumen sin conexión
1. Asegúrese de que volumen hello en cuestión no está en uso antes de desconectarlo.
2. Desconecte volumen hello en el host de hello primero. Esto elimina cualquier riesgo potencial de daños en los datos en el volumen de Hola. Para obtener pasos específicos, consulte las instrucciones de toohello para el sistema operativo host.
3. Después de hello host está sin conexión, desconecte el volumen de hello en dispositivo de hello sin conexión mediante la realización de hello pasos:
   
   1. En hello **dispositivos** , seleccione dispositivos hello, haga doble clic en él y, a continuación, haga clic en hello **contenedores de volúmenes** Hola de ficha **contenedores de volúmenes** pestaña listas en formato tabular todos los Hola contenedores de volúmenes que están asociados con el dispositivo de Hola.
   2. Seleccione un contenedor de volumen y haga clic en lista de hello toodisplay de todos los volúmenes de hello en contenedor de Hola.
   3. Seleccione un volumen y haga clic en **Desconectar**.
   4. Cuando se le pida confirmación, haga clic en **Sí**. Hola volumen debería estar ahora sin conexión.
      
      Después de un volumen está sin conexión, Hola **poner en conexión** opción está disponible.

> [!NOTE]
> Hola **desconectar** comando envía un volumen de saludo de solicitud toohello dispositivo tootake sin conexión. Si hosts siguen usando el volumen de hello, esto da como resultado las conexiones interrumpidas, pero dejar sin conexión el volumen de hello no producirá un error. 
> 
> 

## <a name="delete-a-volume"></a>Eliminar un volumen
> [!IMPORTANT]
> Puede eliminar un volumen solo si está desconectado.
> 
> 

Completar Hola siguiendo los pasos toodelete un volumen.

#### <a name="toodelete-a-volume"></a>toodelete un volumen
1. En hello **dispositivos** , seleccione dispositivos hello, haga doble clic en él y, a continuación, haga clic en hello **contenedores de volúmenes** ficha.
2. Seleccione el contenedor de volúmenes de Hola que tiene el volumen de hello desea toodelete. Haga clic en Hola Hola de tooaccess de contenedor de volumen **volúmenes** página.
3. Todos los volúmenes de hello asociados a este contenedor se muestran en formato tabular. Comprobar el estado de saludo del volumen de Hola que desea toodelete. Si desea toodelete de volumen de hello no está desconectado, dejarlo pasos hello en primer lugar, siguiente sin conexión [desconectar un volumen](#take-a-volume-offline).
4. Después de que el volumen de hello está sin conexión, haga clic en **eliminar** final Hola de página Hola.
5. Cuando se le pida confirmación, haga clic en **Sí**. volumen de Hola se eliminará y Hola **volúmenes** página mostrará la lista de hello actualizado de volúmenes en el contenedor de Hola.
   
   > [!NOTE]
   > Si elimina un volumen anclado localmente, puede que Hola espacio disponible para nuevos volúmenes no se actualiza inmediatamente. Hola el servicio StorSimple Manager actualiza periódicamente disponibles de espacio Hola local. Se recomienda que espere unos minutos antes de intentar nuevo volumen de toocreate Hola.<br> Además, si elimina un volumen anclado localmente y, a continuación, eliminar otro localmente anclados volumen inmediatamente después, se ejecutan trabajos de eliminación de volumen de hello secuencialmente. primer trabajo de eliminación de volumen Hola debe finalizar para que pueda comenzar el siguiente trabajo de eliminación de volumen Hola.
   > 
   > 

## <a name="monitor-a-volume"></a>Supervisar un volumen
La supervisión de volúmenes permite toocollect / O-estadísticas relacionadas con el de un volumen. Supervisión está habilitada de forma predeterminada para hello 32 primeros volúmenes que cree. La supervisión de volúmenes adicionales está deshabilitada de forma predeterminada. La supervisión de volúmenes clonados también está deshabilitada de forma predeterminada.

Realizar Hola siguiendo los pasos tooenable o deshabilitar la supervisión de un volumen.

#### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable o deshabilitar la supervisión de volúmenes
1. En hello **dispositivos** , seleccione dispositivos hello, haga doble clic en él y, a continuación, haga clic en hello **contenedores de volúmenes** ficha.
2. Seleccionar contenedor de volúmenes de hello en qué Hola reside el volumen y, a continuación, haga clic en Hola Hola de tooaccess de contenedor de volumen **volúmenes** página.
3. Todos los volúmenes de hello asociados a este contenedor se muestran en la vista tabular de Hola. Haga clic en y seleccione el volumen de Hola o un clon del volumen.
4. En la parte inferior de Hola de página de hello, haga clic en **modificar**.
5. En el Asistente para modificar el volumen de hello, en **configuración básica**, seleccione **habilitar** o **deshabilitar** de hello **supervisión** lista desplegable.

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[clonar un volumen de StorSimple](storsimple-clone-volume.md).
* Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).

