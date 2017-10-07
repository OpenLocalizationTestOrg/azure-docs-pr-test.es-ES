---
title: "Hola aaaProvision datos ciencia Máquina Virtual para Linux (Ubuntu) en Azure | Documentos de Microsoft"
description: "Configurar y crear una máquina Virtual de ciencia de datos para (Ubuntu) de Linux en Azure toodo análisis y aprendizaje automático."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3bab0ab9-3ea5-41a6-a62a-8c44fdbae43b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 037c126c0a35d8065fc89c591089df73d2b91425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-data-science-virtual-machine-for-linux-ubuntu"></a>Aprovisionar Hola Data Science Virtual Machine para Linux (Ubuntu)
Hola Data Science Virtual Machine para Linux está basado en un Ubuntu imagen de máquina virtual que hace más fácil tooget a iniciarse en profundidad en Azure. Las herramientas de aprendizaje profundo incluyen las siguientes:

  * [Caffe](http://caffe.berkeleyvision.org/): entorno de aprendizaje profundo diseñado para lograr velocidad, expresividad y modularidad
  * [Caffe2](https://github.com/caffe2/caffe2): versión multiplataforma de Caffe
  * [Computational Network Toolkit (CNTK)](https://github.com/Microsoft/CNTK): kit de herramientas de software de aprendizaje profundo de Microsoft Research
  * [H2O](https://www.h2o.ai/): interfaz gráfica de usuario y plataforma de macrodatos de código abierto
  * [Keras](https://keras.io/): API de red neuronal de alto nivel en Python para Theano y TensorFlow
  * [MXNet](http://mxnet.io/): biblioteca de aprendizaje profundo flexible y eficaz con muchos enlaces de lenguaje
  * [NVIDIA DIGITS](https://developer.nvidia.com/digits): sistema gráfico que simplifica las tareas comunes de aprendizaje profundo
  * [TensorFlow](https://www.tensorflow.org/): biblioteca de código abierto para inteligencia automática de Google
  * [Theano](http://deeplearning.net/software/theano/): biblioteca de Python para definir, optimizar y evaluar de manera eficaz expresiones matemáticas que implican matrices multidimensionales
  * [Torch](http://torch.ch/): entorno informático científico con amplia compatibilidad con algoritmos de aprendizaje automático
  * CUDA, cuDNN y controlador NVIDIA Hola
  * Muchos cuadernos de Jupyter Notebook de ejemplo

Todas las bibliotecas que son versiones GPU de hello, aunque también se ejecutarán en hello CPU.

Hola Data Science Virtual Machine para Linux también contiene herramientas populares de informática y desarrollo de las actividades de datos, incluidos:

* Microsoft R Server Developer Edition con Microsoft R Open
* Distribución de Anaconda Python (versiones 2.7 y 3.5), incluidas las bibliotecas de análisis de datos más conocidas
* JuliaPro : distribución protegida del lenguaje Julia con bibliotecas populares científicas y de análisis de datos
* Instancia independiente de Spark y Hadoop de un solo nodo (HDFS, Yarn)
* JupyterHub: servidor de Jupyter Notebook multiusuario compatible con kernels de R, Python, PySpark y Julia
* Explorador de Azure Storage
* Interfaz de la línea de comandos de Azure (CLI) para administrar recursos de Azure
* Herramientas de aprendizaje automático
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): sistema de aprendizaje automático rápido que admite varias técnicas, como el aprendizaje en línea, el uso de hash, la clase AllReduce, las reducciones, learning2search y los aprendizajes activo e interactivo
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): herramienta que proporciona una implementación de árbol ampliada, rápida y precisa
  * [Rattle](http://rattle.togaware.com/): herramienta gráfica que facilita comenzar a trabajar con análisis de datos y aprendizaje automático
  * [LightGBM](https://github.com/Microsoft/LightGBM): entorno de potenciación de gradientes rápido, distribuido y de alto rendimiento
* Azure SDK en Java, Python, node.js, Ruby, PHP
* Bibliotecas en R y Python para usarlas en Aprendizaje automático de Azure y en otros servicios de Azure
* Editores y herramientas de desarrollo (RStudio, PyCharm, IntelliJ, Emacs, vim)


La ciencia de datos implica la iteración de una secuencia de tareas:

1. Buscar, cargar y preprocesar datos
2. Compilar y probar modelos
3. Implementar modelos de Hola para su uso en aplicaciones inteligentes

Los científicos de datos usan varios toocomplete herramientas estas tareas. Puede ser bastante lento toofind hello las versiones del software hello y después compile toodownload e instala estas versiones.

Hola Data Science Virtual Machine para Linux puede facilitar esta carga considerablemente. Usar inicio toojump el proyecto de análisis. Le permite toowork de tareas en varios idiomas, incluidos R, Python, SQL, Java y C++. Hola incluido en hello VM de Azure SDK permite toobuild sus aplicaciones mediante el uso de varios servicios en Linux para la plataforma de nube de Microsoft de Hola. Además, tiene acceso tooother idiomas como Ruby, Perl, PHP y node.js que también están instalados previamente.

No hay ningún cargo de software para esta imagen de VM de ciencia de datos. Se paga solo hello Azure hardware uso cuotas que se evalúan según Hola tamaño de máquina virtual de Hola que se aprovisiona. Obtener más detalles sobre Hola calculan las cuotas pueden encontrarse en hello [página de listado de VM en Azure Marketplace hello](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm/).

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>Otras versiones de hello Data Science Virtual Machine
A [CentOS](machine-learning-data-science-linux-dsvm-intro.md) también está disponible la imagen, con muchas de hello mismo herramientas como Hola Ubuntu imagen. También hay una imagen de [Windows](machine-learning-data-science-provision-vm.md) disponible.

## <a name="prerequisites"></a>Requisitos previos
Antes de que pueda crear una instancia de Data Science Virtual Machine para Linux, debe tener una suscripción a Azure. tooobtain uno, vea [evaluación gratuita de Azure obtener](https://azure.microsoft.com/free/).

## <a name="create-your-data-science-virtual-machine-for-linux"></a>Creación de la instancia de Data Science Virtual Machine para Linux
A continuación, incluimos Hola pasos toocreate una instancia de hello Data Science Virtual Machine para Linux:

1. Navegar por la máquina virtual de toohello enumerar en hello [portal de Azure](https://portal.azure.com/#create/microsoft-ads.linux-data-science-vm-ubuntulinuxdsvmubuntu).
2. Haga clic en **crear** (en la parte inferior de hello) toobring Asistente Hola.![ configurar datos-ciencia-vm](./media/machine-learning-data-science-dsvm-ubuntu-intro/configure-data-science-virtual-machine.png)
3. Hola siguientes secciones proporciona entradas de Hola para cada uno de los pasos de hello en Asistente hello (enumerado en hello derecha del saludo anterior figura) utilizan toocreate Hola Microsoft Data Science Virtual Machine. A continuación, incluimos Hola entradas necesitados tooconfigure cada de estos pasos:
   
   a. **Aspectos básicos**:
   
   * **Nombre**: nombre del servidor de ciencia de datos que está creando.
   * **Nombre de usuario**: identificador de acceso de la primera cuenta.
   * **Contraseña**: contraseña de la primera cuenta (puede usar una clave pública SSH en lugar de una contraseña).
   * **Suscripción**: si tiene más de una suscripción, seleccione Hola uno en qué Hola máquina es toobe creado y factura. Debe tener privilegios de creación de recursos en esta suscripción.
   * **Grupo de recursos**: puede crear uno nuevo o usar un grupo que ya exista.
   * **Ubicación**: Centro de datos seleccione hello más adecuada. Normalmente es el centro de datos de Hola que tenga la mayoría de los datos, o es más cercano ubicación física tooyour más rápido acceso a la red.
   
   b. **Tamaño**:
   
   * Seleccione uno de los tipos de servidor hello que cumpla los requisitos funcionales y límites de costos. Seleccione **ver todos** toosee más opciones de tamaños de máquina virtual. Seleccione una VM de clase NC para aprendizaje de GPU.
   
   c. **Configuración**:
   
   * **Tipo de disco**: elija **Premium** si prefiere una unidad de estado sólido (SSD). De lo contrario, elija **Estándar**. Las VM de GPU requieren un disco estándar.
   * **Cuenta de almacenamiento**: puede crear una nueva cuenta de almacenamiento de Azure en su suscripción, o utilizar uno existente en hello misma ubicación que se ha elegido en hello **Fundamentos** paso del Asistente para saludo.
   * **Otros parámetros**: en la mayoría de los casos, solo se utilice valores predeterminados de Hola. valores no predeterminados de tooconsider, mantenga el mouse sobre un vínculo informativo Hola para ayudar a en campos específicos de Hola.
   
   d. **Resumen**:
   
   * Compruebe que toda la información que ha especificado es correcta.
   
   e. **Comprar**:
   
   * toostart Hola aprovisionamiento, haga clic en **comprar**. Se proporciona un vínculo términos de toohello de transacción de Hola. Hola VM no tiene todos los cargos adicionales más allá del proceso de hello para el tamaño del servidor hello que eligió en hello **tamaño** paso.

Aprovisionamiento de Hello tardará unos 5-10 minutos. estado de Hola de aprovisionamiento de Hola se muestra en hello portal de Azure.

## <a name="how-tooaccess-hello-data-science-virtual-machine-for-linux"></a>¿Cómo tooaccess Hola Data Science Virtual Machine para Linux
Después de Hola que se crea la VM, puede iniciar sesión en tooit a través de SSH. Usar credenciales de cuenta de hello que creó en hello **Fundamentos** sección del paso 3 para la interfaz de shell de texto hello. En Windows, puede descargar una herramienta de cliente SSH como [Putty](http://www.putty.org). Si prefiere un escritorio gráfico (X Windows System), puede usar X11 de reenvío en Putty o instalar el cliente de X2Go Hola.

> [!NOTE]
> cliente Hello X2Go rendimiento significativamente mejor que X11 de reenvío en las pruebas. Se recomienda utilizar el cliente de hello X2Go para una interfaz gráfica de escritorio.
> 
> 

## <a name="installing-and-configuring-x2go-client"></a>Instalación y configuración del cliente X2Go
Hola Linux VM ya se aprovisiona con X2Go server y las conexiones de cliente de tooaccept listo. Hola tooconnect toohello escritorio gráfica de VM de Linux, siga en el cliente:

1. Descargar e instalar el cliente de hello X2Go para la plataforma de cliente de [X2Go](http://wiki.x2go.org/doku.php/doc:installation:x2goclient).    
2. Ejecute el cliente de hello X2Go y seleccione **nueva sesión**. Se abrirá una ventana de configuración con varias pestañas. Escriba Hola parámetros de configuración siguientes:
   * **Pestaña Sesión**:
     * **Host**: nombre de host de Hola o dirección IP de la máquina virtual la ciencia de datos de Linux.
     * **Inicio de sesión**: nombre de usuario en hello VM de Linux.
     * **Puerto SSH**: Déjelo en 22, valor predeterminado de Hola.
     * **Tipo de sesión**: cambio Hola valor tooXFCE. Hola VM de Linux sólo admite actualmente desktop XFCE.
   * **Ficha de medios**: puede desactivar la compatibilidad de sonido y cliente de impresión si no necesita toouse ellos.
   * **Carpetas compartidas**: si desea directorios desde los equipos cliente que se ha montado en hello VM de Linux, agregar directorios del equipo cliente hello que desea tooshare con hello VM en esta pestaña.

Después de iniciar sesión en toohello VM mediante el uso de cliente de SSH de Hola o escritorio gráfica de XFCE a través del cliente de X2Go hello, está listo toostart mediante herramientas de Hola que están instalados y configurados en hello VM. En XFCE, puede ver los accesos directos del menú de las aplicaciones y los iconos del escritorio para muchas de las herramientas de Hola.

## <a name="tools-installed-on-hello-data-science-virtual-machine-for-linux"></a>Herramientas instaladas en hello Data Science Virtual Machine para Linux
### <a name="deep-learning-libraries"></a>Bibliotecas de aprendizaje profundo

#### <a name="cntk"></a>CNTK
Hola Microsoft cognitivos Toolki - también conocido como CNTK - es un código abierto, Kit de herramientas de aprendizaje profundo. Enlaces de Python están disponibles en entornos de hello raíz y py35 Conda. También tiene una herramienta de línea de comandos (cntk) que ya está en la ruta de acceso de Hola.

En JupyterHub hay disponibles cuadernos Python de ejemplo. toorun un ejemplo básico en línea de comandos de hello, ejecute hello siga los comandos en el shell de hello:

    cd /home/[USERNAME]/notebooks/CNTK/HelloWorld-LogisticRegression
    cntk configFile=lr_bs.cntk makeMode=false command=Train

Para obtener más información, vea Hola sección CNTK de [GitHub](https://github.com/Microsoft/CNTK), hello y [CNTK wiki](https://github.com/Microsoft/CNTK/wiki).

#### <a name="caffe"></a>Caffe
Caffe es un profundo marco de hello Berkeley visión y centro de aprendizaje de aprendizaje. Está disponible en /opt/caffe. Puede encontrar ejemplos en /opt/caffe/examples.

#### <a name="caffe2"></a>Caffe2
Caffe2 es un marco de aprendizaje profundo de Facebook basado en Caffe. Está disponible en Python 2.7 en entorno de hello Conda raíz. tooactivate se ejecute siguiente de Hola desde el shell de hello:

    source /anaconda/bin/activate root

En JupyterHub hay disponibles algunos cuadernos de ejemplo.

#### <a name="h2o"></a>H2O
H2O es una plataforma de análisis predictivo y aprendizaje automático rápida, distribuida y en memoria. Se instala un paquete de Python en ambos entornos de Anaconda Hola raíz y py35. También se instala un paquete de R. toostart H2O de ejecutar la línea de comandos hello `java -jar /dsvm/tools/h2o/current/h2o.jar`; hay diversas [opciones de línea de comandos](http://docs.h2o.ai/h2o/latest-stable/h2o-docs/starting-h2o.html#from-the-command-line) que les gusta tooconfigure. Hola de flujo de interfaz de usuario Web puede tener acceso al examinar tooget toohttp://localhost:54321 iniciado. En JupyterHub también hay disponibles cuadernos de ejemplo.

#### <a name="keras"></a>Keras
Keras es una API de red neuronal de alto nivel en Python capaz de ejecutarse en Tensorflow o Theano. Está disponible en entornos de Python de raíz y py35 Hola. 

#### <a name="mxnet"></a>MXNet
MXNet es un entorno de aprendizaje profundo diseñado para lograr eficiencia y flexibilidad. Tiene los enlaces de R y Python incluido en hello DSVM. Se incluyen cuadernos de ejemplo en JupyterHub y hay código de ejemplo disponible en /dsvm/samples/mxnet.

#### <a name="nvidia-digits"></a>NVIDIA DIGITS
Hola NVIDIA profundo aprendizaje GPU entrenamiento sistema, conocido como dígitos, es un sistema toosimplify aprendizaje profundo las tareas comunes como administración de datos, diseñar y redes neuronales de entrenamiento en sistemas GPU y supervisar el rendimiento en tiempo real con visualización avanzada. 

DIGITS está disponible como un servicio llamado digits. Iniciar servicio de Hola y examinar tooget toohttp://localhost:5000 iniciado.

DÍGITOS también se instala como un módulo de Python en entorno de hello Conda root.

#### <a name="tensorflow"></a>TensorFlow
TensorFlow es la biblioteca de aprendizaje profundo de Google. Es una biblioteca de software de código abierto para cálculo numérico con gráficos de flujo de datos. TensorFlow está disponible en el entorno de hello py35 Python y algunos blocs de notas de ejemplo se incluyen en JupyterHub.

#### <a name="theano"></a>Theano
Theano es una biblioteca Python para lograr un cálculo numérico eficaz. Está disponible en entornos de Python de raíz y py35 Hola. 

#### <a name="torch"></a>Torch
Torch es un entorno informático científico con amplia compatibilidad con algoritmos de aprendizaje automático. Está disponible en /dsvm/tools/torch y sesión interactiva de hello th y Administrador de paquetes de luarocks están disponibles en línea de comandos de Hola. Hay ejemplos disponibles en /dsvm/samples/torch.

PyTorch también está disponible en el entorno Anaconda de hello raíz. Puede encontrar ejemplos en /dsvm/samples/pytorch.

### <a name="microsoft-r-server"></a>Microsoft R Server
R es uno de los lenguajes más populares de hello para el análisis de datos y aprendizaje automático. Si desea toouse R para los análisis, Hola VM tiene Microsoft R Server (Sra.) con hello abierto de R (MRO) y Math Kernel Library (MKL). Hola MKL optimiza las operaciones matemáticas comunes en los algoritmos de análisis. MRO es compatible con CRAN R al 100 por ciento, y cualquiera de las bibliotecas de hello R publicadas en CRAN puede instalarse en hello MRO. MRS ofrece el escalado y la operacionalización de los modelos de R en servicios web. Puede editar los programas de R en uno de los editores de valor predeterminado de hello, como RStudio, vi o Emacs. Si está utilizando el editor de Emacs hello, tenga en cuenta ese paquete de Emacs Hola ESS (Emacs habla estadísticas), que simplifica el trabajo con archivos de R en el editor de Emacs hello, se ha instalado previamente.

consola de toolaunch R, basta con que escriba **R** en el shell de Hola. Esto le llevará entorno interactivo de tooan. toodevelop el programa de R, por lo general, utilice un editor como Emacs o vi y, a continuación, ejecutar scripts de hello en R. Con RStudio, tendrá un gráfico completo toodevelop entorno de IDE el programa de R.

También hay un script de R para hello tooinstall [paquetes de R de 20 superior](http://www.kdnuggets.com/2015/06/top-20-r-packages.html) si desea. Este script se puede ejecutar después de que se encuentra en la interfaz interactiva Hola R, que se puede especificar (como se mencionó) escribiendo **R** en el shell de Hola.  

### <a name="python"></a>Python
Para el desarrollo con Python, se ha instalado Anaconda Python Distribution 2.7 y 3.5. Esta distribución contiene Hola base Python junto con unos 300 de hello paquetes más populares matemáticas, ingeniería y datos de análisis. Puede usar los editores de texto predeterminado Hola. Además, puede usar Spyder, un IDE de Python que integra las distribuciones de Anaconda Python. Spyder necesita un escritorio gráfico o el reenvío de X11. Un tooSpyder de acceso directo se proporciona en desktop gráfica Hola.

Puesto que tenemos Python 2.7 y 3.5, tendrá que toospecifically activar versión de Python de hello deseado (conda entorno) desea toowork en Hola sesión actual. proceso de activación de Hello establece la variable toohello versión deseada de Python para la ruta de acceso Hola.

entorno tooactivate Hola Python 2.7 conda, ejecute siguiente de Hola desde el shell de hello:

    source /anaconda/bin/activate root

Python 2.7 se instalará en */anaconda/bin*.

entorno tooactivate Hola 3.5 de Python conda, ejecute siguiente de Hola desde el shell de hello:

    source /anaconda/bin/activate py35


Python 3.5 se instalará en */anaconda/envs/py35/bin*.

tooinvoke una sesión interactiva de Python, simplemente escriba **python** en el shell de Hola. Si se encuentran en una interfaz gráfica o tiene X11 reenvío conjunto de seguridad, puede escribir **pycharm** toolaunch hello PyCharm IDE de Python.

tooinstall bibliotecas adicionales de Python, necesita toorun ```conda``` o ````pip```` comando bajo sudo y proporcionar una ruta de acceso completa del Administrador de paquetes de saludo Python (conda o pip) tooinstall toohello Python entorno correcto. Por ejemplo:

    sudo /anaconda/bin/pip install <package> #for Python 2.7 environment
    sudo /anaconda/envs/py35/bin/pip install <package> # for Python 3.5 environment


### <a name="jupyter-notebook"></a>Jupyter Notebook
Hola distribución de Anaconda también incluye Jupyter notebook, un código de tooshare de entorno y los análisis. el Bloc de notas de Hello Jupyter se accede a través de JupyterHub. Inicie sesión con su nombre de usuario y contraseña de Linux local.

servidor de Hello Jupyter notebook se ha configurado previamente con Python 2, 3 de Python y los kernels de R. No hay un icono del escritorio denominado "Jupyter Notebook" toolaunch Hola explorador tooaccess Hola Bloc de notas server. Si se encuentra en hello VM mediante el cliente de SSH o X2Go, también puede visitar [https://localhost:8000 /](https://localhost:8000/) tooaccess Hola servidor de Jupyter notebook.

> [!NOTE]
> Continúe aunque aparezca una advertencia de certificado.
> 
> 

Servidor de hello Jupyter notebook puede tener acceso desde cualquier host. Solo tiene que escribir *https://\<<Nombre DNS o dirección IP de la máquina virtual\>:8000/*

> [!NOTE]
> Puerto 8000 se abre en firewall de Hola de forma predeterminada cuando se aprovisiona Hola máquina virtual.
> 
> 

Nos hemos empaquetados blocs de notas de ejemplo--Python en uno y otro en R. Puede ver ejemplos de hello vínculo toohello en página de inicio del Bloc de notas de hello después de la autenticación toohello Jupyter notebook utilizando su nombre de usuario de Linux local y la contraseña. Puede crear un nuevo bloc de notas seleccionando **nuevo**y, a continuación, el kernel de idioma apropiado Hola. Si no ve hello **New** botón, haga clic en hello **Jupyter** icono de página de inicio de hello toogo izquierdo superior toohello del servidor de Bloc de notas de Hola.

### <a name="apache-spark-standalone"></a>Apache Spark Standalone 
Una instancia independiente de Apache Spark está preinstalada en hello toohelp Linux DSVM para desarrollar aplicaciones de Spark localmente primero antes de probar e implementar en clústeres de gran tamaño. Puede ejecutar programas de PySpark a través de kernel de Jupyter Hola. Cuando se abre Jupyter y haga clic en el botón "Nuevo" que Hola verá una lista de núcleos disponibles. Hola "Spark – Python" es kernel PySpark de Hola que le permitirá crear Spark aplicaciones mediante el lenguaje de Python. También puede usar un IDE de Python como PyCharm o Spyder toobuild inspirará programa. Desde entonces, se trata de una instancia independiente, pila de Spark Hola se ejecuta dentro de hello llamando a programa cliente. Esto resulta más rápido y más fácil de problemas de tootroubleshoot comparan toodeveloping en un clúster de Spark. 

Un bloc de notas de PySpark de ejemplo se proporciona en Jupyter que se puede encontrar en directorio de "SparkML" hello en el directorio particular de Hola de Jupyter ($ principal/portátiles/SparkML/pySpark). 

Si programa en R para Spark, puede usar Microsoft R Server, SparkR o sparklyr. 

Antes de ejecutar en el contexto de Spark en Microsoft R Server, debe toodo una tooenable de paso el programa de instalación de una vez un único nodo local Hadoop HDFS y una instancia de Yarn. De forma predeterminada, los servicios Hadoop están instalados pero deshabilitados en hello DSVM. En orden tooenable, tienes que hello toorun siga los comandos como Hola raíz primera vez:

    echo -e 'y\n' | ssh-keygen -t rsa -P '' -f ~hadoop/.ssh/id_rsa
    cat ~hadoop/.ssh/id_rsa.pub >> ~hadoop/.ssh/authorized_keys
    chmod 0600 ~hadoop/.ssh/authorized_keys
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa.pub
    chown hadoop:hadoop ~hadoop/.ssh/authorized_keys
    systemctl start hadoop-namenode hadoop-datanode hadoop-yarn

Puede detener hello Hadoop relacionadas con servicios cuando no necesite ejecutando ````systemctl stop hadoop-namenode hadoop-datanode hadoop-yarn```` un ejemplo que muestra cómo Sra. toodevelop y prueba en el contexto de Spark remoto (que es la instancia de Spark independiente de hello en hello DSVM) se proporciona y disponible en hello `/dsvm/samples/MRS` directory. 

### <a name="ides-and-editors"></a>IDE y editores
Puede elegir varios editores de código. Estos incluyen vi/VIM, Emacs, PyCharm, RStudio e IntelliJ. IntelliJ, RStudio y PyCharm son editores gráficos y tendrás toobe firmado en tooa gráfica escritorio toouse ellos. Estos editores tienen escritorio y aplicación toolaunch de accesos directos de menú ellos.

**VIM** y **Emacs** son editores basados en texto. En Emacs, se ha instalado un paquete de complemento llamado Emacs habla estadísticas (ESS) que facilita el trabajo con R en el editor de Emacs Hola. Puede obtener más información en [ESS](http://ess.r-project.org/).

**Látex** se instala mediante hello texlive paquete junto con un complemento de Emacs [auctex](https://www.gnu.org/software/auctex/manual/auctex/auctex.html) paquete, lo que simplifica la creación de los documentos látex Emacs.  

### <a name="databases"></a>Bases de datos

#### <a name="graphical-sql-client"></a>Cliente SQL gráfico
**Ardilla SQL**, se ha proporcionado un cliente SQL gráfico, bases de datos de tooconnect toodifferent (por ejemplo, Microsoft SQL Server y MySQL) y consultas SQL toorun. Esto se puede ejecutar desde una sesión de escritorio gráfica (mediante el cliente de X2Go hello, por ejemplo). tooinvoke ardilla SQL, puede iniciarlo desde el icono de hello en el escritorio de Hola o ejecute hello siguiente comando en el shell de Hola.

    /usr/local/squirrel-sql-3.7/squirrel-sql.sh

Antes de hello use por primera vez, configure los controladores y los alias de la base de datos. controladores JDBC Hola se encuentran en:

*/usr/share/java/jdbcdrivers*

Para obtener más información, consulte [SQuirrel SQL](http://squirrel-sql.sourceforge.net/index.php?page=screenshots).

#### <a name="command-line-tools-for-accessing-microsoft-sql-server"></a>Herramientas de línea de comandos para tener acceso a Microsoft SQL Server
paquete de controladores ODBC de Hola para SQL Server también incluye dos herramientas de línea de comandos:

**BCP**: forma masiva Hola bcp copia datos entre una instancia de Microsoft SQL Server y un archivo de datos en un formato especificado por el usuario. utilidad bcp de Hello puede ser usado tooimport grandes cantidades de filas nuevas en tablas de SQL Server, o tooexport datos de tablas a archivos de datos. tooimport datos en una tabla, debe usar un archivo de formato creado para esa tabla, o comprender Hola estructura de tabla de Hola y tipos de Hola de datos que son válidos para sus columnas.

Puede encontrar más información en [Conexión con bcp](https://msdn.microsoft.com/library/hh568446.aspx).

**Sqlcmd**: puede escribir instrucciones Transact-SQL con la utilidad sqlcmd de hello, así como los procedimientos de sistema y archivos en línea de comandos de Hola de script. Esta herramienta utiliza lotes de tooexecute Transact-SQL de ODBC.

Puede encontrar más información en [Conexión con sqlcmd](https://msdn.microsoft.com/library/hh568447.aspx).

> [!NOTE]
> Existen algunas diferencias en esta utilidad entre las plataformas de Windows y Linux. Consulte la documentación de Hola para obtener más información.
> 
> 

#### <a name="database-access-libraries"></a>Bibliotecas de acceso a las bases de datos
Existen bibliotecas de R y Python tooaccess bases de datos.

* En R, Hola **RODBC** paquete o **dplyr** paquete permite tooquery o ejecutar instrucciones SQL en el servidor de base de datos de Hola.
* En Python, Hola **pyodbc** biblioteca proporciona acceso a la base de datos con ODBC como Hola capa subyacente.  

### <a name="azure-tools"></a>Herramientas de Azure
Hola siguientes herramientas de Azure está instalado en hello VM:

* **Interfaz de línea de comandos de Azure**: Hola CLI de Azure permite toocreate y administrar recursos de Azure a través de los comandos de shell. tooinvoke Hola herramientas de Azure, simplemente escriba **ayuda azure**. Para obtener más información, vea hello [página de documentación de Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).
* **Microsoft Azure Storage Explorer**: Microsoft Azure Storage Explorer es una herramienta gráfica que es usado toobrowse a través de objetos de Hola que ha almacenado en la cuenta de almacenamiento de Azure y tooupload y descarga tooand datos blobs de Azure. Explorador de almacenamiento puede tener acceso desde el icono de acceso directo de escritorio de Hola. Puede invocarlo desde el símbolo del sistema del shell escribiendo **StorageExplorer**. Necesita toobe sesión se inició desde un cliente de X2Go, o tiene X11 reenvío conjunto de seguridad.
* **Bibliotecas de Azure**: siguientes de hello son algunos de bibliotecas de hello previamente instalados.
  
  * **Python**: Hola relacionadas con Azure bibliotecas de Python que se instala son **azure**, **azureml**, **pydocumentdb**, y **pyodbc** . Con hello en primer lugar tres bibliotecas, puede tener acceso a servicios de almacenamiento de Azure, aprendizaje automático de Azure y base de datos de Azure Cosmos (una base de datos NoSQL en Azure). cuarto biblioteca Hello, pyodbc (junto con hello Microsoft ODBC driver para SQL Server), permite acceso tooSQL Server, base de datos de SQL Azure y almacenamiento de datos de SQL Azure de Python, mediante una interfaz ODBC. Escriba **lista pip** toosee Hola a todos aparece las bibliotecas. Ser seguro toorun este comando en ambos Hola Python 2.7 y 3.5 entornos.
  * **R**: Hola relacionadas con Azure bibliotecas de R que se instalan son **AzureML** y **RODBC**.
  * **Java**: lista de Hola de bibliotecas de Java de Azure puede encontrarse en el directorio de hello **/dsvm/sdk/AzureSDKJava** en hello máquina virtual. bibliotecas de clave de Hello son Azure almacenamiento y administración de API, base de datos de Azure Cosmos y JDBC controladores para SQL Server.  

Puede tener acceso a hello [portal de Azure](https://portal.azure.com) desde el explorador Firefox preinstalada de Hola. En el portal de Azure hello, puede crear, administrar y supervisar los recursos de Azure.

### <a name="azure-machine-learning"></a>Aprendizaje automático de Azure
Aprendizaje automático de Azure es un servicio de nube totalmente administrado que le permite toobuild, implementar y compartir las soluciones de análisis predictivos. Puede crear sus experimentos y modelos desde Azure Machine Learning Studio. Se puede tener acceso desde un explorador web en la máquina virtual de hello datos ciencia visitando [aprendizaje automático de Microsoft Azure](https://studio.azureml.net).

Después de iniciar sesión en tooAzure estudio de aprendizaje automático, tendrá acceso tooan experimentación lienzo donde puede crear un flujo lógico para algoritmos de aprendizaje automático de Hola. También dispone acceso tooa Jupyter portátil hospedada en aprendizaje automático de Azure y puede funcionar perfectamente con los experimentos de hello en estudio de aprendizaje automático. Incorporación de operatividad a modelos que ha creado y ajustarlas en una interfaz de servicio web de aprendizaje de automático de Hola. Esto permite que los clientes escritos en las predicciones de tooinvoke de lenguaje de modelos de aprendizaje automático de Hola. Para obtener más información, vea hello [documentación de aprendizaje automático](https://azure.microsoft.com/documentation/services/machine-learning/).

Puede también generar los modelos en R o Python en hello VM y, a continuación, implementarlo en producción en aprendizaje automático de Azure. Se han instalado bibliotecas de R (**AzureML**) y Python (**azureml**) tooenable esta funcionalidad.

Para obtener información sobre cómo toodeploy los modelos de R y Python en aprendizaje automático de Azure, consulte [diez cosas que puede hacer en hello ciencia de datos Virtual Machine](machine-learning-data-science-vm-do-ten-things.md) (en concreto, sección Hola "generar modelos con R o Python y comenzar a ellos Usar aprendizaje automático de Azure").

> [!NOTE]
> Estas instrucciones se escribieron para la versión de Windows hello de hello VM de ciencia de datos. Pero siempre que haya sobre la implementación de modelos tooAzure aprendizaje automático de información de hello es aplicable toohello VM de Linux.
> 
> 

### <a name="machine-learning-tools"></a>Herramientas de aprendizaje automático
Hola VM incluye algunas herramientas y algoritmos que se han compilado previamente y previamente instalado localmente de aprendizaje de automático. Entre ellos se incluyen los siguientes:

* **Vowpal Wabbit**: algoritmo de aprendizaje rápido en línea
* **xgboost**: herramienta que proporciona los algoritmos de árbol ampliados y optimizados
* **Rattle**: herramienta gráfica basada en R para facilitar el modelado y la exploración de datos.
* **Python**: Anaconda Python integra algoritmos de aprendizaje automático con bibliotecas como Scikit-learn. Puede instalar otras bibliotecas mediante hello `pip install` comando.
* **LightGBM**: entorno de potenciación de gradientes rápido, distribuido y de alto rendimiento basado en algoritmos de árbol de decisión.
* **R**: una biblioteca de funciones de aprendizaje de máquina enriquecida está disponible para R. Algunas de las bibliotecas de Hola que previamente se instalan son lm, glm, randomForest, rpart. Puede instalar otras bibliotecas si ejecuta el comando:
  
        install.packages(<lib name>)

Aquí es información adicional sobre hello en primer lugar tres herramientas de aprendizaje de máquina en la lista de Hola.

#### <a name="vowpal-wabbit"></a>Vowpal Wabbit
Vowpal Wabbit es un sistema de aprendizaje automático rápido que emplea varias técnicas, como el aprendizaje en línea, el uso de hash, la clase AllReduce, las reducciones, learning2search y el aprendizaje activo e interactivo.

herramienta de hello toorun en un ejemplo muy básico, Hola siguientes:

    cp -r /dsvm/tools/VowpalWabbit/demo vwdemo
    cd vwdemo
    vw house_dataset

Puede encontrar otras demostraciones más grandes en ese directorio. Para obtener más información sobre VW, consulte [en esta sección de GitHub](https://github.com/JohnLangford/vowpal_wabbit), hello y [wiki de Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit/wiki).

#### <a name="xgboost"></a>XGBoost
Se trata de una biblioteca que está diseñada y optimizada para algoritmos incrementados (de árbol). objetivo de Hola de esta biblioteca es límites de cálculo de hello toopush de extremos de máquinas toohello necesario tooprovide impulso del árbol a gran escala que sea escalable, portátil y precisa.

Se proporciona como una línea de comandos, así como una biblioteca de R.

toouse esta biblioteca de R, puede iniciar una sesión interactiva de R (simplemente escribiendo **R** en el shell de hello) y la biblioteca de Hola de carga.

Este es un ejemplo sencillo que puede ejecutar en el símbolo del sistema de R:

    library(xgboost)

    data(agaricus.train, package='xgboost')
    data(agaricus.test, package='xgboost')
    train <- agaricus.train
    test <- agaricus.test
    bst <- xgboost(data = train$data, label = train$label, max.depth = 2,
                    eta = 1, nthread = 2, nround = 2, objective = "binary:logistic")
    pred <- predict(bst, test$data)

línea de comandos de toorun hello xgboost, presentamos Hola comandos tooexecute en el shell de hello:

    cp -r /dsvm/tools/xgboost/demo/binary_classification/ xgboostdemo
    cd xgboostdemo
    xgboost mushroom.conf


Se escribe un archivo de .model directorio toohello especificado. Puede encontrar información sobre este ejemplo de demostración [en GitHub](https://github.com/dmlc/xgboost/tree/master/demo/binary_classification).

Para obtener más información sobre xgboost, vea hello [página de documentación de xgboost](https://xgboost.readthedocs.org/en/latest/)y su [repositorio de GitHub](https://github.com/dmlc/xgboost).

#### <a name="rattle"></a>Rattle
Cascabel (hello **R** **A**nalytical **T**lápiz **T**o **L**disfrutar **E** asily) usa modelado y exploración de datos basado en GUI. Presenta estadísticas visuales resúmenes de datos, transformaciones que pueden modelarse con facilidad, compila supervisados y controlados modelos de datos de hello, presenta Hola rendimiento de los modelos de forma gráfica y conjuntos de datos nuevos de puntuaciones. También genera código de R, replicar las operaciones de Hola Hola interfaz de usuario que se pueden ejecutar directamente en R o utilizar como punto de partida para su posterior análisis.

toorun sonajero, deberá toobe en una gráfica escritorio inicio de sesión. En el terminal de hello, escriba ```R``` entorno de hello R tooenter. En el símbolo del sistema de hello R, escriba Hola siguientes comandos:

    library(rattle)
    rattle()

Se abrirá una interfaz gráfica con un conjunto de pestañas. Presentamos Hola inicio rápido de los pasos de toouse sonajero necesita un conjunto de datos de tiempo de ejemplo y generar un modelo. En algunos de estos pasos hello, va a instalar tooautomatically solicitadas y cargar algunos paquetes de R necesarios que ya no están en el sistema de Hola.

> [!NOTE]
> Si no tiene paquetes de saludo de tooinstall de acceso del directorio de sistema de hello (valor predeterminado de hello), verá un símbolo del sistema en la consola ventana tooinstall paquetes tooyour personal biblioteca de R. Si ve estos avisos, responda *y* .
> 
> 

1. Haga clic en **Ejecutar**.
2. Un cuadro de diálogo aparece, que le pide que si como ejemplo de Hola de toouse conjunto de datos de tiempo. Haga clic en **Sí** ejemplo de Hola a tooload.
3. Haga clic en hello **modelo** ficha.
4. Haga clic en **Execute** toobuild un árbol de decisión.
5. Haga clic en **dibujar** árbol de decisión de toodisplay Hola.
6. Haga clic en hello **bosque** botón de radio y haga clic en **Execute** toobuild un bosque aleatorio.
7. Haga clic en hello **Evaluate** ficha.
8. Haga clic en hello **riesgo** botón de radio y haga clic en **Execute** gráficos de rendimiento de toodisplay dos riesgo (acumulado).
9. Haga clic en hello **registro** Hola de tooshow ficha generar código de R para hello anteriores operaciones.
   (Debido a errores de tooa en la versión actual de Hola de sonajero, deberá tooinsert un  *#*  carácter delante del *exportar este registro...*  en texto hello del registro de hello.)
10. Haga clic en hello **exportar** con el nombre del archivo de script de Hola R para toosave botón *weather_script. R* carpeta particular de toohello.

Puede salir sonajero y R. Ahora puede modificar Hola genera un script de R o utilizarlo tal cual toorun en cualquier momento toorepeat todo lo que se realizan en hello cascabel interfaz de usuario. Específicamente para principiantes en R, se trata de una manera sencilla de tooquickly realizar análisis y aprendizaje en una interfaz gráfica simple, al generar automáticamente código en R toomodify automático y obtener información.

## <a name="next-steps"></a>Pasos siguientes
A continuación, mostramos cómo puede continuar con las tareas de aprendizaje y exploración:

* Hola [ciencia de datos en hello Data Science Virtual Machine para Linux](machine-learning-data-science-linux-dsvm-walkthrough.md) tutorial muestra cómo tooperform ciencia de datos común varias tareas con hello VM de ciencia de datos de Linux aprovisionado aquí. 
* Explorar Hola diversas herramientas de ciencia de datos en Hola ciencia de datos VM tratando de herramientas de Hola que se describen en este artículo. También puede ejecutar *dsvm-más-info* en el shell de hello dentro de la máquina virtual de Hola para una introducción y punteros toomore obtener información básica acerca de las herramientas de hello instalado en hello VM.  
* Obtenga información acerca de cómo toobuild-to-end las soluciones analíticas sistemáticamente mediante el uso de Hola [proceso de ciencia de datos de equipo](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).
* Visite hello [Cortana análisis galería](http://gallery.cortanaanalytics.com) para análisis de datos y aprendizaje de máquina ejemplos que Hola use Cortana Analytics Suite.

