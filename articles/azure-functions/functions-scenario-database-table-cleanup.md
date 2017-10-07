---
title: aaaUse funciones de Azure tooperform una base de datos limpiar tarea | Documentos de Microsoft
description: Use las funciones de Azure tooschedule una tarea que se conecta tooAzure tooperiodically de base de datos SQL limpiar filas.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 076f5f95-f8d2-42c7-b7fd-6798856ba0bb
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/22/2017
ms.author: glenga
ms.openlocfilehash: 063a25fe8d14a75d54e9b72cec9fc1e25fa3ff44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a>Usar funciones de Azure tooconnect tooan base de datos de SQL Azure
Este tema muestra cómo toouse funciones de Azure toocreate programada del trabajo que limpia filas de una tabla en una base de datos de SQL Azure. función de Hello nuevo C# se crea en función de una plantilla de desencadenador de temporizador predefinidos en hello portal de Azure. toosupport este escenario, también debe establecer una cadena de conexión de base de datos como una configuración de aplicación de la función de hello. Este escenario usa una operación masiva con la base de datos de Hola. toohave las función proceso CRUD de las operaciones individuales en una tabla de aplicaciones móviles, debe usar en su lugar [enlaces de aplicaciones móviles](functions-bindings-mobile-apps.md).

## <a name="prerequisites"></a>Requisitos previos

+ En este tema se usa una función desencadenada por un temporizador. Hola completa los pasos en el tema de hello [crear una función de Azure que se desencadena por un temporizador](functions-create-scheduled-function.md) versión toocreate C# de esta función.   

+ Este tema muestra un comando de Transact-SQL que ejecuta una operación de limpieza de forma masiva en hello **SalesOrderHeader** tabla de base de datos de ejemplo de Hola AdventureWorksLT. datos de ejemplo AdventureWorksLT de toocreate Hola Hola completa los pasos de tema de hello [crear una base de datos de SQL Azure en el portal de Azure hello](../sql-database/sql-database-get-started-portal.md). 

## <a name="get-connection-information"></a>Obtención de información sobre la conexión

Se necesita la cadena de conexión de Hola de tooget de base de datos de Hola que creó al completar [crear una base de datos de SQL Azure en el portal de Azure hello](../sql-database/sql-database-get-started-portal.md).

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
 
3. Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y seleccione la base de datos en hello **bases de datos SQL** página.

4. Seleccione **mostrar cadenas de conexión de base de datos** hello copia completa y **ADO.NET** cadena de conexión.

    ![Copie la cadena de conexión de ADO.NET Hola.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a>Establece la cadena de conexión de Hola 

Una aplicación de la función hospeda ejecución Hola de las funciones de Azure. Es una mejor las cadenas de conexión de toostore de práctica y otros secretos en la configuración de aplicación de la función. Con la configuración de aplicación impide la divulgación accidental de la cadena de conexión de hello con el código. 

1. Navegar por la aplicación de la función de tooyour que creó [crear una función de Azure que se desencadena por un temporizador](functions-create-scheduled-function.md).

2. Seleccione **Características de la plataforma** > **Configuración de la aplicación**.
   
    ![Configuración de la aplicación para la aplicación de la función de hello.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. Desplácese hacia abajo demasiado**las cadenas de conexión** y agregar una cadena de conexión mediante configuración de hello como se especifica en la tabla de Hola.
   
    ![Agregar una configuración de la aplicación de la cadena toohello conexión función.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | Configuración       | Valor sugerido | Descripción             | 
    | ------------ | ------------------ | --------------------- | 
    | **Name**  |  sqldb_connection  | Hola tooaccess usado almacena cadena de conexión en el código de función.    |
    | **Valor** | Cadena copiada  | Más allá de la cadena de conexión de Hola que copió en la sección anterior de Hola. |
    | **Tipo** | SQL Database | Usar conexión de base de datos SQL de hello predeterminada. |   

3. Haga clic en **Guardar**.

Ahora, puede agregar Hola función código de C# que se conecta tooyour base de datos SQL.

## <a name="update-your-function-code"></a>Actualización del código de función

1. En la aplicación de la función, seleccione función de hello desencadenada por el temporizador.
 
3. Agregue Hola siguiendo las referencias de ensamblado en parte superior de Hola Hola existente del código de función:

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. Agregue los siguiente hello `using` función toohello de instrucciones:
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. Reemplazar existente hello **ejecutar** función con el siguiente código de hello:
    ```cs
    public static async Task Run(TimerInfo myTimer, TraceWriter log)
    {
        var str = ConfigurationManager.ConnectionStrings["sqldb_connection"].ConnectionString;
        using (SqlConnection conn = new SqlConnection(str))
        {
            conn.Open();
            var text = "UPDATE SalesLT.SalesOrderHeader " + 
                    "SET [Status] = 5  WHERE ShipDate < GetDate();";

            using (SqlCommand cmd = new SqlCommand(text, conn))
            {
                // Execute hello command and log hello # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    Este comando de ejemplo actualiza hello **estado** columna según la fecha de envío de Hola. Debería actualizar 32 filas de datos.

5. Haga clic en **guardar**, Hola inspección **registros** windows para hello función ejecución, a continuación, anote Hola número de filas actualizadas en hello **SalesOrderHeader** tabla.

    ![Ver registros de funciones de Hola.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a>Pasos siguientes

A continuación, obtenga información acerca de cómo las funciones de toouse a toointegrate Logic Apps con otros servicios.

> [!div class="nextstepaction"] 
> [Creación de una función que se integre con Logic Apps](functions-twitter-email.md)

Para obtener más información acerca de las funciones, vea Hola temas siguientes:

* [Azure Functions developer reference](functions-reference.md)  
  contiene las referencias del programador para codificar funciones y definir desencadenadores y enlaces.
* [Prueba de Azure Functions](functions-test-a-function.md)  
  describe las diversas herramientas y técnicas para probar sus funciones.  
