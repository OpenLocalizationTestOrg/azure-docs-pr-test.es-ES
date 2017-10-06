---
title: "aaaProvision nuevos inquilinos en una aplicación de varios inquilinos que usa la base de datos de SQL de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooprovision y catálogo de nuevo los inquilinos Hola aplicación Wingtip SaaS"
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
ms.date: 08/11/2017
ms.author: sstein
ms.openlocfilehash: eb26f523305650c2124e36707d187dfcdad06fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="provision-new-tenants-and-register-them-in-hello-catalog"></a>Aprovisionar nuevos inquilinos y registrarlos en el catálogo de Hola

En este tutorial, aprenderá sobre aprovisionar hello y patrones de SaaS de catálogo y cómo se implementan en hello aplicación SaaS Wingtip. Crear, inicializar nuevas bases de datos de inquilino y registrarlos en el catálogo de la aplicación hello inquilino. catálogo de Hello es una base de datos que mantiene la asignación de hello entre varios inquilinos de la aplicación de SaaS hello y sus datos. catálogo de Hello desempeña un papel importante dirigir la base de datos de aplicación solicitudes toohello correcta.  

En este tutorial, aprenderá a:

> [!div class="checklist"]

> * Aprovisionar un nuevo inquilino único, incluidos todos los pasos de su implementación
> * Aprovisionar un lote de inquilinos adicionales


toocomplete se ha completado este tutorial, asegúrese de hello seguro después de requisitos previos:

* se implementa la aplicación de SaaS Wingtip Hello. vea toodeploy en menos de cinco minutos, [implementar y explorar la aplicación de SaaS Wingtip hello](sql-database-saas-tutorial.md)
* Azure PowerShell está instalado. Para más información, consulte [Introducción a Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).

## <a name="introduction-toohello-saas-catalog-pattern"></a>Introducción toohello patrón de catálogo de SaaS

En una aplicación de SaaS multiempresa de seguridad de base de datos, es importante tooknow donde se almacena información para cada inquilino. En el patrón de catálogo de SaaS hello, una base de datos de catálogo es toohold usado Hola asignación entre cada inquilino y donde se almacenan sus datos. aplicación de SaaS Wingtip Hello usa a un único inquilino por arquitectura de base de datos, pero patrón básico de Hola de almacenar la asignación de inquilino a base de datos en un catálogo se aplica si se utiliza una base de datos de inquilino único o múltiple.

Cada inquilino se asigna una clave que identifica a ellos en el catálogo de Hola y que se asigna toohello ubicación de base de datos adecuado de Hola. En la aplicación de SaaS Wingtip hello, clave de hello está formado de un código hash del nombre del inquilino de Hola. Esto permite utiliza de parte del nombre de inquilino de Hola de toobe de dirección URL de aplicación Hola clave de hello tooconstruct. También se podrían utilizar otros esquemas de claves de inquilino.  

catálogo de Hello permite Hola nombre o la ubicación de hello toobe de base de datos cambiado con un impacto mínimo en la aplicación hello.  En un modelo de base de datos multiinquilino, esto también permite mover a un inquilino entre bases de datos.  catálogo de Hello también puede ser usado tooindicate si un inquilino o base de datos está sin conexión durante el mantenimiento u otras acciones. Esto se explora en hello [restaurar tutorial de un solo inquilino](sql-database-saas-tutorial-restore-single-tenant.md).

Además, catálogo de hello, que está en vigor una base de datos de administración de una aplicación SaaS, puede almacenar metadatos de inquilino o base de datos adicionales, como Hola capa o edición de una base de datos, la versión del esquema, el plan de servicio o SLA que ofrece tootenants y otra información que permite la administración de aplicaciones, soporte al cliente o los procesos de devops.  

Más allá de hello aplicación SaaS, catálogo Hola puede permitir a las herramientas de base de datos.  En el ejemplo de Hola a Wingtip SaaS, catálogo de hello es consulta entre inquilinos de tooenable usado, explorada en hello [tutorial de análisis ad hoc](sql-database-saas-tutorial-adhoc-analytics.md). Administración del trabajo entre bases de datos se explora en hello [administración del esquema](sql-database-saas-tutorial-schema-management.md) y [inquilino análisis](sql-database-saas-tutorial-tenant-analytics.md) tutoriales. 

