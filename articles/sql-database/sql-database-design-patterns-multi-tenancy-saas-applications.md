---
title: patrones de aaaDesign para las aplicaciones SaaS de varios inquilinos y la base de datos de SQL de Azure | Documentos de Microsoft
description: "Este artículo describen los requisitos de Hola y patrones comunes de la arquitectura de datos de aplicaciones de base de datos de varios inquilinos que se ejecutan en un entorno de nube necesitan tooconsider Hola varias desventajas asociadas a estos patrones. También se explica cómo ayuda Base de datos SQL de Azure con sus grupos elásticos y herramientas elásticas a afrontar estos requisitos de forma garantizada."
keywords: 
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 1dd20c6b-ddbb-40ef-ad34-609d398d008a
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-design
ms.date: 02/01/2017
ms.author: srinia
ms.openlocfilehash: a4b58935b08cb78792e65a675d680de708b709fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multi-tenant-saas-applications-and-azure-sql-database"></a>Modelos de diseño para las aplicaciones SaaS multiinquilino y Azure SQL Database
En este artículo, puede obtener información sobre los requisitos de Hola y patrones comunes de la arquitectura de datos de software de varios inquilinos como un aplicaciones de base de datos de servicio (SaaS) que se ejecutan en un entorno de nube. También se explican los factores de Hola que necesita tooconsider y Hola ventajas y desventajas de patrones de diseño diferentes. Los grupos y herramientas elásticos de Base de datos SQL de Azure pueden ayudarle a satisfacer necesidades específicas sin poner en peligro otros objetivos.

A veces, los desarrolladores de tomar decisiones que trabajan con sus intereses a largo plazo cuando diseñan modelos de inquilinos para capas de datos de Hola de aplicaciones de varios inquilinos. Inicialmente, al menos, un desarrollador puede percibir facilidad de desarrollo y menores costos de proveedor de servicio de nube como más importante que la escalabilidad de Hola o de aislamiento de inquilinos de una aplicación. Esta opción puede provocar problemas de satisfacción toocustomer y una corrección de curso costosa más adelante.

Una aplicación de varios inquilinos es una aplicación hospedada en un entorno de nube y que proporciona Hola al mismo conjunto de servicios toohundreds o miles de inquilinos que no comparta ni ver los datos de todas las demás. Un ejemplo es una aplicación de SaaS que proporciona servicios tootenants en un entorno hospedado en la nube.

## <a name="multi-tenant-applications"></a>Aplicaciones multiinquilino
En aplicaciones multiinquilino, se pueden particionar fácilmente los datos y la carga de trabajo. Puede dividir datos y la carga de trabajo, por ejemplo, a lo largo de los límites del inquilino, porque la mayoría de las solicitudes se produce dentro de los confines de Hola de inquilinos. Esa propiedad es inherente a los datos de Hola y carga de trabajo de Hola y favorece patrones de aplicación Hola descritos en este artículo.

Los desarrolladores usar este tipo de aplicación en completo espectro de Hola de aplicaciones basadas en la nube, incluidas:

* Las aplicaciones de base de datos de socios comerciales que se toohello transición en la nube como aplicaciones de SaaS
* Aplicaciones de SaaS integradas para la nube de Hola de hello masa
* Aplicaciones directas y orientadas a clientes
* Aplicaciones empresariales orientadas a empleados

Aplicaciones de SaaS que están diseñadas para una nube de Hola o aquellos con raíces como aplicaciones de base de datos de socios comerciales normalmente las aplicaciones de varios inquilinos. Estas aplicaciones de SaaS ofrecen una aplicación de software especializado como un inquilinos tootheir de servicio. Los inquilinos pueden tener acceso a servicios de aplicación hello y tener la propiedad completa de datos asociados almacenados como parte de la aplicación hello. Pero tootake aprovechar las ventajas de Hola de SaaS, los inquilinos debe entregar cierto control sobre sus propios datos. Confían en tookeep de proveedor de servicio de SaaS Hola sus datos seguros y aislados de datos de otros inquilinos. Ejemplos de este tipo de aplicación SaaS multiinquilino son MYOB, SnelStart y Salesforce.com. Cada una de estas aplicaciones se puede crear particiones a lo largo de los límites de inquilinos y los patrones de diseño de aplicaciones compatibilidad Hola que se explican en este artículo.

