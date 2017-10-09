---
title: arquitectura de conectividad de base de datos de SQL aaaAzure | Documentos de Microsoft
description: Este documento explica Hola de arquitectura de conectividad SQLDB de Azure desde dentro de Azure o desde fuera de Azure.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a>Arquitectura de conectividad de Azure SQL Database 

En este artículo se explica la arquitectura de conectividad de base de datos de SQL Azure de Hola y explica el funcionan de los distintos componentes de hello toodirect instancia de tooyour de tráfico de la base de datos de SQL Azure. Estos componentes de conectividad de base de datos de SQL Azure funcionen toohello de tráfico de red de toodirect base de datos de Azure con clientes que se conectan desde dentro de Azure y con clientes que se conectan desde fuera de Azure. En este artículo también proporciona toochange de ejemplos de script cómo se produce la conectividad y consideraciones de hello relacionados con la configuración de conectividad de toochanging Hola predeterminada. Si le surge alguna pregunta después de leer este artículo, póngase en contacto con Dhruv en dmalik@microsoft.com. 

## <a name="connectivity-architecture"></a>Arquitectura de conectividad

Hola siguiente diagrama proporciona una descripción general de hello arquitectura de conectividad de base de datos de SQL Azure. 

![Descripción general de la arquitectura](./media/sql-database-connectivity-architecture/architecture-overview.png)


Hello pasos siguientes describen cómo es la conexión establecida tooan base de datos SQL de Azure a través de puerta de enlace de base de datos de SQL Azure de Hola y Hola base de datos de SQL Azure software equilibrador de carga (SLB).

- Los clientes dentro de Azure o fuera de Azure conectan toohello SLB, que tiene una dirección IP pública y escucha en el puerto 1433.
- Hola SLB dirige la puerta de enlace de tráfico toohello base de datos de SQL Azure.
- puerta de enlace de Hello redirige Hola tráfico toohello correcta del proxy middleware.
- Hola proxy middleware redirige Hola tráfico toohello SQL Azure base de datos correspondiente.

> [!IMPORTANT]
> Cada uno de estos componentes distribuye de denegación de protección de servicio (DDoS) integrado en la red de Hola y de capa de aplicación Hola.
>

## <a name="connectivity-from-within-azure"></a>Conectividad desde dentro de Azure

Si va a conectarse desde dentro de Azure, las conexiones tienen una directiva de conexión predeterminada basada en el **redireccionamiento**. Una directiva de **redirigir** significa que las conexiones después de la sesión TCP hello es la base de datos de SQL Azure de toohello establecida, sesión de cliente de hello es, a continuación, redirige toohello middleware de proxy con una cambio toohello destino dirección IP virtual de de hello toothat de puerta de enlace de base de datos de SQL Azure de middleware de proxy de Hola. Por lo tanto, todos los paquetes posteriores fluyen directamente a través de middleware de proxy de hello, omitiendo la puerta de enlace de base de datos de SQL Azure Hola. Hola siguiente diagrama ilustra este flujo de tráfico.