En la aplicación de SaaS Wingtip hello, catálogo Hola se implementa mediante características de administración de particiones de Hola de hello [biblioteca de cliente de base de datos elástica (EDCL)](sql-database-elastic-database-client-library.md). Hola EDCL habilita una aplicación toocreate, administrar y usar un mapa de particiones de seguridad de base de datos. Un mapa de particiones contiene una lista de particiones (bases de datos) y asignación de hello entre bases de datos y claves (inquilinos).  Funciones EDCL se puedan usar desde aplicaciones o scripts de PowerShell durante las entradas de hello toocreate en mapa de particiones de Hola de aprovisionamiento del inquilino y desde las aplicaciones tooefficiently conectan toohello base de datos correcta. Se almacena en caché en EDCL conexión información toominimize Hola tráfico toohello catálogo base de datos y acelerar la aplicación hello.  

> [!IMPORTANT]
> los datos de asignación de Hello están accesibles en la base de datos de catálogo de hello, pero *no editarlo*! Para editar datos de asignación, utilice únicamente las API de la biblioteca de cliente de Elastic Database. Manipular directamente los datos de asignación de hello riesgos Hola de daño de catálogo y no se admiten.


## <a name="introduction-toohello-saas-provisioning-pattern"></a>Patrón de aprovisionamiento de SaaS toohello de introducción

Durante la incorporación de un nuevo inquilino a una aplicación SaaS que usa el modelo de base de datos de un solo inquilino, se debe aprovisionar una nueva base de datos de inquilino.  Debe crearse en la ubicación adecuada de Hola y de nivel de servicio, inicializado con los datos de referencia y el esquema adecuado y después se registran en el catálogo de hello bajo la clave de inquilino adecuado de Hola.  

Distintos enfoques pueden ser usado toodatabase aprovisionamiento, lo que podría incluir la ejecución de scripts SQL, la implementación de un bacpac o copiar una base de datos 'maestra' plantilla.  

debe se ha comprendido Hola aprovisionamiento del método que utilice en su estrategia general de administración de esquema, que debe asegurarse de que se ha aprovisionado nuevas bases de datos con el esquema más reciente de Hola.  Esto se explora en hello [tutorial de administración de esquema](sql-database-saas-tutorial-schema-management.md).  

Hola Wingtip SaaS aplicación aprovisiona nuevos inquilinos mediante la copia de una base de datos maestra con el nombre basetenantdb, implementada en el servidor de catálogo Hola.  Aprovisionamiento podría se integra en la aplicación hello como parte de una experiencia de inicio de sesión o admiten sin conexión con las secuencias de comandos. Este tutorial describe el aprovisionamiento con PowerShell. scripts de aprovisionamiento de Hello copiar hello basetenantdb toocreate una nueva base de datos de inquilinos en un grupo elástico, a continuación, inicializarlo con información específica del inquilino y registrarlo en mapa de particiones del catálogo de Hola.  En la aplicación de ejemplo de Hola, las bases de datos se les asignan nombres basados en nombre del inquilino de hello, pero esto no es una parte fundamental del modelo de hello: uso de Hola de catálogo de hello permite cualquier base de datos de nombre toobe asignado toohello. + 


## <a name="get-hello-wingtip-application-scripts"></a>Obtener scripts de la aplicación hello Wingtip

Hello Wingtip SaaS scripts y código fuente de aplicación están disponibles en hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositorio de github. [Pasos de secuencias de comandos de toodownload Hola Wingtip SaaS](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).


## <a name="provision-and-catalog-detailed-walkthrough"></a>Tutorial detallado de aprovisionamiento y catalogación

toounderstand cómo Hola Wingtip aplicación implementa nuevo inquilino de aprovisionamiento, agregue un punto de interrupción y recorrer el flujo de trabajo de Hola durante el aprovisionamiento de un inquilino:

1. Abra... \\Módulos de aprendizaje\\ProvisionAndCatalog\\_ProvisionAndCatalog.ps1 demostración_ y Hola de conjunto de parámetros siguientes:
   * **$TenantName** = nombre de Hola de nuevo escenario de hello (por ejemplo, *Bushwillow Blues*).
   * **$VenueType** = uno de los tipos de ubicación predefinida de hello: *blues*, classicalmusic, fiesta, jazz, judo, motorracing, multipropósito, opera, rockmusic, fútbol.
   * **$DemoScenario** = **1**, establezca demasiado**1** demasiado*aprovisionar un solo inquilino*.

1. Agregar un punto de interrupción, coloque el cursor en cualquier lugar en línea hello 48, línea que dice: *nuevo inquilino '*y presione **F9**.

   ![punto de interrupción](media/sql-database-saas-tutorial-provision-and-catalog/breakpoint.png)

1. Presione de script de Hola toorun **F5**.

1. Después de la ejecución de script de Hola se detiene en el punto de interrupción de hello, presione **F11** toostep en código de hello.

   ![punto de interrupción](media/sql-database-saas-tutorial-provision-and-catalog/debug.png)



