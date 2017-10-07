---
title: "desarrollo de la acción de aaaScript con HDInsight basados en Linux - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Bash scripts toocustomize clústeres de HDInsight basados en Linux. característica de acción de secuencia de comandos de Hola de HDInsight permite las secuencias de comandos de toorun durante o después de la creación del clúster. Las secuencias de comandos pueden ser toochange usa valores de configuración de clúster o instalar software adicional."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a>Desarrollo de la acción de script con HDInsight

Obtenga información acerca de cómo su clúster de HDInsight con Bash toocustomize secuencias de comandos. Las acciones de script son un toocustomize de manera HDInsight durante o después de la creación del clúster.

> [!IMPORTANT]
> pasos de Hello en este documento requieren un clúster de HDInsight que usa Linux. Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="what-are-script-actions"></a>¿Qué son las acciones de script?

Acciones de script son scripts de Bash que Azure se ejecuta en los cambios de configuración de toomake de nodos de clúster de Hola o instalarán software. Una acción de secuencia de comandos se ejecuta como raíz y proporciona acceso completo de nodos de clúster de derechos toohello.

Acciones de script se pueden aplicar mediante Hola siguientes métodos:

| Utilice este tooapply método una secuencia de comandos... | Durante la creación del clúster... | En un clúster en ejecución... |
| --- |:---:|:---:|
| Portal de Azure |✓  |✓ |
| Azure PowerShell |✓ |✓ |
| Azure CLI |&nbsp; |✓ |
| SDK .NET de HDInsight |✓ |✓ |
| Plantilla de Azure Resource Manager |✓ |&nbsp; |

