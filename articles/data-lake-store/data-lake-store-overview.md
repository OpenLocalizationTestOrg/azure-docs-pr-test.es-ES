---
title: "aaaOverview de almacén de Azure Data Lake | Documentos de Microsoft"
description: "Comprender qué es el valor de hello y almacén de Data Lake de Azure proporciona a través de otros almacenes de datos"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: b3475057-9427-4492-a3af-25a802a23a79
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 5a60a6b86a51c44647cf4ee168fb333d1c37b1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-data-lake-store"></a>Información general del Almacén de Azure Data Lake
El Almacén de Azure Data Lake es un repositorio de gran escala en toda la empresa para cargas de trabajo de análisis de macrodatos. Azure Data Lake permite toocapture datos de cualquier velocidad de ingesta, tamaño y tipo en un solo lugar para análisis operativos y exploratorios.

> [!TIP]
> Hola de uso [ruta de acceso de aprendizaje de almacén de Data Lake](https://azure.microsoft.com/documentation/learning-paths/data-lake-store-self-guided-training/) toostart explorar el servicio de almacén de Azure Data Lake Hola.
> 
> 

Almacén de Data Lake de Azure puede tener acceso desde Hadoop (disponible con clúster de HDInsight) utilizando Hola WebHDFS compatible con las API de REST. Está específicamente diseñado tooenable analizar los datos de hello almacenan y se optimizan para el rendimiento en escenarios de análisis de datos. Fuera del cuadro de hello, incluye todas las funcionalidades de nivel empresarial de hello, seguridad, facilidad de uso, escalabilidad, confiabilidad y disponibilidad, esenciales para casos de uso empresarial del mundo real.

![Azure Data Lake](./media/data-lake-store-overview/data-lake-store-concept.png)

Algunas de las capacidades clave de Hola de hello Azure Data Lake Hola siguientes.

### <a name="built-for-hadoop"></a>Creado para Hadoop
almacén de Azure Data Lake Hello es un sistema de archivos de Apache Hadoop compatible con sistema de archivos de distribuido de Hadoop (HDFS) y funciona con el ecosistema de Hadoop de Hola.  El existente HDInsight aplicaciones o servicios que usan hello WebHDFS API pueden integrar fácilmente en el almacén de Data Lake. Además, el Almacén de Data Lake expone una interfaz de REST compatible con WebHDFS para aplicaciones.

Los datos almacenados en el Almacén de Data Lake se pueden analizar fácilmente mediante marcos analíticos de Hadoop como MapReduce o Hive. Clústeres de HDInsight de Azure de Microsoft se pueden aprovisionar y configurar toodirectly acceder a los datos almacenados en el almacén de Data Lake.

### <a name="unlimited-storage-petabyte-files"></a>Almacenamiento ilimitado, archivos de petabytes de tamaño
El Almacén de Azure Data Lake proporciona almacenamiento ilimitado y es adecuado para almacenar diversos datos para análisis. No se impone ningún límite en tamaños de cuenta, tamaños de archivo o cantidad de Hola de datos que pueden almacenarse en un data lake. Archivos individuales pueden oscilar entre toopetabytes kilobytes de tamaño que realiza una excelente opción toostore cualquier tipo de datos. Datos se almacenan de forma duradera y hace copias en varios y no hay ningún límite en cuanto tiempo Hola para qué hello datos pueden almacenarse en lake de datos de Hola.

### <a name="performance-tuned-for-big-data-analytics"></a>Rendimiento optimizado para el análisis de macrodatos
Almacén de Azure Data Lake se crea para ejecutar sistemas analíticos que requieren rendimiento masivos tooquery y analizar grandes cantidades de datos de gran escala. lago de datos de Hola propaga partes de un archivo durante un número de servidores de almacenamiento individuales. Esto mejora Hola rendimiento de lectura al leer el archivo de hello en paralelo para realizar análisis de datos.

### <a name="enterprise-ready-highly-available-and-secure"></a>Listo para la empresa: Alta disponibilidad y seguridad
El Almacén de Azure Data Lake proporciona confiabilidad y disponibilidad estándar del sector. Los activos de datos se almacenan de manera duradera mediante la realización de copias redundantes tooguard frente a los errores inesperados. Las empresas pueden usar Azure Data Lake en sus soluciones como parte importante de su plataforma de datos existente.

Almacén de Data Lake también proporciona seguridad de nivel empresarial de los datos de hello almacenado. Para obtener más información, consulte [Protección de los datos almacenados en el Almacén de Azure Data Lake](#DataLakeStoreSecurity).

### <a name="all-data"></a>Todos los datos
El Almacén de Azure Data Lake puede almacenar cualquier dato en su formato nativo, tal cual, sin necesidad de transformarlo antes. Almacén de Data Lake no requieren un toobe esquema definido antes de que se cargan datos hello, dejando los datos de toohello framework analíticos individuales toointerpret hello y definir un esquema en tiempo de Hola de análisis de Hola. Que se va a toostore capaz de archivos de formatos y tamaños arbitrarios hace toohandle de almacén de Data Lake estructurado, datos estructurados y semiestructurados.

Los contenedores de datos de Almacén de Azure Data Lake son básicamente carpetas y archivos. Opera en los datos de hello almacenado mediante el SDK, Portal de Azure y Azure Powershell. Siempre que ponen los datos en el almacén de hello mediante estas interfaces y los contenedores adecuados de Hola, puede almacenar cualquier tipo de datos. Almacén de Data Lake no lleva a cabo ningún control especial de datos basada en el tipo de saludo de datos que almacena.

## <a name="DataLakeStoreSecurity"></a>Protección de los datos en el Almacén de Azure Data Lake
Almacén de Azure Data Lake usa Azure Active Directory para la autenticación y listas de control de acceso (ACL) toomanage acceder a los datos tooyour.

| Característica | Description |
| --- | --- |
| Autenticación |Almacén de Azure Data Lake se integra con Azure Active Directory (AAD) para la administración de identidades y acceso para todos los datos de hello almacenados en el almacén de Azure Data Lake. Como resultado de la integración de hello, ventajas de Azure Data Lake de todas las características AAD, tales como la autenticación multifactor, acceso condicional, el control de acceso basado en roles, supervisión de la utilización en la aplicación, seguridad, supervisión y alertas, etcetera. Almacén de Azure Data Lake admite Hola protocolo OAuth 2.0 para la autenticación con en la interfaz REST de Hola. |
| Control de acceso |Almacén de Azure Data Lake proporciona control de acceso por compatibilidad con los permisos de estilo de POSIX expuestos por hello WebHDFS protocolo. Hola datos Lake almacén Public Preview (versión actual de hello), ACL pueden habilitarse en la carpeta raíz de hello, en las subcarpetas y en archivos individuales. Para más información sobre cómo funcionan las ACL en el contexto de Data Lake Store, consulte [Control de acceso en Data Lake Store](data-lake-store-access-control.md). |
| Cifrado |Almacén de Data Lake también proporciona cifrado para los datos que se almacenan en la cuenta de hello. Especifique la configuración de cifrado de Hola durante la creación de una cuenta de almacén de Data Lake. Puede optar toohave los datos cifrados u optar por sin cifrado. Para obtener más información sobre cómo configuración relacionada con el cifrado de tooprovide, consulte [empezar a trabajar con el almacén de Azure Data Lake con hello Azure Portal](data-lake-store-get-started-portal.md). |

Desea toolearn más sobre la protección de datos de almacén de Data Lake. Siga los vínculos de hello siguientes.

* Para obtener instrucciones sobre cómo toosecure los datos en el almacén de Data Lake, consulte [proteger los datos en el almacén de Azure Data Lake](data-lake-store-secure-data.md).
* ¿Prefiere vídeos? [Vea este vídeo](https://mix.office.com/watch/1q2mgzh9nn5lx) acerca de cómo se almacenan los datos de toosecure en el almacén de Data Lake.

## <a name="applications-compatible-with-azure-data-lake-store"></a>Aplicaciones compatibles con el Almacén de Azure Data Lake
Almacén de Azure Data Lake es compatible con los componentes de origen más abiertos en el ecosistema de Hadoop de Hola. También se integra perfectamente con otros servicios de Azure. Por ello, Almacén de Data Lake es una opción perfecta para sus necesidades de almacenamiento de datos. Siga los vínculos de hello siguientes toolearn más información acerca de cómo puede utilizarse el almacén de Data Lake con los componentes de código abierto, así como otros servicios de Azure.

* Consulte [Abrir aplicaciones Big Data de origen que funcionan con el Almacén de Azure Data Lake](data-lake-store-compatible-oss-other-applications.md) para obtener una lista de aplicaciones de código abierto interoperables con el Almacén de Azure Data Lake.
* Vea [integración con otros servicios de Azure](data-lake-store-integrate-with-other-services.md) toounderstand cómo pueden usarse almacén de Data Lake con otro Azure servicios tooenable una gama más amplia de escenarios.
* Vea [escenarios para usar almacén de Data Lake](data-lake-store-data-scenarios.md) toolearn cómo almacenar toouse Data Lake en escenarios como la introducción de datos, procesamiento de datos, descarga de datos y visualización de los datos.

## <a name="what-is-azure-data-lake-store-file-system-adl"></a>¿Qué es el sistema de archivos de Azure Data Lake Store file system (adl://)?
Almacén de Data Lake son accesibles a través de hello nuevo filesystem, Hola AzureDataLakeFilesystem (adl: / /), en entornos de Hadoop (disponibles con clúster de HDInsight). Las aplicaciones y servicios que utilizan adl: / / son tootake puede aprovechar aún más la optimización del rendimiento que no están actualmente disponibles en WebHDFS. Como resultado, proporciona de almacén de Data Lake Hola flexibilidad tooeither hacer uso un rendimiento óptimo Hola con hello recomendada la opción de usar adl: / / o mantener el código existente por ininterrumpido toouse hello WebHDFS API directamente. HDInsight de Azure aprovecha completamente hello AzureDataLakeFilesystem tooprovide Hola obtener el mejor rendimiento en el almacén de Data Lake.

Puede tener acceso a los datos de uso de almacén de Data Lake de hello `adl://<data_lake_store_name>.azuredatalakestore.net`. Para obtener más información sobre cómo tooaccess Hola datos de almacén de Data Lake hello, consulte [ver las propiedades del programa Hola a los datos almacenan](data-lake-store-get-started-portal.md#properties)

## <a name="how-do-i-start-using-azure-data-lake-store"></a>¿Cómo comenzar a usar el Almacén de Azure Data Lake?
Vea [como introducción al uso del almacén de Data Lake Hola Portal de Azure](data-lake-store-get-started-portal.md), en cómo tooprovision un almacén de Data Lake utilizando Hola Portal de Azure. Una vez que se ha aprovisionado Azure Data Lake, aprenderá cómo toouse ofertas de grandes cantidades de datos, como análisis de Azure Data Lake o HDInsight de Azure con el almacén de Data Lake. También puede crear una cuenta de almacén de Azure Data Lake de un toocreate de aplicación .NET y realizar operaciones como datos de carga, descarga datos, etcetera.

* [Tutorial: Introducción a Análisis de Azure Data Lake mediante el Portal de vista previa de Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Uso de HDInsight de Azure con el Almacén de Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Introducción al Almacén de Azure Data Lake mediante SDK de .NET](data-lake-store-get-started-net-sdk.md)

## <a name="data-lake-store-videos"></a>Vídeos de Almacén de Data Lake
Si prefiere ver vídeos toolearn, almacén de Data Lake proporciona vídeos en una variedad de características.

* [Create an Azure Data Lake Store Account (Creación de una cuenta de Almacén de Azure Data Lake)](https://mix.office.com/watch/1k1cycy4l4gen)
* [Use Hola Explorador de datos tooManage datos de almacén de Azure Data Lake](https://mix.office.com/watch/icletrxrh6pc)
* [Conecte el almacén de análisis de Azure Data Lake tooAzure Data Lake](https://mix.office.com/watch/qwji0dc9rx9k)
* [Access Azure Data Lake Store via Data Lake Analytics](https://mix.office.com/watch/1n0s45up381a8)
* [Conecte el almacén de Azure HDInsight tooAzure Data Lake](https://mix.office.com/watch/l93xri2yhtp2)
* [Access Azure Data Lake Store via Hive and Pig (Acceso a Almacén de Azure Data Lake con Análisis a través de Hive and Pig)](https://mix.office.com/watch/1n9g5w0fiqv1q)
* [Usar DistCp (copia de distribuido de Hadoop) toocopy datos tooand de almacén de Azure Data Lake](https://mix.office.com/watch/1liuojvdx6sie)
* [Usar Apache Sqoop toomove datos entre orígenes relacionales y almacén de Azure Data Lake](https://mix.office.com/watch/1butcdjxmu114)
* [Data Orchestration using Azure Data Factory for Azure Data Lake Store (Orquestación de datos mediante Azure Data Factory para el Almacén de Azure Data Lake)](https://mix.office.com/watch/1oa7le7t2u4ka)
* [Proteger los datos en el almacén de Azure Data Lake Hola](https://mix.office.com/watch/1q2mgzh9nn5lx)

