---
title: "Lección 10 del tutorial de Azure Analysis Services: Creación de particiones | Microsoft Docs"
description: "Describe cómo crear particiones en el proyecto del tutorial de Azure Analysis Services."
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
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: df74d9cbdcf4916c24955e491767589e72389155
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-10-create-partitions"></a><span data-ttu-id="42412-103">Lección 10: Creación de particiones</span><span class="sxs-lookup"><span data-stu-id="42412-103">Lesson 10: Create partitions</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="42412-104">En esta lección creará particiones para dividir la tabla FactInternetSales en partes lógicas más pequeñas que se puedan procesar (actualizar) de manera independiente de otras particiones.</span><span class="sxs-lookup"><span data-stu-id="42412-104">In this lesson, you create partitions to divide the FactInternetSales table into smaller logical parts that can be processed (refreshed) independent of other partitions.</span></span> <span data-ttu-id="42412-105">De forma predeterminada, todas las tablas que incluya en el modelo tienen una partición, que incluye todas las columnas y las filas de la tabla.</span><span class="sxs-lookup"><span data-stu-id="42412-105">By default, every table you include in your model has one partition, which includes all the table’s columns and rows.</span></span> <span data-ttu-id="42412-106">En el caso de la tabla FactInternetSales, queremos dividir los datos por año: una partición para cada uno de los cinco años de la tabla.</span><span class="sxs-lookup"><span data-stu-id="42412-106">For the FactInternetSales table, we want to divide the data by year; one partition for each of the table’s five years.</span></span> <span data-ttu-id="42412-107">Así, cada partición se podrá procesar de manera independiente.</span><span class="sxs-lookup"><span data-stu-id="42412-107">Each partition can then be processed independently.</span></span> <span data-ttu-id="42412-108">Para obtener más información, consulte [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular) (Particiones).</span><span class="sxs-lookup"><span data-stu-id="42412-108">To learn more, see [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span></span> 
  
<span data-ttu-id="42412-109">Tiempo estimado para completar esta lección: **15 minutos**</span><span class="sxs-lookup"><span data-stu-id="42412-109">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="42412-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="42412-110">Prerequisites</span></span>  
<span data-ttu-id="42412-111">Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden.</span><span class="sxs-lookup"><span data-stu-id="42412-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="42412-112">Antes de llevar a cabo las tareas de esta lección, debe haber finalizado la lección anterior: [Lección 9: Creación de jerarquías](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="42412-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 9: Create Hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>  
  
## <a name="create-partitions"></a><span data-ttu-id="42412-113">Creación de particiones</span><span class="sxs-lookup"><span data-stu-id="42412-113">Create partitions</span></span>  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a><span data-ttu-id="42412-114">Para crear particiones en la tabla FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="42412-114">To create partitions in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="42412-115">En el Explorador de modelos tabulares, expanda **Tablas** y haga clic con el botón derecho en **FactInternetSales** > **Particiones**.</span><span class="sxs-lookup"><span data-stu-id="42412-115">In Tabular Model Explorer, expand **Tables**, and then right-click **FactInternetSales** > **Partitions**.</span></span>  
  
2.  <span data-ttu-id="42412-116">En el Administrador de particiones, haga clic en **Copiar** y cambie el nombre por **FactInternetSales2010**.</span><span class="sxs-lookup"><span data-stu-id="42412-116">In Partition Manager, click **Copy**, and then change the name to **FactInternetSales2010**.</span></span>
  
    <span data-ttu-id="42412-117">Como quiere que la partición incluya solo las filas de un período determinado (para el año 2010), debe modificar la expresión de consulta.</span><span class="sxs-lookup"><span data-stu-id="42412-117">Because you want the partition to include only those rows within a certain period, for the year 2010, you must modify the query expression.</span></span>
  
4.  <span data-ttu-id="42412-118">Haga clic en **Diseño** para abrir el Editor de consultas y, luego, haga clic en la consulta **FactInternetSales2010**.</span><span class="sxs-lookup"><span data-stu-id="42412-118">Click **Design** to open Query Editor, and then click the **FactInternetSales2010** query.</span></span>