Las aplicaciones que ofrecen un servicio directo toocustomers o tooemployees dentro de una organización (tooas a menudo que se hace referencia a los usuarios, en lugar de los inquilinos) son otra categoría en el espectro de aplicación de varios inquilinos de Hola. Los clientes suscriben toohello servicio y no poseen datos Hola Hola proveedor de servicios recopilan y almacena. Proveedores de servicios tienen menos estrictas tookeep requisitos aislados entre sí más allá de la normativa de privacidad impuestas por el gobierno de datos de sus clientes. Ejemplos de este tipo de aplicación multiinquilino orientada al cliente son proveedores de contenido multimedia como Netflix, Spotify y Xbox LIVE. Otros ejemplos de aplicaciones en las que se pueden crear particiones fácilmente son aquellas para Internet orientadas al cliente o las aplicaciones de Internet de las cosas (IoT), en las que cada cliente o dispositivo sirve de partición. Los límites de partición pueden separar a los usuarios y los dispositivos.

No todas las aplicaciones se particionan fácilmente a lo largo de una sola propiedad como inquilino, cliente, usuario o dispositivo. Una aplicación de planeación de recursos empresariales (ERP) compleja, por ejemplo, tiene productos, pedidos y clientes. Suele tener una estructura compleja con miles de tablas muy interconectadas.

No hay ninguna estrategia de partición única puede aplicar tooall tablas y trabajar a través de la carga de trabajo de la aplicación. Este artículo se centra en las aplicaciones multiinquilino que tienen cargas de trabajo y datos que se pueden particionar fácilmente.

## <a name="multi-tenant-application-design-trade-offs"></a>Ventajas y desventajas del diseño de las aplicaciones multiinquilino
modelo de diseño de Hola que un desarrollador de aplicaciones de varios inquilinos elige normalmente se basa en una cuenta de hello siguientes factores:

* **Aislamiento de inquilinos**. desarrollador de Hello debe tooensure que ningún inquilino tiene datos de los inquilinos de tooother de acceso no deseado. requisito de aislamiento de Hello extiende tooother propiedades, como proporcionar protección de vecinos con ruido, que se va a toorestore capaz de datos de un inquilino e implementar personalizaciones específicas del inquilino.
* **Costo de los recursos en la nube**. Una aplicación de SaaS necesita toobe precios competitivos. Un desarrollador de aplicaciones de varios inquilinos puede elija toooptimize para reducir el costo de uso de Hola de recursos de nube, como almacenamiento y los costos de proceso.
* **Facilidad de DevOps**. Un desarrollador de aplicaciones de varios inquilinos debe tooincorporate protección de aislamiento, mantener y supervisar el estado de saludo de su aplicación y el esquema de base de datos y solucionar problemas del inquilino. Complejidad de desarrollo de aplicaciones y la operación traduce directamente tooincreased costo y desafíos con la satisfacción de los inquilinos.
* **Escalabilidad**. Hola capacidad tooincrementally agregar varios inquilinos y la capacidad de los inquilinos que necesiten es imperativo tooa correcta operación de SaaS.

Cada uno de estos factores tiene ventajas y desventajas en comparación con tooanother. Hola costo más bajo en la nube no se puedan ofrecer la experiencia de desarrollo más conveniente de saludo de la oferta. Es importante para que un desarrollador toomake informado opciones sobre estas opciones y sus ventajas e inconvenientes durante el proceso de diseño de aplicación Hola.

Un modelo de desarrollo conocidas es toopack varios inquilinos en una o varias bases de datos. ventajas de Hola de este enfoque son un costo menor porque se paga por algunas bases de datos y la simplicidad relativa Hola sobre cómo trabajar con un número limitado de las bases de datos. Pero con el tiempo, un desarrollador de aplicaciones multiinquilino SaaS se dará cuenta de que esta opción presenta grandes inconvenientes en lo relativo a aislamiento de inquilinos y escalabilidad. Si el aislamiento de inquilinos es importante, esfuerzo adicional es necesario tooprotect inquilino datos en el almacenamiento compartido de acceso no autorizado o a los vecinos con ruido. Este esfuerzo adicional puede aumentar de forma significativa los esfuerzos de desarrollo y los costos de mantenimiento del aislamiento. De forma similar, si es necesario agregar los inquilinos, este patrón de diseño normalmente requiere datos de conocimientos tooredistribute inquilino a través de la capa de datos de las bases de datos tooproperly escala Hola de una aplicación.  

