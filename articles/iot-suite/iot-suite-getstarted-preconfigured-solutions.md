---
title: aaaGet a trabajar con soluciones preconfiguradas | Documentos de Microsoft
description: "Siga este tutorial toolearn cómo toodeploy un conjunto de IoT de Azure configurado previamente la solución."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a>Empezar a trabajar con soluciones de hello preconfigurado

Conjunto de Azure IoT [soluciones preconfiguradas] [ lnk-preconfigured-solutions] combinar varias IoT de Azure servicios toodeliver-to-end soluciones que implementan escenarios empresariales IoT. Hola *supervisión remota* solución preconfigurada conecta tooand supervisa los dispositivos. Puede utilizar Hola solución tooanalyze Hola flujo de datos de los dispositivos y los resultados del negocio tooimprove realizando procesos responder automáticamente toothat flujo de datos.

Este tutorial muestra cómo la supervisión remota de tooprovision Hola había preconfigurado solución. También le guía a través de características básicas de Hola de solución de hello preconfigurado. Puede tener acceso a muchas de estas características de solución de hello *panel* que implementa como parte de la solución de hello preconfigurado:

![Panel de la solución preconfigurada de supervisión remota][img-dashboard]

toocomplete este tutorial, necesita una suscripción activa de Azure.

> [!NOTE]
> En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para más información, consulte la [evaluación gratuita de Azure][lnk_free_trial].

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a>Información general de escenario

Al implementar Hola solución preconfigurada de supervisión remoto, se rellena previamente con recursos que permiten toostep a través de un escenario común de supervisión remoto. En este escenario, varios dispositivos conectados toohello solución dependen de los valores de temperatura inesperado. Hello las secciones siguientes muestran cómo para:

* Identificar los dispositivos de hello enviar valores de temperatura inesperado.
* Configurar estos dispositivos toosend más detallados telemetría.
* Corregir el problema de hello mediante la actualización de firmware de hello en estos dispositivos.
* Compruebe que la acción ha resuelto el problema de Hola.

Una característica clave de este escenario es que puede realizar todas estas acciones de forma remota desde el panel de la solución de Hola. No es necesario dispositivos toohello de acceso físico.

## <a name="view-hello-solution-dashboard"></a>Panel de vista Hola solución

panel de la solución de Hello permite toomanage solución de hello implementado. Por ejemplo, puede ver la telemetría, agregar dispositivos y configurar las reglas.

1. Cuando el aprovisionamiento de hello está completado e indica el icono de Hola para su solución preconfigurada **listo**, elija **iniciar** tooopen su portal de solución de supervisión remoto en una nueva pestaña.

    ![Iniciar solución de hello preconfigurado][img-launch-solution]

1. De forma predeterminada, el portal de solución de hello muestra hello *panel*. Puede navegar por las áreas de tooother del portal de solución de hello con menú de hello en el lado izquierdo de Hola de página de Hola.

    ![Panel de la solución preconfigurada de supervisión remota][img-menu]

panel de Hello muestra hello siguiente información:

* Un mapa que muestra la ubicación de Hola de cada dispositivo conectado toohello solución. Cuando ejecuta por primera vez solución hello, hay 25 dispositivos simulados. dispositivos simulados Hello se implementan una como trabajos Web de Azure y solución de hello usa información de tooplot de API de Bing Maps de hello en el mapa de Hola. Vea hello [preguntas más frecuentes sobre] [ lnk-faq] toolearn cómo toomake Hola dinámicos de mapa.
* Un panel **Historial de telemetría** que traza los datos de telemetría de temperatura y humedad de un dispositivo seleccionado prácticamente en tiempo real y muestra los datos agregados, como la humedad máxima, mínima y media.
* Un panel **Historial de alarmas** que muestra los últimos eventos de alarma cuando un valor de telemetría ha superado un umbral. Puede definir sus propios alarmas en ejemplos de adición toohello creados por la solución de hello preconfigurado.
* Un panel **Trabajos** que muestra información acerca de los trabajos programados. En la página **Trabajos de administración** puede programar sus propios trabajos.

## <a name="view-alarms"></a>Vista de alarmas

panel de historial de alarma de Hello muestra cinco dispositivos informas mayor que los valores de telemetría esperado.

