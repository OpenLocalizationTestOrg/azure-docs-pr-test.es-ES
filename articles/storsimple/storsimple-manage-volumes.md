---
title: "aaaManage los volúmenes de StorSimple | Documentos de Microsoft"
description: "Explica cómo tooadd, modificar, supervisar y eliminar volúmenes de StorSimple y cómo tootake ellos sin conexión si es necesario."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ccabd859-590c-4568-a81d-6ff38f125be3
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/11/2016
ms.author: v-sharos
ms.openlocfilehash: 8dc646261ee2ad8f2b80291518716f4de55b63f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-volumes"></a>Usar volúmenes de toomanage de servicio de StorSimple Manager Hola
[!INCLUDE [storsimple-version-selector-manage-volumes](../../includes/storsimple-version-selector-manage-volumes.md)]

## <a name="overview"></a>Información general
Este tutorial le explica cómo toouse Hola toocreate de servicio de StorSimple Manager y administrar los volúmenes en el dispositivo de StorSimple de Hola y el dispositivo virtual StorSimple.

Hola el servicio StorSimple Manager es una extensión de hello portal de Azure clásico que le permite administrar la solución de StorSimple de una única interfaz web. En volúmenes de toomanaging de suma, puede usar toocreate de servicio de StorSimple Manager hello y administrar los servicios de StorSimple, ver y administrar dispositivos, ver alertas y ver y administrar las directivas de copia de seguridad y el catálogo de copia de seguridad de Hola.

> [!NOTE]
> Azure StorSimple solo puede crear volúmenes con aprovisionamiento fino. No es posible crear volúmenes total o parcialmente aprovisionados en un sistema de Azure StorSimple.
> 
> El aprovisionamiento fino es una tecnología de virtualización en el que el almacenamiento disponible parece tooexceed los recursos físicos. En lugar de reservar almacenamiento suficiente de antemano, Azure StorSimple usa tooallocate de aprovisionamiento fino suficiente requisitos de espacio en toomeet actual. naturaleza elástica de Hola de almacenamiento en nube facilita este enfoque porque StorSimple de Azure puede aumentar o disminuir toomeet cambiantes exigencias de almacenamiento de nube.
> 
> 

## <a name="hello-volumes-page"></a>página de volúmenes de Hola
Hola **volúmenes** página permite los volúmenes de almacenamiento de hello toomanage que se ha aprovisionado en el dispositivo de StorSimple de Microsoft Azure de Hola para sus iniciadores (servidores). Muestra la lista de Hola de volúmenes en el dispositivo StorSimple.

 ![Página de volúmenes](./media/storsimple-manage-volumes/HCS_VolumesPage.png)

Un volumen se compone de una serie de atributos:

* **Nombre** : un nombre descriptivo que debe ser únicos y ayuda a identificar el volumen de Hola. Este nombre también se usa en los informes de supervisión cuando se filtra por un volumen específico.
* **Estado** : puede estar conectado o desconectado. Si un volumen está sin conexión, no es visible tooinitiators (servidores) que se permiten acceso toouse Hola volumen.
* **Capacidad** : especifica cómo gran volumen de hello es, según lo percibido por el iniciador de hello (servidor). Capacidad especifica la cantidad total de Hola de datos que se pueden almacenar por el iniciador de hello (servidor). Los volúmenes tienen aprovisionamiento fino y los datos están desduplicados. Esto implica que el dispositivo no preasigne la capacidad de almacenamiento físico internamente o en la nube de hello según la capacidad del volumen tooconfigured. capacidad del volumen Hola se asigna y consume a demanda.
* **Tipo de** : puede ser el tipo de volumen hello en capas o archivado (un subtipo de escalonado)
* **Acceso** – especifica iniciadores de hello (servidores) que se permiten acceso toothis volumen. Los iniciadores que no sean miembros del registro de control de acceso (ACR) que está asociado a Hola volumen no verán el volumen de Hola.
* **Supervisión** : especifica si se está supervisando un volumen. Un volumen tendrá la supervisión habilitada de forma predeterminada cuando se crea. Sin embargo, la supervisión estará deshabilitada para un clon del volumen. tooenable supervisión de un volumen, siga las instrucciones de hello en el Monitor de un volumen.

Hola tareas más comunes asociadas con un volumen son:

* Agregar un volumen
* Modificar un volumen
* Eliminar un volumen
* Desconectar un volumen
* Supervisar un volumen

