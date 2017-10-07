---
title: acceso de aaaRestrict mediante firmas de acceso compartido - HDInsight de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse firmas de acceso compartido toorestrict HDInsight acceso toodata almacenado en blobs de almacenamiento de Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a>Usar firmas de acceso compartido de almacenamiento de Azure toorestrict acceso toodata en HDInsight

HDInsight tiene acceso completo toodata en cuentas de almacenamiento de Azure de hello asociadas Hola clúster. Puede usar firmas de acceso compartido en los datos de hello blob contenedor toorestrict acceso toohello. Por ejemplo, tooprovide acceso de solo lectura toohello los datos. Las firmas de acceso compartido (SAS) son una característica de cuentas de almacenamiento de Azure que le permite toolimit acceso toodata. Por ejemplo, proporcionar toodata de acceso de solo lectura.

> [!IMPORTANT]
> Para una solución con Apache Ranger, considere la posibilidad de usar HDInsight unido a un dominio. Para obtener más información, vea hello [configurar Unidos al dominio HDInsight](hdinsight-domain-joined-configure.md) documento.

> [!WARNING]
> HDInsight debe tener el almacenamiento de acceso completo toohello predeterminado para el clúster de Hola.

## <a name="requirements"></a>Requisitos

* Una suscripción de Azure
* C# o Python. El código de ejemplo de C# se proporciona como una solución de Visual Studio.

  * Se debe usar la versión de Visual Studio 2013, 2015 o 2017
  * Se debe usar la versión de Python 2.7 o superior.

* Un clúster de HDInsight basados en Linux o [Azure PowerShell] [ powershell] -si tiene un clúster existente basada en Linux, puede usar Ambari tooadd un clúster de toohello de firma de acceso compartido. Si no es así, puede usar Azure PowerShell toocreate un clúster y agregar una firma de acceso compartido durante la creación del clúster.

    > [!IMPORTANT]
    > Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior. Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Hola archivos de ejemplo de [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature). Este repositorio incluye Hola siguientes elementos:

  * Un proyecto de Visual Studio que puede crear un contenedor de almacenamiento, una directiva almacenada y una SAS para su uso con HDInsight.
  * Un script de Python que puede crear un contenedor de almacenamiento, una directiva almacenada y una SAS para su uso con HDInsight.
  * Un script de PowerShell que puede crear un HDInsight de clúster y configurar toouse Hola SAS.

## <a name="shared-access-signatures"></a>Las firmas de acceso compartido

Hay dos formas de firmas de acceso compartido:

* Ad hoc: Hola hora de inicio, la hora de expiración y permisos para hello SAS se especifican en hello URI de SAS.

* Directiva de acceso almacenada: se define una directiva de acceso almacenada en un contenedor de recursos, como un contenedor de blobs. Una directiva puede tener restricciones toomanage usado para una o varias firmas de acceso compartido. Al asociar una SAS con una directiva de acceso almacenada, Hola SAS hereda las restricciones de hello: Hola hora de inicio, la hora de expiración y permisos - definidos para la directiva de acceso de hello almacenado.

Hello diferencia entre Hola dos formatos es importante para un escenario clave: revocación. Una SAS es una dirección URL, por lo que cualquier persona que obtiene Hola SAS puede utilizar, independientemente de quién lo ha solicitado toobegin con. Si una SAS se publica públicamente, se puede utilizar cualquier usuario de Hola a todos. Una SAS distribuida es válida hasta que se produzca una de las cuatro situaciones:

1. hora de expiración de Hello especificado en hello que SAS se alcanza.

2. hora de expiración de Hello especificado en la directiva de acceso de hello almacenado al que hace referencia Hola que SAS se alcanza. los escenarios siguientes Hello causa un tiempo de expiración hello toobe alcanzado:

    * ha transcurrido el intervalo de tiempo de saludo.
    * Directiva de acceso de Hello almacenado es toohave modificado una hora de expiración en hello anterior. Al cambiar la hora de expiración de hello es una manera de toorevoke Hola SAS.

3. Hola almacenado al que hace referencia Hola que SAS se elimina, que es hello de toorevoke de otra manera SAS de directiva de acceso. Si vuelve a crear la directiva de acceso Hola almacenado con hello mismo nombre, todos los tokens SAS de directiva anterior Hola son válidos (si no ha superado la hora de expiración de hello en hello SAS). Si piensa toorevoke Hola SAS, ser seguro toouse un nombre diferente si vuelve a crear la directiva de acceso Hola con una hora de expiración en hello futuras.

