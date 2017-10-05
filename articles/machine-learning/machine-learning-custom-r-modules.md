---
title: "Creación de módulos R personalizados en Azure Machine Learning | Microsoft Docs"
description: "Inicio rápido para la creación de módulos R personalizados en Aprendizaje automático de Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 964ddb551a475243891abce8a2b835e65569a4ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="0e030-103">Creación de módulos R personalizados en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="0e030-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="0e030-104">En este tema se describe cómo crear e implementar un módulo R personalizado en Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e030-104">This topic describes how to author and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="0e030-105">Se explica qué son los módulos R personalizados y qué archivos se usan para definirlos.</span><span class="sxs-lookup"><span data-stu-id="0e030-105">It explains what custom R modules are and what files are used to define them.</span></span> <span data-ttu-id="0e030-106">Muestra cómo construir estos archivos y cómo registrar el módulo para implementarlo en un área de trabajo de Aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="0e030-106">It illustrates how to construct the files that define a module and how to register the module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="0e030-107">Los elementos y atributos que se utilizan en la definición del módulo personalizado se describen a continuación con más detalle.</span><span class="sxs-lookup"><span data-stu-id="0e030-107">The elements and attributes used in the definition of the custom module are then described in more detail.</span></span> <span data-ttu-id="0e030-108">También se describe cómo utilizar la funcionalidad y los archivos auxiliares, y varias salidas.</span><span class="sxs-lookup"><span data-stu-id="0e030-108">How to use auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="0e030-109">¿Qué es un módulo R personalizado?</span><span class="sxs-lookup"><span data-stu-id="0e030-109">What is a custom R module?</span></span>
<span data-ttu-id="0e030-110">Un **módulo personalizado** es un módulo definido por el usuario que se puede cargar en el área de trabajo de un usuario y ejecutarlo como parte de un experimento de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e030-110">A **custom module** is a user-defined module that can be uploaded to your workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="0e030-111">Un **módulo de R personalizado** es un módulo personalizado que ejecuta una función de R definida por el usuario.</span><span class="sxs-lookup"><span data-stu-id="0e030-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="0e030-112">**R** es un lenguaje de programación de computación estadística y gráficos utilizado ampliamente por científicos estadísticos y de datos para implementar algoritmos.</span><span class="sxs-lookup"><span data-stu-id="0e030-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="0e030-113">Actualmente, R es el único lenguaje que se admite en los módulos personalizados, pero en las próximas versiones se ha programado la compatibilidad con idiomas adicionales.</span><span class="sxs-lookup"><span data-stu-id="0e030-113">Currently, R is the only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="0e030-114">Los módulos personalizados tienen un **estado de primera clase** en Aprendizaje automático de Azure, en el sentido de que se pueden usar como cualquier otro módulo.</span><span class="sxs-lookup"><span data-stu-id="0e030-114">Custom modules have **first-class status** in Azure Machine Learning in the sense that they can be used just like any other module.</span></span> <span data-ttu-id="0e030-115">Pueden ejecutarse con otros módulos e incluirse en experimentos publicados o visualizaciones.</span><span class="sxs-lookup"><span data-stu-id="0e030-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="0e030-116">Usted tiene control sobre el algoritmo implementado por el módulo, los puertos de entrada y de salida a utilizar, los parámetros de modelado y otros distintos comportamientos en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="0e030-116">You have control over the algorithm implemented by the module, the input and output ports to be used, the modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="0e030-117">En la galería de Cortana Intelligence también se puede publicar un experimento con módulos personalizados para compartirlo fácilmente.</span><span class="sxs-lookup"><span data-stu-id="0e030-117">An experiment that contains custom modules can also be published into the Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="0e030-118">Archivos de un módulo R personalizado</span><span class="sxs-lookup"><span data-stu-id="0e030-118">Files in a custom R module</span></span>
<span data-ttu-id="0e030-119">Un módulo R personalizado se define mediante un archivo .zip que contiene, como mínimo, dos archivos:</span><span class="sxs-lookup"><span data-stu-id="0e030-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="0e030-120">Un **archivo de origen** que implementa la función R expuesta por el módulo.</span><span class="sxs-lookup"><span data-stu-id="0e030-120">A **source file** that implements the R function exposed by the module</span></span>
* <span data-ttu-id="0e030-121">Un **archivo de definición XML** que describe la interfaz del módulo personalizado.</span><span class="sxs-lookup"><span data-stu-id="0e030-121">An **XML definition file** that describes the custom module interface</span></span>

