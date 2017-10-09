---
title: "consultas de análisis de aaaRun en varias bases de datos SQL de Azure | Documentos de Microsoft"
description: "Extracción de datos de las bases de datos de inquilino en una base de datos de análisis para el análisis sin conexión"
keywords: tutorial de base de datos sql
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
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a>Extracción de datos de las bases de datos de inquilino en una base de datos de análisis para el análisis sin conexión

En este tutorial, utilice un consultas de toorun de trabajo elástica en cada base de datos de inquilinos. trabajo de Hello extrae datos de ventas de vale y los carga en una base de datos de análisis (o el almacenamiento de datos) para el análisis. Hola base de datos de análisis es, a continuación, consultar información tooextract desde estos datos de operaciones diarios de todos los inquilinos.


En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear base de datos de análisis de inquilinos de Hola
> * Crear un trabajo programado tooretrieve de datos y rellenar la base de datos de análisis de Hola

toocomplete este tutorial, asegúrese de hello seguro siguiendo los requisitos previos se cumplen:

* se implementa la aplicación de SaaS Wingtip Hello. vea toodeploy en menos de cinco minutos, [implementar y explorar la aplicación de SaaS Wingtip hello](sql-database-saas-tutorial.md)
* Azure PowerShell está instalado. Para más información, consulte [Introducción a Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).
* se instala la versión más reciente de Hola de SQL Server Management Studio (SSMS). [Descarga e instalación de SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a>Patrón de análisis operativos de inquilino

Una de las grandes oportunidades de hello con aplicaciones de SaaS es toouse Hola inquilino completo que se almacena en la nube de Hola. Utilice esta información sobre toogain los datos en la operación de Hola y el uso de la aplicación y los inquilinos. Estos datos pueden guiarle característica desarrollo, las mejoras de facilidad de uso y otras mejoras en la aplicación hello y plataforma. Es fácil obtener acceso a estos datos cuando se encuentran en una sola base de datos multiinquilino, pero no es tan fácil cuando se distribuyen a escala en miles de bases de datos. Tooaccessing de un enfoque estos datos son toouse elástico trabajos, lo que permite resultados de la consulta devuelve resultados de toobe de ejecución de trabajo capturados en una base de datos de salida y la tabla.

## <a name="get-hello-wingtip-application-scripts"></a>Obtener scripts de la aplicación hello Wingtip

Hello Wingtip SaaS scripts y código fuente de aplicación están disponibles en hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositorio de github. [Pasos de secuencias de comandos de toodownload Hola Wingtip SaaS](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="deploy-a-database-for-tenant-analytics-results"></a>Implementar una base de datos para resultados de análisis de inquilino

Este tutorial requiere toohave que un Hola de toocapture implementada de la base de datos resultante de la ejecución del trabajo de scripts que contienen consultas que devuelven resultados. Vamos a crear una base de datos denominada tenantanalytics con este fin.

1. Abra... \\Módulos de aprendizaje\\análisis operativos\\inquilino análisis\\*demostración TenantAnalyticsDB.ps1* en hello *PowerShell ISE* y establecer Hola siguiente valor:
   * **$DemoScenario** = **2***Deploy operational analytics database*
1. Presione **F5** script de demostración de hello toorun (esa Hola llamadas *TenantAnalyticsDB.ps1 implementar* secuencia de comandos) que crea la base de datos de análisis de inquilinos de Hola.

## <a name="create-some-data-for-hello-demo"></a>Crear algunos datos de demostración de hello

1. Abra... \\Módulos de aprendizaje\\análisis operativos\\inquilino análisis\\*demostración TenantAnalyticsDB.ps1* en hello *PowerShell ISE* y establecer Hola siguiente valor:
   * **$DemoScenario** = **1***Purchase tickets for events at all venues*
1. Presione **F5** toorun Hola script y crear incidencia de historial de compras.


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a>Crear un análisis de inquilino de trabajo programado tooretrieve sobre la compra de vales

Este script crea una información de compra de vales de trabajo tooretrieve de todos los inquilinos. Después de haber agregado en una sola tabla, puede obtener enriquecidas métricas precisos sobre vale compras patrones a través de los inquilinos de Hola.

1. Abra SSMS y conéctese toohello catálogo -&lt;usuario&gt;. database.windows.net server
1. Abra ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*.
1. Modificar &lt;usuario&gt;, usar el nombre de usuario hello usa al implementar la aplicación de SaaS Wingtip hello en parte superior de Hola de script de Hola, **sp\_agregar\_destino\_grupo\_miembro** y **sp\_agregar\_paso de trabajo**
1. Haga clic en, seleccione **conexión**y conecte toohello catálogo -&lt;usuario&gt;. database.windows.net server, si aún no está conectado
1. Asegúrese de que está conectado toohello **jobaccount** base de datos del sistema y presione **F5** para ejecutar el script de Hola

* **SP\_agregar\_destino\_grupo** crea el nombre del grupo de destino de hello *TenantGroup*, ahora tenemos tooadd miembros de destino.
* **SP\_agregar\_destino\_grupo\_miembro** agrega un *server* tipo de miembro que considere todas las bases de datos dentro de ese servidor (tenga en cuenta esto es hello customer1 - destino &lt;Usuario&gt; servidor que contiene las bases de datos del inquilino de Hola) en tiempo de trabajo de ejecución debe incluirse en el trabajo de Hola.
* **sp\_add\_job** crea un trabajo programado semanal denominado "Ticket Purchases from all Tenants".
* **SP\_agregar\_jobstep** crea toda la información de hello vale compra de paso de trabajo de Hola que contiene tooretrieve de texto de comando de T-SQL de todos los inquilinos y Hola copia devolver el conjunto de resultados en una tabla denominada  *AllTicketsPurchasesfromAllTenants*
* Hola restantes en el script de Hola muestran existencia Hola de objetos de Hola y supervisar la ejecución de trabajo. Revise el valor de estado de Hola de hello **ciclo de vida** estado de la columna toomonitor Hola. Una vez, se realizó correctamente, trabajo de hello ha finalizado correctamente en todas las bases de datos de inquilino y hello dos bases de datos adicionales que contengan Hola hacen referencia a tabla.

Script de Hola se ejecute correctamente debe dar lugar a resultados similares:

![results](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a>Crear un tooretrieve de trabajo un recuento de resumen del vale de compra a todos los inquilinos

Este script crea una suma de tooretrieve de trabajo de todas las compras de vales de todos los inquilinos.

1. Abra SSMS y conéctese toohello *catálogo -&lt;usuario&gt;. database.windows.net* server
1. Archivo de hello abrir... \\Módulos de aprendizaje\\aprovisionar y catálogo\\análisis operativos\\inquilino análisis\\*TicketPurchasesfromAllTenants.sql de resultados*
1. Modificar &lt;usuario&gt;, usar el nombre de usuario hello usa al implementar la aplicación de SaaS Wingtip hello en un script de Hola, en hello **sp\_agregar\_jobstep** procedimiento almacenado
1. Haga clic en, seleccione **conexión**y conecte toohello catálogo -&lt;usuario&gt;. database.windows.net server, si aún no está conectado
1. Asegúrese de que está conectado toohello **tenantanalytics** base de datos del sistema y presione **F5** para ejecutar el script de Hola

Script de Hola se ejecute correctamente debe dar lugar a resultados similares:

![results](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* **sp\_add\_job** crea un trabajo programado semanal denominado "ResultsTicketsOrders".

* **SP\_agregar\_jobstep** crea toda la información de hello vale compra de paso de trabajo de Hola que contiene tooretrieve de texto de comando de T-SQL de todos los inquilinos y devolver el conjunto de resultados en una tabla denominada CountofTicketOrders de Hola de copia

* Hola restantes en el script de Hola muestran existencia Hola de objetos de Hola y supervisar la ejecución de trabajo. Revise el valor de estado de Hola de hello **ciclo de vida** estado de la columna toomonitor Hola. Una vez, se realizó correctamente, trabajo de hello ha finalizado correctamente en todas las bases de datos de inquilino y hello dos bases de datos adicionales que contengan Hola hacen referencia a tabla.


## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo:

> [!div class="checklist"]
> * Implementar una base de datos de análisis de inquilinos
> * Crear un trabajo programado tooretrieve los datos analíticos a través de los inquilinos

¡Enhorabuena!

## <a name="additional-resources"></a>Recursos adicionales

* Adicionales [tutoriales que parten Hola aplicación Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Trabajos elásticos](sql-database-elastic-jobs-overview.md)
