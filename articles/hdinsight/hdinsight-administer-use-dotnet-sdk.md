---
title: "clústeres de aaaManage Hadoop en HDInsight con .NET SDK - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooperform administrativa tareas para hello clústeres de Hadoop en HDInsight con HDInsight .NET SDK."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: fd134765-c2a0-488a-bca6-184d814d78e9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d8bbf966b7eba3e943dfb2f764d15d8e52b9be71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a>Administración de clústeres de Hadoop en HDInsight con el SDK de .NET
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Obtenga información acerca de cómo usar los clústeres de toomanage HDInsight [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).

**Requisitos previos**

Antes de comenzar este artículo, debe tener el siguiente hello:

* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="connect-tooazure-hdinsight"></a>Conectar tooAzure HDInsight

Necesita Hola siguientes paquetes de Nuget:

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

Hello ejemplo de código siguiente muestra cómo tooconnect tooAzure antes de poder administrar HDInsight clústeres en su suscripción de Azure.

    using System;
    using Microsoft.Azure;
    using Microsoft.Azure.Management.HDInsight;
    using Microsoft.Azure.Management.HDInsight.Models;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;

    namespace HDInsightManagement
    {
        class Program
        {
            private static HDInsightManagementClient _hdiManagementClient;
            // Replace with your AAD tenant ID if necessary
            private const string TenantId = UserTokenProvider.CommonTenantId; 
            private const string SubscriptionId = "<Your Azure Subscription ID>";
            // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
            private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";

            static void Main(string[] args)
            {
                // Authenticate and get a token
                var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
                // Flag subscription for HDInsight, if it isn't already.
                EnableHDInsight(authToken);
                // Get an HDInsight management client
                _hdiManagementClient = new HDInsightManagementClient(authToken);

                // insert code here

                System.Console.WriteLine("Press ENTER toocontinue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate tooan Azure subscription and retrieve an authentication token
            /// </summary>
            static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
            {
                var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
                var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/", 
                    ClientId, 
                    new Uri("urn:ietf:wg:oauth:2.0:oob"), 
                    PromptBehavior.Always, 
                    UserIdentifier.AnyUser);
                return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
            }
            /// <summary>
            /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
            /// </summary>
            /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
            /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
            /// <param name="authToken">An authentication token for your Azure subscription</param>
            static void EnableHDInsight(TokenCloudCredentials authToken)
            {
                // Create a client for hello Resource manager and set hello subscription ID
                var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
                resourceManagementClient.SubscriptionId = SubscriptionId;
                // Register hello HDInsight provider
                var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
            }
        }
    }

Al ejecutar este programa, verá un mensaje.  Si no desea que el símbolo del sistema de toosee hello, consulte [crear aplicaciones de .NET HDInsight de autenticación no interactiva](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

## <a name="create-clusters"></a>Creación de clústeres
Vea [basados en Linux crear clústeres de HDInsight utilizando Hola SDK para .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)

## <a name="list-clusters"></a>Enumeración de clústeres
Hello fragmento de código siguiente enumera los clústeres y algunas propiedades:

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a>Eliminación de clústeres
Usar hello siguiente fragmento de código toodelete un clúster de forma sincrónica o asincrónica: 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a>Escalado de clústeres
característica de ajuste de escala de clúster de Hola permite toochange número de Hola de nodos de trabajador usado por un clúster que se ejecuta en HDInsight de Azure sin necesidad de toore-crear clúster Hola.

> [!NOTE]
> Solo son compatibles los clústeres con la versión 3.1.3 de HDInsight, o superior. Si no está seguro de la versión de Hola del clúster, puede comprobar la página de propiedades de Hola.  Consulte [Enumeración y visualización de clústeres](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
> 
> 

impacto de Hola de cambiar el número de Hola de nodos de datos para cada tipo de clúster compatible con HDInsight:

* Hadoop
  
    Perfectamente puede aumentar el número de Hola de nodos de trabajador en un clúster de Hadoop que se ejecuta sin afectar a los trabajos pendientes o en ejecución. También se pueden enviar trabajos nuevos mientras Hola operación está en curso. Errores en una operación de ajuste de escala se controlan correctamente para que hello clúster siempre se deja en un estado funcional.
  
    Cuando un clúster de Hadoop es reducido reduciendo el número de Hola de nodos de datos, algunos de los servicios de hello en clúster de Hola se reinician. Esto hace que ejecutan todos y pendiente de trabajos toofail al término de Hola Hola la operación de escalado. Sin embargo, puede volver a enviar trabajos de hello una vez completada la operación de Hola.
* HBase
  
    Sin problemas, puede agregar o quitar el clúster de HBase tooyour nodos mientras se está ejecutando. Los servidores regionales se equilibran automáticamente dentro de unos pocos minutos después de completar la operación de escalado de Hola. No obstante, puede equilibrar manualmente servidores regionales Hola iniciando sesión en el nodo principal de hello del clúster y ejecución Hola siguientes comandos de una ventana del símbolo del sistema:
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm
  
    Sin problemas, puede agregar o quitar el clúster de Storm de tooyour de nodos de datos mientras se está ejecutando. Sin embargo, tras finalizar correctamente la operación de escalado de hello, debe topología de hello toorebalance.
  
    Esto se puede realizar de dos formas:
  
  * La interfaz de usuario web de Storm
  * La herramienta de la interfaz de línea de comandos (CLI)
    
    Consulte toohello [documentación de Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) para obtener más detalles.
    
    interfaz de usuario de web de Storm Hola está disponible en el clúster de HDInsight de hello:
    
    ![Reequilibrio de escalado de HDInsight Storm](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    Este es un ejemplo cómo toouse Hola CLI comando topología de Storm Hola toorebalance:
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

Hola código fragmento siguiente muestra cómo tooresize un clúster de forma sincrónica o asincrónica:

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a>Concesión o revocación del acceso
Clústeres de HDInsight tienen Hola después de servicios web HTTP (todos estos servicios tienen extremos RESTful):

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

De manera predeterminada, estos servicios se conceden para el acceso. Puede revocar y conceder acceso de Hola. toorevoke:

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

toogrant:

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> Por conceder o revocar el acceso de hello, se restablecerá la contraseña y el nombre de usuario del clúster de Hola.
> 
> 

Esto puede hacerse a través de hello Portal. Vea [HDInsight administrar mediante el uso de Hola portal de Azure][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>Actualización de las credenciales de usuario HTTP
Es Hola mismo procedimiento como [HTTP conceder o revocar acceso](#grant/revoke-access). Si se concedió clúster Hola Hola acceso HTTP, debe revocar primero.  Y, a continuación, conceder acceso de hello con nuevas credenciales de usuario HTTP.

## <a name="find-hello-default-storage-account"></a>Busque la cuenta de almacenamiento predeterminada de Hola
Hola siguiente fragmento de código muestra cómo tooget nombre de cuenta de almacenamiento predeterminado de Hola y Hola clave de cuenta de almacenamiento predeterminada para un clúster.

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a>Envío de trabajos
**trabajos de MapReduce toosubmit**

Consulte [Ejecución de ejemplos de Hadoop en HDInsight](hdinsight-hadoop-run-samples-linux.md).

**trabajos de Hive toosubmit** 

Consulte [Ejecución de consultas de Hive mediante el SDK de .NET de HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md).

**trabajos de Pig toosubmit**

Consulte [Ejecución de trabajos de Pig con el SDK de .NET para Hadoop en HDInsight](hdinsight-hadoop-use-pig-dotnet-sdk.md).

**trabajos de Sqoop toosubmit**

Consulte [Uso de Sqoop con HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).

**trabajos de Oozie toosubmit**

Vea [Oozie de uso con Hadoop toodefine y ejecutar un flujo de trabajo en HDInsight](hdinsight-use-oozie-linux-mac.md).

## <a name="upload-data-tooazure-blob-storage"></a>Cargar el almacenamiento de blobs de datos tooAzure
Vea [cargar datos tooHDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Otras referencias
* [Documentación de referencia del SDK de HDInsight](https://msdn.microsoft.com/library/mt271028.aspx)
* [Administrar HDInsight mediante Hola portal de Azure][hdinsight-admin-portal]
* [Administración de HDInsight con la interfaz de la línea de comandos][hdinsight-admin-cli]
* [Creación de clústeres de HDInsight][hdinsight-provision]
* [Cargar datos tooHDInsight][hdinsight-upload-data]
* [Introducción a Azure HDInsight][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-portal-linux.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md


