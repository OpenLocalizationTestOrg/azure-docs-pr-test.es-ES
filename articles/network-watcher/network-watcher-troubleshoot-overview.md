---
title: "tooresource aaaIntroduction solución de problemas en el Monitor de red de Azure | Documentos de Microsoft"
description: "Esta página proporciona una visión general de las capacidades de solución de problemas de recursos de Monitor de red de Hola"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a>Tooresource de introducción para solucionar problemas de Monitor de red de Azure

Las puertas de enlace de red virtual proporcionan conectividad entre recursos locales y otras redes virtuales dentro de Azure. Estas puertas de enlace y sus conexiones de supervisión es fundamental tooensuring comunicación no se interrumpe. Monitor de red proporciona Hola capacidad tootroubleshoot puertas de enlace de red Virtual y las conexiones. Se puede llamar a través del portal de hello, PowerShell, CLI o API de REST. Cuando se llama, Monitor de red diagnostica mantenimiento Hola de puerta de enlace de red virtual de Hola o conexión y los resultados adecuados de hello devuelto. Esta solicitud es una transacción de larga duración, se devuelve el resultado de hello cuando se complete el diagnóstico de Hola.

![portal][2]

## <a name="results"></a>Results

Hola preliminar resultados proporcionan una perspectiva general del estado de saludo del recurso de Hola. Puede proporcionar información más detallada para recursos tal y como se muestra en los pasos de la sección de hello:

Hello siguiente lista es la API de solucionar problemas de valores de hello devueltos con hello:

* **startTime** -este valor es el tiempo de Hola Hola solucionar problemas de llamada de API que se inició.
* **hora de finalización** -este valor es la hora hello en que finalizó la solución de problemas de Hola.
* **code**: este valor es UnHealthy si se produce un único error de diagnóstico.
* **resultados** -resultados es un conjunto de resultados devuelto en la puerta de enlace de red virtual de conexión o hello de Hola.
    * **Id. de** -este valor es el tipo de error de Hola.
    * **resumen** -este valor es un resumen de error de Hola.
    * **detallada** -este valor proporciona una descripción detallada del error de Hola.
    * **recommendedActions** -esta propiedad es una colección de las acciones recomendadas tootake.
      * **actionText** -este valor contiene texto hello que describe qué tootake de acción.
      * **actionUri** -este valor proporciona Hola URI toodocumentation acerca de cómo tooact.
      * **actionUriText** -este valor es una breve descripción de texto de acción de hello.

Hola siguientes tablas muestran Hola diferentes tipos de error (Id. en los resultados de hello precede a lista) que están disponibles y si el error de hello crea registros.

### <a name="gateway"></a>Puerta de enlace

| Tipo de error | Motivo | Registro|
|---|---|---|
| NoFault | Cuando no se detecta ningún error. |Sí|
| GatewayNotFound | No se encuentra la puerta de enlace o no está aprovisionada. |No|
| PlannedMaintenance |  La instancia de puerta de enlace está en mantenimiento.  |No|
| UserDrivenUpdate | Cuando hay una actualización del usuario en curso. Podría tratarse de una operación de cambio de tamaño. | No |
| VipUnResponsive | No se puede llegar a la instancia principal de Hola de hello puerta de enlace. Esto sucede cuando se produce un error de sondeo de estado de Hola. | No |
| PlatformInActive | Hay un problema con la plataforma de Hola. | No|
| ServiceNotRunning | no se está ejecutando el servicio subyacente Hola. | No|
| NoConnectionsFoundForGateway | No hay ninguna conexión existe en la puerta de enlace de Hola. Esto es solo una advertencia.| No|
| ConnectionsNotConnected | Las conexiones no están conectadas. Esto es solo una advertencia.| Sí|
| GatewayCPUUsageExceeded | uso de CPU de la puerta de enlace actual de Hello es > 95%. | Sí |

### <a name="connection"></a>Conexión

