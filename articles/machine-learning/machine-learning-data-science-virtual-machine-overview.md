---
title: "¿aaaWhat es una máquina Virtual de ciencia de datos? | Microsoft Docs"
description: "¿Cómo tooget comenzaron a establecer escenarios clave de análisis con datos ciencia las máquinas virtuales."
keywords: "herramientas de ciencia de datos, máquina virtual de ciencia de datos, herramientas para la ciencia de datos, ciencia de datos de linux"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d4f91270-dbd2-4290-ab2b-b7bfad0b2703
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;bradsev
ms.openlocfilehash: 18c7a75208671c663f3b6be6ee8d0bf666772e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-cloud-based-data-science-virtual-machine-for-linux-and-windows"></a>Introducción toohello basada en la nube Data Science Virtual Machine para Linux y Windows
Hola Máquina Virtual de ciencia de datos (DSVM) es una imagen de máquina virtual personalizada en la nube de Microsoft Azure creada específicamente para realizar la ciencia de datos. Tiene muchas ciencia de datos muy popular y otras herramientas preinstalada y preconfigurada toojump-comience a crear aplicaciones inteligentes para análisis avanzado. Está disponible en Windows Server y en Linux. La edición de Windows de la DSVM se ofrece en Server 2016 y Server 2012. Ofrecemos edición de Linux de hello DSVM en Ubuntu 16.04 LTS y en las distribuciones de Linux-based OpenLogic 7.2 CentOS. 

En este tema se describe lo que puede hacer con hello VM de ciencia de datos, se describe algunos de los escenarios clave de hello para el uso de hello VM, detalla las características clave de hello disponibles en Windows hello y versiones de Linux y proporciona instrucciones sobre cómo tooget a utilizarlos.

## <a name="what-can-i-do-with-hello-data-science-virtual-machine"></a>¿Qué puedo hacer con hello Data Science Virtual Machine?
objetivo de Hola de hello Data Science Virtual Machine es tooprovide profesionales de datos en todos los roles con un entorno de ciencia de datos sin fricción y niveles de especialización. Esta VM le ahorra el tiempo que pasaría si implantara un entorno comparable usted mismo. En su lugar, inicie el proyecto de ciencia de datos inmediatamente en una instancia de VM recién creada. 

Hola VM de ciencia de datos está diseñado y está configurado para trabajar con los escenarios de uso generales. Puede escalar verticalmente o reducir verticalmente el entorno a medida que cambian las necesidades del proyecto. Se está toouse capaz de sus tareas de ciencia de datos de tooprogram idioma preferido. Puede instalar otras herramientas y personalizar el sistema de Hola para sus necesidades específicas.

## <a name="key-scenarios"></a>Escenarios principales
En esta sección se sugiere algunos escenarios clave para qué Hola se puede implementar la máquina virtual de ciencia de datos.

### <a name="preconfigured-analytics-desktop-in-hello-cloud"></a>Preconfigurado escritorio de análisis en la nube de Hola
Hola VM de ciencia de datos proporciona una configuración de línea de base para que los equipos de ciencia de datos buscando tooreplace sus escritorios locales con un equipo de escritorio administrado en la nube. Esta línea base garantiza que todos los científicos de datos de hello en un equipo tienen una configuración coherente con los experimentos tooverify y fomentar la colaboración. También disminuye los costos al reducir la carga del administrador del sistema de Hola y guardar en tiempo de hello necesarios tooevaluate, instalar y mantener Hola distintos paquetes de software necesarias toodo análisis avanzados.  

### <a name="data-science-training-and-education"></a>Educación y formación de ciencia de datos
Instructores Enterprise y educadores que impartir las clases de ciencia de datos normalmente ofrecen una tooensure de imagen de máquina virtual que sus alumnos tienen una configuración coherente y que los ejemplos de hello funcionan predecible. Hola VM de ciencia de datos, crea un entorno de petición con una configuración coherente que simplifica los desafíos de incompatibilidad y soporte técnico de Hola. Casos en que estos entornos tenga toobe se compilan con frecuencia, especialmente para las clases de aprendizaje más cortas, se benefician sustancialmente.

