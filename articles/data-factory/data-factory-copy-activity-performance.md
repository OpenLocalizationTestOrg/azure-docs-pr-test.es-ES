---
title: "aaaCopy actividad Guía de rendimiento y optimización | Documentos de Microsoft"
description: "Obtenga información acerca de los factores claves que afectan al rendimiento de Hola de movimiento de datos en Data Factory de Azure cuando se usa la actividad de copia."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 4b9a6a4f-8cf5-4e0a-a06f-8133a2b7bc58
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jingwang
ms.openlocfilehash: b0fb5a76c34752d07e8ddfffbb799a05fb5d6be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-activity-performance-and-tuning-guide"></a>Guía de optimización y rendimiento de la actividad de copia
Copiar actividad de Azure Data Factory ofrece una solución de carga de datos de alto rendimiento fiable y segura de primera clase. Permite toocopy decenas de terabytes de datos cada día en una gran variedad de nube y almacenes de datos local. Rendimiento de carga de datos de ultrarápido están tooensure clave que pueda centrarse en el problema de "big data" hello principal: compilar soluciones de análisis avanzados y obtener información detallada de todos los datos.

Azure proporciona un conjunto de nivel empresarial soluciones de almacenamiento de datos y el almacenamiento de datos y la actividad de copia ofrece una experiencia que resulta fácil tooconfigure y configurar de carga de datos altamente optimizadas. Con solo una actividad de copia, puede conseguir:

* Cargar datos en **Azure SQL Data Warehouse** a **1,2 GBps**. Para un tutorial con un caso de uso, consulte [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carga de 1 TB en Azure SQL Data Warehouse en 15 minutos con Azure Data Factory).
* Cargar datos en **Azure Blob Storage** a **1,0 GBps**
* Cargar datos en **Azure Data Lake Store** a **1,0 GBps**

En este artículo se describe:

* [Los números de referencia de rendimiento](#performance-reference) compatible toohelp de almacenes de datos de origen y el receptor tiene previsto del proyecto.
* Hola de características que pueden mejorar el rendimiento de copia en diversos escenarios, incluidos [unidades de movimiento de datos en la nube](#cloud-data-movement-units), [copia en paralelo](#parallel-copy), y [provisionalmente copia](#staged-copy);
* [Directrices de ajuste de rendimiento](#performance-tuning-steps) en cómo tootune Hola hello y rendimiento claves factores que pueden afectar a copian el rendimiento.

> [!NOTE]
> Si no está familiarizado con la actividad de copia, consulte [Movimiento de datos con la actividad de copia](data-factory-data-movement-activities.md) antes de leer este artículo.
>

## <a name="performance-reference"></a>Referencia de rendimiento

Como referencia, tabla siguiente se muestra hello copia rendimiento número en MBps para hello tiene pares de origen y el receptor basados en las pruebas internas. A efectos de comparación, también muestra cómo distintos valores de [unidades de movimiento de datos de nube](#cloud-data-movement-units) o de [escalabilidad de Data Management Gateway](data-factory-data-management-gateway-high-availability-scalability.md) (varios nodos de puerta de enlace) pueden contribuir al rendimiento de copias.

![Matriz de rendimiento](./media/data-factory-copy-activity-performance/CopyPerfRef.png)


**Toonote puntos:**
* El rendimiento se calcula utilizando Hola siguiente fórmula: [tamaño de los datos leídos del origen] / [duración de la ejecución de actividad de copia].
* números de referencia de rendimiento de Hello en la tabla de Hola se midieron mediante [TPC-H](http://www.tpc.org/tpch/) conjunto de datos en una actividad de copia individual en ejecución.
* En los almacenes de datos de Azure, origen de Hola y el receptor son Hola misma región de Azure.
* Para la copia híbrida entre local y nube almacenes de datos, cada nodo de puerta de enlace se estaba ejecutando en un equipo que estaba independiente Hola local almacén de datos con por debajo de la especificación. Durante la ejecución de una sola actividad de puerta de enlace, operación de copia de hello consume solo una pequeña parte de la máquina de pruebas de hello CPU, memoria o ancho de banda de red. Obtenga más información en [Consideraciones sobre Data Management Gateway](#considerations-for-data-management-gateway).
    <table>
    <tr>
        <td>CPU</td>
        <td>Intel Xeon E5-2660 v2 de 32 núcleos a 2,20 GHz</td>
    </tr>
    <tr>
        <td>Memoria</td>
        <td>128 GB</td>
    </tr>
    <tr>
        <td>Red</td>
        <td>Interfaz de Internet: 10 Gbps; interfaz de intranet: 40 Gbps</td>
    </tr>
    </table>


> [!TIP]
> Puede lograr un mayor rendimiento mediante el aprovechamiento de más unidades de movimiento de datos (DMUs) que Hola predeterminado DMUs máximos, que es 32 para una actividad de copia de nube para ejecutar. Por ejemplo, con 100 DMU, puede copiar datos de Azure Blob a Azure Data Lake Store a una velocidad de **1 GBps**. Vea hello [unidades de movimiento de datos en la nube](#cloud-data-movement-units) sección para obtener más información acerca de esta característica y Hola admite el escenario. Póngase en contacto con [soporte técnico de Azure](https://azure.microsoft.com/support/) toorequest DMUs más.

## <a name="parallel-copy"></a>Copia en paralelo
Puede leer el origen de datos de Hola o escribir el destino de datos toohello **en paralelo en una ejecución de la actividad de copia**. Esta característica mejora el rendimiento de Hola de una operación de copia y reduce el tiempo de hello tarda toomove datos.

Esta configuración es diferente de hello **simultaneidad** propiedad en la definición de actividad de Hola. Hola **simultaneidad** propiedad determina el número de Hola de **se ejecuta la actividad simultánea de copia** tooprocess datos desde windows actividad diferente (1 too2 A.M. AM, ESTOY 2 too3 AM, ESTOY 3 too4 AM, y así sucesivamente). Esta funcionalidad es útil cuando se realiza una carga histórica. capacidad de copia en paralelo de Hola aplica tooa **única de ejecución de actividad**.

Echemos un vistazo a un escenario de ejemplo. En el siguiente ejemplo de Hola, varios sectores de hello último necesitan toobe procesado. Data Factory ejecuta una única instancia de actividad de copia (una ejecución de actividad) para cada segmento:

* segmento de datos de Hola desde la primera ventana de actividad hello (1 too2 AM ESTOY) == > actividad ejecuta 1
* segmento de datos de saludo de la segunda ventana de actividad hello (2 too3 AM ESTOY) == > actividad ejecuta 2
* segmento de datos de saludo de la segunda ventana de actividad hello (3 too4 AM ESTOY) == > actividad ejecuta 3

y así sucesivamente.

En este ejemplo, cuando hello **simultaneidad** se establece el valor too2, **actividad ejecuta 1** y **actividad ejecuta 2** copiar datos desde dos ventanas de la actividad **simultáneamente**  tooimprove rendimiento del movimiento de datos. Sin embargo, si varios archivos están asociados con la actividad de ejecución 1, servicio de movimiento de datos de hello copia archivos desde Hola origen toohello destino archivos a la vez.

### <a name="cloud-data-movement-units"></a>Unidades de movimiento de datos de nube
A **unidad de movimiento de datos en la nube (DMU)** es una medida que representa la potencia de hello (una combinación de asignación de recursos de red, CPU y memoria) de una sola unidad de factoría de datos. Una DMU podría utilizarse en una operación de copia de una nube a otra, pero no en una copia híbrida.

De forma predeterminada, factoría de datos utiliza un tooperform DMU nube solo una única actividad de copia que se ejecute. toooverride este valor predeterminado, especifique un valor para hello **cloudDataMovementUnits** propiedad tal como se indica a continuación. Para obtener información sobre el nivel de Hola de ganancia de rendimiento podría obtener cuando se configura más unidades para un origen de copia específica y el receptor, vea hello [referencia de rendimiento](#performance-reference).

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "cloudDataMovementUnits": 32
        }
    }
]
```
Hola **valores permitidos** para hello **cloudDataMovementUnits** propiedad son 1 (valor predeterminado), 2, 4, 8, 16, 32. Hola **número real de nube DMUs** que la operación de copia de Hola se utiliza en tiempo de ejecución es igual tooor menor que valor Hola configurado, dependiendo de su modelo de datos.

> [!NOTE]
> Si necesita más DMU de nube para aumentar el rendimiento, póngase en contacto con el [servicio técnico de Azure](https://azure.microsoft.com/support/). Configuración de 8 y versiones posteriores actualmente sólo funcionan cuando se **copiar varios archivos de Blob almacenamiento/almacén de Data Lake/Amazon S3/nube FTP/nube SFTP tooBlob almacenamiento o almacén de Data Lake/SQL Azure base de datos SQL**.
>

### <a name="parallelcopies"></a>parallelCopies
Puede usar hello **parallelCopies** paralelismo de hello tooindicate de propiedad que desea que la actividad de copia toouse. Esta propiedad se puede considerar como número máximo de Hola de subprocesos dentro de la actividad de copia que se puede leer desde el origen o escribir tooyour receptor los almacenes de datos en paralelo.

Para cada ejecución de actividad de copia, factoría de datos determina el número de Hola de paralelo copia toouse toocopy datos de almacén de datos de origen de Hola y almacén de datos de destino de toohello. número predeterminado de Hola de copias en paralelo que utiliza depende de tipo de Hola de origen y receptor que está usando.  

| Origen y receptor | Recuento predeterminado de copias en paralelo determinado por servicio |
| --- | --- |
| Copia de datos entre almacenes basados en archivos (Blob Storage, Data Lake Store, Amazon S3, un sistema de archivos local, un HDFS local) |Entre 1 y 32. Depende de tamaño de Hola de archivos de Hola y número de Hola de unidades de movimiento de datos en la nube (DMUs) toocopy usa datos entre dos almacenes de datos en la nube o configuración física de Hola de Hola máquina de puerta de enlace que se usa para obtener una copia híbrida (toocopy datos tooor desde un almacén de datos local ). |
| Copiar los datos de **tooAzure el almacenamiento de tabla de almacén de los datos de origen** |4 |
| Todos los demás pares de origen y receptor |1 |

Por lo general, el comportamiento predeterminado de hello debe darle mejor rendimiento de Hola. Sin embargo, hello toocontrol cargar en equipos que hospedan los almacenes de datos o el rendimiento de la copia de tootune, puede elegir toooverride Hola valor predeterminado y especifique un valor para hello **parallelCopies** propiedad. Hola valor debe ser entre 1 y 32 (ambos inclusive). En tiempo de ejecución para un rendimiento óptimo hello, actividad de copia utiliza un valor que es menor o igual valor toohello que establezca.

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "parallelCopies": 8
        }
    }
]
```
Toonote puntos:

* Para copiar datos entre almacenes basados en archivos, Hola **parallelCopies** determinar paralelismo hello en nivel de archivo Hola. Hola fragmentación dentro de un único archivo sucedería debajo de forma automática y transparente, y está diseñada toouse Hola mejor adecuado tamaño del fragmento de para un almacén de datos de origen dada escriba datos tooload en paralelo y ortogonal tooparallelCopies. número real de Hola de hello datos movimiento servicio utiliza para la operación de copia de hello en tiempo de ejecución no está más de número de Hola de archivos que tiene copias en paralelo. Si es el comportamiento de la copia de hello **mergeFile**, actividad de copia no se puede aprovechar las ventajas de paralelismo de nivel de archivo.
* Cuando se especifica un valor para hello **parallelCopies** propiedad, considere la posibilidad de aumento de carga de hello en los almacenes de datos de origen y el receptor y toogateway si es una copia híbrida. Esto sucede especialmente cuando haya varias actividades o las ejecuciones simultáneas de hello mismas actividades que se ejecutan contra Hola mismo almacén de datos. Si observa que el almacén de datos de Hola o puerta de enlace se desborda con carga hello, disminuir hello **parallelCopies** carga de valor toorelieve Hola.
* Al copiar los datos de almacenes que no están toostores basados en archivos que están basados en archivos, servicio de movimiento de datos de hello omite hello **parallelCopies** propiedad. Aunque se especifica el paralelismo, no se aplica en este caso.

> [!NOTE]
> Debe usar Hola de Data Management Gateway versión 1.11 o posterior toouse **parallelCopies** característica al hacer una copia híbrida.
>
>

toobetter estas dos propiedades y tooenhance el rendimiento de movimiento de datos, consulte hello [casos de uso de ejemplo](#case-study-use-parallel-copy). No es necesario tooconfigure **parallelCopies** tootake aprovechar el comportamiento predeterminado de Hola. Si configura **parallelCopies** y lo hace en un valor demasiado pequeño, es posible que varias DMU de nube no se utilicen completamente.  

### <a name="billing-impact"></a>Impacto en la facturación
Tiene **importante** tooremember que se le cobra según el tiempo total de Hola de operación de copia de Hola. Si un trabajo de copia usa una hora de tootake con una unidad de una nube y ahora se tarda 15 minutos con cuatro unidades en la nube, hello general sigue siendo de factura casi Hola igual. Por ejemplo, va a utilizar cuatro unidades de nube. la primera unidad de la nube de Hello invierte en 10 minutos, Hola una tercera, 5 minutos, hello una segunda, 10 minutos y Hola una cuarta, 5 minutos, todo en una ejecución de actividad de copia. Se le cobra por hora de hello copia total (movimiento de datos), que es de 10 + 10 + 5 + 5 = 30 minutos. El uso de **parallelCopies** no afecta a la facturación.

## <a name="staged-copy"></a>copia almacenada provisionalmente
Cuando se copian datos desde un almacén de datos de origen datos almacén tooa receptor, puede elegir el almacenamiento de blobs de toouse como una ubicación de almacenamiento provisional almacenamiento provisional. Almacenamiento provisional es especialmente útil en hello casos siguientes:

1. **Desea que los datos de tooingest de varios almacenes de datos en almacenamiento de datos de SQL a través de PolyBase**. Almacenamiento de datos de SQL utiliza PolyBase como un tooload de mecanismo de alto rendimiento una gran cantidad de datos en almacenamiento de datos de SQL. Sin embargo, los datos de origen de hello deben estar en el almacenamiento de blobs y debe cumplir criterios adicionales. Al cargar datos desde un almacén de datos distinto de Almacenamiento de blobs, puede activar la copia de datos mediante el Almacenamiento de blobs provisional. En ese caso, factoría de datos realiza Hola requerido datos transformaciones tooensure que cumpla los requisitos de Hola de PolyBase. A continuación, utiliza datos de PolyBase tooload en almacenamiento de datos de SQL. Para obtener más información, consulte [datos de uso PolyBase tooload en almacenamiento de datos de SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse). Para un tutorial con un caso de uso, consulte [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carga de 1 TB en Azure SQL Data Warehouse en 15 minutos con Azure Data Factory).
2. **A veces se tarda un tiempo tooperform un movimiento de datos híbridos (es decir, toocopy entre un almacén de datos local y un almacén de datos en la nube) a través de una conexión de red lenta**. tooimprove rendimiento, puede comprimir Hola datos de forma local para que se tarda menos tiempo de almacén de datos de almacenamiento provisional de toomove datos toohello en la nube de Hola. A continuación, puede descomprimir los datos de Hola Hola almacén de almacenamiento provisional antes de cargarlos en el almacén de datos de destino de Hola.
3. **No desea tooopen puertos excepto el puerto 80 y el puerto 443 en el firewall, debido a las directivas de TI corporativas**. Por ejemplo, cuando se copian datos desde un receptor de base de datos de SQL Azure local tooan de almacén de datos o un receptor de almacenamiento de datos de SQL Azure, necesita tooactivate de comunicación de TCP saliente en el puerto 1433 para firewall de Windows hello y del firewall corporativo. En este escenario, aprovechar las ventajas de hello puerta de enlace toofirst copia datos tooa Blob almacenamiento provisional instancia sobre HTTP o HTTPS en el puerto 443. A continuación, cargar datos de hello en base de datos SQL o almacenamiento de datos SQL desde el almacenamiento provisional de almacenamiento de blobs. En este flujo, no necesita tooenable el puerto 1433.

### <a name="how-staged-copy-works"></a>Funcionamiento de las copias almacenadas provisionalmente
Al activar la característica de almacenamiento provisional de hello, primero los datos Hola se copian desde el almacén de datos de hello origen toohello almacén de datos de almacenamiento provisional (aportar su propia). A continuación, los datos de Hola se copian desde el almacén de datos de receptor de toohello de almacén de datos de almacenamiento provisional de Hola. Factoría de datos administra automáticamente el flujo de dos fases de Hola para usted. Factoría de datos también limpia los datos temporales de hello ensayo almacenamiento una vez completado el movimiento de datos Hola.

En caso de copia de hello en la nube (origen y receptor de datos almacenes están en la nube de hello), no se utiliza la puerta de enlace. Hola servicio factoría de datos realiza las operaciones de copia de Hola.

![Copias almacenadas provisionalmente: escenario de modelo en la nube](media/data-factory-copy-activity-performance/staged-copy-cloud-scenario.png)

En escenario de copia de hello híbrido (origen es local y receptor está en la nube de hello), puerta de enlace de hello mueve tooa almacén de datos de almacenamiento provisional del almacén de datos de los datos de origen de Hola. Servicio de factoría de datos se mueve el almacén de datos del receptor de toohello del almacén de datos de almacenamiento provisional de datos de Hola. Copiar datos de un tooan de almacén de datos en la nube local de almacén de datos mediante almacenamiento provisional también es compatible con el flujo de hello invertida.

![Copias almacenadas provisionalmente: escenario de modelo híbrido](media/data-factory-copy-activity-performance/staged-copy-hybrid-scenario.png)

Al activar el movimiento de datos mediante el uso de un almacén de almacenamiento provisional, puede especificar si desea comprimir antes de mover los datos de origen de Hola y almacén de datos provisionales de tooan o almacén de datos de almacenamiento provisional, a continuación, se descomprimen antes de mover datos desde una versión preliminar de hello datos toobe o almacén de datos del receptor de toohello de almacén de datos de almacenamiento provisionales.

Actualmente, no se pueden copiar datos entre dos almacenes de datos locales mediante almacenamiento provisional. Esperamos que este toobe opción disponible pronto.

### <a name="configuration"></a>Configuración
Configurar hello **enableStaging** configuración de toospecify de actividad de copia si desea Hola datos toobe provisionalmente en almacenamiento de blobs antes de cargarlos en un almacén de datos de destino. Al establecer **enableStaging** tooTRUE, especificar propiedades adicionales de hello enumerados en la tabla siguiente Hola. Si no tiene uno, también deberá toocreate un almacenamiento de Azure o almacenamiento compartido servicio vinculado de firma de acceso para el almacenamiento provisional.

| Propiedad | Description | Valor predeterminado | Obligatorio |
| --- | --- | --- | --- |
| **enableStaging** |Especifique si desea que toocopy datos a través de un provisional almacén de almacenamiento provisional. |False |No |
| **linkedServiceName** |Especificar nombre de Hola de un [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) o [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) servicio, que hace referencia la instancia de toohello de almacenamiento que usan como una ubicación de almacenamiento provisional ensayo vinculado. <br/><br/> No se puede usar almacenamiento con un dato de tooload de firma de acceso compartido en almacenamiento de datos de SQL a través de PolyBase. Puede usarlo en todos los demás casos. |N/D |Sí, cuando **enableStaging** se establece tooTRUE |
| **path** |Especifique la ruta de almacenamiento de blobs de Hola que desea que los datos de hello provisionalmente toocontain. Si no se proporciona una ruta de acceso, el servicio de hello crea un contenedor toostore los datos temporales. <br/><br/> Especifique una ruta de acceso solo si usar almacenamiento con una firma de acceso compartido, o si necesita toobe de datos temporales en una ubicación específica. |N/D |No |
| **enableCompression** |Especifica si se deben comprimir los datos antes de que se copian toohello destino. Esta configuración reduce el volumen de Hola de datos que se transfieren. |False |No |

Aquí es una definición de ejemplo de actividad de copia con propiedades de Hola que se describen en la tabla anterior de hello:

```json
"activities":[  
{
    "name": "Sample copy activity",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDBOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlSink"
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob",
            "path": "stagingcontainer/path",
            "enableCompression": true
        }
    }
}
]
```

### <a name="billing-impact"></a>Impacto en la facturación
Los cargos que se le realizan se basan en dos elementos: duración de la copia y tipo de copia.

* Cuando se usa durante la copia de nube (copiar datos desde un almacén de datos en la nube datos almacén tooanother en la nube), de almacenamiento provisional se cargan Hola [suma de la duración de la copia de los pasos 1 y 2] x [precio de unidad de copia de nube].
* Cuando se usa almacenamiento provisional durante la copia híbrida (copiar datos desde un almacén de datos local datos almacén tooa en la nube), se le cobra por [duración de la copia híbrida] x [precio por unidad copia híbrida] + [duración de la copia en la nube] x [precio de unidad de copia de nube].

## <a name="performance-tuning-steps"></a>Pasos de optimización del rendimiento
Se recomienda que realice estos pasos rendimiento de hello tootune del servicio en la factoría de datos con la actividad de copia:

1. **Establezca una línea base**. Durante la fase de desarrollo de hello, probar la canalización mediante el uso de actividad de copia en una muestra representativa de datos. Puede usar hello factoría de datos [segmentación modelo](data-factory-scheduling-and-execution.md) cantidad de hello toolimit de datos, trabajar con.

   Recopilar tiempo de ejecución y características de rendimiento mediante hello **supervisión y administración de aplicaciones**. Elija **Supervisión y administración** en la página de inicio de Data Factory. En la vista de árbol de hello, elija hello **conjunto de datos de salida**. Hola **Windows actividad** elija Hola de ejecución de la actividad de copia. **Ventanas de la actividad** muestra la duración de la actividad de copia de Hola y el tamaño de Hola de datos de Hola que se copian. rendimiento de Hello aparece en **Explorer de la ventana de actividad**. toolearn más información acerca de la aplicación hello, consulte [supervisar y administrar las canalizaciones de factoría de datos de Azure mediante el uso de Hola supervisión y administración de aplicaciones](data-factory-monitor-manage-app.md).

   ![Detalles de ejecución de actividad](./media/data-factory-copy-activity-performance/mmapp-activity-run-details.png)

   Más adelante en el artículo de hello, puede comparar el rendimiento de Hola y la configuración del su escenario tooCopy actividad [referencia de rendimiento](#performance-reference) de nuestras pruebas.
2. **Diagnostique y optimice el rendimiento**. Si observa de rendimiento de hello no cumple sus expectativas, deberá tooidentify cuellos de botella de rendimiento. A continuación, optimizar el rendimiento tooremove o reducir el efecto de Hola de cuellos de botella. Una descripción completa de diagnóstico de rendimiento es más allá del ámbito de Hola de este artículo, pero estas son algunas consideraciones comunes:

   * Características de rendimiento:
     * [Copia paralela](#parallel-copy)
     * [Unidades de movimiento de datos de nube](#cloud-data-movement-units)
     * [Copias almacenadas provisionalmente](#staged-copy)
     * [Escalabilidad de Data Management Gateway](data-factory-data-management-gateway-high-availability-scalability.md)
   * [Data Management Gateway](#considerations-for-data-management-gateway)
   * [Origen](#considerations-for-the-source)
   * [Sink](#considerations-for-the-sink)
   * [Serialización y deserialización](#considerations-for-serialization-and-deserialization)
   * [Compresión](#considerations-for-compression)
   * [Asignación de columnas](#considerations-for-column-mapping)
   * [Otras consideraciones](#other-considerations)
3. **Expanda el conjunto de datos completo de hello configuración tooyour**. Cuando esté satisfecho con el rendimiento y resultados de la ejecución de hello, puede expandir la definición de Hola y toocover período activo de canalización de todo el conjunto de datos.

## <a name="considerations-for-data-management-gateway"></a>Consideraciones sobre Data Management Gateway
**El programa de instalación de puerta de enlace**: le recomendamos que use un toohost máquina dedicada Data Management Gateway. Vea [Consideraciones sobre el uso de Data Management Gateway](data-factory-data-management-gateway.md#considerations-for-using-gateway).  

**Supervisión de la puerta de enlace y la escala-vertical u horizontalmente**: una sola puerta de enlace lógica con uno o más nodos de puerta de enlace puede servir varias actividades de copia se ejecuta en hello mismo tiempo al mismo tiempo. Puede ver instantánea casi en tiempo real de la utilización de recursos (CPU, memoria, network(in/out), etc.) en un equipo de puerta de enlace así como ver el número de Hola de trabajos simultáneos frente a Hola portal de Azure, el límite de [puerta de enlace de Monitor en el portal de hello](data-factory-data-management-gateway.md#monitor-gateway-in-the-portal). Si tiene necesidad de mucha en movimiento de datos híbridos con gran número de ejecuciones de actividad de copia simultánea o con gran volumen de datos toocopy, considere la posibilidad de demasiado[escalar en horizontal como puerta de enlace](data-factory-data-management-gateway-high-availability-scalability.md#scale-considerations) así como toobetter utilizar el recurso o copiar de tooprovision más tooempower de recursos. 

## <a name="considerations-for-hello-source"></a>Consideraciones para el origen de Hola
### <a name="general"></a>General
Asegúrese de que Hola subyacente de almacén de datos no se desborda con otras cargas de trabajo que se ejecutan en o en el mismo.

En los almacenes de datos de Microsoft, consulte [de supervisión y optimización temas](#performance-reference) que son almacenes toodata específico y ayudará a comprender los datos almacenan las características de rendimiento, minimizar los tiempos de respuesta y maximizar el rendimiento.

Si copia datos de almacenamiento de blobs tooSQL almacenamiento de datos, considere el uso de **PolyBase** tooboost rendimiento. Vea [datos de uso PolyBase tooload en almacenamiento de datos de SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) para obtener más información. Para un tutorial con un caso de uso, consulte [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carga de 1 TB en Azure SQL Data Warehouse en 15 minutos con Azure Data Factory).

### <a name="file-based-data-stores"></a>Almacenes de datos basados en archivos
*(Incluye Blob Storage, Data Lake Store, Amazon S3, sistemas de archivos locales y HDFS local)*

* **Tamaño de archivo medio y número de archivos**: la actividad de copia transfiere datos de archivo en archivo. Con hello movido de la misma cantidad de datos toobe, hello el rendimiento global es más bajo si datos Hola consisten de muchos archivos pequeños en lugar de unos pocos archivos grandes debido toohello fase de arranque para cada archivo. Por lo tanto, si es posible, combinar archivos pequeños en mayor rendimiento mayor toogain de archivos.
* **Formato y compresión de archivos**: para más rendimiento tooimprove de formas, vea hello [consideraciones para la serialización y deserialización](#considerations-for-serialization-and-deserialization) y [consideraciones para la compresión](#considerations-for-compression) secciones.
* Para hello **sistema de archivos local** escenario en el que **Data Management Gateway** es requerido, vea hello [consideraciones para Data Management Gateway](#considerations-for-data-management-gateway) sección.

### <a name="relational-data-stores"></a>Almacenes de datos relacionales
*(Incluye SQL Database, SQL Data Warehouse, Amazon Redshift, bases de datos SQL Server y Oracle, MySQL, DB2, Teradata, Sybase y bases de datos PostgreSQL, etc.)*

* **Patrón de datos**: el esquema de tabla afecta al rendimiento de la copia. Un tamaño de fila grande le ofrece un mejor rendimiento que el tamaño de fila pequeños, toocopy Hola la misma cantidad de datos. motivo de Hello es que esa base de datos de hello puede recuperar más eficazmente menos lotes de datos que contienen menos filas.
* **Consulta o procedimiento almacenado**: optimizar Hola la lógica de consulta de Hola o procedimiento almacenado que especifique en los datos de toofetch de origen de actividad de copia de hello más eficazmente.
* Para **bases de datos relacionales local**, como SQL Server y Oracle, que requieren el uso de Hola de **Data Management Gateway**, vea hello [consideraciones para Data Management Gateway](#considerations-on-data-management-gateway) sección.

## <a name="considerations-for-hello-sink"></a>Consideraciones para el receptor de Hola
### <a name="general"></a>General
Asegúrese de que Hola subyacente de almacén de datos no se desborda con otras cargas de trabajo que se ejecutan en o en el mismo.

En los almacenes de datos de Microsoft, consulte demasiado[de supervisión y optimización temas](#performance-reference) que son almacenes de toodata específico. Estos temas pueden ayudarle a entender las características de rendimiento de almacén de datos y cómo el tiempo de respuesta de toominimize y maximizar el rendimiento.

Si va a copiar datos de **almacenamiento de blobs** demasiado**almacenamiento de datos SQL**, considere el uso de **PolyBase** tooboost rendimiento. Vea [datos de uso PolyBase tooload en almacenamiento de datos de SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) para obtener más información. Para un tutorial con un caso de uso, consulte [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carga de 1 TB en Azure SQL Data Warehouse en 15 minutos con Azure Data Factory).

### <a name="file-based-data-stores"></a>Almacenes de datos basados en archivos
*(Incluye Blob Storage, Data Lake Store, Amazon S3, sistemas de archivos locales y HDFS local)*

* **Copiar comportamiento**: si se copian datos desde un almacén de datos basados en archivos diferentes, actividad de copia tiene tres opciones a través de hello **copyBehavior** propiedad. Conserva la jerarquía, aplana la jerarquía o combina archivos. Conservar o eliminar la estructura de jerarquía tiene poca o ninguna sobrecarga de rendimiento, pero combinar archivos hace tooincrease sobrecarga de rendimiento.
* **Formato y compresión de archivos**: vea hello [consideraciones para la serialización y deserialización](#considerations-for-serialization-and-deserialization) y [consideraciones para la compresión](#considerations-for-compression) secciones para más rendimiento tooimprove de formas .
* **Almacenamiento de blobs**: actualmente, Almacenamiento de blobs solo admite blobs en bloques para optimizar la transferencia de datos y el rendimiento.
* Para **sistemas de archivos local** escenarios que requieren el uso de Hola de **Data Management Gateway**, vea hello [consideraciones para Data Management Gateway](#considerations-for-data-management-gateway) sección.

### <a name="relational-data-stores"></a>Almacenes de datos relacionales
*(Incluye SQL Database, SQL Data Warehouse, bases de datos SQL Server y bases de datos Oracle)*

* **Copiar comportamiento**: según propiedades de Hola que ha establecido para **sqlSink**, actividad de copia escribe la base de datos de destino de toohello de datos de maneras diferentes.
  * De forma predeterminada, Hola datos movimiento servicio usa datos de tooinsert Hola API de copia masiva en modo append, que proporciona Hola obtener el mejor rendimiento.
  * Si configura un procedimiento almacenado en el receptor de hello, base de datos de Hola aplica a una fila de datos de Hola a la vez en lugar de como una carga masiva. El rendimiento disminuye considerablemente. Si el conjunto de datos es grande, cuando sea aplicable, considere la posibilidad de hello toousing **sqlWriterCleanupScript** propiedad.
  * Si configura hello **sqlWriterCleanupScript** ejecutar propiedad para cada actividad de copia, los desencadenadores de servicio de Hola Hola script y, a continuación, utilizar datos de saludo API de copia masiva tooinsert Hola. Por ejemplo, toooverwrite Hola toda la tabla con datos más recientes de hello, puede especificar un script toofirst eliminar todos los registros antes de nuevos datos de carga masiva Hola de origen de Hola.
* **Patrón de datos y tamaño de lote**:
  * El esquema de tabla afecta al rendimiento de la copia. toocopy Hola la misma cantidad de datos, un tamaño de fila grande proporciona mejor rendimiento que un tamaño de fila pequeños porque la base de datos de hello más eficazmente puede confirmar menos lotes de datos.
  * La actividad de copia inserta datos en una serie de lotes. Puede establecer Hola número de filas en un lote mediante el uso de hello **valor writeBatchSize** propiedad. Si los datos tienen filas pequeño, puede establecer hello **valor writeBatchSize** propiedad con un toobenefit de valor superior de la sobrecarga de lote menor y mayor rendimiento. Si el tamaño de fila de Hola de los datos es grande, tenga cuidado al aumentar **valor writeBatchSize**. Un valor alto podría provocar el error de copia tooa mediante la sobrecarga de la base de datos de Hola.
* Para **bases de datos relacionales local** , como SQL Server y Oracle, que requieren el uso de Hola de **Data Management Gateway**, vea hello [consideraciones para Data Management Gateway](#considerations-for-data-management-gateway) sección.

### <a name="nosql-stores"></a>Almacenes NoSQL
*(Incluye Table Storage y Azure Cosmos DB)*

* Para **Almacenamiento de tablas**:
  * **Partición**: escribir particiones de datos toointerleaved drásticamente degrada el rendimiento. Ordenar los datos de origen por la clave de partición para que los datos de Hola se insertan eficazmente en una partición después de otro, o ajustar Hola lógica toowrite Hola datos tooa única partición.
* Para **Azure Cosmos DB**:
  * **Tamaño del lote**: Hola **valor writeBatchSize** propiedad establece el número de Hola de las solicitudes paralelas documentos de toocreate de servicio de base de datos de Azure Cosmos toohello. Puede esperar un rendimiento mejor al aumentar **valor writeBatchSize** porque más de las solicitudes paralelas se envían tooAzure Cosmos DB. Sin embargo, espere a que la limitación cuando se escribe tooAzure Cosmos DB (mensaje de error de hello es "Solicitud velocidad es grande"). Varios factores pueden provocar una limitación, incluido el tamaño del documento, número de Hola de términos en documentos de hello y Hola directiva de indexación de la colección de destino. tooachieve un mayor rendimiento de copia, considere el uso de una colección mejor, por ejemplo, S3.

## <a name="considerations-for-serialization-and-deserialization"></a>Consideraciones sobre serialización y deserialización
La serialización y deserialización pueden tener lugar cuando el conjunto de datos de entrada o el conjunto de datos de salida es un archivo. Consulte [Formatos de archivo y de compresión admitidos](data-factory-supported-file-and-compression-formats.md) con detalles sobre los formatos de archivo que admite la actividad de copia.

**Comportamiento de copia**:

* Al copiar archivos entre almacenes de datos basados en archivos:
  * Cuando los conjuntos de datos de entrada y salidos tienen no Hola igual o ninguna configuración de formato de archivo, servicio de movimiento de datos de Hola ejecuta una copia binaria sin necesidad de serialización o deserialización. Verá un escenario de toohello de rendimiento en comparación con mayor, en qué Hola configuración de formato de archivo de origen y el receptor es diferente entre sí.
  * Cuando la entrada y conjuntos de datos de salida ambos están en formato de texto y la codificación de hello solo tipo es iguales, servicio de movimiento de datos de hello sólo realiza la conversión de codificación. Todavía no hace ninguna serialización y deserialización, lo que produce una sobrecarga del rendimiento en comparación con copia binaria tooa.
  * Cuando la entrada y salidos conjuntos de datos ambos tienen distintos formatos de archivo o distintas configuraciones, como delimitadores, Hola servicio de movimiento de datos deserializa toostream de datos de origen, transformación y, a continuación, serializarlo en formato de salida de hello indicada. Esta operación produce una sobrecarga de rendimiento mucho más significativo en comparación con los escenarios de tooother.
* Si copia los archivos a/desde un almacén de datos que no está basado en archivos (por ejemplo, desde un almacén relacional de almacén basado en archivo tooa), el paso de serialización o deserialización de hello es necesario. Este paso produce una sobrecarga considerable sobre el rendimiento.

**Formato de archivo**: formato de archivo de Hola que elija puede afectar al rendimiento de la copia. Por ejemplo, Avro es un formato binario compacto que almacena metadatos con datos. Tiene una amplia compatibilidad con en el ecosistema de Hadoop de hello para el procesamiento y la consulta. Sin embargo, Avro es más cara para la serialización y deserialización, los resultados de menor rendimiento de copia en comparación con formato tootext. Realice su elección del formato de archivo a lo largo de hello flujo de procesamiento completo. Comenzar con los datos de formulario Hola se almacenan en y del origen de almacenes de datos o toobe extraídos de sistemas externos; Hola mejor formato de almacenamiento, procesamiento analítico y consultar; y en qué formato se deben exportar datos de hello en puestos de datos para herramientas de informes y visualización. En ocasiones, un formato de archivo que no es óptimo para leer y escribir el rendimiento podría ser una buena elección cuando considere Hola general analíticos proceso.

## <a name="considerations-for-compression"></a>Consideraciones sobre la compresión
Cuando el conjunto de datos de entrada o de salida es un archivo, puede establecer la actividad de copia tooperform compresión y descompresión tal y como escribe el destino de toohello de datos. Si elige compresión, está buscando el equilibrio entre entrada/salida (E/S) y CPU. La compresión de datos de hello supone un costo adicional en recursos de proceso. Pero, a cambio, se reduce la E/S de red y el almacenamiento. Según los datos, puede que observe un aumento en el rendimiento general de la actividad de copia.

**Códec**: la actividad de copia admite los tipos de compresión gzip, bzip2 y Deflate. HDInsight de Azure puede consumir los tres tipos de procesamiento. Cada códec de compresión tiene sus ventajas. Por ejemplo, bzip2 tiene rendimiento de copia más bajo de hello, pero obtendrá Hola Hive consulta un rendimiento óptimo con bzip2 porque se puede dividir para su procesamiento. Gzip es la opción de hello más equilibrada, y se utiliza con más frecuencia Hola. Elija un códec de Hola que mejor se adapte a su escenario de extremo a extremo.

**Nivel:**para cada códec de compresión, puede elegir entre dos opciones: compresión más rápida y compresión más óptima. Hello más rápido comprimido opción comprime datos Hola lo más rápido posible, incluso si el archivo resultante de hello no se comprime un rendimiento óptimo. Hello óptimamente comprimido opción emplea más tiempo en la compresión y da como resultado una cantidad mínima de datos. Puede probar ambas toosee de opciones que proporciona un mejor rendimiento global en su caso.

**Una consideración**: toocopy una gran cantidad de datos entre un almacén local y la nube de hello, considere el uso de almacenamiento de blobs provisional con la compresión. Uso de almacenamiento provisional es útil cuando ancho de banda de saludo de la red corporativa y los servicios de Azure es el factor de limitación de Hola y desea conjunto de datos de entrada de Hola y datos de salida establecen ambos toobe en formato sin comprimir. En concreto, puede dividir una única actividad de copia en dos. Hola copia actividad copia primero desde provisionales de tooan de origen de Hola o blob de almacenamiento provisional en un formato comprimido. segunda actividad de copia de Hello copia datos de hello comprimido de almacenamiento provisional y, a continuación, descomprime mientras escribe toohello receptor.

## <a name="considerations-for-column-mapping"></a>Consideraciones sobre la asignación de columnas
Puede establecer hello **columnMappings** propiedad en todos los toomap de actividad de copia o un subconjunto de hello columnas de salida de toohello de columnas de entrada. Después de que el servicio de movimiento de datos de hello lee datos de Hola de origen de hello, necesita tooperform de asignación de columna en los datos de hello antes de escribir Hola datos toohello receptor. Este procesamiento adicional reduce la capacidad de proceso de la copia.

Si el almacén de datos de origen es consultable, por ejemplo, si se trata de un almacén relacional como base de datos SQL o SQL Server, o si es un almacén NoSQL como almacenamiento de tabla o base de datos de Azure Cosmos, considere la posibilidad de insertar el filtrado de columnas de Hola y la reordenación de lógica toohello **consulta**  propiedad en lugar de usar la asignación de columna. De esta manera, proyección de Hola se produce mientras el servicio de movimiento de datos de hello lee el almacén de datos de los datos de origen de hello, donde resulta mucho más eficaz.

## <a name="other-considerations"></a>Otras consideraciones
Si hello el tamaño de datos que desee toocopy es grande, puede ajustar los datos de hello business lógica toofurther partición mediante Hola mecanismo la segmentación de factoría de datos. A continuación, programar la actividad de copia toorun con más frecuencia ejecutar de tamaño de los datos tooreduce Hola para cada actividad de copia.

Tener cuidado al número de Hola de conjuntos de datos y las actividades de copia que requieren la factoría de datos tooconnector toohello mismo almacén de datos en hello mismo tiempo. Muchos de los trabajos de copia concurrente podrían limitar un almacén de datos y provocar toodegraded rendimiento, copie reintentos interno del trabajo y en algunos casos, errores de ejecución.

## <a name="sample-scenario-copy-from-an-on-premises-sql-server-tooblob-storage"></a>Escenario de ejemplo: copia desde un almacenamiento de tooBlob de SQL Server local
**Escenario**: una canalización se compila toocopy datos desde un almacenamiento de tooBlob de SQL Server local en formato CSV. toomake Hola trabajo de copia con mayor rapidez, se deben comprimir archivos CSV de hello en formato del bzip2.

**Prueba y análisis**: rendimiento de Hola de actividad de copia es inferior a 2 MBps, que es mucho más lenta que las pruebas comparativas de rendimiento de Hola.

**Análisis de rendimiento y optimización**: tootroubleshoot Hola problema de rendimiento, echemos un vistazo a cómo se procesa y se mueven datos Hola.

1. **Leer datos**: puerta de enlace abre un tooSQL conexión del servidor y envía Hola consulta. SQL Server responde enviando hello tooGateway de flujo de datos a través de la intranet de Hola.
2. **Serializar y comprimir los datos**: puerta de enlace serializa el formato de tooCSV de flujo de datos de Hola y comprime Hola flujo de datos tooa bzip2.
3. **Escribir datos**: puerta de enlace de carga de almacenamiento con tooBlob Hola bzip2 secuencias a través de Internet de Hola.

Como puede ver, datos de Hola se va a procesar y mover de forma secuencial streaming: SQL Server > LAN > puerta de enlace > WAN > almacenamiento de blobs. **Hello el rendimiento general está determinado por rendimiento mínimo de Hola a través de la canalización de hello**.

![flujo de datos](./media/data-factory-copy-activity-performance/case-study-pic-1.png)

Uno o varios de hello siguiendo los factores que podrían provocar cuello de botella de rendimiento de Hola.

* **Origen:**el propio SQL Server tiene un rendimiento bajo debido a cargas intensas.
* **Data Management Gateway**
  * **LAN**: puerta de enlace está muy alejado del equipo de SQL Server de Hola y tiene una conexión de ancho de banda bajo.
  * **Puerta de enlace**: puerta de enlace ha alcanzado su Hola de tooperform de limitaciones de carga de las siguientes operaciones:
    * **Serialización**: serializar tooCSV de flujo de datos de hello formato tiene un rendimiento lento.
    * **Compresión**: ha elegido un códec de compresión lenta (por ejemplo, bzip2, a 2,8 MBps con Core i7).
  * **WAN**: ancho de banda de hello entre la red corporativa de Hola y los servicios de Azure es baja (por ejemplo, T1 = 1,544 kbps. T2 = 6,312 kbps).
* **Receptor**: el Almacenamiento de blobs tiene un rendimiento bajo. (Esta situación es improbable porque su SLA garantiza un mínimo de 60 MBps).

En este caso, compresión de datos del bzip2 podría ralentizar canalización todo Hola. Cambiar el códec de compresión gzip tooa podría facilitar este cuello de botella.

## <a name="sample-scenarios-use-parallel-copy"></a>Escenarios de ejemplo: uso de la copia en paralelo
**Escenario I:** copiar 1.000 archivos de 1 MB de almacenamiento de tooBlob del sistema de archivos de hello local.

**Análisis y ajuste del rendimiento**: por ejemplo, si ha instalado la puerta de enlace en un equipo de cuatro núcleos, factoría de datos utiliza 16 copias en paralelo toomove archivos de almacenamiento de tooBlob de sistema de archivos de hello simultáneamente. Esta ejecución en paralelo debe tener como resultado un alto rendimiento. También puede especificar explícitamente Hola recuento de copias en paralelo. Al copiar muchos archivos pequeños, las copias en paralelo ayudan considerablemente al rendimiento al usar los recursos de forma más eficaz.

![Escenario 1.](./media/data-factory-copy-activity-performance/scenario-1.png)

**Escenario II**: copiar 20 blobs de 500 MB de almacenamiento de blobs tooData Lake almacén análisis y, a continuación, ajustar el rendimiento.

**Análisis y ajuste del rendimiento**: en este escenario, factoría de datos copia datos de Hola de almacén de lago de tooData de almacenamiento de blobs mediante el uso de solo copia (**parallelCopies** establecer too1) y las unidades de movimiento de datos en la nube único. Hello rendimiento observa will puede cierre toothat descrito en hello [sección de referencia de rendimiento](#performance-reference).   

![Escenario 2.](./media/data-factory-copy-activity-performance/scenario-2.png)

**Escenario III**: el tamaño de cada archivo es mayor que decenas de MB y el volumen total es grande.

**Análisis y la habilitación de rendimiento**: aumentar **parallelCopies** no genera un mejor rendimiento de copia debido a limitaciones de recursos de hello de una DMU único de la nube. En su lugar, debe especificar en la nube más DMUs tooget más recursos tooperform Hola el movimiento de datos. No especifica un valor para hello **parallelCopies** propiedad. Factoría de datos controla el paralelismo de Hola de. En este caso, si establece **cloudDataMovementUnits** too4, un rendimiento de aproximadamente cuatro veces ocurre.

![Escenario 3.](./media/data-factory-copy-activity-performance/scenario-3.png)

## <a name="reference"></a>Referencia
Estos son supervisión del rendimiento y optimización de referencias para algunos de los almacenes de datos de hello admitida:

* Azure Storage (que incluyeBlob Storage y Table Storage): [Objetivos de escalabilidad de Azure Storage](../storage/common/storage-scalability-targets.md) y [Lista de comprobación de rendimiento y escalabilidad de Azure Storage](../storage/common/storage-performance-checklist.md)
* Base de datos SQL Azure: Puede [supervisar el rendimiento de hello](../sql-database/sql-database-single-database-monitor.md) y comprobar el porcentaje de unidad (DTU) de transacciones de base de datos de Hola
* Almacenamiento de datos SQL de Azure: su capacidad se mide en unidades de almacenamiento de datos (DWU); consulte [Administración de la potencia de proceso en Almacenamiento de datos SQL de Azure (información general)](../sql-data-warehouse/sql-data-warehouse-manage-compute-overview.md)
* Azure Cosmos DB: [Niveles de rendimiento de Azure Cosmos DB](../documentdb/documentdb-performance-levels.md)
* Instancia de SQL Server local: [Supervisión y optimización del rendimiento](https://msdn.microsoft.com/library/ms189081.aspx)
* Servidor de archivos local: [Performance Tuning for File Servers](https://msdn.microsoft.com/library/dn567661.aspx)