5.  <span data-ttu-id="42412-119">En la vista previa, haga clic en la flecha hacia abajo del encabezado de columna **OrderDate** y haga clic en **Filtros de fecha y hora** > **Entre**.</span><span class="sxs-lookup"><span data-stu-id="42412-119">In preview, click the down arrow in the **OrderDate** column heading, and then click **Date/Time Filters** > **Between**.</span></span>

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  <span data-ttu-id="42412-121">En el cuadro de diálogo Filtrar filas, en **Mostrar filas donde: OrderDate**, deje **posterior a o igual que** y, en el campo de fecha, escriba **1/1/2010**.</span><span class="sxs-lookup"><span data-stu-id="42412-121">In the Filter Rows dialog box, in **Show rows where: OrderDate**, leave **is after or equal to**, and then in the date field, enter **1/1/2010**.</span></span> <span data-ttu-id="42412-122">Deje seleccionado el operador **Y**, seleccione **anterior a**; luego, en el campo de fecha, escriba **1/1/2011** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="42412-122">Leave the **And** operator selected, then select **is before**, then in the date field, enter **1/1/2011**, and then click **OK**.</span></span>

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    <span data-ttu-id="42412-124">Observe que en PASOS APLICADOS del Editor de consultas encontrará otro paso denominado Filas filtradas.</span><span class="sxs-lookup"><span data-stu-id="42412-124">Notice in Query Editor, in APPLIED STEPS, you see another step named Filtered Rows.</span></span> <span data-ttu-id="42412-125">Este filtro consiste en seleccionar solo las fechas de los pedidos de 2010.</span><span class="sxs-lookup"><span data-stu-id="42412-125">This filter is to select only order dates from 2010.</span></span>

8.  <span data-ttu-id="42412-126">Haga clic en **Import**.</span><span class="sxs-lookup"><span data-stu-id="42412-126">Click **Import**.</span></span>

    <span data-ttu-id="42412-127">En el Administrador de particiones, observe que la expresión de consulta ahora tiene una cláusula Filas filtradas adicional.</span><span class="sxs-lookup"><span data-stu-id="42412-127">In Partition Manager, notice the query expression now has an additional Filtered Rows clause.</span></span>

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    <span data-ttu-id="42412-129">Esta instrucción especifica que esta partición debe incluir solo los datos de esas filas donde el valor OrderDate está en el año 2010, tal como se especifica en la cláusula Filas filtradas.</span><span class="sxs-lookup"><span data-stu-id="42412-129">This statement specifies this partition should include only the data in those rows where the OrderDate is in the 2010 calendar year as specified in the filtered rows clause.</span></span>  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a><span data-ttu-id="42412-130">Para crear una partición para el año 2011</span><span class="sxs-lookup"><span data-stu-id="42412-130">To create a partition for the 2011 year</span></span>  
  
1.  <span data-ttu-id="42412-131">En la lista de particiones, haga clic en la partición **FactInternetSales2010** que ha creado y, luego, haga clic en **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="42412-131">In the partitions list, click the **FactInternetSales2010** partition you created, and then click **Copy**.</span></span>  <span data-ttu-id="42412-132">Cambie el nombre de la partición a **FactInternetSales2011**.</span><span class="sxs-lookup"><span data-stu-id="42412-132">Change the partition name to **FactInternetSales2011**.</span></span> 

    <span data-ttu-id="42412-133">No es necesario usar el Editor de consultas para crear otra cláusula Filas filtradas.</span><span class="sxs-lookup"><span data-stu-id="42412-133">You do not need to use Query Editor to create a new filtered rows clause.</span></span> <span data-ttu-id="42412-134">Como ha creado una copia de la consulta para el 2010, lo único que tiene que hacer es efectuar un pequeño cambio en la consulta del 2011.</span><span class="sxs-lookup"><span data-stu-id="42412-134">Because you created a copy of the query for 2010, all you need to do is make a slight change in the query for 2011.</span></span>
  
2.  <span data-ttu-id="42412-135">En **Expresión de consulta**, para que esta partición incluya solo las filas del año 2011, reemplace los años de la cláusula Filas filtradas por **2011** y **2012**, respectivamente; así:</span><span class="sxs-lookup"><span data-stu-id="42412-135">In **Query Expression**, in-order for this partition to include only those rows for the 2011 year, replace the years in the Filtered Rows clause with **2011** and **2012**, respectively, like:</span></span>  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="to-create-partitions-for-2012-2013-and-2014"></a><span data-ttu-id="42412-136">Para crear particiones para los años 2012, 2013 y 2014</span><span class="sxs-lookup"><span data-stu-id="42412-136">To create partitions for 2012, 2013, and 2014.</span></span>  
  
- <span data-ttu-id="42412-137">Siga los pasos anteriores (creación de particiones para los años 2012, 2013 y 2014, y cambio de los años en la cláusula Filas filtradas) para incluir solo las filas correspondientes a ese año.</span><span class="sxs-lookup"><span data-stu-id="42412-137">Follow the previous steps, creating partitions for 2012, 2013, and 2014, changing the years in the Filtered Rows clause to include only rows for that year.</span></span> 
  

