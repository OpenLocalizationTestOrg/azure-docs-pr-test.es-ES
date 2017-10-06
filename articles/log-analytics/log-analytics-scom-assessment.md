---
title: "aaaOptimize del entorno de System Center Operations Manager con análisis de registros de Azure | Documentos de Microsoft"
description: "Puede usar Hola sistema Center Operations Manager evaluación solución tooassess Hola a riesgo y el estado de los entornos de servidor a intervalos regulares."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: tysonn
ms.assetid: 49aad8b1-3e05-4588-956c-6fdd7715cda1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c024e53826e91524c120bdb98ae7d96d6dc37d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-environment-with-hello-system-center-operations-manager-assessment-preview-solution"></a>Optimizar el entorno con hello solución de System Center Operations Manager evaluación (versión preliminar)

![Símbolo de System Center Operations Manager Assessment](./media/log-analytics-scom-assessment/scom-assessment-symbol.png)

Puede usar Hola evaluación de Operations Manager del sistema Center solución tooassess Hola a riesgo y el estado de los entornos de servidor de System Center Operations Manager a intervalos regulares. En este artículo le ayuda a instalar, configurar y usar soluciones de Hola para que pueda tomar medidas correctivas para detectar posibles problemas.

Esta solución proporciona una lista de prioridades de infraestructura de servidor implementada tooyour específico de recomendaciones. recomendaciones de Hola se clasifican en foco cuatro áreas que le ayudarán a rápidamente comprender Hola a riesgo y tomar medidas correctivas.

recomendaciones de Hello efectuadas se basan en los conocimientos de Hola y experiencias adquiridas por los ingenieros de Microsoft de miles de visitas de clientes. Cada recomendación proporcionan instrucciones acerca de por qué un problema podría ser importante tooyou y cómo tooimplement Hola sugiere cambios.

Puede elegir las áreas de enfoque que son más importante organización tooyour y realizar un seguimiento del progreso hacia la consecución de un entorno de riesgo libre y en buen estado.

Después de que haya agregado la solución de Hola y una evaluación haya finalizado, resumen se muestra información de las áreas de enfoque en hello **sistema Center Operations Manager evaluación** panel para su infraestructura. Hello las secciones siguientes describen cómo toouse Hola información en hello **sistema Center Operations Manager evaluación** panel, donde puede ver y, a continuación, tomar las acciones recomendadas para su infraestructura SCOM.

![icono de la solución System Center Operations Manager](./media/log-analytics-scom-assessment/scom-tile.png)

![panel de Evaluación de System Center Operations Manager](./media/log-analytics-scom-assessment/scom-dashboard01.png)

## <a name="installing-and-configuring-hello-solution"></a>Instalar y configurar soluciones de Hola

solución de Hello funciona con el sistema de Microsoft Operations Manager 2012 R2 y 2012 SP1.

Usar hello después tooinstall de información y configurar soluciones de Hola.

 - Antes de poder usar una solución de evaluación en OMS, debe tener instalada la solución de Hola. Instale la solución de Hola de [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) o siguiendo las instrucciones de hello en [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md).

 - Después de agregar el área de trabajo de hello solución toohello, icono de System Center Operations Manager evaluación de hello en el panel de hello muestra el mensaje de Hola configuración adicional necesaria. Haga clic en el icono de Hola y siga los pasos de configuración de hello mencionados en la página de Hola

 ![Icono del panel de System Center Operations Manager](./media/log-analytics-scom-assessment/scom-configrequired-tile.png)

 Configuración del programa Hola a System Center Operations Manager puede realizarse a través de script de Hola siguiendo los pasos de hello mencionados en la página de configuración de Hola de solución de hello en OMS.

 En su lugar, evaluación de hello tooconfigure a través de la consola de SCOM, Hola de seguimiento a continuación los pasos de hello mismo orden