<span data-ttu-id="0e030-122">También se pueden incluir archivos auxiliares adicionales en el archivo .zip que proporcionan una funcionalidad a la que se puede tener acceso desde el módulo personalizado.</span><span class="sxs-lookup"><span data-stu-id="0e030-122">Additional auxiliary files can also be included in the .zip file that provides functionality that can be accessed from the custom module.</span></span> <span data-ttu-id="0e030-123">Esta opción se describe en el apartado **Argumentos** de la sección de referencia **Elementos del archivo de definición XML** que sigue al ejemplo de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="0e030-123">This option is discussed in the **Arguments** part of the reference section **Elements in the XML definition file** following the quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="0e030-124">Ejemplo de inicio rápido: definir, empaquetar y registrar un módulo R personalizado</span><span class="sxs-lookup"><span data-stu-id="0e030-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="0e030-125">En este ejemplo se muestra cómo construir los archivos que requiere un módulo R personalizado, empaquetarlos en un archivo zip y, a continuación, registrar el módulo en un área de trabajo de Aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="0e030-125">This example illustrates how to construct the files required by a custom R module, package them into a zip file, and then register the module in your Machine Learning workspace.</span></span> <span data-ttu-id="0e030-126">Tanto el paquete zip de ejemplo como los archivos de ejemplo se pueden descargar en [Descargar el archivo CustomAddRows.zip](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="0e030-126">The example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="the-source-file"></a><span data-ttu-id="0e030-127">El archivo de origen</span><span class="sxs-lookup"><span data-stu-id="0e030-127">The source file</span></span>
<span data-ttu-id="0e030-128">Considere el ejemplo de un módulo **Custom Add Rows** (Agregar filas personalizado) que modifica la implementación estándar del módulo de **Agregar filas** que se usa para concatenar las filas (observaciones) de dos conjuntos de datos (tramas de datos).</span><span class="sxs-lookup"><span data-stu-id="0e030-128">Consider the example of a **Custom Add Rows** module that modifies the standard implementation of the **Add Rows** module used to concatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="0e030-129">El módulo **Agregar filas** estándar anexa las filas del segundo conjunto de datos de entrada al final del primer conjunto de datos de entrada mediante el algoritmo `rbind`.</span><span class="sxs-lookup"><span data-stu-id="0e030-129">The standard **Add Rows** module appends the rows of the second input dataset to the end of the first input dataset using the `rbind` algorithm.</span></span> <span data-ttu-id="0e030-130">La función `CustomAddRows` personalizada acepta dos conjuntos de datos de forma similar, pero también acepta un parámetro booleano de intercambio como entrada adicional.</span><span class="sxs-lookup"><span data-stu-id="0e030-130">The customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="0e030-131">Si el parámetro de intercambio está establecido en **FALSE**, devuelve el mismo conjunto de datos que la implementación estándar.</span><span class="sxs-lookup"><span data-stu-id="0e030-131">If the swap parameter is set to **FALSE**, it returns the same data set as the standard implementation.</span></span> <span data-ttu-id="0e030-132">Pero si el parámetro de intercambio es **TRUE**, la función anexará filas del primer conjunto de datos de entrada al final del segundo conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="0e030-132">But if the swap parameter is **TRUE**, the function appends rows of first input dataset to the end of the second dataset instead.</span></span> <span data-ttu-id="0e030-133">El archivo CustomAddRows.R que contiene la implementación de la función R `CustomAddRows` expuesta por el módulo **Agregar filas personalizado** tiene el siguiente código R.</span><span class="sxs-lookup"><span data-stu-id="0e030-133">The CustomAddRows.R file that contains the implementation of the R `CustomAddRows` function exposed by the **Custom Add Rows** module has the following R code.</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="the-xml-definition-file"></a><span data-ttu-id="0e030-134">El archivo de definición XML</span><span class="sxs-lookup"><span data-stu-id="0e030-134">The XML definition file</span></span>
<span data-ttu-id="0e030-135">Para exponer esta función `CustomAddRows` como módulo de Aprendizaje automático de Azure, se debe crear un archivo de definición XML para especificar la apariencia y comportamiento que debe tener el módulo **Agregar filas personalizado** .</span><span class="sxs-lookup"><span data-stu-id="0e030-135">To expose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created to specify how the **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset to another. Dataset 2 is concatenated to Dataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify the base language, script file and R function to use for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: The values of the id attributes in the Input and Arg elements must match the parameter names in the R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>The combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="0e030-136">Es muy importante que tenga en cuenta que el valor de los atributos **id** de los elementos **Input** y **Arg** del archivo XML deben coincidir EXACTAMENTE con los nombres de parámetro de función del código de R del archivo CustomAddRows.R: (*dataset1*, *dataset2* y *swap* en el ejemplo).</span><span class="sxs-lookup"><span data-stu-id="0e030-136">It is critical to note that the value of the **id** attributes of the **Input** and **Arg** elements in the XML file must match the function parameter names of the R code in the CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in the example).</span></span> <span data-ttu-id="0e030-137">De forma similar, el valor el atributo **entryPoint** del elemento **Language** debe coincidir EXACTAMENTE con el nombre de la función del script de R (*CustomAddRows* en el ejemplo).</span><span class="sxs-lookup"><span data-stu-id="0e030-137">Similarly, the value of the **entryPoint** attribute of the **Language** element must match the name of the function in the R script EXACTLY: (*CustomAddRows* in the example).</span></span> 

<span data-ttu-id="0e030-138">En cambio, el atributo **id** de los elementos **Output** no se corresponde con las variables del script de R.</span><span class="sxs-lookup"><span data-stu-id="0e030-138">In contrast, the **id** attribute for the **Output** element does not correspond to any variables in the R script.</span></span> <span data-ttu-id="0e030-139">Cuando se requiere más de una salida, simplemente devuelva una lista de la función de R con los resultados colocados *en el mismo orden* en que los elementos **Outputs** se declaran en el archivo XML.</span><span class="sxs-lookup"><span data-stu-id="0e030-139">When more than one output is required, simply return a list from the R function with results placed *in the same order* as **Outputs** elements are declared in the XML file.</span></span>

### <a name="package-and-register-the-module"></a><span data-ttu-id="0e030-140">Empaquetamiento y registro del módulo</span><span class="sxs-lookup"><span data-stu-id="0e030-140">Package and register the module</span></span>
<span data-ttu-id="0e030-141">Guarde estos dos archivos como *CustomAddRows.R* y *CustomAddRows.xml* y comprima los dos archivos juntos en un archivo *CustomAddRows.zip*.</span><span class="sxs-lookup"><span data-stu-id="0e030-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip the two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="0e030-142">Para registrarlos en su área de trabajo de Machine Learning, vaya al área de trabajo de Machine Learning Studio, haga clic en el botón **+NEW** (+Nuevo) de la parte inferior y elija **MODULE -> FROM ZIP PACKAGE** (Módulo -> De paquete zip) para cargar el nuevo módulo **Custom Add Rows** (Agregar filas personalizado).</span><span class="sxs-lookup"><span data-stu-id="0e030-142">To register them in your Machine Learning workspace, go to your workspace in the Machine Learning Studio, click the **+NEW** button on the bottom and choose **MODULE -> FROM ZIP PACKAGE** to upload the new **Custom Add Rows** module.</span></span>

