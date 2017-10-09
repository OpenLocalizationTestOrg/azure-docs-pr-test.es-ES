---
título: aaa "PowerShell: clúster de HDInsight de Azure con el almacén de Data Lake como almacenamiento adicional | Servicios de Microsoft Docs":-: almacén de data lake, hdinsight documentationcenter: '' autor: nitinme manager: editor jhubbard: cgronlun

MS.AssetId: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: almacén de data lake ms.devlang: na ms.topic: artículo ms.tgt_pltfrm: na ms.workload: ms.date de grandes cantidades de datos: 06/08/2017 ms.author: nitinme

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a>Use toocreate un clúster de HDInsight de Azure PowerShell con almacén de Data Lake (como almacenamiento adicional)
> [!div class="op_single_selector"]
> * [Uso del Portal](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Uso de PowerShell (para el almacenamiento predeterminado)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Uso de PowerShell (para el almacenamiento adicional)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Uso de Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Obtenga información acerca de cómo toouse Azure PowerShell tooconfigure un HDInsight de clúster con el almacén de Azure Data Lake **como almacenamiento adicional**. Para obtener instrucciones sobre cómo toocreate una HDInsight de clúster con el almacén de Data Lake de Azure como almacenamiento predeterminado, consulte [crear un clúster de HDInsight con el almacén de Data Lake como almacenamiento predeterminado](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).

> [!NOTE]
> Si va a almacén de toouse Azure Data Lake como almacenamiento adicional para el clúster de HDInsight, se recomienda hacer esto al crear el clúster de hello tal como se describe en este artículo. Agregar almacén de Azure Data Lake como almacenamiento adicional tooan clúster de HDInsight existente es un proceso complicado y propensa a tooerrors.
>

En el caso de los tipos de clúster compatibles, Data Lake Store se puede usar como almacenamiento predeterminado o como cuenta de almacenamiento adicional. Cuando se utiliza el almacén de Data Lake como almacenamiento adicional, cuenta de almacenamiento predeterminada de Hola para clústeres de hello seguirán estando Blobs de almacenamiento de Azure (WASB) y archivos relacionados con el clúster de hello (por ejemplo, registros, etc.) se escriben todavía almacenamiento predeterminado de toohello, mientras que los datos de Hola que desea tooprocess pueden almacenarse en una cuenta de almacén de Data Lake. Usar almacén de Data Lake como una cuenta de almacenamiento adicional no afecta a rendimiento u Hola capacidad tooread/escritura toohello almacenamiento Hola clúster.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>Uso de Data Lake Store para el almacenamiento de clústeres de HDInsight

Estas son algunas consideraciones importantes que deben tenerse en cuenta al usar HDInsight con Data Lake Store:

* Clústeres de HDInsight de toocreate opción con acceso tooData Lake almacén como almacenamiento adicional está disponible para las versiones 3.2, 3.4, 3.5 y 3.6 de HDInsight.

Configuración de HDInsight toowork con el almacén de Data Lake con PowerShell implica Hola pasos:

* Creación de un Almacén de Azure Data Lake
* Configure la autenticación para basada en roles acceder tooData Lake almacén
* Crear el clúster de HDInsight con el almacén de autenticación tooData Lake
* Ejecutar un trabajo de prueba en el clúster de Hola

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, debe tener el siguiente hello:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 o versiones posteriores**. Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).
* **Windows SDK**. Puede instalarlo desde [aquí](https://dev.windows.com/en-us/downloads). Utilice este toocreate un certificado de seguridad.
* **Entidad de servicio de Azure Active Directory** Pasos de este tutorial proporcionan instrucciones sobre cómo toocreate una entidad de servicio en Azure AD. Sin embargo, debe ser un toocreate capaz de Azure AD administrador toobe una entidad de servicio. Si eres un administrador de Azure AD, puede omitir este requisito previo y continuar con tutorial Hola.

    **Si no es un administrador de Azure AD**, no será capaz de tooperform Hola pasos necesarios toocreate una entidad de servicio. En este caso, su administrador de Azure AD debe generar primero una entidad de servicio antes de crear un clúster de HDInsight con Data Lake Store. Además, entidad de servicio de hello debe crearse con un certificado, como se describe en [crear una entidad de servicio con el certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).

## <a name="create-an-azure-data-lake-store"></a>Creación de un Almacén de Azure Data Lake
Siga estos toocreate pasos un almacén de Data Lake.

1. Desde el escritorio, abra una nueva ventana de PowerShell de Azure y escriba el siguiente fragmento de código de hello. Cuando toolog solicitada, asegúrese de que inicie sesión como un administrador o propietario de la suscripción de hello:

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > Si recibe un mensaje de error similar demasiado`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` al registrar el proveedor de recursos de almacén de Data Lake hello, es posible que la suscripción no está permitido para el almacén de Azure Data Lake. Asegúrese de habilitar su suscripción de Azure en la versión preliminar pública de Data Lake Store siguiendo estas [instrucciones](data-lake-store-get-started-portal.md).
   >
   >
2. La cuenta de Almacén de Azure Data Lake se asocia con un grupo de recursos de Azure. Comience creando un grupo de recursos de Azure.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    La salida debe ser parecida a la siguiente:

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Cree una cuenta de Almacén de Azure Data Lake. cuenta de Hello nombre que especifique debe contener solo letras minúsculas y números.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    Debería ver una salida similar Hola siguiente:

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

5. Cargar algunos tooAzure de datos de ejemplo Data Lake. Vamos a usar más adelante en este tooverify de artículo que datos de hello sean accesibles desde un clúster de HDInsight. Si desea obtener algunos tooupload de datos de ejemplo, puede obtener hello **ambulancia datos** carpeta de hello [repositorio de Git de Azure datos Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>Configure la autenticación para basada en roles acceder tooData Lake almacén
Cada una de las suscripciones de Azure está asociada a un Azure Active Directory. Los usuarios y servicios que tienen acceso a recursos de suscripción de hello mediante el Portal de Azure clásico de Hola o API de administrador de recursos de Azure deben autenticarse primero con la que Azure Active Directory. Se concede acceso tooAzure suscripciones y servicios mediante la asignación de rol adecuado de hello en un recurso de Azure.  Para los servicios, una entidad de servicio identifica servicio Hola Hola Azure Active Directory (AAD). Esta sección muestra cómo toogrant una aplicación de servicio, como HDInsight, tooan de acceso a recursos de Azure (Hola cuenta de almacén de Data Lake de Azure que creó anteriormente) al crear una entidad de servicio para la aplicación hello y asignarles roles toothat a través de Azure PowerShell.

tooset la autenticación de Active Directory para Data Lake de Azure, debe realizar Hola siguiente las tareas.

* Creación de un certificado autofirmado
* Creación de una aplicación en Azure Active Directory y una entidad de servicio

### <a name="create-a-self-signed-certificate"></a>Creación de un certificado autofirmado
Asegúrese de que tiene [Windows SDK](https://dev.windows.com/en-us/downloads) instalado antes de continuar con hello pasos de esta sección. Debe también ha creado un directorio, como **C:\mycertdir**, donde se creará el certificado de Hola.

1. Desde la ventana de PowerShell de hello, navegue ubicación toohello donde se instaló el SDK de Windows (normalmente, `C:\Program Files (x86)\Windows Kits\10\bin\x86` y usar hello [MakeCert] [ makecert] toocreate utilidad un certificado autofirmado y un clave privada. Usar hello siga los comandos.

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    Es posible que la contraseña de clave privada tooenter solicitadas Hola. Después de comando de Hola se ejecuta correctamente, debería ver un **CertFile.cer** y **mykey.pvk** en directorio de hello certificado especificado.
2. Hola de uso [Pvk2Pfx] [ pvk2pfx] utilidad tooconvert Hola .pvk y .cer archivos archivo .pfx MakeCert tooa creado. Ejecutar el siguiente comando de Hola.

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    Cuando se le solicite escribir contraseña de clave privada de hello especificado anteriormente. Hola valor especificado en hello **-po** parámetro es la contraseña de Hola que está asociado con el archivo .pfx de Hola. Después de que se complete correctamente el comando hello, también verá un CertFile.pfx en directorio de hello certificado especificado.

### <a name="create-an-azure-active-directory-and-a-service-principal"></a>Creación de una aplicación en Azure Active Directory y una entidad de servicio
En esta sección, realizar pasos de hello toocreate una entidad de servicio para una aplicación de Azure Active Directory, asignar a una entidad de servicio de rol toohello y autenticarse como entidad de servicio de hello proporcionando un certificado. Ejecutar Hola después toocreate de comandos en una aplicación en Azure Active Directory.

1. Pegue Hola siguientes cmdlets en la ventana de consola de PowerShell de hello. Asegúrese de que valor Hola que especifique para hello **- DisplayName** propiedad es única. Además, Hola valores para **- página principal** y **- IdentiferUris** son valores de marcador de posición y no se comprueban.

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. Crear a una entidad de servicio con Id. de aplicación Hola.

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. Conceda carpeta de almacén de Data Lake del toohello de acceso principal de servicio de Hola y archivo hello que tendrá acceso de clúster de HDInsight Hola. fragmento de código de Hello siguiente proporciona raíz de toohello de acceso del programa Hola a almacén de Data Lake (donde haya copiado el archivo de datos de ejemplo de Hola) de la cuenta y Hola propio archivo.

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a>Creación de un clúster de HDInsight en Linux con Data Lake Store como almacenamiento adicional

En esta sección, se creará un clúster de Hadoop en HDInsight basado en Linux con Data Lake Store como almacenamiento adicional. En esta versión, clúster de HDInsight de Hola y Hola almacén de Data Lake deben estar en hello misma ubicación.

1. Iniciar al recuperar el identificador del inquilino de suscripción de Hola. Lo necesitará más adelante.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. En esta versión, para un clúster de Hadoop, almacén de Data Lake solo sirve como un almacenamiento adicional para el clúster de Hola. almacenamiento predeterminado de Hello seguirán siendo blobs hello en el almacenamiento de Azure (WASB). Por lo tanto, primero crearemos Hola contenedores de almacenamiento y la cuenta de almacenamiento necesarios para el clúster de Hola.

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. Crear el clúster de HDInsight de Hola. Usar hello siguientes cmdlets.

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    Después de que se complete correctamente el cmdlet de hello, debería ver una salida de hello clúster detalles del anuncio.


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Ejecutar trabajos de prueba en Hola de toouse de clúster de HDInsight de hello almacén de Data Lake
Después de haber configurado un clúster de HDInsight, se puede ejecutar trabajos de prueba en hello clúster tootest ese hello HDInsight clúster puede tener acceso a almacén de Data Lake. toodo por lo tanto, se ejecutará un trabajo de Hive de ejemplo que crea una tabla con datos de ejemplo de Hola que cargan almacén de Data Lake de tooyour anteriores.

En esta sección aprenderá lo SSH en hello HDInsight Linux de clúster que ha creado y ejecutar una consulta de Hive de ejemplo de Hola.

* Si está usando un tooSSH de cliente de Windows en clúster de hello, consulte [utilizar SSH con Linux-based Hadoop en HDInsight de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Si está usando un tooSSH de cliente de Linux en clúster de hello, consulte [utilizar SSH con Linux-based Hadoop en HDInsight de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

1. Una vez conectado, inicie Hola Hive CLI mediante Hola siguiente comando:

        hive
2. Hola CLI, escriba Hola siguiendo las instrucciones toocreate una nueva tabla denominada **vehículos** mediante el uso de datos de ejemplo de Hola Hola almacén de Data Lake:

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    Debería ver un siguiente toohello similar de salida:

        1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
        1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
        1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
        1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
        1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
        1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
        1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
        1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
        1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
        1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1

## <a name="access-data-lake-store-using-hdfs-commands"></a>Acceso al Almacén de Data Lake mediante comandos de HDFS
Una vez haya configurado el almacén de hello HDInsight clúster toouse Data Lake, puede usar comandos de shell de hello HDFS tooaccess Hola almacén.

En esta sección aprenderá lo SSH en hello HDInsight Linux de clúster que ha creado y ejecutar comandos HDFS Hola.

* Si está usando un tooSSH de cliente de Windows en clúster de hello, consulte [utilizar SSH con Linux-based Hadoop en HDInsight de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Si está usando un tooSSH de cliente de Linux en clúster de hello, consulte [utilizar SSH con Linux-based Hadoop en HDInsight de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)

Una vez conectado, use Hola siguientes archivos HDFS filesystem comando toolist Hola Hola almacén de Data Lake.

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

Esto debería incluir archivo hello que cargan almacén de Data Lake de toohello anteriores.

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

También puede usar hello `hdfs dfs -put` comando tooupload algunos toohello archivos del almacén de Data Lake y, a continuación, usar `hdfs dfs -ls` tooverify si los archivos de saludo se cargaron correctamente.

## <a name="see-also"></a>Otras referencias
* [Portal: Crear un toouse de clúster de HDInsight almacén de Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
