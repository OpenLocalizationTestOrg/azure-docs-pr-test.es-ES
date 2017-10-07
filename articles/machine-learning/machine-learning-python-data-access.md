---
title: "aaaAccess conjuntos de datos con la biblioteca de cliente de Python de aprendizaje automático | Documentos de Microsoft"
description: "Instalar y usar hello tooaccess de biblioteca de cliente de Python y administrar datos de aprendizaje automático de Azure de forma segura un entorno local de Python."
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a><span data-ttu-id="7b235-103">Conjuntos de datos de Access con Python utilizando la biblioteca de cliente de Python de aprendizaje automático de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="7b235-103">Access datasets with Python using hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="7b235-104">vista previa de Hola de biblioteca de cliente de Python de aprendizaje automático de Microsoft Azure puede habilitar un acceso seguro tooyour conjuntos de datos de aprendizaje automático de Azure desde un entorno local de Python y permite la creación de hello y administración de conjuntos de datos en un área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="7b235-104">hello preview of Microsoft Azure Machine Learning Python client library can enable secure access tooyour Azure Machine Learning datasets from a local Python environment and enables hello creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="7b235-105">Este tema proporciona instrucciones sobre cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="7b235-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="7b235-106">instalar biblioteca de cliente de Python de aprendizaje automático de Hola</span><span class="sxs-lookup"><span data-stu-id="7b235-106">install hello Machine Learning Python client library</span></span> 
* <span data-ttu-id="7b235-107">obtener acceso y cargar conjuntos de datos, incluidas las instrucciones sobre cómo tooget autorización tooaccess conjuntos de datos de aprendizaje automático de Azure de su entorno local de Python</span><span class="sxs-lookup"><span data-stu-id="7b235-107">access and upload datasets, including instructions on how tooget authorization tooaccess Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="7b235-108">obtener acceso a los conjuntos de datos intermedios de experimentos;</span><span class="sxs-lookup"><span data-stu-id="7b235-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="7b235-109">usar conjuntos de datos de hello Python cliente biblioteca tooenumerate, tener acceso a metadatos, lectura Hola del contenido de un conjunto de datos, crear nuevos conjuntos de datos y actualizar conjuntos de datos existentes</span><span class="sxs-lookup"><span data-stu-id="7b235-109">use hello Python client library tooenumerate datasets, access metadata, read hello contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="7b235-110"><a name="prerequisites"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7b235-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="7b235-111">biblioteca de cliente de Python Hola se ha probado en hello siguientes entornos:</span><span class="sxs-lookup"><span data-stu-id="7b235-111">hello Python client library has been tested under hello following environments:</span></span>

* <span data-ttu-id="7b235-112">Windows, Mac y Linux</span><span class="sxs-lookup"><span data-stu-id="7b235-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="7b235-113">Python 2.7, 3.3 y 3.4</span><span class="sxs-lookup"><span data-stu-id="7b235-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="7b235-114">Tiene una dependencia en hello siguientes paquetes:</span><span class="sxs-lookup"><span data-stu-id="7b235-114">It has a dependency on hello following packages:</span></span>

* <span data-ttu-id="7b235-115">Solicitudes</span><span class="sxs-lookup"><span data-stu-id="7b235-115">requests</span></span>
* <span data-ttu-id="7b235-116">Python-dateutil</span><span class="sxs-lookup"><span data-stu-id="7b235-116">python-dateutil</span></span>
* <span data-ttu-id="7b235-117">Pandas</span><span class="sxs-lookup"><span data-stu-id="7b235-117">pandas</span></span>

