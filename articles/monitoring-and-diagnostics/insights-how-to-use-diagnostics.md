---
title: "supervisión de aaaEnable y diagnósticos de Microsoft Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset de diagnóstico para los recursos en Azure."
author: rboucher
manager: carolz
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: af1947a9-c211-4aa1-8924-880a86240be4
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 865d010c5846fff6d871e20eca2bc4ac35028354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-monitoring-and-diagnostics"></a>Habilitación de supervisión y diagnóstico
Hola [Portal de Azure](https://portal.azure.com), puede configurar enriquecidos y frecuentes, los datos de supervisión y diagnóstico sobre los recursos. También puede usar hello [API de REST](https://msdn.microsoft.com/library/azure/dn931932.aspx) o [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooconfigure diagnóstico mediante programación.

Los datos de diagnóstico, supervisión y métrica de Azure se guardan en una cuenta de almacenamiento de su elección. Esto le permite toouse cualquier conjunto de herramientas desea que los datos de hello tooread, desde el Explorador de almacenamiento, herramientas de terceros toothird de BI de tooPower.

## <a name="when-you-create-a-resource"></a>Cuando se crea un recurso
La mayoría de servicios le permite tooenable diagnóstico cuando se crea en primer lugar en hello [Portal de Azure](https://portal.azure.com).

1. Vaya demasiado**New** y elija recursos de Hola que le interesen.
2. Seleccione **Configuración opcional**.
    ![Hoja Diagnósticos](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)
3. Seleccione **Diagnósticos** y haga clic en **Activar**. Necesitará cuenta de almacenamiento de hello toochoose que desea toobe de diagnóstico guardado en. Se le cobrarán tarifas normales por el almacenamiento y las transacciones al enviar la cuenta de almacenamiento de tooa de diagnóstico.
4. Haga clic en **Aceptar** y crear el recurso de Hola.

## <a name="change-settings-for-an-existing-resource"></a>Cambio de la configuración de un recurso existente
Si ya ha creado un recurso y desea que la configuración de diagnóstico hello toochange (nivel de toochange Hola de recopilación de datos, por ejemplo), puede hacerlo directamente en hello Portal de Azure.

1. Recursos de toohello y haga clic en hello **configuración** comando.
2. Haga clic en **Diagnósticos**.
3. Hola **diagnósticos** hoja tiene todas de diagnóstico posible hello y supervisar los datos de colección para ese recurso. Para algunos recursos también puede elegir un **retención** directiva para los datos de hello, tooclean, configúrelo de la cuenta de almacenamiento.
    ![Diagnósticos de almacenamiento](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)
4. Una vez que ha elegido la configuración, haga clic en hello **guardar** comando. Puede tardar un poco mientras que para la supervisión de datos tooshow seguridad si va a habilitar, para hello primera vez.

### <a name="categories-of-data-collection-for-virtual-machines"></a>Categorías de recopilación de datos para máquinas virtuales
Para máquinas virtuales de todos los registros y las métricas se grabará a intervalos de un minuto, por lo que siempre puede tener información actualizada la mayoría de hello sobre su equipo.

* **Métricas básicas** : métricas de mantenimiento sobre la máquina virtual, como el procesador y la memoria.
* **Métricas web y de red** : métricas sobre las conexiones de red y los servicios web.
* **Las métricas de .NET** : las métricas relacionadas con aplicaciones .NET y ASP.NET Hola se ejecutan en la máquina virtual
* **Métricas SQL** : si está ejecutando el servicio SQL de Microsoft, sus métricas de rendimiento.
* **Registros de eventos de aplicación de Windows** : eventos de Windows que se envían los canales de aplicación toohello
* **Registros de sistema de eventos de Windows** : eventos de Windows que se envían toohello canal del sistema. También se incluyen todos los eventos de [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).
* **Registros de seguridad de eventos de Windows** : eventos de Windows que se envían el canal de seguridad toohello
* **Registros de infraestructura de diagnóstico** : registro acerca de la infraestructura de recopilación de diagnósticos de Hola
* **Registros IIS** : registros sobre su servidor IIS.

Tenga en cuenta que en este momento no se admiten ciertas distribuciones de Linux y, Hola agente invitado debe estar instalado en la máquina virtual de Hola.

## <a name="next-steps"></a>Pasos siguientes
* [Reciba notificaciones de alerta](insights-receive-alert-notifications.md) cada vez que se produzcan eventos de operaciones o las métricas traspasen un umbral.
* [Supervisar las métricas de servicio](insights-how-to-customize-monitoring.md) toomake que el servicio esté disponible y capacidad de respuesta.
* [Escalar el número de instancias automáticamente](insights-how-to-scale.md) toomake seguro de la escala de servicio según la demanda.
* [Supervisar el rendimiento de la aplicación](../application-insights/app-insights-azure-web-apps.md) si desea toounderstand exactamente cómo se está realizando el código en la nube de Hola.
* [Ver eventos y registros de actividad](insights-debugging-with-events.md) toolearn todo lo que se ha producido en el servicio.
* [Realizar un seguimiento de estado del servicio](insights-service-health.md) toofind out cuando Azure ha experimentado interrupciones de degradación o servicio de rendimiento.

