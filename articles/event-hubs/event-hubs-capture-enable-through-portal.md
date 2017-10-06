---
title: "Habilitar aaaAzure captura de los centros de eventos a través del portal | Documentos de Microsoft"
description: "Habilitar característica de captura de los centros de eventos de hello mediante Hola portal de Azure."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a>Habilitar la captura de los centros de eventos mediante Hola portal de Azure

Puede configurar la captura en tiempo de creación de base de datos central Hola eventos con hello [portal de Azure](https://portal.azure.com). Puede cualquier tooan de datos de captura hello Azure [almacenamiento de blobs](https://azure.microsoft.com/services/storage/blobs/) contenedor o tooan [almacén de Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) cuenta.

## <a name="capture-data-tooan-azure-storage-account"></a>Cuenta de almacenamiento de Azure de datos tooan de captura  

Cuando se crea un centro de eventos, puede habilitar la captura, haga clic en hello **en** botón en hello **crear centro de eventos** portal hoja. A continuación, especifique una cuenta de almacenamiento y el contenedor, haga clic en **el almacenamiento de Azure** en hello **proveedor capturar** cuadro. Como capturar de concentradores de eventos utiliza la autenticación de servicio al servicio con el almacenamiento, no es necesario toospecify una cadena de conexión de almacenamiento. Selector de recursos de Hello seleccionará automáticamente el recurso de hello URI para la cuenta de almacenamiento. Si se usa Azure Resource Manager, es preciso suministrar explícitamente dicho identificador URI como una cadena.

período de tiempo de saludo predeterminado es 5 minutos. valor mínimo de Hello es 1, Hola máximo 15. Hola **tamaño** ventana tiene un intervalo de 10-500 MB.

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a>Cuenta de almacén de Azure Data Lake tooan de datos de captura

toocapture datos tooAzure almacén de Data Lake, cree una cuenta de almacén de Data Lake y un concentrador de eventos:

### <a name="create-an-azure-data-lake-store-account-and-folders"></a>Creación de una cuenta de Azure Data Lake Store y de carpetas

1. Crear una cuenta de almacén de Data Lake, siga las instrucciones de hello en [empezar a trabajar con el almacén de Data Lake de Azure mediante el portal de Azure de hello](../data-lake-store/data-lake-store-get-started-portal.md). 
2. Cree una carpeta en esta cuenta, siga las instrucciones de Hola Hola [crear carpetas en la cuenta de almacén de Azure Data Lake](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) sección.
3. En la hoja de la cuenta de almacén de Data Lake de hello, haga clic en **Explorador de datos**.
4. Haga clic en **Acceder**.
5. Haga clic en **Agregar**.
6. Hola **buscar por nombre o correo electrónico** cuadro, escriba **Microsoft.EventHubs** y, a continuación, seleccione esta opción. 
7. Hola **permisos** ficha aparece. Establecer permisos de hello tal y como se muestra en hello figura siguiente:

    ![][6]

8. Haga clic en **Aceptar**.
9. Ahora, cree una carpeta en la carpeta raíz de hello examinando toohello la carpeta de destino y haga clic en el nombre de la carpeta de Hola.
10. Haga clic en **Acceder**.
11. Haga clic en **Agregar**.
12. Hola **buscar por nombre o correo electrónico** cuadro, escriba **Microsoft.EventHubs** y, a continuación, seleccione esta opción.
13. Hola **permisos** ficha aparece de nuevo. Establecer permisos de hello tal y como se muestra en hello figura siguiente:

    ![][5]

### <a name="create-an-event-hub"></a>Creación de un centro de eventos

1. Tenga en cuenta debe ser ese centro de eventos de Hola Hola misma suscripción de Azure como Hola almacén de Data Lake de Azure que acaba de crear. Centro de eventos de Hola de crear, haga clic en hello **en** situado bajo **capturar** en hello **crear centro de eventos** portal hoja. 
2. Hola **crear centro de eventos** portal hoja, seleccione **almacén de Azure Data Lake** de hello **proveedor capturar** cuadro.
3. En **seleccione almacén de Data Lake**, especifique la cuenta de almacén de Data Lake que creó anteriormente y Hola Hola **ruta de acceso de datos Lake** , escriba la carpeta de datos de toohello Hola ruta de acceso que ha creado.

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a>Adición o configuración de Capture en un centro de eventos existente

Se puede configurar Capture en los centros de eventos existentes que se encuentran en los espacios de nombres de Event Hubs. tooenable capturar en un centro de eventos existente, o toochange la configuración de captura, haga clic en Hola Hola de tooload de espacio de nombres **Essentials** blade, a continuación, haga clic en Centro de eventos de hello para el que desea tooenable o cambiar la configuración de captura de Hola. Por último, haga clic en hello **propiedades** sección de hello Abrir hoja y, a continuación, editar la configuración de captura de hello, como se muestra en hello siguientes ilustraciones:

### <a name="azure-blob-storage"></a>Almacenamiento de blobs de Azure

![][2]

### <a name="azure-data-lake-store"></a>Almacén de Azure Data Lake

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a>Pasos siguientes

La Event Hubs Capture también se puede configurar a través de las plantillas de Azure Resource Manager. Para más información, consulte [Habilitar Capture mediante la plantilla de Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).
