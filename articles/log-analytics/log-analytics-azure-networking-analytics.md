---
title: "solución de análisis de red en el análisis de registros aaaAzure | Documentos de Microsoft"
description: "Puede usar Hola soluciones de análisis de redes de Azure en registros de puerta de enlace de aplicaciones de Azure y análisis de registros tooreview registros de grupo de seguridad de red de Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a>Soluciones de supervisión de redes de Azure en Log Analytics

Análisis de registros ofrecen Hola siguientes soluciones para supervisar las redes:
* Monitor de rendimiento de red (NPM)
 * Supervisar el estado de saludo de la red
* Azure tooreview de análisis de puerta de enlace de aplicaciones
 * Registros de Azure Application Gateway
 * Métricas de Azure Application Gateway
* Tooreview de análisis del grupo de seguridad de red de Azure
 * Registros de Azure Network Security Group

## <a name="network-performance-monitor-npm"></a>Network Performance Monitor (NPM) (monitor de rendimiento de red)

Hola [Monitor de rendimiento de red](log-analytics-network-performance-monitor.md) solución de administración es una solución, que supervisa la disponibilidad de redes, la disponibilidad y el estado de Hola de supervisión de red.  Es utilizado toomonitor conectividad entre:

* Nube pública y entorno local
* Centros de datos y ubicaciones de usuario (sucursales)
* Subredes que hospedan distintos niveles de una aplicación de varios niveles.

Para más información consulte [Network Performance Monitor](log-analytics-network-performance-monitor.md).

## <a name="azure-application-gateway-and-network-security-group-analytics"></a>Azure Application Gateway y Network Security Group Analytics
soluciones de Hola toouse:
1. Agregar tooLog de solución de administración de hello análisis, y
2. Habilitar el área de trabajo de diagnóstico toodirect Hola diagnósticos tooa análisis de registros. No es necesario toowrite Hola registros tooAzure almacenamiento de blobs.

Puede habilitar el diagnóstico y solución de hello correspondientes para uno o ambos de los grupos de seguridad de red y puerta de enlace de aplicaciones.

Si no habilita el registro de diagnóstico para un tipo de recurso determinado, pero instalar soluciones de hello, hojas de panel de Hola para ese recurso están en blanco y mostrar un mensaje de error.