1. [Establecer Hola ejecutar como cuenta de sistema Center Operations Manager](#operations-manager-run-as-accounts-for-oms)  
2. [Configurar regla de System Center Operations Manager evaluación Hola](#configure-the-assessment-rule)

## <a name="system-center-operations-manager-assessment-data-collection-details"></a>Información detallada sobre la recopilación de datos de Evaluación de System Center Operations Manager

Hola evaluación de System Center Operations Manager recopila datos WMI, datos del registro, datos de registro de eventos, datos de Operations Manager a través de Windows PowerShell, las consultas SQL, recopilador de información de archivo con el servidor hello que ha habilitado.

Hello tabla siguiente muestran los métodos de recopilación de datos para System Center Operations Manager evaluación y con qué frecuencia se recopilan los datos por un agente.

| plataforma | Agente directo | Agente de SCOM | Azure Storage | ¿Se necesita SCOM? | Datos del agente de SCOM enviados a través del grupo de administración | Frecuencia de recopilación |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | | | | &#8226; | | siete días |

## <a name="operations-manager-run-as-accounts-for-oms"></a>Cuentas de ejecución de Operations Manager para OMS

OMS se basa en módulos de administración para las cargas de trabajo tooprovide servicios de valor añadido. Cada carga de trabajo requiere los módulos de administración de toorun de privilegios de cargas de trabajo específicas en un contexto de seguridad diferente, como una cuenta de dominio. Configurar un Operations Manager ejecutar como cuenta tooprovide información de credenciales.

Usar hello siguiente información tooset Hola Operations Manager ejecutar como cuenta de sistema Center Operations Manager.

### <a name="set-hello-run-as-account"></a>Cuenta de ejecución del conjunto Hola

1. En la consola de Operations Manager hello, vaya toohello **administración** ficha.
2. En hello **configuración de ejecución**, haga clic en **cuentas**.
3. Crear cuenta de ejecución, después a través del Asistente para crear una cuenta de Windows hello Hola. Hola cuenta toouse es Hola identificado y con todos los requisitos previos de Hola a continuación:

    >[!NOTE]
    Hola cuenta de ejecución debe cumplir los siguientes requisitos:
    - Un miembro de la cuenta de dominio del grupo de administradores local de hello en todos los servidores en el entorno de hello (todas las operaciones Manager Roles - servidor de administración, base de datos de Operations Manager, almacenamiento de datos, informes, consola Web, puerta de enlace)
    - Rol de administrador de la operación de grupo de administración de Hola que se va a evaluar
    - Ejecute hello [script](#sql-script-to-grant-granular-permissions-to-the-run-as-account) toogrant permisos granulares toohello cuenta en la instancia de SQL utilizada por Operations Manager.
      Nota: Si esta cuenta tiene derechos de sysadmin ya, a continuación, omitir la ejecución del script de Hola.

4. En **Seguridad de distribución**, seleccione **Más seguro**.
5. Especifique el servidor de administración de Hola dónde se distribuye la cuenta de hello.
3. Retroceda toohello configuración de ejecución y haga clic en **perfiles**.
4. Busque hello *perfil de valoración de SCOM*.
5. debe ser el nombre del perfil de Hello: *Microsoft System Center Advisor SCOM evaluación de perfil de ejecución*.
6. Haga clic en y actualizar sus propiedades y agregar Hola recientemente creado la cuenta de identificación que creó en el paso 3.

### <a name="sql-script-toogrant-granular-permissions-toohello-run-as-account"></a>SQL script toogrant permisos granulares toohello cuenta de ejecución

Ejecute hello después SQL script toogrant requerido permisos toohello cuenta de identificación de instancia de SQL de hello usa Operations Manager.

```
-- Replace <UserName> with hello actual user name being used as Run As Account.
USE master

-- Create login for hello user, comment this line if login is already created.
CREATE LOGIN [UserName] FROM WINDOWS


--GRANT permissions toouser.
GRANT VIEW SERVER STATE too[UserName]
GRANT VIEW ANY DEFINITION too[UserName]
GRANT VIEW ANY DATABASE too[UserName]

-- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
-- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
EXEC sp_msforeachdb N'USE [?]; CREATE USER [UserName] FOR LOGIN [UserName];'

Use msdb
GRANT SELECT too[UserName]
Go

--Give SELECT permission on all Operations Manager related Databases

--Replace hello Operations Manager database name with hello one in your environment
Use [OperationsManager];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager DatawareHouse database name with hello one in your environment
Use [OperationsManagerDW];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager Audit Collection database name with hello one in your environment
Use [OperationsManagerAC];
GRANT SELECT too[UserName]
GO

--Give db_owner on [OperationsManager] DB
--Replace hello Operations Manager database name with hello one in your environment
USE [OperationsManager]
GO
ALTER ROLE [db_owner] ADD MEMBER [UserName]

```


### <a name="configure-hello-assessment-rule"></a>Configurar reglas de evaluación de Hola

Hola sistema Center Operations Manager evaluación módulo de administración de la solución incluye una regla denominada *Microsoft System Center Asesor de SCOM evaluación ejecutar evaluación regla*. Esta regla es responsable de ejecutar la evaluación de Hola. tooenable Hola regla y configurar la frecuencia de hello, use Hola procedimientos siguientes.

De forma predeterminada, Hola Microsoft System Center Asesor de SCOM evaluación ejecutar evaluación regla está deshabilitada. evaluación de hello toorun, debe habilitar la regla hello en un servidor de administración. Usar hello pasos.

#### <a name="enable-hello-rule-for-a-specific-management-server"></a>Habilita la regla de Hola de un servidor de administración específico

1. Hola **Authoring** área de trabajo de la consola de Operations Manager hello, busque la regla de hello *Microsoft System Center Asesor de SCOM evaluación ejecutar evaluación regla* en hello **reglas** panel.
2. En los resultados de búsqueda de hello, seleccione Hola que incluye el texto hello *tipo: servidor de administración*.
3. Haga clic en regla de hello y, a continuación, haga clic en **invalida** > **para un determinado objeto de clase: servidor de administración**.
4.  En la lista de servidores de administración disponibles de hello, seleccione el servidor de administración de Hola donde se debe ejecutar regla Hola.
5.  Asegúrese de que cambia el valor de invalidación demasiado**True** para hello **habilitado** el valor del parámetro.  
    ![invalidar parámetro](./media/log-analytics-scom-assessment/rule.png)

Mientras se encuentra en esta ventana, configurar la frecuencia de Hola de hello ejecutar mediante el procedimiento siguiente Hola.

#### <a name="configure-hello-run-frequency"></a>Configurar la frecuencia de hello ejecutar

evaluación de Hello es intervalo predeterminado de Hola de toorun configurado cada 10.080 minutos (o siete días). Puede invalidar el valor mínimo tooa de hello valor de 1440 minutos (o un día). valor Hola representa el intervalo de tiempo mínimo de hello necesario entre ejecuciones sucesivas de evaluación. intervalo de saludo toooverride, use Hola pasos siguientes.

1. Hola **Authoring** área de trabajo de la consola de Operations Manager hello, busque la regla de hello *Microsoft System Center Asesor de SCOM evaluación ejecutar evaluación regla* en hello **reglas** panel.
2. En los resultados de búsqueda de hello, seleccione Hola que incluye el texto hello *tipo: servidor de administración*.
3. Haga clic en regla de hello y, a continuación, haga clic en **Hola de invalidación de regla** > **para todos los objetos de clase: servidor de administración**.
4. Hola de cambio **intervalo** tooyour del valor de parámetro deseado el valor del intervalo. En el ejemplo de Hola siguiente, el valor de Hola se establece too1440 minutos (un día).  
    ![parámetro de intervalo](./media/log-analytics-scom-assessment/interval.png)  
    Si el valor de Hola se establece a que no requiere herramientas de 1440 minutos, regla de Hola se ejecuta en un intervalo de un día. En este ejemplo, regla de hello omite el valor del intervalo de Hola y se ejecuta con una frecuencia de un día.


## <a name="understanding-how-recommendations-are-prioritized"></a>Cómo se establecen prioridades entre las recomendaciones

Cada recomendación efectuada se proporciona un valor de ponderación que identifica Hola importancia relativa de la recomendación de Hola. Se muestran solo recomendaciones más importantes de hello 10.

### <a name="how-weights-are-calculated"></a>Cálculo de las ponderaciones

Las ponderaciones son valores agregados en función de tres factores principales:

- Hola *probabilidad* que un asunto identificado pueda causar problemas. Una probabilidad más alta equivale tooa mayor puntuación total de recomendación de Hola.
- Hola *impacto* de problema de hello en su organización en caso de que se produzca un problema. Un mayor impacto equivale tooa mayor puntuación total de recomendación de Hola.
- Hola *esfuerzo* necesario recomendación de hello tooimplement. Un mayor esfuerzo equivale tooa de puntuación total menor para la recomendación de Hola.

Hola ponderación de cada recomendación se expresa como un porcentaje de hello puntuación total disponible para cada área de enfoque. Por ejemplo, si una recomendación en el área de enfoque de disponibilidad y continuidad del negocio de hello tiene una puntuación del 5%, implementación de esa recomendación aumenta la disponibilidad y continuidad del negocio puntuación total por 5%.

### <a name="focus-areas"></a>Áreas de enfoque

**Disponibilidad y continuidad empresarial** : este apartado muestra recomendaciones relacionadas con la disponibilidad de servicio, la resistencia de la infraestructura y la protección del negocio.

**Rendimiento y escalabilidad** -esta área de enfoque muestra toohelp recomendaciones de su organización crecer de infraestructura de TI, asegúrese de que su entorno de TI cumple los requisitos de rendimiento actuales y es capaz de toorespond toochanging necesidades de infraestructura.

**Actualización, migración e implementación** : toohelp recomendaciones actualizar muestra esta área de enfoque, migración e implementar la infraestructura existente de SQL Server tooyour.

**Operaciones y supervisión** : esta área de enfoque muestra recomendaciones toohelp agilizar las operaciones de TI, implementar el mantenimiento preventivo y maximizar el rendimiento.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>¿Debe conseguir tooscore 100% en cada área de enfoque?

No necesariamente. Hola recomendaciones se basan en los conocimientos de Hola y las experiencias adquiridas por los ingenieros de Microsoft fruto de miles de visitas de clientes. Sin embargo, no hay dos infraestructuras de servidores son Hola igual y determinadas recomendaciones puedan ser tooyou más o menos relevante. Por ejemplo, algunas recomendaciones de seguridad pueden ser menos relevantes si las máquinas virtuales no están expuesto toohello Internet. Algunas recomendaciones de disponibilidad pueden ser menos relevantes para los servicios que proporcionan informes y recopilaciones de datos ad hoc de baja prioridad. Los problemas que son tooa importante para el negocio maduro pueden inicio de tooa menos importante. Puede desea tooidentify qué áreas de enfoque son prioritarias para usted y, a continuación, observar cómo cambian las puntuaciones con el tiempo.

Cada recomendación incluye pautas que indican por qué es importante. Use esta guía tooevaluate si implementa la recomendación de hello es adecuado para usted, dada la naturaleza de Hola de sus necesidades de negocio de hello y servicios de TI de su organización.

## <a name="use-assessment-focus-area-recommendations"></a>Uso de las recomendaciones de área de enfoque de evaluación

Antes de poder usar una solución de evaluación en OMS, debe tener instalada la solución de Hola. tooread más acerca de cómo instalar soluciones, consulte [soluciones de análisis de registro agregar desde la Galería de soluciones de hello](log-analytics-add-solutions.md). Después de instalarlo, puede ver resumen de Hola de recomendaciones mediante el icono de System Center Operations Manager evaluación de hello en la página de información general de Hola de OMS.

Hola de vista resume de las evaluaciones de cumplimiento para su infraestructura y, a continuación, profundizar en recomendaciones.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>recomendaciones de tooview para una acción correctora foco área y take

1. En hello **Introducción** página, haga clic en hello **sistema Center Operations Manager evaluación** icono.
2. En hello **sistema Center Operations Manager evaluación** página, revise la información de resumen de hello en uno de los módulos de área de enfoque de hello y, a continuación, haga clic en uno tooview recomendaciones para dicha área de enfoque.
3. En cualquiera de las páginas de área de enfoque de hello, puede ver recomendaciones de hello prioridad diseñadas para su entorno. Haga clic en una recomendación en **objetos afectados** tooview detalles sobre por qué se realiza la recomendación de Hola.  
    ![área de enfoque](./media/log-analytics-scom-assessment/focus-area.png)
4. Puede tomar las medidas correctivas que se sugieren en **Acciones sugeridas**. Cuando se haya tratado elemento hello, evaluaciones posteriores registrarán que recomienda acciones se han realizado y aumentará su calificación de cumplimiento de normas. Los asuntos que se hayan corregido aparecerán en **Objetos superados**.

## <a name="ignore-recommendations"></a>Omisión de las recomendaciones

Si tiene las recomendaciones que desea tooignore, puede crear un archivo de texto que OMS usa tooprevent recomendaciones que aparecen en los resultados de la evaluación.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-want-tooignore"></a>recomendaciones de tooidentify que desea tooignore

1. Inicie sesión en el área de trabajo de tooyour y abra búsqueda de registros. Usar hello siguiendo las recomendaciones de toolist de consultas con error para los equipos de su entorno.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

    Esta es una consulta de búsqueda de registros de Hola de captura de pantalla que muestra:  
    ![búsqueda de registros](./media/log-analytics-scom-assessment/scom-log-search.png)

2. Elija las recomendaciones que desea tooignore. Usará los valores de hello de RecommendationId en el procedimiento siguiente Hola.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate y usar un archivo de texto IgnoreRecommendations.txt

1. Cree un archivo llamado IgnoreRecommendations.txt.
2. Pegue o escriba cada valor de RecommendationId para cada recomendación desea tooignore OMS en una línea independiente y, a continuación, guarde y cierre el archivo hello.
3. Coloque el archivo de Hola Hola después de carpeta en cada equipo donde desea que las recomendaciones de tooignore OMS.
4. En el servidor de administración de Operations Manager de hello - *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server.

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify que se omiten las recomendaciones

1. Después de hello próxima evaluación programada se ejecuta de forma predeterminada cada siete días, Hola especificado se marcan como omitidas y no aparecerán en el panel de evaluación de hello recomendaciones.
2. Puede usar Hola después a toolist de las consultas de búsqueda de registros todas las recomendaciones de hello pasa por alto.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

3. Si más adelante decide que desea que las recomendaciones de toosee pasa por alto, quite todos los archivos IgnoreRecommendations.txt o quite los valores de Recommendationid de ellos.

## <a name="system-center-operations-manager-assessment-solution-faq"></a>Preguntas más frecuentes sobre la solución Evaluación de System Center Operations Manager

*Había agregado el área de trabajo de hello evaluación solución toomy OMS. Pero no veo recomendaciones Hola. ¿Por qué no?* Después de agregar la solución de hello, utilice Hola siguiendo los pasos vista Hola recomendaciones en panel de OMS Hola.  

- [Establecer Hola ejecutar como cuenta de sistema Center Operations Manager](#operations-manager-run-as-accounts-for-oms)  
- [Configurar regla de System Center Operations Manager evaluación Hola](#configure-the-assessment-rule)


*¿Cuál es la frecuencia con un tooconfigure manera Hola evaluación se realiza?* Sí. Vea [Hola configurar frecuencia de ejecución](#configure-the-run-frequency).

*¿Si se detecta otro servidor después de que he agregado soluciones de System Center Operations Manager evaluación hello, se evaluará?* Sí, después de la detección, se evaluará cada siete días de forma predeterminada.

*¿Cuál es el nombre de hello del proceso de Hola que Hola la recopilación de datos?* AdvisorAssessment.exe

*¿Dónde se ejecuta proceso de hello AdvisorAssessment.exe?* AdvisorAssessment.exe se ejecuta con servicio de mantenimiento del servidor de administración de Hola Hola donde está habilitada la regla de evaluación de Hola. Con ese proceso, la detección de todo el entorno se realiza mediante la recopilación de datos remotos.

*¿Cuánto tiempo tarda en recopilar datos?* Recopilación de datos en el servidor de hello tarda aproximadamente una hora. Puede tardar más en entornos que tienen muchas instancias o bases de datos de Operations Manager.

*¿Qué ocurre si se establece el intervalo de saludo de hello evaluación que no requiere herramientas de 1440 minutos?*  evaluación hello es toorun preconfigurado en un máximo de una vez al día. Si invalida tooa valor de intervalo de hello inferior a 1440 minutos, evaluación de hello usa 1440 minutos como valor de intervalo de saludo.

*¿Cómo tooknow si hay errores de requisitos previos?* Si ejecutó la evaluación de hello y no ve los resultados, es probable que algunos de los requisitos previos para la evaluación de Hola Hola produjo un error. Puede ejecutar consultas: `Type=Operation Solution=SCOMAssessment` y `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` en hello toosee de búsqueda de registros no se pudo requisitos previos.

*Los requisitos previos que no se cumplen muestran el mensaje `Failed tooconnect toohello SQL Instance (….).`. ¿Cuál es el problema de hello?* AdvisorAssessment.exe, proceso de Hola que recopila los datos, se ejecuta con servicio de mantenimiento del servidor de administración de Hola Hola. Como parte de la evaluación de hello, proceso de hello intenta tooconnect toohello SQL Server donde está presente la base de datos de Operations Manager Hola. Este error puede producirse cuando las reglas de firewall bloquean la instancia de SQL Server de hello conexión toohello.

*¿Qué tipo de datos se recopilan?*  Hola siguientes tipos de datos se recopila: - WMI - registro datos - EventLog - Operations Manager datos a través de Windows PowerShell, las consultas SQL y archivo de recopilador de información.

*¿Por qué tengo tooconfigure una cuenta de ejecución?* Para un servidor de Operations Manager, se ejecutan varias consultas SQL. Puedan toorun, debe usar una cuenta de ejecución con los permisos necesarios. Además, las credenciales de administrador local son necesario tooquery WMI.

*¿Por qué se muestran solo Hola 10 recomendaciones principales?* En lugar de darle una lista exhaustiva y abrumadora de tareas, se recomienda centrarse primero en un nivel de prioridad de hello recomendaciones. Después de aplicarlas, se mostrarán más recomendaciones. Si lo prefiere lista detallada de toosee hello, puede ver todas las recomendaciones mediante la búsqueda de registros.

*¿Hay una manera tooignore una recomendación?* Sí, consulte hello [omitir recomendaciones](#Ignore-recommendations).


## <a name="next-steps"></a>Pasos siguientes

- [Buscar registros](log-analytics-log-searches.md) tooview obtener datos de la evaluación de System Center Operations Manager y las recomendaciones.
