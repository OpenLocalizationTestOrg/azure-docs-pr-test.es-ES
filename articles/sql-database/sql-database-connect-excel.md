---
title: aaaConnect Excel tooSQL base de datos | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconnect Microsoft Excel tooAzure SQL de base de datos en la nube de Hola. Importación de datos en Excel para la generación de informes y la exploración de datos."
services: sql-database
keywords: conectar excel toosql, importar datos tooexcel
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 0048849432023145bd1009d45b6d9b64a9c7ac3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a>Conectar la base de datos de SQL de Azure de tooan de Excel y crear un informe

Conectar la base de datos de Excel tooa SQL en la nube de hello e importar datos y crear tablas y gráficos basados en los valores de la base de datos de Hola. En este tutorial que establecerá la conexión de hello entre Excel y una tabla de base de datos, guardar archivo de Hola que almacena información de conexión de hello y datos de Excel y, a continuación, crear un gráfico dinámico de hello valores de base de datos.

Antes de comenzar, necesitará una Base de datos SQL en Azure. Si no tiene uno, vea [crear la primera base de datos SQL](sql-database-get-started-portal.md) tooget una base de datos con datos de ejemplo activos y en funcionamiento en unos minutos. En este artículo se importarán los datos de ejemplo en Excel de dicho artículo, pero puede seguir los pasos con sus propios datos.

También necesitará una copia de Excel. Este artículo usa [Microsoft Excel 2016](https://products.office.com/).

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a>Conectar la base de datos de Excel tooa SQL y crear un archivo odc
1. tooconnect base de datos de tooSQL de Excel, abra Excel y, a continuación, crear un nuevo libro o abra un libro de Excel existente.
2. En la barra de menús de hello al principio de Hola de página de hello, haga clic en **datos**, haga clic en **desde otros orígenes**y, a continuación, haga clic en **de SQL Server**.
   
   ![Seleccionar origen de datos: conectar la base de datos de Excel tooSQL.](./media/sql-database-connect-excel/excel_data_source.png)
   
   Hola Asistente para la conexión de datos se abre.
3. Hola **conectar tooDatabase Server** cuadro de diálogo, Hola de tipo base de datos SQL **nombre del servidor** desea tooconnect tooin Hola forma <*servername* > **. database.windows.net**. Por ejemplo, **adworkserver.database.windows.net**.
4. En **las credenciales de inicio de sesión**, haga clic en **Hola de uso después de nombre de usuario y contraseña**, Hola de tipo **nombre de usuario** y **contraseña** configurado para Hola servidor de base de datos SQL cuando se creó y, a continuación, haga clic en **siguiente**.
   
   ![Escriba las credenciales de inicio de sesión y nombre de servidor de Hola](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > Dependiendo de su entorno de red, es posible no que pueda tooconnect o puede perder la conexión de hello si el servidor de base de datos SQL de hello no permite el tráfico desde la dirección IP del cliente. Vaya toohello [portal de Azure](https://portal.azure.com/), haga clic en servidores SQL Server, haga clic en el servidor, haga clic en firewall en la configuración y agregue la dirección IP del cliente. Vea [la configuración del firewall tooconfigure](sql-database-configure-firewall-settings.md) para obtener más información.
   > 
   > 
5. Hola **Seleccionar base de datos y tabla** cuadro de diálogo, la base de datos de hello select que desee toowork con de lista de hello y, a continuación, haga clic en las tablas de Hola o vistas que desee toowork con (elegimos **vGetAllCategories**) y, a continuación, Haga clic en **siguiente**.
   
    ![Selección de una base de datos y una tabla.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    Hola **Guardar archivo de conexión de datos y finalizar** abre el cuadro de diálogo, donde se proporciona información sobre el archivo de conexión (*.odc) de base de datos de Office de Hola que utiliza Excel. Puede dejar los valores predeterminados de Hola o personalizar las selecciones.
6. Puede dejar los valores predeterminados de hello, pero Hola Nota **nombre de archivo** en particular. A **descripción**, **Nombre_descriptivo**, y **palabras clave de búsqueda** ayudarle y recordar a otros usuarios que se está conectando tooand encontrar Hola de conexiones. Haga clic en **siempre intenta realizar toouse este archivo de datos de toorefresh** si desea que la información de conexión almacenada en el archivo odc de hello, de modo que puede actualizar cuando se conecta tooit y, a continuación, haga clic en **finalizar**.
   
    ![Almacenamiento de un archivo odc](./media/sql-database-connect-excel/save-odc-file.png)
   
    Hola **importar datos** aparece el cuadro de diálogo.

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a>Importar datos de hello en Excel y crear un gráfico dinámico
Ahora que ha establecido conexión de Hola y el archivo de hello creado con la información de conexión y de datos, está leyendo datos de hello tooimport.

1. Hola **importar datos** cuadro de diálogo, haga clic en la opción de Hola que desee para presentar los datos en la hoja de cálculo de hello y, a continuación, haga clic en **Aceptar**. Elegimos **Gráfico dinámico**. También puede elegir toocreate una **nueva hoja de cálculo** o demasiado**agregar este modelo de datos de datos tooa**. Para más información sobre los modelos de datos, consulte [Crear un modelo de datos en Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B). Haga clic en **propiedades** tooexplore información sobre el archivo odc de Hola que creó en hello anteriores paso y toochoose las opciones para actualizar los datos de Hola.
   
    ![Elegir formato de Hola para los datos en Excel](./media/sql-database-connect-excel/import-data.png)
   
    hoja de cálculo de Hello tiene ahora una tabla dinámica vacío y el gráfico.
2. En **PivotTable Fields**, seleccione todas las casillas de verificación de Hola Hola campos que desee tooview.
   
    ![Configuración de informe de base de datos.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> Si desea tooconnect otro libros y hojas de cálculo toohello base de datos Excel, haga clic en **datos**, haga clic en **conexiones**, haga clic en **agregar**, elegir conexión de Hola que creó en lista de hello y, a continuación, haga clic en **abiertos**.
> ![Apertura de una conexión desde otro libro](./media/sql-database-connect-excel/open-from-another-workbook.png)
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[conectar tooSQL base de datos con SQL Server Management Studio](sql-database-connect-query-ssms.md) para consultar y análisis avanzados.
* Obtenga información acerca de las ventajas de Hola de [grupos elásticos](sql-database-elastic-pool.md).
* Obtenga información acerca de cómo demasiado[crear una aplicación web que se conecta tooSQL base de datos en hello back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).

