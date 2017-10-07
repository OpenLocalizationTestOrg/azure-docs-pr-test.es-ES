---
title: aaaScaling out con base de datos de SQL de Azure | Documentos de Microsoft
description: "Software que los desarrolladores de un servicio (SaaS) puede crear fácilmente elástico, bases de datos escalables en hello mediante estas herramientas en la nube"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: d15a2e3f-5adf-41f0-95fa-4b945448e184
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: 82a561e07389d8619727a540fa9424248c087eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-out-with-azure-sql-database"></a>Escalado horizontal con Base de datos SQL de Azure
Puede escalar fácilmente bases de datos de SQL Azure mediante hello **bases de datos elásticas** herramientas. Estas herramientas y características le permiten usar Hola prácticamente ilimitada recursos de la base de datos **base de datos de SQL Azure** toocreate soluciones para cargas de trabajo transaccionales y especialmente Software como aplicaciones de servicio (SaaS). Características de base de datos elásticos se componen de siguiente hello:

* [Biblioteca de cliente de base de datos elástica](sql-database-elastic-database-client-library.md): biblioteca de cliente de hello es una característica que permite toocreate y mantener bases de datos particionadas.  Consulte [Introducción a las herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md).
* [Herramienta de división y combinación de Base de datos elástica](sql-database-elastic-scale-overview-split-and-merge.md): mueve datos entre bases de datos particionadas. Esto es útil para mover los datos de varios inquilinos base de datos tooa único inquilino base de datos (o viceversa). Consulte el [tutorial de la herramienta de división y combinación de Base de datos elástica](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
* [Trabajos de base de datos elásticos](sql-database-elastic-jobs-overview.md) (versión preliminar): Use trabajos toomanage gran número de bases de datos SQL de Azure. Realice fácilmente operaciones administrativas, como cambios de esquema, administración de credenciales, actualizaciones de datos de referencia, recopilación de datos de rendimiento o de trabajos de recolección de telemetría de inquilinos (cliente).
* [Consulta de base de datos elástica](sql-database-elastic-query-overview.md) (versión preliminar): permite consulta toorun Transact-SQL que abarca varias bases de datos. Esto habilita las herramientas de tooreporting de conexión, como Excel, Power BI, Tableau, etcetera.
* [Las transacciones elásticas](sql-database-elastic-transactions-overview.md): esta característica permite las transacciones de toorun que abarcan varias bases de datos en la base de datos de SQL Azure. Las transacciones de base de datos elástica están disponibles para aplicaciones .NET mediante ADO .NET e integrar con experiencia de programación familiar hello mediante hello [System.Transaction clases](https://msdn.microsoft.com/library/system.transactions.aspx).

gráfico de Hello siguiente muestra una arquitectura que incluye hello **características de base de datos elástica** en colección de relaciones tooa de bases de datos.

En este gráfico, los colores de la base de datos de hello representan esquemas. Las bases de datos con hello mismo recurso compartido de color Hola mismo esquema.

1. Un conjunto de **bases de datos de SQL de Azure** se hospedan en Azure con la arquitectura de particionamiento.
2. Hola **biblioteca de cliente de base de datos elástica** se establece toomanage usa una partición.
3. Un subconjunto de las bases de datos de Hola se colocan en un **grupo elástico**. (Consulte [¿Qué es un grupo?](sql-database-elastic-pool.md)).
4. Un **trabajo de Elastic Database** ejecuta scripts de T-SQL programados o ad-hoc en todas las bases de datos.
5. Hola **herramienta Dividir-combinar** son datos de uso toomove de tooanother de una partición.
6. Hola **consulta de base de datos elástica** permite toowrite una consulta que abarca todas las bases de datos en el conjunto de particiones de Hola.
7. **Las transacciones elásticas** permite las transacciones de toorun que abarcan varias bases de datos. 

![Herramientas de Base de datos elástica][1]

## <a name="why-use-hello-tools"></a>¿Por qué usar herramientas de hello?
Dotar de capacidad de ampliación y escalabilidad a las aplicaciones en la nube ha sido sencillo para el almacenamiento de blobs y las máquinas virtuales; basta con sumar o restar unidades, o bien con aumentar la potencia. Pero sigue siendo un desafío para el procesamiento de datos con estado en bases de datos relacionales. Estos son los desafíos que han surgido en estos escenarios:

* Aumentar y reducir la capacidad de parte de la base de datos relacional de hello de la carga de trabajo.
* La administración de las zonas activas puede afectar a un subconjunto específico de datos, como un usuario final (inquilino) particularmente ocupado.

Tradicionalmente, se han abordado escenarios como estos invirtiendo en aplicaciones de Hola de toosupport de servidores de bases de datos de gran escala. Sin embargo, esta opción está limitada en la nube de Hola donde todo el procesamiento se produce en hardware estándar predefinidas. En su lugar, la distribución de datos y que se procesan en muchas bases de datos estructurados exactamente igual (un modelo de escalabilidad horizontal conocido como "particionamiento") proporciona una alternativa tootraditional enfoques de escalado vertical tanto en términos de costo y elasticidad.

## <a name="horizontal-and-vertical-scaling"></a>Escalado horizontal y vertical
Hola siguiente ilustración muestra hello dimensiones horizontal y vertical de ajuste de escala, que son maneras básicas de Hola se pueden escalar las bases de datos elástica Hola.

![Escalado horizontal frente a vertical][2]

Escalado horizontal refiere tooadding o quitar las bases de datos en el rendimiento general o capacidad de tooadjust de orden. También se denomina "escalado horizontal". El particionamiento, en el que los datos se dividen a través de una colección de bases de datos estructurados exactamente igual, es un común tooimplement de manera horizontal ajuste de escala.  

Escalado vertical refiere tooincreasing o disminuir el nivel de rendimiento de Hola de una base de datos individual, esto también se conoce como "escalado."

La mayoría de las aplicaciones de bases de datos a escala de la nube usarán una combinación de estas dos estrategias. Por ejemplo, puede usar un Software como una aplicación de servicio horizontal escala tooprovision nuevo a los clientes finales y vertical escalado tooallow recursos bases de datos toogrow o reducir de cada cliente final según sea necesario por carga de trabajo de Hola.

* Escalado horizontal se administra con hello [biblioteca de cliente de base de datos elástica](sql-database-elastic-database-client-library.md).
* Escalado vertical se realiza mediante el nivel de servicio de Azure PowerShell cmdlets toochange hello, o mediante la colocación de las bases de datos en un grupo elástico.

## <a name="sharding"></a>Clave de particionamiento
*Particionamiento* es una técnica toodistribute grandes cantidades de datos estructurados de forma idéntica en varias bases de datos independientes. Su uso se ha extendido entre los desarrolladores de nube que crean ofertas de software como servicio (SAAS) para empresas o clientes finales. Estos clientes finales son a menudo tooas que se hace referencia "inquilinos". El particionamiento puede ser necesario por diversos motivos:  

* cantidad total de Hola de datos es demasiado grande toofit dentro de los límites de Hola de una sola base de datos
* rendimiento de las transacciones Hola de hello carga de trabajo general excede las capacidades de Hola de una sola base de datos
* Los inquilinos pueden requerir el aislamiento físico entre sí, por lo que se necesitan bases de datos independientes para cada inquilino
* Diferentes secciones de una base de datos pueden necesitar tooreside en regiones geográficas diferentes para cumplimiento de normas, el rendimiento o motivos geopolíticos.

En otros escenarios, como la recopilación de datos de los dispositivos distribuidos, particionamiento puede ser toofill usa un conjunto de bases de datos que se organizan temporalmente. Por ejemplo, una base de datos independiente se puede destinar tooeach día o una semana. En ese caso, clave de particionamiento de hello puede ser una fecha de Hola que representan de entero (está presente en todas las filas de tablas particionadas Hola) y las consultas que recuperan información de un intervalo de fechas deben enrutarse por subconjunto de toohello de aplicación Hola de bases de datos que abarca el intervalo de hello en pregunta.

Particionamiento funciona mejor cuando todas las transacciones en una aplicación pueden ser restringido tooa único valor de una clave de particionamiento. Que se garantiza que todas las transacciones se tooa local de base de datos específica.

## <a name="multi-tenant-and-single-tenant"></a>De un solo inquilino y multiinquilino
Algunas aplicaciones usan el enfoque más sencillo de Hola de creación de una base de datos independiente para cada inquilino. Se trata de hello **patrón de particionamiento de un solo inquilino** que proporciona aislamiento, capacidad de copia de seguridad/restauración y recurso de ajuste de escala con una granularidad de Hola de inquilino de Hola. Con el particionamiento de un solo inquilino, cada base de datos está asociado con un valor de identificador específicos del inquilino (o valor de clave de cliente), pero no siempre debe presente en los propios datos Hola esa clave. Se Hola tooroute de responsabilidad de la aplicación cada solicitud toohello base de datos adecuada - y biblioteca de cliente de hello puede simplificar este proceso.

![Un solo inquilino frente a multiinquilinos][4]

Otros escenarios empaquetan varios inquilinos juntos en bases de datos, en lugar de aislarlos en bases de datos independientes. Esto es común en **patrón de particionamiento de varios inquilinos** - y pueden estar dirigida por hecho de Hola que una aplicación administra grandes cantidades de inquilinos muy pequeños. En el particionamiento de varios inquilinos, filas de hello en tablas de base de datos de hello están diseñados toocarry una clave que identifica la clave de particionamiento o de Id. de inquilino de Hola. De nuevo, capa de aplicación hello es responsable de enrutar la base de datos de un inquilino solicitud toohello adecuada y esto puede ser compatibles con la biblioteca de cliente de base de datos elástica Hola. Además, seguridad de nivel de fila puede ser usado toofilter las filas que se puede tener acceso cada inquilino - para obtener más información, consulte [aplicaciones de varios inquilinos con las herramientas de bases de datos elásticas y seguridad de nivel de fila](sql-database-elastic-tools-multi-tenant-row-level-security.md). Redistribución de datos entre bases de datos puede resultar necesario con el patrón de particionamiento de varios inquilinos de Hola y esto se realiza mediante la herramienta Dividir-combinar de hello elástico de base de datos. toolearn más información acerca de los patrones de diseño para aplicaciones de SaaS con grupos elásticos, consulte [patrones de diseño para aplicaciones de SaaS multiempresa con base de datos de SQL Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).

### <a name="move-data-from-multiple-toosingle-tenancy-databases"></a>Mover los datos de varias bases de datos de inquilinos toosingle
Al crear una aplicación de SaaS, es típico toooffer posibles clientes una versión de prueba de Hola software. En este caso, resulta rentable toouse una base de datos de varios inquilinos para datos de Hola. Sin embargo, cuando un cliente potencial se convierte en un cliente, una base de datos de inquilino único es mejor, puesto que ofrece un mejor rendimiento. Si cliente hello había creado datos durante el período de prueba de hello, use hello [herramienta Dividir-combinar](sql-database-elastic-scale-overview-split-and-merge.md) toomove datos Hola Hola multiempresa toohello nueva único inquilino base de datos.

## <a name="next-steps"></a>Pasos siguientes
Para una aplicación de ejemplo que muestra la biblioteca de cliente de hello, consulte [empezar a trabajar con herramientas de base de datos elástica](sql-database-elastic-scale-get-started.md).

herramientas de hello toouse tooconvert existente las bases de datos, vea [tooscale horizontal existente migrar las bases de datos](sql-database-elastic-convert-to-use-elastic-tools.md).

detalles de hello toosee de grupo elástico de hello, consulte [consideraciones de precio y el rendimiento para un grupo elástico](sql-database-elastic-pool.md), o crear un nuevo grupo con [grupos elásticos](sql-database-elastic-pool-manage-portal.md).  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-introduction/tools.png
[2]:./media/sql-database-elastic-scale-introduction/h_versus_vert.png
[3]:./media/sql-database-elastic-scale-introduction/overview.png
[4]:./media/sql-database-elastic-scale-introduction/single_v_multi_tenant.png

