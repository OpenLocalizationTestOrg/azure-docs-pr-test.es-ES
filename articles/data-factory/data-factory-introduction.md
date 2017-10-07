---
title: "aaaIntroduction tooData generador, un servicio de integración de datos | Documentos de Microsoft"
description: "Sepa lo que es Azure Data Factory: un servicio de integración de datos basado en la nube que organiza y automatiza el movimiento y la transformación de datos."
keywords: "integración de datos, integración de datos de nube, qué es azure data factory"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: cec68cb5-ca0d-473b-8ae8-35de949a009e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 4cc30515315efc938951057743ff8eb3701214ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-data-factory"></a>Introducción tooAzure factoría de datos 
## <a name="what-is-azure-data-factory"></a>¿Qué es Azure Data Factory?
¿En Hola a todos de grandes cantidades de datos, cómo se datos existentes aprovecha de empresa? ¿Es datos posibles tooenrich generados en la nube de hello mediante datos de referencia de orígenes de datos locales u otros orígenes de datos dispares? Por ejemplo, una compañía de juegos recopila muchos registros generados por juegos en nube Hola. Desea tooanalyze estas informaciones de toogain registros en las preferencias de toocustomer, datos demográficos, el comportamiento de uso etc. tooidentify subida y ventas cruzadas oportunidades de desarrollar nuevas atractivas de crecimiento del negocio toodrive características y ofrecer una mejor experiencia toocustomers. 

Estos registros, empresa hello tooanalyze necesita que los datos de referencia de hello toouse como información de clientes, información sobre los mismos, información que se encuentra en un almacén de datos local de la campaña de marketing. Por lo tanto, la compañía de hello desea tooingest datos del registro de almacén de datos de nube de Hola y datos de referencia de almacén de datos local de Hola. A continuación, procesar Hola datos mediante el uso de Hadoop en hello (HDInsight de Azure) en la nube y publicación resultados de hello almacenan datos en un almacén de datos en la nube como almacenamiento de datos de SQL Azure o un datos locales, como SQL Server. Desea este toorun de flujo de trabajo semanal una vez. 

¿Qué se necesita es una plataforma que permite Hola empresa toocreate un flujo de trabajo que puede introducir datos tanto local como almacenes de datos en la nube y los datos de transformación o un proceso mediante el uso de los servicios de proceso existentes como Hadoop y publicar Hola resultados tooan local o almacén de datos de tooconsume de aplicaciones de BI en la nube. 

![Introducción a Data Factory](media/data-factory-introduction/what-is-azure-data-factory.png) 

Factoría de datos de Azure es la plataforma de Hola para este tipo de escenarios. Es un **servicio de integración de datos en la nube que le permite toocreate flujos de trabajo de datos en la nube de Hola para orquestar y automatizar el movimiento de datos y transformación de datos**. Con Data Factory de Azure, puede crear y programar controladas por datos flujos de trabajo (denominados canalizaciones) que puede recopilar datos de almacenes de datos dispares, proceso o transformar datos hello mediante el uso de servicios de proceso, como Hadoop de HDInsight de Azure, Spark, Azure Data Lake Análisis y aprendizaje automático de Azure y publicar resultados toodata de datos se almacena como almacenamiento de datos de SQL Azure para tooconsume de las aplicaciones de business intelligence (BI).  

Es más una plataforma Extraer y cargar (EL) y luego Transformar y cargar (TL) que una plataforma tradicional Extraer, transformar y cargar (ETL). transformaciones de Hola que se llevan a cabo están tootransform/procesamiento de datos mediante servicios de proceso en lugar de tooperform las transformaciones, como los de Hola para agregar columnas, contando el número de filas, ordenar datos, etcetera de derivadas. 

Actualmente, de factoría de datos de Azure, los datos de Hola que se usan y generados por los flujos de trabajo están **datos segmenta tiempo** (cada hora, diariamente, semanalmente, etcetera). Por ejemplo, una canalización puede leer datos de entrada, procesar datos y generar datos de salida una vez al día. También puede ejecutar un flujo de trabajo una sola vez.  
  

## <a name="how-does-it-work"></a>¿Cómo funciona? 
las canalizaciones de Hello (flujos de trabajo de datos) de factoría de datos de Azure normalmente realizan Hola siga tres pasos:

![Tres fases de Azure Data Factory](media/data-factory-introduction/three-information-production-stages.png)

### <a name="connect-and-collect"></a>Conectar y recopilar
Las empresas tienen datos de varios tipos ubicados en orígenes dispares. Hello primer paso en la creación de un sistema de producción de información es las tooconnect tooall Hola necesario fuentes de datos y procesamiento, como los servicios de SaaS, recursos compartidos, FTP, web con servicios de archivos y mover Hola datos según convenga tooa centralizada ubicación para posteriores procesamiento.

