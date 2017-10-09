---
title: datos de aaaUpload para trabajos de Hadoop en HDInsight | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooupload y acceso a datos para los trabajos de Hadoop en HDInsight utilizando Hola CLI de Azure, el Explorador de almacenamiento de Azure, Azure PowerShell, línea de comandos de Hadoop de Hola o Sqoop."
keywords: "extracción, transformación y carga de datos de hadoop, obtención de datos en hadoop, carga de datos de hadoop"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 15da602085d41c19789e34800f3d9e238d7d1de8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a>Carga de datos para trabajos de Hadoop en HDInsight
HDInsight de Azure ofrece un sistema de archivos distribuido de Hadoop (HDFS) completo a través del servicio de almacenamiento de blobs de Azure. Está diseñado como un tooprovide de extensión HDFS una perfecta experiencia toocustomers. Habilita Hola conjunto completo de componentes de hello Hadoop ecosistema toooperate directamente en los datos de Hola que administra. El almacenamiento de blobs de Azure y HDFS son sistemas de archivos diferentes que se han optimizado para el almacenamiento de datos y el cálculo en ellos. Para obtener información acerca de las ventajas de hello del uso de almacenamiento de blobs de Azure, consulte [almacenamiento de blobs de Azure de uso con HDInsight][hdinsight-storage].

**Requisitos previos**

Tenga en cuenta Hola siguiente requisito antes de empezar:

* Un clúster de HDInsight de Azure. Para obtener instrucciones, consulte [Introducción a HDInsight de Azure][hdinsight-get-started] o [Aprovisionamiento de clústeres de HDInsight][hdinsight-provision].

## <a name="why-blob-storage"></a>Motivos para almacenar blobs
Suelen ser clústeres de HDInsight de Azure implementa toorun trabajos de MapReduce y clústeres de Hola se quitan después de completan estos trabajos. Mantener datos de hello en clústeres HDFS hello cuando finalicen los cálculos sería un toostore forma costosa estos datos. Almacenamiento de blobs de Azure es una alta disponibilidad, altamente escalable y de alta capacidad, la opción de almacenamiento de bajo costo y pueden compartirse para datos que están toobe procesada con HDInsight. Almacenar datos en un blob permite clústeres de HDInsight de Hola que sirven para toobe cálculo publicado sin ningún riesgo sin pérdida de datos.

### <a name="directories"></a>Directorios
Los contenedores del almacenamiento de blobs de Azure almacenan los datos como pares de clave/valor y no hay jerarquía de directorios. Sin embargo Hola "/" caracteres pueden usarse en toomake de nombre de clave de hello parece como si un archivo se almacena en una estructura de directorios. HDInsight los ve como si fueran directorios reales.

Por ejemplo, la clave de un blob puede ser *input/log1.txt*. No existe ningún directorio de "entrada" real, pero debido a toohello presencia de hello carácter "/" en el nombre de clave de hello, tiene el aspecto de Hola de una ruta de acceso de archivo.

Por eso, si usa las herramientas de Azure Explorer, puede que vea algunos archivos de 0 bytes. Estos archivos tienen dos propósitos:

* Si hay carpetas vacías, marcadas de existencia de Hola de carpeta Hola. Almacenamiento de blobs de Azure es lo suficientemente inteligente tooknow que si existe un blob denominado foo/barra, hay una carpeta denominada **foo**. Pero Hola toosignify de manera única una carpeta vacía denominada **foo** es tener este archivo especial 0 bytes en su lugar.
* Contienen metadatos especial que es necesitan por hello Hadoop file systems, en particular los permisos de Hola y los propietarios de carpetas de Hola.

## <a name="command-line-utilities"></a>Utilidades de la ea de comandos
Microsoft proporciona Hola siguientes utilidades toowork con almacenamiento de blobs de Azure:

