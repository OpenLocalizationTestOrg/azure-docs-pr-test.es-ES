---
title: "Habilitación de la supervisión y el diagnóstico de Microsoft Azure | Microsoft Docs"
description: "Obtenga información acerca de la configuración del diagnóstico de los recursos en Azure."
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
ms.openlocfilehash: b82bb1ab419831e803689edb2a2a7fe256dde5a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enable-monitoring-and-diagnostics"></a>Habilitación de supervisión y diagnóstico
En el [Portal Azure](https://portal.azure.com), puede configurar datos exhaustivos y frecuentes de supervisión y diagnóstico sobre sus recursos. También puede usar la [API de REST](https://msdn.microsoft.com/library/azure/dn931932.aspx) o el [SDK de .NET](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) para configurar diagnósticos mediante programación.

Los datos de diagnóstico, supervisión y métrica de Azure se guardan en una cuenta de almacenamiento de su elección. Esto le permite usar las herramientas que quiera, desde un explorador de almacenamiento, pasando por Power BI hasta herramientas de terceros, para leer los datos.

## <a name="when-you-create-a-resource"></a>Cuando se crea un recurso
La mayoría de los servicios le permiten habilitar el diagnóstico cuando los crea por primera vez en el [Portal Azure](https://portal.azure.com).

1. Vaya a **Nuevo** y elija el recurso que le interesa.
2. Seleccione **Configuración opcional**.
    ![Hoja Diagnósticos](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)
3. Seleccione **Diagnósticos** y haga clic en **Activar**. Deberá elegir la cuenta de almacenamiento en la que quiere que se guarden los diagnósticos. Cuando envíe diagnósticos a una cuenta de almacenamiento, se le cobrará de acuerdo a las tarifas de datos normales relativas a almacenamiento y transacciones.
4. Haga clic en **Aceptar** y cree el recurso.

## <a name="change-settings-for-an-existing-resource"></a>Cambio de la configuración de un recurso existente
Si ya ha creado un recurso y desea cambiar la configuración de diagnóstico (para cambiar el nivel de recopilación de datos, por ejemplo), puede hacerlo directamente en el Portal de Azure.

1. Vaya al recurso y haga clic en el comando **Configuración** .
2. Haga clic en **Diagnósticos**.
3. La hoja **Diagnósticos** contiene todos los datos posibles recopilados sobre supervisión y diagnóstico asociados con ese recurso. En algunos recursos también puede elegir una directiva de **Retención** para los datos, para limpiarlos de la cuenta de almacenamiento.
    ![Diagnósticos de almacenamiento](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)
4. Después de que haya elegido la configuración, haga clic en el comando **Guardar** . Puede que los datos de supervisión tarden un rato en mostrarse si es la primera vez que habilita esta opción.

### <a name="categories-of-data-collection-for-virtual-machines"></a>Categorías de recopilación de datos para máquinas virtuales
Todos los registros y métricas de las máquinas virtuales se registran a intervalos de un minuto, así que siempre dispondrá de la información más actualizada sobre la máquina.

* **Métricas básicas** : métricas de mantenimiento sobre la máquina virtual, como el procesador y la memoria.
* **Métricas web y de red** : métricas sobre las conexiones de red y los servicios web.
* **Métricas .NET** : métricas sobre las aplicaciones .NET y ASP.NET que se ejecutan en la máquina virtual.
* **Métricas SQL** : si está ejecutando el servicio SQL de Microsoft, sus métricas de rendimiento.
* **Registros de la aplicación de eventos de Windows** : los eventos de Windows que se envían al canal de la aplicación.
* **Registros del sistema de eventos de Windows** : los eventos de Windows que se envían al canal del sistema. También se incluyen todos los eventos de [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).
* **Registros de seguridad de eventos de Windows** : los eventos de Windows que se envían al canal de seguridad.
* **Registros de infraestructura de diagnóstico** : registro sobre la infraestructura de recopilación de diagnósticos.
* **Registros IIS** : registros sobre su servidor IIS.

Tenga en cuenta que actualmente no se admiten algunas distribuciones de Linux y que, además, el agente invitado debe instalarse en la máquina virtual.

## <a name="next-steps"></a>Pasos siguientes
* [Reciba notificaciones de alerta](insights-receive-alert-notifications.md) cada vez que se produzcan eventos de operaciones o las métricas traspasen un umbral.
* [Supervise las métricas de servicio](insights-how-to-customize-monitoring.md) para asegurarse de que el servicio está disponible y responde correctamente.
* [Escale el número de instancias automáticamente](insights-how-to-scale.md) para asegurarse de que la escala de servicio está basada en la demanda.
* [Supervise el rendimiento de la aplicación](../application-insights/app-insights-azure-web-apps.md) si desea comprender exactamente cómo funciona su código en la nube.
* [Vea eventos y el registro de actividades](insights-debugging-with-events.md) para saber todo lo que ha sucedido en el servicio.
* [Realice el seguimiento del estado del servicio](insights-service-health.md) para averiguar cuándo ha sufrido  Azure interrupciones del servicio o degradación del rendimiento.
