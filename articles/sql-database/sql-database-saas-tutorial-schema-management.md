---
title: "esquema de base de datos de SQL Azure aaaManage en una aplicación de varios inquilinos | Documentos de Microsoft"
description: "Administración del esquema para varios inquilinos en una aplicación multiinquilino que usa Azure SQL Database"
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
ms.date: 07/28/2017
ms.author: billgib; sstein
ms.openlocfilehash: ea946e556808dabd60dd39cb8173d0512d4bddec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-schema-for-multiple-tenants-in-hello-wingtip-saas-application"></a>Administrar esquemas para varios inquilinos en hello aplicación Wingtip SaaS

Hola [primer tutorial de SaaS Wingtip](sql-database-saas-tutorial.md) muestra cómo puede proporcionar una base de datos de inquilino y registrarlo en el catálogo de hello aplicación hello. Como cualquier aplicación Hola aplicación SaaS Wingtip evolucionará con el tiempo y a veces será necesario base de datos de cambios toohello. Pueden incluir cambios de esquema nueva o modificada, datos de referencia nuevos o modificados y el rendimiento de la aplicación óptimo de tooensure de las tareas rutinarias de la base de datos mantenimiento. Con una aplicación SaaS, estos cambios deben toobe implementa de manera coordinada a través de una línea potencialmente masiva de las bases de datos de inquilino. Para estos toobe cambios en el futuro de inquilinos bases de datos, será necesario toobe incorporar Hola proceso de aprovisionamiento.

Este tutorial explora dos escenarios - implementación de las actualizaciones de datos de referencia para todos los inquilinos y reoptimización un índice en hello de la tabla que contiene datos de referencia de Hola. Hola [trabajos elásticos](sql-database-elastic-jobs-overview.md) característica es tooexecute usa estas operaciones en todos los inquilinos y hello *dorada* base de datos de inquilinos que se utiliza como plantilla para nuevas bases de datos.

En este tutorial, aprenderá a:

> [!div class="checklist"]

> * Crear una cuenta de trabajo
> * Consultas entre varios inquilinos
> * Actualizar datos en todas las bases de datos de inquilino
> * Crear un índice en una tabla en todas las bases de datos de inquilino


toocomplete este tutorial, asegúrese de hello seguro siguiendo los requisitos previos se cumplen:

