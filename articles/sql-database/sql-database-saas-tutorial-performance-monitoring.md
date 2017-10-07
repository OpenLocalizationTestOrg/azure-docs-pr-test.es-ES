---
title: "rendimiento de aaaMonitor de muchas bases de datos de SQL Azure en una aplicación de SaaS multiempresa | Documentos de Microsoft"
description: "Supervisar y administrar el rendimiento de las bases de datos y los grupos de aplicación de SaaS de Wingtip de base de datos de SQL Azure hello"
keywords: tutorial de SQL Database
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: f0d7ba456c485b7de249a56abac3cf4be3857285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-of-hello-wingtip-saas-application"></a>Supervisar el rendimiento de hello aplicación Wingtip SaaS

En este tutorial se describen varios escenarios clave de administración de rendimiento que se usan en aplicaciones de SaaS. Utiliza una actividad de toosimulate del generador de carga entre todas las bases de datos de inquilino, se muestran supervisión integrada de Hola y características de alertas de base de datos SQL y grupos elásticos.

aplicación de SaaS Wingtip Hello usa un modelo de datos único inquilino, donde cada lugar (inquilino) tiene su propia base de datos. Al igual que muchas aplicaciones de SaaS, Hola prevé patrón de carga de trabajo de inquilino es imprevisible y esporádico. En otras palabras, las ventas de entradas pueden producirse en cualquier momento. tootake la ventaja de este patrón de uso típico de la base de datos, las bases de datos se implementan en grupos de bases de datos elásticas de inquilino. Grupos elásticos optimizan el costo de Hola de una solución mediante el uso compartido de recursos entre varias bases de datos. Con este tipo de patrón, es importante toomonitor base de datos y tooensure de uso de recursos de grupo que carga razonablemente se reparten entre grupos. También debe tooensure que las bases de datos individuales tienen los recursos adecuados y que no están alcanzando grupos sus [eDTU](sql-database-what-is-a-dtu.md) límites. Este tutorial explora formas toomonitor y administrar grupos y las bases de datos y cómo tootake acción correctora en toovariations de respuesta de carga de trabajo.

En este tutorial, aprenderá a:

> [!div class="checklist"]

> * Simular el uso en las bases de datos del inquilino de hello mediante la ejecución de un generador de carga proporcionado
> * Bases de datos de inquilino de hello monitor como responden toohello aumento de carga
> * Escalar verticalmente Hola grupo elástico en respuesta toohello mayor de la base de datos de carga
> * Aprovisionar una segunda actividad de base de datos del saldo tooload grupo elástico


toocomplete se ha completado este tutorial, asegúrese de hello seguro después de requisitos previos:

* se implementa la aplicación de SaaS Wingtip Hello. vea toodeploy en menos de cinco minutos, [implementar y explorar la aplicación de SaaS Wingtip hello](sql-database-saas-tutorial.md)
* Azure PowerShell está instalado. Para más información, consulte [Introducción a Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).

## <a name="introduction-toosaas-performance-management-patterns"></a>Patrones de la administración de rendimiento de introducción tooSaaS

Administración del rendimiento de la base de datos consta de compilación y analizar datos de rendimiento y, a continuación, reacción toothis datos mediante el ajuste de parámetros toomaintain un tiempo de respuesta aceptable para su aplicación. Cuando se hospedan a varios inquilinos, grupos elástico de base de datos son un tooprovide de manera rentable y administración los recursos de un grupo de bases de datos con cargas de trabajo impredecibles. Con ciertos patrones de carga de trabajo, se pueden beneficiar de la administración en grupo un mínimo de dos bases de datos S3.

![medios](./media/sql-database-saas-tutorial-performance-monitoring/app-diagram.png)

Grupos y las bases de datos de hello en grupos, deben ser supervisado tooensure pueden permanecer dentro de intervalos aceptables de rendimiento. Optimizar Hola grupo toomeet Hola necesidades especiales de configuración de carga de trabajo agregado Hola de todas las bases de datos, asegurarse de que hello Edtu de grupo adecuado para hello carga de trabajo general. Ajustar Hola por base de datos min y por base de datos máximo de eDTU valores tooappropriate valores para sus requisitos de aplicación específica.

### <a name="performance-management-strategies"></a>Estrategias de administración del rendimiento

