---
title: Conectar tooAzure base de datos de MySQL desde MySQL Workbench | Documentos de Microsoft
description: "Este tutorial rápido proporciona Hola pasos toouse MySQL Workbench tooconnect y consultar datos de base de datos de Azure para MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: seanli1988
ms.service: mysql-database
ms.custom: mvc
ms.topic: article
ms.date: 08/23/2017
ms.openlocfilehash: c64fcb9bb99ba06aa3a95eec420d5d5ef4a31d14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-mysql-workbench-tooconnect-and-query-data"></a>Base de datos de Azure para MySQL: Use MySQL Workbench tooconnect y consultar datos
Este tutorial rápido muestra cómo tooconnect tooan base de datos de Azure para el uso de MySQL Hola aplicación MySQL Workbench. 

## <a name="prerequisites"></a>Requisitos previos
Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:
- [Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)
- [Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)

## <a name="install-mysql-workbench"></a>Instalación de MySQL Workbench
Descargar e instalar el MySQL Workbench en el equipo de [sitio Web de MySQL de hello](https://dev.mysql.com/downloads/workbench/).

## <a name="get-connection-information"></a>Obtención de información sobre la conexión
Obtener Hola conexión información necesaria tooconnect toohello base de datos MySQL. Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).

2. En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque el servidor de Hola se haya creado, como **myserver4demo**.

3. Haga clic en el nombre del servidor de Hola.

4. Servidor de hello seleccione **propiedades** página. Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.

 ![Nombre del servidor de Azure Database for MySQL](./media/connect-workbench/1-server-properties-name-login.png)
 
5. Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.

## <a name="connect-toohello-server-using-mysql-workbench"></a>Conectar con MySQL Workbench de servidor de toohello 
servidor de MySQL de tooconnect tooAzure mediante Hola GUI MySQL Workbench:

1.  Inicie Hola aplicación MySQL Workbench en el equipo. 

2.  En **el programa de instalación nueva conexión** diálogo cuadro, escriba Hola siguiente información en hello **parámetros** ficha:

    ![Configuración de una conexión nueva](./media/connect-workbench/2-setup-new-connection.png)

    | **Configuración** | **Valor sugerido** | **Descripción del campo** |
    |---|---|---|
    |   Nombre de la conexión | Conexión de demostración | Especifique una etiqueta para esta conexión. |
    | Método de conexión | Estándar (TCP/IP) | Estándar (TCP/IP) es suficiente. |
    | Nombre de host. | *nombre del servidor* | Especifique el valor de nombre de servidor de Hola que se usó cuando creó Hola base de datos de Azure para MySQL anteriormente. El servidor de ejemplo que se muestra es myserver4demo.mysql.database.azure.com. Usar el nombre de dominio completo de hello (\*. mysql.database.azure.com) tal y como se muestra en el ejemplo de Hola. Siga los pasos Hola Hola anterior sección tooget Hola información de la conexión si no recuerda el nombre del servidor.  |
    | Port | 3306 | Utilice siempre el puerto 3306 al conectarse tooAzure base de datos de MySQL. |
    | Nombre de usuario |  *nombre de inicio de sesión del administrador del servidor* | Escriba Hola server inicio de sesión nombre de usuario administrador especificó al crear Hola base de datos de Azure para MySQL anteriormente. El nombre de usuario de nuestro ejemplo es myadmin@myserver4demo. Siga los pasos Hola Hola anterior sección tooget Hola información de la conexión si no recuerda el nombre de usuario de Hola. formato de Hello es  *username@servername* .
    | Password | la contraseña | Haga clic en **almacén en el almacén...**  contraseña de botón toosave Hola. |

3.   Haga clic en **Probar conexión** tootest si todos los parámetros están configurados correctamente. 

4.   Haga clic en **Aceptar** conexión de hello toosave. 

5.   En la lista de Hola de **MySQL conexiones**, haga clic en servidor de hello mosaico correspondiente tooyour y espere hello toobe de conexión establecida.

6.   Una pestaña SQL nueva se abre con un editor en blanco en el que puede escribir las consultas.

    > [!NOTE]
    > De forma predeterminada, la seguridad de conexión SSL es necesaria y se aplica al servidor de Azure Database para MySQL. Normalmente ninguna configuración adicional con certificados SSL es necesaria para el servidor de MySQL Workbench tooconnect tooyour. Para obtener más información sobre SSL, consulte [tooAzure base de datos de conexión de conectividad de configurar SSL en su aplicación toosecurely para MySQL](./howto-configure-ssl.md).  Si necesita toodisable SSL, visite el portal de Azure de Hola y haga clic en hello conexión seguridad página toodisable Hola exigir SSL conexión botón de alternancia.

## <a name="create-a-table-insert-data-read-data-update-data-delete-data"></a>Creación de una tabla, inserción de datos, lectura de datos, actualización de datos, eliminación de datos
1. Copie y pegue el código de ejemplo de Hola SQL en un tooillustrate de pestaña SQL en blanco algunos datos de ejemplo.

    Este código crea una base de datos vacía llamada quickstartdb y luego crea una tabla de ejemplo llamada inventario. Inserta filas, a continuación, se lee filas Hola. Cambia datos Hola con una instrucción update y lecturas Hola filas de nuevo. Por último, se elimina una fila y lee filas Hola de nuevo.
    
    ```sql
    -- Create a database
    -- DROP DATABASE IF EXISTS quickstartdb;
    CREATE DATABASE quickstartdb;
    USE quickstartdb;
    
    -- Create a table and insert rows
    DROP TABLE IF EXISTS inventory;
    CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);
    INSERT INTO inventory (name, quantity) VALUES ('banana', 150);
    INSERT INTO inventory (name, quantity) VALUES ('orange', 154);
    INSERT INTO inventory (name, quantity) VALUES ('apple', 100);
    
    -- Read
    SELECT * FROM inventory;
    
    -- Update
    UPDATE inventory SET quantity = 200 WHERE id = 1;
    SELECT * FROM inventory;
    
    -- Delete
    DELETE FROM inventory WHERE id = 2;
    SELECT * FROM inventory;
    ```

    captura de pantalla de Hello muestra un ejemplo de Hola código SQL en la salida de SQL Workbench y Hola después de que se ha ejecutado.
    
    ![Código de pestaña de SQL Workbench MySQL toorun ejemplo SQL](media/connect-workbench/3-workbench-sql-tab.png)

2. ejemplo de Hola a toorun código SQL, haga clic en icono en la barra de herramientas de Hola de Hola de rayo de hello **archivo SQL** ficha.
3. Tenga en cuenta Hola tres resultados con pestañas en hello **cuadrícula de resultados** sección en medio de Hola de página Hola. 
4. Hola aviso **salida** lista final Hola de página Hola. se muestra el estado de Hola de cada comando. 

Ahora, ha conectado tooAzure base de datos de MySQL con MySQL Workbench y ha consultado datos mediante el lenguaje SQL Hola.

## <a name="next-steps"></a>Pasos siguientes
> [!div class="nextstepaction"]
> [Migración de una base de datos mediante exportación e importación](./concepts-migrate-import-export.md)
