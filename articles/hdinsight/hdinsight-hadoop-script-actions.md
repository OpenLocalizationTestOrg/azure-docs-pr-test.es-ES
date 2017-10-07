---
title: "desarrollo de la acción con HDInsight - Azure aaaScript | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocustomize Hadoop clústeres con la acción de secuencia de comandos. Acción de secuencia de comandos puede ser usado tooinstall software adicional con una configuración de Hola de clúster o toochange de Hadoop de las aplicaciones instaladas en un clúster."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 836d68a8-8b21-4d69-8b61-281a7fe67f21
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 4fc3a389df8a003f7129ab00b4cd9bc7ad81a419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-script-action-scripts-for-hdinsight-windows-based-clusters"></a>Desarrollo de acciones de script para clústeres basados en Windows de HDInsight
Obtenga información acerca de cómo toowrite acción de secuencia de comandos de las secuencias de comandos para HDInsight. Para obtener más información acerca del uso de acciones de script, vea [Personalización de un clúster de HDInsight mediante la acción de script](hdinsight-hadoop-customize-cluster.md). Hola mismo artículo escrito para clústeres de HDInsight basados en Linux, encontrará [secuencias de comandos de acción de secuencia de comandos de desarrollar para HDInsight](hdinsight-hadoop-script-actions-linux.md).



> [!IMPORTANT]
> Hola pasos de este trabajo sólo de documento para clústeres de HDInsight basados en Windows. HDInsight solo está disponible en Windows en versiones inferiores a la 3.4. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Para obtener información sobre el uso de las acciones de script con clústeres basados en Linux, consulte [Desarrollo de la acción de script con HDInsight (Linux)](hdinsight-hadoop-script-actions-linux.md).
>
>



Acción de secuencia de comandos puede ser usado tooinstall software adicional con una configuración de Hola de clúster o toochange de Hadoop de las aplicaciones instaladas en un clúster. Las acciones de script son scripts que se ejecutan en nodos de clúster de hello cuando se implementan clústeres de HDInsight, y se ejecutan una vez que los nodos de clúster de hello completar configuración de HDInsight. Una acción de secuencia de comandos se ejecuta con privilegios de cuenta de administrador de sistema y proporciona nodos de clúster de toohello de derechos de acceso completo. Cada clúster puede proporcionarse con una lista de toobe de acciones de script ejecutado en orden de hello en el que se especifican.

> [!NOTE]
> Si experimenta Hola mensaje de error siguiente:
>
> System.Management.Automation.CommandNotFoundException; ExceptionMessage: Hola término 'Guardar-HDIFile' no se reconoce como nombre de Hola de cmdlet, función, archivo de script o programa ejecutable. Revisar la ortografía de hello del nombre de hello, o si incluyó una ruta de acceso, compruebe que dicha ruta de acceso de hello es correcta e inténtelo de nuevo.
> Es porque no incluyen métodos auxiliares de Hola.  Vea [Métodos auxiliares para scripts personalizados](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).
>
>

## <a name="sample-scripts"></a>Scripts de ejemplo
Para crear clústeres de HDInsight en el sistema operativo Windows, Hola acción de secuencia de comandos es el script de PowerShell de Azure. Hello script siguiente es un ejemplo para configurar los archivos de configuración de sitio de hello:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    param (
        [parameter(Mandatory)][string] $ConfigFileName,
        [parameter(Mandatory)][string] $Name,
        [parameter(Mandatory)][string] $Value,
        [parameter()][string] $Description
    )

    if (!$Description) {
        $Description = ""
    }

    $hdiConfigFiles = @{
        "hive-site.xml" = "$env:HIVE_HOME\conf\hive-site.xml";
        "core-site.xml" = "$env:HADOOP_HOME\etc\hadoop\core-site.xml";
        "hdfs-site.xml" = "$env:HADOOP_HOME\etc\hadoop\hdfs-site.xml";
        "mapred-site.xml" = "$env:HADOOP_HOME\etc\hadoop\mapred-site.xml";
        "yarn-site.xml" = "$env:HADOOP_HOME\etc\hadoop\yarn-site.xml"
    }

    if (!($hdiConfigFiles[$ConfigFileName])) {
        Write-HDILog "Unable tooconfigure $ConfigFileName because it is not part of hello HDI configuration files."
        return
    }

    [xml]$configFile = Get-Content $hdiConfigFiles[$ConfigFileName]

    $existingproperty = $configFile.configuration.property | where {$_.Name -eq $Name}

    if ($existingproperty) {
        $existingproperty.Value = $Value
        $existingproperty.Description = $Description
    } else {
        $newproperty = @($configFile.configuration.property)[0].Clone()
        $newproperty.Name = $Name
        $newproperty.Value = $Value
        $newproperty.Description = $Description
        $configFile.configuration.AppendChild($newproperty)
    }

    $configFile.Save($hdiConfigFiles[$ConfigFileName])

    Write-HDILog "$configFileName has been configured."

