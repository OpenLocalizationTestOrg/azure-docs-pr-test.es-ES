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
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a>Diez cosas que puede hacer en la ciencia de datos de hello Máquina Virtual
Hola Máquina Virtual de ciencia de datos de Microsoft (DSVM) es un entorno de desarrollo de ciencia de datos eficaz que permite tooperform diversas tareas de exploración y el modelado de datos. Hello entorno viene ya compilado e integrados con datos muy popular varias herramientas de análisis que hacen que sea fácil tooget a trabajar rápidamente con el análisis local, en la nube o híbridas implementaciones. Hola DSVM trabaja en estrecha colaboración con muchos servicios de Azure y es capaz de tooread y procesar los datos que ya está almacenados en Azure, en almacenamiento de datos de SQL Azure Data Lake de Azure, almacenamiento de Azure, o en la base de datos de Azure Cosmos. También puede sacar provecho de otras herramientas de análisis como Aprendizaje automático de Azure y Data Factory de Azure.

En este artículo se le guiará por el proceso de toouse su tooperform DSVM ciencia de datos de varias tareas e interactuar con otros servicios de Azure. Estas son algunas de las acciones de Hola que puede realizar en hello DSVM:

1. Explorar datos y desarrollar modelos de forma local en hello DSVM mediante Microsoft R Server, Python
2. Usar un tooexperiment de Jupyter notebook con los datos en un explorador utilizando una versión lista de enterprise de R diseñado para escalabilidad y rendimiento de Python 2, 3 de Python, Microsoft R
3. Poner en operación los modelos creados con R y Python en Aprendizaje automático de Azure para que aplicaciones cliente puedan tener acceso a los modelos mediante una sencilla interfaz de servicios web
4. Administrar los recursos de Azure mediante Azure Portal o PowerShell
5. Ampliar el espacio de almacenamiento y compartir código o conjuntos de datos de gran escala entre todo el equipo mediante la creación de almacenamiento de archivos de Azure como una unidad que se puede montar en la máquina virtual de ciencia de datos (DSVM)
6. Compartir código con su equipo mediante GitHub y obtener acceso a su repositorio mediante Hola preinstalados clientes Git - Git Bash, Git GUI.
7. Acceder a diversos servicios de análisis y datos de Azure, como Azure Blob Storage, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse y bases de datos
8. Crear informes y panel con Power BI Desktop preinstalado en hello DSVM Hola e implementarlas en la nube de Hola
9. Escalar dinámicamente su toomeet DSVM que su proyecto necesite
10. Instalar herramientas adicionales en la máquina virtual   