![Historial de alarma de la lista de tareas en el panel de la solución de Hola][img-alarms]

> [!NOTE]
> Estas alarmas se generan por una regla que se incluye en la solución de hello preconfigurado. Esta regla genera una alerta cuando el valor de temperatura de hello enviada por un dispositivo supera los 60. Puede definir sus propias reglas y acciones eligiendo [reglas](#add-a-rule) y [acciones](#add-an-action) en el menú izquierdo Hola.

## <a name="view-devices"></a>Vista de dispositivos

Hola *dispositivos* lista muestra todos los dispositivos de hello registrado en soluciones de Hola. Desde la lista de dispositivos de hello, puede ver y editar los metadatos del dispositivo, agregar o quitar dispositivos e invocar métodos en los dispositivos. Puede filtrar y ordenar lista de Hola de dispositivos en la lista de dispositivos de Hola. También puede personalizar las columnas de Hola que se muestra en la lista de dispositivos de Hola.

1. Elija **dispositivos** tooshow lista de dispositivos de Hola para esta solución.

   ![Lista de dispositivos de Hola de vista en el portal de solución de Hola][img-devicelist]

1. lista de dispositivos de Hello inicialmente muestra 25 dispositivos simulados creados por el proceso de aprovisionamiento de Hola. Puede agregar más dispositivos simulados y físicos toohello solución.

1. detalles de hello tooview de un dispositivo, elija un dispositivo en la lista de dispositivos de Hola.

   ![Ver detalles del dispositivo hello en el portal de solución de Hola][img-devicedetails]

Hola **detalles del dispositivo** panel contiene seis secciones:

* Una colección de vínculos que permiten toocustomize Hola icono de dispositivo, deshabilitar dispositivos hello, agregar una regla, invocan un método o envían un comando. Para ver una comparación de comandos (mensajes de dispositivo a la nube) y métodos (métodos directos), consulte [Guía de comunicación de nube a dispositivo][lnk-c2d-guidance].
* Hola **dispositivo gemelas - etiquetas** sección le permite tooedit valores de etiqueta para el dispositivo de Hola. Puede mostrar valores de etiqueta en la lista de dispositivos de Hola y usar la lista de dispositivos de etiqueta valores toofilter Hola.
* Hola **dispositivo gemelas - propiedades deseado** sección le permite tooset propiedad valores toobe enviado toohello dispositivo.
* Hola **dispositivo gemelas - propiedades notificado** sección muestra valores de propiedad enviados desde dispositivo Hola.
* Hola **propiedades del dispositivo** sección muestra información del registro de la identidad de hello como dispositivo de hello claves id y la autenticación.
* Hola **trabajos recientes** sección muestra información sobre todos los trabajos que tienen recientemente destinados a este dispositivo.

## <a name="filter-hello-device-list"></a>Filtrar la lista de dispositivos de Hola

Puede usar un filtro toodisplay solo aquellos dispositivos que va a enviar valores de temperatura inesperado. Hola remoto solución preconfigurada de supervisión incluye hello **dispositivos en mal estado** filtrar los dispositivos tooshow con un valor de temperatura media superior a 60. También puede [crear sus propios filtros](#add-a-filter).

1. Elija **Abrir filtro guardado** toodisplay una lista de los filtros disponibles. A continuación, elija **dispositivos en mal estado** filtro de Hola tooapply:

    ![Mostrar la lista de Hola de filtros][img-unhealthy-filter]

1. lista de dispositivos de Hello ahora muestra solo los dispositivos con un valor de la temperatura media superior a 60.

    ![Lista de dispositivos filtrado de Hola de vista que muestra los dispositivos en mal estado][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a>Actualizar las propiedades deseadas

Ha identificado un conjunto de dispositivos que pueden necesitar corrección. Sin embargo, decide que no es suficiente para un diagnóstico más detallado claro del problema de Hola frecuencia de datos de Hola de 15 segundos. Cambiar Hola telemetría frecuencia toofive segundos tooprovide con toobetter de puntos de datos más diagnosticar el problema de Hola. Puede insertar esta configuración cambio tooyour los dispositivos remotos desde el portal de solución de Hola. Puede realizar el cambio de hello una vez, evaluar el impacto de hello y, a continuación, actuar en los resultados de Hola.

Siga estos toorun pasos un trabajo que cambia hello **TelemetryInterval** deseado de propiedad para los dispositivos de hello afectado. Cuando los dispositivos de hello reciben Hola nueva **TelemetryInterval** valor de propiedad, cambian su telemetría de toosend configuración cada cinco segundos en lugar de cada 15 segundos:

1. Mientras se visualizan lista Hola de dispositivos incorrecto en la lista de dispositivos de hello, elija **programador de trabajos**, a continuación, **Editar dispositivo gemelas**.

1. Llamar al trabajo de hello **intervalo de cambio de telemetría**.

1. Cambiar valor Hola de hello **propiedad deseada** nombre **deseado. Config.TelemetryInterval** toofive segundos.

1. Seleccione **Programación**.

    ![Cambiar hello TelemetryInterval propiedad toofive segundos][img-change-interval]

1. Puede supervisar el progreso de hello del trabajo de hello en hello **trabajos de administración** página del portal de Hola.

> [!NOTE]
> Si desea toochange un valor de propiedad para un dispositivo individual, utilice hello **propiedades deseadas** sección Hola **detalles del dispositivo** panel en lugar de ejecutar un trabajo.

Esta tarea establece el valor de Hola de hello **TelemetryInterval** deseado propiedad gemelas de dispositivo de Hola para todos los dispositivos seleccionados por el filtro de Hola de Hola. dispositivos de Hello recuperar este valor del doble de dispositivo de Hola y actualización su comportamiento. Cuando un dispositivo recupera y procesa una propiedad deseada de un doble de dispositivo, Establece Hola correspondiente notificado value (propiedad).

## <a name="invoke-methods"></a>Invocación de métodos

Mientras se ejecuta el trabajo de hello, observará en lista de Hola de dispositivos incorrecto que todos estos dispositivos tienen firmware antiguo (menor que la versión 1.6) versiones.

![Hola de vista notifica la versión de firmware para dispositivos en mal estado Hola][img-old-firmware]

Esta versión de firmware puede ser la causa de raíz de Hola de hello inesperado porque sabe que otros dispositivos correcto eran actualizado recientemente tooversion 2.0 de los valores de temperatura. También puede usar integrada de hello **dispositivos de firmware anterior** filtrar tooidentify los dispositivos con las versiones de firmware anteriores. Desde el portal de hello, a continuación, se pueden actualizar remotamente todos los dispositivos de hello sigan ejecutando versiones de firmware anterior:

1. Elija **Abrir filtro guardado** toodisplay una lista de los filtros disponibles. A continuación, elija **dispositivos de firmware anterior** filtro de Hola tooapply:

    ![Mostrar la lista de Hola de filtros][img-old-filter]

1. lista de dispositivos de Hello ahora muestra solo los dispositivos con las versiones de firmware anteriores. Esta lista incluye cinco dispositivos de hello identificados por hello **dispositivos en mal estado** filtro y tres dispositivos adicionales:

    ![Lista de dispositivos filtrado de Hola de vista mostrará dispositivos antiguos][img-filtered-old-list]

1. Elija **Programador de trabajos** y a continuación, **Invocar método**.

1. Establecer **nombre del trabajo** demasiado**tooversion de actualización de Firmware 2.0**.

1. Elija **InitiateFirmwareUpdate** como hello **método**.

1. Conjunto hello **FwPackageUri** parámetro demasiado**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.

1. Seleccione **Programación**. valor predeterminado de Hello es Hola trabajo toorun ahora.

    ![Crear el firmware de Hola de tooupdate de trabajo de los dispositivos de hello seleccionado][img-method-update]

> [!NOTE]
> Elija si desea que un método en un dispositivo individual tooinvoke, **métodos** en hello **detalles del dispositivo** panel en lugar de ejecutar un trabajo.

Este trabajo invoca hello **InitiateFirmwareUpdate** método directo en todos los dispositivos de Hola Hola filtro seleccionados. Dispositivos responderán inmediatamente tooIoT concentrador y, a continuación, inician el proceso de actualización de firmware de Hola de forma asincrónica. los dispositivos de Hello proporcionan información de estado sobre el proceso de actualización de firmware de Hola a través de los valores de propiedad notificado, como se muestra en las siguientes capturas de pantalla de Hola. Elija hello **actualizar** información de Hola de icono tooupdate en las listas de dispositivo y el trabajo de hello:

![Lista de trabajos que muestra la ejecución de lista de actualización de firmware de hello][img-update-1]
![lista de dispositivos que muestra el estado de actualización de firmware][img-update-2]
![trabajo mostrando Hola firmware actualización lista completa][img-update-3]

> [!NOTE]
> En un entorno de producción, puede programar trabajos toorun durante una ventana de mantenimiento designado.

## <a name="scenario-review"></a>Revisión del escenario

En este escenario, ha identificado un problema potencial con algunos de los dispositivos remotos mediante el historial de alarma de hello en el panel de Hola y un filtro. Que, a continuación, filtro Hola usado y un trabajo tooremotely configuran Hola dispositivos tooprovide más toohelp información diagnosticar el problema de Hola. Por último, se utilizan un filtro y un mantenimiento de tooschedule de trabajo en los dispositivos de hello afectado. Si devuelve toohello panel, puede comprobar que ya no son las alarmas procedentes de dispositivos de la solución. Puede utilizar un filtro tooverify que Hola firmware está actualizado en todos los dispositivos de hello en la solución y que no son dispositivos no hay más incorrecto:

![Filtro que muestra que todos los dispositivos tienen firmware actualizado][img-updated]

![Filtro que muestra que todos los dispositivos tiene un estado correcto][img-healthy]

## <a name="other-features"></a>Otras características

Hello las secciones siguientes describen algunas características adicionales de hello solución preconfigurada de supervisión remota que no se describen como parte del escenario anterior Hola.

### <a name="customize-columns"></a>Personalización de columnas

Puede personalizar la información de Hola se muestra en la lista de dispositivos de hello eligiendo **editor columna**. Puede agregar y quitar las columnas que muestran los valores de propiedad y etiqueta notificados. Las columnas también se pueden reordenar y cambiar de nombre:

   ![Lista de dispositivos de columna editor ion Hola][img-columneditor]

### <a name="customize-hello-device-icon"></a>Personalizar el icono de dispositivo de Hola

Puede personalizar el icono de dispositivo de hello aparece en la lista de dispositivos de Hola de hello **detalles del dispositivo** panel como se indica a continuación:

1. Elija Hola Hola de tooopen de icono de lápiz **Editar imagen** panel para un dispositivo:

   ![Abrir el editor de imágenes del dispositivo][img-startimageedit]

1. Cargar una nueva imagen o utilizar una de las imágenes existentes hello y, a continuación, elija **guardar**:

   ![Modificar editor de imágenes del dispositivo][img-imageedit]

1. Hello imagen que ha seleccionado ahora muestra de Hola **icono** columna para dispositivo Hola.

> [!NOTE]
> image de Hola se almacena en almacenamiento de blobs. Una etiqueta en gemelas de dispositivo de hello contiene una imagen de toohello de vínculo en el almacenamiento de blobs.

### <a name="add-a-device"></a>Agregar un dispositivo

Al implementar soluciones de hello preconfigurado, aprovisionar automáticamente 25 dispositivos de ejemplo que puede ver en la lista de dispositivos de Hola. Estos dispositivos son *dispositivos simulados* que se ejecutan en un WebJob de Azure. Dispositivos simulados facilitan automáticamente tooexperiment con la solución de hello preconfigurado sin Hola necesidad toodeploy real físico dispositivos. Si desea tooconnect una solución de toohello dispositivo real, vea hello [conectar su toohello de dispositivo remoto solución preconfigurada de supervisión] [ lnk-connect-rm] tutorial.

Hello pasos siguientes muestran cómo tooadd una solución de toohello dispositivo simulado:

1. Navegue toohello back-lista de dispositivos.

1. elegir un dispositivo, tooadd **+ agregar un dispositivo** en la esquina izquierda inferior de Hola.

   ![Agregar una solución de toohello preconfigurado de dispositivo][img-adddevice]

1. Elija **Agregar nuevo** en hello **dispositivo simulado** icono.

   ![Establecer nuevos detalles de los dispositivos en el panel][img-addnew]

   En toocreating de agregar un nuevo dispositivo simulado, también puede agregar un dispositivo físico si elige toocreate una **dispositivo personalizado**. toolearn más información acerca de la conexión de dispositivos físicos toohello solución, consulte [conectar su toohello dispositivo IoT Suite solución preconfigurada de supervisión remota][lnk-connect-rm].

1. Seleccione **Let me define my own Device ID** (Permitirme definir mi propio identificador de dispositivo) y escriba un nombre de identificador de dispositivo único como **mydevice_01**.

1. Seleccione **Create**.

   ![Guardar un dispositivo nuevo][img-definedevice]

1. En el paso 3 de **agregar un dispositivo simulado**, elija **realiza** lista de dispositivos de tooreturn toohello.

1. Puede ver el dispositivo **ejecutando** en la lista de dispositivos de Hola.

    ![Ver un dispositivo nuevo en la lista de dispositivos][img-runningnew]

1. También puede ver Hola simulados telemetría desde el nuevo dispositivo en el panel de hello:

    ![Ver telemetría desde el nuevo dispositivo][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a>Deshabilitar y eliminar un dispositivo

Puede deshabilitar un dispositivo y, después, quitarlo:

![Deshabilitar y quitar un dispositivo][img-disable]

### <a name="add-a-rule"></a>Agregar una regla

No hay reglas para el nuevo dispositivo de Hola que acaba de agregar. En esta sección, agregará una regla que desencadena una alarma cuando temperatura Hola Hola nuevo dispositivo supera grados 47. Antes de empezar, observe que historial de telemetría de Hola de nuevo dispositivo de hello en el panel de hello muestra la temperatura del dispositivo Hola nunca supere el 45 grados.

1. Navegue toohello back-lista de dispositivos.

1. tooadd una regla para dispositivos de hello, seleccione el nuevo dispositivo de hello **lista de dispositivos**y, a continuación, elija **Agregar regla**.

1. Crear una regla que usa **temperatura** como campo de datos de Hola y utiliza **AlarmTemp** como salida de hello cuando temperatura Hola supera 47 grados:

    ![Agregar una regla de dispositivo][img-adddevicerule]

1. los cambios, elija a toosave **guardar y ver las reglas**.

1. Elija **comandos** en panel de detalles de dispositivo de hello en dispositivo nuevo Hola.

    ![Agregar una regla de dispositivo][img-adddevicerule2]

1. Seleccione **ChangeSetPointTemp** desde la lista de comandos de Hola y establezca **SetPointTemp** too45. A continuación, elija **Enviar comando**:

    ![Agregar una regla de dispositivo][img-adddevicerule3]

1. Navegue panel toohello atrás. Después de unos minutos, verá una nueva entrada en hello **historial de alarma** panel cuando temperatura Hola notificados por el nuevo dispositivo supera el umbral de 47 grados de hello:

    ![Agregar una regla de dispositivo][img-adddevicerule4]

1. Puede revisar y editar todas las reglas en hello **reglas** página del panel de hello:

    ![Enumerar reglas de dispositivo][img-rules]

1. Puede revisar y editar todas las acciones de Hola que pueden realizarse en la regla de tooa de respuesta en hello **acciones** página del panel de hello:

    ![Enumerar acciones de dispositivo][img-actions]

> [!NOTE]
> Es toodefine posibles acciones que pueden enviar un mensaje de correo electrónico o SMS en respuesta tooa regla o integrar con un sistema de línea de negocio a través de un [aplicación lógica][lnk-logic-apps]. Para obtener más información, vea hello [tooyour de conectar la aplicación de lógica en la supervisión remota de Azure IoT conjunto preconfigurado solución][lnk-logicapptutorial].

### <a name="manage-filters"></a>Administración de filtros

En la lista de dispositivos de hello, puede crear, guardar y volver a cargar filtros toodisplay una lista personalizada de concentrador de dispositivos conectados tooyour. toocreate un filtro:

1. Elija el icono de filtro de edición de Hola por encima de la lista de Hola de dispositivos:

    ![Editor de filtros de hello abierto][img-editfiltericon]

1. Hola **editor de filtros**, agregar campos de hello, operadores y lista de dispositivos de valores toofilter Hola. Puede agregar varios toorefine cláusulas el filtro. Elija **filtro** filtro de Hola tooapply:

    ![Crear un filtro][img-filtereditor]

1. En este ejemplo, la lista de Hola se filtra por fabricante y número de modelo:

    ![Lista filtrada][img-filterelist]

1. toosave el filtro con un nombre personalizado, elija hello **Guardar como** icono:

    ![Agregar un filtro][img-savefilter]

1. tooreapply un filtro guardado previamente, elija hello **Abrir filtro guardado** icono:

    ![Abrir un filtro][img-openfilter]

Se pueden crear filtros basados en el Id. de dispositivo, estado del dispositivo, propiedades deseadas, propiedades notificadas y etiquetas. Agregar su propio dispositivo tooa de etiquetas personalizadas en hello **etiquetas** sección de hello **detalles del dispositivo** panel o ejecutar un trabajo tooupdate etiquetas en varios dispositivos.

> [!NOTE]
> Hola **editor de filtros**, puede usar hello **vista avanzada** tooedit Hola texto de la consulta directamente.

### <a name="commands"></a>Comandos:

De hello **detalles del dispositivo** panel, puede enviar el dispositivo de toohello de comandos. Cuando se inicia por primera vez un dispositivo, envía información sobre Hola comandos admite toohello solución. Para obtener una explicación de las diferencias de hello entre los comandos y métodos, consulte [opciones de centro de IoT de Azure en la nube al dispositivo][lnk-c2d-guidance].

1. Elija **comandos** en hello **detalles del dispositivo** panel del dispositivo seleccionado hello:

   ![Comandos de los dispositivos en el panel][img-devicecommands]

1. Seleccione **PingDevice** desde la lista de comandos de Hola.

1. Elija **Enviar comando**.

1. Puede ver estado de saludo del comando de Hola Hola historial de comandos.

   ![Estado de los comandos en el panel][img-pingcommand]

solución de Hello realiza un seguimiento de estado Hola de cada comando que envía. Inicialmente es el resultado de hello **pendiente**. Cuando el dispositivo de hello informa de que se ha ejecutado el comando hello, del conjunto de resultados de hello es demasiado**correcto**.

## <a name="behind-hello-scenes"></a>Entre bastidores de Hola

Al implementar una solución preconfigurada, el proceso de implementación de hello crea varios recursos en hello Azure suscripción que ha seleccionado. Puede ver estos recursos en hello Azure [portal][lnk-portal]. proceso de implementación de Hello crea un **grupo de recursos** con un nombre basado en el nombre de Hola que elija para su solución preconfigurada:

![Solución preconfigurada en hello portal de Azure][img-portal]

Puede ver configuración de Hola de cada recurso mediante su selección en la lista de Hola de recursos de grupo de recursos de Hola.

También puede ver el código fuente de hello para la solución de hello preconfigurado. Hola código fuente de solución preconfigurada de supervisión remota está en hello [-iot-remoto-supervisión de azure] [ lnk-rmgithub] repositorio de GitHub:

* Hola **DeviceAdministration** carpeta contiene el código de origen de hello para el panel de Hola.
* Hola **simulador** carpeta contiene código de fuente de hello de dispositivo simulado Hola.
* Hola **EventProcessor** carpeta contiene el código de origen de Hola para procesos de back-end de Hola que controla la telemetría de Hola entrantes.

Cuando haya terminado, puede eliminar solución Hola preconfigurado de su suscripción de Azure en hello [azureiotsuite.com] [ lnk-azureiotsuite] sitio. Este sitio le permite eliminar tooeasily que todos Hola recursos que estaban aprovisionados al crear soluciones de hello preconfigurado.

> [!NOTE]
> tooensure eliminar todos los elementos relacionados con la solución toohello preconfigurado, eliminarlo de hello [azureiotsuite.com] [ lnk-azureiotsuite] de sitio y no se elimine el grupo de recursos de hello en el portal de Hola.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha implementado una solución de trabajo configurado preconfigurada, puede seguir introducción con Suite IoT leyendo Hola siguientes artículos:

* [Tutorial de la solución preconfigurada de supervisión remota][lnk-rm-walkthrough]
* [Conectar su toohello de dispositivo remoto solución preconfigurada de supervisión][lnk-connect-rm]
* [Permisos en el sitio de hello azureiotsuite.com][lnk-permissions]

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md