## <a name="delete-the-factinternetsales-partition"></a><span data-ttu-id="42412-138">Eliminar la partición FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="42412-138">Delete the FactInternetSales partition</span></span>
<span data-ttu-id="42412-139">Ahora que tiene particiones para cada año, puede eliminar la partición FactInternetSales. Procure que no se produzca ninguna superposición al elegir Procesar todo para procesar las particiones.</span><span class="sxs-lookup"><span data-stu-id="42412-139">Now that you have partitions for each year, you can delete the FactInternetSales partition; preventing overlap when choosing Process all when processing partitions.</span></span>

#### <a name="to-delete-the-factinternetsales-partition"></a><span data-ttu-id="42412-140">Para eliminar la partición FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="42412-140">To delete the FactInternetSales partition</span></span>
-  <span data-ttu-id="42412-141">Haga clic en la partición FactInternetSales y haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="42412-141">Click the FactInternetSales partition, and then click **Delete**.</span></span>



## <a name="process-partitions"></a><span data-ttu-id="42412-142">Procesar las particiones</span><span class="sxs-lookup"><span data-stu-id="42412-142">Process partitions</span></span>  
<span data-ttu-id="42412-143">En el Administrador de particiones, observe que en la columna **Procesado por última vez** de cada una de las nuevas particiones que ha creado se muestra que estas particiones nunca se han procesado.</span><span class="sxs-lookup"><span data-stu-id="42412-143">In Partition Manager, notice the **Last Processed** column for each of the new partitions you created shows these partitions have never been processed.</span></span> <span data-ttu-id="42412-144">Al crear particiones debe ejecutar la operación Procesar particiones o Procesar tabla para actualizar los datos de esas particiones.</span><span class="sxs-lookup"><span data-stu-id="42412-144">When you create partitions, you should run a Process Partitions or Process Table operation to refresh the data in those partitions.</span></span>  
  
#### <a name="to-process-the-factinternetsales-partitions"></a><span data-ttu-id="42412-145">Para procesar las particiones FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="42412-145">To process the FactInternetSales partitions</span></span>  
  
1.  <span data-ttu-id="42412-146">Haga clic en **Aceptar** para cerrar el Administrador de particiones.</span><span class="sxs-lookup"><span data-stu-id="42412-146">Click **OK** to close Partition Manager.</span></span>  
  
2.  <span data-ttu-id="42412-147">Haga clic en la tabla **FactInternetSales** y, luego, haga clic en el menú **Modelo** > **Proceso** > **Procesar particiones**.</span><span class="sxs-lookup"><span data-stu-id="42412-147">Click the **FactInternetSales** table, then click the **Model** menu > **Process** > **Process Partitions**.</span></span>  
  
3.  <span data-ttu-id="42412-148">En el cuadro de diálogo Procesar particiones, compruebe que **Modo** está establecido en **Proceso predeterminado**.</span><span class="sxs-lookup"><span data-stu-id="42412-148">In the Process Partitions dialog box, verify **Mode** is set to **Process Default**.</span></span>  
  
4.  <span data-ttu-id="42412-149">Seleccione la casilla de la columna **Proceso** de cada una de las cinco particiones que ha creado y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="42412-149">Select the checkbox in the **Process** column for each of the five partitions you created, and then click **OK**.</span></span>  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    <span data-ttu-id="42412-151">Si se le piden las credenciales de suplantación, escriba el nombre de usuario y la contraseña de Windows que ha especificado en la lección 2.</span><span class="sxs-lookup"><span data-stu-id="42412-151">If you're prompted for Impersonation credentials, enter the Windows user name and password you specified in Lesson 2.</span></span>  
  
    <span data-ttu-id="42412-152">Aparece el cuadro de diálogo **Procesamiento de datos**, en el que se muestran los detalles del proceso de cada partición.</span><span class="sxs-lookup"><span data-stu-id="42412-152">The **Data Processing** dialog box appears and displays process details for each partition.</span></span> <span data-ttu-id="42412-153">Tenga en cuenta que se transfiere un número de filas diferente para cada partición.</span><span class="sxs-lookup"><span data-stu-id="42412-153">Notice that a different number of rows for each partition are transferred.</span></span> <span data-ttu-id="42412-154">Cada partición incluye solamente las filas del año especificado en la cláusula WHERE de la instrucción SQL.</span><span class="sxs-lookup"><span data-stu-id="42412-154">Each partition includes only those rows for the year specified in the WHERE clause in the SQL Statement.</span></span> <span data-ttu-id="42412-155">Cuando el procesamiento haya finalizado, continúe y cierre el cuadro de diálogo Procesamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="42412-155">When processing is finished, go ahead and close the Data Processing dialog box.</span></span>  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a><span data-ttu-id="42412-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="42412-157">What's next?</span></span>
<span data-ttu-id="42412-158">Vaya a la siguiente lección: [Lección 11: Creación de roles](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="42412-158">Go to the next lesson: [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md).</span></span> 
