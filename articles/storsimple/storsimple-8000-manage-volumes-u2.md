---
title: "volúmenes de StorSimple aaaManage (actualización 3) | Documentos de Microsoft"
description: "Explica cómo tooadd, modificar, supervisar y eliminar volúmenes de StorSimple y cómo tootake ellos sin conexión si es necesario."
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
ms.workload: NA
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 6228c4486dd5a7887df670c4c4584c4edcdfc509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-volumes-update-3-or-later"></a>Usar Hola Administrador de dispositivos de StorSimple servicio toomanage volúmenes (Update 3 o posterior)

## <a name="overview"></a>Información general

Este tutorial le explica cómo toouse Hola toocreate de servicio de administrador de dispositivos de StorSimple y administrar los volúmenes en dispositivos de la serie StorSimple 8000 Hola con Update 3 y versiones posteriores.

Hola servicio Administrador de dispositivos de StorSimple es una extensión en hello portal de Azure que le permite administrar la solución de StorSimple de una única interfaz web. Usar volúmenes toomanage portal Azure de hello en todos los dispositivos. También puede crear y administrar los servicios de StorSimple, administrar dispositivos, directivas de copia de seguridad y el catálogo de copias de seguridad, y ver las alertas.

## <a name="volume-types"></a>Tipos de volúmenes

Los volúmenes de StorSimple pueden ser:

* **Anclado localmente volúmenes**: los datos en estos volúmenes permanecen en el dispositivo StorSimple local hello en todo momento.
* **En niveles volúmenes**: datos de estos volúmenes pueden retrasar toohello en la nube.

Un volumen de archivo es un tipo de volumen en capas. Hola desduplicación fragmento tamaño usado para los volúmenes de archivado permite segmentos de mayor tootransfer de hello dispositivo de datos toohello en la nube.