script de Hola toma cuatro parámetros, nombre de archivo de configuración de hello, propiedad de Hola que desee toomodify, valor de Hola que desee tooset y una descripción. Por ejemplo:

    hive-site.xml hive.metastore.client.socket.timeout 90

Estos parámetros se establece hello hive.metastore.client.socket.timeout valor too90 en el archivo de hive-site.xml hello.  valor de Hello predeterminado es 60 segundos.

Este script de ejemplo se puede encontrar también en [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).

HDInsight proporciona varias secuencias de comandos tooinstall de componentes adicionales en clústeres de HDInsight:

| Nombre | Script |
| --- | --- |
| **Instalar Spark** |https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1. Vea [Instalación y uso de Spark en clústeres de HDInsight][hdinsight-install-spark]. |
| **Instalar R** |https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1. Consulte [Instalación y uso de R en clústeres de HDInsight][hdinsight-r-scripts]. |
| **Instalar Solr** |https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1. Vea [Instalación y uso de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install.md). |
| - **Instalar Giraph** |https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1. Vea [Instalación y uso de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install.md). |

Acción de secuencia de comandos se puede implementar de hello portal de Azure, Azure PowerShell o mediante el uso de Hola HDInsight .NET SDK.  Para obtener más información, consulte [Personalización de un clúster de HDInsight mediante la acción de script][hdinsight-cluster-customize].

> [!NOTE]
> las secuencias de comandos de ejemplo de Hola trabajar solo con la versión de clúster de HDInsight 3.1 o posterior. Para obtener más información acerca de las versiones de clústeres de HDInsight, consulte las [versiones de clústeres de HDInsight](hdinsight-component-versioning.md).
>
>

## <a name="helper-methods-for-custom-scripts"></a>Métodos auxiliares para scripts personalizados
Los métodos auxiliares de la acción de script son utilidades que puede usar al escribir scripts personalizados. Estos métodos se definen en [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1)y puede incluirse en las secuencias de comandos mediante el siguiente ejemplo de Hola:

    # Download config action module from a well-known directory.
    $CONFIGACTIONURI = "https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1";
    $CONFIGACTIONMODULE = "C:\apps\dist\HDInsightUtilities.psm1";
    $webclient = New-Object System.Net.WebClient;
    $webclient.DownloadFile($CONFIGACTIONURI, $CONFIGACTIONMODULE);

    # (TIP) Import config action helper method module toomake writing config action easy.
    if (Test-Path ($CONFIGACTIONMODULE))
    {
        Import-Module $CONFIGACTIONMODULE;
    }
    else
    {
        Write-Output "Failed tooload HDInsightUtilities module, exiting ...";
        exit;
    }

Estos son los métodos auxiliares de Hola que se proporcionan con esta secuencia de comandos:

| Método auxiliar | Description |
| --- | --- |
| **Save-HDIFile** |Descarga un archivo de hello Especifica ubicación tooa de identificador uniforme de recursos (URI) en el disco local de Hola que está asociado con hello Azure VM nodo toohello asignado clúster. |
| **Expand-HDIZippedFile** |Descomprimir un archivo comprimido. |
| **Invoke-HDICmdScript** |Ejecutar un script desde cmd.exe. |
| **Write-HDILog** |Escribe un resultado de script personalizado de hello utilizado para una acción de secuencia de comandos. |
| **Get-Services** |Obtener una lista de servicios que se ejecutan en el equipo de Hola donde se ejecuta el script de Hola. |
| **Get-Service** |Con el nombre de servicio específico de hello como entrada, obtener información detallada sobre un servicio específico (el nombre del servicio, procesar el identificador, estado, etc.) en la máquina de Hola donde se ejecuta el script de Hola. |
| **Get-HDIServices** |Obtener una lista de servicios de HDInsight que se ejecutan en el equipo de Hola donde se ejecuta el script de Hola. |
| **Get-HDIService** |Con hello HDInsight servicio nombre específico como entrada, obtener información detallada sobre un servicio específico (el nombre del servicio, procesar el identificador, estado, etc.) en la máquina de Hola donde se ejecuta el script de Hola. |
| **Get-ServicesRunning** |Obtener una lista de servicios que se ejecutan en el equipo de Hola donde se ejecuta el script de Hola. |
| **Get-ServiceRunning** |Compruebe si está ejecutando un servicio específico (por nombre) en el equipo de Hola donde se ejecuta el script de Hola. |
| **Get-HDIServicesRunning** |Obtener una lista de servicios de HDInsight que se ejecutan en el equipo de Hola donde se ejecuta el script de Hola. |
| **Get-HDIServiceRunning** |Compruebe si está ejecutando un servicio HDInsight específico (por nombre) en el equipo de Hola donde se ejecuta el script de Hola. |
| **Get-HDIHadoopVersion** |Obtener la versión de Hola de Hadoop instalado en equipo Hola donde se ejecuta el script de Hola. |
| **Test-IsHDIHeadNode** |Comprobar si el equipo de Hola donde se ejecuta el script de Hola es un nodo principal. |
| **Test-IsActiveHDIHeadNode** |Compruebe si el equipo Hola donde se ejecuta el script de Hola es un nodo principal activo. |
| **Test-IsHDIDataNode** |Compruebe si el equipo Hola donde se ejecuta el script de Hola es un nodo de datos. |
| **Edit-HDIConfigFile** |Editar archivos de configuración de hello hive-site.xml, core-site.xml, hdfs-site.xml, mapred-site.xml o yarn-site.xml. |

## <a name="best-practices-for-script-development"></a>Prácticas recomendadas para el desarrollo de script
Al desarrollar un script personalizado para un clúster de HDInsight, hay varios tookeep prácticas recomendadas en cuenta:

* Busque la versión de Hadoop de Hola

    HDInsight sólo la versión 3.1 (Hadoop 2.4) y versiones posteriores de compatibilidad con componentes personalizados de tooinstall de acción de secuencia de comandos en un clúster. En el script personalizado, debe usar hello **HDIHadoopVersion Get** versión auxiliar método toocheck hello Hadoop antes de continuar con la realización de otras tareas en el script de Hola.
* Proporcionar estable vincula tooscript recursos

    Los usuarios deben asegurarse de que todos los scripts de Hola y otros artefactos que se utiliza en la personalización de Hola de un clúster siguen estando disponibles a lo largo de la duración de Hola de clúster de Hola y que las versiones de Hola de estos archivos no cambian durante el saludo. Estos recursos son necesarios si Hola restablecer la imagen inicial de nodos de clúster de hello es necesaria. procedimiento recomendado de Hello es toodownload y archivar todo el contenido de una cuenta de almacenamiento que Hola controles de usuario. Puede tratarse de cuenta de almacenamiento predeterminada de Hola o cualquiera de las cuentas de almacenamiento adicionales de hello especificadas en tiempo de Hola de implementación para un clúster personalizado.
    Hola Spark R personalizar y ejemplos de clúster proporcionado en la documentación de hello, por ejemplo, hemos realizado una copia local de los recursos de hello en esta cuenta de almacenamiento: https://hdiconfigactions.blob.core.windows.net/.
* Asegúrese de que el script de personalización de clúster de hello es idempotente

    Debe esperar que los nodos de Hola de un clúster de HDInsight está restableciendo imagen inicial durante la vigencia de clúster de Hola. script de personalización de Hello clúster se ejecuta cada vez que se está restableciendo imagen inicial de un clúster. Esta secuencia de comandos debe ser idempotente toobe diseñado en sentido Hola que tras restablecer la imagen inicial, el script de Hola debe asegurarse de que ese clúster Hola se devuelve toohello que mismo Personalizar estado que se encontraba justo después de script de Hola se ejecutó para hello primera hora en que el clúster de Hola se inicialmente creado. Por ejemplo, si un script personalizado instalado una aplicación en D:\AppLocation en su primera ejecución, a continuación, en cada ejecución subsiguiente, tras restaurar, el script de Hola debe comprobar si aplicación hello existe en hello D:\AppLocation ubicación antes de continuar con otro pasos de secuencia de comandos de Hola.
