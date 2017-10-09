---
title: "¿aaaWhat es el almacenamiento de datos de SQL Azure? | Microsoft Docs"
description: "Base de datos distribuida de clase empresarial, capaz de procesar volúmenes de petabytes de datos relacionales y no relacionales. Es con grow de la primera almacenamiento de datos en la nube del sector de hello, reducir y hacer una pausa en segundos."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: bjhubbard
editor: 
ms.assetid: 4006c201-ec71-4982-b8ba-24bba879d7bb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 2/28/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 5fefe40879230f123c2e4a90b9c20a35779cf711
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-sql-data-warehouse"></a>¿Qué es Almacenamiento de datos SQL de Azure?
Azure SQL Data Warehouse es una base de datos relacional, de escalado horizontal, basada en la nube y de procesamiento paralelo masivo (MPP), capaz de procesar volúmenes masivos de datos. 

Almacenamiento de datos SQL

* Combina la base de datos relacional SQL Server de hello con capacidades de escalado horizontal de nube de Azure. 
* Separa el almacenamiento del proceso.
* Habilita el aumento, la disminución, la pausa o la reanudación del proceso. 
* Se integra en hello plataforma Windows Azure.
* Utiliza SQL Server Transact-SQL (T-SQL) y sus herramientas.
* Cumple con distintos requisitos de seguridad legales y empresariales como SOC e ISO.

Este artículo describen las principales características de Hola de almacenamiento de datos SQL.

## <a name="massively-parallel-processing-architecture"></a>Arquitectura de procesamiento paralelo masivo
El Almacenamiento de datos SQL es un sistema de base de datos distribuidas de procesamiento masivo en paralelo (MPP). Entre bastidores de hello, almacenamiento de datos SQL se propaga a los datos en varios almacenamiento sin elementos compartidos y unidades de procesamiento. Hola datos se almacenan en una capa de almacenamiento con redundancia local Premium encima de las cuales los nodos de cálculo vinculados dinámicamente ejecutan consultas. Carga un toorunning de enfoque "divide y vencerás" de toma de almacenamiento de datos SQL y las consultas complejas. Las solicitudes se reciben un nodo de Control, optimizado para la distribución y, a continuación, pasa tooCompute nodos toodo su trabajo en paralelo.

Con el almacenamiento y el proceso separados, SQL Data Warehouse hace lo siguiente:

* Aumentar o reducir el tamaño del almacenamiento independiente del proceso.
* Aumentar o reducir la capacidad de proceso sin mover datos.
* Pausar la capacidad de proceso mientras se dejan los datos intactos, solo se paga por el almacenamiento.
* Reanudar la capacidad de proceso durante las horas operativas.

Hello siguiente diagrama muestra la arquitectura de hello con más detalle.

![Arquitectura de Almacenamiento de datos SQL][1]

**Nodo de control:** nodo de Control de hello administra y optimiza las consultas. Es Hola front-end que interactúa con todas las aplicaciones y las conexiones. En el almacén de datos de SQL, nodo de Control de hello funciona con la base de datos de SQL y conecta tooit busca y siente Hola igual. En la superficie de hello, nodo de Control de hello coordina todos los movimientos de datos de Hola y cálculo requerido toorun consultas en paralelo en los datos distribuidos. Cuando se envía una tooSQL de consulta de T-SQL almacenamiento de datos, nodo de Control de Hola transforma en separar las consultas que se ejecutan en cada nodo de ejecución en paralelo.

**Nodos de proceso:** nodos de proceso de hello actúan como power Hola detrás de almacenamiento de datos SQL. Son bases de datos SQL que almacenan los datos y procesan la consulta. Al agregar datos, almacenamiento de datos SQL distribuye los nodos de proceso de hello filas tooyour. nodos de proceso de Hello son trabajadores de Hola que se ejecutan las consultas en paralelo hello en los datos. Después del procesamiento, pasan el nodo de Control de hello resultados toohello atrás. consulta de hello toofinish, nodo de Control de hello agrega resultados de Hola y devuelve Hola resultado final.

