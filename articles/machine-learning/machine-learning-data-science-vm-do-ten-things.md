---
title: acciones de aaaTen que puede realizar en Hola Data Science Virtual Machine | Documentos de Microsoft
description: "Realizar diversas exploración de datos y tareas de modelado en ciencia de datos de hello Máquina Virtual."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 145dfe3e-2bd2-478f-9b6e-99d97d789c62
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;weig;bradsev
ms.openlocfilehash: 4dfe22f14f00208c63e26ce44b05123c9ac4b850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a><span data-ttu-id="44d9a-103">Diez cosas que puede hacer en la ciencia de datos de hello Máquina Virtual</span><span class="sxs-lookup"><span data-stu-id="44d9a-103">Ten things you can do on hello Data science Virtual Machine</span></span>
<span data-ttu-id="44d9a-104">Hola Máquina Virtual de ciencia de datos de Microsoft (DSVM) es un entorno de desarrollo de ciencia de datos eficaz que permite tooperform diversas tareas de exploración y el modelado de datos.</span><span class="sxs-lookup"><span data-stu-id="44d9a-104">hello Microsoft Data Science Virtual Machine (DSVM) is a powerful data science development environment that enables you tooperform various data exploration and modeling tasks.</span></span> <span data-ttu-id="44d9a-105">Hello entorno viene ya compilado e integrados con datos muy popular varias herramientas de análisis que hacen que sea fácil tooget a trabajar rápidamente con el análisis local, en la nube o híbridas implementaciones.</span><span class="sxs-lookup"><span data-stu-id="44d9a-105">hello environment comes already built and bundled with several popular data analytics tools that make it easy tooget started quickly with your analysis for On-premises, Cloud or hybrid deployments.</span></span> <span data-ttu-id="44d9a-106">Hola DSVM trabaja en estrecha colaboración con muchos servicios de Azure y es capaz de tooread y procesar los datos que ya está almacenados en Azure, en almacenamiento de datos de SQL Azure Data Lake de Azure, almacenamiento de Azure, o en la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="44d9a-106">hello DSVM works closely with many Azure services and is able tooread and process data that is already stored on Azure, in Azure SQL Data Warehouse, Azure Data Lake, Azure Storage, or in Azure Cosmos DB.</span></span> <span data-ttu-id="44d9a-107">También puede sacar provecho de otras herramientas de análisis como Aprendizaje automático de Azure y Data Factory de Azure.</span><span class="sxs-lookup"><span data-stu-id="44d9a-107">It can also leverage other analytics tools such as Azure Machine Learning and Azure Data Factory.</span></span>

<span data-ttu-id="44d9a-108">En este artículo se le guiará por el proceso de toouse su tooperform DSVM ciencia de datos de varias tareas e interactuar con otros servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="44d9a-108">In this article we walk you through how toouse your DSVM tooperform various data science tasks and interact with other Azure services.</span></span> <span data-ttu-id="44d9a-109">Estas son algunas de las acciones de Hola que puede realizar en hello DSVM:</span><span class="sxs-lookup"><span data-stu-id="44d9a-109">Here are some of hello things you can do on hello DSVM:</span></span>

1. <span data-ttu-id="44d9a-110">Explorar datos y desarrollar modelos de forma local en hello DSVM mediante Microsoft R Server, Python</span><span class="sxs-lookup"><span data-stu-id="44d9a-110">Explore data and develop models locally on hello DSVM using Microsoft R Server, Python</span></span>
2. <span data-ttu-id="44d9a-111">Usar un tooexperiment de Jupyter notebook con los datos en un explorador utilizando una versión lista de enterprise de R diseñado para escalabilidad y rendimiento de Python 2, 3 de Python, Microsoft R</span><span class="sxs-lookup"><span data-stu-id="44d9a-111">Use a Jupyter notebook tooexperiment with your data on a browser using Python 2, Python 3, Microsoft R an enterprise ready version of R designed for scalability and performance</span></span>
3. <span data-ttu-id="44d9a-112">Poner en operación los modelos creados con R y Python en Aprendizaje automático de Azure para que aplicaciones cliente puedan tener acceso a los modelos mediante una sencilla interfaz de servicios web</span><span class="sxs-lookup"><span data-stu-id="44d9a-112">Operationalize models built using R and Python on Azure Machine Learning so client applications can access your models using a simple web services interface</span></span>
4. <span data-ttu-id="44d9a-113">Administrar los recursos de Azure mediante Azure Portal o PowerShell</span><span class="sxs-lookup"><span data-stu-id="44d9a-113">Administer your Azure resources using  Azure portal or Powershell</span></span>
5. <span data-ttu-id="44d9a-114">Ampliar el espacio de almacenamiento y compartir código o conjuntos de datos de gran escala entre todo el equipo mediante la creación de almacenamiento de archivos de Azure como una unidad que se puede montar en la máquina virtual de ciencia de datos (DSVM)</span><span class="sxs-lookup"><span data-stu-id="44d9a-114">Extend your storage space and share large-scale datasets / code across your whole team by creating an Azure File storage as a mountable drive on your DSVM</span></span>
6. <span data-ttu-id="44d9a-115">Compartir código con su equipo mediante GitHub y obtener acceso a su repositorio mediante Hola preinstalados clientes Git - Git Bash, Git GUI.</span><span class="sxs-lookup"><span data-stu-id="44d9a-115">Share code with your team using GitHub and access your repository using hello pre-installed Git clients - Git Bash, Git GUI.</span></span>
7. <span data-ttu-id="44d9a-116">Acceder a diversos servicios de análisis y datos de Azure, como Azure Blob Storage, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse y bases de datos</span><span class="sxs-lookup"><span data-stu-id="44d9a-116">Access various Azure data and analytics services like Azure blob storage, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse & databases</span></span>
8. <span data-ttu-id="44d9a-117">Crear informes y panel con Power BI Desktop preinstalado en hello DSVM Hola e implementarlas en la nube de Hola</span><span class="sxs-lookup"><span data-stu-id="44d9a-117">Build reports and dashboard using hello Power BI Desktop pre-installed on hello DSVM and deploy them on hello cloud</span></span>
9. <span data-ttu-id="44d9a-118">Escalar dinámicamente su toomeet DSVM que su proyecto necesite</span><span class="sxs-lookup"><span data-stu-id="44d9a-118">Dynamically scale your DSVM toomeet your project needs</span></span>
10. <span data-ttu-id="44d9a-119">Instalar herramientas adicionales en la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="44d9a-119">Install additional tools on your virtual machine</span></span>   

