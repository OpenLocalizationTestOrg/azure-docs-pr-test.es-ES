---
title: aaaConnect tooSQL utilizar C y C++ de la base de datos | Documentos de Microsoft
description: "Ejemplo de Hola a usar código en este toobuild inicio rápido de una aplicación moderna con C++ y respaldado por una base de datos relacional eficaz en la nube de hello con base de datos de SQL Azure."
services: sql-database
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: 
ms.assetid: 07d9e0b1-3234-4f17-a252-a7559160a9db
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 03/06/2017
ms.author: edmacauley
ms.openlocfilehash: 9b581424c91bfdd93deb6914212629519a011d8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-database-using-c-and-c"></a>Conectar tooSQL utilizar C y C++ de la base de datos
Esta entrada está destinada a los desarrolladores de C y C++ que traten tooconnect tooAzure base de datos SQL. Se desglosa en secciones por lo que puede ir sección toohello que captura mejor su interés. 

## <a name="prerequisites-for-hello-cc-tutorial"></a>Requisitos previos para el tutorial de C o C++ Hola
Asegúrese de que tiene Hola siguientes elementos:

* Una cuenta de Azure activa. Si no tiene una, puede registrarse para obtener una [prueba gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* [Visual Studio](https://www.visualstudio.com/downloads/). Debe instalar toobuild de componentes de lenguaje de C++ de Hola y ejecutar este ejemplo.
* [Visual C++ for Linux Development](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e) (Visual C++ para el desarrollo de aplicaciones para Linux). Si está desarrollando en Linux, también debe instalar extensión de hello Linux de Visual Studio. 

## <a id="AzureSQL"></a>Azure SQL Database y SQL Server en máquinas virtuales
SQL Azure se basa en Microsoft SQL Server y está diseñada tooprovide un servicio escalable, rendimiento y alta disponibilidad. Hay muchas ventajas toousing SQL Azure a través de la base de datos propietario ejecuta de forma local. Con SQL Azure no tiene tooinstall, configurar, mantener o administre su base de datos, pero solo Hola contenido y estructura de saludo de la base de datos. Lo que nos suele preocupar de las bases de datos, como la redundancia y la tolerancia a errores, está ya integrado. 

Actualmente, Azure tiene dos opciones para hospedar cargas de trabajo de SQL Server: Azure SQL Database, una base de datos como servicio, y SQL Server en máquinas virtuales (VM). No se obtendrá en los detalles sobre las diferencias de hello entre estos dos salvo que la base de datos de SQL Azure es la mejor opción para nuevas aplicaciones basadas en nube tootake aprovechar Hola ahorros en costos y optimización del rendimiento que servicios en la nube proporcionan. Si se va a migrar o extender el entorno local en la nube aplicaciones toohello, SQL server en la máquina virtual de Azure quizá funcione mejor para usted. tookeep cosas simple para este artículo, vamos a crear una base de datos de SQL Azure. 

## <a id="ODBC"></a>Tecnologías de acceso a datos: ODBC y OLE DB
Conexión tooAzure base de datos SQL no es diferente y actualmente hay dos maneras de tooconnect toodatabases: ODBC (Open Database connectivity) y OLE DB (base de datos de vinculación e incrustación de objetos). En los últimos años, Microsoft se ha alineado con [ODBC para el acceso a datos relacionales nativos](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/). ODBC es relativamente sencillo y también mucho más rápido que OLE DB. Hola aquí la única advertencia es que ODBC usa una API de estilo C anterior. 

## <a id="Create"></a>Paso 1: Creación de una base de datos de Azure SQL
Vea hello [Introducción a la página](sql-database-get-started-portal.md) toolearn cómo toocreate una base de datos de ejemplo.  Como alternativa, puede seguir este [breve vídeo de dos minutos](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/) toocreate una base de datos de SQL Azure mediante Hola portal de Azure.

## <a id="ConnectionString"></a>Paso 2: Obtención de la cadena de conexión
Después de aprovisionar la base de datos de SQL Azure, necesita toocarry out Hola siguiendo la información de conexión de toodetermine de pasos y agregar la dirección IP de cliente para el acceso de firewall. 

En [portal de Azure](https://portal.azure.com/), vaya la cadena de conexión de ODBC de base de datos de SQL Azure de tooyour mediante el uso de hello **mostrar cadenas de conexión de base de datos** aparece como parte de la sección de información general de hello para la base de datos: 

![ODBCConnectionString](./media/sql-database-develop-cplusplus-simple/azureportal.png)

![ODBCConnectionStringProps](./media/sql-database-develop-cplusplus-simple/dbconnection.png)

Copie el contenido de Hola de hello **ODBC (incluye Node.js) [autenticación de SQL]** cadena. Usamos esta cadena tooconnect más adelante desde el intérprete de línea de comandos de C++ ODBC. Esta cadena proporciona detalles como controlador de hello, servidor y otros parámetros de conexión de base de datos. 

## <a id="Firewall"></a>Paso 3: Agregar el firewall de toohello IP
Toohello sección de firewall para el servidor de base de datos y agregue su [firewall del cliente IP toohello siguiendo estos pasos](sql-database-configure-firewall-settings.md) toomake seguro de que podemos establecer una conexión correcta: 

![AddyourIPWindow](./media/sql-database-develop-cplusplus-simple/ip.png)

En este momento, ha configurado la base de datos de SQL Azure y están listo tooconnect desde el código de C++. 

## <a id="Windows"></a>Paso 4: Conexión desde una aplicación de C o C++ de Windows
Le permite conectarse fácilmente tooyour [base de datos de SQL de Azure mediante ODBC en Windows con este ejemplo](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29) que compile con Visual Studio. ejemplo de Hola implementa un intérprete de línea de comandos de ODBC que puede ser utilizados tooconnect tooour base de datos de SQL Azure. Este ejemplo toma las un archivo de archivo (DSN) del nombre de origen de base de datos como un argumento de línea de comandos o cadena de conexión detallado de Hola que se copió anteriormente de hello portal de Azure. Abrirá la página de propiedades de Hola para este proyecto y pegue la cadena de conexión de Hola como un argumento de comando, como se muestra aquí: 

![DSN Propsfile](./media/sql-database-develop-cplusplus-simple/props.png)

Asegúrese de que proporcionar detalles de autenticación adecuado de hello para la base de datos como parte de esa cadena de conexión de base de datos. 

Iniciar toobuild de aplicación Hola se. Debería ver Hola siguiente ventana validar una conexión correcta. Incluso puede ejecutar algunos comandos básicos de SQL como **crear tabla** toovalidate la conectividad de base de datos:

![Comandos SQL](./media/sql-database-develop-cplusplus-simple/sqlcommands.png)

Como alternativa, podría crear un DSN de archivo mediante el Asistente de Hola que se inicia cuando se proporciona ningún argumento de comando. Se recomienda que lo intente también con esta opción. Puede usar este archivo DSN para la automatización y protección de la configuración de autenticación: 

![Create DSN File](./media/sql-database-develop-cplusplus-simple/datasource.png)

¡Enhorabuena! Ahora se ha conectado correctamente tooAzure SQL con C++ y ODBC en Windows. Puede continuar leyendo toodo Hola igual para así la plataforma Linux. 

## <a id="Linux"></a>Paso 5: Conexión desde una aplicación de C o C++ de Linux
En caso de que aún no lo ha escuchado noticias Hola aún, Visual Studio ahora permite toodevelop así la aplicación de C++ Linux. Puede leer acerca de este escenario nuevo en hello [Visual C++ para el desarrollo de Linux](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) blog. toobuild para Linux, necesita un equipo remoto donde se está ejecutando la distribución de Linux. Si no dispone de ninguno, puede configurar uno rápidamente mediante [Azure Virtual Machines de Linux](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Para este tutorial, supongamos que tenga configurada una distribución de Linux de Ubuntu 16.04. también deben aplicar estos pasos de Hello tooUbuntu 15.10, Red Hat 6 y Red Hat 7. 

Hello pasos siguientes instalación bibliotecas de hello necesarias para SQL y ODBC para su distribución:

    sudo su
    sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/mssql-ubuntu-test/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list'
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    apt-get update
    apt-get install msodbcsql
    apt-get install unixodbc-dev-utf16 #this step is optional but recommended*

Inicie Visual Studio. En Herramientas -> Opciones -> multiplataforma -> Administrador de conexiones, agregue un cuadro de conexión tooyour Linux: 

![Tools Options](./media/sql-database-develop-cplusplus-simple/tools.png)

Una vez establecida la conexión a través de SSH, cree una plantilla Empty project (Linux): 

![New project template](./media/sql-database-develop-cplusplus-simple/template.png)

A continuación, puede agregar un [nuevo archivo de código fuente C y reemplazarlo por este contenido](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c). Con hello SQLAllocHandle utilizando las API de ODBC y SQLSetConnectAttr, SQLDriverConnect, debe ser capaz de tooinitialize y establecer una base de datos de conexión tooyour. Al igual que con el ejemplo de Hola a ODBC de Windows, debe tooreplace Hola SQLDriverConnect a llamada con detalles de Hola de los parámetros de cadena de conexión de base de datos copiados de hello portal de Azure previamente. 

     retcode = SQLDriverConnect(
        hdbc, NULL, "Driver=ODBC Driver 13 for SQL"
                    "Server;Server=<yourserver>;Uid=<yourusername>;Pwd=<"
                    "yourpassword>;database=<yourdatabase>",
        SQL_NTS, outstr, sizeof(outstr), &outstrlen, SQL_DRIVER_NOPROMPT);

Hola toodo última cosa antes de compilar tooadd **odbc** como una dependencia de biblioteca: 

![Adding ODBC as an input library](./media/sql-database-develop-cplusplus-simple/lib.png)

toolaunch su aplicación, abrirá Hola consola de Linux de hello **depurar** menú: 

![Linux Console](./media/sql-database-develop-cplusplus-simple/linuxconsole.png)

Si la conexión se realizó correctamente, ahora debería ver el nombre de base de datos actual de hello imprime en hello consola de Linux: 

![Linux Console Window Output](./media/sql-database-develop-cplusplus-simple/linuxconsolewindow.png)

¡Enhorabuena! Ha completado correctamente el tutorial de Hola y ahora se puede conectar la base de datos de SQL Azure tooyour desde C++ en las plataformas Windows y Linux.

## <a id="GetSolution"></a>Obtener Hola completa C/C++ solución del tutorial
Puede encontrar la solución de GetStarted de Hola que contiene todos los ejemplos de hello en este artículo en github:

* [Ejemplo de Windows en C++ ODBC](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29), descargue tooAzure tooconnect de ejemplo de ODBC de C++ de Windows hello SQL
* [Ejemplo de ODBC C++ Linux](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29), descargar Hola Linux de ejemplo de ODBC de C++ tooconnect tooAzure SQL

## <a name="next-steps"></a>Pasos siguientes
* Hola de revisión [información general sobre el desarrollo de base de datos de SQL](sql-database-develop-overview.md)
* Obtener más información sobre hello [referencia de la API de ODBC](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)

## <a name="additional-resources"></a>Recursos adicionales
* [Modelos de diseño para las aplicaciones SaaS multiinquilino con base de datos SQL de Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* Explorar todas las hello [funciones de base de datos SQL](https://azure.microsoft.com/services/sql-database/)