**Almacenamiento:** los datos se almacenan en Almacenamiento de blobs de Azure. Cuando los nodos de proceso interactúan con los datos, se escribir y leer tooand directamente desde el almacenamiento de blobs. Puesto que el almacenamiento de Azure se expande transparente y ampliamente, almacenamiento de datos SQL puede hacer Hola igual. Puesto que el proceso y el almacenamiento son independientes, Almacenamiento de datos SQL puede escalar automáticamente el almacenamiento por separado del escalado del proceso, y viceversa. Almacenamiento de blobs de Azure también está totalmente tolerante a errores y optimiza Hola copia de seguridad y proceso de restauración.

**Servicio de movimiento de datos:** servicio de movimiento de datos (DMS) mueve datos entre los nodos de Hola. DMS proporciona nodos de proceso de hello acceso toodata que necesitan para combinaciones y agregaciones. DMS no es un servicio de Azure Es un servicio de Windows que se ejecuta junto con la base de datos SQL en todos los nodos de Hola. DMS es un proceso en segundo plano con el que no se va a interactuar directamente. Sin embargo, puede mirar planes de consultas toosee cuando se producen las operaciones DMS, puesto que el movimiento de datos es necesario toorun cada consulta en paralelo.

## <a name="optimized-for-data-warehouse-workloads"></a>Optimizado para cargas de trabajo de almacenamiento de datos
Hola enfoque MPP le resultará más fácil por varias optimizaciones de rendimiento específicos, incluida la de almacenamiento de datos:

* Un optimizador de consultas distribuido y un conjunto de estadísticas complejas en todos los datos. Con información sobre la distribución y el tamaño de los datos, servicio de hello es capaz de toooptimize consultas al evaluar el costo de Hola de operaciones de consulta distribuida específica.
* Algoritmos avanzados y técnicas integran en datos de hello tooefficiently mover datos de movimiento proceso entre los recursos informáticos como consulta de hello tooperform necesarios. Estas operaciones de movimiento de datos se compilan, y todas las optimizaciones toohello Data Movement Service se producen automáticamente.
* Índices de **columnstore** agrupado de manera predeterminada. Mediante el uso de almacenamiento basado en columnas, almacenamiento de datos SQL obtiene por término medio 5 relación de compresión de x con el almacenamiento tradicional orientado por filas y seguridad too10x o más mejoras de rendimiento de consulta. Las consultas de análisis que requieran tooscan un gran número de filas funcione mejor con índices de almacén de columnas.


## <a name="predictable-and-scalable-performance-with-data-warehouse-units"></a>Rendimiento predecible y escalable con unidades de almacenamiento de datos
SQL Data Warehouse se genera con tecnologías similares a SQL Database, lo que significa que los usuarios pueden esperar un rendimiento coherente y predecible para las consultas analíticas. Los usuarios deben deberá esperar a escala de rendimiento toosee linealmente ya que agregar o quitar nodos de proceso. Asignación de recursos tooyour almacenamiento de datos SQL se mide en unidades de almacenamiento de datos (a Dwu). A Dwu es una medida de recursos subyacentes como la CPU, memoria, e/s por segundo, que se asignan tooyour almacenamiento de datos SQL. Número de Hola de a Dwu si aumenta los recursos y rendimiento. En concreto, las DWU ofrecen las siguientes garantías:

* Es capaz de tooscale el almacén de datos sin preocuparse por software o hardware subyacentes Hola.
* Es posible predecir la mejora del rendimiento para un nivel de unidad antes de cambiar el proceso de Hola de su almacén de datos.
* Hello hardware y software de la instancia subyacente pueden cambiar o mover sin que ello afecte el rendimiento de la carga de trabajo.
* Microsoft puede mejorar Hola subyacente arquitectura del servicio de hello sin afectar al rendimiento de saludo de la carga de trabajo.
* Microsoft rápidamente puede mejorar el rendimiento en el almacén de datos de SQL, de forma que sea escalable y uniformemente efectos Hola sistema.

