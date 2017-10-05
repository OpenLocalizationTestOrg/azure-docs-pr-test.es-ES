---
title: Acceso a conjuntos de datos con la biblioteca de cliente de Python de Machine Learning | Microsoft Docs
description: "Instale y use la biblioteca de cliente de Python para tener acceso y administrar datos de Aprendizaje automático de Azure de forma segura desde un entorno local de Python."
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
ms.openlocfilehash: e3ae712e0f8d386f637520fbbff4b348bc86f32d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="access-datasets-with-python-using-the-azure-machine-learning-python-client-library"></a><span data-ttu-id="f1811-103">Acceso a conjuntos de datos con Python mediante la biblioteca de cliente de Python de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="f1811-103">Access datasets with Python using the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="f1811-104">La versión preliminar de la biblioteca de cliente de Python de Aprendizaje automático de Microsoft Azure puede permitir un acceso seguro a los conjuntos de datos de Aprendizaje automático de Azure desde un entorno local de Python, así como la creación y administración de conjuntos de datos en un área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f1811-104">The preview of Microsoft Azure Machine Learning Python client library can enable secure access to your Azure Machine Learning datasets from a local Python environment and enables the creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="f1811-105">Este tema proporciona instrucciones sobre cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="f1811-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="f1811-106">instalar la biblioteca de cliente de Python de Aprendizaje automático;</span><span class="sxs-lookup"><span data-stu-id="f1811-106">install the Machine Learning Python client library</span></span> 
* <span data-ttu-id="f1811-107">obtener acceso y cargar conjuntos de datos, con instrucciones sobre cómo obtener autorización para el acceso a conjuntos de datos de Aprendizaje automático de Azure desde el entorno local de Python;</span><span class="sxs-lookup"><span data-stu-id="f1811-107">access and upload datasets, including instructions on how to get authorization to access Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="f1811-108">obtener acceso a los conjuntos de datos intermedios de experimentos;</span><span class="sxs-lookup"><span data-stu-id="f1811-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="f1811-109">usar la biblioteca de cliente de Python para enumerar conjuntos de datos, obtener acceso a los metadatos, leer el contenido de un conjunto de datos, crear nuevos conjuntos de datos y actualizar conjuntos de datos existentes.</span><span class="sxs-lookup"><span data-stu-id="f1811-109">use the Python client library to enumerate datasets, access metadata, read the contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="f1811-110"><a name="prerequisites"></a>Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f1811-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="f1811-111">La biblioteca de cliente de Python se ha probado en los siguientes entornos:</span><span class="sxs-lookup"><span data-stu-id="f1811-111">The Python client library has been tested under the following environments:</span></span>

* <span data-ttu-id="f1811-112">Windows, Mac y Linux</span><span class="sxs-lookup"><span data-stu-id="f1811-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="f1811-113">Python 2.7, 3.3 y 3.4</span><span class="sxs-lookup"><span data-stu-id="f1811-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="f1811-114">Tiene una dependencia en los siguientes paquetes:</span><span class="sxs-lookup"><span data-stu-id="f1811-114">It has a dependency on the following packages:</span></span>

* <span data-ttu-id="f1811-115">Solicitudes</span><span class="sxs-lookup"><span data-stu-id="f1811-115">requests</span></span>
* <span data-ttu-id="f1811-116">Python-dateutil</span><span class="sxs-lookup"><span data-stu-id="f1811-116">python-dateutil</span></span>
* <span data-ttu-id="f1811-117">Pandas</span><span class="sxs-lookup"><span data-stu-id="f1811-117">pandas</span></span>

