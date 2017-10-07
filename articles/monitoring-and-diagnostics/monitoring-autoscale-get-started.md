---
title: "aaaGet iniciado con el escalado automático de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooscale el recurso de Azure."
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a>Introducción al escalado automático en Azure
Este artículo se describe cómo tooset la configuración de escalado automático para el recurso en el portal de Microsoft Azure Hola.

Escalado automático de Monitor de Azure se aplica solo toovirtual conjuntos de escalas de máquina, servicios en la nube, planes de servicio de aplicaciones de Azure y los entornos del servicio de aplicación. 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a>Detectar la configuración de escalado automático de hello en su suscripción
Puede detectar todos los recursos de hello para el que es aplicable en el Monitor de Azure de escalado automático. Usar hello siguiendo los pasos para ver un tutorial paso a paso:

1. Abra hello [portal de Azure.][1]
2. Haga clic en el icono de Monitor de Azure de hello en el panel izquierdo de Hola.
  ![Abrir Azure Monitor][2]
3. Haga clic en **escalado automático** tooview todos los recursos de hello para el escalado automático es aplicable, junto con su estado actual de escalado automático.
  ![Detectar el escalado automático en Azure Monitor][3]

Puede usar el panel de filtro de Hola en hello tooscope superior hacia abajo tooselect recursos de lista de hello en un grupo de recursos específico, determinados tipos de recursos o un recurso específico.

Para cada recurso, encontrará el recuento de instancias actual de Hola y el estado de escalado automático de Hola. Hola estado de escalado automático puede ser:

- **No configurado**: aún no se ha habilitado el escalado automático para este recurso.
- **Habilitado**: se ha habilitado el escalado automático para este recurso.
- **Deshabilitado**: se ha deshabilitado el escalado automático para este recurso.

## <a name="create-your-first-autoscale-setting"></a>Creación de la primera configuración de escalado automático

Supongamos ahora, vaya a través de un tutorial paso a paso simple toocreate la primera configuración de escalado automático.

1. Abra hello **escalado automático** hoja en el Monitor de Azure y seleccione un recurso que desea tooscale. (hello pasos siguientes utiliza un plan de servicio de aplicaciones asociado a una aplicación web. Puede [crear su primera aplicación web de ASP.NET en Azure en cinco minutos][4]).
2. Tenga en cuenta que el recuento de instancias actual de hello es 1. Haga clic en **Enable autoscale** (Habilitar escalado automático).
  ![Configuración de escalado para la nueva aplicación web][5]
3. Proporcione un nombre para la configuración de escala de hello y, a continuación, haga clic en **agregar una regla de**. Observe las opciones de regla de escala de Hola que abrir un panel de contexto en el lado derecho de Hola. De forma predeterminada, se establece la instancia de recuento en 1 si el porcentaje de CPU del recurso de Hola Hola supera el 70 por ciento de hello opción tooscale. Deje los valores predeterminados y haga clic en **Agregar**.
  ![Crear configuración de escalado para una aplicación web][6]
4. Ahora ha creado su primera regla de escalado. Tenga en cuenta que Hola UX recomienda mejores prácticas e indica que "se recomienda toohave al menos una escala en la regla." toodo para:
  
    a. Haga clic en **Agregar una regla**. 

    b. Establecer **operador** demasiado**menor que**.

    c. Establecer **umbral** demasiado**20**.

    d. Establecer **operación** demasiado**disminuir el número por**.

   Ahora debería tener una configuración de escalado que escale o reduzca horizontalmente en función del uso de CPU.
   ![Escala en función de la CPU][8]
5. Haga clic en **Guardar**.

¡Enhorabuena! Ahora que ha creado correctamente su primer tooautoscale de configuración de escala en función de la aplicación web de uso de CPU.

> [!NOTE] 
> Hello mismos pasos son aplicable tooget a trabajar con una escala de máquinas virtuales en la nube o conjunto de rol de servicio.

## <a name="other-considerations"></a>Otras consideraciones
### <a name="scale-based-on-a-schedule"></a>Escalación según una programación
Además tooscale en función de la CPU, puede establecer la escala de manera diferente para determinados días de la semana de Hola.

1. Haga clic en **Add a scale condition** (Agregar una condición de escalado).
2. Configurar reglas de hello y modo de escala de hello es igual Hola como condición de hello predeterminada.
3. Seleccione **repita días específicos** de programación de Hola.
4. Seleccione los días de Hola y tiempo de inicio y fin de Hola para cuándo se debe aplicar la condición de la escala de Hola.

![Condición de escalado basada en programación][9]
### <a name="scale-differently-on-specific-dates"></a>Escalado distinto en fechas concretas
Además tooscale en función de la CPU, puede establecer la escala de manera diferente para las fechas concretas.

1. Haga clic en **Add a scale condition** (Agregar una condición de escalado).
2. Configurar reglas de hello y modo de escala de hello es igual Hola como condición de hello predeterminada.
3. Seleccione **especificar fechas de inicio y fin** de programación de Hola.
4. Seleccione las fechas de inicio y fin de Hola y la hora de inicio y fin de Hola para cuándo se debe aplicar la condición de la escala de Hola.

![Condición de escalado basada en fechas][10]

### <a name="view-hello-scale-history-of-your-resource"></a>Ver el historial de la escala de hello del recurso
Cada vez que el recurso se escala hacia arriba o hacia abajo, se registra un evento en el registro de actividad de Hola. Puede ver historial de la escala de hello del recurso para hello las últimas 24 horas cambiando toohello **historial de ejecución** ficha.

![Historial de ejecuciones][11]

Si desea que el historial de escala completa hello tooview (para una copia de seguridad too90 días), seleccione **haga clic aquí toosee detalles más**. Abre el registro de actividad de Hello, con el escalado automático ya seleccionado para el recurso y la categoría.

### <a name="view-hello-scale-definition-of-your-resource"></a>Ver definición de la escala de hello del recurso
El escalado automático es un recurso de Azure Resource Manager. Puede ver la definición de la escala de hello en JSON cambiando toohello **JSON** ficha.

![Definición de escala][12]

Puede realizar cambios en JSON directamente, si es necesario. Estos cambios se reflejarán después de guardarlos.

### <a name="disable-autoscale-and-manually-scale-your-instances"></a>Deshabilitar el escalado automático y escalar manualmente las instancias
Puede haber ocasiones cuando desee toodisable la configuración de escala actual y escalar manualmente el recurso.

Haga clic en hello **deshabilitar escalado automático** situado en la parte superior de Hola.
![Deshabilitar escalado automático][13]

> [!NOTE] 
> Esta opción deshabilita su configuración. Sin embargo, puede volver tooit después de habilitar el escalado automático nuevo. 

Ahora puede establecer el número de Hola de instancias que desee tooscale toomanually.

![Definición manual de escalado][14]

Siempre puede volver tooAutoscale haciendo clic en **habilita el escalado automático** y, a continuación, **guardar**.

## <a name="next-steps"></a>Pasos siguientes
- [Crear una alerta de registro de actividad toomonitor todas las operaciones de motor de escalado automático en su suscripción](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [Crear una alerta de registro de actividad toomonitor error en todos los operaciones de escala-escalabilidad de escalado automático en su suscripción](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png

