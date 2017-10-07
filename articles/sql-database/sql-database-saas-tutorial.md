---
title: "aaaDeploy y explore la aplicación de SaaS Wingtip multiempresa de Hola que utiliza la base de datos de SQL de Azure | Documentos de Microsoft"
description: "Implementar y explore la aplicación de varios inquilinos de SaaS Wingtip hello, que muestra los patrones de SaaS con la base de datos de SQL Azure."
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
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: 7c528ee19472d3b8c7a285b2f86013945e8f4bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-explore-a-multi-tenant-application-that-uses-azure-sql-database---wingtip-saas"></a>Implementación y exploración de una aplicación SaaS multiinquilino que usa Azure SQL Database

En este tutorial, implementar y explorar la aplicación de SaaS Wingtip hello. aplicación Hello usa un base de datos-por inquilino, patrón de aplicación de SaaS, tooservice varios inquilinos. aplicación Hello es características de tooshowcase diseño de base de datos de SQL Azure que simplifican la habilitar escenarios de SaaS.

Hola de cinco minutos después de hacer clic *implementar tooAzure* botón siguiente, tiene una aplicación de SaaS multiempresa, usando la base de datos de SQL, hasta y ejecutando en la nube de Hola. aplicación Hello se implementa con tres de los inquilinos de ejemplo, cada uno con su propia base de datos, todos los implementados en un grupo elástico de SQL. aplicación Hello es implementado tooyour suscripción de Azure, lo que le proporciona acceso completo tooexplore y trabajar con componentes de aplicaciones individuales de Hola. Hola aplicación origen código y administración de las secuencias de comandos están disponibles en hello repositorio WingtipSaaS GitHub.


En este tutorial, obtendrá información:

> [!div class="checklist"]

> * ¿Cómo toodeploy Hola aplicación Wingtip SaaS
> * Donde tooget Hola código fuente de aplicación y las secuencias de comandos de administración
> * Acerca de los servidores de hello, los grupos y las bases de datos que forman la aplicación hello
> * Cómo los inquilinos asignan datos tootheir con hello *catálogo*
> * ¿Cómo tooprovision un nuevo inquilino
> * ¿Cómo toomonitor inquilino actividad en la aplicación hello

tooexplore diferentes SaaS modelos de diseño y administración, un [serie de tutoriales relacionados](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials) está disponible que se basan en esta implementación inicial. Al pasar por los tutoriales de hello, profundizar en las secuencias de comandos de hello proporcionado y examinar cómo se implementan los patrones de SaaS diferentes Hola. Paso a paso a través de scripts de hello en cada tutorial toogain una comprensión más profunda cómo tooimplement Hola la base de datos de SQL muchas características que simplifican el desarrollo de aplicaciones de SaaS.

## <a name="prerequisites"></a>Requisitos previos

toocomplete se ha completado este tutorial, asegúrese de hello seguro después de requisitos previos:

* Azure PowerShell está instalado. Para más información, consulte [Introducción a Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).

## <a name="deploy-hello-wingtip-saas-application"></a>Implementar aplicaciones de SaaS Wingtip Hola

Implementar la aplicación de SaaS Wingtip hello:

1. Si hace clic en hello **implementar tooAzure** botón abre la plantilla de implementación de hello toohello portal Azure Wingtip SaaS. plantilla de Hello requiere dos valores de parámetro; un nombre para un nuevo grupo de recursos y un nombre de usuario que distingue esta implementación de otras implementaciones de aplicación de SaaS Wingtip hello. paso siguiente Hola proporciona detalles para establecer estos valores.

   Asegúrese de seguro toonote Hola exactamente los valores que use, ya que necesitará tooenter en una configuración de archivo más adelante.

   <a href="http://aka.ms/deploywtpapp" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

1. Escriba los valores de parámetro necesario para la implementación de hello:

    > [!IMPORTANT]
    > Para realizar la demostración, se ha eliminado intencionadamente la protección de varios firewalls de autenticación y del servidor. **Cree un nuevo grupo de recursos** y no use grupos de recursos, servidores o grupos existentes. No use esta aplicación, ni ninguno de los recursos que se crean, para producción. Eliminar este recurso del grupo cuando haya terminado con hello aplicación toostop relacionados con la facturación.

    * **Grupo de recursos** : seleccione esta opción **crear nuevo** y proporcionar un **nombre** Hola para grupo de recursos. Seleccione un **ubicación** de lista desplegable de Hola.
    * **Usuario**: algunos recursos requieren nombres que sean globalmente únicos. unicidad de tooensure, cada vez que implemente la aplicación hello proporcionar un valor de recursos de toodifferentiate que ha creado, de recursos creados por cualquier otra implementación de aplicación Wingtip Hola. Se recomienda un valor bajo toouse **usuario** nombre, como sus iniciales junto con un número (por ejemplo, *bg1*) y, a continuación, usarla en nombre de grupo de recursos de hello (por ejemplo, *wingtip-bg1*). El parámetro **Usuario** solo puede contener letras, números y guiones (sin espacios). Hello primero y último carácter debe ser una letra o un número (se recomienda todas las minúsculas).


