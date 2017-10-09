---
title: recomendaciones de rendimiento aaaApply - base de datos de SQL de Azure | Documentos de Microsoft
description: "Puede utilizar las recomendaciones de rendimiento de Azure toofind portal Hola que pueden optimizar el rendimiento de la base de datos de SQL Azure o toocorrect algún problema identificado en la carga de trabajo."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a>Búsqueda y aplicación de recomendaciones de rendimiento

Puede utilizar las recomendaciones de rendimiento de Azure toofind portal Hola que pueden optimizar el rendimiento de la base de datos de SQL Azure o toocorrect algún problema identificado en la carga de trabajo. **Recomendación de rendimiento** página de portal de Azure le permite toofind hello las mejores recomendaciones en función de su impacto potencial. 

## <a name="viewing-recommendations"></a>Visualización de recomendaciones

tooview y aplicar recomendaciones de rendimiento, necesita Hola correcto [el control de acceso basado en roles](../active-directory/role-based-access-control-what-is.md) permisos en Azure. **Lector**, **colaborador de la base de datos de SQL** permisos son necesarios tooview recomendaciones, y **propietario**, **colaborador de la base de datos de SQL** se requieren permisos tooexecute ninguna acción; crear o quitar índices y cancelar la creación del índice.

Usar hello siguiendo las recomendaciones de rendimiento de toofind de pasos en el portal de Azure:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Vaya demasiado**más servicios** > **bases de datos SQL**y seleccione la base de datos.
3. Navegue demasiado**recomendación de rendimiento** tooview recomendaciones disponibles para la base de datos seleccionada de Hola.

Recomendaciones de rendimiento son shonw en hello tabla toohello similares que se muestra en hello figura siguiente:

![Recomendaciones](./media/sql-database-advisor-portal/recommendations.png)

Las recomendaciones se ordenan por su posible impacto en el rendimiento en hello siguientes categorías:

| Impacto | Descripción |
|:--- |:--- |
| Alto |Recomendaciones de alto impacto deben proporcionar el impacto de rendimiento más importante de Hola. |
| Mediano |Las recomendaciones de impacto moderado deben mejorar el rendimiento, pero no de manera significativa. |
| Bajo |Las recomendaciones de bajo impacto deben proporcionar un mejor rendimiento que el que se produciría sin ellas, pero es posible que las mejoras no sean significativas. |


> [!NOTE]
> La base de datos de SQL Azure debe toomonitor actividades al menos un día en orden tooidentify algunas recomendaciones. Hola base de datos de SQL Azure puede optimizar más fácilmente para patrones de consulta coherente que sea posible para ráfagas irregular aleatorios de actividad. Si las recomendaciones no están disponible corrently, Hola **recomendación de rendimiento** página proporciona un mensaje que explica por qué.
> 

También puede ver el estado de Hola de operaciones históricas de Hola. Seleccione una recomendación o estado toosee más detalles.

Este es un ejemplo de la recomendación "Crear el índice" Hola portal de Azure.