Sin factoría de datos, las empresas deben crear componentes de movimiento de datos personalizados o escribir toointegrate servicios personalizados estos orígenes de datos y el procesamiento. Es costoso y disco duro toointegrate y mantener estos sistemas, y a menudo carece de nivel empresarial Hola supervisión y alertas y los controles de Hola que puede ofrecer un servicio completamente administrado.

Con el generador de datos, puede usar Hola actividad de copia en una canalización de datos toomove datos desde tanto de forma local y almacén de datos de centralización tooa almacenes de datos origen en la nube de Hola para su posterior análisis en la nube. Por ejemplo, puede recopilar datos en un almacén de Azure Data Lake y transformación Hola de datos más adelante mediante el uso de un servicio de proceso de análisis de Data Lake de Azure. O también puede recopilar los datos en Azure Blob Storage y transformarlos más adelante mediante el uso de un clúster de Hadoop de Azure HDInsight.

### <a name="transform-and-enrich"></a>Transformar y enriquecer
Una vez que los datos están presentes en un almacén de datos centralizado en la nube de hello, desea Hola recopilan datos toobe procesada o transformarse mediante el uso de los servicios de proceso, como Hadoop de HDInsight, Spark, análisis de Data Lake y aprendizaje automático. Desea tooreliably producen transformar datos en un entornos de producción de programación fácil de mantener y controlada toofeed con datos de confianza. 

### <a name="publish"></a>Publicar 
Entregar datos transformados de la nube de hello orígenes tooon locales como SQL Server o conservarla en la nube de orígenes de almacenamiento para su uso por business intelligence (BI) y herramientas de análisis y otras aplicaciones.

## <a name="key-components"></a>Componentes claves
Una suscripción de Azure puede tener una o varias instancias de Azure Data Factory (o factorías de datos). Factoría de datos de Azure se compone de cuatro componentes claves que funcionan conjuntamente tooprovide plataforma de hello en el que puede crear flujos de trabajo de datos con pasos toomove y transformar datos. 

### <a name="pipeline"></a>Canalización
Una factoría de datos puede tener una o más canalizaciones. Una canalización es un grupo de actividades. Juntas, las actividades de hello en una canalización de realizan una tarea. Por ejemplo, una canalización puede contener un grupo de actividades que recopila datos de un blob de Azure y, a continuación, ejecutar una consulta de Hive en un datos de hello toopartition del clúster de HDInsight. ventaja de Hola de esto es que esa canalización Hola permite actividades de hello toomanage como un conjunto en lugar de cada uno de ellos individualmente. Por ejemplo, puede implementar y programar la canalización, hello, en lugar de las actividades de Hola por separado. 

### <a name="activity"></a>Actividad
Una canalización puede tener una o más actividades. Actividades definen Hola acciones tooperform en los datos. Por ejemplo, puede utilizar una toocopy de datos de actividad de copia de almacén de datos de tooanother de almacén de datos. De forma similar, puede usar una actividad de Hive, que se ejecuta una consulta de Hive en un tootransform de clúster de HDInsight de Azure o analizar los datos. Data Factory admite dos tipos de actividades: actividades de movimiento de datos y actividades de transformación de datos.

### <a name="data-movement-activities"></a>Actividades de movimiento de datos
Actividad de copia de factoría de datos copia datos de un almacén de datos de origen datos almacén tooa receptor. Factoría de datos admite Hola siguientes almacenes de datos. Se pueden escribir datos de cualquier origen tooany receptor. Haga clic en un toolearn de almacén de datos cómo toocopy tooand de datos de ese almacén.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

Para más información, consulte el artículo sobre [actividades de movimiento de datos](data-factory-data-movement-activities.md).

### <a name="data-transformation-activities"></a>Actividades de transformación de datos
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

Para más información, consulte el artículo sobre [actividades de transformación de datos](data-factory-data-transformation-activities.md).

### <a name="custom-net-activities"></a>Actividades personalizadas de .NET
Si necesita datos toomove/desde un almacén de datos que la actividad de copia no admite, o transformar datos mediante su propia lógica, cree un **actividad personalizada de .NET**. Consulte el artículo [Uso de actividades personalizadas en una canalización de Data Factory de Azure](data-factory-use-custom-activities.md)para obtener más información sobre la creación y el uso de una actividad personalizada.

### <a name="datasets"></a>Conjuntos de datos
Cada actividad toma cero o más conjuntos de datos como entrada y genera uno o varios conjuntos de datos como salida. Conjuntos de datos representan las estructuras de datos en almacenes de datos de hello, que simplemente seleccione o hacen referencia a datos de Hola que desee toouse en sus actividades como entradas ni salidas. Por ejemplo, un conjunto de datos de Blob de Azure especifica contenedor de blob de Hola y la carpeta en almacenamiento de blobs de Azure Hola desde qué Hola canalización lea datos Hola. O bien, un conjunto de datos de la tabla de SQL Azure especifica actividad hello escribe datos de salida de hello tabla toowhich Hola. 

