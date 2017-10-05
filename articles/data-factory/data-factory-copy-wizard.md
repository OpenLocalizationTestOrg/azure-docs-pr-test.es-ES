---
title: "Copia fácil de datos con el Asistente para copia - Azure | Microsoft Docs"
description: "Obtenga información sobre cómo utilizar el Asistente para copia de Data Factory para copiar datos de orígenes de datos admitidos en receptores."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f904972f-cd33-48db-9755-2b3196ae4168
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 282cb4484f8209e6bb36f2a02d7a897f1ba0aa8e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="copy-or-move-data-easily-with-azure-data-factory-copy-wizard"></a><span data-ttu-id="648bb-103">Copia o movimiento sencillos de datos con el Asistente para copia de Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="648bb-103">Copy or move data easily with Azure Data Factory Copy Wizard</span></span>
<span data-ttu-id="648bb-104">El Asistente para copia de factoría de datos de Azure se usa para simplificar el proceso de ingesta de datos, que normalmente es el primer paso en un escenario de integración de datos de un extremo a otro.</span><span class="sxs-lookup"><span data-stu-id="648bb-104">The Azure Data Factory Copy Wizard is to ease the process of ingesting data, which is usually a first step in an end-to-end data integration scenario.</span></span> <span data-ttu-id="648bb-105">Para aprender el uso del Asistente para copia de Azure Data Factory no es preciso conocer las definiciones de JSON de servicios vinculados, conjuntos de datos y canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="648bb-105">When going through the Azure Data Factory Copy Wizard, you do not need to understand any JSON definitions for linked services, datasets, and pipelines.</span></span> <span data-ttu-id="648bb-106">Sin embargo, después de completar todos los pasos del asistente, este crea automáticamente una canalización para copiar datos del origen de datos seleccionado al destino seleccionado.</span><span class="sxs-lookup"><span data-stu-id="648bb-106">However, after you complete all the steps in the wizard, the wizard automatically creates a pipeline to copy data from the selected data source to the selected destination.</span></span> <span data-ttu-id="648bb-107">Además, el Asistente para copia ayuda a validar los datos que se van a ingerir en el momento de creación, lo que ahorra mucho tiempo, especialmente la primera vez que se van a ingerir datos del origen de datos.</span><span class="sxs-lookup"><span data-stu-id="648bb-107">In addition, the Copy Wizard helps you to validate the data being ingested at the time of authoring, which saves much of your time, especially when you are ingesting data for the first time from the data source.</span></span> <span data-ttu-id="648bb-108">Si quiere iniciar el Asistente para copia, haga clic en el icono **Copiar datos** de la página principal de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="648bb-108">To start the Copy Wizard, click the **Copy data** tile on the home page of your data factory.</span></span>

