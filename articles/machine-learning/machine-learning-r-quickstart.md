---
title: "tutorial de aaaQuickstart de lenguaje de R para el aprendizaje automático | Documentos de Microsoft"
description: "Use este tutorial tooget iniciada rápidamente con lenguaje Hola R toocreate de estudio de aprendizaje automático de Azure una solución de previsión de programación de R."
keywords: "inicio rápido, idioma r, lenguaje de programación r, tutorial de programación r"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="3c013-104">Tutorial de inicio rápido de lenguaje de programación de hello R de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="3c013-104">Quickstart tutorial for hello R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="3c013-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="3c013-105">Introduction</span></span>
<span data-ttu-id="3c013-106">Este tutorial de inicio rápido le ayuda a empezar rápidamente a ampliar el aprendizaje automático de Azure mediante el lenguaje de programación de hello R.</span><span class="sxs-lookup"><span data-stu-id="3c013-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using hello R programming language.</span></span> <span data-ttu-id="3c013-107">Seguir este tutorial toocreate de programación de R, probar y ejecutar código de R en aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c013-107">Follow this R programming tutorial toocreate, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="3c013-108">Cuando se trabaja a través del tutorial, creará una solución de previsión completa mediante el lenguaje de hello R en aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c013-108">As you work through tutorial, you will create a complete forecasting solution by using hello R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="3c013-109">Aprendizaje automático de Microsoft Azure contiene muchos módulos versátiles de manipulación de datos y aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="3c013-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="3c013-110">lenguaje R eficaz de Hola se ha descrito como Hola lengua franca de análisis.</span><span class="sxs-lookup"><span data-stu-id="3c013-110">hello powerful R language has been described as hello lingua franca of analytics.</span></span> <span data-ttu-id="3c013-111">Por suerte, manipulación de datos y análisis en aprendizaje automático de Azure puede ampliarse mediante el uso de R. Esta combinación proporciona Hola escalabilidad y facilidad de implementación de aprendizaje automático de Azure con la flexibilidad de Hola y análisis profundo de R.</span><span class="sxs-lookup"><span data-stu-id="3c013-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides hello scalability and ease of deployment of Azure Machine Learning with hello flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a><span data-ttu-id="3c013-112">Conjunto de datos de previsión y Hola</span><span class="sxs-lookup"><span data-stu-id="3c013-112">Forecasting and hello dataset</span></span>
<span data-ttu-id="3c013-113">La previsión es un método de análisis ampliamente utilizado y bastante útil.</span><span class="sxs-lookup"><span data-stu-id="3c013-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="3c013-114">Intervalo de predecir las ventas de temporada elementos, determinar los niveles de inventario óptimo, variables macroeconómicas toopredicting usos comunes.</span><span class="sxs-lookup"><span data-stu-id="3c013-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, toopredicting macroeconomic variables.</span></span> <span data-ttu-id="3c013-115">La previsión suele realizarse con modelos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="3c013-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="3c013-116">Datos de series temporales son datos en el que los valores de hello tienen un índice de tiempo.</span><span class="sxs-lookup"><span data-stu-id="3c013-116">Time series data is data in which hello values have a time index.</span></span> <span data-ttu-id="3c013-117">índice de tiempo de Hello puede ser normal, por ejemplo, cada mes o cada minuto, o irregulares.</span><span class="sxs-lookup"><span data-stu-id="3c013-117">hello time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="3c013-118">Los modelos de serie temporal se basan en datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="3c013-118">A time series model is based on time series data.</span></span> <span data-ttu-id="3c013-119">lenguaje de programación de Hello R contiene un marco de trabajo flexible y una amplia análisis de datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="3c013-119">hello R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="3c013-120">En esta guía de inicio rápido, trabajaremos con los productos lácteos de California y los datos de precios.</span><span class="sxs-lookup"><span data-stu-id="3c013-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="3c013-121">Estos datos incluyen información mensual en producción de hello de varios productos lácteos y el precio de Hola de fat leche, un estándar de la prueba comparativa.</span><span class="sxs-lookup"><span data-stu-id="3c013-121">This data includes monthly information on hello production of several dairy products and hello price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="3c013-122">Hola los datos utilizados en este artículo, junto con scripts de R, pueden ser [descargarse aquí][download].</span><span class="sxs-lookup"><span data-stu-id="3c013-122">hello data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="3c013-123">Estos datos originalmente se sintetizan de información disponible en hello Universidad de Wisconsin en http://future.aae.wisc.edu/tab/production.html.</span><span class="sxs-lookup"><span data-stu-id="3c013-123">This data was originally synthesized from information available from hello University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="3c013-124">Organización</span><span class="sxs-lookup"><span data-stu-id="3c013-124">Organization</span></span>
<span data-ttu-id="3c013-125">Tal y como se muestra cómo toocreate, probar y ejecutar código de R de manipulación de datos y análisis en el entorno de aprendizaje automático de Azure de hello, que se progresamos en varios pasos.</span><span class="sxs-lookup"><span data-stu-id="3c013-125">We will progress through several steps as you learn how toocreate, test and execute analytics and data manipulation R code in hello Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="3c013-126">En primer lugar, exploraremos conceptos básicos de Hola de usando el lenguaje de hello R en el entorno de estudio de aprendizaje automático de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-126">First we will explore hello basics of using hello R language in hello Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="3c013-127">A continuación, que progresamos toodiscussing diversos aspectos de la E/S de datos, código de R y gráficos en el entorno de aprendizaje automático de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-127">Then we progress toodiscussing various aspects of I/O for data, R code and graphics in hello Azure Machine Learning environment.</span></span>
* <span data-ttu-id="3c013-128">A continuación, se construirá primera parte de nuestra solución previsión de hello mediante la creación de código para la limpieza de datos y transformación.</span><span class="sxs-lookup"><span data-stu-id="3c013-128">We will then construct hello first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="3c013-129">Con nuestros datos preparados se realizará un análisis de correlaciones de hello entre algunas de las variables de hello en el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="3c013-129">With our data prepared we will perform an analysis of hello correlations between several of hello variables in our dataset.</span></span>
* <span data-ttu-id="3c013-130">Por último, crearemos un modelo de previsión de serie temporal estacional para la producción de leche.</span><span class="sxs-lookup"><span data-stu-id="3c013-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <span data-ttu-id="3c013-131"><a id="mlstudio"></a>Interacción con el lenguaje R para Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="3c013-131"><a id="mlstudio"></a>Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="3c013-132">En esta sección le guiará por algunos conceptos básicos de la interacción con el lenguaje de programación de hello R en el entorno de estudio de aprendizaje automático de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-132">This section takes you through some basics of interacting with hello R programming language in hello Machine Learning Studio environment.</span></span> <span data-ttu-id="3c013-133">lenguaje de Hello R proporciona una herramienta eficaz toocreate personalizar datos y análisis manipulación módulos dentro del entorno de aprendizaje automático de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-133">hello R language provides a powerful tool toocreate customized analytics and data manipulation modules within hello Azure Machine Learning environment.</span></span>

<span data-ttu-id="3c013-134">Usaré RStudio toodevelop, probar y depurar código de R en una pequeña escala.</span><span class="sxs-lookup"><span data-stu-id="3c013-134">I will use RStudio toodevelop, test and debug R code on a small scale.</span></span> <span data-ttu-id="3c013-135">Este código es, a continuación, cortar y pegar en una [ejecutar Script de R] [ execute-r-script] módulo en estudio de aprendizaje automático listo toorun.</span><span class="sxs-lookup"><span data-stu-id="3c013-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready toorun.</span></span>  