<span data-ttu-id="7b235-118">Se recomienda utilizar una distribución de Python como [Anaconda](http://continuum.io/downloads#all) o [Canopy](https://store.enthought.com/downloads/), que vienen con Python, IPython e instalar los paquetes de saludo tres mencionados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7b235-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and hello three packages listed above installed.</span></span> <span data-ttu-id="7b235-119">Aunque IPython no es estrictamente necesario, es un excelente entorno para manipular y visualizar datos de forma interactiva.</span><span class="sxs-lookup"><span data-stu-id="7b235-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="7b235-120"><a name="installation"></a>¿Cómo tooinstall Hola biblioteca de cliente de Python de aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="7b235-120"><a name="installation"></a>How tooinstall hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="7b235-121">biblioteca de cliente de Python de aprendizaje automático de Azure de Hello también debe estar instalado toocomplete tareas de hello descritas en este tema.</span><span class="sxs-lookup"><span data-stu-id="7b235-121">hello Azure Machine Learning Python client library must also be installed toocomplete hello tasks outlined in this topic.</span></span> <span data-ttu-id="7b235-122">Está disponible de hello [índice del paquete Python](https://pypi.python.org/pypi/azureml).</span><span class="sxs-lookup"><span data-stu-id="7b235-122">It is available from hello [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="7b235-123">tooinstall en su entorno de Python, ejecute Hola siguiente comando desde el entorno de Python local:</span><span class="sxs-lookup"><span data-stu-id="7b235-123">tooinstall it in your Python environment, run hello following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="7b235-124">Como alternativa, puede descargar e instalar desde orígenes de hello en [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span><span class="sxs-lookup"><span data-stu-id="7b235-124">Alternatively, you can download and install from hello sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="7b235-125">Si tiene instalado en su equipo de git, puede usar pip tooinstall directamente desde el repositorio de git de hello:</span><span class="sxs-lookup"><span data-stu-id="7b235-125">If you have git installed on your machine, you can use pip tooinstall directly from hello git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="7b235-126"><a name="datasetAccess"></a>Usar conjuntos de datos de tooaccess de fragmentos de código de Studio</span><span class="sxs-lookup"><span data-stu-id="7b235-126"><a name="datasetAccess"></a>Use Studio Code snippets tooaccess datasets</span></span>
<span data-ttu-id="7b235-127">biblioteca de cliente de Python Hola proporciona conjuntos de datos existentes de acceso mediante programación tooyour de experimentos que se han ejecutado.</span><span class="sxs-lookup"><span data-stu-id="7b235-127">hello Python client library gives you programmatic access tooyour existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="7b235-128">Desde la interfaz web de hello Studio, puede generar fragmentos de código que incluyen todos los toodownload de la información necesaria de Hola y deserializar los conjuntos de datos como objetos de trama de datos de Pandas en su equipo de ubicación.</span><span class="sxs-lookup"><span data-stu-id="7b235-128">From hello Studio web interface, you can generate code snippets that include all hello necessary information toodownload and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="7b235-129"><a name="security"></a>Seguridad de acceso a datos</span><span class="sxs-lookup"><span data-stu-id="7b235-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="7b235-130">Hola Studio proporcionados para usarlo con la biblioteca de cliente de Python de hello incluye el identificador de área de trabajo y la autorización de fragmentos de código de token.</span><span class="sxs-lookup"><span data-stu-id="7b235-130">hello code snippets provided by Studio for use with hello Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="7b235-131">Estos proporcionan el área de trabajo de acceso completo tooyour y deben estar protegidos, como una contraseña.</span><span class="sxs-lookup"><span data-stu-id="7b235-131">These provide full access tooyour workspace and must be protected, like a password.</span></span>

<span data-ttu-id="7b235-132">Por motivos de seguridad, funcionalidad de fragmento de código de hello solo está disponible toousers que tienen su rol establecer como **propietario** para el área de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b235-132">For security reasons, hello code snippet functionality is only available toousers that have their role set as **Owner** for hello workspace.</span></span> <span data-ttu-id="7b235-133">El rol se muestra en el estudio de aprendizaje automático de Azure en hello **usuarios** página en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="7b235-133">Your role is displayed in Azure Machine Learning Studio on hello **USERS** page under **Settings**.</span></span>

![Seguridad][security]

<span data-ttu-id="7b235-135">Si su rol no está establecido como **propietario**, puede solicitar toobe Invitado como un propietario o pida Hola propietario de hello tooprovide de área de trabajo, con el fragmento de código de hello.</span><span class="sxs-lookup"><span data-stu-id="7b235-135">If your role is not set as **Owner**, you can either request toobe reinvited as an owner, or ask hello owner of hello workspace tooprovide you with hello code snippet.</span></span>

<span data-ttu-id="7b235-136">token de autorización de hello tooobtain, puede hacer uno de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="7b235-136">tooobtain hello authorization token, you can do one of hello following:</span></span>

* <span data-ttu-id="7b235-137">Solicite un token a un propietario.</span><span class="sxs-lookup"><span data-stu-id="7b235-137">Ask for a token from an owner.</span></span> <span data-ttu-id="7b235-138">Los propietarios pueden acceder a sus tokens de autorización de la página de configuración de Hola de su área de trabajo de Studio.</span><span class="sxs-lookup"><span data-stu-id="7b235-138">Owners can access their authorization tokens from hello Settings page of their workspace in Studio.</span></span> <span data-ttu-id="7b235-139">Seleccione **configuración** de hello dejado panel y haga clic en **TOKENS de autorización** toosee Hola tokens principales y secundarios.</span><span class="sxs-lookup"><span data-stu-id="7b235-139">Select **Settings** from hello left pane and click **AUTHORIZATION TOKENS** toosee hello primary and secondary tokens.</span></span>  <span data-ttu-id="7b235-140">Aunque Hola principal o tokens de autorización secundaria de hello pueden utilizarse en el fragmento de código de hello, se recomienda que los propietarios solo compartan tokens de autorización secundaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b235-140">Although either hello primary or hello secondary authorization tokens can be used in hello code snippet, it is recommended that owners only share hello secondary authorization tokens.</span></span>

![Tokens de autorización](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="7b235-142">Pida toorole toobe promocionada del propietario.</span><span class="sxs-lookup"><span data-stu-id="7b235-142">Ask toobe promoted toorole of owner.</span></span>  <span data-ttu-id="7b235-143">toodo esto, un propietario actual del toofirst de necesidades del área de trabajo de hello quitarle de su área de trabajo de hello, a continuación, vuelva a invitar a tooit como propietario.</span><span class="sxs-lookup"><span data-stu-id="7b235-143">toodo this, a current owner of hello workspace needs toofirst remove you from hello workspace then re-invite you tooit as an owner.</span></span>

<span data-ttu-id="7b235-144">Una vez que han obtenido los desarrolladores de Id. de área de trabajo de Hola y autorización token, son tooaccess capaz de área de trabajo de hello mediante el fragmento de código de hello, independientemente de su rol.</span><span class="sxs-lookup"><span data-stu-id="7b235-144">Once developers have obtained hello workspace id and authorization token, they are able tooaccess hello workspace using hello code snippet regardless of their role.</span></span>

<span data-ttu-id="7b235-145">Tokens de autorización se administran en hello **TOKENS de autorización** página en **configuración**.</span><span class="sxs-lookup"><span data-stu-id="7b235-145">Authorization tokens are managed on hello **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="7b235-146">Puede volver a generar ellos, pero este procedimiento revoca el token de acceso toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="7b235-146">You can regenerate them, but this procedure revokes access toohello previous token.</span></span>

### <span data-ttu-id="7b235-147"><a name="accessingDatasets"></a>Obtener acceso a los conjuntos de datos desde una aplicación local de Python</span><span class="sxs-lookup"><span data-stu-id="7b235-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="7b235-148">En estudio de aprendizaje automático, haga clic en **conjuntos de datos** en barra de navegación de Hola Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="7b235-148">In Machine Learning Studio, click **DATASETS** in hello navigation bar on hello left.</span></span>
2. <span data-ttu-id="7b235-149">Seleccione el conjunto de datos de hello le gustaría tooaccess.</span><span class="sxs-lookup"><span data-stu-id="7b235-149">Select hello dataset you would like tooaccess.</span></span> <span data-ttu-id="7b235-150">Puede seleccionar cualquiera de los conjuntos de datos de Hola de hello **Mis conjuntos de datos** lista o de hello **ejemplos** lista.</span><span class="sxs-lookup"><span data-stu-id="7b235-150">You can select any of hello datasets from hello **MY DATASETS** list or from hello **SAMPLES** list.</span></span>
3. <span data-ttu-id="7b235-151">En la barra de herramientas de hello inferior, haga clic en **generar código de acceso a datos**.</span><span class="sxs-lookup"><span data-stu-id="7b235-151">From hello bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="7b235-152">Si los datos de hello en un formato incompatible con la biblioteca de cliente de Python hello, este botón está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="7b235-152">If hello data is in a format incompatible with hello Python client library, this button is disabled.</span></span>
   
    ![CONJUNTOS DE DATOS][datasets]
4. <span data-ttu-id="7b235-154">Seleccione el fragmento de código de hello en ventana hello que aparece y se copia tooyour Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="7b235-154">Select hello code snippet from hello window that appears and copy it tooyour clipboard.</span></span>
   
    ![Código de acceso][dataset-access-code]
5. <span data-ttu-id="7b235-156">Pegue el código de hello en Bloc de notas de saludo de la aplicación local de Python.</span><span class="sxs-lookup"><span data-stu-id="7b235-156">Paste hello code into hello notebook of your local Python application.</span></span>
   
    ![Bloc de notas][ipython-dataset]

## <span data-ttu-id="7b235-158"><a name="accessingIntermediateDatasets"></a>Obtener acceso a los conjuntos de datos intermedios de experimentos de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="7b235-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="7b235-159">Después de ejecuta un experimento en hello estudio de aprendizaje automático, es posible tooaccess Hola intermedio los conjuntos de datos de nodos de salida de hello de módulos.</span><span class="sxs-lookup"><span data-stu-id="7b235-159">After an experiment is run in hello Machine Learning Studio, it is possible tooaccess hello intermediate datasets from hello output nodes of modules.</span></span> <span data-ttu-id="7b235-160">Los conjuntos de datos intermedios son datos que se han creado y utilizado para pasos intermedios cuando se ha ejecutado una herramienta de modelo.</span><span class="sxs-lookup"><span data-stu-id="7b235-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="7b235-161">Pueden tener acceso a conjuntos de datos intermedio como formato de datos de hello es compatible con la biblioteca de cliente de Python Hola.</span><span class="sxs-lookup"><span data-stu-id="7b235-161">Intermediate datasets can be accessed as long as hello data format is compatible with hello Python client library.</span></span>

<span data-ttu-id="7b235-162">Hola se admiten los formatos siguientes (constantes para estos están en hello `azureml.DataTypeIds` clase):</span><span class="sxs-lookup"><span data-stu-id="7b235-162">hello following formats are supported (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="7b235-163">PlainText</span><span class="sxs-lookup"><span data-stu-id="7b235-163">PlainText</span></span>
* <span data-ttu-id="7b235-164">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="7b235-164">GenericCSV</span></span>
* <span data-ttu-id="7b235-165">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="7b235-165">GenericTSV</span></span>
* <span data-ttu-id="7b235-166">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="7b235-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="7b235-167">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="7b235-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="7b235-168">Puede determinar el formato de hello desplazando el puntero sobre un nodo de salida del módulo.</span><span class="sxs-lookup"><span data-stu-id="7b235-168">You can determine hello format by hovering over a module output node.</span></span> <span data-ttu-id="7b235-169">Se muestra junto con el nombre de nodo de hello, información sobre herramientas.</span><span class="sxs-lookup"><span data-stu-id="7b235-169">It is displayed along with hello node name, in a tooltip.</span></span>

<span data-ttu-id="7b235-170">Algunos de los módulos de hello, como hello [división] [ split] módulo, formato de salida tooa denominado `Dataset`, que no es compatible con la biblioteca de cliente de Python Hola.</span><span class="sxs-lookup"><span data-stu-id="7b235-170">Some of hello modules, such as hello [Split][split] module, output tooa format named `Dataset`, which is not supported by hello Python client library.</span></span>

![Formato de conjunto de datos][dataset-format]

<span data-ttu-id="7b235-172">Necesita toouse un módulo de conversión, como [convertir tooCSV][convert-to-csv], tooget una salida a un formato compatible.</span><span class="sxs-lookup"><span data-stu-id="7b235-172">You need toouse a conversion module, such as [Convert tooCSV][convert-to-csv], tooget an output into a supported format.</span></span>

![Formato GenericCSV][csv-format]

<span data-ttu-id="7b235-174">Hello pasos siguientes muestran un ejemplo que crea un experimento, lo ejecuta y tiene acceso a conjunto de datos intermedio Hola.</span><span class="sxs-lookup"><span data-stu-id="7b235-174">hello following steps show an example that creates an experiment, runs it and accesses hello intermediate dataset.</span></span>

1. <span data-ttu-id="7b235-175">Cree un experimento nuevo.</span><span class="sxs-lookup"><span data-stu-id="7b235-175">Create a new experiment.</span></span>
2. <span data-ttu-id="7b235-176">Inserte un módulo **Conjunto de datos de clasificación binaria de ingresos en el censo de adultos** .</span><span class="sxs-lookup"><span data-stu-id="7b235-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="7b235-177">Insertar un [división] [ split] módulo y conecte la salida del módulo de conjunto de datos de entrada toohello.</span><span class="sxs-lookup"><span data-stu-id="7b235-177">Insert a [Split][split] module, and connect its input toohello dataset module output.</span></span>
4. <span data-ttu-id="7b235-178">Insertar un [convertir tooCSV] [ convert-to-csv] módulo y conectar su entrada tooone de hello [división] [ split] módulo genera.</span><span class="sxs-lookup"><span data-stu-id="7b235-178">Insert a [Convert tooCSV][convert-to-csv] module and connect its input tooone of hello [Split][split] module outputs.</span></span>
5. <span data-ttu-id="7b235-179">Guardar experimento hello, ejecútelo y esperar a que toofinish ejecutando.</span><span class="sxs-lookup"><span data-stu-id="7b235-179">Save hello experiment, run it, and wait for it toofinish running.</span></span>
6. <span data-ttu-id="7b235-180">Haga clic en el nodo de salida de hello en hello [convertir tooCSV] [ convert-to-csv] módulo.</span><span class="sxs-lookup"><span data-stu-id="7b235-180">Click hello output node on hello [Convert tooCSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="7b235-181">Cuando aparezca el menú contextual de hello, seleccione **generar código de acceso a datos**.</span><span class="sxs-lookup"><span data-stu-id="7b235-181">When hello context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![Menú contextual][experiment]
8. <span data-ttu-id="7b235-183">Seleccione el fragmento de código de hello y cópielo tooyour Portapapeles desde la ventana de Hola que aparece.</span><span class="sxs-lookup"><span data-stu-id="7b235-183">Select hello code snippet and copy it tooyour clipboard from hello window that appears.</span></span>
   
    ![Código de acceso][intermediate-dataset-access-code]
9. <span data-ttu-id="7b235-185">Pegue el código de hello en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="7b235-185">Paste hello code in your notebook.</span></span>
   
    ![Bloc de notas][ipython-intermediate-dataset]
10. <span data-ttu-id="7b235-187">Puede visualizar datos Hola con matplotlib.</span><span class="sxs-lookup"><span data-stu-id="7b235-187">You can visualize hello data using matplotlib.</span></span> <span data-ttu-id="7b235-188">Esto se muestra en un histograma para la columna de edad de hello:</span><span class="sxs-lookup"><span data-stu-id="7b235-188">This displays in a histogram for hello age column:</span></span>
    
    ![Histograma][ipython-histogram]

## <span data-ttu-id="7b235-190"><a name="clientApis"></a>Usar tooaccess de biblioteca de cliente de Python de aprendizaje automático de hello, leer, crear y administrar conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="7b235-190"><a name="clientApis"></a>Use hello Machine Learning Python client library tooaccess, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="7b235-191">Área de trabajo</span><span class="sxs-lookup"><span data-stu-id="7b235-191">Workspace</span></span>
<span data-ttu-id="7b235-192">área de trabajo de Hello es el punto de entrada de hello para la biblioteca de cliente de Python Hola.</span><span class="sxs-lookup"><span data-stu-id="7b235-192">hello workspace is hello entry point for hello Python client library.</span></span> <span data-ttu-id="7b235-193">Proporcionar hello `Workspace` una instancia de clase con la toocreate de token de identificador y la autorización de área de trabajo:</span><span class="sxs-lookup"><span data-stu-id="7b235-193">Provide hello `Workspace` class with your workspace id and authorization token toocreate an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="7b235-194">Enumerar los conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="7b235-194">Enumerate datasets</span></span>
<span data-ttu-id="7b235-195">tooenumerate todos los conjuntos de datos en un área de trabajo determinado:</span><span class="sxs-lookup"><span data-stu-id="7b235-195">tooenumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="7b235-196">tooenumerate Hola simplemente creados por el usuario los conjuntos de datos:</span><span class="sxs-lookup"><span data-stu-id="7b235-196">tooenumerate just hello user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="7b235-197">conjuntos de datos de ejemplo de Hola simplemente tooenumerate:</span><span class="sxs-lookup"><span data-stu-id="7b235-197">tooenumerate just hello example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="7b235-198">Puede tener acceso a un conjunto de datos por nombre (que distingue mayúsculas de minúsculas):</span><span class="sxs-lookup"><span data-stu-id="7b235-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="7b235-199">O bien, puede tener acceso a él por su índice:</span><span class="sxs-lookup"><span data-stu-id="7b235-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="7b235-200">Metadatos</span><span class="sxs-lookup"><span data-stu-id="7b235-200">Metadata</span></span>
<span data-ttu-id="7b235-201">Conjuntos de datos tienen metadatos, en toocontent de adición.</span><span class="sxs-lookup"><span data-stu-id="7b235-201">Datasets have metadata, in addition toocontent.</span></span> <span data-ttu-id="7b235-202">(Los conjuntos de datos intermedios son una regla de excepción de toothis y no tiene ningún metadato.)</span><span class="sxs-lookup"><span data-stu-id="7b235-202">(Intermediate datasets are an exception toothis rule and do not have any metadata.)</span></span>

<span data-ttu-id="7b235-203">Algunos valores de metadatos son asignados por el usuario de hello en tiempo de creación:</span><span class="sxs-lookup"><span data-stu-id="7b235-203">Some metadata values are assigned by hello user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="7b235-204">Los demás son valores asignados por el Aprendizaje automático de Azure:</span><span class="sxs-lookup"><span data-stu-id="7b235-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="7b235-205">Vea hello `SourceDataset` clase para más de metadatos Hola disponibles.</span><span class="sxs-lookup"><span data-stu-id="7b235-205">See hello `SourceDataset` class for more on hello available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="7b235-206">Leer contenido</span><span class="sxs-lookup"><span data-stu-id="7b235-206">Read contents</span></span>
<span data-ttu-id="7b235-207">fragmentos de código de Hello proporcionados por estudio de aprendizaje automático automáticamente descargarán y deserializar el objeto de hello dataset tooa Pandas trama de datos.</span><span class="sxs-lookup"><span data-stu-id="7b235-207">hello code snippets provided by Machine Learning Studio automatically download and deserialize hello dataset tooa Pandas DataFrame object.</span></span> <span data-ttu-id="7b235-208">Esto se hace con hello `to_dataframe` método:</span><span class="sxs-lookup"><span data-stu-id="7b235-208">This is done with hello `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="7b235-209">Si prefiere datos sin procesar de toodownload hello y realizar la deserialización de hello usted mismo, es una opción.</span><span class="sxs-lookup"><span data-stu-id="7b235-209">If you prefer toodownload hello raw data, and perform hello deserialization yourself, that is an option.</span></span> <span data-ttu-id="7b235-210">En el momento de hello, esto es Hola única opción de formatos, como 'ARFF', no se puede deserializar la biblioteca de cliente de Python que Hola.</span><span class="sxs-lookup"><span data-stu-id="7b235-210">At hello moment, this is hello only option for formats such as 'ARFF', which hello Python client library cannot deserialize.</span></span>

<span data-ttu-id="7b235-211">contenido de hello tooread como texto:</span><span class="sxs-lookup"><span data-stu-id="7b235-211">tooread hello contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="7b235-212">contenido de hello tooread como binario:</span><span class="sxs-lookup"><span data-stu-id="7b235-212">tooread hello contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="7b235-213">También puede abrir un contenido de toohello la secuencia:</span><span class="sxs-lookup"><span data-stu-id="7b235-213">You can also just open a stream toohello contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="7b235-214">Crear un conjunto de datos nuevo</span><span class="sxs-lookup"><span data-stu-id="7b235-214">Create a new dataset</span></span>
<span data-ttu-id="7b235-215">biblioteca de cliente de Python de Hello permite tooupload conjuntos de datos desde el programa de Python.</span><span class="sxs-lookup"><span data-stu-id="7b235-215">hello Python client library allows you tooupload datasets from your Python program.</span></span> <span data-ttu-id="7b235-216">Estos conjuntos de datos estarán disponibles para utilizarse en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="7b235-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="7b235-217">Si tiene datos en una trama de datos de Pandas, use Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="7b235-217">If you have your data in a Pandas DataFrame, use hello following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="7b235-218">Si sus datos ya están serializados, puede utilizar:</span><span class="sxs-lookup"><span data-stu-id="7b235-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="7b235-219">biblioteca de cliente de Python Hello es capaz de tooserialize da formato a una trama de datos de Pandas toohello a continuación (constantes para estos están en hello `azureml.DataTypeIds` clase):</span><span class="sxs-lookup"><span data-stu-id="7b235-219">hello Python client library is able tooserialize a Pandas DataFrame toohello following formats (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="7b235-220">PlainText</span><span class="sxs-lookup"><span data-stu-id="7b235-220">PlainText</span></span>
* <span data-ttu-id="7b235-221">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="7b235-221">GenericCSV</span></span>
* <span data-ttu-id="7b235-222">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="7b235-222">GenericTSV</span></span>
* <span data-ttu-id="7b235-223">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="7b235-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="7b235-224">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="7b235-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="7b235-225">Actualizar un registro existente</span><span class="sxs-lookup"><span data-stu-id="7b235-225">Update an existing dataset</span></span>
<span data-ttu-id="7b235-226">Si intentas tooupload un nuevo conjunto de datos con un nombre que coincida con un conjunto de datos existente, debe obtener un error de conflicto.</span><span class="sxs-lookup"><span data-stu-id="7b235-226">If you try tooupload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="7b235-227">tooupdate un conjunto de datos existente, primero debe tooget un conjunto de datos de referencia toohello existente:</span><span class="sxs-lookup"><span data-stu-id="7b235-227">tooupdate an existing dataset, you first need tooget a reference toohello existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="7b235-228">A continuación, utilice `update_from_dataframe` tooserialize y reemplazar contenido Hola del conjunto de datos de hello en Azure:</span><span class="sxs-lookup"><span data-stu-id="7b235-228">Then use `update_from_dataframe` tooserialize and replace hello contents of hello dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="7b235-229">Si desea que el formato diferente del tooa tooserialize Hola datos, especifique un valor para hello opcional `data_type_id` parámetro.</span><span class="sxs-lookup"><span data-stu-id="7b235-229">If you want tooserialize hello data tooa different format, specify a value for hello optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="7b235-230">Opcionalmente, puede establecer una nueva descripción especificando un valor para hello `description` parámetro.</span><span class="sxs-lookup"><span data-stu-id="7b235-230">You can optionally set a new description by specifying a value for hello `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

<span data-ttu-id="7b235-231">Opcionalmente, puede establecer un nuevo nombre especificando un valor para hello `name` parámetro.</span><span class="sxs-lookup"><span data-stu-id="7b235-231">You can optionally set a new name by specifying a value for hello `name` parameter.</span></span> <span data-ttu-id="7b235-232">De ahora en adelante, recuperará Hola conjunto de datos con nombre nuevo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b235-232">From now on, you'll retrieve hello dataset using hello new name only.</span></span> <span data-ttu-id="7b235-233">Hola siguiente código actualiza la descripción, nombre y los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b235-233">hello following code updates hello data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="7b235-234">Hola `data_type_id`, `name` y `description` parámetros son opcionales y el valor anterior de tootheir predeterminado.</span><span class="sxs-lookup"><span data-stu-id="7b235-234">hello `data_type_id`, `name` and `description` parameters are optional and default tootheir previous value.</span></span> <span data-ttu-id="7b235-235">Hola `dataframe` parámetro siempre es necesario.</span><span class="sxs-lookup"><span data-stu-id="7b235-235">hello `dataframe` parameter is always required.</span></span>

<span data-ttu-id="7b235-236">Si sus datos ya están serializados, puede utilizar`update_from_raw_data` en lugar de `update_from_dataframe`.</span><span class="sxs-lookup"><span data-stu-id="7b235-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="7b235-237">Funcionará de una forma similar si pasa `raw_data` en lugar de `dataframe`.</span><span class="sxs-lookup"><span data-stu-id="7b235-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

