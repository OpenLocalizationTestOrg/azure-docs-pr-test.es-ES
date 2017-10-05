---
title: "Tutorial rápido del lenguaje R para Machine Learning | Microsoft Docs"
description: "Use este tutorial para empezar a utilizar rápidamente el lenguaje de programación R con Azure Machine Learning Studio con el fin de crear una solución de previsión."
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
ms.openlocfilehash: 598f5ce445e520b6cdc347c80f7f3dcbc9c2c9e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="quickstart-tutorial-for-the-r-programming-language-for-azure-machine-learning"></a><span data-ttu-id="48fb5-104">Tutorial de inicio rápido en la programación en lenguaje R para Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="48fb5-104">Quickstart tutorial for the R programming language for Azure Machine Learning</span></span>

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a><span data-ttu-id="48fb5-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="48fb5-105">Introduction</span></span>
<span data-ttu-id="48fb5-106">Este tutorial rápido le ayudará a comenzar a ampliar Aprendizaje automático de Azure mediante el uso del lenguaje de programación R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-106">This quickstart tutorial helps you quickly start extending Azure Machine Learning by using the R programming language.</span></span> <span data-ttu-id="48fb5-107">Siga este tutorial de programación R para crear, probar y ejecutar código R en Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="48fb5-107">Follow this R programming tutorial to create, test and execute R code within Azure Machine Learning.</span></span> <span data-ttu-id="48fb5-108">A medida que vaya avanzando en este tutorial, creará una solución completa de previsión mediante el lenguaje R en Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="48fb5-108">As you work through tutorial, you will create a complete forecasting solution by using the R language in Azure Machine Learning.</span></span>  

<span data-ttu-id="48fb5-109">Aprendizaje automático de Microsoft Azure contiene muchos módulos versátiles de manipulación de datos y aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="48fb5-109">Microsoft Azure Machine Learning contains many powerful machine learning and data manipulation modules.</span></span> <span data-ttu-id="48fb5-110">El lenguaje R se conoce como la lingua franca del análisis de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-110">The powerful R language has been described as the lingua franca of analytics.</span></span> <span data-ttu-id="48fb5-111">Afortunadamente, la manipulación y el análisis de datos en Aprendizaje automático de Azure se pueden ampliar mediante R. Esta combinación une la escalabilidad y sencillez en la implementación de Aprendizaje automático de Azure con la flexibilidad y el análisis profundo de R.
</span><span class="sxs-lookup"><span data-stu-id="48fb5-111">Happily, analytics and data manipulation in Azure Machine Learning can be extended by using R. This combination provides the scalability and ease of deployment of Azure Machine Learning with the flexibility and deep analytics of R.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-the-dataset"></a><span data-ttu-id="48fb5-112">Previsión y conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="48fb5-112">Forecasting and the dataset</span></span>
<span data-ttu-id="48fb5-113">La previsión es un método de análisis ampliamente utilizado y bastante útil.</span><span class="sxs-lookup"><span data-stu-id="48fb5-113">Forecasting is a widely employed and quite useful analytical method.</span></span> <span data-ttu-id="48fb5-114">La previsión suele utilizarse para crear predicciones de ventas de productos estacionales, para determinar los niveles de inventario óptimos o para predecir las variables macroeconómicas.</span><span class="sxs-lookup"><span data-stu-id="48fb5-114">Common uses range from predicting sales of seasonal items, determining optimal inventory levels, to predicting macroeconomic variables.</span></span> <span data-ttu-id="48fb5-115">La previsión suele realizarse con modelos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="48fb5-115">Forecasting is typically done with time series models.</span></span>

<span data-ttu-id="48fb5-116">Los datos de series temporales son datos en los que los valores tienen un índice temporal.</span><span class="sxs-lookup"><span data-stu-id="48fb5-116">Time series data is data in which the values have a time index.</span></span> <span data-ttu-id="48fb5-117">El índice temporal puede ser normal, es decir, cada mes o cada minuto; o bien puede ser irregular.</span><span class="sxs-lookup"><span data-stu-id="48fb5-117">The time index can be regular, e.g. every month or every minute, or irregular.</span></span> <span data-ttu-id="48fb5-118">Los modelos de serie temporal se basan en datos de series temporales.</span><span class="sxs-lookup"><span data-stu-id="48fb5-118">A time series model is based on time series data.</span></span> <span data-ttu-id="48fb5-119">El lenguaje de programación R contiene un marco de trabajo flexible y amplias características de análisis de datos de serie temporales.</span><span class="sxs-lookup"><span data-stu-id="48fb5-119">The R programming language contains a flexible framework and extensive analytics for time series data.</span></span>

<span data-ttu-id="48fb5-120">En esta guía de inicio rápido, trabajaremos con los productos lácteos de California y los datos de precios.</span><span class="sxs-lookup"><span data-stu-id="48fb5-120">In this quickstart guide we will be working with California dairy production and pricing data.</span></span> <span data-ttu-id="48fb5-121">Estos datos incluyen información mensual acerca de la producción de varios de los productos lácteos, así como sobre el precio de la grasa láctea, materia prima de referencia.</span><span class="sxs-lookup"><span data-stu-id="48fb5-121">This data includes monthly information on the production of several dairy products and the price of milk fat, a benchmark commodity.</span></span>

<span data-ttu-id="48fb5-122">Los datos usados en este artículo, junto con scripts R, se pueden [descargar aquí][download].</span><span class="sxs-lookup"><span data-stu-id="48fb5-122">The data used in this article, along with R scripts, can be [downloaded here][download].</span></span> <span data-ttu-id="48fb5-123">Estos datos están tomados de la información disponible de la universidad de Wisconsin en http://future.aae.wisc.edu/tab/production.html.</span><span class="sxs-lookup"><span data-stu-id="48fb5-123">This data was originally synthesized from information available from the University of Wisconsin at http://future.aae.wisc.edu/tab/production.html.</span></span>

### <a name="organization"></a><span data-ttu-id="48fb5-124">Organización</span><span class="sxs-lookup"><span data-stu-id="48fb5-124">Organization</span></span>
<span data-ttu-id="48fb5-125">En esta sección abordaremos distintos pasos a medida que aprenda a crear, probar y ejecutar código R de análisis y manipulación de datos en entornos de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="48fb5-125">We will progress through several steps as you learn how to create, test and execute analytics and data manipulation R code in the Azure Machine Learning environment.</span></span>  

* <span data-ttu-id="48fb5-126">Primero analizaremos los aspectos básicos del uso del lenguaje R en el entorno de Estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="48fb5-126">First we will explore the basics of using the R language in the Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="48fb5-127">A continuación, se tratarán distintos aspectos de la E/S de datos, el código R y los gráficos en entornos de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="48fb5-127">Then we progress to discussing various aspects of I/O for data, R code and graphics in the Azure Machine Learning environment.</span></span>
* <span data-ttu-id="48fb5-128">Llegados a este punto, crearemos la primera parte de nuestra solución de previsión mediante la creación de código para la limpieza y la transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-128">We will then construct the first part of our forecasting solution by creating code for data cleaning and transformation.</span></span>
* <span data-ttu-id="48fb5-129">Con los datos preparados, realizamos un análisis de las correlaciones existentes entre varias de las variables de nuestro conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-129">With our data prepared we will perform an analysis of the correlations between several of the variables in our dataset.</span></span>
* <span data-ttu-id="48fb5-130">Por último, crearemos un modelo de previsión de serie temporal estacional para la producción de leche.</span><span class="sxs-lookup"><span data-stu-id="48fb5-130">Finally, we will create a seasonal time series forecasting model for milk production.</span></span>

## <span data-ttu-id="48fb5-131"><a id="mlstudio"></a>Interacción con el lenguaje R para Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="48fb5-131"><a id="mlstudio"></a>Interact with R language in Machine Learning Studio</span></span>
<span data-ttu-id="48fb5-132">Esta sección le guiará por algunos aspectos básicos de la interacción con el lenguaje de programación R en el entorno de Estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="48fb5-132">This section takes you through some basics of interacting with the R programming language in the Machine Learning Studio environment.</span></span> <span data-ttu-id="48fb5-133">El lenguaje R proporciona una herramienta eficaz para crear módulos de manipulación de datos y de análisis personalizado en el entorno de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="48fb5-133">The R language provides a powerful tool to create customized analytics and data manipulation modules within the Azure Machine Learning environment.</span></span>

<span data-ttu-id="48fb5-134">Utilizaremos RStudio para desarrollar, probar y depurar el código R a escala reducida.</span><span class="sxs-lookup"><span data-stu-id="48fb5-134">I will use RStudio to develop, test and debug R code on a small scale.</span></span> <span data-ttu-id="48fb5-135">A continuación, este código se cortará y pegará en un módulo [Ejecutar script R][execute-r-script] en Machine Learning Studio listo para ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="48fb5-135">This code is then cut and paste into an [Execute R Script][execute-r-script] module in Machine Learning Studio ready to run.</span></span>  

### <a name="the-execute-r-script-module"></a><span data-ttu-id="48fb5-136">Módulo Ejecutar script de R</span><span class="sxs-lookup"><span data-stu-id="48fb5-136">The Execute R Script module</span></span>
<span data-ttu-id="48fb5-137">En Machine Learning Studio, los scripts R se ejecutan dentro del módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-137">Within Machine Learning Studio, R scripts are run within the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="48fb5-138">En la ilustración 1, se muestra un ejemplo del módulo [Ejecutar script R][execute-r-script] en Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="48fb5-138">An example of the [Execute R Script][execute-r-script] module in Machine Learning Studio is shown in Figure 1.</span></span>

 ![Lenguaje de programación R: el módulo Ejecutar script de R seleccionado en Estudio de aprendizaje automático][1]

<span data-ttu-id="48fb5-140">*Ilustración 1. Entorno de Estudio de aprendizaje automático que muestra el módulo Ejecutar script de R seleccionado.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-140">*Figure 1. The Machine Learning Studio environment showing the Execute R Script module selected.*</span></span>

<span data-ttu-id="48fb5-141">Tomando como referencia la ilustración 1, veamos algunas de las partes principales del entorno de Machine Learning Studio necesarias para trabajar con el módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-141">Referring to Figure 1, let's look at some of the key parts of the Machine Learning Studio environment for working with the [Execute R Script][execute-r-script] module.</span></span>

* <span data-ttu-id="48fb5-142">Los módulos utilizados en el experimento se muestran en el panel central.</span><span class="sxs-lookup"><span data-stu-id="48fb5-142">The modules in the experiment are shown in the center pane.</span></span>
* <span data-ttu-id="48fb5-143">La parte superior del panel derecho contiene una ventana para ver y editar los scripts de código R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-143">The upper part of the right pane contains a window to view and edit your R scripts.</span></span>  
* <span data-ttu-id="48fb5-144">La parte inferior del panel derecho muestra algunas propiedades del módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-144">The lower part of right pane shows some properties of the [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="48fb5-145">Para ver los registros de error y de salida, haga clic en los puntos correspondientes de este panel.</span><span class="sxs-lookup"><span data-stu-id="48fb5-145">You can view the error and output logs by clicking on the appropriate spots of this pane.</span></span>

<span data-ttu-id="48fb5-146">Por supuesto, analizaremos el módulo [Ejecutar script R][execute-r-script] con mayor detalle en el resto de este documento.</span><span class="sxs-lookup"><span data-stu-id="48fb5-146">We will, of course, be discussing the [Execute R Script][execute-r-script] in greater detail in the rest of this document.</span></span>

<span data-ttu-id="48fb5-147">Cuando se utilicen funciones complejas de R, es recomendable editar, probar y depurar el código en RStudio.</span><span class="sxs-lookup"><span data-stu-id="48fb5-147">When working with complex R functions, I recommend that you edit, test and debug in RStudio.</span></span> <span data-ttu-id="48fb5-148">Al igual que con cualquier desarrollo de software, amplíe el código de forma incremental y pruébelo en casos de prueba más sencillos. </span><span class="sxs-lookup"><span data-stu-id="48fb5-148">As with any software development, extend your code incrementally and test it on small simple test cases.</span></span> <span data-ttu-id="48fb5-149">Luego, corte y pegue las funciones en la ventana de scripts R del módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-149">Then cut and paste your functions into the R script window of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="48fb5-150">Este enfoque le permite aprovechar el entorno de desarrollo integrado (IDE) de RStudio y la eficacia de Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="48fb5-150">This approach allows you to harness both the RStudio integrated development environment (IDE) and the power of Azure Machine Learning.</span></span>  

