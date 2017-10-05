---
title: Ciencia de los datos en Linux Data Science Virtual Machine | Microsoft Docs
description: "Procedimiento para realizar varias tareas comunes de ciencia de los datos con la máquina virtual de Linux Data Science."
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
ms.openlocfilehash: 6da9a8e3f9f8ac851c2a8deb861ac1d0b3ec5874
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="data-science-on-the-linux-data-science-virtual-machine"></a><span data-ttu-id="4a19d-103">Ciencia de los datos en Linux Data Science Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="4a19d-103">Data science on the Linux Data Science Virtual Machine</span></span>
<span data-ttu-id="4a19d-104">En este tutorial se muestra cómo realizar varias tareas comunes de ciencia de los datos con la máquina virtual de Linux Data Science.</span><span class="sxs-lookup"><span data-stu-id="4a19d-104">This walkthrough shows you how to perform several common data science tasks with the Linux Data Science VM.</span></span> <span data-ttu-id="4a19d-105">Linux Data Science Virtual Machine (DSVM) es una imagen de máquina virtual disponible en Azure que viene preinstalada con una colección de herramientas usadas normalmente en el análisis de los datos y el aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="4a19d-105">The Linux Data Science Virtual Machine (DSVM) is a virtual machine image available on Azure that is pre-installed with a collection of tools commonly used for data analytics and machine learning.</span></span> <span data-ttu-id="4a19d-106">Los componentes de software principales se detallan en el tema [Aprovisionamiento de Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="4a19d-106">The key software components are itemized in the [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md) topic.</span></span> <span data-ttu-id="4a19d-107">La imagen de máquina virtual permite comenzar a trabajar fácilmente con la ciencia de los datos en cuestión de minutos, sin tener que instalar ni configurar cada una de las herramientas de forma individual.</span><span class="sxs-lookup"><span data-stu-id="4a19d-107">The VM image makes it easy to get started doing data science in minutes, without having to install and configure each of the tools individually.</span></span> <span data-ttu-id="4a19d-108">Puede escalar la máquina virtual verticalmente de manera fácil, si es necesario, y detenerla cuando no la use.</span><span class="sxs-lookup"><span data-stu-id="4a19d-108">You can easily scale up the VM, if needed, and stop it when not in use.</span></span> <span data-ttu-id="4a19d-109">Así que este recurso es tanto elástico como rentable.</span><span class="sxs-lookup"><span data-stu-id="4a19d-109">So this resource is both elastic and cost-efficient.</span></span>

<span data-ttu-id="4a19d-110">En las tareas de ciencias de los datos que se demuestran en este tutorial se siguen los pasos descritos en el [proceso de ciencia de los datos en equipos](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span><span class="sxs-lookup"><span data-stu-id="4a19d-110">The data science tasks demonstrated in this walkthrough follow the steps outlined in the [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).</span></span> <span data-ttu-id="4a19d-111">Este proceso proporciona un enfoque sistemático sobre la ciencia de los datos que permite a los equipos de científicos de los datos colaborar de manera efectiva durante el ciclo de vida de creación de aplicaciones inteligentes.</span><span class="sxs-lookup"><span data-stu-id="4a19d-111">This process provides a systematic approach to data science that enables teams of data scientists to effectively collaborate over the lifecycle of building intelligent applications.</span></span> <span data-ttu-id="4a19d-112">El proceso de ciencia de los datos también proporciona un marco iterativo para la ciencia de los datos que pueden seguir los individuos.</span><span class="sxs-lookup"><span data-stu-id="4a19d-112">The data science process also provides an iterative framework for data science that can be followed by an individual.</span></span>

<span data-ttu-id="4a19d-113">En este tutorial analizamos el conjunto de datos [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) .</span><span class="sxs-lookup"><span data-stu-id="4a19d-113">We analyze the [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset in this walkthrough.</span></span> <span data-ttu-id="4a19d-114">Se trata de un conjunto de correos electrónicos macados como es correo no deseado o no es correo no deseado, y también contiene algunas estadísticas sobre el contenido de los correos electrónicos.</span><span class="sxs-lookup"><span data-stu-id="4a19d-114">This is a set of emails that are marked as either spam or ham (meaning they are not spam), and also contains some statistics on the content of the emails.</span></span> <span data-ttu-id="4a19d-115">Las estadísticas incluidas se describen en la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="4a19d-115">The statistics included are discussed in the next but one section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a19d-116">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4a19d-116">Prerequisites</span></span>
<span data-ttu-id="4a19d-117">Antes de poder usar una máquina virtual de Linux Data Science, debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4a19d-117">Before you can use a Linux Data Science Virtual Machine, you must have the following:</span></span>

* <span data-ttu-id="4a19d-118">Una **suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="4a19d-118">An **Azure subscription**.</span></span> <span data-ttu-id="4a19d-119">Si ya tiene una, consulte [Cree su cuenta gratuita de Azure hoy mismo](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="4a19d-119">If you do not already have one, see [Create your free Azure account today](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="4a19d-120">Una [**máquina virtual de ciencia de los datos de Linux**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="4a19d-120">A [**Linux data science VM**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm).</span></span> <span data-ttu-id="4a19d-121">Para más información sobre el aprovisionamiento de esta máquina virtual, consulte [Aprovisionamiento de Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span><span class="sxs-lookup"><span data-stu-id="4a19d-121">For information on provisioning this VM, see [Provision the Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).</span></span>
* <span data-ttu-id="4a19d-122">[X2Go](http://wiki.x2go.org/doku.php) instalado en su equipo y abierta una sesión de XFCE.</span><span class="sxs-lookup"><span data-stu-id="4a19d-122">[X2Go](http://wiki.x2go.org/doku.php) installed on your computer and opened an XFCE session.</span></span> <span data-ttu-id="4a19d-123">Para más información sobre la instalación y la configuración de un **cliente X2Go**, consulte [Instalación y configuración del cliente X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span><span class="sxs-lookup"><span data-stu-id="4a19d-123">For information on installing and configuring an **X2Go client**, see [Installing and configuring X2Go client](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).</span></span> 
* <span data-ttu-id="4a19d-124">Una **cuenta de AzureML**.</span><span class="sxs-lookup"><span data-stu-id="4a19d-124">An **AzureML account**.</span></span> <span data-ttu-id="4a19d-125">Si aún no tiene una, suscríbase en la [página principal de AzureML](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="4a19d-125">If you don't already have one, sign up for new one at the [AzureML homepage](https://studio.azureml.net/).</span></span> <span data-ttu-id="4a19d-126">Hay un nivel de uso gratuito para ayudarle a comenzar.</span><span class="sxs-lookup"><span data-stu-id="4a19d-126">There is a free usage tier to help you get started.</span></span>

## <a name="download-the-spambase-dataset"></a><span data-ttu-id="4a19d-127">Descarga del conjunto de datos spambase</span><span class="sxs-lookup"><span data-stu-id="4a19d-127">Download the spambase dataset</span></span>
<span data-ttu-id="4a19d-128">El conjunto de datos [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) es un conjunto de datos relativamente pequeño que contiene únicamente 4601 ejemplos.</span><span class="sxs-lookup"><span data-stu-id="4a19d-128">The [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) dataset is a relatively small set of data that contains only 4601 examples.</span></span> <span data-ttu-id="4a19d-129">Este tamaño es adecuado para demostrar algunas de las características principales de la máquina virtual de Data Sciencie ya que mantiene los requisitos de recursos en un nivel modesto.</span><span class="sxs-lookup"><span data-stu-id="4a19d-129">This is a convenient size to use when demonstrating that some of the key features of the Data Science VM as it keeps the resource requirements modest.</span></span>

> [!NOTE]
> <span data-ttu-id="4a19d-130">Este tutorial se creó en una máquina virtual Linux Data Science de tamaño D2 v2.</span><span class="sxs-lookup"><span data-stu-id="4a19d-130">This walkthrough was created on a D2 v2-sized Linux Data Science Virtual Machine.</span></span> <span data-ttu-id="4a19d-131">Esta DSVM tiene la capacidad para controlar los procedimientos de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="4a19d-131">This size DSVM is capable of handling the procedures in this walkthrough.</span></span>
>
>

<span data-ttu-id="4a19d-132">Si necesita más espacio de almacenamiento, puede crear discos adicionales y conectarlos a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4a19d-132">If you need more storage space, you can create additional disks and attach them to your VM.</span></span> <span data-ttu-id="4a19d-133">Estos discos usan almacenamiento de Azure persistente, por lo que sus datos se conservan incluso cuando el servidor se reaprovisiona debido a un cambio de tamaño o se apaga.</span><span class="sxs-lookup"><span data-stu-id="4a19d-133">These disks use persistent Azure storage, so their data is preserved even when the server is reprovisioned due to resizing or is shut down.</span></span> <span data-ttu-id="4a19d-134">Para agregar un disco y conectarlo a la máquina virtual, siga las instrucciones que se describen en [Adición de un disco a una máquina virtual Linux](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4a19d-134">To add a disk and attach it to your VM, follow the instructions in [Add a disk to a Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4a19d-135">En estos pasos se usa la interfaz de la línea de comandos de Azure (CLI de Azure), que ya está instalada en la DSVM.</span><span class="sxs-lookup"><span data-stu-id="4a19d-135">These steps use the Azure Command-Line Interface (Azure CLI), which is already installed on the DSVM.</span></span> <span data-ttu-id="4a19d-136">De modo que estos procedimientos se pueden realizar por completo en la propia máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4a19d-136">So these procedures can be done entirely from the VM itself.</span></span> <span data-ttu-id="4a19d-137">Otra opción para aumentar el almacenamiento es usar [archivos de Azure](../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4a19d-137">Another option to increase storage is to use [Azure files](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="4a19d-138">Para descargar los datos, abra una ventana de terminal y ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="4a19d-138">To download the data, open a terminal window and run this command:</span></span>

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

<span data-ttu-id="4a19d-139">El archivo descargado no tiene una fila de encabezado, así que vamos a crear otro archivo que la tenga.</span><span class="sxs-lookup"><span data-stu-id="4a19d-139">The downloaded file does not have a header row, so let's create another file that does have a header.</span></span> <span data-ttu-id="4a19d-140">Ejecute este comando para crear un archivo con los encabezados adecuados:</span><span class="sxs-lookup"><span data-stu-id="4a19d-140">Run this command to create a file with the appropriate headers:</span></span>

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

<span data-ttu-id="4a19d-141">A continuación, concatene los dos archivos junto con el comando:</span><span class="sxs-lookup"><span data-stu-id="4a19d-141">Then concatenate the two files together with the command:</span></span>

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

<span data-ttu-id="4a19d-142">El conjunto de datos tiene varios tipos de estadísticas sobre cada correo electrónico:</span><span class="sxs-lookup"><span data-stu-id="4a19d-142">The dataset has several types of statistics on each email:</span></span>

* <span data-ttu-id="4a19d-143">Las columnas como ***word\_freq\_WORD*** indican el porcentaje de palabras en el correo electrónico que coinciden con *WORD*.</span><span class="sxs-lookup"><span data-stu-id="4a19d-143">Columns like ***word\_freq\_WORD*** indicate the percentage of words in the email that match *WORD*.</span></span> <span data-ttu-id="4a19d-144">Por ejemplo, si *word\_freq\_make* es 1, el 1% de todas las palabras en el correo electrónico son *make*.</span><span class="sxs-lookup"><span data-stu-id="4a19d-144">For example, if *word\_freq\_make* is 1, then 1% of all words in the email were *make*.</span></span>
* <span data-ttu-id="4a19d-145">Las columnas como ***char\_freq\_CHAR*** indican el porcentaje de todos los caracteres en el correo electrónico que son *CHAR*.</span><span class="sxs-lookup"><span data-stu-id="4a19d-145">Columns like ***char\_freq\_CHAR*** indicate the percentage of all characters in the email that were *CHAR*.</span></span>
* <span data-ttu-id="4a19d-146">***capital\_run\_length\_longest*** es la mayor longitud de una secuencia de letras mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="4a19d-146">***capital\_run\_length\_longest*** is the longest length of a sequence of capital letters.</span></span>
* <span data-ttu-id="4a19d-147">***capital\_run\_length\_average*** es la longitud media de todas las secuencias de letras mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="4a19d-147">***capital\_run\_length\_average*** is the average length of all sequences of capital letters.</span></span>
* <span data-ttu-id="4a19d-148">***capital\_run\_length\_total*** es la longitud media de todas las secuencias de letras mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="4a19d-148">***capital\_run\_length\_total*** is the total length of all sequences of capital letters.</span></span>
* <span data-ttu-id="4a19d-149">***spam*** indica si el correo electrónico se considera correo no deseado o no (1 = es correo no deseado, 0 = no es correo no deseado).</span><span class="sxs-lookup"><span data-stu-id="4a19d-149">***spam*** indicates whether the email was considered spam or not (1 = spam, 0 = not spam).</span></span>

## <a name="explore-the-dataset-with-microsoft-r-open"></a><span data-ttu-id="4a19d-150">Exploración del conjunto de datos con Microsoft R Open</span><span class="sxs-lookup"><span data-stu-id="4a19d-150">Explore the dataset with Microsoft R Open</span></span>
<span data-ttu-id="4a19d-151">Vamos a examinar los datos y a realizar algunas tareas básicas de aprendizaje automático con R. La máquina virtual de Data Science viene preinstalada con [Microsoft R Open](https://mran.revolutionanalytics.com/open/).</span><span class="sxs-lookup"><span data-stu-id="4a19d-151">Let's examine the data and do some basic machine learning with R. The Data Science VM comes with [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installed.</span></span> <span data-ttu-id="4a19d-152">Las bibliotecas matemáticas multiproceso de esta versión de R ofrecen un rendimiento mejor que diversas versiones de un único subproceso.</span><span class="sxs-lookup"><span data-stu-id="4a19d-152">The multithreaded math libraries in this version of R offer better performance than various single-threaded versions.</span></span> <span data-ttu-id="4a19d-153">Microsoft R Open proporciona también reproducibilidad mediante una instantánea del repositorio de paquetes CRAN.</span><span class="sxs-lookup"><span data-stu-id="4a19d-153">Microsoft R Open also provides reproducibility by using a snapshot of the CRAN package repository.</span></span>

<span data-ttu-id="4a19d-154">Para obtener copias de los ejemplos de código usados en este tutorial, clone el repositorio **Azure-Machine-Learning-Data-Science** con GIT, que viene preinstalado en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4a19d-154">To get copies of the code samples used in this walkthrough, clone the **Azure-Machine-Learning-Data-Science** repository using git, which is pre-installed on the VM.</span></span> <span data-ttu-id="4a19d-155">Desde la línea de comandos de GIT, ejecute:</span><span class="sxs-lookup"><span data-stu-id="4a19d-155">From the git command line, run:</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="4a19d-156">Abra una ventana de terminal e inicie una nueva sesión de R con la consola interactiva de R.</span><span class="sxs-lookup"><span data-stu-id="4a19d-156">Open a terminal window and start a new R session with the R interactive console.</span></span>

> [!NOTE]
> <span data-ttu-id="4a19d-157">También puede usar RStudio para los siguientes procedimientos.</span><span class="sxs-lookup"><span data-stu-id="4a19d-157">You can also use RStudio for the following procedures.</span></span> <span data-ttu-id="4a19d-158">Para instalar RStudio, ejecute este comando en un terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span><span class="sxs-lookup"><span data-stu-id="4a19d-158">To install RStudio, execute this command at a terminal: `./Desktop/DSVM\ tools/installRStudio.sh`</span></span>
>
>

<span data-ttu-id="4a19d-159">Para importar los datos y configurar el entorno, ejecute:</span><span class="sxs-lookup"><span data-stu-id="4a19d-159">To import the data and set up the environment, run:</span></span>

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

<span data-ttu-id="4a19d-160">Para ver estadísticas de resumen sobre cada columna:</span><span class="sxs-lookup"><span data-stu-id="4a19d-160">To see summary statistics about each column:</span></span>

    summary(data)

<span data-ttu-id="4a19d-161">Para tener una vista diferente de los datos:</span><span class="sxs-lookup"><span data-stu-id="4a19d-161">For a different view of the data:</span></span>

    str(data)

<span data-ttu-id="4a19d-162">Esto muestra el tipo de cada variable y algunos de los primeros valores del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="4a19d-162">This shows you the type of each variable and the first few values in the dataset.</span></span>

<span data-ttu-id="4a19d-163">La columna *spam* se leyó como un entero, pero es en realidad una variable (o factor) categórica.</span><span class="sxs-lookup"><span data-stu-id="4a19d-163">The *spam* column was read as an integer, but it's actually a categorical variable (or factor).</span></span> <span data-ttu-id="4a19d-164">Para establecer su tipo:</span><span class="sxs-lookup"><span data-stu-id="4a19d-164">To set its type:</span></span>

    data$spam <- as.factor(data$spam)

<span data-ttu-id="4a19d-165">Para realizar un análisis de exploración, use el paquete [ggplot2](http://ggplot2.org/) , una conocida biblioteca de gráficos para R que ya está instalada en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4a19d-165">To do some exploratory analysis, use the [ggplot2](http://ggplot2.org/) package, a popular graphing library for R that is already installed on the VM.</span></span> <span data-ttu-id="4a19d-166">Observe, por los datos de resumen que se mostraron anteriormente, que tenemos estadísticas de resumen sobre la frecuencia del carácter de signo de exclamación.</span><span class="sxs-lookup"><span data-stu-id="4a19d-166">Note, from the summary data displayed earlier, that we have summary statistics on the frequency of the exclamation mark character.</span></span> <span data-ttu-id="4a19d-167">Vamos a trazar aquí esas frecuencias con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="4a19d-167">Let's plot those frequencies here with the following commands:</span></span>

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="4a19d-168">Puesto que la barra de cero está sesgando el trazado, vamos a deshacernos de ella:</span><span class="sxs-lookup"><span data-stu-id="4a19d-168">Since the zero bar is skewing the plot, let's get rid of it:</span></span>

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="4a19d-169">Hay una densidad no trivial por encima de 1 que parece interesante.</span><span class="sxs-lookup"><span data-stu-id="4a19d-169">There is a non-trivial density above 1 that looks interesting.</span></span> <span data-ttu-id="4a19d-170">Echemos un vistazo solo a esos datos:</span><span class="sxs-lookup"><span data-stu-id="4a19d-170">Let's look at just that data:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

<span data-ttu-id="4a19d-171">A continuación, los vamos a dividir en: es correo no deseado y no es correo no deseado:</span><span class="sxs-lookup"><span data-stu-id="4a19d-171">Then split it by spam vs ham:</span></span>

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

<span data-ttu-id="4a19d-172">Estos ejemplos deben permitirle realizar trazados similares de las demás columnas para explorar los datos contenidos en ellas.</span><span class="sxs-lookup"><span data-stu-id="4a19d-172">These examples should enable you to make similar plots of the other columns to explore the data contained in them.</span></span>

## <a name="train-and-test-an-ml-model"></a><span data-ttu-id="4a19d-173">Entrenamiento y prueba de un modelo de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4a19d-173">Train and test an ML model</span></span>
<span data-ttu-id="4a19d-174">Ahora vamos a entrenar un par de modelos de aprendizaje automático para clasificar los correos electrónicos del conjunto de datos según si son correo no deseado o no es correo no deseado.</span><span class="sxs-lookup"><span data-stu-id="4a19d-174">Now let's train a couple of machine learning models to classify the emails in the dataset as containing either span or ham.</span></span> <span data-ttu-id="4a19d-175">Hemos entrenado un modelo de árbol de decisiones y un modelo de bosque aleatorio en esta sección y después probaremos su precisión en las predicciones.</span><span class="sxs-lookup"><span data-stu-id="4a19d-175">We train a decision tree model and a random forest model in this section and then test their accuracy of their predictions.</span></span>

> [!NOTE]
> <span data-ttu-id="4a19d-176">El paquete rpart (árboles de regresión y particionamiento recursivo) usado en el siguiente código ya está instalado en la máquina virtual de Data Science.</span><span class="sxs-lookup"><span data-stu-id="4a19d-176">The rpart (Recursive Partitioning and Regression Trees) package used in the following code is already installed on the Data Science VM.</span></span>
>
>

<span data-ttu-id="4a19d-177">En primer lugar, vamos a dividir el conjunto de datos en conjuntos de entrenamiento y conjuntos de prueba:</span><span class="sxs-lookup"><span data-stu-id="4a19d-177">First, let's split the dataset into training and test sets:</span></span>

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

<span data-ttu-id="4a19d-178">Luego, crearemos un árbol de decisiones para clasificar los correos electrónicos.</span><span class="sxs-lookup"><span data-stu-id="4a19d-178">And then create a decision tree to classify the emails.</span></span>

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

<span data-ttu-id="4a19d-179">El resultado es este:</span><span class="sxs-lookup"><span data-stu-id="4a19d-179">Here is the result:</span></span>

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

<span data-ttu-id="4a19d-181">Para determinar su rendimiento en el conjunto de entrenamiento, use el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="4a19d-181">To determine how well it performs on the training set, use the following code:</span></span>

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="4a19d-182">Para determinar su rendimiento en el conjunto de prueba:</span><span class="sxs-lookup"><span data-stu-id="4a19d-182">To determine how well it performs on the test set:</span></span>

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

<span data-ttu-id="4a19d-183">Vamos a probar un modelo de bosque aleatorio.</span><span class="sxs-lookup"><span data-stu-id="4a19d-183">Let's also try a random forest model.</span></span> <span data-ttu-id="4a19d-184">Los bosques aleatorios entrenan multitud de árboles de decisiones y generan una clase que es el modo de las clasificaciones de todos los árboles de decisiones individuales.</span><span class="sxs-lookup"><span data-stu-id="4a19d-184">Random forests train a multitude of decision trees and output a class that is the mode of the classifications from all of the individual decision trees.</span></span> <span data-ttu-id="4a19d-185">Proporcionan un enfoque de aprendizaje automático más poderoso ya que corrigen la tendencia de un modelo de árbol de decisiones a saturar en exceso un conjunto de datos de entrenamiento.</span><span class="sxs-lookup"><span data-stu-id="4a19d-185">They provide a more powerful machine learning approach as they correct for the tendency of a decision tree model to overfit a training dataset.</span></span>

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-to-azure-ml"></a><span data-ttu-id="4a19d-186">Implementación de un modelo en Azure ML</span><span class="sxs-lookup"><span data-stu-id="4a19d-186">Deploy a model to Azure ML</span></span>
<span data-ttu-id="4a19d-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) es un servicio en la nube que permite la creación e implementación de forma fácil de modelos de análisis predictivo.</span><span class="sxs-lookup"><span data-stu-id="4a19d-187">[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) is a cloud service that makes it easy to build and deploy predictive analytics models.</span></span> <span data-ttu-id="4a19d-188">Una de las interesantes características de AzureML es la posibilidad de publicar cualquier función de R como un servicio web.</span><span class="sxs-lookup"><span data-stu-id="4a19d-188">One of the nice features of AzureML is its ability to publish any R function as a web service.</span></span> <span data-ttu-id="4a19d-189">El paquete de R de AzureML permite realizar la implementación de forma fácil, justo desde nuestra sesión en la DSVM.</span><span class="sxs-lookup"><span data-stu-id="4a19d-189">The AzureML R package makes deployment easy to do right from our R session on the DSVM.</span></span>

<span data-ttu-id="4a19d-190">Para implementar el código del árbol de decisiones de la sección anterior, debe iniciar sesión en Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4a19d-190">To deploy the decision tree code from the previous section, you need to sign in to Azure Machine Learning Studio.</span></span> <span data-ttu-id="4a19d-191">Necesita el identificador del área de trabajo y un token de autorización para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="4a19d-191">You need your workspace ID and an authorization token to sign in.</span></span> <span data-ttu-id="4a19d-192">Para encontrar estos valores e inicializar las variables de AzureML con ellos:</span><span class="sxs-lookup"><span data-stu-id="4a19d-192">To find these values and initialize the AzureML variables with them:</span></span>

<span data-ttu-id="4a19d-193">Seleccione **Configuración** en el menú izquierdo.</span><span class="sxs-lookup"><span data-stu-id="4a19d-193">Select **Settings** on the left-hand menu.</span></span> <span data-ttu-id="4a19d-194">Anote su **WORKSPACE ID**(ID DE ÁREA DE TRABAJO).</span><span class="sxs-lookup"><span data-stu-id="4a19d-194">Note your **WORKSPACE ID**.</span></span> <span data-ttu-id="4a19d-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span><span class="sxs-lookup"><span data-stu-id="4a19d-195">![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)</span></span>

<span data-ttu-id="4a19d-196">Seleccione **Authorization Tokens** (Tokens de autorización) en el menú principal y anote su **Primary Authorization Token** (Token de autorización principal).![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span><span class="sxs-lookup"><span data-stu-id="4a19d-196">Select **Authorization Tokens** from the overhead menu and note your **Primary Authorization Token**.![3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)</span></span>

<span data-ttu-id="4a19d-197">Cargue el paquete de **AzureML** y luego establezca los valores de las variables con su token y su id. de área de trabajo en la sesión de R de la DSVM:</span><span class="sxs-lookup"><span data-stu-id="4a19d-197">Load the **AzureML** package and then set values of the variables with your token and workspace ID in your R session on the DSVM:</span></span>

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


<span data-ttu-id="4a19d-198">Vamos a simplificar el modelo para que esta demostración sea más fácil de implementar.</span><span class="sxs-lookup"><span data-stu-id="4a19d-198">Let's simplify the model to make this demonstration easier to implement.</span></span> <span data-ttu-id="4a19d-199">Seleccione las tres variables del árbol de decisiones más cercanas a la raíz y cree un nuevo árbol solo con esas tres variables:</span><span class="sxs-lookup"><span data-stu-id="4a19d-199">Pick the three variables in the decision tree closest to the root and build a new tree using just those three variables:</span></span>

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

<span data-ttu-id="4a19d-200">Necesitamos una función de predicción que tome las características como una entrada y devuelva los valores previstos:</span><span class="sxs-lookup"><span data-stu-id="4a19d-200">We need a prediction function that takes the features as an input and returns the predicted values:</span></span>

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

<span data-ttu-id="4a19d-201">Publique la función predictSpam en AzureML mediante la función **publishWebService** :</span><span class="sxs-lookup"><span data-stu-id="4a19d-201">Publish the predictSpam function to AzureML using the **publishWebService** function:</span></span>

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

<span data-ttu-id="4a19d-202">Esta función toma la función **predictSpam**, crea un servicio web llamado **spamWebService** con entradas y salidas definidas y devuelve información sobre el nuevo punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="4a19d-202">This function takes the **predictSpam** function, creates a web service named **spamWebService** with defined inputs and outputs, and returns information about the new endpoint.</span></span>

<span data-ttu-id="4a19d-203">Vea los detalles del servicio web publicado, junto con su punto de conexión de API y las claves de acceso con el comando:</span><span class="sxs-lookup"><span data-stu-id="4a19d-203">View details of the published web service, including its API endpoint and access keys with the command:</span></span>

    spamWebService[[2]]

<span data-ttu-id="4a19d-204">Para probarlo en las 10 primeras filas del conjunto de prueba:</span><span class="sxs-lookup"><span data-stu-id="4a19d-204">To try it out on the first 10 rows of the test set:</span></span>

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a><span data-ttu-id="4a19d-205">Uso de otras herramientas disponibles</span><span class="sxs-lookup"><span data-stu-id="4a19d-205">Use other tools available</span></span>
<span data-ttu-id="4a19d-206">En las secciones restantes se muestra cómo usar algunas de las herramientas instaladas en la máquina virtual de Linux Data Science. Esta es la lista de herramientas que se describe:</span><span class="sxs-lookup"><span data-stu-id="4a19d-206">The remaining sections show how to use some of the tools installed on the Linux Data Science VM.Here is the list of tools discussed:</span></span>

* <span data-ttu-id="4a19d-207">XGBoost</span><span class="sxs-lookup"><span data-stu-id="4a19d-207">XGBoost</span></span>
* <span data-ttu-id="4a19d-208">Python</span><span class="sxs-lookup"><span data-stu-id="4a19d-208">Python</span></span>
* <span data-ttu-id="4a19d-209">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="4a19d-209">Jupyterhub</span></span>
* <span data-ttu-id="4a19d-210">Rattle</span><span class="sxs-lookup"><span data-stu-id="4a19d-210">Rattle</span></span>
* <span data-ttu-id="4a19d-211">PostgreSQL & Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="4a19d-211">PostgreSQL & Squirrel SQL</span></span>
* <span data-ttu-id="4a19d-212">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4a19d-212">SQL Server Data Warehouse</span></span>

## <a name="xgboost"></a><span data-ttu-id="4a19d-213">XGBoost</span><span class="sxs-lookup"><span data-stu-id="4a19d-213">XGBoost</span></span>
<span data-ttu-id="4a19d-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) es una herramienta que proporciona una implementación de árbol ampliada rápida y precisa.</span><span class="sxs-lookup"><span data-stu-id="4a19d-214">[XGBoost](https://xgboost.readthedocs.org/en/latest/) is a tool that provides a fast and accurate boosted tree implementation.</span></span>

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

<span data-ttu-id="4a19d-215">XGBoost también se puede llamar desde Python o una línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="4a19d-215">XGBoost can also call from python or a command line.</span></span>

## <a name="python"></a><span data-ttu-id="4a19d-216">Python</span><span class="sxs-lookup"><span data-stu-id="4a19d-216">Python</span></span>
<span data-ttu-id="4a19d-217">Para el desarrollo con Python, se han instalado las distribuciones 2.7 y 3.5 de Anaconda Python en la DSVM.</span><span class="sxs-lookup"><span data-stu-id="4a19d-217">For development using Python, the Anaconda Python distributions 2.7 and 3.5 have been installed in the DSVM.</span></span>

> [!NOTE]
> <span data-ttu-id="4a19d-218">La distribución Anaconda incluye [Condas](http://conda.pydata.org/docs/index.html), que se puede usar para crear entornos personalizados para Python que tengan instalados diferentes versiones o paquetes.</span><span class="sxs-lookup"><span data-stu-id="4a19d-218">The Anaconda distribution includes [Condas](http://conda.pydata.org/docs/index.html), which can be used to create custom environments for Python that have different versions and/or packages installed in them.</span></span>
>
>

<span data-ttu-id="4a19d-219">Vamos a leer algunos de los conjuntos de datos spambase y a clasificar los correos electrónicos con máquinas vectoriales de apoyo en scikit-learn:</span><span class="sxs-lookup"><span data-stu-id="4a19d-219">Let's read in some of the spambase dataset and classify the emails with support vector machines in scikit-learn:</span></span>

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="4a19d-220">Para realizar predicciones:</span><span class="sxs-lookup"><span data-stu-id="4a19d-220">To make predictions:</span></span>

    clf.predict(X.ix[0:20, :])

<span data-ttu-id="4a19d-221">Para mostrar cómo publicar un punto de conexión de AzureML, vamos a crear un modelo más simple con tres variables como hicimos cuando publicamos el modelo de R anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4a19d-221">To show how to publish an AzureML endpoint, let's make a simpler model the three variables as we did when we published the R model previously.</span></span>

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

<span data-ttu-id="4a19d-222">Para publicar el modelo en AzureML:</span><span class="sxs-lookup"><span data-stu-id="4a19d-222">To publish the model to AzureML:</span></span>

    # Publish the model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about the resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call the model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> <span data-ttu-id="4a19d-223">Esto solo está disponible para Python 2.7 y todavía no se admite en la versión 3.5.</span><span class="sxs-lookup"><span data-stu-id="4a19d-223">This is only available for python 2.7 and is not yet supported on 3.5.</span></span> <span data-ttu-id="4a19d-224">Realice la ejecución con **/anaconda/bin/python2.7**.</span><span class="sxs-lookup"><span data-stu-id="4a19d-224">Run with **/anaconda/bin/python2.7**.</span></span>
>
>

## <a name="jupyterhub"></a><span data-ttu-id="4a19d-225">Jupyterhub</span><span class="sxs-lookup"><span data-stu-id="4a19d-225">Jupyterhub</span></span>
<span data-ttu-id="4a19d-226">La distribución Anaconda en la DSVM viene con Jupyter Notebook, un entorno multiplataforma para compartir código y análisis de Python, R o Julia.</span><span class="sxs-lookup"><span data-stu-id="4a19d-226">The Anaconda distribution in the DSVM comes with a Jupyter notebook, a cross-platform environment to share Python, R, or Julia code and analysis.</span></span> <span data-ttu-id="4a19d-227">Se accede a Jupyter Notebook mediante JupyterHub.</span><span class="sxs-lookup"><span data-stu-id="4a19d-227">The Jupyter notebook is accessed through JupyterHub.</span></span> <span data-ttu-id="4a19d-228">Para iniciar sesión se usa el nombre de usuario local y la contraseña de Linux en ***https://\<nombre DNS o dirección IP de la máquina virtual\>:8000/***.</span><span class="sxs-lookup"><span data-stu-id="4a19d-228">You sign in using your local Linux user name and password at ***https://\<VM DNS name or IP Address\>:8000/***.</span></span> <span data-ttu-id="4a19d-229">Todos los archivos de configuración de JupyterHub se encuentran en el directorio **/etc/jupyterhub**.</span><span class="sxs-lookup"><span data-stu-id="4a19d-229">All configuration files for JupyterHub are found in directory **/etc/jupyterhub**.</span></span>

<span data-ttu-id="4a19d-230">Hay varios cuadernos de muestra ya instalados en la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="4a19d-230">Several sample notebooks are already installed on the VM:</span></span>

* <span data-ttu-id="4a19d-231">Consulte [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) para ver un cuaderno de ejemplo de Python.</span><span class="sxs-lookup"><span data-stu-id="4a19d-231">See the [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) for a sample Python notebook.</span></span>
* <span data-ttu-id="4a19d-232">Consulte [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) para ver un cuaderno de **R** de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="4a19d-232">See [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) for a sample **R** notebook.</span></span>
* <span data-ttu-id="4a19d-233">Consulte [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) para ver otro cuaderno de ejemplo de **Python** .</span><span class="sxs-lookup"><span data-stu-id="4a19d-233">See the [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) for another sample **Python** notebook.</span></span>

> [!NOTE]
> <span data-ttu-id="4a19d-234">El lenguaje Julia también está disponible desde la línea de comandos en la máquina virtual de Linux Data Science.</span><span class="sxs-lookup"><span data-stu-id="4a19d-234">The Julia language is also available from the command line on the Linux Data Science VM.</span></span>
>
>

## <a name="rattle"></a><span data-ttu-id="4a19d-235">Rattle</span><span class="sxs-lookup"><span data-stu-id="4a19d-235">Rattle</span></span>
<span data-ttu-id="4a19d-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (R Analytical Tool To Learn Easily) es una herramienta gráfica de R para la minería de datos.</span><span class="sxs-lookup"><span data-stu-id="4a19d-236">[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (the R Analytical Tool To Learn Easily) is a graphical R tool for data mining.</span></span> <span data-ttu-id="4a19d-237">Presenta una interfaz intuitiva que permite cargar, explorar y transformar los datos y crear y evaluar modelos de forma fácil.</span><span class="sxs-lookup"><span data-stu-id="4a19d-237">It has an intuitive interface that makes it easy to load, explore, and transform data and build and evaluate models.</span></span>  <span data-ttu-id="4a19d-238">El artículo [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) (Rattle: una GUI de minería de datos para R) proporciona un tutorial que demuestra sus características.</span><span class="sxs-lookup"><span data-stu-id="4a19d-238">The article [Rattle: A Data Mining GUI for R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) provides a walkthrough that demonstrates its features.</span></span>

<span data-ttu-id="4a19d-239">Instale e inicie Rattle con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="4a19d-239">Install and start Rattle with the following commands:</span></span>

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> <span data-ttu-id="4a19d-240">No es necesario instalarlo en la DSVM.</span><span class="sxs-lookup"><span data-stu-id="4a19d-240">Installation is not required on the DSVM.</span></span> <span data-ttu-id="4a19d-241">Sin embargo, Rattle puede pedirle que instale paquetes adicionales cuando se carga.</span><span class="sxs-lookup"><span data-stu-id="4a19d-241">But Rattle may prompt you to install additional packages when it loads.</span></span>
>
>

<span data-ttu-id="4a19d-242">Rattle usa una interfaz de usuario basada en pestañas.</span><span class="sxs-lookup"><span data-stu-id="4a19d-242">Rattle uses a tab-based interface.</span></span> <span data-ttu-id="4a19d-243">La mayoría de las pestañas corresponden a pasos del [proceso de ciencia de los datos](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), como cargar los datos o explorarlos.</span><span class="sxs-lookup"><span data-stu-id="4a19d-243">Most of the tabs correspond to steps in the [Data Science Process](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), like loading data or exploring it.</span></span> <span data-ttu-id="4a19d-244">El proceso de ciencia de los datos fluye de izquierda a derecha por las pestañas.</span><span class="sxs-lookup"><span data-stu-id="4a19d-244">The data science process flows from left to right through the tabs.</span></span> <span data-ttu-id="4a19d-245">Pero la última pestaña contiene un registro de los comandos de R ejecutados por Rattle.</span><span class="sxs-lookup"><span data-stu-id="4a19d-245">But the last tab contains a log of the R commands run by Rattle.</span></span>

<span data-ttu-id="4a19d-246">Para cargar y configurar el conjunto de datos:</span><span class="sxs-lookup"><span data-stu-id="4a19d-246">To load and configure the dataset:</span></span>

* <span data-ttu-id="4a19d-247">Para cargar el archivo, seleccione la pestaña **Data** (Datos).</span><span class="sxs-lookup"><span data-stu-id="4a19d-247">To load the file, select the **Data** tab, then</span></span>
* <span data-ttu-id="4a19d-248">Elija el selector junto a **Filename** (Nombre de archivo) y elija **spambaseHeaders.data**.</span><span class="sxs-lookup"><span data-stu-id="4a19d-248">Choose the selector next to **Filename** and choose **spambaseHeaders.data**.</span></span>
* <span data-ttu-id="4a19d-249">Para cargar el archivo</span><span class="sxs-lookup"><span data-stu-id="4a19d-249">To load the file.</span></span> <span data-ttu-id="4a19d-250">seleccione **Execute** (Ejecutar) en la fila superior de botones.</span><span class="sxs-lookup"><span data-stu-id="4a19d-250">select **Execute** in the top row of buttons.</span></span> <span data-ttu-id="4a19d-251">Verá un resumen de cada columna, junto con su tipo de datos identificado, si es una entrada, un destino u otro tipo de variable, y el número de valores únicos.</span><span class="sxs-lookup"><span data-stu-id="4a19d-251">You should see a summary of each column, including its identified data type, whether it's an input, a target, or other type of variable, and the number of unique values.</span></span>
* <span data-ttu-id="4a19d-252">Rattle ha identificado correctamente la columna **correo no deseado** como el destino.</span><span class="sxs-lookup"><span data-stu-id="4a19d-252">Rattle has correctly identified the **spam** column as the target.</span></span> <span data-ttu-id="4a19d-253">Seleccione la columna de correo no deseado y luego establezca el **tipo de datos de destino** en **Categoric** (Categórico).</span><span class="sxs-lookup"><span data-stu-id="4a19d-253">Select the spam column, then set the **Target Data Type** to **Categoric**.</span></span>

<span data-ttu-id="4a19d-254">Para explorar los datos:</span><span class="sxs-lookup"><span data-stu-id="4a19d-254">To explore the data:</span></span>

* <span data-ttu-id="4a19d-255">Seleccione la pestaña **Explore** (Explorar).</span><span class="sxs-lookup"><span data-stu-id="4a19d-255">Select the **Explore** tab.</span></span>
* <span data-ttu-id="4a19d-256">Haga clic en **Summary** (Resumen) y luego en **Execute** (Ejecutar) para ver alguna información sobre los tipos de variables y algunas estadísticas de resumen.</span><span class="sxs-lookup"><span data-stu-id="4a19d-256">Click **Summary**, then **Execute**, to see some information about the variable types and some summary statistics.</span></span>
* <span data-ttu-id="4a19d-257">Para ver otros tipos de estadísticas sobre cada variable, seleccione otras opciones como **Describe** (Describir) o **Basics** (Fundamentos).</span><span class="sxs-lookup"><span data-stu-id="4a19d-257">To view other types of statistics about each variable, select other options like **Describe** or **Basics**.</span></span>

<span data-ttu-id="4a19d-258">La pestaña **Explore** (Explorar) le permite generar muchos trazados detallados.</span><span class="sxs-lookup"><span data-stu-id="4a19d-258">The **Explore** tab also allows you to generate many insightful plots.</span></span> <span data-ttu-id="4a19d-259">Para trazar un histograma de los datos:</span><span class="sxs-lookup"><span data-stu-id="4a19d-259">To plot a histogram of the data:</span></span>

* <span data-ttu-id="4a19d-260">Seleccione **Distributions**(Distribuciones).</span><span class="sxs-lookup"><span data-stu-id="4a19d-260">Select **Distributions**.</span></span>
* <span data-ttu-id="4a19d-261">Busque en **Histogram** (Histograma) **word_freq_remove** y **word_freq_you**.</span><span class="sxs-lookup"><span data-stu-id="4a19d-261">Check **Histogram** for **word_freq_remove** and **word_freq_you**.</span></span>
* <span data-ttu-id="4a19d-262">Seleccione **Execute**(Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="4a19d-262">Select **Execute**.</span></span> <span data-ttu-id="4a19d-263">Verá ambos trazados de densidad en una sola ventana gráfica, donde está claro que la palabra "you" aparece con mucha más frecuencia que "remove".</span><span class="sxs-lookup"><span data-stu-id="4a19d-263">You should see both density plots in a single graph window, where it is clear that the word "you" appears much more frequently in emails than "remove".</span></span>

<span data-ttu-id="4a19d-264">Los trazados de correlación también son interesantes.</span><span class="sxs-lookup"><span data-stu-id="4a19d-264">The Correlation plots are also interesting.</span></span> <span data-ttu-id="4a19d-265">Para crear uno:</span><span class="sxs-lookup"><span data-stu-id="4a19d-265">To create one:</span></span>

* <span data-ttu-id="4a19d-266">Elija **Correlation** (Correlación) como el **tipo**.</span><span class="sxs-lookup"><span data-stu-id="4a19d-266">Choose **Correlation** as the **Type**, then</span></span>
* <span data-ttu-id="4a19d-267">Seleccione **Execute**(Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="4a19d-267">Select **Execute**.</span></span>
* <span data-ttu-id="4a19d-268">Rattle le avisa de que recomienda 40 variables como máximo.</span><span class="sxs-lookup"><span data-stu-id="4a19d-268">Rattle warns you that it recommends a maximum of 40 variables.</span></span> <span data-ttu-id="4a19d-269">Seleccione **Yes** (Sí) para ver la trazado.</span><span class="sxs-lookup"><span data-stu-id="4a19d-269">Select **Yes** to view the plot.</span></span>

<span data-ttu-id="4a19d-270">Surgen algunas correlaciones interesantes: por ejemplo, "technology" está estrechamente relacionado con "HP" y "labs".</span><span class="sxs-lookup"><span data-stu-id="4a19d-270">There are some interesting correlations that come up: "technology" is strongly correlated to "HP" and "labs", for example.</span></span> <span data-ttu-id="4a19d-271">También está estrechamente correlacionado con "650", porque el código de área de los donantes del conjunto de datos es 650.</span><span class="sxs-lookup"><span data-stu-id="4a19d-271">It is also strongly correlated to "650", because the area code of the dataset donors is 650.</span></span>

<span data-ttu-id="4a19d-272">Los valores numéricos de las correlaciones entre palabras están disponibles en la ventana de exploración.</span><span class="sxs-lookup"><span data-stu-id="4a19d-272">The numeric values for the correlations between words are available in the Explore window.</span></span> <span data-ttu-id="4a19d-273">Es interesante advertir, por ejemplo, que "technology" está correlacionada negativamente con "your" y "money".</span><span class="sxs-lookup"><span data-stu-id="4a19d-273">It is interesting to note, for example, that "technology" is negatively correlated with "your" and "money".</span></span>

<span data-ttu-id="4a19d-274">Rattle puede transformar el conjunto de datos para tratar algunos problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="4a19d-274">Rattle can transform the dataset to handle some common issues.</span></span> <span data-ttu-id="4a19d-275">Por ejemplo, le permite volver a escalar características, imputar valores que faltan, administrar los valores atípicos y quitar variables u observaciones con datos que faltan.</span><span class="sxs-lookup"><span data-stu-id="4a19d-275">For example, it allows you to rescale features, impute missing values, handle outliers, and remove variables or observations with missing data.</span></span> <span data-ttu-id="4a19d-276">Rattle también puede identificar reglas de asociación entre observaciones o variables.</span><span class="sxs-lookup"><span data-stu-id="4a19d-276">Rattle can also identify association rules between observations and/or variables.</span></span> <span data-ttu-id="4a19d-277">Estas pestañas escapan del ámbito de este tutorial de introducción.</span><span class="sxs-lookup"><span data-stu-id="4a19d-277">These tabs are out of scope for this introductory walkthrough.</span></span>

<span data-ttu-id="4a19d-278">Rattle también puede realizar análisis del clúster.</span><span class="sxs-lookup"><span data-stu-id="4a19d-278">Rattle can also perform cluster analysis.</span></span> <span data-ttu-id="4a19d-279">Vamos a excluir algunas características para que la salida sea más fácil de leer.</span><span class="sxs-lookup"><span data-stu-id="4a19d-279">Let's exclude some features to make the output easier to read.</span></span> <span data-ttu-id="4a19d-280">En la pestaña **Data** (Datos), elija **Ignore** (Ignorar) junto a cada una de las variables excepto estos diez términos:</span><span class="sxs-lookup"><span data-stu-id="4a19d-280">On the **Data** tab, choose **Ignore** next to each of the variables except these ten items:</span></span>

* <span data-ttu-id="4a19d-281">word_freq_hp</span><span class="sxs-lookup"><span data-stu-id="4a19d-281">word_freq_hp</span></span>
* <span data-ttu-id="4a19d-282">word_freq_technology</span><span class="sxs-lookup"><span data-stu-id="4a19d-282">word_freq_technology</span></span>
* <span data-ttu-id="4a19d-283">word_freq_george</span><span class="sxs-lookup"><span data-stu-id="4a19d-283">word_freq_george</span></span>
* <span data-ttu-id="4a19d-284">word_freq_remove</span><span class="sxs-lookup"><span data-stu-id="4a19d-284">word_freq_remove</span></span>
* <span data-ttu-id="4a19d-285">word_freq_your</span><span class="sxs-lookup"><span data-stu-id="4a19d-285">word_freq_your</span></span>
* <span data-ttu-id="4a19d-286">word_freq_dollar</span><span class="sxs-lookup"><span data-stu-id="4a19d-286">word_freq_dollar</span></span>
* <span data-ttu-id="4a19d-287">word_freq_money</span><span class="sxs-lookup"><span data-stu-id="4a19d-287">word_freq_money</span></span>
* <span data-ttu-id="4a19d-288">capital_run_length_longest</span><span class="sxs-lookup"><span data-stu-id="4a19d-288">capital_run_length_longest</span></span>
* <span data-ttu-id="4a19d-289">word_freq_business</span><span class="sxs-lookup"><span data-stu-id="4a19d-289">word_freq_business</span></span>
* <span data-ttu-id="4a19d-290">spam</span><span class="sxs-lookup"><span data-stu-id="4a19d-290">spam</span></span>

<span data-ttu-id="4a19d-291">A continuación, vuelva a la pestaña **Cluster** (Clúster), elija **KMeans** y establezca *Number of clusters* (Número de clústeres) en 4.</span><span class="sxs-lookup"><span data-stu-id="4a19d-291">Then go back to the **Cluster** tab, choose **KMeans**, and set the *Number of clusters* to 4.</span></span> <span data-ttu-id="4a19d-292">A continuación, elija **Execute**(Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="4a19d-292">Then **Execute**.</span></span> <span data-ttu-id="4a19d-293">Los resultados se muestran en la ventana de salida.</span><span class="sxs-lookup"><span data-stu-id="4a19d-293">The results are displayed in the output window.</span></span> <span data-ttu-id="4a19d-294">Un clúster tiene alta frecuencia de "george" y "hp" y es probablemente un correo electrónico comercial legítimo.</span><span class="sxs-lookup"><span data-stu-id="4a19d-294">One cluster has high frequency of "george" and "hp" and is probably a legitimate business email.</span></span>

<span data-ttu-id="4a19d-295">Para crear un modelo de aprendizaje automático de árbol de decisiones sencillo:</span><span class="sxs-lookup"><span data-stu-id="4a19d-295">To build a simple decision tree machine learning model:</span></span>

* <span data-ttu-id="4a19d-296">Seleccione la pestaña **Model** (Modelo).</span><span class="sxs-lookup"><span data-stu-id="4a19d-296">Select the **Model** tab,</span></span>
* <span data-ttu-id="4a19d-297">Elija **Tree** (Árbol) en **Type** (Tipo).</span><span class="sxs-lookup"><span data-stu-id="4a19d-297">Choose **Tree** as the **Type**.</span></span>
* <span data-ttu-id="4a19d-298">Seleccione **Execute** (Ejecutar) para mostrar el árbol en forma de texto en la ventana de salida.</span><span class="sxs-lookup"><span data-stu-id="4a19d-298">Select **Execute** to display the tree in text form in the output window.</span></span>
* <span data-ttu-id="4a19d-299">Seleccione el botón **Draw** (Dibujar) para ver una versión gráfica.</span><span class="sxs-lookup"><span data-stu-id="4a19d-299">Select the **Draw** button to view a graphical version.</span></span> <span data-ttu-id="4a19d-300">Se parece bastante al árbol que obtuvimos anteriormente mediante *rpart*.</span><span class="sxs-lookup"><span data-stu-id="4a19d-300">This looks quite similar to the tree we obtained earlier using *rpart*.</span></span>

<span data-ttu-id="4a19d-301">Una de las características interesantes de Rattle es la posibilidad de ejecutar varios métodos de aprendizaje automático y evaluarlos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="4a19d-301">One of the nice features of Rattle is its ability to run several machine learning methods and quickly evaluate them.</span></span> <span data-ttu-id="4a19d-302">A continuación se muestra el procedimiento:</span><span class="sxs-lookup"><span data-stu-id="4a19d-302">Here is the procedure:</span></span>

* <span data-ttu-id="4a19d-303">Elija **All** (Todo) como **Type**.</span><span class="sxs-lookup"><span data-stu-id="4a19d-303">Choose **All** for the **Type**.</span></span>
* <span data-ttu-id="4a19d-304">Seleccione **Execute**(Ejecutar).</span><span class="sxs-lookup"><span data-stu-id="4a19d-304">Select **Execute**.</span></span>
* <span data-ttu-id="4a19d-305">Cuando finalice, puede hacer clic en cualquier **tipo**, como **SVM** y ver los resultados.</span><span class="sxs-lookup"><span data-stu-id="4a19d-305">After it finishes you can click any single **Type**, like **SVM**, and view the results.</span></span>
* <span data-ttu-id="4a19d-306">También puede comparar el rendimiento de los modelos en el conjunto de validación mediante la pestaña **Evaluate** (Evaluar). Por ejemplo, la selección **Error Matrix** (Matriz de errores) muestra la matriz de confusiones, los errores generales y la media de errores de clase de cada modelo en el conjunto de validación.</span><span class="sxs-lookup"><span data-stu-id="4a19d-306">You can also compare the performance of the models on the validation set using the **Evaluate** tab. For example, the **Error Matrix** selection shows you the confusion matrix, overall error, and averaged class error for each model on the validation set.</span></span>
* <span data-ttu-id="4a19d-307">También puede trazar curvas ROC, realizar análisis de sensibilidad y llevar a cabo otros tipos de evaluaciones de modelos.</span><span class="sxs-lookup"><span data-stu-id="4a19d-307">You can also plot ROC curves, perform sensitivity analysis, and do other types of model evaluations.</span></span>

<span data-ttu-id="4a19d-308">Cuando haya terminado de crear modelos, seleccione la pestaña **Log** (Registrar) para ver el código R ejecutado por Rattle durante la sesión.</span><span class="sxs-lookup"><span data-stu-id="4a19d-308">Once you're finished building models, select the **Log** tab to view the R code run by Rattle during your session.</span></span> <span data-ttu-id="4a19d-309">Puede seleccionar el botón **Export** (Exportar) para guardarlo.</span><span class="sxs-lookup"><span data-stu-id="4a19d-309">You can select the **Export** button to save it.</span></span>

> [!NOTE]
> <span data-ttu-id="4a19d-310">Hay un error en la versión actual de Rattle.</span><span class="sxs-lookup"><span data-stu-id="4a19d-310">There is a bug in current release of Rattle.</span></span> <span data-ttu-id="4a19d-311">Para modificar el script o usarlo para repetir los pasos más adelante, debe insertar un carácter # delante de *Export this log ...* (Exportar este registro) en el texto del registro.</span><span class="sxs-lookup"><span data-stu-id="4a19d-311">To modify the script or use it to repeat your steps later, you must insert a # character in front of *Export this log ... * in the text of the log.</span></span>
>
>

## <a name="postgresql--squirrel-sql"></a><span data-ttu-id="4a19d-312">PostgreSQL & Squirrel SQL</span><span class="sxs-lookup"><span data-stu-id="4a19d-312">PostgreSQL & Squirrel SQL</span></span>
<span data-ttu-id="4a19d-313">La DSVM viene con PostgreSQL instalado.</span><span class="sxs-lookup"><span data-stu-id="4a19d-313">The DSVM comes with PostgreSQL installed.</span></span> <span data-ttu-id="4a19d-314">PostgreSQL es una base de datos relacional sofisticada de código abierto.</span><span class="sxs-lookup"><span data-stu-id="4a19d-314">PostgreSQL is a sophisticated, open-source relational database.</span></span> <span data-ttu-id="4a19d-315">En esta sección se muestra cómo cargar nuestro conjunto de datos de correo no deseado en PostgreSQL y luego consultarlo.</span><span class="sxs-lookup"><span data-stu-id="4a19d-315">This section shows how to load our spam dataset into PostgreSQL and then query it.</span></span>

<span data-ttu-id="4a19d-316">Antes de cargar los datos, debe permitir la autenticación de contraseña desde el host local.</span><span class="sxs-lookup"><span data-stu-id="4a19d-316">Before you can load the data, you need to allow password authentication from the localhost.</span></span> <span data-ttu-id="4a19d-317">En un símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="4a19d-317">At a command prompt:</span></span>

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

<span data-ttu-id="4a19d-318">Cerca de la parte inferior del archivo de configuración, hay varias líneas que detallan las conexiones permitidas:</span><span class="sxs-lookup"><span data-stu-id="4a19d-318">Near the bottom of the config file are several lines that detail the allowed connections:</span></span>

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

<span data-ttu-id="4a19d-319">Cambie la línea "IPv4 local connections" para usar md5 en lugar de ident, así podremos iniciar sesión con un nombre de usuario y una contraseña:</span><span class="sxs-lookup"><span data-stu-id="4a19d-319">Change the "IPv4 local connections" line to use md5 instead of ident, so we can log in using a username and password:</span></span>

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

<span data-ttu-id="4a19d-320">Reinicie el servicio de postgres:</span><span class="sxs-lookup"><span data-stu-id="4a19d-320">And restart the postgres service:</span></span>

    sudo systemctl restart postgresql

<span data-ttu-id="4a19d-321">Para iniciar psql, un terminal interactivo para PostgreSQL, con el usuario de postgres integrado, ejecuta el siguiente comando desde un símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="4a19d-321">To launch psql, an interactive terminal for PostgreSQL, as the built-in postgres user, run the following command from a prompt:</span></span>

    sudo -u postgres psql

<span data-ttu-id="4a19d-322">Cree una nueva cuenta de usuario, con el mismo nombre de usuario que el de la cuenta de Linux con el que ha iniciado la sesión, y proporcione una contraseña:</span><span class="sxs-lookup"><span data-stu-id="4a19d-322">Create a new user account, using the same username as the Linux account you're currently logged in as, and give it a password:</span></span>

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

<span data-ttu-id="4a19d-323">A continuación, inicie sesión en psql con su usuario:</span><span class="sxs-lookup"><span data-stu-id="4a19d-323">Then log in to psql as your user:</span></span>

    psql

<span data-ttu-id="4a19d-324">Importe los datos en una base de datos:</span><span class="sxs-lookup"><span data-stu-id="4a19d-324">And import the data into a new database:</span></span>

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

<span data-ttu-id="4a19d-325">Ahora, vamos a explorar los datos y a ejecutar algunas consultas mediante **Squirrel SQL**, una herramienta gráfica que le permite interactuar con bases de datos mediante un controlador JDBC.</span><span class="sxs-lookup"><span data-stu-id="4a19d-325">Now, let's explore the data and run some queries using **Squirrel SQL**, a graphical tool that lets you interact with databases via a JDBC driver.</span></span>

<span data-ttu-id="4a19d-326">Para comenzar, inicie SQL Squirrel desde el menú de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4a19d-326">To get started, launch Squirrel SQL from the Applications menu.</span></span> <span data-ttu-id="4a19d-327">Para configurar el controlador:</span><span class="sxs-lookup"><span data-stu-id="4a19d-327">To set up the driver:</span></span>

* <span data-ttu-id="4a19d-328">Seleccione **Windows** y luego **View Drivers** (Ver controladores).</span><span class="sxs-lookup"><span data-stu-id="4a19d-328">Select **Windows**, then **View Drivers**.</span></span>
* <span data-ttu-id="4a19d-329">Haga clic con el botón derecho en **PostgreSQL** y seleccione **Modify Driver** (Modificar controlador).</span><span class="sxs-lookup"><span data-stu-id="4a19d-329">Right-click on **PostgreSQL** and select **Modify Driver**.</span></span>
* <span data-ttu-id="4a19d-330">Seleccione **Extra Class Path** (Ruta de clase adicional) y luego **Add** (Agregar).</span><span class="sxs-lookup"><span data-stu-id="4a19d-330">Select **Extra Class Path**, then **Add**.</span></span>
* <span data-ttu-id="4a19d-331">Escriba ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** para **File Name** (Nombre de archivo) y</span><span class="sxs-lookup"><span data-stu-id="4a19d-331">Enter ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** for the **File Name** and</span></span>
* <span data-ttu-id="4a19d-332">seleccione **Open**(Abrir).</span><span class="sxs-lookup"><span data-stu-id="4a19d-332">Select **Open**.</span></span>
* <span data-ttu-id="4a19d-333">Elija List Drivers (Mostrar controladores) y seleccione **org.postgresql.Driver** en **Class Name** (Nombre de clase), a continuación, seleccione **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="4a19d-333">Choose List Drivers, then select **org.postgresql.Driver** in **Class Name**, and select **OK**.</span></span>

<span data-ttu-id="4a19d-334">Para configurar la conexión al servidor local:</span><span class="sxs-lookup"><span data-stu-id="4a19d-334">To set up the connection to the local server:</span></span>

* <span data-ttu-id="4a19d-335">Seleccione **Windows** y luego **View Aliases** (Ver alias).</span><span class="sxs-lookup"><span data-stu-id="4a19d-335">Select **Windows**, then **View Aliases.**</span></span>
* <span data-ttu-id="4a19d-336">Elija el botón **+** para crear un nuevo alias.</span><span class="sxs-lookup"><span data-stu-id="4a19d-336">Choose the **+** button to make a new alias.</span></span>
* <span data-ttu-id="4a19d-337">Asígnele el nombre *Spam database* (Base de datos de correo no deseado) y elija **PostgreSQL** en la lista desplegable **Driver** (Controlador).</span><span class="sxs-lookup"><span data-stu-id="4a19d-337">Name it *Spam database*, choose **PostgreSQL** in the **Driver** drop-down.</span></span>
* <span data-ttu-id="4a19d-338">Establezca la dirección URL en *jdbc:postgresql://localhost/spam*.</span><span class="sxs-lookup"><span data-stu-id="4a19d-338">Set the URL to *jdbc:postgresql://localhost/spam*.</span></span>
* <span data-ttu-id="4a19d-339">Escriba su *nombre de usuario* y *contraseña*.</span><span class="sxs-lookup"><span data-stu-id="4a19d-339">Enter your *username* and *password*.</span></span>
* <span data-ttu-id="4a19d-340">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4a19d-340">Click **OK**.</span></span>
* <span data-ttu-id="4a19d-341">Para abrir la ventana **Connection** (Conexión), haga doble clic en el alias ***Spam database*** (Base de datos de correo no deseado).</span><span class="sxs-lookup"><span data-stu-id="4a19d-341">To open the **Connection** window, double-click the ***Spam database*** alias.</span></span>
* <span data-ttu-id="4a19d-342">Seleccione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="4a19d-342">Select **Connect**.</span></span>

<span data-ttu-id="4a19d-343">Para ejecutar algunas consultas:</span><span class="sxs-lookup"><span data-stu-id="4a19d-343">To run some queries:</span></span>

* <span data-ttu-id="4a19d-344">Seleccione la pestaña **SQL** .</span><span class="sxs-lookup"><span data-stu-id="4a19d-344">Select the **SQL** tab.</span></span>
* <span data-ttu-id="4a19d-345">Escriba una consulta sencilla, por ejemplo `SELECT * from data;` en el cuadro de texto de consulta en la parte superior de la pestaña SQL.</span><span class="sxs-lookup"><span data-stu-id="4a19d-345">Enter a simple query such as `SELECT * from data;` in the query textbox at the top of the SQL tab.</span></span>
* <span data-ttu-id="4a19d-346">Presione **Ctrl + Entrar** para ejecutarla.</span><span class="sxs-lookup"><span data-stu-id="4a19d-346">Press **Ctrl-Enter** to run it.</span></span> <span data-ttu-id="4a19d-347">Squirrel SQL devuelve de forma predeterminada las 100 primeras filas de la consulta.</span><span class="sxs-lookup"><span data-stu-id="4a19d-347">By default Squirrel SQL returns the first 100 rows from your query.</span></span>

<span data-ttu-id="4a19d-348">Hay muchas más consultas que se podrían ejecutar para explorar estos datos.</span><span class="sxs-lookup"><span data-stu-id="4a19d-348">There are many more queries you could run to explore this data.</span></span> <span data-ttu-id="4a19d-349">Por ejemplo, ¿de qué modo la frecuencia de la palabra *make* es diferente en es correo no deseado y no es correo no deseado?</span><span class="sxs-lookup"><span data-stu-id="4a19d-349">For example, how does the frequency of the word *make* differ between spam and ham?</span></span>

    SELECT avg(word_freq_make), spam from data group by spam;

<span data-ttu-id="4a19d-350">O, ¿cuáles son las características del correo electrónico que con frecuencia contiene *3d*?</span><span class="sxs-lookup"><span data-stu-id="4a19d-350">Or what are the characteristics of email that frequently contain *3d*?</span></span>

    SELECT * from data order by word_freq_3d desc;

<span data-ttu-id="4a19d-351">La mayoría de los correos electrónicos en los que aparece *3d* con frecuencia es aparentemente correo no deseado, así que podría ser una característica útil para crear un modelo predictivo para clasificar los correos electrónicos.</span><span class="sxs-lookup"><span data-stu-id="4a19d-351">Most emails that have a high occurrence of *3d* are apparently spam, so it could be a useful feature for building a predictive model to classify the emails.</span></span>

<span data-ttu-id="4a19d-352">Si quisiera realizar aprendizaje automático con datos almacenados en una base de datos de PostgreSQL, podría usar [MADlib](http://madlib.incubator.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="4a19d-352">If you wanted to perform machine learning with data stored in a PostgreSQL database, consider using [MADlib](http://madlib.incubator.apache.org/).</span></span>

## <a name="sql-server-data-warehouse"></a><span data-ttu-id="4a19d-353">SQL Server Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4a19d-353">SQL Server Data Warehouse</span></span>
<span data-ttu-id="4a19d-354">Almacenamiento de datos SQL de Azure es una base de datos de escalado horizontal y basada en la nube capaz de procesar volúmenes masivos de datos (tanto relacionales como no relacionales).</span><span class="sxs-lookup"><span data-stu-id="4a19d-354">Azure SQL Data Warehouse is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span> <span data-ttu-id="4a19d-355">Para más información, consulte [¿Qué es Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="4a19d-355">For more information, see [What is Azure SQL Data Warehouse?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)</span></span>

<span data-ttu-id="4a19d-356">Para conectarse al almacén de datos y crear la tabla, ejecute el siguiente comando desde un símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="4a19d-356">To connect to the data warehouse and create the table, run the following command from a command prompt:</span></span>

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

<span data-ttu-id="4a19d-357">A continuación, en el símbolo del sistema de sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="4a19d-357">Then at the sqlcmd prompt:</span></span>

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

<span data-ttu-id="4a19d-358">Copie los datos con bcp:</span><span class="sxs-lookup"><span data-stu-id="4a19d-358">Copy data with bcp:</span></span>

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> <span data-ttu-id="4a19d-359">Los extremos de las líneas en el archivo descargable son de estilo Windows, pero bcp espera estilo UNIX, por lo que debemos indicar a bcp que con la marca -r.</span><span class="sxs-lookup"><span data-stu-id="4a19d-359">The line endings in the downloaded file are Windows-style, but bcp expects UNIX-style, so we need to tell bcp that with the -r flag.</span></span>
>
>

<span data-ttu-id="4a19d-360">Y la consulta con sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="4a19d-360">And query with sqlcmd:</span></span>

    select top 10 spam, char_freq_dollar from spam;
    GO

<span data-ttu-id="4a19d-361">También puede consultar con Squirrel SQL.</span><span class="sxs-lookup"><span data-stu-id="4a19d-361">You could also query with Squirrel SQL.</span></span> <span data-ttu-id="4a19d-362">Siga pasos similares para PostgreSQL, mediante el controlador JDBC de Microsoft MSSQL Server, que se puede encontrar en ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span><span class="sxs-lookup"><span data-stu-id="4a19d-362">Follow similar steps for PostgreSQL, using the Microsoft MSSQL Server JDBC Driver, which can be found in ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a19d-363">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4a19d-363">Next steps</span></span>
<span data-ttu-id="4a19d-364">Para ver una introducción de los temas que lo guiarán por las tareas que componen el proceso de ciencia de datos en Azure, consulte [Proceso de ciencia de los datos en equipos (TDSP)](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="4a19d-364">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="4a19d-365">Para ver una descripción de otros tutoriales completos que demuestren los pasos del proceso de ciencia de los datos en equipo en escenarios concretos, consulte [Tutoriales del proceso de ciencia de datos en equipos](data-science-process-walkthroughs.md).</span><span class="sxs-lookup"><span data-stu-id="4a19d-365">For a description of other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios, see [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md).</span></span> <span data-ttu-id="4a19d-366">En los tutoriales también se muestra cómo combinar servicios y herramientas en la nube y locales en un flujo de trabajo o una canalización con el fin de crear una aplicación inteligente.</span><span class="sxs-lookup"><span data-stu-id="4a19d-366">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span></span>