<span data-ttu-id="f1811-118">Se recomienda utilizar una distribución de Python como [Anaconda](http://continuum.io/downloads#all) o [Canopy](https://store.enthought.com/downloads/), incluidas con Python, IPython y los tres paquetes instalados enumerados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f1811-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and the three packages listed above installed.</span></span> <span data-ttu-id="f1811-119">Aunque IPython no es estrictamente necesario, es un excelente entorno para manipular y visualizar datos de forma interactiva.</span><span class="sxs-lookup"><span data-stu-id="f1811-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="f1811-120"><a name="installation"></a>Cómo instalar la biblioteca de cliente de Python de Aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="f1811-120"><a name="installation"></a>How to install the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="f1811-121">La biblioteca cliente de Python de Azure Machine Learning también debe instalarse para completar las tareas descritas en este tema.</span><span class="sxs-lookup"><span data-stu-id="f1811-121">The Azure Machine Learning Python client library must also be installed to complete the tasks outlined in this topic.</span></span> <span data-ttu-id="f1811-122">Está disponible desde el [Índice de paquetes de Python](https://pypi.python.org/pypi/azureml).</span><span class="sxs-lookup"><span data-stu-id="f1811-122">It is available from the [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="f1811-123">Para instalarlo en su entorno de Python, ejecute el siguiente comando desde el entorno de Python local:</span><span class="sxs-lookup"><span data-stu-id="f1811-123">To install it in your Python environment, run the following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="f1811-124">Como alternativa, puede descargar e instalar desde los orígenes de [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span><span class="sxs-lookup"><span data-stu-id="f1811-124">Alternatively, you can download and install from the sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="f1811-125">Si tiene git instalado en su equipo, puede usar pip para instalar directamente desde el repositorio de git:</span><span class="sxs-lookup"><span data-stu-id="f1811-125">If you have git installed on your machine, you can use pip to install directly from the git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="f1811-126"><a name="datasetAccess"></a>Utilizar fragmentos de código del Estudio para tener acceso a los conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="f1811-126"><a name="datasetAccess"></a>Use Studio Code snippets to access datasets</span></span>
<span data-ttu-id="f1811-127">La biblioteca de cliente de Python proporciona acceso mediante programación a los conjuntos de datos existentes de los experimentos que se han ejecutado.</span><span class="sxs-lookup"><span data-stu-id="f1811-127">The Python client library gives you programmatic access to your existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="f1811-128">Desde la interfaz de web del Estudio, puede generar fragmentos de código que incluyen toda la información necesaria para descargar y deserializar los conjuntos de datos como objetos Pandas DataFrame en el equipo de la ubicación.</span><span class="sxs-lookup"><span data-stu-id="f1811-128">From the Studio web interface, you can generate code snippets that include all the necessary information to download and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="f1811-129"><a name="security"></a>Seguridad de acceso a datos</span><span class="sxs-lookup"><span data-stu-id="f1811-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="f1811-130">Los fragmentos de código proporcionados por el Estudio para su uso con la biblioteca de cliente de Python incluyen el identificador de área de trabajo y el token de autorización.</span><span class="sxs-lookup"><span data-stu-id="f1811-130">The code snippets provided by Studio for use with the Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="f1811-131">Estos proporcionan acceso completo a su área de trabajo y se deben proteger, como una contraseña.</span><span class="sxs-lookup"><span data-stu-id="f1811-131">These provide full access to your workspace and must be protected, like a password.</span></span>

<span data-ttu-id="f1811-132">Por motivos de seguridad, la funcionalidad de fragmento de código solo está disponible para los usuarios que tengan su rol definido como **Propietario** para el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f1811-132">For security reasons, the code snippet functionality is only available to users that have their role set as **Owner** for the workspace.</span></span> <span data-ttu-id="f1811-133">Su rol se muestra en la página **USUARIOS** de Azure Machine Learning Studio, en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="f1811-133">Your role is displayed in Azure Machine Learning Studio on the **USERS** page under **Settings**.</span></span>

![Seguridad][security]

<span data-ttu-id="f1811-135">Si su rol no está establecido como **Propietario**, puede solicitar que se le vuelva a invitar como propietario o pedir al propietario del área de trabajo que le proporcione el fragmento de código.</span><span class="sxs-lookup"><span data-stu-id="f1811-135">If your role is not set as **Owner**, you can either request to be reinvited as an owner, or ask the owner of the workspace to provide you with the code snippet.</span></span>

<span data-ttu-id="f1811-136">Para obtener el token de autorización, puede realizar una de las acciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="f1811-136">To obtain the authorization token, you can do one of the following:</span></span>

* <span data-ttu-id="f1811-137">Solicite un token a un propietario.</span><span class="sxs-lookup"><span data-stu-id="f1811-137">Ask for a token from an owner.</span></span> <span data-ttu-id="f1811-138">Los propietarios pueden tener acceso a sus tokens de autorización en la página Configuración de su área de trabajo en el Estudio.</span><span class="sxs-lookup"><span data-stu-id="f1811-138">Owners can access their authorization tokens from the Settings page of their workspace in Studio.</span></span> <span data-ttu-id="f1811-139">Seleccione **Configuración** en el panel izquierdo y haga clic en **TOKENS DE AUTORIZACIÓN** para ver los tokens primarios y secundarios.</span><span class="sxs-lookup"><span data-stu-id="f1811-139">Select **Settings** from the left pane and click **AUTHORIZATION TOKENS** to see the primary and secondary tokens.</span></span>  <span data-ttu-id="f1811-140">Aunque se pueden utilizar los tokens de autorización principales y secundarios, se recomienda que los propietarios solo compartan los tokens de autorización secundarios.</span><span class="sxs-lookup"><span data-stu-id="f1811-140">Although either the primary or the secondary authorization tokens can be used in the code snippet, it is recommended that owners only share the secondary authorization tokens.</span></span>

![Tokens de autorización](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="f1811-142">Pida que le amplíen al rol de propietario.</span><span class="sxs-lookup"><span data-stu-id="f1811-142">Ask to be promoted to role of owner.</span></span>  <span data-ttu-id="f1811-143">Para ello, un propietario actual del área de trabajo debe quitarle primero del área de trabajo y, a continuación, volver a invitarle como propietario.</span><span class="sxs-lookup"><span data-stu-id="f1811-143">To do this, a current owner of the workspace needs to first remove you from the workspace then re-invite you to it as an owner.</span></span>

<span data-ttu-id="f1811-144">Cuando los desarrolladores hayan obtenido el identificador de área de trabajo y el token de autorización, podrán acceder al área de trabajo usando el fragmento de código independientemente de su rol.</span><span class="sxs-lookup"><span data-stu-id="f1811-144">Once developers have obtained the workspace id and authorization token, they are able to access the workspace using the code snippet regardless of their role.</span></span>

<span data-ttu-id="f1811-145">Los tokens de autorización se administran en la página **TOKENS DE AUTORIZACIÓN**, en **CONFIGURACIÓN**.</span><span class="sxs-lookup"><span data-stu-id="f1811-145">Authorization tokens are managed on the **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="f1811-146">Puede volver a generarlos, pero este procedimiento revoca el acceso al token anterior.</span><span class="sxs-lookup"><span data-stu-id="f1811-146">You can regenerate them, but this procedure revokes access to the previous token.</span></span>

### <span data-ttu-id="f1811-147"><a name="accessingDatasets"></a>Obtener acceso a los conjuntos de datos desde una aplicación local de Python</span><span class="sxs-lookup"><span data-stu-id="f1811-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="f1811-148">En Machine Learning Studio, haga clic en la opción **CONJUNTOS DE DATOS** de la barra de navegación de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="f1811-148">In Machine Learning Studio, click **DATASETS** in the navigation bar on the left.</span></span>
2. <span data-ttu-id="f1811-149">Seleccione el conjunto de datos al que le gustaría tener acceso.</span><span class="sxs-lookup"><span data-stu-id="f1811-149">Select the dataset you would like to access.</span></span> <span data-ttu-id="f1811-150">Puede seleccionar cualquiera de los conjuntos de datos de las listas **MIS CONJUNTOS DE DATOS** o **EJEMPLOS**.</span><span class="sxs-lookup"><span data-stu-id="f1811-150">You can select any of the datasets from the **MY DATASETS** list or from the **SAMPLES** list.</span></span>
3. <span data-ttu-id="f1811-151">En la barra de herramientas de la parte inferior, haga clic en **Generate Data Access Code**(Generar código de acceso a datos).</span><span class="sxs-lookup"><span data-stu-id="f1811-151">From the bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="f1811-152">Este botón se deshabilitará si los datos están en un formato no compatible con la biblioteca cliente de Python.</span><span class="sxs-lookup"><span data-stu-id="f1811-152">If the data is in a format incompatible with the Python client library, this button is disabled.</span></span>
   
    ![CONJUNTOS DE DATOS][datasets]
4. <span data-ttu-id="f1811-154">Seleccione el fragmento de código de la ventana que aparece y cópielo al Portapapeles.</span><span class="sxs-lookup"><span data-stu-id="f1811-154">Select the code snippet from the window that appears and copy it to your clipboard.</span></span>
   
    ![Código de acceso][dataset-access-code]
5. <span data-ttu-id="f1811-156">Pegue el código en el Bloc de notas de su aplicación local de Python.</span><span class="sxs-lookup"><span data-stu-id="f1811-156">Paste the code into the notebook of your local Python application.</span></span>
   
    ![Bloc de notas][ipython-dataset]

## <span data-ttu-id="f1811-158"><a name="accessingIntermediateDatasets"></a>Obtener acceso a los conjuntos de datos intermedios de experimentos de Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="f1811-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="f1811-159">Después de ejecutar un experimento en el Estudio de aprendizaje automático, es posible tener acceso a los conjuntos de datos intermedios desde los nodos de salida de los módulos.</span><span class="sxs-lookup"><span data-stu-id="f1811-159">After an experiment is run in the Machine Learning Studio, it is possible to access the intermediate datasets from the output nodes of modules.</span></span> <span data-ttu-id="f1811-160">Los conjuntos de datos intermedios son datos que se han creado y utilizado para pasos intermedios cuando se ha ejecutado una herramienta de modelo.</span><span class="sxs-lookup"><span data-stu-id="f1811-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="f1811-161">El acceso a los conjuntos de datos intermedios es posible siempre que el formato de los datos sea compatible con la biblioteca de cliente de Python.</span><span class="sxs-lookup"><span data-stu-id="f1811-161">Intermediate datasets can be accessed as long as the data format is compatible with the Python client library.</span></span>

<span data-ttu-id="f1811-162">Se admiten los siguientes formatos (sus constantes están en la clase `azureml.DataTypeIds` ):</span><span class="sxs-lookup"><span data-stu-id="f1811-162">The following formats are supported (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="f1811-163">PlainText</span><span class="sxs-lookup"><span data-stu-id="f1811-163">PlainText</span></span>
* <span data-ttu-id="f1811-164">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="f1811-164">GenericCSV</span></span>
* <span data-ttu-id="f1811-165">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="f1811-165">GenericTSV</span></span>
* <span data-ttu-id="f1811-166">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="f1811-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="f1811-167">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="f1811-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="f1811-168">Puede determinar el formato desplazando el mouse sobre un nodo de salida del módulo.</span><span class="sxs-lookup"><span data-stu-id="f1811-168">You can determine the format by hovering over a module output node.</span></span> <span data-ttu-id="f1811-169">Aparecerá junto al nombre del nodo, en la información sobre herramientas.</span><span class="sxs-lookup"><span data-stu-id="f1811-169">It is displayed along with the node name, in a tooltip.</span></span>

<span data-ttu-id="f1811-170">Algunos de los módulos, como el de [División][split], dan como resultado un formato denominado `Dataset`, que no es compatible con la biblioteca de cliente de Python.</span><span class="sxs-lookup"><span data-stu-id="f1811-170">Some of the modules, such as the [Split][split] module, output to a format named `Dataset`, which is not supported by the Python client library.</span></span>

![Formato de conjunto de datos][dataset-format]

<span data-ttu-id="f1811-172">Necesitará usar un módulo de conversión, como [Convertir en CSV][convert-to-csv], para obtener un resultado en un formato compatible.</span><span class="sxs-lookup"><span data-stu-id="f1811-172">You need to use a conversion module, such as [Convert to CSV][convert-to-csv], to get an output into a supported format.</span></span>

![Formato GenericCSV][csv-format]

<span data-ttu-id="f1811-174">Los pasos siguientes muestran un ejemplo que crea un experimento, lo ejecuta y tiene acceso al conjunto de datos intermedio.</span><span class="sxs-lookup"><span data-stu-id="f1811-174">The following steps show an example that creates an experiment, runs it and accesses the intermediate dataset.</span></span>

1. <span data-ttu-id="f1811-175">Cree un experimento nuevo.</span><span class="sxs-lookup"><span data-stu-id="f1811-175">Create a new experiment.</span></span>
2. <span data-ttu-id="f1811-176">Inserte un módulo **Conjunto de datos de clasificación binaria de ingresos en el censo de adultos** .</span><span class="sxs-lookup"><span data-stu-id="f1811-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="f1811-177">Inserte un módulo [División][split] y conecte su entrada a la salida del módulo del conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="f1811-177">Insert a [Split][split] module, and connect its input to the dataset module output.</span></span>
4. <span data-ttu-id="f1811-178">Inserte un módulo [Convertir a CSV][convert-to-csv] y conecte su entrada a una de las salidas del módulo [División][split].</span><span class="sxs-lookup"><span data-stu-id="f1811-178">Insert a [Convert to CSV][convert-to-csv] module and connect its input to one of the [Split][split] module outputs.</span></span>
5. <span data-ttu-id="f1811-179">Guarde el experimento, ejecútelo y espere a que finalice su ejecución.</span><span class="sxs-lookup"><span data-stu-id="f1811-179">Save the experiment, run it, and wait for it to finish running.</span></span>
6. <span data-ttu-id="f1811-180">Haga clic en el nodo de salida del módulo [Convertir en CSV][convert-to-csv].</span><span class="sxs-lookup"><span data-stu-id="f1811-180">Click the output node on the [Convert to CSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="f1811-181">Cuando aparezca el menú contextual, seleccione **Generar código de acceso a datos**.</span><span class="sxs-lookup"><span data-stu-id="f1811-181">When the context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![Menú contextual][experiment]
8. <span data-ttu-id="f1811-183">Seleccione el fragmento de código y cópielo en la ventana que se muestra.</span><span class="sxs-lookup"><span data-stu-id="f1811-183">Select the code snippet and copy it to your clipboard from the window that appears.</span></span>
   
    ![Código de acceso][intermediate-dataset-access-code]
9. <span data-ttu-id="f1811-185">Pegue el código en el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="f1811-185">Paste the code in your notebook.</span></span>
   
    ![Bloc de notas][ipython-intermediate-dataset]
10. <span data-ttu-id="f1811-187">Puede visualizar los datos con matplotlib.</span><span class="sxs-lookup"><span data-stu-id="f1811-187">You can visualize the data using matplotlib.</span></span> <span data-ttu-id="f1811-188">Esto se muestra en un histograma de la columna de tiempo:</span><span class="sxs-lookup"><span data-stu-id="f1811-188">This displays in a histogram for the age column:</span></span>
    
    ![Histograma][ipython-histogram]

## <span data-ttu-id="f1811-190"><a name="clientApis"></a>Use la biblioteca de cliente de Python de Aprendizaje automático para obtener acceso, leer, crear y administrar conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="f1811-190"><a name="clientApis"></a>Use the Machine Learning Python client library to access, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="f1811-191">Área de trabajo</span><span class="sxs-lookup"><span data-stu-id="f1811-191">Workspace</span></span>
<span data-ttu-id="f1811-192">El área de trabajo es el punto de entrada para la biblioteca de cliente de Python.</span><span class="sxs-lookup"><span data-stu-id="f1811-192">The workspace is the entry point for the Python client library.</span></span> <span data-ttu-id="f1811-193">Proporcione la clase `Workspace` con su id. de área de trabajo y token de autorización para crear una instancia:</span><span class="sxs-lookup"><span data-stu-id="f1811-193">Provide the `Workspace` class with your workspace id and authorization token to create an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="f1811-194">Enumerar los conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="f1811-194">Enumerate datasets</span></span>
<span data-ttu-id="f1811-195">Para enumerar todos los conjuntos de datos en un área determinado:</span><span class="sxs-lookup"><span data-stu-id="f1811-195">To enumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="f1811-196">Para enumerar solo los conjuntos de datos creados por el usuario:</span><span class="sxs-lookup"><span data-stu-id="f1811-196">To enumerate just the user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="f1811-197">Para enumerar solo los conjuntos de datos de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f1811-197">To enumerate just the example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="f1811-198">Puede tener acceso a un conjunto de datos por nombre (que distingue mayúsculas de minúsculas):</span><span class="sxs-lookup"><span data-stu-id="f1811-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="f1811-199">O bien, puede tener acceso a él por su índice:</span><span class="sxs-lookup"><span data-stu-id="f1811-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="f1811-200">Metadatos</span><span class="sxs-lookup"><span data-stu-id="f1811-200">Metadata</span></span>
<span data-ttu-id="f1811-201">Los conjuntos de datos tienen metadatos, además de contenido.</span><span class="sxs-lookup"><span data-stu-id="f1811-201">Datasets have metadata, in addition to content.</span></span> <span data-ttu-id="f1811-202">(Los conjuntos de datos intermedios son una excepción a esta regla y no tienen metadatos).</span><span class="sxs-lookup"><span data-stu-id="f1811-202">(Intermediate datasets are an exception to this rule and do not have any metadata.)</span></span>

<span data-ttu-id="f1811-203">Algunos valores de metadatos son asignados por el usuario en tiempo de creación:</span><span class="sxs-lookup"><span data-stu-id="f1811-203">Some metadata values are assigned by the user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="f1811-204">Los demás son valores asignados por el Aprendizaje automático de Azure:</span><span class="sxs-lookup"><span data-stu-id="f1811-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="f1811-205">Vea la clase `SourceDataset` para obtener más información sobre los metadatos disponibles.</span><span class="sxs-lookup"><span data-stu-id="f1811-205">See the `SourceDataset` class for more on the available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="f1811-206">Leer contenido</span><span class="sxs-lookup"><span data-stu-id="f1811-206">Read contents</span></span>
<span data-ttu-id="f1811-207">Los fragmentos de código que proporciona el Estudio de aprendizaje automático descargan y deserializan automáticamente el conjunto de datos a un objeto Pandas DataFrame.</span><span class="sxs-lookup"><span data-stu-id="f1811-207">The code snippets provided by Machine Learning Studio automatically download and deserialize the dataset to a Pandas DataFrame object.</span></span> <span data-ttu-id="f1811-208">Esto se hace en el método `to_dataframe` :</span><span class="sxs-lookup"><span data-stu-id="f1811-208">This is done with the `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="f1811-209">Si prefiere descargar los datos sin procesar y realizar la deserialización usted mismo, tiene esa opción.</span><span class="sxs-lookup"><span data-stu-id="f1811-209">If you prefer to download the raw data, and perform the deserialization yourself, that is an option.</span></span> <span data-ttu-id="f1811-210">En este momento, esta es la única opción para formatos como 'ARFF', que la biblioteca de cliente de Python no puede deserializar.</span><span class="sxs-lookup"><span data-stu-id="f1811-210">At the moment, this is the only option for formats such as 'ARFF', which the Python client library cannot deserialize.</span></span>

<span data-ttu-id="f1811-211">Para leer el contenido como texto:</span><span class="sxs-lookup"><span data-stu-id="f1811-211">To read the contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="f1811-212">Para leer el contenido como binario:</span><span class="sxs-lookup"><span data-stu-id="f1811-212">To read the contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="f1811-213">También puede abrir una secuencia para el contenido:</span><span class="sxs-lookup"><span data-stu-id="f1811-213">You can also just open a stream to the contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="f1811-214">Crear un conjunto de datos nuevo</span><span class="sxs-lookup"><span data-stu-id="f1811-214">Create a new dataset</span></span>
<span data-ttu-id="f1811-215">La biblioteca cliente de Python permite cargar conjuntos de datos desde el programa de Python.</span><span class="sxs-lookup"><span data-stu-id="f1811-215">The Python client library allows you to upload datasets from your Python program.</span></span> <span data-ttu-id="f1811-216">Estos conjuntos de datos estarán disponibles para utilizarse en el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f1811-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="f1811-217">Si tiene sus datos en un Pandas DataFrame, utilice el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="f1811-217">If you have your data in a Pandas DataFrame, use the following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="f1811-218">Si sus datos ya están serializados, puede utilizar:</span><span class="sxs-lookup"><span data-stu-id="f1811-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="f1811-219">La biblioteca cliente de Python puede serializar una trama de datos de Pandas en los siguientes formatos (sus constantes se encuentran en la clase `azureml.DataTypeIds` ):</span><span class="sxs-lookup"><span data-stu-id="f1811-219">The Python client library is able to serialize a Pandas DataFrame to the following formats (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="f1811-220">PlainText</span><span class="sxs-lookup"><span data-stu-id="f1811-220">PlainText</span></span>
* <span data-ttu-id="f1811-221">GenericCSV</span><span class="sxs-lookup"><span data-stu-id="f1811-221">GenericCSV</span></span>
* <span data-ttu-id="f1811-222">GenericTSV</span><span class="sxs-lookup"><span data-stu-id="f1811-222">GenericTSV</span></span>
* <span data-ttu-id="f1811-223">GenericCSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="f1811-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="f1811-224">GenericTSVNoHeader</span><span class="sxs-lookup"><span data-stu-id="f1811-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="f1811-225">Actualizar un registro existente</span><span class="sxs-lookup"><span data-stu-id="f1811-225">Update an existing dataset</span></span>
<span data-ttu-id="f1811-226">Si trata de cargar un nuevo conjunto de datos con un nombre que coincida con un conjunto de datos existente, debería recibir un error de conflicto.</span><span class="sxs-lookup"><span data-stu-id="f1811-226">If you try to upload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="f1811-227">Para actualizar un conjunto de datos existente, primero debe obtener una referencia al conjunto de datos existente:</span><span class="sxs-lookup"><span data-stu-id="f1811-227">To update an existing dataset, you first need to get a reference to the existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="f1811-228">A continuación, utilice `update_from_dataframe` para serializar y reemplazar el contenido del conjunto de datos en Azure:</span><span class="sxs-lookup"><span data-stu-id="f1811-228">Then use `update_from_dataframe` to serialize and replace the contents of the dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="f1811-229">Si desea serializar los datos a un formato diferente, especifique un valor para el parámetro opcional `data_type_id` .</span><span class="sxs-lookup"><span data-stu-id="f1811-229">If you want to serialize the data to a different format, specify a value for the optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="f1811-230">Opcionalmente, puede definir una nueva descripción especificando un valor para el parámetro `description` .</span><span class="sxs-lookup"><span data-stu-id="f1811-230">You can optionally set a new description by specifying a value for the `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up to feb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to feb 2015'

<span data-ttu-id="f1811-231">Opcionalmente, puede definir un nuevo nombre especificando un valor para el parámetro `name` .</span><span class="sxs-lookup"><span data-stu-id="f1811-231">You can optionally set a new name by specifying a value for the `name` parameter.</span></span> <span data-ttu-id="f1811-232">De ahora en adelante, solo podrá recuperar el conjunto de datos con el nuevo nombre.</span><span class="sxs-lookup"><span data-stu-id="f1811-232">From now on, you'll retrieve the dataset using the new name only.</span></span> <span data-ttu-id="f1811-233">El siguiente código actualiza los datos, el nombre y la descripción.</span><span class="sxs-lookup"><span data-stu-id="f1811-233">The following code updates the data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up to feb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up to feb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="f1811-234">Los parámetros `data_type_id`, `name` y `description` son opcionales y tienen el valor anterior como predeterminado.</span><span class="sxs-lookup"><span data-stu-id="f1811-234">The `data_type_id`, `name` and `description` parameters are optional and default to their previous value.</span></span> <span data-ttu-id="f1811-235">El parámetro `dataframe` siempre es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="f1811-235">The `dataframe` parameter is always required.</span></span>

<span data-ttu-id="f1811-236">Si sus datos ya están serializados, puede utilizar`update_from_raw_data` en lugar de `update_from_dataframe`.</span><span class="sxs-lookup"><span data-stu-id="f1811-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="f1811-237">Funcionará de una forma similar si pasa `raw_data` en lugar de `dataframe`.</span><span class="sxs-lookup"><span data-stu-id="f1811-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

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