Si es necesario, puede cambiar el tipo de volumen Hola de tootiered local o de toolocal en capas. Para obtener más información, consulte demasiado[cambiar el tipo de volumen hello](#change-the-volume-type).

### <a name="locally-pinned-volumes"></a>Volúmenes anclados localmente

Los volúmenes anclados localmente son totalmente aprovisionados volúmenes que no capa de datos toohello en la nube, lo que garantiza que local garantiza de datos principales, independientemente de conectividad en la nube. Los datos de los volúmenes anclados localmente no se desduplican ni comprimen, pero las instantáneas de dichos volúmenes se desduplican. 

Los volúmenes anclados localmente están totalmente aprovisionados, por lo que debe haber espacio suficiente en el dispositivo cuando los crea. Puede aprovisionar volúmenes anclados localmente tooa tamaño máximo de 8 TB en el dispositivo de StorSimple 8100 hello y 20 TB en dispositivo 8600 de Hola. StorSimple reserva el espacio local restantes hello en dispositivo Hola de instantáneas, metadatos y el procesamiento de datos. Puede aumentar tamaño de Hola de un volumen anclado localmente toohello espacio máximo disponible, pero no se puede reducir tamaño de Hola de un volumen una vez creado.

Cuando se crea un volumen anclado localmente, se reduce el espacio disponible de hello para la creación de volúmenes en capas. Hola inversa también es cierto: si tiene volúmenes en capas existentes, espacio de hello disponible para crear localmente anclado volúmenes será inferior a los límites máximos Hola indicados anteriormente. Para obtener más información sobre los volúmenes locales, consulte toohello [preguntas más frecuentes sobre los volúmenes anclados localmente](storsimple-8000-local-volume-faq.md).

### <a name="tiered-volumes"></a>Volúmenes en capas

Los volúmenes en capas son volúmenes con aprovisionamiento fino en qué Hola con frecuencia datos de acceso permanece local en el dispositivo de Hola y menos datos utilizados con frecuencia es automáticamente en niveles toohello en la nube. El aprovisionamiento fino es una tecnología de virtualización en el que el almacenamiento disponible parece tooexceed los recursos físicos. En lugar de reservar almacenamiento suficiente de antemano, StorSimple usa tooallocate de aprovisionamiento fino suficiente requisitos de espacio en toomeet actual. naturaleza elástica de Hola de almacenamiento en nube facilita este enfoque porque StorSimple puede aumentar o disminuir toomeet cambiantes exigencias de almacenamiento de nube.

Si utilizas Hola volumen en capas para los datos de archivo, seleccione hello **usar este volumen de datos acceso menos frecuente archivados** tamaño del fragmento de desduplicación casilla toochange Hola para su volumen too512 KB. Si no selecciona esta opción, el volumen en capas correspondiente de Hola utilizará un tamaño de fragmento de 64 KB. Un tamaño de fragmento de desduplicación permite la transferencia de hello tooexpedite hello de dispositivo de nube de toohello de los datos de archivo grande.


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

## <a name="hello-volumes-blade"></a>hoja de volúmenes de Hola

Hola **volúmenes** hoja permite los volúmenes de almacenamiento de hello toomanage que se ha aprovisionado en el dispositivo de StorSimple de Microsoft Azure de Hola para sus iniciadores (servidores). Muestra la lista de Hola de volúmenes en hello StorSimple dispositivos conectados tooyour servicio.

 ![Página de volúmenes](./media/storsimple-8000-manage-volumes-u2/volumeslist.png)

Un volumen se compone de una serie de atributos:

* **Nombre del volumen** : un nombre descriptivo que debe ser únicos y ayuda a identificar el volumen de Hola. Este nombre también se usa en los informes de supervisión cuando se filtra por un volumen específico. Una vez que se crea el volumen de hello, no se puede cambiar el nombre.
* **Estado** : puede estar conectado o desconectado. Si un volumen está sin conexión, no es visible tooinitiators (servidores) que se permiten acceso toouse Hola volumen.
* **Capacidad** : especifica la cantidad total de Hola de datos que se pueden almacenar por el iniciador de hello (servidor). Los volúmenes anclados localmente se aprovisionan por completo y residen en el dispositivo StorSimple Hola. Aprovisionamiento fino de los volúmenes en capas y Hola datos se desduplican. Con volúmenes con aprovisionamiento fino, el dispositivo no preasigne la capacidad de almacenamiento físico internamente o en la nube de hello según la capacidad del volumen tooconfigured. capacidad del volumen Hola se asigna y consume a demanda.
* **Tipo de** : indica si el volumen de hello es **"en capas"** (Hola predeterminado) o **anclado localmente**.

Use las instrucciones de hello en este hello tooperform tutorial siguiente las tareas:

* Agregar un volumen 
* Modificar un volumen 
* Cambiar el tipo de volumen Hola
* Eliminar un volumen 
* Desconectar un volumen 
* Supervisar un volumen 

## <a name="add-a-volume"></a>Agregar un volumen

Ya [creó un volumen](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume) durante la implementación del dispositivo de la serie StorSimple 8000. El procedimiento para agregar un volumen es similar.

#### <a name="tooadd-a-volume"></a>tooadd un volumen

1. Desde la lista tabular de Hola de dispositivos de Hola Hola **dispositivos** hoja, seleccione el dispositivo. Haga clic en **+ Agregar volumen**.

    ![Adición de un nuevo volumen](./media/storsimple-8000-manage-volumes-u2/step5createvol1.png)

2. Hola **agregar un volumen** hoja:
   
    1. Hola **dispositivo seleccione** campo se rellena automáticamente con el dispositivo actual.

    2. Desde la lista desplegable de hello, seleccione el contenedor de volúmenes de hello en las que necesite tooadd un volumen.

    3.  Escriba un **Nombre** para el volumen. Una vez que se crea el volumen de hello, no se puede cambiar el nombre de volumen de Hola.

    4. En la lista desplegable de hello, seleccione hello **tipo** para su volumen. Para cargas de trabajo que requieren garantías locales, latencias bajas y un rendimiento más alto, seleccione un volumen **Localmente anclado** . Para todos los demás datos, seleccione un volumen **En capas** . Si usa este volumen para datos de archivo, seleccione **Usar este volumen para los datos de archivo a los que accede con menos frecuencia**.
      
       Un volumen en capas se aprovisiona de manera fina y se puede crear rápidamente. Seleccionar **usar este volumen de datos acceso menos frecuente archivados** volumen en capas destinado a los datos de archivo cambios tamaño del fragmento de desduplicación de Hola para su volumen too512 KB. Si este campo no está activado, volumen en capas correspondiente de hello usa un tamaño de fragmento de 64 KB. Un tamaño de fragmento de desduplicación permite la transferencia de hello tooexpedite hello de dispositivo de nube de toohello de los datos de archivo grande.
       
       Un volumen anclado localmente se realiza un aprovisionamiento grueso y asegura que los datos principal de hello en volumen de hello permanece dispositivo toohello local y no volcarse toohello en la nube.  Si crea un volumen anclado localmente, comprobación de espacio disponible en los niveles de hello local dispositivo de hello tooprovision volumen de Hola de hello tamaño solicitado. operación Hola de creación de un volumen anclado localmente puede implicar verter los datos existentes de la nube de toohello de dispositivo de Hola y Hola tomadas el volumen de hello toocreate puede ser largo. tiempo total de Hello depende de tamaño de hello del volumen de hello aprovisionado, el ancho de banda de red disponible y datos de hello en el dispositivo.

    5. Especificar hello **capacidad aprovisionada** para su volumen. Tome nota de la capacidad de Hola que está disponible en función de tipo de volumen de hello seleccionado. Hola especifica el tamaño del volumen no debe superar el espacio disponible de Hola.
      
       Puede aprovisionar volúmenes en capas hasta too200 TB en dispositivo 8100 Hola o volúmenes anclados localmente una too8.5 TB. En el dispositivo 8600 mayor de hello, puede aprovisionar volúmenes anclados localmente una too22.5 TB o volúmenes en capas hasta too500 TB. Que haya espacio local en el dispositivo de Hola Hola toohost necesario trabajar el conjunto de volúmenes en capas, creación de volúmenes anclados localmente afecta Hola espacio disponible para aprovisionar volúmenes en capas. Por lo tanto, si crea un volumen anclado localmente, se reduce el espacio disponible para la creación de volúmenes en capas. De forma similar, si se crea un volumen en capas, se reduce el espacio disponible de hello para la creación de volúmenes anclados localmente.
      
       Si se aprovisiona un volumen anclado localmente de 8,5 TB (tamaño máximo permitido) en el dispositivo 8100, es que agote todo Hola local el espacio disponible en los dispositivos de Hola. No se puede crear cualquier volumen en capas desde ese punto en adelante, porque no hay ningún espacio local en espacio de trabajo de hello dispositivo toohost Hola de hello en niveles de volumen. Volúmenes en capas existentes también afectan al espacio Hola disponible. Por ejemplo, si tiene un dispositivo 8100 que ya cuenta con volúmenes en capas de aproximadamente 106 TB, solo 4 TB de espacio estarán disponibles para volúmenes anclados localmente.

    6. Hola **hosts conectados** , a continuación, haga clic en la flecha de Hola. 

        ![Hosts conectados](./media/storsimple-8000-manage-volumes-u2/step5createvol2.png)

    7. Hola **hosts conectados** hoja, seleccione un ACR existente o agregue un nuevo ACR. Si elige un nuevo ACR, a continuación, proporcione un **nombre** para el ACR, proporcionar hello **iSCSI Qualified Name** (IQN) de su host de Windows. Si no tienes Hola IQN, vaya demasiado[Get hello IQN de un host de Windows Server](#get-the-iqn-of-a-windows-server-host). Haga clic en **Crear**. Se crea un volumen con hello especificado valores.

        ![Click Create](./media/storsimple-8000-manage-volumes-u2/step5createvol3.png)

El nuevo volumen ahora está listo toouse.

> [!NOTE]
> Si crea un volumen anclado localmente y, a continuación, crear otro localmente anclados volumen inmediatamente después, se ejecutan los trabajos de creación de volumen de hello secuencialmente. primer trabajo de creación de volumen Hola debe finalizar para que pueda comenzar el siguiente trabajo de creación de volumen Hola.

## <a name="modify-a-volume"></a>Modificar un volumen

Modificar un volumen cuando necesite tooexpand, o cambiar Hola hosts que tienen acceso a los volúmenes de Hola.

> [!IMPORTANT]
> * Si modifica el tamaño del volumen de hello en dispositivo de hello, el tamaño del volumen de hello debe toobe cambia en el host de hello así.
> * pasos de lado del host de Hello descritos aquí son para Windows Server 2012 (2012R2). Los procedimientos para Linux u otros sistemas operativos de host serán diferentes. Consulte instrucciones del sistema operativo host tooyour al modificar el volumen de hello en un host que ejecuta otro sistema operativo.

#### <a name="toomodify-a-volume"></a>toomodify un volumen

1. Servicio de administrador de dispositivos de StorSimple tooyour y, a continuación, haga clic en **dispositivos**. Desde la lista tabular de Hola de dispositivos de hello, seleccione el dispositivo de Hola que tiene intención de toomodify de volumen de Hola. Haga clic en **Configuración > Volúmenes**.

    ![Vaya tooVolumes hoja](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

2. De hello tabular listado de volúmenes, seleccione el volumen de Hola y haga clic en el menú contextual de tooinvoke Hola. Seleccione **desconectar** volumen de hello tootake modificará sin conexión.

    ![Seleccionar y desconectar el volumen](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. Hola **desconectar** hoja, revisar Hola impacto de desconectar el volumen de Hola y seleccione Hola casilla de verificación correspondiente. Asegúrese de que volumen correspondiente de hello en el host de hello es sin conexión por primera vez. Para obtener información sobre cómo tootake un volumen sin conexión en el servidor de host había conectado tooStorSimple, consulte toooperating instrucciones específicas del sistema. Haga clic en **Desconectar**.

    ![Revisar el impacto de desconectar el volumen](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

4. Después de volumen de hello está sin conexión (como se muestra en el estado del volumen de hello), seleccione el volumen de Hola y haga clic en el menú contextual de tooinvoke Hola. Seleccione **Modificar volumen**.

    ![Seleccionar Modificar volumen](./media/storsimple-8000-manage-volumes-u2/modifyvol9.png)


5. Hola **Modificar volumen** hoja, puede hacer Hola siguientes cambios:
   
   1. Hola volumen **nombre** no se puede editar.
   2. Convertir hello **tipo** desde tootiered anclado localmente o desde toolocally en capas anclado (vea [cambiar el tipo de volumen hello](#change-the-volume-type) para obtener más información).
   3. Aumentar hello **capacidad aprovisionada**. Hola **capacidad aprovisionada** solo puede incrementarse. No se puede reducir un volumen después de crearlo.
   4. En **hosts conectados**, puede modificar Hola ACR. toomodify un ACR, volumen de hello debe estar sin conexión.

       ![Revisar el impacto de desconectar el volumen](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

5. Haga clic en **guardar** toosave los cambios. Cuando se le pida confirmación, haga clic en **Sí**. Hola portal de Azure mostrará un mensaje de volumen de actualización. Mostrará un mensaje de confirmación cuando se ha actualizado correctamente el volumen de Hola.

    ![Revisar el impacto de desconectar el volumen](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)

7. Si se va a expandir un volumen, complete Hola siguiendo los pasos en el equipo de host de Windows:
   
   1. Vaya demasiado**administración de equipos** ->**administración de discos**.
   2. Haga clic con el botón derecho en **Administración de discos** y seleccione **Volver a examinar los discos**.
   3. En lista de Hola de discos, seleccione el volumen de Hola que ha actualizado, contextual y, a continuación, seleccione **Extender volumen**. se inicia el Asistente para extender volúmenes de Hola. Haga clic en **Siguiente**.
   4. Complete el Asistente de hello, acepte los valores predeterminados de Hola. Una vez finalizado el Asistente de hello, volumen de hello debe mostrar hello mayor tamaño.
      
      > [!NOTE]
      > Si expanda un volumen anclado localmente y, a continuación, otro localmente anclados volumen inmediatamente después, se ejecutan trabajos de expansión del volumen de hello secuencialmente. primer trabajo de expansión del volumen Hola debe finalizar para que pueda comenzar el siguiente trabajo de expansión del volumen Hola.
      

## <a name="change-hello-volume-type"></a>Cambiar el tipo de volumen Hola

Puede cambiar el tipo de volumen Hola de toolocally en capas anclado o de tootiered anclado localmente. Sin embargo, esta conversión no debería tener lugar con frecuencia.

### <a name="tiered-toolocal-volume-conversion-considerations"></a>Consideraciones de conversión de volumen en capas toolocal

Algunas de las razones para convertir un volumen de toolocally en capas anclado son:

* Garantías locales respecto a la disponibilidad de datos y el rendimiento.
* Eliminación de problemas de conectividad y latencias en la nube.

Normalmente, estos son pequeños volúmenes existentes que desea tooaccess con frecuencia. Un volumen anclado localmente está aprovisionado por completo cuando se crea. 

Si va a convertir un volumen de volumen en capas tooa anclado localmente, StorSimple comprueba que haya espacio suficiente en el dispositivo antes de iniciar la conversión de Hola. Si no tiene suficiente espacio, recibirá un error y se cancelará la operación de Hola. 

> [!NOTE]
> Antes de comenzar una conversión de en capas toolocally anclado, asegúrese de que consideres Hola requisitos de espacio de las otras cargas de trabajo. 

Conversión de un volumen en capas tooa anclado localmente puede afectar negativamente el rendimiento del dispositivo. Además, Hola después factores podría aumentar Hola tiempo de conversión de Hola toocomplete:

* No hay suficiente ancho de banda.
* No hay ninguna copia de seguridad actual.

efectos de hello toominimize que podrían tener estos factores:

* Revise su directivas de límite de ancho de banda y asegúrese de que haya disponible un ancho de banda dedicado de 40 Mbps.
* Programar la conversión de Hola durante horas de poca actividad.
* Tome una instantánea en la nube antes de empezar la conversión de Hola.

Si va a convertir varios volúmenes (compatible con distintas cargas de trabajo), a continuación, debe dar prioridad conversión del volumen de Hola para que los volúmenes mayor prioridad se convierten en primer lugar. Por ejemplo, debe convertir los volúmenes que hospedan máquinas virtuales o volúmenes con cargas de trabajo SQL antes que los volúmenes con cargas de trabajo de recursos compartidos de archivos.

### <a name="local-tootiered-volume-conversion-considerations"></a>Consideraciones de conversión de volumen local tootiered

Puede que desee toochange un tooa volumen anclado localmente en niveles de volumen si necesita espacio adicional tooprovision otros volúmenes. Al convertir tootiered de volumen de hello anclado localmente, Hola capacidad disponible en los incrementos de dispositivo de Hola por tamaño de hello de la capacidad de hello publicado. Si los problemas de conectividad evitan la conversión de Hola de un volumen de hello tipo local toohello en niveles tipo, hello volumen local que va a mostrar propiedades de un volumen en capas hasta que se complete la conversión de Hola. Esto es porque pueden que algunos datos hayan esparcido toohello en la nube. Estos datos volcados continúan toooccupy espacio local en dispositivo Hola que no se liberarán hasta que la operación de Hola se reinicia y se completó.

> [!NOTE]
> La conversión de un volumen puede tardar algún tiempo y una conversión no se puede cancelar una vez que se ha iniciado. Hola volumen permanece en línea durante la conversión de hello y puede realizar copias de seguridad, pero no se puede expandir o restaurar el volumen de hello mientras conversión Hola lleva a cabo.


#### <a name="toochange-hello-volume-type"></a>tipo de volumen de hello toochange

1. Servicio de administrador de dispositivos de StorSimple tooyour y, a continuación, haga clic en **dispositivos**. Desde la lista tabular de Hola de dispositivos de hello, seleccione el dispositivo de Hola que tiene intención de toomodify de volumen de Hola. Haga clic en **Configuración > Volúmenes**.

    ![Vaya tooVolumes hoja](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. De hello tabular listado de volúmenes, seleccione el volumen de Hola y haga clic en el menú contextual de tooinvoke Hola. Seleccione **Modificar**.

    ![Seleccionar Modificar en el menú contextual](./media/storsimple-8000-manage-volumes-u2/changevoltype2.png)

4. En hello **Modificar volumen** hoja, cambie el tipo de volumen Hola seleccionando nuevo tipo de Hola de Hola **tipo** lista desplegable.
   
   * Si va a cambiar el tipo de hello demasiado**anclado localmente**, StorSimple comprobará toosee si no hay capacidad suficiente.
   * Si va a cambiar el tipo de hello demasiado**"en capas"** y este volumen se usará para los datos de archivo, seleccione hello **usar este volumen de datos acceso menos frecuente archivados** casilla de verificación.
   * Si está configurando un volumen anclado localmente como en niveles o _viceversa_, aparece hello siguiente mensaje.
   
    ![Mensaje de cambio del tipo de volumen](./media/storsimple-8000-manage-volumes-u2/changevoltype3.png)

7. Haga clic en **guardar** cambios de hello toosave. Cuando se le solicite confirmación, haga clic en **Sí** proceso de conversión de toostart Hola. 

    ![Guardar y confirmar](./media/storsimple-8000-manage-volumes-u2/modifyvol11.png)

8. Hola portal de Azure muestra una notificación para la creación de trabajo de Hola que actualizaría volumen Hola. Haga clic en estado de Hola Hola notificaciones toomonitor de trabajo de conversión del volumen Hola.

    ![Trabajo de conversión de volumen](./media/storsimple-8000-manage-volumes-u2/changevoltype5.png)

## <a name="take-a-volume-offline"></a>Desconectar un volumen

Puede que necesite tootake un volumen sin conexión cuando está planeando toomodify o eliminar el volumen de Hola. Cuando un volumen está desconectado, no está disponible para el acceso de lectura y escritura. Debe desconectar volumen hello en el host de Hola y dispositivo Hola.

#### <a name="tootake-a-volume-offline"></a>tootake un volumen sin conexión

1. Asegúrese de que volumen hello en cuestión no está en uso antes de desconectarlo.
2. Desconecte volumen hello en el host de hello primero. Esto elimina cualquier riesgo potencial de daños en los datos en el volumen de Hola. Para obtener pasos específicos, consulte las instrucciones de toohello para el sistema operativo host.
3. Después de hello host está sin conexión, desconecte el volumen de hello en dispositivo de hello sin conexión mediante la realización de hello pasos:
   
    1. Servicio de administrador de dispositivos de StorSimple tooyour y, a continuación, haga clic en **dispositivos**. Desde la lista tabular de Hola de dispositivos de hello, seleccione el dispositivo de Hola que tiene intención de toomodify de volumen de Hola. Haga clic en **Configuración > Volúmenes**.

        ![Vaya tooVolumes hoja](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

    2. De hello tabular listado de volúmenes, seleccione el volumen de Hola y haga clic en el menú contextual de tooinvoke Hola. Seleccione **desconectar** volumen de hello tootake modificará sin conexión.

        ![Seleccionar y desconectar el volumen](./media/storsimple-8000-manage-volumes-u2/modifyvol4.png)

3. Hola **desconectar** hoja, revisar Hola impacto de desconectar el volumen de Hola y seleccione Hola casilla de verificación correspondiente. Haga clic en **Desconectar**. 

    ![Revisar el impacto de desconectar el volumen](./media/storsimple-8000-manage-volumes-u2/modifyvol5.png)
      
      Se le notificará cuando Hola volumen está desconectado. Hola volumen también actualiza el estado del tooOffline.
      
4. Después de un volumen está sin conexión, si selecciona el volumen de Hola y contextuales, **poner en conexión** opción está disponible en el menú contextual de Hola.

> [!NOTE]
> Hola **desconectar** comando envía un volumen de saludo de solicitud toohello dispositivo tootake sin conexión. Si hosts siguen usando el volumen de hello, esto da como resultado las conexiones interrumpidas, pero dejar sin conexión el volumen de hello no producirá un error.

## <a name="delete-a-volume"></a>Eliminar un volumen

> [!IMPORTANT]
> Puede eliminar un volumen solo si está desconectado.

Completar Hola siguiendo los pasos toodelete un volumen.

#### <a name="toodelete-a-volume"></a>toodelete un volumen

1. Servicio de administrador de dispositivos de StorSimple tooyour y, a continuación, haga clic en **dispositivos**. Desde la lista tabular de Hola de dispositivos de hello, seleccione el dispositivo de Hola que tiene intención de toomodify de volumen de Hola. Haga clic en **Configuración > Volúmenes**.

    ![Vaya tooVolumes hoja](./media/storsimple-8000-manage-volumes-u2/modifyvol2.png)

3. Comprobar el estado de saludo del volumen de Hola que desea toodelete. Si el volumen de hello desea toodelete no está sin conexión, desconectarlo primero. Siga los pasos de hello en [desconectar un volumen](#take-a-volume-offline).
4. Después de hello volumen está desconectado, seleccionar volumen hello, haga clic en el menú contextual de tooinvoke Hola y, a continuación, seleccione **eliminar**.

    ![Seleccionar Eliminar en el menú contextual](./media/storsimple-8000-manage-volumes-u2/deletevol1.png)

5. Hola **eliminar** hoja, revise y seleccione Hola casilla con impacto de saludo de la eliminación de un volumen. Al eliminar un volumen, se perderán todos los datos de Hola que reside en el volumen de Hola. 

    ![Guardado y confirmación de los cambios](./media/storsimple-8000-manage-volumes-u2/deletevol2.png)

6. Después de elimina el volumen de hello, Hola lista tabular de volúmenes actualiza eliminación de hello tooindicate.

    ![Lista de volúmenes actualizada](./media/storsimple-8000-manage-volumes-u2/deletevol3.png)
   
   > [!NOTE]
   > Si elimina un volumen anclado localmente, puede que Hola espacio disponible para nuevos volúmenes no se actualiza inmediatamente. Hola servicio Administrador de dispositivos de StorSimple actualiza periódicamente disponibles de espacio Hola local. Se recomienda que espere unos minutos antes de intentar nuevo volumen de toocreate Hola.
   >
   > Además, si elimina un volumen anclado localmente y, a continuación, eliminar otro localmente anclados volumen inmediatamente después, se ejecutan trabajos de eliminación de volumen de hello secuencialmente. primer trabajo de eliminación de volumen Hola debe finalizar para que pueda comenzar el siguiente trabajo de eliminación de volumen Hola.

## <a name="monitor-a-volume"></a>Supervisar un volumen

La supervisión de volúmenes permite toocollect / O-estadísticas relacionadas con el de un volumen. Supervisión está habilitada de forma predeterminada para hello 32 primeros volúmenes que cree. La supervisión de volúmenes adicionales está deshabilitada de forma predeterminada. 

> [!NOTE]
> La supervisión de volúmenes clonados está deshabilitada de forma predeterminada.


Realizar Hola siguiendo los pasos tooenable o deshabilitar la supervisión de un volumen.

#### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable o deshabilitar la supervisión de volúmenes

1. Servicio de administrador de dispositivos de StorSimple tooyour y, a continuación, haga clic en **dispositivos**. Desde la lista tabular de Hola de dispositivos de hello, seleccione el dispositivo de Hola que tiene intención de toomodify de volumen de Hola. Haga clic en **Configuración > Volúmenes**.
2. De hello tabular listado de volúmenes, seleccione el volumen de Hola y haga clic en el menú contextual de tooinvoke Hola. Seleccione **Modificar**.
3. Hola **Modificar volumen** hoja, para **supervisión** seleccione **habilitar** o **deshabilitar** tooenable o deshabilitar la supervisión.

    ![Deshabilitar la supervisión](./media/storsimple-8000-manage-volumes-u2/monitorvol1.png) 

4. Haga clic en **Guardar** y, cuando se le pida confirmación, haga clic en **Sí**. Hola portal de Azure muestra una notificación para actualizar el volumen de hello y, a continuación, en un mensaje de confirmación, después de que el volumen de Hola se actualizó correctamente.

## <a name="next-steps"></a>Pasos siguientes

* Obtenga información acerca de cómo demasiado[clonar un volumen de StorSimple](storsimple-8000-clone-volume-u2.md).
* Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de administrador de dispositivos de StorSimple el dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

