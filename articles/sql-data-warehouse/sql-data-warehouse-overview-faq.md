---
title: "aaaAzure SQL datos de almacenamiento de las preguntas más frecuentes | Documentos de Microsoft"
description: "En este artículo se muestran las preguntas más frecuentes sobre Azure SQL Data Warehouse para clientes y desarrolladores"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 09fd3f65d9507b09fcb8f477742c7d020add2755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a>Preguntas más frecuentes de SQL Data Warehouse

## <a name="general"></a>General

P: ¿Qué ofrece SQL Data Warehouse en cuanto a seguridad de datos?

A. SQL Data Warehouse ofrece varias soluciones para proteger datos, como TDE y la auditoría. Para obtener más información, consulte [Seguridad].

P: ¿Dónde puedo encontrar los estándares empresariales o legales que cumple SQL Data Warehouse?

A. Visite hello [Microsoft Compliance] página para diversas ofertas de cumplimiento por producto como SOC e ISO. Primero elija por título de cumplimiento de normas, a continuación, expanda Azure en hello Microsoft en el ámbito en la nube servicios en el lado derecho de Hola de hello página toosee qué servicios son servicios de Azure es compatibles.

P: ¿Puedo conectar Power BI?

A. Sí. Aunque Power BI admite la consulta directa con SQL Data Warehouse, no se ha diseñado para administrar gran cantidad de usuarios o datos en tiempo real. Para usar Power BI con fines de producción, se recomienda usar Power BI sobre IaaS de servicio de análisis o Azure Analysis Services. 

P: ¿Qué son los límites de capacidad de SQL Data Warehouse?

A. Consulte nuestra página de [límites de capacidad] actuales. 

P: ¿Por qué tardan tanto tiempo en completarse las operaciones de escalado, pausar y reanudación?

A. Una serie de factores puede influir en tiempo de presentación para las operaciones de administración de proceso. Un caso habitual de operaciones de ejecución prolongada es la reversión de transacciones. Cuando se inicia una operación de escalado o pausa, se bloquean todas las sesiones entrantes y se purgan las consultas. En el sistema de hello pedidos tooleave en un estado estable, se deben poner las transacciones antes de que pueda comenzar una operación. Hola mayor número de Hola y de mayor tamaño del registro de hello de transacciones, se detenido a operación de hello más hello de restaurar el estado estable de hello sistema tooa.

## <a name="user-support"></a>Asistencia técnica de usuario

P: Tengo una solicitud de característica, ¿dónde puede enviarla?

A. Si tiene una solicitud de característica, envíala a nuestra página [UserVoice].

P: ¿Cómo puedo hacer una determinada acción?

A. Para obtener ayuda con las tareas de desarrollo con SQL Data Warehouse, puede hacer preguntas en nuestra [Stack Overflow]. 

P: ¿Cómo puedo enviar una vale de asistencia técnica?

A. Los [vales de asistencia técnica] puede presentarse a través de Azure Portal.

## <a name="sql-languagefeature-support"></a>Compatibilidad con características o lenguajes de SQL 

P: ¿Qué tipos de datos admite SQL Data Warehouse?

A. Vea los [tipos de datos] de SQL Data Warehouse.

P: ¿Qué características de tablas se admiten?

A. Aunque SQL Data Warehouse es compatible con muchas características, algunas no se admiten y se documentan en la página sobre [características de tablas no admitidas].

## <a name="tooling-and-administration"></a>Administración y herramientas

P: ¿Se admiten proyectos de bases de datos en Visual Studio?

A. En estos momentos, no admitimos proyectos de bases de datos en Visual Studio para SQL Data Warehouse. Si desea que toocast un voto tooget esta característica, visite nuestro User Voice [solicitud de características de proyectos de base de datos].

P: ¿SQL Data Warehouse admite las API de REST?

A. Sí. La mayoría de las funciones REST que se pueden utilizar con la base de datos SQL también están disponibles con SQL Data Warehouse. Puede encontrar información sobre las API en las páginas de documentación de REST o [MSDN].


## <a name="loading"></a>Carga

P: ¿Qué controladores de cliente se admiten?

A. Compatibilidad con controladores de almacenamiento de datos puede encontrarse en hello [las cadenas de conexión] página

P.: ¿Qué formatos de archivo admite PolyBase con SQL Data Warehouse?

R.: Orc, RC, Parquet y texto delimitado sin formato.

P: ¿qué puede conectar toofrom de almacenamiento de datos de SQL con PolyBase? 

R.: [Azure Data Lake Store] e instancias de [Azure Storage Blobs].

P: ¿es posible aplicación de cálculo cuando se conecte tooAzure Blobs de almacenamiento o ADLS? 

R: no, PolyBase de almacenamiento de datos de SQL interactúa sólo los componentes de almacenamiento de Hola. 

P: ¿puedo conectarme tooHDI?

R: HDI sirve como capa HDFS hello ADLS o WASB. Si tiene uno de los dos como la capa HDFS, puede cargar datos en SQL Data Warehouse. Sin embargo, no se puede generar la instancia HDI de toohello de cálculo de la aplicación. 

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre SQL Data Warehouse, vea nuestra página [Introducción].


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[las cadenas de conexión]: ./sql-data-warehouse-connection-strings.md
[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[vales de asistencia técnica]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Seguridad]: ./sql-data-warehouse-overview-manage-security.md
[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[límites de capacidad]: ./sql-data-warehouse-service-capacity-limits.md
[tipos de datos]: ./sql-data-warehouse-tables-data-types.md
[características de tablas no admitidas]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[Azure Storage Blobs]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[solicitud de características de proyectos de base de datos]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[Introducción]: ./sql-data-warehouse-overview-faq.md