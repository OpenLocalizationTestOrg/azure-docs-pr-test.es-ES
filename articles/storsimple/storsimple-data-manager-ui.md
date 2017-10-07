---
title: aaaMicrosoft Azure StorSimple UI de Data Manager | Documentos de Microsoft
description: "Describe cómo toouse servicio (vista previa privada) de la interfaz de usuario de administrador de datos de StorSimple"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b0ee12b3e495400b54e48eb1a98c68b1af2e5f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-using-hello-storsimple-data-manager-service-ui-private-preview"></a>Administrar mediante el servicio de datos de StorSimple Manager de hello (Private Preview) de la interfaz de usuario

Este artículo explica cómo puede usar Hola transformación de datos de administrador de datos de StorSimple UI tooperform en datos que residen en dispositivos de la serie StorSimple 8000 Hola. Hello datos transformados pueden, a continuación, utilizarse otros servicios de Azure, como los servicios multimedia de Azure, HDInsight de Azure, aprendizaje automático de Azure y búsqueda de Azure. 


## <a name="use-storsimple-data-transformation"></a>Uso de transformación de datos de StorSimple

Hola, Administrador de datos de StorSimple es recursos Hola dentro del cual se pueden crear instancias de transformación de datos. Hola servicios de transformación de datos permite mover los datos de su tooblobs de dispositivo de StorSimple local en el almacenamiento de Azure. Por tanto, en el flujo de trabajo deberá detalles de hello toospecify sobre los datos de hello y el dispositivo de StorSimple de interés que desea que la cuenta de almacenamiento de toomove toohello.

### <a name="create-a-storsimple-data-manager-service"></a>Creación de un servicio StorSimple Data Manager

Realizar Hola siguiendo los pasos toocreate un servicio de administrador de datos de StorSimple.

1. toocreate un servicio de datos de StorSimple Manager, vaya demasiado[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)

2. Haga clic en hello  **+**  icono y búsqueda para el Administrador de datos de StorSimple. Haga clic en el servicio StorSimple Data Manager y, después, en **Create** (Crear).