![Descripción general de la arquitectura](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a>Conectividad desde fuera de Azure

Si va a conectarse desde fuera de Azure, las conexiones tienen una directiva de conexión predeterminada basada en el **proxy**. Una directiva de **Proxy** significa que la sesión TCP de Hola se establece a través de puerta de enlace de base de datos de SQL Azure hello y todos los paquetes posteriores fluyen a través de Hola puerta de enlace. Hola siguiente diagrama ilustra este flujo de tráfico.

![Descripción general de la arquitectura](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a>Direcciones IP de la puerta de enlace de Azure SQL Database

tooconnect tooan SQL Azure base de datos de recursos locales, deberá tooallow puerta de enlace de red saliente tráfico toohello base de datos de SQL Azure para su región de Azure. Las conexiones sólo se van a través de puerta de enlace de hello al conectarse en modo de Proxy, que es el predeterminado de hello cuando se conecta desde recursos locales.

Hola tabla siguiente se muestran Hola principal y secundaria de direcciones IP de puerta de enlace de base de datos de SQL Azure de Hola para todas las regiones de datos. En algunas regiones, hay dos direcciones IP. En estas regiones, dirección IP principal de hello es Hola dirección IP de puerta de enlace de Hola y Hola segunda dirección IP es una dirección IP de conmutación por error. dirección de conmutación por error de Hello es Hola dirección toowhich tengamos que pasamos la disponibilidad del servicio de servidor tookeep Hola alta. Para estas regiones, se recomienda permitir saliente tooboth direcciones IP de Hola. dirección IP de la segunda Hello es propiedad de Microsoft y no escuchar todos los servicios hasta que se activa por las conexiones de base de datos de SQL Azure tooaccept.

| Nombre de región | Dirección IP principal | Dirección IP secundaria |
| --- | --- |--- |
| Australia Oriental | 191.238.66.109 | 13.75.149.87 |
| Sudeste de Australia | 191.239.192.109 | 13.73.109.251 |
| Sur de Brasil | 104.41.11.5 | |    
| Centro de Canadá | 40.85.224.249 | |    
| Este de Canadá | 40.86.226.166 | |
| Central EE. UU.: | 23.99.160.139 | 13.67.215.62 |
| Asia oriental | 191.234.2.139 | 52.175.33.150 |
| Este de EE. UU. 1 | 191.238.6.43 | 40.121.158.30 |
| Este de EE. UU. 2 | 191.239.224.107 | 40.79.84.180 |
| India central | 104.211.96.159  | |   
| Sur de India | 104.211.224.146  | |
| India occidental | 104.211.160.80 | |
| Este de Japón | 191.237.240.43 | 13.78.61.196 |
| Oeste de Japón | 191.238.68.11 | 104.214.148.156 |
| Corea Central | 52.231.32.42 | |
| Corea del Sur | 52.231.200.86 |  |
| Centro-Norte de EE. UU | 23.98.55.75 | 23.96.178.199 |
| Europa del Norte | 191.235.193.75 | 40.113.93.91 |
| Centro-Sur de EE. UU | 23.98.162.75 | 13.66.62.124 |
| Sudeste de Asia | 23.100.117.95 | 104.43.15.0 |
| Norte del Reino Unido | 13.87.97.210 | |
| Sur de Reino Unido 1 | 51.140.184.11 | |    
| Sur del Reino Unido 2 | 13.87.34.7 | |
| Oeste de Reino Unido | 51.141.8.11  | |
| Centro occidental de EE.UU. | 13.78.145.25 | |
| Europa occidental | 191.237.232.75 | 40.68.37.158 |
| Oeste de EE. UU. 1 | 23.99.34.75 | 104.42.238.205 |
| Oeste de EE. UU. 2 | 13.66.226.202  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a>Cambio de la directiva de conexión de Azure SQL Database

Hola toochange directiva de conexión de base de datos de SQL Azure para un servidor de base de datos de SQL Azure, use hello [API de REST](https://msdn.microsoft.com/library/azure/mt604439.aspx). 

- Si la directiva de conexión se establece demasiado**Proxy**, todo el flujo de paquetes a través de puerta de enlace de base de datos de SQL Azure Hola de red. Para esta configuración, debe IP de puerta de enlace de tooallow tooonly saliente Hola base de datos de SQL Azure. El uso de la configuración de **proxy** ofrece más latencia que la de **redireccionamiento**. 
- Si está configurando la directiva de conexión **redirigir**, todos los paquetes de red directamente fluyen toohello middleware proxy. Para esta configuración, debe tooallow saliente toomultiple direcciones IP. 

## <a name="script-toochange-connection-settings"></a>Configuración de conexión de script toochange

> [!IMPORTANT]
> Este script requiere hello [módulo Azure PowerShell](/powershell/azure/install-azurerm-ps).
>

Hola siguiente script de PowerShell muestra cómo toochange Hola directiva de conexión.

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a>Pasos siguientes

- Para obtener información sobre cómo toochange Hola directiva de conexión de base de datos de SQL Azure para un servidor de base de datos de SQL Azure, consulte [Create o directiva de conexión del servidor de actualización utilizando Hola API de REST](https://msdn.microsoft.com/library/azure/mt604439.aspx).
- Para obtener información sobre el comportamiento de conexión de Azure SQL Database para clientes que usan ADO.NET 4.5 o una versión posterior, vea [Puertos más allá de 1433 para ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).
- Para obtener información general sobre el desarrollo de aplicaciones, vea [Introducción al desarrollo de aplicaciones en SQL Database](sql-database-develop-overview.md).
