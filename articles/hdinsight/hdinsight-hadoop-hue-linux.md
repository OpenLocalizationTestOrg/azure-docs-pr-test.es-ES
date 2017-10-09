---
title: "aaaHue con Hadoop en clústeres basados en HDInsight Linux - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooinstall matiz en HDInsight de clústeres y utilice túnel tooroute Hola solicitudes tooHue. Usar el almacenamiento de toobrowse de matiz y ejecutar Pig o Hive."
keywords: matiz hadoop
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 9e57fcca-e26c-479d-a745-7b80a9290447
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: f086cbad2a90cc6903fbfccbf4a6be44f8999d07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-hue-on-hdinsight-hadoop-clusters"></a>Instalación y uso de Hue en clústeres de Hadoop para HDInsight

Obtenga información acerca de cómo tooinstall matiz en HDInsight de clústeres y utilice túnel tooroute Hola solicitudes tooHue.

> [!IMPORTANT]
> pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="what-is-hue"></a>¿Qué es Hue?
El matiz es que un conjunto de aplicaciones Web utiliza toointeract con un clúster de Hadoop. Puede usar el matiz toobrowse Hola almacenamiento asociado a un clúster de Hadoop (WASB, en caso de hello de clústeres de HDInsight), ejecutar trabajos de Hive y scripts de Pig y así sucesivamente. Hello componentes siguientes están disponibles con las instalaciones de matiz en un clúster de Hadoop de HDInsight.

* Editor Beeswax de Hive
* Pig
* Administrador de la tienda de metadatos
* Oozie
* FileBrowser (que se comunica el contenedor predeterminado de tooWASB)
* Explorador web