A menudo el aislamiento de inquilinos es un requisito fundamental en aplicaciones de varios inquilinos de SaaS que cumplir los requisitos de toobusinesses y organizaciones. A un desarrollador pueden seducirle más las ventajas percibidas con respecto a la sencillez y el costo que el aislamiento de inquilinos y la escalabilidad. Puede demostrar a este desequilibrio complejas y caras como servicio de hello crece y se convierten en requisitos de aislamiento de inquilinos más importantes y administrada en el nivel de aplicación Hola. Sin embargo, en aplicaciones de varios inquilinos que proporcionan un toocustomers directa y consumo de servicio, aislamiento de inquilinos podría ser una prioridad inferior a optimizar el coste de recursos de nube.

## <a name="multi-tenant-data-models"></a>Modelos de datos multiinquilino
Las prácticas de diseño comunes para colocar los datos del inquilino siguen tres modelos distintos que se muestran en la Figura 1.

![Modelos de datos de aplicaciones multiinquilino](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-multi-tenant-data-models.png)

Figura 1: Prácticas de diseño comunes para los modelos de datos multiinquilino

* **Base de datos por inquilino**. Cada inquilino tiene su propia base de datos. Todos los datos específicos del inquilino es la base de datos del inquilino toohello reducidos y aislado de otros inquilinos y sus datos.
* **Bases de datos divididas compartidas**. Varios inquilinos comparten una de varias bases de datos. Un conjunto distinto de los inquilinos asignado tooeach base de datos mediante una estrategia de particiones como hash, el intervalo o el particionamiento de lista. Esta estrategia de distribución de datos a menudo es el particionamiento de tooas que se hace referencia.
* **Única base de datos compartida**. Una única base de datos, a veces grande, contiene datos de todos los inquilinos, cuya ambigüedad se elimina con una columna de identificador de inquilino.

> [!NOTE]
> Un desarrollador de aplicaciones puede elegir tooplace varios inquilinos en esquemas de base de datos diferente y, a continuación, usar a distintos inquilinos de hello esquema nombre toodisambiguate Hola. No se recomienda este enfoque porque normalmente requiere el uso de Hola de SQL dinámico y no puede ser eficaz en el almacenamiento en caché de plan. En el resto de Hola de este artículo, nos centramos en el enfoque de la tabla de hello compartido para esta categoría de aplicación de varios inquilinos.
> 
> 

## <a name="popular-multi-tenant-data-models"></a>Modelos de datos multiinquilino más conocidos
Es tipos diferentes de hello tooevaluate importante de los modelos de datos de varios inquilinos en cuanto a Hola aplicación diseño ventajas e inconvenientes que ya hemos identificado. Estos factores ayuda a caracterizar Hola tres más comunes multiempresa modelos de datos que se ha descrito anteriormente y su uso de la base de datos tal como se muestra en la figura 2.

* **Aislamiento**. grado de Hola de aislamiento entre los inquilinos puede ser una medida de cuánto aislamiento de inquilinos logra un modelo de datos.
* **Costo de los recursos en la nube**. cantidad de Hola de uso compartido entre los inquilinos de recursos puede optimizar el coste de recursos de nube. Un recurso puede definirse como proceso de Hola y el costo de almacenamiento.
* **Costo de DevOps**. facilidad de Hola de desarrollo de aplicaciones, implementación y administración reduce el costo total de la operación de SaaS.  

En la figura 2, eje de Hola Y muestra el nivel de Hola de aislamiento de inquilinos. eje de Hello X muestra el nivel de Hola de uso compartido de recursos. gris Hello, flecha diagonal en medio de hello indica dirección Hola de costos de DevOps, tienden más tooincrease o disminución.

![Modelos de diseño de aplicaciones multiinquilino más conocidos](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-popular-application-patterns.png)

Figure 2: Modelos de datos multiinquilino más conocidos