> [!NOTE]
> Se aplican cargos de uso adicionales para muchos de los servicios de almacenamiento y análisis de la datos adicionales de hello enumerados en este artículo. Consulte toohello [precios de Azure](https://azure.microsoft.com/pricing/) página para obtener más información.
> 
> 

**Requisitos previos**

* Necesita una suscripción de Azure. Puede suscribirse a una evaluación gratuita [aquí](https://azure.microsoft.com/free/).
* Las instrucciones para el aprovisionamiento de un Data Science Virtual Machine en hello portal de Azure están disponibles en [crear una máquina virtual](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a>1. Explorar datos y desarrollar modelos con el Servidor R de Microsoft o Python
Puede usar los análisis de datos de lenguajes como toodo R y Python derecha en hello DSVM.

Para R, puede usar un IDE llamado "Revolution R Enterprise 8.0" que se pueden encontrar en el menú de inicio de Hola o escritorio Hola. Microsoft ofrece bibliotecas adicionales además de los Hola abierto tooenable de origen/CRAN-R escalable hello y análisis de capacidad tooanalyze datos mayor que el tamaño de memoria de hello permitido realizando análisis en paralelo fragmentado. También puede instalar el IDE de R que prefiera, como [RStudio](https://www.rstudio.com/products/rstudio-desktop/).

Para Python, puede usar un IDE como Visual Studio Community Edition que tiene Hola Python Tools para la extensión de Visual Studio (PTVS) preinstalado. De forma predeterminada, en PTVS solo está configurada una versión básica de Python 2.7 (sin ninguna biblioteca de análisis como SciKit o Pandas). En orden tooenable Anaconda Python 2.7 y 3.5, necesita toodo Hola siguiente:

* Crear entornos personalizados para cada versión desplazándose demasiado**herramientas** -> **Python Tools** -> **entornos de Python** y, a continuación, haga clic en " **+ Personalizado**"en Visual Studio 2015 Community Edition Hola
* Escriba una descripción y establezca el entorno de hello las rutas de acceso de prefijo como *c:\anaconda* Anaconda Python 2.7 o *c:\anaconda\envs\py35* para Anaconda Python 3.5
* Haga clic en **detección automática** y, a continuación, **aplicar** entorno de hello toosave.

Esta es la configuración de entorno personalizado Hola aspecto en Visual Studio.

![Programa de instalación de PTVS](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

Vea hello [documentación PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) para obtener más información acerca de cómo toocreate entornos de Python.

Ahora se configuran toocreate un nuevo proyecto de Python. Navegue demasiado**archivo** -> **New** -> **proyecto** -> **Python** y seleccione el tipo de saludo de Aplicación de Python que se va a compilar. Se puede establecer el entorno de Python de Hola Hola actual proyecto toohello versión deseada (Anaconda 2.7 o 3.5): Hola contextual **entorno de Python**, seleccione **entornos de Python de agregar o quitar**, y a continuación, seleccione Hola deseado entorno tooassociate con proyecto Hola. Puede encontrar más información sobre cómo trabajar con PTVS en producto hello [documentación](https://github.com/Microsoft/PTVS/wiki) página.

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a>2. Con un modelo y Jupyter Notebook tooexplore sus datos con Python o R
Hola Jupyter Notebook es un entorno eficaz que proporciona una basada en explorador "IDE" para el modelado y exploración de datos. Puede utilizar Python 2, 3 de Python o R (código abierto y Hola Microsoft R Server) en Jupyter Notebook.

Hola toolaunch Jupyter Notebook haga clic en el icono de menú de inicio de Hola / titulada de icono del escritorio **Jupyter Notebook**. En hello DSVM también puede examinar demasiado "https://localhost:9999 /" tooaccess Hola Jupiter Bloc de notas. Si le pide una contraseña, use las instrucciones proporcionadas en hello ***cómo toocreate una contraseña segura en el servidor de hello Jupyter notebook*** sección de hello [Hola aprovisionar Microsoft Data Science Virtual Machine](machine-learning-data-science-provision-vm.md)tema toocreate contraseña segura tooaccess hello Jupyter notebook. 

Una vez abierto el Bloc de notas de hello, debería ver un directorio que contiene unos blocs de notas de ejemplo que están preconfiguradas en hello DSVM. Ahora puede:

* Haga clic en el código de hello toosee de hello Bloc de notas.
* Ejecutar cada celda presionando **MAYÚS+ENTRAR**.
* ejecutar el Bloc de notas completo Hola haciendo clic en **celda** -> **ejecutar**
* crear un nuevo bloc de notas haciendo clic en hello Jupyter icono (esquina superior izquierda) y, a continuación, haga clic en **New** botón en hello derecho y, a continuación, elegir el idioma de Bloc de notas de hello (también conocido como kernels).   

> [!NOTE]
> Actualmente admitimos Python 2.7, Python 3.5 y R. kernel Hola R para admitir la programación en código abierto R así como enterprise Hola escalable Microsoft R Server.   
> 
> 

Una vez que esté en el Bloc de notas de Hola puede explorar los datos, generar modelo hello, probar modelo Hola utilizando su elección de bibliotecas.

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a>3. Compilación de modelos mediante R y Python, y hacer que estén operativos mediante Aprendizaje automático de Azure
Una vez que ha creado y ha validado el modelo Hola próximo paso es normalmente toodeploy en producción. Esto permite a su cliente predicciones de modelo de aplicaciones tooinvoke hello en un tiempo real o en una base de modo por lotes. Aprendizaje automático de Azure proporciona un mecanismo toooperationalize un modelo integrado de R o Python.

Cuando se ponga en acción el modelo de aprendizaje automático de Azure, se expone un servicio web que permite a los clientes toomake llamadas REST que pasan parámetros de entrada y reciban las predicciones de modelo de hello como salidas.   

> [!NOTE]
> Si no aún registrarse para el aprendizaje automático de Azure, puede obtener un área de trabajo estándar o un área de trabajo gratuita visitando hello [estudio de aprendizaje automático de Azure](https://studio.azureml.net/) página principal y haga clic en "Introducción".   
> 
> 

### <a name="build-and-operationalize-python-models"></a>Compilación y puesta en operación de modelos de Python
Este es un fragmento de código desarrollado en Python Jupyter Notebook que compile un modelo simple utilizando biblioteca SciKit: Obtenga información de Hola.

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

método Hello usa toodeploy su tooAzure de modelos de python aprendizaje automático ajusta Hola predicción de modelo de Hola a una función y decora con atributos proporcionados por la biblioteca de python de aprendizaje automático de Azure preinstalada de Hola que indican su equipo de Azure Id. de área de trabajo de aprendizaje y la clave de API, Hola de entrada y devuelven los parámetros.  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

Un cliente ahora puede realizar llamadas toohello web service. Hay contenedores de conveniencia que construyen las solicitudes de API de REST de Hola. Este es un servicio web de ejemplo código tooconsume Hola.

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> biblioteca de aprendizaje automático de Azure Hola solo se admite actualmente en Python 2.7.   
> 
> 

### <a name="build-and-operationalize-r-models"></a>Compilación y puesta en operación de modelos de R
Puede implementar modelos de R generados en hello Data Science Virtual Machine o en otro lugar en aprendizaje automático de Azure de forma que sea similar toohow se realiza para Python. Su Hola pasos:

* crear un tooprovide de archivo settings.json el Id. de área de trabajo y la autenticación de token tal y como se muestra en el siguiente ejemplo de código de hello.
* escribir un contenedor para el modelo de hello predict, función.
* llamar a ```publishWebService``` en hello toopass de biblioteca de aprendizaje automático de Azure en el contenedor de la función de Hola.  

Aquí es Hola procedimiento y fragmentos de código que pueden ser usado tooset up, compilar, publicar y consumir un modelo como un servicio web de aprendizaje automático de Azure.

#### <a name="setup"></a>Configuración
1. Instalar paquetes de R de aprendizaje de máquina de hello escribiendo ```install.packages("AzureML")``` en Revolution R Enterprise 8.0 IDE o en el IDE de R.
2. Descargue la RTools de [aquí](https://cran.r-project.org/bin/windows/Rtools/). Debe Hola zip utilidad en la ruta de acceso de hello (y con nombre zip.exe) toooperationalize el paquete de R en aprendizaje automático.
3. Crear un archivo settings.json en un directorio denominado ```.azureml``` en su directorio particular y escriba los parámetros de Hola desde el área de trabajo de aprendizaje automático de Azure:

Estructura del archivo settings.json:

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a>Creación de un modelo en R y posterior publicación en Azure Machine Learning
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

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a>Consumir el modelo de hello implementado en aprendizaje automático de Azure
modelo de hello tooconsume desde una aplicación cliente, usamos toolook de biblioteca de aprendizaje automático de Azure Hola seguridad Hola servicio web publicado por nombre usando hello `services` el punto de conexión de API llamada toodetermine Hola. A continuación, se llame a hello `consume` función y pase Hola datos marco toobe predicho.
Hola siguiente código es el modelo de Hola de tooconsume usado publicado como un servicio web de aprendizaje automático de Azure.

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

Puede encontrar más información acerca de la biblioteca de R de aprendizaje de máquina de Azure de hello [aquí](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a>4. Administrar los recursos de Azure mediante el Portal de Azure o PowerShell
Hola DSVM no solo permite toobuild la solución de análisis de forma local en Hola máquina virtual, pero también permite tooaccess servicios en la nube de Microsoft Azure. Azure proporciona varios servicios de proceso, almacenamiento, análisis de datos y de otra índole que puede administrar desde su DSVM y a los que puede tener acceso desde dicho entorno.

tooadminister los recursos de nube y suscripción Azure puede usar el explorador y el punto de toothe [portal de Azure](https://portal.azure.com). También puede usar Azure Powershell tooadminister su suscripción de Azure y sus recursos a través de una secuencia de comandos.
Puede ejecutar Powershell de Azure desde un acceso directo en el escritorio de Hola o de hello iniciar menú titulada "Microsoft Azure Powershell". Para obtener más información sobre cómo administrar su suscripción y los recursos de Azure mediante los scripts de Windows PowerShell, consulte la [documentación de Microsoft Azure PowerShell](../powershell-azure-resource-manager.md) .

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a>5. Ampliar el espacio de almacenamiento con un sistema de archivos compartidos
Pueden compartir los científicos de datos grandes conjuntos de datos, código u otros recursos en el equipo de Hola. Hola DSVM propio tiene unos 70GB de espacio disponible. tooextend su almacenamiento, puede usar Hola servicio de archivos de Azure y montar en hello DSVM o tener acceso a él a través de una API de REST.   

> [!NOTE]
> Hola el espacio máximo del recurso compartido de servicio de archivos de Azure de hello es 5TB y límite de tamaño de archivo individual es 1TB.   
> 
> 

Puede usar Azure Powershell toocreate un recurso compartido de servicio de archivos de Azure. Aquí es toorun de script de Hola en Azure PowerShell toocreate un recurso compartido de servicio de archivos de Azure.

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


Ahora que ha creado un recurso compartido de archivos de Azure, puede montarlo en cualquier máquina virtual de Azure. Se recomienda que Hola VM sea en el mismo centro de datos de Azure como la latencia de tooavoid de cuenta de almacenamiento de Hola y datos gastos de transferencia. Presentamos unidad de hello comandos toomount hello en hello DSVM que se pueden ejecutar en Azure Powershell.

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


Ahora puede tener acceso a esta unidad tal y como lo haría con cualquier unidad normal en hello máquina virtual.

## <a name="6-share-code-with-your-team-using-github"></a>6. Compartir código con su equipo mediante GitHub
GitHub es un repositorio de código donde puede encontrar una gran cantidad de código de ejemplo y orígenes para distintas herramientas con varias tecnologías compartidas por la Comunidad de desarrolladores de Hola. Utiliza Git como Hola versiones de tecnología tootrack y el almacén de archivos de código de hello. GitHub es también una plataforma donde puede crear su propios toostore repositorio código compartido de su equipo y la documentación, implementar el control de versiones y también controlar quién tiene acceso tooview y contribuir en el código. Visite hello [páginas de Ayuda de GitHub](https://help.github.com/) para obtener más información sobre el uso de Git. Puede usar GitHub como uno de hello formas toocollaborate con su equipo, utilice el código desarrollado por la Comunidad de Hola y contribuir código toohello atrás Comunidad.

Hola DSVM ya viene cargado con las herramientas de cliente en la línea de comandos como bien GUI tooaccess repositorio de GitHub. Hola toowork de herramienta de línea de comandos con Git y GitHub se denomina Git Bash. Visual Studio instalada en hello DSVM tiene extensiones de Git de Hola. Puede encontrar iconos de inicio para estas herramientas en el menú de inicio de Hola y de escritorio de Hola.

código de toodownload desde un repositorio de GitHub usar hello ```git clone``` comando. Por ejemplo repositorio de ciencia de datos toodownload publicado por Microsoft en el directorio actual de hello puede ejecutar Hola siguiente comando una vez que esté en ```git-bash```.

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

En Visual Studio, puede hacerlo Hola la misma operación de clonación. Hola siguiente captura de pantalla muestra cómo tooaccess Git y GitHub herramientas en Visual Studio.

![GIT en Visual Studio](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

Puede encontrar más información sobre cómo usar Git toowork con su repositorio de GitHub de varios recursos disponibles en github.com. Hola [hoja de referencia](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) es una referencia útil.

## <a name="7-access-various-azure-data-and-analytics-services"></a>7. Obtener acceso a diversos servicios de análisis y datos de Azure
### <a name="azure-blob"></a>Blob de Azure
Un blob de Azure es un almacenamiento confiable y económico para muchos y pocos datos. Echemos un vistazo a cómo puede mover datos tooAzure Blob y acceder a los datos almacenados en un Blob de Azure.

**Requisito previo**

* **Cree una cuenta de Almacenamiento de blobs de Azure desde el [Portal de Azure](https://portal.azure.com).**

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* Confirmar esa herramienta de línea de comandos preinstalada AzCopy Hola se encuentra en ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```. Puede agregue Hola contenedor hello azcopy.exe tooyour ruta de acceso entorno tooavoid variable escriba Hola comando completo ruta del directorio al ejecutar esta herramienta. Para obtener más información sobre la herramienta AzCopy consulte demasiado[documentación AzCopy](../storage/common/storage-use-azcopy.md)
* Inicie la herramienta Explorador de almacenamiento de Azure de Hola. Se puede descargar en el [Explorador de almacenamiento de Microsoft Azure](http://storageexplorer.com/). 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

**Mover los datos de la máquina virtual tooAzure Blob: AzCopy**

datos de toomove entre los archivos locales y el almacenamiento de blobs, puede utilizar AzCopy en línea de comandos o PowerShell:

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

Reemplace **C:\myfolder** toohello ruta de acceso donde se almacena el archivo, **mystorageaccount** tooyour nombre de cuenta de almacenamiento de blobs, **mycontainer** toohello nombre del contenedor, **clave de la cuenta de almacenamiento** tooyour clave de acceso de almacenamiento de blobs. Las credenciales de su cuenta de almacenamiento puede encontrarlas en el [Portal de Azure](https://portal.azure.com).

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

Ejecute el comando de AzCopy en PowerShell o desde el símbolo del sistema. Aquí puede ver algunos ejemplos del uso de comandos de AzCopy:

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



Una vez que ejecute su tooan de toocopy de comandos de AzCopy blobs de Azure vea que el archivo aparece en el Explorador de almacenamiento de Azure en breve.

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

**Mover los datos de la máquina virtual tooAzure Blob: Explorador de almacenamiento de Azure**

También puede cargar datos de archivo local de hello en la máquina virtual mediante el Explorador de almacenamiento de Azure:

* contenedor de tooupload datos tooa, seleccione Hola Hola de contenedor y haga clic en de destino **cargar** botón.![ Cargar en el Explorador de almacenamiento](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)
* Haga clic en hello **...**  toohello derecha de hello **archivos** , seleccione uno o varios tooupload de archivos de sistema de archivos de Hola y haga clic en **cargar** toobegin cargar archivos de Hola.![ Cargar archivos tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)

**Lectura de datos de Blob de Azure: módulo lector de Machine Learning**

En estudio de aprendizaje automático de Azure puede usar un **módulo importar datos** datos tooread desde el blob.

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

**Lectura de datos de Blob de Azure: ODBC de Python**

Puede usar **BlobService** biblioteca tooread directamente los datos de blob en un programa de Jupyter Notebook o Python.

En primer lugar, importe los paquetes necesarios:

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

A continuación, especifique sus credenciales de la cuenta de Blob de Azure y lea los datos del blob:

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

se leen datos de Hello en como una trama de datos:

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a>Azure Data Lake
Azure Data Lake Store es un repositorio a gran escala para cargas de trabajo de análisis de macrodatos compatible con el sistema de archivos distribuido Hadoop (HDFS), Funciona con el ecosistema de Hadoop de Hola y Hola análisis de Data Lake de Azure. Se muestra cómo puede mover datos a almacén de Azure Data Lake hello y ejecutar análisis mediante el análisis de Data Lake de Azure.

**Requisito previo**

* Cree un análisis de Azure Data Lake Analytics en el [Portal de Azure](https://portal.azure.com).

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* Hola **Azure Data Lake Tools** en **Visual Studio** se encuentra en este [vínculo](https://www.microsoft.com/download/details.aspx?id=49504) ya está instalado en Visual Studio Community Edition que se encuentra en la máquina virtual de Hola Hola. Después de iniciar Visual Studio e iniciar sesión en su suscripción de Azure, debería ver su cuenta de análisis de datos de Azure y almacenamiento en el panel izquierdo de Hola de Visual Studio.

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

**Mover los datos de la máquina virtual tooData Lake: Explorador de Azure Data Lake**

Puede usar **Explorador de Azure Data Lake** datos tooupload de los archivos locales de hello en el almacenamiento de máquina Virtual tooData Lake.

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

También puede compilar un tooproductionize de canalización de datos su tooor de movimiento de datos de Azure Data Lake con hello [Factory(ADF) de datos de Azure](https://azure.microsoft.com/services/data-factory/). Nos referimos toothis [artículo](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide le guían a través de los datos de saludo pasos toobuild Hola canalizaciones.

**Leer datos de Azure Blob tooData Lake: U-SQL**

Si los datos residen en el Almacenamiento de blobs de Azure, puede leer directamente los datos desde el blob de almacenamiento de Azure en una consulta U-SQL. Antes de crear la consulta SQL U, asegúrese de que la cuenta de almacenamiento blob está vinculado tooyour Azure Data Lake. Vaya demasiado**portal de Azure**, busque el panel de análisis de Data Lake de Azure, haga clic en **agregar origen de datos**, seleccione el tipo de almacenamiento demasiado**el almacenamiento de Azure** y conecte el almacenamiento de Azure Nombre de cuenta y la clave. A continuación, está tooreference capaz de hello datos almacenados en la cuenta de almacenamiento de Hola.

![Escribir la clave y la cuenta de almacenamiento](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

En Visual Studio, puede leer datos del almacenamiento de blobs, lleve a cabo algunos manipulación de datos, ingeniería de características y salida Hola resultante datos tooeither Azure Data Lake o almacenamiento de blobs de Azure. Al hacer referencia a datos de hello en almacenamiento de blobs, use **wasb: / /**; al hacer referencia a datos de hello en Azure Data Lake, use **swbhdfs: / /**

![Trama de datos](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

Puede usar hello las siguientes consultas SQL U en Visual Studio:

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



Después de la consulta enviada toohello server, se muestra un diagrama que muestra el estado de saludo de su trabajo.

![Diagrama de estado de trabajo](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

**Consulta de datos en Data Lake: U-SQL**

Después de que el conjunto de datos de hello es ingestión en Azure Data Lake, puede usar [lenguaje SQL U](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery y explorar datos Hola. Lenguaje SQL U es similar tooT-SQL, pero combina algunas características de C# para que los usuarios puedan escribir módulos personalizados, funciones definidas por el usuario y etcetera. Puede utilizar scripts de hello en el paso anterior de Hola.

Una vez consulta hello tooserver enviado, tripdata_summary. CSV puede encontrarse en breve **Explorador de Azure Data Lake**, puede obtener una vista previa de datos de Hola por archivo de hello de menú contextual.

![Archivo en el Explorador de Azure Data Lake](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

información de archivo de Hola toosee:

![Resumen del archivo](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a>Clústeres de Hadoop de HDInsight
HDInsight de Azure es un servicio administrado de Apache Hadoop, Spark, HBase y Storm en nube Hola. Puede trabajar fácilmente con los clústeres de HDInsight de Azure de la máquina virtual de hello datos ciencia.

**Requisito previo**

* Cree una cuenta de Almacenamiento de blobs de Azure desde el [Portal de Azure](https://portal.azure.com). Esta cuenta de almacenamiento es datos de uso toostore para clústeres de HDInsight.

![Creación de una cuenta de Azure Blob Storage](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* Personalice los clústeres de Hadoop de HDInsight de Azure desde el [Portal de Azure](machine-learning-data-science-customize-hadoop-cluster.md)
  
  * Debe vincular la cuenta de almacenamiento de hello creada con el clúster de HDInsight cuando se crea. Esta cuenta de almacenamiento se utiliza para tener acceso a datos que pueden ser procesados en el clúster de Hola.

![Vincular toostorage cuenta creado con clúster de HDInsight](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* Debe habilitar **acceso remoto** toohello del nodo principal del clúster de hello después de crearlo. Recordar las credenciales de acceso remoto de Hola que especifique aquí (que son distintas de las especificadas para el clúster de hello en su creación): vaya necesitando en procedimiento posterior Hola.

![Habilitación del acceso remoto](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* Cree un área de trabajo de Azure Machine Learning. Los experimentos de Machine Learning se almacenarán en este área de trabajo de Machine Learning. Seleccionar opciones de hello resaltado en el Portal de tal y como se muestra en la siguiente captura de pantalla de hello:

![Creación de un área de trabajo de Aprendizaje automático de Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* A continuación, escriba los parámetros de hello para el área de trabajo

![Especificación de parámetros de un área de trabajo de Machine Learning](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* Cargue los datos mediante el cuaderno de IPython. Importar paquetes necesarios en primer lugar, conecte las credenciales, crear una base de datos en la cuenta de almacenamiento y luego los datos tooHDI clústeres de carga.

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


* Como alternativa, puede seguir este [tutorial](machine-learning-data-science-process-hive-walkthrough.md) tooupload clúster tooHDI de Nueva York Taxi datos. Entre los principales pasos se encuentran los siguientes:
  
  * AzCopy: Descargar comprimido CSV desde la carpeta local de blob público tooyour
  * AzCopy: cargar descomprimida CSV de clúster de tooHDI de carpeta local
  * Inicie sesión en el nodo principal de Hola de clúster de Hadoop y preparar para el análisis de exploración de datos

Una vez datos Hola clúster tooHDI cargado, puede comprobar los datos en el Explorador de almacenamiento de Azure. Y tendrá un archivo nyctaxidb de base de datos creado en el clúster HDI.

**Exploración de datos: consultas de Hive en Python**

Puesto que los datos de hello en clúster de Hadoop, puede usar hello pyodbc paquete tooconnect tooHadoop clústeres y consultar mediante Hive toodo exploración y la ingeniería de la característica de base de datos. Puede ver las tablas existentes Hola que se creó en el paso de requisitos previos de Hola.

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![Consulta de las tablas existentes](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

Echemos un vistazo a número de Hola de registros de cada mes y hello las frecuencias de superpuesto o no en la tabla de ida y vuelta de hello:

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

Podemos también distancia Hola entre seleccionar una ubicación y la ubicación de caída de proceso y, a continuación, compárela toohello distancia de viaje.

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

Ahora vamos a preparar una muestra reducida (1%) de un conjunto de datos para el modelado. Podemos usar estos datos en el módulo lector de Machine Learning.

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

Después de un tiempo, puede ver datos de Hola se han cargado en clústeres de Hadoop:

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Tabla de datos](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

**Lectura de datos de HDI mediante Machine Learning: módulo lector**

También puede usar hello **lector** módulo en la base de datos de estudio de aprendizaje automático tooaccess hello en clúster de Hadoop. Conecte credenciales de Hola de los clústeres HDI y tooenable de la cuenta de almacenamiento de Azure Cree modelos con la base de datos en clústeres HDI de aprendizaje de máquina de realizando una operación.

![Propiedades del módulo lector](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

Hello conjunto de datos con puntuación puede verse a continuación:

![Visualización del conjunto de datos con puntuación](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a>Almacenamiento de datos SQL de Azure y bases de datos
Almacenamiento de datos SQL Azure es un almacén de datos elástico que funciona como un servicio con experiencia SQL Server empresarial.

Puede aprovisionar el almacenamiento de datos de SQL Azure siguiendo las instrucciones de hello proporcionadas en este [artículo](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md). Una vez que aprovisione el almacenamiento de datos de SQL Azure, puede usar este [tutorial](machine-learning-data-science-process-sqldw-walkthrough.md) al cargar los datos de toodo, exploración y modelado utilizando los datos dentro de hello almacenamiento de datos SQL.

#### <a name="azure-cosmos-db"></a>Azure Cosmos DB
Base de datos de Cosmos Azure es una base de datos NoSQL en nube Hola. Le permite toowork con documentos como JSON y permite documentos hello toostore y la consulta.

Necesita hello toodo siguientes por requisitos pasos tooaccess base de datos de Azure Cosmos de hello DSVM.

1. Instale el SDK de Python de DocumentDB (ejecute ```pip install pydocumentdb``` desde el símbolo del sistema).
2. Cree una base de datos y una cuenta de Azure Cosmos DB en [Azure Portal](https://portal.azure.com).
3. Descargar "Herramienta de migración de base de datos de Azure Cosmos" de [aquí](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) y extraer tooa directorio de su elección
4. Importar datos JSON (datos volcano) almacenados en un [blob público](https://cahandson.blob.core.windows.net/samples/volcano.json) en DB Cosmos con siguiente herramienta de migración toohello de comando parámetros (dtui.exe del directorio de Hola donde instaló la herramienta de migración de base de datos de Cosmos hello). Escriba la ubicación de origen y de destino de hello con estos parámetros:
   
    /s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1

Una vez que se importan datos de hello, puede ir tooJupyter y Bloc de notas abierto Hola titulada *DocumentDBSample* que contiene python tooaccess documentos de código y realice algunas consultas básicas. Se puede obtener más información acerca de la base de datos de Cosmos visitando servicio hello [página de documentación de](https://docs.microsoft.com/azure/cosmos-db/).

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a>8. Generar informes y panel con hello Power BI Desktop
Permítanos visualizar archivo JSON Volcano hello que hemos visto en hello anterior ejemplo de base de datos de Cosmos en Power BI toogain visuales visiones Hola datos. Los pasos detallados están disponibles en hello [artículo Power BI](../cosmos-db/powerbi-visualize.md). Estos son los pasos de alto nivel de hello:

1. Abra Power BI Desktop y presione "Obtenga datos". Especifique la dirección URL de hello como: https://cahandson.blob.core.windows.net/samples/volcano.json
2. Debería ver registros JSON de hello importados como una lista
3. Convertir la tabla de tooa de lista de Hola para Power BI pueda trabajar con hello igual
4. Expanda columnas Hola haciendo clic en hello expandirán icono (Hola uno con icono de "flecha izquierda y una flecha derecha" hello en hello derecha de la columna de hello)
5. Observe que la ubicación es un campo de "Registro". Expandir registro de hello y seleccione sólo Hola coordenadas. Las coordenadas es una columna de la lista.
6. Agregar una nueva columna tooconvert Hola lista coordenadas de columnas en una columna de LatLong independiente de coma concatenar Hola dos elementos de hello coordenadas lista campo usando la fórmula de hello ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.
7. Por último, convertir hello ```Elevation``` tooDecimal de columna y seleccione hello **cerrar** y **aplicar**.

En lugar de pasos anteriores, puede pegar Hola siguiente código de scripts de pasos de Hola que se usan en Hola Editor avanzado en Power BI que permite transformaciones de datos de hello toowrite en un lenguaje de consulta.

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



Ahora tiene datos de hello en el modelo de datos de Power BI. Power BI Desktop debe aparecer como sigue:

![Power BI Desktop](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

Ya puede empezar a crear informes y visualizaciones con el modelo de datos de Hola. Puede seguir los pasos de hello en este [artículo Power BI](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild un informe. resultado de Hello final es un informe similar Hola siguiente.

![Vista de informes de Power BI Desktop: conector de Power BI](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a>9. Escalar dinámicamente su toomeet DSVM que su proyecto necesite
Puede escalar arriba y abajo hello DSVM toomeet que su proyecto necesite. Si no necesita toouse Hola VM de jornada laboral de Hola o los fines de semana, puede apagar simplemente Hola VM de hello [portal de Azure](https://portal.azure.com).

> [!NOTE]
> Acumulando cargos de proceso si utiliza simplemente el botón de apagado del sistema operativo de hello en hello máquina virtual.  
> 
> 

Si necesita toohandle un análisis a gran escala y necesita más capacidad de CPU, memoria o disco encontrará gran varios tamaños VM en términos de núcleos de CPU, capacidad de memoria y los tipos de disco (incluidas las unidades de estado sólido) que satisfacen las necesidades presupuestarias y proceso. Hello lista completa de las máquinas virtuales junto con sus precios por hora de cálculo está disponible en hello [precios de máquinas virtuales de Azure](https://azure.microsoft.com/pricing/details/virtual-machines/) página.

De forma similar, si reduce la necesidad de capacidad de procesamiento de la máquina virtual (por ejemplo: mover un tooa de carga de trabajo principales Hadoop o en un clúster de Spark), puede reducir clúster Hola de hello [portal de Azure](https://portal.azure.com) y va toohello configuración de la máquina virtual instancia. Aquí puede ver una captura de pantalla.

![Configuración de la instancia de VM](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a>10. Instalar herramientas adicionales en la máquina virtual
Nos hemos empaquetar varias herramientas que creemos son tooaddress capaz de muchas de las necesidades de análisis de datos comunes de Hola y que deben ahorrarle tiempo al evitar tener tooinstall y configurar los entornos de uno a uno y ahorrar dinero por pagar solo por recursos que Use.

Puedes sacar provecho de otros datos de Azure y generar perfiles de servicios de análisis en este artículo tooenhance su entorno de análisis. Somos conscientes de que en algunos casos sus necesidades pueden requerir herramientas adicionales, incluidas algunas herramientas propiedad de terceros. Tener acceso administrativo completo en hello máquina virtual tooinstall nuevas herramientas que necesita. También puede instalar paquetes adicionales de Python y R que no estén instalados previamente. En el caso de Python, puede utilizar ```conda``` o ```pip```. Para R puede usar hello ```install.packages()``` en hello R la consola o usar hello IDE y elija "**paquetes** -> **paquetes de instalación...** ".

## <a name="summary"></a>Resumen
Éstas son sólo algunas de las acciones de Hola que puede realizar en hello Microsoft Data Science Virtual Machine. Hay muchas más cosas que puede hacer toomake un entorno de análisis efectivo.

