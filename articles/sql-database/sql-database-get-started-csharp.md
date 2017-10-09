---
title: "C#: introducción a Azure SQL Database | Microsoft Docs"
description: Probar la base de datos SQL para desarrollar aplicaciones SQL y C# y crear una base de datos de SQL Azure con C# mediante Hola biblioteca de base de datos de SQL para. NET.
keywords: probar sql, sql c#
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: cfff2299-a474-4054-8d99-759af1ae5188
ms.service: sql-database
ms.custom: develop apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: csharp
ms.workload: data-management
ms.date: 10/04/2016
ms.author: sstein
ms.openlocfilehash: e880ebabd53546bea37a13186b0f1a13db35b684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-toocreate-a-sql-database-with-hello-sql-database-library-for-net"></a>Usar C# toocreate una base de datos SQL con hello biblioteca de base de datos de SQL para .NET

Obtenga información acerca de cómo toocreate toouse C# SQL Azure base de datos con hello [biblioteca de administración de SQL de Microsoft Azure para .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql). Este artículo describe cómo toocreate una sola base de datos con SQL y C#. toocreate grupos elásticos, consulte [crear un grupo elástico](sql-database-elastic-pool-manage-csharp.md).

Hola biblioteca de administración de base de datos de SQL Azure para .NET proporciona un [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-en función de API que ajusta hello [basado en el Administrador de recursos de la API de REST de la base de datos de SQL](https://docs.microsoft.com/rest/api/sql/).

> [!NOTE]
> Muchas características nuevas de la base de datos SQL solo se admiten cuando se usa hello [modelo de implementación de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), por lo que se debe utilizar siempre hello más reciente **biblioteca de administración de base de datos de SQL Azure para .NET ([documentos](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**. Hola anterior [bibliotecas basadas en el modelo de implementación clásica](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) se admiten por razones de compatibilidad, por lo que recomendamos usar bibliotecas más recientes de administrador de recursos en función de Hola.
> 
> 

pasos de hello toocomplete en este artículo, necesita siguiente de hello:

* Una suscripción de Azure. Si tiene una suscripción de Azure simplemente haga clic en **cuenta gratuita** princip Hola de esta página y, a continuación, vuelven a estar toofinish en este artículo.
* Visual Studio. Para obtener una copia gratuita de Visual Studio, vea hello [descargas de Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs) página.

> [!NOTE]
> Este artículo permite crear una nueva base de datos SQL en blanco. Modificar hello *CreateOrUpdateDatabase(...)*  método hello siguiendo las bases de datos de ejemplo toocopy, escalar las bases de datos, cree una base de datos en un grupo, etcetera.  
> 

## <a name="create-a-console-app-and-install-hello-required-libraries"></a>Crear una aplicación de consola e instalar las bibliotecas de hello necesario
1. Inicie Visual Studio.
2. Haga clic en **Archivo** > **Nuevo** > **Proyecto**.
3. Cree una **aplicación de consola** C# y asígnele el nombre *SqlDbConsoleApp*

toocreate una base de datos SQL con C#, Hola de carga requiere las bibliotecas de administración (con hello [consola del Administrador de paquetes](http://docs.nuget.org/Consume/Package-Manager-Console)):

1. Haga clic en **Herramientas** > **Administrador de paquetes NuGet** > **Consola del administrador de paquetes**.
2. Tipo de `Install-Package Microsoft.Azure.Management.Sql -Pre` tooinstall hello más reciente [biblioteca de administración de Microsoft Azure SQL](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).
3. Tipo de `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` tooinstall hello [biblioteca del Administrador de recursos de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).
4. Tipo de `Install-Package Microsoft.Azure.Common.Authentication -Pre` tooinstall hello [biblioteca de autenticación común de Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication). 

> [!NOTE]
> Hello ejemplos de este artículo usan una forma sincrónica de cada solicitud de API y el bloque hasta la finalización de la llamada REST de hello en hello servicio subyacente. Hay métodos asincrónicos disponibles.
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a>Creación de un servidor de SQL Database, una regla de firewall y una base de datos SQL: ejemplo de C#
Hola siguiendo el ejemplo crea un grupo de recursos, servidor, regla de firewall y una base de datos SQL. Ver, [crear un tooaccess de entidad de seguridad de servicio recursos](#create-a-service-principal-to-access-resources) tooget hello `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` variables.

Reemplace el contenido de Hola de **Program.cs** con siguiente de Hola y Hola de actualización `{variables}` con sus valores de la aplicación (no incluya hello `{}`).

    using Microsoft.Azure;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.Azure.Management.Sql;
    using Microsoft.Azure.Management.Sql.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System;

    namespace SqlDbConsoleApp
    {
    class Program
       {
        // For details about these four (4) values, see
        // https://azure.microsoft.com/documentation/articles/resource-group-authenticate-service-principal/
        static string _subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _tenantId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationSecret = "{your-password}";

        // Create management clients for hello Azure resources your app needs toowork with.
        // This app works with Resource Groups, and Azure SQL Database.
        static ResourceManagementClient _resourceMgmtClient;
        static SqlManagementClient _sqlMgmtClient;

        // Authentication token
        static AuthenticationResult _token;

        // Azure resource variables
        static string _resourceGroupName = "{resource-group-name}";
        static string _resourceGrouplocation = "{Azure-region}";

        static string _serverlocation = _resourceGrouplocation;
        static string _serverName = "{server-name}";
        static string _serverAdmin = "{server-admin-login}";
        static string _serverAdminPassword = "{server-admin-password}";

        static string _firewallRuleName = "{firewall-rule-name}";
        static string _startIpAddress = "{0.0.0.0}";
        static string _endIpAddress = "{255.255.255.255}";

        static string _databaseName = "{dbfromcsarticle}";
        static string _databaseEdition = DatabaseEditions.Basic;
        static string _databasePerfLevel = ""; // "S0", "S1", and so on here for other tiers


        static void Main(string[] args)
        {
            // Authenticate:
            _token = GetToken(_tenantId, _applicationId, _applicationSecret);
            Console.WriteLine("Token acquired. Expires on:" + _token.ExpiresOn);

            // Instantiate management clients:
            _resourceMgmtClient = new ResourceManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken));
            _sqlMgmtClient = new SqlManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken)) { SubscriptionId = _subscriptionId };

            Console.WriteLine("Resource group...");
            ResourceGroup rg = CreateOrUpdateResourceGroup(_resourceMgmtClient, _subscriptionId, _resourceGroupName, _resourceGrouplocation);
            Console.WriteLine("Resource group: " + rg.Id);


            Console.WriteLine("Server...");
            Server sgr = CreateOrUpdateServer(_sqlMgmtClient, _resourceGroupName, _serverlocation, _serverName, _serverAdmin, _serverAdminPassword);
            Console.WriteLine("Server: " + sgr.Id);

            Console.WriteLine("Server firewall...");
            FirewallRule fwr = CreateOrUpdateFirewallRule(_sqlMgmtClient, _resourceGroupName, _serverName, _firewallRuleName, _startIpAddress, _endIpAddress);
            Console.WriteLine("Server firewall: " + fwr.Id);

            Console.WriteLine("Database...");
            Database dbr = CreateOrUpdateDatabase(_sqlMgmtClient, _resourceGroupName, _serverName, _databaseName, _databaseEdition, _databasePerfLevel);
            Console.WriteLine("Database: " + dbr.Id);


            Console.WriteLine("Press any key toocontinue...");
            Console.ReadKey();
        }

        static ResourceGroup CreateOrUpdateResourceGroup(ResourceManagementClient resourceMgmtClient, string subscriptionId, string resourceGroupName, string resourceGroupLocation)
        {
            ResourceGroup resourceGroupParameters = new ResourceGroup()
            {
                Location = resourceGroupLocation,
            };
            resourceMgmtClient.SubscriptionId = subscriptionId;
            ResourceGroup resourceGroupResult = resourceMgmtClient.ResourceGroups.CreateOrUpdate(resourceGroupName, resourceGroupParameters);
            return resourceGroupResult;
        }

        static Server CreateOrUpdateServer(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverLocation, string serverName, string serverAdmin, string serverAdminPassword)
        {
            Server serverParameters = new Server()
            {
                Location = serverLocation,
                AdministratorLogin = serverAdmin,
                AdministratorLoginPassword = serverAdminPassword,
                Version = "12.0"
            };
            Server serverResult = sqlMgmtClient.Servers.CreateOrUpdate(resourceGroupName, serverName, serverParameters);
            return serverResult;
        }

        static FirewallRule CreateOrUpdateFirewallRule(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string firewallRuleName, string startIpAddress, string endIpAddress)
        {
            FirewallRule firewallParameters = new FirewallRule()
            {
                StartIpAddress = startIpAddress,
                EndIpAddress = endIpAddress
            };
            FirewallRule firewallResult = sqlMgmtClient.FirewallRules.CreateOrUpdate(resourceGroupName, serverName, firewallRuleName, firewallParameters);
            return firewallResult;
        }

        static Database CreateOrUpdateDatabase(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string databaseName, string databaseEdition, string databasePerfLevel)
        {
            // Retrieve hello server that will host this database
            Server currentServer = sqlMgmtClient.Servers.Get(resourceGroupName, serverName);

            // Create a database: configure create or update parameters and properties explicitly
            Database newDatabaseParameters = new Database()
            {
                Location = currentServer.Location,
                CreateMode = CreateMode.Default,
                Edition = databaseEdition,
                RequestedServiceObjectiveName = databasePerfLevel

            };
            Database dbResponse = sqlMgmtClient.Databases.CreateOrUpdate(resourceGroupName, serverName, databaseName, newDatabaseParameters);
            return dbResponse;
        }



        private static AuthenticationResult GetToken(string tenantId, string applicationId, string applicationSecret)
        {
            AuthenticationContext authContext = new AuthenticationContext("https://login.windows.net/" + tenantId);
            _token = authContext.AcquireToken("https://management.core.windows.net/", new ClientCredential(applicationId, applicationSecret));
            return _token;
        }
      }
    }





## <a name="create-a-service-principal-tooaccess-resources"></a>Crear un tooaccess de entidad de seguridad de servicio de recursos
Hello siguiente script de PowerShell crea aplicación de Active Directory (AD) de Hola y el servicio de hello principal que necesitamos tooauthenticate nuestra aplicación de C#. script de Hola genera valores que necesitamos Hola anterior a C# de ejemplo. Para obtener información detallada, vea [toocreate de PowerShell de Azure Use una entidad de servicio tooaccess recursos](../azure-resource-manager/resource-group-authenticate-service-principal.md).

    # Sign in tooAzure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set toohello subscription you want toowork with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is hello display name for your app, must be unique in your directory.
    # $uri does not need toobe a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for hello app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # tooavoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun hello following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output hello values we need for our C# application toosuccessfully authenticate

    Write-Output "Copy these values into hello C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret



## <a name="next-steps"></a>Pasos siguientes
Ahora que has intentado base de datos SQL y configurar una base de datos con C#, todo está listo para hello siguientes artículos:

* [Conectarse tooSQL base de datos con SQL Server Management Studio y realizar una consulta de T-SQL de ejemplo](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a>Recursos adicionales
* [Base de datos SQL](https://azure.microsoft.com/documentation/services/sql-database/)
* [Database (clase)](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

<!--Image references-->
[1]: ./media/sql-database-get-started-csharp/aad.png
[2]: ./media/sql-database-get-started-csharp/permissions.png
[3]: ./media/sql-database-get-started-csharp/getdomain.png
[4]: ./media/sql-database-get-started-csharp/aad2.png
[5]: ./media/sql-database-get-started-csharp/aad-applications.png
[6]: ./media/sql-database-get-started-csharp/add.png
[7]: ./media/sql-database-get-started-csharp/add-application.png
[8]: ./media/sql-database-get-started-csharp/add-application2.png
[9]: ./media/sql-database-get-started-csharp/clientid.png
