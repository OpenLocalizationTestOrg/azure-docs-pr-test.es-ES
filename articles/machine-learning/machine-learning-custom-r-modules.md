---
title: "aaaAuthor los módulos de R personalizado en aprendizaje automático de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a><span data-ttu-id="d6804-103">Creación de módulos R personalizados en Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="d6804-103">Author custom R modules in Azure Machine Learning</span></span>
<span data-ttu-id="d6804-104">Este tema se describe cómo tooauthor e implementar un módulo personalizado de R en aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6804-104">This topic describes how tooauthor and deploy a custom R module in Azure Machine Learning.</span></span> <span data-ttu-id="d6804-105">Explica qué son los módulos de R personalizados y qué archivos son toodefine usado ellos.</span><span class="sxs-lookup"><span data-stu-id="d6804-105">It explains what custom R modules are and what files are used toodefine them.</span></span> <span data-ttu-id="d6804-106">Ilustra cómo tooconstruct Hola archivos que definen un módulo y cómo tooregister Hola módulo para la implementación en un área de trabajo de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="d6804-106">It illustrates how tooconstruct hello files that define a module and how tooregister hello module for deployment in a Machine Learning workspace.</span></span> <span data-ttu-id="d6804-107">Hello elementos y atributos que se utilizan en la definición de Hola de módulo personalizado de hello son, a continuación, se describe con más detalle.</span><span class="sxs-lookup"><span data-stu-id="d6804-107">hello elements and attributes used in hello definition of hello custom module are then described in more detail.</span></span> <span data-ttu-id="d6804-108">Cómo también se describe la funcionalidad auxiliar toouse y archivos y varias salidas.</span><span class="sxs-lookup"><span data-stu-id="d6804-108">How toouse auxiliary functionality and files and multiple outputs is also discussed.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a><span data-ttu-id="d6804-109">¿Qué es un módulo R personalizado?</span><span class="sxs-lookup"><span data-stu-id="d6804-109">What is a custom R module?</span></span>
<span data-ttu-id="d6804-110">A **módulo personalizado** es un módulo definido por el usuario que se puede carga el área de trabajo de tooyour y se ejecuta como parte de un experimento de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6804-110">A **custom module** is a user-defined module that can be uploaded tooyour workspace and executed as part of an Azure Machine Learning experiment.</span></span> <span data-ttu-id="d6804-111">Un **módulo de R personalizado** es un módulo personalizado que ejecuta una función de R definida por el usuario.</span><span class="sxs-lookup"><span data-stu-id="d6804-111">A **custom R module** is a custom module that executes a user-defined R function.</span></span> <span data-ttu-id="d6804-112">**R** es un lenguaje de programación de computación estadística y gráficos utilizado ampliamente por científicos estadísticos y de datos para implementar algoritmos.</span><span class="sxs-lookup"><span data-stu-id="d6804-112">**R** is a programming language for statistical computing and graphics that is widely used by statisticians and data scientists for implementing algorithms.</span></span> <span data-ttu-id="d6804-113">Actualmente, R es admitido en módulos personalizados, pero la compatibilidad para idiomas adicionales está programada para futuras versiones de idioma solo Hola.</span><span class="sxs-lookup"><span data-stu-id="d6804-113">Currently, R is hello only language supported in custom modules, but support for additional languages is scheduled for future releases.</span></span>

<span data-ttu-id="d6804-114">Los módulos personalizados tienen **estatus** aprendizaje automático de Azure en sentido Hola que puede usarse como cualquier otro módulo.</span><span class="sxs-lookup"><span data-stu-id="d6804-114">Custom modules have **first-class status** in Azure Machine Learning in hello sense that they can be used just like any other module.</span></span> <span data-ttu-id="d6804-115">Pueden ejecutarse con otros módulos e incluirse en experimentos publicados o visualizaciones.</span><span class="sxs-lookup"><span data-stu-id="d6804-115">They can be executed with other modules, included in published experiments or in visualizations.</span></span> <span data-ttu-id="d6804-116">Tiene control sobre el algoritmo de hello implementado por el módulo de hello, Hola toobe de puertos de entrada y salida que se usa, Hola parámetros de modelado y otros distintos comportamientos en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="d6804-116">You have control over hello algorithm implemented by hello module, hello input and output ports toobe used, hello modeling parameters, and other various runtime behaviors.</span></span> <span data-ttu-id="d6804-117">Un experimento contiene módulos personalizados también se puede publicar en hello Cortana Intelligence Galería para compartir fácilmente.</span><span class="sxs-lookup"><span data-stu-id="d6804-117">An experiment that contains custom modules can also be published into hello Cortana Intelligence Gallery for easy sharing.</span></span>

## <a name="files-in-a-custom-r-module"></a><span data-ttu-id="d6804-118">Archivos de un módulo R personalizado</span><span class="sxs-lookup"><span data-stu-id="d6804-118">Files in a custom R module</span></span>
<span data-ttu-id="d6804-119">Un módulo R personalizado se define mediante un archivo .zip que contiene, como mínimo, dos archivos:</span><span class="sxs-lookup"><span data-stu-id="d6804-119">A custom R module is defined by a .zip file that contains, at a minimum, two files:</span></span>

* <span data-ttu-id="d6804-120">A **archivo de código fuente** que implementa la función de hello R expuesta por el módulo de Hola</span><span class="sxs-lookup"><span data-stu-id="d6804-120">A **source file** that implements hello R function exposed by hello module</span></span>
* <span data-ttu-id="d6804-121">Un **archivo de definición XML** que describe la interfaz de módulo personalizado de Hola</span><span class="sxs-lookup"><span data-stu-id="d6804-121">An **XML definition file** that describes hello custom module interface</span></span>

