---
title: "las consultas de análisis de aaaRun ad-hoc a través de varias bases de datos SQL de Azure | Documentos de Microsoft"
description: "Ejecute las consultas de análisis ad hoc a través de varias bases de datos SQL en la aplicación de varios inquilinos de hello Wingtip SaaS."
keywords: tutorial de SQL Database
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: billgib; sstein
ms.openlocfilehash: 140cd51fdd03b5a548147282b51ceb0ad80c944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-ad-hoc-analytics-queries-across-all-wingtip-saas-tenants"></a>Ejecución de consultas de análisis ad hoc en todos los inquilinos SaaS de Wingtip

En este tutorial, ejecutar consultas distribuidas en todo conjunto de bases de datos de inquilino de hello tooenable "ad-hoc" análisis. Consulta elástico es consultas tooenable usado distribuido, lo que requiere que se implementa una base de datos de análisis adicional (servidor de catálogo toohello). Estas consultas pueden extraer información ocultos en hello cotidianas operacionales de datos de aplicación de SaaS Wingtip hello.


En este tutorial, obtendrá información:

> [!div class="checklist"]

> * Acerca de las vistas globales de hello en cada base de datos, que permiten consultar eficaz entre los inquilinos
> * ¿Cómo toodeploy una base de datos de análisis ad hoc
> * ¿Cómo toorun consultas distribuidas en todas las bases de datos de inquilino



toocomplete se ha completado este tutorial, asegúrese de hello seguro después de requisitos previos:

* se implementa la aplicación de SaaS Wingtip Hello. vea toodeploy en menos de cinco minutos, [implementar y explorar la aplicación de SaaS Wingtip hello](sql-database-saas-tutorial.md)
* Azure PowerShell está instalado. Para más información, consulte [Introducción a Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).
* SQL Server Management Studio (SSMS) está instalado. toodownload e instale SSMS, vea [descargar SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


## <a name="ad-hoc-analytics-pattern"></a>Patrón de análisis ad hoc

Una de las grandes oportunidades de hello con aplicaciones de SaaS es ingente cantidad de Hola de toouse de datos de inquilino que se almacenan de forma centralizada en la nube de Hola. Utilice esta información sobre toogain los datos en la operación de Hola y el uso de la aplicación, los inquilinos, sus usuarios, las preferencias, comportamientos, etcetera. Esta información puede guiarle en el desarrollo de características, mejoras de facilidad de uso y otras inversiones en sus aplicaciones y servicios.

Es fácil obtener acceso a estos datos en una sola base de datos multiinquilino, pero no es tan fácil cuando se distribuyen a escala en miles de bases de datos. Un enfoque es toouse [consulta elástico](sql-database-elastic-query-overview.md), lo que permite realizar consultas a través de un conjunto distribuido de bases de datos con el esquema común. Consulta flexible usa un único *head* base de datos en el que se definen las tablas externas que reflejado tablas o vistas en hello distribuyen las bases de datos (inquilino). Las consultas se envían toothis principal base de datos es tooproduce compilado un plan de consulta distribuida, con algunas partes de la consulta de hello Enviar hacia abajo en las bases de datos del inquilino de toohello según sea necesario. Consulta flexible utiliza mapa de particiones de hello en ubicación hello tooprovide de base de datos de catálogo de Hola de bases de datos de inquilino de Hola. La configuración y la consulta son sencillas y utilizan [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference) estándar; además, admiten consultas ad hoc desde herramientas como Power BI y Excel.

Al distribuir las consultas entre bases de datos de inquilino de hello, elástica consulta proporciona una visión inmediata en los datos de producción en vivo. Sin embargo, cuando consulta elástico extrae datos de potencialmente muchas bases de datos, consultas latencia a veces puede ser superior de las consultas equivalentes envían única la base de datos de varios inquilinos tooa. Se debe tener cuidado al diseñar consultas con datos de hello toominimize que se devuelven. Consulta flexible es a menudo más apropiada para las consultas pequeñas cantidades de datos en tiempo real, como opuesto toobuilding utilizadas con frecuencia o las consultas de análisis complejos o informes. Si las consultas no funcionan correctamente, examine hello [plan de ejecución](https://docs.microsoft.com/sql/relational-databases/performance/display-an-actual-execution-plan) toosee qué parte de la consulta de Hola se ha insertado hacia abajo de la base de datos remota toohello y se devuelve la cantidad de datos. Las consultas que requieren un procesamiento analítico complejo en algunos casos pueden ser mejor atendidas si se extraen los datos de inquilino en una base de datos dedicada o un almacenamiento de datos optimizado para las consultas de análisis. Este patrón se explica en hello [tutorial de análisis de inquilino](sql-database-saas-tutorial-tenant-analytics.md). 

## <a name="get-hello-wingtip-application-scripts"></a>Obtener scripts de la aplicación hello Wingtip

Hello Wingtip SaaS scripts y código fuente de aplicación están disponibles en hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositorio de github. [Pasos de secuencias de comandos de toodownload Hola Wingtip SaaS](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="create-ticket-sales-data"></a>Creación de datos de ventas de entradas

toorun consultas en un conjunto de datos más interesante, crear datos de ventas de vale ejecutando Hola vale generador.

1. Hola *PowerShell ISE*, abra Hola... \\Módulos de aprendizaje\\análisis operativos\\"ad hoc" análisis\\*AdhocAnalytics.ps1 demostración* de secuencias de comandos y establezca Hola siguientes valores:
   * **$DemoScenario** = 1, **Purchase tickets for events at all venues** (comprar entradas para eventos de todas las ubicaciones).
2. Presione **F5** para ejecutar el script de Hola y generar ventas de vale. Mientras se ejecuta el script de Hola, continúe con los pasos de hello en este tutorial. datos de vale de Hola se consultan en hello *ejecutar consultas distribuida ad hoc* sección, por lo que espere Hola vale generador toocomplete, si aún está en ejecución cuando se obtiene toothat ejercicio.

## <a name="explore-hello-global-views"></a>Explorar vistas globales Hola

Hola aplicación SaaS de Wingtip se basa en un modelo de inquilinos por base de datos, por lo que se define el esquema de base de datos de inquilino de Hola desde la perspectiva del inquilino único. Existe información específica del inquilino en una tabla, *Venue*, que siempre tiene una sola fila y, además, se ha diseñado como montón, sin clave principal. No es necesario toobe relacionadas con otras tablas en el esquema de hello toohello *lugar* tabla, ya que en el uso normal, nunca hay alguna duda de qué datos de hello inquilino pertenecen.

Sin embargo, al consultar a través de todas las bases de datos, es importante que elástico consulta puede tratar datos de hello como si forma parte de una base de datos lógica particionada por inquilino. tooachieve esto, un conjunto de vistas 'globales' son la base de datos de inquilinos de toohello agregada que proyecte un Id. de inquilino en cada una de las tablas de Hola que se consultan globalmente. Por ejemplo, hello *VenueEvents* vista agrega una calculada *VenueId* toohello columnas proyectan de hello *eventos* tabla. Mediante la definición de tabla externa de hello en la base de datos principal de hello sobre *VenueEvents* (en lugar de hello subyacente *eventos* tabla), consulta flexible es capaz de toopush hacia abajo en función de las combinaciones *VenueId* para que se pueden ejecutar en paralelo en cada base de datos remoto (en lugar de en la base de datos principal de hello). Esto reduce considerablemente Hola cantidad de datos que se devuelven, lo que da como resultado un aumento sustancial del rendimiento para muchas consultas. Estas vistas globales se han creado previamente en todas las bases de datos de inquilino (y en *basetenantdb*).

1. Abra SSMS y [conectar toohello tenants1 -&lt;usuario&gt; server](sql-database-wtp-overview.md#explore-database-schema-and-execute-sql-queries-using-ssms).
2. Expanda **Bases de datos**, haga clic con el botón derecho en **contosoconcerthall** y seleccione **Nueva consulta**.
3. Ejecute hello después de diferencia de hello tooexplore de consultas entre tablas de único inquilino de Hola y vistas globales hello:

   ```T-SQL
   -- hello base Venue table, that has no VenueId associated.
   SELECT * FROM Venue

   -- Notice hello plural name 'Venues'. This view projects a VenueId column.
   SELECT * FROM Venues

   -- hello base Events table, which has no VenueId column.
   SELECT * FROM Events

   -- This view projects hello VenueId retrieved from hello Venues table.
   SELECT * FROM VenueEvents
   ```

En estas vistas, Hola *VenueId* se calcula como un hash del nombre de la ubicación de hello, pero cualquier enfoque podría ser toointroduce usa un valor único. Este enfoque es similar toohello manera clave de inquilino de Hola se calcula para su uso en el catálogo de Hola.

definición de hello tooexamine de hello *recintos* vista:

1. En **Explorador de objetos**, expanda **contosoconcerthall** > **Vistas**:

   ![vistas](media/sql-database-saas-tutorial-adhoc-analytics/views.png)

2. Haga clic con el botón derecho en **dbo.Venues**.
3. Seleccione **Incluir vista como** > **CREATE To** > **Nueva ventana del Editor de consultas**.

Script cualquiera de hello otro *lugar* vistas toosee cómo agregan hello *VenueId*.

## <a name="deploy-hello-database-used-for-ad-hoc-distributed-queries"></a>Implementar base de datos de hello utilizada para consultas distribuida ad hoc

Este ejercicio implementa hello *adhocanalytics* base de datos. Se trata de hello base de datos principal que contendrá el esquema de hello usado para realizar consultas en varias bases de datos de todos los inquilinos. base de datos de Hello es toohello implementada existente de servidor de catálogo, que es el servidor de hello usado para todos los relacionados con la administración de bases de datos de aplicación de ejemplo de Hola.

1. Abra... \\Módulos de aprendizaje\\análisis operativos\\"ad hoc" análisis\\*demostración AdhocAnalytics.ps1* en hello *PowerShell ISE* conjunto hello y valores siguientes:
   * **$DemoScenario** = 2, **Implementar una base de datos de análisis ad hoc**.

2. Presione **F5** toorun Hola script y crear hello *adhocanalytics* base de datos.

En la siguiente sección hello, Agregar base de datos de esquema toohello por lo que puede ser usado toorun distribuida consultas.

## <a name="configure-hello-database-for-running-distributed-queries"></a>Configurar base de datos de Hola para ejecutar consultas distribuidas

Este ejercicio agrega esquema (origen de datos externo de Hola y definiciones de tabla externa) toohello ad-hoc análisis base de datos que permite realizar consultas en varias bases de datos de todos los inquilinos.

1. Abra SQL Server Management Studio y conéctese toohello creado en el paso anterior de Hola de base de datos de análisis ad hoc. nombre de Hola de base de datos de hello será adhocanalytics.
2. Abra ...\Learning Modules\Operational Analytics\Adhoc Analytics\ *Initialize-AdhocAnalyticsDB.sql* en SSMS.
3. Revisar la secuencia de comandos SQL de Hola y tenga en cuenta Hola siguiente:

   Consulta flexible utiliza una credencial de ámbito de base de datos tooaccess cada de bases de datos de inquilino de Hola. Esta credencial debe toobe disponible en todas las bases de datos de Hola y normalmente se debe conceder los derechos mínimos de hello necesitan tooenable estas consultas ad hoc.

    ![crear credencial](media/sql-database-saas-tutorial-adhoc-analytics/create-credential.png)

   Hello origen de datos externo, que está había definido mapa de particiones de toouse Hola inquilino en la base de datos de catálogo de Hola. Al utilizar esto como origen de datos externo de hello, las consultas son bases de datos de tooall distribuida registrados en el catálogo de hello cuando se ejecuta la consulta de Hola. Ya que los nombres de servidor son diferentes para cada implementación, este script de inicialización Obtiene la ubicación de Hola de base de datos de catálogo de hello mediante la recuperación de servidor actual de hello (@@servername) donde se ejecuta el script de Hola.

    ![crear origen de datos externos](media/sql-database-saas-tutorial-adhoc-analytics/create-external-data-source.png)

   Hola tablas externas que hacen referencia a vistas globales de Hola se describe en la sección anterior de Hola y definido con **distribución = SHARDED(VenueId)**. Dado que cada *VenueId* tooa única base de datos se asigna Esto mejora el rendimiento para muchos escenarios como se muestra en la siguiente sección de Hola.

    ![crear tablas externas](media/sql-database-saas-tutorial-adhoc-analytics/external-tables.png)

   tabla local Hello *VenueTypes* que se crean y rellenan. Esta tabla de datos de referencia es común en todas las bases de datos de inquilino, por lo que se puede representar como una tabla local y rellena con datos comunes de Hola. Para algunas consultas que esto puede reducir Hola cantidad de datos movidos entre las bases de datos del inquilino de Hola y Hola *adhocanalytics* base de datos.

    ![crear tabla](media/sql-database-saas-tutorial-adhoc-analytics/create-table.png)

   Si incluye tablas de referencia de esta manera, ser datos y el esquema de tabla de hello tooupdate seguro cada vez que actualice las bases de datos del inquilino de Hola.

4. Presione **F5** toorun Hola script e inicializar hello *adhocanalytics* base de datos. 

Ahora puede ejecutar consultas distribuidas y recopilar información de todos los inquilinos.

## <a name="run-ad-hoc-distributed-queries"></a>Ejecución de consultas distribuidas ad hoc

Ahora que hello *adhocanalytics* base de datos está configurado, siga adelante y ejecute algunas consultas distribuidas. Incluir plan de ejecución de Hola para una mejor comprensión de donde sucede el procesamiento de consultas de Hola. 

Al inspeccionar el plan de ejecución de hello, mantenga el mouse sobre los iconos del plan de Hola para obtener más información. 

Toonote importante, es esa configuración **distribución = SHARDED(VenueId)** cuando se define el origen de datos externo de hello, mejora el rendimiento en muchos escenarios. Dado que cada *VenueId* asigna tooa única base de datos filtrado es datos fácilmente done remotamente, devolver Hola solo es necesario.

1. Abra ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\*Demo-AdhocAnalyticsQueries.sql* en SSMS.
2. Asegúrese de que está conectado toohello **adhocanalytics** base de datos.
3. Seleccione hello **consulta** menú y haga clic en **incluir Plan de ejecución real**
4. Resaltar hello *qué lugares están registrados actualmente?* consulta y presione **F5**.

   consulta Hola devuelve la lista de todo lugar de hello, que ilustra cómo rápido y fácil que es tooquery a través de todos los inquilinos y los datos devueltos desde cada inquilino.

   Inspeccionar el plan de Hola y que coste íntegro de hello es consultas remotas Hola porque estamos simplemente base de datos de curso tooeach inquilinos y seleccionando información de ubicación de Hola.

   ![SELECT * FROM dbo.Venues](media/sql-database-saas-tutorial-adhoc-analytics/query1-plan.png)

5. Consulta de hello seleccione siguiente y presione **F5**.

   Esta consulta combina datos de las bases de datos del inquilino de Hola y Hola local *VenueTypes* tabla (local, ya que es una tabla de hello *adhocanalytics* base de datos).

   Inspeccionar el plan de Hola y ver ese Hola mayoría del costo es consultas remotas Hola ya que se consulta la información de ubicación de cada inquilino (dbo. Recintos), y, a continuación, realice una combinación rápida local con hello locales *VenueTypes* nombre descriptivo de tabla toodisplay Hola.

   ![Combinación de datos remotos y locales](media/sql-database-saas-tutorial-adhoc-analytics/query2-plan.png)

6. Ahora seleccione hello *día en que fueron Hola mayoría vales vendidos?* consulta y presione **F5**.

   Esta consulta hace una combinación y una agregación un poco más complejas. ¿Qué es toonote importante es que remotamente realiza la mayor parte del procesamiento de hello y, una vez más, se devolver solo las filas Hola de que necesitemos, devolver una única fila con el número de venta del cada lugar vale agregado por día.

   ![query](media/sql-database-saas-tutorial-adhoc-analytics/query3-plan.png)


## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo:

> [!div class="checklist"]

> * Ejecutar consultas distribuidas en todas las bases de datos de inquilinos
> * Implementar una base de datos de análisis ad hoc y agregar consultas de esquema tooit toorun distribuida.


Ahora, intente hello [tutorial de análisis de inquilino](sql-database-saas-tutorial-tenant-analytics.md) tooexplore tooa independiente análisis de datos para el procesamiento de análisis más complejo de extracción...

## <a name="additional-resources"></a>Recursos adicionales

* Adicionales [tutoriales que parten Hola aplicación Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Consulta elástica](sql-database-elastic-query-overview.md)
