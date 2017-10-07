---
title: alertas de base de datos SQL de Azure toocreate portal aaaUse | Documentos de Microsoft
description: "Usar alertas de base de datos SQL de Azure toocreate portal hello, que pueden desencadenar notificaciones o la automatización cuando se cumplen las condiciones de Hola que especifique."
author: aamalvea
manager: jhubbard
editor: 
services: sql-database
documentationcenter: 
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: sql-database
ms.custom: monitor and tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: aamalvea
ms.openlocfilehash: 4e494b130a26c4cdf42445cb49648fce9bf4d300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toocreate-alerts-for-azure-sql-database-and-data-warehouse"></a>Usar alertas de toocreate de portal de Azure para la base de datos de SQL Azure y almacenamiento de datos

## <a name="overview"></a>Información general
Este artículo muestra cómo tooset las alertas de base de datos de SQL Azure y almacenamiento de datos mediante Hola portal de Azure. En este artículo también se indican procedimientos recomendados para establecer periodos de alerta.    

Puede recibir una alerta basada en las métricas de supervisión para los servicios de Azure o los eventos sobre ellos.

* **Valores de métrica** : hello desencadenadores de alerta cuando el valor Hola de una métrica especificada está fuera de un umbral asignar en cualquier dirección. Es decir, desencadena tanto cuando primero se cumple la condición de hello y, a continuación, después cuando la condición que ya no se cumple.    
* **Eventos de registro de actividades** : una alerta puede desencadenarse en *cada* evento o solo cuando se produce una serie de eventos.

Puede configurar una alerta toodo hello las siguientes cuando se desencadena:

* enviar el administrador del servicio de toohello de notificaciones de correo electrónico y coadministradores
* enviar correo electrónico mensajes de correo electrónico de tooadditional que especifique.
* Llamar a un webhook.

Puede obtener información sobre las reglas de alerta y configurarlas mediante:

