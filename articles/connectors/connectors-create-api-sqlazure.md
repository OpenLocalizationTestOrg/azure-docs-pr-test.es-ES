---
title: "Conector de base de datos de SQL Azure de hello aaaAdd en las aplicaciones lógicas | Documentos de Microsoft"
description: "Información general sobre el conector de Base de datos SQL de Azure con los parámetros de la API de REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a9ca0f446d05dc00f310a908eee8d50e41fcd82b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-sql-database-connector"></a>Empezar a trabajar con el conector de base de datos de SQL Azure Hola
Mediante el conector de base de datos de SQL Azure de hello, crear flujos de trabajo para su organización que administran datos de las tablas. 

Con Base de datos SQL:

* Compilar el flujo de trabajo mediante la adición de una base de datos de los clientes de tooa cliente nuevo o actualizar un pedido en una base de datos de pedidos.
* Usar acciones tooget una fila de datos, insertar una fila nueva e incluso eliminar. Por ejemplo, al crear un registro en Dynamics CRM Online (desencadenador), inserte una fila en una base de datos SQL de Azure (acción). 

Este tema muestra cómo toouse Hola conector de base de datos SQL en una aplicación de lógica, y también listas Hola acciones.

toolearn más información acerca de las aplicaciones lógicas, consulte [¿cuáles son las aplicaciones lógicas](../logic-apps/logic-apps-what-are-logic-apps.md) y [crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooazure-sql-database"></a>Conectar tooAzure base de datos SQL
Antes de que la aplicación lógica puede tener acceso a cualquier servicio, primero cree un *conexión* toohello servicio. Una conexión proporciona conectividad entre una aplicación lógica y otro servicio. Por ejemplo, tooconnect tooSQL base de datos, en primer lugar crear una base de datos de SQL *conexión*. toocreate una conexión, escriba las credenciales de Hola que suele usar el servicio de hello tooaccess a que se conecta. Por lo tanto, en la base de datos de SQL, escriba la conexión de base de datos SQL credenciales toocreate Hola. 

#### <a name="create-hello-connection"></a>Crear conexiones de Hola
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a>Uso de un desencadenador
Este conector no tiene ningún desencadenador. Utilice otra aplicación de lógica de desencadenadores toostart hello, como un desencadenador de periodicidad, un desencadenador de HTTP Webhook, desencadenadores disponibles con otros conectores y mucho más. En [Creación de una nueva aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md) se puede ver un ejemplo.

## <a name="use-an-action"></a>Uso de una acción
Una acción es una operación que se llevan a cabo definidos en una aplicación de la lógica de flujo de trabajo de Hola. [Más información acerca de las acciones](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Seleccione el signo más Hola. Vea elegir entre varias opciones: **agregar una acción**, **agregar una condición**, o uno de hello **más** opciones.
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. Elija **Add an action**(Agregar una acción).
3. En el cuadro de texto hello, escriba "sql" tooget una lista de todas las acciones disponibles Hola.
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. En nuestro ejemplo, elija **SQL Server - Obtener fila**. Si ya existe una conexión, a continuación, seleccione hello **nombre de la tabla** en Hola de lista desplegable lista y escriba hello **identificador de fila** desea tooreturn.
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    Si se le solicitará información de conexión de hello, a continuación, escriba la conexión de hello detalles toocreate Hola. [Crear conexiones de hello](connectors-create-api-sqlazure.md#create-the-connection) en este tema se describen estas propiedades. 
   
   > [!NOTE]
   > En este ejemplo, devolvemos una fila de una tabla. datos de hello toosee en esta fila, agregue otra acción que crea un archivo mediante los campos de Hola de tabla de Hola. Por ejemplo, agregar una acción de OneDrive que usa hello, FirstName y LastName campos toocreate un archivo nuevo en la cuenta de almacenamiento de hello en la nube. 
   > 
   > 
5. **Guardar** los cambios (esquina superior izquierda de la barra de herramientas de hello). La aplicación lógica se guarda y se puede habilitar automáticamente.

## <a name="connector-specific-details"></a>Detalles específicos del conector

Ver los desencadenadores y las acciones definidas en swagger hello y también los límites de hello [detalles del conector](/connectors/sql/). 

## <a name="next-steps"></a>Pasos siguientes
[Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md). Explorar Hola otros conectores disponibles en las aplicaciones lógicas en nuestro [lista de las API](apis-list.md).