Para obtener más información sobre el uso de estas acciones de secuencia de comandos de tooapply de métodos, vea [HDInsight personalizar clústeres mediante acciones de script](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="bestPracticeScripting"></a>Prácticas recomendadas para el desarrollo de scripts

Al desarrollar un script personalizado para un clúster de HDInsight, hay varios tookeep prácticas recomendadas en cuenta:

* [Versión de Hadoop de Hola de destino](#bPS1)
* [Hola versión del sistema operativo de destino](#bps10)
* [Proporcionar estable vincula tooscript recursos](#bPS2)
* [Usar recursos compilados previamente](#bPS4)
* [Asegúrese de que el script de personalización de clúster de hello es idempotente](#bPS3)
* [Asegurar la alta disponibilidad de la arquitectura de clúster de Hola](#bPS5)
* [Configurar el almacenamiento de blobs de Azure de hello componentes personalizados toouse](#bPS6)
* [Escribir información tooSTDOUT y STDERR](#bPS7)
* [Guardar los archivos como ASCII con el fin de línea LF](#bps8)
* [Usar toorecover de lógica de reintento de errores transitorios](#bps9)

> [!IMPORTANT]
> Acciones de script deben completarse dentro de 60 minutos o se produce un error en el proceso de Hola. Durante el aprovisionamiento de nodo, el script de Hola se ejecuta simultáneamente con otros procesos de instalación y configuración. La competición por los recursos, como el ancho de banda de red o de tiempo de CPU puede provocar Hola script tootake más toofinish que lo hace en el entorno de desarrollo.

### <a name="bPS1"></a>Versión de Hadoop de Hola de destino

Las distintas versiones de HDInsight tienen distintas versiones de componentes y servicios de Hadoop instalados. Si la secuencia de comandos espera una versión específica de un servicio o componente, solo debería usar script de Hola con la versión de Hola de HDInsight que incluye componentes de hello necesario. Puede encontrar información sobre las versiones del componente incluido con HDInsight con hello [versiones de componentes de HDInsight](hdinsight-component-versioning.md) documento.

### <a name="bps10"></a>Versión de Hola SO de destino

HDInsight basados en Linux se basa en hello distribución Ubuntu Linux. Las distintas versiones de HDInsight se basan en diferentes versiones de Ubuntu, que podrían cambiar el funcionamiento del script. Por ejemplo, HDInsight 3.4 y versiones anteriores se basan en versiones de Ubuntu que emplean Upstart. La versión 3.5 se basa en Ubuntu 16.04, que utiliza Systemd. Systemd y advenedizo utilizan comandos diferentes, por lo que se debe escribir el script toowork con ambos.

Otra diferencia importante entre HDInsight 3.4 y 3.5 es que `JAVA_HOME` señale tooJava 8.

Puede comprobar versión Hola SO mediante `lsb_release`. Hello código siguiente muestra cómo toodetermine si hello secuencia de comandos se ejecuta en Ubuntu 14 o 16:

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

Puede encontrar el script completo de Hola que contiene estos fragmentos de código en https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.

Para versión de Hola de Ubuntu que usa HDInsight, vea hello [HDInsight la versión del componente](hdinsight-component-versioning.md) documento.

vea las diferencias de hello toounderstand entre Systemd y advenedizo, [Systemd para los usuarios de advenedizo](https://wiki.ubuntu.com/SystemdForUpstartUsers).

### <a name="bPS2"></a>Proporcionar estable vincula tooscript recursos

Hello secuencia de comandos y los recursos asociados deben permanecer disponibles durante toda la duración de Hola de clúster de Hola. Estos recursos son necesarios si se agregan nuevos nodos de clúster toohello durante las operaciones de ajuste de escala.

procedimiento recomendado de Hello es toodownload y archivar todo el contenido de una cuenta de almacenamiento de Azure en su suscripción.

> [!IMPORTANT]
> cuenta de almacenamiento de Hello utilizada debe ser cuenta de almacenamiento del predeterminada Hola para clúster de Hola o un contenedor público, de solo lectura en ninguna otra cuenta de almacenamiento.

Por ejemplo, ejemplos de hello proporcionados por Microsoft se almacenan en hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) cuenta de almacenamiento. Se trata de un contenedor público, de solo lectura mantenido por el equipo de HDInsight de Hola.

### <a name="bPS4"></a>Usar recursos compilados previamente

Hola tooreduce tiempo toma toorun Hola script, evitar las operaciones que se compilan los recursos desde el código fuente. Por ejemplo, la compilación previa de recursos y almacenarlos en un blob de la cuenta de almacenamiento de Azure en hello mismo centro de datos como HDInsight.

### <a name="bPS3"></a>Asegúrese de que el script de personalización de clúster de hello es idempotente

Los scripts deben ser idempotentes. Si se ejecuta el script de Hola varias veces, debería devolver Hola toohello clúster mismo estado cada vez.

Por ejemplo, un script que modifique los archivos de configuración no debería agregar entradas duplicadas si se ejecuta varias veces.

### <a name="bPS5"></a>Asegurar la alta disponibilidad de la arquitectura de clúster de Hola

Los clústeres de HDInsight basados en Linux proporcionan dos nodos principales que están activos en el clúster de Hola y acciones de secuencia de comandos se ejecutan en ambos nodos. Si instala los componentes Hola esperan sólo un nodo principal, no instale componentes de hello en ambos nodos principales.

> [!IMPORTANT]
> Servicios proporcionados como parte de HDInsight son toofail diseñada sobre entre dos nodos principales del Hola según sea necesario. Esta funcionalidad no se amplía toocustom que se instalen a través de acciones de script. Si necesita una disponibilidad elevada en componentes personalizados, deberá implementar su propio mecanismo de conmutación por error.

### <a name="bPS6"></a>Configurar el almacenamiento de blobs de Azure de hello componentes personalizados toouse

Componentes que se instalan en el clúster de hello podrían tener una configuración predeterminada que utiliza el almacenamiento de sistema de archivos distribuido de Hadoop (HDFS). HDInsight usa el almacenamiento de Azure o el almacén de Data Lake como almacenamiento predeterminado de Hola. Ambos proporcionan un sistema de archivos compatibles de HDFS que conserva los datos incluso si se elimina el clúster de Hola. Puede que tenga los componentes de tooconfigure instalar toouse WASB o ADL en lugar de HDFS.

Para la mayoría de las operaciones, no es necesario toospecify sistema de archivos de Hola. Por ejemplo, siguiente Hola copia archivo del archivo giraph-examples.jar hello de almacenamiento de toocluster del sistema de archivos local de hello:

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

En este ejemplo, Hola `hdfs` comando usa forma transparente el almacenamiento de clúster predeterminado de Hola. Para algunas operaciones, puede que necesite toospecify Hola URI. Por ejemplo, `adl:///example/jars` para Data Lake Store o `wasb:///example/jars` para Azure Storage.

### <a name="bPS7"></a>Escribir información tooSTDOUT y STDERR

HDInsight registra el resultado de script que está escrito tooSTDOUT y STDERR. Puede ver esta información mediante la interfaz de usuario de web de hello Ambari.

> [!NOTE]
> Ambari solo está disponible si Hola clúster se creó correctamente. Si usa una acción de secuencia de comandos durante la creación del clúster y se produce un error de creación, consulte sección de solución de problemas de hello [HDInsight personalizar clústeres mediante la acción de secuencia de comandos](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) para conocer otras maneras de obtener acceso a información registrada.

Mayoría de las utilidades y los paquetes de instalación ya escriben información tooSTDOUT y STDERR, sin embargo, puede que desee tooadd inicio de sesión adicional. texto toosend tooSTDOUT, use `echo`. Por ejemplo:

```bash
echo "Getting ready tooinstall Foo"
```

De forma predeterminada, `echo` envía Hola tooSTDOUT de cadena. toodirect, tooSTDERR, agregue `>&2` antes de `echo`. Por ejemplo:

```bash
>&2 echo "An error occurred installing Foo"
```

Esto redirige la información escrita tooSTDOUT tooSTDERR (2) en su lugar. Para obtener más información sobre la redirección de E/S, consulte [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).

Para obtener más información sobre la visualización de información registrada por las acciones de script, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)

### <a name="bps8"></a> Guardar los archivos como ASCII con el fin de línea LF

Los scripts de Bash deben almacenarse con formato ASCII, con líneas terminadas con LF. Se pueden producir archivos que se almacenan como UTF-8, o usan CRLF como final de la línea de Hola Hola siguiente error:

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <a name="bps9"></a>Usar toorecover de lógica de reintento de errores transitorios

Al descargar archivos, instalar paquetes mediante get apt u otras acciones que transmiten datos a través de Hola internet, acción de hello puede producirse errores debido a errores de red tootransient. Por ejemplo, recurso remoto de Hola que se está comunicando con puede estar en proceso de Hola de errores sobre el nodo de copia de seguridad de tooa.

toomake los errores de tootransient resistente a errores de secuencia de comandos, puede implementar la lógica de reintento. Hola siguiente función muestra cómo tooimplement lógica de reintento. Vuelve a intentar la operación de hello tres veces antes de desistir.

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

Hello en los ejemplos siguientes se muestran cómo toouse esta función.

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <a name="helpermethods"></a>Métodos auxiliares para scripts personalizados

Los métodos auxiliares de la acción de script son utilidades que puede usar al escribir scripts personalizados. Estos métodos se encuentran en el script [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh). Usar hello después toodownload y usarlas como parte de la secuencia de comandos:

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

Hola después Ayudantes disponibles para su uso en la secuencia de comandos:

| Uso de la aplicación auxiliar | Descripción |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |Descarga un archivo de hello origen URI toohello ruta de acceso especificada. De forma predeterminada, no sobrescribirá un archivo existente. |
| `untar_file TARFILE DESTDIR` |Extrae un archivo tar (mediante `-xf`) toohello directorio de destino. |
| `test_is_headnode` |Si se ejecutaba en un nodo principal del clúster, devuelve 1. En caso contrario, devuelve 0. |
| `test_is_datanode` |Si el nodo actual de hello es un nodo de datos (trabajo), devuelve un 1; en caso contrario, es 0. |
| `test_is_first_datanode` |Si el nodo actual de hello es datos primera hello (trabajo) nodo (con nombre workernode0) devuelve un 1; en caso contrario, es 0. |
| `get_headnodes` |Devuelve el nombre de dominio completo de Hola de hello headnodes de clúster Hola. Los nombres están delimitados por comas. En caso de error, se devuelve una cadena vacía. |
| `get_primary_headnode` |Obtiene el nombre de dominio completo de Hola de nodo principal de hello principal. En caso de error, se devuelve una cadena vacía. |
| `get_secondary_headnode` |Obtiene el nombre de dominio completo de Hola de nodo principal de hello secundaria. En caso de error, se devuelve una cadena vacía. |
| `get_primary_headnode_number` |Obtiene el sufijo numérico de Hola de nodo principal primario de Hola. En caso de error, se devuelve una cadena vacía. |
| `get_secondary_headnode_number` |Obtiene el sufijo numérico de Hola de nodo principal secundario de Hola. En caso de error, se devuelve una cadena vacía. |

## <a name="commonusage"></a>Patrones de uso común

Esta sección proporciona instrucciones sobre cómo implementar algunos Hola patrones de uso comunes que pueden surgir al escribir sus propios scripts personalizados.

### <a name="passing-parameters-tooa-script"></a>Pasar parámetros de script tooa

En algunos casos, un script puede requerir parámetros. Por ejemplo, puede necesitar contraseña de administrador de Hola para clúster hello cuando se usa la API de REST de Ambari Hola.

Se denominan parámetros pasados script toohello *parámetros posicionales*y se asignan demasiado`$1` para el primer parámetro hello, `$2` para hello segundo y por lo que la sesión. `$0`contiene el nombre de hello del propio script de Hola.

Valores pasados toohello script como parámetros deberían estar entre comillas simples ('). Este modo se asegura que Hola pasado el valor se trata como un literal.

### <a name="setting-environment-variables"></a>Establecimiento de variables de entorno

Establecer una variable de entorno se realiza por hello siguiente instrucción:

    VARIABLENAME=value

Donde VARIABLENAME es nombre Hola de variable de saludo. uso de variables, tooaccess hello `$VARIABLENAME`. Por ejemplo, tooassign un valor proporcionado por un parámetro posicional como una variable de entorno denominada contraseña, usaría Hola siguiente instrucción:

    PASSWORD=$1

A continuación, podría utilizar la información de acceso subsiguiente toohello `$PASSWORD`.

Las variables de entorno que se establece en el script de Hola solo existen en ámbito de Hola de script de Hola. En algunos casos, deberá variables de entorno de todo el sistema de tooadd que se conservarán cuando finalice el script de Hola. variables de entorno de todo el sistema de tooadd, Agregar variable Hola demasiado`/etc/environment`. Por ejemplo, hello siguiente instrucción agrega `HADOOP_CONF_DIR`:

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Toolocations de acceso donde se almacenan los scripts personalizados de Hola

Toocustomize de secuencias de comandos que se utiliza un clúster debe toobe almacenado en una de las siguientes ubicaciones de Hola:

* Un __cuenta de almacenamiento de Azure__ que está asociado con el clúster de Hola.

* Un __cuenta de almacenamiento adicional__ asociado con el clúster de Hola.

* Un __URI legible públicamente__. Por ejemplo, un toodata de dirección URL almacenado en OneDrive, Dropbox o en otro archivo de servicio de hospedaje.

* Un __cuenta de almacén de Azure Data Lake__ que está asociado con el clúster de HDInsight Hola. Para más información sobre el uso de Azure Data Lake Store con HDInsight, consulte [Creación de un clúster de HDInsight con Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

    > [!NOTE]
    > Hola servicio principal HDInsight utiliza tooaccess almacén de Data Lake debe tener acceso de lectura toohello script.

Recursos utilizados por el script de Hola también deben estar disponibles públicamente.

Almacenar archivos de hello en una cuenta de almacenamiento de Azure o un almacén de Data Lake de Azure proporciona un acceso rápido, como en hello red de Azure.

> [!NOTE]
> Hola URI formato usado tooreference Hola script depende de servicio Hola usándola. Para las cuentas de almacenamiento asociadas con el clúster de HDInsight de hello, use `wasb://` o `wasbs://`. Para los URI legibles públicamente, use `http://` o `https://`. Para Data Lake Store, use `adl://`.

### <a name="checking-hello-operating-system-version"></a>Comprobación de la versión de sistema operativo de Hola

Las distintas versiones de HDInsight se basan en versiones específicas de Ubuntu. Puede haber diferencias entre las versiones del sistema operativo que debe comprobar en el script. Por ejemplo, puede que necesite tooinstall un archivo binario que está enlazada toohello versión de Ubuntu.

versión de Hola OS toocheck, use `lsb_release`. Por ejemplo, hello siguiente secuencia de comandos muestra cómo tooreference una tar específico de archivos según Hola versión del sistema operativo:

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <a name="deployScript"></a>Lista de comprobación para implementar una acción de script

Estos son los pasos de Hola que se llevaron a cabo al preparar toodeploy estas secuencias de comandos:

* Coloque los archivos de Hola que contienen scripts personalizados de hello en un lugar que sea accesible para nodos de clúster de Hola durante la implementación. Por ejemplo, hello almacenamiento predeterminado para el clúster de Hola. Los archivos también se pueden almacenar en servicios de hospedaje visibles públicamente.
* Compruebe que el script de Hola es impotent. Esto permite que toobe de script de Hola ejecuta varias veces en hello mismo nodo.
* Use un hello tookeep de archivo temporal directorio/tmp descargan archivos utilizados por las secuencias de comandos de hello y, a continuación, limpiarlas después de que se han ejecutado las secuencias de comandos.
* Si se cambian los valores de configuración de nivel de sistema operativo o archivos de configuración de servicio de Hadoop, puede que desee toorestart HDInsight servicios.

## <a name="runScriptAction"></a>¿Cómo toorun una acción de secuencia de comandos

Puede utilizar clústeres de HDInsight de toocustomize script acciones con hello siguientes métodos:

* Azure Portal
* Azure PowerShell
* Plantillas de Azure Resource Manager
* Hola HDInsight .NET SDK.

Para obtener más información sobre el uso de cada método, consulte [cómo toouse script acción](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="sampleScripts"></a>Ejemplos de scripts personalizados

Microsoft proporciona secuencias de comandos de ejemplo tooinstall componentes en un clúster de HDInsight. Vea los siguientes vínculos para ver más acciones de script de ejemplo de Hola.

* [Instalación y uso de Hue en clústeres de HDInsight](hdinsight-hadoop-hue-linux.md)
* [Instalación y uso de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install-linux.md)
* [Instalación y uso de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install-linux.md)
* [Instalación o actualización de Mono en clústeres de HDInsight](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a>Solución de problemas

siguiente Hola es errores que pueden producirse al utilizar secuencias de comandos que se han desarrollado:

**Error**: `$'\r': command not found`. A veces seguido de `syntax error: unexpected end of file`.

*Causa*: este error se produce cuando las líneas de hello en una secuencia de comandos se terminan con CRLF. Los sistemas UNIX esperan sólo LF como final de la línea de saludo.

Este problema suele producirse cuando se ha creado en un entorno de Windows, el script de Hola CRLF sea una línea común final para muchos editores de texto en Windows.

*Resolución*: si es una opción en el editor de texto, seleccione formato Unix o LF final de la línea de saludo. También puede usar Hola siguientes comandos en un tooan de Unix sistema toochange Hola CRLF LF:

> [!NOTE]
> Hello siguientes comandos son aproximadamente equivalentes en que deben cambiar Hola CRLF línea finales tooLF. Seleccione una basada en utilidades de hello disponibles en el sistema.

| Comando | Notas |
| --- | --- |
| `unix2dos -b INFILE` |archivo original de Hello está respaldado por una. Extensión BAK |
| `tr -d '\r' < INFILE > OUTFILE` |OUTFILE contendrá una versión con finales de línea solo LF |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | Modifica el archivo hello directamente |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |OUTFILE contendrá una versión con finales de línea solo LF. |

**Error**: `line 1: #!/usr/bin/env: No such file or directory`.

*Causa*: este error se produce cuando hello script se guarda como UTF-8 con una marca de orden de bytes (BOM).

*Resolución*: guardar el archivo hello como ASCII o UTF-8 sin una marca BOM. También puede usar el siguiente comando en un sistema Linux o Unix toocreate un archivo sin Hola BOM de hello:

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

Reemplace `INFILE` con archivo hello que contiene Hola BOM. `OUTFILE`debe ser un nuevo nombre de archivo que contiene el script de Hola sin Hola BOM.

## <a name="seeAlso"></a>Pasos siguientes

* Obtenga información acerca de cómo demasiado[clústeres de HDInsight personalizar mediante la acción de secuencia de comandos](hdinsight-hadoop-customize-cluster-linux.md)
* Hola de uso [referencia de SDK de HDInsight .NET](https://msdn.microsoft.com/library/mt271028.aspx) toolearn más acerca de cómo crear aplicaciones .NET que administración HDInsight
* Hola de uso [API de REST de HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn cómo clústeres acciones de administración de toouse REST tooperform en HDInsight.
