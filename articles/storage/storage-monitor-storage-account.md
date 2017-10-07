---
title: aaaHow toomonitor una cuenta de almacenamiento de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomonitor una cuenta de almacenamiento de Azure mediante el uso de Hola portal de Azure."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: 782873648fdbccc0191a074cd4044f97af8b7c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-storage-account-in-hello-azure-portal"></a>Supervisar una cuenta de almacenamiento en hello portal de Azure

[Análisis de Azure Storage](storage-analytics.md) proporciona métricas para todos los servicios de almacenamiento y registros para blobs, colas y tablas. Puede usar hello [portal de Azure](https://portal.azure.com) tooconfigure qué métricas y los registros se registra para su cuenta y configura gráficos que proporcionan representaciones visuales de los datos de métricas.

> [!NOTE]
> Hay costos asociados a examinar los datos de supervisión de hello portal de Azure. Para obtener más información, consulte [Facturación y análisis de almacenamiento](/rest/api/storageservices/Storage-Analytics-and-Billing).
>
> Almacenamiento de archivos de Azure admite actualmente las métricas del Análisis de almacenamiento, pero aún no admite el registro.
>
> Cuentas de almacenamiento con un tipo de replicación de almacenamiento con redundancia de zona (ZRS) actualmente no tiene las métricas de Hola o capacidad de registro habilitados.
> 
> Para obtener una guía detallada sobre el uso de análisis de almacenamiento y otra herramientas tooidentify, diagnosticar y solucionar problemas relacionados con el almacenamiento de Azure, vea [supervisar, diagnosticar y solucionar problemas de almacenamiento de Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).
>

## <a name="configure-monitoring-for-a-storage-account"></a>la supervisión para una cuenta de almacenamiento

1. Hola [portal de Azure](https://portal.azure.com), seleccione **cuentas de almacenamiento**, a continuación, panel de cuenta hello tooopen de nombre de la cuenta de almacenamiento de Hola.
1. Seleccione **diagnósticos** en hello **supervisión** sección de hoja de menú de Hola.

    ![OpcionesSupervisión](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. Seleccione hello **tipo** de datos de métricas para cada **servicio** desea toomonitor y Hola **directiva de retención** para datos de Hola. También puede deshabilitar la supervisión estableciendo **estado** demasiado**desactivar**.

    ![OpcionesSupervisión](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   Hay dos tipos de métricas que puede habilitar para cada servicio. Ambos están habilitados de forma predeterminada en el caso de nuevas cuentas de almacenamiento:

   * **Agregados**: recopila métricas como entrada/salida, disponibilidad, latencia y porcentajes de éxito. Estas métricas se agregan para hello blob, cola, tabla y servicios de archivo.
   * **Por API**: en suma toohello las métricas agregadas, recopila Hola el mismo conjunto de métricas para cada operación de almacenamiento en hello API del servicio de almacenamiento de Azure.

   Directiva de retención de datos de hello tooset, mover hello **retención (días)** control deslizante o escriba Hola número de días de tooretain de datos, de 1 too365. valor predeterminado de Hola para las nuevas cuentas de almacenamiento es siete días. Si no desea tooset una directiva de retención, escriba cero. Si no hay ninguna directiva de retención, es tooyou toodelete Hola datos de supervisión.

   > [!WARNING]
   > Se le cobrará si elimina manualmente datos de métricas. Datos de análisis obsoleto (anterior a la directiva de retención de datos) se eliminan por sistema Hola sin costo alguno. Se recomienda establecer una directiva de retención en función de cuánto tiempo desea tooretain datos de análisis de almacenamiento para su cuenta. Consulte [¿Qué se le facturará cuando habilite las métricas de almacenamiento?](storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) para más información.
   >

1. Cuando haya terminado la configuración de supervisión de hello, seleccione **guardar**.

Un conjunto predeterminado de las métricas se muestra en los gráficos en la hoja de cuenta de almacenamiento de hello, así como las hojas de servicio individuales de hello (blob, cola, tabla y archivo). Una vez que ha habilitado las métricas para un servicio, puede llevar hasta hora tooan para tooappear de datos en sus gráficos. Puede seleccionar **editar** en cualquier métrica del gráfico demasiado[configurar qué métricas](#how-to-customize-metrics-charts) se muestran en el gráfico de Hola.

Puede deshabilitar la colección de métricas y registro estableciendo **estado** demasiado**desactivar**.

> [!NOTE]
> Almacenamiento de Azure usa [almacenamiento de tablas](storage-introduction.md#table-storage) toostore las métricas de hello para la cuenta de almacenamiento y las métricas de Hola de almacenes en tablas en su cuenta. Para más información, consulte [Cómo se almacenan las métricas](storage-analytics.md#how-metrics-are-stored).
>

## <a name="customize-metrics-charts"></a>Personalización de gráficos de métricas

Usar hello siguiendo el procedimiento toochoose qué tooview de métricas de almacenamiento en un gráfico de métricas. 

1. Muestra un gráfico de métricas de almacenamiento en el portal de Azure Hola primero. Puede encontrar los gráficos en hello **hoja de la cuenta de almacenamiento** y Hola **métricas** hoja para un servicio concreto (blob, cola, tabla, archivo).

   En este ejemplo, trabajamos con hello después de gráfico que aparece en hello **hoja de la cuenta de almacenamiento**:

   ![Selección de gráfico en Azure Portal](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. A continuación, haga clic en cualquier lugar dentro de Hola Hola de tooopen de gráfico **métrica** hoja. Seleccione **Editar gráfico** tooopen hello **Editar gráfico** hoja.

   ![Botón Editar gráfico de la hoja del gráfico](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. En hello **Editar gráfico** hoja, seleccione hello **intervalo de tiempo** de toodisplay de métricas de hello en gráfico de Hola y Hola **servicio** (blob, cola, tabla o archivo) cuyas métricas que desea toodisplay. Aquí hemos seleccionado hello toodisplay más allá de las métricas de la semana para servicio de blob de hello:

   ![Selección de intervalo y el servicio de hora en la hoja de hello Editar gráfico](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. Seleccione Hola individuales **métricas** tenía como aparece en gráfico de Hola, a continuación, haga clic en **Aceptar**. Por ejemplo, aquí hemos elegido hello toodisplay *ContainerCount* y *ObjectCount* métricas:

   ![Selección de métricas individuales en la hoja Editar gráfico](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

La configuración del gráfico no afectan a la colección de hello, agregación o almacenamiento de datos en la cuenta de almacenamiento de Hola de supervisión, solo Hola visualización de los datos de métricas.

### <a name="metrics-availability-in-charts"></a>Disponibilidad de las métricas en los gráficos

lista de Hola de cambios de métricas disponibles en función de servicio que ha elegido en la lista desplegable de Hola y tipo de unidad de hello del gráfico de Hola que está editando. Por ejemplo, puede seleccionar métricas de porcentaje como *PercentNetworkError* y *PercentThrottlingError* solo si está editando un gráfico que muestra las unidades en porcentajes:

![Gráfico de porcentaje de error de solicitud en hello portal de Azure](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a>Resolución de métricas

las métricas de Hello seleccionado en el diagnóstico determina la resolución de Hola de métricas de Hola que están disponibles para su cuenta:

* **Agregados**: la supervisión proporciona métricas como entrada/salida, disponibilidad, latencia y porcentajes de éxito. Estas métricas se agregan de hello, tabla, archivo, servicios blob y cola.
* **Por API** proporciona una solución más preciso, con las métricas disponibles para las operaciones de almacenamiento individuales, además de toohello agregados de nivel de servicio.

## <a name="configure-metrics-alerts"></a>Configuración de las alertas de métricas

Puede crear alertas toonotify cuando se alcanzan los umbrales para las métricas de recursos de almacenamiento.

1. Hola tooopen **hoja de reglas de alerta**, desplácese hacia abajo toohello **supervisión** sección de hello **hoja de menú** y seleccione **reglas de alerta**.
1. Seleccione **Agregar alerta** tooopen hello **agregar una regla de alerta** hoja
1. Seleccione un **recursos** (blob, archivo, poner en cola, tabla) de Hola desplegable y escriba un **nombre** y **descripción** para la nueva regla de alerta.
1. Seleccione hello **métrica** para que le gustaría tooadd una alerta, una alerta **condición**y un **umbral**. cambios de tipo de unidad de umbral de Hello según la métrica de Hola que ha elegido. Por ejemplo, "count" es el tipo de unidad de Hola para *ContainerCount*, durante la unidad de Hola para hello *PercentNetworkError* métrica es un porcentaje.
1. Seleccione hello **período**. Las métricas que alcanzan o superan Hola umbral en desencadenador de período de hello una alerta.
1. (Opcional) Configure las notificaciones de **Correo electrónico** y **Webhook**. Para más información sobre webhooks, consulte [Configuración de un webhook en una alerta de métrica de Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md). Si no configura las notificaciones de correo electrónico o webhook, alertas aparecerá solo en hello portal de Azure.

!['Agregar una regla de alerta' hoja Hola portal de Azure](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-toohello-portal-dashboard"></a>Agregar panel del portal toohello métricas gráficos

Puede agregar gráficos de métricas de almacenamiento de Azure para cualquiera de su panel de portal de tooyour de cuentas de almacenamiento.

1. Seleccione haga clic en **editar panel** mientras se visualiza el panel en hello [portal de Azure](https://portal.azure.com).
1. Hola **icono galería**, seleccione **buscar iconos por** > **tipo**.
1. Seleccione **Tipo** > **Cuentas de almacenamiento**.
1. En **recursos**, seleccione cuenta de almacenamiento de hello cuyas métricas que se va tooadd toohello panel.
1. Seleccione **Categorías** > **Supervisión**.
1. Gráfico de Hola de arrastrar y colocar en mosaico en el panel de métrica de hello le gustaría mostrar. Repita para todas las métricas le gustaría que se muestra en el panel de Hola. Hola después de la imagen, se resalta el gráfico de "Blobs - Nº Total de solicitudes" hello como un ejemplo, pero todos los gráficos de hello están disponibles para la ubicación en el panel.

   ![Galería de iconos de Azure Portal](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. Seleccione **realiza personalizar** cerca parte superior de hello del panel de hello cuando haya terminado de agregar los gráficos.

Una vez que ha agregado el panel de tooyour de gráficos, se puede personalizar aún más tal y como se describe en [personalizar gráficos de métricas](#how-to-customize-metrics-charts).

## <a name="configure-logging"></a>registro

Puede indicar a registros de diagnósticos de toosave de almacenamiento de Azure para lectura, escritura y eliminación de solicitudes de hello, tabla, servicios blob y cola. Directiva de retención de datos de Hello establece también aplica a registros de toothese.

> [!NOTE]
> Almacenamiento de archivos de Azure admite actualmente las métricas del Análisis de almacenamiento, pero aún no admite el registro.
>

1. Hola [portal de Azure](https://portal.azure.com), seleccione **cuentas de almacenamiento**, y después el nombre de hoja de hello almacenamiento cuenta tooopen Hola almacenamiento cuenta Hola.
1. Seleccione **diagnósticos** en hello **supervisión** sección de hoja de menú de Hola.

    ![Elemento de menú de diagnósticos en supervisión en hello portal de Azure.](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. Asegúrese de **estado** se establece demasiado**en**, seleccione hello y **servicios** para el que desea que el registro tooenable.

    ![Configurar el registro de hello portal de Azure.](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. Haga clic en **Guardar**.

registros de diagnóstico de Hola se guardan en un contenedor de blobs denominado $logs en su cuenta de almacenamiento. Puede ver los datos de registro de hello mediante un explorador de almacenamiento como hello [Explorador de almacenamiento de Microsoft](http://storageexplorer.com), o mediante programación con la biblioteca de cliente de almacenamiento de Hola o PowerShell.

Para obtener información sobre cómo acceder al contenedor de hello $logs, consulte [habilitar el registro de almacenamiento y acceso a datos de registro](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).

## <a name="next-steps"></a>Pasos siguientes

* Consiga más información acerca de [métricas, registro y facturación](storage-analytics.md) para el análisis de almacenamiento.
* [Habilitar métricas de Azure Storage y visualizar datos de métricas](storage-enable-and-view-metrics.md) mediante PowerShell y mediante programación con C#.
