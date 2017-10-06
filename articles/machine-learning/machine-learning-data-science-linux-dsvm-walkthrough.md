---
title: Ciencia aaaData en hello Linux Data Science Virtual Machine | Documentos de Microsoft
description: "Cómo tooperform ciencia de datos común varias tareas con Hola VM de ciencia de datos de Linux."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a>Ciencia de datos en hello Linux Data Science Virtual Machine
Este tutorial muestra cómo tooperform ciencia de datos común varias tareas con hello VM de ciencia de datos de Linux. Hola Máquina Virtual de ciencia de datos de Linux (DSVM) es una imagen de máquina virtual disponible en Azure que viene preinstalado con un conjunto de herramientas usadas para el análisis de datos y aprendizaje automático. componentes de software clave Hola se detallan en hello [Hola aprovisionar Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) tema. Hello imagen de máquina virtual resulta fácil tooget comenzaron a establecer la ciencia de datos en minutos, sin necesidad de tooinstall y configurar cada una de las herramientas de hello individualmente. Fácilmente puede escalar verticalmente Hola de máquina virtual, si es necesario y detenerlo cuando no esté en uso. Así que este recurso es tanto elástico como rentable.

tareas de ciencia de datos mostradas en este tutorial Hello siguen los pasos de hello descritos en hello [proceso de ciencia de datos de equipo](https://azure.microsoft.com/documentation/learning-paths/data-science-process/). Este proceso proporciona una ciencia toodata enfoque sistemático que permite que los equipos de tooeffectively colaborar a través del ciclo de vida de saludo de la creación de aplicaciones inteligentes los científicos de datos. el proceso de ciencia de datos de Hello también proporciona un marco de trabajo iterativo de ciencia de datos que puede ir seguida de un usuario individual.

Analizamos hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) conjunto de datos en este tutorial. Se trata de un conjunto de mensajes de correo electrónico que se marcan como spam o ham (es decir, no son spam), y también contiene estadísticas de contenido de Hola de correos electrónicos de Hola. estadísticas de Hello incluidas se tratan en hello junto pero una sección.

## <a name="prerequisites"></a>Requisitos previos
Para poder usar Linux Data Science Virtual Machine, debe tener el siguiente hello:

