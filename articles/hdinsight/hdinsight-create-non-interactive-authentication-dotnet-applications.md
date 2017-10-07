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
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="8ce72-103">Crear aplicaciones .NET para HDInsight de autenticación no interactiva</span><span class="sxs-lookup"><span data-stu-id="8ce72-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="8ce72-104">Puede ejecutar la aplicación de HDInsight de Azure .NET bajo la identidad de la aplicación (no interactivo) o con identidad Hola de hello usuario que inició sesión de la aplicación hello (interactiva).</span><span class="sxs-lookup"><span data-stu-id="8ce72-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under hello identity of hello signed-in user of hello application (interactive).</span></span> <span data-ttu-id="8ce72-105">Para obtener un ejemplo de aplicación interactiva de hello, consulte [conectar tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="8ce72-105">For a sample of hello interactive application, see [Connect tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="8ce72-106">Este artículo muestra cómo toocreate autenticación no interactiva .NET aplicación tooconnect tooAzure y administrar HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ce72-106">This article shows you how toocreate non-interactive authentication .NET application tooconnect tooAzure and manage HDInsight.</span></span>

<span data-ttu-id="8ce72-107">Desde su aplicación de .NET no interactiva, necesita:</span><span class="sxs-lookup"><span data-stu-id="8ce72-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="8ce72-108">El identificador de inquilino de su suscripción a Azure (también conocido como identificador de directorio).</span><span class="sxs-lookup"><span data-stu-id="8ce72-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="8ce72-109">Consulte [Obtención del identificador de inquilino](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="8ce72-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="8ce72-110">identificador de cliente de aplicación de Azure Active Directory Hola.</span><span class="sxs-lookup"><span data-stu-id="8ce72-110">hello Azure Active Directory application client ID.</span></span> <span data-ttu-id="8ce72-111">Consulte [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) (Creación de una aplicación de Azure Active Directory) y el apartado sobre cómo [conseguir un id. de aplicación](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).</span><span class="sxs-lookup"><span data-stu-id="8ce72-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="8ce72-112">clave secreta de Hello Azure Active Directory aplicación.</span><span class="sxs-lookup"><span data-stu-id="8ce72-112">hello Azure Active Directory application secret key.</span></span> <span data-ttu-id="8ce72-113">Consulte [Obtención de la clave de autenticación](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="8ce72-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ce72-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8ce72-114">Prerequisites</span></span>
* <span data-ttu-id="8ce72-115">Clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8ce72-115">HDInsight cluster.</span></span> <span data-ttu-id="8ce72-116">Consulte el [tutorial de introducción](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="8ce72-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-toorole"></a><span data-ttu-id="8ce72-117">Asignar toorole de aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ce72-117">Assign Azure AD application toorole</span></span>
<span data-ttu-id="8ce72-118">Debe asignar Hola aplicación tooa [rol](../active-directory/role-based-access-built-in-roles.md) toogrant, permisos para realizar acciones.</span><span class="sxs-lookup"><span data-stu-id="8ce72-118">You must assign hello application tooa [role](../active-directory/role-based-access-built-in-roles.md) toogrant it permissions for performing actions.</span></span> <span data-ttu-id="8ce72-119">Puede establecer el ámbito de hello en nivel de Hola de suscripción de hello, el grupo de recursos o el recurso.</span><span class="sxs-lookup"><span data-stu-id="8ce72-119">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="8ce72-120">permisos de Hello son heredados toolower niveles de ámbito (por ejemplo, agregar que un rol de lector de toohello de aplicación para un grupo de recursos significa que puede leer el grupo de recursos de Hola y los recursos que contenga).</span><span class="sxs-lookup"><span data-stu-id="8ce72-120">hello permissions are inherited toolower levels of scope (for example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains).</span></span> <span data-ttu-id="8ce72-121">En este tutorial, establecerá el ámbito de hello en el nivel de grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ce72-121">In this tutorial, you will set hello scope at hello resource group level.</span></span> <span data-ttu-id="8ce72-122">Para obtener más información, vea [usar recursos de rol asignaciones toomanage acceso tooyour suscripción de Azure](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="8ce72-122">For more information, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="8ce72-123">**Hola tooadd aplicación del propietario rol toohello Azure AD**</span><span class="sxs-lookup"><span data-stu-id="8ce72-123">**tooadd hello Owner role toohello Azure AD application**</span></span>

1. <span data-ttu-id="8ce72-124">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8ce72-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8ce72-125">Haga clic en **grupo de recursos** en el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ce72-125">Click **Resource Group** from hello left pane.</span></span>
3. <span data-ttu-id="8ce72-126">Haga clic en el grupo de recursos de Hola que contiene el clúster de HDInsight de Hola donde se ejecutará la consulta de Hive más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8ce72-126">Click hello resource group that contains hello HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="8ce72-127">Si hay demasiados grupos de recursos, puede usar el filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ce72-127">If there are too many resource groups, you can use hello filter.</span></span>
4. <span data-ttu-id="8ce72-128">Haga clic en **(de índices IAM) de control de acceso** de menú de grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ce72-128">Click **Access control (IAM)** from hello resource group menu.</span></span>
5. <span data-ttu-id="8ce72-129">Haga clic en **agregar** de hello **usuarios** hoja.</span><span class="sxs-lookup"><span data-stu-id="8ce72-129">Click **Add** from hello **Users** blade.</span></span>
6. <span data-ttu-id="8ce72-130">Siga Hola de hello instrucción tooadd **propietario** rol toohello aplicación de Azure AD que creó en el último procedimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ce72-130">Follow hello instruction tooadd hello **Owner** role toohello Azure AD application you created in hello last procedure.</span></span> <span data-ttu-id="8ce72-131">Cuando haya completado correctamente, verá la aplicación hello aparecen en la hoja de hello usuarios con el rol de propietario de Hola.</span><span class="sxs-lookup"><span data-stu-id="8ce72-131">When you complete it successfully, you shall see hello application listed in hello Users blade with hello Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="8ce72-132">Desarrollar la aplicación de cliente de HDInsight</span><span class="sxs-lookup"><span data-stu-id="8ce72-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="8ce72-133">Cree una aplicación de consola en C#</span><span class="sxs-lookup"><span data-stu-id="8ce72-133">Create a C# console application.</span></span>
2. <span data-ttu-id="8ce72-134">Agregue Hola siguientes paquetes de Nuget:</span><span class="sxs-lookup"><span data-stu-id="8ce72-134">Add hello following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="8ce72-135">Usar hello siguiendo el ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="8ce72-135">Use hello following code sample:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8ce72-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8ce72-136">Next steps</span></span>
* [<span data-ttu-id="8ce72-137">Creación de una aplicación de Azure Active Directory y una entidad de servicio mediante el portal</span><span class="sxs-lookup"><span data-stu-id="8ce72-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="8ce72-138">Autenticar una entidad de servicio con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8ce72-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="8ce72-139">Control de acceso basado en roles de Azure</span><span class="sxs-lookup"><span data-stu-id="8ce72-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
