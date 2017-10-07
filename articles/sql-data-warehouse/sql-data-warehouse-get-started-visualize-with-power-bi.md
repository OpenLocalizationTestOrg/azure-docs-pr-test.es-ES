---
title: aaaVisualize datos de almacenamiento de datos de SQL con Microsoft Azure de Power BI
description: "Visualización de datos de Almacenamiento de datos SQL con Power BI"
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a>Visualización de datos con Power BI
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Este tutorial muestra cómo toouse Power BI tooconnect tooSQL almacenamiento de datos y crear unas visualizaciones básicas.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a>Requisitos previos
toostep a través de este tutorial, necesitará:

* Un almacén de datos de SQL previamente cargados con base de datos de hello AdventureWorksDW. tooprovision, vea [crear un almacén de datos de SQL] [ Create a SQL Data Warehouse] y elegir los datos de ejemplo de Hola tooload. Si ya tiene un almacenamiento de datos pero no tiene datos de ejemplo, puede [cargar manualmente los datos de ejemplo][load sample data manually].

## <a name="1-connect-tooyour-database"></a>1. Conectar la base de datos de tooyour
tooopen Power BI y conectar la base de datos de AdventureWorksDW tooyour:

1. Inicio de sesión en hello [portal de Azure][Azure portal].
2. Haga clic en **Bases de datos SQL** y elija su base de datos de Almacenamiento de datos SQL de AdventureWorks.
   
    ![Buscar la base de datos][1]
3. Haga clic en el botón 'Abrir en Power BI' hello.
   
    ![Botón Power BI][2]
4. Ahora debería ver la página de conexión de almacenamiento de datos SQL de hello mostrar la dirección web de base de datos. Haga clic en Siguiente.
   
    ![Conexión de Power BI][3]
5. Escriba el nombre de usuario de Azure SQL server y la contraseña y será la base de datos de almacenamiento de datos SQL de tooyour conectados de forma continua.
   
    ![Inicio de sesión de Power BI][4]
6. Una vez que han iniciado sesión en Power BI, haga clic en conjunto de datos de hello AdventureWorksDW en hoja izquierdo Hola. Se abrirá la base de datos de Hola.
   
    ![Apertura de AdventureWorksDW en Power BI][5]

## <a name="2-create-a-report"></a>2. Creación de un informe
Se está ahora listo toouse Power BI tooanalyze los datos de ejemplo AdventureWorksDW. análisis de hello tooperform, AdventureWorksDW tiene una vista denominada AggregateSales. Esta vista contiene algunas de las métricas clave de Hola para análisis de ventas de Hola de empresa de Hola.

1. toocreate un mapa del importe de ventas según el código de toopostal, en el panel de la derecha de campos de hello, haga clic en hello AggregateSales vista tooexpand se. Haga clic en tooselect de hello PostalCode y SalesAmount columnas ellos.
   
    ![Selección de AggregateSales en Power BI][6]
   
    Power BI reconoce automáticamente estos datos como geográficos y los coloca en un mapa.
   
    ![Mapa Power BI][7]
2. Este paso crea un gráfico de barras que muestra la cantidad de ventas por los ingresos del cliente. toocreate este toohello vaya expandido AggregateSales vista. Haga clic en el campo SalesAmount Hola. Arrastre hacia la izquierda Hola ingresos de los clientes campo toohello y colóquelo en el eje.
   
    ![Selección del eje en Power BI][8]
   
    Gráfico de barras de Hola se mueve sobre Hola izquierda.
   
    ![Barra Power BI][9]
3. Este paso crea un gráfico de líneas que muestra el importe de ventas por fecha de pedido. toocreate este toohello vaya expandido AggregateSales vista. Haga clic en SalesAmount y OrderDate. En la columna de visualizaciones de hello haga clic en el icono de gráfico de líneas de hello; Esto es primer icono de hello en la segunda línea de hello en visualizaciones.
   
    ![Selección del gráfico de líneas de Power BI][10]
   
    Ahora tiene un informe que muestra tres diferentes visualizaciones de datos de Hola.
   
    ![LíneaPower BI][11]

Para guardar el progreso en cualquier momento, haga clic en **Archivo** y seleccione **Guardar**.

## <a name="next-steps"></a>Pasos siguientes
Ahora que hemos dado algunos toowarm tiempo con datos de ejemplo de Hola, vea cómo demasiado[desarrollar][develop], [cargar][load], o [ migrar][migrate]. O eche un vistazo a hello [sitio Web de Power BI][Power BI website].

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
