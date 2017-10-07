---
title: "aaaIntro Wingtip SaaS: aplicación de varios inquilinos de base de datos de SQL de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de mediante el uso de una aplicación de varios inquilinos de ejemplo que utiliza la base de datos de SQL de Azure, aplicación de SaaS Wingtip hello"
keywords: tutorial de SQL Database
services: sql-database
author: stevestein
manager: jhubbard
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: sstein
ms.openlocfilehash: daeed293116fca22718831b780533be6ef2ad178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-wingtip-saas-application"></a>Introducción toohello aplicación Wingtip SaaS

Hola *Wingtip SaaS* aplicación es una aplicación de varios inquilinos de ejemplo que muestra hello ventajas únicas derivadas de base de datos SQL. aplicación Hello usa un base de datos-por inquilino, patrón de aplicación de SaaS, tooservice varios inquilinos. aplicación Hello es tooshowcase diseñada características de base de datos de SQL Azure que permiten escenarios de SaaS, incluidos varios patrones de diseño y administración de SaaS. desarrollar tooquickly y en ejecución, implementa la aplicación de SaaS Wingtip hello en menos de cinco minutos.

Scripts de administración y el código de origen de aplicaciones están disponibles en hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositorio de github. secuencias de comandos de hello toorun, [descargar la carpeta de módulos de aprendizaje de hello](#download-and-unblock-the-wingtip-saas-scripts) tooyour de equipo local.

## <a name="sql-database-wingtip-saas-tutorials"></a>Tutoriales de SaaS de Wingtip de SQL Database

Después de implementar la aplicación hello, explorar Hola tutoriales que se basan en la implementación inicial de Hola. En estos tutoriales se exploran patrones comunes de SaaS que aprovechan las ventajas de las características integradas de SQL Database, SQL Data Warehouse y otros servicios de Azure. Tutoriales incluyen scripts de PowerShell, con explicaciones detalladas que simplifican considerablemente la descripción, e implementar Hola mismos patrones de administración de SaaS en sus aplicaciones.


| Tutorial | Descripción |
|:--|:--|
|[Implementar y explorar la aplicación de SaaS Wingtip hello](sql-database-saas-tutorial.md)| **COMIENCE AQUÍ.** Implementar y explore Hola Wingtip SaaS aplicación tooyour suscripción de Azure. |
|[Aprovisionamiento y registro de inquilinos en el catálogo](sql-database-saas-tutorial-provision-and-catalog.md)| Obtenga información acerca de la aplicación hello conecta tootenants con una base de datos de catálogo, y cómo se asigna el catálogo de hello los inquilinos tootheir datos. |
|[Supervisión y administración del rendimiento](sql-database-saas-tutorial-performance-monitoring.md)| Obtenga información acerca de cómo las características de supervisión de toouse de base de datos SQL y cómo tooset alertas cuando se superan los umbrales de rendimiento. |
|[Supervisión con Log Analytics (OMS)](sql-database-saas-tutorial-log-analytics.md) | Obtenga información acerca del uso de [análisis de registros](../log-analytics/log-analytics-overview.md) toomonitor grandes cantidades de recursos entre varios grupos. |
|[Restauración de un solo inquilino](sql-database-saas-tutorial-restore-single-tenant.md)| Obtenga información acerca de cómo toorestore un tooa de base de datos de inquilino anterior al momento dado. Pasos toorestore tooa bases de datos paralelas, dejando Hola inquilino base de datos existente en línea, también se incluyen. |
|[Administración de esquemas de inquilino](sql-database-saas-tutorial-schema-management.md)| Obtenga información acerca de cómo tooupdate esquema y actualizar los datos de referencia entre todos los inquilinos de Wingtip SaaS. |
|[Ejecución de análisis ad hoc](sql-database-saas-tutorial-adhoc-analytics.md) | Cree una base de datos de análisis ad hoc y ejecute consultas distribuidas en tiempo real en todos los inquilinos.  |
|[Ejecución de análisis de inquilino](sql-database-saas-tutorial-tenant-analytics.md) | Extraiga datos de inquilino a una base de datos de análisis o un almacén de datos para ejecutar consultas analíticas sin conexión. |



## <a name="application-architecture"></a>Arquitectura de la aplicación

aplicación de SaaS Wingtip Hello usa el modelo de base de datos por inquilino hello y utiliza la eficacia de toomaximize grupos elásticos de SQL. Para el aprovisionamiento y la asignación de datos de los inquilinos tootheir, se utiliza una base de datos de catálogo. aplicación de SaaS Wingtip de núcleo de Hello, utiliza un grupo con tres inquilinos de ejemplo, además de Hola catálogo de base de datos. Completar muchas de hello Wingtip SaaS tutoriales dar lugar a la implementación inicial de complementos toohello, mediante la introducción de las bases de datos analíticos, entre bases de datos administración de esquemas, etcetera.


![Arquitectura de SaaS Wingtip](media/sql-database-wtp-overview/app-architecture.png)


Al pasar por los tutoriales de Hola y trabajar con la aplicación hello, es importante toofocus sobre los patrones de SaaS Hola tal y como se relacionan con la capa de datos de toohello. En otras palabras, se centran en la capa de datos de Hola y más no analizar la propia aplicación Hola. Descripción de implementación de Hola de estos patrones de SaaS es clave tooimplementing estos patrones en las aplicaciones, teniendo en cuenta las modificaciones necesarias para sus requisitos empresariales específicos.

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>Descargar y desbloquear scripts de SaaS Wingtip Hola

Es posible que Windows bloquee el contenido ejecutable (scripts, archivos DLL) cuando se descarguen y extraigan archivos ZIP desde un origen externo. Al extraer los scripts de Hola desde un archivo zip, ***siga los pasos de Hola a continuación el archivo .zip de toounblock Hola antes de extraer***. Esto garantiza que las secuencias de comandos de Hola se permiten toorun.

1. Examinar demasiado[repositorio de github de SaaS Wingtip hello](https://github.com/Microsoft/WingtipSaaS).
1. Haga clic en **Clone or download** (Clonar o descargar).
1. Haga clic en **Download ZIP** y guarde el archivo hello.
1. Menú contextual hello **WingtipSaaS master.zip** de archivos y seleccione **propiedades**.
1. En hello **General** ficha, seleccione **Unblock**.
1. Haga clic en **Aceptar**.
1. Extraiga los archivos de saludo.

Las secuencias de comandos se encuentran en hello *... \\WingtipSaaS master\\módulos de aprendizaje* carpeta.


## <a name="working-with-hello-wingtip-saas-powershell-scripts"></a>Trabajar con Scripts de PowerShell de SaaS Wingtip Hola

Hola tooget más fuera del ejemplo de Hola necesita toodive en scripts de hello proporcionado. Utilizar puntos de interrupción y siga los pasos de secuencias de comandos de hello, examina los detalles de Hola de cómo se implementan los patrones de SaaS diferentes Hola. tooeasily recorrer Hola proporciona scripts y módulos para comprender mejor, se recomienda usar Hola de hello [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).

### <a name="update-hello-configuration-file-for-your-deployment"></a>Actualizar archivo de configuración de hello para la implementación

Editar hello **UserConfig.psm1** archivo con hello grupos y usuarios valor del recurso que establece durante la implementación:

1. Abra hello *PowerShell ISE* y cargar... \\Módulos de aprendizaje\\*UserConfig.psm1* 
1. Actualización *ResourceGroupName* y *nombre* con valores específicos de hello para la implementación (en líneas 10 y 11 solo).
1. ¡Guardar los cambios de Hola!

Configuración de estos valores aquí simplemente evita tener tooupdate estos valores específicos de la implementación en todos los scripts.

### <a name="execute-scripts-by-pressing-f5"></a>Ejecución de scripts presionando F5

Usan varias secuencias de comandos *$PSScriptRoot* toonavigate carpetas, y *$PSScriptRoot* sólo se evalúa cuando se ejecutan scripts presionando **F5**.  Resaltar y ejecutar una selección (**F8**) puede dar lugar a errores, por tanto, presione **F5** al ejecutar los scripts.

### <a name="step-through-hello-scripts-tooexamine-hello-implementation"></a>Paso a través de hello scripts de implementación de hello tooexamine

secuencias de comandos de Hello mejor manera toounderstand hello es revisar paso por paso a través de ellos toosee lo que hacen. Extraer del repositorio Hola incluida **demostración -** secuencias de comandos que presentan un flujo de trabajo de alto nivel de toofollow fácil. Hola **demostración -** scripts muestran Hola pasos necesarios tooaccomplish cada tarea, por tanto, establecer puntos de interrupción y el profundizar un poco más Hola individuales llama toosee detalles de implementación para hello diferentes patrones de SaaS.

Sugerencias para explorar y recorrer los scripts de PowerShell:

* Abra **demostración -** scripts en hello PowerShell ISE.
* Ejecute o continúe con **F5** (no se recomienda el uso de **F8** porque *$PSScriptRoot* no se evalúa cuando se ejecutan las selecciones de un script).
* Para colocar puntos de interrupción, haga clic o seleccione una línea y presione **F9**.
* Salte una llamada de función o script con **F10**.
* Vaya a una llamada de función o script con **F11**.
* Paso a paso de la función actual de Hola o secuencia de comandos llamada con **MAYÚS + F11**.


## <a name="explore-database-schema-and-execute-sql-queries-using-ssms"></a>Exploración del esquema de base de datos y ejecución de consultas SQL con SSMS

Use [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) tooconnect y examinar Hola servidores de aplicaciones y bases de datos.

implementación de Hello inicialmente tiene dos bases de datos de SQL servidores tooconnect demasiado-Hola *tenants1 -&lt;usuario&gt;*  hello y servidor *catálogo -&lt;usuario&gt;* server. tooensure una conexión de demostración correcta, ambos servidores tienen un [regla de firewall](sql-database-firewall-configure.md) permitir todas las direcciones IP a través de.


1. Abra *SSMS* y conéctese toohello *tenants1 -&lt;usuario&gt;. database.windows.net* server.
1. Haga clic en **Conectar** > **Motor de base de datos...**:

   ![Servidor de catálogo](media/sql-database-wtp-overview/connect.png)

1. Las credenciales para la demo son: inicio de sesión = *developer*, contraseña =*P@ssword1*.

   ![connection](media\sql-database-wtp-overview\tenants1-connect.png)

1. Repita los pasos 2 y 3 y conectar toohello *catálogo -&lt;usuario&gt;. database.windows.net* server.

Después de conectarse correctamente debería ver ambos servidores. La lista de bases de datos podría ser diferente, dependiendo de los inquilinos de hello que ha aprovisionado:

![Explorador de objetos](media/sql-database-wtp-overview/object-explorer.png)



## <a name="next-steps"></a>Pasos siguientes

[Implementar aplicaciones de SaaS Wingtip Hola](sql-database-saas-tutorial.md)
