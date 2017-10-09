---
title: aaaConnect tooAzure almacenamiento de datos de SQL - SSMS | Documentos de Microsoft
description: Usar SQL Server Management Studio (SSMS) tooconnect tooand consulta de almacenamiento de datos de SQL Azure.
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a>Conectar tooSQL almacenamiento de datos con SQL Server Management Studio (SSMS)
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Usar SQL Server Management Studio (SSMS) tooconnect tooand consulta de almacenamiento de datos de SQL Azure. 

## <a name="prerequisites"></a>Requisitos previos
toouse este tutorial, necesita:

* Una cuenta de SQL Data Warehouse existente. toocreate uno, vea [crear un almacén de datos de SQL][Create a SQL Data Warehouse].
* SQL Server Management Studio (SSMS) instalado. [Instale SSMS][Install SSMS] de forma gratuita si aún no lo tiene.
* Hola completo nombre de SQL server. toofind, vea [conectar tooSQL Data Warehouse][Connect tooSQL Data Warehouse].

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. Conectar tooyour almacenamiento de datos SQL
1. Abra SSMS.
2. Abra el Explorador de objetos. toodo, seleccione **archivo** > **conectar Explorador de objetos**.
   
    ![Explorador de objetos de SQL Server][1]
3. Rellene los campos de hello en ventana de hello conectar tooServer.
   
    ![Conectar tooServer][2]
   
   * **Nombre del servidor**. Escriba hello **nombre del servidor** ha identificado anteriormente.
   * **Autenticación**. Seleccione **Autenticación de SQL Server** o **Autenticación integrada de Active Directory**.
   * **Nombre de usuario** y **Contraseña**. Escriba el nombre de usuario y la contraseña si la autenticación de SQL Server se seleccionó anteriormente.
   * Haga clic en **Conectar**.
4. tooexplore, expanda el servidor de SQL Azure. Puede ver bases de datos de hello asociadas con el servidor de Hola. Expandir AdventureWorksDW toosee Hola tablas en la base de datos de ejemplo.
   
    ![Explorar AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a>2. Ejecución de una consulta de ejemplo
Ahora que ha sido establecida tooyour base de datos de una conexión, vamos a escribir una consulta.

1. Haga clic con el botón derecho en la base de datos en el Explorador de objetos de SQL Server.
2. Seleccione **Nueva consulta**. Se abre una nueva ventana de consulta.
   
    ![Nueva consulta][4]
3. Copie esta consulta TSQL en la ventana de consulta de hello:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Ejecutar consulta Hola. toodo, haga clic en `Execute` o use Hola después de método abreviado: `F5`.
   
    ![Ejecutar consulta][5]
5. Buscar en los resultados de la consulta de Hola. En este ejemplo, la tabla FactInternetSales de hello tiene 60398 filas.
   
    ![Resultados de la consulta][6]

## <a name="next-steps"></a>Pasos siguientes
Ahora que puede conectarse y consultar, intente [visualizar datos Hola con Power BI][visualizing hello data with PowerBI].

tooconfigure su entorno para la autenticación de Azure Active Directory, vea [autenticar tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
