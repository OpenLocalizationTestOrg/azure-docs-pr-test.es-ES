---
title: "Hola aaaAdd conector en las aplicaciones lógicas de almacenamiento de blobs de Azure | Documentos de Microsoft"
description: "Empezar a trabajar y configurar el conector de almacenamiento de blobs de Azure de hello en una aplicación de lógica"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a>Usar el conector de almacenamiento de blobs de Azure de hello en una aplicación de lógica
Tooupload de conector de almacenamiento de blobs de Azure de uso hello, actualizar, obtener y eliminar los blobs en la cuenta de almacenamiento, todo dentro de una aplicación de lógica.  

Con Almacenamiento de blobs de Azure:

* Cree un flujo de trabajo cargando nuevos proyectos u obteniendo archivos recientemente actualizados.
* Use acciones tooget metadatos de archivo, eliminar un archivo, copia archivos y mucho más. Por ejemplo, cuando se actualiza una herramienta en un sitio web de Azure (desencadenador), se actualiza un archivo en Blob Storage (acción). 

Este tema muestra cómo toouse Hola blob conector de almacenamiento en una aplicación de lógica.

toolearn más información acerca de las aplicaciones lógicas, consulte [¿cuáles son las aplicaciones lógicas](../logic-apps/logic-apps-what-are-logic-apps.md) y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).

toolearn más información acerca de las aplicaciones lógicas, consulte [¿cuáles son las aplicaciones lógicas](../logic-apps/logic-apps-what-are-logic-apps.md) y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooazure-blob-storage"></a>Conectar el almacenamiento de blobs de tooAzure
Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero cree un *conexión* toohello servicio. Una conexión proporciona conectividad entre una aplicación lógica y otro servicio. Por ejemplo, cuenta de almacenamiento de tooconnect tooa, crea primero un almacenamiento de blobs *conexión*. toocreate una conexión, escriba las credenciales de Hola que suele usar el servicio de hello tooaccess se conecta a. Por lo que con el almacenamiento de Azure, escriba conexión de hello credenciales tooyour almacenamiento cuenta toocreate Hola. 

#### <a name="create-hello-connection"></a>Crear conexiones de Hola
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a>Uso de un desencadenador
Este conector no tiene ningún desencadenador. Utilice otra aplicación de lógica de desencadenadores toostart hello, como un desencadenador de periodicidad, un desencadenador de HTTP Webhook, desencadenadores disponibles con otros conectores y mucho más. En [Creación de una nueva aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md) se puede ver un ejemplo.

## <a name="use-an-action"></a>Uso de una acción
Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola.

1. Seleccione el signo más Hola. Vea elegir entre varias opciones: **agregar una acción**, **agregar una condición**, o uno de hello **más** opciones.
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. Elija **Add an action**(Agregar una acción).
3. En el cuadro de texto hello, escriba "blob" tooget una lista de todas las acciones disponibles Hola.
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. En nuestro ejemplo, elija **AzureBlob - Obtener metadatos de archivo mediante la ruta de acceso**. Si ya existe una conexión, a continuación, seleccione hello **...** (Mostrar selector) botón tooselect un archivo.
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    Si se le solicitará información de conexión de hello, a continuación, escriba la conexión de hello detalles toocreate Hola. [Crear conexiones de hello](connectors-create-api-azureblobstorage.md#create-the-connection) en este tema se describen estas propiedades. 
   
   > [!NOTE]
   > En este ejemplo, obtenemos Hola metadatos de un archivo. toosee Hola metadatos, agregue otra acción que crea un archivo nuevo con otro conector. Por ejemplo, agregar una acción de OneDrive que crea un nuevo archivo "test" basándose en los metadatos de Hola. 


5. **Guardar** los cambios (esquina superior izquierda de la barra de herramientas de hello). La aplicación lógica se guarda y se puede habilitar automáticamente.

> [!TIP]
> [Explorador de almacenamiento](http://storageexplorer.com/) es una herramienta excelente demasiado administrar varias cuentas de almacenamiento.

## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/azureblobconnector/). 

## <a name="next-steps"></a>Pasos siguientes
[Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md). Explorar Hola otros conectores disponibles en las aplicaciones lógicas en nuestro [lista de las API](apis-list.md).