> [!NOTE]
> En enero de 2017 Hola admite manera de enviar registros de puertas de enlace de aplicaciones y grupos de seguridad de red tooLog cambiado de análisis. Si ve hello **el análisis de redes de Azure (en desuso)** solución, consulte demasiado[migrar desde soluciones de análisis de red antiguo hello](#migrating-from-the-old-networking-analytics-solution) para conocer los pasos necesita toofollow.
>
>

## <a name="review-azure-networking-data-collection-details"></a>Revisión de los detalles de recopilación de datos de redes de Azure
análisis de la puerta de enlace de aplicaciones de Azure de Hola y soluciones de administración de análisis de grupo de seguridad de red de hello recopilan registros de diagnósticos directamente desde las puertas de enlace de aplicaciones de Azure y los grupos de seguridad de red. No es necesario toowrite Hola registros tooAzure almacenamiento de blobs y no hay ningún agente es necesario para la recopilación de datos.

Hello tabla siguiente muestran los métodos de recopilación de datos y otros detalles acerca de cómo se recopilan los datos para el análisis de la puerta de enlace de aplicaciones de Azure y análisis del grupo de seguridad de red de Hola.

| Plataforma | Agente directo | Agente System Center Operations Manager | Azure | ¿Se requiere Operations Manager? | Se envían los datos del agente de Operations Manager a través del grupo de administración | Frecuencia de recopilación |
| --- | --- | --- | --- | --- | --- | --- |
| Azure |  |  |&#8226; |  |  |Cuando se inicia sesión |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a>Solución Azure Application Gateway Analytics de Log Analytics

![Símbolo de Azure Application Gateway Analytics](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

Hola siguiendo los registros es compatibles con las puertas de enlace de la aplicación:

* ApplicationGatewayAccessLog
* ApplicationGatewayPerformanceLog
* ApplicationGatewayFirewallLog

Hola siguiendo las métricas se admite para las puertas de enlace de la aplicación:

* Rendimiento de 5 minutos

### <a name="install-and-configure-hello-solution"></a>Instalar y configurar soluciones de Hola
Usar hello siguiendo las instrucciones tooinstall y configurar soluciones de análisis de hello puerta de enlace de aplicaciones de Azure:

1. Habilitar la solución de análisis de puerta de enlace de aplicaciones de Azure Hola de [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) o mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).
2. Habilitar el registro de diagnóstico para hello [las puertas de enlace de la aplicación](../application-gateway/application-gateway-diagnostics.md) desea toomonitor.

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a>Habilitar los diagnósticos de puerta de enlace de aplicaciones de Azure en el portal de Hola

1. Hola portal de Azure, navegue toohello Application Gateway recursos toomonitor
2. Seleccione *registros de diagnóstico* hello tooopen después de la página

   ![imagen del recurso de Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. Haga clic en *Activar diagnósticos* hello tooopen después de la página

   ![imagen del recurso de Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. tooturn en diagnóstico, haga clic en *en* en *estado*
5. Haga clic en la casilla de verificación de Hola para *enviar tooLog análisis*
6. Seleccione un área de trabajo de Log Analytics existente o cree un área de trabajo.
7. Haga clic en la casilla de hello en **registro** para cada uno de toocollect de tipos de registro de hello
8. Haga clic en *guardar* registro de hello tooenable de diagnóstico tooLog análisis

#### <a name="enable-azure-network-diagnostics-using-powershell"></a>Habilitación de los diagnósticos de red de Azure con PowerShell

Hola siguiente script de PowerShell ofrece un ejemplo de cómo tooenable registro de diagnóstico para las puertas de enlace de la aplicación.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a>Uso de análisis de Azure Application Gateway
![imagen del icono de análisis de Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

Tras hacer clic en hello **análisis de puerta de enlace de aplicaciones de Azure** icono en hello información general, puede ver resúmenes de los registros y, a continuación, profundizar en toodetails para hello siguientes categorías:

* Registros de acceso de Application Gateway
  * Errores de cliente y servidor de los registros de acceso de Application Gateway
  * Solicitudes por hora para cada Application Gateway
  * Solicitudes fallidas por hora para cada Application Gateway
  * Errores por agente de usuario de las puertas de enlace de las aplicaciones
* Rendimiento de Application Gateway
  * Estado de host de Application Gateway
  * Percentil 95 y máximo para las solicitudes fallidas de Application Gateway

![imagen del panel de análisis de Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![imagen del panel de análisis de Azure Application Gateway](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

En hello **análisis de puerta de enlace de aplicaciones de Azure** panel, revise la información de resumen de Hola de uno de los módulos de hello y, a continuación, haga clic en uno tooview para obtener información acerca de la página de búsqueda de registros de Hola.

En cualquiera de las páginas de búsqueda de registro de hello, puede ver los resultados por tiempo, resultados detallados y el historial de búsqueda de registros. También puede filtrar por resultados de facetas toonarrow Hola.


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a>Solución Azure Network Security Group Analytics de Log Analytics

![Símbolo de Azure Network Security Group Analytics](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

Hola siguiendo los registros es compatibles con grupos de seguridad de red:

* NetworkSecurityGroupEvent
* NetworkSecurityGroupRuleCounter

### <a name="install-and-configure-hello-solution"></a>Instalar y configurar soluciones de Hola
Usar hello siguiendo las instrucciones tooinstall y configurar soluciones de análisis de redes de Azure de hello:

1. Habilitar la solución de análisis de grupo de seguridad de red de Azure Hola de [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) o mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).
2. Habilitar el registro de diagnóstico para hello [grupo de seguridad de red](../virtual-network/virtual-network-nsg-manage-log.md) recursos que desee toomonitor.

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a>Habilitar los diagnósticos de grupo de seguridad de red de Azure en el portal de Hola

1. Hola portal de Azure, navegue toomonitor de recurso de grupo de seguridad de red toohello
2. Seleccione *registros de diagnóstico* hello tooopen después de la página

   ![imagen del recurso Grupo de seguridad de red de Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. Haga clic en *Activar diagnósticos* hello tooopen después de la página

   ![imagen del recurso Grupo de seguridad de red de Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. tooturn en diagnóstico, haga clic en *en* en *estado*
5. Haga clic en la casilla de verificación de Hola para *enviar tooLog análisis*
6. Seleccione un área de trabajo de Log Analytics existente o cree un área de trabajo.
7. Haga clic en la casilla de hello en **registro** para cada uno de toocollect de tipos de registro de hello
8. Haga clic en *guardar* registro de hello tooenable de diagnóstico tooLog análisis

### <a name="enable-azure-network-diagnostics-using-powershell"></a>Habilitación de los diagnósticos de red de Azure con PowerShell

Hola siguiente script de PowerShell ofrece un ejemplo de cómo tooenable registro de diagnóstico para los grupos de seguridad de red
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a>Uso de Azure Network Security Group Analytics
Tras hacer clic en hello **análisis de grupo de seguridad de red de Azure** icono en hello información general, puede ver resúmenes de los registros y, a continuación, profundizar en toodetails para hello siguientes categorías:

* Flujos bloqueados de grupos de seguridad de red
  * Reglas de los grupos de seguridad de red con flujos bloqueados
  * Direcciones MAC con flujos bloqueados
* Flujos permitidos en los grupos de seguridad de red
  * Reglas de los grupos de seguridad de red con flujos permitidos
  * Direcciones MAC con flujos permitidos

![imagen del panel Azure Network Security Group Analytics](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![imagen del panel Azure Network Security Group Analytics](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

En hello **análisis de grupo de seguridad de red de Azure** panel, revise la información de resumen de Hola de uno de los módulos de hello y, a continuación, haga clic en uno tooview para obtener información acerca de la página de búsqueda de registros de Hola.

En cualquiera de las páginas de búsqueda de registro de hello, puede ver los resultados por tiempo, resultados detallados y el historial de búsqueda de registros. También puede filtrar por resultados de facetas toonarrow Hola.

## <a name="migrating-from-hello-old-networking-analytics-solution"></a>Migración de soluciones de análisis de red antiguo Hola
En enero de 2017 Hola admite la manera de enviar registros de puertas de enlace de aplicaciones de Azure y grupos de seguridad de red de Azure tooLog cambiado de análisis. Estos cambios proporcionan Hola siguientes ventajas:
+ Los registros se escriben directamente tooLog análisis sin Hola necesita toouse una cuenta de almacenamiento
+ Menor latencia de tiempo de hello cuando los registros están genera toothem está disponible en el análisis de registros
+ Menos pasos de configuración
+ Un formato común para todos los tipos de diagnósticos de Azure

Hola toouse actualiza soluciones:

1. [Configurar toobe de diagnóstico enviado tooLog análisis directamente desde las puertas de enlace de aplicaciones de Azure](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [Configurar toobe de diagnóstico que se envían directamente tooLog análisis de grupos de seguridad de red de Azure](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. Habilitar hello *análisis de puerta de enlace de aplicaciones de Azure* hello y *análisis de grupo de seguridad de red de Azure* solución mediante Hola proceso se describe en [soluciones de análisis de registros agregar desde Hola Galería de soluciones](log-analytics-add-solutions.md)
3. Actualizar cualquier consulta guardada, paneles o alertas toouse Hola nuevo tipo de datos
  + El tipo es tooAzureDiagnostics. Puede usar registros de red de hello ResourceType toofilter tooAzure.

    | En lugar de: | Uso: |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + Para cualquier campo que tenga un sufijo de \_s, \_d., o \_g en nombre de hello, cambiar Hola primer carácter toolower mayúsculas y minúsculas
   + Para cualquier campo que tenga un sufijo de \_o en nombre, datos de Hola se divide en campos individuales en función de los nombres de campo de hello anidado.
4. Quitar hello *análisis de redes de Azure (en desuso)* solución.
  + Si usa PowerShell, utilice `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`.

Datos recopilan antes de cambiar de hello no está visible en la nueva solución de Hola. Puede seguir tooquery para este uso de datos Hola tipo anterior y nombres de campo.

## <a name="troubleshooting"></a>Solución de problemas
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Pasos siguientes
* Use [búsquedas de registro de análisis de registros](log-analytics-log-searches.md) tooview obtener datos de diagnóstico de Azure.