* tooavoid tener toomanually supervisar el rendimiento, que resulta más eficaz**establecer alertas que desencadenan cuando las bases de datos o grupos extraviado fuera de los intervalos normales**.
* Hola toorespond las fluctuaciones de tooshort término en el nivel de rendimiento de agregado de Hola de un grupo, **nivel de eDTU de grupo se puede escalar hacia arriba o hacia abajo**. Si se produce esta fluctuación de forma regular o de predicción, **ajuste de escala en el grupo de hello puede ser toooccur programada automáticamente**. Por ejemplo, cuando haya poca carga de trabajo (por la noche o durante el fin de semana), redúzcalo verticalmente.
* las fluctuaciones de término toolonger toorespond o cambios en Hola número de bases de datos, **bases de datos individuales se pueden mover a otros grupos**.
* toorespond tooshort término aumenta en *individuales* carga de base de datos **bases de datos individuales pueden deja fuera de un grupo y asignar un nivel de rendimiento individuales**. Una vez que se reduce la carga de hello, base de datos de hello, a continuación, se pueden devolver toohello grupo. Cuando esto se conoce de antemano, las bases de datos se pueden mover antelación tooensure Hola base de datos siempre tiene recursos Hola necesarios, tooavoid impacto en otras bases de datos en bloque de Hola. Si este requisito es de predicción, como un lugar experimentan un urgente de ventas de vale para un evento popular, este comportamiento de administración puede integrarse en la aplicación hello.

