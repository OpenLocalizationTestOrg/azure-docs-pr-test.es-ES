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
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a><span data-ttu-id="8768b-103">Ciencia de datos en hello Linux Data Science Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="8768b-103">Data science on hello Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="8768b-104">Este tutorial muestra cómo tooperform ciencia de datos común varias tareas con hello VM de ciencia de datos de Linux.</span><span class="sxs-lookup"><span data-stu-id="8768b-104">This walkthrough shows you how tooperform several common data science tasks with hello Linux Data Science VM.</span></span> <span data-ttu-id="8768b-105">Hola Máquina Virtual de ciencia de datos de Linux (DSVM) es una imagen de máquina virtual disponible en Azure que viene preinstalado con un conjunto de herramientas usadas para el análisis de datos y aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="8768b-105">hello Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="8768b-106">componentes de software clave Hola se detallan en hello [Hola aprovisionar Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) tema.</span><span class="sxs-lookup"><span data-stu-id="8768b-106">hello key software components are itemized in hello [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="8768b-107">Hello imagen de máquina virtual resulta fácil tooget comenzaron a establecer la ciencia de datos en minutos, sin necesidad de tooinstall y configurar cada una de las herramientas de hello individualmente.</span><span class="sxs-lookup"><span data-stu-id="8768b-107">hello VM image makes it easy tooget started doing data science in minutes, without having tooinstall and configure each of hello tools individually.</span></span> <span data-ttu-id="8768b-108">Fácilmente puede escalar verticalmente Hola de máquina virtual, si es necesario y detenerlo cuando no esté en uso.</span><span class="sxs-lookup"><span data-stu-id="8768b-108">You can easily scale up hello VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="8768b-109">Así que este recurso es tanto elástico como rentable.</span><span class="sxs-lookup"><span data-stu-id="8768b-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="8768b-110">tareas de ciencia de datos mostradas en este tutorial Hello siguen los pasos de hello descritos en hello [proceso de ciencia de datos de equipo](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span><span class="sxs-lookup"><span data-stu-id="8768b-110">hello data science tasks demonstrated in this walkthrough follow hello steps outlined in hello [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="8768b-111">Este proceso proporciona una ciencia toodata enfoque sistemático que permite que los equipos de tooeffectively colaborar a través del ciclo de vida de saludo de la creación de aplicaciones inteligentes los científicos de datos.</span><span class="sxs-lookup"><span data-stu-id="8768b-111">This process provides a systematic approach toodata science that enables teams of data scientists tooeffectively collaborate over hello lifecycle of building intelligent applications.</span></span> <span data-ttu-id="8768b-112">el proceso de ciencia de datos de Hello también proporciona un marco de trabajo iterativo de ciencia de datos que puede ir seguida de un usuario individual.</span><span class="sxs-lookup"><span data-stu-id="8768b-112">hello data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="8768b-113">Analizamos hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) conjunto de datos en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8768b-113">We analyze hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="8768b-114">Se trata de un conjunto de mensajes de correo electrónico que se marcan como spam o ham (es decir, no son spam), y también contiene estadísticas de contenido de Hola de correos electrónicos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8768b-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on hello content of hello emails.</span></span> <span data-ttu-id="8768b-115">estadísticas de Hello incluidas se tratan en hello junto pero una sección.</span><span class="sxs-lookup"><span data-stu-id="8768b-115">hello statistics included are discussed in hello next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8768b-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8768b-116">Prerequisites</span></span>
<span data-ttu-id="8768b-117">Para poder usar Linux Data Science Virtual Machine, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="8768b-117">Before you can use a Linux Data Science Virtual Machine, you must have hello following:</span></span>

* <span data-ttu-id="8768b-118">Una **suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="8768b-118">An **Azure subscription**.</span></span> <span data-ttu-id="8768b-119">Si ya tiene una, consulte [Cree su cuenta gratuita de Azure hoy mismo](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="8768b-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="8768b-120">Una [**máquina virtual de ciencia de los datos de Linux**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="8768b-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="8768b-121">Para obtener información sobre el aprovisionamiento de esta máquina virtual, consulte [Hola aprovisionar Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span><span class="sxs-lookup"><span data-stu-id="8768b-121">For information on provisioning this VM, see [Provision hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="8768b-122">[X2Go](http://wiki.x2go.org/doku.php) instalado en su equipo y abierta una sesión de XFCE.</span><span class="sxs-lookup"><span data-stu-id="8768b-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="8768b-123">Para más información sobre la instalación y la configuración de un **cliente X2Go**, consulte [Instalación y configuración del cliente X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span><span class="sxs-lookup"><span data-stu-id="8768b-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="8768b-124">Una **cuenta de AzureML**.</span><span class="sxs-lookup"><span data-stu-id="8768b-124">An **AzureML account**.</span></span> <span data-ttu-id="8768b-125">Si aún no tiene, registrarse para obtener uno nuevo en hello [página principal de aprendizaje automático de Azure](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="8768b-125">If you don't already have one, sign up for new one at hello [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="8768b-126">Hay un toohelp de nivel de uso libre que empezar a trabajar.</span><span class="sxs-lookup"><span data-stu-id="8768b-126">There is a free usage tier toohelp you get started.</span></span>

## <a name="download-hello-spambase-dataset"></a><span data-ttu-id="8768b-127">Descargar el conjunto de datos de hello spambase</span><span class="sxs-lookup"><span data-stu-id="8768b-127">Download hello spambase dataset</span></span>
<span data-ttu-id="8768b-128">Hola [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) conjunto de datos es un conjunto de datos que contenga solo 4601 ejemplos relativamente pequeño.</span><span class="sxs-lookup"><span data-stu-id="8768b-128">hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="8768b-129">Esto resulta un tamaño adecuado toouse que muestra algunas de las principales características de Hola de hello VM de ciencia de datos tal como se mantiene los requisitos de recursos de hello moderado.</span><span class="sxs-lookup"><span data-stu-id="8768b-129">This is a convenient size toouse when demonstrating that some of hello key features of hello Data Science VM as it keeps hello resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="8768b-130">Este tutorial se creó en una máquina virtual Linux Data Science de tamaño D2 v2.</span><span class="sxs-lookup"><span data-stu-id="8768b-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="8768b-131">Este tamaño DSVM es capaz de controlar los procedimientos de hello en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8768b-131">This size DSVM is capable of handling hello procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="8768b-132">Si necesita más espacio de almacenamiento, puede crear discos adicionales y conéctelas tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8768b-132">If you need more storage space, you can create additional disks and attach them tooyour VM.</span></span> <span data-ttu-id="8768b-133">Estos discos utilizan almacenamiento de Azure persistente, por lo que sus datos se conservan incluso cuando se volverá a aprovisionar el servidor de hello due tooresizing o se apaga.</span><span class="sxs-lookup"><span data-stu-id="8768b-133">These disks use persistent Azure storage, so their data is preserved even when hello server is reprovisioned due tooresizing or is shut down.</span></span> <span data-ttu-id="8768b-134">tooadd un disco y adjuntarla tooyour VM, siga las instrucciones de hello en [agregar una VM de Linux de disco tooa](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8768b-134">tooadd a disk and attach it tooyour VM, follow hello instructions in [Add a disk tooa Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="8768b-135">Estos pasos utiliza Hola interfaz de línea de comandos de Azure (Azure CLI), que ya está instalado en hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="8768b-135">These steps use hello Azure Command-Line Interface (Azure CLI), which is already installed on hello DSVM.</span></span> <span data-ttu-id="8768b-136">Por lo que se pueden realizar estos procedimientos completamente desde Hola propia máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8768b-136">So these procedures can be done entirely from hello VM itself.</span></span> <span data-ttu-id="8768b-137">Otra opción de almacenamiento de tooincrease es toouse [archivos de Azure](../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8768b-137">Another option tooincrease storage is toouse [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="8768b-138">datos de hello toodownload, abra una ventana de terminal y ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="8768b-138">toodownload hello data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="8768b-139">Hola de archivo descargado no tiene una fila de encabezado, así que vamos a crear otro archivo que tiene un encabezado.</span><span class="sxs-lookup"><span data-stu-id="8768b-139">hello downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="8768b-140">Ejecute este comando toocreate un archivo con encabezados adecuados de hello:</span><span class="sxs-lookup"><span data-stu-id="8768b-140">Run this command toocreate a file with hello appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="8768b-141">A continuación, concatenar dos archivos de hello junto con el comando hello:</span><span class="sxs-lookup"><span data-stu-id="8768b-141">Then concatenate hello two files together with hello command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="8768b-142">conjunto de datos de Hello tiene varios tipos de estadísticas en cada correo electrónico:</span><span class="sxs-lookup"><span data-stu-id="8768b-142">hello dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="8768b-143">Al igual que las columnas ***word\_frecuencia\_WORD*** indicar el porcentaje de Hola de palabras en correo electrónico de Hola que coinciden con *WORD*.</span><span class="sxs-lookup"><span data-stu-id="8768b-143">Columns like ***word\_freq\_WORD*** indicate hello percentage of words in hello email that match *WORD*.</span></span> <span data-ttu-id="8768b-144">Por ejemplo, si *word\_frecuencia\_realizar* es 1, 1% de todas las palabras en correo electrónico de hello estaban *realizar*.</span><span class="sxs-lookup"><span data-stu-id="8768b-144">For example, if *word\_freq\_make* is 1, then 1% of all words in hello email were *make*.</span></span>
* <span data-ttu-id="8768b-145">Al igual que las columnas ***char\_frecuencia\_CHAR*** indicar Hola porcentaje de todos los caracteres de correo electrónico de Hola que estaban *CHAR*.</span><span class="sxs-lookup"><span data-stu-id="8768b-145">Columns like ***char\_freq\_CHAR*** indicate hello percentage of all characters in hello email that were *CHAR*.</span></span>
* <span data-ttu-id="8768b-146">***capital\_ejecutar\_longitud\_más larga*** es Hola mayor longitud de una secuencia de letras en mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="8768b-146">***capital\_run\_length\_longest*** is hello longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="8768b-147">***capital\_ejecutar\_longitud\_Media*** es Hola longitud promedio de todas las secuencias de letras en mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="8768b-147">***capital\_run\_length\_average*** is hello average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="8768b-148">***capital\_ejecutar\_longitud\_total*** es Hola longitud total de todas las secuencias de letras en mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="8768b-148">***capital\_run\_length\_total*** is hello total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="8768b-149">***spam*** indica si correo electrónico Hola se considera spam o no (1 = correo basura, 0 = no correo no deseado).</span><span class="sxs-lookup"><span data-stu-id="8768b-149">***spam*** indicates whether hello email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-hello-dataset-with-microsoft-r-open"></a><span data-ttu-id="8768b-150">Explorar el conjunto de datos de hello con Microsoft R Open</span><span class="sxs-lookup"><span data-stu-id="8768b-150">Explore hello dataset with Microsoft R Open</span></span>
<span data-ttu-id="8768b-151">Vamos a examinar los datos de Hola y realice un aprendizaje de automático básico con r. hello VM de ciencia de datos viene con [Microsoft R Open](https://mran.revolutionanalytics.com/open/) preinstalado.</span><span class="sxs-lookup"><span data-stu-id="8768b-151">Let's examine hello data and do some basic machine learning with R. hello Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="8768b-152">Hello bibliotecas de matemáticas multiproceso en esta versión de R ofrecen un mejor rendimiento que varias versiones de un único subproceso.</span><span class="sxs-lookup"><span data-stu-id="8768b-152">hello multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="8768b-153">Microsoft R Open también proporciona reproducción mediante el uso de una instantánea del repositorio de paquetes CRAN Hola.</span><span class="sxs-lookup"><span data-stu-id="8768b-153">Microsoft R Open also provides reproducibility by using a snapshot of hello CRAN package repository.</span></span>

<span data-ttu-id="8768b-154">ejemplos que se usará en este tutorial, Hola de clon de código de tooget copias de hello **Azure Machine Learning datos ciencia** repositorio mediante git, que viene preinstalado en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8768b-154">tooget copies of hello code samples used in this walkthrough, clone hello **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on hello VM.</span></span> <span data-ttu-id="8768b-155">Desde la línea de comandos de git de hello, ejecute:</span><span class="sxs-lookup"><span data-stu-id="8768b-155">From hello git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="8768b-156">Abra una ventana de terminal e iniciar una nueva sesión de R con consolas interactivas Hola R.</span><span class="sxs-lookup"><span data-stu-id="8768b-156">Open a terminal window and start a new R session with hello R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="8768b-157">También puede utilizar RStudio para hello procedimientos siguientes.</span><span class="sxs-lookup"><span data-stu-id="8768b-157">You can also use RStudio for hello following procedures.</span></span> <span data-ttu-id="8768b-158">tooinstall RStudio, ejecute este comando en una terminal:`./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="8768b-158">tooinstall RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="8768b-159">datos de hello tooimport y configurar el entorno de hello, ejecute:</span><span class="sxs-lookup"><span data-stu-id="8768b-159">tooimport hello data and set up hello environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="8768b-160">toosee estadísticas de resumen acerca de cada columna:</span><span class="sxs-lookup"><span data-stu-id="8768b-160">toosee summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="8768b-161">Para obtener una vista diferente de los datos de hello:</span><span class="sxs-lookup"><span data-stu-id="8768b-161">For a different view of hello data:</span></span>

    str(data)

<span data-ttu-id="8768b-162">Esto muestra Hola tipo de cada variable y primero Hola pocos valores en el conjunto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8768b-162">This shows you hello type of each variable and hello first few values in hello dataset.</span></span>

<span data-ttu-id="8768b-163">Hola *spam* columna leyó como un entero, pero es realmente una categoría variable (o fases).</span><span class="sxs-lookup"><span data-stu-id="8768b-163">hello *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="8768b-164">tooset su tipo:</span><span class="sxs-lookup"><span data-stu-id="8768b-164">tooset its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="8768b-165">toodo algunos análisis de exploración, use hello [ggplot2](http://ggplot2.org/) del paquete, una biblioteca de diagrama popular para R que ya está instalado en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8768b-165">toodo some exploratory analysis, use hello [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on hello VM.</span></span> <span data-ttu-id="8768b-166">Tenga en cuenta, de datos de resumen de hello mostrados anteriormente, que tenemos las estadísticas de resumen de frecuencia de Hola de carácter de signo de admiración Hola.</span><span class="sxs-lookup"><span data-stu-id="8768b-166">Note, from hello summary data displayed earlier, that we have summary statistics on hello frequency of hello exclamation mark character.</span></span> <span data-ttu-id="8768b-167">Vamos a trazar las frecuencias aquí con hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="8768b-167">Let's plot those frequencies here with hello following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="8768b-168">Puesto que la barra de hello cero es sesgar trazado hello, vamos a deshacerse de él:</span><span class="sxs-lookup"><span data-stu-id="8768b-168">Since hello zero bar is skewing hello plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="8768b-169">Hay una densidad no trivial por encima de 1 que parece interesante.</span><span class="sxs-lookup"><span data-stu-id="8768b-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="8768b-170">Echemos un vistazo solo a esos datos:</span><span class="sxs-lookup"><span data-stu-id="8768b-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="8768b-171">A continuación, los vamos a dividir en: es correo no deseado y no es correo no deseado:</span><span class="sxs-lookup"><span data-stu-id="8768b-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="8768b-172">Estos ejemplos deben permiten toomake gráficos similares de hello otro tooexplore columnas Hola datos contenidos en ellas.</span><span class="sxs-lookup"><span data-stu-id="8768b-172">These examples should enable you toomake similar plots of hello other columns tooexplore hello data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="8768b-173">Entrenamiento y prueba de un modelo de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8768b-173">Train and test an ML model</span></span>
<span data-ttu-id="8768b-174">Ahora vamos a un par de aprendizaje automático de entrenar modelos tooclassify correos electrónicos de hello en el conjunto de datos de hello como que contiene uno abarcan o jamón.</span><span class="sxs-lookup"><span data-stu-id="8768b-174">Now let's train a couple of machine learning models tooclassify hello emails in hello dataset as containing either span or ham.</span></span> <span data-ttu-id="8768b-175">Hemos entrenado un modelo de árbol de decisiones y un modelo de bosque aleatorio en esta sección y después probaremos su precisión en las predicciones.</span><span class="sxs-lookup"><span data-stu-id="8768b-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="8768b-176">paquete de rpart (partición recursiva y árboles de regresión) Hola utilizado en el siguiente código de hello ya está instalado en hello VM de ciencia de datos.</span><span class="sxs-lookup"><span data-stu-id="8768b-176">hello rpart (Recursive Partitioning and Regression Trees) package used in hello following code is already installed on hello Data Science VM.</span></span>
>
>

<span data-ttu-id="8768b-177">En primer lugar, vamos a dividir el conjunto de datos de hello en conjuntos de entrenamiento y prueba:</span><span class="sxs-lookup"><span data-stu-id="8768b-177">First, let's split hello dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="8768b-178">Y, a continuación, cree un Hola de tooclassify del árbol de decisión mensajes de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="8768b-178">And then create a decision tree tooclassify hello emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="8768b-179">Éste es el resultado de hello:</span><span class="sxs-lookup"><span data-stu-id="8768b-179">Here is hello result:</span></span>

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="8768b-181">conjunto de toodetermine grado lleva a cabo en el entrenamiento de hello, usar hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="8768b-181">toodetermine how well it performs on hello training set, use hello following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="8768b-182">la medida de toodetermine que realiza en el conjunto de pruebas de hello:</span><span class="sxs-lookup"><span data-stu-id="8768b-182">toodetermine how well it performs on hello test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="8768b-183">Vamos a probar un modelo de bosque aleatorio.</span><span class="sxs-lookup"><span data-stu-id="8768b-183">Let's also try a random forest model.</span></span> <span data-ttu-id="8768b-184">Bosques aleatorios entrenar un gran número de árboles de decisión y una clase que es el modo de Hola de clasificaciones de Hola de todos los árboles de decisión individuales de Hola de salida.</span><span class="sxs-lookup"><span data-stu-id="8768b-184">Random forests train a multitude of decision trees and output a class that is hello mode of hello classifications from all of hello individual decision trees.</span></span> <span data-ttu-id="8768b-185">Proporcionan un enfoque de aprendizaje como corrijan para la tendencia de Hola de un toooverfit de modelo de árbol de decisión un conjunto de datos de entrenamiento de automático más eficaz.</span><span class="sxs-lookup"><span data-stu-id="8768b-185">They provide a more powerful machine learning approach as they correct for hello tendency of a decision tree model toooverfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a><span data-ttu-id="8768b-186">Implementar un tooAzure modelo ML</span><span class="sxs-lookup"><span data-stu-id="8768b-186">Deploy a model tooAzure ML</span></span>
<span data-ttu-id="8768b-187">[Estudio de aprendizaje automático de Azure](https://studio.azureml.net/) (AzureML) es un servicio de nube que resulta fácil toobuild e implementa modelos de análisis predictivos.</span><span class="sxs-lookup"><span data-stu-id="8768b-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy toobuild and deploy predictive analytics models.</span></span> <span data-ttu-id="8768b-188">Una de las características de "nice" hello de aprendizaje automático de Azure es su toopublish capacidad cualquier R funcionar como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="8768b-188">One of hello nice features of AzureML is its ability toopublish any R function as a web service.</span></span> <span data-ttu-id="8768b-189">Hola paquete AzureML R hace toodo fácil implementación directamente desde la sesión de R en hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="8768b-189">hello AzureML R package makes deployment easy toodo right from our R session on hello DSVM.</span></span>

<span data-ttu-id="8768b-190">toodeploy el código de árbol de decisión de Hola desde la sección anterior de hello, deberá toosign en tooAzure estudio de aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="8768b-190">toodeploy hello decision tree code from hello previous section, you need toosign in tooAzure Machine Learning Studio.</span></span> <span data-ttu-id="8768b-191">Necesita el identificador de área de trabajo y un toosign de token de autorización en.</span><span class="sxs-lookup"><span data-stu-id="8768b-191">You need your workspace ID and an authorization token toosign in.</span></span> <span data-ttu-id="8768b-192">toofind estos valores y variables de aprendizaje automático de Azure de hello inicializar con ellos:</span><span class="sxs-lookup"><span data-stu-id="8768b-192">toofind these values and initialize hello AzureML variables with them:</span></span>

<span data-ttu-id="8768b-193">Seleccione **configuración** en el menú izquierdo Hola.</span><span class="sxs-lookup"><span data-stu-id="8768b-193">Select **Settings** on hello left-hand menu.</span></span> <span data-ttu-id="8768b-194">Anote su **WORKSPACE ID**(ID DE ÁREA DE TRABAJO).</span><span class="sxs-lookup"><span data-stu-id="8768b-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="8768b-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="8768b-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="8768b-196">Seleccione **Tokens de autorización** de menú de sobrecarga de hello y observe la **el Token de autorización principal**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="8768b-196">Select **Authorization Tokens** from hello overhead menu and note your **Primary Authorization Token**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="8768b-197">Hola carga **AzureML** del paquete y, a continuación, establecer los valores de variables de Hola por su identificador de área de trabajo y el símbolo (token) en la sesión de R en Hola DSVM:</span><span class="sxs-lookup"><span data-stu-id="8768b-197">Load hello **AzureML** package and then set values of hello variables with your token and workspace ID in your R session on hello DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="8768b-198">Vamos a simplificar Hola modelo toomake esta tooimplement más fácil de demostración.</span><span class="sxs-lookup"><span data-stu-id="8768b-198">Let's simplify hello model toomake this demonstration easier tooimplement.</span></span> <span data-ttu-id="8768b-199">Elegir Hola tres variables en la raíz de toohello más cercano de árbol de decisión de Hola y crear un nuevo árbol con solo esas tres variables:</span><span class="sxs-lookup"><span data-stu-id="8768b-199">Pick hello three variables in hello decision tree closest toohello root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="8768b-200">Se necesita una función de predicción que tiene características de hello como entrada y devuelve Hola valores de predicción:</span><span class="sxs-lookup"><span data-stu-id="8768b-200">We need a prediction function that takes hello features as an input and returns hello predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="8768b-201">Publicar hello predictSpam función tooAzureML con hello **publishWebService** función:</span><span class="sxs-lookup"><span data-stu-id="8768b-201">Publish hello predictSpam function tooAzureML using hello **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="8768b-202">Esta función toma hello **predictSpam** de función, se crea un servicio web denominado **spamWebService** con definen entradas y salidas y devuelve información sobre el nuevo extremo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8768b-202">This function takes hello **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about hello new endpoint.</span></span>

<span data-ttu-id="8768b-203">Ver detalles de hello publican servicio web, incluidas sus claves de punto de conexión y acceso de API con el comando hello:</span><span class="sxs-lookup"><span data-stu-id="8768b-203">View details of hello published web service, including its API endpoint and access keys with hello command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="8768b-204">tootry márquelo en Hola 10 primeras filas del conjunto de pruebas de hello:</span><span class="sxs-lookup"><span data-stu-id="8768b-204">tootry it out on hello first 10 rows of hello test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="8768b-205">Uso de otras herramientas disponibles</span><span class="sxs-lookup"><span data-stu-id="8768b-205">Use other tools available</span></span>
<span data-ttu-id="8768b-206">en las secciones restantes Hola muestran cómo toouse algunas de las herramientas de hello instalado en Hola VM de ciencia de datos de Linux. Esta es Hola lista de herramientas que se describen:</span><span class="sxs-lookup"><span data-stu-id="8768b-206">hello remaining sections show how toouse some of hello tools installed on hello Linux Data Science VM.Here is hello list of tools discussed:</span></span>

* <span data-ttu-id="8768b-207">XGBoost</span><span class="sxs-lookup"><span data-stu-id="8768b-207">XGBoost</span></span>
* <span data-ttu-id="8768b-208">Python</span><span class="sxs-lookup"><span data-stu-id="8768b-208">Python</span></span>
* <span data-ttu-id="8768b-209">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="8768b-209">Jupyterhub</span></span>
* <span data-ttu-id="8768b-210">Rattle</span><span class="sxs-lookup"><span data-stu-id="8768b-210">Rattle</span></span>
* <span data-ttu-id="8768b-211">PostgreSQL & Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="8768b-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="8768b-212">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8768b-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="8768b-213">XGBoost</span><span class="sxs-lookup"><span data-stu-id="8768b-213">XGBoost</span></span>
<span data-ttu-id="8768b-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) es una herramienta que proporciona una implementación de árbol ampliada rápida y precisa.</span><span class="sxs-lookup"><span data-stu-id="8768b-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

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

<span data-ttu-id="8768b-215">XGBoost también se puede llamar desde Python o una línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="8768b-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="8768b-216">Python</span><span class="sxs-lookup"><span data-stu-id="8768b-216">Python</span></span>
<span data-ttu-id="8768b-217">Para el desarrollo con Python, distribuciones de hello Anaconda Python 2.7 y 3.5 se hayan instalado en hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="8768b-217">For development using Python, hello Anaconda Python distributions 2.7 and 3.5 have been installed in hello DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="8768b-218">incluye Hola distribución de Anaconda [Condas](http://conda.pydata.org/docs/index.html), que puede ser usado toocreate entornos personalizados de Python que tienen diferentes versiones y/o paquetes instalados en ellos.</span><span class="sxs-lookup"><span data-stu-id="8768b-218">hello Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used toocreate custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="8768b-219">Vamos a leer en parte del conjunto de datos de hello spambase y clasificar los correos electrónicos de hello con las máquinas de vectores de soporte técnico en scikit-Obtenga información acerca de:</span><span class="sxs-lookup"><span data-stu-id="8768b-219">Let's read in some of hello spambase dataset and classify hello emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="8768b-220">predicciones de toomake:</span><span class="sxs-lookup"><span data-stu-id="8768b-220">toomake predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="8768b-221">tooshow cómo toopublish un punto de conexión de aprendizaje automático de Azure, vamos a hacer un modelo más sencillo Hola tres variables como hicimos cuando se publica el modelo de hello R previamente.</span><span class="sxs-lookup"><span data-stu-id="8768b-221">tooshow how toopublish an AzureML endpoint, let's make a simpler model hello three variables as we did when we published hello R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="8768b-222">toopublish Hola modelo tooAzureML:</span><span class="sxs-lookup"><span data-stu-id="8768b-222">toopublish hello model tooAzureML:</span></span>

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
> <span data-ttu-id="8768b-223">Esto solo está disponible para Python 2.7 y todavía no se admite en la versión 3.5.</span><span class="sxs-lookup"><span data-stu-id="8768b-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="8768b-224">Realice la ejecución con **/anaconda/bin/python2.7**.</span><span class="sxs-lookup"><span data-stu-id="8768b-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="8768b-225">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="8768b-225">Jupyterhub</span></span>
<span data-ttu-id="8768b-226">distribución de Anaconda Hola Hola DSVM incluye Jupyter notebook, un código de Python, R o Julia tooshare entorno multiplataforma y análisis.</span><span class="sxs-lookup"><span data-stu-id="8768b-226">hello Anaconda distribution in hello DSVM comes with a Jupyter notebook, a cross-platform environment tooshare Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="8768b-227">el Bloc de notas de Hello Jupyter se accede a través de JupyterHub.</span><span class="sxs-lookup"><span data-stu-id="8768b-227">hello Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="8768b-228">Para iniciar sesión se usa el nombre de usuario local y la contraseña de Linux en ***https://\<nombre DNS o dirección IP de la máquina virtual\>:8000/***.</span><span class="sxs-lookup"><span data-stu-id="8768b-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="8768b-229">Todos los archivos de configuración de JupyterHub se encuentran en el directorio **/etc/jupyterhub**.</span><span class="sxs-lookup"><span data-stu-id="8768b-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="8768b-230">Varios blocs de notas de ejemplo ya están instalados en hello VM:</span><span class="sxs-lookup"><span data-stu-id="8768b-230">Several sample notebooks are already installed on hello VM:</span></span>

* <span data-ttu-id="8768b-231">Vea hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) de un bloc de notas de Python de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8768b-231">See hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="8768b-232">Consulte [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) para ver un cuaderno de **R** de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8768b-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="8768b-233">Vea hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) para obtener otro ejemplo **Python** Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="8768b-233">See hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="8768b-234">Hola lenguaje Julia también está disponible en línea de comandos Hola Hola VM de ciencia de datos de Linux.</span><span class="sxs-lookup"><span data-stu-id="8768b-234">hello Julia language is also available from hello command line on hello Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="8768b-235">Rattle</span><span class="sxs-lookup"><span data-stu-id="8768b-235">Rattle</span></span>
<span data-ttu-id="8768b-236">[Cascabel](https://cran.r-project.org/web/packages/rattle/index.html) (Hola herramienta analíticos R tooLearn fácilmente) es una herramienta gráfica de R para minería de datos.</span><span class="sxs-lookup"><span data-stu-id="8768b-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (hello R Analytical Tool tooLearn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="8768b-237">Tiene una interfaz intuitiva que hace más fácil tooload, explorar y transformar los datos y crear y evaluar modelos.</span><span class="sxs-lookup"><span data-stu-id="8768b-237">It has an intuitive interface that makes it easy tooload, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="8768b-238">artículo de Hello [cascabel: GUI de minería de datos A para R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) ofrece un tutorial que muestra sus características.</span><span class="sxs-lookup"><span data-stu-id="8768b-238">hello article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="8768b-239">Instale e inicie sonajero con hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="8768b-239">Install and start Rattle with hello following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="8768b-240">No es necesario instalar en hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="8768b-240">Installation is not required on hello DSVM.</span></span> <span data-ttu-id="8768b-241">Sin embargo, sonajero puede solicitar paquetes adicionales de tooinstall cuando se carga.</span><span class="sxs-lookup"><span data-stu-id="8768b-241">But Rattle may prompt you tooinstall additional packages when it loads.</span></span>
>
>

<span data-ttu-id="8768b-242">Rattle usa una interfaz de usuario basada en pestañas.</span><span class="sxs-lookup"><span data-stu-id="8768b-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="8768b-243">La mayoría de las pestañas de hello corresponden toosteps Hola [proceso de ciencia de datos](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), como la carga de datos o explorándolo.</span><span class="sxs-lookup"><span data-stu-id="8768b-243">Most of hello tabs correspond toosteps in hello [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="8768b-244">el proceso de ciencia de datos Hola fluye de izquierda tooright a través de las pestañas de Hola.</span><span class="sxs-lookup"><span data-stu-id="8768b-244">hello data science process flows from left tooright through hello tabs.</span></span> <span data-ttu-id="8768b-245">Pero la última ficha que hello contiene un registro de los comandos de hello R ejecutar sonajero.</span><span class="sxs-lookup"><span data-stu-id="8768b-245">But hello last tab contains a log of hello R commands run by Rattle.</span></span>

<span data-ttu-id="8768b-246">tooload y configurar el conjunto de datos de hello:</span><span class="sxs-lookup"><span data-stu-id="8768b-246">tooload and configure hello dataset:</span></span>

* <span data-ttu-id="8768b-247">archivo de hello tooload, seleccione hello **datos** ficha, a continuación,</span><span class="sxs-lookup"><span data-stu-id="8768b-247">tooload hello file, select hello **Data** tab, then</span></span>
* <span data-ttu-id="8768b-248">Elija selector Hola siguiente demasiado**Filename** y elija **spambaseHeaders.data**.</span><span class="sxs-lookup"><span data-stu-id="8768b-248">Choose hello selector next too**Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="8768b-249">archivo de hello tooload.</span><span class="sxs-lookup"><span data-stu-id="8768b-249">tooload hello file.</span></span> <span data-ttu-id="8768b-250">Seleccione **Execute** en la fila superior de Hola de botones.</span><span class="sxs-lookup"><span data-stu-id="8768b-250">select **Execute** in hello top row of buttons.</span></span> <span data-ttu-id="8768b-251">Debería ver un resumen de cada columna, incluidos su tipo de datos identificado, ya sea una entrada, un destino u otro tipo de variable y número de Hola de valores únicos.</span><span class="sxs-lookup"><span data-stu-id="8768b-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and hello number of unique values.</span></span>
* <span data-ttu-id="8768b-252">Sonajero ha identificado correctamente hello **spam** columna como destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="8768b-252">Rattle has correctly identified hello **spam** column as hello target.</span></span> <span data-ttu-id="8768b-253">Columna de spam seleccione hello y, a continuación, conjunto hello **tipo de datos de destino** demasiado**Categoric**.</span><span class="sxs-lookup"><span data-stu-id="8768b-253">Select hello spam column, then set hello **Target Data Type** too**Categoric**.</span></span>

<span data-ttu-id="8768b-254">datos de Hola tooexplore:</span><span class="sxs-lookup"><span data-stu-id="8768b-254">tooexplore hello data:</span></span>

* <span data-ttu-id="8768b-255">Seleccione hello **explorar** ficha.</span><span class="sxs-lookup"><span data-stu-id="8768b-255">Select hello **Explore** tab.</span></span>
* <span data-ttu-id="8768b-256">Haga clic en **resumen**, a continuación, **Execute**, toosee cierta información sobre los tipos de variable de Hola y algunas estadísticas de resumen.</span><span class="sxs-lookup"><span data-stu-id="8768b-256">Click **Summary**, then **Execute**, toosee some information about hello variable types and some summary statistics.</span></span>
* <span data-ttu-id="8768b-257">tooview otros tipos de estadísticas sobre cada variable, seleccione otras opciones como **describir** o **Fundamentos**.</span><span class="sxs-lookup"><span data-stu-id="8768b-257">tooview other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="8768b-258">Hola **explorar** pestaña también le permite toogenerate muchas precisos traza.</span><span class="sxs-lookup"><span data-stu-id="8768b-258">hello **Explore** tab also allows you toogenerate many insightful plots.</span></span> <span data-ttu-id="8768b-259">un histograma de los datos de Hola tooplot:</span><span class="sxs-lookup"><span data-stu-id="8768b-259">tooplot a histogram of hello data:</span></span>

* <span data-ttu-id="8768b-260">Seleccione **Distributions**(Distribuciones).</span><span class="sxs-lookup"><span data-stu-id="8768b-260">Select **Distributions**.</span></span>
* <span data-ttu-id="8768b-261">Busque en **Histogram** (Histograma) **word_freq_remove** y **word_freq_you**.</span><span class="sxs-lookup"><span data-stu-id="8768b-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="8768b-262">Seleccione **Execute**(Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="8768b-262">Select **Execute**.</span></span> <span data-ttu-id="8768b-263">Debería ver que dos densidad de traza en una ventana de gráfico único, donde resulta evidente esa palabra Hola "usted" aparece con mucha más frecuencia en los correos electrónicos de "quitar".</span><span class="sxs-lookup"><span data-stu-id="8768b-263">You should see both density plots in a single graph window, where it is clear that hello word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="8768b-264">los gráficos de correlación Hello también resultan interesantes.</span><span class="sxs-lookup"><span data-stu-id="8768b-264">hello Correlation plots are also interesting.</span></span> <span data-ttu-id="8768b-265">toocreate uno:</span><span class="sxs-lookup"><span data-stu-id="8768b-265">toocreate one:</span></span>

* <span data-ttu-id="8768b-266">Elija **correlación** como hello **tipo**, a continuación,</span><span class="sxs-lookup"><span data-stu-id="8768b-266">Choose **Correlation** as hello **Type**, then</span></span>
* <span data-ttu-id="8768b-267">Seleccione **Execute**(Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="8768b-267">Select **Execute**.</span></span>
* <span data-ttu-id="8768b-268">Rattle le avisa de que recomienda 40 variables como máximo.</span><span class="sxs-lookup"><span data-stu-id="8768b-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="8768b-269">Seleccione **Sí** trazado de hello tooview.</span><span class="sxs-lookup"><span data-stu-id="8768b-269">Select **Yes** tooview hello plot.</span></span>

<span data-ttu-id="8768b-270">Hay algunas correlaciones interesantes que surjan: "la tecnología" fuertemente se correlaciona demasiado "HP" y "laboratorios", por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8768b-270">There are some interesting correlations that come up: "technology" is strongly correlated too"HP" and "labs", for example.</span></span> <span data-ttu-id="8768b-271">Es también muy correlacionado demasiado "650", porque es de código de área de Hola de donantes de conjunto de datos de hello 650.</span><span class="sxs-lookup"><span data-stu-id="8768b-271">It is also strongly correlated too"650", because hello area code of hello dataset donors is 650.</span></span>

<span data-ttu-id="8768b-272">valores numéricos de Hola para correlaciones Hola entre las palabras están disponibles en la ventana de exploración de hello.</span><span class="sxs-lookup"><span data-stu-id="8768b-272">hello numeric values for hello correlations between words are available in hello Explore window.</span></span> <span data-ttu-id="8768b-273">Es interesante toonote, por ejemplo, que "la tecnología" negativamente está correlacionada con "su" y "money".</span><span class="sxs-lookup"><span data-stu-id="8768b-273">It is interesting toonote, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="8768b-274">Sonajero puede transformar Hola dataset toohandle algunos problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="8768b-274">Rattle can transform hello dataset toohandle some common issues.</span></span> <span data-ttu-id="8768b-275">Por ejemplo, permite características toorescale, imputar valores ausentes, tratar los valores atípicos y quitar variables u observaciones con los datos que faltan.</span><span class="sxs-lookup"><span data-stu-id="8768b-275">For example, it allows you toorescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="8768b-276">Rattle también puede identificar reglas de asociación entre observaciones o variables.</span><span class="sxs-lookup"><span data-stu-id="8768b-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="8768b-277">Estas pestañas escapan del ámbito de este tutorial de introducción.</span><span class="sxs-lookup"><span data-stu-id="8768b-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="8768b-278">Rattle también puede realizar análisis del clúster.</span><span class="sxs-lookup"><span data-stu-id="8768b-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="8768b-279">Permite excluir algunos tooread características toomake Hola salida sea más fácil.</span><span class="sxs-lookup"><span data-stu-id="8768b-279">Let's exclude some features toomake hello output easier tooread.</span></span> <span data-ttu-id="8768b-280">En hello **datos** ficha, elija **omitir** tooeach siguiente de variables de hello excepto estos diez elementos:</span><span class="sxs-lookup"><span data-stu-id="8768b-280">On hello **Data** tab, choose **Ignore** next tooeach of hello variables except these ten items:</span></span>

* <span data-ttu-id="8768b-281">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="8768b-281">word_freq_hp</span></span>
* <span data-ttu-id="8768b-282">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="8768b-282">word_freq_technology</span></span>
* <span data-ttu-id="8768b-283">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="8768b-283">word_freq_george</span></span>
* <span data-ttu-id="8768b-284">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="8768b-284">word_freq_remove</span></span>
* <span data-ttu-id="8768b-285">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="8768b-285">word_freq_your</span></span>
* <span data-ttu-id="8768b-286">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="8768b-286">word_freq_dollar</span></span>
* <span data-ttu-id="8768b-287">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="8768b-287">word_freq_money</span></span>
* <span data-ttu-id="8768b-288">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="8768b-288">capital_run_length_longest</span></span>
* <span data-ttu-id="8768b-289">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="8768b-289">word_freq_business</span></span>
* <span data-ttu-id="8768b-290">spam</span><span class="sxs-lookup"><span data-stu-id="8768b-290">spam</span></span>

<span data-ttu-id="8768b-291">A continuación, regrese toohello **clúster** ficha, elija **KMeans**, conjunto hello y *número de clústeres* too4.</span><span class="sxs-lookup"><span data-stu-id="8768b-291">Then go back toohello **Cluster** tab, choose **KMeans**, and set hello *Number of clusters* too4.</span></span> <span data-ttu-id="8768b-292">A continuación, elija **Execute**(Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="8768b-292">Then **Execute**.</span></span> <span data-ttu-id="8768b-293">resultados de Hola se muestran en la ventana de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="8768b-293">hello results are displayed in hello output window.</span></span> <span data-ttu-id="8768b-294">Un clúster tiene alta frecuencia de "george" y "hp" y es probablemente un correo electrónico comercial legítimo.</span><span class="sxs-lookup"><span data-stu-id="8768b-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="8768b-295">toobuild un modelo de aprendizaje automático de árbol de decisión simple:</span><span class="sxs-lookup"><span data-stu-id="8768b-295">toobuild a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="8768b-296">Seleccione hello **modelo** ficha,</span><span class="sxs-lookup"><span data-stu-id="8768b-296">Select hello **Model** tab,</span></span>
* <span data-ttu-id="8768b-297">Elija **árbol** como hello **tipo**.</span><span class="sxs-lookup"><span data-stu-id="8768b-297">Choose **Tree** as hello **Type**.</span></span>
* <span data-ttu-id="8768b-298">Seleccione **Execute** ventana de salida de árbol de hello toodisplay en formato de texto en Hola.</span><span class="sxs-lookup"><span data-stu-id="8768b-298">Select **Execute** toodisplay hello tree in text form in hello output window.</span></span>
* <span data-ttu-id="8768b-299">Seleccione hello **dibujar** botón tooview una versión gráfica.</span><span class="sxs-lookup"><span data-stu-id="8768b-299">Select hello **Draw** button tooview a graphical version.</span></span> <span data-ttu-id="8768b-300">Esto parece muy similar árbol toohello se ha obtenido anteriormente mediante *rpart*.</span><span class="sxs-lookup"><span data-stu-id="8768b-300">This looks quite similar toohello tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="8768b-301">Una de las características de "nice" hello de sonajero es su toorun capacidad aprendizaje automático de varios métodos y evalúe rápidamente.</span><span class="sxs-lookup"><span data-stu-id="8768b-301">One of hello nice features of Rattle is its ability toorun several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="8768b-302">Éste es el procedimiento de hello:</span><span class="sxs-lookup"><span data-stu-id="8768b-302">Here is hello procedure:</span></span>

* <span data-ttu-id="8768b-303">Elija **todos los** para hello **tipo**.</span><span class="sxs-lookup"><span data-stu-id="8768b-303">Choose **All** for hello **Type**.</span></span>
* <span data-ttu-id="8768b-304">Seleccione **Execute**(Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="8768b-304">Select **Execute**.</span></span>
* <span data-ttu-id="8768b-305">Una vez finalizada puede hacer clic en cualquier único **tipo**, como **SVM**y ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="8768b-305">After it finishes you can click any single **Type**, like **SVM**, and view hello results.</span></span>
* <span data-ttu-id="8768b-306">También puede comparar el rendimiento de Hola de modelos de hello en la validación de hello establecen a través de hello **Evaluate** ficha. Por ejemplo, hello **Error matriz** selección muestra matriz de confusión hello, error general y error de clase promedio de cada modelo en hello validación establecida.</span><span class="sxs-lookup"><span data-stu-id="8768b-306">You can also compare hello performance of hello models on hello validation set using hello **Evaluate** tab. For example, hello **Error Matrix** selection shows you hello confusion matrix, overall error, and averaged class error for each model on hello validation set.</span></span>
* <span data-ttu-id="8768b-307">También puede trazar curvas ROC, realizar análisis de sensibilidad y llevar a cabo otros tipos de evaluaciones de modelos.</span><span class="sxs-lookup"><span data-stu-id="8768b-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="8768b-308">Una vez que haya terminado de generar modelos, seleccione hello **registro** pestaña código de hello R tooview ejecutado por sonajero durante la sesión.</span><span class="sxs-lookup"><span data-stu-id="8768b-308">Once you're finished building models, select hello **Log** tab tooview hello R code run by Rattle during your session.</span></span> <span data-ttu-id="8768b-309">Puede seleccionar hello **exportar** toosave de botón.</span><span class="sxs-lookup"><span data-stu-id="8768b-309">You can select hello **Export** button toosave it.</span></span>

> [!NOTE]
> <span data-ttu-id="8768b-310">Hay un error en la versión actual de Rattle.</span><span class="sxs-lookup"><span data-stu-id="8768b-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="8768b-311">toomodify Hola script o use toorepeat los pasos de una versión posterior, debe insertar un carácter # delante del * exportar este registro... * en texto hello del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="8768b-311">toomodify hello script or use it toorepeat your steps later, you must insert a # character in front of *Export this log ... * in hello text of hello log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="8768b-312">PostgreSQL & Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="8768b-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="8768b-313">Hola DSVM incluye PostgreSQL instalado.</span><span class="sxs-lookup"><span data-stu-id="8768b-313">hello DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="8768b-314">PostgreSQL es una base de datos relacional sofisticada de código abierto.</span><span class="sxs-lookup"><span data-stu-id="8768b-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="8768b-315">Esta sección se muestra cómo tooload nuestro conjunto de datos de correo no deseado en PostgreSQL y, a continuación, realizar consultas sobre él.</span><span class="sxs-lookup"><span data-stu-id="8768b-315">This section shows how tooload our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="8768b-316">Antes de poder cargar los datos de hello, necesita la autenticación de contraseña de tooallow desde el host local de Hola.</span><span class="sxs-lookup"><span data-stu-id="8768b-316">Before you can load hello data, you need tooallow password authentication from hello localhost.</span></span> <span data-ttu-id="8768b-317">En un símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="8768b-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="8768b-318">Final Hola del archivo de configuración de hello son varias líneas donde se detallan Hola conexiones permitida:</span><span class="sxs-lookup"><span data-stu-id="8768b-318">Near hello bottom of hello config file are several lines that detail hello allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="8768b-319">Cambiar Hola "Las conexiones locales de IPv4" línea toouse md5 en lugar de ident, por lo que se puede iniciar sesión con un nombre de usuario y una contraseña:</span><span class="sxs-lookup"><span data-stu-id="8768b-319">Change hello "IPv4 local connections" line toouse md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="8768b-320">Y reinicie el servicio de hello postgres:</span><span class="sxs-lookup"><span data-stu-id="8768b-320">And restart hello postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="8768b-321">toolaunch psql, un terminal interactivo para PostgreSQL, como usuario de hello postgres integrados, ejecute hello siguiente comando desde un símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="8768b-321">toolaunch psql, an interactive terminal for PostgreSQL, as hello built-in postgres user, run hello following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="8768b-322">Crear una nueva cuenta de usuario, mediante Hola el mismo nombre de usuario como Hola cuenta Linux actualmente inició sesión como y asígnele una contraseña:</span><span class="sxs-lookup"><span data-stu-id="8768b-322">Create a new user account, using hello same username as hello Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="8768b-323">A continuación, inicie sesión en toopsql como el usuario:</span><span class="sxs-lookup"><span data-stu-id="8768b-323">Then log in toopsql as your user:</span></span>

    psql

<span data-ttu-id="8768b-324">E importar datos de hello en una base de datos:</span><span class="sxs-lookup"><span data-stu-id="8768b-324">And import hello data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="8768b-325">Ahora, vamos a explorar los datos de Hola y ejecute algunas consultas mediante **ardilla SQL**, una herramienta gráfica que le permite interactuar con bases de datos a través de un controlador JDBC.</span><span class="sxs-lookup"><span data-stu-id="8768b-325">Now, let's explore hello data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="8768b-326">tooget iniciado, inicie SQL ardilla desde el menú "Applications" Hola.</span><span class="sxs-lookup"><span data-stu-id="8768b-326">tooget started, launch Squirrel SQL from hello Applications menu.</span></span> <span data-ttu-id="8768b-327">tooset controlador hello:</span><span class="sxs-lookup"><span data-stu-id="8768b-327">tooset up hello driver:</span></span>

* <span data-ttu-id="8768b-328">Seleccione **Windows** y luego **View Drivers** (Ver controladores).</span><span class="sxs-lookup"><span data-stu-id="8768b-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="8768b-329">Haga clic con el botón derecho en **PostgreSQL** y seleccione **Modify Driver** (Modificar controlador).</span><span class="sxs-lookup"><span data-stu-id="8768b-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="8768b-330">Seleccione **Extra Class Path** (Ruta de clase adicional) y luego **Add** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="8768b-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="8768b-331">Escriba ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** para hello **nombre de archivo** y</span><span class="sxs-lookup"><span data-stu-id="8768b-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for hello **File Name** and</span></span>
* <span data-ttu-id="8768b-332">seleccione **Open**(Abrir).</span><span class="sxs-lookup"><span data-stu-id="8768b-332">Select **Open**.</span></span>
* <span data-ttu-id="8768b-333">Elija List Drivers (Mostrar controladores) y seleccione **org.postgresql.Driver** en **Class Name** (Nombre de clase), a continuación, seleccione **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="8768b-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="8768b-334">tooset de servidor local de hello conexión toohello:</span><span class="sxs-lookup"><span data-stu-id="8768b-334">tooset up hello connection toohello local server:</span></span>

* <span data-ttu-id="8768b-335">Seleccione **Windows** y luego **View Aliases** (Ver alias).</span><span class="sxs-lookup"><span data-stu-id="8768b-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="8768b-336">Elija hello  **+**  toomake botón un nuevo alias.</span><span class="sxs-lookup"><span data-stu-id="8768b-336">Choose hello **+** button toomake a new alias.</span></span>
* <span data-ttu-id="8768b-337">Asígnele el nombre *base de datos de Spam*, elija **PostgreSQL** en hello **controlador** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="8768b-337">Name it *Spam database*, choose **PostgreSQL** in hello **Driver** drop-down.</span></span>
* <span data-ttu-id="8768b-338">Establecer la dirección URL de hello demasiado*jdbc:postgresql://localhost/spam*.</span><span class="sxs-lookup"><span data-stu-id="8768b-338">Set hello URL too*jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="8768b-339">Escriba su *nombre de usuario* y *contraseña*.</span><span class="sxs-lookup"><span data-stu-id="8768b-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="8768b-340">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8768b-340">Click **OK**.</span></span>
* <span data-ttu-id="8768b-341">Hola tooopen **conexión** ventana, haga doble clic en hello ***base de datos de Spam*** alias.</span><span class="sxs-lookup"><span data-stu-id="8768b-341">tooopen hello **Connection** window, double-click hello ***Spam database*** alias.</span></span>
* <span data-ttu-id="8768b-342">Seleccione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="8768b-342">Select **Connect**.</span></span>

<span data-ttu-id="8768b-343">toorun algunas consultas:</span><span class="sxs-lookup"><span data-stu-id="8768b-343">toorun some queries:</span></span>

* <span data-ttu-id="8768b-344">Seleccione hello **SQL** ficha.</span><span class="sxs-lookup"><span data-stu-id="8768b-344">Select hello **SQL** tab.</span></span>
* <span data-ttu-id="8768b-345">Escriba una consulta sencilla como `SELECT * from data;` en cuadro de texto de consulta de hello en parte superior de Hola de pestaña de hello SQL.</span><span class="sxs-lookup"><span data-stu-id="8768b-345">Enter a simple query such as `SELECT * from data;` in hello query textbox at hello top of hello SQL tab.</span></span>
* <span data-ttu-id="8768b-346">Presione **Ctrl-Entrar** toorun lo.</span><span class="sxs-lookup"><span data-stu-id="8768b-346">Press **Ctrl-Enter** toorun it.</span></span> <span data-ttu-id="8768b-347">De forma predeterminada ardilla SQL devuelve Hola 100 primeras filas de la consulta.</span><span class="sxs-lookup"><span data-stu-id="8768b-347">By default Squirrel SQL returns hello first 100 rows from your query.</span></span>

<span data-ttu-id="8768b-348">Hay muchas consultas más que podría ejecutar tooexplore estos datos.</span><span class="sxs-lookup"><span data-stu-id="8768b-348">There are many more queries you could run tooexplore this data.</span></span> <span data-ttu-id="8768b-349">Por ejemplo, ¿cómo Hola frecuencia de la palabra Hola *realizar* difieren entre correo no deseado y ham?</span><span class="sxs-lookup"><span data-stu-id="8768b-349">For example, how does hello frequency of hello word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="8768b-350">O ¿cuáles son las características de saludo de correo electrónico que suelen contengan *3d*?</span><span class="sxs-lookup"><span data-stu-id="8768b-350">Or what are hello characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="8768b-351">La mayoría de correos electrónicos que tienen una repetición de alta *3d* son aparentemente correo no deseado, por lo que podría ser una característica útil para la creación de un saludo de tooclassify modelo predictivo mensajes de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="8768b-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model tooclassify hello emails.</span></span>

<span data-ttu-id="8768b-352">Si deseara aprendizaje automático de tooperform con datos almacenados en una base de datos PostgreSQL, considere el uso de [MADlib](http://madlib.incubator.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="8768b-352">If you wanted tooperform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="8768b-353">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8768b-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="8768b-354">Almacenamiento de datos SQL de Azure es una base de datos de escalado horizontal y basada en la nube capaz de procesar volúmenes masivos de datos (tanto relacionales como no relacionales).</span><span class="sxs-lookup"><span data-stu-id="8768b-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="8768b-355">Para más información, consulte [¿Qué es Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="8768b-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="8768b-356">tooconnect toohello datos de almacenamiento y crean tabla de hello, siguiente ejecución Hola comando desde un símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="8768b-356">tooconnect toohello data warehouse and create hello table, run hello following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="8768b-357">A continuación, en el símbolo del sistema de hello sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="8768b-357">Then at hello sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="8768b-358">Copie los datos con bcp:</span><span class="sxs-lookup"><span data-stu-id="8768b-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="8768b-359">fin de línea de Hello en el archivo descargado Hola es basado en Windows, pero bcp espera estilo UNIX, por lo que necesitamos bcp tootell que con Hola marca - r.</span><span class="sxs-lookup"><span data-stu-id="8768b-359">hello line endings in hello downloaded file are Windows-style, but bcp expects UNIX-style, so we need tootell bcp that with hello -r flag.</span></span>
>
>

<span data-ttu-id="8768b-360">Y la consulta con sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="8768b-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="8768b-361">También puede consultar con Squirrel SQL.</span><span class="sxs-lookup"><span data-stu-id="8768b-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="8768b-362">Seguir pasos similares para PostgreSQL, usando Hola controlador JDBC de Microsoft MSSQL Server, lo que puede encontrarse en ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span><span class="sxs-lookup"><span data-stu-id="8768b-362">Follow similar steps for PostgreSQL, using hello Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8768b-363">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8768b-363">Next steps</span></span>
<span data-ttu-id="8768b-364">Para obtener información general de temas que le guiarán por tareas de Hola que componen el proceso de ciencia de datos de hello en Azure, consulte [proceso de ciencia de datos de equipo](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="8768b-364">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="8768b-365">Para obtener una descripción de los otros tutoriales to-end que muestran los pasos de Hola Hola proceso de ciencia de datos de equipo para escenarios específicos, consulte [tutoriales de proceso de ciencia de datos de equipo](data-science-process-walkthroughs.md).</span><span class="sxs-lookup"><span data-stu-id="8768b-365">For a description of other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="8768b-366">Hola tutoriales también muestran el funcionamiento de cloud toocombine y herramientas local y servicios en un flujo de trabajo o canalización toocreate una aplicación inteligente.</span><span class="sxs-lookup"><span data-stu-id="8768b-366">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>