Seguimiento de ejecución del script de Hola mediante hello **depurar** opciones de menú - **F10** y **F11** toostep sobre o en hello llamada a funciones. Para obtener más información sobre cómo depurar scripts de PowerShell, consulte [Sugerencias para trabajar con scripts de PowerShell y depurarlos](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise).


siguiente Hello no es pasos seguir tooexplicitly, sino una explicación del flujo de trabajo de hello que recorre paso a paso durante la depuración de script de Hola:

1. **Hola de importación SubscriptionManagement.psm1** módulo que contiene funciones para iniciar sesión en tooAzure y seleccionando Hola suscripción de Azure que está trabajando.
1. **Hola de importación CatalogAndDatabaseManagement.psm1** módulo que proporciona un catálogo y el nivel del inquilino abstracción sobre hello [administración de particiones](sql-database-elastic-scale-shard-map-management.md) funciones. Se trata de un módulo importante que encapsula gran parte del patrón de catálogo de Hola y merece la pena mencionar.
1. **Obtenga los detalles de configuración**. Ir a Get-configuración (F11) y vea cómo se especifica la configuración de aplicación Hola. Los nombres de recursos y otros valores específicos de la aplicación se definen aquí, pero no cambiar ninguno de estos valores hasta que esté familiarizado con las secuencias de comandos de Hola.
1. **Obtener objetos de catálogo de hello**. Ir a Get-catálogo que crea y devuelve un objeto de catálogo que se usa en el script de nivel superior de Hola.  Esta función utiliza las funciones de administración de particiones que se importan desde **AzureShardManagement.psm1**. objeto de catálogo de Hola se compone de siguiente hello:
   * $catalogServerFullyQualifiedName se construye utilizando troncal estándar hello más el nombre de usuario: _catálogo -\<usuario\>. database.windows.net_.
   * $catalogDatabaseName se recuperan desde la configuración de hello: *tenantcatalog*.
   * se inicializa el objeto de $shardMapManager de base de datos de catálogo de Hola.
   * objeto $shardMap se inicializa desde hello *tenantcatalog* mapa de particiones en la base de datos de catálogo de Hola.
   Un objeto de catálogo está compuesto por y devuelve y utilizan en script un nivel más alto de Hola.
1. **Calcular la nueva clave de inquilino hello**. Una función hash es clave de inquilino de hello toocreate usado de nombre del inquilino Hola.
1. **Comprobar si ya existe la clave de inquilino de hello**. catálogo de Hola se comprueba la clave de hello tooensure está disponible.
1. **base de datos de inquilinos de Hola se aprovisiona con New-TenantDatabase.** Use **F11** toostep en y ver cómo es la base de datos de hello aprovisionado con un [plantilla de Azure Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).

nombre de la base de datos de Hola se construye a partir de hello inquilino nombre toomake claro qué partición pertenece a toowhich inquilino. (Fácilmente se podrían usar otras estrategias para asignar nombres a base de datos.) + Una plantilla de administrador de recursos es toocreate usa una base de datos de inquilinos mediante la copia de una base de datos maestra (baseTenantDB) en el servidor de catálogo Hola. Un enfoque alternativo podría ser toocreate una base de datos vacía y e inicializarlo después mediante la importación de un bacpac o tooexecute un script de inicialización desde una ubicación conocida.  

plantilla del Administrador de recursos de Hola está en la carpeta de hello ...\Learning Modules\Common\: *tenantdatabasecopytemplate.json*

Después de crea la base de datos de inquilinos de hello, a continuación, resulta más **inicializa con el nombre de lugar (inquilino) de Hola y el tipo de ubicación de hello**. Aquí también podría realizarse otro tipo de inicialización.

Hola **base de datos de inquilino está registrado en el catálogo de hello** con *TenantDatabaseToCatalog agregar* con clave de inquilino de Hola. Use **F11** toostep en los detalles de hello:

* base de datos de catálogo de Hola se agrega el mapa de particiones toohello (lista de Hola de bases de datos conocidos).
* Hola asignación de esa partición de toohello vínculos Hola clave-valor se crea.
* Metadatos adicionales (nombre del lugar de hello) acerca de inquilino de Hola se agregan toohello tabla de los inquilinos en el catálogo de Hola.  tabla de inquilinos de Hello no forma parte del esquema de ShardManagement Hola y Hola EDCL no lo instala.  Esta tabla muestra cómo puede extenderse a base de datos de catálogo de hello datos de toosupport adicionales específicos de la aplicación.   


Después de que finalice el aprovisionamiento, ejecución devuelve toohello original *demostración ProvisionAndCatalog* secuencia de comandos, que abre hello **eventos** página para nuevo inquilino de hello en el Explorador de hello:

   ![events](media/sql-database-saas-tutorial-provision-and-catalog/new-tenant.png)


