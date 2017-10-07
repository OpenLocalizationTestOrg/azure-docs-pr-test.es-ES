---
title: "autenticación no interactiva aaaCreate HDInsight .NET autorizarán - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo las aplicaciones de .NET HDInsight de autenticación no interactiva toocreate."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 8e32430f-6404-498a-9fcd-f20338d964af
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 5367c160b0146e6b855486b95f363e8fe7f1c98f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a>Crear aplicaciones .NET para HDInsight de autenticación no interactiva
Puede ejecutar la aplicación de HDInsight de Azure .NET bajo la identidad de la aplicación (no interactivo) o con identidad Hola de hello usuario que inició sesión de la aplicación hello (interactiva). Para obtener un ejemplo de aplicación interactiva de hello, consulte [conectar tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight). Este artículo muestra cómo toocreate autenticación no interactiva .NET aplicación tooconnect tooAzure y administrar HDInsight.

Desde su aplicación de .NET no interactiva, necesita:

* El identificador de inquilino de su suscripción a Azure (también conocido como identificador de directorio). Consulte [Obtención del identificador de inquilino](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).
* identificador de cliente de aplicación de Azure Active Directory Hola. Consulte [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) (Creación de una aplicación de Azure Active Directory) y el apartado sobre cómo [conseguir un id. de aplicación](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).
* clave secreta de Hello Azure Active Directory aplicación. Consulte [Obtención de la clave de autenticación](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)

## <a name="prerequisites"></a>Requisitos previos
* Clúster de HDInsight. Consulte el [tutorial de introducción](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).



## <a name="assign-azure-ad-application-toorole"></a>Asignar toorole de aplicación de Azure AD
Debe asignar Hola aplicación tooa [rol](../active-directory/role-based-access-built-in-roles.md) toogrant, permisos para realizar acciones. Puede establecer el ámbito de hello en nivel de Hola de suscripción de hello, el grupo de recursos o el recurso. permisos de Hello son heredados toolower niveles de ámbito (por ejemplo, agregar que un rol de lector de toohello de aplicación para un grupo de recursos significa que puede leer el grupo de recursos de Hola y los recursos que contenga). En este tutorial, establecerá el ámbito de hello en el nivel de grupo de recursos de Hola. Para obtener más información, vea [usar recursos de rol asignaciones toomanage acceso tooyour suscripción de Azure](../active-directory/role-based-access-control-configure.md)

**Hola tooadd aplicación del propietario rol toohello Azure AD**

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **grupo de recursos** en el panel izquierdo de Hola.
3. Haga clic en el grupo de recursos de Hola que contiene el clúster de HDInsight de Hola donde se ejecutará la consulta de Hive más adelante en este tutorial. Si hay demasiados grupos de recursos, puede usar el filtro de Hola.
4. Haga clic en **(de índices IAM) de control de acceso** de menú de grupo de recursos de Hola.
5. Haga clic en **agregar** de hello **usuarios** hoja.
6. Siga Hola de hello instrucción tooadd **propietario** rol toohello aplicación de Azure AD que creó en el último procedimiento de Hola. Cuando haya completado correctamente, verá la aplicación hello aparecen en la hoja de hello usuarios con el rol de propietario de Hola.

## <a name="develop-hdinsight-client-application"></a>Desarrollar la aplicación de cliente de HDInsight

1. Cree una aplicación de consola en C#
2. Agregue Hola siguientes paquetes de Nuget:

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. Usar hello siguiendo el ejemplo de código:

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Common.Authentication;
        using Microsoft.Azure.Common.Authentication.Factories;
        using Microsoft.Azure.Common.Authentication.Models;
        using Microsoft.Azure.Management.Resources;
        using Microsoft.Azure.Management.HDInsight;
        
        namespace CreateHDICluster
        {
            internal class Program
            {
                private static HDInsightManagementClient _hdiManagementClient;
        
                private static Guid SubscriptionId = new Guid("<Enter Your Azure Subscription ID>");
                private static string tenantID = "<Enter Your Tenant ID (A.K.A. Directory ID)>";
                private static string applicationID = "<Enter Your Application ID>";
                private static string secretKey = "<Enter hello Application Secret Key>";
        
                private static void Main(string[] args)
                {
                    var key = new SecureString();
                    foreach (char c in secretKey) { key.AppendChar(c); }

                    var tokenCreds = GetTokenCloudCredentials(tenantID, applicationID, key);
                    var subCloudCredentials = GetSubscriptionCloudCredentials(tokenCreds, SubscriptionId);
        
                    var resourceManagementClient = new ResourceManagementClient(subCloudCredentials);
                    resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        
                    _hdiManagementClient = new HDInsightManagementClient(subCloudCredentials);
        
                    var results = _hdiManagementClient.Clusters.List();
                    foreach (var name in results.Clusters)
                    {
                        Console.WriteLine("Cluster Name: " + name.Name);
                        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
                        Console.WriteLine("\t Cluster location: " + name.Location);
                        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
                    }
                    Console.WriteLine("Press Enter toocontinue");
                    Console.ReadLine();
                }

                /// Get hello access token for a service principal and provided key                
                public static TokenCloudCredentials GetTokenCloudCredentials(string tenantId, string clientId, SecureString secretKey)
                {
                    var authFactory = new AuthenticationFactory();
                    var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
                    var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
                    var accessToken =
                        authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
        
                    return new TokenCloudCredentials(accessToken);
                }
        
                public static SubscriptionCloudCredentials GetSubscriptionCloudCredentials(SubscriptionCloudCredentials creds, Guid subId)
                {
                    return new TokenCloudCredentials(subId.ToString(), ((TokenCloudCredentials)creds).Token);
                }
            }
        }

## <a name="next-steps"></a>Pasos siguientes
* [Creación de una aplicación de Azure Active Directory y una entidad de servicio mediante el portal](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Autenticar una entidad de servicio con Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md)