Las Unidades de almacenamiento de datos proporcionan una medida de tres métricas que están muy correlacionadas con el rendimiento de la carga de trabajo del almacenamiento de datos. siguientes de Hello clave escala de las métricas de carga de trabajo linealmente con a Dwu Hola.

**Examen y agregación:** consulta de almacenamiento de datos estándar que examina un gran número de filas y realiza después una agregación compleja. Se trata de una operación de gran consumo de E/S y CPU.

**Carga:** Hola datos tooingest de capacidad en el servicio de Hola. Las cargas se ejecutan mejor con PolyBase de Azure Storage Blob o Azure Data Lake. Esta métrica es red toostress diseñada y aspectos de la CPU del servicio de Hola.

**Crear tabla como Select (CTAS):** CTAS mide Hola capacidad toocopy una tabla. Esto implica la lectura de datos de almacenamiento, distribuir entre nodos de hello de dispositivo de Hola y escribir toostorage de nuevo. Se trata de una operación con un uso intensivo de CPU, E/S y red.

## <a name="built-on-sql-server"></a>Creado sobre SQL Server
Almacenamiento de datos de SQL se basa en el motor de base de datos relacional de SQL Server de hello e incluye muchas características de Hola que espera de un almacén de datos de empresa. Si ya sabe T-SQL, resulta fácil tootransfer su tooSQL conocimiento del almacenamiento de datos. Si van a adelantar o introducción, ejemplos de Hola a través de la documentación de hello le ayudará a empezar. En general, puede pensar en forma de Hola que nos hemos generar elementos del lenguaje Hola de almacenamiento de datos de SQL como sigue:

* Almacenamiento de datos SQL emplea sintaxis de T-SQL para muchas operaciones. También admite un amplio conjunto de construcciones SQL tradicionales, como procedimientos almacenados, funciones definidas por el usuario, partición de tabla, índices e intercalaciones.
* SQL Data Warehouse también contiene varias características recientes de SQL Server, como los índices **columnstore** agrupados, la integración de PolyBase y la auditoría de datos (junto con la evaluación de amenazas).
* Ciertos elementos del lenguaje T-SQL que son menos habituales para las cargas de trabajo de almacenamiento de datos, o que son más recientes tooSQL Server, no esté disponibles actualmente. Para obtener más información, vea hello [documentación sobre migración][Migration documentation].

Con compatibilidad de características entre SQL Server, almacenamiento de datos SQL, base de datos SQL y sistema de la plataforma de análisis y Hola Transact-SQL, puede desarrollar una solución que satisface sus necesidades de datos. Puede decidir donde tookeep los datos, basándose en el rendimiento, seguridad y requisitos de escala y, a continuación, transferir los datos según sea necesario entre distintos sistemas.

## <a name="data-protection"></a>Protección de datos
Almacenamiento de datos SQL almacena todos los datos en Azure Premium mediante el almacenamiento con redundancia local. Varias copias sincrónicas de datos de Hola se mantienen en hello protección de datos local center tooguarantee transparente de los datos frente a errores localizados. Además, SQL Data Warehouse realiza automáticamente una copia de seguridad de las bases de datos activas (no en pausa) a intervalos periódicos mediante instantáneas de Azure Storage. toolearn más información sobre cómo una copia de seguridad y restauración funciona, vea hello [información general de copia de seguridad y restauración][Backup and restore overview].

## <a name="integrated-with-microsoft-tools"></a>Integrado con herramientas de Microsoft
Almacenamiento de datos SQL integra muchas de las herramientas de Hola que pueden estar familiarizados con los usuarios de SQL Server. Estas herramientas son:

**Herramientas tradicionales de SQL Server:** Almacenamiento de datos SQL se integra totalmente con SQL Server Analysis Services, Integration Services y Reporting Services.

**Herramientas basadas en la nube:** SQL Data Warehouse se puede integrar con varios servicios de Azure, como Data Factory, Stream Analytics, Machine Learning y Power BI. Para ver una lista completa, consulte la [información general sobre las herramientas integradas][Integrated tools overview].