![Cargar archivo zip](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="0e030-144">El módulo **Agregar filas personalizado** ya está preparado para que los experimentos de Aprendizaje automático tengan acceso a él.</span><span class="sxs-lookup"><span data-stu-id="0e030-144">The **Custom Add Rows** module is now ready to be accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-the-xml-definition-file"></a><span data-ttu-id="0e030-145">Elementos del archivo de definición XML</span><span class="sxs-lookup"><span data-stu-id="0e030-145">Elements in the XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="0e030-146">Elementos Module</span><span class="sxs-lookup"><span data-stu-id="0e030-146">Module elements</span></span>
<span data-ttu-id="0e030-147">El elemento **Module** se usa para definir un módulo personalizado en el archivo XML.</span><span class="sxs-lookup"><span data-stu-id="0e030-147">The **Module** element is used to define a custom module in the XML file.</span></span> <span data-ttu-id="0e030-148">Se pueden definir varios módulos en un archivo XML mediante el uso de varios elementos **Module** .</span><span class="sxs-lookup"><span data-stu-id="0e030-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="0e030-149">Cada uno de los módulos del área de trabajo debe tener un nombre único.</span><span class="sxs-lookup"><span data-stu-id="0e030-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="0e030-150">Registre un módulo personalizado con el mismo nombre que un módulo personalizado existente y reemplazará el módulo existente por otro nuevo.</span><span class="sxs-lookup"><span data-stu-id="0e030-150">Register a custom module with the same name as an existing custom module and it replaces the existing module with the new one.</span></span> <span data-ttu-id="0e030-151">Sin embargo, los módulos personalizados se pueden registrar con el mismo nombre que un módulo de Aprendizaje automático de Azure existente.</span><span class="sxs-lookup"><span data-stu-id="0e030-151">Custom modules can, however, be registered with the same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="0e030-152">Si es así, aparecerán en la categoría **Custom** de la paleta del módulo.</span><span class="sxs-lookup"><span data-stu-id="0e030-152">If so, they appear in the **Custom** category of the module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset to another...</Description>/> 


<span data-ttu-id="0e030-153">Dentro del elemento **Module** , puede especificar dos elementos opcionales adicionales:</span><span class="sxs-lookup"><span data-stu-id="0e030-153">Within the **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="0e030-154">un elemento **Owner** que está incrustado en el módulo</span><span class="sxs-lookup"><span data-stu-id="0e030-154">an **Owner** element that is embedded into the module</span></span>  
* <span data-ttu-id="0e030-155">un elemento **Description** que contiene el texto que se muestra en la ayuda rápida del módulo y cuando mantiene el puntero sobre el módulo en la interfaz de usuario de Aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="0e030-155">a **Description** element that contains text that is displayed in quick help for the module and when you hover over the module in the Machine Learning UI.</span></span>

<span data-ttu-id="0e030-156">Reglas para los límites de caracteres de los elementos Module:</span><span class="sxs-lookup"><span data-stu-id="0e030-156">Rules for characters limits in the Module elements:</span></span>

* <span data-ttu-id="0e030-157">El valor del atributo **name** del elemento **Module** no debe superar los 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="0e030-157">The value of the **name** attribute in the **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="0e030-158">El contenido del elemento **Description** no debe superar los 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="0e030-158">The content of the **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="0e030-159">El contenido del elemento **Owner** no debe superar los 32 caracteres.</span><span class="sxs-lookup"><span data-stu-id="0e030-159">The content of the **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="0e030-160">Los resultados de un módulo pueden ser deterministas o no deterministas.** De forma predeterminada, se considera que todos los módulos son deterministas.</span><span class="sxs-lookup"><span data-stu-id="0e030-160">A module's results can be deterministic or nondeterministic.** By default, all modules are considered to be deterministic.</span></span> <span data-ttu-id="0e030-161">Es decir, dado un conjunto de parámetros y datos de entrada que no cambian, el módulo debe devolver los mismos resultados cada vez que se ejecute RAND o una función.</span><span class="sxs-lookup"><span data-stu-id="0e030-161">That is, given an unchanging set of input parameters and data, the module should return the same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="0e030-162">Dado este comportamiento, Estudio de aprendizaje automático de Azure solo volverá a ejecutar los módulos marcados como deterministas si un parámetro o los datos de entrada han cambiado.</span><span class="sxs-lookup"><span data-stu-id="0e030-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or the input data has changed.</span></span> <span data-ttu-id="0e030-163">La devolución de los resultados almacenados en caché también proporciona una ejecución mucho más rápida de los experimentos.</span><span class="sxs-lookup"><span data-stu-id="0e030-163">Returning the cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="0e030-164">Hay funciones que son no deterministas, como RAND o una función que devuelve la fecha o la hora actual.</span><span class="sxs-lookup"><span data-stu-id="0e030-164">There are functions that are nondeterministic, such as RAND or a function that returns the current date or time.</span></span> <span data-ttu-id="0e030-165">Si el módulo usa una función no determinista, puede especificar que el módulo es no determinista estableciendo el atributo opcional **isDeterministic** en **FALSE**.</span><span class="sxs-lookup"><span data-stu-id="0e030-165">If your module uses a nondeterministic function, you can specify that the module is non-deterministic by setting the optional **isDeterministic** attribute to **FALSE**.</span></span> <span data-ttu-id="0e030-166">Esto garantiza que el módulo se volverá a ejecutar siempre que se ejecute el experimento, aunque la entrada y los parámetros del módulo no hayan cambiado.</span><span class="sxs-lookup"><span data-stu-id="0e030-166">This insures that the module is rerun whenever the experiment is run, even if the module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="0e030-167">Definición de lenguaje</span><span class="sxs-lookup"><span data-stu-id="0e030-167">Language Definition</span></span>
<span data-ttu-id="0e030-168">El elemento **Lenguage** del archivo de definición XML se usa para especificar el idioma del módulo personalizado.</span><span class="sxs-lookup"><span data-stu-id="0e030-168">The **Language** element in your XML definition file is used to specify the custom module language.</span></span> <span data-ttu-id="0e030-169">Actualmente, R es el único lenguaje que se admite.</span><span class="sxs-lookup"><span data-stu-id="0e030-169">Currently, R is the only supported language.</span></span> <span data-ttu-id="0e030-170">El valor del atributo **sourceFile** debe ser el nombre del archivo R que contiene la función a la que se va a llamar cuando se ejecute el módulo.</span><span class="sxs-lookup"><span data-stu-id="0e030-170">The value of the **sourceFile** attribute must be the name of the R file that contains the function to call when the module is run.</span></span> <span data-ttu-id="0e030-171">Este archivo debe formar parte del paquete zip.</span><span class="sxs-lookup"><span data-stu-id="0e030-171">This file must be part of the zip package.</span></span> <span data-ttu-id="0e030-172">El valor del atributo **entryPoint** es el nombre de la función a la que se llama y debe coincidir con una función válida que se define en el archivo de origen.</span><span class="sxs-lookup"><span data-stu-id="0e030-172">The value of the **entryPoint** attribute is the name of the function being called and must match a valid function defined with in the source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="0e030-173">Puertos</span><span class="sxs-lookup"><span data-stu-id="0e030-173">Ports</span></span>
<span data-ttu-id="0e030-174">Los puertos de entrada y salida de un módulo personalizado se especifican en los elementos secundarios de la sección **Ports** del archivo de definición XML.</span><span class="sxs-lookup"><span data-stu-id="0e030-174">The input and output ports for a custom module are specified in child elements of the **Ports** section of the XML definition file.</span></span> <span data-ttu-id="0e030-175">El orden de estos elementos determina el diseño que ven (UX) los usuarios.</span><span class="sxs-lookup"><span data-stu-id="0e030-175">The order of these elements determines the layout experienced (UX) by users.</span></span> <span data-ttu-id="0e030-176">La primera **entrada** o **salida** secundaria que aparezca en el elemento **Ports** del archivo XML se convertirá en el puerto de entrada del punto de conexión situado más a la izquierda en la experiencia de usuario de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0e030-176">The first child **input** or **output** listed in the **Ports** element of the XML file becomes the left-most input port in the Machine Learning UX.</span></span>
<span data-ttu-id="0e030-177">Cada puerto de entrada y salida puede tener un elemento secundario **Description** que especifica el texto que se muestra cuando mantiene el puntero sobre el puerto en la interfaz de usuario de Aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="0e030-177">Each input and output port may have an optional **Description** child element that specifies the text shown when you hover the mouse cursor over the port in the Machine Learning UI.</span></span>

<span data-ttu-id="0e030-178">**Reglas de puertos**:</span><span class="sxs-lookup"><span data-stu-id="0e030-178">**Ports Rules**:</span></span>

* <span data-ttu-id="0e030-179">El número máximo de **puertos de entrada y salida** es 8 para cada uno.</span><span class="sxs-lookup"><span data-stu-id="0e030-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="0e030-180">Elementos de entrada</span><span class="sxs-lookup"><span data-stu-id="0e030-180">Input elements</span></span>
<span data-ttu-id="0e030-181">Los puertos de entrada le permiten pasar datos a una función y un área de trabajo de R.</span><span class="sxs-lookup"><span data-stu-id="0e030-181">Input ports allow you to pass data to your R function and workspace.</span></span> <span data-ttu-id="0e030-182">Los **tipos de datos** que se admiten para los puertos de entrada son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="0e030-182">The **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="0e030-183">**DataTable:** este tipo se pasa a la función de R como data.frame.</span><span class="sxs-lookup"><span data-stu-id="0e030-183">**DataTable:** This type is passed to your R function as a data.frame.</span></span> <span data-ttu-id="0e030-184">De hecho, todos los tipos (por ejemplo, archivos CSV o archivos ARFF) que admite Aprendizaje automático y que son compatibles con **DataTable** se convierten automáticamente en data.frame.</span><span class="sxs-lookup"><span data-stu-id="0e030-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted to a data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="0e030-185">El atributo **id** asociado a cada puerto de entrada de **DataTable** debe tener un valor único y dicho valor debe coincidir con el parámetro con nombre correspondiente de la función de R.</span><span class="sxs-lookup"><span data-stu-id="0e030-185">The **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="0e030-186">El valor **NULL** de los puertos de **DataTable** opcionales que no se pasan como entrada en un experimento se pasa a la función de R y los puertos zip opcionales se ignorarán si la entrada no está conectada.</span><span class="sxs-lookup"><span data-stu-id="0e030-186">Optional **DataTable** ports that are not passed as input in an experiment have the value **NULL** passed to the R function and optional zip ports are ignored if the input is not connected.</span></span> <span data-ttu-id="0e030-187">El atributo **isOptional** es opcional para los tipos **DataTable** y **Zip**, y es *false* de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0e030-187">The **isOptional** attribute is optional for both the **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="0e030-188">**Zip:** los módulos personalizados pueden aceptar un archivo .zip como entrada.</span><span class="sxs-lookup"><span data-stu-id="0e030-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="0e030-189">Esta entrada se desempaqueta en el directorio de trabajo de R de la función</span><span class="sxs-lookup"><span data-stu-id="0e030-189">This input is unpacked into the R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files to be extracted to the R working directory.</Description>
           </Input>

<span data-ttu-id="0e030-190">En el caso de los módulos de R personalizados, el identificador de un puerto Zip no tiene que coincidir con los parámetros de la función de R.</span><span class="sxs-lookup"><span data-stu-id="0e030-190">For custom R modules, the id for a Zip port does not have to match any parameters of the R function.</span></span> <span data-ttu-id="0e030-191">Esto se debe a que el archivo zip se extrae automáticamente en el directorio de trabajo de R.</span><span class="sxs-lookup"><span data-stu-id="0e030-191">This is because the zip file is automatically extracted to the R working directory.</span></span>

<span data-ttu-id="0e030-192">**Reglas de entrada:**</span><span class="sxs-lookup"><span data-stu-id="0e030-192">**Input Rules:**</span></span>

* <span data-ttu-id="0e030-193">El valor del atributo **id** del elemento **Input** debe ser un nombre de variable de R válido.</span><span class="sxs-lookup"><span data-stu-id="0e030-193">The value of the **id** attribute of the **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="0e030-194">El valor del atributo **id** del elemento **Input** no debe superar los 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="0e030-194">The value of the **id** attribute of the **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="0e030-195">El valor del atributo **name** del elemento **Input** no debe superar los 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="0e030-195">The value of the **name** attribute of the **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="0e030-196">El contenido del elemento **Description** no debe superar los 128 caracteres.</span><span class="sxs-lookup"><span data-stu-id="0e030-196">The content of the **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="0e030-197">El valor del atributo **type** del elemento **Input** debe ser *Zip* o *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="0e030-197">The value of the **type** attribute of the **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="0e030-198">El valor del atributo **isOptional** del elemento **Input** no es necesario (y es *false* de forma predeterminada cuando no se especifica); pero si se especifica, debe ser *true* o *false*.</span><span class="sxs-lookup"><span data-stu-id="0e030-198">The value of the **isOptional** attribute of the **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="0e030-199">Elementos de salida</span><span class="sxs-lookup"><span data-stu-id="0e030-199">Output elements</span></span>
<span data-ttu-id="0e030-200">**Puertos de salida estándar:** los puertos de salida se asignan a los valores devueltos desde la función de R, y luego pueden usarlos los módulos posteriores.</span><span class="sxs-lookup"><span data-stu-id="0e030-200">**Standard output ports:** Output ports are mapped to the return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="0e030-201">*DataTable* es el único tipo de puerto de salida estándar que se admite actualmente.</span><span class="sxs-lookup"><span data-stu-id="0e030-201">*DataTable* is the only standard output port type supported currently.</span></span> <span data-ttu-id="0e030-202">(Próximamente se incluirá compatibilidad con *Learners* y *Transforms*). Una salida de *DataTable* se define como:</span><span class="sxs-lookup"><span data-stu-id="0e030-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="0e030-203">En el caso de las salidas de los módulos de R personalizados, el valor del atributo **id** no tiene que corresponder con nada del script de R, debe ser único.</span><span class="sxs-lookup"><span data-stu-id="0e030-203">For outputs in custom R modules, the value of the **id** attribute does not have to correspond with anything in the R script, but it must be unique.</span></span> <span data-ttu-id="0e030-204">En el caso de la salida de un módulo individual, el valor devuelto de la función de R debe ser *data.frame*.</span><span class="sxs-lookup"><span data-stu-id="0e030-204">For a single module output, the return value from the R function must be a *data.frame*.</span></span> <span data-ttu-id="0e030-205">Para emitir más de un objeto de un tipo de datos admitidos, es necesario especificar los puertos de salida correspondientes en el archivo de definición de XML y los objetos deben devolverse como una lista.</span><span class="sxs-lookup"><span data-stu-id="0e030-205">In order to output more than one object of a supported data type, the appropriate output ports need to be specified in the XML definition file and the objects need to be returned as a list.</span></span> <span data-ttu-id="0e030-206">Los objetos emitidos se asignan a los puertos de salida de izquierda a derecha, reflejando el orden en que los objetos se colocan en la lista devuelta.</span><span class="sxs-lookup"><span data-stu-id="0e030-206">The output objects are assigned to output ports from left to right, reflecting the order in which the objects are placed in the returned list.</span></span>

<span data-ttu-id="0e030-207">Por ejemplo, si quiere modificar el módulo **Custom Add Rows** (Personalizar Agregar filas) para que genere los dos conjuntos de datos originales, *dataset1* y *dataset2*, además del conjunto de datos recién incorporado *dataset* (de izquierda a derecha, así: *dataset*, *dataset1*, *dataset2*), defina los puertos de salida en el archivo CustomAddRows.xml, tal como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="0e030-207">For example, if you want to modify the **Custom Add Rows** module to output the original two datasets, *dataset1* and *dataset2*, in addition to the new joined dataset, *dataset*, (in an order, from left to right, as: *dataset*, *dataset1*, *dataset2*), then define the output ports in the CustomAddRows.xml file as follows:</span></span>

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


<span data-ttu-id="0e030-208">Y devuelva la lista de objetos de una lista en el orden correcto en "CustomAddRows.R":</span><span class="sxs-lookup"><span data-stu-id="0e030-208">And return the list of objects in a list in the correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="0e030-209">**Salida de visualización:** también puede especificar un puerto de salida del tipo *Visualization*que muestra la salida del dispositivo gráfico de R y la salida de la consola.</span><span class="sxs-lookup"><span data-stu-id="0e030-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays the output from the R graphics device and console output.</span></span> <span data-ttu-id="0e030-210">Este puerto no forma parte de la salida de la función de R y no interfiere en el orden de los restantes tipos de puerto de salida.</span><span class="sxs-lookup"><span data-stu-id="0e030-210">This port is not part of the R function output and does not interfere with the order of the other output port types.</span></span> <span data-ttu-id="0e030-211">Para agregar un puerto de visualización a los módulos personalizados, agregue un elemento **Output** con un valor de *Visualization* para su atributo **type**:</span><span class="sxs-lookup"><span data-stu-id="0e030-211">To add a visualization port to the custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View the R console graphics device output.</Description>
    </Output>

<span data-ttu-id="0e030-212">**Reglas de salida:**</span><span class="sxs-lookup"><span data-stu-id="0e030-212">**Output Rules:**</span></span>

* <span data-ttu-id="0e030-213">El valor del atributo **id** del elemento **Output** debe ser un nombre de variable de R válido.</span><span class="sxs-lookup"><span data-stu-id="0e030-213">The value of the **id** attribute of the **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="0e030-214">El valor del atributo **id** del elemento **Output** no debe superar los 32 caracteres.</span><span class="sxs-lookup"><span data-stu-id="0e030-214">The value of the **id** attribute of the **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="0e030-215">El valor del atributo **name** del elemento **Output** no debe superar los 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="0e030-215">The value of the **name** attribute of the **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="0e030-216">El valor del atributo **type** del elemento **Output** debe ser *Visualization*.</span><span class="sxs-lookup"><span data-stu-id="0e030-216">The value of the **type** attribute of the **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="0e030-217">Argumentos</span><span class="sxs-lookup"><span data-stu-id="0e030-217">Arguments</span></span>
<span data-ttu-id="0e030-218">Se pueden pasar datos adicionales a la función de R a través de los parámetros del módulo que se definen en el elemento **Arguments** .</span><span class="sxs-lookup"><span data-stu-id="0e030-218">Additional data can be passed to the R function via module parameters which are defined in the **Arguments** element.</span></span> <span data-ttu-id="0e030-219">Estos parámetros aparecen en el panel de propiedades de la derecha de la interfaz de usuario de Aprendizaje automático cuando está seleccionado el módulo.</span><span class="sxs-lookup"><span data-stu-id="0e030-219">These parameters appear in the rightmost properties pane of the Machine Learning UI when the module is selected.</span></span> <span data-ttu-id="0e030-220">Los argumentos pueden ser cualquiera de los tipos admitidos, o bien puede crear una enumeración personalizada cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0e030-220">Arguments can be any of the supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="0e030-221">Al igual que los elementos **Ports**, los elementos **Arguments** pueden tener un elemento **Description** opcional que especifica el texto que aparece al mantener el ratón sobre el nombre del parámetro.</span><span class="sxs-lookup"><span data-stu-id="0e030-221">Similar to the **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies the text that appears when you hover the mouse over the parameter name.</span></span>
<span data-ttu-id="0e030-222">Las propiedades opcionales de un módulo, como defaultValue, minValue y maxValue, se pueden agregar a cualquier argumento como atributos de un elemento **Properties** .</span><span class="sxs-lookup"><span data-stu-id="0e030-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added to any argument as attributes to a **Properties** element.</span></span> <span data-ttu-id="0e030-223">Las propiedades válidas para el elemento **Properties** dependen del tipo de argumento y se describen con los siguientes tipos de argumento admitidos en la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="0e030-223">Valid properties for the **Properties** element depend on the argument type and are described with the supported argument types in the next section.</span></span> <span data-ttu-id="0e030-224">Argumentos con el **isOptional** propiedad establecida en **"true"** no requieren que el usuario que especifique un valor.</span><span class="sxs-lookup"><span data-stu-id="0e030-224">Arguments with the **isOptional** property set to **"true"** do not require the user to enter a value.</span></span> <span data-ttu-id="0e030-225">Si no se proporciona un valor al argumento, el argumento no se pasa a la función de punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="0e030-225">If a value is not provided to the argument, then the argument is not passed to the entry point function.</span></span> <span data-ttu-id="0e030-226">Los argumentos de la función de punto de entrada que son opcionales deben tratarse de forma explícita mediante la función, por ejemplo, asignar un valor predeterminado de NULL en la definición de función de punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="0e030-226">Arguments of the entry point function that are optional need to be explicitly handled by the function, e.g. assigned a default value of NULL in the entry point function definition.</span></span> <span data-ttu-id="0e030-227">Un argumento opcional solo aplicará las demás restricciones de argumento, es decir, min o max, si el usuario proporciona un valor.</span><span class="sxs-lookup"><span data-stu-id="0e030-227">An optional argument will only enforce the other argument constraints, i.e. min or max, if a value is provided by the user.</span></span>
<span data-ttu-id="0e030-228">Al igual que con las entradas y salidas, es fundamental que cada uno de los parámetros tenga valores de identificadores únicos asociados a ellos.</span><span class="sxs-lookup"><span data-stu-id="0e030-228">As with inputs and outputs, it is critical that each of the parameters have unique id values associated with them.</span></span> <span data-ttu-id="0e030-229">En nuestro ejemplo de inicio rápido, el parámetro/id asociado era *swap*.</span><span class="sxs-lookup"><span data-stu-id="0e030-229">In our quick start example the associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="0e030-230">Elemento Arg</span><span class="sxs-lookup"><span data-stu-id="0e030-230">Arg element</span></span>
<span data-ttu-id="0e030-231">Los parámetros del módulo se definen mediante el elemento secundario **Arg** de la sección **Arguments** del archivo de definición XML.</span><span class="sxs-lookup"><span data-stu-id="0e030-231">A module parameter is defined using the **Arg** child element of the **Arguments** section of the XML definition file.</span></span> <span data-ttu-id="0e030-232">Al igual que con los elementos secundarios de la sección **Ports**, el orden de los parámetros de la sección **Arguments** define el diseño que se encuentra en la experiencia de usuario.</span><span class="sxs-lookup"><span data-stu-id="0e030-232">As with the child elements in the **Ports** section, the ordering of parameters in the **Arguments** section defines the layout encountered in the UX.</span></span> <span data-ttu-id="0e030-233">Los parámetros aparecen de arriba abajo en la interfaz de usuario en el mismo orden en que se definen en el archivo XML.</span><span class="sxs-lookup"><span data-stu-id="0e030-233">The parameters appear from top down in the UI in the same order in which they are defined in the XML file.</span></span> <span data-ttu-id="0e030-234">Aquí se enumeran los tipos admitidos por Aprendizaje automático para los parámetros.</span><span class="sxs-lookup"><span data-stu-id="0e030-234">The types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="0e030-235">**int** : parámetro de tipo entero (32 bits).</span><span class="sxs-lookup"><span data-stu-id="0e030-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="0e030-236">*Propiedades opcionales*: **min**, **max**, **default** e **isOptional**</span><span class="sxs-lookup"><span data-stu-id="0e030-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="0e030-237">**double** : parámetro de tipo doble.</span><span class="sxs-lookup"><span data-stu-id="0e030-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="0e030-238">*Propiedades opcionales*: **min**, **max**, **default** e **isOptional**</span><span class="sxs-lookup"><span data-stu-id="0e030-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="0e030-239">**bool** : parámetro booleano que se representa mediante una casilla en la experiencia de usuario.</span><span class="sxs-lookup"><span data-stu-id="0e030-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="0e030-240">*Propiedades opcionales*: **default** : false si no se ha establecido</span><span class="sxs-lookup"><span data-stu-id="0e030-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="0e030-241">**string**: una cadena estándar.</span><span class="sxs-lookup"><span data-stu-id="0e030-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="0e030-242">*Propiedades opcionales*: **default** e **isOptional**</span><span class="sxs-lookup"><span data-stu-id="0e030-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="0e030-243">**ColumnPicker**: parámetro de selección de columnas.</span><span class="sxs-lookup"><span data-stu-id="0e030-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="0e030-244">Este tipo se representa en la experiencia de usuario como selector de columnas.</span><span class="sxs-lookup"><span data-stu-id="0e030-244">This type renders in the UX as a column chooser.</span></span> <span data-ttu-id="0e030-245">El elemento **Property** se usa aquí para especificar el identificador del puerto desde el que se seleccionarán columnas, donde el tipo de puerto de destino debe ser *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="0e030-245">The **Property** element is used here to specify the id of the port from which columns are selected, where the target port type must be *DataTable*.</span></span> <span data-ttu-id="0e030-246">El resultado de la selección de columnas se pasará a la función de R como una lista de cadenas que contiene los nombres de columna seleccionados.</span><span class="sxs-lookup"><span data-stu-id="0e030-246">The result of the column selection is passed to the R function as a list of strings containing the selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="0e030-247">*Propiedades requeridas*: **portId**; coincide con el identificador de un elemento Input con tipo *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="0e030-247">*Required Properties*: **portId** - matches the id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="0e030-248">*Propiedades opcionales*:</span><span class="sxs-lookup"><span data-stu-id="0e030-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="0e030-249">**allowedTypes** : permite filtrar los tipos de columnas entre los que puede elegir.</span><span class="sxs-lookup"><span data-stu-id="0e030-249">**allowedTypes** - Filters the column types from which you can pick.</span></span> <span data-ttu-id="0e030-250">Los valores válidos son:</span><span class="sxs-lookup"><span data-stu-id="0e030-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="0e030-251">Numeric</span><span class="sxs-lookup"><span data-stu-id="0e030-251">Numeric</span></span>
    * <span data-ttu-id="0e030-252">Booleano</span><span class="sxs-lookup"><span data-stu-id="0e030-252">Boolean</span></span>
    * <span data-ttu-id="0e030-253">Categorías</span><span class="sxs-lookup"><span data-stu-id="0e030-253">Categorical</span></span>
    * <span data-ttu-id="0e030-254">string</span><span class="sxs-lookup"><span data-stu-id="0e030-254">String</span></span>
    * <span data-ttu-id="0e030-255">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="0e030-255">Label</span></span>
    * <span data-ttu-id="0e030-256">Característica</span><span class="sxs-lookup"><span data-stu-id="0e030-256">Feature</span></span>
    * <span data-ttu-id="0e030-257">Score</span><span class="sxs-lookup"><span data-stu-id="0e030-257">Score</span></span>
    * <span data-ttu-id="0e030-258">Todo</span><span class="sxs-lookup"><span data-stu-id="0e030-258">All</span></span>
  * <span data-ttu-id="0e030-259">**default** : entre las selecciones predeterminadas válidas para el selector de columna se incluyen:</span><span class="sxs-lookup"><span data-stu-id="0e030-259">**default** - Valid default selections for the column picker include:</span></span> 
    
    * <span data-ttu-id="0e030-260">None</span><span class="sxs-lookup"><span data-stu-id="0e030-260">None</span></span>
    * <span data-ttu-id="0e030-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="0e030-261">NumericFeature</span></span>
    * <span data-ttu-id="0e030-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="0e030-262">NumericLabel</span></span>
    * <span data-ttu-id="0e030-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="0e030-263">NumericScore</span></span>
    * <span data-ttu-id="0e030-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="0e030-264">NumericAll</span></span>
    * <span data-ttu-id="0e030-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="0e030-265">BooleanFeature</span></span>
    * <span data-ttu-id="0e030-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="0e030-266">BooleanLabel</span></span>
    * <span data-ttu-id="0e030-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="0e030-267">BooleanScore</span></span>
    * <span data-ttu-id="0e030-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="0e030-268">BooleanAll</span></span>
    * <span data-ttu-id="0e030-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="0e030-269">CategoricalFeature</span></span>
    * <span data-ttu-id="0e030-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="0e030-270">CategoricalLabel</span></span>
    * <span data-ttu-id="0e030-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="0e030-271">CategoricalScore</span></span>
    * <span data-ttu-id="0e030-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="0e030-272">CategoricalAll</span></span>
    * <span data-ttu-id="0e030-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="0e030-273">StringFeature</span></span>
    * <span data-ttu-id="0e030-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="0e030-274">StringLabel</span></span>
    * <span data-ttu-id="0e030-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="0e030-275">StringScore</span></span>
    * <span data-ttu-id="0e030-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="0e030-276">StringAll</span></span>
    * <span data-ttu-id="0e030-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="0e030-277">AllLabel</span></span>
    * <span data-ttu-id="0e030-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="0e030-278">AllFeature</span></span>
    * <span data-ttu-id="0e030-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="0e030-279">AllScore</span></span>
    * <span data-ttu-id="0e030-280">Todo</span><span class="sxs-lookup"><span data-stu-id="0e030-280">All</span></span>

<span data-ttu-id="0e030-281">**Desplegable**: lista (desplegable) especificada por el usuario que se muestra.</span><span class="sxs-lookup"><span data-stu-id="0e030-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="0e030-282">Los elementos de la lista desplegable se especifican en el elemento **Properties** mediante un elemento **Item**.</span><span class="sxs-lookup"><span data-stu-id="0e030-282">The dropdown items are specified within the **Properties** element using an **Item** element.</span></span> <span data-ttu-id="0e030-283">El **id** de cada **elemento** debe ser único y debe ser una variable de R válida.</span><span class="sxs-lookup"><span data-stu-id="0e030-283">The **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="0e030-284">El valor del **nombre** de un **elemento** actúa como el texto que aparece y el valor que se pasa a la función de R.</span><span class="sxs-lookup"><span data-stu-id="0e030-284">The value of the **name** of an **Item** serves as both the text that you see and the value that is passed to the R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="0e030-285">*Propiedades opcionales*:</span><span class="sxs-lookup"><span data-stu-id="0e030-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="0e030-286">**default**: el valor de la propiedad predeterminada debe corresponder a un valor de identificador de uno de los elementos **Item**.</span><span class="sxs-lookup"><span data-stu-id="0e030-286">**default** - The value for the default property must correspond with an id value from one of the **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="0e030-287">Archivos auxiliares</span><span class="sxs-lookup"><span data-stu-id="0e030-287">Auxiliary Files</span></span>
<span data-ttu-id="0e030-288">Cualquier archivo que se coloque en el archivo ZIP de módulo personalizado estará disponible para su uso durante el tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="0e030-288">Any file that is placed in your custom module ZIP file is going to be available for use during execution time.</span></span> <span data-ttu-id="0e030-289">Se conservarán todas las estructuras de directorios presentes.</span><span class="sxs-lookup"><span data-stu-id="0e030-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="0e030-290">Esto significa que el abastecimiento de archivos funcionará igual localmente y en la ejecución de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e030-290">This means that file sourcing works the same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="0e030-291">Observe que todos los archivos se extraen en el directorio 'src', por lo que todas las rutas de acceso deberían tener el prefijo 'src/'.</span><span class="sxs-lookup"><span data-stu-id="0e030-291">Notice that all files are extracted to ‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="0e030-292">Por ejemplo, supongamos que desea quitar tanto todas las filas con ND como todas las filas duplicadas del conjunto de datos antes de generarlo en CustomAddRows y que ya ha escrito una función de R que lo hace en el archivo RemoveDupNARows.R:</span><span class="sxs-lookup"><span data-stu-id="0e030-292">For example, say you want to remove any rows with NAs from the dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="0e030-293">Puede originar el archivo auxiliar RemoveDupNARows.R en la función CustomAddRows:</span><span class="sxs-lookup"><span data-stu-id="0e030-293">You can source the auxiliary file RemoveDupNARows.R in the CustomAddRows function:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

<span data-ttu-id="0e030-294">A continuación, cargue un archivo zip que contenga "myAddRows.R", "myAddRows.xml" y "removeDupNARows.R" como módulo de R personalizado.</span><span class="sxs-lookup"><span data-stu-id="0e030-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="0e030-295">Entorno de ejecución</span><span class="sxs-lookup"><span data-stu-id="0e030-295">Execution Environment</span></span>
<span data-ttu-id="0e030-296">El entorno de ejecución del script de R usa la misma versión de R que el módulo **Ejecutar script de R** y puede usar los mismos paquetes predeterminados.</span><span class="sxs-lookup"><span data-stu-id="0e030-296">The execution environment for the R script uses the same version of R as the **Execute R Script** module and can use the same default packages.</span></span> <span data-ttu-id="0e030-297">También puede agregar paquetes de R adicionales al módulo personalizado incluyéndolos en el paquete zip del módulo personalizado.</span><span class="sxs-lookup"><span data-stu-id="0e030-297">You can also add additional R packages to your custom module by including them in the custom module zip package.</span></span> <span data-ttu-id="0e030-298">Solo tiene que cargarlos en el script de R como lo haría en su propio entorno de R.</span><span class="sxs-lookup"><span data-stu-id="0e030-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="0e030-299">**limitaciones del entorno de ejecución** se incluyen:</span><span class="sxs-lookup"><span data-stu-id="0e030-299">**Limitations of the execution environment** include:</span></span>

* <span data-ttu-id="0e030-300">Sistema de archivos no persistentes: los archivos escritos cuando se ejecuta el módulo personalizado no persistirán en varias ejecuciones del mismo módulo.</span><span class="sxs-lookup"><span data-stu-id="0e030-300">Non-persistent file system: Files written when the custom module is run are not persisted across multiple runs of the same module.</span></span>
* <span data-ttu-id="0e030-301">Sin acceso de red</span><span class="sxs-lookup"><span data-stu-id="0e030-301">No network access</span></span>