![Asistente para copia](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="an-intuitive-wizard-for-copying-data"></a><span data-ttu-id="648bb-110">Un asistente intuitivo para copiar datos</span><span class="sxs-lookup"><span data-stu-id="648bb-110">An intuitive wizard for copying data</span></span>
<span data-ttu-id="648bb-111">Este asistente permite mover fácilmente los datos de una gran variedad de orígenes a distintos destinos en cuestión de minutos.</span><span class="sxs-lookup"><span data-stu-id="648bb-111">This wizard allows you to easily move data from a wide variety of sources to destinations in minutes.</span></span> <span data-ttu-id="648bb-112">Después de pasar por el asistente, se crea automáticamente una canalización con una actividad de copia, junto con las entidades de Data Factory dependientes (servicios vinculados y conjuntos de datos).</span><span class="sxs-lookup"><span data-stu-id="648bb-112">After going through the wizard, a pipeline with a copy activity is automatically created for you along with dependent Data Factory entities (linked services and datasets).</span></span> <span data-ttu-id="648bb-113">No se requieren más pasos para crear la canalización.</span><span class="sxs-lookup"><span data-stu-id="648bb-113">No additional steps are required to create the pipeline.</span></span>   

![Selección de origen de datos](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> <span data-ttu-id="648bb-115">Para ver instrucciones detalladas para crear una canalización de ejemplo para copiar datos desde un Azure blob a una tabla de Azure SQL Database, consulte el artículo [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="648bb-115">See [Copy Wizard tutorial](data-factory-copy-data-wizard-tutorial.md) article for step-by-step instructions to create a sample pipeline to copy data from an Azure blob to an Azure SQL Database table.</span></span> 
> 
> 

<span data-ttu-id="648bb-116">El asistente se ha diseñado desde el principio específicamente para los macrodatos.</span><span class="sxs-lookup"><span data-stu-id="648bb-116">The wizard is designed with big data in mind from the start.</span></span> <span data-ttu-id="648bb-117">Permite crear, de manera simple y eficiente, canalizaciones de Data Factory que muevan cientos de carpetas, archivos o tablas mediante el Asistente de copia de datos.</span><span class="sxs-lookup"><span data-stu-id="648bb-117">It is simple and efficient to author Data Factory pipelines that move hundreds of folders, files, or tables using the Copy Data wizard.</span></span> <span data-ttu-id="648bb-118">El asistente admite las tres características siguientes: vista previa de datos automática, captura y asignación de esquema, y filtrado de datos.</span><span class="sxs-lookup"><span data-stu-id="648bb-118">The wizard supports the following three features: Automatic data preview, schema capture and mapping, and filtering data.</span></span> 

## <a name="automatic-data-preview"></a><span data-ttu-id="648bb-119">Vista previa de datos automática</span><span class="sxs-lookup"><span data-stu-id="648bb-119">Automatic data preview</span></span>
<span data-ttu-id="648bb-120">El Asistente para copia permite revisar parte de los datos del origen de datos seleccionado para que pueda validar si los datos son los que desea copiar.</span><span class="sxs-lookup"><span data-stu-id="648bb-120">The copy wizard allows you to review part of the data from the selected data source for you to validate whether the data it is the right data you want to copy.</span></span> <span data-ttu-id="648bb-121">Además, si los datos de origen están en un archivo de texto, el Asistente para copia analiza dicho archivo para obtener más información sobre el esquema y los delimitadores de columna y fila automáticamente.</span><span class="sxs-lookup"><span data-stu-id="648bb-121">In addition, if the source data is in a text file, the copy wizard parses the text file to learn row and column delimiters, and schema automatically.</span></span> 

![Configuración del formato de archivo](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a><span data-ttu-id="648bb-123">Captura y asignación de esquema</span><span class="sxs-lookup"><span data-stu-id="648bb-123">Schema capture and mapping</span></span>
<span data-ttu-id="648bb-124">En algunos casos, es posible que el esquema de datos de entrada no coincida con el esquema de datos de salida.</span><span class="sxs-lookup"><span data-stu-id="648bb-124">The schema of input data may not match the schema of output data in some cases.</span></span> <span data-ttu-id="648bb-125">En este escenario, es preciso asignar columnas del esquema de origen a columnas del esquema de destino.</span><span class="sxs-lookup"><span data-stu-id="648bb-125">In this scenario, you need to map columns from the source schema to columns from the destination schema.</span></span> 

<span data-ttu-id="648bb-126">El Asistente para copia asigna automáticamente columnas del esquema de origen a columnas del esquema de destino.</span><span class="sxs-lookup"><span data-stu-id="648bb-126">The copy wizard automatically maps columns in the source schema to columns in the destination schema.</span></span> <span data-ttu-id="648bb-127">Las asignaciones se pueden invalidar mediante el uso de las listas desplegables (o) se puede especificar si una columna debe omitirse al copiar los datos.</span><span class="sxs-lookup"><span data-stu-id="648bb-127">You can override the mappings by using the drop-down lists (or) specify whether a column needs to be skipped while copying the data.</span></span>   

![Asignación de esquemas](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a><span data-ttu-id="648bb-129">Filtrado de datos</span><span class="sxs-lookup"><span data-stu-id="648bb-129">Filtering data</span></span>
<span data-ttu-id="648bb-130">El asistente permite filtrar los datos de origen para seleccionar solo aquellos que deben copiarse en el destino o en el almacén de datos receptor.</span><span class="sxs-lookup"><span data-stu-id="648bb-130">The wizard allows you to filter source data to select only the data that needs to be copied to the destination/sink data store.</span></span> <span data-ttu-id="648bb-131">El filtrado reduce el volumen de los datos se copian en el almacén de datos del receptor, por lo que mejora el rendimiento de la operación de copia.</span><span class="sxs-lookup"><span data-stu-id="648bb-131">Filtering reduces the volume of the data to be copied to the sink data store and therefore enhances the throughput of the copy operation.</span></span> <span data-ttu-id="648bb-132">Proporciona una manera flexible de filtrar los datos de una base de datos relacional mediante el lenguaje de consulta SQL (o) archivos en una carpeta de blobs de Azure mediante [Funciones y variables de Data Factory](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="648bb-132">It provides a flexible way to filter data in a relational database by using SQL query language (or) files in an Azure blob folder by using [Data Factory functions and variables](data-factory-functions-variables.md).</span></span>   

### <a name="filtering-of-data-in-a-database"></a><span data-ttu-id="648bb-133">Filtrado de datos de una base de datos</span><span class="sxs-lookup"><span data-stu-id="648bb-133">Filtering of data in a database</span></span>
<span data-ttu-id="648bb-134">En el ejemplo, la consulta SQL usa la función `Text.Format` y la variable `WindowStart`.</span><span class="sxs-lookup"><span data-stu-id="648bb-134">In the example, the SQL query uses the `Text.Format` function and `WindowStart` variable.</span></span> 

![Validación de expresiones](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a><span data-ttu-id="648bb-136">Filtrar datos en una carpeta de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="648bb-136">Filtering of data in an Azure blob folder</span></span>
<span data-ttu-id="648bb-137">Puede usar variables en la ruta de acceso de la carpeta para copiar datos desde una carpeta que se determina en el runtime según las [variables del sistema](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="648bb-137">You can use variables in the folder path to copy data from a folder that is determined at runtime based on [system variables](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="648bb-138">Estas son las variables que se admiten: **{year}**, **{month}**, **{day}**, **{hour}**, **{minute}** y **{custom}**.</span><span class="sxs-lookup"><span data-stu-id="648bb-138">The supported variables are: **{year}**, **{month}**, **{day}**, **{hour}**, **{minute}**, and **{custom}**.</span></span> <span data-ttu-id="648bb-139">Ejemplo: carpetaDeEntrada/{year}/{month}/{day}.</span><span class="sxs-lookup"><span data-stu-id="648bb-139">Example: inputfolder/{year}/{month}/{day}.</span></span>

<span data-ttu-id="648bb-140">Supongamos que tiene carpetas de entrada con el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="648bb-140">Suppose that you have input folders in the following format:</span></span>

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

<span data-ttu-id="648bb-141">Haga clic en el botón **Examinar** de **Archivo o carpeta**, vaya a una de estas carpetas (por ejemplo, 2016->03->01->02) y haga clic en **Elegir**.</span><span class="sxs-lookup"><span data-stu-id="648bb-141">Click the **Browse** button for **File or folder**, browse to one of these folders (for example, 2016->03->01->02), and click **Choose**.</span></span> <span data-ttu-id="648bb-142">En el cuadro de texto, debería aparecer `2016/03/01/02`.</span><span class="sxs-lookup"><span data-stu-id="648bb-142">You should see `2016/03/01/02` in the text box.</span></span> <span data-ttu-id="648bb-143">Sustituya **2016** por **{year}**, **03** por **{month}**, **01** por **{day}** y **02** por **{hour}** y presione la tecla TAB.</span><span class="sxs-lookup"><span data-stu-id="648bb-143">Now, replace **2016** with **{year}**, **03** with **{month}**, **01** with **{day}**, and **02** with **{hour}**, and press Tab.</span></span> <span data-ttu-id="648bb-144">Aparecerán listas desplegables en las que podrá seleccionar el formato de estas cuatro variables:</span><span class="sxs-lookup"><span data-stu-id="648bb-144">You should see drop-down lists to select the format for these four variables:</span></span>

![Uso de variables del sistema](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

<span data-ttu-id="648bb-146">Como se muestra en la siguiente captura de pantalla, también puede usar una variable **personalizada** y cualquier [cadena de formato admitida](https://msdn.microsoft.com/library/8kb3ddd4.aspx).</span><span class="sxs-lookup"><span data-stu-id="648bb-146">As shown in the following screenshot, you can also use a **custom** variable and any [supported format strings](https://msdn.microsoft.com/library/8kb3ddd4.aspx).</span></span> <span data-ttu-id="648bb-147">Para seleccionar una carpeta con esa estructura, utilice primero el botón **Examinar** .</span><span class="sxs-lookup"><span data-stu-id="648bb-147">To select a folder with that structure, use the **Browse** button first.</span></span> <span data-ttu-id="648bb-148">A continuación, reemplace un valor por **{custom}**y presione la tecla Tabulación para ver el cuadro de texto donde puede escribir la cadena de formato.</span><span class="sxs-lookup"><span data-stu-id="648bb-148">Then replace a value with **{custom}**, and press Tab to see the text box where you can type the format string.</span></span>     

![Uso de la variable personalizada](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="support-for-diverse-data-and-object-types"></a><span data-ttu-id="648bb-150">Compatibilidad con distintos tipos de objetos y datos</span><span class="sxs-lookup"><span data-stu-id="648bb-150">Support for diverse data and object types</span></span>
<span data-ttu-id="648bb-151">Gracias al Asistente para copia se pueden mover de manera eficaz cientos de tablas, archivos o carpetas.</span><span class="sxs-lookup"><span data-stu-id="648bb-151">By using the Copy Wizard, you can efficiently move hundreds of folders, files, or tables.</span></span>

![Selección de tablas desde las que se van a copiar datos](./media/data-factory-copy-wizard/select-tables-to-copy-data.png)

## <a name="scheduling-options"></a><span data-ttu-id="648bb-153">Opciones de programación</span><span class="sxs-lookup"><span data-stu-id="648bb-153">Scheduling options</span></span>
<span data-ttu-id="648bb-154">Puede ejecutar la operación de copia una vez o de forma periódica (cada hora, día, etc.).</span><span class="sxs-lookup"><span data-stu-id="648bb-154">You can run the copy operation once or on a schedule (hourly, daily, and so on).</span></span> <span data-ttu-id="648bb-155">Estas opciones se pueden utilizar para los distintos conectores locales y en la nube, así como para la copia del escritorio local.</span><span class="sxs-lookup"><span data-stu-id="648bb-155">Both of these options can be used for the breadth of the connectors across on-premises, cloud, and local desktop copy.</span></span>

<span data-ttu-id="648bb-156">Una operación de copia única permite el movimiento de datos desde un origen a un destino solamente una vez.</span><span class="sxs-lookup"><span data-stu-id="648bb-156">A one-time copy operation enables data movement from a source to a destination only once.</span></span> <span data-ttu-id="648bb-157">Se aplica a los datos de cualquier tamaño y en cualquier formato admitido.</span><span class="sxs-lookup"><span data-stu-id="648bb-157">It applies to data of any size and any supported format.</span></span> <span data-ttu-id="648bb-158">La copia programada permite copiar datos con una frecuencia prescrita.</span><span class="sxs-lookup"><span data-stu-id="648bb-158">The scheduled copy allows you to copy data on a prescribed recurrence.</span></span> <span data-ttu-id="648bb-159">Puede utilizar las opciones avanzadas (como el reintento, el tiempo de espera y las alertas) para configurar la copia programada.</span><span class="sxs-lookup"><span data-stu-id="648bb-159">You can use rich settings (like retry, timeout, and alerts) to configure the scheduled copy.</span></span>

![Propiedades de programación](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a><span data-ttu-id="648bb-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="648bb-161">Next steps</span></span>
<span data-ttu-id="648bb-162">Si quiere ver un tutorial rápido sobre el uso del Asistente para copia de Data Factory a fin de crear una canalización con una actividad de copia, consulte [Tutorial: crear una canalización con la actividad de copia mediante el Asistente para copia de Data Factory](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="648bb-162">For a quick walkthrough of using the Data Factory Copy Wizard to create a pipeline with Copy Activity, see [Tutorial: Create a pipeline using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>
