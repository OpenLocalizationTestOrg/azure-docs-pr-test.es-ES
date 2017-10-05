---
title: "Lección 2 del tutorial de Azure Analysis Services: Obtención de datos | Microsoft Docs"
description: "Describe cómo obtener e importar datos en el proyecto del tutorial de Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: e77de4b9a74b528fa8a7ce86424fc14628b2cacc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-2-get-data"></a>Lección 2: Obtención de datos

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

En esta lección, usará Obtención de datos en SSDT para conectarse a la base de datos de ejemplo AdventureWorksDW2014, seleccionar datos, obtener una vista previa, filtrar e importar en el área de trabajo del modelo.  
  
Al usar Obtención de datos, puede importar datos de diversos de orígenes: Azure SQL Database, Oracle, Sybase, fuente OData, Teradata, archivos y mucho más. También puede consultar datos mediante una expresión de fórmula de Power Query M.
  
Tiempo estimado para completar esta lección: **10 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 1: Creación de un proyecto de modelo tabular](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Crear una conexión  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw2014-database"></a>Para crear una conexión a la base de datos AdventureWorksDW2014  
  
1.  En el Explorador de modelos tabulares, haga clic con el botón derecho en **Orígenes de datos** > **Importar desde el origen de datos**.  
  
    De este modo se inicia Obtención de datos, que le guiará por el proceso de conexión a un origen de datos. Si no ve el Explorador de modelos tabulares, en el **Explorador de soluciones**, haga doble clic en **Model.bim** para abrir el modelo en el diseñador. 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  En Obtención de datos, haga clic en **Base de datos** > **Base de datos de SQL Server** > **Conectar**.  
  
3.  En el cuadro de diálogo **Base de datos de SQL Server**, en **Servidor**, escriba el nombre del servidor en el que ha instalado la base de datos AdventureWorksDW2014 y haga clic en **Conectar**.  

4.  Cuando se le pida que escriba las credenciales, debe especificar las credenciales que Analysis Services usa para conectarse al origen de datos al importar y procesar datos. En **Modo de suplantación**, seleccione **Suplantar cuenta**, escriba las credenciales y haga clic en **Conectar**. Se recomienda que use una cuenta cuya contraseña no expire.

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > El uso de una cuenta de usuario y contraseña de Windows proporciona el método más seguro de conectarse a un origen de datos.
  
5.  En el navegador, seleccione la base de datos **AdventureWorksDW2014** y haga clic en **Aceptar**. De este modo, se crea la conexión con la base de datos. 
  
6.  En el navegador, active la casilla de las tablas siguientes: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory** y **FactInternetSales**.  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
Después de hacer clic en Aceptar, se abre el Editor de consultas. En la sección siguiente, seleccione solo los datos que desea importar.

  
## <a name="filter-the-table-data"></a>Filtrar los datos de tabla  
Las tablas de la base de datos de ejemplo AdventureWorksDW2014 contienen datos que no es necesario incluir en el modelo. Siempre que sea posible, le interesa filtrar los datos que no son necesarios para ahorrar el espacio en memoria que usa el modelo. Filtre algunas de las columnas de las tablas, de modo que no se importen en la base de datos del área de trabajo o en la base de datos del modelo una vez que se haya implementado. 
  
#### <a name="to-filter-the-table-data-before-importing"></a>Para filtrar los datos de la tabla antes de importar  
  
1.  En el Editor de consultas, seleccione la tabla **DimCustomer**. Aparece una vista de la tabla DimCustomer en el origen de datos (la base de datos de ejemplo AdventureWorksDWQ2014). 
  
2.  Seleccione al mismo tiempo (Ctrl+clic) **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**, haga clic con el botón derecho y, después, haga clic en **Quitar columnas**. 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    Dado que los valores de estas columnas no son pertinentes para el análisis de ventas por Internet, no es necesario importar estas columnas. Si elimina las columnas innecesarias, el modelo será más pequeño y eficaz.  
  
4.  Elimine las siguientes columnas de cada tabla para filtrar las tablas restantes:  
    
    **DimDate**
    
      |Columna|  
      |--------|  
      |DateKey|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |Columna|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |Columna|  
      |-----------|  
      |**SpanishProductName**|  
      |**FrenchProductName**|  
      |**FrenchDescription**|  
      |**ChineseDescription**|  
      |**ArabicDescription**|  
      |**HebrewDescription**|  
      |**ThaiDescription**|  
      |**GermanDescription**|  
      |**JapaneseDescription**|  
      |**TurkishDescription**|  
  
    **DimProductCategory**
  
      |Columna|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |Columna|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |Columna|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Importar las tablas y los datos de columna seleccionados  
Ahora que ha obtenido una vista previa y ha filtrado los datos innecesarios, puede importar los datos que quiera. El asistente importa los datos de las tablas junto con las relaciones entre las tablas. Se crean nuevas tablas y columnas en el modelo y no se importan los datos filtrados.  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>Para importar las tablas y los datos de columna seleccionados  
  
1.  Revise lo que ha seleccionado. Si todo es correcto, haga clic en **Importar**. En el cuadro de diálogo Procesamiento de datos se muestra el estado de los datos que se van a importar del origen de datos en la base de datos del área de trabajo.
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  Haga clic en **Cerrar**.  

  
## <a name="save-your-model-project"></a>Guardar el proyecto de modelo  
Es importante que guarde con frecuencia el proyecto de modelo.  
  
#### <a name="to-save-the-model-project"></a>Para guardar el proyecto de modelo  
  
-   Haga clic en **Archivo** > **Guardar todo**.  
  
## <a name="whats-next"></a>Pasos siguientes
[Lección 3: Marcado como tabla de fechas](../tutorials/aas-lesson-3-mark-as-date-table.md)

  
  