## <a name="provision-a-batch-of-tenants"></a>Aprovisionamiento de un lote de inquilinos

Este ejercicio aprovisiona un lote de 17 inquilinos. Se recomienda que proporcionar este lote de inquilinos antes de iniciar otros tutoriales Wingtip SaaS, así que no hay más de unos pocos toowork de bases de datos con.

1. Abra... \\Módulos de aprendizaje\\ProvisionAndCatalog\\*demostración ProvisionAndCatalog.ps1* en hello *PowerShell ISE* y cambiar hello *$ DemoScenario* too3 de parámetro:
   * **$DemoScenario** = **3**, también cambian**3** demasiado*aprovisionar un lote de inquilinos*.
1. Presione **F5** y ejecute el script de Hola.

script de Hola implementa un lote de inquilinos adicionales. Usa un [plantilla de Azure Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md) que controla el lote de hello y, a continuación, los delegados de aprovisionamiento de cada plantilla vinculada de tooa de base de datos. Uso de plantillas de esta manera permite Azure Resource Manager toobroker Hola proceso para su script de aprovisionamiento. Plantillas de aprovisionar bases de datos en paralelo donde puede y manejar los reintentos si es necesario, optimizar el proceso general de Hola. Hola script es idempotente por lo que si se produce un error o se detiene por alguna razón, vuelva a ejecutarlo.

### <a name="verify-hello-batch-of-tenants-successfully-deployed"></a>Compruebe el lote de Hola de inquilinos que se implementó correctamente

* Abra hello *tenants1* servidor examinando tooyour lista de servidores en hello [portal de Azure](https://portal.azure.com), haga clic en **bases de datos SQL**y compruebe el lote de Hola de 17 bases de datos adicionales están ahora en la lista de hello:

   ![lista de base de datos](media/sql-database-saas-tutorial-provision-and-catalog/database-list.png)



## <a name="other-provisioning-patterns"></a>Otros patrones de aprovisionamiento

Entre los patrones de aprovisionamiento que no se describen en este tutorial se incluyen los siguientes:

**Aprovisionamiento previo de bases de datos.** Hola previamente aprovisionamiento patrón aprovecha el hecho de Hola que las bases de datos en un grupo elástico no agregan costos adicionales. La facturación es para el grupo elástico hello, no Hola bases de datos y las bases de datos inactivas no consuman ningún recurso. Al aprovisionar previamente bases de datos en un grupo y asignarlas posteriormente cuando sea necesario, puede reducirse considerablemente el tiempo de incorporación del inquilino. número de Hola de bases de datos que se suministran previamente pudo ajustará como tookeep necesitan un búfer adecuado para hello prever la velocidad de aprovisionamiento.

**Aprovisionamiento automático** En el patrón de aprovisionamiento automático de hello, un servicio de aprovisionamiento dedicado es tooprovision usa servidores, los grupos y las bases de datos automáticamente según sea necesario, incluidas bases de datos previamente aprovisionamiento en grupos elásticos si lo desea. Y si las bases de datos se encargó anular y se elimina, deficiencias en grupos elásticos pueden ser completadas por hello aprovisionamiento del servicio según sea necesario. Este servicio puede ser simple o complejo; por ejemplo, puede controlarse el aprovisionamiento en varias regiones geográficas y configurarse automáticamente la replicación geográfica si se utiliza dicha estrategia para la recuperación ante desastres. Con el patrón de aprovisionamiento automático de hello, una aplicación cliente o la secuencia de comandos podría enviar un aprovisionamiento toobe de cola de tooa de solicitud procesada por hello aprovisionamiento del servicio y, a continuación, podría sondear realización de toodetermine del servicio de Hola. Si se utiliza el aprovisionamiento previamente, se podrían administrar las solicitudes rápidamente con servicio de hello administra el aprovisionamiento de una base de datos de reemplazo que se ejecuta en segundo plano de Hola.



## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo:

> [!div class="checklist"]

> * Aprovisionar un nuevo inquilino único
> * Aprovisionar un lote de inquilinos adicionales
> * Ir a detalles de Hola de aprovisionamiento de los inquilinos y registrarlos en el catálogo de Hola

Intente hello [tutorial de supervisión de rendimiento](sql-database-saas-tutorial-performance-monitoring.md).

## <a name="additional-resources"></a>Recursos adicionales

* Adicionales [tutoriales que parten Hola aplicación Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Biblioteca de cliente de base de datos elástica](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-database-client-library)
* [Cómo tooDebug Scripts en Windows PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise)