| Tipo de error | Motivo | Registro|
|---|---|---|
| NoFault | Cuando no se detecta ningún error. |Sí|
| GatewayNotFound | No se encuentra la puerta de enlace o no está aprovisionada. |No|
| PlannedMaintenance | La instancia de puerta de enlace está en mantenimiento.  |No|
| UserDrivenUpdate | Cuando hay una actualización del usuario en curso. Podría tratarse de una operación de cambio de tamaño.  | No |
| VipUnResponsive | No se puede llegar a la instancia principal de Hola de hello puerta de enlace. Se produce cuando se produce un error de sondeo de estado de Hola. | No |
| ConnectionEntityNotFound | Falta una configuración de conexión. | No |
| ConnectionIsMarkedDisconnected | Hola conexión está marcada como "desconectada". |No|
| ConnectionNotConfiguredOnGateway | servicio de Hello subyacente no tiene Hola que conexión configurada. | Sí |
| ConnectionMarkedStandy | Hola servicio subyacente está marcada como en espera.| Sí|
| Autenticación | Error de coincidencia de clave previamente compartida. | Sí|
| PeerReachability | puerta de enlace de Hello del mismo nivel no está accesible. | Sí|
| IkePolicyMismatch | puerta de enlace de Hello del mismo nivel tiene directivas IKE que no son compatibles con Azure. | Sí|
| Error de WfpParse | Error al registro WFP Hola análisis. |Sí|

## <a name="supported-gateway-types"></a>Tipos de puerta de enlace admitidos

Hello lista siguiente se muestran compatibilidad hello muestra que las puertas de enlace y las conexiones son compatibles con la solución de problemas de Monitor de red.
|  |  |
|---------|---------|
|**Tipos de puerta de enlace**   |         |
|VPN      | Compatible        |
|ExpressRoute | No compatible |
|HyperNet | No compatible|
|**Tipos de VPN** | |
|Basado en ruta | Compatible|
|Basado en directiva | No compatible|
|**Tipos de conexión**||
|IPSec| Compatible|
|VNet2Vnet| Compatible|
|ExpressRoute| No compatible|
|HyperNet| No compatible|
|VPNClient| No compatible|

## <a name="log-files"></a>Archivos de registro

los archivos de registro para solucionar problemas de recursos de Hola se almacenan en una cuenta de almacenamiento una vez finalizada la solución de problemas de recursos. Hello siguiente imagen muestra contenido de ejemplo de Hola de una llamada que generó un error.

![Archivo ZIP][1]

> [!NOTE]
> En algunos casos, solo un subconjunto de archivos de registro de hello se escribe toostorage.

Para obtener instrucciones acerca de cómo descargar archivos desde cuentas de almacenamiento de azure, consulte demasiado[Introducción al almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Otra herramienta que se puede utilizar es el Explorador de Storage. Para obtener más información acerca del explorador de almacenamiento puede encontrarse aquí en hello siguiente vínculo: [Explorador de almacenamiento](http://storageexplorer.com/)

### <a name="connectionstatstxt"></a>ConnectionStats.txt

Hola **ConnectionStats.txt** archivo contiene estadísticas generales de hello conexión, incluidos los bytes de entrada y salida, el estado de conexión y Hola Hola de tiempo se estableció la conexión.

> [!NOTE]
> Si Hola llamada toohello solución de problemas de API devuelve correcto, lo único que Hola devolvió en el archivo zip de hello es un **ConnectionStats.txt** archivo.

contenido de Hola de este archivo es similar toohello siguiente ejemplo:

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a>CPUStats.txt

Hola **CPUStats.txt** archivo que contiene el uso de CPU y memoria disponible en el tiempo de presentación de las pruebas.  contenido de Hola de este archivo es similar toohello siguiente ejemplo:

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a>IKEErrors.txt

Hola **IKEErrors.txt** archivo contiene los errores de IKE que se encontraron durante la supervisión.

Hello en el ejemplo siguiente se muestra hello contenido de un archivo IKEErrors.txt. Los errores pueden variar según el problema de Hola.

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a>Scrubbed-wfpdiag.txt

Hola **Scrubbed wfpdiag.txt** archivo de registro contiene el registro de wfp Hola. Este registro contiene el registro de errores de IKE y AuthIP, y de pérdida de paquetes.

Hello en el ejemplo siguiente se muestra contenido de hello del archivo de Scrubbed wfpdiag.txt de Hola. En este ejemplo, una clave compartida Hola de una conexión no era correcta como se puede ver desde la línea 3 de Hola desde la parte inferior de Hola. Hola siguiente ejemplo es un fragmento de código de registro completo de hello, como registro de hello puede tardar mucho tiempo según el problema de Hola.

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a>wfpdiag.txt.sum

Hola **wfpdiag.txt.sum** archivo es un registro que muestra los búferes de Hola y eventos procesados.

Hello en el ejemplo siguiente se es Hola contenido de un archivo wfpdiag.txt.sum.
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo toodiagnose puertas de enlace de VPN y conexiones a través de Hola portal visitando [solución de problemas de puerta de enlace: portal de Azure](network-watcher-troubleshoot-manage-portal.md).
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