* Instalar componentes personalizados en ubicación óptima Hola

    Cuando se restablece la imagen inicial nodos del clúster, unidad de recurso de hello C:\ y D:\ unidad del sistema pueden cambiar el formato, lo que causará Hola pérdida de datos y las aplicaciones instaladas de esas unidades. Esto también podría ocurrir si un nodo de la máquina virtual de Azure (VM) que forma parte del clúster de hello deja de funcionar y se sustituye por un nuevo nodo. Puede instalar componentes en hello unidad D:\ o en ubicación de C:\apps hello en clúster de Hola. Todas las demás ubicaciones en hello unidad C:\ están reservadas. Especifique la ubicación de Hola donde las aplicaciones o bibliotecas son toobe instalado en el script de personalización de clúster de Hola.
* Asegurar la alta disponibilidad de la arquitectura de clúster de Hola

    HDInsight tiene una arquitectura activo / pasivo para lograr alta disponibilidad, en que un nodo principal está en modo activo (donde se ejecutan los servicios de HDInsight de hello) y Hola otro nodo principal está en modo de espera (en qué HDInsight no se ejecutan servicios). nodos de Hello cambiar entre modos activos y pasivos si se interrumpen servicios HDInsight. Si una acción de secuencia de comandos es servicios tooinstall usado en ambos nodos principales para alta disponibilidad, tenga en cuenta que esa Hola mecanismo de conmutación por error de HDInsight no es capaz de tooautomatically producirá un error de estos servicios instalados por el usuario. Servicios instalados por el usuario por lo que en HDInsight nodos principales que son esperado toobe de alta disponibilidad deben tener su propio mecanismo de conmutación por error si se encuentra en modo activo / pasivo o estar en modo activo / activo.

    Se ejecuta un comando de acción de secuencia de comandos de HDInsight en ambos nodos principales al rol de nodo principal de Hola se especifica como un valor en hello *ClusterRoleCollection* parámetro. Por tanto, cuando diseñe un script personalizado, asegúrese de que el script reconoce esta configuración. No debe encontrarse con problemas donde hello mismos servicios están instalados e iniciados en ambos nodos principales de Hola y terminan compiten entre sí. Además, tenga en cuenta que se pierdan datos durante el restablecimiento de imagen inicial, por lo que el software instalado mediante una acción de secuencia de comandos tiene toobe toosuch resistente eventos. Las aplicaciones deben tener toowork diseñada con datos de alta disponibilidad que se distribuyen por varios nodos. Tenga en cuenta que como máximo 1/5 de nodos de hello en un clúster puede restaurarse en hello mismo tiempo.
* Configurar el almacenamiento de blobs de Azure de hello componentes personalizados toouse

    componentes personalizados de Hola que se instalación en los nodos de clúster de hello podrían tener un toouse de configuración predeterminado almacenamiento de sistema de archivos distribuido de Hadoop (HDFS). Debe cambiar Hola configuración toouse almacenamiento de blobs de Azure en su lugar. En un restablecimiento de imagen inicial de clúster, obtiene el formato sistema de archivos HDFS hello y se perderá cualquier dato que se almacena allí. El empleo de Azure Blob Storage garantiza la conservación de los datos.

## <a name="common-usage-patterns"></a>Patrones de uso común
Esta sección proporciona instrucciones sobre cómo implementar algunos Hola patrones de uso comunes que pueden surgir al escribir sus propios scripts personalizados.

### <a name="configure-environment-variables"></a>Configuración de las variables de entorno
A menudo en el desarrollo de la acción de secuencia de comandos, cree Hola necesita tooset variables de entorno. Por ejemplo, un escenario más probable es al descargar un archivo binario de un sitio externo, instalarlo en clúster de Hola y agregar ubicación de Hola de donde es variable de entorno 'PATH' tooyour instalado. Hola siguiente fragmento de código muestra cómo las variables de entorno tooset en Hola script personalizado.

    Write-HDILog "Starting environment variable setting at: $(Get-Date)";
    [Environment]::SetEnvironmentVariable('MDS_RUNNER_CUSTOM_CLUSTER', 'true', 'Machine');