1. **Implementar la aplicación hello**.

    * Haga clic en tooagree toohello términos y condiciones.
    * Haga clic en **Comprar**.

1. Supervisar el estado de implementación, haga clic en **notificaciones** (icono de campana Hola derecha del cuadro de búsqueda de hello). Implementar aplicaciones de SaaS Wingtip Hola tarda aproximadamente cinco minutos.

   ![implementación correcta](media/sql-database-saas-tutorial/succeeded.png)

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>Descargar y desbloquear scripts de SaaS Wingtip Hola

Mientras se está implementando la aplicación hello, descargar scripts de administración y el código de origen de Hola.

> [!IMPORTANT]
> Es posible que Windows bloquee el contenido ejecutable (scripts, archivos DLL) cuando se descarguen y extraigan archivos ZIP desde un origen externo. Al extraer los scripts de Hola desde un archivo zip, siga los pasos de Hola a continuación el archivo .zip de toounblock Hola antes de extraer. Esto garantiza que las secuencias de comandos de Hola se permiten toorun.

1. Examinar demasiado[repositorio de github de SaaS Wingtip hello](https://github.com/Microsoft/WingtipSaaS).
1. Haga clic en **Clone or download** (Clonar o descargar).
1. Haga clic en **Download ZIP** y guarde el archivo hello.
1. Menú contextual hello **WingtipSaaS master.zip** de archivos y seleccione **propiedades**.
1. En hello **General** ficha, seleccione **Unblock**y haga clic en **aplicar**.
1. Haga clic en **Aceptar**.
1. Extraiga los archivos de saludo.

Las secuencias de comandos se encuentran en hello *... \\WingtipSaaS master\\módulos de aprendizaje* carpeta.

## <a name="update-hello-configuration-file-for-this-deployment"></a>Actualizar archivo de configuración de Hola para esta implementación

Antes de ejecutar cualquier secuencia de comandos, establezca hello *grupo de recursos* y *usuario* valores en **UserConfig.psm1**. Establecer valores toohello establecidos durante la implementación de estas variables.

1. Abra... \\Módulos de aprendizaje\\*UserConfig.psm1* en hello *PowerShell ISE*
1. Actualización *ResourceGroupName* y *nombre* con valores específicos de hello para la implementación (en líneas 10 y 11 solo).
1. ¡Guardar los cambios de Hola!

Si se define aquí simplemente evita tener tooupdate estos valores específicos de la implementación en todos los scripts.

## <a name="run-hello-application"></a>Ejecutar la aplicación hello

aplicación Hello muestra lugares, como salas de concierto, tréboles jazz, deportes tréboles, que hospedan los eventos. Recintos registrar como clientes (o inquilinos) de plataforma de Wingtip hello, para eventos de toolist fácilmente y venden entradas. Cada lugar obtiene una toomanage de aplicación web personalizado y enumerar a sus eventos y vender vales, independientes y aislados de otros inquilinos. Tras bastidores de hello, cada inquilino Obtiene una base de datos SQL que se implementa en un grupo elástico de SQL.

Un centro de **concentrador de eventos** proporciona una lista del inquilino de implementación de tooyour específico de direcciones URL.

1. Abra hello _concentrador de eventos_ en el explorador web: http://events.wtp.&lt; USUARIO&gt;. trafficmanager.net (reemplazar por el nombre de usuario de su implementación):

    ![events hub](media/sql-database-saas-tutorial/events-hub.png)

1. Haga clic en **Fabrikam Jazz Club** en el *centro de eventos*.

   ![Eventos](./media/sql-database-saas-tutorial/fabrikam.png)


distribución de hello toocontrol de las solicitudes entrantes, usos de aplicación Hola [ *Azure Traffic Manager*](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview). páginas de eventos de Hello, que son específicos del inquilino, requieren que se incluyen nombres de inquilino en hello las direcciones URL. Hola a todos los inquilinos las direcciones URL incluyen específica de su *usuario* valor y seguir este formato: http://events.wtp.&lt; USUARIO&gt;.trafficmanager.net/*fabrikamjazzclub*. aplicación de eventos de Hello analiza el nombre del inquilino Hola de dirección URL de Hola y usa una clave tooaccess un catálogo mediante toocreate [ *administración de mapa de particiones*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-scale-shard-map-management). Hola ubicación de base de datos del inquilino de catálogo mapas hello toohello clave. Hola **concentrador de eventos** usa metadatos extendidos en nombre del inquilino de hello catálogo tooretrieve Hola asociado a cada lista de hello tooprovide de base de datos de direcciones URL.

En un entorno de producción, normalmente se crearía un registro CNAME DNS para [ *apuntar un dominio de internet de la empresa* ](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-point-internet-domain) perfil del Administrador de tráfico de Hola.

## <a name="start-generating-load-on-hello-tenant-databases"></a>Iniciar la generación de carga en las bases de datos del inquilino de Hola

Ahora que hello aplicación se implementa, vamos a colocarla toowork! Hola *LoadGenerator demostración* script de PowerShell inicia una carga de trabajo que se ejecutan en todas las bases de datos de inquilino. carga de Hola mundo real en muchas aplicaciones de SaaS normalmente es esporádico e imprevisibles. toosimulate este tipo de carga, el generador de hello genera una carga que se distribuye entre todos los inquilinos, con ráfagas aleatorios en cada inquilino que se producen en intervalos aleatorios. Por este motivo tarda varios minutos para tooemerge de patrón de carga de hello, por lo que es mejor generador de hello toolet ejecutar para al menos tres o cuatro minutos antes de supervisión Hola de carga.

1. Hola *PowerShell ISE*, abra Hola... \\Módulos de aprendizaje\\utilidades\\*LoadGenerator.ps1 demostración* secuencia de comandos.
1. Presione **F5** para ejecutar el script de Hola e iniciar el generador de carga de hello (deje Hola valores de parámetros predeterminados por ahora).

> [!IMPORTANT]
> toorun otras secuencias de comandos, abra una nueva ventana de PowerShell ISE. Generador de carga de saludo se está ejecutando como una serie de trabajos en la sesión de PowerShell local. Hola *LoadGenerator.ps1 demostración* script inicia Hola carga real generador de comandos, que se ejecuta como una serie de trabajos en segundo plano generación de carga más de una tarea en primer plano. Un trabajo del generador de carga se invoca para cada base de datos registrado en el catálogo de Hola. Hola trabajos en ejecución en la sesión de PowerShell local, por lo que cerrar sesión de PowerShell de hello deja todos los trabajos. Si se suspende el equipo, se pausa la generación de carga y se reanudará cuando reactive el equipo.

Una vez que el generador de carga de hello invoca trabajos de generación de carga para cada inquilino, tarea de primer plano de hello permanece en un estado de invocación de trabajo, donde se inicia trabajos en segundo plano adicionales para los nuevos inquilinos proporcionados posteriormente. Puede usar *Ctrl-C* o presione hello *detener* tarea de primer plano de botón toostop hello, pero fondo existente los trabajos continuarán generar carga en cada base de datos. Si necesita toomonitor y controlar los trabajos en segundo plano hello, use *Get-Job*, *Receive-Job* y *Stop-Job*. Mientras está ejecutando tarea de primer plano de hello no se use Hola mismo tooexecute de sesión de PowerShell otras secuencias de comandos. toorun otras secuencias de comandos, abra una nueva ventana de PowerShell ISE.

Si desea que la sesión del generador de carga de toorestart hello, por ejemplo con parámetros diferentes, puede detener tarea de primer plano de hello y, a continuación, vuelva a ejecutar hello *LoadGenerator.ps1 demostración* secuencia de comandos. Volver a ejecutar *LoadGenerator.ps1 demostración* primero detiene cualquier actualmente ejecuta trabajos y, a continuación, el generador de Hola de reinicios, que inicia un nuevo conjunto de trabajos con los parámetros actuales de Hola.

Por ahora, déjelo generador de carga de hello ejecutando en el estado de invocación de trabajo Hola.


## <a name="provision-a-new-tenant"></a>Aprovisionamiento de un nuevo inquilino

implementación inicial de Hello crea tres de los inquilinos de ejemplo, pero vamos a crear otro toosee inquilino cómo esto afecta a la aplicación hello implementado. flujo de trabajo de Hello inquilinos el aprovisionamiento de Wingtip SaaS se detalla en hello [tutorial aprovisionar y catálogo](sql-database-saas-tutorial-provision-and-catalog.md). En este paso, se crea rápidamente un inquilino.

1. Abra... \\Modules\Provision de aprendizaje y catálogo\\*demostración ProvisionAndCatalog.ps1* en hello *PowerShell ISE*.
1. Presione **F5** para ejecutar el script de Hola (deje Hola predeterminada valores por ahora).

   > [!NOTE]
   > Usan muchas secuencias de comandos de SaaS Wingtip *$PSScriptRoot* tooallow navegar por las funciones de toocall de carpetas en otros scripts. Esta variable se evalúa solo cuando se ejecuta el script de Hola presionando **F5**.  Resaltar y ejecutar una selección (**F8**) puede dar lugar a errores, por tanto, presione **F5** al ejecutar los scripts.

base de datos nuevos inquilinos Hola se crea en un grupo elástico de SQL, inicializado y registra en el catálogo de Hola. Después de aprovisionar correcta, nuevo inquilino de hello del vale de venta *eventos* sitio aparece en el explorador:

![Nuevo inquilino](./media/sql-database-saas-tutorial/red-maple-racing.png)

Actualizar hello *concentrador de eventos* y nuevo inquilino de hello ahora no aparece en la lista de Hola.


## <a name="explore-hello-servers-pools-and-tenant-databases"></a>Explorar servidores hello, grupos y las bases de datos de inquilinos

Ahora que ha iniciado la ejecución de una carga en colección Hola de inquilinos, echemos un vistazo a algunos de los recursos de Hola que se implementaron:

1. En el [portal de Azure](http://portal.azure.com), busque tooyour lista de servidores SQL Server y abra el **catálogo -&lt;usuario&gt;**  server. servidor de catálogo de Hello contiene dos bases de datos. Hola **tenantcatalog**, hello y **basetenantdb** (vacío *dorada* o copia de base de datos de plantilla que está toocreate nuevos inquilinos).

   ![bases de datos](./media/sql-database-saas-tutorial/databases.png)

1. Vuelva tooyour lista de servidores SQL Server y abra hello **tenants1 -&lt;usuario&gt;**  servidor que hospeda las bases de datos del inquilino de Hola. Todas las bases de datos de inquilinos son _elásticas estándar_ en un conjunto estándar de 50 eDTU. Observe también hay un _arce rojo competir_ base de datos, base de datos de inquilinos de hello ha aprovisionado anteriormente.

   ![Servidor](./media/sql-database-saas-tutorial/server.png)

## <a name="monitor-hello-pool"></a>Grupo de Hola de Monitor

Si se ha ejecutado el generador de carga de Hola durante varios minutos, suficiente datos deben estar disponible toostart observar algunos de hello las funciones integradas en grupos y las bases de datos de seguimiento.

1. Examinar el servidor de toohello **tenants1 -&lt;usuario&gt;**y haga clic en **Pool1** para ver el uso de recursos para el grupo de hello (generador de carga de Hola se ejecutó durante una hora en hello después de gráficos) :

   ![supervisar grupo](./media/sql-database-saas-tutorial/monitor-pool.png)

Estos dos gráficos ilustran es el grado de idoneidad de los grupos elásticos y de SQL Database para las cargas de trabajo de una aplicación SaaS. Cuatro bases de datos que están entre irrupción tooas hasta 40 Edtu fácilmente admitidos en un grupo de eDTU de 50. Si ya se han aprovisionado como bases de datos independiente, desean contar con cada toobe necesita un S2 (50 DTU) toosupport Hola ráfagas. costo de Hola de bases de datos de 4 independiente S2 sería precio de hello casi 3 veces de grupo de Hola y grupo Hola todavía tiene una gran cantidad de espacio en cabeza para muchas bases de datos más. En situaciones del mundo real, los clientes de la base de datos SQL se están ejecutando actualmente seguridad too500 bases de datos en grupos de eDTU 200. Para obtener más información, vea hello [tutorial de supervisión de rendimiento](sql-database-saas-tutorial-performance-monitoring.md).


## <a name="next-steps"></a>Pasos siguientes

En este tutorial ha obtenido información:

> [!div class="checklist"]

> * ¿Cómo toodeploy Hola aplicación Wingtip SaaS
> * Acerca de los servidores de hello, los grupos y las bases de datos que forman la aplicación hello
> * Los inquilinos son datos tootheir asignada con hello *catálogo*
> * ¿Cómo tooprovision nuevos inquilinos
> * ¿Cómo tooview grupo uso toomonitor inquilino actividad
> * ¿Cómo toostop de recursos de ejemplo toodelete relacionados con la facturación

Ahora, intente hello [tutorial aprovisionar y catálogo](sql-database-saas-tutorial-provision-and-catalog.md)



## <a name="additional-resources"></a>Recursos adicionales

* Adicionales [tutoriales que se basan en Hola aplicación Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* toolearn sobre grupos elásticos, consulte [ *¿qué es un grupo elástico de SQL Azure*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool)
* toolearn acerca de los trabajos elásticos, consulte [ *bases de datos de escala horizontal en la nube de administración*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)
* toolearn acerca de las aplicaciones SaaS de varios inquilinos, consulte [ *diseñar modelos para las aplicaciones SaaS de varios inquilinos*](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)
