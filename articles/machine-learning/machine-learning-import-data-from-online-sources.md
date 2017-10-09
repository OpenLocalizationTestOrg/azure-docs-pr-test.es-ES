---
title: "datos de aaaImport en estudio de aprendizaje automático de orígenes de datos en línea | Documentos de Microsoft"
description: "¿Cómo tooimport los datos de entrenamiento estudio de aprendizaje automático de Azure de varios orígenes en línea."
keywords: "importar datos, formato de datos, tipos de datos, orígenes de datos, datos de entrenamiento"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 701b93fe-765b-4d15-a1cf-9b607f17add6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: aae6907cdd0b4dc373ae08c2569caa276c198b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-azure-machine-learning-studio-from-various-online-data-sources-with-hello-import-data-module"></a>Importar datos en estudio de aprendizaje automático de Azure de varios orígenes de datos en línea con el módulo de importación de datos de Hola
Este artículo describe la compatibilidad de hello para la importación de datos en línea de varios orígenes e información de hello necesaria toomove datos de estos orígenes en un experimento de aprendizaje automático de Azure.

> [!NOTE]
> Este artículo proporciona información general sobre hello [importar datos] [ import-data] módulo. Para obtener más información acerca de los tipos de Hola de datos puede tener acceso, formatos y parámetros, respuestas toocommon preguntas, vea el tema de referencia de módulo de Hola para hello [importar datos] [ import-data] módulo.
> 
> 

<!-- -->

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

