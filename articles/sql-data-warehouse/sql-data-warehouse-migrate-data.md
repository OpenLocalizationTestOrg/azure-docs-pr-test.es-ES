---
title: aaaMigrate el almacenamiento de datos de datos tooSQL | Documentos de Microsoft
description: Sugerencias para migrar el almacenamiento de datos SQL de datos tooAzure para desarrollar soluciones.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a>Migración de los datos
Se pueden mover datos de distintos orígenes a Almacenamiento de datos SQL con diversas herramientas.  Copia de ADF y SSIS, bcp pueden ser utilizado tooachieve este objetivo. Sin embargo, a medida que aumenta la cantidad de Hola de datos debería pensar en dividir el proceso de migración de datos de hello en pasos. Esta opción proporciona Hola oportunidad toooptimize cada paso para obtener un rendimiento y de resistencia tooensure una migración de datos sin problemas.

En primer lugar, este artículo describe escenarios de migración simple de Hola de copia de ADF, SSIS y bcp. A continuación, busque un poco más en cómo se puede optimizar la migración de Hola.

## <a name="azure-data-factory-adf-copy"></a>Copia de Factoría de datos de Azure (ADF)
[Copia de ADF][ADF Copy] forma parte de [Azure Data Factory][Azure Data Factory]. Puede usar tooexport ADF copia los archivos de tooflat de datos que reside en el almacenamiento local, archivos sin formato tooremote mantienen en el almacenamiento de blobs de Azure o directamente en el almacén de datos SQL.

Si los datos se inicia en archivos planos, primero deberá tootransfer se tooAzure blob de almacenamiento antes de iniciar una carga en el almacén de datos SQL. Una vez que se transfieren datos de hello en el almacenamiento de blobs de Azure puede elegir toouse [ADF copia] [ ADF Copy] nuevo toopush datos hello en almacenamiento de datos de SQL.

PolyBase también proporciona una opción de alto rendimiento para cargar los datos de Hola. Sin embargo, eso significa tener que usar dos herramientas en lugar de una. Si necesita obtener el mejor rendimiento de hello, a continuación, usar PolyBase. Si desea una experiencia única herramienta (y datos de hello no son masivos) ADF es la respuesta.


> 
> 

Principal sobre toohello artículo para algunos great siguiente [ejemplos ADF][ADF samples].

## <a name="integration-services"></a>Servicios de integración
Integration Services (SSIS) es una herramienta eficaz y flexible de extracción, transformación y carga de datos (ETL) que admite varias opciones de carga de datos, flujos de trabajo complejos y transformación de datos. Usar SSIS toosimply transferencia datos tooAzure o como parte de una migración más amplia.

> [!NOTE]
> SSIS puede exportar tooUTF-8 sin marca de orden de bytes de hello en el archivo hello. tooconfigure esto primero debe usar Hola derivar datos de caracteres de columna componente tooconvert hello en Hola página de códigos de datos flujo toouse Hola 65001 UTF-8. Una vez que se han convertido columnas hello, Hola datos toohello archivos planos destino adaptador asegurar que la escritura que 65001 también se ha seleccionado como página de códigos de hello para el archivo hello.
> 
> 

SSIS conecta tooSQL almacenamiento de datos tal y como conectaría tooa implementación de SQL Server. Sin embargo, las conexiones tendrá toobe mediante un administrador de conexiones de ADO.NET. También debe tener cuidado para hello tooconfigure "Use inserción masiva cuando esté disponible" rendimiento de toomaximize de configuración. Consulte toohello [adaptador de destino de ADO.NET] [ ADO.NET destination adapter] más información acerca de esta propiedad de artículo toolearn

> [!NOTE]
> No se admite la conexión tooAzure almacenamiento de datos SQL mediante OLE DB.
> 
> 

Además, siempre hay posibilidad de Hola que un paquete puede producir un error debido a problemas de red o toothrottling. Paquetes de diseño, por lo que se puedan reanudar en punto de Hola de error, sin rehacer de trabajo que se complete antes de error de Hola.

Para obtener más información, consulte hello [documentación SSIS][SSIS documentation].

## <a name="bcp"></a>bcp
bcp es una utilidad de línea de comandos que se ha diseñado para la importación y exportación de datos de archivos planos. Puede producirse alguna transformación durante la exportación de datos. transformaciones simples tooperform utilizar una consulta tooselect y transforman datos de Hola. Una vez exportado, a continuación, se pueden cargar archivos planos Hola directamente en la base de datos de almacenamiento de datos SQL de hello destino Hola.