Esta instrucción establece la variable de entorno de hello **MDS_RUNNER_CUSTOM_CLUSTER** toohello valor 'true' y también establece Hola ámbito de esta variable toobe todo el equipo. A veces es importante que las variables de entorno se establecen en el ámbito adecuado de Hola, equipo o usuario. Consulte [aquí][1] para obtener más información sobre cómo establecer las variables de entorno.

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Toolocations de acceso donde se almacenan los scripts personalizados de Hola
Secuencias de comandos utilizadas toocustomize un tooeither de necesidades del clúster ser en la cuenta de almacenamiento predeterminada de hello para el clúster de Hola o en un contenedor público de solo lectura en ninguna otra cuenta de almacenamiento. Si el script tiene acceso a recursos ubicados en otros lugares tienen toobe en accesible públicamente (al menos públicas de solo lectura). Por ejemplo podría desea tooaccess un archivo y guárdelo con hello SaveFile HDI comando.

    Save-HDIFile -SrcUri 'https://somestorageaccount.blob.core.windows.net/somecontainer/some-file.jar' -DestFile 'C:\apps\dist\hadoop-2.4.0.2.1.9.0-2196\share\hadoop\mapreduce\some-file.jar'

En este ejemplo, debe asegurarse de que el contenedor de hello 'somecontainer' en la cuenta de almacenamiento 'somestorageaccount' es accesible públicamente. En caso contrario, el script de Hola produce una excepción 'No se encontró' y producirá un error.

### <a name="pass-parameters-toohello-add-azurermhdinsightscriptaction-cmdlet"></a>Pasar parámetros toohello AzureRmHDInsightScriptAction agregar cmdlet
toopass varios parámetros toohello AzureRmHDInsightScriptAction agregar cmdlet, necesita toocontain del valor de cadena de tooformat Hola todos los parámetros de script de Hola. Por ejemplo:

    "-CertifcateUri wasb:///abc.pfx -CertificatePassword 123456 -InstallFolderName MyFolder"

o

    $parameters = '-Parameters "{0};{1};{2}"' -f $CertificateName,$certUriWithSasToken,$CertificatePassword


### <a name="throw-exception-for-failed-cluster-deployment"></a>Inicio de excepción para error en implementación de clúster
Si desea tooget con precisión una notificación del hecho de Hola de dicha personalización de clúster no se realizó correctamente según lo previsto, es importante toothrow una excepción y producirá un error de creación del clúster Hola. Por ejemplo, podría desea tooprocess un archivo si existe y controlar el caso de error de Hola donde archivo hello no existe. Esto garantizará que el script de Hola se cierra correctamente y correctamente se conoce el estado de Hola de clúster de Hola. Hello fragmento de código siguiente proporciona un ejemplo de cómo tooachieve esto:

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    exit
    }

En este fragmento de código, si no existía archivo hello, provocaría tooa estado donde script de Hola realmente se cierra correctamente después de imprimir el mensaje de error de Hola y clúster Hola alcanza el estado de ejecución suponiendo que se "correctamente" completado el proceso de personalización de clústeres. Si desea toobe con precisión una notificación del hecho de Hola de esa personalización clúster básicamente no se realizó correctamente según lo esperado debido a un archivo que falta, es más adecuado toothrow una excepción y producirá un error de paso de personalización de clústeres de Hola. tooachieve esto debe usar Hola siguiente fragmento de código de ejemplo en su lugar.

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    throw
    }


## <a name="checklist-for-deploying-a-script-action"></a>Lista de comprobación para implementar una acción de script
Estos son los pasos de Hola que se llevaron a cabo al preparar toodeploy estas secuencias de comandos:

1. Coloque los archivos de Hola que contienen scripts personalizados de hello en un lugar que sea accesible para nodos de clúster de Hola durante la implementación. Esto puede ser cualquiera de predeterminado de Hola o más cuentas de almacenamiento especificadas en tiempo de presentación de la implementación del clúster, o cualquier otro contenedor de almacenamiento accesibles públicamente.
2. Agregar comprobaciones en las secuencias de comandos toomake seguro de que se ejecuta de manera idempotente, para que el script de Hola se puede ejecutar varias veces en hello mismo nodo.
3. Hola de uso **Write-Output** tooSTDOUT de tooprint de cmdlet de PowerShell de Azure, así como STDERR. No utilice **Write-Host**.
4. Usar una carpeta de archivo temporal, como $env: TEMP, tookeep Hola descargado archivo usado por las secuencias de comandos de hello y, a continuación, limpiarlas después de que se han ejecutado las secuencias de comandos.
5. Instale el software personalizado solo en D:\ o en C:\apps. Otras ubicaciones en la unidad C: de hello no deben usarse como están reservadas. Tenga en cuenta que instale los archivos en la unidad C: de hello fuera de la carpeta de hello C:\apps puede derivar en errores de instalación durante la reimages del nodo de Hola.
6. En el caso de hello que se han modificado los valores de configuración de nivel de sistema operativo o archivos de configuración de servicio de Hadoop, puede que desee toorestart HDInsight servicios para que puede seleccionar cualquier configuración de nivel de sistema operativo, como las variables de entorno de hello set en scripts de Hola.

## <a name="debug-custom-scripts"></a>Depuración de scripts personalizados
registros de errores de script de Hola se almacenan, junto con otros resultados, en la cuenta de almacenamiento predeterminada de Hola que especificó para el clúster de hello en su creación. Hello registros almacenan en una tabla con nombre de hello *u < \cluster-name-fragment >< \time-stamp > setuplog*. Se trata de registros agregados que tienen registros de todos los nodos de hello (nodo principal y nodos de trabajador) en qué Hola script se ejecuta en el clúster de Hola.
Una manera sencilla de registros de hello toocheck es toouse HDInsight Tools para Visual Studio. Para instalar herramientas de hello, consulte [Introducción al uso de Hadoop de Visual Studio tools para HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)

**registro de hello toocheck con Visual Studio**

1. Abra Visual Studio.
2. Haga clic en **Ver**, y, luego, haga clic en **Explorador de servidores**.
3. Haga clic en "Azure", haga clic en conectar demasiado**suscripciones de Microsoft Azure**y, a continuación, escriba sus credenciales.
4. Expanda **almacenamiento**, expanda y cuenta de almacenamiento de Azure de hello usada como sistema de archivos predeterminado de hello **tablas**y, a continuación, haga doble clic en el nombre de la tabla de Hola.

Puede también remoto en toosee de nodos de clúster de hello STDOUT y STDERR para scripts personalizados. Hello los registros en cada nodo se nodo toothat solo específico y se registran en **C:\HDInsightLogs\DeploymentAgent.log**. Estos archivos de registro registran todas las salidas desde un script personalizado de Hola. Un fragmento de código de registro de ejemplo para una acción de script de Spark tiene este aspecto:

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand; Details : BEGIN: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Starting Spark installation at: 09/04/2014 21:46:02 Done with Spark installation at: 09/04/2014 21:46:38;

    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand;
    Details : END: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;


En este registro, es obvio que Hola Spark Generar script de acción se ha ejecutado en la máquina virtual denominada HEADNODE0 hello y que se produce ninguna excepción durante la ejecución de Hola.

En caso de Hola que se produce un error de ejecución, la salida de hello que lo describe también está incluida en este archivo de registro. información de Hello proporcionada en estos registros debe ser útil para depurar problemas de secuencia de comandos que pueden surgir.

## <a name="see-also"></a>Otras referencias
* [Personalización de los clústeres de HDInsight mediante la acción de script][hdinsight-cluster-customize]
* [Instalación y uso de Spark en clústeres de HDInsight][hdinsight-install-spark]
* [Instalación y uso de R en clústeres de Hadoop de HDInsight][hdinsight-r-scripts]
* [Instalación y uso de Solr en clústeres de Hadoop de HDInsight](hdinsight-hadoop-solr-install.md).
* [Instalación y uso de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install.md).

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-r-scripts]: hdinsight-hadoop-r-scripts.md
[powershell-install-configure]: install-configure-powershell.md

<!--Reference links in article-->
[1]: https://msdn.microsoft.com/library/96xafkes(v=vs.110).aspx
