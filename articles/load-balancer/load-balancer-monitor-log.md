---
title: aaaMonitor operaciones, eventos y contadores de equilibrador de carga | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooenable eventos de alerta y sondeo de registro de estado de mantenimiento para el equilibrador de carga de Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a>Análisis del registros para el Equilibrador de carga de Azure

Puede usar diferentes tipos de registros en Azure toomanage y solucionar problemas de equilibradores de carga. Algunos de estos registros pueden tener acceso a través del portal de Hola. Se pueden extraer todos los registros desde Azure Blob Storage y visualizarse en distintas herramientas, como Excel y PowerBI. Se puede obtener más información sobre Hola diferentes tipos de registros de lista de hello siguiente.

* **Registros de auditoría:** puede usar [los registros de auditoría de Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anteriormente conocido como registros operativos) tooview todas las operaciones que se va a tooyour enviado suscripciones de Azure y su estado. Los registros de auditoría están habilitados de forma predeterminada y pueden verse en hello portal de Azure.
* **Registros de eventos de alertas:** puede utilizar esta rasied de alertas de registro tooview equilibrador de carga de Hola. estado de Hola Hola equilibrador de carga se recopila cada cinco minutos. Este registro se escribe solo si se produce un evento de alerta del equilibrador de carga.
* **Registros de sondeo de estado:** puede utilizar esta tooview los registros de problemas detectados por el sondeo de estado, como el número de Hola de instancias en el grupo back-end que no reciben las solicitudes del equilibrador de carga de hello debido a errores de sondeo de estado. Este registro se escribe toowhen hay un cambio en el estado de sondeo de estado de Hola.

> [!IMPORTANT]
> El análisis de registros actualmente solo funciona para los equilibradores de carga orientados hacia Internet. Registros solo están disponibles para los recursos implementados en el modelo de implementación del Administrador de recursos de Hola. No puede usar registros de recursos en el modelo de implementación clásica de Hola. Para obtener más información acerca de los modelos de implementación de hello, consulte [Administrador de recursos de la descripción y la implementación clásica](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="enable-logging"></a>Habilitación del registro

El registro de auditoría se habilita automáticamente para todos los recursos de Resource Manager. Necesita eventos tooenable y toostart de registro de mantenimiento sondeo recopilar datos de hello disponibles a través de esos registros. Usar hello siguiendo el registro de pasos tooenable.

Inicio de sesión toohello [portal de Azure](http://portal.azure.com). Si aún no tiene un equilibrador de carga, [cree uno](load-balancer-get-started-internet-arm-ps.md) antes de continuar.

1. En el portal de hello, haga clic en **examinar**.
2. Seleccione **Equilibradores de carga**.

    ![portal - load-balancer](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. Seleccione un equilibrador de carga existente >> **Toda la configuración**.
4. En hello derecha del cuadro de diálogo Hola nombre Hola Hola de equilibrador de carga, desplácese demasiado**supervisión**, haga clic en **diagnósticos**.

    ![portal - load-balancer-settings](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. Hola **diagnósticos** panel, en **estado**, seleccione **en**.
6. Haga clic en **Cuenta de almacenamiento**.
7. En **Registros**, seleccione una cuenta de almacenamiento existente o cree una nueva. Utilice toodetermine de control deslizante de Hola durante cuántos días correspondientes a los datos de eventos se almacenarán en los registros de eventos de Hola. 
8. Haga clic en **Guardar**.

    ![Portal - Registros de diagnósticos](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> Los registros de auditoría no requieren una cuenta de almacenamiento separada. Hola uso de almacenamiento para el evento y el estado de registro de sondeo supondrán un coste adicional de servicio.

## <a name="audit-log"></a>Registro de auditoría

registro de auditoría de Hola se genera de forma predeterminada. Hola registros se conservan durante 90 días en el almacén de registros de eventos de Azure. Obtener más información sobre estos registros leyendo hello [ver eventos y registros de auditoría](../monitoring-and-diagnostics/insights-debugging-with-events.md) artículo.

## <a name="alert-event-log"></a>Registro de eventos de alerta

Este registro solo se genera si lo habilitó para cada uno de los equilibradores de carga. eventos de Hola se registran en formato JSON y se almacena en la cuenta de almacenamiento de hello especificada cuando se habilitó el registro de hello. Hola aquí te mostramos un ejemplo de un evento.

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

Hola JSON de salida muestra hello *eventname* propiedad que se describirá el motivo de Hola Hola equilibrador de carga crea una alerta. En este caso, alerta de hello generada venció el agotamiento de puertos de tooTCP causado por origen que IP NAT limita (SNAT).

## <a name="health-probe-log"></a>Registro de sondeo de estado

Este registro solo se genera si lo habilitó para cada uno de los equilibradores de carga, tal como se indicó anteriormente. Hola datos se almacenan en la cuenta de almacenamiento de hello especificada cuando se habilitó el registro de hello. Se crea un contenedor denominado 'loadbalancerprobehealthstatus de registros de visión' y se registra Hola datos siguientes:

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

salida JSON de Hello muestra de Hola propiedades campo Hola información básica de estado de mantenimiento de sondeo de Hola. Hola *dipDownCount* propiedad muestra el número total de Hola de instancias en hello back-end, que no están recibiendo tráfico de red debido a las respuestas del sondeo de toofailed.

## <a name="view-and-analyze-hello-audit-log"></a>Ver y analizar el registro de auditoría de Hola

Puede ver y analizar datos de registro de auditoría mediante cualquiera de los siguientes métodos de hello:

* **Herramientas de Azure:** recuperar información de los registros de auditoría de Hola a través de PowerShell de Azure, hello Azure interfaz de línea de comandos (CLI), Hola API de REST de Azure, u Hola portal de vista previa. Instrucciones paso a paso para cada método se detallan en hello [auditoría de las operaciones con el Administrador de recursos](../azure-resource-manager/resource-group-audit.md) artículo.
* **Power BI:** si todavía no tiene una cuenta de [Power BI](https://powerbi.microsoft.com/pricing), puede probarlo gratis. Con hello [contenido de los registros de auditoría de Azure para Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), puede analizar los datos con paneles configurados previamente o puede personalizar vistas toosuit sus requisitos.

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a>Ver y analizar el sondeo de estado de Hola y de registro de eventos

Necesita tooconnect tooyour almacenamiento de la cuenta y recuperar entradas de registro de hello JSON para registros de sondeo de estado y eventos. Una vez descargados los archivos de hello JSON, puede convertir tooCSV y view en Excel, Power BI o cualquier otra herramienta de visualización de datos.

> [!TIP]
> Si está familiarizado con los conceptos básicos del cambio de valores de constantes y variables de C# y Visual Studio, puede usar hello [iniciar herramientas de convertidor](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponible en GitHub.

## <a name="additional-resources"></a>Recursos adicionales

* [Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) (Visualizar los registros de auditoría de Azure con Power BI).
* [View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) (Visualizar los registros de auditoría de Azure con Power BI).

## <a name="next-steps"></a>Pasos siguientes

[Descripción de los sondeos del equilibrador de carga](load-balancer-custom-probe-overview.md)