## <a name="add-a-volume"></a>Agregar un volumen
Ya [creó un volumen](storsimple-deployment-walkthrough-u1.md#step-6-create-a-volume) durante la implementación de la solución de StorSimple. El procedimiento para agregar un volumen es similar.

### <a name="tooadd-a-volume"></a>tooadd un volumen
1. En hello **dispositivos** , seleccione dispositivos hello, haga doble clic en él y, a continuación, haga clic en hello **contenedores de volúmenes** ficha.
2. Seleccione un contenedor de volumen y haga clic en la flecha de hello en hello correspondiente fila tooaccess Hola volúmenes asociados con el contenedor de Hola.
3. Haga clic en **agregar** final Hola de página Hola. inicia el asistente Agregar un volumen de Hola.
   
     ![Agregar configuración básica del asistente de volumen](./media/storsimple-manage-volumes/AddVolume1.png)
4. Hola, agregar un asistente de volumen, en **configuración básica**, Hola siguientes:
   
   1. Proporcione un **Nombre** para el volumen.
   2. Especificar hello **capacidad aprovisionada** para su volumen en GB o TB. capacidad de Hello debe estar entre 1 GB y 64 TB para un dispositivo físico. capacidad máxima de Hola que se puede aprovisionar para un volumen en un dispositivo StorSimple virtual es de 30 TB.
   3. Seleccione hello **tipo de uso** para su volumen. Si utilizas Hola volumen en capas para los datos de archivo, seleccione hello **usar este volumen de datos acceso menos frecuente archivados** casilla de verificación cambia el tamaño del fragmento de desduplicación de Hola para su volumen too512 KB. Si no selecciona esta opción, el volumen en capas correspondiente de Hola utilizará un tamaño de fragmento de 64 KB. Un tamaño de fragmento de desduplicación permite la transferencia de hello tooexpedite hello de dispositivo de nube de toohello de los datos de archivo grande. (Volúmenes en capas se denominaban volúmenes principales.)
   4. Haga clic en el icono de flecha de hello ![icono de flecha](./media/storsimple-manage-volumes/HCS_ArrowIcon.png)toogo toohello **configuración adicional** página.
      
        ![Agregar configuración adicional del asistente de volumen](./media/storsimple-manage-volumes/AddVolume2.png)
5. En **Configuración adicional**, agregue un nuevo registro de control de acceso (ACR):
   
   1. Seleccione un registro de control de acceso (ACR) de la lista desplegable de Hola. También puede agregar un nuevo ACR. Acr determinan qué hosts pueden acceder a los volúmenes de hello coincidente IQN de host con el que aparece en el registro de hello.
   2. Se recomienda que habilite una copia de seguridad predeterminada seleccionando hello **habilitar una copia de seguridad predeterminado para este volumen** casilla de verificación.
   3. Haga clic en el icono de verificación de Hola ![Icono de marca de verificación](./media/storsimple-manage-volumes/HCS_CheckIcon.png) volumen de hello toocreate con hello especificó los valores.

El nuevo volumen ahora está listo toouse.

## <a name="modify-a-volume"></a>Modificar un volumen
Modificar un volumen cuando necesite tooexpand, o cambiar Hola hosts que tienen acceso a los volúmenes de Hola.

> [!IMPORTANT]
> * Si modifica el tamaño del volumen de hello en dispositivo de hello, el tamaño del volumen de hello debe toobe cambia en el host de hello así.
> * pasos de lado del host de Hello descritos aquí son para Windows Server 2012 (2012R2). Los procedimientos para Linux u otros sistemas operativos de host serán diferentes. Consulte instrucciones del sistema operativo host tooyour al modificar el volumen de hello en un host que ejecuta otro sistema operativo.
> 
> 

### <a name="toomodify-a-volume"></a>toomodify un volumen
1. En hello **dispositivos** , seleccione dispositivos hello, haga doble clic en él y, a continuación, haga clic en hello **contenedor de volúmenes** ficha. Esta página muestra en formato tabular de todos los contenedores de volúmenes de Hola que están asociados con el dispositivo de Hola.
2. Seleccione un contenedor de volumen y haga clic en lista de hello toodisplay de todos los volúmenes de hello en contenedor de Hola.
3. En hello **volúmenes** , seleccione un volumen y haga clic en **modificar**.
4. Hola modificar el Asistente para volumen, en **configuración básica**, puede hacer siguiente hello:
   
   * Editar hello **nombre** y **tipo** si desea toomodify un volumen de archivo de volumen en capas tooan seleccionando hello **usar este volumen de datos acceso menos frecuente archivados** tamaño del fragmento de desduplicación casilla toochange Hola para su volumen too512 KB.
   * Aumentar hello **capacidad aprovisionada**. Hola **capacidad aprovisionada** solo puede incrementarse. No se puede reducir un volumen después de crearlo.
     
     > [!NOTE]
     > No se puede cambiar contenedor de volúmenes de hello después de su asignación tooa volumen.
     > 
     > 
5. En **configuración adicional**, puede hacer siguiente hello:
   
   * Modificar ACR hello, siempre que el volumen de hello está sin conexión. Si el volumen de hello está en línea, deberá tootake primero sin conexión. Consulte los pasos de toohello en [desconectar un volumen](#take-a-volume-offline) toomodifying anterior Hola ACR.
   * Modificar la lista de Hola de ACR después Hola volumen está sin conexión.
     
     > [!NOTE]
     > No se puede cambiar hello **habilitar una copia de seguridad predeterminado para este volumen** opción volumen Hola.
     > 
     > 
6. Guarde los cambios haciendo clic en el icono de verificación de Hola ![icono de marca de verificación](./media/storsimple-manage-volumes/HCS_CheckIcon.png). Hola portal de Azure clásico mostrará un mensaje de volumen de actualización. Mostrará un mensaje de confirmación cuando se ha actualizado correctamente el volumen de Hola.
7. Si se va a expandir un volumen, complete Hola siguiendo los pasos en el equipo de host de Windows:
   
   1. Vaya demasiado**administración de equipos** ->**administración de discos**.
   2. Haga clic con el botón derecho en **Administración de discos** y seleccione **Volver a examinar los discos**.
   3. En lista de Hola de discos, seleccione el volumen de Hola que ha actualizado, contextual y, a continuación, seleccione **Extender volumen**. se inicia el Asistente para extender volúmenes de Hola. Haga clic en **Siguiente**.
   4. Complete el Asistente de hello, acepte los valores predeterminados de Hola. Una vez finalizado el Asistente de hello, volumen de hello debe mostrar hello mayor tamaño.

![Vídeo disponible](./media/storsimple-manage-volumes/Video_icon.png)**Vídeo disponible**

toowatch un vídeo que muestra cómo tooexpand un volumen, haga clic en [aquí](https://azure.microsoft.com/documentation/videos/expand-a-storsimple-volume/).

## <a name="take-a-volume-offline"></a>Desconectar un volumen
Puede que necesite tootake un volumen sin conexión cuando piensa toomodify lo o delete. Cuando un volumen está desconectado, no está disponible para el acceso de lectura y escritura. Necesitará tootake Hola volumen sin conexión en el host de hello, así como en el dispositivo de Hola. Realizar Hola siguiendo los pasos tootake un volumen sin conexión.

### <a name="tootake-a-volume-offline"></a>tootake un volumen sin conexión
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

### <a name="toodelete-a-volume"></a>toodelete un volumen
1. En hello **dispositivos** , seleccione dispositivos hello, haga doble clic en él y, a continuación, haga clic en hello **contenedores de volúmenes** ficha.
2. Seleccione el contenedor de volúmenes de Hola que tiene el volumen de hello desea toodelete. Haga clic en Hola Hola de tooaccess de contenedor de volumen **volúmenes** página.
3. Todos los volúmenes de hello asociados a este contenedor se muestran en formato tabular. Comprobar el estado de saludo del volumen de Hola que desea toodelete. Si desea toodelete de volumen de hello no está desconectado, dejarlo pasos hello en primer lugar, siguiente sin conexión [desconectar un volumen](#take-a-volume-offline).
4. Después de que el volumen de hello está sin conexión, haga clic en **eliminar** final Hola de página Hola.
5. Cuando se le pida confirmación, haga clic en **Sí**. volumen de Hola se eliminará y Hola **volúmenes** página mostrará la lista de hello actualizado de volúmenes en el contenedor de Hola.

## <a name="monitor-a-volume"></a>Supervisar un volumen
La supervisión de volúmenes permite toocollect / O-estadísticas relacionadas con el de un volumen. Supervisión está habilitada de forma predeterminada para hello 32 primeros volúmenes que cree. La supervisión de volúmenes adicionales está deshabilitada de forma predeterminada. La supervisión de volúmenes clonados también está deshabilitada de forma predeterminada.

Realizar Hola siguiendo los pasos tooenable o deshabilitar la supervisión de un volumen.

### <a name="tooenable-or-disable-volume-monitoring"></a>tooenable o deshabilitar la supervisión de volúmenes
1. En hello **dispositivos** , seleccione dispositivos hello, haga doble clic en él y, a continuación, haga clic en hello **contenedores de volúmenes** ficha.
2. Seleccionar contenedor de volúmenes de hello en qué Hola reside el volumen y, a continuación, haga clic en Hola Hola de tooaccess de contenedor de volumen **volúmenes** página.
3. Todos los volúmenes de hello asociados a este contenedor se muestran en la vista tabular de Hola. Haga clic en y seleccione el volumen de Hola o un clon del volumen.
4. En la parte inferior de Hola de página de hello, haga clic en **modificar**.
5. En el Asistente para modificar el volumen de hello, en **configuración básica**, seleccione **habilitar** o **deshabilitar** de hello **supervisión** lista desplegable.
   
    ![Modificar la configuración básica de un volumen](./media/storsimple-manage-volumes/HCS_MonitorVolumeM.png)

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[clonar un volumen de StorSimple](storsimple-clone-volume.md).
* Obtenga información acerca de cómo demasiado[uso Hola tooadminister de servicio de StorSimple Manager el dispositivo StorSimple](storsimple-manager-service-administration.md).