#### <a name="execute-r-code"></a><span data-ttu-id="48fb5-151">Ejecución del código R</span><span class="sxs-lookup"><span data-stu-id="48fb5-151">Execute R code</span></span>
<span data-ttu-id="48fb5-152">Cualquier código R del módulo [Ejecutar script R][execute-r-script] se ejecutará cuando haga clic en el botón **Ejecutar** para ejecutar el experimento.</span><span class="sxs-lookup"><span data-stu-id="48fb5-152">Any R code in the [Execute R Script][execute-r-script] module will execute when you run the experiment by clicking on the **Run** button.</span></span> <span data-ttu-id="48fb5-153">Cuando haya finalizado la ejecución, aparecerá una marca de verificación en el icono [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-153">When execution has completed, a check mark will appear on the [Execute R Script][execute-r-script] icon.</span></span>

#### <a name="defensive-r-coding-for-azure-machine-learning"></a><span data-ttu-id="48fb5-154">Codificación R defensiva para Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="48fb5-154">Defensive R coding for Azure Machine Learning</span></span>
<span data-ttu-id="48fb5-155">Si está desarrollando código R para un servicio web utilizando Aprendizaje automático de Azure, deberá planear cómo tratará el código las entradas de datos inesperadas y las excepciones.</span><span class="sxs-lookup"><span data-stu-id="48fb5-155">If you are developing R code for, say, a web service by using Azure Machine Learning, you should definitely plan how your code will deal with an unexpected data input and exceptions.</span></span> <span data-ttu-id="48fb5-156">Para mantener la claridad, he preferido no entrar en muchos detalles en cuanto al método de comprobación o control de excepciones en la mayoría de los ejemplos de código mostrados.</span><span class="sxs-lookup"><span data-stu-id="48fb5-156">To maintain clarity, I have not included much in the way of checking or exception handling in most of the code examples shown.</span></span> <span data-ttu-id="48fb5-157">Sin embargo, conforme avancemos compartiré varios ejemplos de funciones mediante la capacidad de control de excepciones de R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-157">However, as we proceed I will give you several examples of functions by using R's exception handling capability.</span></span>  

<span data-ttu-id="48fb5-158">Si necesita un tratamiento más completado del control de excepciones de R, le recomiendo que lea las secciones correspondientes del manual de Wickham que se detallan en el [Apéndice B: información adicional](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="48fb5-158">If you need a more complete treatment of R exception handling, I recommend you read the applicable sections of the book by Wickham listed in [Appendix B - Further Reading](#appendixb).</span></span>

#### <a name="debug-and-test-r-in-machine-learning-studio"></a><span data-ttu-id="48fb5-159">Depuración y prueba de R en Estudio de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="48fb5-159">Debug and test R in Machine Learning Studio</span></span>
<span data-ttu-id="48fb5-160">Nuevamente, recomiendo probar y depurar el código de R a escala reducida en RStudio.</span><span class="sxs-lookup"><span data-stu-id="48fb5-160">To reiterate, I recommend you test and debug your R code on a small scale in RStudio.</span></span> <span data-ttu-id="48fb5-161">Sin embargo, hay casos en los que necesitará rastrear problemas de código R en el propio módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-161">However, there are cases where you will need to track down R code problems in the [Execute R Script][execute-r-script] itself.</span></span> <span data-ttu-id="48fb5-162">Además, se recomienda comprobar los resultados en Estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="48fb5-162">In addition, it is good practice to check your results in Machine Learning Studio.</span></span>

<span data-ttu-id="48fb5-163">Los resultados de la ejecución del código R y de la plataforma Aprendizaje automático de Azure pueden encontrarse en el archivo output.log.</span><span class="sxs-lookup"><span data-stu-id="48fb5-163">Output from the execution of your R code and on the Azure Machine Learning platform is found primarily in output.log.</span></span> <span data-ttu-id="48fb5-164">Se mostrará información adicional en el archivo error.log.</span><span class="sxs-lookup"><span data-stu-id="48fb5-164">Some additional information will be seen in error.log.</span></span>  

<span data-ttu-id="48fb5-165">Si se produce un error en Estudio de aprendizaje automático durante la ejecución del código R, lo primero que debe hacer es consultar el archivo error.log.</span><span class="sxs-lookup"><span data-stu-id="48fb5-165">If an error occurs in Machine Learning Studio while running your R code, your first course of action should be to look at error.log.</span></span> <span data-ttu-id="48fb5-166">Este archivo puede contener mensajes de error útiles que le ayudarán a comprender y a corregir el error.</span><span class="sxs-lookup"><span data-stu-id="48fb5-166">This file can contain useful error messages to help you understand and correct your error.</span></span> <span data-ttu-id="48fb5-167">Para ver el archivo error.log, haga clic en **Ver registro de errores** en el **panel de propiedades** del módulo [Ejecutar script R][execute-r-script] que contiene el error.</span><span class="sxs-lookup"><span data-stu-id="48fb5-167">To view error.log, click on **View error log** on the **properties pane** for the [Execute R Script][execute-r-script] containing the error.</span></span>

<span data-ttu-id="48fb5-168">Por ejemplo, ejecuté el siguiente código R con una variable y sin definir en un módulo [Ejecutar script R][execute-r-script]:</span><span class="sxs-lookup"><span data-stu-id="48fb5-168">For example, I ran the following R code, with an undefined variable y, in an [Execute R Script][execute-r-script] module:</span></span>

    x <- 1.0
    z <- x + y

<span data-ttu-id="48fb5-169">Este código no se puede ejecutar, lo que da lugar a un error.</span><span class="sxs-lookup"><span data-stu-id="48fb5-169">This code fails to execute, resulting in an error condition.</span></span> <span data-ttu-id="48fb5-170">Al hacer clic en **Ver registro de errores** en el **panel de propiedades**, se muestra la pantalla de la ilustración 2.</span><span class="sxs-lookup"><span data-stu-id="48fb5-170">Clicking on **View error log** on the **properties pane** produces the display shown in Figure 2.</span></span>

  ![Mensaje de error emergente][2]

<span data-ttu-id="48fb5-172">*Ilustración 2. Mensaje de error emergente.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-172">*Figure 2. Error message pop-up.*</span></span>

<span data-ttu-id="48fb5-173">Parece que tenemos que consultar el archivo output.log para poder ver el mensaje de error R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-173">It looks like we need to look in output.log to see the R error message.</span></span> <span data-ttu-id="48fb5-174">Haga clic en el módulo [Ejecutar script R][execute-r-script] y, luego, en el elemento **Ver archivo output.log** del **panel de propiedades** que se encuentra a la derecha.</span><span class="sxs-lookup"><span data-stu-id="48fb5-174">Click on the [Execute R Script][execute-r-script] and then click on the **View output.log** item on the **properties pane** to the right.</span></span> <span data-ttu-id="48fb5-175">Se abrirá una nueva ventana del explorador y podrá ver lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-175">A new browser window opens, and I see the following.</span></span>

    [Critical]     Error: Error 0063: The following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

<span data-ttu-id="48fb5-176">Este mensaje de error no contiene sorpresas e identifica claramente el problema.</span><span class="sxs-lookup"><span data-stu-id="48fb5-176">This error message contains no surprises and clearly identifies the problem.</span></span>

<span data-ttu-id="48fb5-177">Imprima estos valores en el archivo output.log para comprobar el valor de los objetos en R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-177">To inspect the value of any object in R, you can print these values to the output.log file.</span></span> <span data-ttu-id="48fb5-178">Las reglas para examinar los valores de objeto son las mismas que las que se usan en sesiones interactivas de código R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-178">The rules for examining object values are essentially the same as in an interactive R session.</span></span> <span data-ttu-id="48fb5-179">Por ejemplo, si escribe un nombre de variable en una línea, el valor del objeto se imprimirá al archivo output.log.</span><span class="sxs-lookup"><span data-stu-id="48fb5-179">For example, if you type a variable name on a line, the value of the object will be printed to the output.log file.</span></span>  

#### <a name="packages-in-machine-learning-studio"></a><span data-ttu-id="48fb5-180">Paquetes de Estudio de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="48fb5-180">Packages in Machine Learning Studio</span></span>
<span data-ttu-id="48fb5-181">Aprendizaje automático de Azure incluye más de 350 paquetes del lenguaje R preinstalados.</span><span class="sxs-lookup"><span data-stu-id="48fb5-181">Azure Machine Learning comes with over 350 preinstalled R language packages.</span></span> <span data-ttu-id="48fb5-182">Puede usar el código siguiente en el módulo [Ejecutar script R][execute-r-script] para recuperar una lista de paquetes preinstalados.</span><span class="sxs-lookup"><span data-stu-id="48fb5-182">You can use the following code in the [Execute R Script][execute-r-script] module to retrieve a list of the preinstalled packages.</span></span>

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

<span data-ttu-id="48fb5-183">Siga leyendo si no comprende la última línea de este código.</span><span class="sxs-lookup"><span data-stu-id="48fb5-183">If you don't understand the last line of this code at the moment, read on.</span></span> <span data-ttu-id="48fb5-184">En el resto del documento se describe con detalle el uso de R en el entorno Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="48fb5-184">In the rest of this document we will extensively discuss using R in the Azure Machine Learning environment.</span></span>

### <a name="introduction-to-rstudio"></a><span data-ttu-id="48fb5-185">Introducción a RStudio</span><span class="sxs-lookup"><span data-stu-id="48fb5-185">Introduction to RStudio</span></span>
<span data-ttu-id="48fb5-186">RStudio es un IDE ampliamente usado para R. Utilizaremos RStudio para editar, probar y depurar el código R utilizado en esta guía de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="48fb5-186">RStudio is a widely used IDE for R. I will use RStudio for editing, testing and debugging some of the R code used in this quick start guide.</span></span> <span data-ttu-id="48fb5-187">Una vez que el código R se pruebe y esté listo, simplemente deberá cortar y pegar desde el editor de RStudio en un módulo [Ejecutar script R][execute-r-script] de Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="48fb5-187">Once R code is tested and ready, you simply cut and paste from the RStudio editor into a Machine Learning Studio [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="48fb5-188">Si no tiene instalado el lenguaje de programación R en su equipo de sobremesa, es recomendable que lo instale ahora.</span><span class="sxs-lookup"><span data-stu-id="48fb5-188">If you do not have the R programming language installed on your desktop machine, I recommend you do so now.</span></span> <span data-ttu-id="48fb5-189">Encontrará descargas gratuitas del lenguaje R abierto están disponibles en la red completa de archivos de R o CRAN en [http://www.r-project.org/](http://www.r-project.org/).</span><span class="sxs-lookup"><span data-stu-id="48fb5-189">Free downloads of open source R language are available at the Comprehensive R Archive Network (CRAN) at [http://www.r-project.org/](http://www.r-project.org/).</span></span> <span data-ttu-id="48fb5-190">Hay descargas disponibles para Windows, Mac OS y Linux/UNIX.</span><span class="sxs-lookup"><span data-stu-id="48fb5-190">There are downloads available for Windows, Mac OS, and Linux/UNIX.</span></span> <span data-ttu-id="48fb5-191">Elija el espejo más cercano a su ubicación y siga las instrucciones de descarga.</span><span class="sxs-lookup"><span data-stu-id="48fb5-191">Choose a nearby mirror and follow the download directions.</span></span> <span data-ttu-id="48fb5-192">Además, CRAN contiene una gran cantidad de paquetes de manipulación de datos y análisis de utilidad.</span><span class="sxs-lookup"><span data-stu-id="48fb5-192">In addition, CRAN contains a wealth of useful analytics and data manipulation packages.</span></span>

<span data-ttu-id="48fb5-193">Si no está familiarizado con RStudio, descargue e instale la versión de escritorio.</span><span class="sxs-lookup"><span data-stu-id="48fb5-193">If you are new to RStudio, you should download and install the desktop version.</span></span> <span data-ttu-id="48fb5-194">Encontrará descargas de RStudio para Windows, Mac OS y Linux/UNIX en http://www.rstudio.com/products/RStudio/.</span><span class="sxs-lookup"><span data-stu-id="48fb5-194">You can find the RStudio downloads for Windows, Mac OS, and Linux/UNIX at http://www.rstudio.com/products/RStudio/.</span></span> <span data-ttu-id="48fb5-195">Siga las instrucciones proporcionadas para instalar RStudio en su equipo.</span><span class="sxs-lookup"><span data-stu-id="48fb5-195">Follow the directions provided to install RStudio on your desktop machine.</span></span>  

<span data-ttu-id="48fb5-196">Encontrará un tutorial de introducción a RStudio en https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span><span class="sxs-lookup"><span data-stu-id="48fb5-196">A tutorial introduction to RStudio is available at https://support.rstudio.com/hc/sections/200107586-Using-RStudio.</span></span>

<span data-ttu-id="48fb5-197">En el [Apéndice A][appendixa], encontrará información adicional sobre el uso de RStudio.</span><span class="sxs-lookup"><span data-stu-id="48fb5-197">I provide some additional information on using RStudio in [Appendix A][appendixa].</span></span>  

## <span data-ttu-id="48fb5-198"><a id="scriptmodule"></a>Obtención de datos dentro y fuera del módulo Ejecutar script de R</span><span class="sxs-lookup"><span data-stu-id="48fb5-198"><a id="scriptmodule"></a>Get data in and out of the Execute R Script module</span></span>
<span data-ttu-id="48fb5-199">En esta sección, veremos cómo introducir y extraer datos del módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-199">In this section we will discuss how you get data into and out of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="48fb5-200">Revisaremos cómo controlar los distintos tipos de datos leídos dentro y fuera del módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-200">We will review how to handle various data types read into and out of the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="48fb5-201">Encontrará el código completo de esta sección en el archivo zip que descargó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-201">The complete code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="load-and-check-data-in-machine-learning-studio"></a><span data-ttu-id="48fb5-202">Carga y comprobación de datos en Estudio de aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="48fb5-202">Load and check data in Machine Learning Studio</span></span>
#### <span data-ttu-id="48fb5-203"><a id="loading"></a>Carga del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="48fb5-203"><a id="loading"></a>Load the dataset</span></span>
<span data-ttu-id="48fb5-204">En primer lugar, comience por cargar el archivo **csdairydata.csv** en Estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="48fb5-204">We will start by loading the **csdairydata.csv** file into Azure Machine Learning Studio.</span></span>

* <span data-ttu-id="48fb5-205">Iniciar su entorno Estudio de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="48fb5-205">Start your Azure Machine Learning Studio environment.</span></span>
* <span data-ttu-id="48fb5-206">Haga clic en **+ NUEVO** en la parte inferior izquierda de la pantalla y seleccione **Conjunto de datos**.</span><span class="sxs-lookup"><span data-stu-id="48fb5-206">Click on **+ NEW** at the lower left of your screen and select **Dataset**.</span></span>
* <span data-ttu-id="48fb5-207">Seleccione **From Local File** (De archivo local) y luego **Examinar** para seleccionar el archivo.</span><span class="sxs-lookup"><span data-stu-id="48fb5-207">Select **From Local File**, and then **Browse** to select the file.</span></span>
* <span data-ttu-id="48fb5-208">Asegúrese de haber seleccionado la opción **Archivo CSV genérico con encabezado (.csv)** como el tipo de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-208">Make sure you have selected **Generic CSV file with header (.csv)** as the type for the dataset.</span></span>
* <span data-ttu-id="48fb5-209">Haga clic en la marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="48fb5-209">Click the check mark.</span></span>
* <span data-ttu-id="48fb5-210">Una vez cargado el conjunto de datos, debería ver el nuevo conjunto de datos haciendo clic en la pestaña **Conjuntos de datos** .</span><span class="sxs-lookup"><span data-stu-id="48fb5-210">After the dataset has been uploaded, you should see the new dataset by clicking on the **Datasets** tab.</span></span>  

#### <a name="create-an-experiment"></a><span data-ttu-id="48fb5-211">Creación de un experimento</span><span class="sxs-lookup"><span data-stu-id="48fb5-211">Create an experiment</span></span>
<span data-ttu-id="48fb5-212">Ahora que tenemos algunos datos en Estudio de aprendizaje automático, debemos crear un experimento para realizar el análisis.</span><span class="sxs-lookup"><span data-stu-id="48fb5-212">Now that we have some data in Machine Learning Studio, we need to create an experiment to do the analysis.</span></span>  

* <span data-ttu-id="48fb5-213">Haga clic en **+ NUEVO** en la parte inferior izquierda y seleccione **Experiment** (Experimento) y luego **Blank Experiment** (Experimento en blanco).</span><span class="sxs-lookup"><span data-stu-id="48fb5-213">Click on **+ NEW** at the lower left and select **Experiment**, then **Blank Experiment**.</span></span>
* <span data-ttu-id="48fb5-214">Para asignar un nombre al experimento, seleccione y modifique el título **Experimento creado el...** en la parte superior de la página.</span><span class="sxs-lookup"><span data-stu-id="48fb5-214">You can name your experiment by selecting, and modifying, the **Experiment created on ...** title at the top of the page.</span></span> <span data-ttu-id="48fb5-215">Por ejemplo, cámbielo a **Análisis de productos lácteos de CA**.</span><span class="sxs-lookup"><span data-stu-id="48fb5-215">For example, changing it to **CA Dairy Analysis**.</span></span>
* <span data-ttu-id="48fb5-216">A la izquierda de la página del experimento, expanda **Saved Datasets** (Conjuntos de datos guardados) y luego **My Datasets** (Mis conjuntos de datos).</span><span class="sxs-lookup"><span data-stu-id="48fb5-216">On the left of the experiment page, expand **Saved Datasets**, and then **My Datasets**.</span></span> <span data-ttu-id="48fb5-217">Debería ver **cadairydata.csv** que ha cargado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-217">You should see the **cadairydata.csv** that you uploaded earlier.</span></span>
* <span data-ttu-id="48fb5-218">Arrastre y suelte el **conjunto de datos csdairydata.csv** en el experimento.</span><span class="sxs-lookup"><span data-stu-id="48fb5-218">Drag and drop the **csdairydata.csv dataset** onto the experiment.</span></span>
* <span data-ttu-id="48fb5-219">En el cuadro **Búsqueda de elementos de experimento** ubicado en la parte superior del panel izquierdo, escriba [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-219">In the **Search experiment items** box on the top of the left pane, type [Execute R Script][execute-r-script].</span></span> <span data-ttu-id="48fb5-220">El módulo aparecerá en la lista de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="48fb5-220">You will see the module appear in the search list.</span></span>
* <span data-ttu-id="48fb5-221">Arrastre y suelte el módulo [Ejecutar script R][execute-r-script] en el pallet.</span><span class="sxs-lookup"><span data-stu-id="48fb5-221">Drag and drop the [Execute R Script][execute-r-script] module onto your pallet.</span></span>  
* <span data-ttu-id="48fb5-222">Conecte la salida del **conjunto de datos csdairydata.csv** a la entrada ubicada más a la izquierda (**Dataset1**) del módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-222">Connect the output of the **csdairydata.csv dataset** to the leftmost input (**Dataset1**) of the [Execute R Script][execute-r-script].</span></span>
* <span data-ttu-id="48fb5-223">**¡Recuerde hacer clic en 'Guardar'!.**</span><span class="sxs-lookup"><span data-stu-id="48fb5-223">**Don't forget to click on 'Save'!**</span></span>  

<span data-ttu-id="48fb5-224">En este punto el experimento debería tener un aspecto similar al de la ilustración 3.</span><span class="sxs-lookup"><span data-stu-id="48fb5-224">At this point your experiment should look something like Figure 3.</span></span>

![Experimento Análisis de productos lácteos de CA con el conjunto de datos y el módulo Ejecutar script de R.][3]

<span data-ttu-id="48fb5-226">*Ilustración 3. Experimento Análisis de productos lácteos de CA con el conjunto de datos y el módulo Ejecutar script de R.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-226">*Figure 3. The CA Dairy Analysis experiment with dataset and Execute R Script module.*</span></span>

#### <a name="check-on-the-data"></a><span data-ttu-id="48fb5-227">Comprobación de los datos</span><span class="sxs-lookup"><span data-stu-id="48fb5-227">Check on the data</span></span>
<span data-ttu-id="48fb5-228">Echemos un vistazo a los datos que se han cargado en nuestro experimento.</span><span class="sxs-lookup"><span data-stu-id="48fb5-228">Let's have a look at the data we have loaded into our experiment.</span></span> <span data-ttu-id="48fb5-229">En el experimento, haga clic en el resultado del **conjunto de datos cadairydata.csv** y seleccione **Visualizar**.</span><span class="sxs-lookup"><span data-stu-id="48fb5-229">In the experiment, click on the output of the **cadairydata.csv dataset** and select **visualize**.</span></span> <span data-ttu-id="48fb5-230">Debería ver algo parecido a lo que se muestra en la ilustración 4.</span><span class="sxs-lookup"><span data-stu-id="48fb5-230">You should see something like Figure 4.</span></span>  

![Resumen del conjunto de datos cadairydata.csv][4]

<span data-ttu-id="48fb5-232">*Ilustración 4. Resumen del conjunto de datos cadairydata.csv.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-232">*Figure 4. Summary of the cadairydata.csv dataset.*</span></span>

<span data-ttu-id="48fb5-233">En esta vista hay una gran cantidad de información útil.</span><span class="sxs-lookup"><span data-stu-id="48fb5-233">In this view we see a lot of useful information.</span></span> <span data-ttu-id="48fb5-234">Pueden verse las primeras filas de dicho conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-234">We can see the first several rows of that dataset.</span></span> <span data-ttu-id="48fb5-235">Si se selecciona una columna, la sección de estadísticas muestra más información sobre ella.</span><span class="sxs-lookup"><span data-stu-id="48fb5-235">If we select a column, the Statistics section shows more information about the column.</span></span> <span data-ttu-id="48fb5-236">Por ejemplo, la fila de tipo de característica muestra los tipos de datos que Azure Machine Learning Studio asignó a la columna.</span><span class="sxs-lookup"><span data-stu-id="48fb5-236">For example, the Feature Type row shows us what data types Azure Machine Learning Studio assigned to the column.</span></span> <span data-ttu-id="48fb5-237">Echar un vistazo rápido de este modo es una buena práctica de comprobación antes de empezar a realizar cualquier trabajo más importante.</span><span class="sxs-lookup"><span data-stu-id="48fb5-237">Having a quick look like this is a good sanity check before we start to do any serious work.</span></span>

### <a name="first-r-script"></a><span data-ttu-id="48fb5-238">Primer script de R</span><span class="sxs-lookup"><span data-stu-id="48fb5-238">First R script</span></span>
<span data-ttu-id="48fb5-239">A continuación, vamos a crear nuestro primer script de código R para experimentar con él en Estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="48fb5-239">Let's create a simple first R script to experiment with in Azure Machine Learning Studio.</span></span> <span data-ttu-id="48fb5-240">Para ello, he creado y probado el siguiente script en RStudio.</span><span class="sxs-lookup"><span data-stu-id="48fb5-240">I have created and tested the following script in RStudio.</span></span>  

    ## Only one of the following two lines should be used
    ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
    ## If in RStudio, use the second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="48fb5-241">Ahora necesito transferir este script a Estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="48fb5-241">Now I need to transfer this script to Azure Machine Learning Studio.</span></span> <span data-ttu-id="48fb5-242">Basta con cortar y pegar.</span><span class="sxs-lookup"><span data-stu-id="48fb5-242">I could simply cut and paste.</span></span> <span data-ttu-id="48fb5-243">Sin embargo, en este caso, transferiré el script de código R mediante un archivo zip.</span><span class="sxs-lookup"><span data-stu-id="48fb5-243">However, in this case, I will transfer my R script via a zip file.</span></span>

### <a name="data-input-to-the-execute-r-script-module"></a><span data-ttu-id="48fb5-244">Introducción de datos en el módulo de script de ejecución de código R</span><span class="sxs-lookup"><span data-stu-id="48fb5-244">Data input to the Execute R Script module</span></span>
<span data-ttu-id="48fb5-245">Echemos un vistazo a las entradas del módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-245">Let's have a look at the inputs to the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="48fb5-246">En este ejemplo se leerán los datos de productos lácteos de California en el módulo [Ejecutar script de R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-246">In this example we will read the California dairy data into the [Execute R Script][execute-r-script] module.</span></span>  

<span data-ttu-id="48fb5-247">Existen tres entradas posibles para el módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-247">There are three possible inputs for the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="48fb5-248">Puede usar cualquiera de estas entradas o todas ellas, dependiendo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48fb5-248">You may use any one or all of these inputs, depending on your application.</span></span> <span data-ttu-id="48fb5-249">También se puede utilizar un script de código R que no tome ninguna entrada.</span><span class="sxs-lookup"><span data-stu-id="48fb5-249">It is also perfectly reasonable to use an R script that takes no input at all.</span></span>  

<span data-ttu-id="48fb5-250">Echemos un vistazo a cada una de estas entradas de izquierda a derecha.</span><span class="sxs-lookup"><span data-stu-id="48fb5-250">Let's look at each of these inputs, going from left to right.</span></span> <span data-ttu-id="48fb5-251">Para ver los nombres de cada una de las entradas, coloque el cursor sobre la entrada y lea la información sobre herramientas.</span><span class="sxs-lookup"><span data-stu-id="48fb5-251">You can see the names of each of the inputs by placing your cursor over the input and reading the tooltip.</span></span>  

#### <a name="script-bundle"></a><span data-ttu-id="48fb5-252">Paquete de script</span><span class="sxs-lookup"><span data-stu-id="48fb5-252">Script Bundle</span></span>
<span data-ttu-id="48fb5-253">La entrada Paquete de script permite pasar el contenido de un archivo ZIP al módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-253">The Script Bundle input allows you to pass the contents of a zip file into [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="48fb5-254">Puede utilizar uno de los siguientes comandos para leer el contenido del archivo zip en su código R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-254">You can use one of the following commands to read the contents of the zip file into your R code.</span></span>

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> <span data-ttu-id="48fb5-255">Aprendizaje automático de Azure trata los archivos del archivo zip como si se encontrasen en el directorio src/, por lo que necesitará agregar el nombre del directorio como prefijo a los nombres de archivo.</span><span class="sxs-lookup"><span data-stu-id="48fb5-255">Azure Machine Learning treats files in the zip as if they are in the src/ directory, so you need to prefix your file names with this directory name.</span></span> <span data-ttu-id="48fb5-256">Por ejemplo, si el archivo zip contiene los archivos `yourfile.R` y `yourData.rdata` en la raíz del archivo zip, los tratará como `src/yourfile.R` y `src/yourData.rdata` al utilizar `source` y `load`.</span><span class="sxs-lookup"><span data-stu-id="48fb5-256">For example, if the zip contains the files `yourfile.R` and `yourData.rdata` in the root of the zip, you would address these as `src/yourfile.R` and `src/yourData.rdata` when using `source` and `load`.</span></span>
> 
> 

<span data-ttu-id="48fb5-257">Ya se ha explicado el proceso de carga de conjuntos de datos en [Carga del conjunto de datos](#loading).</span><span class="sxs-lookup"><span data-stu-id="48fb5-257">We already discussed loading datasets in [Loading the dataset](#loading).</span></span> <span data-ttu-id="48fb5-258">Una vez creado y probado el script de código R que se muestra en la sección anterior, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="48fb5-258">Once you have created and tested the R script shown in the previous section, do the following:</span></span>

1. <span data-ttu-id="48fb5-259">Guarde el script de código R en un archivo .R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-259">Save the R script into a .R file.</span></span> <span data-ttu-id="48fb5-260">Llamaré a mi archivo de script "simpleplot.R".</span><span class="sxs-lookup"><span data-stu-id="48fb5-260">I call my script file "simpleplot.R".</span></span> <span data-ttu-id="48fb5-261">Este es el contenido.</span><span class="sxs-lookup"><span data-stu-id="48fb5-261">Here's the contents.</span></span>
   
        ## Only one of the following two lines should be used
        ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
        ## If in RStudio, use the second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## The following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. <span data-ttu-id="48fb5-262">Cree un archivo zip y copie el script en el archivo zip.</span><span class="sxs-lookup"><span data-stu-id="48fb5-262">Create a zip file and copy your script into this zip file.</span></span> <span data-ttu-id="48fb5-263">En Windows, puede hacer clic con el botón derecho en el archivo, seleccionar **Enviar a** y luego **Carpeta comprimida**.</span><span class="sxs-lookup"><span data-stu-id="48fb5-263">On Windows, you can right-click on the file and select **Send to**, and then **Compressed folder**.</span></span> <span data-ttu-id="48fb5-264">Esto creará un nuevo archivo zip que contiene el archivo "simpleplot.R".</span><span class="sxs-lookup"><span data-stu-id="48fb5-264">This will create a new zip file containing the "simpleplot.R" file.</span></span>
3. <span data-ttu-id="48fb5-265">Agregue el archivo a los **conjuntos de datos** de Machine Learning Studio y especifique el tipo como **ZIP**.</span><span class="sxs-lookup"><span data-stu-id="48fb5-265">Add your file to the **datasets** in Machine Learning Studio, specifying the type as **zip**.</span></span> <span data-ttu-id="48fb5-266">Ahora debería ver el archivo zip en los conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-266">You should now see the zip file in your datasets.</span></span>
4. <span data-ttu-id="48fb5-267">Arrastre y suelte el archivo ZIP de los **conjuntos de datos** al **lienzo de ML Studio**.</span><span class="sxs-lookup"><span data-stu-id="48fb5-267">Drag and drop the zip file from **datasets** onto the **ML Studio canvas**.</span></span>
5. <span data-ttu-id="48fb5-268">Conecte la salida del icono de **datos del zip** a la entrada **Paquete de script** del módulo [Ejecutar código de R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-268">Connect the output of the **zip data** icon to the **Script Bundle** input of the [Execute R Script][execute-r-script] module.</span></span>
6. <span data-ttu-id="48fb5-269">Escriba la función `source()` con el nombre del archivo ZIP en la ventana de código del módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-269">Type the `source()` function with your zip file name into the code window for the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="48fb5-270">En mi caso escribí `source("src/simpleplot.R")`.</span><span class="sxs-lookup"><span data-stu-id="48fb5-270">In my case I typed `source("src/simpleplot.R")`.</span></span>  
7. <span data-ttu-id="48fb5-271">Asegúrese de hacer clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="48fb5-271">Make sure you click **Save**.</span></span>

<span data-ttu-id="48fb5-272">Una vez completados estos pasos, el módulo [Ejecutar script R][execute-r-script] ejecutará el script R en el archivo ZIP cuando se ejecute el experimento.</span><span class="sxs-lookup"><span data-stu-id="48fb5-272">Once these steps are complete, the [Execute R Script][execute-r-script] module will execute the R script in the zip file when the experiment is run.</span></span> <span data-ttu-id="48fb5-273">En este punto el experimento debería tener un aspecto similar al que se muestra en la ilustración 5.</span><span class="sxs-lookup"><span data-stu-id="48fb5-273">At this point your experiment should look something like Figure 5.</span></span>

![Experimento con el script de código R comprimido en un archivo zip][6]

<span data-ttu-id="48fb5-275">*Ilustración 5. Experimento con el script de código R comprimido en un archivo zip.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-275">*Figure 5. Experiment using zipped R script.*</span></span>

#### <a name="dataset1"></a><span data-ttu-id="48fb5-276">DataSet1</span><span class="sxs-lookup"><span data-stu-id="48fb5-276">Dataset1</span></span>
<span data-ttu-id="48fb5-277">Puede pasar una tabla de datos rectangular al código R mediante la entrada Dataset1.</span><span class="sxs-lookup"><span data-stu-id="48fb5-277">You can pass a rectangular table of data to your R code by using the Dataset1 input.</span></span> <span data-ttu-id="48fb5-278">En nuestro script sencillo, la función `maml.mapInputPort(1)` lee los datos del puerto 1.</span><span class="sxs-lookup"><span data-stu-id="48fb5-278">In our simple script the `maml.mapInputPort(1)` function reads the data from port 1.</span></span> <span data-ttu-id="48fb5-279">Estos datos se asignan a un nombre de variable de la trama de datos en el código.</span><span class="sxs-lookup"><span data-stu-id="48fb5-279">This data is then assigned to a dataframe variable name in your code.</span></span> <span data-ttu-id="48fb5-280">En nuestro script sencillo, la primera línea de código realiza la asignación.</span><span class="sxs-lookup"><span data-stu-id="48fb5-280">In our simple script the first line of code performs the assignment.</span></span>

    cadairydata <- maml.mapInputPort(1)

<span data-ttu-id="48fb5-281">Ejecute el experimento haciendo clic en el botón **Ejecutar** .</span><span class="sxs-lookup"><span data-stu-id="48fb5-281">Execute your experiment by clicking on the **Run** button.</span></span> <span data-ttu-id="48fb5-282">Cuando finalice la ejecución, haga clic en el módulo [Ejecutar script R][execute-r-script] y, luego, haga clic en **Ver registro de salida** en la página de propiedades.</span><span class="sxs-lookup"><span data-stu-id="48fb5-282">When the execution finishes, click on the [Execute R Script][execute-r-script] module and then click **View output log** on the properties pane.</span></span> <span data-ttu-id="48fb5-283">Debería aparecer una nueva página en el explorador que muestre el contenido del archivo output.log.</span><span class="sxs-lookup"><span data-stu-id="48fb5-283">A new page should appear in your browser showing the contents of the output.log file.</span></span> <span data-ttu-id="48fb5-284">Al desplazarse hacia abajo, debería ver algo similar a lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-284">When you scroll down you should see something like the following.</span></span>

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

<span data-ttu-id="48fb5-285">Más abajo en la página se especifica información más detallada sobre las columnas, con un aspecto similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-285">Farther down the page is more detailed information on the columns, which will look something like the following.</span></span>

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

<span data-ttu-id="48fb5-286">Estos resultados son los esperados e incluyen 228 observaciones y 9 columnas en el marco de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-286">These results are mostly as expected, with 228 observations and 9 columns in the dataframe.</span></span> <span data-ttu-id="48fb5-287">Pueden verse los nombres de columna, el tipo de datos de código R y un ejemplo de cada columna.</span><span class="sxs-lookup"><span data-stu-id="48fb5-287">We can see the column names, the R data type and a sample of each column.</span></span>

> [!NOTE]
> <span data-ttu-id="48fb5-288">Esta misma salida impresa está disponible desde el resultado del dispositivo R del módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-288">This same printed output is conveniently available from the R Device output of the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="48fb5-289">Abordaremos las salidas del módulo [Ejecutar script R][execute-r-script] en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-289">We will discuss the outputs of the [Execute R Script][execute-r-script] module in the next section.</span></span>  
> 
> 

#### <a name="dataset2"></a><span data-ttu-id="48fb5-290">Dataset2</span><span class="sxs-lookup"><span data-stu-id="48fb5-290">Dataset2</span></span>
<span data-ttu-id="48fb5-291">El comportamiento de la entrada Dataset2 es idéntico al de la entrada Dataset1.</span><span class="sxs-lookup"><span data-stu-id="48fb5-291">The behavior of the Dataset2 input is identical to that of Dataset1.</span></span> <span data-ttu-id="48fb5-292">Con esta entrada, se puede pasar una segunda tabla rectangular de datos al código R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-292">Using this input you can pass a second rectangular table of data into your R code.</span></span> <span data-ttu-id="48fb5-293">La función `maml.mapInputPort(2)`con el argumento 2, se utiliza para pasar estos datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-293">The function `maml.mapInputPort(2)`, with the argument 2, is used to pass this data.</span></span>  

### <a name="execute-r-script-outputs"></a><span data-ttu-id="48fb5-294">Ejecución de resultados de script de código R</span><span class="sxs-lookup"><span data-stu-id="48fb5-294">Execute R Script outputs</span></span>
#### <a name="output-a-dataframe"></a><span data-ttu-id="48fb5-295">Generación de tramas de datos</span><span class="sxs-lookup"><span data-stu-id="48fb5-295">Output a dataframe</span></span>
<span data-ttu-id="48fb5-296">Es posible generar el contenido de un marco de datos R como tabla rectangular a través del puerto Dataset1 de resultado mediante la función `maml.mapOutputPort()` .</span><span class="sxs-lookup"><span data-stu-id="48fb5-296">You can output the contents of an R dataframe as a rectangular table through the Result Dataset1 port by using the `maml.mapOutputPort()` function.</span></span> <span data-ttu-id="48fb5-297">En nuestro script de código R sencillo, esto se realiza con la siguiente línea.</span><span class="sxs-lookup"><span data-stu-id="48fb5-297">In our simple R script this is performed by the following line.</span></span>

    maml.mapOutputPort('cadairydata')

<span data-ttu-id="48fb5-298">Después de ejecutar el experimento, haga clic en el puerto de salida Dataset1 y, a continuación, haga clic en **Visualizar**.</span><span class="sxs-lookup"><span data-stu-id="48fb5-298">After running the experiment, click on the Result Dataset1 output port and then click on **Visualize**.</span></span> <span data-ttu-id="48fb5-299">Debería ver algo parecido a lo que se muestra en la ilustración 6.</span><span class="sxs-lookup"><span data-stu-id="48fb5-299">You should see something like Figure 6.</span></span>

![Visualización de la salida de los datos de productos lácteos de California][7]

<span data-ttu-id="48fb5-301">*Ilustración 6. Visualización de la salida de los datos de productos lácteos de California.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-301">*Figure 6. The visualization of the output of the California dairy data.*</span></span>

<span data-ttu-id="48fb5-302">Este resultado es idéntico a la entrada, justo como se esperaba.</span><span class="sxs-lookup"><span data-stu-id="48fb5-302">This output looks identical to the input, exactly as we expected.</span></span>  

### <a name="r-device-output"></a><span data-ttu-id="48fb5-303">Resultados del dispositivo R</span><span class="sxs-lookup"><span data-stu-id="48fb5-303">R Device output</span></span>
<span data-ttu-id="48fb5-304">La salida del dispositivo del módulo [Ejecutar script R][execute-r-script] contiene la salida de mensajes y gráficos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-304">The Device output of the [Execute R Script][execute-r-script] module contains messages and graphics output.</span></span> <span data-ttu-id="48fb5-305">Los mensajes de error y de resultados estándar de R se envían al puerto de salida del dispositivo R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-305">Both standard output and standard error messages from R are sent to the R Device output port.</span></span>  

<span data-ttu-id="48fb5-306">Para ver la salida del dispositivo R, haga clic en el puerto y, a continuación, en **Visualizar**.</span><span class="sxs-lookup"><span data-stu-id="48fb5-306">To view the R Device output, click on the port and then on **Visualize**.</span></span> <span data-ttu-id="48fb5-307">En la ilustración 7 puede verse el resultado estándar y el error estándar del script de código R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-307">We see the standard output and standard error from the R script in Figure 7.</span></span>

![Salida estándar y errores estándar desde el puerto del dispositivo R][8]

<span data-ttu-id="48fb5-309">*Ilustración 7. Salida estándar y errores estándar desde el puerto del dispositivo R.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-309">*Figure 7. Standard output and standard error from the R Device port.*</span></span>

<span data-ttu-id="48fb5-310">Si nos desplazamos hacia abajo, se puede ver el resultado de gráficos de nuestro script de código R en la ilustración 8.</span><span class="sxs-lookup"><span data-stu-id="48fb5-310">Scrolling down we see the graphics output from our R script in Figure 8.</span></span>  

![Salida gráfica desde el puerto de dispositivo R][9]

<span data-ttu-id="48fb5-312">*Ilustración 8. Salida gráfica desde el puerto de dispositivo R.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-312">*Figure 8. Graphics output from the R Device port.*</span></span>  

## <span data-ttu-id="48fb5-313"><a id="filtering"></a>Transformación y filtrado de datos</span><span class="sxs-lookup"><span data-stu-id="48fb5-313"><a id="filtering"></a>Data filtering and transformation</span></span>
<span data-ttu-id="48fb5-314">En esta sección se realizarán operaciones básicas de filtrado y transformación de datos de productos lácteos de California.</span><span class="sxs-lookup"><span data-stu-id="48fb5-314">In this section we will perform some basic data filtering and transformation operations on the California dairy data.</span></span> <span data-ttu-id="48fb5-315">Al final de esta sección, dispondrá de datos en formato adecuado para la creación de un modelo analítico.</span><span class="sxs-lookup"><span data-stu-id="48fb5-315">By the end of this section we will have data in a format suitable for building an analytic model.</span></span>  

<span data-ttu-id="48fb5-316">En esta sección se realizarán varias tareas de transformación y limpieza de datos comunes: transformación de tipos, filtrado de tramas de datos, adición de nuevas columnas de cálculo y transformaciones de valor.</span><span class="sxs-lookup"><span data-stu-id="48fb5-316">More specifically, in this section we will perform several common data cleaning and transformation tasks: type transformation, filtering on dataframes, adding new computed columns, and value transformations.</span></span> <span data-ttu-id="48fb5-317">Esta información general le ayudará a tratar con muchas de las variaciones que encontrará cuando se enfrente a problemas reales.</span><span class="sxs-lookup"><span data-stu-id="48fb5-317">This background should help you deal with the many variations encountered in real-world problems.</span></span>

<span data-ttu-id="48fb5-318">El código R completo de esta sección está disponible en el archivo zip descargado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-318">The complete R code for this section is available in the zip file you downloaded earlier.</span></span>

### <a name="type-transformations"></a><span data-ttu-id="48fb5-319">Transformaciones de tipo</span><span class="sxs-lookup"><span data-stu-id="48fb5-319">Type transformations</span></span>
<span data-ttu-id="48fb5-320">Ahora que podemos leer los datos de productos lácteos de California en código R en el módulo [Ejecutar script R][execute-r-script], es necesario asegurarse de que los datos de las columnas tienen el tipo y el formato deseados.</span><span class="sxs-lookup"><span data-stu-id="48fb5-320">Now that we can read the California dairy data into the R code in the [Execute R Script][execute-r-script] module, we need to ensure that the data in the columns has the intended type and format.</span></span>  

<span data-ttu-id="48fb5-321">R es un lenguaje con tipos dinámicos, lo que significa que los tipos de datos se convierten de un tipo a otro según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="48fb5-321">R is a dynamically typed language, which means that data types are coerced from one to another as required.</span></span> <span data-ttu-id="48fb5-322">Los tipos de datos atómicos en R incluyen caracteres, números y operaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="48fb5-322">The atomic data types in R include numeric, logical and character.</span></span> <span data-ttu-id="48fb5-323">El tipo de factor se utiliza para almacenar de manera compacta datos categóricos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-323">The factor type is used to compactly store categorical data.</span></span> <span data-ttu-id="48fb5-324">Encontrará mucha más información sobre los tipos de datos en las referencias en el [Apéndice B: lectura adicional](#appendixb).</span><span class="sxs-lookup"><span data-stu-id="48fb5-324">You can find much more information on data types in the references in [Appendix B - Further reading](#appendixb).</span></span>

<span data-ttu-id="48fb5-325">Cuando se lean datos tabulares en código R desde un origen externo, se recomienda comprobar siempre los tipos resultantes de las columnas.</span><span class="sxs-lookup"><span data-stu-id="48fb5-325">When tabular data is read into R from an external source, it is always a good idea to check the resulting types in the columns.</span></span> <span data-ttu-id="48fb5-326">Es posible que desee una columna de caracteres de tipo, pero en muchos casos esto se mostrará como factor o viceversa.</span><span class="sxs-lookup"><span data-stu-id="48fb5-326">You may want a column of type character, but in many cases this will show up as factor or vice versa.</span></span> <span data-ttu-id="48fb5-327">En otros casos, la columna que piensa que debe ser numérica se mostrará con datos de caracteres como, por ejemplo, '1,23' en lugar de 1,23 como número de punto flotante.</span><span class="sxs-lookup"><span data-stu-id="48fb5-327">In other cases a column you think should be numeric is represented by character data, e.g. '1.23' rather than 1.23 as a floating point number.</span></span>  

<span data-ttu-id="48fb5-328">Afortunadamente, es fácil realizar la conversión de un tipo a otro, siempre que sea posible la asignación.</span><span class="sxs-lookup"><span data-stu-id="48fb5-328">Fortunately, it is easy to convert one type to another, as long as mapping is possible.</span></span> <span data-ttu-id="48fb5-329">Por ejemplo, no se puede convertir 'Nevada' a un valor numérico, pero se puede convertir en un factor (variable de categoría).</span><span class="sxs-lookup"><span data-stu-id="48fb5-329">For example, you cannot convert 'Nevada' into a numeric value, but you can convert it to a factor (categorical variable).</span></span> <span data-ttu-id="48fb5-330">Como otro ejemplo, puede convertir el valor numérico 1 en un carácter '1' o en un factor.</span><span class="sxs-lookup"><span data-stu-id="48fb5-330">As another example, you can convert a numeric 1 into a character '1' or a factor.</span></span>  

<span data-ttu-id="48fb5-331">La sintaxis para cualquiera de estas conversiones es simple: `as.datatype()`.</span><span class="sxs-lookup"><span data-stu-id="48fb5-331">The syntax for any of these conversions is simple: `as.datatype()`.</span></span> <span data-ttu-id="48fb5-332">Estas funciones de conversión de tipos incluyen lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-332">These type conversion functions include the following.</span></span>

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

<span data-ttu-id="48fb5-333">Viendo los tipos de datos de las columnas introducidas en la sección anterior: todas las columnas son de tipo numérico, excepto la columna con la etiqueta 'Month', que es de carácter de tipo.</span><span class="sxs-lookup"><span data-stu-id="48fb5-333">Looking at the data types of the columns we input in the previous section: all columns are of type numeric, except for the column labeled 'Month', which is of type character.</span></span> <span data-ttu-id="48fb5-334">A continuación, vamos a convertirla en un factor y a probar los resultados.</span><span class="sxs-lookup"><span data-stu-id="48fb5-334">Let's convert this to a factor and test the results.</span></span>  

<span data-ttu-id="48fb5-335">He eliminado la línea que creaba la matriz de trazado de dispersión y he agregado una línea para convertir la columna 'Month' en un factor.</span><span class="sxs-lookup"><span data-stu-id="48fb5-335">I have deleted the line that created the scatterplot matrix and added a line converting the 'Month' column to a factor.</span></span> <span data-ttu-id="48fb5-336">En mi experimento solo cortaré y pegaré el código R en la ventana de código del módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-336">In my experiment I will just cut and paste the R code into the code window of the [Execute R Script][execute-r-script] Module.</span></span> <span data-ttu-id="48fb5-337">También puede actualizar el archivo zip y cargarlo en Estudio de aprendizaje automático de Azure; aunque esto implica varios pasos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-337">You could also update the zip file and upload it to Azure Machine Learning Studio, but this takes several steps.</span></span>  

    ## Only one of the following two lines should be used
    ## If running in Machine Learning Studio, use the first line with maml.mapInputPort()
    ## If in RStudio, use the second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure the coding is consistent and convert column to a factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check the result
    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

<span data-ttu-id="48fb5-338">Vamos a ejecutar este código y a examinar el registro de salida del script de R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-338">Let's execute this code and look at the output log for the R script.</span></span> <span data-ttu-id="48fb5-339">Los datos pertinentes del registro se muestran en la ilustración 9.</span><span class="sxs-lookup"><span data-stu-id="48fb5-339">The relevant data from the log is shown in Figure 9.</span></span>

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="48fb5-340">*Ilustración 9. Resumen del marco de datos con una variable de factor.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-340">*Figure 9. Summary of the dataframe with a factor variable.*</span></span>

<span data-ttu-id="48fb5-341">El tipo de Month debe ser ahora '**Factor con 14 niveles**'.</span><span class="sxs-lookup"><span data-stu-id="48fb5-341">The type for Month should now say '**Factor w/ 14 levels**'.</span></span> <span data-ttu-id="48fb5-342">Esto es un problema, puesto que un año solo tiene 12 meses.</span><span class="sxs-lookup"><span data-stu-id="48fb5-342">This is a problem since there are only 12 months in the year.</span></span> <span data-ttu-id="48fb5-343">También puede realizar comprobaciones para ver que el tipo de **Visualizar** del puerto Result Dataset (Conjunto de datos de resultados) es **Categorical**.</span><span class="sxs-lookup"><span data-stu-id="48fb5-343">You can also check to see that the type in **Visualize** of the Result Dataset port is '**Categorical**'.</span></span>

<span data-ttu-id="48fb5-344">El problema es que la columna 'Month' no se ha codificado de forma sistemática.</span><span class="sxs-lookup"><span data-stu-id="48fb5-344">The problem is that the 'Month' column has not been coded systematically.</span></span> <span data-ttu-id="48fb5-345">En algunos casos, un mes se denomina Abril y en otros se abrevia como Abr. Podemos resolver este problema recortando la cadena a 3 caracteres.</span><span class="sxs-lookup"><span data-stu-id="48fb5-345">In some cases a month is called April and in others it is abbreviated as Apr. We can solve this problem by trimming the string to 3 characters.</span></span> <span data-ttu-id="48fb5-346">La línea de código tendrá el aspecto siguiente:</span><span class="sxs-lookup"><span data-stu-id="48fb5-346">The line of code now looks like the following:</span></span>

    ## Ensure the coding is consistent and convert column to a factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

<span data-ttu-id="48fb5-347">Vuelva a ejecutar el experimento y vea el registro de salida.</span><span class="sxs-lookup"><span data-stu-id="48fb5-347">Rerun the experiment and view the output log.</span></span> <span data-ttu-id="48fb5-348">Los resultados esperados se muestran en la ilustración 10.</span><span class="sxs-lookup"><span data-stu-id="48fb5-348">The expected results are shown in Figure 10.</span></span>  

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="48fb5-349">*Ilustración 10. Resumen del marco de datos con el número correcto de niveles de factor.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-349">*Figure 10. Summary of the dataframe with correct number of factor levels.*</span></span>

<span data-ttu-id="48fb5-350">Nuestra variable factor tiene ahora los 12 niveles deseados.</span><span class="sxs-lookup"><span data-stu-id="48fb5-350">Our factor variable now has the desired 12 levels.</span></span>

### <a name="basic-data-frame-filtering"></a><span data-ttu-id="48fb5-351">Filtrado del marco de datos básico</span><span class="sxs-lookup"><span data-stu-id="48fb5-351">Basic data frame filtering</span></span>
<span data-ttu-id="48fb5-352">Las tramas de datos R incluyen capacidades de filtrado eficaces.</span><span class="sxs-lookup"><span data-stu-id="48fb5-352">R dataframes support powerful filtering capabilities.</span></span> <span data-ttu-id="48fb5-353">Es posible obtener subconjuntos de los conjuntos de datos mediante el uso de filtros lógicos en filas o columnas.</span><span class="sxs-lookup"><span data-stu-id="48fb5-353">Datasets can be subsetted by using logical filters on either rows or columns.</span></span> <span data-ttu-id="48fb5-354">En muchos casos, serán necesarios criterios de filtro complejos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-354">In many cases, complex filter criteria will be required.</span></span> <span data-ttu-id="48fb5-355">Las referencias de [Apéndice B: lectura adicional](#appendixb) contienen ejemplos extensos del filtrado de tramas de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-355">The references in [Appendix B - Further reading](#appendixb) contain extensive examples of filtering dataframes.</span></span>  

<span data-ttu-id="48fb5-356">En nuestro conjunto de datos, es necesario crear un bit de filtrado.</span><span class="sxs-lookup"><span data-stu-id="48fb5-356">There is one bit of filtering we should do on our dataset.</span></span> <span data-ttu-id="48fb5-357">Si observamos las columnas de la trama de datos cadairydata, podemos ver que hay dos columnas innecesarias.</span><span class="sxs-lookup"><span data-stu-id="48fb5-357">If you look at the columns in the cadairydata dataframe, you will see two unnecessary columns.</span></span> <span data-ttu-id="48fb5-358">La primera columna contiene solo un número de fila, que no es muy útil.</span><span class="sxs-lookup"><span data-stu-id="48fb5-358">The first column just holds a row number, which is not very useful.</span></span> <span data-ttu-id="48fb5-359">La segunda columna, Year.Month, contiene información redundante.</span><span class="sxs-lookup"><span data-stu-id="48fb5-359">The second column, Year.Month, contains redundant information.</span></span> <span data-ttu-id="48fb5-360">Estas dos columnas se pueden excluir fácilmente mediante el código R siguiente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-360">We can easily exclude these columns by using the following R code.</span></span>

> [!NOTE]
> <span data-ttu-id="48fb5-361">De ahora en adelante en esta sección, solo mostraré el código adicional que voy a agregar en el módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-361">From now on in this section, I will just show you the additional code I am adding in the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="48fb5-362">Voy a agregar cada nueva línea **antes** de la función `str()`.</span><span class="sxs-lookup"><span data-stu-id="48fb5-362">I will add each new line **before** the `str()` function.</span></span> <span data-ttu-id="48fb5-363">Esta función se utiliza para comprobar los resultados en Estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="48fb5-363">I use this function to verify my results in Azure Machine Learning Studio.</span></span>
> 
> 

<span data-ttu-id="48fb5-364">Voy a agregar la línea siguiente a mi código R en el módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-364">I add the following line to my R code in the [Execute R Script][execute-r-script] module.</span></span>

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

<span data-ttu-id="48fb5-365">Ejecute este código en su experimento y compruebe el resultado del registro de salida.</span><span class="sxs-lookup"><span data-stu-id="48fb5-365">Run this code in your experiment and check the result from the output log.</span></span> <span data-ttu-id="48fb5-366">Estos resultados se muestran en la ilustración 11.</span><span class="sxs-lookup"><span data-stu-id="48fb5-366">These results are shown in Figure 11.</span></span>

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="48fb5-367">*Ilustración 11. Resumen de la trama de datos con dos columnas quitadas.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-367">*Figure 11. Summary of the dataframe with two columns removed.*</span></span>

<span data-ttu-id="48fb5-368">¡Buenas noticias!</span><span class="sxs-lookup"><span data-stu-id="48fb5-368">Good news!</span></span> <span data-ttu-id="48fb5-369">Se obtienen los resultados esperados.</span><span class="sxs-lookup"><span data-stu-id="48fb5-369">We get the expected results.</span></span>

### <a name="add-a-new-column"></a><span data-ttu-id="48fb5-370">Adición de una columna nueva</span><span class="sxs-lookup"><span data-stu-id="48fb5-370">Add a new column</span></span>
<span data-ttu-id="48fb5-371">Para crear modelos de serie temporal será conveniente tener una columna que contenga los meses desde el inicio de la serie temporal.</span><span class="sxs-lookup"><span data-stu-id="48fb5-371">To create time series models it will be convenient to have a column containing the months since the start of the time series.</span></span> <span data-ttu-id="48fb5-372">Por ello, crearemos una nueva columna 'Month.Count'.</span><span class="sxs-lookup"><span data-stu-id="48fb5-372">We will create a new column 'Month.Count'.</span></span>

<span data-ttu-id="48fb5-373">Para facilitar la organización del código, crearemos la primera función simple, `num.month()`.</span><span class="sxs-lookup"><span data-stu-id="48fb5-373">To help organize the code we will create our first simple function, `num.month()`.</span></span> <span data-ttu-id="48fb5-374">A continuación, aplicaremos esta función para crear una nueva columna en la trama de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-374">We will then apply this function to create a new column in the dataframe.</span></span> <span data-ttu-id="48fb5-375">El nuevo código es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="48fb5-375">The new code is as follows.</span></span>

    ## Create a new column with the month count
    ## Function to find the number of months from the first
    ## month of the time series
    num.month <- function(Year, Month) {
      ## Find the starting year
      min.year  <- min(Year)

      ## Compute the number of months from the start of the time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute the new column for the dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

<span data-ttu-id="48fb5-376">Ahora ejecute el experimento actualizado y use el registro de salida para ver los resultados.</span><span class="sxs-lookup"><span data-stu-id="48fb5-376">Now run the updated experiment and use the output log to view the results.</span></span> <span data-ttu-id="48fb5-377">Estos resultados se muestran en la ilustración 12.</span><span class="sxs-lookup"><span data-stu-id="48fb5-377">These results are shown in Figure 12.</span></span>

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="48fb5-378">*Ilustración 12. Resumen de la trama de datos con la columna adicional.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-378">*Figure 12. Summary of the dataframe with the additional column.*</span></span>

<span data-ttu-id="48fb5-379">Parece que todo funciona correctamente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-379">It looks like everything is working.</span></span> <span data-ttu-id="48fb5-380">Tenemos la nueva columna con los valores esperados en nuestra trama de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-380">We have the new column with the expected values in our dataframe.</span></span>

### <a name="value-transformations"></a><span data-ttu-id="48fb5-381">Transformaciones de valor</span><span class="sxs-lookup"><span data-stu-id="48fb5-381">Value transformations</span></span>
<span data-ttu-id="48fb5-382">En esta sección se realizarán algunas transformaciones simples en los valores de algunas de las columnas de nuestra trama de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-382">In this section we will perform some simple transformations on the values in some of the columns of our dataframe.</span></span> <span data-ttu-id="48fb5-383">El lenguaje R admite las transformaciones de valores casi arbitrarias.</span><span class="sxs-lookup"><span data-stu-id="48fb5-383">The R language supports nearly arbitrary value transformations.</span></span> <span data-ttu-id="48fb5-384">Las referencias de [Apéndice B: lectura adicional](#appendixb) contienen ejemplos extensos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-384">The references in [Appendix B - Further Reading](#appendixb) contain extensive examples.</span></span>

<span data-ttu-id="48fb5-385">Si examinamos los valores de los resúmenes de nuestra trama de datos deberíamos ver algo extraño.</span><span class="sxs-lookup"><span data-stu-id="48fb5-385">If you look at the values in the summaries of our dataframe you should see something odd here.</span></span> <span data-ttu-id="48fb5-386">¿Se produce más de helado que leche en California?</span><span class="sxs-lookup"><span data-stu-id="48fb5-386">Is more ice cream than milk produced in California?</span></span> <span data-ttu-id="48fb5-387">Por supuesto que no. Esto no tiene sentido, por desgracia para los amantes del helado.</span><span class="sxs-lookup"><span data-stu-id="48fb5-387">No, of course not, as this makes no sense, sad as this fact may be to some of us ice cream lovers.</span></span> <span data-ttu-id="48fb5-388">Las unidades son diferentes.</span><span class="sxs-lookup"><span data-stu-id="48fb5-388">The units are different.</span></span> <span data-ttu-id="48fb5-389">El precio se especifica en unidades de libras, la leche se especifica en unidades de millones de libras y el helado en unidades de mil galones. Asimismo, el requesón se proporciona en unidades de miles de libras.</span><span class="sxs-lookup"><span data-stu-id="48fb5-389">The price is in units of US pounds, milk is in units of 1 M US pounds, ice cream is in units of 1,000 US gallons, and cottage cheese is in units of 1,000 US pounds.</span></span> <span data-ttu-id="48fb5-390">Suponiendo que el peso del helado sea de 6,5 libras por galón, podemos realizar fácilmente la multiplicación para convertir estos valores para que se expresen en las mismas unidades de miles de libras.</span><span class="sxs-lookup"><span data-stu-id="48fb5-390">Assuming ice cream weighs about 6.5 pounds per gallon, we can easily do the multiplication to convert these values so they are all in equal units of 1,000 pounds.</span></span>

<span data-ttu-id="48fb5-391">Para nuestro modelo de pronóstico, utilizaremos un modelo de multiplicación de tendencia y de ajuste de temporada de estos datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-391">For our forecasting model we use a multiplicative model for trend and seasonal adjustment of this data.</span></span> <span data-ttu-id="48fb5-392">Una transformación de registro permite usar un modelo lineal, lo que simplifica este proceso.</span><span class="sxs-lookup"><span data-stu-id="48fb5-392">A log transformation allows us to use a linear model, simplifying this process.</span></span> <span data-ttu-id="48fb5-393">Podemos aplicar la transformación de registro en la misma función en la que se aplica el multiplicador.</span><span class="sxs-lookup"><span data-stu-id="48fb5-393">We can apply the log transformation in the same function where the multiplier is applied.</span></span>

<span data-ttu-id="48fb5-394">En el código siguiente, voy a definir una nueva función, `log.transform()`, y la aplicaré a las filas que contienen los valores numéricos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-394">In the following code, I define a new function, `log.transform()`, and apply it to the rows containing the numerical values.</span></span> <span data-ttu-id="48fb5-395">La función R `Map()` se utiliza para aplicar la función `log.transform()` a las columnas seleccionadas de la trama de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-395">The R `Map()` function is used to apply the `log.transform()` function to the selected columns of the dataframe.</span></span> <span data-ttu-id="48fb5-396">`Map()` es similar a `apply()`, pero permite más de una lista de argumentos de la función.</span><span class="sxs-lookup"><span data-stu-id="48fb5-396">`Map()` is similar to `apply()` but allows for more than one list of arguments to the function.</span></span> <span data-ttu-id="48fb5-397">Tenga en cuenta que una lista de multiplicadores proporciona el segundo argumento de la función `log.transform()` .</span><span class="sxs-lookup"><span data-stu-id="48fb5-397">Note that a list of multipliers supplies the second argument to the `log.transform()` function.</span></span> <span data-ttu-id="48fb5-398">La función `na.omit()` se utiliza para realizar limpieza y garantizar que no haya valores no definidos o que falten en la trama de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-398">The `na.omit()` function is used as a bit of cleanup to ensure we do not have missing or undefined values in the dataframe.</span></span>

    log.transform <- function(invec, multiplier = 1) {
      ## Function for the transformation, which is the log
      ## of the input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments to function log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier to funcition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check the input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap the multiplication in tryCatch
      ## If there is an exception, print the warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply the transformation function to the 4 columns
    ## of the dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

<span data-ttu-id="48fb5-399">La función `log.transform()` realiza bastantes acciones.</span><span class="sxs-lookup"><span data-stu-id="48fb5-399">There is quite a bit happening in the `log.transform()` function.</span></span> <span data-ttu-id="48fb5-400">La mayor parte de este código comprueba si hay posibles problemas con los argumentos o aborda las excepciones que pueden producirse durante los cálculos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-400">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span></span> <span data-ttu-id="48fb5-401">En realidad, solo unas pocas líneas de este código realizan los cálculos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-401">Only a few lines of this code actually do the computations.</span></span>

<span data-ttu-id="48fb5-402">El objetivo de la programación defensiva es evitar que y¡un error en una función impida que el procesamiento continúe.</span><span class="sxs-lookup"><span data-stu-id="48fb5-402">The goal of the defensive programming is to prevent the failure of a single function that prevents processing from continuing.</span></span> <span data-ttu-id="48fb5-403">Un error repentino en un análisis cuya ejecución lleva mucho tiempo puede resultar muy frustrante para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="48fb5-403">An abrupt failure of a long-running analysis can be quite frustrating for users.</span></span> <span data-ttu-id="48fb5-404">Para evitar esta situación, se deben elegir valores devueltos predeterminados para limitar los daños en el procesamiento de nivel inferior.</span><span class="sxs-lookup"><span data-stu-id="48fb5-404">To avoid this situation, default return values must be chosen that will limit damage to downstream processing.</span></span> <span data-ttu-id="48fb5-405">También se genera un mensaje para avisar a los usuarios de que se ha producido un error.</span><span class="sxs-lookup"><span data-stu-id="48fb5-405">A message is also produced to alert users that something has gone wrong.</span></span>

<span data-ttu-id="48fb5-406">Si no está familiarizado con la programación defensiva en R, es posible que este código pueda parecerle complejo.</span><span class="sxs-lookup"><span data-stu-id="48fb5-406">If you are not used to defensive programming in R, all this code may seem a bit overwhelming.</span></span> <span data-ttu-id="48fb5-407">Por ello, lo guiaré a través de los pasos principales:</span><span class="sxs-lookup"><span data-stu-id="48fb5-407">I will walk you through the major steps:</span></span>

1. <span data-ttu-id="48fb5-408">Se define un vector de cuatro mensajes.</span><span class="sxs-lookup"><span data-stu-id="48fb5-408">A vector of four messages is defined.</span></span> <span data-ttu-id="48fb5-409">Estos mensajes se usan para comunicar información acerca de algunos de los posibles errores y excepciones que pueden producirse con este código.</span><span class="sxs-lookup"><span data-stu-id="48fb5-409">These messages are used to communicate information about some of the possible errors and exceptions that can occur with this code.</span></span>
2. <span data-ttu-id="48fb5-410">Devolveré un valor de NA para cada caso.</span><span class="sxs-lookup"><span data-stu-id="48fb5-410">I return a value of NA for each case.</span></span> <span data-ttu-id="48fb5-411">Hay muchas otras posibilidades que pueden tener menos efectos secundarios.</span><span class="sxs-lookup"><span data-stu-id="48fb5-411">There are many other possibilities that might have fewer side effects.</span></span> <span data-ttu-id="48fb5-412">Podría devolver un vector de ceros o el vector de entrada original, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="48fb5-412">I could return a vector of zeroes, or the original input vector, for example.</span></span>
3. <span data-ttu-id="48fb5-413">Las comprobaciones se ejecutan en los argumentos de la función.</span><span class="sxs-lookup"><span data-stu-id="48fb5-413">Checks are run on the arguments to the function.</span></span> <span data-ttu-id="48fb5-414">En cada caso, si se detecta un error, se devuelve un valor predeterminado y la función `warning()` produce un mensaje.</span><span class="sxs-lookup"><span data-stu-id="48fb5-414">In each case, if an error is detected, a default value is returned and a message is produced by the `warning()` function.</span></span> <span data-ttu-id="48fb5-415">Utilizaremos la función `warning()` en lugar de `stop()`, ya que esta finaliza la ejecución, que es justo lo que estamos tratando de evitar.</span><span class="sxs-lookup"><span data-stu-id="48fb5-415">I am using `warning()` rather than `stop()` as the latter will terminate execution, exactly what I am trying to avoid.</span></span> <span data-ttu-id="48fb5-416">He escrito este código en un estilo de procedimiento, ya que, en este caso, un enfoque funcional sería demasiado complejo.</span><span class="sxs-lookup"><span data-stu-id="48fb5-416">Note that I have written this code in a procedural style, as in this case a functional approach seemed complex and obscure.</span></span>
4. <span data-ttu-id="48fb5-417">Los cálculos de registros se encapsulan en `tryCatch()` para que las excepciones no detengan el procesamiento de forma abrupta.</span><span class="sxs-lookup"><span data-stu-id="48fb5-417">The log computations are wrapped in `tryCatch()` so that exceptions will not cause an abrupt halt to processing.</span></span> <span data-ttu-id="48fb5-418">Sin `tryCatch()` , la mayoría de los errores que generan las funciones de R dan como resultado una señal de detención, que hace justamente eso.</span><span class="sxs-lookup"><span data-stu-id="48fb5-418">Without `tryCatch()` most errors raised by R functions result in a stop signal, which does just that.</span></span>

<span data-ttu-id="48fb5-419">Ejecute este código R en el experimento y preste atención al resultado impreso en el archivo output.log.</span><span class="sxs-lookup"><span data-stu-id="48fb5-419">Execute this R code in your experiment and have a look at the printed output in the output.log file.</span></span> <span data-ttu-id="48fb5-420">Ahora verá los valores transformados de las cuatro columnas en el registro, tal como se muestra en la ilustración 13.</span><span class="sxs-lookup"><span data-stu-id="48fb5-420">You will now see the transformed values of the four columns in the log, as shown in Figure 13.</span></span>

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
    [ModuleOutput] [1] "Saving the following item(s):  .maml.oport1"

<span data-ttu-id="48fb5-421">*Ilustración 13. Resumen de los valores transformados en la trama de datos.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-421">*Figure 13. Summary of the transformed values in the dataframe.*</span></span>

<span data-ttu-id="48fb5-422">Como puede, observar, los valores se han transformado.</span><span class="sxs-lookup"><span data-stu-id="48fb5-422">We see the values have been transformed.</span></span> <span data-ttu-id="48fb5-423">La producción de leche ahora supera con creces la producción de otros productos lácteos, recordando que ahora estamos examinando una escala logarítmica.</span><span class="sxs-lookup"><span data-stu-id="48fb5-423">Milk production now greatly exceeds all other dairy product production, recalling that we are now looking at a log scale.</span></span>

<span data-ttu-id="48fb5-424">En este momento nuestros datos se limpian y estamos preparados el modelado.</span><span class="sxs-lookup"><span data-stu-id="48fb5-424">At this point our data is cleaned up and we are ready for some modeling.</span></span> <span data-ttu-id="48fb5-425">Según el resumen de visualización de la salida Conjunto de datos de resultado del módulo [Ejecutar script R][execute-r-script], verá que la columna "Month" es "Categorical" con 12 valores únicos, nuevamente tal como deseaba.</span><span class="sxs-lookup"><span data-stu-id="48fb5-425">Looking at the visualization summary for the Result Dataset output of our [Execute R Script][execute-r-script] module, you will see the 'Month' column is 'Categorical' with 12 unique values, again, just as we wanted.</span></span>

## <span data-ttu-id="48fb5-426"><a id="timeseries"></a>Análisis de correlación y objetos de series temporales</span><span class="sxs-lookup"><span data-stu-id="48fb5-426"><a id="timeseries"></a>Time series objects and correlation analysis</span></span>
<span data-ttu-id="48fb5-427">En esta sección se explorarán objetos básicos de series temporales R y se analizarán las correlaciones entre algunas de las variables.</span><span class="sxs-lookup"><span data-stu-id="48fb5-427">In this section we will explore a few basic R time series objects and analyze the correlations between some of the variables.</span></span> <span data-ttu-id="48fb5-428">Nuestro objetivo es producir una trama de datos que contiene la información de correlación en pares en varios intervalos de salida.</span><span class="sxs-lookup"><span data-stu-id="48fb5-428">Our goal is to output a dataframe containing the pairwise correlation information at several lags.</span></span>

<span data-ttu-id="48fb5-429">El código R completo de esta sección está disponible en el archivo zip descargado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-429">The complete R code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="time-series-objects-in-r"></a><span data-ttu-id="48fb5-430">Objetos de series de temporales de R</span><span class="sxs-lookup"><span data-stu-id="48fb5-430">Time series objects in R</span></span>
<span data-ttu-id="48fb5-431">Como ya se ha mencionado, las series temporales son series de valores de datos indexados por tiempo.</span><span class="sxs-lookup"><span data-stu-id="48fb5-431">As already mentioned, time series are a series of data values indexed by time.</span></span> <span data-ttu-id="48fb5-432">Los objetos de series temporales de R se utilizan para crear y administrar el índice de tiempo.</span><span class="sxs-lookup"><span data-stu-id="48fb5-432">R time series objects are used to create and manage the time index.</span></span> <span data-ttu-id="48fb5-433">La utilización de objetos de series temporales ofrece varias ventajas.</span><span class="sxs-lookup"><span data-stu-id="48fb5-433">There are several advantages to using time series objects.</span></span> <span data-ttu-id="48fb5-434">Los objetos de series temporales le liberan de los numerosos detalles de la administración de los valores de índice de series temporales que se encapsulan en el objeto.</span><span class="sxs-lookup"><span data-stu-id="48fb5-434">Time series objects free you from the many details of managing the time series index values that are encapsulated in the object.</span></span> <span data-ttu-id="48fb5-435">Además, los objetos de series temporales permiten utilizar los distintos métodos de la serie temporal para realizar tareas de trazado, impresión, modelado, etc.</span><span class="sxs-lookup"><span data-stu-id="48fb5-435">In addition, time series objects allow you to use the many time series methods for plotting, printing, modeling, etc.</span></span>

<span data-ttu-id="48fb5-436">La clase de serie temporal POSIXct es la que se utiliza con más frecuencia y es relativamente sencilla.</span><span class="sxs-lookup"><span data-stu-id="48fb5-436">The POSIXct time series class is commonly used and is relatively simple.</span></span> <span data-ttu-id="48fb5-437">Esta serie temporal mide el tiempo desde el inicio del periodo, el 1 de enero de 1970.</span><span class="sxs-lookup"><span data-stu-id="48fb5-437">This time series class measures time from the start of the epoch, January 1, 1970.</span></span> <span data-ttu-id="48fb5-438">En este ejemplo se utilizarán los objetos de serie temporal POSIXct.</span><span class="sxs-lookup"><span data-stu-id="48fb5-438">We will use POSIXct time series objects in this example.</span></span> <span data-ttu-id="48fb5-439">Otras clases de objeto de serie temporal R ampliamente utilizadas son las clases zoo y xts, así como las series temporales extensibles.</span><span class="sxs-lookup"><span data-stu-id="48fb5-439">Other widely used R time series object classes include zoo and xts, extensible time series.</span></span>
<!-- Additional information on R time series objects is provided in the references in Section 5.7. [commenting because this section doesn't exist, even in the original] -->

### <a name="time-series-object-example"></a><span data-ttu-id="48fb5-440">Ejemplo de objeto de serie temporal</span><span class="sxs-lookup"><span data-stu-id="48fb5-440">Time series object example</span></span>
<span data-ttu-id="48fb5-441">Comencemos con el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="48fb5-441">Let's get started with our example.</span></span> <span data-ttu-id="48fb5-442">Arrastre y suelte un **nuevo** módulo [Ejecutar script R][execute-r-script] en el experimento.</span><span class="sxs-lookup"><span data-stu-id="48fb5-442">Drag and drop a **new** [Execute R Script][execute-r-script] module into your experiment.</span></span> <span data-ttu-id="48fb5-443">Conecte el puerto de salida del conjunto de datos 1 de resultados del módulo [Ejecutar script R][execute-r-script] al puerto de entrada del conjunto de datos 1 del nuevo módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-443">Connect the Result Dataset1 output port of the existing [Execute R Script][execute-r-script] module to the Dataset1 input port of the new [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="48fb5-444">Como hicimos en los primeros ejemplos, a medida que progresamos en el ejemplo, solo mostraré en algunos puntos las líneas adicionales incrementales de código R en cada paso.</span><span class="sxs-lookup"><span data-stu-id="48fb5-444">As I did for the first examples, as we progress through the example, at some points I will show only the incremental additional lines of R code at each step.</span></span>  

#### <a name="reading-the-dataframe"></a><span data-ttu-id="48fb5-445">Lectura de la trama de datos</span><span class="sxs-lookup"><span data-stu-id="48fb5-445">Reading the dataframe</span></span>
<span data-ttu-id="48fb5-446">Como primer paso, vamos leer una trama de datos y nos aseguraremos de que se obtienen los resultados esperados.</span><span class="sxs-lookup"><span data-stu-id="48fb5-446">As a first step, let's read in a dataframe and make sure we get the expected results.</span></span> <span data-ttu-id="48fb5-447">El código siguiente debe funcionar.</span><span class="sxs-lookup"><span data-stu-id="48fb5-447">The following code should do the job.</span></span>

    # Comment the following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check the results

<span data-ttu-id="48fb5-448">Ahora, vamos a ejecutar el experimento.</span><span class="sxs-lookup"><span data-stu-id="48fb5-448">Now, run the experiment.</span></span> <span data-ttu-id="48fb5-449">El registro de la nueva forma de ejecutar script de R debería parecerse a la ilustración 14.</span><span class="sxs-lookup"><span data-stu-id="48fb5-449">The log of the new Execute R Script shape should look like Figure 14.</span></span>

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

<span data-ttu-id="48fb5-450">*Ilustración 14. Resumen de la trama de datos en el módulo Ejecutar script de R.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-450">*Figure 14. Summary of the dataframe in the Execute R Script module.*</span></span>

<span data-ttu-id="48fb5-451">Estos datos tienen el tipo y el formato esperados.</span><span class="sxs-lookup"><span data-stu-id="48fb5-451">This data is of the expected types and format.</span></span> <span data-ttu-id="48fb5-452">Tenga en cuenta que la columna 'Month' es de factor de tipo y tiene el número de niveles esperado.</span><span class="sxs-lookup"><span data-stu-id="48fb5-452">Note that the 'Month' column is of type factor and has the expected number of levels.</span></span>

#### <a name="creating-a-time-series-object"></a><span data-ttu-id="48fb5-453">Creación de un objeto de serie temporal</span><span class="sxs-lookup"><span data-stu-id="48fb5-453">Creating a time series object</span></span>
<span data-ttu-id="48fb5-454">Necesitamos agregar un objeto de serie temporal a nuestra trama de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-454">We need to add a time series object to our dataframe.</span></span> <span data-ttu-id="48fb5-455">Reemplace el código actual por el siguiente, que agrega una nueva columna de la clase POSIXct.</span><span class="sxs-lookup"><span data-stu-id="48fb5-455">Replace the current code with the following, which adds a new column of class POSIXct.</span></span>

    # Comment the following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check the results

<span data-ttu-id="48fb5-456">Ahora, compruebe el registro.</span><span class="sxs-lookup"><span data-stu-id="48fb5-456">Now, check the log.</span></span> <span data-ttu-id="48fb5-457">Debería ser similar al que se muestra en la ilustración 15.</span><span class="sxs-lookup"><span data-stu-id="48fb5-457">It should look like Figure 15.</span></span>

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

<span data-ttu-id="48fb5-458">*Ilustración 15. Resumen de la trama de datos con un objeto de serie temporal.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-458">*Figure 15. Summary of the dataframe with a time series object.*</span></span>

<span data-ttu-id="48fb5-459">Podemos ver en el resumen que la nueva columna es en realidad de la clase POSIXct.</span><span class="sxs-lookup"><span data-stu-id="48fb5-459">We can see from the summary that the new column is in fact of class POSIXct.</span></span>

### <a name="exploring-and-transforming-the-data"></a><span data-ttu-id="48fb5-460">Exploración y transformación de los datos</span><span class="sxs-lookup"><span data-stu-id="48fb5-460">Exploring and transforming the data</span></span>
<span data-ttu-id="48fb5-461">Exploremos algunas de las variables de este conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-461">Let's explore some of the variables in this dataset.</span></span> <span data-ttu-id="48fb5-462">Una matriz de trazado de dispersión es una buena manera de generar un vistazo rápido.</span><span class="sxs-lookup"><span data-stu-id="48fb5-462">A scatterplot matrix is a good way to produce a quick look.</span></span> <span data-ttu-id="48fb5-463">Voy a reemplazar la función `str()` del código R anterior por la siguiente línea.</span><span class="sxs-lookup"><span data-stu-id="48fb5-463">I am replacing the `str()` function in the previous R code with the following line.</span></span>

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

<span data-ttu-id="48fb5-464">Ejecute este código y observe qué sucede.</span><span class="sxs-lookup"><span data-stu-id="48fb5-464">Run this code and see what happens.</span></span> <span data-ttu-id="48fb5-465">El trazado producido en el puerto del dispositivo R debería parecerse al que se muestra en la ilustración 16.</span><span class="sxs-lookup"><span data-stu-id="48fb5-465">The plot produced at the R Device port should look like Figure 16.</span></span>

![Matriz de trazado de dispersión de las variables seleccionadas][17]

<span data-ttu-id="48fb5-467">*Ilustración 16. Matriz de trazado de dispersión de las variables seleccionadas.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-467">*Figure 16. Scatterplot matrix of selected variables.*</span></span>

<span data-ttu-id="48fb5-468">Como se puede observar, hay una estructura extraña en las relaciones entre estas variables.</span><span class="sxs-lookup"><span data-stu-id="48fb5-468">There is some odd-looking structure in the relationships between these variables.</span></span> <span data-ttu-id="48fb5-469">Quizás esto se debe a las tendencias en los datos y al hecho de que no hemos estandarizado las variables.</span><span class="sxs-lookup"><span data-stu-id="48fb5-469">Perhaps this arises from trends in the data and from the fact that we have not standardized the variables.</span></span>

### <a name="correlation-analysis"></a><span data-ttu-id="48fb5-470">Análisis de correlación</span><span class="sxs-lookup"><span data-stu-id="48fb5-470">Correlation analysis</span></span>
<span data-ttu-id="48fb5-471">Para realizar el análisis de correlación, necesitamos anular las tendencias y estandarizar las variables.</span><span class="sxs-lookup"><span data-stu-id="48fb5-471">To perform correlation analysis we need to both de-trend and standardize the variables.</span></span> <span data-ttu-id="48fb5-472">Para ello, basta con usar la función `scale()` de R que permite centrar y escalar las variables.</span><span class="sxs-lookup"><span data-stu-id="48fb5-472">We could simply use the R `scale()` function, which both centers and scales variables.</span></span> <span data-ttu-id="48fb5-473">Esta función también puede ejecutarse más rápido.</span><span class="sxs-lookup"><span data-stu-id="48fb5-473">This function might well run faster.</span></span> <span data-ttu-id="48fb5-474">Sin embargo, voy a mostrar un ejemplo de programación defensiva en R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-474">However, I want to show you an example of defensive programing in R.</span></span>

<span data-ttu-id="48fb5-475">La función `ts.detrend()` que se muestra a continuación realiza estas dos operaciones.</span><span class="sxs-lookup"><span data-stu-id="48fb5-475">The `ts.detrend()` function shown below performs both of these operations.</span></span> <span data-ttu-id="48fb5-476">Las siguientes dos líneas de código permiten anular las tendencias de datos y estandarizar los valores.</span><span class="sxs-lookup"><span data-stu-id="48fb5-476">The following two lines of code de-trend the data and then standardize the values.</span></span>

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function to de-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time to have the same length',
                    'ERROR: ts.detrend requires argument ts to be of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros to return as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # The input arguments are not of the same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If the ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If the ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that the Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend the time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply the detrend.ts function to the variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot the results to look at the relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

<span data-ttu-id="48fb5-477">La función `ts.detrend()` realiza bastantes acciones.</span><span class="sxs-lookup"><span data-stu-id="48fb5-477">There is quite a bit happening in the `ts.detrend()` function.</span></span> <span data-ttu-id="48fb5-478">La mayor parte de este código comprueba si hay posibles problemas con los argumentos o aborda las excepciones que pueden producirse durante los cálculos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-478">Most of this code is checking for potential problems with the arguments or dealing with exceptions, which can still arise during the computations.</span></span> <span data-ttu-id="48fb5-479">En realidad, solo unas pocas líneas de este código realizan los cálculos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-479">Only a few lines of this code actually do the computations.</span></span>

<span data-ttu-id="48fb5-480">Ya hemos analizado un ejemplo de programación defensiva en [Transformaciones de valor](#valuetransformations).</span><span class="sxs-lookup"><span data-stu-id="48fb5-480">We have already discussed an example of defensive programming in [Value transformations](#valuetransformations).</span></span> <span data-ttu-id="48fb5-481">Ambos bloques de cálculo se incluyen en `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="48fb5-481">Both computation blocks are wrapped in `tryCatch()`.</span></span> <span data-ttu-id="48fb5-482">Para algunos errores, es recomendable devolver el vector de entrada original, mientras que en otros casos es preferible devolver un vector de ceros.</span><span class="sxs-lookup"><span data-stu-id="48fb5-482">For some errors it makes sense to return the original input vector, and in other cases, I return a vector of zeros.</span></span>  

<span data-ttu-id="48fb5-483">Tenga en cuenta que la regresión lineal usada para anular las tendencias es una regresión de la serie temporal.</span><span class="sxs-lookup"><span data-stu-id="48fb5-483">Note that the linear regression used for de-trending is a time series regression.</span></span> <span data-ttu-id="48fb5-484">La variable de predicción es un objeto de la serie temporal.</span><span class="sxs-lookup"><span data-stu-id="48fb5-484">The predictor variable is a time series object.</span></span>  

<span data-ttu-id="48fb5-485">Una vez definida la función `ts.detrend()` , se aplica a las variables de interés en nuestra trama de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-485">Once `ts.detrend()` is defined we apply it to the variables of interest in our dataframe.</span></span> <span data-ttu-id="48fb5-486">Es necesario forzar la lista resultante creada con la función `lapply()` en los datos de la trama de datos mediante la función `as.data.frame()`.</span><span class="sxs-lookup"><span data-stu-id="48fb5-486">We must coerce the resulting list created by `lapply()` to data dataframe by using `as.data.frame()`.</span></span> <span data-ttu-id="48fb5-487">Debido a los aspectos defensivos de la función `ts.detrend()`, si no se procesa alguna de las variables, no se impedirá el correcto procesamiento de las demás.</span><span class="sxs-lookup"><span data-stu-id="48fb5-487">Because of defensive aspects of `ts.detrend()`, failure to process one of the variables will not prevent correct processing of the others.</span></span>  

<span data-ttu-id="48fb5-488">La última línea de código crea un trazado de dispersión en pares.</span><span class="sxs-lookup"><span data-stu-id="48fb5-488">The final line of code creates a pairwise scatterplot.</span></span> <span data-ttu-id="48fb5-489">Después de ejecutar el código R, se mostrarán los resultados del trazado de dispersión en la ilustración 17.</span><span class="sxs-lookup"><span data-stu-id="48fb5-489">After running the R code, the results of the scatterplot are shown in Figure 17.</span></span>

![Trazado de dispersión en pares de series temporales estandarizadas y con las tendencias anuladas][18]

<span data-ttu-id="48fb5-491">*Ilustración 17. Trazado de dispersión en pares de series temporales estandarizadas y con las tendencias anuladas.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-491">*Figure 17. Pairwise scatterplot of de-trended and standardized time series.*</span></span>

<span data-ttu-id="48fb5-492">Puede comparar estos resultados con los que se muestran en la ilustración 16.</span><span class="sxs-lookup"><span data-stu-id="48fb5-492">You can compare these results to those shown in Figure 16.</span></span> <span data-ttu-id="48fb5-493">Con la tendencia quitad y las variables estandarizadas, podemos ver que la estructura en las relaciones entre estas variables es menor.</span><span class="sxs-lookup"><span data-stu-id="48fb5-493">With the trend removed and the variables standardized, we see a lot less structure in the relationships between these variables.</span></span>

<span data-ttu-id="48fb5-494">El código necesario para calcular las correlaciones como objetos ccf R es el siguiente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-494">The code to compute the correlations as R ccf objects is as follows.</span></span>

    ## A function to compute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of the pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute the list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

<span data-ttu-id="48fb5-495">La ejecución de este código genera el registro mostrado en la ilustración 18.</span><span class="sxs-lookup"><span data-stu-id="48fb5-495">Running this code produces the log shown in Figure 18.</span></span>

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

<span data-ttu-id="48fb5-496">*Ilustración 18. Lista de objetos ccf del análisis de correlación en pares.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-496">*Figure 18. List of ccf objects from the pairwise correlation analysis.*</span></span>

<span data-ttu-id="48fb5-497">Hay un valor de correlación para cada intervalo.</span><span class="sxs-lookup"><span data-stu-id="48fb5-497">There is a correlation value for each lag.</span></span> <span data-ttu-id="48fb5-498">Ninguno de estos valores de correlación es lo suficientemente grande como para ser significativo.</span><span class="sxs-lookup"><span data-stu-id="48fb5-498">None of these correlation values is large enough to be significant.</span></span> <span data-ttu-id="48fb5-499">Por lo tanto, podemos concluir que podemos modelar cada variable de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-499">We can therefore conclude that we can model each variable independently.</span></span>

### <a name="output-a-dataframe"></a><span data-ttu-id="48fb5-500">Generación de tramas de datos</span><span class="sxs-lookup"><span data-stu-id="48fb5-500">Output a dataframe</span></span>
<span data-ttu-id="48fb5-501">Hemos calculado las correlaciones en pares como una lista de objetos ccf de R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-501">We have computed the pairwise correlations as a list of R ccf objects.</span></span> <span data-ttu-id="48fb5-502">Esto supone un problema, ya que el puerto de salida del conjunto de resultados resultante requiere una trama de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-502">This presents a bit of a problem as the Result Dataset output port really requires a dataframe.</span></span> <span data-ttu-id="48fb5-503">Además, el objeto ccf es en sí mismo una lista y solo necesitamos los valores del primer elemento de esta lista, es decir, las correlaciones de los distintos intervalos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-503">Further, the ccf object is itself a list and we want only the values in the first element of this list, the correlations at the various lags.</span></span>

<span data-ttu-id="48fb5-504">El código siguiente permite extraer los valores de los intervalos de la lista de objetos ccf, que son listas en sí mismos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-504">The following code extracts the lag values from the list of ccf objects, which are themselves lists.</span></span>

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with the row names column and the
    ## correlation data frame and assign the column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## The following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

<span data-ttu-id="48fb5-505">La primera línea de código puede parecer compleja, por lo que es posible que necesite algunas explicaciones para comprenderla.</span><span class="sxs-lookup"><span data-stu-id="48fb5-505">The first line of code is a bit tricky, and some explanation may help you understand it.</span></span> <span data-ttu-id="48fb5-506">Desde dentro hacia fuera, tenemos lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="48fb5-506">Working from the inside out we have the following:</span></span>

1. <span data-ttu-id="48fb5-507">El operador "**[[**" con el argumento "**1**" permite seleccionar el vector de correlaciones en los intervalos desde el primer elemento de la lista de objetos ccf.</span><span class="sxs-lookup"><span data-stu-id="48fb5-507">The '**[[**' operator with the argument '**1**' selects the vector of correlations at the lags from the first element of the ccf object list.</span></span>
2. <span data-ttu-id="48fb5-508">La función `do.call()` se aplica a la función `rbind()` sobre los elementos de las devoluciones de la lista mediante `lapply()`.</span><span class="sxs-lookup"><span data-stu-id="48fb5-508">The `do.call()` function applies the `rbind()` function over the elements of the list returns by `lapply()`.</span></span>
3. <span data-ttu-id="48fb5-509">La función `data.frame()` fuerza el resultado producido por `do.call()` en una trama de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-509">The `data.frame()` function coerces the result produced by `do.call()` to a dataframe.</span></span>

<span data-ttu-id="48fb5-510">Tenga en cuenta que los nombres de fila están en una columna de la trama de datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-510">Note that the row names are in a column of the dataframe.</span></span> <span data-ttu-id="48fb5-511">Esto permite conservar los nombres de fila cuando son la salida del módulo [Ejecutar script R][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="48fb5-511">Doing so preserves the row names when they are output from the [Execute R Script][execute-r-script].</span></span>

<span data-ttu-id="48fb5-512">La ejecución del código genera la salida que se muestra en la ilustración 19 cuando se usa **Visualizar** para la salida en el puerto del conjunto de datos de resultados.</span><span class="sxs-lookup"><span data-stu-id="48fb5-512">Running the code produces the output shown in Figure 19 when I **Visualize** the output at the Result Dataset port.</span></span> <span data-ttu-id="48fb5-513">Los nombres de fila están en la primera columna, según lo previsto.</span><span class="sxs-lookup"><span data-stu-id="48fb5-513">The row names are in the first column, as intended.</span></span>

![Resultados del análisis de correlación][20]

<span data-ttu-id="48fb5-515">*Ilustración 19. Resultados del análisis de correlación.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-515">*Figure 19. Results output from the correlation analysis.*</span></span>

## <span data-ttu-id="48fb5-516"><a id="seasonalforecasting"></a>Ejemplo de serie temporal: previsión estacional</span><span class="sxs-lookup"><span data-stu-id="48fb5-516"><a id="seasonalforecasting"></a>Time series example: seasonal forecasting</span></span>
<span data-ttu-id="48fb5-517">Nuestros datos están ahora en un formato adecuado para el análisis y hemos determinado que no hay correlaciones significativas entre las variables.</span><span class="sxs-lookup"><span data-stu-id="48fb5-517">Our data is now in a form suitable for analysis, and we have determined there are no significant correlations between the variables.</span></span> <span data-ttu-id="48fb5-518">Vamos a continuar y a crear un modelo de previsión de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="48fb5-518">Let's move on and create a time series forecasting model.</span></span> <span data-ttu-id="48fb5-519">Mediante este modelo, realizaremos una previsión de la producción de leche para California para los 12 meses de 2013.</span><span class="sxs-lookup"><span data-stu-id="48fb5-519">Using this model we will forecast California milk production for the 12 months of 2013.</span></span>

<span data-ttu-id="48fb5-520">Nuestro modelo de pronóstico tendrá dos componentes, un componente de tendencia y un componente de temporada.</span><span class="sxs-lookup"><span data-stu-id="48fb5-520">Our forecasting model will have two components, a trend component and a seasonal component.</span></span> <span data-ttu-id="48fb5-521">La previsión completa es el producto de estos dos componentes.</span><span class="sxs-lookup"><span data-stu-id="48fb5-521">The complete forecast is the product of these two components.</span></span> <span data-ttu-id="48fb5-522">Este tipo de modelo se conoce como un modelo de multiplicación.</span><span class="sxs-lookup"><span data-stu-id="48fb5-522">This type of model is known as a multiplicative model.</span></span> <span data-ttu-id="48fb5-523">La alternativa es un modelo de suma.</span><span class="sxs-lookup"><span data-stu-id="48fb5-523">The alternative is an additive model.</span></span> <span data-ttu-id="48fb5-524">Ya hemos aplicado una transformación de registro a las variables de interés, que hace que este análisis sea manejable.</span><span class="sxs-lookup"><span data-stu-id="48fb5-524">We have already applied a log transformation to the variables of interest, which makes this analysis tractable.</span></span>

<span data-ttu-id="48fb5-525">El código R completo de esta sección está disponible en el archivo zip descargado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-525">The complete R code for this section is in the zip file you downloaded earlier.</span></span>

### <a name="creating-the-dataframe-for-analysis"></a><span data-ttu-id="48fb5-526">Creación de la trama de datos para el análisis</span><span class="sxs-lookup"><span data-stu-id="48fb5-526">Creating the dataframe for analysis</span></span>
<span data-ttu-id="48fb5-527">Para empezar, agregue un **nuevo** módulo [Ejecutar script R][execute-r-script] al experimento.</span><span class="sxs-lookup"><span data-stu-id="48fb5-527">Start by adding a **new** [Execute R Script][execute-r-script] module to your experiment.</span></span> <span data-ttu-id="48fb5-528">Conecte la salida **Conjunto de datos de resultados** del módulo [Ejecutar script R][execute-r-script] existente a la entrada **Conjunto de datos 1** del módulo nuevo.</span><span class="sxs-lookup"><span data-stu-id="48fb5-528">Connect the **Result Dataset** output of the existing [Execute R Script][execute-r-script] module to the **Dataset1** input of the new module.</span></span> <span data-ttu-id="48fb5-529">El resultado debería ser similar al que se muestra en la ilustración 20.</span><span class="sxs-lookup"><span data-stu-id="48fb5-529">The result should look something like Figure 20.</span></span>

![Experimento con el nuevo módulo Ejecutar script de R agregado][21]

<span data-ttu-id="48fb5-531">*Ilustración 20. Experimento con el nuevo módulo Ejecutar script de R agregado.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-531">*Figure 20. The experiment with the new Execute R Script module added.*</span></span>

<span data-ttu-id="48fb5-532">Al igual que el análisis de correlación que acabamos de finalizar, tenemos que agregar una columna con un objeto de serie temporal POSIXct.</span><span class="sxs-lookup"><span data-stu-id="48fb5-532">As with the correlation analysis we just completed, we need to add a column with a POSIXct time series object.</span></span> <span data-ttu-id="48fb5-533">El código siguiente se encargará de realizar esta operación.</span><span class="sxs-lookup"><span data-stu-id="48fb5-533">The following code will do just this.</span></span>

    # If running in Machine Learning Studio, uncomment the first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

<span data-ttu-id="48fb5-534">Ejecute este código y examine el registro.</span><span class="sxs-lookup"><span data-stu-id="48fb5-534">Run this code and look at the log.</span></span> <span data-ttu-id="48fb5-535">El resultado deberá ser similar al que se muestra en la ilustración 21.</span><span class="sxs-lookup"><span data-stu-id="48fb5-535">The result should look like Figure 21.</span></span>

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

<span data-ttu-id="48fb5-536">*Ilustración 21. Resumen de la trama de datos.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-536">*Figure 21. A summary of the dataframe.*</span></span>

<span data-ttu-id="48fb5-537">Con este resultado, estamos preparados para iniciar nuestro análisis.</span><span class="sxs-lookup"><span data-stu-id="48fb5-537">With this result, we are ready to start our analysis.</span></span>

### <a name="create-a-training-dataset"></a><span data-ttu-id="48fb5-538">Creación de un conjunto de datos de entrenamiento</span><span class="sxs-lookup"><span data-stu-id="48fb5-538">Create a training dataset</span></span>
<span data-ttu-id="48fb5-539">Con la trama de datos construida, necesitamos crear un conjunto de datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="48fb5-539">With the dataframe constructed we need to create a training dataset.</span></span> <span data-ttu-id="48fb5-540">Estos datos incluirán todas las observaciones, excepto las últimas 12, que corresponden al año 2013 y que forman nuestro conjunto de datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="48fb5-540">This data will include all of the observations except the last 12, of the year 2013, which is our test dataset.</span></span> <span data-ttu-id="48fb5-541">El siguiente código crea subconjuntos de la trama de datos y gráficas de las variables de producción junto con las variables de precios.</span><span class="sxs-lookup"><span data-stu-id="48fb5-541">The following code subsets the dataframe and creates plots of the dairy production and price variables.</span></span> <span data-ttu-id="48fb5-542">A continuación, crearé gráficos de las cuatro producciones y de las variables de precios.</span><span class="sxs-lookup"><span data-stu-id="48fb5-542">I then create plots of the four production and price variables.</span></span> <span data-ttu-id="48fb5-543">Se utilizará una función anónima para definir algunos argumentos para el trazado y para, a continuación, iterar la lista de los otros dos argumentos con `Map()`.</span><span class="sxs-lookup"><span data-stu-id="48fb5-543">An anonymous function is used to define some augments for plot, and then iterate over the list of the other two arguments with `Map()`.</span></span> <span data-ttu-id="48fb5-544">Si piensa que un bucle for podría haber funcionado para esta operación, está en lo cierto.</span><span class="sxs-lookup"><span data-stu-id="48fb5-544">If you are thinking that a for loop would have worked fine here, you are correct.</span></span> <span data-ttu-id="48fb5-545">Sin embargo, puesto que R es un lenguaje funcional, he preferido ofrecer un enfoque funcional.</span><span class="sxs-lookup"><span data-stu-id="48fb5-545">But, since R is a functional language I am showing you a functional approach.</span></span>

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

<span data-ttu-id="48fb5-546">La ejecución del código genera series de gráficos temporales desde el resultado del dispositivo R que se muestra en la ilustración 22.</span><span class="sxs-lookup"><span data-stu-id="48fb5-546">Running the code produces the series of time series plots from the R Device output shown in Figure 22.</span></span> <span data-ttu-id="48fb5-547">Tenga en cuenta que el eje temporal se muestra en unidades de fechas. Esta es una de las ventajas del método de gráfico de series temporales.</span><span class="sxs-lookup"><span data-stu-id="48fb5-547">Note that the time axis is in units of dates, a nice benefit of the time series plot method.</span></span>

![Primero de los trazados de series temporales de la producción de productos lácteos de California y de los datos de precios](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Segundos de los trazados de series temporales de la producción de productos lácteos de California y de los datos de precios](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Tercero de los trazados de series temporales de la producción de productos lácteos de California y de los datos de precios](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Cuarto de los trazados de series temporales de la producción de productos lácteos de California y de los datos de precios](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

<span data-ttu-id="48fb5-552">*Ilustración 22. Trazados de series temporales de la producción de productos lácteos de California y de los datos de precios.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-552">*Figure 22. Time series plots of California dairy production and price data.*</span></span>

### <a name="a-trend-model"></a><span data-ttu-id="48fb5-553">Modelo de tendencia</span><span class="sxs-lookup"><span data-stu-id="48fb5-553">A trend model</span></span>
<span data-ttu-id="48fb5-554">Una vez creado el objeto de la serie temporal y tras haber analizado los datos, procederemos con la creación de un modelo de tendencias para los datos de producción de leche de California.</span><span class="sxs-lookup"><span data-stu-id="48fb5-554">Having created a time series object and having had a look at the data, let's start to construct a trend model for the California milk production data.</span></span> <span data-ttu-id="48fb5-555">Para ello, utilizaremos una regresión de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="48fb5-555">We can do this with a time series regression.</span></span> <span data-ttu-id="48fb5-556">Sin embargo, resulta evidente en el trazado, que necesitaremos algo más una pendiente y una intercepción para modelar con precisión la tendencia observada en los datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="48fb5-556">However, it is clear from the plot that we will need more than a slope and intercept to accurately model the observed trend in the training data.</span></span>

<span data-ttu-id="48fb5-557">Dada la pequeña escala de los datos, crearé el modelo de la tendencia en RStudio para, a continuación, cortar y pegar el modelo resultante en Aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="48fb5-557">Given the small scale of the data, I will build the model for trend in RStudio and then cut and paste the resulting model into Azure Machine Learning.</span></span> <span data-ttu-id="48fb5-558">RStudio proporciona un entorno interactivo para este tipo de análisis interactivo.</span><span class="sxs-lookup"><span data-stu-id="48fb5-558">RStudio provides an interactive environment for this type of interactive analysis.</span></span>

<span data-ttu-id="48fb5-559">Como primer intento, probaré con una regresión polinómica con potencia de hasta 3.</span><span class="sxs-lookup"><span data-stu-id="48fb5-559">As a first attempt, I will try a polynomial regression with powers up to 3.</span></span> <span data-ttu-id="48fb5-560">Existe un claro riesgo de sobreajuste con estos modelos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-560">There is a real danger of over-fitting these kinds of models.</span></span> <span data-ttu-id="48fb5-561">Por lo tanto, es mejor evitar los términos de alto nivel.</span><span class="sxs-lookup"><span data-stu-id="48fb5-561">Therefore, it is best to avoid high order terms.</span></span> <span data-ttu-id="48fb5-562">La función `I()` impide la interpretación del contenido (interpreta el contenido "tal cual") y permite escribir una función interpretada de manera literal en una ecuación de regresión.</span><span class="sxs-lookup"><span data-stu-id="48fb5-562">The `I()` function inhibits interpretation of the contents (interprets the contents 'as is') and allows you to write a literally interpreted function in a regression equation.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

<span data-ttu-id="48fb5-563">Esto genera lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-563">This generates the following.</span></span>

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

<span data-ttu-id="48fb5-564">A partir de los valores de P (Pr(>|t|)) obtenidos en este resultado, podemos ver que el término al cuadrado puede que no sea significativo.</span><span class="sxs-lookup"><span data-stu-id="48fb5-564">From P values (Pr(>|t|)) in this output, we can see that the squared term may not be significant.</span></span> <span data-ttu-id="48fb5-565">Voy a utilizar la función `update()` para modificar este modelo quitando el término al cuadrado.</span><span class="sxs-lookup"><span data-stu-id="48fb5-565">I will use the `update()` function to modify this model by dropping the squared term.</span></span>

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

<span data-ttu-id="48fb5-566">Esto genera lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-566">This generates the following.</span></span>

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

<span data-ttu-id="48fb5-567">Mucho mejor ahora.</span><span class="sxs-lookup"><span data-stu-id="48fb5-567">This looks better.</span></span> <span data-ttu-id="48fb5-568">Todos los términos son significativos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-568">All of the terms are significant.</span></span> <span data-ttu-id="48fb5-569">Sin embargo, el valor 2e-16 es un valor predeterminado y no debe tomarse muy en serio.</span><span class="sxs-lookup"><span data-stu-id="48fb5-569">However, the 2e-16 value is a default value, and should not be taken too seriously.</span></span>  

<span data-ttu-id="48fb5-570">Como prueba de validez, vamos a crear un gráfico de serie temporal de los datos de producción de productos lácteos de California con la curva de tendencias.</span><span class="sxs-lookup"><span data-stu-id="48fb5-570">As a sanity test, let's make a time series plot of the California dairy production data with the trend curve shown.</span></span> <span data-ttu-id="48fb5-571">Agregué el código siguiente en el modelo [Ejecutar script R][execute-r-script] (no RStudio) de Azure Machine Learning para crear el modelo y hacer un gráfico.</span><span class="sxs-lookup"><span data-stu-id="48fb5-571">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] model (not RStudio) to create the model and make a plot.</span></span> <span data-ttu-id="48fb5-572">El resultado aparece en la ilustración 23.</span><span class="sxs-lookup"><span data-stu-id="48fb5-572">The result is shown in Figure 23.</span></span>

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![Datos de producción de leche de California con modelo de tendencias](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

<span data-ttu-id="48fb5-574">*Ilustración 23. Datos de producción de leche de California con modelo de tendencias.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-574">*Figure 23. California milk production data with trend model shown.*</span></span>

<span data-ttu-id="48fb5-575">Parece que el modelo de tendencias se ajusta bastante bien a los datos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-575">It looks like the trend model fits the data fairly well.</span></span> <span data-ttu-id="48fb5-576">Además, no parece que haya signos de sobreajuste como, por ejemplo formas extrañas en la curva de modelo.</span><span class="sxs-lookup"><span data-stu-id="48fb5-576">Further, there does not seem to be evidence of over-fitting, such as odd wiggles in the model curve.</span></span>  

### <a name="seasonal-model"></a><span data-ttu-id="48fb5-577">Modelo de temporada</span><span class="sxs-lookup"><span data-stu-id="48fb5-577">Seasonal model</span></span>
<span data-ttu-id="48fb5-578">Con un modelo de tendencias en mano, necesitamos ir más allá e incluir los efectos estacionales.</span><span class="sxs-lookup"><span data-stu-id="48fb5-578">With a trend model in hand, we need to push on and include the seasonal effects.</span></span> <span data-ttu-id="48fb5-579">Usaremos el mes del año como una variable ficticia en el modelo lineal para capturar el efecto de cada mes.</span><span class="sxs-lookup"><span data-stu-id="48fb5-579">We will use the month of the year as a dummy variable in the linear model to capture the month-by-month effect.</span></span> <span data-ttu-id="48fb5-580">Tenga en cuenta que al introducir variables factor en un modelo, la intercepción no se debe calcular.</span><span class="sxs-lookup"><span data-stu-id="48fb5-580">Note that when you introduce factor variables into a model, the intercept must not be computed.</span></span> <span data-ttu-id="48fb5-581">Si no lo hace, la fórmula tendrá un exceso de especificación y R quitará uno de los factores deseados pero conservará el término de intercepción.</span><span class="sxs-lookup"><span data-stu-id="48fb5-581">If you do not do this, the formula is over-specified and R will drop one of the desired factors but keep the intercept term.</span></span>

<span data-ttu-id="48fb5-582">Puesto que tenemos un modelo de tendencias satisfactorio, podemos utilizar la función `update()` para agregar los nuevos términos al modelo existente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-582">Since we have a satisfactory trend model we can use the `update()` function to add the new terms to the existing model.</span></span> <span data-ttu-id="48fb5-583">El valor -1 en la fórmula de actualización quita el término de intercepción.</span><span class="sxs-lookup"><span data-stu-id="48fb5-583">The -1 in the update formula drops the intercept term.</span></span> <span data-ttu-id="48fb5-584">Si continuamos en RStudio:</span><span class="sxs-lookup"><span data-stu-id="48fb5-584">Continuing in RStudio for the moment:</span></span>

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

<span data-ttu-id="48fb5-585">Esto genera lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="48fb5-585">This generates the following.</span></span>

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

<span data-ttu-id="48fb5-586">Vemos que el modelo ya no tiene ningún término de intercepción y que cuenta con 12 factores de mes.</span><span class="sxs-lookup"><span data-stu-id="48fb5-586">We see that the model no longer has an intercept term and has 12 significant month factors.</span></span> <span data-ttu-id="48fb5-587">Esto es exactamente lo que queríamos ver.</span><span class="sxs-lookup"><span data-stu-id="48fb5-587">This is exactly what we wanted to see.</span></span>

<span data-ttu-id="48fb5-588">A continuación, crearemos otro gráfico de serie temporal con los datos de producción de productos lácteos de California para ver cómo funciona el modelo de temporada.</span><span class="sxs-lookup"><span data-stu-id="48fb5-588">Let's make another time series plot of the California dairy production data to see how well the seasonal model is working.</span></span> <span data-ttu-id="48fb5-589">Agregué el código siguiente en el módulo [Ejecutar script R][execute-r-script] de Azure Machine Learning para crear el modelo y hacer un gráfico.</span><span class="sxs-lookup"><span data-stu-id="48fb5-589">I have added the following code in the Azure Machine Learning [Execute R Script][execute-r-script] to create the model and make a plot.</span></span>

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

<span data-ttu-id="48fb5-590">La ejecución de este código en Aprendizaje automático de Azure genera el gráfico que se muestra en la ilustración 24.</span><span class="sxs-lookup"><span data-stu-id="48fb5-590">Running this code in Azure Machine Learning produces the plot shown in Figure 24.</span></span>

![Producción de leche de California con modelo que incluye los efectos de temporada](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

<span data-ttu-id="48fb5-592">*Ilustración 24. Producción de leche de California con modelo que incluye los efectos de temporada.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-592">*Figure 24. California milk production with model including seasonal effects.*</span></span>

<span data-ttu-id="48fb5-593">El ajuste a los datos que se muestran en la ilustración 24 es bastante alentador.</span><span class="sxs-lookup"><span data-stu-id="48fb5-593">The fit to the data shown in Figure 24 is rather encouraging.</span></span> <span data-ttu-id="48fb5-594">Tanto la tendencia como el efecto estacional (variación mensual) parecen ser razonables.</span><span class="sxs-lookup"><span data-stu-id="48fb5-594">Both the trend and the seasonal effect (monthly variation) look reasonable.</span></span>

<span data-ttu-id="48fb5-595">Con el fin de realizar una comprobación adicional en nuestro modelo, veamos los valores residuales.</span><span class="sxs-lookup"><span data-stu-id="48fb5-595">As another check on our model, let's have a look at the residuals.</span></span> <span data-ttu-id="48fb5-596">El código siguiente calcula los valores de predicción de los dos modelos, calcula los valores residuales para el modelo de temporada y, a continuación, crea un trazado de estos valores residuales para los datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="48fb5-596">The following code computes the predicted values from our two models, computes the residuals for the seasonal model, and then plots these residuals for the training data.</span></span>

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot the residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

<span data-ttu-id="48fb5-597">El gráfico de valores residuales se muestra en la ilustración 25.</span><span class="sxs-lookup"><span data-stu-id="48fb5-597">The residual plot is shown in Figure 25.</span></span>

![Valores residuales del modelo estacional para los datos de entrenamiento](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

<span data-ttu-id="48fb5-599">*Ilustración 25. Valores residuales del modelo estacional para los datos de entrenamiento.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-599">*Figure 25. Residuals of the seasonal model for the training data.*</span></span>

<span data-ttu-id="48fb5-600">Estos valores residuales parecen ser razonables.</span><span class="sxs-lookup"><span data-stu-id="48fb5-600">These residuals look reasonable.</span></span> <span data-ttu-id="48fb5-601">No hay ninguna estructura determinada, excepto el efecto de la recesión de 2008 y 2009 que nuestro modelo no tiene especialmente en cuenta.</span><span class="sxs-lookup"><span data-stu-id="48fb5-601">There is no particular structure, except the effect of the 2008-2009 recession, which our model does not account for particularly well.</span></span>

<span data-ttu-id="48fb5-602">El gráfico que se muestra en la ilustración 25 es útil para detectar los patrones que dependen del tiempo en los valores residuales.</span><span class="sxs-lookup"><span data-stu-id="48fb5-602">The plot shown in Figure 25 is useful for detecting any time-dependent patterns in the residuals.</span></span> <span data-ttu-id="48fb5-603">El enfoque explícito de cálculo y gráficos de los valores residuales que he utilizado coloca los valores residuales por orden cronológico en el gráfico.</span><span class="sxs-lookup"><span data-stu-id="48fb5-603">The explicit approach of computing and plotting the residuals I used places the residuals in time order on the plot.</span></span> <span data-ttu-id="48fb5-604">Por otro lado, si hubiese creado el trazado con la  `milk.lm$residuals`, este no estaría ordenado de forma cronológica.</span><span class="sxs-lookup"><span data-stu-id="48fb5-604">If, on the other hand, I had plotted `milk.lm$residuals`, the plot would not have been in time order.</span></span>

<span data-ttu-id="48fb5-605">También puede usar la función `plot.lm()` para generar una serie de trazados de diagnóstico:</span><span class="sxs-lookup"><span data-stu-id="48fb5-605">You can also use `plot.lm()` to produce a series of diagnostic plots.</span></span>

    ## Show the diagnostic plots for the model
    plot(milk.lm2, ask = FALSE)

<span data-ttu-id="48fb5-606">Este código genera una serie de trazados de diagnósticos que se muestran en la ilustración 26.</span><span class="sxs-lookup"><span data-stu-id="48fb5-606">This code produces a series of diagnostic plots shown in Figure 26.</span></span>

![Primero de los trazados de diagnóstico para el modelo estacional](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Segundo de los trazados de diagnóstico para el modelo estacional](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Tercero de los trazados de diagnóstico para el modelo estacional](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Cuarto de los trazados de diagnóstico para el modelo estacional](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

<span data-ttu-id="48fb5-611">*Ilustración 26. Trazados de diagnóstico para el modelo estacional.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-611">*Figure 26. Diagnostic plots for the seasonal model.*</span></span>

<span data-ttu-id="48fb5-612">Existen varios puntos influyentes identificados en estos gráficos, pero nada por lo que debamos preocuparnos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-612">There are a few highly influential points identified in these plots, but nothing to cause great concern.</span></span> <span data-ttu-id="48fb5-613">Además, podemos ver en el gráfico Normal Q-Q que los valores residuales son próximos a los de distribución normal, una suposición importante para los modelos lineales.</span><span class="sxs-lookup"><span data-stu-id="48fb5-613">Further, we can see from the Normal Q-Q plot that the residuals are close to normally distributed, an important assumption for linear models.</span></span>

### <a name="forecasting-and-model-evaluation"></a><span data-ttu-id="48fb5-614">Evaluación del modelo y predicción</span><span class="sxs-lookup"><span data-stu-id="48fb5-614">Forecasting and model evaluation</span></span>
<span data-ttu-id="48fb5-615">Hay solo una cosa más que nos falta por hacer para completar nuestro ejemplo.</span><span class="sxs-lookup"><span data-stu-id="48fb5-615">There is just one more thing to do to complete our example.</span></span> <span data-ttu-id="48fb5-616">Tenemos que calcular las previsiones y evaluar el error con respecto a los datos reales.</span><span class="sxs-lookup"><span data-stu-id="48fb5-616">We need to compute forecasts and measure the error against the actual data.</span></span> <span data-ttu-id="48fb5-617">Nuestra previsión será para los 12 meses de 2013.</span><span class="sxs-lookup"><span data-stu-id="48fb5-617">Our forecast will be for the 12 months of 2013.</span></span> <span data-ttu-id="48fb5-618">Podemos calcular una evaluación de error para esta previsión de los datos reales que no forman parte de nuestro conjunto de datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="48fb5-618">We can compute an error measure for this forecast to the actual data that is not part of our training dataset.</span></span> <span data-ttu-id="48fb5-619">Además, podemos comparar el rendimiento de los 18 años de datos de entrenamiento con los 12 meses de los datos de prueba.</span><span class="sxs-lookup"><span data-stu-id="48fb5-619">Additionally, we can compare performance on the 18 years of training data to the 12 months of test data.</span></span>  

<span data-ttu-id="48fb5-620">Se utiliza una gran cantidad de métricas para medir el rendimiento de los modelos de serie temporal.</span><span class="sxs-lookup"><span data-stu-id="48fb5-620">A number of metrics are used to measure the performance of time series models.</span></span> <span data-ttu-id="48fb5-621">En nuestro caso, usaremos el error cuadrático medio (RMS).</span><span class="sxs-lookup"><span data-stu-id="48fb5-621">In our case we will use the root mean square (RMS) error.</span></span> <span data-ttu-id="48fb5-622">La función siguiente calcula el error RMS entre dos series.</span><span class="sxs-lookup"><span data-stu-id="48fb5-622">The following function computes the RMS error between two series.</span></span>  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function to compute the RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments to function RMS.error of wrong type encountered",
                    "ERROR: Input vector to function RMS.error is too short",
                    "ERROR: Input vectors to function RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check the arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate the values, else just copy
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

    ## Compute the RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

<span data-ttu-id="48fb5-623">Como ocurre con la función `log.transform()` explicada en la sección "Transformaciones de valor", en esta función hay una gran cantidad de código de recuperación de excepciones y de comprobación de errores.</span><span class="sxs-lookup"><span data-stu-id="48fb5-623">As with the `log.transform()` function we discussed in the "Value transformations" section, there is quite a lot of error checking and exception recovery code in this function.</span></span> <span data-ttu-id="48fb5-624">Los principios empleados son los mismos.</span><span class="sxs-lookup"><span data-stu-id="48fb5-624">The principles employed are the same.</span></span> <span data-ttu-id="48fb5-625">El trabajo se realiza en dos puntos en la función `tryCatch()`.</span><span class="sxs-lookup"><span data-stu-id="48fb5-625">The work is done in two places wrapped in `tryCatch()`.</span></span> <span data-ttu-id="48fb5-626">En primer lugar, se potencia la serie temporal, ya que hemos estado trabajando con los registros de los valores.</span><span class="sxs-lookup"><span data-stu-id="48fb5-626">First, the time series are exponentiated, since we have been working with the logs of the values.</span></span> <span data-ttu-id="48fb5-627">En segundo lugar, se calcula el error RMS real.</span><span class="sxs-lookup"><span data-stu-id="48fb5-627">Second, the actual RMS error is computed.</span></span>  

<span data-ttu-id="48fb5-628">Equipados con una función para medir el error RMS, vamos a compilar y a crear una trama de datos que contenga los errores RMS.</span><span class="sxs-lookup"><span data-stu-id="48fb5-628">Equipped with a function to measure the RMS error, let's build and output a dataframe containing the RMS errors.</span></span> <span data-ttu-id="48fb5-629">Incluiremos términos para el modelo de tendencias únicamente y para el modelo completo con factores de temporada.</span><span class="sxs-lookup"><span data-stu-id="48fb5-629">We will include terms for the trend model alone and the complete model with seasonal factors.</span></span> <span data-ttu-id="48fb5-630">El siguiente código realiza el trabajo con los dos modelos lineales que hemos creado.</span><span class="sxs-lookup"><span data-stu-id="48fb5-630">The following code does the job by using the two linear models we have constructed.</span></span>

    ## Compute the RMS error in a dataframe
    ## Include the row names in the first column so they will
    ## appear in the output of the Execute R Script
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

    ## The following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

<span data-ttu-id="48fb5-631">La ejecución de este código genera el resultado que se muestra en la ilustración 27 en el puerto de salida del conjunto de datos de resultado.</span><span class="sxs-lookup"><span data-stu-id="48fb5-631">Running this code produces the output shown in Figure 27 at the Result Dataset output port.</span></span>

![Comparación de errores RMS para los modelos][26]

<span data-ttu-id="48fb5-633">*Ilustración 27. Comparación de errores RMS para los modelos.*</span><span class="sxs-lookup"><span data-stu-id="48fb5-633">*Figure 27. Comparison of RMS errors for the models.*</span></span>

<span data-ttu-id="48fb5-634">Según estos resultados, podemos ver que el hecho de agregar factores estacionales al modelo reduce significativamente el error RMS.</span><span class="sxs-lookup"><span data-stu-id="48fb5-634">From these results, we see that adding the seasonal factors to the model reduces the RMS error significantly.</span></span> <span data-ttu-id="48fb5-635">No es sorprendente que el error RMS de los datos de entrenamiento sea menor que el del pronóstico.</span><span class="sxs-lookup"><span data-stu-id="48fb5-635">Not too surprisingly, the RMS error for the training data is a bit less than for the forecast.</span></span>

## <span data-ttu-id="48fb5-636"><a id="appendixa"></a>APÉNDICE A: guía de RStudio</span><span class="sxs-lookup"><span data-stu-id="48fb5-636"><a id="appendixa"></a>APPENDIX A: Guide to RStudio</span></span>
<span data-ttu-id="48fb5-637">RStudio cuenta con una documentación bastante extensa, por lo que en este apéndice me limitaré a proporcionar vínculos a secciones claves de la documentación de RStudio.</span><span class="sxs-lookup"><span data-stu-id="48fb5-637">RStudio is quite well documented, so in this appendix I will provide some links to the key sections of the RStudio documentation to get you started.</span></span>

1. <span data-ttu-id="48fb5-638">Creación de proyectos</span><span class="sxs-lookup"><span data-stu-id="48fb5-638">Creating projects</span></span>
   
   <span data-ttu-id="48fb5-639">Puede organizar y administrar el código de R en proyectos mediante RStudio.</span><span class="sxs-lookup"><span data-stu-id="48fb5-639">You can organize and manage your R code into projects by using RStudio.</span></span> <span data-ttu-id="48fb5-640">La documentación que utiliza proyectos se encuentra en https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span><span class="sxs-lookup"><span data-stu-id="48fb5-640">The documentation that uses projects can be found at https://support.rstudio.com/hc/articles/200526207-Using-Projects.</span></span>
   
   <span data-ttu-id="48fb5-641">Recomiendo seguir estas instrucciones y crear un proyecto para los ejemplos de código R de este documento.</span><span class="sxs-lookup"><span data-stu-id="48fb5-641">I recommend that you follow these directions and create a project for the R code examples in this document.</span></span>  
2. <span data-ttu-id="48fb5-642">Edición y ejecución de código R</span><span class="sxs-lookup"><span data-stu-id="48fb5-642">Editing and executing R code</span></span>
   
   <span data-ttu-id="48fb5-643">RStudio proporciona un entorno integrado para editar y ejecutar código R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-643">RStudio provides an integrated environment for editing and executing R code.</span></span> <span data-ttu-id="48fb5-644">La documentación se encuentra en https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span><span class="sxs-lookup"><span data-stu-id="48fb5-644">Documentation can be found at https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.</span></span>
3. <span data-ttu-id="48fb5-645">Depuración</span><span class="sxs-lookup"><span data-stu-id="48fb5-645">Debugging</span></span>
   
   <span data-ttu-id="48fb5-646">RStudio incluye eficaces capacidades de depuración.</span><span class="sxs-lookup"><span data-stu-id="48fb5-646">RStudio includes powerful debugging capabilities.</span></span> <span data-ttu-id="48fb5-647">Encontrará la documentación de estas características en https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span><span class="sxs-lookup"><span data-stu-id="48fb5-647">Documentation for these features is at https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.</span></span>
   
   <span data-ttu-id="48fb5-648">Las características de solución de problemas en puntos de interrupción se documentan en https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="48fb5-648">The breakpoint troubleshooting features are documented at https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.</span></span>

## <span data-ttu-id="48fb5-649"><a id="appendixb"></a>APÉNDICE B: lectura adicional</span><span class="sxs-lookup"><span data-stu-id="48fb5-649"><a id="appendixb"></a>APPENDIX B: Further reading</span></span>
<span data-ttu-id="48fb5-650">Este tutorial de programación R cubre los aspectos básicos de lo que debe usar el lenguaje R con Estudio de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="48fb5-650">This R programming tutorial covers the basics of what you need to use the R language with Azure Machine Learning Studio.</span></span> <span data-ttu-id="48fb5-651">Si no está familiarizado con el código R, encontrará dos introducciones disponibles en CRAN:</span><span class="sxs-lookup"><span data-stu-id="48fb5-651">If you are not familiar with R, two introductions are available on CRAN:</span></span>

* <span data-ttu-id="48fb5-652">R for Beginners de Emmanuel Paradis es un buen punto de partida. Lo encontrará en http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span><span class="sxs-lookup"><span data-stu-id="48fb5-652">R for Beginners by Emmanuel Paradis is a good place to start at http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.</span></span>  
* <span data-ttu-id="48fb5-653">Una introducción a R de W.</span><span class="sxs-lookup"><span data-stu-id="48fb5-653">An Introduction to R by W. N.</span></span> <span data-ttu-id="48fb5-654">Venables et.</span><span class="sxs-lookup"><span data-stu-id="48fb5-654">Venables et.</span></span> <span data-ttu-id="48fb5-655">al.</span><span class="sxs-lookup"><span data-stu-id="48fb5-655">al.</span></span> <span data-ttu-id="48fb5-656">profundiza un poco más en la materia. La encontrará en http://cran.r-project.org/doc/manuals/R-intro.html.</span><span class="sxs-lookup"><span data-stu-id="48fb5-656">goes into a bit more depth, at http://cran.r-project.org/doc/manuals/R-intro.html.</span></span>

<span data-ttu-id="48fb5-657">Existen muchas obras sobre el código R que pueden servirle como punto de partida.</span><span class="sxs-lookup"><span data-stu-id="48fb5-657">There are many books on R that can help you get started.</span></span> <span data-ttu-id="48fb5-658">Estas son algunas que considero más útiles:</span><span class="sxs-lookup"><span data-stu-id="48fb5-658">Here are a few I find useful:</span></span>

* <span data-ttu-id="48fb5-659">The Art of R Programming: A Tour of Statistical Software Design de Norman Matloff ofrece una excelente introducción a la programación en código R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-659">The Art of R Programming: A Tour of Statistical Software Design by Norman Matloff is an excellent introduction to programming in R.</span></span>  
* <span data-ttu-id="48fb5-660">R Cookbook de Paul Teetor ofrece un enfoque del uso del código R basado en problemas y soluciones.</span><span class="sxs-lookup"><span data-stu-id="48fb5-660">R Cookbook by Paul Teetor provides a problem and solution approach to using R.</span></span>  
* <span data-ttu-id="48fb5-661">R in Action de Robert Kabacoff es otro libro que puede resultarle muy útil.</span><span class="sxs-lookup"><span data-stu-id="48fb5-661">R in Action by Robert Kabacoff is another useful introductory book.</span></span> <span data-ttu-id="48fb5-662">El sitio de web complementario Quick R es un recurso que le será de gran utilidad: http://www.statmethods.net/.</span><span class="sxs-lookup"><span data-stu-id="48fb5-662">The companion Quick R website is a useful resource at http://www.statmethods.net/.</span></span>
* <span data-ttu-id="48fb5-663">R Inferno de Patrick Burns es un libro sorprendentemente divertido que lo ayudará a abordar numerosos temas complejos con los que puede encontrarse a la hora de programar en código R. Esta obra está disponible gratis en http://www.burns-stat.com/documents/books/the-r-inferno/.</span><span class="sxs-lookup"><span data-stu-id="48fb5-663">R Inferno by Patrick Burns is a surprisingly humorous book that deals with a number of tricky and difficult topics that can be encountered when programming in R. The book is available for free at http://www.burns-stat.com/documents/books/the-r-inferno/.</span></span>
* <span data-ttu-id="48fb5-664">Si desea obtener información más detallada sobre temas avanzados de R, recomendamos el título Advanced R de Hadley Wickham.</span><span class="sxs-lookup"><span data-stu-id="48fb5-664">If you want a deep dive into advanced topics in R, have a look at the book Advanced R by Hadley Wickham.</span></span> <span data-ttu-id="48fb5-665">La versión en línea de este libro está disponible de forma gratuita en http://adv-r.had.co.nz/.</span><span class="sxs-lookup"><span data-stu-id="48fb5-665">The online version of this book is available for free at http://adv-r.had.co.nz/.</span></span>

<span data-ttu-id="48fb5-666">Podrá encontrar un catálogo de series temporales de R en la vista de tareas CRAN para análisis de series temporales: http://cran.r-project.org/web/views/TimeSeries.html.</span><span class="sxs-lookup"><span data-stu-id="48fb5-666">A catalogue of R time series packages can be found in the CRAN Task View for time series analysis: http://cran.r-project.org/web/views/TimeSeries.html.</span></span> <span data-ttu-id="48fb5-667">Para obtener información sobre paquetes de objetos de series temporales, debe hacer referencia a la documentación de ese paquete.</span><span class="sxs-lookup"><span data-stu-id="48fb5-667">For information on specific time series object packages, you should refer to the documentation for that package.</span></span>

<span data-ttu-id="48fb5-668">El libro Introductory Time Series with R de Paul Cowpertwait y Andrew Metcalfe ofrece una introducción al uso de R para el análisis de series temporales.</span><span class="sxs-lookup"><span data-stu-id="48fb5-668">The book Introductory Time Series with R by Paul Cowpertwait and Andrew Metcalfe provides an introduction to using R for time series analysis.</span></span> <span data-ttu-id="48fb5-669">No obstante, existen muchos más textos teóricos que proporcionan ejemplos de R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-669">Many more theoretical texts provide R examples.</span></span>

<span data-ttu-id="48fb5-670">Algunos recursos excelentes en Internet:</span><span class="sxs-lookup"><span data-stu-id="48fb5-670">Some great internet resources:</span></span>

* <span data-ttu-id="48fb5-671">DataCamp: DataCamp enseña R desde la comodidad del explorador con lecciones en vídeo y ejercicios de codificación.</span><span class="sxs-lookup"><span data-stu-id="48fb5-671">DataCamp: DataCamp teaches R in the comfort of your browser with video lessons and coding exercises.</span></span> <span data-ttu-id="48fb5-672">Existen tutoriales interactivos sobre los paquetes y las técnicas más recientes de R.</span><span class="sxs-lookup"><span data-stu-id="48fb5-672">There are interactive tutorials on the latest R techniques and packages.</span></span> <span data-ttu-id="48fb5-673">Tutorial interactivo gratis de R en https://www.datacamp.com/courses/introduction-to-r</span><span class="sxs-lookup"><span data-stu-id="48fb5-673">Take the free interactive R tutorial at https://www.datacamp.com/courses/introduction-to-r</span></span>
* <span data-ttu-id="48fb5-674">Una guía de introducción a R de Programiz en https://www.programiz.com/r-programming</span><span class="sxs-lookup"><span data-stu-id="48fb5-674">A guide on Getting started with R from Programiz https://www.programiz.com/r-programming</span></span>
* <span data-ttu-id="48fb5-675">Un tutorial rápido de R Kelly Black de la Universidad de Clarkson: http://www.cyclismo.org/tutorial/R/</span><span class="sxs-lookup"><span data-stu-id="48fb5-675">A quick R tutorial by Kelly Black from Clarkson University http://www.cyclismo.org/tutorial/R/</span></span>
* <span data-ttu-id="48fb5-676">Recopilación de más de 60 recursos de R en http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span><span class="sxs-lookup"><span data-stu-id="48fb5-676">60+ R resources listed at http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html</span></span>

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