* Una **suscripción de Azure**. Si ya tiene una, consulte [Cree su cuenta gratuita de Azure hoy mismo](https://azure.microsoft.com/free/).
* Una [**máquina virtual de ciencia de los datos de Linux**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm). Para obtener información sobre el aprovisionamiento de esta máquina virtual, consulte [Hola aprovisionar Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).
* [X2Go](http://wiki.x2go.org/doku.php) instalado en su equipo y abierta una sesión de XFCE. Para más información sobre la instalación y la configuración de un **cliente X2Go**, consulte [Instalación y configuración del cliente X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client). 
* Una **cuenta de AzureML**. Si aún no tiene, registrarse para obtener uno nuevo en hello [página principal de aprendizaje automático de Azure](https://studio.azureml.net/). Hay un toohelp de nivel de uso libre que empezar a trabajar.

## <a name="download-hello-spambase-dataset"></a>Descargar el conjunto de datos de hello spambase
Hola [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) conjunto de datos es un conjunto de datos que contenga solo 4601 ejemplos relativamente pequeño. Esto resulta un tamaño adecuado toouse que muestra algunas de las principales características de Hola de hello VM de ciencia de datos tal como se mantiene los requisitos de recursos de hello moderado.

> [!NOTE]
> Este tutorial se creó en una máquina virtual Linux Data Science de tamaño D2 v2. Este tamaño DSVM es capaz de controlar los procedimientos de hello en este tutorial.
>
>

Si necesita más espacio de almacenamiento, puede crear discos adicionales y conéctelas tooyour máquina virtual. Estos discos utilizan almacenamiento de Azure persistente, por lo que sus datos se conservan incluso cuando se volverá a aprovisionar el servidor de hello due tooresizing o se apaga. tooadd un disco y adjuntarla tooyour VM, siga las instrucciones de hello en [agregar una VM de Linux de disco tooa](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Estos pasos utiliza Hola interfaz de línea de comandos de Azure (Azure CLI), que ya está instalado en hello DSVM. Por lo que se pueden realizar estos procedimientos completamente desde Hola propia máquina virtual. Otra opción de almacenamiento de tooincrease es toouse [archivos de Azure](../storage/files/storage-how-to-use-files-linux.md).

datos de hello toodownload, abra una ventana de terminal y ejecute este comando:

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

Hola de archivo descargado no tiene una fila de encabezado, así que vamos a crear otro archivo que tiene un encabezado. Ejecute este comando toocreate un archivo con encabezados adecuados de hello:

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

A continuación, concatenar dos archivos de hello junto con el comando hello:

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

conjunto de datos de Hello tiene varios tipos de estadísticas en cada correo electrónico:

* Al igual que las columnas ***word\_frecuencia\_WORD*** indicar el porcentaje de Hola de palabras en correo electrónico de Hola que coinciden con *WORD*. Por ejemplo, si *word\_frecuencia\_realizar* es 1, 1% de todas las palabras en correo electrónico de hello estaban *realizar*.
* Al igual que las columnas ***char\_frecuencia\_CHAR*** indicar Hola porcentaje de todos los caracteres de correo electrónico de Hola que estaban *CHAR*.
* ***capital\_ejecutar\_longitud\_más larga*** es Hola mayor longitud de una secuencia de letras en mayúsculas.
* ***capital\_ejecutar\_longitud\_Media*** es Hola longitud promedio de todas las secuencias de letras en mayúsculas.
* ***capital\_ejecutar\_longitud\_total*** es Hola longitud total de todas las secuencias de letras en mayúsculas.
* ***spam*** indica si correo electrónico Hola se considera spam o no (1 = correo basura, 0 = no correo no deseado).

## <a name="explore-hello-dataset-with-microsoft-r-open"></a>Explorar el conjunto de datos de hello con Microsoft R Open
Vamos a examinar los datos de Hola y realice un aprendizaje de automático básico con r. hello VM de ciencia de datos viene con [Microsoft R Open](https://mran.revolutionanalytics.com/open/) preinstalado. Hello bibliotecas de matemáticas multiproceso en esta versión de R ofrecen un mejor rendimiento que varias versiones de un único subproceso. Microsoft R Open también proporciona reproducción mediante el uso de una instantánea del repositorio de paquetes CRAN Hola.

ejemplos que se usará en este tutorial, Hola de clon de código de tooget copias de hello **Azure Machine Learning datos ciencia** repositorio mediante git, que viene preinstalado en hello máquina virtual. Desde la línea de comandos de git de hello, ejecute:

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

Abra una ventana de terminal e iniciar una nueva sesión de R con consolas interactivas Hola R.

> [!NOTE]
> También puede utilizar RStudio para hello procedimientos siguientes. tooinstall RStudio, ejecute este comando en una terminal:`./Desktop/DSVM\ tools/installRStudio.sh`
>
>

datos de hello tooimport y configurar el entorno de hello, ejecute:

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

toosee estadísticas de resumen acerca de cada columna:

    summary(data)

Para obtener una vista diferente de los datos de hello:

    str(data)

Esto muestra Hola tipo de cada variable y primero Hola pocos valores en el conjunto de datos de Hola.

Hola *spam* columna leyó como un entero, pero es realmente una categoría variable (o fases). tooset su tipo:

    data$spam <- as.factor(data$spam)

toodo algunos análisis de exploración, use hello [ggplot2](http://ggplot2.org/) del paquete, una biblioteca de diagrama popular para R que ya está instalado en hello máquina virtual. Tenga en cuenta, de datos de resumen de hello mostrados anteriormente, que tenemos las estadísticas de resumen de frecuencia de Hola de carácter de signo de admiración Hola. Vamos a trazar las frecuencias aquí con hello siguientes comandos:

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Puesto que la barra de hello cero es sesgar trazado hello, vamos a deshacerse de él:

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Hay una densidad no trivial por encima de 1 que parece interesante. Echemos un vistazo solo a esos datos:

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

A continuación, los vamos a dividir en: es correo no deseado y no es correo no deseado:

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

Estos ejemplos deben permiten toomake gráficos similares de hello otro tooexplore columnas Hola datos contenidos en ellas.

## <a name="train-and-test-an-ml-model"></a>Entrenamiento y prueba de un modelo de Machine Learning
Ahora vamos a un par de aprendizaje automático de entrenar modelos tooclassify correos electrónicos de hello en el conjunto de datos de hello como que contiene uno abarcan o jamón. Hemos entrenado un modelo de árbol de decisiones y un modelo de bosque aleatorio en esta sección y después probaremos su precisión en las predicciones.

> [!NOTE]
> paquete de rpart (partición recursiva y árboles de regresión) Hola utilizado en el siguiente código de hello ya está instalado en hello VM de ciencia de datos.
>
>

En primer lugar, vamos a dividir el conjunto de datos de hello en conjuntos de entrenamiento y prueba:

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

Y, a continuación, cree un Hola de tooclassify del árbol de decisión mensajes de correo electrónico.

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

Éste es el resultado de hello:

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

conjunto de toodetermine grado lleva a cabo en el entrenamiento de hello, usar hello siguiente código:

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

la medida de toodetermine que realiza en el conjunto de pruebas de hello:

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

Vamos a probar un modelo de bosque aleatorio. Bosques aleatorios entrenar un gran número de árboles de decisión y una clase que es el modo de Hola de clasificaciones de Hola de todos los árboles de decisión individuales de Hola de salida. Proporcionan un enfoque de aprendizaje como corrijan para la tendencia de Hola de un toooverfit de modelo de árbol de decisión un conjunto de datos de entrenamiento de automático más eficaz.

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a>Implementar un tooAzure modelo ML
[Estudio de aprendizaje automático de Azure](https://studio.azureml.net/) (AzureML) es un servicio de nube que resulta fácil toobuild e implementa modelos de análisis predictivos. Una de las características de "nice" hello de aprendizaje automático de Azure es su toopublish capacidad cualquier R funcionar como un servicio web. Hola paquete AzureML R hace toodo fácil implementación directamente desde la sesión de R en hello DSVM.

toodeploy el código de árbol de decisión de Hola desde la sección anterior de hello, deberá toosign en tooAzure estudio de aprendizaje automático. Necesita el identificador de área de trabajo y un toosign de token de autorización en. toofind estos valores y variables de aprendizaje automático de Azure de hello inicializar con ellos:

Seleccione **configuración** en el menú izquierdo Hola. Anote su **WORKSPACE ID**(ID DE ÁREA DE TRABAJO). ![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)

Seleccione **Tokens de autorización** de menú de sobrecarga de hello y observe la **el Token de autorización principal**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)

Hola carga **AzureML** del paquete y, a continuación, establecer los valores de variables de Hola por su identificador de área de trabajo y el símbolo (token) en la sesión de R en Hola DSVM:

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


Vamos a simplificar Hola modelo toomake esta tooimplement más fácil de demostración. Elegir Hola tres variables en la raíz de toohello más cercano de árbol de decisión de Hola y crear un nuevo árbol con solo esas tres variables:

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

Se necesita una función de predicción que tiene características de hello como entrada y devuelve Hola valores de predicción:

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

Publicar hello predictSpam función tooAzureML con hello **publishWebService** función:

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

Esta función toma hello **predictSpam** de función, se crea un servicio web denominado **spamWebService** con definen entradas y salidas y devuelve información sobre el nuevo extremo de Hola.

Ver detalles de hello publican servicio web, incluidas sus claves de punto de conexión y acceso de API con el comando hello:

    spamWebService[[2]]

tootry márquelo en Hola 10 primeras filas del conjunto de pruebas de hello:

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a>Uso de otras herramientas disponibles
en las secciones restantes Hola muestran cómo toouse algunas de las herramientas de hello instalado en Hola VM de ciencia de datos de Linux. Esta es Hola lista de herramientas que se describen:

* XGBoost
* Python
* Jupyterhub
* Rattle
* PostgreSQL & Squirrel SQL
* SQL Server Data Warehouse

## <a name="xgboost"></a>XGBoost
[XGBoost](https://xgboost.readthedocs.org/en/latest/) es una herramienta que proporciona una implementación de árbol ampliada rápida y precisa.

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

XGBoost también se puede llamar desde Python o una línea de comandos.

## <a name="python"></a>Python
Para el desarrollo con Python, distribuciones de hello Anaconda Python 2.7 y 3.5 se hayan instalado en hello DSVM.

> [!NOTE]
> incluye Hola distribución de Anaconda [Condas](http://conda.pydata.org/docs/index.html), que puede ser usado toocreate entornos personalizados de Python que tienen diferentes versiones y/o paquetes instalados en ellos.
>
>

Vamos a leer en parte del conjunto de datos de hello spambase y clasificar los correos electrónicos de hello con las máquinas de vectores de soporte técnico en scikit-Obtenga información acerca de:

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

predicciones de toomake:

    clf.predict(X.ix[0:20, :])

tooshow cómo toopublish un punto de conexión de aprendizaje automático de Azure, vamos a hacer un modelo más sencillo Hola tres variables como hicimos cuando se publica el modelo de hello R previamente.

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

toopublish Hola modelo tooAzureML:

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> Esto solo está disponible para Python 2.7 y todavía no se admite en la versión 3.5. Realice la ejecución con **/anaconda/bin/python2.7**.
>
>

## <a name="jupyterhub"></a>Jupyterhub
distribución de Anaconda Hola Hola DSVM incluye Jupyter notebook, un código de Python, R o Julia tooshare entorno multiplataforma y análisis. el Bloc de notas de Hello Jupyter se accede a través de JupyterHub. Para iniciar sesión se usa el nombre de usuario local y la contraseña de Linux en ***https://\<nombre DNS o dirección IP de la máquina virtual\>:8000/***. Todos los archivos de configuración de JupyterHub se encuentran en el directorio **/etc/jupyterhub**.

Varios blocs de notas de ejemplo ya están instalados en hello VM:

* Vea hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) de un bloc de notas de Python de ejemplo.
* Consulte [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) para ver un cuaderno de **R** de ejemplo.
* Vea hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) para obtener otro ejemplo **Python** Bloc de notas.

> [!NOTE]
> Hola lenguaje Julia también está disponible en línea de comandos Hola Hola VM de ciencia de datos de Linux.
>
>

## <a name="rattle"></a>Rattle
[Cascabel](https://cran.r-project.org/web/packages/rattle/index.html) (Hola herramienta analíticos R tooLearn fácilmente) es una herramienta gráfica de R para minería de datos. Tiene una interfaz intuitiva que hace más fácil tooload, explorar y transformar los datos y crear y evaluar modelos.  artículo de Hello [cascabel: GUI de minería de datos A para R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) ofrece un tutorial que muestra sus características.

Instale e inicie sonajero con hello siguientes comandos:

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> No es necesario instalar en hello DSVM. Sin embargo, sonajero puede solicitar paquetes adicionales de tooinstall cuando se carga.
>
>

Rattle usa una interfaz de usuario basada en pestañas. La mayoría de las pestañas de hello corresponden toosteps Hola [proceso de ciencia de datos](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), como la carga de datos o explorándolo. el proceso de ciencia de datos Hola fluye de izquierda tooright a través de las pestañas de Hola. Pero la última ficha que hello contiene un registro de los comandos de hello R ejecutar sonajero.

tooload y configurar el conjunto de datos de hello:

* archivo de hello tooload, seleccione hello **datos** ficha, a continuación,
* Elija selector Hola siguiente demasiado**Filename** y elija **spambaseHeaders.data**.
* archivo de hello tooload. Seleccione **Execute** en la fila superior de Hola de botones. Debería ver un resumen de cada columna, incluidos su tipo de datos identificado, ya sea una entrada, un destino u otro tipo de variable y número de Hola de valores únicos.
* Sonajero ha identificado correctamente hello **spam** columna como destino de Hola. Columna de spam seleccione hello y, a continuación, conjunto hello **tipo de datos de destino** demasiado**Categoric**.

datos de Hola tooexplore:

* Seleccione hello **explorar** ficha.
* Haga clic en **resumen**, a continuación, **Execute**, toosee cierta información sobre los tipos de variable de Hola y algunas estadísticas de resumen.
* tooview otros tipos de estadísticas sobre cada variable, seleccione otras opciones como **describir** o **Fundamentos**.

Hola **explorar** pestaña también le permite toogenerate muchas precisos traza. un histograma de los datos de Hola tooplot:

* Seleccione **Distributions**(Distribuciones).
* Busque en **Histogram** (Histograma) **word_freq_remove** y **word_freq_you**.
* Seleccione **Execute**(Ejecutar). Debería ver que dos densidad de traza en una ventana de gráfico único, donde resulta evidente esa palabra Hola "usted" aparece con mucha más frecuencia en los correos electrónicos de "quitar".

los gráficos de correlación Hello también resultan interesantes. toocreate uno:

* Elija **correlación** como hello **tipo**, a continuación,
* Seleccione **Execute**(Ejecutar).
* Rattle le avisa de que recomienda 40 variables como máximo. Seleccione **Sí** trazado de hello tooview.

Hay algunas correlaciones interesantes que surjan: "la tecnología" fuertemente se correlaciona demasiado "HP" y "laboratorios", por ejemplo. Es también muy correlacionado demasiado "650", porque es de código de área de Hola de donantes de conjunto de datos de hello 650.

valores numéricos de Hola para correlaciones Hola entre las palabras están disponibles en la ventana de exploración de hello. Es interesante toonote, por ejemplo, que "la tecnología" negativamente está correlacionada con "su" y "money".

Sonajero puede transformar Hola dataset toohandle algunos problemas comunes. Por ejemplo, permite características toorescale, imputar valores ausentes, tratar los valores atípicos y quitar variables u observaciones con los datos que faltan. Rattle también puede identificar reglas de asociación entre observaciones o variables. Estas pestañas escapan del ámbito de este tutorial de introducción.

Rattle también puede realizar análisis del clúster. Permite excluir algunos tooread características toomake Hola salida sea más fácil. En hello **datos** ficha, elija **omitir** tooeach siguiente de variables de hello excepto estos diez elementos:

* word_freq_hp
* word_freq_technology
* word_freq_george
* word_freq_remove
* word_freq_your
* word_freq_dollar
* word_freq_money
* capital_run_length_longest
* word_freq_business
* spam

A continuación, regrese toohello **clúster** ficha, elija **KMeans**, conjunto hello y *número de clústeres* too4. A continuación, elija **Execute**(Ejecutar). resultados de Hola se muestran en la ventana de salida de hello. Un clúster tiene alta frecuencia de "george" y "hp" y es probablemente un correo electrónico comercial legítimo.

toobuild un modelo de aprendizaje automático de árbol de decisión simple:

* Seleccione hello **modelo** ficha,
* Elija **árbol** como hello **tipo**.
* Seleccione **Execute** ventana de salida de árbol de hello toodisplay en formato de texto en Hola.
* Seleccione hello **dibujar** botón tooview una versión gráfica. Esto parece muy similar árbol toohello se ha obtenido anteriormente mediante *rpart*.

Una de las características de "nice" hello de sonajero es su toorun capacidad aprendizaje automático de varios métodos y evalúe rápidamente. Éste es el procedimiento de hello:

* Elija **todos los** para hello **tipo**.
* Seleccione **Execute**(Ejecutar).
* Una vez finalizada puede hacer clic en cualquier único **tipo**, como **SVM**y ver los resultados de Hola.
* También puede comparar el rendimiento de Hola de modelos de hello en la validación de hello establecen a través de hello **Evaluate** ficha. Por ejemplo, hello **Error matriz** selección muestra matriz de confusión hello, error general y error de clase promedio de cada modelo en hello validación establecida.
* También puede trazar curvas ROC, realizar análisis de sensibilidad y llevar a cabo otros tipos de evaluaciones de modelos.

Una vez que haya terminado de generar modelos, seleccione hello **registro** pestaña código de hello R tooview ejecutado por sonajero durante la sesión. Puede seleccionar hello **exportar** toosave de botón.

> [!NOTE]
> Hay un error en la versión actual de Rattle. toomodify Hola script o use toorepeat los pasos de una versión posterior, debe insertar un carácter # delante del * exportar este registro... * en texto hello del registro de hello.
>
>

## <a name="postgresql--squirrel-sql"></a>PostgreSQL & Squirrel SQL
Hola DSVM incluye PostgreSQL instalado. PostgreSQL es una base de datos relacional sofisticada de código abierto. Esta sección se muestra cómo tooload nuestro conjunto de datos de correo no deseado en PostgreSQL y, a continuación, realizar consultas sobre él.

Antes de poder cargar los datos de hello, necesita la autenticación de contraseña de tooallow desde el host local de Hola. En un símbolo del sistema:

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

Final Hola del archivo de configuración de hello son varias líneas donde se detallan Hola conexiones permitida:

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

Cambiar Hola "Las conexiones locales de IPv4" línea toouse md5 en lugar de ident, por lo que se puede iniciar sesión con un nombre de usuario y una contraseña:

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

Y reinicie el servicio de hello postgres:

    sudo systemctl restart postgresql

toolaunch psql, un terminal interactivo para PostgreSQL, como usuario de hello postgres integrados, ejecute hello siguiente comando desde un símbolo del sistema:

    sudo -u postgres psql

Crear una nueva cuenta de usuario, mediante Hola el mismo nombre de usuario como Hola cuenta Linux actualmente inició sesión como y asígnele una contraseña:

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

A continuación, inicie sesión en toopsql como el usuario:

    psql

E importar datos de hello en una base de datos:

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

Ahora, vamos a explorar los datos de Hola y ejecute algunas consultas mediante **ardilla SQL**, una herramienta gráfica que le permite interactuar con bases de datos a través de un controlador JDBC.

tooget iniciado, inicie SQL ardilla desde el menú "Applications" Hola. tooset controlador hello:

* Seleccione **Windows** y luego **View Drivers** (Ver controladores).
* Haga clic con el botón derecho en **PostgreSQL** y seleccione **Modify Driver** (Modificar controlador).
* Seleccione **Extra Class Path** (Ruta de clase adicional) y luego **Add** (Agregar).
* Escriba ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** para hello **nombre de archivo** y
* seleccione **Open**(Abrir).
* Elija List Drivers (Mostrar controladores) y seleccione **org.postgresql.Driver** en **Class Name** (Nombre de clase), a continuación, seleccione **OK** (Aceptar).

tooset de servidor local de hello conexión toohello:

* Seleccione **Windows** y luego **View Aliases** (Ver alias).
* Elija hello  **+**  toomake botón un nuevo alias.
* Asígnele el nombre *base de datos de Spam*, elija **PostgreSQL** en hello **controlador** lista desplegable.
* Establecer la dirección URL de hello demasiado*jdbc:postgresql://localhost/spam*.
* Escriba su *nombre de usuario* y *contraseña*.
* Haga clic en **Aceptar**.
* Hola tooopen **conexión** ventana, haga doble clic en hello ***base de datos de Spam*** alias.
* Seleccione **Conectar**.

toorun algunas consultas:

* Seleccione hello **SQL** ficha.
* Escriba una consulta sencilla como `SELECT * from data;` en cuadro de texto de consulta de hello en parte superior de Hola de pestaña de hello SQL.
* Presione **Ctrl-Entrar** toorun lo. De forma predeterminada ardilla SQL devuelve Hola 100 primeras filas de la consulta.

Hay muchas consultas más que podría ejecutar tooexplore estos datos. Por ejemplo, ¿cómo Hola frecuencia de la palabra Hola *realizar* difieren entre correo no deseado y ham?

    SELECT avg(word_freq_make), spam from data group by spam;

O ¿cuáles son las características de saludo de correo electrónico que suelen contengan *3d*?

    SELECT * from data order by word_freq_3d desc;

La mayoría de correos electrónicos que tienen una repetición de alta *3d* son aparentemente correo no deseado, por lo que podría ser una característica útil para la creación de un saludo de tooclassify modelo predictivo mensajes de correo electrónico.

Si deseara aprendizaje automático de tooperform con datos almacenados en una base de datos PostgreSQL, considere el uso de [MADlib](http://madlib.incubator.apache.org/).

## <a name="sql-server-data-warehouse"></a>SQL Server Data Warehouse
Almacenamiento de datos SQL de Azure es una base de datos de escalado horizontal y basada en la nube capaz de procesar volúmenes masivos de datos (tanto relacionales como no relacionales). Para más información, consulte [¿Qué es Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)

tooconnect toohello datos de almacenamiento y crean tabla de hello, siguiente ejecución Hola comando desde un símbolo del sistema:

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

A continuación, en el símbolo del sistema de hello sqlcmd:

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

Copie los datos con bcp:

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> fin de línea de Hello en el archivo descargado Hola es basado en Windows, pero bcp espera estilo UNIX, por lo que necesitamos bcp tootell que con Hola marca - r.
>
>

Y la consulta con sqlcmd:

    select top 10 spam, char_freq_dollar from spam;
    GO

También puede consultar con Squirrel SQL. Seguir pasos similares para PostgreSQL, usando Hola controlador JDBC de Microsoft MSSQL Server, lo que puede encontrarse en ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.

## <a name="next-steps"></a>Pasos siguientes
Para obtener información general de temas que le guiarán por tareas de Hola que componen el proceso de ciencia de datos de hello en Azure, consulte [proceso de ciencia de datos de equipo](http://aka.ms/datascienceprocess).

Para obtener una descripción de los otros tutoriales to-end que muestran los pasos de Hola Hola proceso de ciencia de datos de equipo para escenarios específicos, consulte [tutoriales de proceso de ciencia de datos de equipo](data-science-process-walkthroughs.md). Hola tutoriales también muestran el funcionamiento de cloud toocombine y herramientas local y servicios en un flujo de trabajo o canalización toocreate una aplicación inteligente.
