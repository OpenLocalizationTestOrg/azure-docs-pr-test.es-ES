---
title: aaaGet a trabajar con R Server en HDInsight - Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate un Apache inspirará en clúster de HDInsight que incluye el servidor de R y enviar un script de R en clúster de Hola."
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a>Introducción al uso del servidor de R en HDInsight

HDInsight incluye una toobe de opción R Server integrado en el clúster de HDInsight. Esta opción permite a los scripts de R cálculos de toouse Spark y MapReduce toorun distribuida. En este documento, aprenderá cómo toocreate un servidor de R en los clústeres de HDInsight y, a continuación, ejecutar una R de archivo de comandos que se muestra el uso de Spark para distribuye los cálculos de R.


## <a name="prerequisites"></a>Requisitos previos

* **Una suscripción a Azure**: antes de comenzar este tutorial, debe tener una suscripción a Azure. Artículo vaya toohello [evaluación gratuita de Azure de Microsoft obtener](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) para obtener más información.
* **Un cliente de Shell seguro (SSH)**: se usa un SSH cliente tooremotely conectar el clúster de HDInsight toohello y ejecutar comandos directamente en clúster de Hola. Para más información, consulte [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
* **Claves SSH (opcionales)**: puede proteger Hola SSH cuenta usada tooconnect toohello clúster con una contraseña o una clave pública. Con una contraseña es más fácil y permite tooget se inicia sin necesidad de toocreate un par de claves pública y privada. Sin embargo, es más seguro utilizar una clave.

> [!NOTE]
> Hola en este documento da por sentado que está utilizando una contraseña.


## <a name="automated-cluster-creation"></a>Creación automatizada del clúster

Puede automatizar la creación de hello de HDInsight R Servers mediante Azure Resource Manager plantillas, Hola SDK y también PowerShell.

* toocreate un servidor de R con una plantilla de administración de recursos de Azure, consulte [implementar un clúster de HDInsight de servidor de R](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).
* toocreate un servidor de R mediante Hola .NET SDK, vea [crear clústeres basados en Linux en HDInsight con hello .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* toodeploy R Server con powershell, consulte el artículo de hello en [crear un servidor de R en HDInsight con PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a>Crear clúster de hello mediante Hola portal de Azure

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).

2. Seleccione **NUEVO** -> **Inteligencia y análisis**, -> **HDInsight**.

    ![Imagen de la creación de un nuevo clúster](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. Hola **creación rápida** rápida, escriba un nombre para el clúster de Hola Hola **nombre del clúster** campo. Si tiene varias suscripciones de Azure, use hello **suscripción** entrada tooselect Hola uno desea toouse.

    ![Opciones de nombre de clúster y suscripción](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. Seleccione **clúster tipo** tooopen hello **configuración de clúster** hoja. En hello **configuración de clúster** hoja, seleccione Hola siguientes opciones:

    * **Tipo de clúster**: R Server
    * **Versión**: versión de Hola select de tooinstall R Server en clúster de Hola. versión de Hola actualmente disponible es ***9.1 de servidor de R (HDI 3.6)***. Notas de la versión para las versiones disponibles de Hola de R Server están disponibles [aquí](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).
    * **Edición de la Comunidad de R Studio para R Server**: esta IDE basadas en el explorador se instala de forma predeterminada en el nodo del borde de Hola. Si prefiere toonot instalarla, a continuación, desactive la casilla de verificación de Hola. Si elige toohave instalan, dirección URL de hello para tener acceso a Hola inicio de sesión RStudio Server se encuentra en una hoja de aplicación de portal para el clúster, una vez que se ha creado.
    * Dejar Hola otras opciones en valores predeterminados de Hola y usar hello **seleccione** toosave Hola clúster tipo de botón.

        ![Captura de pantalla de la hoja del tipo de clúster](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. Escriba un **Nombre de usuario de inicio de sesión del clúster** y una **Contraseña de inicio de sesión del clúster**.

    Especifique un **Nombre de usuario de SSH**. SSH es tooremotely usado conectarse toohello clúster con un **Shell seguro (SSH)** cliente. Puede especificar usuario SSH de hello en este cuadro de diálogo o después de que se haya creado el clúster de hello (en la pestaña de configuración de hello para el clúster de hello). R Server está configurado tooexpect una **nombre de usuario SSH** de "remoteuser".  **Si utiliza un nombre de usuario diferente, debe realizar un paso adicional después de crear el clúster de Hola.**

    Cuadro de hello deje activada para **usar la misma contraseña como inicio de sesión de clúster** toouse **contraseña** como hello tipo de autenticación, a menos que se prefiere el uso de una clave pública.  Necesita un par de claves pública/privada tooaccess R Server en clúster de Hola a través de un cliente como, por ejemplo, RTV, RStudio u otro IDE de escritorio remoto. Si instala Hola edición community de RStudio Server, debe toochoose una contraseña SSH.     

    toocreate y use un par de claves pública y privada, desactive la opción **usar la misma contraseña como inicio de sesión de clúster** y, a continuación, seleccione **clave pública** y haga lo siguiente. Estas instrucciones asumen que dispone de Cygwin con ssh-keygen o equivalente instalado.

    * Generar un par de claves pública/privada Hola desde línea de comandos en su equipo portátil:

        ssh-keygen -t rsa -b 2048

    * Siga Hola prompt tooname un archivo de clave y, a continuación, escriba una frase de contraseña para una mayor seguridad. La pantalla debe ser similar Hola después de imagen:

        ![Línea de comando SSH en Windows](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * Este comando crea un archivo de clave privada y un archivo de clave público en el nombre < private-key-filename > Hola pub, por ejemplo furiosa y furiosa.pub.

        ![Dir SSH](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * A continuación, especifique el archivo de clave pública de hello (&#42;. pub) al asignar HDI credenciales de clúster y por último, confirme su grupo de recursos y región y seleccione **siguiente**.

        ![Hoja Credenciales](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * Cambiar los permisos de archivo de clave privada de hello en su equipo portátil:

        chmod 600 <nombreDeArchivoDeClavePrivada>

   * Use el archivo de clave privada de hello mediante SSH para inicio de sesión remoto:

        ssh –i <private-key-filename> remoteuser@<hostname public ip>

      O bien, como definiciones de Hola de parte de su Hadoop Spark cálculo para R Server en el cliente de Hola. Vea hello **Using Microsoft R Server como un cliente de Hadoop** en la subsección [crear un contexto de proceso para Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).

6. Creación rápida de Hello pasa toohello **almacenamiento** cuenta de almacenamiento de hello hoja tooselect toobe de configuración para la ubicación principal de Hola Hola usado por clúster Hola de sistema de archivos de HDFS. Seleccione una cuenta de Azure Storage nueva o existente o una cuenta de almacenamiento de Data Lake existente.

    - Si selecciona una cuenta de almacenamiento de Azure, se selecciona una cuenta de almacenamiento existente seleccionando **seleccionar una cuenta de almacenamiento** y, a continuación, seleccione cuenta pertinente Hola. Crear una nueva cuenta con hello **crear nuevo** vínculo Hola **seleccionar una cuenta de almacenamiento** sección.

      > [!NOTE]
      > Si selecciona **New** debe especificar un nombre para la nueva cuenta de almacenamiento Hola. Una marca de verificación verde aparece si se acepta el nombre de Hola.

      Hola **contenedor predeterminado** nombre de toohello de los valores predeterminados del clúster de Hola. Deje este valor predeterminado como el valor de Hola.

      Si se ha seleccionado una nueva opción de cuenta de almacenamiento un símbolo del sistema tooselect **ubicación** se especificado tooselect qué región toocreate Hola cuenta de almacenamiento.  

         ![Hoja Origen de datos](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > También se estén seleccionando la ubicación de hello para el origen de datos predeterminado de hello establece la ubicación de Hola Hola del clúster de HDInsight. Hello clúster y forma predeterminada el origen de datos debe Hola misma región.

    - Si desea que toouse un almacén de Data Lake existente, a continuación, seleccione Hola toouse de cuenta de almacenamiento ADLS y agregar clúster hello *agregar* identidad tooyour clúster tooallow toohello en el almacén acceso. Para más información sobre este proceso, consulte [Creación de un clúster de HDInsight con Data Lake Store mediante Azure Portal](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).

    Hola de uso **seleccione** configuración del origen de datos de botón toosave Hola.


7. Hola **resumen** blade, a continuación, muestra toovalidate toda la configuración. Aquí puede cambiar su **tamaño de clúster** toomodify Hola número de servidores en el clúster y hay que especificar ninguno **acciones de Script** desea toorun. A menos que sepa que necesita un clúster mayor, deje el número de Hola de nodos de trabajador en el valor predeterminado es hello `4`. Hola se calcula el costo de clúster de Hola se muestra en la hoja de Hola.

    ![Resumen del clúster](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > Si es necesario, puede cambiar el tamaño de su clúster más adelante a través de hello Portal (**clúster** -> **configuración** -> **escala clúster**) tooincrease o reducir el número de Hola de nodos de trabajador.  Este cambio de tamaño puede ser útil ralentí hacia abajo de clúster de hello cuando no esté en uso, o para agregar las necesidades de capacidad toomeet Hola de tareas más grandes.
   >
   >

   Algunos tookeep factores en cuenta al asignar el tamaño de su clúster, nodos de datos de Hola y el nodo del borde de hello incluyen:  

   * rendimiento de Hola de análisis de R Server distribuidos en Spark sea proporcional toohello número de nodos de trabajador cuando hello es grande.  

   * Hola el rendimiento de análisis de servidor de R es lineal en el tamaño de Hola de los datos que se va a analizar. Por ejemplo:  

     * Para los datos de toomodest pequeños, rendimiento es mejor cuando se analizan en un contexto de proceso local en el nodo del borde de Hola.  Para obtener más información sobre los escenarios de hello en la que Hola local y Spark contextos de proceso funcionan mejor, consulte Opciones de contexto de proceso para el servidor de R en HDInsight.<br>
     * Si debe iniciar sesión en el nodo del borde toohello y ejecuta el script R, a continuación, se ejecutan todos pero hello las funciones ScaleR rx <strong>localmente</strong> en el nodo del borde de Hola. Por lo tanto Hola memoria y número de núcleos del nodo de hello borde debe ajustarse según corresponda. Hola que esto mismo se aplica si usa R Server en HDI como un contexto de proceso remoto desde su portátil.

     ![Hoja Niveles de precios de nodo](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     Hola de uso **seleccione** nodo del botón toosave Hola precios de configuración.

   Observe que también existe el vínculo **Descargar plantilla y parámetros**. Haga clic en este vínculo toodisplay las secuencias de comandos que pueden ser usado tooautomate Hola creación de un clúster con la configuración seleccionada de Hola. Estas secuencias de comandos también están disponibles en hello Azure entrada portal para el clúster una vez que se ha creado.

   > [!NOTE]
   > Tarda algún tiempo para hello clúster toobe creado, normalmente alrededor de 20 minutos. Usar icono hello en el panel de inicio de Hola u Hola **notificaciones** entrada en hello deja de hello página toocheck en proceso de creación de hello.
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a>Conectar tooRStudio Server

Si ha elegido tooinclude edición community de RStudio Server en la instalación, puede tener acceso a inicio de sesión de hello RStudio a través de dos métodos diferentes.

1. Vaya toohello después de la dirección URL (donde **CLUSTERNAME** es Hola nombre del clúster de Hola que ha creado):

    https://**CLUSTERNAME**.azurehdinsight.net/rstudio/

2. Abrir entrada de hello para el clúster en hello portal de Azure, seleccione hello **R Server paneles** vínculo rápido y, a continuación, seleccionando hello **R Studio panel**:

     ![Panel de acceso Hola R studio](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Panel de acceso Hola R studio](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > Independientemente del método hello utilizado, hello primera vez que inicie sesión en necesita tooauthenticate dos veces.  En la primera autenticación hello, proporcionar hello *identificador de usuario de administración de clúster* y *contraseña*. En el segundo mensaje Hola, proporcionar hello *SSH userid* y *contraseña*. Registros subsiguientes inicios solo requieren hello *contraseña SSH* y *userid*.

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a>Conectar el nodo del borde toohello R Server

Conectar visita el nodo del borde de servidor de clúster de HDInsight de hello mediante SSH con el comando hello:

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> Puede encontrar Hola `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` dirección Hola portal de Azure, seleccione el clúster, a continuación, **toda la configuración de** -> **aplicaciones** -> **RServer**. Esto muestra información de extremo de SSH para el nodo del borde de Hola Hola.
>
> ![Imagen de hello SSH extremo para el nodo del borde de Hola](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

Si utiliza un toosecure de contraseña de su cuenta de usuario SSH, son tooenter solicitada se. Si utiliza una clave pública, puede que tenga hello toouse `-i` toospecify parámetro Hola clave privada correspondiente. Por ejemplo:

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Para obtener más información, consulte [conectar tooHDInsight (Hadoop) mediante SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

Una vez conectado, llegan en un símbolo del sistema siguiente toohello similar:

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a>Habilitación de varios usuarios simultáneos

Puede habilitar a varios usuarios simultáneos agregando más usuarios para el nodo del borde hello en qué hello RStudio Comunidad se ejecuta la versión.

Al crear un clúster de HDInsight, es preciso especificar dos usuarios, un usuario HTTP y un usuario SSH:

![Usuario simultáneo 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- **Nombre de usuario de inicio de sesión del clúster**: un usuario HTTP para la autenticación a través de la puerta de enlace de HDInsight de Hola que es usado tooprotect hello HDInsight clústeres que ha creado. Este usuario HTTP es tooaccess usado hello Ambari UI, interfaz de usuario de YARN, así como otros componentes de interfaz de usuario.
- **El nombre de usuario de Secure Shell (SSH)**: un clúster de hello SSH tooaccess de usuario a través de shell seguro. Este usuario es un usuario de hello sistema Linux para todos los nodos principales de hello, nodos de trabajador y nodos de borde. Para poder utilizar tooaccess de shell seguro cualquiera de los nodos de hello en un clúster remoto.

versión de comunidad de R Studio Server de Hello usada en hello Microsoft R Server en clúster de HDInsight tipo acepta únicamente el nombre de usuario de Linux y una contraseña como un mecanismo de inicio de sesión. No admite tokens de paso. Por tanto, si ha creado un nuevo clúster y desea toouse R Studio tooaccess, necesita toolog en dos veces.

- Primero inicie sesión con credenciales de usuario de hello HTTP a través de hello puerta de enlace de HDInsight: 

    ![Usuario simultáneo 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- A continuación, usar toolog de credenciales de usuario SSH de hello en tooRStudio:
  
    ![Usuario simultáneo 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

Actualmente, una cuenta de usuario SSH solo se puede crear al aprovisionar un clúster de HDInsight. Para clústeres de varios usuarios tooaccess Microsoft R Server en HDInsight tooenable necesitamos toocreate usuarios adicionales en hello sistema Linux.

Porque RStudio Comunidad de servidor se ejecuta en el nodo del borde del clúster de hello, hay varios pasos a continuación:

1. Usar toolog de usuario SSH de hello creado en el nodo del borde toohello
2. Agregar más usuarios de Linux al nodo perimetral.
3. Utilice la versión de comunidad RStudio con creado por el usuario Hola

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a>Paso 1: Utilizar toolog de usuario SSH de hello creado en el nodo del borde toohello

Descargar cualquier herramienta SSH (como Putty) y usar hello toolog de usuario SSH existente en. A continuación, siga las instrucciones de hello proporcionadas en [conectar tooHDInsight (Hadoop) mediante SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess Hola nodo del borde. dirección de nodo del borde Hola para R Server en clúster de HDInsight es: *clustername-ed-ssh.azurehdinsight.net*


### <a name="step-2-add-more-linux-users-in-edge-node"></a>Paso 2: Adición de más usuarios de Linux al nodo perimetral

tooadd un nodo del borde usuario toohello, ejecutar comandos de hello:

    sudo useradd yournewusername -m
    sudo passwd yourusername

Debería ver Hola después de elementos devueltos: 

![Usuario simultáneo 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

Cuando se le solicite "contraseña actual de Kerberos:", simplemente presione las teclas **ENTRAR** tooignore lo. Hola `-m` opción `useradd` comando indica que el sistema de hello creará una carpeta particular de usuario de hello, que es necesario para la versión de comunidad RStudio.


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a>Paso 3: Versión Use RStudio Comunidad con creado por el usuario Hola

Usar Hola creado por el usuario toolog en tooRStudio:

![Usuario simultáneo 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

Observe que RStudio indica que está usando el nuevo usuario de hello (aquí, por ejemplo, *sshuser6*) toolog en clúster de hello: 

![Usuario simultáneo 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

También puede iniciar sesión con credenciales de hello original (de forma predeterminada, es *sshuser*) simultáneamente en otra ventana del explorador.

Puede enviar un trabajo mediante las funciones de scaleR. Este es un ejemplo de Hola comandos usados toorun un trabajo:

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


Tenga en cuenta que los trabajos de hello enviados en diferentes nombres de usuario en la interfaz de usuario de YARN:

![Usuario simultáneo 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

Tenga en cuenta también que Hola recién agregado usuarios no tienen privilegios de raíz en el sistema Linux, pero ha Hola mismo tener acceso a archivos de Hola de tooall en el almacenamiento remoto de HDFS y WASB Hola.


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a>Usar la consola de hello R

1. Desde la sesión de SSH de hello, use Hola después de la consola de comandos toostart Hola R:  

        R

2. Debería ver resultados similares toohello siguiente:
    
    R versión 3.2.2 (2015-08-14)--"Fire Safety" Copyright (C) 2015 hello R Foundation para la plataforma de informática en estadística: x86_64 pc linux-gnu (64 bits)

    R es un software gratuito y NO INCLUYE NINGUNA GARANTÍA.
    Son tooredistribute bienvenida en determinadas condiciones.
    Escriba 'license()' o 'licence()' para obtener más información de distribución.

    Compatibilidad con lenguaje natural siempre que se ejecute en una configuración regional en inglés

    R es un proyecto de colaboración con muchos colaboradores.
    Escriba 'contributors()' para obtener más información y 'citation()' en cómo toocite R o R paquetes en las publicaciones.

    Escriba 'demo()' para algunos demostraciones, 'help()' para obtener ayuda en línea o 'help.start()' para un toohelp de interfaz de explorador HTML.
    Escriba 'q()' tooquit R.

    Microsoft R Server versión 8.0: una distribución mejorada de los paquetes de Microsoft R Copyright (C) 2016 Microsoft Corporation

    Escriba 'readme()' para leer las notas de la versión.
    >

3. De hello `>` símbolo del sistema, puede escribir código de R. Servidor de R incluye paquetes que le permiten tooeasily interactúan con Hadoop y ejecutar cálculos distribuidos. Por ejemplo, usar hello después de raíz de comando tooview Hola Hola predeterminado de sistema de archivos para el clúster de HDInsight de hello:

    rxHadoopListFiles("/")

4. También puede usar el direccionamiento de estilo de hello WASB.

    rxHadoopListFiles("wasb:///")


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a>Uso de R Server en HDI desde una instancia remota de Microsoft R Server o Microsoft R Client

Es posible tooset el contexto de proceso de Hadoop Spark de HDI de toohello de acceso desde una instancia remota de Microsoft R Server o Microsoft R cliente que se ejecuta en un escritorio o portátil. Vea **Using Microsoft R Server como un cliente de Hadoop** subsección Hola [crear un contexto de proceso para Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md). toodo por lo tanto, necesita hello toospecify siguientes opciones al definir el contexto de proceso de hello RxSpark en su equipo portátil: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches y sshProfileScript. Por ejemplo:


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a>Usar un contexto de proceso

Un contexto de proceso le permite toocontrol, si se debe realizar localmente en el nodo del borde de Hola o se distribuyen por los nodos en clúster de HDInsight de Hola Hola cálculo.

1. Desde la consola de hello R (en una sesión de SSH) o el servidor de RStudio, usar hello después de datos de ejemplo de código tooload en el almacenamiento de saludo predeterminado de HDInsight:

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. A continuación, vamos a crear alguna información de datos y definir dos orígenes de datos de modo que podemos trabajar con datos de Hola.

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. Vamos a ejecutar una regresión logística basados en datos de hello mediante el contexto de proceso local Hola.

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    Debería ver resultados que termina por toohello similares de las líneas siguientes:

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. A continuación, vamos a ejecutar Hola mismo regresión logística con contexto de Spark Hola. contexto de Spark Hola distribuye Hola procesar a través de todos los nodos de trabajador de hello en clúster de HDInsight Hola.

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > También puede utilizar el cálculo de toodistribute MapReduce en nodos de clúster. Para más información sobre el contexto de proceso, consulte [Opciones de contexto de proceso para R Server en HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).


## <a name="distribute-r-code-toomultiple-nodes"></a>Distribuir los nodos de toomultiple de código de R

Con el servidor de R, fácilmente puede tomar código existente, R y ejecutar a través de varios nodos de clúster de hello mediante `rxExec`. Esta función es útil cuando se realiza un barrido de parámetros o simulaciones. Hola código siguiente es un ejemplo de cómo toouse `rxExec`:

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

Si todavía utilizas Hola Spark o contexto de MapReduce, este comando devuelve un valor nodename Hola para nodos de trabajador de hello ese código de hello `(Sys.info()["nodename"])` se ejecuta en. Por ejemplo, en un clúster de cuatro nodos, se espera tooreceive salida siguiente de toohello similar:

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="accessing-data-in-hive-and-parquet"></a>Acceso a datos en Hive y Parquet

Una característica disponible en R Server 9.1 permite toodata de acceso directo de Hive y Parquet para su uso por las funciones ScaleR en contexto de proceso de hello Spark. Estas capacidades están disponibles a través de la nueva ScaleR origen de datos funciona denominados RxHiveData y RxParquetData que funcionan a través del uso de datos de Spark SQL tooload directamente en una trama de datos de Spark para el análisis por ScaleR.  

Hola siguiente código proporciona ejemplos de código en el uso de las nuevas funciones de hello:

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


Para obtener más información sobre el uso de estas nuevas funciones, vea Hola ayuda en pantalla de R Server mediante el uso de hello `?RxHivedata` y `?RxParquetData` comandos.  


## <a name="install-additional-r-packages-on-hello-edge-node"></a>Instalar paquetes de R adicionales en el nodo del borde de Hola

Si desea que tooinstall paquetes de R adicionales en el nodo del borde de hello, puede usar `install.packages()` directamente desde Hola consola de R cuando toohello conectado arista nodo a través de SSH. Sin embargo, si necesita tooinstall paquetes de R en nodos de trabajador de Hola de clúster de hello, debe usar una acción de secuencia de comandos.

Acciones de script son scripts de Bash que usa toomake configuración cambios toohello HDInsight clúster o tooinstall software adicional, como paquetes de R adicionales. paquetes adicionales de tooinstall mediante una acción de secuencia de comandos, utilice Hola pasos:

> [!IMPORTANT]
> Uso de paquetes de R adicionales de acciones de Script tooinstall sólo puede utilizarse una vez creado el clúster de Hola. No utilice este procedimiento durante la creación del clúster, tal y como script de Hola se basa en R Server está completamente instalado y configurado.
>
>

1. De hello [portal de Azure](https://portal.azure.com), seleccione el servidor de R en clúster de HDInsight.

2. De hello **configuración** hoja, seleccione **acciones de Script** y, a continuación, **Enviar nueva** toosubmit una nueva acción de secuencia de comandos.

   ![Imagen de la hoja Acciones de script](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. De hello **acción de secuencia de comandos de envío** hoja, proporcionar Hola siguiente información:

   * **Nombre**: descriptivo nombre tooidentify esta secuencia de comandos

   * **URI de script de Bash**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`

   * **Head** (Principal): este elemento debe estar **desactivado**.

   * **Worker** (De trabajo): este elemento debe estar **activado**.

   * **Edge nodes** (Nodos perimetrales): este elemento debe estar **desactivado**.

   * **Zookeeper**: este elemento debe estar **activado**.

   * **Parámetros**: Hola R paquetes toobe instalado. Por ejemplo: `bitops stringr arules`

   * **Persist this script...** (Continuar con este script…): debe estar **activado**.  

   > [!NOTE]
   > 1. De forma predeterminada, se instalan todos los paquetes de R desde una instantánea del repositorio de Microsoft MRAN Hola coherente con la versión de Hola de R Server que se ha instalado. Si desea que tooinstall las versiones más recientes de los paquetes, no hay algunos riesgos de incompatibilidad. Sin embargo este tipo de instalación es posible mediante la especificación de `useCRAN` como Hola primer elemento del paquete de Hola de lista de, por ejemplo `useCRAN bitops, stringr, arules`.  
   > 2. Algunos paquetes de R requieren otras bibliotecas de sistema de Linux. Para mayor comodidad, nos hemos preinstalado dependencias Hola necesarios Hola top 100 más populares paquetes de R. Sin embargo, si paquetes de R de hello que instalar requieren bibliotecas aparte de estos, a continuación, debe descargar el script de base de hello usada aquí y agregar pasos tooinstall Hola sistema bibliotecas. Debe a continuación carga Hola modificar script tooa público blob contenedor de almacenamiento de Azure y usar paquetes de hello modificar script tooinstall Hola.
   >    Para más información sobre cómo desarrollar acciones de script, consulte [Desarrollo de acciones de script](hdinsight-hadoop-script-actions-linux.md).  
   >
   >

   ![Agregar una Acción de script](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. Seleccione **crear** secuencia de comandos de toorun Hola. Una vez completado el script de Hola, paquetes de saludo R están disponibles en todos los nodos de trabajador.


## <a name="using-microsoft-r-server-operationalization"></a>Uso de la operacionalización de Microsoft R Server

Una vez completado el modelado de datos, puede poner las predicciones de hello modelo toomake. tooconfigure de puesta en marcha Microsoft R Server, lleve a cabo Hola pasos:

En primer lugar, ssh en el nodo del borde de Hola. Por ejemplo, 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Después de utilizar ssh, cambie el directorio para la versión pertinente de Hola y sudo Hola dotnet dll: 

- Para Microsoft R Server 9.1:

    cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll

- Para Microsoft R Server 9.0:

    cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll

puesta en marcha tooconfigure Microsoft R Server con una configuración de un solo cuadro Hola siguientes:

1. Seleccione “Configure R Server for Operationalization” (Configurar R Server para operacionalización)
2. Seleccione “A. One-box (web + compute nodes)” [One-box (web y nodos de proceso)]
3. Escriba una contraseña para hello **administración** usuario

![operacionalización one box](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

Como paso opcional, puede realizar comprobaciones de diagnóstico mediante la ejecución de una prueba de diagnóstico tal y como se muestra a continuación:

1. Seleccione “6. Ejecutar pruebas de diagnóstico”
2. Seleccione “A. Configuración de pruebas”
3. Escriba el nombre de usuario = "admin" y la contraseña del paso de configuración anterior
4. Confirme el estado general = pass
5. Utilidad de administración de Hola de salida
6. Salga de SSH

![Diagnóstico de operacionalización](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
>**Retrasos prolongados al consumir el servicio web en Spark**
>
>Si se producen retrasos prolongados al intentar tooconsume un servicio web creado con las funciones de mrsdeploy en un contexto de proceso Spark, deberá tooadd algunas carpetas que faltan. Hola aplicación Spark pertenece el usuario tooa denominado '*rserve2*' cada vez que se invoque desde un servicio web mediante las funciones de mrsdeploy. toowork resolver este problema:

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


En esta fase, la configuración de hello para la puesta en marcha está completa. Ahora puede usar hello 'mrsdeploy' en su toohello de tooconnect RClient puesta en marcha en el nodo del borde del paquete y empezar a usar sus características como [la ejecución remota de](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) y [servicios web](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette). Dependiendo de si el clúster se configura en una red virtual o no, debe tooset de puerto de túnel hacia delante a través de inicio de sesión SSH. Hello siguientes secciones se explica cómo tooset seguridad este túnel.

### <a name="rserver-cluster-on-virtual-network"></a>RServer Cluster en una red virtual

Asegúrese de que permitir el tráfico a través del nodo del puerto 12800 toohello borde. De este modo, puede usar la característica de puesta en marcha de hello borde nodo tooconnect toohello.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


Si hello `remoteLogin()` no se puede conectar el nodo del borde toohello, pero puede que el nodo del borde SSH toohello, es necesario tooverify si se ha establecido el tráfico de tooallow de regla de hello en el puerto 12800 correctamente o no. Si continúa el problema de hello tooface, puede solucionarlo mediante la configuración de puerto de túnel hacia delante a través de SSH. Para obtener instrucciones, consulte Hola pasos de la sección.

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a>RServer Cluster no configurado en una red virtual

Si el clúster no está configurado en la red virtual o si tiene problemas con la conectividad a través de la red virtual, puede utilizar la tunelización de reenvío del puerto de SSH:

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

En Putty, también se puede configurar.

![conexión ssh de putty](./media/hdinsight-hadoop-r-server-get-started/putty.png)

Una vez que la sesión SSH está activa, el tráfico del puerto de su equipo 12800 Hola se reenvía el puerto del nodo del borde de toohello 12800 a través de la sesión de SSH. Asegúrese de utilizar `127.0.0.1:12800` en el método `remoteLogin()`. Esto se registra en la puesta en marcha del nodo del borde de toohello a través de reenvío de puerto.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a>¿Cómo tooscale Microsoft R Server puesta en marcha de proceso nodos en nodos de trabajo de HDInsight

### <a name="decommission-hello-worker-nodes"></a>Retirada de nodos de trabajador de Hola

Microsoft R Server no se administra actualmente mediante Yarn. Si los nodos de trabajador de hello no están dado de baja, hello Yarn el Administrador de recursos no funcionará según lo previsto porque no tendrá constancia de recursos de hello utilizados por el servidor de Hola. En orden tooavoid esta situación, se recomienda retirada nodos de trabajador de hello antes de escalar horizontalmente los nodos de proceso de Hola.

Nodos de trabajador de toodecommissioning de pasos:

* Inicie sesión en la consola de Ambari del clúster tooHDI y haga clic en la ficha "hosts"
* Seleccionar nodos de trabajador (toobe dado de baja), haga clic en "Acciones" > "Hosts seleccionado" > "Hosts" > haga clic en "Activar el modo de mantenimiento de ON". Por ejemplo, hemos seleccionado toodecommission wn3 y wn4 en hello después de la imagen.  

   ![retirar nodos de trabajo](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* Seleccione **Acciones** > **Hosts seleccionados** > **DataNodes** > haga clic en **Retirar**
* Seleccione **Acciones** > **Hosts seleccionados** > **NodeManagers** > haga clic en **Retirar**
* Seleccione **Acciones** > **Hosts seleccionados** > **DataNodes** > haga clic en **Detener**
* Seleccione **Acciones** > **Hosts seleccionados** > **NodeManagers** > haga clic en **Detener**
* Seleccione **Acciones** > **Hosts seleccionados** > **Hosts** > haga clic en **Detener todos los componentes**
* Anule la selección de nodos de trabajador de Hola y seleccione los nodos principales de Hola
* Seleccione **Acciones** > **Hosts seleccionados** > "**Hosts** > **Reiniciar todos los componentes**

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a>Configuración de los nodos de proceso en cada nodo de trabajo retirado

1. SSH en cada nodo de trabajo retirado.
2. Ejecute la utilidad de administración mediante `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.
3. Escriba "1" tooselect opción "Configurar R Server para la puesta en marcha".
4. Especifique la opción de "c" tooselect "C." Nodo de proceso". Esto configura el nodo de proceso de Hola en el nodo de trabajo Hola.
5. Utilidad de administración de hello de salida.

### <a name="add-compute-nodes-details-on-web-node"></a>Incorporación de detalles de nodos de proceso en el nodo web

Una vez que se han configurado todos los nodos de trabajo retirados toorun nodo de proceso, vuelven a estar en el nodo del borde de Hola y agregar direcciones IP de los nodos de trabajo retirados en configuración del nodo de hello Microsoft R Server web:

* SSH en el nodo del borde de Hola.
* Ejecute `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.
* Busque la sección "URI" Hola y agregue la IP del nodo de trabajo y los detalles de puerto.

    ![línea de comandos para retirar nodos de trabajo](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a>Solución de problemas

Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).


## <a name="next-steps"></a>Pasos siguientes

Ahora debe comprender cómo toocreate un nuevo clúster de HDInsight que incluye los conceptos básicos de hello y R Server Hola del uso Hola consola de R desde una sesión de SSH. Hello en los temas siguientes se explican otras maneras de administrar y trabajar con R Server en HDInsight:

* [Agregar servidor RStudio tooHDInsight (si no se instala durante la creación del clúster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Opciones de contexto de proceso para R Server en HDInsight (versión preliminar)](hdinsight-hadoop-r-server-compute-contexts.md)
* [Opciones de Azure Storage para R Server en HDInsight](hdinsight-hadoop-r-server-storage.md)
