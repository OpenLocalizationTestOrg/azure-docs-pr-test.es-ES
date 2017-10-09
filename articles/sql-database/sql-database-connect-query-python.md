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
# <a name="use-python-tooquery-an-azure-sql-database"></a><span data-ttu-id="f07e9-103">Usar Python tooquery una base de datos de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="f07e9-103">Use Python tooquery an Azure SQL database</span></span>

 <span data-ttu-id="f07e9-104">Este inicio rápido se muestra cómo toouse [Python](https://python.org) tooconnect tooan SQL Azure la base de datos y usar datos de tooquery de instrucciones de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="f07e9-104">This quick start demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f07e9-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f07e9-105">Prerequisites</span></span>

<span data-ttu-id="f07e9-106">toocomplete rápida de este tutorial de inicio, asegúrese de que tiene Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="f07e9-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="f07e9-107">Una base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="f07e9-107">An Azure SQL database.</span></span> <span data-ttu-id="f07e9-108">Este inicio rápido utiliza recursos de hello creados mediante uno de estos tutoriales:</span><span class="sxs-lookup"><span data-stu-id="f07e9-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="f07e9-109">Creación de la base de datos: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f07e9-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="f07e9-110">Creación de la base de datos: CLI</span><span class="sxs-lookup"><span data-stu-id="f07e9-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="f07e9-111">Creación de la base de datos: PowerShell</span><span class="sxs-lookup"><span data-stu-id="f07e9-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="f07e9-112">A [regla de firewall de nivel de servidor](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) para la dirección IP pública de hello del equipo de Hola se usa para este tutorial de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="f07e9-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="f07e9-113">Ha instalado Python y el software relacionado para el sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="f07e9-113">You have installed Python and related software for your operating system.</span></span>

    - <span data-ttu-id="f07e9-114">**MacOS**: Homebrew instalar Python, instalar el controlador ODBC de Hola y SQLCMD y, a continuación, instale Hola controlador Python para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f07e9-114">**MacOS**: Install Homebrew and Python, install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="f07e9-115">Consulte los [pasos 1.2, 1.3 y 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span><span class="sxs-lookup"><span data-stu-id="f07e9-115">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/mac/).</span></span>
    - <span data-ttu-id="f07e9-116">**Ubuntu**: instalar Python y otros necesarios paquetes y, a continuación, instalar Hola controlador Python para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f07e9-116">**Ubuntu**:  Install Python and other required packages, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="f07e9-117">Consulte los [pasos 1.2, 1.3 y 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="f07e9-117">See [Steps 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu/).</span></span>
    - <span data-ttu-id="f07e9-118">**Windows**: instale la versión más reciente de Hola de Python (variable de entorno está configurada ahora para usted), instalar el controlador ODBC de Hola y SQLCMD y, a continuación, instale Hola controlador Python para SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f07e9-118">**Windows**: Install hello newest version of Python (environment variable is now configured for you), install hello ODBC driver and SQLCMD, and then install hello Python Driver for SQL Server.</span></span> <span data-ttu-id="f07e9-119">Consulte [pasos 1.2, 1.3 y 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span><span class="sxs-lookup"><span data-stu-id="f07e9-119">See [Step 1.2, 1.3, and 2.1](https://www.microsoft.com/sql-server/developer-get-started/python/windows/).</span></span> 

## <a name="sql-server-connection-information"></a><span data-ttu-id="f07e9-120">Información de conexión de SQL server</span><span class="sxs-lookup"><span data-stu-id="f07e9-120">SQL server connection information</span></span>

<span data-ttu-id="f07e9-121">Obtener base de datos SQL de Azure de toohello de tooconnect de hello conexión información necesaria.</span><span class="sxs-lookup"><span data-stu-id="f07e9-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="f07e9-122">Necesitará el nombre del servidor de acceso completa de hello, nombre de base de datos y la información de inicio de sesión en los procedimientos siguientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="f07e9-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="f07e9-123">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f07e9-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f07e9-124">Seleccione **bases de datos SQL** desde el menú de la izquierda, hello y haga clic en la base de datos en hello **bases de datos SQL** página.</span><span class="sxs-lookup"><span data-stu-id="f07e9-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="f07e9-125">En hello **Introducción** página de la base de datos, revisión Hola servidor nombre completo como se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="f07e9-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="f07e9-126">Puede mantener el mouse sobre toobring de nombre de servidor hello seguridad hello **haga clic en toocopy** opción.</span><span class="sxs-lookup"><span data-stu-id="f07e9-126">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="f07e9-128">Si olvida su información de inicio de sesión de servidor, vaya toohello base de datos de SQL server página tooview Hola administrador nombre del servidor y, si es necesario, restablecer la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="f07e9-128">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name and, if necessary, reset hello password.</span></span>     
    
## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="f07e9-129">Insertar la base de datos SQL de tooquery de código</span><span class="sxs-lookup"><span data-stu-id="f07e9-129">Insert code tooquery SQL database</span></span> 

1. <span data-ttu-id="f07e9-130">En el editor de texto, cree un nuevo archivo, **sqltest.py**.</span><span class="sxs-lookup"><span data-stu-id="f07e9-130">In your favorite text editor, create a new file, **sqltest.py**.</span></span>  

2. <span data-ttu-id="f07e9-131">Reemplace el contenido de hello con hello siguiente de código y agregue los valores adecuados de hello para el servidor, la base de datos, el usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="f07e9-131">Replace hello contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-hello-code"></a><span data-ttu-id="f07e9-132">Ejecutar código de hello</span><span class="sxs-lookup"><span data-stu-id="f07e9-132">Run hello code</span></span>

1. <span data-ttu-id="f07e9-133">En hello símbolo del sistema, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="f07e9-133">At hello command prompt, run hello following commands:</span></span>

   ```Python
   python sqltest.py
   ```

2. <span data-ttu-id="f07e9-134">Compruebe que 20 filas de top Hola se devuelven y, a continuación, cierre la ventana de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f07e9-134">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f07e9-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f07e9-135">Next steps</span></span>

- [<span data-ttu-id="f07e9-136">Diseño de su primera base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="f07e9-136">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="f07e9-137">Controladores de Microsoft para Python para SQL Server</span><span class="sxs-lookup"><span data-stu-id="f07e9-137">Microsoft Python Drivers for SQL Server</span></span>](https://docs.microsoft.com/sql/connect/python/python-driver-for-sql-server/)
- [<span data-ttu-id="f07e9-138">Centro para desarrolladores de Python</span><span class="sxs-lookup"><span data-stu-id="f07e9-138">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/?v=17.23h)