4. clave de la cuenta de Hello que estaba toocreate usado Hola SAS se vuelve a generar. Regenerando la clave de hello hace que todas las aplicaciones que usan la autenticación de clave toofail anterior Hola. Actualizar todos los componentes toohello nueva clave.

> [!IMPORTANT]
> Un URI de firma de acceso compartido está asociado a la firma de hello cuenta clave toocreate usado Hola y Hola asociados directiva de acceso almacenada (si existe). Si no se especifica ninguna directiva de acceso almacenada, hello toorevoke de manera sólo firma de acceso compartido es toochange Hola cuenta clave.

Se recomienda usar siempre las directivas de acceso almacenadas. Al utilizar las directivas almacenadas, puede revocar las firmas o ampliar la fecha de expiración de hello según sea necesario. pasos de Hello en este documento utiliza toogenerate de directivas de acceso almacenada SAS.

Para obtener más información sobre firmas de acceso compartido, consulte [modelo SAS de descripción hello](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

### <a name="create-a-stored-policy-and-sas-using-c"></a>Creación de una directiva almacenada y una SAS mediante C\#

1. Abra la solución de hello en Visual Studio.

2. En el Explorador de soluciones, haga doble clic en hello **SASToken** de proyecto y seleccione **propiedades**.

3. Seleccione **configuración** y agregue los valores de hello siguientes entradas:

   * StorageConnectionString: Hola cadena de conexión de cuenta de almacenamiento de Hola que desea que toocreate una directiva almacenada y la SAS para. Hola formato debe ser `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` donde `myaccount` es Hola nombre de la cuenta de almacenamiento y `mykey` es clave Hola Hola cuenta de almacenamiento.

   * ContainerName: contenedor de hello de cuenta de almacenamiento de Hola que desee tener acceso toorestrict a.

   * SASPolicyName: Hola nombre toouse para hello almacena toocreate de directiva.

   * FileToUpload: ruta de acceso tooa archivo hello que es cargado toohello contenedor.

4. Ejecute el proyecto de Hola. Información toohello similar después de texto se muestra una vez que se ha generado Hola SAS:

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Guarde el token de directiva SAS de hello, el nombre de la cuenta de almacenamiento y el nombre del contenedor. Estos valores se utilizan al asociar la cuenta de almacenamiento de Hola a su clúster de HDInsight.

### <a name="create-a-stored-policy-and-sas-using-python"></a>Creación de una directiva almacenada y una SAS mediante Python

1. Abrir archivo SASToken.py de hello y cambiar Hola siguientes valores:

   * directiva\_nombre: Hola nombre toouse para hello almacenado toocreate de directiva.

   * almacenamiento\_cuenta\_nombre: nombre de hello de la cuenta de almacenamiento.

   * almacenamiento\_cuenta\_clave: Hola clave Hola cuenta de almacenamiento.

   * almacenamiento\_contenedor\_nombre: contenedor Hola de cuenta de almacenamiento de Hola que desee tener acceso toorestrict a.

   * en el ejemplo se\_archivo\_ruta de acceso: Hola ruta tooa archivo que es cargado toohello contenedor.

2. Ejecutar script de Hola. Muestra hello SAS token similar toohello después de texto cuando se completa el script de Hola:

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Guarde el token de directiva SAS de hello, el nombre de la cuenta de almacenamiento y el nombre del contenedor. Estos valores se utilizan al asociar la cuenta de almacenamiento de Hola a su clúster de HDInsight.

## <a name="use-hello-sas-with-hdinsight"></a>Usar SAS Hola con HDInsight

Al crear un clúster de HDInsight, debe especificar una cuenta de almacenamiento principal y puede especificar, opcionalmente, cuentas de almacenamiento adicionales. Ambos métodos de adición de almacenamiento requieren cuentas de almacenamiento de toohello de acceso completo y contenedores que se utilizan.

toouse un contenedor tooa de acceso de toolimit de firma de acceso compartido, agregar una entrada personalizada toohello **core sitio** configuración de clúster de Hola.

* Para **basados en Windows** o **basados en Linux** clústeres de HDInsight, puede agregar la entrada de Hola durante su creación mediante PowerShell.
* Para **basados en Linux** clústeres de HDInsight, cambiar la configuración de hello después de la creación de clúster con Ambari.

### <a name="create-a-cluster-that-uses-hello-sas"></a>Crear un clúster que usa Hola SAS

Un ejemplo de creación de un clúster de HDInsight que hello usa SAS se incluye en hello `CreateCluster` directorio del repositorio de Hola. toouse, Hola de uso después avanza:

1. Abra hello `CreateCluster\HDInsightSAS.ps1` archivo en un editor de texto y modifique Hola siguiente valores al principio de saludo del documento de Hola.

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    Por ejemplo, cambiar `'mycluster'` toohello nombre del clúster de Hola que desea toocreate. valores de Hello SAS deben coincidir con valores de hello de los pasos anteriores de hello al crear una cuenta de almacenamiento y el token de SAS.

    Una vez que han cambiado los valores de hello, guarde el archivo de Hola.

2. Abra un nuevo símbolo del sistema de Azure PowerShell. Si no está familiarizado con Azure PowerShell, o si no lo ha instalado, consulte [Cómo instalar y configurar Azure PowerShell][powershell].

1. Desde el símbolo del sistema de hello, utilice Hola después comando tooauthenticate tooyour suscripción de Azure:

    ```powershell
    Login-AzureRmAccount
    ```

    Cuando se le solicite, inicie sesión con la cuenta de hello para la suscripción de Azure.

    Si su cuenta está asociada a varias suscripciones de Azure, puede que necesite toouse `Select-AzureRmSubscription` suscripción de hello tooselect desea toouse.

4. Desde el símbolo del sistema de hello, cambiar directorios toohello `CreateCluster` directorio que contiene el archivo de hello HDInsightSAS.ps1. A continuación, usar hello sigue la secuencia de comandos de hello toorun

    ```powershell
    .\HDInsightSAS.ps1
    ```

    Durante la ejecución de secuencias de comandos hello, registra el símbolo del sistema de salida toohello PowerShell mientras crea recursos Hola cuentas de grupo y de almacenamiento. Eres usuario de hello HTTP tooenter solicitadas para hello clúster de HDInsight. Esta cuenta es el clúster de toohello de acceso HTTP/s toosecure usado.

    Si está creando un clúster basado en Linux, se le solicitará un nombre de cuenta de usuario SSH y una contraseña. Esta cuenta es registro tooremotely usado en clúster toohello.

   > [!IMPORTANT]
   > Cuando se le solicite Hola HTTP/s o SSH nombre de usuario y contraseña, debe proporcionar una contraseña que cumpla Hola siguiendo criterios:
   >
   > * Debe tener como mínimo 10 caracteres.
   > * Debe contener al menos un dígito.
   > * Debe incluir al menos un carácter no alfanumérico.
   > * Debe contener al menos una mayúscula o una minúscula.

Se tarda un tiempo para este toocomplete de secuencia de comandos, normalmente unos 15 minutos. Cuando se completa en el script de Hola sin errores, se ha creado el clúster de Hola.

### <a name="use-hello-sas-with-an-existing-cluster"></a>Usar SAS Hola con un clúster existente

Si tiene un clúster existente basada en Linux, puede agregar Hola SAS toohello **core sitio** configuración mediante el uso de hello pasos:

1. Abra hello Ambari web interfaz de usuario para el clúster. Hola una dirección de esta página es https://YOURCLUSTERNAME.azurehdinsight.net. Cuando se le solicite, autenticar clúster toohello con nombre de administrador de hello (admin) y contraseña que ha utilizado al crear el clúster de Hola.

2. En hello parte izquierda de la interfaz de usuario de web de Ambari hello, seleccione **HDFS** y, a continuación, seleccione hello **configuraciones** ficha en medio de Hola de página Hola.

3. Seleccione hello **avanzadas** ficha y, a continuación, desplácese hasta que encuentre hello **personalizado core-sitio** sección.

4. Expanda hello **personalizado core-sitio** sección, a continuación, final de desplazamiento toohello y seleccione hello **Agregar propiedad... ** vínculo. Los valores siguientes de Hola de uso para hello **clave** y **valor** campos:

   * **Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net
   * **Valor**: Hola SAS devolviendo Hola aplicación de C# o Python haya ejecutado anteriormente

     Reemplace **CONTAINERNAME** con el nombre del contenedor de Hola usó con la aplicación de C# o SAS de hello. Reemplace **STORAGEACCOUNTNAME** con nombre de la cuenta de almacenamiento Hola ha usado.

5. Haga clic en hello **agregar** toosave esta clave y valor, a continuación, haga clic en hello **guardar** botón cambios de configuración de toosave Hola. Cuando se le pida, agregue una descripción de cambio de hello ("Agregar acceso de almacenamiento SAS" por ejemplo) y, a continuación, haga clic en **guardar**.

    Haga clic en **Aceptar** cuando se hayan completado los cambios de Hola.

   > [!IMPORTANT]
   > Debe reiniciar varios servicios para que hello cambio surta efecto.

6. En la interfaz de usuario del web Ambari hello, seleccione **HDFS** en lista de Hola Hola izquierda y, a continuación, seleccione **reiniciar todos los** de hello **acciones de servicio** lista desplegable lista de hello derecho. Cuando se le solicite, seleccione **Turn on maintenance mode** (Activar modo de mantenimiento) y, a continuación, "Confirm Restart All" ("Confirmar reiniciar todo").

    Repita este proceso para MapReduce2 y YARN.

7. Una vez que se hayan reiniciado los servicios de hello, seleccione cada uno de ellos y deshabilitar el modo de mantenimiento de hello **acciones de servicio** de lista desplegable.

## <a name="test-restricted-access"></a>Prueba de acceso restringido

tooverify que ha restringido el acceso, Hola de uso siguientes métodos:

* Para **basados en Windows** clústeres de HDInsight, use el clúster de toohello tooconnect de escritorio remoto. Para obtener más información, consulte [conectar tooHDInsight mediante RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

    Una vez conectado, usar hello **Hadoop de línea de comandos** icono en hello escritorio tooopen un símbolo del sistema.

* Para **basados en Linux** clústeres de HDInsight, utilizar SSH tooconnect toohello clúster. Para más información, consulte [Uso SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Una vez conectado toohello clúster, use Hola después tooverify pasos que sólo se pueden leer y mostrar elementos en la cuenta de almacenamiento SAS hello:

1. contenido de hello toolist del contenedor de hello, utilice Hola siguiente comando desde el símbolo del sistema de hello: 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    Reemplace **SASCONTAINER** con nombre hello del contenedor de hello creado para la cuenta de almacenamiento SAS Hola. Reemplace **SASACCOUNTNAME** con el nombre de Hola de cuenta de almacenamiento de hello usada para hello SAS.

    lista de Hello incluye archivo hello cargado cuando se creó el contenedor de Hola y SAS.

2. Usar hello después tooverify de comando que se puede leer el contenido de hello del archivo hello. Reemplace hello **SASCONTAINER** y **SASACCOUNTNAME** como en el paso anterior de Hola. Reemplace **FILENAME** con nombre de hello del archivo de hello muestra en el comando anterior hello:

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    Este comando muestra el contenido de Hola de archivo hello.

3. Usar hello después de sistema de archivos local de comando toodownload Hola archivo toohello:

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    Este comando descargas Hola tooa archivo local denominado **testfile.txt**.

4. Siguiente Hola de uso del comando tooupload Hola archivo local tooa nuevo archivo denominado **testupload.txt** en hello almacenamiento SAS:

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    Recibirá un toohello similar de mensaje siguiente texto:

        put: java.io.IOException

    Este error se produce debido a la ubicación de almacenamiento de hello lectura + lista solo. Usar hello siguiente datos de hello tooput de comando de almacenamiento predeterminado de hello para el clúster hello, que se puede escribir:

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    En esta ocasión, operación Hola debe completarse correctamente.

## <a name="troubleshooting"></a>Solución de problemas

### <a name="a-task-was-canceled"></a>Se ha cancelado una tarea

**Síntomas**: al crear un clúster con la secuencia de comandos de PowerShell de hello, es posible que reciba Hola mensaje de error siguiente:

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

**Causa**: este error puede producirse si usa una contraseña de usuario de administrador/HTTP hello para el clúster de Hola o (para los clústeres basados en Linux) usuario SSH Hola.

**Resolución**: usar una contraseña que cumpla Hola siguiendo criterios:

* Debe tener como mínimo 10 caracteres.
* Debe contener al menos un dígito.
* Debe incluir al menos un carácter no alfanumérico.
* Debe contener al menos una mayúscula o una minúscula.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha aprendido cómo tooadd almacenamiento limitado con acceso tooyour clúster de HDInsight, obtenga información acerca de otro toowork formas con datos en el clúster:

* [Uso de Hive con HDInsight](hdinsight-use-hive.md)
* [Uso de Pig con HDInsight](hdinsight-use-pig.md)
* [Uso de MapReduce con HDInsight](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