Hello cuadrante inferior derecho en la figura 2 muestra un patrón de aplicación que utiliza una base de datos único potencialmente grande, compartida y Hola compartido tabla (o un esquema independiente) enfoque. Es conveniente para uso compartido porque todos los inquilinos usan Hola mismos recursos (CPU, memoria, entrada/salida) de una base de datos de la base de datos de recursos. Sin embargo, el aislamiento de inquilinos es limitado. Puede que tenga a los inquilinos de tooprotect de pasos adicionales de tootake entre sí en el nivel de aplicación Hola. Estos pasos adicionales pueden aumentar considerablemente el costo de DevOps de Hola de desarrollar y administrar la aplicación hello. Escalabilidad está limitada por la escala de Hola de hardware de Hola que hospeda la base de datos de Hola.

Cuadrante inferior izquierda de Hello en la figura 2 muestra varios inquilinos particionados a través de varias bases de datos (a menudo, un hardware diferente, se escalan unidades). Cada base de datos hospeda un subconjunto de los inquilinos, que aborda Hola preocupación de escalabilidad de otros patrones. Si tiene más capacidad para varios inquilinos, puede colocar fácilmente los inquilinos de hello en nuevas bases de datos asignados toonew unidades de escalado de hardware. Sin embargo, se reduce la cantidad de Hola de uso compartido de recursos. Solo los inquilinos colocan en hello mismo unidades de escala compartan recursos. Este enfoque proporciona aislamiento de tootenant de poca mejora porque muchos inquilinos todavía se colocan sin que se va a protegidos automáticamente frente a sus respectivas acciones. La complejidad de la aplicación permanece alta.

Cuadrante de la parte superior izquierda de Hello en la figura 2 es el tercer enfoque de Hola. Coloca los datos de cada inquilino en su propia base de datos. Este enfoque tiene unas propiedades de aislamiento de inquilinos excelentes pero limita el uso compartido de recursos cuando cada base de datos tiene sus propios recursos específicos. Es un buen enfoque si todos los inquilinos tienen cargas de trabajo predecibles. Si se convierten en las cargas de trabajo de inquilino menos predecibles, proveedor de hello no puede optimizar el uso compartido de recursos. La imprevisibilidad es habitual entre las aplicaciones SaaS. proveedor de Hola o bien debe aprovisionar excesivos toomeet demanda o recursos inferior. Ambas acciones provocan unos costos mayores o una menor satisfacción de los inquilinos. Un mayor grado de uso compartido entre los inquilinos de recursos se convierte en la solución de hello toomake deseable más rentable. Creciente número de Hola de bases de datos también aumenta DevOps costo toodeploy y mantener la aplicación hello. A pesar de estos problemas, este método proporciona aislamiento de hello mejor y más fácil para los inquilinos.

Estos factores también influyen en el modelo de diseño de hello que un cliente elige:

* **Propiedad de los datos de los inquilinos**. Una aplicación en el que los inquilinos conservan la propiedad de sus propios datos favorece el patrón de Hola de una sola base de datos por inquilino.
* **Escala**. Una aplicación destinada a cientos de miles o millones de inquilinos favorece los enfoques de uso compartido de bases de datos como el particionamiento. Los requisitos de aislamiento pueden seguir planteando dificultades.
* **Modelo y valor empresarial**. Si los ingresos por inquilino de una aplicación son reducidos (menos de un dólar), los requisitos de aislamiento son menos críticos y tiene sentido compartir la base de datos. Si los ingresos por inquilino son algunos dólares o más, es más factible usar un modelo de base de datos por inquilino. Puede resultar útil reducir los costos de desarrollo.

Dados Hola diseño ventajas e inconvenientes que se muestra en la figura 2, un modelo de varios inquilinos ideal necesita las propiedades de aislamiento de inquilinos buena tooincorporate con óptimo de los recursos de uso compartido entre los inquilinos. Este modelo se adapta en la categoría de Hola que se describe en el cuadrante de hello superior derecha de la figura 2.

## <a name="multi-tenancy-support-in-azure-sql-database"></a>Compatibilidad con la arquitectura multiinquilino en Azure SQL Database
Azure SQL Database es compatible con todos los modelos de aplicaciones multiinquilino descritos en la Figura 2. Con grupos elásticos, también admite un patrón de aplicación que combina el uso compartido de recursos buena y ventajas del aislamiento de Hola de base de datos por inquilino Hola enfocan (vea Cuadrante superior derecha de hello en la figura 3). Herramientas de bases de datos elásticas y capacidades en la base de datos SQL ayudan a reducir Hola costo toodevelop y utilizar una aplicación que tiene muchas bases de datos (que se muestra en el área de hello sombreado en la figura 3). Estas herramientas pueden ayudarle a crear y administrar aplicaciones que usan cualquiera de los patrones de hello varias bases de datos.