* se implementa la aplicación de SaaS Wingtip Hello. vea toodeploy en menos de cinco minutos, [implementar y explorar la aplicación de SaaS Wingtip hello](sql-database-saas-tutorial.md)
* Azure PowerShell está instalado. Para más información, consulte [Introducción a Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).
* se instala la versión más reciente de Hola de SQL Server Management Studio (SSMS). [Descarga e instalación de SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

*Este tutorial usa características de hello servicio de base de datos SQL que se encuentran en una vista previa limitada (trabajos de base de datos elástica). Si desea toodo en este tutorial, proporcione el identificador de suscripción tooSaaSFeedback@microsoft.com con el asunto = elástico de vista previa de los trabajos. Después de recibir la confirmación de que se ha habilitado la suscripción, [descargar e instalar los cmdlets de trabajos de la versión preliminar más reciente de hello](https://github.com/jaredmoo/azure-powershell/releases). Esta versión preliminar es limitada, de modo que póngase en contacto SaaSFeedback@microsoft.com si necesita asistencia.*


## <a name="introduction-toosaas-schema-management-patterns"></a>Introducción tooSaaS patrones de la administración de esquema

Hello inquilino único por base de datos de SaaS patrón ventajas de muchas maneras de aislamiento de los datos Hola que da como resultado, pero en hello mismo tiempo que aumenta la complejidad adicional de Hola de mantener y administrar muchas bases de datos. [Trabajos elásticos](sql-database-elastic-jobs-overview.md) facilita la administración y la administración de nivel de datos SQL de Hola. Trabajos permiten toosecurely y ejecutan de forma confiable, tareas (secuencias de comandos de T-SQL) independientes de la interacción del usuario o una entrada, en un grupo de bases de datos. Este método puede ser utilizado toodeploy esquema y los cambios de datos de referencia entre todos los inquilinos en una aplicación. Trabajos elásticos también pueden ser utilizado toomaintain una *dorada* utiliza la copia de base de datos de hello toocreate nuevos inquilinos, así se garantiza siempre tenga hello más recientes esquema y datos de referencia.

![pantalla](media/sql-database-saas-tutorial-schema-management/schema-management.png)


## <a name="elastic-jobs-limited-preview"></a>Versión preliminar limitada de Trabajos elásticos

Hay una nueva versión de Trabajos elásticos que ahora es una característica integrada de Azure SQL Database (no requiere servicios ni componentes adicionales). Esta nueva versión de Trabajos elásticos ofrece actualmente una versión preliminar limitada. Esta vista previa limitada actualmente admite cuentas de trabajo de PowerShell toocreate y toocreate de T-SQL y administrar trabajos.

> [!NOTE]
> *Este tutorial usa características de hello servicio de base de datos SQL que se encuentran en una vista previa limitada (trabajos de base de datos elástica). Si desea toodo en este tutorial, proporcione el identificador de suscripción tooSaaSFeedback@microsoft.com con el asunto = elástico de vista previa de los trabajos. Después de recibir la confirmación de que se ha habilitado la suscripción, [descargar e instalar los cmdlets de trabajos de la versión preliminar más reciente de hello](https://github.com/jaredmoo/azure-powershell/releases). Esta versión preliminar es limitada, de modo que póngase en contacto SaaSFeedback@microsoft.com si necesita asistencia.*

## <a name="get-hello-wingtip-application-scripts"></a>Obtener scripts de la aplicación hello Wingtip

Hello Wingtip SaaS scripts y código fuente de aplicación están disponibles en hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositorio de github. [Pasos de secuencias de comandos de toodownload Hola Wingtip SaaS](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="create-a-job-account-database-and-new-job-account"></a>Creación de una base de datos de cuentas de trabajo y una nueva cuenta de trabajo

Este tutorial necesita que usar PowerShell toocreate Hola trabajo base de datos y el trabajo de cuenta. Como MSDB y el Agente SQL, trabajos elástico usa SQL Azure base de datos toostore definiciones de trabajos, el estado de trabajo y el historial. Una vez creada la cuenta de trabajo de hello, puede crear y supervisar trabajos inmediatamente.

1. Abra... \\Módulos de aprendizaje\\Schema Management\\*demostración SchemaManagement.ps1* en hello **PowerShell ISE**.
1. Presione **F5** secuencia de comandos de toorun Hola.

Hola *demostración SchemaManagement.ps1* Hola de llamadas de script *implementar SchemaManagement.ps1* script toocreate una *S2* base de datos denominada **jobaccount** en el servidor de catálogo Hola. A continuación, crea la cuenta de trabajo de hello, pasar la base de datos de hello jobaccount como una llamada de creación de cuenta de trabajo de parámetro toohello.

## <a name="create-a-job-toodeploy-new-reference-data-tooall-tenants"></a>Crear un trabajo de los inquilinos tooall de datos nueva referencia toodeploy

Cada base de datos de inquilinos incluye un conjunto de tipos de ubicación que definen el tipo de saludo de eventos que se hospedan en un lugar. En este ejercicio, implementar un tipo de ubicación adicional actualización tooall Hola inquilino bases de datos tooadd dos: *motocicleta competir* y *natación Club*. Estos tipos de jurisdicción corresponden toohello imagen de fondo que se ven en la aplicación de eventos de hello inquilino.

Haga clic en el menú desplegable menú de tipo de ubicación de Hola y validar que están disponibles solo 10 opciones de tipo de ubicación y específicamente esa 'Motocicleta competir' y 'Natación Club' no están incluidos en la lista de Hola.

Ahora vamos a crear un Hola de trabajo tooupdate *VenueTypes* de tabla en todas las bases de datos de inquilino de Hola y agregar nuevos tipos de jurisdicción Hola.

toocreate un nuevo trabajo, se utiliza un conjunto de trabajos creados en la base de datos de hello jobaccount cuando se creó la cuenta de trabajo de Hola de procedimientos almacenados del sistema.

1. Abra SSMS y conectar el servidor de catálogo toohello: catálogo -\<usuario\>. database.windows.net server
1. Conecte también servidor de inquilinos de toohello: tenants1 -\<usuario\>. database.windows.net
1. Examinar toohello *contosoconcerthall* base de datos en hello *tenants1* Hola de servidor y consulta *VenueTypes* tooconfirm de tabla que *motocicleta competir*  y *natación Club* **no son** en la lista de resultados de Hola.
1. Archivo de hello abrir... \\Módulos de aprendizaje\\administración del esquema\\DeployReferenceData.sql
1. Modificar la instrucción de hello: establecer @wtpUser = &lt;usuario&gt; y sustituya el valor de usuario de hello usa al implementar la aplicación de Wingtip hello
1. Asegúrese de base de datos de jobaccount toohello conectado y presione **F5** para ejecutar el script de Hola

* **SP\_agregar\_destino\_grupo** crea el nombre de grupo de destino de hello DemoServerGroup, ahora tenemos tooadd miembros de destino.
* **SP\_agregar\_destino\_grupo\_miembro** agrega un *server* tipo de miembro que considere todas las bases de datos dentro de ese servidor (tenga en cuenta esto es hello tenants1-dedestino&lt; Usuario&gt; servidor que contiene las bases de datos del inquilino de Hola) en tiempo de trabajo de ejecución debe incluirse en el trabajo de hello, hello en segundo lugar está agregando un *base de datos* tienen como destino el tipo de miembro, específicamente Hola (base de datos 'maestra' basetenantdb) que reside en el catálogo -&lt;usuario&gt; server y por último otro *base de datos* destino grupo miembro tipo tooinclude hello adhocanalytics base de datos que se usa en un tutorial posterior.
* **sp\_add\_job** crea un trabajo llamado “Reference Data Deployment”.
* **SP\_agregar\_jobstep** crea Hola paso de trabajo que contiene la tabla de referencia en la Hola por tooupdate de texto de comando de T-SQL, VenueTypes
* Hola restantes en el script de Hola muestran existencia Hola de objetos de Hola y supervisar la ejecución de trabajo. Use este valor de estado de las consultas tooreview Hola Hola **ciclo de vida de** toodetermine de columna al trabajo de hello ha finalizado correctamente en todas las bases de datos de inquilino y Hola dos bases de datos adicionales que contiene la tabla de referencia de Hola.

1. En SSMS, busque toohello *contosoconcerthall* base de datos en hello *tenants1* Hola de servidor y consulta *VenueTypes* tooconfirm de tabla que *motocicleta Competir* y *natación Club* **son** ahora en la lista de resultados de Hola.


## <a name="create-a-job-toomanage-hello-reference-table-index"></a>Crear un índice de tabla de referencia de trabajo toomanage Hola

Similar toohello ejercicio anterior, este ejercicio crea un índice de hello toorebuild de trabajo en la clave principal de la tabla de referencia de hello, puede realizar una operación de administración de bases de datos habituales un administrador después de una carga de datos de gran tamaño en una tabla.

Crear un trabajo mediante Hola trabajos mismo 'sistema' procedimientos almacenados.

1. Abra SSMS y conéctese toohello catálogo -&lt;usuario&gt;. database.windows.net server
1. Archivo de hello abrir... \\Módulos de aprendizaje\\administración del esquema\\OnlineReindex.sql
1. Haga clic en, seleccione la conexión y conectarse toohello catálogo -&lt;usuario&gt;. database.windows.net server, si aún no está conectado
1. Asegúrese de que es la base de datos de jobaccount toohello conectado y presione script de Hola toorun F5

* sp\_add\_job crea un nuevo trabajo denominado “Online Reindex PK\_\_VenueTyp\_\_265E44FD7FD4C885”.
* SP\_agregar\_jobstep crea paso de trabajo de Hola que contiene código T-SQL comando texto tooupdate Hola índice




## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo:

> [!div class="checklist"]

> * Crear un tooquery de la cuenta de trabajo en varios inquilinos
> * Actualizar datos en todas las bases de datos de inquilino
> * Crear un índice en una tabla en todas las bases de datos de inquilino

[Tutorial de análisis ad hoc](sql-database-saas-tutorial-adhoc-analytics.md)


## <a name="additional-resources"></a>Recursos adicionales

* [Tutoriales adicionales que se basan en la implementación de aplicaciones de SaaS Wingtip Hola](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Administración de bases de datos escaladas horizontalmente en la nube](sql-database-elastic-jobs-overview.md)
* [Creación y administración de bases de datos escaladas horizontalmente](sql-database-elastic-jobs-create-and-manage.md)
