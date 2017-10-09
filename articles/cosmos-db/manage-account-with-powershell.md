---
title: "Automatización de la base de datos de Cosmos - aaaAzure de administración con Powershell | Documentos de Microsoft"
description: Use Azure Powershell para administrar las cuentas de Azure Cosmos DB.
services: cosmos-db
author: dmakwana
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: dimakwan
ms.openlocfilehash: 3239fb815918a0e47bff69fcd1ab6562519e429b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a>Creación de una cuenta de Azure Cosmos DB mediante PowerShell

Hello guía siguiente describe comandos tooautomate administración de las cuentas de base de datos de base de datos de Azure Cosmos con Azure Powershell. También incluye las claves de cuenta de toomanage de comandos y las prioridades de conmutación por error de [cuentas de base de datos de varias regiones][scaling-globally]. Actualizar la cuenta de base de datos permite las directivas de coherencia de toomodify y agregar o quitar regiones. Para la administración de varias plataformas de su cuenta de base de datos de Azure Cosmos, puede usar [CLI de Azure](cli-samples.md), hello [API de REST de proveedor de recursos][rp-rest-api], o hello [Azure Portal de](create-documentdb-dotnet.md#create-account).

## <a name="getting-started"></a>Introducción

Siga las instrucciones de hello en [cómo tooinstall y configurar Azure PowerShell] [ powershell-install-configure] tooinstall y registro en Azure Resource Manager tooyour cuenta de Powershell.

### <a name="notes"></a>Notas

* Si desea que hello tooexecute estos comandos sin necesidad de confirmación del usuario, anexar hello `-Force` marca toohello comando.
* Hola todos los siguientes comandos son sincrónicas.

## <a id="create-documentdb-account-powershell"></a> Creación de una cuenta de Azure Cosmos DB

Este comando permite toocreate una cuenta de base de datos de la base de datos de Azure Cosmos. Configure la nueva cuenta de base de datos como de región única o de [varias regiones][scaling-globally] con una determinada [directiva de coherencia](consistency-levels.md).

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`nombre de la ubicación de Hola de hello escribir región de cuenta de base de datos de Hola. Esta ubicación es toohave requiere un valor de prioridad de conmutación por error de 0. Debe haber exactamente una región de escritura por cuenta de base de datos.
* `<read-region-location>`nombre de la ubicación de Hola de hello lee región de cuenta de base de datos de Hola. Esta ubicación es toohave requiere un valor de prioridad de conmutación por error de mayor que 0. Puede haber más de una región de lectura por cuenta de base de datos.
* `<ip-range-filter>`Especifica el conjunto de Hola de direcciones IP o intervalos de direcciones IP de CIDR formulario toobe incluido como lista de direcciones IP de cliente para una cuenta de base de datos determinada de elementos permitido de Hola. Los intervalos o direcciones IP deben ir separados por una coma y no deben contener espacios. Para más información, consulte [Compatibilidad con el firewall de Azure Cosmos DB](firewall-support.md).
* `<default-consistency-level>`nivel de coherencia Hola predeterminado de la cuenta de base de datos de Azure Cosmos Hola. Para más información, consulte [Niveles de coherencia en Azure Cosmos DB](consistency-levels.md).
* `<max-interval>`Cuando se utiliza con coherencia Bounded Staleness, este valor representa cantidad de tiempo de Hola de obsolescencia (en segundos) tolerado. El intervalo aceptado para este valor es de 1 - 100.
* `<max-staleness-prefix>`Cuando se utiliza con coherencia Bounded Staleness, este valor representa el número de Hola de solicitudes obsoletas tolerado. El intervalo aceptado para este valor es de 1 - 2.147.483.647.
* `<resource-group-name>`nombre de Hola de hello [grupo de recursos de Azure] [ azure-resource-groups] toowhich Hola cuenta de base de datos de base de datos de Azure Cosmos nueva pertenece a.
* `<resource-group-location>`ubicación de Hola de hello cuenta de base de datos de grupo de recursos de Azure toowhich Hola nueva base de datos de Azure Cosmos pertenece.
* `<database-account-name>`nombre de Hola de base de datos de base de datos de Azure Cosmos de hello cuenta toobe creado. Sólo puede utilizar letras minúsculas, números, hello '-' caracteres y debe tener entre 3 y 50 caracteres.

Ejemplo: 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a>Notas
* Hello en el ejemplo anterior se crea una base de datos cuenta con dos regiones. También es posible toocreate una cuenta de base de datos con una región (que se designa como la región de escritura de Hola y tiene un valor de prioridad de conmutación por error de 0) o más de dos regiones. Para obtener más información, vea la información de [cuentas de bases de datos de varias regiones][scaling-globally].
* ubicaciones de Hello deben ser las regiones en el que está disponible con carácter general base de datos de Azure Cosmos. lista actual de Hola de regiones se proporciona en hello [página regiones de Azure](https://azure.microsoft.com/regions/#services).

## <a id="update-documentdb-account-powershell"></a> Actualización de una cuenta de base de datos de DocumentDB

Este comando permite tooupdate propiedades de la cuenta de base de datos de la base de datos de Azure Cosmos. Esto incluye la directiva de coherencia de Hola y ubicaciones de hello qué cuenta de base de datos de hello existe en.

> [!NOTE]
> Este comando permite regiones tooadd y quitar, pero no permite las prioridades de conmutación por error de toomodify. las prioridades de conmutación por error de toomodify, consulte [a continuación](#modify-failover-priority-powershell).

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`nombre de la ubicación de Hola de hello escribir región de cuenta de base de datos de Hola. Esta ubicación es toohave requiere un valor de prioridad de conmutación por error de 0. Debe haber exactamente una región de escritura por cuenta de base de datos.
* `<read-region-location>`nombre de la ubicación de Hola de hello lee región de cuenta de base de datos de Hola. Esta ubicación es toohave requiere un valor de prioridad de conmutación por error de mayor que 0. Puede haber más de una región de lectura por cuenta de base de datos.
* `<default-consistency-level>`nivel de coherencia Hola predeterminado de la cuenta de base de datos de Azure Cosmos Hola. Para más información, consulte [Niveles de coherencia en Azure Cosmos DB](consistency-levels.md).
* `<ip-range-filter>`Especifica el conjunto de Hola de direcciones IP o intervalos de direcciones IP de CIDR formulario toobe incluido como lista de direcciones IP de cliente para una cuenta de base de datos determinada de elementos permitido de Hola. Los intervalos o direcciones IP deben ir separados por una coma y no deben contener espacios. Para más información, consulte [Compatibilidad con el firewall de Azure Cosmos DB](firewall-support.md).
* `<max-interval>`Cuando se utiliza con coherencia Bounded Staleness, este valor representa cantidad de tiempo de Hola de obsolescencia (en segundos) tolerado. El intervalo aceptado para este valor es de 1 - 100.
* `<max-staleness-prefix>`Cuando se utiliza con coherencia Bounded Staleness, este valor representa el número de Hola de solicitudes obsoletas tolerado. El intervalo aceptado para este valor es de 1 - 2.147.483.647.
* `<resource-group-name>`nombre de Hola de hello [grupo de recursos de Azure] [ azure-resource-groups] toowhich Hola cuenta de base de datos de base de datos de Azure Cosmos nueva pertenece a.
* `<resource-group-location>`ubicación de Hola de hello cuenta de base de datos de grupo de recursos de Azure toowhich Hola nueva base de datos de Azure Cosmos pertenece.
* `<database-account-name>`nombre de Hola de base de datos de base de datos de Azure Cosmos de hello cuenta toobe actualizado.

Ejemplo: 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <a id="delete-documentdb-account-powershell"></a> Eliminación de una cuenta de base de datos de DocumentDB

Este comando permite toodelete una cuenta de base de datos de base de datos de Azure Cosmos existente.

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* `<resource-group-name>`nombre de Hola de hello [grupo de recursos de Azure] [ azure-resource-groups] toowhich Hola cuenta de base de datos de base de datos de Azure Cosmos nueva pertenece a.
* `<database-account-name>`nombre de Hola de base de datos de base de datos de Azure Cosmos de hello cuenta toobe eliminado.

Ejemplo:

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="get-documentdb-properties-powershell"></a> Obtención de las propiedades de una cuenta de base de datos de DocumentDB

Este comando permite propiedades de hello tooget de una cuenta de base de datos de base de datos de Azure Cosmos existente.

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`nombre de Hola de hello [grupo de recursos de Azure] [ azure-resource-groups] toowhich Hola cuenta de base de datos de base de datos de Azure Cosmos nueva pertenece a.
* `<database-account-name>`nombre de Hola de hello cuenta de base de datos de la base de datos de Azure Cosmos.

Ejemplo:

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="update-tags-powershell"></a> Actualización de la etiquetas de una cuenta de base de datos de Azure Cosmos DB

Hello ejemplo siguiente se describe cómo tooset [etiquetas de recursos de Azure] [ azure-resource-tags] para la base de datos de Azure Cosmos cuenta de base de datos.

> [!NOTE]
> Este comando se puede combinar con hello crear o actualizar comandos anexando hello `-Tags` marca con el parámetro correspondiente de Hola.

Ejemplo:

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <a id="list-account-keys-powershell"></a> Enumerar claves de cuenta

Cuando se crea una cuenta de base de datos de Azure Cosmos, servicio de hello genera dos claves de acceso principal que pueden usarse para la autenticación cuando se tiene acceso a la cuenta de base de datos de Azure Cosmos Hola. Al proporcionar dos claves de acceso, base de datos de Azure Cosmos permite claves de hello tooregenerate con ninguna cuenta de base de datos de Azure Cosmos tooyour de interrupción. También están disponibles las claves de solo lectura para autenticar las operaciones de solo lectura. Hay dos claves de lectura y escritura (principal y secundaria) y dos claves de solo lectura (principal y secundaria).

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`nombre de Hola de hello [grupo de recursos de Azure] [ azure-resource-groups] toowhich Hola cuenta de base de datos de base de datos de Azure Cosmos nueva pertenece a.
* `<database-account-name>`nombre de Hola de hello cuenta de base de datos de la base de datos de Azure Cosmos.

Ejemplo:

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="list-connection-strings-powershell"></a> Enumeración de cadenas de conexión

Para las cuentas de MongoDB, Hola tooconnect de cadena de conexión que se puede recuperar su cuenta de base de datos de MongoDB aplicación toohello mediante el siguiente comando de Hola.

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`nombre de Hola de hello [grupo de recursos de Azure] [ azure-resource-groups] toowhich Hola cuenta de base de datos de base de datos de Azure Cosmos nueva pertenece a.
* `<database-account-name>`nombre de Hola de hello cuenta de base de datos de la base de datos de Azure Cosmos.

Ejemplo:

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="regenerate-account-key-powershell"></a> Regenerar la clave de cuenta

Debe cambiar la cuenta de base de datos de Azure Cosmos de tooyour de claves de acceso de hello periódicamente toohelp proteger las conexiones. Dos claves de acceso se asignan tooenable se toomaintain conexiones toohello cuenta de base de datos de Azure Cosmos mediante una clave de acceso mientras regenera Hola otra clave de acceso.

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* `<resource-group-name>`nombre de Hola de hello [grupo de recursos de Azure] [ azure-resource-groups] toowhich Hola cuenta de base de datos de base de datos de Azure Cosmos nueva pertenece a.
* `<database-account-name>`nombre de Hola de hello cuenta de base de datos de la base de datos de Azure Cosmos.
* `<key-kind>`Uno de hello cuatro tipos de claves: ["Principal" | " Secundaria "|" PrimaryReadonly "|" SecondaryReadonly"] que desearía tooregenerate.

Ejemplo:

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <a id="modify-failover-priority-powershell"></a> Modificación de la prioridad de conmutación por error de una cuenta de base de datos de Azure Cosmos DB

Para las cuentas de base de datos de varias regiones, puede cambiar la prioridad de conmutación por error de Hola de hello diversas regiones que Hola cuenta de base de datos de la base de datos de Azure Cosmos existe en. Para obtener más información sobre la conmutación por error en la cuenta de base de datos de Azure Cosmos DB, consulte [Distribución de datos global con Azure Cosmos DB][distribute-data-globally].

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* `<write-region-location>`nombre de la ubicación de Hola de hello escribir región de cuenta de base de datos de Hola. Esta ubicación es toohave requiere un valor de prioridad de conmutación por error de 0. Debe haber exactamente una región de escritura por cuenta de base de datos.
* `<read-region-location>`nombre de la ubicación de Hola de hello lee región de cuenta de base de datos de Hola. Esta ubicación es toohave requiere un valor de prioridad de conmutación por error de mayor que 0. Puede haber más de una región de lectura por cuenta de base de datos.
* `<resource-group-name>`nombre de Hola de hello [grupo de recursos de Azure] [ azure-resource-groups] toowhich Hola cuenta de base de datos de base de datos de Azure Cosmos nueva pertenece a.
* `<database-account-name>`nombre de Hola de hello cuenta de base de datos de la base de datos de Azure Cosmos.

Ejemplo:

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a>Pasos siguientes

* tooconnect con. NET, vea [conectar y consultas con .NET](create-documentdb-dotnet.md).
* tooconnect mediante .NET Core, vea [conectar y consultas con .NET Core](create-documentdb-dotnet-core.md).
* tooconnect con Node.js, vea [conectar y consulta con Node.js y una aplicación de MongoDB](create-mongodb-nodejs.md).

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
