---
title: "valores de aaaGet para la autenticación de aplicación, base de datos de SQL de Azure | Documentos de Microsoft"
description: "Cree una entidad de servicio para tener acceso a SQL Database desde el código."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
tags: 
ms.assetid: b43e43bb-6660-49e6-b069-abde97eb5770
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 09/30/2016
ms.author: sstein
ms.openlocfilehash: b57dc075ec9e679da9f2f5fa53e02312539cdf07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-required-values-for-authenticating-an-application-tooaccess-sql-database-from-code"></a>Obtener valores de hello necesario para autenticar un tooaccess de aplicación base de datos SQL desde el código
toocreate y administrar la base de datos SQL desde el código que se debe registrar la aplicación en dominio de Azure Active Directory (AAD) de hello en la suscripción de Hola donde se han creado los recursos de Azure.

## <a name="create-a-service-principal-tooaccess-resources-from-an-application"></a>Crear un tooaccess de entidad de seguridad de servicio de recursos desde una aplicación
Necesita toohave hello más reciente [Azure PowerShell](https://msdn.microsoft.com/library/mt619274.aspx) instalado y en ejecución. Para obtener información detallada, vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azureps-cmdlets-docs).

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




## <a name="see-also"></a>Otras referencias
* [Creación de una Base de datos SQL con C#](sql-database-get-started-csharp.md)
* [Conexión tooSQL base de datos mediante Active Directory autenticación de Azure](sql-database-aad-authentication.md)