Hola [portal de Azure](https://portal.azure.com) proporciona supervisión y alertas relacionadas con la mayoría de los recursos integrados. Para SQL Database, la supervisión y las alertas están disponibles para las bases de datos y los grupos. Este integradas de supervisión y alerta es específico del recurso, por lo que es toouse adecuada para pequeñas cantidades de recursos, pero no es muy práctico cuando se trabaja con muchos recursos.

Para escenarios de alto volumen donde se trabaja con muchos recursos, se puede usar [Log Analytics (OMS)](sql-database-saas-tutorial-log-analytics.md). Se trata de un servicio de Azure independiente que proporciona análisis de los registros de diagnóstico emitidos y de telemetría recopilados en un área de trabajo de Log Analytics. Análisis de registros pueden recopilar la telemetría de muchos servicios y ser tooquery usado y establecer alertas.

## <a name="get-hello-wingtip-application-source-code-and-scripts"></a>Obtener scripts y código fuente hello Wingtip

Hello Wingtip SaaS scripts y código fuente de aplicación están disponibles en hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositorio de github. [Pasos de secuencias de comandos de toodownload Hola Wingtip SaaS](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="provision-additional-tenants"></a>Aprovisionamiento de inquilinos adicionales

Mientras grupos pueden ser rentables con solo dos bases de datos de S3, Hola más bases de datos que se encuentran en Hola Hola de grupo más rentable Hola promedio efecto se convierte en. Para una buena comprensión de cómo funciona la administración y la supervisión del rendimiento a escala, para este tutorial se necesitan al menos 20 bases de datos implementadas.

Si ha proporcionado un lote de inquilinos en un tutorial anterior, omitir toohello [simular el uso en todas las bases de datos de inquilino](#simulate-usage-on-all-tenant-databases) sección.

1. Abra... \\Módulos de aprendizaje\\administración y supervisión del rendimiento\\*demostración PerformanceMonitoringAndManagement.ps1* en hello *PowerShell ISE*. Mantenga este script abierta, ya que se van a ejecutar varios escenarios en este tutorial.
1. Establezca **$DemoScenario** = **1**, **Aprovisionamiento de un lote de inquilinos**
1. Presione **F5** secuencia de comandos de toorun Hola.

script de Hola implementará a 17 inquilinos en menos de cinco minutos.

Hola *New-TenantBatch* script utiliza un conjunto anidado o vinculado de [el Administrador de recursos](../azure-resource-manager/index.md) plantillas que crear un lote de inquilinos, que de forma predeterminada, copia la base de datos de hello **basetenantdb** en hello catálogo server toocreate Hola inquilino bases de datos, a continuación, registra estos en el catálogo de Hola y finalmente los inicializa con el tipo de nombre y la ubicación del inquilino de Hola. Esto es coherente con la manera de hello aplicación hello aprovisiona a un nuevo inquilino. Los cambios realizados demasiado*basetenantdb* es tooany aplicado nuevos inquilinos aprovisionados a partir de ahí. Vea hello [tutorial de administración de esquema](sql-database-saas-tutorial-schema-management.md) toosee cómo cambia el esquema de toomake demasiado*existente* bases de datos de inquilinos (incluidos hello *basetenantdb* base de datos).

## <a name="simulate-usage-on-all-tenant-databases"></a>Simulación de uso en todas las bases de datos de inquilinos

Hola *PerformanceMonitoringAndManagement.ps1 demostración* script es siempre que simula una carga de trabajo que se ejecutan en todas las bases de datos de inquilino. la carga de Hola se genera mediante uno de los escenarios de carga disponibles de hello:

| Demostración | Escenario |
|:--|:--|
| 2 | Generación de una carga de intensidad normal (aprox. 40 DTU) |
| 3 | Generación de una carga con ráfagas más prolongadas y frecuentes por base de datos|
| 4 | Generación de una carga con mayores ráfagas de DTU por base de datos (aprox. 80 DTU)|
| 5 | Generación de una carga normal y una carga elevada en un solo inquilino (aprox. 95 DTU)|
| 6 | Generación de una carga desequilibrada en varios grupos|

Generador de carga de Hola se aplica un *sintético* base de datos de carga de CPU solo tooevery inquilinos. Generador de Hello inicia un trabajo para cada base de datos de inquilinos, que llama a un procedimiento almacenado periódicamente que genera una carga de Hola. intervalos, la duración y niveles de carga de hello (en Edtu) varían entre todas las bases de datos, simulación de la actividad de inquilinos imprevisible.

1. Abra... \\Módulos de aprendizaje\\administración y supervisión del rendimiento\\*demostración PerformanceMonitoringAndManagement.ps1* en hello *PowerShell ISE*. Mantenga este script abierta, ya que se van a ejecutar varios escenarios en este tutorial.
1. Establezca **$DemoScenario** = **2**, *Generación de una carga de intensidad normal*.
1. Presione **F5** tooapply un tooall de carga de las bases de datos de inquilino.

Wingtip es una aplicación de SaaS, y carga de Hola mundo real en una aplicación de SaaS normalmente es esporádico e imprevisibles. toosimulate esto, Hola carga generador genera una carga aleatorio se distribuye entre todos los inquilinos. Para tooemerge de patrón de carga hello, por lo que ejecutar el generador de carga de Hola durante 3 a 5 minutos antes de intentar toomonitor Hola carga en las secciones siguientes de Hola se necesitan varios minutos.

> [!IMPORTANT]
> Generador de carga de saludo se está ejecutando como una serie de trabajos en la sesión de PowerShell local. Mantener hello *PerformanceMonitoringAndManagement.ps1 demostración* ficha abierta. Si cerrar pestaña de Hola o suspender su equipo, deja de generador de carga de Hola. Generador de carga de Hello permanece en un *invocar trabajo* estado donde genera una carga en los nuevos inquilinos que se aprovisionan después de que se inició el generador de Hola. Use *Ctrl-C* toostop invocar nuevos trabajos y script de Hola de salida. Generador de carga de Hello continuará toorun, pero solo en los inquilinos existentes.

## <a name="monitor-resource-usage-using-hello-azure-portal"></a>Supervisar el uso de recursos con hello portal de Azure

uso de recursos de hello toomonitor que los resultados de Hola de carga que se aplica, abrir el grupo de portal toohello de Hola que contiene las bases de datos del inquilino de hello:

1. Abra hello [portal de Azure](https://portal.azure.com) y examinar toohello *tenants1 -&lt;usuario&gt;*  server.
1. Desplácese hacia abajo, busque los grupos elásticos y haga clic en **Pool1**. Este grupo contiene todas las bases de datos del inquilino de hello creados hasta ahora.

Observar hello **grupo elástico supervisión** y **supervisión de bases de datos elásticas** gráficos.

Hola utilización de recursos del grupo es uso de la base de datos agregados de Hola para todas las bases de datos en bloque de Hola. gráfico de base de datos de Hello muestra hello cinco bases de datos más recientes:

![](./media/sql-database-saas-tutorial-performance-monitoring/pool1.png)

Porque hay bases de datos adicionales en el grupo de hello más allá de Hola cinco principal, uso del grupo de hello muestra las actividades que no se reflejan en el gráfico de cinco bases de datos principales de Hola. Para ver detalles adicionales, haga clic en **Uso de recursos de base de datos**:

![](./media/sql-database-saas-tutorial-performance-monitoring/database-utilization.png)


## <a name="set-performance-alerts-on-hello-pool"></a>Establecer alertas de rendimiento en el bloque de Hola

Establecer una alerta en el grupo de Hola que se desencadena en \>utilización del 75% como sigue:

1. Abra *Pool1* (en hello *tenants1 -\<usuario\>*  server) en hello [portal de Azure](https://portal.azure.com).
1. Haga clic en **Reglas de alerta** y en **+ Agregar alerta**:

   ![agregar alerta](media/sql-database-saas-tutorial-performance-monitoring/add-alert.png)

1. Proporcione un nombre, como **High DTU**,
1. Establecer Hola siguientes valores:
   * **Métrica = eDTU percentage**
   * **Condición = greater than**.
   * **Umbral = 75**.
   * **Período = sobre Hola últimos 30 minutos**.
1. Agregar una toohello de dirección de correo electrónico *administrador adicional email(s)* y haga clic en **Aceptar**.

   ![Establecer alerta](media/sql-database-saas-tutorial-performance-monitoring/alert-rule.png)


## <a name="scale-up-a-busy-pool"></a>Escalado vertical de un grupo ocupado

Si aumenta el nivel de carga global de hello en un punto de toohello de grupo que maxes out grupo hello y alcanza el 100% del uso de eDTU, a continuación, rendimiento de la base de datos individual se ve afectado, potencialmente los tiempos de respuesta de consulta para todas las bases de datos en bloque de Hola.

**Corto plazo**, considere la posibilidad de escalar verticalmente recursos adicionales de hello grupo tooprovide o quitar las bases de datos del grupo de hello (moverlos tooother grupos, o fuera del nivel de servicio independiente de hello grupo tooa).

**A largo plazo**, considere la posibilidad de optimizar las consultas o un índice de rendimiento de base de datos de uso tooimprove. Función hello tooperformance de sensibilidad de la aplicación emite a su tooscale de práctica recomendada un grupo de seguridad antes de llegar a 100% del uso de eDTU. Usar una alerta toowarn, de antemano.

Puede simular un grupo de disponibilidad por incrementar la carga de hello producida por el generador de Hola. Causando hello tooburst de bases de datos con más frecuencia y para carga agregado ya lo está, creciente hello en el grupo de hello sin cambiar los requisitos de Hola de bases de datos individuales de Hola. Cómo ampliar el grupo de hello fácilmente se realiza en el portal de Hola o de PowerShell. Este ejercicio usa portal Hola.

1. Establecer *$DemoScenario* = **3**, _generar carga con ráfagas más y más frecuentes por base de datos_ intensidad de hello tooincrease de carga agregado de hello en grupo de Hello sin cambiar la carga máxima de hello requerida por cada base de datos.
1. Presione **F5** tooapply un tooall de carga de las bases de datos de inquilino.

1. Vaya demasiado**Pool1** Hola portal de Azure.

Hola Monitor aumenta el uso de eDTU de grupo en el gráfico superior Hola. Tarda unos minutos para nuevos tookick de carga Hola superior, pero rápidamente verá grupo Hola iniciar toohit máxima utilización, y como carga de hello steadies en el nuevo patrón de hello, rápidamente sobrecargas grupo Hola.

1. tooscale grupo hello, haga clic en **Configurar grupo** en parte superior de Hola de hello **Pool1** página.
1. Ajustar hello **eDTU del grupo** configuración demasiado**100**. Cambiar hello eDTU del grupo no cambia las opciones de cada base de datos de hello (que sigue siendo 50 eDTU máx. por base de datos). Puede ver los valores de cada base de datos de hello en hello derecha de hello **Configurar grupo** página.
1. Haga clic en **guardar** agrupación de toosubmit Hola solicitudes tooscale Hola.

Vuelva demasiado**Pool1** > **Introducción** hello tooview gráficos de supervisión. Supervisar el efecto de Hola de proporcionar grupo Hola con más recursos (aunque con algunas bases de datos y una carga aleatoria no resulta siempre fácil toosee forma concluyente hasta que se ejecuta durante algún tiempo). Aunque se trata de hello gráficos tenga en cuenta que el 100% en hello superior gráfico ahora representa 100 Edtu, mientras que en hello inferior gráfico 100% es todavía 50 Edtu como Hola por base de datos máximo sigue siendo 50 Edtu.

Bases de datos permanecen en línea y estén totalmente disponibles a lo largo del proceso de Hola. En hello último momento como cada base de datos está listo toobe habilitado con hello eDTU del grupo nuevo, todas las conexiones activas se interrumpen. Código de la aplicación siempre debe escribirse tooretry quitar conexiones por lo que se volverá a conectar la base de datos de toohello en grupo de escalado de Hola.

## <a name="load-balance-between-pools"></a>Equilibrio de carga entre grupos

Como una alternativa tooscaling grupo hello, cree un segundo grupo y mover las bases de datos en él hello toobalance cargar entre Hola dos grupos. toodo se debe crear este nuevo grupo de hello en Hola mismo servidor que hello en primer lugar.

1. Hola [portal de Azure](https://portal.azure.com), abra hello **tenants1 -&lt;usuario&gt;**  server.
1. Haga clic en **+ nuevo grupo** toocreate un bloque de servidor actual Hola.
1. En hello **grupo elástico de base de datos** plantilla:

    1. Establecer **nombre** demasiado*Pool2*.
    1. Deje Hola tarifa como **grupo estándar**.
    1. Haga clic en **Configurar grupo**.
    1. Establecer **eDTU del grupo** demasiado*eDTU 50*.
    1. Haga clic en **agregar bases de datos** toosee una lista de bases de datos servidor hello que pueden agregarse demasiado*Pool2*.
    1. Seleccione cualquier toomove 10 bases de datos en estas toohello nuevo grupo y, a continuación, haga clic en **seleccione**. Si ha ha estado ejecutando el generador de carga de hello, servicio Hola ya sabe que el perfil de rendimiento requiere un grupo mayor que 50 eDTU del tamaño predeterminado hello y recomienda a partir de una configuración de eDTU 100.

    ![recomendación](media/sql-database-saas-tutorial-performance-monitoring/configure-pool.png)

    1. Para este tutorial, deje predeterminado de hello en 50 Edtu y haga clic en **seleccione** nuevo.
    1. Seleccione **Aceptar** toocreate Hola nuevo grupo y toomove Hola seleccionado bases de datos en él.

Crear grupo de Hola y mover las bases de datos de Hola tarda unos minutos. Tal y como se han movido a las bases de datos permanecen en línea y totalmente accesible hasta Hola muy último momento, momento en que se cierran todas las conexiones abiertas. Tiene alguna lógica de reintento, siempre y cuando los clientes conectarán a continuación, toohello base de datos en el nuevo grupo de Hola.

Examinar demasiado**Pool2** (en hello *tenants1* server) tooopen Hola grupo y supervisar su rendimiento. Si no lo ve, espera para el aprovisionamiento de hello toocomplete de grupo nuevo.

Ahora verá que el uso de los recursos en *Pool1* ha disminuido y que *Pool2* tiene una carga similar.

## <a name="manage-performance-of-a-single-database"></a>Administrar el rendimiento de una sola base de datos

Si una base de datos en un grupo experimenta una carga intensiva prolongada, dependiendo de la configuración del grupo de hello, puede suelen toodominate recursos de hello en el grupo de Hola y afectar a otras bases de datos. Si la actividad de hello es probable que toocontinue durante algún tiempo, base de datos de Hola se puede mover temporalmente fuera del grupo de Hola. Esto permite Hola Hola de toohave de base de datos de recursos adicionales necesarios y que se aísla de hello otras bases de datos.

Este ejercicio simula el efecto de Hola de Contoso un auditorio experimentando una carga elevada al vales vaya a la venta de un concierto popular.

1. Abra Hola... \\ *PerformanceMonitoringAndManagement.ps1 demostración* secuencia de comandos.
1. Establezca **$DemoScenario = 5, Generación de una carga normal y una carga elevada en un solo inquilino (aprox. 95 DTU).**
1. Establezca **$SingleTenantDatabaseName = contosoconcerthall**
1. Ejecutar script de Hola con **F5**.


1. Hola [portal de Azure](https://portal.azure.com) abrir **Pool1**.
1. Inspeccionar hello **grupo elástico supervisión** del gráfico y busque el uso de eDTU de grupo de hello aumentado. Después de un minuto o dos, una mayor carga de hello debe iniciar tookick en y, rápidamente, debería ver que el grupo de Hola llega a 100% de utilización.
1. Inspeccionar hello **supervisión de bases de datos elásticas** presentación que se muestra en las bases de datos más recientes de Hola Hola última hora. Hola *contosoconcerthall* base de datos pronto debe aparecer como una de las bases de datos más recientes de hello cinco.
1. **Haga clic en supervisión de bases de datos elásticas de hello** **gráfico** y lo abre hello **utilización de recursos de base de datos** página donde puede supervisar cualquiera de las bases de datos de Hola. Esto le permite aislar la presentación de Hola de hello *contosoconcerthall* base de datos.
1. En la lista de Hola de bases de datos, haga clic en **contosoconcerthall**.
1. Haga clic en **tarifa (escala Dtu)** tooopen hello **configurar rendimiento** página donde puede establecer un nivel de rendimiento independiente para la base de datos de Hola.
1. Haga clic en hello **estándar** pestaña Opciones de escala de tooopen hello en el nivel estándar Hola.
1. Deslice hello **control deslizante DTU** tooright tooselect **100** Dtu. Tenga en cuenta esta condición corresponde el objetivo de servicio toohello, **S3**.
1. Haga clic en **aplicar** toomove Hola base de datos del grupo de Hola y conviértala en un *para estándar S3* base de datos.
1. Una vez finalizada la escala es una completa, monitor Hola efecto en la base de datos de hello contosoconcerthall y Pool1 en las hojas elásticas de base de datos y de grupo Hola.

Una vez que desaparezca de la carga elevada de hello en base de datos de hello contosoconcerthall debe rápidamente vuelve toohello grupo tooreduce su costo. Si no está claro al que se realizará podría establecer una alerta en la base de datos de hello, que se desencadenará cuando el uso de su DTU cae por debajo de Hola por base de datos máximo en el grupo de Hola. El movimiento de una base de datos a un grupo se describe en el ejercicio 5.

## <a name="other-performance-management-patterns"></a>Otros modelos de administración del rendimiento

**Ajuste de escala preferentes** en donde se explorar cómo tooscale una base de datos aislado, sabía que toolook de base de datos para anterior ejercicio de Hola. Si Administración de Hola de Contoso un auditorio tenía informado Wingtips de venta de vale inminente de hello, base de datos de Hola se hayan movido fuera del grupo de hello antelación. En caso contrario, es probable que habría requería una alerta en el grupo de Hola o toospot de la base de datos de hello lo que estaba sucediendo. Desearía toolearn respecto de hello otros inquilinos de hello grupo quejan de reducción del rendimiento. Y si el inquilino de hello puede predecir cuánto necesitan recursos adicionales, puede configurar una base de datos de automatización de Azure runbook toomove Hola fuera del grupo de hello y, a continuación, realizar la copia en una programación definida.

**Autoservicio escalado inquilino** porque el ajuste de escala es una tarea que se llaman fácilmente a través de la API de administración de hello, puede fácilmente crear bases de datos de inquilino de tooscale de capacidad de hello en la aplicación de acceso de inquilino y ofrecer como una característica de su servicio de SaaS. Por ejemplo, permitir que los inquilinos self-administer escalado vertical y horizontalmente, quizás directamente vinculada facturación tootheir!

**Ajuste de escala en un grupo de arriba y abajo en los patrones de uso de toomatch de una programación**

Cuando el uso de inquilinos agregado sigue los patrones de uso de predicción, puede usar Automatización de Azure tooscale un grupo de arriba y abajo según una programación. Por ejemplo, puede reducir un grupo verticalmente después de las 6 p.m. y escalarlo de nuevo antes de las 6 a.m. entre semana porque sabe que se necesitan menos recursos.



## <a name="next-steps"></a>Pasos siguientes

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Simular el uso en las bases de datos del inquilino de hello mediante la ejecución de un generador de carga proporcionado
> * Bases de datos de inquilino de hello monitor como responden toohello aumento de carga
> * Escalar verticalmente Hola grupo elástico en respuesta toohello mayor de la base de datos de carga
> * Aprovisionar una segunda actividad de base de datos de grupo elástico tooload saldo Hola

[Tutorial sobre la restauración de un único inquilino](sql-database-saas-tutorial-restore-single-tenant.md)


## <a name="additional-resources"></a>Recursos adicionales

* Adicionales [tutoriales que se basan en la implementación de aplicaciones de SaaS Wingtip Hola](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Grupos elásticos de SQL](sql-database-elastic-pool.md)
* [Azure Automation](../automation/automation-intro.md)
* [Log Analytics](sql-database-saas-tutorial-log-analytics.md): tutorial de configuración y uso de Log Analytics
