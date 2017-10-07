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
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a>Tutorial de inicio rápido de lenguaje de programación de hello R de aprendizaje automático de Azure

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a>Introducción
Este tutorial de inicio rápido le ayuda a empezar rápidamente a ampliar el aprendizaje automático de Azure mediante el lenguaje de programación de hello R. Seguir este tutorial toocreate de programación de R, probar y ejecutar código de R en aprendizaje automático de Azure. Cuando se trabaja a través del tutorial, creará una solución de previsión completa mediante el lenguaje de hello R en aprendizaje automático de Azure.  

Aprendizaje automático de Microsoft Azure contiene muchos módulos versátiles de manipulación de datos y aprendizaje automático. lenguaje R eficaz de Hola se ha descrito como Hola lengua franca de análisis. Por suerte, manipulación de datos y análisis en aprendizaje automático de Azure puede ampliarse mediante el uso de R. Esta combinación proporciona Hola escalabilidad y facilidad de implementación de aprendizaje automático de Azure con la flexibilidad de Hola y análisis profundo de R.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a>Conjunto de datos de previsión y Hola
La previsión es un método de análisis ampliamente utilizado y bastante útil. Intervalo de predecir las ventas de temporada elementos, determinar los niveles de inventario óptimo, variables macroeconómicas toopredicting usos comunes. La previsión suele realizarse con modelos de serie temporal.

Datos de series temporales son datos en el que los valores de hello tienen un índice de tiempo. índice de tiempo de Hello puede ser normal, por ejemplo, cada mes o cada minuto, o irregulares. Los modelos de serie temporal se basan en datos de series temporales. lenguaje de programación de Hello R contiene un marco de trabajo flexible y una amplia análisis de datos de series temporales.

En esta guía de inicio rápido, trabajaremos con los productos lácteos de California y los datos de precios. Estos datos incluyen información mensual en producción de hello de varios productos lácteos y el precio de Hola de fat leche, un estándar de la prueba comparativa.

Hola los datos utilizados en este artículo, junto con scripts de R, pueden ser [descargarse aquí][download]. Estos datos originalmente se sintetizan de información disponible en hello Universidad de Wisconsin en http://future.aae.wisc.edu/tab/production.html.

### <a name="organization"></a>Organización
Tal y como se muestra cómo toocreate, probar y ejecutar código de R de manipulación de datos y análisis en el entorno de aprendizaje automático de Azure de hello, que se progresamos en varios pasos.  

* En primer lugar, exploraremos conceptos básicos de Hola de usando el lenguaje de hello R en el entorno de estudio de aprendizaje automático de Azure Hola.
* A continuación, que progresamos toodiscussing diversos aspectos de la E/S de datos, código de R y gráficos en el entorno de aprendizaje automático de Azure de Hola.
* A continuación, se construirá primera parte de nuestra solución previsión de hello mediante la creación de código para la limpieza de datos y transformación.
* Con nuestros datos preparados se realizará un análisis de correlaciones de hello entre algunas de las variables de hello en el conjunto de datos.
* Por último, crearemos un modelo de previsión de serie temporal estacional para la producción de leche.

## <a id="mlstudio"></a>Interacción con el lenguaje R para Machine Learning Studio
En esta sección le guiará por algunos conceptos básicos de la interacción con el lenguaje de programación de hello R en el entorno de estudio de aprendizaje automático de Hola. lenguaje de Hello R proporciona una herramienta eficaz toocreate personalizar datos y análisis manipulación módulos dentro del entorno de aprendizaje automático de Azure Hola.

Usaré RStudio toodevelop, probar y depurar código de R en una pequeña escala. Este código es, a continuación, cortar y pegar en una [ejecutar Script de R] [ execute-r-script] módulo en estudio de aprendizaje automático listo toorun.  

### <a name="hello-execute-r-script-module"></a>módulo ejecutar Script de R de Hola
En estudio de aprendizaje automático, se ejecutan los scripts de R en hello [ejecutar Script de R] [ execute-r-script] módulo. Un ejemplo de Hola [ejecutar Script de R] [ execute-r-script] módulo en estudio de aprendizaje automático se muestra en la figura 1.

 ![Lenguaje de programación R: módulo ejecutar Script de R de hello seleccionado en estudio de aprendizaje automático][1]

*Figura 1. entorno de estudio de aprendizaje automático de Hello mostrar hello ejecutar Script de R módulo seleccionado.*

Que hace referencia tooFigure 1, veamos algunos de los elementos clave de hello del entorno de estudio de aprendizaje automático de Hola para trabajar con hello [ejecutar Script de R] [ execute-r-script] módulo.

* módulos de Hello en el experimento de Hola se muestran en el panel central de Hola.
* parte superior de Hello del panel derecho de hello contiene un tooview de ventana y editar los scripts de R.  
* parte inferior de Hello del panel derecho muestra algunas propiedades de hello [ejecutar Script de R][execute-r-script]. Puede ver los registros de error y de salida de hello haciendo clic en las zonas adecuado Hola de este panel.

Por supuesto, analizaremos hello [ejecutar Script de R] [ execute-r-script] con más detalle en el resto de Hola de este documento.

Cuando se utilicen funciones complejas de R, es recomendable editar, probar y depurar el código en RStudio. Al igual que con cualquier desarrollo de software, amplíe el código de forma incremental y pruébelo en casos de prueba más sencillos.  A continuación, cortar y pegar las funciones en la ventana de script de Hola R de hello [ejecutar Script de R] [ execute-r-script] módulo. Este enfoque permite que tooharness RStudio entorno de desarrollo integrado (IDE) de Hola y Hola potencia de aprendizaje automático de Azure.  

#### <a name="execute-r-code"></a>Ejecución del código R
Cualquier código de R en hello [ejecutar Script de R] [ execute-r-script] módulo se ejecutará cuando se ejecute el experimento de Hola haciendo clic en hello **ejecutar** botón. Cuando haya finalizado la ejecución, aparecerá una marca de verificación en hello [ejecutar Script de R] [ execute-r-script] icono.

#### <a name="defensive-r-coding-for-azure-machine-learning"></a>Codificación R defensiva para Aprendizaje automático de Azure
Si está desarrollando código R para un servicio web utilizando Aprendizaje automático de Azure, deberá planear cómo tratará el código las entradas de datos inesperadas y las excepciones. toomaintain claridad, he no incluí gran parte de manera Hola de comprobación o control de excepciones en la mayoría de los ejemplos de código de hello mostrados. Sin embargo, conforme avancemos compartiré varios ejemplos de funciones mediante la capacidad de control de excepciones de R.  

