---
title: Conectar tooAzure base de datos de MySQL desde C++ | Documentos de Microsoft
description: "Este tutorial rápido proporciona un ejemplo de código de C++ puede utilizar tooconnect y consultar los datos de la base de datos MySQL."
services: mysql
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: C++
ms.topic: hero-article
ms.date: 08/03/2017
ms.openlocfilehash: d027597bf02b1eacab9b8808957399f6e54e63cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a>Base de datos de Azure para MySQL: Use conector c/c ++ tooconnect y consultar datos
Este tutorial rápido muestra cómo tooconnect tooan Azure la base de datos de MySQL mediante una aplicación de C++. Muestra cómo toouse tooquery de instrucciones de SQL, insertar, actualizar y eliminar datos en la base de datos de Hola. Hello pasos descritos en este artículo se suponen que está familiarizado con el desarrollo con C++ y que son tooworking nueva con la base de datos de Azure para MySQL.

## <a name="prerequisites"></a>Requisitos previos
Este tutorial rápido usa recursos de hello creados en cualquiera de estas guías como punto de partida:
- [Create an Azure Database for MySQL server using Azure Portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)
- [Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)

Además, deberá:
- Instalar [.NET Framework](https://www.microsoft.com/net/download)
- Instalar [Visual Studio](https://www.visualstudio.com/downloads/)
- Instalación de [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/) 
- Instalación de [Boost](http://www.boost.org/)

## <a name="install-visual-studio-and-net"></a>Instalación de Visual Studio y .NET
pasos de Hello en esta sección se supone que está familiarizado con el desarrollo con. NET.

### <a name="windows"></a>**Windows**
1. Instale Visual Studio 2017 Community, que es un IDE gratuito, ampliable, rico en contenido y visualmente atractivo para la creación de aplicaciones modernas para Android, iOS, Windows, así como aplicaciones web y de base de datos, y servicios en la nube. Puede instalar Hola completa de .NET Framework o simplemente .NET Core. fragmentos de código de Hello en hello inicio rápido de trabajar con cualquiera. Si ya tiene Visual Studio instalados en su equipo, omita Hola dos pasos siguientes.
   - Descargar hello [instalador de Visual Studio de 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15). 
   - Ejecute el programa de instalación de Hola y siga Hola instalación indicaciones toocomplete Hola.

### <a name="configure-visual-studio"></a>**Configuración de Visual Studio**
1. Desde Visual Studio, la propiedad de proyecto > Propiedades de configuración > C/C++ > vinculador > general > directorios de bibliotecas adicionales, agregue el directorio de lib\opt de hello (es decir,: C:\Program Files (x86) \MySQL\MySQL conector C++ 1.1.9\lib\opt) de hello c ++ conector.
2. Desde Visual Studio, propiedad de proyecto > propiedades de configuración > C/C++ > general > directorios de inclusión adicionales
   - Agregue el directorio include/ del conector de c ++ (es decir, C:\Archivos de programa (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)
   - Agregue el directorio raíz de la biblioteca Boost (es decir, C:\boost_1_64_0\)
3. Desde Visual Studio, la propiedad de proyecto > Propiedades de configuración > C/C++ > vinculador > entrada > dependencias adicionales, agregue mysqlcppconn.lib en el campo de texto hello
4. Cualquier mysqlcppconn.dll de copia de hello c ++ conector carpeta library en paso 3 toohello mismo directorio que el ejecutable de la aplicación hello o Agregar variable de entorno toohello para que la aplicación pueda encontrarlo.

## <a name="get-connection-information"></a>Obtención de información sobre la conexión
Obtener Hola conexión información necesaria tooconnect toohello base de datos MySQL. Es necesario Hola credenciales de inicio de sesión y nombre de servidor completo.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú de la izquierda de hello en el portal de Azure, haga clic en **todos los recursos** y busque el servidor de Hola se haya creado, como **myserver4demo**.
3. Haga clic en el nombre del servidor de Hola.
4. Servidor de hello seleccione **propiedades** página. Tome nota de hello **nombre del servidor** y **nombre de inicio de sesión del Administrador de servidor**.
 ![Nombre del servidor de Azure Database for MySQL](./media/connect-cpp/1_server-properties-name-login.png)
5. Si olvida su información de inicio de sesión de servidor, vaya a toohello **información general sobre** página Nombre de inicio de sesión de administrador del servidor de tooview hello y, si es necesario, restablecer la contraseña de Hola.

## <a name="connect-create-table-and-insert-data"></a>Conexión, creación de una tabla e inserción de datos
Código tooconnect siguiente de Hola de uso y cargar datos de hello mediante **CREATE TABLE** y **INSERT INTO** instrucciones SQL. código de Hello utiliza clase sql::Driver de hello connect() método tooestablish una tooMySQL de conexión. A continuación, código de hello usa método createStatement() y Execute toorun Hola comandos base de datos. 

Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos. 

```c++
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::Statement *stmt;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }

    stmt = con>createStatement();
    stmt>execute("DROP TABLE IF EXISTS inventory");
    cout << "Finished dropping table (if existed)" << endl;
    stmt>execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
    cout << "Finished creating table" << endl;
    delete stmt;

    pstmt = con>prepareStatement("INSERT INTO inventory(name, quantity) VALUES(?,?)");
    pstmt>setString(1, "banana");
    pstmt>setInt(2, 150);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "orange");
    pstmt>setInt(2, 154);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "apple");
    pstmt>setInt(2, 100);
    pstmt>execute();
    cout << "One row inserted." << endl;
    
    delete pstmt;   
    delete con;
    system("pause");
    return 0;

```

## <a name="read-data"></a>Lectura de datos

Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **seleccione** instrucción SQL. código de Hello utiliza clase sql::Driver de hello connect() método tooestablish una tooMySQL de conexión. A continuación, código de hello usa el método prepareStatement() y executeQuery() toorun Hola seleccionar comandos. Por último código de hello usa next() tooadvance toohello registros en los resultados de Hola. A continuación, el código de hello usa valores de hello tooparse getInt() y getString() en el registro de hello.

Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos. 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

//  select  
    pstmt = con>prepareStatement("SELECT * FROM inventory;");
    result = pstmt>executeQuery();  
    
    while (result>next())
        printf("Reading from table=(%d, %s, %d)\n", result>getInt(1), result>getString(2).c_str(), result>getInt(3));   
    
    delete result;
    delete pstmt;   
    delete con;
    system("pause");
    return 0;
}
```

## <a name="update-data"></a>Actualización de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **actualización** instrucción SQL. código de Hello utiliza clase sql::Driver de hello connect() método tooestablish una tooMySQL de conexión. A continuación, código de hello usa método prepareStatement() y executeQuery() toorun Hola comandos de actualización. 

Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos. 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

    //update
    pstmt = con>prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?");
    pstmt>setInt(1, 200);
    pstmt>setString(2, "banana");
    pstmt>executeQuery();
    printf("Row updated\n");
    
    delete con;
    delete pstmt;
    system("pause");
    return 0;
}
```


## <a name="delete-data"></a>Eliminación de datos
Código tooconnect siguiente de Hola de uso y leer datos de hello mediante un **eliminar** instrucción SQL. código de Hello utiliza clase sql::Driver de hello connect() método tooestablish una tooMySQL de conexión. A continuación, código de hello usa método prepareStatement() y executeQuery() toorun Hola eliminar comandos.

Reemplazar parámetros de Host, DBName, usuario y contraseña de hello con valores de hello que especificó cuando creó el servidor de Hola y de base de datos. 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }
        
    //delete
    pstmt = con>prepareStatement("DELETE FROM inventory WHERE name = ?");
    pstmt>setString(1, "orange");
    result = pstmt>executeQuery();
    printf("Row deleted\n");    
    
    delete pstmt;
    delete con;
    delete result;
    system("pause");
    return 0;
}
```

## <a name="next-steps"></a>Pasos siguientes
> [!div class="nextstepaction"]
> [Migrar su tooAzure de base de datos base de datos de MySQL para uso de volcado de memoria y la restauración de MySQL](concepts-migrate-dump-restore.md)
