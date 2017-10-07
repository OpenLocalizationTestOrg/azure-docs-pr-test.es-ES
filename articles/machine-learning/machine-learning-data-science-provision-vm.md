---
title: Hola aaaProvision Microsoft Data Science Virtual Machine | Documentos de Microsoft
description: "Configure y cree una instancia de Data Science Virtual Machine en Azure para realizar análisis y aprendizaje automático."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e1467c0f-497b-48f7-96a0-7f806a7bec0b
ms.service: machine-learning
ms.workload: data-services
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 907a3bdc7e480d05e8e245f5e50d632900fcf471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-microsoft-data-science-virtual-machine"></a>Aprovisionar Hola Microsoft Data Science Virtual Machine
Hola Microsoft Data Science Virtual Machine es una imagen de máquina virtual (VM) de Windows Azure previamente instalado y configurado con varias herramientas conocidas que se usan habitualmente para análisis de datos y el aprendizaje automático. herramientas de Hello incluidas son:

* Microsoft R Server Developer Edition
* Anaconda Python Distribution
* Notebook de Jupyter (con kernels R, Python)
* Visual Studio Community Edition
* Power BI Desktop
* SQL Server 2016 Developer Edition
* Herramientas de aprendizaje automático y análisis
  * [Computational Network Toolkit (CNTK)](https://github.com/Microsoft/CNTK): kit de herramientas de software de aprendizaje profundo de Microsoft Research
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): sistema de aprendizaje automático rápido que admite varias técnicas, como el aprendizaje en línea, el uso de hash, la clase AllReduce, las reducciones, learning2search y los aprendizajes activo e interactivo
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): herramienta que proporciona una implementación de árbol ampliada, rápida y precisa
  * [Cascabel](http://rattle.togaware.com/) (Hola herramienta analíticos R tooLearn fácilmente): una herramienta que facilita la introducción a la máquina de aprendizaje en R fácil, con la exploración de datos basados en GUI y modelado de generación automática de código de R y análisis de datos.
  * [mxnet](https://github.com/dmlc/mxnet): un entorno de aprendizaje en profundidad diseñado para lograr eficiencia y flexibilidad
  * [Weka](http://www.cs.waikato.ac.nz/ml/weka/): software de minería de datos visual y aprendizaje automático de Java.
  * [Apache Drill](https://drill.apache.org/): motor de consultas SQL sin esquemas para Hadoop, NoSQL y almacenamiento en la nube.  Es compatible con ODBC y JDBC tooenable interfaces consultar NoSQL y archivos de herramientas estándar de BI como Power BI, Excel, una plantilla.
* Bibliotecas en R y Python para usarlas en Aprendizaje automático de Azure y en otros servicios de Azure
* GIT incluidos Git Bash toowork con repositorios de código de origen incluidos GitHub, Visual Studio Team Services
* Puertos de Windows de varias utilidades de línea de comandos de Linux populares (en otras, awk, sed, perl, grep, buscar, wget, curl, etc.) accesibles mediante el símbolo del sistema. 

La ciencia de datos implica la iteración de una secuencia de tareas:

1. Buscar, cargar y preprocesar datos
2. Compilar y probar modelos
3. Implementar modelos de Hola para su uso en aplicaciones inteligentes

Los científicos de datos utilice una variedad de herramientas toocomplete estas tareas. Puede ser bastante lento toofind hello las versiones del software de hello y, a continuación, descargarlas e instalarlas. Hola Microsoft Data Science Virtual Machine puede facilitar esta carga proporcionando una imagen listos para usar que se puede aprovisionar en Azure con varias herramientas populares todos previamente instalado y configurado. 

Hola Microsoft Data Science Virtual Machine impulsa el proyecto de análisis. Le permite toowork de tareas en varios idiomas, incluidos R, Python, SQL y C#. Visual Studio proporciona un IDE toodevelop y probar el código que sea fácil toouse. Hola incluido en hello VM de Azure SDK permite toobuild sus aplicaciones mediante diversos servicios en la plataforma de nube de Microsoft. 

No hay ningún cargo de software para esta imagen de VM de ciencia de datos. Solo paga por las cuotas de uso de Azure de Hola depende de qué tamaño Hola de máquina virtual de hello que aprovisionar. Obtener más detalles sobre Hola proceso cuotas pueden encontrarse en la sección de detalles de precios en Hola Hola [Data Science Virtual Machine](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) página. 

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>Otras versiones de hello Data Science Virtual Machine
A [CentOS](machine-learning-data-science-linux-dsvm-intro.md) también está disponible la imagen, con muchas de hello mismo herramientas como Hola imagen de Windows. También hay una imagen de [Ubuntu](machine-learning-data-science-dsvm-ubuntu-intro.md) disponible, con muchas herramientas similares más marcos de trabajo de aprendizaje profundo.

## <a name="prerequisites"></a>Requisitos previos
Para poder crear un Microsoft Data Science Virtual Machine, debe tener el siguiente hello:

* **Una suscripción de Azure**: tooobtain un, consulte [evaluación gratuita de Azure obtener](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Una cuenta de almacenamiento de Azure**: toocreate un, consulte [crear una cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account). También se puede crear cuenta de almacenamiento de hello como parte del proceso de Hola de creación de hello VM si no desea toouse una cuenta existente.

## <a name="create-your-microsoft-data-science-virtual-machine"></a>Creación de su Microsoft Data Science Virtual Machine
Una instancia de Microsoft Data Science Virtual Machine Hola le presentamos Hola pasos toocreate:

1. Navegar por la máquina virtual de toohello enumerar en [portal de Azure](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).
2. Seleccione hello **crear** situado en hello inferior toobe realizada en un asistente.![ configurar datos-ciencia-vm](./media/machine-learning-data-science-provision-vm/configure-data-science-virtual-machine.png)
3. Hola asistente que se utiliza toocreate Hola requiere Microsoft Data Science Virtual Machine **entradas** para cada uno de hello **cinco pasos** enumerado en hello derecha de esta ilustración. A continuación, incluimos Hola entradas necesitados tooconfigure cada de estos pasos:
   
   1. **Aspectos básicos**
      
      1. **Nombre**: nombre del servidor de ciencia de datos que está creando.
      2. **Nombre de usuario**: identificador de inicio de sesión de la cuenta del administrador.
      3. **Contraseña**: contraseña de la cuenta del administrador.
      4. **Suscripción**: si tiene más de una suscripción, seleccione Hola uno en qué Hola máquina es toobe creado y factura.
      5. **Grupo de recursos**: puede crear uno nuevo o usar un grupo que ya exista.
      6. **Ubicación**: Centro de datos seleccione hello más adecuada. Normalmente es el centro de datos de Hola que tenga la mayoría de los datos o que esté más cercano ubicación física tooyour más rápido acceso a la red.
   2. **Tamaño**: seleccione uno de los tipos de servidor hello que cumpla los requisitos funcionales y límites de costos. Para obtener más opciones de tamaños de máquina virtual, seleccione "Ver todo".
   3. **Configuración**:
      
      1. **Tipo de disco**: elija Premium si prefiere una unidad de estado sólido (SSD), de lo contrario elija "Estándar".
      2. **Cuenta de almacenamiento**: puede crear una nueva cuenta de almacenamiento de Azure en su suscripción o utilizar uno existente en hello mismo *ubicación* que se ha elegido en hello **Fundamentos** paso del Asistente para saludo.
      3. **Otros parámetros**: normalmente que usar valores predeterminados de Hola. Puede mantener el mouse sobre un vínculo informativo Hola para obtener ayuda acerca de campos específicos de hello en caso de que desea usar de hello tooconsider de valores no predeterminados.
   4. **Resumen**: Compruebe que toda la información que ha especificado es correcta.
   5. **Comprar**: haga clic en **comprar** toostart Hola aprovisionamiento. Se proporciona un vínculo términos de toohello de transacción de Hola. Hola VM no tiene todos los cargos adicionales más allá del proceso de hello para el tamaño del servidor hello que eligió en hello **tamaño** paso. 

> [!NOTE]
> Aprovisionamiento de Hello tardará aproximadamente 10-20 minutos. estado de Hola de aprovisionamiento de Hola se muestra en hello portal de Azure.
> 
> 

## <a name="how-tooaccess-hello-microsoft-data-science-virtual-machine"></a>¿Cómo tooaccess Hola Microsoft Data Science Virtual Machine
Una vez Hola se crea la VM, puede escritorio remoto en él usando credenciales de cuenta de administrador de Hola que configuró en hello anterior **Fundamentos** sección. 

Una vez que la máquina virtual se crea y suministra, está listo toostart mediante herramientas de Hola que están instalados y configurados en él. Hay iconos del menú Inicio y los iconos del escritorio para muchas de las herramientas de Hola. 

## <a name="how-toocreate-a-strong-password-for-jupyter-and-start-hello-notebook-server"></a>¿Cómo toocreate una contraseña segura para Jupyter y empezar a Hola servidor Bloc de notas
De forma predeterminada, el servidor de hello Jupyter notebook es configurado previamente pero deshabilitado en hello VM hasta que se establezca una contraseña Jupyter. llama a toocreate una contraseña segura para el servidor de Jupyter notebook Hola instalado en el equipo de hello, Hola ejecución siguiente comando en un símbolo de hello Máquina Virtual de ciencia de datos o haga doble clic en el acceso directo de escritorio de hello hemos proporcionado  **Establecer contraseña de Jupyter & Inicio** desde una cuenta de administrador de máquina virtual local.

    C:\dsvm\tools\setup\JupyterSetPasswordAndStart.cmd

Siga los mensajes de saludo y elija una contraseña segura cuando se le solicite.

Hello script anterior crea un hash de contraseña y las almacena en el archivo de configuración de hello Jupyter ubicado en: **C:\ProgramData\jupyter\jupyter_notebook_config.py** en nombre de parámetro hello ***c. NotebookApp.password***.

script de Hola también habilita y ejecuta servidor de Jupyter de hello en segundo plano de Hola. Servidor de Jupyter se crea como una tarea de windows en el programador de tareas de WIndows hello invoca **Start_IPython_Notebook**.  Puede que tenga toowait durante unos segundos después de establecer la contraseña de hello antes de abrir Bloc de notas de hello en el explorador. Vea a continuación Hola sección titulada **Jupyter Notebook** en cómo tooaccess Hola servidor de Jupyter notebook. 


## <a name="tools-installed-on-hello-microsoft-data-science-virtual-machine"></a>Herramientas instaladas en hello Microsoft Data Science Virtual Machine

### <a name="microsoft-r-server-developer-edition"></a>Microsoft R Server Developer Edition
Si desea toouse R para los análisis, Hola VM tiene edición para desarrolladores de Microsoft R Server instalado. Microsoft R Server es una plataforma de análisis de nivel empresarial que se puede implementar ampliamente gracias a que R es compatible, escalable y seguro. La compatibilidad con una variedad de estadísticas de grandes cantidades de datos, modelado de predicción y capacidades de aprendizaje automático, R Server Hola compatibilidad plena con multitud de análisis: exploración, análisis, visualización y modelado. Al usar y extender R de código abierto, Microsoft R Server es totalmente compatible con scripts de R, las funciones y los paquetes CRAN, tooanalyze datos a escala empresarial. También se analizan las limitaciones en memoria de Hola de R de código fuente abierto agregando paralelo y fragmentado de procesamiento de datos. Esto le permite analizar los toorun datos muy por encima de lo que cabe en la memoria principal.  Visual Studio Community Edition incluye en hello que VM contiene herramientas de R de hello para la extensión de Visual Studio que proporciona un IDE completo para trabajar con R. También puede descargar y usar, así como otros IDE [RStudio](http://www.rstudio.com). 

### <a name="python"></a>Python
Para el desarrollo con Python, se ha instalado Anaconda Python Distribution 2.7 y 3.5. Esta distribución contiene Hola base Python junto con unos 300 de hello paquetes más populares matemáticas, ingeniería y datos de análisis. Puede usar Python Tools para Visual Studio (PTVS) que se instala en la edición de Visual Studio 2015 Community de Hola o uno de hello que IDE incluirse con Anaconda como inactivo o Spyder. Puede iniciar uno de estos métodos, debe buscar en la barra de búsqueda de hello (**Win** + **S** clave).

> [!NOTE]
> Hola toopoint Python Tools para Visual Studio en Anaconda Python 2.7 y 3.5, deberá toocreate personalizado entornos para cada versión. tooset estas rutas de acceso de entorno de Visual Studio 2015 Community Edition, Hola vaya demasiado**herramientas** -> **Python Tools** -> **entornos de Python** y, a continuación, haga clic en **+ personalizada**. 
> 
> 

Anaconda Python 2.7 se instala en C:\Anaconda y Anaconda Python 3.5 se instala en c:\Anaconda\envs\py35. Consulte la [documentación de PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) para ver los pasos detallados. 

### <a name="jupyter-notebook"></a>Jupyter Notebook
Distribución de anaconda también incluye Jupyter notebook, un código de tooshare de entorno y los análisis. Previamente se ha configurado un servidor de notebooks de Jupyter con kernels de Python 2.7, Python 3.4, Python 3.5 y R. Hay un icono del escritorio con el nombre "Jupyter Notebook toolaunch Hola explorador tooaccess Hola servidor Bloc de notas. Si se encuentra en hello VM a través de escritorio remoto, también puede visitar [https://localhost:9999 /](https://localhost:9999/) tooaccess Hola servidor de Jupyter notebook cuando inicia sesión en toohello máquina virtual.

> [!NOTE]
> Continúe aunque aparezca una advertencia de certificado. 
> 
> 

Se ha empaquetado varios blocs de notas de ejemplo de Python y en R. Hola mostrar blocs de notas de Jupyter cómo toowork con Microsoft R Server, SQL Server 2016 R Services (análisis en bases de datos), Python, Microsoft cognitivos ToolKit (CNTK) para el aprendizaje profundo y otro Azure tecnologías de una vez que inicie sesión en tooJupyter. Puede ver ejemplos de hello vínculo toohello en página de inicio del Bloc de notas de hello después de la autenticación toohello Jupyter notebook mediante contraseña de Hola que creó en un paso anterior. 

### <a name="visual-studio-2015-community-edition"></a>Visual Studio 2015 Community Edition
Visual Studio Community edition instalado en hello máquina virtual. Es una versión gratuita de hello IDE popular de Microsoft que puede usar para fines de evaluación y para los equipos pequeños. Es posible desproteger Hola términos de licencia [aquí](https://www.visualstudio.com/support/legal/mt171547).  Abra Visual Studio haciendo doble clic en el icono del escritorio Hola o hello **iniciar** menú. Para buscar programas, también puede usar **Win** + **S** y escribir "Visual Studio". Una vez ahí, puede crear proyectos en lenguajes como C#, Python, R o node.js. Complementos también se instalan que hacen que sea conveniente toowork con servicios de Azure como el catálogo de datos de Azure y Azure HDInsight (Hadoop, Spark), Azure Data Lake. 

> [!NOTE]
> Quizás vea un mensaje que indica que el período de evaluación ha expirado. Escriba sus credenciales de cuenta de Microsoft o crear un nuevo toohello de acceso de tooget de cuenta gratuita Visual Studio Community Edition. 
> 
> 

### <a name="sql-server-2016-developer-edition"></a>SQL Server 2016 Developer Edition
Proporciona una versión para desarrolladores de SQL Server 2016 con análisis de R Services toorun en bases de datos en VM de Hola. R Services proporciona una plataforma para desarrollar e implementar aplicaciones inteligentes. Puede usar lenguaje de R enriquecido y eficaz de Hola y Hola muchos paquetes de modelos de toocreate de comunidad de Hola y generar predicciones para los datos de SQL Server. Puede mantener datos de análisis de toohello cerrar porque R Services (en bases de datos) se integran lenguaje Hola R con SQL Server. Esto elimina los costos de Hola y riesgos de seguridad asociados con el movimiento de datos.

> [!NOTE]
> Hola SQL Server 2016 developer edition solo pueden usarse para el desarrollo y con fines de prueba. Necesita una licencia toorun en producción. 
> 
> 

Puede tener acceso a SQL server de hello iniciando **SQL Server Management Studio**. El nombre de la máquina virtual se rellena como Hola nombre del servidor. Utilice la autenticación de Windows cuando inicia sesión como Hola administrador en Windows. Una vez que esté en SQL Server Management Studio, puede crear otros usuarios, crear bases de datos, importar datos y ejecutar consultas SQL. 

análisis de tooenable en bases de datos mediante Microsoft R, ejecute hello siguiente comando como una sola acción en SQL Server management studio después de iniciar sesión como administrador del servidor hello de tiempo. 

        CREATE LOGIN [%COMPUTERNAME%\SQLRUserGroup] FROM WINDOWS 

        (Please replace hello %COMPUTERNAME% with your VM name)


### <a name="azure"></a>Azure
Se instalan varias herramientas de Azure en hello VM:

* Hay un acceso directo de escritorio tooaccess documentación del SDK de Azure de Hola. 
* **AzCopy**: usa toomove datos dentro y fuera de la cuenta de almacenamiento de Microsoft Azure. uso de toosee, tipo **Azcopy** en un uso de hello toosee de símbolo del sistema. 
* **Microsoft Azure Storage Explorer**: usar toobrowse a través de objetos de hello almacenada dentro de su tooand de datos de cuenta de almacenamiento de Azure y la transferencia del almacenamiento de Azure. Puede escribir **Explorador de almacenamiento** de búsqueda o buscar en Hola tooaccess del menú de inicio de Windows esta herramienta. 
* **Adlcopy**: usa toomove datos tooAzure Data Lake. uso de toosee, tipo **adlcopy** en un símbolo del sistema. 
* **dtui**: usa toomove tooand de datos de base de datos de Azure Cosmos, una base de datos NoSQL nube Hola. Escriba **dtui** en el símbolo del sistema. 
* **Microsoft Data Management Gateway**: permite el traslado de datos entre orígenes de datos locales y en la nube. Se usa en herramientas como Azure Data Factory. 
* **Microsoft Azure Powershell**: emplea una herramienta tooadminister los recursos de Azure en hello en la máquina virtual también está instalado el lenguaje de scripting de Powershell. 

### <a name="power-bi"></a>Power BI
toohelp va a crear paneles y visualizaciones excelentes, hello **Power BI Desktop** se ha instalado. Usar estos datos de toopull de herramienta de orígenes diferentes, tooauthor los paneles e informes y toopublish les toohello en la nube. Para obtener información, vea hello [Power BI](http://powerbi.microsoft.com) sitio. Puede encontrar Power BI desktop en el menú de inicio de Hola. 

> [!NOTE]
> Es necesario un tooaccess de cuenta de Office 365 Power BI. 
> 
> 

## <a name="additional-microsoft-development-tools"></a>Herramientas de desarrollo de Microsoft adicionales
Hola [ **instalador de plataforma Web de Microsoft** ](https://www.microsoft.com/web/downloads/platform.aspx) puede ser usado toodiscover y descargue otras herramientas de desarrollo de Microsoft. También es una herramienta de toohello de método abreviado proporcionada en el escritorio de Microsoft Data Science Virtual Machine Hola.  

## <a name="important-directories-on-hello-vm"></a>Directorios importantes en hello VM
| Elemento | Directorio |
| --- | --- |
| Configuraciones del servidor de notebooks de Jupyter |C:\ProgramData\jupyter |
| Directorio principal de ejemplos de notebooks de Jupyter |c:\dsvm\notebooks |
| Otros ejemplos |c:\dsvm\samples |
| Anaconda (predeterminado: Python 2.7) |c:\Anaconda |
| Entorno Anaconda Python 3.5 |c:\Anaconda\envs\py35 |
| Directorio de la instancia de R Server Standalone (instancia predeterminada de R basada en R3.2.2) |C:\Archivos de programa\Microsoft SQL Server\130\R_SERVER |
| Directorio de la instancia en base de datos de R Server (R3.2.2) |C:\Archivos de programa\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES |
| Directorio de la instancia de Microsoft R Open (R3.3.1) |C:\Archivos de programa\Microsoft\MRO-3.3.1 |
| Herramientas varias |c:\dsvm\tools |

> [!NOTE]
> Las instancias de hello que Microsoft Data Science Virtual Machine creado antes 1.5.0 (antes del 3 de septiembre de 2016) utilizan una estructura de directorios ligeramente diferente que los especificados en la tabla anterior de Hola. 
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Estos es algunos toocontinue de pasos siguiente el aprendizaje y la exploración. 

* Explorar Hola diversas herramientas de ciencia de datos en la ciencia de datos de hello VM haciendo clic en hello menú Inicio y desproteger Hola herramientas que se indican en el menú de Hola.
* Navegue demasiado**C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\RevoScaleR\demoScripts** para obtener ejemplos de uso de hello RevoScaleR biblioteca de R que admite el análisis de datos a escala empresarial.  
* Leer el artículo de hello: [10 cosas que puede hacer en hello ciencia de datos Máquina Virtual](http://aka.ms/dsvmtenthings)
* Obtenga información acerca de cómo Hola toobuild final tooend las soluciones analíticas sistemáticamente mediante [proceso de ciencia de datos de equipo](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).
* Visite hello [Cortana Intelligence galería](http://gallery.cortanaintelligence.com) para análisis de datos y aprendizaje de máquina ejemplos que Hola de uso conjunto de inteligencia de Cortana. También hemos proporcionado un icono en hello **iniciar** menú y escritorio Hola de galería de toothis de hello máquinas virtuales.