![Modelos de Base de datos SQL de Azure](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-patterns-sqldb.png)

Figura 3: Modelos de aplicaciones multiinquilino en Azure SQL Database

## <a name="database-per-tenant-model-with-elastic-pools-and-tools"></a>Modelo de base de datos por inquilino con grupos elásticos y herramientas
Grupos elásticos en la base de datos SQL combinan aislamiento de inquilinos con recursos compartidos entre el enfoque de base de datos por inquilino de Hola de inquilino bases de datos toobetter soporte técnico. SQL Database es una solución de capa de datos para los proveedores de SaaS que crean aplicaciones multiinquilino. carga de Hola de recursos compartidos entre los inquilinos se desplaza de nivel de servicio de base de datos de hello aplicación capa toohello. complejidad de Hola de administrar y consultar a escala entre bases de datos se ha simplificado con trabajos elásticos, consulta flexible, transacciones elásticas y biblioteca de cliente de base de datos elástica Hola.

| Requisitos de la aplicación | Funcionalidades de Base de datos SQL |
| --- | --- |
| Aislamiento de inquilinos y uso compartido de recursos |[Grupos elásticos](sql-database-elastic-pool.md): asignar un grupo de recursos de base de datos SQL y compartir recursos de hello entre distintas bases de datos. Además, las bases de datos individuales pueden extraer tantos recursos de grupo de hello como los picos de demanda de capacidad de tooaccommodate necesario due toochanges en las cargas de trabajo de inquilino. grupo elástico de Hello, sí se puede escalar hacia arriba o hacia abajo según sea necesario. Grupos elásticos también proporcionan la facilidad de capacidad de administración, supervisión y solución de problemas de nivel de grupo de Hola. |
| Facilidad de DevOps entre bases de datos |[Grupos elásticos](sql-database-elastic-pool.md): como se indica anteriormente. |
| | [Consulta elástica](sql-database-elastic-query-horizontal-partitioning.md): consulta entre bases de datos para informes o análisis entre inquilinos. |
| | [Trabajos elásticos](sql-database-elastic-jobs-overview.md): paquete e implementar de forma confiable las operaciones de mantenimiento de base de datos o bases de datos de toomultiple de cambios de esquema de base de datos. |
| | [Las transacciones elásticas](sql-database-elastic-transactions-overview.md): proceso cambia tooseveral bases de datos de forma atómica y aislada. Las transacciones elásticas son necesarias cuando las aplicaciones necesitan garantías de "todo o nada" para varias operaciones de base de datos. |
| | [Biblioteca de cliente de base de datos elástica](sql-database-elastic-database-client-library.md): administrar las distribuciones de datos y la asignación de los inquilinos toodatabases. |

## <a name="shared-models"></a>Modelos compartidos
Como se describió anteriormente, para la mayoría proveedores de SaaS, el enfoque de modelo compartido puede plantear problemas con el aislamiento de los inquilinos, así como complejidades con el desarrollo y mantenimiento de la aplicación. Sin embargo, en aplicaciones de varios inquilinos que ofrecen un servicio directamente de los inquilinos tooconsumers, requisitos de aislamiento no es una prioridad alta como minimizan los costos. Pueden ser capaz de toopack inquilinos en uno o más bases de datos a un costo de tooreduce de alta densidad. Los modelos de base de datos compartida con una o varias bases de datos particionadas pueden agregar eficacia al uso compartido de recursos y reducir el costo general. La base de datos de SQL Azure proporciona aislamiento para una mayor seguridad y administración a escala Hola nivel de datos de generación de algunas características que ayudan a los clientes.