> [!NOTE]
> A menudo resulta una Hola de tooencapsulate conveniente exportación las transformaciones que se usa durante los datos en una vista de sistema de origen de Hola. Esto garantiza que se conserva la lógica de Hola y Hola proceso es repetible.
> 
> 

Las ventajas de bcp son:

* Simplicidad. se toobuild simple y ejecutarán comandos de bcp
* Proceso de carga reiniciable. Carga una vez exportado Hola pueden ejecutar un número ilimitado de veces

Las limitaciones de bcp son:

* bcp solo funciona con archivos planos tabulados. No funciona con archivos, como xml o JSON.
* Capacidades de transformación de datos son de solo copia intermedia de exportación de toohello limitado y son de naturaleza simples
* bcp no ha sido adaptado toobe sólida cuando Hola de cargar datos en internet. Cualquier inestabilidad en la red puede provocar un error de carga.
* bcp se basa en el esquema Hola estén presentes en la carga de toohello anteriores de base de datos de destino de Hola

Para obtener más información, consulte [usar datos de tooload de bcp en almacenamiento de datos de SQL][Use bcp tooload data into SQL Data Warehouse].

## <a name="optimizing-data-migration"></a>Optimización de migración de datos
Un proceso de migración de datos SQLDW puede dividirse eficazmente en tres pasos independientes:

1. Exportación de datos de origen
2. Transferencia de datos tooAzure
3. Cargar en la base de datos de hello destino SQLDW

Cada paso puede ser individualmente optimizado toocreate un proceso de migración sólido, podrá volver a iniciar y flexible que maximiza el rendimiento en cada paso.

## <a name="optimizing-data-load"></a>Optimización de carga de datos
Examinando estos en orden inverso durante un momento; datos de tooload de manera más rápidos de saludo están a través de PolyBase. Optimizar para un proceso de carga de PolyBase coloca los requisitos previos en hello pasos anteriores por lo que es mejor toounderstand esto por adelantado. Son las siguientes:

1. Codificación de archivos de datos
2. Formato de archivos de datos
3. Ubicación de archivos de datos

### <a name="encoding"></a>Codificación
PolyBase requiere toobe de archivos de datos UTF-8 o UTF-16FE. 



### <a name="format-of-data-files"></a>Formato de archivos de datos
PolyBase exige un terminador de fila fijo de \n o una línea nueva. Los archivos de datos deben cumplir toothis estándar. No hay ninguna restricción sobre terminadores de columna o de cadena.

Tendrá toodefine todas las columnas en el archivo hello como parte de la tabla externa en PolyBase. Asegúrese de que todas las columnas exportadas son necesarias y que los tipos de Hola ajustan toohello necesario estándares.

Por favor, consulte toohello [migrar el esquema] artículo para obtener detalles sobre los tipos de datos admitidos.

### <a name="location-of-data-files"></a>Ubicación de archivos de datos
Almacenamiento de datos de SQL utiliza datos de tooload de PolyBase de almacenamiento de blobs de Azure exclusivamente. Por lo tanto, los datos de hello deben primero transferidos en el almacenamiento de blobs.

## <a name="optimizing-data-transfer"></a>Optimización de transferencia de datos
Uno de los elementos más lentas de Hola de migración de datos es la transferencia de Hola de hello tooAzure de datos. No solo el ancho de banda de red puede ser un problema, sino que la confiabilidad de la red también puede dificultar seriamente el progreso. De forma predeterminada tooAzure migración de datos es sobre Hola internet tan Hola posibilidades de errores de transferencia que se producen es bastante probable. Sin embargo, estos errores pueden requerir volver a enviar en su totalidad o en parte de toobe de datos.

Afortunadamente tiene varias velocidad de opciones tooimprove hello y resistencia de este proceso:

### <a name="expressrouteexpressroute"></a>[ExpressRoute][ExpressRoute]
Puede que desee usar tooconsider [ExpressRoute] [ ExpressRoute] toospeed la transferencia de Hola. [ExpressRoute] [ ExpressRoute] proporciona a una conexión privada establecida tooAzure para conexión de hello no pasa por Hola internet pública. No se trata en ningún caso de un paso obligatorio. Sin embargo, mejora el rendimiento al realizar inserciones tooAzure de datos de una implementación local o instalación de colocalización.

ventajas del uso de Hola [ExpressRoute] [ ExpressRoute] son:

1. Mayor confiabilidad
2. Mayor velocidad de red
3. Menor latencia de red
4. Mayor seguridad de red

[ExpressRoute] [ ExpressRoute] es beneficioso para varios escenarios; no solo Hola migración.

¿Le interesa? Para obtener más información y los precios, visite hello [documentación de ExpressRoute][ExpressRoute documentation].

### <a name="azure-import-and-export-service"></a>Servicio Importación/Exportación de Azure
Hello Azure servicio de importación y exportación es un proceso de transferencia de datos diseñado para grandes (GB ++) toomassive (TB ++) las transferencias de datos en Azure. Implica escribir su toodisks de datos y su posterior envío tooan centro de datos de Azure. contenido del disco Hello, a continuación, se cargarán en Blobs de almacenamiento de Azure en su nombre.

Una vista de alto nivel del proceso de exportación de importación de hello es como sigue:

1. Configurar un contenedor de almacenamiento de blobs de Azure tooreceive Hola datos
2. Exportar el almacenamiento de datos toolocal
3. Copiar Hola datos too3.5 pulgadas SATA II/III unidades de disco duro con hello [herramienta de importación y exportación de Azure]
4. Crear un trabajo de importación mediante hello importación de Azure y servicio de exportación que proporciona archivos de diario de hello generados por hello [herramienta de importación y exportación de Azure]
5. Enviar discos de hello su centro de datos de Azure designado
6. Los datos están el contenedor de almacenamiento de blobs de Azure de tooyour transferidos
7. Cargar datos de hello en SQLDW con PolyBase

### <a name="azcopyazcopy-utility"></a>Utilidad [AZCopy][AZCopy]
Hola [AZCopy][AZCopy] utilidad es una herramienta excelente para obtener los datos transferidos a Blobs de almacenamiento de Azure. Está diseñada para pequeñas (MB ++) toovery grandes (GB ++) las transferencias de datos. [AZCopy] también ha sido un buen rendimiento resistente de tooprovide diseñada al transferir datos tooAzure de modo que es una excelente opción para el paso de transferencia de datos de Hola. Una vez transferidos puede cargar datos de hello con PolyBase en almacenamiento de datos de SQL. También puede incorporar AZCopy a los paquetes SSIS con una tarea "Ejecutar proceso".

toouse AZCopy necesitará toodownload e instalarlo primero. Hay una [versión de producción][production version] y una [versión preliminar][preview version] disponibles.

tooupload un archivo desde el sistema de archivos que se necesitará un comando como Hola uno a continuación:

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

Un resumen del proceso general podría ser:

1. Configurar un contenedor de almacenamiento de Azure blob tooreceive Hola datos
2. Exportar el almacenamiento de datos toolocal
3. Los datos en el contenedor de almacenamiento de blobs de Azure de hello AZCopy
4. Cargar datos de hello en almacenamiento de datos de SQL con PolyBase

Documentación completa disponible: [AZCopy][AZCopy].

## <a name="optimizing-data-export"></a>Optimización de exportación de datos
Además tooensuring que exportación Hola cumple requisitos toohello dispuestos PolyBase puede buscar también exportación de hello toooptimize Hola proceso de datos tooimprove Hola aún más.



### <a name="data-compression"></a>Compresión de datos
PolyBase puede leer datos comprimidos con gzip. Si es capaz de toocompress que los archivos de datos toogzip, a continuación, se minimizará la cantidad de Hola de datos que se va a insertar en la red de Hola.

### <a name="multiple-files"></a>Varios archivos
Dividir las tablas grandes en varios archivos no solo ayuda a tooimprove exportar velocidad, también ayuda a con transferencia re-startability y Hola facilidad de uso general de los datos de hello una vez en el almacenamiento de blobs de Azure de Hola. Uno de hello muchas características "nice" de PolyBase es que se leen todos los archivos de hello dentro de una carpeta y tratarlo como una tabla. Por lo tanto es archivos de hello tooisolate una buena idea para cada tabla en su propia carpeta.

PolyBase también admite una característica conocida como "cruce de carpetas recursivo". Puede utilizar esta característica toofurther mejorar la organización de Hola de los datos exportados tooimprove la administración de datos.

toolearn más información acerca de la carga de datos con PolyBase, consulte [datos de uso PolyBase tooload en almacenamiento de datos de SQL][Use PolyBase tooload data into SQL Data Warehouse].

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de la migración, consulte [migrar el almacenamiento de datos de solución tooSQL][Migrate your solution tooSQL Data Warehouse].
Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