* [Portal de Azure](../monitoring-and-diagnostics/insights-alerts-portal.md)
* [PowerShell](../monitoring-and-diagnostics/insights-alerts-powershell.md)
* [Interfaz de la línea de comandos (CLI)](../monitoring-and-diagnostics/insights-alerts-command-line-interface.md)
* [API de REST de Azure Monitor](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>Crear una regla de alerta en una métrica con hello portal de Azure
1. Hola [portal](https://portal.azure.com/), busque está interesado en la supervisión de recursos de Hola y selecciónelo.
2. Este paso es diferente para SQL Database y los grupos elásticos frente a SQL Data Warehouse: 

   - **Base de datos SQL y solo grupos elástico**: seleccione **alertas** o **reglas de alerta** en la sección supervisión de Hola. icono y texto hello pueden variar ligeramente para los distintos recursos.  
   
     ![Supervisión](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButton.png)
  
   - **Almacenamiento de datos de SQL sólo**: seleccione **supervisión** en hello sección tareas comunes. Haga clic en hello **DWU uso** gráfico.

     ![TAREAS COMUNES](../monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButtonDW.png)

3. Seleccione hello **Agregar alerta** comando y rellene los campos de Hola.
   
    ![Agregar alerta](../monitoring-and-diagnostics/media/insights-alerts-portal/AddDBAlertPage.png)
4. Asígnele un **nombre** a la regla de alerta y elija una **descripción**, que también se muestra los correos electrónicos de notificación.
5. Seleccione hello **métrica** desea toomonitor y después elija una **condición** y **umbral** valor de métrica de Hola. También elegido hello **período** de tiempo que Hola métrica regla debe cumplirse antes de desencadenadores de alerta de Hola. Por ejemplo, si usa el período de Hola "PT5M" y busca de la alerta de CPU superior al 80%, alerta de hello desencadena cuando Hola CPU ha estado anterior de forma coherente el 80% durante 5 minutos. Una vez que se produce el primer desencadenador que hello, desencadena nuevo cuando Hola CPU permanezca por debajo de 80% durante 5 minutos. Hola medida de CPU se produce cada 1 minuto.   
6. Comprobar **propietarios de correo electrónico...**  si desea que los administradores y coadministradores toobe por correo electrónico cuando Hola alerta se activa.
7. Si desea que los mensajes de correo electrónico adicionales tooreceive una notificación cuando hello alerta se desencadena, agregarlos en hello **email(s) Administrador adicional** campo. Separe las direcciones de correo electrónico con punto y coma, de la siguiente manera: *email@contoso.com;email2@contoso.com*
8. Colocar en un URI válido en hello **Webhook** campo si desea que se llama cuando Hola alerta se activa.
9. Seleccione **Aceptar** cuando toocreate done Hola alerta.   

Dentro de unos minutos, alerta de hello está activo y se desencadena como se describió anteriormente.

## <a name="managing-your-alerts"></a>Administración de las alertas
Una vez que haya creado una alerta, puede seleccionarla y:

* Ver un gráfico que muestra umbral de métrica de Hola y los valores reales de Hola Hola día anterior.
* Editar la alerta o eliminarla.
* **Deshabilitar** o **habilitar** si desea tootemporarily detener o reanudar la recepción de notificaciones de esa alerta.


## <a name="sql-database-alert-values"></a>Valores de las alertas de SQL Database

| Tipo de recurso | Nombre de métrica | Nombre descriptivo | Tipo de agregación | Ventana de tiempo mínimo de la alerta|
| --- | --- | --- | --- | --- |
| Base de datos SQL | cpu_percent | Porcentaje de CPU | Media | 5 minutos |
| Base de datos SQL | physical_data_read_percent | Porcentaje de E/S de datos | Media | 5 minutos |
| Base de datos SQL | log_write_percent | Porcentaje de E/S de registro | Media | 5 minutos |
| Base de datos SQL | dtu_consumption_percent | Porcentaje de DTU | Media | 5 minutos |
| Base de datos SQL | storage | Tamaño total de base de datos | Máxima | 30 minutos |
| Base de datos SQL | connection_successful | Conexiones correctas | Total | 10 minutos |
| Base de datos SQL | connection_failed | Conexiones con errores | Total | 10 minutos |
| Base de datos SQL | blocked_by_firewall | Bloqueado por el firewall | Total | 10 minutos |
| Base de datos SQL | deadlock | Interbloqueos | Total | 10 minutos |
| Base de datos SQL | storage_percent | Porcentaje de tamaño de base de datos | Máxima | 30 minutos |
| Base de datos SQL | xtp_storage_percent | Porcentaje de almacenamiento de OLTP en memoria (versión preliminar) | Media | 5 minutos |
| Base de datos SQL | workers_percent | Porcentaje de trabajos | Media | 5 minutos |
| Base de datos SQL | sessions_percent | Porcentaje de sesiones | Media | 5 minutos |
| Base de datos SQL | dtu_limit | Límite de DTU | Media | 5 minutos |
| Base de datos SQL | dtu_used | DTU utilizada | Media | 5 minutos |
||||||
| Grupo elástico | cpu_percent | Porcentaje de CPU | Media | 10 minutos |
| Grupo elástico | physical_data_read_percent | Porcentaje de E/S de datos | Media | 10 minutos |
| Grupo elástico | log_write_percent | Porcentaje de E/S de registro | Media | 10 minutos |
| Grupo elástico | dtu_consumption_percent | Porcentaje de DTU | Media | 10 minutos |
| Grupo elástico | storage_percent | Porcentaje de almacenamiento | Media | 10 minutos |
| Grupo elástico | workers_percent | Porcentaje de trabajos | Media | 10 minutos |
| Grupo elástico | eDTU_limit | Límite de eDTU | Media | 10 minutos |
| Grupo elástico | storage_limit | Límite de almacenamiento | Media | 10 minutos |
| Grupo elástico | eDTU_used | eDTU utilizada | Media | 10 minutos |
| Grupo elástico | storage_used | Almacenamiento utilizado | Media | 10 minutos |
||||||               
| SQL Data Warehouse | cpu_percent | Porcentaje de CPU | Media | 10 minutos |
| SQL Data Warehouse | physical_data_read_percent | Porcentaje de E/S de datos | Media | 10 minutos |
| SQL Data Warehouse | storage | Tamaño total de base de datos | Máxima | 10 minutos |
| SQL Data Warehouse | connection_successful | Conexiones correctas | Total | 10 minutos |
| SQL Data Warehouse | connection_failed | Conexiones con errores | Total | 10 minutos |
| SQL Data Warehouse | blocked_by_firewall | Bloqueado por el firewall | Total | 10 minutos |
| SQL Data Warehouse | service_level_objective | Objetivo de nivel de servicio de base de datos de Hola | Total | 10 minutos |
| SQL Data Warehouse | dwu_limit | Límite de DWU | Máxima | 10 minutos |
| SQL Data Warehouse | dwu_consumption_percent | Porcentaje de DWU | Media | 10 minutos |
| SQL Data Warehouse | dwu_used | DWU utilizada | Media | 10 minutos |
||||||


## <a name="next-steps"></a>Pasos siguientes
* [Obtener una visión general de supervisión de Azure](../monitoring-and-diagnostics/monitoring-overview.md) incluidos Hola los tipos de información que puede recopilar y supervisar.
* Obtenga más información sobre cómo [configurar webhooks en las alertas](../monitoring-and-diagnostics/insights-webhooks-alerts.md).
* Obtenga [información general sobre los registros de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) para recopilar métricas detalladas de alta frecuencia sobre el servicio.
* Obtener un [información general de la colección de métricas](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake que el servicio esté disponible y capacidad de respuesta.
