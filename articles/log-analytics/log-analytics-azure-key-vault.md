---
title: "aaaAzure solución de almacén de claves en el análisis de registros | Documentos de Microsoft"
description: "Puede usar soluciones de almacén de claves de Azure de hello en tooreview de análisis de registros que registra el almacén de claves de Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 5e25e6d6-dd20-4528-9820-6e2958a40dae
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 1c6eae26ded7ad55b0159a3be09cdc9901596298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a>Solución de Azure Key Vault Analytics en Log Analytics

![Símbolo de Key Vault](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

Puede usar soluciones de almacén de claves de Azure de hello en tooreview de análisis de registros que registra AuditEvent de almacén de claves de Azure.

solución de hello toouse, deberá tooenable el registro de diagnósticos del almacén de claves de Azure y área de trabajo de análisis de registros de hello directa diagnósticos tooa. No es necesario toowrite Hola registros tooAzure almacenamiento de blobs.

> [!NOTE]
> En enero de 2017 Hola admite la manera de enviar registros de análisis cambiado de tooLog de almacén de claves. Si la solución de almacén de claves de hello usa muestra *(en desuso)* en el título de hello, consulte demasiado[migrar de solución de almacén de claves anterior hello](#migrating-from-the-old-key-vault-solution) para conocer los pasos necesita toofollow.
>
>

## <a name="install-and-configure-hello-solution"></a>Instalar y configurar soluciones de Hola
Usar hello siguiendo las instrucciones tooinstall y configurar soluciones de almacén de claves de Azure de hello:

1. Habilitar la solución de almacén de claves de Azure Hola desde [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) o mediante el proceso de hello descrito en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).
2. Habilitar los diagnósticos de registro de toomonitor de recursos del almacén de claves de hello, utilizando cualquier hello [portal](#enable-key-vault-diagnostics-in-the-portal) o [PowerShell](#enable-key-vault-diagnostics-using-powershell)

### <a name="enable-key-vault-diagnostics-in-hello-portal"></a>Habilitar los diagnósticos de almacén de claves en el portal de Hola

1. Hola portal de Azure, navegue toomonitor de recursos del almacén de claves de toohello
2. Seleccione *registros de diagnóstico* hello tooopen después de la página

   ![imagen del icono de Azure Key Vault](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. Haga clic en *Activar diagnósticos* hello tooopen después de la página

   ![imagen del icono de Azure Key Vault](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. tooturn en diagnóstico, haga clic en *en* en *estado*
5. Haga clic en la casilla de verificación de Hola para *enviar tooLog análisis*
6. Seleccione un área de trabajo de Log Analytics existente o cree un área de trabajo.
7. tooenable *AuditEvent* registros, haga clic en la casilla de verificación de Hola de inicio de sesión
8. Haga clic en *guardar* registro de hello tooenable de diagnóstico tooLog análisis

### <a name="enable-key-vault-diagnostics-using-powershell"></a>Habilitación de los diagnósticos de Key Vault mediante PowerShell
Hola siguiente script de PowerShell ofrece un ejemplo de cómo toouse `Set-AzureRmDiagnosticSetting` tooenable registro de diagnóstico para el almacén de claves:
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a>Revisión de los detalles de recopilación de datos de Azure Key Vault
Solución de almacén de claves de Azure recopila registros de diagnósticos directamente desde el almacén de claves de Hola.
No es necesario toowrite Hola registros tooAzure almacenamiento de blobs y no hay ningún agente es necesario para la recopilación de datos.

Hello tabla siguiente muestran los métodos de recopilación de datos y otros detalles acerca de cómo se recopilan los datos de almacén de claves de Azure.

| Plataforma | Agente directo | Agente System Center Operations Manager | Azure | ¿Se requiere Operations Manager? | Se envían los datos del agente de Operations Manager a través del grupo de administración | Frecuencia de recopilación |
| --- | --- | --- | --- | --- | --- | --- |
| Azure |  |  |&#8226; |  |  | a la llegada |

## <a name="use-azure-key-vault"></a>Uso de Azure Key Vault
Después de [instalar soluciones de hello](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), ver los datos de almacén de claves de hello haciendo clic en hello **el almacén de claves de Azure** icono de hello **información general sobre** página de análisis de registros.

![imagen del icono de Azure Key Vault](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

Tras hacer clic en hello **Introducción** icono, puede ver los resúmenes de los registros y, a continuación, explorar en toodetails para hello siguientes categorías:

* Volumen de todas las operaciones de almacén de claves a través del tiempo
* Volúmenes de operaciones fallidas a través del tiempo
* Promedio de latencia operacional por operación
* Calidad de servicio para las operaciones con el número de Hola de las operaciones que tarden más de 1000 ms y una lista de las operaciones que tarden más de 1.000 ms.

![imagen del panel de Azure Key Vault](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![imagen del panel de Azure Key Vault](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="tooview-details-for-any-operation"></a>detalles de tooview para cualquier operación
1. En hello **Introducción** página, haga clic en hello **el almacén de claves de Azure** icono.
2. En hello **el almacén de claves de Azure** panel, revise la información de resumen de Hola de uno de los módulos de hello y, a continuación, haga clic en uno tooview información detallada sobre él en la página de búsqueda de registros de Hola.

    En cualquiera de las páginas de búsqueda de registro de hello, puede ver los resultados por tiempo, resultados detallados y el historial de búsqueda de registros. También puede filtrar por resultados de facetas toonarrow Hola.

## <a name="log-analytics-records"></a>Registros de Log Analytics
Hola soluciones de almacén de claves de Azure analiza los registros que tienen un tipo de **KeyVaults** que se recopilan de [AuditEvent registros](../key-vault/key-vault-logging.md) en diagnósticos de Azure.  Propiedades de estos registros se encuentran en hello en la tabla siguiente:  

| Propiedad | Descripción |
|:--- |:--- |
| Escriba |*AzureDiagnostics* |
| SourceSystem |*Las tablas de Azure* |
| CallerIpAddress |Dirección IP del cliente de Hola que realizó la solicitud de Hola |
| Categoría | *AuditEvent* |
| CorrelationId |Un GUID opcional que Hola cliente puede pasar toocorrelate registros de cliente con los registros del lado del servicio (el almacén de claves). |
| DurationMs |Duración de la solicitud de API de REST de tooservice hello, en milisegundos. Este tiempo no incluye latencia de red, por lo que el tiempo de Hola que mide en el lado del cliente de hello podría no coincidir con este momento. |
| httpStatusCode_d |Código de estado HTTP devuelto por la solicitud de hello (por ejemplo, *200*) |
| id_s |Identificador único de la solicitud de Hola |
| identity_claim_appid_g | GUID para el Id. de aplicación Hola |
| nombreOperación |Nombre de operación de hello, como se documenta en [registro de almacén de claves de Azure](../key-vault/key-vault-logging.md) |
| OperationVersion |Versión de API de REST solicitada por el cliente de hello (por ejemplo *2015-06-01*) |
| requestUri_s |Identificador URI de solicitud de Hola |
| Recurso |Nombre del almacén de claves de Hola |
| ResourceGroup |Grupo de recursos de almacén de claves de Hola |
| ResourceId |Identificador de recursos del Administrador de recursos de Azure Para los registros de almacén de claves, trata de identificador de recurso de almacén de claves de Hola. |
| ResourceProvider |*MICROSOFT.KEYVAULT* |
| ResourceType | *ALMACENES* |
| ResultSignature |Código de estado HTTP (por ejemplo, *OK*) |
| ResultType |Resultado de solicitud de API de REST (por ejemplo, *Correcto*) |
| SubscriptionId |Identificador de suscripción de Azure de suscripción de Hola que contiene el almacén de claves de Hola |

## <a name="migrating-from-hello-old-key-vault-solution"></a>Migración de soluciones de almacén de claves anterior Hola
En enero de 2017 Hola admite la manera de enviar registros de análisis cambiado de tooLog de almacén de claves. Estos cambios proporcionan Hola siguientes ventajas:
+ Los registros se escriben directamente tooLog análisis sin Hola necesita toouse una cuenta de almacenamiento
+ Menor latencia de tiempo de hello cuando los registros están genera toothem está disponible en el análisis de registros
+ Menos pasos de configuración
+ Un formato común para todos los tipos de diagnósticos de Azure

Hola toouse actualiza solución:

1. [Configurar toobe de diagnóstico enviado tooLog análisis directamente desde el almacén de claves](#enable-key-vault-diagnostics-in-the-portal)  
2. Habilitar soluciones de almacén de claves de Azure de hello mediante se describe en el proceso de hello [soluciones de análisis de registros agregue de hello Galería de soluciones](log-analytics-add-solutions.md)
3. Actualizar cualquier consulta guardada, paneles o alertas toouse Hola nuevo tipo de datos
  + Es de tipo de cambio con respecto a: KeyVaults tooAzureDiagnostics. Puede usar Hola ResourceType toofilter tooKey el almacén de registros.
  - En lugar de `Type=KeyVaults`, use `Type=AzureDiagnostics ResourceType=VAULTS`.
  + Campos: (Los nombres de campo distinguen entre mayúsculas y minúsculas).
  - Para cualquier campo que tenga un sufijo de \_s, \_d., o \_g en nombre de hello, cambiar Hola primer carácter toolower mayúsculas y minúsculas
  - Para cualquier campo que tenga un sufijo de \_o en nombre, datos de Hola se divide en campos individuales en función de los nombres de campo de hello anidado. Por ejemplo, hello UPN del autor de llamada de Hola se almacena en un campo`identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`
   - TooCallerIPAddress CallerIpAddress de campo cambiado
   - El campo RemoteIPCountry ya no está presente.
4. Quitar hello *análisis de almacén de claves (en desuso)* solución. Si usa PowerShell, utilice `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`.

Datos recopilan antes de cambiar de hello no está visible en la nueva solución de Hola. Puede seguir tooquery para este uso de datos Hola tipo anterior y nombres de campo.

## <a name="troubleshooting"></a>Solución de problemas
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Pasos siguientes
* Use [búsquedas de registro de análisis de registros](log-analytics-log-searches.md) tooview obtener datos de almacén de claves de Azure.
