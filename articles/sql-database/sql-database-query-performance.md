---
title: "aaaQuery información del rendimiento de base de datos de SQL de Azure | Documentos de Microsoft"
description: "Supervisión del rendimiento de consulta identifica Hola mayoría usan la CPU realiza consultas con una base de datos de SQL Azure."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a>Query Performance Insight de Base de datos SQL de Azure
Administrar y optimizar el rendimiento de Hola de bases de datos relacional son una tarea difícil que requiere conocimientos importantes e inversión de tiempo. Información de rendimiento de consultas permite toospend menos tiempo a la solución de problemas de rendimiento de la base de datos proporcionando siguiente hello:

* Información más detallada sobre el consumo de recursos (DTU) de las bases de datos. 
* Hola principales consultas por recuento de CPU/duración/ejecución, que pueden optimizarse para mejorar el rendimiento.
* Hola capacidad toodrill hacia abajo en los detalles de Hola de una consulta, ver su texto y el historial de utilización de recursos. 
* Anotaciones de ajuste del rendimiento que muestran las acciones realizadas por el [Asesor de Base de datos SQL de Azure](sql-database-advisor.md)  



## <a name="prerequisites"></a>Requisitos previos
* Información de rendimiento de consultas requiere que el [Almacén de consultas](https://msdn.microsoft.com/library/dn817826.aspx) esté activo en la base de datos. Si no se está ejecutando el almacén de consultas, el portal de hello solicita tooturn en.

## <a name="permissions"></a>Permisos
siguiente Hello [el control de acceso basado en roles](../active-directory/role-based-access-control-what-is.md) permisos son necesario toouse Query Performance Insight: 

* **Lector**, **propietario**, **colaborador**, **colaborador de la base de datos de SQL**, o **SQL Server colaborador** permisos son tooview requiere Hola que consumen más recursos gráficos y las consultas. 
* **Propietario**, **colaborador**, **colaborador de la base de datos de SQL**, o **SQL Server colaborador** permisos son necesarios tooview texto de la consulta.

## <a name="using-query-performance-insight"></a>Uso de Query Performance Insight
Información de rendimiento de consultas es fácil toouse:

* Abra [portal de Azure](https://portal.azure.com/) y base de datos de búsqueda que desea tooexamine. 
  * En el menú de la izquierda, bajo Soporte y solución de problemas, seleccione "Información de rendimiento de consultas".
* En la primera ficha hello, revise la lista de Hola de las consultas principales de consumo de recursos.
* Seleccione una consulta individual tooview sus detalles.
* Abra el [Asesor de Base de datos SQL de Azure](sql-database-advisor.md) y compruebe si existen recomendaciones disponibles.
* Usar controles deslizantes o zoom toochange iconos observado intervalo.
  
    ![panel de rendimiento](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> Un par de horas de datos debe toobe capturado por el almacén de consultas para la información de rendimiento de consultas de base de datos SQL tooprovide. Si no tiene ninguna actividad base de datos de Hola o almacén de consultas no estaba activo durante un período de tiempo determinado, gráficos de hello estará vacíos cuando se muestra ese período de tiempo. Puede habilitar el almacén de consulta en cualquier momento si no se está ejecutando.   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a>Revisión de las consultas que más CPU consumen
Hola [portal](http://portal.azure.com) Hola siguientes:

1. Base de datos SQL tooa y haga clic en **toda la configuración de** > **soporte técnico y solución de problemas** > **consultar información de rendimiento de**. 
   
    ![Información de rendimiento de consultas][1]
   
    se abre la vista de consultas top Hello y se muestran consultas de consumo de CPU superiores Hola.
2. Haga clic en alrededor de gráfico de Hola para obtener más información.<br>Hello línea superior muestra total % DTU de base de datos de hello, mientras que las barras de hello muestran % de CPU utilizado en consultas de hello seleccionado durante el intervalo seleccionado de hello (por ejemplo, si **semana pasada** se selecciona cada barra representa un día).
   
    ![principales consultas][2]
   
    cuadrícula de la parte inferior de Hello representa información agregada para las consultas de hello visible.
   
   * Id. de consulta: identificador único de la consulta en la base de datos.
   * CPU por consulta durante el intervalo observable (depende de la función de agregación).
   * Duración por consulta (depende de la función de agregación).
   * Número total de ejecuciones para una consulta determinada.
     
     Seleccionar o borrar tooinclude de las consultas individuales o excluirlos de gráfico de hello mediante las casillas de verificación.
3. Si los datos se convierte en obsoletos, haga clic en hello **actualizar** botón.
4. Puede usar controles deslizantes y el intervalo de observación de zoom botones toochange e investigar picos: ![configuración](./media/sql-database-query-performance/zoom.png)
5. Opcionalmente, si desea una vista diferente, puede seleccionar la pestaña **Personalizado** y establecer:
   
   * Métrica (CPU, duración, recuento de ejecuciones)
   * Intervalo de tiempo (últimas 24 horas, semana anterior, mes anterior). 
   * Número de consultas.
   * Función de agregación.
     
     ![Configuración](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a>Visualización de los detalles de las consultas individuales
detalles de la consulta tooview:

1. Haga clic en cualquier consulta en la lista de Hola de las consultas principales.
   
    ![details](./media/sql-database-query-performance/details.png)
2. se abre la vista de detalles de Hola y recuento de consumo/duración/ejecución de CPU de hello las consultas se divide en el tiempo.
3. Haga clic en alrededor de gráfico de Hola para obtener más información.
   
   * Gráfico superior muestra los línea con total % DTU de base de datos, y las barras de Hola % de CPU utilizado por la consulta seleccionada Hola.
   * Segundo gráfico muestra la duración total por consulta seleccionada Hola.
   * Gráfico de la parte inferior muestra el número total de ejecuciones por consulta seleccionada Hola.
     
     ![detalles de consulta][3]
4. Si lo desea, utilice los controles deslizantes, botones de zoom o haga clic en **configuración** toocustomize cómo se muestran los datos de consulta o toopick un período de tiempo diferente.

## <a name="review-top-queries-per-duration"></a>Revisión de las principales consultas por duración
En actualización reciente de Hola de Query Performance Insight, presentamos dos nuevas métricas que pueden ayudarle a identificar posibles cuellos de botella: recuento de ejecución y la duración.<br>

Consultas de larga duración tienen mayor potencial de hello más recursos de bloqueo, bloquear a otros usuarios y limitar la escalabilidad. También son mejores candidatas para la optimización de Hola.<br>

tooidentify consultas de larga ejecución:

1. Abra la pestaña **Personalizado** en Información de rendimiento de consultas para la base de datos seleccionada
2. Cambiar las métricas toobe **duración**
3. Seleccione el número de consultas y el intervalo de observación
4. Seleccione la función de agregación
   
   * **Sum** aumenta el tiempo de ejecución de todas las consultas durante todo el intervalo de observación.
   * **Max** busca consultas cuyo tiempo de ejecución era máximo en todo el intervalo de observación.
   * **AVG** busca el tiempo medio de ejecución de todas las ejecuciones de consulta y mostrarle Hola superior fuera de estos promedios. 
     
     ![duración de la consulta][4]

## <a name="review-top-queries-per-execution-count"></a>Revisión de las principales consultas por recuento de ejecuciones
Es posible que el elevado número de ejecuciones no afecte a la propia base de datos y el uso de recursos puede ser bajo, pero la aplicación general podría ralentizarse.

En algunos casos, recuento de ejecución muy alto puede provocar tooincrease de red de ida y vuelta. Los ciclos de ida y vuelta afectan significativamente al rendimiento. Son latencia toonetwork de asunto y toodownstream latencia del servidor. 

Por ejemplo, muchos sitios Web orientadas a datos con un alto grado tener acceso a base de datos de Hola para cada solicitud de usuario. Mientras que la agrupación de conexiones permite, hello aumenta el tráfico de red y la carga de procesamiento en el servidor de base de datos de hello pueden afectar negativamente al rendimiento.  Consejo general es tookeep mínimo absoluto de tooan de viajes de ida y vuelta.

tooidentify se ejecutan con frecuencia consultas consultas ("locuaces"):

1. Abra la pestaña **Personalizado** en Información de rendimiento de consultas para la base de datos seleccionada
2. Cambiar las métricas toobe **recuento de ejecución**
3. Seleccione el número de consultas y el intervalo de observación
   
    ![recuento de ejecuciones de la consulta][5]

## <a name="understanding-performance-tuning-annotations"></a>Descripción de las anotaciones de ajuste del rendimiento
Mientras se explora la carga de trabajo en Query Performance Insight, quizás haya notado iconos con una línea vertical en la parte superior gráfico Hola.<br>

Estos iconos son anotaciones; representan el rendimiento que afecta a las acciones realizadas por el [Asesor de Base de datos SQL de Azure](sql-database-advisor.md). Al desplazamiento de anotación, obtendrá información básica acerca de la acción de hello:

![anotación de la consulta][6]

Si desea obtener más tooknow o aplicar la recomendación del asistente, haga clic en el icono de Hola. Se abrirán los detalles de la acción. Si se trata de una recomendación activa, puede aplicarla inmediatamente mediante el comando.

![detalles de la anotación de la consulta][7]

### <a name="multiple-annotations"></a>Varias anotaciones.
Es posible que debido a nivel de zoom, las anotaciones que se cierre tooeach otros obtener contraerá en uno. Un icono especial representará este suceso y, al hacer clic en él, se abrirá una nueva hoja donde se mostrará una lista de las anotaciones agrupadas.
Correlación de consultas y las acciones de optimización del rendimiento puede ayudar a toobetter a comprender la carga de trabajo. 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a>Optimización de la configuración de almacén de consultas de Hola para Query Performance Insight
Durante el uso de información de rendimiento de consultas, pueden surgir Hola siguientes mensajes del almacén de consultas:

* "El Almacén de consultas no está configurado correctamente en esta base de datos. Haga clic aquí toolearn más."
* "El Almacén de consultas no está configurado correctamente en esta base de datos. Haga clic aquí toochange configuración." 

Estos mensajes suelen aparecen al almacén de consultas no es capaz de toocollect nuevos datos. 

El primer caso sucede si el Almacén de consultas está en estado de solo lectura y los parámetros están óptimamente establecidos. Para solucionarlo, puede aumentar el tamaño del Almacén de consultas o borrar el Almacén de consultas.

![botón qds][8]

El segundo caso sucede si el Almacén de consultas está desactivado o los parámetros no están óptimamente establecidos. <br>Puede cambiar Hola captura y retención enable y directivas de almacén de consultas mediante la ejecución de comandos siguientes o directamente desde el portal:

![botón qds][9]

### <a name="recommended-retention-and-capture-policy"></a>Directiva de retención y captura recomendada
Hay dos tipos de directivas de retención:

* Tamaño basa - si se alcanza tooAUTO conjunto limpiará datos automáticamente si se encuentran cerca tamaño máximo.
* Tiempo en la función: de forma predeterminada se establecerá too30 días, lo que significa que, si el almacén de consultas se quedará sin espacio, eliminará consultar información más de 30 días

La directiva de capturas se podría establecer como:

* **Todas**: captura todas las consultas.
* **Automática**: se ignoran las consultas poco frecuentes y las consultas con una duración de ejecución y compilación insignificantes. Los umbrales para la duración del tiempo de ejecución y de compilación y para el recuento de ejecuciones se determinan internamente. Se trata de una opción predeterminada de Hola.
* **Ninguna**: el Almacén de consultas deja de capturar nuevas consultas, pero las estadísticas en tiempo de ejecución de las consultas ya capturadas siguen recopilándose.

Se recomienda establecer todas las directivas tooAUTO y limpia directiva too30 días:

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

Aumentar el tamaño del almacén de consultas. Esto podría ser realizadas por base de datos de conexión tooa y emitir consulta siguiente:

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

Aplicar esta configuración finalmente realizará el almacén de consultas recopilar nuevas consultas, sin embargo, si no desea toowait puede borrar el almacén de consultas. 

> [!NOTE]
> Ejecución de la consulta siguiente eliminará toda la información actual de hello almacén de consultas. 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a>Resumen
Información de rendimiento de consultas le ayudará a comprender el impacto de hello de la carga de trabajo de consulta y cómo se relaciona con toodatabase el consumo de recursos. Con esta característica, aprenderá acerca de las consultas que consumen más de hello y, identificar fácilmente hello las toofix antes de que resulten un problema.

## <a name="next-steps"></a>Pasos siguientes
Para obtener más recomendaciones acerca de cómo mejorar el rendimiento de saludo de la base de datos SQL, haga clic en [recomendaciones](sql-database-advisor.md) en hello **Query Performance Insight** hoja.

![Asesor de rendimiento](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