### <a name="linked-services"></a>Servicios vinculados
Servicios vinculados son muy similares a las cadenas de conexión, que definen la información de conexión de hello necesaria para los recursos de tooexternal tooconnect de factoría de datos. Considerar esta forma: un servicio vinculado define el origen de datos de hello conexión toohello y un conjunto de datos representa la estructura de Hola de datos de Hola. Por ejemplo, un servicio vinculado de almacenamiento de Azure especifica la cuenta de almacenamiento de Azure de toohello de tooconnect de cadena de conexión. Además, un conjunto de datos de Blob de Azure especifica contenedor de blob de Hola y la carpeta de Hola que contiene los datos de Hola.   

Los servicios vinculados se utilizan con dos fines en Data Factory:

* toorepresent una **almacén de datos** incluidos, pero sin limitarse a, un servidor local SQL Server, base de datos de Oracle, recurso compartido de archivos o una cuenta de almacenamiento de blobs de Azure. Vea hello [las actividades de movimiento de datos](#data-movement-activities) sección para obtener una lista de almacenes de datos compatibles.
* toorepresent una **recursos de proceso** que puede hospedar ejecución Hola de una actividad. Por ejemplo, hello HDInsightHive actividad se ejecuta en un clúster de Hadoop de HDInsight. Consulte la sección sobre [actividades de transformación de datos](#data-transformation-activities) para ver una lista de los entornos de procesos admitidos.

### <a name="relationship-between-data-factory-entities"></a>Relación entre las entidades de Data Factory
![Diagrama: Data Factory, un servicio de integración de datos en la nube - conceptos clave](./media/data-factory-introduction/data-integration-service-key-concepts.png)
**Figura 2.** Relaciones entre conjuntos de datos, actividades, canalizaciones y servicios vinculados

## <a name="supported-regions"></a>Regiones admitidas
Actualmente, puede crear generadores de datos en hello **oeste de Estados Unidos**, **UU**, y **Europa del Norte** regiones. Sin embargo, una factoría de datos puede tener acceso a almacenes de datos y servicios en otros datos de toomove de regiones de Azure entre los almacenes de datos de proceso o procesamiento de datos con servicios de proceso.

Azure Data Factory no almacena ningún dato. Le permite crear flujos de trabajo de datos tooorchestrate movimiento de datos entre [admite almacenes de datos](#data-movement-activities) y el procesamiento de datos mediante [servicios de proceso](#data-transformation-activities) en otras regiones o en local entorno. También permite demasiado[supervisar y administrar flujos de trabajo](data-factory-monitor-manage-pipelines.md) mediante programación y mecanismos de interfaz de usuario.

Aunque factoría de datos solo está disponible en **oeste de Estados Unidos**, **UU**, y **Europa del Norte** regiones, servicio de hello activando el movimiento de datos de Hola de factoría de datos está disponible [global](data-factory-data-movement-activities.md#global) en varias regiones. Si un almacén de datos está protegido por un firewall, un [Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) instalados en sus entorno local mueve los datos hello en su lugar.

Por ejemplo, supongamos que sus entornos de proceso, tales como clúster de Azure HDInsight y Azure Machine Learning, se ejecutan fuera de la región de Europa Occidental. Puede crear y utilizar una instancia de la factoría de datos de Azure en Europa del Norte y usar trabajos tooschedule en los entornos de proceso en Europa occidental. Tarda unos pocos milisegundos para trabajo de hello tootrigger factoría de datos en su entorno de proceso pero Hola hora para ejecutar el trabajo de hello en el entorno informático no cambia.

## <a name="get-started-with-creating-a-pipeline"></a>Introducción a la creación de una canalización
Puede usar una de esas herramientas o las canalizaciones de datos de las API toocreate de factoría de datos de Azure: 

- Azure Portal
- Visual Studio
- PowerShell
- API de .NET
- API de REST
- Plantilla de Azure Resource Manager. 

toolearn cómo canalizaciones toobuild factorías de datos con datos, siga las instrucciones paso a paso de hello tutoriales:

| Tutorial | Descripción |
| --- | --- |
| [Movimiento de datos entre dos almacenes de datos en la nube](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) |En este tutorial, creará una factoría de datos con una canalización que **mueve datos** de base de datos de tooSQL de almacenamiento de blobs. |
| [Transformar datos usando el clúster de Hadoop](data-factory-build-your-first-pipeline.md) |En este tutorial, va a crear su primera instancia de Azure Data Factory con una canalización de datos que **procesa los datos** ejecutando el script de Hive en un clúster de Azure HDInsight (Hadoop). |
| [Movimiento de datos entre un almacén de datos local y un almacén de datos en la nube con Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) |En este tutorial, va a crear una factoría de datos con una canalización que **mueve datos** desde una **local** tooan de base de datos de SQL Server blobs de Azure. Como parte del tutorial de hello, instalar y configurar Hola Data Management Gateway en su equipo. |