3. Si la suscripción está habilitada para la creación de este servicio, vea Hola después de hoja.

    ![Creación de un recurso de StorSimple Data Manager](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. Escriba las entradas de Hola y haga clic en **crear**. Hola especifica la ubicación debe ser Hola uno que contiene las cuentas de almacenamiento y el servicio StorSimple Manager. Actualmente, solo se admiten las regiones oeste de EE. UU. y Europa occidental. Por lo tanto, el servicio StorSimple Manager, el servicio de administrador de datos y el Hola asociado cuenta de almacenamiento deben estar todos en regiones de hello anterior compatible. Se tarda aproximadamente un servicio de hello toocreate minutos.

### <a name="create-a-data-transformation-job-definition"></a>Creación de una definición del trabajo de transformación de datos

Dentro de un servicio de datos de StorSimple Manager, deberá toocreate una definición de trabajo de transformación de datos. Una definición de trabajo especifica los detalles de los datos de Hola que esté interesado en mover a una cuenta de almacenamiento en formato nativo de Hola. 

Realizar Hola siguiendo los pasos toocreate una nueva definición de trabajo de transformación de datos.

1.  Navegue servicio toohello que ha creado. Haga clic en **+ Job Definition** (+ Definición de trabajo).

    ![Haga clic en + Job Definition (+ Definición de trabajo)](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. nueva hoja de definición de trabajo Hola se abre. Asigne un nombre a la definición de trabajo y haga clic en **Origen**. Hola **Configurar origen de datos** hoja, especifique los detalles de hello del dispositivo StorSimple y Hola datos de interés.

    ![Creación de una definición de trabajo](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. Al ser un servicio Data Manager nuevo, no se configuran repositorios de datos. tooadd el StorSimple Manager como un repositorio de datos, haga clic en ejecutar **agregar nueva** en Hola lista desplegable del repositorio de datos y, a continuación, haga clic en **Agregar repositorio de datos**.

4. Elija **serie 8000 de StorSimple Manager** como repositorio de hello escriba y especifique las propiedades de Hola de su **StorSimple Manager**. Para hello **Id. de recurso** campo, necesita tooenter Hola número antes de hello **:** en la clave de registro de hello del Administrador de StorSimple.

    ![Creación de un origen de datos](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  Pulse **OK** (Aceptar) cuando haya terminado. Esto guarda el repositorio de datos y StorSimple Manager se pueden reutilizar en otras definiciones de trabajo sin tener que volver a escribir estos parámetros. Tarda unos segundos después de hacer clic en **Aceptar** para hello tooshow de StorSimple Manager seguridad en la lista desplegable de Hola.

6.  Hola **Configurar origen de datos** hoja, escriba el nombre del dispositivo de Hola y Hola nombre del volumen que tiene los datos de interés.

7.  Hola **filtro** subsección, escriba el directorio raíz de Hola que contiene los datos de interés (este campo debe empezar por un `\`). Aquí también se pueden agregar los filtros de archivo.

8.  Servicios de transformación de datos de Hello funciona en los datos de Hola que se insertan una toohello Azure a través de las instantáneas. Cuando se ejecuta este trabajo, puede elegir tootake una copia de seguridad cada vez que se ejecuta este trabajo (toowork en los datos más recientes) o toouse Hola última copia de seguridad existente en la nube de hello (si está trabajando en algunos de los datos archivados).

    ![Detalles del origen de datos nuevo](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. A continuación, es necesario la configuración de destino de hello toobe configurado. Se admiten dos 2 tipos de destinos: cuentas de Azure Storage y cuentas de Azure Media Services. Elija las cuentas de almacenamiento tooput archivos en blobs en esa cuenta. Elegir cuenta de servicios multimedia tooput archivos en activos de esa cuenta. Una vez más, necesitamos tooadd un repositorio. En la lista desplegable de hello, seleccione **agregar nueva** y, a continuación, **configurar**.

    ![Crear el receptor de datos](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. En este caso, puede seleccionar tipo de hello del repositorio que desee hello y tooadd otros parámetros asociados con el repositorio de Hola. En ambos casos, una cola de almacenamiento se crea cuando se ejecuta el trabajo de Hola. Esta cola se rellena con mensajes de los blobs transformados a medida que están listos. nombre de Hola de esta cola es Hola igual que el nombre de Hola Hola de definición de trabajo. Si selecciona **servicios multimedia** como tipo de repositorio de hello, a continuación, también puede especificar las credenciales de cuenta de almacenamiento donde se crea la cola de Hola.

    ![Detalles del receptor de datos nuevo](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. Después de Agregar repositorio de datos de hello (que tarda unos segundos), encontrará repositorio hello en la lista desplegable de hello en hello **nombre de la cuenta de destino**.  Elegir destino de Hola que necesita.

12. Haga clic en **Aceptar** definición del trabajo toocreate Hola. La definición de trabajo ya está configurada. Puede utilizar esta definición de trabajo varias veces a través de hello interfaz de usuario.

    ![Agregar una definición de trabajo nueva](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-hello-job-definition"></a>Ejecutar la definición del trabajo Hola

Siempre que tenga datos de toomove de StorSimple toohello cuenta de almacenamiento que ha especificado en la definición del trabajo hello, necesitará tooinvoke lo. Hay cierta flexibilidad para cambiar los parámetros de hello cada vez que se invoca el trabajo de Hola. pasos de Hello son los siguientes:

1. Seleccione el servicio de datos de StorSimple Manager y vaya demasiado**supervisión**. Haga clic en **Run now** (Ejecutar ahora).

    ![Desencadenar la definición de trabajo](./media/storsimple-data-manager-ui/run-now.png)

2. Elija la definición del trabajo de Hola que desea toorun. Haga clic en **los parámetros de ejecución** toomodify cualquier configuración que podría desear toochange para esta ejecución del trabajo.

    ![Ejecutar configuración de trabajo](./media/storsimple-data-manager-ui/run-settings.png)

3. Haga clic en **Aceptar** y, a continuación, haga clic en **ejecutar** toolaunch su trabajo. toomonitor este trabajo, vaya toohello **trabajos** página en el Administrador de datos de StorSimple.

    ![Lista y estado de los trabajos](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. En suma toomonitoring Hola **trabajos** hoja, también puede escuchar en cola de almacenamiento de Hola dónde se agrega un mensaje cada vez que se mueve un archivo de cuenta de almacenamiento de StorSimple toohello.


## <a name="next-steps"></a>Pasos siguientes

[Utilice trabajos de administrador de StorSimple de datos de .NET SDK toolaunch](storsimple-data-manager-dotnet-jobs.md).