<span data-ttu-id="d6804-122">Archivos auxiliares adicionales también pueden incluirse en el archivo .zip de Hola que proporciona la funcionalidad que puede tener acceso desde el módulo personalizado de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6804-122">Additional auxiliary files can also be included in hello .zip file that provides functionality that can be accessed from hello custom module.</span></span> <span data-ttu-id="d6804-123">Esta opción se describe en hello **argumentos** forma parte de la sección de referencia de hello **elementos en el archivo de definición XML de hello** siguiente ejemplo de Hola inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="d6804-123">This option is discussed in hello **Arguments** part of hello reference section **Elements in hello XML definition file** following hello quickstart example.</span></span>

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a><span data-ttu-id="d6804-124">Ejemplo de inicio rápido: definir, empaquetar y registrar un módulo R personalizado</span><span class="sxs-lookup"><span data-stu-id="d6804-124">Quickstart example: define, package, and register a custom R module</span></span>
<span data-ttu-id="d6804-125">Este ejemplo ilustra cómo tooconstruct Hola archivos requeridos por un módulo personalizado de R, empaquetarlos en un archivo zip y, a continuación, un módulo de hello registrar en el área de trabajo de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="d6804-125">This example illustrates how tooconstruct hello files required by a custom R module, package them into a zip file, and then register hello module in your Machine Learning workspace.</span></span> <span data-ttu-id="d6804-126">Hello archivos de ejemplo y el paquete de ejemplo zip pueden descargarse desde [CustomAddRows.zip Descargar archivo](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="d6804-126">hello example zip package and sample files can be downloaded from [Download CustomAddRows.zip file](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409).</span></span>

## <a name="hello-source-file"></a><span data-ttu-id="d6804-127">archivo de código fuente de Hola</span><span class="sxs-lookup"><span data-stu-id="d6804-127">hello source file</span></span>
<span data-ttu-id="d6804-128">Considere la posibilidad de ejemplo de Hola de un **personalizado agregar filas** módulo que modifica la implementación estándar de Hola de hello **agregar filas** módulo usa tooconcatenate filas (observaciones) de dos conjuntos de datos (tramas de datos).</span><span class="sxs-lookup"><span data-stu-id="d6804-128">Consider hello example of a **Custom Add Rows** module that modifies hello standard implementation of hello **Add Rows** module used tooconcatenate rows (observations) from two datasets (data frames).</span></span> <span data-ttu-id="d6804-129">Hola estándar **agregar filas** módulo anexa filas de hello del segundo conjunto de datos de entrada toohello final de Hola de hello primera entrada conjunto de datos mediante hello `rbind` algoritmo.</span><span class="sxs-lookup"><span data-stu-id="d6804-129">hello standard **Add Rows** module appends hello rows of hello second input dataset toohello end of hello first input dataset using hello `rbind` algorithm.</span></span> <span data-ttu-id="d6804-130">Hola personalizado `CustomAddRows` función acepta dos conjuntos de datos de forma similar, pero también acepta un parámetro booleano intercambio como una entrada adicional.</span><span class="sxs-lookup"><span data-stu-id="d6804-130">hello customized `CustomAddRows` function similarly accepts two datasets, but also accepts a Boolean swap parameter as an additional input.</span></span> <span data-ttu-id="d6804-131">Si el parámetro de intercambio de Hola se establece demasiado**FALSE**, devuelve Hola el mismo conjunto de datos como Hola implementación estándar.</span><span class="sxs-lookup"><span data-stu-id="d6804-131">If hello swap parameter is set too**FALSE**, it returns hello same data set as hello standard implementation.</span></span> <span data-ttu-id="d6804-132">Sin embargo, si el parámetro de intercambio de hello es **TRUE**, función hello anexa filas del primer conjunto de datos de entrada toohello end de hello segundo conjunto de datos en su lugar.</span><span class="sxs-lookup"><span data-stu-id="d6804-132">But if hello swap parameter is **TRUE**, hello function appends rows of first input dataset toohello end of hello second dataset instead.</span></span> <span data-ttu-id="d6804-133">archivo CustomAddRows.R Hello que contiene la implementación de Hola de hello R `CustomAddRows` función expuesta por hello **personalizado agregar filas** módulo tiene Hola siguiente código de R.</span><span class="sxs-lookup"><span data-stu-id="d6804-133">hello CustomAddRows.R file that contains hello implementation of hello R `CustomAddRows` function exposed by hello **Custom Add Rows** module has hello following R code.</span></span>

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

### <a name="hello-xml-definition-file"></a><span data-ttu-id="d6804-134">archivo de definición XML de Hola</span><span class="sxs-lookup"><span data-stu-id="d6804-134">hello XML definition file</span></span>
<span data-ttu-id="d6804-135">tooexpose esto `CustomAddRows` función como un módulo de aprendizaje automático de Azure, un archivo de definición XML debe crearse toospecify cómo Hola **personalizado agregar filas** módulo debe aspecto y comportamiento.</span><span class="sxs-lookup"><span data-stu-id="d6804-135">tooexpose this `CustomAddRows` function as an Azure Machine Learning module, an XML definition file must be created toospecify how hello **Custom Add Rows** module should look and behave.</span></span> 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


<span data-ttu-id="d6804-136">Es toonote crítico que Hola valo hello **Id. de** atributos de hello **entrada** y **Arg** elementos en el archivo XML de hello deben coincidir con los nombres de parámetro de función de Hola de hello R código de archivo de hello CustomAddRows.R exactamente: (*dataset1*, *dataset2*, y *intercambio* en el ejemplo de Hola).</span><span class="sxs-lookup"><span data-stu-id="d6804-136">It is critical toonote that hello value of hello **id** attributes of hello **Input** and **Arg** elements in hello XML file must match hello function parameter names of hello R code in hello CustomAddRows.R file EXACTLY: (*dataset1*, *dataset2*, and *swap* in hello example).</span></span> <span data-ttu-id="d6804-137">Hola de forma similar, el valor de hello **entryPoint** atributo de hello **lenguaje** elemento debe coincidir exactamente con hello nombre de función de hello en el script de Hola R: (*CustomAddRows* en el ejemplo de Hola).</span><span class="sxs-lookup"><span data-stu-id="d6804-137">Similarly, hello value of hello **entryPoint** attribute of hello **Language** element must match hello name of hello function in hello R script EXACTLY: (*CustomAddRows* in hello example).</span></span> 

<span data-ttu-id="d6804-138">En cambio, Hola **Id. de** atributo para hello **salida** elemento no corresponde tooany variables de script de Hola R.</span><span class="sxs-lookup"><span data-stu-id="d6804-138">In contrast, hello **id** attribute for hello **Output** element does not correspond tooany variables in hello R script.</span></span> <span data-ttu-id="d6804-139">Cuando se requiere más de un resultado, simplemente devuelven una lista de función hello R con resultados colocados *Hola mismo orden* como **salidas** elementos se declaran en el archivo XML de hello.</span><span class="sxs-lookup"><span data-stu-id="d6804-139">When more than one output is required, simply return a list from hello R function with results placed *in hello same order* as **Outputs** elements are declared in hello XML file.</span></span>

### <a name="package-and-register-hello-module"></a><span data-ttu-id="d6804-140">Módulo de Hola de paquete y registro</span><span class="sxs-lookup"><span data-stu-id="d6804-140">Package and register hello module</span></span>
<span data-ttu-id="d6804-141">Guardar estos dos archivos como *CustomAddRows.R* y *CustomAddRows.xml* y, a continuación, zip Hola dos archivos juntos en un *CustomAddRows.zip* archivo.</span><span class="sxs-lookup"><span data-stu-id="d6804-141">Save these two files as *CustomAddRows.R* and *CustomAddRows.xml* and then zip hello two files together into a *CustomAddRows.zip* file.</span></span>

<span data-ttu-id="d6804-142">tooregister en el área de trabajo de aprendizaje automático, área de trabajo vaya tooyour Hola estudio de aprendizaje automático, haga clic en hello **+ nuevo** situado en la parte inferior de Hola y elija **módulo -> de ZIP del paquete** tooupload Hola nueva **personalizado agregar filas** módulo.</span><span class="sxs-lookup"><span data-stu-id="d6804-142">tooregister them in your Machine Learning workspace, go tooyour workspace in hello Machine Learning Studio, click hello **+NEW** button on hello bottom and choose **MODULE -> FROM ZIP PACKAGE** tooupload hello new **Custom Add Rows** module.</span></span>

![Cargar archivo zip](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

<span data-ttu-id="d6804-144">Hola **personalizado agregar filas** módulo ahora está listo toobe acceso a sus experimentos de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="d6804-144">hello **Custom Add Rows** module is now ready toobe accessed by your Machine Learning experiments.</span></span>

## <a name="elements-in-hello-xml-definition-file"></a><span data-ttu-id="d6804-145">Elementos de archivo de definición XML de Hola</span><span class="sxs-lookup"><span data-stu-id="d6804-145">Elements in hello XML definition file</span></span>
### <a name="module-elements"></a><span data-ttu-id="d6804-146">Elementos Module</span><span class="sxs-lookup"><span data-stu-id="d6804-146">Module elements</span></span>
<span data-ttu-id="d6804-147">Hola **módulo** elemento es toodefine usado un módulo personalizado en el archivo XML de hello.</span><span class="sxs-lookup"><span data-stu-id="d6804-147">hello **Module** element is used toodefine a custom module in hello XML file.</span></span> <span data-ttu-id="d6804-148">Se pueden definir varios módulos en un archivo XML mediante el uso de varios elementos **Module** .</span><span class="sxs-lookup"><span data-stu-id="d6804-148">Multiple modules can be defined in one XML file using multiple **module** elements.</span></span> <span data-ttu-id="d6804-149">Cada uno de los módulos del área de trabajo debe tener un nombre único.</span><span class="sxs-lookup"><span data-stu-id="d6804-149">Each module in your workspace must have a unique name.</span></span> <span data-ttu-id="d6804-150">Registrar un módulo personalizado con el mismo nombre como un módulo personalizado existente de Hola y reemplaza módulo existente Hola con hello uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="d6804-150">Register a custom module with hello same name as an existing custom module and it replaces hello existing module with hello new one.</span></span> <span data-ttu-id="d6804-151">Sin embargo, los módulos personalizados se pueden registrar con el mismo nombre como un módulo de aprendizaje automático de Azure existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6804-151">Custom modules can, however, be registered with hello same name as an existing Azure Machine Learning module.</span></span> <span data-ttu-id="d6804-152">Si es así, aparecen en hello **personalizado** categoría de la paleta de módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6804-152">If so, they appear in hello **Custom** category of hello module palette.</span></span>

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


<span data-ttu-id="d6804-153">Dentro de hello **módulo** elemento, puede especificar dos elementos opcionales adicionales:</span><span class="sxs-lookup"><span data-stu-id="d6804-153">Within hello **Module** element, you can specify two additional optional elements:</span></span>

* <span data-ttu-id="d6804-154">un **propietario** elemento incrustado en el módulo de Hola</span><span class="sxs-lookup"><span data-stu-id="d6804-154">an **Owner** element that is embedded into hello module</span></span>  
* <span data-ttu-id="d6804-155">un **descripción** elemento que contiene el texto que se muestra en la Ayuda rápida para el módulo de Hola y cuando mantenga el mouse sobre módulo Hola Hola interfaz de usuario de aprendizaje de máquina.</span><span class="sxs-lookup"><span data-stu-id="d6804-155">a **Description** element that contains text that is displayed in quick help for hello module and when you hover over hello module in hello Machine Learning UI.</span></span>

<span data-ttu-id="d6804-156">Reglas para los límites de caracteres en elementos de módulo de hello:</span><span class="sxs-lookup"><span data-stu-id="d6804-156">Rules for characters limits in hello Module elements:</span></span>

* <span data-ttu-id="d6804-157">Hola valo hello **nombre** atributo Hola **módulo** elemento no debe superar los 64 caracteres de longitud.</span><span class="sxs-lookup"><span data-stu-id="d6804-157">hello value of hello **name** attribute in hello **Module** element must not exceed 64 characters in length.</span></span> 
* <span data-ttu-id="d6804-158">Hola contenido de hello **descripción** elemento no debe superar los 128 caracteres de longitud.</span><span class="sxs-lookup"><span data-stu-id="d6804-158">hello content of hello **Description** element must not exceed 128 characters in length.</span></span>
* <span data-ttu-id="d6804-159">Hola contenido de hello **propietario** elemento no debe superar los 32 caracteres de longitud.</span><span class="sxs-lookup"><span data-stu-id="d6804-159">hello content of hello **Owner** element must not exceed 32 characters in length.</span></span>

<span data-ttu-id="d6804-160">Resultados de un módulo pueden ser deterministas o nondeterministic.* * de forma predeterminada, todos los módulos se consideran toobe determinista.</span><span class="sxs-lookup"><span data-stu-id="d6804-160">A module's results can be deterministic or nondeterministic.** By default, all modules are considered toobe deterministic.</span></span> <span data-ttu-id="d6804-161">Es decir, dado un conjunto de parámetros de entrada y los datos que no cambian, módulo de hello debería devolver Hola mismo da como resultado eacRAND o una vez functionh que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="d6804-161">That is, given an unchanging set of input parameters and data, hello module should return hello same results eacRAND or a functionh time it is run.</span></span> <span data-ttu-id="d6804-162">Dado este comportamiento, estudio de aprendizaje automático de Azure solo vuelve a ejecutar los módulos que se marca como determinista si un parámetro o datos de entrada de hello ha cambiado.</span><span class="sxs-lookup"><span data-stu-id="d6804-162">Given this behavior, Azure Machine Learning Studio only reruns modules marked as deterministic if a parameter or hello input data has changed.</span></span> <span data-ttu-id="d6804-163">Devolver los resultados de hello en caché, también proporciona mucho una ejecución más rápida de experimentos.</span><span class="sxs-lookup"><span data-stu-id="d6804-163">Returning hello cached results also provides much faster execution of experiments.</span></span>

<span data-ttu-id="d6804-164">Hay funciones que no son deterministas, como RAND o una función que devuelve Hola fecha y hora actuales.</span><span class="sxs-lookup"><span data-stu-id="d6804-164">There are functions that are nondeterministic, such as RAND or a function that returns hello current date or time.</span></span> <span data-ttu-id="d6804-165">Si el módulo usa una función no determinista, puede especificar ese módulo hello no es determinista por establecer Hola opcional **isDeterministic** atributo demasiado**FALSE**.</span><span class="sxs-lookup"><span data-stu-id="d6804-165">If your module uses a nondeterministic function, you can specify that hello module is non-deterministic by setting hello optional **isDeterministic** attribute too**FALSE**.</span></span> <span data-ttu-id="d6804-166">Esto garantiza que ese módulo Hola se vuelve a ejecutar siempre que se ejecute el experimento de hello, incluso si hello módulo parámetros de entrada y no han cambiado.</span><span class="sxs-lookup"><span data-stu-id="d6804-166">This insures that hello module is rerun whenever hello experiment is run, even if hello module input and parameters have not changed.</span></span> 

### <a name="language-definition"></a><span data-ttu-id="d6804-167">Definición de lenguaje</span><span class="sxs-lookup"><span data-stu-id="d6804-167">Language Definition</span></span>
<span data-ttu-id="d6804-168">Hola **lenguaje** element en el archivo de definición XML es el idioma de módulo personalizado de Hola de toospecify usado.</span><span class="sxs-lookup"><span data-stu-id="d6804-168">hello **Language** element in your XML definition file is used toospecify hello custom module language.</span></span> <span data-ttu-id="d6804-169">Actualmente, R es Hola solo admite el idioma.</span><span class="sxs-lookup"><span data-stu-id="d6804-169">Currently, R is hello only supported language.</span></span> <span data-ttu-id="d6804-170">Hola valo hello **sourceFile** atributo debe ser el nombre de hello del archivo de hello R que contiene Hola función toocall cuando se ejecuta el módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6804-170">hello value of hello **sourceFile** attribute must be hello name of hello R file that contains hello function toocall when hello module is run.</span></span> <span data-ttu-id="d6804-171">Este archivo debe ser parte del paquete comprimido de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6804-171">This file must be part of hello zip package.</span></span> <span data-ttu-id="d6804-172">Hola valo hello **entryPoint** atributo es Hola nombre de función hello que se llama y debe coincidir con una función válida que se definen en el archivo de código fuente de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6804-172">hello value of hello **entryPoint** attribute is hello name of hello function being called and must match a valid function defined with in hello source file.</span></span>

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a><span data-ttu-id="d6804-173">Puertos</span><span class="sxs-lookup"><span data-stu-id="d6804-173">Ports</span></span>
<span data-ttu-id="d6804-174">Hello puertos de entrada y salidos para un módulo personalizado especificados en los elementos secundarios de hello **puertos** sección del archivo de definición XML de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6804-174">hello input and output ports for a custom module are specified in child elements of hello **Ports** section of hello XML definition file.</span></span> <span data-ttu-id="d6804-175">orden de Hola de estos elementos determina Hola diseño experimentado (UX) por los usuarios.</span><span class="sxs-lookup"><span data-stu-id="d6804-175">hello order of these elements determines hello layout experienced (UX) by users.</span></span> <span data-ttu-id="d6804-176">primer elemento secundario de Hello **entrada** o **salida** enumerados en hello **puertos** elemento del archivo XML de Hola se convierte en el puerto de entrada del extremo izquierdo de Hola Hola UX. de aprendizaje de máquina</span><span class="sxs-lookup"><span data-stu-id="d6804-176">hello first child **input** or **output** listed in hello **Ports** element of hello XML file becomes hello left-most input port in hello Machine Learning UX.</span></span>
<span data-ttu-id="d6804-177">Cada entrada y puerto de salida puede tener una función opcional **descripción** elemento secundario que especifica el texto hello se muestra cuando coloques el cursor del mouse de hello en el puerto de Hola Hola interfaz de usuario de aprendizaje de máquina.</span><span class="sxs-lookup"><span data-stu-id="d6804-177">Each input and output port may have an optional **Description** child element that specifies hello text shown when you hover hello mouse cursor over hello port in hello Machine Learning UI.</span></span>

<span data-ttu-id="d6804-178">**Reglas de puertos**:</span><span class="sxs-lookup"><span data-stu-id="d6804-178">**Ports Rules**:</span></span>

* <span data-ttu-id="d6804-179">El número máximo de **puertos de entrada y salida** es 8 para cada uno.</span><span class="sxs-lookup"><span data-stu-id="d6804-179">Maximum number of **input and output ports** is 8 for each.</span></span>

### <a name="input-elements"></a><span data-ttu-id="d6804-180">Elementos de entrada</span><span class="sxs-lookup"><span data-stu-id="d6804-180">Input elements</span></span>
<span data-ttu-id="d6804-181">Puertos de entrada permiten área de trabajo y función de toopass datos tooyour R.</span><span class="sxs-lookup"><span data-stu-id="d6804-181">Input ports allow you toopass data tooyour R function and workspace.</span></span> <span data-ttu-id="d6804-182">Hola **tipos de datos** que son compatibles con puertos de entrada son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="d6804-182">hello **data types** that are supported for input ports are as follows:</span></span> 

<span data-ttu-id="d6804-183">**DataTable:** se pasa este tipo de función tooyour R como un data.frame.</span><span class="sxs-lookup"><span data-stu-id="d6804-183">**DataTable:** This type is passed tooyour R function as a data.frame.</span></span> <span data-ttu-id="d6804-184">De hecho, los tipos (por ejemplo, archivos CSV o archivos ARFF) que son compatibles con el aprendizaje automático y que son compatibles con **DataTable** son data.frame tooa convertido automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d6804-184">In fact, any types (for example, CSV files or ARFF files) that are supported by Machine Learning and that are compatible with **DataTable** are converted tooa data.frame automatically.</span></span> 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

<span data-ttu-id="d6804-185">Hola **identificador** atributo asociado con cada uno de ellos **DataTable** puerto de entrada debe tener un valor único y este valor debe coincidir con el parámetro en la función de R con nombre correspondiente.</span><span class="sxs-lookup"><span data-stu-id="d6804-185">hello **id** attribute associated with each **DataTable** input port must have a unique value and this value must match its corresponding named parameter in your R function.</span></span>
<span data-ttu-id="d6804-186">Opcional **DataTable** puertos que no se pasan como entrada en un experimento tienen valor hello **NULL** función pasado toohello R y los puertos de zip opcional se omiten si Hola entrada no está conectado.</span><span class="sxs-lookup"><span data-stu-id="d6804-186">Optional **DataTable** ports that are not passed as input in an experiment have hello value **NULL** passed toohello R function and optional zip ports are ignored if hello input is not connected.</span></span> <span data-ttu-id="d6804-187">Hola **isOptional** atributo es opcional para ambos hello **DataTable** y **código postal** tipos y *false* de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d6804-187">hello **isOptional** attribute is optional for both hello **DataTable** and **Zip** types and is *false* by default.</span></span>

<span data-ttu-id="d6804-188">**Zip:** los módulos personalizados pueden aceptar un archivo .zip como entrada.</span><span class="sxs-lookup"><span data-stu-id="d6804-188">**Zip:** Custom modules can accept a zip file as input.</span></span> <span data-ttu-id="d6804-189">Esta entrada se desempaqueta en el directorio de trabajo de hello R de la función</span><span class="sxs-lookup"><span data-stu-id="d6804-189">This input is unpacked into hello R working directory of your function</span></span>

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

<span data-ttu-id="d6804-190">Para los módulos de R personalizados, Id. de Hola para un puerto Zip no tiene toomatch los parámetros de función hello R.</span><span class="sxs-lookup"><span data-stu-id="d6804-190">For custom R modules, hello id for a Zip port does not have toomatch any parameters of hello R function.</span></span> <span data-ttu-id="d6804-191">Esto es porque el archivo zip de hello es automáticamente extraídos toohello R directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d6804-191">This is because hello zip file is automatically extracted toohello R working directory.</span></span>

<span data-ttu-id="d6804-192">**Reglas de entrada:**</span><span class="sxs-lookup"><span data-stu-id="d6804-192">**Input Rules:**</span></span>

* <span data-ttu-id="d6804-193">Hola valo hello **Id. de** atributo de hello **entrada** elemento debe ser un nombre de variable válido de R.</span><span class="sxs-lookup"><span data-stu-id="d6804-193">hello value of hello **id** attribute of hello **Input** element must be a valid R variable name.</span></span>
* <span data-ttu-id="d6804-194">Hola valo hello **Id. de** atributo de hello **entrada** elemento no debe superar los 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d6804-194">hello value of hello **id** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="d6804-195">Hola valo hello **nombre** atributo de hello **entrada** elemento no debe superar los 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d6804-195">hello value of hello **name** attribute of hello **Input** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="d6804-196">Hola contenido de hello **descripción** elemento no debe tener más de 128 caracteres</span><span class="sxs-lookup"><span data-stu-id="d6804-196">hello content of hello **Description** element must not be longer than 128 characters</span></span>
* <span data-ttu-id="d6804-197">Hola valo hello **tipo** atributo de hello **entrada** el elemento debe estar *código postal* o *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="d6804-197">hello value of hello **type** attribute of hello **Input** element must be *Zip* or *DataTable*.</span></span>
* <span data-ttu-id="d6804-198">Hola valo hello **isOptional** atributo de hello **entrada** elemento no es necesario (y es *false* de forma predeterminada cuando no se especifica); pero si se especifica, debe ser *true* o *false*.</span><span class="sxs-lookup"><span data-stu-id="d6804-198">hello value of hello **isOptional** attribute of hello **Input** element is not required (and is *false* by default when not specified); but if it is specified, it must be *true* or *false*.</span></span>

### <a name="output-elements"></a><span data-ttu-id="d6804-199">Elementos de salida</span><span class="sxs-lookup"><span data-stu-id="d6804-199">Output elements</span></span>
<span data-ttu-id="d6804-200">**Puertos de salida estándar:** puertos de salida son asignadas toohello valores devueltos de la función de R, que, a continuación, se puede usar módulos posteriores.</span><span class="sxs-lookup"><span data-stu-id="d6804-200">**Standard output ports:** Output ports are mapped toohello return values from your R function, which can then be used by subsequent modules.</span></span> <span data-ttu-id="d6804-201">*DataTable* Hola tipo de puerto de salida estándar sólo admitidos actualmente.</span><span class="sxs-lookup"><span data-stu-id="d6804-201">*DataTable* is hello only standard output port type supported currently.</span></span> <span data-ttu-id="d6804-202">(Próximamente se incluirá compatibilidad con *Learners* y *Transforms*). Una salida de *DataTable* se define como:</span><span class="sxs-lookup"><span data-stu-id="d6804-202">(Support for *Learners* and *Transforms* is forthcoming.) A *DataTable* output is defined as:</span></span>

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

<span data-ttu-id="d6804-203">Los resultados en los módulos de R personalizados, Hola valo hello **identificador** atributo no tiene toocorrespond con nada en el script de Hola R, pero debe ser único.</span><span class="sxs-lookup"><span data-stu-id="d6804-203">For outputs in custom R modules, hello value of hello **id** attribute does not have toocorrespond with anything in hello R script, but it must be unique.</span></span> <span data-ttu-id="d6804-204">Para una salida de módulo único, valor devuelto de Hola de función hello R debe ser un *data.frame*.</span><span class="sxs-lookup"><span data-stu-id="d6804-204">For a single module output, hello return value from hello R function must be a *data.frame*.</span></span> <span data-ttu-id="d6804-205">En Ordenar toooutput más de un objeto de un tipo de datos admitidos, puertos de salida correspondiente Hola necesitan toobe especificado en el archivo de definición XML de Hola y Hola objetos necesitan ser toobe devuelve como una lista.</span><span class="sxs-lookup"><span data-stu-id="d6804-205">In order toooutput more than one object of a supported data type, hello appropriate output ports need toobe specified in hello XML definition file and hello objects need toobe returned as a list.</span></span> <span data-ttu-id="d6804-206">objetos de salida de Hello asigna puertos toooutput desde tooright izquierdo, reflejar el orden de hello en el que se colocan los objetos de hello en hello devuelve la lista.</span><span class="sxs-lookup"><span data-stu-id="d6804-206">hello output objects are assigned toooutput ports from left tooright, reflecting hello order in which hello objects are placed in hello returned list.</span></span>

<span data-ttu-id="d6804-207">Por ejemplo, si desea hello toomodify **personalizado agregar filas** toooutput módulo Hola originales dos conjuntos de datos, *dataset1* y *dataset2*, además unido toohello nueva conjunto de datos, *conjunto de datos*, (en un orden, de izquierda tooright, como: *conjunto de datos*, *dataset1*, *dataset2*), a continuación, defina Hola puertos en el archivo de hello CustomAddRows.xml de salida como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="d6804-207">For example, if you want toomodify hello **Custom Add Rows** module toooutput hello original two datasets, *dataset1* and *dataset2*, in addition toohello new joined dataset, *dataset*, (in an order, from left tooright, as: *dataset*, *dataset1*, *dataset2*), then define hello output ports in hello CustomAddRows.xml file as follows:</span></span>

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


<span data-ttu-id="d6804-208">Y devuelve la lista de Hola de objetos en una lista en orden correcto de hello en 'CustomAddRows.R':</span><span class="sxs-lookup"><span data-stu-id="d6804-208">And return hello list of objects in a list in hello correct order in ‘CustomAddRows.R’:</span></span>

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

<span data-ttu-id="d6804-209">**Salida de visualización:** también puede especificar un puerto de salida de tipo *visualización*, que muestra información sobre Hola de salida de consola y dispositivo de gráficos de hello R.</span><span class="sxs-lookup"><span data-stu-id="d6804-209">**Visualization output:** You can also specify an output port of type *Visualization*, which displays hello output from hello R graphics device and console output.</span></span> <span data-ttu-id="d6804-210">Este puerto no es parte de la salida de función hello R y no interfiere con el orden de Hola de hello otro tipos de puerto de salida.</span><span class="sxs-lookup"><span data-stu-id="d6804-210">This port is not part of hello R function output and does not interfere with hello order of hello other output port types.</span></span> <span data-ttu-id="d6804-211">Agregar una visualización puerto toohello módulos personalizados de tooadd una **salida** elemento con un valor de *visualización* para su **tipo** atributo:</span><span class="sxs-lookup"><span data-stu-id="d6804-211">tooadd a visualization port toohello custom modules, add an **Output** element with a value of *Visualization* for its **type** attribute:</span></span>

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

<span data-ttu-id="d6804-212">**Reglas de salida:**</span><span class="sxs-lookup"><span data-stu-id="d6804-212">**Output Rules:**</span></span>

* <span data-ttu-id="d6804-213">Hola valo hello **identificador** atributo de hello **salida** elemento debe ser un nombre de variable válido de R.</span><span class="sxs-lookup"><span data-stu-id="d6804-213">hello value of hello **id** attribute of hello **Output** element must be a valid R variable name.</span></span>
* <span data-ttu-id="d6804-214">Hola valo hello **identificador** atributo de hello **salida** elemento no debe superar los 32 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d6804-214">hello value of hello **id** attribute of hello **Output** element must not be longer than 32 characters.</span></span>
* <span data-ttu-id="d6804-215">Hola valo hello **nombre** atributo de hello **salida** elemento no debe superar los 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d6804-215">hello value of hello **name** attribute of hello **Output** element must not be longer than 64 characters.</span></span>
* <span data-ttu-id="d6804-216">Hola valo hello **tipo** atributo de hello **salida** el elemento debe estar *visualización*.</span><span class="sxs-lookup"><span data-stu-id="d6804-216">hello value of hello **type** attribute of hello **Output** element must be *Visualization*.</span></span>

### <a name="arguments"></a><span data-ttu-id="d6804-217">Argumentos</span><span class="sxs-lookup"><span data-stu-id="d6804-217">Arguments</span></span>
<span data-ttu-id="d6804-218">Datos adicionales se pueden pasar toohello R función a través de los parámetros del módulo que se definen en hello **argumentos** elemento.</span><span class="sxs-lookup"><span data-stu-id="d6804-218">Additional data can be passed toohello R function via module parameters which are defined in hello **Arguments** element.</span></span> <span data-ttu-id="d6804-219">Estos parámetros aparecen en panel de propiedades más a la derecha de Hola de interfaz de usuario de aprendizaje de máquina de hello cuando está seleccionado el módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6804-219">These parameters appear in hello rightmost properties pane of hello Machine Learning UI when hello module is selected.</span></span> <span data-ttu-id="d6804-220">Los argumentos pueden ser cualquiera de los tipos compatibles de Hola o puede crear una enumeración personalizada cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="d6804-220">Arguments can be any of hello supported types or you can create a custom enumeration when needed.</span></span> <span data-ttu-id="d6804-221">Toohello similar **puertos** elementos, **argumentos** elementos pueden tener una función opcional **descripción** elemento que especifica el texto hello que aparece al colocar el puntero del mouse Hola nombre de parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6804-221">Similar toohello **Ports** elements, **Arguments** elements can have an optional **Description** element that specifies hello text that appears when you hover hello mouse over hello parameter name.</span></span>
<span data-ttu-id="d6804-222">Se pueden agregar propiedades opcionales para un módulo, por ejemplo, defaultValue, minValue y maxValue tooany argumento como atributos tooa **propiedades** elemento.</span><span class="sxs-lookup"><span data-stu-id="d6804-222">Optional properties for a module, such as defaultValue, minValue, and maxValue can be added tooany argument as attributes tooa **Properties** element.</span></span> <span data-ttu-id="d6804-223">Propiedades válidas para hello **propiedades** elemento dependen de tipo de argumento de Hola y se describen con hello admite tipos de argumento en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="d6804-223">Valid properties for hello **Properties** element depend on hello argument type and are described with hello supported argument types in hello next section.</span></span> <span data-ttu-id="d6804-224">Argumentos con hello **isOptional** propiedad establecida demasiado**"true"** no requieren Hola usuario tooenter un valor.</span><span class="sxs-lookup"><span data-stu-id="d6804-224">Arguments with hello **isOptional** property set too**"true"** do not require hello user tooenter a value.</span></span> <span data-ttu-id="d6804-225">Si no se proporciona un valor toohello argumento, argumento de hello no se pasa toohello función de punto de entrada.</span><span class="sxs-lookup"><span data-stu-id="d6804-225">If a value is not provided toohello argument, then hello argument is not passed toohello entry point function.</span></span> <span data-ttu-id="d6804-226">Argumentos de función de punto de entrada de Hola que son toobe necesidad opcional controle explícitamente la función hello, por ejemplo, asigna un valor predeterminado es NULL en la definición de función de punto de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6804-226">Arguments of hello entry point function that are optional need toobe explicitly handled by hello function, e.g. assigned a default value of NULL in hello entry point function definition.</span></span> <span data-ttu-id="d6804-227">Un argumento opcional solo aplicará Hola otras restricciones de argumento, es decir, min o max, si un valor proporcionado por el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6804-227">An optional argument will only enforce hello other argument constraints, i.e. min or max, if a value is provided by hello user.</span></span>
<span data-ttu-id="d6804-228">Al igual que con las entradas y salidas, es fundamental que cada uno de los parámetros de hello tiene valores de identificador único asociados a ellos.</span><span class="sxs-lookup"><span data-stu-id="d6804-228">As with inputs and outputs, it is critical that each of hello parameters have unique id values associated with them.</span></span> <span data-ttu-id="d6804-229">En nuestro tutorial era ejemplo Hola asociados parámetro/id *intercambio*.</span><span class="sxs-lookup"><span data-stu-id="d6804-229">In our quick start example hello associated id/parameter was *swap*.</span></span>

### <a name="arg-element"></a><span data-ttu-id="d6804-230">Elemento Arg</span><span class="sxs-lookup"><span data-stu-id="d6804-230">Arg element</span></span>
<span data-ttu-id="d6804-231">Un parámetro de módulo se define utilizando hello **Arg** elemento secundario de hello **argumentos** sección del archivo de definición XML de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6804-231">A module parameter is defined using hello **Arg** child element of hello **Arguments** section of hello XML definition file.</span></span> <span data-ttu-id="d6804-232">Al igual que con los elementos secundarios Hola Hola **puertos** sección, Hola ordenar los parámetros en hello **argumentos** sección define el diseño de hello en hello UX.</span><span class="sxs-lookup"><span data-stu-id="d6804-232">As with hello child elements in hello **Ports** section, hello ordering of parameters in hello **Arguments** section defines hello layout encountered in hello UX.</span></span> <span data-ttu-id="d6804-233">Hello parámetros aparecen de arriba hacia abajo en hello interfaz de usuario en el mismo orden en que se definen de hello en el archivo XML de hello.</span><span class="sxs-lookup"><span data-stu-id="d6804-233">hello parameters appear from top down in hello UI in hello same order in which they are defined in hello XML file.</span></span> <span data-ttu-id="d6804-234">a continuación se enumeran los tipos de Hello admitidos por aprendizaje automático para los parámetros.</span><span class="sxs-lookup"><span data-stu-id="d6804-234">hello types supported by Machine Learning for parameters are listed here.</span></span> 

<span data-ttu-id="d6804-235">**int** : parámetro de tipo entero (32 bits).</span><span class="sxs-lookup"><span data-stu-id="d6804-235">**int** – an Integer (32-bit) type parameter.</span></span>

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* <span data-ttu-id="d6804-236">*Propiedades opcionales*: **min**, **max**, **default** e **isOptional**</span><span class="sxs-lookup"><span data-stu-id="d6804-236">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="d6804-237">**double** : parámetro de tipo doble.</span><span class="sxs-lookup"><span data-stu-id="d6804-237">**double** – a double type parameter.</span></span>

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* <span data-ttu-id="d6804-238">*Propiedades opcionales*: **min**, **max**, **default** e **isOptional**</span><span class="sxs-lookup"><span data-stu-id="d6804-238">*Optional Properties*: **min**, **max**, **default** and **isOptional**</span></span>

<span data-ttu-id="d6804-239">**bool** : parámetro booleano que se representa mediante una casilla en la experiencia de usuario.</span><span class="sxs-lookup"><span data-stu-id="d6804-239">**bool** – a Boolean parameter that is represented by a check-box in UX.</span></span>

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* <span data-ttu-id="d6804-240">*Propiedades opcionales*: **default** : false si no se ha establecido</span><span class="sxs-lookup"><span data-stu-id="d6804-240">*Optional Properties*: **default** - false if not set</span></span>

<span data-ttu-id="d6804-241">**string**: una cadena estándar.</span><span class="sxs-lookup"><span data-stu-id="d6804-241">**string**: a standard string</span></span>

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* <span data-ttu-id="d6804-242">*Propiedades opcionales*: **default** e **isOptional**</span><span class="sxs-lookup"><span data-stu-id="d6804-242">*Optional Properties*: **default** and **isOptional**</span></span>

<span data-ttu-id="d6804-243">**ColumnPicker**: parámetro de selección de columnas.</span><span class="sxs-lookup"><span data-stu-id="d6804-243">**ColumnPicker**: a column selection parameter.</span></span> <span data-ttu-id="d6804-244">Este tipo se representa en hello UX como un selector de columnas.</span><span class="sxs-lookup"><span data-stu-id="d6804-244">This type renders in hello UX as a column chooser.</span></span> <span data-ttu-id="d6804-245">Hola **propiedad** elemento es el Id. de Hola de toospecify aquí usado del puerto de Hola desde el que se seleccionan las columnas, donde el tipo de puerto de destino de hello debe ser de *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="d6804-245">hello **Property** element is used here toospecify hello id of hello port from which columns are selected, where hello target port type must be *DataTable*.</span></span> <span data-ttu-id="d6804-246">resultado de Hello de selección de la columna de Hola se pasa toohello R función como una lista de cadenas que contienen nombres de columna de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="d6804-246">hello result of hello column selection is passed toohello R function as a list of strings containing hello selected column names.</span></span> 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* <span data-ttu-id="d6804-247">*Propiedades necesarias*: **portId** -coincidencias Hola Id. de un elemento de entrada con tipo *DataTable*.</span><span class="sxs-lookup"><span data-stu-id="d6804-247">*Required Properties*: **portId** - matches hello id of an Input element with type *DataTable*.</span></span>
* <span data-ttu-id="d6804-248">*Propiedades opcionales*:</span><span class="sxs-lookup"><span data-stu-id="d6804-248">*Optional Properties*:</span></span>
  
  * <span data-ttu-id="d6804-249">**allowedTypes** -tipos de las columnas de hello filtros desde la que puede elegir.</span><span class="sxs-lookup"><span data-stu-id="d6804-249">**allowedTypes** - Filters hello column types from which you can pick.</span></span> <span data-ttu-id="d6804-250">Los valores válidos son:</span><span class="sxs-lookup"><span data-stu-id="d6804-250">Valid values include:</span></span> 
    
    * <span data-ttu-id="d6804-251">Numeric</span><span class="sxs-lookup"><span data-stu-id="d6804-251">Numeric</span></span>
    * <span data-ttu-id="d6804-252">Booleano</span><span class="sxs-lookup"><span data-stu-id="d6804-252">Boolean</span></span>
    * <span data-ttu-id="d6804-253">Categorías</span><span class="sxs-lookup"><span data-stu-id="d6804-253">Categorical</span></span>
    * <span data-ttu-id="d6804-254">string</span><span class="sxs-lookup"><span data-stu-id="d6804-254">String</span></span>
    * <span data-ttu-id="d6804-255">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="d6804-255">Label</span></span>
    * <span data-ttu-id="d6804-256">Característica</span><span class="sxs-lookup"><span data-stu-id="d6804-256">Feature</span></span>
    * <span data-ttu-id="d6804-257">Score</span><span class="sxs-lookup"><span data-stu-id="d6804-257">Score</span></span>
    * <span data-ttu-id="d6804-258">Todo</span><span class="sxs-lookup"><span data-stu-id="d6804-258">All</span></span>
  * <span data-ttu-id="d6804-259">**valor predeterminado** -selecciones predeterminadas válido para el selector de columna Hola incluyen:</span><span class="sxs-lookup"><span data-stu-id="d6804-259">**default** - Valid default selections for hello column picker include:</span></span> 
    
    * <span data-ttu-id="d6804-260">None</span><span class="sxs-lookup"><span data-stu-id="d6804-260">None</span></span>
    * <span data-ttu-id="d6804-261">NumericFeature</span><span class="sxs-lookup"><span data-stu-id="d6804-261">NumericFeature</span></span>
    * <span data-ttu-id="d6804-262">NumericLabel</span><span class="sxs-lookup"><span data-stu-id="d6804-262">NumericLabel</span></span>
    * <span data-ttu-id="d6804-263">NumericScore</span><span class="sxs-lookup"><span data-stu-id="d6804-263">NumericScore</span></span>
    * <span data-ttu-id="d6804-264">NumericAll</span><span class="sxs-lookup"><span data-stu-id="d6804-264">NumericAll</span></span>
    * <span data-ttu-id="d6804-265">BooleanFeature</span><span class="sxs-lookup"><span data-stu-id="d6804-265">BooleanFeature</span></span>
    * <span data-ttu-id="d6804-266">BooleanLabel</span><span class="sxs-lookup"><span data-stu-id="d6804-266">BooleanLabel</span></span>
    * <span data-ttu-id="d6804-267">BooleanScore</span><span class="sxs-lookup"><span data-stu-id="d6804-267">BooleanScore</span></span>
    * <span data-ttu-id="d6804-268">BooleanAll</span><span class="sxs-lookup"><span data-stu-id="d6804-268">BooleanAll</span></span>
    * <span data-ttu-id="d6804-269">CategoricalFeature</span><span class="sxs-lookup"><span data-stu-id="d6804-269">CategoricalFeature</span></span>
    * <span data-ttu-id="d6804-270">CategoricalLabel</span><span class="sxs-lookup"><span data-stu-id="d6804-270">CategoricalLabel</span></span>
    * <span data-ttu-id="d6804-271">CategoricalScore</span><span class="sxs-lookup"><span data-stu-id="d6804-271">CategoricalScore</span></span>
    * <span data-ttu-id="d6804-272">CategoricalAll</span><span class="sxs-lookup"><span data-stu-id="d6804-272">CategoricalAll</span></span>
    * <span data-ttu-id="d6804-273">StringFeature</span><span class="sxs-lookup"><span data-stu-id="d6804-273">StringFeature</span></span>
    * <span data-ttu-id="d6804-274">StringLabel</span><span class="sxs-lookup"><span data-stu-id="d6804-274">StringLabel</span></span>
    * <span data-ttu-id="d6804-275">StringScore</span><span class="sxs-lookup"><span data-stu-id="d6804-275">StringScore</span></span>
    * <span data-ttu-id="d6804-276">StringAll</span><span class="sxs-lookup"><span data-stu-id="d6804-276">StringAll</span></span>
    * <span data-ttu-id="d6804-277">AllLabel</span><span class="sxs-lookup"><span data-stu-id="d6804-277">AllLabel</span></span>
    * <span data-ttu-id="d6804-278">AllFeature</span><span class="sxs-lookup"><span data-stu-id="d6804-278">AllFeature</span></span>
    * <span data-ttu-id="d6804-279">AllScore</span><span class="sxs-lookup"><span data-stu-id="d6804-279">AllScore</span></span>
    * <span data-ttu-id="d6804-280">Todo</span><span class="sxs-lookup"><span data-stu-id="d6804-280">All</span></span>

<span data-ttu-id="d6804-281">**Desplegable**: lista (desplegable) especificada por el usuario que se muestra.</span><span class="sxs-lookup"><span data-stu-id="d6804-281">**DropDown**: a user-specified enumerated (dropdown) list.</span></span> <span data-ttu-id="d6804-282">elementos de lista desplegable de Hola se especifican en hello **propiedades** elemento mediante un **elemento** elemento.</span><span class="sxs-lookup"><span data-stu-id="d6804-282">hello dropdown items are specified within hello **Properties** element using an **Item** element.</span></span> <span data-ttu-id="d6804-283">Hola **identificador** para cada **elemento** debe ser único y una variable de R válida.</span><span class="sxs-lookup"><span data-stu-id="d6804-283">hello **id** for each **Item** must be unique and a valid R variable.</span></span> <span data-ttu-id="d6804-284">Hola valo hello **nombre** de un **elemento** actúa como texto hello que se ve y valor de Hola que se pasa la función toohello R.</span><span class="sxs-lookup"><span data-stu-id="d6804-284">hello value of hello **name** of an **Item** serves as both hello text that you see and hello value that is passed toohello R function.</span></span>

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* <span data-ttu-id="d6804-285">*Propiedades opcionales*:</span><span class="sxs-lookup"><span data-stu-id="d6804-285">*Optional Properties*:</span></span>
  * <span data-ttu-id="d6804-286">**valor predeterminado** : hello valor de la propiedad predeterminada de hello debe corresponder con un valor de identificador de uno de hello **elemento** elementos.</span><span class="sxs-lookup"><span data-stu-id="d6804-286">**default** - hello value for hello default property must correspond with an id value from one of hello **Item** elements.</span></span>

### <a name="auxiliary-files"></a><span data-ttu-id="d6804-287">Archivos auxiliares</span><span class="sxs-lookup"><span data-stu-id="d6804-287">Auxiliary Files</span></span>
<span data-ttu-id="d6804-288">Cualquier archivo que se coloca en el archivo ZIP de módulo personalizado es continuo toobe disponible para su uso durante el tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="d6804-288">Any file that is placed in your custom module ZIP file is going toobe available for use during execution time.</span></span> <span data-ttu-id="d6804-289">Se conservarán todas las estructuras de directorios presentes.</span><span class="sxs-lookup"><span data-stu-id="d6804-289">Any directory structures present are preserved.</span></span> <span data-ttu-id="d6804-290">Esto significa que funciona de origen de archivo Hola mismo localmente y en la ejecución de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6804-290">This means that file sourcing works hello same locally and in Azure Machine Learning execution.</span></span> 

> [!NOTE]
> <span data-ttu-id="d6804-291">Tenga en cuenta que todos los archivos extraídos too'src' directory para que todas las rutas de acceso deben tener ' src /' prefijo.</span><span class="sxs-lookup"><span data-stu-id="d6804-291">Notice that all files are extracted too‘src’ directory so all paths should have ‘src/’ prefix.</span></span>
> 
> 

<span data-ttu-id="d6804-292">Por ejemplo, suponga que desee tooremove las filas con NAs de conjunto de datos de Hola y quita todas las filas duplicadas, antes de generar en CustomAddRows y ya ha escrito una función de R que lo hace en un archivo RemoveDupNARows.R:</span><span class="sxs-lookup"><span data-stu-id="d6804-292">For example, say you want tooremove any rows with NAs from hello dataset, and also remove any duplicate rows, before outputting it into CustomAddRows, and you’ve already written an R function that does that in a file RemoveDupNARows.R:</span></span>

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
<span data-ttu-id="d6804-293">Puede obtener el archivo auxiliar RemoveDupNARows.R Hola Hola CustomAddRows función:</span><span class="sxs-lookup"><span data-stu-id="d6804-293">You can source hello auxiliary file RemoveDupNARows.R in hello CustomAddRows function:</span></span>

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

<span data-ttu-id="d6804-294">A continuación, cargue un archivo zip que contenga "myAddRows.R", "myAddRows.xml" y "removeDupNARows.R" como módulo de R personalizado.</span><span class="sxs-lookup"><span data-stu-id="d6804-294">Next, upload a zip file containing ‘CustomAddRows.R’, ‘CustomAddRows.xml’, and ‘RemoveDupNARows.R’ as a custom R module.</span></span>

## <a name="execution-environment"></a><span data-ttu-id="d6804-295">Entorno de ejecución</span><span class="sxs-lookup"><span data-stu-id="d6804-295">Execution Environment</span></span>
<span data-ttu-id="d6804-296">entorno de ejecución de Hola para script de Hola R usa Hola misma versión de R que hello **ejecutar Script de R** módulo y puede usar Hola mismo predeterminado paquetes.</span><span class="sxs-lookup"><span data-stu-id="d6804-296">hello execution environment for hello R script uses hello same version of R as hello **Execute R Script** module and can use hello same default packages.</span></span> <span data-ttu-id="d6804-297">También puede agregar más módulo personalizado de R paquetes tooyour incluyéndolos en el paquete comprimido de módulo personalizado de Hola.</span><span class="sxs-lookup"><span data-stu-id="d6804-297">You can also add additional R packages tooyour custom module by including them in hello custom module zip package.</span></span> <span data-ttu-id="d6804-298">Solo tiene que cargarlos en el script de R como lo haría en su propio entorno de R.</span><span class="sxs-lookup"><span data-stu-id="d6804-298">Just load them in your R script as you would in your own R environment.</span></span> 

<span data-ttu-id="d6804-299">**Limitaciones del entorno de ejecución de hello** incluyen:</span><span class="sxs-lookup"><span data-stu-id="d6804-299">**Limitations of hello execution environment** include:</span></span>

* <span data-ttu-id="d6804-300">Sistema de archivos no persistentes: no se conservan los archivos escritos cuando se ejecuta el módulo personalizado de Hola durante varias ejecuciones de hello mismo módulo.</span><span class="sxs-lookup"><span data-stu-id="d6804-300">Non-persistent file system: Files written when hello custom module is run are not persisted across multiple runs of hello same module.</span></span>
* <span data-ttu-id="d6804-301">Sin acceso de red</span><span class="sxs-lookup"><span data-stu-id="d6804-301">No network access</span></span>