Si necesita un tratamiento más completado del control de excepciones de R, recomienda leer secciones aplicables de Hola de libro de hello Wickham enumerado en [Apéndice B - más información](#appendixb).

#### <a name="debug-and-test-r-in-machine-learning-studio"></a>Depuración y prueba de R en Estudio de aprendizaje automático
tooreiterate, recomienda probar y depurar el código de R en una pequeña escala en RStudio. Sin embargo, hay casos donde debe tootrack problemas de código de R en hello [ejecutar Script de R] [ execute-r-script] propio. Además, es recomendable toocheck los resultados en estudio de aprendizaje automático.

Resultado de la ejecución del código R y en la plataforma de aprendizaje automático de Azure de Hola Hola se encuentra principalmente en salida.log. Se mostrará información adicional en el archivo error.log.  

Si se produce un error en estudio de aprendizaje automático mientras se ejecuta el código de R, la primera línea de conducta debe toolook en error.log. Este archivo puede contener toohelp de mensajes de error útil entender y corrija el error. tooview error.log, haga clic en **Ver registro de errores** en hello **panel Propiedades** para hello [ejecutar Script de R] [ execute-r-script] que contiene el error de Hola.

Por ejemplo, se ejecutó Hola siguiente código de R, con un variable y sin definir, en un [ejecutar Script de R] [ execute-r-script] módulo:

    x <- 1.0
    z <- x + y

Este código produce un error tooexecute, lo que produce una condición de error. Al hacer clic en **Ver registro de errores** en hello **panel Propiedades** produce Hola presentación que se muestra en la figura 2.

  ![Mensaje de error emergente][2]

*Ilustración 2. Mensaje de error emergente.*

Parece que necesitamos toolook salida.log toosee Hola R mensaje de error. Haga clic en hello [ejecutar Script de R] [ execute-r-script] y, a continuación, haga clic en hello **ver salida.log** elemento en hello **panel Propiedades** toohello derecha. Se abre una nueva ventana del explorador, y yo vemos siguiente Hola.

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

Este mensaje de error no contiene sorpresas e identifique claramente el problema de Hola.

valor de hello tooinspect de cualquier objeto de R, puede imprimir estos archivos de valores toohello salida.log. las reglas de Hola para examinar el objeto de los valores son básicamente iguales Hola como en una sesión interactiva de R. Por ejemplo, si escribe un nombre de variable en una línea, valor de hello del objeto de hello será toohello impreso salida.log archivo.  

#### <a name="packages-in-machine-learning-studio"></a>Paquetes de Estudio de aprendizaje automático
Aprendizaje automático de Azure incluye más de 350 paquetes del lenguaje R preinstalados. Puede usar Hola después el código de hello [ejecutar Script de R] [ execute-r-script] módulo tooretrieve una lista de hello preinstalado paquetes.

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

Si no entiende la última línea de este código de hello en el momento de hello, siga leyendo. En el resto de Hola de este documento, trataremos mucho uso de R en el entorno de aprendizaje automático de Azure de Hola.

### <a name="introduction-toorstudio"></a>Introducción tooRStudio
RStudio es un IDE ampliamente utilizado para R. Usaré RStudio para editar, probar y depurar parte del código de hello R utilizada en esta guía de inicio rápido. Una vez probados y listo código R, simplemente cortar y pegar desde el editor de RStudio hello en un estudio de aprendizaje automático [ejecutar Script de R] [ execute-r-script] módulo.  

Si no tiene el lenguaje de programación de hello R instalado en su equipo de escritorio, recomienda que hacerlo ahora. Descargas gratuitas de lenguaje de código abierto R están disponibles en hello red completa de archivo de R (CRAN) en [http://www.r-project.org/](http://www.r-project.org/). Hay descargas disponibles para Windows, Mac OS y Linux/UNIX. Elija un reflejo cercano y siga las instrucciones de descarga de Hola. Además, CRAN contiene una gran cantidad de paquetes de manipulación de datos y análisis de utilidad.

Si está tooRStudio nueva, debe descargar e instalar la versión de escritorio de Hola. Puede encontrar Hola que rstudio descarga para Windows, Mac OS y Linux/UNIX a http://www.rstudio.com/products/RStudio/. Siga las instrucciones de hello proporcionadas tooinstall RStudio en su equipo de escritorio.  

Una introducción al tutorial tooRStudio está disponible en https://support.rstudio.com/hc/sections/200107586-Using-RStudio.

En el [Apéndice A][appendixa], encontrará información adicional sobre el uso de RStudio.  

## <a id="scriptmodule"></a>Obtener datos dentro y fuera del módulo ejecutar Script de R de Hola
En esta sección, veremos cómo obtener los datos dentro y fuera de hello [ejecutar Script de R] [ execute-r-script] módulo. Analizaremos cómo toohandle diversos tipos de datos de lectura dentro y fuera de hello [ejecutar Script de R] [ execute-r-script] módulo.

Hola de código completo de esta sección se encuentra en el archivo zip de Hola que descargó anteriormente.

### <a name="load-and-check-data-in-machine-learning-studio"></a>Carga y comprobación de datos en Estudio de aprendizaje automático
#### <a id="loading"></a>El conjunto de datos de carga Hola
Empezaremos cargar hello **csdairydata.csv** archivo en estudio de aprendizaje automático de Azure.

* Iniciar su entorno Estudio de aprendizaje automático de Azure
* Haga clic en **+ nuevo** en hello parte inferior izquierda de la pantalla y seleccione **conjunto de datos**.
* Seleccione **de archivo Local**y, a continuación, **examinar** archivo de hello tooselect.
* Asegúrese de que ha seleccionado **archivo CSV genérico con encabezado (.csv)** como tipo de hello para el conjunto de datos de Hola.
* Haga clic en la marca de verificación de Hola.
* Después de que se ha cargado el conjunto de datos de hello, debería ver Hola nuevo conjunto de datos haciendo clic en hello **conjuntos de datos** ficha.  

#### <a name="create-an-experiment"></a>Creación de un experimento
Ahora que tenemos algunos datos en estudio de aprendizaje automático, necesitamos toocreate un análisis de experimento toodo Hola.  

* Haga clic en **+ nuevo** en hello inferior izquierdo y seleccione **experimento**, a continuación, **en blanco de experimento**.
* Puede nombrar el experimento mediante la selección y modificar, Hola **experimento creado en...**  el título a la parte superior de Hola de página de Hola. Por ejemplo, cambiar demasiado**CA lácteos Analysis**.
* Izquierda Hola de página de experimento de hello, expanda **conjuntos de datos guardados**y, a continuación, **Mis conjuntos de datos**. Debería ver Hola **cadairydata.csv** que haya cargado anteriormente.
* Hola de arrastrar y colocar **csdairydata.csv dataset** en el experimento de Hola.
* Hola **búsqueda experimentar elementos** cuadro en la parte superior de hello del panel izquierdo de hello, tipo [ejecutar Script de R][execute-r-script]. Verá módulo Hola aparecen en la lista de búsqueda de Hola.
* Hola de arrastrar y colocar [ejecutar Script de R] [ execute-r-script] módulo en el palet.  
* Conecte la salida de hello de hello **csdairydata.csv dataset** entrada izquierda toohello (**Dataset1**) de hello [ejecutar Script de R][execute-r-script].
* **No olvide tooclick en 'Guardar'.**  

En este punto el experimento debería tener un aspecto similar al de la ilustración 3.

![Hola CA lácteos Analysis experimentar con el conjunto de datos y módulo ejecutar Script de R][3]

*Figura 3. Hola CA lácteos Analysis experimentar con el conjunto de datos y módulo ejecutar Script de R.*

#### <a name="check-on-hello-data"></a>Comprobar datos Hola
Echemos un vistazo a los datos de saludo que se han cargado en el experimento. En el experimento de hello, haga clic en salida de hello de hello **conjunto de datos de cadairydata.csv** y seleccione **visualizar**. Debería ver algo parecido a lo que se muestra en la ilustración 4.  

![Resumen del conjunto de datos de hello cadairydata.csv][4]

*Ilustración 4. Resumen del conjunto de datos de hello cadairydata.csv.*

En esta vista hay una gran cantidad de información útil. Podemos ver Hola primera varias filas de ese conjunto de datos. Si se selecciona una columna, Hola sección de estadísticas de muestra para obtener más información acerca de la columna de Hola. Por ejemplo, fila de tipo de característica de hello muestra qué tipos de datos estudio de aprendizaje automático de Azure asigna la columna toohello. Tener una visión rápida parecido a esto es una buena comprobación antes de empezar cualquier trabajo grave toodo.

### <a name="first-r-script"></a>Primer script de R
Vamos a crear un simple tooexperiment con script primera R en estudio de aprendizaje automático de Azure. He creado y probado Hola siguiente secuencia de comandos en RStudio.  

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

Ahora necesito tootransfer esta tooAzure script estudio de aprendizaje automático. Basta con cortar y pegar. Sin embargo, en este caso, transferiré el script de código R mediante un archivo zip.

### <a name="data-input-toohello-execute-r-script-module"></a>Módulo de ejecutar Script de R toohello de entrada de datos
Echemos un vistazo a Hola entradas toohello [ejecutar Script de R] [ execute-r-script] módulo. En este ejemplo se leerá los datos de hello California lecheras en hello [ejecutar Script de R] [ execute-r-script] módulo.  

Hay tres entradas posibles para hello [ejecutar Script de R] [ execute-r-script] módulo. Puede usar cualquiera de estas entradas o todas ellas, dependiendo de la aplicación. También es perfectamente razonable toouse una R script que no toma ninguna entrada.  

Echemos un vistazo a cada una de estas entradas, desde la izquierda tooright. Puede ver los nombres Hola cada una de las entradas de hello colocando el cursor sobre entrada hello y leer información sobre herramientas de Hola.  

#### <a name="script-bundle"></a>Paquete de script
Hello proporcionados por el paquete de scripts permite toopass Hola contenido de un archivo zip en [ejecutar Script de R] [ execute-r-script] módulo. Puede usar uno de hello después el contenido de hello tooread de comandos del archivo zip de hello en el código de R.

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> Aprendizaje automático de Azure trata los archivos en zip hello como si fueran en hello src / directory, por lo que necesita tooprefix nombres de los archivos con este nombre de directorio. Por ejemplo, si hello zip contiene archivos de hello `yourfile.R` y `yourData.rdata` en raíz de Hola de zip Hola, ¿tratarlos como `src/yourfile.R` y `src/yourData.rdata` al usar `source` y `load`.
> 
> 

Ya se explicó conjuntos de datos de carga en [cargar el conjunto de datos de hello](#loading). Una vez que haya creado y probado script de Hola R que se muestra en la sección anterior de hello, Hola siguientes:

1. Guardar script de Hola R en una. Archivo de R. Llamaré a mi archivo de script "simpleplot.R". Este es el contenido de Hola.
   
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
2. Cree un archivo zip y copie el script en el archivo zip. En Windows, puede haga doble clic en el archivo hello y seleccione **enviar a**y, a continuación, **carpeta comprimida**. Esto creará un nuevo archivo zip que contiene Hola "simpleplot. Archivo de R".
3. Agregar el archivo toohello **conjuntos de datos** en estudio de aprendizaje automático, especificación de tipo hello como **postal**. Ahora debería ver el archivo zip de hello en los conjuntos de datos.
4. Arrastrar y colocar Hola ZIP del **conjuntos de datos** en hello **lienzo de estudio de aprendizaje automático**.
5. Conecte la salida de hello de hello **comprimir datos** icono toohello **agrupación de scripts** entrada de hello [ejecutar Script de R] [ execute-r-script] módulo.
6. Hola de tipo `source()` función con el nombre del archivo zip en la ventana de código de hello para hello [ejecutar Script de R] [ execute-r-script] módulo. En mi caso escribí `source("src/simpleplot.R")`.  
7. Asegúrese de hacer clic en **Guardar**.

Una vez completados estos pasos, Hola [ejecutar Script de R] [ execute-r-script] módulo ejecutará el script de Hola R en el archivo zip de hello cuando se ejecute el experimento de Hola. En este punto el experimento debería tener un aspecto similar al que se muestra en la ilustración 5.

![Experimento con el script de código R comprimido en un archivo zip][6]

*Ilustración 5. Experimento con el script de código R comprimido en un archivo zip.*

#### <a name="dataset1"></a>DataSet1
Puede pasar una tabla rectangular de código de tooyour R datos mediante la entrada de hello Dataset1. En nuestro Hola de secuencia de comandos simple `maml.mapInputPort(1)` función lee los datos de Hola de puerto 1. Estos datos, a continuación, se asignan el nombre de variable tooa trama de datos en el código. En nuestro script simple primera línea de código de hello realiza la asignación de Hola.

    cadairydata <- maml.mapInputPort(1)

Ejecutar el experimento, haga clic en hello **ejecutar** botón. Cuando concluya la ejecución de hello, haga clic en hello [ejecutar Script de R] [ execute-r-script] módulo y, a continuación, haga clic en **Ver registro de salida** en el panel de propiedades de Hola. Debe aparecer una nueva página en el explorador que muestra contenido de Hola de archivo de hello salida.log. Cuando se desplaza hacia abajo verá algo parecido a Hola siguiente.

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

Más abajo Hola página es información más detallada sobre las columnas de hello, que será similar al siguiente Hola.

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

Estos resultados son principalmente según lo previsto con 9 columnas en la trama de datos de Hola y 228 observaciones. Podemos ver los nombres de columna de hello, tipo de datos de hello R y un ejemplo de cada columna.

> [!NOTE]
> Esta misma salida impresa hay cómodamente en hello salida de dispositivo de R de hello [ejecutar Script de R] [ execute-r-script] módulo. Trataremos las salidas de Hola de hello [ejecutar Script de R] [ execute-r-script] módulo en la sección siguiente Hola.  
> 
> 

#### <a name="dataset2"></a>Dataset2
Hello comportamiento de entrada de hello Dataset2 es idéntico toothat DataSet1. Con esta entrada, se puede pasar una segunda tabla rectangular de datos al código R. Hola función `maml.mapInputPort(2)`, con el argumento de hello 2, es toopass usa estos datos.  

### <a name="execute-r-script-outputs"></a>Ejecución de resultados de script de código R
#### <a name="output-a-dataframe"></a>Generación de tramas de datos
Puede generar contenido de Hola de una trama de datos de R como una tabla rectangular a través del puerto de hello Dataset1 de resultados mediante el uso de hello `maml.mapOutputPort()` función. En nuestro script de R simple, esto se realiza con hello después de línea.

    maml.mapOutputPort('cadairydata')

Después de la ejecución experimento de hello, haga clic en puerto de salida de resultado Dataset1 Hola y, a continuación, haga clic en **visualizar**. Debería ver algo parecido a lo que se muestra en la ilustración 6.

![Visualización de Hola de salida de hello de hello datos lecheras de California][7]

*Figura 6. Visualización de Hola de salida de hello de hello datos lecheras de California.*

Esta salida es la siguiente entrada toohello idénticos, exactamente como se esperaba.  

### <a name="r-device-output"></a>Resultados del dispositivo R
Hola salida de dispositivo de hello [ejecutar Script de R] [ execute-r-script] módulo contiene la salida de mensajes y los gráficos. Ambos mensajes de error estándar y de salida estándares de R se envían toohello puerto de salida de dispositivo de R.  

Hola tooview R dispositivo de salida, haga clic en el puerto de hello y, a continuación, en **visualizar**. Vemos salida estándar de Hola y el error estándar desde un script de Hola R en la figura 7.

![Salida estándar y el error estándar de hello puerto de dispositivo de R][8]

*Ilustración 7. Salida estándar y el error estándar de hello puerto de dispositivo de R.*

Desplace hacia abajo se ve un resultado de gráficos de Hola de nuestro script de R en la figura 8.  

![Salida de gráficos de hello puerto de dispositivo de R][9]

*Ilustración 8. Gráficos de salida de hello puerto de dispositivo de R.*  

## <a id="filtering"></a>Transformación y filtrado de datos
En esta sección se llevará a cabo algunos datos básicos de filtrado y operaciones de transformación en hello datos lecheras de California. Extremo de Hola de esta sección tenemos datos en un formato adecuado para generar un modelo analítico.  

En esta sección se realizarán varias tareas de transformación y limpieza de datos comunes: transformación de tipos, filtrado de tramas de datos, adición de nuevas columnas de cálculo y transformaciones de valor. Este fondo debe ayudar a tratar con hello muchas variaciones encontradas problemas reales.

código de R completo de Hola de esta sección está disponible en el archivo zip de Hola que descargó anteriormente.

### <a name="type-transformations"></a>Transformaciones de tipo
Ahora que podemos leer datos de hello California lecheras en código de hello R de hello [ejecutar Script de R] [ execute-r-script] módulo, necesitamos tooensure que los datos de hello en columnas de hello tienen tipo hello diseñado y el formato.  

R es un lenguaje con tipos dinámicos, lo que significa que los tipos de datos se convierten de un tooanother según sea necesario. tipos de datos atómico de Hello en R son numéricos, lógica y de caracteres. tipo de factor de Hello es toocompactly usado categorías de almacén de datos. Puede encontrar mucha más información sobre los tipos de datos en las referencias de hello en [Apéndice B - lectura adicional](#appendixb).

Cuando se leen los datos tabulares en R desde un origen externo, siempre es un Hola de toocheck buena idea resultante tipos de columnas de Hola. Es posible que desee una columna de caracteres de tipo, pero en muchos casos esto se mostrará como factor o viceversa. En otros casos, la columna que piensa que debe ser numérica se mostrará con datos de caracteres como, por ejemplo, '1,23' en lugar de 1,23 como número de punto flotante.  

Afortunadamente, es fácil tooconvert una tooanother de tipo, siempre que sea posible la asignación. Por ejemplo, no se puede convertir 'Nevada' en un valor numérico, pero se puede convertir el factor de tooa (variable de categoría). Como otro ejemplo, puede convertir el valor numérico 1 en un carácter '1' o en un factor.  

sintaxis de Hola para cualquiera de estas conversiones es simple: `as.datatype()`. Estas funciones de conversión de tipo hello siguientes.

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

Examinando los tipos de datos de Hola de columnas de Hola se de entrada en la sección anterior de hello: todas las columnas son de tipo numérico, excepto la columna de hello con la etiqueta 'Month', que es de carácter de tipo. Vamos a convertir este factor tooa y Hola resultados de pruebas.  

He eliminé línea hello que crea la matriz scatterplot de Hola y se agrega una línea convertir factor de hello 'Month' columna tooa. En el experimento simplemente se corte y pegue el código de hello R en la ventana de código de hello de hello [ejecutar Script de R] [ execute-r-script] módulo. También puede actualizar el archivo zip de Hola y cargarlo tooAzure estudio de aprendizaje automático, pero esto lleva a cabo varios pasos.  

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

Vamos a ejecutar este código y buscar en el registro de salida de hello para hello script de R. datos importantes de Hola de registro de hello se muestran en la figura 9.

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

*Ilustración 9. Resumen de la trama de datos de hello con una variable de factor.*

Ahora debe indicar el tipo de Hello para el mes '**Factor con 14 niveles**'. Se trata de un problema dado que hay solo 12 meses de año de Hola. También puede comprobar toosee que Hola tipo en **visualizar** del conjunto de datos de resultado de hello es puerto '**categorías**'.

problema de Hello es esa columna no se codificó sistemáticamente ' Month' hello. En algunos casos, un mes se denomina Abril y en otros se abrevia como Abr. Se puede resolver este problema si recortar los caracteres de too3 Hola de una cadena. línea de saludo de código ahora Hola siguiente aspecto:

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

Vuelva a ejecutar el experimento de Hola y ver el registro de salida de hello. Hola espera resultados se muestran en la figura 10.  

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

*Ilustración 10. Resumen de la trama de datos de hello con el número correcto de niveles de factor.*

La variable de factor tiene ahora Hola deseado 12 niveles.

### <a name="basic-data-frame-filtering"></a>Filtrado del marco de datos básico
Las tramas de datos R incluyen capacidades de filtrado eficaces. Es posible obtener subconjuntos de los conjuntos de datos mediante el uso de filtros lógicos en filas o columnas. En muchos casos, serán necesarios criterios de filtro complejos. Hola hace referencia en [Apéndice B - lectura adicional](#appendixb) contienen ejemplos detallados del filtrado de tramas de datos.  

En nuestro conjunto de datos, es necesario crear un bit de filtrado. Si observa en las columnas de hello en la trama de datos de hello cadairydata, verá dos columnas innecesarias. primera columna de Hello solo contiene un número de fila, lo que no resulta muy útil. Hola segunda columna, Year.Month, contiene información redundante. Podemos fácilmente excluimos estas columnas mediante el uso de hello siguiente código de R.

> [!NOTE]
> De ahora en esta sección, simplemente mostrará Hola código adicional agrego Hola [ejecutar Script de R] [ execute-r-script] módulo. Agregará a cada nueva línea **antes de** hello `str()` función. Usar esta función tooverify mis resultados en estudio de aprendizaje automático de Azure.
> 
> 

Agregar Hola siguiente línea toomy R código de hello [ejecutar Script de R] [ execute-r-script] módulo.

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

Ejecutar este código en el experimento y compruebe el resultado de hello de registro de salida de hello. Estos resultados se muestran en la ilustración 11.

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

*Ilustración 11. Se quitó el resumen de la trama de datos de hello con dos columnas.*

¡Buenas noticias! Se produce un error Hola esperado.

### <a name="add-a-new-column"></a>Adición de una columna nueva
modelos de serie temporal de toocreate resultará conveniente toohave una columna que contiene Hola meses desde el inicio de Hola de serie temporal de Hola. Por ello, crearemos una nueva columna 'Month.Count'.

toohelp organizar el código de hello vamos a crear nuestra primera función simple, `num.month()`. A continuación, aplicaremos esta toocreate función una nueva columna en la trama de datos de Hola. nuevo código de Hello es como sigue.

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

Ahora ejecute experimento Hola actualizado y use Hola resultados registro tooview Hola. Estos resultados se muestran en la ilustración 12.

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

*Ilustración 12. Resumen de hello trama de datos con columnas adicionales de Hola.*

Parece que todo funciona correctamente. Tenemos nueva columna con los valores esperados Hola de hello en la trama de datos.

### <a name="value-transformations"></a>Transformaciones de valor
En esta sección se realizará algunas transformaciones simples en valores de hello en algunas de las columnas de hello de la trama de datos. idioma de Hello R admite transformaciones de valor casi arbitrario. Hola hace referencia en [Apéndice B - más información](#appendixb) contienen ejemplos exhaustivos.

Si observa valores de hello en resúmenes de saludo de la trama de datos debería ver algo impar aquí. ¿Se produce más de helado que leche en California? No, por supuesto no es así, como esto no tiene sentido, sad como este hecho puede ser toosome de nosotros amantes de helado. unidades de Hello son diferentes. precio de Hello es en unidades de nosotros libras, leche en unidades de 1 M libras de Estados Unidos, helado esté en unidades de 1.000 nos galones, y requesón es en unidades de 1.000 libras de Estados Unidos. Suponiendo que helado Pondere los unos 6,5 libras por galón, podemos crear fácilmente Hola tooconvert multiplicación estos valores para que tengan todas las unidades iguales de 1.000 libras.

Para nuestro modelo de pronóstico, utilizaremos un modelo de multiplicación de tendencia y de ajuste de temporada de estos datos. Una transformación de registro nos permite toouse un modelo lineal, ya que simplifica este proceso. Podemos aplicar transformación de registro de hello en la misma función que se aplica el multiplicador de Hola de Hola.

En el siguiente código de hello, definir una nueva función, `log.transform()`y aplicarlo filas toohello que contiene valores numéricos de Hola. Hola R `Map()` función es tooapply usado hello `log.transform()` toohello de función seleccionado columnas de hello trama de datos. `Map()`es similar demasiado`apply()` pero permite más de una lista de función de toohello de argumentos. Tenga en cuenta que una lista de multiplicadores suministra hello segundo argumento toohello `log.transform()` función. Hola `na.omit()` función se utiliza como un poco de limpieza tooensure, no nos tenemos que faltan o valores no definidos en Hola trama de datos.

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

Hay una gran ocurra bit en hello `log.transform()` función. La mayor parte de este código es buscar posibles problemas con argumentos de Hola o tratar con las excepciones, que todavía pueden surgir durante los cálculos de Hola. Unas pocas líneas de este código realmente Hola cálculos.

objetivo de Hola de programación estable hello es Error de hello tooprevent de una sola función que se impide el procesamiento de continuar. Un error repentino en un análisis cuya ejecución lleva mucho tiempo puede resultar muy frustrante para los usuarios. tooavoid esta situación, de forma predeterminada, se deben elegir valores devueltos que limitará daños toodownstream procesamiento. Un mensaje también es usuarios tooalert generados que ha salido mal.

Si no estás programación toodefensive utilizados en R, todo este código puede parecer un poco abrumador. Le guiará por los pasos principales que hello:

1. Se define un vector de cuatro mensajes. Estos mensajes son utilizados toocommunicate información sobre algunos de los errores posibles de Hola y las excepciones que pueden producirse con este código.
2. Devolveré un valor de NA para cada caso. Hay muchas otras posibilidades que pueden tener menos efectos secundarios. Podría devolver un vector de ceros o vector de entrada original de hello, por ejemplo.
3. Comprobaciones se realizan en función de hello argumentos toohello. En cada caso, si se detecta un error, se devuelve un valor predeterminado y genera un mensaje Hola `warning()` función. Estoy usando `warning()` en lugar de `stop()` como Hola este último finalizará la ejecución, exactamente lo que estoy tratando de tooavoid. He escrito este código en un estilo de procedimiento, ya que, en este caso, un enfoque funcional sería demasiado complejo.
4. cálculos de registro de Hello se encapsulan en `tryCatch()` para que las excepciones no provocará una tooprocessing halt abrupto. Sin `tryCatch()` , la mayoría de los errores que generan las funciones de R dan como resultado una señal de detención, que hace justamente eso.

Ejecutar este código de R en el experimento e imprimieron un vistazo a Hola resultado en hello salida.log archivo. Ahora verá los valores de hello transforman de hello registrar cuatro columnas en hello, tal como se muestra en la figura 13.

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

*Ilustración 13. Resumen de hello transforma valores de hello trama de datos.*

Podemos ver valores de hello han sido transformados. La producción de leche ahora supera con creces la producción de otros productos lácteos, recordando que ahora estamos examinando una escala logarítmica.

En este momento nuestros datos se limpian y estamos preparados el modelado. Examinando la visualización de hello resumen Hola conjunto de datos de resultado de salida de nuestra [ejecutar Script de R] [ execute-r-script] módulo, podrá ver columnas de 'Month' hello 'Categorías' con 12 valores únicos, nuevo, tal y como deseaba .

## <a id="timeseries"></a>Análisis de correlación y objetos de series temporales
En esta sección se explorará unos pocos objetos básicos de serie de tiempo de R y analizar correlaciones Hola entre algunas de las variables de Hola. Nuestro objetivo es toooutput una trama de datos que contiene hello en pares correlación información en varios retrasos.

Hola de código de R completo de esta sección se encuentra en el archivo zip de Hola que descargó anteriormente.

### <a name="time-series-objects-in-r"></a>Objetos de series de temporales de R
Como ya se ha mencionado, las series temporales son series de valores de datos indexados por tiempo. Objetos de series de tiempo de R son toocreate usado y administración el índice de la hora de Hola. Hay varias ventajas toousing tiempo serie objetos. Objetos de la serie de tiempo de evitan Hola muchos detalles de la administración de valores de índice de series de tiempo de Hola que se encapsulan en objetos de Hola. Además, objetos de la serie de tiempo de permitir que se toouse Hola muchos métodos de la serie de tiempo para trazar, imprimir, modelado, etcetera.

Hola POSIXct clase en tiempo de serie es más frecuente y es relativamente sencilla. Esta clase de la serie de tiempo mide el tiempo de inicio de Hola de época de hello, el 1 de enero de 1970. En este ejemplo se utilizarán los objetos de serie temporal POSIXct. Otras clases de objeto de serie temporal R ampliamente utilizadas son las clases zoo y xts, así como las series temporales extensibles.
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a>Ejemplo de objeto de serie temporal
Comencemos con el ejemplo. Arrastre y suelte un **nuevo** módulo [Ejecutar script R][execute-r-script] en el experimento. Conecte los puertos de salida de hello Dataset1 de resultado de hello existente [ejecutar Script de R] [ execute-r-script] puerto de hello nueva entrada de módulo toohello Dataset1 [ejecutar Script de R] [ execute-r-script] módulo.

Tal como hice para obtener ejemplos primera hello, como se avance por el ejemplo hello, en algunos puntos que mostrará solo Hola incrementales líneas adicionales de código de R en cada paso.  

#### <a name="reading-hello-dataframe"></a>Trama de datos de lectura Hola
Como primer paso, vamos a leer en una trama de datos y asegúrese de que se produce un error Hola esperado. Hello código siguiente debe hacer el trabajo de Hola.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

Ahora, ejecute el experimento de Hola. registro de Hello de la nueva forma de ejecutar Script de R Hola debería parecerse a la figura 14.

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

*Ilustración 14. Resumen de la trama de datos de hello en el módulo ejecutar Script de R de Hola.*

Estos datos son de formato y los tipos de hello esperado. Observe que la columna de 'Month' hello es de factor de tipo y ha Hola se esperaba un número de niveles.

#### <a name="creating-a-time-series-object"></a>Creación de un objeto de serie temporal
Necesitamos tooadd una trama de datos de tiempo serie objeto tooour. Reemplace el código actual de hello con siguiente hello, que agrega una nueva columna de la clase POSIXct.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

Ahora, compruebe el registro de hello. Debería ser similar al que se muestra en la ilustración 15.

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

*Ilustración 15. Resumen de hello trama de datos con un objeto de la serie de tiempo.*

Podemos ver de hello resumen que la columna nueva hello es en realidad de clase POSIXct.

### <a name="exploring-and-transforming-hello-data"></a>Explorar y transformar datos de Hola
Vamos a explorar algunas de las variables de hello en este conjunto de datos. Una matriz de scatterplot es un tooproduce buena forma un vistazo. Estoy reemplazando hello `str()` función en código de R anterior Hola con hello después de línea.

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

Ejecute este código y observe qué sucede. trazado de Hello producida Hola puerto de dispositivo de R debería parecerse figura 16.

![Matriz de trazado de dispersión de las variables seleccionadas][17]

*Ilustración 16. Matriz de trazado de dispersión de las variables seleccionadas.*

Hay alguna estructura extraña en relaciones de hello entre estas variables. Quizás esto surge de tendencias en los datos de Hola y de hechos de Hola que no hemos estandarizado variables Hola.

### <a name="correlation-analysis"></a>Análisis de correlación
análisis de correlación tooperform necesitamos tooboth anular de tendencia y estandarizar las variables de Hola. Simplemente podríamos usar Hola R `scale()` función, que se centra tanto escala variables. Esta función también puede ejecutarse más rápido. Sin embargo, deseo tooshow se muestra un ejemplo de programación estable en R.

Hola `ts.detrend()` función se muestra a continuación realiza estas dos operaciones. Hello dos líneas de código siguientes anular tendencias datos hello y, a continuación, normalizar los valores de hello.

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

Hay una gran ocurra bit en hello `ts.detrend()` función. La mayor parte de este código es buscar posibles problemas con argumentos de Hola o tratar con las excepciones, que todavía pueden surgir durante los cálculos de Hola. Unas pocas líneas de este código realmente Hola cálculos.

Ya hemos analizado un ejemplo de programación defensiva en [Transformaciones de valor](#valuetransformations). Ambos bloques de cálculo se incluyen en `tryCatch()`. En ciertos casos realiza vector de entrada original sentido tooreturn hello y en otros casos, devuelve un vector de ceros.  

Tenga en cuenta que usa para anular tendencias de regresión lineal de hello es una regresión de series de tiempo. variable de elemento de predicción de Hello es un objeto de la serie de tiempo.  

Una vez `ts.detrend()` se define se aplican toohello variables de interés en nuestra trama de datos. Nos debemos coerce lista resultante Hola creado por `lapply()` toodata trama de datos mediante el uso de `as.data.frame()`. Debido a aspectos estable de `ts.detrend()`, tooprocess error una de las variables de hello no impedirá que corregir el procesamiento del programa Hola a otros usuarios.  

línea final de Hola de código crea un scatterplot en pares. Después de ejecutar código de hello R, resultados de Hola de hello scatterplot se muestran en la figura 17.

![Trazado de dispersión en pares de series temporales estandarizadas y con las tendencias anuladas][18]

*Ilustración 17. Trazado de dispersión en pares de series temporales estandarizadas y con las tendencias anuladas.*

Puede comparar estos toothose de resultados se muestra en la figura 16. Con hello tendencia quitado y Hola variables estandarizadas, vemos mucho menos estructura en relaciones de hello entre estas variables.

las correlaciones de toocompute Hola código de Hello como objetos de R ccf es como sigue.

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

Ejecutar este código genera el registro de hello que se muestra en la figura 18.

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

*Ilustración 18. Lista de ccf objetos de análisis de correlación en pares de Hola.*

Hay un valor de correlación para cada intervalo. Ninguno de estos valores de correlación es lo suficientemente grande como toobe significativo. Por lo tanto, podemos concluir que podemos modelar cada variable de forma independiente.

### <a name="output-a-dataframe"></a>Generación de tramas de datos
Nos hemos calculado correlaciones en pares de hello como una lista de objetos de R ccf. Esto presenta un poco de un problema como puerto de salida del conjunto de datos de resultado de hello realmente requiere una trama de datos. Además, objeto ccf de hello es una lista y queremos solo los valores de hello en el primer elemento de esta lista, correlaciones hello en Hola de hello retrasos distintos.

Hola siguientes código extrae Hola lag valores de lista de Hola de objetos de ccf, que son listas.

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

Hola primera línea de código es un poco complicado y explicación puede ayudarle a entenderlo. Trabajar en profundidad de hello tenemos siguiente hello:

1. Hola '**[[**'operador con el argumento de hello'**1**' selecciona Hola vector de correlaciones en hello retrasos del primer elemento de lista de objetos de hello ccf de Hola.
2. Hola `do.call()` función aplica hello `rbind()` devuelve función sobre los elementos de Hola de lista de hello `lapply()`.
3. Hola `data.frame()` función convierte el resultado de hello generado por `do.call()` tooa trama de datos.

Tenga en cuenta que los nombres de fila Hola están en una columna de la trama de datos de Hola. Si lo hace, conserva los nombres de la fila de hello cuando vuelven de hello [ejecutar Script de R][execute-r-script].

Ejecutar código de hello produce el resultado de hello se muestra en la figura 19 cuando se **visualizar** Hola resultado al puerto del conjunto de datos de resultado de hello. nombres de la fila de Hello están en la primera columna de hello, según lo previsto.

![Salida de resultados de análisis de correlación de Hola][20]

*Ilustración 19. Resultados de salida del análisis de correlación de Hola.*

## <a id="seasonalforecasting"></a>Ejemplo de serie temporal: previsión estacional
Nuestros datos ahora están en un formato adecuado para el análisis y hemos determinado que no hay significativas correlaciones entre las variables de Hola. Vamos a continuar y a crear un modelo de previsión de serie temporal. Mediante este modelo se predecir producción de leche de California para hello 12 meses de 2013.

Nuestro modelo de pronóstico tendrá dos componentes, un componente de tendencia y un componente de temporada. previsión completa de Hello es producto Hola de estos dos componentes. Este tipo de modelo se conoce como un modelo de multiplicación. alternativa de Hello es un modelo de sumando. Ya hemos aplicado variables registro transformación toohello de interés, lo que hace este análisis manejable.

Hola de código de R completo de esta sección se encuentra en el archivo zip de Hola que descargó anteriormente.

### <a name="creating-hello-dataframe-for-analysis"></a>Creación de hello trama de datos para el análisis
Empiece agregando un **nueva** [ejecutar Script de R] [ execute-r-script] experimento tooyour de módulo. Conectar hello **conjunto de datos de resultado** salida de hello existente [ejecutar Script de R] [ execute-r-script] módulo toohello **Dataset1** entrada del nuevo módulo de Hola. resultado de Hello debe ser similar a la figura 20.

![Hola experimentar con el nuevo módulo de ejecutar Script de R Hola agregado][21]

*Figura 20. Hola experimentar con el nuevo módulo de ejecutar Script de R Hola agregado.*

Como con el análisis de correlación de Hola que se acaba de completar, necesitamos tooadd una columna con un objeto de series de tiempo POSIXct. Hola siguiente código hará esto es exactamente.

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

Ejecutar este código y examine el registro de hello. resultado de Hello debe ser similar de la figura 21.

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

*Ilustración 21. Resumen de la trama de datos de Hola.*

Con este resultado, estamos listo toostart nuestro análisis.

### <a name="create-a-training-dataset"></a>Creación de un conjunto de datos de entrenamiento
Con la trama de datos de hello construido necesitamos toocreate un conjunto de datos de entrenamiento. Estos datos incluyen todas las observaciones de hello salvo Hola últimas 12, del año de hello 2013, que es el conjunto de datos de prueba. a continuación Hola trama de datos de Hola de subconjuntos de código y crea los gráficos de las variables de producción y el precio del lecheras Hola. A continuación, crear gráficos de hello cuatro variables de producción y el precio. Una función anónima es toodefine usa algunos amplía para trazado y, a continuación, recorrer en iteración la lista de Hola de hello otros dos argumentos con `Map()`. Si piensa que un bucle for podría haber funcionado para esta operación, está en lo cierto. Sin embargo, puesto que R es un lenguaje funcional, he preferido ofrecer un enfoque funcional.

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

Ejecución de código de hello genera Hola serie de serie temporal de traza de salida de dispositivo de R Hola que se muestra en la figura 22. Tenga en cuenta ese eje de tiempo de hello en unidades de fechas, una ventaja de tiempo de hello serie traza método.

![Primero de los trazados de series temporales de la producción de productos lácteos de California y de los datos de precios](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Segundos de los trazados de series temporales de la producción de productos lácteos de California y de los datos de precios](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Tercero de los trazados de series temporales de la producción de productos lácteos de California y de los datos de precios](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Cuarto de los trazados de series temporales de la producción de productos lácteos de California y de los datos de precios](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

*Ilustración 22. Trazados de series temporales de la producción de productos lácteos de California y de los datos de precios.*

### <a name="a-trend-model"></a>Modelo de tendencia
Al haber creado un objeto de la serie de tiempo y haya tenido un vistazo a los datos de hello, comencemos tooconstruct un modelo de tendencia para hello datos de producción de leche de California. Para ello, utilizaremos una regresión de serie temporal. Sin embargo, resulta claro de trazado de Hola que se se necesita más de un tooaccurately pendiente y la intersección de modelo Hola observada tendencias en los datos de entrenamiento de Hola.

Dado pequeña escala de datos de Hola de hello, se generar modelo Hola de tendencia en RStudio y, a continuación, corte y pegue modelo resultante de hello en aprendizaje automático de Azure. RStudio proporciona un entorno interactivo para este tipo de análisis interactivo.

Como el primer intento, intentará una regresión polinómica con enciende too3. Existe un claro riesgo de sobreajuste con estos modelos. Por lo tanto, es mejor términos de orden superior tooavoid. Hola `I()` función inhibe la interpretación de contenido de hello (interpreta el contenido de Hola "tal cual") y le permite toowrite una función literalmente interpretada de una ecuación de regresión.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

Esto genera el siguiente Hola.

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

De valores P (Pr (> | t |)) en esta salida, podemos ver que Hola cuadrático término no puede ser importante. Utilizo hello `update()` función toomodify este modelo por quitar Hola cuadrado término.

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

Esto genera el siguiente Hola.

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

Mucho mejor ahora. Todos los términos de Hola de son significativos. Sin embargo, Hola 2e-16 valor es un valor predeterminado y no debe tomarse muy en serio.  

Como una prueba de comprobación, vamos a hacer un gráfico de serie de tiempo de hello datos de producción de lácteos California con una curva de tendencia de Hola que se muestra. He agregado Hola después el código de hello aprendizaje automático de Azure [ejecutar Script de R] [ execute-r-script] toocreate de modelo (no RStudio) Hola modelo y realizar un gráfico. Hola resultado se muestra en la figura 23.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![Datos de producción de leche de California con modelo de tendencias](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

*Ilustración 23. Datos de producción de leche de California con modelo de tendencias.*

Parece que el modelo de tendencia de Hola se adapta a los datos de hello bastante bien. Además, no parece que no hay evidencia de toobe de sobreajustar, como impar ondulará en curva de modelo de Hola.  

### <a name="seasonal-model"></a>Modelo de temporada
Con un modelo de tendencia en mano, se necesita toopush en y se incluyen efectos estacionales Hola. Mes de hello del año de Hola se usará como una variable ficticia en vigor de hello modelo lineal toocapture Hola por meses. Tenga en cuenta que cuando se introducen las variables de factor en un modelo, intercept hello no haya que calcular. Si no lo hace, fórmula hello es demasiado especificado y R se colocará uno Hola deseado factores, pero tenga término de intercepción de Hola.

Puesto que tenemos un modelo de tendencia satisfactorio, podemos utilizar hello `update()` toohello de modelo existente de términos de hello tooadd de función nueva. Hola -1 en la fórmula de la actualización de hello quita el término de intercepción de Hola. Continuar en RStudio para el momento de hello:

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

Esto genera el siguiente Hola.

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

Se ve ese modelo Hola ya no tiene un término de intercepción y tiene 12 factores importantes del mes. Esto es exactamente lo que deseamos toosee.

Vamos a hacer otro trazado de series de tiempo de hello California lácteos datos toosee grado funciona modelo estacionales Hola. He agregado Hola después el código de hello aprendizaje automático de Azure [ejecutar Script de R] [ execute-r-script] toocreate Hola modelo y realizar un gráfico.

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

Ejecutar este código en aprendizaje automático de Azure genera trazado Hola que se muestra en la figura 24.

![Producción de leche de California con modelo que incluye los efectos de temporada](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

*Ilustración 24. Producción de leche de California con modelo que incluye los efectos de temporada.*

Hello toohello ajuste datos se muestra en la figura 24 son esperanzadores en su lugar. Tendencia de Hola y el efecto de temporada de hello (variación mensual) buscan razonables.

Como otra comprobación en nuestro modelo, echemos un vistazo a los valores residuales Hola. Hello siguiente calcula código Hola valores de predicción de nuestras dos modelos, calcula valores residuales de Hola para modelo estacionales hello y, a continuación, traza estos valores residuales para datos de entrenamiento de Hola.

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

trazado residual Hola se muestra en la figura 25.

![Valores residuales del modelo de temporada de Hola para datos de entrenamiento de Hola](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

*Ilustración 25. Valores residuales del modelo de temporada de Hola para datos de entrenamiento de Hola.*

Estos valores residuales parecen ser razonables. No hay ninguna estructura determinada, excepto el efecto de Hola de recesión Hola 2008 y 2009, que nuestro modelo no tiene en cuenta especialmente bien.

trazado de Hola que se muestra en la figura 25 es útil para detectar los patrones dependientes del tiempo en valores residuales Hola. enfoque explícito de Hola de informática y trazar residuos de hello que he usado coloca valores residuales hello en orden cronológico en el gráfico de Hola. Si, en hello otra parte, había trazada `milk.lm$residuals`, no habría sido trazado hello en orden cronológico.

También puede usar `plot.lm()` tooproduce una serie de gráficos de diagnóstico.

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

Este código genera una serie de trazados de diagnósticos que se muestran en la ilustración 26.

![Primero de los gráficos de diagnóstico para modelo estacionales Hola](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Segundo de los gráficos de diagnóstico para el modelo de temporada de Hola](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Tercera parte de los gráficos de diagnóstico para modelo estacionales Hola](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Cuarta parte de los gráficos de diagnóstico para modelo estacionales Hola](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

*Ilustración 26. Traza de diagnóstico para modelo estacionales Hola.*

Hay unos cuantos puntos altamente influyentes identificados en estos gráficos, pero a nada toocause nos preocupamos por TI. Además, podemos ver de trazado de hello Normal Q-Q que valores residuales Hola son cerrar toonormally distribuida, una suposición importante para los modelos lineales.

### <a name="forecasting-and-model-evaluation"></a>Evaluación del modelo y predicción
Hay solo un toocomplete de toodo algo más en nuestro ejemplo. Se necesitan toocompute previsiones y medir error Hola frente a los datos reales de Hola. Nuestro pronóstico será de hello 12 meses de 2013. Se puede calcular una medida de error para este toohello previsión los datos reales que no forma parte de nuestro conjunto de datos de entrenamiento. Además, se puede comparar el rendimiento en hello 18 años de toohello de datos de entrenamiento 12 meses de datos de prueba.  

Se usa un número de métricas de rendimiento de hello toomeasure de modelos de serie temporal. En nuestro caso utilizamos error cuadrático medio (RMS) de Hola. Hello función siguiente calcula el Hola RMS error entre dos series.  

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

Al igual que con hello `log.transform()` función analizamos en Hola sección "Transformaciones" Value", no hay una gran cantidad de código de recuperación de comprobación y la excepción de error con el de esta función. principios de Hello empleados se Hola mismo. Hello realizan trabajo en dos lugares ajustados en `tryCatch()`. En primer lugar, serie temporal de hello es exponentiated, ya que hemos estado trabajando con registros de Hola de valores de hello. En segundo lugar, se calcula el error de RMS de hello real.  

Equipado con un Hola de toomeasure de la función error de RMS, vamos a compilar y una trama de datos que contienen errores de hello RMS de salida. Se incluye términos Hola tendencia exclusivamente para modelo y el modelo completo de hello con factores estacionales. Hello código siguiente Hola trabajo mediante el uso de modelos lineales dos Hola que se ha construido.

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

Ejecutar este código genera la salida de hello se muestra en la figura 27 en puerto de salida del conjunto de datos de resultado de hello.

![Comparación de errores de RMS para los modelos de Hola][26]

*Ilustración 27. Comparación de errores de RMS para los modelos de Hola.*

En estos resultados, vemos que la adición Hola factores estacionales toohello modelo reduce el error de RMS Hola significativamente. Demasiado Evidentemente, error Hola RMS para los datos de entrenamiento de hello es un poco menor que para hello de previsión.

## <a id="appendixa"></a>Apéndice A: Guía tooRStudio
RStudio está muy bien documentado, por lo que en este apéndice proporcionarán algunos toohello vínculos secciones claves de hello RStudio documentación tooget inició.

1. Creación de proyectos
   
   Puede organizar y administrar el código de R en proyectos mediante RStudio. documentación de Hola que usa proyectos se puede encontrar en https://support.rstudio.com/hc/articles/200526207-Using-Projects.
   
   Recomienda que siga estas instrucciones y crear un proyecto para obtener ejemplos de código de hello R en este documento.  
2. Edición y ejecución de código R
   
   RStudio proporciona un entorno integrado para editar y ejecutar código R. La documentación se encuentra en https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.
3. Depuración
   
   RStudio incluye eficaces capacidades de depuración. Encontrará la documentación de estas características en https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.
   
   características de solución de problemas de punto de interrupción de Hola se documentan en https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.

## <a id="appendixb"></a>APÉNDICE B: lectura adicional
Este tutorial abarca Hola Fundamentos de la programación de R de lo que necesita toouse Hola lenguaje R con estudio de aprendizaje automático de Azure. Si no está familiarizado con el código R, encontrará dos introducciones disponibles en CRAN:

* R para principiantes por Emmanuel Paradis es un toostart ideal en http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.  
* Una visita de introducción por W. N. Venables et. al. profundiza un poco más en la materia. La encontrará en http://cran.r-project.org/doc/manuals/R-intro.html.

Existen muchas obras sobre el código R que pueden servirle como punto de partida. Estas son algunas que considero más útiles:

* Hola carátulas de programación en R: un paseo de estadística diseño de Software por Norman Matloff es un tooprogramming introducción excelente en R.  
* Libro de cocina R por Paul Teetor proporciona un enfoque problema y solución toousing R.  
* R in Action de Robert Kabacoff es otro libro que puede resultarle muy útil. sitio Web de Hello complementaria R rápida es un recurso útil en http://www.statmethods.net/.
* R Inferno por Patrick Burns es un libro sorprendentemente divertido que se ocupa de un número de complicada y difíciles de temas que se pueden encontrar cuando se programan en la libreta de hello r. está disponible de forma gratuita en http://www.burns-stat.com/documents/books/the-r-inferno/.
* Si desea profundización en temas avanzados de R, eche un vistazo a la libreta de hello avanzadas R por Hadley Wickham. Hola versión en línea de este libro está disponible de forma gratuita en http://adv-r.had.co.nz/.

Encontrará un catálogo tiempo serie de paquetes de R en hello CRAN tareas vista para el análisis de series temporales: http://cran.r-project.org/web/views/TimeSeries.html. Para obtener información sobre los paquetes de objeto de serie de tiempo específico, debe hacer referencia a documentación toohello de ese paquete.

Hola guía introductoria serie temporal con R por Paul Cowpertwait y Andrew Metcalfe proporciona una introducción toousing R para análisis de series temporales. No obstante, existen muchos más textos teóricos que proporcionan ejemplos de R.

Algunos recursos excelentes en Internet:

* DataCamp: DataCamp enseña R en comodidad Hola del explorador con vídeo lecciones y ejercicios de codificación. Hay interactivos tutoriales sobre técnicas de R más recientes de Hola y paquetes. Realice el tutorial de R libre interactivo de Hola a https://www.datacamp.com/courses/introduction-to-r
* Una guía de introducción a R de Programiz en https://www.programiz.com/r-programming
* Un tutorial rápido de R Kelly Black de la Universidad de Clarkson: http://www.cyclismo.org/tutorial/R/
* Recopilación de más de 60 recursos de R en http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html

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