| Requisitos de la aplicación | Funcionalidades de Base de datos SQL |
| --- | --- |
| Características de aislamiento de seguridad |[Seguridad de nivel de fila](https://msdn.microsoft.com/library/dn765131.aspx) |
| [Crear un esquema de la base de datos](https://msdn.microsoft.com/library/dd207005.aspx) | |
| Facilidad de DevOps entre bases de datos |[Consulta elástica](sql-database-elastic-query-horizontal-partitioning.md) |
| | [Trabajos elásticos](sql-database-elastic-jobs-overview.md) |
| | [Transacciones elásticas](sql-database-elastic-transactions-overview.md) |
| | [Biblioteca de cliente de base de datos elástica](sql-database-elastic-database-client-library.md) |
| | [Dividir y combinar bases de datos elásticas](sql-database-elastic-scale-overview-split-and-merge.md) |

## <a name="summary"></a>Resumen
Los requisitos de aislamiento de inquilinos son importantes para la mayoría de las aplicaciones SaaS multiinquilino. aislamiento de Hello mejor opción tooprovide se basa en gran medida hacia el enfoque de la base de datos por inquilino de Hola. Hello otros dos enfoques requieren inversión en las capas de aplicación compleja que requieran el aislamiento de desarrollo experimentado personal tooprovide, lo que aumenta significativamente el costo y el riesgo. Si no se han ejecutado para requisitos de aislamiento al principio de desarrollo de servicios de hello, la retroadaptados ellos puede ser incluso más costosa en primero dos modelos de Hola. inconvenientes principales Hola asociados con el modelo de base de datos por inquilino Hola son los costos de recursos de nube tooincreased relacionados debido tooreduced de uso compartido y el mantenimiento y administración de varias bases de datos. Los desarrolladores de aplicaciones SaaS tienen a menudo problemas con estos aspectos.

Aunque ventajas e inconvenientes pueden ser principales obstáculos con proveedores de servicios de base de datos en la nube mayoría, base de datos de SQL Azure elimina las barreras de hello con sus capacidades de la base de datos elástica y el grupo elástico. Los programadores de SaaS pueden combinar las características de aislamiento de Hola de un modelo de base de datos por inquilino y optimizar mejoras de facilidad de uso de recursos hello y uso compartido de muchas bases de datos mediante el uso de grupos elásticos y herramientas asociadas.

Los proveedores de aplicaciones multiinquilino sin requisitos de aislamiento de inquilinos y que pueden empaquetar los inquilinos de una base de datos a alta densidad, podrían encontrarse con que los modelos de datos compartidos proporcionan eficacia adicional en el uso compartido de recursos y reducen el costo total. Las herramientas de bases de datos elásticas de Azure SQL Database, las bibliotecas de particionamiento y las características de seguridad ayudan a los proveedores de SaaS a crear y administrar las aplicaciones multiinquilino.

## <a name="next-steps"></a>Pasos siguientes
[Empezar a trabajar con herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md) con una aplicación de ejemplo que muestra la biblioteca de cliente de Hola.

Cree un [panel personalizado de grupo elástico para SaaS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools-custom-dashboard) con una aplicación de ejemplo que use grupos elásticos para una solución de base de datos escalable y rentable.

Usar herramientas de base de datos de SQL Azure Hola demasiado[migrar tooscale de bases de datos existente a](sql-database-elastic-convert-to-use-elastic-tools.md).

toocreate un grupo elástico utilizando hello Azure portal, vea [crear un grupo elástico](sql-database-elastic-pool-manage-portal.md).  

Obtenga información acerca de cómo demasiado[supervisar y administrar un grupo elástico](sql-database-elastic-pool-manage-portal.md).

## <a name="additional-resources"></a>Recursos adicionales

* [Implementación y exploración de una aplicación SaaS multiinquilino que usa Azure SQL Database](sql-database-saas-tutorial.md)
* [¿Qué es un grupo elástico de Azure?](sql-database-elastic-pool.md)
* [Escalado horizontal con Base de datos SQL de Azure](sql-database-elastic-scale-introduction.md)
* [Aplicaciones de múltiples inquilinos con herramientas de bases de datos elásticas y seguridad de nivel de fila](sql-database-elastic-tools-multi-tenant-row-level-security.md)
* [Autenticación en aplicaciones multiinquilino mediante Azure Active Directory y OpenID Connect](../guidance/guidance-multitenant-identity-authenticate.md)
* [Aplicación Tailspin Surveys](../guidance/guidance-multitenant-identity-tailspin.md)


## <a name="questions-and-feature-requests"></a>Preguntas y solicitudes de características

Si tiene preguntas, nosotros buscar en hello [foro de base de datos SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted). Agregar una solicitud de característica en hello [foro de comentarios de la base de datos SQL](https://feedback.azure.com/forums/217321-sql-database/).