### <a name="on-demand-elastic-capacity-for-large-scale-projects"></a>Capacidad elástica a petición para proyectos de gran escala
La exploración y el modelado de datos a gran escala o las competencias/hackathons de ciencia de datos requieren un escalado horizontal de la capacidad de hardware, normalmente durante poco tiempo. Hola VM de ciencia de datos puede ayudar a replicar Hola datos ciencia entorno rápidamente informe a petición, en los servidores escalados horizontalmente que permiten que requieren gran potencia toobe recursos informáticos de experimentos ejecute.

### <a name="short-term-experimentation-and-evaluation"></a>Evaluación y experimentación a corto plazo
Hello VM de ciencia de datos pueden tooevaluate usado o aprender herramientas como Microsoft R Server, SQL Server, herramientas de Visual Studio, Jupyter, profundidad de aprendizaje / kits de herramientas de aprendizaje automático y nuevas herramientas populares en Hola Comunidad con un esfuerzo mínimo de instalación. Puesto que Hola VM de ciencia de datos puede configurarse rápidamente, se puede aplicar en otros escenarios de uso a corto plazo como la replicación de experimentos publicados, demostraciones, tutoriales siguientes en las sesiones en línea o los tutoriales de conferencia de ejecución.

### <a name="deep-learning"></a>Aprendizaje profundo
ciencia de datos de Hello VM puede usarse para el modelo de aprendizaje mediante algoritmos de aprendizaje profundo en GPU (unidades de procesamiento de gráficos) basado en hardware. Gracias a la VM escalado capacidades de nube de Azure, DSVM le permitirá usar hardware de GPU basado en la nube de hello según la necesidad. Puede cambiar uno tooa GPU en VM al entrenar modelos grandes o necesitan cálculos de alta velocidad al mantener Hola mismo disco del sistema operativo.  edición de Windows Server 2016 Hola de DSVM viene preinstalado con controladores de GPU, marcos de trabajo y la versión GPU de hello profundo algoritmos de aprendizaje. En Hola Linux profunda de aprendizaje en GPU sólo está habilitada en hello [Data Science Virtual Machine para Linux (Ubuntu) edition](http://aka.ms/dsvm/ubuntu). Puede implementar las ediciones de Ubuntu/Windows-2016 Hola de VM de ciencia de datos toonon GPU según máquina virtual de Azure en cuyo caso todos los marcos de trabajo de aprendizaje profundo de hello le modo de reserva toohello CPU. Anteriormente, para Windows Server 2012 publicamos un [kit de herramientas de aprendizaje profundo](http://aka.ms/dsvm/deeplearning), pero ahora recomendamos usar Windows Server 2016 para las cargas de trabajo de aprendizaje profundo basadas en Windows. edición de Linux-based CentOS Hola de hello DSVM contiene solo Hola CPU compilaciones de algunas Hola profundo de aprendizaje de herramientas (CNTK, Tensorflow MXNet) pero no vienen preinstaladas con marcos de trabajo y controladores GPU de Hola. 

## <a name="whats-included-in-hello-data-science-vm"></a>¿Qué se incluye en hello VM de ciencia de datos?
Hola Data Science Virtual Machine tiene muchos ciencia de datos muy popular y profunda herramientas ya instalado y configurado de aprendizaje. También incluye herramientas que hacen que sea fácil toowork con diversos productos de datos y análisis de Azure. Le permite explorar y generar modelos predictivos en conjuntos de datos a gran escala utilizando Hola Microsoft R Server o SQL Server 2016. Un host de otras herramientas de la Comunidad de código abierto de Hola y de Microsoft también son blocs de notas e incluye, así como ejemplo de código. Hello tabla siguiente detalla y compara los componentes principales de hello incluidos en Windows hello y ediciones de Linux de hello Data Science Virtual Machine.


| **Herramienta**                                                           | **Edición de Windows** | **Edición de Linux** |
| :------------------------------------------------------------------ |:-------------------:|:------------------:|
| [Microsoft R Open](https://mran.microsoft.com/open/) con paquetes populares preinstalados   |Y                      | Y             |
| [Microsoft R Server](https://msdn.microsoft.com/microsoft-r/) Developer Edition incluye: <br />  &nbsp;&nbsp;&nbsp;&nbsp;*   [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started) Marco de trabajo de R paralelo y distribuido de alto rendimiento<br />  &nbsp;&nbsp;&nbsp;&nbsp;*   [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction) Nuevos algoritmos de aprendizaje automático de última generación de Microsoft <br />  &nbsp;&nbsp;&nbsp;&nbsp;*   [Operacionalización de R](https://msdn.microsoft.com/microsoft-r/operationalize/about)                                            |Y                      | Y <br/> (MicrosoftML aún no disponible)|
| [Microsoft Office](https://products.office.com/en-us/business/office-365-proplus-business-software) Pro Plus con activación compartida: Excel, Word y PowerPoint   |Y                      |N              |
| [Anaconda Python](https://www.continuum.io/) 2.7, 3.5 con paquetes populares preinstalados    |Y                      |Y              |
| [JuliaPro](https://juliacomputing.com/products/juliapro.html) con paquetes populares para lenguaje Julia preinstalados                         |Y                      |Y              |
| Bases de datos relacionales                                                            | [SQL Server 2016 SP1](https://www.microsoft.com/sql-server/sql-server-2016) <br/> Developer Edition| [PostgreSQL](https://www.postgresql.org/) |
| Herramientas de base de datos                                                       | * SQL Server Management Studio <br/>* SQL Server Integration Services<br/>* [bcp, sqlcmd](https://docs.microsoft.com/sql/tools/command-prompt-utility-reference-database-engine)<br /> * Controladores ODBC/JDBC| * [SQuirreL SQL](http://squirrel-sql.sourceforge.net/) (herramienta de consulta), <br /> * bcp, sqlcmd <br /> * Controladores ODBC/JDBC|
| Análisis de base de datos escalable con servicios de R de SQL Server | Y     |N              |
| **[Jupyter Notebook Server](http://jupyter.org/) con los kernel siguientes,**                                  | Y     | Y |
|     &nbsp;&nbsp;&nbsp;&nbsp;* R | Y | Y |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Python 2.7 y 3.5 | Y | Y |
|     &nbsp;&nbsp;&nbsp;&nbsp;* Julia | Y | Y |
|     &nbsp;&nbsp;&nbsp;&nbsp;* PySpark | N | Y |
|     &nbsp;&nbsp;&nbsp;&nbsp;*   [Sparkmagic](https://github.com/jupyter-incubator/sparkmagic) | N | Y (solo Ubuntu) |
|     &nbsp;&nbsp;&nbsp;&nbsp;* SparkR     | N | Y |
| JupyterHub (servidor de cuadernos de varios usuarios)| N | Y |
| **Herramientas de desarrollo, entornos de desarrollo integrados y editores de código**| | |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Visual Studio 2017 (Community Edition)](https://www.visualstudio.com/community/) &gt; con Git Plugin, Azure HDInsight (Hadoop), Data Lake, SQL Server Data Tools, [Node.js](https://github.com/Microsoft/nodejstools), [Python](http://aka.ms/ptvs) y [Herramientas de R para Visual Studio (RTVS)](http://microsoft.github.io/RTVS-docs/) | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Visual Studio Code](https://code.visualstudio.com/) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [RStudio Desktop](https://www.rstudio.com/products/rstudio/#Desktop) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [RStudio Server](https://www.rstudio.com/products/rstudio/#Server) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [PyCharm](https://www.jetbrains.com/pycharm/) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Atom](https://atom.io/) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Juno (Julia IDE)](http://junolab.org/)| Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* Vim y Emacs | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* Git y GitBash | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* OpenJDK | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* .NET Framework | Y | N |
| PowerBI Desktop | Y | N |
| Tooaccess de SDK de Azure y conjunto de inteligencia de Cortana de servicios | Y | Y |
| **Herramientas de movimiento de datos y administración** | | |
| &nbsp;&nbsp;&nbsp;&nbsp;* Explorador de Azure Storage | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [CLI de Azure](https://docs.microsoft.com/cli/azure/overview) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* Azure Powershell | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Azcopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy) | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Adlcopy (Almacén de Azure Data Lake)](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob) | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Herramienta DocDB Data Migration](https://docs.microsoft.com/azure/documentdb/documentdb-import-data) | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Microsoft Data Management Gateway](https://msdn.microsoft.com/library/dn879362.aspx): traslado de datos entre local y la nube | Y | N |
| &nbsp;&nbsp;&nbsp;&nbsp;* Utilidades de línea de comandos Unix/Linux | Y | Y |
| [Apache Drill](http://drill.apache.org) para la exploración de datos | Y | Y |
| **Herramientas de aprendizaje automático** |||
| &nbsp;&nbsp;&nbsp;&nbsp;* Integración con [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) (R, Python) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Xgboost](https://github.com/dmlc/xgboost) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Weka](http://www.cs.waikato.ac.nz/ml/weka/) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Rattle](http://rattle.togaware.com/) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [LightGBM](https://github.com/Microsoft/LightGBM) | N | Y (solo Ubuntu) |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [H2O](https://www.h2o.ai/h2o/) | N | Y (solo Ubuntu) |
| **Herramientas de aprendizaje profundo basado en GPU** |Edición de Windows Server 2016  |Edición de Ubuntu |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Microsoft Cognitive Toolkit (CNTK)](http://cntk.ai) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Tensorflow](https://www.tensorflow.org/) | Y | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [MXNet](http://mxnet.io/) | Y | Y|
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Caffe y Caffe2](https://github.com/caffe2/caffe2) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Torch](http://torch.ch/) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Theano](https://github.com/Theano/Theano) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [Keras](https://keras.io/)| N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [NVidia Digits](https://github.com/NVIDIA/DIGITS) | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;*   [CUDA, CUDNN, Nvidia Driver](https://developer.nvidia.com/cuda-toolkit) | Y | Y |
| **Plataforma de macrodatos (solo Devtest)**|||
| &nbsp;&nbsp;&nbsp;&nbsp;* [Spark](http://spark.apache.org/) Standalone local | N | Y |
| &nbsp;&nbsp;&nbsp;&nbsp;* [Hadoop](http://hadoop.apache.org/) (HDFS, YARN) local | N | Y |



## <a name="how-tooget-started-with-hello-windows-data-science-vm"></a>¿Cómo tooget partió Hola VM de ciencia de datos de Windows
* Cree una instancia de la edición de Windows DSVM Hola deseado, vaya a
  * [DSVM basada en Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft-ads.windows-data-science-vm)
  
  o 
  * [DSVM basada en Windows Server 2012](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) 
* Haga clic en hello **obtener TI ahora** botón.
* Inicie sesión en toohello VM desde el escritorio remoto con credenciales de Hola que especificó cuando creó Hola máquina virtual.
* toodiscover e iniciar herramientas de hello disponibles, haga clic en hello **iniciar** menú.

## <a name="get-started-with-hello-linux-data-science-vm"></a>Empezar a trabajar con hello VM de ciencia de datos de Linux
* Cree una instancia de hello deseado edición Linux DSVM desplazándose demasiado
  * [DSVM basada en Ubuntu](http://aka.ms/dsvm/ubuntu)

  o

  * [DSVM basada en OpenLogic CentOS](http://aka.ms/dsvm/centos)

  
* Haga clic en hello **obtenerlo ahora** botón.
* Inicie sesión en toohello VM desde un cliente SSH como Putty o comando SSH, con credenciales de Hola que especificó cuando creó Hola máquina virtual.
* En el símbolo del shell de hello, escriba información de más de dsvm.
* Para un escritorio gráfico, descargue el cliente hello X2Go para su plataforma de cliente [aquí](http://wiki.x2go.org/doku.php/doc:installation:x2goclient) y siga las instrucciones de hello en el documento de la máquina virtual de ciencia de datos de Linux de hello [Hola aprovisionar Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client).

## <a name="next-steps"></a>Pasos siguientes
### <a name="for-hello-windows-data-science-vm"></a>Para hello VM de ciencia de datos de Windows
* Para obtener más información sobre cómo las herramientas disponible en la versión de Windows hello toorun específico, consulte [Hola aprovisionar Microsoft Data Science Virtual Machine](machine-learning-data-science-provision-vm.md) y
* Para obtener más información sobre cómo tooperform diversas tareas necesarias para el proyecto de ciencia de datos en hello VM de Windows, vea [diez cosas que puede hacer en hello ciencia de datos Virtual Machine](machine-learning-data-science-vm-do-ten-things.md).

### <a name="for-hello-linux-data-science-vm"></a>Para hello VM de ciencia de datos de Linux
* Para obtener más información sobre cómo las herramientas disponible en la versión de Linux de hello toorun específico, consulte [Hola aprovisionar Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-intro.md).
* Para ver un tutorial que muestra cómo tooperform ciencia de datos común varias tareas con hello VM de Linux, consulte [ciencia de datos en hello Linux Data Science Virtual Machine](machine-learning-data-science-linux-dsvm-walkthrough.md).