> [!WARNING]
> Componentes suministrados con clúster de HDInsight de hello son totalmente compatibles y Microsoft Support le ayudarán tooisolate y resolver los problemas relacionados toothese componentes.
>
> Componentes personalizados reciben soporte comercialmente razonable toohelp toofurther solucionar el problema de Hola. Esto podría producir en resolver el problema de hello ni pedir que tooengage canales disponibles para hello abrir tecnologías de origen donde se encuentra la amplia experiencia para que la tecnología. Por ejemplo, hay diversos sitios de la comunidad que se pueden usar, como el [foro de MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Los proyectos de Apache también tienen sitios de proyecto en [http://apache.org](http://apache.org) (por ejemplo, [Hadoop](http://hadoop.apache.org/)).
>
>

## <a name="install-hue-using-script-actions"></a>Instalación de Hue mediante acciones de script

Hola script tooinstall matiz en un clúster de HDInsight basados en Linux está disponible en https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. Puede usar este tooinstall script matiz en clústeres con Blobs de almacenamiento de Azure (WASB) o almacén de Azure Data Lake como almacenamiento predeterminado.

Esta sección proporciona instrucciones sobre cómo toouse Hola script al aprovisionar el clúster de hello mediante Hola portal de Azure.

> [!NOTE]
> Azure PowerShell, Hola CLI de Azure, hello HDInsight .NET SDK o plantillas del Administrador de recursos de Azure también pueden ser utilizados tooapply acciones de script. También puede aplicar tooalready de acciones de script clústeres en ejecución. Para obtener más información, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster-linux.md).
>
>

1. Iniciar el aprovisionamiento de un clúster mediante el uso de pasos de hello en [clústeres de HDInsight de aprovisionar en Linux](hdinsight-hadoop-provision-linux-clusters.md), pero no complete el aprovisionamiento.

   > [!NOTE]
   > clústeres de matiz tooinstall en HDInsight, hello tamaño recomendado de nodo principal es al menos A4 (8 núcleos, 14 GB de memoria).
   >
   >
2. En hello **configuración opcional** hoja, seleccione **acciones de Script**y proporcionar información de hello tal y como se muestra a continuación:

    ![Proporcionar parámetros de acción de script para Hue](./media/hdinsight-hadoop-hue-linux/hue-script-action.png "Proporcionar parámetros de acción de script para Hue")

   * **NOMBRE**: escriba un nombre descriptivo para la acción de secuencia de comandos de Hola.
   * **URI DE SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
   * **PRINCIPAL**: active esta opción.
   * **TRABAJO**: déjelo en blanco.
   * **ZOOKEEPER**: déjelo en blanco.
   * **PARÁMETROS**: déjelo en blanco.
3. Final de Hola de hello **acciones de Script**, usar hello **seleccione** configuración del botón toosave Hola. Por último, utilice hello **seleccione** situado en la parte inferior de Hola de hello **configuración opcional** información de configuración opcional de hoja toosave Hola.
4. Continuar aprovisionamiento clúster Hola tal y como se describe en [clústeres de HDInsight de aprovisionar en Linux](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="use-hue-with-hdinsight-clusters"></a>Use Hue con clústeres de HDInsight

Túnel SSH es Hola única manera tooaccess matiz en clúster de Hola una vez que se está ejecutando. Protocolo de túnel a través de SSH permite Hola tráfico toogo directamente el nodo principal de toohello de hello clúster donde se está ejecutando el matiz. Después de que el clúster de hello haya terminado el aprovisionamiento, utilice Hola siguiendo los pasos toouse matiz en un clúster de HDInsight Linux.

> [!NOTE]
> Se recomienda usar Firefox web explorador toofollow Hola estas instrucciones.
>
>

1. Usar información de hello en [tooaccess uso de SSH túnel Ambari web de interfaz de usuario, ResourceManager, JobHistory, NameNode, Oozie y otra interfaz de usuario web](hdinsight-linux-ambari-ssh-tunnel.md) toocreate un SSH de túnel desde el clúster de HDInsight de toohello de sistema de cliente y, a continuación, configurar el Web Explorador toouse Hola túnel SSH como un proxy.

2. Una vez que haya creado un túnel SSH y configurado el tráfico de tooproxy de explorador a través de él, debe buscar el nombre de host de hello del nodo principal de hello principal. Puede hacerlo mediante la conexión de clúster toohello mediante SSH en el puerto 22. Por ejemplo, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net` donde **nombre de usuario** es el nombre de usuario SSH y **CLUSTERNAME** es Hola nombre del clúster.

    Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Una vez conectado, use Hola después de nombre de dominio completo de comando tooobtain Hola de nodo principal de hello principal:

        hostname -f

    Esto devolverá un nombre similar toohello detrás:

        hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

    Esto es nombre de host de hello del nodo principal primario de Hola donde el sitio Web de matiz Hola se encuentra.
4. Usar el portal de matiz de Hola de hello explorador tooopen en http://HOSTNAME:8888. Reemplace el nombre de host por nombre de hello obtenido en el paso anterior de Hola.

   > [!NOTE]
   > Al iniciar sesión para hello primera vez, se iniciará solicitada toocreate un toolog de cuenta en el portal de matiz toohello. credenciales de Hola que especifique aquí serán portal toohello limitado y no están relacionadas toohello administrador o credenciales de usuario SSH que especificó al clúster de hello aprovisionar.
   >
   >

    ![Portal de matiz de inicio de sesión toohello](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-login.png "especificar credenciales para el portal de matiz")

### <a name="run-a-hive-query"></a>Ejecución de una consulta de Hive
1. En el portal de matiz de hello, haga clic en **editores de consultas**y, a continuación, haga clic en **Hive** editor de subárboles tooopen Hola.

    ![Uso de Hive](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-use-hive.png "Uso de Hive")
2. En hello **Assist** ficha **base de datos**, debería ver **hivesampletable**. Se trata de una tabla de ejemplo que se incluye con todos los clústeres de Hadoop en HDInsight. Escriba una consulta de ejemplo en el panel derecho de Hola y ver el resultado de hello en hello **resultados** ficha Panel de Hola a continuación, como se muestra en la captura de pantalla de Hola.

    ![Ejecución de consultas de Hive](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-hive-query.png "Ejecución de consultas de Hive")

    También puede usar hello **gráfico** ficha toosee una representación visual del resultado de hello.

### <a name="browse-hello-cluster-storage"></a>Buscar en almacenamiento de clúster de Hola
1. En el portal de matiz de hello, haga clic en **Explorador de archivos** en la esquina superior derecha de Hola de barra de menús de Hola.
2. De forma predeterminada se abre el Explorador de archivos de hello en hello **/usuario/myuser** directory. Haga clic en la barra diagonal justo antes de directorio de usuario de hello en toogo toohello raíz de hello ruta de acceso del contenedor de almacenamiento de Azure Hola asociado con el clúster de Hola Hola.

    ![Uso del explorador de archivos](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-file-browser.png "Uso del explorador de archivos")
3. Haga doble clic en un archivo o carpeta toosee hello las operaciones disponibles. Hola de uso **cargar** botón en el directorio actual de hello esquina derecha tooupload archivos toohello. Hola de uso **New** botón toocreate nuevos archivos o directorios.

> [!NOTE]
> Explorador de archivos de matiz Hola solo puede mostrar contenido de Hola Hola predeterminado del contenedor de asociado con clúster de HDInsight de Hola. Cualquier adicionales cuentas/contenedores de almacenamiento que ha asociado con el clúster de hello no será accesibles mediante el Explorador de archivos de Hola. Sin embargo, contenedores adicionales Hola asociados Hola clúster siempre serán accesibles para los trabajos de Hive de Hola. Por ejemplo, si escribe el comando de hello `dfs -ls wasb://newcontainer@mystore.blob.core.windows.net` en el editor de Hive hello, puede ver contenido de Hola de contenedores adicionales también. En este comando, **newcontainer** no es contenedor de hello predeterminado asociado a un clúster.
>
>

## <a name="important-considerations"></a>Consideraciones importantes
1. Hola script utilizado tooinstall matiz lo instala únicamente en el nodo principal en principal del clúster de Hola Hola.

2. Durante la instalación, se reinician varios servicios de Hadoop (HDFS, YARN, MR2, Oozie) para actualizar la configuración de Hola. Cuando finalice el script de Hola, instalar el matiz, puede tardar algún tiempo para otro toostart de servicios de Hadoop. Esto podría afectar inicialmente al rendimiento de Hue. Una vez que todos los servicios se inician, la funcionalidad de Hue será total.
3. Matiz no entiende Tez trabajos, que es el valor predeterminado actual de Hola de Hive. Si desea toouse MapReduce como Hola motor de ejecución de Hive, actualice Hola Hola de toouse de secuencia de comandos siguiente comando en el script:

        set hive.execution.engine=mr;

4. Con los clústeres de Linux, puede tener un escenario donde los servicios están ejecutándose en nodo principal primario de hello mientras Hola, Administrador de recursos podría ejecutarse en hello secundaria. Este escenario podría provocar errores (se muestra a continuación) cuando se utiliza detalles de tooview de matiz de trabajos de ejecución en clúster de Hola. Sin embargo, puede ver detalles del trabajo hello cuando se haya completado el trabajo de Hola.

   ![Error en el portal de Hue](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-error.png "Error en el portal de Hue")

   Se trata de vencimiento tooa un problema conocido. Como alternativa, modificar Ambari para que hello active el Administrador de recursos también se ejecuta en el nodo principal de hello principal.
5. Hue entiende WebHDFS, mientras que los clústeres de HDInsight usan Almacenamiento de Azure mediante `wasb://`. Por lo tanto, se utiliza con la acción de secuencia de comandos de script personalizado de hello instala WebWasb, que es un servicio compatible con WebHDFS para hablar tooWASB. Por lo tanto, aunque el portal de matiz Hola dice HDFS en lugares (al igual que cuando mueve el mouse sobre hello **Explorador de archivos**), se debe interpretar como WASB.

## <a name="next-steps"></a>Pasos siguientes
* [Instalación de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install-linux.md). Utilice tooinstall de personalización de clúster de clústeres de Giraph en Hadoop de HDInsight. Giraph permite gráfico tooperform Hadoop de procesamiento y se puede utilizar con HDInsight de Azure.
* [Instalación de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install-linux.md). Utilice tooinstall de personalización de clúster de clústeres de Solr en Hadoop de HDInsight. Solr permite operaciones de búsqueda eficaces tooperform en los datos almacenados.
* [Instalación de R en clústeres de HDInsight](hdinsight-hadoop-r-scripts-linux.md). Usar clúster personalización tooinstall R en clústeres de Hadoop de HDInsight. R es un entorno y lenguaje de código abierto para computación estadística. Proporciona cientos de de funciones estadísticas integradas y su propio lenguaje de programación que combina aspectos de la programación funcional y orientada a objetos. También proporciona amplias capacidades gráficas.

[powershell-install-configure]: install-configure-powershell-linux.md
[hdinsight-provision]: hdinsight-provision-clusters-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
