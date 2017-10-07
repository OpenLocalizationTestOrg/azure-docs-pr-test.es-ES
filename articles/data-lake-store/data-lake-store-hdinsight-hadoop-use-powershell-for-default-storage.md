---
title: "clústeres de HDInsight aaaCreate con almacén de Data Lake como almacenamiento predeterminado mediante PowerShell | Documentos de Microsoft"
description: "Utilice toocreate de PowerShell de Azure y clústeres de HDInsight con el almacén de Azure Data Lake"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a>Creación de clústeres de HDInsight con Data Lake Store como almacenamiento predeterminado mediante PowerShell
> [!div class="op_single_selector"]
> * [Usar hello portal de Azure](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Uso de PowerShell (para el almacenamiento predeterminado)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Uso de PowerShell (para almacenamiento adicional)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Uso de Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

Obtenga información acerca de cómo clústeres toouse tooconfigure de PowerShell de Azure HDInsight de Azure con Azure almacén de Data Lake, como almacenamiento predeterminado. Para obtener instrucciones sobre la creación de un clúster de HDInsight con Azure Data Lake Store como almacenamiento adicional, consulte [Uso de Azure PowerShell para crear clústeres de HDInsight con Data Lake Store (como almacenamiento adicional)](data-lake-store-hdinsight-hadoop-use-powershell.md).

Estas son algunas consideraciones importantes que deben tenerse en cuenta al usar HDInsight con Data Lake Store:

* clústeres de HDInsight de Hello opción toocreate con acceso tooData Lake almacén como almacenamiento predeterminado está disponible para HDInsight versión 3.5 y 3.6.

* Hola opción toocreate clústeres de HDInsight con acceso tooData Lake almacén como almacenamiento predeterminado es *no está disponible* para los clústeres de HDInsight Premium.

tooconfigure toowork de HDInsight con el almacén de Data Lake con PowerShell, siga las instrucciones de hello en las secciones siguientes cinco de Hola.

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar este tutorial, asegúrese de que se cumple Hola según los requisitos:

* **Una suscripción de Azure**: vaya demasiado[evaluación gratuita de Azure obtener](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 o mayor**: vea [cómo tooinstall y configurar PowerShell](/powershell/azure/overview).
* **Kit de desarrollo de Software (SDK) de Windows**: tooinstall SDK de Windows, vaya demasiado[descarga y las herramientas para Windows 10](https://dev.windows.com/en-us/downloads). Hola SDK es toocreate usa un certificado de seguridad.
* **Entidad de servicio de Azure Active Directory**: en este tutorial se describe cómo toocreate una entidad de servicio en Azure Active Directory (Azure AD). Sin embargo, toocreate una entidad de servicio, debe ser un administrador de Azure AD. Si es administrador, puede omitir este requisito previo y continuar con tutorial Hola.

    >[!NOTE]
    >Solamente puede crear una entidad de servicio si es administrador de Azure AD. Su administrador de Azure AD debe generar una entidad de servicio antes de crear un clúster de HDInsight con Data Lake Store. Hello entidad de servicio debe crearse con un certificado, como se describe en [crear una entidad de servicio con el certificado](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).
    >

## <a name="create-a-data-lake-store-account"></a>Crear una cuenta de Almacén de Data Lake
toocreate una cuenta de almacén de Data Lake Hola siguientes:

1. Desde el escritorio, abra una ventana de PowerShell y, a continuación, escriba los siguientes fragmentos de Hola. Cuando esté toosign solicitada en Inicio de sesión como uno de los administradores de suscripciones de Hola o propietarios. 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > Si registrar proveedor de recursos de almacén de Data Lake hello y recibe un mensaje de error similar demasiado`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, su suscripción no estén en la lista blanca para almacén de Data Lake. tooenable su suscripción de Azure para preview pública de almacén de Data Lake de hello, siga las instrucciones de hello en [empezar a trabajar con el almacén de Azure Data Lake utilizando Hola portal de Azure](data-lake-store-get-started-portal.md).
    >

2. Una cuenta de Data Lake Store se asocia con un grupo de recursos de Azure. Comience a crear un grupo de recursos.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    La salida debe ser parecida a la siguiente:

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. Cree una cuenta de Data Lake Store. cuenta de Hello nombre que especifique debe contener solo letras minúsculas y números.

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

4. El uso de almacén de Data Lake como almacenamiento predeterminado requiere toospecify que una ruta de acceso los raíz toowhich Hola específicos para clúster archivos se copian durante la creación del clúster. una ruta de acceso raíz, que es toocreate **/clústeres/hdiadlcluster** en el fragmento de código de hello, usar hello siguientes cmdlets:

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a>Configure la autenticación para basada en roles acceder tooData Lake almacén
Cada una de las suscripciones de Azure está asociada a una entidad de Azure AD. Los usuarios y servicios que acceder a los recursos de suscripción mediante el uso de Hola portal de Azure u Hola API del Administrador de recursos de Azure deben autenticarse primero con Azure AD. Se concede acceso tooAzure suscripciones y servicios mediante la asignación de rol adecuado de hello en un recurso de Azure. Servicios, una entidad de servicio identifica el servicio de hello en Azure AD.

Esta sección muestra cómo service toogrant una aplicación, por ejemplo, HDInsight, tooan de acceso a recursos de Azure (Hola cuenta de almacén de Data Lake que creó anteriormente). La forma de hacerlo es mediante la creación de un servicio principal para la aplicación hello y asignación de roles tooit a través de PowerShell.

tooset la autenticación de Active Directory para Azure Data Lake, realizar tareas de Hola Hola siguientes dos secciones.

### <a name="create-a-self-signed-certificate"></a>Creación de un certificado autofirmado
Asegúrese de que tiene [Windows SDK](https://dev.windows.com/en-us/downloads) instalado antes de continuar con hello pasos de esta sección. Debe también ha creado un directorio, como *C:\mycertdir*, donde crear certificado Hola.

1. Desde la ventana de PowerShell de hello, vaya ubicación toohello donde se instaló el SDK de Windows (normalmente, *C:\Program Files (x86) \Windows Kits\10\bin\x86*) y usar hello [MakeCert] [ makecert] toocreate utilidad un certificado autofirmado y una clave privada. Usar hello siguientes comandos:

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    Es posible que la contraseña de clave privada tooenter solicitadas Hola. Después de que el comando de Hola se ejecuta correctamente, debería ver **CertFile.cer** y **mykey.pvk** en directorio de certificado de Hola que especificó.
2. Hola de uso [Pvk2Pfx] [ pvk2pfx] utilidad tooconvert Hola .pvk y .cer archivos archivo .pfx MakeCert tooa creado. Ejecute el siguiente comando de hello:

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    Cuando se le pida, escriba Hola contraseña de clave privada que especificó anteriormente. Hola valor especificado en hello **-po** parámetro es la contraseña de Hola que esté asociada con el archivo .pfx de hello. Una vez se ha completado correctamente el comando hello, también debería observar una **CertFile.pfx** en directorio de certificado de Hola que especificó.

### <a name="create-an-azure-ad-and-a-service-principal"></a>Creación de una aplicación en Azure AD y una entidad de servicio
En esta sección, cree a una entidad de servicio para una aplicación de Azure AD, asignar a una entidad de servicio de rol toohello y autenticarse como entidad de servicio de hello proporcionando un certificado. toocreate una aplicación en Azure AD, ejecute hello siguientes comandos:

1. Pegue Hola siguientes cmdlets en la ventana de consola de PowerShell de hello. Asegúrese de que ese valor de Hola que especifique para hello **- DisplayName** propiedad es única. Hola valores para **- página principal** y **- IdentiferUris** son valores de marcador de posición y no se comprueban.

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
2. Crear a una entidad de servicio mediante el uso de Id. de aplicación Hola.

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. Conceda raíz del almacén de Data Lake de toohello de hello servicio acceso principal y todas las carpetas de hello en la ruta de acceso raíz de Hola que especificó anteriormente. Usar hello siguientes cmdlets:

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a>Crear un clúster de HDInsight Linux con el almacén de Data Lake como almacenamiento predeterminado de Hola

En esta sección, creará un clúster de HDInsight Hadoop Linux con el almacén de Data Lake como almacenamiento predeterminado de Hola. En esta versión, Hola clúster de HDInsight y almacén de Data Lake debe ser Hola misma ubicación.

1. Recuperar el Id. de inquilino de suscripción de Hola y almacenarlo toouse más tarde.

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. Crear el clúster de HDInsight de hello mediante Hola siguientes cmdlets:

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    Después de hello cmdlet se ha completado correctamente, debería ver una salida que muestra detalles del clúster Hola.

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a>Ejecutar trabajos de prueba en toouse de clúster de HDInsight de hello almacén de Data Lake
Después de haber configurado un clúster de HDInsight, puede ejecutar trabajos de prueba en el mismo tooensure que puede tener acceso a almacén de Data Lake. toodo por lo tanto, ejecute un toocreate de trabajo de Hive de ejemplo una tabla que usa datos de ejemplo de Hola que ya está disponibles en el almacén de Data Lake en  *<cluster root>/example/data/sample.log*.

En esta sección, se realiza una conexión de Secure Shell (SSH) en hello clúster de HDInsight Linux que creó y, a continuación, ejecutar una consulta de Hive de ejemplo.

* Si usas un toomake de cliente de Windows una conexión SSH en el clúster hello, consulte [utilizar SSH con Linux-based Hadoop en HDInsight de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Si usas un toomake de cliente de Linux una conexión SSH en el clúster hello, consulte [utilizar SSH con Linux-based Hadoop en HDInsight de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

1. Después de realizar la conexión de hello, iniciar la interfaz de línea de comandos de hello Hive (CLI) mediante Hola siguiente comando:

        hive
2. Use Hola CLI tooenter Hola siguiendo las instrucciones toocreate una nueva tabla denominada **vehículos** mediante el uso de datos de ejemplo de Hola en almacén de Data Lake:

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Debería ver el resultado de la consulta de hello en la consola de SSH de Hola.

    >[!NOTE]
    >Hola datos de ejemplo de ruta de acceso toohello Hola anterior comando CREATE TABLE están `adl:///example/data/`, donde `adl:///` es Hola clúster raíz. Después de ejemplo de Hola de raíz de clúster de Hola que se especifica en este tutorial, el comando de hello es `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`. Puede usar alternativa más corto de Hola o proporcionar Hola ruta de acceso completa toohello clúster raíz.
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a>Acceso a Data Lake Store mediante comandos de HDFS
Después de haber configurado el almacén de hello HDInsight clúster toouse Data Lake, puede usar almacén de sistema de archivos distribuido de Hadoop (HDFS) shell comandos tooaccess Hola.

En esta sección, se realiza una conexión SSH en hello clúster de HDInsight Linux que ha creado y, a continuación, ejecutar comandos HDFS Hola.

* Si usas un toomake de cliente de Windows una conexión SSH en el clúster hello, consulte [utilizar SSH con Linux-based Hadoop en HDInsight de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).
* Si usas un toomake de cliente de Linux una conexión SSH en el clúster hello, consulte [utilizar SSH con Linux-based Hadoop en HDInsight de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).

Una vez que haya realizado la conexión de hello, enumerar archivos de hello en el almacén de Data Lake mediante Hola siguiente comando de sistema de archivo HDFS.

    hdfs dfs -ls adl:///

También puede usar hello `hdfs dfs -put` comando tooupload un almacén de archivos tooData Lake y, a continuación, usar `hdfs dfs -ls` tooverify si los archivos de saludo se cargaron correctamente.

## <a name="see-also"></a>Otras referencias
* [Portal de Azure: crear un toouse de clúster de HDInsight almacén de Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
