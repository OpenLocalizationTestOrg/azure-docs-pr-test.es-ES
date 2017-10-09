---
title: aaaConnect tooAzure almacenamiento de datos de SQL - VSTS | Documentos de Microsoft
description: Consultas en Almacenamiento de datos SQL con Visual Studio.
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a>Conectar tooSQL almacenamiento de datos con Visual Studio como SSDT
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Use Visual Studio tooquery almacenamiento de datos de SQL Azure en tan solo unos minutos. Este método usa la extensión de SQL Server Data Tools (SSDT) de hello en Visual Studio. 

## <a name="prerequisites"></a>Requisitos previos
toouse este tutorial, necesita:

* Una cuenta de SQL Data Warehouse existente. toocreate uno, vea [crear un almacén de datos de SQL][Create a SQL Data Warehouse].
* SSDT para Visual Studio. Si tiene Visual Studio, probablemente ya tenga este componente. Para ver opciones e instrucciones de instalación, consulte [Instalación de Visual Studio 2015 y SSDT para SQL Data Warehouse][Installing Visual Studio and SSDT].
* Hola completo nombre de SQL server. toofind, vea [conectar tooSQL Data Warehouse][Connect tooSQL Data Warehouse].

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. Conectar tooyour almacenamiento de datos SQL
1. Abra Visual Studio 2013 o 2015
2. Abra el Explorador de objetos de SQL Server. toodo, seleccione **vista** > **Explorador de objetos de SQL Server**.
   
    ![Explorador de objetos de SQL Server][1]
3. Haga clic en hello **agregar SQL Server** icono.
   
    ![Agregar SQL Server][2]
4. Rellene los campos de hello en ventana de hello conectar tooServer.
   
    ![Conectar tooServer][3]
   
   * **Nombre del servidor**. Escriba hello **nombre del servidor** ha identificado anteriormente.
   * **Autenticación**. Seleccione **Autenticación de SQL Server** o **Autenticación integrada de Active Directory**.
   * **Nombre de usuario** y **Contraseña**. Escriba el nombre de usuario y la contraseña si la autenticación de SQL Server se seleccionó anteriormente.
   * Haga clic en **Conectar**.
5. tooexplore, expanda el servidor de SQL Azure. Puede ver bases de datos de hello asociadas con el servidor de Hola. Expandir AdventureWorksDW toosee Hola tablas en la base de datos de ejemplo.
   
    ![Explorar AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a>2. Ejecución de una consulta de ejemplo
Ahora que ha sido establecida tooyour base de datos de una conexión, vamos a escribir una consulta.

1. Haga clic con el botón derecho en la base de datos en el Explorador de objetos de SQL Server.
2. Seleccione **Nueva consulta**. Se abre una nueva ventana de consulta.
   
    ![Nueva consulta][5]
3. Copie esta consulta TSQL en la ventana de consulta de hello:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Ejecutar consulta Hola. toodo esto, haga clic en la flecha verde de Hola o usar hello siguiendo el método abreviado: `CTRL` + `SHIFT` + `E`.
   
    ![Ejecutar consulta][6]
5. Buscar en los resultados de la consulta de Hola. En este ejemplo, la tabla FactInternetSales de hello tiene 60398 filas.
   
    ![Resultados de la consulta][7]

## <a name="next-steps"></a>Pasos siguientes
Ahora que puede conectarse y consultar, intente [visualizar datos Hola con Power BI][visualizing hello data with PowerBI].

tooconfigure su entorno para la autenticación de Azure Active Directory, vea [autenticar tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