### <a name="hello-execute-r-script-module"></a><span data-ttu-id="3c013-136">módulo ejecutar Script de R de Hola</span><span class="sxs-lookup"><span data-stu-id="3c013-136">hello Execute R Script module</span></span>
<span data-ttu-id="3c013-137">En estudio de aprendizaje automático, se ejecutan los scripts de R en hello [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-137">Within Machine Learning Studio, R scripts are run within hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="3c013-138">Un ejemplo de Hola [ejecutar Script de R] [ execute-r-script] módulo en estudio de aprendizaje automático se muestra en la figura 1.</span><span class="sxs-lookup"><span data-stu-id="3c013-138">An example of hello [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![Lenguaje de programación R: módulo ejecutar Script de R de hello seleccionado en estudio de aprendizaje automático][1]

<span data-ttu-id="3c013-140">*Figura 1. entorno de estudio de aprendizaje automático de Hello mostrar hello ejecutar Script de R módulo seleccionado.*</span><span class="sxs-lookup"><span data-stu-id="3c013-140">*Figure 1. hello Machine Learning Studio environment showing hello Execute R Script module selected.*</span></span>

<span data-ttu-id="3c013-141">Que hace referencia tooFigure 1, veamos algunos de los elementos clave de hello del entorno de estudio de aprendizaje automático de Hola para trabajar con hello [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-141">Referring tooFigure 1, let's look at some of hello key parts of hello Machine Learning Studio environment for working with hello [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="3c013-142">módulos de Hello en el experimento de Hola se muestran en el panel central de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-142">hello modules in hello experiment are shown in hello center pane.</span></span>
* <span data-ttu-id="3c013-143">parte superior de Hello del panel derecho de hello contiene un tooview de ventana y editar los scripts de R.</span><span class="sxs-lookup"><span data-stu-id="3c013-143">hello upper part of hello right pane contains a window tooview and edit your R scripts.</span></span>  
* <span data-ttu-id="3c013-144">parte inferior de Hello del panel derecho muestra algunas propiedades de hello [ejecutar Script de R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="3c013-144">hello lower part of right pane shows some properties of hello [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="3c013-145">Puede ver los registros de error y de salida de hello haciendo clic en las zonas adecuado Hola de este panel.</span><span class="sxs-lookup"><span data-stu-id="3c013-145">You can view hello error and output logs by clicking on hello appropriate spots of this pane.</span></span>

<span data-ttu-id="3c013-146">Por supuesto, analizaremos hello [ejecutar Script de R] [ execute-r-script] con más detalle en el resto de Hola de este documento.</span><span class="sxs-lookup"><span data-stu-id="3c013-146">We will, of course, be discussing hello [Execute R Script][execute-r-script] in greater detail in hello rest of this document.</span></span>

<span data-ttu-id="3c013-147">Cuando se utilicen funciones complejas de R, es recomendable editar, probar y depurar el código en RStudio.</span><span class="sxs-lookup"><span data-stu-id="3c013-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="3c013-148">Al igual que con cualquier desarrollo de software, amplíe el código de forma incremental y pruébelo en casos de prueba más sencillos. </span><span class="sxs-lookup"><span data-stu-id="3c013-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="3c013-149">A continuación, cortar y pegar las funciones en la ventana de script de Hola R de hello [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-149">Then cut and paste your functions into hello R script window of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="3c013-150">Este enfoque permite que tooharness RStudio entorno de desarrollo integrado (IDE) de Hola y Hola potencia de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c013-150">This approach allows you tooharness both hello RStudio integrated development environment (IDE) and hello power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="3c013-151">Ejecución del código R</span><span class="sxs-lookup"><span data-stu-id="3c013-151">Execute R code</span></span>
<span data-ttu-id="3c013-152">Cualquier código de R en hello [ejecutar Script de R] [ execute-r-script] módulo se ejecutará cuando se ejecute el experimento de Hola haciendo clic en hello **ejecutar** botón.</span><span class="sxs-lookup"><span data-stu-id="3c013-152">Any R code in hello [Execute R Script][execute-r-script] module will execute when you run hello experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="3c013-153">Cuando haya finalizado la ejecución, aparecerá una marca de verificación en hello [ejecutar Script de R] [ execute-r-script] icono.</span><span class="sxs-lookup"><span data-stu-id="3c013-153">When execution has completed, a check mark will appear on hello [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="3c013-154">Codificación R defensiva para Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="3c013-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="3c013-155">Si está desarrollando código R para un servicio web utilizando Aprendizaje automático de Azure, deberá planear cómo tratará el código las entradas de datos inesperadas y las excepciones.</span><span class="sxs-lookup"><span data-stu-id="3c013-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="3c013-156">toomaintain claridad, he no incluí gran parte de manera Hola de comprobación o control de excepciones en la mayoría de los ejemplos de código de hello mostrados.</span><span class="sxs-lookup"><span data-stu-id="3c013-156">toomaintain clarity, I have not included much in hello way of checking or exception handling in most of hello code examples shown.</span></span> <span data-ttu-id="3c013-157">Sin embargo, conforme avancemos compartiré varios ejemplos de funciones mediante la capacidad de control de excepciones de R.</span><span class="sxs-lookup"><span data-stu-id="3c013-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="3c013-158">Si necesita un tratamiento más completado del control de excepciones de R, recomienda leer secciones aplicables de Hola de libro de hello Wickham enumerado en [Apéndice B - más información](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="3c013-158">If you need a more complete treatment of R exception handling, I recommend you read hello applicable sections of hello book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="3c013-159">Depuración y prueba de R en Estudio de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="3c013-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="3c013-160">tooreiterate, recomienda probar y depurar el código de R en una pequeña escala en RStudio.</span><span class="sxs-lookup"><span data-stu-id="3c013-160">tooreiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="3c013-161">Sin embargo, hay casos donde debe tootrack problemas de código de R en hello [ejecutar Script de R] [ execute-r-script] propio.</span><span class="sxs-lookup"><span data-stu-id="3c013-161">However, there are cases where you will need tootrack down R code problems in hello [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="3c013-162">Además, es recomendable toocheck los resultados en estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="3c013-162">In addition, it is good practice toocheck your results in Machine Learning Studio.</span></span>

<span data-ttu-id="3c013-163">Resultado de la ejecución del código R y en la plataforma de aprendizaje automático de Azure de Hola Hola se encuentra principalmente en salida.log.</span><span class="sxs-lookup"><span data-stu-id="3c013-163">Output from hello execution of your R code and on hello Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="3c013-164">Se mostrará información adicional en el archivo error.log.</span><span class="sxs-lookup"><span data-stu-id="3c013-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="3c013-165">Si se produce un error en estudio de aprendizaje automático mientras se ejecuta el código de R, la primera línea de conducta debe toolook en error.log.</span><span class="sxs-lookup"><span data-stu-id="3c013-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be toolook at error.log.</span></span> <span data-ttu-id="3c013-166">Este archivo puede contener toohelp de mensajes de error útil entender y corrija el error.</span><span class="sxs-lookup"><span data-stu-id="3c013-166">This file can contain useful error messages toohelp you understand and correct your error.</span></span> <span data-ttu-id="3c013-167">tooview error.log, haga clic en **Ver registro de errores** en hello **panel Propiedades** para hello [ejecutar Script de R] [ execute-r-script] que contiene el error de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-167">tooview error.log, click on **View error log** on hello **properties pane** for hello [Execute R Script][execute-r-script] containing hello error.</span></span>

<span data-ttu-id="3c013-168">Por ejemplo, se ejecutó Hola siguiente código de R, con un variable y sin definir, en un [ejecutar Script de R] [ execute-r-script] módulo:</span><span class="sxs-lookup"><span data-stu-id="3c013-168">For example, I ran hello following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="3c013-169">Este código produce un error tooexecute, lo que produce una condición de error.</span><span class="sxs-lookup"><span data-stu-id="3c013-169">This code fails tooexecute, resulting in an error condition.</span></span> <span data-ttu-id="3c013-170">Al hacer clic en **Ver registro de errores** en hello **panel Propiedades** produce Hola presentación que se muestra en la figura 2.</span><span class="sxs-lookup"><span data-stu-id="3c013-170">Clicking on **View error log** on hello **properties pane** produces hello display shown in Figure 2.</span></span>

  ![Mensaje de error emergente][2]

<span data-ttu-id="3c013-172">*Ilustración 2. Mensaje de error emergente.*</span><span class="sxs-lookup"><span data-stu-id="3c013-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="3c013-173">Parece que necesitamos toolook salida.log toosee Hola R mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="3c013-173">It looks like we need toolook in output.log toosee hello R error message.</span></span> <span data-ttu-id="3c013-174">Haga clic en hello [ejecutar Script de R] [ execute-r-script] y, a continuación, haga clic en hello **ver salida.log** elemento en hello **panel Propiedades** toohello derecha.</span><span class="sxs-lookup"><span data-stu-id="3c013-174">Click on hello [Execute R Script][execute-r-script] and then click on hello **View output.log** item on hello **properties pane** toohello right.</span></span> <span data-ttu-id="3c013-175">Se abre una nueva ventana del explorador, y yo vemos siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-175">A new browser window opens, and I see hello following.</span></span>

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="3c013-176">Este mensaje de error no contiene sorpresas e identifique claramente el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-176">This error message contains no surprises and clearly identifies hello problem.</span></span>

<span data-ttu-id="3c013-177">valor de hello tooinspect de cualquier objeto de R, puede imprimir estos archivos de valores toohello salida.log.</span><span class="sxs-lookup"><span data-stu-id="3c013-177">tooinspect hello value of any object in R, you can print these values toohello output.log file.</span></span> <span data-ttu-id="3c013-178">las reglas de Hola para examinar el objeto de los valores son básicamente iguales Hola como en una sesión interactiva de R.</span><span class="sxs-lookup"><span data-stu-id="3c013-178">hello rules for examining object values are essentially hello same as in an interactive R session.</span></span> <span data-ttu-id="3c013-179">Por ejemplo, si escribe un nombre de variable en una línea, valor de hello del objeto de hello será toohello impreso salida.log archivo.</span><span class="sxs-lookup"><span data-stu-id="3c013-179">For example, if you type a variable name on a line, hello value of hello object will be printed toohello output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="3c013-180">Paquetes de Estudio de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="3c013-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="3c013-181">Aprendizaje automático de Azure incluye más de 350 paquetes del lenguaje R preinstalados.</span><span class="sxs-lookup"><span data-stu-id="3c013-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="3c013-182">Puede usar Hola después el código de hello [ejecutar Script de R] [ execute-r-script] módulo tooretrieve una lista de hello preinstalado paquetes.</span><span class="sxs-lookup"><span data-stu-id="3c013-182">You can use hello following code in hello [Execute R Script][execute-r-script] module tooretrieve a list of hello preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="3c013-183">Si no entiende la última línea de este código de hello en el momento de hello, siga leyendo.</span><span class="sxs-lookup"><span data-stu-id="3c013-183">If you don't understand hello last line of this code at hello moment, read on.</span></span> <span data-ttu-id="3c013-184">En el resto de Hola de este documento, trataremos mucho uso de R en el entorno de aprendizaje automático de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-184">In hello rest of this document we will extensively discuss using R in hello Azure Machine Learning environment.</span></span>

### <a name="introduction-toorstudio"></a><span data-ttu-id="3c013-185">Introducción tooRStudio</span><span class="sxs-lookup"><span data-stu-id="3c013-185">Introduction tooRStudio</span></span>
<span data-ttu-id="3c013-186">RStudio es un IDE ampliamente utilizado para R. Usaré RStudio para editar, probar y depurar parte del código de hello R utilizada en esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="3c013-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of hello R code used in this quick start guide.</span></span> <span data-ttu-id="3c013-187">Una vez probados y listo código R, simplemente cortar y pegar desde el editor de RStudio hello en un estudio de aprendizaje automático [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-187">Once R code is tested and ready, you simply cut and paste from hello RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="3c013-188">Si no tiene el lenguaje de programación de hello R instalado en su equipo de escritorio, recomienda que hacerlo ahora.</span><span class="sxs-lookup"><span data-stu-id="3c013-188">If you do not have hello R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="3c013-189">Descargas gratuitas de lenguaje de código abierto R están disponibles en hello red completa de archivo de R (CRAN) en [http://www.r-project.org/](http://www.r-project.org/).</span><span class="sxs-lookup"><span data-stu-id="3c013-189">Free downloads of open source R language are available at hello Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="3c013-190">Hay descargas disponibles para Windows, Mac OS y Linux/UNIX.</span><span class="sxs-lookup"><span data-stu-id="3c013-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="3c013-191">Elija un reflejo cercano y siga las instrucciones de descarga de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-191">Choose a nearby mirror and follow hello download directions.</span></span> <span data-ttu-id="3c013-192">Además, CRAN contiene una gran cantidad de paquetes de manipulación de datos y análisis de utilidad.</span><span class="sxs-lookup"><span data-stu-id="3c013-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="3c013-193">Si está tooRStudio nueva, debe descargar e instalar la versión de escritorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-193">If you are new tooRStudio, you should download and install hello desktop version.</span></span> <span data-ttu-id="3c013-194">Puede encontrar Hola que rstudio descarga para Windows, Mac OS y Linux/UNIX a http://www.rstudio.com/products/RStudio/.</span><span class="sxs-lookup"><span data-stu-id="3c013-194">You can find hello RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="3c013-195">Siga las instrucciones de hello proporcionadas tooinstall RStudio en su equipo de escritorio.</span><span class="sxs-lookup"><span data-stu-id="3c013-195">Follow hello directions provided tooinstall RStudio on your desktop machine.</span></span>  

<span data-ttu-id="3c013-196">Una introducción al tutorial tooRStudio está disponible en https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span><span class="sxs-lookup"><span data-stu-id="3c013-196">A tutorial introduction tooRStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="3c013-197">En el [Apéndice A][appendixa], encontrará información adicional sobre el uso de RStudio.</span><span class="sxs-lookup"><span data-stu-id="3c013-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <span data-ttu-id="3c013-198"><a id="scriptmodule"></a>Obtener datos dentro y fuera del módulo ejecutar Script de R de Hola</span><span class="sxs-lookup"><span data-stu-id="3c013-198"><a id="scriptmodule"></a>Get data in and out of hello Execute R Script module</span></span>
<span data-ttu-id="3c013-199">En esta sección, veremos cómo obtener los datos dentro y fuera de hello [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-199">In this section we will discuss how you get data into and out of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="3c013-200">Analizaremos cómo toohandle diversos tipos de datos de lectura dentro y fuera de hello [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-200">We will review how toohandle various data types read into and out of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="3c013-201">Hola de código completo de esta sección se encuentra en el archivo zip de Hola que descargó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3c013-201">hello complete code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="3c013-202">Carga y comprobación de datos en Estudio de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="3c013-202">Load and check data in Machine Learning Studio</span></span>
#### <span data-ttu-id="3c013-203"><a id="loading"></a>El conjunto de datos de carga Hola</span><span class="sxs-lookup"><span data-stu-id="3c013-203"><a id="loading"></a>Load hello dataset</span></span>
<span data-ttu-id="3c013-204">Empezaremos cargar hello **csdairydata.csv** archivo en estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c013-204">We will start by loading hello **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="3c013-205">Iniciar su entorno Estudio de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="3c013-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="3c013-206">Haga clic en **+ nuevo** en hello parte inferior izquierda de la pantalla y seleccione **conjunto de datos**.</span><span class="sxs-lookup"><span data-stu-id="3c013-206">Click on **+ NEW** at hello lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="3c013-207">Seleccione **de archivo Local**y, a continuación, **examinar** archivo de hello tooselect.</span><span class="sxs-lookup"><span data-stu-id="3c013-207">Select **From Local File**, and then **Browse** tooselect hello file.</span></span>
* <span data-ttu-id="3c013-208">Asegúrese de que ha seleccionado **archivo CSV genérico con encabezado (.csv)** como tipo de hello para el conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-208">Make sure you have selected **Generic CSV file with header (.csv)** as hello type for hello dataset.</span></span>
* <span data-ttu-id="3c013-209">Haga clic en la marca de verificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-209">Click hello check mark.</span></span>
* <span data-ttu-id="3c013-210">Después de que se ha cargado el conjunto de datos de hello, debería ver Hola nuevo conjunto de datos haciendo clic en hello **conjuntos de datos** ficha.</span><span class="sxs-lookup"><span data-stu-id="3c013-210">After hello dataset has been uploaded, you should see hello new dataset by clicking on hello **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="3c013-211">Creación de un experimento</span><span class="sxs-lookup"><span data-stu-id="3c013-211">Create an experiment</span></span>
<span data-ttu-id="3c013-212">Ahora que tenemos algunos datos en estudio de aprendizaje automático, necesitamos toocreate un análisis de experimento toodo Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-212">Now that we have some data in Machine Learning Studio, we need toocreate an experiment toodo hello analysis.</span></span>  

* <span data-ttu-id="3c013-213">Haga clic en **+ nuevo** en hello inferior izquierdo y seleccione **experimento**, a continuación, **en blanco de experimento**.</span><span class="sxs-lookup"><span data-stu-id="3c013-213">Click on **+ NEW** at hello lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="3c013-214">Puede nombrar el experimento mediante la selección y modificar, Hola **experimento creado en...**  el título a la parte superior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-214">You can name your experiment by selecting, and modifying, hello **Experiment created on ...** title at hello top of hello page.</span></span> <span data-ttu-id="3c013-215">Por ejemplo, cambiar demasiado**CA lácteos Analysis**.</span><span class="sxs-lookup"><span data-stu-id="3c013-215">For example, changing it too**CA Dairy Analysis**.</span></span>
* <span data-ttu-id="3c013-216">Izquierda Hola de página de experimento de hello, expanda **conjuntos de datos guardados**y, a continuación, **Mis conjuntos de datos**.</span><span class="sxs-lookup"><span data-stu-id="3c013-216">On hello left of hello experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="3c013-217">Debería ver Hola **cadairydata.csv** que haya cargado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3c013-217">You should see hello **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="3c013-218">Hola de arrastrar y colocar **csdairydata.csv dataset** en el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-218">Drag and drop hello **csdairydata.csv dataset** onto hello experiment.</span></span>
* <span data-ttu-id="3c013-219">Hola **búsqueda experimentar elementos** cuadro en la parte superior de hello del panel izquierdo de hello, tipo [ejecutar Script de R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="3c013-219">In hello **Search experiment items** box on hello top of hello left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="3c013-220">Verá módulo Hola aparecen en la lista de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-220">You will see hello module appear in hello search list.</span></span>
* <span data-ttu-id="3c013-221">Hola de arrastrar y colocar [ejecutar Script de R] [ execute-r-script] módulo en el palet.</span><span class="sxs-lookup"><span data-stu-id="3c013-221">Drag and drop hello [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="3c013-222">Conecte la salida de hello de hello **csdairydata.csv dataset** entrada izquierda toohello (**Dataset1**) de hello [ejecutar Script de R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="3c013-222">Connect hello output of hello **csdairydata.csv dataset** toohello leftmost input (**Dataset1**) of hello [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="3c013-223">**No olvide tooclick en 'Guardar'.**</span><span class="sxs-lookup"><span data-stu-id="3c013-223">**Don't forget tooclick on 'Save'!**</span></span>  

<span data-ttu-id="3c013-224">En este punto el experimento debería tener un aspecto similar al de la ilustración 3.</span><span class="sxs-lookup"><span data-stu-id="3c013-224">At this point your experiment should look something like Figure 3.</span></span>

![Hola CA lácteos Analysis experimentar con el conjunto de datos y módulo ejecutar Script de R][3]

<span data-ttu-id="3c013-226">*Figura 3. Hola CA lácteos Analysis experimentar con el conjunto de datos y módulo ejecutar Script de R.*</span><span class="sxs-lookup"><span data-stu-id="3c013-226">*Figure 3. hello CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-hello-data"></a><span data-ttu-id="3c013-227">Comprobar datos Hola</span><span class="sxs-lookup"><span data-stu-id="3c013-227">Check on hello data</span></span>
<span data-ttu-id="3c013-228">Echemos un vistazo a los datos de saludo que se han cargado en el experimento.</span><span class="sxs-lookup"><span data-stu-id="3c013-228">Let's have a look at hello data we have loaded into our experiment.</span></span> <span data-ttu-id="3c013-229">En el experimento de hello, haga clic en salida de hello de hello **conjunto de datos de cadairydata.csv** y seleccione **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="3c013-229">In hello experiment, click on hello output of hello **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="3c013-230">Debería ver algo parecido a lo que se muestra en la ilustración 4.</span><span class="sxs-lookup"><span data-stu-id="3c013-230">You should see something like Figure 4.</span></span>  

![Resumen del conjunto de datos de hello cadairydata.csv][4]

<span data-ttu-id="3c013-232">*Ilustración 4. Resumen del conjunto de datos de hello cadairydata.csv.*</span><span class="sxs-lookup"><span data-stu-id="3c013-232">*Figure 4. Summary of hello cadairydata.csv dataset.*</span></span>

<span data-ttu-id="3c013-233">En esta vista hay una gran cantidad de información útil.</span><span class="sxs-lookup"><span data-stu-id="3c013-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="3c013-234">Podemos ver Hola primera varias filas de ese conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="3c013-234">We can see hello first several rows of that dataset.</span></span> <span data-ttu-id="3c013-235">Si se selecciona una columna, Hola sección de estadísticas de muestra para obtener más información acerca de la columna de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-235">If we select a column, hello Statistics section shows more information about hello column.</span></span> <span data-ttu-id="3c013-236">Por ejemplo, fila de tipo de característica de hello muestra qué tipos de datos estudio de aprendizaje automático de Azure asigna la columna toohello.</span><span class="sxs-lookup"><span data-stu-id="3c013-236">For example, hello Feature Type row shows us what data types Azure Machine Learning Studio assigned toohello column.</span></span> <span data-ttu-id="3c013-237">Tener una visión rápida parecido a esto es una buena comprobación antes de empezar cualquier trabajo grave toodo.</span><span class="sxs-lookup"><span data-stu-id="3c013-237">Having a quick look like this is a good sanity check before we start toodo any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="3c013-238">Primer script de R</span><span class="sxs-lookup"><span data-stu-id="3c013-238">First R script</span></span>
<span data-ttu-id="3c013-239">Vamos a crear un simple tooexperiment con script primera R en estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c013-239">Let's create a simple first R script tooexperiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="3c013-240">He creado y probado Hola siguiente secuencia de comandos en RStudio.</span><span class="sxs-lookup"><span data-stu-id="3c013-240">I have created and tested hello following script in RStudio.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="3c013-241">Ahora necesito tootransfer esta tooAzure script estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="3c013-241">Now I need tootransfer this script tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="3c013-242">Basta con cortar y pegar.</span><span class="sxs-lookup"><span data-stu-id="3c013-242">I could simply cut and paste.</span></span> <span data-ttu-id="3c013-243">Sin embargo, en este caso, transferiré el script de código R mediante un archivo zip.</span><span class="sxs-lookup"><span data-stu-id="3c013-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-toohello-execute-r-script-module"></a><span data-ttu-id="3c013-244">Módulo de ejecutar Script de R toohello de entrada de datos</span><span class="sxs-lookup"><span data-stu-id="3c013-244">Data input toohello Execute R Script module</span></span>
<span data-ttu-id="3c013-245">Echemos un vistazo a Hola entradas toohello [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-245">Let's have a look at hello inputs toohello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="3c013-246">En este ejemplo se leerá los datos de hello California lecheras en hello [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-246">In this example we will read hello California dairy data into hello [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="3c013-247">Hay tres entradas posibles para hello [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-247">There are three possible inputs for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="3c013-248">Puede usar cualquiera de estas entradas o todas ellas, dependiendo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c013-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="3c013-249">También es perfectamente razonable toouse una R script que no toma ninguna entrada.</span><span class="sxs-lookup"><span data-stu-id="3c013-249">It is also perfectly reasonable toouse an R script that takes no input at all.</span></span>  

<span data-ttu-id="3c013-250">Echemos un vistazo a cada una de estas entradas, desde la izquierda tooright.</span><span class="sxs-lookup"><span data-stu-id="3c013-250">Let's look at each of these inputs, going from left tooright.</span></span> <span data-ttu-id="3c013-251">Puede ver los nombres Hola cada una de las entradas de hello colocando el cursor sobre entrada hello y leer información sobre herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-251">You can see hello names of each of hello inputs by placing your cursor over hello input and reading hello tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="3c013-252">Paquete de script</span><span class="sxs-lookup"><span data-stu-id="3c013-252">Script Bundle</span></span>
<span data-ttu-id="3c013-253">Hello proporcionados por el paquete de scripts permite toopass Hola contenido de un archivo zip en [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-253">hello Script Bundle input allows you toopass hello contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="3c013-254">Puede usar uno de hello después el contenido de hello tooread de comandos del archivo zip de hello en el código de R.</span><span class="sxs-lookup"><span data-stu-id="3c013-254">You can use one of hello following commands tooread hello contents of hello zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="3c013-255">Aprendizaje automático de Azure trata los archivos en zip hello como si fueran en hello src / directory, por lo que necesita tooprefix nombres de los archivos con este nombre de directorio.</span><span class="sxs-lookup"><span data-stu-id="3c013-255">Azure Machine Learning treats files in hello zip as if they are in hello src/ directory, so you need tooprefix your file names with this directory name.</span></span> <span data-ttu-id="3c013-256">Por ejemplo, si hello zip contiene archivos de hello `yourfile.R` y `yourData.rdata` en raíz de Hola de zip Hola, ¿tratarlos como `src/yourfile.R` y `src/yourData.rdata` al usar `source` y `load`.</span><span class="sxs-lookup"><span data-stu-id="3c013-256">For example, if hello zip contains hello files `yourfile.R` and `yourData.rdata` in hello root of hello zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="3c013-257">Ya se explicó conjuntos de datos de carga en [cargar el conjunto de datos de hello](#loading).</span><span class="sxs-lookup"><span data-stu-id="3c013-257">We already discussed loading datasets in [Loading hello dataset](#loading).</span></span> <span data-ttu-id="3c013-258">Una vez que haya creado y probado script de Hola R que se muestra en la sección anterior de hello, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="3c013-258">Once you have created and tested hello R script shown in hello previous section, do hello following:</span></span>

1. <span data-ttu-id="3c013-259">Guardar script de Hola R en una. Archivo de R.</span><span class="sxs-lookup"><span data-stu-id="3c013-259">Save hello R script into a .R file.</span></span> <span data-ttu-id="3c013-260">Llamaré a mi archivo de script "simpleplot.R".</span><span class="sxs-lookup"><span data-stu-id="3c013-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="3c013-261">Este es el contenido de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-261">Here's hello contents.</span></span>
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="3c013-262">Cree un archivo zip y copie el script en el archivo zip.</span><span class="sxs-lookup"><span data-stu-id="3c013-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="3c013-263">En Windows, puede haga doble clic en el archivo hello y seleccione **enviar a**y, a continuación, **carpeta comprimida**.</span><span class="sxs-lookup"><span data-stu-id="3c013-263">On Windows, you can right-click on hello file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="3c013-264">Esto creará un nuevo archivo zip que contiene Hola "simpleplot. Archivo de R".</span><span class="sxs-lookup"><span data-stu-id="3c013-264">This will create a new zip file containing hello "simpleplot.R" file.</span></span>
3. <span data-ttu-id="3c013-265">Agregar el archivo toohello **conjuntos de datos** en estudio de aprendizaje automático, especificación de tipo hello como **postal**.</span><span class="sxs-lookup"><span data-stu-id="3c013-265">Add your file toohello **datasets** in Machine Learning Studio, specifying hello type as **zip**.</span></span> <span data-ttu-id="3c013-266">Ahora debería ver el archivo zip de hello en los conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="3c013-266">You should now see hello zip file in your datasets.</span></span>
4. <span data-ttu-id="3c013-267">Arrastrar y colocar Hola ZIP del **conjuntos de datos** en hello **lienzo de estudio de aprendizaje automático**.</span><span class="sxs-lookup"><span data-stu-id="3c013-267">Drag and drop hello zip file from **datasets** onto hello **ML Studio canvas**.</span></span>
5. <span data-ttu-id="3c013-268">Conecte la salida de hello de hello **comprimir datos** icono toohello **agrupación de scripts** entrada de hello [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-268">Connect hello output of hello **zip data** icon toohello **Script Bundle** input of hello [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="3c013-269">Hola de tipo `source()` función con el nombre del archivo zip en la ventana de código de hello para hello [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-269">Type hello `source()` function with your zip file name into hello code window for hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="3c013-270">En mi caso escribí `source("src/simpleplot.R")`.</span><span class="sxs-lookup"><span data-stu-id="3c013-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="3c013-271">Asegúrese de hacer clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3c013-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="3c013-272">Una vez completados estos pasos, Hola [ejecutar Script de R] [ execute-r-script] módulo ejecutará el script de Hola R en el archivo zip de hello cuando se ejecute el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-272">Once these steps are complete, hello [Execute R Script][execute-r-script] module will execute hello R script in hello zip file when hello experiment is run.</span></span> <span data-ttu-id="3c013-273">En este punto el experimento debería tener un aspecto similar al que se muestra en la ilustración 5.</span><span class="sxs-lookup"><span data-stu-id="3c013-273">At this point your experiment should look something like Figure 5.</span></span>

![Experimento con el script de código R comprimido en un archivo zip][6]

<span data-ttu-id="3c013-275">*Ilustración 5. Experimento con el script de código R comprimido en un archivo zip.*</span><span class="sxs-lookup"><span data-stu-id="3c013-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="3c013-276">DataSet1</span><span class="sxs-lookup"><span data-stu-id="3c013-276">Dataset1</span></span>
<span data-ttu-id="3c013-277">Puede pasar una tabla rectangular de código de tooyour R datos mediante la entrada de hello Dataset1.</span><span class="sxs-lookup"><span data-stu-id="3c013-277">You can pass a rectangular table of data tooyour R code by using hello Dataset1 input.</span></span> <span data-ttu-id="3c013-278">En nuestro Hola de secuencia de comandos simple `maml.mapInputPort(1)` función lee los datos de Hola de puerto 1.</span><span class="sxs-lookup"><span data-stu-id="3c013-278">In our simple script hello `maml.mapInputPort(1)` function reads hello data from port 1.</span></span> <span data-ttu-id="3c013-279">Estos datos, a continuación, se asignan el nombre de variable tooa trama de datos en el código.</span><span class="sxs-lookup"><span data-stu-id="3c013-279">This data is then assigned tooa dataframe variable name in your code.</span></span> <span data-ttu-id="3c013-280">En nuestro script simple primera línea de código de hello realiza la asignación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-280">In our simple script hello first line of code performs hello assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="3c013-281">Ejecutar el experimento, haga clic en hello **ejecutar** botón.</span><span class="sxs-lookup"><span data-stu-id="3c013-281">Execute your experiment by clicking on hello **Run** button.</span></span> <span data-ttu-id="3c013-282">Cuando concluya la ejecución de hello, haga clic en hello [ejecutar Script de R] [ execute-r-script] módulo y, a continuación, haga clic en **Ver registro de salida** en el panel de propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-282">When hello execution finishes, click on hello [Execute R Script][execute-r-script] module and then click **View output log** on hello properties pane.</span></span> <span data-ttu-id="3c013-283">Debe aparecer una nueva página en el explorador que muestra contenido de Hola de archivo de hello salida.log.</span><span class="sxs-lookup"><span data-stu-id="3c013-283">A new page should appear in your browser showing hello contents of hello output.log file.</span></span> <span data-ttu-id="3c013-284">Cuando se desplaza hacia abajo verá algo parecido a Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="3c013-284">When you scroll down you should see something like hello following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="3c013-285">Más abajo Hola página es información más detallada sobre las columnas de hello, que será similar al siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-285">Farther down hello page is more detailed information on hello columns, which will look something like hello following.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

<span data-ttu-id="3c013-286">Estos resultados son principalmente según lo previsto con 9 columnas en la trama de datos de Hola y 228 observaciones.</span><span class="sxs-lookup"><span data-stu-id="3c013-286">These results are mostly as expected, with 228 observations and 9 columns in hello dataframe.</span></span> <span data-ttu-id="3c013-287">Podemos ver los nombres de columna de hello, tipo de datos de hello R y un ejemplo de cada columna.</span><span class="sxs-lookup"><span data-stu-id="3c013-287">We can see hello column names, hello R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="3c013-288">Esta misma salida impresa hay cómodamente en hello salida de dispositivo de R de hello [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-288">This same printed output is conveniently available from hello R Device output of hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="3c013-289">Trataremos las salidas de Hola de hello [ejecutar Script de R] [ execute-r-script] módulo en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-289">We will discuss hello outputs of hello [Execute R Script][execute-r-script] module in hello next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="3c013-290">Dataset2</span><span class="sxs-lookup"><span data-stu-id="3c013-290">Dataset2</span></span>
<span data-ttu-id="3c013-291">Hello comportamiento de entrada de hello Dataset2 es idéntico toothat DataSet1.</span><span class="sxs-lookup"><span data-stu-id="3c013-291">hello behavior of hello Dataset2 input is identical toothat of Dataset1.</span></span> <span data-ttu-id="3c013-292">Con esta entrada, se puede pasar una segunda tabla rectangular de datos al código R.</span><span class="sxs-lookup"><span data-stu-id="3c013-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="3c013-293">Hola función `maml.mapInputPort(2)`, con el argumento de hello 2, es toopass usa estos datos.</span><span class="sxs-lookup"><span data-stu-id="3c013-293">hello function `maml.mapInputPort(2)`, with hello argument 2, is used toopass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="3c013-294">Ejecución de resultados de script de código R</span><span class="sxs-lookup"><span data-stu-id="3c013-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="3c013-295">Generación de tramas de datos</span><span class="sxs-lookup"><span data-stu-id="3c013-295">Output a dataframe</span></span>
<span data-ttu-id="3c013-296">Puede generar contenido de Hola de una trama de datos de R como una tabla rectangular a través del puerto de hello Dataset1 de resultados mediante el uso de hello `maml.mapOutputPort()` función.</span><span class="sxs-lookup"><span data-stu-id="3c013-296">You can output hello contents of an R dataframe as a rectangular table through hello Result Dataset1 port by using hello `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="3c013-297">En nuestro script de R simple, esto se realiza con hello después de línea.</span><span class="sxs-lookup"><span data-stu-id="3c013-297">In our simple R script this is performed by hello following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="3c013-298">Después de la ejecución experimento de hello, haga clic en puerto de salida de resultado Dataset1 Hola y, a continuación, haga clic en **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="3c013-298">After running hello experiment, click on hello Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="3c013-299">Debería ver algo parecido a lo que se muestra en la ilustración 6.</span><span class="sxs-lookup"><span data-stu-id="3c013-299">You should see something like Figure 6.</span></span>

![Visualización de Hola de salida de hello de hello datos lecheras de California][7]

<span data-ttu-id="3c013-301">*Figura 6. Visualización de Hola de salida de hello de hello datos lecheras de California.*</span><span class="sxs-lookup"><span data-stu-id="3c013-301">*Figure 6. hello visualization of hello output of hello California dairy data.*</span></span>

<span data-ttu-id="3c013-302">Esta salida es la siguiente entrada toohello idénticos, exactamente como se esperaba.</span><span class="sxs-lookup"><span data-stu-id="3c013-302">This output looks identical toohello input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="3c013-303">Resultados del dispositivo R</span><span class="sxs-lookup"><span data-stu-id="3c013-303">R Device output</span></span>
<span data-ttu-id="3c013-304">Hola salida de dispositivo de hello [ejecutar Script de R] [ execute-r-script] módulo contiene la salida de mensajes y los gráficos.</span><span class="sxs-lookup"><span data-stu-id="3c013-304">hello Device output of hello [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="3c013-305">Ambos mensajes de error estándar y de salida estándares de R se envían toohello puerto de salida de dispositivo de R.</span><span class="sxs-lookup"><span data-stu-id="3c013-305">Both standard output and standard error messages from R are sent toohello R Device output port.</span></span>  

<span data-ttu-id="3c013-306">Hola tooview R dispositivo de salida, haga clic en el puerto de hello y, a continuación, en **visualizar**.</span><span class="sxs-lookup"><span data-stu-id="3c013-306">tooview hello R Device output, click on hello port and then on **Visualize**.</span></span> <span data-ttu-id="3c013-307">Vemos salida estándar de Hola y el error estándar desde un script de Hola R en la figura 7.</span><span class="sxs-lookup"><span data-stu-id="3c013-307">We see hello standard output and standard error from hello R script in Figure 7.</span></span>

![Salida estándar y el error estándar de hello puerto de dispositivo de R][8]

<span data-ttu-id="3c013-309">*Ilustración 7. Salida estándar y el error estándar de hello puerto de dispositivo de R.*</span><span class="sxs-lookup"><span data-stu-id="3c013-309">*Figure 7. Standard output and standard error from hello R Device port.*</span></span>

<span data-ttu-id="3c013-310">Desplace hacia abajo se ve un resultado de gráficos de Hola de nuestro script de R en la figura 8.</span><span class="sxs-lookup"><span data-stu-id="3c013-310">Scrolling down we see hello graphics output from our R script in Figure 8.</span></span>  

![Salida de gráficos de hello puerto de dispositivo de R][9]

<span data-ttu-id="3c013-312">*Ilustración 8. Gráficos de salida de hello puerto de dispositivo de R.*</span><span class="sxs-lookup"><span data-stu-id="3c013-312">*Figure 8. Graphics output from hello R Device port.*</span></span>  

## <span data-ttu-id="3c013-313"><a id="filtering"></a>Transformación y filtrado de datos</span><span class="sxs-lookup"><span data-stu-id="3c013-313"><a id="filtering"></a>Data filtering and transformation</span></span>
<span data-ttu-id="3c013-314">En esta sección se llevará a cabo algunos datos básicos de filtrado y operaciones de transformación en hello datos lecheras de California.</span><span class="sxs-lookup"><span data-stu-id="3c013-314">In this section we will perform some basic data filtering and transformation operations on hello California dairy data.</span></span> <span data-ttu-id="3c013-315">Extremo de Hola de esta sección tenemos datos en un formato adecuado para generar un modelo analítico.</span><span class="sxs-lookup"><span data-stu-id="3c013-315">By hello end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="3c013-316">En esta sección se realizarán varias tareas de transformación y limpieza de datos comunes: transformación de tipos, filtrado de tramas de datos, adición de nuevas columnas de cálculo y transformaciones de valor.</span><span class="sxs-lookup"><span data-stu-id="3c013-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="3c013-317">Este fondo debe ayudar a tratar con hello muchas variaciones encontradas problemas reales.</span><span class="sxs-lookup"><span data-stu-id="3c013-317">This background should help you deal with hello many variations encountered in real-world problems.</span></span>

<span data-ttu-id="3c013-318">código de R completo de Hola de esta sección está disponible en el archivo zip de Hola que descargó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3c013-318">hello complete R code for this section is available in hello zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="3c013-319">Transformaciones de tipo</span><span class="sxs-lookup"><span data-stu-id="3c013-319">Type transformations</span></span>
<span data-ttu-id="3c013-320">Ahora que podemos leer datos de hello California lecheras en código de hello R de hello [ejecutar Script de R] [ execute-r-script] módulo, necesitamos tooensure que los datos de hello en columnas de hello tienen tipo hello diseñado y el formato.</span><span class="sxs-lookup"><span data-stu-id="3c013-320">Now that we can read hello California dairy data into hello R code in hello [Execute R Script][execute-r-script] module, we need tooensure that hello data in hello columns has hello intended type and format.</span></span>  

<span data-ttu-id="3c013-321">R es un lenguaje con tipos dinámicos, lo que significa que los tipos de datos se convierten de un tooanother según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3c013-321">R is a dynamically typed language, which means that data types are coerced from one tooanother as required.</span></span> <span data-ttu-id="3c013-322">tipos de datos atómico de Hello en R son numéricos, lógica y de caracteres.</span><span class="sxs-lookup"><span data-stu-id="3c013-322">hello atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="3c013-323">tipo de factor de Hello es toocompactly usado categorías de almacén de datos.</span><span class="sxs-lookup"><span data-stu-id="3c013-323">hello factor type is used toocompactly store categorical data.</span></span> <span data-ttu-id="3c013-324">Puede encontrar mucha más información sobre los tipos de datos en las referencias de hello en [Apéndice B - lectura adicional](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="3c013-324">You can find much more information on data types in hello references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="3c013-325">Cuando se leen los datos tabulares en R desde un origen externo, siempre es un Hola de toocheck buena idea resultante tipos de columnas de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-325">When tabular data is read into R from an external source, it is always a good idea toocheck hello resulting types in hello columns.</span></span> <span data-ttu-id="3c013-326">Es posible que desee una columna de caracteres de tipo, pero en muchos casos esto se mostrará como factor o viceversa.</span><span class="sxs-lookup"><span data-stu-id="3c013-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="3c013-327">En otros casos, la columna que piensa que debe ser numérica se mostrará con datos de caracteres como, por ejemplo, '1,23' en lugar de 1,23 como número de punto flotante.</span><span class="sxs-lookup"><span data-stu-id="3c013-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="3c013-328">Afortunadamente, es fácil tooconvert una tooanother de tipo, siempre que sea posible la asignación.</span><span class="sxs-lookup"><span data-stu-id="3c013-328">Fortunately, it is easy tooconvert one type tooanother, as long as mapping is possible.</span></span> <span data-ttu-id="3c013-329">Por ejemplo, no se puede convertir 'Nevada' en un valor numérico, pero se puede convertir el factor de tooa (variable de categoría).</span><span class="sxs-lookup"><span data-stu-id="3c013-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it tooa factor (categorical variable).</span></span> <span data-ttu-id="3c013-330">Como otro ejemplo, puede convertir el valor numérico 1 en un carácter '1' o en un factor.</span><span class="sxs-lookup"><span data-stu-id="3c013-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="3c013-331">sintaxis de Hola para cualquiera de estas conversiones es simple: `as.datatype()`.</span><span class="sxs-lookup"><span data-stu-id="3c013-331">hello syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="3c013-332">Estas funciones de conversión de tipo hello siguientes.</span><span class="sxs-lookup"><span data-stu-id="3c013-332">These type conversion functions include hello following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="3c013-333">Examinando los tipos de datos de Hola de columnas de Hola se de entrada en la sección anterior de hello: todas las columnas son de tipo numérico, excepto la columna de hello con la etiqueta 'Month', que es de carácter de tipo.</span><span class="sxs-lookup"><span data-stu-id="3c013-333">Looking at hello data types of hello columns we input in hello previous section: all columns are of type numeric, except for hello column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="3c013-334">Vamos a convertir este factor tooa y Hola resultados de pruebas.</span><span class="sxs-lookup"><span data-stu-id="3c013-334">Let's convert this tooa factor and test hello results.</span></span>  

<span data-ttu-id="3c013-335">He eliminé línea hello que crea la matriz scatterplot de Hola y se agrega una línea convertir factor de hello 'Month' columna tooa.</span><span class="sxs-lookup"><span data-stu-id="3c013-335">I have deleted hello line that created hello scatterplot matrix and added a line converting hello 'Month' column tooa factor.</span></span> <span data-ttu-id="3c013-336">En el experimento simplemente se corte y pegue el código de hello R en la ventana de código de hello de hello [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-336">In my experiment I will just cut and paste hello R code into hello code window of hello [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="3c013-337">También puede actualizar el archivo zip de Hola y cargarlo tooAzure estudio de aprendizaje automático, pero esto lleva a cabo varios pasos.</span><span class="sxs-lookup"><span data-stu-id="3c013-337">You could also update hello zip file and upload it tooAzure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="3c013-338">Vamos a ejecutar este código y buscar en el registro de salida de hello para hello script de R.</span><span class="sxs-lookup"><span data-stu-id="3c013-338">Let's execute this code and look at hello output log for hello R script.</span></span> <span data-ttu-id="3c013-339">datos importantes de Hola de registro de hello se muestran en la figura 9.</span><span class="sxs-lookup"><span data-stu-id="3c013-339">hello relevant data from hello log is shown in Figure 9.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="3c013-340">*Ilustración 9. Resumen de la trama de datos de hello con una variable de factor.*</span><span class="sxs-lookup"><span data-stu-id="3c013-340">*Figure 9. Summary of hello dataframe with a factor variable.*</span></span>

<span data-ttu-id="3c013-341">Ahora debe indicar el tipo de Hello para el mes '**Factor con 14 niveles**'.</span><span class="sxs-lookup"><span data-stu-id="3c013-341">hello type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="3c013-342">Se trata de un problema dado que hay solo 12 meses de año de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-342">This is a problem since there are only 12 months in hello year.</span></span> <span data-ttu-id="3c013-343">También puede comprobar toosee que Hola tipo en **visualizar** del conjunto de datos de resultado de hello es puerto '**categorías**'.</span><span class="sxs-lookup"><span data-stu-id="3c013-343">You can also check toosee that hello type in **Visualize** of hello Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="3c013-344">problema de Hello es esa columna no se codificó sistemáticamente ' Month' hello.</span><span class="sxs-lookup"><span data-stu-id="3c013-344">hello problem is that hello 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="3c013-345">En algunos casos, un mes se denomina Abril y en otros se abrevia como Abr. Se puede resolver este problema si recortar los caracteres de too3 Hola de una cadena.</span><span class="sxs-lookup"><span data-stu-id="3c013-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming hello string too3 characters.</span></span> <span data-ttu-id="3c013-346">línea de saludo de código ahora Hola siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="3c013-346">hello line of code now looks like hello following:</span></span>

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="3c013-347">Vuelva a ejecutar el experimento de Hola y ver el registro de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="3c013-347">Rerun hello experiment and view hello output log.</span></span> <span data-ttu-id="3c013-348">Hola espera resultados se muestran en la figura 10.</span><span class="sxs-lookup"><span data-stu-id="3c013-348">hello expected results are shown in Figure 10.</span></span>  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="3c013-349">*Ilustración 10. Resumen de la trama de datos de hello con el número correcto de niveles de factor.*</span><span class="sxs-lookup"><span data-stu-id="3c013-349">*Figure 10. Summary of hello dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="3c013-350">La variable de factor tiene ahora Hola deseado 12 niveles.</span><span class="sxs-lookup"><span data-stu-id="3c013-350">Our factor variable now has hello desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="3c013-351">Filtrado del marco de datos básico</span><span class="sxs-lookup"><span data-stu-id="3c013-351">Basic data frame filtering</span></span>
<span data-ttu-id="3c013-352">Las tramas de datos R incluyen capacidades de filtrado eficaces.</span><span class="sxs-lookup"><span data-stu-id="3c013-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="3c013-353">Es posible obtener subconjuntos de los conjuntos de datos mediante el uso de filtros lógicos en filas o columnas.</span><span class="sxs-lookup"><span data-stu-id="3c013-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="3c013-354">En muchos casos, serán necesarios criterios de filtro complejos.</span><span class="sxs-lookup"><span data-stu-id="3c013-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="3c013-355">Hola hace referencia en [Apéndice B - lectura adicional](#appendixb) contienen ejemplos detallados del filtrado de tramas de datos.</span><span class="sxs-lookup"><span data-stu-id="3c013-355">hello references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="3c013-356">En nuestro conjunto de datos, es necesario crear un bit de filtrado.</span><span class="sxs-lookup"><span data-stu-id="3c013-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="3c013-357">Si observa en las columnas de hello en la trama de datos de hello cadairydata, verá dos columnas innecesarias.</span><span class="sxs-lookup"><span data-stu-id="3c013-357">If you look at hello columns in hello cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="3c013-358">primera columna de Hello solo contiene un número de fila, lo que no resulta muy útil.</span><span class="sxs-lookup"><span data-stu-id="3c013-358">hello first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="3c013-359">Hola segunda columna, Year.Month, contiene información redundante.</span><span class="sxs-lookup"><span data-stu-id="3c013-359">hello second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="3c013-360">Podemos fácilmente excluimos estas columnas mediante el uso de hello siguiente código de R.</span><span class="sxs-lookup"><span data-stu-id="3c013-360">We can easily exclude these columns by using hello following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="3c013-361">De ahora en esta sección, simplemente mostrará Hola código adicional agrego Hola [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-361">From now on in this section, I will just show you hello additional code I am adding in hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="3c013-362">Agregará a cada nueva línea **antes de** hello `str()` función.</span><span class="sxs-lookup"><span data-stu-id="3c013-362">I will add each new line **before** hello `str()` function.</span></span> <span data-ttu-id="3c013-363">Usar esta función tooverify mis resultados en estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c013-363">I use this function tooverify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="3c013-364">Agregar Hola siguiente línea toomy R código de hello [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-364">I add hello following line toomy R code in hello [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="3c013-365">Ejecutar este código en el experimento y compruebe el resultado de hello de registro de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="3c013-365">Run this code in your experiment and check hello result from hello output log.</span></span> <span data-ttu-id="3c013-366">Estos resultados se muestran en la ilustración 11.</span><span class="sxs-lookup"><span data-stu-id="3c013-366">These results are shown in Figure 11.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="3c013-367">*Ilustración 11. Se quitó el resumen de la trama de datos de hello con dos columnas.*</span><span class="sxs-lookup"><span data-stu-id="3c013-367">*Figure 11. Summary of hello dataframe with two columns removed.*</span></span>

<span data-ttu-id="3c013-368">¡Buenas noticias!</span><span class="sxs-lookup"><span data-stu-id="3c013-368">Good news!</span></span> <span data-ttu-id="3c013-369">Se produce un error Hola esperado.</span><span class="sxs-lookup"><span data-stu-id="3c013-369">We get hello expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="3c013-370">Adición de una columna nueva</span><span class="sxs-lookup"><span data-stu-id="3c013-370">Add a new column</span></span>
<span data-ttu-id="3c013-371">modelos de serie temporal de toocreate resultará conveniente toohave una columna que contiene Hola meses desde el inicio de Hola de serie temporal de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-371">toocreate time series models it will be convenient toohave a column containing hello months since hello start of hello time series.</span></span> <span data-ttu-id="3c013-372">Por ello, crearemos una nueva columna 'Month.Count'.</span><span class="sxs-lookup"><span data-stu-id="3c013-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="3c013-373">toohelp organizar el código de hello vamos a crear nuestra primera función simple, `num.month()`.</span><span class="sxs-lookup"><span data-stu-id="3c013-373">toohelp organize hello code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="3c013-374">A continuación, aplicaremos esta toocreate función una nueva columna en la trama de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-374">We will then apply this function toocreate a new column in hello dataframe.</span></span> <span data-ttu-id="3c013-375">nuevo código de Hello es como sigue.</span><span class="sxs-lookup"><span data-stu-id="3c013-375">hello new code is as follows.</span></span>

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="3c013-376">Ahora ejecute experimento Hola actualizado y use Hola resultados registro tooview Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-376">Now run hello updated experiment and use hello output log tooview hello results.</span></span> <span data-ttu-id="3c013-377">Estos resultados se muestran en la ilustración 12.</span><span class="sxs-lookup"><span data-stu-id="3c013-377">These results are shown in Figure 12.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="3c013-378">*Ilustración 12. Resumen de hello trama de datos con columnas adicionales de Hola.*</span><span class="sxs-lookup"><span data-stu-id="3c013-378">*Figure 12. Summary of hello dataframe with hello additional column.*</span></span>

<span data-ttu-id="3c013-379">Parece que todo funciona correctamente.</span><span class="sxs-lookup"><span data-stu-id="3c013-379">It looks like everything is working.</span></span> <span data-ttu-id="3c013-380">Tenemos nueva columna con los valores esperados Hola de hello en la trama de datos.</span><span class="sxs-lookup"><span data-stu-id="3c013-380">We have hello new column with hello expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="3c013-381">Transformaciones de valor</span><span class="sxs-lookup"><span data-stu-id="3c013-381">Value transformations</span></span>
<span data-ttu-id="3c013-382">En esta sección se realizará algunas transformaciones simples en valores de hello en algunas de las columnas de hello de la trama de datos.</span><span class="sxs-lookup"><span data-stu-id="3c013-382">In this section we will perform some simple transformations on hello values in some of hello columns of our dataframe.</span></span> <span data-ttu-id="3c013-383">idioma de Hello R admite transformaciones de valor casi arbitrario.</span><span class="sxs-lookup"><span data-stu-id="3c013-383">hello R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="3c013-384">Hola hace referencia en [Apéndice B - más información](#appendixb) contienen ejemplos exhaustivos.</span><span class="sxs-lookup"><span data-stu-id="3c013-384">hello references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="3c013-385">Si observa valores de hello en resúmenes de saludo de la trama de datos debería ver algo impar aquí.</span><span class="sxs-lookup"><span data-stu-id="3c013-385">If you look at hello values in hello summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="3c013-386">¿Se produce más de helado que leche en California?</span><span class="sxs-lookup"><span data-stu-id="3c013-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="3c013-387">No, por supuesto no es así, como esto no tiene sentido, sad como este hecho puede ser toosome de nosotros amantes de helado.</span><span class="sxs-lookup"><span data-stu-id="3c013-387">No, of course not, as this makes no sense, sad as this fact may be toosome of us ice cream lovers.</span></span> <span data-ttu-id="3c013-388">unidades de Hello son diferentes.</span><span class="sxs-lookup"><span data-stu-id="3c013-388">hello units are different.</span></span> <span data-ttu-id="3c013-389">precio de Hello es en unidades de nosotros libras, leche en unidades de 1 M libras de Estados Unidos, helado esté en unidades de 1.000 nos galones, y requesón es en unidades de 1.000 libras de Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="3c013-389">hello price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="3c013-390">Suponiendo que helado Pondere los unos 6,5 libras por galón, podemos crear fácilmente Hola tooconvert multiplicación estos valores para que tengan todas las unidades iguales de 1.000 libras.</span><span class="sxs-lookup"><span data-stu-id="3c013-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do hello multiplication tooconvert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="3c013-391">Para nuestro modelo de pronóstico, utilizaremos un modelo de multiplicación de tendencia y de ajuste de temporada de estos datos.</span><span class="sxs-lookup"><span data-stu-id="3c013-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="3c013-392">Una transformación de registro nos permite toouse un modelo lineal, ya que simplifica este proceso.</span><span class="sxs-lookup"><span data-stu-id="3c013-392">A log transformation allows us toouse a linear model, simplifying this process.</span></span> <span data-ttu-id="3c013-393">Podemos aplicar transformación de registro de hello en la misma función que se aplica el multiplicador de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-393">We can apply hello log transformation in hello same function where hello multiplier is applied.</span></span>

<span data-ttu-id="3c013-394">En el siguiente código de hello, definir una nueva función, `log.transform()`y aplicarlo filas toohello que contiene valores numéricos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-394">In hello following code, I define a new function, `log.transform()`, and apply it toohello rows containing hello numerical values.</span></span> <span data-ttu-id="3c013-395">Hola R `Map()` función es tooapply usado hello `log.transform()` toohello de función seleccionado columnas de hello trama de datos.</span><span class="sxs-lookup"><span data-stu-id="3c013-395">hello R `Map()` function is used tooapply hello `log.transform()` function toohello selected columns of hello dataframe.</span></span> <span data-ttu-id="3c013-396">`Map()`es similar demasiado`apply()` pero permite más de una lista de función de toohello de argumentos.</span><span class="sxs-lookup"><span data-stu-id="3c013-396">`Map()` is similar too`apply()` but allows for more than one list of arguments toohello function.</span></span> <span data-ttu-id="3c013-397">Tenga en cuenta que una lista de multiplicadores suministra hello segundo argumento toohello `log.transform()` función.</span><span class="sxs-lookup"><span data-stu-id="3c013-397">Note that a list of multipliers supplies hello second argument toohello `log.transform()` function.</span></span> <span data-ttu-id="3c013-398">Hola `na.omit()` función se utiliza como un poco de limpieza tooensure, no nos tenemos que faltan o valores no definidos en Hola trama de datos.</span><span class="sxs-lookup"><span data-stu-id="3c013-398">hello `na.omit()` function is used as a bit of cleanup tooensure we do not have missing or undefined values in hello dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="3c013-399">Hay una gran ocurra bit en hello `log.transform()` función.</span><span class="sxs-lookup"><span data-stu-id="3c013-399">There is quite a bit happening in hello `log.transform()` function.</span></span> <span data-ttu-id="3c013-400">La mayor parte de este código es buscar posibles problemas con argumentos de Hola o tratar con las excepciones, que todavía pueden surgir durante los cálculos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-400">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="3c013-401">Unas pocas líneas de este código realmente Hola cálculos.</span><span class="sxs-lookup"><span data-stu-id="3c013-401">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="3c013-402">objetivo de Hola de programación estable hello es Error de hello tooprevent de una sola función que se impide el procesamiento de continuar.</span><span class="sxs-lookup"><span data-stu-id="3c013-402">hello goal of hello defensive programming is tooprevent hello failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="3c013-403">Un error repentino en un análisis cuya ejecución lleva mucho tiempo puede resultar muy frustrante para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="3c013-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="3c013-404">tooavoid esta situación, de forma predeterminada, se deben elegir valores devueltos que limitará daños toodownstream procesamiento.</span><span class="sxs-lookup"><span data-stu-id="3c013-404">tooavoid this situation, default return values must be chosen that will limit damage toodownstream processing.</span></span> <span data-ttu-id="3c013-405">Un mensaje también es usuarios tooalert generados que ha salido mal.</span><span class="sxs-lookup"><span data-stu-id="3c013-405">A message is also produced tooalert users that something has gone wrong.</span></span>

<span data-ttu-id="3c013-406">Si no estás programación toodefensive utilizados en R, todo este código puede parecer un poco abrumador.</span><span class="sxs-lookup"><span data-stu-id="3c013-406">If you are not used toodefensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="3c013-407">Le guiará por los pasos principales que hello:</span><span class="sxs-lookup"><span data-stu-id="3c013-407">I will walk you through hello major steps:</span></span>

1. <span data-ttu-id="3c013-408">Se define un vector de cuatro mensajes.</span><span class="sxs-lookup"><span data-stu-id="3c013-408">A vector of four messages is defined.</span></span> <span data-ttu-id="3c013-409">Estos mensajes son utilizados toocommunicate información sobre algunos de los errores posibles de Hola y las excepciones que pueden producirse con este código.</span><span class="sxs-lookup"><span data-stu-id="3c013-409">These messages are used toocommunicate information about some of hello possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="3c013-410">Devolveré un valor de NA para cada caso.</span><span class="sxs-lookup"><span data-stu-id="3c013-410">I return a value of NA for each case.</span></span> <span data-ttu-id="3c013-411">Hay muchas otras posibilidades que pueden tener menos efectos secundarios.</span><span class="sxs-lookup"><span data-stu-id="3c013-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="3c013-412">Podría devolver un vector de ceros o vector de entrada original de hello, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3c013-412">I could return a vector of zeroes, or hello original input vector, for example.</span></span>
3. <span data-ttu-id="3c013-413">Comprobaciones se realizan en función de hello argumentos toohello.</span><span class="sxs-lookup"><span data-stu-id="3c013-413">Checks are run on hello arguments toohello function.</span></span> <span data-ttu-id="3c013-414">En cada caso, si se detecta un error, se devuelve un valor predeterminado y genera un mensaje Hola `warning()` función.</span><span class="sxs-lookup"><span data-stu-id="3c013-414">In each case, if an error is detected, a default value is returned and a message is produced by hello `warning()` function.</span></span> <span data-ttu-id="3c013-415">Estoy usando `warning()` en lugar de `stop()` como Hola este último finalizará la ejecución, exactamente lo que estoy tratando de tooavoid.</span><span class="sxs-lookup"><span data-stu-id="3c013-415">I am using `warning()` rather than `stop()` as hello latter will terminate execution, exactly what I am trying tooavoid.</span></span> <span data-ttu-id="3c013-416">He escrito este código en un estilo de procedimiento, ya que, en este caso, un enfoque funcional sería demasiado complejo.</span><span class="sxs-lookup"><span data-stu-id="3c013-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="3c013-417">cálculos de registro de Hello se encapsulan en `tryCatch()` para que las excepciones no provocará una tooprocessing halt abrupto.</span><span class="sxs-lookup"><span data-stu-id="3c013-417">hello log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt tooprocessing.</span></span> <span data-ttu-id="3c013-418">Sin `tryCatch()` , la mayoría de los errores que generan las funciones de R dan como resultado una señal de detención, que hace justamente eso.</span><span class="sxs-lookup"><span data-stu-id="3c013-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="3c013-419">Ejecutar este código de R en el experimento e imprimieron un vistazo a Hola resultado en hello salida.log archivo.</span><span class="sxs-lookup"><span data-stu-id="3c013-419">Execute this R code in your experiment and have a look at hello printed output in hello output.log file.</span></span> <span data-ttu-id="3c013-420">Ahora verá los valores de hello transforman de hello registrar cuatro columnas en hello, tal como se muestra en la figura 13.</span><span class="sxs-lookup"><span data-stu-id="3c013-420">You will now see hello transformed values of hello four columns in hello log, as shown in Figure 13.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

<span data-ttu-id="3c013-421">*Ilustración 13. Resumen de hello transforma valores de hello trama de datos.*</span><span class="sxs-lookup"><span data-stu-id="3c013-421">*Figure 13. Summary of hello transformed values in hello dataframe.*</span></span>

<span data-ttu-id="3c013-422">Podemos ver valores de hello han sido transformados.</span><span class="sxs-lookup"><span data-stu-id="3c013-422">We see hello values have been transformed.</span></span> <span data-ttu-id="3c013-423">La producción de leche ahora supera con creces la producción de otros productos lácteos, recordando que ahora estamos examinando una escala logarítmica.</span><span class="sxs-lookup"><span data-stu-id="3c013-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="3c013-424">En este momento nuestros datos se limpian y estamos preparados el modelado.</span><span class="sxs-lookup"><span data-stu-id="3c013-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="3c013-425">Examinando la visualización de hello resumen Hola conjunto de datos de resultado de salida de nuestra [ejecutar Script de R] [ execute-r-script] módulo, podrá ver columnas de 'Month' hello 'Categorías' con 12 valores únicos, nuevo, tal y como deseaba .</span><span class="sxs-lookup"><span data-stu-id="3c013-425">Looking at hello visualization summary for hello Result Dataset output of our [Execute R Script][execute-r-script] module, you will see hello 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <span data-ttu-id="3c013-426"><a id="timeseries"></a>Análisis de correlación y objetos de series temporales</span><span class="sxs-lookup"><span data-stu-id="3c013-426"><a id="timeseries"></a>Time series objects and correlation analysis</span></span>
<span data-ttu-id="3c013-427">En esta sección se explorará unos pocos objetos básicos de serie de tiempo de R y analizar correlaciones Hola entre algunas de las variables de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-427">In this section we will explore a few basic R time series objects and analyze hello correlations between some of hello variables.</span></span> <span data-ttu-id="3c013-428">Nuestro objetivo es toooutput una trama de datos que contiene hello en pares correlación información en varios retrasos.</span><span class="sxs-lookup"><span data-stu-id="3c013-428">Our goal is toooutput a dataframe containing hello pairwise correlation information at several lags.</span></span>

<span data-ttu-id="3c013-429">Hola de código de R completo de esta sección se encuentra en el archivo zip de Hola que descargó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3c013-429">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="3c013-430">Objetos de series de temporales de R</span><span class="sxs-lookup"><span data-stu-id="3c013-430">Time series objects in R</span></span>
<span data-ttu-id="3c013-431">Como ya se ha mencionado, las series temporales son series de valores de datos indexados por tiempo.</span><span class="sxs-lookup"><span data-stu-id="3c013-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="3c013-432">Objetos de series de tiempo de R son toocreate usado y administración el índice de la hora de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-432">R time series objects are used toocreate and manage hello time index.</span></span> <span data-ttu-id="3c013-433">Hay varias ventajas toousing tiempo serie objetos.</span><span class="sxs-lookup"><span data-stu-id="3c013-433">There are several advantages toousing time series objects.</span></span> <span data-ttu-id="3c013-434">Objetos de la serie de tiempo de evitan Hola muchos detalles de la administración de valores de índice de series de tiempo de Hola que se encapsulan en objetos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-434">Time series objects free you from hello many details of managing hello time series index values that are encapsulated in hello object.</span></span> <span data-ttu-id="3c013-435">Además, objetos de la serie de tiempo de permitir que se toouse Hola muchos métodos de la serie de tiempo para trazar, imprimir, modelado, etcetera.</span><span class="sxs-lookup"><span data-stu-id="3c013-435">In addition, time series objects allow you toouse hello many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="3c013-436">Hola POSIXct clase en tiempo de serie es más frecuente y es relativamente sencilla.</span><span class="sxs-lookup"><span data-stu-id="3c013-436">hello POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="3c013-437">Esta clase de la serie de tiempo mide el tiempo de inicio de Hola de época de hello, el 1 de enero de 1970.</span><span class="sxs-lookup"><span data-stu-id="3c013-437">This time series class measures time from hello start of hello epoch, January 1, 1970.</span></span> <span data-ttu-id="3c013-438">En este ejemplo se utilizarán los objetos de serie temporal POSIXct.</span><span class="sxs-lookup"><span data-stu-id="3c013-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="3c013-439">Otras clases de objeto de serie temporal R ampliamente utilizadas son las clases zoo y xts, así como las series temporales extensibles.</span><span class="sxs-lookup"><span data-stu-id="3c013-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="3c013-440">Ejemplo de objeto de serie temporal</span><span class="sxs-lookup"><span data-stu-id="3c013-440">Time series object example</span></span>
<span data-ttu-id="3c013-441">Comencemos con el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3c013-441">Let's get started with our example.</span></span> <span data-ttu-id="3c013-442">Arrastre y suelte un **nuevo** módulo [Ejecutar script R][execute-r-script] en el experimento.</span><span class="sxs-lookup"><span data-stu-id="3c013-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="3c013-443">Conecte los puertos de salida de hello Dataset1 de resultado de hello existente [ejecutar Script de R] [ execute-r-script] puerto de hello nueva entrada de módulo toohello Dataset1 [ejecutar Script de R] [ execute-r-script] módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-443">Connect hello Result Dataset1 output port of hello existing [Execute R Script][execute-r-script] module toohello Dataset1 input port of hello new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="3c013-444">Tal como hice para obtener ejemplos primera hello, como se avance por el ejemplo hello, en algunos puntos que mostrará solo Hola incrementales líneas adicionales de código de R en cada paso.</span><span class="sxs-lookup"><span data-stu-id="3c013-444">As I did for hello first examples, as we progress through hello example, at some points I will show only hello incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-hello-dataframe"></a><span data-ttu-id="3c013-445">Trama de datos de lectura Hola</span><span class="sxs-lookup"><span data-stu-id="3c013-445">Reading hello dataframe</span></span>
<span data-ttu-id="3c013-446">Como primer paso, vamos a leer en una trama de datos y asegúrese de que se produce un error Hola esperado.</span><span class="sxs-lookup"><span data-stu-id="3c013-446">As a first step, let's read in a dataframe and make sure we get hello expected results.</span></span> <span data-ttu-id="3c013-447">Hello código siguiente debe hacer el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-447">hello following code should do hello job.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

<span data-ttu-id="3c013-448">Ahora, ejecute el experimento de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-448">Now, run hello experiment.</span></span> <span data-ttu-id="3c013-449">registro de Hello de la nueva forma de ejecutar Script de R Hola debería parecerse a la figura 14.</span><span class="sxs-lookup"><span data-stu-id="3c013-449">hello log of hello new Execute R Script shape should look like Figure 14.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

<span data-ttu-id="3c013-450">*Ilustración 14. Resumen de la trama de datos de hello en el módulo ejecutar Script de R de Hola.*</span><span class="sxs-lookup"><span data-stu-id="3c013-450">*Figure 14. Summary of hello dataframe in hello Execute R Script module.*</span></span>

<span data-ttu-id="3c013-451">Estos datos son de formato y los tipos de hello esperado.</span><span class="sxs-lookup"><span data-stu-id="3c013-451">This data is of hello expected types and format.</span></span> <span data-ttu-id="3c013-452">Observe que la columna de 'Month' hello es de factor de tipo y ha Hola se esperaba un número de niveles.</span><span class="sxs-lookup"><span data-stu-id="3c013-452">Note that hello 'Month' column is of type factor and has hello expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="3c013-453">Creación de un objeto de serie temporal</span><span class="sxs-lookup"><span data-stu-id="3c013-453">Creating a time series object</span></span>
<span data-ttu-id="3c013-454">Necesitamos tooadd una trama de datos de tiempo serie objeto tooour.</span><span class="sxs-lookup"><span data-stu-id="3c013-454">We need tooadd a time series object tooour dataframe.</span></span> <span data-ttu-id="3c013-455">Reemplace el código actual de hello con siguiente hello, que agrega una nueva columna de la clase POSIXct.</span><span class="sxs-lookup"><span data-stu-id="3c013-455">Replace hello current code with hello following, which adds a new column of class POSIXct.</span></span>

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

<span data-ttu-id="3c013-456">Ahora, compruebe el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="3c013-456">Now, check hello log.</span></span> <span data-ttu-id="3c013-457">Debería ser similar al que se muestra en la ilustración 15.</span><span class="sxs-lookup"><span data-stu-id="3c013-457">It should look like Figure 15.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="3c013-458">*Ilustración 15. Resumen de hello trama de datos con un objeto de la serie de tiempo.*</span><span class="sxs-lookup"><span data-stu-id="3c013-458">*Figure 15. Summary of hello dataframe with a time series object.*</span></span>

<span data-ttu-id="3c013-459">Podemos ver de hello resumen que la columna nueva hello es en realidad de clase POSIXct.</span><span class="sxs-lookup"><span data-stu-id="3c013-459">We can see from hello summary that hello new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-hello-data"></a><span data-ttu-id="3c013-460">Explorar y transformar datos de Hola</span><span class="sxs-lookup"><span data-stu-id="3c013-460">Exploring and transforming hello data</span></span>
<span data-ttu-id="3c013-461">Vamos a explorar algunas de las variables de hello en este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="3c013-461">Let's explore some of hello variables in this dataset.</span></span> <span data-ttu-id="3c013-462">Una matriz de scatterplot es un tooproduce buena forma un vistazo.</span><span class="sxs-lookup"><span data-stu-id="3c013-462">A scatterplot matrix is a good way tooproduce a quick look.</span></span> <span data-ttu-id="3c013-463">Estoy reemplazando hello `str()` función en código de R anterior Hola con hello después de línea.</span><span class="sxs-lookup"><span data-stu-id="3c013-463">I am replacing hello `str()` function in hello previous R code with hello following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="3c013-464">Ejecute este código y observe qué sucede.</span><span class="sxs-lookup"><span data-stu-id="3c013-464">Run this code and see what happens.</span></span> <span data-ttu-id="3c013-465">trazado de Hello producida Hola puerto de dispositivo de R debería parecerse figura 16.</span><span class="sxs-lookup"><span data-stu-id="3c013-465">hello plot produced at hello R Device port should look like Figure 16.</span></span>

![Matriz de trazado de dispersión de las variables seleccionadas][17]

<span data-ttu-id="3c013-467">*Ilustración 16. Matriz de trazado de dispersión de las variables seleccionadas.*</span><span class="sxs-lookup"><span data-stu-id="3c013-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="3c013-468">Hay alguna estructura extraña en relaciones de hello entre estas variables.</span><span class="sxs-lookup"><span data-stu-id="3c013-468">There is some odd-looking structure in hello relationships between these variables.</span></span> <span data-ttu-id="3c013-469">Quizás esto surge de tendencias en los datos de Hola y de hechos de Hola que no hemos estandarizado variables Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-469">Perhaps this arises from trends in hello data and from hello fact that we have not standardized hello variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="3c013-470">Análisis de correlación</span><span class="sxs-lookup"><span data-stu-id="3c013-470">Correlation analysis</span></span>
<span data-ttu-id="3c013-471">análisis de correlación tooperform necesitamos tooboth anular de tendencia y estandarizar las variables de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-471">tooperform correlation analysis we need tooboth de-trend and standardize hello variables.</span></span> <span data-ttu-id="3c013-472">Simplemente podríamos usar Hola R `scale()` función, que se centra tanto escala variables.</span><span class="sxs-lookup"><span data-stu-id="3c013-472">We could simply use hello R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="3c013-473">Esta función también puede ejecutarse más rápido.</span><span class="sxs-lookup"><span data-stu-id="3c013-473">This function might well run faster.</span></span> <span data-ttu-id="3c013-474">Sin embargo, deseo tooshow se muestra un ejemplo de programación estable en R.</span><span class="sxs-lookup"><span data-stu-id="3c013-474">However, I want tooshow you an example of defensive programing in R.</span></span>

<span data-ttu-id="3c013-475">Hola `ts.detrend()` función se muestra a continuación realiza estas dos operaciones.</span><span class="sxs-lookup"><span data-stu-id="3c013-475">hello `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="3c013-476">Hello dos líneas de código siguientes anular tendencias datos hello y, a continuación, normalizar los valores de hello.</span><span class="sxs-lookup"><span data-stu-id="3c013-476">hello following two lines of code de-trend hello data and then standardize hello values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="3c013-477">Hay una gran ocurra bit en hello `ts.detrend()` función.</span><span class="sxs-lookup"><span data-stu-id="3c013-477">There is quite a bit happening in hello `ts.detrend()` function.</span></span> <span data-ttu-id="3c013-478">La mayor parte de este código es buscar posibles problemas con argumentos de Hola o tratar con las excepciones, que todavía pueden surgir durante los cálculos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-478">Most of this code is checking for potential problems with hello arguments or dealing with exceptions, which can still arise during hello computations.</span></span> <span data-ttu-id="3c013-479">Unas pocas líneas de este código realmente Hola cálculos.</span><span class="sxs-lookup"><span data-stu-id="3c013-479">Only a few lines of this code actually do hello computations.</span></span>

<span data-ttu-id="3c013-480">Ya hemos analizado un ejemplo de programación defensiva en [Transformaciones de valor](#valuetransformations).</span><span class="sxs-lookup"><span data-stu-id="3c013-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="3c013-481">Ambos bloques de cálculo se incluyen en `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="3c013-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="3c013-482">En ciertos casos realiza vector de entrada original sentido tooreturn hello y en otros casos, devuelve un vector de ceros.</span><span class="sxs-lookup"><span data-stu-id="3c013-482">For some errors it makes sense tooreturn hello original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="3c013-483">Tenga en cuenta que usa para anular tendencias de regresión lineal de hello es una regresión de series de tiempo.</span><span class="sxs-lookup"><span data-stu-id="3c013-483">Note that hello linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="3c013-484">variable de elemento de predicción de Hello es un objeto de la serie de tiempo.</span><span class="sxs-lookup"><span data-stu-id="3c013-484">hello predictor variable is a time series object.</span></span>  

<span data-ttu-id="3c013-485">Una vez `ts.detrend()` se define se aplican toohello variables de interés en nuestra trama de datos.</span><span class="sxs-lookup"><span data-stu-id="3c013-485">Once `ts.detrend()` is defined we apply it toohello variables of interest in our dataframe.</span></span> <span data-ttu-id="3c013-486">Nos debemos coerce lista resultante Hola creado por `lapply()` toodata trama de datos mediante el uso de `as.data.frame()`.</span><span class="sxs-lookup"><span data-stu-id="3c013-486">We must coerce hello resulting list created by `lapply()` toodata dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="3c013-487">Debido a aspectos estable de `ts.detrend()`, tooprocess error una de las variables de hello no impedirá que corregir el procesamiento del programa Hola a otros usuarios.</span><span class="sxs-lookup"><span data-stu-id="3c013-487">Because of defensive aspects of `ts.detrend()`, failure tooprocess one of hello variables will not prevent correct processing of hello others.</span></span>  

<span data-ttu-id="3c013-488">línea final de Hola de código crea un scatterplot en pares.</span><span class="sxs-lookup"><span data-stu-id="3c013-488">hello final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="3c013-489">Después de ejecutar código de hello R, resultados de Hola de hello scatterplot se muestran en la figura 17.</span><span class="sxs-lookup"><span data-stu-id="3c013-489">After running hello R code, hello results of hello scatterplot are shown in Figure 17.</span></span>

![Trazado de dispersión en pares de series temporales estandarizadas y con las tendencias anuladas][18]

<span data-ttu-id="3c013-491">*Ilustración 17. Trazado de dispersión en pares de series temporales estandarizadas y con las tendencias anuladas.*</span><span class="sxs-lookup"><span data-stu-id="3c013-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="3c013-492">Puede comparar estos toothose de resultados se muestra en la figura 16.</span><span class="sxs-lookup"><span data-stu-id="3c013-492">You can compare these results toothose shown in Figure 16.</span></span> <span data-ttu-id="3c013-493">Con hello tendencia quitado y Hola variables estandarizadas, vemos mucho menos estructura en relaciones de hello entre estas variables.</span><span class="sxs-lookup"><span data-stu-id="3c013-493">With hello trend removed and hello variables standardized, we see a lot less structure in hello relationships between these variables.</span></span>

<span data-ttu-id="3c013-494">las correlaciones de toocompute Hola código de Hello como objetos de R ccf es como sigue.</span><span class="sxs-lookup"><span data-stu-id="3c013-494">hello code toocompute hello correlations as R ccf objects is as follows.</span></span>

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="3c013-495">Ejecutar este código genera el registro de hello que se muestra en la figura 18.</span><span class="sxs-lookup"><span data-stu-id="3c013-495">Running this code produces hello log shown in Figure 18.</span></span>

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

<span data-ttu-id="3c013-496">*Ilustración 18. Lista de ccf objetos de análisis de correlación en pares de Hola.*</span><span class="sxs-lookup"><span data-stu-id="3c013-496">*Figure 18. List of ccf objects from hello pairwise correlation analysis.*</span></span>

<span data-ttu-id="3c013-497">Hay un valor de correlación para cada intervalo.</span><span class="sxs-lookup"><span data-stu-id="3c013-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="3c013-498">Ninguno de estos valores de correlación es lo suficientemente grande como toobe significativo.</span><span class="sxs-lookup"><span data-stu-id="3c013-498">None of these correlation values is large enough toobe significant.</span></span> <span data-ttu-id="3c013-499">Por lo tanto, podemos concluir que podemos modelar cada variable de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="3c013-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="3c013-500">Generación de tramas de datos</span><span class="sxs-lookup"><span data-stu-id="3c013-500">Output a dataframe</span></span>
<span data-ttu-id="3c013-501">Nos hemos calculado correlaciones en pares de hello como una lista de objetos de R ccf.</span><span class="sxs-lookup"><span data-stu-id="3c013-501">We have computed hello pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="3c013-502">Esto presenta un poco de un problema como puerto de salida del conjunto de datos de resultado de hello realmente requiere una trama de datos.</span><span class="sxs-lookup"><span data-stu-id="3c013-502">This presents a bit of a problem as hello Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="3c013-503">Además, objeto ccf de hello es una lista y queremos solo los valores de hello en el primer elemento de esta lista, correlaciones hello en Hola de hello retrasos distintos.</span><span class="sxs-lookup"><span data-stu-id="3c013-503">Further, hello ccf object is itself a list and we want only hello values in hello first element of this list, hello correlations at hello various lags.</span></span>

<span data-ttu-id="3c013-504">Hola siguientes código extrae Hola lag valores de lista de Hola de objetos de ccf, que son listas.</span><span class="sxs-lookup"><span data-stu-id="3c013-504">hello following code extracts hello lag values from hello list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="3c013-505">Hola primera línea de código es un poco complicado y explicación puede ayudarle a entenderlo.</span><span class="sxs-lookup"><span data-stu-id="3c013-505">hello first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="3c013-506">Trabajar en profundidad de hello tenemos siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="3c013-506">Working from hello inside out we have hello following:</span></span>

1. <span data-ttu-id="3c013-507">Hola '**[[**'operador con el argumento de hello'**1**' selecciona Hola vector de correlaciones en hello retrasos del primer elemento de lista de objetos de hello ccf de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-507">hello '**[[**' operator with hello argument '**1**' selects hello vector of correlations at hello lags from hello first element of hello ccf object list.</span></span>
2. <span data-ttu-id="3c013-508">Hola `do.call()` función aplica hello `rbind()` devuelve función sobre los elementos de Hola de lista de hello `lapply()`.</span><span class="sxs-lookup"><span data-stu-id="3c013-508">hello `do.call()` function applies hello `rbind()` function over hello elements of hello list returns by `lapply()`.</span></span>
3. <span data-ttu-id="3c013-509">Hola `data.frame()` función convierte el resultado de hello generado por `do.call()` tooa trama de datos.</span><span class="sxs-lookup"><span data-stu-id="3c013-509">hello `data.frame()` function coerces hello result produced by `do.call()` tooa dataframe.</span></span>

<span data-ttu-id="3c013-510">Tenga en cuenta que los nombres de fila Hola están en una columna de la trama de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-510">Note that hello row names are in a column of hello dataframe.</span></span> <span data-ttu-id="3c013-511">Si lo hace, conserva los nombres de la fila de hello cuando vuelven de hello [ejecutar Script de R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="3c013-511">Doing so preserves hello row names when they are output from hello [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="3c013-512">Ejecutar código de hello produce el resultado de hello se muestra en la figura 19 cuando se **visualizar** Hola resultado al puerto del conjunto de datos de resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="3c013-512">Running hello code produces hello output shown in Figure 19 when I **Visualize** hello output at hello Result Dataset port.</span></span> <span data-ttu-id="3c013-513">nombres de la fila de Hello están en la primera columna de hello, según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="3c013-513">hello row names are in hello first column, as intended.</span></span>

![Salida de resultados de análisis de correlación de Hola][20]

<span data-ttu-id="3c013-515">*Ilustración 19. Resultados de salida del análisis de correlación de Hola.*</span><span class="sxs-lookup"><span data-stu-id="3c013-515">*Figure 19. Results output from hello correlation analysis.*</span></span>

## <span data-ttu-id="3c013-516"><a id="seasonalforecasting"></a>Ejemplo de serie temporal: previsión estacional</span><span class="sxs-lookup"><span data-stu-id="3c013-516"><a id="seasonalforecasting"></a>Time series example: seasonal forecasting</span></span>
<span data-ttu-id="3c013-517">Nuestros datos ahora están en un formato adecuado para el análisis y hemos determinado que no hay significativas correlaciones entre las variables de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between hello variables.</span></span> <span data-ttu-id="3c013-518">Vamos a continuar y a crear un modelo de previsión de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="3c013-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="3c013-519">Mediante este modelo se predecir producción de leche de California para hello 12 meses de 2013.</span><span class="sxs-lookup"><span data-stu-id="3c013-519">Using this model we will forecast California milk production for hello 12 months of 2013.</span></span>

<span data-ttu-id="3c013-520">Nuestro modelo de pronóstico tendrá dos componentes, un componente de tendencia y un componente de temporada.</span><span class="sxs-lookup"><span data-stu-id="3c013-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="3c013-521">previsión completa de Hello es producto Hola de estos dos componentes.</span><span class="sxs-lookup"><span data-stu-id="3c013-521">hello complete forecast is hello product of these two components.</span></span> <span data-ttu-id="3c013-522">Este tipo de modelo se conoce como un modelo de multiplicación.</span><span class="sxs-lookup"><span data-stu-id="3c013-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="3c013-523">alternativa de Hello es un modelo de sumando.</span><span class="sxs-lookup"><span data-stu-id="3c013-523">hello alternative is an additive model.</span></span> <span data-ttu-id="3c013-524">Ya hemos aplicado variables registro transformación toohello de interés, lo que hace este análisis manejable.</span><span class="sxs-lookup"><span data-stu-id="3c013-524">We have already applied a log transformation toohello variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="3c013-525">Hola de código de R completo de esta sección se encuentra en el archivo zip de Hola que descargó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3c013-525">hello complete R code for this section is in hello zip file you downloaded earlier.</span></span>

### <a name="creating-hello-dataframe-for-analysis"></a><span data-ttu-id="3c013-526">Creación de hello trama de datos para el análisis</span><span class="sxs-lookup"><span data-stu-id="3c013-526">Creating hello dataframe for analysis</span></span>
<span data-ttu-id="3c013-527">Empiece agregando un **nueva** [ejecutar Script de R] [ execute-r-script] experimento tooyour de módulo.</span><span class="sxs-lookup"><span data-stu-id="3c013-527">Start by adding a **new** [Execute R Script][execute-r-script] module tooyour experiment.</span></span> <span data-ttu-id="3c013-528">Conectar hello **conjunto de datos de resultado** salida de hello existente [ejecutar Script de R] [ execute-r-script] módulo toohello **Dataset1** entrada del nuevo módulo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-528">Connect hello **Result Dataset** output of hello existing [Execute R Script][execute-r-script] module toohello **Dataset1** input of hello new module.</span></span> <span data-ttu-id="3c013-529">resultado de Hello debe ser similar a la figura 20.</span><span class="sxs-lookup"><span data-stu-id="3c013-529">hello result should look something like Figure 20.</span></span>

![Hola experimentar con el nuevo módulo de ejecutar Script de R Hola agregado][21]

<span data-ttu-id="3c013-531">*Figura 20. Hola experimentar con el nuevo módulo de ejecutar Script de R Hola agregado.*</span><span class="sxs-lookup"><span data-stu-id="3c013-531">*Figure 20. hello experiment with hello new Execute R Script module added.*</span></span>

<span data-ttu-id="3c013-532">Como con el análisis de correlación de Hola que se acaba de completar, necesitamos tooadd una columna con un objeto de series de tiempo POSIXct.</span><span class="sxs-lookup"><span data-stu-id="3c013-532">As with hello correlation analysis we just completed, we need tooadd a column with a POSIXct time series object.</span></span> <span data-ttu-id="3c013-533">Hola siguiente código hará esto es exactamente.</span><span class="sxs-lookup"><span data-stu-id="3c013-533">hello following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="3c013-534">Ejecutar este código y examine el registro de hello.</span><span class="sxs-lookup"><span data-stu-id="3c013-534">Run this code and look at hello log.</span></span> <span data-ttu-id="3c013-535">resultado de Hello debe ser similar de la figura 21.</span><span class="sxs-lookup"><span data-stu-id="3c013-535">hello result should look like Figure 21.</span></span>

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

<span data-ttu-id="3c013-536">*Ilustración 21. Resumen de la trama de datos de Hola.*</span><span class="sxs-lookup"><span data-stu-id="3c013-536">*Figure 21. A summary of hello dataframe.*</span></span>

<span data-ttu-id="3c013-537">Con este resultado, estamos listo toostart nuestro análisis.</span><span class="sxs-lookup"><span data-stu-id="3c013-537">With this result, we are ready toostart our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="3c013-538">Creación de un conjunto de datos de entrenamiento</span><span class="sxs-lookup"><span data-stu-id="3c013-538">Create a training dataset</span></span>
<span data-ttu-id="3c013-539">Con la trama de datos de hello construido necesitamos toocreate un conjunto de datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="3c013-539">With hello dataframe constructed we need toocreate a training dataset.</span></span> <span data-ttu-id="3c013-540">Estos datos incluyen todas las observaciones de hello salvo Hola últimas 12, del año de hello 2013, que es el conjunto de datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="3c013-540">This data will include all of hello observations except hello last 12, of hello year 2013, which is our test dataset.</span></span> <span data-ttu-id="3c013-541">a continuación Hola trama de datos de Hola de subconjuntos de código y crea los gráficos de las variables de producción y el precio del lecheras Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-541">hello following code subsets hello dataframe and creates plots of hello dairy production and price variables.</span></span> <span data-ttu-id="3c013-542">A continuación, crear gráficos de hello cuatro variables de producción y el precio.</span><span class="sxs-lookup"><span data-stu-id="3c013-542">I then create plots of hello four production and price variables.</span></span> <span data-ttu-id="3c013-543">Una función anónima es toodefine usa algunos amplía para trazado y, a continuación, recorrer en iteración la lista de Hola de hello otros dos argumentos con `Map()`.</span><span class="sxs-lookup"><span data-stu-id="3c013-543">An anonymous function is used toodefine some augments for plot, and then iterate over hello list of hello other two arguments with `Map()`.</span></span> <span data-ttu-id="3c013-544">Si piensa que un bucle for podría haber funcionado para esta operación, está en lo cierto.</span><span class="sxs-lookup"><span data-stu-id="3c013-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="3c013-545">Sin embargo, puesto que R es un lenguaje funcional, he preferido ofrecer un enfoque funcional.</span><span class="sxs-lookup"><span data-stu-id="3c013-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="3c013-546">Ejecución de código de hello genera Hola serie de serie temporal de traza de salida de dispositivo de R Hola que se muestra en la figura 22.</span><span class="sxs-lookup"><span data-stu-id="3c013-546">Running hello code produces hello series of time series plots from hello R Device output shown in Figure 22.</span></span> <span data-ttu-id="3c013-547">Tenga en cuenta ese eje de tiempo de hello en unidades de fechas, una ventaja de tiempo de hello serie traza método.</span><span class="sxs-lookup"><span data-stu-id="3c013-547">Note that hello time axis is in units of dates, a nice benefit of hello time series plot method.</span></span>

![Primero de los trazados de series temporales de la producción de productos lácteos de California y de los datos de precios](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Segundos de los trazados de series temporales de la producción de productos lácteos de California y de los datos de precios](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Tercero de los trazados de series temporales de la producción de productos lácteos de California y de los datos de precios](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Cuarto de los trazados de series temporales de la producción de productos lácteos de California y de los datos de precios](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="3c013-552">*Ilustración 22. Trazados de series temporales de la producción de productos lácteos de California y de los datos de precios.*</span><span class="sxs-lookup"><span data-stu-id="3c013-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="3c013-553">Modelo de tendencia</span><span class="sxs-lookup"><span data-stu-id="3c013-553">A trend model</span></span>
<span data-ttu-id="3c013-554">Al haber creado un objeto de la serie de tiempo y haya tenido un vistazo a los datos de hello, comencemos tooconstruct un modelo de tendencia para hello datos de producción de leche de California.</span><span class="sxs-lookup"><span data-stu-id="3c013-554">Having created a time series object and having had a look at hello data, let's start tooconstruct a trend model for hello California milk production data.</span></span> <span data-ttu-id="3c013-555">Para ello, utilizaremos una regresión de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="3c013-555">We can do this with a time series regression.</span></span> <span data-ttu-id="3c013-556">Sin embargo, resulta claro de trazado de Hola que se se necesita más de un tooaccurately pendiente y la intersección de modelo Hola observada tendencias en los datos de entrenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-556">However, it is clear from hello plot that we will need more than a slope and intercept tooaccurately model hello observed trend in hello training data.</span></span>

<span data-ttu-id="3c013-557">Dado pequeña escala de datos de Hola de hello, se generar modelo Hola de tendencia en RStudio y, a continuación, corte y pegue modelo resultante de hello en aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c013-557">Given hello small scale of hello data, I will build hello model for trend in RStudio and then cut and paste hello resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="3c013-558">RStudio proporciona un entorno interactivo para este tipo de análisis interactivo.</span><span class="sxs-lookup"><span data-stu-id="3c013-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="3c013-559">Como el primer intento, intentará una regresión polinómica con enciende too3.</span><span class="sxs-lookup"><span data-stu-id="3c013-559">As a first attempt, I will try a polynomial regression with powers up too3.</span></span> <span data-ttu-id="3c013-560">Existe un claro riesgo de sobreajuste con estos modelos.</span><span class="sxs-lookup"><span data-stu-id="3c013-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="3c013-561">Por lo tanto, es mejor términos de orden superior tooavoid.</span><span class="sxs-lookup"><span data-stu-id="3c013-561">Therefore, it is best tooavoid high order terms.</span></span> <span data-ttu-id="3c013-562">Hola `I()` función inhibe la interpretación de contenido de hello (interpreta el contenido de Hola "tal cual") y le permite toowrite una función literalmente interpretada de una ecuación de regresión.</span><span class="sxs-lookup"><span data-stu-id="3c013-562">hello `I()` function inhibits interpretation of hello contents (interprets hello contents 'as is') and allows you toowrite a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="3c013-563">Esto genera el siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-563">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

<span data-ttu-id="3c013-564">De valores P (Pr (> | t |)) en esta salida, podemos ver que Hola cuadrático término no puede ser importante.</span><span class="sxs-lookup"><span data-stu-id="3c013-564">From P values (Pr(>|t|)) in this output, we can see that hello squared term may not be significant.</span></span> <span data-ttu-id="3c013-565">Utilizo hello `update()` función toomodify este modelo por quitar Hola cuadrado término.</span><span class="sxs-lookup"><span data-stu-id="3c013-565">I will use hello `update()` function toomodify this model by dropping hello squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="3c013-566">Esto genera el siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-566">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

<span data-ttu-id="3c013-567">Mucho mejor ahora.</span><span class="sxs-lookup"><span data-stu-id="3c013-567">This looks better.</span></span> <span data-ttu-id="3c013-568">Todos los términos de Hola de son significativos.</span><span class="sxs-lookup"><span data-stu-id="3c013-568">All of hello terms are significant.</span></span> <span data-ttu-id="3c013-569">Sin embargo, Hola 2e-16 valor es un valor predeterminado y no debe tomarse muy en serio.</span><span class="sxs-lookup"><span data-stu-id="3c013-569">However, hello 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="3c013-570">Como una prueba de comprobación, vamos a hacer un gráfico de serie de tiempo de hello datos de producción de lácteos California con una curva de tendencia de Hola que se muestra.</span><span class="sxs-lookup"><span data-stu-id="3c013-570">As a sanity test, let's make a time series plot of hello California dairy production data with hello trend curve shown.</span></span> <span data-ttu-id="3c013-571">He agregado Hola después el código de hello aprendizaje automático de Azure [ejecutar Script de R] [ execute-r-script] toocreate de modelo (no RStudio) Hola modelo y realizar un gráfico.</span><span class="sxs-lookup"><span data-stu-id="3c013-571">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) toocreate hello model and make a plot.</span></span> <span data-ttu-id="3c013-572">Hola resultado se muestra en la figura 23.</span><span class="sxs-lookup"><span data-stu-id="3c013-572">hello result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![Datos de producción de leche de California con modelo de tendencias](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="3c013-574">*Ilustración 23. Datos de producción de leche de California con modelo de tendencias.*</span><span class="sxs-lookup"><span data-stu-id="3c013-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="3c013-575">Parece que el modelo de tendencia de Hola se adapta a los datos de hello bastante bien.</span><span class="sxs-lookup"><span data-stu-id="3c013-575">It looks like hello trend model fits hello data fairly well.</span></span> <span data-ttu-id="3c013-576">Además, no parece que no hay evidencia de toobe de sobreajustar, como impar ondulará en curva de modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-576">Further, there does not seem toobe evidence of over-fitting, such as odd wiggles in hello model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="3c013-577">Modelo de temporada</span><span class="sxs-lookup"><span data-stu-id="3c013-577">Seasonal model</span></span>
<span data-ttu-id="3c013-578">Con un modelo de tendencia en mano, se necesita toopush en y se incluyen efectos estacionales Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-578">With a trend model in hand, we need toopush on and include hello seasonal effects.</span></span> <span data-ttu-id="3c013-579">Mes de hello del año de Hola se usará como una variable ficticia en vigor de hello modelo lineal toocapture Hola por meses.</span><span class="sxs-lookup"><span data-stu-id="3c013-579">We will use hello month of hello year as a dummy variable in hello linear model toocapture hello month-by-month effect.</span></span> <span data-ttu-id="3c013-580">Tenga en cuenta que cuando se introducen las variables de factor en un modelo, intercept hello no haya que calcular.</span><span class="sxs-lookup"><span data-stu-id="3c013-580">Note that when you introduce factor variables into a model, hello intercept must not be computed.</span></span> <span data-ttu-id="3c013-581">Si no lo hace, fórmula hello es demasiado especificado y R se colocará uno Hola deseado factores, pero tenga término de intercepción de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-581">If you do not do this, hello formula is over-specified and R will drop one of hello desired factors but keep hello intercept term.</span></span>

<span data-ttu-id="3c013-582">Puesto que tenemos un modelo de tendencia satisfactorio, podemos utilizar hello `update()` toohello de modelo existente de términos de hello tooadd de función nueva.</span><span class="sxs-lookup"><span data-stu-id="3c013-582">Since we have a satisfactory trend model we can use hello `update()` function tooadd hello new terms toohello existing model.</span></span> <span data-ttu-id="3c013-583">Hola -1 en la fórmula de la actualización de hello quita el término de intercepción de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-583">hello -1 in hello update formula drops hello intercept term.</span></span> <span data-ttu-id="3c013-584">Continuar en RStudio para el momento de hello:</span><span class="sxs-lookup"><span data-stu-id="3c013-584">Continuing in RStudio for hello moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="3c013-585">Esto genera el siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-585">This generates hello following.</span></span>

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

<span data-ttu-id="3c013-586">Se ve ese modelo Hola ya no tiene un término de intercepción y tiene 12 factores importantes del mes.</span><span class="sxs-lookup"><span data-stu-id="3c013-586">We see that hello model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="3c013-587">Esto es exactamente lo que deseamos toosee.</span><span class="sxs-lookup"><span data-stu-id="3c013-587">This is exactly what we wanted toosee.</span></span>

<span data-ttu-id="3c013-588">Vamos a hacer otro trazado de series de tiempo de hello California lácteos datos toosee grado funciona modelo estacionales Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-588">Let's make another time series plot of hello California dairy production data toosee how well hello seasonal model is working.</span></span> <span data-ttu-id="3c013-589">He agregado Hola después el código de hello aprendizaje automático de Azure [ejecutar Script de R] [ execute-r-script] toocreate Hola modelo y realizar un gráfico.</span><span class="sxs-lookup"><span data-stu-id="3c013-589">I have added hello following code in hello Azure Machine Learning [Execute R Script][execute-r-script] toocreate hello model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="3c013-590">Ejecutar este código en aprendizaje automático de Azure genera trazado Hola que se muestra en la figura 24.</span><span class="sxs-lookup"><span data-stu-id="3c013-590">Running this code in Azure Machine Learning produces hello plot shown in Figure 24.</span></span>

![Producción de leche de California con modelo que incluye los efectos de temporada](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="3c013-592">*Ilustración 24. Producción de leche de California con modelo que incluye los efectos de temporada.*</span><span class="sxs-lookup"><span data-stu-id="3c013-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="3c013-593">Hello toohello ajuste datos se muestra en la figura 24 son esperanzadores en su lugar.</span><span class="sxs-lookup"><span data-stu-id="3c013-593">hello fit toohello data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="3c013-594">Tendencia de Hola y el efecto de temporada de hello (variación mensual) buscan razonables.</span><span class="sxs-lookup"><span data-stu-id="3c013-594">Both hello trend and hello seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="3c013-595">Como otra comprobación en nuestro modelo, echemos un vistazo a los valores residuales Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-595">As another check on our model, let's have a look at hello residuals.</span></span> <span data-ttu-id="3c013-596">Hello siguiente calcula código Hola valores de predicción de nuestras dos modelos, calcula valores residuales de Hola para modelo estacionales hello y, a continuación, traza estos valores residuales para datos de entrenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-596">hello following code computes hello predicted values from our two models, computes hello residuals for hello seasonal model, and then plots these residuals for hello training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="3c013-597">trazado residual Hola se muestra en la figura 25.</span><span class="sxs-lookup"><span data-stu-id="3c013-597">hello residual plot is shown in Figure 25.</span></span>

![Valores residuales del modelo de temporada de Hola para datos de entrenamiento de Hola](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="3c013-599">*Ilustración 25. Valores residuales del modelo de temporada de Hola para datos de entrenamiento de Hola.*</span><span class="sxs-lookup"><span data-stu-id="3c013-599">*Figure 25. Residuals of hello seasonal model for hello training data.*</span></span>

<span data-ttu-id="3c013-600">Estos valores residuales parecen ser razonables.</span><span class="sxs-lookup"><span data-stu-id="3c013-600">These residuals look reasonable.</span></span> <span data-ttu-id="3c013-601">No hay ninguna estructura determinada, excepto el efecto de Hola de recesión Hola 2008 y 2009, que nuestro modelo no tiene en cuenta especialmente bien.</span><span class="sxs-lookup"><span data-stu-id="3c013-601">There is no particular structure, except hello effect of hello 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="3c013-602">trazado de Hola que se muestra en la figura 25 es útil para detectar los patrones dependientes del tiempo en valores residuales Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-602">hello plot shown in Figure 25 is useful for detecting any time-dependent patterns in hello residuals.</span></span> <span data-ttu-id="3c013-603">enfoque explícito de Hola de informática y trazar residuos de hello que he usado coloca valores residuales hello en orden cronológico en el gráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-603">hello explicit approach of computing and plotting hello residuals I used places hello residuals in time order on hello plot.</span></span> <span data-ttu-id="3c013-604">Si, en hello otra parte, había trazada `milk.lm$residuals`, no habría sido trazado hello en orden cronológico.</span><span class="sxs-lookup"><span data-stu-id="3c013-604">If, on hello other hand, I had plotted `milk.lm$residuals`, hello plot would not have been in time order.</span></span>

<span data-ttu-id="3c013-605">También puede usar `plot.lm()` tooproduce una serie de gráficos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="3c013-605">You can also use `plot.lm()` tooproduce a series of diagnostic plots.</span></span>

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="3c013-606">Este código genera una serie de trazados de diagnósticos que se muestran en la ilustración 26.</span><span class="sxs-lookup"><span data-stu-id="3c013-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![Primero de los gráficos de diagnóstico para modelo estacionales Hola](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Segundo de los gráficos de diagnóstico para el modelo de temporada de Hola](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Tercera parte de los gráficos de diagnóstico para modelo estacionales Hola](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Cuarta parte de los gráficos de diagnóstico para modelo estacionales Hola](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="3c013-611">*Ilustración 26. Traza de diagnóstico para modelo estacionales Hola.*</span><span class="sxs-lookup"><span data-stu-id="3c013-611">*Figure 26. Diagnostic plots for hello seasonal model.*</span></span>

<span data-ttu-id="3c013-612">Hay unos cuantos puntos altamente influyentes identificados en estos gráficos, pero a nada toocause nos preocupamos por TI.</span><span class="sxs-lookup"><span data-stu-id="3c013-612">There are a few highly influential points identified in these plots, but nothing toocause great concern.</span></span> <span data-ttu-id="3c013-613">Además, podemos ver de trazado de hello Normal Q-Q que valores residuales Hola son cerrar toonormally distribuida, una suposición importante para los modelos lineales.</span><span class="sxs-lookup"><span data-stu-id="3c013-613">Further, we can see from hello Normal Q-Q plot that hello residuals are close toonormally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="3c013-614">Evaluación del modelo y predicción</span><span class="sxs-lookup"><span data-stu-id="3c013-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="3c013-615">Hay solo un toocomplete de toodo algo más en nuestro ejemplo.</span><span class="sxs-lookup"><span data-stu-id="3c013-615">There is just one more thing toodo toocomplete our example.</span></span> <span data-ttu-id="3c013-616">Se necesitan toocompute previsiones y medir error Hola frente a los datos reales de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-616">We need toocompute forecasts and measure hello error against hello actual data.</span></span> <span data-ttu-id="3c013-617">Nuestro pronóstico será de hello 12 meses de 2013.</span><span class="sxs-lookup"><span data-stu-id="3c013-617">Our forecast will be for hello 12 months of 2013.</span></span> <span data-ttu-id="3c013-618">Se puede calcular una medida de error para este toohello previsión los datos reales que no forma parte de nuestro conjunto de datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="3c013-618">We can compute an error measure for this forecast toohello actual data that is not part of our training dataset.</span></span> <span data-ttu-id="3c013-619">Además, se puede comparar el rendimiento en hello 18 años de toohello de datos de entrenamiento 12 meses de datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="3c013-619">Additionally, we can compare performance on hello 18 years of training data toohello 12 months of test data.</span></span>  

<span data-ttu-id="3c013-620">Se usa un número de métricas de rendimiento de hello toomeasure de modelos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="3c013-620">A number of metrics are used toomeasure hello performance of time series models.</span></span> <span data-ttu-id="3c013-621">En nuestro caso utilizamos error cuadrático medio (RMS) de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c013-621">In our case we will use hello root mean square (RMS) error.</span></span> <span data-ttu-id="3c013-622">Hello función siguiente calcula el Hola RMS error entre dos series.</span><span class="sxs-lookup"><span data-stu-id="3c013-622">hello following function computes hello RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="3c013-623">Al igual que con hello `log.transform()` función analizamos en Hola sección "Transformaciones" Value", no hay una gran cantidad de código de recuperación de comprobación y la excepción de error con el de esta función.</span><span class="sxs-lookup"><span data-stu-id="3c013-623">As with hello `log.transform()` function we discussed in hello "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="3c013-624">principios de Hello empleados se Hola mismo.</span><span class="sxs-lookup"><span data-stu-id="3c013-624">hello principles employed are hello same.</span></span> <span data-ttu-id="3c013-625">Hello realizan trabajo en dos lugares ajustados en `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="3c013-625">hello work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="3c013-626">En primer lugar, serie temporal de hello es exponentiated, ya que hemos estado trabajando con registros de Hola de valores de hello.</span><span class="sxs-lookup"><span data-stu-id="3c013-626">First, hello time series are exponentiated, since we have been working with hello logs of hello values.</span></span> <span data-ttu-id="3c013-627">En segundo lugar, se calcula el error de RMS de hello real.</span><span class="sxs-lookup"><span data-stu-id="3c013-627">Second, hello actual RMS error is computed.</span></span>  

<span data-ttu-id="3c013-628">Equipado con un Hola de toomeasure de la función error de RMS, vamos a compilar y una trama de datos que contienen errores de hello RMS de salida.</span><span class="sxs-lookup"><span data-stu-id="3c013-628">Equipped with a function toomeasure hello RMS error, let's build and output a dataframe containing hello RMS errors.</span></span> <span data-ttu-id="3c013-629">Se incluye términos Hola tendencia exclusivamente para modelo y el modelo completo de hello con factores estacionales.</span><span class="sxs-lookup"><span data-stu-id="3c013-629">We will include terms for hello trend model alone and hello complete model with seasonal factors.</span></span> <span data-ttu-id="3c013-630">Hello código siguiente Hola trabajo mediante el uso de modelos lineales dos Hola que se ha construido.</span><span class="sxs-lookup"><span data-stu-id="3c013-630">hello following code does hello job by using hello two linear models we have constructed.</span></span>

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="3c013-631">Ejecutar este código genera la salida de hello se muestra en la figura 27 en puerto de salida del conjunto de datos de resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="3c013-631">Running this code produces hello output shown in Figure 27 at hello Result Dataset output port.</span></span>

![Comparación de errores de RMS para los modelos de Hola][26]

<span data-ttu-id="3c013-633">*Ilustración 27. Comparación de errores de RMS para los modelos de Hola.*</span><span class="sxs-lookup"><span data-stu-id="3c013-633">*Figure 27. Comparison of RMS errors for hello models.*</span></span>

<span data-ttu-id="3c013-634">En estos resultados, vemos que la adición Hola factores estacionales toohello modelo reduce el error de RMS Hola significativamente.</span><span class="sxs-lookup"><span data-stu-id="3c013-634">From these results, we see that adding hello seasonal factors toohello model reduces hello RMS error significantly.</span></span> <span data-ttu-id="3c013-635">Demasiado Evidentemente, error Hola RMS para los datos de entrenamiento de hello es un poco menor que para hello de previsión.</span><span class="sxs-lookup"><span data-stu-id="3c013-635">Not too surprisingly, hello RMS error for hello training data is a bit less than for hello forecast.</span></span>

## <span data-ttu-id="3c013-636"><a id="appendixa"></a>Apéndice A: Guía tooRStudio</span><span class="sxs-lookup"><span data-stu-id="3c013-636"><a id="appendixa"></a>APPENDIX A: Guide tooRStudio</span></span>
<span data-ttu-id="3c013-637">RStudio está muy bien documentado, por lo que en este apéndice proporcionarán algunos toohello vínculos secciones claves de hello RStudio documentación tooget inició.</span><span class="sxs-lookup"><span data-stu-id="3c013-637">RStudio is quite well documented, so in this appendix I will provide some links toohello key sections of hello RStudio documentation tooget you started.</span></span>

1. <span data-ttu-id="3c013-638">Creación de proyectos</span><span class="sxs-lookup"><span data-stu-id="3c013-638">Creating projects</span></span>
   
   <span data-ttu-id="3c013-639">Puede organizar y administrar el código de R en proyectos mediante RStudio.</span><span class="sxs-lookup"><span data-stu-id="3c013-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="3c013-640">documentación de Hola que usa proyectos se puede encontrar en https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span><span class="sxs-lookup"><span data-stu-id="3c013-640">hello documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="3c013-641">Recomienda que siga estas instrucciones y crear un proyecto para obtener ejemplos de código de hello R en este documento.</span><span class="sxs-lookup"><span data-stu-id="3c013-641">I recommend that you follow these directions and create a project for hello R code examples in this document.</span></span>  
2. <span data-ttu-id="3c013-642">Edición y ejecución de código R</span><span class="sxs-lookup"><span data-stu-id="3c013-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="3c013-643">RStudio proporciona un entorno integrado para editar y ejecutar código R.</span><span class="sxs-lookup"><span data-stu-id="3c013-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="3c013-644">La documentación se encuentra en https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span><span class="sxs-lookup"><span data-stu-id="3c013-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="3c013-645">Depuración</span><span class="sxs-lookup"><span data-stu-id="3c013-645">Debugging</span></span>
   
   <span data-ttu-id="3c013-646">RStudio incluye eficaces capacidades de depuración.</span><span class="sxs-lookup"><span data-stu-id="3c013-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="3c013-647">Encontrará la documentación de estas características en https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span><span class="sxs-lookup"><span data-stu-id="3c013-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="3c013-648">características de solución de problemas de punto de interrupción de Hola se documentan en https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="3c013-648">hello breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <span data-ttu-id="3c013-649"><a id="appendixb"></a>APÉNDICE B: lectura adicional</span><span class="sxs-lookup"><span data-stu-id="3c013-649"><a id="appendixb"></a>APPENDIX B: Further reading</span></span>
<span data-ttu-id="3c013-650">Este tutorial abarca Hola Fundamentos de la programación de R de lo que necesita toouse Hola lenguaje R con estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="3c013-650">This R programming tutorial covers hello basics of what you need toouse hello R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="3c013-651">Si no está familiarizado con el código R, encontrará dos introducciones disponibles en CRAN:</span><span class="sxs-lookup"><span data-stu-id="3c013-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="3c013-652">R para principiantes por Emmanuel Paradis es un toostart ideal en http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span><span class="sxs-lookup"><span data-stu-id="3c013-652">R for Beginners by Emmanuel Paradis is a good place toostart at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="3c013-653">Una visita de introducción por W. N.</span><span class="sxs-lookup"><span data-stu-id="3c013-653">An Introduction tooR by W. N.</span></span> <span data-ttu-id="3c013-654">Venables et.</span><span class="sxs-lookup"><span data-stu-id="3c013-654">Venables et.</span></span> <span data-ttu-id="3c013-655">al.</span><span class="sxs-lookup"><span data-stu-id="3c013-655">al.</span></span> <span data-ttu-id="3c013-656">profundiza un poco más en la materia. La encontrará en http://cran.r-project.org/doc/manuals/R-intro.html.</span><span class="sxs-lookup"><span data-stu-id="3c013-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="3c013-657">Existen muchas obras sobre el código R que pueden servirle como punto de partida.</span><span class="sxs-lookup"><span data-stu-id="3c013-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="3c013-658">Estas son algunas que considero más útiles:</span><span class="sxs-lookup"><span data-stu-id="3c013-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="3c013-659">Hola carátulas de programación en R: un paseo de estadística diseño de Software por Norman Matloff es un tooprogramming introducción excelente en R.</span><span class="sxs-lookup"><span data-stu-id="3c013-659">hello Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction tooprogramming in R.</span></span>  
* <span data-ttu-id="3c013-660">Libro de cocina R por Paul Teetor proporciona un enfoque problema y solución toousing R.</span><span class="sxs-lookup"><span data-stu-id="3c013-660">R Cookbook by Paul Teetor provides a problem and solution approach toousing R.</span></span>  
* <span data-ttu-id="3c013-661">R in Action de Robert Kabacoff es otro libro que puede resultarle muy útil.</span><span class="sxs-lookup"><span data-stu-id="3c013-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="3c013-662">sitio Web de Hello complementaria R rápida es un recurso útil en http://www.statmethods.net/.</span><span class="sxs-lookup"><span data-stu-id="3c013-662">hello companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="3c013-663">R Inferno por Patrick Burns es un libro sorprendentemente divertido que se ocupa de un número de complicada y difíciles de temas que se pueden encontrar cuando se programan en la libreta de hello r. está disponible de forma gratuita en http://www.burns-stat.com/documents/books/the-r-inferno/.</span><span class="sxs-lookup"><span data-stu-id="3c013-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. hello book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="3c013-664">Si desea profundización en temas avanzados de R, eche un vistazo a la libreta de hello avanzadas R por Hadley Wickham.</span><span class="sxs-lookup"><span data-stu-id="3c013-664">If you want a deep dive into advanced topics in R, have a look at hello book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="3c013-665">Hola versión en línea de este libro está disponible de forma gratuita en http://adv-r.had.co.nz/.</span><span class="sxs-lookup"><span data-stu-id="3c013-665">hello online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="3c013-666">Encontrará un catálogo tiempo serie de paquetes de R en hello CRAN tareas vista para el análisis de series temporales: http://cran.r-project.org/web/views/TimeSeries.html.</span><span class="sxs-lookup"><span data-stu-id="3c013-666">A catalogue of R time series packages can be found in hello CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="3c013-667">Para obtener información sobre los paquetes de objeto de serie de tiempo específico, debe hacer referencia a documentación toohello de ese paquete.</span><span class="sxs-lookup"><span data-stu-id="3c013-667">For information on specific time series object packages, you should refer toohello documentation for that package.</span></span>

<span data-ttu-id="3c013-668">Hola guía introductoria serie temporal con R por Paul Cowpertwait y Andrew Metcalfe proporciona una introducción toousing R para análisis de series temporales.</span><span class="sxs-lookup"><span data-stu-id="3c013-668">hello book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction toousing R for time series analysis.</span></span> <span data-ttu-id="3c013-669">No obstante, existen muchos más textos teóricos que proporcionan ejemplos de R.</span><span class="sxs-lookup"><span data-stu-id="3c013-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="3c013-670">Algunos recursos excelentes en Internet:</span><span class="sxs-lookup"><span data-stu-id="3c013-670">Some great internet resources:</span></span>

* <span data-ttu-id="3c013-671">DataCamp: DataCamp enseña R en comodidad Hola del explorador con vídeo lecciones y ejercicios de codificación.</span><span class="sxs-lookup"><span data-stu-id="3c013-671">DataCamp: DataCamp teaches R in hello comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="3c013-672">Hay interactivos tutoriales sobre técnicas de R más recientes de Hola y paquetes.</span><span class="sxs-lookup"><span data-stu-id="3c013-672">There are interactive tutorials on hello latest R techniques and packages.</span></span> <span data-ttu-id="3c013-673">Realice el tutorial de R libre interactivo de Hola a https://www.datacamp.com/courses/introduction-to-r</span><span class="sxs-lookup"><span data-stu-id="3c013-673">Take hello free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="3c013-674">Una guía de introducción a R de Programiz en https://www.programiz.com/r-programming</span><span class="sxs-lookup"><span data-stu-id="3c013-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="3c013-675">Un tutorial rápido de R Kelly Black de la Universidad de Clarkson: http://www.cyclismo.org/tutorial/R/</span><span class="sxs-lookup"><span data-stu-id="3c013-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="3c013-676">Recopilación de más de 60 recursos de R en http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span><span class="sxs-lookup"><span data-stu-id="3c013-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
