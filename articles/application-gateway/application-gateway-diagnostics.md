---
title: "aaaMonitor obtener acceso a los registros, registros de rendimiento, estado de back-end y las métricas de puerta de enlace de aplicaciones | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooenable y administrar los registros de acceso y registros de rendimiento para la puerta de enlace de aplicaciones"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a>Mantenimiento del back-end, registro de diagnóstico y métricas de Application Gateway

Mediante el uso de puerta de enlace de aplicaciones de Azure, puede supervisar los recursos en hello siguientes maneras:

* [Estado de back-end](#back-end-health): puerta de enlace de aplicaciones proporciona mantenimiento de hello capacidad toomonitor Hola de servidores de Hola Hola grupos de back-end a través de hello portal de Azure y a través de PowerShell. También puede encontrar el estado de Hola de grupos de back-end de Hola a través de los registros de diagnóstico de rendimiento de Hola.

* [Registros](#diagnostic-logs): los registros permiten para el rendimiento, acceso, y otro datos toobe guarda o consumidos de un recurso con fines de supervisión.

* [Métricas](#metrics): en estos momentos, Application Gateway tiene una métrica. Esta métrica mide el rendimiento de Hola de puerta de enlace de aplicaciones de hello en bytes por segundo.

## <a name="back-end-health"></a>Mantenimiento del back-end

Puerta de enlace de aplicaciones proporciona mantenimiento de hello capacidad toomonitor Hola de miembros individuales de grupos de back-end de Hola a través del portal hello, PowerShell y Hola interfaz de línea de comandos (CLI). También puede encontrar un estado agregado resumen de grupos de back-end a través de los registros de diagnóstico de rendimiento de Hola. 

informe de mantenimiento de back-end de Hello refleja la salida de hello de instancias de hello Application Gateway mantenimiento sondeo toohello back-end. Cuando el sondeo se realiza correctamente y Hola volver final puede recibir tráfico, se considera correcta. En caso contrario, se considera incorrecto.

> [!IMPORTANT]
> Si hay un grupo de seguridad de red (NSG) en una subred de puerta de enlace de aplicaciones, abra 65503 65534 de intervalos de puertos de subred de puerta de enlace de aplicación hello para el tráfico entrante. Estos puertos son necesarios para toowork de API de hello estado back-end.


### <a name="view-back-end-health-through-hello-portal"></a>Ver el estado de back-end a través del portal de Hola

En el portal de hello, mantenimiento de back-end se proporciona automáticamente. En una puerta de enlace de aplicaciones existente, vaya a **Supervisión** > **Estado del back-end**. 

Cada miembro del grupo de back-end de Hola se muestra en esta página (ya sea una NIC, IP o FQDN). Se muestran el nombre del grupo de back-end, el puerto, la configuración HTTP del back-end y el estado de mantenimiento. Los valores válidos para el estado de mantenimiento son **Correcto**, **Incorrecto** y **Desconocido**.

> [!NOTE]
> Si ve un estado de mantenimiento de back-end de **desconocido**, asegúrese de que ese acceso toohello back-end no está bloqueada por una regla de NSG, una ruta definida por el usuario (UDR) o un DNS personalizado en la red virtual de Hola.

![Mantenimiento del back-end][10]

### <a name="view-back-end-health-through-powershell"></a>Visualización del mantenimiento del back-end mediante PowerShell

Hola siguiente código de PowerShell muestra cómo tooview mantenimiento de back-end mediante el uso de Hola `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a>Visualización del mantenimiento del back-end mediante la CLI de Azure 2.0

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a>Results

Hola siguiente fragmento de código muestra un ejemplo de respuesta de hello:

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <a name="diagnostic-logging"></a>Registros de diagnóstico

Puede usar varios tipos de registros de Azure toomanage y solucionar problemas de las puertas de enlace de la aplicación. Puede tener acceso a algunos de estos registros a través del portal de Hola. Se pueden extraer todos los registros de Azure Blob Storage y visualizarse en distintas herramientas, como [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel y PowerBI. Puede aprender más sobre Hola diferentes tipos de registros de hello lista siguiente:

* **Registro de actividad**: puede usar [registros de actividad de Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anteriormente conocidos como registros operativos y los registros de auditoría) tooview todas las operaciones que son envían tooyour suscripción de Azure y su estado. Las entradas del registro de actividades se recopilan de forma predeterminada, y puede verlos en hello portal de Azure.
* **Registro de acceso**: puede usar esta patrones de acceso de registro tooview puerta de enlace de aplicación y analizar información importante, incluyendo llamador Hola IP, dirección URL solicitada, latencia de la respuesta, código de retorno y los bytes de entrada y salida. El registro de acceso se recopila cada 300 segundos. Este registro contiene un registro por cada instancia de Application Gateway. instancia de puerta de enlace de aplicación Hola puede identificarse por la propiedad instanceId de Hola.
* **Registro de rendimiento**: puede usar esta tooview de registro que el rendimiento de las instancias de puerta de enlace de aplicaciones. Este registro captura la información de rendimiento de cada instancia, incluida la cantidad total de solicitudes atendidas, el rendimiento en bytes, la cantidad de solicitudes con error y el número de instancias de back-end con un mantenimiento correcto o incorrecto. El registro de rendimiento se recopila cada 60 segundos.
* **Registro de Firewall**: puede usar este registro de solicitudes de Hola de tooview que se registra con el modo de detección o prevención de una puerta de enlace de la aplicación que está configurado con el servidor de aplicaciones web de Hola.

> [!NOTE]
> Registros solo están disponibles para los recursos implementados en el modelo de implementación de hello Azure Resource Manager. No puede usar registros de recursos en el modelo de implementación clásica de Hola. Para entender mejor de los modelos de hello dos, vea hello [Administrador de recursos de la descripción y la implementación clásica](../azure-resource-manager/resource-manager-deployment-model.md) artículo.

Tiene tres opciones para almacenar los archivos de registro:

* **Cuenta de almacenamiento**: cuentas que resultan especialmente útiles para registros cuando estos se almacenan durante mucho tiempo y se revisan cuando es necesario.
* **Los concentradores de eventos**: concentradores de eventos son una buena opción para la integración con otra información de seguridad y tooget alertas en los recursos de las herramientas de administración de eventos (SEIM).
* **Log Analytics**: se usa para la supervisión general en tiempo real de la aplicación o para examinar las tendencias.

### <a name="enable-logging-through-powershell"></a>Habilitación del registro con PowerShell

El registro de actividades se habilita automáticamente para todos los recursos de Resource Manager. Debe habilitar el acceso y toostart de registro de rendimiento recolección de datos de hello disponibles a través de esos registros. tooenable registro Hola uso pasos:

1. Tenga en cuenta los identificadores de recursos de su cuenta de almacenamiento, donde se almacenan los datos de registro de hello. Este valor es del formulario de hello: / Subscriptions /\<subscriptionId\>/ResourceGroups /\<nombre del grupo de recursos\>/providers/Microsoft.Storage/storageAccounts/\<denombredelacuentadealmacenamiento\>. Puede usar cualquier cuenta de almacenamiento de la suscripción. Hola toofind portal Azure puede usar esta información.

    ![Portal: identificador de recurso de la cuenta de almacenamiento](./media/application-gateway-diagnostics/diagnostics1.png)

2. Observe el identificador de recurso de la puerta de enlace de aplicaciones para la que se está habilitando el registro. Este valor es del formulario de hello: / Subscriptions /\<subscriptionId\>/ResourceGroups /\<nombre del grupo de recursos\>/providers/Microsoft.Network/applicationGateways/\<puerta de enlace de aplicaciones nombre\>. Puede utilizar Hola portal toofind esta información.

    ![Portal: identificador de recurso de la puerta de enlace de aplicaciones](./media/application-gateway-diagnostics/diagnostics2.png)

3. Habilitar el registro de diagnóstico utilizando Hola siguiente cmdlet de PowerShell:

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
>Los registros de actividades no requieren una cuenta de almacenamiento separada. uso de Hola de almacenamiento para el acceso y el registro de rendimiento incurre en cargos por servicio.

### <a name="enable-logging-through-hello-azure-portal"></a>Habilitar el registro a través de hello portal de Azure

1. En Hola portal de Azure, busque el recurso y haga clic en **registros de diagnóstico**.

   Hay tres registros de auditoría disponibles para Application Gateway:

   * Registro de acceso
   * Registro de rendimiento
   * Registro de firewall

2. recopilar datos de toostart, haga clic en **Activar diagnósticos**.

   ![Activación de los diagnósticos][1]

3. Hola **configuración de diagnóstico** hoja proporciona una configuración de Hola para hello registros de diagnóstico. En este ejemplo, análisis de registros almacena los registros de Hola. Haga clic en **configurar** en **análisis de registros** tooconfigure el área de trabajo. También puede utilizar un registros de diagnóstico de Hola de almacenamiento cuenta toosave y centros de eventos.

   ![Iniciar el proceso de configuración Hola][2]

4. En Operations Management Suite (OMS), elija un área de trabajo existente o cree uno. Este ejemplo utiliza una existente.

   ![Opciones para áreas de trabajo OMS][3]

5. Confirmar configuración de Hola y haga clic en **guardar**.

   ![Hoja de configuración de diagnóstico con selecciones][4]

### <a name="activity-log"></a>Registro de actividades

Azure genera el registro de actividad de Hola de forma predeterminada. Hola registros se conservan durante 90 días en almacén de hello Azure registros de eventos. Obtener más información sobre estos registros leyendo hello [ver eventos y registros de actividad](../monitoring-and-diagnostics/insights-debugging-with-events.md) artículo.

### <a name="access-log"></a>Registro de acceso

registro de acceso de Hola se genera solo si se ha habilitado en cada instancia de puerta de enlace de aplicaciones, como se detalla en hello pasos anteriores. Hola datos se almacenan en la cuenta de almacenamiento de Hola que especificó cuando se habilitó el registro de hello. Cada acceso de puerta de enlace de aplicaciones se registra en formato JSON, tal y como se muestra en el siguiente ejemplo de Hola:


|Valor  |Descripción  |
|---------|---------|
|instanceId     | Esa solicitud Hola atienden la instancia de puerta de enlace de aplicaciones.        |
|clientIP     | IP de origen para la solicitud de saludo.        |
|clientPort     | Puerto de solicitud de Hola de origen.       |
|httpMethod     | Método HTTP utilizado por solicitud de saludo.       |
|requestUri     | URI de solicitud recibido Hola.        |
|RequestQuery     | **Server enrutara**: instancia de grupo Back-end que se envió la solicitud de saludo. </br> **X-AzureApplicationGateway-registro-ID**: Id. de correlación usado para solicitud de saludo. Puede ser problemas de tráfico de tootroubleshoot usadas en servidores de back-end de Hola. </br>**ESTADO del servidor**: código de respuesta HTTP que recibe de puerta de enlace de aplicaciones de back-end de Hola.       |
|UserAgent     | Agente de usuario Hola HTTP del encabezado de solicitud.        |
|httpStatus     | Código de estado HTTP devuelto toohello cliente de puerta de enlace de aplicaciones.       |
|HttpVersion     | Versión HTTP de solicitud de saludo.        |
|receivedBytes     | Tamaño de paquete recibido, en bytes.        |
|sentBytes| Tamaño de paquete enviado, en bytes.|
|timeTaken| Período de tiempo (en milisegundos) que se tarda en un toobe solicitud procesados y su toobe de respuesta enviados. Esto se calcula como el intervalo de saludo de tiempo de hello cuando la puerta de enlace de aplicación recibe el primer byte de una hora de toohello de solicitud HTTP respuesta Hola enviar operación finalice Hola. Es importante toonote que Hola campo Time-Taken normalmente incluye el tiempo de Hola que viajan a través de red de hello paquetes de saludo de solicitud y respuesta. |
|sslEnabled| Indica si los grupos de back-end de comunicación toohello utilizan SSL. Los valores válidos son on y off.|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a>Registro de rendimiento

registro de rendimiento de Hola se genera solo si se ha habilitado en cada instancia de puerta de enlace de aplicaciones, como se detalla en hello pasos anteriores. Hola datos se almacenan en la cuenta de almacenamiento de Hola que especificó cuando se habilitó el registro de hello. datos de registro de rendimiento de saludo se generan en intervalos de 1 minuto. se registra Hola datos siguientes:


|Valor  |Descripción  |
|---------|---------|
|instanceId     |  Instancia de Application Gateway para la que se van a generar los datos. Si hay varias instancias de Application Gateway, hay una fila por cada instancia.        |
|healthyHostCount     | Número de hosts correcto en el grupo de back-end de Hola.        |
|unHealthyHostCount     | Número de hosts en mal estado en el grupo de back-end de Hola.        |
|requestCount     | Número de solicitudes atendidas.        |
|latency | Latencia (en milisegundos) de las solicitudes de hello instancia toohello back-end que atiende solicitudes de Hola. |
|failedRequestCount| Número de solicitudes con error.|
|throughput| Rendimiento medio desde el último registro de hello, medido en bytes por segundo.|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> Latencia se calcula a partir de la hora de hello cuando el primer byte de la solicitud HTTP de Hola Hola es tiempo toohello recibidos cuando se envía el último byte de respuesta HTTP Hola Hola. Suma del Hola su de Hola tiempo de procesamiento de puerta de enlace de aplicaciones más hello toohello de costo de red nuevo finalizar, más tiempo de Hola que Hola back-end toma tooprocess Hola solicitud.

### <a name="firewall-log"></a>Registro de firewall

registro de firewall de Hola se genera solo si se ha habilitado para cada puerta de enlace de la aplicación, como se detalla en hello pasos anteriores. Este registro también requiere que firewall de aplicación web de hello esté configurado en una puerta de enlace de la aplicación. Hola datos se almacenan en la cuenta de almacenamiento de Hola que especificó cuando se habilitó el registro de hello. se registra Hola datos siguientes:


|Valor  |Descripción  |
|---------|---------|
|instanceId     | Instancia de Application Gateway para la que se van a generar los datos de firewall. Si hay varias instancias de Application Gateway, hay una fila por cada instancia.         |
|clientIp     |   IP de origen para la solicitud de saludo.      |
|clientPort     |  Puerto de solicitud de Hola de origen.       |
|requestUri     | Dirección URL de solicitud recibida Hola.       |
|ruleSetType     | Tipo de conjunto de reglas. valor de Hello disponible es OWASP.        |
|ruleSetVersion     | Versión utilizada del conjunto de reglas. Los valores disponibles son 2.2.9 y 3.0.     |
|ruleId     | Id. de regla de hello desencadenar el evento.        |
|Mensaje     | Mensaje descriptivo para desencadenar eventos de Hola. En la sección de detalles de Hola se proporcionan más detalles.        |
|action     |  Acción realizada en la solicitud de saludo. Los valores disponibles son Blocked y Allowed.      |
|site     | Sitio para que Hola se generó el registro. Actualmente, solo se incluye Global porque las reglas son globales.|
|details     | Detalles del programa Hola a desencadenar el evento.        |
|details.message     | Descripción de regla de Hola.        |
|details.data     | Datos específicos encuentran en la solicitud esa regla coincidente Hola.         |
|details.file     | Archivo de configuración que contiene la regla de Hola.        |
|details.line     | Número de línea del archivo de configuración de Hola que desencadenó el evento de Hola.       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a>Ver y analizar el registro de actividad de Hola

Puede ver y analizar datos de registro de actividad mediante cualquiera de los siguientes métodos de hello:

* **Herramientas de Azure**: recuperar la información de registro de actividad de Hola a través de PowerShell de Azure, CLI de Azure, API de REST de Azure, Hola Hola u Hola portal de Azure. Instrucciones paso a paso para cada método se detallan en hello [operaciones de actividad con el Administrador de recursos](../azure-resource-manager/resource-group-audit.md) artículo.
* **Power BI:** si todavía no tiene una cuenta de [Power BI](https://powerbi.microsoft.com/pricing) , puede probarlo gratis. Mediante el uso de hello [contenido de los registros de actividad de Azure para Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), puede analizar los datos con paneles preconfigurados que pueden usar tal cual o personalizar.

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a>Ver y analizar el acceso de hello, el rendimiento y los registros de firewall

Azure [análisis de registros](../log-analytics/log-analytics-azure-networking-analytics.md) puede recopilar archivos de registro de eventos y contadores de hello de la cuenta de almacenamiento de blobs. Incluye visualizaciones y tooanalyze de las capacidades de búsqueda eficaces los registros.

También puede conectar la cuenta de almacenamiento de tooyour y recuperar entradas de registro de hello JSON para los registros de acceso y el rendimiento. Después de descargar los archivos JSON hello, puede convertirlos tooCSV y verlos en Excel, Power BI o cualquier otra herramienta de visualización de datos.

> [!TIP]
> Si está familiarizado con los conceptos básicos del cambio de valores de constantes y variables de C# y Visual Studio, puede usar hello [iniciar herramientas de convertidor](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponible en GitHub.
> 
> 

## <a name="metrics"></a>Métricas

Las métricas son una característica para determinados recursos de Azure donde puede ver los contadores de rendimiento en el portal de Hola. En el caso de Application Gateway, actualmente hay disponible una métrica. Esta métrica es el rendimiento, y puede verlo en el portal de Hola. Puerta de enlace de aplicaciones de tooan y haga clic en **métricas**. valores de hello tooview, seleccione rendimiento Hola **métricas disponibles** sección. Hola después de la imagen, puede ver un ejemplo con filtros de Hola que puede usar datos de hello toodisplay en intervalos de tiempo diferentes.

![Vista de métrica con filtros][5]

vea una lista actualizada de las métricas, toosee [métricas con el Monitor de Azure admitidas](../monitoring-and-diagnostics/monitoring-supported-metrics.md).

### <a name="alert-rules"></a>Las reglas de alertas

Puede iniciar las reglas de alerta en función de las métricas de un recurso. Por ejemplo, una alerta puede llamar a un webhook o un administrador de correo electrónico si el rendimiento de puerta de enlace de aplicación Hola Hola es encima, debajo o con un umbral durante un período especificado.

Hola ejemplo siguiente le guía por la creación de una regla de alerta que envía un administrador de tooan de correo electrónico después de las infracciones de rendimiento un umbral:

1. Haga clic en **Agregar alerta métrica** tooopen hello **Agregar regla** hoja. También puede tener acceso a esta hoja de hoja de métricas de Hola.

   ![Botón “Agregar alerta de métrica”][6]

2. En hello **Agregar regla** hoja, rellene el nombre de hello, condición y notificar a secciones y haga clic en **Aceptar**.

   * Hola **condición** selector, seleccione uno de los valores de hello cuatro: **mayor**, **igual o mayor que**, **inferior a**, o  **Menor o igual que**.

   * Hola **período** selector, seleccione un período de 5 minutos too6 horas.

   * Si selecciona **correo electrónico a los propietarios, contributors y readers**, correo electrónico de hello puede ser dinámica en función de los usuarios de Hola que tienen acceso a recursos de toothat. En caso contrario, puede proporcionar una lista separada por comas de los usuarios de hello **email(s) Administrador adicional** cuadro.

   ![Hoja Agregar regla][7]

Si se supera el umbral de hello, llega un correo electrónico que es toohello similar uno Hola después de imagen:

![Correo electrónico para el umbral infringido][8]

Después de crear una alerta de métrica, aparece una lista de alertas. Proporciona una visión general de todas las reglas de alerta de Hola.

![Lista de alertas y reglas][9]

toolearn más información acerca de las notificaciones de alerta, consulte [recibir notificaciones de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

toounderstand más información acerca de webhooks y cómo se pueden utilizar las alertas, visite [configurar un webhook en una alerta de métrica Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="next-steps"></a>Pasos siguientes

* Visualice el contador y los registros de eventos con [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).
* Consulte la entrada de blog [Visualize your Azure Activity Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) (Visualizar los registros de actividades de Azure con Power BI).
* Consulte la entrada de blog [View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) (Consulta y análisis de registros de auditoría de Azure en Power BI y más).

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