> [!NOTE]
> <span data-ttu-id="44d9a-120">Se aplican cargos de uso adicionales para muchos de los servicios de almacenamiento y análisis de la datos adicionales de hello enumerados en este artículo.</span><span class="sxs-lookup"><span data-stu-id="44d9a-120">Additional usage charges apply for many of hello additional data storage and analytics services listed in this article.</span></span> <span data-ttu-id="44d9a-121">Consulte toohello [precios de Azure](https://azure.microsoft.com/pricing/) página para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="44d9a-121">Please refer toohello [Azure Pricing](https://azure.microsoft.com/pricing/) page for details.</span></span>
> 
> 

<span data-ttu-id="44d9a-122">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="44d9a-122">**Prerequisites**</span></span>

* <span data-ttu-id="44d9a-123">Necesita una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="44d9a-123">You need an Azure subscription.</span></span> <span data-ttu-id="44d9a-124">Puede suscribirse a una evaluación gratuita [aquí](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="44d9a-124">You can sign up for a free trial [here](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="44d9a-125">Las instrucciones para el aprovisionamiento de un Data Science Virtual Machine en hello portal de Azure están disponibles en [crear una máquina virtual](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="44d9a-125">Instructions for provisioning a Data Science Virtual Machine on hello Azure portal are available at [Creating a virtual machine](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span></span>

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a><span data-ttu-id="44d9a-126">1. Explorar datos y desarrollar modelos con el Servidor R de Microsoft o Python</span><span class="sxs-lookup"><span data-stu-id="44d9a-126">1. Explore data and develop models using Microsoft R Server or Python</span></span>
<span data-ttu-id="44d9a-127">Puede usar los análisis de datos de lenguajes como toodo R y Python derecha en hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="44d9a-127">You can use languages like R and Python toodo your data analytics right on hello DSVM.</span></span>

<span data-ttu-id="44d9a-128">Para R, puede usar un IDE llamado "Revolution R Enterprise 8.0" que se pueden encontrar en el menú de inicio de Hola o escritorio Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-128">For R, you can use an IDE called "Revolution R Enterprise 8.0" that can be found on hello start menu or hello desktop.</span></span> <span data-ttu-id="44d9a-129">Microsoft ofrece bibliotecas adicionales además de los Hola abierto tooenable de origen/CRAN-R escalable hello y análisis de capacidad tooanalyze datos mayor que el tamaño de memoria de hello permitido realizando análisis en paralelo fragmentado.</span><span class="sxs-lookup"><span data-stu-id="44d9a-129">Microsoft has provided additional libraries on top of hello Open source/CRAN-R tooenable scalable analytics and hello ability tooanalyze data larger than hello memory size allowed by doing parallel chunked analysis.</span></span> <span data-ttu-id="44d9a-130">También puede instalar el IDE de R que prefiera, como [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span><span class="sxs-lookup"><span data-stu-id="44d9a-130">You can also install an R IDE of your choice like [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span></span>

<span data-ttu-id="44d9a-131">Para Python, puede usar un IDE como Visual Studio Community Edition que tiene Hola Python Tools para la extensión de Visual Studio (PTVS) preinstalado.</span><span class="sxs-lookup"><span data-stu-id="44d9a-131">For Python, you can use an IDE like Visual Studio Community Edition which has hello Python Tools for Visual Studio (PTVS) extension pre-installed.</span></span> <span data-ttu-id="44d9a-132">De forma predeterminada, en PTVS solo está configurada una versión básica de Python 2.7 (sin ninguna biblioteca de análisis como SciKit o Pandas).</span><span class="sxs-lookup"><span data-stu-id="44d9a-132">By default, only a basic Python 2.7 is configured on PTVS (without any analytics library like SciKit, Pandas).</span></span> <span data-ttu-id="44d9a-133">En orden tooenable Anaconda Python 2.7 y 3.5, necesita toodo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="44d9a-133">In order tooenable Anaconda Python 2.7 and 3.5, you need toodo hello following:</span></span>

* <span data-ttu-id="44d9a-134">Crear entornos personalizados para cada versión desplazándose demasiado**herramientas** -> **Python Tools** -> **entornos de Python** y, a continuación, haga clic en " **+ Personalizado**"en Visual Studio 2015 Community Edition Hola</span><span class="sxs-lookup"><span data-stu-id="44d9a-134">Create custom environments for each version by navigating too**Tools** -> **Python Tools** -> **Python Environments** and then clicking "**+ Custom**" in hello Visual Studio 2015 Community Edition</span></span>
* <span data-ttu-id="44d9a-135">Escriba una descripción y establezca el entorno de hello las rutas de acceso de prefijo como *c:\anaconda* Anaconda Python 2.7 o *c:\anaconda\envs\py35* para Anaconda Python 3.5</span><span class="sxs-lookup"><span data-stu-id="44d9a-135">Give a description and set hello environment prefix paths as *c:\anaconda* for Anaconda Python 2.7 OR *c:\anaconda\envs\py35* for Anaconda Python 3.5</span></span>
* <span data-ttu-id="44d9a-136">Haga clic en **detección automática** y, a continuación, **aplicar** entorno de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="44d9a-136">Click **Auto Detect** and then **Apply** toosave hello environment.</span></span>

<span data-ttu-id="44d9a-137">Esta es la configuración de entorno personalizado Hola aspecto en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="44d9a-137">Here is what hello custom environment setup looks like in Visual Studio.</span></span>

![Programa de instalación de PTVS](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

<span data-ttu-id="44d9a-139">Vea hello [documentación PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) para obtener más información acerca de cómo toocreate entornos de Python.</span><span class="sxs-lookup"><span data-stu-id="44d9a-139">See hello [PTVS documentation](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) for additional details on how toocreate Python Environments.</span></span>

<span data-ttu-id="44d9a-140">Ahora se configuran toocreate un nuevo proyecto de Python.</span><span class="sxs-lookup"><span data-stu-id="44d9a-140">Now you are set up toocreate a new Python project.</span></span> <span data-ttu-id="44d9a-141">Navegue demasiado**archivo** -> **New** -> **proyecto** -> **Python** y seleccione el tipo de saludo de Aplicación de Python que se va a compilar.</span><span class="sxs-lookup"><span data-stu-id="44d9a-141">Navigate too**File** -> **New** -> **Project** -> **Python** and select hello type of Python application you are building.</span></span> <span data-ttu-id="44d9a-142">Se puede establecer el entorno de Python de Hola Hola actual proyecto toohello versión deseada (Anaconda 2.7 o 3.5): Hola contextual **entorno de Python**, seleccione **entornos de Python de agregar o quitar**, y a continuación, seleccione Hola deseado entorno tooassociate con proyecto Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-142">You can set hello Python environment for hello current project toohello desired version (Anaconda 2.7 or 3.5): right-click hello **Python environment**, select **Add/Remove Python Environments**, and then select hello desired environment tooassociate with hello project.</span></span> <span data-ttu-id="44d9a-143">Puede encontrar más información sobre cómo trabajar con PTVS en producto hello [documentación](https://github.com/Microsoft/PTVS/wiki) página.</span><span class="sxs-lookup"><span data-stu-id="44d9a-143">You can find more information about working with PTVS on hello product [documentation](https://github.com/Microsoft/PTVS/wiki) page.</span></span>

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a><span data-ttu-id="44d9a-144">2. Con un modelo y Jupyter Notebook tooexplore sus datos con Python o R</span><span class="sxs-lookup"><span data-stu-id="44d9a-144">2. Using a Jupyter Notebook tooexplore and model your data with Python or R</span></span>
<span data-ttu-id="44d9a-145">Hola Jupyter Notebook es un entorno eficaz que proporciona una basada en explorador "IDE" para el modelado y exploración de datos.</span><span class="sxs-lookup"><span data-stu-id="44d9a-145">hello Jupyter Notebook is a powerful environment that provides a browser-based "IDE" for data exploration and modeling.</span></span> <span data-ttu-id="44d9a-146">Puede utilizar Python 2, 3 de Python o R (código abierto y Hola Microsoft R Server) en Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="44d9a-146">You can use Python 2, Python 3 or R (both Open Source and hello Microsoft R Server) in a Jupyter Notebook.</span></span>

<span data-ttu-id="44d9a-147">Hola toolaunch Jupyter Notebook haga clic en el icono de menú de inicio de Hola / titulada de icono del escritorio **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="44d9a-147">toolaunch hello Jupyter Notebook click on hello start menu icon / desktop icon titled **Jupyter Notebook**.</span></span> <span data-ttu-id="44d9a-148">En hello DSVM también puede examinar demasiado "https://localhost:9999 /" tooaccess Hola Jupiter Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="44d9a-148">On hello DSVM you can also browse too"https://localhost:9999/" tooaccess hello Jupiter Notebook.</span></span> <span data-ttu-id="44d9a-149">Si le pide una contraseña, use las instrucciones proporcionadas en hello ***cómo toocreate una contraseña segura en el servidor de hello Jupyter notebook*** sección de hello [Hola aprovisionar Microsoft Data Science Virtual Machine](machine-learning-data-science-provision-vm.md)tema toocreate contraseña segura tooaccess hello Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="44d9a-149">If it prompts you for a password, use instructions provided in hello ***How toocreate a strong password on hello Jupyter notebook server*** section of hello [Provision hello Microsoft Data Science Virtual Machine](machine-learning-data-science-provision-vm.md) topic toocreate a strong password tooaccess hello Jupyter notebook.</span></span> 

<span data-ttu-id="44d9a-150">Una vez abierto el Bloc de notas de hello, debería ver un directorio que contiene unos blocs de notas de ejemplo que están preconfiguradas en hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="44d9a-150">Once you have opened hello notebook, you should see a directory that contains a few example notebooks that are pre-packaged into hello DSVM.</span></span> <span data-ttu-id="44d9a-151">Ahora puede:</span><span class="sxs-lookup"><span data-stu-id="44d9a-151">Now you can:</span></span>

* <span data-ttu-id="44d9a-152">Haga clic en el código de hello toosee de hello Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="44d9a-152">click on hello notebook toosee hello code.</span></span>
* <span data-ttu-id="44d9a-153">Ejecutar cada celda presionando **MAYÚS+ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="44d9a-153">execute each cell by pressing **SHIFT-ENTER**.</span></span>
* <span data-ttu-id="44d9a-154">ejecutar el Bloc de notas completo Hola haciendo clic en **celda** -> **ejecutar**</span><span class="sxs-lookup"><span data-stu-id="44d9a-154">run hello entire notebook by clicking on **Cell** -> **Run**</span></span>
* <span data-ttu-id="44d9a-155">crear un nuevo bloc de notas haciendo clic en hello Jupyter icono (esquina superior izquierda) y, a continuación, haga clic en **New** botón en hello derecho y, a continuación, elegir el idioma de Bloc de notas de hello (también conocido como kernels).</span><span class="sxs-lookup"><span data-stu-id="44d9a-155">create a new notebook by clicking on hello Jupyter Icon (left top corner) and then clicking **New** button on hello right and then choosing hello notebook language (also known as kernels).</span></span>   

> [!NOTE]
> <span data-ttu-id="44d9a-156">Actualmente admitimos Python 2.7, Python 3.5 y R. kernel Hola R para admitir la programación en código abierto R así como enterprise Hola escalable Microsoft R Server.</span><span class="sxs-lookup"><span data-stu-id="44d9a-156">Currently we support Python 2.7, Python 3.5 and R. hello R kernel supports programming in both Open source R as well as hello enterprise scalable Microsoft R Server.</span></span>   
> 
> 

<span data-ttu-id="44d9a-157">Una vez que esté en el Bloc de notas de Hola puede explorar los datos, generar modelo hello, probar modelo Hola utilizando su elección de bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="44d9a-157">Once you are in hello notebook you can explore your data, build hello model, test hello model using your choice of libraries.</span></span>

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a><span data-ttu-id="44d9a-158">3. Compilación de modelos mediante R y Python, y hacer que estén operativos mediante Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="44d9a-158">3. Build models using R or Python and Operationalize them using Azure Machine Learning</span></span>
<span data-ttu-id="44d9a-159">Una vez que ha creado y ha validado el modelo Hola próximo paso es normalmente toodeploy en producción.</span><span class="sxs-lookup"><span data-stu-id="44d9a-159">Once you have built and validated your model hello next step is usually toodeploy it into production.</span></span> <span data-ttu-id="44d9a-160">Esto permite a su cliente predicciones de modelo de aplicaciones tooinvoke hello en un tiempo real o en una base de modo por lotes.</span><span class="sxs-lookup"><span data-stu-id="44d9a-160">This allows your client applications tooinvoke hello model predictions on a real time or on a batch mode basis.</span></span> <span data-ttu-id="44d9a-161">Aprendizaje automático de Azure proporciona un mecanismo toooperationalize un modelo integrado de R o Python.</span><span class="sxs-lookup"><span data-stu-id="44d9a-161">Azure Machine Learning provides a mechanism toooperationalize a model built in either R or Python.</span></span>

<span data-ttu-id="44d9a-162">Cuando se ponga en acción el modelo de aprendizaje automático de Azure, se expone un servicio web que permite a los clientes toomake llamadas REST que pasan parámetros de entrada y reciban las predicciones de modelo de hello como salidas.</span><span class="sxs-lookup"><span data-stu-id="44d9a-162">When you operationalize your model in Azure Machine Learning, a web service is exposed that allows clients toomake REST calls that pass in input parameters and receive predictions from hello model as outputs.</span></span>   

> [!NOTE]
> <span data-ttu-id="44d9a-163">Si no aún registrarse para el aprendizaje automático de Azure, puede obtener un área de trabajo estándar o un área de trabajo gratuita visitando hello [estudio de aprendizaje automático de Azure](https://studio.azureml.net/) página principal y haga clic en "Introducción".</span><span class="sxs-lookup"><span data-stu-id="44d9a-163">If you have not yet signed up for Azure Machine Learning, you can obtain a free workspace or a standard workspace by visiting hello [Azure Machine Learning Studio](https://studio.azureml.net/) home page and clicking on "Get Started".</span></span>   
> 
> 

### <a name="build-and-operationalize-python-models"></a><span data-ttu-id="44d9a-164">Compilación y puesta en operación de modelos de Python</span><span class="sxs-lookup"><span data-stu-id="44d9a-164">Build and Operationalize Python models</span></span>
<span data-ttu-id="44d9a-165">Este es un fragmento de código desarrollado en Python Jupyter Notebook que compile un modelo simple utilizando biblioteca SciKit: Obtenga información de Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-165">Here is a snippet of code developed in a Python Jupyter Notebook that builds a simple model using hello SciKit-learn library.</span></span>

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

<span data-ttu-id="44d9a-166">método Hello usa toodeploy su tooAzure de modelos de python aprendizaje automático ajusta Hola predicción de modelo de Hola a una función y decora con atributos proporcionados por la biblioteca de python de aprendizaje automático de Azure preinstalada de Hola que indican su equipo de Azure Id. de área de trabajo de aprendizaje y la clave de API, Hola de entrada y devuelven los parámetros.</span><span class="sxs-lookup"><span data-stu-id="44d9a-166">hello method used toodeploy your python models tooAzure Machine Learning wraps hello prediction of hello model into a function and decorates it with attributes provided by hello pre-installed Azure Machine Learning python library that denote your Azure Machine Learning workspace ID, API Key, and hello input and return parameters.</span></span>  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

<span data-ttu-id="44d9a-167">Un cliente ahora puede realizar llamadas toohello web service.</span><span class="sxs-lookup"><span data-stu-id="44d9a-167">A client can now make calls toohello web service.</span></span> <span data-ttu-id="44d9a-168">Hay contenedores de conveniencia que construyen las solicitudes de API de REST de Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-168">There are convenience wrappers that construct hello REST API requests.</span></span> <span data-ttu-id="44d9a-169">Este es un servicio web de ejemplo código tooconsume Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-169">Here is a sample code tooconsume hello web service.</span></span>

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> <span data-ttu-id="44d9a-170">biblioteca de aprendizaje automático de Azure Hola solo se admite actualmente en Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="44d9a-170">hello Azure Machine Learning library is only supported on Python 2.7 currently.</span></span>   
> 
> 

### <a name="build-and-operationalize-r-models"></a><span data-ttu-id="44d9a-171">Compilación y puesta en operación de modelos de R</span><span class="sxs-lookup"><span data-stu-id="44d9a-171">Build and Operationalize R models</span></span>
<span data-ttu-id="44d9a-172">Puede implementar modelos de R generados en hello Data Science Virtual Machine o en otro lugar en aprendizaje automático de Azure de forma que sea similar toohow se realiza para Python.</span><span class="sxs-lookup"><span data-stu-id="44d9a-172">You can deploy R models built on hello Data Science Virtual Machine or elsewhere onto Azure Machine Learning in a manner that is similar toohow it is done for Python.</span></span> <span data-ttu-id="44d9a-173">Su Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="44d9a-173">Her are hello steps:</span></span>

* <span data-ttu-id="44d9a-174">crear un tooprovide de archivo settings.json el Id. de área de trabajo y la autenticación de token tal y como se muestra en el siguiente ejemplo de código de hello.</span><span class="sxs-lookup"><span data-stu-id="44d9a-174">create a settings.json file tooprovide your workspace ID and auth token as shown in hello following code sample.</span></span>
* <span data-ttu-id="44d9a-175">escribir un contenedor para el modelo de hello predict, función.</span><span class="sxs-lookup"><span data-stu-id="44d9a-175">write a wrapper for hello model's predict function.</span></span>
* <span data-ttu-id="44d9a-176">llamar a ```publishWebService``` en hello toopass de biblioteca de aprendizaje automático de Azure en el contenedor de la función de Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-176">call ```publishWebService``` in hello Azure Machine Learning library toopass in hello function wrapper.</span></span>  

<span data-ttu-id="44d9a-177">Aquí es Hola procedimiento y fragmentos de código que pueden ser usado tooset up, compilar, publicar y consumir un modelo como un servicio web de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="44d9a-177">Here is hello procedure and code snippets that can be used tooset up, build, publish, and consume a model as a web service in Azure Machine Learning.</span></span>

#### <a name="setup"></a><span data-ttu-id="44d9a-178">Configuración</span><span class="sxs-lookup"><span data-stu-id="44d9a-178">Setup</span></span>
1. <span data-ttu-id="44d9a-179">Instalar paquetes de R de aprendizaje de máquina de hello escribiendo ```install.packages("AzureML")``` en Revolution R Enterprise 8.0 IDE o en el IDE de R.</span><span class="sxs-lookup"><span data-stu-id="44d9a-179">Install hello Machine Learning R package by typing ```install.packages("AzureML")``` in Revolution R Enterprise 8.0 IDE or your R IDE.</span></span>
2. <span data-ttu-id="44d9a-180">Descargue la RTools de [aquí](https://cran.r-project.org/bin/windows/Rtools/).</span><span class="sxs-lookup"><span data-stu-id="44d9a-180">Download RTools from [here](https://cran.r-project.org/bin/windows/Rtools/).</span></span> <span data-ttu-id="44d9a-181">Debe Hola zip utilidad en la ruta de acceso de hello (y con nombre zip.exe) toooperationalize el paquete de R en aprendizaje automático.</span><span class="sxs-lookup"><span data-stu-id="44d9a-181">You need hello zip utility in hello path (and named zip.exe) toooperationalize your R package into Machine Learning.</span></span>
3. <span data-ttu-id="44d9a-182">Crear un archivo settings.json en un directorio denominado ```.azureml``` en su directorio particular y escriba los parámetros de Hola desde el área de trabajo de aprendizaje automático de Azure:</span><span class="sxs-lookup"><span data-stu-id="44d9a-182">Create a settings.json file under a directory called ```.azureml``` under your home directory and enter hello parameters from your Azure Machine Learning workspace:</span></span>

<span data-ttu-id="44d9a-183">Estructura del archivo settings.json:</span><span class="sxs-lookup"><span data-stu-id="44d9a-183">settings.json File structure:</span></span>

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a><span data-ttu-id="44d9a-184">Creación de un modelo en R y posterior publicación en Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="44d9a-184">Build a model in R and publish it in Azure Machine Learning</span></span>
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function toopublish based on hello model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a><span data-ttu-id="44d9a-185">Consumir el modelo de hello implementado en aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="44d9a-185">Consume hello model deployed in Azure Machine Learning</span></span>
<span data-ttu-id="44d9a-186">modelo de hello tooconsume desde una aplicación cliente, usamos toolook de biblioteca de aprendizaje automático de Azure Hola seguridad Hola servicio web publicado por nombre usando hello `services` el punto de conexión de API llamada toodetermine Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-186">tooconsume hello model from a client application, we use hello Azure Machine Learning library toolook up hello published web service by name using hello `services` API call toodetermine hello endpoint.</span></span> <span data-ttu-id="44d9a-187">A continuación, se llame a hello `consume` función y pase Hola datos marco toobe predicho.</span><span class="sxs-lookup"><span data-stu-id="44d9a-187">Then you just call hello `consume` function and pass in hello data frame toobe predicted.</span></span>
<span data-ttu-id="44d9a-188">Hola siguiente código es el modelo de Hola de tooconsume usado publicado como un servicio web de aprendizaje automático de Azure.</span><span class="sxs-lookup"><span data-stu-id="44d9a-188">hello following code is used tooconsume hello model published as an Azure Machine Learning web service.</span></span>

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

<span data-ttu-id="44d9a-189">Puede encontrar más información acerca de la biblioteca de R de aprendizaje de máquina de Azure de hello [aquí](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span><span class="sxs-lookup"><span data-stu-id="44d9a-189">More information about hello Azure Machine Learning R library can be found [here](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span></span>

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a><span data-ttu-id="44d9a-190">4. Administrar los recursos de Azure mediante el Portal de Azure o PowerShell</span><span class="sxs-lookup"><span data-stu-id="44d9a-190">4. Administer your Azure resources using Azure portal or Powershell</span></span>
<span data-ttu-id="44d9a-191">Hola DSVM no solo permite toobuild la solución de análisis de forma local en Hola máquina virtual, pero también permite tooaccess servicios en la nube de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="44d9a-191">hello DSVM not only allows you toobuild your analytics solution locally on hello virtual machine, but also allows you tooaccess services on Microsoft's Azure cloud.</span></span> <span data-ttu-id="44d9a-192">Azure proporciona varios servicios de proceso, almacenamiento, análisis de datos y de otra índole que puede administrar desde su DSVM y a los que puede tener acceso desde dicho entorno.</span><span class="sxs-lookup"><span data-stu-id="44d9a-192">Azure provides several compute, storage, data analytics services and other services that you can administer and access from your DSVM.</span></span>

<span data-ttu-id="44d9a-193">tooadminister los recursos de nube y suscripción Azure puede usar el explorador y el punto de toothe [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="44d9a-193">tooadminister your Azure subscription and cloud resources you can use your browser and point toothe [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="44d9a-194">También puede usar Azure Powershell tooadminister su suscripción de Azure y sus recursos a través de una secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="44d9a-194">You can also use Azure Powershell tooadminister your Azure subscription and resources via a script.</span></span>
<span data-ttu-id="44d9a-195">Puede ejecutar Powershell de Azure desde un acceso directo en el escritorio de Hola o de hello iniciar menú titulada "Microsoft Azure Powershell".</span><span class="sxs-lookup"><span data-stu-id="44d9a-195">You can run Azure Powershell from a shortcut on hello desktop or from hello start menu titled "Microsoft Azure Powershell".</span></span> <span data-ttu-id="44d9a-196">Para obtener más información sobre cómo administrar su suscripción y los recursos de Azure mediante los scripts de Windows PowerShell, consulte la [documentación de Microsoft Azure PowerShell](../powershell-azure-resource-manager.md) .</span><span class="sxs-lookup"><span data-stu-id="44d9a-196">Refer to [Microsoft Azure Powershell documentation](../powershell-azure-resource-manager.md) for more information on how you can administer your Azure subscription and resources using Windows Powershell scripts.</span></span>

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a><span data-ttu-id="44d9a-197">5. Ampliar el espacio de almacenamiento con un sistema de archivos compartidos</span><span class="sxs-lookup"><span data-stu-id="44d9a-197">5. Extend your storage space with a shared file system</span></span>
<span data-ttu-id="44d9a-198">Pueden compartir los científicos de datos grandes conjuntos de datos, código u otros recursos en el equipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-198">Data scientists can share large datasets, code or other resources within hello team.</span></span> <span data-ttu-id="44d9a-199">Hola DSVM propio tiene unos 70GB de espacio disponible.</span><span class="sxs-lookup"><span data-stu-id="44d9a-199">hello DSVM itself has about 70GB of space available.</span></span> <span data-ttu-id="44d9a-200">tooextend su almacenamiento, puede usar Hola servicio de archivos de Azure y montar en hello DSVM o tener acceso a él a través de una API de REST.</span><span class="sxs-lookup"><span data-stu-id="44d9a-200">tooextend your storage, you can use hello Azure File Service and either mount it on hello DSVM or access it via a REST API.</span></span>   

> [!NOTE]
> <span data-ttu-id="44d9a-201">Hola el espacio máximo del recurso compartido de servicio de archivos de Azure de hello es 5TB y límite de tamaño de archivo individual es 1TB.</span><span class="sxs-lookup"><span data-stu-id="44d9a-201">hello maximum space of hello Azure File Service share is 5TB and individual file size limit is 1TB.</span></span>   
> 
> 

<span data-ttu-id="44d9a-202">Puede usar Azure Powershell toocreate un recurso compartido de servicio de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="44d9a-202">You can use Azure Powershell toocreate an Azure File Service share.</span></span> <span data-ttu-id="44d9a-203">Aquí es toorun de script de Hola en Azure PowerShell toocreate un recurso compartido de servicio de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="44d9a-203">Here is hello script toorun under Azure PowerShell toocreate an Azure File service share.</span></span>

    # Authenticate tooAzure.
    Login-AzureRmAccount
    # Select your subscription
    Get-AzureRmSubscription –SubscriptionName "<your subscription name>" | Select-AzureRmSubscription
    # Create a new resource group.
    New-AzureRmResourceGroup -Name <dsvmdatarg>
    # Create a new storage account. You can reuse existing storage account if you wish.
    New-AzureRmStorageAccount -Name <mydatadisk> -ResourceGroupName <dsvmdatarg> -Location "<Azure Data Center Name For eg. South Central US>" -Type "Standard_LRS"
    # Set your current working storage account
    Set-AzureRmCurrentStorageAccount –ResourceGroupName "<dsvmdatarg>" –StorageAccountName <mydatadisk>

    # Create a Azure File Service Share
    $s = New-AzureStorageShare <<teamsharename>>
    # Create a directory under hello FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List hello share tooconfirm that everything worked
    Get-AzureStorageFile -Share $s


<span data-ttu-id="44d9a-204">Ahora que ha creado un recurso compartido de archivos de Azure, puede montarlo en cualquier máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="44d9a-204">Now that you have created an Azure file share, you can mount it in any virtual machine in Azure.</span></span> <span data-ttu-id="44d9a-205">Se recomienda que Hola VM sea en el mismo centro de datos de Azure como la latencia de tooavoid de cuenta de almacenamiento de Hola y datos gastos de transferencia.</span><span class="sxs-lookup"><span data-stu-id="44d9a-205">It is highly recommended that hello VM is in same Azure data center as hello storage account tooavoid latency and data transfer charges.</span></span> <span data-ttu-id="44d9a-206">Presentamos unidad de hello comandos toomount hello en hello DSVM que se pueden ejecutar en Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="44d9a-206">Here are hello commands toomount hello drive on hello DSVM that you can run on Azure Powershell.</span></span>

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


<span data-ttu-id="44d9a-207">Ahora puede tener acceso a esta unidad tal y como lo haría con cualquier unidad normal en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="44d9a-207">Now you can access this drive as you would any normal drive on hello VM.</span></span>

## <a name="6-share-code-with-your-team-using-github"></a><span data-ttu-id="44d9a-208">6. Compartir código con su equipo mediante GitHub</span><span class="sxs-lookup"><span data-stu-id="44d9a-208">6. Share code with your team using GitHub</span></span>
<span data-ttu-id="44d9a-209">GitHub es un repositorio de código donde puede encontrar una gran cantidad de código de ejemplo y orígenes para distintas herramientas con varias tecnologías compartidas por la Comunidad de desarrolladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-209">GitHub is a code repository where you can find a lot of sample code and sources for different tools using various technologies shared by hello developer community.</span></span> <span data-ttu-id="44d9a-210">Utiliza Git como Hola versiones de tecnología tootrack y el almacén de archivos de código de hello.</span><span class="sxs-lookup"><span data-stu-id="44d9a-210">It uses Git as hello technology tootrack and store versions of hello code files.</span></span> <span data-ttu-id="44d9a-211">GitHub es también una plataforma donde puede crear su propios toostore repositorio código compartido de su equipo y la documentación, implementar el control de versiones y también controlar quién tiene acceso tooview y contribuir en el código.</span><span class="sxs-lookup"><span data-stu-id="44d9a-211">GitHub is also a platform where you can create your own repository toostore your team's shared code and documentation, implement version control and also control who have access tooview and contribute code.</span></span> <span data-ttu-id="44d9a-212">Visite hello [páginas de Ayuda de GitHub](https://help.github.com/) para obtener más información sobre el uso de Git.</span><span class="sxs-lookup"><span data-stu-id="44d9a-212">Please visit hello [GitHub help pages](https://help.github.com/) for more information on using Git.</span></span> <span data-ttu-id="44d9a-213">Puede usar GitHub como uno de hello formas toocollaborate con su equipo, utilice el código desarrollado por la Comunidad de Hola y contribuir código toohello atrás Comunidad.</span><span class="sxs-lookup"><span data-stu-id="44d9a-213">You can use GitHub as one of hello ways toocollaborate with your team, use code developed by hello community and contribute code back toohello community.</span></span>

<span data-ttu-id="44d9a-214">Hola DSVM ya viene cargado con las herramientas de cliente en la línea de comandos como bien GUI tooaccess repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="44d9a-214">hello DSVM already comes loaded with client tools on both command-line as well GUI tooaccess GitHub repository.</span></span> <span data-ttu-id="44d9a-215">Hola toowork de herramienta de línea de comandos con Git y GitHub se denomina Git Bash.</span><span class="sxs-lookup"><span data-stu-id="44d9a-215">hello command-line tool toowork with Git and GitHub is called Git Bash.</span></span> <span data-ttu-id="44d9a-216">Visual Studio instalada en hello DSVM tiene extensiones de Git de Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-216">Visual Studio installed on hello DSVM has hello Git extensions.</span></span> <span data-ttu-id="44d9a-217">Puede encontrar iconos de inicio para estas herramientas en el menú de inicio de Hola y de escritorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-217">You can find start-up icons for these tools on hello start menu and hello desktop.</span></span>

<span data-ttu-id="44d9a-218">código de toodownload desde un repositorio de GitHub usar hello ```git clone``` comando.</span><span class="sxs-lookup"><span data-stu-id="44d9a-218">toodownload code from a GitHub repository you use hello ```git clone``` command.</span></span> <span data-ttu-id="44d9a-219">Por ejemplo repositorio de ciencia de datos toodownload publicado por Microsoft en el directorio actual de hello puede ejecutar Hola siguiente comando una vez que esté en ```git-bash```.</span><span class="sxs-lookup"><span data-stu-id="44d9a-219">For example toodownload data science repository published by Microsoft into hello current directory you can run hello following command once you are in ```git-bash```.</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="44d9a-220">En Visual Studio, puede hacerlo Hola la misma operación de clonación.</span><span class="sxs-lookup"><span data-stu-id="44d9a-220">In Visual Studio, you can do hello same clone operation.</span></span> <span data-ttu-id="44d9a-221">Hola siguiente captura de pantalla muestra cómo tooaccess Git y GitHub herramientas en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="44d9a-221">hello  following screen-shot shows how tooaccess Git and GitHub tools in Visual Studio.</span></span>

![GIT en Visual Studio](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

<span data-ttu-id="44d9a-223">Puede encontrar más información sobre cómo usar Git toowork con su repositorio de GitHub de varios recursos disponibles en github.com. Hola [hoja de referencia](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) es una referencia útil.</span><span class="sxs-lookup"><span data-stu-id="44d9a-223">You can find more information on using Git toowork with your GitHub repository from several resources available on github.com. hello [cheat sheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) is a useful reference.</span></span>

## <a name="7-access-various-azure-data-and-analytics-services"></a><span data-ttu-id="44d9a-224">7. Obtener acceso a diversos servicios de análisis y datos de Azure</span><span class="sxs-lookup"><span data-stu-id="44d9a-224">7. Access various Azure data and analytics services</span></span>
### <a name="azure-blob"></a><span data-ttu-id="44d9a-225">Blob de Azure</span><span class="sxs-lookup"><span data-stu-id="44d9a-225">Azure Blob</span></span>
<span data-ttu-id="44d9a-226">Un blob de Azure es un almacenamiento confiable y económico para muchos y pocos datos.</span><span class="sxs-lookup"><span data-stu-id="44d9a-226">Azure blob is a reliable, economical cloud storage for data big and small.</span></span> <span data-ttu-id="44d9a-227">Echemos un vistazo a cómo puede mover datos tooAzure Blob y acceder a los datos almacenados en un Blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="44d9a-227">Let us look at how you can move data tooAzure Blob and access data stored in an Azure Blob.</span></span>

<span data-ttu-id="44d9a-228">**Requisito previo**</span><span class="sxs-lookup"><span data-stu-id="44d9a-228">**Prerequisite**</span></span>

* <span data-ttu-id="44d9a-229">**Cree una cuenta de Almacenamiento de blobs de Azure desde el [Portal de Azure](https://portal.azure.com).**</span><span class="sxs-lookup"><span data-stu-id="44d9a-229">**Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).**</span></span>

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="44d9a-231">Confirmar esa herramienta de línea de comandos preinstalada AzCopy Hola se encuentra en ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span><span class="sxs-lookup"><span data-stu-id="44d9a-231">Confirm that hello pre-installed command-line AzCopy tool is found at ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span></span> <span data-ttu-id="44d9a-232">Puede agregue Hola contenedor hello azcopy.exe tooyour ruta de acceso entorno tooavoid variable escriba Hola comando completo ruta del directorio al ejecutar esta herramienta.</span><span class="sxs-lookup"><span data-stu-id="44d9a-232">You can add hello directory containing hello azcopy.exe tooyour PATH environment variable tooavoid typing hello full command path when running this tool.</span></span> <span data-ttu-id="44d9a-233">Para obtener más información sobre la herramienta AzCopy consulte demasiado[documentación AzCopy](../storage/common/storage-use-azcopy.md)</span><span class="sxs-lookup"><span data-stu-id="44d9a-233">For more info on AzCopy tool please refer too[AzCopy documentation](../storage/common/storage-use-azcopy.md)</span></span>
* <span data-ttu-id="44d9a-234">Inicie la herramienta Explorador de almacenamiento de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-234">Start hello Azure Storage Explorer tool.</span></span> <span data-ttu-id="44d9a-235">Se puede descargar en el [Explorador de almacenamiento de Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="44d9a-235">It can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

<span data-ttu-id="44d9a-237">**Mover los datos de la máquina virtual tooAzure Blob: AzCopy**</span><span class="sxs-lookup"><span data-stu-id="44d9a-237">**Move data from VM tooAzure Blob: AzCopy**</span></span>

<span data-ttu-id="44d9a-238">datos de toomove entre los archivos locales y el almacenamiento de blobs, puede utilizar AzCopy en línea de comandos o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="44d9a-238">toomove data between your local files and blob storage, you can use AzCopy in command-line or PowerShell:</span></span>

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

<span data-ttu-id="44d9a-239">Reemplace **C:\myfolder** toohello ruta de acceso donde se almacena el archivo, **mystorageaccount** tooyour nombre de cuenta de almacenamiento de blobs, **mycontainer** toohello nombre del contenedor, **clave de la cuenta de almacenamiento** tooyour clave de acceso de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="44d9a-239">Replace **C:\myfolder** toohello path where your file is stored, **mystorageaccount** tooyour blob storage account name, **mycontainer** toohello container name, **storage account key** tooyour blob storage access key.</span></span> <span data-ttu-id="44d9a-240">Las credenciales de su cuenta de almacenamiento puede encontrarlas en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="44d9a-240">You can find your storage account credentials in [Azure portal](https://portal.azure.com).</span></span>

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

<span data-ttu-id="44d9a-242">Ejecute el comando de AzCopy en PowerShell o desde el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="44d9a-242">Run AzCopy command in PowerShell or from a command prompt.</span></span> <span data-ttu-id="44d9a-243">Aquí puede ver algunos ejemplos del uso de comandos de AzCopy:</span><span class="sxs-lookup"><span data-stu-id="44d9a-243">Here is some example usage of AzCopy command:</span></span>

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



<span data-ttu-id="44d9a-244">Una vez que ejecute su tooan de toocopy de comandos de AzCopy blobs de Azure vea que el archivo aparece en el Explorador de almacenamiento de Azure en breve.</span><span class="sxs-lookup"><span data-stu-id="44d9a-244">Once you run your AzCopy command toocopy tooan Azure blob you see your file shows up in Azure Storage Explorer shortly.</span></span>

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

<span data-ttu-id="44d9a-246">**Mover los datos de la máquina virtual tooAzure Blob: Explorador de almacenamiento de Azure**</span><span class="sxs-lookup"><span data-stu-id="44d9a-246">**Move data from VM tooAzure Blob: Azure Storage Explorer**</span></span>

<span data-ttu-id="44d9a-247">También puede cargar datos de archivo local de hello en la máquina virtual mediante el Explorador de almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="44d9a-247">You can also upload data from hello local file in your VM using Azure Storage Explorer:</span></span>

* <span data-ttu-id="44d9a-248">contenedor de tooupload datos tooa, seleccione Hola Hola de contenedor y haga clic en de destino **cargar** botón.![ Cargar en el Explorador de almacenamiento](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="44d9a-248">tooupload data tooa container, select hello target container and click hello **Upload** button.![Upload in Storage Explorer](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span></span>
* <span data-ttu-id="44d9a-249">Haga clic en hello **...**  toohello derecha de hello **archivos** , seleccione uno o varios tooupload de archivos de sistema de archivos de Hola y haga clic en **cargar** toobegin cargar archivos de Hola.![ Cargar archivos tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="44d9a-249">Click on hello **...** toohello right of hello **Files** box, select one or multiple files tooupload from hello file system and click **Upload** toobegin uploading hello files.![Upload files tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span></span>

<span data-ttu-id="44d9a-250">**Lectura de datos de Blob de Azure: módulo lector de Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="44d9a-250">**Read data from Azure Blob: Machine Learning reader module**</span></span>

<span data-ttu-id="44d9a-251">En estudio de aprendizaje automático de Azure puede usar un **módulo importar datos** datos tooread desde el blob.</span><span class="sxs-lookup"><span data-stu-id="44d9a-251">In Azure Machine Learning Studio you can use an **Import Data module** tooread data from your blob.</span></span>

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

<span data-ttu-id="44d9a-253">**Lectura de datos de Blob de Azure: ODBC de Python**</span><span class="sxs-lookup"><span data-stu-id="44d9a-253">**Read data from Azure Blob: Python ODBC**</span></span>

<span data-ttu-id="44d9a-254">Puede usar **BlobService** biblioteca tooread directamente los datos de blob en un programa de Jupyter Notebook o Python.</span><span class="sxs-lookup"><span data-stu-id="44d9a-254">You can use **BlobService** library tooread data directly from blob in a Jupyter Notebook or Python program.</span></span>

<span data-ttu-id="44d9a-255">En primer lugar, importe los paquetes necesarios:</span><span class="sxs-lookup"><span data-stu-id="44d9a-255">First, import required packages:</span></span>

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random

<span data-ttu-id="44d9a-256">A continuación, especifique sus credenciales de la cuenta de Blob de Azure y lea los datos del blob:</span><span class="sxs-lookup"><span data-stu-id="44d9a-256">Then plug in your Azure Blob account credentials and read data from Blob:</span></span>

    CONTAINERNAME = 'xxx'
    STORAGEACCOUNTNAME = 'xxxx'
    STORAGEACCOUNTKEY = 'xxxxxxxxxxxxxxxx'
    BLOBNAME = 'nyctaxidataset/nyctaxitrip/trip_data_1.csv'
    localfilename = 'trip_data_1.csv'
    LOCALDIRECTORY = os.getcwd()
    LOCALFILE =  os.path.join(LOCALDIRECTORY, localfilename)

    #download from blob
    t1 = time.time()
    blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
    blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILE)
    t2 = time.time()
    print(("It takes %s seconds toodownload "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'hello size of hello data is: %d rows and  %d columns' % df1.shape

<span data-ttu-id="44d9a-257">se leen datos de Hello en como una trama de datos:</span><span class="sxs-lookup"><span data-stu-id="44d9a-257">hello data is read in as a data frame:</span></span>

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a><span data-ttu-id="44d9a-259">Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="44d9a-259">Azure Data Lake</span></span>
<span data-ttu-id="44d9a-260">Azure Data Lake Store es un repositorio a gran escala para cargas de trabajo de análisis de macrodatos compatible con el sistema de archivos distribuido Hadoop (HDFS),</span><span class="sxs-lookup"><span data-stu-id="44d9a-260">Azure Data Lake Storage is a hyper-scale repository for big data analytics workloads and compatible with Hadoop Distributed File System (HDFS).</span></span> <span data-ttu-id="44d9a-261">Funciona con el ecosistema de Hadoop de Hola y Hola análisis de Data Lake de Azure.</span><span class="sxs-lookup"><span data-stu-id="44d9a-261">It works with both hello Hadoop ecosystem and hello Azure Data Lake Analytics.</span></span> <span data-ttu-id="44d9a-262">Se muestra cómo puede mover datos a almacén de Azure Data Lake hello y ejecutar análisis mediante el análisis de Data Lake de Azure.</span><span class="sxs-lookup"><span data-stu-id="44d9a-262">We show how you can move data into hello Azure Data Lake Store and run analytics using Azure Data Lake Analytics.</span></span>

<span data-ttu-id="44d9a-263">**Requisito previo**</span><span class="sxs-lookup"><span data-stu-id="44d9a-263">**Prerequisite**</span></span>

* <span data-ttu-id="44d9a-264">Cree un análisis de Azure Data Lake Analytics en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="44d9a-264">Create your Azure Data Lake Analytics in [Azure portal](https://portal.azure.com).</span></span>

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* <span data-ttu-id="44d9a-266">Hola **Azure Data Lake Tools** en **Visual Studio** se encuentra en este [vínculo](https://www.microsoft.com/download/details.aspx?id=49504) ya está instalado en Visual Studio Community Edition que se encuentra en la máquina virtual de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-266">hello  **Azure Data Lake Tools** in **Visual Studio** found at this  [link](https://www.microsoft.com/download/details.aspx?id=49504) is already installed on hello Visual Studio Community Edition which is on hello virtual machine.</span></span> <span data-ttu-id="44d9a-267">Después de iniciar Visual Studio e iniciar sesión en su suscripción de Azure, debería ver su cuenta de análisis de datos de Azure y almacenamiento en el panel izquierdo de Hola de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="44d9a-267">After starting Visual Studio and logging in your Azure subscription, you should see your Azure Data Analytics account and storage in hello left panel of Visual Studio.</span></span>

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

<span data-ttu-id="44d9a-269">**Mover los datos de la máquina virtual tooData Lake: Explorador de Azure Data Lake**</span><span class="sxs-lookup"><span data-stu-id="44d9a-269">**Move data from VM tooData Lake: Azure Data Lake Explorer**</span></span>

<span data-ttu-id="44d9a-270">Puede usar **Explorador de Azure Data Lake** datos tooupload de los archivos locales de hello en el almacenamiento de máquina Virtual tooData Lake.</span><span class="sxs-lookup"><span data-stu-id="44d9a-270">You can use **Azure Data Lake Explorer** tooupload data from hello local files in your Virtual Machine tooData Lake storage.</span></span>

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

<span data-ttu-id="44d9a-272">También puede compilar un tooproductionize de canalización de datos su tooor de movimiento de datos de Azure Data Lake con hello [Factory(ADF) de datos de Azure](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="44d9a-272">You can also build a data pipeline tooproductionize your data movement tooor from Azure Data Lake using hello [Azure Data Factory(ADF)](https://azure.microsoft.com/services/data-factory/).</span></span> <span data-ttu-id="44d9a-273">Nos referimos toothis [artículo](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide le guían a través de los datos de saludo pasos toobuild Hola canalizaciones.</span><span class="sxs-lookup"><span data-stu-id="44d9a-273">We refer you toothis [article](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide you through hello steps toobuild hello data pipelines.</span></span>

<span data-ttu-id="44d9a-274">**Leer datos de Azure Blob tooData Lake: U-SQL**</span><span class="sxs-lookup"><span data-stu-id="44d9a-274">**Read data from Azure Blob tooData Lake: U-SQL**</span></span>

<span data-ttu-id="44d9a-275">Si los datos residen en el Almacenamiento de blobs de Azure, puede leer directamente los datos desde el blob de almacenamiento de Azure en una consulta U-SQL.</span><span class="sxs-lookup"><span data-stu-id="44d9a-275">If your data resides in Azure Blob storage, you can directly read data from Azure storage blob in U-SQL query.</span></span> <span data-ttu-id="44d9a-276">Antes de crear la consulta SQL U, asegúrese de que la cuenta de almacenamiento blob está vinculado tooyour Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="44d9a-276">Before composing your U-SQL query, make sure your blob storage account is linked tooyour Azure Data Lake.</span></span> <span data-ttu-id="44d9a-277">Vaya demasiado**portal de Azure**, busque el panel de análisis de Data Lake de Azure, haga clic en **agregar origen de datos**, seleccione el tipo de almacenamiento demasiado**el almacenamiento de Azure** y conecte el almacenamiento de Azure Nombre de cuenta y la clave.</span><span class="sxs-lookup"><span data-stu-id="44d9a-277">Go too**Azure portal**, find your Azure Data Lake Analytics dashboard, click **Add Data Source**, select storage type too**Azure Storage** and plug in your Azure Storage Account Name and Key.</span></span> <span data-ttu-id="44d9a-278">A continuación, está tooreference capaz de hello datos almacenados en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-278">Then you are able tooreference hello data stored in hello storage account.</span></span>

![Escribir la clave y la cuenta de almacenamiento](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

<span data-ttu-id="44d9a-280">En Visual Studio, puede leer datos del almacenamiento de blobs, lleve a cabo algunos manipulación de datos, ingeniería de características y salida Hola resultante datos tooeither Azure Data Lake o almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="44d9a-280">In Visual Studio, you can read data from blob storage, do some data manipulation, feature engineering, and output hello resulting data tooeither Azure Data Lake or Azure Blob Storage.</span></span> <span data-ttu-id="44d9a-281">Al hacer referencia a datos de hello en almacenamiento de blobs, use **wasb: / /**; al hacer referencia a datos de hello en Azure Data Lake, use **swbhdfs: / /**</span><span class="sxs-lookup"><span data-stu-id="44d9a-281">When you reference hello data in blob storage, use **wasb://**; when you reference hello data in Azure Data Lake, use **swbhdfs://**</span></span>

![Trama de datos](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

<span data-ttu-id="44d9a-283">Puede usar hello las siguientes consultas SQL U en Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="44d9a-283">You may use hello following U-SQL queries in Visual Studio:</span></span>

    @a =
        EXTRACT medallion string,
                hack_license string,
                vendor_id string,
                rate_code string,
                store_and_fwd_flag string,
                pickup_datetime string,
                dropoff_datetime string,
                passenger_count int,
                trip_time_in_secs double,
                trip_distance double,
                pickup_longitude string,
                pickup_latitude string,
                dropoff_longitude string,
                dropoff_latitude string

        FROM "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Input Data File Name>"
        USING Extractors.Csv();

    @b =
        SELECT vendor_id,
        COUNT(medallion) AS cnt_medallion,
        SUM(passenger_count) AS cnt_passenger,
        AVG(trip_distance) AS avg_trip_dist,
        MIN(trip_distance) AS min_trip_dist,
        MAX(trip_distance) AS max_trip_dist,
        AVG(trip_time_in_secs) AS avg_trip_time
        FROM @a
        GROUP BY vendor_id;

    OUTPUT @b   
    too"swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    too"wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



<span data-ttu-id="44d9a-284">Después de la consulta enviada toohello server, se muestra un diagrama que muestra el estado de saludo de su trabajo.</span><span class="sxs-lookup"><span data-stu-id="44d9a-284">After your query is submitted toohello server, a diagram showing hello status of your job is displayed.</span></span>

![Diagrama de estado de trabajo](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

<span data-ttu-id="44d9a-286">**Consulta de datos en Data Lake: U-SQL**</span><span class="sxs-lookup"><span data-stu-id="44d9a-286">**Query data in Data Lake: U-SQL**</span></span>

<span data-ttu-id="44d9a-287">Después de que el conjunto de datos de hello es ingestión en Azure Data Lake, puede usar [lenguaje SQL U](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery y explorar datos Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-287">After hello dataset is ingested into Azure Data Lake, you can use [U-SQL language](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery and explore hello data.</span></span> <span data-ttu-id="44d9a-288">Lenguaje SQL U es similar tooT-SQL, pero combina algunas características de C# para que los usuarios puedan escribir módulos personalizados, funciones definidas por el usuario y etcetera. Puede utilizar scripts de hello en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-288">U-SQL language is similar tooT-SQL, but combines some features from C# so that users can write customized modules, user-defined functions, and etc. You can use hello scripts in hello previous step.</span></span>

<span data-ttu-id="44d9a-289">Una vez consulta hello tooserver enviado, tripdata_summary. CSV puede encontrarse en breve **Explorador de Azure Data Lake**, puede obtener una vista previa de datos de Hola por archivo de hello de menú contextual.</span><span class="sxs-lookup"><span data-stu-id="44d9a-289">After hello query is submitted tooserver, tripdata_summary.CSV can be found shortly in **Azure Data Lake Explorer**, you may preview hello data by right-click hello file.</span></span>

![Archivo en el Explorador de Azure Data Lake](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

<span data-ttu-id="44d9a-291">información de archivo de Hola toosee:</span><span class="sxs-lookup"><span data-stu-id="44d9a-291">toosee hello file information:</span></span>

![Resumen del archivo](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a><span data-ttu-id="44d9a-293">Clústeres de Hadoop de HDInsight</span><span class="sxs-lookup"><span data-stu-id="44d9a-293">HDInsight Hadoop Clusters</span></span>
<span data-ttu-id="44d9a-294">HDInsight de Azure es un servicio administrado de Apache Hadoop, Spark, HBase y Storm en nube Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-294">Azure HDInsight is a managed Apache Hadoop, Spark, HBase, and Storm service on hello cloud.</span></span> <span data-ttu-id="44d9a-295">Puede trabajar fácilmente con los clústeres de HDInsight de Azure de la máquina virtual de hello datos ciencia.</span><span class="sxs-lookup"><span data-stu-id="44d9a-295">You can work easily with Azure HDInsight clusters from hello data science virtual machine.</span></span>

<span data-ttu-id="44d9a-296">**Requisito previo**</span><span class="sxs-lookup"><span data-stu-id="44d9a-296">**Prerequisite**</span></span>

* <span data-ttu-id="44d9a-297">Cree una cuenta de Almacenamiento de blobs de Azure desde el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="44d9a-297">Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="44d9a-298">Esta cuenta de almacenamiento es datos de uso toostore para clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="44d9a-298">This storage account is used toostore data for HDInsight clusters.</span></span>

![Creación de una cuenta de Azure Blob Storage](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="44d9a-300">Personalice los clústeres de Hadoop de HDInsight de Azure desde el [Portal de Azure](machine-learning-data-science-customize-hadoop-cluster.md)</span><span class="sxs-lookup"><span data-stu-id="44d9a-300">Customize Azure HDInsight Hadoop Clusters from [Azure portal](machine-learning-data-science-customize-hadoop-cluster.md)</span></span>
  
  * <span data-ttu-id="44d9a-301">Debe vincular la cuenta de almacenamiento de hello creada con el clúster de HDInsight cuando se crea.</span><span class="sxs-lookup"><span data-stu-id="44d9a-301">You must link hello storage account created with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="44d9a-302">Esta cuenta de almacenamiento se utiliza para tener acceso a datos que pueden ser procesados en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-302">This storage account is used for accessing data that can be processed within hello cluster.</span></span>

![Vincular toostorage cuenta creado con clúster de HDInsight](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* <span data-ttu-id="44d9a-304">Debe habilitar **acceso remoto** toohello del nodo principal del clúster de hello después de crearlo.</span><span class="sxs-lookup"><span data-stu-id="44d9a-304">You must enable **Remote Access** toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="44d9a-305">Recordar las credenciales de acceso remoto de Hola que especifique aquí (que son distintas de las especificadas para el clúster de hello en su creación): vaya necesitando en procedimiento posterior Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-305">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them in hello subsequent procedure.</span></span>

![Habilitación del acceso remoto](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* <span data-ttu-id="44d9a-307">Cree un área de trabajo de Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="44d9a-307">Create an Azure Machine Learning workspace.</span></span> <span data-ttu-id="44d9a-308">Los experimentos de Machine Learning se almacenarán en este área de trabajo de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="44d9a-308">Your Machine Learning Experiments are stored in this Machine Learning workspace.</span></span> <span data-ttu-id="44d9a-309">Seleccionar opciones de hello resaltado en el Portal de tal y como se muestra en la siguiente captura de pantalla de hello:</span><span class="sxs-lookup"><span data-stu-id="44d9a-309">Select hello highlighted options in Portal as shown in hello following screenshot:</span></span>

![Creación de un área de trabajo de Aprendizaje automático de Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* <span data-ttu-id="44d9a-311">A continuación, escriba los parámetros de hello para el área de trabajo</span><span class="sxs-lookup"><span data-stu-id="44d9a-311">Then enter hello parameters for your workspace</span></span>

![Especificación de parámetros de un área de trabajo de Machine Learning](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* <span data-ttu-id="44d9a-313">Cargue los datos mediante el cuaderno de IPython.</span><span class="sxs-lookup"><span data-stu-id="44d9a-313">Upload data using IPython Notebook.</span></span> <span data-ttu-id="44d9a-314">Importar paquetes necesarios en primer lugar, conecte las credenciales, crear una base de datos en la cuenta de almacenamiento y luego los datos tooHDI clústeres de carga.</span><span class="sxs-lookup"><span data-stu-id="44d9a-314">First import required packages, plug in credentials, create a db in your storage account, then load data tooHDI clusters.</span></span>

        #Import required Packages
        import pyodbc
        import time as time
        import json
        import os
        import urllib
        import urllib2
        import warnings
        import re
        import pandas as pd
        import matplotlib.pyplot as plt
        from azure.storage.blob import BlobService
        warnings.filterwarnings("ignore", category=UserWarning, module='urllib2')


        #Create hello connection tooHive using ODBC
        SERVER_NAME='xxx.azurehdinsight.net'
        DATABASE_NAME='nyctaxidb'
        USERID='xxx'
        PASSWORD='xxxx'
        DB_DRIVER='Microsoft Hive ODBC Driver'
        driver = 'DRIVER={' + DB_DRIVER + '}'
        server = 'Host=' + SERVER_NAME + ';Port=443'
        database = 'Schema=' + DATABASE_NAME
        hiveserv = 'HiveServerType=2'
        auth = 'AuthMech=6'
        uid = 'UID=' + USERID
        pwd = 'PWD=' + PASSWORD
        CONNECTION_STRING = ';'.join([driver,server,database,hiveserv,auth,uid,pwd])
        connection = pyodbc.connect(CONNECTION_STRING, autocommit=True)
        cursor=connection.cursor()


        #Create Hive database and tables
        queryString = "create database if not exists nyctaxidb;"
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.trip
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            rate_code string,
                            store_and_fwd_flag string,
                            pickup_datetime string,
                            dropoff_datetime string,
                            passenger_count int,
                            trip_time_in_secs double,
                            trip_distance double,
                            pickup_longitude double,
                            pickup_latitude double,
                            dropoff_longitude double,
                            dropoff_latitude double)  
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.fare
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            pickup_datetime string,
                            payment_type string,
                            fare_amount double,
                            surcharge double,
                            mta_tax double,
                            tip_amount double,
                            tolls_amount double,
                            total_amount double)
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)


        #Upload data from blob storage tooHDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* <span data-ttu-id="44d9a-315">Como alternativa, puede seguir este [tutorial](machine-learning-data-science-process-hive-walkthrough.md) tooupload clúster tooHDI de Nueva York Taxi datos.</span><span class="sxs-lookup"><span data-stu-id="44d9a-315">Alternately,  you can follow this [walkthrough](machine-learning-data-science-process-hive-walkthrough.md) tooupload NYC Taxi data tooHDI cluster.</span></span> <span data-ttu-id="44d9a-316">Entre los principales pasos se encuentran los siguientes:</span><span class="sxs-lookup"><span data-stu-id="44d9a-316">Major steps include:</span></span>
  
  * <span data-ttu-id="44d9a-317">AzCopy: Descargar comprimido CSV desde la carpeta local de blob público tooyour</span><span class="sxs-lookup"><span data-stu-id="44d9a-317">AzCopy: download zipped CSV's from public blob tooyour local folder</span></span>
  * <span data-ttu-id="44d9a-318">AzCopy: cargar descomprimida CSV de clúster de tooHDI de carpeta local</span><span class="sxs-lookup"><span data-stu-id="44d9a-318">AzCopy: upload unzipped CSV's from local folder tooHDI cluster</span></span>
  * <span data-ttu-id="44d9a-319">Inicie sesión en el nodo principal de Hola de clúster de Hadoop y preparar para el análisis de exploración de datos</span><span class="sxs-lookup"><span data-stu-id="44d9a-319">Log into hello head node of Hadoop cluster and prepare for exploratory data analysis</span></span>

<span data-ttu-id="44d9a-320">Una vez datos Hola clúster tooHDI cargado, puede comprobar los datos en el Explorador de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="44d9a-320">After hello data is loaded tooHDI cluster, you can check your data in Azure Storage Explorer.</span></span> <span data-ttu-id="44d9a-321">Y tendrá un archivo nyctaxidb de base de datos creado en el clúster HDI.</span><span class="sxs-lookup"><span data-stu-id="44d9a-321">And you have a database nyctaxidb created in HDI cluster.</span></span>

<span data-ttu-id="44d9a-322">**Exploración de datos: consultas de Hive en Python**</span><span class="sxs-lookup"><span data-stu-id="44d9a-322">**Data exploration: Hive Queries in Python**</span></span>

<span data-ttu-id="44d9a-323">Puesto que los datos de hello en clúster de Hadoop, puede usar hello pyodbc paquete tooconnect tooHadoop clústeres y consultar mediante Hive toodo exploración y la ingeniería de la característica de base de datos.</span><span class="sxs-lookup"><span data-stu-id="44d9a-323">Since hello data is in Hadoop cluster, you can use hello pyodbc package tooconnect tooHadoop Clusters and query database using Hive toodo exploration and feature engineering.</span></span> <span data-ttu-id="44d9a-324">Puede ver las tablas existentes Hola que se creó en el paso de requisitos previos de Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-324">You can view hello existing tables we created in hello prerequisite step.</span></span>

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![Consulta de las tablas existentes](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

<span data-ttu-id="44d9a-326">Echemos un vistazo a número de Hola de registros de cada mes y hello las frecuencias de superpuesto o no en la tabla de ida y vuelta de hello:</span><span class="sxs-lookup"><span data-stu-id="44d9a-326">Let's look at hello number of records in each month and hello frequencies of tipped or not in hello trip table:</span></span>

    queryString = """
        select month, count(*) from nyctaxidb.trip group by month;
        """
    results = pd.read_sql(queryString,connection)

    %matplotlib inline

    results.columns = ['month', 'trip_count']
    df = results.copy()
    df.index = df['month']
    df['trip_count'].plot(kind='bar')


![Trazado del número de registros de cada mes](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Number_Records_by_Month_v3.PNG)

    queryString = """
        SELECT tipped, COUNT(*) AS tip_freq
        FROM
        (
            SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
            FROM nyctaxidb.fare
        )tc
        GROUP BY tipped;
        """
    results = pd.read_sql(queryString,connection)

    results.columns = ['tipped', 'trip_count']
    df = results.copy()
    df.index = df['tipped']
    df['trip_count'].plot(kind='bar')


![Trazado de frecuencias de propina](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Frequency_tip_or_not_v3.PNG)

<span data-ttu-id="44d9a-329">Podemos también distancia Hola entre seleccionar una ubicación y la ubicación de caída de proceso y, a continuación, compárela toohello distancia de viaje.</span><span class="sxs-lookup"><span data-stu-id="44d9a-329">We can also compute hello distance between pickup location and dropoff location and then compare it toohello trip distance.</span></span>

    queryString = """
                    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
                        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
                        *radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
                        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
                        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
                        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*
                        pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance
                        from nyctaxidb.trip
                        where month=1
                            and pickup_longitude between -90 and -30
                            and pickup_latitude between 30 and 90
                            and dropoff_longitude between -90 and -30
                            and dropoff_latitude between 30 and 90;
                """
    results = pd.read_sql(queryString,connection)
    results.head(5)


![Tabla de recogida y depósito](./media/machine-learning-data-science-vm-do-ten-things/Exploration_compute_pickup_dropoff_distance_v2.PNG)

    results.columns = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude',
                       'dropoff_latitude', 'trip_distance', 'trip_time_in_secs', 'direct_distance']
    df = results.loc[results['trip_distance']<=100] #remove outliers
    df = df.loc[df['direct_distance']<=100] #remove outliers
    plt.scatter(df['direct_distance'], df['trip_distance'])


![Trazado de distancia de distancia de recogida/caída tootrip](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

<span data-ttu-id="44d9a-332">Ahora vamos a preparar una muestra reducida (1%) de un conjunto de datos para el modelado.</span><span class="sxs-lookup"><span data-stu-id="44d9a-332">Now let's prepare a down-sampled (1%) set of data for modeling.</span></span> <span data-ttu-id="44d9a-333">Podemos usar estos datos en el módulo lector de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="44d9a-333">We can use this data in Machine Learning reader module.</span></span>

        queryString = """
        create  table if not exists nyctaxi_downsampled_dataset_testNEW (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\\n'
        stored as textfile;
        """
        cursor.execute(queryString)

        --- now insert contents of hello join into hello preceding internal table

        queryString = """
        insert overwrite table nyctaxi_downsampled_dataset_testNEW
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class
        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance,
        rand() as sample_key

        from trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01
        """
        cursor.execute(queryString)

<span data-ttu-id="44d9a-334">Después de un tiempo, puede ver datos de Hola se han cargado en clústeres de Hadoop:</span><span class="sxs-lookup"><span data-stu-id="44d9a-334">After a while, you can see hello data has been loaded in Hadoop clusters:</span></span>

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Tabla de datos](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

<span data-ttu-id="44d9a-336">**Lectura de datos de HDI mediante Machine Learning: módulo lector**</span><span class="sxs-lookup"><span data-stu-id="44d9a-336">**Read data from HDI using Machine Learning: reader module**</span></span>

<span data-ttu-id="44d9a-337">También puede usar hello **lector** módulo en la base de datos de estudio de aprendizaje automático tooaccess hello en clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="44d9a-337">You may also use hello **reader** module in Machine Learning Studio tooaccess hello database in Hadoop cluster.</span></span> <span data-ttu-id="44d9a-338">Conecte credenciales de Hola de los clústeres HDI y tooenable de la cuenta de almacenamiento de Azure Cree modelos con la base de datos en clústeres HDI de aprendizaje de máquina de realizando una operación.</span><span class="sxs-lookup"><span data-stu-id="44d9a-338">Plug in hello credentials of your HDI clusters and Azure Storage Account tooenable build ing machine learning models using database in HDI clusters.</span></span>

![Propiedades del módulo lector](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

<span data-ttu-id="44d9a-340">Hello conjunto de datos con puntuación puede verse a continuación:</span><span class="sxs-lookup"><span data-stu-id="44d9a-340">hello scored dataset can then be viewed:</span></span>

![Visualización del conjunto de datos con puntuación](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a><span data-ttu-id="44d9a-342">Almacenamiento de datos SQL de Azure y bases de datos</span><span class="sxs-lookup"><span data-stu-id="44d9a-342">Azure SQL Data Warehouse & databases</span></span>
<span data-ttu-id="44d9a-343">Almacenamiento de datos SQL Azure es un almacén de datos elástico que funciona como un servicio con experiencia SQL Server empresarial.</span><span class="sxs-lookup"><span data-stu-id="44d9a-343">Azure SQL Data Warehouse is an elastic data warehouse as a service with enterprise-class SQL Server experience.</span></span>

<span data-ttu-id="44d9a-344">Puede aprovisionar el almacenamiento de datos de SQL Azure siguiendo las instrucciones de hello proporcionadas en este [artículo](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="44d9a-344">You can provision your Azure SQL Data Warehouse by following hello instructions provided in this [article](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span></span> <span data-ttu-id="44d9a-345">Una vez que aprovisione el almacenamiento de datos de SQL Azure, puede usar este [tutorial](machine-learning-data-science-process-sqldw-walkthrough.md) al cargar los datos de toodo, exploración y modelado utilizando los datos dentro de hello almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="44d9a-345">Once you provision your Azure SQL Data Warehouse, you can use this [walkthrough](machine-learning-data-science-process-sqldw-walkthrough.md) toodo data upload, exploration and modeling using data within hello SQL Data Warehouse.</span></span>

#### <a name="azure-cosmos-db"></a><span data-ttu-id="44d9a-346">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="44d9a-346">Azure Cosmos DB</span></span>
<span data-ttu-id="44d9a-347">Base de datos de Cosmos Azure es una base de datos NoSQL en nube Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-347">Azure Cosmos DB is a NoSQL database in hello cloud.</span></span> <span data-ttu-id="44d9a-348">Le permite toowork con documentos como JSON y permite documentos hello toostore y la consulta.</span><span class="sxs-lookup"><span data-stu-id="44d9a-348">It allows you toowork with documents like JSON and allows you toostore and query hello documents.</span></span>

<span data-ttu-id="44d9a-349">Necesita hello toodo siguientes por requisitos pasos tooaccess base de datos de Azure Cosmos de hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="44d9a-349">You need toodo hello following per-requisites steps tooaccess Azure Cosmos DB from hello DSVM.</span></span>

1. <span data-ttu-id="44d9a-350">Instale el SDK de Python de DocumentDB (ejecute ```pip install pydocumentdb``` desde el símbolo del sistema).</span><span class="sxs-lookup"><span data-stu-id="44d9a-350">Install DocumentDB Python SDK (Run ```pip install pydocumentdb``` from command prompt)</span></span>
2. <span data-ttu-id="44d9a-351">Cree una base de datos y una cuenta de Azure Cosmos DB en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="44d9a-351">Create an Azure Cosmos DB account and a database from [Azure portal](https://portal.azure.com)</span></span>
3. <span data-ttu-id="44d9a-352">Descargar "Herramienta de migración de base de datos de Azure Cosmos" de [aquí](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) y extraer tooa directorio de su elección</span><span class="sxs-lookup"><span data-stu-id="44d9a-352">Download "Azure Cosmos DB Migration Tool" from [here](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) and extract tooa directory of your choice</span></span>
4. <span data-ttu-id="44d9a-353">Importar datos JSON (datos volcano) almacenados en un [blob público](https://cahandson.blob.core.windows.net/samples/volcano.json) en DB Cosmos con siguiente herramienta de migración toohello de comando parámetros (dtui.exe del directorio de Hola donde instaló la herramienta de migración de base de datos de Cosmos hello).</span><span class="sxs-lookup"><span data-stu-id="44d9a-353">Import JSON data (volcano data) stored on a [public blob](https://cahandson.blob.core.windows.net/samples/volcano.json) into Cosmos DB with following command parameters toohello migration tool (dtui.exe from hello directory where you installed hello Cosmos DB Migration Tool).</span></span> <span data-ttu-id="44d9a-354">Escriba la ubicación de origen y de destino de hello con estos parámetros:</span><span class="sxs-lookup"><span data-stu-id="44d9a-354">Enter hello source and target location with these parameters:</span></span>
   
    <span data-ttu-id="44d9a-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span><span class="sxs-lookup"><span data-stu-id="44d9a-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span></span>

<span data-ttu-id="44d9a-356">Una vez que se importan datos de hello, puede ir tooJupyter y Bloc de notas abierto Hola titulada *DocumentDBSample* que contiene python tooaccess documentos de código y realice algunas consultas básicas.</span><span class="sxs-lookup"><span data-stu-id="44d9a-356">Once you import hello data, you can go tooJupyter and open hello notebook titled *DocumentDBSample* which contains python code tooaccess DocumentDB and do some basic querying.</span></span> <span data-ttu-id="44d9a-357">Se puede obtener más información acerca de la base de datos de Cosmos visitando servicio hello [página de documentación de](https://docs.microsoft.com/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="44d9a-357">You can learn more about Cosmos DB by visiting hello service [documentation page](https://docs.microsoft.com/azure/cosmos-db/).</span></span>

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a><span data-ttu-id="44d9a-358">8. Generar informes y panel con hello Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="44d9a-358">8. Build reports and dashboard using hello Power BI Desktop</span></span>
<span data-ttu-id="44d9a-359">Permítanos visualizar archivo JSON Volcano hello que hemos visto en hello anterior ejemplo de base de datos de Cosmos en Power BI toogain visuales visiones Hola datos.</span><span class="sxs-lookup"><span data-stu-id="44d9a-359">Let us visualize hello Volcano JSON file that we saw in hello preceding Cosmos DB example in Power BI toogain visual insights into hello data.</span></span> <span data-ttu-id="44d9a-360">Los pasos detallados están disponibles en hello [artículo Power BI](../cosmos-db/powerbi-visualize.md).</span><span class="sxs-lookup"><span data-stu-id="44d9a-360">Detailed steps are available in hello [Power BI article](../cosmos-db/powerbi-visualize.md).</span></span> <span data-ttu-id="44d9a-361">Estos son los pasos de alto nivel de hello:</span><span class="sxs-lookup"><span data-stu-id="44d9a-361">Here are hello high-level steps:</span></span>

1. <span data-ttu-id="44d9a-362">Abra Power BI Desktop y presione "Obtenga datos".</span><span class="sxs-lookup"><span data-stu-id="44d9a-362">Open Power BI Desktop and do "Get Data".</span></span> <span data-ttu-id="44d9a-363">Especifique la dirección URL de hello como: https://cahandson.blob.core.windows.net/samples/volcano.json</span><span class="sxs-lookup"><span data-stu-id="44d9a-363">Specify hello URL as: https://cahandson.blob.core.windows.net/samples/volcano.json</span></span>
2. <span data-ttu-id="44d9a-364">Debería ver registros JSON de hello importados como una lista</span><span class="sxs-lookup"><span data-stu-id="44d9a-364">You should see hello JSON records imported as a list</span></span>
3. <span data-ttu-id="44d9a-365">Convertir la tabla de tooa de lista de Hola para Power BI pueda trabajar con hello igual</span><span class="sxs-lookup"><span data-stu-id="44d9a-365">Convert hello list tooa table so Power BI can work with hello same</span></span>
4. <span data-ttu-id="44d9a-366">Expanda columnas Hola haciendo clic en hello expandirán icono (Hola uno con icono de "flecha izquierda y una flecha derecha" hello en hello derecha de la columna de hello)</span><span class="sxs-lookup"><span data-stu-id="44d9a-366">Expand hello columns by clicking on hello expand icon (hello one with hello "left arrow and a right arrow" icon on hello right of hello column)</span></span>
5. <span data-ttu-id="44d9a-367">Observe que la ubicación es un campo de "Registro".</span><span class="sxs-lookup"><span data-stu-id="44d9a-367">Notice that location is a "Record" field.</span></span> <span data-ttu-id="44d9a-368">Expandir registro de hello y seleccione sólo Hola coordenadas.</span><span class="sxs-lookup"><span data-stu-id="44d9a-368">Expand hello record and select only hello coordinates.</span></span> <span data-ttu-id="44d9a-369">Las coordenadas es una columna de la lista.</span><span class="sxs-lookup"><span data-stu-id="44d9a-369">Coordinate is a list column</span></span>
6. <span data-ttu-id="44d9a-370">Agregar una nueva columna tooconvert Hola lista coordenadas de columnas en una columna de LatLong independiente de coma concatenar Hola dos elementos de hello coordenadas lista campo usando la fórmula de hello ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span><span class="sxs-lookup"><span data-stu-id="44d9a-370">Add a new column tooconvert hello list coordinate column into a comma separate LatLong column concatenating hello two elements in hello coordinate list field using hello formula ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span></span>
7. <span data-ttu-id="44d9a-371">Por último, convertir hello ```Elevation``` tooDecimal de columna y seleccione hello **cerrar** y **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="44d9a-371">Finally convert hello ```Elevation``` column tooDecimal and select hello **Close** and **Apply**.</span></span>

<span data-ttu-id="44d9a-372">En lugar de pasos anteriores, puede pegar Hola siguiente código de scripts de pasos de Hola que se usan en Hola Editor avanzado en Power BI que permite transformaciones de datos de hello toowrite en un lenguaje de consulta.</span><span class="sxs-lookup"><span data-stu-id="44d9a-372">Instead of preceding steps, you can paste hello following code that scripts out hello steps used in hello Advanced Editor in Power BI that allows you toowrite hello data transformations in a query language.</span></span>

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



<span data-ttu-id="44d9a-373">Ahora tiene datos de hello en el modelo de datos de Power BI.</span><span class="sxs-lookup"><span data-stu-id="44d9a-373">You now have hello data in your Power BI data model.</span></span> <span data-ttu-id="44d9a-374">Power BI Desktop debe aparecer como sigue:</span><span class="sxs-lookup"><span data-stu-id="44d9a-374">Your Power BI desktop should appear as follows:</span></span>

![Power BI Desktop](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

<span data-ttu-id="44d9a-376">Ya puede empezar a crear informes y visualizaciones con el modelo de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="44d9a-376">You can start building reports and visualizations using hello data model.</span></span> <span data-ttu-id="44d9a-377">Puede seguir los pasos de hello en este [artículo Power BI](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild un informe.</span><span class="sxs-lookup"><span data-stu-id="44d9a-377">You can follow hello steps in this [Power BI article](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild a report.</span></span> <span data-ttu-id="44d9a-378">resultado de Hello final es un informe similar Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="44d9a-378">hello end result is a report that looks like hello following.</span></span>

![Vista de informes de Power BI Desktop: conector de Power BI](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a><span data-ttu-id="44d9a-380">9. Escalar dinámicamente su toomeet DSVM que su proyecto necesite</span><span class="sxs-lookup"><span data-stu-id="44d9a-380">9. Dynamically scale your DSVM toomeet your project needs</span></span>
<span data-ttu-id="44d9a-381">Puede escalar arriba y abajo hello DSVM toomeet que su proyecto necesite.</span><span class="sxs-lookup"><span data-stu-id="44d9a-381">You can scale up and down hello DSVM toomeet your project needs.</span></span> <span data-ttu-id="44d9a-382">Si no necesita toouse Hola VM de jornada laboral de Hola o los fines de semana, puede apagar simplemente Hola VM de hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="44d9a-382">If you don't need toouse hello VM in hello evening or weekends, you can just shut down hello VM from hello [Azure portal](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="44d9a-383">Acumulando cargos de proceso si utiliza simplemente el botón de apagado del sistema operativo de hello en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="44d9a-383">You incur compute charges if you use just hello Operating system shutdown button on hello VM.</span></span>  
> 
> 

<span data-ttu-id="44d9a-384">Si necesita toohandle un análisis a gran escala y necesita más capacidad de CPU, memoria o disco encontrará gran varios tamaños VM en términos de núcleos de CPU, capacidad de memoria y los tipos de disco (incluidas las unidades de estado sólido) que satisfacen las necesidades presupuestarias y proceso.</span><span class="sxs-lookup"><span data-stu-id="44d9a-384">If you need toohandle some large-scale analysis and need more CPU and/or memory and/or disk capacity you can find a large choice of VM sizes in terms of CPU cores, memory capacity and disk types (including Solid state drives) that meet your compute and budgetary needs.</span></span> <span data-ttu-id="44d9a-385">Hello lista completa de las máquinas virtuales junto con sus precios por hora de cálculo está disponible en hello [precios de máquinas virtuales de Azure](https://azure.microsoft.com/pricing/details/virtual-machines/) página.</span><span class="sxs-lookup"><span data-stu-id="44d9a-385">hello full list of VMs along with their hourly compute pricing is available on hello [Azure Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/) page.</span></span>

<span data-ttu-id="44d9a-386">De forma similar, si reduce la necesidad de capacidad de procesamiento de la máquina virtual (por ejemplo: mover un tooa de carga de trabajo principales Hadoop o en un clúster de Spark), puede reducir clúster Hola de hello [portal de Azure](https://portal.azure.com) y va toohello configuración de la máquina virtual instancia.</span><span class="sxs-lookup"><span data-stu-id="44d9a-386">Similarly, if your need for VM processing capacity reduces (for example: you moved a major workload tooa Hadoop or a Spark cluster), you can scale down hello cluster from hello [Azure portal](https://portal.azure.com) and going toohello settings of your VM instance.</span></span> <span data-ttu-id="44d9a-387">Aquí puede ver una captura de pantalla.</span><span class="sxs-lookup"><span data-stu-id="44d9a-387">Here is a screenshot.</span></span>

![Configuración de la instancia de VM](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a><span data-ttu-id="44d9a-389">10. Instalar herramientas adicionales en la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="44d9a-389">10. Install additional tools on your virtual machine</span></span>
<span data-ttu-id="44d9a-390">Nos hemos empaquetar varias herramientas que creemos son tooaddress capaz de muchas de las necesidades de análisis de datos comunes de Hola y que deben ahorrarle tiempo al evitar tener tooinstall y configurar los entornos de uno a uno y ahorrar dinero por pagar solo por recursos que Use.</span><span class="sxs-lookup"><span data-stu-id="44d9a-390">We have packaged several tools that we believe are able tooaddress many of hello common data analytics needs and that should save you time by avoiding having tooinstall and configure your environments one by one and save you money by paying only for resources that you use.</span></span>

<span data-ttu-id="44d9a-391">Puedes sacar provecho de otros datos de Azure y generar perfiles de servicios de análisis en este artículo tooenhance su entorno de análisis.</span><span class="sxs-lookup"><span data-stu-id="44d9a-391">You can leverage other Azure data and analytics services profiled in this article tooenhance your analytics environment.</span></span> <span data-ttu-id="44d9a-392">Somos conscientes de que en algunos casos sus necesidades pueden requerir herramientas adicionales, incluidas algunas herramientas propiedad de terceros.</span><span class="sxs-lookup"><span data-stu-id="44d9a-392">We understand that in some cases your needs may require additional tools, including some proprietary third-party tools.</span></span> <span data-ttu-id="44d9a-393">Tener acceso administrativo completo en hello máquina virtual tooinstall nuevas herramientas que necesita.</span><span class="sxs-lookup"><span data-stu-id="44d9a-393">You have full administrative access on hello virtual machine tooinstall new tools you need.</span></span> <span data-ttu-id="44d9a-394">También puede instalar paquetes adicionales de Python y R que no estén instalados previamente.</span><span class="sxs-lookup"><span data-stu-id="44d9a-394">You can also install additional packages in Python and R that are not pre-installed.</span></span> <span data-ttu-id="44d9a-395">En el caso de Python, puede utilizar ```conda``` o ```pip```.</span><span class="sxs-lookup"><span data-stu-id="44d9a-395">For Python you can use either ```conda``` or ```pip```.</span></span> <span data-ttu-id="44d9a-396">Para R puede usar hello ```install.packages()``` en hello R la consola o usar hello IDE y elija "**paquetes** -> **paquetes de instalación...** ".</span><span class="sxs-lookup"><span data-stu-id="44d9a-396">For R you can use hello ```install.packages()``` in hello R console or use hello IDE and choose "**Packages** -> **Install Packages...**".</span></span>

## <a name="summary"></a><span data-ttu-id="44d9a-397">Resumen</span><span class="sxs-lookup"><span data-stu-id="44d9a-397">Summary</span></span>
<span data-ttu-id="44d9a-398">Éstas son sólo algunas de las acciones de Hola que puede realizar en hello Microsoft Data Science Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="44d9a-398">These are just some of hello things you can do on hello Microsoft Data Science Virtual Machine.</span></span> <span data-ttu-id="44d9a-399">Hay muchas más cosas que puede hacer toomake un entorno de análisis efectivo.</span><span class="sxs-lookup"><span data-stu-id="44d9a-399">There are many more things you can do toomake it an effective analytics environment.</span></span>

