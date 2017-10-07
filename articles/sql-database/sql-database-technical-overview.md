---
title: "¿aaaWhat es el servicio de base de datos de SQL Azure de hello? | Microsoft Docs"
description: "Obtener una base de datos de introducción tooSQL: detalles técnicos y capacidades de Microsoft relacionales (RDBMS) de sistema de administración en la nube de Hola de base de datos."
keywords: "Introducción toosql, toosql preliminar, ¿qué es la base de datos sql"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: cgronlun
ms.assetid: c561f600-a292-4e3b-b1d4-8ab89b81db48
ms.service: sql-database
ms.custom: overview
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/30/2017
ms.author: carlrab
ms.openlocfilehash: 24ca383ad7e140133d19debc8899f172ee4aa424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-sql-database-service"></a>¿Qué es el servicio de base de datos de SQL Azure Hola? 

SQL Database es un servicio de base de datos relacional de uso general de Microsoft Azure que admite estructuras como datos relacionales, JSON, espacial y XML. Proporciona [un rendimiento escalable dinámicamente](sql-database-service-tiers.md) y opciones como [índices de almacén de columnas](https://docs.microsoft.com/sql/relational-databases/indexes/columnstore-indexes-overview) para realizar un análisis analítico extremo y generar informes, y [OLTP en memoria](sql-database-in-memory.md) para el procesamiento extremo de transacciones. Microsoft administra todas las correcciones y actualización de base de código SQL Hola sin problemas y abstrae toda la administración de la infraestructura subyacente de Hola. 

Base de datos SQL comparte su base de código con hello [el motor de base de datos de Microsoft SQL Server](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation). Con la estrategia de primero en la nube de Microsoft, capacidades más recientes de Hola de SQL Server son tooSQL primer lanzamiento base de datos y, a continuación, tooSQL propio servidor. Este enfoque proporciona hello las capacidades de SQL Server más recientes con ninguna sobrecarga para aplicar una revisión o actualización - y con estas nuevas características probarse en millones de bases de datos. Para obtener información acerca de las nuevas funcionalidades, consulte:

- **[Guía básica de Azure de la base de datos SQL](https://azure.microsoft.com/roadmap/?category=databases)**: un toofind lugar ' s new y qué viene a continuación siguiente. 
- **[Blog de Azure SQL Database](https://azure.microsoft.com/blog/topics/database)**: el lugar en el que los miembros del equipo de producto de SQL Server escriben entradas acerca de las noticias y características de SQL Database. 

SQL Database ofrece un rendimiento predecible en varios niveles de servicio que proporciona escalabilidad dinámica sin tiempo de inactividad, optimización inteligente integrada, escalabilidad y disponibilidad globales, y opciones de seguridad avanzadas (todo ello casi sin necesidad de administración). Estas capacidades permiten toofocus en desarrollo de aplicaciones rápida y acelerar su toomarket de tiempo, en lugar de asignar un tiempo muy valioso y máquinas virtuales de toomanaging de recursos y la infraestructura. Hola servicio está actualmente en 38 datos de base de datos de SQL centra en Hola a todos, con más centros de datos con regularidad, ponga en línea que le permite toorun la base de datos en un centro de datos cerca de usted.

> [!NOTE]
> Para obtener información acerca de la plataforma de seguridad de Azure, consulte [Centro de confianza de Azure](https://azure.microsoft.com/support/trust-center/security/).
>

## <a name="scalable-performance-and-pools"></a>Grupos y rendimiento escalable

Con SQL Database, cada base de datos está aislada de las demás y es portátil, cada una con su propio [nivel de servicio](sql-database-service-tiers.md) con un nivel de rendimiento garantizado. Base de datos SQL proporciona diferentes niveles de rendimiento para distintas necesidades y permite que las bases de datos toobe toomaximize agrupados Hola el uso de recursos y ahorrar dinero.

### <a name="adjust-performance-and-scale-without-downtime"></a>Ajuste del rendimiento y escalabilidad sin tiempo de inactividad

Base de datos SQL ofrece cuatro niveles de servicio, las cargas de trabajo de base de datos de toosupport tooheavyweight ligera: Basic, Standard, Premium y RS Premium. Puede crear su primera aplicación en una base de datos pequeño, único en un bajo costo por mes y, a continuación, cambiar su nivel de servicio manualmente o mediante programación a cualquier necesidad de hello toomeet de tiempo de la solución. Puede ajustar el rendimiento sin tiempo de inactividad tooyour aplicación o tooyour los clientes. Habilita la escalabilidad dinámica su base de datos tootransparently responder toorapidly cambiar los requisitos de recursos y habilita tooonly se paga por los recursos de Hola que necesite cuando los necesite.

   ![escalado](./media/sql-database-what-is-a-dtu/single_db_dtus.png)

### <a name="elastic-pools-toomaximize-resource-utilization"></a>Utilización de recursos de toomaximize grupos elásticos

Para muchas empresas y aplicaciones, que se pueda toocreate bases de datos únicos y marcado rendimiento hacia arriba o hacia abajo a petición es suficiente, especialmente si los patrones de uso son relativamente predecibles. Pero si tiene patrones de uso imprevistos, puede hacer los costos de disco duro toomanage y su modelo empresarial. [Grupos elásticos](sql-database-elastic-pool.md) está diseñada toosolve este problema. concepto de Hello es sencillo. Asignar el grupo de tooa de recursos de rendimiento en lugar de una base de datos individual y pagar para recursos de rendimiento colectivo de Hola de agrupación de hello en lugar de rendimiento de la base de datos único. 

   ![grupos elásticos](./media/sql-database-what-is-a-dtu/sqldb_elastic_pools.png)

Con grupos elásticos, no es necesario toofocus para marcar rendimiento de base de datos hacia arriba y abajo a medida que varía la demanda de recursos. Hello las bases de datos agrupados consumen recursos de rendimiento de Hola de grupo elástico de Hola según sea necesario. Las bases de datos agrupados consumen pero no superan los límites de hello del bloque de hello, por lo que el costo sigue siendo predecible incluso si no hace uso de la base de datos individuales. ¿Qué es más, también puede [agregar y quitar el grupo de servidores de bases de datos toohello](sql-database-elastic-pool-manage-portal.md), ajuste de escala en la aplicación de una serie de toothousands de las bases de datos, todo ello en un presupuesto que usted controla. También puede mínimo de control Hola y Hola de recursos máximos disponibles toodatabases en hello grupo tooensure que ninguna base de datos en bloque de hello usa todos los recursos del grupo y que cada base de datos agrupado tiene una cantidad mínima garantizada de recursos. toolearn más información acerca de los patrones de diseño para aplicaciones de SaaS con grupos elásticos, consulte [patrones de diseño para aplicaciones de SaaS multiempresa con base de datos de SQL](sql-database-design-patterns-multi-tenancy-saas-applications.md).

### <a name="blend-single-databases-with-pooled-databases"></a>Fusión de bases de datos únicas con bases de datos en grupos

Independientemente de lo que use (bases de datos únicas o grupos elásticos) no se encontrará bloqueado. Puede fusionar las bases de datos únicos con grupos elásticos y cambiar los niveles de servicio de Hola de bases de datos únicas y grupos elásticos rápida y fácilmente tooadapt tooyour situación. Con power hello y alcance de Azure, es posible a combinación-y-match otro Azure servicios con la aplicación única diseñar sus necesidades, unidad de costo y las eficiencias de recursos de toomeet de base de datos SQL y desbloquear nuevas oportunidades de negocio.

### <a name="extensive-monitoring-and-alerting-capabilities"></a>Extensas funcionalidades de supervisión y alerta

Pero, ¿cómo se puede comparar rendimiento relativo de Hola de bases de datos únicas y grupos elásticos? ¿Cómo sabrá Hola integral haga clic cuando marque arriba y abajo? Usar hello [supervisión de rendimiento integrado](sql-database-performance.md) y [alertas](sql-database-insights-alerts-portal.md) herramientas, combinadas con una clasificación de rendimiento Hola tomando como base [unidades de transacción de base de datos (Dtu) para bases de datos únicos y Dtu elásticas (Edtu) para grupos elásticos](sql-database-what-is-a-dtu.md). Uso de estas herramientas, puede evaluar rápidamente impacto Hola de escalar verticalmente en función de su suscripción actual o se proyecta necesidades de rendimiento. Para más detalles, consulte [Opciones y rendimiento de SQL Database: comprender lo que está disponible en cada nivel de servicio](sql-database-service-tiers.md) .

Además, SQL Database puede [emitir métricas y registros de diagnóstico](sql-database-metrics-diag-logging.md) para facilitar la supervisión. Puede configurar el uso de recursos de base de datos SQL toostore, los trabajadores y sesiones y conectividad en uno de estos recursos de Azure:

- **Azure Storage**: para archivar grandes cantidades de telemetría a un pequeño precio
- **Azure Event Hub**: para integrar la telemetría de SQL Database con una solución de supervisión personalizada o canalizaciones activas
- **Azure Log Analytics**: para la solución de supervisión integrada con funcionalidades de generación de informes, alertas y mitigación

    ![arquitectura](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="availability-capabilities"></a>Funcionalidades de disponibilidad

El contrato de nivel de servicio [(SLA)](http://azure.microsoft.com/support/legal/sla/)de Azure de disponibilidad del 99,99 %, líder del sector, con la tecnología de una red global de centros de datos administrados por Microsoft, ayuda a mantener las aplicaciones en funcionamiento de forma ininterrumpida. Además, SQL Database proporciona características de [continuidad empresarial y escalabilidad global](sql-database-business-continuity.md) integradas, entre las que se incluyen:

- **[Copias de seguridad automáticas](sql-database-automated-backups.md)**: SQL Database realiza automáticamente copias de seguridad completas, diferenciales y del registro de transacciones.
- **[Restauraciones en un momento](sql-database-recovery-using-backups.md)**: base de datos SQL es compatible con punto de recuperación tooany en el tiempo en período de retención de copia de seguridad automática de Hola.
- **[Replicación geográfica activa](sql-database-geo-replication-overview.md)**: base de datos SQL permite tooconfigure una secundaria legible toofour bases de datos de cualquier Hola igual o distribuida globalmente centros de datos de Azure.  Por ejemplo, si tiene una aplicación de SaaS con una base de datos de catálogo que tiene un gran volumen de transacciones simultáneas de solo lectura, utilice la replicación geográfica activa tooenable global leer escala y quitar cuellos de botella en hello principal debido a las cargas de trabajo tooread. 
- **[Grupos de conmutación por error](sql-database-geo-replication-overview.md)**: base de datos SQL le permite tooenable alta disponibilidad y equilibrio de carga de escala global, incluidos la replicación geográfica transparente y conmutación por error de grandes conjuntos de bases de datos y grupos elásticos. Grupos de conmutación por error y la creación de permite de replicación geográfica activa de las aplicaciones de SaaS distribuidas globalmente con muy poca administración sobrecarga dejar todos los Hola complejo supervisión, enrutamiento y conmutación por error orquestación tooSQL base de datos.

## <a name="built-in-intelligence"></a>Inteligencia integrada

Con la base de datos de SQL, obtendrá inteligencia incorporada que le ayuda a reducir considerablemente los costos de Hola de ejecutar y administrar las bases de datos y maximiza el rendimiento y seguridad de la aplicación. Ejecuta millones de clientes en las cargas de trabajo durante las 24 horas, base de datos de SQL recopila y procesa una cantidad masiva de datos de telemetría, que también totalmente respeta la privacidad de los clientes entre bastidores de Hola. Varios algoritmos continuamente están evaluando los datos de telemetría de Hola para que pueda obtener información y adaptar con la aplicación de servicio Hola. En función de este análisis, servicio de hello aparece con rendimiento mejorar las cargas de trabajo de recomendaciones adaptada tooyour concreto. 

### <a name="automatic-performance-tuning"></a>Ajuste automático del rendimiento

Base de datos SQL proporciona una visión detallada de hello las consultas que necesita toomonitor. La base de datos de SQL aprende acerca de los patrones de la base de datos y permite tooadapt la carga de trabajo de tooyour de esquema de base de datos. SQL Database proporciona recomendaciones para el ajuste del rendimiento mediante [SQL Database Advisor](sql-database-advisor.md), donde puede consultar las acciones de optimización y aplicarlas. Sin embargo, supervisar constantemente una base de datos es una tarea ardua y tediosa, sobre todo cuando se trabaja con muchas bases de datos. Administrar un gran número de bases de datos podría ser eficazmente toodo imposible incluso con todas las herramientas disponibles e informes que proporcionan la base de datos de SQL y el portal de Azure. En lugar de supervisión y optimización de la base de datos manualmente, considere la posibilidad de delegar algunas de Hola de supervisión y optimización tooSQL de acciones mediante la característica de ajuste automático de la base de datos. Base de datos SQL aplicar recomendaciones, pruebas y comprueba cada uno de su rendimiento de Hola de optimización acciones tooensure mantiene mejorar automáticamente. De esta manera, base de datos SQL se adapta automáticamente tooyour cargas de trabajo de manera controlada y segura. El ajuste automático significa que rendimiento hello de la base de datos se supervisa y se comparan antes y después de cada acción de optimización con cuidado, y si no mejora el rendimiento de hello, se revierte la acción para la optimización de Hola.

Hoy en día, muchas de nuestros partners ejecutando [aplicaciones de varios inquilinos de SaaS](sql-database-design-patterns-multi-tenancy-saas-applications.md) encima de la base de datos SQL está confiando en automáticas de rendimiento para la optimización toomake seguro sus aplicaciones siempre tienen un rendimiento estable y predecible. Para ellos, esta característica enormemente si reduce el riesgo de Hola de tener un incidente de rendimiento en medio de Hola de noche Hola. Además, puesto que parte de su base de clientes también utiliza SQL Server, usan Hola mismas recomendaciones de indización proporcionan por base de datos SQL toohelp sus clientes de SQL Server.

Hay dos aspectos del ajuste automático disponibles en SQL Database:

- **[Administración de índices automática](sql-database-automatic-tuning.md#automatic-index-management)**: identifica tanto los índices que se deben agregar a la base de datos como los que se deben quitar.
- **[Corrección automática de planes](sql-database-automatic-tuning.md#automatic-plan-choice-correction)**: identifica planes problemáticos y corrige los problemas de rendimiento de los planes de SQL (próximamente, ya disponible en SQL Server 2017).

### <a name="adaptive-query-processing"></a>Procesamiento adaptable de consultas

También estamos agregando hello [procesamiento de consultas adaptable](/sql/relational-databases/performance/adaptive-query-processing) familia de características tooSQL base de datos, incluida la ejecución intercalada de funciones con valores de tabla de múltiples instrucciones, comentarios de concesión de memoria de modo de lotes y combinaciones adaptable de modo de lotes . Cada una de estas características de procesamiento de consultas adaptable aplica técnicas similares "aprender y adaptar", ayudando a más problemas de optimización de consulta difíciles de tratar de dirección rendimiento problemas toohistorically relacionados.

### <a name="intelligent-threat-detection"></a>Detección de amenazas inteligente

 [Detección de amenazas SQL](sql-database-threat-detection.md) aprovecha [auditoría de base de datos SQL](sql-database-auditing.md) toocontinuously monitor SQL Azure bases de datos para datos confidenciales de intentos potencialmente perjudiciales que tooaccess. Detección de amenazas SQL proporciona una nueva capa de seguridad, lo cual permite toodetect de los clientes y responde a amenazas de toopotential cuando se producen al proporcionar alertas de seguridad en actividades anómalas. Los usuarios reciben alertas cuando se producen actividades sospechosas en la base de datos, aparecen vulnerabilidades potenciales y ataques de inyección de SQL, y existen patrones anómalos de acceso a la base de datos. Amenaza SQL para alertas de detección proporcionan detalles de actividad sospechosa y recomendarán acción sobre cómo tooinvestigate y mitigar la amenaza de Hola. Los usuarios pueden explorar Hola eventos sospechosos toodetermine si los resultados de evento de Hola desde un tooaccess intento, incumplen o vulnerabilidad de seguridad de datos en la base de datos de Hola. La detección de amenazas resulta sencillo tooaddress posibles amenazas toohello base de datos sin necesidad de hello toobe un experto en seguridad o administrar sistemas de supervisión de seguridad avanzada.

## <a name="advanced-security-and-compliance"></a>Conformidad y seguridad avanzada

Base de datos SQL proporciona una gama de [características integradas de seguridad y cumplimiento](sql-database-security-overview.md) toohelp la aplicación cumplir distintos requisitos de seguridad y cumplimiento de normas. 

### <a name="auditing-for-compliance-and-security"></a>Auditoría de seguridad y cumplimiento

[Auditoría de base de datos de SQL](sql-database-auditing.md) realiza un seguimiento de eventos de base de datos y escribe el registro de auditoría tooan en su cuenta de almacenamiento de Azure. La auditoría puede ayudarle a mantener el cumplimiento de normativas, comprender la actividad de las bases de datos y conocer las discrepancias y anomalías que pueden indicar problemas en el negocio o infracciones de seguridad sospechosas.

### <a name="data-encryption-at-rest"></a>Cifrado de datos en reposo

Base de datos SQL [cifrado de datos transparente](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database) ayuda a protegerse contra amenazas de Hola de actividad malintencionada mediante la realización de cifrado en tiempo real y el descifrado de base de datos de hello, copias de seguridad asociadas y archivos de registro de transacciones en reposo sin necesidad de cambios toohello aplicación. Desde mayo de 2017, todas las bases de datos SQL de Azure recién creadas tienen automáticamente la protección del cifrado de datos transparente (TDE). TDE es SQL cifrado en reposo tecnología probada que requiere muchos tooprotect de estándares de cumplimiento de normas contra el robo de medios de almacenamiento. Los clientes pueden administrar las claves de cifrado de TDE hello y otros secretos de forma segura y ser conforme con el almacén de claves de Azure.

### <a name="data-encryption-in-motion"></a>Cifrado de datos en movimiento

Base de datos SQL es Hola única base de datos toooffer protección del sistema de los datos confidenciales en tránsito en reposo y durante el procesamiento de consultas con [Always Encrypted](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine). Always Encrypted es un primer sector que ofrece datos sin parangón seguridad contra violaciones de robo de Hola de datos críticos. Por ejemplo, con Always Encrypted, números de tarjeta de crédito de los clientes se almacenan cifrados en la base de datos de hello siempre, incluso durante el procesamiento de consultas, lo que permite el descifrado en el momento de Hola de uso personal autorizado o las aplicaciones que necesitan tooprocess esos datos.

### <a name="dynamic-data-masking"></a>Enmascaramiento de datos dinámicos

[Enmascaramiento de datos dinámicos de la base de datos SQL](sql-database-dynamic-data-masking-get-started.md) limita la exposición de información confidencial ocultándolos toonon privilegios a los usuarios. Enmascaramiento dinámico de datos ayuda a evitar datos toosensitive de acceso no autorizado al habilitar clientes toodesignate cuánto Hola confidencial tooreveal con un impacto mínimo en el nivel de aplicación Hola. Es una característica de seguridad basada en directivas que oculta los datos confidenciales Hola Hola conjunto de resultados de una consulta de campos de la base de datos designada, Hola datos en la base de datos de hello no cambian.

### <a name="row-level-security"></a>Seguridad de nivel de fila

[Seguridad de nivel de fila](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) permite que los clientes toocontrol acceso toorows en una tabla de base de datos basada en características de Hola de usuario de Hola que se ejecuta una consulta (como según el contexto de ejecución o de pertenencia de grupo). Seguridad de nivel de fila (RLS) simplifica el diseño de Hola y codificación de seguridad de la aplicación. RLS permite tooimplement restricciones de acceso de la fila de datos. Por ejemplo, garantizar que los trabajadores puedan acceder solamente las filas de datos que son pertinentes tootheir departamento o restringir una empresa del cliente con datos acceso tooonly Hola datos tootheir relevante.

### <a name="azure-active-directory-integration-and-multi-factor-authentication"></a>Integración de Azure Active Directory y autenticación multifactor

Habilita la base de datos SQL se toocentrally administrar identidades de usuario de base de datos y otros servicios de Microsoft con [integración de Azure Active Directory](sql-database-aad-authentication.md). Esta funcionalidad simplifica la administración de permisos y mejora la seguridad. Azure Active Directory admite [la autenticación multifactor](sql-database-ssms-mfa-authentication.md) seguridad de datos y aplicaciones de tooincrease de (MFA) que un único proceso inicie sesión en la ejecución.

### <a name="compliance-certification"></a>Certificación de cumplimiento

SQL Database participa en auditorías periódicas y se ha certificado con varios estándares de cumplimiento. Para obtener más información, vea hello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/), donde puede encontrar la lista más reciente de Hola de [certificaciones de cumplimiento de la base de datos SQL](https://azure.microsoft.com/support/trust-center/services/).

## <a name="easy-to-use-tools"></a>Herramientas fáciles de usar

SQL Database facilita la creación y el mantenimiento de aplicaciones y aumenta su productividad. Base de datos SQL le permite toofocus en lo que hace mejor: crear fantásticas aplicaciones. En SQL Database, puede realizar labores de administración y desarrollo mediante las herramientas y los conocimientos que ya posee.

- **[Hola portal de Azure](https://portal.azure.com/)**: una aplicación basada en web para administrar todos los servicios de Azure 
- **[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)**: una aplicación de cliente gratuita y descargable para administrar cualquier infraestructura de SQL desde tooSQL base de datos de SQL Server
- **[SQL Server Data Tools en Visual Studio](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)**: una aplicación cliente gratuita que se puede descargar para desarrollar bases de datos relacionales de SQL Server, bases de datos de Azure SQL, paquetes de Integration Services, modelos de datos de Analysis Services e informes de Reporting Services.
- **[Código de Visual Studio](https://code.visualstudio.com/docs)**: un, puede descargar código abierto, editor de código para Windows, Mac OS y Linux que admita extensiones, incluidas hello [mssql extensión](https://aka.ms/mssql-marketplace) para realizar consultas en Microsoft SQL Server Base de datos SQL Azure y almacenamiento de datos SQL.

Base de datos SQL admite la creación de aplicaciones con Python, Java, Node.js, PHP, Ruby y en hello MacOS. NET, Linux y Windows. Base de datos SQL admite Hola mismo [bibliotecas de conexiones de](sql-database-libraries.md) como SQL Server.

## <a name="engage-with-hello-sql-server-engineering-team"></a>Ponerse en contacto con el equipo de ingeniería de hello SQL Server

- [Cambio de pila de DBA](https://dba.stackexchange.com/questions/tagged/sql-server): formule preguntas sobre administración de base de datos
- [Desbordamiento de pila](http://stackoverflow.com/questions/tagged/sql-server): formule preguntas sobre desarrollo
- [Foros de MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver): formule preguntas técnicas
- [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback): informe de errores y características de la solicitud
- [Reddit](https://www.reddit.com/r/SQLServer/): analice SQL Server

## <a name="next-steps"></a>Pasos siguientes

- Vea hello [página de precios](https://azure.microsoft.com/pricing/details/sql-database/) para comparaciones de costo de grupos elásticos y base de datos única y calculadoras.

- Consulte que estos rápida inicia tooget inició:

  - [Crear una base de datos SQL en hello portal de Azure](sql-database-get-started-portal.md)  
  - [Crear una base de datos SQL con hello CLI de Azure](sql-database-get-started-cli.md)
  - [Creación de una base de datos SQL con PowerShell](sql-database-get-started-powershell.md)

- Para obtener ejemplos de la CLI de Azure y de PowerShell, consulte:
  - [Ejemplos de la CLI de Azure para SQL Database](sql-database-cli-samples.md)
  - [Ejemplos de Azure PowerShell para SQL Database](sql-database-powershell-samples.md)
