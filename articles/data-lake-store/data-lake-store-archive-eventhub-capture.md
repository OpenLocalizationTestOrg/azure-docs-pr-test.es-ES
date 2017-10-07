---
title: "aaaCapture datos desde los centros de eventos en el almacén de Azure Data Lake | Documentos de Microsoft"
description: "Datos de toocapture de almacén de Azure Data Lake de uso de los centros de eventos"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a>Datos de toocapture de almacén de Azure Data Lake de uso de los centros de eventos

Obtenga información acerca de cómo toouse datos de almacén de Azure Data Lake toocapture recibido por centros de eventos de Azure.

## <a name="prerequisites"></a>Requisitos previos

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Una cuenta de Almacén de Azure Data Lake**. Para obtener instrucciones sobre cómo toocreate un, consulte [empezar a trabajar con el almacén de Azure Data Lake](data-lake-store-get-started-portal.md).

*  **Un espacio de nombres de Event Hubs**. Para obtener instrucciones, consulte [Creación de un espacio de nombres de Event Hubs](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace). Asegurarse de que cuenta de almacén de Data Lake hello y espacio de nombres de los centros de eventos de Hola Hola misma suscripción de Azure.


## <a name="assign-permissions-tooevent-hubs"></a>Asignar permisos de los centros de tooEvent

En esta sección, creará una carpeta dentro de la cuenta de hello donde desea toocapture Hola datos desde los centros de eventos. También asigna permisos tooEvent concentradores para que pueden escribir datos en una cuenta de almacén de Data Lake. 

1. Abrir cuenta de almacén de Data Lake Hola donde desea que los datos de toocapture los centros de eventos y, a continuación, haga clic en **Explorador de datos**.

    ![Explorador de datos de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Explorador de datos de Data Lake Store")

2.  Haga clic en **nueva carpeta** y, a continuación, escriba un nombre para la carpeta donde desea que los datos de hello toocapture.

    ![Crear una carpeta en Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Crear una carpeta en Data Lake Store")

3. Asignar permisos en la raíz de Hola de hello almacén de Data Lake. 

    a. Haga clic en **Explorador de datos**, seleccione raíz Hola Hola cuenta de almacén de Data Lake y, a continuación, haga clic en **acceso**.

    ![Asignar permisos a la raíz de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Asignar permisos a la raíz de Data Lake Store")

    b. En **Acceso**, haga clic en **Agregar**, en **Seleccionar usuario o grupo** y después busque `Microsoft.EventHubs`. 

    ![Asignar permisos a la raíz de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Asignar permisos a la raíz de Data Lake Store")
    
    Haga clic en **Seleccionar**.

    c. En **Asignar permisos**, haga clic en **Seleccionar permisos**. Establecer **permisos** demasiado**Execute**. Establecer **agregar a** demasiado**esta carpeta y todos los elementos secundarios**. Establecer **agregar como** demasiado**una entrada de permiso de acceso y una entrada de permiso predeterminado**.

    ![Asignar permisos a la raíz de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Asignar permisos a la raíz de Data Lake Store")

    Haga clic en **Aceptar**.

4. Asignar permisos para las carpetas de hello en la cuenta de almacén de Data Lake donde desea toocapture datos.

    a. Haga clic en **Explorador de datos**, seleccione la carpeta de Hola Hola cuenta de almacén de Data Lake y, a continuación, haga clic en **acceso**.

    ![Asignar permisos a la carpeta de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Asignar permisos a la carpeta de Data Lake Store")

    b. En **Acceso**, haga clic en **Agregar**, en **Seleccionar usuario o grupo** y después busque `Microsoft.EventHubs`. 

    ![Asignar permisos a la carpeta de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Asignar permisos a la carpeta de Data Lake Store")
    
    Haga clic en **Seleccionar**.

    c. En **Asignar permisos**, haga clic en **Seleccionar permisos**. Establecer **permisos** demasiado**lectura, escritura,** y **Execute**. Establecer **agregar a** demasiado**esta carpeta y todos los elementos secundarios**. Por último, establezca **agregar como** demasiado**una entrada de permiso de acceso y una entrada de permiso predeterminado**.

    ![Asignar permisos a la carpeta de Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Asignar permisos a la carpeta de Data Lake Store")
    
    Haga clic en **Aceptar**. 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a>Configurar almacén de los centros de eventos toocapture data tooData Lake

En esta sección, creará un centro de eventos en un espacio de nombres de Event Hubs. También configurará Hola concentrador de eventos toocapture datos tooan cuenta de almacén de Azure Data Lake. En esta sección, se da por supuesto que ya ha creado un espacio de nombres de Event Hubs.

2. De hello **Introducción** de espacio de nombres de los centros de eventos de hello, haga clic en **+ concentrador de eventos**.

    ![Crear centro de eventos](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Crear centro de eventos")

3. Proporcione la siguiente Hola valores tooconfigure centros de eventos toocapture datos tooData Lake almacén.

    ![Crear centro de eventos](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Crear centro de eventos")

    a. Proporcione un nombre para hello concentrador de eventos.
    
    b. Para este tutorial, establezca **recuento de particiones** y **retención de mensajes** valores predeterminados de toohello.
    
    c. Establecer **capturar** demasiado**en**. Conjunto hello **período de tiempo** (con qué frecuencia toocapture) y **ventana de tamaño** (toocapture de tamaño de datos). 
    
    d. Para **proveedor capturar**, seleccione **almacén de Azure Data Lake** y seleccione Hola Hola almacén de Data Lake que creó anteriormente. Para **ruta de acceso de datos Lake**, escriba el nombre de Hola de carpeta de Hola que creó en hello cuenta de almacén de Data Lake. Solo se necesita carpeta de toohello de tooprovide Hola ruta de acceso relativa.

    e. Deje hello **formatos de nombre de archivo de ejemplo captura** valor predeterminado de toohello. Esta opción rige la estructura de carpetas de Hola que se crea en la carpeta de captura de Hola.

    f. Haga clic en **Crear**.

## <a name="test-hello-setup"></a>Programa de instalación de prueba Hola

Ahora puede probar la solución de hello enviando datos toohello concentrador de eventos de Azure. Siga las instrucciones de hello en [enviar eventos centros de eventos de tooAzure](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md). Una vez que empezar a enviar datos de hello, verá datos Hola reflejados en el almacén de Data Lake con la estructura de carpetas de Hola que especificó. Por ejemplo, verá una estructura de carpetas tal y como se muestra en la siguiente captura de pantalla, en el almacén de Data Lake de Hola.

![Datos de ejemplo del centro de eventos en Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Datos de ejemplo del centro de eventos en Data Lake Store")

> [!NOTE]
> Incluso si no tiene mensajes que entran en los centros de eventos, los concentradores de eventos escribe archivos vacíos con solo a los encabezados hello en hello cuenta de almacén de Data Lake. Hello archivos se escriben en hello mismo intervalo de tiempo que haya especificado durante la creación de centros de eventos de Hola.
> 
>

## <a name="analyze-data-in-data-lake-store"></a>Análisis de datos en el Almacén de Data Lake

Una vez en el almacén de Data Lake datos hello, puede ejecutar trabajos analíticos tooprocess y delicadas datos Hola. Vea [USQL Avro ejemplo](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) acerca de cómo toodo este mediante el análisis de Data Lake de Azure.
  

## <a name="see-also"></a>Otras referencias
* [Protección de los datos en el Almacén de Data Lake](data-lake-store-secure-data.md)
* [Copiar los datos de almacén de Blobs de Azure almacenamiento Lake tooData](data-lake-store-copy-data-azure-storage-blob.md)
