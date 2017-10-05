---
title: "Creación de aplicaciones .NET para HDInsight de autenticación no interactiva - Azure | Microsoft Docs"
description: "Obtenga información sobre cómo crear aplicaciones .NET para HDInsight de autenticación no interactiva."
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
ms.openlocfilehash: 7821a9e60e60ff01cff06db2a6f216a260c1c41a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="fb7e1-103">Crear aplicaciones .NET para HDInsight de autenticación no interactiva</span><span class="sxs-lookup"><span data-stu-id="fb7e1-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="fb7e1-104">Puede ejecutar su aplicación .NET para Azure HDInsight en la propia identidad de la aplicación (no interactiva) o en la identidad del usuario con sesión iniciada de la aplicación (interactiva).</span><span class="sxs-lookup"><span data-stu-id="fb7e1-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under the identity of the signed-in user of the application (interactive).</span></span> <span data-ttu-id="fb7e1-105">Para obtener un ejemplo de la aplicación interactiva, consulte [Conexión a Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="fb7e1-105">For a sample of the interactive application, see [Connect to Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="fb7e1-106">En este artículo se muestra cómo crear aplicaciones .NET de autenticación no interactivas para conectarse a Azure y administrar HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fb7e1-106">This article shows you how to create non-interactive authentication .NET application to connect to Azure and manage HDInsight.</span></span>

<span data-ttu-id="fb7e1-107">Desde su aplicación de .NET no interactiva, necesita:</span><span class="sxs-lookup"><span data-stu-id="fb7e1-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="fb7e1-108">El identificador de inquilino de su suscripción a Azure (también conocido como identificador de directorio).</span><span class="sxs-lookup"><span data-stu-id="fb7e1-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="fb7e1-109">Consulte [Obtención del identificador de inquilino](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="fb7e1-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="fb7e1-110">El id. de cliente de la aplicación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fb7e1-110">The Azure Active Directory application client ID.</span></span> <span data-ttu-id="fb7e1-111">Consulte [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) (Creación de una aplicación de Azure Active Directory) y el apartado sobre cómo [conseguir un id. de aplicación](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).</span><span class="sxs-lookup"><span data-stu-id="fb7e1-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="fb7e1-112">La clave secreta de la aplicación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fb7e1-112">The Azure Active Directory application secret key.</span></span> <span data-ttu-id="fb7e1-113">Consulte [Obtención de la clave de autenticación](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="fb7e1-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb7e1-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fb7e1-114">Prerequisites</span></span>
* <span data-ttu-id="fb7e1-115">Clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fb7e1-115">HDInsight cluster.</span></span> <span data-ttu-id="fb7e1-116">Consulte el [tutorial de introducción](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="fb7e1-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-to-role"></a><span data-ttu-id="fb7e1-117">Asignación de una aplicación de Azure AD a un rol</span><span class="sxs-lookup"><span data-stu-id="fb7e1-117">Assign Azure AD application to role</span></span>
<span data-ttu-id="fb7e1-118">Debe asignar la aplicación a un [rol](../active-directory/role-based-access-built-in-roles.md) para concederle permisos para realizar acciones.</span><span class="sxs-lookup"><span data-stu-id="fb7e1-118">You must assign the application to a [role](../active-directory/role-based-access-built-in-roles.md) to grant it permissions for performing actions.</span></span> <span data-ttu-id="fb7e1-119">Puede establecer el ámbito en el nivel de suscripción, grupo de recursos o recurso.</span><span class="sxs-lookup"><span data-stu-id="fb7e1-119">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="fb7e1-120">Los permisos se heredan en los niveles inferiores de ámbito (por ejemplo, el hecho de agregar una aplicación al rol Lector para un grupo de recursos significa que esta puede leer el grupo de recursos y los recursos que contenga).</span><span class="sxs-lookup"><span data-stu-id="fb7e1-120">The permissions are inherited to lower levels of scope (for example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains).</span></span> <span data-ttu-id="fb7e1-121">En este tutorial, establecerá el ámbito en el nivel del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="fb7e1-121">In this tutorial, you will set the scope at the resource group level.</span></span> <span data-ttu-id="fb7e1-122">Para obtener más información, consulte [Uso de asignaciones de roles para administrar el acceso a los recursos de la suscripción de Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="fb7e1-122">For more information, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="fb7e1-123">**Para agregar el rol de propietario a la aplicación de Azure AD**</span><span class="sxs-lookup"><span data-stu-id="fb7e1-123">**To add the Owner role to the Azure AD application**</span></span>

1. <span data-ttu-id="fb7e1-124">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fb7e1-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fb7e1-125">Haga clic en **Grupo de recursos** en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="fb7e1-125">Click **Resource Group** from the left pane.</span></span>
3. <span data-ttu-id="fb7e1-126">Haga clic en el grupo de recursos que contiene el clúster de HDInsight donde ejecutará la consulta de Hive más adelante en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="fb7e1-126">Click the resource group that contains the HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="fb7e1-127">Si hay demasiados grupos de recursos, puede usar el filtro.</span><span class="sxs-lookup"><span data-stu-id="fb7e1-127">If there are too many resource groups, you can use the filter.</span></span>
4. <span data-ttu-id="fb7e1-128">En el menú de grupo de recursos, haga clic en **Control de acceso (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="fb7e1-128">Click **Access control (IAM)** from the resource group menu.</span></span>
5. <span data-ttu-id="fb7e1-129">Haga clic en **Agregar** en la hoja **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="fb7e1-129">Click **Add** from the **Users** blade.</span></span>
6. <span data-ttu-id="fb7e1-130">Siga las instrucciones para agregar el rol de **propietario** a la aplicación de Azure AD que creó en el último procedimiento.</span><span class="sxs-lookup"><span data-stu-id="fb7e1-130">Follow the instruction to add the **Owner** role to the Azure AD application you created in the last procedure.</span></span> <span data-ttu-id="fb7e1-131">Cuando lo complete correctamente, verá la aplicación enumerada en la hoja Usuarios con el rol de propietario.</span><span class="sxs-lookup"><span data-stu-id="fb7e1-131">When you complete it successfully, you shall see the application listed in the Users blade with the Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="fb7e1-132">Desarrollar la aplicación de cliente de HDInsight</span><span class="sxs-lookup"><span data-stu-id="fb7e1-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="fb7e1-133">Cree una aplicación de consola en C#</span><span class="sxs-lookup"><span data-stu-id="fb7e1-133">Create a C# console application.</span></span>
2. <span data-ttu-id="fb7e1-134">Agregue los siguientes paquetes NuGet:</span><span class="sxs-lookup"><span data-stu-id="fb7e1-134">Add the following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="fb7e1-135">Use el código de ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="fb7e1-135">Use the following code sample:</span></span>

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
                private static string secretKey = "<Enter the Application Secret Key>";
        
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
                    Console.WriteLine("Press Enter to continue");
                    Console.ReadLine();
                }

                /// Get the access token for a service principal and provided key                
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

## <a name="next-steps"></a><span data-ttu-id="fb7e1-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fb7e1-136">Next steps</span></span>
* [<span data-ttu-id="fb7e1-137">Creación de una aplicación de Azure Active Directory y una entidad de servicio mediante el portal</span><span class="sxs-lookup"><span data-stu-id="fb7e1-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="fb7e1-138">Autenticar una entidad de servicio con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fb7e1-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="fb7e1-139">Control de acceso basado en roles de Azure</span><span class="sxs-lookup"><span data-stu-id="fb7e1-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
