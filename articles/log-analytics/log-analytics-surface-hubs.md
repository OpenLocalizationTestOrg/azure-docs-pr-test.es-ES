---
title: "aaaMonitor Surface hub con análisis de registros de Azure | Documentos de Microsoft"
description: "Utilice Hola Surface Hub solución tootrack Hola estado de sus centros de superficie y entender cómo se están utilizando."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 623d30e749cafdd4a34ba0c5b3408164f1b4a95b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-tootrack-their-health"></a>Supervisar Surface hub con análisis de registros tootrack su estado de mantenimiento

![Símbolo de Surface Hub](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

Este artículo describe cómo puede utilizar Hola solución Surface Hub en dispositivos de Microsoft Surface Hub toomonitor de análisis de registros con hello Microsoft Operations Management Suite (OMS). Inicie sesión ayuda a análisis que realiza el seguimiento de estado de Hola de sus centros de superficie, así como comprender cómo se están utilizando.

Cada Surface Hub tiene Hola instalado Microsoft Monitoring Agent. Su mediante el agente de Hola que puede enviar datos desde su tooOMS Surface Hub. Archivos de registro se leen desde su Surface hub y, a continuación, se envían toohello servicio OMS. Problemas como servidores está sin conexión, Hola calendario no está sincronizando, o si cuenta Hola del dispositivo no se puede toolog en Skype se muestran en OMS en panel de hello Surface Hub. Si usa datos de hello en el panel de hello, puede identificar los dispositivos que no se ejecuta, o que están afectando otros problemas y, potencialmente aplicar correcciones para problemas de hello detectado.

## <a name="installing-and-configuring-hello-solution"></a>Instalar y configurar soluciones de Hola
Usar hello después tooinstall de información y configurar soluciones de Hola. En orden toomanage sus centros de superficie de hello Microsoft Operations Management Suite (OMS), necesitará Hola siguientes:

* Una suscripción válida demasiado[OMS](http://www.microsoft.com/oms).
* Un [suscripción de OMS](https://azure.microsoft.com/pricing/details/log-analytics/) nivel que admite Hola número de dispositivos que desee toomonitor. Los precios de OMS varían en función de cuántos dispositivos inscritos haya y de la cantidad de datos que se procesen. Debe tener tootake esto en cuenta al planear la implementación de Surface Hub.

A continuación, se agrega una suscripción de Microsoft Azure existente de OMS suscripción tooyour o crear una nueva área de trabajo directamente a través del portal de OMS Hola. Las instrucciones detalladas para usar cualquiera de estos métodos se encuentran en el artículo de [introducción a Log Analytics](log-analytics-get-started.md). Una vez configurada la suscripción de OMS Hola, hay dos tooenroll maneras los dispositivos Surface Hub:

* Automáticamente mediante Intune
* Manualmente a través de la aplicación **Configuración** del dispositivo Surface Hub.

## <a name="set-up-monitoring"></a>Configuración de la supervisión
Puede supervisar el estado de Hola y la actividad de su centro de superficie con análisis de registros de OMS. Puede inscribir Hola Surface Hub de OMS mediante Intune o localmente mediante **configuración** en hello Surface Hub.

## <a name="connect-surface-hubs-toooms-through-intune"></a>Conectar Surface hub tooOMS a través de Intune
Se le necesita Hola Id. de área de trabajo y clave de área de trabajo para el área de trabajo OMS de Hola que va a administrar sus centros de superficie. Puede obtenerlos Hola portal de OMS.

Intune es un producto de Microsoft que le permite toocentrally administrar opciones de configuración de OMS de hello tooone aplicado o varios de los dispositivos. Siga estos pasos tooconfigure los dispositivos a través de Intune:

1. Inicie sesión en tooIntune.
2. Navegue demasiado**configuración** > **orígenes conectados**.
3. Cree o edite una directiva basada en plantilla de hello Surface Hub.
4. Navegue toohello sección OMS (visión operativa de Azure) de directiva de Hola y agregar hello *Id. de área de trabajo* y *clave de área de trabajo* toohello directiva.
5. Guardar directiva Hola.
6. Asociar directiva Hola grupo adecuado de Hola de dispositivos.

   ![Directiva de Intune](./media/log-analytics-surface-hubs/intune.png)

Intune sincroniza, a continuación, configuración de OMS Hola con dispositivos de hello en grupo de destino de hello, inscribe en el área de trabajo OMS.

## <a name="connect-surface-hubs-toooms-using-hello-settings-app"></a>Conectar tooOMS Surface hub mediante la aplicación de configuración de hello
Se le necesita Hola Id. de área de trabajo y clave de área de trabajo para el área de trabajo OMS de Hola que va a administrar sus centros de superficie. Puede obtenerlos Hola portal de OMS.

Si no usa Intune toomanage su entorno, puede inscribir dispositivos manualmente en **configuración** en cada Surface Hub:

1. En Surface Hub, abra **Configuración**.
2. Escriba las credenciales de administrador de dispositivos hello cuando se le solicite.
3. Haga clic en **este dispositivo**y Hola en **supervisión**, haga clic en **configurar opciones de OMS**.
4. Seleccione **Habilitar supervisión**.
5. En el cuadro de diálogo de configuración de OMS hello, escriba Hola **Id. de área de trabajo** tipo hello y **clave de área de trabajo**.  
   ![settings](./media/log-analytics-surface-hubs/settings.png)
6. Haga clic en **Aceptar** configuración de toocomplete Hola.

Aparecerá una confirmación que indica si Hola la configuración de OMS se generó correctamente aplicado toohello dispositivo. Si es así, aparecerá un mensaje indicando que el agente Hola conectado correctamente toohello servicio OMS. dispositivo de Hello, a continuación, comienza a enviar datos tooOMS donde puede ver y actuar en él.

## <a name="monitor-surface-hubs"></a>Supervisión de dispositivos Surface Hub
La supervisión de los dispositivos Surface Hubs con OMS es muy similar a la de todos los demás dispositivos inscritos.

1. Inicie sesión en toohello portal de OMS.
2. Vaya a Panel de paquete de solución de toohello Surface Hub.
3. Se muestra el estado del dispositivo.

   ![Panel de Surface Hub](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

Puede crear [alertas](log-analytics-alerts.md) en función de las búsquedas de registros existentes o personalizadas. Con Hola Hola de datos que OMS recopila de los concentradores de superficie, puede buscar problemas y alerta sobre condiciones de Hola que defina para los dispositivos.

## <a name="next-steps"></a>Pasos siguientes
* Use [búsquedas de registro de análisis de registros](log-analytics-log-searches.md) tooview detallada datos Surface Hub.
* Crear [alertas](log-analytics-alerts.md) toonotify cuando se producen problemas con los concentradores de superficie.