**Herramientas de terceros:** muchos proveedores de herramientas de terceros ha certificado la integración de sus herramientas con SQL Data Warehouse. Para ver una lista completa, consulte los [asociados de soluciones de SQL Data Warehouse][SQL Data Warehouse solution partners].

## <a name="hybrid-data-sources-scenarios"></a>Escenarios de orígenes de datos híbridos
Polybase le permite tooleverage los datos de orígenes diferentes mediante el uso de comandos de T-SQL conocidos. Polybase le permite tooquery datos no relacionales contenidos en almacenamiento de blobs de Azure como si fuera una tabla normal. Usar datos de Polybase tooquery no relacionales o datos no relacionales tooimport en almacenamiento de datos de SQL.

* PolyBase usa datos no relacionales de tooaccess de tablas externas. las definiciones de tabla de Hola se almacenan en el almacén de datos de SQL y puede tener acceso a ellos mediante el uso de SQL y herramientas, como obtendría acceso a datos relacionales normales.
* Polybase es independiente en su integración. Se expone Hola características similares y orígenes de hello tooall de funcionalidad que admite. datos de Hello leídos por Polybase pueden estar en diversos formatos, incluidos archivos delimitados o ORC.
* PolyBase puede ser tooaccess usa almacenamiento de blobs que también es que se va a usar como almacenamiento para un clúster de HDInsight. Este proporciona acceso toohello mismos datos con herramientas relacionales y no relacionales.

## <a name="sla"></a>Contrato de nivel de servicio
SQL Data Warehouse ofrece un acuerdo de nivel de servicio (SLA) de nivel de producto como parte del SLA de Microsoft Online Services. Para más información, visite [SLA para SQL Data Warehouse][SLA for SQL Data Warehouse]. Para obtener información de SLA sobre todos los otros productos pueden visitar hello [contratos de nivel de servicio] Azure página o descargarlos en hello [licencias por volumen] [ Volume Licensing] página. 

## <a name="next-steps"></a>Pasos siguientes
Ahora que ya conoce un poco acerca de almacenamiento de datos SQL, obtenga información acerca de cómo tooquickly [crear un almacén de datos de SQL] [ create a SQL Data Warehouse] y [cargar datos de ejemplo][load sample data]. Si es nuevo tooAzure, es posible hello [Glosario de Azure] [ Azure glossary] útiles que se pueden encontrar términos nuevos. O bien, examine algunos de estos otros recursos de SQL Data Warehouse.  

* [Casos de éxito de clientes]
* [Blogs]
* [Solicitud de función]
* [Vídeos]
* [Blogs de Customer Advisory Team]
* [Creación de una incidencia de soporte técnico]
* [Foro de MSDN]
* [Foro Stack Overflow]
* [Twitter]

<!--Image references-->
[1]: ./media/sql-data-warehouse-overview-what-is/dwarchitecture.png

<!--Article references-->
[Creación de una incidencia de soporte técnico]: ./sql-data-warehouse-get-started-create-support-ticket.md
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md
[Migration documentation]: ./sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[Integrated tools overview]: ./sql-data-warehouse-overview-integrate.md
[Backup and restore overview]: ./sql-data-warehouse-restore-database-overview.md
[Azure glossary]: ../azure-glossary-cloud-terminology.md

<!--MSDN references-->

<!--Other Web references-->
[Casos de éxito de clientes]: https://azure.microsoft.com/case-studies/?service=sql-data-warehouse
[Blogs]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[Blogs de Customer Advisory Team]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Solicitud de función]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[Foro de MSDN]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureSQLDataWarehouse
[Foro Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Vídeos]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
[SLA for SQL Data Warehouse]: https://azure.microsoft.com/en-us/support/legal/sla/sql-data-warehouse/v1_0/
[Volume Licensing]: http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=37
[contratos de nivel de servicio]: https://azure.microsoft.com/en-us/support/legal/sla/
