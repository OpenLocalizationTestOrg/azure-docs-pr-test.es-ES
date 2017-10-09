---
title: aaaUse Python tooquery base de datos de SQL de Azure | Documentos de Microsoft
description: "Este tema muestra cómo toouse Python toocreate un programa que conecta tooan base de datos de SQL Azure y consultas mediante instrucciones Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 452ad236-7a15-4f19-8ea7-df528052a3ad
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 08/08/2017
ms.author: carlrab
ms.openlocfilehash: 6c786e7a61f5ed3e7d2395da59acfeae008e90e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-tooquery-an-azure-sql-database"></a>Usar Python tooquery una base de datos de SQL Azure

 Este inicio rápido se muestra cómo toouse [Python](https://python.org) tooconnect tooan SQL Azure la base de datos y usar datos de tooquery de instrucciones de Transact-SQL.

## <a name="prerequisites"></a>Requisitos previos

toocomplete rápida de este tutorial de inicio, asegúrese de que tiene Hola siguientes:

- Una base de datos SQL de Azure. Este inicio rápido utiliza recursos de hello creados mediante uno de estos tutoriales: 

   - [Creación de la base de datos: Azure Portal](sql-database-get-started-portal.md)
   - [Creación de la base de datos: CLI](sql-database-get-started-cli.md)
   - [Creación de la base de datos: PowerShell](sql-database-get-started-powershell.md)

- A [regla de firewall de nivel de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para la dirección IP pública de hello del equipo de Hola se usa para este tutorial de inicio rápido.

- Ha instalado Python y el software relacionado para el sistema operativo.

    - **MacOS**: Homebrew instalar Python, instalar el controlador ODBC de Hola y SQLCMD y, a continuación, instale Hola controlador Python para SQL Server. Consulte los [pasos 1.2, 1.3 y 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).
    - **Ubuntu**: instalar Python y otros necesarios paquetes y, a continuación, instalar Hola controlador Python para SQL Server. Consulte los [pasos 1.2, 1.3 y 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).
    - **Windows**: instale la versión más reciente de Hola de Python (variable de entorno está configurada ahora para usted), instalar el controlador ODBC de Hola y SQLCMD y, a continuación, instale Hola controlador Python para SQL Server. Consulte [pasos 1.2, 1.3 y 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/). 

## <a name="sql-server-connection-information"></a>Información de conexión de SQL server

Obtener base de datos SQL de Azure de toohello de tooconnect de hello conexión información necesaria. Necesitará el nombre del servidor de acceso completa de hello, nombre de base de datos y la información de inicio de sesión en los procedimientos siguientes de Hola.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página. 
3. En hello **Introducción** página de la base de datos, revisión Hola servidor nombre completo como se muestra en hello después de la imagen. Puede mantener el mouse sobre toobring de nombre de servidor hello seguridad hello **haga clic en toocopy** opción.  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. Si olvida su información de inicio de sesión de servidor, vaya toohello base de datos de SQL server página tooview Hola administrador nombre del servidor y, si es necesario, restablecer la contraseña de Hola.     
    
## <a name="insert-code-tooquery-sql-database"></a>Insertar la base de datos SQL de tooquery de código 

1. En el editor de texto, cree un nuevo archivo, **sqltest.py**.  

2. Reemplace el contenido de hello con hello siguiente de código y agregue los valores adecuados de hello para el servidor, la base de datos, el usuario y la contraseña.

```Python
import pyodbc
server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

## <a name="run-hello-code"></a>Ejecutar código de hello

1. En hello símbolo del sistema, ejecute hello siguientes comandos:

   ```Python
   python sqltest.py
   ```

2. Compruebe que 20 filas de top Hola se devuelven y, a continuación, cierre la ventana de la aplicación hello.

## <a name="next-steps"></a>Pasos siguientes

- [Diseño de su primera base de datos SQL de Azure](sql-database-design-first-database.md)
- [Controladores de Microsoft para Python para SQL Server](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [Centro para desarrolladores de Python](https://azure.microsoft.com/develop/python/?v=17.23h)