| Herramienta | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Interfaz de la línea de comandos de Azure][azurecli] |✔ |✔ |✔ |
| [Azure PowerShell][azure-powershell] | | |✔ |
| [AzCopy][azure-azcopy] | | |✔ |
| [Línea de comandos de Hadoop](#commandline) |✔ |✔ |✔ |

> [!NOTE]
> Mientras Hola CLI de Azure y Azure PowerShell, AzCopy todos pueden usarse desde fuera de Azure, hello Hadoop comando solo está disponible en el clúster de HDInsight de Hola y solo permite cargar datos de sistema de archivos local de hello en el almacenamiento de blobs de Azure.
>
>

### <a id="xplatcli"></a>Azure CLI
Hola CLI de Azure es una herramienta de multiplataforma que le permite toomanage Azure servicios. Usar hello siguiendo el almacenamiento de blobs de pasos tooupload datos tooAzure:

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. [Instalar y configurar Hola CLI de Azure para Mac, Linux y Windows](../cli-install-nodejs.md).
2. Abra un símbolo del sistema, bash u otro shell y usar hello después tooauthenticate tooyour suscripción de Azure.

        azure login

    Cuando se le solicite, escriba Hola nombre de usuario y una contraseña para su suscripción.
3. Escriba Hola después cuentas de almacenamiento de comando toolist Hola para su suscripción:

        azure storage account list
4. Seleccionar cuenta de almacenamiento de Hola que contiene datos de blob de Hola que desee toowork con y luego use Hola después la tecla de comando tooretrieve Hola para esta cuenta:

        azure storage account keys list <storage-account-name>

    Esto debería devolver las claves **Principal** y **Secundaria**. Hola copia **principal** valor de clave porque se usará en pasos de Hola.
5. Usar hello después comando tooretrieve una lista de contenedores de blob dentro de la cuenta de almacenamiento de hello:

        azure storage container list -a <storage-account-name> -k <primary-key>
6. Usar hello después tooupload de comandos y descargar archivos toohello blob:

   * tooupload un archivo:

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * toodownload un archivo:

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> Si siempre trabajará con hello misma cuenta de almacenamiento, puede establecer Hola después de las variables de entorno en lugar de especificar la cuenta de Hola y de clave para cada comando:
>
> * **AZURE\_almacenamiento\_cuenta**: nombre de cuenta de almacenamiento de Hola
> * **AZURE\_almacenamiento\_acceso\_clave**: clave de cuenta de almacenamiento de Hola
>
>

### <a id="powershell"></a>Azure PowerShell
Azure PowerShell es un entorno de scripting que puede usar toocontrol y automatizar la implementación de Hola y administración de las cargas de trabajo en Azure. Para obtener información acerca de cómo configurar su toorun de estación de trabajo Azure PowerShell, consulte [instalar y configurar Azure PowerShell](/powershell/azure/overview).

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

**tooupload un almacenamiento de blobs de tooAzure de archivos local**

1. Consola de Azure PowerShell Hola abiertos como se indica en [instalar y configurar Azure PowerShell](/powershell/azure/overview).
2. Establecer valores de hello de hello cinco primeras variables en hello siguiente secuencia de comandos:

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get hello storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create hello storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy hello file from local workstation toohello Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. Hola pegar en hello Azure PowerShell consola toorun se toocopy Hola los archivos de scripts.

Por ejemplo PowerShell toowork de scripts creados con HDInsight, vea [herramientas de HDInsight](https://github.com/blackmist/hdinsight-tools).

### <a id="azcopy"></a>AzCopy
AzCopy es una herramienta de línea de comandos que se haya diseñado toosimplify Hola tarea de transferencia de datos dentro y fuera de una cuenta de almacenamiento de Azure. Puede usarla como una herramienta independiente o incorporarla a una aplicación existente. [Descarga de AzCopy][azure-azcopy-download]

Hola AzCopy sintaxis es:

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

Para obtener más información, consulte [AzCopy: carga y descarga de archivos para blobs de Azure][azure-azcopy].

### <a id="commandline"></a>Línea de comandos de Hadoop
línea de comandos de Hadoop de Hello sólo es útil para almacenar datos en el almacenamiento de blobs al datos Hola ya están presentes en el nodo principal del clúster Hola.

Hola de orden toouse Hadoop comando, debe conectarse primero nodo principal de toohello mediante uno de los siguientes métodos de hello:

* **HDInsight para Windows**: [conectar mediante Escritorio remoto](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)
* **HDInsight basados en Linux**: conectarse a través de SSH ([Hola comando SSH](hdinsight-hadoop-linux-use-ssh-unix.md) o [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))

Una vez conectado, puede usar Hola después tooupload sintaxis toostorage de un archivo.

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

Por ejemplo: `hadoop fs -copyFromLocal data.txt /example/data/data.txt`

Como sistema de archivos predeterminado de Hola para HDInsight está en almacenamiento de blobs de Azure, /example/data.txt aparece realmente en almacenamiento de blobs de Azure. También puede consultar el archivo toohello como:

    wasb:///example/data/data.txt

o

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

Para obtener una lista de otros comandos de Hadoop que funcionan con archivos, consulte [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)

> [!WARNING]
> En los clústeres de HBase, tamaño de bloque predeterminado de hello usa al escribir los datos es de 256KB. Si bien esto funciona bien cuando se usa la API de REST o HBase APIs, utilizando hello `hadoop` o `hdfs dfs` datos de toowrite de comandos mayores de GB de ~ 12 genera un error. Vea hello [excepción de almacenamiento para la operación de escritura en el blob](#storageexception) sección para obtener más información.
>
>

## <a name="graphical-clients"></a>Clientes gráficos
También hay varias aplicaciones que proporcionan una interfaz gráfica para trabajar con el almacenamiento de Azure. Hola te mostramos una lista de algunas de estas aplicaciones:

| Cliente | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Microsoft Visual Studio Tools para HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |✔ |✔ |✔ |
| [Explorador de almacenamiento de Azure](http://storageexplorer.com/) |✔ |✔ |✔ |
| [Cloud Storage Studio 2](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |✔ |
| [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) | | |✔ |
| [Azure Explorer](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |✔ |
| [Cyberduck](https://cyberduck.io/) | |✔ |✔ |

### <a name="visual-studio-tools-for-hdinsight"></a>Visual Studio Tools para HDInsight
Para obtener más información, consulte [Navigate Hola recursos vinculados](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).

### <a id="storageexplorer"></a>Explorador de almacenamiento de Azure
*Explorador de almacenamiento de Azure* es una herramienta útil para inspeccionar y modificar datos de Hola de blobs. Se trata de una herramienta gratuita que se puede descargar de [http://storageexplorer.com/](http://storageexplorer.com/). código de Hello fuente está disponible en este vínculo también.

Antes de usar la herramienta de hello, debe conocer la clave de nombre y la cuenta de la cuenta de almacenamiento de Azure. Para obtener instrucciones sobre cómo obtener esta información, vea Hola "Cómo: ver, copiar y regenerar almacenamiento de claves de acceso" sección de [crear, administrar o eliminar una cuenta de almacenamiento][azure-create-storage-account].

1. Ejecute el explorador de almacenamiento de Azure. Si es Hola primera vez ha ejecutado Hola Explorador de almacenamiento, se le pedirá para hello **_Storage nombre-cuenta** y **clave de la cuenta de almacenamiento**. Si ha ejecutado con anterioridad, usar hello **agregar** botón tooadd un nuevo nombre de cuenta de almacenamiento y la clave.

    Escriba Hola nombre y clave de cuenta de almacenamiento de hello utilizada por el clúster de HDInsight y, a continuación, seleccione **Guardar & Abrir**.

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. En lista de hello de la izquierda de toohello de contenedores de interfaz de hello, haga clic en nombre de Hola Hola del contenedor de que está asociado a su clúster de HDInsight. De forma predeterminada, esto es nombre Hola Hola del clúster de HDInsight, pero puede ser diferente si ha especificado un nombre específico al crear el clúster de Hola.
3. Desde la barra de herramientas de hello, seleccione el icono de carga de Hola.

    ![Barra de herramientas con el icono de carga resaltado](./media/hdinsight-upload-data/toolbar.png)
4. Especificar un tooupload de archivo y, a continuación, haga clic en **abiertos**. Cuando se le pida, seleccione **cargar** raíz del toohello del archivo tooupload Hola Hola del contenedor de almacenamiento. Si desea tooupload Hola archivo tooa ruta de acceso específica, escriba la ruta de acceso de Hola Hola **destino** campo y, a continuación, seleccione **cargar**.

    ![Cuadro de diálogo de carga de archivos](./media/hdinsight-upload-data/fileupload.png)

    Una vez que ha finalizado la carga del archivo hello, puede usarlo desde trabajos en clúster de HDInsight Hola.

## <a name="mount-azure-blob-storage-as-local-drive"></a>Montar el almacenamiento de blobs de Azure como unidad local
Vea [Montaje del almacenamiento de blobs de Azure como unidad local](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).

## <a name="services"></a>Servicios
### <a name="azure-data-factory"></a>Azure Data Factory
Hola servicio Data Factory de Azure es un servicio completamente administrado para crear servicios de movimiento de datos, procesamiento de datos y almacenamiento de datos en las canalizaciones de producción de datos optimizado, escalable y confiable.

Factoría de datos de Azure pueden ser datos de toomove usado en el almacenamiento de blobs de Azure, o toocreate las canalizaciones de datos que utilizan directamente funciones HDInsight como Hive y Pig.

Para obtener más información, vea hello [documentación de Data Factory de Azure](https://azure.microsoft.com/documentation/services/data-factory/).

### <a id="sqoop"></a>Apache Sqoop
Sqoop es una herramienta diseñada tootransfer de datos entre bases de datos relacionales y de Hadoop. Puede usar lo tooimport datos desde un sistema de administración de bases de datos relacionales (RDBMS), como SQL Server, MySQL u Oracle en el sistema de archivos distribuido de Hadoop de hello (HDFS), transforme datos hello Hadoop MapReduce o subárbol y, a continuación, exportar datos de hello en un RDBMS.

Para obtener más información, consulte [Use Sqoop with Hadoop in HDInsight (Uso de Sqoop con HDInsight)][hdinsight-use-sqoop].

## <a name="development-sdks"></a>SDK de desarrollo
Almacenamiento de blobs de Azure también puede tener acceso mediante un SDK de Azure de hello después de los lenguajes de programación:

* .NET
* Java
* Node.js
* PHP
* Python
* Ruby

Para obtener más información acerca de cómo instalar hello Azure SDK, vea [descargas de Azure](https://azure.microsoft.com/downloads/)

## <a name="troubleshooting"></a>Solución de problemas
### <a id="storageexception"></a>Excepción de almacenamiento para escritura en blob
**Síntomas**: al usar hello `hadoop` o `hdfs dfs` comandos toowrite los archivos que son ~ 12 GB o mayores en un clúster de HBase, puede encontrar Hola siguiente error:

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: hello request body is too large and exceeds hello maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

**Causa**: tamaño de bloque predeterminado tooa de 256 KB de clústeres de HBase en HDInsight al escribir tooAzure almacenamiento. Si bien esto funciona para HBase APIs o las API de REST, se producirá un error cuando se usa hello `hadoop` o `hdfs dfs` utilidades de línea de comandos.

**Resolución**: Use `fs.azure.write.request.size` toospecify un tamaño de bloque. Puede hacerlo de forma por uso mediante el uso de hello `-D` parámetro. Hello aquí te mostramos un ejemplo de cómo utilizar este parámetro con hello `hadoop` comando:

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

También puede aumentar el valor de Hola de `fs.azure.write.request.size` global mediante el uso de Ambari. Hello siguientes pasos pueden resultar usar valor de hello toochange en hello Ambari Web UI:

1. En el explorador, vaya toohello Ambari Web UI para el clúster. Se trata de https://CLUSTERNAME.azurehdinsight.net, donde **CLUSTERNAME** es Hola nombre del clúster.

    Cuando se le solicite, escriba Hola administrador nombre y una contraseña para el clúster de Hola.
2. En la parte izquierda de la pantalla de bienvenida de hello, seleccione **HDFS**y, a continuación, seleccione hello **configuraciones** ficha.
3. Hola **filtro...**  , escriba `fs.azure.write.request.size`. Se mostrará el campo de Hola y el valor actual en medio de Hola de página Hola.
4. Cambie el valor de hello 262144 (256KB) toohello nuevo valor. Por ejemplo, 4194304 (4 MB).

![Imagen de cambiar el valor de Hola a través de la interfaz de usuario de Ambari Web](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

Para obtener más información sobre el uso de Ambari, consulte [administrar clústeres de HDInsight con hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).

## <a name="next-steps"></a>Pasos siguientes
Ahora que sabe cómo leer datos de tooget en HDInsight, Hola siguiendo artículos toolearn cómo tooperform analysis:

* [Introducción a Azure HDInsight][hdinsight-get-started]
* [Envío de trabajos de Hadoop mediante programación][hdinsight-submit-jobs]
* [Uso de Hive con HDInsight][hdinsight-use-hive]
* [Uso de Pig con HDInsight][hdinsight-use-pig]

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
