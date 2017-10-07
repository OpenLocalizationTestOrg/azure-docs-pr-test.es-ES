---
title: "Azure Portal: Creación y administración de un grupo elástico de SQL Database | Microsoft Docs"
description: "Obtenga información acerca de cómo toouse Hola portal de Azure y toomanage de inteligencia incorporada de la base de datos de SQL, supervisar y ajustar un grupo elástico escalable toooptimize base de datos de rendimiento y costo de administrar."
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a>Crear y administrar un grupo elástico con hello portal de Azure
Este tema muestra cómo toocreate y administrar escalable [grupos elásticos](sql-database-elastic-pool.md) con hello portal de Azure. También puede crear y administrar un grupo elástico Azure con [PowerShell](sql-database-elastic-pool-manage-powershell.md), API de REST de Hola o [C#](sql-database-elastic-pool-manage-csharp.md). También puede crear y mover bases de datos dentro y fuera de los grupos elásticos mediante [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

## <a name="create-an-elastic-pool"></a>Creación de un grupo elástico 

Hay dos maneras de crear un grupo elástico. Puede hacerlo desde el principio si sabe Hola grupo el programa de instalación que desee, o inicia con una recomendación de servicio de Hola. Base de datos de SQL tiene inteligencia incorporada que recomienda el programa de instalación de un grupo elástico si es más rentable en función de hello más allá de telemetría de uso para las bases de datos.

Puede crear varios grupos en un servidor, pero no se puede agregar las bases de datos de distintos servidores en hello mismo grupo. 

> [!NOTE]
> Los grupos elásticos están disponibles con carácter general (GA) en todas las regiones de Azure excepto oeste de la India, donde actualmente se encuentran en versión preliminar.  La disponibilidad general de grupos elásticos en esta región se producirá tan pronto como sea posible.
>

### <a name="step-1-create-an-elastic-pool"></a>Paso 1: Crear un grupo elástico

Crear un grupo elástico de existente **server** hoja en el portal de hello es hello más fáciles manera toomove bases de datos existentes en un grupo elástico.

> [!NOTE]
> También puede crear un grupo elástico mediante una búsqueda **grupo elástico de SQL** en hello **Marketplace** o haga clic en **+ agregar** en hello **grupos elásticos SQL**examinar hoja. Es capaz de toospecify un servidor nuevo o existente a través de este flujo de trabajo de aprovisionamiento del bloque.
>
>

1. Hola [portal de Azure](http://portal.azure.com/), haga clic en **más servicios**  **>**  **servidores SQL Server**y, a continuación, haga clic en servidor de Hola que contiene Hola bases de datos desea que el grupo elástico de tooadd tooan.
2. Haga clic en **Grupo nuevo**.

    ![Agregar grupo tooa servidor](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    **O**

    Es posible que vea un mensaje que indica que no existe se recomiendan grupos elásticos para servidor hello. Haga clic en hello toosee Hola mensaje que recomienda pools basándose en la telemetría de uso de la base de datos históricos y, a continuación, haga clic en toosee de nivel de hello más detalles y personalizar el grupo de Hola. Vea [comprender las recomendaciones de grupos](#understand-elastic-pool-recommendations) más adelante en este tema para cómo Hola actuación.

    ![grupo recomendado](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. Hola **grupo elástico** aparece hoja, que es donde se especifican los valores de hello para el grupo. Si hace clic en **nuevo grupo** en el paso anterior de hello, hello tarifa es **estándar** está seleccionada de forma predeterminada y ninguna base de datos. Puede crear un grupo vacío o especificar un conjunto de bases de datos de ese toomove de servidor en el grupo de Hola. Si va a crear un grupo recomendado, Hola recomienda tarifa, configuración de rendimiento y se completan automáticamente la lista de bases de datos, pero todavía se pueden cambiar.

    ![Configuración de grupos elásticos](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. Especifique un nombre para el grupo elástico hello, o déjela como valor predeterminado de Hola.

### <a name="step-2-choose-a-pricing-tier"></a>Paso 2: Elegir un plan de tarifa

Hello tarifa del grupo determina Hola características elastics toohello disponibles en el grupo de Hola y Hola número máximo de Edtu (eDTU máx.) y la base de datos de almacenamiento (GB) tooeach disponibles. Para más detalles, consulte Niveles de servicio.

nivel de precios toochange hello para el grupo de hello, haga clic en **tarifa**, haga clic en hello tarifa que desee y, a continuación, haga clic en **seleccione**.

> [!IMPORTANT]
> Después de elegir el nivel de precios de Hola y confirmar los cambios, haga clic en **Aceptar** en último paso hello, no será hello toochange capaz de tarifa del grupo de Hola. toochange Hola a nivel de precios para un grupo elástico existente, crear un grupo elástico en el nivel de precios deseada de Hola y migrar toothis nuevo grupo de bases de datos de Hola.
>

![Seleccione un nivel de precios.](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a>Paso 3: Configurar grupo de Hola

Después de establecer el nivel de precios de hello, haga clic en Configurar grupo que agregar las bases de datos, Edtu de grupo de conjunto y almacenamiento (GB de grupo), y donde establecer hello Edtu min y max para elastics hello en grupo de Hola.

1. Haga clic en **Configurar grupo**
2. Seleccione las bases de datos de hello desea tooadd toohello grupo. Este paso es opcional al crear el grupo de Hola. Las bases de datos pueden agregarse una vez creado el grupo de Hola.
    Haga clic en bases de datos de tooadd, **Agregar base de datos**, haga clic en las bases de datos de Hola que desee tooadd y, a continuación, haga clic en hello **seleccione** botón.

    ![Agregar bases de datos](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    Si las bases de datos de Hola que trabaja tienen suficiente telemetría históricas de uso, Hola **estimado de eDTU y GB uso** hello y gráfico **uso de eDTU real** toohelp de actualización de gráfico de barras realizar configuración decisiones. Además, servicio de hello puede proporcionarle un toohelp de mensaje de recomendación, ajustar Hola grupo. Consulte [Recomendaciones dinámicas](#understand-elastic-pool-recommendations).

3. Usar controles de hello en hello **Configurar grupo** tooexplore configuración de página y configurar el grupo de servidores. Consulte los [límites de los grupos elásticos](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) para ver más información sobre los límites de cada nivel de servicio y las [consideraciones sobre precios y rendimiento para los grupos elásticos](sql-database-elastic-pool.md) para ver instrucciones detalladas sobre el ajuste de tamaño correcto de un grupo elástico. Para más información sobre la configuración del grupo, consulte las [propiedades del grupo elástico](sql-database-elastic-pool.md#database-properties-for-pooled-databases).

    ![Configuración de grupos elásticos](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. Haga clic en **seleccione** en hello **Configurar grupo** hoja después de cambiar la configuración.
5. Haga clic en **Aceptar** grupo de hello toocreate.

## <a name="understand-elastic-pool-recommendations"></a>Descripción de las recomendaciones de grupos elásticos

Hola servicio de base de datos SQL se evalúa como el historial de uso y recomienda uno o más grupos cuando resulta más rentable que las bases de datos único. Cada recomendación se configura con un subconjunto de las bases de datos del servidor de Hola que mejor se ajustan grupo Hola único.

![grupo recomendado](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

recomendación de grupo de Hello consta de:

- Un nivel de precios para el grupo de hello (Basic, Standard, Premium o Premium RS)
- Las **eDTU del grupo** adecuadas (también denominadas eDTU máx. por grupo)
- Hola **eDTU máxima** y **eDTU mín.** por base de datos
- lista de Hola de bases de datos recomendados para el grupo de Hola

> [!IMPORTANT]
> servicio de Hello tiene últimos 30 días de telemetría de hello en cuenta al recomendar grupos. Para toobe de base de datos que se consideran como candidata para un grupo elástico, debe existir para al menos 7 días. Las bases de datos que ya están en un grupo elástico no se consideran candidatas para las recomendaciones de grupos elásticos.
>

servicio de Hello evalúa las necesidades de recursos y rentabilidad de hello móvil único bases de datos en cada nivel de servicio en grupos de hello mismo nivel. Por ejemplo, se evalúan todas las bases de datos Standard en un servidor para que quepan en un bloque de bases de datos elásticas Standard. Esto significa servicio hello no hace recomendaciones de nivel entre como mover una base de datos estándar en un grupo de Premium.

Después de agregar el grupo de servidores de bases de datos toohello, las recomendaciones se generan dinámicamente según el uso históricos Hola de bases de datos de Hola que seleccionó. Estas recomendaciones se muestran en hello eDTU y GB gráfico de uso y de un encabezado de recomendación en parte superior de Hola de hello **Configurar grupo** hoja. Estas recomendaciones son tooassist previsto en la creación de un grupo elástico optimizado para las bases de datos específicos.

![Recomendaciones dinámicas](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a>Administración y supervisión de un grupo elástico

Puede usar hello toomonitor de portal de Azure y administrar bases de datos de hello en el grupo de Hola y un grupo elástico. Desde el portal de hello, puede supervisar el uso de Hola de un grupo elástico y bases de datos de hello dentro de ese grupo. También puede realizar un conjunto de cambios grupo elástico tooyour y enviar todos los cambios realizados en hello mismo tiempo. Estos cambios incluyen agregar o quitar bases de datos, cambiar la configuración del grupo elástico o cambiar la configuración de la base de datos.

Hola siguiente gráfico muestra un grupo elástico de ejemplo. vista de Hello incluye:

*  Gráficos para supervisar el uso de recursos de grupo elástico de Hola y bases de datos de hello contenidas en el grupo de Hola.
*  Hola **configurar** grupo botón toomake cambia toohello de grupo elástico.
*  Hola **crear base de datos** botón que crea una base de datos y lo agrega el grupo elástico de toohello actual.
*  Los trabajos elásticos que le ayudarán a administran un gran número de bases de datos mediante la ejecución de scripts de Transact SQL en todas las bases de datos de una lista.

![Vista Grupo][2]

Puede ir tooa determinado grupo toosee su utilización de recursos. De forma predeterminada, el grupo de hello es uso de eDTU y almacenamiento de tooshow configurado para hello última hora. gráfico de Hello puede ser tooshow configurado diferentes métricas sobre varias ventanas de tiempo.

1. Seleccione un toowork grupo elástico con.
2. En **Supervisión de grupo elástico** hay un gráfico con la etiqueta **Uso de recursos**. Haga clic en el gráfico de Hola.

    ![Supervisión de grupo elástico][3]

    Hola **métrica** abre la hoja, que muestra una vista detallada de Hola especificados métricas en el período de tiempo especificado de Hola.   

    ![Cuadro de métricas][9]

### <a name="toocustomize-hello-chart-display"></a>presentación de gráfico de hello toocustomize

Puede editar gráfico de Hola y Hola hoja métrica toodisplay otras métricas como porcentaje de CPU, porcentaje de E/S de datos y porcentaje de E/S de registro utilizado.

1. En la hoja de métricas de hello, haga clic en **editar**.

    ![Haga clic en Editar.][6]

2. Hola **Editar gráfico** hoja, seleccione un intervalo de tiempo (más allá de la hora, en la actualidad, o más allá de la semana), o haga clic en **personalizado** tooselect cualquier intervalo de fechas en hello dos últimas semanas. Seleccionar tipo de gráfico de hello (barra o línea), a continuación, seleccione Hola recursos toomonitor.

   > [!Note]
   > Solo el gráfico de métricas con hello misma unidad de medida se pueden mostrar en hello en hello mismo tiempo. Por ejemplo, si selecciona "porcentaje de eDTU" solo puede seleccionar otras métricas de porcentaje como unidad de medida de Hola.
   >

    ![Haga clic en Editar.](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. y, a continuación, haga clic en **Aceptar**.

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>Administración y supervisión de bases de datos en un grupo elástico

También se pueden supervisar bases de datos individuales en caso de un problema potencial.

1. En **Supervisión de base de datos elástica**hay un gráfico que muestra las métricas para cinco bases de datos. De forma predeterminada, Hola gráfico muestra hello principales 5 bases de datos en bloque de hello mediante el uso de eDTU promedio en hello última hora. Haga clic en el gráfico de Hola.

    ![Supervisión de grupo elástico][4]

2. Hola **utilización de recursos de base de datos** aparece hoja. Esto proporciona una vista detallada de uso de la base de datos de hello en bloque de Hola. Con la cuadrícula de hello en parte inferior de Hola de hoja de hello, puede seleccionar las bases de datos en hello grupo toodisplay su uso en el gráfico de hello (seguridad de bases de datos de too5). También puede personalizar la ventana de métricas y la hora de hello muestra en el gráfico de hello haciendo clic en **Editar gráfico**.

    ![Hoja de utilización de recursos de base de datos][8]

### <a name="toocustomize-hello-view"></a>vista de hello toocustomize

1. Hola **utilización de recursos de la base de datos** hoja, haga clic en **Editar gráfico**.

    ![Clic en Editar gráfico](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. Hola **editar** hoja de gráfico, seleccione un intervalo de tiempo (más allá de hora o más allá de 24 horas) o haga clic en **personalizado** tooselect día diferente en hello más allá de toodisplay de 2 semanas.

    ![Clic en Personalizado](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. Haga clic en hello **comparar las bases de datos** tooselect un toouse métrica diferentes al comparar las bases de datos de lista desplegable.

    ![Editar gráfico de Hola](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>tooselect toomonitor de bases de datos

En la lista de bases de datos de Hola Hola **utilización de recursos de base de datos** hoja, puede encontrar las bases de datos determinadas consultando a través de páginas de hello en lista de Hola o escribiendo en nombre de Hola de una base de datos. Base de datos de uso Hola casilla tooselect Hola.

![Busque toomonitor de bases de datos][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a>Agregar un recurso de grupo elástico tooan alerta

Puede agregar el grupo elástico de reglas tooan que envíe correo electrónico de alerta o toopeople cadenas tooURL los puntos de conexión al grupo elástico Hola alcanza un umbral de uso que configuró.

**tooadd un recurso de tooany alerta:**

1. Haga clic en hello **utilización de recursos** Hola de gráfico tooopen **métrica** hoja, haga clic en **Agregar alerta**y, a continuación, rellene la información de Hola Hola **agregar una alerta regla** hoja (**recursos** se configura automáticamente de grupo de hello toobe trabaja con).
2. Escriba un **nombre** y **descripción** que identifica tooyou alerta hello y destinatarios de Hola.
3. Elija un **métrica** que desea tooalert de lista de Hola.

    gráfico de Hello dinámicamente muestra la utilización de recursos para esa métrica toohelp que elija un umbral.

4. Elija una **condición** (mayor que, menor que, etc.) y un **umbral**.
5. Elija un **período** de tiempo que Hola métrica regla debe cumplirse antes de desencadenadores de alerta de Hola.
6. Haga clic en **Aceptar**.

Para más información, consulte cómo [crear alertas de SQL Database en Azure Portal](sql-database-insights-alerts-portal.md).

## <a name="move-a-database-into-an-elastic-pool"></a>Movimiento de una base de datos a un grupo elástico

Puede agregar o quitar las bases de datos de un grupo existente. las bases de datos de Hello pueden estar en otros grupos. Sin embargo, solo puede agregar bases de datos que están en Hola mismo servidor lógico.

1. En la hoja de hello para el grupo de hello, en **bases de datos elásticas** haga clic en **Configurar grupo**.

    ![Haga clic en Configurar grupo.][1]

2. Hola **Configurar grupo** hoja, haga clic en **agregar toopool**.

    ![Haga clic en Agregar toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. Hola **agregar bases de datos** hoja, base de datos de hello select o el grupo de servidores de bases de datos tooadd toohello. Después, haga clic en **Seleccionar**.

    ![Seleccione las bases de datos tooadd](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    Hola **Configurar grupo** hoja ahora listas Hola base de datos seleccionada toobe agregado, con su estado establecido demasiado**pendiente**.

    ![Adiciones de grupo pendientes.](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. Hola **hoja de grupo configurar**, haga clic en **guardar**.

    ![Haga clic en Guardar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a>Movimiento de una base de datos fuera de un grupo elástico

1. Hola **Configurar grupo** hoja, base de datos seleccione Hola o tooremove de las bases de datos.

    ![lista de bases de datos](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. Haga clic en **Quitar del grupo**.

    ![lista de bases de datos](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    Hola **Configurar grupo** hoja ahora listas Hola base de datos seleccionada toobe quitado junto con su estado establecido demasiado**pendiente**.

    ![Adición de base de datos de vista previa y eliminación](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. Hola **hoja de grupo configurar**, haga clic en **guardar**.

    ![Haga clic en Guardar](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a>Cambio de la configuración de rendimiento de un grupo elástico

Al supervisar la utilización de recursos de Hola de un grupo elástico, es posible que descubra que no se necesitan algunos ajustes. Quizá grupo Hola necesita un cambio en los límites de rendimiento o almacenamiento de Hola. Posiblemente desee toochange configuración de base de datos de hello en el grupo de Hola. Puede cambiar el programa de instalación de Hola de grupo de Hola en cualquier momento tooget Hola mejor equilibrio entre rendimiento y costo. Consulte [¿Cuándo se debe utilizar un grupo elástico?](sql-database-elastic-pool.md) para más información.

toochange hello Edtu o almacenamiento limita por grupo y Edtu por base de datos:

1. Abra hello **Configurar grupo** hoja.

    En **configuración de grupo elástico**, use cualquier configuración del grupo de control deslizante toochange Hola.

    ![Uso de recursos de grupos elásticos](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. Cuando se cambia la configuración de hello, hello muestra hello mensual costo estimado de cambios de Hola.

    ![Actualización de un grupo elástico y nuevo coste mensual](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a>Latencia de las operaciones de grupos elásticos
* Cambiar normalmente Hola min Edtu por base de datos o el número máximo de Edtu por base de datos completa en 5 minutos o menos.
* Cambiar hello Edtu por grupo de depende de la cantidad total de Hola de espacio utilizado por todas las bases de datos de grupo de Hola. Los cambios tienen un duración media de 90 minutos o menos por cada 100 GB. Por ejemplo, si utiliza el espacio total de Hola por todas las bases de datos de grupo de hello es de 200 GB, Hola espera latencia para cambiar hello eDTU del grupo por grupo es de 3 horas o menos.

## <a name="next-steps"></a>Pasos siguientes

- toounderstand qué un grupo elástico, consulte [grupo elástico de base de datos SQL](sql-database-elastic-pool.md).
- Para una guía sobre cómo usar grupos elásticos, consulte las [consideraciones de precio y rendimiento para grupos elásticos](sql-database-elastic-pool.md).
- secuencias de comandos de toouse trabajos elástico toorun Transact-SQL frente a cualquier número de bases de datos en el grupo de hello, vea [información general de los trabajos elástico](sql-database-elastic-jobs-overview.md).
- tooquery a través de cualquier número de bases de datos en el grupo de hello, consulte [información general sobre consultas elástico](sql-database-elastic-query-overview.md).
- Para las transacciones de cualquier número de bases de datos en el grupo de hello, consulte [transacciones elásticas](sql-database-elastic-transactions-overview.md).


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
