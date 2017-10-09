---
title: "aaaOptimize su entorno de SQL Server con análisis de registros de Azure | Documentos de Microsoft"
description: "Con análisis de registros de Azure, puede usar Hola evaluación de SQL solución tooassess Hola a riesgo y el estado de los entornos de SQL server a intervalos regulares."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f31326d8cdad3ef5d5a190614d1a18c1dac826ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-sql-server-environment-with-hello-sql-assessment-solution-in-log-analytics"></a>Optimizar el entorno de SQL Server con hello soluciones de evaluación de SQL de análisis de registros

![Símbolo de SQL Assessment](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

Puede usar Hola evaluación de SQL solución tooassess Hola a riesgo y el estado de los entornos de servidor a intervalos regulares. En este artículo le ayudará a instalar la solución de Hola para que pueda tomar medidas correctivas para detectar posibles problemas.

Esta solución proporciona una lista de prioridades de infraestructura de servidor implementada tooyour específico de recomendaciones. recomendaciones de Hola se clasifican en seis foco áreas que le ayudarán a rápidamente comprender Hola a riesgo y tomar medidas correctivas.

recomendaciones de Hello efectuadas se basan en los conocimientos de Hola y experiencias adquiridas por los ingenieros de Microsoft de miles de visitas de clientes. Cada recomendación proporcionan instrucciones acerca de por qué un problema podría ser importante tooyou y cómo tooimplement Hola sugiere cambios.

Puede elegir las áreas de enfoque que son más importante organización tooyour y realizar un seguimiento del progreso hacia la consecución de un entorno de riesgo libre y en buen estado.

Después de que haya agregado la solución de Hola y una evaluación haya finalizado, resumen se muestra información de las áreas de enfoque en hello **evaluación de SQL** panel para la infraestructura de hello en su entorno. Hello las secciones siguientes describen cómo toouse Hola información en hello **evaluación de SQL** panel, donde puede ver y, a continuación, tomar las acciones recomendadas para su infraestructura de SQL server.

![imagen del icono de evaluación de SQL](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![imagen del panel de evaluación de SQL](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-hello-solution"></a>Instalar y configurar soluciones de Hola
Evaluación de SQL funciona con todas las versiones actualmente compatibles de SQL Server para las ediciones Standard, Developer y Enterprise de Hola.

Usar hello después tooinstall de información y configurar soluciones de Hola.

* Deben instalarse agentes en servidores con SQL Server instalado.
* Hola solución de evaluación de SQL requiere una versión compatible de .NET Framework 4 instalado en cada equipo que tiene un agente OMS.
* En soluciones de orden tooinstall hello, usuario de hello debe ser un administrador o colaborador toohello suscripción de Azure cuando utilizando Hola portal de Azure. Además, el usuario de hello debe ser un miembro de hello OMS área de trabajo colaborador o administrador de rol en el portal de OMS de Hola.
* Cuando se utiliza el agente de Operations Manager Hola con la evaluación de SQL, necesitará una cuenta de Operations Manager Run-As toouse. Para más información, consulte [Cuentas de ejecución de Operations Manager para OMS](#operations-manager-run-as-accounts-for-oms) más adelante.

  > [!NOTE]
  > Hola MMA agente no admite cuentas de Operations Manager Run-As.
  >
  >
* Agregar tooyour de solución de evaluación de SQL Hola se describe el área de trabajo OMS mediante el proceso de hello en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md). No es necesario realizar ninguna configuración más.

> [!NOTE]
> Después de Agregar solución hello, archivo de hello AdvisorAssessment.exe se agrega tooservers con agentes. Datos de configuración se leen y, a continuación, envían toohello servicio OMS en la nube de Hola para su procesamiento. Lógica es aplicado toohello recibe datos y servicio de nube de hello registra datos de Hola.

## <a name="sql-assessment-data-collection-details"></a>Detalles de la recopilación de datos de la evaluación de SQL
Evaluación de SQL recopila datos WMI, datos del registro, los datos de rendimiento y los resultados de vista de administración dinámica de SQL Server que se utilizan a agentes de Hola que se ha habilitado.

Hello tabla siguiente muestran los métodos de recopilación de datos para los agentes, si es necesario Operations Manager (SCOM) y cómo se recopilan los datos a menudo por un agente.

| plataforma | Agente directo | Agente de SCOM | Azure Storage | ¿Se necesita SCOM? | Datos del agente de SCOM enviados a través del grupo de administración | Frecuencia de recopilación |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  | &#8226; |7 días |

## <a name="operations-manager-run-as-accounts-for-oms"></a>Cuentas de ejecución de Operations Manager para OMS
Análisis de registros de OMS utilizan hello agente de Operations Manager y toocollect del grupo de administración y servicio OMS de toohello de datos de envío. OMS se basa en módulos de administración para las cargas de trabajo tooprovide servicios de valor añadido. Cada carga de trabajo requiere los módulos de administración de toorun de privilegios de cargas de trabajo específicas en un contexto de seguridad diferente, como una cuenta de dominio. Necesita información de credenciales de tooprovide mediante la configuración de una cuenta de Operations Manager ejecutar como.

Usar hello siga información tooset Hola Operations Manager cuenta de ejecución para la evaluación de SQL.

### <a name="set-hello-run-as-account-for-sql-assessment"></a>Defina Hola ejecutar como cuenta de evaluación de SQL
 Si ya usas Hola módulo de administración de SQL Server, debe utilizar esa cuenta de ejecución.

#### <a name="tooconfigure-hello-sql-run-as-account-in-hello-operations-console"></a>Hola tooconfigure SQL cuenta de ejecución en la consola del operador Hola
> [!NOTE]
> Si utilizas hello OMS dirigir el agente, en lugar de agente SCOM hello, módulo de administración de hello siempre se ejecuta en el contexto de seguridad de Hola de hello cuenta de sistema Local. Omitir pasos 1-5 siguiente y, a continuación, ejecución o Hola ejemplo de T-SQL o Powershell, especificando NT AUTHORITY\SYSTEM como nombre de usuario de Hola.
>
>

1. En Operations Manager, abra la consola del operador de hello y, a continuación, haga clic en **administración**.
2. En **Run As Configuration** (Configuración de ejecución), haga clic en **Perfiles** y abra **OMS SQL Assessment Run As Profile** (Perfil de ejecución de evaluación de SQL para OMS).
3. En hello **cuentas de ejecución** página, haga clic en **agregar**.
4. Seleccione una cuenta de identificación de Windows que contiene las credenciales de hello necesarias para SQL Server, o haga clic en **New** toocreate uno.

   > [!NOTE]
   > Hola ejecutar como el tipo de cuenta debe ser Windows. Hola cuenta de ejecución también debe formar parte del grupo de administradores Local en todos los servidores de Windows que hospedan instancias de SQL Server.
   >
   >
5. Haga clic en **Guardar**.
6. Modifique y, a continuación, ejecute hello según la muestra de T-SQL en cada tooRun necesario de instancia de SQL Server toogrant permisos mínimos cuenta tooperform evaluación de SQL. Sin embargo, esto no es necesario toodo si una cuenta de ejecución ya forma parte del rol de servidor sysadmin de hello en instancias de SQL Server.

```
---
    -- Replace <UserName> with hello actual user name being used as Run As Account.
    USE master

    -- Create login for hello user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions toouser.
    GRANT VIEW SERVER STATE too[<UserName>]
    GRANT VIEW ANY DEFINITION too[<UserName>]
    GRANT VIEW ANY DATABASE too[<UserName>]

    -- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
    -- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="tooconfigure-hello-sql-run-as-account-using-windows-powershell"></a>Hola tooconfigure SQL cuenta de ejecución mediante Windows PowerShell
Abra una ventana de PowerShell y ejecute Hola siguiente secuencia de comandos después de haberlo actualizado con la información:

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a>Cómo se establecen prioridades entre las recomendaciones
Cada recomendación efectuada se proporciona un valor de ponderación que identifica Hola importancia relativa de la recomendación de Hola. Hola solo se muestran diez recomendaciones más importantes.

### <a name="how-weights-are-calculated"></a>Cálculo de las ponderaciones
Las ponderaciones son valores agregados en función de tres factores principales:

* Hola *probabilidad* que un asunto identificado pueda causar problemas. Una probabilidad más alta equivale tooa mayor puntuación total de recomendación de Hola.
* Hola *impacto* de problema de hello en su organización en caso de que se produzca un problema. Un mayor impacto equivale tooa mayor puntuación total de recomendación de Hola.
* Hola *esfuerzo* necesario recomendación de hello tooimplement. Un mayor esfuerzo equivale tooa de puntuación total menor para la recomendación de Hola.

Hola ponderación de cada recomendación se expresa como un porcentaje de hello puntuación total disponible para cada área de enfoque. Por ejemplo, si una recomendación de seguridad de Hola y de área de enfoque de cumplimiento tiene una puntuación del 5%, implementación de esa recomendación aumentará la seguridad y cumplimiento de normas puntuación total por 5%.

### <a name="focus-areas"></a>Áreas de enfoque
**Seguridad y cumplimiento** : este apartado muestra recomendaciones en caso de posibles amenazas e infracciones de seguridad, directivas corporativas y requisitos de cumplimiento técnico, legal y reglamentario.

**Disponibilidad y continuidad empresarial** : este apartado muestra recomendaciones relacionadas con la disponibilidad de servicio, la resistencia de la infraestructura y la protección del negocio.

**Rendimiento y escalabilidad** -esta área de enfoque muestra toohelp recomendaciones de su organización crecer de infraestructura de TI, asegúrese de que su entorno de TI cumple los requisitos de rendimiento actuales y es capaz de toorespond toochanging necesidades de infraestructura.

**Actualización, migración e implementación** : toohelp recomendaciones actualizar muestra esta área de enfoque, migración e implementar la infraestructura existente de SQL Server tooyour.

**Operaciones y supervisión** : esta área de enfoque muestra recomendaciones toohelp agilizar las operaciones de TI, implementar el mantenimiento preventivo y maximizar el rendimiento.

**Administración de cambios y configuración** -recomendaciones muestra esta área de enfoque toohelp proteger las operaciones diarias, asegúrese de que cambios no negativamente afectar a la infraestructura, establecer procedimientos de control de cambios y tootrack y auditoría configuraciones del sistema.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>¿Debe conseguir tooscore 100% en cada área de enfoque?
No necesariamente. Hola recomendaciones se basan en los conocimientos de Hola y las experiencias adquiridas por los ingenieros de Microsoft fruto de miles de visitas de clientes. Sin embargo, no hay dos infraestructuras de servidores son Hola igual y determinadas recomendaciones puedan ser tooyou más o menos relevante. Por ejemplo, algunas recomendaciones de seguridad pueden ser menos relevantes si las máquinas virtuales no están expuesto toohello Internet. Algunas recomendaciones de disponibilidad pueden ser menos relevantes para los servicios que proporcionan informes y recopilaciones de datos ad hoc de baja prioridad. Los problemas que son tooa importante para el negocio maduro pueden inicio de tooa menos importante. Puede desea tooidentify qué áreas de enfoque son prioritarias para usted y, a continuación, observar cómo cambian las puntuaciones con el tiempo.

Cada recomendación incluye pautas que indican por qué es importante. Debe usar esta guía tooevaluate si implementa la recomendación de hello es adecuado para usted, dada la naturaleza de Hola de sus necesidades de negocio de hello y servicios de TI de su organización.

## <a name="use-assessment-focus-area-recommendations"></a>Uso de las recomendaciones de área de enfoque de evaluación
Antes de poder usar una solución de evaluación en OMS, debe tener instalada la solución de Hola. tooread más acerca de cómo instalar soluciones, consulte [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md). Después de instalarlo, puede ver resumen de Hola de recomendaciones mediante el icono de evaluación de SQL de hello en la página de información general de Hola de OMS.

Hola de vista resume de las evaluaciones de cumplimiento para su infraestructura y, a continuación, profundizar en recomendaciones.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>recomendaciones de tooview para una acción correctora foco área y take
1. En hello **Introducción** página, haga clic en hello **evaluación de SQL** icono.
2. En hello **evaluación de SQL** página, revise la información de resumen de hello en uno de los módulos de área de enfoque de hello y, a continuación, haga clic en uno tooview recomendaciones para dicha área de enfoque.
3. En cualquiera de las páginas de área de enfoque de hello, puede ver recomendaciones de hello prioridad diseñadas para su entorno. Haga clic en una recomendación en **objetos afectados** tooview detalles sobre por qué se realiza la recomendación de Hola.  
    ![imagen de las recomendaciones de evaluación de SQL](./media/log-analytics-sql-assessment/sql-assess-focus.png)
4. Puede tomar las medidas correctivas que se sugieren en **Acciones sugeridas**. Cuando se haya tratado elemento hello, evaluaciones posteriores registrarán que recomienda acciones se han realizado y aumentará su calificación de cumplimiento de normas. Los asuntos que se hayan corregido aparecerán en **Objetos superados**.

## <a name="ignore-recommendations"></a>Omisión de las recomendaciones
Si tiene las recomendaciones que desea tooignore, puede crear un archivo de texto que utilice OMS tooprevent recomendaciones que aparecen en los resultados de la evaluación.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-will-ignore"></a>recomendaciones de tooidentify que pasarán por alto
1. Inicie sesión en el área de trabajo de tooyour y abra búsqueda de registros. Usar hello siguiendo las recomendaciones de toolist de consultas con error para los equipos de su entorno.

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   Esta es una consulta de búsqueda de registros de captura de pantalla mostrando hello: ![no se pudo recomendaciones](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)
2. Elija las recomendaciones que desea tooignore. Usará los valores de hello de RecommendationId en el procedimiento siguiente Hola.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate y usar un archivo de texto IgnoreRecommendations.txt
1. Cree un archivo llamado IgnoreRecommendations.txt.
2. Pegue o escriba cada valor de RecommendationId para cada recomendación desea tooignore OMS en una línea independiente y, a continuación, guarde y cierre el archivo hello.
3. Coloque el archivo de Hola Hola después de carpeta en cada equipo donde desea que las recomendaciones de tooignore OMS.
   * En equipos con Microsoft Monitoring Agent (conectado directamente o a través de Operations Manager): hello *SystemDrive*: \Program Files\Microsoft Monitoring Agent\Agent
   * En el servidor de administración de Operations Manager de hello - *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify que se omiten las recomendaciones
1. Después de hello próxima evaluación programada se ejecuta de forma predeterminada cada 7 días, Hola especificado se marcan como omitidas y no aparecerán en el panel de evaluación de hello recomendaciones.
2. Puede usar Hola después a toolist de las consultas de búsqueda de registros todas las recomendaciones de hello pasa por alto.

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. Si más adelante decide que desea que las recomendaciones de toosee pasa por alto, quite todos los archivos IgnoreRecommendations.txt o quite los valores de Recommendationid de ellos.

## <a name="sql-assessment-solution-faq"></a>Preguntas más frecuentes sobre soluciones de evaluación de SQL
*¿Con qué frecuencia se ejecuta una evaluación?*

* evaluación de Hola se realiza cada 7 días.

*¿Cuál es la frecuencia con un tooconfigure manera Hola evaluación se realiza?*

* De momento, no.

*¿Si se detecta otro servidor después de que he agregado Hola solución de evaluación de SQL, se evaluará?*

* Sí, una vez que se detecte, se evaluará cada 7 días a partir de entonces.

*¿Si se retira un servidor, cuándo se quitará de evaluación de hello?*

* Si un servidor no envía datos durante 3 semanas, se quitará.

*¿Cuál es el nombre de hello del proceso de Hola que Hola la recopilación de datos?*

* AdvisorAssessment.exe

*¿Cuánto tarda para toobe de datos que se recopilan?*

* recopilación de datos reales de Hello en servidor hello tarda aproximadamente 1 hora. Puede tardar más en servidores que tengan un gran número de bases de datos o instancias de SQL.

*¿Qué tipo de datos se recopila?*

* se recopila Hola siguientes tipos de datos:
  * WMI
  * Registro
  * Contadores de rendimiento
  * Vistas de administración dinámica (DMV) de SQL

*¿Hay una manera tooconfigure cuando los datos se recopilan?*

* De momento, no.

*¿Por qué tengo tooconfigure una cuenta de ejecución?*

* Para SQL Server, se ejecuta un número reducido de consultas SQL. En orden para ellos se debe usar toorun, una cuenta de ejecución con tooSQL de permisos VIEW SERVER STATE.  Además, en orden tooquery WMI, se necesitan credenciales de administrador local.

*¿Por qué se muestran solo Hola 10 recomendaciones principales?*

* En lugar de darle una lista exhaustiva y abrumadora de tareas, se recomienda centrarse primero en un nivel de prioridad de hello recomendaciones. Después de aplicarlas, se mostrarán más recomendaciones. Si lo prefiere lista detallada de toosee hello, puede ver todas las recomendaciones mediante la búsqueda de registros OMS Hola.

*¿Hay una manera tooignore una recomendación?*

* Sí, consulte la sección [Omisión de las recomendaciones](#ignore-recommendations) anterior.

## <a name="next-steps"></a>Pasos siguientes
* [Buscar registros](log-analytics-log-searches.md) tooview obtener datos de la evaluación de SQL y las recomendaciones.