## <a name="introduction"></a>Introducción
Mediante el uso de hello [importar datos] [ import-data] módulo, se pueden tener acceso a datos de uno de varios orígenes de datos en línea mientras se está ejecutando el experimento [estudio de aprendizaje automático de Azure](https://studio.azureml.net/Home):

* Una dirección URL web con HTTP
* Hadoop con HiveQL
* Almacenamiento de blobs de Azure
* Tabla de Azure
* Base de datos SQL de Azure o SQL Server en máquina virtual de Azure
* La base de datos de SQL Server local
* Un proveedor de fuentes de datos, actualmente OData
* Azure CosmosDB (anteriormente denominado DocumentDB)

tooaccess orígenes de datos en línea en el experimento Studio, agregar hello [importar datos] [ import-data] tooyour de módulo, seleccione hello **origen de datos**y, a continuación, proporcionar parámetros de hello necesarios tooaccess Hola datos. orígenes de datos en línea Hello compatibles se detallan en tabla Hola siguiente. Esta tabla también resumen los formatos de archivo de Hola que son compatibles y parámetros que son utilizados tooaccess Hola datos.

Tenga en cuenta que, como a estos datos de entrenamiento se tiene acceso mientras se está ejecutando el experimento, solo están disponibles en ese experimento. En comparación, los datos que se ha almacenado en un módulo de conjunto de datos son experimento tooany disponible en el área de trabajo.

> [!IMPORTANT]
> Actualmente, Hola [importar datos] [ import-data] y [exportar datos] [ export-data] módulos pueden leer y escribir datos solo del almacenamiento de Azure creado mediante Hola Modelo de implementación clásica. En otras palabras, Hola nuevo tipo de cuenta de almacenamiento de blobs de Azure que ofrece una capa de acceso de almacenamiento activa o capa de acceso de almacenamiento frío aún no se admite. 
> 
> Por lo general, las cuentas de almacenamiento de Azure que podría haber creado antes de que esta opción de servicio estuviera disponible no deberían verse afectadas. 
> Si necesita toocreate una nueva cuenta, seleccione **clásico** para hello implementación de modelo, o use el Administrador de recursos y seleccione **de propósito General** en lugar de **almacenamiento de blobs** para **Cuenta kind**. 
> 
> Para obtener más información, consulte [Capas de almacenamiento de acceso frecuente y acceso esporádico](../storage/blobs/storage-blob-storage-tiers.md).
> 
> 

## <a name="supported-online-data-sources"></a>Orígenes de datos en línea admitidos
Aprendizaje automático de Azure **importar datos** módulo admite los siguientes orígenes de datos de hello:

| Origen de datos | Description | Parámetros |
| --- | --- | --- |
| Dirección URL web a través de HTTP |Lee datos en valores separados por comas (CSV), valores separados por tabulaciones (TSV), formato de archivo de atributo-relación (ARFF) y formatos de máquinas de vectores de soporte (SVM-light), desde cualquier dirección URL web que use HTTP |<b>Dirección URL</b>: especifica el nombre completo del archivo de hello, incluida la dirección URL del sitio de Hola y nombre de archivo de hello, con cualquier extensión de Hola. <br/><br/><b>Formato de datos</b>: especifica uno de los datos de hello admitida formatos: CSV, TSV, ARFF o svmlight. Si los datos de hello tienen una fila de encabezado, es tooassign usa nombres de columna. |
| Hadoop/HDFS |Lee datos de almacenamiento distribuido de Hadoop. Especificar datos de Hola que desee con HiveQL, un lenguaje de consulta similar a SQL. HiveQL también puede ser usado tooaggregate datos y filtrarlos antes de agregar datos de hello tooMachine estudio de aprendizaje. |<b>Consulta de base de datos de Hive</b>: especifica la consulta de Hive hello usa datos de hello toogenerate.<br/><br/><b>URI del servidor de HCatalog </b> : nombre de hello especificado del clúster con el formato de hello  *&lt;el nombre del clúster&gt;. azurehdinsight.net.*<br/><br/><b>Nombre de cuenta de usuario de Hadoop</b>: especifica la cuenta de usuario de Hadoop de hello nombre usa el clúster de hello tooprovision.<br/><br/><b>Contraseña de cuenta de usuario de Hadoop</b> : especifica hello las credenciales utilizadas al aprovisionar el clúster de Hola. Para más información, consulte [Creación de clústeres de Hadoop en HDInsight](../hdinsight/hdinsight-provision-clusters.md).<br/><br/><b>Ubicación de los datos de salida</b>: Especifica si los datos de Hola se almacenan en un sistema de archivos distribuido de Hadoop (HDFS) o en Azure. <br/><ul>Si almacena datos de salida en HDFS, especifique URI del servidor HDFS Hola. (Estar seguro de nombre de clúster de HDInsight de hello toouse sin prefijo de hello HTTPS://). <br/><br/>Si almacena los datos de salida en Azure, debe especificar el nombre de cuenta de almacenamiento de Azure de hello, tecla de acceso de almacenamiento y el nombre del contenedor de almacenamiento.</ul> |
| Base de datos SQL |Lee los datos almacenados en una base de datos SQL Azure o en una base de datos SQL Server que se ejecuta en una máquina virtual de Azure. |<b>Nombre del servidor de base de datos</b>: especifica Hola nombre del servidor de hello en qué Hola se ejecuta la base de datos.<br/><ul>En el caso de base de datos de SQL Azure escriba el nombre del servidor de Hola que se genera. Normalmente tiene forma de hello  *&lt;generated_identifier&gt;. database.windows.net.* <br/><br/>En el caso de un servidor SQL Server hospedado en una máquina virtual de Azure, escriba *tcp:&lt;nombre DNS de la máquina virtual&gt;, 1433*</ul><br/><b>Nombre de base de datos </b>: especifica el nombre de Hola de base de datos de hello en el servidor de Hola. <br/><br/><b>Nombre de cuenta de usuario de servidor</b>: especifica un nombre de usuario para una cuenta que tenga permisos de acceso de la base de datos de Hola. <br/><br/><b>Contraseña de cuenta de usuario de servidor</b>: especifica la contraseña de hello para la cuenta de usuario de Hola.<br/><br/><b>Aceptar cualquier certificado de servidor</b>: Utilice esta opción (menos segura) si desea tooskip revisar certificado de sitio de hello antes de leer los datos.<br/><br/><b>Consulta de base de datos</b>: escriba una instrucción SQL que describe datos de Hola que desee tooread. |
| SQL Database local |Lee los datos que se almacenan en una instancia de SQL Database local. |<b>Puerta de enlace de datos</b>: especifica el nombre de Hola de hello Data Management Gateway instalado en un equipo donde puede tener acceso a la base de datos de SQL Server. Para obtener información acerca de cómo configurar la puerta de enlace de hello, consulte [realizar análisis avanzados con aprendizaje automático de Azure utilizando los datos de un servidor local de SQL](machine-learning-use-data-from-an-on-premises-sql-server.md).<br/><br/><b>Nombre del servidor de base de datos</b>: especifica Hola nombre del servidor de hello en qué Hola se ejecuta la base de datos.<br/><br/><b>Nombre de base de datos </b>: especifica el nombre de Hola de base de datos de hello en el servidor de Hola. <br/><br/><b>Nombre de cuenta de usuario de servidor</b>: especifica un nombre de usuario para una cuenta que tenga permisos de acceso de la base de datos de Hola. <br/><br/><b>Nombre de usuario y contraseña</b>: haga clic en <b>escriba valores</b> tooenter sus credenciales de base de datos. Puede usar la autenticación integrada de Windows o la autenticación de SQL Server según la configuración de SQL Server local.<br/><br/><b>Consulta de base de datos</b>: escriba una instrucción SQL que describe datos de Hola que desee tooread. |
| tabla de Azure |Lee datos de hello servicio tabla de almacenamiento de Azure.<br/><br/>Si lee grandes cantidades de datos con poca frecuencia, utilice Hola servicio tabla de Azure. Proporciona una solución de almacenamiento flexible, no relacional (No SQL), escalable a gran escala, económica y de alta disponibilidad. |Hola opciones Hola **importar datos** cambian en función de si se accede a información pública o a una cuenta de almacenamiento privado que requiere credenciales de inicio de sesión. Esto viene determinado por hello <b>tipo de autenticación</b> que puede tener el valor de "PublicOrSAS" o "Account", cada uno de los cuales tiene su propio conjunto de parámetros. <br/><br/><b>Pública o firma de acceso compartido (SAS) URI</b>: Hola parámetros son:<br/><br/><ul><b>URI de la tabla</b>: especifica Hola público o dirección URL de SAS para la tabla de Hola.<br/><br/><b>Especifica hello tooscan de filas para los nombres de propiedad</b>: Hola valores son <i>TopN</i> tooscan Hola especifica el número de filas, o <i>ScanAll</i> tooget todas las filas de tabla de Hola. <br/><br/>Si los datos de hello son homogéneos y predecibles, se recomienda que seleccione *TopN* y escriba un número para N. Para las tablas grandes, esto puede producir en los tiempos de lectura más rápidas.<br/><br/>Si los datos de hello están estructurados con conjuntos de propiedades que varían en función de profundidad de Hola y la posición de la tabla de hello, elija hello *ScanAll* opción tooscan todas las filas. Esto garantiza la integridad de saludo de la propiedad resultante y la conversión de metadatos.<br/><br/></ul><b>Cuenta de almacenamiento privado</b>: Hola parámetros son: <br/><br/><ul><b>Nombre de la cuenta</b>: especifica Hola nombre de cuenta de hello que contenga Hola tabla tooread.<br/><br/><b>Clave de cuenta</b>: especifica la clave de almacenamiento de hello asociada con cuenta de hello.<br/><br/><b>Nombre de la tabla</b> : especifica Hola nombre de tabla de Hola que contiene Hola datos tooread.<br/><br/><b>Tooscan de filas para los nombres de propiedad</b>: Hola valores son <i>TopN</i> tooscan Hola especifica el número de filas, o <i>ScanAll</i> tooget todas las filas de tabla de Hola.<br/><br/>Si los datos de hello son homogéneos y predecibles, le recomendamos que seleccione *TopN* y escriba un número para N. Para las tablas grandes, esto puede producir en los tiempos de lectura más rápidas.<br/><br/>Si los datos de hello están estructurados con conjuntos de propiedades que varían en función de profundidad de Hola y la posición de la tabla de hello, elija hello *ScanAll* opción tooscan todas las filas. Esto garantiza la integridad de saludo de la propiedad resultante y la conversión de metadatos.<br/><br/> |
| Almacenamiento de blobs de Azure |Lee los datos almacenados en el servicio de Blob de hello en el almacenamiento de Azure, incluidas imágenes, texto no estructurado o datos binarios.<br/><br/>Puede usar Hola Blob servicio toopublicly exponen datos o tooprivately almacén de datos de la aplicación. Puede tener acceso a los datos desde cualquier lugar a través de conexiones HTTP o HTTPS. |Hola opciones Hola **importar datos** cambio de módulo dependiendo de si se accede a información pública o a una cuenta de almacenamiento privado que requiere credenciales de inicio de sesión. Esto viene determinado por hello <b>tipo de autenticación</b> que puede tener un valor de "PublicOrSAS" o de "Cuenta".<br/><br/><b>Pública o firma de acceso compartido (SAS) URI</b>: Hola parámetros son:<br/><br/><ul><b>URI</b>: especifica Hola público o dirección URL de SAS de blob de almacenamiento de Hola.<br/><br/><b>Formato de archivo</b>: especifica el formato de Hola de datos de Hola Hola servicio Blob. formatos de Hello admitido son CSV, TSV y ARFF.<br/><br/></ul><b>Cuenta de almacenamiento privado</b>: Hola parámetros son: <br/><br/><ul><b>Nombre de la cuenta</b>: especifica Hola nombre de cuenta de hello que contiene datos de blob de hello desea tooread.<br/><br/><b>Clave de cuenta</b>: especifica la clave de almacenamiento de hello asociada con cuenta de hello.<br/><br/><b>Ruta de acceso toocontainer, directorio o blob </b> : especifica Hola nombre del blob de Hola que contiene hello tooread de datos.<br/><br/><b>Formato de archivo BLOB</b>: especifica el formato de Hola de datos de hello en el servicio de blob de Hola. Hello formatos de datos admitidos son CSV, TSV, ARFF, CSV con una codificación especificada y Excel. <br/><br/><ul>Si el formato de hello es CSV o TSV, ser tooindicate seguro de si el archivo hello contiene una fila de encabezado.<br/><br/>Puede usar datos de hello Excel opción tooread libros de Excel. Hola <i>formato de datos de Excel</i> opción, indique si los datos de hello están en un intervalo de hoja de cálculo de Excel o en una tabla de Excel. Hola <i>hoja de Excel o tabla incrustada </i>opción, especifique el nombre de Hola de hoja de Hola o tabla que desee tooread desde.</ul><br/> |
| Proveedor de fuente de distribución de datos |Lee datos de un proveedor de fuente admitido. Formato de Open Data Protocol (OData) Hola actualmente, solo se admite. |<b>Tipo de contenido de datos</b>: especifica el formato de OData de Hola.<br/><br/><b>Dirección URL de origen</b>: especifica la dirección URL completa de Hola para hello fuente de datos. <br/>Por ejemplo, Hola siguientes lecturas de la dirección URL de base de datos de ejemplo de Hola Northwind: http://services.odata.org/northwind/northwind.svc/ |

## <a name="next-steps"></a>Pasos siguientes

[Implementación de servicios web Azure ML que usan módulos de importación y exportación de datos](machine-learning-web-services-that-use-import-export-modules.md)


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C/