![Creación de índice](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a>Aplicación de las recomendaciones
La base de datos de SQL Azure proporciona control total sobre cómo se recomendaciones habilitado mediante cualquiera de hello tres opciones siguientes: 

* Aplicar recomendaciones individuales una a una.
* Habilitar hello tooautomatically optimización automática aplicar recomendaciones.
* tooimplement una recomendación manualmente, ejecute hello recomienda script de T-SQL en la base de datos.

Seleccione cualquier tooview recomendación sus detalles y, a continuación, haga clic en **Ver script** tooreview Hola detalles exactos de la creación de recomendación de Hola.

base de datos de Hello permanece en línea mientras se aplica la recomendación de hello: usar recomendación de rendimiento o el ajuste automático de nunca deja sin conexión una base de datos.

### <a name="apply-an-individual-recommendation"></a>Aplicar una recomendación individual
Puede revisar y aceptar recomendaciones una a una.

1. En hello **recomendaciones** hoja, seleccione una recomendación.
2. En hello **detalles** hoja haga clic en **aplicar** botón.
   
    ![Aplicar recomendaciones](./media/sql-database-advisor-portal/apply.png)

Recomendación seleccionado se aplicará en la base de datos de Hola.

### <a name="removing-recommendations-from-hello-list"></a>Quitar las recomendaciones de la lista de Hola
Si la lista de recomendaciones contiene elementos que desee tooremove de lista de hello, puede descartar la recomendación de hello:

1. Seleccione una recomendación en la lista de Hola de **recomendaciones** detalles de hello tooopen.
2. Haga clic en **descartar** en hello **detalles** hoja.

Si lo desea, puede agregar elementos descartados de atrás toohello **recomendaciones** lista:

1. En hello **recomendaciones** hoja haga clic en **vista descartada**.
2. Seleccione un elemento descartado de hello lista tooview sus detalles.
3. Si lo desea, haga clic en **deshacer descartar** tooadd Hola índice toohello atrás lista principal de **recomendaciones**.


### <a name="enable-automatic-tuning"></a>Habilitación del ajuste automático
Puede establecer las recomendaciones de tooimplement de base de datos de SQL Azure Hola automáticamente. A medida que las recomendaciones estén disponibles, estas se aplicarán de manera automática. Como con todas las recomendaciones administradas por hello servicio si impacto en el rendimiento hello es la recomendación de hello negativo se revertirán.

1. En hello **recomendaciones** hoja, haga clic en **automatizar**:
   
    ![Configuración del asesor](./media/sql-database-advisor-portal/settings.png)
2. Seleccione tooautomate de acciones:
   
    ![Índices recomendados](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a>Ejecutar manualmente Hola recomendada script T-SQL
Seleccione cualquier recomendación y haga clic en **Ver script**. Ejecute este script en la base de datos toomanually aplique la recomendación de Hola.

*Índices que se ejecutan manualmente no se supervisan y validados para el impacto de rendimiento servicio hello* por lo que se sugiere que supervisar estos índices después de la creación tooverify proporcionan mejoras de rendimiento y ajustar o eliminarlos si es necesario. Si desea conocer detalles sobre la creación de índices, consulte [CREAR ÍNDICE (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).

### <a name="canceling-recommendations"></a>Cancelación de recomendaciones
Las recomendaciones que se encuentran en estado **Pending**, **Verifying** o **Success** pueden cancelarse. Las recomendaciones con estado **Executing** no se pueden cancelar.

1. Seleccione una recomendación en hello **historial para la optimización** Hola de área tooopen **detalles recomendaciones** hoja.
2. Haga clic en **cancelar** tooabort proceso de Hola de aplicando la recomendación de Hola.

## <a name="monitoring-operations"></a>Supervisión de operaciones
Puede que una recomendación no se aplique de manera inmediata. portal de Hello proporciona detalles sobre el estado de saludo de la recomendación. siguiente Hola es Estados posibles que puede ser un índice en:

| Estado | Descripción |
|:--- |:--- |
| Pending |El comando de aplicación de recomendaciones se ha recibido y su ejecución está programada. |
| Executing |se está aplicando la recomendación de Hola. |
| Comprobando |Recomendación se aplicó correctamente y servicio Hola está midiendo las ventajas de Hola. |
| Correcto |La recomendación se aplicó correctamente y se han medido ventajas. |
| Error |Se produjo un error durante el proceso de Hola de aplicando la recomendación de Hola. Esto puede ser un problema transitorio, o posiblemente una tabla de toohello de cambios de esquema y script de Hola ya no es válido. |
| En reversión |recomendación de Hola se aplicó, pero consideró no eficiente y se está revirtiendo automáticamente. |
| Reverted |recomendación de Hola se revirtió. |

Haga clic en una recomendación en proceso de hello lista toosee más detalles:

![Índices recomendados](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a>Reversión de una recomendación
Si ha usado la recomendación de hello rendimiento recomendaciones tooapply Hola (es decir, que no ejecutó el script de Hola T-SQL manualmente) revertirá automáticamente se si encuentra toobe de impacto de rendimiento de hello negativo. Si por alguna razón, sencillamente, toorevert una recomendación para ello siguiente hello:

1. Seleccione una recomendación aplicada en hello **para la optimización historial** área.
2. Haga clic en **Revert** en hello **detalles de recomendación** hoja.

![Índices recomendados](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a>Supervisión del impacto en el rendimiento de las recomendaciones de índices
Después de que se han implementado correctamente recomendaciones (actualmente, las operaciones de índice y solo las recomendaciones de las consultas se parametrizan) puede hacer clic en **consulta visión** en hello recomendación detalles hoja tooopen [consulta Información del rendimiento](sql-database-query-performance.md) y ver el impacto en el rendimiento de las consultas principales Hola.

![Supervisar el impacto en el rendimiento](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a>Resumen
Azure SQL Database ofrece recomendaciones para mejorar el rendimiento de la base de datos SQL. Al proporcionar scripts T-SQL, así como opciones de ejecución individual y completamente automática, consigue ayuda útil para optimizar la base de datos y, en última instancia, para mejorar el rendimiento de las consultas.

## <a name="next-steps"></a>Pasos siguientes
Supervisar sus recomendaciones y continuar tooapply les toorefine rendimiento. Las cargas de trabajo de bases de datos son dinámicas y cambian con frecuencia. La base de datos de SQL Azure continuará toomonitor y se proporcionan recomendaciones que pueden mejorar el rendimiento de la base de datos. 

* Vea [el ajuste automático](sql-database-automatic-tuning.md) Hola de toolearn más información sobre el ajuste automático de la base de datos de SQL Azure.
* Consulte [Recomendaciones de rendimiento](sql-database-advisor.md) para ver información general sobre las recomendaciones de rendimiento de Azure SQL Database.
* Vea [información de rendimiento de consultas](sql-database-query-performance.md) toolearn acerca de cómo ver el impacto en el rendimiento de las consultas principales Hola.

## <a name="additional-resources"></a>Recursos adicionales
* [Almacén de consultas](https://msdn.microsoft.com/library/dn817826.aspx)
* [CREATE INDEX](https://msdn.microsoft.com/library/ms188783.aspx)
* [Control de acceso basado en rol](../active-directory/role-based-access-control-what-is.md)

