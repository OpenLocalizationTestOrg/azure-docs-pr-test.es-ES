---
title: "los extremos REST de aaaCall con HTTP + Swagger conector para las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Conectar los extremos de tooREST de lógica de aplicaciones a través de Swagger con Hola HTTP + conector de Swagger"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a>Empezar a trabajar con Hola HTTP + acción de Swagger

Puede crear un extremo REST de primera clase conector tooany a través de un [Swagger documento](https://swagger.io) cuando usas Hola HTTP + Swagger acción en el flujo de trabajo de aplicación lógica. También puede extender lógica aplicaciones toocall cualquier extremo REST con una experiencia de diseñador de la aplicación lógica de primera clase.

toolearn cómo toocreate las aplicaciones lógicas con conectores, consulte [crear una nueva aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a>Uso de HTTP + Swagger como desencadenador o acción

Hola HTTP + Swagger desencadenador y la acción del trabajo mismo Hola como hello [acción HTTP](connectors-native-http.md) pero ofrecer una mejor experiencia de diseñador de la aplicación lógica mediante la exposición de la estructura de la API de Hola y salidas de hello [Swagger metadatos](https://swagger.io) . También puede utilizar Hola HTTP + Swagger conector como un desencadenador. Si desea que un desencadenador de sondeo tooimplement, siguen el patrón de sondeo de Hola que se describe en [crear personalizado toocall API otras API, servicios y sistemas de aplicaciones de lógica de](../logic-apps/logic-apps-create-api-app.md#polling-triggers).

Más información sobre [las acciones y los desencadenadores de aplicaciones lógicas](connectors-overview.md).

Este es un ejemplo de cómo toouse Hola HTTP + Swagger operación como una acción en un flujo de trabajo en una aplicación de lógica.

1. Seleccione hello **nuevo paso** botón.
2. Seleccione **Add an action**(Agregar una acción).
3. En el cuadro de búsqueda de la acción de hello, escriba **swagger** toolist Hola HTTP + Swagger acción.
   
    ![Acción de selección de HTTP + Swagger](./media/connectors-native-http-swagger/using-action-1.png)
4. Escriba la dirección URL de Hola para un documento de Swagger:
   
   * toowork de hello Diseñador de la lógica de aplicaciones, Hola URL debe ser un extremo HTTPS y ha habilitado CORS.
   * Si el documento de Swagger de hello no cumple este requisito, puede usar [con CORS habilita el almacenamiento de Azure](#hosting-swagger-from-storage) documento de hello toostore.
5. Haga clic en **siguiente** tooread y presentación de Hola Swagger documento.
6. Agregue todos los parámetros que son necesarios para la llamada de hello HTTP.
   
    ![Completar acción HTTP](./media/connectors-native-http-swagger/using-action-2.png)
7. toosave y publicar la aplicación lógica, haga clic en **guardar** en la barra de herramientas del diseñador.

### <a name="host-swagger-from-azure-storage"></a>Hospedar Swagger desde Azure Storage
Puede ser conveniente tooreference un documento de Swagger que no se hospeda o que no cumple los requisitos de seguridad y entre orígenes de hello para el Diseñador de Hola. tooresolve este problema, puede almacenar documentos de Swagger de hello en el almacenamiento de Azure y habilitar CORS tooreference Hola documentos.  

Presentamos Hola pasos toocreate, configurar y almacenar documentos de Swagger en el almacenamiento de Azure:

1. [Crear una cuenta de Azure Storage con Azure Blob Storage](../storage/common/storage-create-storage-account.md). tooperform este paso, establecer permisos demasiado**acceso público**.

2. Habilitar CORS en blob Hola. 

   tooautomatically esta configuración, puede usar [esta secuencia de comandos de PowerShell](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).

3. Cargar blob de hello Swagger archivos toohello. 

   Puede realizar este paso de hello [portal de Azure](https://portal.azure.com) o desde una herramienta como [Azure Storage Explorer](http://storageexplorer.com/).

4. Hacer referencia a un documento de toohello vínculo HTTPS en almacenamiento de blobs de Azure. 

   vínculo de Hello utiliza este formato:

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a>Detalles técnicos
Siguientes son los detalles de Hola de hello desencadenadores y acciones que este HTTP + Swagger conector es compatible con.

## <a name="http--swagger-triggers"></a>Desencadenadores HTTP + Swagger
Un desencadenador es un evento que puede ser el flujo de trabajo hello toostart utilizado que se define en una aplicación de lógica. [Más información sobre los desencadenadores.](connectors-overview.md) Hola HTTP + Swagger conector tiene un desencadenador.

| Desencadenador | Description |
| --- | --- |
| HTTP + Swagger |Realizar una llamada HTTP y devolver el contenido de la respuesta de Hola |

## <a name="http--swagger-actions"></a>Acciones HTTP + Swagger
Una acción es una operación que se lleva a cabo por flujo de trabajo de Hola que se define en una aplicación de lógica. [Más información acerca de las acciones.](connectors-overview.md) Hola HTTP + Swagger conector tiene una acción posible.

| Acción | Description |
| --- | --- |
| HTTP + Swagger |Realizar una llamada HTTP y devolver el contenido de la respuesta de Hola |

### <a name="action-details"></a>Detalles de la acción
Hola HTTP + Swagger conector viene con una acción posible. A continuación encontrará información sobre cada una de las acciones de Hola, hello correspondiente detalles de salida que están asociados a su uso y sus campos de entrada obligatorios y opcionales.

#### <a name="http--swagger"></a>HTTP + Swagger
Realice una solicitud HTTP saliente con ayuda de los metadatos de Swagger.
Un asterisco (*) significa un campo obligatorio.

| Nombre para mostrar | Nombre de propiedad | Description |
| --- | --- | --- |
| Método* |estático |Toouse de verbo HTTP. |
| URI* |uri |URI de solicitud de hello HTTP. |
| Encabezados |encabezados |Un objeto JSON de tooinclude de encabezados HTTP. |
| Cuerpo |body |Hola cuerpo de solicitud HTTP. |
| Autenticación |Autenticación |Toouse de autenticación para la solicitud. Para obtener más información, vea hello [conector HTTP](connectors-native-http.md#authentication). |

**Detalles de salida**

Respuesta HTTP

| Nombre de propiedad | Tipo de datos | Description |
| --- | --- | --- |
| encabezados |objeto |Encabezados de respuesta |
| Cuerpo |objeto |Objeto de respuesta |
| Código de estado |int |Código de estado HTTP |

### <a name="http-responses"></a>Respuestas HTTP
Al realizar llamadas toovarious acciones, podría obtener determinadas respuestas. A continuación se incluye una tabla que describe las respuestas y descripciones correspondientes.

| Nombre | Descripción |
| --- | --- |
| 200 |OK |
| 202 |Accepted |
| 400 |Solicitud incorrecta |
| 401 |No autorizado |
| 403 |Prohibido |
| 404 |No encontrado |
| 500 |Error interno del servidor Error desconocido. |

- - -
## <a name="next-steps"></a>Pasos siguientes

* [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md)
* [Buscar otros conectores](apis-list.md)